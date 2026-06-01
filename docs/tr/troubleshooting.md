# Sorun Giderme

## MSI kurulumu başarısız

Kontrol edin:

- MSI administrator olarak mı çalışıyor?
- Port kullanımda mı?
- `C:\ProgramData\PassMan\logs` altında installer log var mı?
- Windows servis durumu nedir?

## Sunucu açılmıyor

1. Sunucuda `https://127.0.0.1:1903/api/profile` kontrol edin.
2. `PassManServer` servis durumunu kontrol edin.
3. Firewall ve port yönlendirmesini doğrulayın.
4. Server loglarını redacted olarak inceleyin.

## DC Agent bağlanmıyor

- Agent makinesinden `<PASSMAN_URL>` erişimini test edin.
- `-Status` ile config/service/log durumunu görün.
- Bind username formatını domain ile birlikte kullanın.
- Token veya password değerlerini loga yazmayın.

## Extension eşleşmesi pending kalıyor

- Pairing code süresi dolmuş olabilir.
- Yanlış kullanıcı adı girilmiş olabilir.
- Kullanıcının açık kasası olmayabilir.
- Cihaz PassMan panelinde onay bekliyor olabilir.

## Update yüzde 76 civarında kalıyor

MSI servis restart aşamasında olabilir. Servis geri geldikten sonra Update Center tekrar açıldığında hedef versiyon, installer log ve running version üzerinden durum uzlaştırılır. Hata devam ederse verbose MSI loglarını inceleyin.
