1. Explain what lives inside of an account.
   - All accounts have storage, as we learned in the lesson. The storage has a path with a domain and identifier structure. The valid domains are /storage/, /public/, and /private/

2. What is the difference between the /storage/, /public/, and /private/ paths?
   - The /storage/ - Only the account owner has access to stored objects
   - The /public/ - Anyone has access to objects
   - The /private/ - Only folks that the contract account owner allows can access the storage. 

3. What does .save() do? What does .load() do? What does .borrow() do?
   - .save() - Save an object to account /storage/ domain
   - .load() - Loads an object from accout /storage/ domain
   - .borrow() - Returns a reference from storage without removing it from the accounts /storage/ domain.

4. Explain why we couldn't save something to our account storage inside a script.
   - Jacob, you know this answer. Scripts can't modify state.

5. Explain why I couldn't save something to your account.
   - Well, because it's my account. No one has access to save directly to your account storage. Only the `AuthAccount` has that ability. 

6. Define a contract that returns a resource that has at least 1 field in it. Then, write 2 transactions:
   - A transaction that first saves the resource to account storage, then loads it out of account storage, logs a field inside the resource, and destroys it.

    ```
    import Weather from 0x03

    transaction() {

        prepare(acct: AuthAccount) {
            let weatherResourceSave <- Weather.createWeather()
            acct.save(<- weatherResourceSave, to: /storage/myWeather)
            log("You have created and saved new weather resouce to account storage")

            let weatherResourceLoad <- acct.load<@Weather.WeatherResource>(from: /storage/myWeather)
                                        ?? panic("Storage domain not found")
            log("is it cold: ")
            log(weatherResourceLoad.isCold)
            destroy weatherResourceLoad

        }

        execute {

        }

    }
    ```

   - A transaction that first saves the resource to account storage, then borrows a reference to it, and logs a field inside the resource.

    ```
    import Weather from 0x03

    transaction() {

        prepare(acct: AuthAccount) {
            let weatherResourceSave <- Weather.createWeather()
            acct.save(<- weatherResourceSave, to: /storage/myWeather)
            log("You have created and saved new weather resouce to account storage")

            let weatherResourceBorrow = acct.borrow<&Weather.WeatherResource>(from: /storage/myWeather)
                                        ?? panic("Storage domain not found")
            log("is it cold: ")
            log(weatherResourceBorrow.isCold)
        }

        execute {

        }

    }
    ```
