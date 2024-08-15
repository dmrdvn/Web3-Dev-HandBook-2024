# Döngüler

Döngüler, belirli bir koşul sağlandığı sürece kod bloklarının tekrar tekrar çalıştırılmasını sağlar. Solidity'de üç ana döngü türü vardır: `for`, `while`, ve `do-while` döngüleri. Her biri farklı durumlarda kullanılır ve belirli avantajlar sunar.

## **1. For Döngüsü**

`For` döngüsü, genellikle belirli bir sayıda tekrar yapmak için kullanılır. Genellikle bir sayaç değişkeni içerir ve döngü bu değişkenin belirli bir aralıkta olup olmadığını kontrol eder.

**Syntax**

```solidity
for (initialization; condition; update) {
    // Döngü bloğu
}
```

**Örnek**

```solidity
function sum(uint256 _n) public pure returns (uint256) {
    uint256 total = 0;
    for (uint256 i = 1; i <= _n; i++) {
        total += i;
    }
    return total;
}
```

Bu örnekte, `sum` fonksiyonu 1'den `_n`'e kadar olan sayıların toplamını hesaplar. `for` döngüsü `i` değişkenini 1'den başlayarak `_n`'e kadar artırır ve her adımda toplamı günceller.

## **2. While Döngüsü**

`While` döngüsü, belirli bir koşul sağlandığı sürece kod bloğunu çalıştırır. Koşulun başta doğru olması gerekir, aksi takdirde döngü hiç çalışmayabilir.

**Syntax**

```solidity
while (condition) {
    // Döngü bloğu
}
```

**Örnek**

```solidity
function decrement(uint256 _n) public pure returns (uint256) {
    uint256 count = _n;
    while (count > 0) {
        count--;
    }
    return count;
}
```

Bu örnekte, `decrement` fonksiyonu `_n` değerinden başlar ve sıfıra kadar azaltır. `while` döngüsü, `count` sıfırdan büyük olduğu sürece çalışır ve her adımda `count` değişkenini bir azaltır.

## **3. Do-While Döngüsü**

`Do-While` döngüsü, kod bloğunu en az bir kez çalıştırır ve ardından koşulu kontrol eder. Koşul doğru olduğu sürece döngü devam eder.

**Syntax**

```solidity
do {
    // Döngü bloğu
} while (condition);
```

**Örnek**

```solidity
function increment(uint256 _n) public pure returns (uint256) {
    uint256 count = _n;
    do {
        count++;
    } while (count < 10);
    return count;
}
```

Bu örnekte, `increment` fonksiyonu `_n` değerinden başlayarak 10'a kadar artırır. `do-while` döngüsü, `count` değeri 10'dan küçük olduğu sürece çalışır ve her adımda `count` değişkenini bir artırır.

## **Örnek Uygulama**

Aşağıda, bir dizi üzerinde iterasyon yaparak her bir öğeyi işleyen bir kontrat örneği bulunmaktadır:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract LoopExample {
    uint256[] public numbers;

    function addNumbers(uint256[] memory _numbers) public {
        for (uint256 i = 0; i < _numbers.length; i++) {
            numbers.push(_numbers[i]);
        }
    }

    function sumNumbers() public view returns (uint256) {
        uint256 total = 0;
        for (uint256 i = 0; i < numbers.length; i++) {
            total += numbers[i];
        }
        return total;
    }
}
```

Bu kontratta:

* `addNumbers` fonksiyonu, verilen bir dizi sayıyı `numbers` dizisine ekler.
* `sumNumbers` fonksiyonu, `numbers` dizisindeki tüm sayıları toplar.
