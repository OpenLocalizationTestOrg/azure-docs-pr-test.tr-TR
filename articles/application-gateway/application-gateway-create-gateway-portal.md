---
title: "aaaCreate bir uygulama ağ geçidi - Azure portalı | Microsoft Docs"
description: "Nasıl toocreate kullanarak uygulama ağ geçidi hello portal öğrenin"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 54dffe95-d802-4f86-9e2e-293f49bd1e06
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 24c1d5701eae372cd233162ceb58dea36a3b6a39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-hello-portal"></a>Merhaba portal ile bir uygulama ağ geçidi oluşturma

[Uygulama ağ geçidi](application-gateway-introduction.md) olan çeşitli katman 7 Yük Dengeleme, uygulamanız için sunumu bir hizmet olarak uygulama teslim Denetleyicisi'ni (ADC) sağlayan ayrılmış bir sanal uygulama. Bu makalede bir uygulama hello Azure portal kullanarak ve arka uç üye olarak var olan bir sunucu ekleme ağ geçidi hello adımları toocreate alır.

## <a name="log-in-tooazure"></a>İçinde tooAzure oturum

Azure Portalı ' toohello oturum [http://portal.azure.com](http://portal.azure.com)

## <a name="create-application-gateway"></a>Uygulama ağ geçidi oluşturma

toocreate bir uygulama ağ geçidi izleyin tam hello adımları. Uygulama ağ geçidi, kendi alt gerektirir. Bir sanal ağ oluştururken, birden çok alt ağı yeterli adres alanı toohave bıraktığınızdan emin olun. Dağıtılan tooa alt Hello uygulama ağ geçidi olduktan sonra yalnızca başka uygulama ağ geçitleri tooit eklenebilir.

1. Merhaba Sık Kullanılanlar hello portalı bölmesinde **yeni**
1. Merhaba, **yeni** dikey penceresinde tıklatın **ağ**. Merhaba, **ağ** dikey penceresinde tıklatın **uygulama ağ geçidi**hello görüntü aşağıdaki gösterildiği gibi:

    ![Uygulama ağ geçidi oluşturma][1]

1. Merhaba, **Temelleri** görüntülenirse, dikey hello aşağıdaki değerleri girin ve ardından **Tamam**:

   | **Ayar** | **Değer** | **Ayrıntılar**|
   |---|---|---|
   |**Ad**|AdatumAppGateway|Merhaba uygulama ağ geçidi Hello adı|
   |**Katmanı**|Standart|Standart ve WAF değerleri kullanılabilir. Ziyaret [web uygulaması güvenlik duvarı](application-gateway-web-application-firewall-overview.md) toolearn WAF hakkında daha fazla bilgi.|
   |**SKU boyutu**|Orta|Standart katmanı seçildiğinde küçük, Orta ve büyük seçimlerdir. WAF katmanı seçerken, Orta ve büyük yalnızca seçeneklerdir.|
   |**Örnek sayısı**|2|Merhaba uygulama ağ geçidi yüksek kullanılabilirlik için örnek sayısı. Örnek sayısı 1 yalnızca sınama amacıyla kullanılmalıdır.|
   |**Abonelik**|[Aboneliğiniz]|Bir abonelik toocreate hello uygulama ağ geçidi seçin.|
   |**Kaynak grubu**|**Yeni Oluştur:** AdatumAppGatewayRG|Bir kaynak grubu oluşturun. Merhaba kaynak grubu adı, seçtiğiniz hello abonelik içinde benzersiz olmalıdır. Merhaba okuyun, kaynak grupları hakkında daha fazla toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) genel bakış makalesi.|
   |**Konum**|Batı ABD||

1. Merhaba, **ayarları** altında görüntülenen dikey **sanal ağ**, tıklatın **sanal ağ seçin**. Merhaba **Seç sanal ağ** dikey pencere açılır.  Tıklatın **Yeni Oluştur** tooopen hello **sanal ağ oluştur** dikey.

   ![sanal ağ seçin][2]

1. Merhaba üzerinde **oluşturma sanal ağ dikey** hello aşağıdaki değerleri girin ve ardından **Tamam**. Merhaba **sanal ağ oluştur** ve **Seç sanal ağ** dikey pencereleri kapatın. Bu adım hello doldurur **alt** hello alanını **ayarları** seçilen hello alt dikey.

   | **Ayar** | **Değer** | **Ayrıntılar**|
   |---|---|---|
   |**Ad**|AdatumAppGatewayVNET|Merhaba uygulama ağ geçidi adı|
   |**Adres alanı**|10.0.0.0/16|Merhaba sanal ağın adres alanı hello budur|
   |**Alt ağ adı**|AppGatewaySubnet|Merhaba uygulama ağ geçidi için hello alt ağ adı|
   |**Alt ağ adres aralığı**|10.0.0.0/28|Bu alt ağ daha fazla ek alt ağlar hello sanal ağında arka uç havuzu üyeleri için izin verir|

1. Merhaba üzerinde **ayarları** altında dikey **ön uç IP yapılandırmasını**, seçin **ortak** hello olarak **IP adresi türü**

1. Hello üzerinde **ayarları** altında dikey **genel IP adresi** tıklatın **genel bir IP adresi seçin**, hello **genel IP adresi seçin** dikey penceresini açar , tıklatın **Yeni Oluştur**.

   ![genel IP seçin][3]

1. Merhaba üzerinde **ortak IP adresi oluştur** dikey penceresinde hello varsayılan değeri kabul edin ve tıklatın **Tamam**. Merhaba dikey penceresi kapanır ve hello doldurur **genel IP adresi** seçilen hello ortak IP adresine sahip.

1. Merhaba üzerinde **ayarları** altında dikey **dinleyici Yapılandırması**, tıklatın **HTTP** altında **Protokolü**. Başlangıç bağlantı noktası toouse hello girin **bağlantı noktası** alan.

2. Tıklatın **Tamam** hello üzerinde **ayarları** dikey toocontinue.

1. Merhaba hello ayarlarını gözden geçirin **Özet** tıklayın ve dikey **Tamam** hello uygulama ağ geçidi toostart oluşturma. Bir uygulama ağ geçidi oluşturma, uzun süre çalışan bir görevdir ve zaman toocomplete alır.

## <a name="add-servers-toobackend-pools"></a>Sunucuları toobackend havuzları ekleme

Merhaba uygulama ağ geçidi oluşturduktan sonra hello uygulama toobe yük dengeli ana bilgisayar hello sistemlerinin hala toobe eklenen toohello uygulama ağ geçidi gerekir. Merhaba IP adresleri, FQDN veya bu sunucuların NIC'ler toohello arka uç adres havuzlarında eklenir.

### <a name="ip-address-or-fqdn"></a>IP adresi veya FQDN

1. Hello Azure portalında oluşturulan hello uygulama ağ geçidi ile **Sık Kullanılanlar** bölmesinde tıklatın **tüm kaynakları**. Merhaba tıklatın **AdatumAppGateway** uygulama ağ geçidi'nde hello tüm kaynak dikey. Merhaba aboneliği zaten içinde birçok kaynak varsa, girebilirsiniz **AdatumAppGateway** hello içinde **ada göre Filtrele...** kutusunu tooeasily erişim hello uygulama ağ geçidi.

1. oluşturduğunuz hello uygulama ağ geçidi görüntülenir. Tıklatın **arka uç havuzları**ve hello geçerli arka uç havuzunu **appGatewayBackendPool**, hello **appGatewayBackendPool** dikey pencere açılır.

   ![Uygulama ağ geçidi arka uç havuzları][4]

1. Tıklatın **hedef Ekle** FQDN değerlerini tooadd IP adreslerini. Seçin **IP adresi veya FQDN** hello olarak **türü** ve IP adresi veya FQDN hello alanına girin. Ek arka uç havuzu üyeleri için bu adımı yineleyin. Tıklatın tamamlanınca **kaydetmek**.

### <a name="virtual-machine-and-nic"></a>Sanal makine ve NIC

Bu gibi durumlarda, sanal makine NIC de arka uç havuzu üyeleri ekleyebilirsiniz. Aynı sanal ağ hello uygulama ağ geçidi aracılığıyla kullanılabilen hello yalnızca sanal makinelerde açılır hello.

1. Hello Azure portalında oluşturulan hello uygulama ağ geçidi ile **Sık Kullanılanlar** bölmesinde tıklatın **tüm kaynakları**. Merhaba tıklatın **AdatumAppGateway** uygulama ağ geçidi'nde hello tüm kaynak dikey. Merhaba aboneliği zaten içinde birçok kaynak varsa, girebilirsiniz **AdatumAppGateway** hello içinde **ada göre Filtrele...** kutusunu tooeasily erişim hello uygulama ağ geçidi.

1. oluşturduğunuz hello uygulama ağ geçidi görüntülenir. Tıklatın **arka uç havuzları**ve hello geçerli arka uç havuzunu **appGatewayBackendPool**, hello **appGatewayBackendPool** dikey pencere açılır.

   ![Uygulama ağ geçidi arka uç havuzları][5]

1. Tıklatın **hedef Ekle** FQDN değerlerini tooadd IP adreslerini. Seçin **sanal makine** hello olarak **türü** ve hello sanal makine ve NIC toouse seçin. Tıklatın tamamlanınca **Kaydet**

   > [!NOTE]
   > Merhaba açılan kutuda bulunan Hello uygulama ağ geçidi olarak yalnızca sanal makineleri aynı sanal ağ hello.

## <a name="clean-up-resources"></a>Kaynakları temizleme

Artık gerektiğinde Merhaba kaynak grubu, uygulama ağ geçidi ve tüm ilişkili kaynakları silin. toodo hello uygulama ağ geçidi dikey ve tıklatın hello kaynak grubu, seçin **silmek**.

## <a name="next-steps"></a>Sonraki adımlar

Bu senaryoda, bir uygulama ağ geçidi dağıtılmış ve bir sunucu toohello arka uç eklenir. Merhaba sonraki tooconfigure hello uygulama ağ geçidi ayarlarını değiştirme ve ayarlama kuralları hello ağ geçidi tarafından adımlardır. Bu adımları makaleler hello ziyaret ederek bulunabilir:

Nasıl toocreate özel durumu ziyaret ederek yoklamaları öğrenin [bir özel durum araştırması oluştur](application-gateway-create-probe-portal.md)

Nasıl tooconfigure SSL boşaltma ve Al hello maliyetli SSL şifre çözme ziyaret ederek, web sunucuları kapalı öğrenin [SSL boşaltma yapılandırın](application-gateway-ssl-portal.md)

Bilgi nasıl tooprotect uygulamalarınızla [Web uygulaması güvenlik duvarı](application-gateway-webapplicationfirewall-overview.md) uygulama ağ geçidi özelliğidir.

<!--Image references-->
[1]: ./media/application-gateway-create-gateway-portal/figure1.png
[2]: ./media/application-gateway-create-gateway-portal/figure2.png
[3]: ./media/application-gateway-create-gateway-portal/figure3.png
[4]: ./media/application-gateway-create-gateway-portal/figure4.png
[5]: ./media/application-gateway-create-gateway-portal/figure5.png
[scenario]: ./media/application-gateway-create-gateway-portal/scenario.png
