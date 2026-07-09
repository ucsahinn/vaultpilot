# Eklenti eşleşmesi beklemede kalıyor

Chromium eklentisi kurulu olduğu halde VaultPilot paneli beklemede kalıyor, cihazı göstermiyor veya bir kez eşleşip sonra eşitlemiyorsa bu makaleyi kullanın. Eşleştirme hesap, origin ve tarayıcı profili sınırlarına bağlıdır; paketi yeniden üretmeden önce bu üç sınırı kontrol edin.

## İlk Müdahale

1. VaultPilot içinde [Tarayıcı eklentisi](../../docs/tr/screen-browser-extension.md) ekranını açın ve tekrar denerken sayfayı açık tutun.
2. Extension server origin değerinin operatöre gösterilen VaultPilot host, port ve scheme bilgisiyle birebir aynı olduğunu doğrulayın.
3. Kodun süresi dolduysa veya eklenti başka tarayıcı profili içinde açıldıysa yeni eşleştirme kodu başlatın.
4. Eklentideki username ile VaultPilot'ta oturum açmış hesabın aynı olduğunu kontrol edin.
5. Secret sync beklemeden önce VaultPilot web UI içinde en az bir vault unlock edilmiş olmalı.
6. Yeni cihazı Browser Extension ekranından onaylayın, sonra eski veya tekrarlı cihazları revoke edin.

## Neyi Kontrol Etmeli

| Sınır | Belirti | Aksiyon |
| --- | --- | --- |
| Origin | Kod kabul edilir ama server pending kalır | `https://<SERVER_HOST>:<PORT>` değerini scheme ve port dahil birebir eşleştirin. |
| Browser profile | Bir profilde çalışır, diğerinde çalışmaz | Her profile ayrı pairing yapın veya sadece yönetilen profile kullanın. |
| Account | Cihaz başka kullanıcı altında görünür | Extension'dan çıkış yapın, doğru VaultPilot kullanıcısıyla tekrar pairing yapın. |
| Vault unlock | Cihaz approved ama kayıt sync olmaz | İlgili vault'u unlock edin ve erişim atamasını kontrol edin. |
| Device list | Aynı profile için birden fazla satır var | Eski cihazları revoke edin, tek sefer pair edin ve yeni label'ı kaydedin. |

## Güvenli Kanıt

- Extension versiyonu ve browser ailesi.
- `<VAULTPILOT_URL>` gibi redakte VaultPilot origin.
- Pairing state: new, pending, approved, revoked veya expired.
- Public kanalda kullanıcı adları redakte edilmiş device label ve timestamp.
- Sadece console error kategorisi; token veya wrapped pairing material paylaşmayın.

## Güvenlik

Eklenti, pairing materyalini Chromium profilinde PIN ile sarmalar. Plaintext secret değerleri, master password, pairing secret ve API client secret kalıcı browser storage, screenshot veya public issue içinde tutulmamalıdır.

İlgili: [Tarayıcı eklentisi ekranı](../../docs/tr/screen-browser-extension.md), [Browser extension rehberi](../../docs/tr/browser-extension.md), [Chrome Web Store review KB](chrome-web-store-review.md), [Public issue redaction](public-issue-redaction.md).
