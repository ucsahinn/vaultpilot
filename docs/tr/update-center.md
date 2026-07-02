# Güncelleme Merkezi

VaultPilot Güncelleme Merkezi ana Windows MSI paketini yönetir. Tarayıcı eklentisi Chrome Web Store üzerinden kurulur ve güncellenir; Offline Share Decrypter ve VaultPilot DC Agent Service bileşenleri release notlarında izlenir ve MSI veya belgelenmiş release asset'leriyle yenilenir.

![VaultPilot update center](../../assets/screenshots/update-center.png)

Screenshot notu: bu görsel PassMan compatibility line'dan geçici layout referansı olarak tutulur. Final 2.0 screenshotları yeniden alınana kadar VaultPilot 2.0 release veya branding kanıtı değildir.

## Güvenli Güncelleme Modeli

VaultPilot şunları doğrular:

- İmzalı update manifesti.
- Paket URL'si ve dosya adı.
- SHA-256 checksum.
- MSI Authenticode signer thumbprint.
- Dosya boyutu ve release metadata'sı.

İmzalı manifest lokal release signer thumbprint'ini pin'lediğinde VaultPilot-managed update trust için global CA chain zorunlu değildir. Windows SmartScreen itibarı ve geniş OS-level güven için CA-backed veya trusted-signing sertifika hâlâ önerilir.

## Normal Güncelleme Akışı

1. Yedek dışa aktarın.
2. Güncelleme Merkezi'ni açın.
3. Güncellemeleri kontrol edin.
4. Sürüm, notlar, signer ve checksum bilgisini inceleyin.
5. Güncellemeyi başlatın.
6. VaultPilot MSI'ı sunucuda indirir ve doğrular.
7. Quiet Windows Installer akışı çalışır.
8. VaultPilot servisi yeniden başlar.
9. Konsolu yeniden açıp sürüm ve sağlık durumunu doğrulayın.

## Release Asset'leri

Güncel 2.0.0 GitHub Release asset seti şunları içerir:

- `VaultPilot-2.0.0-x64.msi`
- `vaultpilot-update.json`
- Chrome Web Store eklenti listelemesi: `https://chromewebstore.google.com/detail/passman-enterprise-vault/hjkbedlaieikhkoplgpiohlaakgebobi?hl=tr`
- `vaultpilot-browser-vault-extension.zip` yalnızca release arşivi ve geliştirme fallback çıktısı

Chrome Web Store listeleme URL'si tarihsel mağaza slug'ını taşıyabilir; yayınlanmış extension ID `hjkbedlaieikhkoplgpiohlaakgebobi` değerini doğrulayın.
- `vaultpilot-extension-update.json`
- `vaultpilot-share-decrypter.zip`
- `vaultpilot-share-decrypter.json`
- `vaultpilot-dc-agent.ps1`
- `vaultpilot-dc-agent.json`

Manuel doğrulama gerektiğinde kurulumdan veya iç dağıtımdan önce [release asset doğrulama](release-asset-verification.md) sayfasını kullanın. Asset adlarını, boyutları ve SHA-256 değerlerini local rebuild klasörleriyle değil GitHub Release `v2.0.0` ile karşılaştırın.

## Bileşen Notları

Güncelleme Merkezi tarayıcı eklentisi için ayrı installer akışı açmamalıdır; eklenti kurulum ve güncelleme dağıtımını Chrome Web Store yönetir. DC agent ve decrypter için de ayrı installer akışı açmamalıdır. Sürüm notları görünür kalır; fakat MSI server paketiyle gelen destek dosyalarını yeniler. Operatörler manuel kurulum veya kurtarma gerektiğinde en güncel release asset'ini yine indirebilir.

## Sorun Giderme

| Belirti | İlk kontrol |
| --- | --- |
| Güncelleme yüzde 76 civarında duruyor | MSI imzası ve Windows Installer event log. |
| Checksum uyuşmuyor | İndirilen MSI'ı silip release asset üzerinden tekrar deneyin. |
| Servis yeniden başlamıyor | `VaultPilotServer` durumunu sorgulayın ve installer loglarını inceleyin. |
| Sürüm değişmedi | MSI'ın tamamlandığını doğrulayın, sonra servisi yeniden başlatın. |
