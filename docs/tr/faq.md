# SSS

## VaultPilot bulut servisi mi?

Hayır. VaultPilot self-hosted Windows Server uygulamasıdır.

## Ana parola sunucuya gider mi?

Hayır. Ana parola tarayıcıda kullanılır; sunucuya plaintext ana parola gönderilmez.

## Public repo kaynak kod içeriyor mu?

Hayır. Public repo dokümantasyon, release notları ve GitHub Release asset'leri içindir. Kaynak kod private repoda kalır.

## Local signer güvenli mi?

VaultPilot-managed update zinciri için imzalı manifest MSI signer thumbprint'ini pin'liyorsa local signer kabul edilebilir. Windows SmartScreen itibarı için CA-backed veya trusted signing önerilir.

## Dosyalar paylaşılabilir mi?

Evet. Seçilen dosya kayıtları dış paylaşım paketine dahil edilebilir. Expiry ve kullanım limiti belirlenmelidir.
