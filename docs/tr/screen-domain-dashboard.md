# Etki Alanı Dashboard Ekranı

Üst çubuktaki `?` bu sayfayı Etki Alanı dashboard ekranından açar. Active Directory kaynaklı kimlik bilgilerine, eşitleme ağacı sağlığına veya dizin nesnesi sayılarına güvenmeden önce bu ekranı kullanın.

## Burada Ne Yapılır

- Eşitlenmiş kullanıcı, grup veya kimlik bilgisini incelemeden önce DC Agent bağlantısını doğrulayın.
- Bayat sync timestamp değerlerini, ajan, URL ve token yolu kontrol edilene kadar operasyon riski sayın.
- Directory sayılarını public rapor değeri olarak değil, sağlık sinyali olarak kullanın.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Eşitleme tamam | Kimlik bilgisi incelemesine geçmeden önce son eşitleme yaşını doğrulayın. |
| Bayat | Dizin kaynaklı kayıtları düzenlemeden önce agent servis durumunu kontrol edin. |
| Unauthorized | Provider token'ını döndürün ve mevcut provider kartındaki repair komutunu kullanın. |

## İşlemden Önce

- Kayıtların bayat olduğunu varsaymadan önce son başarılı eşitleme zamanını kontrol edin.
- Provider sağlığını, seçili obje sayılarını ve ajan durumunu birlikte okuyun.
- Bu dashboard üzerinden imported credential düzeltmeyin; değişikliğin sahibi olan provider veya kayıt görünümüne gidin.

## Güvenli Kanıt

- Paylaşılabilir: provider sağlık kategorisi, son eşitleme yaşı, kategori bazlı seçili obje sayısı ve redakte hata kodu.
- Gizli kalmalı: domain adı, distinguished name, OU path, bind account, agent token ve internal directory tree ekran görüntüleri.
- Token repair, bind failure veya directory scope kanıtı gerçek tenant değerleri gerektiriyorsa private support kullanın.

## Operatör Notları

Domain adı, distinguished name, OU path, bind account, agent token veya internal directory tree ekran görüntüsü yayınlamayın.

## İlgili

- [Active Directory ajanı](active-directory-agent.md)
- [Active Directory kayıtları ekranı](screen-active-directory-records.md)
- [DC Agent sorun giderme](../../kb/tr/dc-agent-service.md)
