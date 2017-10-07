---
title: aaaHow toocreate Azure API Management API'leri
description: "Bilgi nasıl toocreate ve Azure API Management'te API'leri yapılandırın."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 14c20da4-f29f-4b28-bec7-3d4c50b734da
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 48ed8d93947253aa1e67ad995927ed6101cac072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-apis-in-azure-api-management"></a><span data-ttu-id="9034f-103">Nasıl toocreate Azure API Management API'leri</span><span class="sxs-lookup"><span data-stu-id="9034f-103">How toocreate APIs in Azure API Management</span></span>
<span data-ttu-id="9034f-104">API Management bir API İstemci uygulamaları tarafından çağrılabilen işlemler kümesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="9034f-104">An API in API Management represents a set of operations that can be invoked by client applications.</span></span> <span data-ttu-id="9034f-105">Yeni API hello yayımcı portalında oluşturulur ve ardından operations eklenen hello istenen.</span><span class="sxs-lookup"><span data-stu-id="9034f-105">New APIs are created in hello publisher portal, and then hello desired operations are added.</span></span> <span data-ttu-id="9034f-106">Merhaba işlemleri eklendikten sonra hello API tooa ürün eklenir ve yayımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="9034f-106">Once hello operations are added, hello API is added tooa product and can be published.</span></span> <span data-ttu-id="9034f-107">Bir API yayımlandığında, geliştiriciler tarafından kullanılan abone tooand olabilir.</span><span class="sxs-lookup"><span data-stu-id="9034f-107">Once an API is published, it can be subscribed tooand used by developers.</span></span>

<span data-ttu-id="9034f-108">Bu kılavuz, hello işleminde hello ilk adımı gösterir: nasıl toocreate ve yeni bir API API Management içinde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9034f-108">This guide shows hello first step in hello process: how toocreate and configure a new API in API Management.</span></span> <span data-ttu-id="9034f-109">Operations ekleme ve bir ürün yayımlama hakkında daha fazla bilgi için bkz: [nasıl tooadd işlemleri tooan API] [ How tooadd operations tooan API] ve [nasıl toocreate ürün ve yayımlama] [ How toocreate and publish a product].</span><span class="sxs-lookup"><span data-stu-id="9034f-109">For more information on adding operations and publishing a product, see [How tooadd operations tooan API][How tooadd operations tooan API] and [How toocreate and publish a product][How toocreate and publish a product].</span></span>

## <span data-ttu-id="9034f-110"><a name="create-new-api"></a>Yeni bir API oluşturma</span><span class="sxs-lookup"><span data-stu-id="9034f-110"><a name="create-new-api"> </a>Create a new API</span></span>
<span data-ttu-id="9034f-111">API oluşturulur ve hello yayımcı portalında yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="9034f-111">APIs are created and configured in hello publisher portal.</span></span> <span data-ttu-id="9034f-112">tooaccess hello yayımcı portalı, tıklatın **yayımcı portalına** API Management hizmetiniz için hello Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="9034f-112">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Yayımcı portalı][api-management-management-console]

> <span data-ttu-id="9034f-114">Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="9034f-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="9034f-115">Tıklatın **API'leri** hello gelen **API Management** sol hello ve ardından menüsünde **API ekleme**.</span><span class="sxs-lookup"><span data-stu-id="9034f-115">Click **APIs** from hello **API Management** menu on hello left, and then click **add API**.</span></span>

![API oluşturma][api-management-create-api]

<span data-ttu-id="9034f-117">Kullanım hello **yeni API ekleme** penceresi tooconfigure hello yeni API.</span><span class="sxs-lookup"><span data-stu-id="9034f-117">Use hello **Add new API** window tooconfigure hello new API.</span></span>

![Yeni API ekle][api-management-add-new-api]

<span data-ttu-id="9034f-119">alanları aşağıdaki hello kullanılan tooconfigure hello yeni API ' dir.</span><span class="sxs-lookup"><span data-stu-id="9034f-119">hello following fields are used tooconfigure hello new API.</span></span>

* <span data-ttu-id="9034f-120">**Web API adı** hello API için benzersiz ve açıklayıcı bir ad sağlar.</span><span class="sxs-lookup"><span data-stu-id="9034f-120">**Web API name** provides a unique and descriptive name for hello API.</span></span> <span data-ttu-id="9034f-121">Merhaba Geliştirici ve yayımcı portallarında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9034f-121">It is displayed in hello developer and publisher portals.</span></span>
* <span data-ttu-id="9034f-122">**Web hizmeti URL'si** başvuruları hello hello API uygulama HTTP hizmeti.</span><span class="sxs-lookup"><span data-stu-id="9034f-122">**Web service URL** references hello HTTP service implementing hello API.</span></span> <span data-ttu-id="9034f-123">API management toothis adresi isteklerini iletir.</span><span class="sxs-lookup"><span data-stu-id="9034f-123">API management forwards requests toothis address.</span></span>
* <span data-ttu-id="9034f-124">**Web API'si URL soneki** eklenmiş toohello temel hello API management hizmeti URL'sidir.</span><span class="sxs-lookup"><span data-stu-id="9034f-124">**Web API URL suffix** is appended toohello base URL for hello API management service.</span></span> <span data-ttu-id="9034f-125">Merhaba temel URL bir API Management hizmet örneği tarafından barındırılan tüm API'leri yaygındır.</span><span class="sxs-lookup"><span data-stu-id="9034f-125">hello base URL is common for all APIs hosted by an API Management service instance.</span></span> <span data-ttu-id="9034f-126">API Management API'leri kendi soneki ayırır ve bu nedenle hello soneki her API için belirtilen yayımcı için benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9034f-126">API Management distinguishes APIs by their suffix and therefore hello suffix must be unique for every API for a given publisher.</span></span>
* <span data-ttu-id="9034f-127">**Web API'si URL şeması** hangi protokollerin kullanılan tooaccess hello API olabileceğini belirler.</span><span class="sxs-lookup"><span data-stu-id="9034f-127">**Web API URL scheme** determines which protocols can be used tooaccess hello API.</span></span> <span data-ttu-id="9034f-128">HTTPs varsayılan olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="9034f-128">HTTPs is specified by default.</span></span>
* <span data-ttu-id="9034f-129">toooptionally bu yeni API tooa ürün eklemek için hello tıklatın **ürünler (isteğe bağlı)** açılır ve bir ürün seçin.</span><span class="sxs-lookup"><span data-stu-id="9034f-129">toooptionally add this new API tooa product, click hello **Products (optional)** drop-down and choose a product.</span></span> <span data-ttu-id="9034f-130">Bu adım, yinelenen birden çok tooadd hello API toomultiple ürünleri kez olabilir.</span><span class="sxs-lookup"><span data-stu-id="9034f-130">This step can be repeated multiple times tooadd hello API toomultiple products.</span></span>

<span data-ttu-id="9034f-131">Değerleri yapılandırılmış Hello istenen sonra tıklayın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="9034f-131">Once hello desired values are configured, click **Save**.</span></span> <span data-ttu-id="9034f-132">Merhaba yeni API oluşturulduktan sonra hello hello API için Özet sayfasında hello yayımcı Portalı'nda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9034f-132">Once hello new API is created, hello summary page for hello API is displayed in hello publisher portal.</span></span>

![API özeti][api-management-api-summary]

## <span data-ttu-id="9034f-134"><a name="configure-api-settings"></a>API yapılandırma ayarları</span><span class="sxs-lookup"><span data-stu-id="9034f-134"><a name="configure-api-settings"> </a>Configure API settings</span></span>
<span data-ttu-id="9034f-135">Merhaba kullanabilirsiniz **ayarları** tooverify sekmesinde ve API hello yapılandırmasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="9034f-135">You can use hello **Settings** tab tooverify and edit hello configuration for an API.</span></span> <span data-ttu-id="9034f-136">**Web API adı**, **Web hizmeti URL'si**, ve **Web API'si URL soneki** hello API oluşturulduğunda ve değiştirilebilir başlangıçta burada ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="9034f-136">**Web API name**, **Web service URL**, and **Web API URL suffix** are initially set when hello API is created and can be modified here.</span></span> <span data-ttu-id="9034f-137">**Açıklama** isteğe bağlı bir açıklama sağlar ve **Web API'si URL şeması** hangi protokollerin kullanılan tooaccess hello API olabileceğini belirler.</span><span class="sxs-lookup"><span data-stu-id="9034f-137">**Description** provides an optional description, and **Web API URL scheme** determines which protocols can be used tooaccess hello API.</span></span>

![API ayarları][api-management-api-settings]

<span data-ttu-id="9034f-139">tooconfigure ağ geçidi hello arka uç hizmeti için uygulama hello API, kimlik doğrulaması hello **güvenlik** sekmesini hello **kimlik bilgileriyle** açılan kullanılan tooconfigure olabilir **HTTP temel** veya **istemci sertifikalarını** kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="9034f-139">tooconfigure gateway authentication for hello backend service implementing hello API, select hello **Security** tab. hello **With credentials** drop-down can be used tooconfigure **HTTP basic** or **Client certificates** authentication.</span></span> <span data-ttu-id="9034f-140">toouse HTTP temel kimlik doğrulaması, istenen hello kimlik bilgilerini girmeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="9034f-140">toouse HTTP basic authentication, simply enter hello desired credentials.</span></span> <span data-ttu-id="9034f-141">İstemci sertifikası kimlik doğrulamasını kullanma hakkında daha fazla bilgi için bkz: [nasıl toosecure arka uç hizmetlerini kullanan istemci sertifikası kimlik Azure API Management'te][How toosecure back-end services using client certificate authentication in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="9034f-141">For information on using client certificate authentication, see [How toosecure back-end services using client certificate authentication in Azure API Management][How toosecure back-end services using client certificate authentication in Azure API Management].</span></span>

<span data-ttu-id="9034f-142">Merhaba **güvenlik** sekmesi ayrıca kullanılan tooconfigure olması **kullanıcı yetkilendirme** OAuth 2.0 kullanan.</span><span class="sxs-lookup"><span data-stu-id="9034f-142">hello **Security** tab can also be used tooconfigure **User authorization** using OAuth 2.0.</span></span> <span data-ttu-id="9034f-143">Daha fazla bilgi için bkz: [nasıl tooauthorize Geliştirici kullanarak hesapları Azure API Management'te OAuth 2.0][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="9034f-143">For more information, see [How tooauthorize developer accounts using OAuth 2.0 in Azure API Management][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].</span></span>

![Temel kimlik doğrulama ayarları][api-management-api-settings-credentials]

<span data-ttu-id="9034f-145">Tıklatın **kaydetmek** toosave değişikliklerini API ayarları toohello yapın.</span><span class="sxs-lookup"><span data-stu-id="9034f-145">Click **Save** toosave any changes you make toohello API settings.</span></span>

## <span data-ttu-id="9034f-146"><a name="next-steps"> </a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9034f-146"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="9034f-147">Bir API oluşturulduğunu ve yapılandırılan hello ayarları hello sonraki adımlar sonra tooadd hello işlemleri toohello API, hello API tooa ürün ekleme ve böylece geliştiriciler için kullanılabilir yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="9034f-147">Once an API is created and hello settings configured, hello next steps are tooadd hello operations toohello API, add hello API tooa product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="9034f-148">Daha fazla bilgi için aşağıdaki makaleler hello bakın.</span><span class="sxs-lookup"><span data-stu-id="9034f-148">For more information, see hello following articles.</span></span>

* <span data-ttu-id="9034f-149">[Nasıl tooadd işlemleri tooan API][How tooadd operations tooan API]</span><span class="sxs-lookup"><span data-stu-id="9034f-149">[How tooadd operations tooan API][How tooadd operations tooan API]</span></span>
* <span data-ttu-id="9034f-150">[Nasıl toocreate ürün ve yayımlama][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="9034f-150">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

[api-management-create-api]: ./media/api-management-howto-create-apis/api-management-create-api.png
[api-management-management-console]: ./media/api-management-howto-create-apis/api-management-management-console.png
[api-management-add-new-api]: ./media/api-management-howto-create-apis/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-create-apis/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-create-apis/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-create-apis/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-create-apis/api-management-echo-operations.png

[What is an API?]: #what-is-api
[Create a new API]: #create-new-api
[Configure API settings]: #configure-api-settings
[Configure API operations]: #configure-api-operations
[Next steps]: #next-steps

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How toosecure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How tooauthorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
