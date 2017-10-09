---
title: "aaaUsing PlayReady ve/veya Widevine dinamik ortak şifreleme | Microsoft Docs"
description: "Microsoft Azure Media Services, Microsoft PlayReady DRM korumalı, toodeliver MPEG-DASH, kesintisiz akış ve Http canlı akış (HLS) akışlar sağlar. Ayrıca, Widevine DRM ile şifrelenmiş DASH toodelivery sağlar. Bu konu, toodynamically nasıl şifrelemek PlayReady ve Widevine DRM ile gösterir."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 548d1a12-e2cb-45fe-9307-4ec0320567a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 0475e6ec80dcf39eb4e5c4ad4d17f821502951bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-playready-andor-widevine-dynamic-common-encryption"></a><span data-ttu-id="e182b-105">PlayReady ve/veya Widevine dinamik ortak şifreleme kullanma</span><span class="sxs-lookup"><span data-stu-id="e182b-105">Using PlayReady and/or Widevine dynamic common encryption</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e182b-106">.NET</span><span class="sxs-lookup"><span data-stu-id="e182b-106">.NET</span></span>](media-services-protect-with-drm.md)
> * [<span data-ttu-id="e182b-107">Java</span><span class="sxs-lookup"><span data-stu-id="e182b-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="e182b-108">PHP</span><span class="sxs-lookup"><span data-stu-id="e182b-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
>
>

<span data-ttu-id="e182b-109">Microsoft Azure Media Services sağlar toodeliver MPEG-DASH, kesintisiz akış ve HTTP canlı akış (HLS) akışlar ile korunan [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="e182b-109">Microsoft Azure Media Services enables you toodeliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="e182b-110">Ayrıca, Widevine DRM lisansına sahip toodeliver şifrelenmiş DASH akışları sağlar.</span><span class="sxs-lookup"><span data-stu-id="e182b-110">It also enables you toodeliver encrypted DASH streams with Widevine DRM licenses.</span></span> <span data-ttu-id="e182b-111">PlayReady ve Widevine, ortak şifreleme (ISO/IEC 23001-7 CENC) belirtimi hello şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="e182b-111">Both PlayReady and Widevine are encrypted per hello Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span> <span data-ttu-id="e182b-112">Kullanabileceğiniz [AMS .NET SDK'sı](https://www.nuget.org/packages/windowsazure.mediaservices/) (3.5.1 hello sürümünden başlayarak) veya API tooconfigure, AssetDeliveryConfiguration toouse Widevine getirin.</span><span class="sxs-lookup"><span data-stu-id="e182b-112">You can use [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (starting with hello version 3.5.1) or REST API tooconfigure your AssetDeliveryConfiguration toouse Widevine.</span></span>

<span data-ttu-id="e182b-113">Media Services, PlayReady ve Widevine DRM lisansları teslim etmek üzere bir hizmet sunar.</span><span class="sxs-lookup"><span data-stu-id="e182b-113">Media Services provides a service for delivering PlayReady and Widevine DRM licenses.</span></span> <span data-ttu-id="e182b-114">Media Services de hello haklarını yapılandırmanıza olanak tanıyan API'ler sağlar ve hello PlayReady veya Widevine DRM çalışma zamanı tooenforce için bir kullanıcı istediğiniz kısıtlamaları oynar geri korumalı içeriği.</span><span class="sxs-lookup"><span data-stu-id="e182b-114">Media Services also provides APIs that let you configure hello rights and restrictions that you want for hello PlayReady or Widevine DRM runtime tooenforce when a user plays back protected content.</span></span> <span data-ttu-id="e182b-115">Kullanıcı DRM korumalı bir içerik istediğinde, Merhaba oynatıcı uygulaması hello AMS lisans hizmetinden bir lisans ister.</span><span class="sxs-lookup"><span data-stu-id="e182b-115">When a user requests a DRM protected content, hello player application will request a license from hello AMS license service.</span></span> <span data-ttu-id="e182b-116">yetkili olup olmadığını hello AMS lisans hizmeti bir lisans toohello oynatıcı gönderirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e182b-116">hello AMS license service will issue a license toohello player if it is authorized.</span></span> <span data-ttu-id="e182b-117">PlayReady veya Widevine lisans hello istemci player toodecrypt ve akış Merhaba içeriğine tarafından kullanılan hello şifre çözme anahtarını içerir.</span><span class="sxs-lookup"><span data-stu-id="e182b-117">A PlayReady or Widevine license contains hello decryption key that can be used by hello client player toodecrypt and stream hello content.</span></span>

<span data-ttu-id="e182b-118">Widevine lisansları teslim AMS ortaklarını toohelp aşağıdaki hello de kullanabilirsiniz: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="e182b-118">You can also use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span> <span data-ttu-id="e182b-119">Daha fazla bilgi için [Axinom](media-services-axinom-integration.md) ve [castLabs](media-services-castlabs-integration.md) ile tümleştirme makalelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="e182b-119">For more information, see: integration with [Axinom](media-services-axinom-integration.md) and [castLabs](media-services-castlabs-integration.md).</span></span>

<span data-ttu-id="e182b-120">Media Services, anahtar isteğinde bulunan kullanıcıları yetkilendirmenin birden çok yöntemini destekler.</span><span class="sxs-lookup"><span data-stu-id="e182b-120">Media Services supports multiple ways of authorizing users who make key requests.</span></span> <span data-ttu-id="e182b-121">Merhaba içerik anahtarı yetkilendirme ilkesini bir veya daha fazla yetkilendirme kısıtlamaları olabilir: açık veya belirteç kısıtlama.</span><span class="sxs-lookup"><span data-stu-id="e182b-121">hello content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="e182b-122">Merhaba belirteç kısıtlamalı ilkenin, bir güvenli belirteç hizmeti (STS) tarafından verilmiş bir belirteç tarafından eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="e182b-122">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="e182b-123">Media Services hello belirteçleri destekler [basit Web belirteçleri](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) biçimi ve [JSON Web belirteci](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) biçimi.</span><span class="sxs-lookup"><span data-stu-id="e182b-123">Media Services supports tokens in hello [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) format and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) format.</span></span> <span data-ttu-id="e182b-124">Daha fazla bilgi için yapılandırma hello içerik anahtarının yetkilendirme ilkesini bakın.</span><span class="sxs-lookup"><span data-stu-id="e182b-124">For more information, see Configure hello content key’s authorization policy.</span></span>

<span data-ttu-id="e182b-125">tootake avantajı dinamik şifrelenmesi toohave Çoklu bit hızlı MP4 dosyası ya da Çoklu bit hızlı kesintisiz akış kaynak dosyası içeren bir varlık gerekir.</span><span class="sxs-lookup"><span data-stu-id="e182b-125">tootake advantage of dynamic encryption, you need toohave an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="e182b-126">(Bu konunun ilerleyen bölümlerinde açıklanan) hello varlık için tooconfigure hello teslim ilkeleri de gerekir.</span><span class="sxs-lookup"><span data-stu-id="e182b-126">You also need tooconfigure hello delivery policies for hello asset (described later in this topic).</span></span> <span data-ttu-id="e182b-127">Ardından, akış URL'si hello belirtilen hello biçime bağlı olarak, hello isteğe bağlı Akış sunucusu bu hello akış seçmiş olduğunuz hello protokolde teslim güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="e182b-127">Then, based on hello format specified in hello streaming URL, hello On-Demand Streaming server will ensure that hello stream is delivered in hello protocol you have chosen.</span></span> <span data-ttu-id="e182b-128">Sonuç olarak, yalnızca toostore gerekir ve tek bir depolama biçiminde ve Media Services hello dosyaları ödeme hello her istemciden gelen isteklere göre uygun HTTP yanıtı derler ve.</span><span class="sxs-lookup"><span data-stu-id="e182b-128">As a result, you only need toostore and pay for hello files in a single storage format and Media Services will build and serve hello appropriate HTTP response based on each request from a client.</span></span>

<span data-ttu-id="e182b-129">Bu konuda benzeri PlayReady ve Widevine gibi birden çok DRM ile korunan medya teslim uygulamalar üzerinde çalışmak yararlı toodevelopers olacaktır.</span><span class="sxs-lookup"><span data-stu-id="e182b-129">This topic would be useful toodevelopers that work on applications that deliver media protected with multiple DRMs, such as PlayReady and Widevine.</span></span> <span data-ttu-id="e182b-130">Merhaba konu nasıl tooconfigure hello PlayReady lisans teslimat hizmetinin Yetkilendirme İlkeleri ile yalnızca yetkili istemcilerin PlayReady veya Widevine lisansları alabilmesini olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="e182b-130">hello topic shows you how tooconfigure hello PlayReady license delivery service with authorization policies so that only authorized clients could receive PlayReady or Widevine licenses.</span></span> <span data-ttu-id="e182b-131">Ayrıca gösterir nasıl toouse dinamik şifrelemenin PlayReady veya Widevine DRM tire üzerinden.</span><span class="sxs-lookup"><span data-stu-id="e182b-131">It also shows how toouse dynamic encryption encryption with PlayReady or Widevine DRM over DASH.</span></span>

>[!NOTE]
><span data-ttu-id="e182b-132">AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu.</span><span class="sxs-lookup"><span data-stu-id="e182b-132">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="e182b-133">İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu.</span><span class="sxs-lookup"><span data-stu-id="e182b-133">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

## <a name="download-sample"></a><span data-ttu-id="e182b-134">Örnek indirme</span><span class="sxs-lookup"><span data-stu-id="e182b-134">Download sample</span></span>
<span data-ttu-id="e182b-135">Bu makalede açıklanan hello örnek indirebilirsiniz [burada](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).</span><span class="sxs-lookup"><span data-stu-id="e182b-135">You can download hello sample described in this article from [here](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).</span></span>

## <a name="configuring-dynamic-common-encryption-and-drm-license-delivery-services"></a><span data-ttu-id="e182b-136">Dinamik Ortak Şifreleme ve DRM Lisans Teslimat Hizmetlerini Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e182b-136">Configuring Dynamic Common Encryption and DRM License Delivery Services</span></span>

<span data-ttu-id="e182b-137">Merhaba, hello Media Services lisans teslimat hizmeti ve dinamik şifreleme kullanarak PlayReady ile varlıklarınızı korurken tooperform gerekir genel adımlar verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e182b-137">hello following are general steps that you would need tooperform when protecting your assets with PlayReady, using hello Media Services license delivery service, and also using dynamic encryption.</span></span>

1. <span data-ttu-id="e182b-138">Bir varlık oluşturun ve dosyaları hello varlığa yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e182b-138">Create an asset and upload files into hello asset.</span></span>
2. <span data-ttu-id="e182b-139">Merhaba varlık içeren hello dosya toohello Uyarlamalı bit hızı MP4 kümesine kodlayın.</span><span class="sxs-lookup"><span data-stu-id="e182b-139">Encode hello asset containing hello file toohello adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="e182b-140">Bir içerik anahtarı oluşturup kodlanmış hello varlıkla ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="e182b-140">Create a content key and associate it with hello encoded asset.</span></span> <span data-ttu-id="e182b-141">Media Services'de hello içerik anahtarı hello varlığın şifreleme anahtarını içerir.</span><span class="sxs-lookup"><span data-stu-id="e182b-141">In Media Services, hello content key contains hello asset’s encryption key.</span></span>
4. <span data-ttu-id="e182b-142">Merhaba içerik anahtarının yetkilendirme ilkesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e182b-142">Configure hello content key’s authorization policy.</span></span> <span data-ttu-id="e182b-143">Merhaba içerik anahtarı yetkilendirme ilkesinin tarafınızdan yapılandırılması ve hello içerik anahtar toobe teslim toohello istemcisi için sırayla hello istemci tarafından karşılanır.</span><span class="sxs-lookup"><span data-stu-id="e182b-143">hello content key authorization policy must be configured by you and met by hello client in order for hello content key toobe delivered toohello client.</span></span>

    <span data-ttu-id="e182b-144">Merhaba içerik anahtarı yetkilendirme ilkesini oluştururken toospecify hello aşağıdaki gerekir: teslim yöntemi (PlayReady veya Widevine), kısıtlamalar (açık veya belirteç) ve başlangıç anahtarı nasıl teslim edildiğini tanımlayan bilgileri belirli toohello anahtar teslim türüne toohello istemci ([PlayReady](media-services-playready-license-template-overview.md) veya [Widevine](media-services-widevine-license-template-overview.md) lisans şablonu).</span><span class="sxs-lookup"><span data-stu-id="e182b-144">When creating hello content key authorization policy, you need toospecify hello following: delivery method (PlayReady or Widevine), restrictions (open or token), and information specific toohello key delivery type that defines how hello key is delivered toohello client ([PlayReady](media-services-playready-license-template-overview.md) or [Widevine](media-services-widevine-license-template-overview.md) license template).</span></span>

5. <span data-ttu-id="e182b-145">Bir varlık için Hello teslim ilkesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e182b-145">Configure hello delivery policy for an asset.</span></span> <span data-ttu-id="e182b-146">Merhaba teslim ilkesi yapılandırması içerir: teslim Protokolü (örneğin, MPEG DASH, HLS, kesintisiz akış veya tümü), hello dinamik şifreleme (örneğin, ortak şifreleme), PlayReady veya Widevine lisans edinme URL'si.</span><span class="sxs-lookup"><span data-stu-id="e182b-146">hello delivery policy configuration includes: delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all), hello type of dynamic encryption (for example, Common Encryption), PlayReady or Widevine license acquisition URL.</span></span>

    <span data-ttu-id="e182b-147">Merhaba üzerinde farklı ilke tooeach Protokolü uygulayabilir aynı varlık.</span><span class="sxs-lookup"><span data-stu-id="e182b-147">You could apply different policy tooeach protocol on hello same asset.</span></span> <span data-ttu-id="e182b-148">Örneğin, PlayReady şifreleme tooSmooth/DASH ve AES zarfı tooHLS uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e182b-148">For example, you could apply PlayReady encryption tooSmooth/DASH and AES Envelope tooHLS.</span></span> <span data-ttu-id="e182b-149">Bir teslim ilkesinde tanımlanmayan tüm protokollerin (örneğin, yalnızca hello protokol olarak HLS belirten tek bir ilke ekliyorsunuz) akışla aktarılması engellenir.</span><span class="sxs-lookup"><span data-stu-id="e182b-149">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="e182b-150">Merhaba özel durum toothis hiç tanımlanmış hiçbir varlık teslim ilkesini varsa ' dir.</span><span class="sxs-lookup"><span data-stu-id="e182b-150">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="e182b-151">Ardından, tüm protokoller hello Temizle izin verilir.</span><span class="sxs-lookup"><span data-stu-id="e182b-151">Then, all protocols will be allowed in hello clear.</span></span>

6. <span data-ttu-id="e182b-152">Bir OnDemand Bulucu sipariş tooget bir akış URL'si oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e182b-152">Create an OnDemand locator in order tooget a streaming URL.</span></span>

<span data-ttu-id="e182b-153">Hello hello konunun sonunda eksiksiz bir .NET örneği bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e182b-153">You will find a complete .NET example at hello end of hello topic.</span></span>

<span data-ttu-id="e182b-154">Görüntü aşağıdaki hello yukarıda açıklanan hello akışı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e182b-154">hello following image demonstrates hello workflow described above.</span></span> <span data-ttu-id="e182b-155">Burada hello belirteci kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e182b-155">Here hello token is used for authentication.</span></span>

![PlayReady ile koruma](./media/media-services-content-protection-overview/media-services-content-protection-with-drm.png)

<span data-ttu-id="e182b-157">Bu konunun geri kalanında Hello ayrıntılı açıklamalar, kod örnekleri ve nasıl tooachieve hello yukarıda açıklanan görevleri göster bağlantılar tootopics sağlar.</span><span class="sxs-lookup"><span data-stu-id="e182b-157">hello rest of this topic provides detailed explanations, code examples, and links tootopics that show you how tooachieve hello tasks described above.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="e182b-158">Geçerli sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="e182b-158">Current limitations</span></span>
<span data-ttu-id="e182b-159">Eklemek veya bir varlık teslim ilkesini güncelleştirmek, hello ilişkili Bulucuyu (varsa) silin ve yeni bir Bulucu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e182b-159">If you add or update an asset delivery policy, you must delete hello associated locator (if any) and create a new locator.</span></span>

<span data-ttu-id="e182b-160">Azure Media Services aracılığıyla Widevine ile şifrelerken sınırlama: Şu anda, birden çok içerik anahtarı desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="e182b-160">Limitation when encrypting with Widevine with Azure Media Services: currently, multiple content keys are not supported.</span></span>

## <a name="create-an-asset-and-upload-files-into-hello-asset"></a><span data-ttu-id="e182b-161">Bir varlık oluşturun ve dosyaları hello varlığa yükleyin</span><span class="sxs-lookup"><span data-stu-id="e182b-161">Create an asset and upload files into hello asset</span></span>
<span data-ttu-id="e182b-162">Sipariş toomanage kodlamak ve videolarınızı, akış içeriğinizi önce Microsoft Azure Media Services'e yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e182b-162">In order toomanage, encode, and stream your videos, you must first upload your content into Microsoft Azure Media Services.</span></span> <span data-ttu-id="e182b-163">Yüklenmesinin ardından içeriğiniz daha fazla işleme ve akış hello bulutta güvenli bir şekilde depolanır.</span><span class="sxs-lookup"><span data-stu-id="e182b-163">Once uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="e182b-164">Ayrıntılı bilgi için bkz. [Media Services hesabına dosya yükleme](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="e182b-164">For detailed information, see [Upload Files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <a name="encode-hello-asset-containing-hello-file-toohello-adaptive-bitrate-mp4-set"></a><span data-ttu-id="e182b-165">Merhaba varlık içeren hello dosya toohello Uyarlamalı bit hızı MP4 kümesine kodlayın</span><span class="sxs-lookup"><span data-stu-id="e182b-165">Encode hello asset containing hello file toohello adaptive bitrate MP4 set</span></span>
<span data-ttu-id="e182b-166">Dinamik şifreleme ile tek ihtiyacınız olan toocreate Çoklu bit hızlı MP4 dosyası ya da Çoklu bit hızlı kesintisiz akış kaynak dosyası içeren bir varlık.</span><span class="sxs-lookup"><span data-stu-id="e182b-166">With dynamic encryption all you need is toocreate an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="e182b-167">Merhaba hello bildiriminde belirtilen biçime bağlı olarak ve istek parçalara, hello isteğe bağlı Akış sunucusu, hello akış seçmiş olduğunuz hello protokolde almanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="e182b-167">Then, based on hello specified format in hello manifest and fragment request, hello On-Demand Streaming server will ensure that you receive hello stream in hello protocol you have chosen.</span></span> <span data-ttu-id="e182b-168">Sonuç olarak, yalnızca toostore gerekir ve tek bir depolama biçiminde ve Media Services hizmeti hello dosyaları ödeme hello istemciden gelen isteklere göre uygun yanıtı derler ve.</span><span class="sxs-lookup"><span data-stu-id="e182b-168">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span> <span data-ttu-id="e182b-169">Daha fazla bilgi için bkz: Merhaba [dinamik paketlemeye genel bakış](media-services-dynamic-packaging-overview.md) konu.</span><span class="sxs-lookup"><span data-stu-id="e182b-169">For more information, see hello [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) topic.</span></span>

<span data-ttu-id="e182b-170">Yönergeler için tooencode, bkz: [nasıl tooencode medya Kodlayıcı standart kullanarak bir varlık](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="e182b-170">For instructions on how tooencode, see [How tooencode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <span data-ttu-id="e182b-171"><a id="create_contentkey"></a>Bir içerik anahtarı oluşturup kodlanmış hello varlıkla ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="e182b-171"><a id="create_contentkey"></a>Create a content key and associate it with hello encoded asset</span></span>
<span data-ttu-id="e182b-172">Media Services'de hello içerik anahtarı tooencrypt bir varlık istediğiniz başlangıç anahtarı içeren ile.</span><span class="sxs-lookup"><span data-stu-id="e182b-172">In Media Services, hello content key contains hello key that you want tooencrypt an asset with.</span></span>

<span data-ttu-id="e182b-173">Ayrıntılı bilgi için bkz. [İçerik anahtarı oluşturma](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="e182b-173">For detailed information, see [Create content key](media-services-dotnet-create-contentkey.md).</span></span>

## <span data-ttu-id="e182b-174"><a id="configure_key_auth_policy"></a>Merhaba içerik anahtarının yetkilendirme ilkesini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="e182b-174"><a id="configure_key_auth_policy"></a>Configure hello content key’s authorization policy</span></span>
<span data-ttu-id="e182b-175">Media Services, anahtar isteğinde bulunan kullanıcıların kimlik doğrulamasını yapmanın birden çok yöntemini destekler.</span><span class="sxs-lookup"><span data-stu-id="e182b-175">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="e182b-176">Merhaba içerik anahtarı yetkilendirme ilkesinin tarafınızdan yapılandırılması ve hello anahtar toobe toohello istemci teslim sırayla hello istemci (oynatıcı) tarafından karşılanır.</span><span class="sxs-lookup"><span data-stu-id="e182b-176">hello content key authorization policy must be configured by you and met by hello client (player) in order for hello key toobe delivered toohello client.</span></span> <span data-ttu-id="e182b-177">Merhaba içerik anahtarı yetkilendirme ilkesini bir veya daha fazla yetkilendirme kısıtlamaları olabilir: açık veya belirteç kısıtlama.</span><span class="sxs-lookup"><span data-stu-id="e182b-177">hello content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span>

<span data-ttu-id="e182b-178">Ayrıntılı bilgi için bkz. [İçerik Anahtarı Yetkilendirme İlkesini Yapılandırma](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).</span><span class="sxs-lookup"><span data-stu-id="e182b-178">For detailed information, see [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).</span></span>

## <span data-ttu-id="e182b-179"><a id="configure_asset_delivery_policy"></a>Varlık teslim ilkesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e182b-179"><a id="configure_asset_delivery_policy"></a>Configure asset delivery policy</span></span>
<span data-ttu-id="e182b-180">Varlığınıza Hello teslim ilkesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e182b-180">Configure hello delivery policy for your asset.</span></span> <span data-ttu-id="e182b-181">Varlık teslim ilkesi yapılandırması hello bazı şeyleri içerir:</span><span class="sxs-lookup"><span data-stu-id="e182b-181">Some things that hello asset delivery policy configuration includes:</span></span>

* <span data-ttu-id="e182b-182">Merhaba DRM lisans edinme URL'si.</span><span class="sxs-lookup"><span data-stu-id="e182b-182">hello DRM license acquisition URL.</span></span>
* <span data-ttu-id="e182b-183">Merhaba varlık teslim Protokolü (örneğin, MPEG DASH, HLS, kesintisiz akış veya tümü).</span><span class="sxs-lookup"><span data-stu-id="e182b-183">hello asset delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all).</span></span>
* <span data-ttu-id="e182b-184">(Bu durumda, ortak şifreleme) dinamik şifreleme türü Hello.</span><span class="sxs-lookup"><span data-stu-id="e182b-184">hello type of dynamic encryption (in this case, Common Encryption).</span></span>

<span data-ttu-id="e182b-185">Ayrıntılı bilgi için bkz. [Varlık teslim ilkesini yapılandırma](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="e182b-185">For detailed information, see [Configure asset delivery policy ](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <span data-ttu-id="e182b-186"><a id="create_locator"></a>Bir OnDemand Bulucu sipariş tooget bir akış URL'si içinde akış oluşturma</span><span class="sxs-lookup"><span data-stu-id="e182b-186"><a id="create_locator"></a>Create an OnDemand streaming locator in order tooget a streaming URL</span></span>
<span data-ttu-id="e182b-187">Kullanıcı URL'si kesintisiz, DASH veya HLS akış hello ile tooprovide gerekir.</span><span class="sxs-lookup"><span data-stu-id="e182b-187">You will need tooprovide your user with hello streaming URL for Smooth, DASH or HLS.</span></span>

> [!NOTE]
> <span data-ttu-id="e182b-188">Varlığınızın teslim ilkesini ekler veya güncelleştirirseniz, mevcut bulucuyu (varsa) silip yeni bir bulucu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e182b-188">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
>
>

<span data-ttu-id="e182b-189">Yönergeler için nasıl toopublish bir varlık ve yapı bir akış URL'si bkz [akış URL'si oluşturma](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="e182b-189">For instructions on how toopublish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="e182b-190">Test belirteci alma</span><span class="sxs-lookup"><span data-stu-id="e182b-190">Get a test token</span></span>
<span data-ttu-id="e182b-191">Merhaba hello anahtar yetkilendirme ilkesi için kullanılan belirteç kısıtlamasına dayalı bir test belirteci alın.</span><span class="sxs-lookup"><span data-stu-id="e182b-191">Get a test token based on hello token restriction that was used for hello key authorization policy.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string.
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);


<span data-ttu-id="e182b-192">Merhaba kullanabilirsiniz [AMS Oynatıcısı](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest akışınızı.</span><span class="sxs-lookup"><span data-stu-id="e182b-192">You can use hello [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest your stream.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="e182b-193">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e182b-193">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="e182b-194">Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="e182b-194">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="e182b-195">Öğeleri çok aşağıdaki hello eklemek**appSettings** app.config dosyasında tanımlanan:</span><span class="sxs-lookup"><span data-stu-id="e182b-195">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="e182b-196">Örnek</span><span class="sxs-lookup"><span data-stu-id="e182b-196">Example</span></span>

<span data-ttu-id="e182b-197">Merhaba aşağıdaki örnek, .net için Azure Media Services SDK'sı sunulan işlevini gösterir-(özellikle hello özelliği toodefine bir Widevine lisans şablonu ve Azure Media Services'den Widevine lisansı isteme) sürüm 3.5.2'de.</span><span class="sxs-lookup"><span data-stu-id="e182b-197">hello following sample demonstrates functionality that was introduced in Azure Media Services SDK for .Net -Version 3.5.2 (specifically, hello ability toodefine a Widevine license template and request a Widevine license from Azure Media Services).</span></span>

<span data-ttu-id="e182b-198">Bu bölümde gösterilen hello koduyla Hello kodu Program.cs dosyanızdaki üzerine.</span><span class="sxs-lookup"><span data-stu-id="e182b-198">Overwrite hello code in your Program.cs file with hello code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="e182b-199">Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için).</span><span class="sxs-lookup"><span data-stu-id="e182b-199">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="e182b-200">Merhaba kullanması gereken her zaman kullanıyorsanız, aynı ilke kimliği hello aynı gün / erişim izinlerini, örneğin, uzun bir süre (karşıya yükleme olmayan ilkeleri) yerinde hedeflenen tooremain olan bulucular ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="e182b-200">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="e182b-201">Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="e182b-201">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="e182b-202">Emin tooupdate değişkenleri, giriş dosyalarınızın bulunduğu toopoint toofolders olun.</span><span class="sxs-lookup"><span data-stu-id="e182b-202">Make sure tooupdate variables toopoint toofolders where your input files are located.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.Widevine;
    using Newtonsoft.Json;

    namespace DynamicEncryptionWithDRM
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        private static readonly Uri _sampleAudience =
            new Uri(ConfigurationManager.AppSettings["Audience"]);

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            bool tokenRestriction = false;
            string tokenTemplateString = null;

            IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
            Console.WriteLine("Uploaded asset: {0}", asset.Id);

            IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
            Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

            IContentKey key = CreateCommonTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("PlayReady License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense));
            Console.WriteLine();

            if (tokenRestriction)
            tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
            else
            AddOpenAuthorizationPolicy(key);

            Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
            Console.WriteLine();

            CreateAssetDeliveryPolicy(encodedAsset, key);
            Console.WriteLine("Created asset delivery policy. \n");
            Console.WriteLine();

            if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
            {
            // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
            // back into a TokenRestrictionTemplate class instance.
            TokenRestrictionTemplate tokenTemplate =
                TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

            // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello http://amsplayer.azurewebsites.net/azuremediaplayer.html player tootest streams.
            // Note that DASH works on IE 11 (via PlayReady), Edge (via PlayReady), Chrome (via Widevine).

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted DASH URL: {0}/manifest(format=mpd-time-csf)", url);

            Console.ReadLine();
        }

        static public IAsset UploadFileAndCreateAsset(string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
            Console.WriteLine("File does not exist.");
            return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
        {
            var encodingPreset = "Adaptive Streaming";

            IJob job = _context.Jobs.Create(String.Format("Encoding into Mp4 {0} too{1}",
                        inputAsset.Name,
                        encodingPreset));

            var mediaProcessors =
            _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

            var latestMediaProcessor =
            mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

            ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
            encodeTask.InputAssets.Add(inputAsset);
            encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset), AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }


        static public IContentKey CreateCommonTypeContentKey(IAsset asset)
        {

            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryption);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }

        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {

            // Create ContentKeyAuthorizationPolicy with Open restrictions
            // and create authorization policy          

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Open",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                    Requirements = null
                }
                };

            // Configure PlayReady and Widevine license templates.
            string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

            string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

            IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.PlayReadyLicense,
                restrictions, PlayReadyLicenseTemplate);

            IContentKeyAuthorizationPolicyOption WidevinePolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.Widevine,
                restrictions, WidevineLicenseTemplate);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common Content Key with no restrictions").
                Result;


            contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
            contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);
            // Associate hello content key authorization policy with hello content key.
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Token Authorization Policy",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                    Requirements = tokenTemplateString,
                }
                };

            // Configure PlayReady and Widevine license templates.
            string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

            string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

            IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.PlayReadyLicense,
                restrictions, PlayReadyLicenseTemplate);

            IContentKeyAuthorizationPolicyOption WidevinePolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.Widevine,
                restrictions, WidevineLicenseTemplate);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
            contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        static private string GenerateTokenRequirements()
        {
            TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

            template.PrimaryVerificationKey = new SymmetricVerificationKey();
            template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();
            template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

            return TokenRestrictionTemplateSerializer.Serialize(template);
        }

        static private string ConfigurePlayReadyLicenseTemplate()
        {
            // hello following code configures PlayReady License Template using .NET classes
            // and returns hello XML string.

            //hello PlayReadyLicenseResponseTemplate class represents hello template for hello response sent back toohello end user.
            //It contains a field for a custom data string between hello license server and hello application
            //(may be useful for custom app logic) as well as a list of one or more license templates.
            PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

            // hello PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
            // toobe returned toohello end users.
            //It contains hello data on hello content key in hello license and any rights or restrictions toobe
            //enforced by hello PlayReady DRM runtime when using hello content key.
            PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
            //Configure whether hello license is persistent (saved in persistent storage on hello client)
            //or non-persistent (only held in memory while hello player is using hello license).  
            licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

            // AllowTestDevices controls whether test devices can use hello license or not.  
            // If true, hello MinimumSecurityLevel property of hello license
            // is set too150.  If false (hello default), hello MinimumSecurityLevel property of hello license is set too2000.
            licenseTemplate.AllowTestDevices = true;

            // You can also configure hello Play Right in hello PlayReady license by using hello PlayReadyPlayRight class.
            // It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions
            // configured in hello license and on hello PlayRight itself (for playback specific policy).
            // Much of hello policy on hello PlayRight has toodo with output restrictions
            // which control hello types of outputs that hello content can be played over and
            // any restrictions that must be put in place when using a given output.
            // For example, if hello DigitalVideoOnlyContentRestriction is enabled,
            //then hello DRM runtime will only allow hello video toobe displayed over digital outputs
            //(analog video outputs won’t be allowed toopass hello content).

            //IMPORTANT: These types of restrictions can be very powerful but can also affect hello consumer experience.
            // If hello output protections are configured too restrictive,
            // hello content might be unplayable on some clients. For more information, see hello PlayReady Compliance Rules document.

            // For example:
            //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

            responseTemplate.LicenseTemplates.Add(licenseTemplate);

            return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
        }

        private static string ConfigureWidevineLicenseTemplate()
        {
            var template = new WidevineMessage
            {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                    new ContentKeySpecs
                    {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                    security_level = 1,
                    track_type = "SD"
                    }
                },
            policy_overrides = new
            {
                can_play = true,
                can_persist = true,
                can_renew = false
            }
            };

            string configuration = JsonConvert.SerializeObject(template);
            return configuration;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            // Get hello PlayReady license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);

            // GetKeyDeliveryUrl for Widevine attaches hello KID toohello URL.
            // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
            // hello WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption
            // tooappend /? KID =< keyId > toohello end of hello url when creating hello manifest.
            // As a result Widevine license acquisition URL will have KID appended twice,
            // so we need tooremove hello KID that in hello URL when we call GetKeyDeliveryUrl.

            Uri widevineUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine);
            UriBuilder uriBuilder = new UriBuilder(widevineUrl);
            uriBuilder.Query = String.Empty;
            widevineUrl = uriBuilder.Uri;

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
                    {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl, widevineUrl.ToString()}

            };

            // In this case we only specify Dash streaming protocol in hello delivery policy,
            // All other protocols will be blocked from streaming.
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }

        /// <summary>
        /// Gets hello streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator toohello streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL toohello manifest file.
            return originLocator.Path + assetFile.Name;
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int length)
        {
            var returnValue = new byte[length];

            using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
            {
            rng.GetBytes(returnValue);
            }

            return returnValue;
        }
        }
    }


## <a name="next-step"></a><span data-ttu-id="e182b-203">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="e182b-203">Next step</span></span>
<span data-ttu-id="e182b-204">Media Services öğrenme yollarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="e182b-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e182b-205">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="e182b-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="e182b-206">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="e182b-206">See also</span></span>
[<span data-ttu-id="e182b-207">Çoklu DRM ve Access Control ile CENC</span><span class="sxs-lookup"><span data-stu-id="e182b-207">CENC with Multi-DRM and Access Control</span></span>](media-services-cenc-with-multidrm-access-control.md)

[<span data-ttu-id="e182b-208">AMS ile Widevine paketlemeyi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e182b-208">Configure Widevine packaging with AMS</span></span>](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)

[<span data-ttu-id="e182b-209">Azure Media Services’ta Google Widevine lisans teslim hizmetleri ile tanışın</span><span class="sxs-lookup"><span data-stu-id="e182b-209">Announcing Google Widevine license delivery services in Azure Media Services</span></span>](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/)
