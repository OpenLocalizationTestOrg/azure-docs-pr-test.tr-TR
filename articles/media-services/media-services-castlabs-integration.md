---
title: "aaaUsing castLabs toodeliver Widevine lisansları tooAzure Media Services | Microsoft Docs"
description: "Bu makalede, Azure Media Services (AMS) toodeliver, PlayReady ve Widevine DRMs AMS tarafından dinamik olarak şifrelenmiş bir akış nasıl kullanabileceğinizi açıklar. Medya Hizmetleri PlayReady lisans sunucusundan Hello PlayReady lisans gelir ve castLabs lisans sunucusu tarafından Widevine lisans teslim edilir."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 2a9a408a-a995-49e1-8d8f-ac5b51e17d40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: Mingfeiy;willzhan;Juliako
ms.openlocfilehash: 80d2778fb283a96361e7e511990a36c2f551a310
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-castlabs-toodeliver-widevine-licenses-tooazure-media-services"></a><span data-ttu-id="6c726-104">CastLabs toodeliver Widevine lisansları tooAzure Media Services'i kullanma</span><span class="sxs-lookup"><span data-stu-id="6c726-104">Using castLabs toodeliver Widevine licenses tooAzure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6c726-105">Axinom</span><span class="sxs-lookup"><span data-stu-id="6c726-105">Axinom</span></span>](media-services-axinom-integration.md)
> * [<span data-ttu-id="6c726-106">castLabs</span><span class="sxs-lookup"><span data-stu-id="6c726-106">castLabs</span></span>](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="6c726-107">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="6c726-107">Overview</span></span>
<span data-ttu-id="6c726-108">Bu makalede, Azure Media Services (AMS) toodeliver, PlayReady ve Widevine DRMs AMS tarafından dinamik olarak şifrelenmiş bir akış nasıl kullanabileceğinizi açıklar.</span><span class="sxs-lookup"><span data-stu-id="6c726-108">This article describes how you can use Azure Media Services (AMS) toodeliver a stream that is dynamically encrypted by AMS with both PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="6c726-109">Merhaba PlayReady lisans Media Services PlayReady lisans sunucusundan gelen ve Widevine lisans teslim tarafından **castLabs** lisans sunucusu.</span><span class="sxs-lookup"><span data-stu-id="6c726-109">hello PlayReady license comes from Media Services PlayReady license server and Widevine license is delivered by **castLabs** license server.</span></span>

<span data-ttu-id="6c726-110">korunan içeriği akış tooplayback (PlayReady ve/veya Widevine) CENC tarafından kullandığınız [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="6c726-110">tooplayback streaming content protected by CENC (PlayReady and/or Widevine), you can use  [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="6c726-111">Bkz: [AMP belge](http://amp.azure.net/libs/amp/latest/docs/) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="6c726-111">See [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details.</span></span>

<span data-ttu-id="6c726-112">bir üst düzey Azure Media Services ve castLabs tümleştirme mimarisi diyagramı aşağıdaki hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="6c726-112">hello following diagram demonstrates a high-level Azure Media Services and castLabs integration architecture.</span></span>

![Tümleştirme](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a><span data-ttu-id="6c726-114">Tipik sistem ayarlama</span><span class="sxs-lookup"><span data-stu-id="6c726-114">Typical system set up</span></span>
* <span data-ttu-id="6c726-115">Medya içeriği AMS içinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="6c726-115">Media content is stored in AMS.</span></span>
* <span data-ttu-id="6c726-116">İçerik anahtarı anahtar kimliklerini castLabs ve AMS içinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="6c726-116">Key IDs of content keys are stored in both castLabs and AMS.</span></span>
* <span data-ttu-id="6c726-117">castLabs ve AMS belirteci kimlik doğrulaması yerleşik olarak sahiptir.</span><span class="sxs-lookup"><span data-stu-id="6c726-117">castLabs and AMS both have token authentication built in.</span></span> <span data-ttu-id="6c726-118">Aşağıdaki bölümlerde hello kimlik doğrulama belirteçleri tartışın.</span><span class="sxs-lookup"><span data-stu-id="6c726-118">hello following sections discuss authentication tokens.</span></span> 
* <span data-ttu-id="6c726-119">Bir istemci toostream hello video istediğinde hello içerik ile dinamik olarak şifrelenir **ortak şifreleme** (CENC) ve akış ve tire AMS tooSmooth tarafından dinamik olarak paketlenir.</span><span class="sxs-lookup"><span data-stu-id="6c726-119">When a client requests toostream hello video, hello content is dynamically encrypted with **Common Encryption** (CENC) and dynamically packaged by AMS tooSmooth Streaming and DASH.</span></span> <span data-ttu-id="6c726-120">Biz, PlayReady M2TS başlangıç akışı şifreleme HLS Akış Protokolü için de sunar.</span><span class="sxs-lookup"><span data-stu-id="6c726-120">We also deliver PlayReady M2TS elementary stream encryption for HLS streaming protocol.</span></span>
* <span data-ttu-id="6c726-121">PlayReady lisans AMS lisans sunucusundan alınır ve Widevine lisans castLabs lisans sunucusundan alınır.</span><span class="sxs-lookup"><span data-stu-id="6c726-121">PlayReady license is retrieved from AMS license server and Widevine license is retrieved from castLabs license server.</span></span> 
* <span data-ttu-id="6c726-122">Media Player hello istemci platformu özelliği temelinde hangi lisans toofetch otomatik olarak karar verir.</span><span class="sxs-lookup"><span data-stu-id="6c726-122">Media Player automatically decides which license toofetch based on hello client platform capability.</span></span> 

## <a name="authentication-token-generation-for-getting-a-license"></a><span data-ttu-id="6c726-123">Bir lisans almak için kimlik doğrulama belirteci oluşturma</span><span class="sxs-lookup"><span data-stu-id="6c726-123">Authentication token generation for getting a license</span></span>
<span data-ttu-id="6c726-124">Hem castLabs hem de AMS (JSON Web belirteci) JWT belirteci biçimi kullanılan tooauthorize lisans destekler.</span><span class="sxs-lookup"><span data-stu-id="6c726-124">Both castLabs and AMS support JWT (JSON Web Token) token format used tooauthorize a license.</span></span> 

### <a name="jwt-token-in-ams"></a><span data-ttu-id="6c726-125">AMS JWT belirteci</span><span class="sxs-lookup"><span data-stu-id="6c726-125">JWT token in AMS</span></span>
<span data-ttu-id="6c726-126">Aşağıdaki tablonun hello AMS JWT belirteci açıklar.</span><span class="sxs-lookup"><span data-stu-id="6c726-126">hello following table describes JWT token in AMS.</span></span> 

| <span data-ttu-id="6c726-127">Veren</span><span class="sxs-lookup"><span data-stu-id="6c726-127">Issuer</span></span> | <span data-ttu-id="6c726-128">Güvenli belirteç hizmeti (STS) hello veren dizeden seçildi</span><span class="sxs-lookup"><span data-stu-id="6c726-128">Issuer string from hello chosen Secure Token Service (STS)</span></span> |
| --- | --- |
| <span data-ttu-id="6c726-129">Hedef kitle</span><span class="sxs-lookup"><span data-stu-id="6c726-129">Audience</span></span> |<span data-ttu-id="6c726-130">STS hello İzleyici dizeden kullanılan</span><span class="sxs-lookup"><span data-stu-id="6c726-130">Audience string from hello used STS</span></span> |
| <span data-ttu-id="6c726-131">Talepleri</span><span class="sxs-lookup"><span data-stu-id="6c726-131">Claims</span></span> |<span data-ttu-id="6c726-132">Talepler kümesi</span><span class="sxs-lookup"><span data-stu-id="6c726-132">A set of claims</span></span> |
| <span data-ttu-id="6c726-133">NotBefore</span><span class="sxs-lookup"><span data-stu-id="6c726-133">NotBefore</span></span> |<span data-ttu-id="6c726-134">Merhaba belirtecin geçerliliğini Başlat</span><span class="sxs-lookup"><span data-stu-id="6c726-134">Start validity of hello token</span></span> |
| <span data-ttu-id="6c726-135">Süre sonu</span><span class="sxs-lookup"><span data-stu-id="6c726-135">Expires</span></span> |<span data-ttu-id="6c726-136">Son hello belirtecin geçerliliğini</span><span class="sxs-lookup"><span data-stu-id="6c726-136">End validity of hello token</span></span> |
| <span data-ttu-id="6c726-137">SigningCredentials</span><span class="sxs-lookup"><span data-stu-id="6c726-137">SigningCredentials</span></span> |<span data-ttu-id="6c726-138">Lisans sunucusu ve STS, castLabs olan PlayReady lisans sunucusu arasında paylaşılan hello anahtar simetrik ya da asimetrik anahtar olabilir.</span><span class="sxs-lookup"><span data-stu-id="6c726-138">hello key that is shared among PlayReady License Server, castLabs License Server and STS, it could be either symmetric or asymmetric key.</span></span> |

### <a name="jwt-token-in-castlabs"></a><span data-ttu-id="6c726-139">CastLabs JWT belirteci</span><span class="sxs-lookup"><span data-stu-id="6c726-139">JWT token in castLabs</span></span>
<span data-ttu-id="6c726-140">Aşağıdaki tablonun hello castLabs JWT belirteci açıklar.</span><span class="sxs-lookup"><span data-stu-id="6c726-140">hello following table describes JWT token in castLabs.</span></span> 

| <span data-ttu-id="6c726-141">Ad</span><span class="sxs-lookup"><span data-stu-id="6c726-141">Name</span></span> | <span data-ttu-id="6c726-142">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6c726-142">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6c726-143">optData</span><span class="sxs-lookup"><span data-stu-id="6c726-143">optData</span></span> |<span data-ttu-id="6c726-144">Sizinle ilgili bilgileri içeren bir JSON dizesi.</span><span class="sxs-lookup"><span data-stu-id="6c726-144">A JSON string containing information about you.</span></span> |
| <span data-ttu-id="6c726-145">CRT</span><span class="sxs-lookup"><span data-stu-id="6c726-145">crt</span></span> |<span data-ttu-id="6c726-146">Bir hello varlık hakkında bilgi içeren JSON dizesi, lisans bilgileri ve kayıttan yürütme hakları.</span><span class="sxs-lookup"><span data-stu-id="6c726-146">A JSON string containing information about hello asset, its license info and playback rights.</span></span> |
| <span data-ttu-id="6c726-147">IAT</span><span class="sxs-lookup"><span data-stu-id="6c726-147">iat</span></span> |<span data-ttu-id="6c726-148">Geçerli datetime dönem Hello.</span><span class="sxs-lookup"><span data-stu-id="6c726-148">hello current datetime in epoch.</span></span> |
| <span data-ttu-id="6c726-149">jti</span><span class="sxs-lookup"><span data-stu-id="6c726-149">jti</span></span> |<span data-ttu-id="6c726-150">(Her belirteci yalnızca bir kez hello castLabs sisteminde kullanılabilir) bu belirteç hakkında benzersiz bir tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="6c726-150">A unique identifier about this token (every token can only be used once in hello castLabs system).</span></span> |

## <a name="sample-solution-set-up"></a><span data-ttu-id="6c726-151">Örnek çözümü ayarlayın</span><span class="sxs-lookup"><span data-stu-id="6c726-151">Sample solution set up</span></span>
<span data-ttu-id="6c726-152">Merhaba [örnek çözümü](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) iki projeden oluşan:</span><span class="sxs-lookup"><span data-stu-id="6c726-152">hello [sample solution](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) consists of two projects:</span></span>

* <span data-ttu-id="6c726-153">PlayReady ve Widevine DRM kısıtlamaları kullanılan tooset zaten alınan bir varlık üzerinde olabilir bir konsol uygulaması.</span><span class="sxs-lookup"><span data-stu-id="6c726-153">A console app that can be used tooset DRM restrictions on an already ingested asset, for both PlayReady and Widevine.</span></span>
* <span data-ttu-id="6c726-154">Bir çok Basitleştirilmiş sürümü bir STS olarak görülebilir belirteçleri dışarı aktarır bir Web uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="6c726-154">A Web Application that hands out tokens, which could be seen as a VERY SIMPLIFIED version of an STS.</span></span>

<span data-ttu-id="6c726-155">toouse hello konsol uygulaması:</span><span class="sxs-lookup"><span data-stu-id="6c726-155">toouse hello console application:</span></span>

1. <span data-ttu-id="6c726-156">Merhaba app.config toosetup AMS kimlik bilgileri, castLabs kimlik bilgileri, STS yapılandırma ve paylaşılan anahtar değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6c726-156">Change hello app.config toosetup AMS credentials, castLabs credentials, STS configuration and shared key.</span></span>
2. <span data-ttu-id="6c726-157">Bir varlık AMS yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6c726-157">Upload an Asset into AMS.</span></span>
3. <span data-ttu-id="6c726-158">Merhaba gelen Get hello UUID varlık karşıya ve hello Program.cs dosyasındaki satır 32 değiştirin:</span><span class="sxs-lookup"><span data-stu-id="6c726-158">Get hello UUID from hello uploaded Asset, and change Line 32 in hello Program.cs file:</span></span>
   
      <span data-ttu-id="6c726-159">var objIAsset _bağlamı =. Assets.Where (x = > x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf"). FirstOrDefault();</span><span class="sxs-lookup"><span data-stu-id="6c726-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span></span>
4. <span data-ttu-id="6c726-160">Bir AssetID hello castLabs sisteminde (Merhaba Program.cs dosyasındaki satır 44) hello varlık adlandırmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="6c726-160">Use an AssetId for naming hello asset in hello castLabs system (Line 44 in hello Program.cs file).</span></span>
   
   <span data-ttu-id="6c726-161">İçin AssetID ayarlamalısınız **castLabs**; toobe benzersiz bir alfasayısal dize gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="6c726-161">You must set AssetId for **castLabs**; it needs toobe a unique alphanumeric string.</span></span>
5. <span data-ttu-id="6c726-162">Merhaba programını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6c726-162">Run hello program.</span></span>

<span data-ttu-id="6c726-163">toouse hello Web uygulaması (STS):</span><span class="sxs-lookup"><span data-stu-id="6c726-163">toouse hello Web Application (STS):</span></span>

1. <span data-ttu-id="6c726-164">Değişiklik hello web.config toosetup castlabs satıcı kimliği, hello STS yapılandırma ve hello paylaşılan anahtar.</span><span class="sxs-lookup"><span data-stu-id="6c726-164">Change hello web.config toosetup castlabs merchant ID, hello STS configuration and hello shared key.</span></span>
2. <span data-ttu-id="6c726-165">Web siteleri tooAzure dağıtın.</span><span class="sxs-lookup"><span data-stu-id="6c726-165">Deploy tooAzure Websites.</span></span>
3. <span data-ttu-id="6c726-166">Toohello Web sitesine gidin.</span><span class="sxs-lookup"><span data-stu-id="6c726-166">Navigate toohello website.</span></span>

## <a name="playing-back-a-video"></a><span data-ttu-id="6c726-167">Bir video kayıttan yürütme</span><span class="sxs-lookup"><span data-stu-id="6c726-167">Playing back a video</span></span>
<span data-ttu-id="6c726-168">tooplayback video şifreli ortak şifreleme ile (PlayReady ve/veya Widevine), hello kullanabilirsiniz [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="6c726-168">tooplayback a video encrypted with common encryption (PlayReady and/or Widevine), you can use hello [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="6c726-169">Merhaba konsol uygulaması çalıştırırken hello içerik anahtarı kimliği ve hello bildirim URL echoed.</span><span class="sxs-lookup"><span data-stu-id="6c726-169">When running hello console app, hello Content Key ID and hello Manifest URL are echoed.</span></span>

1. <span data-ttu-id="6c726-170">Yeni bir sekme açın ve, STS başlatın: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span><span class="sxs-lookup"><span data-stu-id="6c726-170">Open a new tab and launch your STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span></span>
2. <span data-ttu-id="6c726-171">Çok Git[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="6c726-171">Go too[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
3. <span data-ttu-id="6c726-172">Akış URL'si hello yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="6c726-172">Paste in hello streaming URL.</span></span>
4. <span data-ttu-id="6c726-173">Merhaba tıklatın **Gelişmiş Seçenekler** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="6c726-173">Click hello **Advanced Options** checkbox.</span></span>
5. <span data-ttu-id="6c726-174">Merhaba, **koruma** açılan listesinde, select PlayReady ve/veya Widevine.</span><span class="sxs-lookup"><span data-stu-id="6c726-174">In hello **Protection** dropdown, select PlayReady and/or Widevine.</span></span>
6. <span data-ttu-id="6c726-175">Merhaba belirteci metin kutusuna, STS dan aldığınız hello belirteci yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="6c726-175">Paste hello token that you got from your STS in hello Token textbox.</span></span> 
   
   <span data-ttu-id="6c726-176">Merhaba castLab lisans sunucusu hello gerek yoktur "taşıyıcı =" hello belirteci önünde öneki.</span><span class="sxs-lookup"><span data-stu-id="6c726-176">hello castLab license server does not need hello “Bearer=” prefix in front of hello token.</span></span> <span data-ttu-id="6c726-177">Bu nedenle, hello belirteci göndermeden önce lütfen kaldırın.</span><span class="sxs-lookup"><span data-stu-id="6c726-177">So please remove that before submitting hello token.</span></span>
7. <span data-ttu-id="6c726-178">Merhaba player güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="6c726-178">Update hello player.</span></span>
8. <span data-ttu-id="6c726-179">Merhaba video oynatma.</span><span class="sxs-lookup"><span data-stu-id="6c726-179">hello video should be playing.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="6c726-180">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="6c726-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6c726-181">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="6c726-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

