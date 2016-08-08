# FreeCodeCamp
# Advanced Algorithm Scripting Solutions

####1. Validate US Telephone Numbers
```JavaScript
function telephoneCheck(str) {
    var regex = /^1? ?(\d{3}|\(\d{3}\))[ -]?\d{3}[ -]?\d{4}$/;
    return regex.test(str);
}
```
