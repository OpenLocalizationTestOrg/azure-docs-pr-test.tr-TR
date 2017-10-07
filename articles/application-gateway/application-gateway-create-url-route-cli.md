---
title: "URL yönlendirme kullanarak bir uygulama ağ geçidi kuralları - aaaCreate Azure CLI 2.0 | Microsoft Docs"
description: "Bu sayfa yönergeleri toocreate sağlar, URL yönlendirme kurallarını kullanarak bir Azure uygulama ağ geçidi yapılandırma"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: 335b52be258945e1172eb0252b732e0e6ecb2ef0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing-with-azure-cli-20"></a><span data-ttu-id="20ea8-103">Azure CLI 2.0 ile yol tabanlı yönlendirme kullanarak bir uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="20ea8-103">Create an application gateway using Path-based routing with Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="20ea8-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="20ea8-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="20ea8-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="20ea8-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="20ea8-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="20ea8-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="20ea8-107">URL yolu tabanlı yönlendirme hello URL yola bir Http isteğinin göre tooassociate yollar sağlar.</span><span class="sxs-lookup"><span data-stu-id="20ea8-107">URL Path-based routing enables you tooassociate routes based on hello URL path of an Http request.</span></span> <span data-ttu-id="20ea8-108">Merhaba uygulama ağ geçidi sunulan hello URL için yapılandırılmış bir rota tooa arka uç havuzu ise denetler ve arka uç havuzu hello ağ trafiği toohello tanımlanan gönderir.</span><span class="sxs-lookup"><span data-stu-id="20ea8-108">It checks if there is a route tooa back-end pool configured for hello URL presented in hello Application Gateway and sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="20ea8-109">Farklı içerik türlerini toodifferent arka uç sunucu havuzu tooload bakiye istekleri URL tabanlı yönlendirme için ortak bir kullanılır.</span><span class="sxs-lookup"><span data-stu-id="20ea8-109">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="20ea8-110">URL tabanlı yönlendirme yeni bir kural türü tooapplication ağ geçidi sunar.</span><span class="sxs-lookup"><span data-stu-id="20ea8-110">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="20ea8-111">Uygulama ağ geçidi sahip iki kural türleri: temel ve PathBasedRouting.</span><span class="sxs-lookup"><span data-stu-id="20ea8-111">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="20ea8-112">Temel kural türü hello arka uç için hepsini hizmeti tooround bir kez deneme dağıtımı sırasında PathBasedRouting ayrıca havuzları, ayrıca hello arka uç havuzu seçerken hello istek URL'sinin yol deseni dikkate alır sağlar.</span><span class="sxs-lookup"><span data-stu-id="20ea8-112">Basic rule type provides round-robin service for hello back-end pools while PathBasedRouting in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello back-end pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="20ea8-113">Senaryo</span><span class="sxs-lookup"><span data-stu-id="20ea8-113">Scenario</span></span>

<span data-ttu-id="20ea8-114">Aşağıdaki örneğine hello iki arka uç sunucu havuzu ile trafiği contoso.com için uygulama ağ geçidi hizmet: varsayılan sunucu havuzu ve bir görüntü sunucu havuzu.</span><span class="sxs-lookup"><span data-stu-id="20ea8-114">In hello following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: a default server pool and an image server pool.</span></span>

<span data-ttu-id="20ea8-115">İstekleri için http://contoso.com/image * tooimage sunucu havuzuna (imagesBackendPool) yönlendirilen, hello yol deseni eşleşmiyor, varsayılan sunucu havuzuna (appGatewayBackendPool) seçilidir.</span><span class="sxs-lookup"><span data-stu-id="20ea8-115">Requests for http://contoso.com/image* are routed tooimage server pool (imagesBackendPool), if hello path pattern does not match, a default server pool (appGatewayBackendPool) is selected.</span></span>

![URL rota](./media/application-gateway-create-url-route-cli/scenario.png)

## <a name="log-in-tooazure"></a><span data-ttu-id="20ea8-117">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="20ea8-117">Log in tooAzure</span></span>

<span data-ttu-id="20ea8-118">Açık hello **Microsoft Azure komut istemi**ve oturum açın.</span><span class="sxs-lookup"><span data-stu-id="20ea8-118">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="20ea8-119">Aynı zamanda `az login` aka.ms/devicelogin adresindeki kodunu girerek gerektirir cihaz oturum açma için hello anahtar olmadan.</span><span class="sxs-lookup"><span data-stu-id="20ea8-119">You can also use `az login` without hello switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="20ea8-120">Örnek önceki hello yazın sonra bir kod sağlanır.</span><span class="sxs-lookup"><span data-stu-id="20ea8-120">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="20ea8-121">Bir tarayıcı toocontinue hello oturum açma işleminde toohttps://aka.MS/devicelogin gidin.</span><span class="sxs-lookup"><span data-stu-id="20ea8-121">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![cmd gösteren cihaz oturum açma][1]

<span data-ttu-id="20ea8-123">Merhaba tarayıcıda aldığınız hello kodu girin.</span><span class="sxs-lookup"><span data-stu-id="20ea8-123">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="20ea8-124">Yeniden yönlendirilen tooa oturum açma sayfası var.</span><span class="sxs-lookup"><span data-stu-id="20ea8-124">You are redirected tooa sign-in page.</span></span>

![Tarayıcı tooenter kodu][2]

<span data-ttu-id="20ea8-126">Merhaba kod girildikten sonra Kapat hello tarayıcı toocontinue hello senaryoyla oturumunuz.</span><span class="sxs-lookup"><span data-stu-id="20ea8-126">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![başarıyla oturum açıldı][3]

## <a name="add-a-path-based-rule-tooan-existing-application-gateway"></a><span data-ttu-id="20ea8-128">Bir kural yol tabanlı tooan varolan uygulama ağ geçidi Ekle</span><span class="sxs-lookup"><span data-stu-id="20ea8-128">Add a path-based rule tooan existing application gateway</span></span>

<span data-ttu-id="20ea8-129">Tanımlı bir yol kuralı ile bir uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="20ea8-129">Create an application gateway with a path rule defined</span></span>

### <a name="create-a-new-back-end-pool"></a><span data-ttu-id="20ea8-130">Yeni bir arka uç havuzu oluştur</span><span class="sxs-lookup"><span data-stu-id="20ea8-130">Create a new back-end pool</span></span>

<span data-ttu-id="20ea8-131">Uygulama ağ geçidi ayarlarını yapılandırmanız **imagesBackendPool** hello yük dengeli ağ trafiği hello arka uç havuzundaki.</span><span class="sxs-lookup"><span data-stu-id="20ea8-131">Configure application gateway setting **imagesBackendPool** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="20ea8-132">Bu örnekte, hello yeni arka uç havuzu farklı arka uç havuzu ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="20ea8-132">In this example, you configure different back-end pool settings for hello new back-end pool.</span></span> <span data-ttu-id="20ea8-133">Her bir arka uç havuzu kendi arka uç havuzu ayarlarına sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="20ea8-133">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="20ea8-134">Arka uç HTTP ayarları kuralları tooroute trafiği toohello doğru arka uç havuzu üyeleri tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="20ea8-134">Backend HTTP settings are used by rules tooroute traffic toohello correct backend pool members.</span></span> <span data-ttu-id="20ea8-135">Bu, hello protokolü ve trafik toohello arka uç havuzu üyeleri gönderirken kullanılan bağlantı noktası belirler.</span><span class="sxs-lookup"><span data-stu-id="20ea8-135">This determines hello protocol and port that is used when sending traffic toohello backend pool members.</span></span> <span data-ttu-id="20ea8-136">Tanımlama bilgisi tabanlı oturum de hello arka uç HTTP ayarları tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="20ea8-136">Cookie-based sessions are also determined by hello backend HTTP settings.</span></span>  <span data-ttu-id="20ea8-137">Etkinleştirilirse, tanımlama bilgisi tabanlı oturum benzeşimi trafiği toohello gönderir aynı arka uç her paket için önceki istekleri olarak.</span><span class="sxs-lookup"><span data-stu-id="20ea8-137">If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.</span></span>

```azurecli-interactive
az network application-gateway address-pool create \
--gateway-name AdatumAppGateway \
--name imagesBackendPool  \
--resource-group myresourcegroup \
--servers 10.0.0.6 10.0.0.7
```

### <a name="create-a-new-front-end-port"></a><span data-ttu-id="20ea8-138">Yeni ön uç bağlantı noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="20ea8-138">Create a new front-end port</span></span>

<span data-ttu-id="20ea8-139">Merhaba, bir uygulama ağ geçidi için ön uç bağlantı noktasını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="20ea8-139">Configure hello front-end port for an application gateway.</span></span> <span data-ttu-id="20ea8-140">Merhaba ön uç bağlantı noktası yapılandırma nesnesi tarafından dinleyici toodefine ne hello dinleyicisi trafiğini hello uygulama ağ geçidi dinlediği bağlantı noktası kullanılır.</span><span class="sxs-lookup"><span data-stu-id="20ea8-140">hello front-end port configuration object is used by a listener toodefine what port hello Application Gateway listens for traffic on hello listener.</span></span>

```azurecli-interactive
az network application-gateway frontend-port create --port 82 --gateway-name AdatumAppGateway --resource-group myresourcegroup --name port82
```

### <a name="create-a-new-listener"></a><span data-ttu-id="20ea8-141">Yeni bir dinleyici oluşturun</span><span class="sxs-lookup"><span data-stu-id="20ea8-141">Create a new listener</span></span>

<span data-ttu-id="20ea8-142">Merhaba dinleyicisini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="20ea8-142">Configure hello listener.</span></span> <span data-ttu-id="20ea8-143">Bu adım hello dinleyici hello genel IP adresi için yapılandırır ve bağlantı noktası tooreceive gelen ağ trafiğini kullanılır.</span><span class="sxs-lookup"><span data-stu-id="20ea8-143">This step configures hello listener for hello public IP address and port used tooreceive incoming network traffic.</span></span> <span data-ttu-id="20ea8-144">Aşağıdaki örneğine hello önceden yapılandırılmış hello ön uç IP yapılandırmasını, ön uç bağlantı noktası yapılandırması ve bir protokol (http veya https) alır ve hello dinleyicisi yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="20ea8-144">hello following example takes hello previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures hello listener.</span></span> <span data-ttu-id="20ea8-145">Bu örnekte, hello dinleyici tooHTTP trafiği üzerinde daha önce oluşturulan hello genel IP adresi 82 numaralı bağlantı noktasında dinler.</span><span class="sxs-lookup"><span data-stu-id="20ea8-145">In this example, hello listener listens tooHTTP traffic on port 82 on hello public IP address that was created earlier.</span></span>

```azurecli-interactive
az network application-gateway http-listener create --name imageListener --frontend-ip appGatewayFrontendIP  --frontend-port port82 --resource-group myresourcegroup --gateway-name AdatumAppGateway
```

### <a name="create-hello-url-path-map"></a><span data-ttu-id="20ea8-146">Merhaba Url yolu eşlemesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="20ea8-146">Create hello Url path map</span></span>

<span data-ttu-id="20ea8-147">URL kuralı yolları hello arka uç havuzları için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="20ea8-147">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="20ea8-148">Bu adım, uygulama ağ geçidi toodefine hello eşlemesi URL yolu arasındaki toohandle hello gelen trafiğin hangi arka uç havuzuna atanan tarafından kullanılan hello göreli yol yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="20ea8-148">This step configures hello relative path used by application gateway toodefine hello mapping between URL path and which back-end pool is assigned toohandle hello incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20ea8-149">Her bir yol ile başlamalıdır / ve hello yalnızca Yerleştir bir "\*" izin verilir, hello sonunda olur.</span><span class="sxs-lookup"><span data-stu-id="20ea8-149">Each path must start with / and hello only place a "\*" is allowed, is at hello end.</span></span> <span data-ttu-id="20ea8-150">Geçerli örnekler /xyz, /xyz* veya/xyz / *.</span><span class="sxs-lookup"><span data-stu-id="20ea8-150">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="20ea8-151">Merhaba toohello yolu Eşleştirici sat dize herhangi bir metin hello sonra ilk içermiyor "?" veya "#" ve bu karakterleri izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="20ea8-151">hello string fed toohello path matcher does not include any text after hello first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="20ea8-152">Merhaba aşağıdaki örnekte bir kural için oluşturur "/ görüntüleri / *" yol yönlendirme trafiği tooback uç "imagesBackendPool."</span><span class="sxs-lookup"><span data-stu-id="20ea8-152">hello following example creates one rule for "/images/*" path routing traffic tooback-end "imagesBackendPool."</span></span> <span data-ttu-id="20ea8-153">Bu kural her kümesi URL'leri trafiği yönlendirilmiş toohello arka uç olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="20ea8-153">This rule ensures that traffic for each set of urls is routed toohello backend.</span></span> <span data-ttu-id="20ea8-154">Örneğin, http://adatum.com/images/figure1.jpg çok gider "imagesBackendPool."</span><span class="sxs-lookup"><span data-stu-id="20ea8-154">For example, http://adatum.com/images/figure1.jpg goes too"imagesBackendPool."</span></span> <span data-ttu-id="20ea8-155">Merhaba yolu hello önceden tanımlanmış bir yol kurallardan herhangi birinin eşleşmiyorsa, hello kuralı yol haritası yapılandırmasını varsayılan arka uç adres havuzu da yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="20ea8-155">If hello path doesn't match any of hello pre-defined path rules, hello rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="20ea8-156">Örneğin, hello eşleşmeyen trafiği için varsayılan havuzu olarak tanımlanan http://adatum.com/shoppingcart/test.html toopool1 gider.</span><span class="sxs-lookup"><span data-stu-id="20ea8-156">For example, http://adatum.com/shoppingcart/test.html goes toopool1 as it is defined as hello default pool for unmatched traffic.</span></span>

```azurecli-interactive
az network application-gateway url-path-map create \
--gateway-name AdatumAppGateway \
--name imagespathmap \
--paths /images/* \
--resource-group myresourcegroup2 \
--address-pool imagesBackendPool \
--default-address-pool appGatewayBackendPool \
--default-http-settings appGatewayBackendHttpSettings \
--http-settings appGatewayBackendHttpSettings \
--rule-name images
```

## <a name="next-steps"></a><span data-ttu-id="20ea8-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="20ea8-157">Next steps</span></span>

<span data-ttu-id="20ea8-158">Güvenli Yuva Katmanı (SSL) yük boşaltma hakkında toolearn istiyorsanız, bkz: [SSL yük boşaltımı için bir uygulama ağ geçidi](application-gateway-ssl-cli.md).</span><span class="sxs-lookup"><span data-stu-id="20ea8-158">If you want toolearn about Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-cli.md).</span></span>


[scenario]: ./media/application-gateway-create-url-route-cli/scenario.png
[1]: ./media/application-gateway-create-url-route-cli/figure1.png
[2]: ./media/application-gateway-create-url-route-cli/figure2.png
[3]: ./media/application-gateway-create-url-route-cli/figure3.png
