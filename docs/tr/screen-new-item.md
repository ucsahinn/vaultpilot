# Yeni Kayıt Ekranı

Üst çubuktaki `?` bu sayfayı Yeni kayıt ekranından açar. Hangi kayıt türünün oluşturulacağına ve ne kadar meta veri ekleneceğine karar verirken kullanın.

## Burada Ne Yapılır

- En dar kayıt türünü seçin: parola, API key, kimlik bilgisi, sertifika, güvenli not veya dosya.
- Aranabilir sahiplik ve sistem bağlamını meta veri alanlarına koyun; gizli değer yalnız şifreli değer alanında kalmalıdır.
- Etiketleri sadece sonraki inceleme veya rotasyon işine yarıyorsa ekleyin.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Taslak | Gizli değer girmeden önce sahiplik, kasa ve tür kararını bitirin. |
| Validation error | Secret alanlarını support metnine kopyalamadan etiketi ve zorunlu meta veriyi düzeltin. |
| Kayıt engellendi | Tekrar denemeden önce lisans, rol ve kasa erişimi durumunu kontrol edin. |

## İşlemden Önce

- Önce kayıt türünü seçin; tür değişikliği sonradan incelenmesi gereken alanları gizleyebilir.
- Hassas değer girmeden önce hedef kasayı ve sahibi doğrulayın.
- Örneklerde yer tutucu kullanın; production secret değerlerini public notlara yapıştırmayın.

## Güvenli Kanıt

- Paylaşılabilir: hedef kayıt türü, hedef kasa kategorisi, sahip rolü, validation code ve placeholder alan adları.
- Gizli kalmalı: secret değerleri, parola ile eşleşen kullanıcı adları, API key, sertifika materyali, dosya içeriği ve kopyalanmış form ekran görüntüleri.
- Örneklerde yer tutucu kullanın; public kanıta gerçek değer yapıştırıldıysa ilgili değeri rotate edin.

## Operatör Notları

Public örneklere test secret yapıştırmayın. `<SERVICE_NAME>`, `<ACCOUNT_NAME>` ve `<REDACTED_SECRET>` gibi yer tutucular kullanın.

## İlgili

- [Parolalar ekranı](screen-passwords.md)
- [API anahtarları ekranı](screen-api-keys.md)
- [Dosyalar ekranı](screen-files.md)
