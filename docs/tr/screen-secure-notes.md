# G?venli Notlar Ekran?

?st ?ubuktaki `?` d??mesi bu sayfay? **G?venli Notlar** ekran?ndan a?ar. Bu ekran; kurtarma ad?mlar?, bak?m s?ras?nda izlenecek ?zel y?nergeler veya yaln?z yetkili ki?ilerin g?rmesi gereken operasyon notlar? gibi yap?land?r?lm?? bir kay?t t?r?ne s??mayan hassas metinler i?indir. Parola, API anahtar?, sertifika veya dosya kendi kay?t t?r?nde tutulmal?d?r.

Kay?tlar? okuyabilmek i?in a??k bir kasaya eri?iminiz olmal?d?r. Yeni not olu?turma, mevcut notu de?i?tirme, kopyalama veya silme i?lemleri i?in kasada yazma yetkisi ve yaz?labilir lisans gerekir.

## Ekran? Tan?y?n

- **Se?ili ekranda ara** alan? not g?vdesini veya iste?e ba?l? gizli alan? taramaz. Arama; ba?l?k, sahip/ekip, sistem veya referans, URL, sunucu ve etki alan? bilgileri ile kategori, etiket, kaynak ve risk gibi g?r?n?r meta verilerde ?al???r.
- **Ak?ll? filtre ekle** ile kategori, etiket, risk ve kaynak gibi birden fazla ?l??t? birlikte kullanabilirsiniz. Etkin filtreler ayr? rozetler halinde g?r?n?r; **Temizle** t?m?n? kald?r?r.
- T?r filtreleri ve saya?lar g?r?n?r kay?t k?mesini daralt?r. **Kart** ve **Tablo** d??meleri yaln?z g?r?n?m? de?i?tirir; kayd? de?i?tirmez.
- Her sat?rda gizli i?eri?i g?sterme, panoya kopyalama ve i?lem men?s? bulunur. Men?den **Kopyas?n? olu?tur**, **Kayd? d?zenle** veya **Kayd? sil** se?eneklerine ula??l?r.
- **Toplu i?lemler** men?s?ndeki **Excel ?ablonu indir** yazma yetkisi istemez. **Excel?den i?eri aktar** ise yaz?labilir kasa gerektirir ve kay?t eklemeden ?nce ?ak??ma se?enekleriyle bir ?nizleme g?sterir.
- Kay?t se?ildi?inde **Se?ilenleri d??a aktar**, **G?venlik kontrol? ba?lat** ve **Denetim raporuna ekle** salt okunur kullan?mda da a??k kalabilir. **Kategori ata**, **Etiket ata**, **Ar?ivle**, **Pasifle?tir / iptal et**, **Toplu not ekle**, **Se?iliyi d?zenle** ve **Onayla ve kald?r** kasada yazma yetkisi ister. **Toplu payla?** se?imle a??l?r; paketi ger?ekten olu?turabilmek i?in Payla??m ekran?ndaki kasa ve rol ko?ullar? ayr?ca uygulan?r.

## Temel ?? Ak??lar?

### Yeni bir g?venli not olu?turma

1. G?venli Notlar ekran?ndaki **Yeni g?venli not** d??mesini se?in. Bu d??me t?r se?imi istemeden do?rudan g?venli not formunu a?ar.
2. Ba?l??a gizli bilgi yazmadan notun amac?n? anlatan k?sa bir ad verin. ??eri?i, yaln?z do?ru kasaya ve do?ru ki?ilere a??k olacak ?ekilde haz?rlay?n.
3. Sonraki incelemede i?e yarayacak kategori ve etiketleri ekleyin; genel prosed?r metnini gereksiz yere kasaya kopyalamay?n.
4. Kaydetmeden ?nce hedef kasay? do?rulay?n. Kay?t sat?r?ndaki i?lem men?s? daha sonra **Kopyas?n? olu?tur**, **Kayd? d?zenle** ve **Kayd? sil** se?eneklerini sunar.

Beklenen sonu?: Not listede g?r?n?r ve i?eri?i yaln?z kasa a??ld?ktan sonra g?r?nt?lenebilir. Kay?t engellenirse formdaki gizli metni destek mesaj?na kopyalamay?n; yetki, lisans ve kasa durumunu ayr? ayr? kontrol edin.

### Bir notu bulma ve g?venle okuma

1. Arama ve filtrelerle g?r?n?r kay?tlar? daralt?n; not g?vdesinin arama dizinine al?nmad???n? unutmay?n.
2. Do?ru ba?l??? ve son g?ncelleme zaman?n? do?rulay?n.
3. **Gizli de?eri g?ster** se?ildi?inde VaultPilot ?nce **Gizli de?er g?sterilsin mi?** onay?n? a?ar. **Ge?ici g?ster** onay?ndan sonra de?er g?r?n?r olur ve kay?t i?in bir `VIEW` denetim olay? yaz?l?r. ??iniz bitince **Gizli de?eri gizle** se?ene?ini kullan?n.
4. **Gizli de?eri kopyala** not g?vdesini, g?vde yoksa iste?e ba?l? gizli alan? panoya al?r ve ba?ar?l? ak??ta bir `COPY` denetim olay? yazar.

VaultPilot panodaki de?eri 30 saniye sonra temizlemeyi dener; bunu yaln?z pano h?l? ayn? de?eri i?eriyorsa ve taray?c? pano okuma/yazma izni veriyorsa yapabilir. Bu en iyi ?aba korumas?d?r: i?letim sistemi pano ge?mi?ini, bulut e?itlemesini veya de?erin yap??t?r?ld??? ba?ka bir uygulamay? temizleyemez. Hassas bir notu kopyalad?ktan sonra i?i geciktirmeyin ve panonun temizlendi?ini varsaymay?n.

### Notu g?ncelleme veya kald?rma

**Kayd? d?zenle** ile i?eri?i ve s?n?fland?rmay? g?ncelleyin. Bir not art?k gerekli de?ilse silmeden ?nce ba?ka bir ekip taraf?ndan kullan?lmad???n? do?rulay?n. Silme onay? g?r?nene kadar i?lem uygulanmaz; onaydan ?nce vazge?mek g?venli durma noktas?d?r.

## Ekran Durumlar?

| Durum | Operat?r cevab? |
| --- | --- |
| Kay?t yok | Filtre uygulanmad???ndan emin olun. Ger?ekten bo?sa **Yeni kay?t** ile ilk notu olu?turun. |
| E?le?me yok | Etkin ak?ll? filtreleri ve arama metnini temizleyin; bu durum kay?tlar?n silindi?i anlam?na gelmez. |
| Salt okunur | Notlar? okuyabilirsiniz ancak olu?turma, d?zenleme ve silme kapal?d?r. Lisans ve kasa rol?n? kontrol edin. |
| Yetki yetersiz | Notun bulundu?u kasaya eri?im isteyin; ba?ka bir kasada kopya olu?turarak sahiplik s?n?r?n? a?may?n. |
| Kaydetme hatas? | Formu kapatmadan ?nce ba?l?k, i?erik ve zorunlu alanlar? kontrol edin. Gizli metni hata kayd?na eklemeyin. |
| Y?kleniyor | Liste tamamlanana kadar toplu i?lem ba?latmay?n; yenileme sonras?nda se?iminizi yeniden do?rulay?n. |

## ??lemden ?nce

- Metnin parola, API anahtar?, sertifika veya dosya olarak ayr? bir kay?t t?r?nde tutulmas? gerekip gerekmedi?ine karar verin.
- Do?ru kasay?, kay?t sahibini ve saklama amac?n? do?rulay?n.
- Ba?l?k, kategori ve etiketlerin i?eri?i a?madan kayd? tan?mlayabildi?inden; fakat m??teri veya sistem s?rr? a??klamad???ndan emin olun.
- Toplu i?lemde g?r?n?r kay?t say?s? ile se?ili kay?t say?s?n? kar??la?t?r?n.

## G?venli Kan?t

- **Payla??labilir:** ekran?n ad?, yakla??k olay zaman?, kay?t t?r?, maskelenmi? kategori veya etiket yap?s? ve g?r?nen hata kodu.
- **Gizli kalmal?:** not ba?l???, not i?eri?i, gizli alan, i? sistem ad?, kurtarma ayr?nt?lar?, kullan?c? veya m??teri bilgisi ve panoya kopyalanan metin.

Bir sorunu anlatmak i?in ger?ek not i?eri?i gerekmez. Hata yaln?z belirli i?erikle olu?uyorsa sentetik bir notla yeniden ?retin. Ger?ek i?eri?in incelenmesi zorunluysa herkese a??k bir issue yerine ?zel destek kanal?n? kullan?n.

## ?lgili

- [G?venlik ve g?ven modeli](security-and-trust-model.md)
- [Destek kan?t paketi](support-evidence-pack.md)
- [Herkese a??k issue'larda maskeleme](../../kb/tr/public-issue-redaction.md)
