# Kullan?c?lar Ekran?

?st ?ubuktaki `?` bu sayfay? Kullan?c?lar ekran?ndan a?ar. Bu ekran; yerel ve Active Directory kaynakl? kullan?c?lar?, genel rolleri, hesap ve 2FA durumunu ve kasa eri?imi say?s?n? birlikte incelemek i?in kullan?l?r.

Yaln?zca **Owner** ve **Admin** bu ekran? a?abilir. Auditor ile User kullan?c? listesini g?remez. Lisans salt okunur durumdaysa liste ve detaylar incelenebilir, fakat kullan?c?y? de?i?tiren i?lemler kapal?d?r.

## Burada Ne Yap?l?r

- Yerel kullan?c? olu?turulur; ge?ici ana parola ve ilk rol atan?r.
- Kullan?c? ad? ile g?r?nen ad d?zenlenir.
- Owner olmayan kullan?c?ya Admin, Auditor veya User rol? verilir.
- Kullan?c? kapat?l?r, kapasite uygunsa tekrar a??l?r veya kapal? kullan?c? kal?c? silinir.
- Yaln?z kurucu Owner, ba?ka bir Owner olmayan kullan?c? i?in ge?ici parola belirleyebilir veya 2FA kayd?n? s?f?rlayabilir.

Bu ekran yeni bir Owner olu?turmaz. Normal olu?turma ve rol de?i?tirme se?eneklerinde yaln?z **Admin**, **Auditor** ve **User** vard?r.

## Listeyi ve Detay? Okuma

Kullan?c?lar olu?turulma s?ras?yla listelenir. Her sat?rda rol ve kaynak rozeti, g?r?nen ad/kullan?c? ad?, kasa eri?imi say?s?, k?sa public key izi, 2FA ve `ACTIVE`/`DISABLED` durumu g?r?n?r.

**Detay? g?r** ?ekmecesi ayn? bilgileri d?zenli bi?imde sunar. Oturumlar?, kullan?c?ya ait audit zaman ?izelgesini, olu?turulma tarihini, Active Directory DN bilgisini veya tam public key'i g?stermez.

Kaynak rozetleri:

- **Lokal:** VaultPilot i?inde olu?turulan `LOCAL` kullan?c?.
- **E?itleme:** `DIRECTORY` kullan?c?s?; sa?lay?c? bulunursa ad? a??klamada g?r?n?r.
- **Active Directory:** ?ifreli bir AD credential kayd?na ba?l? `CREDENTIAL` kullan?c?.

Bir `LOCAL` kullan?c?n?n ad? se?ili bir directory nesnesiyle e?le?irse aray?z onu sezgisel olarak **E?itleme** etiketiyle g?sterebilir. Bu rozet tek ba??na kesin login source kan?t? de?ildir.

`ACTIVE` kullan?c? oturum a?abilir ve aktif lisans say?m?na dahildir. `DISABLED` kullan?c? oturum a?amaz ve aktif kapasiteyi t?ketmez; kayd? hen?z silinmemi?tir. Y?klemede iskelet sat?rlar, hi? kullan?c? yoksa bo? durum g?r?n?r.

## Yerel Kullan?c? Olu?turma

1. **Yeni kullan?c? olu?tur** panelini a??n.
2. En az iki karakterli, benzersiz kullan?c? ad? girin.
3. ?ste?e ba?l? g?r?nen ad? girin.
4. Admin, Auditor veya User rol?n? se?in.
5. En az 14 karakterli ge?ici ana parolay? iki alana ayn? yaz?n.
6. **Kullan?c? olu?tur** ile kaydedin.

Owner veya Admin rol?, yaz?labilir lisans ve bo? aktif kullan?c? kapasitesi gerekir. Kapasite doluysa lisans? y?kseltin veya art?k giri? yapmamas? gereken kullan?c?y? kapat?n.

Taray?c? ge?ici ana paroladan auth do?rulay?c?s?, kullan?c? anahtar ?ifti ve ki?isel kasa anahtar malzemesi t?retir; sunucuya d?z metin parola g?nderilmez. Sunucu kullan?c?y? `ACTIVE` ve `LOCAL` olarak olu?turur, ki?isel kasay? a?ar ve kullan?c?ya bu kasada Manager eri?imi verir.

Ge?ici parolay? audit notuna, destek kayd?na veya ekran g?r?nt?s?ne yazmay?n. Yaln?z g?venilir ve ayr? bir kanaldan iletin.

## Kullan?c? Bilgisi ve Roller

Owner ve Admin etkin kullan?c?lar?n kullan?c? ad? ile g?r?nen ad?n? d?zenleyebilir. Owner kullan?c? ad? de?i?tirilemez; Admin bir Owner kayd?n? d?zenleyemez. Owner kendi g?r?nen ad?n? de?i?tirebilir.

| Rol | Konsoldaki kapsam |
| --- | --- |
| Admin | Kullan?c?lar? ve kasalar? y?netir; lisans? y?netemez. |
| Auditor | Audit ve sistem durumunu g?r?r; gizli de?erlere veya kasa anahtarlar?na eri?emez. |
| User | Yaln?z atanan kasalar?, o kasadaki Manager/Editor/Viewer rol?ne g?re kullan?r. |

Kullan?c? kendi genel rol?n? de?i?tiremez ve Owner rol? de?i?tirilemez. Aray?z kapal? kullan?c?da d?zenleme ve rol se?imini devre d??? b?rak?r; konsoldan de?i?tirmek i?in ?nce tekrar a??n.

Genel kullan?c? rol? ile kasa rol?n? kar??t?rmay?n. Sat?rdaki kasa say?s?, her kasadaki yetki seviyesini g?stermez.

## Active Directory Giri? Eri?imi

AD giri? eri?imi Kullan?c?lar sat?r?ndan verilmez. ?lgili Active Directory kayd?n?n men?s?ndeki **VaultPilot giri?ine al** veya **VaultPilot giri?inden ??kar** eylemi kullan?l?r.

Bu ak?? yaln?z Owner rol?ne a??kt?r ve yaz?labilir lisans ister. Directory kayna?? i?in sa?lay?c? ile DN, credential kayna?? i?in kaynak secret kayd? gerekir. Yeni y?netilen kullan?c? User rol?yle a??l?r; mevcut Admin veya Auditor rol? korunabilir.

VaultPilot her giri?te LDAP bind yapmaz. Eri?im verildi?inde mevcut ?ifreli AD credential parolas?ndan yerel VaultPilot do?rulay?c?s? ve anahtar malzemesi t?retilir. AD parolas? d??ar?da de?i?irse otomatik e?itlenmez. Se?ili OU veya kullan?c?lar da yaln?z se?im yap?ld??? i?in otomatik olu?turulmaz.

Mevcut y?netilen kullan?c?n?n ortak kasa eri?imi varsa giri? malzemesini bu ak??la yenileme reddedilir. Giri? eri?imini kapatmak kullan?c?y? `DISABLED` yapar ve oturumlar?n? iptal eder.

Kullan?c? durumu ile directory sa?lay?c? se?imi ayr? isteklerde kaydedilir. ?lk i?lem ba?ar?l?, ikinci i?lem ba?ar?s?z olabilir. Hata sonras? Kullan?c?lar listesini ve AD se?im ekran?n? ayr? ayr? yenileyin.

## Parola Belirleme ve 2FA S?f?rlama

Bu i?lemler yaln?z kurucu Owner hesab?na a??kt?r. Yeni kurulumda kullan?c? ad? `VpAdm`'dir; eski `administrator` kurucu hesab? uyumluluk i?in tan?n?r. ??lemler kendi hesab?na veya herhangi bir Owner'a uygulanamaz.

### Ge?ici parola belirleme

- Yeni parola en az 14 karakter olmal? ve onay? e?le?melidir.
- Auth do?rulay?c?s? ile kullan?c? anahtar ?ifti yenilenir.
- 2FA kayd? s?f?rlan?r ve a??k oturumlar iptal edilir.
- `USER_PASSWORD_SET` yaz?l?r; d?z metin parola audit'e yaz?lmaz.

> **Durma ko?ulu:** Bu eylemi kay?ps?z kasa kurtarma veya s?radan parola rotasyonu olarak kullanmay?n. Uygulama yeni ki?isel kasa anahtar? ?retir ve yaln?z kurucu Owner'?n o anda a?abildi?i ortak kasalardaki e?le?en eri?imleri yeni anahtara sarabilir. Mevcut ki?isel kasa i?eri?i veya yeniden sar?lmayan ortak kasa eri?imleri okunamaz hale gelebilir. ??erik ve kasa eri?im envanteri do?rulanmadan devam etmeyin.

### 2FA kayd?n? s?f?rlama

Mevcut authenticator ba?? kald?r?l?r, `TWO_FACTOR_DISABLE` yaz?l?r ve a??k oturumlar iptal edilir. Kullan?c? sonraki ba?ar?l? giri?inden sonra 2FA'y? yeni cihazla yeniden kurabilir. Aktif 2FA yoksa i?lem yap?lmaz.

## Kapatma, Tekrar A?ma ve Kal?c? Silme

### Kullan?c?y? kapatma

Owner veya Admin, kendi hesab? ve Owner d???ndaki etkin kullan?c?y? kapatabilir. Durum `DISABLED` olur, oturumlar iptal edilir, aktif lisans say?m? azal?r ve `USER_DISABLE` yaz?l?r. Aray?z hi?bir Owner'? kapatmaya izin vermez.

### Kullan?c?y? tekrar a?ma

**Tekrar a?** yaln?z kapal? kullan?c?da g?r?n?r. Yaz?labilir lisans ve bo? aktif kullan?c? kapasitesi gerekir. Ba?ar? kullan?c?y? `ACTIVE` yapar ve `USER_UPDATE` yazar.

### Kullan?c?y? kal?c? silme

Yaln?z ?nceden kapat?lm??, kendi hesab?n?z olmayan ve Owner rol?nde olmayan kullan?c? silinebilir. ??lem geri al?namaz.

> **Durma ko?ulu:** Ki?isel kasa, ortak kasa eri?imleri ve kullan?c?ya ba?l? operasyon kay?tlar? i?in sahiplik devri tamamlanmadan silmeyin. Veritaban? ili?kileri; kullan?c? taraf?ndan olu?turulan audit sat?rlar?, extension cihazlar?, API istemcileri, directory sa?lay?c?lar?/i?lemleri, discovery kay?tlar?, dosya par?alar? ve g?nderilen/al?nan payla??m paketleri gibi ba?l? kay?tlar? da kald?rabilir.

Silmeden hemen ?nce `USER_DELETE` olu?turulur. Metadata hedef kullan?c? kimli?i ve rol?, ki?isel kasa say?s? ve silinecek kullan?c? audit ge?mi?inin say?/son hash ?zetini ta??r. Bu, kullan?c?n?n b?t?n eski audit sat?rlar?n?n korundu?u anlam?na gelmez.

## Audit ve ??lem S?n?r?

| ??lem | Audit olay? |
| --- | --- |
| Kullan?c? olu?turma | `USER_CREATE` |
| Bilgi d?zenleme | `USER_UPDATE` |
| Rol de?i?tirme | `USER_ROLE_UPDATE` |
| Kapatma / AD giri?inden ??karma | `USER_DISABLE` |
| Tekrar a?ma / y?netilen eri?imi yenileme | `USER_UPDATE` |
| Kurucu Owner'?n parola belirlemesi | `USER_PASSWORD_SET` |
| 2FA s?f?rlama | `TWO_FACTOR_DISABLE` |
| Kal?c? silme | `USER_DELETE` |

Her olay etkilenen kullan?c?ya ayn? ayr?nt?yla ba?lanmaz. Olu?turma, bilgi/rol de?i?ikli?i, kapatma, tekrar a?ma ve parola olaylar?n?n ?o?u ayr? hedef kullan?c? kimli?i ta??maz. Akt?r, zaman, eylem ve varsa target/metadata birlikte incelenmelidir.

Kullan?c? de?i?ikli?i, audit yaz?m? ve oturum iptali tek atomik i?lem de?ildir. Ge? bir audit veya oturum temizleme hatas?, kullan?c? de?i?tikten sonra g?r?lebilir. Hata sonras? listeyi, hesap durumunu, oturumlar? ve Audit ekran?n? yenileyin; i?lemi k?rlemesine tekrarlamay?n.

## Ekran Durumlar?

| Durum | Operat?r cevab? |
| --- | --- |
| Y?kleniyor | ?skelet sat?rlar kaybolana kadar i?lem ba?latmay?n. |
| Liste bo? | Sunucu profili ve oturumu do?rulay?n; kurucu Owner'?n g?r?nmemesi normal de?ildir. |
| Lisans salt okunur | Yaln?z inceleyin; kullan?c? de?i?tiren i?lem ba?latmay?n. |
| Kapasite dolu | Kullan?c? olu?turmay?n/tekrar a?may?n; kapasite a??n veya lisans? y?kseltin. |
| Kaynak rozeti beklenmedik | Ger?ek login source ile AD se?imini ayr? kontrol edin. |
| ??lem sonras? hata | Kullan?c?, lisans, oturum ve audit durumunu yenileyip do?rulay?n. |
| Parola kurtarma | ??erik ve anahtar eri?im envanteri yoksa durun. |
| Kal?c? silme | Sahiplik devri ve ba??ml?l?k envanteri tamamlanmad?ysa durun. |

## ??lemden ?nce

- Do?ru sunucu profili ve kullan?c? sat?r?nda oldu?unuzu do?rulay?n.
- Genel rol ile kasa rol?n? ayr? inceleyin.
- AD kullan?c?s?nda AD kay?t durumunu ve VaultPilot hesap durumunu ayr? kontrol edin.
- Parola/2FA hedefinin kendi hesab?n?z veya Owner olmad???n? do?rulay?n.
- Kapatma ?ncesi a??k i? ve entegrasyon sahipli?ini devredin.
- Silme ?ncesi kasa, payla??m, API istemcisi, directory/discovery ve audit ba??ml?l?klar?n? ??kar?n.
- Olu?turma veya tekrar a?ma ?ncesi aktif kullan?c? kapasitesini kontrol edin.
- Onay penceresindeki kullan?c? ad?n? son kez do?rulay?n.

## G?venli Kan?t

- Payla??labilir: rol kategorisi, `ACTIVE`/`DISABLED`, 2FA a??k/kapal? ?zeti ve redakte kasa eri?im say?s?.
- Audit olay t?r?, zaman damgas? ve k?salt?lm?? b?t?nl?k hash'i kullan?labilir.
- Lisans kan?t?nda yaln?z aktif kullan?c? toplam? ve limiti g?sterin.
- Gizli kalmal?: ger?ek kullan?c? ad?, g?r?nen ad, e-posta/UPN, DN, public key, ki?isel kasa ad? ve kullan?c? listesi ekran g?r?nt?leri.
- Ge?ici ana parola, TOTP secret, authenticator QR/kurtarma bilgisi veya kasa anahtar? kan?ta eklenmemelidir.
- Private support ekran g?r?nt?s?nde kullan?c? adlar?n? ve anahtar izlerini redakte edin; dolu parola alan?n? ?ekmeyin.

## Operat?r Notlar?

- Ekran son giri? veya son aktivite g?stermez; burada incelenmi? gibi raporlamay?n.
- **Parola belirle** d?? sa?lay?c? parolas?n? de?i?tirmez ve otomatik rotasyon de?ildir.
- AD giri? eri?imi ger?ek zamanl? LDAP do?rulamas? de?ildir; se?ili AD nesneleri otomatik kullan?c? ?retmez.
- Kapatma veriyi silmez; kal?c? silme geri al?namaz ve geni? ba?l?-kay?t etkisine sahiptir.
- Kullan?c? de?i?ikli?i ile audit/oturum temizli?i ayn? atomik s?n?rda de?ildir.
- Yeni Owner olu?turma veya Owner rol?n? devretme kontrol? bu ekranda yoktur.

## ?lgili

- [?lk kurulum, owner ve lisans](first-run-owner-license.md)
- [G?venlik ve g?ven modeli](security-and-trust-model.md)
- [Denetim kayd? ekran?](screen-audit-log.md)
- [Active Directory kay?tlar? ekran?](screen-active-directory-records.md)
- [Payla??m ekran?](screen-sharing.md)
- [Lisans ekran?](screen-license.md)
