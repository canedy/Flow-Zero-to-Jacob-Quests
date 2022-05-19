variable

**a**
- read ：1, 2, 3, 4
- write ：1, 2, 3, (4) - because it's a script, so you can't write there. It's a trick question

**b**
- read ：1, 2, 3, 4
- write ：1

**c**
- read ：1, 2, 3
- write ：1

**d**
- read ：1
- write ：1

function

**publicFunc**
callable ：1, 2, 3, 4

**contractFunc**
callable ：1, 2, 3

**privateFunc**
callable ：1



# Area 1
```
pub fun structFunc() {
    /**************/
    /*** AREA 1 ***/
    /**************/

    // pub(set) var A           - Can read and write
    // pub var B                - Can read and write
    // access(contract) var C   - Can read and write
    // access(self) var D       - Can read and write

    // pub fun publicFunc()                 - can be called
    // access(contract) fun contractFunc()  - can be called
    // access(self) fun privatefunc()       - can be called

}
```
# Area 2
```
pub fun resourceFunc() {
    /**************/
    /*** AREA 2 ***/
    /**************/

    // pub(set) var A           - Can read and write
    // pub var B                - Can read and write
    // access(contract) var C   - Can read and write
    // access(self) var D       - None

    // pub fun publicFunc()                 - can be called
    // access(contract) fun contractFunc()  - can be called
    // access(self) fun privatefunc()       - No
}
```
# Area 3
```
pub fun questsAreFun() {
    /**************/
    /*** AREA 3 ****/
    /**************/

    // pub(set) var A           - Can read and write
    // pub var B                - Can read and write
    // access(contract) var C   - Can read and write
    // access(self) var D       - None

    // pub fun publicFunc()                 - can be called
    // access(contract) fun contractFunc()  - can be called
    // access(self) fun privatefunc()       - No
}
```
# Area 4
```
pub fun main() {
  /**************/
  /*** AREA 4 ***/
  /**************/

  // pub(set) var A           - Can read 
  // pub var B                - Can read 
  // access(contract) var C   - None
  // access(self) var D       - None

  // pub fun publicFunc()                 - can be called
  // access(contract) fun contractFunc()  - No
  // access(self) fun privatefunc()       - No
}
```
