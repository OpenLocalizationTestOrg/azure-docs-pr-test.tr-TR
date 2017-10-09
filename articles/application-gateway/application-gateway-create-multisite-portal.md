---
title: "aaaHost Azure uygulama ağ geçidi ile birden çok sitesi | Microsoft Docs"
description: "Bu sayfa, hello birden çok web uygulamalarını barındırmak için mevcut bir Azure uygulama ağ geçidi yönergeleri tooconfigure sağlar hello Azure portal ile aynı ağ geçidi."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 95f892f6-fa27-47ee-b980-7abf4f2c66a9
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 2172aa2c80720f6f1ab7dd91745b44654bcaee00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="6d41b-103">Birden çok web uygulamalarını barındırmak için mevcut bir uygulama ağ geçidi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6d41b-103">Configure an existing application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6d41b-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="6d41b-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="6d41b-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d41b-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

<span data-ttu-id="6d41b-106">Birden çok siteyi barındıran bir web uygulaması'birden fazla toodeploy üzerinde hello sağlar aynı uygulama ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="6d41b-106">Multiple site hosting allows you toodeploy more than one web application on hello same application gateway.</span></span> <span data-ttu-id="6d41b-107">Ana bilgisayar üst bilgisi hello gelen HTTP isteği, hangi dinleyicisi trafiği alacağı toodetermine kullanır.</span><span class="sxs-lookup"><span data-stu-id="6d41b-107">It relies on presence of host header in hello incoming HTTP request, toodetermine which listener would receive traffic.</span></span> <span data-ttu-id="6d41b-108">Merhaba dinleyicisi sonra hello kuralları tanımı hello ağ geçidi içinde yapılandırıldığı gibi trafik tooappropriate arka uç havuzu yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="6d41b-108">hello listener then directs traffic tooappropriate backend pool as configured in hello rules definition of hello gateway.</span></span> <span data-ttu-id="6d41b-109">SSL etkin web uygulamaları, uygulama ağ geçidi hello sunucu adı göstergesi (SNI) uzantısı toochoose hello doğru dinleyicisi hello web trafiği için kullanır.</span><span class="sxs-lookup"><span data-stu-id="6d41b-109">In SSL enabled web applications, application gateway relies on hello Server Name Indication (SNI) extension toochoose hello correct listener for hello web traffic.</span></span> <span data-ttu-id="6d41b-110">Tooload bakiye istekleri farklı web etki alanları toodifferent arka uç sunucu havuzu için birden çok sitesi barındırmak için ortak bir kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6d41b-110">A common use for multiple site hosting is tooload balance requests for different web domains toodifferent back-end server pools.</span></span> <span data-ttu-id="6d41b-111">Benzer şekilde aynı kök etki alanı üzerinde de barındırılabilecek hello birden çok alt etki alanları aynı uygulama ağ geçidi hello.</span><span class="sxs-lookup"><span data-stu-id="6d41b-111">Similarly multiple subdomains of hello same root domain could also be hosted on hello same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="6d41b-112">Senaryo</span><span class="sxs-lookup"><span data-stu-id="6d41b-112">Scenario</span></span>

<span data-ttu-id="6d41b-113">Aşağıdaki örneğine hello iki arka uç sunucu havuzu ile trafiği contoso.com ve fabrikam.com için uygulama ağ geçidi hizmet: contoso sunucu havuzu ve fabrikam sunucu havuzu.</span><span class="sxs-lookup"><span data-stu-id="6d41b-113">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="6d41b-114">Benzer Kurulum app.contoso.com ve blog.contoso.com gibi kullanılan toohost alt etki alanları olabilir.</span><span class="sxs-lookup"><span data-stu-id="6d41b-114">Similar setup could be used toohost subdomains like app.contoso.com and blog.contoso.com.</span></span>

![çok siteli senaryosu][multisite]

## <a name="before-you-begin"></a><span data-ttu-id="6d41b-116">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="6d41b-116">Before you begin</span></span>

<span data-ttu-id="6d41b-117">Bu senaryo, çoklu site desteği tooan varolan uygulama ağ geçidi ekler.</span><span class="sxs-lookup"><span data-stu-id="6d41b-117">This scenario adds multi-site support tooan existing application gateway.</span></span> <span data-ttu-id="6d41b-118">toocomplete toobe kullanılabilir tooconfigure bu senaryo, var olan bir uygulama ağ geçidi gerekir.</span><span class="sxs-lookup"><span data-stu-id="6d41b-118">toocomplete this scenario, an existing application gateway needs toobe available tooconfigure.</span></span> <span data-ttu-id="6d41b-119">Ziyaret [hello portalı kullanarak bir uygulama ağ geçidi oluşturma](application-gateway-create-gateway-portal.md) toolearn nasıl toocreate hello portal temel uygulama ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="6d41b-119">Visit [Create an application gateway by using hello portal](application-gateway-create-gateway-portal.md) toolearn how toocreate a basic application gateway in hello portal.</span></span>

<span data-ttu-id="6d41b-120">Merhaba hello adımları tooupdate hello uygulama ağ geçidi gerekli şunlardır:</span><span class="sxs-lookup"><span data-stu-id="6d41b-120">hello following are hello steps needed tooupdate hello application gateway:</span></span>

1. <span data-ttu-id="6d41b-121">Her site için arka uç havuzları toouse oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6d41b-121">Create back-end pools toouse for each site.</span></span>
2. <span data-ttu-id="6d41b-122">Dinleyici oluşturmak için her site, uygulama ağ geçidi destekler.</span><span class="sxs-lookup"><span data-stu-id="6d41b-122">Create a listener for each site application gateway supports.</span></span>
3. <span data-ttu-id="6d41b-123">Kuralları toomap hello uygun arka uç ile her bir dinleyici oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6d41b-123">Create rules toomap each listener with hello appropriate back-end.</span></span>

## <a name="requirements"></a><span data-ttu-id="6d41b-124">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="6d41b-124">Requirements</span></span>

* <span data-ttu-id="6d41b-125">**Arka uç sunucusu havuzu:** hello hello arka uç sunucularının IP adresleri listesi.</span><span class="sxs-lookup"><span data-stu-id="6d41b-125">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="6d41b-126">listede hello IP adresleri ya da toohello sanal ağ alt veya ait genel IP/VIP'ye olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6d41b-126">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="6d41b-127">FQDN de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6d41b-127">FQDN can also be used.</span></span>
* <span data-ttu-id="6d41b-128">**Arka uç sunucu havuzu ayarları**: Her havuzun bağlantı noktası, protokol ve tanımlama bilgisi temelli benzeşim gibi ayarları vardır.</span><span class="sxs-lookup"><span data-stu-id="6d41b-128">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="6d41b-129">Bu ayarlar bağlı tooa olan havuzu ve hello havuz içindeki uygulanan tooall sunucularıdır.</span><span class="sxs-lookup"><span data-stu-id="6d41b-129">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="6d41b-130">**Ön uç bağlantı noktası:** Bu bağlantı noktası hello hello uygulama ağ geçidinde açılan genel bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="6d41b-130">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="6d41b-131">Bu bağlantı noktasında trafik trafik ve tooone hello arka uç sunucularının alır yeniden yönlendirildi.</span><span class="sxs-lookup"><span data-stu-id="6d41b-131">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="6d41b-132">**Dinleyici:** hello dinleyicisi sahip bir ön uç bağlantı noktası, bir protokol (Http veya Https, bu değerleri büyük küçük harfe duyarlı) ve hello SSL sertifika adı (SSL yük boşaltımı yapılandırılıyorsa).</span><span class="sxs-lookup"><span data-stu-id="6d41b-132">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="6d41b-133">Çok siteli kullanan bir uygulama ağ geçitleri için ana bilgisayar adı ve SNI göstergeleri de eklenir.</span><span class="sxs-lookup"><span data-stu-id="6d41b-133">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="6d41b-134">**Kural:** hello kural hello dinleyicisi, hello arka uç sunucusu havuzunu bağlar ve belli bir Dinleyicide trafik yönlendirilmiş toowhen hangi arka uç sunucu havuzu hello trafiğinin olmalıdır belirler.</span><span class="sxs-lookup"><span data-stu-id="6d41b-134">**Rule:** hello rule binds hello listener, hello back-end server pool, and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="6d41b-135">Kuralları listelendikleri hello sırada işlenir ve trafik belirginliğe bağımsız olarak eşleşen ilk kural hello aracılığıyla yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="6d41b-135">Rules are processed in hello order they are listed, and traffic will be directed via hello first rule that matches regardless of specificity.</span></span> <span data-ttu-id="6d41b-136">Temel bir dinleyici kullanan bir kural ve çok siteli dinleyicisi hem aynı bağlantı noktası, hello kuralla hello kullanarak bir kuralı varsa, örneğin, hello çok siteli dinleyicisi önce hello kural hello çok siteli kural toofunction sırayla hello temel dinleyicisiyle listelenmiş olması gerekir bekleniyordu.</span><span class="sxs-lookup"><span data-stu-id="6d41b-136">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on hello same port, hello rule with hello multi-site listener must be listed before hello rule with hello basic listener in order for hello multi-site rule toofunction as expected.</span></span> 
* <span data-ttu-id="6d41b-137">**Sertifikalar:** her dinleyicisi benzersiz bir sertifika gerektirir, bu örnekte 2 dinleyicileri için çok siteli oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6d41b-137">**Certificates:** Each listener requires a unique certificate, in this example 2 listeners are created for multi-site.</span></span> <span data-ttu-id="6d41b-138">İki .pfx sertifikaları ve bunları hello parolalarını oluşturulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="6d41b-138">Two .pfx certificates and hello passwords for them need toobe created.</span></span>

## <a name="create-back-end-pools-for-each-site"></a><span data-ttu-id="6d41b-139">Her site için arka uç havuzları oluşturma</span><span class="sxs-lookup"><span data-stu-id="6d41b-139">Create back-end pools for each site</span></span>

<span data-ttu-id="6d41b-140">Uygulama ağ geçidi destekler gerekirse, bu durumda 2 olması oluşturulur, contoso11.com için diğeri için fabrikam11.com her site için bir arka uç havuzu.</span><span class="sxs-lookup"><span data-stu-id="6d41b-140">A back-end pool for each site that application gateway supports is needed, in this case 2 are be created, one for contoso11.com and one for fabrikam11.com.</span></span>

### <a name="step-1"></a><span data-ttu-id="6d41b-141">1. Adım</span><span class="sxs-lookup"><span data-stu-id="6d41b-141">Step 1</span></span>

<span data-ttu-id="6d41b-142">Tooan varolan uygulama ağ geçidi hello Azure portal (https://portal.azure.com) gidin.</span><span class="sxs-lookup"><span data-stu-id="6d41b-142">Navigate tooan existing application gateway in hello Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="6d41b-143">Seçin **arka uç havuzları** tıklatıp **Ekle**</span><span class="sxs-lookup"><span data-stu-id="6d41b-143">Select **Backend pools** and click **Add**</span></span>

![arka uç havuzları ekleme][7]

### <a name="step-2"></a><span data-ttu-id="6d41b-145">2. Adım</span><span class="sxs-lookup"><span data-stu-id="6d41b-145">Step 2</span></span>

<span data-ttu-id="6d41b-146">Merhaba arka uç havuzu hello bilgileri doldurun **pool1**, başlangıç IP adresi veya FQDN hello arka uç sunucuları için ekleme ve tıklatın **Tamam**</span><span class="sxs-lookup"><span data-stu-id="6d41b-146">Fill in hello information for hello back-end pool **pool1**, adding hello ip addresses or FQDNs for hello back-end servers and click **OK**</span></span>

![arka uç havuzu pool1 ayarları][8]

### <a name="step-3"></a><span data-ttu-id="6d41b-148">3. Adım</span><span class="sxs-lookup"><span data-stu-id="6d41b-148">Step 3</span></span>

<span data-ttu-id="6d41b-149">Merhaba arka uç havuzları dikey penceresinde tıklatın **Ekle** tooadd ek bir arka uç havuzu **pool2**, başlangıç IP adresi veya FQDN hello arka uç sunucuları için ekleme ve tıklatın **Tamam**</span><span class="sxs-lookup"><span data-stu-id="6d41b-149">On hello backend-pools blade click **Add** tooadd an additional back-end pool **pool2**, adding hello ip addresses or FQDNS for hello back-end servers and click **OK**</span></span>

![arka uç havuzu pool2 ayarları][9]

## <a name="create-listeners-for-each-back-end"></a><span data-ttu-id="6d41b-151">Her arka uç için dinleyicileri oluşturma</span><span class="sxs-lookup"><span data-stu-id="6d41b-151">Create listeners for each back-end</span></span>

<span data-ttu-id="6d41b-152">Uygulama ağ geçidi HTTP 1.1 dayanır bir Web sitesinde birden çok konak üstbilgileri toohost hello aynı genel IP adresi ve bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="6d41b-152">Application Gateway relies on HTTP 1.1 host headers toohost more than one website on hello same public IP address and port.</span></span> <span data-ttu-id="6d41b-153">Merhaba portalında oluşturulan hello temel dinleyicisi, bu özelliği içermiyor.</span><span class="sxs-lookup"><span data-stu-id="6d41b-153">hello basic listener created in hello portal does not contain this property.</span></span>

### <a name="step-1"></a><span data-ttu-id="6d41b-154">1. Adım</span><span class="sxs-lookup"><span data-stu-id="6d41b-154">Step 1</span></span>

<span data-ttu-id="6d41b-155">Tıklatın **dinleyicileri** varolan uygulama ağ geçidi hello ve tıklatın **çok siteli** tooadd hello ilk dinleyicisi.</span><span class="sxs-lookup"><span data-stu-id="6d41b-155">Click **Listeners** on hello existing application gateway and click **Multi-site** tooadd hello first listener.</span></span>

![dinleyicileri genel bakış dikey penceresi][1]

### <a name="step-2"></a><span data-ttu-id="6d41b-157">2. Adım</span><span class="sxs-lookup"><span data-stu-id="6d41b-157">Step 2</span></span>

<span data-ttu-id="6d41b-158">Merhaba dinleyicisinin hello bilgileri doldurun.</span><span class="sxs-lookup"><span data-stu-id="6d41b-158">Fill out hello information for hello listener.</span></span> <span data-ttu-id="6d41b-159">Bu örnekte SSL sonlandırma yapılandırılır, yeni bir ön uç bağlantı noktası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6d41b-159">In this example SSL termination is configured, create a new frontend port.</span></span> <span data-ttu-id="6d41b-160">SSL sonlandırma için kullanılan hello .pfx sertifika toobe karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6d41b-160">Upload hello .pfx certificate toobe used for SSL termination.</span></span> <span data-ttu-id="6d41b-161">Merhaba yalnızca bu karşılaştırıldığında dikey toohello standart temel dinleyicisi dikey penceresinde hello hostname farktır.</span><span class="sxs-lookup"><span data-stu-id="6d41b-161">hello only difference on this blade compared toohello standard basic listener blade is hello hostname.</span></span>

![Dinleyici özellikleri dikey penceresi][2]

### <a name="step-3"></a><span data-ttu-id="6d41b-163">3. Adım</span><span class="sxs-lookup"><span data-stu-id="6d41b-163">Step 3</span></span>

<span data-ttu-id="6d41b-164">Tıklatın **çok siteli** ve hello ikinci site için hello önceki adımda açıklandığı gibi başka bir dinleyici oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6d41b-164">Click **Multi-site** and create another listener as described in hello previous step for hello second site.</span></span> <span data-ttu-id="6d41b-165">Merhaba ikinci dinleyici için farklı bir sertifika toouse emin olun.</span><span class="sxs-lookup"><span data-stu-id="6d41b-165">Make sure toouse a different certificate for hello second listener.</span></span> <span data-ttu-id="6d41b-166">Merhaba yalnızca bu karşılaştırıldığında dikey toohello standart temel dinleyicisi dikey penceresinde hello hostname farktır.</span><span class="sxs-lookup"><span data-stu-id="6d41b-166">hello only difference on this blade compared toohello standard basic listener blade is hello hostname.</span></span> <span data-ttu-id="6d41b-167">Merhaba dinleyicisinin hello bilgileri doldurun ve tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="6d41b-167">Fill out hello information for hello listener and click **OK**.</span></span>

![Dinleyici özellikleri dikey penceresi][3]

> [!NOTE]
> <span data-ttu-id="6d41b-169">Hello uygulama ağ geçidi için Azure portalı dinleyicileri oluşturulmasını uzun süre çalışan bir görevdir, işlem biraz zaman toocreate hello Bu senaryoda iki dinleyicileri sürebilir.</span><span class="sxs-lookup"><span data-stu-id="6d41b-169">Creation of listeners in hello Azure portal for application gateway is a long running task, it may take some time toocreate hello two listeners in this scenario.</span></span> <span data-ttu-id="6d41b-170">Ne zaman tam hello dinleyicileri görüntü aşağıdaki hello görüldüğü gibi hello Portalı'nda göster:</span><span class="sxs-lookup"><span data-stu-id="6d41b-170">When complete hello listeners show in hello portal as seen in hello following image:</span></span>

![Dinleyici genel bakış][4]

## <a name="create-rules-toomap-listeners-toobackend-pools"></a><span data-ttu-id="6d41b-172">Kuralları toomap dinleyicileri toobackend havuzları oluşturma</span><span class="sxs-lookup"><span data-stu-id="6d41b-172">Create rules toomap listeners toobackend pools</span></span>

### <a name="step-1"></a><span data-ttu-id="6d41b-173">1. Adım</span><span class="sxs-lookup"><span data-stu-id="6d41b-173">Step 1</span></span>

<span data-ttu-id="6d41b-174">Tooan varolan uygulama ağ geçidi hello Azure portal (https://portal.azure.com) gidin.</span><span class="sxs-lookup"><span data-stu-id="6d41b-174">Navigate tooan existing application gateway in hello Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="6d41b-175">Seçin **kuralları** ve hello mevcut varsayılan kuralı seçme **kuralı 1** tıklatıp **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="6d41b-175">Select **Rules** and choose hello existing default rule **rule1** and click **Edit**.</span></span>

### <a name="step-2"></a><span data-ttu-id="6d41b-176">2. Adım</span><span class="sxs-lookup"><span data-stu-id="6d41b-176">Step 2</span></span>

<span data-ttu-id="6d41b-177">Merhaba kuralları dikey görüntü aşağıdaki hello görüldüğü gibi doldurun.</span><span class="sxs-lookup"><span data-stu-id="6d41b-177">Fill out hello rules blade as seen in hello following image.</span></span> <span data-ttu-id="6d41b-178">Merhaba ilk dinleyici ve ilk havuzu seçme ve tıklayarak **kaydetmek** tamamlandığında.</span><span class="sxs-lookup"><span data-stu-id="6d41b-178">Choosing hello first listener and first pool and clicking **Save** when complete.</span></span>

![Mevcut kuralı düzenleyin][6]

### <a name="step-3"></a><span data-ttu-id="6d41b-180">3. Adım</span><span class="sxs-lookup"><span data-stu-id="6d41b-180">Step 3</span></span>

<span data-ttu-id="6d41b-181">Tıklatın **temel kural** toocreate hello ikinci kuralı.</span><span class="sxs-lookup"><span data-stu-id="6d41b-181">Click **Basic rule** toocreate hello second rule.</span></span> <span data-ttu-id="6d41b-182">Merhaba ikinci dinleyici ve ikinci arka uç havuzu ile Merhaba formu doldurun ve tıklayın **Tamam** toosave.</span><span class="sxs-lookup"><span data-stu-id="6d41b-182">Fill out hello form with hello second listener and second backend pool and click **OK** toosave.</span></span>

![temel kural dikey ekleme][10]

<span data-ttu-id="6d41b-184">Bu senaryo, var olan bir uygulama ağ geçidi hello Azure portal aracılığıyla çok siteli desteğiyle yapılandırma tamamlar.</span><span class="sxs-lookup"><span data-stu-id="6d41b-184">This scenario completes configuring an existing application gateway with multi-site support through hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d41b-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6d41b-185">Next steps</span></span>

<span data-ttu-id="6d41b-186">Bilgi nasıl tooprotect ile Web siteleri [uygulama ağ geçidi - Web uygulaması güvenlik duvarı](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="6d41b-186">Learn how tooprotect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

<!--Image references-->
[1]: ./media/application-gateway-create-multisite-portal/figure1.png
[2]: ./media/application-gateway-create-multisite-portal/figure2.png
[3]: ./media/application-gateway-create-multisite-portal/figure3.png
[4]: ./media/application-gateway-create-multisite-portal/figure4.png
[5]: ./media/application-gateway-create-multisite-portal/figure5.png
[6]: ./media/application-gateway-create-multisite-portal/figure6.png
[7]: ./media/application-gateway-create-multisite-portal/figure7.png
[8]: ./media/application-gateway-create-multisite-portal/figure8.png
[9]: ./media/application-gateway-create-multisite-portal/figure9.png
[10]: ./media/application-gateway-create-multisite-portal/figure10.png
[multisite]: ./media/application-gateway-create-multisite-portal/multisite.png
