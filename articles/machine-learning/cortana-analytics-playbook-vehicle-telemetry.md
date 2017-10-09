---
title: "aaaPredict araç sistem durumu ve alışkanlık - Azure yürüten | Microsoft Docs"
description: "Yürüten alışkanlıklarınıza ve araç sistem durumunu Cortana Intelligence toogain gerçek zamanlı ve Tahmine dayalı Öngörüler Hello özelliklerini kullanın."
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
ms.openlocfilehash: 54cc890ff39493bc040bb809721388349665720f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a><span data-ttu-id="f3835-103">Araç telemetri analizi çözüm kitabı</span><span class="sxs-lookup"><span data-stu-id="f3835-103">Vehicle telemetry analytics solution playbook</span></span>
<span data-ttu-id="f3835-104">Bu **menü** bu playbook toohello bölümlerde bağlar.</span><span class="sxs-lookup"><span data-stu-id="f3835-104">This **menu** links toohello chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a><span data-ttu-id="f3835-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f3835-105">Overview</span></span>
<span data-ttu-id="f3835-106">Süper bilgisayarlar hello Laboratuvarın dışına taşınmış ve şimdi bizim Garaj yerleşmiş durumdayken!</span><span class="sxs-lookup"><span data-stu-id="f3835-106">Super computers have moved out of hello lab and are now parked in our garage!</span></span> <span data-ttu-id="f3835-107">Bu modern otomobiller saniyede milyonlarca etkinliği izlemek ve hello özelliği tootrack vermiş algılayıcılar, çok sayıda içerir.</span><span class="sxs-lookup"><span data-stu-id="f3835-107">These cutting-edge automobiles contain a myriad of sensors, giving them hello ability tootrack and monitor millions of events every second.</span></span> <span data-ttu-id="f3835-108">2020 tarafından bu araba çoğunu bağlı toohello Internet yapıldığını bekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="f3835-108">We expect that by 2020, most of these cars will have been connected toohello Internet.</span></span> <span data-ttu-id="f3835-109">Bu bol miktarda veri tooprovide büyük güvenlik, güvenilirlik ve daha iyi yönlendirmeli deneyimi içine dokunma düşünün!</span><span class="sxs-lookup"><span data-stu-id="f3835-109">Imagine tapping into this wealth of data tooprovide greater safety, reliability and a better driving experience!</span></span> <span data-ttu-id="f3835-110">Microsoft, bu gerçekte Cortana Intelligence ile düş yapmıştır.</span><span class="sxs-lookup"><span data-stu-id="f3835-110">Microsoft has made this dream a reality with Cortana Intelligence.</span></span>

<span data-ttu-id="f3835-111">Microsoft'un Cortana Intelligence tam olarak yönetilen bir büyük veri ve tootransform etkinleştirir analytics suite verilerinizi akıllı eyleme Gelişmiş.</span><span class="sxs-lookup"><span data-stu-id="f3835-111">Microsoft’s Cortana Intelligence is a fully managed big data and advanced analytics suite that enables you tootransform your data into intelligent action.</span></span> <span data-ttu-id="f3835-112">Toointroduce istiyoruz Cortana Intelligence araç Telemetri analizi çözüm şablonu toohello.</span><span class="sxs-lookup"><span data-stu-id="f3835-112">We want toointroduce you toohello Cortana Intelligence Vehicle Telemetry Analytics Solution Template.</span></span> <span data-ttu-id="f3835-113">Bu çözümün nasıl araba dealerships, otomobil üreticileri ve sigorta şirketler Cortana Intelligence toogain gerçek zamanlı hello yeteneklerini kullanabilir ve araç sistem durumu ve yürüten Tahmine dayalı Öngörüler alışkanlıklarınıza gösterir.</span><span class="sxs-lookup"><span data-stu-id="f3835-113">This solution demonstrates how car dealerships, automobile manufacturers, and insurance companies can use hello capabilities of Cortana Intelligence toogain real-time and predictive insights on vehicle health and driving habits.</span></span> 

<span data-ttu-id="f3835-114">Merhaba çözümü olarak gerçekleştirilen bir [lambda mimarisi deseni](https://en.wikipedia.org/wiki/Lambda_architecture) hello Cortana Intelligence platformu için tam potansiyelinin hello gösteren gerçek zamanlı ve toplu işleme.</span><span class="sxs-lookup"><span data-stu-id="f3835-114">hello solution is implemented as a [lambda architecture pattern](https://en.wikipedia.org/wiki/Lambda_architecture) showing hello full potential of hello Cortana Intelligence platform for real-time and batch processing.</span></span> <span data-ttu-id="f3835-115">Merhaba çözüm:</span><span class="sxs-lookup"><span data-stu-id="f3835-115">hello solution:</span></span> 

* <span data-ttu-id="f3835-116">bir araç telematik simulator sağlar</span><span class="sxs-lookup"><span data-stu-id="f3835-116">provides a Vehicle Telematics simulator</span></span>
* <span data-ttu-id="f3835-117">Event Hubs Azure'da sanal araç telemetri olayları milyonlarca alma yararlanır</span><span class="sxs-lookup"><span data-stu-id="f3835-117">leverages Event Hubs for ingesting millions of simulated vehicle telemetry events into Azure</span></span> 
* <span data-ttu-id="f3835-118">Stream Analytics toogain gerçek zamanlı Öngörüler araç sistem durumunu kullanır</span><span class="sxs-lookup"><span data-stu-id="f3835-118">uses Stream Analytics toogain real-time insights on vehicle health</span></span>
* <span data-ttu-id="f3835-119">Merhaba verileri daha zengin toplu analiz için uzun vadeli depolamaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="f3835-119">persists hello data into long-term storage for richer batch analytics.</span></span> 
* <span data-ttu-id="f3835-120">Machine Learning avantajlarından anomali algılama gerçek zamanlı yararlanır getirin ve toplu işleme toogain Tahmine dayalı Öngörüler.</span><span class="sxs-lookup"><span data-stu-id="f3835-120">takes advantage of Machine Learning for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="f3835-121">Ölçek ve Data Factory toohandle orchestration, planlama, kaynak yönetimi ve hello toplu işleme ardışık izleme Hdınsight tootransform veri yararlanır</span><span class="sxs-lookup"><span data-stu-id="f3835-121">leverages HDInsight tootransform data at scale and Data Factory toohandle orchestration, scheduling, resource management, and monitoring of hello batch processing pipeline</span></span> 
* <span data-ttu-id="f3835-122">Bu çözüm gerçek zamanlı veri ve Power BI kullanarak Tahmine dayalı analiz görselleştirmeleri için zengin bir Pano sağlar</span><span class="sxs-lookup"><span data-stu-id="f3835-122">gives this solution a rich dashboard for real-time data and predictive analytics visualizations using Power BI</span></span>

## <a name="architecture"></a><span data-ttu-id="f3835-123">Mimari</span><span class="sxs-lookup"><span data-stu-id="f3835-123">Architecture</span></span>
<span data-ttu-id="f3835-124">![Çözüm mimarisi diyagramı](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Şekil 1 – araç Telemetri analizi çözüm mimarisi*</span><span class="sxs-lookup"><span data-stu-id="f3835-124">![Solution architecture diagram](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figure 1 – Vehicle Telemetry Analytics Solution Architecture*</span></span>

<span data-ttu-id="f3835-125">Bu çözüm hello aşağıdakileri içeren **Cortana Intelligence bileşenleri** ve bunların son tooend tümleştirme genişletilebileceğini gösterir:</span><span class="sxs-lookup"><span data-stu-id="f3835-125">This solution includes hello following **Cortana Intelligence components** and showcases their end tooend integration:</span></span>

* <span data-ttu-id="f3835-126">**Olay hub'ları** Azure'da araç telemetri olayları milyonlarca alma için.</span><span class="sxs-lookup"><span data-stu-id="f3835-126">**Event Hubs** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="f3835-127">**Akış analizi** araç sistem üzerinde gerçek zamanlı Öngörüler öğrenilmesi ve bu verileri daha zengin toplu analiz için uzun vadeli depolamaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="f3835-127">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="f3835-128">**Machine Learning** anomali algılama gerçek zamanlı ve toplu toogain Tahmine dayalı Öngörüler işleme.</span><span class="sxs-lookup"><span data-stu-id="f3835-128">**Machine Learning** for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="f3835-129">**Hdınsight** ölçekte çevrelerini tootransform veriler</span><span class="sxs-lookup"><span data-stu-id="f3835-129">**HDInsight** is leveraged tootransform data at scale</span></span>
* <span data-ttu-id="f3835-130">**Veri Fabrikası** planlama, kaynak yönetimi ve izleme hello toplu işleme ardışık orchestration işler.</span><span class="sxs-lookup"><span data-stu-id="f3835-130">**Data Factory** handles orchestration, scheduling, resource management and monitoring of hello batch processing pipeline.</span></span>
* <span data-ttu-id="f3835-131">**Power BI** gerçek zamanlı veri ve Tahmine dayalı analiz görselleştirmeleri için zengin bir Pano bu çözümü sunar.</span><span class="sxs-lookup"><span data-stu-id="f3835-131">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span>

<span data-ttu-id="f3835-132">Bu çözüm iki farklı erişen **veri kaynakları**:</span><span class="sxs-lookup"><span data-stu-id="f3835-132">This solution accesses two different **data sources**:</span></span> 

* <span data-ttu-id="f3835-133">**Benzetimli araç sinyalleri ve tanılama**: tanı bilgilerini ve toohello durumunu hello araç ve düzeni, zaman içinde belirli bir anda yürüten hello karşılık gelen sinyalleri bir araç telematik simulator yayar.</span><span class="sxs-lookup"><span data-stu-id="f3835-133">**Simulated vehicle signals and diagnostics**: A vehicle telematics simulator emits diagnostic information and signals that correspond toohello state of hello vehicle and hello driving pattern at a given point in time.</span></span> 
* <span data-ttu-id="f3835-134">**Araç katalog**: Toplamıdır toomodel eşleme içeren bir başvuru veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="f3835-134">**Vehicle catalog**: A reference dataset containing a VIN toomodel mapping.</span></span>

