---
icon: arrows-to-circle
---

# Konsensus (Fikir Birliği)

Blockchain'de konsensus (consensus), ağdaki tüm katılımcıların (düğümler) belirli bir kurallar dizisi üzerinde anlaşmaya vararak bir karar almasını ve bu kararın ağ genelinde geçerli olmasını sağlayan mekanizmadır.

Konsensus algoritmaları, merkezi olmayan sistemlerde güven ve doğrulama sağlamak için kritik öneme sahiptir.

{% hint style="info" %}
Konsensus yöntemlerinin ortaya çıkmasında büyük önem arz eden "**Bizans Generalleri Problemi**" konusunu araştırabilirsiniz. Bu konu blockchain gibi dağıtık yapılarda birden fazla katılımcının fikir birliğine varabilmesi için karşılaştıkları problem ve çözümlerini el alır.
{% endhint %}

### Konsensus Algoritmalarının Amaçları

1. **Dağıtık Uyum Sağlama:** Merkezi olmayan ağlarda, tüm düğümlerin aynı veriler üzerinde hemfikir olması gereklidir. Bu, ağın güvenilir ve tutarlı olmasını sağlar.
2. **Güvenlik ve Bütünlük:** Konsensus algoritmaları, kötü niyetli aktörlerin ağın bütünlüğünü bozmalarını zorlaştırır. Bu, ağın güvenli olmasını sağlar.
3. **Hata Toleransı:** Ağdaki bazı düğümler arızalansa bile, konsensus algoritmaları ağın çalışmaya devam etmesini sağlar.
4. **Adalet ve Katılım:** Her düğüm, işlemleri doğrulama ve yeni bloklar oluşturma sürecine katılabilir. Bu, ağın adil ve merkeziyetsiz olmasını sağlar.

### Yaygın Konsensus Algoritmaları

**1. Proof of Work (PoW)**

* Madenciler, belirli bir zorluk seviyesini karşılayan bir nonce değeri bulmak için karmaşık matematiksel problemleri çözerler. Bu işlem, önemli miktarda hesaplama gücü gerektirir.
* Güvenlidir ve saldırılara karşı dirençlidir. Madencilik süreci, işlemlerin doğruluğunu garanti eder.
* Eksi olarak enerji yoğundur ve yüksek işlem maliyetlerine yol açabilir. Çevresel etkileri olumsuzdur.
* Örnek olarak Bitcoin, Ethereum (Ethereum 2.0'a geçmeden önce).

**2. Proof of Stake (PoS)**

* Blok oluşturma hakkı, madencilerin sahip oldukları kripto paraların miktarına bağlıdır. Daha fazla varlığa sahip olanlar, blok oluşturma şansına daha fazla sahiptir. En fazla kullanılan konsensus yöntemidir.
* Daha az enerji tüketir, çevre dostudur ve daha hızlı blok oluşturma süresine sahiptir.
* Eksi olarak varlıkların dağılımında adaletsizlik olabilir, çünkü daha fazla varlığa sahip olanlar daha fazla blok oluşturma şansına sahiptir.
* Örnek olarak Ethereum 2.0, Cardano, Tezos.

**3. Delegated Proof of Stake (DPoS)**

* Token sahipleri, blok üreticilerini (delegeler) seçerler. Bu delegeler, blok oluşturma ve doğrulama görevini üstlenirler.
* Daha hızlı ve ölçeklenebilirdir. Katılım ve oylama sistemi, topluluk tarafından yönetilir.
* Eksi olarak DPoS yapılar merkezileşme riski taşır, çünkü sadece seçilmiş delegeler blok üretme yetkisine sahiptir.
* Örnek olarak EOS, TRON.

**4. Practical Byzantine Fault Tolerance (PBFT)**

* Bu algoritma, düğümlerin birbirleriyle iletişim kurarak konsensusa varmasını sağlar. Çoğunluğun anlaşmasına dayanır ve kötü niyetli aktörlere karşı dayanıklıdır.
* Düşük gecikme süresi ve yüksek verimlilik sağlar. Düğümler arasında hızlı anlaşma sağlanır.
* Eksi olarak ağ büyüklüğü arttıkça iletişim maliyetleri artar, bu da ölçeklenebilirlik sorunlarına yol açabilir.
* Örnek olarak Hyperledger Fabric, Zilliqa.

**5. Proof of Authority (PoA)**

* Belirli bir güvenilir otorite tarafından onaylanmış düğümler, blok oluşturma hakkına sahiptir. Bu otoriteler, kimlik doğrulamasından geçer.
* Yüksek verimlilik ve düşük gecikme süresi. Düğümler arasında hızlı konsensus sağlanır.
* Eksi olarak merkezileşme riski taşır, çünkü belirli otoriteler blok oluşturma yetkisine sahiptir.
* Örnek olarak VeChain, POA Network.

### Konsensus Algoritmalarının Seçimi ve Kullanımı

Konsensus algoritmalarının seçimi, bir blockchain ağının ihtiyaçlarına ve hedeflerine bağlıdır. Örneğin, yüksek güvenlik ve merkeziyetsizlik gerektiren bir ağ için PoW tercih edilirken, enerji verimliliği ve hız öncelikli bir ağ için PoS veya DPoS daha uygun olabilir.

**Uygulama Alanları ve Örnekler**

* **Bitcoin:** PoW kullanır ve yüksek güvenlik sağlar. Enerji tüketimi yüksektir.
* **Ethereum:** Başlangıçta PoW kullanırken, Ethereum 2.0 ile PoS'a geçmiştir. Bu, enerji verimliliği sağlar ve ölçeklenebilirliği artırır.
* **EOS:** DPoS kullanır ve yüksek ölçeklenebilirlik sağlar. Delegelerin seçilmesi, topluluk katılımını teşvik eder.
* **Hyperledger Fabric:** PBFT kullanır ve izinli (permissioned) blockchain ağları için uygundur. Yüksek verimlilik sağlar.
