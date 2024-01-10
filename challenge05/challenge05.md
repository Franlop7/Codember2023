# Challenge 05

** The final problem **

The hackers have finally managed to access the database and have left it corrupted. But they seem to have left a hidden message in the database - can you find it?

Our database is in .csv format. The columns are id, username, email, age, location.

A user is only valid if:

- id: exists and is alphanumeric
- username: exists and is alphanumeric
- email: exists and is valid (follows the pattern user@dominio.com)
- age: is optional but if it appears it is a number.
- location: optional, but if it appears it is a text string.

Examples:
```bs
input: 1a421fa,alex,alex9@gmail.com,18,Barcelona
Result: ✅ Valid

input: 9412p_m,maria,mb@hotmail.com,22,CDMX
Result: ❌ Invalid (id is not alphanumeric, the _ is left over.)

input: 494ee0,madeval,mdv@twitch.tv,,
Result: ✅ Valid (age and location are optional)
input: 494ee0,madeval,twitch.tv,22,Montevideo
Result: ❌ Invalid (email is invalid)
```
** How to solve it **

It scans the list of entries in the database and detects invalid entries:

https://codember.dev/data/database_attacked.txt

Find the first character (number or letter) of the username of each invalid user. Put them together in order of appearance and find the hidden message. Then send it with submit. For example:

``submit att4ck``

## solution

```js
function findInvalidCharacter (data) {
	return data.reduce((usersInvalid, row) => {
		const columns = row.split(',');

		const id = columns[0].trim();
		const username = columns[1].trim();
		const email = columns[2].trim();
		const age = columns[3] ? columns[3].trim() : '';
		const location = columns[4] ? columns[4].trim() : '';

		if (!/^[a-zA-Z0-9]+$/.test(id) ||
			!/^[a-zA-Z0-9]+$/.test(username) ||
			!/^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}$/.test(email) ||
			(age !== '' && isNaN(age)) ||
			(location !== '' && typeof location !== 'string')) {
			usersInvalid.push(username[0]);
		}

		return usersInvalid;
	}, []).join('');
}
```
```js
function findInvalidCharacter(data) {
    return data.reduce((usersInvalid, row) => {
        const columns = row.split(',').map(column => column.trim());

        const [id, username, email, age, location] = columns;

        const isValidId = /^[a-zA-Z0-9]+$/.test(id);
        const isValidUsername = /^[a-zA-Z0-9]+$/.test(username);
        const isValidEmail = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}$/.test(email);
        const isValidAge = age === '' || (!isNaN(age) && Number(age) >= 0);
        const isValidLocation = location === '' || typeof location === 'string';

        if (!isValidId || !isValidUsername || !isValidEmail || !isValidAge || !isValidLocation) {
            usersInvalid.push(username[0]);
        }

        return usersInvalid;
    }, []).join('');
}
```

## Reply

```bash
submit youh4v3beenpwnd
```
