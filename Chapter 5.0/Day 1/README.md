1. Describe what an event is, and why it might be useful to a client.
   - You can use this to emit information based on your contract's actions. You can use this to communicate important, and I guess, even unimportant events to the outside world. You can use events to communicate to a log file for compliance activities are 3rd party tools such as Splunk.  

2. Deploy a contract with an event in it, and emit the event somewhere else in the contract indicating that it happened. Using the contract in step 2), add some pre conditions and post conditions to your contract to get used to writing them out.
   - I added comments //----> next to both event, precondition, postcondition that were implemented.

	   ```swift
       access(all) contract Library {

        //----> event that a room has been booked
        access(all) event StudyRoomBooked(_roomName: String)

        access(all) resource interface IRoomPublic {
          access(all) var roomName: String
        }

        access(all) resource StudyRoom: IRoomPublic {

          access(all) var roomName: String
          access(all) var roomAvailable: Bool
          access(all) var roomHasMedia: Bool

          access(all) fun bookRoom(_roomName: String): Bool {

            //----> Check to make sure room is available before booking
            pre {
              self.roomAvailable == false
            }

            //----> Check to see if the request room has media equipment available
            post {
              result true
            }

            self.roomAvailable = true

            //----> emit that the event happened
            emit StudyRoomBooked(_roomName: _roomName)

            if self.roomHasMedia == true {
              return true
            } else {
              return false
            }

          }

          init(_roomName: String) {
            self.roomAvailable = false
            self.roomName = _roomName
            self.roomHasMedia = false
          }
        }

        access(all) fun createStudyRoom(_roomName: String): @StudyRoom {
          return <- create StudyRoom(_roomName: _roomName)
        }

        init() {}

       }
     ```

3. For each of the functions below (numberOne, numberTwo, numberThree), follow the instructions.
   - numberOne: This would pass
   - numberTwo: pre would pass, post would pass
   - numberThree: I think it would fail. It feels like the `self.number` will always be 1 more than the current `self.number` value. It feels like it will keep resetting itself to 0
