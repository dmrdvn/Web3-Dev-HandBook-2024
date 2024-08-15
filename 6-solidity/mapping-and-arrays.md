# Mapping & Arrays

Solidity'de **Mapping** ve **Array** yapıları, verileri organize etmek ve saklamak için kullanılan temel veri yapılarıdır. Bu yapılar, kontrat içinde depolanan bilgileri kolayca yönetmenize olanak tanır.

## **1. Mapping**

**Mapping** (haritalama), anahtar-değer (key-value) çiftleri olarak verileri saklayan bir veri yapısıdır. Solidity'de mapping, bir tür veri tabanı gibi çalışır ve genellikle kontratlarda sıkça kullanılır.

### **Mapping Tanımı**

```solidity
mapping(address => uint) public balances;
```

Bu örnekte, `balances` adında bir mapping tanımlanmıştır. Bu mapping, her bir adres için bir `uint` değeri saklar.

### **Mapping Kullanımı**

Mapping'ler, belirli bir anahtara karşılık gelen değeri saklamak ve bu değere erişmek için kullanılır.

```solidity
function updateBalance(address _account, uint _amount) public {
    balances[_account] = _amount;
}

function getBalance(address _account) public view returns (uint) {
    return balances[_account];
}
```

Bu örnekte, `updateBalance` fonksiyonu belirli bir adresin bakiyesini güncellerken, `getBalance` fonksiyonu o adresin mevcut bakiyesini döndürür.

### **Mapping'in Özellikleri**

* Mapping'ler varsayılan olarak her anahtar için `0` değerini döndürür. Bu, mapping'de var olmayan bir anahtar sorgulandığında da geçerlidir.
* Mapping'ler üzerinde iterasyon (döngü) yapılamaz. Yani, mapping'deki tüm anahtar-değer çiftlerini topluca almak için bir yol yoktur.

## **2. Arrays (Diziler)**

**Array** (dizi), aynı veri türündeki öğelerin bir listesini saklayan bir veri yapısıdır. Solidity'de diziler, sabit boyutlu (`fixed-size`) veya dinamik boyutlu (`dynamic-size`) olabilir.

### **Array Tanımı**

```solidity
uint[] public numbers; // Dinamik boyutlu dizi
uint[5] public fixedNumbers; // Sabit boyutlu dizi (5 elemanlı)
```

Bu örnekte, `numbers` dinamik boyutlu bir dizi, `fixedNumbers` ise sabit boyutlu bir dizidir.

### **Array Kullanımı**

Dizilere eleman ekleyebilir, elemanlara erişebilir ve elemanları güncelleyebilirsiniz.

```solidity
function addNumber(uint _number) public {
    numbers.push(_number); // Diziye eleman ekleme
}

function getNumber(uint _index) public view returns (uint) {
    return numbers[_index]; // Belirli bir indekste bulunan elemanı getirme
}

function updateNumber(uint _index, uint _number) public {
    numbers[_index] = _number; // Belirli bir indeksi güncelleme
}
```

Bu örnekte, `addNumber` fonksiyonu bir sayıyı diziye ekler, `getNumber` belirli bir indeksteki sayıyı döndürür ve `updateNumber` belirli bir indeksteki sayıyı günceller.

### **Array'lerin Özellikleri**

* Dinamik boyutlu diziler `push` ve `pop` gibi fonksiyonlarla genişletilebilir veya daraltılabilir.
* Sabit boyutlu dizilerde dizinin boyutu derleme zamanında belirlenir ve sonradan değiştirilemez.

## **3. Mapping & Array Kombinasyonu**

Mapping ve Array veri yapıları, genellikle daha karmaşık veri yönetimi için bir arada kullanılabilir. Örneğin, belirli adreslerin bir dizi değerini saklamak isteyebilirsiniz.

**Örnek:**

```solidity
mapping(address => uint[]) public userScores;

function addUserScore(address _user, uint _score) public {
    userScores[_user].push(_score);
}

function getUserScores(address _user) public view returns (uint[] memory) {
    return userScores[_user];
}
```

Bu örnekte, `userScores` mapping'i, her bir kullanıcı için bir dizi puan saklar. `addUserScore` fonksiyonu, belirli bir kullanıcıya puan eklerken, `getUserScores` fonksiyonu o kullanıcının puanlarını döndürür.

## **Örnek Uygulama**

Aşağıda, mapping ve array'lerin kullanıldığı bir örnek kontrat bulunmaktadır:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract MappingAndArrayExample {
    // Bir kullanıcının sahip olduğu tokenları saklayan mapping
    mapping(address => uint[]) public tokensOwned;

    // Yeni bir token ekleyen fonksiyon
    function addToken(uint _tokenId) public {
        tokensOwned[msg.sender].push(_tokenId);
    }

    // Belirli bir kullanıcının sahip olduğu tokenları döndüren fonksiyon
    function getTokens(address _owner) public view returns (uint[] memory) {
        return tokensOwned[_owner];
    }

    // Kullanıcının belirli bir tokena sahip olup olmadığını kontrol eden fonksiyon
    function ownsToken(address _owner, uint _tokenId) public view returns (bool) {
        uint[] memory tokens = tokensOwned[_owner];
        for (uint i = 0; i < tokens.length; i++) {
            if (tokens[i] == _tokenId) {
                return true;
            }
        }
        return false;
    }
}
```

Bu kontrat, bir kullanıcının sahip olduğu tokenları saklamak için hem array hem de mapping veri yapılarını kullanır. Kullanıcılar yeni tokenlar ekleyebilir ve sahip oldukları tokenları sorgulayabilir.
