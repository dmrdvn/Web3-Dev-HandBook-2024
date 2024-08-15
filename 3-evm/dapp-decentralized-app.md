---
icon: dice-d6
---

# DApp (Decentralized App)

Blockchain üzerinde çalışan ve merkeziyetsiz bir yapıya sahip uygulamalardır. Aslında akıllı sözleşmelerden farkı DApp'ler bir frontend'e yani ön yüzde sahiptirler.

Yani siz bir akıllı sözleşme yazdığınızda bunu blockchain üzerinde deploy edersiniz ve bu sözleşme belirli bir işlevi yerine getiren ve blokzincir üzerinde otomatik olarak yürütülen bir kod parçasından ibarettir fakat blockchain üzerindeki bir akıllı sözleşmeyle etkileşim kurabilmek için bir frontend eklediğinizde bir dApp yani merkeziyetsiz bir uygulama yapmış oluyorsunuz. \


Hatta dApp'ler genellikle bir veya daha fazla akıllı sözleşme kullanarak çalışır. Akıllı sözleşmeler, dApp'in arka ucunu (backend) oluştururken, dApp'in kendisi kullanıcı arayüzü (frontend) ile tamamlanır.

{% hint style="info" %}
Her dApp'in arkasında en az bir akıllı sözleşme bulunur, ancak her akıllı sözleşme bir dApp değildir. dApp'ler daha geniş bir kapsama sahiptir ve kullanıcı etkileşimini sağlarken, akıllı sözleşmeler genellikle dApp'in fonksiyonlarını yerine getiren bir alt bileşen olarak çalışır.
{% endhint %}

## Ethereum DApp Geliştirme Araç ve Teknolojileri

### Solidity

Ethereum üzerinde akıllı kontratlar (smart contracts) geliştirmek için kullanılan yüksek seviyeli, statik tipli bir programlama dilidir. Söz dizimi (syntax) olarak JavaScript'e benzer ve Ethereum Virtual Machine (EVM) üzerinde çalışmak üzere tasarlanmıştır.

### Hardhat

Ethereum geliştiricileri için bir geliştirme ortamı sunan güçlü bir araçtır. Test, deploy, hata ayıklama ve smart contract geliştirme süreçlerini kolaylaştırır. Akıllı kontratların yerel bir Ethereum ağı üzerinde test edilmesi, hataların düzeltilmesi ve dağıtım süreçlerinin yönetilmesi için kullanılır.&#x20;

### Ganache

Truffle Suite'in (truffle kullanımdan kalktı) bir parçası olan yerel bir blockchain simülatörüdür. Geliştiricilere, hızlı bir şekilde kendi özel Ethereum blockchain ağlarını kurma ve test etme imkanı sağlar. Bilgisayarınızda blockchain ağlarının benzerini çalıştırarak kontratınızı simüle etmenizi sağlar.

### Web3.js

Ethereum blockchain'i ile etkileşim kurmak için kullanılan JavaScript kütüphanesidir. Bu kütüphane, akıllı kontratlar ve Ethereum cüzdanları ile doğrudan etkileşim kurmanıza olanak tanır.

### Ethers.js

Ethereum blockchain'i ile etkileşim kurmak için hafif ve kullanımı kolay bir JavaScript kütüphanesidir. Web3.js'ye benzer işlevler sunar ancak modüler yapısı ve kapsamlı belgeleri ile dikkat çeker.

### Remix

Web tabanlı bir IDE (Integrated Development Environment) olup, Ethereum akıllı kontratlarının yazılması, test edilmesi ve dağıtılması için kullanılır. Kendi içerisinde bir Solidity derleyicisi ve çeşitli eklentiler sunar.&#x20;

Remix, Solidity kodunu gerçek zamanlı olarak derler ve testnet ya da mainnet üzerinde kontratları deploy etme olanağı sağlar.

### OpenZeppelin

Güvenli ve denetlenmiş (audited) Solidity kütüphaneleri ve akıllı kontratlar sunan bir platformdur. Özellikle ERC20, ERC721 gibi standart token kontratlarını içerir. Akıllı kontratları güvenli hale getirmek ve yaygın olarak kullanılan standartları uygulamak için OpenZeppelin kütüphaneleri sık sık kullanır.

### Infura

Ethereum node'ları çalıştırmak zorunda kalmadan blockchain ile etkileşim kurmanıza olanak tanıyan bir API hizmetidir. Altyapı hizmeti olarak sunulur.

### Alchemy

Ethereum ve diğer blockchain ağlarına erişim sağlayan bir altyapı hizmetidir. Ethereum ağı ile etkileşim kurmak için sağlam ve hızlı API'ler sunar. Geliştiriciler için blockchain verilerine erişim, işlem gönderme ve dApp performansını izleme gibi işlevler sağlar.

### Chainlink

Chainlink, akıllı kontratların dış veri kaynaklarıyla etkileşime girmesini sağlayan bir oracle hizmetidir. Akıllı kontratların dış dünyadan veri almasını ve bu verileri kullanarak işlemler gerçekleştirmesini sağlar. Örneğin Chainlink ile piyasa fiyatları veya hava durumu gibi gerçek dünya verilerini akıllı kontratlara entegre edebilirsiniz.

### The Graph

Blockchain verilerini sorgulamak ve indekslemek için kullanılan bir protokoldür. Akıllı kontratların ve blockchain verilerinin sorgulanmasını ve indekslenmesini sağlar. Verilerin hızlı ve verimli bir şekilde sorgulanmasına olanak tanır.
