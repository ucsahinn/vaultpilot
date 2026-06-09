# Release Asset Doğrulama

Bir PassMan public release assetini kurmadan veya kurum içinde dağıtmadan önce bu sayfayı kullan. Amaç, MSI ve destek paketlerinin imzalı manifest ve son public release ile uyumlu olduğunu doğrulamaktır.

## Güncel Release

| Bileşen | Sürüm | Asset |
| --- | ---: | --- |
| PassMan Enterprise Vault Console | 1.8.21 | `PassMan-1.8.21-x64.msi` |
| Chromium Browser Extension | 1.3.1 | Chrome Web Store listing; `passman-chromium-extension.zip` release arşivi |
| Offline Share Decrypter | 1.2.0 | `passman-share-decrypter.zip` |
| PassMan DC Agent Service | 1.2.10 | `passman-ad-agent.ps1` |
| Update manifest | 1.8.21 channel metadata | `passman-update.json` |

## Public Asset Seti

Public GitHub Release yalnızca müşteri güvenli delivery assetlerini içermelidir:

- `PassMan-1.8.21-x64.msi`
- `passman-update.json`
- `passman-chromium-extension.zip`
- `passman-share-decrypter.zip`
- `passman-ad-agent.ps1`

Chrome Web Store listelemesi tarayıcı eklentisi için birincil müşteri kurulum ve güncelleme kanalıdır. Eklenti ZIP'i yalnızca release arşivi, lab doğrulama paketi, lokal geliştirme paketi veya acil fallback çıktısı olarak tutulur.

Git tree içinde MSI, ZIP, EXE, PFX, P12, DB, SQLite, backup veya signing-key dosyası bulunmamalıdır.

## 1.8.21 Asset Metadata

| Asset | Boyut | SHA-256 |
| --- | ---: | --- |
| `PassMan-1.8.21-x64.msi` | 61526016 | `5f56d371d3a75fe57e3a6c9d9b6ba96d819f807c04c5ece42d277e88a51635d0` |
| `passman-update.json` | 1634 | Manifest kendi Ed25519 imza bloğunu içerir. |
| `passman-chromium-extension.zip` | 160905 | `533d1f089f05753b1feff9caa31b6126fada73bcc4c836a738263d653ce6af6f` |
| `passman-share-decrypter.zip` | 40663 | `94750f75efba50e19f5290fc47091341a77d8456b03acd2c9f9b289403c53a86` |
| `passman-ad-agent.ps1` | 97167 | `383c543bbc83b3c4ccd39f2ee39308aef9ef547f9fcc82ddc572dd86a87b71f1` |

## Doğrulama Adımları

1. Son release sayfasını aç.
2. Release tag değerinin `v1.8.21` olduğunu doğrula.
3. `passman-update.json` indir.
4. Manifestin server version olarak `1.8.21` gösterdiğini doğrula.
5. MSI filename değerinin `PassMan-1.8.21-x64.msi` olduğunu doğrula.
6. Asset URL'lerinin public `ucsahinn/passman` GitHub Release hostunu kullandığını doğrula.
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
- [Güvenlik ve güven modeli](security-and-trust-model.md)
- [Destek kanıt paketi](support-evidence-pack.md)
