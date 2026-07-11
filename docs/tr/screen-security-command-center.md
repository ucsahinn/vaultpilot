# G?venlik Komuta Merkezi Ekran?

?st ?ubuktaki `?` simgesi bu yard?m? G?venlik Komuta Merkezi a??kken getirir. Buras? VaultPilot'ta ??nce nereye bakmal?y?m?? sorusunun cevab?d?r: g?venlik skoru, ?ncelikli ?neriler, sunucu haz?rl??? ve operasyon sinyalleri ayn? ?al??ma alan?nda bir araya gelir. B?t?n sistem rolleri ekran? a?abilir; g?r?lebilen veri ve hedef i?lemler role g?re daral?r. Tek ba??na olay raporu ya da de?i?iklik onay? de?ildir.

Komuta Merkezi veriyi de?i?tirmekten ?ok do?ru ayr?nt? ekran?na g?t?r?r. Bir ?neriye veya fakt?re bast???n?zda Parolalar, Active Directory kay?tlar?, Giri? G?venli?i, Entegrasyonlar, Lisans ya da G?ncelleme Merkezi a??l?r; uygun oldu?unda ilgili filtre de haz?rlan?r.

## Ekranda Neler G?r?rs?n?z

- **G?venlik skoru:** 2FA, lisans modu, taray?c? eklentisi, Update Center, parola s?z?nt?s? kontrol?, Active Directory riski, sertifikalardaki sona-erme tarihi meta verisinin eksiksizli?i, ba?ar?s?z i?lemler, dizin sa?lay?c?lar?n?n bildirdi?i e?itleme hatalar? ve kasa i?eri?i olmak ?zere on a??rl?kl? fakt?rden hesaplan?r. Sertifika fakt?r? ger?ek ge?erlilik/sona erme testi, dizin fakt?r? genel ba?lant? testi de?ildir. Skoru tek ba??na ?g?venli? karar? saymay?n.
- **Kritik ve izlenecek ?neriler:** Ana y?zey iki kritik ve iki izlenecek sat?r g?sterir. **Daha fazla ?neri (n)**, kalan s?ral? kuyru?u a?ar; buradaki sat?rlar da do?rudan hedef ekrana gider.
- **Skor kaynaklar? ve dashboard b?l?mleri:** G?venlik, etki alan?, sertifika ve rotasyon ekranlar?na do?rudan ge?i? sa?lar.
- **G?ncel operasyon sinyalleri:** Dosya kotas?, i?lem durumu ve g?ncelleme haz?rl??? gibi canl? ?zetleri g?sterir.
- **Ekran ara?lar?:** Canl? veriyi yenileyebilir, ilgili dok?man? a?abilir ve dashboard g?r?n?m?n? y?netebilirsiniz.

## Yetki ve ?n Ko?ullar

Sahip, Y?netici, Denet?i ve Kullan?c? ekran? a?abilir; fakat baz? sistem sorgular?, hedef ekranlar ve eylemler yetkisiz rolde bo?, k?s?tl? veya pasif kal?r. Kasa kay?tlar?na y?nlenen ayr?nt?lar i?in kilidi a??lm?? kasa ve gizli kay?t kullanmaya izin veren sistem/kasa rol? gerekir; Denet?i kasa i?eriklerini a?amaz. Salt okunur lisans kasa kayd? olu?turan veya de?i?tiren i?lemleri kapat?r. Lisans ve Entegrasyonlar yaln?z Sahibe, Sunucu Ayarlar? okuma Sahip/Y?netici/Denet?iye, sunucu de?i?iklikleri ise Sahibe ?zg? kap?lar uygulayabilir.

## ?nerilen ?al??ma Ak??lar?

### G?nl?k g?venlik kontrol?

1. Skoru, kazan?lan/toplam a??rl??? ve a??k ?neri say?s?n? birlikte okuyun; bu ekranda ba??ms?z bir ?skor g?ncellik? i?areti yoktur.
2. **Kritik** b?l?m?ndeki ilk sat?r? a??n; VaultPilot ilgili ekran? ve varsa haz?r filtreyi getirir.
3. Ayr?nt? ekran?nda sebebi do?rulay?n, i?lemi orada tamamlay?n ve Komuta Merkezi'ne d?n?p yenileyin.

Beklenen sonu?, ?nerinin sa?l?kl? duruma ge?mesi veya yap?lacak i?in a??k?a sahiplenilmesidir. Yenilemeden sonra ayn? uyar? s?r?yorsa art arda k?r de?i?iklik yapmay?n; kaynak ekran?ndaki hata ve zaman bilgisini inceleyin.

### D??en skorun nedenini bulma

En d???k veya uyar? tonundaki skor kayna??n? se?in. 2FA, lisans, eklenti, g?ncelleme, s?z?nt?, AD riski, sertifika sona-erme meta verisi, i?lem ge?mi?i, dizin sa?lay?c? hatas? ve kasa i?eri?i nedenlerini birbirinden ay?r?n; hedef ekranda veriyi do?rulay?n. Sonu? tek bir somut kontrole ba?lanam?yorsa burada durun ve Sunucu Ayarlar?/??lemler ?zerinden sistem sa?l???n? kontrol edin.

### Bir ?neriyi operasyon i?ine d?n??t?rme

?neriyi a??n, hedef ekrandaki kayd? veya bile?eni do?rulay?n, sorumluyu ve yap?laca?? zaman? kurum i?i de?i?iklik kayd?na ekleyin. Komuta Merkezi ?nerilerinde gizleme veya kapatma d??mesi yoktur; tamamlanma ?l??t? kaynak kontrolde d?zelme ve sonraki yenilemede ?nerinin kuyruktan ??kmas?d?r.

## Ekran Durumlar?

| Durum | Operat?r cevab? |
| --- | --- |
| Y?kleniyor | Kartlar tamamlanana kadar skor veya say? ?zerinden karar vermeyin; uzun s?rerse bir kez yenileyin. |
| 82?100 | Skor ye?il banttad?r; yine de a??k ?neri say?s?n? ve her fakt?r?n a??rl???n? kontrol edin. |
| 62?81 | Skor uyar? band?ndad?r; en y?ksek puan etkili sat?r? hedef ekran?nda do?rulay?n. |
| 0?61 | Skor kritik banttad?r; do?rudan eri?im riskini ?nce s?n?rlay?n ve olay? ?zel s?rece ta??y?n. |
| Daha fazla ?neri | G?r?nmeyen kuyru?u a??n; ilk d?rt sat?r b?t?n a??k i?leri temsil etmeyebilir. |
| Haz?rl?k sinyali eksik | Profil, aktif kasa, 2FA, lisans, eklenti veya Update Center hedefini a??p kayna??nda do?rulay?n. |
| Yetki k?s?tl? | Hedef ekran ya da eylem pasifse rol? ve kasa ?yeli?ini normal yetkilendirme s?recinden do?rulay?n. |
| Hata | Mesaj?, zaman? ve etkilenen bile?eni kaydedin; s?rekli yenileyerek ilk kan?t? kaybetmeyin. |

## ??lemden ?nce

- Uyar?n?n tek bir kasay? m?, kullan?c? oturumunu mu, lisans? m? yoksa sunucu bile?enini mi etkiledi?ini belirleyin.
- Ekrandaki y?nlendirmeyi kullan?n; s?z?nt? ve risk filtresi bu yolla hedef ekrana ta??n?r.
- Bir **kasa kayd?n?** yazmadan ?nce aktif kasa rol?n?n **Editor** veya **Manager** oldu?unu ve lisans?n salt okunur olmad???n? do?rulay?n. Sunucu/lisans/entegrasyon hedeflerinde kasa rol? yerine hedef ekran?n kendi sistem rol? ve lisans kurallar? ge?erlidir.
- Birden fazla kritik sinyal varsa ?nce 2FA ve bilinen s?z?nt? gibi do?rudan eri?im risklerini ele al?n.
- Komuta Merkezi say?s?n? nihai denetim kan?t? saymay?n; ilgili kay?t, denetim olay? veya i?lem sonucunu do?rulay?n.

## G?venli Kan?t

- **Payla??labilir:** genel skor band?, ?neri kategorisi, etkilenen VaultPilot bile?eni, redakte hata kodu, g?zlem zaman? ve y?nlendirilen ekran?n ad?.
- **Gizli kalmal?:** kullan?c? ve kasa adlar?, ger?ek kay?t ba?l?klar?, dahili etki alan? ve sunucu adlar?, m??teri say?lar?, eri?im zaman ?izgileri ve gizli de?er g?sterebilecek ekran g?r?nt?leri.
- G?rsel gerekiyorsa yaln?z ilgili kart? al?n; gezinme, kullan?c?, host ve kay?t ba?lam?n? maskeleyin. Ortam tamamen anonimle?tirilemiyorsa public issue yerine private support kullan?n.

## Ne Zaman Durmal? veya Y?kseltmeli

Ayn? kritik sinyal do?rulanm?? bir d?zeltmeden sonra geri geliyorsa, skor kaynaklar? y?klenmiyorsa, denetim verisi ile dashboard ?zeti ?eli?iyorsa veya risk birden fazla kullan?c?y? etkiliyorsa olay? kurum i?i g?venlik sorumlusuna ta??y?n. Destek paketine gizli de?er de?il; saat dilimiyle zaman, s?r?m, bile?en, izlenen ad?mlar ve redakte hata bilgisi ekleyin.

## Operat?r Notlar?

Komuta Merkezi karar vermeyi h?zland?r?r; ayr?nt? ekranlar?n?n yerine ge?mez ve ?neri kartlar?n? gizleme denetimi sunmaz. Sonucu her zaman hedef ekranda ve gerekiyorsa Denetim Kayd?'nda do?rulay?n.

## ?lgili

- [Denetim ve g?venlik duru?u](audit-and-security-posture.md)
- [G?venlik ve g?ven modeli](security-and-trust-model.md)
- [G?venlik Dashboard ekran?](screen-security-dashboard.md)
- [Operasyon runbook](operator-runbook.md)
