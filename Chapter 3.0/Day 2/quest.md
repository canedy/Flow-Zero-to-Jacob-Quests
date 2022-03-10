1. Write your own smart contract that contains two state variables: an array of resources, and a dictionary of resources. Add functions to remove and add to each of them. They must be different from the examples above.

```
pub contract TodoList {

    pub var tasksArray: @[Task]
    pub var tasksDictionary: @{UInt64: Task}

    pub resource Task {
        pub let id: UInt64
        pub let action: String
        
        init(_id: UInt64, _action: String) {
            self.id = _id
            self.action = _action
        }
    }

    // function to add or remove if using array

    pub fun addTaskArray(id: UInt64, action: String) {
        let newTask <- create TodoList.Task(id, action)
        self.tasksArray.append(<- newTask)

    }

    pub fun removeTaskArray(id: UInt64): @Task {
        return <- self.tasksArray.remove(at: id)
    }

    // functions to add or remove if using a Dictonary

    pub fun addTaskDictionary(id: UInt64, action: String) {
       let newTask <- create TodoList.Task(id, action)
       self.tasksDictionary[id] <-! newTask
    }

    pub fun removeTaskDictionary(id: UInt64): @Task {
        let removeTask <- self.tasksDictionary.remove(key: id) ?? panic("Could not remove task based on id")
        return <- removeTask
    }


    init() {
        self.tasksArray <- []
        self.tasksDictionary <- {}
    }
}
```

