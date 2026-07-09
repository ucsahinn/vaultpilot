# Discovery Bulgu İnceleme

Discovery bir secret exposure sinyali gösterdiğinde, import kapalı göründüğünde veya operatör bir bulgunun vault kaydına dönüşüp dönüşmemesi gerektiğinden emin olmadığında bu makaleyi kullanın.

## Belirti

- Discovery parola, API key, sertifika/key, credential, not veya dosya adayı gösterir.
- Bulgu gerçek görünüyor, fakat evidence maskelidir.
- Import adımında bulgu görünmez.
- Import kullanılabilir, ancak güvenli karar yolu gerekir.

## İlk Kontroller

| Kontrol | Beklenen sonuç |
| --- | --- |
| Scope onayı | Scan policy onaylı private network, Windows folder preset, local path veya SMB path gösterir. |
| Dosya onayı | File scan için açık read-only onayı vardır. |
| Bulgu durumu | Import adımında yalnızca ready for import işaretli bulgular görünür. |
| Evidence kalitesi | Güçlü sinyaller detector id, candidate type, masked path, path hash ve redacted evidence gösterir. |
| Kasa durumu | Import için kasa açık olmalıdır, çünkü değer tarayıcıda şifrelenir. |
| Sahiplik | Kaynak sahibi değerin yalnızca dosyada kalmak yerine VaultPilot içine alınmasını onaylar. |

## Güvenli Çözüm Yolu

1. Finding drawer'ı aç.
2. Detector id, candidate type, severity, confidence, masked path, path hash ve evidence hash değerlerini doğrula.
3. Gürültüyse Ignore veya gerekçeli Suppress kullan.
4. Gerçek fakat vault'a alınmaması gereken bir bulguysa operasyon kararını public yorum dışında kaydet.
5. Vault item olmalıysa ready for import işaretle.
6. Hedef kasayı aç.
7. Import adımıyla şifreli vault kaydını oluştur.
8. Scan, review, import preparation ve import completion audit event'lerini kontrol et.

## Gönderilebilecek Güvenli Kanıt

- VaultPilot ve bileşen sürümü.
- Scan adı ve zamanı.
- Detector id, severity, confidence, candidate type, review status, path hash ve evidence hash.
- Drawer içinde görünen redacted evidence.
- Import sırasında kasanın kilitli mi açık mı olduğu.

## Göndermeyin

- Bulguyu üreten kaynak dosyalar.
- Müşteri veya altyapı adı içeren maskesiz path'ler.
- Plaintext secret, token, private key, connection string veya vault export.
- Database, yedek, PFX/P12 paketi veya secret içerebilen ham log.

## Ne Zaman Eskale Edilir

- Bulgu ready durumdayken ve kasa açıkken import başarısız olursa.
- Gerekçeli suppression sonrası aynı bulgu tekrar ederse.
- Scanner reddedilmesi gereken sistem path'i, VaultPilot data path'i veya legacy PassMan data path'i raporlarsa.
- Audit trail review veya import aksiyonunu göstermiyorsa.

İlgili: [Discovery rehberi](../../docs/tr/discovery.md), [Güvenlik ve güven modeli](../../docs/tr/security-and-trust-model.md), [Destek kanıt paketi](../../docs/tr/support-evidence-pack.md).
