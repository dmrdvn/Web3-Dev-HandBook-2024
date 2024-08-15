# Struct & Enum

Solidity'de **Struct** ve **Enum** veri yapıları, daha karmaşık verileri ve durumları saklamak için kullanılır. Bu yapılar, akıllı kontratların daha düzenli ve okunabilir olmasına yardımcı olur.

## **1. Struct**

**Struct**, farklı veri tiplerini bir araya getirip tek bir yapı altında toplamak için kullanılır. Struct'lar, Solidity'de veriyi organize etmenin ve kompleks veri tiplerini yönetmenin güçlü bir yoludur.

```solidity
struct Person {
    string name;
    uint age;
    address wallet;
}
```

Yukarıdaki örnekte `Person` adlı struct, bir kişinin adını (`name`), yaşını (`age`) ve cüzdan adresini (`wallet`) saklar.

### **Struct Kullanımı**

Struct tanımladıktan sonra, bu yapıdan yeni veri oluşturabiliriz.

```solidity
Person public person1 = Person("Alice", 30, 0x1234567890123456789012345678901234567890);
```

Bu kodda, `person1` adında bir `Person` örneği oluşturulmuş ve bu örneğe Alice adında bir kişi atanmıştır.

### **Struct ile Fonksiyonlar**

Struct'lar, fonksiyonlar içinde parametre olarak kullanılabilir veya fonksiyonlardan döndürülebilir.

```solidity
function createPerson(string memory _name, uint _age, address _wallet) public returns (Person memory) {
    return Person(_name, _age, _wallet);
}
```

Bu fonksiyon, bir `Person` struct'ı oluşturur ve döndürür.

### **Struct'ları Depolama**

Struct'lar, mapping ve array gibi veri yapıları içerisinde depolanabilir. Bu, Solidity'de veri tabanı gibi kullanılabilecek güçlü bir yapıdır.

```solidity
mapping(uint => Person) public people;
uint public peopleCount;

function addPerson(string memory _name, uint _age, address _wallet) public {
    people[peopleCount] = Person(_name, _age, _wallet);
    peopleCount++;
}
```

Bu örnekte, `people` adlı bir mapping kullanarak birden fazla kişiyi saklayabilirsiniz.

## **2. Enum**

**Enum**, bir dizi sabit değeri tanımlamak için kullanılır. Özellikle belirli bir durum veya seçenek seti varsa, enum kullanmak kodu daha okunabilir hale getirir.

```solidity
enum Status { Pending, Shipped, Delivered, Canceled }
```

Bu enum, bir siparişin durumlarını saklamak için kullanılabilir: `Pending`, `Shipped`, `Delivered`, `Canceled`.

### **Enum Kullanımı**

Enum tanımlandıktan sonra, bir değişken olarak kullanılabilir:

```solidity
Status public currentStatus;

function setStatus(Status _status) public {
    currentStatus = _status;
}
```

Bu örnekte, `currentStatus` adlı bir enum değişkeni oluşturulmuş ve `setStatus` fonksiyonu ile bu durum ayarlanabilir.

### **Enum ile Koşullu Yapılar**

Enum'lar, koşullu yapılarda kullanılarak belirli işlemler gerçekleştirilirken durumların kontrol edilmesini sağlar:

```solidity
solidityKodu kopyalafunction shipOrder() public {
    require(currentStatus == Status.Pending, "Order cannot be shipped!");
    currentStatus = Status.Shipped;
}
```

Bu örnekte, `shipOrder` fonksiyonu yalnızca sipariş durumu `Pending` olduğunda çalışır ve durumu `Shipped` olarak günceller.

## **Örnek Uygulama**

Aşağıda, hem `Struct` hem `Mapping` hem de `Enum` kullanılarak oluşturulmuş bir örnek kontrat bulunmaktadır:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract StructEnumExample {
    // Enum tanımı
    enum Status { Pending, Shipped, Delivered, Canceled }
    
    // Struct tanımı
    struct Order {
        uint id;
        string item;
        uint quantity;
        Status status;
    }
    
    // Mapping ile siparişleri saklama
    mapping(uint => Order) public orders;
    uint public orderCount;

    // Yeni bir sipariş ekleme fonksiyonu
    function createOrder(string memory _item, uint _quantity) public {
        orders[orderCount] = Order(orderCount, _item, _quantity, Status.Pending);
        orderCount++;
    }
    
    // Sipariş durumunu güncelleme fonksiyonu
    function updateOrderStatus(uint _orderId, Status _status) public {
        Order storage order = orders[_orderId];
        order.status = _status;
    }

    // Siparişin mevcut durumunu kontrol etme fonksiyonu
    function getOrderStatus(uint _orderId) public view returns (Status) {
        return orders[_orderId].status;
    }
}
```

Bu örnekte, `StructEnumExample` adlı kontrat, siparişleri takip etmek için `Order` struct'ını ve sipariş durumlarını izlemek için `Status` enum'ını kullanır. Yeni siparişler eklenebilir, durumları güncellenebilir ve mevcut durumu kontrol edilebilir.
