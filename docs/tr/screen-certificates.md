# Sertifikalar Ekran?

?st ?ubuktaki `?` simgesi Sertifikalar ekran?na ait bu rehberi a?ar. Bu ekran, se?ili kasada tutulan sertifika, sertifika paketi ve ?zel anahtar kay?tlar? i?indir. VaultPilot sunucusunun HTTPS sertifikas?n? kurmaz veya de?i?tirmez; canl? yay?n sertifikas? **Sunucu ayarlar?** i?indeki ayr? ak??tan y?netilir.

Denet?i rol? gizli kay?tlara ve kasa anahtar?na eri?emez. Sahip, Y?netici ve Kullan?c? rolleri yaln?z kendilerine a??lm?? kasalar? kullan?r. Se?ili kasadaki **G?r?nt?leyici** kayd? okuyabilir, gizli materyali ge?ici g?sterebilir, kopyalayabilir ve varsa ?zg?n dosyay? indirebilir. **D?zenleyici** ile kasa **Y?neticisi**, lisans yaz?labilir durumdayken kay?t olu?turabilir, ?o?altabilir, d?zenleyebilir ve silebilir.

## Burada Ne Yap?l?r

- **Sertifikalarda ara** ile ba?l?k, sahip/servis, u? nokta, kategori, etiket, imzalayan, Subject/CN ve seri numaras? i?inde aray?n.
- **Yenileme**, **S?resi doldu**, **Tarih yok** ve **?ptal / pasif** h?zl? filtrelerini; ge?erlilik aral???, sertifika otoritesi ve organizasyon gibi ak?ll? filtrelerle birle?tirin. H?zl? filtre d??mesi yaln?z ilgili kay?t say?s? s?f?rdan b?y?kse g?r?n?r.
- Kart veya tablo g?r?n?m?n? se?in ve yenile d??mesiyle se?ili kasay? yeniden sorgulay?n.
- Yazma yetkiniz varsa **Yeni sertifika** ile edit?r? a??n; edit?rdeki **Sertifika dosyas?n? i?e aktar** alan?n? kullan?n veya sertifika/?zel anahtar materyalini metin olarak yap??t?r?n.
- Sat?r eylemleriyle gizli materyali g?sterin, ?zg?n dosyay? indirin veya men?den ayr?nt?lar? a??n, gizli de?eri kopyalay?n, kay?t kopyas? olu?turun, d?zenleyin ya da silin.

## Ekran? Nas?l Okumal?s?n?z

Liste sat?r? ba?l??? ve son g?ncelleme zaman?n? g?sterir. ??e aktar?lm?? kay?tlarda dosya ad?, bi?im, boyut, kalan s?re, Subject/CN, imzalayan ve SHA-256 ?zetinin k?sa b?l?m? de g?r?nebilir. Bunlar kasa a??ld?ktan sonra kayd? tan?mlayan meta verilerdir; sertifika g?vdesi, ?zel anahtar veya paket i?eri?i de?ildir.

**Sertifika ayr?nt?lar?n? a?** yan paneli kaynak, risk, kay?t durumu, hesap/servis, hedef, kategori, sahip, etiket ve son g?ncelleme gibi ba?lam? g?sterir. Gizli materyali veya ?zg?n dosyay? a???a ??karmaz ve tek ba??na `VIEW` denetim olay? yazmaz.

G?z d??mesi onaydan sonra materyali ?nce taray?c? oturumunda g?r?n?r yapar, ard?ndan `VIEW` olay?n? yazmay? dener. **Gizli de?eri kopyala** ?nce t?m gizli alan? panoya al?r, ard?ndan `COPY` olay?n? yazmay? dener. **Sertifika dosyas?n? indir** yaln?z indirilebilir ?zg?n dosya bulunan kay?tlarda etkinle?ir; dosyay? ?nce indirir, ard?ndan `EXPORT` olay?n? yazmay? dener. Sunucunun denetim iste?ini reddetmesi tamamlanm?? yerel g?sterme, kopyalama veya indirme i?lemini geri almaz; aray?z hata g?sterebilir ve operat?r sonucu denetim kayd?yla uzla?t?rmal?d?r. Gizleme de?eri yeniden maskeler.

### Meta veri ile gizli materyal s?n?r?

Ba?l?k, sahip/servis, u? nokta, not, ge?erlilik tarihi, Subject/CN ve sertifika otoritesi s?n?fland?rmas? kasa a??kken g?r?n?r kay?t ba?lam?d?r. Bunlar da ?ifreli kay?t y?k?nde saklan?r, ancak g?r?nt?lenmeleri i?in ayr?ca gizli de?eri g?sterme onay? gerekmez.

**Sertifika veya ?zel anahtar** alan? zorunlu gizli de?erdir ve varsay?lan olarak maskelenir. Dosya i?e aktar?ld???nda ?zg?n dosya baytlar? ile haz?rlanan materyal ?ifreli kay?t y?k?ne al?n?r. PFX/P12 parolas? i?in ayr? alan yoktur. Paket parolas?n? ba?l?k, sahip/servis, u? nokta veya not alan?na yazmay?n; gerekiyorsa ayr? bir parola kayd?nda y?netin.

Sertifika otoritesi kartlar?nda sa?lay?c? ad?, sinyal a??klamas? ve eri?im bi?imi etiketi g?sterilir. Bir kart se?ildi?inde ?nceki tan?nan sertifika otoritesi etiketi de?i?tirilir, kategori `Certificate` yap?l?r, kaynak bo?sa `manual` atan?r ve `certificate` etiketiyle se?ilen otorite etiketi eklenir. DigiCert, GoDaddy, GlobalSign, Let?s Encrypt, Microsoft CA veya Self-signed se?mek d?? hizmete ba?lanmaz; sertifika d?zenleme, yenileme, yeniden anahtarlama veya iptal i?lemi ba?latmaz.

## ?nerilen ?? Ak??lar?

### Dosyadan sertifika kayd? olu?turma

1. Yazma yetkili kasay? a??p **Yeni sertifika** se?ene?ini kullan?n.
2. Zorunlu ba?l??? girin; sahip/servis ile ilgili u? noktay? kay?t ba?lam? olarak doldurun.
3. **Sertifika dosyas?n? i?e aktar** alan?ndan PEM, CRT, CER, DER, P7B/P7C, PFX/P12, PKCS12, P8/P8E/PK8 veya KEY dosyas? se?in. Dosya s?n?r? 10 MB?t?r.
4. Dosya ad?, bi?im, boyut, i?e aktar?m zaman?, SHA-256 ve bulunabildiyse ge?erlilik/Subject bilgilerini kontrol edin.
5. Gerekiyorsa **Ge?erlilik biti?i** ile **Subject / CN** alanlar?n? d?zeltip sertifika otoritesi s?n?fland?rmas?n? se?in.
6. Gizli alan?n do?ru materyali i?erdi?ini do?rulay?p kayd? saklay?n.

Metin dosyalar?nda Subject, imzalayan, seri numaras? ve biti? zaman? yaln?z tan?nan sat?rlardan ??kar?labilir. ?kili paketlerde bu alanlar otomatik dolmayabilir. Bo? meta veri tek ba??na ge?ersiz paket kan?t? de?ildir; kayna?? ?zel kanaldan do?rulay?n.

### Materyali elle ekleme veya kayd? yenileme

Dosya se?meden ba?l?k girip PEM, sertifika g?vdesi veya ?zel anahtar materyalini zorunlu gizli alana yap??t?rabilirsiniz. Ge?erlilik biti?i ile Subject/CN elle eklenebilir. Elle olu?turulan kay?tta indirilebilir ?zg?n dosya bulunmaz; indirme gerekiyorsa kayd? **D?zenle** ile a??p yetkili kaynak dosyas?n? yeniden i?e aktar?n.

Yenileme incelemesinde ?nce **Yenileme**, **S?resi doldu** ve **Tarih yok** filtrelerini kontrol edin; gerekirse ge?erlilik aral??? veya sertifika otoritesi filtresi ekleyin. Yenilemeyi ilgili sertifika otoritesi ya da kurum s?recinde tamamlay?n. Yeni dosya haz?r oldu?unda mevcut kayd? **D?zenle** ?zerinden g?ncelleyin; s?n?fland?rma kart?n?n yenileme yapmad???n? unutmay?n.

### Materyali g?r?nt?leme, kopyalama veya indirme

Gizli de?eri yaln?z ihtiya? an?nda ve ekran payla??m? kapal?yken g?sterin. Kopyalama sonras? 30 saniyelik pano temizli?i en iyi ?aba yakla??m?yla ?al???r: VaultPilot yaln?z izinler elverirse panoyu okuyabilir ve de?er h?l? ayn?ysa temizleyebilir. ?zin hatas? veya arada panoya yaz?lan farkl? bir de?er temizli?i engeller; ?nceki kopyalama geri al?nm?? olmaz. ?ndirme d??mesi kapal?ysa kay?t elle girilmi? materyal veya indirilebilir ?zg?n dosyas? olmayan eski bir paket i?eriyor olabilir. Dosyay? yetkili kaynaktan yeniden i?e aktar?n; ekranda olmayan bir d?n??t?rme ya da paket parolas? ??zme i?lemi varsaymay?n.

## Ekran Durumlar?

| Durum | Operat?r cevab? |
| --- | --- |
| Y?kleniyor | ?skelet sat?rlar tamamlanmadan sonu? ??karmay?n. |
| Kay?t yok | Yazma yetkiniz varsa ilk kayd? olu?turun; yoksa do?ru kasa ve rol? do?rulay?n. |
| E?le?me yok | Aramay? ve aktif ak?ll? filtreleri temizleyin. |
| Ge?erli | Kalan s?reyi, kullan?lan u? noktay? ve yenileme sorumlusunu yine de do?rulay?n. |
| Yenileme aral???nda | 30 g?n veya daha az kalan kayd? kurumun yenileme s?recine al?n. |
| S?resi doldu | Materyali kullan?ma vermeyin; kaynak durumunu ve yerine ge?en sertifikay? do?rulay?n. |
| Tarih yok | Biti? tarihini yetkili kaynaktan tamamlay?n; bo? de?eri s?n?rs?z ge?erlilik saymay?n. |
| ?ptal / pasif | Kayd? etkin sertifika gibi kullanmay?n; kaynak sistemle uzla?t?r?n. |
| Sertifika okunuyor | ??e aktar?m bitmeden kaydetmeyin veya ikinci dosya se?meyin. |
| Dosya ?ok b?y?k / okunamad? | 10 MB s?n?r?n? ve desteklenen bi?imi do?rulay?n; dosyay? a??k kanala y?klemeyin. |
| ?ndirme kapal? | ?ndirilebilir ?zg?n dosya yoktur; gerekiyorsa yetkili kaynaktan yeniden i?e aktar?n. |
| Yazma kapal? | Kasa rol?n? ve lisans?n salt okunur durumunu kontrol edin. |

## ??lemden ?nce

- Se?ili kasay? ve kasa rol?n?z?n yapmak istedi?iniz i?leme izin verdi?ini do?rulay?n.
- Kay?t yazmadan ?nce lisans?n salt okunur olmad???n? kontrol edin.
- ??lemin kasa kayd?n? m? yoksa sunucunun canl? HTTPS sertifikas?n? m? hedefledi?ini kesinle?tirin.
- Dosya kayna??n?, beklenen SHA-256 ?zetini, Subject/CN bilgisini, imzalayan? ve biti? tarihini g?venilir kanaldan do?rulay?n.
- G?sterme, kopyalama ve indirme i?lemlerinin s?ras?yla `VIEW`, `COPY` ve `EXPORT` denetim olaylar? istedi?ini hesaba kat?n.
- Toplu kategori, etiket, ar?ivleme, pasifle?tirme, not, d?zenleme ve silme eylemlerinin D?zenleyici/Y?netici kasa rol? istedi?ini do?rulay?n.

## G?venli Kan?t

- **Payla??labilir:** sertifika durum s?n?f?, genel ge?erlilik aral???, dosya bi?imi ve boyutu, sertifika otoritesi s?n?f? ve SHA-256 ?zetinin k?sa b?l?m?.
- **Gizli kalmal?:** sertifika veya ?zel anahtar materyali, ?zg?n PEM/KEY/PFX/P12 paketi, paket parolas?, tam seri numaras? ve parmak izi, i? sistem ad?, tam Subject/issuer bilgisi, m??teri u? noktas? ve a??k kay?t ekran g?r?nt?s?.
- Deste?e g?nderilen g?r?nt?de ba?l?k, sahip/servis, URL, Subject/CN, imzalayan ve tam SHA-256 de?erini maskeleyin.
- ?zel anahtar veya paket parolas? a???a ??kt?ysa kopyalama ve yeniden paketlemeyi b?rak?p kurumun olay m?dahale ve sertifika otoritesi s?recini ?zel kanaldan ba?lat?n.

## Ne Zaman Durmal? ve Destek ?stemelisiniz

Dosyan?n SHA-256 ?zeti beklenen de?erle uyu?muyorsa, Subject/issuer veya biti? tarihi kaynak kay?ttan farkl?ysa, ?zg?n dosyan?n kayna?? do?rulanam?yorsa, gizli materyal yanl?? ki?iye g?sterildiyse ya da kasa kayd? canl? sunucu sertifikas? san?l?yorsa durun. Gizli materyali g?ndermeden; kay?t kimli?i, genel bi?im ve boyut, k?sa SHA-256 b?l?m?, hassas ayr?nt?lar? ??kar?lm?? hata ve denenen ad?mlarla ?zel destek kayd? a??n.

## Operat?r Notlar?

Kasa sertifika kayd? bir da??t?m arac? veya sertifika otoritesi istemcisi de?ildir. Dosya i?e aktarmak VaultPilot sunucusunun HTTPS ba??n? de?i?tirmez; canl? yay?n sertifikas? yaln?z **Sunucu ayarlar?** ak???nda y?netilir. Yenileme, sertifika otoritesi ve da??t?m notlar? operasyon ba?lam?d?r, otomatik i?lem de?ildir.

## ?lgili

- [Sertifika Paneli ekran?](screen-certificate-dashboard.md)
- [Sunucu ayarlar? ekran?](screen-server-settings.md)
- [Genel eri?im adresi ve HTTPS](public-host-https-certificate.md)
