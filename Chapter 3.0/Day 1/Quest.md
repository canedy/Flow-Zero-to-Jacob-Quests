1. In words, list 3 reasons why structs are different from resources. 
- They have to be moved or destroyed
- They can't be copied
- The `@` symbol represents a resorce

2. Describe a situation where a resource might be better to use than a struct.
- when you don't want a resouce to copied. You want the resource to moved, but only exisit in one place at a time.

3. What is the keyword to make a new resource?
- `create`

4. Can a resource be created in a script or transaction (assuming there isn't a public function to create one)?
- No, it must be created in a contract only.

5. What is the type of the resource below?
- it is a resource type.

6. find 4 things wrong in code below

`pub fun createJacob(): Jacob {` // you need a `@` symbol. **correction: @Jacob**
  
  `let myJacob = Jacob()` // You to need to use the `<-` move operator and create a new resource. **correction: let myJacob <- create Jacob()**
  
  `return myJacob` // can to move that digital resource. **correction: return <- myJacob**

`}`
