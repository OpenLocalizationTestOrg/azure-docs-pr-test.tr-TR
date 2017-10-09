---
title: "SQL veritabanı müşteri uygulamaları-teknik aaaAzure | Microsoft Docs"
description: "Teknik Ayrıntılar müşteri implementatons Azure SQL veritabanı toosolve iş sorunları hakkında bilgi edinin"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 00c8a713-f20c-4d6b-b8b7-0c1b9ba5f05b
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/03/2017
ms.author: carlrab
ms.openlocfilehash: 84feb0d7407062dab49508a649797230c9491b78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-customer-implementation-technical-studies"></a>Azure SQL veritabanı müşteri uygulaması teknik incelemeleri

- [Daxko](sql-database-implementation-daxko.md): Daxko/CSI yazılım karşılaştığı bir sınama: uygunluk ve dinlenme merkezlerinin müşteri tabanı, hızlı bir şekilde, teşekkürler toohello kapsamlı Kurumsal yazılım çözümünün başarısını büyüyen ancak BT altyapısı ile Merhaba tutmaktan gerekiyor büyüyen bir müşteriye ait temel hello şirketin test BT personeli. Hello şirket gittikçe büyüyen veritabanlarını yönetmek için özellikle yükselen işlemlerinin yükünü kısıtlanmış. Da kötüsü, bu işlem yükünü hello şirketin yazılım yeni mobility özellikleri gibi yeni girişimleri için geliştirme kaynakları içine kesme.

- [GEP](sql-database-implementation-gep.md): GEP, işlerini işlemler, stratejilerini ve finansal performanslarını üzerindeki etkilerini yazılım ve tedarik kılavuzları hello world toomaximize geçici etkinleştirme hizmetleri sunar. Ayrıca tooconsulting ve yönetilen hizmetler, hello şirket akıllı GEP®, bulut tabanlı ve kapsamlı tedarik yazılım platformu tarafından sunar. Ancak, kendi GEP tarafından akıllı şirket içi veri merkezi gibi toosupport çözümleri çalışırken sınırlamaları GEP çalıştırılır: hello Yatırımlar gereken yüksek ve Mevzuat gereklilikleri diğer ülkelerdeki yapmış hello gerekli Yatırımlar daha zorlu hala. Taşıma toohello bulut tarafından GEP BT tooworry BT işlemleri hakkında daha az ve toofocus değerinin yeni kaynaklar için müşterilerinin Merhaba Dünya çapında geliştirme hakkında daha fazla izin vererek, BT kaynaklarını serbest.

- [SnelStart](sql-database-implementation-snelstart.md): SnelStart hello Hollanda popüler finansal ve iş-yönetimi yazılımı küçük ve orta ölçekli işletmeler (SMB) sağlar. 55,000 müşterilerine 110 çalışanlar, bir BT personeli 35 dahil olmak üzere bir personeli tarafından sunulur. Azure üzerinde oluşturulmuş masaüstü yazılım tooa yazılım olarak-hizmet (SaaS) teklifi hareket ettirerek SnelStart en hello yapılan tanıdık ortamlarında C# kullanarak ve performans ve ölçeklenebilirlik hiçbiri üzerinden - tarafından en iyi duruma getirme Yönetimi otomatikleştirme yerleşik hizmetlerin veya Esnek havuzları kullanan altında sağlama işletmeler. Azure kullanarak sağlar müşterilerin şirket içi ve hello arasında taşıma SnelStart hello ortadan bulut.

- [Umbraco](sql-database-implementation-umbraco.md): toosimplify müşteri dağıtımı, Umbraco eklenen Umbraco-bir hizmet olarak (UaaS): şirket içi dağıtımlar için hello ihtiyacını ortadan kaldıran bir yazılım olarak-hizmet (SaaS) sunumu yerleşik ölçeklendirme sağlar ve yönetimini kaldırır Geliştiriciler toofocus ürün çözüm yerine yenilik Yönetimi etkinleştirerek ek yükü. Umbraco, Microsoft Azure tarafından sunulan esnek hizmet olarak platform (PaaS) modeli güvenmek tarafından tüm bu avantajlar hello mümkün tooprovide olur.

- [Çekirdek](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database): çekirdek % 70'sql Database tarafından DTU düşürürken anahtar veritabanının iş yükü Katlar.

- [İsteği](https://customers.microsoft.com/en-US/story/quest): rtifika kendi Spotlight bir hedefi aklınıza tutarak ile SQL Server Enterprise hizmeti sunar: toogive veritabanı uzmanları hello en iyi araçları veri güvenliğini sağlamak için geçici verileri taşıma ve veritabanı işlemleri izleme için kullanılabilir. Microsoft Azure ve Azure SQL veritabanını kullanarak Spotlight ile SQL Server Veritabanı yöneticileri izleyebilir, algılamak, tanılama ve kendi masalarını durduğunu olduğunuz veya evden çalışan SQL Server performans sorunları şekilde tooresolve sağlayın.

- [Microsoft Dynamics](https://customers.microsoft.com/story/dynamics365operationsproductteam): en iyi yöntemler ve hello Dynamics 365 geçirme işlemleri ürün ekibinin deneyimi için gelen öğrenilen dersler kısa Bu örnek olay incelemesi vurgular sipariş tooprovide müşteriler ile tam olarak yönetilen tooAzure SQL veritabanı Yazılım sunumu bir hizmet (SaaS). Azure SQL veritabanı kullanarak hello Dynamics 365 işletim ekibi için mümkün toomanage edildi personel önemli ölçüde daha az hello hizmeti ile çalışır ve otomatik veritabanı yedeklemeyi, veritabanı yedekleme gibi giden kutusu yönetilebilirlik özellikleri ile kolayca ölçeklendirme Bekletme, yüksek kullanılabilirlik ve olağanüstü durum kurtarma özellikleri. Bu hello özelliği tooprovision Önemsiz Otomasyon veritabanlarıyla birlikte Azure SQL veritabanı toobeing konumu büyük ölçekli hizmetler kurmak için harika bir platform ödünç.
