# Güvenli Notlar Ekranı

Üst çubuktaki `?` bu sayfayı Güvenli notlar ekranından açar. Password, API key, certificate veya file kaydına uymayan hassas operasyon metinleri için kullanın.

## Burada Ne Yapılır

- Notları kısa, yapılandırılmış ve sahibi belli tutun.
- Gelecekte inceleme gerekecek bilgiler için uzun serbest metin yerine alan ve etiket kullanın.
- Kimlik bilgisi değerlerini not içine saklamak yerine doğru kayıt türüne taşıyın.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Taslak not | Genel prosedür metnini kaydetmeden önce kazara girilmiş kimlik bilgilerini çıkarın. |
| İnceleme zamanı | Notun hâlâ sahibi ve güncel amacı olduğunu doğrulayın. |
| Çok geniş | İlgisiz prosedürleri daha güvenli access control için ayrı kayıtlara bölün. |

## İşlemden Önce

- İçeriğin not olarak mı kalması gerektiğini yoksa typed secret kaydı mı olması gerektiğini seçin.
- Korunan metni açığa çıkarmadan gelecekteki inceleme için yeterli etiket ve sahiplik metadata'sı ekleyin.
- Hassas değer içermeyen runbook'ları dokümana taşıyın; kasada yalnız korunan operasyon detayları kalsın.

## Güvenli Kanıt

- Paylaşılabilir: not kategorisi, sahip/review durumu, etiket biçimi ve redakte validation concern.
- Gizli kalmalı: müşteri bağlamı taşıyan not başlığı, not içeriği, iç host adı, credential, recovery detayı ve müşteriye özel ifade.
- Public yeniden kullanılabilir prosedür metnini dokümana taşıyın; korunan operasyon detayları kasada kalsın.

## Operatör Notları

Secure note'lar encrypted olsa da public support evidence içinde not başlığı, içerik, iç host adı ve müşteriye özel ifade redakte edilmelidir.

## İlgili

- [Güvenlik ve güven modeli](security-and-trust-model.md)
- [Destek kanıt paketi](support-evidence-pack.md)
- [Public issue redaction KB](../../kb/tr/public-issue-redaction.md)
