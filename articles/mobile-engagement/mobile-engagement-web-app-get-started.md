---
title: "aaaGet Web uygulamaları için Azure Mobile Engagement ile başlatılan | Microsoft Docs"
description: "Bilgi nasıl Web uygulamaları için analizler ve anında iletme bildirimleri ile Azure Mobile Engagement toouse."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04afe53a-4caf-4c80-bd75-20cc630cd75c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: hero-article
ms.date: 06/01/2016
ms.author: piyushjo
ms.openlocfilehash: a84c96cac13bf3b85e72aef55da5c91693e1766c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-web-apps"></a><span data-ttu-id="1198a-103">Web Apps için Azure Mobile Engagement kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="1198a-103">Get started with Azure Mobile Engagement for Web Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="1198a-104">Bu konu, nasıl gösterir toouse Azure Mobile Engagement toounderstand Web uygulama kullanımınızı.</span><span class="sxs-lookup"><span data-stu-id="1198a-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your Web App usage.</span></span>

> [!NOTE]
> <span data-ttu-id="1198a-105">Hello Azure Mobile Engagement hizmet Mart 2018 kullanımdan kaldırılır ve şu anda yalnızca kullanılabilir tooexisting müşterileri içindir.</span><span class="sxs-lookup"><span data-stu-id="1198a-105">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="1198a-106">Daha fazla bilgi için bkz. [Mobile Engagement nedir?](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="1198a-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="1198a-107">Bu öğretici hello aşağıdakileri gerektirir:</span><span class="sxs-lookup"><span data-stu-id="1198a-107">This tutorial requires hello following:</span></span>

* <span data-ttu-id="1198a-108">Visual Studio 2015 veya tercih ettiğiniz başka bir düzenleyici</span><span class="sxs-lookup"><span data-stu-id="1198a-108">Visual Studio 2015 or any other editor of your choice</span></span>
* [<span data-ttu-id="1198a-109">Web SDK</span><span class="sxs-lookup"><span data-stu-id="1198a-109">Web SDK</span></span>](http://aka.ms/P7b453)

<span data-ttu-id="1198a-110">Bu Web SDK Önizleme aşamasındadır ve yalnızca Analytics hello şu anda destekler ve gönderen tarayıcı veya uygulama anında iletme bildirimleri henüz desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="1198a-110">This Web SDK is in Preview and only supports Analytics at hello moment and doesn't support sending browser or in-app push notifications yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="1198a-111">toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1198a-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="1198a-112">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1198a-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1198a-113">Ayrıntılar için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span><span class="sxs-lookup"><span data-stu-id="1198a-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span></span>
> 
> 

## <a name="setup-mobile-engagement-for-your-web-app"></a><span data-ttu-id="1198a-114">Web uygulamanız için Mobile Engagement ayarlama</span><span class="sxs-lookup"><span data-stu-id="1198a-114">Setup Mobile Engagement for your Web app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="1198a-115"><a id="connecting-app"></a>Uygulamanızın toohello Mobile Engagement arka ucuna bağlanmak</span><span class="sxs-lookup"><span data-stu-id="1198a-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="1198a-116">Bu öğretici "Merhaba gerekli en küçük kümesi toocollect verileri olan bir temel tümleştirme" gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="1198a-116">This tutorial presents a "basic integration," which is hello minimal set required toocollect data.</span></span>

<span data-ttu-id="1198a-117">Visual Studio dışında da oluşturulan herhangi bir web uygulaması ile Merhaba adımları takip edebilirsiniz ancak Visual Studio toodemonstrate hello Tümleştirmesi ile temel bir web uygulaması oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="1198a-117">We will create a basic web app with Visual Studio toodemonstrate hello integration though you can follow hello steps with any web application created outside of Visual Studio also.</span></span> 

### <a name="create-a-new-web-app"></a><span data-ttu-id="1198a-118">Yeni bir Web Uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="1198a-118">Create a new Web App</span></span>
<span data-ttu-id="1198a-119">Visual Studio'nun önceki sürümleri başlangıç adımları benzerdir olsa hello aşağıdaki adımlarda Visual Studio 2015 hello kullanımını varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1198a-119">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="1198a-120">Visual Studio'yu başlatın ve hello **giriş** ekran, select **yeni proje**.</span><span class="sxs-lookup"><span data-stu-id="1198a-120">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="1198a-121">Merhaba açılır pencerede seçin **Web** -> **ASP.Net Web uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="1198a-121">In hello pop-up, select **Web** -> **ASP.Net Web Application**.</span></span> <span data-ttu-id="1198a-122">Merhaba doldurup **adı**, **konumu** ve **çözüm adı**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="1198a-122">Fill in hello app **Name**, **Location** and  **Solution name**, and then click **OK**.</span></span>
3. <span data-ttu-id="1198a-123">Merhaba, **bir şablon seçin** açılan, select **boş** altında **ASP.Net 4.5 şablonları** tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="1198a-123">In hello **Select a template** popup, select **Empty** under **ASP.Net 4.5 Templates** and click **OK**.</span></span> 

<span data-ttu-id="1198a-124">İçine biz hello Azure Mobile Engagement Web SDK tümleştirecek yeni boş bir Web uygulaması proje oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="1198a-124">You have now created a new blank Web App project into which we will integrate hello Azure Mobile Engagement Web SDK.</span></span>

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="1198a-125">Uygulamanızın tooMobile Engagement arka ucuna bağlanmak</span><span class="sxs-lookup"><span data-stu-id="1198a-125">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="1198a-126">Adlı yeni bir klasör oluşturun **javascript** çözümünüzdeki ve hello Web SDK JS dosyası ekleme **azure engagement.js** içine.</span><span class="sxs-lookup"><span data-stu-id="1198a-126">Create a new folder called **javascript** in your solution and add hello Web SDK JS file **azure-engagement.js** into it.</span></span> 
2. <span data-ttu-id="1198a-127">Adlı yeni bir dosya ekleme **main.js** bu javascript klasörde koddan hello sahip.</span><span class="sxs-lookup"><span data-stu-id="1198a-127">Add a new file called **main.js** in this javascript folder with hello following code.</span></span> <span data-ttu-id="1198a-128">Tooupdate hello bağlantı dizesi emin olun.</span><span class="sxs-lookup"><span data-stu-id="1198a-128">Make sure tooupdate hello connection string.</span></span> <span data-ttu-id="1198a-129">Bu `azureEngagement` nesne kullanılan tooaccess Web SDK yöntemleri olacaktır.</span><span class="sxs-lookup"><span data-stu-id="1198a-129">This `azureEngagement` object will be used tooaccess Web SDK methods.</span></span> 
   
        var azureEngagement = {
            debug: true,
            connectionString: 'xxxxx'
        };
   
    ![Js dosyaları ile Visual Studio][1]

## <a name="enable-real-time-monitoring"></a><span data-ttu-id="1198a-131">Gerçek zamanlı izlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="1198a-131">Enable real-time monitoring</span></span>
<span data-ttu-id="1198a-132">Verileri gönderme ve hello kullanıcıların etkin olduğundan emin olmak sipariş toostart içinde en az bir etkinlik toohello Mobile Engagement arka göndermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1198a-132">In order toostart sending data and ensuring that hello users are active, you must send at least one Activity toohello Mobile Engagement backend.</span></span> <span data-ttu-id="1198a-133">Bir web uygulaması Merhaba içeriğine bir etkinlikte bir web sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="1198a-133">An activity in hello context of a web app is a web page.</span></span> 

1. <span data-ttu-id="1198a-134">Adlı yeni bir sayfa oluşturma **home.html** çözüm ve hello başlangıç olarak sayfasında web uygulamanız için ayarlama.</span><span class="sxs-lookup"><span data-stu-id="1198a-134">Create a new page called **home.html** in your solution and set it as hello starting page for your web app.</span></span> 
2. <span data-ttu-id="1198a-135">Merhaba iki JavaScript'ler hello gövde etiketi içinde hello aşağıdakileri ekleyerek bu sayfada daha önce eklediğimiz içerir.</span><span class="sxs-lookup"><span data-stu-id="1198a-135">Include hello two javascripts we added earlier in this page by adding hello following within hello body tag.</span></span> 
   
        <script type="text/javascript" src="javascript/main.js"></script>
        <script type="text/javascript" src="javascript/azure-engagement.js"></script>
3. <span data-ttu-id="1198a-136">Merhaba gövde etiketi toocall EngagementAgent's güncelleştirme `startActivity` yöntemi</span><span class="sxs-lookup"><span data-stu-id="1198a-136">Update hello body tag toocall EngagementAgent's `startActivity` method</span></span>
   
        <body onload="engagement.agent.startActivity('Home')">
4. <span data-ttu-id="1198a-137">**home.html** dosyanız bu şekilde görünür</span><span class="sxs-lookup"><span data-stu-id="1198a-137">Here is what your **home.html** will look like</span></span>
   
        <html>
        <head>
            ...
        </head>
        <body onload="engagement.agent.startActivity('Home')">
            <script type="text/javascript" src="javascript/main.js"></script>
            <script type="text/javascript" src="javascript/azure-engagement.js"></script>
        </body>
        </html>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="1198a-138">Uygulamayı gerçek zamanlı izlemeyle bağlama</span><span class="sxs-lookup"><span data-stu-id="1198a-138">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

  ![][2]

## <a name="extend-analytics"></a><span data-ttu-id="1198a-139">Analizi genişletme</span><span class="sxs-lookup"><span data-stu-id="1198a-139">Extend analytics</span></span>
<span data-ttu-id="1198a-140">Web analizi için kullanabileceğiniz SDK'sı şu anda kullanılabilir tüm hello yöntemler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1198a-140">Here are all hello methods currently available with Web SDK that you can use for analytics:</span></span>

1. <span data-ttu-id="1198a-141">Etkinlikler/Web sayfaları:</span><span class="sxs-lookup"><span data-stu-id="1198a-141">Activities/Web pages:</span></span>
   
        engagement.agent.startActivity(name);
        engagement.agent.endActivity();
2. <span data-ttu-id="1198a-142">Olaylar</span><span class="sxs-lookup"><span data-stu-id="1198a-142">Events</span></span>
   
        engagement.agent.sendEvent(name, extras);
3. <span data-ttu-id="1198a-143">Hatalar</span><span class="sxs-lookup"><span data-stu-id="1198a-143">Errors</span></span>
   
        engagement.agent.sendError(name, extras);
4. <span data-ttu-id="1198a-144">İşler</span><span class="sxs-lookup"><span data-stu-id="1198a-144">Jobs</span></span>
   
        engagement.agent.startJob(name);
        engagement.agent.endJob(name);

<!-- Images. -->
[1]: ./media/mobile-engagement-web-app-get-started/visual-studio-solution-js.png
[2]: ./media/mobile-engagement-web-app-get-started/session.png

