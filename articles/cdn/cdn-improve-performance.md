---
title: "Azure CDN dosyalarında sıkıştırma aaaImprove performansı | Microsoft Docs"
description: "Nasıl tooimprove dosya aktarma hızı ve artar sayfa yükleme performansı Azure CDN dosyalarınızda sıkıştırarak öğrenin."
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
ms.openlocfilehash: 9a1698b6c29233c2e2e6fb17cdd8e919ae8bfa1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a><span data-ttu-id="959c3-103">Azure CDN dosyaları sıkıştırarak performansı</span><span class="sxs-lookup"><span data-stu-id="959c3-103">Improve performance by compressing files in Azure CDN</span></span>
<span data-ttu-id="959c3-104">Basit ve etkili yöntemi tooimprove dosya aktarım hızı sıkıştırma olduğu ve önceki dosya boyutunu azaltarak sayfa yükleme performansı artırır hello sunucudan gönderilir.</span><span class="sxs-lookup"><span data-stu-id="959c3-104">Compression is a simple and effective method tooimprove file transfer speed and increase page load performance by reducing file size before it is sent from hello server.</span></span> <span data-ttu-id="959c3-105">Bant genişliği maliyetlerini düşürür ve kullanıcılarınız için daha esnek bir deneyim sağlar.</span><span class="sxs-lookup"><span data-stu-id="959c3-105">It reduces bandwidth costs and provides a more responsive experience for your users.</span></span>

<span data-ttu-id="959c3-106">Tooenable sıkıştırma iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="959c3-106">There are two ways tooenable compression:</span></span>

* <span data-ttu-id="959c3-107">Bu durumda hello hello CDN geçer sıkıştırılmış dosyaları dışarıda bırak ve bunları isteyen sıkıştırılmış dosyaların tooclients teslim kaynak sunucunuzda sıkıştırmasını etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="959c3-107">You can enable compression on your origin server, in which case hello CDN passes through hello compressed files and deliver compressed files tooclients that request them.</span></span>
* <span data-ttu-id="959c3-108">Servis talebi hello CDN sıkıştırır dosyaları hello ve hello kaynak sunucu tarafından sıkıştırılmaz olsa bile bunları tooend kullanıcılar, hizmet doğrudan CDN uç sunucularında sıkıştırmasını etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="959c3-108">You can enable compression directly on CDN edge servers, in which case hello CDN compresses hello files and serve them tooend users, even if they are not compressed by hello origin server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="959c3-109">CDN yapılandırma değişikliklerini bazı zaman toopropagate hello ağ üzerinden alın.</span><span class="sxs-lookup"><span data-stu-id="959c3-109">CDN configuration changes take some time toopropagate through hello network.</span></span>  <span data-ttu-id="959c3-110">İçin <b>akamai'den Azure CDN</b> profilleri yayma genellikle bir dakika içinde tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="959c3-110">For <b>Azure CDN from Akamai</b> profiles, propagation usually completes in under one minute.</span></span>  <span data-ttu-id="959c3-111">İçin <b>verizon'dan Azure CDN</b> profilleri değişikliklerinizin 90 dakika içinde uygulanması genellikle görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="959c3-111">For <b>Azure CDN from Verizon</b> profiles, you will usually see your changes apply within 90 minutes.</span></span>  <span data-ttu-id="959c3-112">Bu hello sıkıştırmayı ayarlama, CDN uç noktası için ayarladığınız ilk kez kullanıyorsanız, 1-2 saat toobe hello sıkıştırma ayarları sorun giderme önce toohello POP dağıtıldıktan emin bekleyen düşünmelisiniz</span><span class="sxs-lookup"><span data-stu-id="959c3-112">If this is hello first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours toobe sure hello compression settings have propagated toohello POPs before troubleshooting</span></span>
> 
> 

## <a name="enabling-compression"></a><span data-ttu-id="959c3-113">Sıkıştırmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="959c3-113">Enabling compression</span></span>
> [!NOTE]
> <span data-ttu-id="959c3-114">Merhaba standart ve Premium CDN katmanları sağlamak hello aynı sıkıştırma işlevselliği, ancak hello kullanıcı arabirimi farklıdır.</span><span class="sxs-lookup"><span data-stu-id="959c3-114">hello Standard and Premium CDN tiers provide hello same compression functionality, but hello user interface differs.</span></span>  <span data-ttu-id="959c3-115">Hello standart ve Premium CDN katmanları arasındaki farklar hakkında daha fazla bilgi için bkz: [Azure CDN'ye genel bakış](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="959c3-115">For more information about hello differences between Standard and Premium CDN tiers, see [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

### <a name="standard-tier"></a><span data-ttu-id="959c3-116">Standart katman</span><span class="sxs-lookup"><span data-stu-id="959c3-116">Standard tier</span></span>
> [!NOTE]
> <span data-ttu-id="959c3-117">Bu bölüm çok geçerlidir**verizon'dan Azure CDN standart** ve **akamai'den Azure CDN standart** profilleri.</span><span class="sxs-lookup"><span data-stu-id="959c3-117">This section applies too**Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles.</span></span>
> 
> 

1. <span data-ttu-id="959c3-118">Merhaba CDN profili sayfasından toomanage istediğiniz hello CDN uç noktası'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="959c3-118">From hello CDN profile page, click hello CDN endpoint you wish toomanage.</span></span>
   
    ![CDN profili sayfasını uç noktaları](./media/cdn-file-compression/cdn-endpoints.png)
   
    <span data-ttu-id="959c3-120">Merhaba CDN uç noktası sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="959c3-120">hello CDN endpoint page opens.</span></span>
2. <span data-ttu-id="959c3-121">Merhaba tıklatın **yapılandırma** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="959c3-121">Click hello **Configure** button.</span></span>
   
    ![CDN profili sayfasını yönetmek düğmesi](./media/cdn-file-compression/cdn-config-btn.png)
   
    <span data-ttu-id="959c3-123">Merhaba CDN yapılandırma sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="959c3-123">hello CDN Configuration page opens.</span></span>
3. <span data-ttu-id="959c3-124">Aç **sıkıştırma**.</span><span class="sxs-lookup"><span data-stu-id="959c3-124">Turn on **Compression**.</span></span>
   
    ![CDN sıkıştırma seçenekleri](./media/cdn-file-compression/cdn-compress-standard.png)
4. <span data-ttu-id="959c3-126">Merhaba varsayılan türleri kullanın veya dosya türlerini ekleyerek veya çıkararak hello listesini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="959c3-126">Use hello default types, or modify hello list by removing or adding file types.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="959c3-127">While olası ZIP, MP3, MP4, JPG, vb. gibi tooapply sıkıştırma toocompressed biçimleri önerilmez.</span><span class="sxs-lookup"><span data-stu-id="959c3-127">While possible, it is not recommended tooapply compression toocompressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span>
   > 
   > 
5. <span data-ttu-id="959c3-128">Yaptığınız değişiklikleri yaptıktan sonra hello tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="959c3-128">After making your changes, click hello **Save** button.</span></span>

### <a name="premium-tier"></a><span data-ttu-id="959c3-129">Premium katman</span><span class="sxs-lookup"><span data-stu-id="959c3-129">Premium tier</span></span>
> [!NOTE]
> <span data-ttu-id="959c3-130">Bu bölüm çok geçerlidir**verizon'dan Azure CDN Premium** profilleri.</span><span class="sxs-lookup"><span data-stu-id="959c3-130">This section applies too**Azure CDN Premium from Verizon** profiles.</span></span>
> 
> 

1. <span data-ttu-id="959c3-131">Merhaba CDN profili sayfasından hello tıklatın **Yönet** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="959c3-131">From hello CDN profile page, click hello **Manage** button.</span></span>
   
    ![CDN profili sayfasını yönetmek düğmesi](./media/cdn-file-compression/cdn-manage-btn.png)
   
    <span data-ttu-id="959c3-133">Merhaba CDN Yönetim Portalı açar.</span><span class="sxs-lookup"><span data-stu-id="959c3-133">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="959c3-134">Merhaba üzerine getirin **HTTP büyük** sekmesini ve ardından hello üzerine getirin **önbellek ayarları** çıkma.</span><span class="sxs-lookup"><span data-stu-id="959c3-134">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="959c3-135">Tıklayın **sıkıştırma**.</span><span class="sxs-lookup"><span data-stu-id="959c3-135">Click on **Compression**.</span></span>

    ![Dosya sıkıştırma seçimi](./media/cdn-file-compression/cdn-compress-select.png)
   
    <span data-ttu-id="959c3-137">Sıkıştırma seçeneklerini görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="959c3-137">Compression options are displayed.</span></span>
   
    ![Dosya sıkıştırma](./media/cdn-file-compression/cdn-compress-files.png)
3. <span data-ttu-id="959c3-139">Merhaba tıklayarak sıkıştırmayı etkinleştir **sıkıştırma etkin** radyo düğmesi.</span><span class="sxs-lookup"><span data-stu-id="959c3-139">Enable compression by clicking hello **Compression Enabled** radio button.</span></span>  <span data-ttu-id="959c3-140">Merhaba MIME türleri bir virgülle ayrılmış liste olarak (boşluksuz) hello toocompress istediğiniz **dosya türlerini** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="959c3-140">Enter hello MIME types you wish toocompress as a comma-delimited list (no spaces) in hello **File Types** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="959c3-141">While olası ZIP, MP3, MP4, JPG, vb. gibi tooapply sıkıştırma toocompressed biçimleri önerilmez.</span><span class="sxs-lookup"><span data-stu-id="959c3-141">While possible, it is not recommended tooapply compression toocompressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span> 
   > 
   > 
4. <span data-ttu-id="959c3-142">Yaptığınız değişiklikleri yaptıktan sonra hello tıklatın **güncelleştirme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="959c3-142">After making your changes, click hello **Update** button.</span></span>

## <a name="compression-rules"></a><span data-ttu-id="959c3-143">Sıkıştırma kuralları</span><span class="sxs-lookup"><span data-stu-id="959c3-143">Compression rules</span></span>
<span data-ttu-id="959c3-144">Bu tablo her senaryo için Azure CDN sıkıştırma davranışı açıklar.</span><span class="sxs-lookup"><span data-stu-id="959c3-144">These tables describe Azure CDN compression behavior for every scenario.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="959c3-145">İçin **verizon'dan Azure CDN** (standart ve Premium), yalnızca uygun dosyaları sıkıştırılır.</span><span class="sxs-lookup"><span data-stu-id="959c3-145">For **Azure CDN from Verizon** (Standard and Premium), only eligible files are compressed.</span></span>  <span data-ttu-id="959c3-146">sıkıştırma için uygun toobe, bir dosya gerekir:</span><span class="sxs-lookup"><span data-stu-id="959c3-146">toobe eligible for compression, a file must:</span></span>
> 
> * <span data-ttu-id="959c3-147">128 bayttan büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="959c3-147">Be larger than 128 bytes.</span></span>
> * <span data-ttu-id="959c3-148">1 MB'tan küçük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="959c3-148">Be smaller than 1 MB.</span></span>
> 
> <span data-ttu-id="959c3-149">İçin **akamai'den Azure CDN**, tüm dosyalar için sıkıştırma uygundur.</span><span class="sxs-lookup"><span data-stu-id="959c3-149">For **Azure CDN from Akamai**, all files are eligible for compression.</span></span>
> 
> <span data-ttu-id="959c3-150">Tüm Azure CDN ürünü için bir dosya olan bir MIME türü olmalıdır [sıkıştırma için yapılandırılmış](#enabling-compression).</span><span class="sxs-lookup"><span data-stu-id="959c3-150">For all Azure CDN products, a file must be a MIME type that has been [configured for compression](#enabling-compression).</span></span>
> 
> <span data-ttu-id="959c3-151">**Verizon'dan Azure CDN** profilleri (standart ve Premium) Destek **gzip** (GNU zip) **deflate**, **bzıp2**, veya **br** (Brotli) kodlama.</span><span class="sxs-lookup"><span data-stu-id="959c3-151">**Azure CDN from Verizon** profiles (Standard and Premium) support **gzip** (GNU zip), **deflate**, **bzip2**, or  **br** (Brotli) encoding.</span></span> <span data-ttu-id="959c3-152">Brotli kodlama için hello sıkıştırma yalnızca hello sınırında yapılır.</span><span class="sxs-lookup"><span data-stu-id="959c3-152">For Brotli encoding, hello compression is done only at hello edge.</span></span> <span data-ttu-id="959c3-153">Merhaba istemci/tarayıcı Brotli kodlama için hello istek göndermesi gerekir ve hello sıkıştırılmış varlık hello kaynak tarafında ilk sıkıştırılmış gerekir.</span><span class="sxs-lookup"><span data-stu-id="959c3-153">hello client/browser must send hello request for Brotli encoding and hello compressed asset must have been compressed on hello origin side first.</span></span> 
>
><span data-ttu-id="959c3-154">**Akamai'den Azure CDN** profilleri desteği yalnızca **gzip** kodlama.</span><span class="sxs-lookup"><span data-stu-id="959c3-154">**Azure CDN from Akamai** profiles support only **gzip** encoding.</span></span>
> 
> <span data-ttu-id="959c3-155">**Akamai'den Azure CDN** uç noktaları her zaman isteği **gzip** kodlanmış hello istemci isteği bakılmaksızın hello kaynak dosyalarından.</span><span class="sxs-lookup"><span data-stu-id="959c3-155">**Azure CDN from Akamai** endpoints always request **gzip** encoded files from hello origin, regardless of hello client request.</span></span> 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a><span data-ttu-id="959c3-156">Sıkıştırma devre dışı veya dosya sıkıştırma için uygun değil</span><span class="sxs-lookup"><span data-stu-id="959c3-156">Compression disabled or file is ineligible for compression</span></span>
| <span data-ttu-id="959c3-157">İstemci istenen biçimi (aracılığıyla Accept-Encoding üstbilgisi)</span><span class="sxs-lookup"><span data-stu-id="959c3-157">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="959c3-158">Önbelleğe alınmış dosya biçimi</span><span class="sxs-lookup"><span data-stu-id="959c3-158">Cached file format</span></span> | <span data-ttu-id="959c3-159">CDN yanıt toohello istemci</span><span class="sxs-lookup"><span data-stu-id="959c3-159">CDN response toohello client</span></span> | <span data-ttu-id="959c3-160">Notlar</span><span class="sxs-lookup"><span data-stu-id="959c3-160">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="959c3-161">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="959c3-161">Compressed</span></span> |<span data-ttu-id="959c3-162">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="959c3-162">Compressed</span></span> |<span data-ttu-id="959c3-163">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="959c3-163">Compressed</span></span> | |
| <span data-ttu-id="959c3-164">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="959c3-164">Compressed</span></span> |<span data-ttu-id="959c3-165">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="959c3-165">Uncompressed</span></span> |<span data-ttu-id="959c3-166">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="959c3-166">Uncompressed</span></span> | |
| <span data-ttu-id="959c3-167">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="959c3-167">Compressed</span></span> |<span data-ttu-id="959c3-168">Önbelleğe alınmamış</span><span class="sxs-lookup"><span data-stu-id="959c3-168">Not cached</span></span> |<span data-ttu-id="959c3-169">Sıkıştırılmış veya sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="959c3-169">Compressed or Uncompressed</span></span> |<span data-ttu-id="959c3-170">Kaynak yanıtta bağlıdır</span><span class="sxs-lookup"><span data-stu-id="959c3-170">Depends on origin response</span></span> |
| <span data-ttu-id="959c3-171">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="959c3-171">Uncompressed</span></span> |<span data-ttu-id="959c3-172">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="959c3-172">Compressed</span></span> |<span data-ttu-id="959c3-173">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="959c3-173">Uncompressed</span></span> | |
| <span data-ttu-id="959c3-174">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="959c3-174">Uncompressed</span></span> |<span data-ttu-id="959c3-175">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="959c3-175">Uncompressed</span></span> |<span data-ttu-id="959c3-176">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="959c3-176">Uncompressed</span></span> | |
| <span data-ttu-id="959c3-177">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="959c3-177">Uncompressed</span></span> |<span data-ttu-id="959c3-178">Önbelleğe alınmamış</span><span class="sxs-lookup"><span data-stu-id="959c3-178">Not cached</span></span> |<span data-ttu-id="959c3-179">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="959c3-179">Uncompressed</span></span> | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a><span data-ttu-id="959c3-180">Sıkıştırma ve dosya sıkıştırma için uygun</span><span class="sxs-lookup"><span data-stu-id="959c3-180">Compression enabled and file is eligible for compression</span></span>
| <span data-ttu-id="959c3-181">İstemci istenen biçimi (aracılığıyla Accept-Encoding üstbilgisi)</span><span class="sxs-lookup"><span data-stu-id="959c3-181">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="959c3-182">Önbelleğe alınmış dosya biçimi</span><span class="sxs-lookup"><span data-stu-id="959c3-182">Cached file format</span></span> | <span data-ttu-id="959c3-183">CDN yanıt toohello istemci</span><span class="sxs-lookup"><span data-stu-id="959c3-183">CDN response toohello client</span></span> | <span data-ttu-id="959c3-184">Notlar</span><span class="sxs-lookup"><span data-stu-id="959c3-184">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="959c3-185">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="959c3-185">Compressed</span></span> |<span data-ttu-id="959c3-186">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="959c3-186">Compressed</span></span> |<span data-ttu-id="959c3-187">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="959c3-187">Compressed</span></span> |<span data-ttu-id="959c3-188">CDN transcodes desteklenen biçimler arasında</span><span class="sxs-lookup"><span data-stu-id="959c3-188">CDN transcodes between supported formats</span></span> |
| <span data-ttu-id="959c3-189">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="959c3-189">Compressed</span></span> |<span data-ttu-id="959c3-190">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="959c3-190">Uncompressed</span></span> |<span data-ttu-id="959c3-191">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="959c3-191">Compressed</span></span> |<span data-ttu-id="959c3-192">CDN sıkıştırır.</span><span class="sxs-lookup"><span data-stu-id="959c3-192">CDN performs compression</span></span> |
| <span data-ttu-id="959c3-193">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="959c3-193">Compressed</span></span> |<span data-ttu-id="959c3-194">Önbelleğe alınmamış</span><span class="sxs-lookup"><span data-stu-id="959c3-194">Not cached</span></span> |<span data-ttu-id="959c3-195">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="959c3-195">Compressed</span></span> |<span data-ttu-id="959c3-196">Kaynak sıkıştırılmamış döndürürse CDN sıkıştırır.</span><span class="sxs-lookup"><span data-stu-id="959c3-196">CDN performs compression if origin returns uncompressed.</span></span>  <span data-ttu-id="959c3-197">**Verizon'dan Azure CDN** geçişleri hello sıkıştırılmamış dosyayı hello ilk isteği ve ardından sıkıştırır ve önbellekleri hello sonraki istekleri için dosya.</span><span class="sxs-lookup"><span data-stu-id="959c3-197">**Azure CDN from Verizon** passes hello uncompressed file on hello first request and then compresses and caches hello file for subsequent requests.</span></span>  <span data-ttu-id="959c3-198">İle dosyaları `Cache-Control: no-cache` üstbilgi hiçbir zaman sıkıştırılır.</span><span class="sxs-lookup"><span data-stu-id="959c3-198">Files with `Cache-Control: no-cache` header will never be compressed.</span></span> |
| <span data-ttu-id="959c3-199">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="959c3-199">Uncompressed</span></span> |<span data-ttu-id="959c3-200">Sıkıştırılmış</span><span class="sxs-lookup"><span data-stu-id="959c3-200">Compressed</span></span> |<span data-ttu-id="959c3-201">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="959c3-201">Uncompressed</span></span> |<span data-ttu-id="959c3-202">CDN açma işlemi gerçekleştirir</span><span class="sxs-lookup"><span data-stu-id="959c3-202">CDN performs decompression</span></span> |
| <span data-ttu-id="959c3-203">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="959c3-203">Uncompressed</span></span> |<span data-ttu-id="959c3-204">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="959c3-204">Uncompressed</span></span> |<span data-ttu-id="959c3-205">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="959c3-205">Uncompressed</span></span> | |
| <span data-ttu-id="959c3-206">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="959c3-206">Uncompressed</span></span> |<span data-ttu-id="959c3-207">Önbelleğe alınmamış</span><span class="sxs-lookup"><span data-stu-id="959c3-207">Not cached</span></span> |<span data-ttu-id="959c3-208">Sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="959c3-208">Uncompressed</span></span> | |

## <a name="media-services-cdn-compression"></a><span data-ttu-id="959c3-209">CDN sıkıştırma medya Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="959c3-209">Media Services CDN Compression</span></span>
<span data-ttu-id="959c3-210">Medya Hizmetleri CDN akış uç noktalarını etkin sıkıştırma şu içerik türlerini hello için varsayılan olarak etkindir: uygulama/vnd.ms-sstr + xml, application/dash+xml,application/vnd.apple.mpegurl, uygulama/f4m + xml.</span><span class="sxs-lookup"><span data-stu-id="959c3-210">For Media Services CDN enabled streaming endpoints, compression is enabled by default for hello following content types: application/vnd.ms-sstr+xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m+xml.</span></span> <span data-ttu-id="959c3-211">Hello sıkıştırma bırakmak olamaz hello Azure portal kullanarak türleri belirtiliyor.</span><span class="sxs-lookup"><span data-stu-id="959c3-211">You cannot enable/disable compression for hello mentioned types using hello Azure portal.</span></span>  

## <a name="see-also"></a><span data-ttu-id="959c3-212">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="959c3-212">See also</span></span>
* [<span data-ttu-id="959c3-213">CDN dosya sıkıştırma sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="959c3-213">Troubleshooting CDN file compression</span></span>](cdn-troubleshoot-compression.md)    

