# Paylaşım Ekranı

Üst çubuktaki `?` bu sayfayı Paylaşım ekranından açar. Seçili kayıtları veya external package'ları süre sonu, alıcı ve kullanım limitiyle paylaşmak için kullanın.

## Burada Ne Yapılır

- Alıcının işi için gereken minimum kayıt setini paylaşın.
- External package oluşturmadan önce süre sonu ve kullanım limiti belirleyin.
- Alıcı yolunu private doğrulayın; passphrase ile paket dosyasını aynı kanaldan göndermeyin.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Taslak share | Paket oluşturmadan önce kayıtları, alıcıyı ve süre sonu bilgisini doğrulayın. |
| Aktif paylaşım | Kullanım durumunu takip edin ve iş bitince erişimi iptal edin. |
| Açma hatası | Yeni paket göndermeden önce dış paylaşım KB'sini kullanın. |

## İşlemden Önce

- Göndermeden önce alıcıyı, kayıt setini, expiry değerini ve maksimum açma limitini doğrulayın.
- İsteği çözen en dar paketi kullanın; kolaylık için tüm vault bağlamını paylaşmayın.
- Ekrandan ayrılmadan önce handoff amacını ve revoke beklentisini kaydedin.

## Güvenli Kanıt

- Paylaşılabilir: paket durumu, expiry policy, maksimum açma policy'si, hata kodu ve redakte alıcı tipi.
- Gizli kalmalı: package JSON, passphrase, alıcı secret'ları, korunan dosya adları ve çözülmüş içerik.
- Delivery proof gerçek alıcı adresi, müşteri etiketi veya paket metadata'sı içeriyorsa private support kullanın.

## Operatör Notları

Public issue paylaşım akışını anlatabilir; paket içeriği, alıcı kimliği, passphrase veya redakte edilmemiş link içeremez.

## İlgili

- [Paylaşım ve offline decrypter](sharing-and-offline-decrypter.md)
- [Dış paylaşım paketi açılamıyor KB](../../kb/tr/external-share-fails.md)
- [Destek kanıt paketi](support-evidence-pack.md)
