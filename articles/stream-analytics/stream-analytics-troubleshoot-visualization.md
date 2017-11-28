---
title: "aaaVisualize ve akış analizi işleri sorunlarını giderme | Microsoft Docs"
description: "Toovisualize akış analizi işi Self Servis hello tanılama diyagramı özelliğini kullanarak sorun giderme için nasıl potansiyel satış öğrenin."
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
ms.openlocfilehash: 8a6715be601fdc47b8d9caf4112da161dad22618
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a><span data-ttu-id="b1248-103">Görselleştirme ve akış analizi işleri sorun giderme</span><span class="sxs-lookup"><span data-stu-id="b1248-103">Visualize and troubleshoot Stream Analytics jobs</span></span>
<span data-ttu-id="b1248-104">Stream Analytics içinde diğer teknolojilerle bulut tabanlı gibi ilgili sorun giderme bazen neden bir işi hello beklenen çıktı (veya bu herhangi bir çıktı) üretmez içine gerekli toolook kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b1248-104">In Stream Analytics, as with other cloud-based technologies, troubleshooting is sometimes needed toolook into why a job does not produce hello expected output (or any output for that matter).</span></span> <span data-ttu-id="b1248-105">Bu durum dikkate alınarak, Stream Analytics iş akışında görselleştirme için hello yeteneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="b1248-105">With this in mind, Stream Analytics provides hello capability for visualizing a streaming job.</span></span> <span data-ttu-id="b1248-106">Bu da bir modelleme araç olarak kullanışlı ve kişiler işlerine belgelerine gerektiren hello yan avantajına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="b1248-106">This is also handy as a modeling tool and has hello side benefit for those requiring documentation of their work.</span></span>

<span data-ttu-id="b1248-107">Merhaba görselleştirme paneli hello girişleri yürütülmekte hello sorgu yanı sıra görünür ve tüm hello çıkışları yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="b1248-107">In hello visualization panel hello inputs are visible as well as hello query being executed and then all hello outputs configured.</span></span> <span data-ttu-id="b1248-108">Bağlantı veya yapılandırma sorunları daha belirgin hale gelebilir ve yararlı toosee görsel bir yapılandırmanızı olabilir.</span><span class="sxs-lookup"><span data-stu-id="b1248-108">Connectivity or configuration issues can become more apparent and it can also be helpful toosee a visual representation of your configuration.</span></span>

## <a name="using-hello-diagnosis-diagram-tool"></a><span data-ttu-id="b1248-109">Merhaba tanılama diyagramı aracını kullanma</span><span class="sxs-lookup"><span data-stu-id="b1248-109">Using hello diagnosis diagram tool</span></span>
<span data-ttu-id="b1248-110">yalnızca tıklayarak bu Görselleştirici hello "Tanılama diyagramı" düğmesini tooaccess hello hello Stream Analytics işi, "Ayarlar" dikey hello.</span><span class="sxs-lookup"><span data-stu-id="b1248-110">tooaccess this visualizer, simply click on hello “Diagnosis diagram” button in hello “Settings” blade of hello of hello Stream Analytics job.</span></span>

![Stream-Analytics-Troubleshoot-visualization-Diagnosis-Diagram](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

<span data-ttu-id="b1248-112">Her giriş ve çıkış renk kodlu tooindicate hello geçerli o bileşenin durumunu, aşağıda gösterildiği gibi ' dir.</span><span class="sxs-lookup"><span data-stu-id="b1248-112">Every input and output is color coded tooindicate hello current state of that component, as shown below.</span></span>

![Stream-Analytics-Troubleshoot-visualization-input-Map](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

<span data-ttu-id="b1248-114">Merhaba kullanıcı toolook Ara sorgu adımları toounderstand hello veri akışı desenleri bir işi içinde istediği zaman, hello görselleştirme aracı kendi bileşen adımları ve hello akışı dizisi hello sorgu hello dökümünü bir görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="b1248-114">When hello user wants toolook at intermediate query steps toounderstand hello data flow patterns inside a job, hello visualization tool provides a view of hello breakdown of hello query into its component steps and hello flow sequence.</span></span> <span data-ttu-id="b1248-115">Her sorgu adımını tıklatarak hello karşılık gelen bölüm gösterildiği gibi bölmesinde düzenleme sorguda gösterir.</span><span class="sxs-lookup"><span data-stu-id="b1248-115">Clicking on each query step will show hello corresponding section in a query editing pane as illustrated.</span></span> 

![Stream-Analytics-Troubleshoot-visualization-intermediate-Steps](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a><span data-ttu-id="b1248-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b1248-117">Next steps</span></span>
* [<span data-ttu-id="b1248-118">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="b1248-118">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="b1248-119">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="b1248-119">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="b1248-120">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="b1248-120">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="b1248-121">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="b1248-121">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="b1248-122">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="b1248-122">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

