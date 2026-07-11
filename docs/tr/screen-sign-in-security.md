# Giri? G?venli?i Ekran?

?st ?ubuktaki `?`, **Sunucu ayarlar? > Giri? g?venli?i** sekmesine ait bu rehberi a?ar. Bu sekme, a??k olan ki?isel profilin ana parola de?i?imini, TOTP tabanl? 2FA ba??n? ve Sahip rol?nde etkin sunucu oturumlar?n? y?netir. VaultPilot giri?i kullan?c? ad?, ana parola ve 2FA a??ksa authenticator koduyla yap?l?r; bu ekranda e-posta ba?lant?s?, e-postayla parola s?f?rlama, harici kimlik sa?lay?c?s?/SSO veya kurtarma kodu ak??? yoktur.

## Eri?im, Rol ve Sunucu Ayarlar? Ba?lam?

Giri? g?venli?i ayr? bir lisans ?zelli?ine ba?l? de?ildir ve b?t?n sistem rolleri sekmeyi g?rebilir. Sahip, Y?netici ve Denet?i di?er Sunucu ayarlar? sekmelerini de g?r?r; yaln?z Kullan?c? rol?nde sekme k?mesi **Giri? g?venli?i** ile s?n?rland?r?l?r. Bundan ayr? olarak, Sahip olmayan herhangi bir rol?n Lisans veya Entegrasyonlar g?r?n?m?ne gitme giri?imi bu ki?isel g?venlik sekmesine y?nlendirilir.

Kendi ana parolas?n? veya 2FA ba??n? de?i?tiren sunucu API'leri Sahip, Y?netici ve Kullan?c? rollerini kabul eder; Denet?i bu formlar? g?rse bile sunucu de?i?ikli?i reddeder. Bu i?lemler lisans yaz?labilirken yap?labilir; salt okunur lisans profil de?i?ikli?ini engeller. Etkin oturum listesini g?rme ve ba?ka bir oturumu kapatma yaln?z Sahip i?indir.

Bu sekme ki?isel profil ba?lam?ndad?r. Sahip burada ba?ka kullan?c?n?n parolas?n? veya 2FA ba??n? s?f?rlamaz. ?lk sahip hesab?n?n, uygun Sahip d??? kullan?c?lar i?in parola belirleme ve 2FA s?f?rlama ara?lar? **Kullan?c?lar** ekran?ndad?r ve farkl? yetki/onay s?n?rlar?na sahiptir.

## Burada Ne Yap?l?r

- Mevcut ana parolay? do?rulay?p en az 14 karakterlik yeni ana parola ve onay?n? girin.
- 2FA kapal?ysa yeni bir TOTP s?rr? ve QR kodu olu?turup ilk alt? haneli authenticator koduyla ba?? etkinle?tirin.
- 2FA a??ksa ba??n hem taray?c? taraf?ndaki ?ifreli kopyas?n?n hem sunucu do?rulama materyalinin haz?r olup olmad???n? okuyun.
- Kay?p telefon veya uygulama de?i?iminde, profil h?l? a??ksa mevcut 2FA ba??n? onayla iptal edip yeni kurulum ba?lat?n.
- Sahip rol?nde etkin oturumlar? kullan?c?, rol, son temas, biti? ve ge?erli oturum durumuyla inceleyin; ge?erli olmayan bir oturumu kapat?n.
- ?st ?ubuktaki **Kasay? kilitle ve oturumu kapat** ile a??k taray?c? profilini elle kilitleyin.

Bu sekmede kilit s?resi ayar?, ba?ar?s?z giri? kilitleme politikas? veya g?venilir cihaz listesi yoktur. Otomatik kilit s?resi sabit 15 dakikad?r ve buradan de?i?tirilemez.

## Ana Parolay? De?i?tirme

**Ana parolay? de?i?tir** formu a??k olan kullan?c?n?n kendi profilini de?i?tirir. Profil kilidi a??k olmal?; mevcut ana parola girilmeli; yeni parola en az 14 karakter olmal? ve onay?yla e?le?melidir. ?stekler on dakikada en fazla alt? parola de?i?imiyle s?n?rland?r?l?r.

Taray?c? mevcut paroladan anahtar t?retir, profil ?zel anahtar?n? yeni anahtarla yeniden ?ifreler ve 2FA a??ksa ana parolayla ?ifreli TOTP kopyas?n? da yeniden ?ifreler. Sunucu mevcut do?rulay?c?y? kontrol eder, yeni do?rulay?c?y? ve ?ifreli materyali kaydeder. D?z metin ana parola sunucu profilinde saklanmaz.

Ba?ar?l? de?i?iklik `PASSWORD_CHANGE` denetim olay? ?retir ve ayn? kullan?c?ya ait di?er kal?c? sunucu oturumlar?n? kapat?r; i?lemi yapan mevcut oturum a??k kal?r. Formun ba?ar?l? mesaj? **profil anahtarlar? yeniden sar?ld?** ifadesini kullan?r. Bu i?lem ba?ka kullan?c?n?n ge?ici parolas?n? belirlemek, profili s?f?rlamak veya unutulmu? ana parolay? kurtarmak de?ildir.

## 2FA Durumlar? ve Kurulum

### 2FA kapal? / Kurulum bekliyor

**2FA kurulumunu ba?lat**, taray?c?da yeni bir TOTP s?rr? ?retir. **Yeni QR olu?tur**, hen?z kaydedilmemi? s?rr? yenisiyle de?i?tirir; eski QR bu a?amada etkin bir ba? de?ildir. Kurulum kart?nda QR kodu, bi?imlendirilmi? manuel anahtar ve alt? haneli kod alan? g?r?n?r.

QR olu?turulurken iskelet g?sterilir. QR ?retilemezse hata g?r?n?r; manuel anahtar ekranda kalabilir. QR veya manuel anahtar ?ok hassast?r. Kodu authenticator uygulamas?na ekledikten sonra g?ncel alt? haneli kodu girip **2FA etkinle?tir** kullan?n. Kod ?nce taray?c?da, sonra sunucuda zaman tolerans?yla do?rulan?r; on dakikada en fazla 12 2FA g?ncelleme iste?i kabul edilir.

Ba?ar?l? kurulumda TOTP s?rr?n?n bir kopyas? kurtarma/yeniden ?ifreleme i?in ana paroladan t?retilen anahtarla, ikinci kopyas? giri? do?rulamas? i?in sunucu anahtar?yla ?ifrelenir. Di?er kal?c? oturumlar kapat?l?r ve `TWO_FACTOR_ENABLE` denetim olay? yaz?l?r. Bir sonraki normal kilit a?mada authenticator kodu gerekir.

### 2FA aktif / Haz?r veya Kontrol

**Aktif** ba?da **Kilit ekran?nda kod istenir** g?r?n?r. Hem `serverTotpReady` hem ana parolayla ?ifreli TOTP kopyas? varsa durum **Haz?r / ?ift ?ifreli kay?t** olur. Bunlardan biri eksikse **Kontrol / Kay?t kontrol ediliyor** g?r?n?r; bunu sa?l?kl? ba? saymay?n.

2FA etkin oldu?u h?lde sunucu do?rulama materyali eksik eski bir profil kilit ekran?nda reddedilir. Ekran, y?netici yede?ine d?nmeyi veya profili s?f?rlamay? s?yler; e-posta, kurtarma kodu veya TOTP atlama se?ene?i sunmaz.

### Kayd? iptal etme ve s?f?rlama s?n?r?

**Kayd? iptal et**, onaydan sonra a??k profilin authenticator ba??n? kald?r?r, di?er kal?c? oturumlar?n? kapat?r ve `TWO_FACTOR_DISABLE` denetim olay? yazar. Ge?erli oturum a??k kal?r. Bu, yeni cihaz i?in 2FA kurulumunu yeniden ba?latmaya izin verir; mevcut TOTP s?rr?n? g?stermez veya kurtarma kodu ?retmez.

Kullan?c? kilitliyken ve authenticator cihaz?na eri?emiyorken bu kendi kendine iptal kullan?lamaz; profilin zaten a??k ve sunucu oturumunun do?rulanm?? olmas? gerekir. ?lk Sahip, **Kullan?c?lar** ekran?nda yaln?z ba?ka ve Sahip olmayan bir kullan?c?n?n 2FA ba??n? s?f?rlayabilir. Kendi hesab? veya Sahip hesab? i?in bu y?netim i?lemi kullan?lamaz.

## Etkin Oturumlar

**Aktif oturumlar** yaln?z Sahip i?in y?klenir ve g?venlik sekmesi a??kken yakla??k 15 saniyede bir yenilenir. **Yenile** ile anl?k sorgu yap?labilir. Liste yaln?z kurulu?un etkin kullan?c?lar?na ait s?resi dolmam?? sunucu oturumlar?n? g?sterir; s?resi dolan kay?tlar sorgu s?ras?nda temizlenir.

?zet; toplam etkin, **bu taray?c?** ve **kapat?labilir** say?s?n? verir. Her sat?rda 18 karakterlik genel oturum kimli?i, kullan?c?/g?r?nen ad, rol, son temas, biti?, durum ve i?lem bulunur. IP adresi, taray?c? ad? veya cihaz parmak izi g?sterilmez; yaln?z bu tabloya bakarak fiziksel cihaz? kesin tan?mlamay?n.

Ge?erli sat?r **Bu oturum** olarak i?aretlenir ve **Kapat** d??mesi devre d???d?r. Ba?ka bir sat?rdaki **Kapat** do?rudan iptal iste?i g?nderir; ikinci bir onay penceresi yoktur. Ba?ar?l? i?lem oturumu siler, listeyi ve denetimi yeniler ve `SESSION_REVOKE` olay? ?retir. Oturum kimli?ini veya kullan?c? ad?n? herkese a??k kan?ta koymay?n.

Liste y?klenirken ?? iskelet sat?r? g?r?n?r. Ayr? bir sorgu hata kart? yoktur; liste iste?i ba?ar?s?z olup veri yoksa **Listelenebilir aktif oturum yok** bo? durumu g?r?lebilir. Bu mesaj? kesin olarak oturum olmad??? kan?t? saymadan ?nce **Yenile**, sunucu ba?lant?s? ve Sahip oturumunu do?rulay?n.

## Elle Kilitleme, Otomatik Kilit ve H?zl? Yeniden A?ma

?st ?ubuktaki **Kasay? kilitle ve oturumu kapat**; a??k/kopyalanm?? kay?t durumunu, olu?turulan payla??m paketini, kilit a?ma TOTP alan?n?, ge?ici 2FA kurulum s?rr?/QR/kodunu, h?zl? a?ma durumunu ve sorgu ?nbelle?ini temizler. Taray?c? anahtarlar?n? uygulama belle?inden kald?r?r ve sunucu ??k???n? en iyi ?abayla ?a??r?r. Payla??m parolas?, se?ili payla??m kay?tlar? ve payla??m paketi meta verisi (`sharePackageMeta`) ise a??k?a s?f?rlanmaz; aray?z kilitlense de bu React durumu bellekte kalabilir.

Kasa 15 dakika taray?c? etkinli?i olmad???nda otomatik kilitlenir. ??aret?i, klavye, kayd?rma, odak ve g?r?n?rl?k de?i?imleri sayac? yeniler. S?re doldu?unda a??k/kopyalanm?? durum, payla??m paketi/parolas? ve se?ili payla??m kay?tlar?, h?zl? a?ma durumu, sunucu oturumu, sorgu ?nbelle?i ve a??k anahtarlar temizlenir. Elle kilitten farkl? olarak payla??m paketi meta verisi (`sharePackageMeta`) ile kilit a?ma ve ge?ici TOTP kurulum durumlar? a??k?a s?f?rlanmaz; kilit ekran? bunlar? gizler, ancak hassas payla??m meta verisini, QR kodunu veya manuel anahtar? g?sterdikten sonra otomatik kilidi temizlik ad?m? saymay?n.

G?r?n?r bir payla??m veya TOTP ak???n? yar?da b?rakt?ysan?z yaln?z kilide g?venmeyin; tam sayfa yeniden y?kleme yap?n.

Normal kilit a?madan sonra 15 dakikal?k h?zl? yeniden a?ma kopyas? SharedWorker/Service Worker ?al??ma zaman? belle?inde tutulabilir; geri y?kleme belirteci taray?c? ge?mi? durumunda bulunur. Eski IndexedDB h?zl? a?ma kal?nt?lar? yaln?z silinir. Bu hat, ana parolay? veya ana paroladan t?retilmi? anahtar? kal?c? taray?c? depolamas?na yazmaz. Elle veya otomatik kilit h?zl? a?ma kopyas?n? temizler.

## Parola, Profil S?f?rlama ve Kurtarma S?n?rlar?

- **Ana parolay? de?i?tir**, a??k kullan?c?n?n mevcut profil anahtarlar?n? yeni parolaya yeniden sarar; veriyi silmez.
- **Kullan?c?lar > Parola belirle**, yaln?z ilk Sahip taraf?ndan ba?ka, Sahip olmayan bir kullan?c? i?in y?r?t?len ayr? i?lemdir. Hedefin oturumlar?n? kapat?r, 2FA's?n? s?f?rlar ve ki?isel kasa anahtar?n? yeni ge?ici parolaya g?re yeniden sarar.
- **Sunucu profilini s?f?rla**, Giri? g?venli?i sekmesindeki bir kontrol de?ildir. Ayr? ve y?k?c? Sahip API ucu, do?rulanm?? Sahip oturumu ile tam `DELETE_LOCAL_PROFILE` ifadesini ister; kurulu?u, kullan?c?lar?, kasalar?, s?rlar?, payla??m/entegrasyon/dizin kay?tlar?n?, denetimi ve b?t?n sunucu oturumlar?n? siler. Bu i?lem unutulmu? parola i?in hafif bir s?f?rlama de?ildir.
- Kilit ekran?ndaki kurtarma mesaj? ?nce ana parola, Caps Lock ve TOTP kodunu kontrol etmeyi; sunucu/profil sorunu s?rerse VaultPilot Backup Tool yede?ine d?nmeyi s?yler. Destek ana parolay?, TOTP s?rr?n? veya oturum ?erezini bilmez ve istememelidir.

Ge?erli taray?c? ak???nda e-posta ile parola s?f?rlama, kurtarma kodu, SMS, IdP y?nlendirmesi veya destek taraf?ndan kimlik do?rulama atlama yoktur.

## ?nerilen ?? Ak??lar?

### ?lk 2FA ba??n? kurma

1. Profil kilidinin a??k, sunucu oturumunun do?rulanm?? ve lisans?n yaz?labilir oldu?unu do?rulay?n.
2. **2FA kurulumunu ba?lat** se?ene?ini kullan?n.
3. QR kodu authenticator uygulamas?yla taray?n veya manuel anahtar? do?rudan uygulamaya girin; ekran g?r?nt?s? almay?n.
4. Uygulamadaki g?ncel alt? haneli kodu girip **2FA etkinle?tir** kullan?n.
5. Durumun **Aktif** ve **Haz?r / ?ift ?ifreli kay?t** oldu?unu do?rulay?n.
6. Kontroll? bir kilitlemeden sonra kullan?c? ad?, ana parola ve yeni TOTP koduyla kilidi a?may? do?rulay?n.

### ??pheli eski bir oturumu kapatma

1. Sahip rol?yle **Aktif oturumlar** listesini yenileyin.
2. Kullan?c?, rol, son temas ve biti? zaman?n? kar??la?t?r?n; cihaz/IP bilgisi olmad???n? unutmay?n.
3. **Bu oturum** sat?r?n? de?il, kapat?lmas? onaylanan di?er sat?r? se?in.
4. **Kapat** se?ene?inin ikinci onay istemeden i?lem yapt???n? dikkate al?p d??meyi bir kez kullan?n.
5. Listenin ve `SESSION_REVOKE` denetim kayd?n?n yenilendi?ini do?rulay?n.

## Ekran Durumlar?

| Durum | Operat?r cevab? |
| --- | --- |
| 2FA kapal? / Kurulum bekliyor | Yeni ba? olu?turun; QR veya manuel anahtar? gizli tutun. |
| QR olu?turuluyor | ?skeletin tamamlanmas?n? bekleyin; yeniden tekrar tekrar QR ?retmeyin. |
| QR olu?turulamad? | Manuel anahtar varsa authenticator uygulamas?na do?rudan girin; yoksa kurulumu yeniden ba?lat?n. |
| Authenticator kodu do?rulanamad? | Alt? hane, cihaz saati ve do?ru hesab? kontrol edin; do?rulamay? atlamay?n. |
| 2FA aktif / Haz?r | Ba??n ?ift ?ifreli materyali mevcut; kontroll? kilit a?ma testi yap?n. |
| 2FA aktif / Kontrol | Eksik ba? materyalini sa?l?kl? saymay?n; kilitlemeden ?nce ?zel kurtarma/yedek plan?n? do?rulay?n. |
| Ana parola de?i?tiriliyor | ?kinci g?nderim yapmay?n; sonu? veya hata mesaj?n? bekleyin. |
| Mevcut parola do?rulanamad? | Do?ru profil/parola ve Caps Lock durumunu kontrol edin; profil s?f?rlamaya acele etmeyin. |
| Oturumlar y?kleniyor | ?? iskelet sat?r?n?n tamamlanmas?n? bekleyin. |
| Listelenebilir aktif oturum yok | Sorgu hatas? i?in ayr? kart olmad???ndan ba?lant?y? ve Sahip rol?n? do?rulay?p yenileyin. |
| Oturum kapat?lamad? | Ge?erli sat?r? se?medi?inizi, Sahip rol?n? ve sunucu ba?lant?s?n? do?rulay?n. |
| Kasa otomatik kilitlendi | Ana parola ve gerekiyorsa TOTP ile yeniden a??n; h?zl? a?man?n temizlendi?ini varsay?n. |
| Sunucu oturumu do?rulanamad? | H?zl? a?ma bellekte 15 dakika korunabilir; ba?lant? gelince otomatik yeniden denemeyi bekleyin. |
| Eski 2FA profili | Sunucu do?rulama materyali yoksa kodu atlamay?n; y?netici yede?i veya onayl? profil kurtarma yolunu kullan?n. |

## ??lemden ?nce

- ??lemin kendi profilinize mi, ba?ka kullan?c?ya m?, yoksa b?t?n sunucu profiline mi etki etti?ini ay?r?n.
- Rol? ve lisans?n yaz?labilir durumunu do?rulay?n; Denet?i formu g?rse bile profil yazamaz.
- 2FA QR kodu veya manuel anahtar g?r?n?rken ekran payla??m?n? ve kayd? kapat?n.
- Ana parola veya 2FA de?i?ikli?inin di?er kal?c? oturumlar? kapataca??n? planlay?n.
- Oturum kapatma d??mesinde ikinci onay olmad???n? ve ge?erli oturumun tablodan kapat?lamad???n? unutmay?n.
- 2FA ba??n? iptal etmeden veya profili s?f?rlamadan ?nce onayl? yedek ve yeniden giri? yolunu do?rulay?n.

## G?venli Kan?t

- Payla??labilir: sistem rol? s?n?f?, 2FA **kapal?/aktif/haz?r/kontrol** durumu, toplam ve kapat?labilir oturum say?s?, yakla??k son temas/biti? aral???, genel hata kategorisi ve geni? zaman aral???.
- Gizli kalmal?: kullan?c?/g?r?nen ad, ana parola ve t?retilmi? do?rulay?c?, TOTP s?rr?, QR kodu, alt? haneli kod, ?ifreli TOTP/?zel anahtar verisi, oturum kimli?i/belirteci/?erezi, profil s?f?rlama kimli?i, yedek dosyas? ve tam zaman damgas?.
- Oturum tablosu cihaz parmak izi veya IP g?stermez; kan?ta bu alanlar? tahmin ederek eklemeyin.
- Ekran g?r?nt?s?nde manuel TOTP anahtar?n? yaln?z bulan?kla?t?rmay?n; tamamen maskeleyin ve g?r?nt?n?n kopyalar?nda kalmad???n? do?rulay?n.

## Ne Zaman Durmal? ve Destek ?stemelisiniz

2FA etkin ama ba? **Kontrol** durumundaysa, sunucu do?rulama materyali eksikse, yeni ana parolayla profil ?zel anahtar? a??lam?yorsa, ba?ka oturumlar de?i?iklik sonras? etkin kal?yorsa, oturum listesi beklenmedik kullan?c? g?steriyorsa veya otomatik kilit hassas ekran durumunu temizlemiyorsa yeni g?venlik de?i?ikli?i yapmay? b?rak?n. Gizli de?er eklemeden rol s?n?f?, genel durum, geni? zaman aral???, hata kodu ve son g?venli ad?mla ?zel destek kayd? a??n.

## Operat?r Notlar?

Giri? g?venli?i bir kimlik sa?lay?c?s? veya e-posta hesab? y?netim ekran? de?ildir. Ana parola, TOTP ve oturum y?netimi VaultPilot sunucusundaki profil ve taray?c? belle?i s?n?rlar?nda ?al???r. Kurtarma kodu, TOTP s?rr?, ana parola, kimlik do?rulama karmas?, ?erez veya tek kullan?ml?k kod g?steren kan?t yay?mlamay?n.

## ?lgili

- [?lk kurulum, owner ve lisans](first-run-owner-license.md)
- [Kullan?c?lar ekran?](screen-users.md)
- [Sunucu ayarlar? ekran?](screen-server-settings.md)
- [Giri? sonras? 401 KB](../../kb/tr/session-401-after-login.md)
- [G?venlik ve g?ven modeli](security-and-trust-model.md)
