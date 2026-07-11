# Güvenlik Komuta Merkezi Ekranı

Üst çubuktaki `?` simgesi bu yardımı Güvenlik Komuta Merkezi açıkken getirir. Burası VaultPilot'ta “önce nereye bakmalıyım?” sorusunun cevabıdır: güvenlik skoru, öncelikli öneriler, sunucu hazırlığı ve operasyon sinyalleri aynı çalışma alanında bir araya gelir. Bütün sistem rolleri ekranı açabilir; görülebilen veri ve hedef işlemler role göre daralır. Tek başına olay raporu ya da değişiklik onayı değildir.

Komuta Merkezi veriyi değiştirmekten çok doğru ayrıntı ekranına götürür. Bir öneriye veya faktöre bastığınızda Parolalar, Active Directory kayıtları, Giriş Güvenliği, Entegrasyonlar, Lisans ya da Güncelleme Merkezi açılır; uygun olduğunda ilgili filtre de hazırlanır.

## Ekranda Neler Görürsünüz

- **Güvenlik skoru:** 2FA, lisans modu, tarayıcı eklentisi, Update Center, parola sızıntısı kontrolü, Active Directory riski, sertifikalardaki sona-erme tarihi meta verisinin eksiksizliği, başarısız işlemler, dizin sağlayıcılarının bildirdiği eşitleme hataları ve kasa içeriği olmak üzere on ağırlıklı faktörden hesaplanır. Sertifika faktörü gerçek geçerlilik/sona erme testi, dizin faktörü genel bağlantı testi değildir. Skoru tek başına “güvenli” kararı saymayın.
- **Kritik ve izlenecek öneriler:** Ana yüzey iki kritik ve iki izlenecek satır gösterir. **Daha fazla öneri (n)**, kalan sıralı kuyruğu açar; buradaki satırlar da doğrudan hedef ekrana gider.
- **Skor kaynakları ve dashboard bölümleri:** Güvenlik, etki alanı, sertifika ve rotasyon ekranlarına doğrudan geçiş sağlar.
- **Güncel operasyon sinyalleri:** Dosya kotası, işlem durumu ve güncelleme hazırlığı gibi canlı özetleri gösterir.
- **Ekran araçları:** Canlı veriyi yenileyebilir, ilgili dokümanı açabilir ve dashboard görünümünü yönetebilirsiniz.

## Yetki ve Ön Koşullar

Sahip, Yönetici, Denetçi ve Kullanıcı ekranı açabilir; fakat bazı sistem sorguları, hedef ekranlar ve eylemler yetkisiz rolde boş, kısıtlı veya pasif kalır. Kasa kayıtlarına yönlenen ayrıntılar için kilidi açılmış kasa ve gizli kayıt kullanmaya izin veren sistem/kasa rolü gerekir; Denetçi kasa içeriklerini açamaz. Salt okunur lisans kasa kaydı oluşturan veya değiştiren işlemleri kapatır. Lisans ve Entegrasyonlar yalnız Sahibe, Sunucu Ayarları okuma Sahip/Yönetici/Denetçiye, sunucu değişiklikleri ise Sahibe özgü kapılar uygulayabilir.

## Önerilen Çalışma Akışları

### Günlük güvenlik kontrolü

1. Skoru, kazanılan/toplam ağırlığı ve açık öneri sayısını birlikte okuyun; bu ekranda bağımsız bir “skor güncellik” işareti yoktur.
2. **Kritik** bölümündeki ilk satırı açın; VaultPilot ilgili ekranı ve varsa hazır filtreyi getirir.
3. Ayrıntı ekranında sebebi doğrulayın, işlemi orada tamamlayın ve Komuta Merkezi'ne dönüp yenileyin.

Beklenen sonuç, önerinin sağlıklı duruma geçmesi veya yapılacak işin açıkça sahiplenilmesidir. Yenilemeden sonra aynı uyarı sürüyorsa art arda kör değişiklik yapmayın; kaynak ekranındaki hata ve zaman bilgisini inceleyin.

### Düşen skorun nedenini bulma

En düşük veya uyarı tonundaki skor kaynağını seçin. 2FA, lisans, eklenti, güncelleme, sızıntı, AD riski, sertifika sona-erme meta verisi, işlem geçmişi, dizin sağlayıcı hatası ve kasa içeriği nedenlerini birbirinden ayırın; hedef ekranda veriyi doğrulayın. Sonuç tek bir somut kontrole bağlanamıyorsa burada durun ve Sunucu Ayarları/İşlemler üzerinden sistem sağlığını kontrol edin.

### Bir öneriyi operasyon işine dönüştürme

Öneriyi açın, hedef ekrandaki kaydı veya bileşeni doğrulayın, sorumluyu ve yapılacağı zamanı kurum içi değişiklik kaydına ekleyin. Komuta Merkezi önerilerinde gizleme veya kapatma düğmesi yoktur; tamamlanma ölçütü kaynak kontrolde düzelme ve sonraki yenilemede önerinin kuyruktan çıkmasıdır.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Yükleniyor | Kartlar tamamlanana kadar skor veya sayı üzerinden karar vermeyin; uzun sürerse bir kez yenileyin. |
| 82–100 | Skor yeşil banttadır; yine de açık öneri sayısını ve her faktörün ağırlığını kontrol edin. |
| 62–81 | Skor uyarı bandındadır; en yüksek puan etkili satırı hedef ekranında doğrulayın. |
| 0–61 | Skor kritik banttadır; doğrudan erişim riskini önce sınırlayın ve olayı özel sürece taşıyın. |
| Daha fazla öneri | Görünmeyen kuyruğu açın; ilk dört satır bütün açık işleri temsil etmeyebilir. |
| Hazırlık sinyali eksik | Profil, aktif kasa, 2FA, lisans, eklenti veya Update Center hedefini açıp kaynağında doğrulayın. |
| Yetki kısıtlı | Hedef ekran ya da eylem pasifse rolü ve kasa üyeliğini normal yetkilendirme sürecinden doğrulayın. |
| Hata | Mesajı, zamanı ve etkilenen bileşeni kaydedin; sürekli yenileyerek ilk kanıtı kaybetmeyin. |

## İşlemden Önce

- Uyarının tek bir kasayı mı, kullanıcı oturumunu mu, lisansı mı yoksa sunucu bileşenini mi etkilediğini belirleyin.
- Ekrandaki yönlendirmeyi kullanın; sızıntı ve risk filtresi bu yolla hedef ekrana taşınır.
- Bir **kasa kaydını** yazmadan önce aktif kasa rolünün **Editor** veya **Manager** olduğunu ve lisansın salt okunur olmadığını doğrulayın. Sunucu/lisans/entegrasyon hedeflerinde kasa rolü yerine hedef ekranın kendi sistem rolü ve lisans kuralları geçerlidir.
- Birden fazla kritik sinyal varsa önce 2FA ve bilinen sızıntı gibi doğrudan erişim risklerini ele alın.
- Komuta Merkezi sayısını nihai denetim kanıtı saymayın; ilgili kayıt, denetim olayı veya işlem sonucunu doğrulayın.

## Güvenli Kanıt

- **Paylaşılabilir:** genel skor bandı, öneri kategorisi, etkilenen VaultPilot bileşeni, redakte hata kodu, gözlem zamanı ve yönlendirilen ekranın adı.
- **Gizli kalmalı:** kullanıcı ve kasa adları, gerçek kayıt başlıkları, dahili etki alanı ve sunucu adları, müşteri sayıları, erişim zaman çizgileri ve gizli değer gösterebilecek ekran görüntüleri.
- Görsel gerekiyorsa yalnız ilgili kartı alın; gezinme, kullanıcı, host ve kayıt bağlamını maskeleyin. Ortam tamamen anonimleştirilemiyorsa public issue yerine private support kullanın.

## Ne Zaman Durmalı veya Yükseltmeli

Aynı kritik sinyal doğrulanmış bir düzeltmeden sonra geri geliyorsa, skor kaynakları yüklenmiyorsa, denetim verisi ile dashboard özeti çelişiyorsa veya risk birden fazla kullanıcıyı etkiliyorsa olayı kurum içi güvenlik sorumlusuna taşıyın. Destek paketine gizli değer değil; saat dilimiyle zaman, sürüm, bileşen, izlenen adımlar ve redakte hata bilgisi ekleyin.

## Operatör Notları

Komuta Merkezi karar vermeyi hızlandırır; ayrıntı ekranlarının yerine geçmez ve öneri kartlarını gizleme denetimi sunmaz. Sonucu her zaman hedef ekranda ve gerekiyorsa Denetim Kaydı'nda doğrulayın.

## İlgili

- [Denetim ve güvenlik duruşu](audit-and-security-posture.md)
- [Güvenlik ve güven modeli](security-and-trust-model.md)
- [Güvenlik Dashboard ekranı](screen-security-dashboard.md)
- [Operasyon runbook](operator-runbook.md)
