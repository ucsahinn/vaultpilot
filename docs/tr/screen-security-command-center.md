# Güvenlik Komuta Merkezi Ekranı

Üst çubuktaki `?` bu sayfayı Güvenlik Komuta Merkezi ekranından açar. Kasa sağlığı, güvenlik duruşu, dizin durumu, sertifika riski, rotasyon hareketi ve güncelleme hazırlığı sinyallerini hızlıca okumak için kullanın.

## Burada Ne Yapılır

- En yeni olaya değil, en yüksek riskli karta bakarak başlayın.
- Skor düşüşlerini aksiyon çağrısı olarak değerlendirin; işlem yapmadan önce audit, lisans, 2FA, sertifika veya dizin sinyalinin kaynağını doğrulayın.
- Düzeltme için dashboard üzerindeki yönlendirme aksiyonlarıyla ilgili workspace'e geçin.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Sakin | Son yenileme zamanını doğrulayın ve planlı incelemeye devam edin. |
| Uyarı | Kayıt değiştirmeden önce ilgili ekrana geçin; kök sinyal görünür kalsın. |
| Bloke | Private support için redakte durum, etkilenen bileşen ve timestamp toplayın. |

## İşlemden Önce

- Sinyalin tüm sistemi mi, tek kasayı mı yoksa bir entegrasyonu mu etkilediğini ayırın.
- Aynı filtre bağlamını korumak için manuel gezinmek yerine ekrandaki yönlendirme aksiyonlarını kullanın.
- Birden fazla kart kırmızıysa önce kimlik doğrulama, lisans ve güncelleme engellerini ele alın.

## Güvenli Kanıt

- Paylaşılabilir: duruş kategorisi, etkilenen bileşen, redakte status, refresh penceresi ve gidilecek ekran.
- Gizli kalmalı: ham dashboard sayıları, hostname, kullanıcı adı, vault adı, tenant timing ve internal context gösteren ekran görüntüleri.
- Birden fazla kırmızı kart auth, lisans veya update engeli gösteriyorsa ve gerçek ortam kanıtı gerekiyorsa private support kullanın.

## Operatör Notları

Bu ekran final rapor değil, komuta yüzeyidir. Host adı, kullanıcı, vault adı, private count veya iç zamanlama gösterebilecek değerleri public issue içine kopyalamayın.

## İlgili

- [Denetim ve güvenlik duruşu](audit-and-security-posture.md)
- [Güvenlik ve güven modeli](security-and-trust-model.md)
- [Operasyon runbook](operator-runbook.md)
