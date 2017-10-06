---
title: "aaaCreate Azure uygulama ağ geçidi - Azure CLI 2.0 | Microsoft Docs"
description: "Nasıl toocreate kullanarak uygulama ağ geçidi hello Azure CLI 2.0 Kaynak Yöneticisi'nde öğrenin"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 952065586cd87d253882438bb779b768d9fd59fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli-20"></a><span data-ttu-id="c6bd9-103">Hello Azure CLI 2.0 kullanarak bir uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c6bd9-103">Create an application gateway by using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c6bd9-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="c6bd9-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="c6bd9-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6bd9-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="c6bd9-106">Azure Klasik PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6bd9-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="c6bd9-107">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="c6bd9-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="c6bd9-108">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c6bd9-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="c6bd9-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c6bd9-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="c6bd9-110">Uygulama ağ geçidi, çeşitli katman 7 Yük Dengeleme yeteneklerini uygulamanız için sunumu uygulama teslim denetleyici (ADC) sağlayan bir hizmet ayrılmış bir sanal gereç olur.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-110">Application Gateway is a dedicated virtual appliance that provides application delivery controller (ADC) as a service, offering various layer 7 load balancing capabilities for your application.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="c6bd9-111">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="c6bd9-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="c6bd9-112">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="c6bd9-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="c6bd9-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) -bizim CLI hello Klasik ve kaynak yönetimi dağıtım modelleri için.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="c6bd9-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="c6bd9-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisite-install-hello-azure-cli-20"></a><span data-ttu-id="c6bd9-115">Önkoşul: hello Azure CLI 2.0 yükleyin</span><span class="sxs-lookup"><span data-stu-id="c6bd9-115">Prerequisite: Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="c6bd9-116">Bu makaledeki adımları tooperform Merhaba, çok ihtiyacınız[hello Azure komut satırı arabirimi Mac, Linux ve Windows (Azure CLI) için yükleme](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="c6bd9-116">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

> [!NOTE]
> <span data-ttu-id="c6bd9-117">Bir Azure hesabınız yoksa, biri gerekir.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-117">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="c6bd9-118">[Buradaki ücretsiz deneme sürümüyle](../active-directory/sign-up-organization.md) kaydolun.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-118">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="c6bd9-119">Senaryo</span><span class="sxs-lookup"><span data-stu-id="c6bd9-119">Scenario</span></span>

<span data-ttu-id="c6bd9-120">Bu senaryoda, nasıl Azure portal kullanarak bir uygulama ağ geçidi toocreate hello öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-120">In this scenario, you learn how toocreate an application gateway using hello Azure portal.</span></span>

<span data-ttu-id="c6bd9-121">Bu senaryo aşağıdakileri yapar:</span><span class="sxs-lookup"><span data-stu-id="c6bd9-121">This scenario will:</span></span>

* <span data-ttu-id="c6bd9-122">Orta uygulama ağ geçidi ile iki örnek oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-122">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="c6bd9-123">Bir ayrılmış 10.0.0.0/16 CIDR bloğu ile AdatumAppGatewayVNET adlı bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-123">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="c6bd9-124">Appgatewaysubnet adlı, CIDR bloğu olarak 10.0.0.0/28 kullanan bir alt ağ oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-124">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="c6bd9-125">Merhaba uygulama ağ geçidi, özel durumu da dahil olmak üzere ek yapılandırma araştırmaları, arka uç havuzu adresleri ve ek kurallar hello uygulama ağ geçidi yapılandırıldıktan sonra ve ilk dağıtım sırasında değil yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-125">Additional configuration of hello application gateway, including custom health probes, backend pool addresses, and additional rules are configured after hello application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c6bd9-126">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="c6bd9-126">Before you begin</span></span>

<span data-ttu-id="c6bd9-127">Azure uygulama ağ geçidi, kendi alt gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-127">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="c6bd9-128">Bir sanal ağ oluştururken, birden çok alt ağı yeterli adres alanı toohave bıraktığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-128">When creating a virtual network, ensure that you leave enough address space toohave multiple subnets.</span></span> <span data-ttu-id="c6bd9-129">Bir uygulama ağ geçidi tooa alt dağıttığınızda, yalnızca ek uygulama ağ geçitleri toohello alt ağa eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-129">Once you deploy an application gateway tooa subnet, only additional application gateways can be added toohello subnet.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="c6bd9-130">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="c6bd9-130">Log in tooAzure</span></span>

<span data-ttu-id="c6bd9-131">Açık hello **Microsoft Azure komut istemi**ve oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-131">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="c6bd9-132">Aynı zamanda `az login` aka.ms/devicelogin adresindeki kodunu girerek gerektirir cihaz oturum açma için hello anahtar olmadan.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-132">You can also use `az login` without hello switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="c6bd9-133">Örnek önceki hello yazın sonra bir kod sağlanır.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-133">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="c6bd9-134">Bir tarayıcı toocontinue hello oturum açma işleminde toohttps://aka.MS/devicelogin gidin.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-134">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![cmd gösteren cihaz oturum açma][1]

<span data-ttu-id="c6bd9-136">Merhaba tarayıcıda aldığınız hello kodu girin.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-136">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="c6bd9-137">Yeniden yönlendirilen tooa oturum açma sayfası var.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-137">You are redirected tooa sign-in page.</span></span>

![Tarayıcı tooenter kodu][2]

<span data-ttu-id="c6bd9-139">Merhaba kod girildikten sonra Kapat hello tarayıcı toocontinue hello senaryoyla oturumunuz.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-139">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![başarıyla oturum açıldı][3]

## <a name="create-hello-resource-group"></a><span data-ttu-id="c6bd9-141">Merhaba kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="c6bd9-141">Create hello resource group</span></span>

<span data-ttu-id="c6bd9-142">Merhaba uygulama ağ geçidi oluşturmadan önce bir kaynak grubu toocontain hello uygulama ağ geçidi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-142">Before creating hello application gateway, a resource group is created toocontain hello application gateway.</span></span> <span data-ttu-id="c6bd9-143">Merhaba aşağıdaki hello komut gösterir.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-143">hello following shows hello command.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="c6bd9-144">Merhaba uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c6bd9-144">Create hello application gateway</span></span>

<span data-ttu-id="c6bd9-145">Merhaba arka ucu için kullanılan hello IP adresleri hello IP adresleri arka uç sunucusu için ' dir.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-145">hello IP addresses used for hello backend are hello IP addresses for your backend server.</span></span> <span data-ttu-id="c6bd9-146">Bu değerleri ya da özel IP hello sanal ağ, genel IP'ler veya tam etki alanı adları, arka uç sunucuları için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-146">These values can be either private IPs in hello virtual network, public ips, or fully qualified domain names for your backend servers.</span></span> <span data-ttu-id="c6bd9-147">Hello aşağıdaki örnek bir uygulama ağ geçidi http ayarları, bağlantı noktalarını ve kurallar için ek yapılandırma ayarları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-147">hello following example creates an application gateway with additional configuration settings for http settings, ports, and rules.</span></span>

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet" \
--subnet-address-prefix "10.0.0.0/28" \
--servers 10.0.0.4 10.0.0.5 \
--capacity 2 \
--sku Standard_Small \
--http-settings-cookie-based-affinity Enabled \
--http-settings-protocol Http \
--frontend-port 80 \
--routing-rule-type Basic \
--http-settings-port 80 \
--public-ip-address "pip2" \
--public-ip-address-allocation "dynamic" \

```

<span data-ttu-id="c6bd9-148">Merhaba önceki örnekte uygulama ağ geçidi hello oluşturma sırasında gerekli olmayan birçok özellikleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-148">hello preceding example shows many properties that are not required during hello creation of an application gateway.</span></span> <span data-ttu-id="c6bd9-149">Aşağıdaki kod örneğine hello hello gerekli bilgilerle bir uygulama ağ geçidi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-149">hello following code example creates an application gateway with hello required information.</span></span>

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet \
--subnet-address-prefix "10.0.0.0/28" \
--servers "10.0.0.5"  \
--public-ip-address pip
```
 
> [!NOTE]
> <span data-ttu-id="c6bd9-150">Aşağıdaki komutu çalıştırın oluşturma hello sırasında sağlanan parametrelerin listesi için: `az network application-gateway create --help`.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-150">For a list of parameters that can be provided during creation run hello following command: `az network application-gateway create --help`.</span></span>

<span data-ttu-id="c6bd9-151">Bu örnek, hello dinleyicisi, arka uç havuzu, arka uç http ayarları ve kuralları için varsayılan ayarlarla temel uygulama ağ geçidi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-151">This example creates a basic application gateway with default settings for hello listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="c6bd9-152">Merhaba sağlama başarılı olduktan sonra bu ayarları toosuit dağıtımınızı değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-152">You can modify these settings toosuit your deployment once hello provisioning is successful.</span></span>
<span data-ttu-id="c6bd9-153">Adımlar bir kez oluşturulduktan sonra önceki hello hello arka uç havuzunun ile tanımlanan, web uygulamanızın zaten varsa, Yük Dengeleme başlar.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-153">If you already have your web application defined with hello backend pool in hello preceding steps, once created, load balancing begins.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="c6bd9-154">Uygulama ağ geçidi DNS adını alma</span><span class="sxs-lookup"><span data-stu-id="c6bd9-154">Get application gateway DNS name</span></span>

<span data-ttu-id="c6bd9-155">Merhaba ağ geçidi oluşturulduktan sonra hello sonraki tooconfigure hello ön uç iletişimi için adımdır.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-155">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="c6bd9-156">Genel IP kullanırken uygulama ağ geçidi için dinamik olarak atanan DNS adı gerekir ve bu durum çok kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-156">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="c6bd9-157">hello uygulama ağ geçidi isabet tooensure son kullanıcılar, bir CNAME kaydı kullanılan toopoint toohello genel bir uç nokta hello uygulama ağ geçidi olabilir.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-157">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="c6bd9-158">[Azure’da özel etki alanı adı yapılandırma](../dns/dns-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="c6bd9-158">[Configuring a custom domain name for in Azure](../dns/dns-custom-domain.md).</span></span> <span data-ttu-id="c6bd9-159">tooconfigure bir diğer ad ayrıntılarını hello uygulama ağ geçidi ve hello Publicıpaddress öğesi ekli toohello uygulama ağ geçidi kullanarak ilişkili IP/DNS adını alır.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-159">tooconfigure an alias, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="c6bd9-160">Merhaba uygulama ağ geçidi DNS adı kullanılan toocreate bir CNAME kaydı hangi noktaları hello iki web uygulamaları toothis DNS adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-160">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="c6bd9-161">Uygulama ağ geçidi başlatmada Hello VIP değişebileceği A kayıtlarını hello kullanımı önerilmez.</span><span class="sxs-lookup"><span data-stu-id="c6bd9-161">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


```azurecli-interactive
az network public-ip show --name "pip" --resource-group "AdatumAppGatewayRG"
```

```
{
  "dnsSettings": {
    "domainNameLabel": null,
    "fqdn": "8c786058-96d4-4f3e-bb41-660860ceae4c.cloudapp.net",
    "reverseFqdn": null
  },
  "etag": "W/\"3b0ac031-01f0-4860-b572-e3c25e0c57ad\"",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/publicIPAddresses/pip2",
  "idleTimeoutInMinutes": 4,
  "ipAddress": "40.121.167.250",
  "ipConfiguration": {
    "etag": null,
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/applicationGateways/AdatumAppGateway2/frontendIPConfigurations/appGatewayFrontendIP",
    "name": null,
    "privateIpAddress": null,
    "privateIpAllocationMethod": null,
    "provisioningState": null,
    "publicIpAddress": null,
    "resourceGroup": "AdatumAppGatewayRG",
    "subnet": null
  },
  "location": "eastus",
  "name": "pip2",
  "provisioningState": "Succeeded",
  "publicIpAddressVersion": "IPv4",
  "publicIpAllocationMethod": "Dynamic",
  "resourceGroup": "AdatumAppGatewayRG",
  "resourceGuid": "3c30d310-c543-4e9d-9c72-bbacd7fe9b05",
  "tags": {
    "cli[2] owner[administrator]": ""
  },
  "type": "Microsoft.Network/publicIPAddresses"
}
```

## <a name="delete-all-resources"></a><span data-ttu-id="c6bd9-162">Tüm kaynakları silme</span><span class="sxs-lookup"><span data-stu-id="c6bd9-162">Delete all resources</span></span>

<span data-ttu-id="c6bd9-163">Bu makalede, aşağıdaki adımları tam hello oluşturulan tüm kaynakları toodelete:</span><span class="sxs-lookup"><span data-stu-id="c6bd9-163">toodelete all resources created in this article, complete hello following steps:</span></span>

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a><span data-ttu-id="c6bd9-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c6bd9-164">Next steps</span></span>

<span data-ttu-id="c6bd9-165">Nasıl toocreate özel durumu ziyaret ederek yoklamaları öğrenin [bir özel durum araştırması oluştur](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="c6bd9-165">Learn how toocreate custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="c6bd9-166">Nasıl tooconfigure SSL boşaltma ve Al hello maliyetli SSL şifre çözme ziyaret ederek, web sunucuları kapalı öğrenin [SSL boşaltma yapılandırın](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="c6bd9-166">Learn how tooconfigure SSL Offloading and take hello costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
