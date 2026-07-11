# Active Directory Kay?tlar? Ekran?

?st ?ubuktaki `?`, Active Directory kay?tlar? ekran?ndan bu k?lavuzu a?ar. Bu ekran aktif kasadaki ?ifreli `CREDENTIAL` kay?tlar?n? okur, her kay?tla saklanan dizin anl?k g?r?nt?s?n? g?sterir ve uygun kay?t, giri? ve DC Agent i?lemlerini sunar. Canl? LDAP taray?c?s?, PAM parola teslim kuyru?u veya genel dizin y?netim konsolu de?ildir.

## Eri?im, Aktif Kasa ve Lisans S?n?r?

Normal gezinme i?in **entegrasyon** lisans ?zelli?i, kilidi a??k aktif kasa ve kasan?n taray?c?da tutulan anahtar? gerekir. Sistem d?zeyinde Owner, Admin ve User kasa s?rr? ekranlar?n? kullanabilir; Auditor kullanamaz. Aktif kasada **Viewer** saklanan kayd? okuyabilir, g?sterebilir, kopyalayabilir, inceleyebilir ve ba?lant? paketi haz?rlayabilir. Silme veya desteklenen d?zenleme gibi kasa kayd? yazma i?lemleri i?in **Editor** ya da **Manager** rol? ile yaz?labilir lisans gerekir.

Dizin sa?lay?c?s? ve DC Agent i?lemlerinin s?n?r? daha dard?r. G?ncel sa?lay?c?/i?lem ?al??ma alan?n? yaln?z Owner y?kler; VaultPilot giri? eri?imini yaln?z Owner de?i?tirebilir ve dizin i?lemlerini yaln?z Owner kuyru?a alabilir. Dizin i?lemi ayr?ca yaz?labilir lisans, g?ncel olarak ??z?mlenen kullan?c? hedefi, **Ba?l?** ajan, ilgili yetenek ve ayr?cal?kl? olmayan hedef gerektirir. Hassas hedef denetimleri sunucuda ve ajanda tekrarlan?r; aray?zdeki kapal? d??me g?venlik s?n?r?n?n kendisi de?ildir.

Salt okunur lisans, lisansl? ?zellik gezinmesini kald?r?r ve kasa/dizin yazmalar?n? engeller. ?nceden y?klenmi? kay?t okunabilir durumda kalabilir; ancak salt okunur kip AD'yi, VaultPilot giri? eri?imini veya ?ifreli kay?t sahipli?ini de?i?tirme izni vermez.

## Kay?t Kayna?? ve Sahiplik

Yeni ve kaynak kontroll? dizin kay?tlar?, **Entegrasyonlar > Active Directory** ekran?nda se?ilip yaz?labilir kasaya aktar?l?r. Active Directory kay?tlar? ekran?nda bilerek **Yeni kay?t** d??mesi yoktur; burada elle RDP veya SSH kimlik bilgisi olu?turulmaz. Sunucu, dizin kaynakl? `CREDENTIAL` i?in e?itlenmi? sa?lay?c? ve kullan?c? DN'i ister; ayn? kasada ayn? sa?lay?c?/kullan?c? kayna??ndan ikinci kay?t olu?turulmas?n? engeller.

Aktar?lan kay?t, se?ili kullan?c?ya ve i?letim ba?lam?na ait ?ifreli bir anl?k g?r?nt? ta??r. Envanterde bulundu?u ?l??de sa?lay?c?, alan ad?, hesap, DN/OU, etkinlik ve kilit durumu, parola durumu sinyalleri, son giri?, son g?r?lme, son e?itleme, ayr?cal?k sinyali, hedef, protokol, kategori, sahip ba?lam?, etiket ve risk i?erebilir. Liste her a??ld???nda AD'ye canl? okuma yapmaz.

DC Agent mevcut AD parolas?n? okuyamaz. Yeni aktar?lan dizin kayd? bu nedenle parolas?z ba?lar. Saklanan hedef veya varsay?lan RDP protokol? yaln?z ba?lant? ba?lam?d?r; hesab?n s?nand???n? ya da hedefin onayl? y?netim u? noktas? oldu?unu kan?tlamaz.

G?r?nen **Sahip** de?eri ?ifreli kay?t ba?lam?ndan gelir: a??k sahip alan?, dizin hesab? veya kullan?c? ad?. Sistem Owner rol?, kasa rol?, AD nesne sahibi veya operasyonel sorumluluk kan?t? de?ildir. Kasa eri?imini ayr?ca Viewer, Editor ve Manager izinleri belirler.

## Arama, Filtreler ve D?zen

Arama kutusu kay?t ba?l???, kullan?c? ad?, URL, hedef, alan ad?, sahip, kategori, kaynak, risk, etiketler, sa?lay?c? ad?, dizin hesab?, ?st DN, nesne t?r? ve protokol i?inde e?le?me arar. Active Directory'yi sorgulamaz ve eksiksiz DN aramas? say?lmamal?d?r.

H?zl? filtre sat?r? veriye g?re olu?ur ve en fazla on denetim g?sterir:

- **T?m?** protokol, kaynak, risk ve ak?ll? filtreleri s?f?rlar.
- E?le?en kay?t varsa **RDP** ve **SSH** g?r?n?r.
- Kaynak k?sayollar? **AD e?itleme**, **Elle girildi**, **??e aktar?ld?** ve **Ke?fedildi** se?eneklerini g?sterebilir.
- E?le?en say? ve sat?rdaki yer izin verdi?inde **Kritik**, **Uyar?**, **S?resi dolmu?** ve **Bilinmiyor** riskleri g?r?nebilir.

H?zl? filtre say?lar?, di?er etkin filtrelerin kesi?iminden de?il aktif kasadaki b?t?n Active Directory kay?tlar?ndan hesaplan?r. Protokol, kaynak veya risk k?sayolu se?ildi?inde di?er kimlik bilgisi k?sayollar? ve ak?ll? filtreler temizlenir.

**Ak?ll? filtre ekle**, y?klenen kay?tlardan se?enek ?retir. Kullan?c? ad? veya sahip, ?r?n/servis, kategori, etiket, protokol, kaynak, risk ve kimlik bilgisi durumu boyutlar? bulunabilir:

| Kimlik bilgisi durumu | Kaynak kural? |
| --- | --- |
| **Y?netilen** | ?ifreli y?kte dizin meta verisi vard?r veya kaynak AD e?itleme ya da Yenilendi'dir. |
| **Y?netilmeyen** | Y?k, y?netilen kural?n? kar??lamaz. |
| **S?resi dolan / pasif** | Risk S?resi dolmu?'tur veya kay?t durumu Disabled/Revoked'dur. |
| **Bilgi eksik** | Saklanan hedef veya kullan?c? ad? yoktur. |

Birden ?ok ak?ll? filtre VE mant???yla birle?ir. Tek filtreyi ?ipinden kald?r?n veya ak?ll? filtre k?mesini **Temizle** ile s?f?rlay?n. Bu durumlar saklanan y?k meta verisini a??klar; g?ncel sa?lay?c? sa?l??? veya parola ge?erlili?i testi de?ildir.

Yo?unluk denetimi **Kart** ve **Tablo** g?r?n?m? aras?nda ge?i? yapar. Tablo ba?l?klar? **Kay?t**, **?ifreli oturum verisi** ve **??lemler**'dir. ?ki g?r?n?m de ayn? filtrelenmi? kay?t k?mesini kullan?r; kay?tlar kasadaki son g?ncelleme s?ras?yla gelir.

## Kay?t Sat?r? ve Ayr?nt? Paneli

Her sat?r ?unlar? g?sterebilir:

- RDP veya SSH kimli?i, ba?l?k, saklanan hedef ve hesap;
- kaynak ve risk ?ipleri;
- varsa dizin alan ad?, ba?lamsal sahip ve son e?itleme zaman?;
- en fazla ?? AD durum ?ipi ve ek durumlar i?in `+N`;
- ?ifreli kayd?n son g?ncelleme zaman?.

Veri varsa AD durum ?ipleri ?u s?rayla ?retilir: **Aktif** veya **Kapal?**, **Kilitli**, **Parola de?i?imi gerekli**, **S?resi dolmu?**, **Yetkili**, **S?resiz parola**, **Eski login** ve **Son giri?**. Kilit, parola s?resinin dolmas? veya zorunlu de?i?tirme sinyali aktar?m s?ras?nda kritik say?l?r. Ayr?cal?kl?, eski oturum, s?resiz parola ve kapal? hesap sinyalleri uyar? durumuna katk? verir. Daha sonraki desteklenen g?ncelleme yenileyene kadar sat?r ?ifreli anl?k g?r?nt?y? g?stermeye devam eder.

**Kay?t ayr?nt?lar?n? a?**; kaynak, risk, kay?t durumu, hesap, hedef, kategori, ba?lamsal sahip, etiketler, son g?ncelleme, AD sa?lay?c?s?, alan ad?, OU/DN, son e?itleme, son giri?, son g?r?lme ve ?zet AD durum listesini i?eren etkile?imi engellemeyen yan paneli a?ar. Panel parola veya ba?ka gizli de?er g?stermez. Yetkiniz varsa ayr? g?sterme veya kopyalama i?lemini kullan?n.

## Kay?t ??lemleri

Sat?rda ?u birincil i?lemler bulunabilir:

- Saklanan RDP hedefi varsa **RDP paketini haz?rla**. Taray?c? `.rdp` dosyas? indirir; kay?tl? parola k?sa ?m?rl? panoya kopyalan?r. ?retilen dosyada yerel kaynak y?nlendirmeleri kapal?d?r.
- Saklanan SSH hedefi varsa **SSH URI a?**. Kay?tl? parola k?sa ?m?rl? panoya kopyalan?r ancak URI i?ine yaz?lmaz.
- Kullan?c? ad? varsa **Kullan?c? ad?n? kopyala**.

??lem men?s? ?unlar? i?erebilir:

- **Kay?t ayr?nt?lar?n? a?**;
- **VaultPilot giri?ine al** veya **VaultPilot giri?inden ??kar**;
- a?a??da a??klanan uygun DC Agent i?lemleri;
- de?er varsa **Gizli de?eri kopyala**, **Gizli de?eri g?ster** ve kullan?c? taraf?ndan ba?lat?lan s?z?nt? kontrol?;
- SSH kayd?nda **SSH komutunu kopyala**; parola komuta eklenmez;
- aktif kasa yaz?labiliyorsa **Kayd? d?zenle** ve **Kayd? sil**.

G?sterme i?lemi onay ister, de?eri taray?c?da ge?ici olarak g?r?n?r yapar ve `VIEW` denetim olay? yazmay? dener. Kopyalama ve ba?lant? i?lemleri gerekti?inde k?sa ?m?rl? pano kullan?r; `COPY` veya `VIEW` kan?t? yazar. Denetim bildirimi ba?ar?s?zsa nedeni inceleyin; bu durum de?eri ba?ka yerde payla?may? g?venli yapmaz.

Genel d?zenleme AD de?i?ikli?i de?ildir. Dizin kontroll? kimlik bilgisi kay?tlar? sunucudaki kaynak kurallar?yla korunur ve men? g?r?nse bile genel d?zenleyici taraf?ndan reddedilebilir. **Kayd? sil**, onaydan sonra ?ifreli kayd? aktif kasadan kald?r?r ve `DELETE` olay? yazar; kaynak AD hesab?n? silmez, kapatmaz, kilidini a?maz veya parolas?n? de?i?tirmez.

`CREDENTIAL` i?in kopya kay?t olu?turma i?lemi yoktur. Genel toplu men? d??a aktarma, kategori/etiket, ar?ivleme, pasifle?tirme/iptal, g?venlik kontrol?, denetim raporu, payla??m, not, d?zenleme ve kald?rma i?lemlerini g?sterebilir; bunlar kasa kayd? i?lemleridir. Toplu LDAP, PAM, parola s?f?rlama, kilit a?ma veya dizin hesab? kapatma i?lemi de?ildir ve dizin sahipli kay?tlar sunucu kaynak k?s?tlar?na tabidir. Hassas d??a aktar?m, onaydan sonra se?ili ??z?lm?? y?kleri dosyaya yazar ve `EXPORT` kan?t? olu?turur.

## VaultPilot Giri? Eri?imi

**VaultPilot giri?ine al**, AD yetkisi de?i?tiren bir i?lem de?il, VaultPilot kullan?c? ya?am d?ng?s? i?lemidir. Owner, yaz?labilir lisans, kullan?labilir kullan?c? ad? ve ?ifreli kay?tta saklanan parola gerekir. ??z?mlenen dizin kayd?nda sa?lay?c? ve DN de zorunludur. Etkinle?tirme, ilgili VaultPilot giri? kimli?ini ve ki?isel kasa anahtar materyalini olu?turur veya yeniden a?ar; kald?rma VaultPilot giri? kimli?ini kapat?r ve g?ncel sa?lay?c? hedefi bulunuyorsa dizin giri? se?imini g?nceller.

VaultPilot kimlik ya?am d?ng?s? yaz?m? ile sa?lay?c?daki giri? se?imi g?ncellemesi ayn? transaction kapsam?nda de?ildir. Kimlik olu?turulmu?, yeniden etkinle?tirilmi? veya kapat?lm?? olabilir; ard?ndan sa?lay?c? se?iminin g?ncellenmesi ba?ar?s?z olabilir. Bu nedenle hata bildirimi b?t?n de?i?ikliklerin geri al?nd???n? kan?tlamaz. Yeniden denemeden ?nce durun; **Kullan?c?lar** ekran?ndaki kimlik ve giri? durumunu, **Entegrasyonlar > Active Directory** i?indeki sa?lay?c? giri? se?imini ve **Denetim G?nl???** ya?am d?ng?s? olaylar?n? uzla?t?r?n.

AD e?itleme kayd?nda normalde parola yoktur; ajan mevcut parolay? okuyamaz. Bu nedenle giri?e alma, onayl? parola de?i?tirme ak??? bir de?er ?retip g?venle kaydedene kadar kapal?d?r. Bu i?lem AD grup de?i?ikli?i, MFA kurulumu, PAM onay? veya dizin parolas?n?n g?ncel oldu?una ili?kin test de?ildir.

## DC Agent ??lemleri ve Yetenek S?n?r?

D?rt hassas kay?t i?lemi yaln?z ?ifreli kay?t, Owner taraf?ndan g?r?lebilen g?ncel sa?lay?c?da bir USER nesnesine ??z?mlenebiliyorsa g?r?n?r:

| Aray?z i?lemi | Ajan ba?ar?l? oldu?unda AD etkisi | Yapmad??? i?lem |
| --- | --- | --- |
| **Kilidi a?** | Hesap kilidini temizler. | Kapal? hesab? a?maz, parolay? de?i?tirmez veya eri?im vermez. |
| **Parola de?i?imi iste** | Bir sonraki oturum a?mada parola de?i?ikli?ini zorunlu k?lar. | Parola ?retmez, hesab?n kilidini a?maz ve tek ba??na VaultPilot giri?ini de?i?tirmez. |
| **Parolay? de?i?tir** | Ajan y?netilen parola ?retir, AD parolas?n? s?f?rlar ve ?retilen de?eri iste?i yapan Owner'?n VaultPilot a??k anahtar?na ?ifreleyerek d?nd?r?r. | Sonraki oturumda yeniden parola de?i?ikli?ini otomatik zorunlu k?lmaz; kurum ilkesi istiyorsa ayr? i?lemi kullan?n. |
| **Hesab? kapat** | AD kullan?c?s?n? kapat?r. | AD nesnesini veya ?ifreli kasa kayd?n? silmez. |

Her hassas i?lem kurumsal onay ister ve e?zamanl? tamamlanmak yerine kuyru?a al?n?r. Ba?l? ajan ilgili yetene?i bildirmelidir: `UNLOCK_ACCOUNT`, `REQUIRE_PASSWORD_CHANGE`, `RESET_TEMP_PASSWORD` veya `DISABLE_ACCOUNT`. Bekleyen, ajan?n i?ledi?i, ba?ar?l?, ba?ar?s?z, inceleme gerekli veya iptal edilmi? sonucu Entegrasyonlar ve ??lemler ekranlar?nda izleyin.

Ayr?cal?kl? veya yerle?ik hedef kesin durma nedenidir. ?stemci, g?ncel ayr?cal?k anl?k g?r?nt?s?ne g?re i?lemleri kapat?r; sunucu hedefi yeniden ??z?mler ve ayr?cal?kl? kullan?c?da hassas i?lemi reddeder; ajan de?i?iklikten ?nce yerle?ik hesap ve ayr?cal?kl? grup durumunu tekrar denetler. ?stek, sa?lay?c? verisi veya yerel i?lem veritaban? d?zenleyerek bu kontrolleri a?may?n.

**Parolay? de?i?tir** AD ?zerinde ba?ar?l? olduktan sonra ?ifreli i?lem sonucu ile kasa kayd?n?n g?ncellenmesi ayr? sonu?lard?r. Kasa anahtar? ve yazma eri?imi varsa taray?c?, ?retilen de?eri iste?i yapan kullan?c? i?in ??zmeyi ve ba?vurulan kasa kayd?na yeniden ?ifrelemeyi dener. Hem ajan ba?ar?s?n? hem de ayr? kay?t g?ncelleme bildirimini, g?ncel kayd? ve denetim kan?t?n? do?rulay?n. Sonu?lar uyu?muyorsa AD parolas?n? de?i?mi?, kasa kayd?n? ise do?rulanmam?? kabul edin; yeniden denemeden ?nce durun.

Bu ekranda do?rudan LDAP bind i?lemi, rastgele PowerShell ?al??t?rma, PAM onay?, oturum kayd? veya ayr?cal?k y?kseltme yoktur. Sa?lay?c? kayd?, se?im, e?itleme, sa?l?k, yetenek ve ajan token i?lemleri **Entegrasyonlar > Active Directory** ekran?na aittir.

## Denetim ve Kan?t

Dizin kayd? aktar?m? kay?t olu?turma kan?t? yazar. G?sterme, kopyalama, ba?lant?, d??a aktarma, d?zenleme ve silme i?lemleri ilgili kasa denetim eylemlerini kullan?r. Dizin i?lemi olu?turma, iptal ve sonu? olaylar?; i?lem, sa?lay?c?, durum ve i?lem kimlikleriyle `DIRECTORY_AGENT_ACTION` kan?t? olarak yaz?l?r. Kesin DN ve ?retilen parola herkese a??k kan?t de?ildir. VaultPilot giri?ine alma/??karma kullan?c? ya?am d?ng?s? kan?t? olu?turur; sa?lay?c? se?im sonucunu ayr?ca do?rulay?n.

Kay?t sat?r?n?, ayr?nt? panelini, i?lem bildirimini, Entegrasyonlar i?lem ge?mi?ini, ??lemler kayd?n? ve Denetim G?nl???n? ayr? kan?t katmanlar? olarak de?erlendirin. Kuyru?a al?nd? bildirimi AD ba?ar?s?n? kan?tlamaz. Ajan ba?ar?s?, ?ifreli parolan?n kasaya yaz?ld???n? kan?tlamaz. De?i?en kasa zaman? da AD i?leminin ba?ar?l? oldu?unu tek ba??na kan?tlamaz.

## Ekran Durumlar?

| Durum | Operat?r cevab? |
| --- | --- |
| Y?kleniyor | ?ifreli kay?tlar al?n?p ??z?l?rken d?rt iskelet sat?r? g?r?n?r. Kasan?n bo? oldu?una karar vermeden ?nce bekleyin. |
| Aktif kasada kay?t yok | Se?ili AD kullan?c?lar?n? Entegrasyonlar ?zerinden aktar?n. Dizin kimlik bilgileri i?in genel bo? durumdaki Yeni kay?t ?nerisini izlemeyin. |
| Filtre e?le?mesi yok | Arama metnini kald?r?n, **T?m?**'n? se?in, ak?ll? filtreleri veya bo? durumdaki **Filtreleri temizle** i?lemini kullan?n. |
| Kay?t ??z?lemiyor | Genel uyar?, bir veya daha fazla kayd?n aktif kasa anahtar?yla ??z?lemedi?ini bildirir. Durun, se?ili kasa/anahtar? do?rulay?n ve kayd?n ?zerine yazmay?n. |
| Liste iste?i kullan?lam?yor | Ayr? liste hata kart? yoktur; ba?ar?s?z istek bo? sonu? gibi g?r?nebilir. Aktar?m veya silme ?ncesi genel bildirimi, oturumu, kasay? ve sunucuyu do?rulay?n. |
| Sa?lay?c? veya USER hedefi ??z?mlenemiyor | ?ifreli kay?t g?r?n?r kal?r ancak g?ncel dizin i?lemleri g?r?nmez. Entegrasyonlar'da sa?lay?c? se?imini ve e?itlemeyi inceleyin. |
| Ajan eski, ?evrimd???, ba?lant? bekliyor veya iptal edilmi? | Dizin i?lemleri kapal? kal?r. Onayl? ajan ba?lant?s?n? d?zeltin; kay?t anl?k g?r?nt?s?n? canl? saymay?n. |
| Yetenek eksik | Ajan ba?l? olsa bile ilgili i?lem kapal?d?r. Yetene?i atlamak yerine onayl? ajan? y?kseltin veya onar?n. |
| Ayr?cal?kl? hedef | Hassas dizin i?lemleri kapal?d?r; sunucu ve ajan denetimleri iste?i reddeder. Kurumun ayr?cal?kl? hesap prosed?r?n? kullan?n. |
| Viewer veya salt okunur lisans | Okuma i?lemleri kalabilir; kasa yazmalar?, giri? de?i?iklikleri ve dizin i?lemleri engellenir. |
| ??lem kuyru?a al?nd? | ??lemi Entegrasyonlar veya ??lemler ekran?nda izleyin; ilk i?lem etkinken tekrar ba?latmay?n. |
| AD i?lemi ba?ar?l?, kasa g?ncellemesi do?rulanmad? | ?ifreli i?lem sonucunu ve denetim kan?t?n? koruyun. Sahiplik uzla?t?r?lmadan ikinci parola s?f?rlamas? yapmay?n. |
| VaultPilot kimli?i ile sa?lay?c? se?imi uyu?muyor | Hata bildiriminin tam rollback oldu?unu varsaymay?n. Kullan?c?lar'daki giri? durumunu, sa?lay?c? se?imini ve Denetim G?nl???n? uzla?t?rmadan i?lemi yinelemeyin. |

## ??lemden ?nce

- Hedef aktif kasay?, sistem rol?n?, kasa rol?n?, entegrasyon ?zelli?ini ve yaz?labilir lisans? do?rulay?n.
- Meta veriyi g?ncel saymadan ?nce kay?t kayna??n?, sa?lay?c?y?, alan ad?n?, hesab?, son e?itlemeyi ve son g?r?lmeyi kar??la?t?r?n.
- Sa?lay?c?n?n ba?l? oldu?unu, kesin yetene?in bulundu?unu ve g?ncel nesnenin USER olarak ??z?mlendi?ini do?rulay?n.
- Ayr?cal?kl? veya yerle?ik hedefte durun; ba?ka u? nokta kullanarak engeli a?may?n.
- Kasa kayd? i?lemini, AD i?lemini ve VaultPilot giri?ine alma i?lemini birbirinden ay?r?n.
- Parola de?i?iminden ?nce ?retilen de?erin hangi kasa kayd?na ve hangi yetkiyle yaz?laca??n? netle?tirin; AD sonucunu, ?ifreli sonucu, kasa g?ncellemesini ve denetimi ayr? ayr? do?rulay?n.
- VaultPilot giri? eri?imi de?i?ecekse Kullan?c?lar'daki kimlik durumunu, sa?lay?c? giri? se?imini ve Denetim G?nl???n? yeniden deneme ?l??t? olarak belirleyin.

## G?venli Kan?t

- Payla??labilir: genel kaynak s?n?f?, RDP veya SSH protokol?, genelle?tirilmi? risk/durum, sistem ve kasa rol? s?n?f?, dizin i?lem t?r?, i?lem durumu, yakla??k zaman aral??? ve redakte hata kategorisi.
- Gizli kalmal?: ba?l?k, kullan?c? ad?/hesap, sahip ba?lam?, hedef, alan ad?, sa?lay?c? ad?, DN/OU/base DN, etiketler, kesin e?itleme/giri? zaman?, ayr?cal?kl? grup adlar?, kay?t/i?lem/sa?lay?c? kimlikleri, RDP paketi, SSH URI/komutu ve tam sat?r veya panel ekran g?r?nt?s?.
- Asla payla?may?n: saklanan veya ?retilen parola, pano i?eri?i, ?ifreli i?lem parola sonucu, ?ifreli kay?t y?k?, kasa anahtar?, ana parola, kullan?c? ?zel anahtar?, bind kimlik bilgisi, ajan token?, ham dizin envanteri, hassas d??a aktar?m veya ger?ek hedef i?eren ajan/sunucu logu.
- Parola, ?retilen i?lem sonucu, bind kimlik bilgisi veya ajan token? herkese a??k kan?ta girdiyse a???a ??km?? kabul edin; ilgili prosed?rle de?i?tirin ya da iptal edin.

## Ne Zaman Durmal? ve Destek ?stemelisiniz

Aktif kasa veya kaynak sa?lay?c? belirsizse, hedef art?k ??z?mlenmiyorsa, ayr?cal?k durumu beklenmedikse, ajan yetene?i/sa?l??? aray?zle ?eli?iyorsa, i?lem inceleme gerekli durumunda kal?yorsa, AD ba?ar? bildirirken kasa parola g?ncellemesi do?rulanam?yorsa, VaultPilot kimlik durumu sa?lay?c? giri? se?imiyle uyu?muyorsa ya da denetim kan?t? yoksa durun. Kullan?c?lar'daki giri? durumu, sa?lay?c? se?imi ve Denetim G?nl??? uzla?t?r?lmadan giri? i?lemini yeniden denemeyin. DN, hesap, parola, token veya d??a aktar?lm?? y?k eklemeden genel kay?t t?r?, sa?lay?c? sa?l?k s?n?f?, yetenek, i?lem t?r?/durumu, yakla??k zaman ve redakte hatayla ?zel destek kayd? a??n.

## Operat?r Notlar?

Active Directory kay?tlar?, dizin kaynakl? ba?lam ta??yan ?ifreli kasa kay?tlar?d?r. Canl? AD nesnesi de?ildir ve genel kimlik bilgisi y?netimi veya PAM katman? olu?turmaz. Sa?lay?c? i?lemlerini Entegrasyonlar'da, i?lem takibini ??lemler'de, kan?t incelemesini Denetim G?nl???nde tutun.

## ?lgili

- [Etki Alan? paneli](screen-domain-dashboard.md)
- [Entegrasyonlar ekran?](screen-integrations.md)
- [??lemler ekran?](screen-executions.md)
- [Denetim G?nl??? ekran?](screen-audit-log.md)
- [Active Directory ajan?](active-directory-agent.md)
- [DC Agent sorun giderme](../../kb/tr/dc-agent-service.md)
