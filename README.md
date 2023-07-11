# clean-code-typescript 
Learning & practicing clean code in typescript

## Table of Contents

- [clean-code-typescript](#clean-code-typescript)
  - [Table of Contents](#table-of-contents)
  - [Why clean code](#why-clean-code)
  - [What is clean code](#what-is-clean-code)
  - [Variables](#variables)
  - [Functions](#functions)
  - [Comments](#comments)
  - [Error Handling](#error-handling)
  - [Unit Tests](#unit-tests)
  - [System Design \& Development Principles](#system-design--development-principles)


## Why clean code

To be a better programmer


## What is clean code

The only way to go fast is to write clean code.

One difference between a smart programmer and a professional programmer is that the professional understands that clarity is king. Professionals use their powers for good and write code that others can understand.

I like my code to be elegant and efficient. -- Bjarne Stroustrup, inventor of C++

Clean code can be read, and enhanced by a developer other than its original author. -- Dave Thomas, godfather of Elipse strategy

Clean code always looks like it was written by someone who cares. -- Michael Feathers


## Variables

- Variable names should be meaningful


  **Bad:**
  ```ts
  let d; // meant to represent days to count
  ```

  **Good:**
  ```ts
  let daysToCount; // More meaningful, no need to guess
  ```

- Class Names
  Classes and objects should have noun or noun phrase names.
  
  **Good:** 
  ```ts
  class Customer {}
  class AddressParser{} 
  ```
  **Bad:**
  ```ts
  // Avoid using Manager, Processor, Data, or Info. 
  class Manager{} // Bad

  // A class name should not be a verb.
  ```

- Method Names
  Methods should have verb or verb phrase names.

  **Good:**
  ```ts
  function postPayment(){}

  function deleteEntity(){}
  ```


- Don's pun

  Avoid using the same word for two purposes. Using the same term for two different ideas is essentially a pun


**[⬆ back to top](#table-of-contents)**

## Functions

- Small! Functions should be small.
- A function should do one thing and do it well. You don't like to read a function more than one screen.
- Avoid using switch / if statetments as much as we can because they mean the function is potentially doing more than one thing
  **Bad:**
  ```ts
  function getPaymentCodeByType(paymentType: string): string{
    let paymentCode = '';
    if(paymentType === "daily"){
      paymentCode = 'PAY_D';
    }else if(paymentType === "weekly"){
      paymentCode = 'PAY_W';
    }else if(paymentType === "bi-weekly"){
      paymentCode = 'PAY_BW';
    }else if(paymentType === "monthly"){
      paymentCode = 'PAY_M';
    }
    return paymentCode;
  }

  ```
  **Good:**
  ```ts

  function getPaymentCodeByType(paymentType: string): string{
    let paymentCode = '';
    
    // Using mapping table
    let paymentTypeCodeMapping = new Map([
                                    ['daily', 'PAY_D'], 
                                    ['weekly', 'PAY_W'],
                                    ['bi-weekly', 'PAY_BW'],
                                    ['monthly', 'PAY_M'],
                                    ]);

    let paymentCode = paymentTypeCodeMapping.get(paymentType)

    return paymentCode;
  }
  ```

- The ideal number of arguments for a function is zero. Next comes one, followed closely by two. Three arguments should be avoided where possible.

  **Bad:**
  ```ts
  function placeOrder(id: number, name: string, amount: number){
    ...
  }

  ```

  **Good:**
  ```ts
  let order = new Order();
  order.id = 1001;
  order.name = 'Roadster'
  order.amount = 10;

  placeOrder(order);

  function placeOrder(order: Order){
    ...
  }

  ```

**[⬆ back to top](#table-of-contents)**


## Comments

- Try to avoid using comments. Explain yourself in code
- As time goes by, comments would be misleading if it's not updated properly
- Use markers such as TODO: FIXME: etc.. Most IDE provides marker tool to show the marker list. like Todo Tree for VSCode

**Good:**
```ts
// TODO: Code smells, need to refactor
// FIXME: I'm not working well, fix me as early as possible

function makePayment(){
  ...
}

```

**[⬆ back to top](#table-of-contents)**


## Error Handling

- Use Exception Rather Than Return Codes
- Write Try-Catch-Finally Statement First

  - In modern TypeScript, we can wrap Try-Catch-Finally logic in Decorator. So we don't see Try-Catch-Finally everywhere in our code. This is to follow DRY - Don't Repeat Yourself principle
- Use unchecked Exceptions

  - The price of checked exception is an Open/Close Principle violation. If we throw a checked exception from a method in our code and the catch is three levels above, we must declare that exception in the signature of each method. This means that a change at a low level of the software can force signature changes on many higher levels. The changed modules must be rebuild and redeployed, even throgh nothing they care about changed. 
- Provide Context with Exceptions

  - So it's easier to get RCA

- Don't Pass Null
  - It's very easy to invite unexpected exceptions such as NullPointerException etc. when dealing with null objects. See what happens passing a null to payment
    ```ts
    function makePayment(payment: Payment) {
      let firstName = payment.user.firstName;
    }
    ```
  - May introduce a lot of if statements to check if it's not null, something like below:

    ```ts
    function makePayment(payment: Payment) {
      if(payment != null){
        if(payment.user != null){
          let firstName = payment.user.firstName;
        }
      }
    }
    ```
- Don't Return Null
  - Likewise, we do not return null from functions in normal case
    ```ts
    function loadUser(userId: number): User{
      let user = null;
      if(userId){
        user = getUserById(userId);
      }

      return user;
    }

    function getUserFullName(user: User): string{
      let user = loadUser();
      let fullName = `${user.firstName} ${user.lastName}`;

      return fullName;
    }
    ```
**[⬆ back to top](#table-of-contents)**

## Unit Tests
- FIRST
  - **Fast** Tests should be fast. When tests run takes time, we don't want to run them frequently
  - **Independent** Tests should not depend on each other. One test's setup doesn't impact others
  - **Repeatable** Tests should be repeatable in any environments
  - **Self-Validating** There should be be some asserts validation in tests to tell if it's success or not
  - **Timely** Writing unit tests before any production code

**[⬆ back to top](#table-of-contents)**


## System Design & Development Principles
- SOLID
  - **Single Responsibility Principle** There should never be more than one reason for a class to change. Every class should have one responsibility.
  - **Open Close Principle** A great software should be open for extension, but close for modification.
  - **Liskov Substitution Principle** Subclass/derived class should be substitutable for their base/parent class. Refer to Polymorphism in OO Design.
  - **Interface Segregation Principle** Clients should not be forced to depend upon interfaces that they do not use.
  - **Dependency Inversion Principle** Depend on abstractions, not concretions. In other words, depend on interfaces, not implementations. An example is Service provider injection in Angular.


- DRY
  - **Don't Repeat Yourself** principle: A piece of logic should only be represented once in an application. Too many try-catch statements in error handling of a system might be a violation of this pattern. We can eliminate this by leveraging the power of **meta programming** such as **Decorator** in TypeScript
 
**[⬆ back to top](#table-of-contents)**











