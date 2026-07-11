# Bildirimler Ekran?

?st ?ubuktaki `?` simgesi Bildirimler ekran?na ait bu rehberi a?ar. Bu ekran, hangi kal?c? denetim olaylar?n?n SMTP e-postas?na aday olaca??n? ve e-postalar?n hangi adreslere y?nlendirilece?ini y?netir. SMTP sunucu ba?lant?s? ayr? **Sunucu ayarlar? > SMTP** sekmesindedir; ?st ?ubuktaki canl? uygulama bildirimleri ise farkl?, oturuma ba?l? bir y?zeydir.

## Eri?im, Rol ve Lisans S?n?r?

Sahip, Y?netici ve Denet?i sistem rolleri Bildirimler ekran?n? a?abilir. Yaln?z **Sahip** al?c?lar? ve olay se?imlerini de?i?tirebilir, ayarlar? kaydedebilir ve SMTP testi g?nderebilir. Y?netici ile Denet?i ayn? veriyi salt okunur g?r?r. Kullan?c? rol? sistem ayarlar?n? g?r?nt?leyemedi?i i?in bu ekrana eri?emez.

Bildirimler ayr? bir lisans ?zelli?iyle kapat?lmaz. Ekrandaki **Salt okunur** durumu lisans modunu de?il, Sahip d???ndaki sistem rol?n? anlat?r. Kasa yazmalar?n? kapatan salt okunur lisans da Sahip i?in bu sunucu d?zeyi ayarlar? veya SMTP testini kendili?inden devre d??? b?rakmaz; i?lem ?ncesinde kurum politikan?z? ayr?ca uygulay?n.

## Burada Ne Yap?l?r

- SMTP'nin a??k/kapal? durumunu, tan?ml? al?c? say?s?n? ve se?ili olay kural? say?s?n? okuyun.
- **E-posta al?c?lar?** alan?nda adresleri ekleyin, tekille?tirin veya kald?r?n.
- **Test al?c?s?** ile ge?erli SMTP form de?erlerini kaydetmeden ?nce kontroll? olarak s?nay?n.
- **T?m?**, **Se?ilenler**, **Info**, **Suspicious** ve **Critical** filtreleriyle olay katalo?unu daralt?n.
- Tek bir olay?n, b?t?n bir ?nem grubunun veya t?m katalo?un e-posta se?imini de?i?tirin.
- Her sat?rdaki **An?nda**, sessizlik aral??? veya e?ik politikas?n? okuyup g?r?lt? ve g?r?n?rl?k dengesini kurun.
- **Bildirimleri kaydet** ve **S?f?rla**, Bildirimler ile di?er Sunucu ayarlar? sekmelerinin payla?t??? formun tamam?nda ?al???r. Ba?ka bir sekmede kaydedilmemi? de?i?iklik varken bu d??meleri kullanmay?n.

## Ekran?n Yap?s?

Bildirimler ekran?n?n kendi i?inde sekme yoktur. ?st durum ?eridi ve iki ana alan bulunur:

- SMTP durum d??mesi ve **SMTP ayarlar?**, **Sunucu ayarlar? > SMTP** sekmesini a?ar.
- **Teslimat** alan? al?c? listesini ve test g?nderimini i?erir.
- **Olay kurallar?** alan? filtreleri, toplu se?imleri, ?nem gruplar?n? ve tek tek olay sat?rlar?n? i?erir.

Durum ?eridindeki **G?nderime haz?r**, yaln?z formda SMTP a??k, host ve g?nderen adresi dolu, en az bir al?c? ve en az bir olay se?ili oldu?u anlam?na gelir. SMTP ba?lant?s?n?n ?al??t???n?, uzak sunucunun iletiyi kabul etti?ini veya al?c?n?n gelen kutusuna teslim edildi?ini kan?tlamaz.

## Teslimat ve SMTP

### Al?c? listesi

Her sat?r, virg?l veya noktal? virg?l ayr? al?c? kabul edilir. Adresler kaydetme ?ncesinde k???k harfe ?evrilir, bo? girdiler kald?r?l?r ve ayn? adres yaln?z bir kez tutulur. SMTP a??kken host, g?nderen e-posta ve en az bir al?c? zorunludur. Kimlik do?rulama a??ksa kullan?c? ad? ile yeni ya da ?nceden kaydedilmi? parola/eri?im anahtar? gerekir.

Bildirimler ekran? SMTP hesab?, host, port, g?nderen adresi, TLS/STARTTLS, kimlik do?rulama kullan?c? ad? veya parolay? d?zenlemez. Bunlar **SMTP ayarlar?** ?zerinden ayr? sekmede y?netilir. SMTP kapat?ld???nda ba?lant? ayr?nt?lar? saklan?r; denetim kay?tlar? ve oturum i?i uygulama bildirimleri devam eder, e-posta g?nderimi durur. Bu s?rada olu?an olaylar?n e-posta adaylar? i?leme s?ras?nda atlan?r ve ilgili ??k?? kuyru?u sat?rlar? silinir; SMTP yeniden a??ld???nda geriye d?n?k g?nderilmez.

### Test g?nderimi

**Test g?nder** yaln?z Sahip rol?nde, SMTP a??kken ve ba?ka test s?rerken de?ilken kullan?labilir. Test i?in ?u de?erler gerekir:

- Ge?erli `1-65535` portu,
- SMTP hostu ve g?nderen e-posta,
- ayr? **Test al?c?s?**,
- kimlik do?rulama a??ksa kullan?c? ad? ile formdaki veya ?nceden kaydedilmi? parola/eri?im anahtar?.

Test, hen?z kaydedilmemi? ge?erli SMTP form de?erlerini kullanabilir. SMTP a??kken sunucu test iste?inde de en az bir bildirim olay? se?imi ister; se?im s?f?rsa d??me kullan?labilir g?r?nse bile test do?rulamada reddedilir. Sunucu on dakikada en fazla be? test iste?i kabul eder. Ba?ar? mesaj?ndaki adres, SMTP sunucusunun al?c?y? kabul etti?ini g?sterir; gelen kutusuna, karantinaya veya son kullan?c?ya kesin teslim kan?t? de?ildir. Ba?ar?l? test `SERVER_MAINTENANCE` denetim olay? yazar. Ba?ar?s?z test ekranda hata ve canl? uygulama bildirimi ?retir, ancak otomatik olarak ba?ar?l? teslimat kan?t? olu?turmaz. Mevcut test e-postas? ?ablonu T?rk?e haz?rlan?r; aray?z dilini de?i?tirmek test iletisinin dilini de?i?tirmez.

## Olay Kurallar? ve ?nem Gruplar?

Filtreler yaln?z g?r?n?r sat?rlar? de?i?tirir; kay?tl? se?imi de?i?tirmez:

| Filtre | G?sterdi?i |
| --- | --- |
| T?m? | SMTP i?in tan?ml? b?t?n denetim olaylar?. |
| Se?ilenler | ?u anda e-posta aday? olarak i?aretlenmi? olaylar. |
| Info | Bak?m ve bilgilendirme olaylar?. |
| Suspicious | ??pheli eri?im ve inceleme isteyen sinyaller. |
| Critical | Kritik g?venlik ve i?lem gerektiren olaylar. |

**T?m?n? se?** b?t?n olaylar? i?aretler. **Temizle** b?t?n i?aretleri kald?r?r. SMTP a??kken se?im s?f?rsa **Bildirimleri kaydet** kapal? kal?r ve SMTP testi de sunucu do?rulamas?nda reddedilir; kaydetmeden veya test etmeden ?nce en az bir olay se?in. SMTP kapal?yken olay se?imi olmadan ayar kaydedilebilir.

Grup ba?l???ndaki onay kutusu o ?nem d?zeyindeki b?t?n olaylar? a?ar veya kapat?r; k?smi se?im kutuda karma durum olarak g?r?n?r. Tek sat?r kutusu yaln?z o olay? de?i?tirir. Se?ilmemi? olaylar silinmez ve Denetim Ge?mi?inde kal?r; yaln?z SMTP e-postas?na aday olmaz.

### ?letim politikas?

Se?ilmi? olmak her olayda hemen bir e-posta g?nderilece?i anlam?na gelmez. Her sat?r kendi politikas?n? g?sterir:

- **An?nda:** olay olu?tu?unda SMTP kuyru?una aday olur.
- **?lk olay, sonra N dk sessizlik:** ilk olay aday olur; ayn? grup sessizlik s?resince bast?r?l?r.
- **N olay / M dk:** yaln?z belirtilen zaman aral???nda e?ik olu?tu?unda aday olur.

Gruplama olaya g?re akt?r veya akt?r-hedef temelinde yap?labilir. Sunucu aday e-postalar? kal?c? ??k?? kuyru?unda i?ler ve ge?ici hatalar? s?n?rl? say?da yeniden dener; kal?c? ret veya deneme s?n?r? son teslimi engelleyebilir. Bildirimler ekran?nda al?c? bazl? teslim makbuzu, okunma bilgisi veya ??k?? kuyru?u ge?mi?i yoktur. Bu nedenle kural se?imi ya da **Kurallar haz?r** durumu teslimat garantisi de?ildir.

## Canl? Bildirimler ile Kal?c? Olaylar?n Fark?

?st ?ubuktaki zil ve yakla??k 5,2 saniye g?r?nen anl?k bildirimler, bu taray?c? oturumundaki i?lem ba?ar?lar?, hatalar? ve sistem iletileridir. En fazla ?? anl?k bildirim ayn? anda g?sterilir. Zil merkezi oturum belle?inde en fazla 30 bildirimi tutar ve son sekizini listeler; ayn? t?r ve metindeki tekrarlar tek kayda indirgenir.

**Okundu i?aretle** zaman damgas?n? koruyarak mevcut kay?tlar? okundu yapar. Okunmu? kay?t varsa **Okunanlar? temizle** yaln?z onlar? kald?r?r; hi? okunmu? kay?t yoksa **T?m?n? temizle** ge?erli oturum listesini bo?alt?r. Tek sat?rdaki kapatma d??mesi o bildirimi ve varsa a??k anl?k bildirimi kald?r?r.

Bu canl? liste sunucu veritaban?na kal?c? yaz?lmaz ve sayfa/oturum yenilenince geri gelmesi beklenmez. Zil merkezini temizlemek Denetim Ge?mi?ini, SMTP ??k?? kuyru?unu, kay?tl? olay kurallar?n? veya g?nderilmi? e-postay? silmez. Tersine, bir denetim olay?n?n kal?c? olmas? onun mutlaka canl? bildirim ya da e-posta ?retece?i anlam?na gelmez.

## ?nerilen ?? Ak??lar?

### ?lk SMTP bildirim kurulumunu do?rulama

1. **SMTP ayarlar?** ?zerinden SMTP'yi a??n; host, port, g?nderen, TLS ve gerekiyorsa kimlik do?rulamay? doldurun.
2. Bildirimler ekran?na d?n?p en az bir ger?ek al?c? girin.
3. ?nce dar bir olay k?mesi se?in; her sat?r?n e?ik veya sessizlik politikas?n? okuyun.
4. Ayr? test al?c?s?na **Test g?nder** kullan?n ve SMTP kabul sonucunu do?rulay?n.
5. Gelen kutusu, istenmeyen posta/karantina ve kurum a? ge?idi kay?tlar?n? ayr?ca kontrol edin.
6. Di?er Sunucu ayarlar? sekmelerinde kaydedilmemi? de?i?iklik olmad???n? do?rulay?n; ard?ndan **Bildirimleri kaydet** se?ene?ini kullan?p sayfay? yeniden a?arak al?c? ve olay say?lar?n?n korundu?unu do?rulay?n.

### G?r?lt?y? azaltma

1. **Se?ilenler** filtresiyle yaln?z e-posta aday? olaylar? g?sterin.
2. ?nce y?ksek hacimli sat?rlar?n e?ik ve sessizlik politikas?n? okuyun.
3. ?nsan m?dahalesi gerektirmeyen sat?rlar? tek tek kapat?n; b?t?n ?nem grubunu yaln?z a??k bir kurum karar?yla kapat?n.
4. Ayar? kaydedin ve de?i?meyen olaylar?n Denetim Ge?mi?inde kalmaya devam etti?ini do?rulay?n.

## Ekran Durumlar?

| Durum | Operat?r cevab? |
| --- | --- |
| Sunucu ayarlar? y?kleniyor | Panelde ayr? iskelet yoktur; de?erler y?klenene kadar varsay?lan SMTP kapal? g?r?n?m?n? kesin durum saymay?n ve kaydetmeyin. |
| Sunucu ayarlar? al?namad? | Panel ayr? hata kart? g?stermeyebilir. Beklenen al?c? veya kurallar yoksa Sunucu ayarlar?n? ve ba?lant?y? do?rulay?p sayfay? yenileyin; bo? formu mevcut ayarlar?n ?st?ne yazmay?n. |
| SMTP kapal? | E-posta g?nderimi yoktur; denetim ve oturum i?i bildirimler devam eder. Bu s?rada atlanan e-posta adaylar? kuyruktan silinir ve SMTP yeniden a??ld???nda geriye d?n?k g?nderilmez. |
| Eksik ayar var | SMTP a??k olsa da host, g?nderen, al?c? veya olay se?imi eksiktir; haz?r kabul etmeyin. |
| G?nderime haz?r / Kurallar haz?r | Yaln?z form b?t?nl??? sa?lanm??t?r; test ve al?c? taraf? do?rulamas? h?l? gerekir. |
| Al?c? yok | SMTP a??kken en az bir ge?erli adres ekleyin. |
| Olay se?ili de?il | SMTP a??ksa en az bir olay se?meden kaydedemezsiniz; test d??mesi kullan?labilir g?r?nse bile sunucu test iste?ini do?rulamada reddeder. |
| Filtrede olay yok | **T?m?** veya ba?ka ?nem filtresine ge?in; kay?tl? se?im kendili?inden de?i?mez. |
| Test g?nderiliyor | ?kinci test ba?latmay?n; sonu? veya hata bildirimini bekleyin. |
| Test kabul edildi | SMTP sunucusu adresi kabul etmi?tir; gelen kutusu teslimini ayr? do?rulay?n. |
| Test g?nderilemedi | Host, port, TLS, kimlik do?rulama, g?nderen, al?c? ve a? eri?imini gizli de?er g?stermeden kontrol edin. |
| Rol nedeniyle salt okunur | Y?netici ve Denet?i kurallar? g?rebilir fakat de?i?tiremez, kaydedemez veya test g?nderemez. |
| Kaydedilmemi? de?i?iklik | Payla??lan form ba?ka Sunucu ayarlar? sekmelerindeki de?i?iklikleri de i?erir. **Bildirimleri kaydet** bunlar? birlikte yazabilir; **S?f?rla** bunlar? da son y?klenen de?erlere d?nd?rebilir. |
| Canl? bildirim yok | Bu yaln?z ge?erli taray?c? oturumunda yeni i?lem sonucu olmad???n? g?sterir; denetim ge?mi?inin bo? oldu?unu g?stermez. |

## ??lemden ?nce

- Oturum rol?n? kontrol edin; al?c?, kural, SMTP testi ve kaydetme i?lemleri i?in Sahip gerekir.
- **Bildirimleri kaydet** veya **S?f?rla** kullanmadan ?nce di?er Sunucu ayarlar? sekmelerinde kaydedilmemi? de?er olmad???n? do?rulay?n; bu i?lemler payla??lan formun tamam?n? etkiler.
- SMTP kanal?n?n a??k oldu?unu ve **G?nderime haz?r** ifadesinin yaln?z form yeterlili?i oldu?unu unutmay?n.
- Al?c? adresinin kurum i?i onay?n?, veri s?n?fland?rmas?n? ve n?bet sorumlulu?unu do?rulay?n.
- Olay sat?r?n?n ?nem grubunu ve ger?ek iletim politikas?n? okuyun; se?ili olay? otomatik olarak an?nda e-posta sanmay?n.
- De?i?iklik ?ncesi mevcut al?c? say?s?n? ve se?ili olay say?s?n? kaydedin; gizli adresleri a??k kan?ta koymay?n.
- Testte kaydedilmemi? SMTP de?erlerinin kullan?labilece?ini ve h?z s?n?r? oldu?unu hesaba kat?n.
- Canl? zil bildirimleri ile kal?c? Denetim Ge?mi?ini birbirinin yerine kullanmay?n.

## G?venli Kan?t

- Payla??labilir: SMTP a??k/kapal? s?n?f?, redakte host s?n?f?, port ve TLS modu, al?c? say?s?, olay ad?/?nem grubu, iletim politikas?, genel hata kodu ve geni? zaman aral???.
- Gizli kalmal?: SMTP kullan?c? ad? ve parola/eri?im anahtar?, ger?ek al?c? ve g?nderen adresleri, tam host ad?, ileti kimli?i, konu/g?vde, denetim hedefi, kullan?c?/kasa ad?, olay zaman? ve kurum i?i y?nlendirme bilgisi.
- Test sonucu payla??rken kabul edilen ger?ek adresi, SMTP hostunu ve ileti kimli?ini maskeleyin; **kabul edildi** ifadesini son teslim kan?t? olarak sunmay?n.
- Ekran g?r?nt?s?nde yaln?z k?rpma yapmay?n; adres, host, olay hedefi, kullan?c?, zaman ve m??teri ba?lam?n? tamamen maskeleyin.

## Ne Zaman Durmal? ve Destek ?stemelisiniz

Y?klenen de?erlerin g?ncel oldu?undan emin de?ilseniz, beklenen al?c?lar kaybolduysa, SMTP testi yanl?? adrese gittiyse, kimlik bilgisi a??k kanala d??t?yse, kritik olaylar denetimde bulundu?u h?lde kuyruk/posta kan?t? olu?muyorsa veya ayn? kural beklenmedik ?l??de fazla ileti ?retiyorsa de?i?iklik yapmay? b?rak?n. Gizli de?er eklemeden; genel SMTP durumu, redakte olay ad?, iletim politikas?, geni? zaman aral???, hata kodu ve son g?venli ad?mla ?zel destek kayd? a??n.

## Operat?r Notlar?

Bildirimler ekran? bir posta kutusu veya teslimat izleme konsolu de?ildir. Al?c? ve olay kurallar?n? kaydeder; ger?ek SMTP ba?lant? ayr?nt?lar? Sunucu ayarlar?ndad?r. Denetim kayd?, SMTP kuyru?u/e-postas? ve taray?c? oturumundaki canl? bildirim ?? ayr? ya?am d?ng?s?ne sahiptir.

SMTP parolas?/eri?im anahtar?, ger?ek e-posta adresi, m??teri hostu, ileti kimli?i, tam hata yan?t? veya olaya ?zel gizli de?er i?eren bildirim ?rne?ini yay?mlamay?n.

## ?lgili

- [Sunucu ayarlar? ekran?](screen-server-settings.md)
- [Denetim Ge?mi?i ekran?](screen-audit-log.md)
- [Denetim ve g?venlik duru?u](audit-and-security-posture.md)
- [Sunucu ayarlar? yeniden ba?latma ve bak?m bilgi bankas?](../../kb/tr/server-settings-restart-maintenance.md)
