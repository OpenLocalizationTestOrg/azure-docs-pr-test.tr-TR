---
title: "aaaWindows Phone Silverlight Reach SDK tümleştirmesi"
description: "Nasıl tooIntegrate Azure Mobile Engagement Reach Windows Phone Silverlight uygulamaları ile"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d3516a6b-db9f-4cdb-a475-4148edf81af1
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 09c8767216e11963c5c600755ab8d4d11cd92034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-reach-sdk-integration"></a><span data-ttu-id="1dd71-103">Windows Phone Silverlight Reach SDK tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="1dd71-103">Windows Phone Silverlight Reach SDK Integration</span></span>
<span data-ttu-id="1dd71-104">Merhaba tümleştirme hello yordamını izleyin [Windows Phone Silverlight Engagement SDK tümleştirmesi](mobile-engagement-windows-phone-integrate-engagement.md) bu kılavuz aşağıdaki önce.</span><span class="sxs-lookup"><span data-stu-id="1dd71-104">You must follow hello integration procedure described in hello [Windows Phone Silverlight Engagement SDK Integration](mobile-engagement-windows-phone-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a><span data-ttu-id="1dd71-105">Windows Phone Silverlight projenize Hello Engagement Reach SDK'sı ekleme</span><span class="sxs-lookup"><span data-stu-id="1dd71-105">Embed hello Engagement Reach SDK into your Windows Phone Silverlight project</span></span>
<span data-ttu-id="1dd71-106">Herhangi bir şey yok tooadd.</span><span class="sxs-lookup"><span data-stu-id="1dd71-106">You do not have anything tooadd.</span></span> <span data-ttu-id="1dd71-107">`EngagementReach`Projenizde başvuruları ve kaynak zaten var.</span><span class="sxs-lookup"><span data-stu-id="1dd71-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="1dd71-108">Hello bulunan görüntüleri özelleştirebilirsiniz `Resources` klasörü projenizin, özellikle hello marka simgesini (Bu varsayılan toohello katılım simge).</span><span class="sxs-lookup"><span data-stu-id="1dd71-108">You can customize images located in hello `Resources` folder of your project, especially hello brand icon (that default toohello Engagement icon).</span></span>
> 
> 

## <a name="add-hello-capabilities"></a><span data-ttu-id="1dd71-109">Merhaba yetenekleri ekleme</span><span class="sxs-lookup"><span data-stu-id="1dd71-109">Add hello capabilities</span></span>
<span data-ttu-id="1dd71-110">Merhaba Engagement Reach SDK'SININ bazı ek yetenekler gerekir.</span><span class="sxs-lookup"><span data-stu-id="1dd71-110">hello Engagement Reach SDK needs some additional capabilities.</span></span>

<span data-ttu-id="1dd71-111">Açık, `WMAppManifest.xml` dosya ve yetenekleri aşağıdaki o hello bildirildiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="1dd71-111">Open your `WMAppManifest.xml` file and be sure that hello following capabilities are declared:</span></span>

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

<span data-ttu-id="1dd71-112">Merhaba ilk hello MPNS hizmet tooallow hello görüntüsünü bildirim tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1dd71-112">hello first one is used by hello MPNS service tooallow hello display of toast notification.</span></span> <span data-ttu-id="1dd71-113">Merhaba ikinci kullanılan tooembed tarayıcı görev hello SDK içine adrestir.</span><span class="sxs-lookup"><span data-stu-id="1dd71-113">hello second one is used tooembed a browser task into hello SDK.</span></span>

<span data-ttu-id="1dd71-114">Merhaba Düzenle `WMAppManifest.xml` dosya ve hello ekleyin `<Capabilities />` etiketi:</span><span class="sxs-lookup"><span data-stu-id="1dd71-114">Edit hello `WMAppManifest.xml` file and add inside hello `<Capabilities />` tag :</span></span>

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-hello-microsoft-push-notification-service"></a><span data-ttu-id="1dd71-115">Merhaba Microsoft anında bildirim hizmeti etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="1dd71-115">Enable hello Microsoft Push Notification Service</span></span>
<span data-ttu-id="1dd71-116">Sipariş toouse hello içinde **Microsoft anında bildirim hizmeti** (MPNS adlandırılır), `WMAppManifest.xml` dosya olmalıdır bir `<App />` ile etiketi bir `Publisher` özniteliğini toohello projenizin adını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1dd71-116">In order toouse hello **Microsoft Push Notification Service** (referred as MPNS) your `WMAppManifest.xml` file must have an `<App />` tag with a `Publisher` attribute set toohello name of your project.</span></span>

## <a name="initialize-hello-engagement-reach-sdk"></a><span data-ttu-id="1dd71-117">Merhaba Engagement Reach SDK'sını başlatma</span><span class="sxs-lookup"><span data-stu-id="1dd71-117">Initialize hello Engagement Reach SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="1dd71-118">Katılım yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1dd71-118">Engagement configuration</span></span>
<span data-ttu-id="1dd71-119">Merhaba katılım yapılandırma hello Merkezi `Resources\EngagementConfiguration.xml` projenizin dosya.</span><span class="sxs-lookup"><span data-stu-id="1dd71-119">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="1dd71-120">Bu dosya toospecify ulaşma yapılandırmasını düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="1dd71-120">Edit this file toospecify reach configuration :</span></span>

* <span data-ttu-id="1dd71-121">*İsteğe bağlı*, hello yerel gönderim (MPNS) etkin olup olmadığını veya arasında değil belirtmek `<enableNativePush>` ve `</enableNativePush>` etiketleri (`true` varsayılan olarak).</span><span class="sxs-lookup"><span data-stu-id="1dd71-121">*Optional*, indicate whether hello native push (MPNS) is activated or not between `<enableNativePush>` and `</enableNativePush>` tags, (`true` by default).</span></span>
* <span data-ttu-id="1dd71-122">*İsteğe bağlı*, arasında hello itme kanal hello adını belirtmek `<channelName>` ve `</channelName>` etiketleri, sağlar hello uygulamanız şu anda kullanın veya bu alanı boş bırakın, aynı.</span><span class="sxs-lookup"><span data-stu-id="1dd71-122">*Optional*, indicate hello name of hello push channel between `<channelName>` and `</channelName>` tags, provide hello same that your application may currently use or leave it empty.</span></span>

<span data-ttu-id="1dd71-123">Çalışma zamanında, bunun yerine, çağırabilirsiniz hello aşağıdaki toospecify istiyorsanız yöntemi hello katılım aracı başlatmadan önce:</span><span class="sxs-lookup"><span data-stu-id="1dd71-123">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization :</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    engagementConfiguration.Reach.EnableNativePush = true;                  
    /* [Optional] whether hello native push (MPNS) is activated or not. */

    engagementConfiguration.Reach.ChannelName = "YOUR_PUSH_CHANNEL_NAME";   
    /* [Optional] Provide hello same channel name that your application may currently use. */

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

> [!TIP]
> <span data-ttu-id="1dd71-124">Merhaba MPNS anında iletme kanal uygulamanızın hello adını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1dd71-124">You can specify hello name of hello MPNS push channel of your application.</span></span> <span data-ttu-id="1dd71-125">Varsayılan olarak, katılım hello AppID üzerinde tabanlı bir ad oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1dd71-125">By default, Engagement creates a name based on hello appId.</span></span> <span data-ttu-id="1dd71-126">Katılım dışında toouse hello itme kanal düşünüyorsanız dışında hiçbir gerek toospecify hello adına kendiniz sahip.</span><span class="sxs-lookup"><span data-stu-id="1dd71-126">You have no need toospecify hello name yourself, except if you plan toouse hello push channel outside of Engagement.</span></span>
> 
> 

### <a name="engagement-initialization"></a><span data-ttu-id="1dd71-127">Katılım başlatma</span><span class="sxs-lookup"><span data-stu-id="1dd71-127">Engagement initialization</span></span>
<span data-ttu-id="1dd71-128">Merhaba değiştirme `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="1dd71-128">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="1dd71-129">Tooyour ekleme `using` deyimleri:</span><span class="sxs-lookup"><span data-stu-id="1dd71-129">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="1dd71-130">INSERT `EngagementReach.Instance.Init` hemen sonra `EngagementAgent.Instance.Init` içinde `Application_Launching` :</span><span class="sxs-lookup"><span data-stu-id="1dd71-130">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in `Application_Launching` :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* <span data-ttu-id="1dd71-131">INSERT `EngagementReach.Instance.OnActivated` hello içinde `Application_Activated` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="1dd71-131">Insert `EngagementReach.Instance.OnActivated` in hello `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> <span data-ttu-id="1dd71-132">Merhaba `EngagementReach.Instance.Init` adanmış bir iş parçacığı çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="1dd71-132">hello `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="1dd71-133">Toodo sahip değil, kendiniz.</span><span class="sxs-lookup"><span data-stu-id="1dd71-133">You do not have toodo it yourself.</span></span>
> 
> 

## <a name="app-store-submission-considerations"></a><span data-ttu-id="1dd71-134">Uygulama mağazası gönderimi dikkat edilecek noktalar</span><span class="sxs-lookup"><span data-stu-id="1dd71-134">App store submission considerations</span></span>
<span data-ttu-id="1dd71-135">Microsoft, hello anında iletme bildirimleri kullanırken bazı kuralları uygular:</span><span class="sxs-lookup"><span data-stu-id="1dd71-135">Microsoft imposes some rules when using hello push notifications:</span></span>

<span data-ttu-id="1dd71-136">Merhaba Microsoft gelen [uygulama ilkeleri] belgeleri, bölüm 2.9:</span><span class="sxs-lookup"><span data-stu-id="1dd71-136">From hello Microsoft [Application Policies] documentation, section 2.9:</span></span>

1) <span data-ttu-id="1dd71-137">Merhaba kullanıcı tooaccept tooreceive anında iletme bildirimleri kaldırmasını isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1dd71-137">You must ask hello user tooaccept tooreceive push notifications.</span></span> <span data-ttu-id="1dd71-138">Ardından, ayarlarınızda bir şekilde toodisable hello anında iletme bildirimleri ekleme.</span><span class="sxs-lookup"><span data-stu-id="1dd71-138">Then, in your settings, add a way toodisable hello push notifications.</span></span>

<span data-ttu-id="1dd71-139">Merhaba EngagementReach nesne sağlayan iki yöntem toomanage hello içinde/opt-çevirin, `EnableNativePush()` ve `DisableNativePush()`.</span><span class="sxs-lookup"><span data-stu-id="1dd71-139">hello EngagementReach object provides two methods toomanage hello opt-in/opt-out, `EnableNativePush()` and `DisableNativePush()`.</span></span> <span data-ttu-id="1dd71-140">, Örneğin, bir seçenek hello ayarları değiştir toodisable ile oluşturduğunuz veya MPNS etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="1dd71-140">You could, for example, create an option in hello settings with a toggle toodisable or enable MPNS.</span></span>

<span data-ttu-id="1dd71-141">Merhaba katılım yapılandırma yoluyla toodeactivate MPNS karar verebilirsiniz\<windows phone-sdk-reach-yapılandırma\>.</span><span class="sxs-lookup"><span data-stu-id="1dd71-141">You can also decide toodeactivate MPNS through hello Engagement configuration\<windows-phone-sdk-reach-configuration\>.</span></span>

> <span data-ttu-id="1dd71-142">2.9.1) hello uygulamayı sağlanan hello bildirimleri toobe ilk tanımlayan gerekir ve **hello kullanıcının express iznini (katılımı) elde**, ve **hangi hello kullanıcı kabul alma dışında bir mekanizma sağlamanız gerekir anında iletme bildirimleri**.</span><span class="sxs-lookup"><span data-stu-id="1dd71-142">2.9.1) hello application must first describe hello notifications toobe provided and **obtain hello user’s express permission (opt-in)**, and **must provide a mechanism through which hello user can opt out of receiving push notifications**.</span></span> <span data-ttu-id="1dd71-143">Sağlanan Hello Microsoft anında bildirim hizmeti kullanarak tüm bildirimleri hello sağlanan açıklama toohello kullanıcı ile tutarlı olmalıdır ve tüm ile uymalıdır geçerli [uygulama ilkeleri] [ Content Policies]ve [belirli uygulama türleri için ek gereksinimler].</span><span class="sxs-lookup"><span data-stu-id="1dd71-143">All notifications provided using hello Microsoft Push Notification Service must be consistent with hello description provided toohello user and must comply with all applicable [Application Policies][Content Policies] and [Additional Requirements for Specific Application Types].</span></span>
> 
> 

2) <span data-ttu-id="1dd71-144">Çok fazla anında iletme bildirimleri kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1dd71-144">You should not use too many push notifications.</span></span> <span data-ttu-id="1dd71-145">Katılım bildirimleri sizin için işler.</span><span class="sxs-lookup"><span data-stu-id="1dd71-145">Engagement will handle notifications for you.</span></span>

> <span data-ttu-id="1dd71-146">2.9.2) hello uygulama ve hello Microsoft anında bildirim hizmeti kullanımı değil aşırı ağ kapasitesi veya bant genişliği hello Microsoft anında bildirim hizmeti veya kullanmanız gerekir, aksi takdirde unduly bir Windows Phone veya diğer Microsoft cihaz veya hizmet yük aşırı ile anında iletme bildirimleri, Microsoft tarafından makul kendi takdirine bağlı olarak belirlenen ve değil zarar veya gerekir herhangi Microsoft ağları veya sunucuları veya tüm üçüncü taraf sunucular ya da ağlara bağlı toohello Microsoft anında bildirim hizmeti ile müdahale.</span><span class="sxs-lookup"><span data-stu-id="1dd71-146">2.9.2) hello application and its use of hello Microsoft Push Notification Service must not excessively use network capacity or bandwidth of hello Microsoft Push Notification Service, or otherwise unduly burden a Windows Phone or other Microsoft device or service with excessive push notifications, as determined by Microsoft in its reasonable discretion, and must not harm or interfere with any Microsoft networks or servers or any third party servers or networks connected toohello Microsoft Push Notification Service.</span></span>
> 
> 

3) <span data-ttu-id="1dd71-147">MPNS toosend criticals bilgi kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="1dd71-147">Do not rely on MPNS toosend criticals information.</span></span> <span data-ttu-id="1dd71-148">Katılım MPNS, kullanır, bu nedenle bu kural katılım hello içinde ön uç oluşturulan hello kampanyaları için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1dd71-148">Engagement uses MPNS, so this rule also applies for hello campaigns created inside hello Engagement front-end.</span></span>

> <span data-ttu-id="1dd71-149">2.9.3) Microsoft anında bildirim hizmeti, kritik veya aksi takdirde görev kullanılan toosend bildirimleri olmayabilir hello yaşam veya sınırlaması kritik bildirimleri ilgili tooa tıbbi cihaz veya koşulu dahil olmak üzere ölüm önemlidir etkileyen.</span><span class="sxs-lookup"><span data-stu-id="1dd71-149">2.9.3) hello Microsoft Push Notification Service may not be used toosend notifications that are mission critical or otherwise could affect matters of life or death, including without limitation critical notifications related tooa medical device or condition.</span></span> <span data-ttu-id="1dd71-150">MICROSOFT açıkça reddeder herhangi garanti olduğunu hello kullan, hello MICROSOFT anında bildirim hizmeti veya teslim, MICROSOFT anında bildirim hizmeti bildirimleri olacak olması kesintisiz hata boş veya aksi halde garanti tooOCCUR ON A gerçek zamanlı olarak.</span><span class="sxs-lookup"><span data-stu-id="1dd71-150">MICROSOFT EXPRESSLY DISCLAIMS ANY WARRANTIES THAT hello USE OF hello MICROSOFT PUSH NOTIFICATION SERVICE OR DELIVERY OF MICROSOFT PUSH NOTIFICATION SERVICE NOTIFICATIONS WILL BE UNINTERRUPTED, ERROR FREE, OR OTHERWISE GUARANTEED tooOCCUR ON A REAL-TIME BASIS.</span></span>
> 
> 

<span data-ttu-id="1dd71-151">**Bu öneriler dikkate almaz, uygulamanızın hello doğrulama işlemi geçer garanti edemez.**</span><span class="sxs-lookup"><span data-stu-id="1dd71-151">**We cannot guarantee that your application will pass hello validation process if you do not respect these recommendations.**</span></span>

## <a name="handle-data-push-optional"></a><span data-ttu-id="1dd71-152">Veri gönderimi (isteğe bağlı) işleme</span><span class="sxs-lookup"><span data-stu-id="1dd71-152">Handle data push (optional)</span></span>
<span data-ttu-id="1dd71-153">Uygulama toobe mümkün tooreceive ulaşma veri gönderimleri isterseniz, iki olayları hello EngagementReach sınıfı tooimplement vardır:</span><span class="sxs-lookup"><span data-stu-id="1dd71-153">If you want your application toobe able tooreceive Reach data pushes, you have tooimplement two events of hello EngagementReach class:</span></span>

    EngagementReach.Instance.DataPushStringReceived += (body) =>
    {
       Debug.WriteLine("String data push message received: " + body);
       return true;
    };

    EngagementReach.Instance.DataPushBase64Received += (decodedBody, encodedBody) =>
    {
       Debug.WriteLine("Base64 data push message received: " + encodedBody);
       // Do something useful with decodedBody like updating an image view
       return true;
    };

<span data-ttu-id="1dd71-154">Her yöntem döndürür bir Boole değeri, bu hello geri çağırma görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1dd71-154">You can see that hello callback of each method returns a boolean.</span></span> <span data-ttu-id="1dd71-155">Katılım hello veri gönderimi gönderdikten sonra bir geri bildirim tooits arka uç gönderir.</span><span class="sxs-lookup"><span data-stu-id="1dd71-155">Engagement sends a feedback tooits back-end after dispatching hello data push.</span></span> <span data-ttu-id="1dd71-156">Merhaba geri çağırma false değeri döndürülürse, hello `exit` geri bildirim gönder olacaktır.</span><span class="sxs-lookup"><span data-stu-id="1dd71-156">If hello callback returns false, hello `exit` feedback will be send.</span></span> <span data-ttu-id="1dd71-157">Aksi durumda olur `action`.</span><span class="sxs-lookup"><span data-stu-id="1dd71-157">Otherwise, it will be `action`.</span></span> <span data-ttu-id="1dd71-158">Geri arama yok hello olaylarını ayarlarsanız hello `drop` geri bildirim tooEngagement döndürülecek.</span><span class="sxs-lookup"><span data-stu-id="1dd71-158">If no callback is set for hello events, hello `drop` feedback will be returned tooEngagement.</span></span>

> [!WARNING]
> <span data-ttu-id="1dd71-159">Katılım mümkün tooreceive katları geribildirimler veri gönderimi için değil.</span><span class="sxs-lookup"><span data-stu-id="1dd71-159">Engagement is not able tooreceive multiples feedbacks for a data push.</span></span> <span data-ttu-id="1dd71-160">Bir olayda birçok işleyicileri tooset planlıyorsanız, hello geri bildirim sonuncu gönderilen toohello karşılık unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1dd71-160">If you plan tooset several handlers on an event, be aware that hello feedback will correspond toohello last one sent.</span></span> <span data-ttu-id="1dd71-161">Bu durumda, tooalways öneririz hello kafa karıştırıcı geri bildirim hello ön uç sahip aynı değeri tooavoid döndürür.</span><span class="sxs-lookup"><span data-stu-id="1dd71-161">In this case, we recommend tooalways returns hello same value tooavoid having confusing feedback on hello front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="1dd71-162">(İsteğe bağlı) kullanıcı arabirimini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="1dd71-162">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="1dd71-163">İlk adım</span><span class="sxs-lookup"><span data-stu-id="1dd71-163">First step</span></span>
<span data-ttu-id="1dd71-164">Biz toocustomize hello ulaşma kullanıcı Arabirimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1dd71-164">We allow you toocustomize hello reach UI.</span></span>

<span data-ttu-id="1dd71-165">toodo bu nedenle, toocreate hello öğesinin bir alt kümesi olan `EngagementReachHandler` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="1dd71-165">toodo so, you have toocreate a subclass of hello `EngagementReachHandler` class.</span></span>

<span data-ttu-id="1dd71-166">**Örnek kod:**</span><span class="sxs-lookup"><span data-stu-id="1dd71-166">**Sample Code :**</span></span>

    using Microsoft.Azure.Engagement;

    namespace Example
    {
       internal class ExampleReachHandler : EngagementReachHandler
       {
          // Override EngagementReachHandler methods depending on your needs
       }
    }

<span data-ttu-id="1dd71-167">Sonra hello Merhaba içeriğine ayarlayın `EngagementReach.Instance.Handler` özel nesnesinde ile alan, `App.xaml.cs` hello sınıfında `Application_Launching` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1dd71-167">Then, set hello content of hello `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within hello `Application_Launching` method.</span></span>

<span data-ttu-id="1dd71-168">**Örnek kod:**</span><span class="sxs-lookup"><span data-stu-id="1dd71-168">**Sample Code :**</span></span>

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> <span data-ttu-id="1dd71-169">Varsayılan olarak, kendi uyarlamasını katılım kullanır `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="1dd71-169">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span> <span data-ttu-id="1dd71-170">Toocreate yoksa, kendi ve bunu yaparsanız, her yöntemi toooverride yok.</span><span class="sxs-lookup"><span data-stu-id="1dd71-170">You don't have toocreate your own, and if you do so, you don't have toooverride every method.</span></span> <span data-ttu-id="1dd71-171">tooselect hello katılım temel nesne Hello varsayılan davranıştır.</span><span class="sxs-lookup"><span data-stu-id="1dd71-171">hello default behavior is tooselect hello Engagement base object.</span></span>
> 
> 

### <a name="layouts"></a><span data-ttu-id="1dd71-172">Düzenleri</span><span class="sxs-lookup"><span data-stu-id="1dd71-172">Layouts</span></span>
<span data-ttu-id="1dd71-173">Varsayılan olarak, ulaşma hello DLL toodisplay hello bildirimleri ve sayfalarının katıştırılmış hello kaynakları kullanır.</span><span class="sxs-lookup"><span data-stu-id="1dd71-173">By default, Reach will use hello embedded resources of hello DLL toodisplay hello notifications and pages.</span></span>

<span data-ttu-id="1dd71-174">Ancak, kendi kaynaklarını tooreflect toouse karar verebilirsiniz, marka bu bileşenlerde.</span><span class="sxs-lookup"><span data-stu-id="1dd71-174">However, you can decide toouse your own resources tooreflect your brand in these components.</span></span>

<span data-ttu-id="1dd71-175">Geçersiz kılabilirsiniz `EngagementReachHandler` alt tootell katılım toouse yöntemleri, düzenler:</span><span class="sxs-lookup"><span data-stu-id="1dd71-175">You can override `EngagementReachHandler` methods in your subclass tootell Engagement toouse your layouts :</span></span>

<span data-ttu-id="1dd71-176">**Örnek kod:**</span><span class="sxs-lookup"><span data-stu-id="1dd71-176">**Sample Code :**</span></span>

    // In your subclass of EngagementReachHandler

    public override string GetTextViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetWebViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetPollUri()
    {
       // return hello path of your own xaml
    }

    public override EngagementNotificationView CreateNotification(EngagementNotificationViewModel viewModel)
    {
       // return a new instance of your own notification
    }

> [!TIP]
> <span data-ttu-id="1dd71-177">Merhaba `CreateNotification` yöntemi null dönebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1dd71-177">hello `CreateNotification` method can return null.</span></span> <span data-ttu-id="1dd71-178">Merhaba bildirim görüntülenmez ve hello reach kampanya bırakılacak.</span><span class="sxs-lookup"><span data-stu-id="1dd71-178">hello notification won't be displayed and hello reach campaign will be dropped.</span></span>
> 
> 

<span data-ttu-id="1dd71-179">toosimplify düzeni uygulamanızı ayrıca kodunuz için temel olarak hizmet verebilir kendi xaml sağlıyoruz.</span><span class="sxs-lookup"><span data-stu-id="1dd71-179">toosimplify your layout implementation, we also provide our own xaml which can serve as a basis for your code.</span></span> <span data-ttu-id="1dd71-180">Merhaba Engagement SDK'sı arşivindeki bulundukları (/ src/reach /).</span><span class="sxs-lookup"><span data-stu-id="1dd71-180">They are located in hello Engagement SDK archive (/src/reach/).</span></span>

> [!WARNING]
> <span data-ttu-id="1dd71-181">Merhaba kullandığımız tam aynı olanlardır sağladığımız hello kaynakları.</span><span class="sxs-lookup"><span data-stu-id="1dd71-181">hello sources that we provide are hello exact same ones that we use.</span></span> <span data-ttu-id="1dd71-182">Bu nedenle toomodify istiyorsanız, bunları doğrudan yok toochange hello ad alanı unutursanız ve ad hello.</span><span class="sxs-lookup"><span data-stu-id="1dd71-182">So if you want toomodify them directly, don't forget toochange hello namespace and hello name.</span></span>
> 
> 

### <a name="notification-position"></a><span data-ttu-id="1dd71-183">Bildirim konumu</span><span class="sxs-lookup"><span data-stu-id="1dd71-183">Notification position</span></span>
<span data-ttu-id="1dd71-184">Varsayılan olarak, bir uygulama bildirimi hello sayfanın sol tarafında Merhaba uygulaması görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="1dd71-184">By default, an in-app notification is displayed at hello bottom left side of hello application.</span></span> <span data-ttu-id="1dd71-185">Merhaba geçersiz kılarak bu davranışı değiştirebilirsiniz `GetNotificationPosition` hello yöntemi `EngagementReachHandler` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="1dd71-185">You can change this behavior by overriding hello `GetNotificationPosition` method of hello `EngagementReachHandler` object.</span></span>

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of hello EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

<span data-ttu-id="1dd71-186">Şu anda hello arasında seçim yapabilirsiniz `BOTTOM` (varsayılan) ve `TOP` konumlar.</span><span class="sxs-lookup"><span data-stu-id="1dd71-186">Currently, you can choose between hello `BOTTOM` (default) and `TOP` positions.</span></span>

### <a name="launch-message"></a><span data-ttu-id="1dd71-187">İleti Başlatma</span><span class="sxs-lookup"><span data-stu-id="1dd71-187">Launch message</span></span>
<span data-ttu-id="1dd71-188">Bir kullanıcı bir sistem bildirimi (bildirim) tıkladığında, katılım başlatır uygulama Merhaba, yük hello Merhaba içeriğine iletileri gönderme ve kampanya karşılık gelen hello hello sayfayı görüntüleme.</span><span class="sxs-lookup"><span data-stu-id="1dd71-188">When a user clicks on a system notification (a toast), Engagement launches hello app, load hello content of hello push messages, and display hello page for hello corresponding campaign.</span></span>

<span data-ttu-id="1dd71-189">Merhaba başlatma (bağlı olarak, ağ hızına hello) hello sayfasının hello uygulama ve hello görüntüsünün arasında bir gecikme yoktur.</span><span class="sxs-lookup"><span data-stu-id="1dd71-189">There is a delay between hello launch of hello application and hello display of hello page (depending on hello speed of your network).</span></span>

<span data-ttu-id="1dd71-190">bir şey yüklüyor tooindicate toohello kullanıcı, bir ilerleme çubuğu veya bir İlerleme göstergesi gibi görsel bir bilgi sağlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="1dd71-190">tooindicate toohello user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="1dd71-191">Katılım kendisi, ancak sağladığı birkaç işleyicileri sizin için işleyemez.</span><span class="sxs-lookup"><span data-stu-id="1dd71-191">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="1dd71-192">tooimplement geri çağırma Merhaba, yapın:</span><span class="sxs-lookup"><span data-stu-id="1dd71-192">tooimplement hello callback, do:</span></span>

    /* hello application has launched and hello content is loading.
     * You should display an indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

    /* hello application has finished loading hello content and hello page
     * is about toobe displayed.
     * You should hide hello indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

    /* hello content has been loaded, but an error has occurred.
     * You can provide an information toohello user.
     * You should hide hello indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

<span data-ttu-id="1dd71-193">Merhaba geri çağırma ayarlayabileceğiniz, `Application_Launching` yöntemi, `App.xaml.cs` dosya, tercihen hello önce `EngagementReach.Instance.Init()` çağırın.</span><span class="sxs-lookup"><span data-stu-id="1dd71-193">You can set hello callback in your `Application_Launching` method of your `App.xaml.cs` file, preferably before hello `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="1dd71-194">Her işleyici hello tarafından kullanıcı Arabirimi iş parçacığı denir.</span><span class="sxs-lookup"><span data-stu-id="1dd71-194">Each handler is called by hello UI Thread.</span></span> <span data-ttu-id="1dd71-195">MessageBox veya bir şey UI ilgili kullanırken tooworry yok.</span><span class="sxs-lookup"><span data-stu-id="1dd71-195">You do not have tooworry when using a MessageBox or something UI-related.</span></span>
> 
> 

[uygulama ilkeleri]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
[belirli uygulama türleri için ek gereksinimler]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx

