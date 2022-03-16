1. What does "force casting" with as! do? Why is it useful in our Collection? 
   - It will downcast a generic type to a more specific type. In our Collection, this is important because it will take the NonFungibleToken contract NFT resource and downcast it to our contract NFT resource.

2. What does auth do? When do we use it?
   - This is something you use for references when downcasting or upcasting them. My take is if you want access to the attribute or function that the reference is being downcasted or upcasted to, you need to use the 'auth' ( Authorized reference ). First, move the generic type with the `auth,` then move the specific type with the `as!`

3. This last quest will be your most difficult yet. Take this contract:

    **Contract**
    ```
    import NonFungibleToken from 0x02
    pub contract CryptoPoops: NonFungibleToken {
      ...
      pub resource interface ICollectionPublic {
        pub fun deposit(token: @NonFungibleToken.NFT)
        pub fun getIDs(): [UInt64]
        pub fun borrowAuthNFT(id: UInt64): &NFT
      }
      ...
      pub resource Collection: NonFungibleToken.Provider, NonFungibleToken.Receiver, NonFungibleToken.CollectionPublic, ICollectionPublic {
      ...
        pub fun borrowAuthNFT(id: UInt64): &NFT {
          let ref = &self.ownedNFTs[id] as auth &NonFungibleToken.NFT
          return ref as! &NFT
        }
      ...
      }
      ...
    }

    ```
    
    **Transaction: Set up Account**
    ```
    import CryptoPoops from 0x01

    transaction {

        prepare(acct: AuthAccount) {
            acct.save(<- CryptoPoops.createEmptyCollection(), to: /storage/Collection)
            acct.link<&CryptoPoops.Collection{CryptoPoops.ICollectionPublic}>(/public/Collection, target: /storage/Collection)
        }

        execute {
            log("Collection created for account")
        }
    }
    ```
    
    **Transaction: Mint NFT**
    ```
    import CryptoPoops from 0x01

    transaction(name: String, favouriteFood: String, luckyNumber: Int) {

        prepare(acct: AuthAccount) {
            let minter = acct.borrow<&CryptoPoops.Minter>(from: /storage/Minter)
                         ?? panic("This accoutn is not the one who deployed the contract")

            let signersCollection = acct.borrow<&CryptoPoops.Collection>(from: /storage/Collection)
                                ?? panic("Signer does not have a CryptoPoops Collection")

            let nft <- minter.createNFT(name: name, favouriteFood: favouriteFood, luckyNumber: luckyNumber)

            signersCollection.deposit(token: <- nft)
        }

        execute {
            log("NFT minted in accounts collection")
        }

    }
    ```
    
    **Script: Read metadata**
    ```
    import CryptoPoops from 0x01

    pub fun main(address: Address, id: UInt64) {

      let publicCollection = getAccount(address).getCapability(/public/Collection)
                              .borrow<&CryptoPoops.Collection{CryptoPoops.ICollectionPublic}>()
                              ?? panic("The address does not have a colleciton.")

      let nftRef: &CryptoPoops.NFT = publicCollection.borrowAuthNFT(id: id)

      log(nftRef.name)
      log(nftRef.favouriteFood)
      log(nftRef.luckyNumber)
    }    
    ```


