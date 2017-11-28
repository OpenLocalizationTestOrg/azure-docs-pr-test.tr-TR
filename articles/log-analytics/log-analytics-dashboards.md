---
title: "aaaCreate Azure günlük analizi özel bir Panoda | Microsoft Docs"
description: "Bu kılavuz, günlük analizi panolar tüm kaydedilmiş günlük işlemlerinizin nasıl görselleştirebilirsiniz anlamanıza yardımcı olur, size tek bir mercek tooview ortamınızı."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: abb07f6c-b356-4f15-85f5-60e4415d0ba2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 73fcf131a91c743d473f37d5a40d52eaf78a7ba3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a><span data-ttu-id="407d4-103">Günlük analizi kullanmak için özel bir pano oluşturun</span><span class="sxs-lookup"><span data-stu-id="407d4-103">Create a custom dashboard for use in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="407d4-104">Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), sonra yeni panolar oluşturun veya varolan Pano düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="407d4-104">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you cannot create new dashboards or edit existing dashboards.</span></span> 

<span data-ttu-id="407d4-105">Bu kılavuz, günlük analizi panolar tüm kaydedilmiş günlük işlemlerinizin nasıl görselleştirebilirsiniz anlamanıza yardımcı olur, size tek bir mercek tooview ortamınızı.</span><span class="sxs-lookup"><span data-stu-id="407d4-105">This guide helps you understand how Log Analytics dashboards can visualize all of your saved log searches, giving you a single lens tooview your environment.</span></span>

![Örnek Pano](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

<span data-ttu-id="407d4-107">Merhaba OMS portalında oluşturduğunuz tüm hello özel panolar hello OMS mobil uygulama de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="407d4-107">All hello custom dashboards that you create in hello OMS portal are also available in hello OMS Mobile App.</span></span> <span data-ttu-id="407d4-108">Sayfaları hello uygulamalar hakkında daha fazla bilgi için aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="407d4-108">See hello following pages for more information about hello apps.</span></span>

* [<span data-ttu-id="407d4-109">Merhaba Microsoft Store mobil uygulamadan OMS</span><span class="sxs-lookup"><span data-stu-id="407d4-109">OMS mobile app from hello Microsoft Store</span></span>](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [<span data-ttu-id="407d4-110">Apple iTunes mobil uygulamadan OMS</span><span class="sxs-lookup"><span data-stu-id="407d4-110">OMS mobile app from Apple iTunes</span></span>](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![Mobil Pano](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a><span data-ttu-id="407d4-112">Benim Panom nasıl oluşturulur?</span><span class="sxs-lookup"><span data-stu-id="407d4-112">How do I create my dashboard?</span></span>
<span data-ttu-id="407d4-113">toobegin, Git toohello OMS genel bakış sayfası.</span><span class="sxs-lookup"><span data-stu-id="407d4-113">toobegin, go toohello OMS Overview page.</span></span> <span data-ttu-id="407d4-114">Merhaba görürsünüz **My Pano** hello sol bölme.</span><span class="sxs-lookup"><span data-stu-id="407d4-114">You'll see hello **My Dashboard** tile on hello left.</span></span> <span data-ttu-id="407d4-115">Toodrill aşağı panonuza tıklatın.</span><span class="sxs-lookup"><span data-stu-id="407d4-115">Click it toodrill down into your dashboard.</span></span>

![Genel Bakış](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a><span data-ttu-id="407d4-117">Bir kutucuk ekleme</span><span class="sxs-lookup"><span data-stu-id="407d4-117">Adding a tile</span></span>
<span data-ttu-id="407d4-118">Uygulamasındaki panolar, kutucuk tarafından kaydedilmiş günlük işlemlerinizin güç sağlar.</span><span class="sxs-lookup"><span data-stu-id="407d4-118">In dashboards, tiles are powered by your saved log searches.</span></span> <span data-ttu-id="407d4-119">OMS hemen başlayabilmesi için kaydedilmiş günlük aramalar, önceden yapılan çoğu ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="407d4-119">OMS comes with many pre-made saved log searches, so you can begin right away.</span></span> <span data-ttu-id="407d4-120">Kullanım hello aşağıdaki adımları bu anahattı nasıl toobegin.</span><span class="sxs-lookup"><span data-stu-id="407d4-120">Use hello following steps that outline how toobegin.</span></span>

<span data-ttu-id="407d4-121">Hello My Pano görünümü, tıklamanız yeterlidir **Özelleştir** tooenter modu özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="407d4-121">In hello My Dashboard view, simply click **Customize** tooenter customize mode.</span></span>

![Resimsel](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 <span data-ttu-id="407d4-123">Merhaba sağ tarafında hello sayfası açılır hello paneli tüm çalışma alanınızı 's kaydedilmiş günlük aramaları gösterir.</span><span class="sxs-lookup"><span data-stu-id="407d4-123">hello panel that opens on hello right side of hello page shows all of your workspace's saved log searches.</span></span> <span data-ttu-id="407d4-124">kaydedilmiş günlük bir kutucuk arama toovisualize kaydedilmiş bir aramayı üzerine gelin ve hello ardından **artı** simgesi.</span><span class="sxs-lookup"><span data-stu-id="407d4-124">toovisualize a saved log search as a tile,  hover over a saved search and then click hello **plus** symbol.</span></span>

![Kutucuk 1 Ekle](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

<span data-ttu-id="407d4-126">Merhaba tıkladığınızda **artı** simge, yeni bir kutucuk hello My Pano görünümü görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="407d4-126">When you click hello **plus** symbol, a new tile appears in hello My Dashboard view.</span></span>

![Kutucuk 2 Ekle](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a><span data-ttu-id="407d4-128">Bir kutucuk Düzenle</span><span class="sxs-lookup"><span data-stu-id="407d4-128">Edit a tile</span></span>
<span data-ttu-id="407d4-129">Hello My Pano görünümü, tıklamanız yeterlidir **Özelleştir** tooenter modu özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="407d4-129">In hello My Dashboard view, simply click  **Customize** tooenter customize mode.</span></span> <span data-ttu-id="407d4-130">Tooedit istediğiniz hello kutucuğa tıklayın.</span><span class="sxs-lookup"><span data-stu-id="407d4-130">Click hello tile you want tooedit.</span></span> <span data-ttu-id="407d4-131">Merhaba sağ panelde tooedit değiştirir ve Seçenekler seçim verir:</span><span class="sxs-lookup"><span data-stu-id="407d4-131">hello right panel changes tooedit, and gives a selection of options:</span></span>

![Döşeme Düzenle](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![Döşeme Düzenle](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a><span data-ttu-id="407d4-134">Döşeme görselleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="407d4-134">Tile visualizations</span></span>
<span data-ttu-id="407d4-135">Döşeme görselleştirmeleri toochoose üç tür vardır:</span><span class="sxs-lookup"><span data-stu-id="407d4-135">There are three kinds of tile visualizations toochoose from:</span></span>

| <span data-ttu-id="407d4-136">grafik türü</span><span class="sxs-lookup"><span data-stu-id="407d4-136">chart type</span></span> | <span data-ttu-id="407d4-137">ne yapar</span><span class="sxs-lookup"><span data-stu-id="407d4-137">what it does</span></span> |
| --- | --- |
| ![Çubuk grafiği](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |<span data-ttu-id="407d4-139">Günlük arama sonuçları bir alana göre veya toplar, kaydedilmiş günlük aramanın sonuçları bir zaman çizelgesi olarak bir çubuk grafik veya bağlı olarak bir alana göre sonuçlarının bir listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="407d4-139">Displays a timeline of your saved log search's results as a bar chart, or a list of results by a field depending on if your log search aggregates results by a field or not.</span></span> |
| ![Ölçüm](./media/log-analytics-dashboards/oms-dashboards-metric.png) |<span data-ttu-id="407d4-141">Toplam günlük arama sonucu isabet döşeme içinde bir sayı olarak görüntüler.</span><span class="sxs-lookup"><span data-stu-id="407d4-141">Displays your total log search result hits as a number in a tile.</span></span> <span data-ttu-id="407d4-142">Ölçüm döşeme tooset hello Eşiğe ulaşıldığında hello döşeme vurgular bir eşiği izin verin.</span><span class="sxs-lookup"><span data-stu-id="407d4-142">Metric tiles allow you tooset a threshold that will highlight hello tile when hello threshold is reached.</span></span> |
| ![Satır](./media/log-analytics-dashboards/oms-dashboards-line.png) |<span data-ttu-id="407d4-144">Bir zaman çizelgesi, kaydedilmiş günlük arama sonucu isabet değerleri içeren bir çizgi grafiği görüntüler.</span><span class="sxs-lookup"><span data-stu-id="407d4-144">Displays a timeline of your saved log search result hits with values as a line chart.</span></span> |

### <a name="threshold"></a><span data-ttu-id="407d4-145">Eşik</span><span class="sxs-lookup"><span data-stu-id="407d4-145">Threshold</span></span>
<span data-ttu-id="407d4-146">Bir eşik hello ölçüm görselleştirme kullanarak bir kutucuğu oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="407d4-146">You can create a threshold on a tile using hello Metric visualization.</span></span> <span data-ttu-id="407d4-147">Üzerinde toocreate hello kutucuğuna bir eşik değeri seçin.</span><span class="sxs-lookup"><span data-stu-id="407d4-147">Select on toocreate a threshold value on hello tile.</span></span> <span data-ttu-id="407d4-148">Merhaba değeri üzerinden veya hello seçilen eşiğin altında olduğunda toohighlight hello döşeme sonra olup olmadığını hello eşik değeri aşağıdaki kümesini seçin.</span><span class="sxs-lookup"><span data-stu-id="407d4-148">Choose whether toohighlight hello tile when hello value is over or under hello chosen threshold, then set hello threshold value below.</span></span>

## <a name="organizing-hello-dashboard"></a><span data-ttu-id="407d4-149">Merhaba Pano düzenleme</span><span class="sxs-lookup"><span data-stu-id="407d4-149">Organizing hello dashboard</span></span>
<span data-ttu-id="407d4-150">tooorganize panonuz, toohello My Pano görünümüne gidin ve tıklatın **Özelleştir** tooenter modu özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="407d4-150">tooorganize your dashboard, navigate toohello My Dashboard view and click **Customize** tooenter customize mode.</span></span> <span data-ttu-id="407d4-151">' I tıklatın ve istediğiniz toomove ve döşeme toobe istediğiniz toowhere taşıma hello bölmesi sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="407d4-151">Click and drag hello tile you want toomove, and move it toowhere you want your tile toobe.</span></span>

![Pano düzenleme](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a><span data-ttu-id="407d4-153">Bir kutucuğunu kaldırma</span><span class="sxs-lookup"><span data-stu-id="407d4-153">Remove a tile</span></span>
<span data-ttu-id="407d4-154">tooremove bir kutucuk toohello My Pano görünümüne gidin ve'ı tıklatın **Özelleştir** tooenter modu özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="407d4-154">tooremove a tile, navigate toohello My Dashboard view and click **Customize** tooenter customize mode.</span></span> <span data-ttu-id="407d4-155">Tooremove istediğiniz, ardından hello sağ paneldeki select hello döşeme **kaldırmak döşeme**.</span><span class="sxs-lookup"><span data-stu-id="407d4-155">Select hello tile you want tooremove, then on hello right panel select **Remove Tile**.</span></span>

![Bir kutucuğunu kaldırma](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a><span data-ttu-id="407d4-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="407d4-157">Next steps</span></span>
* <span data-ttu-id="407d4-158">Oluşturma [uyarıları](log-analytics-alerts.md) günlük analizi toogenerate bildirimleri ve tooremediate sorunları.</span><span class="sxs-lookup"><span data-stu-id="407d4-158">Create [alerts](log-analytics-alerts.md) in Log Analytics toogenerate notifications and tooremediate problems.</span></span>
