# Güvenlik Ve Güven Modeli

Bu public sayfa, private implementasyon veya kaynak kod açığa çıkarmadan VaultPilot güvenlik modelini operatör seviyesinde açıklar.

## Güven Sınırları

| Sınır | Üzerinden geçen veri | Operatör kuralı |
| --- | --- | --- |
| Tarayıcıdan VaultPilot sunucusuna | Authenticated API istekleri ve şifreli vault materyali. | Production erişimde HTTPS kullan; tarayıcı oturumunu gözetimsiz bırakma. |
| VaultPilot sunucusundan SQLite'a | Şifreli secret payloadları ve operasyonel metadata. | Database kopyalama veya public paylaşım yapma; şifreli backup akışını kullan. |
| Update Center'dan GitHub Releases'a | İmzalı manifest ve release assetleri. | Yalnızca manifest imzası, hash, boyut ve signer metadata doğrulanan assetlere güven. |
| Tarayıcı eklentisinden sunucuya | Eşleştirme kodu, sarılmış kasa anahtarı ve şifreli snapshot. | Yalnızca onaylı cihazları eşleştir; eski cihazların erişimini iptal et. |
| DC Agent'dan sunucuya | Directory metadata ve agent heartbeat. | AD bind parolası agent setup akışında lokal kalır; public support'a gönderilmez. |
| Dış paylaşım | Şifreli seçili kayıt paketi ve passphrase korumalı açma akışı. | Yalnızca seçili kayıtları paylaş; passphrase'i ayrı kanaldan ilet. |

## VaultPilot Neyi Korur

- Parola kayıtları, credential, API key, güvenli not, sertifika ve dosya tabanlı secretlar.
- Aktif tarayıcı oturumu boyunca vault unlock materyali.
- Süre sonu, maksimum açma sayısı ve şifreli paket metadata ile share paketleri.
- Manifest imzası, hash, boyut ve MSI signer metadata ile update paketleri.
- Görünür event history ve chain state ile audit kanıtı.

## Operatör Neyi Korumalı

- Ana parolalar ve authenticator cihazları.
- License private veya issuer-side materyali.
- Update signing private keyleri.
- Certificate private keyleri ve PFX/P12 dosyaları.
- Database, backup ve hassas metadata içerebilen loglar.
- AD bind credentialları ve agent tokenları.
- Gerçek kayıt, kullanıcı, internal hostname veya müşteri verisi gösteren ekran görüntüleri.

## Update Güven Zinciri

1. Operatör `vaultpilot-update.json` dosyasını indirir veya kontrol eder.
2. VaultPilot manifest imzasını doğrular.
3. VaultPilot release URL'lerinin izinli GitHub release hostlarında kaldığını doğrular.
4. VaultPilot MSI SHA-256 ve dosya boyutunu karşılaştırır.
5. VaultPilot manifestteki MSI signer thumbprint değerini doğrular.
6. Ancak bundan sonra MSI, VaultPilot-managed update yolu için güvenilir kabul edilir.

CA-backed veya trusted-signing sertifikalar Windows reputation için önerilir. VaultPilot-managed update güveni, imzalı manifest local signer thumbprint değerini pinlediğinde local signer kabul edebilir.

## Public Kanıt Kuralı

Support için yalnızca şunları gönder:

- Version numaraları.
- Redakte edilmiş service state.
- Redakte edilmiş hata mesajları.
- Manifest version, hash, boyut ve signer durumu.
- Gerçek kayıt, URL ve kullanıcıları silinmiş ekran görüntüleri.

Plaintext secret, ana parola, license private materyali, AD bind parolası, database, backup, private key veya PFX/P12 dosyası gönderme.

İlgili sayfalar:

- [Yayın dosyası doğrulama](release-asset-verification.md)
- [Denetim ve güvenlik duruşu](audit-and-security-posture.md)
- [Destek kanıt paketi](support-evidence-pack.md)
