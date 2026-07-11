# G?venlik Ekran?

?st ?ubuktaki `?` simgesi bu yard?m? **G?venlik** ekran? a??kken getirir. Bu ekran, VaultPilot'?n g?venlik sinyallerini tek bir puana indirgemek yerine hangi kayd?n, davran???n veya eri?im olay?n?n inceleme istedi?ini g?sterir. B?t?n sistem rolleri ekran? a?abilir; sorgu i?eri?i, ayr?nt?ya ge?i? ve eylemler role g?re daral?r.

Dashboard kartlar? kasa, denetim, lisans, g?ncelleme, entegrasyon ve i?lem sorgular?ndan ?retilir. Her g?rsel etkile?imli de?ildir: d??me bi?imindeki sat?r ve metrikler hedef ekrana gider; grafik ?ubuklar? ve **Risk da??l?m?** yaln?z okunur. Ekran?n tek **Dashboard ara?lar?** men?s? dok?man? a?ar, veriyi yeniler ve d?zenleme modunu y?netir. Widget ba??na men? yoktur; gizleme ve s?ralama yaln?z d?zenleme modunda g?r?n?r.

## Bu Ekran? Nas?l Okumal?s?n?z

- **G?venlik kapsam?:** Komuta Merkezi skorunun on fakt?r?n? g?sterir: 2FA, lisans, eklenti, g?ncelleme, parola s?z?nt?s?, AD riski, sertifika sona-erme tarihi meta verisinin eksiksizli?i, i?lem ge?mi?i, dizin sa?lay?c? e?itleme hatas? ve kasa i?eri?i. Sertifika sat?r? ger?ek ge?erlilik testi, dizin sat?r? genel ba?lant? testi de?ildir. Her sat?r kazand???/toplam a??rl??? g?sterir ve kaynak ekran?na gider.
- **S?z?nt? kontrol?:** Parolalar? bilinen s?z?nt?da g?r?len, temiz ve hen?z kontrol edilmemi? olarak ay?r?r.
- **Risk da??l?m?:** ?? farkl? hesab? yan yana koyar: **Sa?l?kl? sinyal**, sa?l?kl? skor fakt?rlerini; **?zlenecek konu** ve **Kritik i?lem** ise ton normalizasyonundan sonraki ?nerileri sayar. Bunlar tek bir olay/sinyal n?fusu de?ildir; segmentlere bas?lmaz.
- **Davran?? analizi:** ?ubuk grafik eri?im, oturum ve y?netim olaylar?n? kar??la?t?r?r. Yan?ndaki en fazla be? **Riskli eri?imler** sat?r? t?klanarak ilgili Denetim Kayd? olay?na gidilir.
- **Denetim ?zeti:** En son alt? olay? akt?r, hedef, risk ve zamanla g?sterir. Yaln?z **Olay** s?tunundaki d??me ilgili denetim olay?n? a?ar.
- **Eri?im trendi:** Son yedi g?ndeki kilit a?ma, g?r?nt?leme, kopyalama, doldurma ve entegrasyon e?itleme olaylar?n? sayan salt okunur grafiktir; g?n ?ubuklar? zaman filtresi a?maz.

## Yetki ve Veri Ko?ullar?

Sahip, Y?netici, Denet?i ve Kullan?c? ekran? a?abilir; ancak baz? sistem sorgular? ve ayr?nt? hedefleri yetkisiz rolde bo?, k?s?tl? veya pasif kal?r. Denet?i kasa kay?tlar?n? a?amaz. Gizli kayd? g?stermek veya kopyalamak i?in Denet?i d???ndaki uygun rol ve okunabilir kasa eri?imi; kasa kayd? yazmak i?in ayr?ca aktif kasada **Editor** ya da **Manager** ?yeli?i ve yaz?labilir lisans gerekir. Sistem hedefleri kendi rol kap?lar?n? uygular.

## Uygulanabilir ?nceleme Ak??lar?

### S?z?nt?da g?r?len parolalar? ele alma

1. **S?z?nt? kontrol?** i?indeki s?z?nt? say?s?n?, halka grafi?ini veya ilgili durum sat?r?n? se?in.
2. A??lan Parolalar ekran?nda haz?r s?z?nt? filtresini ve kay?t sahibini do?rulay?n.
3. Parolay? ?nce ait oldu?u sistemde de?i?tirin, ard?ndan VaultPilot kayd?n? g?ncelleyin ve kontrol? yeniden ?al??t?r?n.

Beklenen sonu?, eski de?erin ge?ersiz kalmas? ve yeni kontrol?n temiz sonu? vermesidir. Hedef sistemde de?i?iklik yap?lam?yor veya kay?t sahibi belli de?ilse kasa de?erini tek ba??na de?i?tirip i?i kapatmay?n.

### Beklenmeyen eri?im art???n? inceleme

Eri?im trendindeki y?kseli?in hangi g?ne denk geldi?ini ve toplam? belirleyin. Grafik olay t?r?n? ay?rmaz ve ?ubuklar t?klanmaz. **Denetim ?zeti** yaln?z son alt? olay? g?sterdi?inden ayr?nt?l? zaman ve eylem filtresi i?in sol gezintiyle Denetim Kayd??na gidin; belirli bir olay i?in **Riskli eri?imler** sat?r?n? veya **Olay** d??mesini kullan?n. Beklenen sonu? art???n onayl? ?al??mayla e?le?mesidir; e?le?miyorsa oturum ve hesap g?venli?ini ?zel olay s?recinde inceleyin.

### Kritik risk ile denetim olay?n? e?le?tirme

**Risk da??l?m?** yaln?z ?zet oldu?u i?in kritik segmentten ayr?nt? a??lmaz. Kritik say?y? not edin; **Davran?? analizi > Riskli eri?imler** sat?rlar?ndan veya **Denetim ?zeti** olay d??mesinden kayna?a gidin. Kartlar?n ayn? olay? anlatt???n? varsaymay?n; redakte zaman, i?lem t?r? ve hedef s?n?f?n? kar??la?t?r?n. ?eli?ki varsa yeni de?i?iklik yapmadan veriyi bir kez yenileyin.

## Ekran Durumlar?

| Durum | Operat?r cevab? |
| --- | --- |
| Y?kleniyor | Widget'lar tamamlanana kadar puan, oran veya trend yorumlamay?n. |
| Sa?l?kl? | Kapsam oran?n? ve kontrol bekleyen kay?tlar? do?rulay?p rutin incelemeyi kaydedin; ekranda tek bir k?resel ?son yenileme? zaman? yoktur. |
| ?zlenecek | Kart? a??n, hedef kayd? veya olay? do?rulay?n ve sorumlu takip i?ini belirleyin. |
| Kritik | ?nce etkilenebilecek eri?imi s?n?rland?r?n; ard?ndan kay?t ve denetim ayr?nt?s?n? private s?re?te inceleyin. |
| Bo? | Ger?ekten olay olmad???n? s?ylemeden ?nce kasa, tarih aral??? ve widget g?r?n?rl???n? kontrol edin. |
| Yenileme sonras? de?i?miyor | K?resel zaman damgas? aramay?n; kaynak widget??n sorgusunu ve hedef ekran verisini kontrol edin. |
| Yetki k?s?tl? | Drill-down a??lam?yorsa rol? ve kasa ?yeli?ini do?rulay?n; daha geni? yetkiyi do?rudan kullan?c?ya vermeyin. |
| Hata | Hata metnini ve zaman? koruyun; k?smi widget verisini tam tablo gibi raporlamay?n. |

## ??lemden ?nce

- Widget'?n hangi zaman aral???n? ve veri kayna??n? ?zetledi?ini kontrol edin.
- S?z?nt? sonucu ile risk etiketini, eri?im trendi ile denetim olay?n? birbirinin yerine kullanmay?n.
- Dashboard'dan a??lan filtreyi temizlemeden ?nce hangi sinyalin sizi oraya getirdi?ini not edin.
- Kay?t de?i?ikli?i i?in aktif kasa rol?n? ve lisans?n yaz?labilir oldu?unu do?rulay?n.
- D?zenleme modunda widget gizlemenin veriyi veya riski silmedi?ini unutmay?n; gizli bile?eni yine bu modda geri y?kleyin.

## G?venli Kan?t

- **Payla??labilir:** genel risk seviyesi, sinyal kategorisi, redakte olay t?r?, zaman aral???, kontrol?n son ?al??ma zaman? ve izlenen ??z?m ad?mlar?.
- **Gizli kalmal?:** kullan?c? ve kasa adlar?, ger?ek kay?t ba?l?klar?, URL'ler, dahili host/etki alan? bilgileri, tam eri?im zaman ?izelgesi ve gizli de?er g?r?nen her ekran g?r?nt?s?.
- S?z?nt? kontrol?nde bulunan de?er, parola ?rne?i olarak bile payla??lmaz. Public alana d??en ger?ek bir parola ?nce ait oldu?u sistemde de?i?tirilmelidir.

## Ne Zaman Durmal? veya Y?kseltmeli

Kritik sinyal yenilemeden sonra kaybolmuyorsa, eri?im trendi ile denetim kay?tlar? uyu?muyorsa, bir?ok kullan?c? veya kasa etkileniyorsa ya da dashboard verisi s?rekli bayat kal?yorsa g?venlik sorumlusuna ve gerekirse private support'a y?kseltin. S?r?m, saat dilimiyle zaman, kart ad?, redakte hata ve denedi?iniz ad?mlar yeterlidir.

## Operat?r Notlar?

Bu dashboard bir inceleme y?zeyidir; olay?n kayna?? ilgili kay?t veya Denetim Kayd?'ndad?r. Sa?l?kl? renk tek ba??na t?m parolalar?n kontrol edildi?ini g?stermez. ?zellikle ?kontrol edilmemi?? kay?t say?s?n? s?f?r g?rmeden s?z?nt? kapsam?n? tamamlanm?? saymay?n.

## ?lgili

- [G?venlik ve g?ven modeli](security-and-trust-model.md)
- [Denetim ve g?venlik duru?u](audit-and-security-posture.md)
- [G?venlik Komuta Merkezi ekran?](screen-security-command-center.md)
- [Giri? g?venli?i ekran?](screen-sign-in-security.md)
