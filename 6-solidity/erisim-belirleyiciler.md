# Erişim Belirleyiciler

Solidity'de erişim belirleyiciler, kontrattaki değişkenlerin ve fonksiyonların görünürlüğünü ve erişilebilirliğini kontrol etmek için kullanılır. Bu belirleyiciler, hangi kod parçalarının kontratın hangi bölümlerine erişebileceğini tanımlar.

## 1. `public`

* **Değişkenler için:** Değişken hem dışarıdan hem de kontrat içerisinden erişilebilir. Solidity, `public` olarak tanımlanan durum değişkenleri için arkaplanda otomatik getter fonksiyonları oluşturur.

```solidity
uint256 public publicDegisken = 10;
```

* **Fonksiyonlar için:** Fonksiyon dışarıdan (yani kontrat dışından) ve kontrat içerisinden çağrılabilir.

```solidity
function getValue() public view returns (uint256) {
    return value;
}
```

## 2. `private`

* **Değişkenler için:** Değişken yalnızca tanımlandığı kontratın içinden erişilebilir. Alt kontratlar bile bu değişkene doğrudan erişemez.

```solidity
uint256 private privateDegisken = 42;
```

* **Fonksiyonlar için:** Fonksiyon yalnızca tanımlandığı kontratın içinden çağrılabilir. Alt kontratlar ve dışarıdaki başka bir kontrat bu fonksiyonu çağırma yetkisine sahip değildir.

```solidity
function calculateSecret() private view returns (uint256) {
    return secretValue * 2;
}
```

## **3. `internal`**

* **Değişkenler için:** Değişken, tanımlandığı kontratın içinden ve bu kontratı miras alan (inheriting) kontratlar tarafından erişilebilir. Ancak dışarıdan doğrudan erişilemez.

```solidity
uint256 internal internalDegisken = 100;
```

* **Fonksiyonlar için:** Fonksiyon, tanımlandığı kontratın içinden ve bu kontratı miras alan kontratlar tarafından çağrılabilir. Dışarıdan erişim yoktur.

```solidity
function calculateInternal() internal view returns (uint256) {
    return internalValue * 10;
}
```

## **4. `external`**

* **Fonksiyonlar için:** Fonksiyon yalnızca kontrat dışından çağrılabilir. Kontratın içinde çağrılmak istendiğinde `this` anahtar kelimesi ile çağrılmalıdır. external genelde metamask ile arayüzden tetikleyeceğimiz fonksiyonlarda kullanılır.

```solidity
function externalFunction() external view returns (uint256) {
    return value;
}

function callExternal() public view returns (uint256) {
    return this.externalFunction();
}>
```

**Not:** `external` belirleyicisi değişkenler için kullanılamaz.

## Örnek Uygulama

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract AccessModifiersExample {
    // Public değişken
    uint256 public publicValue = 100;

    // Private değişken
    uint256 private privateValue = 200;

    // Internal değişken
    uint256 internal internalValue = 300;

    // Public fonksiyon
    function getPublicValue() public view returns (uint256) {
        return publicValue;
    }

    // Private fonksiyon
    function getPrivateValue() private view returns (uint256) {
        return privateValue;
    }

    // Internal fonksiyon
    function getInternalValue() internal view returns (uint256) {
        return internalValue;
    }

    // External fonksiyon
    function getExternalValue() external view returns (uint256) {
        return publicValue;
    }

    // Public fonksiyon, private fonksiyonu çağırır
    function callPrivateFunction() public view returns (uint256) {
        return getPrivateValue();
    }

    // Public fonksiyon, internal fonksiyonu çağırır
    function callInternalFunction() public view returns (uint256) {
        return getInternalValue();
    }
}

contract InheritedContract is AccessModifiersExample {
    // Internal fonksiyonu miras aldığımız kontrat üzerinden çağırabiliyoruz
    function accessInternal() public view returns (uint256) {
        return getInternalValue();
    }
}
```
