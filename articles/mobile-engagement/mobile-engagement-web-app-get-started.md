---
title: "Web Apps için Azure Mobile Engagement kullanmaya başlama | Microsoft Belgeleri"
description: "Web Apps için analizler ve anında iletme bildirimleri ile Azure Mobile Engagement kullanmayı öğrenin."
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
ms.openlocfilehash: abcb04e4e0a3ae4fdba3a4ded20b3846ac3b21e6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-web-apps"></a><span data-ttu-id="16705-103">Web Apps için Azure Mobile Engagement kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="16705-103">Get started with Azure Mobile Engagement for Web Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="16705-104">Bu konuda Web Uygulaması kullanımınızı anlamak için Azure Mobile Engagement’ın nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="16705-104">This topic shows you how to use Azure Mobile Engagement to understand your Web App usage.</span></span>

> [!NOTE]
> <span data-ttu-id="16705-105">Azure Mobile Engagement hizmeti, Mart 2018’de devre dışı bırakılacaktır. Şu anda yalnızca mevcut müşteriler tarafından kullanılabilmektedir.</span><span class="sxs-lookup"><span data-stu-id="16705-105">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="16705-106">Daha fazla bilgi için bkz. [Mobile Engagement nedir?](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="16705-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="16705-107">Bu öğretici için aşağıdakiler gereklidir:</span><span class="sxs-lookup"><span data-stu-id="16705-107">This tutorial requires the following:</span></span>

* <span data-ttu-id="16705-108">Visual Studio 2015 veya tercih ettiğiniz başka bir düzenleyici</span><span class="sxs-lookup"><span data-stu-id="16705-108">Visual Studio 2015 or any other editor of your choice</span></span>
* [<span data-ttu-id="16705-109">Web SDK</span><span class="sxs-lookup"><span data-stu-id="16705-109">Web SDK</span></span>](http://aka.ms/P7b453)

<span data-ttu-id="16705-110">Bu Web SDK Önizleme modundadır ve şu anda yalnızca Analizi destekleyip, tarayıcı ya da herhangi bir uygulama içi bildirim göndermeyi henüz desteklememektedir.</span><span class="sxs-lookup"><span data-stu-id="16705-110">This Web SDK is in Preview and only supports Analytics at the moment and doesn't support sending browser or in-app push notifications yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="16705-111">Bu öğreticiyi tamamlamak için etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="16705-111">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="16705-112">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="16705-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="16705-113">Ayrıntılar için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span><span class="sxs-lookup"><span data-stu-id="16705-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span></span>
> 
> 

## <a name="setup-mobile-engagement-for-your-web-app"></a><span data-ttu-id="16705-114">Web uygulamanız için Mobile Engagement ayarlama</span><span class="sxs-lookup"><span data-stu-id="16705-114">Setup Mobile Engagement for your Web app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="16705-115"><a id="connecting-app"></a>Uygulamanızı Mobile Engagement arka ucuna bağlama</span><span class="sxs-lookup"><span data-stu-id="16705-115"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="16705-116">Bu öğreticide, veri toplamak için gereken en küçük grup olan bir "temel tümleştirme" gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="16705-116">This tutorial presents a "basic integration," which is the minimal set required to collect data.</span></span>

<span data-ttu-id="16705-117">Tümleştirmeyi göstermek üzere Visual Studio ile temel bir web uygulaması oluşturulacaktır; ancak Visual Studio’nun dışında oluşturulmuş herhangi bir web uygulamasının adımlarını da izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="16705-117">We will create a basic web app with Visual Studio to demonstrate the integration though you can follow the steps with any web application created outside of Visual Studio also.</span></span> 

### <a name="create-a-new-web-app"></a><span data-ttu-id="16705-118">Yeni bir Web Uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="16705-118">Create a new Web App</span></span>
<span data-ttu-id="16705-119">Aşağıdaki adımlarda Visual Studio 2015 kullanıldığı varsayılmaktadır ancak Visual Studio'nun önceki sürümleri için de benzer adımlar izlenir.</span><span class="sxs-lookup"><span data-stu-id="16705-119">The following steps assume the use of Visual Studio 2015 though the steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="16705-120">Visual Studio'yu başlatın ve **Giriş** ekranında **Yeni Proje**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="16705-120">Start Visual Studio, and in the **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="16705-121">Açılır listeden **Web** -> **ASP.Net Web Uygulaması**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="16705-121">In the pop-up, select **Web** -> **ASP.Net Web Application**.</span></span> <span data-ttu-id="16705-122">Uygulamanın **Ad**, **Konum** ve **Çözüm adı** alanını doldurun ve ardından **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="16705-122">Fill in the app **Name**, **Location** and  **Solution name**, and then click **OK**.</span></span>
3. <span data-ttu-id="16705-123">**Şablon seçin** açılır penceresinde **ASP.Net 4.5 Şablonları** altında **Boş**’u seçin ve **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="16705-123">In the **Select a template** popup, select **Empty** under **ASP.Net 4.5 Templates** and click **OK**.</span></span> 

<span data-ttu-id="16705-124">Azure Mobile Engagement Web SDK’sını tümleştireceğimiz yeni ve boş bir Windows Web Uygulaması projesi oluşturmuş oldunuz.</span><span class="sxs-lookup"><span data-stu-id="16705-124">You have now created a new blank Web App project into which we will integrate the Azure Mobile Engagement Web SDK.</span></span>

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="16705-125">Uygulamanızı Mobile Engagement arka ucuna bağlama</span><span class="sxs-lookup"><span data-stu-id="16705-125">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="16705-126">Çözümünüzde **javascript** adlı yeni bir klasör oluşturun ve **azure-engagement.js** adlı Web SDK JS dosyasını buna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="16705-126">Create a new folder called **javascript** in your solution and add the Web SDK JS file **azure-engagement.js** into it.</span></span> 
2. <span data-ttu-id="16705-127">Aşağıdaki kodla birlikte bu javascript klasörüne **main.js** adlı yeni bir dosya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="16705-127">Add a new file called **main.js** in this javascript folder with the following code.</span></span> <span data-ttu-id="16705-128">Bağlantı dizesini güncelleştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="16705-128">Make sure to update the connection string.</span></span> <span data-ttu-id="16705-129">Bu `azureEngagement` nesnesi Web SDK yöntemlerine erişmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="16705-129">This `azureEngagement` object will be used to access Web SDK methods.</span></span> 
   
        var azureEngagement = {
            debug: true,
            connectionString: 'xxxxx'
        };
   
    ![Js dosyaları ile Visual Studio][1]

## <a name="enable-real-time-monitoring"></a><span data-ttu-id="16705-131">Gerçek zamanlı izlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="16705-131">Enable real-time monitoring</span></span>
<span data-ttu-id="16705-132">Veri göndermeye başlamak ve kullanıcıların etkin olduğundan emin olmak için, Mobile Engagement arka ucuna en az bir Etkinlik göndermelisiniz.</span><span class="sxs-lookup"><span data-stu-id="16705-132">In order to start sending data and ensuring that the users are active, you must send at least one Activity to the Mobile Engagement backend.</span></span> <span data-ttu-id="16705-133">Web uygulaması bağlamında etkinlik bir web sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="16705-133">An activity in the context of a web app is a web page.</span></span> 

1. <span data-ttu-id="16705-134">Çözümünüzde **home.html** adlı yeni bir sayfa oluşturun ve web uygulamanızın başlangıç sayfası olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="16705-134">Create a new page called **home.html** in your solution and set it as the starting page for your web app.</span></span> 
2. <span data-ttu-id="16705-135">Gövde etiketine aşağıdakileri ekleyerek bu sayfada daha önce eklediğimiz iki javascript’i dahil edin.</span><span class="sxs-lookup"><span data-stu-id="16705-135">Include the two javascripts we added earlier in this page by adding the following within the body tag.</span></span> 
   
        <script type="text/javascript" src="javascript/main.js"></script>
        <script type="text/javascript" src="javascript/azure-engagement.js"></script>
3. <span data-ttu-id="16705-136">Gövde etiketini EngagementAgent `startActivity` yöntemini çağıracak şekilde güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="16705-136">Update the body tag to call EngagementAgent's `startActivity` method</span></span>
   
        <body onload="engagement.agent.startActivity('Home')">
4. <span data-ttu-id="16705-137">**home.html** dosyanız bu şekilde görünür</span><span class="sxs-lookup"><span data-stu-id="16705-137">Here is what your **home.html** will look like</span></span>
   
        <html>
        <head>
            ...
        </head>
        <body onload="engagement.agent.startActivity('Home')">
            <script type="text/javascript" src="javascript/main.js"></script>
            <script type="text/javascript" src="javascript/azure-engagement.js"></script>
        </body>
        </html>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="16705-138">Uygulamayı gerçek zamanlı izlemeyle bağlama</span><span class="sxs-lookup"><span data-stu-id="16705-138">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

  ![][2]

## <a name="extend-analytics"></a><span data-ttu-id="16705-139">Analizi genişletme</span><span class="sxs-lookup"><span data-stu-id="16705-139">Extend analytics</span></span>
<span data-ttu-id="16705-140">Analiz için şu anda Web SDK ile birlikte kullanabileceğiniz tüm yöntemler aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="16705-140">Here are all the methods currently available with Web SDK that you can use for analytics:</span></span>

1. <span data-ttu-id="16705-141">Etkinlikler/Web sayfaları:</span><span class="sxs-lookup"><span data-stu-id="16705-141">Activities/Web pages:</span></span>
   
        engagement.agent.startActivity(name);
        engagement.agent.endActivity();
2. <span data-ttu-id="16705-142">Olaylar</span><span class="sxs-lookup"><span data-stu-id="16705-142">Events</span></span>
   
        engagement.agent.sendEvent(name, extras);
3. <span data-ttu-id="16705-143">Hatalar</span><span class="sxs-lookup"><span data-stu-id="16705-143">Errors</span></span>
   
        engagement.agent.sendError(name, extras);
4. <span data-ttu-id="16705-144">İşler</span><span class="sxs-lookup"><span data-stu-id="16705-144">Jobs</span></span>
   
        engagement.agent.startJob(name);
        engagement.agent.endJob(name);

<!-- Images. -->
[1]: ./media/mobile-engagement-web-app-get-started/visual-studio-solution-js.png
[2]: ./media/mobile-engagement-web-app-get-started/session.png

