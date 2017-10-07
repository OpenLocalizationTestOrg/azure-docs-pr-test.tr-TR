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
# <a name="create-an-application-gateway-using-path-based-routing-with-azure-cli-20"></a>Azure CLI 2.0 ile yol tabanlı yönlendirme kullanarak bir uygulama ağ geçidi oluşturma

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-create-url-route-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-url-route-arm-ps.md)
> * [Azure CLI 2.0](application-gateway-create-url-route-cli.md)

URL yolu tabanlı yönlendirme hello URL yola bir Http isteğinin göre tooassociate yollar sağlar. Merhaba uygulama ağ geçidi sunulan hello URL için yapılandırılmış bir rota tooa arka uç havuzu ise denetler ve arka uç havuzu hello ağ trafiği toohello tanımlanan gönderir. Farklı içerik türlerini toodifferent arka uç sunucu havuzu tooload bakiye istekleri URL tabanlı yönlendirme için ortak bir kullanılır.

URL tabanlı yönlendirme yeni bir kural türü tooapplication ağ geçidi sunar. Uygulama ağ geçidi sahip iki kural türleri: temel ve PathBasedRouting. Temel kural türü hello arka uç için hepsini hizmeti tooround bir kez deneme dağıtımı sırasında PathBasedRouting ayrıca havuzları, ayrıca hello arka uç havuzu seçerken hello istek URL'sinin yol deseni dikkate alır sağlar.

## <a name="scenario"></a>Senaryo

Aşağıdaki örneğine hello iki arka uç sunucu havuzu ile trafiği contoso.com için uygulama ağ geçidi hizmet: varsayılan sunucu havuzu ve bir görüntü sunucu havuzu.

İstekleri için http://contoso.com/image * tooimage sunucu havuzuna (imagesBackendPool) yönlendirilen, hello yol deseni eşleşmiyor, varsayılan sunucu havuzuna (appGatewayBackendPool) seçilidir.

![URL rota](./media/application-gateway-create-url-route-cli/scenario.png)

## <a name="log-in-tooazure"></a>İçinde tooAzure oturum

Açık hello **Microsoft Azure komut istemi**ve oturum açın. 

```azurecli
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

## <a name="add-a-path-based-rule-tooan-existing-application-gateway"></a>Bir kural yol tabanlı tooan varolan uygulama ağ geçidi Ekle

Tanımlı bir yol kuralı ile bir uygulama ağ geçidi oluşturma

### <a name="create-a-new-back-end-pool"></a>Yeni bir arka uç havuzu oluştur

Uygulama ağ geçidi ayarlarını yapılandırmanız **imagesBackendPool** hello yük dengeli ağ trafiği hello arka uç havuzundaki. Bu örnekte, hello yeni arka uç havuzu farklı arka uç havuzu ayarlarını yapılandırın. Her bir arka uç havuzu kendi arka uç havuzu ayarlarına sahip olabilir.  Arka uç HTTP ayarları kuralları tooroute trafiği toohello doğru arka uç havuzu üyeleri tarafından kullanılır. Bu, hello protokolü ve trafik toohello arka uç havuzu üyeleri gönderirken kullanılan bağlantı noktası belirler. Tanımlama bilgisi tabanlı oturum de hello arka uç HTTP ayarları tarafından belirlenir.  Etkinleştirilirse, tanımlama bilgisi tabanlı oturum benzeşimi trafiği toohello gönderir aynı arka uç her paket için önceki istekleri olarak.

```azurecli-interactive
az network application-gateway address-pool create \
--gateway-name AdatumAppGateway \
--name imagesBackendPool  \
--resource-group myresourcegroup \
--servers 10.0.0.6 10.0.0.7
```

### <a name="create-a-new-front-end-port"></a>Yeni ön uç bağlantı noktası oluşturma

Merhaba, bir uygulama ağ geçidi için ön uç bağlantı noktasını yapılandırın. Merhaba ön uç bağlantı noktası yapılandırma nesnesi tarafından dinleyici toodefine ne hello dinleyicisi trafiğini hello uygulama ağ geçidi dinlediği bağlantı noktası kullanılır.

```azurecli-interactive
az network application-gateway frontend-port create --port 82 --gateway-name AdatumAppGateway --resource-group myresourcegroup --name port82
```

### <a name="create-a-new-listener"></a>Yeni bir dinleyici oluşturun

Merhaba dinleyicisini yapılandırın. Bu adım hello dinleyici hello genel IP adresi için yapılandırır ve bağlantı noktası tooreceive gelen ağ trafiğini kullanılır. Aşağıdaki örneğine hello önceden yapılandırılmış hello ön uç IP yapılandırmasını, ön uç bağlantı noktası yapılandırması ve bir protokol (http veya https) alır ve hello dinleyicisi yapılandırır. Bu örnekte, hello dinleyici tooHTTP trafiği üzerinde daha önce oluşturulan hello genel IP adresi 82 numaralı bağlantı noktasında dinler.

```azurecli-interactive
az network application-gateway http-listener create --name imageListener --frontend-ip appGatewayFrontendIP  --frontend-port port82 --resource-group myresourcegroup --gateway-name AdatumAppGateway
```

### <a name="create-hello-url-path-map"></a>Merhaba Url yolu eşlemesi oluşturma

URL kuralı yolları hello arka uç havuzları için yapılandırın. Bu adım, uygulama ağ geçidi toodefine hello eşlemesi URL yolu arasındaki toohandle hello gelen trafiğin hangi arka uç havuzuna atanan tarafından kullanılan hello göreli yol yapılandırır.

> [!IMPORTANT]
> Her bir yol ile başlamalıdır / ve hello yalnızca Yerleştir bir "\*" izin verilir, hello sonunda olur. Geçerli örnekler /xyz, /xyz* veya/xyz / *. Merhaba toohello yolu Eşleştirici sat dize herhangi bir metin hello sonra ilk içermiyor "?" veya "#" ve bu karakterleri izin verilmez. 

Merhaba aşağıdaki örnekte bir kural için oluşturur "/ görüntüleri / *" yol yönlendirme trafiği tooback uç "imagesBackendPool." Bu kural her kümesi URL'leri trafiği yönlendirilmiş toohello arka uç olmasını sağlar. Örneğin, http://adatum.com/images/figure1.jpg çok gider "imagesBackendPool." Merhaba yolu hello önceden tanımlanmış bir yol kurallardan herhangi birinin eşleşmiyorsa, hello kuralı yol haritası yapılandırmasını varsayılan arka uç adres havuzu da yapılandırır. Örneğin, hello eşleşmeyen trafiği için varsayılan havuzu olarak tanımlanan http://adatum.com/shoppingcart/test.html toopool1 gider.

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

## <a name="next-steps"></a>Sonraki adımlar

Güvenli Yuva Katmanı (SSL) yük boşaltma hakkında toolearn istiyorsanız, bkz: [SSL yük boşaltımı için bir uygulama ağ geçidi](application-gateway-ssl-cli.md).


[scenario]: ./media/application-gateway-create-url-route-cli/scenario.png
[1]: ./media/application-gateway-create-url-route-cli/figure1.png
[2]: ./media/application-gateway-create-url-route-cli/figure2.png
[3]: ./media/application-gateway-create-url-route-cli/figure3.png
