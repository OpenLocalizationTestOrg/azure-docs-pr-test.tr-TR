---
title: "Azure portalını kullanarak içerik koruma ilkelerini yapılandırma | Microsoft Docs"
description: "Bu makalede Azure portal içerik koruma ilkelerini yapılandırmak için nasıl kullanılacağı gösterilmektedir. Makale ayrıca varlıklarınızı dinamik şifrelemeyi etkinleştirmek nasıl gösterir."
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
ms.openlocfilehash: 67b3fa9936daebeafb7e87fe3a7b0c7e0105b3b3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-content-protection-policies-using-the-azure-portal"></a><span data-ttu-id="8860f-104">Azure portalını kullanarak içerik koruma ilkelerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8860f-104">Configuring content protection policies using the Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="8860f-105">Bu öğreticiyi tamamlamak için bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8860f-105">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="8860f-106">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8860f-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="8860f-107">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="8860f-107">Overview</span></span>
<span data-ttu-id="8860f-108">Microsoft Azure Media Services (AMS), depolama, işleme ve teslim üzerinden bilgisayarınıza çıkışında medyanızdan güvenli olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="8860f-108">Microsoft Azure Media Services (AMS) enables you to secure your media from the time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="8860f-109">Media Services göndermenizi sağlayan içeriğinizi Gelişmiş Şifreleme Standardı ((128-bit şifreleme anahtarları kullanılarak) AES ile), PlayReady ve/veya Widevine DRM ve Apple FairPlay kullanarak ortak şifreleme (CENC) dinamik olarak şifrelenmiş.</span><span class="sxs-lookup"><span data-stu-id="8860f-109">Media Services allows you to deliver your content encrypted dynamically with Advanced Encryption Standard (AES) (using 128-bit encryption keys), common encryption (CENC) using PlayReady and/or Widevine DRM, and Apple FairPlay.</span></span> 

<span data-ttu-id="8860f-110">AMS DRM lisansları teslim etmek için bir hizmet sunar ve AES anahtarları yetkili istemcilere temizleyin.</span><span class="sxs-lookup"><span data-stu-id="8860f-110">AMS provides a service for delivering DRM licenses and AES clear keys to authorized clients.</span></span> <span data-ttu-id="8860f-111">Azure portalında bir oluşturmanızı sağlayan **anahtarı/lisans yetkilendirme ilkesi** şifrelemeleri tüm türleri.</span><span class="sxs-lookup"><span data-stu-id="8860f-111">The Azure portal enables you to create one **key/license authorization policy** for all types of encryptions.</span></span>

<span data-ttu-id="8860f-112">Bu makalede Azure portalıyla içerik koruma ilkeleri yapılandırma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8860f-112">This article demonstrates how to configure content protection policies with the Azure portal.</span></span> <span data-ttu-id="8860f-113">Makale ayrıca varlıklarınızı için dinamik şifreleme uygulamak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="8860f-113">The article also shows how to apply dynamic encryption to your assets.</span></span>


> [!NOTE]
> <span data-ttu-id="8860f-114">Koruma ilkeleri oluşturmak için Klasik Azure portalı kullandıysanız, ilkeleri görüntülenmeyebilir [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8860f-114">If you used the Azure classic portal to create protection policies, the policies may not appear in the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="8860f-115">Ancak, tüm eski ilkeleri hala mevcut.</span><span class="sxs-lookup"><span data-stu-id="8860f-115">However, all the old polices still exist.</span></span> <span data-ttu-id="8860f-116">Azure Media Services .NET SDK kullanarak bunları inceleyin veya [Azure-Media-Services-Gezgini](https://github.com/Azure/Azure-Media-Services-Explorer/releases) Aracı (varlık sağ tıklatın ilkeleri görmek için görüntüleme bilgileri (F4) -> -> içerik anahtarlar sekmesini tıklatın -> tıklatın Aç anahtar).</span><span class="sxs-lookup"><span data-stu-id="8860f-116">You can examine them using the Azure Media Services .NET SDK or the [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) tool (to see the policies, right-click on the asset -> Display information (F4)->click on Content keys tab-> click on the key).</span></span> 
> 
> <span data-ttu-id="8860f-117">Yeni ilkeleri kullanarak, varlık şifrelemek isterseniz, Azure portalıyla yapılandırmak, Kaydet'i tıklatın ve dinamik şifreleme yeniden uygulayın.</span><span class="sxs-lookup"><span data-stu-id="8860f-117">If you want to encrypt your asset using new policies, configure them with the Azure portal, click save, and reapply dynamic encryption.</span></span> 
> 
> 

## <a name="start-configuring-content-protection"></a><span data-ttu-id="8860f-118">İçerik koruma yapılandırma Başlat</span><span class="sxs-lookup"><span data-stu-id="8860f-118">Start configuring content protection</span></span>
<span data-ttu-id="8860f-119">İçerik koruma, AMS hesabınızı genel yapılandırmaya başlamak için portalı kullanmak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="8860f-119">To use the portal to start configuring content protection, global to your AMS account, do the following:</span></span>

1. <span data-ttu-id="8860f-120">[Azure portalında](https://portal.azure.com/) Azure Media Services hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="8860f-120">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="8860f-121">Seçin **ayarları** > **içerik koruma**.</span><span class="sxs-lookup"><span data-stu-id="8860f-121">Select **Settings** > **Content protection**.</span></span>

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a><span data-ttu-id="8860f-123">Anahtar/lisans yetkilendirme ilkesi</span><span class="sxs-lookup"><span data-stu-id="8860f-123">Key/license authorization policy</span></span>
<span data-ttu-id="8860f-124">AMS anahtarını veya lisans isteğinde kullanıcıların kimliklerini doğrulama birden çok yöntemini destekler.</span><span class="sxs-lookup"><span data-stu-id="8860f-124">AMS supports multiple ways of authenticating users who make key or license requests.</span></span> <span data-ttu-id="8860f-125">İçerik anahtarı yetkilendirme ilkesinin tarafınızdan yapılandırılması ve istemciye delived için istemci anahtarı/lisans sırayla tarafından karşılanır.</span><span class="sxs-lookup"><span data-stu-id="8860f-125">The content key authorization policy must be configured by you and met by your client in order for the key/license to be delived to the client.</span></span> <span data-ttu-id="8860f-126">İçerik anahtarı yetkilendirme ilkesini bir veya daha fazla yetkilendirme kısıtlamaları olabilir: **açmak** veya **belirteci** kısıtlama.</span><span class="sxs-lookup"><span data-stu-id="8860f-126">The content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span>

<span data-ttu-id="8860f-127">Azure portalında bir oluşturmanızı sağlayan **anahtarı/lisans yetkilendirme ilkesi** şifrelemeleri tüm türleri.</span><span class="sxs-lookup"><span data-stu-id="8860f-127">The Azure portal enables you to create one **key/license authorization policy** for all types of encryptions.</span></span>

### <a name="open"></a><span data-ttu-id="8860f-128">Açık</span><span class="sxs-lookup"><span data-stu-id="8860f-128">Open</span></span>
<span data-ttu-id="8860f-129">Açık sınırlama Sistem anahtarı anahtar istekte herkes için teslim eder, anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="8860f-129">Open restriction means that the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="8860f-130">Bu kısıtlama, test amaçları için yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="8860f-130">This restriction might be useful for test purposes.</span></span> 

### <a name="token"></a><span data-ttu-id="8860f-131">Belirteç</span><span class="sxs-lookup"><span data-stu-id="8860f-131">Token</span></span>
<span data-ttu-id="8860f-132">Belirteç kısıtlamalı ilkenin beraberinde bir Güvenli Belirteç Hizmeti (STS) tarafından verilmiş bir belirteç bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8860f-132">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="8860f-133">Media Services, basit Web belirteçleri (SWT) biçimini ve JSON Web Token (JWT) biçimlerindeki belirteçleri destekler.</span><span class="sxs-lookup"><span data-stu-id="8860f-133">Media Services supports tokens in the Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span> <span data-ttu-id="8860f-134">Media Services, güvenli belirteç hizmetleri sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="8860f-134">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="8860f-135">Özel bir STS oluşturabilir veya Microsoft Azure ACS sorunu belirteçleri yararlanın.</span><span class="sxs-lookup"><span data-stu-id="8860f-135">You can create a custom STS or leverage Microsoft Azure ACS to issue tokens.</span></span> <span data-ttu-id="8860f-136">STS, belirteç kısıtlamasına yapılandırmasında belirtilen belirtilen anahtarı ve sorunu talepleri imzalı bir belirteç oluşturmak için yapılandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8860f-136">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration.</span></span> <span data-ttu-id="8860f-137">Media Services anahtar teslim hizmeti istenen anahtarı (veya lisans) istemcinin belirtecin geçerli olup olmadığını ve bu belirteci yapılandırmış anahtarı (veya lisans) için talepleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="8860f-137">The Media Services key delivery service will return the requested key (or license) to the client if the token is valid and the claims in the token match those configured for the key (or license).</span></span>

<span data-ttu-id="8860f-138">Belirteç yapılandırma İlkesi sınırlı olduğunda, birincil doğrulama anahtarı, veren ve İzleyici parametreleri belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8860f-138">When configuring the token restricted policy, you must specify the primary verification key, issuer, and audience parameters.</span></span> <span data-ttu-id="8860f-139">Birincil doğrulama anahtar belirteci ile imzalandığı anahtarı içerir, veren belirtecini veren güvenli belirteç hizmeti.</span><span class="sxs-lookup"><span data-stu-id="8860f-139">The primary verification key contains the key that the token was signed with, issuer is the secure token service that issues the token.</span></span> <span data-ttu-id="8860f-140">Kaynak belirteci erişimini yetkilendirir veya (bazen kapsam denir) İzleyici belirteç amacı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="8860f-140">The audience (sometimes called scope) describes the intent of the token or the resource the token authorizes access to.</span></span> <span data-ttu-id="8860f-141">Media Services anahtar teslim hizmeti, bu değerleri belirteci şablon değerleri eşleştiğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="8860f-141">The Media Services key delivery service validates that these values in the token match the values in the template.</span></span>

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a><span data-ttu-id="8860f-143">PlayReady haklar şablonu</span><span class="sxs-lookup"><span data-stu-id="8860f-143">PlayReady rights template</span></span>
<span data-ttu-id="8860f-144">PlayReady haklar şablonu hakkında ayrıntılı bilgi için bkz: [Media Services PlayReady lisans şablonu genel bakış](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8860f-144">For detailed information about the PlayReady rights template, see [Media Services PlayReady License Template Overview](media-services-playready-license-template-overview.md).</span></span>

### <a name="non-persistent"></a><span data-ttu-id="8860f-145">Kalıcı olmayan</span><span class="sxs-lookup"><span data-stu-id="8860f-145">Non persistent</span></span>
<span data-ttu-id="8860f-146">Lisans kalıcı olarak yapılandırırsanız, player lisans kullanırken, yalnızca bellekte tutulur.</span><span class="sxs-lookup"><span data-stu-id="8860f-146">If you configure license as non-persistent, it is only held in memory while the player is using the license.</span></span>  

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a><span data-ttu-id="8860f-148">Kalıcı</span><span class="sxs-lookup"><span data-stu-id="8860f-148">Persistent</span></span>
<span data-ttu-id="8860f-149">Lisans kalıcı olarak yapılandırırsanız, istemci üzerinde kalıcı depolama alanına kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="8860f-149">If you configure the license  as persistent, it is saved in persistent storage on the client.</span></span>

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a><span data-ttu-id="8860f-151">Widevine haklar şablonu</span><span class="sxs-lookup"><span data-stu-id="8860f-151">Widevine rights template</span></span>
<span data-ttu-id="8860f-152">Widevine haklar şablonu hakkında ayrıntılı bilgi için bkz: [Widevine lisans şablonu genel bakış](media-services-widevine-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8860f-152">For detailed information about the Widevine rights template, see [Widevine License Template Overview](media-services-widevine-license-template-overview.md).</span></span>

### <a name="basic"></a><span data-ttu-id="8860f-153">Temel</span><span class="sxs-lookup"><span data-stu-id="8860f-153">Basic</span></span>
<span data-ttu-id="8860f-154">Seçtiğinizde, **temel**, şablonu tüm varsayılanları değerlerle oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8860f-154">When you select **Basic**, the template will be created with all defaults values.</span></span>

### <a name="advanced"></a><span data-ttu-id="8860f-155">Gelişmiş</span><span class="sxs-lookup"><span data-stu-id="8860f-155">Advanced</span></span>
<span data-ttu-id="8860f-156">Widevine yapılandırmalarının öncelikli seçeneği hakkında ayrıntılı açıklamalar için bkz: [bu](media-services-widevine-license-template-overview.md) konu.</span><span class="sxs-lookup"><span data-stu-id="8860f-156">For detailed explanation about advance option of Widevine configurations, see [this](media-services-widevine-license-template-overview.md) topic.</span></span>

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a><span data-ttu-id="8860f-158">FairPlay yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8860f-158">FairPlay configuration</span></span>
<span data-ttu-id="8860f-159">FairPlay şifrelemeyi etkinleştirmek için uygulama sertifika ve uygulama gizli anahtarı (İSTEYİN) FairPlay yapılandırma seçeneği sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8860f-159">To enable FairPlay encryption, you need to provide the App Certificate and Application Secret Key (ASK) through the FairPlay Configuration option.</span></span> <span data-ttu-id="8860f-160">FairPlay yapılandırması ve gereksinimleri hakkında ayrıntılı bilgi için bkz: [bu](media-services-protect-hls-with-fairplay.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="8860f-160">For detailed information about FairPlay configuration and requirements, see [this](media-services-protect-hls-with-fairplay.md) article.</span></span>

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-to-your-asset"></a><span data-ttu-id="8860f-162">Varlık için dinamik şifreleme Uygula</span><span class="sxs-lookup"><span data-stu-id="8860f-162">Apply dynamic encryption to your asset</span></span>
<span data-ttu-id="8860f-163">Dinamik şifreleme yararlanmak için kaynak dosyanızı bit hızı Uyarlamalı MP4 dosyaları kümesine kodlayın gerekir.</span><span class="sxs-lookup"><span data-stu-id="8860f-163">To take advantage of dynamic encryption, you need to encode your source file into a set of adaptive-bitrate MP4 files.</span></span>

### <a name="select-an-asset-that-you-want-to-encrypt"></a><span data-ttu-id="8860f-164">Şifrelemek istediğiniz bir varlığı seçin</span><span class="sxs-lookup"><span data-stu-id="8860f-164">Select an asset that you want to encrypt</span></span>
<span data-ttu-id="8860f-165">Tüm varlıklarınızı görmek için seçin **ayarları** > **varlıklar**.</span><span class="sxs-lookup"><span data-stu-id="8860f-165">To see all your assets, select **Settings** > **Assets**.</span></span>

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a><span data-ttu-id="8860f-167">AES veya DRM ile şifreleme</span><span class="sxs-lookup"><span data-stu-id="8860f-167">Encrypt with AES or DRM</span></span>
<span data-ttu-id="8860f-168">Tuşuna sonra **şifrele** bir varlık üzerinde iki seçenek sunulur: **AES** veya **DRM**.</span><span class="sxs-lookup"><span data-stu-id="8860f-168">Once you press **Encrypt** on an asset, you are presented wtih two choices: **AES** or **DRM**.</span></span> 

#### <a name="aes"></a><span data-ttu-id="8860f-169">AES</span><span class="sxs-lookup"><span data-stu-id="8860f-169">AES</span></span>
<span data-ttu-id="8860f-170">AES anahtar şifrelemesi tüm akış protokollerine etkinleştirilecek Temizle: kesintisiz akış, HLS ve MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="8860f-170">AES clear key encryption will be enabled on all streaming protocols: Smooth Streaming, HLS, and MPEG-DASH.</span></span>

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a><span data-ttu-id="8860f-172">DRM</span><span class="sxs-lookup"><span data-stu-id="8860f-172">DRM</span></span>
<span data-ttu-id="8860f-173">DRM sekmesini seçin, içerik koruma ilkelerinin farklı seçenek sunulur (hangi artık yapılandırmış olmanız gerekir) + akış protokolleri kümesi.</span><span class="sxs-lookup"><span data-stu-id="8860f-173">When you select the DRM tab, you are presented with different choices of content protection policies (which you must have configured by now) + a set of streaming protocols.</span></span>

* <span data-ttu-id="8860f-174">**PlayReady ve Widevine MPEG-DASH ile** -PlayReady ve Widevine DRMs MPEG-DASH akışınızı dinamik olarak şifreler.</span><span class="sxs-lookup"><span data-stu-id="8860f-174">**PlayReady and Widevine with MPEG-DASH** - will dynamically encrypt your MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span>
* <span data-ttu-id="8860f-175">**PlayReady ve Widevine MPEG-DASH ile + HLS ile FairPlay** -PlayReady ve Widevine DRMs olan MPEG-DASH akış dinamik olarak şifreler.</span><span class="sxs-lookup"><span data-stu-id="8860f-175">**PlayReady and Widevine with MPEG-DASH + FairPlay with HLS** - will dynamically encrypt you MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="8860f-176">Ayrıca, HLS akış FairPlay ile şifreler.</span><span class="sxs-lookup"><span data-stu-id="8860f-176">Will also encrypt your HLS streams with FairPlay.</span></span>
* <span data-ttu-id="8860f-177">**PlayReady yalnızca kesintisiz akış, HLS ve MPEG-DASH ile** -kesintisiz akış, HLS, MPEG-DASH akışları PlayReady DRM ile dinamik olarak şifreler.</span><span class="sxs-lookup"><span data-stu-id="8860f-177">**PlayReady only with Smooth Streaming, HLS and MPEG-DASH** - will dynamically encrypt Smooth Streaming, HLS, MPEG-DASH streams with PlayReady DRM.</span></span>
* <span data-ttu-id="8860f-178">**Yalnızca MPEG-DASH ile Widevine** -, MPEG-DASH Widevine DRM ile dinamik olarak şifreler.</span><span class="sxs-lookup"><span data-stu-id="8860f-178">**Widevine only with MPEG-DASH** - will dynamically encrypt you MPEG-DASH with Widevine DRM.</span></span>
* <span data-ttu-id="8860f-179">**FairPlay yalnızca HLS ile** -FairPlay olan, HLS akış dinamik olarak şifreler.</span><span class="sxs-lookup"><span data-stu-id="8860f-179">**FairPlay only with HLS** - will dynamically encrypt your HLS stream with FairPlay.</span></span>

<span data-ttu-id="8860f-180">FairPlay şifrelemesini etkinleştirmek için içerik koruma ayarlar dikey FairPlay yapılandırma seçeneği uygulama sertifika ve uygulama gizli anahtarı (İSTEYİN) sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8860f-180">To enable FairPlay encryption, you need to provide the App Certificate and Application Secret Key (ASK) through the FairPlay Configuration option of the Content Protection settings blade.</span></span>

![İçerik koruma](./media/media-services-portal-content-protection/media-services-content-protection009.png)

<span data-ttu-id="8860f-182">Şifreleme seçimi yaptıktan sonra basın **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="8860f-182">Once you make the encryption selection, press **Apply**.</span></span>

>[!NOTE] 
><span data-ttu-id="8860f-183">Yürüt planlıyorsanız, bir AES HLS Safari'de şifrelenmiş bkz [bu blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="8860f-183">If you are planning to play an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8860f-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8860f-184">Next steps</span></span>
<span data-ttu-id="8860f-185">Media Services öğrenme yollarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="8860f-185">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8860f-186">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="8860f-186">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

