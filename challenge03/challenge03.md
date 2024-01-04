# Challenge 03

** The Spy Cipher Challenge **

A group of spies have discovered that their message encryption system has been compromised.

They have found some passwords that do not comply with the Encryption Security Policy they had in place when they were created.

To solve the problem, they have created a list (your entry to the challenge) of passwords (according to the corrupted database) and the security policy when that password was set.

Example of the list:
```bs
2-4 f: fgff
4-6 z: zzzsg
1-6 h: hhhhhh
```
Each line indicates, separated by : the policy of the key and the key itself.

The key policy specifies the minimum and maximum number of times a given character must appear for the key to be valid. 

For example, 2-4 f means that the key must contain f at least 2 times and at most 4 times.

Knowing this, in the above example, there are 2 valid keys:

The second key, zzzsg, is not; it contains 3 times the letter z, but needs at least 4. The first and third keys are valid: they contain the right amount of f and h, respectively, according to their policies.

** Your challenge: **

Determines how many encryption keys are valid according to your policies.

** How to solve it **

Please review the list of encryption policies and keys in this file:
 
https://codember.dev/data/encryption_policies.txt

Create a program that returns the invalid key number 42 (of all invalid keys, the 42nd in order of occurrence). For example:

``submit bqamidgewtbuz``

## Solution

```js
// Function to find the invalid key number 42 among all invalid keys.
function findInvalidPasswordNumber(input) {
  // Split the input lines and remove blank spaces around them.
  const lines = input.split("\n").map((line) => line.trim());

  // Array for storing invalid keys
  const invalidPasswords = [];

  // Iterate over each line of the entry
  for (let i = 0; i < lines.length; i++) {
    // Separate key and password policy
    const [policy, password] = lines[i].split(": ");

    // Separating the rank and character of politics
    const [range, char] = policy.split(" ");

    // Convert range limits to numbers
    const [minCount, maxCount] = range.split("-").map(Number);

    // Check if the password complies with the policy
    if (!isPasswordValid([minCount, maxCount, char], password)) {
      // Store password in invalid key array
      invalidPasswords.push(password);

      // If 42 invalid keys have already been found, return the invalid key.
      if (invalidPasswords.length === 42) {
        return invalidPasswords[41];
      }
    }
  }

  // If not enough invalid keys were found, return null
  return null;
}
```

```js
function findInvalidPasswordNumber(policy, passwords) {
  const [minCount, maxCount, char] = policy;
  const charCount = (passwords.match(new RegExp(char, "g")) || []).length;
  return minCount <= charCount && charCount <= maxCount;
}
```

## Reply

```bash
submit bgamidqewtbus
```
