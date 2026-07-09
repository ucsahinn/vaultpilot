# SSS

## VaultPilot bulut servisi mi?

Hayır. VaultPilot self-hosted Windows Server uygulamasıdır.

## Ana parola sunucuya gider mi?

Hayır. Ana parola tarayıcıda kullanılır; sunucuya plaintext ana parola gönderilmez.

## Public repo kaynak kod içeriyor mu?

Hayır. Git tree dokümantasyon, release notları, knowledge-base makaleleri, public policy'ler ve yayına uygun hale getirilmiş görsel asset'leri içerir. Müşteri delivery dosyaları GitHub Releases üzerinde ek olarak veya Chrome Web Store üzerinden dağıtılır; kaynak kod private repoda kalır.

## Local signer güvenli mi?

VaultPilot-managed update zinciri için imzalı manifest MSI signer thumbprint'ini pin'liyorsa local signer kabul edilebilir. Windows SmartScreen itibarı için CA-backed veya trusted signing önerilir.

## Dosyalar paylaşılabilir mi?

Evet. Seçilen dosya kayıtları dış paylaşım paketine dahil edilebilir. Expiry ve kullanım limiti belirlenmelidir.

## İlgili

- [Yönetici hızlı başlangıç](admin-quickstart.md)
- [İlk kurulum, owner ve lisans](first-run-owner-license.md)
- [Güvenlik ve güven modeli](security-and-trust-model.md)
- [Destek kanıt paketi](support-evidence-pack.md)
