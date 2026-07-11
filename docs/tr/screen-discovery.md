# Discovery Ekran?

?st ?ubuktaki `?`, **Operasyon > Discovery** ekran?ndan bu rehberi a?ar. Discovery; onayl? ?zel a?, TLS ve dosya maruziyeti kontrolleri i?in denetimli bir inceleme alan?d?r. Operat?r?n de?erlendirece?i sinyaller ve maskelenmi? kan?t ?retir; zafiyet taray?c?s?, kimlik bilgisi deneme arac?, varl?k envanteri veya otomatik temizlik servisi de?ildir.

## Eri?im, Rol ve Lisans S?n?r?

Lisans **Discovery** yetene?ini i?eriyorsa Sahip, Y?netici ve Denet?i ekran? a?abilir. Y?netici ve Denet?i; tarama kurallar?n?, ?al??malar?, bulgular?, bast?rmalar? ve i?e aktar?m durumunu salt okunur g?r?r. Kullan?c? rol? bu ekrana ula?amaz.

Her de?i?iklik Sahip rol?, Discovery yetene?i ve yaz?labilir lisans ister. Tarama kaydetme, ?nizleme veya Tarama ?al??t?rma, i?i durdurma/yeniden ba?latma/logunu silme, bulgu inceleme veya bast?rma, i?e aktar?m materyali haz?rlama ve i?e aktar?m? tamamlama bu s?n?ra dahildir. ??e aktar?m i?in ayr?ca Sahip'in D?zenleyici veya Y?netici oldu?u etkin ve kilidi a??k bir kasa gerekir.

?al??ma alan? a??kken yakla??k on saniyede bir yenilenir. Y?kleme s?ras?nda ?? sat?rl? iskelet, sorgu ba?ar?s?zl???nda ayr? hata paneli g?r?n?r.

## ?? Ad?ml? ?? Ak???

1. **?al??t?r** ? onayl? kapsam? olu?turup kaydedin, kontrolleri se?in, ?nizleme kayd? al?n veya ger?ek tarama ?al??t?r?n.
2. **Bulgular** ? maskelenmi? sinyalleri filtreleyin, kan?t? inceleyin ve karar verin.
3. **??e aktar** ? uygun ve incelenmi? s?n?rl? say?daki dosya bulgusunu iste?e ba?l? olarak etkin kasaya al?n.

??e aktar?m zorunlu de?ildir. A? y?zeyi, sertifika sorunu veya zay?f dosya sinyali kasa kayd?na d?n??meden operat?r bulgusu olarak kalabilir.

## ?al??t?r: Onayl? Tarama Haz?rlama

### Kontrolleri se?me

Yaln?z se?ilen ve kapsam? bulunan kontroller ?al???r:

| Kontrol | Ger?ek davran?? | Gerekli kay?tl? kapsam |
| --- | --- | --- |
| Giri? y?zeyleri | Se?ili portlara ba?lan?r; bilinen ve ayn? kaynaktan bulunan giri? yollar?na s?n?rl? HTTP/HTTPS `GET` istekleri g?nderir. Form veya kimlik bilgisi g?ndermez. | En az bir kabul edilmi? ?zel IPv4 hedefi. |
| SSL/TLS sertifikalar? | TLS ba?lant?s? a??p ge?erlilik, ana makine/parmak izi, kendinden imzal?/i? CA, tekrarl? parmak izi ve AD CS web kan?t?n? okur. | En az bir kabul edilmi? ?zel IPv4 hedefi. |
| Dosyalarda a??k gizli de?erler | Onayl? dosyalar? ge?ici olarak okur; desteklenen gizli de?er, kimlik bilgisi, sertifika ve anahtar sinyalleri i?in yaln?z metadata ve maskelenmi? bulgu olu?turur. | En az bir ??z?mlenmi? haz?r klas?r veya onayl? yol. |

H?zl? se?imler uygun t?m kontrolleri, yaln?z dosyalar? veya A? + SSL/TLS'yi se?er. A? ve dosya kontrolleri birlikte se?ilebilir. ?ki kol e?zamanl? ?al???r; herhangi birindeki hata b?t?n ?al??may? ba?ar?s?z yapar.

### ?zel a? kapsam?

A? kapsam? tek RFC1918 IPv4 adresi, CIDR veya a??k IPv4 aral??? kabul eder. Genel IP, ana makine ad?, IPv6, loopback ve link-local hedef kabul edilmez. Birle?ik s?n?r 512 hedeftir; a??k aral?k tek `/24` i?inde kalmal?d?r. Dolu bir kapsamda tek bir reddedilen giri? bulunmas? bile kayd? engeller.

Hedef ?nizlemesi kabul edilen adresleri geni?letir, reddedilen giri?leri g?sterir ve kalanlar? ?zetlemeden ?nce en fazla 64 e?le?en hedefi listeler. Bu yerel bir kapsam ?nizlemesidir; eri?ilebilirlik testi de?ildir.

Port planlar? d???k g?r?lt?l? yayg?n k?meler sunar: Premium varsay?lan, Web login, Windows kimlik ve Dar TLS. Tarama kural? en fazla 32 benzersiz port kabul eder. Varsay?lan k?me `443, 8443, 9443, 636, 3269, 5986, 80, 8080` de?erleridir.

A? kontrolleri ger?ek trafik ?retir: TCP ba?lant?s?, TLS el s?k??mas? ve s?n?rl? HTTP/HTTPS GET istekleri. Giri? veya AD CS kan?t?n? s?n?fland?rmak i?in HTTP yan?t g?vdesinin en fazla 64 KiB b?l?m? okunabilir; ayn? kaynaktaki s?n?rl? say?daki giri? ba?lant?s? takip edilebilir. Kullan?c? ad?, parola, kimlik do?rulama formu, exploit, kaba kuvvet veya parola p?sk?rtme g?nderilmez.

TLS kontrol?, ge?ersiz veya g?venilmeyen sertifikan?n metadata bilgisini okuyabilmek i?in g?ven zinciri reddine tak?lmaz. IP adresi bi?imindeki hedeflerde SNI g?nderilmez. Sertifika bulgusu risk kan?t?d?r; g?venilir TLS ba?lant?s?n?n ba?ar?yla kuruldu?unu kan?tlamaz.

### Dosya kapsam? ve haz?r klas?rler

Haz?r kaynak gruplar? VaultPilot sunucusunda ??z?mlenir:

- Windows klas?rleri: Masa?st?, Belgeler, ?ndirilenler, OneDrive, Ortak Masa?st? ve Ortak Belgeler.
- Sunucu uygulamalar?: IIS yap?land?rma/site/log konumlar? ile Nginx veya Apache yap?land?rma yollar?.
- DevOps ve y?netim: uygun `.ssh`, `.kube`, `.docker`, `.aws`, Azure ve gcloud profil klas?rleri.

Haz?r se?imler uygun yerel Windows profillerine geni?leyebilir. Ger?ekte hangi yollar?n okunabildi?ini VaultPilot sunucu servis hesab?n?n dosya sistemi izinleri belirler. Eksik veya eri?ilemeyen haz?r yol, a??k hata vermeden hi? dosya ?retmeyebilir.

Ek kapsam; onayl? mutlak s?r?c? yolu veya normal UNC yolu kabul eder. Kay?tl? tarama en fazla 32 ??z?lm?? yol tutar. S?r?c? k?k?, ?st dizine ??kma i?eren yol, cihaz yolu, ?o?u Windows sistem yolu, VaultPilot/eski PassMan veri yolu, sembolik ba?lant?, olu?turulmu? dizin/dosya, desteklenmeyen uzant?, eri?ilemeyen kay?t ve boyut s?n?r?n? a?an dosya atlan?r veya reddedilir.

Kural en fazla 80 izinli uzant? kabul eder. Varsay?lan azami dosya boyutu 5 MB, kesin ?st s?n?r 25 MB'dir. Zaman a??m? 250?15.000 ms, e?zamanl?l?k 1?16 aral???ndad?r.

Dosya incelemesi; desteklenen metin, yap?land?rma, betik, VPN/RDP, kay?t defteri, Terraform, paket y?neticisi kimlik bilgisi, sertifika/anahtar ve desteklenen Office/Excel OOXML i?eri?ini sunucu i?lemi belle?ine ge?ici olarak okuyabilir. Kal?c? Discovery verisi kaynak gizli de?eri de?il; dedekt?r metadatas?, maskeli yol, karmalar, gerek?e kodlar? ve maskelenmi? ?nizleme i?erir. Kaynak dosya de?i?tirilmez, ta??nmaz, karantinaya al?nmaz, temizlenmez veya silinmez.

### A??k onay ve tarama kural? davran???

A? kapsam? **Bu ?zel hedefleri tarama yetkim var**, dosya kapsam? **Bu dosya yollar? salt okunur tarama i?in onayl?** se?imini ister. Kapsam de?i?tirildi?inde ilgili onay s?f?rlan?r. Ge?erli ?zel a? kapsam?, onayl? dosya kapsam? veya ikisinden biri olmadan tarama kaydedilemez.

**Taramay? kaydet** her seferinde yeni tarama kural? olu?turur; mevcut ekranda kay?tl? kural? d?zenleme veya silme i?lemi yoktur. **Bu tarama aktif** kapal? kaydedilirse kural Devre d??? olur. Tarama d??mesi kapan?r; mevcut aray?zde ?nizleme etkin g?r?nebilse de sunucu Devre d??? kural i?in hem ?nizleme hem Taramay? reddeder.

## ?nizleme, Tarama ve ?? Kontrolleri

?nizleme ile Tarama ayn? de?ildir:

- **?nizleme**, hemen tamamlanm?? bir `PREVIEW` i?i ve denetim olay? kaydeder. TCP, TLS, HTTP veya dosya kontrol? yapmaz ve bulgu olu?turmaz.
- **Tarama**, se?ilen kontrolleri ger?ekten y?r?t?r. Birka? dakika s?rebilir; istek i? son duruma ula??nca tamamlan?r, bu s?rada periyodik sorgular kaydedilmi? ilerlemeyi g?sterebilir.

Bir tarama kural? i?in ayn? anda yaln?z bir i? etkin olabilir. ?? durumlar? S?rada, ?al???yor, ?ptal bekleniyor, Tamamland?, ?ptal edildi ve Ba?ar?s?z de?erleridir. ?lerleme; taranan hedef, taranan dosya, i?lenen bulgu ve son g?ncelleme bilgisini g?sterir.

**Durdur** iptal iste?ini kaydeder. ?ptal anl?k de?ildir; ?al??t?r?c? onaylayana kadar kural etkin kal?r ve yeni i? ba?lat?lamaz. **Sil**, yaln?z son duruma ula?m?? i?te onaydan sonra kullan?labilir; ?al??ma logunu siler, ilgili bulgular? korur. **Tekrar**, kay?tl? kural? ve o anda se?ili kontrolleri kullan?r; eski i?in kontrol se?iminin de?i?mez kopyas?n? yeniden oynatmaz.

??lem logu en yeni alt? i?i g?sterir. Geni?letilmi? tarama ge?mi?i d?nen b?t?n i?leri listeler. Sunucu yeniden ba?larsa yar?m kalan etkin i? daha sonra kesintiye u?ram?? veya iptal edilmi? olarak kurtar?labilir.

Ekrandaki bulgu say?s? o ?al??mada i?lenen veya g?ncellenen sinyalleri g?sterir; yaln?z yepyeni benzersiz bulgu sat?r? say?s? oldu?u garanti edilmez.

## Bulgular: Maskelenmi? Sinyalleri ?nceleme

?lk Bulgular g?r?n?m? bilerek **G??l? sinyal + A??k** filtreleriyle ba?lar. Varsay?lan g?r?n?m? geri y?klemek b?t?n bulgular? de?il bu filtreleri getirir. Arama ve geli?mi? filtreler; g?ven, durum, ?nem, kaynak t?r?, aday tipi, varl?k kimli?i, gerek?e kodu, maskeli yol ve karmalar? kapsar.

?lk sayfa 200 bulgu y?kler. **Daha fazla bulgu y?kle** eski sayfalar? getirir; API sayfa ba??na en fazla 500 kay?t kabul eder. Filtreler, toplu se?im, inceleme say?lar? ve ??e aktar yaln?z taray?c?ya y?klenmi? bulgular ?zerinde ?al???r. Filtre d???nda kalan se?imler temizlenene kadar se?ili kalabilir.

Tablo ve detay paneli; ?nem, g?ven, aday tipi, varl?k kimli?i, maskelenmi? ?nizleme, dedekt?r, gerek?e kodlar?, durum, k?salt?lm?? kan?t karmas?, iste?e ba?l? maskeli yol/yol karmas? ve g?ncelleme zaman? g?sterir. Maskelenmi? kan?t bile i? sistemi tan?mlayabilir; bilin?li bi?imde g?venli hale getirilmeden ?zel kanalda tutun.

### Bulgu ya?am d?ng?s?

| Ge?erli durum | Kullan?labilir kararlar |
| --- | --- |
| A??k | ?ncelemeye al, Yok say, Bast?r |
| ?ncelemede | Uygun dosya materyalini Kasaya al?nabilir yap, Yok say, Bast?r, A???a d?nd?r |
| Kasaya al?nabilir | Uygun materyal i?in ??e aktar ekran?n? a? veya A???a d?nd?r |
| Kasaya aktar?ld? | Temizli?i i?aretle |
| Temizli?i do?ruland? | A???a d?nd?r |
| Yok say?ld? | A???a d?nd?r veya Bast?r |
| Bast?r?ld? | A???a d?nd?r |

Yok say yaln?z o bulguyu kapat?r. Bast?r; dedekt?r ve bast?rma anahtar? i?in kal?c? kural olu?turur, gelecekteki benzer sinyaller Bast?r?ld? durumunda saklan?r. Ge?erli aray?z bast?rma nedeni istemez veya g?ndermez; kural normalde **Not yok** g?sterir. Bast?r?lm?? bulguyu A???a d?nd?rmek kal?c? bast?rma kural?n? silmez; bu ekranda bast?rma kural? silme kontrol? yoktur.

Bulgu i?lemleri onay penceresi g?stermez. Toplu **?ncelemeye al**, yaln?z g?r?n?r ve se?ili A??k bulgular? etkiler. Ge?erli aray?z bulguyu mevcut kasa kayd?na ba?lamaz.

Tamamlanan dosya taramas?, daha ?nce g?r?len kan?t ba?ar?yla taranm?? yollardan kaybolursa A??k, ?ncelemede veya Kasaya al?nabilir durumundaki eski dosya bulgusunu otomatik olarak Temizli?i do?ruland? durumuna alabilir. Yok say?ld?, Bast?r?ld? ve Kasaya aktar?ld? durumlar? bu ge?i?le otomatik temizlenmez.

## ??e Aktar: K?sa ?m?rl? Materyal Aktar?m?

Yaln?z dar kapsaml? dosya bulgusu i?e aktar?labilir. Bulgu Kasaya al?nabilir ve `FILE_EXPOSURE` t?r?nde olmal?; yol karmas? ve materyal konumu bulunmal?; Parola, API anahtar?, Sertifika veya Kimlik bilgisi aday? olarak s?n?fland?r?lmal?d?r. A? y?zeyi, TLS bulgusu, not ve genel dosya kan?t? yaln?z sinyaldir.

??e aktar?m adaylar? y?klenmi? bulgulardan olu?ur. Beklenen eski aday g?r?nm?yorsa ?nce Bulgular ekran?nda daha eski sayfalar? y?kleyin.

Her i?e aktar?mda:

1. VaultPilot onayl? kayna?? yeniden okur; yol karmas?, dedekt?r, aday tipi, kan?t karmas? ve materyal parmak izini do?rular.
2. D?z metin de?er yaln?z kullan?c?ya ba?l?, be? dakikal?k k?sa aktar?m i?in d?ner.
3. Taray?c? kayd? olu?turup etkin kasa anahtar?yla ?ifreler.
4. Sunucu belirteci, kan?t?, kasa yazma yetkisini ve aday tipini do?rular; ?ifreli kayd? saklay?p bulguyu Kasaya aktar?ld? durumuna ge?irir.

Kaynak materyal de?i?tiyse, ta??nd?ysa, kaybolduysa veya kan?tla art?k e?le?miyorsa i?e aktar?m durur ve bulgu yeniden incelenmelidir. Sunucu d?z metin kaynak de?eri kal?c? olarak saklamaz.

Se?ili i?e aktar?mlar s?rayla ?al???r; tek atomik i?lem de?ildir. Sonraki kay?t ba?ar?s?z olursa daha ?nce ba?ar?yla aktar?lanlar kasada kal?r. ??e aktar?m kayna?? temizlemez; **Temizli?i i?aretle** yaln?z bulgu i? ak??? durumunu de?i?tirir.

## Denetim ?zi

Discovery; tarama kural? kayd?, ?nizleme/Tarama ba?lang?c?, ?al??ma iptali ve log silme, bulgu inceleme/Yok say/Bast?r, i?e aktar?m haz?rlama ve materyal okuma, genel kasa `IMPORT`, i?e aktar?m tamamlama ve elle temizlik i?aretleme olaylar?n? denetime yazar. ?? logunu silmek bulgular? silmez. Eski dosya bulgular?n?n otomatik temizli?i tamamlanan dosya taramas?n?n par?as?d?r; her sat?r i?in ayr? elle temizlik denetim olay? olarak anlat?lmamal?d?r.

## Ekran Durumlar?

| Durum | Operat?r cevab? |
| --- | --- |
| Discovery y?kleniyor | ?skelet tamamlanana kadar bekleyin; durum bilinmeden ikinci tarama kural? olu?turmay?n. |
| Discovery verisi al?namad? | Oturumu, Discovery yetene?ini ve sunucu ba?lant?s?n? kontrol edin; g?venli hale getirilmi? hatay? koruyun. |
| Salt okunur rol veya lisans | Yaln?z inceleyin. B?t?n i?lemler Sahip ve yaz?labilir Discovery lisans? ister. |
| Kapsam reddedildi | Kapsam? geni?letmeyin veya denetimi a?may?n; ?zel IPv4 kapsam?n? d?zeltin ya da yaln?z dosya taramas? i?in a? alan?n? bo?alt?n. |
| Kural Devre d??? | ?nizleme d??mesinin g?r?n?m?ne g?venmeyin; ?al??ma gerekiyorsa etkin yeni kural olu?turun. |
| Tarama ?al???yor | Kaydedilmi? ilerlemeyi izleyin; ayn? kural ikinci i?i ba?latamaz. |
| ?ptal bekleniyor | ?al??t?r?c? onay?n? bekleyin; taraman?n hemen durdu?unu varsaymay?n. |
| Tarama ba?ar?s?z | ?? detay?n? a??n, gizli de?erleri ??kar?lm?? hata kan?t?n? koruyun, onayl? kural? d?zeltip bilin?li yeniden ba?lat?n. |
| Bulgu yok | ?nizleme de?il ger?ek Tarama tamamland? m? ve se?ilen kontrollerin ge?erli kapsam? var m? kontrol edin. |
| Filtreye uyan bulgu yok | Filtreleri s?f?rlay?n; varsay?lan g?r?n?m bile A??k olmayan ve G??l? olmayan bulgular? gizler. |
| ??e aktar?m kuyru?u bo? | Uygun dosya bulgular?n? inceleyin, gerekiyorsa eski sayfalar? y?kleyin ve do?rulanan materyali Kasaya al?nabilir yap?n. |
| ??e aktar?m kilitli | Sahip'in D?zenleyici veya Y?netici oldu?u yaz?labilir etkin kasay? a??n. |
| ??e aktar?m kan?t? de?i?ti | Durup kayna?? yeniden inceleyin; karma veya parmak izi do?rulamas?n? atlamay?n. |

## ??lemden ?nce

- Her ?zel hedef, UNC payla??m?, s?r?c? yolu ve haz?r se?imle geni?leyen profil alan? i?in a??k yetki al?n.
- VaultPilot sunucu hesab?n?n yaln?z ama?lanan okuma yetkisine sahip oldu?unu do?rulay?n; haz?r se?imler dosya sistemi yetkisi vermez.
- Soruyu yan?tlayan en k???k hedef, port, yol, uzant?, boyut, zaman a??m? ve e?zamanl?l?k kapsam?n? se?in.
- ?nizlemeyi yaln?z kay?tl? plan say?n; ger?ek kan?t gerekti?inde Tarama kullan?n.
- HTTP kontrollerinin GET trafi?i ?retti?ini, dosya kontrollerinin kaynak i?eri?i ge?ici olarak okudu?unu unutmay?n.
- Yok say, Bast?r veya ??e aktar karar?ndan ?nce durum, g?ven, dedekt?r, maskeli yol, gerek?e kodlar? ve sahipli?i inceleyin.
- ??e aktarmadan ?nce etkin kasa, yazma rol?, kay?t sahibi, hedef kategori ve kaynak d?zeltme plan?n? do?rulay?n.

## G?venli Kan?t

- Payla??labilir: genel kontrol t?r?, tarama kural?/i? durumu, yakla??k hedef/dosya/bulgu say?lar?, ?nem, g?ven, aday tipi, dedekt?r kimli?i, geni? zaman aral???, g?venli hale getirilmi? hata s?n?f? ve bilin?li maskelenmi? yol veya ana makine bi?imi.
- Gizli kalmal?: ger?ek IP/CIDR/port envanteri, ana makine ad?, UNC veya yerel yol, kullan?c? ad?, tam varl?k kimli?i, bast?rma anahtar?, kesin zaman damgas?, ham veya ili?kilendirilebilir ?nizleme, kaynak dosya, kaynak de?er, ?zel anahtar/sertifika materyali, i?e aktar?m belirteci, kasa ad?, veritaban?/yedek/d??a aktar?m ve i?e aktar?lan kay?t i?eri?i.
- Kan?t ve yol karmalar? raporlar aras?nda sistemleri ili?kilendirebilir. ?zel destekte tam kar??la?t?rma gerekmiyorsa k?salt?lm?? veya tamamen maskelenmi? de?er payla??n.
- Kaynak dosyay? eklemeyin ve ke?fedilen d?z metni destek kayd?nda yeniden yazmay?n. Maskelenmi? bulgu metadatas? ve ?zel destek kanal? kullan?n.

## Ne Zaman Durmal? ve Destek ?stemelisiniz

Kapsam sahipli?i belirsizse, genel veya beklenmeyen hedef g?r?n?yorsa, haz?r se?im onay d??? alana ??z?l?yorsa, dosya eri?imi ama?lanandan geni?se, ?al??ma ilerlemeden etkin kal?yorsa, iptal onaylanm?yorsa, bulgular beklenenden fazla ba?lam a???a ??kar?yorsa, bast?rma a??klanmam?? sinyal s?n?f?n? gizliyorsa, materyal i?e aktar?m s?ras?nda de?i?iyorsa, s?ral? i?e aktar?m k?smen ba?ar?l? oluyorsa veya temizlik/iptal karar? denetim kan?t?yla ?eli?iyorsa durun. Ger?ek kapsam veya gizli materyal eklemeden rol, genel durum, kontrol t?r?, geni? zaman aral???, k?salt?lm?? karmalar, g?venli hata metni ve son g?venli ad?mla ?zel destek kayd? a??n.

## Operat?r Notlar?

Discovery kan?t toplama ve inceleme arac?d?r; ihlal kan?t? veya hi?bir sorun bulunmad???n?n garantisi de?ildir. Temiz sonu? yaln?z se?ilen kontrolleri, kabul edilen kapsam?, okunabilen dosyalar?, desteklenen bi?imleri, limitleri ve o Taraman?n zaman?n? kapsar. Bulguyu Temizli?i do?ruland? durumuna almak kayna?? de?i?tirmez. Bast?rma kal?c?d?r; yaln?z gelecekteki benzer sinyaller bilin?li olarak gizlenecekse kullan?lmal?d?r.

## ?lgili

- [Discovery rehberi](discovery.md)
- [Discovery bulgu inceleme KB](../../kb/tr/discovery-finding-review.md)
- [Public issue redaction KB](../../kb/tr/public-issue-redaction.md)
- [Denetim Ge?mi?i ekran?](screen-audit-log.md)
