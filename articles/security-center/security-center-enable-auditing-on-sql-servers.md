---
title: "Azure Güvenlik Merkezi'nde SQL sunucularında aaaEnable denetim ve tehdit algılama | Microsoft Docs"
description: "Bu belge size nasıl tooimplement hello Azure Güvenlik Merkezi öneri gösterir. ** üzerinde SQL sunucuları ** denetimi etkinleştirme ve tehdit algılama."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 042fca4d-7dab-4172-8614-e8c21ccb4960
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: b082c48cdbc386f14e677f4e13a7f306f37fd0e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-servers-in-azure-security-center"></a>Azure Güvenlik Merkezi'nde SQL sunucularında denetim ve tehdit algılama etkinleştir
Azure Güvenlik Merkezi Denetim açıldıktan ve tehdit algılama denetim varsa, Azure SQL sunucularınızda tüm veritabanları için etkinleştirilmediyse önerir. Denetim ve tehdit algılama, yönetmeliklere uygunluğu korumanıza, veritabanı etkinliklerini anlamanıza ve ifade eden tutarsızlıklar ve anormallikleri, kavramanıza yardımcı olabilir iş endişeleri veya güvenlik ihlalleri şüpheli.

Denetim ayarladıktan sonra tehdit algılama ayarlarını ve e-postaları tooreceive güvenlik uyarılarını yapılandırabilirsiniz. Tehdit algılama, olası güvenlik tehditlerine toohello veritabanı gösteren anormal veritabanı etkinliklerini algılar. Bu toodetect sağlar ve bunlar ortaya çıktığında toopotential tehditlerine yanıt.

Bu öneri toohello yalnızca Azure SQL Hizmeti uygulanır; Azure altyapı Hizmetleri'nde (Azure Iaas), sanal makinelerde çalışan SQL Server içermez.

> [!NOTE]
> Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar.  Bu, adım adım ilerleyen bir kılavuz değildir.
>
>

## <a name="implement-hello-recommendation"></a>Merhaba öneriyi uygulamayı
1. Merhaba, **önerileri** dikey penceresinde, select **SQL sunucularında denetimi etkinleştirme ve tehdit algılama**.  Merhaba açılır **SQL sunucularında denetimi etkinleştirme ve tehdit algılama** dikey.

   ![SQL sunucularında denetimi etkinleştirme][1]
2. ' Bir SQL server tooenable denetim ve tehdit Algılama'ı seçin. Merhaba açılır **denetim ve tehdit algılama** dikey.

3. Merhaba üzerinde **denetim ve tehdit algılama** dikey penceresinde, select **ON** altında **denetim**.

   ![Denetim Ayarları'nı Aç][2]
4. Merhaba adımları [hello Azure portal, SQL veritabanı denetimi](../sql-database/sql-database-auditing-portal.md) denetim günlüklerini depolanacağı tooconfigure depolama. Merhaba aboneliğinin depolama hesabı için veri toplama hello varsayılan depolama hesabıdır.
5. Merhaba adımları [SQL veritabanı tehdit algılama ile çalışmaya başlama](../sql-database/sql-database-threat-detection.md) üzerinde tooturn ve tehdit algılama ve anormal etkinlikler algılandığında güvenlik uyarı alacak olan e-posta tooconfigure hello liste yapılandırın.

## <a name="see-also"></a>Ayrıca bkz.
Bu makalede, nasıl tooimplement hello Güvenlik Merkezi öneri "Denetlemeyi etkinleştirme ve tehdit algılama SQL sunucularında." gösterdi. SQL veritabanınızın güvenliğini sağlama hakkında daha fazla toolearn hello aşağıdaki bakın:

* [SQL Veritabanınızı güvenli hale getirme](../sql-database/sql-database-security-overview.md)

Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.
* [Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) --nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) --öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.
* [Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) --nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) --hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) --hello en son Azure güvenlik haberlerini ve bilgilerini alın.

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-server/enable-auditing-on-sql-servers.png
[2]: ./media/security-center-enable-auditing-on-sql-server/auditing-settings-blade.png
