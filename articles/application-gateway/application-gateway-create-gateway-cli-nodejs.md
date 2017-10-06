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
# <a name="create-an-application-gateway-by-using-hello-azure-cli"></a>Hello Azure CLI kullanarak bir uygulama ağ geçidi oluşturma

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-gateway-arm.md)
> * [Azure Klasik PowerShell](application-gateway-create-gateway.md)
> * [Azure Resource Manager şablonu](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI 1.0](application-gateway-create-gateway-cli.md)
> * [Azure CLI 2.0](application-gateway-create-gateway-cli.md)
> 
> 

Azure Application Gateway, bir katman 7 yük dengeleyicidir. Merhaba Bulut veya şirket içinde olmalarından bağımsız yük devretme, HTTP isteklerini, farklı sunucular arasında performans amaçlı yönlendirme sağlar. Uygulama ağ geçidi hello şu uygulama teslim özelliklerine sahiptir: HTTP Yük Dengeleme, tanımlama bilgisi tabanlı oturum benzeşimi ve Güvenli Yuva Katmanı (SSL) yük boşaltma, özel sistem durumu araştırmalarının ve desteklemek için çok siteli.

## <a name="prerequisite-install-hello-azure-cli"></a>Önkoşul: hello Azure CLI yükleme

tooperform hello bu makaledeki adımları, çok gerek[hello Azure komut satırı arabirimi Mac, Linux ve Windows (Azure CLI) için yükleme](../xplat-cli-install.md) ve çok ihtiyacınız[tooAzure üzerinde oturum](../xplat-cli-connect.md). 

> [!NOTE]
> Bir Azure hesabınız yoksa, biri gerekir. [Buradaki ücretsiz deneme sürümüyle](../active-directory/sign-up-organization.md) kaydolun.

## <a name="scenario"></a>Senaryo

Bu senaryoda, nasıl Azure portal kullanarak bir uygulama ağ geçidi toocreate hello öğrenin.

Bu senaryo aşağıdakileri yapar:

* Orta uygulama ağ geçidi ile iki örnek oluşturun.
* Bir ayrılmış 10.0.0.0/16 CIDR bloğu ile ContosoVNET adlı bir sanal ağ oluşturun.
* CIDR bloğu 10.0.0.0/28 kullanan subnet01 adlı bir alt ağ oluşturun.

> [!NOTE]
> Merhaba uygulama ağ geçidi, özel durumu da dahil olmak üzere ek yapılandırma araştırmaları, arka uç havuzu adresleri ve ek kurallar hello uygulama ağ geçidi yapılandırıldıktan sonra ve ilk dağıtım sırasında değil yapılandırılır.

## <a name="before-you-begin"></a>Başlamadan önce

Azure uygulama ağ geçidi, kendi alt gerektirir. Bir sanal ağ oluştururken, birden çok alt ağı yeterli adres alanı toohave bıraktığınızdan emin olun. Bir uygulama ağ geçidi tooa alt dağıttığınızda, yalnızca ek uygulama ağ geçitleri eklenen mümkün toobe olan toohello alt ağ.

## <a name="log-in-tooazure"></a>İçinde tooAzure oturum

Açık hello **Microsoft Azure komut istemi**ve oturum açın. 

```azurecli-interactive
azure login
```

Örnek önceki hello yazın sonra bir kod sağlanır. Bir tarayıcı toocontinue hello oturum açma işleminde toohttps://aka.MS/devicelogin gidin.

![cmd gösteren cihaz oturum açma][1]

Merhaba tarayıcıda aldığınız hello kodu girin. Yeniden yönlendirilen tooa oturum açma sayfası var.

![Tarayıcı tooenter kodu][2]

Merhaba kod girildikten sonra Kapat hello tarayıcı toocontinue hello senaryoyla oturumunuz.

![başarıyla oturum açıldı][3]

## <a name="switch-tooresource-manager-mode"></a>TooResource Manager moduna geçin

```azurecli-interactive
azure config mode arm
```

## <a name="create-hello-resource-group"></a>Merhaba kaynak grubu oluştur

Merhaba uygulama ağ geçidi oluşturmadan önce bir kaynak grubu toocontain hello uygulama ağ geçidi oluşturulur. Merhaba aşağıdaki hello komut gösterir.

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a>Sanal ağ oluşturma

Merhaba kaynak grubu oluşturulduktan sonra bir sanal ağ hello uygulama ağ geçidi için oluşturulur.  Aşağıdaki örneğine hello hello adres alanı senaryo notları önceki hello tanımlanan 10.0.0.0/16 olarak oluştu.

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a>Alt ağ oluşturma

Merhaba sanal ağ oluşturulduktan sonra bir alt ağ için hello uygulama ağ geçidi eklenir.  Düşünüyorsanız toouse uygulama ağ geçidi ile bir web uygulaması hello aynı sanal barındırılan ağ hello uygulama ağ geçidi olarak, başka bir alt ağ için yeterli alan emin tooleave olabilir.

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-hello-application-gateway"></a>Merhaba uygulama ağ geçidi oluşturma

Merhaba sanal ağ ve alt ağ oluşturulduktan sonra hello hello uygulama ağ geçidi için ön koşullar tamamlandı. Ayrıca bir daha önce dışarı aktarılan .pfx sertifika ve hello hello sertifikanın parolasını adım aşağıdaki hello için gerekli: hello arka için kullanılan hello IP adresleridir hello IP adresleri arka uç sunucunuz için. Bu değerleri ya da özel IP hello sanal ağ, genel IP'ler veya tam etki alanı adları, arka uç sunucuları için kullanılabilir.

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
> Komutu aşağıdaki hello çalıştırmak oluşturma sırasında sağlanan parametrelerin listesi için: **azure ağ uygulama ağ geçidi oluşturma--Yardım**.

Bu örnek, hello dinleyicisi, arka uç havuzu, arka uç http ayarları ve kuralları için varsayılan ayarlarla temel uygulama ağ geçidi oluşturur. Merhaba sağlama başarılı olduktan sonra bu ayarları toosuit dağıtımınızı değiştirebilirsiniz.
Adımlar bir kez oluşturulduktan sonra önceki hello hello arka uç havuzunun ile tanımlanan, web uygulamanızın zaten varsa, Yük Dengeleme başlar.

## <a name="next-steps"></a>Sonraki adımlar

Nasıl toocreate özel durumu ziyaret ederek yoklamaları öğrenin [bir özel durum araştırması oluştur](application-gateway-create-probe-portal.md)

Nasıl tooconfigure SSL boşaltma ve Al hello maliyetli SSL şifre çözme ziyaret ederek, web sunucuları kapalı öğrenin [SSL boşaltma yapılandırın](application-gateway-ssl-arm.md)

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
