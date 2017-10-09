---
title: "aaaGetting Azure CDN ile çalışmaya | Microsoft Docs"
description: "Bu konu, nasıl tooenable hello Azure içerik teslim ağı (CDN) gösterir. Merhaba öğreticide bir yeni CDN profili ve uç noktası hello oluşturma açıklanmaktadır."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 4ca51224-5423-419b-98cf-89860ef516d2
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0ce9802bfd7b60e70a9a62330f5593fc17ea07d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-cdn"></a><span data-ttu-id="0732a-104">Azure CDN kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="0732a-104">Getting started with Azure CDN</span></span>
<span data-ttu-id="0732a-105">Bu konu başlığında, yeni bir CDN profili ve uç noktası oluşturarak Azure CDN'yi etkinleştirme işlemi boyunca size yol gösterilecektir.</span><span class="sxs-lookup"><span data-stu-id="0732a-105">This topic walks through enabling Azure CDN by creating a new CDN profile and endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0732a-106">Bir giriş toohow CDN çalışır, yanı sıra özelliklerinin bir listesi, hello bkz [CDN'ye genel bakış](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0732a-106">For an introduction toohow CDN works, as well as a list of features, see hello [CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="0732a-107">Yeni bir CDN profili oluşturma</span><span class="sxs-lookup"><span data-stu-id="0732a-107">Create a new CDN profile</span></span>
<span data-ttu-id="0732a-108">CDN profili, CDN uç noktaları koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="0732a-108">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="0732a-109">Her bir profil, bir veya daha fazla CDN uç noktası içerir.</span><span class="sxs-lookup"><span data-stu-id="0732a-109">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="0732a-110">Birden çok profilleri tooorganize toouse isteyebilir CDN uç noktalarınızı internet etki alanı, web uygulaması veya başka bir ölçüt.</span><span class="sxs-lookup"><span data-stu-id="0732a-110">You may wish toouse multiple profiles tooorganize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!NOTE]
> <span data-ttu-id="0732a-111">Varsayılan olarak, tek bir Azure aboneliği sınırlı tooeight CDN profilleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="0732a-111">By default, a single Azure subscription is limited tooeight CDN profiles.</span></span> <span data-ttu-id="0732a-112">Her CDN profili, sınırlı tooten CDN uç noktası değildir.</span><span class="sxs-lookup"><span data-stu-id="0732a-112">Each CDN profile is limited tooten CDN endpoints.</span></span>
> 
> <span data-ttu-id="0732a-113">CDN fiyatlandırması hello CDN profili düzeyinde uygulanır.</span><span class="sxs-lookup"><span data-stu-id="0732a-113">CDN pricing is applied at hello CDN profile level.</span></span> <span data-ttu-id="0732a-114">Fiyatlandırma katmanlarına Azure CDN bir karışımını toouse istiyorsanız, birden çok CDN profili kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0732a-114">If you wish toouse a mix of Azure CDN pricing tiers, you will need multiple CDN profiles.</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="0732a-115">Yeni bir CDN uç noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="0732a-115">Create a new CDN endpoint</span></span>
<span data-ttu-id="0732a-116">**toocreate yeni bir CDN uç noktası**</span><span class="sxs-lookup"><span data-stu-id="0732a-116">**toocreate a new CDN endpoint**</span></span>

1. <span data-ttu-id="0732a-117">Merhaba, [Azure Portal](https://portal.azure.com), tooyour CDN profili gidin.</span><span class="sxs-lookup"><span data-stu-id="0732a-117">In hello [Azure Portal](https://portal.azure.com), navigate tooyour CDN profile.</span></span>  <span data-ttu-id="0732a-118">Bu toohello Pano hello önceki adımda sabitlemiş olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0732a-118">You may have pinned it toohello dashboard in hello previous step.</span></span>  <span data-ttu-id="0732a-119">Bunu tıklayarak bulabilirsiniz değil, varsa **Gözat**, ardından **CDN profili**, ve hello profili tıklatarak tooadd uç noktanızı planladığınız.</span><span class="sxs-lookup"><span data-stu-id="0732a-119">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on hello profile you plan tooadd your endpoint to.</span></span>
   
    <span data-ttu-id="0732a-120">Merhaba CDN profili dikey penceresi görünür.</span><span class="sxs-lookup"><span data-stu-id="0732a-120">hello CDN profile blade appears.</span></span>
   
    ![CDN profili][cdn-profile-settings]
2. <span data-ttu-id="0732a-122">Merhaba tıklatın **uç nokta Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0732a-122">Click hello **Add Endpoint** button.</span></span>
   
    ![Uç nokta ekle düğmesi][cdn-new-endpoint-button]
   
    <span data-ttu-id="0732a-124">Merhaba **bir uç nokta ekleyin** dikey penceresi görünür.</span><span class="sxs-lookup"><span data-stu-id="0732a-124">hello **Add an endpoint** blade appears.</span></span>
   
    ![Uç nokta ekleme dikey penceresi][cdn-add-endpoint]
3. <span data-ttu-id="0732a-126">Bu CDN uç noktası için bir **Ad** girin.</span><span class="sxs-lookup"><span data-stu-id="0732a-126">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="0732a-127">Bu ad kullanılan tooaccess hello etki alanındaki önbelleğe alınmış kaynaklarınıza olacaktır `<endpointname>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="0732a-127">This name will be used tooaccess your cached resources at hello domain `<endpointname>.azureedge.net`.</span></span>
4. <span data-ttu-id="0732a-128">Merhaba, **kaynak türü** açılan listesinde, başlangıç noktası türünüzü seçin.</span><span class="sxs-lookup"><span data-stu-id="0732a-128">In hello **Origin type** dropdown, select your origin type.</span></span>  <span data-ttu-id="0732a-129">Azure Storage hesabı için **Depolama**, Azure Bulut Hizmeti için **Bulut hizmeti**, Azure Web Uygulaması için **Web Uygulaması** veya genel olarak erişilebilen herhangi bir web sunucusu kaynağı (Azure'da veya başka bir konumda barındırılan) için **Özel kaynak** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="0732a-129">Select **Storage** for an Azure Storage account, **Cloud service** for an Azure Cloud Service, **Web App** for an Azure Web App, or **Custom origin** for any other publicly accessible web server origin (hosted in Azure or elsewhere).</span></span>
   
    ![CDN kaynak türü](./media/cdn-create-new-endpoint/cdn-origin-type.png)
5. <span data-ttu-id="0732a-131">Merhaba, **kaynak ana bilgisayar adı** açılan listesinde, kaynak etki alanınızı yazın veya seçin.</span><span class="sxs-lookup"><span data-stu-id="0732a-131">In hello **Origin hostname** dropdown, select or type your origin domain.</span></span>  <span data-ttu-id="0732a-132">Merhaba açılır 4. adımda belirttiğiniz hello türündeki tüm kullanılabilir kaynakları listeler.</span><span class="sxs-lookup"><span data-stu-id="0732a-132">hello dropdown will list all available origins of hello type you specified in step 4.</span></span>  <span data-ttu-id="0732a-133">Seçtiyseniz *özel kaynak* olarak, **kaynak türü**, özel kaynağınıza hello etki alanında yazmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0732a-133">If you selected *Custom origin* as your **Origin type**, you will type in hello domain of your custom origin.</span></span>
6. <span data-ttu-id="0732a-134">Merhaba, **kaynak yolu** metin kutusunda, istediğiniz toocache ya da bırak boş tooallow önbellek 5. adımda belirttiğiniz hello etki alanındaki herhangi bir kaynağa hello yolu toohello kaynakların girin.</span><span class="sxs-lookup"><span data-stu-id="0732a-134">In hello **Origin path** text box, enter hello path toohello resources you want toocache, or leave blank tooallow cache any resource at hello domain you specified in step 5.</span></span>
7. <span data-ttu-id="0732a-135">Merhaba, **kaynak ana bilgisayar üstbilgisi**istediğiniz her istek ile CDN toosend hello hello ana bilgisayar üstbilgisi girin veya hello varsayılan adı bırakın.</span><span class="sxs-lookup"><span data-stu-id="0732a-135">In hello **Origin host header**, enter hello host header you want hello CDN toosend with each request, or leave hello default.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="0732a-136">Bazı Azure Storage ve Web uygulamaları gibi kaynak türleri hello ana bilgisayar üstbilgisi toomatch hello kaynak etki alanı hello gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0732a-136">Some types of origins, such as Azure Storage and Web Apps, require hello host header toomatch hello domain of hello origin.</span></span> <span data-ttu-id="0732a-137">Etki alanından farklı bir ana bilgisayar üstbilgisi gerektiren bir kaynağa sahip değilseniz, hello varsayılan değeri bırakmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0732a-137">Unless you have an origin that requires a host header different from its domain, you should leave hello default value.</span></span>
   > 
   > 
8. <span data-ttu-id="0732a-138">İçin **Protokolü** ve **kaynak bağlantı noktası**, hello protokolleri belirtin ve kullanılan tooaccess hello kaynak üzerindeki bağlantı noktaları.</span><span class="sxs-lookup"><span data-stu-id="0732a-138">For **Protocol** and **Origin port**, specify hello protocols and ports used tooaccess your resources at hello origin.</span></span>  <span data-ttu-id="0732a-139">En az bir protokol (HTTP veya HTTPS) seçilmelidir.</span><span class="sxs-lookup"><span data-stu-id="0732a-139">At least one protocol (HTTP or HTTPS) must be selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0732a-140">Merhaba **kaynak bağlantı noktası** tooretrieve bilgileri hello kaynaktan hangi bağlantı noktası hello uç noktası kullanır, yalnızca etkiler.</span><span class="sxs-lookup"><span data-stu-id="0732a-140">hello **Origin port** only affects what port hello endpoint uses tooretrieve information from hello origin.</span></span>  <span data-ttu-id="0732a-141">Merhaba uç noktanın kendisi yalnızca kullanılabilir tooend istemcilerin hello varsayılan HTTP ve HTTPS bağlantı noktalarındaki (80 ve 443) hello bakılmaksızın olacağını **kaynak bağlantı noktası**.</span><span class="sxs-lookup"><span data-stu-id="0732a-141">hello endpoint itself will only be available tooend clients on hello default HTTP and HTTPS ports (80 and 443), regardless of hello **Origin port**.</span></span>  
   > 
   > <span data-ttu-id="0732a-142">**Akamai'den Azure CDN** uç noktaları hello tam TCP bağlantı noktası aralığı kaynakları için izin vermez.</span><span class="sxs-lookup"><span data-stu-id="0732a-142">**Azure CDN from Akamai** endpoints do not allow hello full TCP port range for origins.</span></span>  <span data-ttu-id="0732a-143">İzin verilmeyen kaynak bağlantı noktalarının listesi için bkz. [Akamai'den Azure CDN İzin Verilen Kaynak Bağlantı Noktaları](https://msdn.microsoft.com/library/mt757337.aspx).</span><span class="sxs-lookup"><span data-stu-id="0732a-143">For a list of origin ports that are not allowed, see [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx).</span></span>  
   > 
   > <span data-ttu-id="0732a-144">CDN erişme HTTPS kullanarak içerik kısıtlamaları aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="0732a-144">Accessing CDN content using HTTPS has hello following constraints:</span></span>
   > 
   > * <span data-ttu-id="0732a-145">Merhaba CDN tarafından sağlanan hello SSL sertifikası kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0732a-145">You must use hello SSL certificate provided by hello CDN.</span></span> <span data-ttu-id="0732a-146">Üçüncü taraf sertifikalar desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="0732a-146">Third party certificates are not supported.</span></span>
   > * <span data-ttu-id="0732a-147">Merhaba CDN tarafından sağlanan etki alanı kullanmanız gerekir (`<endpointname>.azureedge.net`) tooaccess HTTPS içeriği.</span><span class="sxs-lookup"><span data-stu-id="0732a-147">You must use hello CDN-provided domain (`<endpointname>.azureedge.net`) tooaccess HTTPS content.</span></span> <span data-ttu-id="0732a-148">HTTPS desteği Hello CDN şu anda özel sertifikaları desteklemediğinden özel etki alanı adları (CNAME'ler) için kullanılabilir değildir.</span><span class="sxs-lookup"><span data-stu-id="0732a-148">HTTPS support is not available for custom domain names (CNAMEs) since hello CDN does not support custom certificates at this time.</span></span>
   > 
   > 
9. <span data-ttu-id="0732a-149">Merhaba tıklatın **Ekle** düğmesini toocreate hello yeni uç noktası.</span><span class="sxs-lookup"><span data-stu-id="0732a-149">Click hello **Add** button toocreate hello new endpoint.</span></span>
10. <span data-ttu-id="0732a-150">Merhaba uç nokta oluşturulduktan sonra hello profil için uç noktalar listesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="0732a-150">Once hello endpoint is created, it appears in a list of endpoints for hello profile.</span></span> <span data-ttu-id="0732a-151">Merhaba URL toouse tooaccess hello kaynak etki alanının yanı sıra, içeriği önbelleğe Hello liste görünümü gösterir.</span><span class="sxs-lookup"><span data-stu-id="0732a-151">hello list view shows hello URL toouse tooaccess cached content, as well as hello origin domain.</span></span>
    
    ![CDN uç noktası][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > <span data-ttu-id="0732a-153">Merhaba kayıt toopropagate hello CDN aracılığıyla süredir yararlanırken hello uç nokta hemen kullanılabilir olmaz.</span><span class="sxs-lookup"><span data-stu-id="0732a-153">hello endpoint will not immediately be available for use, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="0732a-154"><b>Akamai'den Azure CDN</b> profilleri için yayma işlemi genellikle bir dakika içinde tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="0732a-154">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="0732a-155"><b>Verizon'dan Azure CDN</b> profilleri için yayma işlemi genellikle 90 dakika içinde tamamlanır ancak bazı durumlarda daha uzun sürebilir.</span><span class="sxs-lookup"><span data-stu-id="0732a-155">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
    > 
    > <span data-ttu-id="0732a-156">Toouse hello CDN etki alanı adı Hello uç nokta yapılandırması toohello Pop'lere yayılmadan önce deneyen kullanıcılar HTTP 404 yanıt kodlarını alır.</span><span class="sxs-lookup"><span data-stu-id="0732a-156">Users who try toouse hello CDN domain name before hello endpoint configuration has propagated toohello POPs will receive HTTP 404 response codes.</span></span>  <span data-ttu-id="0732a-157">Uç noktanızı oluşturmanızın ardından birkaç saat geçmesine karşın 404 yanıtlarını almaya devam ediyorsanız lütfen bkz. [404 durumu döndüren CDN uç noktası sorunlarını giderme](cdn-troubleshoot-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="0732a-157">If it's been several hours since you created your endpoint and you're still receiving 404 responses, please see [Troubleshooting CDN endpoints returning 404 statuses](cdn-troubleshoot-endpoint.md).</span></span>
    > 
    > 

## <a name="see-also"></a><span data-ttu-id="0732a-158">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="0732a-158">See Also</span></span>
* [<span data-ttu-id="0732a-159">İsteklerin önbelleğe alınma davranışını sorgu dizeleriyle denetleme</span><span class="sxs-lookup"><span data-stu-id="0732a-159">Controlling caching behavior of requests with query strings</span></span>](cdn-query-string.md)
* [<span data-ttu-id="0732a-160">Nasıl tooMap CDN içerik tooa özel etki alanı</span><span class="sxs-lookup"><span data-stu-id="0732a-160">How tooMap CDN Content tooa Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="0732a-161">Azure CDN uç noktasında varlıkları önceden yükleme</span><span class="sxs-lookup"><span data-stu-id="0732a-161">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="0732a-162">Azure CDN Uç Noktasını Temizleme</span><span class="sxs-lookup"><span data-stu-id="0732a-162">Purge an Azure CDN Endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="0732a-163">404 durumları döndüren CDN uç noktası sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="0732a-163">Troubleshooting CDN endpoints returning 404 statuses</span></span>](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: ./media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-create-new-endpoint/cdn-endpoint-success.png
