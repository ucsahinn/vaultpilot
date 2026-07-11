# API Anahtarlar? Ekran?

?st ?ubuktaki `?`, API Anahtarlar? ?al??ma alan? a??kken bu ba?lama ?zel rehberi a?ar. Bu ekran; servis anahtar?, eri?im belirteci ve benzeri makineden makineye gizli de?erleri aktif kasada bulmak, incelemek ve yetkiniz varsa g?ncellemek i?indir. VaultPilot?taki bir kayd? ?iptal? durumuna almak, sa?lay?c?daki ger?ek anahtar? iptal etmez.

## Eri?im, Kasa Rol? ve Lisans

- Sahip, Y?netici ve Kullan?c? sistem rolleri, kendilerine okunabilir kasa eri?imi verildiyse API anahtar? ?al??ma alan?n? kullanabilir. Denet?i gizli kay?t ?al??ma alan?na giremez.
- Kay?tlar?n ??z?lebilmesi i?in aktif kasan?n kilidi a??k ve kasa anahtar?n?n taray?c? oturumunda kullan?labilir olmas? gerekir.
- Listeleme, g?sterme ve kopyalama okunabilir kasa eri?imi ister. Olu?turma, kopya ?retme, d?zenleme, silme ve yazan toplu i?lemler i?in aktif kasada **Editor** veya **Manager** rol? ve salt okunur olmayan lisans gerekir.
- Sistem rol? tek ba??na kasa yetkisi vermez. ??lemden ?nce do?ru aktif kasay? ve bu kasadaki rol?n?z? do?rulay?n.

## Burada Ne Yap?l?r

- Ba?l?k, istemci/sahip/servis hesab?, sa?lay?c? konsol URL?si, API anahtar? veya token de?eri ve kapsam/rotasyon notu i?eren ?ifreli kay?t olu?turulur.
- Arama, h?zl? filtreler ve ak?ll? filtrelerle g?r?n?r kay?t k?mesi daralt?l?r.
- Gizli de?er kopyalan?r veya onaydan sonra ekranda g?sterilir; ge?erli HTTP/HTTPS adresi varsa sa?lay?c? konsolu a??l?r.
- Kay?t kopyalan?r, d?zenlenir, silinir, payla??m ak???na haz?rlan?r ya da kontroll? toplu i?leme al?n?r.

## Arama, Filtreler ve G?r?n?m

Metin aramas?; ba?l?k, istemci/sahip alan?, URL, sunucu ad?, etki alan?, kategori, kaynak, risk ve etiketlerde ?al???r. Gizli anahtar de?erinin i?inde arama yap?lmaz.

H?zl? filtreler veriye g?re **T?m?**, **Kritik**, **Uyar?**, **??e aktar?ld?** ve en s?k ?r?n, kategori veya etiket se?eneklerinden en fazla yedisini g?sterir. **Ak?ll? filtre ekle** ile birden fazla ko?ul se?ildi?inde kay?t b?t?n ko?ullarla e?le?melidir. **T?m?** t?r, risk ve ak?ll? filtreleri varsay?lana d?nd?r?r; arama metnini ayr?ca temizlemeniz gerekebilir.

**Kart** g?r?n?m? daha geni? kay?t kartlar?, **Tablo** g?r?n?m? s?k? kolon d?zeni kullan?r. **Yenile** kay?t sorgusunu tekrar ?al??t?r?r. Kay?tlar son g?ncellenen ?nce gelecek ?ekilde al?n?r.

### Se?im kapsam?

- Bir filtre kayd? gizlese bile daha ?nce i?aretlenen kay?t bellekte se?ili kalabilir.
- **T?m?n? se?**, o anda g?r?n?r kay?tlar? yeni se?im yapar. G?r?n?rlerin tamam? se?iliyse **Se?imi temizle** b?t?n se?imi bo?alt?r.
- ?stteki say? g?r?n?r se?imi sayarken baz? toplu i?lemler bellekte kalan g?r?nmez kimlikleri de kullan?r. Filtre de?i?tirdikten sonra se?imi a??k?a temizleyip yeniden kurun.

## Kay?t Sat?r? ??lemleri

Birincil i?lemler **Gizli de?eri kopyala** ve ge?erli bir HTTP/HTTPS adresi varsa **Konsolu a?**t?r. **Di?er i?lemler** men?s?nde ?unlar bulunur:

- **Gizli de?eri g?ster / gizle**
- **URL?yi kopyala**
- **Kopya olu?tur**
- **Kayd? d?zenle**
- **Kayd? sil**

**Konsolu a?** yaln?z do?rulanabilen HTTP/HTTPS adresini yeni ba?lamda a?ar ve `VIEW` olay? yazmay? dener. Sa?lay?c?ya giri? yapmaz, anahtar? do?rulamaz ve ger?ek kapsam? sorgulamaz.

## G?sterme, Kopyalama ve Denetim

**Gizli de?eri g?ster** ?nce hassas de?er uyar?s? ister. De?er kartta g?r?n?r ve ard?ndan `VIEW` olay? yaz?lmaya ?al???l?r. G?sterim k?sa bir saya?la otomatik kapanmaz; siz gizleyene, ba?ka kay?t g?sterene, kasay? kilitleyene veya 15 dakikal?k hareketsizlik kilidi ?al??ana kadar a??k kalabilir.

Anahtar veya URL panoya yaz?ld?ktan sonra `COPY` olay? olu?turulmaya ?al???l?r. Pano temizleme zamanlay?c?s? 30 saniye sonra, pano h?l? ayn? de?eri i?eriyorsa bo? de?er yazmay? dener. Taray?c? kapanmas?, pano izni, i?letim sistemi veya pano y?neticisi temizli?i engelleyebilir. Zamanlay?c?y? eri?imin geri al?nd??? garantisi saymay?n.

Pano yaz?m? ve ekranda g?sterme, denetim iste?inden ?nce ger?ekle?ir. Denetim yaz?lamasa bile de?er ekranda veya panoda bulunabilir; eksik olay, de?erin a??lmad???n? kan?tlamaz.

## Yeni Kay?t ve D?zenleme

**Yeni API anahtar?** d?zenleyicisi zorunlu ba?l?k ile gizli de?er; iste?e ba?l? istemci/sahip/servis hesab?, konsol URL?si ve kapsam/rotasyon notu sunar. Taslak de?er d?zenleme s?ras?nda taray?c?da d?z metin olarak bulunur. Ekran payla??m?n? ve omuz ?zerinden g?r?nt?lemeyi y?netin.

Kaydetme s?ras?nda veri aktif kasa anahtar?yla taray?c?da ?ifrelenir. Yeni kay?t `CREATE`, g?ncelleme `EDIT` olay? ?retir. **D?zenle** yaln?z VaultPilot kayd?n? de?i?tirir; sa?lay?c?daki token de?eri, kapsam?, s?resi veya istemci ayarlar? de?i?mez.

### De?er ?retici ve sona erme meta verisi

D?zenleyicideki ?retici taray?c?da ?al???r; varsay?lan uzunluk 24, aral?k 12?64 karakterdir. K???k harfler her zaman havuzdad?r; b?y?k harf, rakam ve sembol se?enekleri havuzu geni?letir. ?retilen de?er yaln?z form alan?n? doldurur. Sa?lay?c?da anahtar ?retmez, do?rulamaz, d?nd?rmez veya iptal etmez; ger?ek anahtar? ?nce sa?lay?c?n?n onayl? ak???nda olu?turun.

Manuel d?zenleyicide ayr? bir sona erme tarihi alan? yoktur. `API Keys` Excel sayfas?yla i?e aktar?lan `expiresAt`, ?ifreli kay?t meta verisi olur; otomatik rotasyon/iptal planlamaz ve sa?lay?c?daki ger?ek sona erme durumunu kan?tlamaz. ??e aktarma kayna?? `imported`, durumu `ACTIVE` yapar; risk yaln?z i?e aktarma an?nda tarih ge?mi?se `expired`, aksi halde `unknown` olarak atan?r. Bu s?n?fland?rmay? kendili?inden ilerleyen canl? s?re takibi saymay?n.

Bir anahtar rotasyonunda g?venli s?ra ?udur:

1. Sa?lay?c?da yeni anahtar? en az gerekli kapsamla ?retin.
2. T?keten sistemi kontroll? bak?m penceresinde yeni de?ere ge?irin ve i?levi do?rulay?n.
3. Eski anahtar? sa?lay?c?da iptal edin.
4. VaultPilot kayd?n? ve operasyon notunu g?ncelleyin; denetim izini uzla?t?r?n.

VaultPilot sa?lay?c?ya ba?lan?p bu ad?mlar? otomatik uygulamaz.

## Kopya, Silme ve Toplu ??lemler

**Kopya olu?tur** ayn? kasada yeni bir ?ifreli kay?t ?retir; sa?lay?c?da yeni anahtar olu?turmaz. **Kayd? sil** ikinci onaydan sonra VaultPilot kayd?n? geri al?namaz bi?imde kald?r?r; sa?lay?c?daki anahtar ?al??maya devam edebilir.

Toplu men?; Excel ?ablonu/i?e aktarma, d?z metin d??a aktarma, kategori ve etiket atama, ar?ivleme, pasifle?tirme/iptal, g?venlik kontrol?, denetim raporu, payla??m, not ekleme, ilk se?iliyi d?zenleme ve onayl? silme i?lemlerini i?erir.

- **Pasifle?tir / iptal et**, se?ili API anahtarlar?n?n ?ifreli meta verisini `REVOKED`, kaynak alan?n? `revoked` ve riski `warning` yapar. Sa?lay?c?ya iptal iste?i g?ndermez.
- **Se?ilenleri d??a aktar**, ??z?lm?? tam kay?tlar? ve anahtar de?erlerini d?z metin JSON dosyas?na yazar. Dosya ayr? bir hassas veri kopyas?d?r; indirme sonras? otomatik silinmez.
- **Denetim raporuna ekle**, gizli de?er yerine kay?t meta verisini CSV?ye yazar.
- Toplu g?ncelleme ve silme kay?tlar? s?rayla i?ler. Ortadaki hata ?nceki ba?ar?lar? geri almaz; yenileyip ger?ek kapsam? ve denetim olaylar?n? uzla?t?rmadan tekrar ?al??t?rmay?n.
- **Toplu payla?**, se?imi Payla??m ekran?n?n y?ntem ad?m?na ta??r; paket hen?z g?nderilmez ve se?im yetki kazand?rmaz. Dahili al?c? paketi i?in Sahip/Y?netici sistem rol?, aktif kasada **Manager** ve yaz?labilir lisans; harici paket i?in aktif kasada **Manager** ve yaz?labilir lisans gerekir.
- ?G?venlik kontrol?? HIBP parola denetim mekanizmas?n? gizli de?ere uygulayabilir; bir API anahtar?n?n sa?lay?c?da ge?erli, do?ru kapsaml? veya s?zmam?? oldu?unu kan?tlamaz.

## Ekran Durumlar?

| Durum | Operat?r cevab? |
| --- | --- |
| Kay?tlar y?kleniyor | ?skelet sat?rlar? kaybolana kadar bekleyin; gerekirse oturumu ve aktif kasay? do?rulay?p **Yenile** kullan?n. |
| Kay?t yok | Do?ru kasa ve kilit durumunu do?rulay?n; yazma yetkiniz varsa **Yeni API anahtar?** ile ba?lay?n. |
| E?le?en kay?t yok | Aramay?, h?zl? filtreyi ve ak?ll? filtre ?iplerini ayr? ayr? temizleyin. |
| Salt okunur | G?sterme ve kopyalama m?mk?n olabilir; kay?t de?i?tiren i?lemler kapal?d?r. |
| `REVOKED` | Yaln?z VaultPilot meta verisidir. Sa?lay?c? konsolunda ger?ek iptal durumunu ayr?ca do?rulay?n. |
| Pano veya denetim hatas? | De?er zaten a??lm?? olabilir. Panoyu elle temizleyin, g?sterimi kapat?n ve olay? ayr? kanaldan uzla?t?r?n. |
| Toplu i?lem yar?m kald? | K?rlemesine tekrar etmeyin; gizli se?imi, de?i?en kay?tlar? ve sa?lay?c?daki ger?ek durumu kar??la?t?r?n. |

## ??lemden ?nce

- Anahtar?n sahibini, t?keten uygulamalar?, ortam?n?, kapsam?n? ve bak?m penceresini belirleyin.
- Aktif kasay? ve se?ili kay?tlar? do?rulay?n; filtre de?i?tiyse se?imi temizleyip yeniden kurun.
- G?sterme, kopyalama veya d??a aktarma ?ncesinde ekran payla??m?n? ve pano y?neticilerini kapat?n.
- Sa?lay?c?da iptal/rotasyon yetkiniz ve geri d?n?? plan?n?z olmadan VaultPilot meta verisini ?iptal edildi? diye de?i?tirmeyin.
- Payla??mda al?c?y?, s?reyi, kullan?m s?n?r?n? ve teslim kanal?n? Payla??m ekran?nda yeniden kontrol edin.

## G?venli Kan?t

- Payla??labilir: ekran ad?, geni? zaman aral???, genel sa?lay?c? t?r?, kay?t say?s?, redakte edilmi? hata s?n?f?, genel rotasyon durumu ve yazma yetkisinin bulunup bulunmad???.
- Gizli kalmal?: API anahtar?/token de?eri, tam istemci kimli?i, ba?l?k ile URL e?le?mesi, kapsam ayr?nt?s?, kasa ad?/kimli?i, tam zaman damgas?, se?ili kay?tlar, pano i?eri?i, d?z metin d??a aktar?m ve de?er g?steren ekran g?r?nt?s?.
- Bir de?er genel kanala girdiyse panoyu temizlemek yeterli de?ildir. Sa?lay?c?da anahtar? iptal edin, yeni anahtar ?retin, t?keticileri g?ncelleyin ve ancak sonra kasa kayd?n? uzla?t?r?n.

## Ne Zaman Durmal?

Aktif kasa, anahtar sahibi veya t?keten sistem belirsizse; sa?lay?c?da ger?ek rotasyon/iptal yetkisi yoksa; gizli toplu se?imden ??pheleniyorsan?z; pano ya da ekran kayd? kontrol?n?z d???nda ise; denetim izi i?lemle ?eli?iyorsa; toplu i?lem yar?m kald?ysa veya yaln?z VaultPilot kayd?n? de?i?tirerek d?? sistemde rotasyon tamamland? san?lacaksa durun. Son g?venli ad?m? ?zel kanalda uzla?t?rmadan i?lemi tekrarlamay?n.

## Operat?r Notlar?

VaultPilot API anahtar? kayd?n? diskte ?ifreli saklar; kilidi a??k taray?c? g?sterme, d?zenleme, kopyalama ve d??a aktarma i?in de?eri ge?ici olarak d?z metne ?evirir. Ekran, pano ve indirilen JSON ayr? g?ven s?n?rlar?d?r. `REVOKED`, `ARCHIVED` veya silinmi? bir VaultPilot kayd?n? sa?lay?c?daki anahtar?n durumuna ili?kin kan?t olarak raporlamay?n.

## ?lgili

- [G?venlik ve g?ven modeli](security-and-trust-model.md)
- [Payla??m ekran?](screen-sharing.md)
- [Denetim Ge?mi?i ekran?](screen-audit-log.md)
- [Public API referans?](public-api-reference.md)
- [Entegrasyon API client'lar?](api-clients.md)
- [API client eri?imi KB](../../kb/tr/api-client-401.md)
- [G?venli destek kan?t?](support-evidence-pack.md)
