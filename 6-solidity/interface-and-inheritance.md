# Interface & Inheritance

**Interface** ve **Inheritance** (kalıtım), Solidity'de kodun yeniden kullanılabilirliğini ve modülerliğini artırmak için kullanılan güçlü araçlardır. Bu özellikler, akıllı kontratları daha esnek ve yönetilebilir hale getirir.

## **1. Interface**

**Interface**, bir kontratın başka bir kontrat veya dış bir sistemle nasıl etkileşime gireceğini tanımlayan bir yapıdır. Interface'ler sadece fonksiyon başlıklarını içerir, fonksiyonların nasıl çalıştığı hakkında bilgi vermez. Interface'ler, diğer kontratların belirli bir arayüzü izlemesini sağlar ve fonksiyonların hangi isimlere sahip olduğunu ve parametrelerin neler olduğunu belirtir.&#x20;

Bir interface tanımlarken sadece fonksiyonun adı ve parametreleri yazılır, fonksiyon içeriği yazılmaz.

**Syntax**

```solidity
interface IExample {
    function doSomething(uint256 _value) external returns (bool);
}
```

Bu örnekte, `IExample` adında bir interface tanımlanmış ve `doSomething` fonksiyonu için başlık verilmiştir. Bu fonksiyonun nasıl çalıştığı hakkında bilgi içermez.

**Interface Kullanımı**

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

interface ICalculator {
    function add(uint256 a, uint256 b) external pure returns (uint256);
}

contract CalculatorUser {
    ICalculator public calculator;

    constructor(address _calculatorAddress) {
        calculator = ICalculator(_calculatorAddress);
    }

    function calculateSum(uint256 a, uint256 b) public view returns (uint256) {
        return calculator.add(a, b);
    }
}
```

Bu örnekte:

* `ICalculator` adında bir interface tanımlanmıştır.
* `CalculatorUser` kontratı, bu interface'i kullanarak başka bir kontratın `add` fonksiyonunu çağırır.

## **2. Inheritance (Kalıtım)**

**Inheritance**, bir kontratın başka bir kontratın özelliklerini ve fonksiyonlarını miras almasını sağlar. Bu, kodun yeniden kullanılabilirliğini artırır ve kodun daha modüler olmasını sağlar. Kalıtım, bir kontratın başka bir kontratın tüm fonksiyonlarını ve durum değişkenlerini devralmasını sağlar.

**Syntax**

```solidity
contract Parent {
    uint256 public value;

    function setValue(uint256 _value) public {
        value = _value;
    }
}

contract Child is Parent {
    function doubleValue() public view returns (uint256) {
        return value * 2;
    }
}
```

Bu örnekte:

* `Parent` kontratı bir `value` değişkeni ve `setValue` fonksiyonunu içerir.
* `Child` kontratı, `Parent` kontratını miras alır ve `value` değişkenine ve `setValue` fonksiyonuna erişebilir. Ayrıca `doubleValue` adında bir fonksiyon ekler.

## **3. Çoklu Kalıtım**

Solidity'de bir kontrat birden fazla kontratı miras alabilir. Bu, çoklu kalıtım olarak bilinir ve çeşitli arayüzler veya kontratlar arasında kod paylaşımını sağlar.

**Syntax**

```solidity
contract Base1 {
    function func1() public pure returns (string memory) {
        return "Base1";
    }
}

contract Base2 {
    function func2() public pure returns (string memory) {
        return "Base2";
    }
}

contract Derived is Base1, Base2 {
    function func3() public pure returns (string memory) {
        return "Derived";
    }
}
```

Bu örnekte:

* `Derived` kontratı, hem `Base1` hem de `Base2` kontratlarını miras alır ve her iki kontratın fonksiyonlarına erişebilir.

## **Örnek Uygulama**

Aşağıda, bir akıllı kontratın arayüzü ve kalıtım özelliklerini kullanan bir örnek bulunmaktadır:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

// Interface tanımı
interface IStore {
    function set(uint256 _value) external;
    function get() external view returns (uint256);
}

// Base kontrat
contract Storage {
    uint256 private value;

    function set(uint256 _value) public {
        value = _value;
    }

    function get() public view returns (uint256) {
        return value;
    }
}

// Derived kontrat
contract EnhancedStorage is Storage, IStore {
    function increment(uint256 _value) public {
        uint256 current = get();
        set(current + _value);
    }
}
```

Bu örnekte:

* `IStore` adında bir interface tanımlanmış ve `set` ve `get` fonksiyonları için başlık verilmiştir.
* `Storage` kontratı, `value` değişkenini saklar ve bu değeri ayarlamak ve almak için fonksiyonlar içerir.
* `EnhancedStorage` kontratı, hem `Storage` kontratını hem de `IStore` arayüzünü miras alır ve `increment` fonksiyonunu ekler.
