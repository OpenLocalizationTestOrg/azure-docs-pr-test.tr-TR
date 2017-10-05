---
title: "Azure Mobile Engagement Web SDK tümleştirmesi | Microsoft Docs"
description: "En son güncelleştirmeleri ve Azure Mobile Engagement Web SDK'sı için yordamlar"
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
ms.openlocfilehash: 7d8eaa180e277741a583522ee62d68f5247b92bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a><span data-ttu-id="d7636-103">Bir web uygulamasına Azure Mobile Engagement tümleştirme</span><span class="sxs-lookup"><span data-stu-id="d7636-103">Integrate Azure Mobile Engagement in a web application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d7636-104">Windows Evrensel</span><span class="sxs-lookup"><span data-stu-id="d7636-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="d7636-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="d7636-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="d7636-106">iOS</span><span class="sxs-lookup"><span data-stu-id="d7636-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="d7636-107">Android</span><span class="sxs-lookup"><span data-stu-id="d7636-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="d7636-108">Bu makaledeki yordamlar analizi ve izleme işlevleri Azure Mobile Engagement web uygulamanızda etkinleştirmek için en basit yolu açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d7636-108">The procedures in this article describe the simplest way to activate the analytics and monitoring functions in Azure Mobile Engagement in your web application.</span></span>

<span data-ttu-id="d7636-109">Kullanıcılar, oturumlar, etkinlikleri, kilitlenme ve technicals ilgili tüm İstatistikler işlem için gereken günlüğü raporları etkinleştirme adımlarını izleyin.</span><span class="sxs-lookup"><span data-stu-id="d7636-109">Follow the steps to activate the log reports that are needed to compute all statistics about users, sessions, activities, crashes, and technicals.</span></span> <span data-ttu-id="d7636-110">Olaylar, hatalar ve işleri gibi uygulama bağımlı istatistikler için günlüğü raporları el ile Azure Mobile Engagement API'sini kullanarak etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7636-110">For application-dependent statistics, such as events, errors, and jobs, you must activate log reports manually by using the Azure Mobile Engagement API.</span></span> <span data-ttu-id="d7636-111">Daha fazla bilgi için bilgi [bir web uygulamasında API etiketleme Gelişmiş Mobile Engagement kullanmayı](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="d7636-111">For more information, learn [how to use the advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="d7636-112">Giriş</span><span class="sxs-lookup"><span data-stu-id="d7636-112">Introduction</span></span>
<span data-ttu-id="d7636-113">[Azure Mobile Engagement Web SDK Yükle](http://aka.ms/P7b453).</span><span class="sxs-lookup"><span data-stu-id="d7636-113">[Download the Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).</span></span>
<span data-ttu-id="d7636-114">Mobile Engagement Web SDK tek bir JavaScript dosyası sevk site veya web uygulamanızın her sayfasına eklemek olan azure-engagement.js.</span><span class="sxs-lookup"><span data-stu-id="d7636-114">The Mobile Engagement Web SDK is shipped as a single JavaScript file, azure-engagement.js, which you have to include in each page of your site or web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d7636-115">Bu komut dosyasını çalıştırmadan önce uygulamanız için Mobile Engagement yapılandırmak için yazma bir komut dosyası veya kod parçacığı çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7636-115">Before you run this script, you must run a script or code snippet that you write to configure Mobile Engagement for your application.</span></span>
> 
> 

## <a name="browser-compatibility"></a><span data-ttu-id="d7636-116">Tarayıcı uyumluluğu</span><span class="sxs-lookup"><span data-stu-id="d7636-116">Browser compatibility</span></span>
<span data-ttu-id="d7636-117">Mobile Engagement Web SDK'sı, kodlama ve etki alanları arası AJAX istekleri (W3C CORS belirtimi olan) yanı sıra kod çözme yerel JSON kullanır.</span><span class="sxs-lookup"><span data-stu-id="d7636-117">The Mobile Engagement Web SDK uses native JSON encoding and decoding, in addition to cross-domain AJAX requests (relying on the W3C CORS specification).</span></span> <span data-ttu-id="d7636-118">Aşağıdaki tarayıcılarla uyumludur:</span><span class="sxs-lookup"><span data-stu-id="d7636-118">It's compatible with the following browsers:</span></span>

* <span data-ttu-id="d7636-119">Microsoft Edge 12 +</span><span class="sxs-lookup"><span data-stu-id="d7636-119">Microsoft Edge 12+</span></span>
* <span data-ttu-id="d7636-120">Internet Explorer 10 +</span><span class="sxs-lookup"><span data-stu-id="d7636-120">Internet Explorer 10+</span></span>
* <span data-ttu-id="d7636-121">Firefox 3.5 +</span><span class="sxs-lookup"><span data-stu-id="d7636-121">Firefox 3.5+</span></span>
* <span data-ttu-id="d7636-122">Chrome 4 +</span><span class="sxs-lookup"><span data-stu-id="d7636-122">Chrome 4+</span></span>
* <span data-ttu-id="d7636-123">Safari 6 +</span><span class="sxs-lookup"><span data-stu-id="d7636-123">Safari 6+</span></span>
* <span data-ttu-id="d7636-124">Opera 12 +</span><span class="sxs-lookup"><span data-stu-id="d7636-124">Opera 12+</span></span>

## <a name="configure-mobile-engagement"></a><span data-ttu-id="d7636-125">Mobil katılım yapılandırın</span><span class="sxs-lookup"><span data-stu-id="d7636-125">Configure Mobile Engagement</span></span>
<span data-ttu-id="d7636-126">Bir genel oluşturan bir komut dosyası yazma `azureEngagement` aşağıdaki örnekteki gibi JavaScript nesne.</span><span class="sxs-lookup"><span data-stu-id="d7636-126">Write a script that creates a global `azureEngagement` JavaScript object, as in the following example.</span></span> <span data-ttu-id="d7636-127">Sitenizi katları sayfaları olabileceğinden, bu örnek, bu komut dosyası her sayfada dahil olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="d7636-127">Because your site might have multiples pages, this example assumes that this script is included in every page.</span></span> <span data-ttu-id="d7636-128">Bu örnekte, JavaScript nesne adlı `azure-engagement-conf.js`.</span><span class="sxs-lookup"><span data-stu-id="d7636-128">In this example, the JavaScript object is named `azure-engagement-conf.js`.</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

<span data-ttu-id="d7636-129">`connectionString` Uygulamanızı Azure portalında görüntülenen için bir değer.</span><span class="sxs-lookup"><span data-stu-id="d7636-129">The `connectionString` value for your application is displayed in the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="d7636-130">`appVersionName`ve `appVersionCode` isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="d7636-130">`appVersionName` and `appVersionCode` are optional.</span></span> <span data-ttu-id="d7636-131">Ancak, böylece analytics sürüm bilgileri işleyebilmesi için bunları yapılandırmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="d7636-131">However, we recommend that you configure them so that analytics can process version information.</span></span>
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a><span data-ttu-id="d7636-132">Mobile Engagement betikleri sayfalarınızda içerir</span><span class="sxs-lookup"><span data-stu-id="d7636-132">Include Mobile Engagement scripts in your pages</span></span>
<span data-ttu-id="d7636-133">Mobile Engagement betikleri sayfalarınıza aşağıdaki yollardan biriyle ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d7636-133">Add Mobile Engagement scripts to your pages in one of the following ways:</span></span>

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

<span data-ttu-id="d7636-134">Veya bu:</span><span class="sxs-lookup"><span data-stu-id="d7636-134">Or this:</span></span>

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a><span data-ttu-id="d7636-135">Diğer ad</span><span class="sxs-lookup"><span data-stu-id="d7636-135">Alias</span></span>
<span data-ttu-id="d7636-136">Mobile Engagement Web SDK komut dosyası yüklendikten sonra oluşturduğu **katılım** SDK API'leri erişmek için diğer ad.</span><span class="sxs-lookup"><span data-stu-id="d7636-136">After the Mobile Engagement Web SDK script is loaded, it creates the **engagement** alias to access the SDK APIs.</span></span> <span data-ttu-id="d7636-137">SDK yapılandırmasını tanımlamak için bu diğer ad kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="d7636-137">You cannot use this alias to define the SDK configuration.</span></span> <span data-ttu-id="d7636-138">Bu diğer adı, bu belgede bir başvuru olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d7636-138">This alias is used as a reference in this documentation.</span></span>

<span data-ttu-id="d7636-139">Varsayılan diğer ad sayfanızdan başka bir genel değişkeni ile çakışırsa, Mobile Engagement Web SDK'sı yükleme önce bu yapılandırmada şu şekilde tanımlayabilirsiniz olduğunu unutmayın:</span><span class="sxs-lookup"><span data-stu-id="d7636-139">Note that if the default alias conflicts with another global variable from your page, you can redefine it in the configuration as follows before you load the Mobile Engagement Web SDK:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a><span data-ttu-id="d7636-140">Temel raporlama</span><span class="sxs-lookup"><span data-stu-id="d7636-140">Basic reporting</span></span>
<span data-ttu-id="d7636-141">Temel Mobile Engagement ' raporlama, kullanıcılar, oturumlar, etkinlikler ile çökmeler ilgili istatistikler gibi oturum düzeyi istatistikleri ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d7636-141">Basic reporting in Mobile Engagement covers session-level statistics, such as statistics about users, sessions, activities, and crashes.</span></span>

### <a name="session-tracking"></a><span data-ttu-id="d7636-142">Oturum izleme</span><span class="sxs-lookup"><span data-stu-id="d7636-142">Session tracking</span></span>
<span data-ttu-id="d7636-143">Mobile Engagement oturum etkinlikler dizisini bölünür, her bir ad tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="d7636-143">A Mobile Engagement session is divided into a sequence of activities, each identified by a name.</span></span>

<span data-ttu-id="d7636-144">Klasik Web sitesinde, sitenizin her sayfada farklı bir etkinlik bildirmek öneririz.</span><span class="sxs-lookup"><span data-stu-id="d7636-144">In a classic website, we recommend that you declare a different activity on each page of your site.</span></span> <span data-ttu-id="d7636-145">Hangi asla geçerli sayfa değişiklikleri bir Web sitesi veya web uygulaması için etkinliklerini izlemek page içinde daha küçük bir ölçekte gibi isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7636-145">For a website or web application in which the current page never changes, you might want to track the activities on a smaller scale, such as within the page.</span></span>

<span data-ttu-id="d7636-146">Başlat veya geçerli kullanıcı etkinliği değiştirmek için her iki durumda da çağrı `engagement.agent.startActivity` işlevi.</span><span class="sxs-lookup"><span data-stu-id="d7636-146">Either way, to start or change the current user activity, call the `engagement.agent.startActivity` function.</span></span> <span data-ttu-id="d7636-147">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="d7636-147">For example:</span></span>

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

<span data-ttu-id="d7636-148">Mobile Engagement sunucunun bir açık oturum üç uygulama sayfası kapatıldıktan sonra dakika içinde otomatik olarak sona erer.</span><span class="sxs-lookup"><span data-stu-id="d7636-148">The Mobile Engagement server automatically ends an open session within three minutes after the application page is closed.</span></span>

<span data-ttu-id="d7636-149">Alternatif olarak, bir oturumu el ile çağırarak sonlandırabilir `engagement.agent.endActivity`.</span><span class="sxs-lookup"><span data-stu-id="d7636-149">Alternatively, you can end a session manually by calling `engagement.agent.endActivity`.</span></span> <span data-ttu-id="d7636-150">Bu geçerli bir kullanıcı etkinliği 'Boşta.' için ayarlar</span><span class="sxs-lookup"><span data-stu-id="d7636-150">This sets the current user activity to 'Idle.'</span></span>  <span data-ttu-id="d7636-151">Oturum, sürece 10 saniye sonra sona erecek için yeni bir çağrı `engagement.agent.startActivity` oturum sürdürür.</span><span class="sxs-lookup"><span data-stu-id="d7636-151">The session will end 10 seconds later unless a new call to `engagement.agent.startActivity` resumes the session.</span></span>

<span data-ttu-id="d7636-152">10 saniye arasında bir gecikme genel katılım nesnesinde aşağıdaki gibi yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d7636-152">You can configure the 10-second delay in the global engagement object, as follows:</span></span>

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end the session as soon as endActivity is called

> [!NOTE]
> <span data-ttu-id="d7636-153">Kullanamazsınız `engagement.agent.endActivity` içinde `onunload` geri çağırma çünkü bu aşamada AJAX çağrıları yapamazsınız.</span><span class="sxs-lookup"><span data-stu-id="d7636-153">You cannot use `engagement.agent.endActivity` in the `onunload` callback because you cannot make AJAX calls at this stage.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="d7636-154">Gelişmiş raporlama</span><span class="sxs-lookup"><span data-stu-id="d7636-154">Advanced reporting</span></span>
<span data-ttu-id="d7636-155">İsteğe bağlı olarak, uygulamaya özgü olaylar, hatalar ve işleri rapor istiyorsanız, Mobile Engagement API'sini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7636-155">Optionally, if you want to report application-specific events, errors, and jobs, you need to use the Mobile Engagement API.</span></span> <span data-ttu-id="d7636-156">Mobile Engagement API aracılığıyla erişim `engagement.agent` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="d7636-156">You access the Mobile Engagement API through the `engagement.agent` object.</span></span>

<span data-ttu-id="d7636-157">Tüm mobil katılım API'sindeki Mobile Engagement'ın gelişmiş özelliklerinden erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7636-157">You can access all of the advanced capabilities in Mobile Engagement in the Mobile Engagement API.</span></span> <span data-ttu-id="d7636-158">API makalesinde ayrıntılı [bir web uygulamasında API etiketleme Gelişmiş Mobile Engagement kullanmayı](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="d7636-158">The API is detailed in the article [How to use the advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="customize-the-urls-used-for-ajax-calls"></a><span data-ttu-id="d7636-159">AJAX çağrıları için kullanılan URL'leri özelleştirme</span><span class="sxs-lookup"><span data-stu-id="d7636-159">Customize the URLs used for AJAX calls</span></span>
<span data-ttu-id="d7636-160">Mobile Engagement Web SDK'sı URL'leri özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7636-160">You can customize URLs that the Mobile Engagement Web SDK uses.</span></span> <span data-ttu-id="d7636-161">Örneğin, günlük URL'si (SDK uç noktası için günlük) tanımlanacak yapılandırma bu gibi geçersiz kılabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d7636-161">For example, to redefine the log URL (the SDK endpoint for logging), you can override the configuration like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

<span data-ttu-id="d7636-162">URL işlevlerinizi ile başlayan bir dize döndürecek varsa `/`, `//`, `http://`, veya `https://`, varsayılan düzenini kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="d7636-162">If your URL functions return a string that begins with `/`, `//`, `http://`, or `https://`, the default scheme is not used.</span></span> <span data-ttu-id="d7636-163">Varsayılan olarak, `https://` düzeni, bu URL'ler için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d7636-163">By default, the `https://` scheme is used for those URLs.</span></span> <span data-ttu-id="d7636-164">Varsayılan şema özelleştirmek istiyorsanız, bu gibi yapılandırma geçersiz kıl:</span><span class="sxs-lookup"><span data-stu-id="d7636-164">If you want to customize the default scheme, override the configuration, like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
