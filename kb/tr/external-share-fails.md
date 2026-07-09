# Dış paylaşım paketi açılamıyor

Offline share decrypter paketi reddediyor, passphrase hatası veriyor, metadata'yı kabul etmiyor veya açıldığı halde beklenen kayıtları göstermiyorsa bu makaleyi kullanın. Dış paylaşım paketleri sınırlı ve offline erişim için tasarlanmıştır; share'i yeniden oluşturmadan önce paket bütünlüğünü ve alıcı tarafındaki işlem akışını kontrol edin.

## İlk Müdahale

1. [Paylaşım](../../docs/tr/screen-sharing.md) ekranını açın ve paketin yalnız hedef kayıtlarla oluşturulduğunu doğrulayın.
2. Package JSON dosyasının editlenmediğini, chat uygulaması tarafından yeniden biçimlendirilmediğini, farklı formata çevrilmediğini veya dokümana yapıştırılmadığını kontrol edin.
3. Passphrase değerinin one-time display ekranından alındığını ve package dosyasıyla aynı kanaldan gönderilmediğini doğrulayın.
4. Expiry, maksimum açma sayısı ve paketin daha önce kullanılıp kullanılmadığını kontrol edin.
5. Recipient browser'ın Web Crypto desteklediğini ve local file execution engellemediğini doğrulayın.
6. Hâlâ açılmıyorsa eski share'i revoke edin ve daha dar kayıt setiyle yeni package oluşturun.

## Hata Tipleri

| Hata | Olası sebep | Operatör aksiyonu |
| --- | --- | --- |
| Wrong passphrase | Yazım, boşluk veya yanlış recipient mesajı | Passphrase'i private kanaldan tekrar gönderin; package yanında göndermeyin. |
| Tampered metadata | Package export sonrası değişmiş | Share'i revoke edip VaultPilot'tan yeniden oluşturun. |
| Expired package | Zaman penceresi geçmiş | Gerekçeli yeni expiry ile yeni package oluşturun. |
| Exhausted usage count | Maksimum açma hakkı dolmuş | Yeni paket vermeden önce alıcı tarafındaki işlem akışını kontrol edin. |
| Unsupported version | Eski decrypter veya ileri package formatı | Package ile aynı release context içindeki decrypter'ı kullanın. |

## Güvenli Kanıt

- Package oluşturma zamanı, expiry ve max-open policy.
- Decrypter error kategorisi ve browser ailesi.
- Paketin `.json` attachment olarak gönderilip gönderilmediği.
- Package içeriği değil, `<SHARE_ID>` gibi yer tutucu.
- Passphrase'in aynı kanaldan gönderilmediği bilgisi.

## Göndermeyin

Public support kanalına package JSON, passphrase, recipient identity, record name, decrypted content screenshot veya private link göndermeyin.

İlgili: [Paylaşım ekranı](../../docs/tr/screen-sharing.md), [Sharing ve offline decrypter](../../docs/tr/sharing-and-offline-decrypter.md), [Support evidence pack](../../docs/tr/support-evidence-pack.md), [Public issue redaction](public-issue-redaction.md).
