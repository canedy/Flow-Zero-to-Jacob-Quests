# Explain, in your own words, the 2 things resource interfaces can be used for (we went over both in today's content)

- Interfaces allow you to create restrictions around resources. They are required functions and fields that must be implemented in the resources. Interactions with the resource are only allowed for items in the interface.

# Define your own contract

```
pub contract MealPlan {

    pub var plansDictionary: @{String: Plan}

    pub resource interface IPublic {
        //pub fun eat(_time: UInt64)
    }

    pub resource Plan: IPublic {
        pub let timeOfDay: UInt64
        pub let typeOfMeal: String
        pub(set) var fastingPeriod: Bool

        pub fun eat(_time: UInt64) {
            if self.timeOfDay < _time {
                self.fastingPeriod = true
            } else {
                self.fastingPeriod = false
            }
        }

        init(_timeOfDay: UInt64, _typeOfMeal: String, _fastingPeriod: Bool) {
            self.timeOfDay = _timeOfDay
            self.typeOfMeal = _typeOfMeal
            self.fastingPeriod = _fastingPeriod
        }
    }

    pub fun getMealPlanReference(key: String): &Plan {
        return &self.plansDictionary[key] as &Plan
    }

    // No Interface Resource

    pub fun createMealPlanNoInterface(_time: UInt64, _timeOfDay: String) {
        let test: @Plan <-! create Plan(_timeOfDay: 8, _typeOfMeal: "6 Sushi Rolls,", _fastingPeriod: false)
        test.eat(_time: _time)
        self.plansDictionary[_timeOfDay] <-! test
    }

    // Yes Interface Resource

    pub fun createMealPlanYesInterface(_time: UInt64, _timeOfDay: String) {
        let test: @Plan{IPublic} <-! create Plan(_timeOfDay: 8, _typeOfMeal: "6 Sushi Rolls,", _fastingPeriod: false)
        test.eat(_time: _time)
        self.plansDictionary[_timeOfDay] <-! test
    }

    pub fun hasEaten(_time: UInt64, _timeOfDay: String) {
        let value =  &self.plansDictionary[_timeOfDay] as &Plan
        value.eat(_time: _time)
    }

    init() {
        self.plansDictionary <- {
            "Monday": <- create Plan(_timeOfDay: 8, _typeOfMeal: "4 Eggs, Grapefruit", _fastingPeriod: false),
            "Tuesday": <- create Plan(_timeOfDay: 8, _typeOfMeal: "8oz Chicken, 2 Cups Broccoli", _fastingPeriod: false)
        }
    }

}
```

# How would we fix this code?
- Beucase we are using interface (restrction) we need to add the `changeGreeting` signature to the interface
- also because varable `favouriteFruit` is part of the interface we need wire it up in the `Test` function as an allowed restriction.

> Example changes highlighted in yellow

![image](https://user-images.githubusercontent.com/2507134/157977044-e03c679c-f92b-476f-b8c9-859ad23dc51d.png)

