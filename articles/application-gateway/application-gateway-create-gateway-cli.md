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
# <a name="create-an-application-gateway-by-using-hello-azure-cli-20"></a>Hello Azure CLI 2.0 kullanarak bir uygulama ağ geçidi oluşturma

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-gateway-arm.md)
> * [Azure Klasik PowerShell](application-gateway-create-gateway.md)
> * [Azure Resource Manager şablonu](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI 1.0](application-gateway-create-gateway-cli.md)
> * [Azure CLI 2.0](application-gateway-create-gateway-cli.md)

Uygulama ağ geçidi, çeşitli katman 7 Yük Dengeleme yeteneklerini uygulamanız için sunumu uygulama teslim denetleyici (ADC) sağlayan bir hizmet ayrılmış bir sanal gereç olur.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi

CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

* [Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) -bizim CLI hello Klasik ve kaynak yönetimi dağıtım modelleri için.
* [Azure CLI 2.0](application-gateway-create-gateway-cli.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için

## <a name="prerequisite-install-hello-azure-cli-20"></a>Önkoşul: hello Azure CLI 2.0 yükleyin

Bu makaledeki adımları tooperform Merhaba, çok ihtiyacınız[hello Azure komut satırı arabirimi Mac, Linux ve Windows (Azure CLI) için yükleme](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

> [!NOTE]
> Bir Azure hesabınız yoksa, biri gerekir. [Buradaki ücretsiz deneme sürümüyle](../active-directory/sign-up-organization.md) kaydolun.

## <a name="scenario"></a>Senaryo

Bu senaryoda, nasıl Azure portal kullanarak bir uygulama ağ geçidi toocreate hello öğrenin.

Bu senaryo aşağıdakileri yapar:

* Orta uygulama ağ geçidi ile iki örnek oluşturun.
* Bir ayrılmış 10.0.0.0/16 CIDR bloğu ile AdatumAppGatewayVNET adlı bir sanal ağ oluşturun.
* Appgatewaysubnet adlı, CIDR bloğu olarak 10.0.0.0/28 kullanan bir alt ağ oluşturacaksınız.

> [!NOTE]
> Merhaba uygulama ağ geçidi, özel durumu da dahil olmak üzere ek yapılandırma araştırmaları, arka uç havuzu adresleri ve ek kurallar hello uygulama ağ geçidi yapılandırıldıktan sonra ve ilk dağıtım sırasında değil yapılandırılır.

## <a name="before-you-begin"></a>Başlamadan önce

Azure uygulama ağ geçidi, kendi alt gerektirir. Bir sanal ağ oluştururken, birden çok alt ağı yeterli adres alanı toohave bıraktığınızdan emin olun. Bir uygulama ağ geçidi tooa alt dağıttığınızda, yalnızca ek uygulama ağ geçitleri toohello alt ağa eklenebilir.

## <a name="log-in-tooazure"></a>İçinde tooAzure oturum

Açık hello **Microsoft Azure komut istemi**ve oturum açın. 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> Aynı zamanda `az login` aka.ms/devicelogin adresindeki kodunu girerek gerektirir cihaz oturum açma için hello anahtar olmadan.

Örnek önceki hello yazın sonra bir kod sağlanır. Bir tarayıcı toocontinue hello oturum açma işleminde toohttps://aka.MS/devicelogin gidin.

![cmd gösteren cihaz oturum açma][1]

Merhaba tarayıcıda aldığınız hello kodu girin. Yeniden yönlendirilen tooa oturum açma sayfası var.

![Tarayıcı tooenter kodu][2]

Merhaba kod girildikten sonra Kapat hello tarayıcı toocontinue hello senaryoyla oturumunuz.

![başarıyla oturum açıldı][3]

## <a name="create-hello-resource-group"></a>Merhaba kaynak grubu oluştur

Merhaba uygulama ağ geçidi oluşturmadan önce bir kaynak grubu toocontain hello uygulama ağ geçidi oluşturulur. Merhaba aşağıdaki hello komut gösterir.

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-hello-application-gateway"></a>Merhaba uygulama ağ geçidi oluşturma

Merhaba arka ucu için kullanılan hello IP adresleri hello IP adresleri arka uç sunucusu için ' dir. Bu değerleri ya da özel IP hello sanal ağ, genel IP'ler veya tam etki alanı adları, arka uç sunucuları için kullanılabilir. Hello aşağıdaki örnek bir uygulama ağ geçidi http ayarları, bağlantı noktalarını ve kurallar için ek yapılandırma ayarları oluşturur.

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

Merhaba önceki örnekte uygulama ağ geçidi hello oluşturma sırasında gerekli olmayan birçok özellikleri gösterir. Aşağıdaki kod örneğine hello hello gerekli bilgilerle bir uygulama ağ geçidi oluşturur.

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
> Aşağıdaki komutu çalıştırın oluşturma hello sırasında sağlanan parametrelerin listesi için: `az network application-gateway create --help`.

Bu örnek, hello dinleyicisi, arka uç havuzu, arka uç http ayarları ve kuralları için varsayılan ayarlarla temel uygulama ağ geçidi oluşturur. Merhaba sağlama başarılı olduktan sonra bu ayarları toosuit dağıtımınızı değiştirebilirsiniz.
Adımlar bir kez oluşturulduktan sonra önceki hello hello arka uç havuzunun ile tanımlanan, web uygulamanızın zaten varsa, Yük Dengeleme başlar.

## <a name="get-application-gateway-dns-name"></a>Uygulama ağ geçidi DNS adını alma

Merhaba ağ geçidi oluşturulduktan sonra hello sonraki tooconfigure hello ön uç iletişimi için adımdır. Genel IP kullanırken uygulama ağ geçidi için dinamik olarak atanan DNS adı gerekir ve bu durum çok kullanışlı değildir. hello uygulama ağ geçidi isabet tooensure son kullanıcılar, bir CNAME kaydı kullanılan toopoint toohello genel bir uç nokta hello uygulama ağ geçidi olabilir. [Azure’da özel etki alanı adı yapılandırma](../dns/dns-custom-domain.md). tooconfigure bir diğer ad ayrıntılarını hello uygulama ağ geçidi ve hello Publicıpaddress öğesi ekli toohello uygulama ağ geçidi kullanarak ilişkili IP/DNS adını alır. Merhaba uygulama ağ geçidi DNS adı kullanılan toocreate bir CNAME kaydı hangi noktaları hello iki web uygulamaları toothis DNS adı olmalıdır. Uygulama ağ geçidi başlatmada Hello VIP değişebileceği A kayıtlarını hello kullanımı önerilmez.


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

## <a name="delete-all-resources"></a>Tüm kaynakları silme

Bu makalede, aşağıdaki adımları tam hello oluşturulan tüm kaynakları toodelete:

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a>Sonraki adımlar

Nasıl toocreate özel durumu ziyaret ederek yoklamaları öğrenin [bir özel durum araştırması oluştur](application-gateway-create-probe-portal.md)

Nasıl tooconfigure SSL boşaltma ve Al hello maliyetli SSL şifre çözme ziyaret ederek, web sunucuları kapalı öğrenin [SSL boşaltma yapılandırın](application-gateway-ssl-arm.md)

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
