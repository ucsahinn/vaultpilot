# Rotasyon Ekranı

Üst çubuktaki `?` bu sayfayı Rotasyon ekranından açar. Parola, kimlik bilgisi ve API key rotasyon planını sahiplik ve denetim kanıtı kaybetmeden yapmak için kullanın.

## Burada Ne Yapılır

- Rotasyon işini seçmeden önce risk ve yaşa göre sıralayın.
- Kimlik bilgisini değiştirmeden önce sahip, sistem, kasa ve bağımlı entegrasyonu doğrulayın.
- Olay kaynaklı emergency rotation gerekiyorsa nedenini kayda bağlayın.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Takvimde | Owner ve sonraki rotasyon tarihi bilgisini güncel tutun. |
| Gecikmiş | Kayıt sahibiyle kontrollü change window planlayın. |
| Bloke | Kör rotasyon yapmayın; önce sahip, bağımlılık ve denetim bağlamı toplayın. |

## İşlemden Önce

- Rotasyon hedefinin hâlâ sahibi ve geri dönüş yolu olduğunu doğrulayın.
- Aktif entegrasyonu etkileyebilecek credential değişmeden önce son kullanım sinyallerini inceleyin.
- Çalıştırmadan önce bakım penceresini ve etkilenen kasaları kaydedin.

## Güvenli Kanıt

- Paylaşılabilir: rotasyon durumu, yaş aralığı, etkilenen sistem kategorisi, sahip rolü ve redakte kontrol sonucu.
- Gizli kalmalı: eski değer, yeni değer, recovery code, share passphrase, hedef kullanıcı adı ve müşteri sistemini tanımlayan dependency detayı.
- Emergency rotation kanıtı incident context veya secret taşıyan ekran görüntüsü içeriyorsa private support kullanın.

## Operatör Notları

Rotation evidence iş sistemi ve kontrol sonucunu anlatmalıdır. Eski veya yeni değerler, recovery code, share passphrase ya da redakte edilmemiş ekran görüntüsü yayınlanmaz.

## İlgili

- [Operasyon runbook](operator-runbook.md)
- [Parolalar ekranı](screen-passwords.md)
- [API anahtarları ekranı](screen-api-keys.md)
