# Release Asset Doğrulama

Bir VaultPilot yayın dosyasını kurmadan veya kurum içinde dağıtmadan önce bu sayfayı kullanın. Amaç, MSI ve destek paketlerinin imzalı manifest ve doğrulanmış GitHub Release ile uyumlu olduğunu kanıtlamaktır.

## Release Durumu

Güncel doğrulanmış public release, 23 Temmuz 2026'da yayınlanan GitHub Release [`v3.0.2`](https://github.com/ucsahinn/vaultpilot/releases/tag/v3.0.2).

Herkese açık doğrulama kaynağı olarak GitHub Release asset metadata'sını esas alın. Yayınlanmamış build çıktısı, kopyalanmış paketler, destek eki veya sohbet üzerinden gelen dosyalar release kanıtı değildir.

## VaultPilot 3.0.2 Bileşenleri

| Bileşen | Sürüm | Asset |
| --- | ---: | --- |
| VaultPilot Enterprise Vault Console | 3.0.2 | `VaultPilot-3.0.2-x64.msi` |
| Chromium Browser Extension | Chrome Web Store 1.3.3; v3.0.2 arşivi 1.3.3 | Chrome Web Store listing; varsayılan manifestoda ZIP yok |
| Offline Share Decrypter | 1.2.1 | `vaultpilot-share-decrypter.zip` |
| VaultPilot DC Agent Service | 1.2.22 | `vaultpilot-dc-agent.ps1` |
| Update manifest | 3.0.2 channel metadata | `vaultpilot-update.json` |

## VaultPilot 3.0.2 Yayın Kanıtı

Bu tablo, müşteri indirmelerinde kullanılan ve bağımsız olarak doğrulanan public `v3.0.2` dosya setini kaydeder.

| Bileşen | Sürüm | Teslim yolu |
| --- | ---: | --- |
| VaultPilot Enterprise Vault Console | 3.0.2 | Sürümlü Windows MSI ve imzalı güncelleme manifesti |
| Chromium Browser Extension | 1.3.3 | Chrome Web Store sürümü; bu yayında extension ZIP yok |
| Offline Share Decrypter | 1.2.1 | Sürümlü yayın arşivi ve imzalı bileşen manifesti |
| VaultPilot DC Agent Service | 1.2.22 | Sürümlü PowerShell dosyası ve imzalı bileşen manifesti |
| VaultPilot Backup Tool | 1.0.3 | Sunucuyla gelen destek bileşeni; ayrı GitHub Release dosyası değildir |
| VaultPilot Log Collector | 1.0.3 | Sunucuyla gelen destek bileşeni; ayrı GitHub Release dosyası değildir |

## Public Asset Seti

Public GitHub Release şu müşteri güvenli teslim dosyalarını içerir. Bu tablo 23 Temmuz 2026 tarihinde yayımlanan ve yerelde doğrulanan dosya setini kaydeder:

| Asset | Boyut | SHA-256 |
| --- | ---: | --- |
| `VaultPilot-3.0.2-x64.msi` | 65,441,792 | `33f43c95379b53122c92674ad6bef973ad29f6a29a44dd761d2ebd263a6e249e` |
| `vaultpilot-update.json` | 1,374 | `25dba9059350152c37d687b7061a5ad254f70fc57aef4814a473e8a9a6842397` |
| `vaultpilot-share-decrypter.zip` | 51,566 | `e72cef76a1a8389339ea75469e6467b908cd51cd7e8f6381fcb61910eb9af756` |
| `vaultpilot-share-decrypter.json` | 218 | `5d4af2cd0be93f7d553a37def1446d71962c9d0f5a8403038455197659ba7da8` |
| `vaultpilot-dc-agent.ps1` | 234,224 | `1db27b19a7417b00da5102cebc39e85529ea07f0b957e76d63c7fed4b9e8f8a8` |
| `vaultpilot-dc-agent.json` | 213 | `ebaaeed49bf1be99df8f3607addea5adc60cc9c339204c69dd16b37a23362ea3` |
| `VpUninstallTool-3.0.2-x64.msi` | 69,632 | `bca790aa016ed4627fcf7cdba49768dde27d6fb6b8c3740f407cc26ed131558e` |

Chrome Web Store listelemesi tarayıcı eklentisi için birincil müşteri kurulum ve güncelleme kanalıdır ve GitHub Release'den bağımsız ilerleyebilir. Canlı mağaza `1.3.3` gösterir; varsayılan `v3.0.2` güncelleme manifestosu extension ZIP yayımlamaz.

MSI, manifestoda sabitlenen VaultPilot geliştirme imzalayıcısıyla Authenticode imzalıdır ve RFC3161 zaman damgası yoktur. VaultPilot yönetimli güncellemeler imzalı manifestoyu, kesin SHA-256 değerini ve signer thumbprint'ini doğrular; ancak Windows güveni ve SmartScreen itibarı ortama bağlıdır. Yayımlanan MSI hash'i için commit-bound final artifact, standalone payload ve managed-component kanıtları geçti. Bu hotfix MSI için yeni yerel Health, elevated Repair/Health ve fiziksel Windows Sandbox Install/Health kanıtı yeniden çalıştırılmadı.

Legacy uyumluluk dosyaları yalnız kurulu migration ve rollback yollarında kalabilir; yeni public release'ler sadece VaultPilot adlı müşteri varlıklarını içerir.

Git tree içinde MSI, ZIP, EXE, PFX, P12, DB, SQLite, backup veya signing-key dosyası bulunmamalıdır.

## Doğrulama Adımları

1. GitHub Release [`v3.0.2`](https://github.com/ucsahinn/vaultpilot/releases/tag/v3.0.2) sayfasını aç.
2. Release tag değerinin `v3.0.2` olduğunu ve kurum politikanız özellikle izin vermedikçe draft/prerelease olmadığını doğrula.
3. O release içinden `vaultpilot-update.json` indir.
4. Manifestin server version olarak `3.0.2` gösterdiğini doğrula.
5. MSI dosya adının `VaultPilot-3.0.2-x64.msi` olduğunu doğrula.
6. Asset URL'lerinin onaylı public GitHub Release hostunu kullandığını doğrula.
7. İndirilen dosya boyutlarını ve SHA-256 değerlerini yukarıdaki tabloyla ve ilgili bileşen manifestte yer alıyorsa manifest ile karşılaştır.
8. MSI Authenticode signer metadata değerini manifest signer thumbprint ile karşılaştır.
9. Extension release arşivi, decrypter ve DC Agent package hash değerlerini kurum içinde dağıtmadan önce doğrula; tarayıcı kullanıcıları eklentiyi Chrome Web Store'dan kurup güncellemelidir.

## Windows Doğrulama Komutları

Bu komutları indirilmiş release dosyalarını içeren geçici bir klasörden çalıştırın. Çıktıyı kurum içi release kanıtıyla saklayın; herkese açık paylaşmadan önce lokal path veya hostname değerlerini redakte edin.

```powershell
gh release view v3.0.2 --repo ucsahinn/vaultpilot --json tagName,name,isDraft,isPrerelease,publishedAt,assets,url

Get-ChildItem -File |
  Where-Object { $_.Name -like 'VaultPilot-3.0.2-x64.msi' -or $_.Name -like 'vaultpilot-*' -or $_.Name -like 'VpUninstallTool-*' } |
  Select-Object Name,Length

Get-FileHash .\VaultPilot-3.0.2-x64.msi -Algorithm SHA256
Get-FileHash .\vaultpilot-* -Algorithm SHA256

Get-AuthenticodeSignature .\VaultPilot-3.0.2-x64.msi |
  Format-List Status,StatusMessage,SignerCertificate
```

`gh release view` farklı tag, draft/prerelease durumu, asset sayısı, boyut, digest veya URL gösterirse devam etme; önce bu sayfayı ve public external-surface drift register'ını güncelle.

## Kurum İçinde Kaydedilebilecek Kanıt

| Kanıt | Public kayda uygun mu? |
| --- | --- |
| Release tag, dosya adları, boyutlar ve hash değerleri | Evet. |
| MSI signer subject ve thumbprint | Evet. |
| Manifest signature değeri | Evet. |
| Lokal install path, private hostname ve kullanıcı adları | Önce redakte et. |
| License code, signing private key, PFX/P12 veya database | Asla. |

## Doğrulama Başarısızsa

Paketi kurmayın veya dağıtmayın. Release tag, asset adı, beklenen hash, gözlenen hash, dosya boyutu ve signer durumunu toplayın; satın alma veya onboarding materyallerindeki lisanslı destek kanalını kullanın.

İlgili sayfalar:

- [Güncelleme Merkezi](update-center.md)
- [Kaldırma, veri saklama ve rollback](uninstall-rollback-data-retention.md)
- [Güvenlik ve güven modeli](security-and-trust-model.md)
- [Destek kanıt paketi](support-evidence-pack.md)
