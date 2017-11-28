---
title: "aaaCreate Azure uygulama ağ geçidi - Azure CLI 1.0 | Microsoft Docs"
description: "Nasıl toocreate kullanarak uygulama ağ geçidi hello Azure CLI 1.0 Kaynak Yöneticisi'nde öğrenin"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3c0d2d96b6be404d0372d00f0deb2a32959ca419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli"></a><span data-ttu-id="35134-103">Hello Azure CLI kullanarak bir uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="35134-103">Create an application gateway by using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="35134-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="35134-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="35134-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="35134-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="35134-106">Azure Klasik PowerShell</span><span class="sxs-lookup"><span data-stu-id="35134-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="35134-107">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="35134-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="35134-108">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="35134-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="35134-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="35134-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)
> 
> 

<span data-ttu-id="35134-110">Azure Application Gateway, bir katman 7 yük dengeleyicidir.</span><span class="sxs-lookup"><span data-stu-id="35134-110">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="35134-111">Merhaba Bulut veya şirket içinde olmalarından bağımsız yük devretme, HTTP isteklerini, farklı sunucular arasında performans amaçlı yönlendirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="35134-111">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="35134-112">Uygulama ağ geçidi hello şu uygulama teslim özelliklerine sahiptir: HTTP Yük Dengeleme, tanımlama bilgisi tabanlı oturum benzeşimi ve Güvenli Yuva Katmanı (SSL) yük boşaltma, özel sistem durumu araştırmalarının ve desteklemek için çok siteli.</span><span class="sxs-lookup"><span data-stu-id="35134-112">Application gateway has hello following application delivery features: HTTP load balancing, cookie-based session affinity, and Secure Sockets Layer (SSL) offload, custom health probes, and support for multi-site.</span></span>

## <a name="prerequisite-install-hello-azure-cli"></a><span data-ttu-id="35134-113">Önkoşul: hello Azure CLI yükleme</span><span class="sxs-lookup"><span data-stu-id="35134-113">Prerequisite: Install hello Azure CLI</span></span>

<span data-ttu-id="35134-114">tooperform hello bu makaledeki adımları, çok gerek[hello Azure komut satırı arabirimi Mac, Linux ve Windows (Azure CLI) için yükleme](../xplat-cli-install.md) ve çok ihtiyacınız[tooAzure üzerinde oturum](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="35134-114">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](../xplat-cli-install.md) and you need too[log on tooAzure](../xplat-cli-connect.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="35134-115">Bir Azure hesabınız yoksa, biri gerekir.</span><span class="sxs-lookup"><span data-stu-id="35134-115">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="35134-116">[Buradaki ücretsiz deneme sürümüyle](../active-directory/sign-up-organization.md) kaydolun.</span><span class="sxs-lookup"><span data-stu-id="35134-116">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="35134-117">Senaryo</span><span class="sxs-lookup"><span data-stu-id="35134-117">Scenario</span></span>

<span data-ttu-id="35134-118">Bu senaryoda, nasıl Azure portal kullanarak bir uygulama ağ geçidi toocreate hello öğrenin.</span><span class="sxs-lookup"><span data-stu-id="35134-118">In this scenario, you learn how toocreate an application gateway using hello Azure portal.</span></span>

<span data-ttu-id="35134-119">Bu senaryo aşağıdakileri yapar:</span><span class="sxs-lookup"><span data-stu-id="35134-119">This scenario will:</span></span>

* <span data-ttu-id="35134-120">Orta uygulama ağ geçidi ile iki örnek oluşturun.</span><span class="sxs-lookup"><span data-stu-id="35134-120">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="35134-121">Bir ayrılmış 10.0.0.0/16 CIDR bloğu ile ContosoVNET adlı bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="35134-121">Create a virtual network named ContosoVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="35134-122">CIDR bloğu 10.0.0.0/28 kullanan subnet01 adlı bir alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="35134-122">Create a subnet called subnet01 that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="35134-123">Merhaba uygulama ağ geçidi, özel durumu da dahil olmak üzere ek yapılandırma araştırmaları, arka uç havuzu adresleri ve ek kurallar hello uygulama ağ geçidi yapılandırıldıktan sonra ve ilk dağıtım sırasında değil yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="35134-123">Additional configuration of hello application gateway, including custom health probes, backend pool addresses, and additional rules are configured after hello application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="35134-124">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="35134-124">Before you begin</span></span>

<span data-ttu-id="35134-125">Azure uygulama ağ geçidi, kendi alt gerektirir.</span><span class="sxs-lookup"><span data-stu-id="35134-125">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="35134-126">Bir sanal ağ oluştururken, birden çok alt ağı yeterli adres alanı toohave bıraktığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="35134-126">When creating a virtual network, ensure that you leave enough address space toohave multiple subnets.</span></span> <span data-ttu-id="35134-127">Bir uygulama ağ geçidi tooa alt dağıttığınızda, yalnızca ek uygulama ağ geçitleri eklenen mümkün toobe olan toohello alt ağ.</span><span class="sxs-lookup"><span data-stu-id="35134-127">Once you deploy an application gateway tooa subnet, only additional application gateways are able toobe added toohello subnet.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="35134-128">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="35134-128">Log in tooAzure</span></span>

<span data-ttu-id="35134-129">Açık hello **Microsoft Azure komut istemi**ve oturum açın.</span><span class="sxs-lookup"><span data-stu-id="35134-129">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
azure login
```

<span data-ttu-id="35134-130">Örnek önceki hello yazın sonra bir kod sağlanır.</span><span class="sxs-lookup"><span data-stu-id="35134-130">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="35134-131">Bir tarayıcı toocontinue hello oturum açma işleminde toohttps://aka.MS/devicelogin gidin.</span><span class="sxs-lookup"><span data-stu-id="35134-131">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![cmd gösteren cihaz oturum açma][1]

<span data-ttu-id="35134-133">Merhaba tarayıcıda aldığınız hello kodu girin.</span><span class="sxs-lookup"><span data-stu-id="35134-133">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="35134-134">Yeniden yönlendirilen tooa oturum açma sayfası var.</span><span class="sxs-lookup"><span data-stu-id="35134-134">You are redirected tooa sign-in page.</span></span>

![Tarayıcı tooenter kodu][2]

<span data-ttu-id="35134-136">Merhaba kod girildikten sonra Kapat hello tarayıcı toocontinue hello senaryoyla oturumunuz.</span><span class="sxs-lookup"><span data-stu-id="35134-136">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![başarıyla oturum açıldı][3]

## <a name="switch-tooresource-manager-mode"></a><span data-ttu-id="35134-138">TooResource Manager moduna geçin</span><span class="sxs-lookup"><span data-stu-id="35134-138">Switch tooResource Manager Mode</span></span>

```azurecli-interactive
azure config mode arm
```

## <a name="create-hello-resource-group"></a><span data-ttu-id="35134-139">Merhaba kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="35134-139">Create hello resource group</span></span>

<span data-ttu-id="35134-140">Merhaba uygulama ağ geçidi oluşturmadan önce bir kaynak grubu toocontain hello uygulama ağ geçidi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="35134-140">Before creating hello application gateway, a resource group is created toocontain hello application gateway.</span></span> <span data-ttu-id="35134-141">Merhaba aşağıdaki hello komut gösterir.</span><span class="sxs-lookup"><span data-stu-id="35134-141">hello following shows hello command.</span></span>

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="35134-142">Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="35134-142">Create a virtual network</span></span>

<span data-ttu-id="35134-143">Merhaba kaynak grubu oluşturulduktan sonra bir sanal ağ hello uygulama ağ geçidi için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="35134-143">Once hello resource group is created, a virtual network is created for hello application gateway.</span></span>  <span data-ttu-id="35134-144">Aşağıdaki örneğine hello hello adres alanı senaryo notları önceki hello tanımlanan 10.0.0.0/16 olarak oluştu.</span><span class="sxs-lookup"><span data-stu-id="35134-144">In hello following example, hello address space was as 10.0.0.0/16 as defined in hello preceding scenario notes.</span></span>

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a><span data-ttu-id="35134-145">Alt ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="35134-145">Create a subnet</span></span>

<span data-ttu-id="35134-146">Merhaba sanal ağ oluşturulduktan sonra bir alt ağ için hello uygulama ağ geçidi eklenir.</span><span class="sxs-lookup"><span data-stu-id="35134-146">After hello virtual network is created, a subnet is added for hello application gateway.</span></span>  <span data-ttu-id="35134-147">Düşünüyorsanız toouse uygulama ağ geçidi ile bir web uygulaması hello aynı sanal barındırılan ağ hello uygulama ağ geçidi olarak, başka bir alt ağ için yeterli alan emin tooleave olabilir.</span><span class="sxs-lookup"><span data-stu-id="35134-147">If you plan toouse application gateway with a web app hosted in hello same virtual network as hello application gateway, be sure tooleave enough room for another subnet.</span></span>

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="35134-148">Merhaba uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="35134-148">Create hello application gateway</span></span>

<span data-ttu-id="35134-149">Merhaba sanal ağ ve alt ağ oluşturulduktan sonra hello hello uygulama ağ geçidi için ön koşullar tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="35134-149">Once hello virtual network and subnet are created, hello pre-requisites for hello application gateway are complete.</span></span> <span data-ttu-id="35134-150">Ayrıca bir daha önce dışarı aktarılan .pfx sertifika ve hello hello sertifikanın parolasını adım aşağıdaki hello için gerekli: hello arka için kullanılan hello IP adresleridir hello IP adresleri arka uç sunucunuz için.</span><span class="sxs-lookup"><span data-stu-id="35134-150">Additionally a previously exported .pfx certificate and hello password for hello certificate are required for hello following step: hello IP addresses used for hello backend are hello IP addresses for your backend server.</span></span> <span data-ttu-id="35134-151">Bu değerleri ya da özel IP hello sanal ağ, genel IP'ler veya tam etki alanı adları, arka uç sunucuları için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="35134-151">These values can be either private IPs in hello virtual network, public ips, or fully qualified domain names for your backend servers.</span></span>

```azurecli-interactive
azure network application-gateway create \
--name AdatumAppGateway \
--location eastus \
--resource-group ContosoRG \
--vnet-name ContosoVNET \
--subnet-name subnet01 \
--servers 134.170.185.46,134.170.188.221,134.170.185.50 \
--capacity 2 \
--sku-tier Standard \
--routing-rule-type Basic \
--frontend-port 80 \
--http-settings-cookie-based-affinity Enabled \
--http-settings-port 80 \
--http-settings-protocol http \
--frontend-port http \
--sku-name Standard_Medium
```

> [!NOTE]
> <span data-ttu-id="35134-152">Komutu aşağıdaki hello çalıştırmak oluşturma sırasında sağlanan parametrelerin listesi için: **azure ağ uygulama ağ geçidi oluşturma--Yardım**.</span><span class="sxs-lookup"><span data-stu-id="35134-152">For a list of parameters that can be provided during creation run hello following command: **azure network application-gateway create --help**.</span></span>

<span data-ttu-id="35134-153">Bu örnek, hello dinleyicisi, arka uç havuzu, arka uç http ayarları ve kuralları için varsayılan ayarlarla temel uygulama ağ geçidi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="35134-153">This example creates a basic application gateway with default settings for hello listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="35134-154">Merhaba sağlama başarılı olduktan sonra bu ayarları toosuit dağıtımınızı değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="35134-154">You can modify these settings toosuit your deployment once hello provisioning is successful.</span></span>
<span data-ttu-id="35134-155">Adımlar bir kez oluşturulduktan sonra önceki hello hello arka uç havuzunun ile tanımlanan, web uygulamanızın zaten varsa, Yük Dengeleme başlar.</span><span class="sxs-lookup"><span data-stu-id="35134-155">If you already have your web application defined with hello backend pool in hello preceding steps, once created, load balancing begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35134-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="35134-156">Next steps</span></span>

<span data-ttu-id="35134-157">Nasıl toocreate özel durumu ziyaret ederek yoklamaları öğrenin [bir özel durum araştırması oluştur](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="35134-157">Learn how toocreate custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="35134-158">Nasıl tooconfigure SSL boşaltma ve Al hello maliyetli SSL şifre çözme ziyaret ederek, web sunucuları kapalı öğrenin [SSL boşaltma yapılandırın](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="35134-158">Learn how tooconfigure SSL Offloading and take hello costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
