---
title: "aaa \"Azure Analysis Services Adventure Works Öğreticisi | Microsoft Docs\""
description: "Azure Analysis Services için Hello Adventure Works Öğreticisi sunar"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: 2df8b3ab4e8c4ffbe0086418d60fd2e2abd35e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-analysis-services---adventure-works-tutorial"></a>Azure Analysis Services - Adventure Works Öğreticisi

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Bu öğretici hakkında dersleri sağlar toocreate hello 1400 uyumluluk düzeyine sahip tablo modeli kullanarak dağıtabilirsiniz [SQL Server veri Araçları (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).  

Yeni tooAnalysis Hizmetleri ve tablo modelleme değilseniz, bu öğreticiyi tamamlamak hello hızlı şekilde toolearn nasıl olduğunu toocreate ve temel tablo modeli dağıtın. Merhaba Önkoşullar olduktan sonra yerinde, iki toothree saatleri toocomplete arasında olması.  
  
## <a name="what-you-learn"></a>Öğrenecekleriniz   
  
-   Nasıl yeni bir tablolu model toocreate proje hello **1400 uyumluluk düzeyi** ssdt'de.
  
-   Nasıl bir tablo modeli projesine ilişkisel bir veritabanındaki tooimport veri.  
  
-   Nasıl toocreate ve hello modelindeki tablolar arasında ilişkiler yönetin.  
  
-   Sütunları, ölçüleri ve ana performans göstergelerini'de, kullanıcılar Yardım kritik iş ölçümleri analiz edin toocreate nasıl hesaplanır.  
  
-   Nasıl toocreate Perspektifler yönetin ve kullanıcıları daha kolay Yardım hiyerarşileri, iş ve uygulamaya özgü görüşlerini sağlayarak model verileri göz atın.  
  
-   Nasıl toocreate bölümleri, tablo verileri daha küçük diğer bölümlerdeki bağımsız olarak işlenebilen mantıksal parçalara bölmek.  
  
-   Nasıl toosecure model nesneleri ve veri kullanıcı üyeleriyle rolleri oluşturarak.  
  
-   Nasıl toodeploy tablolu model tooan **Azure Analysis Services** sunucusu veya bir şirket içi SQL Server 2017 Analysis Services sunucusu.  
  
## <a name="prerequisites"></a>Ön koşullar  
toocomplete Bu öğretici, gerekir:  
  
-   Bir Azure Analysis Services veya SQL Server 2017 Analysis Services modelinize toodeploy örneği. Ücretsiz [Azure Analysis Services denemesi](https://azure.microsoft.com/services/analysis-services/) için kaydolun ve [bir sunucu oluşturun](../analysis-services-create-server.md). Veya kaydolun ve [SQL Server 2017 Community Technology Preview](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp)’ı indirin. 

-   Bir SQL Server veri ambarı veya Azure SQL Data Warehouse hello ile [AdventureWorksDW2014 örnek veritabanı](http://go.microsoft.com/fwlink/?LinkID=335807). Bu örnek veritabanı hello veri gerekli toocomplete Bu öğretici içerir. [Ücretsiz SQL Server sürümlerini](https://www.microsoft.com/sql-server/sql-server-downloads) indirin. Veya ücretsiz bir [Azure SQL Veritabanı denemesi](https://azure.microsoft.com/services/sql-database/) için kaydolun. 

    **Önemli:** bir şirket içi SQL sunucusunda hello örnek veritabanını yüklemek ve model tooan Azure Analysis Services sunucusuna dağıtırsanız bir [şirket içi veri ağ geçidi](../analysis-services-gateway.md) gereklidir.

-   Merhaba en son sürümünü [SQL Server veri Araçları (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

-   Merhaba en son sürümünü [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).    

-   [Power BI Desktop](https://powerbi.microsoft.com/desktop/) veya Excel gibi bir istemci uygulaması. 

## <a name="scenario"></a>Senaryo  
Bu öğretici, kurgusal bir şirket olan Adventure Works Cycles’ı temel alır. Adventure Works üretir ve bisiklet, bölümleri ve Donatılar toocommercial pazarlarda Kuzey Amerika, Avrupa ve Asya dağıtan bir büyük, çokuluslu üretim şirketidir. Merhaba şirket 500 çalışanları kullanır. Ayrıca, Adventure Works pazar ağının tamamında çeşitli bölgesel satış ekipleri görevlendirir. Projenize satış ve pazarlama kullanıcıları tooanalyze Internet satış verileri hello AdventureWorksDW veritabanında için tablo modeli toocreate ' dir.  
  
toocomplete hello öğretici, çeşitli dersleri tamamlamanız gerekir. Her derste çeşitli görevler vardır. Her görev sırasına Tamamlanıyor hello Ders tamamlamak için gereklidir. Belirli bir dersteyken benzer bir sonucu elde etmek için farklı görevlerle karşılaşabilirsiniz, ancak her görevi tamamlama biçiminiz biraz farklıdır. Bu var olduğunu genellikle yöntemi gösterir birden fazla yollarından toocomplete bir görev ve toochallenge becerileri kullanarak, önceki dersleri ve görevleri öğrendiniz.  
  
Merhaba dersleri Hello amacı hello özelliklerinin çoğunu kullanarak temel tablo modeli yazma size SSDT dahil tooguide budur. Her ders hello önceki Ders kurulu olduğundan hello dersleri sırayla tamamlamanız gerekir.
  
Bu öğretici bir sunucu veya veritabanı yönetme SSMS kullanarak veya bir istemci kullanarak Azure portalında bir sunucu yönetmeyle ilgili dersleri uygulama toobrowse model verileri sağlamaz. 


## <a name="lessons"></a>Dersler  
Bu öğretici dersleri aşağıdaki hello içerir:  
  
|Ders|Tahmini süre toocomplete|  
|----------|------------------------------|  
|[1 - Yeni tablosal model projesi oluşturma](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)|10 dakika|  
|[2 - Veri alma](../tutorials/aas-lesson-2-get-data.md)|10 dakika|  
|[3 - Tarih Tablosu olarak işaretleme](../tutorials/aas-lesson-3-mark-as-date-table.md)|3 dakika|  
|[4 - İlişki oluşturma](../tutorials/aas-lesson-4-create-relationships.md)|10 dakika|  
|[5 - Hesaplanan sütunlar oluşturma](../tutorials/aas-lesson-5-create-calculated-columns.md)|15 dakika|
|[6 - Ölçü oluşturma](../tutorials/aas-lesson-6-create-measures.md)|30 dakika|  
|[7 - Ana Performans Göstergeleri (KPI) oluşturma](../tutorials/aas-lesson-7-create-key-performance-indicators.md)|15 dakika|  
|[8 - Perspektif oluşturma](../tutorials/aas-lesson-8-create-perspectives.md)|5 dakika|  
|[9 - Hiyerarşi oluşturma](../tutorials/aas-lesson-9-create-hierarchies.md)|20 dakika|  
|[10 - Bölüm oluşturma](../tutorials/aas-lesson-10-create-partitions.md)|15 dakika|  
|[11 - Rol oluşturma](../tutorials/aas-lesson-11-create-roles.md)|15 dakika|  
|[12 - Excel’de çözümleme](../tutorials/aas-lesson-12-analyze-in-excel.md)|5 dakika| 
|[13 - Dağıtma](../tutorials/aas-lesson-13-deploy.md)|5 dakika|  
  
## <a name="supplemental-lessons"></a>Ek dersler  
Bu derslerin gerekli toocomplete hello öğretici değildir, ancak yazma özelliklerini daha iyi anlamak Gelişmiş sekmeli modelde yararlı olabilir.  
  
|Ders|Tahmini süre toocomplete|  
|----------|------------------------------|  
|[Ayrıntı Satırları](../tutorials/aas-supplemental-lesson-detail-rows.md)|10 dakika|
|[Dinamik güvenlik](../tutorials/aas-supplemental-lesson-dynamic-security.md)|30 dakika|
|[Düzensiz hiyerarşiler](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)|20 dakika| 

  
## <a name="next-steps"></a>Sonraki adımlar  
başlatıldı, tooget bkz [Ders 1: yeni bir tablolu modeli projesi oluşturmak](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).  
  
  
  

