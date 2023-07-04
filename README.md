# clean-code-typescript 
Learning & practicing clean code in typescript

## Table of Contents

  0. [Why clean code](#why-clean-code)
  1. [What is clean code](#what-is-clean-code)
  2. [Variables](#variables)
  3. [Functions](#functions)

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

```

**Good:**
```ts

```













