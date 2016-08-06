# FreeCodeCamp Solutions

####1. Bonfire: Roman Numeral Converter
####### mySolution:
```JavaScript
function convertToRoman(num) {
    var newArr = [];
    var arr = num.toString().split("");
    // convert the given number into string
    var zero = "0";
    var n = ["3000", "2000", "1000", "900", "800", "700", "600", "500", "400", "300", "200", "100", "90", "80", "70", "60", "50", "40", "30", "20", "10", "9", "8", "7", "6", "5", "4", "3", "2", "1"];
    var r = ["MMM", "MM", "M", "CM", "DCCC", "DCC", "DC", "D", "CD", "CCC", "CC", "C", "XC", "LXXX", "LXX", "LX", "L", "XL", "XXX", "XX", "X", "IX", "VIII", "VII", "VI", "V", "IV", "III", "II", "I"];
    for (var i = 0; i < arr.length; i++) {
        arr[i] = arr[i] + zero.repeat(arr.length - i - 1);
        // loop through the array, add specific number of "0" in place
        // e.g. ["1", "0", "2", "3"] would be ["1000", "000", "20", "3"]
        for (var j = 0; j < n.length; j++) {
            if (n[j] === arr[i]) {
                newArr.push(r[j]);
                num = newArr.join('');
            }
        }
    }
    return num;
}
convertToRoman(1023);
```
####### betterSolution:
```JavaScript
function convert(num) {
    var converted = ''
        , decimals = [1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1]
        , romanN = ['M', 'CM', 'D', 'CD', 'C', 'XC', 'L', 'XL', 'X', 'IX', 'V', 'IV', 'I'];
    // reduce amount of numbers to loop through to only include those smaller or = to num
    var filtered = decimals.filter(function (item) {
        return item <= num;
    });
    // using the index in the initial dec. array of the first possible
    // outcome from the new array, remove all roman numerals before
    var nRoman = romanN.slice(decimals.indexOf(filtered[0]));
    for (var i = 0; i < filtered.length; i++) {
        while (num >= filtered[i]) {
            converted += nRoman[i];
            num -= filtered[i];
        }
    }
    return converted;
}
convert(2450);
```

####2. Bonfire: Wherefore art thou
```JavaScript
function whatIsInAName(collection, source){
    var arr = collection.filter(function(item){
        for(var i in source){
            if(source[i] != item[i]){
                return false;
            }
        }
        return true;
    });
    return arr;
}
```

####3. Bonfire: Pig Latin
####### mySolution:
```JavaScript
function translatePigLatin(str) {
    var newStr = "";
    var position = str.search(/[aeiou]/);
    // search for the first vowel and return its position
    if (str[0] === "a" || str[0] === "e" || str[0] === "i" || str[0] === "o" || str[0] === "u") {
        newStr = str + "way";
    }
    else {
        var head = str.substring(0, position);
        // chop of whatever preceding the vowel
        var body = str.slice(position);
        // keep the rest after head is being chopped off
        newStr = body + head + "ay";
    }
    return newStr;
}
translatePigLatin("glove");
```

####### betterSolution:
```JavaScript
function translate(str) {
    // Create variables to be used
    var pigLatin = '';
    var regex = /[aeiou]/gi;
    // Check if the first character is a vowel
    if (str[0].match(regex)) {
        pigLatin = str + 'way';
    }
    else {
        // Find how many consonants before the firs vowel.
        var vowelIndice = str.indexOf(str.match(regex)[0]);
        // Take the string from the first vowel to the last char
        // then add the consonants that were previously omitted and add the ending.
        pigLatin = str.substr(vowelIndice) + str.substr(0, vowelIndice) + 'ay';
    }
    return pigLatin;
}
```

####4. Bonfire: DNA Pairing
```JavaScript
function pairElement(str) {
    var newArr = str.split("");
    var final = new Array(newArr.length);
    for (var i = 0; i < newArr.length; i++) {
        final[i] = [];
        if (newArr[i] === "G") {
            final[i].push("G");
            final[i].push("C");
        }
        else if (newArr[i] === "C") {
            final[i].push("C");
            final[i].push("G");
        }
        else if (newArr[i] === "A") {
            final[i].push("A");
            final[i].push("T");
        }
        else if (newArr[i] === "T") {
            final[i].push("T");
            final[i].push("A");
        }
    }
    return final;
}
```
####4. Bonfire: Missing letters
```JavaScript
function fearNotLetter(str) {
    // loop through string
    for (var i = 1; i < str.length - 1; i++) {
        // check whether all letter have consequential unicode values
        if ((str.charCodeAt([i + 1]) - str.charCodeAt([i])) != 1) {
            // if there are any gaps, return missing letter
            return String.fromCharCode(str.charCodeAt([i]) + 1);
        }
    }
    // else continue until the function returns undefined;
    return undefined;
}
fearNotLetter('abce');
```

####4. Bonfire: Sorted Union
```JavaScript
function uniteUnique(arr) {
    var final = [];
    // Loop through the arguments object
    for (var i = 0; i < arguments.length; i++) {
        var currentArray = arguments[i];
        // Loops through the array at hand
        for (var j = 0; j < currentArray.length; j++) {
            // Checks if the value is already on the final array
            if (final.indexOf(currentArray[j]) < 0) {
                final.push(currentArray[j]);
            }
        }
    }
    return final;
}
uniteUnique([1, 3, 2], [5, 2, 1, 4], [2, 1]);
```

####5. Bonfire: Convert HTML Entities
```JavaScript
function convertHTML(str) {
    var splittedStr = str.split("");
    for (var i = 0; i < splittedStr.length; i++) {
        switch (splittedStr[i]) {
        case "<":
            splittedStr[i] = "&lt;";
            break;
        case ">":
            splittedStr[i] = "&gt;";
            break;
        case "&":
            splittedStr[i] = "&amp;";
            break;
        case '"':
            splittedStr[i] = "&quot;";
            break;
        case "'":
            splittedStr[i] = "&apos;";
            break;
        }
    }
    splittedStr = splittedStr.join("");
    return splittedStr;
}
convertHTML("Dolce & Gabbana");
```

####6. Bonfire: Spinal Tap Case
```JavaScript
function spinalCase(str) {
    str = str.replace(/([a-z])([A-Z])/g, "$1 $2");
    // $n represents the nth match
    // replace everything follows this pattern aA with a space between each occurrence;
    return str.replace(/\s|_/g, "-").toLowerCase();
    // replace space or underscore with dash
}
spinalCase('The_Andy_Griffith_Show');
```

####7. Bonfire: Sum All Odd Fibonacci Numbers
```JavaScript
function sumFibs(num) {
    var preNumber = 0;
    var curNumber = 1;
    var sum = 0;
    while (curNumber <= num) {
        if (curNumber % 2 !== 0) {
            sum += curNumber;
        }
        var added = preNumber + curNumber;
        preNumber = curNumber;
        curNumber = added;
    }
    return sum;
}
sumFibs(4);
```
####7. Bonfire: Sum All Primes
```JavaScript
function sumPrimes(num) {
    var primes = [];
    var total = 0;
    for (var i = 2; i <= num; i++) {
        var isPrime = true;
        // Determine if i is actually a prime by dividing it by every number from 2 to i
        for (var j = 2; j < i; j++) {
            if (i % j === 0) {
                isPrime = false;
            }
        }
        if (isPrime) {
            primes.push(i);
        }
    }
    total = primes.reduce(function (a, b) {
        return a + b;
    });
    return total;
}
sumPrimes(977);
```
