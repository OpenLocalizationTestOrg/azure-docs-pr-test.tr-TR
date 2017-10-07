---
title: "aaaUse hello köşe yürütme görünümü Visual Studio için Data Lake araçları içinde | Microsoft Docs"
description: "Nasıl toouse hello köşe yürütme görünümü tooexam Data Lake Analytics işlerini öğrenin."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5366d852-e7d6-44cf-a88c-e9f52f15f7df
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/13/2016
ms.author: jgao
ms.openlocfilehash: fb54d2af8a32aa27a54ff50a73c1b4903677a21e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a><span data-ttu-id="e6317-103">Visual Studio için Data Lake araçları içinde Hello köşe yürütme görünümü kullanın</span><span class="sxs-lookup"><span data-stu-id="e6317-103">Use hello Vertex Execution View in Data Lake Tools for Visual Studio</span></span>
<span data-ttu-id="e6317-104">Nasıl toouse hello köşe yürütme görünümü tooexam Data Lake Analytics işlerini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="e6317-104">Learn how toouse hello Vertex Execution View tooexam Data Lake Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6317-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e6317-105">Prerequisites</span></span>

<span data-ttu-id="e6317-106">Visual Studio toodevelop U-SQL betiği için Data Lake araçları kullanarak, temel bilgiye gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6317-106">You need basic knowledge of using Data Lake Tools for Visual Studio toodevelop U-SQL script.</span></span>  <span data-ttu-id="e6317-107">Bkz: [öğretici: Visual Studio için Data Lake Araçları'nı kullanarak U-SQL betikleri geliştirme](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e6317-107">See [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>

## <a name="open-hello-vertex-execution-view"></a><span data-ttu-id="e6317-108">Merhaba köşe yürütme görünümü Aç</span><span class="sxs-lookup"><span data-stu-id="e6317-108">Open hello Vertex Execution View</span></span>
<span data-ttu-id="e6317-109">U-SQL işi Visual Studio için Data Lake araçları içinde açın.</span><span class="sxs-lookup"><span data-stu-id="e6317-109">Open a U-SQL job in Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="e6317-110">Tıklatın **köşe yürütme görünümü** sol alt köşede, hello.</span><span class="sxs-lookup"><span data-stu-id="e6317-110">Click **Vertex Execution View** in hello bottom left corner.</span></span> <span data-ttu-id="e6317-111">İstendiğinde tooload profilleri ilk olabilir ve ağ bağlantınızı bağlı olarak biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="e6317-111">You may be prompted tooload profiles first and it can take some time depending on your network connectivity.</span></span>

![Data Lake Analytics köşe yürütme görünümü araçları](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a><span data-ttu-id="e6317-113">Köşe yürütme görünümü anlama</span><span class="sxs-lookup"><span data-stu-id="e6317-113">Understand Vertex Execution View</span></span>
<span data-ttu-id="e6317-114">Merhaba köşe yürütme görünümü üç bölümden oluşur:</span><span class="sxs-lookup"><span data-stu-id="e6317-114">hello Vertex Execution View has three parts:</span></span>

![Data Lake Analytics köşe yürütme görünümü araçları](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

<span data-ttu-id="e6317-116">Merhaba **köşe Seçici** hello sol olanak tanır (10 veri top gibi okuma veya aşamasına göre seçin) özellikleri tarafından köşeleri seçin.</span><span class="sxs-lookup"><span data-stu-id="e6317-116">hello **Vertex selector** on hello left lets you select vertices by features (such as top 10 data read, or choose by stage).</span></span> <span data-ttu-id="e6317-117">Merhaba en yaygın olarak kullanılan filtreleri biri toosee hello **kritik yol köşelerinin**.</span><span class="sxs-lookup"><span data-stu-id="e6317-117">One of hello most commonly-used filters is toosee hello **vertices on critical path**.</span></span> <span data-ttu-id="e6317-118">Merhaba **kritik yol** hello uzun bir U-SQL işi köşe zincirine olduğu.</span><span class="sxs-lookup"><span data-stu-id="e6317-118">hello **Critical path** is hello longest chain of vertices of a U-SQL job.</span></span> <span data-ttu-id="e6317-119">Anlama hello kritik yol işleriniz hangi köşe hello uzun süren denetleyerek en iyi duruma getirme için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="e6317-119">Understanding hello critical path is useful for optimizing your jobs by checking which vertex takes hello longest time.</span></span>
  
![Data Lake Analytics köşe yürütme görünümü araçları](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

<span data-ttu-id="e6317-121">Merhaba üst orta bölmesinde gösterilir hello **tüm hello köşeleri durumunu çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="e6317-121">hello top center pane shows hello **running status of all hello vertices**.</span></span>
  
![Data Lake Analytics köşe yürütme görünümü araçları](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

<span data-ttu-id="e6317-123">Merhaba alt bölmeyi her köşe hakkında bilgileri gösterir:</span><span class="sxs-lookup"><span data-stu-id="e6317-123">hello bottom center pane shows information about each vertex:</span></span>
* <span data-ttu-id="e6317-124">İşlem adı: Merhaba köşe örneğinin hello adı.</span><span class="sxs-lookup"><span data-stu-id="e6317-124">Process Name: hello name of hello vertex instance.</span></span> <span data-ttu-id="e6317-125">StageName farklı bölümlerinin oluşan | VertexName | VertexRunInstance.</span><span class="sxs-lookup"><span data-stu-id="e6317-125">It is composed of different parts in StageName|VertexName|VertexRunInstance.</span></span> <span data-ttu-id="e6317-126">Örneğin, hello SV7_Split [62] .v1 köşe hello ikinci çalışan örneği için (.v1, dizini 0'dan başlayarak) anlamına gelir 62 köşe sayısının aşama SV7_Split.</span><span class="sxs-lookup"><span data-stu-id="e6317-126">For example, hello SV7_Split[62].v1 vertex stands for hello second running instance (.v1, index starting from 0) of Vertex number 62 in Stage SV7_Split.</span></span>
* <span data-ttu-id="e6317-127">Toplam veri okuma/yazılan: hello verileri bu köşe tarafından okunur/yazılır.</span><span class="sxs-lookup"><span data-stu-id="e6317-127">Total Data Read/Written: hello data was read/written by this vertex.</span></span>
* <span data-ttu-id="e6317-128">Durumu/Çıkış durumu: hello köşe sonlandığında hello son durum.</span><span class="sxs-lookup"><span data-stu-id="e6317-128">State/Exit Status: hello final status when hello vertex is ended.</span></span>
* <span data-ttu-id="e6317-129">Çıkış kodu/hatası türü: hello köşe başarısız olduğunda hello hatası.</span><span class="sxs-lookup"><span data-stu-id="e6317-129">Exit Code/Failure Type: hello error when hello vertex failed.</span></span>
* <span data-ttu-id="e6317-130">Oluşturma nedeni: Neden hello köşe oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="e6317-130">Creation Reason: Why hello vertex was created.</span></span>
* <span data-ttu-id="e6317-131">Kaynak gecikme/işlem gecikmesi/PN sıra gecikme süresi: hello hello köşe toowait kaynakları, tooprocess veri ve hello sırasındaki toostay için geçen süre.</span><span class="sxs-lookup"><span data-stu-id="e6317-131">Resource Latency/Process Latency/PN Queue Latency: hello time taken for hello vertex toowait for resources, tooprocess data, and toostay in hello queue.</span></span>
* <span data-ttu-id="e6317-132">İşlem/Creator GUID: Merhaba geçerli çalışan köşe veya oluşturana GUID.</span><span class="sxs-lookup"><span data-stu-id="e6317-132">Process/Creator GUID: GUID for hello current running vertex or its creator.</span></span>
* <span data-ttu-id="e6317-133">Sürüm: hello n. köşe çalıştıran hello örneği (Merhaba sistem zamanlayın bir köşesinin yeni örnekleri birçok nedeni, örneğin yük devretme, işlem için artıklık, vb.)</span><span class="sxs-lookup"><span data-stu-id="e6317-133">Version: hello N-th instance of hello running vertex (hello system might schedule new instances of a vertex for many reasons, for example failover, compute redundancy, etc.)</span></span>
* <span data-ttu-id="e6317-134">Sürümü zaman oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="e6317-134">Version Created Time.</span></span>
* <span data-ttu-id="e6317-135">İşlem oluşturma başlangıç süre/işlem sıraya alınan süre/işlem başlangıç saati/işlem tam zamanı: hello köşe işlemi oluşturma; başladığında Merhaba köşe işlem tooqueue başladığında; ne zaman belirli köşe işlemi başlar hello; Merhaba belirli köşe tamamlandığında.</span><span class="sxs-lookup"><span data-stu-id="e6317-135">Process Create Start Time/Process Queued Time/Process Start Time/Process Complete Time: when hello vertex process starts creation; when hello vertex process starts tooqueue; when hello certain vertex process starts; when hello certain vertex is completed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6317-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e6317-136">Next steps</span></span>
* <span data-ttu-id="e6317-137">toolog tanılama bilgilerini görmek [Azure Data Lake Analytics için tanılama günlükleri erişme](data-lake-analytics-diagnostic-logs.md)</span><span class="sxs-lookup"><span data-stu-id="e6317-137">toolog diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span></span>
* <span data-ttu-id="e6317-138">toosee daha karmaşık bir sorgu görmek [Web sitesi günlüklerini çözümleme Azure Data Lake Analytics'i kullanarak](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="e6317-138">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="e6317-139">tooview iş ayrıntılarını görmek [kullanım iş tarayıcı ve Azure Data lake Analytics işleri için iş görünümünde](data-lake-analytics-data-lake-tools-view-jobs.md)</span><span class="sxs-lookup"><span data-stu-id="e6317-139">tooview job details, see [Use Job Browser and Job View for Azure Data lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md)</span></span>
