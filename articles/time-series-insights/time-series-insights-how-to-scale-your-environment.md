---
title: "aaaHow tooscale Azure zaman serisi Öngörüler ortamınızı | Microsoft Docs"
description: "Bu öğretici kapsayan nasıl tooscale Azure zaman serisi Öngörüler ortamınızı"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: 55eda388997589185bd34228762b95e182b228ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-your-time-series-insights-environment"></a><span data-ttu-id="f570f-103">Nasıl tooscale zaman serisi Öngörüler ortamınızı</span><span class="sxs-lookup"><span data-stu-id="f570f-103">How tooscale your Time Series Insights environment</span></span>

<span data-ttu-id="f570f-104">Bu öğretici kapsayan nasıl tooscale zaman serisi Öngörüler ortamınızı.</span><span class="sxs-lookup"><span data-stu-id="f570f-104">This tutorial covers how tooscale your Time Series Insights environment.</span></span>

> [!NOTE]
> <span data-ttu-id="f570f-105">Ölçek büyütme sku türleri arasında izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="f570f-105">Scale up across sku types is not allowed.</span></span> <span data-ttu-id="f570f-106">S1 Sku olan bir ortamda bir S2 ortamına dönüştürülemiyor.</span><span class="sxs-lookup"><span data-stu-id="f570f-106">An environment with a S1 Sku cannot be converted into an S2 environment.</span></span>

## <a name="s1-sku-ingress-rates-and-capacities"></a><span data-ttu-id="f570f-107">S1 SKU giriş hızları ve kapasiteleri</span><span class="sxs-lookup"><span data-stu-id="f570f-107">S1 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="f570f-108">S1 SKU kapasitesi</span><span class="sxs-lookup"><span data-stu-id="f570f-108">S1 SKU Capacity</span></span> | <span data-ttu-id="f570f-109">Giriş oranı</span><span class="sxs-lookup"><span data-stu-id="f570f-109">Ingress Rate</span></span> | <span data-ttu-id="f570f-110">Maksimum depolama kapasitesi</span><span class="sxs-lookup"><span data-stu-id="f570f-110">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="f570f-111">1</span><span class="sxs-lookup"><span data-stu-id="f570f-111">1</span></span> | <span data-ttu-id="f570f-112">1 GB (1 milyon olay)</span><span class="sxs-lookup"><span data-stu-id="f570f-112">1 GB (1 million events)</span></span> | <span data-ttu-id="f570f-113">Aylık 30 GB (30 milyon olay)</span><span class="sxs-lookup"><span data-stu-id="f570f-113">30 GB (30 million events) per month</span></span> |
| <span data-ttu-id="f570f-114">10</span><span class="sxs-lookup"><span data-stu-id="f570f-114">10</span></span> | <span data-ttu-id="f570f-115">10 GB (10 milyon olay)</span><span class="sxs-lookup"><span data-stu-id="f570f-115">10 GB (10 million events)</span></span> | <span data-ttu-id="f570f-116">Ayda 300 GB (300 milyon olay)</span><span class="sxs-lookup"><span data-stu-id="f570f-116">300 GB (300 million events) per month</span></span> |

## <a name="s2-sku-ingress-rates-and-capacities"></a><span data-ttu-id="f570f-117">S2 SKU giriş hızları ve kapasiteleri</span><span class="sxs-lookup"><span data-stu-id="f570f-117">S2 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="f570f-118">S2 SKU kapasitesi</span><span class="sxs-lookup"><span data-stu-id="f570f-118">S2 SKU Capacity</span></span> | <span data-ttu-id="f570f-119">Giriş oranı</span><span class="sxs-lookup"><span data-stu-id="f570f-119">Ingress Rate</span></span> | <span data-ttu-id="f570f-120">Maksimum depolama kapasitesi</span><span class="sxs-lookup"><span data-stu-id="f570f-120">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="f570f-121">1</span><span class="sxs-lookup"><span data-stu-id="f570f-121">1</span></span> | <span data-ttu-id="f570f-122">10 GB (10 milyon olay)</span><span class="sxs-lookup"><span data-stu-id="f570f-122">10 GB (10 million events)</span></span> | <span data-ttu-id="f570f-123">Ayda 300 GB (300 milyon olay)</span><span class="sxs-lookup"><span data-stu-id="f570f-123">300 GB (300 million events) per month</span></span> |
| <span data-ttu-id="f570f-124">10</span><span class="sxs-lookup"><span data-stu-id="f570f-124">10</span></span> | <span data-ttu-id="f570f-125">100 GB (100 milyon olay)</span><span class="sxs-lookup"><span data-stu-id="f570f-125">100 GB (100 million events)</span></span> | <span data-ttu-id="f570f-126">Aylık 3 TB (3 milyon olay)</span><span class="sxs-lookup"><span data-stu-id="f570f-126">3 TB (3 billion events) per month</span></span> |

<span data-ttu-id="f570f-127">Kapasiteleri doğrusal olarak, S1 sku kapasitesi 2 ile her ay gün giriş oranı ve 60 GB (60 milyon olayları) başına 2 GB (2 milyon) olayları destekler şekilde ölçeklendirilir.</span><span class="sxs-lookup"><span data-stu-id="f570f-127">Capacities scale linearly, so a S1 sku with capacity 2 supports 2 GB (2 million) events per day ingress rate and 60 GB (60 million events) per month.</span></span>

## <a name="changing-hello-capacity-of-your-environment"></a><span data-ttu-id="f570f-128">Merhaba kapasite ortamınızın değiştirme</span><span class="sxs-lookup"><span data-stu-id="f570f-128">Changing hello capacity of your environment</span></span>

1. <span data-ttu-id="f570f-129">Hello Azure portal, select ortamı, kapasite hello toochange istiyor.</span><span class="sxs-lookup"><span data-stu-id="f570f-129">In hello Azure portal, select hello environment whose capacity you want toochange.</span></span>
1. <span data-ttu-id="f570f-130">Ayarlar altında Yapılandır'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f570f-130">Under Settings, click Configure.</span></span>
1. <span data-ttu-id="f570f-131">Giriş ücretlerinizi hello gereksinimlerini karşılayan hello kapasite kaydırıcı tooselect hello kapasitesini ve depolama kapasitesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f570f-131">Use hello Capacity slider tooselect hello capacity that meets hello requirements for your ingress rates and storage capacity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f570f-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f570f-132">Next steps</span></span>

* <span data-ttu-id="f570f-133">Merhaba yeni kapasite yeterli olduğunu doğrulayın tooprevent azaltma.</span><span class="sxs-lookup"><span data-stu-id="f570f-133">Verify that hello new capacity is sufficient tooprevent throttling.</span></span> <span data-ttu-id="f570f-134">Merhaba daha fazla ayrıntı için bkz *ortamınızı bastırma* bölüm [burada](time-series-insights-diagnose-and-solve-problems.md).</span><span class="sxs-lookup"><span data-stu-id="f570f-134">For more details, see hello *Your environment might be getting throttled* section [here](time-series-insights-diagnose-and-solve-problems.md).</span></span>
