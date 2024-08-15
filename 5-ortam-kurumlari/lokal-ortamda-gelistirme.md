---
icon: desktop
---

# Lokal Ortamda Geliştirme

## NodeJS ve NPM

Bilgisayar üzerinden kontrat deploy edebilmek için bazı kurulumlara ihtiyacımız bulunmaktadır. Öncelikle bir paket yöneticisine ihtiyacımız var. Aşağı bölümde iki farklı işletim sistemi için de indirme linkleri mevcut. Buradan size uygun olan adımı seçerek indirme ve kuruluma devam edebilirsiniz.

{% tabs %}
{% tab title="MacOS" %}
* [Node.js resmi web sitesinden](https://nodejs.org/) MacOS için Node.js'in LTS (Long Term Support) sürümünü indirin.
* İndirilen `.pkg` dosyasını çalıştırarak Node.js ve npm’i kurun.
* Kurulum tamamlandıktan sonra, Terminal'i açın ve aşağıdaki komutları kullanarak Node.js ve npm’in başarıyla kurulduğunu kontrol edin. Versiyon bilgisi geliyorsa kurulum tamamdır.

```bash
node -v
npm -v
```
{% endtab %}

{% tab title="Windows" %}
* [Node.js resmi web sitesinden](https://nodejs.org/) Windows için Node.js'in LTS (Long Term Support) sürümünü indirin.
* İndirilen `.msi` dosyasını çalıştırarak Node.js ve npm’i kurun.
* Kurulum tamamlandıktan sonra, Komut İstemcisi'ni açın ve aşağıdaki komutları kullanarak Node.js ve npm’in başarıyla kurulduğunu kontrol edin:

```bash
node -v
npm -v
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Tüm kodlama işlemlerini VS Code üzerinde yapacağımız için eğer indirmediyseniz [buradan](https://code.visualstudio.com/) VS Code uygulamasını bilgisayarınıza indiriniz.
{% endhint %}

## Hardhat Kurulumu

Paket yöneticisini kullanarak Hardhat'i bilgisayarımıza kuracağız.

Bilgisayarınızda terminal/konsol'u açarak bir dizin oluşturunuz.

```bash
mkdir helloSolidity
```

Daha sonra oluşturduğunuz proje dizinine giderek, projeyi VS Code ile açınız. Eğer `code .` komutu sizde çalışmıyorsa VS Code uygulamasını kendiniz başlatıp oluşturduğunuz proje dizinini VS Code ortamında açabilirsiniz.

```bash
cd helloSolidity
code .
```

Şimdi -tek seferlik olmak üzere- hardhat paketlerini yüklemek için aşağıdaki komutu kullanıyoruz. Bu komutu ister daha önceki terminal/konsol ekranından isterseniz de VS Code içindeki dahili terminal ekranından girebilirsiniz.

```bash
npm install --save-dev hardhat
```

Artık paketlerimiz yüklendiğine göre proje dizinimizde Hardhat kurulumunu yapabiliriz. VS Code içindeki dahili terminal ekranına aşağıdaki komutu giriniz.

```
npx hardhat init
```

Yukarıdaki komutu girdiğinizde sizi aşağıdaki gibi bir kurulum ekranı karşılayacak.

Burada `Create a JavaScript` project veya `Create a TypeScript` project diyerek Hardhat kurulumunu tamamlayabilirsiniz.

<figure><img src="../.gitbook/assets/hardhat setup.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Genelde sektörde TypeScript kullanılmaktadır dolayısıyla birçok modül ve framework TypeScript desteklemektedir. Fakat TypeScript'e aşina değilseniz JavaScript'de kullanılabilir.
{% endhint %}

### Compile Etme/Derleme

Yazdığınız kodları derlemek için aşağıdaki komutu kullanabilirsiniz. Terminal veya Komut İstemcisi'ni açın ve proje kök dizininde olduğunuzdan emin olun.

```bash
npx hardhat compile
```

### Test Etme

Proje kök dizininde `test` adlı bir klasör bulun. Eğer yoksa oluşturun.

`test` klasöründe bir test dosyası oluşturun (örneğin, `MyContract.test.js`) ve aşağıdaki kodu ekleyin

```javascript
const { expect } = require("chai");

describe("MyContract", function () {
  it("should set and get the value", async function () {
    const [owner] = await ethers.getSigners();
    const MyContract = await ethers.getContractFactory("MyContract");
    const contract = await MyContract.deploy();
    await contract.setValue(100);
    expect(await contract.getValue()).to.equal(100);
  });
});

```

Testleri çalıştırmak için aşağıdaki komutu kullanabilirsiniz.

```bash
npx hardhat test
```

{% hint style="info" %}
Test ve deploy araçları olan Mocha, Chai, Ignition ve Ethers.js araçları Hardhart kurulumu ile birlikte gelmektedir.
{% endhint %}

### Deploy/Dağıtma

Sözleşmeyi dağıtmak için Hardhat Ignition modülünü kullanacağız.

`ignition/modules` klasöründe aşağıdaki kodların bulunduğu `Lock` adında bir dosya bulacaksınız. Eğer yoksa bu dosyayı elle oluşturabilirsiniz.

```typescript
import { buildModule } from "@nomicfoundation/hardhat-ignition/modules";

const JAN_1ST_2030 = 1893456000;
const ONE_GWEI: bigint = 1_000_000_000n;

const LockModule = buildModule("LockModule", (m) => {
  const unlockTime = m.getParameter("unlockTime", JAN_1ST_2030);
  const lockedAmount = m.getParameter("lockedAmount", ONE_GWEI);

  const lock = m.contract("Lock", [unlockTime], {
    value: lockedAmount,
  });

  return { lock };
});

export default LockModule;

```

Test ağı (testnet) veya ana ağa (mainnet) deploy etmek için uygun yapılandırmaları `hardhat.config.js` dosyasında yapın.&#x20;

Dağıtımı yapmak için aşağıdaki komutu çalıştırabilirsiniz.

```bash
npx hardhat ignition deploy ./ignition/modules/Lock.ts
```
