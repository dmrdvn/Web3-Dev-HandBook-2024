---
icon: wallet
---

# Ethers.js

Ethers.js, EVM üzerindeki blockchainler ile etkileşime geçmek için kullanılan hafif ve kullanıcı dostu bir JavaScript kütüphanesidir. Akıllı Kontratlar ile iletişim kurmak, hesapları yönetmek, işlemler gerçekleştirmek ve blockchain verilerini almak gibi birçok işlemi kolayca yapmanıza olanak sağlar.

## 1 - Kurulum

Ethers kütüphanesinin kurulumu için öncelikle bağımlılıkları projenize import etmeniz gerekmektedir.

```bash
npm install --save ethers
//veya
yarn add ethers
```

## 2 - Ethers.js ile Temel İşlemler

### Ethers.js'i Projeye Dahil Etmek

Ethers.js kurulumu yaptıktan sonra akıllı sözleşmenizin en üstünde kullandığınız frameworke göre (react.js, next.js, vanillaJS) aşağıdaki komutlardan uygun olanını kullanabilirsiniz.

```javascript
const { ethers } = require("ethers");
// veya ES6 modülleri kullanıyorsanız
import { ethers } from "ethers";
```

### Bir Ethereum Cüzdanı Oluşturma

Akıllı sözleşmemizde `createRandom()` fonksiyonu ile yeni bir cüzdan oluşturabiliriz.

```javascript
// Rastgele bir cüzdan oluşturma
const wallet = ethers.Wallet.createRandom();
console.log(`Address: ${wallet.address}`);
console.log(`Private Key: ${wallet.privateKey}`);
```

### Bir Cüzdanı Mevcut Bir Private Key ile İçe Aktarma

Oluşturduğumuz cüzdan adresini ve private key'i import etmemiz gerektiği durumlar olabilir.

```javascript
const privateKey = "PRIVATE_KEY";
const wallet = new ethers.Wallet(privateKey);
console.log(`Address: ${wallet.address}`);
```

### Bir Ethereum Node'una Bağlanma

Ethers.js, farklı provider'larla çalışabilir. Örneğin, Infura veya Alchemy gibi bir servis sağlayıcı ile Ethereum blockchain'e bağlanabilirsiniz.

```javascript
const provider = new ethers.providers.InfuraProvider("homestead", "INFURA_PROJECT_ID");
// veya
const provider = new ethers.providers.AlchemyProvider("homestead", "ALCHEMY_API_KEY");
```

### Bir Hesap Bakiyesini Kontrol Etme

```javascript
const address = "0xAdresGir";
provider.getBalance(address).then((balance) => {
    console.log(`Balance: ${ethers.utils.formatEther(balance)} ETH`);
});
```

### Bir Varlık Gönderme İşlemi/Transaction

Metamask arayüzünü kullanmadan kontrat üzerinden bakiye transferi de yapabilirsiniz.

```javascript
const tx = {
    to: "0xAlıcıAdresi",
    value: ethers.utils.parseEther("0.01") // Gönderilecek ETH miktarı
};

wallet.connect(provider).sendTransaction(tx).then((transaction) => {
    console.log(`Transaction Hash: ${transaction.hash}`);
});
```

### Bir Smart Contract ile Etkileşim

Kullanıcılarınız akıllı sözleşmeleriniz ile sitenin ön yüzünden etkileşime geçebilmesi için ethers.js mükemmel bir araçtır. Sözleşmenizi deploy ederken otomatik oluşturulan bir `ABI kodu` bulunmaktadır. Bu ABI kodunu ister `contractABI` kısmına ekleyebilir isterseniz de bunu harici bir dosyadan çağırabilirsiniz.

```javascript
const contractABI = [
    // ABI burada olmalı
];
const contractAddress = "0xKontratAdresi";
const contract = new ethers.Contract(contractAddress, contractABI, provider);

// Örneğin bir fonksiyonu çağırmak için
contract.someFunction().then((result) => {
    console.log(result);
});
```

## 3 - Ethers.js ile Ekstra Araçlar ve Yardımcı Fonksiyonlar

### BigNumber Kullanımı

Akıllı sözleşmelerde birimler ifade edilirken `Wei` kullanılır. Bu nedenle sayılar çok büyük olmakta ve bu yüzden BigNumber hatası almaktayız.&#x20;

{% hint style="info" %}
1 ether = 1000000000000000000 wei (19 hane)
{% endhint %}

Burada ethers.js'in bize sağladığı yerleşik BigNumber dönüşümü sayesinde büyük sayılarla çalışabilmekteyiz.

```javascript
const bigNumber = ethers.BigNumber.from("1000000000000000000");
console.log(bigNumber.toString()); // 1000000000000000000
```

### Event Dinleme

Bir akıllı sözleşmenin veya bireysel bir hesabın event'lerini aşağıdaki yöntemle dinleyebiliriz.

```javascript
contract.on("Transfer", (from, to, value) => {
    console.log(`${from} -> ${to} : ${ethers.utils.formatEther(value)} ETH`);
});
```
