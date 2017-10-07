---
title: "Azure kaynaklarınızı ile Azure DNS aaaIntegrate | Microsoft Docs"
description: "Bilgi nasıl toouse Azure DNS Azure kaynaklarınız için DNS tooprovide boyunca."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: b9b6f829513f0ad9da510190c75bc60dc7431545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-dns-tooprovide-custom-domain-settings-for-an-azure-service"></a>Azure DNS tooprovide özel etki alanı ayarları için bir Azure hizmeti kullanın

Azure DNS destek özel etki alanları veya, bir tam etki alanı adı (FQDN) sahip herhangi bir Azure kaynaklarınızı için özel bir etki alanı için DNS sağlar. Azure web uygulaması varsa ve kullanıcıları tooaccess istiyorsanız örneğidir ya da tarafından contoso.com ya da www.contoso.com bir FQDN kullanarak. Bu makalede özel etki alanlarını kullanmak için Azure hizmeti Azure DNS ile yapılandıracağınız anlatılmaktadır.

## <a name="prerequisites"></a>Ön koşullar

Sipariş toouse içinde Azure DNS etki alanınız için öncelikle, etki alanı tooAzure DNS temsilci gerekir. Ziyaret [bir etki alanı tooAzure DNS temsilci](./dns-delegate-domain-azure-dns.md) yönelik yönergeler tooconfigure adı sunucularınız için temsilci. Etki alanınızı temsilci tooyour Azure DNS bölgesi olduğunda, gereken mümkün tooconfigure hello DNS kayıtlarını demektir.

Bir gösterim veya özel etki alanı için yapılandırabileceğiniz [Azure işlev uygulamalarının](#azure-function-app), [Azure IOT](#azure-iot), [ortak IP adresleri](#public-ip-address), [uygulama hizmeti (Web uygulamaları)](#app-service-web-apps), [Blob storage](#blob-storage), ve [Azure CDN](#azure-cdn).

## <a name="azure-function-app"></a>Azure işlev uygulaması

tooconfigure Azure işlevi uygulamalar için özel bir etki alanı, hello işlev uygulaması kendisini yapılandırmasına yanı sıra bir CNAME kaydı oluşturulur.
 
Çok gidin**diğer** > **işlev uygulaması** ve işlev uygulamanızı seçin. Tıklatın **Platform özellikleri** ve altında **ağ** tıklatın **özel etki alanları**.

![işlev uygulaması dikey](./media/dns-custom-domain/functionapp.png)

Not hello geçerli url hello üzerinde **özel etki alanları** dikey penceresinde, bu adres hello diğer ad olarak oluşturulan hello DNS kaydı için kullanılır.

![özel etki alanı dikey penceresi](./media/dns-custom-domain/functionshostname.png)

Tooyour DNS bölgesi gidin ve tıklayın **+ kayıt kümesine**. Merhaba hello üzerinde aşağıdaki bilgilerle doldurun **kayıt kümesi ekleme** tıklayın ve dikey **Tamam** toocreate onu.

|Özellik  |Değer  |Açıklama  |
|---------|---------|---------|
|Ad     | myfunctionapp        | Bu değer hello etki alanı adı etiketi birlikte hello FQDN hello özel etki alanı adı için kullanılabilir.        |
|Tür     | CNAME        | Kullanım bir CNAME kaydı bir diğer ad kullanıyor.        |
|TTL     | 1        | 1 1 saat boyunca kullanılır        |
|TTL birim     | Saat        | Saat hello zaman ölçümü kullanılır         |
|Diğer ad     | adatumfunction.azurewebsites.NET        | Hello DNS adı varsayılan toohello işlevi uygulama tarafından sağlanan hello adatumfunction.azurewebsites.net DNS adının olduğundan bu örnekte, hello diğer oluşturuyorsunuz.        |

Geri tooyour işlevi uygulamasına gidin, tıklatın **Platform özellikleri**ve altında **ağ** tıklatın **özel etki alanları**, altında **ana bilgisayar adları**tıklatın **+ ana bilgisayar adını eklemek**.

Merhaba üzerinde **ana bilgisayar adını eklemek** dikey penceresinde hello CNAME kaydı hello girin **ana bilgisayar adı** metin alanı ve tıklatın **doğrulama**. Merhaba kayıt bulundu mümkün toobe olduysa, hello **ana bilgisayar adını eklemek** düğmesi görünür. Tıklatın **ana bilgisayar adını eklemek** tooadd hello diğer adı.

![ana bilgisayar adı dikey işlevi uygulamalar ekleme](./media/dns-custom-domain/functionaddhostname.png)

## <a name="azure-iot"></a>Azure IoT

Azure IOT hello hizmette kendisini gerekli özelleştirmeler yok. bir CNAME kaydı toohello kaynakları işaret yalnızca toouse bir IOT Hub ile özel bir etki alanı gereklidir.

Çok gidin**nesnelerin interneti** > **IOT hub'ı** ve IOT hub'ı seçin. Merhaba üzerinde **genel bakış** dikey penceresinde, Not hello hello IOT hub'ı FQDN'si.

![IOT hub'ı dikey penceresi](./media/dns-custom-domain/iot.png)

Ardından, tooyour DNS bölgesi gidin ve tıklayın **+ kayıt kümesine**. Merhaba hello üzerinde aşağıdaki bilgilerle doldurun **kayıt kümesi ekleme** tıklayın ve dikey **Tamam** toocreate onu.


|Özellik  |Değer  |Açıklama  |
|---------|---------|---------|
|Ad     | myiothub        | Bu değer hello etki alanı adı etiketi ile birlikte hello FQDN hello IOT hub'ına yönelik değildir.        |
|Tür     | CNAME        | Kullanım bir CNAME kaydı bir diğer ad kullanıyor.
|TTL     | 1        | 1 1 saat boyunca kullanılır        |
|TTL birim     | Saat        | Saat hello zaman ölçümü kullanılır         |
|Diğer ad     | adatumIOT.azure devices.net        | Hello DNS adı hello IOT hub tarafından sağlanan hello adatumIOT.azure devices.net ana bilgisayar adı olduğundan bu örnekte, hello diğer oluşturuyorsunuz.

Merhaba kayıt oluşturulduktan sonra hello CNAME kaydı kullanarak ad çözümlemesini test`nslookup`

## <a name="public-ip-address"></a>Genel IP adresi

Uygulama ağ geçidi, yük dengeleyici, bulut hizmeti, Resource Manager VM'ler gibi kaynak adres tooconfigure bir genel IP kullanan hizmetler için özel bir etki alanı ve klasik sanal makineleri, bir CNAME kaydı kullanılır.

Çok gidin**ağ** > **genel IP adresi**, hello genel IP kaynağı seçin ve tıklatın **yapılandırma**. Başlangıç IP adresi gösterilen bildirmek.

![genel IP dikey penceresi](./media/dns-custom-domain/publicip.png)

Tooyour DNS bölgesi gidin ve tıklayın **+ kayıt kümesine**. Merhaba hello üzerinde aşağıdaki bilgilerle doldurun **kayıt kümesi ekleme** tıklayın ve dikey **Tamam** toocreate onu.


|Özellik  |Değer  |Açıklama  |
|---------|---------|---------|
|Ad     | mywebserver        | Bu değer hello etki alanı adı etiketi birlikte hello FQDN hello özel etki alanı adı için kullanılabilir.        |
|Tür     | A        | Bir A kaydı Hello kaynak IP adresi olarak kullanın.        |
|TTL     | 1        | 1 1 saat boyunca kullanılır        |
|TTL birim     | Saat        | Saat hello zaman ölçümü kullanılır         |
|IP Adresi     | <your ip address>       | Merhaba genel IP adresi.|

![bir A kaydını oluşturun](./media/dns-custom-domain/arecord.png)

Merhaba A kaydı oluşturulduktan sonra çalıştırmak `nslookup` toovalidate hello kayıt giderir.

![genel IP dns araması](./media/dns-custom-domain/publicipnslookup.png)

## <a name="app-service-web-apps"></a>Uygulama Hizmeti (Web uygulamaları)

Merhaba aşağıdaki adımlar, bir app service web uygulaması için özel bir etki alanı nasıl yapılandıracağınız uygulayın.

Çok gidin**Web ve mobil** > **uygulama hizmeti** seçip bir özel etki alanı adı yapılandırma ve tıklatın hello kaynak **özel etki alanları**.

Not hello geçerli url hello üzerinde **özel etki alanları** dikey penceresinde, bu adres hello diğer ad olarak oluşturulan hello DNS kaydı için kullanılır.

![özel etki alanlarını dikey penceresi](./media/dns-custom-domain/url.png)

Tooyour DNS bölgesi gidin ve tıklayın **+ kayıt kümesine**. Merhaba hello üzerinde aşağıdaki bilgilerle doldurun **kayıt kümesi ekleme** tıklayın ve dikey **Tamam** toocreate onu.


|Özellik  |Değer  |Açıklama  |
|---------|---------|---------|
|Ad     | mywebserver        | Bu değer hello etki alanı adı etiketi birlikte hello FQDN hello özel etki alanı adı için kullanılabilir.        |
|Tür     | CNAME        | Kullanım bir CNAME kaydı bir diğer ad kullanıyor. Merhaba kaynak IP adresi kullanıldığında, bir A kaydı olarak kullanılır.        |
|TTL     | 1        | 1 1 saat boyunca kullanılır        |
|TTL birim     | Saat        | Saat hello zaman ölçümü kullanılır         |
|Diğer ad     | webserver.azurewebsites.NET        | Hello DNS adı varsayılan toohello web uygulama tarafından sağlanan hello webserver.azurewebsites.net DNS adının olduğundan bu örnekte, hello diğer oluşturuyorsunuz.        |


![Bir CNAME kaydı oluşturun](./media/dns-custom-domain/createcnamerecord.png)

Merhaba özel etki alanı adı için yapılandırılmış geri toohello uygulama hizmeti gidin. Tıklatın **özel etki alanları**, ardından **ana bilgisayar adları**. oluşturduğunuz tooadd hello CNAME kaydı, tıklatın **+ ana bilgisayar adını eklemek**.

![Şekil 1](./media/dns-custom-domain/figure1.png)

Merhaba işlemi tamamlandıktan sonra çalıştırmak **nslookup** toovalidate ad çözümlemesinin çalıştığından.

![Şekil 1](./media/dns-custom-domain/finalnslookup.png)

özel etki alanı tooApp hizmeti eşleme hakkında daha fazla toolearn ziyaret [bir var olan özel DNS adı tooAzure Web Apps eşleme](../app-service-web/app-service-web-tutorial-custom-domain.md?toc=%dns%2ftoc.json).

Özel bir etki alanı toopurchase gerekiyorsa, ziyaret [Azure Web uygulamaları için özel etki alanı adı satın](../app-service-web/custom-dns-web-site-buydomains-web-app.md) toolearn uygulama hizmeti etki alanları hakkında daha fazla.

## <a name="blob-storage"></a>Blob depolama

Merhaba aşağıdaki adımlar, hello asverify yöntemini kullanarak bir blob depolama hesabı için bir CNAME kaydı nasıl yapılandıracağınız uygulayın. Bu yöntem kapalı kalma süresi sağlar.

Çok gidin**depolama** > **depolama hesapları**, depolama hesabınızı seçin ve tıklatın **özel etki alanı**. 2. adım altında Hello FQDN bildirmek, bu değer kullanılır toocreate hello ilk CNAME kaydı

![BLOB Depolama özel etki alanı](./media/dns-custom-domain/blobcustomdomain.png)

Tooyour DNS bölgesi gidin ve tıklayın **+ kayıt kümesine**. Merhaba hello üzerinde aşağıdaki bilgilerle doldurun **kayıt kümesi ekleme** tıklayın ve dikey **Tamam** toocreate onu.


|Özellik  |Değer  |Açıklama  |
|---------|---------|---------|
|Ad     | asverify.mystorageaccount        | Bu değer hello etki alanı adı etiketi birlikte hello FQDN hello özel etki alanı adı için kullanılabilir.        |
|Tür     | CNAME        | Kullanım bir CNAME kaydı bir diğer ad kullanıyor.        |
|TTL     | 1        | 1 1 saat boyunca kullanılır        |
|TTL birim     | Saat        | Saat hello zaman ölçümü kullanılır         |
|Diğer ad     | asverify.adatumfunctiona9ed.BLOB.Core.Windows.NET        | Hello DNS adı varsayılan toohello depolama hesabı tarafından sağlanan hello asverify.adatumfunctiona9ed.blob.core.windows.net DNS adının olduğundan bu örnekte, hello diğer oluşturuyorsunuz.        |

Tıklayarak geri tooyour depolama hesabına gidin **depolama** > **depolama hesapları**, depolama hesabınızı seçin ve tıklatın **özel etki alanı**. Alias oluşturduğunuz hello asverify öneki hello metin kutusundaki onay olmadan hello türü ** dolaylı CNAME doğrulaması kullan ve tıklayın **kaydetmek**. Bu adım tamamlandıktan sonra tooyour DNS bölgesi dönüp hello asverify öneki olmadan bir CNAME kaydı oluşturun.  Noktayı sonra güvenli toodelete hello CNAME kaydı hello cdnverify önekine sahip olursunuz.

![BLOB Depolama özel etki alanı](./media/dns-custom-domain/indirectvalidate.png)

DNS çözümlemesi çalıştırarak doğrula`nslookup`

bir özel etki alanı tooa blob storage uç eşleme hakkında daha fazla ziyaret toolearn [Blob storage uç noktanız için özel etki alanı adı yapılandırma](../storage/blobs/storage-custom-domain-name.md?toc=%dns%2ftoc.json)

## <a name="azure-cdn"></a>Azure CDN

Merhaba aşağıdaki adımlar, hello cdnverify yöntemini kullanarak bir CDN uç noktası için bir CNAME kaydı nasıl yapılandıracağınız uygulayın. Bu yöntem kapalı kalma süresi sağlar.

Çok gidin**ağ** > **CDN profili**CDN profilinizi seçin ve tıklatın **uç noktaları** altında **genel**.

İle çalışma ve tıklayın hello uç nokta seçin **+ özel etki alanı**. Not hello **uç noktası ana bilgisayar adı** bu değer hello kayıt olduğundan bu hello CNAME kaydı işaret eder.

![CDN özel etki alanı](./media/dns-custom-domain/endpointcustomdomain.png)

Tooyour DNS bölgesi gidin ve tıklayın **+ kayıt kümesine**. Merhaba hello üzerinde aşağıdaki bilgilerle doldurun **kayıt kümesi ekleme** tıklayın ve dikey **Tamam** toocreate onu.

|Özellik  |Değer  |Açıklama  |
|---------|---------|---------|
|Ad     | cdnverify.mycdnendpoint        | Bu değer hello etki alanı adı etiketi birlikte hello FQDN hello özel etki alanı adı için kullanılabilir.        |
|Tür     | CNAME        | Kullanım bir CNAME kaydı bir diğer ad kullanıyor.        |
|TTL     | 1        | 1 1 saat boyunca kullanılır        |
|TTL birim     | Saat        | Saat hello zaman ölçümü kullanılır         |
|Diğer ad     | cdnverify.adatumcdnendpoint.azureedge.NET        | Hello DNS adı varsayılan toohello depolama hesabı tarafından sağlanan hello cdnverify.adatumcdnendpoint.azureedge.net DNS adının olduğundan bu örnekte, hello diğer oluşturuyorsunuz.        |

Tıklayarak geri tooyour CDN uç noktası gidin **ağ** > **CDN profili**, CDN profilinizi seçin. Tıklatın **+ özel etki alanı** hello cdnverify öneki olmadan CNAME kaydı diğer adınızı girin ve tıklatın **Ekle**.

Bu adım tamamlandıktan sonra tooyour DNS bölgesi dönüp hello cdnverify öneki olmadan bir CNAME kaydı oluşturun.  Noktayı sonra güvenli toodelete hello CNAME kaydı hello cdnverify önekine sahip olursunuz. CDN hakkında daha fazla bilgi ve nasıl özel bir etki alanı hello Ara kayıt adım olmadan tooconfigure ziyaret [harita Azure CDN içerik tooa özel etki alanı](../cdn/cdn-map-content-to-custom-domain.md?toc=%dns%2ftoc.json).

## <a name="next-steps"></a>Sonraki adımlar

Nasıl çok öğrenin[geriye doğru DNS Azure içinde barındırılan hizmetler için yapılandırma](dns-reverse-dns-for-azure-services.md).
