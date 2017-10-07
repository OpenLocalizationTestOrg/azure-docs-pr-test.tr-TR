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
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-hello-portal"></a>Hello portalı kullanarak bir uygulama ağ geçidi için bir yol tabanlı kuralı oluşturma

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-create-url-route-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-url-route-arm-ps.md)
> * [Azure CLI 2.0](application-gateway-create-url-route-cli.md)

URL yolu tabanlı yönlendirme hello URL yola Http isteğinin göre tooassociate yollar sağlar. Merhaba uygulama ağ geçidi listelenen hello URL için yapılandırılmış bir rota tooa arka uç havuzu ise denetler ve arka uç havuzu hello ağ trafiği toohello tanımlanan gönderir. Farklı içerik türlerini toodifferent arka uç sunucu havuzu tooload bakiye istekleri URL tabanlı yönlendirme için ortak bir kullanılır.

URL tabanlı yönlendirme yeni bir kural türü tooapplication ağ geçidi sunar. Uygulama ağ geçidi sahip iki kural türleri: temel ve yol tabanlı kuralları. temel kural türü Merhaba, sağlar hepsini hizmeti hello arka uç için yol tabanlı kurallar sırasında ayrıca tooround bir kez deneme dağıtımı havuzları, ayrıca hello uygun arka uç havuzu seçerken hello istek URL'sinin yol deseni dikkate alır.

## <a name="scenario"></a>Senaryo

Merhaba aşağıdaki senaryoyu yol tabanlı bir kuralı var olan bir uygulama ağ geçidi oluşturmada size gider.
Merhaba senaryo, zaten hello adımları çok izlediğinizden varsayar[bir uygulama ağ geçidi oluşturma](application-gateway-create-gateway-portal.md).

![URL rota][scenario]

## <a name="createrule"></a>Merhaba yol tabanlı kuralı oluşturma

Yol tabanlı bir kural kullanılabilir dinleyici toouse sahip emin tooverify olması hello kural oluşturmadan önce kendi dinleyici gerektirir.

### <a name="step-1"></a>1. Adım

Toohello gidin [Azure portal](http://portal.azure.com) ve var olan bir uygulama ağ geçidi seçin. Tıklatın **kuralları**

![Application Gateway’e genel bakış][1]

### <a name="step-2"></a>2. Adım

Tıklatın **yol tabanlı** düğmesini tooadd yol tabanlı yeni bir kural.

### <a name="step-3"></a>3. Adım

Merhaba **yol tabanlı Kuralı Ekle** dikey iki bölümü vardır. Merhaba ilk hello dinleyicisi, hello adını hello kuralı ve hello varsayılan yolu ayarları tanımlandığı bölümüdür. Merhaba varsayılan yolu hello özel yol tabanlı rota altında kalan değil rotalar için ayarlarıdır. Merhaba hello ikinci bölümü **yol tabanlı Kuralı Ekle** dikey olan burada hello yol tabanlı kurallar kendilerini tanımlarsınız.

**Temel ayarlar**

* **Ad** -bu değer hello Portalı'nda erişilebilir olan bir kolay ad toohello kuralıdır.
* **Dinleyici** -hello kural için kullanılan hello dinleyicisi bu değerdir.
* **Varsayılan arka uç havuzu** -Bu ayar hello varsayılan kural için kullanılan hello arka uç toobe tanımlayan hello ayardır
* **Varsayılan HTTP ayarları** -Bu ayar hello varsayılan kural için kullanılan hello HTTP ayarları toobe tanımlayan hello ayardır.

**Yol tabanlı kurallar**

* **Ad** -bu değer bir kolay ad toopath tabanlı kuralıdır.
* **Yollar** -Bu ayar hello yolu hello kural arar, trafiği iletirken tanımlar.
* **Arka uç havuzu** -Bu ayar hello kural için kullanılan hello arka uç toobe tanımlayan hello ayardır
* **HTTP ayarı** -Bu ayar hello kural için kullanılan hello HTTP ayarları toobe tanımlayan hello ayardır.

> [!IMPORTANT]
> Yollar: yol desenleri toomatch hello listesi. Her ile başlamalıdır / ve hello yalnızca Yerleştir bir "\*" izin hello sonunda değil. Geçerli örnekler /xyz, /xyz* veya/xyz / *.  

![Doldurulan bilgilerle Ekle yol tabanlı kural dikey penceresi][2]

Yol tabanlı kural tooan ekleme varolan uygulama ağ geçidi bir kolay hello portal üzerinden işlemidir. Yol tabanlı bir kural oluşturduktan sonra düzenlenen tooadd ek kurallar olabilir. 

![ek yol tabanlı kuralları ekleme][3]

Bu adım, yol tabanlı rota yapılandırır. Önemli toounderstand istekleri değil yazılır, uygulama ağ geçidi istekleri Gelen gibi hello istek ve hello url deseni gönderir hello isteği toohello uygun arka uç basic inceler.

## <a name="next-steps"></a>Sonraki adımlar

tooconfigure SSL boşaltma Azure uygulama ağ geçidi ile nasıl görürüm toolearn [SSL boşaltma yapılandırın](application-gateway-ssl-portal.md)

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png
