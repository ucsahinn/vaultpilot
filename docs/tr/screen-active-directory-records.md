# Active Directory Kayıtları Ekranı

Üst çubuktaki `?` bu sayfayı Active Directory kayıtları ekranından açar. Dizin kaynaklı kimlik bilgilerini, hesap meta verilerini ve kayıt sahipliği incelemesini burada yönetin.

## Burada Ne Yapılır

- Kayıt sahipliğini değiştirmeden önce kayıt kaynağını, domain'i, hesap durumunu ve son eşitleme bilgisini doğrulayın.
- Disabled, locked, expired veya privileged dizin sinyallerini inceleme nedeni olarak ele alın.
- Kaydın bayat olduğunu varsaymadan önce DC Agent sağlık yolunu kontrol edin.

## Ekran Durumları

| Durum | Operatör cevabı |
| --- | --- |
| Sync tamam | Kayıt kullanılmadan önce sahip ve son eşitleme bilgisini inceleyin. |
| Kaynak yok | Kasa durumunu değiştirmeden önce kaynak hesabın hâlâ var olduğunu doğrulayın. |
| Conflict | Manuel düzenleme öncesi dizindeki kaynak kaydı netleştirin. |

## İşlemden Önce

- Kaydın bayat olduğuna karar vermeden önce kasa kaydını provider durumuyla karşılaştırın.
- Credential'ın synced, manuel imported veya review bekleyen durumda olup olmadığını kontrol edin.
- Sahip, kasa ataması veya review durumu değişirken provider kanıt izini koruyun.

## Güvenli Kanıt

- Paylaşılabilir: kayıt durumu, son eşitleme aralığı, provider sağlık kategorisi ve redakte review kararı.
- Gizli kalmalı: distinguished name, OU path, domain adı, bind account, agent ID, agent token ve ham directory tree ekran görüntüleri.
- Sahiplik, ayrıcalıklı hesap durumu veya kaynak kayıt çakışması redakte metadata ile açıklanamıyorsa private support kullanın.

## Operatör Notları

Distinguished name, OU path, domain adı, agent ID, agent token veya gerçek hesap meta verisi içeren ekran görüntüsü yayınlamayın.

## İlgili

- [Etki Alanı dashboard ekranı](screen-domain-dashboard.md)
- [Active Directory ajanı](active-directory-agent.md)
- [DC Agent sorun giderme](../../kb/tr/dc-agent-service.md)
