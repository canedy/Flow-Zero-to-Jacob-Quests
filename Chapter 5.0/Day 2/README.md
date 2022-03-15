1. Explain why standards can be beneficial to the Flow ecosystem.
   - Like any system, standards allow one to expect the same outcome regardless of how things are implemented. It lowers the learning curve for the developer. The developer knows that it works the same and has been audited by the community. No matter where you are in the world, everyone understands the following symbols and how to interact with them. 🛑, 🚦. Fundamentally that is what having a contract standard does.

2. What is YOUR favourite food?
   -	Everything. :-) I'm going to go with meatloaf and mash potatoes. 

3. Please fix this code (Hint: There are two things wrong):

   - In the contract interface, when you have a resource interface, you have to implement the interface on the resource. 
      ```typescript
      pub contract interface ITest {
      ...
      pub resource Stuff: ITest {
      ...
      }
      ...
      }
      ```

   - In the implementing contract, you need to reference the interface as follows. 
      ```typescript
      pub contract Test: ITest {
      ...
      }
      ```

    - In the implemented contract, you can remove the `pub resource interface IStuff` and make sure they implement the contract interface IStuff as follows. 
      ```typescript
      ...
      pub resource Stuff: ITest.IStuff {
      ...
      }
      ```

