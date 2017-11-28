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
# <a name="leverage-other-services-with-sql-data-warehouse"></a><span data-ttu-id="1ce12-103">SQL veri ambarı diğer hizmetlerle yararlanın</span><span class="sxs-lookup"><span data-stu-id="1ce12-103">Leverage other services with SQL Data Warehouse</span></span>
<span data-ttu-id="1ce12-104">Ayrıca tooits işlevselliği çekirdek, SQL Data Warehouse kullanıcılar tooleverage sağlayan birçok hello diğer Azure Hizmetleri, yanında.</span><span class="sxs-lookup"><span data-stu-id="1ce12-104">In addition tooits core functionality, SQL Data Warehouse enables users tooleverage many of hello other services in Azure alongside it.</span></span>  <span data-ttu-id="1ce12-105">Özellikle, biz toodeeply hello aşağıdakilerle tümleştirme adımları şu anda attıktan:</span><span class="sxs-lookup"><span data-stu-id="1ce12-105">Specifically, we have currently taken steps toodeeply integrate with hello following:</span></span>

* <span data-ttu-id="1ce12-106">Power BI</span><span class="sxs-lookup"><span data-stu-id="1ce12-106">Power BI</span></span>
* <span data-ttu-id="1ce12-107">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1ce12-107">Azure Data Factory</span></span>
* <span data-ttu-id="1ce12-108">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1ce12-108">Azure Machine Learning</span></span>
* <span data-ttu-id="1ce12-109">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1ce12-109">Azure Stream Analytics</span></span>

<span data-ttu-id="1ce12-110">Azure ekosistemi hello arasında daha fazla hizmetleriyle tooconnect çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="1ce12-110">We are working tooconnect with more services across hello Azure ecosystem.</span></span>

## <a name="power-bi"></a><span data-ttu-id="1ce12-111">Power BI</span><span class="sxs-lookup"><span data-stu-id="1ce12-111">Power BI</span></span>
<span data-ttu-id="1ce12-112">Power BI tümleştirmesi hello dinamik Raporlama ile SQL Data Warehouse tooleverage hello işlem gücü ve Power BI görselleştirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="1ce12-112">Power BI integration allows you tooleverage hello compute power of SQL Data Warehouse with hello dynamic reporting and visualization of Power BI.</span></span> <span data-ttu-id="1ce12-113">Power BI tümleştirmesi şu anda içerir:</span><span class="sxs-lookup"><span data-stu-id="1ce12-113">Power BI integration currently includes:</span></span>

* <span data-ttu-id="1ce12-114">**Connect doğrudan**: daha gelişmiş SQL veri ambarına karşı mantıksal aşağı itme bağlantıyla.</span><span class="sxs-lookup"><span data-stu-id="1ce12-114">**Direct Connect**: A more advanced connection with logical pushdown against SQL Data Warehouse.</span></span>  <span data-ttu-id="1ce12-115">Bu, daha büyük bir ölçekte daha hızlı analizini sağlar.</span><span class="sxs-lookup"><span data-stu-id="1ce12-115">This provides faster analysis on a larger scale.</span></span>
* <span data-ttu-id="1ce12-116">**Power bı'da Aç**: hello 'Power bı'da Aç' düğmesini örneği bilgi tooPower daha sorunsuz bir bağlantı için izin verme BI geçirir.</span><span class="sxs-lookup"><span data-stu-id="1ce12-116">**Open in Power BI**: hello 'Open in Power BI' button passes instance information tooPower BI, allowing for a more seamless connection.</span></span>

<span data-ttu-id="1ce12-117">Bkz: [Power BI ile tümleştirme](sql-data-warehouse-integrate-power-bi.md) veya hello [Power BI belgelerine](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="1ce12-117">See [Integrate with Power BI](sql-data-warehouse-integrate-power-bi.md) or hello [Power BI documentation](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) for more information.</span></span>

## <a name="azure-data-factory"></a><span data-ttu-id="1ce12-118">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1ce12-118">Azure Data Factory</span></span>
<span data-ttu-id="1ce12-119">Azure Data Factory, kullanıcıların karmaşık Extract yük ardışık düzenleri bir yönetilen platform toocreate sağlar.</span><span class="sxs-lookup"><span data-stu-id="1ce12-119">Azure Data Factory gives users a managed platform toocreate complex Extract-Load pipelines.</span></span>  <span data-ttu-id="1ce12-120">Azure Data Factory ile SQL Data Warehouse'un tümleştirme hello aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="1ce12-120">SQL Data Warehouse's integration with Azure Data Factory includes hello following:</span></span>

* <span data-ttu-id="1ce12-121">**Saklı yordamlar**: SQL Data Warehouse saklı yordamları hello yürütülmesi düzenlemek.</span><span class="sxs-lookup"><span data-stu-id="1ce12-121">**Stored Procedures**: Orchestrate hello execution of stored procedures on SQL Data Warehouse.</span></span>
* <span data-ttu-id="1ce12-122">**Kopya**: SQL Data Warehouse kullanım ADF toomove verileri.</span><span class="sxs-lookup"><span data-stu-id="1ce12-122">**Copy**: Use ADF toomove data into SQL Data Warehouse.</span></span>  <span data-ttu-id="1ce12-123">Bu işlem ADF'nin standart veri taşıma mekanizması kullanabilir veya hello altında PolyBase kapsar.</span><span class="sxs-lookup"><span data-stu-id="1ce12-123">This operation can use ADF's standard data movement mechanism or PolyBase under hello covers.</span></span> 

<span data-ttu-id="1ce12-124">Bkz: [Azure Data Factory ile tümleştirme](sql-data-warehouse-integrate-azure-data-factory.md) veya hello [Azure Data Factory belgelerine](https://azure.microsoft.com/documentation/services/data-factory/) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="1ce12-124">See [Integrate with Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) or hello [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/) for more information.</span></span>

## <a name="azure-machine-learning"></a><span data-ttu-id="1ce12-125">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1ce12-125">Azure Machine Learning</span></span>
<span data-ttu-id="1ce12-126">Azure Machine Learning toocreate karmaşık modelleri çok sayıda Tahmine dayalı araçları yararlanarak kullanıcıların sağlayan tam olarak yönetilen analiz hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="1ce12-126">Azure Machine Learning is a fully managed analytics service which allows users toocreate intricate models leveraging a large set of predictive tools.</span></span>  <span data-ttu-id="1ce12-127">SQL veri ambarı varsayılan olarak, aşağıdaki işlevselliği hello ile hem kaynak hem de bu modeller için hedef olarak desteklenir:</span><span class="sxs-lookup"><span data-stu-id="1ce12-127">SQL Data Warehouse is supported as both a source and destination for these models with hello following functionality:</span></span>

* <span data-ttu-id="1ce12-128">**Veri okuma:** SQL veri ambarına karşı T-SQL kullanarak ölçekte modelleri sürücü.</span><span class="sxs-lookup"><span data-stu-id="1ce12-128">**Read Data:** Drive models at scale using T-SQL against SQL Data Warehouse.</span></span>
* <span data-ttu-id="1ce12-129">**Veri yaz:** herhangi modelden değişiklikleri geri tooSQL veri ambarı.</span><span class="sxs-lookup"><span data-stu-id="1ce12-129">**Write Data:** Commit changes from any model back tooSQL Data Warehouse.</span></span>

<span data-ttu-id="1ce12-130">Bkz: [Azure Machine Learning ile tümleştirme](sql-data-warehouse-integrate-azure-machine-learning.md) veya hello [Azure Machine Learning belge](https://azure.microsoft.com/services/machine-learning/) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="1ce12-130">See [Integrate with Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) or hello [Azure Machine Learning documentation](https://azure.microsoft.com/services/machine-learning/) for more information.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="1ce12-131">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1ce12-131">Azure Stream Analytics</span></span>
<span data-ttu-id="1ce12-132">Azure Stream Analytics, işleme ve Azure olay Hub'ından oluşturulan olay verilerini tüketen tam olarak yönetilen, karmaşık bir altyapıdır.</span><span class="sxs-lookup"><span data-stu-id="1ce12-132">Azure Stream Analytics is a complex, fully managed infrastructure for processing and consuming event data generated from Azure Event Hub.</span></span>  <span data-ttu-id="1ce12-133">SQL veri ambarı ile tümleştirme, akış için veri toobe etkili bir şekilde işlenir ve derin etkinleştirme ilişkisel veri depolanan, daha fazla analiz Gelişmiş izin verir.</span><span class="sxs-lookup"><span data-stu-id="1ce12-133">Integration with SQL Data Warehouse allows for streaming data toobe effectively processed and stored alongside relational data enabling deeper, more advanced analysis.</span></span>  

* <span data-ttu-id="1ce12-134">**İş çıktısı:** gönderme çıktısını Stream Analytics işleri doğrudan tooSQL veri ambarı.</span><span class="sxs-lookup"><span data-stu-id="1ce12-134">**Job Output:** Send output from Stream Analytics jobs directly tooSQL Data Warehouse.</span></span>

<span data-ttu-id="1ce12-135">Bkz: [Azure akış Analizi ile tümleştirme](sql-data-warehouse-integrate-azure-stream-analytics.md) veya hello [Azure akış analizi belgeleri](https://azure.microsoft.com/documentation/services/stream-analytics/) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="1ce12-135">See [Integrate with Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) or hello [Azure Stream Analytics documentation](https://azure.microsoft.com/documentation/services/stream-analytics/) for more information.</span></span>

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
