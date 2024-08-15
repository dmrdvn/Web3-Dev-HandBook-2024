# Veri Tipleri

Solidity'de veri tipleri, akıllı kontratların verilerini nasıl saklayacağını ve işleyeceğini belirleyen temellerdir. Veri tipleri, kontratların güvenli ve optimize edilmiş bir şekilde çalışmasını sağlar.&#x20;

Veri tipleri iki ana kategoriye ayrılır: **Değer Tipleri (Value Types)** ve **Referans Tipleri (Reference Types)**.

## 1. Değer Tipleri (Value Types)

Değer tipleri, değişkenlerin kendisi üzerinde saklanır. Bu, değerin direkt olarak bellekte depolandığı anlamına gelir.

### Boolean (`bool`)

Boolean değişkeni tanımlarken en başta bool ifadesini belirtiyoruz, daha sonra değişken adını ve sonra da değişken değerini belirtiyoruz.\
Boolean iki değerden birini alabilir: `true` veya `false`.

```solidity
bool isActive = true;
```

### Integer (`int` ve `uint`)

Integer tam sayıları belirttiğimiz değişken türüdür. int veya uint olarak iki farklı versiyonu vardır.

`int`: İşaretli tamsayıları (negatif ve pozitif) saklar.

`uint`: İşaretsiz tamsayıları (sadece pozitif) saklar.

Hem `int` hem de `uint` için `8` ile `256` bit arasında seçim yapabilirsiniz (8'in katları olarak).\
Örneğin int8, int16, int32 ... int256 veya uint8, uint16, uint32,... uint256 gibi.

```solidity
int256 minValue = -500;
uint256 maxValue = 500;
```

{% hint style="info" %}
Blockchain'lerde genelde pozitif tam sayılar kullanıldığı için daha çok **uint** türünde integer değişkenler kullanacağız. Fakat nadirde olsa int türünde negatif tam sayılar kullanıldığı da olmaktadır.
{% endhint %}

### Address

`address`, bir Ethereum adresini saklamak için kullanılır. Genellikle kontrat adresleri veya kullanıcı adresleri bu tipte olur. \
Tanımlarken address değişken tipi belirtilir, değişken adı yazılır, son olarak da değişken değeri yazılır.

```solidity
address owner = 0x1234567890123456789012345678901234567890;
```

### Bytes

Solidity'de sabit veya değişken uzunlukta ham veri (raw data) saklamak için kullanılır. Verileri bayt cinsinden (byte) temsil eder ve genellikle düşük seviyeli işlemler, hashing işlemleri veya veri paketlerini saklamak için kullanılır.

Aslında string ile aynı işleve sahip olsalar da byte'ların farkı değişken üzerinde manipülasyona imkan tanımasıdır. Böyle durumlarda string değişkeni önce byte tipine dönüştürürüz ve manipülasyonu uygularız, son olarak string türüne geri dönüştürürüz.

&#x20;`bytes1`'den `bytes32`'ye kadar türleri vardır. Sadece `bytes` olarak yazıldığı durumlarda dinamik bir değişken olur.

```solidity
bytes32 data = "0x1234567890abcdef";
```

### Enum

Belirli bir dizi sabit değeri tanımlamak için kullanılır. Enum'lar, kodu daha okunabilir hale getirmek ve belirli bir veri kümesi arasında seçim yapmayı kolaylaştırmak için idealdir.\
Aslında enum'ların kullanım alanları daha geniş bir konu içeriği ama şimdilik `"1 veya 0 ile ifade ettiğimiz sabit durumların daha kolay ifade edilmesi için"` kullanıldığını bilmeniz yeterli olacaktır.

```solidity
enum Status { Pending, Active, Completed } //Tanımladık
Status currentStatus = Status.Pending; //Daha öncede tanımladığımız enum ı kullandık
```

## 2. Referans Tipleri (Reference Types)

Referans tipleri, bellek üzerinde saklanan verilere referans tutar. Bu tipler daha büyük veri yapıları için kullanılır.

### Arrays

Aynı türdeki elemanların sıralı bir listesidir.

```solidity
uint[] numbers = [1, 2, 3, 4];
```

### Structs

Farklı türdeki verileri tek bir yapıda saklamak için kullanılır.

```solidity
//Struct tanımladık
struct Person {
    string name;
    uint age;
}
//Tanımlanan Struct'ı kullanıyoruz
Person person = Person("Alice", 30);
```

### Mapping

İkili verileri key-value şeklinde saklar. Parametre olarak bir `key` verirsiniz ve size karşılığı olan `value` değerini döner. \
Örnekte balances mapping değişkenini kullanarak address tipinden bir parametre veriyoruz ve karşığında uint tipinde veri alıyoruz.

```solidity
mapping(address => uint) balances;
```

## Örnek Projeler

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract ExampleContract {
    // Boolean değişkeni
    bool public isActive = true;

    // İşaretsiz tamsayı değişkeni
    uint256 public balance = 1000;

    // Address değişkeni
    address public owner;

    // Bytes32 değişkeni
    bytes32 public data = "Merhaba";

    // Enum tanımı
    enum Status { Pending, Active, Completed }
    Status public currentStatus;

    // Struct tanımı
    struct Person {
        string name;
        uint age;
    }
    Person public person;

    // Mapping tanımı
    mapping(address => uint) public balances;

    // Constructor (başlatıcı) fonksiyonu
    constructor() {
        owner = msg.sender;
        person = Person("Alice", 30);
        currentStatus = Status.Pending;
        balances[owner] = balance;
    }
}
```
