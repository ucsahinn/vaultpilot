# Release Asset Doğrulama

Bir VaultPilot public release assetini kurmadan veya kurum içinde dağıtmadan önce bu sayfayı kullan. Amaç, MSI ve destek paketlerinin imzalı manifest ve değerlendirilen kesin GitHub Release ile uyumlu olduğunu doğrulamaktır.

## Release Durumu

30 Haziran 2026 itibarıyla doğrulanan son yayınlı GitHub Release hâlâ `v1.8.21`. Aşağıdaki tablo hazırlanan VaultPilot 2.0.0 asset setidir; `v2.0.0` GitHub Release, final assetler, manifest, imzalar ve hashler yayınlanıp doğrulanmadan public kanıt sayılmamalıdır.

## Hazırlanan 2.0.0 Asset Seti

| Bileşen | Sürüm | Asset |
| --- | ---: | --- |
| VaultPilot Enterprise Vault Console | 2.0.0 | `VaultPilot-2.0.0-x64.msi` yayın sonrası |
| Chromium Browser Extension | 1.3.1 | Chrome Web Store listing; `vaultpilot-browser-vault-extension.zip` release arşivi |
| Offline Share Decrypter | 1.2.0 | `vaultpilot-share-decrypter.zip` |
| VaultPilot DC Agent Service | 1.2.10 | `vaultpilot-dc-agent.ps1` yayın sonrası |
| Update manifest | 2.0.0 channel metadata | `vaultpilot-update.json` yayın sonrası |

## Public Asset Seti

Public GitHub Release yalnızca müşteri güvenli delivery assetlerini içermelidir:

- `VaultPilot-2.0.0-x64.msi`
- `vaultpilot-update.json`
- `vaultpilot-browser-vault-extension.zip`
- `vaultpilot-share-decrypter.zip`
- `vaultpilot-dc-agent.ps1`

Chrome Web Store listelemesi tarayıcı eklentisi için birincil müşteri kurulum ve güncelleme kanalıdır. Eklenti ZIP'i yalnızca release arşivi, lab doğrulama paketi, lokal geliştirme paketi veya acil fallback çıktısı olarak tutulur.

Git tree içinde MSI, ZIP, EXE, PFX, P12, DB, SQLite, backup veya signing-key dosyası bulunmamalıdır.

## 2.0.0 Asset Metadata Durumu

Final 2.0.0 boyut ve SHA-256 değerleri burada özellikle yazılmadı. Bu değerler `npm run build:windows`, manifest issue/verify, MSI doğrulama ve yayın kanıtı tamamlandıktan sonra release gate çıktısından alınmalıdır.

30 Haziran 2026 itibarıyla doğrulanan son GitHub Release hâlâ `v1.8.21`; eski `1.8.22` boyut veya hash değerleri 2.0.0 kanıtı olarak yeniden kullanılmamalıdır.

## Doğrulama Adımları

1. `v2.0.0` GitHub Release sayfasını yalnızca yayın sonrasında aç. Release yoksa bu sayfayı sadece yayın öncesi checklist olarak kullan.
2. Release tag değerinin `v2.0.0` olduğunu ve kurum politikanız özellikle izin vermedikçe draft/prerelease olmadığını doğrula.
3. O release içinden `vaultpilot-update.json` indir.
4. Manifestin server version olarak `2.0.0` gösterdiğini doğrula.
5. MSI filename değerinin `VaultPilot-2.0.0-x64.msi` olduğunu doğrula.
6. Asset URL'lerinin onaylı public GitHub Release hostunu kullandığını doğrula.
7. İndirilen MSI boyutu ve SHA-256 değerini manifest ile karşılaştır.
8. MSI Authenticode signer metadata değerini manifest signer thumbprint ile karşılaştır.
9. Extension release arşivi, decrypter ve DC Agent package hash değerlerini kurum içinde dağıtmadan önce doğrula; tarayıcı kullanıcıları eklentiyi Chrome Web Store'dan kurup güncellemelidir.

## Kurum İçinde Kaydedilebilecek Kanıt

| Kanıt | Public kayda uygun mu? |
| --- | --- |
| Release tag, dosya adları, boyutlar ve hash değerleri | Evet. |
| MSI signer subject ve thumbprint | Evet. |
| Manifest signature değeri | Evet. |
| Lokal install path, private hostname ve kullanıcı adları | Önce redakte et. |
| License code, signing private key, PFX/P12 veya database | Asla. |

## Doğrulama Başarısızsa

Paketi kurma veya dağıtma. Release tag, asset adı, beklenen hash, gözlenen hash, dosya boyutu ve signer durumunu topla; private support kanalı kullan.

İlgili sayfalar:

- [Güncelleme Merkezi](update-center.md)
- [Kaldırma, veri saklama ve rollback](uninstall-rollback-data-retention.md)
- [Güvenlik ve güven modeli](security-and-trust-model.md)
- [Destek kanıt paketi](support-evidence-pack.md)
