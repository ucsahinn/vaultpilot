# Parolalar Ekran?

?st ?ubuktaki `?`, Parolalar ekran? a??kken bu ba?lama ?zel rehberi a?ar. Bu ekran, aktif kasadaki parola kay?tlar?n? bulmak, incelemek ve yetkiniz varsa d?zenlemek i?indir. Buradaki ?retme, kopyalama ve ?otomatik doldurma paketi? i?lemleri hedef sistem hesab?n? kendili?inden de?i?tirmez.

## Eri?im, Kasa Rol? ve Lisans

- Sahip, Y?netici ve Kullan?c? sistem rolleri, kendilerine okunabilir kasa eri?imi verildiyse parola ?al??ma alan?n? kullanabilir. Denet?i gizli kay?t ?al??ma alan?na giremez.
- Kay?tlar?n ??z?lebilmesi i?in aktif kasan?n kilidi a??k ve kasa anahtar?n?n taray?c? oturumunda kullan?labilir olmas? gerekir.
- G?r?nt?leme okunabilir kasa eri?imi ister. Olu?turma, kopya ?retme, d?zenleme, silme ve yazan toplu i?lemler i?in aktif kasada **Editor** veya **Manager** rol? ve salt okunur olmayan lisans gerekir.
- Salt okunur lisans listeleme, g?sterme, kopyalama ve yerel s?z?nt? kontrol?ne engel de?ildir; kasa verisini de?i?tiren i?lemler kapal?d?r.
- Sistem rol? tek ba??na kasa yetkisi vermez. Her i?lemden ?nce do?ru aktif kasay? ve o kasadaki rol?n?z? do?rulay?n.

## Burada Ne Yap?l?r

- Ba?l?k, kullan?c? ad?/e-posta, giri? URL'si, parola ve not i?eren kay?tlar olu?turulur veya yeniden ?ifrelenerek g?ncellenir.
- Arama, h?zl? filtreler ve birle?tirilebilir ak?ll? filtrelerle g?r?n?r kay?t k?mesi daralt?l?r.
- Kart veya tablo g?r?n?m?nde parola, kullan?c? ad? ve URL ayr? i?lemlerle kopyalan?r.
- HIBP Pwned Passwords ?zerinden iste?e ba?l? s?z?nt? kontrol? ?al??t?r?l?r.
- Se?ili kay?tlar payla??m ekran?na veya toplu d?zenleme, rapor, d??a aktarma ve silme i?lemlerine haz?rlan?r.

## Arama, Filtreler ve G?r?n?m

Metin aramas?; ba?l?k, kullan?c? ad?, URL, sunucu ad?, etki alan?, sahip, kategori, kaynak, risk ve etiket alanlar?nda ?al???r. Parola de?erinin i?inde arama yap?lmaz.

H?zl? filtre band? veriye g?re **T?m?**, **S?z?nt? g?r?ld?**, **Kontrol bekliyor**, **Uyar?** ve en s?k ?r?n/servis ya da kategori se?eneklerinden en fazla yedisini g?sterir. **Ak?ll? filtre ekle** men?s?nde kullan?c? ad? veya sahip, ?r?n/servis, kategori, etiket ve s?z?nt? durumu se?enekleri bulunabilir. Birden fazla ak?ll? filtre birlikte se?ildi?inde kay?t b?t?n ko?ullarla e?le?melidir.

Bir filtre ?ipine basmak yaln?z o filtreyi, **Temizle** b?t?n ak?ll? filtreleri kald?r?r. **T?m?** h?zl? filtresi t?r, risk ve ak?ll? filtre durumunu varsay?lana d?nd?r?r; arama metnini ayr?ca temizlemeniz gerekebilir.

**Kart** daha geni? kay?t kartlar?, **Tablo** kolon ba?l?kl? s?k? yerle?im kullan?r. **Yenile** kay?t sorgusunu tekrar ?al??t?r?r. Kay?tlar son g?ncellenen ?nce gelecek ?ekilde al?n?r.

### Se?im kapsam?

- Tek tek i?aretlenen kay?tlar filtre de?i?ti?inde g?r?n?m d???nda kalabilir ama se?ili kalabilir.
- **T?m?n? se?**, o anda g?r?n?r kay?tlar? se?im olarak yazar; ?nceki gizli se?imi korumaz. G?r?n?rlerin t?m? se?iliyse **Se?imi temizle** b?t?n se?imi bo?alt?r.
- ?stteki se?ili say?s? yaln?z g?r?n?r se?imi sayar; baz? toplu i?lemler bellekte se?ili kalan g?r?nmez kay?tlar? da kullan?r. Filtre de?i?tirdikten sonra se?imi a??k?a temizleyip yeniden kurun.

## Kay?t Sat?r? ??lemleri

Parola sat?r?n?n birincil i?lemleri **Gizli de?eri kopyala** ve ge?erli HTTP/HTTPS adresi varsa **Siteyi a?**t?r. Di?er i?lemler men?s?nde ?unlar bulunur:

- **Otomatik doldurma paketi haz?rla**
- **S?z?nt? kontrol?**
- **Kullan?c? ad?n? kopyala**
- **Gizli de?eri g?ster / gizle**
- **URL'yi kopyala**
- **Kopya olu?tur**, **Kayd? d?zenle** ve **Kayd? sil**

**Siteyi a?** yaln?z do?rulanabilen HTTP/HTTPS adresini a?ar ve `VIEW` olay? yazmay? dener. Giri? yapmaz ve sayfadaki alanlar? doldurmaz.

## G?sterme, Kopyalama ve Denetim

**Gizli de?eri g?ster** ?nce uyar? onay? ister. De?er ard?ndan taray?c?daki kartta g?r?n?r ve `VIEW` olay? yaz?l?r. G?sterim sabit k?sa bir saya?la kapanmaz; d??meyle gizleyene, ba?ka bir kayd? g?sterene, kasay? kilitleyene veya 15 dakikal?k hareketsizlik kilidi devreye girene kadar a??k kalabilir.

Parola, kullan?c? ad?, URL ve doldurma paketi i?letim sistemi panosuna yaz?l?r; ard?ndan `COPY` olay? olu?turulur. Pano temizleme zamanlay?c?s? 30 saniyedir ve yaln?z pano h?l? ayn? de?eri i?eriyorsa bo? yazmay? dener. Taray?c?n?n kapanmas?, pano izni, i?letim sistemi veya pano y?neticisi bu temizli?i engelleyebilir; zamanlay?c? eri?imin geri al?nd???na dair garanti de?ildir.

Pano yaz?m? ve g?r?n?r k?lma, denetim iste?inden ?nce ger?ekle?ir. Denetim yaz?m? sonradan ba?ar?s?z olsa bile de?er ekranda veya panoda bulunabilir. Denetim olay?n?n olmamas? hassas de?erin hi? a??lmad???n? kan?tlamaz.

### ?Otomatik doldurma paketi? s?n?r?

Bu ekrandaki **Otomatik doldurma paketi haz?rla**, kullan?c? ad? ile parolay? sekmeyle ayr?lm?? tek metin olarak panoya kopyalar ve `COPY` olay? yazar. Kullan?c? bu metni hedef sayfan?n kullan?c? ad? alan?na yap??t?r?r. Bu i?lem taray?c? eklentisini uzaktan ?al??t?rmaz; alanlar? buldu?unu, doldurdu?unu veya giri?in ba?ar?l? oldu?unu garanti etmez. VaultPilot Browser Vault Extension'?n sayfa i?i doldurma ak??? ayr? bir g?ven s?n?r?d?r.

## HIBP S?z?nt? Kontrol?

Tek kay?t veya d?zenleyicideki **S?z?nt? kontrol?**, parolan?n SHA-1 ?zetini taray?c?da hesaplar. Yaln?z ?zetin ilk be? karakteri `api.pwnedpasswords.com/range` adresine g?nderilir; tam parola ve tam ?zet g?nderilmez. D?nen son ekler taray?c?da kar??la?t?r?l?r ve istek dolgu ba?l??? kullan?r.

Sonu? **S?z?nt? g?r?ld?** veya **Bulunmad?** olarak, g?r?lme say?s? ve kontrol zaman? ile g?sterilir. **Bulunmad?**, parolan?n g??l?, benzersiz veya g?venli oldu?unu kan?tlamaz. **S?z?nt? g?r?ld?** sonucunda ?nce ger?ek sistemde parolay? de?i?tirin, sonra kasa kayd?n? g?ncelleyin.

Tek kay?t kontrol? ?zel bir sunucu denetim olay? yazmaz. Toplu **G?venlik kontrol? ba?lat**, ba?ar?yla kontrol etti?i her kay?t i?in `VIEW` olay? yazmay? dener.

Sonu?lar parola olmadan; kay?t kimli?i, durum, g?r?lme say?s? ve zaman bilgisiyle bu taray?c? profilinin `localStorage` alan?nda tutulur. Ba?ka taray?c? veya temizlenmi? depolama farkl? sonu? k?mesi g?sterir. Kay?t parolas? de?i?tiyse eski sonu? g?ncel de?eri temsil etmeyebilir; karar vermeden ?nce yeniden kontrol edin.

## Yeni Kay?t ve D?zenleyici

**Yeni parola** d?zenleyicisi zorunlu ba?l?k ve parola; iste?e ba?l? kullan?c? ad?/e-posta, giri? URL'si ve not alanlar? sunar. Parola tasla?? d?zenleyicide d?z metin g?r?nen bir metin alan?ndad?r; ekran payla??m? ve omuz ?zerinden g?r?nt?leme riskini y?netin.

Kaydetme s?ras?nda kay?t aktif kasa anahtar?yla taray?c?da ?ifrelenir. Yeni kay?t `CREATE`, g?ncelleme `EDIT` olay? ?retir. **D?zenle** mevcut kayd? Yeni kay?t ekran?na ta??r; **Kaydet** hedef sistem hesab?n? de?il yaln?z ?ifreli kasa kayd?n? g?nceller.

### Parola ?retici

?retici varsay?lan olarak 24 karakter kullan?r. Aray?z 12-64 karakter aral??? ile b?y?k harf, rakam ve sembol se?enekleri sunar; k???k harf k?mesi her zaman etkindir. ?retim taray?c?da `crypto.getRandomValues` ile yap?l?r. Etkin s?n?flar olas? karakter havuzuna eklenir; her etkin s?n?ftan mutlaka bir karakter gelmesi garanti edilmez.

**K?sa**, **Haz?r** ve **G??l?** g?stergeleri yaln?z uzunlu?a bakar: 16 karakterden k?sa, 16-23 ve en az 24. Bunlar hedef sistem politikas?n?, benzersizli?i veya s?z?nt? durumunu do?rulamaz.

S?z?nt?l? karttaki **Yeni parola ?ret**, ge?erli ayarlarla yeni de?er olu?turup d?zenleyiciyi a?ar. Siz **Kaydet** demeden kasa kayd?na yaz?lmaz; hedef sistem parolas?n? hi?bir zaman otomatik de?i?tirmez.

## Kopya, Silme, Toplu ??lem ve Payla??m

**Kopya olu?tur**, ayn? kasada yeni kay?t ?retir ve ba?l??a ?kopyas?? ekler. D?? sistemde ikinci hesap olu?turmaz. Yazma yetkisi gerekir ve yeni kay?t `CREATE` olay? b?rak?r.

**Kayd? sil**, geri al?namaz i?lem i?in ikinci onay ister ve ba?ar?l? oldu?unda `DELETE` olay? ?retir. Yaln?z kasa kayd?n? kald?r?r; hedef sistem hesab?n? kapatmaz veya parolas?n? de?i?tirmez.

Toplu i?lemler men?s?nde Excel ?ablonu indirme/i?e aktarma, d??a aktarma, kategori veya etiket atama, ar?ivleme, pasifle?tirme, g?venlik kontrol?, denetim raporu, payla??m, not ekleme, ilk se?iliyi d?zenleme ve onayl? silme bulunur.

- Kategori, etiket, ar?iv, pasifle?tirme, not, d?zenleme, i?e aktarma ve silme yazma yetkisi ister.
- **Pasifle?tir / iptal et**, parola kayd?n?n ?ifreli meta verisini `DISABLED` yapar; hedef hesab? devre d??? b?rakmaz.
- **Se?ilenleri d??a aktar**, ??z?len tam kay?tlar? ve parolalar? d?z metin JSON dosyas?na yazar; tehlikeli i?lem onay? ister. Denetim olaylar? sonradan en iyi ?abayla yaz?l?r.
- **Denetim raporuna ekle**, parola de?erini de?il kay?t meta verilerini CSV dosyas?na yazar.
- Toplu d?zenleme ve silme kay?tlar? s?rayla i?ler; ortadaki hata ?nceki ba?ar?l? de?i?iklikleri geri almaz. Kasay? yenileyip kay?tlar? ve denetim izini uzla?t?r?n.
- **Toplu payla?**, se?ili kimlikleri Payla??m ekran?n?n y?ntem ad?m?na ta??r; hen?z paket g?ndermez. Ger?ek g?nderim Payla??m ?zelli?i, Manager rol?, yaz?labilir lisans ve se?ilen y?ntemin ayr? kurallar?na tabidir.

## Ekran Durumlar?

| Durum | Operat?r cevab? |
| --- | --- |
| Kay?tlar y?kleniyor | D?rt iskelet sat?r? kaybolana kadar bekleyin; gerekirse oturumu do?rulay?p **Yenile** kullan?n. |
| Kasada kay?t yok | Aktif kasay? ve kilit durumunu do?rulay?n; yazma yetkiniz varsa **Yeni parola** ile ba?lay?n. |
| E?le?en kay?t yok | Arama metnini, h?zl? filtreyi ve ak?ll? filtre ?iplerini ayr? ayr? temizleyin. |
| Liste bo? ama kay?t bekleniyor | Ayr? sorgu hata kart? yoktur. Oturumu, sunucu ba?lant?s?n?, aktif kasay? ve a? iste?ini kontrol edin. |
| Salt okunur | G?sterme ve kopyalama m?mk?n olabilir; olu?turma, kopya, d?zenleme, silme ve yazan toplu i?lemler kapal?d?r. |
| Pano hatas? | De?er panoya yaz?lm?? olabilir. Panoyu elle temizleyip `COPY` denetim izini kontrol edin. |
| G?sterim denetimi yaz?lamad? | De?er g?r?n?r kalabilir. Hemen gizleyin veya kasay? kilitleyin; denetimi ayr?ca uzla?t?r?n. |
| S?z?nt? kontrol? kullan?lam?yor | A?, taray?c? politikas? veya HIBP eri?imini kontrol edin; sonucu ?temiz? saymay?n. |
| S?z?nt? g?r?ld? | Hedef sistemde ger?ek parolay? de?i?tirin, sonra kasa kayd?n? g?ncelleyip yeniden kontrol edin. |
| Toplu i?lem yar?m kald? | K?rlemesine tekrarlamay?n; g?r?n?r/gizli se?imi, kasa durumunu ve denetim olaylar?n? kar??la?t?r?n. |

## ??lemden ?nce

- Do?ru aktif kasa, kay?t ba?l???, kullan?c? ad? ve URL'nin ayn? hesaba ait oldu?unu do?rulay?n.
- G?sterme, kopyalama veya d??a aktarma ?ncesinde ekran payla??m?n? ve pano y?neticilerini kapat?n.
- Filtre de?i?tirdiyseniz gizli kalm?? toplu se?imi temizleyip kapsam? yeniden kurun.
- Yeni parolay? ?nce hedef sistemde uygulama, ard?ndan kasa kayd?n? g?ncelleme s?ras?n? planlay?n.
- Payla??mda al?c?y?, s?reyi, kullan?m hakk?n? ve teslim s?n?r?n? Payla??m ekran?nda yeniden do?rulay?n.

## G?venli Kan?t

- Payla??labilir: ekran ad?, genel kart/tablo g?r?n?m?, geni? zaman aral???, kay?t say?s?, genel filtre t?r?, hesapla ili?kilendirilemeyen s?z?nt? durumu, genel hata s?n?f? ve rol/lisans?n yaz?labilir olup olmad???.
- Gizli kalmal?: parola, kullan?c? ad? ile URL e?le?mesi, kay?t ba?l???, not, kasa ad?/kimli?i, tam zaman damgas?, belirli hesapla ili?kili HIBP say?s?, se?ili kay?t k?mesi, pano i?eri?i, d?z metin JSON d??a aktar?m? ve de?er g?steren ekran g?r?nt?s?.
- Parola veya doldurma paketi genel kanala girdiyse panonun temizlenmesini beklemekle yetinmeyin; hedef sistemde parolay? de?i?tirin ve kasa kayd?n? ard?ndan g?ncelleyin.

## Ne Zaman Durmal?

Aktif kasa belirsizse, kay?t ile hedef URL e?le?miyorsa, gizli toplu se?imden ??pheleniyorsan?z, pano veya ekran kayd? kontrol?n?z d???nda ise, denetim olay? i?lemle ?eli?iyorsa, s?z?nt? sonucu eski olabilecekse, toplu i?lem yar?m kald?ysa ya da yeni parola hedef sistemde uygulanmadan yaln?z kasa kayd? de?i?tirilecekse durun. Kapsam? ve son g?venli ad?m? ?zel kanalda uzla?t?rmadan i?lemi tekrarlamay?n.

## Operat?r Notlar?

VaultPilot parola kayd?n? ?ifreli saklar; ancak kilidi a??k taray?c? oturumu g?sterme, d?zenleme, HIBP kontrol?, d??a aktarma ve pano i?lemleri i?in de?eri ge?ici olarak d?z metne ?evirir. Ekran, pano ve indirilen d?z metin dosya bu anda ayr? g?ven s?n?rlar?d?r. VaultPilot'taki ?pasif?, ?yeni parola? veya ?otomatik doldurma paketi? i?lemlerini hedef sistemde tamamlanm?? hesap de?i?ikli?i olarak raporlamay?n.

## ?lgili

- [G?venlik ve g?ven modeli](security-and-trust-model.md)
- [Payla??m ekran?](screen-sharing.md)
- [Taray?c? eklentisi ekran?](screen-browser-extension.md)
- [Denetim Ge?mi?i ekran?](screen-audit-log.md)
- [G?venli destek kan?t?](support-evidence-pack.md)
- [Operat?r ?al??ma k?lavuzu](operator-runbook.md)
