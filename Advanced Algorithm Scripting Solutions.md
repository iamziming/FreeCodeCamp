# FreeCodeCamp
# Advanced Algorithm Scripting Solutions

####1. Validate US Telephone Numbers
```JavaScript
function telephoneCheck(str) {
    var regex = /^1? ?(\d{3}|\(\d{3}\))[ -]?\d{3}[ -]?\d{4}$/;
    return regex.test(str);
}
```

####2. Symmetric Difference
```JavaScript
function sym() {
    var args = [];
    for (var i = 0; i < arguments.length; i++) {
        args.push(arguments[i]);
    }

    function symDiff(arrayOne, arrayTwo) {
        var result = [];
        arrayOne.forEach(function (item) {
            if (arrayTwo.indexOf(item) < 0 && result.indexOf(item) < 0) {
                result.push(item);
            }
        });
        arrayTwo.forEach(function (item) {
            if (arrayOne.indexOf(item) < 0 && result.indexOf(item) < 0) {
                result.push(item);
            }
        });
        return result;
    }
    return args.reduce(symDiff);
}
```

####3. Exact Change
```JavaScript
function checkCashRegister(price, cash, cid) {
    cash = cash * 100;
    price = price * 100;
    var change = cash - price
        , changeLeft = change;
    var totalCid = getTotalCid(cid);
    var result = [];
    if (change > totalCid) {
        return 'Insufficient Funds';
    }
    else if (change === totalCid) {
        return 'Closed';
    }
    for (var i = cid.length - 1; i >= 0; i--) {
        var coinName = cid[i][0]
            , coinTotal = cid[i][1] * 100
            , singalCoinValue = getValue(coinName)
            , amountOfCoin = coinTotal / singalCoinValue
            , toReturn = 0;
        while (changeLeft >= singalCoinValue && amountOfCoin > 0) {
            changeLeft -= singalCoinValue;
            amountOfCoin--;
            toReturn++;
            console.log(changeLeft);
        }
        if (toReturn > 0) {
            result.push([coinName, toReturn * (singalCoinValue / 100)]);
        }
    }
    if (getTotalCid(result) != change) {
        return 'Insufficient Funds';
    }
    return result;

    function getTotalCid(cid) {
        var total = 0;
        for (var i = 0; i < cid.length; i++) {
            total += cid[i][1] * 100;
        }
        return total;
    }

    function getValue(coinOrBill) {
        switch (coinOrBill) {
        case 'PENNY':
            return 1;
        case 'NICKEL':
            return 5;
        case 'DIME':
            return 10;
        case 'QUARTER':
            return 25;
        case 'ONE':
            return 100;
        case 'FIVE':
            return 500;
        case 'TEN':
            return 1000;
        case 'TWENTY':
            return 2000;
        case 'ONE HUNDRED':
            return 10000;
        }
    }
}
```

####4. Inventory Update
```JavaScript
function updateInventory(arr1, arr2) {
    var found = false;
    for (j = 0; j < arr2.length; j++) {
        found = false;
        for (i = 0; i < arr1.length; i++) {
            if (arr2[j][1] == arr1[i][1]) {
                arr1[i][0] += arr2[j][0];
                found = true;
            }
        }
        if (found === false) {
            arr1.push(arr2[j]);
        }
    }
    arr1.sort(function (a, b) {
        if (a[1] < b[1]) {
            return -1;
        }
        else if (a[1] > b[1]) {
            return 1;
        }
    });
    return arr1;
}
var curInv = [[21, "Bowling Ball"], [2, "Dirty Sock"], [1, "Hair Pin"], [5, "Microphone"]];
var newInv = [[2, "Hair Pin"], [3, "Half-Eaten Apple"], [67, "Bowling Ball"], [7, "Toothpaste"]];
updateInventory(curInv, newInv);
```

####5. No repeats please
```JavaScript
function permAlone(str) {
    var permutations = []
        , nextWord = []
        , chars = [];
    if (typeof str === 'string') chars = str.split('');
    permutate(chars);

    function permutate(chars) {
        if (chars.length === 0) {
            permutations.push(nextWord.join(''));
        }
        for (var i = 0; i < chars.length; i++) {
            chars.push(chars.shift());
            nextWord.push(chars[0]);
            permutate(chars.slice(1));
            nextWord.pop();
        }
    }
    var regex = /(.)\1/g;
    var filtered = permutations.filter(function (string) {
        return !string.match(regex);
    });
    return filtered.length;
}
permAlone('abc');
```

####6. Friendly Date Ranges
```JavaScript
function makeFriendlyDates(arr) {
    var start = new Date(arr[0]), 
        end = new Date(arr[1]), 
        currYear = new Date().getUTCFullYear();
    
    var startYear = start.getUTCFullYear(), 
        startMonth = start.getUTCMonth(), 
        startDay = start.getUTCDate(), 
        endYear = end.getUTCFullYear(), 
        endMonth = end.getUTCMonth(), 
        endDay = end.getUTCDate();
    
    var months = ["January", "February", "March", "April", "May", "June"
               , "July", "August", "September", "October", "November", "December"];
    // check for same date
    if (start.getTime() === end.getTime()) {
        if (currYear === startYear) {
            // Same Date, this year
            return [months[startMonth] + " " + ordinalize(startDay)];
        }
        else {
            // Same Date, not this year
            return [months[startMonth] + " " + ordinalize(startDay) + ", " + startYear];
        }
    }
    // check for same month
    else if (startYear === endYear && startMonth === endMonth) {
        if (currYear === startYear) {
            // Same Month, this year
            return [months[startMonth] + " " + ordinalize(startDay), ordinalize(endDay)];
        }
        else {
            // Same Month, not this year
            return [months[startMonth] + " " + ordinalize(startDay) + ", " + startYear, ordinalize(endDay)];
        }
    }
    // check for same year
    else if (sameYear(start, end)) {
        if (currYear === startYear) {
            // Start Date in this year, end date less than 1 year away
            return [months[startMonth] + " " + ordinalize(startDay), months[endMonth] + " " + ordinalize(endDay)];
        }
        else {
            // Dates fall within same year. Start Date is NOT in this year
            return [months[startMonth] + " " + ordinalize(startDay) + ", " + startYear, months[endMonth] + " " + ordinalize(endDay)];
        }
    }
    // does not meet any of the above conditions
    else {
        // display both full dates
        return [months[startMonth] + " " + ordinalize(startDay) + ", " + startYear, months[endMonth] + " " + ordinalize(endDay) + ", " + endYear];
    }
    // sameYear returns true if the date objects are less than one year apart, otherwise returns false
    function sameYear(d1, d2) {
        var years = d2.getUTCFullYear() - d1.getUTCFullYear();
        var origYear = d1.getUTCFullYear();
        d1.setUTCFullYear(d2.getUTCFullYear());
        if (d2 < d1) years--;
        d1.setUTCFullYear(origYear);
        if (years < 1) return true;
        return false;
    }
    // ordinalize returns a formatted day string
    function ordinalize(n) {
        switch (n) {
        case 1:
        case 21:
        case 31:
            return n + 'st';
        case 2:
        case 22:
            return n + 'nd';
        case 3:
        case 23:
            return n + 'rd';
        default:
            return n + 'th';
        }
    }
}
makeFriendlyDates(['2016-07-01', '2016-07-04']);
```

####7. Make a Person
```JavaScript
var Person = function (firstAndLast) {
    var fullName = firstAndLast;
    this.getFirstName = function () {
        return fullName.split(" ")[0];
    };
    this.getLastName = function () {
        return fullName.split(" ")[1];
    };
    this.getFullName = function () {
        return fullName;
    };
    this.setFirstName = function (name) {
        fullName = name + " " + fullName.split(" ")[1];
    };
    this.setLastName = function (name) {
        fullName = fullName.split(" ")[0] + " " + name;
    };
    this.setFullName = function (name) {
        fullName = name;
    };
};
var bob = new Person('Bob Ross');
bob.getFullName();
```

####8. Map the Debris
```JavaScript
function orbitalPeriod(arr) {
    var GM = 398600.4418;
    var earthRadius = 6367.4447;
    
    arr.forEach(function(obj){
        var orbPeriod = Math.round(2*Math.PI*Math.sqrt(Math.pow(earthRadius + obj.avgAlt, 3)/GM));
        obj.orbitalPeriod = orbPeriod;  // assign value to a new property of the current object
        delete obj.avgAlt;
    });
    
    return arr;
}
orbitalPeriod([{name: "sputnik", avgAlt: 35873.5553}]);
```
