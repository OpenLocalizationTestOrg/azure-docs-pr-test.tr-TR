---
title: "Azure Ağ İzleyicisi aaaIntroduction tooconnectivity iade | Microsoft Docs"
description: "Bu sayfa hello Ağ İzleyicisi bağlantı yeteneğini genel bir bakış sağlar"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 52fc4547f167cea2992a046859dc0550d136e80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooconnectivity-check-in-azure-network-watcher"></a>Azure Ağ İzleyicisi giriş tooconnectivity denetleyin

Merhaba bağlantı özelliği olan Ağ İzleyicisi Merhaba yetenek toocheck bir sanal makine tooa sanal makineden (VM), tam etki alanı adı (FQDN) URI, doğrudan bir TCP bağlantı sağlar ya da IPv4 adresi. Ağ senaryoları karmaşık, ağ güvenlik grupları, güvenlik duvarları, kullanıcı tanımlı yollar ve Azure tarafından sağlanan kaynaklar kullanılarak uygulanır. Karmaşık Yapılandırmalar bağlantı sorunlarını giderme zor olun. Ağ İzleyicisi zaman toofind hello miktarını azaltın ve bağlantısı sorunlarını algılayacak yardımcı olur. döndürülen hello sonuçları bir bağlantı sorunu tooa platform veya kullanıcı yapılandırma sorunu olup içine Öngörüler sağlayabilir. Bağlantı kontrol edileceği ile [PowerShell](network-watcher-connectivity-powershell.md), [Azure CLI](network-watcher-connectivity-cli.md), ve [REST API](network-watcher-connectivity-rest.md).

> [!IMPORTANT]
> Bağlantı onay gerektiren bir sanal makine uzantısı `AzureNetworkWatcherExtension`. Bir Windows VM Hello uzantısı yüklemek için ziyaret [Windows için Azure Ağ İzleyicisi Aracısı sanal makine uzantısı](../virtual-machines/windows/extensions-nwa.md) ve Linux VM ziyaret edin: [Azure Ağ İzleyicisi Aracısı sanal makine uzantısı Linuxiçin](../virtual-machines/linux/extensions-nwa.md).

## <a name="response"></a>Yanıt

Aşağıdaki tablonun hello bağlantı denetimi çalışmasını bitirdikten sonra döndürülen hello özellikleri gösterir.

|Özellik  |Açıklama  |
|---------|---------|
|ConnectionStatus     | Merhaba bağlantı denetimi Hello durumu. Olası sonuçları **erişilebilir** ve **ulaşılamıyor**.        |
|AvgLatencyInMs     | Ortalama gecikme süresi sırasında hello bağlantı denetimi milisaniye cinsinden. (Yalnızca durumunu denetleme erişilebilir olup olmadığını gösterilen)        |
|MinLatencyInMs     | Merhaba bağlantı sırasında en düşük gecikme süresi, milisaniye cinsinden denetleyin. (Yalnızca durumunu denetleme erişilebilir olup olmadığını gösterilen)        |
|MaxLatencyInMs     | Merhaba bağlantı sırasında en fazla gecikme süresi, milisaniye cinsinden denetleyin. (Yalnızca durumunu denetleme erişilebilir olup olmadığını gösterilen)        |
|ProbesSent     | Merhaba denetimi sırasında gönderilen araştırmalar sayısı. En yüksek değer 100'dür.        |
|ProbesFailed     | Merhaba denetimi sırasında başarısız araştırmalar sayısı. En yüksek değer 100'dür.        |
|Atlama     | Kaynak toodestination gelen atlama atlama yoluyla.        |
|[] Atlama sayısı. Türü     | Kaynak türü. Olası değerler şunlardır: **kaynak**, **değerinin VirtualAppliance**, **VnetLocal**, ve **Internet**.        |
|[] Atlama sayısı. Kimliği | Merhaba atlama benzersiz tanımlayıcısı.|
|[] Atlama sayısı. Adres | Merhaba atlamanın IP adresi.|
|[] Atlama sayısı. ResourceId | Merhaba atlama bir Azure kaynağı ise hello atlama ResourceId. Bu bir Internet kaynağına ResourceId ise, **Internet**. |
|[] Atlama sayısı. NextHopIds | Merhaba hello sonraki atlamanın gerçekleştirilecek benzersiz tanımlayıcısı.|
|[] Atlama sayısı. Sorunları | Bu atlama hello denetimi sırasında karşılaşılan sorunlar koleksiyonu. Herhangi bir sorun olsaydı, hello değeri boştur.|
|[] Atlama sayısı. [] Verir. Kaynak | Sorun oluştuğu hello geçerli atlamada. Olası değerler şunlardır:<br/> **Gelen** -sorundur hello önceki atlama toohello geçerli atlama hello bağlantısından üzerinde<br/>**Giden** -sorundur hello geçerli atlama toohello sonraki atlama hello bağlantısından üzerinde<br/>**Yerel** -hello geçerli atlamada bir sorundur.|
|[] Atlama sayısı. [] Verir. Önem derecesi | Merhaba önem derecesi hello sorunu algılandı. Olası değerler şunlardır: **hata** ve **uyarı**. |
|[] Atlama sayısı. [] Verir. Türü |Merhaba türü sorun bulundu. Olası değerler şunlardır: <br/>**CPU**<br/>**Bellek**<br/>**GuestFirewall**<br/>**DnsResolution**<br/>**NetworkSecurityRule**<br/>**UserDefinedRoute** |
|[] Atlama sayısı. [] Verir. Bağlam |Merhaba sorun bulundu ilişkin ayrıntılar.|
|[] Atlama sayısı. [] Verir. Bağlam [] .key |Merhaba anahtar değer çifti anahtarı döndürüldü.|
|[] Atlama sayısı. [] Verir. Bağlam [] .value |Merhaba anahtar değer çifti değer döndürdü.|

Merhaba, atlama üzerinde bulunan bir sorun örneği aşağıdadır.

```json
"Issues": [
    {
        "Origin": "Outbound",
        "Severity": "Error",
        "Type": "NetworkSecurityRule",
        "Context": [
            {
                "key": "RuleName",
                "value": "UserRule_Port80"
            }
        ]
    }
]
```
## <a name="fault-types"></a>Hata türleri

Merhaba bağlantı denetimi hello bağlantısı ile ilgili hata türlerini döndürür. Merhaba aşağıdaki tabloda döndürülen hello geçerli hata türlerinin bir listesini sağlar.

|Tür  |Açıklama  |
|---------|---------|
|CPU     | Yüksek CPU kullanımı.       |
|Bellek     | Yüksek bellek kullanımı.       |
|GuestFirewall     | Trafik tooa sanal makine güvenlik duvarı yapılandırması engellendi.        |
|DNSResolution     | Merhaba hedef adresi için DNS çözümlemesi başarısız oldu.        |
|NetworkSecurityRule    | Trafik bir NSG kuralı tarafından engellenmiş (Kural döndürülür)        |
|UserDefinedRoute|Trafik tooa kullanıcı tanımlı veya sistem yolu bırakılır. |

### <a name="next-steps"></a>Sonraki adımlar

Bilgi nasıl tooverify bağlantı tooa kaynak şu adresi ziyaret ederek: [Azure Ağ İzleyicisi ile Bağlanılırlığı denetleyin](network-watcher-connectivity-powershell.md).

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png

