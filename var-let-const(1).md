# 🧠 Différences entre `var`, `let` et `const` en JavaScript

En JavaScript, on peut déclarer des variables avec `var`, `let` ou `const`.  
Chacun a ses particularités en termes de **portée (scope)**, de **mutabilité** et de **hoisting** (levage de déclaration).

---

## 📚 Table des matières

- [1. `var`](#-1-var)
- [2. `let`](#-2-let)
- [3. `const`](#-3-const)
- [Tableau comparatif](#-tableau-comparatif)
- [Bonnes pratiques](#-bonnes-pratiques)
- [Exemple combiné](#-exemple-combiné)
- [En résumé rapide](#-en-résumé-rapide)

---

## 🔸 1. `var`

- **Portée** : *fonctionnelle* (ou globale si en dehors d'une fonction)
- **Redéclarable** : ✅ Oui
- **Réassignable** : ✅ Oui
- **Hoisting** : ✅ Oui — mais initialisée à `undefined`

### Exemple :
```js
function testVar() {
  if (true) {
    var x = 5;
  }
  console.log(x); // 5 (accessible même hors du bloc)
}
```

🔴 **Attention** : `var` peut causer des bugs car elle ignore les blocs `{}`.

---

## 🔹 2. `let`

- **Portée** : *bloc* (`{ ... }`)
- **Redéclarable** : ❌ Non (dans une même portée)
- **Réassignable** : ✅ Oui
- **Hoisting** : ✅ Oui — mais **inaccessible avant déclaration** (zone morte temporelle)

### Exemple :
```js
function testLet() {
  if (true) {
    let y = 10;
  }
  console.log(y); // ❌ ReferenceError: y is not defined
}
```

✅ **Utiliser `let`** quand on prévoit de modifier la valeur de la variable.

---

## 🧊 3. `const`

- **Portée** : *bloc* (`{ ... }`)
- **Redéclarable** : ❌ Non
- **Réassignable** : ❌ Non
- **Hoisting** : ✅ Oui — mais **inaccessible avant déclaration**

### Exemple :
```js
const z = 42;
z = 50; // ❌ TypeError: Assignment to constant variable

const obj = { name: "ChatGPT" };
obj.name = "GPT-4"; // ✅ OK car on ne change pas la référence de l'objet
```

✅ **À privilégier** par défaut : elle empêche les réassignations par erreur.

---

## 📋 Tableau comparatif

| Mot-clé  | Portée     | Redéclarable | Réassignable | Hoisting | Remarques                        |
|----------|------------|--------------|--------------|----------|----------------------------------|
| `var`    | Fonction   | ✅ Oui        | ✅ Oui        | ✅ Oui   | Obsolète, à éviter               |
| `let`    | Bloc       | ❌ Non        | ✅ Oui        | ✅ Oui*  | Pour variables modifiables       |
| `const`  | Bloc       | ❌ Non        | ❌ Non        | ✅ Oui*  | Pour constantes (ou objets)      |

> 💡 *Hoisting avec `let` et `const` : la déclaration est levée, mais la variable est **inaccessible jusqu'à son initialisation** (zone morte temporelle).

---

## ✅ Bonnes pratiques

- 🔹 Utiliser `const` **par défaut**
- 🔸 Utiliser `let` **si la valeur doit changer**
- ❌ Éviter `var`, sauf pour lire ou maintenir du vieux code

---

## 🧪 Exemple combiné

```js
function exemple() {
  var a = 1;
  let b = 2;
  const c = 3;

  if (true) {
    var a = 10;   // Redéclare et écrase
    let b = 20;   // Nouvelle variable locale au bloc
    // c = 30;    // ❌ Erreur : on ne peut pas réassigner une const
    console.log(a, b, c); // 10, 20, 3
  }

  console.log(a); // 10 (modifié à l'intérieur)
  console.log(b); // 2 (valeur initiale)
  console.log(c); // 3 (constante)
}
```

---

## 📎 En résumé rapide

- `var` → **ancien**, piège à bugs, à éviter
- `let` → **moderne**, souple, pour les variables qui changent
- `const` → **par défaut**, fiable, prévient les erreurs

---

🧠 Happy coding !
