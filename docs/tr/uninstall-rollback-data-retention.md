# Kaldırma, Veri Saklama ve Rollback

Bu rehberi Windows hostundan VaultPilot kaldırılacağı, server verisi korunacağı veya başarısız yükseltme sonrası rollback yapılacağı zaman kullanın. Varsayılan yaklaşım konservatiftir: kaldırma işlemi, ayrı ve onaylı bir purge planı yoksa encrypted vault verisini yok etmemelidir.

## Güvenlik Sınırı

| Alan | Varsayılan |
| --- | --- |
| Servis kaldırma | MSI maintenance veya paketli uninstall helper üzerinden yapılabilir. |
| Data dizini | Varsayılan olarak korunur. Normal uninstall sırasında `C:\ProgramData\VaultPilot` veya legacy `C:\ProgramData\PassMan` silinmez. |
| Yedekler | Uninstall, rollback veya yıkıcı destek adımı öncesinde export edilir ve doğrulanır. |
| Purge | Yıkıcı kabul edilir ve bu public doküman dışında açık operatör onayı gerektirir. |
| Kanıt | Yalnızca redakte edilmiş servis durumu, sürüm, log ve hata metni paylaşılır. Database, backup, PFX/P12 paketi, private key veya ana parola asla paylaşılmaz. |

## Uninstall veya Rollback Öncesi

1. Kurulu sürümü, servis adını, public host değerini ve public HTTPS portunu kaydedin.
2. Şifreli backup export alın ve server diski dışında saklayın.
3. Backup'ın temiz bir doğrulama profilinde veya staging hostunda içe aktarılabildiğini doğrulayın.
4. Data path'in `C:\ProgramData\VaultPilot` mi yoksa legacy `C:\ProgramData\PassMan` compatibility path'i mi olduğunu kaydedin.
5. Hedef imzalı MSI veya rollback paketini yalnızca GitHub Releases üzerinden indirin.
6. Çalıştırmadan önce paket adını, signer bilgisini, SHA-256 değerini ve manifesti doğrulayın.

## Veriyi Koruyarak Normal Kaldırma

1. Windows Apps and Features ekranını açın veya aynı MSI'ı maintenance mode ile çalıştırın.
2. Remove seçeneğini yalnızca doğrulanmış backup varsa kullanın.
3. MSI maintenance'ın Windows servisini, firewall kuralını ve kurulu server dosyalarını kaldırmasına izin verin.
4. Ayrı bir purge onayı yoksa data dizinini koruyun.
5. Servisin kalktığını doğrulayın:

```powershell
sc.exe query VaultPilotServer
```

Komut servisin bulunmadığını söyleyebilir. Uninstall sonrası bu beklenen sonuçtur. Private hostname veya support context içerebilecek ham logları public kanala eklemeyin.

## Rollback Yolu

Rollback normal update akışı değil, kontrollü recovery aksiyonudur.

1. Sunucuya geniş kullanıcı erişimini durdurun.
2. Mevcut data dizinini koruyun ve UI hâlâ erişilebiliyorsa taze backup export alın.
3. Önceki imzalı MSI paketini GitHub Releases üzerinden indirin.
4. Önceki MSI ve manifest kanıtını doğrulayın.
5. Önceki MSI'ı Administrator olarak çalıştırın.
6. Servisin başladığını ve tarayıcının `https://<SERVER_HOST>:1903` veya yapılandırılan public HTTPS portunu açtığını doğrulayın.
7. Erişimi yeniden açmadan önce owner unlock, lisans durumu, audit görünürlüğü, extension pairing ve Update Center durumunu doğrulayın.

Rollback başarısızsa durun ve redakte edilmiş support evidence pack toplayın. SQLite database veya key material üzerinde elle değişiklik yapmayın.

## Data Purge Sınırı

Public docs kopyala-yapıştır purge komutu vermez. Data dizinini silmek encrypted vault payload, wrapped key, audit metadata, lisans durumu, server ayarları ve sertifika materyalini kalıcı olarak kaldırabilir. Purge kararı backup kanıtı ve açık onay içeren private operasyon değişiklik kaydında verilmelidir.

## Restore Tatbikatı

Restore testini uninstall işleminden ayrı yapın:

1. Temiz doğrulama hostu veya profili kullanın.
2. Şifreli backup'ı içe aktarın.
3. Item count, integrity manifest, owner unlock ve audit görünürlüğünü doğrulayın.
4. Restore'un çalıştığına dair yalnızca redakte edilmiş kanıt kaydedin.

İlgili sayfalar:

- [Yedekleme ve geri yükleme](backups-and-restore.md)
- [Windows Server kurulumu](install-windows-server.md)
- [Release asset doğrulama](release-asset-verification.md)
- [Destek kanıt paketi](support-evidence-pack.md)
