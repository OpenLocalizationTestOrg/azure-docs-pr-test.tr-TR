---
title: "Windows Phone Silverlight SDK yükseltme yordamları"
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
ms.openlocfilehash: f87f65788075c7f4067e77946e1bcbc8f3709317
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a><span data-ttu-id="6378d-103">Windows Phone Silverlight SDK yükseltme yordamları</span><span class="sxs-lookup"><span data-stu-id="6378d-103">Windows Phone Silverlight SDK Upgrade Procedures</span></span>
<span data-ttu-id="6378d-104">Uygulamanıza bizim SDK daha eski bir sürümü zaten bütünleştirdiyseniz, SDK'yı yükseltirken aşağıdaki noktaları dikkate almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6378d-104">If you already have integrated an older version of our SDK into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="6378d-105">SDK çeşitli sürümleri eksik, birçok yordamı uygulamanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="6378d-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="6378d-106">Örneğin, 0.10.1 önce "Kimden 0.9.0'dan 0.10.1 için" yordamını takip etmek için sahip 0.11.0 sonra "Kimden 0.10.1 0.11.0 için" yordamı geçiş ise.</span><span class="sxs-lookup"><span data-stu-id="6378d-106">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span></span>

## <a name="from-200-to-330"></a><span data-ttu-id="6378d-107">2.0.0 3.3.0 için</span><span class="sxs-lookup"><span data-stu-id="6378d-107">From 2.0.0 to 3.3.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="6378d-108">Test günlükleri</span><span class="sxs-lookup"><span data-stu-id="6378d-108">Test logs</span></span>
<span data-ttu-id="6378d-109">SDK'sı tarafından üretilen konsol günlükleri artık etkin/devre dışı bırakılmış/filtrelenmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="6378d-109">Console logs produced by the SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="6378d-110">Bu özelleştirmek için özellik güncelleştirme `EngagementAgent.Instance.TestLogEnabled` bulunan değer birine `EngagementTestLogLevel` numaralandırma, örneğin:</span><span class="sxs-lookup"><span data-stu-id="6378d-110">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-to-200"></a><span data-ttu-id="6378d-111">1.1.1 2.0.0 için</span><span class="sxs-lookup"><span data-stu-id="6378d-111">From 1.1.1 to 2.0.0</span></span>
<span data-ttu-id="6378d-112">Aşağıdaki nasıl Azure Mobile Engagement tarafından desteklenen bir uygulamaya Capptain SAS tarafından sunulan Capptain hizmetinden bir SDK tümleştirmesi geçirileceğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="6378d-112">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="6378d-113">Capptain ve Mobile Engagement aynı Hizmetleri değildir ve aşağıda verilen yordamı yalnızca istemci uygulaması geçirmek nasıl vurgular.</span><span class="sxs-lookup"><span data-stu-id="6378d-113">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="6378d-114">Uygulama SDK'yı geçirme verilerinizi Capptain sunucularından Mobile Engagement sunucuya geçişi YAPILMAZ</span><span class="sxs-lookup"><span data-stu-id="6378d-114">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="6378d-115">Önceki bir sürümünden geçiş yapıyorsanız, Lütfen 1.1.1 için önce geçirmenizi sonra aşağıdaki yordamı uygulamak için Capptain web sitesine bakın</span><span class="sxs-lookup"><span data-stu-id="6378d-115">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.1.1 first then apply the following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="6378d-116">Nuget paketi</span><span class="sxs-lookup"><span data-stu-id="6378d-116">Nuget package</span></span>
<span data-ttu-id="6378d-117">Değiştir **Capptain.WindowsPhone** tarafından **MicrosoftAzure.MobileEngagement** Nuget paketi.</span><span class="sxs-lookup"><span data-stu-id="6378d-117">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="6378d-118">Mobil katılım uygulama</span><span class="sxs-lookup"><span data-stu-id="6378d-118">Applying Mobile Engagement</span></span>
<span data-ttu-id="6378d-119">Terimi SDK kullanan `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="6378d-119">The SDK uses the term `Engagement`.</span></span> <span data-ttu-id="6378d-120">Projenizi bu değişikliği eşleşecek şekilde güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6378d-120">You need to update your project to match this change.</span></span>

<span data-ttu-id="6378d-121">Geçerli Capptain nuget paketini kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6378d-121">You need to uninstall your current Capptain nuget package.</span></span> <span data-ttu-id="6378d-122">Tüm değişikliklerinizi Capptain Kaynaklar klasörünü kaldırılacak göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="6378d-122">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="6378d-123">Bu dosyaları saklamak isterseniz bir kopyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6378d-123">If you want to keep those files then make a copy of them.</span></span>

<span data-ttu-id="6378d-124">Bundan sonra projenizde yeni Microsoft Azure katılım nuget paketini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6378d-124">After that, install the new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="6378d-125">Doğrudan üzerinde bulabilirsiniz [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span><span class="sxs-lookup"><span data-stu-id="6378d-125">You can find it directly on [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span></span> <span data-ttu-id="6378d-126">Bu eylem, katılım tarafından kullanılan tüm kaynakları dosyalarının yerini alır ve yeni katılım DLL, proje başvuruları ekler.</span><span class="sxs-lookup"><span data-stu-id="6378d-126">This action replaces all resources files used by Engagement and adds the new Engagement DLL to your project References.</span></span>

<span data-ttu-id="6378d-127">Proje başvuruları Capptain DLL başvurularını silerek temizlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6378d-127">You have to clean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="6378d-128">Bunu yapmazsanız Capptain sürümü çakışır ve hataları gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="6378d-128">If you do not make this, the version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="6378d-129">Capptain kaynakları özelleştirdiyseniz, eski dosyaları içeriğinizi kopyalayın ve bunları yeni katılım dosyalar yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="6378d-129">If you have customized Capptain resources, copy your old files content and paste them in the new Engagement files.</span></span> <span data-ttu-id="6378d-130">Xaml ve cs dosyaları güncelleştirilmesi gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6378d-130">Please note that both xaml and cs files have to be updated.</span></span>

<span data-ttu-id="6378d-131">Bu adımlar tamamlandığında yeni katılım başvurular tarafından eski Capptain başvuruları değiştirin yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="6378d-131">When those steps are completed you only have to replace old Capptain references by the new Engagement references.</span></span>

1. <span data-ttu-id="6378d-132">Tüm Capptain ad alanlarını güncelleştirilmesi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="6378d-132">All Capptain namespaces have to be updated.</span></span>
   
    <span data-ttu-id="6378d-133">Geçişten önce:</span><span class="sxs-lookup"><span data-stu-id="6378d-133">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="6378d-134">Geçişten sonra:</span><span class="sxs-lookup"><span data-stu-id="6378d-134">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="6378d-135">"Capptain" içeren tüm Capptain sınıfları "Katılım" içermelidir.</span><span class="sxs-lookup"><span data-stu-id="6378d-135">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="6378d-136">Geçişten önce:</span><span class="sxs-lookup"><span data-stu-id="6378d-136">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="6378d-137">Geçişten sonra:</span><span class="sxs-lookup"><span data-stu-id="6378d-137">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="6378d-138">XAML dosyaları için de Capptain ad alanı ve özniteliklerini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="6378d-138">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="6378d-139">Geçişten önce:</span><span class="sxs-lookup"><span data-stu-id="6378d-139">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="6378d-140">Geçişten sonra:</span><span class="sxs-lookup"><span data-stu-id="6378d-140">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="6378d-141">İçin diğer kaynaklar Capptain resimler gibi bunlar ayrıca "Katılım" kullanacak şekilde yeniden adlandırıldığı gerektiğini lütfen unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6378d-141">For the other resources like Capptain pictures, please note that they also have been renamed to use "Engagement".</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="6378d-142">Uygulama Kimliği / SDK anahtarı</span><span class="sxs-lookup"><span data-stu-id="6378d-142">Application ID / SDK Key</span></span>
<span data-ttu-id="6378d-143">Katılım bağlantı dizesini kullanır.</span><span class="sxs-lookup"><span data-stu-id="6378d-143">Engagement uses a connection string.</span></span> <span data-ttu-id="6378d-144">Mobile Engagement ile bir uygulama kimliği ve bir SDK anahtarı belirtmeniz gerekmez, yalnızca bir bağlantı dizesi belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6378d-144">You don't have to specify an application ID and an SDK key with Mobile Engagement, you only have to specify a connection string.</span></span> <span data-ttu-id="6378d-145">Bunu EngagementConfiguration dosyanızı ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6378d-145">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="6378d-146">Katılım yapılandırma ayarlanabilir, `Resources\EngagementConfiguration.xml` projenizin dosya.</span><span class="sxs-lookup"><span data-stu-id="6378d-146">The Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="6378d-147">Belirtmek için bu dosyayı düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="6378d-147">Edit this file to specify:</span></span>

* <span data-ttu-id="6378d-148">Uygulama bağlantı dizenizi etiketleri arasına `<connectionString>` ve `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="6378d-148">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="6378d-149">Bunun yerine çalışma zamanında belirtmek istiyorsanız, katılım aracı başlatmadan önce aşağıdaki yöntemini çağırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6378d-149">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="6378d-150">Bağlantı dizesi, uygulamanız için Azure Klasik Portalı'nda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="6378d-150">The connection string for your application is displayed in the Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="6378d-151">Öğe adı değişikliği</span><span class="sxs-lookup"><span data-stu-id="6378d-151">Items name change</span></span>
<span data-ttu-id="6378d-152">Tüm öğeleri adlı *capptain* adlandırılmış *engagement*.</span><span class="sxs-lookup"><span data-stu-id="6378d-152">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="6378d-153">Benzer şekilde *Capptain* için *Engagement*.</span><span class="sxs-lookup"><span data-stu-id="6378d-153">Similarly for *Capptain* to *Engagement*.</span></span>

<span data-ttu-id="6378d-154">Yaygın olarak kullanılan Capptain öğeleri örnekleri:</span><span class="sxs-lookup"><span data-stu-id="6378d-154">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="6378d-155">Şimdi EngagementConfiguration adlı CapptainConfiguration</span><span class="sxs-lookup"><span data-stu-id="6378d-155">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="6378d-156">Şimdi EngagementAgent adlı CapptainAgent</span><span class="sxs-lookup"><span data-stu-id="6378d-156">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="6378d-157">Şimdi EngagementReach adlı CapptainReach</span><span class="sxs-lookup"><span data-stu-id="6378d-157">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="6378d-158">Şimdi EngagementHttpConfig adlı CapptainHttpConfig</span><span class="sxs-lookup"><span data-stu-id="6378d-158">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="6378d-159">Şimdi GetEngagementPageName adlı GetCapptainPageName</span><span class="sxs-lookup"><span data-stu-id="6378d-159">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="6378d-160">Ayrıca etkiler yeniden adlandırmak Not yöntemleri geçersiz kılındı.</span><span class="sxs-lookup"><span data-stu-id="6378d-160">Note that rename also affects overridden methods.</span></span>

