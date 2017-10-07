---
title: aaaManage ilk API'nizi Azure API Management | Microsoft Docs
description: "Nasıl toocreate API'leri, işlemleri ekleyin ve API Management ile çalışmaya başlama öğrenin."
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
ms.openlocfilehash: 7d43f33aa359c4d1e605e9fb41e43d323ca6a777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a><span data-ttu-id="f460d-103">İlk API’nizi Azure API Management’te yönetme</span><span class="sxs-lookup"><span data-stu-id="f460d-103">Manage your first API in Azure API Management</span></span>
## <span data-ttu-id="f460d-104"><a name="overview"> </a>Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f460d-104"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="f460d-105">Bu kılavuz size nasıl tooquickly Azure API Management'i kullanmaya başlayacağınızı ve ilk API çağrınızı yapmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="f460d-105">This guide shows you how tooquickly get started in using Azure API Management and make your first API call.</span></span>

## <span data-ttu-id="f460d-106"><a name="concepts"> </a>Azure API Management nedir?</span><span class="sxs-lookup"><span data-stu-id="f460d-106"><a name="concepts"> </a>What is Azure API Management?</span></span>
<span data-ttu-id="f460d-107">Azure API Management tootake herhangi bir arka uçtan kullanın ve temel alan tam özellikli bir API programını başlatın.</span><span class="sxs-lookup"><span data-stu-id="f460d-107">You can use Azure API Management tootake any backend and launch a full-fledged API program based on it.</span></span>

<span data-ttu-id="f460d-108">Yaygın senaryolar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f460d-108">Common scenarios include:</span></span>

* <span data-ttu-id="f460d-109">**Mobil altyapıyı koruma**: API anahtarlarına erişim geçişi sağlayarak, azaltma ile DOS saldırılarını önleyerek ya da JWT belirtecini doğrulama gibi gelişmiş güvenlik ilkelerini kullanarak mobil altyapıyı koruyun.</span><span class="sxs-lookup"><span data-stu-id="f460d-109">**Securing mobile infrastructure** by gating access with API keys, preventing DOS attacks by using throttling, or using advanced security policies like JWT token validation.</span></span>
* <span data-ttu-id="f460d-110">**ISV iş ortağı ekosistemlerini etkinleştirme** hello Geliştirici üzerinden hızlı iş ortağı ekleme sunarak portal ve API cephesi toodecouple dahili uygulamalardan gelen derleme iş ortağı kullanımı için hazır değil.</span><span class="sxs-lookup"><span data-stu-id="f460d-110">**Enabling ISV partner ecosystems** by offering fast partner onboarding through hello developer portal and building an API facade toodecouple from internal implementations that are not ripe for partner consumption.</span></span>
* <span data-ttu-id="f460d-111">**Bir dahili API programı çalıştırma** hello kuruluş toocommunicate hello kullanılabilirliği ve son hakkında tooAPIs değişiklikleri için merkezi bir konumda sunarak, Kurumsal hesaplar temelinde erişim geçişi sağlayarak tüm temel alarak arasında güvenli bir kanalı API ağ geçidi hello ve arka uç hello.</span><span class="sxs-lookup"><span data-stu-id="f460d-111">**Running an internal API program** by offering a centralized location for hello organization toocommunicate about hello availability and latest changes tooAPIs, gating access based on organizational accounts, all based on a secured channel between hello API gateway and hello backend.</span></span>

<span data-ttu-id="f460d-112">Merhaba sistem bileşenleri aşağıdaki Merhaba oluşur:</span><span class="sxs-lookup"><span data-stu-id="f460d-112">hello system is made up of hello following components:</span></span>

* <span data-ttu-id="f460d-113">Merhaba **API ağ geçidi** hello uç noktası:</span><span class="sxs-lookup"><span data-stu-id="f460d-113">hello **API gateway** is hello endpoint that:</span></span>
  
  * <span data-ttu-id="f460d-114">API çağrıları ve bunları tooyour arka uçlarını yönlendiren kabul eder.</span><span class="sxs-lookup"><span data-stu-id="f460d-114">Accepts API calls and routes them tooyour backends.</span></span>
  * <span data-ttu-id="f460d-115">API anahtarları, JWT belirteçleri, sertifikaları ve diğer kimlik bilgilerini doğrular.</span><span class="sxs-lookup"><span data-stu-id="f460d-115">Verifies API keys, JWT tokens, certificates, and other credentials.</span></span>
  * <span data-ttu-id="f460d-116">Kullanım kotalarını ve oran limitlerini uygular.</span><span class="sxs-lookup"><span data-stu-id="f460d-116">Enforces usage quotas and rate limits.</span></span>
  * <span data-ttu-id="f460d-117">Merhaba çalışma sırasında kod değişiklikleri olmadan API'nizi dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="f460d-117">Transforms your API on hello fly without code modifications.</span></span>
  * <span data-ttu-id="f460d-118">Ayarlandığında arka uç yanıtlarını önbelleğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="f460d-118">Caches backend responses where set up.</span></span>
  * <span data-ttu-id="f460d-119">Analiz amaçlı çağrı meta verilerini günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="f460d-119">Logs call metadata for analytics purposes.</span></span>
* <span data-ttu-id="f460d-120">Merhaba **yayımcı portalına** API programınızı ayarladığınız hello yönetim arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="f460d-120">hello **publisher portal** is hello administrative interface where you set up your API program.</span></span> <span data-ttu-id="f460d-121">Bunu şunlar için kullanın:</span><span class="sxs-lookup"><span data-stu-id="f460d-121">Use it to:</span></span>
  
  * <span data-ttu-id="f460d-122">API şeması tanımlama ya da içeri aktarma.</span><span class="sxs-lookup"><span data-stu-id="f460d-122">Define or import API schema.</span></span>
  * <span data-ttu-id="f460d-123">API'leri ürünler halinde paketleme.</span><span class="sxs-lookup"><span data-stu-id="f460d-123">Package APIs into products.</span></span>
  * <span data-ttu-id="f460d-124">Kota veya dönüşüm hello API'leri gibi ilkeleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f460d-124">Set up policies like quotas or transformations on hello APIs.</span></span>
  * <span data-ttu-id="f460d-125">Analizlerden öngörüler edinme</span><span class="sxs-lookup"><span data-stu-id="f460d-125">Get insights from analytics.</span></span>
  * <span data-ttu-id="f460d-126">Kullanıcıları yönetme.</span><span class="sxs-lookup"><span data-stu-id="f460d-126">Manage users.</span></span>
* <span data-ttu-id="f460d-127">Merhaba **Geliştirici Portalı** yapabileceği hello ana web varlığı görevi geliştiriciler için hizmet eder:</span><span class="sxs-lookup"><span data-stu-id="f460d-127">hello **developer portal** serves as hello main web presence for developers, where they can:</span></span>
  
  * <span data-ttu-id="f460d-128">API belgelerini okuma.</span><span class="sxs-lookup"><span data-stu-id="f460d-128">Read API documentation.</span></span>
  * <span data-ttu-id="f460d-129">Merhaba etkileşimli konsol üzerinden bir API'yi deneyin.</span><span class="sxs-lookup"><span data-stu-id="f460d-129">Try out an API via hello interactive console.</span></span>
  * <span data-ttu-id="f460d-130">Bir hesap oluşturun ve tooget API anahtarları abone olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f460d-130">Create an account and subscribe tooget API keys.</span></span>
  * <span data-ttu-id="f460d-131">Kendi kullanımlarına ilişkin analize erişme.</span><span class="sxs-lookup"><span data-stu-id="f460d-131">Access analytics on their own usage.</span></span>

## <span data-ttu-id="f460d-132"><a name="create-service-instance"> </a>API Management örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="f460d-132"><a name="create-service-instance"> </a>Create an API Management instance</span></span>
> [!NOTE]
> <span data-ttu-id="f460d-133">toocomplete Bu öğretici bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f460d-133">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="f460d-134">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f460d-134">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="f460d-135">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][Azure Free Trial].</span><span class="sxs-lookup"><span data-stu-id="f460d-135">For details, see [Azure Free Trial][Azure Free Trial].</span></span>
> 
> 

<span data-ttu-id="f460d-136">API Management ile çalışmanın hello ilk adımı toocreate bir hizmet örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f460d-136">hello first step in working with API Management is toocreate a service instance.</span></span> <span data-ttu-id="f460d-137">İçinde toohello oturum [Azure Portal] [ Azure Portal] tıklatıp **yeni**, **Web + mobil**, **API Management**.</span><span class="sxs-lookup"><span data-stu-id="f460d-137">Sign in toohello [Azure Portal][Azure Portal] and click **New**, **Web + Mobile**, **API Management**.</span></span>

![Yeni API Management örneği][api-management-create-instance-menu]

<span data-ttu-id="f460d-139">İçin **adı**, benzersiz bir alt etki alanı adı toouse hello hizmeti URL'sini belirtin.</span><span class="sxs-lookup"><span data-stu-id="f460d-139">For **Name**, specify a unique sub-domain name toouse for hello service URL.</span></span>

<span data-ttu-id="f460d-140">İstenen hello seçin **abonelik**, **kaynak grubu** ve **konumu** hizmet Örneğiniz için.</span><span class="sxs-lookup"><span data-stu-id="f460d-140">Choose hello desired **Subscription**, **Resource group** and **Location** for your service instance.</span></span>

<span data-ttu-id="f460d-141">Girin **Contoso Ltd.** hello için **kuruluş adı**ve e-posta adresinizi hello **yönetici e-posta** alan.</span><span class="sxs-lookup"><span data-stu-id="f460d-141">Enter **Contoso Ltd.** for hello **Organization Name**, and enter your email address in hello **Administrator E-Mail** field.</span></span>

> [!NOTE]
> <span data-ttu-id="f460d-142">Bu e-posta adresi hello API Management sisteminden gelen bildirimler için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f460d-142">This email address is used for notifications from hello API Management system.</span></span> <span data-ttu-id="f460d-143">Daha fazla bilgi için bkz: [nasıl tooconfigure bildirimleri ve e-posta şablonları Azure API Management'te][How tooconfigure notifications and email templates in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="f460d-143">For more information, see [How tooconfigure notifications and email templates in Azure API Management][How tooconfigure notifications and email templates in Azure API Management].</span></span>
> 
> 

![Yeni API Management hizmeti][api-management-create-instance-step1]

<span data-ttu-id="f460d-145">API Management hizmeti örnekleri üç katmanda kullanılabilir: Geliştirici, Standart ve Premium.</span><span class="sxs-lookup"><span data-stu-id="f460d-145">API Management service instances are available in three tiers: Developer, Standard, and Premium.</span></span>

> [!NOTE]
> <span data-ttu-id="f460d-146">Merhaba Geliştirici katmanı, geliştirme, test ve pilot API programları yüksek kullanılabilirlik ilgili bir sorun olduğu için ' dir.</span><span class="sxs-lookup"><span data-stu-id="f460d-146">hello Developer Tier is for development, testing, and pilot API programs where high availability is not a concern.</span></span> <span data-ttu-id="f460d-147">Merhaba standart ve Premium katmanlar, daha fazla trafik ayrılmış birim sayısı toohandle ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f460d-147">In hello Standard and Premium tiers, you can scale your reserved unit count toohandle more traffic.</span></span> <span data-ttu-id="f460d-148">Merhaba standart ve Premium katmanlar, API Management hizmeti ile Merhaba çoğu işlem gücü ve performans sağlar.</span><span class="sxs-lookup"><span data-stu-id="f460d-148">hello Standard and Premium tiers provide your API Management service with hello most processing power and performance.</span></span> <span data-ttu-id="f460d-149">Bu öğreticiyi herhangi bir katmanı kullanarak tamamlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f460d-149">You can complete this tutorial by using any tier.</span></span> <span data-ttu-id="f460d-150">API Management katmanları hakkında daha fazla bilgi için bkz. [API Management fiyatlandırması][API Management pricing].</span><span class="sxs-lookup"><span data-stu-id="f460d-150">For more information about API Management tiers, see [API Management pricing][API Management pricing].</span></span>
> 
> 

<span data-ttu-id="f460d-151">Tıklatın **oluşturma** toostart, hizmet örneği sağlama.</span><span class="sxs-lookup"><span data-stu-id="f460d-151">Click **Create** toostart provisioning your service instance.</span></span>

![Yeni API Management hizmeti][api-management-instance-created]

<span data-ttu-id="f460d-153">Merhaba hizmet örneği oluşturulduktan sonra hello sonraki adıma toocreate olduğunu veya bir API içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="f460d-153">Once hello service instance is created, hello next step is toocreate or import an API.</span></span>

## <span data-ttu-id="f460d-154"><a name="create-api"> </a>Bir API'yi içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="f460d-154"><a name="create-api"> </a>Import an API</span></span>
<span data-ttu-id="f460d-155">Bir API, istemci uygulamasından çağrılabilen işlemler grubundan oluşur.</span><span class="sxs-lookup"><span data-stu-id="f460d-155">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="f460d-156">API işlemleri yönlendirilirken tooexisting web hizmetleridir.</span><span class="sxs-lookup"><span data-stu-id="f460d-156">API operations are proxied tooexisting web services.</span></span>

<span data-ttu-id="f460d-157">API'ler el ile oluşturulabilir (ve API’lere işlem eklenebilir) veya içeri aktarılabilir.</span><span class="sxs-lookup"><span data-stu-id="f460d-157">APIs can be created (and operations can be added) manually, or they can be imported.</span></span> <span data-ttu-id="f460d-158">Bu öğreticide, size Microsoft tarafından sağlanan ve Azure üzerinde barındırılan bir örnek hesaplayıcı web hizmeti için API hello alacak.</span><span class="sxs-lookup"><span data-stu-id="f460d-158">In this tutorial, we will import hello API for a sample calculator web service provided by Microsoft and hosted on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="f460d-159">API oluşturma ve işlemleri el ile ekleme hakkında yönergeler için bkz [nasıl toocreate API'leri](api-management-howto-create-apis.md) ve [nasıl tooadd işlemleri tooan API](api-management-howto-add-operations.md).</span><span class="sxs-lookup"><span data-stu-id="f460d-159">For guidance on creating an API and manually adding operations, see [How toocreate APIs](api-management-howto-create-apis.md) and [How tooadd operations tooan API](api-management-howto-add-operations.md).</span></span>
> 
> 

<span data-ttu-id="f460d-160">API hello yayımcı Portalı'ndan yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="f460d-160">APIs are configured from hello publisher portal.</span></span> <span data-ttu-id="f460d-161">tooreach, tıklatın **yayımcı portalına** hello hizmet araç çubuğundan.</span><span class="sxs-lookup"><span data-stu-id="f460d-161">tooreach it, click **Publisher portal** from hello service toolbar.</span></span>

![Yayımcı portalı][api-management-management-console]

<span data-ttu-id="f460d-163">tooimport hello hesaplayıcı API'sini, tıklatın **API'leri** hello gelen **API Management** sol hello ve ardından menüsünde **içeri aktarma API'si**.</span><span class="sxs-lookup"><span data-stu-id="f460d-163">tooimport hello calculator API, click **APIs** from hello **API Management** menu on hello left, and then click **Import API**.</span></span>

![API’yi İçeri Aktar düğmesi][api-management-import-api]

<span data-ttu-id="f460d-165">Aşağıdaki adımları tooconfigure hello hesaplayıcı API'si hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f460d-165">Perform hello following steps tooconfigure hello calculator API:</span></span>

1. <span data-ttu-id="f460d-166">Tıklatın **URL'den**, girin **http://calcapi.cloudapp.net/calcapi.json** hello içine **belirtim belgesi URL'si** metin kutusuna ve hello tıklatın **Swagger**  radyo düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f460d-166">Click **From URL**, enter **http://calcapi.cloudapp.net/calcapi.json** into hello **Specification document URL** text box, and click hello **Swagger** radio button.</span></span>
2. <span data-ttu-id="f460d-167">Tür **calc** hello içine **Web API'si URL soneki** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="f460d-167">Type **calc** into hello **Web API URL suffix** text box.</span></span>
3. <span data-ttu-id="f460d-168">Tıklatın hello **ürünler (isteğe bağlı)** kutusuna ve seçin **Starter**.</span><span class="sxs-lookup"><span data-stu-id="f460d-168">Click in hello **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="f460d-169">Tıklatın **kaydetmek** tooimport hello API.</span><span class="sxs-lookup"><span data-stu-id="f460d-169">Click **Save** tooimport hello API.</span></span>

![Yeni API ekle][api-management-import-new-api]

> [!NOTE]
> <span data-ttu-id="f460d-171">**API Management** şu anda içeri aktarma için Swagger belgesinin 1.2 ve 2.0 sürümünü destekler.</span><span class="sxs-lookup"><span data-stu-id="f460d-171">**API Management** currently supports both 1.2 and 2.0 version of Swagger document for import.</span></span> <span data-ttu-id="f460d-172">[Swagger 2.0 belirtimi](http://swagger.io/specification) `host`, `basePath` ve `schemes` özelliklerinin isteğe bağlı olduğunu belirtse dahi, Swagger 2.0 belgeniz bu özellikleri **İÇERMELİDİR**; aksi takdirde içeri aktarılmaz.</span><span class="sxs-lookup"><span data-stu-id="f460d-172">Make sure that, even though [Swagger 2.0 specification](http://swagger.io/specification) declares that `host`, `basePath`, and `schemes` properties are optional, your Swagger 2.0 document **MUST** contain those properties; otherwise it won't get imported.</span></span> 
> 
> 

<span data-ttu-id="f460d-173">Merhaba API içeri aktarıldığında hello hello API için Özet sayfasında hello yayımcı Portalı'nda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f460d-173">Once hello API is imported, hello summary page for hello API is displayed in hello publisher portal.</span></span>

![API özeti][api-management-imported-api-summary]

<span data-ttu-id="f460d-175">Merhaba API bölümünde birden çok sekme bulunur.</span><span class="sxs-lookup"><span data-stu-id="f460d-175">hello API section has several tabs.</span></span> <span data-ttu-id="f460d-176">Merhaba **Özet** sekmesi, temel ölçümleri ve hello API hakkında bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f460d-176">hello **Summary** tab displays basic metrics and information about hello API.</span></span> <span data-ttu-id="f460d-177">Merhaba [ayarları](api-management-howto-create-apis.md#configure-api-settings) sekme kullanılan tooview ve düzenleme hello API yapılandırmasını kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f460d-177">hello [Settings](api-management-howto-create-apis.md#configure-api-settings) tab is used tooview and edit hello configuration for an API.</span></span> <span data-ttu-id="f460d-178">Merhaba [Operations](api-management-howto-add-operations.md) sekme kullanılan toomanage hello API'nin işlemlerini kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f460d-178">hello [Operations](api-management-howto-add-operations.md) tab is used toomanage hello API's operations.</span></span> <span data-ttu-id="f460d-179">Merhaba **güvenlik** sekmesi, temel kimlik doğrulaması kullanarak hello arka uç sunucusu için kullanılan tooconfigure Ağ Geçidi kimlik doğrulaması olabilir veya [karşılıklı sertifika kimlik doğrulaması](api-management-howto-mutual-certificates.md)ve tooconfigure [ OAuth 2.0 kullanarak kullanıcı kimlik doğrulaması](api-management-howto-oauth2.md).</span><span class="sxs-lookup"><span data-stu-id="f460d-179">hello **Security** tab can be used tooconfigure gateway authentication for hello backend server by using Basic authentication or [mutual certificate authentication](api-management-howto-mutual-certificates.md), and tooconfigure [user authorization by using OAuth 2.0](api-management-howto-oauth2.md).</span></span>  <span data-ttu-id="f460d-180">Merhaba **sorunları** sekmesi, Apı'lerinizi kullanan hello geliştiriciler tarafından bildirilen kullanılan tooview sorunları aynıdır.</span><span class="sxs-lookup"><span data-stu-id="f460d-180">hello **Issues** tab is used tooview issues reported by hello developers who are using your APIs.</span></span> <span data-ttu-id="f460d-181">Merhaba **ürünleri** sekmesi bu API'yi içeren kullanılan tooconfigure hello ürünleri aynıdır.</span><span class="sxs-lookup"><span data-stu-id="f460d-181">hello **Products** tab is used tooconfigure hello products that contain this API.</span></span>

<span data-ttu-id="f460d-182">Varsayılan olarak, her bir API Management örneği iki örnek ürün ile birlikte gelir:</span><span class="sxs-lookup"><span data-stu-id="f460d-182">By default, each API Management instance comes with two sample products:</span></span>

* <span data-ttu-id="f460d-183">**Başlangıç**</span><span class="sxs-lookup"><span data-stu-id="f460d-183">**Starter**</span></span>
* <span data-ttu-id="f460d-184">**Sınırsız**</span><span class="sxs-lookup"><span data-stu-id="f460d-184">**Unlimited**</span></span>

<span data-ttu-id="f460d-185">Merhaba API içeri aktarılırken Bu öğreticide, toohello Starter ürün hello temel hesaplayıcı API'si eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="f460d-185">In this tutorial, hello Basic Calculator API was added toohello Starter product when hello API was imported.</span></span>

<span data-ttu-id="f460d-186">Sipariş toomake çağrıları tooan API'si, geliştiricilerin önce erişim tooit verir tooa ürün abone olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="f460d-186">In order toomake calls tooan API, developers must first subscribe tooa product that gives them access tooit.</span></span> <span data-ttu-id="f460d-187">Geliştiriciler hello Geliştirici Portalı'nda tooproducts abone olabilir ya da yöneticiler geliştiricileri tooproducts hello yayımcı portalında abone olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f460d-187">Developers can subscribe tooproducts in hello developer portal, or administrators can subscribe developers tooproducts in hello publisher portal.</span></span> <span data-ttu-id="f460d-188">Zaten abone tooevery ürün varsayılan olacak şekilde hello API Management örneği hello önceki adımları hello öğreticide oluşturduğunuz olduğundan, bir yönetici demektir.</span><span class="sxs-lookup"><span data-stu-id="f460d-188">You are an administrator since you created hello API Management instance in hello previous steps in hello tutorial, so you are already subscribed tooevery product by default.</span></span>

## <span data-ttu-id="f460d-189"><a name="call-operation"></a>Hello Geliştirici portalından bir işlem çağırma</span><span class="sxs-lookup"><span data-stu-id="f460d-189"><a name="call-operation"> </a>Call an operation from hello developer portal</span></span>
<span data-ttu-id="f460d-190">İşlemler uygun şekilde tooview sağlayan doğrudan hello Geliştirici portalından çağrılabilir ve bir API'nin işlemlerini hello test edin.</span><span class="sxs-lookup"><span data-stu-id="f460d-190">Operations can be called directly from hello developer portal, which provides a convenient way tooview and test hello operations of an API.</span></span> <span data-ttu-id="f460d-191">Bu öğretici adımında hello temel hesaplayıcı API'SİNİN çağıracak **iki tamsayı Ekle** işlemi.</span><span class="sxs-lookup"><span data-stu-id="f460d-191">In this tutorial step, you will call hello Basic Calculator API's **Add two integers** operation.</span></span> <span data-ttu-id="f460d-192">Tıklatın **Geliştirici Portalı** hello hello menüden hello yayımcı portalının sağ üst.</span><span class="sxs-lookup"><span data-stu-id="f460d-192">Click **Developer portal** from hello menu at hello top right of hello publisher portal.</span></span>

![Geliştirici portalı][api-management-developer-portal-menu]

<span data-ttu-id="f460d-194">Tıklatın **API'leri** hello üst menüsünden ve ardından **temel hesaplayıcı** toosee hello kullanılabilir işlemleri.</span><span class="sxs-lookup"><span data-stu-id="f460d-194">Click **APIs** from hello top menu, and then click **Basic Calculator** toosee hello available operations.</span></span>

![Geliştirici portalı][api-management-developer-portal-calc-api]

<span data-ttu-id="f460d-196">Merhaba örnek açıklamalarını ve hello API ve bu işlemi kullanacak hello geliştiriciler için belgeleri sağlayarak işlemlerini birlikte aktarılan parametreleri unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f460d-196">Note hello sample descriptions and parameters that were imported along with hello API and operations, providing documentation for hello developers that will use this operation.</span></span> <span data-ttu-id="f460d-197">İşlemler el ile eklendiğinde de bu açıklamalar eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="f460d-197">These descriptions can also be added when operations are added manually.</span></span>

<span data-ttu-id="f460d-198">toocall hello **iki tamsayı Ekle** işlemi, tıklatın **deneyin**.</span><span class="sxs-lookup"><span data-stu-id="f460d-198">toocall hello **Add two integers** operation, click **Try it**.</span></span>

![Deneyin][api-management-developer-portal-calc-api-console]

<span data-ttu-id="f460d-200">Merhaba parametreler için bazı değerler girin veya hello Varsayılanları tutun ve ardından **Gönder**.</span><span class="sxs-lookup"><span data-stu-id="f460d-200">You can enter some values for hello parameters or keep hello defaults, and then click **Send**.</span></span>

![HTTP Al][api-management-invoke-get]

<span data-ttu-id="f460d-202">Bir işlem çağrıldıktan sonra hello Geliştirici Portalı hello görüntüler **yanıt durumu**, hello **yanıt üstbilgilerini**ve tüm **yanıt içeriği**.</span><span class="sxs-lookup"><span data-stu-id="f460d-202">After an operation is invoked, hello developer portal displays hello **Response status**, hello **Response headers**, and any **Response content**.</span></span>

![Yanıt][api-management-invoke-get-response]

## <span data-ttu-id="f460d-204"><a name="view-analytics">.</a>Analizi görüntüleme</span><span class="sxs-lookup"><span data-stu-id="f460d-204"><a name="view-analytics"> </a>View analytics</span></span>
<span data-ttu-id="f460d-205">Temel hesaplayıcı, anahtar seçerek yayımcı portalına geri toohello için tooview analiz **Yönet** hello hello menüden hello Geliştirici portalının sağ üst.</span><span class="sxs-lookup"><span data-stu-id="f460d-205">tooview analytics for Basic Calculator, switch back toohello publisher portal by selecting **Manage** from hello menu at hello top right of hello developer portal.</span></span>

![Yönet][api-management-manage-menu]

<span data-ttu-id="f460d-207">Merhaba hello yayımcı portalı için varsayılan görünüm olan hello **Pano**, API Management Örneğinize genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="f460d-207">hello default view for hello publisher portal is hello **Dashboard**, which provides an overview of your API Management instance.</span></span>

![Pano][api-management-dashboard]

<span data-ttu-id="f460d-209">Vurgulu hello fare hello grafiği için üzerinden **temel hesaplayıcı** toosee hello belirli ölçümleri belirli bir süre için API hello hello kullanımı.</span><span class="sxs-lookup"><span data-stu-id="f460d-209">Hover hello mouse over hello chart for **Basic Calculator** toosee hello specific metrics for hello usage of hello API for a given time period.</span></span>

> [!NOTE]
> <span data-ttu-id="f460d-210">Grafiğinizde grafiğinizde satır görmüyorsanız, geri toohello Geliştirici portalına geçin ve hello API bazı çağrılar yapın, birkaç dakika bekleyin ve toohello panoya geri dönün.</span><span class="sxs-lookup"><span data-stu-id="f460d-210">If you don't see any lines on your chart, switch back toohello developer portal and make some calls into hello API, wait a few moments, and then come back toohello dashboard.</span></span>
> 
> 

<span data-ttu-id="f460d-211">Tıklatın **ayrıntıları görüntüle** tooview hello Özet sayfası hello görüntülenen hello ölçümleri daha büyük bir sürümü de dahil olmak üzere API.</span><span class="sxs-lookup"><span data-stu-id="f460d-211">Click **View Details** tooview hello summary page for hello API, including a larger version of hello displayed metrics.</span></span>

![Analiz][api-management-mouse-over]

![Özet][api-management-api-summary-metrics]

<span data-ttu-id="f460d-214">Ayrıntılı Ölçümler ve raporlar için tıklatın **Analytics** hello gelen **API Management** hello sol menüsünde.</span><span class="sxs-lookup"><span data-stu-id="f460d-214">For detailed metrics and reports, click **Analytics** from hello **API Management** menu on hello left.</span></span>

![Genel Bakış][api-management-analytics-overview]

<span data-ttu-id="f460d-216">Merhaba **Analytics** bölümü aşağıdaki dört sekme hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="f460d-216">hello **Analytics** section has hello following four tabs:</span></span>

* <span data-ttu-id="f460d-217">**Bir bakışta** genel kullanım ve sistem durumu ölçümleri yanı sıra üst geliştiriciler, en iyi ürünler, sık kullanılan API'ler ve sık kullanılan işlemleri hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="f460d-217">**At a glance** provides overall usage and health metrics, as well as hello top developers, top products, top APIs, and top operations.</span></span>
* <span data-ttu-id="f460d-218">**Kullanım** sekmesi coğrafi bir temsil dahil olmak üzere API çağrıları ve bant genişliğine ilişkin ayrıntılı bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="f460d-218">**Usage** provides an in-depth look at API calls and bandwidth, including a geographical representation.</span></span>
* <span data-ttu-id="f460d-219">**Durum**sekmesi durum kodları, önbellek başarı oranları, yanıt zamanları ve API ve hizmet yanıt zamanlarına odaklanır.</span><span class="sxs-lookup"><span data-stu-id="f460d-219">**Health** focuses on status codes, cache success rates, response times, and API and service response times.</span></span>
* <span data-ttu-id="f460d-220">**Etkinlik** geliştirici, ürün, API ve işleme göre belirli etkinlik hello detaya raporlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="f460d-220">**Activity** provides reports that drill down on hello specific activity by developer, product, API, and operation.</span></span>

## <span data-ttu-id="f460d-221"><a name="next-steps"> </a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f460d-221"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="f460d-222">Nasıl çok öğrenin[API'nizi oran sınırları ile koruma](api-management-howto-product-with-rules.md).</span><span class="sxs-lookup"><span data-stu-id="f460d-222">Learn how too[Protect your API with rate limits](api-management-howto-product-with-rules.md).</span></span>

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add hello new API tooa product]: #add-api-to-product
[Subscribe toohello product that contains hello API]: #subscribe
[Call an operation from hello Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How toomanage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How tooconfigure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
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
