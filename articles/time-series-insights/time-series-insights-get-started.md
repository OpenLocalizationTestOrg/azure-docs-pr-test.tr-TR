---
title: "bir Azure zaman serisi Öngörüler ortam aaaCreate | Microsoft Docs"
description: "Bu öğreticide, nasıl toocreate zaman serisi ortam tooan olay kaynağına bağlanmak ve tooanalyze olay verilerinizi dakika içinde hazır öğreneceksiniz."
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: omravi
ms.openlocfilehash: 7120fc9a6e4d4a4972f8cb37e4d9945cfb746fd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-time-series-insights-environment-in-hello-azure-portal"></a><span data-ttu-id="a0366-103">Hello Azure portal yeni bir zaman serisi Öngörüler ortamı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a0366-103">Create a new Time Series Insights environment in hello Azure portal</span></span>

<span data-ttu-id="a0366-104">Zaman Serisi Görüşleri ortamı, giriş ve depolama kapasitesi olan bir Azure kaynağıdır.</span><span class="sxs-lookup"><span data-stu-id="a0366-104">Time Series Insights environment is an Azure resource with ingress and storage capacity.</span></span> <span data-ttu-id="a0366-105">Müşteriler hello gerekli kapasiteye sahip ortamlarda hello Azure portal aracılığıyla sağlayın.</span><span class="sxs-lookup"><span data-stu-id="a0366-105">Customers provision environments via hello Azure portal with hello required capacity.</span></span>

## <a name="steps-toocreate-hello-environment"></a><span data-ttu-id="a0366-106">Adımları toocreate hello ortamı</span><span class="sxs-lookup"><span data-stu-id="a0366-106">Steps toocreate hello environment</span></span>

<span data-ttu-id="a0366-107">Bu adımları toocreate ortamınızı izleyin:</span><span class="sxs-lookup"><span data-stu-id="a0366-107">Follow these steps toocreate your environment:</span></span>

1.  <span data-ttu-id="a0366-108">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a0366-108">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="a0366-109">Merhaba artı işareti ("+") içinde hello üst köşe sol tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a0366-109">Click hello plus sign (“+”) in hello top left corner.</span></span>
3.  <span data-ttu-id="a0366-110">"İçin zaman serisi Insights" Merhaba arama kutusuna arama yapın.</span><span class="sxs-lookup"><span data-stu-id="a0366-110">Search for “Time Series Insights” in hello search box.</span></span>

  ![Merhaba zaman serisi Öngörüler ortam oluşturma](media/get-started/getstarted-create-environment1.png)

4.  <span data-ttu-id="a0366-112">“Zaman Serisi Görüşleri” öğesini seçin, “Oluştur” düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a0366-112">Select “Time Series Insights”, click “Create”.</span></span>

  ![Merhaba zaman serisi Öngörüler kaynak grubu oluştur](media/get-started/getstarted-create-environment2.png)

5.  <span data-ttu-id="a0366-114">Ortam adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="a0366-114">Specify environment name.</span></span> <span data-ttu-id="a0366-115">Bu ad hello ortamında temsil edecek [zaman serisi explorer](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a0366-115">This name will represent hello environment in [time series explorer](https://insights.timeseries.azure.com).</span></span>
6.  <span data-ttu-id="a0366-116">Bir abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="a0366-116">Select a subscription.</span></span> <span data-ttu-id="a0366-117">Olay kaynağınızı içeren aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="a0366-117">Choose one that contains your event source.</span></span> <span data-ttu-id="a0366-118">Zaman serisi Öngörüler otomatik-Azure IOT Hub algılayabilir ve aynı abonelikte bulunan olay hub'ı kaynakları hello.</span><span class="sxs-lookup"><span data-stu-id="a0366-118">Time Series Insights can auto-detect Azure IoT Hub and Event Hub resources existing in hello same subscription.</span></span>
7.  <span data-ttu-id="a0366-119">Kaynak grubunu seçin veya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a0366-119">Select or create a resource group.</span></span> <span data-ttu-id="a0366-120">Kaynak grubu, birlikte kullanılan Azure kaynakları koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="a0366-120">A resource group is a collection of Azure resources used together.</span></span>
8.  <span data-ttu-id="a0366-121">Barındırma konumunu seçin.</span><span class="sxs-lookup"><span data-stu-id="a0366-121">Select a hosting location.</span></span> <span data-ttu-id="a0366-122">Veri tooavoid taşımayı arasında veri merkezleri, olay kaynağı içeren konumunu seçin.</span><span class="sxs-lookup"><span data-stu-id="a0366-122">tooavoid moving data across data centers, choose location that contains your event source.</span></span>
9.  <span data-ttu-id="a0366-123">Fiyatlandırma katmanını seçin.</span><span class="sxs-lookup"><span data-stu-id="a0366-123">Select a pricing tier.</span></span>
10. <span data-ttu-id="a0366-124">Kapasite seçin.</span><span class="sxs-lookup"><span data-stu-id="a0366-124">Select capacity.</span></span> <span data-ttu-id="a0366-125">Oluşturduktan sonra ortam kapasitesini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0366-125">You can change capacity of an environment after creation.</span></span>
11. <span data-ttu-id="a0366-126">Ortamınızı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a0366-126">Create your environment.</span></span> <span data-ttu-id="a0366-127">Oturum zaman ortam toohello panonuz kolay erişim için de sabitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0366-127">You can also pin your environment toohello dashboard for easy access whenever you sign in.</span></span>

  ![Merhaba zaman serisi Öngörüler PIN toodashboard oluşturma](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a><span data-ttu-id="a0366-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a0366-129">Next steps</span></span>

* <span data-ttu-id="a0366-130">[Veri erişim ilkeleri tanımlamanıza](time-series-insights-data-access.md) tooaccess ortamınızda [zaman serisi Insights portalı](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="a0366-130">[Define data access policies](time-series-insights-data-access.md) tooaccess your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
* [<span data-ttu-id="a0366-131">Olay kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a0366-131">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="a0366-132">[Olayları göndermek](time-series-insights-send-events.md) toohello olay kaynağı</span><span class="sxs-lookup"><span data-stu-id="a0366-132">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
