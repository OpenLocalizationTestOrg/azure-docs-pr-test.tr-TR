---
title: "aaaCreate yol tabanlı bir kural - Azure uygulama ağ geçidi - Azure portalı | Microsoft Docs"
description: "Bilgi nasıl toocreate kullanarak bir uygulama ağ geçidi için bir yol tabanlı kuralı hello portalı"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 87bd93bc-e1a6-45db-a226-555948f1feb7
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: 21cb52c426ca5f7dfedf07a96e87fbc85d243647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-hello-portal"></a><span data-ttu-id="5b26e-103">Hello portalı kullanarak bir uygulama ağ geçidi için bir yol tabanlı kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b26e-103">Create a Path-based rule for an application gateway by using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5b26e-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="5b26e-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="5b26e-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b26e-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="5b26e-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5b26e-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="5b26e-107">URL yolu tabanlı yönlendirme hello URL yola Http isteğinin göre tooassociate yollar sağlar.</span><span class="sxs-lookup"><span data-stu-id="5b26e-107">URL Path-based routing enables you tooassociate routes based on hello URL path of Http request.</span></span> <span data-ttu-id="5b26e-108">Merhaba uygulama ağ geçidi listelenen hello URL için yapılandırılmış bir rota tooa arka uç havuzu ise denetler ve arka uç havuzu hello ağ trafiği toohello tanımlanan gönderir.</span><span class="sxs-lookup"><span data-stu-id="5b26e-108">It checks if there is a route tooa back-end pool configured for hello URL listed in hello Application Gateway and sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="5b26e-109">Farklı içerik türlerini toodifferent arka uç sunucu havuzu tooload bakiye istekleri URL tabanlı yönlendirme için ortak bir kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5b26e-109">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="5b26e-110">URL tabanlı yönlendirme yeni bir kural türü tooapplication ağ geçidi sunar.</span><span class="sxs-lookup"><span data-stu-id="5b26e-110">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="5b26e-111">Uygulama ağ geçidi sahip iki kural türleri: temel ve yol tabanlı kuralları.</span><span class="sxs-lookup"><span data-stu-id="5b26e-111">Application gateway has two rule types: basic and path-based rules.</span></span> <span data-ttu-id="5b26e-112">temel kural türü Merhaba, sağlar hepsini hizmeti hello arka uç için yol tabanlı kurallar sırasında ayrıca tooround bir kez deneme dağıtımı havuzları, ayrıca hello uygun arka uç havuzu seçerken hello istek URL'sinin yol deseni dikkate alır.</span><span class="sxs-lookup"><span data-stu-id="5b26e-112">hello basic rule type, provides round-robin service for hello back-end pools while path-based rules in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello appropriate backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="5b26e-113">Senaryo</span><span class="sxs-lookup"><span data-stu-id="5b26e-113">Scenario</span></span>

<span data-ttu-id="5b26e-114">Merhaba aşağıdaki senaryoyu yol tabanlı bir kuralı var olan bir uygulama ağ geçidi oluşturmada size gider.</span><span class="sxs-lookup"><span data-stu-id="5b26e-114">hello following scenario goes through creating a Path-based rule in an existing application gateway.</span></span>
<span data-ttu-id="5b26e-115">Merhaba senaryo, zaten hello adımları çok izlediğinizden varsayar[bir uygulama ağ geçidi oluşturma](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5b26e-115">hello scenario assumes that you have already followed hello steps too[Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

![URL rota][scenario]

## <span data-ttu-id="5b26e-117"><a name="createrule"></a>Merhaba yol tabanlı kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b26e-117"><a name="createrule"></a>Create hello Path-based rule</span></span>

<span data-ttu-id="5b26e-118">Yol tabanlı bir kural kullanılabilir dinleyici toouse sahip emin tooverify olması hello kural oluşturmadan önce kendi dinleyici gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5b26e-118">A Path-based rule requires its own listener, before creating hello rule be sure tooverify you have an available listener toouse.</span></span>

### <a name="step-1"></a><span data-ttu-id="5b26e-119">1. Adım</span><span class="sxs-lookup"><span data-stu-id="5b26e-119">Step 1</span></span>

<span data-ttu-id="5b26e-120">Toohello gidin [Azure portal](http://portal.azure.com) ve var olan bir uygulama ağ geçidi seçin.</span><span class="sxs-lookup"><span data-stu-id="5b26e-120">Navigate toohello [Azure portal](http://portal.azure.com) and select an existing application gateway.</span></span> <span data-ttu-id="5b26e-121">Tıklatın **kuralları**</span><span class="sxs-lookup"><span data-stu-id="5b26e-121">Click **Rules**</span></span>

![Application Gateway’e genel bakış][1]

### <a name="step-2"></a><span data-ttu-id="5b26e-123">2. Adım</span><span class="sxs-lookup"><span data-stu-id="5b26e-123">Step 2</span></span>

<span data-ttu-id="5b26e-124">Tıklatın **yol tabanlı** düğmesini tooadd yol tabanlı yeni bir kural.</span><span class="sxs-lookup"><span data-stu-id="5b26e-124">Click **Path-based** button tooadd a new Path-based rule.</span></span>

### <a name="step-3"></a><span data-ttu-id="5b26e-125">3. Adım</span><span class="sxs-lookup"><span data-stu-id="5b26e-125">Step 3</span></span>

<span data-ttu-id="5b26e-126">Merhaba **yol tabanlı Kuralı Ekle** dikey iki bölümü vardır.</span><span class="sxs-lookup"><span data-stu-id="5b26e-126">hello **Add path-based rule** blade has two sections.</span></span> <span data-ttu-id="5b26e-127">Merhaba ilk hello dinleyicisi, hello adını hello kuralı ve hello varsayılan yolu ayarları tanımlandığı bölümüdür.</span><span class="sxs-lookup"><span data-stu-id="5b26e-127">hello first section is where you defined hello listener, hello name of hello rule and hello default path settings.</span></span> <span data-ttu-id="5b26e-128">Merhaba varsayılan yolu hello özel yol tabanlı rota altında kalan değil rotalar için ayarlarıdır.</span><span class="sxs-lookup"><span data-stu-id="5b26e-128">hello default path settings are for routes that do not fall under hello custom path-based route.</span></span> <span data-ttu-id="5b26e-129">Merhaba hello ikinci bölümü **yol tabanlı Kuralı Ekle** dikey olan burada hello yol tabanlı kurallar kendilerini tanımlarsınız.</span><span class="sxs-lookup"><span data-stu-id="5b26e-129">hello second section of hello **Add path-based rule** blade is where you define hello path-based rules themselves.</span></span>

<span data-ttu-id="5b26e-130">**Temel ayarlar**</span><span class="sxs-lookup"><span data-stu-id="5b26e-130">**Basic Settings**</span></span>

* <span data-ttu-id="5b26e-131">**Ad** -bu değer hello Portalı'nda erişilebilir olan bir kolay ad toohello kuralıdır.</span><span class="sxs-lookup"><span data-stu-id="5b26e-131">**Name** - This value is a friendly name toohello rule that is accessible in hello portal.</span></span>
* <span data-ttu-id="5b26e-132">**Dinleyici** -hello kural için kullanılan hello dinleyicisi bu değerdir.</span><span class="sxs-lookup"><span data-stu-id="5b26e-132">**Listener** - This value is hello listener that is used for hello rule.</span></span>
* <span data-ttu-id="5b26e-133">**Varsayılan arka uç havuzu** -Bu ayar hello varsayılan kural için kullanılan hello arka uç toobe tanımlayan hello ayardır</span><span class="sxs-lookup"><span data-stu-id="5b26e-133">**Default backend pool** - This setting is hello setting that defines hello back-end toobe used for hello default rule</span></span>
* <span data-ttu-id="5b26e-134">**Varsayılan HTTP ayarları** -Bu ayar hello varsayılan kural için kullanılan hello HTTP ayarları toobe tanımlayan hello ayardır.</span><span class="sxs-lookup"><span data-stu-id="5b26e-134">**Default HTTP settings** - This setting is hello setting that defines hello HTTP settings toobe used for hello default rule.</span></span>

<span data-ttu-id="5b26e-135">**Yol tabanlı kurallar**</span><span class="sxs-lookup"><span data-stu-id="5b26e-135">**Path-based rules**</span></span>

* <span data-ttu-id="5b26e-136">**Ad** -bu değer bir kolay ad toopath tabanlı kuralıdır.</span><span class="sxs-lookup"><span data-stu-id="5b26e-136">**Name** - This value is a friendly name toopath-based rule.</span></span>
* <span data-ttu-id="5b26e-137">**Yollar** -Bu ayar hello yolu hello kural arar, trafiği iletirken tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5b26e-137">**Paths** - This setting defines hello path hello rule looks for when forwarding traffic</span></span>
* <span data-ttu-id="5b26e-138">**Arka uç havuzu** -Bu ayar hello kural için kullanılan hello arka uç toobe tanımlayan hello ayardır</span><span class="sxs-lookup"><span data-stu-id="5b26e-138">**Backend Pool** - This setting is hello setting that defines hello back-end toobe used for hello rule</span></span>
* <span data-ttu-id="5b26e-139">**HTTP ayarı** -Bu ayar hello kural için kullanılan hello HTTP ayarları toobe tanımlayan hello ayardır.</span><span class="sxs-lookup"><span data-stu-id="5b26e-139">**HTTP setting** - This setting is hello setting that defines hello HTTP settings toobe used for hello rule.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5b26e-140">Yollar: yol desenleri toomatch hello listesi.</span><span class="sxs-lookup"><span data-stu-id="5b26e-140">Paths: hello list of path patterns toomatch.</span></span> <span data-ttu-id="5b26e-141">Her ile başlamalıdır / ve hello yalnızca Yerleştir bir "\*" izin hello sonunda değil.</span><span class="sxs-lookup"><span data-stu-id="5b26e-141">Each must start with / and hello only place a "\*" is allowed is at hello end.</span></span> <span data-ttu-id="5b26e-142">Geçerli örnekler /xyz, /xyz* veya/xyz / *.</span><span class="sxs-lookup"><span data-stu-id="5b26e-142">Valid examples are /xyz, /xyz* or /xyz/*.</span></span>  

![Doldurulan bilgilerle Ekle yol tabanlı kural dikey penceresi][2]

<span data-ttu-id="5b26e-144">Yol tabanlı kural tooan ekleme varolan uygulama ağ geçidi bir kolay hello portal üzerinden işlemidir.</span><span class="sxs-lookup"><span data-stu-id="5b26e-144">Adding a path-based rule tooan existing application gateway is an easy process through hello portal.</span></span> <span data-ttu-id="5b26e-145">Yol tabanlı bir kural oluşturduktan sonra düzenlenen tooadd ek kurallar olabilir.</span><span class="sxs-lookup"><span data-stu-id="5b26e-145">After a path-based rule has been created, it can be edited tooadd additional rules.</span></span> 

![ek yol tabanlı kuralları ekleme][3]

<span data-ttu-id="5b26e-147">Bu adım, yol tabanlı rota yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="5b26e-147">This step configures a path-based route.</span></span> <span data-ttu-id="5b26e-148">Önemli toounderstand istekleri değil yazılır, uygulama ağ geçidi istekleri Gelen gibi hello istek ve hello url deseni gönderir hello isteği toohello uygun arka uç basic inceler.</span><span class="sxs-lookup"><span data-stu-id="5b26e-148">It is important toounderstand that requests are not rewritten, as requests come in application gateway inspects hello request and basic on hello url pattern sends hello request toohello appropriate back-end.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b26e-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5b26e-149">Next steps</span></span>

<span data-ttu-id="5b26e-150">tooconfigure SSL boşaltma Azure uygulama ağ geçidi ile nasıl görürüm toolearn [SSL boşaltma yapılandırın](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="5b26e-150">toolearn how tooconfigure SSL Offloading with Azure Application Gateway, see [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png
