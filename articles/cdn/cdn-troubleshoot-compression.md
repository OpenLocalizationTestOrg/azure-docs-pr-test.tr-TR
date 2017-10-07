---
title: "Azure CDN aaaTroubleshooting dosya sıkıştırmasını | Microsoft Docs"
description: "Azure CDN dosya sıkıştırma ile ilgili sorunları giderin."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: a6624e65-1a77-4486-b473-8d720ce28f8b
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f00b98beaf6b3b3cd30108ece65a8191edc06ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-file-compression"></a><span data-ttu-id="e1c5b-103">CDN dosya sıkıştırma sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="e1c5b-103">Troubleshooting CDN file compression</span></span>
<span data-ttu-id="e1c5b-104">Bu makale ile ilgili sorunları gidermenize yardımcı [CDN dosya sıkıştırma](cdn-improve-performance.md).</span><span class="sxs-lookup"><span data-stu-id="e1c5b-104">This article helps you troubleshoot issues with [CDN file compression](cdn-improve-performance.md).</span></span>

<span data-ttu-id="e1c5b-105">Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz üzerinde Azure uzmanlar hello [MSDN Azure hello ve yığın taşması forumları hello](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="e1c5b-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and hello Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="e1c5b-106">Alternatif olarak, Azure destek olay dosya.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-106">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="e1c5b-107">Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/support/options/) tıklatıp **destek alın**.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-107">Go toohello [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="e1c5b-108">Belirti</span><span class="sxs-lookup"><span data-stu-id="e1c5b-108">Symptom</span></span>
<span data-ttu-id="e1c5b-109">Uç noktanız için sıkıştırma etkin, ancak dosyalar sıkıştırılmamış döndürülen.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-109">Compression for your endpoint is enabled, but files are being returned uncompressed.</span></span>

> [!TIP]
> <span data-ttu-id="e1c5b-110">toocheck dosyalarınızı sıkıştırılmış döndürülen olsun, bir aracı gibi toouse gerek [Fiddler](http://www.telerik.com/fiddler) veya tarayıcınızın [Geliştirici Araçları](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span><span class="sxs-lookup"><span data-stu-id="e1c5b-110">toocheck whether your files are being returned compressed, you need toouse a tool like [Fiddler](http://www.telerik.com/fiddler) or your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span></span>  <span data-ttu-id="e1c5b-111">Onay hello HTTP yanıt üstbilgilerini, önbelleğe alınan CDN içerik döndürdü.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-111">Check hello HTTP response headers returned with your cached CDN content.</span></span>  <span data-ttu-id="e1c5b-112">Adlı bir üst bilgi olup olmadığını `Content-Encoding` değerini **gzip**, **bzıp2**, veya **deflate**, içeriğinizi sıkıştırılır.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-112">If there is a header named `Content-Encoding` with a value of **gzip**, **bzip2**, or **deflate**, your content is compressed.</span></span>
> 
> ![İçerik Kodlama üstbilgisi](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a><span data-ttu-id="e1c5b-114">Nedeni</span><span class="sxs-lookup"><span data-stu-id="e1c5b-114">Cause</span></span>
<span data-ttu-id="e1c5b-115">Dahil birkaç olası nedenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e1c5b-115">There are several possible causes, including:</span></span>

* <span data-ttu-id="e1c5b-116">Merhaba, içerik sıkıştırma için uygun değil istedi.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-116">hello requested content is not eligible for compression.</span></span>
* <span data-ttu-id="e1c5b-117">Sıkıştırma hello için etkin değil istenen dosya türü.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-117">Compression is not enabled for hello requested file type.</span></span>
* <span data-ttu-id="e1c5b-118">Merhaba HTTP isteği, geçerli sıkıştırma türünü isteyen bir üst bilgisi içermiyordu.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-118">hello HTTP request did not include a header requesting a valid compression type.</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="e1c5b-119">Sorun giderme adımları</span><span class="sxs-lookup"><span data-stu-id="e1c5b-119">Troubleshooting steps</span></span>
> [!TIP]
> <span data-ttu-id="e1c5b-120">Yeni uç nokta dağıtırken olduğu gibi ile bazı zaman toopropagate hello ağ üzerinden CDN yapılandırma değişiklikleri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-120">As with deploying new endpoints, CDN configuration changes take some time toopropagate through hello network.</span></span>  <span data-ttu-id="e1c5b-121">Genellikle, değişiklikler 90 dakika içinde uygulanır.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-121">Usually, changes are applied within 90 minutes.</span></span>  <span data-ttu-id="e1c5b-122">Bu hello sıkıştırmayı ayarlama, CDN uç noktası için ayarladığınız ilk kez kullanıyorsanız, 1-2 saat toobe hello sıkıştırma ayarları toohello POP dağıtıldıktan emin bekleyen düşünmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-122">If this is hello first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours toobe sure hello compression settings have propagated toohello POPs.</span></span> 
> 
> 

### <a name="verify-hello-request"></a><span data-ttu-id="e1c5b-123">Merhaba isteği doğrulayın</span><span class="sxs-lookup"><span data-stu-id="e1c5b-123">Verify hello request</span></span>
<span data-ttu-id="e1c5b-124">İlk olarak, biz hello istek üzerinde bir hızlı sağlamlık denetimi yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-124">First, we should do a quick sanity check on hello request.</span></span>  <span data-ttu-id="e1c5b-125">Tarayıcınızın kullanabilirsiniz [Geliştirici Araçları](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview hello istekleri yapılan.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-125">You can use your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview hello requests being made.</span></span>

* <span data-ttu-id="e1c5b-126">Tooyour uç nokta URL'si Hello isteği gönderiliyor doğrulayın `<endpointname>.azureedge.net`ve kaynağınıza değil.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-126">Verify hello request is being sent tooyour endpoint URL, `<endpointname>.azureedge.net`, and not your origin.</span></span>
* <span data-ttu-id="e1c5b-127">Merhaba isteği içerdiğini doğrulayın bir **Accept-Encoding** üstbilgi ve hello değer bu üst bilgiyi içeren için **gzip**, **deflate**, veya **bzıp2** .</span><span class="sxs-lookup"><span data-stu-id="e1c5b-127">Verify hello request contains an **Accept-Encoding** header, and hello value for that header contains **gzip**, **deflate**, or **bzip2**.</span></span>

> [!NOTE]
> <span data-ttu-id="e1c5b-128">**Akamai'den Azure CDN** yalnızca destek profilleri **gzip** kodlama.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-128">**Azure CDN from Akamai** profiles only support **gzip** encoding.</span></span>
> 
> 

![CDN istek üstbilgileri](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a><span data-ttu-id="e1c5b-130">Sıkıştırma ayarları (standart CDN profili) doğrulayın</span><span class="sxs-lookup"><span data-stu-id="e1c5b-130">Verify compression settings (Standard CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="e1c5b-131">CDN profilinizi ise bu adım yalnızca geçerli bir **verizon'dan Azure CDN standart** veya **akamai'den Azure CDN standart** profili.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-131">This step only applies if your CDN profile is an **Azure CDN Standard from Verizon** or **Azure CDN Standard from Akamai** profile.</span></span> 
> 
> 

<span data-ttu-id="e1c5b-132">Merhaba tooyour uç gidin [Azure portal](https://portal.azure.com) hello tıklatıp **yapılandırma** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-132">Navigate tooyour endpoint in hello [Azure portal](https://portal.azure.com) and click hello **Configure** button.</span></span>

* <span data-ttu-id="e1c5b-133">Sıkıştırma etkin doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-133">Verify compression is enabled.</span></span>
* <span data-ttu-id="e1c5b-134">Merhaba hello sıkıştırılmış toobe sıkıştırılmış biçimleri hello listesinde yer içerik için MIME türünü doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-134">Verify hello MIME type for hello content toobe compressed is included in hello list of compressed formats.</span></span>

![CDN sıkıştırma ayarları](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a><span data-ttu-id="e1c5b-136">Sıkıştırma ayarları (Premium CDN profili) doğrulayın</span><span class="sxs-lookup"><span data-stu-id="e1c5b-136">Verify compression settings (Premium CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="e1c5b-137">CDN profilinizi ise bu adım yalnızca geçerli bir **verizon'dan Azure CDN Premium** profili.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-137">This step only applies if your CDN profile is an **Azure CDN Premium from Verizon** profile.</span></span>
> 
> 

<span data-ttu-id="e1c5b-138">Merhaba tooyour uç gidin [Azure portal](https://portal.azure.com) hello tıklatıp **Yönet** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-138">Navigate tooyour endpoint in hello [Azure portal](https://portal.azure.com) and click hello **Manage** button.</span></span>  <span data-ttu-id="e1c5b-139">Merhaba ek portalı açar.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-139">hello supplemental portal will open.</span></span>  <span data-ttu-id="e1c5b-140">Merhaba üzerine getirin **HTTP büyük** sekmesini ve ardından hello üzerine getirin **önbellek ayarları** çıkma.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-140">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="e1c5b-141">Tıklatın **sıkıştırma**.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-141">Click **Compression**.</span></span> 

* <span data-ttu-id="e1c5b-142">Sıkıştırma etkin doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-142">Verify compression is enabled.</span></span>
* <span data-ttu-id="e1c5b-143">Merhaba doğrulayın **dosya türlerini** listesini içeren bir virgülle ayrılmış listesi (boşluksuz) MIME türleri.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-143">Verify hello **File Types** list contains a comma-separated list (no spaces) of MIME types.</span></span>
* <span data-ttu-id="e1c5b-144">Merhaba hello sıkıştırılmış toobe sıkıştırılmış biçimleri hello listesinde yer içerik için MIME türünü doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-144">Verify hello MIME type for hello content toobe compressed is included in hello list of compressed formats.</span></span>

![CDN premium sıkıştırma ayarları](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-hello-content-is-cached"></a><span data-ttu-id="e1c5b-146">Merhaba içerik önbelleğe doğrulayın</span><span class="sxs-lookup"><span data-stu-id="e1c5b-146">Verify hello content is cached</span></span>
> [!NOTE]
> <span data-ttu-id="e1c5b-147">CDN profilinizi ise bu adım yalnızca geçerli bir **verizon'dan Azure CDN** profil (standart veya Premium).</span><span class="sxs-lookup"><span data-stu-id="e1c5b-147">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="e1c5b-148">Tarayıcınızın Geliştirici Araçları'nı kullanarak hello yanıt üstbilgileri tooensure hello dosyası burada istenmektedir hello bölgede önbelleğe denetleyin.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-148">Using your browser's developer tools, check hello response headers tooensure hello file is cached in hello region where it is being requested.</span></span>

* <span data-ttu-id="e1c5b-149">Merhaba denetleyin **Server** yanıtı üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-149">Check hello **Server** response header.</span></span>  <span data-ttu-id="e1c5b-150">Merhaba üstbilgi hello biçiminde olması gerektiğini **Platform (POP/sunucu kimliği)**hello aşağıdaki örnekte görüldüğü gibi.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-150">hello header should have hello format **Platform (POP/Server ID)**, as seen in hello following example.</span></span>
* <span data-ttu-id="e1c5b-151">Merhaba denetleyin **X önbellek** yanıtı üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-151">Check hello **X-Cache** response header.</span></span>  <span data-ttu-id="e1c5b-152">Merhaba üstbilgi kimler **İSABET**.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-152">hello header should read **HIT**.</span></span>  

![CDN yanıt üstbilgileri](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-hello-file-meets-hello-size-requirements"></a><span data-ttu-id="e1c5b-154">Merhaba dosyası başlangıç boyutu gereksinimlerini karşıladığını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="e1c5b-154">Verify hello file meets hello size requirements</span></span>
> [!NOTE]
> <span data-ttu-id="e1c5b-155">CDN profilinizi ise bu adım yalnızca geçerli bir **verizon'dan Azure CDN** profil (standart veya Premium).</span><span class="sxs-lookup"><span data-stu-id="e1c5b-155">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="e1c5b-156">sıkıştırma için uygun toobe, bir dosya boyutu gereksinimleri aşağıdaki hello karşılaması gerekir:</span><span class="sxs-lookup"><span data-stu-id="e1c5b-156">toobe eligible for compression, a file must meet hello following size requirements:</span></span>

* <span data-ttu-id="e1c5b-157">128 bayt daha büyük.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-157">Larger than 128 bytes.</span></span>
* <span data-ttu-id="e1c5b-158">1 MB'tan küçük.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-158">Smaller than 1 MB.</span></span>

### <a name="check-hello-request-at-hello-origin-server-for-a-via-header"></a><span data-ttu-id="e1c5b-159">Merhaba kaynak sunucu için Hello isteğiyle denetleyin bir **aracılığıyla** üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="e1c5b-159">Check hello request at hello origin server for a **Via** header</span></span>
<span data-ttu-id="e1c5b-160">Merhaba **aracılığıyla** HTTP üstbilgisi gösterir isteği hello toohello web sunucusu bir proxy sunucusu tarafından geçirilen.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-160">hello **Via** HTTP header indicates toohello web server that hello request is being passed by a proxy server.</span></span>  <span data-ttu-id="e1c5b-161">Varsayılan olarak Microsoft IIS web sunucuları sıkıştırma yanıtları hello istek içerdiğinde bir **aracılığıyla** üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="e1c5b-161">Microsoft IIS web servers by default do not compress responses when hello request contains a **Via** header.</span></span>  <span data-ttu-id="e1c5b-162">toooverride Bu davranış hello aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="e1c5b-162">toooverride this behavior, perform hello following:</span></span>

* <span data-ttu-id="e1c5b-163">**IIS 6**: [ayarlamak HcNoCompressionForProxies hello IIS metatabanı özelliklerinde = "FALSE"](https://msdn.microsoft.com/library/ms525390.aspx)</span><span class="sxs-lookup"><span data-stu-id="e1c5b-163">**IIS 6**: [Set HcNoCompressionForProxies="FALSE" in hello IIS Metabase properties](https://msdn.microsoft.com/library/ms525390.aspx)</span></span>
* <span data-ttu-id="e1c5b-164">**IIS 7 ve en fazla**: [ayarlanacağı **noCompressionForHttp10** ve **noCompressionForProxies** tooFalse hello sunucu yapılandırması](http://www.iis.net/configreference/system.webserver/httpcompression)</span><span class="sxs-lookup"><span data-stu-id="e1c5b-164">**IIS 7 and up**: [Set both **noCompressionForHttp10** and **noCompressionForProxies** tooFalse in hello server configuration](http://www.iis.net/configreference/system.webserver/httpcompression)</span></span>

