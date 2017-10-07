---
title: "Azure Ağ İzleyicisi ile ağ güvenlik grupları için aaaIntroduction tooflow günlüğü | Microsoft Docs"
description: "Bu sayfa toouse NSG akış Azure Ağ İzleyicisi özelliği nasıl günlüğe yazacağını açıklar"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 47d91341-16f1-45ac-85a5-e5a640f5d59e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: da85e946147b14717144cb47d1c742057c6dfa24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooflow-logging-for-network-security-groups"></a>Ağ güvenlik grupları için giriş tooflow günlüğü

Ağ güvenlik grubu akış günlükleri, giriş ve çıkış IP trafiği bir ağ güvenlik grubu aracılığıyla tooview bilgilerini sağlayan Ağ İzleyicisi özelliğidir. Bu akış günlükleri json biçiminde yazılmıştır ve giden Göster gelen akış kuralı başına temelinde hello NIC hello akış uygular, 5-tanımlama grubu ilgili bilgilere hello akış (kaynak/hedef IP, kaynak/hedef bağlantı noktası, Protokolü) ve hello varsa trafiğine izin veya engellendi.

![Akış günlükleri genel bakış][1]

Hedef ağ güvenlik grupları akış günlükleri, ancak bunlar görüntülenmez aynı hello diğer günlükler hello. Akış günlükleri hello aşağıdaki örnekte gösterildiği gibi yalnızca bir depolama hesabı ve aşağıdaki hello günlük yolu içinde depolanır:

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

aynı hello diğer açtığında görülen bekletme ilkeleri uygulamak tooflow günlükleri. Günlükleri 1 gün too365 gün ayarlanabilir bir bekletme ilkesi vardır. Hello günlükleri sonsuza kadar bir bekletme ilkesi ayarlanmamışsa saklanır.

## <a name="log-file"></a>Günlük dosyası

Akış günlükleri, birden çok özelliği vardır. Merhaba liste aşağıda hello NSG akış günlükte döndürülen hello özellikleri listesi verilmiştir:

* **zaman** - hello olayın günlüğe yazıldığı zaman zaman
* **SistemKimliği** -ağ güvenlik grubu kaynak kimliği
* **Kategori** -hello kategorisi başlangıç olayı, bu her zaman olmaya NetworkSecurityGroupFlowEvent
* **ResourceId** -kaynak hello NSG kimliğini hello
* **operationName** -her zaman NetworkSecurityGroupFlowEvents
* **Özellikler** -hello akışının özellikleri koleksiyonu
    * **Sürüm** -hello akış günlüğü olay şeması sürüm numarası
    * **Akışlar** -akışları koleksiyonu. Bu özelliği farklı kurallar için birden fazla varlık içeriyor
        * **Kural** -hangi Merhaba akışları listelenen kuralı
            * **Akışlar** -akışları koleksiyonu
                * **Mac** -hello NIC hello burada hello akış toplandı VM için MAC adresini hello
                * **flowTuples** -virgülle ayrılmış biçimde hello akış tanımlama grubu için birden çok özellik içeren bir dize
                    * **Zaman damgası** -UNIX dönem biçiminde hello akış oluştuğu sırada bu hello zaman damgası değerdir
                    * **Kaynak IP** - hello IP kaynağı
                    * **Hedef IP** -hedef IP hello
                    * **Kaynak bağlantı noktası** - hello kaynak bağlantı noktası
                    * **Hedef bağlantı noktası** -hedef bağlantı noktası hello
                    * **Protokol** -hello hello akışının protokolü. Geçerli değerler **T** TCP için ve **U** UDP için
                    * **Trafik akışı** -hello hello trafik akış yönü. Geçerli değerler **ı** gelen ve **O** için giden.
                    * **Trafik** - trafiğine izin verilen veya reddedilen olup olmadığını. Geçerli değerler **A** izin ve **D** reddedildi için.


Merhaba, akış günlüğü örneği verilmiştir. Gördüğünüz gibi hello önceki bölümde açıklanan hello özellik listesi izleyin birden çok kayıt vardır. 

> [!NOTE]
> Merhaba flowTuples özelliği virgülle ayrılmış bir liste değerler.
 
```json
{
    "records": 
    [
        
        {
             "time": "2017-02-16T22:00:32.8950000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282421,42.119.146.95,10.1.0.4,51529,5358,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282370,163.28.66.17,10.1.0.4,61771,3389,T,I,A","1487282393,5.39.218.34,10.1.0.4,58596,3389,T,I,A","1487282393,91.224.160.154,10.1.0.4,61540,3389,T,I,A","1487282423,13.76.89.229,10.1.0.4,53163,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:01:32.8960000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282481,195.78.210.194,10.1.0.4,53,1732,U,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282435,61.129.251.68,10.1.0.4,57776,3389,T,I,A","1487282454,84.25.174.170,10.1.0.4,59085,3389,T,I,A","1487282477,77.68.9.50,10.1.0.4,65078,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:02:32.9040000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282492,175.182.69.29,10.1.0.4,28918,5358,T,I,D","1487282505,71.6.216.55,10.1.0.4,8080,8080,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282512,91.224.160.154,10.1.0.4,59046,3389,T,I,A"]}]}]}
        }
        ,
        ...
```

## <a name="next-steps"></a>Sonraki adımlar

Tooenable akış ziyaret ederek nasıl günlüğe yazacağını öğrenin [günlüğü etkinleştirme akışı](network-watcher-nsg-flow-logging-portal.md).

NSG oturum açma hakkında bilgi edinin ziyaret ederek [günlük analizi için ağ güvenlik grupları (Nsg'ler)](../virtual-network/virtual-network-nsg-manage-log.md).

Trafik izin verilen veya bir VM'ye ziyaret ederek reddedilen varsa öğrenmek [IP akış ile doğrulama trafiği doğrulayın](network-watcher-check-ip-flow-verify-portal.md)

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

