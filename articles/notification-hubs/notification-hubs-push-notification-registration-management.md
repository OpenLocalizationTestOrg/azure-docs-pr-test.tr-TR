---
title: "aaaRegistration Yönetimi"
description: "Bu konuda nasıl tooregister aygıtları sipariş tooreceive notification hubs ile anında iletme bildirimleri açıklanmaktadır."
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
ms.openlocfilehash: 76471a45c7a0da1614ceed82b73cdb3319979ff7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="registration-management"></a><span data-ttu-id="ef1f1-103">Kayıt yönetimi</span><span class="sxs-lookup"><span data-stu-id="ef1f1-103">Registration management</span></span>
## <a name="overview"></a><span data-ttu-id="ef1f1-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="ef1f1-104">Overview</span></span>
<span data-ttu-id="ef1f1-105">Bu konuda nasıl tooregister aygıtları sipariş tooreceive notification hubs ile anında iletme bildirimleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-105">This topic explains how tooregister devices with notification hubs in order tooreceive push notifications.</span></span> <span data-ttu-id="ef1f1-106">Merhaba konu kayıtlar yüksek düzeyde açıklanır ve ardından aygıtları kaydetmeye yönelik hello iki ana desenleri sunar: hello aygıttan kaydetme doğrudan toohello bildirim hub'ı ve bir uygulama arka ucu kaydediliyor.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-106">hello topic describes registrations at a high level, then introduces hello two main patterns for registering devices: registering from hello device directly toohello notification hub, and registering through an application backend.</span></span> 

## <a name="what-is-device-registration"></a><span data-ttu-id="ef1f1-107">Cihaz kaydı nedir</span><span class="sxs-lookup"><span data-stu-id="ef1f1-107">What is device registration</span></span>
<span data-ttu-id="ef1f1-108">Bildirim hub'ı ile cihaz kaydı kullanarak gerçekleştirilir bir **kayıt** veya **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-108">Device registration with a Notification Hub is accomplished using a **Registration** or **Installation**.</span></span>

#### <a name="registrations"></a><span data-ttu-id="ef1f1-109">Kayıtlar</span><span class="sxs-lookup"><span data-stu-id="ef1f1-109">Registrations</span></span>
<span data-ttu-id="ef1f1-110">Bir kayıt etiketleri ve büyük olasılıkla bir şablonu ile bir aygıt için Platform bildirim hizmeti (PNS) işlemek hello ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-110">A registration associates hello Platform Notification Service (PNS) handle for a device with tags and possibly a template.</span></span> <span data-ttu-id="ef1f1-111">Merhaba PNS tanıtıcısını ChannelURI, cihaz belirteci veya GCM kayıt kimliği olabilir. Etiketler kullanılan tooroute bildirimleri toohello doğru cihaz tanıtıcılarını kümesidir.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-111">hello PNS handle could be a ChannelURI, device token, or GCM registration id. Tags are used tooroute notifications toohello correct set of device handles.</span></span> <span data-ttu-id="ef1f1-112">Daha fazla bilgi için bkz: [Yönlendirme ve etiket ifadeleri](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="ef1f1-112">For more information, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span> <span data-ttu-id="ef1f1-113">Kullanılan tooimplement kayıt başına dönüştürme şablonlarıdır.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-113">Templates are used tooimplement per-registration transformation.</span></span> <span data-ttu-id="ef1f1-114">Daha fazla bilgi için bkz: [şablonları](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="ef1f1-114">For more information, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>

#### <a name="installations"></a><span data-ttu-id="ef1f1-115">Yüklemeleri</span><span class="sxs-lookup"><span data-stu-id="ef1f1-115">Installations</span></span>
<span data-ttu-id="ef1f1-116">Yüklemesi geliştirilmiş olabilir itme paketi içeren kayıt ilgili özellikler.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-116">An Installation is an enhanced registration that includes a bag of push related properties.</span></span> <span data-ttu-id="ef1f1-117">Bu, en son ve en iyi yaklaşımı tooregistering aygıtlarınızı hello olur.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-117">It is hello latest and best approach tooregistering your devices.</span></span> <span data-ttu-id="ef1f1-118">Ancak, istemci tarafı .NET SDK'sı tarafından desteklenmiyor ([Notification Hub SDK'sı arka uç işlemleri için](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) henüz dağıtmadığı.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-118">However, it is not supported by client side .NET SDK ([Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) as of yet.</span></span>  <span data-ttu-id="ef1f1-119">Hello istemci CİHAZDAN kaydediyorsunuz varsa toouse hello yani [Notification Hubs REST API'si](https://msdn.microsoft.com/library/mt621153.aspx) yaklaşımını toosupport yüklemeleri.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-119">This means if you are registering from hello client device itself, you would have toouse hello [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx) approach toosupport installations.</span></span> <span data-ttu-id="ef1f1-120">Bir arka uç hizmeti kullanıyorsanız, mümkün toouse olmalıdır [Notification Hub SDK'sı arka uç işlemleri için](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="ef1f1-120">If you are using a backend service, you should be able toouse [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="ef1f1-121">Merhaba, bazı önemli avantajı toousing yüklemeler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ef1f1-121">hello following are some key advantages toousing installations:</span></span>

* <span data-ttu-id="ef1f1-122">Oluşturma veya bir yüklemeyi güncelleştirme ıdempotent tam değil.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-122">Creating or updating an installation is fully idempotent.</span></span> <span data-ttu-id="ef1f1-123">Bu nedenle tüm yinelenen kayıtları endişeniz olmadan deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-123">So you can retry it without any concerns about duplicate registrations.</span></span>
* <span data-ttu-id="ef1f1-124">Merhaba yükleme modeli kolay toodo tek tek iter - belirli bir aygıtı hedefleme kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-124">hello installation model makes it easy toodo individual pushes - targeting specific device.</span></span> <span data-ttu-id="ef1f1-125">Bir sistem etiketi **"$InstallationId: [InstallationID]"** her bağlı yükleme kaydı otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-125">A system tag **"$InstallationId:[installationId]"** is automatically added with each installation based registration.</span></span> <span data-ttu-id="ef1f1-126">Bu nedenle hiçbir ek kodlama toodo gerek kalmadan belirli bir aygıt gönderme toothis etiketi tootarget çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-126">So you can call a send toothis tag tootarget a specific device without having toodo any additional coding.</span></span>
* <span data-ttu-id="ef1f1-127">Yüklemeleri kullanarak, toodo kısmi kayıt güncelleştirmeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-127">Using installations also enables you toodo partial registration updates.</span></span> <span data-ttu-id="ef1f1-128">Merhaba kısmi güncelleştirme yüklemesinin hello kullanarak bir düzeltme eki yöntemiyle istenmeden [JSON düzeltme eki standart](https://tools.ietf.org/html/rfc6902).</span><span class="sxs-lookup"><span data-stu-id="ef1f1-128">hello partial update of an installation is requested with a PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902).</span></span> <span data-ttu-id="ef1f1-129">Bu, özellikle hello kayıt tooupdate etiketlerini istediğinizde kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-129">This is particularly useful when you want tooupdate tags on hello registration.</span></span> <span data-ttu-id="ef1f1-130">Merhaba tüm kayıt aşağı toopull yoksa ve tüm hello önceki etiketleri tekrar tekrar gönderin.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-130">You don't have toopull down hello entire registration and then resend all hello previous tags again.</span></span>

<span data-ttu-id="ef1f1-131">Yüklemenin aşağıdaki özelliklere hello hello içerebilir.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-131">An installation can contain hello hello following properties.</span></span> <span data-ttu-id="ef1f1-132">Merhaba yükleme özellikleri bakın, tam bir listesi için [oluşturmak veya bir yükleme ile REST API üzerine](https://msdn.microsoft.com/library/azure/mt621153.aspx) veya [yükleme özellikleri](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) hello için.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-132">For a complete listing of hello installation properties see, [Create or Overwrite an Installation with REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx) or [Installation Properties](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) for hello .</span></span>

    // Example installation format tooshow some supported properties
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



<span data-ttu-id="ef1f1-133">Bu kayıtlar ve varsayılan olarak yüklemeleri artık sona önemli toonote olur.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-133">It is important toonote that registrations and installations by default no longer expire.</span></span>

<span data-ttu-id="ef1f1-134">Kayıtlar ve yüklemeleri her cihaz/kanal için geçerli bir PNS tanıtıcısını içermelidir.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-134">Registrations and installations must contain a valid PNS handle for each device/channel.</span></span> <span data-ttu-id="ef1f1-135">PNS tanıtıcılarını yalnızca hello aygıttaki istemci uygulamasında alınabilir, bir desen hello istemci uygulaması ile bir cihazda doğrudan tooregister olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-135">Because PNS handles can only be obtained in a client app on hello device, one pattern is tooregister directly on that device with hello client app.</span></span> <span data-ttu-id="ef1f1-136">Merhaba üzerinde tootags hello uygulama arka uç toomanage cihaz kaydında gerektirebilir diğer yandan, güvenlik konuları ve iş mantığı ilgili.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-136">On hello other hand, security considerations and business logic related tootags might require you toomanage device registration in hello app back-end.</span></span> 

#### <a name="templates"></a><span data-ttu-id="ef1f1-137">Şablonlar</span><span class="sxs-lookup"><span data-stu-id="ef1f1-137">Templates</span></span>
<span data-ttu-id="ef1f1-138">Toouse istiyorsanız [şablonları](notification-hubs-templates-cross-platform-push-messages.md), hello aygıt yüklemesi de JSON bu aygıt ile ilişkili tüm şablonları tutun (Yukarıdaki örnek bakın) biçimlendirin.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-138">If you want toouse [Templates](notification-hubs-templates-cross-platform-push-messages.md), hello device installation also hold all templates associated with that device in a JSON format (see sample above).</span></span> <span data-ttu-id="ef1f1-139">Merhaba şablon adları farklı şablonları hello için hedef Yardım aynı aygıt.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-139">hello template names help target different templates for hello same device.</span></span>

<span data-ttu-id="ef1f1-140">Her bir şablon adı tooa şablon gövde ve etiketleri isteğe bağlı bir dizi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-140">Note that each template name maps tooa template body and an optional set of tags.</span></span> <span data-ttu-id="ef1f1-141">Ayrıca, her platform ek şablon özelliklere sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-141">Moreover, each platform can have additional template properties.</span></span> <span data-ttu-id="ef1f1-142">Windows Mağazası'nın (WNS kullanarak) ve Windows Phone 8 (MPNS kullanarak) için ek bir üstbilgi kümesi hello şablonunun parçası olabilir.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-142">For Windows Store (using WNS) and Windows Phone 8 (using MPNS), an additional set of headers can be part of hello template.</span></span> <span data-ttu-id="ef1f1-143">APNs Hello durumda sabit veya tooa şablon ifadesi bir süre sonu özelliği tooeither ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-143">In hello case of APNs, you can set an expiry property tooeither a constant or tooa template expression.</span></span> <span data-ttu-id="ef1f1-144">Merhaba yükleme özellikleri bakın, tam bir listesi için [oluşturmak veya bir yükleme ile REST üzerine](https://msdn.microsoft.com/library/azure/mt621153.aspx) konu.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-144">For a complete listing of hello installation properties see, [Create or Overwrite an Installation with REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) topic.</span></span>

#### <a name="secondary-tiles-for-windows-store-apps"></a><span data-ttu-id="ef1f1-145">Windows mağazası uygulamaları için ikincil döşeme</span><span class="sxs-lookup"><span data-stu-id="ef1f1-145">Secondary Tiles for Windows Store Apps</span></span>
<span data-ttu-id="ef1f1-146">Windows mağazası istemci uygulamaları için gönderen bildirimleri toosecondary döşeme olduğu aynı toohello birincil bir gönderme olarak hello.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-146">For Windows Store client applications, sending notifications toosecondary tiles is hello same as sending them toohello primary one.</span></span> <span data-ttu-id="ef1f1-147">Bu ayrıca yüklemelerde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-147">This is also supported in installations.</span></span> <span data-ttu-id="ef1f1-148">İkincil döşeme hangi ' % s'hello SDK istemci uygulamanızdan şeffaf bir şekilde işler farklı bir ChannelUri gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-148">Note that secondary tiles have a different ChannelUri, which hello SDK on your client app handles transparently.</span></span>

<span data-ttu-id="ef1f1-149">Merhaba SecondaryTiles sözlük kullanan Windows mağazası uygulamanızı kullanılan toocreate hello SecondaryTiles nesne aynı TileId hello.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-149">hello SecondaryTiles dictionary uses hello same TileId that is used toocreate hello SecondaryTiles object in your Windows Store app.</span></span>
<span data-ttu-id="ef1f1-150">Olarak ile Merhaba birincil ChannelUri, ikincil döşeme ChannelUris herhangi bir anda değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-150">As with hello primary ChannelUri, ChannelUris of secondary tiles can change at any moment.</span></span> <span data-ttu-id="ef1f1-151">Sipariş tookeep hello yüklemelerde hello bildirim hub'ı güncelleştirilmiş hello aygıt bunları hello ile yenilemeniz gerekir hello ikincil döşeme geçerli ChannelUris.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-151">In order tookeep hello installations in hello notification hub updated, hello device must refresh them with hello current ChannelUris of hello secondary tiles.</span></span>

## <a name="registration-management-from-hello-device"></a><span data-ttu-id="ef1f1-152">Merhaba aygıttan kayıt yönetimi</span><span class="sxs-lookup"><span data-stu-id="ef1f1-152">Registration management from hello device</span></span>
<span data-ttu-id="ef1f1-153">Cihaz kaydı istemci uygulamaları yönetirken hello arka uç yalnızca bildirim göndermek için sorumludur.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-153">When managing device registration from client apps, hello backend is only responsible for sending notifications.</span></span> <span data-ttu-id="ef1f1-154">İstemci uygulamaları PNS tanıtıcılarını toodate yukarı tutmak ve etiketleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-154">Client apps keep PNS handles up toodate, and register tags.</span></span> <span data-ttu-id="ef1f1-155">Resim aşağıdaki hello bu deseni gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-155">hello following picture illustrates this pattern.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

<span data-ttu-id="ef1f1-156">Merhaba cihaz ilk PNS hello hello PNS ele alır ve sonra hello bildirim hub'ı doğrudan kaydeder.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-156">hello device first retrieves hello PNS handle from hello PNS, then registers with hello notification hub directly.</span></span> <span data-ttu-id="ef1f1-157">Merhaba kaydı başarılı olduktan sonra hello uygulama arka ucu o kayıt hedefleyen bir bildirim gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-157">After hello registration is successful, hello app backend can send a notification targeting that registration.</span></span> <span data-ttu-id="ef1f1-158">Hakkında daha fazla bilgi için toosend bildirimleri bkz [Yönlendirme ve etiket ifadeleri](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="ef1f1-158">For more information about how toosend notifications, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>
<span data-ttu-id="ef1f1-159">Bu durumda, kullanacağınız Not hello aygıttan bildirim hub'larınız yalnızca hakları tooaccess dinler.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-159">Note that in this case, you will use only Listen rights tooaccess your notification hubs from hello device.</span></span> <span data-ttu-id="ef1f1-160">Daha fazla bilgi için bkz: [güvenlik](notification-hubs-push-notification-security.md).</span><span class="sxs-lookup"><span data-stu-id="ef1f1-160">For more information, see [Security](notification-hubs-push-notification-security.md).</span></span>

<span data-ttu-id="ef1f1-161">Merhaba aygıttan kaydetme hello basit bir yöntemdir, ancak bazı kısıtlamaları vardır.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-161">Registering from hello device is hello simplest method, but it has some drawbacks.</span></span>
<span data-ttu-id="ef1f1-162">Merhaba ilk dezavantajı hello uygulama etkin durumdayken bir istemci uygulaması yalnızca kendi etiketleri güncelleştirebilirsiniz olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-162">hello first drawback is that a client app can only update its tags when hello app is active.</span></span> <span data-ttu-id="ef1f1-163">Bir kullanıcının hello ilk aygıt bir ek etiketi (örneğin, takımınız) kaydettiğinde etiketleri ilgili toosport ekipleri, kayıt iki cihazlar varsa, örneğin, hello ikinci bir cihaz hello takımınız hakkında hello bildirimler hello hello uygulamasını kadar almaz İkinci bir cihaz ikinci bir kez çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-163">For example, if a user has two devices that register tags related toosport teams, when hello first device registers for an additional tag (for example, Seahawks), hello second device will not receive hello notifications about hello Seahawks until hello app on hello second device is executed a second time.</span></span> <span data-ttu-id="ef1f1-164">Etiketler birden çok aygıt tarafından etkilenir, daha genel olarak, etiketleri hello arka ucundan yönetme bir arzu seçenektir.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-164">More generally, when tags are affected by multiple devices, managing tags from hello backend is a desirable option.</span></span>
<span data-ttu-id="ef1f1-165">Hello ikinci dezavantajı hello istemci uygulamasından kayıt yönetimi, uygulamaları ele olduğundan, hello kayıt toospecific etiketleri güvenliğini sağlama fazladan bakımı, "etiketi düzeyi güvenlik." Merhaba bölümünde açıklandığı gibi gerektirmesidir</span><span class="sxs-lookup"><span data-stu-id="ef1f1-165">hello second drawback of registration management from hello client app is that, since apps can be hacked, securing hello registration toospecific tags requires extra care, as explained in hello section “Tag-level security.”</span></span>

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-an-installation"></a><span data-ttu-id="ef1f1-166">Örnek kod tooregister bir bildirim hub'ından bir yükleme kullanarak bir cihazı ile</span><span class="sxs-lookup"><span data-stu-id="ef1f1-166">Example code tooregister with a notification hub from a device using an installation</span></span>
<span data-ttu-id="ef1f1-167">Şu anda yalnızca hello kullanarak destekleniyorsa [Notification Hubs REST API'si](https://msdn.microsoft.com/library/mt621153.aspx).</span><span class="sxs-lookup"><span data-stu-id="ef1f1-167">At this time, this is only supported using hello [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx).</span></span>

<span data-ttu-id="ef1f1-168">Hello kullanarak hello düzeltme eki yöntemini de kullanabilirsiniz [JSON düzeltme eki standart](https://tools.ietf.org/html/rfc6902) hello yükleme güncelleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-168">You can also use hello PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating hello installation.</span></span>

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

        // Determine hello targetUri that we will sign
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



#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration"></a><span data-ttu-id="ef1f1-169">Örnek kod tooregister bir bildirim hub'ından bir kaydı kullanarak bir cihazı ile</span><span class="sxs-lookup"><span data-stu-id="ef1f1-169">Example code tooregister with a notification hub from a device using a registration</span></span>
<span data-ttu-id="ef1f1-170">Bu yöntemler oluşturun veya bunlar adı verilir hello cihaz için bir kayıt güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-170">These methods create or update a registration for hello device on which they are called.</span></span> <span data-ttu-id="ef1f1-171">Bu sipariş tooupdate hello tanıtıcısı veya hello etiketlerinde, hello tüm kayıt üzerine yazmalıdır anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-171">This means that in order tooupdate hello handle or hello tags, you must overwrite hello entire registration.</span></span> <span data-ttu-id="ef1f1-172">Her zaman belirli bir aygıt gereklidir hello geçerli etiketler güvenilir deposuyla gerekir böylece kayıtlar geçici olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-172">Remember that registrations are transient, so you should always have a reliable store with hello current tags that a specific device needs.</span></span>

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // hello Device id from hello PNS
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // If you are registering from hello client itself, then store this registration id in device
    // storage. Then when hello app starts, you can check if a registration id already exists or not before
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


## <a name="registration-management-from-a-backend"></a><span data-ttu-id="ef1f1-173">Kayıt Yönetimi'nden bir arka uç</span><span class="sxs-lookup"><span data-stu-id="ef1f1-173">Registration management from a backend</span></span>
<span data-ttu-id="ef1f1-174">Kayıtlar hello arka ucundan yönetme ek kod yazma gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-174">Managing registrations from hello backend requires writing additional code.</span></span> <span data-ttu-id="ef1f1-175">Merhaba CİHAZDAN Hello uygulamasını hello uygulama (etiketleri ve şablonlar ile birlikte) her başlatıldığında güncelleştirilmiş PNS tanıtıcı toohello arka uç hello ve hello arka uç bu tanıtıcıyı hello bildirim hub'ındaki güncelleştirmeniz gerekir sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-175">hello app from hello device must provide hello updated PNS handle toohello backend every time hello app starts (along with tags and templates), and hello backend must update this handle on hello notification hub.</span></span> <span data-ttu-id="ef1f1-176">Bu tasarım resim aşağıdaki hello gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-176">hello following picture illustrates this design.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

<span data-ttu-id="ef1f1-177">hello yararları hello arka ucundan kayıtlarını yönetme, etiket tooits kayıt eklemeden önce hello karşılık gelen uygulamasını hello cihazda devre dışı olduğunda bile hello özelliği toomodify etiketleri tooregistrations ve tooauthenticate hello istemci uygulamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-177">hello advantages of managing registrations from hello backend include hello ability toomodify tags tooregistrations even when hello corresponding app on hello device is inactive, and tooauthenticate hello client app before adding a tag tooits registration.</span></span>

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-backend-using-an-installation"></a><span data-ttu-id="ef1f1-178">Örnek kod tooregister bir bildirim hub'ından bir yükleme seçeneğini kullanarak bir arka uç ile</span><span class="sxs-lookup"><span data-stu-id="ef1f1-178">Example code tooregister with a notification hub from a backend using an installation</span></span>
<span data-ttu-id="ef1f1-179">Hello istemci aygıt hala alır PNS tanıtıcısını ve ilgili yükleme özellikleri eskisi ve özel bir API hello kaydı gerçekleştirmek ve onları yetkilendirmek hello arka uç üzerinde etiketler vb. hello arka uç çağrıları hello yararlanabilir [Notification Hub SDK'sı arka uç işlemleri](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="ef1f1-179">hello client device still gets its PNS handle and relevant installation properties as before and calls a custom API on hello backend that can perform hello registration and authorize tags etc. hello backend can leverage hello [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="ef1f1-180">Hello kullanarak hello düzeltme eki yöntemini de kullanabilirsiniz [JSON düzeltme eki standart](https://tools.ietf.org/html/rfc6902) hello yükleme güncelleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-180">You can also use hello PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating hello installation.</span></span>

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // Custom API on hello backend
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


        // In hello backend we can control if a user is allowed tooadd tags
        //installation.Tags = new List<string>(deviceUpdate.Tags);
        //installation.Tags.Add("username:" + username);

        await hub.CreateOrUpdateInstallationAsync(installation);

        return Request.CreateResponse(HttpStatusCode.OK);
    }


#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration-id"></a><span data-ttu-id="ef1f1-181">Örnek kod tooregister bildirim hub'ı bir kayıt kimliği kullanılarak bir aygıttan ile</span><span class="sxs-lookup"><span data-stu-id="ef1f1-181">Example code tooregister with a notification hub from a device using a registration id</span></span>
<span data-ttu-id="ef1f1-182">Uygulama arka ucunuzdan, kayıtlar üzerinde temel CRUDS işlemler gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-182">From your app backend, you can perform basic CRUDS operations on registrations.</span></span> <span data-ttu-id="ef1f1-183">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ef1f1-183">For example:</span></span>

    var hub = NotificationHubClient.CreateClientFromConnectionString("{connectionString}", "hubName");

    // create a registration description object of hello correct type, e.g.
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


<span data-ttu-id="ef1f1-184">Merhaba arka uç kaydı güncelleştirmeleri arasındaki eşzamanlılık işlemelidir.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-184">hello backend must handle concurrency between registration updates.</span></span> <span data-ttu-id="ef1f1-185">Hizmet veri yolu iyimser eşzamanlılık denetimini kayıt yönetimi sunar.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-185">Service Bus offers optimistic concurrency control for registration management.</span></span> <span data-ttu-id="ef1f1-186">Merhaba HTTP düzeyde, bu kayıt yönetim işlemlerini ETag, hello kullanımıyla uygulanır.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-186">At hello HTTP level, this is implemented with hello use of ETag on registration management operations.</span></span> <span data-ttu-id="ef1f1-187">Bu özellik, saydam bir güncelleştirme eşzamanlılık nedenlerle reddedilirse, bir özel durum SDKs tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-187">This feature is transparently used by Microsoft SDKs, which throw an exception if an update is rejected for concurrency reasons.</span></span> <span data-ttu-id="ef1f1-188">Merhaba uygulama arka ucu, bu özel durumları işleme ve gerekirse hello güncelleştirme yeniden deneniyor sorumludur.</span><span class="sxs-lookup"><span data-stu-id="ef1f1-188">hello app backend is responsible for handling these exceptions and retrying hello update if required.</span></span>

