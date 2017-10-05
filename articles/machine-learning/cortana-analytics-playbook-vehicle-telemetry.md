---
title: "Araç durumu tahmin etmek ve alışkanlık - Azure yürüten | Microsoft Docs"
description: "Araç sistem durumu ve yürüten gerçek zamanlı ve Tahmine dayalı Öngörüler elde etmek için Cortana Intelligence yeteneklerini kullanabilir alışkanlıklarınıza."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 09fad60b-2f48-488b-8a7e-47d1f969ec6f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: d202d314c61416cf306f760f93e0a4a88a1ab42b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a><span data-ttu-id="de619-103">Araç telemetri analizi çözüm kitabı</span><span class="sxs-lookup"><span data-stu-id="de619-103">Vehicle telemetry analytics solution playbook</span></span>
<span data-ttu-id="de619-104">Bu **menü** bu playbook bölümlerde bağlanır.</span><span class="sxs-lookup"><span data-stu-id="de619-104">This **menu** links to the chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a><span data-ttu-id="de619-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="de619-105">Overview</span></span>
<span data-ttu-id="de619-106">Süper bilgisayarlar Laboratuvarın dışına taşınmış ve şimdi bizim Garaj yerleşmiş durumdayken!</span><span class="sxs-lookup"><span data-stu-id="de619-106">Super computers have moved out of the lab and are now parked in our garage!</span></span> <span data-ttu-id="de619-107">Bu modern otomobiller algılayıcılar, izlemek ve saniyede milyonlarca olayı izleme olanağı veren çok sayıda içerir.</span><span class="sxs-lookup"><span data-stu-id="de619-107">These cutting-edge automobiles contain a myriad of sensors, giving them the ability to track and monitor millions of events every second.</span></span> <span data-ttu-id="de619-108">2020 tarafından bu araba çoğunu Internet'e bağlı, bekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="de619-108">We expect that by 2020, most of these cars will have been connected to the Internet.</span></span> <span data-ttu-id="de619-109">Bu bol miktarda büyük güvenlik, güvenilirlik ve daha iyi yönlendirmeli bir deneyim sağlamak için veri içine dokunma düşünün!</span><span class="sxs-lookup"><span data-stu-id="de619-109">Imagine tapping into this wealth of data to provide greater safety, reliability and a better driving experience!</span></span> <span data-ttu-id="de619-110">Microsoft, bu gerçekte Cortana Intelligence ile düş yapmıştır.</span><span class="sxs-lookup"><span data-stu-id="de619-110">Microsoft has made this dream a reality with Cortana Intelligence.</span></span>

<span data-ttu-id="de619-111">Microsoft'un Cortana Intelligence tam olarak yönetilen büyük veri ve akıllı eyleme verilerinizi dönüştürmenizi sağlar Gelişmiş analytics suite ' dir.</span><span class="sxs-lookup"><span data-stu-id="de619-111">Microsoft’s Cortana Intelligence is a fully managed big data and advanced analytics suite that enables you to transform your data into intelligent action.</span></span> <span data-ttu-id="de619-112">Cortana Intelligence araç Telemetri analizi çözüm şablonu tanıtmak istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="de619-112">We want to introduce you to the Cortana Intelligence Vehicle Telemetry Analytics Solution Template.</span></span> <span data-ttu-id="de619-113">Bu çözümün nasıl araba dealerships, otomobil üreticileri ve sigorta şirketler Cortana Intelligence yeteneklerini gerçek zamanlı kazanmak için kullanabilir ve araç sistem durumu ve yürüten Tahmine dayalı Öngörüler alışkanlıklarınıza gösterir.</span><span class="sxs-lookup"><span data-stu-id="de619-113">This solution demonstrates how car dealerships, automobile manufacturers, and insurance companies can use the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits.</span></span> 

<span data-ttu-id="de619-114">Çözüm olarak uygulanan bir [lambda mimarisi deseni](https://en.wikipedia.org/wiki/Lambda_architecture) tam için Cortana Intelligence platformun olası gösteren gerçek zamanlı ve toplu işleme.</span><span class="sxs-lookup"><span data-stu-id="de619-114">The solution is implemented as a [lambda architecture pattern](https://en.wikipedia.org/wiki/Lambda_architecture) showing the full potential of the Cortana Intelligence platform for real-time and batch processing.</span></span> <span data-ttu-id="de619-115">Çözüm:</span><span class="sxs-lookup"><span data-stu-id="de619-115">The solution:</span></span> 

* <span data-ttu-id="de619-116">bir araç telematik simulator sağlar</span><span class="sxs-lookup"><span data-stu-id="de619-116">provides a Vehicle Telematics simulator</span></span>
* <span data-ttu-id="de619-117">Event Hubs Azure'da sanal araç telemetri olayları milyonlarca alma yararlanır</span><span class="sxs-lookup"><span data-stu-id="de619-117">leverages Event Hubs for ingesting millions of simulated vehicle telemetry events into Azure</span></span> 
* <span data-ttu-id="de619-118">araç sistem üzerinde gerçek zamanlı Öngörüler elde etmek için Stream Analytics kullanır</span><span class="sxs-lookup"><span data-stu-id="de619-118">uses Stream Analytics to gain real-time insights on vehicle health</span></span>
* <span data-ttu-id="de619-119">verileri daha zengin toplu analiz için uzun vadeli depolamaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="de619-119">persists the data into long-term storage for richer batch analytics.</span></span> 
* <span data-ttu-id="de619-120">Machine Learning avantajlarından anomali algılama gerçek zamanlı yararlanır getirin ve Tahmine dayalı Öngörüler elde etmek için işleme toplu.</span><span class="sxs-lookup"><span data-stu-id="de619-120">takes advantage of Machine Learning for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="de619-121">ölçekli veri ve orchestration, planlama, kaynak yönetimi ve izleme toplu işleme ardışık işlemek için veri fabrikası dönüştürmek için Hdınsight yararlanır</span><span class="sxs-lookup"><span data-stu-id="de619-121">leverages HDInsight to transform data at scale and Data Factory to handle orchestration, scheduling, resource management, and monitoring of the batch processing pipeline</span></span> 
* <span data-ttu-id="de619-122">Bu çözüm gerçek zamanlı veri ve Power BI kullanarak Tahmine dayalı analiz görselleştirmeleri için zengin bir Pano sağlar</span><span class="sxs-lookup"><span data-stu-id="de619-122">gives this solution a rich dashboard for real-time data and predictive analytics visualizations using Power BI</span></span>

## <a name="architecture"></a><span data-ttu-id="de619-123">Mimari</span><span class="sxs-lookup"><span data-stu-id="de619-123">Architecture</span></span>
<span data-ttu-id="de619-124">![Çözüm mimarisi diyagramı](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Şekil 1 – araç Telemetri analizi çözüm mimarisi*</span><span class="sxs-lookup"><span data-stu-id="de619-124">![Solution architecture diagram](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figure 1 – Vehicle Telemetry Analytics Solution Architecture*</span></span>

<span data-ttu-id="de619-125">Bu çözümü şunlardır **Cortana Intelligence bileşenleri** ve bunların uçtan uca tümleştirme genişletilebileceğini gösterir:</span><span class="sxs-lookup"><span data-stu-id="de619-125">This solution includes the following **Cortana Intelligence components** and showcases their end to end integration:</span></span>

* <span data-ttu-id="de619-126">**Olay hub'ları** Azure'da araç telemetri olayları milyonlarca alma için.</span><span class="sxs-lookup"><span data-stu-id="de619-126">**Event Hubs** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="de619-127">**Akış analizi** araç sistem üzerinde gerçek zamanlı Öngörüler öğrenilmesi ve bu verileri daha zengin toplu analiz için uzun vadeli depolamaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="de619-127">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="de619-128">**Machine Learning** anomali algılama gerçek zamanlı ve toplu işleme Tahmine dayalı Öngörüler elde edin.</span><span class="sxs-lookup"><span data-stu-id="de619-128">**Machine Learning** for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="de619-129">**Hdınsight** ölçeğinde veri dönüştürme için de</span><span class="sxs-lookup"><span data-stu-id="de619-129">**HDInsight** is leveraged to transform data at scale</span></span>
* <span data-ttu-id="de619-130">**Veri Fabrikası** planlama, kaynak yönetimi ve izleme toplu işleme ardışık orchestration işler.</span><span class="sxs-lookup"><span data-stu-id="de619-130">**Data Factory** handles orchestration, scheduling, resource management and monitoring of the batch processing pipeline.</span></span>
* <span data-ttu-id="de619-131">**Power BI** gerçek zamanlı veri ve Tahmine dayalı analiz görselleştirmeleri için zengin bir Pano bu çözümü sunar.</span><span class="sxs-lookup"><span data-stu-id="de619-131">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span>

<span data-ttu-id="de619-132">Bu çözüm iki farklı erişen **veri kaynakları**:</span><span class="sxs-lookup"><span data-stu-id="de619-132">This solution accesses two different **data sources**:</span></span> 

* <span data-ttu-id="de619-133">**Benzetimli araç sinyalleri ve tanılama**: araç telematik simulator tanılama bilgileri ve karşılık gelen sinyalleri araç ve belirli bir noktada yönlendirmeli düzeni durumuna zamanında yayar.</span><span class="sxs-lookup"><span data-stu-id="de619-133">**Simulated vehicle signals and diagnostics**: A vehicle telematics simulator emits diagnostic information and signals that correspond to the state of the vehicle and the driving pattern at a given point in time.</span></span> 
* <span data-ttu-id="de619-134">**Araç katalog**: Toplamıdır modeli eşleme içeren bir başvuru veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="de619-134">**Vehicle catalog**: A reference dataset containing a VIN to model mapping.</span></span>

