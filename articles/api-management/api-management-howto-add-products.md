---
title: "Oluşturma ve Azure API Management'te bir ürün yayımlama"
description: "Oluşturma ve Azure API Management'te ürünleri yayımlama öğrenin."
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
ms.openlocfilehash: 73bf4451ba1b71807e22440beecc73a7e8045c5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-publish-a-product-in-azure-api-management"></a><span data-ttu-id="3af72-103">Oluşturma ve Azure API Management'te bir ürün yayımlama</span><span class="sxs-lookup"><span data-stu-id="3af72-103">How to create and publish a product in Azure API Management</span></span>
<span data-ttu-id="3af72-104">Azure API Management'te bir ürün kullanım kotası ve kullanım koşullarını yanı sıra bir veya daha fazla API'leri içerir.</span><span class="sxs-lookup"><span data-stu-id="3af72-104">In Azure API Management, a product contains one or more APIs as well as a usage quota and the terms of use.</span></span> <span data-ttu-id="3af72-105">Bir ürün yayımlandığında, geliştiriciler ürüne abone ve ürün API'lerine kullanmaya başlar.</span><span class="sxs-lookup"><span data-stu-id="3af72-105">Once a product is published, developers can subscribe to the product and begin to use the product's APIs.</span></span> <span data-ttu-id="3af72-106">Konu Ürün oluşturma, bir API ekleme ve geliştiriciler için yayımlama için bir kılavuz sağlar.</span><span class="sxs-lookup"><span data-stu-id="3af72-106">The topic provides a guide to creating a product, adding an API, and publishing it for developers.</span></span>

## <span data-ttu-id="3af72-107"><a name="create-product"></a>Ürün oluşturma</span><span class="sxs-lookup"><span data-stu-id="3af72-107"><a name="create-product"> </a>Create a product</span></span>
<span data-ttu-id="3af72-108">Operations eklenir ve bir API yayımcı portalında yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="3af72-108">Operations are added and configured to an API in the publisher portal.</span></span> <span data-ttu-id="3af72-109">Yayımcı portalına erişmek için tıklatın **yayımcı portalına** API Management hizmetiniz için Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="3af72-109">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Yayımcı portalı][api-management-management-console]

> <span data-ttu-id="3af72-111">Henüz bir API Management hizmeti örneği oluşturmadıysanız, [Azure API Management'i kullanmaya başlama][Get started with Azure API Management] öğreticisinde [API Management hizmet örneği oluşturma][Create an API Management service instance]'ya bakın.</span><span class="sxs-lookup"><span data-stu-id="3af72-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="3af72-112">Tıklayın **ürünleri** görüntülemek için soldaki menüde **ürünleri** sayfasında ve tıklayın **Ürün Ekle**.</span><span class="sxs-lookup"><span data-stu-id="3af72-112">Click on **Products** in the menu on the left to display the **Products** page, and click **Add Product**.</span></span>

![Ürünler][api-management-products]

![Yeni ürün][api-management-add-new-product]

<span data-ttu-id="3af72-115">Ürün için açıklayıcı bir ad girin **adı** alan ve ürün içinde açıklamasını **açıklama** alan.</span><span class="sxs-lookup"><span data-stu-id="3af72-115">Enter a descriptive name for the product in the **Name** field and a description of the product in the **Description** field.</span></span>

<span data-ttu-id="3af72-116">API Management ürünleri olabilir **açık** veya **korumalı**.</span><span class="sxs-lookup"><span data-stu-id="3af72-116">Products in API Management can be **Open** or **Protected**.</span></span> <span data-ttu-id="3af72-117">Korumalı ürünleri kullanabilmek için bunlara abone olmak gerekir, açık ürünler abonelik olmadan kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3af72-117">Protected products must be subscribed to before they can be used, while open products can be used without a subscription.</span></span> <span data-ttu-id="3af72-118">Denetleme **abonelik iste** bir abonelik gerektiren korumalı ürün oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="3af72-118">Check **Require subscription** to create a protected product that requires a subscription.</span></span> <span data-ttu-id="3af72-119">Bu varsayılan ayardır.</span><span class="sxs-lookup"><span data-stu-id="3af72-119">This is the default setting.</span></span>

<span data-ttu-id="3af72-120">Denetleme **abonelik onayı iste** gözden geçirin ve kabul edin ya da bu ürünün abonelik girişimleri reddetmek için yönetici istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="3af72-120">Check **Require subscription approval** if you want an administrator to review and accept or reject subscription attempts to this product.</span></span> <span data-ttu-id="3af72-121">Kutunun işaretli değilse abonelik girişimleri otomatik onaylı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3af72-121">If the box is unchecked, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="3af72-122">Abonelikler hakkında daha fazla bilgi için bkz: [bir ürüne abone olanları görüntüleme][View subscribers to a product].</span><span class="sxs-lookup"><span data-stu-id="3af72-122">For more information on subscriptions, see [View subscribers to a product][View subscribers to a product].</span></span>

<span data-ttu-id="3af72-123">Birden çok kez ürüne abone olmak Geliştirici hesaplarının izin verecek şekilde denetleyin **birden çok abonelik izin** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="3af72-123">To allow developer accounts to subscribe multiple times to the product, check the **Allow multiple subscriptions** check box.</span></span> <span data-ttu-id="3af72-124">Her geliştirici hesabını, bu kutu işaretli değilse, yalnızca tek bir kez ürüne abone olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3af72-124">If this box is not checked, each developer account can subscribe only a single time to the product.</span></span>

![Sınırsız birden çok abonelik][api-management-unlimited-multiple-subscriptions]

<span data-ttu-id="3af72-126">Birden çok aboneliğe sayısını sınırlamak için denetleme **aynı anda abonelik sayısını sınırlandır** onay kutusunu işaretleyin ve abonelik sınırı girin.</span><span class="sxs-lookup"><span data-stu-id="3af72-126">To limit the count of multiple simultaneous subscriptions, check the **Limit number of simultaneous subscriptions to** check box and enter the subscription limit.</span></span> <span data-ttu-id="3af72-127">Aşağıdaki örnekte, dört geliştirici her hesap için aynı anda abonelik sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="3af72-127">In the following example, simultaneous subscriptions are limited to four per developer account.</span></span>

![Dört birden çok abonelik][api-management-four-multiple-subscriptions]

<span data-ttu-id="3af72-129">Tüm yeni ürün seçenekleri yapılandırıldıktan sonra tıklatın **kaydetmek** yeni ürün oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="3af72-129">Once all new product options are configured, click **Save** to create the new product.</span></span>

![Ürünler][api-management-products-page]

> <span data-ttu-id="3af72-131">Varsayılan olarak yeni ürünler yayımdan ve yalnızca görünür **Yöneticiler** grubu.</span><span class="sxs-lookup"><span data-stu-id="3af72-131">By default new products are unpublished, and are visible only to the  **Administrators** group.</span></span>
> 
> 

<span data-ttu-id="3af72-132">Bir ürün yapılandırmak için ürün adı tıklayın **ürünleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="3af72-132">To configure a product, click on the product name in the **Products** tab.</span></span>

## <span data-ttu-id="3af72-133"><a name="add-apis"></a>Bir ürüne API ekleme</span><span class="sxs-lookup"><span data-stu-id="3af72-133"><a name="add-apis"> </a>Add APIs to a product</span></span>
<span data-ttu-id="3af72-134">**Ürünleri** sayfa yapılandırması için dört bağlantılarını içerir: **Özet**, **ayarları**, **görünürlük**, ve  **Aboneler**.</span><span class="sxs-lookup"><span data-stu-id="3af72-134">The **Products** page contains four links for configuration: **Summary**, **Settings**, **Visibility**, and **Subscribers**.</span></span> <span data-ttu-id="3af72-135">**Özet** sekme, burada API'leri ekleyebilir ve yayımlama veya yayımdan bir ürün kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3af72-135">The **Summary** tab is where you can add APIs and publish or unpublish a product.</span></span>

![Özet][api-management-new-product-summary]

<span data-ttu-id="3af72-137">Ürünü yayımlamadan önce bir veya daha fazla API'leri eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3af72-137">Before publishing your product you need to add one or more APIs.</span></span> <span data-ttu-id="3af72-138">Bunu yapmak için tıklatın **ürüne API Ekle**.</span><span class="sxs-lookup"><span data-stu-id="3af72-138">To do this, click **Add API to product**.</span></span>

![API ekleme][api-management-add-apis-to-product]

<span data-ttu-id="3af72-140">İstenen API'leri tıklatıp **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="3af72-140">Select the desired APIs and click **Save**.</span></span>

## <span data-ttu-id="3af72-141"><a name="add-description"></a>Açıklayıcı bilgiler için ürün ekleme</span><span class="sxs-lookup"><span data-stu-id="3af72-141"><a name="add-description"> </a>Add descriptive information to a product</span></span>
<span data-ttu-id="3af72-142">**Ayarları** sekme amacı, erişim sağladığı API'ları ve diğer yararlı bilgiler gibi ürün hakkında ayrıntılı bilgi sağlamak sağlar.</span><span class="sxs-lookup"><span data-stu-id="3af72-142">The **Settings** tab allows you to provide detailed information about the product such as its purpose, the APIs it provides access to, and other useful information.</span></span> <span data-ttu-id="3af72-143">İçerik, API çağırmayı ve düz metin veya HTML biçimlendirmesi yazılabilir geliştiriciler hedefleyen.</span><span class="sxs-lookup"><span data-stu-id="3af72-143">The content is targeted at the developers that will be calling the API and can be written in plain text or HTML markup.</span></span>

![Ürün ayarları][api-management-product-settings]

<span data-ttu-id="3af72-145">Denetleme **abonelik iste** abonelik olmadan çağrılabilir açık bir ürün oluşturmak için onay kutusunun işaretini kaldırın veya kullanılmak üzere bir abonelik gerektiren korumalı ürün oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="3af72-145">Check **Require subscription** to create a protected product that requires a subscription to be used, or clear the checkbox to create an open product that can be called without a subscription.</span></span>

<span data-ttu-id="3af72-146">Seçin **abonelik onayı iste** el ile tüm ürün abonelik isteklerini onaylama istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="3af72-146">Select **Require subscription approval** if you want to manually approve all product subscription requests.</span></span> <span data-ttu-id="3af72-147">Varsayılan olarak tüm ürün abonelikler otomatik olarak verilir.</span><span class="sxs-lookup"><span data-stu-id="3af72-147">By default all product subscriptions are granted automatically.</span></span>

<span data-ttu-id="3af72-148">Birden çok kez ürüne abone olmak Geliştirici hesaplarının izin verecek şekilde denetleyin **birden çok abonelik izin** onay kutusunu işaretleyin ve isteğe bağlı olarak bir sınırı belirtin.</span><span class="sxs-lookup"><span data-stu-id="3af72-148">To allow developer accounts to subscribe multiple times to the product, check the **Allow multiple subscriptions** check box and optionally specify a limit.</span></span> <span data-ttu-id="3af72-149">Her geliştirici hesabını, bu kutu işaretli değilse, yalnızca tek bir kez ürüne abone olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3af72-149">If this box is not checked, each developer account can subscribe only a single time to the product.</span></span>

<span data-ttu-id="3af72-150">İsteğe bağlı olarak doldurmak **kullanım koşulları** hangi aboneleri ürünü kullanmak için kabul etmelisiniz ürün için kullanım koşullarını açıklayan alan.</span><span class="sxs-lookup"><span data-stu-id="3af72-150">Optionally fill in the **Terms of use** field describing the terms of use for the product which subscribers must accept in order to use the product.</span></span>

## <span data-ttu-id="3af72-151"><a name="publish-product"></a>Bir ürün yayımlama</span><span class="sxs-lookup"><span data-stu-id="3af72-151"><a name="publish-product"> </a>Publish a product</span></span>
<span data-ttu-id="3af72-152">Bir ürün API'lerinde çağrılabilir önce ürünün yayımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3af72-152">Before the APIs in a product can be called, the product must be published.</span></span> <span data-ttu-id="3af72-153">Üzerinde **Özet** ürün için sekmesini tıklatın, **Yayımla**ve ardından **Evet, Yayımla** onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="3af72-153">On the **Summary** tab for the product, click **Publish**, and then click **Yes, publish it** to confirm.</span></span> <span data-ttu-id="3af72-154">Daha önce yayımlanmış bir ürüne özel yapmak için tıklatın **yayımdan**.</span><span class="sxs-lookup"><span data-stu-id="3af72-154">To make a previously published product private, click **Unpublish**.</span></span>

![Ürünü yayımlama][api-management-publish-product]

## <span data-ttu-id="3af72-156"><a name="make-visible"></a>Bir ürün geliştiriciler tarafından görülebilir kılma</span><span class="sxs-lookup"><span data-stu-id="3af72-156"><a name="make-visible"> </a>Make a product visible to developers</span></span>
<span data-ttu-id="3af72-157">**Görünürlük** sekme hangi rollerin Geliştirici portalında ürün görebilecek ve ürüne abone seçmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="3af72-157">The **Visibility** tab allows you to choose which roles are able to see the product on the developer portal and subscribe to the product.</span></span>

![Ürün görünürlüğü][api-management-product-visiblity]

<span data-ttu-id="3af72-159">Etkinleştirmek veya bir grup geliştiriciler için bir ürün görünürlüğünü devre dışı bırakmak için denetleyin veya grubun yanındaki onay kutusunun işaretini kaldırın ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="3af72-159">To enable or disable visibility of a product for the developers in a group, check or uncheck the check box beside the group and then click **Save**.</span></span>

> <span data-ttu-id="3af72-160">Daha fazla bilgi için bkz: [oluşturma ve Azure API Management'ta Geliştirici hesaplarını yönetmek için grupları kullanma][How to create and use groups to manage developer accounts in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="3af72-160">For more information, see [How to create and use groups to manage developer accounts in Azure API Management][How to create and use groups to manage developer accounts in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="3af72-161"><a name="view-subscribers"></a>Bir ürüne abone olanları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="3af72-161"><a name="view-subscribers"> </a>View subscribers to a product</span></span>
<span data-ttu-id="3af72-162">**Aboneleri** sekmesi ürüne abone olan geliştiricilere listeler.</span><span class="sxs-lookup"><span data-stu-id="3af72-162">The **Subscribers** tab lists the developers who have subscribed to the product.</span></span> <span data-ttu-id="3af72-163">Her geliştirici ayarlarını ve Ayrıntılar Geliştirici adına tıklayarak görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="3af72-163">The details and settings for each developer can be viewed by clicking on the developer's name.</span></span> <span data-ttu-id="3af72-164">Bu örnekte hiçbir geliştiriciler henüz ürüne abone oldunuz.</span><span class="sxs-lookup"><span data-stu-id="3af72-164">In this example no developers have yet subscribed to the product.</span></span>

![Geliştiriciler][api-management-developer-list]

## <span data-ttu-id="3af72-166"><a name="next-steps"> </a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3af72-166"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="3af72-167">İstenen API'ler eklendiğine ve ürün yayımlanan sonra geliştiriciler ürüne abone ve API'leri çağırmak başlayın.</span><span class="sxs-lookup"><span data-stu-id="3af72-167">Once the desired APIs are added and the product published, developers can subscribe to the product and begin to call the APIs.</span></span> <span data-ttu-id="3af72-168">Bu öğeleri yanı sıra Gelişmiş Ürün yapılandırma gösteren bir öğretici için bkz: [oluşturma ve Gelişmiş Ürün ayarları Azure API Management'te yapılandırma][How create and configure advanced product settings in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="3af72-168">For a tutorial that demonstrates these items as well as advanced product configuration see [How create and configure advanced product settings in Azure API Management][How create and configure advanced product settings in Azure API Management].</span></span>

<span data-ttu-id="3af72-169">Aşağıdaki videoda ürünleri ile çalışma hakkında daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="3af72-169">For more information about working with products, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs to a product]: #add-apis
[Add descriptive information to a product]: #add-description
[Publish a product]: #publish-product
[Make a product visible to developers]: #make-visible
[View subscribers to a product]: #view-subscribers
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


[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How to create and use groups to manage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
