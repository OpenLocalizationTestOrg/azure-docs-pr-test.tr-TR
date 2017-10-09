---
title: SQL Data Warehouse ile Azure Data Factory aaaUse | Microsoft Docs
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
ms.openlocfilehash: d40a547830f9681504253d39ae3066800a955c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a><span data-ttu-id="f5f36-103">SQL Data Warehouse ile Azure Data Factory kullanın</span><span class="sxs-lookup"><span data-stu-id="f5f36-103">Use Azure Data Factory with SQL Data Warehouse</span></span>
<span data-ttu-id="f5f36-104">Azure Data Factory veri aktarımını hello ve saklı yordamlar SQL veri ambarı üzerinde yürütülmesi yönetme için tam olarak yönetilen bir yöntem sağlar.</span><span class="sxs-lookup"><span data-stu-id="f5f36-104">Azure Data Factory provides a fully managed method for orchestrating hello transfer of data and execution of stored procedures on SQL Data Warehouse.</span></span>  <span data-ttu-id="f5f36-105">Bu, toomore kolayca sağlayacak Kurulum ve zamanlama karmaşık ayıklamak dönüştürme ve yükleme (ETL) yordamlar SQL veri ambarı ile.</span><span class="sxs-lookup"><span data-stu-id="f5f36-105">This will allow you toomore easily set-up and schedule complex Extract Transform and Load (ETL) procedures with SQL Data Warehouse.</span></span> <span data-ttu-id="f5f36-106">Azure Data Factory daha kapsamlı bir genel bakış için bkz: Merhaba [Azure Data Factory belgelerine][Azure Data Factory documentation].</span><span class="sxs-lookup"><span data-stu-id="f5f36-106">For a more complete overview of Azure Data Factory, see hello [Azure Data Factory documentation][Azure Data Factory documentation].</span></span>

## <a name="data-movement"></a><span data-ttu-id="f5f36-107">Veri Taşıma</span><span class="sxs-lookup"><span data-stu-id="f5f36-107">Data Movement</span></span>
<span data-ttu-id="f5f36-108">Azure Data Factory hem şirket içi kaynakları hem de farklı Azure hizmetleri arasında veri taşıma sağlar.</span><span class="sxs-lookup"><span data-stu-id="f5f36-108">Azure Data Factory enables data movement between both on-premises sources and different Azure services.</span></span>  <span data-ttu-id="f5f36-109">Genel, geçerli tümleştirme Azure Data Factory ile veri taşıma tooand hello aşağıdaki konumlardan gelen destekler:</span><span class="sxs-lookup"><span data-stu-id="f5f36-109">Overall, current integration with Azure Data Factory supports data movement tooand from hello following locations:</span></span>

* <span data-ttu-id="f5f36-110">Azure blob depolama</span><span class="sxs-lookup"><span data-stu-id="f5f36-110">Azure blob storage</span></span>
* <span data-ttu-id="f5f36-111">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="f5f36-111">Azure SQL Database</span></span>
* <span data-ttu-id="f5f36-112">Şirket içi SQL Server</span><span class="sxs-lookup"><span data-stu-id="f5f36-112">On-premises SQL Server</span></span>
* <span data-ttu-id="f5f36-113">SQL Server Iaas üzerinde</span><span class="sxs-lookup"><span data-stu-id="f5f36-113">SQL Server on IaaS</span></span>

<span data-ttu-id="f5f36-114">Nasıl bir verileri tooset kopyalama etkinliği hakkında bilgi için bkz: [Azure Data Factory ile veri kopyalama][Copy data with Azure Data Factory]</span><span class="sxs-lookup"><span data-stu-id="f5f36-114">For information on how tooset up a data copy activity see [Copy data with Azure Data Factory][Copy data with Azure Data Factory]</span></span>

## <a name="stored-procedures"></a><span data-ttu-id="f5f36-115">Saklı Yordamlar</span><span class="sxs-lookup"><span data-stu-id="f5f36-115">Stored Procedures</span></span>
 <span data-ttu-id="f5f36-116">Hello aynı şekilde bu olabilir tooschedule veri aktarımı, Azure Data Factory can da kullanılan tooorchestrate hello saklı yordamlar yürütülmesi kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f5f36-116">In hello same way it can be used tooschedule data transfer, Azure Data Factory can also be used tooorchestrate hello execution of stored procedures.</span></span>  <span data-ttu-id="f5f36-117">Bu, daha karmaşık ardışık düzen toobe oluşturulan verir ve Azure veri fabrikasının özelliği tooleverage hello hesaplama gücüne SQL veri ambarı genişletir.</span><span class="sxs-lookup"><span data-stu-id="f5f36-117">This allows more complex pipelines toobe created and extends Azure Data Factory's ability tooleverage hello computational power of SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5f36-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f5f36-118">Next steps</span></span>
<span data-ttu-id="f5f36-119">Tümleştirme genel bakış için bkz: [SQL Data Warehouse tümleştirme genel bakış][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="f5f36-119">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>
<span data-ttu-id="f5f36-120">Geliştirme ile ilgili daha fazla ipucu için bkz. [SQL Veri Ambarı’nda geliştirmeye genel bakış][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="f5f36-120">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->

[Copy data with Azure Data Factory]: ../data-factory/data-factory-data-movement-activities.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]: ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory documentation]:https://azure.microsoft.com/documentation/services/data-factory/

