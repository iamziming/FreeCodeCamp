# FreeCodeCamp Solutions

####1. Bonfire: Roman Numeral Converter
####### mySolution:
```JavaScript
function convertToRoman(num) {
    
    var newArr = [];
    var arr = num.toString().split("");
    //convert the given number into string
    var zero = "0";
    
    var n = ["3000", "2000", "1000", "900", "800", "700", "600", "500", "400", "300", "200", "100", "90", "80", "70", "60", "50", "40", "30", "20", "10", "9", "8", "7", "6", "5", "4", "3", "2", "1"];
    var r = ["MMM", "MM", "M", "CM", "DCCC", "DCC", "DC", "D", "CD", "CCC", "CC", "C", "XC", "LXXX", "LXX", "LX", "L", "XL", "XXX", "XX", "X", "IX", "VIII", "VII", "VI", "V", "IV", "III", "II", "I"];

    for(var i = 0; i < arr.length; i++){
        arr[i] = arr[i] + zero.repeat(arr.length - i - 1);
        //loop through the array, add specific number of "0" in place
        //e.g. ["1", "0", "2", "3"] would be ["1000", "000", "20", "3"]
        for(var j = 0; j < n.length; j++){
            if(n[j] === arr[i]){
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
    var converted = '',
        decimals = [1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5,  4, 1],
        romanN = ['M', 'CM', 'D', 'CD', 'C', 'XC', 'L', 'XL', 'X', 'IX', 'V', 'IV', 'I'];
    // reduce amount of numbers to loop through to only include those smaller or = to num
    var filtered = decimals.filter(function(item) {
        return item <= num;
    });
    // using the index in the initial dec. array of the first possible
    // outcome from the new array, remove all roman numerals before
    var nRoman = romanN.slice(decimals.indexOf(filtered[0]));

    for (var i = 0; i < filtered.length; i++) {
        while(num >= filtered[i]) {
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
