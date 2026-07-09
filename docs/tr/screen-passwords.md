# Parolalar Ekranı

Üst çubuktaki `?` bu sayfayı Parolalar ekranından açar. Onaylı sistemlere, paylaşılan operasyon hesaplarına veya bireysel servis hesaplarına ait giriş kayıtları için kullanın.

## Burada Ne Yapılır

- Gösterme veya kopyalama öncesi URL, sahip, kullanıcı adı, kategori ve etiketleri doğrulayın.
- Gösterme ve kopyalama aksiyonlarını bilinçli kullanın; ikisi de yararlı denetim kanıtı bırakmalıdır.
- Zayıf, bayat veya sızmış kayıtları önce sahip sistem içinde döndürün, sonra kasa kaydını güncelleyin.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Boş sonuç | Kayıt yok demeden önce filtreleri temizleyin. |
| Rotation gerekli | Değeri değiştirmeden önce sahip ve bağımlılıkları doğrulayın. |
| Erişim reddedildi | Normal sahiplik akışı üzerinden kasa ataması isteyin. |

## İşlemden Önce

- Kopyalama veya doldurma öncesi seçili kasa, URL ve kullanıcı adının birlikte doğru olduğunu doğrulayın.
- Başkalarının kullandığı bir kaydı düzenlemeden önce sahip, son inceleme ve rotasyon sinyallerine bakın.
- Notlarda düz metin değer yerine kaydın kullanım rolünü anlatın.

## Güvenli Kanıt

- Paylaşılabilir: kayıt kategorisi, kasa atama durumu, rotasyon durumu, access-denied code ve redakte owner rolü.
- Gizli kalmalı: düz metin parola, hedef URL ile eşleşen kullanıcı adı, değer gösteren ekran görüntüsü, autofill içeriği ve pano dökümü.
- Public alana düşen her parola değerini compromised kabul edin ve önce sahip sistem üzerinden rotate edin.

## Operatör Notları

Düz metin parola, değer gösteren ekran görüntüsü, tarayıcı otomatik doldurma içeriği veya pano dökümü yayınlamayın.

## İlgili

- [Güvenlik ve güven modeli](security-and-trust-model.md)
- [Tarayıcı eklentisi ekranı](screen-browser-extension.md)
- [Operasyon runbook](operator-runbook.md)
