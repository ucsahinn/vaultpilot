# Güncelleme yüzde 76 civarında kalıyor

Yüzde 76 aşaması genellikle VaultPilot'ın release manifest ve MSI paket doğrulamasını bitirip sessiz Windows Installer akışına geçtiği noktadır. Server servisi bu sırada restart edebilir; bu yüzden browser geçici olarak bağlantıyı kaybetse bile update sağlıklı ilerliyor olabilir.

## İlk Müdahale

1. [Güncellemeler](../../docs/tr/screen-updates.md) ekranını açın ve refresh yapmadan önce job detail'i görünür bırakın.
2. Tekrar denemeden önce beklenen service restart penceresinin bitmesini bekleyin.
3. VaultPilot'ı tekrar açıp UI veya server status üzerinden çalışan versiyonu kontrol edin.
4. Update job detail içinde final state, MSI path, SHA-256 ve signer durumunu inceleyin.
5. Job uzlaşmıyorsa Windows Installer event log ve verbose MSI log kontrolüne geçin.
6. Latest release manifest'in beklenen MSI ve SHA-256 hash'e işaret ettiğini doğrulayın.

## Neyi Kontrol Etmeli

| Kanıt | Sağlıklı sinyal | Sorun sinyali |
| --- | --- | --- |
| Release manifest | Signature, version ve package URL hedef release ile eşleşir. | Manifest beklenmedik değişmiş veya doğrulanamıyor. |
| Package hash | SHA-256 manifest ile eşleşir. | Hash mismatch, eksik package veya partial download var. |
| Signer | Signer thumbprint pinned manifest evidence ile eşleşir. | Bilinmeyen signer veya yalnız local trust'a dayanan signer var. |
| Windows Installer | Service restart ve install completion event görünür. | Installer error, rollback veya completion event eksik. |
| Job state | Service geri geldikten sonra job reconcile olur. | Server reachable olduğu halde job stale kalır. |

## Güvenli Kanıt

- Update öncesi ve sonrası VaultPilot version.
- Update job id yer tutucusu, durum, yüzde ve final error category.
- MSI filename, SHA-256 ve signature status.
- Redakte Windows Installer event id ve timestamp.
- Servisin restart edip tekrar online olup olmadığı.

## Yapmayın

Manifest doğrulamasını bypass etmeyin, MSI'ı manuel değiştirmeyin, signer trust'ı değiştirmeyin, database job row edit etmeyin ve local path, username veya secret içerebilecek raw logları public paylaşmayın.

İlgili: [Güncellemeler ekranı](../../docs/tr/screen-updates.md), [Update Center](../../docs/tr/update-center.md), [Yayın dosyası doğrulama](../../docs/tr/release-asset-verification.md), [Publication runbook](../../docs/tr/publication-runbook.md).
