---
icon: wallet
---

# Web3.js

Web3.js de EVM üzerindeki blockchain ağları ile etkileşim kurmak için kullanılan bir diğer popüler JavaScript kütüphanesidir.&#x20;

DApp (Decentralized Application) geliştiricileri tarafından, smart contract'ler ile etkileşim, hesapların yönetimi, işlemlerin gönderilmesi ve blockchain verilerinin alınması gibi görevler için yaygın olarak kullanılır.

## 1 - Kurulum

Web3.js kütüphanesinin kurulumu için öncelikle bağımlılıkları projenize import etmeniz gerekmektedir.

```bash
npm install web3
//veya
yarn add web3
```

## 2 - Web3.js ile Temel İşlemler

### Web3.js'i Projeye Dahil Etmek

Web3.js kurulumu yaptıktan sonra akıllı sözleşmenizin en üstünde kullandığınız frameworke göre (react.js, next.js, vanillaJS) aşağıdaki komutlardan uygun olanını kullanabilirsiniz.

```javascript
const Web3 = require('web3');
// veya ES6 modülleri kullanıyorsanız
import Web3 from 'web3';
```

### Bir Ethereum Cüzdanı Oluşturma

Akıllı sözleşmemizde `create()` fonksiyonu ile yeni bir cüzdan oluşturabiliriz.

```javascript
const account = web3.eth.accounts.create();
console.log(`Address: ${account.address}`);
console.log(`Private Key: ${account.privateKey}`);
```

### Bir Cüzdanı Mevcut Bir Private Key ile İçe Aktarma

Oluşturduğumuz cüzdan adresini ve private key'i import etmemiz gerektiği durumlar olabilir.

```javascript
const privateKey = "PRIVATE_KEY";
const wallet = new ethers.Wallet(privateKey);
console.log(`Address: ${wallet.address}`);
```

### Bir Ethereum Node'una Bağlanma

Web3.js, farklı provider'larla çalışabilir. Örneğin, Infura veya Alchemy gibi bir servis sağlayıcı ile Ethereum blockchain'e bağlanabilirsiniz.

```javascript
// Infura kullanarak bir provider oluşturma
const web3 = new Web3(new Web3.providers.HttpProvider("https://mainnet.infura.io/v3/YOUR_INFURA_PROJECT_ID"));
```

### Bir Hesap Bakiyesini Kontrol Etme

```javascript
web3.eth.getBalance("0xAdresGir").then((balance) => {
    console.log(`Balance: ${web3.utils.fromWei(balance, 'ether')} ETH`);
});
```

### Bir Varlık Gönderme İşlemi/Transaction

Metamask arayüzünü kullanmadan kontrat üzerinden bakiye transferi de yapabilirsiniz.

```javascript
const tx = {
    from: '0xGönderenAdres',
    to: '0xAlıcıAdres',
    value: web3.utils.toWei('0.01', 'ether'), // Gönderilecek ETH miktarı
    gas: 21000
};

web3.eth.accounts.signTransaction(tx, 'YOUR_PRIVATE_KEY').then((signedTx) => {
    web3.eth.sendSignedTransaction(signedTx.rawTransaction).then((receipt) => {
        console.log(`Transaction Hash: ${receipt.transactionHash}`);
    });
});
```

### Bir Smart Contract ile Etkileşim

Kullanıcılarınız akıllı sözleşmeleriniz ile sitenin ön yüzünden etkileşime geçebilmesi için web3.js de mükemmel bir araçtır. Tek lazım olan akıllı sözleşme adresi ve ABI kodu.

Sözleşmenizi deploy ederken otomatik oluşturulan bir `ABI kodu` bulunmaktadır. Bu ABI kodunu ister `contractABI` kısmına ekleyebilir isterseniz de bunu harici bir dosyadan çağırabilirsiniz.

```javascript
const contractABI = [
    // ABI burada olmalı
];
const contractAddress = "0xKontratAdresi";
const contract = new web3.eth.Contract(contractABI, contractAddress);

// Örneğin bir fonksiyonu çağırmak için
contract.methods.someFunction().call().then((result) => {
    console.log(result);
});
```

## 3 - Web3.js Ekstra Araçlar ve Yardımcı Fonksiyonlar

### BigNumber Kullanımı

Akıllı sözleşmelerde birimler ifade edilirken `Wei` kullanılır. Bu nedenle sayılar çok büyük olmakta ve bu yüzden BigNumber hatası almaktayız.&#x20;

{% hint style="info" %}
1 ether = 1000000000000000000 wei (19 hane)
{% endhint %}

Burada Web3.js'in bize sağladığı yerleşik BigNumber dönüşümü sayesinde büyük sayılarla çalışabilmekteyiz.

```javascript
const bigNumber = web3.utils.toBN('1000000000000000000');
console.log(bigNumber.toString()); // 1000000000000000000
```

### Event Dinleme

Bir akıllı sözleşmenin veya bireysel bir hesabın event'lerini aşağıdaki yöntemle dinleyebiliriz.

```javascript
contract.events.Transfer({
    filter: {value: web3.utils.toWei('100', 'ether')}, // Değeri 100 ETH olan transferleri dinleme
    fromBlock: 0
}, (error, event) => {
    if (!error) {
        console.log(event);
    }
});
```

### Hash Oluşturma

```javascript
const hash = web3.utils.sha3('Hello, World!');
console.log(hash);
```
