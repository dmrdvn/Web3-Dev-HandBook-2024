---
icon: wallet
---

# Particle Network

Particle Network'ü web3.js ve ethers.js den ayıran bazı farklılıklar mevcut.&#x20;

Sadece bir provider ve cüzdan yönetiminden ziyade web3 projeleri için kimlik doğrulama, ipfs, analytics ve kullanıcı deneyimi gibi özellikler sunan bir platformdur. Kullanıcılar, Web3 projelerinde güvenli bir şekilde oturum açabilir, kripto cüzdanlarını yönetebilir ve blockchain uygulamalarıyla etkileşime geçebilir.&#x20;

Bu platform, geliştiricilere entegre edilebilir SDK'lar ve API'ler sağlar.

## 1 - Kurulum

```bash
npm install @particle-network/auth
//veya
yarn add @particle-network/auth
```

Particle Network'ü projeye dahil ettikten sonra kimlik doğrulama ve cüzdan yönetimi gibi temel işlemleri gerçekleştirebilirsiniz.

## 2 - Particle Network SDK'sini Projeye Dahil Etmek

```javascript
import { ParticleNetwork } from '@particle-network/auth';
```

## 3 - Particle Network Temel İşlemler

### Particle Network Başlatma

Particle Network'ü kullanmaya başlamak için öncelikle bir `ParticleNetwork` örneği oluşturmanız gerekmektedir. Bu aşamada, Particle Network'ü yapılandırmak için gerekli bilgileri (API anahtarı, ortam bilgileri vb.) girmeniz gerekecek.

`projectId`, `clientKey`, `appId` gibi bilgileri [buradan](https://dashboard.particle.network/#/login) platforma giriş yaparak edinebilirsini.

```javascript
const particle = new ParticleNetwork({
    projectId: 'YOUR_PROJECT_ID', // Particle Dashboard'dan alabilirsiniz
    clientKey: 'YOUR_CLIENT_KEY', // Particle Dashboard'dan alabilirsiniz
    appId: 'YOUR_APP_ID',         // Particle Dashboard'dan alabilirsiniz
    network: 'mainnet',           // veya 'testnet'
    chainId: 1                    // Ethereum mainnet için 1, diğer ağlar için uygun chain ID'sini kullanın
});
```

### Kullanıcı Oturumu Açma

Kullanıcılar, çeşitli yöntemlerle Particle Network üzerinden oturum açabilirler. Örneğin, e-posta ve şifre ile oturum açabilir.

```javascript
particle.auth.loginWithEmailAndPassword('user@example.com', 'password123')
    .then(user => {
        console.log('Kullanıcı oturum açtı:', user);
    })
    .catch(error => {
        console.error('Oturum açma hatası:', error);
    });
```

### Kullanıcı Kayıt Olma

Yeni kullanıcılar Particle Network üzerinden kayıt olabilir.

```javascript
particle.auth.registerWithEmailAndPassword('newuser@example.com', 'password123')
    .then(user => {
        console.log('Yeni kullanıcı kayıt oldu:', user);
    })
    .catch(error => {
        console.error('Kayıt hatası:', error);
    });
```

**Kullanıcı Oturumunu Kontrol Etme**

Kullanıcının oturumunun açık olup olmadığını kontrol edebilirsiniz.

```javascript
const currentUser = particle.auth.currentUser;
if (currentUser) {
    console.log('Kullanıcı oturum açtı:', currentUser);
} else {
    console.log('Hiçbir kullanıcı oturum açmadı.');
}
```

**Kullanıcı Oturumunu Kapatma**

Kullanıcı oturumunu kapatmak için.

```javascript
particle.auth.logout()
    .then(() => {
        console.log('Kullanıcı oturumu kapattı');
    })
    .catch(error => {
        console.error('Oturum kapatma hatası:', error);
    });
```

## Bu kısım devam edecek...
