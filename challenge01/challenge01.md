# Challenge 01


## Solución

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