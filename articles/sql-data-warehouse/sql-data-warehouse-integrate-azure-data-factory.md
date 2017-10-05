---
title: "SQL Data Warehouse ile Azure Data Factory kullanın | Microsoft Docs"
description: "Çözümleri geliştirme için Azure SQL Data Warehouse ile Azure Data Factory (ADF) kullanma ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 492de762-c7a2-4cdb-943f-3135230e94f1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 7cd113f4a92635bc68253c2beb165ad1f0c96569
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a>SQL Data Warehouse ile Azure Data Factory kullanın
Azure Data Factory veri aktarımını ve saklı yordamlar SQL veri ambarı üzerinde yürütülmesi yönetme için tam olarak yönetilen bir yöntem sağlar.  Bu yordamlara daha kolay kurulum ve zamanlama karmaşık ayıklamak dönüştürme ve yükleme (ETL) SQL veri ambarı ile olanak sağlar. Azure Data Factory daha kapsamlı bir genel bakış için bkz: [Azure Data Factory belgelerine][Azure Data Factory documentation].

## <a name="data-movement"></a>Veri Taşıma
Azure Data Factory hem şirket içi kaynakları hem de farklı Azure hizmetleri arasında veri taşıma sağlar.  Genel, geçerli tümleştirme Azure Data Factory ile veri taşıma için ve aşağıdaki konumlardan destekler:

* Azure blob depolama
* Azure SQL Database
* Şirket içi SQL Server
* SQL Server Iaas üzerinde

Kopya etkinliği bir verileri ayarlama hakkında bilgi için bkz [Azure Data Factory ile veri kopyalama][Copy data with Azure Data Factory]

## <a name="stored-procedures"></a>Saklı Yordamlar
 Veri aktarımı zamanlamak için kullanılabilir aynı şekilde Azure Data Factory de saklı yordamlar yürütülmesi düzenlemek için kullanılabilir.  Bu oluşturulacak daha karmaşık ardışık düzen verir ve Azure veri fabrikasının SQL Data Warehouse hesaplama gücünü yararlanan yeteneğini genişletir.

## <a name="next-steps"></a>Sonraki adımlar
Tümleştirme genel bakış için bkz: [SQL Data Warehouse tümleştirme genel bakış][SQL Data Warehouse integration overview].
Geliştirme ile ilgili daha fazla ipucu için bkz. [SQL Veri Ambarı’nda geliştirmeye genel bakış][SQL Data Warehouse development overview].

<!--Image references-->

<!--Article references-->

[Copy data with Azure Data Factory]: ../data-factory/data-factory-data-movement-activities.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]: ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory documentation]:https://azure.microsoft.com/documentation/services/data-factory/

