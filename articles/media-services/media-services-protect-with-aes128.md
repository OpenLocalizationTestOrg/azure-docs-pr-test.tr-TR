---
title: "aaaUsing AES-128 dinamik şifreleme ve anahtar teslim hizmeti | Microsoft Docs"
description: "Microsoft Azure Media Services, toodeliver AES 128 bit şifreleme anahtarları ile şifrelenmiş içeriğinizi sağlar. Media Services de şifreleme anahtarlarını tooauthorized kullanıcılar sunar hello anahtar teslim hizmeti sağlar. Bu konu, nasıl toodynamically AES-128 ile şifrelemek ve hello anahtar teslim Hizmeti'yle gösterir."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 4d2c10af-9ee0-408f-899b-33fa4c1d89b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: cb1b413ec2ba79f7437464099cf72236ab93f312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-aes-128-dynamic-encryption-and-key-delivery-service"></a><span data-ttu-id="44852-105">AES-128 dinamik şifreleme ve anahtar teslim hizmeti kullanma</span><span class="sxs-lookup"><span data-stu-id="44852-105">Using AES-128 dynamic encryption and key delivery service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="44852-106">.NET</span><span class="sxs-lookup"><span data-stu-id="44852-106">.NET</span></span>](media-services-protect-with-aes128.md)
> * [<span data-ttu-id="44852-107">Java</span><span class="sxs-lookup"><span data-stu-id="44852-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="44852-108">PHP</span><span class="sxs-lookup"><span data-stu-id="44852-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="44852-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="44852-109">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="44852-110">Bkz: [bu](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) tooprotect medyanızı AES şifreleme ile nasıl içerik genel bir bakış için video.</span><span class="sxs-lookup"><span data-stu-id="44852-110">See [this](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) video for an overview of how tooprotect your Media Content with AES encryption.</span></span>
> 
> 

<span data-ttu-id="44852-111">Microsoft Azure Media Services toodeliver Http canlı-akış (HLS) ve Gelişmiş Şifreleme Standardı ((128-bit şifreleme anahtarları kullanılarak) AES ile) şifrelenmiş kesintisiz akışlara sağlar.</span><span class="sxs-lookup"><span data-stu-id="44852-111">Microsoft Azure Media Services enables you toodeliver Http-Live-Streaming (HLS) and Smooth Streams encrypted with Advanced Encryption Standard (AES) (using 128-bit encryption keys).</span></span> <span data-ttu-id="44852-112">Media Services de şifreleme anahtarlarını tooauthorized kullanıcılar sunar hello anahtar teslim hizmeti sağlar.</span><span class="sxs-lookup"><span data-stu-id="44852-112">Media Services also provides hello Key Delivery service that delivers encryption keys tooauthorized users.</span></span> <span data-ttu-id="44852-113">Bir varlık için Media Services tooencrypt istiyorsanız, tooassociate hello varlık ile bir şifreleme anahtarı gerekir ve ayrıca hello anahtarı için yetkilendirme ilkelerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="44852-113">If you want for Media Services tooencrypt an asset, you need tooassociate an encryption key with hello asset and also configure authorization policies for hello key.</span></span> <span data-ttu-id="44852-114">Bir akış player tarafından istendiğinde Media Services belirtilen hello kullanan anahtar toodynamically AES şifreleme kullanarak içeriğinizi şifreleyin.</span><span class="sxs-lookup"><span data-stu-id="44852-114">When a stream is requested by a player, Media Services uses hello specified key toodynamically encrypt your content using AES encryption.</span></span> <span data-ttu-id="44852-115">toodecrypt hello akış hello anahtar teslim hizmetinden hello anahtar hello player isteyin.</span><span class="sxs-lookup"><span data-stu-id="44852-115">toodecrypt hello stream, hello player will request hello key from hello key delivery service.</span></span> <span data-ttu-id="44852-116">tooget hello anahtar desteklemediğini hello kullanıcıdır toodecide yetkili, hello hizmet hello anahtar için belirtilen hello yetkilendirme ilkelerini değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="44852-116">toodecide whether or not hello user is authorized tooget hello key, hello service evaluates hello authorization policies that you specified for hello key.</span></span>

<span data-ttu-id="44852-117">Media Services, anahtar isteğinde bulunan kullanıcıların kimlik doğrulamasını yapmanın birden çok yöntemini destekler.</span><span class="sxs-lookup"><span data-stu-id="44852-117">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="44852-118">Merhaba içerik anahtarı yetkilendirme ilkesini bir veya daha fazla yetkilendirme kısıtlamaları olabilir: açık veya belirteç kısıtlama.</span><span class="sxs-lookup"><span data-stu-id="44852-118">hello content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="44852-119">Merhaba belirteç kısıtlamalı ilkenin, bir güvenli belirteç hizmeti (STS) tarafından verilmiş bir belirteç tarafından eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="44852-119">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="44852-120">Media Services hello belirteçleri destekler [basit Web belirteçleri](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) biçimi ve [JSON Web belirteci](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) biçimi.</span><span class="sxs-lookup"><span data-stu-id="44852-120">Media Services supports tokens in hello [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) format and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) format.</span></span> <span data-ttu-id="44852-121">Daha fazla bilgi için bkz: [hello içerik anahtarının yetkilendirme ilkesini yapılandırma](media-services-protect-with-aes128.md#configure_key_auth_policy).</span><span class="sxs-lookup"><span data-stu-id="44852-121">For more information, see [Configure hello content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span>

<span data-ttu-id="44852-122">tootake avantajı dinamik şifrelenmesi toohave Çoklu bit hızlı MP4 dosyası ya da Çoklu bit hızlı kesintisiz akış kaynak dosyası içeren bir varlık gerekir.</span><span class="sxs-lookup"><span data-stu-id="44852-122">tootake advantage of dynamic encryption, you need toohave an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="44852-123">Ayrıca (Bu konunun ilerleyen bölümlerinde açıklanan) hello varlık için tooconfigure hello teslim ilkesini gerekir.</span><span class="sxs-lookup"><span data-stu-id="44852-123">You also need tooconfigure hello delivery policy for hello asset (described later in this topic).</span></span> <span data-ttu-id="44852-124">Ardından, akış URL'si hello belirtilen hello biçime bağlı olarak, hello isteğe bağlı Akış sunucusu bu hello akış seçmiş olduğunuz hello protokolde teslim güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="44852-124">Then, based on hello format specified in hello streaming URL, hello On-Demand Streaming server will ensure that hello stream is delivered in hello protocol you have chosen.</span></span> <span data-ttu-id="44852-125">Sonuç olarak, yalnızca toostore gerekir ve tek bir depolama biçiminde ve Media Services hizmeti hello dosyaları ödeme hello istemciden gelen isteklere göre uygun yanıtı derler ve.</span><span class="sxs-lookup"><span data-stu-id="44852-125">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="44852-126">Bu konu, korumalı medya teslim eden uygulamalar üzerinde çalışması yararlı toodevelopers olacaktır.</span><span class="sxs-lookup"><span data-stu-id="44852-126">This topic would be useful toodevelopers that work on applications that deliver protected media.</span></span> <span data-ttu-id="44852-127">Merhaba konu nasıl tooconfigure hello anahtar teslim hizmeti Yetkilendirme İlkeleri ile yalnızca yetkili istemcilerin hello şifreleme anahtarları alabilir böylece gösterir.</span><span class="sxs-lookup"><span data-stu-id="44852-127">hello topic shows you how tooconfigure hello key delivery service with authorization policies so that only authorized clients could receive hello encryption keys.</span></span> <span data-ttu-id="44852-128">Ayrıca gösterir nasıl toouse dinamik şifreleme.</span><span class="sxs-lookup"><span data-stu-id="44852-128">It also shows how toouse dynamic encryption.</span></span>


## <a name="aes-128-dynamic-encryption-and-key-delivery-service-workflow"></a><span data-ttu-id="44852-129">AES-128 dinamik şifreleme ve anahtar teslim hizmeti iş akışı</span><span class="sxs-lookup"><span data-stu-id="44852-129">AES-128 Dynamic Encryption and Key Delivery Service Workflow</span></span>

<span data-ttu-id="44852-130">Merhaba, varlıklarınızı hello Media Services anahtar teslimat hizmeti ve dinamik şifreleme kullanarak AES ile şifrelerken tooperform gerekir genel adımlar şunlardır.</span><span class="sxs-lookup"><span data-stu-id="44852-130">hello following are general steps that you would need tooperform when encrypting your assets with AES, using hello Media Services key delivery service, and also using dynamic encryption.</span></span>

1. <span data-ttu-id="44852-131">[Bir varlık oluşturun ve dosyaları hello varlığa yükleyin](media-services-protect-with-aes128.md#create_asset).</span><span class="sxs-lookup"><span data-stu-id="44852-131">[Create an asset and upload files into hello asset](media-services-protect-with-aes128.md#create_asset).</span></span>
2. <span data-ttu-id="44852-132">[Merhaba varlığı içeren Hello dosya toohello bit hızı Uyarlamalı MP4 kümesine kodlayın](media-services-protect-with-aes128.md#encode_asset).</span><span class="sxs-lookup"><span data-stu-id="44852-132">[Encode hello asset containing hello file toohello adaptive bitrate MP4 set](media-services-protect-with-aes128.md#encode_asset).</span></span>
3. <span data-ttu-id="44852-133">[Bir içerik anahtarı oluşturup kodlanmış hello varlıkla ilişkilendirme](media-services-protect-with-aes128.md#create_contentkey).</span><span class="sxs-lookup"><span data-stu-id="44852-133">[Create a content key and associate it with hello encoded asset](media-services-protect-with-aes128.md#create_contentkey).</span></span> <span data-ttu-id="44852-134">Media Services'de hello içerik anahtarı hello varlığın şifreleme anahtarını içerir.</span><span class="sxs-lookup"><span data-stu-id="44852-134">In Media Services, hello content key contains hello asset’s encryption key.</span></span>
4. <span data-ttu-id="44852-135">[Merhaba içerik anahtarının yetkilendirme ilkesini yapılandırma](media-services-protect-with-aes128.md#configure_key_auth_policy).</span><span class="sxs-lookup"><span data-stu-id="44852-135">[Configure hello content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span> <span data-ttu-id="44852-136">Merhaba içerik anahtarı yetkilendirme ilkesinin tarafınızdan yapılandırılması ve hello içerik anahtar toobe teslim toohello istemcisi için sırayla hello istemci tarafından karşılanır.</span><span class="sxs-lookup"><span data-stu-id="44852-136">hello content key authorization policy must be configured by you and met by hello client in order for hello content key toobe delivered toohello client.</span></span>
5. <span data-ttu-id="44852-137">[Bir varlık için Hello teslim ilkesini yapılandırma](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span><span class="sxs-lookup"><span data-stu-id="44852-137">[Configure hello delivery policy for an asset](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span></span> <span data-ttu-id="44852-138">Merhaba teslim ilkesi yapılandırması içerir: anahtar edinme URL'si ve başlatma vektörü (IV) (AES 128 gerektiren aynı IV toobe sağlanan şifrelerken hello ve çözme) teslim Protokolü (örneğin, MPEG DASH, HLS, kesintisiz akış veya tümü), hello türü dinamik şifreleme (örneğin, zarf veya dinamik şifreleme).</span><span class="sxs-lookup"><span data-stu-id="44852-138">hello delivery policy configuration includes: key acquisition URL and Initialization Vector (IV) (AES 128 requires hello same IV toobe supplied when encrypting and decrypting), delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all), hello type of dynamic encryption (for example, envelope or no dynamic encryption).</span></span>

    <span data-ttu-id="44852-139">Merhaba üzerinde farklı ilke tooeach Protokolü uygulayabilir aynı varlık.</span><span class="sxs-lookup"><span data-stu-id="44852-139">You could apply different policy tooeach protocol on hello same asset.</span></span> <span data-ttu-id="44852-140">Örneğin, PlayReady şifreleme tooSmooth/DASH ve AES zarfı tooHLS uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44852-140">For example, you could apply PlayReady encryption tooSmooth/DASH and AES Envelope tooHLS.</span></span> <span data-ttu-id="44852-141">Bir teslim ilkesinde tanımlanmayan tüm protokollerin (örneğin, yalnızca hello protokol olarak HLS belirten tek bir ilke ekliyorsunuz) akışla aktarılması engellenir.</span><span class="sxs-lookup"><span data-stu-id="44852-141">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="44852-142">Merhaba özel durum toothis hiç tanımlanmış hiçbir varlık teslim ilkesini varsa ' dir.</span><span class="sxs-lookup"><span data-stu-id="44852-142">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="44852-143">Ardından, tüm protokoller hello Temizle izin verilir.</span><span class="sxs-lookup"><span data-stu-id="44852-143">Then, all protocols will be allowed in hello clear.</span></span>

6. <span data-ttu-id="44852-144">[Bir OnDemand Bulucu oluşturmanız](media-services-protect-with-aes128.md#create_locator) içinde bir akış URL'si tooget sipariş.</span><span class="sxs-lookup"><span data-stu-id="44852-144">[Create an OnDemand locator](media-services-protect-with-aes128.md#create_locator) in order tooget a streaming URL.</span></span>

<span data-ttu-id="44852-145">Merhaba konu aynı zamanda gösterir [bir istemci uygulaması hello anahtar teslim hizmetinden bir anahtar nasıl isteyebilir](media-services-protect-with-aes128.md#client_request).</span><span class="sxs-lookup"><span data-stu-id="44852-145">hello topic also shows [how a client application can request a key from hello key delivery service](media-services-protect-with-aes128.md#client_request).</span></span>

<span data-ttu-id="44852-146">Tam .NET bulacaksınız [örnek](media-services-protect-with-aes128.md#example) hello konu hello sonunda.</span><span class="sxs-lookup"><span data-stu-id="44852-146">You will find a complete .NET [example](media-services-protect-with-aes128.md#example) at hello end of hello topic.</span></span>

<span data-ttu-id="44852-147">Görüntü aşağıdaki hello yukarıda açıklanan hello akışı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="44852-147">hello following image demonstrates hello workflow described above.</span></span> <span data-ttu-id="44852-148">Burada hello belirteci kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="44852-148">Here hello token is used for authentication.</span></span>

![AES-128 ile koruma](./media/media-services-content-protection-overview/media-services-content-protection-with-aes.png)

<span data-ttu-id="44852-150">Bu konunun geri kalanında Hello ayrıntılı açıklamalar, kod örnekleri ve nasıl tooachieve hello yukarıda açıklanan görevleri göster bağlantılar tootopics sağlar.</span><span class="sxs-lookup"><span data-stu-id="44852-150">hello rest of this topic provides detailed explanations, code examples, and links tootopics that show you how tooachieve hello tasks described above.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="44852-151">Geçerli sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="44852-151">Current limitations</span></span>
<span data-ttu-id="44852-152">Varlığınızın teslim ilkesini ekler veya güncelleştirirseniz, mevcut bulucuyu (varsa) silip yeni bir bulucu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="44852-152">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>

## <span data-ttu-id="44852-153"><a id="create_asset"></a>Bir varlık oluşturun ve dosyaları hello varlığa yükleyin</span><span class="sxs-lookup"><span data-stu-id="44852-153"><a id="create_asset"></a>Create an asset and upload files into hello asset</span></span>
<span data-ttu-id="44852-154">Sipariş toomanage kodlamak ve videolarınızı, akış içeriğinizi önce Microsoft Azure Media Services'e yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="44852-154">In order toomanage, encode, and stream your videos, you must first upload your content into Microsoft Azure Media Services.</span></span> <span data-ttu-id="44852-155">Yüklenmesinin ardından içeriğiniz daha fazla işleme ve akış hello bulutta güvenli bir şekilde depolanır.</span><span class="sxs-lookup"><span data-stu-id="44852-155">Once uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span> 

<span data-ttu-id="44852-156">Ayrıntılı bilgi için bkz. [Media Services hesabına dosya yükleme](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="44852-156">For detailed information, see [Upload Files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <span data-ttu-id="44852-157"><a id="encode_asset"></a>Merhaba varlık içeren hello dosya toohello Uyarlamalı bit hızı MP4 kümesine kodlayın</span><span class="sxs-lookup"><span data-stu-id="44852-157"><a id="encode_asset"></a>Encode hello asset containing hello file toohello adaptive bitrate MP4 set</span></span>
<span data-ttu-id="44852-158">Dinamik şifreleme ile tek ihtiyacınız olan toocreate Çoklu bit hızlı MP4 dosyası ya da Çoklu bit hızlı kesintisiz akış kaynak dosyası içeren bir varlık.</span><span class="sxs-lookup"><span data-stu-id="44852-158">With dynamic encryption all you need is toocreate an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="44852-159">Merhaba hello bildiriminde belirtilen biçime bağlı olarak veya istek parçalara, hello isteğe bağlı Akış sunucusu, hello akış seçmiş olduğunuz hello protokolde almanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="44852-159">Then, based on hello specified format in hello manifest or fragment request, hello On-Demand Streaming server will ensure that you receive hello stream in hello protocol you have chosen.</span></span> <span data-ttu-id="44852-160">Sonuç olarak, yalnızca toostore gerekir ve tek bir depolama biçiminde ve Media Services hizmeti hello dosyaları ödeme hello istemciden gelen isteklere göre uygun yanıtı derler ve.</span><span class="sxs-lookup"><span data-stu-id="44852-160">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span> <span data-ttu-id="44852-161">Daha fazla bilgi için bkz: Merhaba [dinamik paketlemeye genel bakış](media-services-dynamic-packaging-overview.md) konu.</span><span class="sxs-lookup"><span data-stu-id="44852-161">For more information, see hello [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) topic.</span></span>

>[!NOTE]
><span data-ttu-id="44852-162">AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu.</span><span class="sxs-lookup"><span data-stu-id="44852-162">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="44852-163">İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu.</span><span class="sxs-lookup"><span data-stu-id="44852-163">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
>
><span data-ttu-id="44852-164">Ayrıca, toobe mümkün toouse dinamik paketleme ve dinamik şifreleme Varlığınızı içermelidir Uyarlamalı bit hızlı MP4s veya uyarlamalı bit hızlı kesintisiz akış dosyaları kümesidir.</span><span class="sxs-lookup"><span data-stu-id="44852-164">Also, toobe able toouse dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="44852-165">Yönergeler için tooencode, bkz: [nasıl tooencode medya Kodlayıcı standart kullanarak bir varlık](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="44852-165">For instructions on how tooencode, see [How tooencode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <span data-ttu-id="44852-166"><a id="create_contentkey"></a>Bir içerik anahtarı oluşturup kodlanmış hello varlıkla ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="44852-166"><a id="create_contentkey"></a>Create a content key and associate it with hello encoded asset</span></span>
<span data-ttu-id="44852-167">Media Services'de hello içerik anahtarı tooencrypt bir varlık istediğiniz başlangıç anahtarı içeren ile.</span><span class="sxs-lookup"><span data-stu-id="44852-167">In Media Services, hello content key contains hello key that you want tooencrypt an asset with.</span></span>

<span data-ttu-id="44852-168">Ayrıntılı bilgi için bkz. [İçerik anahtarı oluşturma](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="44852-168">For detailed information, see [Create content key](media-services-dotnet-create-contentkey.md).</span></span>

## <span data-ttu-id="44852-169"><a id="configure_key_auth_policy"></a>Merhaba içerik anahtarının yetkilendirme ilkesini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="44852-169"><a id="configure_key_auth_policy"></a>Configure hello content key’s authorization policy</span></span>
<span data-ttu-id="44852-170">Media Services, anahtar isteğinde bulunan kullanıcıların kimlik doğrulamasını yapmanın birden çok yöntemini destekler.</span><span class="sxs-lookup"><span data-stu-id="44852-170">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="44852-171">Merhaba içerik anahtarı yetkilendirme ilkesinin tarafınızdan yapılandırılması ve hello anahtar toobe toohello istemci teslim sırayla hello istemci (oynatıcı) tarafından karşılanır.</span><span class="sxs-lookup"><span data-stu-id="44852-171">hello content key authorization policy must be configured by you and met by hello client (player) in order for hello key toobe delivered toohello client.</span></span> <span data-ttu-id="44852-172">Merhaba içerik anahtarı yetkilendirme ilkesini bir veya daha fazla yetkilendirme kısıtlamaları olabilir: açın, simge restriction ya da IP kısıtlaması.</span><span class="sxs-lookup"><span data-stu-id="44852-172">hello content key authorization policy could have one or more authorization restrictions: open, token restriction, or IP restriction.</span></span>

<span data-ttu-id="44852-173">Ayrıntılı bilgi için bkz. [İçerik Anahtarı Yetkilendirme İlkesini Yapılandırma](media-services-dotnet-configure-content-key-auth-policy.md).</span><span class="sxs-lookup"><span data-stu-id="44852-173">For detailed information, see [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md).</span></span>

## <span data-ttu-id="44852-174"><a id="configure_asset_delivery_policy"></a>Varlık teslim ilkesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="44852-174"><a id="configure_asset_delivery_policy"></a>Configure asset delivery policy</span></span>
<span data-ttu-id="44852-175">Varlığınıza Hello teslim ilkesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="44852-175">Configure hello delivery policy for your asset.</span></span> <span data-ttu-id="44852-176">Varlık teslim ilkesi yapılandırması hello bazı şeyleri içerir:</span><span class="sxs-lookup"><span data-stu-id="44852-176">Some things that hello asset delivery policy configuration includes:</span></span>

* <span data-ttu-id="44852-177">başlangıç anahtarı edinme URL'si.</span><span class="sxs-lookup"><span data-stu-id="44852-177">hello Key acquisition URL.</span></span> 
* <span data-ttu-id="44852-178">Merhaba başlatma vektörü (IV) toouse hello Zarf şifreleme için.</span><span class="sxs-lookup"><span data-stu-id="44852-178">hello Initialization Vector (IV) toouse for hello envelope encryption.</span></span> <span data-ttu-id="44852-179">AES 128, şifreleme ve şifre çözme aynı IV toobe sağlanan hello gerektirir.</span><span class="sxs-lookup"><span data-stu-id="44852-179">AES 128 requires hello same IV toobe supplied when encrypting and decrypting.</span></span> 
* <span data-ttu-id="44852-180">Merhaba varlık teslim Protokolü (örneğin, MPEG DASH, HLS, kesintisiz akış veya tümü).</span><span class="sxs-lookup"><span data-stu-id="44852-180">hello asset delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all).</span></span>
* <span data-ttu-id="44852-181">dinamik şifreleme (örneğin, AES zarfı) Hello türü veya dinamik şifreleme yok.</span><span class="sxs-lookup"><span data-stu-id="44852-181">hello type of dynamic encryption (for example, AES envelope) or no dynamic encryption.</span></span> 

<span data-ttu-id="44852-182">Ayrıntılı bilgi için bkz. [Varlık teslim ilkesini yapılandırma](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="44852-182">For detailed information, see [Configure asset delivery policy ](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <span data-ttu-id="44852-183"><a id="create_locator"></a>Bir OnDemand Bulucu sipariş tooget bir akış URL'si içinde akış oluşturma</span><span class="sxs-lookup"><span data-stu-id="44852-183"><a id="create_locator"></a>Create an OnDemand streaming locator in order tooget a streaming URL</span></span>
<span data-ttu-id="44852-184">Kullanıcı URL'si kesintisiz, DASH veya HLS akış hello ile tooprovide gerekir.</span><span class="sxs-lookup"><span data-stu-id="44852-184">You will need tooprovide your user with hello streaming URL for Smooth, DASH or HLS.</span></span>

> [!NOTE]
> <span data-ttu-id="44852-185">Varlığınızın teslim ilkesini ekler veya güncelleştirirseniz, mevcut bulucuyu (varsa) silip yeni bir bulucu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="44852-185">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
> 
> 

<span data-ttu-id="44852-186">Yönergeler için nasıl toopublish bir varlık ve yapı bir akış URL'si bkz [akış URL'si oluşturma](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="44852-186">For instructions on how toopublish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="44852-187">Test belirteci alma</span><span class="sxs-lookup"><span data-stu-id="44852-187">Get a test token</span></span>
<span data-ttu-id="44852-188">Merhaba hello anahtar yetkilendirme ilkesi için kullanılan belirteç kısıtlamasına dayalı bir test belirteci alın.</span><span class="sxs-lookup"><span data-stu-id="44852-188">Get a test token based on hello token restriction that was used for hello key authorization policy.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate = 
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);

<span data-ttu-id="44852-189">Merhaba kullanabilirsiniz [AMS Oynatıcısı](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest akışınızı.</span><span class="sxs-lookup"><span data-stu-id="44852-189">You can use hello [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest your stream.</span></span>

## <span data-ttu-id="44852-190"><a id="client_request"></a>Nasıl istemciniz bir anahtar hello anahtar teslim hizmetinden isteyebilir miyim?</span><span class="sxs-lookup"><span data-stu-id="44852-190"><a id="client_request"></a>How can your client request a key from hello key delivery service?</span></span>
<span data-ttu-id="44852-191">Merhaba önceki adımda tooa bildirim dosyası işaret eden hello URL oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="44852-191">In hello previous step, you constructed hello URL that points tooa manifest file.</span></span> <span data-ttu-id="44852-192">İstemci tooextract hello gerekli bilgileri sipariş toomake isteği toohello anahtar teslim hizmeti bildirim dosyalarından akış hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="44852-192">Your client needs tooextract hello necessary information from hello streaming manifest files in order toomake a request toohello key delivery service.</span></span>

### <a name="manifest-files"></a><span data-ttu-id="44852-193">Bildirim dosyası</span><span class="sxs-lookup"><span data-stu-id="44852-193">Manifest files</span></span>
<span data-ttu-id="44852-194">Merhaba istemci gerekir (aynı zamanda içerik anahtarı kimliği (çocuk) içeren) tooextract hello URL hello bildirim dosyası değeri.</span><span class="sxs-lookup"><span data-stu-id="44852-194">hello client needs tooextract hello URL (that also contains content key Id (kid)) value from hello manifest file.</span></span> <span data-ttu-id="44852-195">Merhaba istemci tooget hello şifreleme anahtarı hello anahtar teslim hizmetinden daha sonra deneyecek.</span><span class="sxs-lookup"><span data-stu-id="44852-195">hello client will then try tooget hello encryption key from hello key delivery service.</span></span> <span data-ttu-id="44852-196">Merhaba istemcisini de tooextract hello IV değeri gerekiyor ve aşağıdaki kod parçacığında hello stream.hello şifresini kullanım gösterir hello <Protection> hello kesintisiz akış bildiriminin öğesi.</span><span class="sxs-lookup"><span data-stu-id="44852-196">hello client also needs tooextract hello IV value and use it do decrypt hello stream.hello following snippet shows hello <Protection> element of hello Smooth Streaming manifest.</span></span>

    <Protection>
      <ProtectionHeader SystemID="B47B251A-2409-4B42-958E-08DBAE7B4EE9">
        <ContentProtection xmlns:sea="urn:mpeg:dash:schema:sea:2012" schemeIdUri="urn:mpeg:dash:sea:2012">
          <sea:SegmentEncryption schemeIdUri="urn:mpeg:dash:sea:aes128-cbc:2013"/>
          <sea:KeySystem keySystemUri="urn:mpeg:dash:sea:keysys:http:2013"/>
          <sea:CryptoPeriod IV="0xD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7" 
                            keyUriTemplate="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
                                            kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d"/>
        </ContentProtection>
      </ProtectionHeader>
    </Protection>

<span data-ttu-id="44852-197">HLS Hello durumda hello kök bildirimi segment dosyalarıyla ayrılır.</span><span class="sxs-lookup"><span data-stu-id="44852-197">In hello case of HLS, hello root manifest is broken into segment files.</span></span> 

<span data-ttu-id="44852-198">Örneğin, hello kök bildirimidir: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) ve segment dosya adlarının bir listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="44852-198">For example, hello root manifest is: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) and it contains a list of segment file names.</span></span>

    . . . 
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=630133,RESOLUTION=424x240,CODECS="avc1.4d4015,mp4a.40.2",AUDIO="audio"
    QualityLevels(514369)/Manifest(video,format=m3u8-aapl)
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=965441,RESOLUTION=636x356,CODECS="avc1.4d401e,mp4a.40.2",AUDIO="audio"
    QualityLevels(842459)/Manifest(video,format=m3u8-aapl)
    …

<span data-ttu-id="44852-199">Merhaba segment dosyalardan birini (örneğin, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should metin düzenleyicide açın #EXT-X-hello dosyayı şifreli gösteren anahtar içerir.</span><span class="sxs-lookup"><span data-stu-id="44852-199">If you open one of hello segment files in text editor (for example, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should contain #EXT-X-KEY which indicates that hello file is encrypted.</span></span>

    #EXTM3U
    #EXT-X-VERSION:4
    #EXT-X-ALLOW-CACHE:NO
    #EXT-X-MEDIA-SEQUENCE:0
    #EXT-X-TARGETDURATION:9
    #EXT-X-KEY:METHOD=AES-128,
    URI="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
         kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d",
            IV=0XD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7
    #EXT-X-PROGRAM-DATE-TIME:1970-01-01T00:00:00.000+00:00
    #EXTINF:8.425708,no-desc
    Fragments(video=0,format=m3u8-aapl)
    #EXT-X-ENDLIST

>[!NOTE] 
><span data-ttu-id="44852-200">Tooplay planlıyorsanız bir AES HLS Safari'de şifrelenmiş bkz [bu blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="44852-200">If you are planning tooplay an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

### <a name="request-hello-key-from-hello-key-delivery-service"></a><span data-ttu-id="44852-201">Merhaba anahtar teslim hizmetinden Hello anahtarı iste</span><span class="sxs-lookup"><span data-stu-id="44852-201">Request hello key from hello key delivery service</span></span>

<span data-ttu-id="44852-202">Merhaba aşağıdaki kod nasıl toosend isteği toohello Media Services anahtar teslim hizmeti anahtar teslim (Merhaba bildirimden ayıklandı) URI kullanılarak gösterir ve bir belirteç (Bu konuda değil konuşun nasıl tooget basit Web güvenli bir belirteci Hizmeti'nden belirteçleri hakkında).</span><span class="sxs-lookup"><span data-stu-id="44852-202">hello following code shows how toosend a request toohello Media Services key delivery service using a key delivery Uri (that was extracted from hello manifest) and a token (this topic does not talk about how tooget Simple Web Tokens from a Secure Token Service).</span></span>

    private byte[] GetDeliveryKey(Uri keyDeliveryUri, string token)
    {
        HttpWebRequest request = (HttpWebRequest)WebRequest.Create(keyDeliveryUri);

        request.Method = "POST";
        request.ContentType = "text/xml";
        if (!string.IsNullOrEmpty(token))
        {
            request.Headers[AuthorizationHeader] = token;
        }
        request.ContentLength = 0;

        var response = request.GetResponse();

        var stream = response.GetResponseStream();
        if (stream == null)
        {
            throw new NullReferenceException("Response stream is null");
        }

        var buffer = new byte[256];
        var length = 0;
        while (stream.CanRead && length <= buffer.Length)
        {
            var nexByte = stream.ReadByte();
            if (nexByte == -1)
            {
                break;
            }
            buffer[length] = (byte)nexByte;
            length++;
        }
        response.Close();

        // AES keys must be exactly 16 bytes (128 bits).
        var key = new byte[length];
        Array.Copy(buffer, key, length);
        return key;
    }

## <a name="protect-your-content-with-aes-128-using-net"></a><span data-ttu-id="44852-203">İçeriğinizi AES-128 ile korumak .NET kullanma</span><span class="sxs-lookup"><span data-stu-id="44852-203">Protect your content with AES-128 using .NET</span></span>

### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="44852-204">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="44852-204">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="44852-205">Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="44852-205">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="44852-206">Öğeleri çok aşağıdaki hello eklemek**appSettings** app.config dosyasında tanımlanan:</span><span class="sxs-lookup"><span data-stu-id="44852-206">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

### <span data-ttu-id="44852-207"><a id="example"></a>Örnek</span><span class="sxs-lookup"><span data-stu-id="44852-207"><a id="example"></a>Example</span></span>

<span data-ttu-id="44852-208">Bu bölümde gösterilen hello koduyla Hello kodu Program.cs dosyanızdaki üzerine.</span><span class="sxs-lookup"><span data-stu-id="44852-208">Overwrite hello code in your Program.cs file with hello code shown in this section.</span></span>
 
>[!NOTE]
><span data-ttu-id="44852-209">Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için).</span><span class="sxs-lookup"><span data-stu-id="44852-209">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="44852-210">Merhaba kullanması gereken her zaman kullanıyorsanız, aynı ilke kimliği hello aynı gün / erişim izinlerini, örneğin, uzun bir süre (karşıya yükleme olmayan ilkeleri) yerinde hedeflenen tooremain olan bulucular ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="44852-210">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="44852-211">Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="44852-211">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="44852-212">Emin tooupdate değişkenleri, giriş dosyalarınızın bulunduğu toopoint toofolders olun.</span><span class="sxs-lookup"><span data-stu-id="44852-212">Make sure tooupdate variables toopoint toofolders where your input files are located.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Security.Cryptography;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace AESDynamicEncryptionAndKeyDeliverySvc
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // A Uri describing hello issuer of hello token.  
        // Must match hello value in hello token for hello token toobe considered valid.
        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        // hello Audience or Scope of hello token.  
        // Must match hello value in hello token for hello token toobe considered valid.
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

            IContentKey key = CreateEnvelopeTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified 
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

            //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
            //so you have tooadd it in front of hello token string. 
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello bit.ly/aesplayer Flash player tootest hello URL 
            // (with open authorization policy). 
            // Paste hello URL and click hello Update button tooplay hello video. 
            //
            string URL = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Smooth Streaming Url: {0}/manifest", URL);
            Console.WriteLine();
            Console.WriteLine("HLS Url: {0}/manifest(format=m3u8-aapl)", URL);
            Console.WriteLine();

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
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.StorageEncrypted);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);


            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with hello encoding details, using a string preset.
            // In this case "Adaptive Streaming" preset is used.
            ITask task = job.Tasks.AddNew("My encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
            ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }

        static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
        {
            // Create envelope encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                keyId,
                contentKey,
                "ContentKey",
                ContentKeyType.EnvelopeEncryption);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }

        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {
            // Create ContentKeyAuthorizationPolicy with Open restrictions 
            // and create authorization policy             
            IContentKeyAuthorizationPolicy policy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Open Authorization Policy").Result;

            List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

            ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
            Name = "HLS Open Authorization Policy",
            KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
            Requirements = null // no requirements needed for HLS
        };

            restrictions.Add(restriction);

            IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "policy",
            ContentKeyDeliveryType.BaselineHttp,
            restrictions,
            "");

            policy.Options.Add(policyOption);

            // Add ContentKeyAutorizationPolicy tooContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            IContentKeyAuthorizationPolicy policy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("HLS token restricted authorization policy").Result;

            List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

            ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
                Name = "Token Authorization Policy",
                KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                Requirements = tokenTemplateString
            };

            restrictions.Add(restriction);

            //You could have multiple options 
            IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "Token option for HLS",
            ContentKeyDeliveryType.BaselineHttp,
            restrictions,
            null  // no key delivery data is needed for HLS
            );

            policy.Options.Add(policyOption);

            // Add ContentKeyAutorizationPolicy tooContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);

            return tokenTemplateString;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);

            string envelopeEncryptionIV = Convert.ToBase64String(GetRandomBuffer(16));

            // When configuring delivery policy, you can choose tooassociate it
            // with a key acquisition URL that has a KID appended or
            // or a key acquisition URL that does not have a KID appended  
            // in which case a content key can be reused. 

            // EnvelopeKeyAcquisitionUrl:  contains a key ID in hello key URL.
            // EnvelopeBaseKeyAcquisitionUrl:  hello URL does not contains a key ID

            // hello following policy configuration specifies: 
            // key url that will have KID=<Guid> appended toohello envelope and
            // hello Initialization Vector (IV) toouse for hello envelope encryption.

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeKeyAcquisitionUrl, keyAcquisitionUri.ToString()}
            };

            IAssetDeliveryPolicy assetDeliveryPolicy =
            _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
                AssetDeliveryPolicyType.DynamicEnvelopeEncryption,
                AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.Dash,
                assetDeliveryPolicyConfiguration);

            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
            assetDeliveryPolicy.AssetDeliveryPolicyType);
        }

        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset. 

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                EndsWith(".ism")).
                FirstOrDefault();

            // Create a 30-day readonly access policy. 
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
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

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int size)
        {
            byte[] randomBytes = new byte[size];
            using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
            {
            rng.GetBytes(randomBytes);
            }

            return randomBytes;
        }
        }
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="44852-213">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="44852-213">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="44852-214">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="44852-214">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

