# Lisans Ekran?

?st ?ubuktaki `?` simgesi Lisans ekran?na ait bu rehberi a?ar. Burada yaln?z ?lisans var m??? sorusunun cevab? de?il; do?rulanan plan, aktif kullan?c? kapasitesi, kalan s?re, yazma durumu ve kullan?labilir mod?ller birlikte g?r?l?r.

Bu ekran?n operat?r? **Sahip (Owner)** rol?d?r. Y?netici, Denet?i ve Kullan?c? rolleri lisans?n etkisini kilitli mod?ller veya salt okunur davran?? ?zerinden g?rebilir, ancak Lisans ?al??ma alan?n? a?amaz ve lisans kayd?n? y?netemez. Lisans etkinle?tirme ya da temizleme gerekti?inde i?lemi Sahip kullan?c?ya aktar?n. Rol s?n?r?n? ba?ka bir hesap veya do?rudan API iste?iyle a?maya ?al??may?n.

## Burada Ne Yap?l?r

- Durum rozetini **Aktif kullan?c?**, **Plan**, **Kalan g?n**, kapasite ?ubu?u ve **Plan yetenekleri** ile birlikte okuyun.
- Deneme s?r?m?ndeki 30 g?n ve 3 kullan?c? s?n?r?n?, imzal? lisans?n m??teri ve kullan?c? limitiyle kar??t?rmay?n.
- Men? g?r?n?r olsa bile mevcut plana dahil olmayan mod?l?n kilitli kalabilece?ini unutmay?n.
- **Mevcut lisans? temizle** i?leminin kasa verisini, kullan?c?lar?, oturumlar? veya denetim kan?t?n? de?il, sunucuda saklanan t?m lisans kay?tlar?n? kald?rd???n? bilin.

## Ekran? Nas?l Okumal?s?n?z

?st b?l?mdeki rozet lisans modunu, kapasite ?ubu?u aktif kullan?c?lar?n limite oran?n? g?sterir. **Yazma durumu** salt okunur oldu?unda kasa kay?tlar?n? de?i?tirme, yeni kullan?c? ve kasa olu?turma, payla??m, eklenti e?le?tirme, Discovery y?netimi ve i?e aktar?m?, dizin ajan? de?i?iklikleri ile g?ncelleme kurulumu gibi yazma ve y?netim i?lemleri kapan?r. Mevcut ?ifreli veriyi okuma ve kurtarma yollar? korunur. ?zin verilen kesin i?lemler i?in salt okunur mod rehberini izleyin. **Plan yetenekleri** b?l?m?ndeki a??k ve s?n?rl? kartlar, bir mod?l?n neden kullan?labildi?ini ya da kilitli kald???n? a??klar.

**Lisans ya?am d?ng?s?** band?, yenilemenin ne kadar acil oldu?unu 60, 30 ve 7 g?nl?k pencerelerle belirtir. Yaln?z rozet rengine bakmay?n; m??teri, plan, kalan g?n, kapasite ve yetenek listesinin birbiriyle tutarl? oldu?undan emin olun.

## ?nerilen ?? Ak??lar?

### Lisans durumunu a??klama

1. Modu, yazma durumunu ve kalan g?n? okuyun.
2. Aktif kullan?c? say?s?n? lisans limitiyle kar??la?t?r?n.
3. Kullan?lmak istenen mod?l? **Plan yetenekleri** i?inde bulun.
4. Son olarak kullan?c?n?n rol?n?n o i?lemi yapmaya izin verip vermedi?ini kontrol edin.

Beklenen sonu?, sorunun s?re, kapasite, plan kapsam? veya rol kaynakl? oldu?unun a??k?a ayr?lmas?d?r. Ekran verisi y?klenmiyorsa lisans kodunu yeniden girmeyin; sayfay? yenileyin ve sunucu sa?l???n? do?rulay?n.

### ?mzal? lisans? etkinle?tirme

1. Sahip hesab?yla oturum a??n.
2. Kodun do?ru m??teriye ve sat?n al?nan plana ait oldu?unu ?zel kanaldan do?rulay?n.
3. Kodu **Lisans kodu** alan?na yap??t?r?p **Lisans? etkinle?tir** d??mesini kullan?n.
4. Do?rulama sonras? m??teri, plan, limit, kalan g?n, yazma durumu ve yetenek listesini yeniden okuyun.

Ba?ar?l? i?lemde imzal? lisans bilgileri g?r?n?r ve yaln?z sat?n al?nan yetenekler a??l?r. Ekran **Lisans kodu do?rulanamad?** hatas? verirse art arda denemeyin; alan? temizleyin, hata metnini hassas ayr?nt?lar? ??kararak kaydedin ve ?zel deste?e ge?in. Aktivasyon tamamlan?r ancak m??teri, plan veya kapasite bekledi?iniz de?erle uyu?mazsa yeni bir de?i?iklik yapmadan durun.

### Yenileme ve kapasite planlama

Kalan s?re 60, 30 veya 7 g?n band?na geldi?inde yenileme sorumlusunu ve hedef tarihi belirleyin. Kapasite y?zde 90'a yakla??yorsa yeni kullan?c? a?madan ?nce aktif kullan?c? listesini sat?n al?nan limitle uzla?t?r?n. Yeni kod haz?r de?ilse mevcut lisans? temizlemeyin; temizleme bir geri alma mekanizmas? de?ildir ve sunucuyu deneme ya da salt okunur davran???na ta??yabilir.

### Lisans? yenileme veya de?i?tirme

Yeni kod haz?r oldu?unda mevcut lisans? ?nceden temizlemeyin. Sahip hesab?yla yeni kodu do?rudan **Lisans? etkinle?tir** alan?ndan uygulay?n. En son etkinle?tirilen lisans kayd? g?ncel kay?t olur. M??teri, plan, kullan?c? limiti, kalan g?n, yazma durumu ve ?zelliklerin beklenen de?erleri g?sterdi?ini do?rulay?n. Sonu? farkl?ysa ikinci bir kod denemeden durun.

### Mevcut lisans? temizleme

**Mevcut lisans? temizle**, yenileme veya geri alma d??mesi de?ildir. Sunucuda saklanan t?m lisans kay?tlar?n? a??k?a kald?rmak ve kurulum tarihine g?re deneme veya salt okunur durumunun yeniden hesaplanmas?n? kabul etmek istedi?inizde kullan?n. Onay penceresini okuyun. ??lemden sonra kasa verisinin, kullan?c?lar?n, oturumlar?n ve denetim kan?t?n?n korundu?unu, lisans modunun ise beklenen duruma ge?ti?ini do?rulay?n.

## Ekran Durumlar?

| Durum | Operat?r cevab? |
| --- | --- |
| Lisansl? | A??k ?zelliklerin sat?n al?nan planla e?le?ti?ini do?rulay?n. |
| Deneme | 30 g?nl?k s?reyi, 3 kullan?c? s?n?r?n? ve kilitli mod?lleri planlay?n. |
| Salt okunur | Kurtarma eri?imini koruyun ve de?i?iklikten ?nce salt okunur mod rehberini izleyin. |
| Kapasite kullan?labilir | Kullan?m? izleyin; i?lem gerekmez. |
| Kapasite dolmak ?zere | Yeni kullan?c? a?madan ?nce aktif kullan?c? say?s?n? ve sat?n al?nan limiti uzla?t?r?n. |
| Ya?am d?ng?s? uyar?s? | 60, 30 veya 7 g?nl?k yenileme e?i?ine g?re onay sahibini ve hedef tarihi belirleyin. |
| Aktivasyon do?rulanamad? | Tekrar tekrar denemeyin; hata metnini hassas ayr?nt?lar? ??kararak kaydedip ?zel destek isteyin. |
| Y?kleniyor | Kod girmeden ?nce k?sa s?re bekleyin; gerekirse sayfay? yenileyip sunucu eri?imini do?rulay?n. |

## ??lemden ?nce

- Eksik bir ?zelli?i ara?t?rmadan ?nce lisans durumunu, plan?, biti? tarihini, kapasiteyi ve a??k mod?lleri do?rulay?n.
- Lisans de?i?iminden ?nce Sahip hesab?yla oturum a?abildi?inizi ve yedek d??a aktarma yolunun eri?ilebilir oldu?unu do?rulay?n.
- Lisans kodlar?n?, imzal? lisans i?eri?ini ve m??teriye ait kullan?m haklar?n? herkese a??k destek kanallar?ndan uzak tutun.
- Kurumdaki de?i?iklik onay sahibini ve etkilenen payda?lar? belirleyin; yeni kodun haz?r oldu?unu do?rulay?n.
- De?i?iklikten sonra yaln?z rozetin rengini de?il, yazma durumunu ve plan yeteneklerini de yeniden kontrol edin.

## G?venli Kan?t

- Payla??labilir: lisans durumu, genel plan grubu, s?re penceresi, a??k ?zellik kategorisi ve hassas ayr?nt?lar? ??kar?lm?? hata kodu.
- Gizli kalmal?: lisans kodu, imzal? lisans i?eri?i, lisans? d?zenleyen tarafa ait ?zel imza materyali, m??teriye ait kullan?m haklar? ve m??teri ad?n? g?steren ekran g?r?nt?leri.
- Lisans kodu do?rulanam?yorsa, kapasite sat?n al?nan de?erle uyu?muyorsa veya kurtarma eri?imi belirsizse ?zel destek kullan?n.
- Ekran g?r?nt?s? gerekiyorsa m??teri ad? ve e-posta alanlar?n? tamamen maskeleyin; yaln?z k?rpmak yeterli de?ildir.

## Ne Zaman Durmal? ve Destek ?stemelisiniz

Lisans kodu do?rulanam?yorsa, etkinle?tirme sonras? lisans ba?ka bir m??teriyi g?steriyorsa, kapasite sat?n al?nan de?erle uyu?muyorsa veya salt okunur durumda kurtarma eri?imi belirsizse de?i?iklik yapmay? b?rak?n. Lisans kodunu ya da imzal? i?eri?i g?ndermeden g?r?n?r durumu, hassas ayr?nt?lar? ??kar?lm?? hata kodunu, genel plan grubunu ve s?re penceresini i?eren ?zel destek kayd? a??n.

## Operat?r Notlar?

Lisans kodu, ?zel lisans materyali, imzal? lisans i?eri?i veya m??teriye ait kullan?m haklar?n? g?steren ekran g?r?nt?s? yay?nlamay?n.

## ?lgili

- [Lisans ya?am d?ng?s?](license-lifecycle.md)
- [Lisans salt okunur mod rehberi](../../kb/tr/license-read-only.md)
- [?lk kurulum, Sahip kullan?c? ve lisans](first-run-owner-license.md)
