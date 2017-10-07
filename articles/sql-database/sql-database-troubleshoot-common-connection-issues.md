---
title: "aaaTroubleshoot ortak bağlantı sorunları tooAzure SQL veritabanı"
description: "Adımları tooidentify ve çözümleme ortak bağlantı hatalarını Azure SQL veritabanı için."
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: ac463d1c-aec8-443d-b66e-fa5eadcccfa8
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: eb5f2d7b123a76942c7e4a84a7f475344fbcb144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-connection-issues-tooazure-sql-database"></a>Bağlantı sorunları tooAzure SQL veritabanı sorunlarını giderme
Merhaba bağlantı tooAzure SQL veritabanı başarısız olduğunda, aldığınız [hata iletileri](sql-database-develop-error-messages.md). Bu makalede, Azure SQL veritabanı bağlantı sorunları gidermenize yardımcı olan merkezi bir konudur. Tanıttığı [hello yaygın nedenler](#cause) bağlantı sorunları, önerir [bir sorun giderme aracı](#try-the-troubleshooter-for-azure-sql-database-connectivity-issues) , kimlik hello sorun yardımcı olur ve sorun giderme adımları toosolve sağlar [ geçici hataları](#troubleshoot-transient-errors) ve [kalıcı veya geçici olmayan hata](#troubleshoot-persistent-errors). 

Merhaba bağlantı sorunlarıyla karşılaşırsanız hello deneyin sorun giderme bu makalede açıklanan adımları.
[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="cause"></a>Nedeni
Bağlantı sorunları aşağıdakilerden herhangi birini hello tarafından kaynaklanabilir:

* Hata tooapply en iyi yöntemler ve tasarım yönergeleri hello uygulama tasarım işlemi sırasında.  Bkz: [SQL veritabanı geliştirme genel bakış](sql-database-develop-overview.md) tooget başlatıldı.
* Azure SQL veritabanı yeniden yapılandırma
* Güvenlik duvarı ayarları
* Bağlantı zaman aşımı
* Hatalı oturum açma bilgileri
* Bazı Azure SQL veritabanı kaynaklardaki maksimum sınırına ulaştı

Genellikle, bağlantı sorunları tooAzure SQL veritabanı şu şekilde sınıflandırılabilir:

* [Geçici hataları (kısa süreli veya aralıklı)](#troubleshoot-transient-errors)
* [Kalıcı veya geçici olmayan hatalar (düzenli olarak yinelenmesini hatalar)](#troubleshoot-persistent-errors)

## <a name="try-hello-troubleshooter-for-azure-sql-database-connectivity-issues"></a>Azure SQL veritabanı bağlantı sorunları için Hello sorun gidericisini deneyin
Belirli bağlantı hatayla karşılaşırsanız, deneyin [bu aracı](https://support.microsoft.com/help/10085/troubleshooting-connectivity-issues-with-microsoft-azure-sql-database), hangi kimlik hızlı bir şekilde Yardım ve sorununuzu.

## <a name="troubleshoot-transient-errors"></a>Geçici hataları giderme

Bir uygulama tooan Azure SQL veritabanına bağlandığında, hello aşağıdaki hata iletisini alıyorsunuz:

```
Error code 40613: "Database <x> on server <y> is not currently available. Please retry hello connection later. If hello problem persists, contact customer support, and provide them hello session tracing ID of <z>"
```

> [!NOTE]
> Bu hata iletisini genellikle geçicidir (kısa süreli).
> 
> 

Bu hata hello Azure veritabanı yükleniyor oluşur taşındı (veya yeniden yapılandırılması) ve bağlantı toohello SQL veritabanını uygulamanızı kaybeder. SQL veritabanı yeniden yapılandırma olayları olay (örneğin, bir yazılım yükseltmesi) veya planlanmamış bir olay (örneğin, bir işlem kilitlenme veya Yük Dengeleme) nedeniyle oluşur. Çoğu yeniden yapılandırma olaylar genelde kısa ömürlüdür ve 60 saniyeden daha kısa bir süre içinde en çok tamamlanmalıdır. Ancak, bu olaylar bazen büyük bir işlem uzun süre çalışan kurtarma sebep olduğunda gibi daha uzun toofinish alabilir.

### <a name="steps-tooresolve-transient-connectivity-issues"></a>Adımları tooresolve geçici bağlantı sorunları

1. Merhaba denetleyin [Microsoft Azure hizmet Panosu'nu](https://azure.microsoft.com/status) hangi hello sırasında hatalar önceden raporlanan hello uygulama tarafından hello süre boyunca gerçekleşen tüm bilinen kesintiler için.
2. Azure SQL veritabanı düzenli aralıklarla yeniden yapılandırma olayları beklediğiniz ve uygulamak gibi tooa bulut hizmetine uygulamalar, uygulama hataları toousers olarak görünmesini yerine bu hataları mantığı toohandle yeniden deneyin. Gözden geçirme hello [geçici hataları](sql-database-connectivity-issues.md) bölüm hello en iyi yöntemler ve tasarım yönergeleri [SQL veritabanı geliştirme genel bakış](sql-database-develop-overview.md) daha fazla bilgi ve genel stratejileri yeniden deneyin. Ardından, kod örnekleri, bkz: [SQL Database ve SQL Server için bağlantı kitaplıkları](sql-database-libraries.md) özellikleri için.
3. Bir veritabanı kaynak sınırlarına yaklaştığında toobe geçici bir bağlantı sorunu görünebilir. Bkz: [performans sorunlarını giderme](sql-database-troubleshoot-performance.md).
4. Bağlantısı sorunları devam ya da hello uygulamanızı hello hatayla karşılaştığında süresi 60 saniye aşarsa dosya ya da belirli bir gün içinde birden çok tekrarı hello hata görürseniz, bir Azure destek isteği seçerek **destekalın** hello üzerinde [Azure Destek](https://azure.microsoft.com/support/options) site.

## <a name="troubleshoot-persistent-errors"></a>Kalıcı hatalarında sorun giderme
Merhaba uygulaması tooconnect tooAzure SQL veritabanına kalıcı olarak başarısız olursa, genellikle hello aşağıdakilerden biri ile ilgili bir sorunu gösterir:

* Güvenlik duvarı yapılandırması. Hello Azure SQL veritabanı veya istemci tarafı Güvenlik Duvarı bağlantılarını tooAzure SQL veritabanı engelliyor.
* Ağ yeniden yapılandırma hello istemci tarafında: Örneğin, yeni bir IP adresi veya bir proxy sunucu.
* Kullanıcı hatası: Örneğin, hello sunucu adı bağlantı dizesinde hello gibi bağlantı parametrelerini yanlış yazdınız.

### <a name="steps-tooresolve-persistent-connectivity-issues"></a>Adımları tooresolve kalıcı bağlantı sorunları
1. Ayarlanan [güvenlik duvarı kuralları](sql-database-configure-firewall-settings.md) tooallow hello istemci IP adresi. Geçici sınama amacıyla, IP adresi aralığı başlangıç ve bitiş IP adresi aralığı hello 255.255.255.255 kullanarak hello olarak 0.0.0.0 kullanarak bir güvenlik duvarı kuralı ayarlayın. Bu hello sunucu tooall IP adreslerini açar. Bu bağlantı sorunu çözümlenirse, bu kuralı kaldırmak ve uygun şekilde sınırlı IP adresi veya adres aralığı için bir güvenlik duvarı kuralı oluşturun. 
2. Tüm güvenlik duvarlarında hello Internet ile Merhaba istemci arasında bağlantı noktası 1433 giden bağlantılar için açık olduğundan emin olun. Gözden geçirme [hello Windows Güvenlik Duvarı tooAllow SQL Server erişimi yapılandırma](https://msdn.microsoft.com/library/cc646023.aspx) ve [karma kimlik gerekli bağlantı noktalarını ve protokolleri](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-ports) tooadditional noktaları ek işaretçileri ilgili için tooopen gerekir Azure Active Directory kimlik doğrulaması.
3. Bağlantı dizenizi ve diğer bağlantı ayarlarını doğrulayın. Bkz: hello hello bağlantı dizesi bölümünde [bağlantı sorunları konu](sql-database-connectivity-issues.md#connections-to-azure-sql-database).
4. Merhaba panosunda hizmet durumunu kontrol edin. Bölgesel bir kesintinin olduğunu düşünüyorsanız, bkz: [bir kesintisinden kurtarma](sql-database-disaster-recovery.md) adımları toorecover tooa yeni bölge için.

## <a name="next-steps"></a>Sonraki adımlar
* [Azure SQL veritabanı performans sorunlarını giderme](sql-database-troubleshoot-performance.md)
* [Microsoft Azure arama hello belgeler](http://azure.microsoft.com/search/documentation/)
* [Görünüm hello toohello Azure SQL veritabanı hizmetinin en son güncelleştirmeleri](http://azure.microsoft.com/updates/?service=sql-database)

## <a name="additional-resources"></a>Ek kaynaklar
* [SQL veritabanı geliştirme genel bakış](sql-database-develop-overview.md)
* [Genel geçici hata işleme Kılavuzu](../best-practices-retry-general.md)
* [SQL Database ve SQL Server için bağlantı kitaplıkları](sql-database-libraries.md)

