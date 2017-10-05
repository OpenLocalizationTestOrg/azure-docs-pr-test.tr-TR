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
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a><span data-ttu-id="82d65-103">SQL Data Warehouse ile Azure Data Factory kullanın</span><span class="sxs-lookup"><span data-stu-id="82d65-103">Use Azure Data Factory with SQL Data Warehouse</span></span>
<span data-ttu-id="82d65-104">Azure Data Factory veri aktarımını ve saklı yordamlar SQL veri ambarı üzerinde yürütülmesi yönetme için tam olarak yönetilen bir yöntem sağlar.</span><span class="sxs-lookup"><span data-stu-id="82d65-104">Azure Data Factory provides a fully managed method for orchestrating the transfer of data and execution of stored procedures on SQL Data Warehouse.</span></span>  <span data-ttu-id="82d65-105">Bu yordamlara daha kolay kurulum ve zamanlama karmaşık ayıklamak dönüştürme ve yükleme (ETL) SQL veri ambarı ile olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="82d65-105">This will allow you to more easily set-up and schedule complex Extract Transform and Load (ETL) procedures with SQL Data Warehouse.</span></span> <span data-ttu-id="82d65-106">Azure Data Factory daha kapsamlı bir genel bakış için bkz: [Azure Data Factory belgelerine][Azure Data Factory documentation].</span><span class="sxs-lookup"><span data-stu-id="82d65-106">For a more complete overview of Azure Data Factory, see the [Azure Data Factory documentation][Azure Data Factory documentation].</span></span>

## <a name="data-movement"></a><span data-ttu-id="82d65-107">Veri Taşıma</span><span class="sxs-lookup"><span data-stu-id="82d65-107">Data Movement</span></span>
<span data-ttu-id="82d65-108">Azure Data Factory hem şirket içi kaynakları hem de farklı Azure hizmetleri arasında veri taşıma sağlar.</span><span class="sxs-lookup"><span data-stu-id="82d65-108">Azure Data Factory enables data movement between both on-premises sources and different Azure services.</span></span>  <span data-ttu-id="82d65-109">Genel, geçerli tümleştirme Azure Data Factory ile veri taşıma için ve aşağıdaki konumlardan destekler:</span><span class="sxs-lookup"><span data-stu-id="82d65-109">Overall, current integration with Azure Data Factory supports data movement to and from the following locations:</span></span>

* <span data-ttu-id="82d65-110">Azure blob depolama</span><span class="sxs-lookup"><span data-stu-id="82d65-110">Azure blob storage</span></span>
* <span data-ttu-id="82d65-111">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="82d65-111">Azure SQL Database</span></span>
* <span data-ttu-id="82d65-112">Şirket içi SQL Server</span><span class="sxs-lookup"><span data-stu-id="82d65-112">On-premises SQL Server</span></span>
* <span data-ttu-id="82d65-113">SQL Server Iaas üzerinde</span><span class="sxs-lookup"><span data-stu-id="82d65-113">SQL Server on IaaS</span></span>

<span data-ttu-id="82d65-114">Kopya etkinliği bir verileri ayarlama hakkında bilgi için bkz [Azure Data Factory ile veri kopyalama][Copy data with Azure Data Factory]</span><span class="sxs-lookup"><span data-stu-id="82d65-114">For information on how to set up a data copy activity see [Copy data with Azure Data Factory][Copy data with Azure Data Factory]</span></span>

## <a name="stored-procedures"></a><span data-ttu-id="82d65-115">Saklı Yordamlar</span><span class="sxs-lookup"><span data-stu-id="82d65-115">Stored Procedures</span></span>
 <span data-ttu-id="82d65-116">Veri aktarımı zamanlamak için kullanılabilir aynı şekilde Azure Data Factory de saklı yordamlar yürütülmesi düzenlemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="82d65-116">In the same way it can be used to schedule data transfer, Azure Data Factory can also be used to orchestrate the execution of stored procedures.</span></span>  <span data-ttu-id="82d65-117">Bu oluşturulacak daha karmaşık ardışık düzen verir ve Azure veri fabrikasının SQL Data Warehouse hesaplama gücünü yararlanan yeteneğini genişletir.</span><span class="sxs-lookup"><span data-stu-id="82d65-117">This allows more complex pipelines to be created and extends Azure Data Factory's ability to leverage the computational power of SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82d65-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="82d65-118">Next steps</span></span>
<span data-ttu-id="82d65-119">Tümleştirme genel bakış için bkz: [SQL Data Warehouse tümleştirme genel bakış][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="82d65-119">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>
<span data-ttu-id="82d65-120">Geliştirme ile ilgili daha fazla ipucu için bkz. [SQL Veri Ambarı’nda geliştirmeye genel bakış][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="82d65-120">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->

[Copy data with Azure Data Factory]: ../data-factory/data-factory-data-movement-activities.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]: ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory documentation]:https://azure.microsoft.com/documentation/services/data-factory/

