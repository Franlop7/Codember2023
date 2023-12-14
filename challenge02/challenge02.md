# Challenge 02

** Mini Compiler Challenge **

In the world of espionage, a coding language is used with symbols that perform simple mathematical operations.

Your task is to create a mini-compiler that interprets and executes programs written in this symbol language.

The operations of the language are as follows:

```bs
"#" Increments the numerical value by 1.

"@" Decrements the numerical value by 1.

"*" Multiplies the numerical value by itself.

"&" Prints the current numerical value.
```

The initial numeric value is 0 and the operations must be applied in the order in which they appear in the symbol string.

** Examples of entry: **

```bs
input: "##*&"

expected output: "4"

Explanation: Increment (1), increment (2), multiplies (4), print (4).


input: "&##&*&@&"

expected output: "0243"

Explanation: Print (0), increment (1), increment (2), print (2), multiplies (4), print (4), decrement (3), print (3).
```

** You Challenge: **

Develop a mini compiler that takes a string of text and returns another string of text with the result of running the program.

** How to solve it **

Solve the message you will find in this file:

https://codember.dev/data/message_02.txt

Create a program to which you pass the above message as input. Send the output with the command "submit" in the terminal, for example like this:

``submit 024899488``

## Solution

```js
function miniCompiler(input) {
  // Initialise variables
  let value = 0;
  let result = "";

  // Convert string to array and use forEach to iterate
  input.split("").forEach((input) => {
    if (input === "#") {
      value++;
    } else if (input === "@") {
      value--;
    } else if (input === "*") {
      value *= value;
    } else if (input === "&") {
      result += value;
    }
    // Ignore unknown characters
  });

  // Return cumulative result
  return result;
}
```

```js
function miniCompiler(input) {
  let value = 0;
  let result = "";

  for (let i = 0; i < input.length; i++) {
    switch (input[i]) {
      case "#":
        value++;
        break;
      case "@":
        value--;
        break;
      case "*":
        value *= value;
        break;
      case "&":
        result += value;
        break;
      default:
        break;
    }
  }

  return result;
}
```

```js
function miniCompiler(input) {
  let value = 0;
  return input
    .split("&")
    .slice(0, -1)
    .reduce((acc, curr) => {
      [...curr].forEach((item, _) => {
        if (item === "#") value++;
        if (item === "@") value--;
        if (item === "*") value *= value;
      });
      return (acc += value);
    }, "");
}
```



## Reply

```bash
submit 024899455
```
