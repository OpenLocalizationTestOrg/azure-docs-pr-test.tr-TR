---
title: "aaaWindows Phone Silverlight SDK yükseltme yordamları"
description: "Windows Phone Silverlight SDK yükseltme yordamları için Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 87130026-9759-4659-9184-788a3627a165
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d72e7b8a59ef2c0a95b22efbf1e5257271399ddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a><span data-ttu-id="b7cb8-103">Windows Phone Silverlight SDK yükseltme yordamları</span><span class="sxs-lookup"><span data-stu-id="b7cb8-103">Windows Phone Silverlight SDK Upgrade Procedures</span></span>
<span data-ttu-id="b7cb8-104">Uygulamanıza bizim SDK daha eski bir sürümü zaten bütünleştirdiyseniz noktaları hello SDK yükseltirken aşağıdaki tooconsider hello sahip.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-104">If you already have integrated an older version of our SDK into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="b7cb8-105">Merhaba SDK çeşitli sürümleri eksik birkaç yordamları toofollow olabilir.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="b7cb8-106">0.10.1 geçirirseniz örneğin hello izleyin toofirst sahip too0.11.0 "0.9.0'dan gelen too0.10.1" yordamı sonra hello "0.10.1 gelen too0.11.0" yordamı.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-106">For example if you migrate from 0.10.1 too0.11.0 you have toofirst follow hello "from 0.9.0 too0.10.1" procedure then hello "from 0.10.1 too0.11.0" procedure.</span></span>

## <a name="from-200-too330"></a><span data-ttu-id="b7cb8-107">2.0.0 gelen too3.3.0</span><span class="sxs-lookup"><span data-stu-id="b7cb8-107">From 2.0.0 too3.3.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="b7cb8-108">Test günlükleri</span><span class="sxs-lookup"><span data-stu-id="b7cb8-108">Test logs</span></span>
<span data-ttu-id="b7cb8-109">Konsol günlükleri Hello SDK tarafından üretilen artık etkin/devre dışı bırakılmış/filtrelenmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-109">Console logs produced by hello SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="b7cb8-110">toocustomize Bu, güncelleştirme hello özellik `EngagementAgent.Instance.TestLogEnabled` tooone hello kullanılabilir hello değerinin `EngagementTestLogLevel` numaralandırma, örneğin:</span><span class="sxs-lookup"><span data-stu-id="b7cb8-110">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-too200"></a><span data-ttu-id="b7cb8-111">1.1.1 gelen too2.0.0</span><span class="sxs-lookup"><span data-stu-id="b7cb8-111">From 1.1.1 too2.0.0</span></span>
<span data-ttu-id="b7cb8-112">Merhaba toomigrate'nın Azure Mobile Engagement tarafından desteklenen bir uygulamaya bir SDK tümleştirmesi hello Capptain hizmet gelen Capptain SAS tarafından nasıl sunulan açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-112">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b7cb8-113">Capptain ve Mobile Engagement olan değil hello aynı Hizmetleri ve yalnızca aşağıda verilen hello yordamı nasıl toomigrate hello istemci uygulamaları vurgular.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-113">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="b7cb8-114">Geçirme hello SDK hello uygulama hello Capptain sunucuları toohello Mobile Engagement sunuculardan veri geçişi YAPILMAZ</span><span class="sxs-lookup"><span data-stu-id="b7cb8-114">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="b7cb8-115">Önceki bir sürümünden geçiş yapıyorsanız, lütfen hello Capptain web sitesi toomigrate too1.1.1 ilk başvurun sonra hello aşağıdaki yordamı uygulayın</span><span class="sxs-lookup"><span data-stu-id="b7cb8-115">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.1.1 first then apply hello following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="b7cb8-116">Nuget paketi</span><span class="sxs-lookup"><span data-stu-id="b7cb8-116">Nuget package</span></span>
<span data-ttu-id="b7cb8-117">Değiştir **Capptain.WindowsPhone** tarafından **MicrosoftAzure.MobileEngagement** Nuget paketi.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-117">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="b7cb8-118">Mobil katılım uygulama</span><span class="sxs-lookup"><span data-stu-id="b7cb8-118">Applying Mobile Engagement</span></span>
<span data-ttu-id="b7cb8-119">Merhaba SDK kullanan hello terim `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-119">hello SDK uses hello term `Engagement`.</span></span> <span data-ttu-id="b7cb8-120">Proje toomatch tooupdate gereken bu değişikliği.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-120">You need tooupdate your project toomatch this change.</span></span>

<span data-ttu-id="b7cb8-121">Toouninstall, geçerli Capptain nuget paketi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-121">You need toouninstall your current Capptain nuget package.</span></span> <span data-ttu-id="b7cb8-122">Tüm değişikliklerinizi Capptain Kaynaklar klasörünü kaldırılacak göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-122">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="b7cb8-123">Tookeep istiyorsanız, bu dosyaların bir kopyasını sonra yapın.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-123">If you want tookeep those files then make a copy of them.</span></span>

<span data-ttu-id="b7cb8-124">Bundan sonra projenizde hello yeni Microsoft Azure katılım nuget paketini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-124">After that, install hello new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="b7cb8-125">Doğrudan üzerinde bulabilirsiniz [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span><span class="sxs-lookup"><span data-stu-id="b7cb8-125">You can find it directly on [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span></span> <span data-ttu-id="b7cb8-126">Tüm kaynak dosyaları katılım tarafından kullanılan ve hello yeni katılım DLL tooyour ekler bu eylem değiştirir başvuruları yansıtın.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-126">This action replaces all resources files used by Engagement and adds hello new Engagement DLL tooyour project References.</span></span>

<span data-ttu-id="b7cb8-127">Proje başvuruları Capptain DLL başvurularını silerek tooclean sahip.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-127">You have tooclean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="b7cb8-128">Bunu yapmazsanız Capptain hello sürümü çakışır ve hataları gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-128">If you do not make this, hello version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="b7cb8-129">Capptain kaynakları özelleştirdiyseniz, eski dosyaları içeriğinizi kopyalayın ve bunları hello yeni katılım dosyalarında yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-129">If you have customized Capptain resources, copy your old files content and paste them in hello new Engagement files.</span></span> <span data-ttu-id="b7cb8-130">Xaml ve cs dosyaları güncelleştirilmiş toobe gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-130">Please note that both xaml and cs files have toobe updated.</span></span>

<span data-ttu-id="b7cb8-131">Bu adımlar tamamlandığında tooreplace eski Capptain başvurular hello yeni katılım başvurular tarafından yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-131">When those steps are completed you only have tooreplace old Capptain references by hello new Engagement references.</span></span>

1. <span data-ttu-id="b7cb8-132">Tüm Capptain ad güncelleştirilmiş toobe sahip.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-132">All Capptain namespaces have toobe updated.</span></span>
   
    <span data-ttu-id="b7cb8-133">Geçişten önce:</span><span class="sxs-lookup"><span data-stu-id="b7cb8-133">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="b7cb8-134">Geçişten sonra:</span><span class="sxs-lookup"><span data-stu-id="b7cb8-134">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="b7cb8-135">"Capptain" içeren tüm Capptain sınıfları "Katılım" içermelidir.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-135">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="b7cb8-136">Geçişten önce:</span><span class="sxs-lookup"><span data-stu-id="b7cb8-136">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="b7cb8-137">Geçişten sonra:</span><span class="sxs-lookup"><span data-stu-id="b7cb8-137">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="b7cb8-138">XAML dosyaları için de Capptain ad alanı ve özniteliklerini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-138">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="b7cb8-139">Geçişten önce:</span><span class="sxs-lookup"><span data-stu-id="b7cb8-139">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="b7cb8-140">Geçişten sonra:</span><span class="sxs-lookup"><span data-stu-id="b7cb8-140">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="b7cb8-141">İçin diğer kaynakları Capptain resimler gibi Merhaba, bunlar da yeniden adlandırılmış toouse "Katılım" kaldırılmış lütfen unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-141">For hello other resources like Capptain pictures, please note that they also have been renamed toouse "Engagement".</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="b7cb8-142">Uygulama Kimliği / SDK anahtarı</span><span class="sxs-lookup"><span data-stu-id="b7cb8-142">Application ID / SDK Key</span></span>
<span data-ttu-id="b7cb8-143">Katılım bağlantı dizesini kullanır.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-143">Engagement uses a connection string.</span></span> <span data-ttu-id="b7cb8-144">Bir uygulama kimliği ve Mobile Engagement SDK'sı anahtarla toospecify yoksa, toospecify bir bağlantı dizesi yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-144">You don't have toospecify an application ID and an SDK key with Mobile Engagement, you only have toospecify a connection string.</span></span> <span data-ttu-id="b7cb8-145">Bunu EngagementConfiguration dosyanızı ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-145">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="b7cb8-146">Merhaba katılım yapılandırma ayarlanabilir, `Resources\EngagementConfiguration.xml` projenizin dosya.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-146">hello Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="b7cb8-147">Bu dosya toospecify düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="b7cb8-147">Edit this file toospecify:</span></span>

* <span data-ttu-id="b7cb8-148">Uygulama bağlantı dizenizi etiketleri arasına `<connectionString>` ve `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-148">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="b7cb8-149">Çalışma zamanında, bunun yerine, çağırabilirsiniz hello aşağıdaki toospecify istiyorsanız yöntemi hello katılım aracı başlatmadan önce:</span><span class="sxs-lookup"><span data-stu-id="b7cb8-149">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="b7cb8-150">Merhaba bağlantı dizesi, uygulamanız için hello Klasik Azure portalı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-150">hello connection string for your application is displayed in hello Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="b7cb8-151">Öğe adı değişikliği</span><span class="sxs-lookup"><span data-stu-id="b7cb8-151">Items name change</span></span>
<span data-ttu-id="b7cb8-152">Tüm öğeleri adlı *capptain* adlandırılmış *engagement*.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-152">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="b7cb8-153">Benzer şekilde *Capptain* çok*Engagement*.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-153">Similarly for *Capptain* too*Engagement*.</span></span>

<span data-ttu-id="b7cb8-154">Yaygın olarak kullanılan Capptain öğeleri örnekleri:</span><span class="sxs-lookup"><span data-stu-id="b7cb8-154">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="b7cb8-155">Şimdi EngagementConfiguration adlı CapptainConfiguration</span><span class="sxs-lookup"><span data-stu-id="b7cb8-155">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="b7cb8-156">Şimdi EngagementAgent adlı CapptainAgent</span><span class="sxs-lookup"><span data-stu-id="b7cb8-156">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="b7cb8-157">Şimdi EngagementReach adlı CapptainReach</span><span class="sxs-lookup"><span data-stu-id="b7cb8-157">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="b7cb8-158">Şimdi EngagementHttpConfig adlı CapptainHttpConfig</span><span class="sxs-lookup"><span data-stu-id="b7cb8-158">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="b7cb8-159">Şimdi GetEngagementPageName adlı GetCapptainPageName</span><span class="sxs-lookup"><span data-stu-id="b7cb8-159">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="b7cb8-160">Ayrıca etkiler yeniden adlandırmak Not yöntemleri geçersiz kılındı.</span><span class="sxs-lookup"><span data-stu-id="b7cb8-160">Note that rename also affects overridden methods.</span></span>

