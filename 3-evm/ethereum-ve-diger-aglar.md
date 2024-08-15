---
icon: link
---

# Ethereum ve Diğer Ağlar

Ethereum, akıllı sözleşmelerin ve merkeziyetsiz uygulamaların (DApps) geliştirilmesine olanak tanıyan ilk blockchain platformlarından biridir.

Solidity gibi diller kullanılarak Ethereum üzerinde sözleşmeler yazılmaktadır.

Ethereum, birçok merkeziyetsiz uygulamaya ev sahipliği yapmaktadır. (Uniswap, Aave, MakerDAO )

DeFi projelerinin de çoğu Ethereum üzerinde çalışmaktadır.

## Diğer Popüler Blockchainler (Solana, ICP, vs.)

EVM kullanmayan birçok blockchain ağı da bulunmaktadır. Bunlardan bazılarını inceleyeceğiz. Tabi bu ağların da kendine göre bazı avantaj ve dezavantajları bulunmaktadır.

**Solana :** Yüksek işlem hızı ve düşük maliyetlerin olduğu, PoS konsensusu kullanan popüler bir blockchaindir. Solana'da akıllı sözleşme yazmak için genelde Rust, C gibi diller kullanılır.&#x20;

**ICP (Internet Computer) :** Web hızında ve web ölçeğinde çalışan full merkeziyetsiz bir blockchain. Aslında ICP bir blockchainden ziyade birden fazla blockchain'in bulunduğu bir platformdur.

ICP'yi diğer blockchainlerden ayıran başka bir nokta da tam merkeziyetsizlik sunmasıdır. Normalde Ethereum, Solana gibi ağların node'ları halihazırda AWS gibi bulut sunucularda barındığı için tam olarak merkeziyetsiz değildir, ayrıca dApp'lerin ön yüzleri de yine geleneksel olarak hosting/sunucularda barınmaktadır. ICP'de ise hem backend hem frontend Internet Computer Protocol dediğimiz platformda barınmaktadır. Bu da ICP'yi tam merkeziyetsiz bir platform haline getirmektedir. Fakat dezavantaj olarak ekosistemi zayıftır, geliştiriciler için de öğrenme eğrisi karışıktır. ICP üzerinde Rust ve Motoko dilleri kullanılarak Canister(Akıllı Sözleşme) yazılır.

**Cosmos:** ICP gibi farklı blockchainlerin cosmos üzerinde birbirleriyle iletişim kurabilmesi için geliştirildi. Aslında Cosmos'da ICP ile aynı vizyona sahiptir; "blockchainlerin interneti olmak".

Cosmos SDK ile Cosmos üzerinde kendi blok zincirinizi geliştirebilirsiniz.

| Özellikler               | Ethereum                  | Solana             | ICP                          | Cosmos                       |
| ------------------------ | ------------------------- | ------------------ | ---------------------------- | ---------------------------- |
| **Konsensus**            | PoS                       | PoH & PoS          | Chain Key                    | Tendermint BFT               |
| **Hedef**                | Akıllı Kontratlar & dApps | Yüksek Hızlı dApps | Merkeziyetsiz İnternet       | Blokzincirler Arası İletişim |
| **Gas Ücretleri**        | Yüksek                    | Düşük              | Yok (Cycle var)              | Düşük                        |
| **Programlama Dilleri**  | Solidity                  | Rust, C, C++       | Rust, Motoko                 | Go (Cosmos SDK)              |
| **Ölçeklenebilirlik**    | Orta                      | Yüksek             | Yüksek                       | Yüksek (IBC ile)             |
| **Merkeziyetsizlik**     | Yüksek                    | Düşük/Orta         | Orta/Yüksek                  | Yüksek                       |
| **Öne Çıkan Özellikler** | EVM, Layer 2 Çözümler     | Yüksek İşlem Hızı  | Web Hızında Merkeziyetsizlik | IBC, Modüler Yapı            |

