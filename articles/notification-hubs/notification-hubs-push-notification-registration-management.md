---
title: "Kayıt Yönetimi"
description: "Bu konuda, anında iletme bildirimleri almak için notification hubs ile cihazları kaydetmek açıklanmaktadır."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: fd0ee230-132c-4143-b4f9-65cef7f463a1
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: a1a349150ef4c7837932706f0c4fcc8d022ec7ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="registration-management"></a><span data-ttu-id="27300-103">Kayıt yönetimi</span><span class="sxs-lookup"><span data-stu-id="27300-103">Registration management</span></span>
## <a name="overview"></a><span data-ttu-id="27300-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="27300-104">Overview</span></span>
<span data-ttu-id="27300-105">Bu konuda, anında iletme bildirimleri almak için notification hubs ile cihazları kaydetmek açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="27300-105">This topic explains how to register devices with notification hubs in order to receive push notifications.</span></span> <span data-ttu-id="27300-106">Konu kayıtlar yüksek düzeyde açıklanır ve cihazlar kaydettirmek için iki ana modeli sunar: bildirim hub'ına doğrudan CİHAZDAN kaydetme ve bir uygulama arka ucu kaydediliyor.</span><span class="sxs-lookup"><span data-stu-id="27300-106">The topic describes registrations at a high level, then introduces the two main patterns for registering devices: registering from the device directly to the notification hub, and registering through an application backend.</span></span> 

## <a name="what-is-device-registration"></a><span data-ttu-id="27300-107">Cihaz kaydı nedir</span><span class="sxs-lookup"><span data-stu-id="27300-107">What is device registration</span></span>
<span data-ttu-id="27300-108">Bildirim hub'ı ile cihaz kaydı kullanarak gerçekleştirilir bir **kayıt** veya **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="27300-108">Device registration with a Notification Hub is accomplished using a **Registration** or **Installation**.</span></span>

#### <a name="registrations"></a><span data-ttu-id="27300-109">Kayıtlar</span><span class="sxs-lookup"><span data-stu-id="27300-109">Registrations</span></span>
<span data-ttu-id="27300-110">Bir kaydı bir aygıt için Platform bildirim hizmeti (PNS) tanıtıcı etiketleri ve büyük olasılıkla bir şablon ile ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="27300-110">A registration associates the Platform Notification Service (PNS) handle for a device with tags and possibly a template.</span></span> <span data-ttu-id="27300-111">PNS tanıtıcısını ChannelURI, cihaz belirteci veya GCM kayıt kimliği olabilir.</span><span class="sxs-lookup"><span data-stu-id="27300-111">The PNS handle could be a ChannelURI, device token, or GCM registration id.</span></span> <span data-ttu-id="27300-112">Etiketler cihaz tanıtıcılarını doğru kümesine bildirimleri yönlendirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="27300-112">Tags are used to route notifications to the correct set of device handles.</span></span> <span data-ttu-id="27300-113">Daha fazla bilgi için bkz: [Yönlendirme ve etiket ifadeleri](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="27300-113">For more information, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span> <span data-ttu-id="27300-114">Şablonları kayıt başına dönüştürme uygulamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="27300-114">Templates are used to implement per-registration transformation.</span></span> <span data-ttu-id="27300-115">Daha fazla bilgi için bkz: [şablonları](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="27300-115">For more information, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>

#### <a name="installations"></a><span data-ttu-id="27300-116">Yüklemeleri</span><span class="sxs-lookup"><span data-stu-id="27300-116">Installations</span></span>
<span data-ttu-id="27300-117">Yüklemesi geliştirilmiş olabilir itme paketi içeren kayıt ilgili özellikler.</span><span class="sxs-lookup"><span data-stu-id="27300-117">An Installation is an enhanced registration that includes a bag of push related properties.</span></span> <span data-ttu-id="27300-118">Bunu aygıtlarınızı kaydetme en son ve en iyi yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="27300-118">It is the latest and best approach to registering your devices.</span></span> <span data-ttu-id="27300-119">Ancak, istemci tarafı .NET SDK'sı tarafından desteklenmiyor ([Notification Hub SDK'sı arka uç işlemleri için](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) henüz dağıtmadığı.</span><span class="sxs-lookup"><span data-stu-id="27300-119">However, it is not supported by client side .NET SDK ([Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) as of yet.</span></span>  <span data-ttu-id="27300-120">Bu istemci CİHAZDAN kaydediyorsunuz varsa kullanılacak anlamına gelir [Notification Hubs REST API'si](https://msdn.microsoft.com/library/mt621153.aspx) yaklaşım yüklemelerini desteklemek için.</span><span class="sxs-lookup"><span data-stu-id="27300-120">This means if you are registering from the client device itself, you would have to use the [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx) approach to support installations.</span></span> <span data-ttu-id="27300-121">Arka uç hizmeti kullanıyorsanız, kullanabilmek için olmalısınız [Notification Hub SDK'sı arka uç işlemleri için](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="27300-121">If you are using a backend service, you should be able to use [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="27300-122">Yüklemeleri kullanmanın önemli avantajlarından bazıları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="27300-122">The following are some key advantages to using installations:</span></span>

* <span data-ttu-id="27300-123">Oluşturma veya bir yüklemeyi güncelleştirme ıdempotent tam değil.</span><span class="sxs-lookup"><span data-stu-id="27300-123">Creating or updating an installation is fully idempotent.</span></span> <span data-ttu-id="27300-124">Bu nedenle tüm yinelenen kayıtları endişeniz olmadan deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27300-124">So you can retry it without any concerns about duplicate registrations.</span></span>
* <span data-ttu-id="27300-125">Yükleme modeli tek tek iter - belirli bir aygıtı hedefleme yapılacağı kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="27300-125">The installation model makes it easy to do individual pushes - targeting specific device.</span></span> <span data-ttu-id="27300-126">Bir sistem etiketi **"$InstallationId: [InstallationID]"** her bağlı yükleme kaydı otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="27300-126">A system tag **"$InstallationId:[installationId]"** is automatically added with each installation based registration.</span></span> <span data-ttu-id="27300-127">Bu nedenle hiçbir ek kodlama yapmak zorunda kalmadan belirli bir aygıt hedeflemek için bu etikete gönderme çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27300-127">So you can call a send to this tag to target a specific device without having to do any additional coding.</span></span>
* <span data-ttu-id="27300-128">Yüklemeleri kullanarak, kısmi kayıt güncelleştirmeler yapmak de sağlar.</span><span class="sxs-lookup"><span data-stu-id="27300-128">Using installations also enables you to do partial registration updates.</span></span> <span data-ttu-id="27300-129">Bir düzeltme eki yöntemi kullanılarak ile kısmi güncelleştirme yüklemesinin istenilen [JSON düzeltme eki standart](https://tools.ietf.org/html/rfc6902).</span><span class="sxs-lookup"><span data-stu-id="27300-129">The partial update of an installation is requested with a PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902).</span></span> <span data-ttu-id="27300-130">Kayıt etiketlerini güncelleştirmek istediğinizde özellikle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="27300-130">This is particularly useful when you want to update tags on the registration.</span></span> <span data-ttu-id="27300-131">Tüm kayıt çekmek ve önceki tüm etiketleri yeniden yeniden gerekmez.</span><span class="sxs-lookup"><span data-stu-id="27300-131">You don't have to pull down the entire registration and then resend all the previous tags again.</span></span>

<span data-ttu-id="27300-132">Bir yükleme içerebilir aşağıdaki özellikleri.</span><span class="sxs-lookup"><span data-stu-id="27300-132">An installation can contain the the following properties.</span></span> <span data-ttu-id="27300-133">Yükleme özellikleri bakın, tam bir listesi için [oluşturmak veya bir yükleme ile REST API üzerine](https://msdn.microsoft.com/library/azure/mt621153.aspx) veya [yükleme özellikleri](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) için.</span><span class="sxs-lookup"><span data-stu-id="27300-133">For a complete listing of the installation properties see, [Create or Overwrite an Installation with REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx) or [Installation Properties](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) for the .</span></span>

    // Example installation format to show some supported properties
    {
        installationId: "",
        expirationTime: "",
        tags: [],
        platform: "",
        pushChannel: "",
        ………
        templates: {
            "templateName1" : {
                body: "",
                tags: [] },
            "templateName2" : {
                body: "",
                // Headers are for Windows Store only
                headers: {
                    "X-WNS-Type": "wns/tile" }
                tags: [] }
        },
        secondaryTiles: {
            "tileId1": {
                pushChannel: "",
                tags: [],
                templates: {
                    "otherTemplate": {
                        bodyTemplate: "",
                        headers: {
                            ... }
                        tags: [] }
                }
            }
        }
    }



<span data-ttu-id="27300-134">Kayıtlar ve varsayılan olarak yüklemeleri artık dolacağını dikkate almak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="27300-134">It is important to note that registrations and installations by default no longer expire.</span></span>

<span data-ttu-id="27300-135">Kayıtlar ve yüklemeleri her cihaz/kanal için geçerli bir PNS tanıtıcısını içermelidir.</span><span class="sxs-lookup"><span data-stu-id="27300-135">Registrations and installations must contain a valid PNS handle for each device/channel.</span></span> <span data-ttu-id="27300-136">PNS tanıtıcılarını yalnızca aygıttaki istemci uygulamasında elde edilebilir olduğundan, istemci uygulaması ile bir cihazda doğrudan kaydetmek için bir düzen yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="27300-136">Because PNS handles can only be obtained in a client app on the device, one pattern is to register directly on that device with the client app.</span></span> <span data-ttu-id="27300-137">Diğer taraftan, güvenlikle ilgili önemli noktalar ve etiketler için ilgili iş mantığı, uygulama arka ucunu cihaz kaydında yönetmenizi gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="27300-137">On the other hand, security considerations and business logic related to tags might require you to manage device registration in the app back-end.</span></span> 

#### <a name="templates"></a><span data-ttu-id="27300-138">Şablonlar</span><span class="sxs-lookup"><span data-stu-id="27300-138">Templates</span></span>
<span data-ttu-id="27300-139">Kullanmak istiyorsanız, [şablonları](notification-hubs-templates-cross-platform-push-messages.md), aygıt yüklemesi de JSON bu aygıt ile ilişkili tüm şablonları tutun (Yukarıdaki örnek bakın) biçimlendirin.</span><span class="sxs-lookup"><span data-stu-id="27300-139">If you want to use [Templates](notification-hubs-templates-cross-platform-push-messages.md), the device installation also hold all templates associated with that device in a JSON format (see sample above).</span></span> <span data-ttu-id="27300-140">Şablon adları hedef farklı şablonları aynı aygıt için yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="27300-140">The template names help target different templates for the same device.</span></span>

<span data-ttu-id="27300-141">Her bir şablon adı bir şablon gövde ve isteğe bağlı bir dizi etiketi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="27300-141">Note that each template name maps to a template body and an optional set of tags.</span></span> <span data-ttu-id="27300-142">Ayrıca, her platform ek şablon özelliklere sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="27300-142">Moreover, each platform can have additional template properties.</span></span> <span data-ttu-id="27300-143">Windows Mağazası'nın (WNS kullanarak) ve Windows Phone 8 (MPNS kullanarak) için ek bir üstbilgi kümesi şablonunun parçası olabilir.</span><span class="sxs-lookup"><span data-stu-id="27300-143">For Windows Store (using WNS) and Windows Phone 8 (using MPNS), an additional set of headers can be part of the template.</span></span> <span data-ttu-id="27300-144">APNs söz konusu olduğunda, bir süre sonu özelliğini ya da veya şablon ifadesi ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27300-144">In the case of APNs, you can set an expiry property to either a constant or to a template expression.</span></span> <span data-ttu-id="27300-145">Yükleme özellikleri bakın, tam bir listesi için [oluşturmak veya bir yükleme ile REST üzerine](https://msdn.microsoft.com/library/azure/mt621153.aspx) konu.</span><span class="sxs-lookup"><span data-stu-id="27300-145">For a complete listing of the installation properties see, [Create or Overwrite an Installation with REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) topic.</span></span>

#### <a name="secondary-tiles-for-windows-store-apps"></a><span data-ttu-id="27300-146">Windows mağazası uygulamaları için ikincil döşeme</span><span class="sxs-lookup"><span data-stu-id="27300-146">Secondary Tiles for Windows Store Apps</span></span>
<span data-ttu-id="27300-147">Windows mağazası istemci uygulamaları için ikincil döşeme bildirimleri gönderme birincil birine göndererek ile aynı olur.</span><span class="sxs-lookup"><span data-stu-id="27300-147">For Windows Store client applications, sending notifications to secondary tiles is the same as sending them to the primary one.</span></span> <span data-ttu-id="27300-148">Bu ayrıca yüklemelerde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="27300-148">This is also supported in installations.</span></span> <span data-ttu-id="27300-149">İkincil döşeme istemci uygulamanızdan SDK şeffaf bir şekilde işler farklı bir ChannelUri gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="27300-149">Note that secondary tiles have a different ChannelUri, which the SDK on your client app handles transparently.</span></span>

<span data-ttu-id="27300-150">Windows mağazası uygulamanızı SecondaryTiles nesnesi oluşturmak için kullanılan aynı TileId SecondaryTiles sözlük kullanır.</span><span class="sxs-lookup"><span data-stu-id="27300-150">The SecondaryTiles dictionary uses the same TileId that is used to create the SecondaryTiles object in your Windows Store app.</span></span>
<span data-ttu-id="27300-151">Birincil ChannelUri gibi ile ikincil döşeme ChannelUris herhangi bir anda değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27300-151">As with the primary ChannelUri, ChannelUris of secondary tiles can change at any moment.</span></span> <span data-ttu-id="27300-152">Güncelleştirilen bildirim hub'ı yüklemeleri tutmak için aygıt bunları ikincil döşeme geçerli ChannelUris ile yenilemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="27300-152">In order to keep the installations in the notification hub updated, the device must refresh them with the current ChannelUris of the secondary tiles.</span></span>

## <a name="registration-management-from-the-device"></a><span data-ttu-id="27300-153">Cihaz kayıt yönetimi</span><span class="sxs-lookup"><span data-stu-id="27300-153">Registration management from the device</span></span>
<span data-ttu-id="27300-154">Cihaz kaydı istemci uygulamaları yönetirken, arka uç yalnızca bildirim göndermek için sorumludur.</span><span class="sxs-lookup"><span data-stu-id="27300-154">When managing device registration from client apps, the backend is only responsible for sending notifications.</span></span> <span data-ttu-id="27300-155">İstemci uygulamaları PNS tanıtıcılarını güncel tutun ve etiketleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="27300-155">Client apps keep PNS handles up to date, and register tags.</span></span> <span data-ttu-id="27300-156">Aşağıdaki resimde bu deseni gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="27300-156">The following picture illustrates this pattern.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

<span data-ttu-id="27300-157">Cihaz önce PNS PNS tanıtıcısını alır, sonra bildirim hub'ı ile doğrudan kaydeder.</span><span class="sxs-lookup"><span data-stu-id="27300-157">The device first retrieves the PNS handle from the PNS, then registers with the notification hub directly.</span></span> <span data-ttu-id="27300-158">Kayıt başarılı olduktan sonra uygulama arka ucu, kayıt hedefleyen bir bildirim gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27300-158">After the registration is successful, the app backend can send a notification targeting that registration.</span></span> <span data-ttu-id="27300-159">Bildirimleri gönderme hakkında daha fazla bilgi için bkz: [Yönlendirme ve etiket ifadeleri](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="27300-159">For more information about how to send notifications, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>
<span data-ttu-id="27300-160">Bu durumda, kullanacağınız not yalnızca bildirim hub'larınız aygıttan erişim hakları dinler.</span><span class="sxs-lookup"><span data-stu-id="27300-160">Note that in this case, you will use only Listen rights to access your notification hubs from the device.</span></span> <span data-ttu-id="27300-161">Daha fazla bilgi için bkz: [güvenlik](notification-hubs-push-notification-security.md).</span><span class="sxs-lookup"><span data-stu-id="27300-161">For more information, see [Security](notification-hubs-push-notification-security.md).</span></span>

<span data-ttu-id="27300-162">Aygıttan kaydetme basit yöntemidir, ancak bazı kısıtlamaları vardır.</span><span class="sxs-lookup"><span data-stu-id="27300-162">Registering from the device is the simplest method, but it has some drawbacks.</span></span>
<span data-ttu-id="27300-163">İlk dezavantajı, uygulama etkinken bir istemci uygulaması yalnızca kendi etiketleri güncelleştirebilirsiniz olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="27300-163">The first drawback is that a client app can only update its tags when the app is active.</span></span> <span data-ttu-id="27300-164">Bir kullanıcının ilk aygıt bir ek etiketi (örneğin, takımınız) kaydettiğinde Spor takıma ilgili etiketleri kaydetme iki cihazlar varsa, ikinci cihaza uygulamanın kadar Örneğin, ikinci bir cihaz takımınız hakkında bildirimler almaz ikinci kez yürütüldü.</span><span class="sxs-lookup"><span data-stu-id="27300-164">For example, if a user has two devices that register tags related to sport teams, when the first device registers for an additional tag (for example, Seahawks), the second device will not receive the notifications about the Seahawks until the app on the second device is executed a second time.</span></span> <span data-ttu-id="27300-165">Etiketler birden çok aygıt tarafından etkilenir, daha genel olarak, etiketleri arka ucundan yönetme bir arzu seçenektir.</span><span class="sxs-lookup"><span data-stu-id="27300-165">More generally, when tags are affected by multiple devices, managing tags from the backend is a desirable option.</span></span>
<span data-ttu-id="27300-166">Kayıt Yönetimi istemci uygulamasından ikinci dezavantajı uygulamaları ele olduğundan, kayıt belirli etiketleri için güvenli hale getirme ek bakım, "etiketi düzeyi güvenlik." bölümünde açıklandığı gibi gerektirmesidir</span><span class="sxs-lookup"><span data-stu-id="27300-166">The second drawback of registration management from the client app is that, since apps can be hacked, securing the registration to specific tags requires extra care, as explained in the section “Tag-level security.”</span></span>

#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-an-installation"></a><span data-ttu-id="27300-167">Bildirim hub'ı bir yükleme seçeneğini kullanarak bir aygıt ile kaydetmek için örnek kod</span><span class="sxs-lookup"><span data-stu-id="27300-167">Example code to register with a notification hub from a device using an installation</span></span>
<span data-ttu-id="27300-168">Şu anda yalnızca kullanarak destekleniyorsa [Notification Hubs REST API'si](https://msdn.microsoft.com/library/mt621153.aspx).</span><span class="sxs-lookup"><span data-stu-id="27300-168">At this time, this is only supported using the [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx).</span></span>

<span data-ttu-id="27300-169">Düzeltme eki yöntemini kullanarak da kullanabilirsiniz [JSON düzeltme eki standart](https://tools.ietf.org/html/rfc6902) yükleme güncelleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="27300-169">You can also use the PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating the installation.</span></span>

    class DeviceInstallation
    {
        public string installationId { get; set; }
        public string platform { get; set; }
        public string pushChannel { get; set; }
        public string[] tags { get; set; }
    }

    private async Task<HttpStatusCode> CreateOrUpdateInstallationAsync(DeviceInstallation deviceInstallation,
         string hubName, string listenConnectionString)
    {
        if (deviceInstallation.installationId == null)
            return HttpStatusCode.BadRequest;

        // Parse connection string (https://msdn.microsoft.com/library/azure/dn495627.aspx)
        ConnectionStringUtility connectionSaSUtil = new ConnectionStringUtility(listenConnectionString);
        string hubResource = "installations/" + deviceInstallation.installationId + "?";
        string apiVersion = "api-version=2015-04";

        // Determine the targetUri that we will sign
        string uri = connectionSaSUtil.Endpoint + hubName + "/" + hubResource + apiVersion;

        //=== Generate SaS Security Token for Authorization header ===
        // See, https://msdn.microsoft.com/library/azure/dn495627.aspx
        string SasToken = connectionSaSUtil.getSaSToken(uri, 60);

        using (var httpClient = new HttpClient())
        {
            string json = JsonConvert.SerializeObject(deviceInstallation);

            httpClient.DefaultRequestHeaders.Add("Authorization", SasToken);

            var response = await httpClient.PutAsync(uri, new StringContent(json, System.Text.Encoding.UTF8, "application/json"));
            return response.StatusCode;
        }
    }

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    string installationId = null;
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a installation id in application data, create and store as application data.
    if (!settings.ContainsKey("__NHInstallationId"))
    {
        installationId = Guid.NewGuid().ToString();
        settings.Add("__NHInstallationId", installationId);
    }

    installationId = (string)settings["__NHInstallationId"];

    var deviceInstallation = new DeviceInstallation
    {
        installationId = installationId,
        platform = "wns",
        pushChannel = channel.Uri,
        //tags = tags.ToArray<string>()
    };

    var statusCode = await CreateOrUpdateInstallationAsync(deviceInstallation, 
                        "<HUBNAME>", "<SHARED LISTEN CONNECTION STRING>");

    if (statusCode != HttpStatusCode.Accepted)
    {
        var dialog = new MessageDialog(statusCode.ToString(), "Registration failed. Installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
    else
    {
        var dialog = new MessageDialog("Registration successful using installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }



#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-a-registration"></a><span data-ttu-id="27300-170">Bildirim hub'ı kullanarak bir kaydı bir aygıttan ile kaydetmek için örnek kod</span><span class="sxs-lookup"><span data-stu-id="27300-170">Example code to register with a notification hub from a device using a registration</span></span>
<span data-ttu-id="27300-171">Bu yöntemler oluşturun veya bunlar üzerinde adlandırılır cihaz için bir kayıt güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="27300-171">These methods create or update a registration for the device on which they are called.</span></span> <span data-ttu-id="27300-172">Başka bir deyişle, tanıtıcı veya etiketleri güncelleştirmek için tüm kayıt üzerine yazmalıdır.</span><span class="sxs-lookup"><span data-stu-id="27300-172">This means that in order to update the handle or the tags, you must overwrite the entire registration.</span></span> <span data-ttu-id="27300-173">Her zaman belirli bir aygıt gereklidir geçerli etiketler güvenilir deposuyla gerekir böylece kayıtlar geçici olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="27300-173">Remember that registrations are transient, so you should always have a reliable store with the current tags that a specific device needs.</span></span>

    // Initialize the Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // The Device id from the PNS
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // If you are registering from the client itself, then store this registration id in device
    // storage. Then when the app starts, you can check if a registration id already exists or not before
    // creating.
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a registration id in application data, store in application data.
    if (!settings.ContainsKey("__NHRegistrationId"))
    {
        // make sure there are no existing registrations for this push handle (used for iOS and Android)    
        string newRegistrationId = null;
        var registrations = await hub.GetRegistrationsByChannelAsync(pushChannel.Uri, 100);
        foreach (RegistrationDescription registration in registrations)
        {
            if (newRegistrationId == null)
            {
                newRegistrationId = registration.RegistrationId;
            }
            else
            {
                await hub.DeleteRegistrationAsync(registration);
            }
        }

        newRegistrationId = await hub.CreateRegistrationIdAsync();

        settings.Add("__NHRegistrationId", newRegistrationId);
    }

    string regId = (string)settings["__NHRegistrationId"];

    RegistrationDescription registration = new WindowsRegistrationDescription(pushChannel.Uri);
    registration.RegistrationId = regId;
    registration.Tags = new HashSet<string>(YourTags);

    try
    {
        await hub.CreateOrUpdateRegistrationAsync(registration);
    }
    catch (Microsoft.WindowsAzure.Messaging.RegistrationGoneException e)
    {
        settings.Remove("__NHRegistrationId");
    }


## <a name="registration-management-from-a-backend"></a><span data-ttu-id="27300-174">Kayıt Yönetimi'nden bir arka uç</span><span class="sxs-lookup"><span data-stu-id="27300-174">Registration management from a backend</span></span>
<span data-ttu-id="27300-175">Kayıtlar arka ucundan yönetme ek kod yazma gerektirir.</span><span class="sxs-lookup"><span data-stu-id="27300-175">Managing registrations from the backend requires writing additional code.</span></span> <span data-ttu-id="27300-176">Uygulama aygıttan güncelleştirilmiş PNS arka ucuna uygulama (etiketleri ve şablonlar ile birlikte) her başlatılışında işlemek ve arka uç bu tanıtıcıyı bildirim hub'ındaki güncelleştirmelisiniz sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="27300-176">The app from the device must provide the updated PNS handle to the backend every time the app starts (along with tags and templates), and the backend must update this handle on the notification hub.</span></span> <span data-ttu-id="27300-177">Aşağıdaki resimde bu tasarım gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="27300-177">The following picture illustrates this design.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

<span data-ttu-id="27300-178">Kayıtlar arka ucundan yönetme avantajlar cihaza karşılık gelen uygulamanın devre dışı olduğunda bile kayıtlar etiketleri değiştirebilir ve kendi kaydı için bir etiket eklemeden önce istemci uygulamanın kimlik doğrulamasını olanağı vardır.</span><span class="sxs-lookup"><span data-stu-id="27300-178">The advantages of managing registrations from the backend include the ability to modify tags to registrations even when the corresponding app on the device is inactive, and to authenticate the client app before adding a tag to its registration.</span></span>

#### <a name="example-code-to-register-with-a-notification-hub-from-a-backend-using-an-installation"></a><span data-ttu-id="27300-179">Bir bildirim hub'ından bir yükleme seçeneğini kullanarak bir arka uç ile kaydetmek için örnek kod</span><span class="sxs-lookup"><span data-stu-id="27300-179">Example code to register with a notification hub from a backend using an installation</span></span>
<span data-ttu-id="27300-180">İstemci aygıtı hala önce ilgili yüklemeyi özellikleri olarak ve PNS tanıtıcısını alır ve kaydı gerçekleştirmek ve etiketleri vb. yetkilendirmek arka uç özel bir API çağırır. Arka uç yararlanabilirsiniz [Notification Hub SDK'sı arka uç işlemleri için](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="27300-180">The client device still gets its PNS handle and relevant installation properties as before and calls a custom API on the backend that can perform the registration and authorize tags etc. The backend can leverage the [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="27300-181">Düzeltme eki yöntemini kullanarak da kullanabilirsiniz [JSON düzeltme eki standart](https://tools.ietf.org/html/rfc6902) yükleme güncelleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="27300-181">You can also use the PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating the installation.</span></span>

    // Initialize the Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // Custom API on the backend
    public async Task<HttpResponseMessage> Put(DeviceInstallation deviceUpdate)
    {

        Installation installation = new Installation();
        installation.InstallationId = deviceUpdate.InstallationId;
        installation.PushChannel = deviceUpdate.Handle;
        installation.Tags = deviceUpdate.Tags;

        switch (deviceUpdate.Platform)
        {
            case "mpns":
                installation.Platform = NotificationPlatform.Mpns;
                break;
            case "wns":
                installation.Platform = NotificationPlatform.Wns;
                break;
            case "apns":
                installation.Platform = NotificationPlatform.Apns;
                break;
            case "gcm":
                installation.Platform = NotificationPlatform.Gcm;
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }


        // In the backend we can control if a user is allowed to add tags
        //installation.Tags = new List<string>(deviceUpdate.Tags);
        //installation.Tags.Add("username:" + username);

        await hub.CreateOrUpdateInstallationAsync(installation);

        return Request.CreateResponse(HttpStatusCode.OK);
    }


#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-a-registration-id"></a><span data-ttu-id="27300-182">Bildirim hub'ı bir kayıt kimliği kullanılarak bir aygıttan ile kaydetmek için örnek kod</span><span class="sxs-lookup"><span data-stu-id="27300-182">Example code to register with a notification hub from a device using a registration id</span></span>
<span data-ttu-id="27300-183">Uygulama arka ucunuzdan, kayıtlar üzerinde temel CRUDS işlemler gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27300-183">From your app backend, you can perform basic CRUDS operations on registrations.</span></span> <span data-ttu-id="27300-184">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="27300-184">For example:</span></span>

    var hub = NotificationHubClient.CreateClientFromConnectionString("{connectionString}", "hubName");

    // create a registration description object of the correct type, e.g.
    var reg = new WindowsRegistrationDescription(channelUri, tags);

    // Create
    await hub.CreateRegistrationAsync(reg);

    // Get by id
    var r = await hub.GetRegistrationAsync<RegistrationDescription>("id");

    // update
    r.Tags.Add("myTag");

    // update on hub
    await hub.UpdateRegistrationAsync(r);

    // delete
    await hub.DeleteRegistrationAsync(r);


<span data-ttu-id="27300-185">Arka uç kaydı güncelleştirmeleri arasındaki eşzamanlılık işlemelidir.</span><span class="sxs-lookup"><span data-stu-id="27300-185">The backend must handle concurrency between registration updates.</span></span> <span data-ttu-id="27300-186">Hizmet veri yolu iyimser eşzamanlılık denetimini kayıt yönetimi sunar.</span><span class="sxs-lookup"><span data-stu-id="27300-186">Service Bus offers optimistic concurrency control for registration management.</span></span> <span data-ttu-id="27300-187">HTTP düzeyde, bu, kayıt yönetimi işlemleri ETag kullanılmasına uygulanır.</span><span class="sxs-lookup"><span data-stu-id="27300-187">At the HTTP level, this is implemented with the use of ETag on registration management operations.</span></span> <span data-ttu-id="27300-188">Bu özellik, saydam bir güncelleştirme eşzamanlılık nedenlerle reddedilirse, bir özel durum SDKs tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="27300-188">This feature is transparently used by Microsoft SDKs, which throw an exception if an update is rejected for concurrency reasons.</span></span> <span data-ttu-id="27300-189">Uygulama arka ucu, bu özel durumları işleme ve gerekirse güncelleştirme yeniden deneniyor sorumludur.</span><span class="sxs-lookup"><span data-stu-id="27300-189">The app backend is responsible for handling these exceptions and retrying the update if required.</span></span>

