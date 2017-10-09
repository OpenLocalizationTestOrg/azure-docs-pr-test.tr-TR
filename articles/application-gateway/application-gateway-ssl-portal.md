---
title: "aaaConfigure SSL boşaltma - Azure uygulama ağ geçidi - Azure portalı | Microsoft Docs"
description: "Bu sayfa bir uygulama ağ geçidi ile SSL boşaltma hello portalını kullanarak yönergeleri toocreate sağlar"
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
ms.openlocfilehash: e87ac0bbe10ac45e307c18802741c7bc31764a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-portal"></a>Merhaba portalını kullanarak SSL yük boşaltımı için bir uygulama ağ geçidi yapılandırma

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-ssl-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-ssl-arm.md)
> * [Azure Klasik PowerShell](application-gateway-ssl.md)
> * [Azure CLI 2.0](application-gateway-ssl-cli.md)

Azure uygulama ağ geçidi yapılandırılmış tooterminate hello Güvenli Yuva Katmanı (SSL) hello ağ geçidi tooavoid maliyetli SSL şifre çözme görevleri toohappen hello web grubu adresindeki oturumunda olabilir. SSL boşaltma ayrıca hello ön uç sunucusunun kurulumunu ve hello web uygulamasının yönetimini basitleştirir.

## <a name="scenario"></a>Senaryo

Senaryo aşağıdaki hello nasıl yapılandıracağınız SSL boşaltma üzerinde var olan bir uygulama ağ geçidi gider. Merhaba senaryo, zaten hello adımları çok izlediğinizden varsayar[bir uygulama ağ geçidi oluşturma](application-gateway-create-gateway-portal.md).

## <a name="before-you-begin"></a>Başlamadan önce

tooconfigure SSL yük boşaltımı bir uygulama ağ geçidi ile bir sertifika gereklidir. Bu sertifika tooencrypt kullanılan hello uygulama ağ geçidinde yüklenir ve SSL gönderilen hello trafiğin şifresi. Merhaba sertifika toobe kişisel bilgi değişimi (pfx) biçiminde olmalıdır. Bu dosya biçimi, hangi hello uygulama ağ geçidi tooperform hello şifreleme ve şifre çözme trafik tarafından gerekli anahtar toobe dışarı Merhaba özel sağlar.

## <a name="add-an-https-listener"></a>Bir HTTPS dinleyicisi ekleme

Merhaba HTTPS dinleyicisi kendi yapılandırmasını temel alarak trafiği arar ve rota hello trafiği toohello arka uç havuzları yardımcı olur.

### <a name="step-1"></a>1. Adım

Toohello Azure portalına gidin ve var olan bir uygulama ağ geçidi seçin

### <a name="step-2"></a>2. Adım

Dinleyicileri ve hello Ekle düğmesi tooadd dinleyici tıklayın.

![Uygulama ağ geçidi'ne genel bakış dikey][1]

### <a name="step-3"></a>3. Adım

Merhaba dinleyici için gereken bilgileri hello ve karşıya yükleme hello .pfx sertifika, tamamlandığında, Tamam'ı tıklatın doldurun.

**Ad** -bu değer hello dinleyicisi kolay adıdır.

**Ön uç IP yapılandırmasını** -hello dinleyici için kullanılan hello ön uç IP yapılandırması bu değerdir.

**Ön uç bağlantı noktası (ad/bağlantı noktası)** -hello ön ucunda hello uygulama ağ geçidi ve kullanılan hello gerçek bağlantı noktası kullanılan başlangıç bağlantı noktası için bir kolay ad.

**Protokol** -hello ön uç için https veya http kullanılıyorsa bir anahtar toodetermine.

**Sertifika (ad/parola)** - varsa SSL boşaltma kullanılır, bu ayar için bir .pfx sertifika gereklidir ve bir kolay ad ve parola gereklidir.

![Dinleyici dikey ekleme][2]

## <a name="create-a-rule-and-associate-it-toohello-listener"></a>Bir kural oluşturmak ve toohello dinleyicisi ilişkilendirme

Merhaba dinleyicisi şimdi oluşturuldu. Zaman toocreate hello dinleyicisi kural toohandle hello trafiğinden olur. Kuralları nasıl trafiği birden çok oturum tanımlama bilgisi temelli benzeşimi kullanılıp kullanılmadığını dahil olmak üzere, yapılandırma ayarlarını, protokol, bağlantı noktası ve sistem durumu araştırmalarının göre yönlendirilmiş toohello arka uç havuzları tanımlayın.

### <a name="step-1"></a>1. Adım

Merhaba tıklatın **kuralları** hello uygulama ağ geçidi ve ardından Ekle'yi tıklatın.

![Uygulama ağ geçidi kuralları dikey][3]

### <a name="step-2"></a>2. Adım

Merhaba üzerinde **Ekle temel kural** dikey penceresinde hello hello kuralı için kolay ad yazın ve hello önceki adımda oluşturduğunuz hello dinleyicisi seçin. Hello uygun arka uç havuzu ve http ayarını seçin ve tıklatın **Tamam**

![HTTPS Ayarları penceresi][4]

Hello ayarları şimdi toohello uygulama ağ geçidi kaydedildi. Merhaba portal veya PowerShell aracılığıyla kullanılabilir tooview önce hello Kaydet işlemi bu ayarlar için biraz zaman alabilir. Bir kez kaydedilmiş hello uygulama ağ geçidi hello şifreleme ve şifre çözme trafiği işler. Merhaba uygulama ağ geçidi ile Merhaba arka uç web sunucuları arasındaki tüm trafik http üzerinden ele alınacaktır. HTTPS üzerinden başlattıysanız tüm iletişimi geri toohello istemci şifrelenmiş toohello istemci döndürülür.

## <a name="next-steps"></a>Sonraki adımlar

Azure uygulama ağ geçidi ile tooconfigure özel durumu araştırma nasıl toolearn bkz [bir özel durum araştırması oluşturmak](application-gateway-create-gateway-portal.md).

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
