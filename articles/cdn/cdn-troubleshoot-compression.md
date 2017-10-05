---
title: "Azure CDN dosya sıkıştırma sorunlarını giderme | Microsoft Docs"
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
ms.openlocfilehash: 5ef8a8262eb40aa827161764f03a63d031e43273
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-cdn-file-compression"></a><span data-ttu-id="a579a-103">CDN dosya sıkıştırma sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="a579a-103">Troubleshooting CDN file compression</span></span>
<span data-ttu-id="a579a-104">Bu makale ile ilgili sorunları gidermenize yardımcı [CDN dosya sıkıştırma](cdn-improve-performance.md).</span><span class="sxs-lookup"><span data-stu-id="a579a-104">This article helps you troubleshoot issues with [CDN file compression](cdn-improve-performance.md).</span></span>

<span data-ttu-id="a579a-105">Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, üzerinde Azure uzmanlar başvurabilirsiniz [MSDN Azure ve yığın taşması forumlar](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="a579a-105">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="a579a-106">Alternatif olarak, Azure destek olay dosya.</span><span class="sxs-lookup"><span data-stu-id="a579a-106">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="a579a-107">Git [Azure Destek sitesi](https://azure.microsoft.com/support/options/) tıklatıp **destek alın**.</span><span class="sxs-lookup"><span data-stu-id="a579a-107">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="a579a-108">Belirti</span><span class="sxs-lookup"><span data-stu-id="a579a-108">Symptom</span></span>
<span data-ttu-id="a579a-109">Uç noktanız için sıkıştırma etkin, ancak dosyalar sıkıştırılmamış döndürülen.</span><span class="sxs-lookup"><span data-stu-id="a579a-109">Compression for your endpoint is enabled, but files are being returned uncompressed.</span></span>

> [!TIP]
> <span data-ttu-id="a579a-110">Dosyaları sıkıştırılmış döndürülen olup olmadığını denetlemek için gibi bir araç kullanmanız gerekir [Fiddler](http://www.telerik.com/fiddler) veya tarayıcınızın [Geliştirici Araçları](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span><span class="sxs-lookup"><span data-stu-id="a579a-110">To check whether your files are being returned compressed, you need to use a tool like [Fiddler](http://www.telerik.com/fiddler) or your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span></span>  <span data-ttu-id="a579a-111">Onay HTTP yanıt üstbilgilerini, önbelleğe alınan CDN içerik döndürdü.</span><span class="sxs-lookup"><span data-stu-id="a579a-111">Check the HTTP response headers returned with your cached CDN content.</span></span>  <span data-ttu-id="a579a-112">Adlı bir üst bilgi olup olmadığını `Content-Encoding` değerini **gzip**, **bzıp2**, veya **deflate**, içeriğinizi sıkıştırılır.</span><span class="sxs-lookup"><span data-stu-id="a579a-112">If there is a header named `Content-Encoding` with a value of **gzip**, **bzip2**, or **deflate**, your content is compressed.</span></span>
> 
> ![İçerik Kodlama üstbilgisi](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a><span data-ttu-id="a579a-114">Nedeni</span><span class="sxs-lookup"><span data-stu-id="a579a-114">Cause</span></span>
<span data-ttu-id="a579a-115">Dahil birkaç olası nedenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a579a-115">There are several possible causes, including:</span></span>

* <span data-ttu-id="a579a-116">İstenen içerik sıkıştırma için uygun değil.</span><span class="sxs-lookup"><span data-stu-id="a579a-116">The requested content is not eligible for compression.</span></span>
* <span data-ttu-id="a579a-117">Sıkıştırma istenen dosya türü için etkin değil.</span><span class="sxs-lookup"><span data-stu-id="a579a-117">Compression is not enabled for the requested file type.</span></span>
* <span data-ttu-id="a579a-118">HTTP isteği, geçerli sıkıştırma türünü isteyen bir üst bilgisi içermiyordu.</span><span class="sxs-lookup"><span data-stu-id="a579a-118">The HTTP request did not include a header requesting a valid compression type.</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="a579a-119">Sorun giderme adımları</span><span class="sxs-lookup"><span data-stu-id="a579a-119">Troubleshooting steps</span></span>
> [!TIP]
> <span data-ttu-id="a579a-120">Yeni uç nokta dağıtırken olduğu gibi ile CDN yapılandırma değişiklikleri ağ üzerinden yayılması biraz zaman ayırın.</span><span class="sxs-lookup"><span data-stu-id="a579a-120">As with deploying new endpoints, CDN configuration changes take some time to propagate through the network.</span></span>  <span data-ttu-id="a579a-121">Genellikle, değişiklikler 90 dakika içinde uygulanır.</span><span class="sxs-lookup"><span data-stu-id="a579a-121">Usually, changes are applied within 90 minutes.</span></span>  <span data-ttu-id="a579a-122">CDN uç noktanız için sıkıştırmayı ayarlama ayarladınız ilk kez kullanıyorsanız, 1-2 saat ayarlarını Pop'lere yayılmadan sıkıştırma emin olmak için bekleyen düşünmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="a579a-122">If this is the first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours to be sure the compression settings have propagated to the POPs.</span></span> 
> 
> 

### <a name="verify-the-request"></a><span data-ttu-id="a579a-123">İsteği doğrulama</span><span class="sxs-lookup"><span data-stu-id="a579a-123">Verify the request</span></span>
<span data-ttu-id="a579a-124">İlk olarak, biz istek üzerinde bir hızlı sağlamlık denetimi yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a579a-124">First, we should do a quick sanity check on the request.</span></span>  <span data-ttu-id="a579a-125">Tarayıcınızın kullanabilirsiniz [Geliştirici Araçları](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) yapılan istekleri görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="a579a-125">You can use your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) to view the requests being made.</span></span>

* <span data-ttu-id="a579a-126">Uç nokta URL'nizi isteği gönderiliyor doğrulayın `<endpointname>.azureedge.net`ve kaynağınıza değil.</span><span class="sxs-lookup"><span data-stu-id="a579a-126">Verify the request is being sent to your endpoint URL, `<endpointname>.azureedge.net`, and not your origin.</span></span>
* <span data-ttu-id="a579a-127">İstek içerdiğini doğrulayın bir **Accept-Encoding** üstbilgi ve o üstbilgisi değeri içeren **gzip**, **deflate**, veya **bzıp2**.</span><span class="sxs-lookup"><span data-stu-id="a579a-127">Verify the request contains an **Accept-Encoding** header, and the value for that header contains **gzip**, **deflate**, or **bzip2**.</span></span>

> [!NOTE]
> <span data-ttu-id="a579a-128">**Akamai'den Azure CDN** yalnızca destek profilleri **gzip** kodlama.</span><span class="sxs-lookup"><span data-stu-id="a579a-128">**Azure CDN from Akamai** profiles only support **gzip** encoding.</span></span>
> 
> 

![CDN istek üstbilgileri](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a><span data-ttu-id="a579a-130">Sıkıştırma ayarları (standart CDN profili) doğrulayın</span><span class="sxs-lookup"><span data-stu-id="a579a-130">Verify compression settings (Standard CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="a579a-131">CDN profilinizi ise bu adım yalnızca geçerli bir **verizon'dan Azure CDN standart** veya **akamai'den Azure CDN standart** profili.</span><span class="sxs-lookup"><span data-stu-id="a579a-131">This step only applies if your CDN profile is an **Azure CDN Standard from Verizon** or **Azure CDN Standard from Akamai** profile.</span></span> 
> 
> 

<span data-ttu-id="a579a-132">Uç noktanız gidin [Azure portal](https://portal.azure.com) tıklatıp **yapılandırma** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a579a-132">Navigate to your endpoint in the [Azure portal](https://portal.azure.com) and click the **Configure** button.</span></span>

* <span data-ttu-id="a579a-133">Sıkıştırma etkin doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a579a-133">Verify compression is enabled.</span></span>
* <span data-ttu-id="a579a-134">Sıkıştırılacak içerik için MIME türü sıkıştırılmış biçimleri listesinde yer doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a579a-134">Verify the MIME type for the content to be compressed is included in the list of compressed formats.</span></span>

![CDN sıkıştırma ayarları](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a><span data-ttu-id="a579a-136">Sıkıştırma ayarları (Premium CDN profili) doğrulayın</span><span class="sxs-lookup"><span data-stu-id="a579a-136">Verify compression settings (Premium CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="a579a-137">CDN profilinizi ise bu adım yalnızca geçerli bir **verizon'dan Azure CDN Premium** profili.</span><span class="sxs-lookup"><span data-stu-id="a579a-137">This step only applies if your CDN profile is an **Azure CDN Premium from Verizon** profile.</span></span>
> 
> 

<span data-ttu-id="a579a-138">Uç noktanız gidin [Azure portal](https://portal.azure.com) tıklatıp **Yönet** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a579a-138">Navigate to your endpoint in the [Azure portal](https://portal.azure.com) and click the **Manage** button.</span></span>  <span data-ttu-id="a579a-139">Ek Portalı'nı açar.</span><span class="sxs-lookup"><span data-stu-id="a579a-139">The supplemental portal will open.</span></span>  <span data-ttu-id="a579a-140">Üzerine gelerek **HTTP büyük** sekmesini ve ardından üzerine gelerek **önbellek ayarları** çıkma.</span><span class="sxs-lookup"><span data-stu-id="a579a-140">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="a579a-141">Tıklatın **sıkıştırma**.</span><span class="sxs-lookup"><span data-stu-id="a579a-141">Click **Compression**.</span></span> 

* <span data-ttu-id="a579a-142">Sıkıştırma etkin doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a579a-142">Verify compression is enabled.</span></span>
* <span data-ttu-id="a579a-143">Doğrulama **dosya türlerini** listesini içeren bir virgülle ayrılmış listesi (boşluksuz) MIME türleri.</span><span class="sxs-lookup"><span data-stu-id="a579a-143">Verify the **File Types** list contains a comma-separated list (no spaces) of MIME types.</span></span>
* <span data-ttu-id="a579a-144">Sıkıştırılacak içerik için MIME türü sıkıştırılmış biçimleri listesinde yer doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a579a-144">Verify the MIME type for the content to be compressed is included in the list of compressed formats.</span></span>

![CDN premium sıkıştırma ayarları](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-the-content-is-cached"></a><span data-ttu-id="a579a-146">İçerik önbelleğe doğrulayın</span><span class="sxs-lookup"><span data-stu-id="a579a-146">Verify the content is cached</span></span>
> [!NOTE]
> <span data-ttu-id="a579a-147">CDN profilinizi ise bu adım yalnızca geçerli bir **verizon'dan Azure CDN** profil (standart veya Premium).</span><span class="sxs-lookup"><span data-stu-id="a579a-147">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="a579a-148">Tarayıcınızın Geliştirici Araçları'nı kullanarak dosyanın nereye istenmektedir bölgede önbelleğe sağlamak için yanıt üstbilgilerini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="a579a-148">Using your browser's developer tools, check the response headers to ensure the file is cached in the region where it is being requested.</span></span>

* <span data-ttu-id="a579a-149">Denetleme **Server** yanıtı üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="a579a-149">Check the **Server** response header.</span></span>  <span data-ttu-id="a579a-150">Üst bilgisi biçiminde olması **Platform (POP/sunucu kimliği)**, aşağıdaki örnekte görüldüğü gibi.</span><span class="sxs-lookup"><span data-stu-id="a579a-150">The header should have the format **Platform (POP/Server ID)**, as seen in the following example.</span></span>
* <span data-ttu-id="a579a-151">Denetleme **X önbellek** yanıtı üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="a579a-151">Check the **X-Cache** response header.</span></span>  <span data-ttu-id="a579a-152">Üstbilgi okumalısınız **İSABET**.</span><span class="sxs-lookup"><span data-stu-id="a579a-152">The header should read **HIT**.</span></span>  

![CDN yanıt üstbilgileri](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-the-file-meets-the-size-requirements"></a><span data-ttu-id="a579a-154">Dosya boyutu gereksinimleri karşıladığını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="a579a-154">Verify the file meets the size requirements</span></span>
> [!NOTE]
> <span data-ttu-id="a579a-155">CDN profilinizi ise bu adım yalnızca geçerli bir **verizon'dan Azure CDN** profil (standart veya Premium).</span><span class="sxs-lookup"><span data-stu-id="a579a-155">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="a579a-156">Sıkıştırma için uygun olması için bir dosya aşağıdaki boyut gereksinimlerini karşılaması gerekir:</span><span class="sxs-lookup"><span data-stu-id="a579a-156">To be eligible for compression, a file must meet the following size requirements:</span></span>

* <span data-ttu-id="a579a-157">128 bayt daha büyük.</span><span class="sxs-lookup"><span data-stu-id="a579a-157">Larger than 128 bytes.</span></span>
* <span data-ttu-id="a579a-158">1 MB'tan küçük.</span><span class="sxs-lookup"><span data-stu-id="a579a-158">Smaller than 1 MB.</span></span>

### <a name="check-the-request-at-the-origin-server-for-a-via-header"></a><span data-ttu-id="a579a-159">İstek için kaynak sunucuda denetleyin bir **aracılığıyla** üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="a579a-159">Check the request at the origin server for a **Via** header</span></span>
<span data-ttu-id="a579a-160">**Aracılığıyla** HTTP üstbilgisi web sunucusuna istek bir proxy sunucusu tarafından geçirilen gösterir.</span><span class="sxs-lookup"><span data-stu-id="a579a-160">The **Via** HTTP header indicates to the web server that the request is being passed by a proxy server.</span></span>  <span data-ttu-id="a579a-161">Varsayılan olarak Microsoft IIS web sunucuları sıkıştırma yanıtları istek içerdiğinde bir **aracılığıyla** üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="a579a-161">Microsoft IIS web servers by default do not compress responses when the request contains a **Via** header.</span></span>  <span data-ttu-id="a579a-162">Bu davranışı değiştirmek için aşağıdakileri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a579a-162">To override this behavior, perform the following:</span></span>

* <span data-ttu-id="a579a-163">**IIS 6**: [HcNoCompressionForProxies ayarlama IIS metatabanı özelliklerinde = "FALSE"](https://msdn.microsoft.com/library/ms525390.aspx)</span><span class="sxs-lookup"><span data-stu-id="a579a-163">**IIS 6**: [Set HcNoCompressionForProxies="FALSE" in the IIS Metabase properties](https://msdn.microsoft.com/library/ms525390.aspx)</span></span>
* <span data-ttu-id="a579a-164">**IIS 7 ve en fazla**: [ayarlanacağı **noCompressionForHttp10** ve **noCompressionForProxies** false olarak sunucu yapılandırması](http://www.iis.net/configreference/system.webserver/httpcompression)</span><span class="sxs-lookup"><span data-stu-id="a579a-164">**IIS 7 and up**: [Set both **noCompressionForHttp10** and **noCompressionForProxies** to False in the server configuration](http://www.iis.net/configreference/system.webserver/httpcompression)</span></span>

