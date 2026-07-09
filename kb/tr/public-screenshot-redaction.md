# Public Ekran Görüntüsü Redaksiyonu

Public issue, pull request, README, rehber, KB makalesi, Chrome Web Store listing veya social preview için hazırlanan screenshot hassas bilgi içerebilir şüphesi varsa bu makaleyi kullanın.

## İlk Kontroller

1. Görseli yalnız thumbnail olarak değil, full-size açın.
2. Görünen her tablo satırı, drawer, modal, toast, browser bar, tab başlığı, dosya adı, terminal prompt, bildirim ve footer alanını kontrol edin.
3. Gerçek müşteri verisi, hostname, kullanıcı adı, e-posta, secret başlığı, parola, token, lisans değeri, private materyale bağlı hash, support ticket ID, account adı, database, yedek, sertifika, private key, local path ve log arayın.
4. Verinin synthetic olduğunu ve public screenshot standartlarına uyduğunu doğrulayın.

## Hassas Veri Görünüyorsa

Screenshot'ı public olarak commit etmeyin, stage etmeyin, yüklemeyin veya eklemeyin.

| Bulgu | Aksiyon |
| --- | --- |
| Gerçek müşteri, host, kullanıcı, e-posta, internal URL, database, yedek veya support ticket verisi | Screenshot'ı sentetik veri kullanan capture ile değiştirin. Güvensiz görseli git ve public issue dışında tutun. |
| Token, parola, vault kaydı, secret başlığı, private key, sertifika private materyali veya lisans private materyali | Public işlemeyi durdurun. Private owner review edene ve gerekiyorsa rotate veya revoke edene kadar değeri compromised kabul edin. |
| Browser account, dashboard, profil, bildirim veya local klasör verisi | Temiz dokümantasyon profili ve kırpılmış uygulama frame'i ile yeniden capture alın. |
| Fixture olarak görünen release asset hash'i, boyutu, dosya adı veya manifest değeri | Açıklama metninde örnek olduğunu belirtin veya kaldırın. Yayındaki release doğrulaması release asset doğrulama rehberinden yapılmalıdır. |

## Gönderilebilecek Güvenli Kanıt

- Screenshot dosya adı ve görselin ekleneceği sayfa.
- Component ve dokümantasyon sürümü.
- Hassas değerleri `<REDACTED>` ile değiştirilmiş ekran açıklaması.
- Yeni görselin sentetik tenant, user, host, vault ve finding verisi kullanıp kullanmadığı.
- Validation fail ettiyse komut ve exact validator mesajı.

## Public Olarak Gönderilmemesi Gerekenler

- Güvensiz screenshot.
- Çevresindeki müşteri, account veya local operator context'i hâlâ gösteren kırpılmış görseller.
- Raw log, database, yedek, sertifika paketi, vault export, browser profil verisi, support export veya account dashboard screenshot'ı.
- Token, parola, lisans, private key, cookie, session, recovery veya share passphrase değeri.

## Recovery Yolu

1. Private incident review için gerekmiyorsa güvensiz local candidate görseli review setinden çıkarın.
2. Sentetik veri kullanan izole dokümantasyon çalışma ortamı'ından replacement capture alın.
3. Dosya adı değiştiyse ilgili rehberi, görsel tablosunu ve screenshot manifestini güncelleyin.
4. Şunları çalıştırın:

```powershell
npm run validate
git diff --check
gitleaks detect --no-git --redact --verbose --source .
```

Güvensiz görsel zaten commit edildiyse durun ve history cleanup'tan önce private security handling kullanın. Secret-like değeri başka bir commit ekleyerek saklamaya çalışmayın.

İlgili: [Public screenshot standartları](../../docs/tr/public-screenshot-standards.md), [Public issue redaction](public-issue-redaction.md), [Public validation fails](public-validation-fails.md), [Destek politikası](../../SUPPORT.md).
