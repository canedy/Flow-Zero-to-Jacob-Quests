1. Explain why we wouldn't call changeGreeting in a script.
- Scripts can only read a contract. To write or execute against a contract, you need to run a transaction. 
2. What does the AuthAccount mean in the prepare phase of the transaction?
- It is the authorized account that is about to run the transaction. It gives you access to the accounts storage and account level attribute or function in the contract. 
3. What is the difference between the prepare phase and the execute phase in the transaction?
- The prepare phase gives access to account-level information such as storage and contract account level attributes and functions. The execute phase allows you to execute any public-facing function that is not authorized as the account. 

4. This is the hardest quest so far, so if it takes you some time, do not worry! I can help you in the Discord if you have questions.
### 0x03 Contract

![image](https://user-images.githubusercontent.com/2507134/157365955-6ae3ef35-f1c6-422b-b096-517c958c72d4.png)


### Transaction /w results

![image](https://user-images.githubusercontent.com/2507134/157366084-ee232f93-328e-4dfc-afb3-b813a12d5c2d.png)

### Script /w results

![image](https://user-images.githubusercontent.com/2507134/157366170-40035e2c-029e-458d-921b-c5188a1d7b71.png)
