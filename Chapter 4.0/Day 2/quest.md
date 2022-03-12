1. What does .link() do?
   - .link() - This allows you to create capabilities for an authorized account.

2. In your own words (no code), explain how we can use resource interfaces to only expose certain things to the /public/ path.
   - Create a restriction on the resource to allow only the action you want on a function or attribute

3. Deploy a contract that contains a resource that implements a resource interface. Then, do the following:

   ```
    access(all) contract Library {

      access(all) resource interface IRoomPublic {
        access(all) var roomName: String
      }

      access(all) resource StudyRoom: IRoomPublic {

        access(all) var roomName: String
        access(all) var roomAvailable: Bool

        access(all) fun bookRoom(_roomAvailable: Bool) {
          self.roomAvailable = _roomAvailable
        }

        init(_roomName: String) {
          self.roomAvailable = false
          self.roomName = _roomName
        }
      }

      access(all) fun createStudyRoom(_roomName: String): @StudyRoom {
        return <- create StudyRoom(_roomName: _roomName)
      }

      init() {}

    }
   ```
     
   - In a transaction, save the resource to storage and link it to the public with the restrictive interface.
     ```
      import Library from 0x04

        transaction(_roomName: String) {

        prepare(acct: AuthAccount) {
            let studyRoomResourceSave <- Library.createStudyRoom(_roomName: _roomName)
            acct.save(<- studyRoomResourceSave, to: /storage/rooms)
            log("You have created and saved a new study room")

            acct.link<&Library.StudyRoom{Library.IRoomPublic}>(/public/rooms, target: /storage/rooms)
            log("Link to /public/rooms created")

        }

        execute { }

      }
     ```

   - Run a script that tries to access a non-exposed field in the resource interface, and see the error pop up.
     ```
       import Library from 0x04

          pub fun main(address: Address) {

          let publicCapability: Capability<&Library.StudyRoom{Library.IRoomPublic}> = 
              getAccount(address).getCapability<&Library.StudyRoom{Library.IRoomPublic}>(/public/rooms)


          let studyRoomResource: &Library.StudyRoom{Library.IRoomPublic} = publicCapability.borrow() 
                                  ?? panic("Capability does not exist or you don't have rights to it")

          // Error: member of restricted type is not accessible: bookRoom
          studyRoomResource.bookRoom(_roomAvailable: true)

          log("Complete")

      }
     ```

   - Run the script and access something you CAN read from. Return it from the script.
     ```
        import Library from 0x04

          pub fun main(address: Address) {

          let publicCapability: Capability<&Library.StudyRoom{Library.IRoomPublic}> = 
              getAccount(address).getCapability<&Library.StudyRoom{Library.IRoomPublic}>(/public/rooms)


          let studyRoomResource: &Library.StudyRoom{Library.IRoomPublic} = publicCapability.borrow() 
                                ?? panic("Capability does not exist or you don't have rights to it")

          // This work becuase interface allows this restriction
          log(studyRoomResource.roomName)

          log("Complete")

        }     
     ```
