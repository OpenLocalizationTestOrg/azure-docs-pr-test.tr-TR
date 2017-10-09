---
title: "aaaStreaming günlükleri ve konsol"
description: "Akış günlükleri ve konsoluna genel bakış"
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: 3e50a287-781b-4c6a-8c53-eec261889d7a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/12/2016
ms.author: byvinyal
ms.openlocfilehash: bb4b8ce5358da12041e164dfff8f43790dd67924
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-logs-and-hello-console"></a><span data-ttu-id="95d67-103">Akış günlükleri ve hello konsol</span><span class="sxs-lookup"><span data-stu-id="95d67-103">Streaming Logs and hello Console</span></span>
## <a name="streaming-logs"></a><span data-ttu-id="95d67-104">Akış günlükleri</span><span class="sxs-lookup"><span data-stu-id="95d67-104">Streaming Logs</span></span>
<span data-ttu-id="95d67-105">Merhaba **Azure portal** izleme olayları görüntülemenize olanak sağlayan bir tümleşik akış Günlük Görüntüleyici sağlar, **uygulama hizmeti** gerçek zamanlı uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="95d67-105">hello **Azure portal** provides an integrated streaming log viewer that lets you view tracing events from your **App Service** apps in real time.</span></span>  

<span data-ttu-id="95d67-106">Bu özelliği ayarlama birkaç basit adımı gerektirir:</span><span class="sxs-lookup"><span data-stu-id="95d67-106">Setting up this feature requires a few simple steps:</span></span>

* <span data-ttu-id="95d67-107">Kodunuzda izlemeleri yazma</span><span class="sxs-lookup"><span data-stu-id="95d67-107">Write traces in your code</span></span>
* <span data-ttu-id="95d67-108">Uygulamayı etkinleştir **tanılama günlüklerini** uygulamanız için</span><span class="sxs-lookup"><span data-stu-id="95d67-108">Enable Application **Diagnostic Logs** for your app</span></span>
* <span data-ttu-id="95d67-109">Görünüm hello hello yerleşik akıştan **akış günlükleri** hello kullanıcı Arabiriminde **Azure portal**.</span><span class="sxs-lookup"><span data-stu-id="95d67-109">View hello stream from hello built-in **Streaming Logs** UI in hello **Azure portal**.</span></span>

### <a name="how-toowrite-traces-in-your-code"></a><span data-ttu-id="95d67-110">Kodunuzda toowrite nasıl izlediğini</span><span class="sxs-lookup"><span data-stu-id="95d67-110">How toowrite traces in your code</span></span>
<span data-ttu-id="95d67-111">Kodunuzda izlemeleri yazarken kolaydır.</span><span class="sxs-lookup"><span data-stu-id="95d67-111">Writing traces in your code is easy.</span></span>  <span data-ttu-id="95d67-112">C# kod aşağıdaki hello yazma olarak kadar kolaydır:</span><span class="sxs-lookup"><span data-stu-id="95d67-112">In C# it's as easy as writing hello following code:</span></span>

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

<span data-ttu-id="95d67-113">Merhaba izleme sınıfı hello System.Diagnostics ad alanında yaşar.</span><span class="sxs-lookup"><span data-stu-id="95d67-113">hello Trace class lives in hello System.Diagnostics namespace.</span></span>

<span data-ttu-id="95d67-114">Bir node.js uygulamasında bu kod yazabilirsiniz tooachieve hello aynı sonucu:</span><span class="sxs-lookup"><span data-stu-id="95d67-114">In a node.js app you can write this code tooachieve hello same result:</span></span>

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-tooenable-and-view-hello-streaming-logs"></a><span data-ttu-id="95d67-115">Akış günlükleri nasıl tooenable ve görünüm hello</span><span class="sxs-lookup"><span data-stu-id="95d67-115">How tooenable and view hello streaming logs</span></span>
<span data-ttu-id="95d67-116">![][BrowseSitesScreenshot]Tanılama bir uygulama başına temelinde etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="95d67-116">![][BrowseSitesScreenshot] Diagnostics are enabled on a per app basis.</span></span> <span data-ttu-id="95d67-117">Bu özelliği tooenable istediğiniz toohello site göz atarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="95d67-117">Start by browsing toohello site you would like tooenable this feature on.</span></span>  

<span data-ttu-id="95d67-118">![][DiagnosticsLogs]Ayarlar menüsünden toohello kaydırarak **izleme** bölümünde ve tıklayın **(1) tanılama günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="95d67-118">![][DiagnosticsLogs] From settings menu, scroll down toohello **Monitoring** section and click on **(1) Diagnostic Logs**.</span></span> <span data-ttu-id="95d67-119">Ardından **(2) etkinleştir** **uygulama günlüğü (dosya sistemi)** veya **uygulama günlüğü (blob)** hello **düzeyi** seçeneği hello değiştirmenize olanak sağlar izlemeler toocapture önem derecesi.</span><span class="sxs-lookup"><span data-stu-id="95d67-119">Then **(2) enable** **Application Logging (Filesystem)** or **Application Logging (blob)** hello **Level** option lets you change hello severity level of traces toocapture.</span></span> <span data-ttu-id="95d67-120">Yalnızca tooget hello özelliğiyle tanıdık çalışıyorsanız, hello çok düzeyi**ayrıntılı** tooensure tüm izleme deyimleri toplanır.</span><span class="sxs-lookup"><span data-stu-id="95d67-120">If you're just trying tooget familiar with hello feature, set hello level too**Verbose** tooensure all of your trace statements are collected.</span></span>

<span data-ttu-id="95d67-121">' I tıklatın **KAYDETMEK** hello hello dikey ve en üstündeki hazır tooview günlükleri demektir.</span><span class="sxs-lookup"><span data-stu-id="95d67-121">Click **SAVE** at hello top of hello blade and you're ready tooview logs.</span></span>

> [!NOTE]
> <span data-ttu-id="95d67-122">Merhaba yüksek hello **önem düzeyi** daha fazla kaynaklardır tüketilen toolog ve daha fazla izlemeleri üretilmektedir hello hello.</span><span class="sxs-lookup"><span data-stu-id="95d67-122">hello higher hello **severity level** hello more resources are consumed toolog and hello more traces are produced.</span></span> <span data-ttu-id="95d67-123">Emin olun **önem düzeyi** üretim veya yüksek trafiğe sahip site için yapılandırılmış toohello doğru ayrıntı değil.</span><span class="sxs-lookup"><span data-stu-id="95d67-123">Make sure **severity level** is configured toohello correct verbosity for a production or high traffic site.</span></span> 
> 
> 

<span data-ttu-id="95d67-124">![][StreamingLogsScreenshot]tooview hello **akış günlükleri** gelen hello Azure portalı içinde tıklayın **(1) günlük akışı** hello içinde de **izleme** hello ayarları menüsünün bölümünde.</span><span class="sxs-lookup"><span data-stu-id="95d67-124">![][StreamingLogsScreenshot] tooview hello **streaming logs** from within hello Azure portal, click on **(1) Log Stream** also in hello **Monitoring** section of hello settings menu.</span></span> <span data-ttu-id="95d67-125">Uygulamanızı etkin olarak izleme deyimleri yazma sonra hello görmeniz gerekir **(2) akış günlükleri UI** yakın gerçek zamanlı.</span><span class="sxs-lookup"><span data-stu-id="95d67-125">If your app is actively writing trace statements, then you should see them in hello **(2) streaming logs UI** in near real time.</span></span>

## <a name="console"></a><span data-ttu-id="95d67-126">Konsol</span><span class="sxs-lookup"><span data-stu-id="95d67-126">Console</span></span>
<span data-ttu-id="95d67-127">Merhaba **Azure portal** konsol erişimi tooyour uygulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="95d67-127">hello **Azure portal** provides console access tooyour app.</span></span> <span data-ttu-id="95d67-128">Uygulamanızın dosya sistemini inceleyin ve powershell/cmd komut dosyalarını çalıştır.</span><span class="sxs-lookup"><span data-stu-id="95d67-128">You can explore your app's file system and run powershell/cmd scripts.</span></span> <span data-ttu-id="95d67-129">Konsol komutları yürütülürken zaman, çalışan uygulama kodu olarak aynı izinleri ayarlama hello tarafından bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="95d67-129">You are bound by hello same permissions set as your running app code when executing console commands.</span></span> <span data-ttu-id="95d67-130">Erişim tooprotected dizinleri ve yükseltilmiş izinleri gerektiren çalışan komutlar engellenir.</span><span class="sxs-lookup"><span data-stu-id="95d67-130">Access tooprotected directories or running scripts that require elevated permissions is blocked.</span></span>  

<span data-ttu-id="95d67-131">![][ConsoleScreenshot]Çok ayarları menüsünden aşağı kaydırın**geliştirme araçları** bölümünde ve tıklayın **(1) konsol** ve hello **(2) konsol** toohello sağ kullanıcı arabirimini açar.</span><span class="sxs-lookup"><span data-stu-id="95d67-131">![][ConsoleScreenshot] From settings menu, scroll down too**Development Tools** section and click on **(1) Console** and hello **(2) console** UI opens toohello right.</span></span>

<span data-ttu-id="95d67-132">tooget ile Merhaba tanıdık **konsol**, temel komutları gibi deneyin:</span><span class="sxs-lookup"><span data-stu-id="95d67-132">tooget familiar with hello **console**, try basic commands like:</span></span>

`````````````````````````
dir
`````````````````````````

`````````````````````````
cd
`````````````````````````

<!-- Images. -->
[DiagnosticsLogs]: ./media/web-sites-streaming-logs-and-console/diagnostic-logs.png
[BrowseSitesScreenshot]: ./media/web-sites-streaming-logs-and-console/browse-sites.png
[StreamingLogsScreenshot]: ./media/web-sites-streaming-logs-and-console/streaming-logs.png
[ConsoleScreenshot]: ./media/web-sites-streaming-logs-and-console/console.png
