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
# <a name="compatibility-level-for-analysis-services-tabular-models"></a><span data-ttu-id="96dbe-103">Analysis Services tablolu modeller için uyumluluk düzeyi</span><span class="sxs-lookup"><span data-stu-id="96dbe-103">Compatibility level for Analysis Services tabular models</span></span>

<span data-ttu-id="96dbe-104">*Uyumluluk düzeyi* hello Analysis Services altyapısı toorelease özgü davranışlarının başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="96dbe-104">*Compatibility level* refers toorelease-specific behaviors in hello Analysis Services engine.</span></span> <span data-ttu-id="96dbe-105">SQL Server'ın ana sürümleriyle genellikle çakıştığı değişiklikleri toohello uyumluluk düzeyi.</span><span class="sxs-lookup"><span data-stu-id="96dbe-105">Changes toohello compatibility level typically coincide with major releases of SQL Server.</span></span> <span data-ttu-id="96dbe-106">Bu değişiklikler de her iki platform arasında Azure Analysis Services toomaintain eşliği uygulanır.</span><span class="sxs-lookup"><span data-stu-id="96dbe-106">These changes are also implemented in Azure Analysis Services toomaintain parity between both platforms.</span></span> <span data-ttu-id="96dbe-107">Uyumluluk düzeyi değişiklikleri tablo Modellerinizi kullanılabilir özellikler de etkiler.</span><span class="sxs-lookup"><span data-stu-id="96dbe-107">Compatibility level changes also affect features available in your tabular models.</span></span> <span data-ttu-id="96dbe-108">Örneğin, DirectQuery ve tablo nesne meta verilerini hello uyumluluk düzeyine bağlı olarak farklı uygulamaları vardır.</span><span class="sxs-lookup"><span data-stu-id="96dbe-108">For example, DirectQuery and tabular object metadata have different implementations depending on hello compatibility level.</span></span> 

<span data-ttu-id="96dbe-109">Azure Analysis Services tablolu modeller hello 1200 ve 1400 Uyumluluk Düzeyleri destekler.</span><span class="sxs-lookup"><span data-stu-id="96dbe-109">Azure Analysis Services supports tabular models at hello 1200 and 1400 compatibility levels.</span></span>

<span data-ttu-id="96dbe-110">Merhaba son uyumluluk düzeyi 1400 ' dir.</span><span class="sxs-lookup"><span data-stu-id="96dbe-110">hello latest compatibility level is 1400.</span></span> <span data-ttu-id="96dbe-111">Bu düzey, SQL Server 2017 Analysis Services ile örtüşür.</span><span class="sxs-lookup"><span data-stu-id="96dbe-111">This level coincides with SQL Server 2017 Analysis Services.</span></span> <span data-ttu-id="96dbe-112">Merhaba 1400 uyumluluk düzeyi önemli özellikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="96dbe-112">Major features in hello 1400 compatibility level include:</span></span>

*  <span data-ttu-id="96dbe-113">Veri bağlantısı ve tablolu modeller içe için yeni altyapı ZEL API'ları ve TMSL scripting desteği.</span><span class="sxs-lookup"><span data-stu-id="96dbe-113">New infrastructure for data connectivity and import into tabular models with support for TOM APIs and TMSL scripting.</span></span> <span data-ttu-id="96dbe-114">Bu yeni özellik, Azure Blob Depolama alanı gibi ek veri kaynaklarını desteğini etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="96dbe-114">This new feature enables support for additional data sources such as Azure Blob storage.</span></span>
*  <span data-ttu-id="96dbe-115">Veri dönüştürme ve Veri Al ve M ifadeler kullanarak veri karma özellikleri.</span><span class="sxs-lookup"><span data-stu-id="96dbe-115">Data transformation and data mashup capabilities by using Get Data and M expressions.</span></span>
*  <span data-ttu-id="96dbe-116">Ölçüler bir DAX ifadesi ayrıntı satırları özelliğiyle destekler.</span><span class="sxs-lookup"><span data-stu-id="96dbe-116">Measures support a Detail Rows property with a DAX expression.</span></span> <span data-ttu-id="96dbe-117">Bu özelliği, Microsoft Excel toodrill toodetailed veri bir toplanmış raporundan aşağı gibi istemci araçlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="96dbe-117">This property enables client tools like Microsoft Excel toodrill down toodetailed data from an aggregated report.</span></span> <span data-ttu-id="96dbe-118">Örneğin, kullanıcıların ay ve bölge için toplam satış görüntülediğinizde ilişkili hello sipariş ayrıntılarını görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96dbe-118">For example, when users view total sales for a region and month, they can view hello associated order details.</span></span> 
*  <span data-ttu-id="96dbe-119">Nesne düzeyinde güvenlik için tablo ve sütun adları, ayrıca bunların içindeki toohello veri.</span><span class="sxs-lookup"><span data-stu-id="96dbe-119">Object-level security for table and column names, in addition toohello data within them.</span></span>
*  <span data-ttu-id="96dbe-120">Düzensiz hiyerarşileri için gelişmiş destek.</span><span class="sxs-lookup"><span data-stu-id="96dbe-120">Enhanced support for ragged hierarchies.</span></span>
*  <span data-ttu-id="96dbe-121">Performans ve izleme geliştirmeleri.</span><span class="sxs-lookup"><span data-stu-id="96dbe-121">Performance and monitoring improvements.</span></span>
  
## <a name="set-compatibility-level"></a><span data-ttu-id="96dbe-122">Set uyumluluk düzeyi</span><span class="sxs-lookup"><span data-stu-id="96dbe-122">Set compatibility level</span></span> 
 <span data-ttu-id="96dbe-123">SSDT içinde yeni bir tablo modeli projesi oluştururken, üzerinde hello hello uyumluluk düzeyini belirtebilirsiniz **Tabular modeli Tasarımcısı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="96dbe-123">When creating a new tabular model project in SSDT, you can specify hello compatibility level on hello **Tabular model designer** dialog.</span></span> 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 <span data-ttu-id="96dbe-125">Merhaba seçerseniz **bu iletiyi tekrar gösterme** seçeneği, tüm sonraki projeleri hello varsayılan olarak belirttiğiniz hello uyumluluk düzeyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="96dbe-125">If you select hello **Do not show this message again** option, all subsequent projects use hello compatibility level you specified as hello default.</span></span> <span data-ttu-id="96dbe-126">İçinde ssdt'de hello varsayılan uyumluluk düzeyini değiştirebilirsiniz **Araçları** > **seçenekleri**.</span><span class="sxs-lookup"><span data-stu-id="96dbe-126">You can change hello default compatibility level in SSDT in **Tools** > **Options**.</span></span>  
  
 <span data-ttu-id="96dbe-127">tooupgrade SSDT, kümesi hello var olan tablo modeli projesinde **uyumluluk düzeyini** hello modeli özelliğinde **özellikleri** penceresi.</span><span class="sxs-lookup"><span data-stu-id="96dbe-127">tooupgrade an existing tabular model project in SSDT, set  hello **Compatibility Level** property in hello model **Properties** window.</span></span> <span data-ttu-id="96dbe-128">İçinde-unutmayın, hello uyumluluk düzeyini yükseltme işlemi geri alınamaz.</span><span class="sxs-lookup"><span data-stu-id="96dbe-128">Keep in-mind, upgrading hello compatibility level is irreversible.</span></span>
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a><span data-ttu-id="96dbe-129">SQL Server Management Studio'da tablo modelli bir veritabanı uyumluluk düzeyi denetimi</span><span class="sxs-lookup"><span data-stu-id="96dbe-129">Check compatibility level for a tabular model database in SQL Server Management Studio</span></span> 
 <span data-ttu-id="96dbe-130">SSMS, hello veritabanı adına sağ tıklayın > **özellikleri** > **uyumluluk düzeyi**.</span><span class="sxs-lookup"><span data-stu-id="96dbe-130">In SSMS, right-click hello database name > **Properties** > **Compatibility Level**.</span></span>  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a><span data-ttu-id="96dbe-131">SSMS Server'da desteklenen uyumluluk düzeyini denetleyin</span><span class="sxs-lookup"><span data-stu-id="96dbe-131">Check supported compatibility level for a server in SSMS</span></span>  
 <span data-ttu-id="96dbe-132">SSMS, hello sunucu adına sağ tıklayın > **özellikleri** > **desteklenen uyumluluk düzeyi**.</span><span class="sxs-lookup"><span data-stu-id="96dbe-132">In SSMS, right-click hello server name>  **Properties** > **Supported Compatibility Level**.</span></span>  
  
 <span data-ttu-id="96dbe-133">Bu özellik hello yüksek uyumluluk düzeyini (Önizleme hariç) hello sunucuda çalışacak bir veritabanı belirtir.</span><span class="sxs-lookup"><span data-stu-id="96dbe-133">This property specifies hello highest compatibility level of a database that will run on hello server (excluding preview).</span></span> <span data-ttu-id="96dbe-134">desteklenen hello uyumluluk düzeyi değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="96dbe-134">hello supported compatibility level cannot be changed.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="96dbe-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="96dbe-135">Next steps</span></span>
  <span data-ttu-id="96dbe-136">[Azure portalında bir model oluşturma](analysis-services-create-model-portal.md) </span><span class="sxs-lookup"><span data-stu-id="96dbe-136">[Create a model in Azure portal](analysis-services-create-model-portal.md) </span></span>  
  [<span data-ttu-id="96dbe-137">Çözümleme Hizmetleri yönetme</span><span class="sxs-lookup"><span data-stu-id="96dbe-137">Manage Analysis Services</span></span>](analysis-services-manage.md)  
