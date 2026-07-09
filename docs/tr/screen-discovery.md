# Discovery Ekranı

Üst çubuktaki `?` bu sayfayı Discovery ekranından açar. Onaylı ağ, TLS ve dosya maruziyeti kontrollerini çalıştırıp doğrulanmış bulguları kasaya içe aktarmak için kullanın.

## Burada Ne Yapılır

- Yalnız onaylı kapsamı ve yol değerlerini çalıştırın.
- İçe aktarmadan önce bulgu güven düzeyini inceleyin.
- Yalnız VaultPilot'a ait, sahibi belli materyali içe aktarın.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Hazır | Tarama başlatmadan önce kapsam onayını doğrulayın. |
| Bulgu var | İçe aktarmadan önce güven düzeyini ve sahip bilgisini inceleyin. |
| Kapsam reddedildi | Taramayı genişletmeyin; onaylı kapsamı düzeltin veya durun. |

## İşlemden Önce

- Ağ aralığı, dosya yolu ve TLS hedeflerinin tarama için açıkça onaylandığını doğrulayın.
- Her bulguyu otomatik içe aktarım değil, incelenecek kanıt olarak ele alın.
- Yalnız sahibi, hedef kasası ve düzeltme amacı net olan öğeleri içe aktarın.

## Güvenli Kanıt

- Paylaşılabilir: bulgu kategorisi, güven düzeyi, redakte yol veya host biçimi ve kanıt hash'i.
- Gizli kalmalı: ham dosya, maskesiz yol, iç host adı, düz metin kesiti, token, private key ve veritabanı export'u.
- İçe aktarma yalnız sahiplik ve hedef kasa netleşince yapılır; public tartışma bulgu özeti seviyesinde kalmalıdır.

## Operatör Notları

Discovery kanıtı çoğu zaman iç host, dosya adı, sertifika parmak izi veya hassas değer benzeri kesit içerir. Private support dışına çıkmadan önce redakte edin.

## İlgili

- [Discovery rehberi](discovery.md)
- [Discovery bulgu inceleme KB](../../kb/tr/discovery-finding-review.md)
- [Public issue redaction KB](../../kb/tr/public-issue-redaction.md)
