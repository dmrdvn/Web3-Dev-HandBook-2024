# Fonksiyonlar

Solidity'de fonksiyonlar, bir kontratın temel yapı taşlarından biridir. Fonksiyonlar, belirli görevleri yerine getirmek için kod blokları olarak tanımlanır ve bu görevler yerine getirilirken kontratın durumunu değiştirebilir veya veri döndürebilir. Fonksiyonlar, Solidity'de mantığın ve işlemlerin organize edilmesi için kritik bir rol oynar.

## **1. Fonksiyon Tanımı**

Bir fonksiyon, `function` anahtar kelimesi ile tanımlanır. Fonksiyonlar, isteğe bağlı olarak parametreler alabilir ve belirli bir türde veri döndürebilir.

**Basit Bir Fonksiyon Örneği**

```solidity
function add(uint a, uint b) public pure returns (uint) {
    return a + b;
}
```

Bu örnekte, `add` adlı bir fonksiyon tanımlanmıştır. Bu fonksiyon, bir `uint` değeri döndürür ve herhangi bir parametre almaz.

### **Fonksiyonun Parçaları**

* **Fonksiyon İsmi:** Fonksiyonun ismi, `function` anahtar kelimesinden sonra gelir. Örneğin, yukarıdaki örnekte `add` fonksiyon ismidir.
* **Parametreler:** Parantez içinde yer alır ve fonksiyonun işlem yapması için gerekli olan verileri tanımlar. Yukarıdaki örnekte, `uint a` ve `uint b` parametrelerdir.
* **Erişim Belirleyicisi:** Fonksiyonun hangi kapsamda erişilebilir olduğunu belirler (örneğin `public`, `private`, `internal`, `external`).
* **Fonksiyon Türü:** `pure`, `view`, `payable` gibi türlerle fonksiyonun kontratın durumunu değiştirip değiştirmediği veya para transferi yapıp yapmadığı belirtilir.
* **Dönüş Türü:** `returns` ifadesi ile fonksiyonun döndürdüğü veri türü belirtilir. Yukarıdaki örnekte, `uint` veri türü döndürülmektedir.

## 2. Fonksiyon Türleri

Fonksiyonların hangi amaçla kullanıldığını ve nasıl çalıştığını belirten farklı türleri vardır:

*   **Pure Fonksiyonlar:** Kontratın durumunu değiştirmeyen ve blok zincirine veri yazmayan fonksiyonlardır. Yalnızca hesaplama yaparlar. Blockchain verilerini okuyamazlar.

    ```solidity
    function multiply(uint a, uint b) public pure returns (uint) {
        return a * b;
    }
    ```
*   **View Fonksiyonlar:** Kontratın durumunu değiştirmeyen ancak durumu okuyabilen fonksiyonlardır. Bu tür fonksiyonlar, blok zincirinden veri okur.

    ```solidity
    uint public x = 10;

    function getX() public view returns (uint) {
        return x;
    }
    ```
*   **Payable Fonksiyonlar:** Ether veya diğer kripto paraları kontrata göndermek için kullanılan fonksiyonlardır. `payable` anahtar kelimesiyle belirtilir.

    ```solidity
    function deposit() public payable {
        // Ether kontrata gönderildi
    }
    ```

## **3. Erişim Belirleyiciler**

Fonksiyonlara erişim, `public`, `private`, `internal` ve `external` gibi belirleyicilerle kontrol edilir:

*   **public:** Herkesten erişime açıktır. Kontratın dışından ve içinden çağrılabilir.

    ```solidity
    function publicFunction() public {
        // Her yerden erişilebilir
    }
    ```
*   **private:** Yalnızca tanımlandığı kontrat içinde erişilebilir. Kontratın dışından erişim mümkün değildir.

    ```solidity
    function privateFunction() private {
        // Sadece bu kontrat içinde erişilebilir
    }
    ```
*   **internal:** Yalnızca tanımlandığı kontrat ve ondan türetilen kontratlar tarafından erişilebilir.

    ```solidity
    function internalFunction() internal {
        // Bu kontrat ve türetilen kontratlar erişebilir
    }
    ```
*   **external:** Yalnızca kontratın dışından çağrılabilir. Kontratın içinden çağrılmak istenirse, `this.externalFunction()` şeklinde çağrılmalıdır.

    ```solidity
    function externalFunction() external {
        // Sadece kontrat dışından erişilebilir
    }
    ```

## **4. Fonksiyon Aşırı Yükleme (Overloading)**

Solidity, aynı isme sahip ancak farklı parametre türlerine sahip birden fazla fonksiyon tanımlamaya izin verir. Bu konsepte **fonksiyon aşırı yükleme** (overloading) denir.

**Örnek:**

```solidity
function calculate(uint a) public pure returns (uint) {
    return a * 2;
}

function calculate(uint a, uint b) public pure returns (uint) {
    return a + b;
}
```

Bu örnekte, `calculate` isimli iki farklı fonksiyon tanımlanmıştır. İlki bir parametre alır ve onu 2 ile çarparken, ikincisi iki parametre alır ve bunları toplar.

## **5. Fonksiyon Modifiers**

Fonksiyon modifiyerleri, fonksiyonların çalışma şeklini değiştiren veya belirli bir mantık ekleyen özel yapılardır. Modifiyerler, fonksiyonlar çağrılmadan önce ön koşulları kontrol etmek için kullanılır.

**Örnek:**

```solidity
//Ön koşul yani modifier'ı burada tanımlıyoruz.
modifier onlyOwner() {
    // owner msg.sender'a eşitse fonksiyonu çalıştır, değilse hata fırlat.
    require(msg.sender == owner, "Not the contract owner");
    _;
}
//Ön koşulu yani modifier'ı fonksiyon oluştururken ekledik.
function restrictedFunction() public onlyOwner { 
    // Sadece msg.sender owner'a eşitse bu fonksiyon çağırılabilir
}
```

Bu örnekte, `onlyOwner` modifiyeri, fonksiyonu yalnızca kontrat sahibi (`owner`) tarafından çağrılabilecek şekilde sınırlar.

{% hint style="info" %}
Burada msg.sender o andaki işlemi imzalayan kişiyi ifade eden, önceden tanımlanmış global bir değişkendir. Solidity'de varsayılan olarak gelir.
{% endhint %}

## **Örnek Uygulama**

Aşağıda, fonksiyonların farklı türlerini ve modifiyerleri gösteren bir örnek kontrat bulunmaktadır:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract FunctionExample {
    address public owner;
    uint public data;

    constructor() {
        owner = msg.sender;
    }

    modifier onlyOwner() {
        require(msg.sender == owner, "Not the contract owner");
        _;
    }

    function setData(uint _data) public onlyOwner {
        data = _data;
    }

    function getData() public view returns (uint) {
        return data;
    }

    function multiply(uint a, uint b) public pure returns (uint) {
        return a * b;
    }

    function deposit() public payable {
        // Ether kontrata gönderildi
    }
}
```

Bu kontratta, `setData` fonksiyonu yalnızca kontrat sahibi tarafından çağrılabilirken, `getData` fonksiyonu kontrattaki veriyi okuyabilir. `multiply` fonksiyonu ise yalnızca bir hesaplama yapar.
