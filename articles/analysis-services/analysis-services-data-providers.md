---
title: "tooAzure Analysis Services bağlanmak için gereken aaaClient kitaplığı | Microsoft Docs"
description: "İstemci uygulamaları ve araçları tooconnect için Azure Analysis Services gerekli istemci kitaplıkları açıklar"
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
ms.openlocfilehash: 74ba5c05ba76c6587c5aed38f200a1ba469aa4f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="client-libraries-for-connecting-tooazure-analysis-services"></a><span data-ttu-id="d7b89-103">TooAzure Analysis Services bağlanmak için istemci kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="d7b89-103">Client libraries for connecting tooAzure Analysis Services</span></span>

<span data-ttu-id="d7b89-104">İstemci uygulamaları ve araçları tooconnect tooAnalysis Services sunucuları için istemci kitaplıkları gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d7b89-104">Client libraries are necessary for client applications and tools tooconnect tooAnalysis Services servers.</span></span> 

<span data-ttu-id="d7b89-105">Analysis Services üç istemci kitaplıkları kullanın.</span><span class="sxs-lookup"><span data-stu-id="d7b89-105">Analysis Services utilize three client libraries.</span></span> <span data-ttu-id="d7b89-106">ADOMD.NET ve Analysis Services yönetim nesneleri (AMO), yönetilen istemci kitaplıkları markalarıdır.</span><span class="sxs-lookup"><span data-stu-id="d7b89-106">ADOMD.NET and Analysis Services Management Objects (AMO), are managed client libraries.</span></span> <span data-ttu-id="d7b89-107">Merhaba Analysis Services OLE DB sağlayıcısı (MSOLAP DLL) yerel istemci Kitaplığı'dır.</span><span class="sxs-lookup"><span data-stu-id="d7b89-107">hello Analysis Services OLE DB provider (MSOLAP DLL) is a native client library.</span></span> <span data-ttu-id="d7b89-108">Genellikle, tüm üç hello yüklenir aynı anda.</span><span class="sxs-lookup"><span data-stu-id="d7b89-108">Typically, all three are installed at hello same time.</span></span> <span data-ttu-id="d7b89-109">Azure Analysis Services hello en son sürümlerini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d7b89-109">Azure Analysis Services requires hello latest versions.</span></span> 

<span data-ttu-id="d7b89-110">Microsoft Power BI Desktop ve Excel gibi istemci uygulamalarını, tüm üç istemci kitaplıkları yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d7b89-110">Microsoft client applications such as Power BI Desktop and Excel install all three client libraries.</span></span> <span data-ttu-id="d7b89-111">Ancak, hello sürümü veya güncelleştirmelerinin sıklığını bağlı olarak, istemci kitaplıkları hello en son sürümleri Azure Analysis Services tarafından gerekli olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="d7b89-111">However, depending on hello version or frequency of updates, client libraries may not be hello latest versions required by Azure Analysis Services.</span></span> <span data-ttu-id="d7b89-112">Merhaba aynı toocustom uygulamaları veya AsCmd, ZEL, ADOMD.NET gibi diğer arabirimleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d7b89-112">hello same applies toocustom applications or other interfaces such as AsCmd, TOM, ADOMD.NET.</span></span> <span data-ttu-id="d7b89-113">Bu uygulamalar, el ile Merhaba kitaplıkları yükleme gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d7b89-113">These applications require manually installing hello libraries.</span></span> <span data-ttu-id="d7b89-114">Merhaba istemci kitaplıkları el ile yükleme için SQL Server özellik paketlerinde dağıtılabilir paketleri dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="d7b89-114">hello client libraries for manual installation are included in SQL Server feature packs as distributable packages.</span></span> <span data-ttu-id="d7b89-115">Ancak, bu istemci kitaplıkları bağlı toohello SQL Server sürümü ve hello son olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="d7b89-115">However, these client libraries are tied toohello SQL Server version and may not be hello latest.</span></span>  

<span data-ttu-id="d7b89-116">İstemci bağlantıları için istemci kitaplıkları, Azure Analysis Services sunucusu tooa veri kaynağından veri sağlayıcıları gerekli tooconnect farklıdır.</span><span class="sxs-lookup"><span data-stu-id="d7b89-116">Client libraries for client connections are different from data providers required tooconnect from an Azure Analysis Services server tooa data source.</span></span> <span data-ttu-id="d7b89-117">veri kaynağı bağlantıları hakkında daha fazla toolearn bkz [veri kaynağı bağlantıları](analysis-services-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="d7b89-117">toolearn more about datasource connections, see [Datasource connections](analysis-services-datasource.md).</span></span>

## <a name="download-hello-latest-client-libraries"></a><span data-ttu-id="d7b89-118">Merhaba son istemci kitaplıkları indirin</span><span class="sxs-lookup"><span data-stu-id="d7b89-118">Download hello latest client libraries</span></span>  
<span data-ttu-id="d7b89-119">Bir üretim ortamında olan ve tam olarak yayımlanan ve desteklenen sürümlerini gerektirir istemci kitaplıkları aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="d7b89-119">Use hello following client libraries if you are in a production environment and require fully released and supported versions.</span></span>

[<span data-ttu-id="d7b89-120">MSOLAP (amd64)</span><span class="sxs-lookup"><span data-stu-id="d7b89-120">MSOLAP (amd64)</span></span>](https://go.microsoft.com/fwlink/?linkid=829576)</br><span data-ttu-id="d7b89-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span><span class="sxs-lookup"><span data-stu-id="d7b89-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span></span></br><span data-ttu-id="d7b89-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span><span class="sxs-lookup"><span data-stu-id="d7b89-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span></span></br><span data-ttu-id="d7b89-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span><span class="sxs-lookup"><span data-stu-id="d7b89-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="d7b89-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d7b89-124">Next steps</span></span>
<span data-ttu-id="d7b89-125">[Excel ile bağlanma](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="d7b89-125">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
[<span data-ttu-id="d7b89-126">Power BI ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="d7b89-126">Connect with Power BI</span></span>](analysis-services-connect-pbi.md)
