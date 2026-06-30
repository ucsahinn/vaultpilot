# Windows Server Kurulumu

Bu runbook, VaultPilot Server'ın Windows üzerinde normal kurulumu veya yerinde yükseltmesi için kullanılır. Sunucuyu diğer kullanıcılara açmadan önce bu kontroller tamamlanmalıdır.

## Gereksinimler

| Gereksinim | Not |
| --- | --- |
| Windows Server veya onaylı Windows host | Stabil disk ve yedekleme politikası olan kontrollü bir host kullanın. |
| Yönetici yetkisi | MSI, servis kaydı ve firewall kuralı için gerekir. |
| Gelen TCP erişimi | Varsayılan port `1903`; yalnızca ağ politikanız gerektiriyorsa değiştirin. |
| Yedek kararı | Üretim yükseltmesinden önce mevcut data dizinini koruyun veya yedek alın. |
| Release varlıkları | MSI ve update manifestini GitHub Releases üzerinden indirin. Chat veya destek mesajlarından kopyalanmış dosyaları kullanmayın. |

## Kurulum

1. `v2.0.0` GitHub Release yayınlandıktan sonra `VaultPilot-2.0.0-x64.msi` dosyasını indirin.
2. Çalıştırmadan önce dosya adını, kaynağı, checksum değerini ve signer bilgisini doğrulayın. Tam kontrol listesi için [release asset doğrulama](release-asset-verification.md) sayfasını kullanın.
3. MSI'ı Administrator olarak çalıştırın.
4. Kurulum; standalone server, gömülü Node runtime, Prisma/SQLite runtime dosyaları, Windows servisi, firewall kuralı, data dizini ve log dizinini hazırlar.
5. Önce sunucu üzerinden VaultPilot'u açın:

```text
https://127.0.0.1:1903
```

Sonra uzaktan erişimi doğrulayın:

```text
https://<SERVER_HOST>:1903
```

İlk profil oluşturma ve kasa kilidi açma tarayıcı Web Crypto desteği ister. Kurulu server public tarayıcı girişini varsayılan olarak `1903` portunda HTTPS üzerinden açar ve trusted PFX/P12 yapılandırılana kadar managed self-signed sertifika kullanır. Düz HTTP yalnızca internal upstream veya local development yolları içindir; operatör giriş noktası olarak dokümante edilmemelidir.

## Kurulan Yüzeyler

| Yüzey | Değer |
| --- | --- |
| Windows servisi | `VaultPilotServer` |
| Görünen ad | `VaultPilot Server` |
| Data dizini | `C:\ProgramData\VaultPilot`; legacy `C:\ProgramData\PassMan` yalnızca upgrade alias |
| Log dizini | `C:\ProgramData\VaultPilot\logs`; legacy `C:\ProgramData\PassMan\logs` yalnızca upgrade alias |
| Varsayılan port | `1903` |
| Tarayıcı girişi | Trusted PFX/P12 yapılandırılana kadar managed self-signed HTTPS ile `https://<SERVER_HOST>:1903` |

## Kurulum Sonrası Doğrulama

Geniş erişim vermeden önce şu kontrolleri çalıştırın:

```powershell
sc.exe query VaultPilotServer
```

```text
https://127.0.0.1:1903/api/profile
```

Beklenen sonuç:

- Servis kurulu ve çalışır durumda.
- Lokal API cevap veriyor.
- Uzak URL onaylı bir istemciden açılıyor.
- Firewall kuralı yalnızca hedef ağ yolunu açıyor.
- VaultPilot log dizininde kalıcı installer hatası yok.

## İlk Giriş Yolu

Servis doğrulamasından sonra:

1. Owner profilini oluşturun.
2. Ana parola ile kasayı açın.
3. Lisansı uygulayın.
4. Public host ve HTTPS yapılandırmasını tamamlayın.
5. Ek kullanıcı eklemeden önce 2FA'yı etkinleştirin.

## Yükseltme Notları

- Üretim yükseltmesinden önce yedek dışa aktarın.
- MSI'ın server ve destek bileşenlerini birlikte güncellemesine izin verin.
- Offline decrypter ve DC agent script'i MSI tarafından yenilenir ve release notlarında izlenir.
- Destek özellikle istemedikçe kurulu server dizinindeki dosyaları elle değiştirmeyin.

## PassMan Markalı Kurulumdan Yükseltme

Yükseltmeden önce server backup alın ve mevcut servis adını, data dizinini, portu ve çalışan sürümü kaydedin. VaultPilot 2.0 MSI dosyasını Administrator olarak çalıştırın. `C:\ProgramData\PassMan` dizinini veya mevcut servis kayıtlarını elle yeniden adlandırmayın.

Yükseltme sonrasında `VaultPilotServer`, data dizini, Update Center, extension pairing, lisans durumu, audit retention ve Server System diagnostics kontrollerini doğrulayın. Legacy PassMan alias'ları yalnızca compatibility ve rollback için kalabilir.

## Destek İçin Güvenli Kanıt

Redakte edildikten sonra paylaşılabilir:

- MSI dosya adı.
- VaultPilot server sürümü.
- Windows servis durumu.
- Redakte edilmiş installer log kesiti.
- Gerçek host yerine `<SERVER_HOST>` kullanılan tarayıcı URL biçimi.

Database, yedek, PFX/P12 dosyası, private key, ana parola, secret değeri veya gerçek internal hostname paylaşmayın.
