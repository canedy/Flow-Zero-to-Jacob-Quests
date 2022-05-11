1. In words, list 3 reasons why structs are different from resources. Here are some important facts that define resources:
- They cannot be copied
- They cannot be lost (or overwritten)
- They cannot be created whenever you want
- You must be extremely explicit about how you handle a resource (for example, moving them)
- Resources are much harder to deal with

2. Describe a situation where a resource might be better to use than a struct.
- when you don't want a resouce to copied. You want the resource to moved, but only exisit in one place at a time.
- with anything which could potentially represent a valuable digital asset like an NFT we would want to use a resource.

3. What is the keyword to make a new resource?
- `create`

4. Can a resource be created in a script or transaction (assuming there isn't a public function to create one)?
- No, it must be created in a contract only.

5. What is the type of the resource below?
- it is a resource of type Jacob

6. find 4 things wrong in code below

`pub fun createJacob(): Jacob {` // you need a `@` symbol. **correction: @Jacob**
  
  `let myJacob = Jacob()` // You to need to use the `<-` move operator and create a new resource. **correction: let myJacob <- create Jacob()**
  
  `return myJacob` // can to move that digital resource. **correction: return <- myJacob**

`}`
