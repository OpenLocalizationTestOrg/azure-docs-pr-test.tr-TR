---
title: "Azure işlevleri aaaMonitoring | Microsoft Docs"
description: "Bilgi nasıl toomonitor Azure işlevleri."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "azure işlevleri, işlevler, olay işleme, web kancaları, dinamik işlem, sunucusuz mimari"
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/03/2016
ms.author: wesmc
ms.openlocfilehash: 254348d1cefce925654bd9532715b6def571e0ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-functions"></a><span data-ttu-id="79ba7-104">Azure İşlevleri’ni izleme</span><span class="sxs-lookup"><span data-stu-id="79ba7-104">Monitoring Azure Functions</span></span>

## <a name="overview"></a><span data-ttu-id="79ba7-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="79ba7-105">Overview</span></span> 


<span data-ttu-id="79ba7-106">Merhaba **İzleyici** her işlev tooreview verir sekmesi her yürütülmesini bir işlev.</span><span class="sxs-lookup"><span data-stu-id="79ba7-106">hello **Monitor** tab for each function allows you tooreview each execution of a function.</span></span>

![Azure işlevleri İzleyici sekmesi](./media/functions-monitoring/monitor-tab.png) 

<span data-ttu-id="79ba7-108">Bir yürütme tıklatmak, tooreview hello süresi, giriş verilerini, hataları ve ilişkili günlük dosyaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="79ba7-108">Clicking an execution allows you tooreview hello duration, input data, errors, and associated log files.</span></span> <span data-ttu-id="79ba7-109">Yararlı hata ayıklama ve performans işlevlerinizi ayarlama budur.</span><span class="sxs-lookup"><span data-stu-id="79ba7-109">This is useful debugging and performance tuning your functions.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="79ba7-110">Merhaba kullanırken [barındırma planı tüketim](functions-overview.md#pricing) Azure işlevleri için hello **izleme** döşeme hello işlev uygulaması genel bakış dikey penceresinde herhangi bir veri görüntülenmez.</span><span class="sxs-lookup"><span data-stu-id="79ba7-110">When using hello [Consumption hosting plan](functions-overview.md#pricing) for Azure Functions, hello **Monitoring** tile in hello Function App overview blade will not show any data.</span></span> <span data-ttu-id="79ba7-111">Merhaba platform dinamik olarak ölçeklendirir ve işlem örnekleri, bu ölçümleri tüketim plan üzerinde anlamlı olmayacak şekilde yönetir olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="79ba7-111">This is because hello platform dynamically scales and manages compute instances for you, so these metrics are not meaningful on a Consumption plan.</span></span> <span data-ttu-id="79ba7-112">İşlevi uygulamalarınızın toomonitor hello kullanımı, bu makaledeki hello yönergeler yerine kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="79ba7-112">toomonitor hello usage of your Function Apps, you should instead use hello guidance in this article.</span></span>
> 
> <span data-ttu-id="79ba7-113">Aşağıdaki ekran görüntüsünde hello bir örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="79ba7-113">hello following screen-shot shows an example:</span></span>
> 
> ![Merhaba ana kaynak dikey penceresinde izleme](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a><span data-ttu-id="79ba7-115">Gerçek zamanlı izleme</span><span class="sxs-lookup"><span data-stu-id="79ba7-115">Real-time monitoring</span></span>

<span data-ttu-id="79ba7-116">Gerçek zamanlı izleme kullanılabilir tıklayarak **canlı olay akışının** aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="79ba7-116">Real-time monitoring is available by clicking **live event stream** as shown below.</span></span> 

![Canlı olay akışı seçeneği hello İzleyici sekmesi](./media/functions-monitoring/monitor-tab-live-event-stream.png)

<span data-ttu-id="79ba7-118">Merhaba canlı olay akışının yeni bir tarayıcı sekmesinde aşağıda gösterildiği gibi grafik haline.</span><span class="sxs-lookup"><span data-stu-id="79ba7-118">hello live event stream will be graphed in a new browser tab as shown below.</span></span> 

![Canlı olay akışı örnek](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> <span data-ttu-id="79ba7-120">Doldurulmuş, veri toofail toobe neden olabilecek bilinen bir sorun yoktur.</span><span class="sxs-lookup"><span data-stu-id="79ba7-120">There is a known issue that may cause your data toofail toobe populated.</span></span> <span data-ttu-id="79ba7-121">Bu karşılaşırsanız, tooclose hello tarayıcı sekmesinde içeren hello canlı olay akışının ve ardından gerekebilir **canlı olay akışının** yeniden tooallow, tooproperly doldurmak olay akışı veri.</span><span class="sxs-lookup"><span data-stu-id="79ba7-121">If you experience this, you may need tooclose hello browser tab containing hello live event stream and then click **live event stream** again tooallow it tooproperly populate your event stream data.</span></span> 

<span data-ttu-id="79ba7-122">Merhaba canlı olay akışının işlevinizi istatistiklerini aşağıdaki hello grafik:</span><span class="sxs-lookup"><span data-stu-id="79ba7-122">hello live event stream will graph hello following statistics for your function:</span></span>

* <span data-ttu-id="79ba7-123">Saniye başına başlatılan yürütmeleri</span><span class="sxs-lookup"><span data-stu-id="79ba7-123">Executions started per second</span></span>
* <span data-ttu-id="79ba7-124">Saniyede tamamlanan yürütmeleri</span><span class="sxs-lookup"><span data-stu-id="79ba7-124">Executions completed per second</span></span>
* <span data-ttu-id="79ba7-125">Saniyede başarısız yürütmeleri</span><span class="sxs-lookup"><span data-stu-id="79ba7-125">Executions failed per second</span></span>
* <span data-ttu-id="79ba7-126">Milisaniye cinsinden ortalama yürütme süresi.</span><span class="sxs-lookup"><span data-stu-id="79ba7-126">Average execution time in milliseconds.</span></span>

<span data-ttu-id="79ba7-127">Bu istatistikler gerçek zamanlı ancak hello hello yürütme verileri Grafikleme gerçek yaklaşık 10 saniye gecikme süresi olabilir.</span><span class="sxs-lookup"><span data-stu-id="79ba7-127">These statistics are real-time but hello actual graphing of hello execution data may have around 10 seconds of latency.</span></span>






## <a name="monitoring-log-files-from-a-command-line"></a><span data-ttu-id="79ba7-128">Bir komut satırından izleme günlük dosyaları</span><span class="sxs-lookup"><span data-stu-id="79ba7-128">Monitoring log files from a command line</span></span>


<span data-ttu-id="79ba7-129">Günlük dosyaları tooa komut satırı oturumu hello Azure komut satırı arabirimi (CLI) veya PowerShell kullanarak bir yerel iş istasyonunda akışını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79ba7-129">You can stream log files tooa command line session on a local workstation using hello Azure Command Line Interface (CLI) or PowerShell.</span></span>

### <a name="monitoring-function-app-log-files-with-hello-azure-cli"></a><span data-ttu-id="79ba7-130">İşlev uygulama günlük dosyalarının hello Azure CLI ile izleme</span><span class="sxs-lookup"><span data-stu-id="79ba7-130">Monitoring function app log files with hello Azure CLI</span></span>

<span data-ttu-id="79ba7-131">başlatıldı, tooget [hello Azure CLI yükleme](../cli-install-nodejs.md)</span><span class="sxs-lookup"><span data-stu-id="79ba7-131">tooget started, [install hello Azure CLI](../cli-install-nodejs.md)</span></span>

<span data-ttu-id="79ba7-132">Merhaba aşağıdakileri kullanarak Azure hesabınıza günlüğüne komutu ya da hiçbirini Merhaba, ele diğer seçenekleri [tooAzure hello Azure CLI gelen oturum](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="79ba7-132">Log into your Azure account using hello following command, or any of hello other options covered in, [Log in tooAzure from hello Azure CLI](../xplat-cli-connect.md).</span></span>

    azure login

<span data-ttu-id="79ba7-133">Kullanım hello şu komutu tooenable Azure CLI Hizmet Yönetimi (ASM) mod:.</span><span class="sxs-lookup"><span data-stu-id="79ba7-133">Use hello following command tooenable Azure CLI Service Management (ASM) mode:.</span></span>

    azure config mode asm

<span data-ttu-id="79ba7-134">Birden çok aboneliğiniz varsa, aşağıdaki komutları toolist hello aboneliklerinizi ve işlev uygulamanızı içeren kümesi hello geçerli abonelik toohello abonelik kullanın.</span><span class="sxs-lookup"><span data-stu-id="79ba7-134">If you have multiple subscriptions, use hello following commands toolist your subscriptions and set hello current subscription toohello subscription that contains your function app.</span></span>

    azure account list
    azure account set <subscriptionNameOrId>

<span data-ttu-id="79ba7-135">Merhaba bir işlev uygulaması toohello komut satırında hello günlük dosyalarının en aşağıdaki komutu akışı:</span><span class="sxs-lookup"><span data-stu-id="79ba7-135">hello following command will stream hello log files of your function app toohello command line:</span></span>

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a><span data-ttu-id="79ba7-136">PowerShell ile izleme işlevi uygulama günlük dosyaları</span><span class="sxs-lookup"><span data-stu-id="79ba7-136">Monitoring function app log files with PowerShell</span></span>

<span data-ttu-id="79ba7-137">başlatıldı, tooget [Azure PowerShell'i yükleme ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="79ba7-137">tooget started, [install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="79ba7-138">Azure hesabınızda hello aşağıdaki komutu çalıştırarak ekleyin:</span><span class="sxs-lookup"><span data-stu-id="79ba7-138">Add your Azure account by running hello following command:</span></span>

    PS C:\> Add-AzureAccount

<span data-ttu-id="79ba7-139">Birden çok aboneliğiniz varsa, bunları adıyla hello abonelik hello şu anda seçili olan doğru temel komutu toosee aşağıdaki hello ile listeleyebilirsiniz `IsCurrent` özelliği:</span><span class="sxs-lookup"><span data-stu-id="79ba7-139">If you have multiple subscriptions, you can list them by name with hello following command toosee if hello correct subscription is hello currently selected based on `IsCurrent` property:</span></span>

    PS C:\> Get-AzureSubscription

<span data-ttu-id="79ba7-140">Tooset hello etkin bir aboneliğiniz toohello bir işlev uygulaması içeren gerekiyorsa, komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="79ba7-140">If you need tooset hello active subscription toohello one containing your function app, use hello following command:</span></span>

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

<span data-ttu-id="79ba7-141">Akış hello günlükleri tooyour PowerShell oturumu komutu aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="79ba7-141">Stream hello logs tooyour PowerShell session with hello following command:</span></span>

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

<span data-ttu-id="79ba7-142">Daha fazla bilgi için çok başvurun[nasıl yapılır: akış günlükleri web uygulamaları için](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span><span class="sxs-lookup"><span data-stu-id="79ba7-142">For more information refer too[How to: Stream logs for web apps](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="79ba7-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="79ba7-143">Next steps</span></span>
<span data-ttu-id="79ba7-144">Daha fazla bilgi için kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="79ba7-144">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="79ba7-145">İşlevi test etme</span><span class="sxs-lookup"><span data-stu-id="79ba7-145">Testing a function</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="79ba7-146">Ölçek işlevi</span><span class="sxs-lookup"><span data-stu-id="79ba7-146">Scale a function</span></span>](functions-scale.md)

