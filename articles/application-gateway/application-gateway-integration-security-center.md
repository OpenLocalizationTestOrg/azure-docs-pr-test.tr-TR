---
title: "Azure Güvenlik Merkezi ile ağ geçidi tümleştirme aaaApplication | Microsoft Docs"
description: "Bu sayfa, uygulama ağ geçidi Azure Güvenlik Merkezi ile nasıl tümleştirildiği bilgi sağlar."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: e5ea5cf9-3b41-4b85-a12c-e758bff7f3ec
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 06/07/2017
ms.author: gwallace
ms.openlocfilehash: 6f6ace105e84c01f525ab02938e81ce040c5c9d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a>Uygulama ağ geçidi ve Azure Güvenlik Merkezi arasında tümleştirme genel bakış

Uygulama ağ geçidi ve Güvenlik Merkezi, web uygulaması kaynaklarınızı korumanıza nasıl yardımcı öğrenin. Uygulama ağ geçidi web uygulaması Güvenlik Duvarı (WAF) ile tümleşir [Güvenlik Merkezi](../security-center/security-center-intro.md) tooprovide sorunsuz görünüm tooprevent algılamak ve toothreats toounprotected web uygulamaları, ortamınızdaki yanıt.

## <a name="overview"></a>Genel Bakış

Uygulama ağ geçidi WAF Güvenlik Merkezi'nde açığından yararlanma girişimi ve güvenlik açıkları web uygulamaları korumak için önerilir. WAF tarafından korunmayan etkin web kaynakları hello Güvenlik Merkezi'nde yüksek önem derecesi öneriler göster. Web uygulaması güvenlik duvarı için öneriler hello üzerinde gösterilen **genel bakış** sayfasında **uygulamaları**.

![Güvenlik Merkezi ile tümleştirme][1]

Web uygulaması güvenlik duvarı ile ilgili herhangi bir önerimiz tıklatarak hello öneri hello ayrıntılarını gösteren yeni bir dikey pencere açılır.

## <a name="add-a-web-application-firewall-tooan-existing-resource"></a>Web uygulaması güvenlik duvarı tooan mevcut kaynak ekleyin

Çok gidin**daha Hizmetleri** > **güvenlik + kimlik** > **Güvenlik Merkezi** ve hello **Güvenlik Merkezi - genel bakış**  dikey penceresinde tıklatın **uygulamaları**. Merhaba üzerinde **Güvenlik Merkezi - uygulamaları** dikey penceresinde hello tablo, Güvenlik Merkezi, aboneliğinizde algıladı uygulamaların bir listesini içerir.

![Web uygulamaları][3]

Kritik bir sorunu web uygulamasıyla tıklayarak, hello alma **uygulama güvenlik durumu** dikey. Merhaba resimde, bir web uygulaması güvenlik duvarı tarafından korumalı olmayan web uygulaması hello. 

![korumalı web kaynakları][2]

Tıklatın **bir web uygulaması güvenlik duvarı ekleme** altında **önerileri** tooopen hello **bir Web uygulaması güvenlik duvarı ekleme** dikey.

Olmayan mevcut bir uygulama ağ geçidi sahip ya da toocreate yeni bir tane yoksa, tıklatın **Yeni Oluştur** ve hello **yeni Web uygulaması güvenlik duvarı oluşturma** dikey penceresinde ve tıklatın **Microsoft - Uygulama ağ geçidi**. Merhaba adımları toocreate bir uygulama ağ geçidi alır. Bu noktada, bu kaynak bir web uygulaması güvenlik duvarı tarafından korunduğunu şimdi Güvenlik Merkezi korumalı bir kaynağın izler, web uygulamanızın eklenir. Bu, arka uç havuzu üye olarak eklemez.

Mevcut bir uygulama ağ geçidi varsa, bunun altında seçebilirsiniz **var olan çözümünü kullanma**

![Web uygulaması güvenlik duvarı Ekle dikey penceresi][4]

Bir web uygulaması tooan uygulama ağ geçidi Güvenlik Merkezi aracılığıyla arka uç havuzu üye olarak hello kaynak eklemez ekleme, bu hello uygulama ağ geçidi kaynağı üzerinde doğrudan yapılmalıdır.

## <a name="add-a-resource-tooan-existing-web-application-firewall"></a>Bir kaynak tooan varolan web uygulaması güvenlik duvarı ekleme

Çok gidin**daha Hizmetleri** > **güvenlik + kimlik** > **Güvenlik Merkezi** ve hello **Güvenlik Merkezi - genel bakış**  dikey penceresinde tıklatın **iş ortağı çözümleri**. Var olan Güvenlik Merkezi kullanan bir uygulama ağ geçitleri Göster hello **iş ortağı çözümleri** dikey.

![iş ortağı çözümleri][7]

Tıklatın **bağlantı uygulaması** tooopen hello **bağlantı uygulamaları** dikey penceresinde, burada, belirtilen olduğundan hello seçenekleri tooselect var olan uygulamalar. Merhaba uygulamaları tooprotect seçin ve tıklatın **Tamam**. Bu, başlangıç web uygulaması toohello arka uç havuzu hello uygulama ağ geçidi eklemez. Güvenlik Merkezi izlemek için bu hello kaynakları korumalı bir kaynak olarak ayarlar. tooadd hello kaynak bir arka uç havuzu üye olarak bu hello uygulama ağ geçidinde yapılmalıdır, hello geçerli dikey penceresinden tıklayabilirsiniz **çözüm konsolunu** hello web, ekleyebileceğiniz toohello uygulama ağ geçidi kaynağı gerçekleştirilecek toobe Uygulama toohello arka uç havuzu.

![iş ortağı çözümleri uygulamaları][6]

## <a name="finalize-configuration"></a>Yapılandırma Sonlandır

Güvenlik Merkezi parçaları uygulamaları tooan uygulama ağ geçidi korumalı bir kaynağın eklendi.  Bu kaynak hello durumunu izler ve onu bir uygulama ağ geçidi tarafından korunmasını sağlar. Hello sonraki tooadd hello özel IP, genel IP veya NIC, sanal makine toohello arka uç havuzunun hello uygulama ağ geçidi adımdır. Bu, ek bir öneri yapılana kadar **uygulama korumayı Sonlandır** hello kaynağı eklenene kadar gösterilir.

![Web uygulaması güvenlik duvarı Ekle dikey penceresi][5]

## <a name="security-alerts"></a>Güvenlik Uyarıları

Güvenlik Merkezi içinde çok gidin**ALGILAMA** > **güvenlik uyarıları**.  Burada, uygulama ağ geçitleri için WAF uyarıları bulun. Uyarıları WAF kural tarafından bölünür.

![Güvenlik Uyarıları][8]

Bir kural tıklatarak uyarıların bir listesi için bu belirli WAF kuralı sağlar. Her uyarı hello bulma hakkında ek ayrıntılar gösterir. bir bağlantı toohello uygulama ağ geçidi Hello ayrıntıları sağlayın.
 
![Uyarı ayrıntıları][9]

## <a name="next-steps"></a>Sonraki adımlar

nasıl tooenable web uygulaması Güvenlik Duvarı'nı var olan bir uygulama ağ geçidi ziyaret toolearn [oluştur veya güncelleştir web uygulaması güvenlik duvarı ile Azure uygulama ağ geçidi](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png