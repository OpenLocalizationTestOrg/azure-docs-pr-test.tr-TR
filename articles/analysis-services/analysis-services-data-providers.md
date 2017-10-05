---
title: "Azure Analysis Services'a bağlanmak için gereken istemci kitaplığı | Microsoft Docs"
description: "Azure Analysis Services bağlanmak istemci uygulamaları ve araçları için gerekli istemci kitaplıkları açıklar"
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
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: a96e7fe671dc051da35168fa7b49ecba53b4c4a5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="client-libraries-for-connecting-to-azure-analysis-services"></a><span data-ttu-id="50a74-103">Azure Analysis Services'a bağlanmak için istemci kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="50a74-103">Client libraries for connecting to Azure Analysis Services</span></span>

<span data-ttu-id="50a74-104">İstemci kitaplıkları, Analysis Services sunucularına bağlanmak için istemci uygulamaları ve araçları için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="50a74-104">Client libraries are necessary for client applications and tools to connect to Analysis Services servers.</span></span> 

<span data-ttu-id="50a74-105">Analysis Services üç istemci kitaplıkları kullanın.</span><span class="sxs-lookup"><span data-stu-id="50a74-105">Analysis Services utilize three client libraries.</span></span> <span data-ttu-id="50a74-106">ADOMD.NET ve Analysis Services yönetim nesneleri (AMO), yönetilen istemci kitaplıkları markalarıdır.</span><span class="sxs-lookup"><span data-stu-id="50a74-106">ADOMD.NET and Analysis Services Management Objects (AMO), are managed client libraries.</span></span> <span data-ttu-id="50a74-107">Analysis Services OLE DB sağlayıcısı (MSOLAP DLL) yerel istemci Kitaplığı ' dir.</span><span class="sxs-lookup"><span data-stu-id="50a74-107">The Analysis Services OLE DB provider (MSOLAP DLL) is a native client library.</span></span> <span data-ttu-id="50a74-108">Genellikle, tüm üç aynı anda yüklenir.</span><span class="sxs-lookup"><span data-stu-id="50a74-108">Typically, all three are installed at the same time.</span></span> <span data-ttu-id="50a74-109">Azure Analysis Services en son sürümlerini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="50a74-109">Azure Analysis Services requires the latest versions.</span></span> 

<span data-ttu-id="50a74-110">Microsoft Power BI Desktop ve Excel gibi istemci uygulamalarını, tüm üç istemci kitaplıkları yükleyin.</span><span class="sxs-lookup"><span data-stu-id="50a74-110">Microsoft client applications such as Power BI Desktop and Excel install all three client libraries.</span></span> <span data-ttu-id="50a74-111">Ancak, sürüm veya güncelleştirmelerinin sıklığını bağlı olarak, istemci kitaplıkları Azure Analysis Services tarafından gerekli en son sürümlerini olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="50a74-111">However, depending on the version or frequency of updates, client libraries may not be the latest versions required by Azure Analysis Services.</span></span> <span data-ttu-id="50a74-112">Aynı durum AsCmd, TOM, ADOMD.NET gibi özel uygulamalar ve diğer arabirimler için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="50a74-112">The same applies to custom applications or other interfaces such as AsCmd, TOM, ADOMD.NET.</span></span> <span data-ttu-id="50a74-113">Bu uygulamalar, el ile kitaplıkları yükleme gerektirir.</span><span class="sxs-lookup"><span data-stu-id="50a74-113">These applications require manually installing the libraries.</span></span> <span data-ttu-id="50a74-114">İstemci kitaplıkları el ile yükleme için SQL Server özellik paketlerinde dağıtılabilir paketleri dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="50a74-114">The client libraries for manual installation are included in SQL Server feature packs as distributable packages.</span></span> <span data-ttu-id="50a74-115">Ancak, bu istemci kitaplıkları, SQL Server sürümüne bağlıdır ve en son olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="50a74-115">However, these client libraries are tied to the SQL Server version and may not be the latest.</span></span>  

<span data-ttu-id="50a74-116">İstemci bağlantıları için istemci kitaplıkları, Azure Analysis Services sunucusundan bir veri kaynağına bağlanmak için gereken veri sağlayıcıları farklıdır.</span><span class="sxs-lookup"><span data-stu-id="50a74-116">Client libraries for client connections are different from data providers required to connect from an Azure Analysis Services server to a data source.</span></span> <span data-ttu-id="50a74-117">Veri kaynağı bağlantıları hakkında daha fazla bilgi için bkz: [veri kaynağı bağlantıları](analysis-services-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="50a74-117">To learn more about datasource connections, see [Datasource connections](analysis-services-datasource.md).</span></span>

## <a name="download-the-latest-client-libraries"></a><span data-ttu-id="50a74-118">Son istemci kitaplıkları indirin</span><span class="sxs-lookup"><span data-stu-id="50a74-118">Download the latest client libraries</span></span>  
<span data-ttu-id="50a74-119">Aşağıdaki istemci kitaplıklarından kullanın bir üretim ortamında olan ve tam olarak yayımlanan ve desteklenen sürümlerini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="50a74-119">Use the following client libraries if you are in a production environment and require fully released and supported versions.</span></span>

[<span data-ttu-id="50a74-120">MSOLAP (amd64)</span><span class="sxs-lookup"><span data-stu-id="50a74-120">MSOLAP (amd64)</span></span>](https://go.microsoft.com/fwlink/?linkid=829576)</br><span data-ttu-id="50a74-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span><span class="sxs-lookup"><span data-stu-id="50a74-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span></span></br><span data-ttu-id="50a74-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span><span class="sxs-lookup"><span data-stu-id="50a74-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span></span></br><span data-ttu-id="50a74-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span><span class="sxs-lookup"><span data-stu-id="50a74-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="50a74-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="50a74-124">Next steps</span></span>
<span data-ttu-id="50a74-125">[Excel ile bağlanma](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="50a74-125">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
[<span data-ttu-id="50a74-126">Power BI ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="50a74-126">Connect with Power BI</span></span>](analysis-services-connect-pbi.md)
