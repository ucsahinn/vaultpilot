# Entegrasyonlar Ekran?

?st ?ubuktaki `?` simgesi **D?? API** ve **Active Directory** sekmelerinde bu rehberi a?ar. **Taray?c? eklentisi** sekmesinde ayn? simge, o ak???n ayr? [Taray?c? Eklentisi ekran?](screen-browser-extension.md) rehberine gider. Entegrasyonlar ekran? bu ?? ?r?n y?zeyini y?netir.

## Eri?im ve Lisans S?n?r?

Entegrasyonlar ekran? yaln?z VaultPilot **Sahip** sistem rol?ne g?sterilir. Y?netici, Denet?i ve Kullan?c? rolleri API istemcilerini veya dizin sa?lay?c?lar?n? bu ekrandan listeleyemez ve y?netemez. Sol men?de ekran?n a??lmas? i?in lisans?n **Entegrasyon** yetene?ini i?ermesi gerekir; kapsam yoksa men? devre d??? kal?r ve Sahip lisans ekran?na y?nlendirilir.

Salt okunur lisans yeni API istemcisi ve AD ajan? olu?turmay?; dizin kapsam? kaydetme, anl?k e?itleme, ajan i?lemi, ajan eri?im anahtar? yenileme/iptal etme, sa?lay?c? silme ve kasaya AD kayd? aktarma gibi yazma i?lemlerini kapat?r. G?venlik amac?yla mevcut bir API istemcisini veya taray?c? eklentisi cihaz?n? iptal etme yolu salt okunur lisans alt?nda da kullan?labilir. Taray?c? eklentisi k?sayolu ayr?ca lisans?n **Eklenti** yetene?ini kontrol eder.

## Burada Ne Yap?l?r

- **D?? API** sekmesinde salt okunur API yetkilerini se?in, gerekiyorsa en az bir kasa atay?n ve istemci olu?turun.
- Yeni istemcinin gizli de?erini s?re dolmadan kopyalay?n; daha sonra geri g?sterilemez.
- **?stemci defteri** i?inde etkin ve iptal edilmi? istemcileri, kapsamlar?, kasa say?s?n?, son okumay? ve olu?turma bilgisini inceleyin.
- **Audit ak???** i?inden istemci olu?turma, endpoint eri?imi ve iptal olaylar?n? filtreleyip Denetim Ge?mi?indeki ?zg?n olaya ge?in.
- **Active Directory** sekmesinde tek ajan kayd?n? kurun veya onar?n; e?itleme durumunu, OU/grup/kullan?c? a?ac?n? ve ajan yeteneklerini izleyin.
- VaultPilot giri? kapsam? ile kasaya aktar?lacak AD kullan?c? kapsam?n? ayr? y?netin.
- **Taray?c? eklentisi** sekmesinde Chrome Web Store kanal?n?, bekleyen/onayl? cihazlar? ve iptal edilmi? veya s?resi dolmu? cihaz ar?ivini y?netin.

## D?? API

### Yetki matrisi ve endpoint kapsam?

Ekran ilk a??ld???nda ?? operasyonel durum yetkisi se?ilidir. En az bir yetki her zaman se?ili kal?r. **Kasa verisi** se?ilmedik?e kasa atamas? g?r?nmez ve olu?turulan istemci hi?bir kasa kayd?n? okuyamaz.

| Ekrandaki yetki | ?? kapsam | ?zin verilen endpoint | Veri s?n?r? |
| --- | --- | --- | --- |
| Kasa verisi | `SECRETS_READ` | `GET /api/public/v1/secrets` ve `GET /api/public/v1/secrets/{secretId}` | Yaln?z atanm?? kasalar?n ?ifreli snapshot ve tek kay?t ??kt?s?; d?z metin kasa i?eri?i d?nmez. |
| Sunucu durumu | `SERVER_STATUS_READ` | `GET /api/public/v1/server/status` | Sunucu sa?l?k ve ?al??ma durumu. |
| Active Directory | `DIRECTORY_STATUS_READ` | `GET /api/public/v1/directory/status` | Ajan ba?lant?s?, e?itleme ve se?ili nesne say?lar?. |
| G?ncelleme durumu | `UPDATE_STATUS_READ` | `GET /api/public/v1/updates/status` | Update Center paket ve s?r?m sinyali. |

**Kasa verisi** y?ksek dikkat isteyen yetkidir. Se?ildi?inde **API kapsam?ndaki kasalar** alan?ndan en az bir kasa i?aretlenmeden istemci olu?turulamaz. Yaln?z durum endpointlerini kullanan istemci i?in kasa se?meyin; bu se?imde sunucu kasa verisini ??zmez.

### ?stemci olu?turma ve gizli de?er s?n?r?

1. **Yetki matrisi** i?inde yaln?z t?keten sistemin ihtiya? duydu?u gruplar? se?in.
2. **Endpoint kapsam?** alan?nda olu?an ger?ek yollar? kontrol edin.
3. `SECRETS_READ` se?iliyse gerekli en k???k kasa k?mesini i?aretleyin.
4. **?stemci ad?** alan?na sistemi ve amac? ay?rt eden bir ad yaz?n.
5. **?stemci olu?tur** d??mesini kullan?n.
6. Tam istemci kimli?ini ve **Gizli anahtar? kopyala** ile al?nan gizli de?eri t?keten sistemin onayl? gizli de?er deposuna aktar?n.

Gizli de?er ekranda maskeli kal?r. 120 saniyelik saya? sonunda veya **Temizle** se?ildi?inde yaln?z tek seferlik sonu? paneli kapan?r; istemci kayd? ve sunucuda saklanan gizli de?er ?zeti silinmez. Kaybolan gizli de?er yeniden a??lamaz. Gizli de?er kopyaland???nda VaultPilot 30 saniye sonra, yaln?z ayn? de?er h?l? panodaysa, panoyu temizlemeyi dener. Taray?c? izni temizli?i engelleyebilir; ba?ka bir yere yap??t?r?lm?? veya kaydedilmi? kopya geri al?namaz. ?stemci kimli?i kopyas? bu s?reli pano temizli?ini kullanmaz.

### ?stemci defteri, audit ve iptal

?stemci defteri durum, ad, k?salt?lm?? istemci kimli?i, yetkiler, kasa/yetki/denetim kayd? say?lar?, son okuma, olu?turan kullan?c? ve olu?turma zaman?n? g?sterir. **?stemci kimli?ini kopyala** tam kimli?i al?r. **Loglar? g?r** ilgili istemciyi Audit ak???nda se?er. Sunucu, ba?ar?l? public API kullan?m?nda **Son okuma** zaman?n? ve `INTEGRATION_SYNC` denetim olay?n? her istek i?in de?il, istemci ba??na en fazla be? dakikada bir g?nceller. Audit ak??? ge?erli filtre i?in en yeni sekiz olu?turma, ?rneklenmi? endpoint eri?imi veya iptal olay?n? g?sterir; bir sat?r se?ildi?inde Entegrasyon kategorisindeki Denetim Ge?mi?i olay? a??l?r.

**Eri?imi iptal et** onaydan sonra istemciyi `REVOKED` durumuna ta??r. ?ptal edilmi? kay?t defterde kan?t olarak kal?r, yeniden etkinle?tirilemez ve ayn? gizli de?er d?nd?r?lemez. De?i?im gerekiyorsa dar kapsaml? yeni istemciyi olu?turun, t?keten sistemi yeni kimlik bilgisine ge?irin ve ard?ndan eski istemciyi iptal edin.

## Active Directory

### Veri ve parola s?n?r?

VaultPilot DC ajan? etki alan? denetleyicisiyle ayn? a?da ?al???r. DC, Base DN, bind kullan?c? ad?, OU, grup, kullan?c? ve AD durum bilgisini VaultPilot'a g?nderir. Bind parolas? ve mevcut AD kullan?c? parolalar? VaultPilot'a g?nderilmez veya ekranda g?sterilmez. Kasaya aktar?lan AD kayd? kullan?c?/UPN/DN ve durum meta verisiyle, bo? parola alan?yla olu?turulur; gerekirse yeni parola daha sonra yetkili ajan i?lemiyle atan?r ve ?ifreli kayda yaz?l?r.

### ?lk ajan kayd? ve yerel kurulum

1. Sa?lay?c? ad?n? do?rulay?n; varsay?lan otomatik e?itleme aral??? 10 dakikad?r.
2. **Ajan kayd? olu?tur** ile tek sa?lay?c? kayd?n? haz?rlay?n.
3. **Ajan scriptini indir** ile `/downloads/vaultpilot-dc-agent.ps1` dosyas?n? al?n.
4. Ekranda maskeli duran ajan eri?im anahtar?n? **Anahtar? kopyala** ile ayr? al?n.
5. **Komutu kopyala** ile servis kurulum komutunu al?n ve y?netici PowerShell'de ?al??t?r?n; eri?im anahtar?n? yaln?z yerel gizli isteme yap??t?r?n.
6. Gerekirse **VaultPilot ?n kontrol**, **LDAP ?n kontrol**, **Durum komutu** ve **Canl? log** komutlar?n? kullan?n.

HTTPS ?zerinden a??lan konsol, etkin VaultPilot sertifikas?n?n parmak izini ajan komutuna sabitler. Kurumsal CA kullan?yorsan?z Windows g?ven deposunu veya kurum da??t?m politikas?n? ayr?ca y?netin. Ajan kayd? zaten varsa ikinci sa?lay?c? olu?turmay?n; mevcut sat?rdaki **Eri?im anahtar?n? yenile** i?lemi yeni eri?im anahtar? ve onar?m komutu ?retir.

**Anahtar? kopyala** ile al?nan eri?im anahtar? ve **Komutu kopyala** ile al?nan kurulum veya onar?m komutu i?in VaultPilot, ayn? i?erik h?l? panodaysa 30 saniye sonra en iyi ?abayla temizlik dener. **VaultPilot ?n kontrol**, **LDAP ?n kontrol**, **Durum komutu** ve **Canl? log** kopyalar? bu s?reli temizli?i kullanmaz; i?iniz bitince bunlar? panodan kendiniz kald?r?n.

### Sa?lay?c? durumu, a?a? ve kapsamlar

Sa?lay?c? kart? DC, Base DN, ajan s?r?m?, bind kullan?c? ad?, son ba?lant?, son e?itleme ve e?itleme aral???n? g?sterir. Durum etiketi **AJAN BEKLEN?YOR**, **BA?LI**, **BA?LANTI ESK?**, **?EVR?MDI?I** veya **ANAHTAR ?PTAL** olabilir. Ba?l? bir ajan ayr?ca **E??TLEN?YOR**, **E??TLEME KUYRUKTA** veya **HATA** g?sterebilir. **?imdi e?itle** yaln?z komutu kuyru?a al?r; sonu? i?in sa?lay?c? durumunu ve ??lemler ekran?n? izleyin.

**Dizin a?ac?nda ara** alan? OU, grup, kullan?c?, UPN ve DN i?inde arar. **A?a?**, **OU**, **Gruplar** ve **Kullan?c?lar** g?r?n?mleri yaln?z listeyi s?zer. Kullan?c?lar?n VaultPilot ile giri? se?imi an?nda ayr? giri? kapsam?na kaydedilir; Active Directory kay?t aktar?m? i?in yap?lan dal/kullan?c? se?imleri taslak olarak kal?r. ?nce **Kapsam? kaydet**, sonra **Se?ilenleri kasaya aktar** kullan?n. Aktar?m i?in etkin kasada D?zenleyici veya Y?netici eri?imi ve yaz?labilir lisans gerekir; se?ili kullan?c? zaten ayn? kasada varsa atlan?r.

**Ajan yetenekleri** ?eridi yaln?z ajan?n bildirdi?i deste?i g?sterir: **Parola durumu**, **Kilidi a?**, **Parola de?i?imi iste** ve **Parolay? de?i?tir**. Bu ?erit i?lem ba?latmaz. Hassas ajan i?lemleri yaln?z Sahip, yaz?labilir lisans, `CONNECTED` ajan sa?l??? ve ilgili yetenek birlikte varsa ?al???r. Hedef kullan?c? ayr?cal?kl? olarak i?aretlenmi?se hesab? kapatma, kilit a?ma, parola de?i?imi isteme ve **Parolay? de?i?tir** i?lemleri hem aray?zde kapat?l?r hem sunucuda kesin olarak reddedilir. Sonu?lar **Ajan i?lemleri** zaman ?izgisinde g?r?n?r.

**Eri?im anahtar?n? yenile** eski anahtar? hemen ge?ersiz k?lar ve yeni anahtar? yaln?z ge?erli sonu? panelinde verir. **Tehlikeli i?lemler** alt?ndaki **Eri?im anahtar?n? iptal et**, ajan? yeniden kay?t/onar?ma kadar e?itlemeden ??kar?r. **Sa?lay?c?y? kald?r**, sa?lay?c? kayd?n? siler; Windows ajan? yeniden ba?lanmak i?in yeni kay?t ve eri?im anahtar? ister.

## Taray?c? Eklentisi

Bu sekme Chrome Web Store'u normal kurulum kanal? olarak a?ar; yerel ZIP veya geli?tirici modu g?nl?k kurulum ak??? de?ildir. ?zet kartlar? son e?itlemeyi ve onayl?/bekleyen cihaz say?lar?n? yeniler. **Aktif cihazlar** sekmesi `PENDING` ve `APPROVED`, **Ar?iv** sekmesi `REVOKED` ve `EXPIRED` cihazlar? g?sterir.

Bekleyen iste?i onaylamak i?in eklenti popup'?ndaki `XXXX-XXXX` bi?imli sekiz karakterli kodu girin. En az bir kasan?n kilidi a??k ve lisans yaz?labilir olmal?d?r. Cihaz sat?r? yaln?z cihaz ad?n?, e?le?tirme kodunun son d?rt karakterini ve kasa yetkisi say?s?n? g?sterir; kullan?c?, hesap, taray?c? profili ve talebin kayna?? gibi di?er kimlik kontrollerini kurum i?i kanaldan ayr?ca yap?n. Onay, a??k kasalar?n anahtarlar?n? cihaz?n a??k anahtar? i?in sarar; d?z metin kasa kayd? veya ana parola eklenti cihaz listesinde g?sterilmez. Onayl? cihazda g?r?nen kesin i?lem etiketi **?ptal et**'tir. Bu sekmedeki `?`, ayr?nt?l? e?le?tirme ve cihaz durumlar? i?in Taray?c? Eklentisi ekran? rehberini a?ar.

## ?nerilen ?? Ak??lar?

### Yaln?z durum okuyan API istemcisi

1. **Kasa verisi** se?imini kapal? tutun.
2. Sunucu, Active Directory ve G?ncelleme durumu yetkilerinden gerekenleri se?in.
3. Endpoint ?zetinde kasa yolunun bulunmad???n? ve kasa se?icinin a??lmad???n? do?rulay?n.
4. ?stemciyi olu?turup gizli de?eri onayl? sisteme aktar?n.
5. ?lk ba?ar?l? ?a?r?dan sonra **Son okuma** ve Audit ak???ndaki **Endpoint eri?imi** olay?n? do?rulay?n. Ayn? istemcinin sonraki ?a?r?lar? be? dakikal?k ?rnekleme aral???nda bu iki alan? yeniden g?ncellemeyebilir.

### Dizin ajan?n? onarma

1. Ajan sa?l??? ve son ba?lant? zaman?n? kontrol edin; **Durum** ve **Canl? log** komutlar?yla Windows servisini do?rulay?n.
2. Eri?im anahtar? ge?ersiz veya onar?m gerekiyorsa **Eri?im anahtar?n? yenile** i?in onay verin.
3. Yeni eri?im anahtar?n? ayr? kopyalay?n, onar?m komutunu y?netici PowerShell'de ?al??t?r?n ve de?i?meyen DC/bind ayarlar?n? Enter ile koruyun.
4. Sa?l?k `BA?LI` olduktan sonra **?imdi e?itle** kullan?n; ilk e?itleme tamamlanmadan kapsam veya kasa aktar?m? yapmay?n.

## Ekran Durumlar?

| Durum | Operat?r cevab? |
| --- | --- |
| API istemcileri y?kleniyor | ?stemci defterindeki iskelet sat?rlar bitmeden yeni istemci olu?turmay?n. |
| API istemcisi yok | Yetki matrisini g?zden ge?irip yaln?z ger?ek t?keten sistem i?in ilk istemciyi olu?turun. |
| API istemcisi iptal | Kayd? yeniden kullanmay?n; gerekiyorsa yeni ve dar kapsaml? istemci olu?turun. |
| API istemcisi olu?turulamad? | Sahip rol?n?, yaz?labilir lisans?, se?ili yetkiyi ve `SECRETS_READ` i?in kasa atamas?n? kontrol edin. |
| AD sa?lay?c?lar? y?kleniyor | Mevcut kay?t do?rulanana kadar yeni ajan kayd? olu?turmay?n. |
| AD sa?lay?c?lar? al?namad? | **Yeniden dene** kullan?n; hata s?rerken ikinci sa?lay?c? olu?turmay?n. |
| Ajan bekleniyor | Script, yerel eri?im anahtar? istemi, VaultPilot eri?imi ve ilk Windows servis ba?lant?s?n? do?rulay?n. |
| Ba?lant? eski / ?evrimd??? | Hassas dizin i?lemlerini durdurun; durum ve canl? log komutlar?yla servisi ve a?? kontrol edin. |
| Ajan eri?im anahtar? iptal | Yeni eri?im anahtar? ve onar?m komutu olmadan e?itleme beklemeyin. |
| ?lk e?itleme bekleniyor | **?lk e?itlemeyi iste** kullan?n ve a?a? dolana kadar kapsam se?meyin. |
| Kapsam de?i?ikli?i kaydedilmedi | ?nce **Kapsam? kaydet** veya **De?i?iklikleri b?rak**; kasa aktar?m? bu s?rada kapal?d?r. |
| Eklenti e?le?tirmesi bekliyor | Sat?rdaki cihaz ad? ve kod ipucunu e?le?tirin; kullan?c?, hesap ve taray?c? profili do?rulamas?n? kurum i?i kanaldan tamamlay?n. |
| Eklenti iste?i s?resi doldu / iptal | Ar?ivde kan?t olarak inceleyin; gerekirse eklentiden yeni istek ba?lat?n. |
| Salt okunur lisans | Yeni kimlik bilgisi, e?le?tirme ve dizin yazmalar? kapal?d?r; mevcut API istemcisi veya eklenti cihaz? g?venlik amac?yla iptal edilebilir. |

## ??lemden ?nce

- Oturumun Sahip rol?nde oldu?unu ve lisans?n Entegrasyon yetene?ini i?erdi?ini do?rulay?n.
- ??lemin D?? API, Active Directory veya Taray?c? eklentisi sekmesine ait oldu?unu kesinle?tirin.
- API istemcisi i?in t?keten sistem, i? sahibi, gerekli endpointler, en k???k kasa k?mesi ve g?zden ge?irme tarihini kaydedin.
- ?ptalden ?nce yeni istemciye veya yeni ajan eri?im anahtar?na ge?i?in tamamland???n? do?rulay?n; acil g?venlik iptalinde beklemeyin.
- AD ajan? de?i?ikli?inde DC eri?imi, bind kullan?c? ad?, y?netici PowerShell, script kayna?? ve geri d?n?? yolunu haz?rlay?n.
- Kasaya AD kayd? aktar?rken do?ru kasan?n a??k, yaz?labilir ve rol?n?z?n D?zenleyici/Y?netici oldu?unu kontrol edin.
- Eklenti cihaz?n? onaylamadan ?nce sat?rdaki cihaz ad?, kod ipucu ve kasa yetkisi say?s?n? kontrol edin; kullan?c? talebini ve taray?c? profilini kurum i?i kanaldan ayr?ca do?rulay?n.

## G?venli Kan?t

- Payla??labilir: sekme ad?, yetki ad?, redakte endpoint yolu, genel HTTP durum kodu, ajan sa?l?k s?n?f?, nesne say?s? ve eklenti s?r?m?/ma?aza kanal?.
- Gizli kalmal?: tam istemci kimli?i, istemci gizli de?eri, ajan kimli?i/eri?im anahtar?, kurulum veya onar?m komutu, e?le?tirme kodu, cihaz kimli?i, i? DC/alan ad?, Base DN, bind kullan?c? ad?, UPN/DN ve kasa ad?.
- API istemci gizli de?eri, ajan eri?im anahtar? veya e?le?tirme kodu a???a ??kt?ysa genel payla??m? durdurun; ilgili eri?imi iptal edin veya yenileyin ve t?keten sistemi ?zel kanaldan g?ncelleyin.
- Ekran g?r?nt?s?nde yaln?z k?rpma yapmay?n; kod, kimlik, alan ad?, kullan?c?, dosya yolu, komut ve zaman ili?kisini tamamen maskeleyin.

## Ne Zaman Durmal? ve Destek ?stemelisiniz

Beklenen istemciler defterde g?r?nm?yorsa, ayn? AD sa?lay?c?s?ndan ikinci kay?t olu?mak ?zereyse, ajan eri?im anahtar? veya istemci gizli de?eri yanl?? sisteme yap??t?r?ld?ysa, e?le?tirme iste?inin sahibi do?rulanam?yorsa, ajan `STALE`, `OFFLINE` veya `REVOKED` durumundan ??km?yorsa ya da kasaya aktar?m beklenmeyen kullan?c?lar? i?eriyorsa durun. Gizli de?er eklemeden; sekme, genel durum, redakte kay?t kimli?i, zaman, son g?venli ad?m ve hata metniyle ?zel destek kayd? a??n.

## Operat?r Notlar?

Bu ekran d?? sistemlere yazma yetkisi veren genel bir entegrasyon merkezi de?ildir. Public API yaln?z tan?ml? okuma kapsamlar?n? kullan?r. AD ajan? mevcut parolalar? okumaz; desteklenen de?i?iklikleri yetkili komut olarak uygular. Taray?c? eklentisi de yaln?z onaylanan cihaz ve sar?lm?? kasa anahtar? s?n?r?nda ?al???r.

`pmc_` istemci kimli?i, `pms_` istemci gizli de?eri, `pmt_` ajan eri?im anahtar?, e?le?tirme kodu veya i? sunucu bilgisi i?eren ekran g?r?nt?s? ve terminal ??kt?s? yay?mlamay?n.

## ?lgili

- [Entegrasyon API istemcileri](api-clients.md)
- [Public API referans?](public-api-reference.md)
- [Active Directory ajan?](active-directory-agent.md)
- [Active Directory kay?tlar? ekran?](screen-active-directory-records.md)
- [Taray?c? Eklentisi ekran?](screen-browser-extension.md)
- [Taray?c? eklentisi](browser-extension.md)
