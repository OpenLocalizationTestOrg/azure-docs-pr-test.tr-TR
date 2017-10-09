---
title: "aaaAzure veritabanı güvenlik denetim listesi | Microsoft Docs"
description: "Bu makalede, bir dizi denetim listesi için Azure veritabanı güvenlik sağlar."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: tomsh
ms.openlocfilehash: 5e3a69591df3c8508a8707a2d47068342863ce93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-checklist"></a>Azure veritabanı güvenlik denetim listesi

toohelp güvenliği geliştirmek için Azure veritabanı toolimit kullanın ve erişimi denetleme yerleşik güvenlik denetimlerini içerir.

Bunlar:

-   Toocreate sağlayan bir güvenlik duvarı [güvenlik duvarı kuralları](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-firewall-configure) IP adresine göre bağlantı sınırlaması
-   Sunucu düzeyinde güvenlik duvarı hello Azure portal ' erişilebilir
-   Veritabanı düzeyinde güvenlik duvarı kuralları SSMS erişilebilir
-   Güvenli bağlantı dizeleri kullanılarak güvenli bağlantı tooyour veritabanı
-   Access management kullanma
-   Veri şifrelemesi
-   SQL veritabanı denetimi
-   SQL veritabanı tehdit algılama

## <a name="introduction"></a>Giriş
Bulut bilgi işlem tanınmayan toomany uygulama kullanıcıları, Veritabanı yöneticileri ve programcıları yeni güvenlik örneklerinde gerektirir. Sonuç olarak, bazı kuruluşlar şüpheli tooimplement tooperceived güvenlik riskleri nedeniyle veri yönetimi için bir bulut Altyapısı ' dir. Ancak, bu sorunu çoğunu Microsoft Azure ve Microsoft Azure SQL veritabanı yerleşik hello güvenlik özelliklerinin daha iyi anlamasına aracılığıyla alleviated.

## <a name="checklist"></a>Denetim listesi
Merhaba okumanızı öneririz [Azure veritabanı en iyi güvenlik uygulamaları](https://docs.microsoft.com/en-us/azure/security/azure-database-security-best-practices) bu denetim önceki tooreviewing makalesi. Merhaba en iyi yöntemler anladıktan sonra bu denetim dışında en mümkün tooget hello olacaktır. Daha sonra Azure veritabanı güvenlik hello önemli sorunlar ele aldık emin bu denetim listesi toomake kullanabilirsiniz.


|Denetim listesi kategorisi| Açıklama|
| ------------ | -------- |
|**Veri koruma**||
| <br> Hareket/Aktarımdaki şifreleme| <ul><li>[Aktarım Katmanı Güvenliği](https://docs.microsoft.com/en-us/windows-server/security/tls/transport-layer-security-protocol), veri toohello ağlara taşırken veri şifreleme için.</li><li>Veritabanı üzerinde hello tabanlı istemcilerden güvenli iletişim gerektiren [TDS (tablo veri akışı)](https://msdn.microsoft.com/en-in/library/dd357628.aspx) protokolü üzerinden TLS (Aktarım Katmanı Güvenliği).</li></ul> |
|<br>Bekleme sırasında şifreleme| <ul><li>[Saydam veri şifreleme](http://go.microsoft.com/fwlink/?LinkId=526242), etkin olmayan verileri fiziksel olarak dijital biçimde depolanır.</li></ul>|
|**Erişimi denetleme**||  
|<br> Veritabanı Erişimi | <ul><li>[Kimlik doğrulama](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-control-access) (Azure Active Directory kimlik doğrulaması) AD kimlik doğrulaması Azure Active Directory tarafından yönetilen kimlikleri kullanır.</li><li>[Yetkilendirme](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-control-access) kullanıcılar gerekli en düşük ayrıcalık hello verin.</li></ul> |
|<br>Uygulama erişimi| <ul><li>[Satır düzeyi güvenlik](https://msdn.microsoft.com/library/dn765131) (kullanılarak güvenlik ilkesi, aynı anda satır düzeyi erişimi kısıtlama dayalı bir kullanıcının kimliği, rolü veya yürütme bağlamı hello).</li><li>[Dinamik veri maskeleme](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-dynamic-data-masking-get-started) (kullanma izni & İlkesi sınırları gizli verilerin açığa toonon ayrıcalıklı kullanıcılar maskeleyerek)</li></ul>|
|**Öngörülü izleme**||  
| <br>İzleme & algılama| <ul><li>[Denetim](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-auditing) veritabanı olaylarını izler ve tooan denetim günlüğünü Yazar / etkinlik oturum açma, [Azure depolama hesabı](https://docs.microsoft.com/en-us/azure/storage/storage-create-storage-account).</li><li>İzleme Azure veritabanı sistem durumu kullanarak [Azure monitör etkinliği günlükleri](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs).</li><li>[Tehdit algılama](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-threat-detection) olası güvenlik tehditlerine toohello veritabanı gösteren anormal veritabanı etkinliklerini algılar. </li></ul> |
|<br>Azure Güvenlik Merkezi| <ul><li>[Veri izleme](https://docs.microsoft.com/en-us/azure/security-center/security-center-enable-auditing-on-sql-databases) çözüm SQL ve diğer Azure Hizmetleri için izlemeyi Merkezi güvenlik Azure Güvenlik Merkezi'ni kullanın.</li></ul>|     

## <a name="conclusion"></a>Sonuç
Azure veritabanı birçok kuruluş ve yasal uyumluluk gereksinimlerinin karşılanmasına güvenlik özelliklerinin tam aralıklı bir sağlam veritabanı platformudur. Merhaba fiziksel erişimi tooyour veri denetleme ve hello dosya, sütun veya satır düzeyinde saydam veri şifreleme, hücre düzeyi şifreleme veya satır düzeyi güvenlik, veri güvenliği için çeşitli seçenekler kullanarak verileri kolayca koruyabilir. Her zaman şifreli ayrıca işlemlerini şifrelenmiş veriler karşı uygulama güncelleştirmeleri hello işlemi basitleştirme sağlar. Sırayla, SQL veritabanı etkinliği erişim tooauditing günlükleri sağlar nasıl ve ne zaman verilere erişildiğinde tooknow izin vererek gereksinim hello bilgilerle.

## <a name="next-steps"></a>Sonraki adımlar
Kötü amaçlı kullanıcılar ya da yalnızca birkaç basit adımla yetkisiz erişime karşı veritabanınızın hello koruma artırabilir. Bu öğreticide, öğrenin:

- Ayarlanan [güvenlik duvarı kuralları](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-firewall-configure) sunucu ve veya veritabanı için.
- Verilerinizin korunmasına [şifreleme](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/sql-server-encryption).
- Etkinleştirme [SQL veritabanı denetimi](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-auditing).

