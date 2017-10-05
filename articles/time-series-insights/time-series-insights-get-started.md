---
title: "Azure Zaman Serisi Görüşleri ortamı oluşturma | Microsoft Docs"
description: "Bu öğreticide, Zaman Serisi Ortamı oluşturmayı, bunu bir olay kaynağına bağlamayı ve dakikalar içinde olay verilerinizin analizine hazır olmayı öğreneceksiniz."
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
ms.openlocfilehash: eb710795916a2d7beea75a6408a0982fb4dc8750
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-new-time-series-insights-environment-in-the-azure-portal"></a><span data-ttu-id="0fa08-103">Azure Portal’da yeni Zaman Serisi Görüşleri ortamı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0fa08-103">Create a new Time Series Insights environment in the Azure portal</span></span>

<span data-ttu-id="0fa08-104">Zaman Serisi Görüşleri ortamı, giriş ve depolama kapasitesi olan bir Azure kaynağıdır.</span><span class="sxs-lookup"><span data-stu-id="0fa08-104">Time Series Insights environment is an Azure resource with ingress and storage capacity.</span></span> <span data-ttu-id="0fa08-105">Müşteriler, Azure Portal aracılığıyla ortamları gereken kapasiteyle hazırlar.</span><span class="sxs-lookup"><span data-stu-id="0fa08-105">Customers provision environments via the Azure portal with the required capacity.</span></span>

## <a name="steps-to-create-the-environment"></a><span data-ttu-id="0fa08-106">Ortam oluşturma adımları</span><span class="sxs-lookup"><span data-stu-id="0fa08-106">Steps to create the environment</span></span>

<span data-ttu-id="0fa08-107">Ortamınızı oluşturmak için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="0fa08-107">Follow these steps to create your environment:</span></span>

1.  <span data-ttu-id="0fa08-108">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="0fa08-108">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="0fa08-109">Sol üst köşedeki artı işaretine (“+”) tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0fa08-109">Click the plus sign (“+”) in the top left corner.</span></span>
3.  <span data-ttu-id="0fa08-110">Arama kutusunda “Zaman Serisi Görüşleri” için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="0fa08-110">Search for “Time Series Insights” in the search box.</span></span>

  ![Zaman Serisi Görüşleri oluşturma ortam](media/get-started/getstarted-create-environment1.png)

4.  <span data-ttu-id="0fa08-112">“Zaman Serisi Görüşleri” öğesini seçin, “Oluştur” düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0fa08-112">Select “Time Series Insights”, click “Create”.</span></span>

  ![Zaman Serisi Görüşleri oluşturma kaynak grubu](media/get-started/getstarted-create-environment2.png)

5.  <span data-ttu-id="0fa08-114">Ortam adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="0fa08-114">Specify environment name.</span></span> <span data-ttu-id="0fa08-115">Bu ad, [zaman serisi gezgininde](https://insights.timeseries.azure.com) ortamı temsil edecektir.</span><span class="sxs-lookup"><span data-stu-id="0fa08-115">This name will represent the environment in [time series explorer](https://insights.timeseries.azure.com).</span></span>
6.  <span data-ttu-id="0fa08-116">Bir abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="0fa08-116">Select a subscription.</span></span> <span data-ttu-id="0fa08-117">Olay kaynağınızı içeren aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="0fa08-117">Choose one that contains your event source.</span></span> <span data-ttu-id="0fa08-118">Zaman Serisi Görüşleri aynı abonelikteki mevcut Azure IoT Hub ve Event Hub kaynaklarını otomatik olarak algılayabilir.</span><span class="sxs-lookup"><span data-stu-id="0fa08-118">Time Series Insights can auto-detect Azure IoT Hub and Event Hub resources existing in the same subscription.</span></span>
7.  <span data-ttu-id="0fa08-119">Kaynak grubunu seçin veya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0fa08-119">Select or create a resource group.</span></span> <span data-ttu-id="0fa08-120">Kaynak grubu, birlikte kullanılan Azure kaynakları koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="0fa08-120">A resource group is a collection of Azure resources used together.</span></span>
8.  <span data-ttu-id="0fa08-121">Barındırma konumunu seçin.</span><span class="sxs-lookup"><span data-stu-id="0fa08-121">Select a hosting location.</span></span> <span data-ttu-id="0fa08-122">Verileri veri merkezleri arasında taşımaktan kaçınmak için, olay kaynağınızı içeren konumu seçin.</span><span class="sxs-lookup"><span data-stu-id="0fa08-122">To avoid moving data across data centers, choose location that contains your event source.</span></span>
9.  <span data-ttu-id="0fa08-123">Fiyatlandırma katmanını seçin.</span><span class="sxs-lookup"><span data-stu-id="0fa08-123">Select a pricing tier.</span></span>
10. <span data-ttu-id="0fa08-124">Kapasite seçin.</span><span class="sxs-lookup"><span data-stu-id="0fa08-124">Select capacity.</span></span> <span data-ttu-id="0fa08-125">Oluşturduktan sonra ortam kapasitesini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0fa08-125">You can change capacity of an environment after creation.</span></span>
11. <span data-ttu-id="0fa08-126">Ortamınızı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0fa08-126">Create your environment.</span></span> <span data-ttu-id="0fa08-127">Ayrıca, her oturum açtığınızda kolayca erişmek için ortamınızı panoya sabitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0fa08-127">You can also pin your environment to the dashboard for easy access whenever you sign in.</span></span>

  ![Zaman Serisi Görüşleri oluşturma panoya sabitleme](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a><span data-ttu-id="0fa08-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0fa08-129">Next steps</span></span>

* <span data-ttu-id="0fa08-130">[Zaman Serisi Görüşleri Portalı](time-series-insights-data-access.md)’nda ortamınıza erişmek için [veri erişim ilkelerini tanımlama](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="0fa08-130">[Define data access policies](time-series-insights-data-access.md) to access your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
* [<span data-ttu-id="0fa08-131">Olay kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0fa08-131">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="0fa08-132">Olay kaynağına [olayları gönderme](time-series-insights-send-events.md)</span><span class="sxs-lookup"><span data-stu-id="0fa08-132">[Send events](time-series-insights-send-events.md) to the event source</span></span>
