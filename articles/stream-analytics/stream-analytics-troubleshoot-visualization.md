---
title: "Görselleştirme ve akış analizi işleri sorunlarını giderme | Microsoft Docs"
description: "Self Servis tanılama diyagramı özelliğini kullanarak sorun giderme akış analizi işi ardışık görselleştirmek öğrenin."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: d87841cd-c59f-4a46-b46e-8b904fdc12e9
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 18c39a025f750cf5a17c535ab40923b7cafe413d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a><span data-ttu-id="d3b26-103">Görselleştirme ve akış analizi işleri sorun giderme</span><span class="sxs-lookup"><span data-stu-id="d3b26-103">Visualize and troubleshoot Stream Analytics jobs</span></span>
<span data-ttu-id="d3b26-104">Stream Analytics içinde diğer teknolojilerle bulut tabanlı gibi sorun giderme bazen neden bir işi beklenen çıktı (veya bu herhangi bir çıktı) üretmez içine aramak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d3b26-104">In Stream Analytics, as with other cloud-based technologies, troubleshooting is sometimes needed to look into why a job does not produce the expected output (or any output for that matter).</span></span> <span data-ttu-id="d3b26-105">Bu durum dikkate alınarak, Stream Analytics iş akışında görselleştirme için yeteneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="d3b26-105">With this in mind, Stream Analytics provides the capability for visualizing a streaming job.</span></span> <span data-ttu-id="d3b26-106">Bu da bir modelleme araç olarak kullanışlı ve işlerine gerektiren bu belgeleri yan avantajına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d3b26-106">This is also handy as a modeling tool and has the side benefit for those requiring documentation of their work.</span></span>

<span data-ttu-id="d3b26-107">Görselleştirme panelinde girişleri yürütülmekte sorgu ve yapılandırılmış sonra tüm çıktıları yanı sıra görünür.</span><span class="sxs-lookup"><span data-stu-id="d3b26-107">In the visualization panel the inputs are visible as well as the query being executed and then all the outputs configured.</span></span> <span data-ttu-id="d3b26-108">Bağlantı veya yapılandırma sorunları daha belirgin hale gelebilir ve ayrıca yapılandırmanızı görsel gösterimi görmek yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="d3b26-108">Connectivity or configuration issues can become more apparent and it can also be helpful to see a visual representation of your configuration.</span></span>

## <a name="using-the-diagnosis-diagram-tool"></a><span data-ttu-id="d3b26-109">Tanılama diyagramı Aracı'nı kullanma</span><span class="sxs-lookup"><span data-stu-id="d3b26-109">Using the diagnosis diagram tool</span></span>
<span data-ttu-id="d3b26-110">Bu Görselleştirici erişmek için "Ayarlar" dikey penceresinde "Tanılama diyagramı" düğmesine tıklamanız yeterlidir akış analizi işinin.</span><span class="sxs-lookup"><span data-stu-id="d3b26-110">To access this visualizer, simply click on the “Diagnosis diagram” button in the “Settings” blade of the of the Stream Analytics job.</span></span>

![Stream-Analytics-Troubleshoot-visualization-Diagnosis-Diagram](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

<span data-ttu-id="d3b26-112">Her giriş ve çıkış o bileşenin durumunu renk kodlanmış geçerli göstermek için aşağıda gösterildiği gibi ' dir.</span><span class="sxs-lookup"><span data-stu-id="d3b26-112">Every input and output is color coded to indicate the current state of that component, as shown below.</span></span>

![Stream-Analytics-Troubleshoot-visualization-input-Map](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

<span data-ttu-id="d3b26-114">Kullanıcı bir iş içindeki veri akışı desenleri anlamak için Ara sorgu adımları bakmak istediğinde görselleştirme aracı bileşeni adımları ve akışı dizisi sorgu dökümünü bir görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="d3b26-114">When the user wants to look at intermediate query steps to understand the data flow patterns inside a job, the visualization tool provides a view of the breakdown of the query into its component steps and the flow sequence.</span></span> <span data-ttu-id="d3b26-115">Her sorgu adımını tıklatarak karşılık gelen gösterildiği gibi bölmesinde düzenleme sorguda gösterir.</span><span class="sxs-lookup"><span data-stu-id="d3b26-115">Clicking on each query step will show the corresponding section in a query editing pane as illustrated.</span></span> 

![Stream-Analytics-Troubleshoot-visualization-intermediate-Steps](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a><span data-ttu-id="d3b26-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d3b26-117">Next steps</span></span>
* [<span data-ttu-id="d3b26-118">Azure Stream Analytics'e giriş</span><span class="sxs-lookup"><span data-stu-id="d3b26-118">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="d3b26-119">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="d3b26-119">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="d3b26-120">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="d3b26-120">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="d3b26-121">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="d3b26-121">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="d3b26-122">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="d3b26-122">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

