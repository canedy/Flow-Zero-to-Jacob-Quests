1. In a script, initialize an array (that has length == 3) of your favourite people, represented as Strings, and log it.

![image](https://user-images.githubusercontent.com/2507134/157367692-a29e234b-2480-47bc-a67b-51f52087bf83.png)

2. `var favouriteSocialMedia: {String: UInt64} = {"Facebook": 5, "Instagram": 4, "Twitter": 3, "YouTube": 2, "Reddit": 0, "LinkedIn": 1}`

3. Explain what the force unwrap operator `!` - If value returned is a nil it will panic/stop the program.

![image](https://user-images.githubusercontent.com/2507134/157368586-1a342df7-44d5-4d2f-a739-090cd8cb8fe9.png)

4. The errors means that an optional is being passed back when the return is expecting just a type of `String`. You can fix the issue in 1 of 2 ways.
- As we learned in the lesson you can force unwrap the the return value to force it to be a `String` or panic if it is a nil. ex. `return thing[0x03]!`
- You could just update the return value to an optional too. `pub fun main(): String? { ... }`
