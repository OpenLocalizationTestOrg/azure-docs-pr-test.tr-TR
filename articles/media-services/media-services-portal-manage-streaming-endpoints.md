---
title: "Azure portal ile akış uç noktalarını yönetme | Microsoft Docs"
description: "Bu konu Azure portal ile akış uç noktalarını yönetme gösterir."
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
ms.openlocfilehash: 797dced6c3e2525730afa29987259cb9b435ba66
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-streaming-endpoints-with-the-azure-portal"></a><span data-ttu-id="77946-103">Azure portal ile akış uç noktalarını yönetme</span><span class="sxs-lookup"><span data-stu-id="77946-103">Manage streaming endpoints with the Azure portal</span></span>

<span data-ttu-id="77946-104">Bu konu, Azure portalında akış uç noktalarını yönetmek için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="77946-104">This topic shows  how to use the Azure portal to manage streaming endpoints.</span></span> 

>[!NOTE]
><span data-ttu-id="77946-105">Gözden geçirdiğinizden emin olun [genel bakış](media-services-streaming-endpoints-overview.md) konu.</span><span class="sxs-lookup"><span data-stu-id="77946-105">Make sure to review the [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> 

<span data-ttu-id="77946-106">Akış uç ölçeklendirme hakkında daha fazla bilgi için bkz: [bu](media-services-portal-scale-streaming-endpoints.md) konu.</span><span class="sxs-lookup"><span data-stu-id="77946-106">For information about how to scale the streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="start-managing-streaming-endpoints"></a><span data-ttu-id="77946-107">Akış uç noktalarını yönetmeye başlama</span><span class="sxs-lookup"><span data-stu-id="77946-107">Start managing streaming endpoints</span></span> 

<span data-ttu-id="77946-108">Hesabınız için akış uç noktalarını yönetmeye başlamak için aşağıdakileri yapın.</span><span class="sxs-lookup"><span data-stu-id="77946-108">To start managing streaming endpoints for your account, do the following.</span></span>

1. <span data-ttu-id="77946-109">[Azure portalında](https://portal.azure.com/) Azure Media Services hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="77946-109">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="77946-110">İçinde **ayarları** dikey penceresinde, select **akış uç noktaları**.</span><span class="sxs-lookup"><span data-stu-id="77946-110">In the **Settings** blade, select **Streaming endpoints**.</span></span>
   
    ![Akış uç noktası](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> <span data-ttu-id="77946-112">Akış uç noktanızı çalışır durumda olduğunda yalnızca faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="77946-112">You are only billed when your Streaming Endpoint is in running state.</span></span>

## <a name="adddelete-a-streaming-endpoint"></a><span data-ttu-id="77946-113">Bir akış uç ekleme/silme</span><span class="sxs-lookup"><span data-stu-id="77946-113">Add/delete a streaming endpoint</span></span>

>[!NOTE]
><span data-ttu-id="77946-114">Varsayılan akış uç silinemiyor.</span><span class="sxs-lookup"><span data-stu-id="77946-114">The default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="77946-115">Azure portalı kullanarak akış uç noktasını ekleme/silme için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="77946-115">To add/delete streaming endpoint using the Azure portal, do the following:</span></span>

1. <span data-ttu-id="77946-116">Akış uç noktası eklemek için tıklatın **+ uç nokta** sayfanın üst kısmındaki.</span><span class="sxs-lookup"><span data-stu-id="77946-116">To add a streaming endpoint, click the **+ Endpoint** at the top of the page.</span></span> 

    <span data-ttu-id="77946-117">Farklı CDN'ler veya CDN ve doğrudan erişimi olmasını planlıyorsanız, birden çok akış uç noktaları isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="77946-117">You might want multiple Streaming Endpoints if you plan to have different CDNs or a CDN and direct access.</span></span>

2. <span data-ttu-id="77946-118">Akış uç noktasını silmek için basın **silmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="77946-118">To delete a streaming endpoint, press **Delete** button.</span></span>      
3. <span data-ttu-id="77946-119">Tıklatın **Başlat** akış uç başlamak için Başlat.</span><span class="sxs-lookup"><span data-stu-id="77946-119">Click the **Start** button to start the streaming endpoint.</span></span>
   
    ![Akış uç noktası](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <span data-ttu-id="77946-121"><a id="configure_streaming_endpoints"></a>Akış uç noktasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="77946-121"><a id="configure_streaming_endpoints"></a>Configuring the Streaming Endpoint</span></span>
<span data-ttu-id="77946-122">Akış uç noktası aşağıdaki özellikleri yapılandırmanıza olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="77946-122">Streaming Endpoint enables you to configure the following properties:</span></span>

* <span data-ttu-id="77946-123">Erişim denetimi</span><span class="sxs-lookup"><span data-stu-id="77946-123">Access control</span></span>
* <span data-ttu-id="77946-124">Önbellek denetimi</span><span class="sxs-lookup"><span data-stu-id="77946-124">Cache control</span></span>
* <span data-ttu-id="77946-125">Site erişim ilkeleri arası</span><span class="sxs-lookup"><span data-stu-id="77946-125">Cross site access policies</span></span>

<span data-ttu-id="77946-126">Bu özellikler hakkında ayrıntılı bilgi için bkz: [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="77946-126">For detailed information about these properties, see [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="77946-127">Aşağıdakileri yaparak akış uç noktasını yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="77946-127">You can configure streaming endpoint by doing the following:</span></span>

1. <span data-ttu-id="77946-128">Yapılandırmak istediğiniz akış uç noktasını seçin.</span><span class="sxs-lookup"><span data-stu-id="77946-128">Select the streaming endpoint you want to configure.</span></span>
2. <span data-ttu-id="77946-129">Tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="77946-129">Click **Settings**.</span></span>

<span data-ttu-id="77946-130">Alanları kısa bir açıklamasını izler.</span><span class="sxs-lookup"><span data-stu-id="77946-130">A brief description of the fields follows.</span></span>

![Akış uç noktası](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. <span data-ttu-id="77946-132">En büyük önbellek İlkesi: Bu akış uç noktası aracılığıyla sunulan varlıklar için önbellek ömrünü yapılandırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="77946-132">Maximum cache policy: used to configure cache lifetime for assets served through this streaming endpoint.</span></span> <span data-ttu-id="77946-133">Herhangi bir değer ayarlarsanız varsayılan değer kullanılır.</span><span class="sxs-lookup"><span data-stu-id="77946-133">If no value is set, the default is used.</span></span> <span data-ttu-id="77946-134">Varsayılan değerleri de doğrudan Azure depolama alanında tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="77946-134">The default values can also be defined directly in Azure storage.</span></span> <span data-ttu-id="77946-135">Azure CDN akış uç noktası için etkinleştirilirse, önbellek İlkesi değeri 600 saniyeden daha kısa bir süre için ayarlamalısınız değil.</span><span class="sxs-lookup"><span data-stu-id="77946-135">If Azure CDN is enabled for the streaming endpoint, you should not set the cache policy value to less than 600 seconds.</span></span>  
2. <span data-ttu-id="77946-136">İzin verilen IP adreslerini: yayımlanan akış uç noktasına bağlanmasına izin IP adresleri belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="77946-136">Allowed IP addresses: used to specify IP addresses that would be allowed to connect to the published streaming endpoint.</span></span> <span data-ttu-id="77946-137">Belirtilen herhangi bir IP adresi varsa, herhangi bir IP adresi bağlanabilmesi.</span><span class="sxs-lookup"><span data-stu-id="77946-137">If no IP addresses specified, any IP address would be able to connect.</span></span> <span data-ttu-id="77946-138">IP adresleri, tek bir IP adresi (örneğin, ' 10.0.0.1'), bir IP adresi ve CIDR alt ağ maskesi (örneğin, ' 10.0.0.1/22') kullanarak bir IP aralığı veya IP adresi ve noktalı ondalık alt ağ maskesi kullanarak bir IP aralığı belirtilebilir (örneğin, 10.0.0.1 ' () 255.255.255.0)').</span><span class="sxs-lookup"><span data-stu-id="77946-138">IP addresses can be specified as either a single IP address (for example, '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (for example, '10.0.0.1/22'), or an IP range using IP address and a dotted decimal subnet mask (for example, '10.0.0.1(255.255.255.0)').</span></span>
3. <span data-ttu-id="77946-139">Akamai imzası üstbilgi kimlik doğrulaması için yapılandırma: İmza üstbilgi kimlik doğrulama isteği Akamai sunucularından nasıl yapılandırıldığını belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="77946-139">Configuration for Akamai signature header authentication: used to specify how signature header authentication request from Akamai servers is configured.</span></span> <span data-ttu-id="77946-140">Süre sonu UTC biçiminde değil.</span><span class="sxs-lookup"><span data-stu-id="77946-140">Expiration is in UTC.</span></span>

## <a name="scale-your-premium-streaming-endpoint"></a><span data-ttu-id="77946-141">Akış uç noktası, Premium ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="77946-141">Scale your Premium streaming endpoint</span></span>

<span data-ttu-id="77946-142">Daha fazla bilgi için [bu](media-services-portal-scale-streaming-endpoints.md) konu başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="77946-142">For more information, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <span data-ttu-id="77946-143"><a id="enable_cdn"></a>Azure CDN tümleştirmeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="77946-143"><a id="enable_cdn"></a>Enable Azure CDN integration</span></span>

<span data-ttu-id="77946-144">Yeni bir hesap oluşturduğunuzda, varsayılan akış uç noktası Azure CDN tümleştirme varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="77946-144">When you create a new account, default Streaming Endpoint Azure CDN integration is enabled by default.</span></span>

<span data-ttu-id="77946-145">Akış uç noktanızı olması gerekir, daha sonra devre dışı bırak/CDN etkinleştir istiyorsanız, **durduruldu** durumu.</span><span class="sxs-lookup"><span data-stu-id="77946-145">If you later want to disable/enable the CDN, your streaming endpoint must be in the **stopped** state.</span></span> <span data-ttu-id="77946-146">2 saate kadar etkin Azure CDN tümleştirme ve değişikliklerin tüm CDN POP etkin olması ele geçirebilir.</span><span class="sxs-lookup"><span data-stu-id="77946-146">It could take up to 2 hours for the Azure CDN integration to get enabled and for the changes to be active across all the CDN POPs.</span></span> <span data-ttu-id="77946-147">Ancak, can akış uç noktası ve akış kesintileri olmadan akış uç noktasından başlatın ve tümleştirme tamamlandıktan sonra CDN akış teslim edilecek.</span><span class="sxs-lookup"><span data-stu-id="77946-147">However, your can start your streaming endpoint and stream without interruptions from the streaming endpoint and once the integration is complete, the stream will be delivered from the CDN.</span></span> <span data-ttu-id="77946-148">Akış uç noktanızı olacak sağlama süresi boyunca **başlangıç** durumu ve degredad performans gözlemlemek.</span><span class="sxs-lookup"><span data-stu-id="77946-148">During the provisioning period your streaming endpoint will be in **starting** state and you might observe degredad performance.</span></span>

<span data-ttu-id="77946-149">CDN tümleştirme tüm Azure veri merkezleri execpt Çin ve Federal Government bölgelerde etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="77946-149">CDN integration is enabled in all the Azure data centers execpt China and Federal Goverment regions.</span></span>

<span data-ttu-id="77946-150">Etkinleştirildiğinde, **erişim denetimi**, **özel ana bilgisayar adı** ve **Akamai imzası kimlik doğrulaması** yapılandırması devre dışı.</span><span class="sxs-lookup"><span data-stu-id="77946-150">Once it is enabled, the **Access Control**, **Custom hostname** and **Akamai Signature authentication** configuration gets disabled.</span></span>
 
> [!IMPORTANT]
> <span data-ttu-id="77946-151">Azure CDN ile Azure Media Services tümleştirme uygulandığını **verizon'dan Azure CDN** için standart akış uç noktaları.</span><span class="sxs-lookup"><span data-stu-id="77946-151">Azure Media Services integration with Azure CDN is implemented on **Azure CDN from Verizon** for standard streaming endpoints.</span></span> <span data-ttu-id="77946-152">Akış uç noktaları premium tüm kullanılarak yapılandırılabilir **Azure CDN fiyatlandırma katmanlarına ve sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="77946-152">Premium streaming endpoints can be configured using all **Azure CDN pricing tiers and providers**.</span></span> <span data-ttu-id="77946-153">Azure CDN özellikler hakkında daha fazla bilgi için bkz: [CDN'ye genel bakış](../cdn/cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="77946-153">For more information about Azure CDN features, see the [CDN overview](../cdn/cdn-overview.md).</span></span>
 
### <a name="additional-considerations"></a><span data-ttu-id="77946-154">Diğer konular</span><span class="sxs-lookup"><span data-stu-id="77946-154">Additional considerations</span></span>

* <span data-ttu-id="77946-155">CDN akış uç noktası için etkinleştirildiğinde, istemcileri doğrudan kaynaktan içerik isteğinde bulunamaz.</span><span class="sxs-lookup"><span data-stu-id="77946-155">When CDN is enabled for a streaming endpoint, clients cannot request content directly from the origin.</span></span> <span data-ttu-id="77946-156">İçeriğinizi ile veya olmadan CDN test olanağı gerekiyorsa, CDN etkin olmayan başka bir akış uç noktası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="77946-156">If you need the ability to test your content with or without CDN, you can create another streaming endpoint that isn't CDN enabled.</span></span>
* <span data-ttu-id="77946-157">Akış uç noktası ana bilgisayar adı aynı CDN etkinleştirdikten sonra kalır.</span><span class="sxs-lookup"><span data-stu-id="77946-157">Your streaming endpoint hostname remains the same after enabling CDN.</span></span> <span data-ttu-id="77946-158">CDN etkinleştirildikten sonra media services iş akışınıza değişiklik gerekmez.</span><span class="sxs-lookup"><span data-stu-id="77946-158">You don’t need to make any changes to your media services workflow after CDN is enabled.</span></span> <span data-ttu-id="77946-159">Akış uç noktası ana bilgisayar adı strasbourg.streaming.mediaservices.windows.net, CDN etkinleştirdikten sonra Örneğin, tam aynı ana bilgisayar adı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="77946-159">For example, if your streaming endpoint hostname is strasbourg.streaming.mediaservices.windows.net, after enabling CDN, the exact same hostname is used.</span></span>
* <span data-ttu-id="77946-160">Yeni akış uç noktaları için yeni bir uç noktası oluşturarak CDN etkinleştirebilirsiniz; Varolan akış uç noktaları için ilk uç noktayı durdurmak ve ardından CDN bırakmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="77946-160">For new streaming endpoints, you can enable CDN simply by creating a new endpoint; for existing streaming endpoints, you need to first stop the endpoint and then enable/disable the CDN.</span></span>
* <span data-ttu-id="77946-161">Akış uç noktası standart yalnızca kullanılarak yapılandırılabilir **standart Verizon CDN sağlayıcısı** Azure yönetim portalını kullanarak.</span><span class="sxs-lookup"><span data-stu-id="77946-161">Standard streaming endpoint can only be configured using **Verizon Standard CDN provider** using Azure management portal.</span></span> <span data-ttu-id="77946-162">Ancak, REST API'lerini kullanarak diğer Azure CDN sağlayıcıları etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="77946-162">However, you can enable other Azure CDN providers using REST APIs.</span></span>

## <a name="configure-cdn-profile"></a><span data-ttu-id="77946-163">CDN profili yapılandırma</span><span class="sxs-lookup"><span data-stu-id="77946-163">Configure CDN profile</span></span>

<span data-ttu-id="77946-164">CDN profili seçerek yapılandırabileceğiniz **yönetmek CDN** üstten düğme.</span><span class="sxs-lookup"><span data-stu-id="77946-164">You can configure the CDN profile by selecting the **Manage CDN** button from the top.</span></span>

![Akış uç noktası](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a><span data-ttu-id="77946-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="77946-166">Next steps</span></span>
<span data-ttu-id="77946-167">Media Services öğrenme yollarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="77946-167">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="77946-168">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="77946-168">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

