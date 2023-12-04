# Challenge 01

** The challenge **

A spy is sending encrypted messages.

Your mission is to create a programme that helps us look for patterns...

Messages are words separated by spaces like this:

``gato perro perro coche Gato peRRo sol``

We need the program to return the number of times each word appears in the message, regardless of whether it is in upper or lower case.

The result will be a text string with the word and the number of times it appears in the message, in this format:

``gato2perro3coche1sol1``

The words are ordered by their first appearance in the message!

** More examples: **

llaveS casa CASA casa llaves -> llaves2casa3

taza ta za taza -> taza2ta1za1

casas casa casasas -> casas1casa1casas1

** How to solve it **

Solve the message you will find in this file:

https://codember.dev/data/message_01.txt

Submit your solution with the command "submit" in the terminal, for example like this:

``submit perro3gato3coche1sol1``

## Solution

```js
const msg 'words'

function countWords (mensaje) {
	return mensaje.toLowerCase().split(" ").reduce((acc, palabra) => {
		if (acc.includes(palabra)) acc[acc.indexOf(palabra) + 1] += 1;
		else acc.push(palabra, 1);
		return acc;
	}, []).join("");
}


console.log(countingWords(msg))

```

## Reply

```bash
submit murcielago15leon15jirafa15cebra6elefante15rinoceronte15hipopotamo15ardilla15mapache15zorro15lobo15oso15puma2jaguar14tigre10leopardo10gato12perro12caballo14vaca14toro14cerdo14oveja14cabra14gallina10pato10ganso10pavo10paloma10halcon11aguila11buho11colibri9canario8loro8tucan8pinguino7flamenco7
```
