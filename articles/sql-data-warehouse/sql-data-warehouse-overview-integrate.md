---
title: "SQL veri ambarı ile tümleştirilmiş çözümler derleme | Microsoft Docs"
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
ms.openlocfilehash: d407c29f99fd7537590ec787febd84a9e3f4f353
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a><span data-ttu-id="7b6f7-103">SQL veri ambarı diğer hizmetlerle yararlanın</span><span class="sxs-lookup"><span data-stu-id="7b6f7-103">Leverage other services with SQL Data Warehouse</span></span>
<span data-ttu-id="7b6f7-104">Çekirdek işlevselliğini ek olarak, SQL Data Warehouse kullanıcıların diğer hizmetler Azure bunu yanında çoğunu yararlanan olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="7b6f7-104">In addition to its core functionality, SQL Data Warehouse enables users to leverage many of the other services in Azure alongside it.</span></span>  <span data-ttu-id="7b6f7-105">Özellikle, biz derine aşağıdaki ile tümleştirme adımları şu anda attıktan:</span><span class="sxs-lookup"><span data-stu-id="7b6f7-105">Specifically, we have currently taken steps to deeply integrate with the following:</span></span>

* <span data-ttu-id="7b6f7-106">Power BI</span><span class="sxs-lookup"><span data-stu-id="7b6f7-106">Power BI</span></span>
* <span data-ttu-id="7b6f7-107">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="7b6f7-107">Azure Data Factory</span></span>
* <span data-ttu-id="7b6f7-108">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="7b6f7-108">Azure Machine Learning</span></span>
* <span data-ttu-id="7b6f7-109">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7b6f7-109">Azure Stream Analytics</span></span>

<span data-ttu-id="7b6f7-110">Daha fazla Hizmetleri ile Azure ekosistemi bağlanmak için çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="7b6f7-110">We are working to connect with more services across the Azure ecosystem.</span></span>

## <a name="power-bi"></a><span data-ttu-id="7b6f7-111">Power BI</span><span class="sxs-lookup"><span data-stu-id="7b6f7-111">Power BI</span></span>
<span data-ttu-id="7b6f7-112">Power BI tümleştirme, dinamik Raporlama ile SQL Data Warehouse işlem gücü ve Power BI görselleştirme yararlanmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="7b6f7-112">Power BI integration allows you to leverage the compute power of SQL Data Warehouse with the dynamic reporting and visualization of Power BI.</span></span> <span data-ttu-id="7b6f7-113">Power BI tümleştirmesi şu anda içerir:</span><span class="sxs-lookup"><span data-stu-id="7b6f7-113">Power BI integration currently includes:</span></span>

* <span data-ttu-id="7b6f7-114">**Connect doğrudan**: daha gelişmiş SQL veri ambarına karşı mantıksal aşağı itme bağlantıyla.</span><span class="sxs-lookup"><span data-stu-id="7b6f7-114">**Direct Connect**: A more advanced connection with logical pushdown against SQL Data Warehouse.</span></span>  <span data-ttu-id="7b6f7-115">Bu, daha büyük bir ölçekte daha hızlı analizini sağlar.</span><span class="sxs-lookup"><span data-stu-id="7b6f7-115">This provides faster analysis on a larger scale.</span></span>
* <span data-ttu-id="7b6f7-116">**Power bı'da Aç**: Power BI, örnek bilgileri daha sorunsuz bir bağlantı için izin verme 'Power bı'da Aç' düğmesini geçirir.</span><span class="sxs-lookup"><span data-stu-id="7b6f7-116">**Open in Power BI**: The 'Open in Power BI' button passes instance information to Power BI, allowing for a more seamless connection.</span></span>

<span data-ttu-id="7b6f7-117">Bkz: [Power BI ile tümleştirme](sql-data-warehouse-integrate-power-bi.md) veya [Power BI belgelerine](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="7b6f7-117">See [Integrate with Power BI](sql-data-warehouse-integrate-power-bi.md) or the [Power BI documentation](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) for more information.</span></span>

## <a name="azure-data-factory"></a><span data-ttu-id="7b6f7-118">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="7b6f7-118">Azure Data Factory</span></span>
<span data-ttu-id="7b6f7-119">Azure Data Factory, kullanıcıların karmaşık Extract yük işlem hatlarını oluşturmak için yönetilen bir platform sağlar.</span><span class="sxs-lookup"><span data-stu-id="7b6f7-119">Azure Data Factory gives users a managed platform to create complex Extract-Load pipelines.</span></span>  <span data-ttu-id="7b6f7-120">Azure Data Factory ile SQL Data Warehouse'un tümleştirme aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="7b6f7-120">SQL Data Warehouse's integration with Azure Data Factory includes the following:</span></span>

* <span data-ttu-id="7b6f7-121">**Saklı yordamlar**: SQL Data Warehouse saklı yordamları yürütülmesi düzenlemek.</span><span class="sxs-lookup"><span data-stu-id="7b6f7-121">**Stored Procedures**: Orchestrate the execution of stored procedures on SQL Data Warehouse.</span></span>
* <span data-ttu-id="7b6f7-122">**Kopya**: ADF SQL Data Warehouse'a veri taşımak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="7b6f7-122">**Copy**: Use ADF to move data into SQL Data Warehouse.</span></span>  <span data-ttu-id="7b6f7-123">Bu işlem perde arkasında ADF'nin standart veri taşıma mekanizması veya PolyBase kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b6f7-123">This operation can use ADF's standard data movement mechanism or PolyBase under the covers.</span></span> 

<span data-ttu-id="7b6f7-124">Bkz: [Azure Data Factory ile tümleştirme](sql-data-warehouse-integrate-azure-data-factory.md) veya [Azure Data Factory belgelerine](https://azure.microsoft.com/documentation/services/data-factory/) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="7b6f7-124">See [Integrate with Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) or the [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/) for more information.</span></span>

## <a name="azure-machine-learning"></a><span data-ttu-id="7b6f7-125">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="7b6f7-125">Azure Machine Learning</span></span>
<span data-ttu-id="7b6f7-126">Azure Machine Learning Tahmine dayalı araçları büyük bir dizi yararlanarak karmaşık modelleri oluşturma olanağı tanıyan tam olarak yönetilen analiz hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="7b6f7-126">Azure Machine Learning is a fully managed analytics service which allows users to create intricate models leveraging a large set of predictive tools.</span></span>  <span data-ttu-id="7b6f7-127">SQL veri ambarı varsayılan olarak, şu işlevlerle hem kaynak hem de bu modeller için hedef olarak desteklenir:</span><span class="sxs-lookup"><span data-stu-id="7b6f7-127">SQL Data Warehouse is supported as both a source and destination for these models with the following functionality:</span></span>

* <span data-ttu-id="7b6f7-128">**Veri okuma:** SQL veri ambarına karşı T-SQL kullanarak ölçekte modelleri sürücü.</span><span class="sxs-lookup"><span data-stu-id="7b6f7-128">**Read Data:** Drive models at scale using T-SQL against SQL Data Warehouse.</span></span>
* <span data-ttu-id="7b6f7-129">**Veri yaz:** tamamlama geri SQL Data Warehouse için herhangi bir modelden değiştirir.</span><span class="sxs-lookup"><span data-stu-id="7b6f7-129">**Write Data:** Commit changes from any model back to SQL Data Warehouse.</span></span>

<span data-ttu-id="7b6f7-130">Bkz: [Azure Machine Learning ile tümleştirme](sql-data-warehouse-integrate-azure-machine-learning.md) veya [Azure Machine Learning belge](https://azure.microsoft.com/services/machine-learning/) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="7b6f7-130">See [Integrate with Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) or the [Azure Machine Learning documentation](https://azure.microsoft.com/services/machine-learning/) for more information.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="7b6f7-131">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7b6f7-131">Azure Stream Analytics</span></span>
<span data-ttu-id="7b6f7-132">Azure Stream Analytics, işleme ve Azure olay Hub'ından oluşturulan olay verilerini tüketen tam olarak yönetilen, karmaşık bir altyapıdır.</span><span class="sxs-lookup"><span data-stu-id="7b6f7-132">Azure Stream Analytics is a complex, fully managed infrastructure for processing and consuming event data generated from Azure Event Hub.</span></span>  <span data-ttu-id="7b6f7-133">Akış etkili bir şekilde işlenir ve derin, daha gelişmiş analiz etkinleştirme ilişkisel veri depolanan verileri SQL Data Warehouse ile tümleştirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="7b6f7-133">Integration with SQL Data Warehouse allows for streaming data to be effectively processed and stored alongside relational data enabling deeper, more advanced analysis.</span></span>  

* <span data-ttu-id="7b6f7-134">**İş çıktısı:** Gönder çıkış akış analizi işleri doğrudan SQL Data Warehouse için.</span><span class="sxs-lookup"><span data-stu-id="7b6f7-134">**Job Output:** Send output from Stream Analytics jobs directly to SQL Data Warehouse.</span></span>

<span data-ttu-id="7b6f7-135">Bkz: [Azure akış Analizi ile tümleştirme](sql-data-warehouse-integrate-azure-stream-analytics.md) veya [Azure akış analizi belgeleri](https://azure.microsoft.com/documentation/services/stream-analytics/) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="7b6f7-135">See [Integrate with Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) or the [Azure Stream Analytics documentation](https://azure.microsoft.com/documentation/services/stream-analytics/) for more information.</span></span>

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
