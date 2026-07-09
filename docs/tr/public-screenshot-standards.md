# Public Ekran Görüntüsü Standartları

Herkese açık repoya VaultPilot ekran görüntüsü eklerken, değiştirirken veya gözden geçirirken bu sayfayı kullanın. Herkese açık ekran görüntüleri dokümantasyon örneğidir. Operatörün ekranı ve akışı tanımasına yardım eder, fakat release kanıtı, production yönlendirmesi veya müşteri ortamı kanıtı değildir.

## Kaynak Kuralları

- Yalnız dokümantasyon için hazırlanmış izole bir VaultPilot çalışma ortamından capture alın.
- Tenant, host, kullanıcı, grup, vault, kayıt, dosya, finding, paket, lisans ve update verileri synthetic olmalıdır.
- Gerçek hostname, kullanıcı adı, e-posta, müşteri adı, path, database adı, support ticket, log, token değeri, lisans değeri, vault kaydı, secret başlığı, parola, private key veya sertifika materyali göstermeyin.
- Browser chrome, masaüstü bildirimi, local klasör, terminal penceresi, account dashboard ve kişisel profil verisi frame dışında kalmalıdır.
- Görünen sayaç, timestamp, dosya adı, paket boyutu, hash, domain, finding ve aksiyon durumlarını dokümantasyon örneği kabul edin; bunlar release doğrulama verisi olarak kullanılmamalıdır.

## Onaylı Screenshot Manifesti

Validator yalnızca aşağıdaki public screenshot dosyalarını ve [`assets/screenshots/MANIFEST.json`](../../assets/screenshots/MANIFEST.json) içindeki makine tarafından okunabilir envanteri kabul eder. Bu manifest her yüzey için PNG ölçülerini, byte boyutunu, SHA-256 hash değerini, yüzey adını ve sentetik örnek notunu kaydeder; böylece görsel değişimi açık ve review edilebilir kalır.

| Yüzey | Dosya |
| --- | --- |
| Login lock screen | `assets/screenshots/login-lock-screen.png` |
| Security posture dashboard | `assets/screenshots/overview-security-posture.png` |
| Secret records listesi | `assets/screenshots/passwords-record-list.png` |
| Server System ayarları | `assets/screenshots/server-settings.png` |
| Discovery run scope | `assets/screenshots/discovery-run.png` |
| Discovery findings | `assets/screenshots/discovery-findings.png` |
| Discovery import candidates | `assets/screenshots/discovery-import.png` |
| Update Center | `assets/screenshots/update-center-vaultpilot-2.png` |
| Browser extension management | `assets/screenshots/browser-extension-management-vaultpilot-2.png` |
| Active Directory sync tree | `assets/screenshots/active-directory-sync-tree-vaultpilot-2.png` |
| Sharing package flow | `assets/screenshots/sharing-package-flow-vaultpilot-2.png` |

Emekliye ayrılmış legacy compatibility ekran görüntüsü seti geri getirilmemeli, linklenmemeli veya walkthrough kanıtı gibi kullanılmamalıdır. Güncel public screenshot'lar VaultPilot adlandırmalı dosyaları kullanır ve `scripts/validate-docs.mjs` tarafından zorunlu tutulur.

## Kabul Kontrol Listesi

- Dosya PNG ve 2 MB altındadır.
- Dosya adı lowercase kebab-case kullanır.
- Dosya `assets/screenshots/MANIFEST.json` içinde ve `scripts/validate-docs.mjs` içindeki onaylı path listesinde yer alır.
- Manifest ölçüleri, byte boyutu, SHA-256 hash değeri, yüzey etiketi ve sentetik örnek notu final PNG ile eşleşir.
- Markdown alt text'i generic "screenshot" etiketi yerine yüzeyi açıkça adlandırır.
- Görsel operasyon kanıtı sanılabilecekse açıklama metni, görünen değerlerin sentetik örnek olduğunu belirtir.
- Görsel ilgili rehberden veya `docs/README.md` içindeki görsel referans tablosundan linklenir; ham screenshot klasörü linki kullanılmaz.
- Sayfa yüzey bağlamını, ürün sürümü bağlamını ve gösterilen workflow'u açıklar.
- Screenshot secret, müşteri identifier, local operator path, tarayıcı profil verisi ve account dashboard verisi için full-size manuel incelenmiştir.

## Değiştirme Süreci

1. Aday görseli izole dokümantasyon çalışma ortamı'ından capture alın.
2. Git'e eklemeden önce görseli full-size inceleyin.
3. PNG dosyasını `assets/screenshots/` altına koyun.
4. Görseli kullanan rehberi ve `docs/README.md` görsel tablosunu güncelleyin.
5. `assets/screenshots/MANIFEST.json` içine final ölçüleri, byte boyutunu, SHA-256 hash değerini, yüzey etiketini ve sentetik örnek notunu yazın.
6. Dosya path'i değiştiyse `scripts/validate-docs.mjs` içindeki onaylı screenshot path listesini güncelleyin.
7. Kabul edilen manifest değiştiyse bu sayfayı güncelleyin.
8. Şunları çalıştırın:

```powershell
npm run validate
git diff --check
gitleaks detect --no-git --redact --verbose --source .
```

Daha sonra dosya stage edilirse ayrıca çalıştırın:

```powershell
npm run validate:staged
git diff --cached --check
```

## Screenshot Güvenli Değilse

Görseli commit etmeyin veya public olarak eklemeyin. Görseli sentetik veri kullanan capture ile değiştirin. Görsel token, secret değeri, sertifika private materyali, lisans private materyali, müşteri credential'ı veya geliştirici/hesap paneline ait özel veri gösterdiyse ilgili değeri private inceleme tamamlanana ve gerekiyorsa rotate veya revoke edilene kadar compromised kabul edin.

Olay akışı için [Public screenshot redaction](../../kb/tr/public-screenshot-redaction.md), kanıtın public issue'a uygun olup olmadığını ayırmak için [Public issue redaction](../../kb/tr/public-issue-redaction.md) sayfasını kullanın.

İlgili: [Dokümantasyon gateway](../README.md), [Public repo sınırı](public-repository-boundary.md), [Public repo yayın runbook'u](publication-runbook.md), [Chrome Web Store listeleme ve privacy](chrome-web-store-listing.md), [Katkı kuralları](../../CONTRIBUTING.md).
