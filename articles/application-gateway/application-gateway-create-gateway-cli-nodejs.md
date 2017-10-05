---
title: "Bir Azure uygulama ağ geçidi - Azure CLI 1.0 oluşturma | Microsoft Docs"
description: "Resource Manager'da Azure CLI 1.0 kullanarak bir uygulama ağ geçidi oluşturmayı öğrenin"
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
ms.openlocfilehash: e7b16e789e0f241aa8ca2292aacb2bccde8777ee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-by-using-the-azure-cli"></a><span data-ttu-id="62d22-103">Azure CLI kullanarak bir uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="62d22-103">Create an application gateway by using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="62d22-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="62d22-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="62d22-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="62d22-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="62d22-106">Azure Klasik PowerShell</span><span class="sxs-lookup"><span data-stu-id="62d22-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="62d22-107">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="62d22-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="62d22-108">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="62d22-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="62d22-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="62d22-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)
> 
> 

<span data-ttu-id="62d22-110">Azure Application Gateway, bir katman 7 yük dengeleyicidir.</span><span class="sxs-lookup"><span data-stu-id="62d22-110">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="62d22-111">Bulutta veya şirket içinde olmalarından bağımsız olarak, farklı sunucular arasında yük devretme ile HTTP istekleri için performans amaçlı yönlendirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="62d22-111">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="62d22-112">Uygulama ağ geçidi şu uygulama teslim özelliklerine sahiptir: HTTP Yük Dengeleme, tanımlama bilgisi tabanlı oturum benzeşimi ve Güvenli Yuva Katmanı (SSL) yük boşaltma, özel sistem durumu araştırmalarının ve desteklemek için çok siteli.</span><span class="sxs-lookup"><span data-stu-id="62d22-112">Application gateway has the following application delivery features: HTTP load balancing, cookie-based session affinity, and Secure Sockets Layer (SSL) offload, custom health probes, and support for multi-site.</span></span>

## <a name="prerequisite-install-the-azure-cli"></a><span data-ttu-id="62d22-113">Önkoşul: Azure CLI'yı yükleme</span><span class="sxs-lookup"><span data-stu-id="62d22-113">Prerequisite: Install the Azure CLI</span></span>

<span data-ttu-id="62d22-114">Bu makaledeki adımları gerçekleştirmek için gerek [Mac, Linux ve Windows (Azure CLI) için Azure komut satırı arabirimini yükleyin](../xplat-cli-install.md) ve gerek [Azure oturumunu](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="62d22-114">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](../xplat-cli-install.md) and you need to [log on to Azure](../xplat-cli-connect.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="62d22-115">Bir Azure hesabınız yoksa, biri gerekir.</span><span class="sxs-lookup"><span data-stu-id="62d22-115">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="62d22-116">[Buradaki ücretsiz deneme sürümüyle](../active-directory/sign-up-organization.md) kaydolun.</span><span class="sxs-lookup"><span data-stu-id="62d22-116">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="62d22-117">Senaryo</span><span class="sxs-lookup"><span data-stu-id="62d22-117">Scenario</span></span>

<span data-ttu-id="62d22-118">Bu senaryoda, Azure portalını kullanarak bir uygulama ağ geçidi oluşturmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="62d22-118">In this scenario, you learn how to create an application gateway using the Azure portal.</span></span>

<span data-ttu-id="62d22-119">Bu senaryo aşağıdakileri yapar:</span><span class="sxs-lookup"><span data-stu-id="62d22-119">This scenario will:</span></span>

* <span data-ttu-id="62d22-120">Orta uygulama ağ geçidi ile iki örnek oluşturun.</span><span class="sxs-lookup"><span data-stu-id="62d22-120">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="62d22-121">Bir ayrılmış 10.0.0.0/16 CIDR bloğu ile ContosoVNET adlı bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="62d22-121">Create a virtual network named ContosoVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="62d22-122">CIDR bloğu 10.0.0.0/28 kullanan subnet01 adlı bir alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="62d22-122">Create a subnet called subnet01 that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="62d22-123">Özel durumu da dahil olmak üzere uygulama ağ geçidinin ek yapılandırma araştırmaları, arka uç havuzu adresleri ve ek kurallar uygulama ağ geçidi yapılandırıldıktan sonra ve ilk dağıtım sırasında değil yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="62d22-123">Additional configuration of the application gateway, including custom health probes, backend pool addresses, and additional rules are configured after the application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="62d22-124">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="62d22-124">Before you begin</span></span>

<span data-ttu-id="62d22-125">Azure uygulama ağ geçidi, kendi alt gerektirir.</span><span class="sxs-lookup"><span data-stu-id="62d22-125">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="62d22-126">Bir sanal ağ oluştururken, birden çok alt ağa sahip için yeterli adres alanı bıraktığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="62d22-126">When creating a virtual network, ensure that you leave enough address space to have multiple subnets.</span></span> <span data-ttu-id="62d22-127">Bir alt ağ için bir uygulama ağ geçidi dağıttığınızda, yalnızca ek uygulama ağ geçidi alt ağına eklemek kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62d22-127">Once you deploy an application gateway to a subnet, only additional application gateways are able to be added to the subnet.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="62d22-128">Azure'da oturum açma</span><span class="sxs-lookup"><span data-stu-id="62d22-128">Log in to Azure</span></span>

<span data-ttu-id="62d22-129">Açık **Microsoft Azure komut istemi**ve oturum açın.</span><span class="sxs-lookup"><span data-stu-id="62d22-129">Open the **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
azure login
```

<span data-ttu-id="62d22-130">Önceki örnekte yazın sonra bir kod sağlanır.</span><span class="sxs-lookup"><span data-stu-id="62d22-130">Once you type the preceding example, a code is provided.</span></span> <span data-ttu-id="62d22-131">Oturum açma işlemine devam etmek için bir tarayıcıda https://aka.ms/devicelogin gidin.</span><span class="sxs-lookup"><span data-stu-id="62d22-131">Navigate to https://aka.ms/devicelogin in a browser to continue the login process.</span></span>

![cmd gösteren cihaz oturum açma][1]

<span data-ttu-id="62d22-133">Tarayıcıda, aldığınız kodu girin.</span><span class="sxs-lookup"><span data-stu-id="62d22-133">In the browser, enter the code you received.</span></span> <span data-ttu-id="62d22-134">Bir oturum açma sayfasına yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="62d22-134">You are redirected to a sign-in page.</span></span>

![Tarayıcı kodu girin][2]

<span data-ttu-id="62d22-136">Kod girildikten sonra oturum açtığınızdan, üzerinde senaryoyla devam etmek için tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="62d22-136">Once the code has been entered you are signed in, close the browser to continue on with the scenario.</span></span>

![başarıyla oturum açıldı][3]

## <a name="switch-to-resource-manager-mode"></a><span data-ttu-id="62d22-138">Resource Manager moduna geçin</span><span class="sxs-lookup"><span data-stu-id="62d22-138">Switch to Resource Manager Mode</span></span>

```azurecli-interactive
azure config mode arm
```

## <a name="create-the-resource-group"></a><span data-ttu-id="62d22-139">Kaynak grubunu oluşturma</span><span class="sxs-lookup"><span data-stu-id="62d22-139">Create the resource group</span></span>

<span data-ttu-id="62d22-140">Uygulama ağ geçidi oluşturmadan önce bir kaynak grubu, uygulama ağ geçidi içerecek şekilde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="62d22-140">Before creating the application gateway, a resource group is created to contain the application gateway.</span></span> <span data-ttu-id="62d22-141">Aşağıda, komut gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="62d22-141">The following shows the command.</span></span>

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="62d22-142">Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="62d22-142">Create a virtual network</span></span>

<span data-ttu-id="62d22-143">Kaynak grubu oluşturulduktan sonra bir sanal ağ uygulama ağ geçidi için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="62d22-143">Once the resource group is created, a virtual network is created for the application gateway.</span></span>  <span data-ttu-id="62d22-144">Aşağıdaki örnekte, önceki senaryo notları tanımlanan adres alanı 10.0.0.0/16 oluştu.</span><span class="sxs-lookup"><span data-stu-id="62d22-144">In the following example, the address space was as 10.0.0.0/16 as defined in the preceding scenario notes.</span></span>

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a><span data-ttu-id="62d22-145">Alt ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="62d22-145">Create a subnet</span></span>

<span data-ttu-id="62d22-146">Sanal ağ oluşturulduktan sonra bir alt ağ için uygulama ağ geçidi eklenir.</span><span class="sxs-lookup"><span data-stu-id="62d22-146">After the virtual network is created, a subnet is added for the application gateway.</span></span>  <span data-ttu-id="62d22-147">Uygulama ağ geçidiyle aynı sanal ağ içinde barındırılan bir web uygulaması ile uygulama ağ geçidi kullanmayı planlıyorsanız, başka bir alt ağ için yeterli alan olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="62d22-147">If you plan to use application gateway with a web app hosted in the same virtual network as the application gateway, be sure to leave enough room for another subnet.</span></span>

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="62d22-148">Uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="62d22-148">Create the application gateway</span></span>

<span data-ttu-id="62d22-149">Sanal ağ ve alt ağ oluşturulduktan sonra uygulama ağ geçidi için ön koşullar tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="62d22-149">Once the virtual network and subnet are created, the pre-requisites for the application gateway are complete.</span></span> <span data-ttu-id="62d22-150">Ayrıca daha önce dışarı aktarılan .pfx sertifika ve sertifika için parola için aşağıdaki adım gereklidir: arka uç için kullanılan IP adresleri arka uç sunucusu için IP adresleridir.</span><span class="sxs-lookup"><span data-stu-id="62d22-150">Additionally a previously exported .pfx certificate and the password for the certificate are required for the following step: The IP addresses used for the backend are the IP addresses for your backend server.</span></span> <span data-ttu-id="62d22-151">Bu değerler, sanal ağ içinde kullanılabilecek özel IP, genel IP'ler veya arka uç sunucuları için tam etki alanı adları olabilir.</span><span class="sxs-lookup"><span data-stu-id="62d22-151">These values can be either private IPs in the virtual network, public ips, or fully qualified domain names for your backend servers.</span></span>

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
> <span data-ttu-id="62d22-152">Aşağıdaki komutu çalıştırın oluşturma sırasında sağlanan parametrelerin listesi için: **azure ağ uygulama ağ geçidi oluşturma--Yardım**.</span><span class="sxs-lookup"><span data-stu-id="62d22-152">For a list of parameters that can be provided during creation run the following command: **azure network application-gateway create --help**.</span></span>

<span data-ttu-id="62d22-153">Bu örnek, dinleyicisi, arka uç havuzu, arka uç http ayarları ve kuralları için varsayılan ayarlarla temel uygulama ağ geçidi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="62d22-153">This example creates a basic application gateway with default settings for the listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="62d22-154">Bu ayarları sağlama başarılı olduktan sonra dağıtımınızı uyacak şekilde değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62d22-154">You can modify these settings to suit your deployment once the provisioning is successful.</span></span>
<span data-ttu-id="62d22-155">Web uygulamanızın arka uç havuzu oluşturulduktan sonra önceki adımlarda tanımlanan zaten varsa, Yük Dengeleme başlar.</span><span class="sxs-lookup"><span data-stu-id="62d22-155">If you already have your web application defined with the backend pool in the preceding steps, once created, load balancing begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62d22-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="62d22-156">Next steps</span></span>

<span data-ttu-id="62d22-157">Özel sistem durumu araştırmalarının ziyaret ederek oluşturmayı öğrenin [bir özel durum araştırması oluştur](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="62d22-157">Learn how to create custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="62d22-158">SSL boşaltma yapılandırmak ve web sunucularınızın kapalı maliyetli SSL şifre çözme ziyaret ederek ele öğrenin [SSL boşaltma yapılandırın](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="62d22-158">Learn how to configure SSL Offloading and take the costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
