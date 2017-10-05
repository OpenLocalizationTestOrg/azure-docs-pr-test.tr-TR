---
title: "Azure uygulama ağ geçidi - Azure portalı SSL boşaltma - yapılandırma | Microsoft Docs"
description: "Bu sayfa, portal kullanarak SSL ile bir uygulama ağ geçidi oluşturma yönergelerini boşaltma sağlar."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 8373379a-a26a-45d2-aa62-dd282298eff3
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: f61be0cc4c9274c9914f7c468ce48a2a3d0a4f4a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-the-portal"></a>Portalı kullanarak SSL yük boşaltımı için bir uygulama ağ geçidi yapılandırma

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-ssl-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-ssl-arm.md)
> * [Azure Klasik PowerShell](application-gateway-ssl.md)
> * [Azure CLI 2.0](application-gateway-ssl-cli.md)

Azure Application Gateway, web grubunda maliyetli SSL şifre çözme görevlerinin oluşmasından kaçınmak için Güvenli Yuva Katmanı (SSL) oturumunu sonlandırmak amacıyla yapılandırılabilir. SSL yük boşaltımı ön uç sunucusunun kurulumunu ve web uygulamasının yönetimini de basitleştirir.

## <a name="scenario"></a>Senaryo

Aşağıdaki senaryoda nasıl yapılandıracağınız SSL boşaltma üzerinde var olan bir uygulama ağ geçidi gider. Senaryo adımları zaten izlediğinizden varsayar [bir uygulama ağ geçidi oluşturma](application-gateway-create-gateway-portal.md).

## <a name="before-you-begin"></a>Başlamadan önce

Bir uygulama ağ geçidi ile SSL yük boşaltmayı yapılandırmak için bir sertifika gereklidir. Bu sertifika uygulama ağ geçidinde yüklü ve SSL gönderilen trafiğin şifresi ve şifrelemek için kullanılır. Sertifika kişisel bilgi değişimi (pfx) biçiminde olması gerekir. Bu dosya biçimi, uygulama ağ geçidi tarafından şifreleme ve şifre çözme trafik gerçekleştirmek için gereken özel anahtar verilebilsin sağlar.

## <a name="add-an-https-listener"></a>Bir HTTPS dinleyicisi ekleme

Kendi yapılandırmasına bağlı olarak trafik HTTPS dinleyicisi arar ve yardımcı olur, arka uç havuzları trafiği yönlendirmek.

### <a name="step-1"></a>1. Adım

Azure Portalı'na gidin ve var olan bir uygulama ağ geçidi seçin

### <a name="step-2"></a>2. Adım

Dinleyicileri tıklayın ve bir dinleyici eklemek için Ekle düğmesini tıklatın.

![Uygulama ağ geçidi'ne genel bakış dikey][1]

### <a name="step-3"></a>3. Adım

.Pfx sertifika tamamlandıktan sonra Tamam'ı tıklatın gerekli bilgileri karşıya yükleme ve dinleyici için doldurun.

**Ad** -bu değer dinleyicisi kolay adıdır.

**Ön uç IP yapılandırmasını** -dinleyici için kullanılan ön uç IP yapılandırması bu değerdir.

**Ön uç bağlantı noktası (ad/bağlantı noktası)** - bağlantı noktası için bir kolay ad uygulama ağ geçidi ön ucunda gerçek bağlantı noktası kullanılır ve.

**Protokol** -https veya http ön uç için kullanılıp kullanılmadığını belirlemek için bir anahtar.

**Sertifika (ad/parola)** - varsa SSL boşaltma kullanılır, bu ayar için bir .pfx sertifika gereklidir ve bir kolay ad ve parola gereklidir.

![Dinleyici dikey ekleme][2]

## <a name="create-a-rule-and-associate-it-to-the-listener"></a>Bir kural oluşturmak ve dinleyiciye ilişkilendirme

Dinleyici şimdi oluşturuldu. Dinleyici trafiği işlemek için bir kural oluşturmak için zaman yapılır. Kuralları trafiği birden çok oturum tanımlama bilgisi temelli benzeşimi kullanılıp kullanılmadığını dahil olmak üzere, yapılandırma ayarlarını, protokol, bağlantı noktası ve sistem durumu araştırmalarının göre arka uç havuzları nasıl yönlendirildiğini tanımlayın.

### <a name="step-1"></a>1. Adım

Tıklatın **kuralları** uygulama ağ geçidi ve ardından Ekle'yi tıklatın.

![Uygulama ağ geçidi kuralları dikey][3]

### <a name="step-2"></a>2. Adım

Üzerinde **Ekle temel kural** dikey penceresinde, kural için bir kolay ad yazın ve önceki adımda oluşturduğunuz dinleyicisi seçin. Http ayarlama ve uygun arka uç havuzu seçin ve tıklatın **Tamam**

![HTTPS Ayarları penceresi][4]

Ayarları artık uygulama ağ geçidi için kaydedilir. Kaydetme işlemi portal veya PowerShell aracılığıyla görüntülemek kullanılabilir önce bu ayarları biraz zaman alabilir. Uygulama ağ geçidi kaydedildikten sonra şifreleme ve şifre çözme trafiği işler. Uygulama ağ geçidi ve arka uç web sunucuları arasındaki tüm trafik http üzerinden ele alınacaktır. Tüm iletişim https üzerinden başlattıysanız istemciye şifrelenmiş istemciye döndürülür.

## <a name="next-steps"></a>Sonraki adımlar

Azure uygulama ağ geçidi ile bir özel durum araştırması yapılandırma konusunda bilgi edinmek için [bir özel durum araştırması oluşturmak](application-gateway-create-gateway-portal.md).

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
