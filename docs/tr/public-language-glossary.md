# Public Dil Sözlüğü

Bu sayfa VaultPilot public dokümanları yazılırken veya gözden geçirilirken kullanılır. Amaç, Türkçe ve İngilizce metinleri tutarlı tutmak; operatör dokümanını pazarlama metnine çevirmemektir.

## Genel Üslup

- Güncel ürün adı için **VaultPilot** kullan.
- **PassMan** adını yalnızca legacy compatibility bağlamında, eski servisler, data path'ler, header/cookie adları, update alias'ları, protocol string'leri veya geçmiş release notları için kullan.
- Operatör dilini kısa tut: kur, doğrula, incele, döndür, iptal et, yedekle, geri yükle, topla, redakte et.
- Bu public repo içinde product source code, release binary, imza materyali, müşteri verisi, database veya backup bulunduğu izlenimi verme.

## Terim Tercihleri

| Kaynak terim | Tercih edilen Türkçe kullanım | Not |
| --- | --- | --- |
| public repository | public repo veya public dokümantasyon reposu | Repo sınırı anlatılırken `public repo` kalabilir. |
| release | release veya yayın | GitHub Release adı için `release`; doğal cümlede `yayın` kullanılabilir. |
| support | destek | Ürün yüzeyi veya kanal adı değilse `destek` daha temizdir. |
| screenshot | ekran görüntüsü | Public görsellerde `yayına uygun hale getirilmiş UI görseli` ifadesi uygundur. |
| private source | private kaynak kod | Kaynak kodun burada yayınlanmadığını netleştir. |
| signing material | imza materyali | Güvenlik sınırı gerekiyorsa `private signing material` ifadesi korunabilir. |
| artifact | artifact veya çıktı | GitHub Release asset'i için `release artifact`; sıradan üretim dosyası için `çıktı`. |
| placeholder | placeholder | Teknik terim olarak kabul edilir; `<SERVER_HOST>` gibi örneklerle kullan. |
| redacted | redakte edilmiş | Public issue veya destek kanıtı için tercih edilir. |
| issue | issue | GitHub terimi olarak kabul edilir; public intake için `public issue` yaz. |
| evidence | kanıt | Destek bağlamında `kanıt paketi` kullan. |
| token | token | Teknik terim olarak kalsın. |
| endpoint | endpoint | API bağlamında kalsın. |
| client | client | API veya yazılım bileşeni bağlamında kalsın. |

## Çeviri Kuralları

- Ürün adlarını, asset adlarını, package adlarını, komut flag'lerini, endpoint path'lerini ve placeholder token'larını çevirmeyin.
- Türkçe doküman doğal ama operatör odaklı olmalı. Kısa ve net Türkçe cümle, birebir İngilizce çeviriden daha değerlidir.
- İngilizce teknik kelimeyi yalnızca gerçek UI/API terimi olduğunda veya VaultPilot operatör dilinde yerleşik olduğunda kullanın.
- Bir ifade güvenlik sınırını değiştiriyorsa İngilizce ve Türkçe eş sayfaları birlikte güncelleyin.

İlgili sayfalar:

- [Public repo sınırı](public-repository-boundary.md)
- [GitHub repo profili](github-repository-profile.md)
- [Destek kanıt paketi](support-evidence-pack.md)
- [İngilizce doküman ana sayfası](../en/README.md)
