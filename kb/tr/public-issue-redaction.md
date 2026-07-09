# Public Issue Redaction

Bir operatör veya destek mühendisi public issue açmak istediğinde eldeki kanıt tenant, host, kullanıcı, secret veya lisans verisi içerebiliyorsa bu makaleyi kullanın.

## Belirti

Konu doküman, kurulum, update, browser extension, Discovery, DC Agent veya paylaşım akışıyla ilgilidir; fakat mevcut ekran görüntüleri veya loglar ortama özel değerler içerir.

## Public-Safe Kanıt

Şunları ekleyebilirsiniz:

- VaultPilot sürümü ve etkilenen component adı.
- Windows Server sürümü.
- Public release tag'i veya asset adı.
- Redakte edilmiş timestamp ve hata durumu.
- İlgiliyse browser adı ve extension ID.
- `<VAULTPILOT_URL>` veya `<SERVER_HOST>` gibi yer tutucu host biçimi.
- Token, host, kullanıcı, path ve secret değerleri `<REDACTED>` ile değiştirildikten sonra kısa log parçaları.

## Public Paylaşımdan Önce Redakte Edin

Şu değerleri public paylaşmadan önce değiştirin:

- Müşteri, tenant, domain, OU, grup ve kullanıcı adları.
- Internal URL, IP adresi, makine adı ve local path.
- Kasa kayıt başlığı, username, URL, not, dosya ve custom field değerleri.
- Agent ID, agent token, API client ID, API secret, lisans kodu ve private lisans materyali.
- Session ID, cookie, sertifika subject'i ve sertifika private materyali.

## Public Olarak Paylaşmayın

Database, yedek, sertifika paketi, private key, PFX/P12 dosyası, MSI evidence bundle, ham log, support export'u veya gerçek kasa verisini hala gösteren ekran görüntüsü eklemeyin.

## Karar

- Kanıt tamamen redakte edildiyse ve soru public doküman veya ürün davranışıyla ilgiliyse public issue template'ini kullanın.
- Gerekli kanıt issue anlamını kaybetmeden redakte edilemiyorsa private support kullanın.

İlgili: [Destek politikası](../../SUPPORT.md), [public repo sınırı](../../docs/tr/public-repository-boundary.md), [destek kanıt paketi](../../docs/tr/support-evidence-pack.md).
