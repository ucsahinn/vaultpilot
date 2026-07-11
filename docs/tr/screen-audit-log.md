# Denetim Kayd? Ekran?

?st ?ubuktaki `?` simgesi Denetim Kayd? ekran?na ait bu rehberi a?ar. Bu ekran yaln?z kronolojik bir liste de?ildir; i?lemi yapan ki?i, etkilenen hedef, rol, zaman, i?lem ayr?nt?lar? ve b?t?nl?k ?zetlerini ayn? ba?lamda incelemenizi sa?lar.

Aray?zdeki **Operasyon > Denetim kayd?** ba?lant?s? yaln?z Sahip, Y?netici ve Denet?i rollerine g?sterilir. Buna kar??l?k denetim listesini d?nd?ren GET API'si, normal Kullan?c? rol? dahil t?m do?rulanm?? oturumlar? kabul eder. Men? g?r?n?rl??? ile API yetkisini ayn? ?ey saymay?n; her istek i?in sunucunun uygulad??? rol denetimi belirleyicidir. Ekran mevcut olaylar? de?i?tirmez. CSV ve Excel d??a aktar?mlar? yaln?z o anda filtrelenmi? ham olaylar? kapsar.

## Burada Ne Yap?l?r

- ?stteki kategori d??meleri, **??lem t?r?** se?imi ve **Denetimde ara** alan?yla g?r?lt?y? azalt?n.
- Sonu? ?zetindeki ham olay say?s?n?, se?ili kategoriyi ve i?lem t?r?n? d??a aktarmadan ?nce kontrol edin. Arama metni bu ?zette g?sterilmez.
- Bir sat?r? a?arak akt?r, hedef, rol, zaman, i?lem ayr?nt?lar?, bu olay?n ?zeti ve ?nceki olay?n ?zetini birlikte okuyun.
- **Filtreleri temizle** ile ba?lang?? g?r?n?m?ne d?nebilir; CSV veya Excel ile yaln?z g?r?nen sonu?lar? d??a aktarabilirsiniz.
- Bir sat?rdaki `Nx` i?areti, ayn? dakika i?inde ayn? i?lem?akt?r?hedef birle?imindeki olaylar?n aray?zde gruplanm?? oldu?unu g?sterir.

## Ekran? Nas?l Okumal?s?n?z

Kategori d??meleri olaylar? anlaml? gruplara ay?r?r ve her d??medeki say? o gruptaki ham olay miktar?n? g?sterir. **??lem t?r?** belirli bir eylemi, arama alan? ise i?lem ad?, akt?r, hedef, anlat?m, ayr?nt? metni, zaman, olay ?zeti ve hedef kimli?i i?inde e?le?me bulmaya yard?m eder. Ayr? akt?r, hedef, risk veya zaman filtresi yoktur.

Sonu? ?zeti ham olay say?s?n?, se?ili kategoriyi ve i?lem t?r?n? g?sterir; arama metnini g?stermez. Ayn? i?lem, akt?r ve hedef i?in ayn? dakika i?inde olu?an olaylar ekranda tek temsilci sat?r alt?nda `Nx` bi?iminde gruplan?r. Bu sat?ra t?klamak grubun t?m ?yelerini de?il, temsilci olay? ayr?nt? panelinde a?ar. Kategori saya?lar?, sonu? ?zeti ve d??a aktar?mlar ise gruplanmam?? ham olaylar? sayar.

Ayr?nt? panelinde akt?r, hedef, rol, zaman, i?lem ayr?nt?lar?, bu olay?n ?zeti ve ?nceki olay?n ?zeti g?r?n?r. Bunlar operat?r?n elle kar??la?t?raca?? kan?t alanlar?d?r; ekran ?tam?, ?k?smi? veya ?ge?ersiz zincir? sonucu hesaplamaz. ?zellikle kritik de?i?ikliklerde kom?u olaylar? ayr? ayr? a?arak s?ray? ve ?zet ba?lant?s?n? do?rulay?n.

## ?nceleme ?? Ak??lar?

### Belirli bir de?i?ikli?i bulma

1. Olay?n yakla??k zaman?n? ve olas? akt?r ya da hedefi belirleyin.
2. ?nce kategori, sonra **??lem t?r?** se?in.
3. **Denetimde ara** alan?n? son daraltma ad?m? olarak kullan?n.
4. Sat?r? a??p akt?r, hedef, rol ve zaman?n beklenen i?lemle ?rt??t???n? do?rulay?n.

Beklenen sonu?, tek bir olay? yak?n?ndaki olaylardan koparmadan tan?mlamakt?r. Sonu? yoksa hemen ?kay?t tutulmam??? sonucuna varmay?n; **Filtreleri temizle** kullan?n, saat dilimini ve arama yaz?m?n? kontrol edip yeniden deneyin.

### Olay ?zetlerini elle kar??la?t?rma

1. ?lgili olay?n ayr?nt?s?n? a??n.
2. Bu olay?n ?zeti ile ?nceki olay?n ?zetini kaydedin.
3. Sat?r `Nx` ile gruplanm??sa ayr?nt? panelinin yaln?z temsilci olay? g?sterdi?ini not edin.
4. Ayn? zaman aral???ndaki ?nceki ve sonraki ham olaylar? arama ve d??a aktarma yard?m?yla kar??la?t?r?n.

?zetlerin bulunmas?, zincirin uygulama taraf?ndan do?ruland??? anlam?na gelmez. ?nceki ?zetin bo?, beklenmedik veya kom?u olayla uyu?maz g?r?nmesi halinde ham kay?tlar? de?i?tirmeyin; dar zaman aral??? ve redakte edilmi? ba?lamla ?zel destek ak???na ge?in.

### Dar kapsaml? kan?t d??a aktarma

1. Kategori, i?lem t?r? ve arama metnini olaya ili?kin en k???k kapsama getirin.
2. Ham olay say?s?n?, kategori ve i?lem t?r?n? not edin; arama metnini ayr?ca kaydedin.
3. Hangi alanlara ihtiyac?n?z oldu?una g?re CSV veya Excel uyumlu tabloyu se?in.
4. ?ndirilen dosyan?n yan?nda filtreleri ayr? bir inceleme notunda saklay?n; dosya kendi filtre kapsam?n? i?ermez.
5. Orijinali ?zel ve de?i?mez tutun; payla??lacak kopyada kullan?c?, nesne, IP ve m??teri ba?lam?n? redakte edin.

CSV; `created_at`, `action`, `actor`, `target`, `summary`, `details`, `target_id`, `integrity_hash` ve `previous_hash` alanlar?n? i?erir. **Excel** d??mesi ger?ek `.xlsx` de?il, Excel uyumlu HTML tablo ta??yan `.xls` dosyas? ?retir; Created, Action, Actor, Target, Summary, Details ve Integrity hash s?tunlar?n? i?erir, ancak `target_id` ile `previous_hash` alanlar?n? i?ermez.

G?r?nen ham olay say?s? s?f?rsa iki d??a aktarma d??mesi de pasiftir; bo? dosya ?retilmez. Her d??a aktarma, dosyay? indirdikten sonra sunucuya bir `EXPORT` denetim olay? yazma iste?i g?nderir ve listeyi yeniler. Bu olay yaln?z sunucu yazma iste?ini kabul ederse kaydedilir. ?rne?in Denet?i dosyay? indirebilir, ancak Denet?i rol? denetim olay? olu?turamad??? i?in `EXPORT` olay? listeye eklenmeyebilir. Yeni olay kaydedilse bile kendisinden ?nce haz?rlanm?? dosyan?n i?inde yer almaz.

### Aktif olay s?ras?nda g?venli duru?

Yetkisiz eri?im ??phesi, a??klanamayan rol de?i?ikli?i veya olay ?zetlerinde beklenmeyen ba?lant? varsa kritik olmayan y?netim i?lemlerini durdurun. ?lgili zaman aral???n?, ger?ek filtre kapsam?n? ve olay ?zetlerini koruyup olay m?dahale sorumlusuna aktar?n. ?nceleme s?rerken kay?t temizli?i veya saklama s?resi de?i?ikli?i yapmay?n.

## Ekran Durumlar? ve Operasyonel Ko?ullar

| Durum | Operat?r cevab? |
| --- | --- |
| Y?kleniyor | Filtreleri de?i?tirmeden iskelet sat?rlar?n tamamlanmas?n? bekleyin. |
| Filtre sonucu bo? | Filtreleri temizleyin; zaman ve arama ifadesini yeniden do?rulay?n. |
| Gruplanm?? `Nx` sat?r? | Sat?r?n temsilci olay? a?t???n?; saya? ve d??a aktar?m?n ham olaylar? kulland???n? unutmay?n. |
| D??a aktarma kapal? | Filtrelenmi? ham olay say?s? s?f?rd?r; filtreleri g?zden ge?irin. |
| D??a aktarma tamamland? | Dosyan?n kapsam notunu saklay?n; `EXPORT` olay? yaln?z sunucu yazma iste?ini kabul ederse g?r?n?r. |

## ??lemden ?nce

- D??a aktarma ?ncesi kategori, i?lem t?r? ve arama metnini ayarlay?n; ayr? akt?r, hedef veya zaman filtresi olmad???n? unutmay?n.
- Olay ?zetlerini kar??la?t?r?rken yak?n zamanl? ham olaylar? ve `Nx` gruplanmas?n? hesaba kat?n.
- ?zet ba?lant?s? belirsizse ve aktif bir olay incelemesi s?r?yorsa kritik olmayan de?i?iklikleri durdurun.
- D??a aktarma dosyas?n?n g?venli saklama konumunu ve kimlerle payla??laca??n? ?nceden belirleyin.
- Ham olay listesini etkileyebilecek temizlik veya saklama i?lemlerini kan?t sorumlusuyla uzla?t?r?n.
- Arama metnini, saat dilimi varsay?m?n?, kategori ve i?lem t?r?n? dosyadan ayr? kapsam notuna yaz?n.

## G?venli Kan?t

- Payla??labilir: olay kategorisi, dar zaman aral???, akt?r rol?n?n maskelenmi? bi?imi, olay ?zetinin k?sa b?l?m? ve ger?ek filtre kapsam?.
- Gizli kalmal?: kullan?c? ad?, nesne kimli?i, ham denetim d??a aktar?m?, dahili IP ve m??teri ba?lam? i?eren olay materyali.
- ?nceki olay ?zeti eksik veya beklenmedikse kan?t? koruyun; uygulaman?n g?r?n?r bir zincir sa?l?k sonucu ?retmedi?ini a??k?a belirtin.
- Payla??labilir kopyada kategori, i?lem t?r?, arama metni ve ham olay say?s? kals?n; dosyan?n kendi ba??na bu kapsam? anlatmad???n? unutmay?n.
- Ham CSV/Excel dosyas?n?, ayr?nt? panelindeki i?lem ayr?nt?lar?n? veya m??teri ba?lam?n? herkese a??k bir kanala y?klemeyin.

## Ne Zaman Durmal? ve Destek ?stemelisiniz

Olay ?zetleri kom?u ham olaylarla uzla?t?r?lam?yorsa, ayr?nt? akt?r veya hedefle e?le?miyorsa, d??a aktarma beklenen olaylar? vermiyorsa ya da aktif bir g?venlik olay? s?r?yorsa yeni y?netim de?i?iklikleri yapmay?n. Kategori, i?lem t?r?, arama metni, dar zaman aral???, akt?r rol?n?n maskelenmi? bi?imi ve olay ?zetleriyle ?zel destek kayd? a??n; ham m??teri verisini payla?may?n.

## Operat?r Notlar?

Denetim kan?t? kullan?c? ad?, dahili nesne kimli?i ve i?lem zaman?n? g?sterebilir. Herkese a??k kay?tlarda bunlar? redakte edin; ger?ek olay materyali i?in ?zel destek kullan?n.

## ?lgili

- [Denetim ve g?venlik duru?u](audit-and-security-posture.md)
- [Denetim zinciri inceleme KB](../../kb/tr/audit-chain-partial.md)
- [Destek kan?t paketi](support-evidence-pack.md)
