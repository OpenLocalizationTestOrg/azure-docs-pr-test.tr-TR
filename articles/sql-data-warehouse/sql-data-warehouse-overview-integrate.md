---
title: "ile SQL veri ambarı aaaBuild tümleşik çözümleri | Microsoft Docs"
description: "Araçlar ve iş ortakları ile SQL Data Warehouse ile tümleştirme çözümleri. "
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: e2dc8f3f-10e3-4589-a4e2-50c67dfcf67f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: c8a4202dd84305bea4e4c2faf0e4791d026e794f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a>SQL veri ambarı diğer hizmetlerle yararlanın
Ayrıca tooits işlevselliği çekirdek, SQL Data Warehouse kullanıcılar tooleverage sağlayan birçok hello diğer Azure Hizmetleri, yanında.  Özellikle, biz toodeeply hello aşağıdakilerle tümleştirme adımları şu anda attıktan:

* Power BI
* Azure Data Factory
* Azure Machine Learning
* Azure Stream Analytics

Azure ekosistemi hello arasında daha fazla hizmetleriyle tooconnect çalışıyoruz.

## <a name="power-bi"></a>Power BI
Power BI tümleştirmesi hello dinamik Raporlama ile SQL Data Warehouse tooleverage hello işlem gücü ve Power BI görselleştirme sağlar. Power BI tümleştirmesi şu anda içerir:

* **Connect doğrudan**: daha gelişmiş SQL veri ambarına karşı mantıksal aşağı itme bağlantıyla.  Bu, daha büyük bir ölçekte daha hızlı analizini sağlar.
* **Power bı'da Aç**: hello 'Power bı'da Aç' düğmesini örneği bilgi tooPower daha sorunsuz bir bağlantı için izin verme BI geçirir.

Bkz: [Power BI ile tümleştirme](sql-data-warehouse-integrate-power-bi.md) veya hello [Power BI belgelerine](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) daha fazla bilgi için.

## <a name="azure-data-factory"></a>Azure Data Factory
Azure Data Factory, kullanıcıların karmaşık Extract yük ardışık düzenleri bir yönetilen platform toocreate sağlar.  Azure Data Factory ile SQL Data Warehouse'un tümleştirme hello aşağıdakileri içerir:

* **Saklı yordamlar**: SQL Data Warehouse saklı yordamları hello yürütülmesi düzenlemek.
* **Kopya**: SQL Data Warehouse kullanım ADF toomove verileri.  Bu işlem ADF'nin standart veri taşıma mekanizması kullanabilir veya hello altında PolyBase kapsar. 

Bkz: [Azure Data Factory ile tümleştirme](sql-data-warehouse-integrate-azure-data-factory.md) veya hello [Azure Data Factory belgelerine](https://azure.microsoft.com/documentation/services/data-factory/) daha fazla bilgi için.

## <a name="azure-machine-learning"></a>Azure Machine Learning
Azure Machine Learning toocreate karmaşık modelleri çok sayıda Tahmine dayalı araçları yararlanarak kullanıcıların sağlayan tam olarak yönetilen analiz hizmetidir.  SQL veri ambarı varsayılan olarak, aşağıdaki işlevselliği hello ile hem kaynak hem de bu modeller için hedef olarak desteklenir:

* **Veri okuma:** SQL veri ambarına karşı T-SQL kullanarak ölçekte modelleri sürücü.
* **Veri yaz:** herhangi modelden değişiklikleri geri tooSQL veri ambarı.

Bkz: [Azure Machine Learning ile tümleştirme](sql-data-warehouse-integrate-azure-machine-learning.md) veya hello [Azure Machine Learning belge](https://azure.microsoft.com/services/machine-learning/) daha fazla bilgi için.

## <a name="azure-stream-analytics"></a>Azure Stream Analytics
Azure Stream Analytics, işleme ve Azure olay Hub'ından oluşturulan olay verilerini tüketen tam olarak yönetilen, karmaşık bir altyapıdır.  SQL veri ambarı ile tümleştirme, akış için veri toobe etkili bir şekilde işlenir ve derin etkinleştirme ilişkisel veri depolanan, daha fazla analiz Gelişmiş izin verir.  

* **İş çıktısı:** gönderme çıktısını Stream Analytics işleri doğrudan tooSQL veri ambarı.

Bkz: [Azure akış Analizi ile tümleştirme](sql-data-warehouse-integrate-azure-stream-analytics.md) veya hello [Azure akış analizi belgeleri](https://azure.microsoft.com/documentation/services/stream-analytics/) daha fazla bilgi için.

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop/

[Azure Data Factory]: sql-data-warehouse-integrate-azure-data-factory.md
[Azure Machine Learning]: sql-data-warehouse-integrate-azure-machine-learning.md
[Azure Stream Analytics]: sql-data-warehouse-integrate-azure-stream-analytics.md
[Power BI]: sql-data-warehouse-integrate-power-bi.md
[Partners]: sql-data-warehouse-partner-business-intelligence.md

<!--MSDN references-->

<!--Other Web references-->
