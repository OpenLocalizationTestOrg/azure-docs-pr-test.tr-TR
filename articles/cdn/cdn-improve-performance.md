---
title: "Azure CDN dosyaları sıkıştırarak performansı | Microsoft Docs"
description: "Dosya aktarım hızı geliştirmeyi öğrenin ve Azure CDN dosyalarınızda sıkıştırarak sayfa yükleme performansı artırır."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: af1cddff-78d8-476b-a9d0-8c2164e4de5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 7546650e6096a880f4fb4d0c94dd4ecc00b70160
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a><span data-ttu-id="8fc89-103">Azure CDN dosyaları sıkıştırarak performansı</span><span class="sxs-lookup"><span data-stu-id="8fc89-103">Improve performance by compressing files in Azure CDN</span></span>
<span data-ttu-id="8fc89-104">Sıkıştırma, dosya aktarım hızını artırmak ve sunucudan gönderilmeden önce dosya boyutunu azaltarak sayfa yükleme performansı artırmak için basit ve etkili bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="8fc89-104">Compression is a simple and effective method to improve file transfer speed and increase page load performance by reducing file size before it is sent from the server.</span></span> <span data-ttu-id="8fc89-105">Bant genişliği maliyetlerini düşürür ve kullanıcılarınız için daha esnek bir deneyim sağlar.</span><span class="sxs-lookup"><span data-stu-id="8fc89-105">It reduces bandwidth costs and provides a more responsive experience for your users.</span></span>

<span data-ttu-id="8fc89-106">Sıkıştırmayı etkinleştirmek için iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="8fc89-106">There are two ways to enable compression:</span></span>

* <span data-ttu-id="8fc89-107">Kaynak sunucunuzda çalışması CDN sıkıştırılmış dosyaların geçirir, sıkıştırmayı etkinleştir ve sıkıştırılmış dosyaları bunları isteyen istemcilere teslim edin.</span><span class="sxs-lookup"><span data-stu-id="8fc89-107">You can enable compression on your origin server, in which case the CDN passes through the compressed files and deliver compressed files to clients that request them.</span></span>
* <span data-ttu-id="8fc89-108">Sunucularda çalışması CDN dosyaları sıkıştırır doğrudan CDN uç sıkıştırmayı etkinleştir ve kaynak sunucu tarafından sıkıştırılmaz bile, bunları son kullanıcılara hizmet.</span><span class="sxs-lookup"><span data-stu-id="8fc89-108">You can enable compression directly on CDN edge servers, in which case the CDN compresses the files and serve them to end users, even if they are not compressed by the origin server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8fc89-109">CDN yapılandırma değişiklikleri ağ üzerinden yayılması biraz zaman ayırın.</span><span class="sxs-lookup"><span data-stu-id="8fc89-109">CDN configuration changes take some time to propagate through the network.</span></span>  <span data-ttu-id="8fc89-110">İçin <b>akamai'den Azure CDN</b> profilleri yayma genellikle bir dakika içinde tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="8fc89-110">For <b>Azure CDN from Akamai</b> profiles, propagation usually completes in under one minute.</span></span>  <span data-ttu-id="8fc89-111">İçin <b>verizon'dan Azure CDN</b> profilleri değişikliklerinizin 90 dakika içinde uygulanması genellikle görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="8fc89-111">For <b>Azure CDN from Verizon</b> profiles, you will usually see your changes apply within 90 minutes.</span></span>  <span data-ttu-id="8fc89-112">CDN uç noktanız için sıkıştırmayı ayarlama ayarladınız ilk kez kullanıyorsanız, 1-2 saat ayarlarını sorun giderme önce Pop'lere yayılmadan sıkıştırma emin olmak için bekleyen düşünmelisiniz</span><span class="sxs-lookup"><span data-stu-id="8fc89-112">If this is the first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours to be sure the compression settings have propagated to the POPs before troubleshooting</span></span>
> 
> 

## <a name="enabling-compression"></a><span data-ttu-id="8fc89-113">Sıkıştırmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="8fc89-113">Enabling compression</span></span>
> [!NOTE]
> <span data-ttu-id="8fc89-114">Standart ve Premium CDN katmanları için sıkıştırma işlevsellik sağlasa da, kullanıcı arabirimi farklıdır.</span><span class="sxs-lookup"><span data-stu-id="8fc89-114">The Standard and Premium CDN tiers provide the same compression functionality, but the user interface differs.</span></span>  <span data-ttu-id="8fc89-115">Standart ve Premium CDN katmanları arasındaki farklar hakkında daha fazla bilgi için bkz: [Azure CDN'ye genel bakış](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8fc89-115">For more information about the differences between Standard and Premium CDN tiers, see [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

### <a name="standard-tier"></a><span data-ttu-id="8fc89-116">Standart katman</span><span class="sxs-lookup"><span data-stu-id="8fc89-116">Standard tier</span></span>
> [!NOTE]
> <span data-ttu-id="8fc89-117">Bu bölümde uygulandığı **verizon'dan Azure CDN standart** ve **akamai'den Azure CDN standart** profilleri.</span><span class="sxs-lookup"><span data-stu-id="8fc89-117">This section applies to **Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles.</span></span>
> 
> 

1. <span data-ttu-id="8fc89-118">CDN profili sayfasından yönetmek istediğiniz CDN uç noktası'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8fc89-118">From the CDN profile page, click the CDN endpoint you wish to manage.</span></span>
   
    ![CDN profili sayfasını uç noktaları](./media/cdn-file-compression/cdn-endpoints.png)
   
    <span data-ttu-id="8fc89-120">CDN uç noktası sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="8fc89-120">The CDN endpoint page opens.</span></span>
2. <span data-ttu-id="8fc89-121">Tıklatın **yapılandırma** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8fc89-121">Click the **Configure** button.</span></span>
   
    ![CDN profili sayfasını yönetmek düğmesi](./media/cdn-file-compression/cdn-config-btn.png)
   
    <span data-ttu-id="8fc89-123">CDN yapılandırma sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="8fc89-123">The CDN Configuration page opens.</span></span>
3. <span data-ttu-id="8fc89-124">Aç **sıkıştırma**.</span><span class="sxs-lookup"><span data-stu-id="8fc89-124">Turn on **Compression**.</span></span>
   
    ![CDN sıkıştırma seçenekleri](./media/cdn-file-compression/cdn-compress-standard.png)
4. <span data-ttu-id="8fc89-126">Varsayılan türleri kullanın veya dosya türlerini ekleyerek veya çıkararak listesini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8fc89-126">Use the default types, or modify the list by removing or adding file types.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="8fc89-127">While olası, onu ZIP, MP3, MP4, JPG, vb. gibi sıkıştırılmış biçimleri sıkıştırma uygulamak için önerilmez.</span><span class="sxs-lookup"><span data-stu-id="8fc89-127">While possible, it is not recommended to apply compression to compressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span>
   > 
   > 
5. <span data-ttu-id="8fc89-128">Yaptığınız değişiklikleri yaptıktan sonra tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8fc89-128">After making your changes, click the **Save** button.</span></span>

### <a name="premium-tier"></a><span data-ttu-id="8fc89-129">Premium katman</span><span class="sxs-lookup"><span data-stu-id="8fc89-129">Premium tier</span></span>
> [!NOTE]
> <span data-ttu-id="8fc89-130">Bu bölümde uygulandığı **verizon'dan Azure CDN Premium** profilleri.</span><span class="sxs-lookup"><span data-stu-id="8fc89-130">This section applies to **Azure CDN Premium from Verizon** profiles.</span></span>
> 
> 

1. <span data-ttu-id="8fc89-131">CDN profili sayfasından tıklatın **Yönet** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8fc89-131">From the CDN profile page, click the **Manage** button.</span></span>
   
    ![CDN profili sayfasını yönetmek düğmesi](./media/cdn-file-compression/cdn-manage-btn.png)
   
    <span data-ttu-id="8fc89-133">CDN Yönetim Portalı'nı açar.</span><span class="sxs-lookup"><span data-stu-id="8fc89-133">The CDN management portal opens.</span></span>
2. <span data-ttu-id="8fc89-134">Üzerine gelerek **HTTP büyük** sekmesini ve ardından üzerine gelerek **önbellek ayarları** çıkma.</span><span class="sxs-lookup"><span data-stu-id="8fc89-134">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="8fc89-135">Tıklayın **sıkıştırma**.</span><span class="sxs-lookup"><span data-stu-id="8fc89-135">Click on **Compression**.</span></span>

    ![Dosya sıkıştırma seçimi](./media/cdn-file-compression/cdn-compress-select.png)
   
    <span data-ttu-id="8fc89-137">Sıkıştırma seçeneklerini görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8fc89-137">Compression options are displayed.</span></span>
   
    ![Dosya sıkıştırma](./media/cdn-file-compression/cdn-compress-files.png)
3. <span data-ttu-id="8fc89-139">Tıklayarak sıkıştırmayı etkinleştir **sıkıştırma etkin** radyo düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8fc89-139">Enable compression by clicking the **Compression Enabled** radio button.</span></span>  <span data-ttu-id="8fc89-140">İstediğiniz virgülle ayrılmış liste olarak (boşluksuz) sıkıştırmak için MIME türlerini girin **dosya türlerini** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="8fc89-140">Enter the MIME types you wish to compress as a comma-delimited list (no spaces) in the **File Types** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="8fc89-141">While olası, onu ZIP, MP3, MP4, JPG, vb. gibi sıkıştırılmış biçimleri sıkıştırma uygulamak için önerilmez.</span><span class="sxs-lookup"><span data-stu-id="8fc89-141">While possible, it is not recommended to apply compression to compressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span> 
   > 
   > 
4. <span data-ttu-id="8fc89-142">Yaptığınız değişiklikleri yaptıktan sonra tıklatın **güncelleştirme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8fc89-142">After making your changes, click the **Update** button.</span></span>

## <a name="compression-rules"></a><span data-ttu-id="8fc89-143">Sıkıştırma kuralları</span><span class="sxs-lookup"><span data-stu-id="8fc89-143">Compression rules</span></span>
<span data-ttu-id="8fc89-144">Bu tablo her senaryo için Azure CDN sıkıştırma davranışı açıklar.</span><span class="sxs-lookup"><span data-stu-id="8fc89-144">These tables describe Azure CDN compression behavior for every scenario.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8fc89-145">İçin **verizon'dan Azure CDN** (standart ve Premium), yalnızca uygun dosyaları sıkıştırılır.</span><span class="sxs-lookup"><span data-stu-id="8fc89-145">For **Azure CDN from Verizon** (Standard and Premium), only eligible files are compressed.</span></span>  <span data-ttu-id="8fc89-146">Sıkıştırma için uygun olması için bir dosya gerekir:</span><span class="sxs-lookup"><span data-stu-id="8fc89-146">To be eligible for compression, a file must:</span></span>
> 
> * <span data-ttu-id="8fc89-147">128 bayttan büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8fc89-147">Be larger than 128 bytes.</span></span>
> * <span data-ttu-id="8fc89-148">1 MB'tan küçük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8fc89-148">Be smaller than 1 MB.</span></span>
> 
> <span data-ttu-id="8fc89-149">İçin **akamai'den Azure CDN**, tüm dosyalar için sıkıştırma uygundur.</span><span class="sxs-lookup"><span data-stu-id="8fc89-149">For **Azure CDN from Akamai**, all files are eligible for compression.</span></span>
> 
> <span data-ttu-id="8fc89-150">Tüm Azure CDN ürünü için bir dosya olan bir MIME türü olmalıdır [sıkıştırma için yapılandırılmış](#enabling-compression).</span><span class="sxs-lookup"><span data-stu-id="8fc89-150">For all Azure CDN products, a file must be a MIME type that has been [configured for compression](#enabling-compression).</span></span>
> 
> <span data-ttu-id="8fc89-151">**Verizon'dan Azure CDN** profilleri (standart ve Premium) Destek **gzip** (GNU zip) **deflate**, **bzıp2**, veya **br** (Brotli) kodlama.</span><span class="sxs-lookup"><span data-stu-id="8fc89-151">**Azure CDN from Verizon** profiles (Standard and Premium) support **gzip** (GNU zip), **deflate**, **bzip2**, or  **br** (Brotli) encoding.</span></span> <span data-ttu-id="8fc89-152">Brotli kodlama için sıkıştırma yalnızca sınırında yapılır.</span><span class="sxs-lookup"><span data-stu-id="8fc89-152">For Brotli encoding, the compression is done only at the edge.</span></span> <span data-ttu-id="8fc89-153">İstemci/tarayıcı Brotli kodlama için istek göndermesi gerekir ve sıkıştırılmış varlık kaynak tarafında ilk sıkıştırılmış gerekir.</span><span class="sxs-lookup"><span data-stu-id="8fc89-153">The client/browser must send the request for Brotli encoding and the compressed asset must have been compressed on the origin side first.</span></span> 
>
><span data-ttu-id="8fc89-154">**Akamai'den Azure CDN** profilleri desteği yalnızca **gzip** kodlama.</span><span class="sxs-lookup"><span data-stu-id="8fc89-154">**Azure CDN from Akamai** profiles support only **gzip** encoding.</span></span>
> 
> <span data-ttu-id="8fc89-155">**Akamai'den Azure CDN** uç noktaları her zaman isteği **gzip** kodlanmış istemci isteği bağımsız olarak kaynak dosyaları.</span><span class="sxs-lookup"><span data-stu-id="8fc89-155">**Azure CDN from Akamai** endpoints always request **gzip** encoded files from the origin, regardless of the client request.</span></span> 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a><span data-ttu-id="8fc89-156">Sıkıştırma devre dışı veya dosya sıkıştırma için uygun değil</span><span class="sxs-lookup"><span data-stu-id="8fc89-156">Compression disabled or file is ineligible for compression</span></span>
| <span data-ttu-id="8fc89-157">İstemci istenen biçimi (aracılığıyla Accept-Encoding üstbilgisi)</span><span class="sxs-lookup"><span data-stu-id="8fc89-157">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="8fc89-158">Önbelleğe alınmış dosya biçimi</span><span class="sxs-lookup"><span data-stu-id="8fc89-158">Cached file format</span></span> | <span data-ttu-id="8fc89-159">İstemciye CDN yanıtı</span><span class="sxs-lookup"><span data-stu-id="8fc89-159">CDN response to the client</span></span> | <span data-ttu-id="8fc89-160">Notlar</span><span class="sxs-lookup"><span data-stu-id="8fc89-160">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8fc89-161">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="8fc89-161">Compressed</span></span> |<span data-ttu-id="8fc89-162">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="8fc89-162">Compressed</span></span> |<span data-ttu-id="8fc89-163">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="8fc89-163">Compressed</span></span> | |
| <span data-ttu-id="8fc89-164">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="8fc89-164">Compressed</span></span> |<span data-ttu-id="8fc89-165">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="8fc89-165">Uncompressed</span></span> |<span data-ttu-id="8fc89-166">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="8fc89-166">Uncompressed</span></span> | |
| <span data-ttu-id="8fc89-167">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="8fc89-167">Compressed</span></span> |<span data-ttu-id="8fc89-168">Önbelleğe alınmamış</span><span class="sxs-lookup"><span data-stu-id="8fc89-168">Not cached</span></span> |<span data-ttu-id="8fc89-169">Sıkıştırılmış veya sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="8fc89-169">Compressed or Uncompressed</span></span> |<span data-ttu-id="8fc89-170">Kaynak yanıtta bağlıdır</span><span class="sxs-lookup"><span data-stu-id="8fc89-170">Depends on origin response</span></span> |
| <span data-ttu-id="8fc89-171">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="8fc89-171">Uncompressed</span></span> |<span data-ttu-id="8fc89-172">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="8fc89-172">Compressed</span></span> |<span data-ttu-id="8fc89-173">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="8fc89-173">Uncompressed</span></span> | |
| <span data-ttu-id="8fc89-174">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="8fc89-174">Uncompressed</span></span> |<span data-ttu-id="8fc89-175">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="8fc89-175">Uncompressed</span></span> |<span data-ttu-id="8fc89-176">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="8fc89-176">Uncompressed</span></span> | |
| <span data-ttu-id="8fc89-177">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="8fc89-177">Uncompressed</span></span> |<span data-ttu-id="8fc89-178">Önbelleğe alınmamış</span><span class="sxs-lookup"><span data-stu-id="8fc89-178">Not cached</span></span> |<span data-ttu-id="8fc89-179">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="8fc89-179">Uncompressed</span></span> | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a><span data-ttu-id="8fc89-180">Sıkıştırma ve dosya sıkıştırma için uygun</span><span class="sxs-lookup"><span data-stu-id="8fc89-180">Compression enabled and file is eligible for compression</span></span>
| <span data-ttu-id="8fc89-181">İstemci istenen biçimi (aracılığıyla Accept-Encoding üstbilgisi)</span><span class="sxs-lookup"><span data-stu-id="8fc89-181">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="8fc89-182">Önbelleğe alınmış dosya biçimi</span><span class="sxs-lookup"><span data-stu-id="8fc89-182">Cached file format</span></span> | <span data-ttu-id="8fc89-183">İstemciye CDN yanıtı</span><span class="sxs-lookup"><span data-stu-id="8fc89-183">CDN response to the client</span></span> | <span data-ttu-id="8fc89-184">Notlar</span><span class="sxs-lookup"><span data-stu-id="8fc89-184">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8fc89-185">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="8fc89-185">Compressed</span></span> |<span data-ttu-id="8fc89-186">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="8fc89-186">Compressed</span></span> |<span data-ttu-id="8fc89-187">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="8fc89-187">Compressed</span></span> |<span data-ttu-id="8fc89-188">CDN transcodes desteklenen biçimler arasında</span><span class="sxs-lookup"><span data-stu-id="8fc89-188">CDN transcodes between supported formats</span></span> |
| <span data-ttu-id="8fc89-189">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="8fc89-189">Compressed</span></span> |<span data-ttu-id="8fc89-190">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="8fc89-190">Uncompressed</span></span> |<span data-ttu-id="8fc89-191">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="8fc89-191">Compressed</span></span> |<span data-ttu-id="8fc89-192">CDN sıkıştırır.</span><span class="sxs-lookup"><span data-stu-id="8fc89-192">CDN performs compression</span></span> |
| <span data-ttu-id="8fc89-193">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="8fc89-193">Compressed</span></span> |<span data-ttu-id="8fc89-194">Önbelleğe alınmamış</span><span class="sxs-lookup"><span data-stu-id="8fc89-194">Not cached</span></span> |<span data-ttu-id="8fc89-195">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="8fc89-195">Compressed</span></span> |<span data-ttu-id="8fc89-196">Kaynak sıkıştırılmamış döndürürse CDN sıkıştırır.</span><span class="sxs-lookup"><span data-stu-id="8fc89-196">CDN performs compression if origin returns uncompressed.</span></span>  <span data-ttu-id="8fc89-197">**Verizon'dan Azure CDN** sıkıştırılmamış dosyayı ilk istek üzerine geçirir ve ardından sıkıştırır ve sonraki istekleri için dosyayı önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="8fc89-197">**Azure CDN from Verizon** passes the uncompressed file on the first request and then compresses and caches the file for subsequent requests.</span></span>  <span data-ttu-id="8fc89-198">İle dosyaları `Cache-Control: no-cache` üstbilgi hiçbir zaman sıkıştırılır.</span><span class="sxs-lookup"><span data-stu-id="8fc89-198">Files with `Cache-Control: no-cache` header will never be compressed.</span></span> |
| <span data-ttu-id="8fc89-199">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="8fc89-199">Uncompressed</span></span> |<span data-ttu-id="8fc89-200">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="8fc89-200">Compressed</span></span> |<span data-ttu-id="8fc89-201">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="8fc89-201">Uncompressed</span></span> |<span data-ttu-id="8fc89-202">CDN açma işlemi gerçekleştirir</span><span class="sxs-lookup"><span data-stu-id="8fc89-202">CDN performs decompression</span></span> |
| <span data-ttu-id="8fc89-203">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="8fc89-203">Uncompressed</span></span> |<span data-ttu-id="8fc89-204">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="8fc89-204">Uncompressed</span></span> |<span data-ttu-id="8fc89-205">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="8fc89-205">Uncompressed</span></span> | |
| <span data-ttu-id="8fc89-206">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="8fc89-206">Uncompressed</span></span> |<span data-ttu-id="8fc89-207">Önbelleğe alınmamış</span><span class="sxs-lookup"><span data-stu-id="8fc89-207">Not cached</span></span> |<span data-ttu-id="8fc89-208">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="8fc89-208">Uncompressed</span></span> | |

## <a name="media-services-cdn-compression"></a><span data-ttu-id="8fc89-209">CDN sıkıştırma medya Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="8fc89-209">Media Services CDN Compression</span></span>
<span data-ttu-id="8fc89-210">Medya Hizmetleri CDN akış uç noktalarını etkin sıkıştırma aşağıdaki içerik türleri için varsayılan olarak etkindir: uygulama/vnd.ms-sstr + xml, application/dash+xml,application/vnd.apple.mpegurl, uygulama/f4m + xml.</span><span class="sxs-lookup"><span data-stu-id="8fc89-210">For Media Services CDN enabled streaming endpoints, compression is enabled by default for the following content types: application/vnd.ms-sstr+xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m+xml.</span></span> <span data-ttu-id="8fc89-211">Azure portalını kullanarak belirtilen türleri için sıkıştırma bırakmak olamaz.</span><span class="sxs-lookup"><span data-stu-id="8fc89-211">You cannot enable/disable compression for the mentioned types using the Azure portal.</span></span>  

## <a name="see-also"></a><span data-ttu-id="8fc89-212">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="8fc89-212">See also</span></span>
* [<span data-ttu-id="8fc89-213">CDN dosya sıkıştırma sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="8fc89-213">Troubleshooting CDN file compression</span></span>](cdn-troubleshoot-compression.md)    

