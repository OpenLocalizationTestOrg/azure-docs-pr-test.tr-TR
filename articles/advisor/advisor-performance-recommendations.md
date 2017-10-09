---
title: "aaaAzure Danışmanı performans önerileri | Microsoft Docs"
description: "Advisor toooptimize hello Azure dağıtımlarınızı performansını kullanın."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: eb3d928664717f6f322132ac740f42015f56b76e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-performance-recommendations"></a>Advisor performans önerileri

Azure Danışmanı performans önerileri hello hızı ve kritik iş uygulamalarının yanıtlama hızını geliştirilmesine yardımcı olun. Merhaba üzerinde danışmanına performans önerileri alabilirsiniz **performans** hello Danışmanı Pano sekmesi.

![Advisor performans sekmesi](./media/advisor-performance-recommendations/advisor-performance-tab.png)

## <a name="improve-database-performance-with-sql-db-advisor"></a>SQL DB Danışmanı ile veritabanı performansı

Advisor önerileri tüm Azure kaynakları için tutarlı, birleştirilmiş bir görünümünü sağlar. Bu SQL veritabanı Danışmanı toobring ile SQL Azure veritabanı hello performansı artırmak için öneriler tümleştirir. SQL veritabanı Danışmanı'nı kullanım geçmişiniz çözümleyerek SQL Azure veritabanlarınızı hello performansını değerlendirir. Ardından, hello veritabanının tipik iş yükünü çalıştırmak için en uygun öneriler sunar. 

> [!NOTE]
> tooget öneriler, bir veritabanı kullanımı haftada hakkında sahip olması gerekir ve bu hafta içinde var. bazı tutarlı etkinlik olması gerekir. SQL veritabanı Danışmanı daha kolay rastgele WINS'e etkinlik için tutarlı bir sorgu modelleri için en iyi duruma getirebilirsiniz.

SQL Database Advisor hakkında daha fazla bilgi için bkz: [SQL veritabanı Danışmanı'nı](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).

![SQL veritabanı önerileri](./media/advisor-performance-recommendations/advisor-performance-sql.png)

## <a name="improve-redis-cache-performance-and-reliability"></a>Redis önbelleği performansı ve güvenilirliği iyileştirmek

Advisor burada performansını olumsuz yönde yüksek bellek kullanımı, sunucu iş yükü, ağ bant genişliği veya çok sayıda istemci bağlantıları tarafından etkilenebilir Redis önbelleği örnekleri tanımlar. Danışmanı da iyi sağlar olası sorunları önlemek önerileri toohelp yöntemler. Redis önbelleği öneriler hakkında daha fazla bilgi için bkz: [Redis önbelleği Danışmanı](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).


## <a name="improve-app-service-performance-and-reliability"></a>Uygulama hizmeti performans ve güvenilirlik geliştirmek

Azure Danışmanı uygulama hizmetleri deneyiminizi geliştirmek ve ilgili platform özelliklerini keşfetmek için en iyi uygulama önerilerini tümleştirir. Uygulama Hizmetleri önerileri örnekleri şunlardır:
* Algılama, bellek veya CPU kaynaklarını azaltma seçenekleri ile uygulama çalışma zamanları tarafından tükendiği örnekleri.
* Burada collocating kaynakları web uygulamaları ve veritabanları gibi örneklerinin algılama, performans ve düşük maliyetli artırabilir. 

Uygulama Hizmetleri öneriler hakkında daha fazla bilgi için bkz: [Azure App Service için en iyi uygulamaları](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).
![Uygulama Hizmetleri önerileri](./media/advisor-performance-recommendations/advisor-performance-app-service.png)

## <a name="how-tooaccess-performance-recommendations-in-advisor"></a>Nasıl tooaccess Danışmanı performans önerileri

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).

2. Merhaba sol bölmede **daha fazla hizmet**.

3. Hello menü bölmesi altında hizmet **izleme ve Yönetim**, tıklatın **Azure Danışmanı**.  
 Merhaba Danışmanı Panosu görüntülenir.

4. Hello Danışmanı Panoda hello tıklatın **performans** sekmesi.

5. Kendisi için tooreceive önerileri istediğiniz ve ardından hello aboneliği seçin **alma önerileri**.

> [!NOTE]
> tooaccess Advisor önerileri, şunları yapmalısınız ilk *aboneliğinizi kaydetmek* Danışmanı ile. Bir abonelik kayıtlı olduğunda bir *abonelik sahibi* başlatır hello Danışmanı Pano ve tıklama hello **alma önerileri** düğmesi. Bu bir *tek seferlik işlem*. Merhaba abonelik kaydedildikten sonra Advisor önerileri olarak erişebilir *sahibi*, *katkıda bulunan*, veya *okuyucu* abonelik, bir kaynak grubu için veya bir belirli kaynak.

## <a name="next-steps"></a>Sonraki adımlar

Advisor önerileri hakkında daha fazla toolearn bakın:

* [Giriş tooAdvisor](advisor-overview.md)
* [Danışman’ı kullanmaya başlama](advisor-get-started.md)
* [Advisor maliyet önerileri](advisor-performance-recommendations.md)
* [Advisor yüksek kullanılabilirlik önerileri](advisor-high-availability-recommendations.md)
* [Advisor güvenlik önerileri](advisor-security-recommendations.md)

