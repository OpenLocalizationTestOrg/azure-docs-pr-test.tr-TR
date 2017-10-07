---
title: "aaaConfigure SSL boşaltma - Azure uygulama ağ geçidi - Azure CLI 2.0 | Microsoft Docs"
description: "Bu sayfa, Azure CLI 2.0 tarafından bir uygulama ağ geçidi ile SSL boşaltma yönergeleri toocreate sağlar."
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
ms.openlocfilehash: f8d50e0c6ffef17c807938d816410e6d85321c9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-cli-20"></a><span data-ttu-id="4dfe0-103">Azure CLI 2.0 kullanarak SSL yük boşaltımı için bir uygulama ağ geçidi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4dfe0-103">Configure an application gateway for SSL offload by using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4dfe0-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="4dfe0-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="4dfe0-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="4dfe0-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="4dfe0-106">Azure Klasik PowerShell</span><span class="sxs-lookup"><span data-stu-id="4dfe0-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="4dfe0-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4dfe0-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="4dfe0-108">Azure uygulama ağ geçidi yapılandırılmış tooterminate hello Güvenli Yuva Katmanı (SSL) hello ağ geçidi tooavoid maliyetli SSL şifre çözme görevleri toohappen hello web grubu adresindeki oturumunda olabilir.</span><span class="sxs-lookup"><span data-stu-id="4dfe0-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="4dfe0-109">SSL boşaltma ayrıca hello ön uç sunucusundaki sertifika yönetimini basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="4dfe0-109">SSL offload also simplifies certificate management at hello front-end server.</span></span>

## <a name="prerequisite-install-hello-azure-cli-20"></a><span data-ttu-id="4dfe0-110">Önkoşul: hello Azure CLI 2.0 yükleyin</span><span class="sxs-lookup"><span data-stu-id="4dfe0-110">Prerequisite: Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="4dfe0-111">Bu makaledeki adımları tooperform Merhaba, çok ihtiyacınız[hello Azure komut satırı arabirimi Mac, Linux ve Windows (Azure CLI) için yükleme](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="4dfe0-111">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="required-components"></a><span data-ttu-id="4dfe0-112">Gerekli bileşenler</span><span class="sxs-lookup"><span data-stu-id="4dfe0-112">Required components</span></span>

* <span data-ttu-id="4dfe0-113">**Arka uç sunucusu havuzu:** hello hello arka uç sunucularının IP adresleri listesi.</span><span class="sxs-lookup"><span data-stu-id="4dfe0-113">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="4dfe0-114">listede hello IP adresleri ya da toohello sanal ağ alt veya ait genel IP/VIP'ye olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4dfe0-114">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="4dfe0-115">**Arka uç sunucu havuzu ayarları**: Her havuzun bağlantı noktası, protokol ve tanımlama bilgisi temelli benzeşim gibi ayarları vardır.</span><span class="sxs-lookup"><span data-stu-id="4dfe0-115">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="4dfe0-116">Bu ayarlar bağlı tooa olan havuzu ve hello havuz içindeki uygulanan tooall sunucularıdır.</span><span class="sxs-lookup"><span data-stu-id="4dfe0-116">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="4dfe0-117">**Ön uç bağlantı noktası:** Bu bağlantı noktası hello hello uygulama ağ geçidinde açılan genel bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="4dfe0-117">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="4dfe0-118">Bu bağlantı noktasında trafik trafik ve tooone hello arka uç sunucularının alır yeniden yönlendirildi.</span><span class="sxs-lookup"><span data-stu-id="4dfe0-118">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="4dfe0-119">**Dinleyici:** hello dinleyicisi sahip bir ön uç bağlantı noktası, bir protokol (Http veya Https, bu ayarları büyük küçük harfe duyarlı) ve hello SSL sertifika adı (SSL yük boşaltımı yapılandırılıyorsa).</span><span class="sxs-lookup"><span data-stu-id="4dfe0-119">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="4dfe0-120">**Kural:** hello kural hello dinleyicisi ve hello arka uç sunucusu havuzunu bağlar ve belli bir Dinleyicide trafik yönlendirilmiş toowhen hangi arka uç sunucu havuzu hello trafiğinin olmalıdır belirler.</span><span class="sxs-lookup"><span data-stu-id="4dfe0-120">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="4dfe0-121">Şu anda yalnızca hello *temel* kural desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="4dfe0-121">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="4dfe0-122">Merhaba *temel* hepsini bir kez deneme yük dağıtımı kuralıdır.</span><span class="sxs-lookup"><span data-stu-id="4dfe0-122">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="4dfe0-123">**Ek yapılandırma notları**</span><span class="sxs-lookup"><span data-stu-id="4dfe0-123">**Additional configuration notes**</span></span>

<span data-ttu-id="4dfe0-124">SSL sertifikaları yapılandırma, protokolünde hello **HttpListener** çok değiştirmelisiniz*Https* (büyük küçük harf duyarlı).</span><span class="sxs-lookup"><span data-stu-id="4dfe0-124">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="4dfe0-125">Merhaba **SslCertificate** öğesi çok eklenen**HttpListener** hello SSL sertifikası için yapılandırılmış hello değişken değeri.</span><span class="sxs-lookup"><span data-stu-id="4dfe0-125">hello **SslCertificate** element is added too**HttpListener** with hello variable value configured for hello SSL certificate.</span></span> <span data-ttu-id="4dfe0-126">Merhaba ön uç bağlantı noktası güncelleştirilmiş too443 olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4dfe0-126">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="4dfe0-127">**tooenable tanımlama bilgisi temelli benzeşimi**: bir uygulama ağ geçidi isteği bir istemci oturumundan her zaman yönlendirilmiş toohello olduğunu yapılandırılmış tooensure olabilir hello web grubundaki aynı VM.</span><span class="sxs-lookup"><span data-stu-id="4dfe0-127">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="4dfe0-128">Bu senaryo, uygun şekilde hello ağ geçidi toodirect trafiğe izin veren bir oturum tanımlama bilgisi ekleme işlemi tarafından yapılır.</span><span class="sxs-lookup"><span data-stu-id="4dfe0-128">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="4dfe0-129">tanımlama bilgisi temelli benzeşimi tooenable ayarlamak **CookieBasedAffinity** çok*etkin* hello içinde **BackendHttpSettings** öğesi.</span><span class="sxs-lookup"><span data-stu-id="4dfe0-129">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

## <a name="configure-ssl-offload-on-an-existing-application-gateway"></a><span data-ttu-id="4dfe0-130">SSL boşaltma üzerindeki var olan bir uygulama ağ geçidini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4dfe0-130">Configure SSL offload on an existing application gateway</span></span>

```azurecli-interactive
#!/bin/bash

# Create a new front end port toobe used for SSL
az network application-gateway frontend-port create \
  --name sslport \
  --port 443 \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Upload hello .pfx certificate for SSL offload
az network application-gateway ssl-cert create \
  --name "newcert" \
  --cert-file /home/azureuser/self-signed/AdatumAppGatewayCert.pfx \
  --cert-password P@ssw0rd \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new listener referencing hello port and certificate created earlier
az network application-gateway http-listener create \
  --frontend-ip "appGatewayFrontendIP" \
  --frontend-port sslport  \
  --name sslListener \
  --ssl-cert newcert \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new back-end pool toobe used
az network application-gateway address-pool create \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG" \
  --name "appGatewayBackendPool2" \
  --servers 10.0.0.7 10.0.0.8

# Create a new back-end HTTP settings using hello new probe
az network application-gateway http-settings create \
  --name "settings2" \
  --port 80 \
  --cookie-based-affinity Enabled \
  --protocol "Http" \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new rule linking hello listener toohello back-end pool
az network application-gateway rule create \
  --name "rule2" \
  --rule-type Basic \
  --http-settings settings2 \
  --http-listener ssllistener \
  --address-pool temp1 \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

```

## <a name="create-an-application-gateway-with-ssl-offload"></a><span data-ttu-id="4dfe0-131">SSL boşaltma ile birlikte bir uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4dfe0-131">Create an application gateway with SSL Offload</span></span>

<span data-ttu-id="4dfe0-132">Aşağıdaki örnek hello SSL boşaltma ile bir uygulama ağ geçidi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4dfe0-132">hello following sample creates an application gateway with SSL offload.</span></span>  <span data-ttu-id="4dfe0-133">Merhaba sertifika ve sertifika parolası güncelleştirilmiş tooa geçerli özel anahtarı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4dfe0-133">hello certificate and certificate password must be updated tooa valid private key.</span></span>

```azurecli-interactive
#!/bin/bash

# Creates an application gateway with SSL offload
az network application-gateway create \
  --name "AdatumAppGateway3" \
  --location "eastus" \
  --resource-group "AdatumAppGatewayRG2" \
  --vnet-name "AdatumAppGatewayVNET2" \
  --cert-file /home/azureuser/self-signed/AdatumAppGatewayCert.pfx \
  --cert-password P@ssw0rd \
  --vnet-address-prefix "10.0.0.0/16" \
  --subnet "Appgatewaysubnet" \
  --subnet-address-prefix "10.0.0.0/28" \
  --frontend-port 443 \
  --servers "10.0.0.5 10.0.0.4" \
  --capacity 2 \
  --sku "Standard_Small" \
  --http-settings-cookie-based-affinity "Enabled" \
  --http-settings-protocol "Http" \
  --frontend-port "80" \
  --routing-rule-type "Basic" \
  --http-settings-port "80" \
  --public-ip-address "pip" \
  --public-ip-address-allocation "dynamic"
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="4dfe0-134">Uygulama ağ geçidi DNS adını alma</span><span class="sxs-lookup"><span data-stu-id="4dfe0-134">Get application gateway DNS name</span></span>

<span data-ttu-id="4dfe0-135">Merhaba ağ geçidi oluşturulduktan sonra hello sonraki tooconfigure hello ön uç iletişimi için adımdır.</span><span class="sxs-lookup"><span data-stu-id="4dfe0-135">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="4dfe0-136">Genel IP kullanırken uygulama ağ geçidi için dinamik olarak atanan DNS adı gerekir ve bu durum çok kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="4dfe0-136">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="4dfe0-137">hello uygulama ağ geçidi isabet tooensure son kullanıcılar, bir CNAME kaydı kullanılan toopoint toohello genel bir uç nokta hello uygulama ağ geçidi olabilir.</span><span class="sxs-lookup"><span data-stu-id="4dfe0-137">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="4dfe0-138">[Azure’da özel etki alanı adı yapılandırma](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4dfe0-138">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="4dfe0-139">tooconfigure bir diğer ad ayrıntılarını hello uygulama ağ geçidi ve hello Publicıpaddress öğesi ekli toohello uygulama ağ geçidi kullanarak ilişkili IP/DNS adını alır.</span><span class="sxs-lookup"><span data-stu-id="4dfe0-139">tooconfigure an alias, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="4dfe0-140">Merhaba uygulama ağ geçidi DNS adı kullanılan toocreate bir CNAME kaydı hangi noktaları hello iki web uygulamaları toothis DNS adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4dfe0-140">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="4dfe0-141">Uygulama ağ geçidi başlatmada Hello VIP değişebileceği A kayıtlarını hello kullanımı önerilmez.</span><span class="sxs-lookup"><span data-stu-id="4dfe0-141">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="4dfe0-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4dfe0-142">Next steps</span></span>

<span data-ttu-id="4dfe0-143">Bir iç yük dengeleyiciye (ILB) sahip bir uygulama ağ geçidi toouse tooconfigure istiyorsanız, bkz: [bir iç yük dengeleyici (ILB) ile bir uygulama ağ geçidi oluşturma](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="4dfe0-143">If you want tooconfigure an application gateway toouse with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="4dfe0-144">Yük dengeleme seçenekleri hakkında daha fazla genel bilgi edinmek istiyorsanız, bkz.</span><span class="sxs-lookup"><span data-stu-id="4dfe0-144">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="4dfe0-145">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="4dfe0-145">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="4dfe0-146">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="4dfe0-146">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
