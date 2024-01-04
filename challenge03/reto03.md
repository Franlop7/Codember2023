# Reto 03

** El Desafío del Cifrado Espía **

Un grupo de espías ha descubierto que su sistema de cifrado de mensajes está comprometido.

Han encontrado algunas contraseñas que no cumplen con laPolítica de Seguridad de Cifrado que tenían establecida cuando fueron creadas.

Para solucionar el problema, han creado una lista (tu entrada al desafío) de contraseñas (según la base de datos corrupta) y la política de seguridad cuando esa clave fue establecida.

Ejemplo de la lista:
```bs
2-4 f: fgff
4-6 z: zzzsg
1-6 h: hhhhhh
```
Cada línea indica, separado por :, la política de la clave y la clave misma.

La política de la clave especifica el número mínimo y máximo de veces que un carácter dado debe aparecer para que la clave sea válida. 

Por ejemplo, 2-4 f significa que la clave debe contener f al menos 2 veces y como máximo 4 veces.

Sabiendo esto, en el ejemplo anterior, hay 2 claves válidas:

La segunda clave, zzzsg, no lo es; contiene 3 veces la letra z, pero necesita al menos 4. Las primeras y terceras claves son válidas: contienen la cantidad adecuada de f y h, respectivamente, según sus políticas.

** Tu desafío: **

Determina cuántas claves de cifrado son válidas según sus políticas.

** Cómo resolverlo **

Analiza la lista de políticas y claves de cifrado que encontrarás en este archivo:
 
https://codember.dev/data/encryption_policies.txt

Crea un programa que devuelva la clave inválida número 42 (de todas las claves inválidas, la 42ª en orden de aparición). Por ejemplo:

``submit bqamidgewtbuz``

## Solución

```js
// Función para encontrar la clave inválida número 42 entre todas las claves inválidas
function findInvalidPasswordNumber(input) {
  // Dividir las líneas del input y eliminar espacios en blanco alrededor
  const lines = input.split("\n").map((line) => line.trim());

  // Array para almacenar claves inválidas
  const invalidPasswords = [];

  // Iterar sobre cada línea de la entrada
  for (let i = 0; i < lines.length; i++) {
    // Separar la política de la clave y la contraseña
    const [policy, password] = lines[i].split(": ");

    // Separar el rango y el carácter de la política
    const [range, char] = policy.split(" ");

    // Convertir los límites del rango a números
    const [minCount, maxCount] = range.split("-").map(Number);

    // Verificar si la contraseña cumple con la política
    if (!isPasswordValid([minCount, maxCount, char], password)) {
      // Almacenar la contraseña en el array de claves inválidas
      invalidPasswords.push(password);

      // Si ya se han encontrado 42 claves inválidas, devolver dicha clave
      if (invalidPasswords.length === 42) {
        return invalidPasswords[41];
      }
    }
  }

  // Si no se encontraron suficientes claves inválidas, devolver null
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

## Respuesta

```bash
submit bgamidqewtbus
```
