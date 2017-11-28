---
title: "aaaAzure Mobile Engagement Web SDK tümleştirmesi | Microsoft Docs"
description: "en son güncelleştirmeler ve yordamlar hello Azure Mobile Engagement Web SDK'sı için hello"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: b5daa2a2-942b-489d-aa1d-568c3b25e56f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 02/29/2016
ms.author: piyushjo
ms.openlocfilehash: 99613b68b615bec4ddcfcc8e4e0133ce9d887bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a><span data-ttu-id="8847b-103">Bir web uygulamasına Azure Mobile Engagement tümleştirme</span><span class="sxs-lookup"><span data-stu-id="8847b-103">Integrate Azure Mobile Engagement in a web application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8847b-104">Windows Evrensel</span><span class="sxs-lookup"><span data-stu-id="8847b-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="8847b-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="8847b-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="8847b-106">iOS</span><span class="sxs-lookup"><span data-stu-id="8847b-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="8847b-107">Android</span><span class="sxs-lookup"><span data-stu-id="8847b-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="8847b-108">Bu makalede Hello yordamlarda hello en basit yolu tooactivate hello analizi ve Azure Mobile Engagement işlevlerde web uygulamanızda izleme açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8847b-108">hello procedures in this article describe hello simplest way tooactivate hello analytics and monitoring functions in Azure Mobile Engagement in your web application.</span></span>

<span data-ttu-id="8847b-109">Gerekli toocompute hello adımları tooactivate hello günlük raporlar kullanıcıları, oturumlar, etkinlikleri, kilitlenme ve technicals ilgili tüm İstatistikler izleyin.</span><span class="sxs-lookup"><span data-stu-id="8847b-109">Follow hello steps tooactivate hello log reports that are needed toocompute all statistics about users, sessions, activities, crashes, and technicals.</span></span> <span data-ttu-id="8847b-110">Olaylar, hatalar ve işleri gibi uygulama bağımlı istatistikler için günlüğü raporları el ile hello Azure Mobile Engagement API'sini kullanarak etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8847b-110">For application-dependent statistics, such as events, errors, and jobs, you must activate log reports manually by using hello Azure Mobile Engagement API.</span></span> <span data-ttu-id="8847b-111">Daha fazla bilgi için bilgi [nasıl toouse hello Mobile Engagement bir web uygulamasında API etiketleme Gelişmiş](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="8847b-111">For more information, learn [how toouse hello advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="8847b-112">Giriş</span><span class="sxs-lookup"><span data-stu-id="8847b-112">Introduction</span></span>
<span data-ttu-id="8847b-113">[Hello Azure Mobile Engagement Web SDK Yükle](http://aka.ms/P7b453).</span><span class="sxs-lookup"><span data-stu-id="8847b-113">[Download hello Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).</span></span>
<span data-ttu-id="8847b-114">Mobil katılım Web SDK'sı tek bir JavaScript dosyası sevk hello, sahip olduğunuz azure-engagement.js, site veya web uygulamanızın her bir sayfasında tooinclude.</span><span class="sxs-lookup"><span data-stu-id="8847b-114">hello Mobile Engagement Web SDK is shipped as a single JavaScript file, azure-engagement.js, which you have tooinclude in each page of your site or web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8847b-115">Bu komut dosyasını çalıştırmadan önce komut dosyası çalıştırma veya kod parçacığında, tooconfigure Mobile Engagement uygulamanız için yazdığınız kodu.</span><span class="sxs-lookup"><span data-stu-id="8847b-115">Before you run this script, you must run a script or code snippet that you write tooconfigure Mobile Engagement for your application.</span></span>
> 
> 

## <a name="browser-compatibility"></a><span data-ttu-id="8847b-116">Tarayıcı uyumluluğu</span><span class="sxs-lookup"><span data-stu-id="8847b-116">Browser compatibility</span></span>
<span data-ttu-id="8847b-117">Merhaba Mobile Engagement Web SDK kodlama ve kod çözme, ayrıca (Merhaba W3C CORS belirtimi olan) toocross etki alanı AJAX istekleri yerel JSON kullanır.</span><span class="sxs-lookup"><span data-stu-id="8847b-117">hello Mobile Engagement Web SDK uses native JSON encoding and decoding, in addition toocross-domain AJAX requests (relying on hello W3C CORS specification).</span></span> <span data-ttu-id="8847b-118">Tarayıcılar aşağıdaki hello ile uyumludur:</span><span class="sxs-lookup"><span data-stu-id="8847b-118">It's compatible with hello following browsers:</span></span>

* <span data-ttu-id="8847b-119">Microsoft Edge 12 +</span><span class="sxs-lookup"><span data-stu-id="8847b-119">Microsoft Edge 12+</span></span>
* <span data-ttu-id="8847b-120">Internet Explorer 10 +</span><span class="sxs-lookup"><span data-stu-id="8847b-120">Internet Explorer 10+</span></span>
* <span data-ttu-id="8847b-121">Firefox 3.5 +</span><span class="sxs-lookup"><span data-stu-id="8847b-121">Firefox 3.5+</span></span>
* <span data-ttu-id="8847b-122">Chrome 4 +</span><span class="sxs-lookup"><span data-stu-id="8847b-122">Chrome 4+</span></span>
* <span data-ttu-id="8847b-123">Safari 6 +</span><span class="sxs-lookup"><span data-stu-id="8847b-123">Safari 6+</span></span>
* <span data-ttu-id="8847b-124">Opera 12 +</span><span class="sxs-lookup"><span data-stu-id="8847b-124">Opera 12+</span></span>

## <a name="configure-mobile-engagement"></a><span data-ttu-id="8847b-125">Mobil katılım yapılandırın</span><span class="sxs-lookup"><span data-stu-id="8847b-125">Configure Mobile Engagement</span></span>
<span data-ttu-id="8847b-126">Bir genel oluşturan bir komut dosyası yazma `azureEngagement` aşağıdaki örneğine hello olduğu gibi JavaScript nesne.</span><span class="sxs-lookup"><span data-stu-id="8847b-126">Write a script that creates a global `azureEngagement` JavaScript object, as in hello following example.</span></span> <span data-ttu-id="8847b-127">Sitenizi katları sayfaları olabileceğinden, bu örnek, bu komut dosyası her sayfada dahil olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="8847b-127">Because your site might have multiples pages, this example assumes that this script is included in every page.</span></span> <span data-ttu-id="8847b-128">Bu örnekte, hello JavaScript nesne adlı `azure-engagement-conf.js`.</span><span class="sxs-lookup"><span data-stu-id="8847b-128">In this example, hello JavaScript object is named `azure-engagement-conf.js`.</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

<span data-ttu-id="8847b-129">Merhaba `connectionString` değeri, uygulamanızın görüntülenen için Azure portal hello.</span><span class="sxs-lookup"><span data-stu-id="8847b-129">hello `connectionString` value for your application is displayed in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="8847b-130">`appVersionName`ve `appVersionCode` isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="8847b-130">`appVersionName` and `appVersionCode` are optional.</span></span> <span data-ttu-id="8847b-131">Ancak, böylece analytics sürüm bilgileri işleyebilmesi için bunları yapılandırmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="8847b-131">However, we recommend that you configure them so that analytics can process version information.</span></span>
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a><span data-ttu-id="8847b-132">Mobile Engagement betikleri sayfalarınızda içerir</span><span class="sxs-lookup"><span data-stu-id="8847b-132">Include Mobile Engagement scripts in your pages</span></span>
<span data-ttu-id="8847b-133">Mobile Engagement betikleri tooyour sayfaları yolları aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="8847b-133">Add Mobile Engagement scripts tooyour pages in one of hello following ways:</span></span>

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

<span data-ttu-id="8847b-134">Veya bu:</span><span class="sxs-lookup"><span data-stu-id="8847b-134">Or this:</span></span>

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a><span data-ttu-id="8847b-135">Diğer ad</span><span class="sxs-lookup"><span data-stu-id="8847b-135">Alias</span></span>
<span data-ttu-id="8847b-136">Merhaba Mobile Engagement Web SDK komut yüklendikten sonra hello oluşturduğu **katılım** diğer tooaccess hello SDK API'leri.</span><span class="sxs-lookup"><span data-stu-id="8847b-136">After hello Mobile Engagement Web SDK script is loaded, it creates hello **engagement** alias tooaccess hello SDK APIs.</span></span> <span data-ttu-id="8847b-137">Bu diğer ad toodefine hello SDK yapılandırma kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="8847b-137">You cannot use this alias toodefine hello SDK configuration.</span></span> <span data-ttu-id="8847b-138">Bu diğer adı, bu belgede bir başvuru olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8847b-138">This alias is used as a reference in this documentation.</span></span>

<span data-ttu-id="8847b-139">Merhaba varsayılan diğer sayfanızdan başka bir genel değişkeni ile çakışırsa, hello Mobile Engagement Web SDK yükleme önce onu hello yapılandırmasında şu şekilde tanımlayabilirsiniz olduğunu unutmayın:</span><span class="sxs-lookup"><span data-stu-id="8847b-139">Note that if hello default alias conflicts with another global variable from your page, you can redefine it in hello configuration as follows before you load hello Mobile Engagement Web SDK:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a><span data-ttu-id="8847b-140">Temel raporlama</span><span class="sxs-lookup"><span data-stu-id="8847b-140">Basic reporting</span></span>
<span data-ttu-id="8847b-141">Temel Mobile Engagement ' raporlama, kullanıcılar, oturumlar, etkinlikler ile çökmeler ilgili istatistikler gibi oturum düzeyi istatistikleri ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8847b-141">Basic reporting in Mobile Engagement covers session-level statistics, such as statistics about users, sessions, activities, and crashes.</span></span>

### <a name="session-tracking"></a><span data-ttu-id="8847b-142">Oturum izleme</span><span class="sxs-lookup"><span data-stu-id="8847b-142">Session tracking</span></span>
<span data-ttu-id="8847b-143">Mobile Engagement oturum etkinlikler dizisini bölünür, her bir ad tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="8847b-143">A Mobile Engagement session is divided into a sequence of activities, each identified by a name.</span></span>

<span data-ttu-id="8847b-144">Klasik Web sitesinde, sitenizin her sayfada farklı bir etkinlik bildirmek öneririz.</span><span class="sxs-lookup"><span data-stu-id="8847b-144">In a classic website, we recommend that you declare a different activity on each page of your site.</span></span> <span data-ttu-id="8847b-145">Geçerli sayfada hiçbir zaman hangi hello değiştirir bir Web sitesi veya web uygulaması için daha küçük bir ölçek tootrack hello etkinliklerini gibi hello sayfasında isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8847b-145">For a website or web application in which hello current page never changes, you might want tootrack hello activities on a smaller scale, such as within hello page.</span></span>

<span data-ttu-id="8847b-146">Ya da şekilde toostart ya da değişiklik hello geçerli kullanıcı etkinliği, çağrı hello `engagement.agent.startActivity` işlevi.</span><span class="sxs-lookup"><span data-stu-id="8847b-146">Either way, toostart or change hello current user activity, call hello `engagement.agent.startActivity` function.</span></span> <span data-ttu-id="8847b-147">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="8847b-147">For example:</span></span>

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

<span data-ttu-id="8847b-148">Merhaba Mobile Engagement sunucu otomatik olarak üç hello uygulama sayfası kapatıldıktan sonra dakika içinde açık bir oturumu sona erer.</span><span class="sxs-lookup"><span data-stu-id="8847b-148">hello Mobile Engagement server automatically ends an open session within three minutes after hello application page is closed.</span></span>

<span data-ttu-id="8847b-149">Alternatif olarak, bir oturumu el ile çağırarak sonlandırabilir `engagement.agent.endActivity`.</span><span class="sxs-lookup"><span data-stu-id="8847b-149">Alternatively, you can end a session manually by calling `engagement.agent.endActivity`.</span></span> <span data-ttu-id="8847b-150">Bu ayarlar hello geçerli kullanıcı etkinliği too'Idle.'</span><span class="sxs-lookup"><span data-stu-id="8847b-150">This sets hello current user activity too'Idle.'</span></span>  <span data-ttu-id="8847b-151">Merhaba oturumunu 10 saniye sonra sürece yeni bir çok çağrı`engagement.agent.startActivity` hello oturum sürdürür.</span><span class="sxs-lookup"><span data-stu-id="8847b-151">hello session will end 10 seconds later unless a new call too`engagement.agent.startActivity` resumes hello session.</span></span>

<span data-ttu-id="8847b-152">Merhaba 10 saniye arasında bir gecikme hello genel katılım nesnesinde aşağıdaki gibi yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8847b-152">You can configure hello 10-second delay in hello global engagement object, as follows:</span></span>

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end hello session as soon as endActivity is called

> [!NOTE]
> <span data-ttu-id="8847b-153">Kullanamazsınız `engagement.agent.endActivity` hello içinde `onunload` geri çağırma çünkü bu aşamada AJAX çağrıları yapamazsınız.</span><span class="sxs-lookup"><span data-stu-id="8847b-153">You cannot use `engagement.agent.endActivity` in hello `onunload` callback because you cannot make AJAX calls at this stage.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="8847b-154">Gelişmiş raporlama</span><span class="sxs-lookup"><span data-stu-id="8847b-154">Advanced reporting</span></span>
<span data-ttu-id="8847b-155">İsteğe bağlı olarak, tooreport uygulamaya özgü olaylar, hatalar ve işleri istiyorsanız, toouse hello Mobile Engagement API gerekir.</span><span class="sxs-lookup"><span data-stu-id="8847b-155">Optionally, if you want tooreport application-specific events, errors, and jobs, you need toouse hello Mobile Engagement API.</span></span> <span data-ttu-id="8847b-156">Merhaba Mobile Engagement API hello erişim `engagement.agent` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="8847b-156">You access hello Mobile Engagement API through hello `engagement.agent` object.</span></span>

<span data-ttu-id="8847b-157">Tüm Gelişmiş hello Mobile Engagement API, Mobile Engagement'ın özellikleri hello erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8847b-157">You can access all of hello advanced capabilities in Mobile Engagement in hello Mobile Engagement API.</span></span> <span data-ttu-id="8847b-158">Merhaba API hello makalesinde ayrıntılı [nasıl toouse hello Mobile Engagement bir web uygulamasında API etiketleme Gelişmiş](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="8847b-158">hello API is detailed in hello article [How toouse hello advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="customize-hello-urls-used-for-ajax-calls"></a><span data-ttu-id="8847b-159">AJAX çağrıları için kullanılan hello URL'leri özelleştirme</span><span class="sxs-lookup"><span data-stu-id="8847b-159">Customize hello URLs used for AJAX calls</span></span>
<span data-ttu-id="8847b-160">Mobile Engagement Web SDK kullanan bu hello URL'leri özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8847b-160">You can customize URLs that hello Mobile Engagement Web SDK uses.</span></span> <span data-ttu-id="8847b-161">Örneğin, hello yapılandırma kılabilirsiniz tooredefine hello günlük URL'si (Merhaba SDK uç noktası için günlük), şöyle:</span><span class="sxs-lookup"><span data-stu-id="8847b-161">For example, tooredefine hello log URL (hello SDK endpoint for logging), you can override hello configuration like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

<span data-ttu-id="8847b-162">URL işlevlerinizi ile başlayan bir dize döndürecek varsa `/`, `//`, `http://`, veya `https://`, hello varsayılan düzeni kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="8847b-162">If your URL functions return a string that begins with `/`, `//`, `http://`, or `https://`, hello default scheme is not used.</span></span> <span data-ttu-id="8847b-163">Varsayılan olarak, hello `https://` düzeni, bu URL'ler için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8847b-163">By default, hello `https://` scheme is used for those URLs.</span></span> <span data-ttu-id="8847b-164">Toocustomize hello varsayılan düzeni istiyorsanız, bu gibi hello yapılandırma geçersiz kıl:</span><span class="sxs-lookup"><span data-stu-id="8847b-164">If you want toocustomize hello default scheme, override hello configuration, like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
