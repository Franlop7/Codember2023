# Challenge 04

** Hackers damage file system **

In a world where information is power, a hacker known as Savipo Yatar discovers a series of files on a highly protected server.

These files contain secrets that could change the course of history. But there's a problem: some of the files are fakes, designed to deceive intruders. Savipo Yatar must quickly determine which files are real and which are fake.

Each file has a name with two parts, separated by a hyphen (-). The first part is an alphanumeric string and the second part is unchecksum, which is a string consisting of the characters that only appear once in the first part and in the order in which they appear.

Write a program that determines whether a file is real or fake based on these rules.

Examples:
```bs
File name: xyzz33-xy
Result: ✅ True (The checksum is valid)

File name: abcca1-ab1
Result: ❌ False (The checksum should be b1, it is incorrect.)

File name: abbc11-ca
Result: ❌ False (The checksum should be ac, the order is incorrect.)
Each line indicates the name of the file and its corresponding checksum, separated by a hyphen (-).
```

** How to solve it **

Analyse the list of file names and their checksums that you will find in this file:

https://codember.dev/data/files_quarantine.txt

Find the real file number 33 (of all the real files, the 33rd in order of appearance) and send its checksum with submit. For example if the file is xyzz33-xy, you would do:

``submit xy``

## solution

```js
function correctFiles (files) {
	return files.filter(file => {
		const [name, checksum] = file.split('-');
		const uniqueChars = name.split("").filter((char, index, self) => {
			return name.slice(index + 1).indexOf(char) === -1 && self.indexOf(char) === index;
		});
		return checksum === uniqueChars.join("");
	});
}
console.log(correctFiles(files)[32]);
```

## Reply

```bash
submit O2hrQ
```
