---
title: "Akış uç noktaları hello Azure portal ile aaaManage | Microsoft Docs"
description: "Bu konu, nasıl Azure portal ile toomanage akış uç noktalarını hello gösterir."
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: bb1aca25-d23a-4520-8c45-44ef3ecd5371
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: dfa9352894d37edb317a6334d7f109419deb362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-hello-azure-portal"></a><span data-ttu-id="97d64-103">Akış uç hello Azure portal ile yönetin</span><span class="sxs-lookup"><span data-stu-id="97d64-103">Manage streaming endpoints with hello Azure portal</span></span>

<span data-ttu-id="97d64-104">Bu konu, nasıl toouse hello Azure portal toomanage akış uç noktalarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="97d64-104">This topic shows  how toouse hello Azure portal toomanage streaming endpoints.</span></span> 

>[!NOTE]
><span data-ttu-id="97d64-105">Tooreview hello emin olun [genel bakış](media-services-streaming-endpoints-overview.md) konu.</span><span class="sxs-lookup"><span data-stu-id="97d64-105">Make sure tooreview hello [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> 

<span data-ttu-id="97d64-106">Nasıl tooscale hello akış uç noktası hakkında daha fazla bilgi için bkz: [bu](media-services-portal-scale-streaming-endpoints.md) konu.</span><span class="sxs-lookup"><span data-stu-id="97d64-106">For information about how tooscale hello streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="start-managing-streaming-endpoints"></a><span data-ttu-id="97d64-107">Akış uç noktalarını yönetmeye başlama</span><span class="sxs-lookup"><span data-stu-id="97d64-107">Start managing streaming endpoints</span></span> 

<span data-ttu-id="97d64-108">hesabınız için akış uç noktalarını yönetme toostart hello aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="97d64-108">toostart managing streaming endpoints for your account, do hello following.</span></span>

1. <span data-ttu-id="97d64-109">Merhaba, [Azure portal](https://portal.azure.com/), Azure Media Services hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="97d64-109">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="97d64-110">Merhaba, **ayarları** dikey penceresinde, select **akış uç noktaları**.</span><span class="sxs-lookup"><span data-stu-id="97d64-110">In hello **Settings** blade, select **Streaming endpoints**.</span></span>
   
    ![Akış uç noktası](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> <span data-ttu-id="97d64-112">Akış uç noktanızı çalışır durumda olduğunda yalnızca faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="97d64-112">You are only billed when your Streaming Endpoint is in running state.</span></span>

## <a name="adddelete-a-streaming-endpoint"></a><span data-ttu-id="97d64-113">Bir akış uç ekleme/silme</span><span class="sxs-lookup"><span data-stu-id="97d64-113">Add/delete a streaming endpoint</span></span>

>[!NOTE]
><span data-ttu-id="97d64-114">Merhaba varsayılan akış uç noktası silinemiyor.</span><span class="sxs-lookup"><span data-stu-id="97d64-114">hello default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="97d64-115">uç nokta kullanarak akış tooadd/delete Azure portal Merhaba, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="97d64-115">tooadd/delete streaming endpoint using hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="97d64-116">tooadd bir akış uç tıklatın hello **+ uç nokta** hello sayfanın üst kısmındaki hello.</span><span class="sxs-lookup"><span data-stu-id="97d64-116">tooadd a streaming endpoint, click hello **+ Endpoint** at hello top of hello page.</span></span> 

    <span data-ttu-id="97d64-117">Toohave düşünüyorsanız, birden çok akış uç noktaları isteyebilirsiniz farklı CDN'ler veya CDN ve doğrudan erişim.</span><span class="sxs-lookup"><span data-stu-id="97d64-117">You might want multiple Streaming Endpoints if you plan toohave different CDNs or a CDN and direct access.</span></span>

2. <span data-ttu-id="97d64-118">toodelete bir akış uç basın **silmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="97d64-118">toodelete a streaming endpoint, press **Delete** button.</span></span>      
3. <span data-ttu-id="97d64-119">Merhaba tıklatın **Başlat** düğmesini toostart hello akış uç noktası.</span><span class="sxs-lookup"><span data-stu-id="97d64-119">Click hello **Start** button toostart hello streaming endpoint.</span></span>
   
    ![Akış uç noktası](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <span data-ttu-id="97d64-121"><a id="configure_streaming_endpoints"></a>Merhaba akış uç noktasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="97d64-121"><a id="configure_streaming_endpoints"></a>Configuring hello Streaming Endpoint</span></span>
<span data-ttu-id="97d64-122">Akış uç noktası aşağıdaki özelliklere tooconfigure hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="97d64-122">Streaming Endpoint enables you tooconfigure hello following properties:</span></span>

* <span data-ttu-id="97d64-123">Erişim denetimi</span><span class="sxs-lookup"><span data-stu-id="97d64-123">Access control</span></span>
* <span data-ttu-id="97d64-124">Önbellek denetimi</span><span class="sxs-lookup"><span data-stu-id="97d64-124">Cache control</span></span>
* <span data-ttu-id="97d64-125">Site erişim ilkeleri arası</span><span class="sxs-lookup"><span data-stu-id="97d64-125">Cross site access policies</span></span>

<span data-ttu-id="97d64-126">Bu özellikler hakkında ayrıntılı bilgi için bkz: [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="97d64-126">For detailed information about these properties, see [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="97d64-127">Merhaba aşağıdakileri yaparak akış uç noktasını yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="97d64-127">You can configure streaming endpoint by doing hello following:</span></span>

1. <span data-ttu-id="97d64-128">Akış uç noktası tooconfigure istediğiniz hello seçin.</span><span class="sxs-lookup"><span data-stu-id="97d64-128">Select hello streaming endpoint you want tooconfigure.</span></span>
2. <span data-ttu-id="97d64-129">Tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="97d64-129">Click **Settings**.</span></span>

<span data-ttu-id="97d64-130">Merhaba alanları kısa bir açıklamasını izler.</span><span class="sxs-lookup"><span data-stu-id="97d64-130">A brief description of hello fields follows.</span></span>

![Akış uç noktası](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. <span data-ttu-id="97d64-132">En büyük önbellek İlkesi: varlıklar için kullanılan tooconfigure önbellek ömrünü Bu akış uç noktası aracılığıyla sunulan.</span><span class="sxs-lookup"><span data-stu-id="97d64-132">Maximum cache policy: used tooconfigure cache lifetime for assets served through this streaming endpoint.</span></span> <span data-ttu-id="97d64-133">Herhangi bir değer ayarlarsanız, hello varsayılan kullanılır.</span><span class="sxs-lookup"><span data-stu-id="97d64-133">If no value is set, hello default is used.</span></span> <span data-ttu-id="97d64-134">Merhaba varsayılan değerleri de doğrudan Azure depolama alanında tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="97d64-134">hello default values can also be defined directly in Azure storage.</span></span> <span data-ttu-id="97d64-135">Azure CDN akış uç noktası Merhaba etkinleştirilirse, hello önbellek İlkesi değeri tooless 600 saniye daha ayarlanmadı.</span><span class="sxs-lookup"><span data-stu-id="97d64-135">If Azure CDN is enabled for hello streaming endpoint, you should not set hello cache policy value tooless than 600 seconds.</span></span>  
2. <span data-ttu-id="97d64-136">İzin verilen IP adreslerini: tooconnect toohello yayımlanan akış uç izin toospecify IP adresleri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="97d64-136">Allowed IP addresses: used toospecify IP addresses that would be allowed tooconnect toohello published streaming endpoint.</span></span> <span data-ttu-id="97d64-137">Belirtilen IP adresleri ise, herhangi bir IP adresi mümkün tooconnect olabilir.</span><span class="sxs-lookup"><span data-stu-id="97d64-137">If no IP addresses specified, any IP address would be able tooconnect.</span></span> <span data-ttu-id="97d64-138">IP adresleri, tek bir IP adresi (örneğin, ' 10.0.0.1'), bir IP adresi ve CIDR alt ağ maskesi (örneğin, ' 10.0.0.1/22') kullanarak bir IP aralığı veya IP adresi ve noktalı ondalık alt ağ maskesi kullanarak bir IP aralığı belirtilebilir (örneğin, 10.0.0.1 ' () 255.255.255.0)').</span><span class="sxs-lookup"><span data-stu-id="97d64-138">IP addresses can be specified as either a single IP address (for example, '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (for example, '10.0.0.1/22'), or an IP range using IP address and a dotted decimal subnet mask (for example, '10.0.0.1(255.255.255.0)').</span></span>
3. <span data-ttu-id="97d64-139">Akamai imzası üstbilgi kimlik doğrulaması için yapılandırma: İmza üstbilgi kimlik doğrulama isteği Akamai sunucularından nasıl yapılandırılır toospecify kullanılır.</span><span class="sxs-lookup"><span data-stu-id="97d64-139">Configuration for Akamai signature header authentication: used toospecify how signature header authentication request from Akamai servers is configured.</span></span> <span data-ttu-id="97d64-140">Süre sonu UTC biçiminde değil.</span><span class="sxs-lookup"><span data-stu-id="97d64-140">Expiration is in UTC.</span></span>

## <a name="scale-your-premium-streaming-endpoint"></a><span data-ttu-id="97d64-141">Akış uç noktası, Premium ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="97d64-141">Scale your Premium streaming endpoint</span></span>

<span data-ttu-id="97d64-142">Daha fazla bilgi için [bu](media-services-portal-scale-streaming-endpoints.md) konu başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="97d64-142">For more information, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <span data-ttu-id="97d64-143"><a id="enable_cdn"></a>Azure CDN tümleştirmeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="97d64-143"><a id="enable_cdn"></a>Enable Azure CDN integration</span></span>

<span data-ttu-id="97d64-144">Yeni bir hesap oluşturduğunuzda, varsayılan akış uç noktası Azure CDN tümleştirme varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="97d64-144">When you create a new account, default Streaming Endpoint Azure CDN integration is enabled by default.</span></span>

<span data-ttu-id="97d64-145">Daha sonra toodisable/enable hello CDN istiyorsanız, akış uç noktanızı hello olmalıdır **durduruldu** durumu.</span><span class="sxs-lookup"><span data-stu-id="97d64-145">If you later want toodisable/enable hello CDN, your streaming endpoint must be in hello **stopped** state.</span></span> <span data-ttu-id="97d64-146">Tüm hello arasında CDN POP saatlerini too2 hello değişiklikleri toobe etkin ve etkin hello Azure CDN tümleştirme tooget için sürebilir.</span><span class="sxs-lookup"><span data-stu-id="97d64-146">It could take up too2 hours for hello Azure CDN integration tooget enabled and for hello changes toobe active across all hello CDN POPs.</span></span> <span data-ttu-id="97d64-147">Ancak, can akış uç noktası ve akış kesintileri olmadan akış uç noktası hello başlatın ve hello tümleştirme tamamlandıktan sonra CDN hello hello akış teslim edilecek.</span><span class="sxs-lookup"><span data-stu-id="97d64-147">However, your can start your streaming endpoint and stream without interruptions from hello streaming endpoint and once hello integration is complete, hello stream will be delivered from hello CDN.</span></span> <span data-ttu-id="97d64-148">Akış uç noktanızı olacak süresi sağlama hello sırasında **başlangıç** durumu ve degredad performans gözlemlemek.</span><span class="sxs-lookup"><span data-stu-id="97d64-148">During hello provisioning period your streaming endpoint will be in **starting** state and you might observe degredad performance.</span></span>

<span data-ttu-id="97d64-149">CDN tümleştirme tüm hello Azure veri merkezleri execpt Çin ve Federal Government bölgelerde etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="97d64-149">CDN integration is enabled in all hello Azure data centers execpt China and Federal Goverment regions.</span></span>

<span data-ttu-id="97d64-150">Etkinleştirildiğinde, hello **erişim denetimi**, **özel ana bilgisayar adı** ve **Akamai imzası kimlik doğrulaması** yapılandırması devre dışı.</span><span class="sxs-lookup"><span data-stu-id="97d64-150">Once it is enabled, hello **Access Control**, **Custom hostname** and **Akamai Signature authentication** configuration gets disabled.</span></span>
 
> [!IMPORTANT]
> <span data-ttu-id="97d64-151">Azure CDN ile Azure Media Services tümleştirme uygulandığını **verizon'dan Azure CDN** için standart akış uç noktaları.</span><span class="sxs-lookup"><span data-stu-id="97d64-151">Azure Media Services integration with Azure CDN is implemented on **Azure CDN from Verizon** for standard streaming endpoints.</span></span> <span data-ttu-id="97d64-152">Akış uç noktaları premium tüm kullanılarak yapılandırılabilir **Azure CDN fiyatlandırma katmanlarına ve sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="97d64-152">Premium streaming endpoints can be configured using all **Azure CDN pricing tiers and providers**.</span></span> <span data-ttu-id="97d64-153">Hello Azure CDN özellikler hakkında daha fazla bilgi için bkz: [CDN'ye genel bakış](../cdn/cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="97d64-153">For more information about Azure CDN features, see hello [CDN overview](../cdn/cdn-overview.md).</span></span>
 
### <a name="additional-considerations"></a><span data-ttu-id="97d64-154">Diğer konular</span><span class="sxs-lookup"><span data-stu-id="97d64-154">Additional considerations</span></span>

* <span data-ttu-id="97d64-155">CDN akış uç noktası için etkinleştirildiğinde, istemcileri doğrudan hello kaynaktan içerik isteğinde bulunamaz.</span><span class="sxs-lookup"><span data-stu-id="97d64-155">When CDN is enabled for a streaming endpoint, clients cannot request content directly from hello origin.</span></span> <span data-ttu-id="97d64-156">İçeriğinizi ile veya olmadan CDN hello özelliği tootest gerekiyorsa, CDN etkin olmayan başka bir akış uç noktası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97d64-156">If you need hello ability tootest your content with or without CDN, you can create another streaming endpoint that isn't CDN enabled.</span></span>
* <span data-ttu-id="97d64-157">CDN etkinleştirdikten sonra akış uç noktası ana bilgisayar adı kalır aynı hello.</span><span class="sxs-lookup"><span data-stu-id="97d64-157">Your streaming endpoint hostname remains hello same after enabling CDN.</span></span> <span data-ttu-id="97d64-158">CDN etkinleştirildikten sonra tüm değişiklikleri tooyour media services iş akışı toomake gerekmez.</span><span class="sxs-lookup"><span data-stu-id="97d64-158">You don’t need toomake any changes tooyour media services workflow after CDN is enabled.</span></span> <span data-ttu-id="97d64-159">Akış uç noktası ana bilgisayar adı strasbourg.streaming.mediaservices.windows.net, CDN etkinleştirdikten sonra Örneğin, hello tam aynı ana bilgisayar adı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="97d64-159">For example, if your streaming endpoint hostname is strasbourg.streaming.mediaservices.windows.net, after enabling CDN, hello exact same hostname is used.</span></span>
* <span data-ttu-id="97d64-160">Yeni akış uç noktaları için yeni bir uç noktası oluşturarak CDN etkinleştirebilirsiniz; Varolan akış uç noktaları için toofirst Dur hello endpoint ve ardından etkinleştir/devre dışı bırak hello CDN gerekir.</span><span class="sxs-lookup"><span data-stu-id="97d64-160">For new streaming endpoints, you can enable CDN simply by creating a new endpoint; for existing streaming endpoints, you need toofirst stop hello endpoint and then enable/disable hello CDN.</span></span>
* <span data-ttu-id="97d64-161">Akış uç noktası standart yalnızca kullanılarak yapılandırılabilir **standart Verizon CDN sağlayıcısı** Azure yönetim portalını kullanarak.</span><span class="sxs-lookup"><span data-stu-id="97d64-161">Standard streaming endpoint can only be configured using **Verizon Standard CDN provider** using Azure management portal.</span></span> <span data-ttu-id="97d64-162">Ancak, REST API'lerini kullanarak diğer Azure CDN sağlayıcıları etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97d64-162">However, you can enable other Azure CDN providers using REST APIs.</span></span>

## <a name="configure-cdn-profile"></a><span data-ttu-id="97d64-163">CDN profili yapılandırma</span><span class="sxs-lookup"><span data-stu-id="97d64-163">Configure CDN profile</span></span>

<span data-ttu-id="97d64-164">Merhaba seçerek hello CDN profili yapılandırabilirsiniz **yönetmek CDN** hello üst düğmesinden.</span><span class="sxs-lookup"><span data-stu-id="97d64-164">You can configure hello CDN profile by selecting hello **Manage CDN** button from hello top.</span></span>

![Akış uç noktası](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a><span data-ttu-id="97d64-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="97d64-166">Next steps</span></span>
<span data-ttu-id="97d64-167">Media Services öğrenme yollarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="97d64-167">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="97d64-168">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="97d64-168">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

