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
