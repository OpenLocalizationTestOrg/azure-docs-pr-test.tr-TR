---
title: "Azure işlevleri izleme | Microsoft Docs"
description: "Azure işlevleri izleme öğrenin."
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
ms.openlocfilehash: b70214593b1417265387f42306a633bb0df2920e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-azure-functions"></a><span data-ttu-id="45fb7-104">Azure İşlevleri’ni izleme</span><span class="sxs-lookup"><span data-stu-id="45fb7-104">Monitoring Azure Functions</span></span>

## <a name="overview"></a><span data-ttu-id="45fb7-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="45fb7-105">Overview</span></span> 


<span data-ttu-id="45fb7-106">**İzleyici** sekmesi her işlevi işlevinin her yürütme gözden geçirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="45fb7-106">The **Monitor** tab for each function allows you to review each execution of a function.</span></span>

![Azure işlevleri İzleyici sekmesi](./media/functions-monitoring/monitor-tab.png) 

<span data-ttu-id="45fb7-108">Bir yürütme tıklatmak süresi, giriş verilerini, hataları ve ilişkili günlük dosyalarını gözden geçirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="45fb7-108">Clicking an execution allows you to review the duration, input data, errors, and associated log files.</span></span> <span data-ttu-id="45fb7-109">Yararlı hata ayıklama ve performans işlevlerinizi ayarlama budur.</span><span class="sxs-lookup"><span data-stu-id="45fb7-109">This is useful debugging and performance tuning your functions.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="45fb7-110">Kullanırken [barındırma planı tüketim](functions-overview.md#pricing) Azure işlevleri için **izleme** döşeme işlev uygulaması genel bakış dikey penceresinde herhangi bir veri görüntülenmez.</span><span class="sxs-lookup"><span data-stu-id="45fb7-110">When using the [Consumption hosting plan](functions-overview.md#pricing) for Azure Functions, the **Monitoring** tile in the Function App overview blade will not show any data.</span></span> <span data-ttu-id="45fb7-111">Platform dinamik olarak ölçeklendirir ve işlem örnekleri, bu ölçümleri tüketim plan üzerinde anlamlı olmayacak şekilde yönetir olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="45fb7-111">This is because the platform dynamically scales and manages compute instances for you, so these metrics are not meaningful on a Consumption plan.</span></span> <span data-ttu-id="45fb7-112">İşlevi uygulamalarınızı kullanımını izlemek için bunun yerine bu makaledeki yönergeleri kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="45fb7-112">To monitor the usage of your Function Apps, you should instead use the guidance in this article.</span></span>
> 
> <span data-ttu-id="45fb7-113">Aşağıdaki ekran görüntüsünde bir örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="45fb7-113">The following screen-shot shows an example:</span></span>
> 
> ![Ana kaynak dikey penceresinde izleme](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a><span data-ttu-id="45fb7-115">Gerçek zamanlı izleme</span><span class="sxs-lookup"><span data-stu-id="45fb7-115">Real-time monitoring</span></span>

<span data-ttu-id="45fb7-116">Gerçek zamanlı izleme kullanılabilir tıklayarak **canlı olay akışının** aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="45fb7-116">Real-time monitoring is available by clicking **live event stream** as shown below.</span></span> 

![Canlı olay akışı seçeneği İzleyici sekmesi](./media/functions-monitoring/monitor-tab-live-event-stream.png)

<span data-ttu-id="45fb7-118">Canlı olay akışının yeni bir tarayıcı sekmesinde aşağıda gösterildiği gibi grafik haline.</span><span class="sxs-lookup"><span data-stu-id="45fb7-118">The live event stream will be graphed in a new browser tab as shown below.</span></span> 

![Canlı olay akışı örnek](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> <span data-ttu-id="45fb7-120">Verilerinizi doldurulmalıdır başarısız olmasına neden olabilecek bilinen bir sorun yoktur.</span><span class="sxs-lookup"><span data-stu-id="45fb7-120">There is a known issue that may cause your data to fail to be populated.</span></span> <span data-ttu-id="45fb7-121">Bu karşılaşırsanız, canlı olay akışının içeren tarayıcı sekmesini kapatın ve ardından gerekebilir **canlı olay akışının** olay akışı verilerinizi düzgün bir şekilde doldurmak yeniden izin vermek için.</span><span class="sxs-lookup"><span data-stu-id="45fb7-121">If you experience this, you may need to close the browser tab containing the live event stream and then click **live event stream** again to allow it to properly populate your event stream data.</span></span> 

<span data-ttu-id="45fb7-122">Canlı olay akışının işlevinizi aşağıdaki istatistikleri grafik:</span><span class="sxs-lookup"><span data-stu-id="45fb7-122">The live event stream will graph the following statistics for your function:</span></span>

* <span data-ttu-id="45fb7-123">Saniye başına başlatılan yürütmeleri</span><span class="sxs-lookup"><span data-stu-id="45fb7-123">Executions started per second</span></span>
* <span data-ttu-id="45fb7-124">Saniyede tamamlanan yürütmeleri</span><span class="sxs-lookup"><span data-stu-id="45fb7-124">Executions completed per second</span></span>
* <span data-ttu-id="45fb7-125">Saniyede başarısız yürütmeleri</span><span class="sxs-lookup"><span data-stu-id="45fb7-125">Executions failed per second</span></span>
* <span data-ttu-id="45fb7-126">Milisaniye cinsinden ortalama yürütme süresi.</span><span class="sxs-lookup"><span data-stu-id="45fb7-126">Average execution time in milliseconds.</span></span>

<span data-ttu-id="45fb7-127">Bu istatistikler gerçek zamanlı ancak gerçek yürütme verileri Grafikleme yaklaşık 10 saniye gecikme süresi olabilir.</span><span class="sxs-lookup"><span data-stu-id="45fb7-127">These statistics are real-time but the actual graphing of the execution data may have around 10 seconds of latency.</span></span>






## <a name="monitoring-log-files-from-a-command-line"></a><span data-ttu-id="45fb7-128">Bir komut satırından izleme günlük dosyaları</span><span class="sxs-lookup"><span data-stu-id="45fb7-128">Monitoring log files from a command line</span></span>


<span data-ttu-id="45fb7-129">Yerel iş istasyonunda Azure komut satırı arabirimi (CLI) veya PowerShell kullanarak bir komut satırı oturumu için günlük dosyalarını akışını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45fb7-129">You can stream log files to a command line session on a local workstation using the Azure Command Line Interface (CLI) or PowerShell.</span></span>

### <a name="monitoring-function-app-log-files-with-the-azure-cli"></a><span data-ttu-id="45fb7-130">Azure CLI ile izleme işlevi uygulama günlük dosyaları</span><span class="sxs-lookup"><span data-stu-id="45fb7-130">Monitoring function app log files with the Azure CLI</span></span>

<span data-ttu-id="45fb7-131">Başlamak için [Azure CLI yükleme](../cli-install-nodejs.md)</span><span class="sxs-lookup"><span data-stu-id="45fb7-131">To get started, [install the Azure CLI](../cli-install-nodejs.md)</span></span>

<span data-ttu-id="45fb7-132">Aşağıdaki komutu ya da, ele diğer seçeneklerden birini kullanarak Azure hesabınıza günlüğüne [oturum açmak için Azure Azure CLI üzerinden](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="45fb7-132">Log into your Azure account using the following command, or any of the other options covered in, [Log in to Azure from the Azure CLI](../xplat-cli-connect.md).</span></span>

    azure login

<span data-ttu-id="45fb7-133">Azure CLI Hizmet Yönetimi (ASM) modunu etkinleştirmek için aşağıdaki komutu kullanın:.</span><span class="sxs-lookup"><span data-stu-id="45fb7-133">Use the following command to enable Azure CLI Service Management (ASM) mode:.</span></span>

    azure config mode asm

<span data-ttu-id="45fb7-134">Birden çok aboneliğiniz varsa, aboneliklerinizi listelemek ve geçerli Abonelik işlevi uygulamanızı içeren aboneliği ayarlamak için aşağıdaki komutları kullanın.</span><span class="sxs-lookup"><span data-stu-id="45fb7-134">If you have multiple subscriptions, use the following commands to list your subscriptions and set the current subscription to the subscription that contains your function app.</span></span>

    azure account list
    azure account set <subscriptionNameOrId>

<span data-ttu-id="45fb7-135">Aşağıdaki komutu, günlük dosyaları, komut satırı işlevi uygulamanızın akışı:</span><span class="sxs-lookup"><span data-stu-id="45fb7-135">The following command will stream the log files of your function app to the command line:</span></span>

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a><span data-ttu-id="45fb7-136">PowerShell ile izleme işlevi uygulama günlük dosyaları</span><span class="sxs-lookup"><span data-stu-id="45fb7-136">Monitoring function app log files with PowerShell</span></span>

<span data-ttu-id="45fb7-137">Başlamak için [Azure PowerShell'i yükleme ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="45fb7-137">To get started, [install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="45fb7-138">Azure hesabınızda, aşağıdaki komutu çalıştırarak ekleyin:</span><span class="sxs-lookup"><span data-stu-id="45fb7-138">Add your Azure account by running the following command:</span></span>

    PS C:\> Add-AzureAccount

<span data-ttu-id="45fb7-139">Birden çok aboneliğiniz varsa, bunları doğru abonelik şu anda seçili bağlı olup olmadığını görmek için aşağıdaki komutu kullanarak ada göre listeleyebilirsiniz `IsCurrent` özelliği:</span><span class="sxs-lookup"><span data-stu-id="45fb7-139">If you have multiple subscriptions, you can list them by name with the following command to see if the correct subscription is the currently selected based on `IsCurrent` property:</span></span>

    PS C:\> Get-AzureSubscription

<span data-ttu-id="45fb7-140">Etkin bir aboneliğiniz işlevi uygulamanızı içeren bir ayarlamak gerekiyorsa, aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="45fb7-140">If you need to set the active subscription to the one containing your function app, use the following command:</span></span>

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

<span data-ttu-id="45fb7-141">Aşağıdaki komut ile PowerShell oturumunuz için günlükleri akışı:</span><span class="sxs-lookup"><span data-stu-id="45fb7-141">Stream the logs to your PowerShell session with the following command:</span></span>

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

<span data-ttu-id="45fb7-142">Daha fazla bilgi için bkz [nasıl yapılır: akış günlükleri web uygulamaları için](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span><span class="sxs-lookup"><span data-stu-id="45fb7-142">For more information refer to [How to: Stream logs for web apps](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="45fb7-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="45fb7-143">Next steps</span></span>
<span data-ttu-id="45fb7-144">Daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="45fb7-144">For more information, see the following resources:</span></span>

* [<span data-ttu-id="45fb7-145">İşlevi test etme</span><span class="sxs-lookup"><span data-stu-id="45fb7-145">Testing a function</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="45fb7-146">Ölçek işlevi</span><span class="sxs-lookup"><span data-stu-id="45fb7-146">Scale a function</span></span>](functions-scale.md)

