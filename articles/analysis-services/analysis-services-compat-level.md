---
title: "Azure Analysis Services aaaData modeli uyumluluk düzeyi | Microsoft Docs"
description: "Tablo veri modeline uyumluluk düzeyi anlama."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/16/2017
ms.author: owend
ms.openlocfilehash: bfaf0c60666729d1e6e0baf082c046ea9faa4e86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a>Analysis Services tablolu modeller için uyumluluk düzeyi

*Uyumluluk düzeyi* hello Analysis Services altyapısı toorelease özgü davranışlarının başvuruyor. SQL Server'ın ana sürümleriyle genellikle çakıştığı değişiklikleri toohello uyumluluk düzeyi. Bu değişiklikler de her iki platform arasında Azure Analysis Services toomaintain eşliği uygulanır. Uyumluluk düzeyi değişiklikleri tablo Modellerinizi kullanılabilir özellikler de etkiler. Örneğin, DirectQuery ve tablo nesne meta verilerini hello uyumluluk düzeyine bağlı olarak farklı uygulamaları vardır. 

Azure Analysis Services tablolu modeller hello 1200 ve 1400 Uyumluluk Düzeyleri destekler.

Merhaba son uyumluluk düzeyi 1400 ' dir. Bu düzey, SQL Server 2017 Analysis Services ile örtüşür. Merhaba 1400 uyumluluk düzeyi önemli özellikleri şunlardır:

*  Veri bağlantısı ve tablolu modeller içe için yeni altyapı ZEL API'ları ve TMSL scripting desteği. Bu yeni özellik, Azure Blob Depolama alanı gibi ek veri kaynaklarını desteğini etkinleştirir.
*  Veri dönüştürme ve Veri Al ve M ifadeler kullanarak veri karma özellikleri.
*  Ölçüler bir DAX ifadesi ayrıntı satırları özelliğiyle destekler. Bu özelliği, Microsoft Excel toodrill toodetailed veri bir toplanmış raporundan aşağı gibi istemci araçlar sağlar. Örneğin, kullanıcıların ay ve bölge için toplam satış görüntülediğinizde ilişkili hello sipariş ayrıntılarını görüntüleyebilirsiniz. 
*  Nesne düzeyinde güvenlik için tablo ve sütun adları, ayrıca bunların içindeki toohello veri.
*  Düzensiz hiyerarşileri için gelişmiş destek.
*  Performans ve izleme geliştirmeleri.
  
## <a name="set-compatibility-level"></a>Set uyumluluk düzeyi 
 SSDT içinde yeni bir tablo modeli projesi oluştururken, üzerinde hello hello uyumluluk düzeyini belirtebilirsiniz **Tabular modeli Tasarımcısı** iletişim. 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 Merhaba seçerseniz **bu iletiyi tekrar gösterme** seçeneği, tüm sonraki projeleri hello varsayılan olarak belirttiğiniz hello uyumluluk düzeyi kullanın. İçinde ssdt'de hello varsayılan uyumluluk düzeyini değiştirebilirsiniz **Araçları** > **seçenekleri**.  
  
 tooupgrade SSDT, kümesi hello var olan tablo modeli projesinde **uyumluluk düzeyini** hello modeli özelliğinde **özellikleri** penceresi. İçinde-unutmayın, hello uyumluluk düzeyini yükseltme işlemi geri alınamaz.
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a>SQL Server Management Studio'da tablo modelli bir veritabanı uyumluluk düzeyi denetimi 
 SSMS, hello veritabanı adına sağ tıklayın > **özellikleri** > **uyumluluk düzeyi**.  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a>SSMS Server'da desteklenen uyumluluk düzeyini denetleyin  
 SSMS, hello sunucu adına sağ tıklayın > **özellikleri** > **desteklenen uyumluluk düzeyi**.  
  
 Bu özellik hello yüksek uyumluluk düzeyini (Önizleme hariç) hello sunucuda çalışacak bir veritabanı belirtir. desteklenen hello uyumluluk düzeyi değiştirilemez.  

## <a name="next-steps"></a>Sonraki adımlar
  [Azure portalında bir model oluşturma](analysis-services-create-model-portal.md)   
  [Çözümleme Hizmetleri yönetme](analysis-services-manage.md)  
