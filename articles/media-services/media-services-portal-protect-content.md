---
title: "aaaConfiguring içerik koruma ilkeleri kullanılarak hello Azure portalı | Microsoft Docs"
description: "Bu makalede, nasıl toouse hello Azure portal tooconfigure içerik koruma ilkeleri gösterilmektedir. Merhaba makale ayrıca gösterir nasıl tooenable dinamik şifreleme varlıklarınızı için."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 270b3272-7411-40a9-ad42-5acdbba31154
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: 3e7ce6ddaa0e738b5a1e26dafe9eef2df221f039
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-content-protection-policies-using-hello-azure-portal"></a><span data-ttu-id="82b29-104">Hello Azure portal kullanarak içerik koruma ilkelerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="82b29-104">Configuring content protection policies using hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="82b29-105">toocomplete Bu öğretici bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="82b29-105">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="82b29-106">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="82b29-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="82b29-107">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="82b29-107">Overview</span></span>
<span data-ttu-id="82b29-108">Microsoft Azure Media Services (AMS), depolama, işleme ve teslim üzerinden bilgisayarınıza hello çıkışında medyanızdan, toosecure sağlar.</span><span class="sxs-lookup"><span data-stu-id="82b29-108">Microsoft Azure Media Services (AMS) enables you toosecure your media from hello time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="82b29-109">Media Services toodeliver verir içeriğinizi Gelişmiş Şifreleme Standardı ((128-bit şifreleme anahtarları kullanılarak) AES ile), PlayReady ve/veya Widevine DRM ve Apple FairPlay kullanarak ortak şifreleme (CENC) dinamik olarak şifrelenmiş.</span><span class="sxs-lookup"><span data-stu-id="82b29-109">Media Services allows you toodeliver your content encrypted dynamically with Advanced Encryption Standard (AES) (using 128-bit encryption keys), common encryption (CENC) using PlayReady and/or Widevine DRM, and Apple FairPlay.</span></span> 

<span data-ttu-id="82b29-110">AMS DRM lisansları teslim etmek için bir hizmet sunar ve AES anahtarları tooauthorized istemcileri temizleyin.</span><span class="sxs-lookup"><span data-stu-id="82b29-110">AMS provides a service for delivering DRM licenses and AES clear keys tooauthorized clients.</span></span> <span data-ttu-id="82b29-111">Hello Azure portal, toocreate bir sağlar **anahtarı/lisans yetkilendirme ilkesi** şifrelemeleri tüm türleri.</span><span class="sxs-lookup"><span data-stu-id="82b29-111">hello Azure portal enables you toocreate one **key/license authorization policy** for all types of encryptions.</span></span>

<span data-ttu-id="82b29-112">Bu makalede nasıl tooconfigure içerik koruma ilkeleri hello Azure portal ile gösterilir.</span><span class="sxs-lookup"><span data-stu-id="82b29-112">This article demonstrates how tooconfigure content protection policies with hello Azure portal.</span></span> <span data-ttu-id="82b29-113">Merhaba makale ayrıca gösterir nasıl tooapply dinamik şifreleme tooyour varlıklar.</span><span class="sxs-lookup"><span data-stu-id="82b29-113">hello article also shows how tooapply dynamic encryption tooyour assets.</span></span>


> [!NOTE]
> <span data-ttu-id="82b29-114">Hello Azure Klasik portalı toocreate koruma ilkeleri kullandıysanız, hello ilkeleri hello görünmeyebilir [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="82b29-114">If you used hello Azure classic portal toocreate protection policies, hello policies may not appear in hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="82b29-115">Ancak, eski tüm hello hala ilkeler yok.</span><span class="sxs-lookup"><span data-stu-id="82b29-115">However, all hello old polices still exist.</span></span> <span data-ttu-id="82b29-116">Bunları inceleyebilirsiniz kullanarak Azure Media Services .NET SDK veya hello hello [Azure-Media-Services-Gezgini](https://github.com/Azure/Azure-Media-Services-Explorer/releases) Aracı (toosee hello ilkeleri hello varlık üzerinde sağ -> görüntü bilgileri (F4) -> içerik anahtarları sekmesi ->'ı tıklatın Merhaba anahtarını tıklatın).</span><span class="sxs-lookup"><span data-stu-id="82b29-116">You can examine them using hello Azure Media Services .NET SDK or hello [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) tool (toosee hello policies, right-click on hello asset -> Display information (F4)->click on Content keys tab-> click on hello key).</span></span> 
> 
> <span data-ttu-id="82b29-117">Yeni ilkeleri kullanarak, varlık tooencrypt istiyorsanız hello Azure portal ile yapılandırmak, Kaydet'i tıklatın ve dinamik şifreleme yeniden uygulayın.</span><span class="sxs-lookup"><span data-stu-id="82b29-117">If you want tooencrypt your asset using new policies, configure them with hello Azure portal, click save, and reapply dynamic encryption.</span></span> 
> 
> 

## <a name="start-configuring-content-protection"></a><span data-ttu-id="82b29-118">İçerik koruma yapılandırma Başlat</span><span class="sxs-lookup"><span data-stu-id="82b29-118">Start configuring content protection</span></span>
<span data-ttu-id="82b29-119">İçerik koruma, genel tooyour AMS hesabının yapılandırma toouse hello portal toostart hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="82b29-119">toouse hello portal toostart configuring content protection, global tooyour AMS account, do hello following:</span></span>

1. <span data-ttu-id="82b29-120">Merhaba, [Azure portal](https://portal.azure.com/), Azure Media Services hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="82b29-120">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="82b29-121">Seçin **ayarları** > **içerik koruma**.</span><span class="sxs-lookup"><span data-stu-id="82b29-121">Select **Settings** > **Content protection**.</span></span>

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a><span data-ttu-id="82b29-123">Anahtar/lisans yetkilendirme ilkesi</span><span class="sxs-lookup"><span data-stu-id="82b29-123">Key/license authorization policy</span></span>
<span data-ttu-id="82b29-124">AMS anahtarını veya lisans isteğinde kullanıcıların kimliklerini doğrulama birden çok yöntemini destekler.</span><span class="sxs-lookup"><span data-stu-id="82b29-124">AMS supports multiple ways of authenticating users who make key or license requests.</span></span> <span data-ttu-id="82b29-125">Merhaba içerik anahtarı yetkilendirme ilkesinin tarafınızdan yapılandırılması ve sırayla hello anahtar/lisans toobe delived toohello istemcisi için istemci tarafından karşılanır.</span><span class="sxs-lookup"><span data-stu-id="82b29-125">hello content key authorization policy must be configured by you and met by your client in order for hello key/license toobe delived toohello client.</span></span> <span data-ttu-id="82b29-126">Merhaba içerik anahtarı yetkilendirme ilkesini bir veya daha fazla yetkilendirme kısıtlamaları olabilir: **açmak** veya **belirteci** kısıtlama.</span><span class="sxs-lookup"><span data-stu-id="82b29-126">hello content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span>

<span data-ttu-id="82b29-127">Hello Azure portal, toocreate bir sağlar **anahtarı/lisans yetkilendirme ilkesi** şifrelemeleri tüm türleri.</span><span class="sxs-lookup"><span data-stu-id="82b29-127">hello Azure portal enables you toocreate one **key/license authorization policy** for all types of encryptions.</span></span>

### <a name="open"></a><span data-ttu-id="82b29-128">Açık</span><span class="sxs-lookup"><span data-stu-id="82b29-128">Open</span></span>
<span data-ttu-id="82b29-129">Açık sınırlama hello sistem anahtar isteği yapan hello anahtar tooanyone göndereceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="82b29-129">Open restriction means that hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="82b29-130">Bu kısıtlama, test amaçları için yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="82b29-130">This restriction might be useful for test purposes.</span></span> 

### <a name="token"></a><span data-ttu-id="82b29-131">Belirteç</span><span class="sxs-lookup"><span data-stu-id="82b29-131">Token</span></span>
<span data-ttu-id="82b29-132">Merhaba belirteç kısıtlamalı ilkenin, bir güvenli belirteç hizmeti (STS) tarafından verilmiş bir belirteç tarafından eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="82b29-132">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="82b29-133">Media Services, hello basit Web belirteçleri (SWT) biçimi ve JSON Web Token (JWT) biçimlerindeki belirteçleri destekler.</span><span class="sxs-lookup"><span data-stu-id="82b29-133">Media Services supports tokens in hello Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span> <span data-ttu-id="82b29-134">Media Services, güvenli belirteç hizmetleri sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="82b29-134">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="82b29-135">Özel bir STS oluşturabilir veya Microsoft Azure ACS tooissue belirteçleri yararlanın.</span><span class="sxs-lookup"><span data-stu-id="82b29-135">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="82b29-136">Merhaba STS bir belirteci imzalayan belirtilen hello ile yapılandırılmış toocreate olmalıdır hello belirteç kısıtlamasına yapılandırmasında belirtilen anahtarı ve çıkış talep.</span><span class="sxs-lookup"><span data-stu-id="82b29-136">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration.</span></span> <span data-ttu-id="82b29-137">Bu yapılandırılmış hello belirteci için eşleşme hello anahtarı (veya lisans) Hello Media Services anahtar teslim hizmeti hello istenen hello belirteci geçerliyse, anahtarı (veya lisans) toohello istemci ve hello döndürülecek talepleri.</span><span class="sxs-lookup"><span data-stu-id="82b29-137">hello Media Services key delivery service will return hello requested key (or license) toohello client if hello token is valid and hello claims in hello token match those configured for hello key (or license).</span></span>

<span data-ttu-id="82b29-138">Merhaba belirteç kısıtlamalı ilkenin yapılandırırken hello birincil doğrulama anahtarı, veren ve İzleyici parametreleri belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="82b29-138">When configuring hello token restricted policy, you must specify hello primary verification key, issuer, and audience parameters.</span></span> <span data-ttu-id="82b29-139">Merhaba birincil doğrulama anahtarı içeren hello hello belirteci imzalayan, veren hello belirteci veren hello güvenli belirteç hizmeti olan anahtar.</span><span class="sxs-lookup"><span data-stu-id="82b29-139">hello primary verification key contains hello key that hello token was signed with, issuer is hello secure token service that issues hello token.</span></span> <span data-ttu-id="82b29-140">Merhaba kaynak hello belirteci erişimini yetkilendirir veya (bazen kapsam denir) hello İzleyici hello belirteci hello amacı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="82b29-140">hello audience (sometimes called scope) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="82b29-141">Merhaba Media Services anahtar teslim hizmeti bu değerleri hello belirteci hello değerleri hello şablonunda eşleştiğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="82b29-141">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span>

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a><span data-ttu-id="82b29-143">PlayReady haklar şablonu</span><span class="sxs-lookup"><span data-stu-id="82b29-143">PlayReady rights template</span></span>
<span data-ttu-id="82b29-144">Merhaba PlayReady haklar şablonu hakkında ayrıntılı bilgi için bkz: [Media Services PlayReady lisans şablonu genel bakış](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="82b29-144">For detailed information about hello PlayReady rights template, see [Media Services PlayReady License Template Overview](media-services-playready-license-template-overview.md).</span></span>

### <a name="non-persistent"></a><span data-ttu-id="82b29-145">Kalıcı olmayan</span><span class="sxs-lookup"><span data-stu-id="82b29-145">Non persistent</span></span>
<span data-ttu-id="82b29-146">Lisans kalıcı olarak yapılandırırsanız, hello player hello lisans kullanırken, yalnızca bellekte tutulur.</span><span class="sxs-lookup"><span data-stu-id="82b29-146">If you configure license as non-persistent, it is only held in memory while hello player is using hello license.</span></span>  

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a><span data-ttu-id="82b29-148">Kalıcı</span><span class="sxs-lookup"><span data-stu-id="82b29-148">Persistent</span></span>
<span data-ttu-id="82b29-149">Merhaba lisans kalıcı olarak yapılandırırsanız, hello istemcide kalıcı depolama alanına kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="82b29-149">If you configure hello license  as persistent, it is saved in persistent storage on hello client.</span></span>

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a><span data-ttu-id="82b29-151">Widevine haklar şablonu</span><span class="sxs-lookup"><span data-stu-id="82b29-151">Widevine rights template</span></span>
<span data-ttu-id="82b29-152">Merhaba Widevine haklar şablonu hakkında ayrıntılı bilgi için bkz: [Widevine lisans şablonu genel bakış](media-services-widevine-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="82b29-152">For detailed information about hello Widevine rights template, see [Widevine License Template Overview](media-services-widevine-license-template-overview.md).</span></span>

### <a name="basic"></a><span data-ttu-id="82b29-153">Temel</span><span class="sxs-lookup"><span data-stu-id="82b29-153">Basic</span></span>
<span data-ttu-id="82b29-154">Seçtiğinizde, **temel**, hello şablonu tüm varsayılanları değerlerle oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="82b29-154">When you select **Basic**, hello template will be created with all defaults values.</span></span>

### <a name="advanced"></a><span data-ttu-id="82b29-155">Gelişmiş</span><span class="sxs-lookup"><span data-stu-id="82b29-155">Advanced</span></span>
<span data-ttu-id="82b29-156">Widevine yapılandırmalarının öncelikli seçeneği hakkında ayrıntılı açıklamalar için bkz: [bu](media-services-widevine-license-template-overview.md) konu.</span><span class="sxs-lookup"><span data-stu-id="82b29-156">For detailed explanation about advance option of Widevine configurations, see [this](media-services-widevine-license-template-overview.md) topic.</span></span>

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a><span data-ttu-id="82b29-158">FairPlay yapılandırma</span><span class="sxs-lookup"><span data-stu-id="82b29-158">FairPlay configuration</span></span>
<span data-ttu-id="82b29-159">tooenable FairPlay şifreleme hello FairPlay yapılandırma seçeneği tooprovide hello uygulaması sertifikası ve uygulama gizli anahtarı (İSTEYİN) gerekir.</span><span class="sxs-lookup"><span data-stu-id="82b29-159">tooenable FairPlay encryption, you need tooprovide hello App Certificate and Application Secret Key (ASK) through hello FairPlay Configuration option.</span></span> <span data-ttu-id="82b29-160">FairPlay yapılandırması ve gereksinimleri hakkında ayrıntılı bilgi için bkz: [bu](media-services-protect-hls-with-fairplay.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="82b29-160">For detailed information about FairPlay configuration and requirements, see [this](media-services-protect-hls-with-fairplay.md) article.</span></span>

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-tooyour-asset"></a><span data-ttu-id="82b29-162">Dinamik şifreleme tooyour varlık Uygula</span><span class="sxs-lookup"><span data-stu-id="82b29-162">Apply dynamic encryption tooyour asset</span></span>
<span data-ttu-id="82b29-163">tootake avantajı dinamik şifrelenmesi tooencode kaynak dosyanızı bit hızı Uyarlamalı MP4 dosyaları kümesine ihtiyacınız.</span><span class="sxs-lookup"><span data-stu-id="82b29-163">tootake advantage of dynamic encryption, you need tooencode your source file into a set of adaptive-bitrate MP4 files.</span></span>

### <a name="select-an-asset-that-you-want-tooencrypt"></a><span data-ttu-id="82b29-164">Tooencrypt istediğiniz varlığı seçin</span><span class="sxs-lookup"><span data-stu-id="82b29-164">Select an asset that you want tooencrypt</span></span>
<span data-ttu-id="82b29-165">toosee, varlıklar seçin **ayarları** > **varlıklar**.</span><span class="sxs-lookup"><span data-stu-id="82b29-165">toosee all your assets, select **Settings** > **Assets**.</span></span>

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a><span data-ttu-id="82b29-167">AES veya DRM ile şifreleme</span><span class="sxs-lookup"><span data-stu-id="82b29-167">Encrypt with AES or DRM</span></span>
<span data-ttu-id="82b29-168">Tuşuna sonra **şifrele** bir varlık üzerinde iki seçenek sunulur: **AES** veya **DRM**.</span><span class="sxs-lookup"><span data-stu-id="82b29-168">Once you press **Encrypt** on an asset, you are presented wtih two choices: **AES** or **DRM**.</span></span> 

#### <a name="aes"></a><span data-ttu-id="82b29-169">AES</span><span class="sxs-lookup"><span data-stu-id="82b29-169">AES</span></span>
<span data-ttu-id="82b29-170">AES anahtar şifrelemesi tüm akış protokollerine etkinleştirilecek Temizle: kesintisiz akış, HLS ve MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="82b29-170">AES clear key encryption will be enabled on all streaming protocols: Smooth Streaming, HLS, and MPEG-DASH.</span></span>

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a><span data-ttu-id="82b29-172">DRM</span><span class="sxs-lookup"><span data-stu-id="82b29-172">DRM</span></span>
<span data-ttu-id="82b29-173">Merhaba DRM sekmesini seçin, içerik koruma ilkelerinin farklı seçenek sunulur (hangi artık yapılandırmış olmanız gerekir) + akış protokolleri kümesi.</span><span class="sxs-lookup"><span data-stu-id="82b29-173">When you select hello DRM tab, you are presented with different choices of content protection policies (which you must have configured by now) + a set of streaming protocols.</span></span>

* <span data-ttu-id="82b29-174">**PlayReady ve Widevine MPEG-DASH ile** -PlayReady ve Widevine DRMs MPEG-DASH akışınızı dinamik olarak şifreler.</span><span class="sxs-lookup"><span data-stu-id="82b29-174">**PlayReady and Widevine with MPEG-DASH** - will dynamically encrypt your MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span>
* <span data-ttu-id="82b29-175">**PlayReady ve Widevine MPEG-DASH ile + HLS ile FairPlay** -PlayReady ve Widevine DRMs olan MPEG-DASH akış dinamik olarak şifreler.</span><span class="sxs-lookup"><span data-stu-id="82b29-175">**PlayReady and Widevine with MPEG-DASH + FairPlay with HLS** - will dynamically encrypt you MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="82b29-176">Ayrıca, HLS akış FairPlay ile şifreler.</span><span class="sxs-lookup"><span data-stu-id="82b29-176">Will also encrypt your HLS streams with FairPlay.</span></span>
* <span data-ttu-id="82b29-177">**PlayReady yalnızca kesintisiz akış, HLS ve MPEG-DASH ile** -kesintisiz akış, HLS, MPEG-DASH akışları PlayReady DRM ile dinamik olarak şifreler.</span><span class="sxs-lookup"><span data-stu-id="82b29-177">**PlayReady only with Smooth Streaming, HLS and MPEG-DASH** - will dynamically encrypt Smooth Streaming, HLS, MPEG-DASH streams with PlayReady DRM.</span></span>
* <span data-ttu-id="82b29-178">**Yalnızca MPEG-DASH ile Widevine** -, MPEG-DASH Widevine DRM ile dinamik olarak şifreler.</span><span class="sxs-lookup"><span data-stu-id="82b29-178">**Widevine only with MPEG-DASH** - will dynamically encrypt you MPEG-DASH with Widevine DRM.</span></span>
* <span data-ttu-id="82b29-179">**FairPlay yalnızca HLS ile** -FairPlay olan, HLS akış dinamik olarak şifreler.</span><span class="sxs-lookup"><span data-stu-id="82b29-179">**FairPlay only with HLS** - will dynamically encrypt your HLS stream with FairPlay.</span></span>

<span data-ttu-id="82b29-180">tooenable FairPlay şifreleme hello içerik koruma ayarlar dikey FairPlay yapılandırma seçeneğini hello tooprovide hello uygulaması sertifikası ve uygulama gizli anahtarı (İSTEYİN) gerekir.</span><span class="sxs-lookup"><span data-stu-id="82b29-180">tooenable FairPlay encryption, you need tooprovide hello App Certificate and Application Secret Key (ASK) through hello FairPlay Configuration option of hello Content Protection settings blade.</span></span>

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection009.png)

<span data-ttu-id="82b29-182">Merhaba şifreleme seçimi yaptıktan sonra basın **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="82b29-182">Once you make hello encryption selection, press **Apply**.</span></span>

>[!NOTE] 
><span data-ttu-id="82b29-183">Tooplay planlıyorsanız bir AES HLS Safari'de şifrelenmiş bkz [bu blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="82b29-183">If you are planning tooplay an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="82b29-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="82b29-184">Next steps</span></span>
<span data-ttu-id="82b29-185">Media Services öğrenme yollarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="82b29-185">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="82b29-186">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="82b29-186">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

