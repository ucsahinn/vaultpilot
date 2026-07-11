# Sunucu Ayarlar? Ekran?

?st ?ubuktaki `?`, **Eri?im & HTTPS**, **SMTP** veya **Bak?m ve Loglar** sekmesi a??kken bu k?lavuzu a?ar. **Giri? g?venli?i** sekmesinde ise ayn? d??me ki?isel giri? g?venli?i k?lavuzuna gider.

Sunucu ayarlar?n?; kullan?c?lar?n a?aca?? HTTPS adresini belirlemek, SMTP teslim kanal?n? kurmak, kurtarma veya ge?i? verisi almak, kontroll? servis yeniden ba?latmas? kuyru?a koymak ve belirli operasyon ge?mi?lerini yedekleyip temizlemek ya da geri y?klemek i?in kullan?n. Bu ekranda g?nl?k d?nd?rme, g?nl?k saklama veya denetim kayd? saklama de?erlerini de?i?tiren bir kontrol yoktur.

## Eri?im ve Yetki

- Sahip, Y?netici ve Denet?i rolleri ?? sistem sekmesini okuyabilir. Kullan?c? rol? ki?isel **Giri? g?venli?i** alan?na y?nlendirilir.
- Eri?im veya SMTP ayarlar?n? kaydetme, sertifika y?kleme, SMTP testi g?nderme, sunucu yede?i i?e aktarma, servisi yeniden ba?latma ve bak?m yedeklerini ?al??t?r?p geri y?kleme yaln?z Sahip rol?ne a??kt?r.
- Salt okunur lisans, Sahip rol?ne ait bu sunucu i?lemlerini kapatmaz. Ancak kasaya ge?i? verisi almak i?in lisans?n yaz?labilir, aktif kasan?n kilidinin a??k ve kasa rol?n?n **Editor** veya **Manager** olmas? gerekir.
- Y?netici ve Denet?i g?r?n?m? inceleme ama?l?d?r. Aray?zdeki kapal? d??meler sunucudaki Sahip denetimini a?maz.

## Eri?im & HTTPS

**Yay?n adresi veya alan ad?** ile **Yay?n portu**, kullan?c?lar?n a?aca?? adresi tan?mlar. Sunucu, adresi normalle?tirir ve her zaman HTTPS adresi ?retir. Bu ekranda HTTP/HTTPS anahtar? yoktur.

?ki sertifika kayna??ndan birini se?in:

- **Otomatik sertifika**, sunucunun y?netti?i sertifika kayna??n? korur.
- **Kurumsal sertifika**, en fazla 2 MiB boyutunda `.pfx` veya `.p12` dosyas? kabul eder. Kaydetme s?ras?nda dosya sunucunun y?netti?i sertifika dizinine y?klenir ve y?netilen dosya yolu ayarlara yaz?l?r.

Y?kleme alan? sertifika parolas? istemez; sertifika makam?n?, g?ven zincirini, biti? tarihini, ?zel anahtar?n varl???n?, alan ad? e?le?mesini veya ?al??an HTTPS ba?lant?s?n? do?rulamaz. Paketi genel kanallar?n d???nda do?rulay?n; yeniden ba?latma sonras?nda ger?ek HTTPS adresini ayr?ca s?nay?n.

Yay?n adresi, port veya kurumsal sertifika de?i?ikli?i yeniden ba?latmadan sonra taray?c? eri?imini kesebilir. Kaydetmeden ?nce ?al??an adresi not edin ve onayl? bir sunucu konsolu ya da kurtarma ba?lant?s? haz?rlay?n.

## SMTP

**SMTP a??k** se?ildi?inde hesap ad?, SMTP sunucusu, port, g?nderen e-posta, TLS/STARTTLS, kimlik do?rulama, kullan?c? ad? ve parola veya token alanlar? g?r?n?r. **SMTP kapal?**, uygulama i?i bildirimleri ve denetim kayd?n? s?rd?r?rken e-posta g?nderimini durdurur; kimlik do?rulama ayr?ca kapat?l?p form kaydedilmedik?e kay?tl? SMTP ayr?nt?lar? korunur.

?nemli s?n?rlar:

- SMTP sunucusu alan?na yaln?z sunucu ad? girilir. Adres ?emas?, kimlik bilgisi, port, dosya yolu veya sorgu verisi eklemeyin.
- Kimlik do?rulama a??ksa TLS/STARTTLS, kullan?c? ad? ve yeni ya da ?nceden kaydedilmi? parola/token gerekir.
- Parola alan?n? bo? b?rakmak, daha ?nce kaydedilmi? de?eri korur. Aray?z kay?tl? s?rr? geri okuyup g?stermez.
- Al?c?lar ve olay kurallar? bu sekmede de?il, **Bildirimler** ekran?nda y?netilir. SMTP a??lacaksa en az bir al?c? ve bir bildirim olay? bulunmal?d?r.
- **Test g?nder**, ekranda o anda g?r?nen SMTP de?erlerini kaydetmeden kullan?r. Test al?c?s? zorunludur; deneme, tasla?? kal?c?la?t?rmaz.
- Ba?ar?l? test, `SMTP_TEST_EMAIL_SEND` i?lemiyle bir `SERVER_MAINTENANCE` olay? yazar. Parola veya token denetim meta verisine eklenmez.

## Ortak Kaydetme ve S?f?rlama Davran???

Eri?im ve SMTP ayr? sekmeler gibi g?r?n?r; ancak ayn? formu ve ayn? tasla?? payla??r:

- **Ayarlar? kaydet**, yay?n adresini, sertifika se?imini, SMTP yap?land?rmas?n? ve sunucudan y?klenmi? fakat ekranda g?sterilmeyen g?nl?k ilkesi de?erlerini birlikte g?nderir.
- Bu nedenle a??k durumdaki eksik SMTP yap?land?rmas?, **Eri?im & HTTPS** sekmesinden ba?lat?lan kaydetmeyi engelleyebilir. Ge?ersiz yay?n adresi veya port da **SMTP** sekmesinden ba?lat?lan kaydetmeyi durdurabilir.
- **Formu s?f?rla**, iki sekmedeki kaydedilmemi? tasla?? birlikte b?rak?r ve sunucunun son d?nd?rd??? ayarlar? yeniden y?kler. Sunucuda geri alma i?lemi yapmaz.
- Bak?m sekmesi kendi i?lemlerini ?al??t?r?r; bu sekmede Kaydet veya S?f?rla alt ?ubu?u yoktur.
- Kaydetme ba?ar?s? ayar dosyas?n?n yaz?ld???n? g?sterir. Aray?z, yeni de?erlere g?venmeden ?nce servisin yeniden ba?lat?lmas?n? ister.

Kurumsal sertifika se?ildiyse dosya, ayar kayd?ndan ?nce y?klenir. Sonraki do?rulama, kal?c?l?k veya denetim yaz?m? ba?ar?s?z olsa bile y?klenen dosya sunucuda kalabilir. Yeniden denemeden ?nce Sunucu ayarlar?n? tekrar okuyun ve sertifika y?kleme olay?n? denetim kayd?nda aray?n.

## Bak?m ve Loglar

Bu sekme ge?erli veritaban? yolunu, veritaban? koruma durumunu ve servis g?nl?k dosyas?n?n yolunu g?sterir. Bunlar tan? de?eridir; d?zenlenebilir alan de?ildir. G?ncel aray?zde g?nl?k boyutu, destek paketi g?nl?k s?n?r?, g?nl?k saklama veya denetim kayd? saklama kontrol? bulunmaz.

### Sunucu yede?ini i?e aktarma

**Sunucu yede?ini i?e aktar**, VaultPilot Backup Tool ZIP ar?ivini veya ?ifreli JSON d??a aktar?m?n? kabul eder. Bu i?lem birle?tirme de?il, t?m profili geri d?nd?rme i?lemidir:

- Sahip rol? y?klemeden ?nce i?lemi onaylar.
- B?t?nl?k ve ?zg?nl?k bilgisi denetlenir. Eski ya da ba?ka kaynaktan gelen yedek i?in ek risk onay? gerekir.
- Mevcut kurulu?, kullan?c?lar, kasalar, ?ifreli kay?tlar, dosya par?alar? ve denetim ge?mi?i tek veritaban? i?lemi i?inde de?i?tirilir.
- ??e al?nan 2FA ba?lar? temizlenir. Ard?ndan kal?c? oturumlar kapat?l?r ve operat?r yedek profiline ait ana parolayla yeniden kilit a?ar.
- Geri y?klenen profile, adetleri ve ?zg?nl?k denetiminin gev?etilip gev?etilmedi?ini belirten bir `IMPORT` olay? eklenir.

Bu ekranda t?m sunucu yede?i olu?turan veya d??a aktaran bir d??me yoktur. Kurtarma dosyas?n? VaultPilot Backup Tool ile olu?turun.

### ??e aktar?m ve ge?i?

**D??a aktar?m dosyas? se?**, desteklenen dosyay? taray?c?da okur ve Parolalar ekran?nda ?nizleme a?ar. Bitwarden CSV/JSON, LastPass CSV, KeePass XML/CSV, 1Password CSV ve Chrome/Edge CSV bi?imleri g?sterilir. `.1pux` ar?ivi i?e al?nmaz; 1Password CSV d??a aktar?m?n? kullan?n. **VaultPilot ?ablonu**, ?r?n ?ablonunu indirir.

?nizleme, kal?c? kay?t anlam?na gelmez. Son i?e aktarma i?in aktif kasan?n kilidi a??k olmal?; lisans yaz?labilir, kasa rol? Editor veya Manager olmal?d?r. Sat?rlar se?ilen ?ak??ma kural?na g?re s?rayla olu?turulur ya da g?ncellenir. Sonraki bir sat?r hata verdi?inde ?nceki sat?rlar kaydedilmi? olabilir. Yeniden denemeden ?nce sonu? adetlerini ve kay?t baz?ndaki denetim olaylar?n? kar??la?t?r?n.

### Sunucu servisini yeniden ba?latma

**Yeniden ba?lat**, yaln?z Sahip rol?nde ve Sunucu ayarlar? tasla??nda kaydedilmemi? de?i?iklik yokken a??l?r. Uyar? onay?ndan sonra uygulama `VaultPilotServer` veya eski kurulumlarla uyumlu `PassManServer` servisi i?in yeniden ba?latma kuyru?u olu?turur. Sa?l?k denetiminin tamamlanmas?n? beklemez. Konsol k?sa s?re ba?lant?y? kaybedebilir; yaln?z kaydedilmi? ayarlar devreye girebilir.

Kuyruk i?lemi, `SERVER_RESTART_QUEUE` ayr?nt?s?yla `SERVER_RESTART` olay? yazar. Ba?lant? geri geldi?inde servisi, etkin HTTPS adresini ve yeni bir oturum a?may? do?rulay?n.

### Bak?m kay?tlar?

Aray?zdeki tek temizlik bi?imi **Yedekle ve temizle** i?lemidir. Her ?al??t?rmada yaln?z bir kategori ele al?n?r:

| Kategori | Kapsam |
| --- | --- |
| Denetim kayd? | Denetim ekran? ge?mi?i, zincir kontrol? kay?tlar? ve paneldeki denetim ge?mi?i. |
| Ke?if | Ke?if i?leri, bulgular, bast?rmalar ve tarama ilkeleri. |
| ??lemler | ??lem ge?mi?i ve bitmi? arka plan g?revleri; etkin i?lemler ve ?al??an g?revler korunur. |

Uyar? onay?ndan sonra VaultPilot, sunucudaki `maintenance-backups` dizinine kal?c? JSON yede?i yazar, kay?t adedini ve SHA-256 ?zetini kaydeder, ard?ndan yaln?z se?ilen kategoriyi temizler. Kasa s?rlar?, kaynak dosyalar, servis g?nl?k dosyalar? ve di?er bak?m kategorileri bu temizli?e girmez.

Ar?iv tablosu dosya ad?, kategori, olu?turma zaman?, kay?t adedi, boyut, ?zet ve **Geri y?kle** i?lemini g?sterir. Geri y?kleme yaln?z se?ilen kategoriyi yedekteki duruma d?nd?r?r. Yedekten sonra olu?an canl? kay?tlar de?i?ebilir veya kaybolabilir; di?er kategoriler de?i?mez. Temizlik ve geri y?kleme; i?lem, kategori, adetler, yedek dosyas? ad? ve ?zet i?eren `SERVER_MAINTENANCE` kan?t? b?rak?r.

## Giri? G?venli?i Ba?lam?

**Giri? g?venli?i**, Sunucu ayarlar? kabu?una yerle?tirilmi? ki?isel g?venlik alan?d?r; ortak sunucu ayarlar? formunun par?as? de?ildir. Ge?erli kullan?c?n?n ana parola de?i?imini ve 2FA ba??n? y?netir. Yaln?z Sahip rol? ayr?ca etkin oturum tablosunu g?r?r ve ge?erli olmayan oturumlar? kapatabilir.

Bu sekme a??kken ?st ?ubuktaki `?`, bilin?li olarak bu sayfa yerine [Giri? g?venli?i](screen-sign-in-security.md) k?lavuzunu a?ar.

## Denetim ve K?smi Tamamlanma S?n?r?

Bu i?lemlerde as?l etki, izleyen b?t?n kan?tlar yaz?lmadan ?nce olu?abilir. Hata yan?t? her zaman hi?bir ?ey yap?lmad??? anlam?na gelmez:

- Sertifika dosyas?, ayarlar kaydedilmeden ?nce sunucuda saklanabilir.
- Ayarlar, denetim olay? eklenmeden ?nce yaz?lm?? olabilir.
- Test e-postas?, denetim olay? eklenmeden ?nce teslim edilmi? olabilir.
- Servis yeniden ba?latmas?, denetim olay? eklenmeden ?nce kuyru?a al?nm?? olabilir.
- Bak?m yede?iyle kategori temizli?i veya geri y?kleme, son bak?m olay? yaz?lmadan ?nce tamamlanm?? olabilir.
- Profil i?e aktarma, oturum temizli?i tamamlanmadan ?nce veritaban?n? de?i?tirmi? olabilir.
- Ge?i? i?e aktar?m?, sonraki bir sat?r hata vermeden ?nce baz? sat?rlar? kaydetmi? olabilir.

Sonucu belirsiz bir hatadan sonra i?lemi hemen yinelemeyin. ?lgili ekran? yenileyin, etkin durumu kontrol edin, denetim ve operasyon g?nl?klerini inceleyin, varsa kal?c? yedek kayd?n? uzla?t?r?n.

## Ekran Durumlar?

| Durum | Operat?r cevab? |
| --- | --- |
| Sunucu API'si bekleniyor | Tan? verilerinin y?klenmesini bekleyin. S?rerse ge?erli oturumu ve sunucu eri?imini do?rulay?n. |
| G?ncel | Y?klenen taslak, sunucunun d?nd?rd??? kay?tl? ayarlarla e?le?ir. Bu durum d?? HTTPS veya SMTP adresinin ?al??t???n? kan?tlamaz. |
| Kaydedilmemi? de?i?iklik | ??lemden ayr?lmadan ?nce kaydedin ya da s?f?rlay?n. Tasla??n Eri?im ve SMTP sekmelerini birlikte kapsad???n? unutmay?n. |
| Kaydetme sonras? yeniden ba?lat / Yeniden ba?latma gerekli | ?al??an kurtarma ba?lant?s?n? koruyun, ?nce kaydedin, sonra onayl? zamanda Bak?m sekmesinden yeniden ba?lat?n. |
| SMTP kapal? | E-posta durur; uygulama i?i bildirimler ve denetim kayd? s?rer. |
| Parola kay?tl? / Parola yok | Sunucuda kimlik bilgisi vard?r ya da yoktur. Kay?tl? de?er g?sterilmez. |
| Test g?nderiliyor | Sonucu ve hedef posta kutusunu do?rulamadan ikinci test g?ndermeyin. |
| Sahip rol? gerekli | Salt okunur incelemeyi s?rd?r?n veya de?i?ikli?i Sahip rol?ne aktar?n. |
| Bak?m yedek ar?ivi okunuyor | Sunucudaki kal?c? listenin gelmesini bekleyin; hen?z yedek olmad??? sonucuna erken varmay?n. |
| Bak?m yede?i yok | Yaln?z se?ilen kategoriyi ger?ekten temizlemek istiyorsan?z **Yedekle ve temizle** ?al??t?r?n. |
| Kategori bak?m? ?al???yor | Ba?ka kategori bak?m? ba?latmay?n ve servisi yeniden ba?latmay?n. |
| Sunucu yede?i i?e al?n?yor | Taray?c?y? ve sunucuyu eri?ilebilir tutun; sayfay? yenilemeyin, servisi yeniden ba?latmay?n ve dosyay? tekrar y?klemeyin. |
| ??lem hata d?nd?rd? | Yeniden denemeden ?nce etkinin daha ?nce olu?up olu?mad???n? do?rulay?n. |

## ??lemden ?nce

- Etkin rol?, lisans durumunu, a??k sekmeyi ve ama?lanan kapsam? do?rulay?n.
- Eri?im de?i?ikli?inde ?al??an adresi kaydedin ve yeniden ba?latmadan ?nce sunucu konsoluna eri?im haz?rlay?n.
- Kurumsal sertifikan?n kayna??n?, alan ad? kapsam?n?, biti? tarihini, ?zel anahtar?n? ve kurtarma kopyas?n? taray?c? konsolunun d???nda do?rulay?n.
- SMTP i?in g?ndereni, test al?c?s?n?, al?c? listesini, olay kurallar?n? ve bo? parola alan?n?n kay?tl? de?eri korumas? gerekip gerekmedi?ini kontrol edin.
- T?m profil i?e aktar?m? veya y?ksek etkili ba?ka sunucu i?lemleri ?ncesinde VaultPilot Backup Tool ile tam kurtarma yede?i olu?turun.
- Bak?m temizli?inden ?nce kategoriyi adland?r?n, g?r?nen kay?t adedini al?n ve otomatik bak?m yede?inin, tam profil yede?i de?il yaln?z bu kategori i?in geri d?n?? noktas? oldu?unu do?rulay?n.
- Geri y?klemeden ?nce yedek kategorisini, olu?turma zaman?n?, kay?t adedini ve ?zeti kar??la?t?r?n; de?i?ebilecek yeni kay?tlar? belirleyin.
- Ge?i? ?ncesinde do?ru kasan?n kilidini a??n, ilgisiz se?imleri temizleyin, ?ak??ma kural?n? se?in, ge?ersiz veya yinelenen her sat?r? inceleyin.

## G?venli Kan?t

- Payla??labilir: sekme ad?, genel durum, geni? zaman aral???, `<SERVER_HOST>` gibi maskelenmi? sunucu ad?, yay?n portu, sertifika kayna?? ve dosya uzant?s?, SMTP a??k/TLS/kimlik do?rulama bilgisi, al?c? ve olay adetleri, bak?m kategorisi ve toplu ba?ar?/hata adetleri.
- Gizli kalmal?: tam i? sunucu ad? veya IP adresi, veritaban? ve g?nl?k dosyas? yollar?, PFX/P12 i?eri?i, sertifika parolas? veya ?zel anahtar, SMTP kullan?c? ad?/parola/token, g?nderen ve al?c? adresleri, oturum kimlikleri, yedek ZIP/JSON dosyalar?, ge?i? dosyalar?, kay?t adlar?, ham g?nl?kler ve m??teri ba?lam? i?eren kopyalanm?? denetim meta verileri.
- Tam yedek dosyas? ad?n? veya ?zetin tamam?n? yaln?z uzla?t?rma i?in gerekiyorsa onayl? ?zel destek kanal?ndan payla??n.

## Ne Zaman Durmal?

?al??an adres kaydedilmemi?se, sunucu konsoluyla kurtarma m?mk?n de?ilse, sertifika sahipli?i veya ?zel anahtar kapsam? belirsizse, SMTP onays?z al?c?ya gidecekse, aktif kasa ya da ?ak??ma kural? kesin de?ilse, yedek kategorisi veya zaman? ama?lanan geri y?klemeyle e?le?miyorsa, bak?m ar?ivi okunam?yorsa, yeni kategori kay?tlar?n?n etkisi de?erlendirilmemi?se ya da ?nceki deneme belirsiz hata verdiyse durun. Devam etmeden ?nce son kal?c? durumu uzla?t?r?n.

## Operat?r Notlar?

Kaydet i?lemini an?nda ?al??an yap?land?rma de?i?ikli?i, Yeniden ba?lat i?lemini tamamlanm?? sa?l?k denetimi, SMTP test hatas?n? iletinin gitmedi?ine dair kan?t, bak?m yede?ini tam kasa yede?i, ge?i? ?nizlemesini tamamlanm?? i?e aktar?m veya kategori geri y?klemesini t?m sunucuyu geri alma i?lemi olarak anlatmay?n. Sertifika paketlerini, kimlik bilgilerini, kurtarma ar?ivlerini, yerel dosya yollar?n? veya ham g?nl?kleri yay?mlamay?n.

## ?lgili

- [Sunucu Sistemi](server-system.md)
- [Yay?n adresi ve HTTPS](public-host-https-certificate.md)
- [Giri? g?venli?i](screen-sign-in-security.md)
- [Bildirimler ekran?](screen-notifications.md)
- [Denetim Ge?mi?i ekran?](screen-audit-log.md)
- [G?venli destek kan?t?](support-evidence-pack.md)
- [Sunucu ayarlar? yeniden ba?latma ve bak?m bilgi bankas?](../../kb/tr/server-settings-restart-maintenance.md)
- [Yedek i?e aktarma hatas?](../../kb/tr/backup-import-fails.md)
