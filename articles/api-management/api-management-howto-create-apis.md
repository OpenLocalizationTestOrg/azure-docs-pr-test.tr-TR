---
title: "Azure API Management'te API oluşturma"
description: "Oluşturma ve Azure API Management'te API'leri yapılandırmak hakkında bilgi edinin."
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
ms.openlocfilehash: ab08256fbc3caca05bf23a12016ad2acf4fc7412
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-apis-in-azure-api-management"></a><span data-ttu-id="26a33-103">Azure API Management'te API oluşturma</span><span class="sxs-lookup"><span data-stu-id="26a33-103">How to create APIs in Azure API Management</span></span>
<span data-ttu-id="26a33-104">API Management bir API İstemci uygulamaları tarafından çağrılabilen işlemler kümesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="26a33-104">An API in API Management represents a set of operations that can be invoked by client applications.</span></span> <span data-ttu-id="26a33-105">Yeni API'leri yayımcı portalında oluşturulur ve ardından istenen işlemleri eklenir.</span><span class="sxs-lookup"><span data-stu-id="26a33-105">New APIs are created in the publisher portal, and then the desired operations are added.</span></span> <span data-ttu-id="26a33-106">Operations eklendikten sonra API bir ürüne eklenebilir ve yayımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="26a33-106">Once the operations are added, the API is added to a product and can be published.</span></span> <span data-ttu-id="26a33-107">Bir API yayımlandığında abone ve geliştiriciler tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="26a33-107">Once an API is published, it can be subscribed to and used by developers.</span></span>

<span data-ttu-id="26a33-108">Bu kılavuz, işlemde ilk adımı gösterir: oluşturma ve yeni bir API API Management içinde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="26a33-108">This guide shows the first step in the process: how to create and configure a new API in API Management.</span></span> <span data-ttu-id="26a33-109">Operations ekleme ve bir ürün yayımlama hakkında daha fazla bilgi için bkz: [API'ye işlem ekleme] [ How to add operations to an API] ve [nasıl oluşturulacağı ve bir ürün yayımlama][How to create and publish a product].</span><span class="sxs-lookup"><span data-stu-id="26a33-109">For more information on adding operations and publishing a product, see [How to add operations to an API][How to add operations to an API] and [How to create and publish a product][How to create and publish a product].</span></span>

## <span data-ttu-id="26a33-110"><a name="create-new-api"></a>Yeni bir API oluşturma</span><span class="sxs-lookup"><span data-stu-id="26a33-110"><a name="create-new-api"> </a>Create a new API</span></span>
<span data-ttu-id="26a33-111">API oluşturulur ve yayımcı portalında yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="26a33-111">APIs are created and configured in the publisher portal.</span></span> <span data-ttu-id="26a33-112">Yayımcı portalına erişmek için tıklatın **yayımcı portalına** API Management hizmetiniz için Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="26a33-112">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Yayımcı portalı][api-management-management-console]

> <span data-ttu-id="26a33-114">Henüz bir API Management hizmeti örneği oluşturmadıysanız, [Azure API Management'i kullanmaya başlama][Get started with Azure API Management] öğreticisinde [API Management hizmet örneği oluşturma][Create an API Management service instance]'ya bakın.</span><span class="sxs-lookup"><span data-stu-id="26a33-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="26a33-115">Tıklatın **API'leri** gelen **API Management** sol menüsünde ve ardından **API ekleme**.</span><span class="sxs-lookup"><span data-stu-id="26a33-115">Click **APIs** from the **API Management** menu on the left, and then click **add API**.</span></span>

![API oluşturma][api-management-create-api]

<span data-ttu-id="26a33-117">Kullanım **yeni API ekleme** yeni API yapılandırmak için penceresi.</span><span class="sxs-lookup"><span data-stu-id="26a33-117">Use the **Add new API** window to configure the new API.</span></span>

![Yeni API ekle][api-management-add-new-api]

<span data-ttu-id="26a33-119">Aşağıdaki alanları yeni API yapılandırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="26a33-119">The following fields are used to configure the new API.</span></span>

* <span data-ttu-id="26a33-120">**Web API adı** API için benzersiz ve açıklayıcı bir ad sağlar.</span><span class="sxs-lookup"><span data-stu-id="26a33-120">**Web API name** provides a unique and descriptive name for the API.</span></span> <span data-ttu-id="26a33-121">Geliştirici ve yayımcı portallarında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="26a33-121">It is displayed in the developer and publisher portals.</span></span>
* <span data-ttu-id="26a33-122">**Web hizmeti URL'si** API uygulama HTTP hizmeti başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="26a33-122">**Web service URL** references the HTTP service implementing the API.</span></span> <span data-ttu-id="26a33-123">API management bu adrese isteklerini iletir.</span><span class="sxs-lookup"><span data-stu-id="26a33-123">API management forwards requests to this address.</span></span>
* <span data-ttu-id="26a33-124">**Web API'si URL soneki** API management hizmeti temel URL'si eklenir.</span><span class="sxs-lookup"><span data-stu-id="26a33-124">**Web API URL suffix** is appended to the base URL for the API management service.</span></span> <span data-ttu-id="26a33-125">Temel URL bir API Management hizmet örneği tarafından barındırılan tüm API'leri yaygındır.</span><span class="sxs-lookup"><span data-stu-id="26a33-125">The base URL is common for all APIs hosted by an API Management service instance.</span></span> <span data-ttu-id="26a33-126">API Management API'leri kendi soneki ayırır ve bu nedenle soneki her API için belirtilen yayımcı için benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="26a33-126">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API for a given publisher.</span></span>
* <span data-ttu-id="26a33-127">**Web API'si URL şeması** API erişmek için hangi protokollerin kullanılabileceğini belirler.</span><span class="sxs-lookup"><span data-stu-id="26a33-127">**Web API URL scheme** determines which protocols can be used to access the API.</span></span> <span data-ttu-id="26a33-128">HTTPs varsayılan olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="26a33-128">HTTPs is specified by default.</span></span>
* <span data-ttu-id="26a33-129">İsteğe bağlı olarak bu yeni API ürün eklemek için tıklatın **ürünler (isteğe bağlı)** açılır ve bir ürün seçin.</span><span class="sxs-lookup"><span data-stu-id="26a33-129">To optionally add this new API to a product, click the **Products (optional)** drop-down and choose a product.</span></span> <span data-ttu-id="26a33-130">Bu adım, birden fazla ürün için API eklemek için birden çok kez yinelenebilir.</span><span class="sxs-lookup"><span data-stu-id="26a33-130">This step can be repeated multiple times to add the API to multiple products.</span></span>

<span data-ttu-id="26a33-131">İstenen değerleri yapılandırıldıktan sonra tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="26a33-131">Once the desired values are configured, click **Save**.</span></span> <span data-ttu-id="26a33-132">Yeni API oluşturulduktan sonra API için Özet sayfasında yayımcı portalında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="26a33-132">Once the new API is created, the summary page for the API is displayed in the publisher portal.</span></span>

![API özeti][api-management-api-summary]

## <span data-ttu-id="26a33-134"><a name="configure-api-settings"></a>API yapılandırma ayarları</span><span class="sxs-lookup"><span data-stu-id="26a33-134"><a name="configure-api-settings"> </a>Configure API settings</span></span>
<span data-ttu-id="26a33-135">Kullanabileceğiniz **ayarları** doğrulayın ve API yapılandırmasını düzenlemek için sekmesini.</span><span class="sxs-lookup"><span data-stu-id="26a33-135">You can use the **Settings** tab to verify and edit the configuration for an API.</span></span> <span data-ttu-id="26a33-136">**Web API adı**, **Web hizmeti URL'si**, ve **Web API'si URL soneki** API oluşturulduğunda ve değiştirilebilir başlangıçta burada ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="26a33-136">**Web API name**, **Web service URL**, and **Web API URL suffix** are initially set when the API is created and can be modified here.</span></span> <span data-ttu-id="26a33-137">**Açıklama** isteğe bağlı bir açıklama sağlar ve **Web API'si URL şeması** API erişmek için hangi protokollerin kullanılabileceğini belirler.</span><span class="sxs-lookup"><span data-stu-id="26a33-137">**Description** provides an optional description, and **Web API URL scheme** determines which protocols can be used to access the API.</span></span>

![API ayarları][api-management-api-settings]

<span data-ttu-id="26a33-139">API uygulama arka uç hizmetine ağ geçidi kimlik doğrulamasını yapılandırmak için seçin **güvenlik** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="26a33-139">To configure gateway authentication for the backend service implementing the API, select the **Security** tab.</span></span> <span data-ttu-id="26a33-140">**Kimlik bilgileriyle** açılan yapılandırmak için kullanılabilir **HTTP temel** veya **istemci sertifikalarını** kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="26a33-140">The **With credentials** drop-down can be used to configure **HTTP basic** or **Client certificates** authentication.</span></span> <span data-ttu-id="26a33-141">HTTP temel kimlik doğrulaması kullanmak için istenen kimlik bilgilerini girmeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="26a33-141">To use HTTP basic authentication, simply enter the desired credentials.</span></span> <span data-ttu-id="26a33-142">İstemci sertifikası kimlik doğrulamasını kullanma hakkında daha fazla bilgi için bkz: [arka uç hizmetlerini kullanan istemci sertifikası kimlik doğrulaması Azure API Management'te güvenliğini sağlamak nasıl][How to secure back-end services using client certificate authentication in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="26a33-142">For information on using client certificate authentication, see [How to secure back-end services using client certificate authentication in Azure API Management][How to secure back-end services using client certificate authentication in Azure API Management].</span></span>

<span data-ttu-id="26a33-143">**Güvenlik** sekmesinde de kullanılabilir yapılandırmak için **kullanıcı yetkilendirme** OAuth 2.0 kullanan.</span><span class="sxs-lookup"><span data-stu-id="26a33-143">The **Security** tab can also be used to configure **User authorization** using OAuth 2.0.</span></span> <span data-ttu-id="26a33-144">Daha fazla bilgi için bkz: [Azure API Management'te OAuth 2.0 kullanan Geliştirici hesaplarını yetkilendirmede nasıl][How to authorize developer accounts using OAuth 2.0 in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="26a33-144">For more information, see [How to authorize developer accounts using OAuth 2.0 in Azure API Management][How to authorize developer accounts using OAuth 2.0 in Azure API Management].</span></span>

![Temel kimlik doğrulama ayarları][api-management-api-settings-credentials]

<span data-ttu-id="26a33-146">Tıklatın **kaydetmek** API ayarları yaptığınız değişiklikleri kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="26a33-146">Click **Save** to save any changes you make to the API settings.</span></span>

## <span data-ttu-id="26a33-147"><a name="next-steps"> </a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="26a33-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="26a33-148">Bir API oluşturup yapılandırılan ayarları, sonraki adımlar için API işlemleri eklemek üzeresiniz sonra bir ürüne API ekleme ve böylece geliştiriciler için kullanılabilir yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="26a33-148">Once an API is created and the settings configured, the next steps are to add the operations to the API, add the API to a product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="26a33-149">Daha fazla bilgi için aşağıdaki makalelere bakın.</span><span class="sxs-lookup"><span data-stu-id="26a33-149">For more information, see the following articles.</span></span>

* <span data-ttu-id="26a33-150">[API'ye işlem ekleme][How to add operations to an API]</span><span class="sxs-lookup"><span data-stu-id="26a33-150">[How to add operations to an API][How to add operations to an API]</span></span>
* <span data-ttu-id="26a33-151">[Oluşturma ve bir ürün yayımlama][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="26a33-151">[How to create and publish a product][How to create and publish a product]</span></span>

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

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How to secure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How to authorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
