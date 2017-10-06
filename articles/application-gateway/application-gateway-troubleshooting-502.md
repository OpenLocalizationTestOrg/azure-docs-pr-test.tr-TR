---
title: "aaaTroubleshoot Azure uygulama ağ geçidi hatalı ağ geçidi (502) hataları | Microsoft Docs"
description: "Bilgi nasıl tootroubleshoot uygulama ağ geçidi 502 hataları"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 1d431ead-d318-47d8-b3ad-9c69f7e08813
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: a50f736ac157256a53f6fbe3a208f0c11dd58f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a>Uygulama ağ geçidi olarak hatalı ağ geçidi hatalarında sorun giderme

Uygulama ağ geçidi kullanırken nasıl alınan tootroubleshoot hatalı ağ geçidi (502) hataları hakkında bilgi edinin.

## <a name="overview"></a>Genel Bakış

Bir uygulama ağ geçidi yapılandırdıktan sonra kullanıcılar karşılaşabilirsiniz hello hatalardan biri olan "sunucu hatası: 502 - Web sunucusu alınan geçersiz bir yanıt bir ağ geçidi veya proxy sunucu olarak çalışırken". Bu hata nedeniyle toohello aşağıdaki oluşabilir nedenler:

* Azure uygulama ağ geçidi [arka uç havuzu yapılandırılmış ya da boş değil](#empty-backendaddresspool).
* Merhaba VM'ler veya durumlarda hiçbiri [VM ölçek kümesi sağlıklı](#unhealthy-instances-in-backendaddresspool).
* Arka uç VM'ler veya VM ölçek kümesi örneklerinin [vermiyor toohello varsayılan durumu araştırması](#problems-with-default-health-probe.md).
* Geçersiz veya hatalı [özel sistem durumu araştırmalarının yapılandırmasını](#problems-with-custom-health-probe.md).
* [İstek zaman aşımı veya bağlantı sorunları](#request-time-out) kullanıcı istekleri ile.

## <a name="empty-backendaddresspool"></a>Boş BackendAddressPool

### <a name="cause"></a>Nedeni

Merhaba uygulama ağ geçidi VM veya VM ölçek kümesi hello arka uç adres havuzunda yapılandırılmış, herhangi bir müşteri istek yönlendiremezsiniz ve hatalı ağ geçidi hata oluşturur.

### <a name="solution"></a>Çözüm

Merhaba arka uç adres havuzu boş olmadığından emin olun. Bu da PowerShell'i, CLI veya portal aracılığıyla yapılabilir.

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

cmdlet'in önceki hello Hello çıktısını boş arka uç adres havuzu içermelidir. Aşağıdaki iki havuzları, burada döndürülen bir örnek verilmiştir arka uç VM'ler için FQDN veya IP adresleriyle yapılandırılmış. sağlama durumu hello BackendAddressPool hello 'başarılı' olması gerekir.

BackendAddressPoolsText:

```json
[{
    "BackendAddresses": [{
        "ipAddress": "10.0.0.10",
        "ipAddress": "10.0.0.11"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool01",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool01"
}, {
    "BackendAddresses": [{
        "Fqdn": "xyx.cloudapp.net",
        "Fqdn": "abc.cloudapp.net"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool02",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool02"
}]
```

## <a name="unhealthy-instances-in-backendaddresspool"></a>BackendAddressPool kötü durumda

### <a name="cause"></a>Nedeni

BackendAddressPool tüm hello örneklerini sağlam olmaması ise, uygulama ağ geçidi için herhangi bir arka uç tooroute kullanıcı istek bulunmaz. Arka uç örnekleri sağlıklı ancak dağıtılan hello gerekli uygulama yoksa zaman bu hello durumda olabilir.

### <a name="solution"></a>Çözüm

Merhaba örnekleri sağlıklı olduğunu ve Merhaba uygulaması'nın düzgün yapılandırıldığından emin olun. Onay hello arka uç örnekleri mümkün toorespond tooa ping içinde başka bir VM'den varsa, aynı sanal ağı hello. Ortak bir uç nokta ile yapılandırılmışsa, bir tarayıcı isteğini toohello web uygulaması tarafından bakımı yapılabilen olduğundan emin olun.

## <a name="problems-with-default-health-probe"></a>Varsayılan durumu araştırması sorunları

### <a name="cause"></a>Nedeni

502 hataları da varsayılan durumu araştırması hello sık göstergeleri olması arka uç VM'ler erişilemiyor tooreach olduğu. Bir uygulama ağ geçidi örneği sağlandığında, varsayılan sistem durumu araştırma tooeach BackendAddressPool otomatik olarak yapılandırır hello BackendHttpSetting özelliklerini kullanarak. Hiçbir kullanıcı girişi gerekli tooset Bu araştırma. Özellikle, bir Yük Dengeleme kuralı yapılandırıldığında, bir ilişki BackendHttpSetting ve BackendAddressPool arasında yapılır. Bir varsayılan araştırma her bu ilişkilerini ve uygulama ağ geçidi başlatır düzenli sistem durumu denetimi bağlantı tooeach örneğinde hello BackendAddressPool hello BackendHttpSetting öğesinde belirtilen hello bağlantı noktasında yapılandırılır. Aşağıdaki tabloda hello varsayılan durumu araştırması ile ilişkili hello değerleri listelenmektedir.

| Araştırma özelliği | Değer | Açıklama |
| --- | --- | --- |
| Araştırma URL'si |http://127.0.0.1/ |URL yolu |
| aralığı |30 |Saniye cinsinden yoklama aralığı |
| Zaman aşımı |30 |Zaman aşımı saniye cinsinden araştırma |
| Sağlıksız durum eşiği. |3 |Yeniden deneme sayısı araştırma. Merhaba arka arkaya araştırma hatası sayısı hello sağlıksız durum eşiği ulaştıktan sonra hello arka uç sunucu işaretlenmiş. |

### <a name="solution"></a>Çözüm

* Varsayılan site yapılandırıldığından ve 127.0.0.1 dinleme emin olun.
* BackendHttpSetting 80 dışında bir bağlantı noktası belirtiyorsa, bu bağlantı noktasında yapılandırılmış toolisten hello varsayılan site olmalıdır.
* Merhaba çağrısı toohttp://127.0.0.1:port bir HTTP Sonuç kodu 200 döndürmelidir. Bu hello 30 saniye zaman aşımı süresi içinde döndürülmelidir.
* Yapılandırılan bağlantı noktası açık olduğundan ve hiçbir güvenlik duvarı kurallarının veya yapılandırılmış hello bağlantı noktasında gelen veya giden trafiği engellemek Azure ağ güvenlik grupları olduğundan emin olun.
* Azure Klasik sanal makineleri veya Bulut hizmeti FQDN veya genel IP ile kullanılırsa, karşılık gelen hello olun [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) açılır.
* Merhaba VM Azure Resource Manager aracılığıyla yapılandırılır ve uygulama ağ geçidi dağıtıldığı, VNet hello dışında ise [ağ güvenlik grubu](../virtual-network/virtual-networks-nsg.md) yapılandırılmalıdır hello tooallow erişimi istenen bağlantı noktası.

## <a name="problems-with-custom-health-probe"></a>Özel durum araştırması sorunları

### <a name="cause"></a>Nedeni

Özel sistem durumu araştırmalarının ek esneklik toohello varsayılan davranışı yoklama izin verir. Özel araştırmalara kullanırken, kullanıcılar hello yoklama aralığı, hello URL ve yol tootest ve kaç tane başarısız yanıtları tooaccept hello arka uç havuzu örneği sağlıksız olarak işaretleme önce yapılandırabilir. Aşağıdaki ek özelliklere hello eklenir.

| Araştırma özelliği | Açıklama |
| --- | --- |
| Ad |Merhaba araştırma adı. Arka uç HTTP Ayarları'nda kullanılan toorefer toohello araştırma adıdır. |
| Protokol |Toosend hello araştırma kullanılan protokol. Merhaba araştırma hello arka uç HTTP Ayarları'nda tanımlanan hello protokolünü kullanır |
| Host |Ana bilgisayar adı toosend hello araştırma. Yalnızca uygulama ağ geçidinde çok siteli yapılandırıldığında uygulanabilir. Bu VM ana bilgisayar adından farklıdır. |
| Yol |Merhaba araştırma göreli yolu. Merhaba geçerli bir yol başlatır '/'. Merhaba araştırma çok gönderilen\<Protokolü\>://\<konak\>:\<bağlantı noktası\>\<yolu\> |
| aralığı |Aralığı saniye cinsinden araştırma. İki ardışık araştırmalar arasındaki hello zaman aralığını budur. |
| Zaman aşımı |Zaman aşımı saniye cinsinden araştırma. Bu zaman aşımı süresi içinde geçerli bir yanıt alınmazsa, hello araştırma başarısız olarak işaretlenir. |
| Sağlıksız durum eşiği. |Yeniden deneme sayısı araştırma. Merhaba arka arkaya araştırma hatası sayısı hello sağlıksız durum eşiği ulaştıktan sonra hello arka uç sunucu işaretlenmiş. |

### <a name="solution"></a>Çözüm

Özel durumu araştırma tablo önceki hello doğru bir şekilde yapılandırıldığından bu hello doğrulayın. Ayrıca toohello önceki sorun giderme adımları, ayrıca olun hello aşağıdaki:

* Bu hello araştırma göredir hello doğru belirtildiğinden emin olun [Kılavuzu](application-gateway-create-probe-ps.md).
* Uygulama ağ geçidi tek bir site için yapılandırılmışsa, varsayılan hello ana bilgisayar tarafından adı '127.0.0.1', içinde özel araştırma aksi belirtilmedikçe belirtilmesi gerekir.
* Çağrı toohttp emin olun: / /\<konak\>:\<bağlantı noktası\>\<yolu\> 200 bir HTTP Sonuç kodu döndürür.
* Aralık, zaman aşımı ve UnhealtyThreshold hello kabul edilebilir aralık içinde olduğundan emin olun.
* Bir HTTPS kullanarak araştırma hello arka uç sunucu hello arka uç sunucusunun kendisi üzerinde bir geri dönüş sertifikası yapılandırarak SNI gerektirmeyen emin olun. 
* Aralık, zaman aşımı ve UnhealtyThreshold hello kabul edilebilir aralık içinde olduğundan emin olun.

## <a name="request-time-out"></a>İstek zaman aşımı

### <a name="cause"></a>Nedeni

Bir kullanıcı isteği alındığında, uygulama ağ geçidi yapılandırılmış hello kuralları toohello isteği uygular ve tooa arka uç havuzu örnek yönlendirir. Merhaba arka uç örnek yanıt süresinin yapılandırılabilir bir zaman aralığı için bekler. Varsayılan olarak, bu aralığıdır **30 saniye**. Uygulama ağ geçidi, bu aralıkta arka uç uygulamasından bir yanıt alamazsa, kullanıcı isteği 502 bir hata görür.

### <a name="solution"></a>Çözüm

Uygulama ağ geçidi olabilir sonra toodifferent havuzları uygulanan BackendHttpSetting aracılığıyla bu ayarı kullanıcıların tooconfigure sağlar. Farklı arka uç havuzları farklı BackendHttpSetting ve bu nedenle farklı istek zaman aşımına yapılandırılmış olabilir.

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a>Sonraki adımlar

Merhaba önceki adımları hello sorunu çözmezse, açık bir [destek bileti](https://azure.microsoft.com/support/options/).

