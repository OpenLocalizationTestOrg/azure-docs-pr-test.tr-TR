---
title: "aaaHow toocreate ürün ve Azure API Management'te yayımlama"
description: "Bilgi nasıl toocreate ve ürünleri Azure API Management'te yayımlayın."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 31de55cb-9384-490b-a2f2-6dfcf83da764
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: f0a37f08b4e29ca68be9caec4c7604e3b4b6aaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-publish-a-product-in-azure-api-management"></a><span data-ttu-id="af459-103">Nasıl toocreate ve Azure API Management'te bir ürün yayımlama</span><span class="sxs-lookup"><span data-stu-id="af459-103">How toocreate and publish a product in Azure API Management</span></span>
<span data-ttu-id="af459-104">Azure API Management'te bir ürün, bir veya daha fazla API'leri ve bunun yanı sıra bir kullanım kotası ve hello kullanım koşulları içerir.</span><span class="sxs-lookup"><span data-stu-id="af459-104">In Azure API Management, a product contains one or more APIs as well as a usage quota and hello terms of use.</span></span> <span data-ttu-id="af459-105">Bir ürün yayımlandığında, geliştiricilerin toohello ürün abone ve toouse hello ürün API'lerine başlayın.</span><span class="sxs-lookup"><span data-stu-id="af459-105">Once a product is published, developers can subscribe toohello product and begin toouse hello product's APIs.</span></span> <span data-ttu-id="af459-106">Merhaba konu Kılavuzu toocreating bir ürüne API ekleme ve geliştiriciler için yayımlama sağlar.</span><span class="sxs-lookup"><span data-stu-id="af459-106">hello topic provides a guide toocreating a product, adding an API, and publishing it for developers.</span></span>

## <span data-ttu-id="af459-107"><a name="create-product"></a>Ürün oluşturma</span><span class="sxs-lookup"><span data-stu-id="af459-107"><a name="create-product"> </a>Create a product</span></span>
<span data-ttu-id="af459-108">Operations eklenir ve tooan API hello yayımcı portalında yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="af459-108">Operations are added and configured tooan API in hello publisher portal.</span></span> <span data-ttu-id="af459-109">tooaccess hello yayımcı portalı, tıklatın **yayımcı portalına** API Management hizmetiniz için hello Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="af459-109">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Yayımcı portalı][api-management-management-console]

> <span data-ttu-id="af459-111">Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="af459-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="af459-112">Tıklayın **ürünleri** hello sol toodisplay hello hello menüsünde **ürünleri** sayfasında ve tıklayın **Ürün Ekle**.</span><span class="sxs-lookup"><span data-stu-id="af459-112">Click on **Products** in hello menu on hello left toodisplay hello **Products** page, and click **Add Product**.</span></span>

![Ürünler][api-management-products]

![Yeni ürün][api-management-add-new-product]

<span data-ttu-id="af459-115">Hello hello ürün için açıklayıcı bir ad girin **adı** alan ve hello hello üründe açıklamasını **açıklama** alan.</span><span class="sxs-lookup"><span data-stu-id="af459-115">Enter a descriptive name for hello product in hello **Name** field and a description of hello product in hello **Description** field.</span></span>

<span data-ttu-id="af459-116">API Management ürünleri olabilir **açık** veya **korumalı**.</span><span class="sxs-lookup"><span data-stu-id="af459-116">Products in API Management can be **Open** or **Protected**.</span></span> <span data-ttu-id="af459-117">Korumalı ürünleri, bunlar kullanılabilir, açıkken abone toobefore olmalıdır ürünler abonelik olmadan kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="af459-117">Protected products must be subscribed toobefore they can be used, while open products can be used without a subscription.</span></span> <span data-ttu-id="af459-118">Denetleme **abonelik iste** toocreate bir abonelik gerektiren korumalı ürün.</span><span class="sxs-lookup"><span data-stu-id="af459-118">Check **Require subscription** toocreate a protected product that requires a subscription.</span></span> <span data-ttu-id="af459-119">Merhaba varsayılan ayar budur.</span><span class="sxs-lookup"><span data-stu-id="af459-119">This is hello default setting.</span></span>

<span data-ttu-id="af459-120">Denetleme **abonelik onayı iste** bir yönetici tooreview istediğiniz ve kabul edin veya reddedin abonelik toothis ürün çalışır.</span><span class="sxs-lookup"><span data-stu-id="af459-120">Check **Require subscription approval** if you want an administrator tooreview and accept or reject subscription attempts toothis product.</span></span> <span data-ttu-id="af459-121">Merhaba kutusu işaretli değilse abonelik girişimleri otomatik onaylı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="af459-121">If hello box is unchecked, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="af459-122">Abonelikler hakkında daha fazla bilgi için bkz: [görünüm aboneleri tooa ürün][View subscribers tooa product].</span><span class="sxs-lookup"><span data-stu-id="af459-122">For more information on subscriptions, see [View subscribers tooa product][View subscribers tooa product].</span></span>

<span data-ttu-id="af459-123">tooallow Geliştirici hesaplarını toosubscribe birden çok kez toohello ürün denetleyin hello **birden çok abonelik izin** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="af459-123">tooallow developer accounts toosubscribe multiple times toohello product, check hello **Allow multiple subscriptions** check box.</span></span> <span data-ttu-id="af459-124">Her geliştirici hesabını, bu kutu işaretli değilse, yalnızca bir kereliğine toohello ürün abone olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af459-124">If this box is not checked, each developer account can subscribe only a single time toohello product.</span></span>

![Sınırsız birden çok abonelik][api-management-unlimited-multiple-subscriptions]

<span data-ttu-id="af459-126">toolimit hello aynı anda birden fazla abonelik sayısını kontrol hello **aynı anda abonelik sayısını sınırlandır** onay kutusunu işaretleyin ve hello abonelik sınırı girin.</span><span class="sxs-lookup"><span data-stu-id="af459-126">toolimit hello count of multiple simultaneous subscriptions, check hello **Limit number of simultaneous subscriptions to** check box and enter hello subscription limit.</span></span> <span data-ttu-id="af459-127">Aşağıdaki örneğine hello, sınırlı toofour Geliştirici hesabı başına eşzamanlı abonelikler var.</span><span class="sxs-lookup"><span data-stu-id="af459-127">In hello following example, simultaneous subscriptions are limited toofour per developer account.</span></span>

![Dört birden çok abonelik][api-management-four-multiple-subscriptions]

<span data-ttu-id="af459-129">Tüm yeni ürün seçenekleri yapılandırıldıktan sonra tıklatın **kaydetmek** toocreate hello yeni ürün.</span><span class="sxs-lookup"><span data-stu-id="af459-129">Once all new product options are configured, click **Save** toocreate hello new product.</span></span>

![Ürünler][api-management-products-page]

> <span data-ttu-id="af459-131">Varsayılan olarak yeni ürünler yayımdan olduğunda ve görünür yalnızca toohello **Yöneticiler** grubu.</span><span class="sxs-lookup"><span data-stu-id="af459-131">By default new products are unpublished, and are visible only toohello  **Administrators** group.</span></span>
> 
> 

<span data-ttu-id="af459-132">Merhaba hello ürün adı tooconfigure bir ürün tıklayın **ürünleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="af459-132">tooconfigure a product, click on hello product name in hello **Products** tab.</span></span>

## <span data-ttu-id="af459-133"><a name="add-apis"></a>Ekleme API'leri tooa ürün</span><span class="sxs-lookup"><span data-stu-id="af459-133"><a name="add-apis"> </a>Add APIs tooa product</span></span>
<span data-ttu-id="af459-134">Merhaba **ürünleri** sayfa yapılandırması için dört bağlantılarını içerir: **Özet**, **ayarları**, **görünürlük**, ve  **Aboneler**.</span><span class="sxs-lookup"><span data-stu-id="af459-134">hello **Products** page contains four links for configuration: **Summary**, **Settings**, **Visibility**, and **Subscribers**.</span></span> <span data-ttu-id="af459-135">Merhaba **Özet** sekme, burada API'leri ekleyebilir ve yayımlama veya yayımdan bir ürün kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="af459-135">hello **Summary** tab is where you can add APIs and publish or unpublish a product.</span></span>

![Özet][api-management-new-product-summary]

<span data-ttu-id="af459-137">Ürünü yayımlamadan önce bir veya daha fazla API'leri tooadd gerekir.</span><span class="sxs-lookup"><span data-stu-id="af459-137">Before publishing your product you need tooadd one or more APIs.</span></span> <span data-ttu-id="af459-138">toodo bunu, **API Ekle tooproduct**.</span><span class="sxs-lookup"><span data-stu-id="af459-138">toodo this, click **Add API tooproduct**.</span></span>

![API ekleme][api-management-add-apis-to-product]

<span data-ttu-id="af459-140">Select hello istenen API'ler ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="af459-140">Select hello desired APIs and click **Save**.</span></span>

## <span data-ttu-id="af459-141"><a name="add-description"></a>Ekle açıklayıcı bilgiler tooa ürün</span><span class="sxs-lookup"><span data-stu-id="af459-141"><a name="add-description"> </a>Add descriptive information tooa product</span></span>
<span data-ttu-id="af459-142">Merhaba **ayarları** sekme sağlar, tooprovide amacı, hello API'leri erişim sağlar ve diğer yararlı bilgiler gibi hello ürün hakkında ayrıntılı bilgi.</span><span class="sxs-lookup"><span data-stu-id="af459-142">hello **Settings** tab allows you tooprovide detailed information about hello product such as its purpose, hello APIs it provides access to, and other useful information.</span></span> <span data-ttu-id="af459-143">Merhaba içerik hello API çağırma ve düz metin veya HTML biçimlendirmesi yazılabilir hello geliştiriciler hedefleyen.</span><span class="sxs-lookup"><span data-stu-id="af459-143">hello content is targeted at hello developers that will be calling hello API and can be written in plain text or HTML markup.</span></span>

![Ürün ayarları][api-management-product-settings]

<span data-ttu-id="af459-145">Denetleme **abonelik iste** toocreate abonelik toobe kullanılan ya da Temizle gerektiren korumalı ürün hello onay kutusunu toocreate abonelik olmadan çağrılabilen bir ürünü aç.</span><span class="sxs-lookup"><span data-stu-id="af459-145">Check **Require subscription** toocreate a protected product that requires a subscription toobe used, or clear hello checkbox toocreate an open product that can be called without a subscription.</span></span>

<span data-ttu-id="af459-146">Seçin **abonelik onayı iste** toomanually istiyorsanız, tüm ürün abonelik istekleri onaylayabilir.</span><span class="sxs-lookup"><span data-stu-id="af459-146">Select **Require subscription approval** if you want toomanually approve all product subscription requests.</span></span> <span data-ttu-id="af459-147">Varsayılan olarak tüm ürün abonelikler otomatik olarak verilir.</span><span class="sxs-lookup"><span data-stu-id="af459-147">By default all product subscriptions are granted automatically.</span></span>

<span data-ttu-id="af459-148">tooallow Geliştirici hesaplarını toosubscribe birden çok kez toohello ürün denetleyin hello **birden çok abonelik izin** onay kutusunu işaretleyin ve isteğe bağlı olarak bir sınırı belirtin.</span><span class="sxs-lookup"><span data-stu-id="af459-148">tooallow developer accounts toosubscribe multiple times toohello product, check hello **Allow multiple subscriptions** check box and optionally specify a limit.</span></span> <span data-ttu-id="af459-149">Her geliştirici hesabını, bu kutu işaretli değilse, yalnızca bir kereliğine toohello ürün abone olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af459-149">If this box is not checked, each developer account can subscribe only a single time toohello product.</span></span>

<span data-ttu-id="af459-150">İsteğe bağlı olarak hello dolgu **kullanım koşulları** hello kullanım koşullarına aboneleri sipariş toouse hello üründe kabul etmelisiniz hello ürün açıklayan alan.</span><span class="sxs-lookup"><span data-stu-id="af459-150">Optionally fill in hello **Terms of use** field describing hello terms of use for hello product which subscribers must accept in order toouse hello product.</span></span>

## <span data-ttu-id="af459-151"><a name="publish-product"></a>Bir ürün yayımlama</span><span class="sxs-lookup"><span data-stu-id="af459-151"><a name="publish-product"> </a>Publish a product</span></span>
<span data-ttu-id="af459-152">Bir ürün Hello API'leri çağrılabilir önce hello ürünün yayımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="af459-152">Before hello APIs in a product can be called, hello product must be published.</span></span> <span data-ttu-id="af459-153">Merhaba üzerinde **Özet** hello ürün sekmesini tıklatın, **Yayımla**ve ardından **Evet, Yayımla** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="af459-153">On hello **Summary** tab for hello product, click **Publish**, and then click **Yes, publish it** tooconfirm.</span></span> <span data-ttu-id="af459-154">toomake önceden yayımlanmış ürün özel tıklatın **yayımdan**.</span><span class="sxs-lookup"><span data-stu-id="af459-154">toomake a previously published product private, click **Unpublish**.</span></span>

![Ürünü yayımlama][api-management-publish-product]

## <span data-ttu-id="af459-156"><a name="make-visible"></a>Ürün görünür toodevelopers olun</span><span class="sxs-lookup"><span data-stu-id="af459-156"><a name="make-visible"> </a>Make a product visible toodevelopers</span></span>
<span data-ttu-id="af459-157">Merhaba **görünürlük** sekme hangi roller mümkün toosee hello ürün hello Geliştirici Portalı üzerinde ve toohello ürün abone toochoose sağlar.</span><span class="sxs-lookup"><span data-stu-id="af459-157">hello **Visibility** tab allows you toochoose which roles are able toosee hello product on hello developer portal and subscribe toohello product.</span></span>

![Ürün görünürlüğü][api-management-product-visiblity]

<span data-ttu-id="af459-159">bir grup halinde hello geliştiriciler için bir ürün tooenable veya devre dışı bırakma görünürlüğünü denetleme veya hello hello grubunun yanındaki onay kutusunun işaretini kaldırın ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="af459-159">tooenable or disable visibility of a product for hello developers in a group, check or uncheck hello check box beside hello group and then click **Save**.</span></span>

> <span data-ttu-id="af459-160">Daha fazla bilgi için bkz: [nasıl toocreate ve kullanım grupları toomanage Geliştirici Azure API Management'te hesapları][How toocreate and use groups toomanage developer accounts in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="af459-160">For more information, see [How toocreate and use groups toomanage developer accounts in Azure API Management][How toocreate and use groups toomanage developer accounts in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="af459-161"><a name="view-subscribers"></a>Görünüm aboneleri tooa ürün</span><span class="sxs-lookup"><span data-stu-id="af459-161"><a name="view-subscribers"> </a>View subscribers tooa product</span></span>
<span data-ttu-id="af459-162">Merhaba **aboneleri** sekmesi toohello ürün abone olduğunuz hello geliştiriciler listeler.</span><span class="sxs-lookup"><span data-stu-id="af459-162">hello **Subscribers** tab lists hello developers who have subscribed toohello product.</span></span> <span data-ttu-id="af459-163">Merhaba ayrıntılarını ve ayarlar her geliştirici hello geliştiricinin adına tıklayarak görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="af459-163">hello details and settings for each developer can be viewed by clicking on hello developer's name.</span></span> <span data-ttu-id="af459-164">Bu örnekte hiçbir geliştiriciler henüz toohello ürün abone oldunuz.</span><span class="sxs-lookup"><span data-stu-id="af459-164">In this example no developers have yet subscribed toohello product.</span></span>

![Geliştiriciler][api-management-developer-list]

## <span data-ttu-id="af459-166"><a name="next-steps"> </a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="af459-166"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="af459-167">Bir kez hello API'ler eklenmiştir ve hello ürün yayımlanan, geliştiriciler toohello ürün abone ve toocall hello API'leri başlamak istenen.</span><span class="sxs-lookup"><span data-stu-id="af459-167">Once hello desired APIs are added and hello product published, developers can subscribe toohello product and begin toocall hello APIs.</span></span> <span data-ttu-id="af459-168">Bu öğeleri yanı sıra Gelişmiş Ürün yapılandırma gösteren bir öğretici için bkz: [oluşturma ve Gelişmiş Ürün ayarları Azure API Management'te yapılandırma][How create and configure advanced product settings in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="af459-168">For a tutorial that demonstrates these items as well as advanced product configuration see [How create and configure advanced product settings in Azure API Management][How create and configure advanced product settings in Azure API Management].</span></span>

<span data-ttu-id="af459-169">Ürünleri ile çalışma hakkında daha fazla bilgi için video aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="af459-169">For more information about working with products, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs tooa product]: #add-apis
[Add descriptive information tooa product]: #add-description
[Publish a product]: #publish-product
[Make a product visible toodevelopers]: #make-visible
[View subscribers tooa product]: #view-subscribers
[Next steps]: #next-steps

[api-management-management-console]: ./media/api-management-howto-add-products/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-add-products/api-management-add-product.png
[api-management-add-new-product]: ./media/api-management-howto-add-products/api-management-add-new-product.png
[api-management-unlimited-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-unlimited-multiple-subscriptions.png
[api-management-four-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-four-multiple-subscriptions.png
[api-management-products-page]: ./media/api-management-howto-add-products/api-management-products-page.png
[api-management-new-product-summary]: ./media/api-management-howto-add-products/api-management-new-product-summary.png
[api-management-add-apis-to-product]: ./media/api-management-howto-add-products/api-management-add-apis-to-product.png
[api-management-product-settings]: ./media/api-management-howto-add-products/api-management-product-settings.png
[api-management-publish-product]: ./media/api-management-howto-add-products/api-management-publish-product.png
[api-management-product-visiblity]: ./media/api-management-howto-add-products/api-management-product-visibility.png
[api-management-developer-list]: ./media/api-management-howto-add-products/api-management-developer-list.png



[api-management-products]: ./media/api-management-howto-add-products/api-management-products.png
[api-management-]: ./media/api-management-howto-add-products/
[api-management-]: ./media/api-management-howto-add-products/


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How toocreate and use groups toomanage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
