# Etki Alan?

?st ?ubuktaki `?` simgesi bu yard?m? Etki Alan? a??kken getirir. Bu ekran farkl? kaynaklardan gelen d?rt ?zeti bir araya getirir: DC Agent'?n e?itleme anl?k g?r?nt?s? ve se?ilmi? dizin kapsam?, kasadaki RDP/SSH kimlik bilgileri, eri?im denetim kay?tlar?, dizin i? kuyru?u ve daha ?nce y?klenmi? olabilecek taray?c? oturumlar?. Bu veriler ayn? kapsama veya ayn? yenilenme zaman?na sahip de?ildir; ekrandaki toplamlar? Active Directory'nin eksiksiz envanteri olarak yorumlamay?n.

Etki Alan? ekran? ?o?unlukla bir inceleme y?zeyidir. Baz? kartlar filtreli ayr?nt? ekran? a?ar, baz? metrikler ise yaln?z bilgi verir. Dolu bir bile?ende genel bir **?lgili ekrana git** men?s? bulunmaz; bu ?a?r? yaln?z bile?enin k???k bo? durumunda g?r?nebilir. Dolu g?r?n?mde yaln?z d??me olarak sunulan karta bas?n veya sol gezinmeden ilgili ?al??ma alan?na ge?in.

## Ekrandaki D?rt Bile?en

### Etki alan? envanteri

Canl? ajan oran?, kullan?c?, grup/OU ve risk sinyali metriklerini; sa?lay?c? ad?, son g?r?lme/e?itleme zaman? ve se?ilmi? oturum a?ma/kimlik bilgisi say?lar?n? g?sterir. Kayna??, yaln?z Sahip rol?nde ?al??an dizin sa?lay?c?s? sorgusudur. Bu bile?enin i?indeki topoloji, metrikler ve sa?lay?c? sat?rlar? salt okunurdur; ayr?nt? i?in sol gezinmeden Entegrasyonlar > Active Directory ekran?na ge?in.

### Etki alan? e?itleme sa?l???

Nesne da??l?m?ndaki t?klanabilir **Kullan?c?**, **Grup** ve **OU** sat?rlar? Entegrasyonlar'da kar??l?k gelen a?a? filtresini a?ar; say? s?f?rsa veya Sahip yetkisi yoksa pasiftir. **Cihaz**, **Ayr?cal?kl?** ve **Eski nesne** sat?rlar? salt okunurdur. **Ajan kuyru?u** kart?, bekleyen/kiralanm?? dizin i?i say?s?n? kullan?r ve de?er s?f?rdan b?y?kken sistem g?r?n?rl??? olan rolleri ??lemler ekran?na g?t?r?r. Di?er kapsam kartlar? ile ajan sa?l?k sat?rlar? bilgi ama?l?d?r.

### Uzak oturumlar

T?klanabilir RDP ve SSH kartlar?, kasadaki kimlik bilgisi kay?tlar?n?n say?s?n? ve bu kay?tlara ait denetim eri?imlerini birle?tirir; Active Directory Kay?tlar? ekran?n? ilgili protokole g?re filtreler. **AD oturum a?ma** kart? sa?lay?c?daki se?ilmi? oturum a?ma kapsam?n? g?sterir ve salt okunurdur. **Ajan kuyru?u** kart? dizin i?lerinden gelir ve ??lemler ekran?na gidebilir. Eri?im grafi?i denetim kay?tlar?ndan, taray?c? oturumu sat?rlar? ise oturum sorgusundan beslenir. Etki Alan? bu oturum sorgusunu ayr?ca ?al??t?rmad??? i?in yaln?z daha ?nce yetkili bir g?venlik ekran?nda y?klenmi? ?nbellek g?r?nebilir; g?ncel inceleme i?in Giri? G?venli?i ekran?n? kullan?n.

### Kimlik bilgisi ya?am d?ng?s?

Bu bile?en kasadaki Active Directory kimlik bilgileri ile bunlara ait denetim eri?imlerinden ?retilir; dizin se?imi toplamlar?n? kullanmaz. **Kimlik bilgileri**, **Y?netilen**, **S?resi dolan** ve **Bilgi eksik** kartlar? t?klanabilir ve Active Directory Kay?tlar? ekran?n? ilgili durum filtresiyle a?ar. **Kullan?mda** ve **G?ncellenen** kartlar? salt okunurdur. ?Y?netilmeyen? adl? bir ya?am d?ng?s? kart? yoktur. Eri?im grafikleri ile cihaz, kimlik bilgisi, son eri?im ve toplam s?tunlar?n? g?steren tablo da salt okunurdur.

## Yetki, Veri ve Ajan Yetenekleri

Etki alan? sa?lay?c? sorgusu yaln?z **Sahip** rol?nde etkinle?ir. **Y?netici**, **Denet?i** veya **Kullan?c?** ekran kabu?una ula?sa bile bo? ya da s?f?r de?erler ?ajan yok? anlam?na gelmez; bu durum **yetki nedeniyle veri y?klenmedi** olarak de?erlendirilmelidir. Sahip oturumunda da ?nce sorgunun tamamland???n? do?rulay?n.

Ajan?n ilan etti?i yetenekler g?sterilebilecek veri ve yap?labilecek i?lemleri s?n?rlar. Envanter i?in `READ_INVENTORY`, parola durumu i?in `READ_PASSWORD_STATE`; hesap a?ma, sonraki giri?te parola de?i?ikli?i isteme ve ge?ici parola atama i?in ilgili `UNLOCK_ACCOUNT`, `REQUIRE_PASSWORD_CHANGE` ve `RESET_TEMP_PASSWORD` yetenekleri gerekir. Bir yetenek yoksa s?f?r veya eksik metrik ?risk yok? demek de?ildir; veri toplanmam?? olabilir. Hassas dizin eylemleri ayr?ca ajan?n `CONNECTED` olmas?n?, lisans?n yaz?labilir kalmas?n?, Sahip rol?n? ve hedef hesab?n ayr?cal?kl? olmamas?n? gerektirir.

## ?nerilen ?nceleme Ak??lar?

### Ajan sa?l???n? do?rulama

1. Etki alan? envanterindeki canl? ajan oran?n?, sa?lay?c? durumunu ve son g?r?lme/e?itleme zaman?n? okuyun.
2. Durum etiketinin ?nceli?ini do?ru okuyun: ajan sa?l??? `CONNECTED` de?ilse ?nce `STALE`, `OFFLINE`, `AWAITING` veya `REVOKED` g?r?n?r. Ajan ba?l?yken hata varsa **HATA**, ard?ndan etkin e?itleme varsa **E??TLEN?YOR**, yaln?z bunlar yokken bekleyen komut varsa **E??TLEME KUYRUKTA** g?sterilir.
3. Ba?l? olmayan veya hata g?steren sa?lay?c? i?in sol gezinmeden Entegrasyonlar > Active Directory ekran?n? a??n ve sa?lay?c? kart?n? inceleyin.

Beklenen sonu? `CONNECTED` durumu ile ilerleyen son g?r?lme ve e?itleme zaman?d?r. Zaman ilerlemiyorsa yeni kimlik bilgisi aktar?m? veya kapsam de?i?ikli?i ba?latmay?n.

### Se?im kapsam?n? say?larla kar??la?t?rma

Etki alan? e?itleme sa?l???ndaki t?klanabilir **Kullan?c?**, **Grup** veya **OU** sat?r?n? a??n ve Entegrasyonlar'daki haz?rlanm?? filtreyi kontrol edin. Bilgisayar say?s? salt okunurdur; bilgisayar kapsam? i?in Entegrasyonlar'a sol gezinmeden ge?in. Beklenmeyen art?? veya d????te son ba?ar?l? e?itlemeyi ve ajan yeteneklerini kar??la?t?r?n. Tamamlanma ?l??t?, de?i?imin onayl? kapsam g?ncellemesiyle veya kaynak sistemde do?rulanm?? bir sorunla a??klanmas?d?r.

### RDP/SSH sinyalini inceleme

De?eri olan RDP ya da SSH kart?n? se?in; a??lan Active Directory Kay?tlar? ekran?nda protokol filtresinin uyguland???n? do?rulay?n. Kay?t kayna??n?, risk etiketini ve son e?itleme zaman?n? inceleyin. Taray?c? oturumu sat?r?n? veya eri?im grafi?ini t?klayarak ayr?nt? beklemeyin; bu b?l?mler yaln?z ?zet sunar.

### Ya?am d?ng?s? durumunu inceleme

Yaln?z **Kimlik bilgileri**, **Y?netilen**, **S?resi dolan** veya **Bilgi eksik** d??melerinden birini a??n. **Kullan?mda**, **G?ncellenen** ve eri?im tablosu yaln?z ?zet sunar. Kayna?? `ad_sync` olan bir kayd? elle yeniden olu?turmay?n. Kay?t ile dizin nesnesi uyu?muyorsa e?itleme tamamlanana kadar toplu i?lem ba?latmay?n.

## Ekran Durumlar?

| Durum | Operat?r cevab? |
| --- | --- |
| Y?kleniyor | Sahip rol?ne ait sa?lay?c? sorgusu tamamlanmadan toplamlar? ve bo? durumlar? yorumlamay?n. |
| Ba?l? (`CONNECTED`) | Hata, etkin e?itleme veya bekleyen komut yoksa son g?r?lme/e?itleme zamanlar?n? ve gerekli yetenekleri do?rulay?n. |
| HATA | Ba?l? ajan ?zerindeki hata, e?itleme ve kuyruk etiketlerinden ?nce g?sterilir; sa?lay?c? kart?ndaki son hatay? inceleyin. |
| E??TLEN?YOR (`SYNCING`) | Yaln?z ba?l? ve hatas?z ajanda g?r?n?r; i?lemin tamamlanmas?n? bekleyin. |
| E??TLEME KUYRUKTA | Yaln?z ba?l?, hatas?z ve e?itleme ?al??mayan ajanda g?r?n?r; bekleyen i?i ??lemler ekran?nda izleyin. |
| Bekliyor (`AWAITING`) | ?lk ajan yoklamas? tamamlanana kadar aktar?m ve hassas i?lem ba?latmay?n. |
| Bayat (`STALE`) | Ajan servisini, sunucu eri?imini ve sa?lay?c? kart?ndaki son hatay? kontrol edin. |
| ?evrimd??? (`OFFLINE`) | Yeni dizin i?lemlerini durdurun; servis ve ba?lant? kan?t?n? ?zel olarak toplay?n. |
| ?ptal edilmi? (`REVOKED`) | Eski ajan anahtar?n? kullanmay?n; Sahip onayl? yeniden kay?t veya onar?m ak???n? izleyin. |
| Yetki nedeniyle bo? | Sahip olmayan rolde s?f?r de?eri ?ajan yok? diye raporlamay?n; incelemeyi Sahip kullan?c?ya aktar?n. |
| Yetenek eksik | ?lgili veri veya eylemi desteklenmiyor kabul edin; eksik metri?i sa?l?kl? sonu? olarak yorumlamay?n. |
| Hata | Son ba?ar?l? e?itleme zaman?n? koruyun; art arda kapsam de?i?tirerek ilk hatay? g?lgelemeyin. |

## ??lemden ?nce

- Rol?n Sahip oldu?unu, sa?lay?c? sorgusunun tamamland???n? ve g?sterilen tarih-saat bilgilerinin g?ncel oldu?unu do?rulay?n.
- Ajan sa?l?k durumu ile son ba?ar?l? e?itleme zaman?n? birlikte de?erlendirin.
- ?htiya? duyulan veri veya eylem i?in gerekli ajan yetene?inin ilan edildi?ini kontrol edin.
- Ekrandaki salt-okunur metrik ile t?klanabilir filtre kart?n? birbirinden ay?r?n.
- Kimlik bilgisi aktar?m? i?in aktif kasan?n a??k, yaz?labilir ve kasa anahtar?n?n eri?ilebilir oldu?unu do?rulay?n.
- Ayr?cal?kl? hesaplarda hassas eylemleri zorlamay?n; kurumun onayl? Active Directory y?netim yolunu kullan?n.

## G?venli Kan?t

- **Payla??labilir:** ajan sa?l?k kategorisi, son g?r?lme/e?itleme ya??, nesne t?r?ne g?re kimliksizle?tirilmi? toplam, kuyruk durumu, ilan edilen yetenek ad? ve ki?isel veri i?ermeyen hata kodu.
- **Gizli kalmal?:** etki alan? ve etki alan? denetleyicisi adlar?, distinguished name, OU/grup yolu, bind kullan?c?s?, ajan anahtar?, ger?ek kullan?c? listesi, RDP/SSH hedefi ve dizin a?ac? ekran g?r?nt?s?.
- G?nl?k gerekiyorsa kullan?c?, etki alan?, IP, anahtar ve LDAP ayr?nt?lar?n? ??kar?n. Tam maskeleme m?mk?n de?ilse yaln?z ?zel destek kullan?n.

## Ne Zaman Y?kseltmelisiniz

Ajan `CONNECTED` durumuna d?nemiyorsa, e?itleme veya kuyruk ilerlemiyorsa, se?ilmi? kapsam beklenmedik bi?imde de?i?iyorsa, gerekli yetenek kaybolmu?sa ya da bu ekran Active Directory Kay?tlar? ile ?eli?iyorsa konuyu dizin y?netimi ekibine aktar?n. Ajan s?r?m?n?, genel sa?l?k durumunu, saat dilimi belirtilmi? tarih ve saati, hassas ayr?nt?lar? ??kar?lm?? hatay? ve denenen ?n kontrol ad?mlar?n? ekleyin.

## Operat?r Notlar?

Nesne say?lar? kapasite ve sa?l?k sinyalidir; herkese a??k kimlik envanteri de?ildir. Active Directory ve ajan, dizin kaynakl? kimlik bilgisi kay?tlar?n?n as?l kayna??d?r. Ayn? kayd? elle olu?turmak kopya ve yanl?? rotasyon riski do?urur.

## ?lgili

- [Active Directory ajan?](active-directory-agent.md)
- [Active Directory kay?tlar? ekran?](screen-active-directory-records.md)
- [Giri? g?venli?i ekran?](screen-sign-in-security.md)
- [DC Agent sorun giderme](../../kb/tr/dc-agent-service.md)
