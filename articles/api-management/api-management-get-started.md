---
title: "Azure API Management’ta ilk API’nizi yönetme | Microsoft Belgeleri"
description: "API oluşturmayı ve işlemler eklemeyi öğrenin, API Management’i kullanmaya başlayın."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 51b7df8b-1c43-43c6-90c9-0aa24f48206b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 6e76d1ee08f804637999ef2ebf5d25becf6a0408
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a><span data-ttu-id="6c47a-103">İlk API’nizi Azure API Management’te yönetme</span><span class="sxs-lookup"><span data-stu-id="6c47a-103">Manage your first API in Azure API Management</span></span>
## <span data-ttu-id="6c47a-104"><a name="overview"> </a>Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="6c47a-104"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="6c47a-105">Bu kılavuz size Azure API Management’i hızlı bir şekilde nasıl kullanmaya başlayacağınızı ve ilk API çağrınızı yapmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="6c47a-105">This guide shows you how to quickly get started in using Azure API Management and make your first API call.</span></span>

## <span data-ttu-id="6c47a-106"><a name="concepts"> </a>Azure API Management nedir?</span><span class="sxs-lookup"><span data-stu-id="6c47a-106"><a name="concepts"> </a>What is Azure API Management?</span></span>
<span data-ttu-id="6c47a-107">Azure API Management’i bir arka uç almak ve bunu temel alan tam özellikli bir API programını başlatmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c47a-107">You can use Azure API Management to take any backend and launch a full-fledged API program based on it.</span></span>

<span data-ttu-id="6c47a-108">Yaygın senaryolar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="6c47a-108">Common scenarios include:</span></span>

* <span data-ttu-id="6c47a-109">**Mobil altyapıyı koruma**: API anahtarlarına erişim geçişi sağlayarak, azaltma ile DOS saldırılarını önleyerek ya da JWT belirtecini doğrulama gibi gelişmiş güvenlik ilkelerini kullanarak mobil altyapıyı koruyun.</span><span class="sxs-lookup"><span data-stu-id="6c47a-109">**Securing mobile infrastructure** by gating access with API keys, preventing DOS attacks by using throttling, or using advanced security policies like JWT token validation.</span></span>
* <span data-ttu-id="6c47a-110">**ISV iş ortağı ekosistemlerini etkinleştirme**: Geliştirici Portalı üzerinden hızlı iş ortağı ekleyerek ve iş ortağı kullanımı için hazır olmayan dahili uygulamalardan bir API cephesi oluşturarak ISV iş ortağı eko sistemlerini etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="6c47a-110">**Enabling ISV partner ecosystems** by offering fast partner onboarding through the developer portal and building an API facade to decouple from internal implementations that are not ripe for partner consumption.</span></span>
* <span data-ttu-id="6c47a-111">**Dahili API programı çalıştırma** API’lerin kullanılabilirliği ve son değişikliklerine ilişkin iletişim için kuruluşa merkezi bir konum sağlayarak ve kurumsal hesaplar temelinde erişim geçişi sağlayarak, tümü API ağ geçidi ve arka uç arasında güvenli bir kanalı temel alan dahili API programı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6c47a-111">**Running an internal API program** by offering a centralized location for the organization to communicate about the availability and latest changes to APIs, gating access based on organizational accounts, all based on a secured channel between the API gateway and the backend.</span></span>

<span data-ttu-id="6c47a-112">Sistem aşağıdaki bileşenlerden oluşur:</span><span class="sxs-lookup"><span data-stu-id="6c47a-112">The system is made up of the following components:</span></span>

* <span data-ttu-id="6c47a-113">**API ağ geçidi** şunları yapan uç noktadır:</span><span class="sxs-lookup"><span data-stu-id="6c47a-113">The **API gateway** is the endpoint that:</span></span>
  
  * <span data-ttu-id="6c47a-114">API çağrılarını kabul eder ve bunları arka uçlarınıza yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="6c47a-114">Accepts API calls and routes them to your backends.</span></span>
  * <span data-ttu-id="6c47a-115">API anahtarları, JWT belirteçleri, sertifikaları ve diğer kimlik bilgilerini doğrular.</span><span class="sxs-lookup"><span data-stu-id="6c47a-115">Verifies API keys, JWT tokens, certificates, and other credentials.</span></span>
  * <span data-ttu-id="6c47a-116">Kullanım kotalarını ve oran limitlerini uygular.</span><span class="sxs-lookup"><span data-stu-id="6c47a-116">Enforces usage quotas and rate limits.</span></span>
  * <span data-ttu-id="6c47a-117">Kod değişiklikleri olmadan API'nizi anında dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="6c47a-117">Transforms your API on the fly without code modifications.</span></span>
  * <span data-ttu-id="6c47a-118">Ayarlandığında arka uç yanıtlarını önbelleğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="6c47a-118">Caches backend responses where set up.</span></span>
  * <span data-ttu-id="6c47a-119">Analiz amaçlı çağrı meta verilerini günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="6c47a-119">Logs call metadata for analytics purposes.</span></span>
* <span data-ttu-id="6c47a-120">**Yayımcı portalı** API programınızı ayarladığınız yönetim arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="6c47a-120">The **publisher portal** is the administrative interface where you set up your API program.</span></span> <span data-ttu-id="6c47a-121">Bunu şunlar için kullanın:</span><span class="sxs-lookup"><span data-stu-id="6c47a-121">Use it to:</span></span>
  
  * <span data-ttu-id="6c47a-122">API şeması tanımlama ya da içeri aktarma.</span><span class="sxs-lookup"><span data-stu-id="6c47a-122">Define or import API schema.</span></span>
  * <span data-ttu-id="6c47a-123">API'leri ürünler halinde paketleme.</span><span class="sxs-lookup"><span data-stu-id="6c47a-123">Package APIs into products.</span></span>
  * <span data-ttu-id="6c47a-124">API’lerde kota veya dönüşüm gibi ilkeler ayarlama.</span><span class="sxs-lookup"><span data-stu-id="6c47a-124">Set up policies like quotas or transformations on the APIs.</span></span>
  * <span data-ttu-id="6c47a-125">Analizlerden öngörüler edinme</span><span class="sxs-lookup"><span data-stu-id="6c47a-125">Get insights from analytics.</span></span>
  * <span data-ttu-id="6c47a-126">Kullanıcıları yönetme.</span><span class="sxs-lookup"><span data-stu-id="6c47a-126">Manage users.</span></span>
* <span data-ttu-id="6c47a-127">**Geliştirici portalı**, geliştiricilerin şunları yapabileceği ana web varlığı görevi görür:</span><span class="sxs-lookup"><span data-stu-id="6c47a-127">The **developer portal** serves as the main web presence for developers, where they can:</span></span>
  
  * <span data-ttu-id="6c47a-128">API belgelerini okuma.</span><span class="sxs-lookup"><span data-stu-id="6c47a-128">Read API documentation.</span></span>
  * <span data-ttu-id="6c47a-129">Etkileşimli konsol üzerinden bir API’yi deneme.</span><span class="sxs-lookup"><span data-stu-id="6c47a-129">Try out an API via the interactive console.</span></span>
  * <span data-ttu-id="6c47a-130">Bir hesap oluşturma ve API anahtarlarını almak için abone olma.</span><span class="sxs-lookup"><span data-stu-id="6c47a-130">Create an account and subscribe to get API keys.</span></span>
  * <span data-ttu-id="6c47a-131">Kendi kullanımlarına ilişkin analize erişme.</span><span class="sxs-lookup"><span data-stu-id="6c47a-131">Access analytics on their own usage.</span></span>

## <span data-ttu-id="6c47a-132"><a name="create-service-instance"> </a>API Management örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="6c47a-132"><a name="create-service-instance"> </a>Create an API Management instance</span></span>
> [!NOTE]
> <span data-ttu-id="6c47a-133">Bu öğreticiyi tamamlamak için bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6c47a-133">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="6c47a-134">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c47a-134">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="6c47a-135">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][Azure Free Trial].</span><span class="sxs-lookup"><span data-stu-id="6c47a-135">For details, see [Azure Free Trial][Azure Free Trial].</span></span>
> 
> 

<span data-ttu-id="6c47a-136">API Management ile çalışmanın ilk adımı bir hizmet örneği oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="6c47a-136">The first step in working with API Management is to create a service instance.</span></span> <span data-ttu-id="6c47a-137">[Azure Portal][Azure Portal]'da oturum açın ve **Yeni**, **Web + Mobil**, **API Management**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6c47a-137">Sign in to the [Azure Portal][Azure Portal] and click **New**, **Web + Mobile**, **API Management**.</span></span>

![Yeni API Management örneği][api-management-create-instance-menu]

<span data-ttu-id="6c47a-139">**Ad** alanında hizmet URL'si için kullanılacak benzersiz bir alt etki alanı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="6c47a-139">For **Name**, specify a unique sub-domain name to use for the service URL.</span></span>

<span data-ttu-id="6c47a-140">Hizmet örneğiniz için istediğiniz **Abonelik**, **Kaynak grubu** ve **Konum** seçeneklerini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="6c47a-140">Choose the desired **Subscription**, **Resource group** and **Location** for your service instance.</span></span>

<span data-ttu-id="6c47a-141">**Contoso Ltd.**’yi</span><span class="sxs-lookup"><span data-stu-id="6c47a-141">Enter **Contoso Ltd.**</span></span> <span data-ttu-id="6c47a-142">**Kuruluş Adı** olarak girin ve e-posta adresinizi **Yönetici E-postası** alanına girin.</span><span class="sxs-lookup"><span data-stu-id="6c47a-142">for the **Organization Name**, and enter your email address in the **Administrator E-Mail** field.</span></span>

> [!NOTE]
> <span data-ttu-id="6c47a-143">Bu e-posta adresi API Management sisteminden gelen bildirimler için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6c47a-143">This email address is used for notifications from the API Management system.</span></span> <span data-ttu-id="6c47a-144">Daha fazla bilgi için bkz. [Azure API Management'te bildirimleri ve e-posta şablonlarını yapılandırma][How to configure notifications and email templates in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="6c47a-144">For more information, see [How to configure notifications and email templates in Azure API Management][How to configure notifications and email templates in Azure API Management].</span></span>
> 
> 

![Yeni API Management hizmeti][api-management-create-instance-step1]

<span data-ttu-id="6c47a-146">API Management hizmeti örnekleri üç katmanda kullanılabilir: Geliştirici, Standart ve Premium.</span><span class="sxs-lookup"><span data-stu-id="6c47a-146">API Management service instances are available in three tiers: Developer, Standard, and Premium.</span></span>

> [!NOTE]
> <span data-ttu-id="6c47a-147">Geliştirici Katmanı; geliştirme, test ve yüksek kullanılabilirliğin gerekli görülmediği pilot API programları içindir.</span><span class="sxs-lookup"><span data-stu-id="6c47a-147">The Developer Tier is for development, testing, and pilot API programs where high availability is not a concern.</span></span> <span data-ttu-id="6c47a-148">Standart ve Premium katmanlarda, daha fazla trafik işlemek için ayrılmış birim sayınızı ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c47a-148">In the Standard and Premium tiers, you can scale your reserved unit count to handle more traffic.</span></span> <span data-ttu-id="6c47a-149">Standart ve Premium katmanlar, API Management hizmetinize en fazla işlem gücü ve performans sağlar.</span><span class="sxs-lookup"><span data-stu-id="6c47a-149">The Standard and Premium tiers provide your API Management service with the most processing power and performance.</span></span> <span data-ttu-id="6c47a-150">Bu öğreticiyi herhangi bir katmanı kullanarak tamamlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c47a-150">You can complete this tutorial by using any tier.</span></span> <span data-ttu-id="6c47a-151">API Management katmanları hakkında daha fazla bilgi için bkz. [API Management fiyatlandırması][API Management pricing].</span><span class="sxs-lookup"><span data-stu-id="6c47a-151">For more information about API Management tiers, see [API Management pricing][API Management pricing].</span></span>
> 
> 

<span data-ttu-id="6c47a-152">Hizmet örneğinizi sağlamaya başlamak için **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6c47a-152">Click **Create** to start provisioning your service instance.</span></span>

![Yeni API Management hizmeti][api-management-instance-created]

<span data-ttu-id="6c47a-154">Hizmet örneği oluşturulduktan sonra bir API oluşturmak ya da içeri aktarmak sonraki adımdır.</span><span class="sxs-lookup"><span data-stu-id="6c47a-154">Once the service instance is created, the next step is to create or import an API.</span></span>

## <span data-ttu-id="6c47a-155"><a name="create-api"> </a>Bir API'yi içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="6c47a-155"><a name="create-api"> </a>Import an API</span></span>
<span data-ttu-id="6c47a-156">Bir API, istemci uygulamasından çağrılabilen işlemler grubundan oluşur.</span><span class="sxs-lookup"><span data-stu-id="6c47a-156">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="6c47a-157">API işlemleri mevcut web hizmetlerine taşınır.</span><span class="sxs-lookup"><span data-stu-id="6c47a-157">API operations are proxied to existing web services.</span></span>

<span data-ttu-id="6c47a-158">API'ler el ile oluşturulabilir (ve API’lere işlem eklenebilir) veya içeri aktarılabilir.</span><span class="sxs-lookup"><span data-stu-id="6c47a-158">APIs can be created (and operations can be added) manually, or they can be imported.</span></span> <span data-ttu-id="6c47a-159">Bu öğreticide, Microsoft tarafından sağlanan ve Azure üzerinde barındırılan bir örnek hesaplayıcı web hizmeti için API’yi içeri aktaracağız.</span><span class="sxs-lookup"><span data-stu-id="6c47a-159">In this tutorial, we will import the API for a sample calculator web service provided by Microsoft and hosted on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="6c47a-160">API oluşturma ve işlemleri el ile ekleme yönergeleri için bkz. [API oluşturma](api-management-howto-create-apis.md) ve [API’ye işlem ekleme](api-management-howto-add-operations.md).</span><span class="sxs-lookup"><span data-stu-id="6c47a-160">For guidance on creating an API and manually adding operations, see [How to create APIs](api-management-howto-create-apis.md) and [How to add operations to an API](api-management-howto-add-operations.md).</span></span>
> 
> 

<span data-ttu-id="6c47a-161">API’ler yayımcı portalından yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="6c47a-161">APIs are configured from the publisher portal.</span></span> <span data-ttu-id="6c47a-162">Ulaşmak için hizmet araç çubuğundan **Yayımcı portalı**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6c47a-162">To reach it, click **Publisher portal** from the service toolbar.</span></span>

![Yayımcı portalı][api-management-management-console]

<span data-ttu-id="6c47a-164">Hesaplayıcı API’sini içeri aktarmak için, soldaki **API Management** menüsünde **API'ler**’e tıklayın ve ardından **API’yi İçeri Aktar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6c47a-164">To import the calculator API, click **APIs** from the **API Management** menu on the left, and then click **Import API**.</span></span>

![API’yi İçeri Aktar düğmesi][api-management-import-api]

<span data-ttu-id="6c47a-166">Hesaplayıcı API’sini yapılandırmak için aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="6c47a-166">Perform the following steps to configure the calculator API:</span></span>

1. <span data-ttu-id="6c47a-167">**Kaynak URL**’ye tıklayın, **Belirtim belgesi URL’si** metin kutusuna **http://calcapi.cloudapp.net/calcapi.json** girin ve **Swagger** radyo düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6c47a-167">Click **From URL**, enter **http://calcapi.cloudapp.net/calcapi.json** into the **Specification document URL** text box, and click the **Swagger** radio button.</span></span>
2. <span data-ttu-id="6c47a-168">**Web API’si URL soneki** metin kutusuna **calc** yazın. </span><span class="sxs-lookup"><span data-stu-id="6c47a-168">Type **calc** into the **Web API URL suffix** text box.</span></span>
3. <span data-ttu-id="6c47a-169">**Ürünler (isteğe bağlı)** öğesine tıklayın ve **Starter**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="6c47a-169">Click in the **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="6c47a-170">API’yi içeri aktarmak için **Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6c47a-170">Click **Save** to import the API.</span></span>

![Yeni API ekle][api-management-import-new-api]

> [!NOTE]
> <span data-ttu-id="6c47a-172">**API Management** şu anda içeri aktarma için Swagger belgesinin 1.2 ve 2.0 sürümünü destekler.</span><span class="sxs-lookup"><span data-stu-id="6c47a-172">**API Management** currently supports both 1.2 and 2.0 version of Swagger document for import.</span></span> <span data-ttu-id="6c47a-173">[Swagger 2.0 belirtimi](http://swagger.io/specification) `host`, `basePath` ve `schemes` özelliklerinin isteğe bağlı olduğunu belirtse dahi, Swagger 2.0 belgeniz bu özellikleri **İÇERMELİDİR**; aksi takdirde içeri aktarılmaz.</span><span class="sxs-lookup"><span data-stu-id="6c47a-173">Make sure that, even though [Swagger 2.0 specification](http://swagger.io/specification) declares that `host`, `basePath`, and `schemes` properties are optional, your Swagger 2.0 document **MUST** contain those properties; otherwise it won't get imported.</span></span> 
> 
> 

<span data-ttu-id="6c47a-174">API içeri aktarıldığında, yayımcı portalında API’nin özet sayfası gösterilir.</span><span class="sxs-lookup"><span data-stu-id="6c47a-174">Once the API is imported, the summary page for the API is displayed in the publisher portal.</span></span>

![API özeti][api-management-imported-api-summary]

<span data-ttu-id="6c47a-176">API bölümünde birden çok sekme bulunur.</span><span class="sxs-lookup"><span data-stu-id="6c47a-176">The API section has several tabs.</span></span> <span data-ttu-id="6c47a-177">**Özet** sekmesi, API hakkında temel ölçümleri ve bilgileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="6c47a-177">The **Summary** tab displays basic metrics and information about the API.</span></span> <span data-ttu-id="6c47a-178">[Ayarlar](api-management-howto-create-apis.md#configure-api-settings) sekmesi, API yapılandırmasını görüntülemek ve düzenlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6c47a-178">The [Settings](api-management-howto-create-apis.md#configure-api-settings) tab is used to view and edit the configuration for an API.</span></span> <span data-ttu-id="6c47a-179">[İşlemler](api-management-howto-add-operations.md) sekmesi, API işlemlerini yönetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6c47a-179">The [Operations](api-management-howto-add-operations.md) tab is used to manage the API's operations.</span></span> <span data-ttu-id="6c47a-180">**Güvenlik** sekmesi, Temel kimlik doğrulaması ya da [karşılıklı sertifika kimlik doğrulaması](api-management-howto-mutual-certificates.md) kullanarak arka uç sunucusu için ağ geçidi kimlik doğrulamasını yapılandırmak ve [OAuth 2.0 kullanarak kullanıcı kimlik doğrulamasını](api-management-howto-oauth2.md) yapılandırmak üzere kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6c47a-180">The **Security** tab can be used to configure gateway authentication for the backend server by using Basic authentication or [mutual certificate authentication](api-management-howto-mutual-certificates.md), and to configure [user authorization by using OAuth 2.0](api-management-howto-oauth2.md).</span></span>  <span data-ttu-id="6c47a-181">**Sorunlar** sekmesi, API'lerinizi kullanan geliştiriciler tarafından bildirilen sorunları görüntülemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6c47a-181">The **Issues** tab is used to view issues reported by the developers who are using your APIs.</span></span> <span data-ttu-id="6c47a-182">**Ürünler** sekmesi bu API’yi içeren ürünleri yapılandırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6c47a-182">The **Products** tab is used to configure the products that contain this API.</span></span>

<span data-ttu-id="6c47a-183">Varsayılan olarak, her bir API Management örneği iki örnek ürün ile birlikte gelir:</span><span class="sxs-lookup"><span data-stu-id="6c47a-183">By default, each API Management instance comes with two sample products:</span></span>

* <span data-ttu-id="6c47a-184">**Başlangıç**</span><span class="sxs-lookup"><span data-stu-id="6c47a-184">**Starter**</span></span>
* <span data-ttu-id="6c47a-185">**Sınırsız**</span><span class="sxs-lookup"><span data-stu-id="6c47a-185">**Unlimited**</span></span>

<span data-ttu-id="6c47a-186">Bu öğreticide, API içeri aktarılırken Başlangıç ürününe Temel Hesaplayıcı API’si eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="6c47a-186">In this tutorial, the Basic Calculator API was added to the Starter product when the API was imported.</span></span>

<span data-ttu-id="6c47a-187">Bir API’ye çağrı yapmak için, geliştiricilerin önce buna erişim imkanı sağlayan bir ürüne abone olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6c47a-187">In order to make calls to an API, developers must first subscribe to a product that gives them access to it.</span></span> <span data-ttu-id="6c47a-188">Geliştiriciler geliştirici portalında ürünlere abone olabilir ya da yöneticiler geliştiricileri yayım portalında ürünlere abone yapabilir.</span><span class="sxs-lookup"><span data-stu-id="6c47a-188">Developers can subscribe to products in the developer portal, or administrators can subscribe developers to products in the publisher portal.</span></span> <span data-ttu-id="6c47a-189">Öğreticinin önceki adımlarında API Management örneği oluşturduğunuz için siz bir yöneticisiniz, bu nedenle varsayılan olarak her ürüne zaten abone oldunuz.</span><span class="sxs-lookup"><span data-stu-id="6c47a-189">You are an administrator since you created the API Management instance in the previous steps in the tutorial, so you are already subscribed to every product by default.</span></span>

## <span data-ttu-id="6c47a-190"><a name="call-operation"> </a>Geliştirici portalından işlem çağırma</span><span class="sxs-lookup"><span data-stu-id="6c47a-190"><a name="call-operation"> </a>Call an operation from the developer portal</span></span>
<span data-ttu-id="6c47a-191">İşlemler doğrudan bir API’nin işlemlerini görüntülemek ve test etmek için kullanışlı bir yol sağlayan geliştirici portalından çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="6c47a-191">Operations can be called directly from the developer portal, which provides a convenient way to view and test the operations of an API.</span></span> <span data-ttu-id="6c47a-192">Bu öğretici adımında, Temel Hesaplayıcı API’sinin **İki tamsayı ekle** işlemini çağıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="6c47a-192">In this tutorial step, you will call the Basic Calculator API's **Add two integers** operation.</span></span> <span data-ttu-id="6c47a-193">Yayımcı portalının sağ üst kısmında **Geliştirici Portalı**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6c47a-193">Click **Developer portal** from the menu at the top right of the publisher portal.</span></span>

![Geliştirici portalı][api-management-developer-portal-menu]

<span data-ttu-id="6c47a-195">Üstteki menüde **API'ler**’e tıklayın ve ardından kullanılabilir tüm işlemleri görmek için **Temel Hesaplayıcı**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6c47a-195">Click **APIs** from the top menu, and then click **Basic Calculator** to see the available operations.</span></span>

![Geliştirici portalı][api-management-developer-portal-calc-api]

<span data-ttu-id="6c47a-197">Bu işlemi kullanacak geliştiriciler için belgeleri sağlayarak, API ve işlemlerle birlikte, içeri aktarılan örnek açıklamalarını ve parametrelerini not edin.</span><span class="sxs-lookup"><span data-stu-id="6c47a-197">Note the sample descriptions and parameters that were imported along with the API and operations, providing documentation for the developers that will use this operation.</span></span> <span data-ttu-id="6c47a-198">İşlemler el ile eklendiğinde de bu açıklamalar eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="6c47a-198">These descriptions can also be added when operations are added manually.</span></span>

<span data-ttu-id="6c47a-199">**İki tamsayı ekle** işlemini çağırmak için **Deneyin**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6c47a-199">To call the **Add two integers** operation, click **Try it**.</span></span>

![Deneyin][api-management-developer-portal-calc-api-console]

<span data-ttu-id="6c47a-201">Parametreler için bazı değerler girebilir veya varsayılanları tutabilirsiniz, sonra **Gönder**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6c47a-201">You can enter some values for the parameters or keep the defaults, and then click **Send**.</span></span>

![HTTP Al][api-management-invoke-get]

<span data-ttu-id="6c47a-203">Bir işlem çağrıldıktan sonra, geliştirici portalı **Yanıt durumu**, **Yanıt üst ilgileri** ve tüm **Yanıt içeriğini** gösterir.</span><span class="sxs-lookup"><span data-stu-id="6c47a-203">After an operation is invoked, the developer portal displays the **Response status**, the **Response headers**, and any **Response content**.</span></span>

![Yanıt][api-management-invoke-get-response]

## <span data-ttu-id="6c47a-205"><a name="view-analytics">.</a>Analizi görüntüleme</span><span class="sxs-lookup"><span data-stu-id="6c47a-205"><a name="view-analytics"> </a>View analytics</span></span>
<span data-ttu-id="6c47a-206">Temel Hesaplayıcı için analizleri görüntülemek üzere, geliştirici portalının sağ üst kısmındaki menüde **Yönet**’i seçerek yayımcı portalına geri dönün.</span><span class="sxs-lookup"><span data-stu-id="6c47a-206">To view analytics for Basic Calculator, switch back to the publisher portal by selecting **Manage** from the menu at the top right of the developer portal.</span></span>

![Yönet][api-management-manage-menu]

<span data-ttu-id="6c47a-208">Yayımcı portalı için varsayılan görünüm, API Management örneğinize genel bakış sağlayan **Pano**’dur.</span><span class="sxs-lookup"><span data-stu-id="6c47a-208">The default view for the publisher portal is the **Dashboard**, which provides an overview of your API Management instance.</span></span>

![Pano][api-management-dashboard]

<span data-ttu-id="6c47a-210">Belirli bir süre için API’nin kullanımına ilişkin belirli ölçümleri görüntülemek üzere fareyi **Temel Hesaplayıcı** grafiğinin üzerine getirin.</span><span class="sxs-lookup"><span data-stu-id="6c47a-210">Hover the mouse over the chart for **Basic Calculator** to see the specific metrics for the usage of the API for a given time period.</span></span>

> [!NOTE]
> <span data-ttu-id="6c47a-211">Grafiğinizde satır görmüyorsanız, geliştirici portalına dönün ve API’ye bazı çağrılar yapın, birkaç dakika bekleyip panoya geri dönün.</span><span class="sxs-lookup"><span data-stu-id="6c47a-211">If you don't see any lines on your chart, switch back to the developer portal and make some calls into the API, wait a few moments, and then come back to the dashboard.</span></span>
> 
> 

<span data-ttu-id="6c47a-212">Görüntülenen ölçümlerin daha büyük bir sürümü dahil olmak üzere API için özet sayfasını görüntülemek isterseniz **Ayrıntıları Görüntüle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6c47a-212">Click **View Details** to view the summary page for the API, including a larger version of the displayed metrics.</span></span>

![Analiz][api-management-mouse-over]

![Özet][api-management-api-summary-metrics]

<span data-ttu-id="6c47a-215">Ayrıntılı ölçümler ve raporlar için soldaki **API Management** menüsünde **Analiz**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="6c47a-215">For detailed metrics and reports, click **Analytics** from the **API Management** menu on the left.</span></span>

![Genel Bakış][api-management-analytics-overview]

<span data-ttu-id="6c47a-217">**Analiz** bölümünde aşağıdaki dört sekme yer alır:</span><span class="sxs-lookup"><span data-stu-id="6c47a-217">The **Analytics** section has the following four tabs:</span></span>

* <span data-ttu-id="6c47a-218">**Bir bakışta** sekmesi genel kullanım ve durum ölçümlerinin yanı sıra en iyi geliştiriciler, en iyi ürünler, sık kullanılan API'ler ve sık kullanılan işlemleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="6c47a-218">**At a glance** provides overall usage and health metrics, as well as the top developers, top products, top APIs, and top operations.</span></span>
* <span data-ttu-id="6c47a-219">**Kullanım** sekmesi coğrafi bir temsil dahil olmak üzere API çağrıları ve bant genişliğine ilişkin ayrıntılı bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="6c47a-219">**Usage** provides an in-depth look at API calls and bandwidth, including a geographical representation.</span></span>
* <span data-ttu-id="6c47a-220">**Durum**sekmesi durum kodları, önbellek başarı oranları, yanıt zamanları ve API ve hizmet yanıt zamanlarına odaklanır.</span><span class="sxs-lookup"><span data-stu-id="6c47a-220">**Health** focuses on status codes, cache success rates, response times, and API and service response times.</span></span>
* <span data-ttu-id="6c47a-221">**Etkinlik**sekmesi geliştirici, ürün, API ve işleme göre belirli bir etkinliğe ilişkin ayrıntılı raporlar sunar.</span><span class="sxs-lookup"><span data-stu-id="6c47a-221">**Activity** provides reports that drill down on the specific activity by developer, product, API, and operation.</span></span>

## <span data-ttu-id="6c47a-222"><a name="next-steps"> </a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6c47a-222"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="6c47a-223">[Oran limitleri ile API’nizi koruma](api-management-howto-product-with-rules.md) hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="6c47a-223">Learn how to [Protect your API with rate limits](api-management-howto-product-with-rules.md).</span></span>

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add the new API to a product]: #add-api-to-product
[Subscribe to the product that contains the API]: #subscribe
[Call an operation from the Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How to manage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How to configure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md
[API Management pricing]: http://azure.microsoft.com/pricing/details/api-management/

[Azure Portal]: https://portal.azure.com/

[api-management-management-console]: ./media/api-management-get-started/api-management-management-console.png
[api-management-create-instance-menu]: ./media/api-management-get-started/api-management-create-instance-menu.png
[api-management-create-instance-step1]: ./media/api-management-get-started/api-management-create-instance-step1.png
[api-management-create-instance-step2]: ./media/api-management-get-started/api-management-create-instance-step2.png
[api-management-instance-created]: ./media/api-management-get-started/api-management-instance-created.png
[api-management-import-api]: ./media/api-management-get-started/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-get-started/api-management-import-new-api.png
[api-management-imported-api-summary]: ./media/api-management-get-started/api-management-imported-api-summary.png
[api-management-calc-operations]: ./media/api-management-get-started/api-management-calc-operations.png
[api-management-list-products]: ./media/api-management-get-started/api-management-list-products.png
[api-management-add-api-to-product]: ./media/api-management-get-started/api-management-add-api-to-product.png
[api-management-add-myechoapi-to-product]: ./media/api-management-get-started/api-management-add-myechoapi-to-product.png
[api-management-api-added-to-product]: ./media/api-management-get-started/api-management-api-added-to-product.png
[api-management-developers]: ./media/api-management-get-started/api-management-developers.png
[api-management-add-subscription]: ./media/api-management-get-started/api-management-add-subscription.png
[api-management-add-subscription-window]: ./media/api-management-get-started/api-management-add-subscription-window.png
[api-management-subscription-added]: ./media/api-management-get-started/api-management-subscription-added.png
[api-management-developer-portal-menu]: ./media/api-management-get-started/api-management-developer-portal-menu.png
[api-management-developer-portal-calc-api]: ./media/api-management-get-started/api-management-developer-portal-calc-api.png
[api-management-developer-portal-calc-api-console]: ./media/api-management-get-started/api-management-developer-portal-calc-api-console.png
[api-management-invoke-get]: ./media/api-management-get-started/api-management-invoke-get.png
[api-management-invoke-get-response]: ./media/api-management-get-started/api-management-invoke-get-response.png
[api-management-manage-menu]: ./media/api-management-get-started/api-management-manage-menu.png
[api-management-dashboard]: ./media/api-management-get-started/api-management-dashboard.png

[api-management-add-response]: ./media/api-management-get-started/api-management-add-response.png
[api-management-add-response-window]: ./media/api-management-get-started/api-management-add-response-window.png
[api-management-developer-key]: ./media/api-management-get-started/api-management-developer-key.png
[api-management-mouse-over]: ./media/api-management-get-started/api-management-mouse-over.png
[api-management-api-summary-metrics]: ./media/api-management-get-started/api-management-api-summary-metrics.png
[api-management-analytics-overview]: ./media/api-management-get-started/api-management-analytics-overview.png
[api-management-analytics-usage]: ./media/api-management-get-started/api-management-analytics-usage.png
[api-management-]: ./media/api-management-get-started/api-management-.png
[api-management-]: ./media/api-management-get-started/api-management-.png
