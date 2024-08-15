# If Else Yapıları

**If-Else yapıları**, Solidity'de kodun belirli bir koşula bağlı olarak çalışmasını kontrol etmek için kullanılır. Bu yapılar, belirli koşullara göre farklı kod bloklarının çalışmasını sağlar ve programın akışını yönlendirir.

## **1. If-Else Yapısının Temel Kullanımı**

**If-Else** yapısı, bir koşulu kontrol eder ve bu koşul doğruysa bir kod bloğunu çalıştırır; aksi halde başka bir kod bloğunu çalıştırır.

**Temel Syntax:**

```solidity
if (condition) {
    // Koşul doğruysa çalışacak kod bloğu
} else {
    // Koşul yanlışsa çalışacak kod bloğu
}
```

**Örnek:**

```solidity
function checkValue(uint256 _value) public pure returns (string memory) {
    if (_value > 10) {
        return "Value is greater than 10";
    } else {
        return "Value is 10 or less";
    }
}
```

Bu örnekte, `_value` değişkeni 10'dan büyükse "Value is greater than 10" mesajı döndürülür, aksi takdirde "Value is 10 or less" mesajı döndürülür.

## **2. Else If Yapısı**

**Else If** yapısı, birden fazla koşulu kontrol etmek için kullanılır. İlk `if` koşulu sağlanmadığında, `else if` koşulları sırasıyla kontrol edilir.

**Syntax**

```solidity
if (condition1) {
    // Koşul 1 doğruysa çalışacak kod bloğu
} else if (condition2) {
    // Koşul 2 doğruysa çalışacak kod bloğu
} else {
    // Hiçbir koşul sağlanmazsa çalışacak kod bloğu
}
```

**Örnek**

```solidity
function evaluateNumber(uint256 _number) public pure returns (string memory) {
    if (_number > 100) {
        return "Number is greater than 100";
    } else if (_number > 50) {
        return "Number is greater than 50 but less than or equal to 100";
    } else {
        return "Number is 50 or less";
    }
}
```

Bu örnekte, `_number` değişkeni 100'den büyükse ilk mesaj döndürülür, 50 ile 100 arasında ise ikinci mesaj döndürülür, aksi takdirde üçüncü mesaj döndürülür.

## **3. Nested If-Else Yapıları**

**Nested If-Else** yapıları, iç içe geçmiş if-else bloklarını ifade eder. Bir if veya else bloğu içinde başka if-else blokları bulunabilir.

**Örnek**

```solidity
function checkRange(uint256 _value) public pure returns (string memory) {
    if (_value > 0) {
        if (_value < 50) {
            return "Value is between 1 and 50";
        } else if (_value < 100) {
            return "Value is between 51 and 100";
        } else {
            return "Value is greater than or equal to 100";
        }
    } else {
        return "Value is zero or negative";
    }
}
```

Bu örnekte, `_value` pozitifse ve 50'den küçükse birinci mesaj döndürülür, 50 ile 100 arasında ise ikinci mesaj döndürülür, 100 veya daha büyükse üçüncü mesaj döndürülür. `_value` sıfır veya negatifse son mesaj döndürülür.

## **Örnek Uygulama**

Aşağıda, bir kullanıcının rolüne göre farklı mesajlar döndüren bir kontrat örneği bulunmaktadır:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract RoleBasedAccess {
    address public admin;
    address public user;

    constructor() {
        admin = msg.sender;
    }

    function setUser(address _user) public {
        require(msg.sender == admin, "Only admin can set user");
        user = _user;
    }

    function checkAccess(address _address) public view returns (string memory) {
        if (_address == admin) {
            return "Admin access granted";
        } else if (_address == user) {
            return "User access granted";
        } else {
            return "Access denied";
        }
    }
}
```

Bu kontratta:

* `admin` ve `user` adresleri belirlenmiştir.
* `checkAccess` fonksiyonu, verilen adrese göre erişim durumunu kontrol eder ve uygun mesajı döndürür.
