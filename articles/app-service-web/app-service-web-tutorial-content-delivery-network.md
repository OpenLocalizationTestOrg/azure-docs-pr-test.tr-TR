---
title: aaaAdd CDN tooan Azure App Service | Microsoft Docs
description: "Bir içerik teslim ağı (CDN) tooan Azure uygulama hizmeti toocache ekleyin ve statik dosyalarınızı sunucularından Merhaba Dünya Kapat tooyour müşterilere teslim."
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 88b7fd884517279064472b804a6d1dc2921cbd24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-content-delivery-network-cdn-tooan-azure-app-service"></a><span data-ttu-id="d0308-103">İçerik teslim ağı (CDN) tooan Azure uygulama hizmeti Ekle</span><span class="sxs-lookup"><span data-stu-id="d0308-103">Add a Content Delivery Network (CDN) tooan Azure App Service</span></span>

<span data-ttu-id="d0308-104">[Azure içerik teslim ağı (CDN)](../cdn/cdn-overview.md) içerik toousers teslim stratejik olarak yerleştirilmiş konumlardaki tooprovide en yüksek verimlilik statik web içeriği önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="d0308-104">[Azure Content Delivery Network (CDN)](../cdn/cdn-overview.md) caches static web content at strategically placed locations tooprovide maximum throughput for delivering content toousers.</span></span> <span data-ttu-id="d0308-105">Hello CDN web uygulamanız üzerindeki sunucu yükü de azalır.</span><span class="sxs-lookup"><span data-stu-id="d0308-105">hello CDN also decreases server load on your web app.</span></span> <span data-ttu-id="d0308-106">Bu öğreticide gösterilmiştir nasıl tooadd Azure CDN tooa [Azure App Service'in web uygulamasında](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d0308-106">This tutorial shows how tooadd Azure CDN tooa [web app in Azure App Service](app-service-web-overview.md).</span></span> 

<span data-ttu-id="d0308-107">Merhaba giriş sayfası ile çalışan hello örnek statik HTML sitesinin şöyledir:</span><span class="sxs-lookup"><span data-stu-id="d0308-107">Here's hello home page of hello sample static HTML site that you'll work with:</span></span>

![Örnek uygulama ana sayfası](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

<span data-ttu-id="d0308-109">Öğrenecekleriniz:</span><span class="sxs-lookup"><span data-stu-id="d0308-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d0308-110">CDN uç noktası oluşturma.</span><span class="sxs-lookup"><span data-stu-id="d0308-110">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="d0308-111">Önbelleğe alınan varlıkları yenileme.</span><span class="sxs-lookup"><span data-stu-id="d0308-111">Refresh cached assets.</span></span>
> * <span data-ttu-id="d0308-112">Önbelleğe alınmış toocontrol sürümleri kullanım sorgu dizeleri.</span><span class="sxs-lookup"><span data-stu-id="d0308-112">Use query strings toocontrol cached versions.</span></span>
> * <span data-ttu-id="d0308-113">Özel bir etki alanı hello CDN uç noktası için kullanın.</span><span class="sxs-lookup"><span data-stu-id="d0308-113">Use a custom domain for hello CDN endpoint.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0308-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d0308-114">Prerequisites</span></span>

<span data-ttu-id="d0308-115">toocomplete Bu öğretici:</span><span class="sxs-lookup"><span data-stu-id="d0308-115">toocomplete this tutorial:</span></span>

- [<span data-ttu-id="d0308-116">Git'i yükleyin</span><span class="sxs-lookup"><span data-stu-id="d0308-116">Install Git</span></span>](https://git-scm.com/)
- [<span data-ttu-id="d0308-117">Azure CLI 2.0 yükleyin</span><span class="sxs-lookup"><span data-stu-id="d0308-117">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-web-app"></a><span data-ttu-id="d0308-118">Merhaba web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0308-118">Create hello web app</span></span>

<span data-ttu-id="d0308-119">ile izleme hello karşılaşmayacağınızı toocreate hello web uygulaması [statik HTML Hızlı Başlangıç](app-service-web-get-started-html.md) hello aracılığıyla **Gözat toohello uygulama** adım.</span><span class="sxs-lookup"><span data-stu-id="d0308-119">toocreate hello web app that you'll work with, follow hello [static HTML quickstart](app-service-web-get-started-html.md) through hello **Browse toohello app** step.</span></span>

### <a name="have-a-custom-domain-ready"></a><span data-ttu-id="d0308-120">Özel bir etki alanına sahip olma</span><span class="sxs-lookup"><span data-stu-id="d0308-120">Have a custom domain ready</span></span>

<span data-ttu-id="d0308-121">toocomplete hello özel etki alanı adım Bu öğreticinin tooown özel bir etki alanı gerekir ve etki alanı sağlayıcınızın (örneğin, GoDaddy) erişim tooyour DNS kayıt defteri sahip.</span><span class="sxs-lookup"><span data-stu-id="d0308-121">toocomplete hello custom domain step of this tutorial, you need tooown a custom domain and have access tooyour DNS registry for your domain provider (such as GoDaddy).</span></span> <span data-ttu-id="d0308-122">Örneğin, için DNS girişleri tooadd `contoso.com` ve `www.contoso.com`, erişim tooconfigure hello DNS ayarlarını hello olmalıdır `contoso.com` kök etki alanı.</span><span class="sxs-lookup"><span data-stu-id="d0308-122">For example, tooadd DNS entries for `contoso.com` and `www.contoso.com`, you must have access tooconfigure hello DNS settings for hello `contoso.com` root domain.</span></span>

<span data-ttu-id="d0308-123">Bir etki alanı adı zaten yoksa, hello göz önünde bulundurun [uygulama hizmeti etki alanı öğretici](custom-dns-web-site-buydomains-web-app.md) kullanarak bir etki alanı toopurchase hello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="d0308-123">If you don't already have a domain name, consider following hello [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) toopurchase a domain using hello Azure portal.</span></span> 

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="d0308-124">Toohello Azure portalında oturum açın</span><span class="sxs-lookup"><span data-stu-id="d0308-124">Log in toohello Azure portal</span></span>

<span data-ttu-id="d0308-125">Bir tarayıcı açın ve toohello gidin [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d0308-125">Open a browser and navigate toohello [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-a-cdn-profile-and-endpoint"></a><span data-ttu-id="d0308-126">CDN profili ve uç noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0308-126">Create a CDN profile and endpoint</span></span>

<span data-ttu-id="d0308-127">Sol gezinti hello seçin **uygulama hizmetleri**ve ardından hello oluşturulan hello uygulama [statik HTML Hızlı Başlangıç](app-service-web-get-started-html.md).</span><span class="sxs-lookup"><span data-stu-id="d0308-127">In hello left navigation, select **App Services**, and then select hello app that you created in hello [static HTML quickstart](app-service-web-get-started-html.md).</span></span>

![App Service uygulaması hello Portalı'nda seçin](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

<span data-ttu-id="d0308-129">Merhaba, **uygulama hizmeti** sayfasında hello **ayarları** bölümünde, select **Ağ > yapılandırma Azure CDN uygulamanız için**.</span><span class="sxs-lookup"><span data-stu-id="d0308-129">In hello **App Service** page, in hello **Settings** section, select **Networking > Configure Azure CDN for your app**.</span></span>

![CDN hello Portalı'nda seçin](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

<span data-ttu-id="d0308-131">Merhaba, **Azure içerik teslim ağı** sayfasında, hello sağlayın **yeni uç nokta** hello tabloda belirtildiği gibi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d0308-131">In hello **Azure Content Delivery Network** page, provide hello **New endpoint** settings as specified in hello table.</span></span>

![Profil ve uç hello Portalı'nda oluşturma](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| <span data-ttu-id="d0308-133">Ayar</span><span class="sxs-lookup"><span data-stu-id="d0308-133">Setting</span></span> | <span data-ttu-id="d0308-134">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="d0308-134">Suggested value</span></span> | <span data-ttu-id="d0308-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d0308-135">Description</span></span> |
| ------- | --------------- | ----------- |
| <span data-ttu-id="d0308-136">**CDN profili**</span><span class="sxs-lookup"><span data-stu-id="d0308-136">**CDN profile**</span></span> | <span data-ttu-id="d0308-137">myCDNProfile</span><span class="sxs-lookup"><span data-stu-id="d0308-137">myCDNProfile</span></span> | <span data-ttu-id="d0308-138">Seçin **Yeni Oluştur** toocreate CDN profili.</span><span class="sxs-lookup"><span data-stu-id="d0308-138">Select **Create new** toocreate a CDN profile.</span></span> <span data-ttu-id="d0308-139">CDN profili, CDN uç hello ile koleksiyonudur aynı fiyatlandırma katmanı.</span><span class="sxs-lookup"><span data-stu-id="d0308-139">A CDN profile is a collection of CDN endpoints with hello same pricing tier.</span></span> |
| <span data-ttu-id="d0308-140">**Fiyatlandırma katmanı**</span><span class="sxs-lookup"><span data-stu-id="d0308-140">**Pricing tier**</span></span> | <span data-ttu-id="d0308-141">Standart Akamai</span><span class="sxs-lookup"><span data-stu-id="d0308-141">Standard Akamai</span></span> | <span data-ttu-id="d0308-142">Merhaba [fiyatlandırma katmanı](../cdn/cdn-overview.md#azure-cdn-features) hello sağlayıcısı ve kullanılabilir özellikler belirtir.</span><span class="sxs-lookup"><span data-stu-id="d0308-142">hello [pricing tier](../cdn/cdn-overview.md#azure-cdn-features) specifies hello provider and available features.</span></span> <span data-ttu-id="d0308-143">Bu öğreticide, standart Akamai kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="d0308-143">In this tutorial, we are using Standard Akamai.</span></span> |
| <span data-ttu-id="d0308-144">**CDN uç noktası adı**</span><span class="sxs-lookup"><span data-stu-id="d0308-144">**CDN endpoint name**</span></span> | <span data-ttu-id="d0308-145">Merhaba azureedge.net etki alanında benzersiz olan herhangi bir ad</span><span class="sxs-lookup"><span data-stu-id="d0308-145">Any name that is unique in hello azureedge.net domain</span></span> | <span data-ttu-id="d0308-146">Merhaba etki alanındaki önbelleğe alınmış kaynaklarınıza erişen  *\<endpointname >. azureedge.net*.</span><span class="sxs-lookup"><span data-stu-id="d0308-146">You access your cached resources at hello domain *\<endpointname>.azureedge.net*.</span></span>

<span data-ttu-id="d0308-147">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="d0308-147">Select **Create**.</span></span>

<span data-ttu-id="d0308-148">Azure hello profil ve uç noktası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d0308-148">Azure creates hello profile and endpoint.</span></span> <span data-ttu-id="d0308-149">Merhaba yeni uç nokta görünür hello **uç noktaları** listesini hello aynı sayfa ve onu sağlandığında hello durumudur **çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="d0308-149">hello new endpoint appears in hello **Endpoints** list on hello same page, and when it's provisioned hello status is **Running**.</span></span>

![Listede yeni uç nokta](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-hello-cdn-endpoint"></a><span data-ttu-id="d0308-151">Test hello CDN uç noktası</span><span class="sxs-lookup"><span data-stu-id="d0308-151">Test hello CDN endpoint</span></span>

<span data-ttu-id="d0308-152">Verizon fiyatlandırma katmanını seçtiyseniz, uç noktayı yayma işlemi genellikle yaklaşık 90 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="d0308-152">If you selected Verizon pricing tier, it typically takes about 90 minutes for endpoint propagation.</span></span> <span data-ttu-id="d0308-153">Akamai için, yayma işlemi birkaç dakika sürer</span><span class="sxs-lookup"><span data-stu-id="d0308-153">For Akamai, it takes a couple minutes for propagation</span></span>

<span data-ttu-id="d0308-154">Merhaba örnek uygulaması olan bir `index.html` dosya ve *css*, *img*, ve *js* diğer statik varlıklarını içeren klasörleri.</span><span class="sxs-lookup"><span data-stu-id="d0308-154">hello sample app has an `index.html` file and *css*, *img*, and *js* folders that contain other static assets.</span></span> <span data-ttu-id="d0308-155">Tüm bu dosyaların yolları içerik Hello hello aynı hello CDN uç noktada.</span><span class="sxs-lookup"><span data-stu-id="d0308-155">hello content paths for all of these files are hello same at hello CDN endpoint.</span></span> <span data-ttu-id="d0308-156">Örneğin, aşağıdaki URL'lere hello her ikisi de hello erişim *bootstrap.css* hello dosyasında *css* klasörü:</span><span class="sxs-lookup"><span data-stu-id="d0308-156">For example, both of hello following URLs access hello *bootstrap.css* file in hello *css* folder:</span></span>

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

<span data-ttu-id="d0308-157">URL aşağıdaki tarayıcı toohello gidin:</span><span class="sxs-lookup"><span data-stu-id="d0308-157">Navigate a browser toohello following URL:</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![CDN'den sunulan örnek uygulama ana sayfası](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 <span data-ttu-id="d0308-159">Daha önce bir Azure web uygulamasında çalışan aynı sayfa hello bakın.</span><span class="sxs-lookup"><span data-stu-id="d0308-159">You see hello same page that you ran earlier in an Azure web app.</span></span> <span data-ttu-id="d0308-160">Azure CDN hello kaynak web uygulamanızın varlıklar alınan ve bunları hello CDN uç noktasından hizmet</span><span class="sxs-lookup"><span data-stu-id="d0308-160">Azure CDN has retrieved hello origin web app's assets and is serving them from hello CDN endpoint</span></span>

<span data-ttu-id="d0308-161">tooensure bu sayfayı hello CDN, yenileme hello sayfası önbelleğe alınır.</span><span class="sxs-lookup"><span data-stu-id="d0308-161">tooensure that this page is cached in hello CDN, refresh hello page.</span></span> <span data-ttu-id="d0308-162">Merhaba aynı varlık için bazen gerekli hello CDN toocache hello için istenen içerik iki ister.</span><span class="sxs-lookup"><span data-stu-id="d0308-162">Two requests for hello same asset are sometimes required for hello CDN toocache hello requested content.</span></span>

<span data-ttu-id="d0308-163">Azure CDN profilleri ve uç noktaları oluşturma hakkında daha fazla bilgi için bkz. [Azure CDN kullanmaya başlama](../cdn/cdn-create-new-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="d0308-163">For more information about creating Azure CDN profiles and endpoints, see [Getting started with Azure CDN](../cdn/cdn-create-new-endpoint.md).</span></span>

## <a name="purge-hello-cdn"></a><span data-ttu-id="d0308-164">Merhaba CDN Temizle</span><span class="sxs-lookup"><span data-stu-id="d0308-164">Purge hello CDN</span></span>

<span data-ttu-id="d0308-165">Merhaba CDN kaynaklarını hello yaşam süresi (TTL) yapılandırmasını temel alarak hello kaynak web uygulamasından düzenli aralıklarla yeniler.</span><span class="sxs-lookup"><span data-stu-id="d0308-165">hello CDN periodically refreshes its resources from hello origin web app based on hello time-to-live (TTL) configuration.</span></span> <span data-ttu-id="d0308-166">Merhaba varsayılan TTL yedi gündür.</span><span class="sxs-lookup"><span data-stu-id="d0308-166">hello default TTL is seven days.</span></span>

<span data-ttu-id="d0308-167">Bazen güncelleştirilmiş içerik toohello web uygulaması dağıttığınızda hello TTL sona erme--önce toorefresh hello CDN Örneğin, gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="d0308-167">At times you might need toorefresh hello CDN before hello TTL expiration -- for example, when you deploy updated content toohello web app.</span></span> <span data-ttu-id="d0308-168">bir yenileme tootrigger hello CDN kaynakları el ile temizleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0308-168">tootrigger a refresh, you can manually purge hello CDN resources.</span></span> 

<span data-ttu-id="d0308-169">Merhaba öğreticinin bu bölümünde bir değişiklik toohello web uygulaması dağıtma ve hello CDN tootrigger hello CDN toorefresh önbelleğini Temizle.</span><span class="sxs-lookup"><span data-stu-id="d0308-169">In this section of hello tutorial, you deploy a change toohello web app and purge hello CDN tootrigger hello CDN toorefresh its cache.</span></span>

### <a name="deploy-a-change-toohello-web-app"></a><span data-ttu-id="d0308-170">Bir değişiklik toohello web uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="d0308-170">Deploy a change toohello web app</span></span>

<span data-ttu-id="d0308-171">Açık hello `index.html` dosya ve ekleme "-V2" hello aşağıdaki örnekte gösterildiği gibi toohello H1 başlığını:</span><span class="sxs-lookup"><span data-stu-id="d0308-171">Open hello `index.html` file and add "- V2" toohello H1 heading, as shown in hello following example:</span></span> 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

<span data-ttu-id="d0308-172">Değişikliklerinizi kaydetmek ve toohello web uygulaması dağıtma.</span><span class="sxs-lookup"><span data-stu-id="d0308-172">Commit your change and deploy it toohello web app.</span></span>

```bash
git commit -am "version 2"
git push azure master
```

<span data-ttu-id="d0308-173">Dağıtım tamamlandıktan sonra Gözat toohello web uygulaması URL'si ve değiştirme hello bakın.</span><span class="sxs-lookup"><span data-stu-id="d0308-173">Once deployment has completed, browse toohello web app URL and you see hello change.</span></span>

```
http://<appname>.azurewebsites.net/index.html
```

![Web uygulamasındaki başlıkta V2](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

<span data-ttu-id="d0308-175">Toohello CDN uç noktası URL'si hello giriş sayfası ve hello önbelleğe alınmış hello CDN sürümünde henüz dolmadığından olduğundan değişiklik hello görmüyorum göz atın.</span><span class="sxs-lookup"><span data-stu-id="d0308-175">Browse toohello CDN endpoint URL for hello home page and you don't see hello change because hello cached version in hello CDN hasn't expired yet.</span></span> 

```
http://<endpointname>.azureedge.net/index.html
```

![CDN'deki başlıkta V2 yok](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-hello-cdn-in-hello-portal"></a><span data-ttu-id="d0308-177">Merhaba CDN hello portalında Temizle</span><span class="sxs-lookup"><span data-stu-id="d0308-177">Purge hello CDN in hello portal</span></span>

<span data-ttu-id="d0308-178">tootrigger CDN tooupdate önbelleğe alınan sürüm Merhaba, hello CDN Temizle.</span><span class="sxs-lookup"><span data-stu-id="d0308-178">tootrigger hello CDN tooupdate its cached version, purge hello CDN.</span></span>

<span data-ttu-id="d0308-179">Merhaba portal sol gezinti bölmesinde seçin **kaynak grupları**ve ardından web uygulamanız için (contoso.com) oluşturulan hello kaynak grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="d0308-179">In hello portal left navigation, select **Resource groups**, and then select hello resource group that you created for your web app (myResourceGroup).</span></span>

![Kaynak grubu seçin](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

<span data-ttu-id="d0308-181">CDN uç noktanız kaynakların Hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="d0308-181">In hello list of resources, select your CDN endpoint.</span></span>

![Uç nokta seçin](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

<span data-ttu-id="d0308-183">Merhaba hello üstündeki **Endpoint** sayfasında, **Temizleme**.</span><span class="sxs-lookup"><span data-stu-id="d0308-183">At hello top of hello **Endpoint** page, click **Purge**.</span></span>

![Temizleme seçin](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

<span data-ttu-id="d0308-185">Merhaba içerik yolları toopurge istediğiniz girin.</span><span class="sxs-lookup"><span data-stu-id="d0308-185">Enter hello content paths you wish toopurge.</span></span> <span data-ttu-id="d0308-186">Bir tam dosya yolunu toopurge tek bir dosyayı veya bir yol kesimi toopurge geçirmek ve bir klasördeki tüm içeriği yenileyin.</span><span class="sxs-lookup"><span data-stu-id="d0308-186">You can pass a complete file path toopurge an individual file, or a path segment toopurge and refresh all content in a folder.</span></span> <span data-ttu-id="d0308-187">Değiştirdiğiniz beri `index.html`, hello yollarından biri olan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d0308-187">Since you changed `index.html`, make sure that is one of hello paths.</span></span>

<span data-ttu-id="d0308-188">Merhaba sayfasının Hello altında seçin **Temizleme**.</span><span class="sxs-lookup"><span data-stu-id="d0308-188">At hello bottom of hello page, select **Purge**.</span></span>

![Sayfayı temizleyin](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-hello-cdn-is-updated"></a><span data-ttu-id="d0308-190">CDN güncelleştirilmiş bu hello doğrulayın</span><span class="sxs-lookup"><span data-stu-id="d0308-190">Verify that hello CDN is updated</span></span>

<span data-ttu-id="d0308-191">Merhaba temizleme isteği işleme, genellikle birkaç dakika tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="d0308-191">Wait until hello purge request finishes processing, typically a couple of minutes.</span></span> <span data-ttu-id="d0308-192">toosee hello geçerli durumu, select hello zil simgesine hello sayfanın üst kısmındaki hello.</span><span class="sxs-lookup"><span data-stu-id="d0308-192">toosee hello current status, select hello bell icon at hello top of hello page.</span></span> 

![Temizleme bildirimi](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

<span data-ttu-id="d0308-194">Toohello CDN uç noktası URL'si Gözat `index.html`, ve şimdi hello hello giriş sayfasında toohello başlık eklenen V2 bakın.</span><span class="sxs-lookup"><span data-stu-id="d0308-194">Browse toohello CDN endpoint URL for `index.html`, and now you see hello V2 that you added toohello title on hello home page.</span></span> <span data-ttu-id="d0308-195">Bu, hello CDN önbellek yenileninceye olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="d0308-195">This shows that hello CDN cache has been refreshed.</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![CDN'deki başlıkta V2](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

<span data-ttu-id="d0308-197">Daha fazla bilgi için bkz. [Azure CDN uç noktasını temizleme](../cdn/cdn-purge-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="d0308-197">For more information, see [Purge an Azure CDN endpoint](../cdn/cdn-purge-endpoint.md).</span></span> 

## <a name="use-query-strings-tooversion-content"></a><span data-ttu-id="d0308-198">Sorgu dizeleri tooversion içeriği kullanın</span><span class="sxs-lookup"><span data-stu-id="d0308-198">Use query strings tooversion content</span></span>

<span data-ttu-id="d0308-199">Hello Azure CDN önbelleğe alma davranışı seçeneklerini aşağıdaki hello sunar:</span><span class="sxs-lookup"><span data-stu-id="d0308-199">hello Azure CDN offers hello following caching behavior options:</span></span>

* <span data-ttu-id="d0308-200">Sorgu dizelerini yoksay</span><span class="sxs-lookup"><span data-stu-id="d0308-200">Ignore query strings</span></span>
* <span data-ttu-id="d0308-201">Sorgu dizeleri için önbelleğe almayı atla</span><span class="sxs-lookup"><span data-stu-id="d0308-201">Bypass caching for query strings</span></span>
* <span data-ttu-id="d0308-202">Her benzersiz URL'yi önbelleğe al</span><span class="sxs-lookup"><span data-stu-id="d0308-202">Cache every unique URL</span></span> 

<span data-ttu-id="d0308-203">ilk hello bunlardan yalnızca bir önbelleğe alınan sürümü hello URL'de hello sorgu dizesi bağımsız olarak bir varlık yok demektir hello varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="d0308-203">hello first of these is hello default, which means there is only one cached version of an asset regardless of hello query string in hello URL.</span></span> 

<span data-ttu-id="d0308-204">Hello öğreticinin bu bölümünde her benzersiz URL'yi önbelleğe alma davranışını toocache hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d0308-204">In this section of hello tutorial, you change hello caching behavior toocache every unique URL.</span></span>

### <a name="change-hello-cache-behavior"></a><span data-ttu-id="d0308-205">Merhaba önbellek davranışını değiştirme</span><span class="sxs-lookup"><span data-stu-id="d0308-205">Change hello cache behavior</span></span>

<span data-ttu-id="d0308-206">Hello Azure portal'ın **CDN uç noktası** sayfasında, **önbellek**.</span><span class="sxs-lookup"><span data-stu-id="d0308-206">In hello Azure portal **CDN Endpoint** page, select **Cache**.</span></span>

<span data-ttu-id="d0308-207">Seçin **her benzersiz URL'yi önbelleğe** hello gelen **sorgu dizesini önbelleğe alma davranışı** aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="d0308-207">Select **Cache every unique URL** from hello **Query string caching behavior** drop-down list.</span></span>

<span data-ttu-id="d0308-208">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="d0308-208">Select **Save**.</span></span>

![Sorgu dizesini önbelleğe alma davranışı seçin](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a><span data-ttu-id="d0308-210">Benzersiz URL'lerin ayrı olarak önbelleğe alındığını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="d0308-210">Verify that unique URLs are cached separately</span></span>

<span data-ttu-id="d0308-211">Bir tarayıcıda hello CDN uç noktada toohello giriş sayfasına gidin, ancak bir sorgu dizesi içerir:</span><span class="sxs-lookup"><span data-stu-id="d0308-211">In a browser, navigate toohello home page at hello CDN endpoint, but include a query string:</span></span> 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

<span data-ttu-id="d0308-212">Merhaba CDN "V2" Merhaba başlığına içeren hello geçerli uygulama, web içeriği döndürür.</span><span class="sxs-lookup"><span data-stu-id="d0308-212">hello CDN returns hello current web app content, which includes "V2" in hello heading.</span></span> 

<span data-ttu-id="d0308-213">tooensure bu sayfayı hello CDN, yenileme hello sayfası önbelleğe alınır.</span><span class="sxs-lookup"><span data-stu-id="d0308-213">tooensure that this page is cached in hello CDN, refresh hello page.</span></span> 

<span data-ttu-id="d0308-214">Açık `index.html` değiştirip "V2" çok "V3" ve hello değişiklik dağıtın.</span><span class="sxs-lookup"><span data-stu-id="d0308-214">Open `index.html` and change "V2" too"V3", and deploy hello change.</span></span> 

```bash
git commit -am "version 3"
git push azure master
```

<span data-ttu-id="d0308-215">Bir tarayıcıda toohello CDN uç noktası URL'si ile yeni bir sorgu dizesi gibi Git `q=2`.</span><span class="sxs-lookup"><span data-stu-id="d0308-215">In a browser, go toohello CDN endpoint URL with a new query string such as `q=2`.</span></span> <span data-ttu-id="d0308-216">Merhaba CDN hello geçerli alır `index.html` dosya ve "V3" görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d0308-216">hello CDN gets hello current `index.html` file and displays "V3".</span></span>  <span data-ttu-id="d0308-217">Ancak toohello CDN uç noktasıyla hello giderseniz `q=1` sorgu dizesi, "V2" konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="d0308-217">But if you navigate toohello CDN endpoint with hello `q=1` query string, you see "V2".</span></span>

```
http://<endpointname>.azureedge.net/index.html?q=2
```

![CDN'deki başlıkta V3, sorgu dizesi 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

![CDN'deki başlıkta V2, sorgu dizesi 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

<span data-ttu-id="d0308-220">Bu çıktı, her sorgu dizesi farklı şekilde ele gösterir:</span><span class="sxs-lookup"><span data-stu-id="d0308-220">This output shows that each query string is treated differently:</span></span>

* <span data-ttu-id="d0308-221">q = 1 kullanıldı önce şekilde ön belleğe alınmış içeriği (V2) döndürülür.</span><span class="sxs-lookup"><span data-stu-id="d0308-221">q=1 was used before, so cached contents are returned (V2).</span></span>
* <span data-ttu-id="d0308-222">q = 2'dir yeni, böylece hello en son web uygulama içeriği alınır ve (V3) döndürdü.</span><span class="sxs-lookup"><span data-stu-id="d0308-222">q=2 is new, so hello latest web app contents are retrieved and returned (V3).</span></span>

<span data-ttu-id="d0308-223">Daha fazla bilgi için bkz. [Sorgu dizeleri içeren Azure CDN önbelleğe alma davranışını kontrol etme](../cdn/cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="d0308-223">For more information, see [Control Azure CDN caching behavior with query strings](../cdn/cdn-query-string.md).</span></span>

## <a name="map-a-custom-domain-tooa-cdn-endpoint"></a><span data-ttu-id="d0308-224">Bir özel etki alanı tooa CDN uç noktası eşleme</span><span class="sxs-lookup"><span data-stu-id="d0308-224">Map a custom domain tooa CDN endpoint</span></span>

<span data-ttu-id="d0308-225">CNAME kaydı oluşturarak, özel etki alanı tooyour CDN uç noktası eşleme.</span><span class="sxs-lookup"><span data-stu-id="d0308-225">You'll map your custom domain tooyour CDN Endpoint by creating a CNAME record.</span></span> <span data-ttu-id="d0308-226">Bir CNAME kaydı, bir kaynak etki alanı tooa hedef etki alanını eşleyen bir DNS özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="d0308-226">A CNAME record is a DNS feature that maps a source domain tooa destination domain.</span></span> <span data-ttu-id="d0308-227">Örneğin, eşleyebilir `cdn.contoso.com` veya `static.contoso.com` çok`contoso.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="d0308-227">For example, you might map `cdn.contoso.com` or `static.contoso.com` too`contoso.azureedge.net`.</span></span>

<span data-ttu-id="d0308-228">Özel bir etki alanı yoksa, hello göz önünde bulundurun [uygulama hizmeti etki alanı öğretici](custom-dns-web-site-buydomains-web-app.md) kullanarak bir etki alanı toopurchase hello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="d0308-228">If you don't have a custom domain, consider following hello [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) toopurchase a domain using hello Azure portal.</span></span> 

### <a name="find-hello-hostname-toouse-with-hello-cname"></a><span data-ttu-id="d0308-229">Merhaba hostname toouse hello CNAME ile Bul</span><span class="sxs-lookup"><span data-stu-id="d0308-229">Find hello hostname toouse with hello CNAME</span></span>

<span data-ttu-id="d0308-230">Hello Azure portal'ın **Endpoint** sayfasında, emin olun **genel bakış** sol gezinti ve ardından hello hello seçili **+ özel etki alanı** hello sayfanın üst kısmındaki hello düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d0308-230">In hello Azure portal **Endpoint** page, make sure **Overview** is selected in hello left navigation, and then select hello **+ Custom Domain** button at hello top of hello page.</span></span>

![Özel Etki Alanı Ekle'yi seçin](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

<span data-ttu-id="d0308-232">Merhaba, **özel bir etki alanı ekleme** sayfaya, bir CNAME kaydı oluşturma hello uç noktası ana bilgisayar adı toouse bakın.</span><span class="sxs-lookup"><span data-stu-id="d0308-232">In hello **Add a custom domain** page, you see hello endpoint host name toouse in creating a CNAME record.</span></span> <span data-ttu-id="d0308-233">Merhaba ana bilgisayar adı, CDN uç nokta URL'sini türetilmiş:  **&lt;EndpointName >. azureedge.net**.</span><span class="sxs-lookup"><span data-stu-id="d0308-233">hello host name is derived from your CDN endpoint URL: **&lt;EndpointName>.azureedge.net**.</span></span> 

![Etki Alanı Ekle sayfası](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-hello-cname-with-your-domain-registrar"></a><span data-ttu-id="d0308-235">Etki alanı kayıt şirketinizle Hello CNAME yapılandırın</span><span class="sxs-lookup"><span data-stu-id="d0308-235">Configure hello CNAME with your domain registrar</span></span>

<span data-ttu-id="d0308-236">Tooyour etki alanı kayıt şirketinizin web sitesine gidin ve DNS kayıtları oluşturmak için hello bölümünü bulun.</span><span class="sxs-lookup"><span data-stu-id="d0308-236">Navigate tooyour domain registrar's web site, and locate hello section for creating DNS records.</span></span> <span data-ttu-id="d0308-237">Bunu, **Etki Alanı Adı**, **DNS** veya **Ad Sunucusu Yönetimi** gibi bir bölümde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0308-237">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>

<span data-ttu-id="d0308-238">Merhaba bölümü CNAME'ler yönetmek için bulunamıyor.</span><span class="sxs-lookup"><span data-stu-id="d0308-238">Find hello section for managing CNAMEs.</span></span> <span data-ttu-id="d0308-239">CNAME, diğer ad veya alt etki alanları hello sözcüklerinin olup olmadığına bakın ve toogo tooan Gelişmiş Ayarları sayfası olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0308-239">You may have toogo tooan advanced settings page and look for hello words CNAME, Alias, or Subdomains.</span></span>

<span data-ttu-id="d0308-240">Seçilen alt eşleyen bir CNAME kaydı oluşturun (örneğin, **statik** veya **cdn**) toohello **uç noktası ana bilgisayar adı** hello portalında daha önce gösterilen.</span><span class="sxs-lookup"><span data-stu-id="d0308-240">Create a CNAME record that maps your chosen subdomain (for example, **static** or **cdn**) toohello **Endpoint host name** shown earlier in hello portal.</span></span> 

### <a name="enter-hello-custom-domain-in-azure"></a><span data-ttu-id="d0308-241">Azure'da Hello özel etki alanı girin</span><span class="sxs-lookup"><span data-stu-id="d0308-241">Enter hello custom domain in Azure</span></span>

<span data-ttu-id="d0308-242">Toohello iade **özel bir etki alanı ekleme** sayfasında ve hello alt etki alanı, hello iletişim kutusunda dahil olmak üzere, özel etki alanı adı girin.</span><span class="sxs-lookup"><span data-stu-id="d0308-242">Return toohello **Add a custom domain** page, and enter your custom domain, including hello subdomain, in hello dialog box.</span></span> <span data-ttu-id="d0308-243">Örneğin, `cdn.contoso.com` girin.</span><span class="sxs-lookup"><span data-stu-id="d0308-243">For example, enter `cdn.contoso.com`.</span></span>   
   
<span data-ttu-id="d0308-244">Azure hello CNAME kaydı için hello etki alanı adı girdiğiniz var olduğunu doğrular.</span><span class="sxs-lookup"><span data-stu-id="d0308-244">Azure verifies that hello CNAME record exists for hello domain name you have entered.</span></span> <span data-ttu-id="d0308-245">Merhaba CNAME doğru ise, özel etki alanınız doğrulandı.</span><span class="sxs-lookup"><span data-stu-id="d0308-245">If hello CNAME is correct, your custom domain is validated.</span></span>

<span data-ttu-id="d0308-246">Merhaba Internet üzerinde hello CNAME kaydı toopropagate tooname sunucuları için zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="d0308-246">It can take time for hello CNAME record toopropagate tooname servers on hello Internet.</span></span> <span data-ttu-id="d0308-247">Etki alanınızı hemen doğrulanmaz, birkaç dakika bekleyin ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="d0308-247">If your domain is not validated immediately, wait a few minutes and try again.</span></span>

### <a name="test-hello-custom-domain"></a><span data-ttu-id="d0308-248">Test hello özel etki alanı</span><span class="sxs-lookup"><span data-stu-id="d0308-248">Test hello custom domain</span></span>

<span data-ttu-id="d0308-249">Bir tarayıcıda toohello gidin `index.html` özel etki alanınızı kullanarak dosya (örneğin, `cdn.contoso.com/index.html`) hello sonuç tooverify hello aynı olduğunda, doğrudan çok Git olarak`<endpointname>azureedge.net/index.html`.</span><span class="sxs-lookup"><span data-stu-id="d0308-249">In a browser, navigate toohello `index.html` file using your custom domain (for example, `cdn.contoso.com/index.html`) tooverify that hello result is hello same as when you go directly too`<endpointname>azureedge.net/index.html`.</span></span>

![Özel etki alanı URL'si kullanan örnek uygulama ana sayfası](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

<span data-ttu-id="d0308-251">Daha fazla bilgi için bkz: [harita Azure CDN içerik tooa özel etki alanı](../cdn/cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="d0308-251">For more information, see [Map Azure CDN content tooa custom domain](../cdn/cdn-map-content-to-custom-domain.md).</span></span>

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="d0308-252">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d0308-252">Next steps</span></span>

<span data-ttu-id="d0308-253">Öğrendiklerinizi:</span><span class="sxs-lookup"><span data-stu-id="d0308-253">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d0308-254">CDN uç noktası oluşturma.</span><span class="sxs-lookup"><span data-stu-id="d0308-254">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="d0308-255">Önbelleğe alınan varlıkları yenileme.</span><span class="sxs-lookup"><span data-stu-id="d0308-255">Refresh cached assets.</span></span>
> * <span data-ttu-id="d0308-256">Önbelleğe alınmış toocontrol sürümleri kullanım sorgu dizeleri.</span><span class="sxs-lookup"><span data-stu-id="d0308-256">Use query strings toocontrol cached versions.</span></span>
> * <span data-ttu-id="d0308-257">Özel bir etki alanı hello CDN uç noktası için kullanın.</span><span class="sxs-lookup"><span data-stu-id="d0308-257">Use a custom domain for hello CDN endpoint.</span></span>

<span data-ttu-id="d0308-258">Aşağıdaki hello toooptimize CDN performansı nasıl makaleler öğrenin:</span><span class="sxs-lookup"><span data-stu-id="d0308-258">Learn how toooptimize CDN performance in hello following articles:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d0308-259">Azure CDN’de dosyaları sıkıştırarak performansı geliştirme</span><span class="sxs-lookup"><span data-stu-id="d0308-259">Improve performance by compressing files in Azure CDN</span></span>](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="d0308-260">Azure CDN uç noktasında varlıkları önceden yükleme</span><span class="sxs-lookup"><span data-stu-id="d0308-260">Pre-load assets on an Azure CDN endpoint</span></span>](../cdn/cdn-preload-endpoint.md)
