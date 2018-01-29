---
title: "Azure Analysis Services Adventure Works Öğreticisi | Microsoft Docs"
description: "Azure Analysis Services için Adventure Works öğreticisini sunar"
services: analysis-services
documentationcenter: 
author: Minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 01/08/2018
ms.author: owend
ms.openlocfilehash: 9b81e011d3e1ed23465bbd554a0c7376b432b585
ms.sourcegitcommit: 176c575aea7602682afd6214880aad0be6167c52
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/09/2018
---
# <a name="azure-analysis-services---adventure-works-tutorial"></a>Azure Analysis Services - Adventure Works Öğreticisi

Bu öğreticide, [SQL Server Veri Araçları (SSDT) ile Visual Studio](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)’yu kullanarak 1400 uyumluluk düzeyinde bir tablosal modelin nasıl oluşturulduğu ve dağıtıldığı ile ilgili dersler sağlanmaktadır.  

Analysis Services ve tablosal modelleme konusunda yeniyseniz, Visual Studio kullanarak basit bir tablosal model oluşturup dağıtmayı öğrenmenin en hızlı yolu bu öğreticiyi tamamlamaktır. Ön koşullar karşılandıktan sonra, tamamlanması iki ila üç saat arası sürmelidir.  
  
## <a name="what-you-learn"></a>Öğrenecekleriniz   
  
-   SSDT ile Visual Studio’da **1400 uyumluluk düzeyinde** yeni bir tablosal model projesi oluşturma.
  
-   İlişkisel veritabanındaki verileri bir tablosal model projesi çalışma alanı veritabanına aktarma.  
  
-   Modelde tablolar arasındaki ilişkileri oluşturma ve yönetme.  
  
-   Kullanıcıların kritik iş ölçümlerini analiz etmesine yardımcı olan hesaplanan sütunlar, ölçüler ve Temel Performans Göstergeleri oluşturma.  
  
-   Kullanıcıların işletme ve uygulamaya özgü bakış açıları sağlayarak model verilerine daha kolay göz atmasına yardımcı olan perspektifleri ve hiyerarşileri oluşturma ve yönetme.  
  
-   Tablo verilerini diğer bölümlerden bağımsız olarak işlenebilecek daha küçük mantıksal kısımlara ayıran bölümler oluşturma.  
  
-   Kullanıcı üyeleriyle roller oluşturarak model nesnelerinin ve verilerinin güvenliğini sağlama.  
  
-   Bir **Azure Analysis Services** sunucusuna ya da şirket içi SQL Server 2017 Analysis Services sunucusuna tablosal model dağıtma.  
  
## <a name="prerequisites"></a>Önkoşullar  
Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:  
  
-   Bir Azure Analysis Services sunucusu. Ücretsiz [Azure Analysis Services denemesi](https://azure.microsoft.com/services/analysis-services/) için kaydolun ve [bir sunucu oluşturun](../analysis-services-create-server.md). 

-   **Örnek AdventureWorksDW veritabanını** içeren bir [Azure SQL Veri Ambarı](../../sql-data-warehouse/create-data-warehouse-portal.md) veya [Adventure Works örnek veritabanını](http://go.microsoft.com/fwlink/?LinkID=335807) içeren bir SQL Server Veri Ambarı.

    **Önemli:** Örnek veritabanını bir şirket içi SQL Server Veri Ambarına, modelinizi ise bir Azure Analysis Services sunucusuna yüklerseniz [Şirket içi veri ağ geçidi](../analysis-services-gateway.md) gerekir.

-   Visual Studio için [SQL Server Veri Araçları](https://msdn.microsoft.com/library/mt204009.aspx)’nın (SSDT) en son sürümü.

-   [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)’nun (SSMS) en son sürümü.    

-   [Power BI Desktop](https://powerbi.microsoft.com/desktop/) veya Excel gibi bir istemci uygulaması. 

## <a name="scenario"></a>Senaryo  
Bu öğretici, kurgusal bir şirket olan Adventure Works Cycles’ı temel alır. Adventure Works; Kuzey Amerika, Avrupa ve Asya pazarları için bisiklet, parça ve aksesuar üretip pazarlayan büyük, çok uluslu bir üretim şirketidir. Şirketin 500 çalışanı vardır. Ayrıca, Adventure Works pazar ağının tamamında çeşitli bölgesel satış ekipleri görevlendirir. Proje hedefiniz, satış ve pazarlama kullanıcılarının AdventureWorksDW veritabanında İnternet satış verilerini analiz etmesi için tablosal bir model oluşturmaktır.  
  
Öğreticiyi tamamlamak için çeşitli dersleri tamamlamanız gerekir. Her derste çeşitli görevler vardır. Dersin tamamlanması için her görevin sırayla tamamlanması gerekir. Belirli bir dersteyken benzer bir sonucu elde etmek için farklı görevlerle karşılaşabilirsiniz, ancak her görevi tamamlama biçiminiz biraz farklıdır. Bu yöntem, bir görevi gerçekleştirmek için genellikle birden çok yol olduğunu gösterir ve önceki bölümlerde ve görevlerde öğrendiğiniz beceriler konusunda sizi sınar.  
  
Bu kılavuzdaki derslerin amacı, SSDT’deki birçok özelliği kullanarak temel bir tablosal model yazma konusunda size rehberlik etmektir. Her ders bir önceki dersin devamı niteliğinde olduğundan, dersleri sırasıyla tamamlamanız gerekir.
  
Bu öğretici, Azure portalında bir sunucuyu yönetme, SSMS’yi kullanarak bir sunucuyu veya veritabanını yönetme ya da istemci uygulamasını kullanarak model verilerine göz atama konusunda bilgi sağlamaz. 


## <a name="lessons"></a>Dersler  
Bu öğretici aşağıdaki dersleri içerir:  
  
|Ders|Tahmini tamamlanma süresi|  
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
Bu dersler öğreticinin tamamlanması için gerekli değildir, ancak gelişmiş tablosal model yazma özelliklerinin daha iyi anlaşılmasına yardımcı olabilir.  
  
|Ders|Tahmini tamamlanma süresi|  
|----------|------------------------------|  
|[Ayrıntı Satırları](../tutorials/aas-supplemental-lesson-detail-rows.md)|10 dakika|
|[Dinamik güvenlik](../tutorials/aas-supplemental-lesson-dynamic-security.md)|30 dakika|
|[Düzensiz hiyerarşiler](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)|20 dakika| 

  
## <a name="next-steps"></a>Sonraki adımlar  
Başlamak için bkz. [1. Ders: Yeni Tablosal Model Projesi Oluşturma](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).  
  
  
  

