---
title: "Azure Linux VM'ler için olayları zamanlanmış | Microsoft Docs"
description: "Olaylar, Linux sanal makineleriniz için Azure meta veri hizmeti kullanarak zamanlayabilirsiniz."
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: ae9955253647f3277729e7905baf7bb07645de42
ms.sourcegitcommit: 0e1c4b925c778de4924c4985504a1791b8330c71
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/06/2018
---
# <a name="azure-metadata-service-scheduled-events-preview-for-linux-vms"></a>Azure meta veri hizmeti: Linux VM'ler zamanlanmış olaylar (Önizleme)

> [!NOTE] 
> Kullanım koşullarını kabul ediyorum koşuluyla önizlemeleri için kullanılabilir hale getirilir. Daha fazla bilgi için bkz. [Microsoft Azure Önizlemeleri için Microsoft Azure Ek Kullanım Koşulları](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).
>

Zamanlanmış olaylar subservice Azure meta veri hizmeti'de, sanal makine (VM) bakımı için hazırlamak için uygulama zaman verir altında olur. Yaklaşan Bakımı olaylar hakkında bilgi sağlar (örneğin, yeniden başlatma) böylece uygulamanız için hazırlamak ve sınırlamak kesintisi. PaaS ve hem Windows hem de Linux Iaas dahil olmak üzere tüm Azure sanal makineleri türleri kullanılabilir. 

Windows zamanlanan olaylar hakkında daha fazla bilgi için bkz: [zamanlanmış olaylar için Windows Vm'lerini](../windows/scheduled-events.md).

## <a name="why-use-scheduled-events"></a>Zamanlanmış olayları neden kullanılır?

Birçok uygulama, VM bakım için hazırlama zamandan yararlı olabilir. Zamanı kullanılabilirliği, güvenilirlik ve Bakım yapılabilirliğini, geliştirmek uygulamaya özgü görevleri gerçekleştirmek için kullanılabilir dahil olmak üzere: 

- Denetim noktası ve geri yükleme.
- Bağlantı boşaltma.
- Birincil çoğaltma yük devri.
- Bir yük dengeleyici havuzu kaldırma.
- Olay günlüğü.
- Normal şekilde kapatılmasını.

Zamanlanmış olaylarla uygulamanızı bakım zaman ve ortaya etkisini sınırlamak için görevlerini tetikleyin bulabilir.  

Zamanlanmış olayları aşağıdaki kullanım durumlarda olayları sağlar:

- Platform tarafından başlatılan Bakım (örneğin, bir ana bilgisayar işletim sistemi güncelleştirmesi)
- Kullanıcı tarafından başlatılan Bakım (örneğin, bir kullanıcının yeniden başlatır veya bir VM'yi yeniden dağıtır)

## <a name="the-basics"></a>Temel bilgiler  

  Meta veri hizmeti VM içinden erişilebilir bir REST uç noktasını kullanarak sanal makineleri çalıştırma hakkında bilgi gösterir. Böylece dışında VM gösterilmeyen bilgileri nonroutable IP kullanılabilir.

### <a name="scope"></a>Kapsam
Zamanlanmış olayları teslim edilir:

- Tüm sanal makineleri bir bulut hizmetinde.
- Tüm sanal makineleri bir kullanılabilirlik kümesinde.
- Tüm sanal makineleri bir ölçek kümesi yerleştirme grubunda. 

Sonuç olarak, denetleme `Resources` hangi VM'ler etkilenir tanımlamak için olay alanındaki.

### <a name="discover-the-endpoint"></a>Uç noktası bulunamadı
Sanal ağlar için etkinleştirilmiş olan VM'ler için zamanlanmış olayları en son sürümü için tam uç noktadır: 

 > `http://169.254.169.254/metadata/scheduledevents?api-version=2017-08-01`

Bir VM sanal ağ içinde oluşturulduğu burada durumda meta veri hizmeti statik nonroutable IP'den kullanılabilir `169.254.169.254`.
Bulut Hizmetleri ve klasik sanal makineleri için varsayılan durumlar bir sanal ağ içinde VM oluşturulmamışsa ek mantık kullanılacak IP adresini bulmak için gereklidir. Bilgi edinmek için nasıl [konak uç noktası bulunamadı](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm), bu örnek bakın.

### <a name="versioning"></a>Sürüm oluşturma 
Zamanlanmış olayları sürümlü bir hizmettir. Sürümleri zorunludur ve geçerli sürümü `2017-08-01`.

| Sürüm | Sürüm notları | 
| - | - | 
| 2017-08-01 | <li> Iaas VM'ler için kaynak adları alt çizgi $a kaldırıldı<br><li>Tüm istekler için zorlanan meta verileri üstbilgi gereksinimi | 
| 2017-03-01 | <li>Genel Önizleme sürümü


> [!NOTE] 
> Önceki Önizleme sürümleri zamanlanmış {son} API sürümü desteklenen olaylar. Bu biçim artık desteklenmemektedir ve gelecekte kullanım dışı kalacaktır.

### <a name="use-headers"></a>Üst bilgileri kullanma
Meta veri hizmeti sorguladığınızda başlık sağlamalısınız `Metadata:true` istek değildi kasıtsız olarak yeniden yönlendirilen emin olmak için. `Metadata:true` Üstbilgisi tüm zamanlanmış olaylar istekler için gereklidir. Hata istek üstbilgisini meta veri hizmetinden "Hatalı istek" yanıt sonuçlanır.

### <a name="enable-scheduled-events"></a>Zamanlanmış olayları etkinleştir
Zamanlanmış olaylar, istekte ilk kez Azure örtük olarak VM özelliği sağlar. Sonuç olarak, iki dakika içinde ilk çağrıda Gecikmeli yanıt bekler.

> [!NOTE]
> Zamanlanmış olayları otomatik olarak devre dışıdır hizmetiniz için hizmetinizi uç nokta için bir günü değil çağırırsanız. Zamanlanmış olayları hizmetiniz için devre dışı bırakıldıktan sonra hiçbir olay kullanıcı tarafından başlatılan bakım için oluşturulur.

### <a name="user-initiated-maintenance"></a>Kullanıcı tarafından başlatılan bakım
Azure portal, API, CLI veya PowerShell aracılığıyla kullanıcı tarafından başlatılan VM bakım zamanlanmış bir olayı sonuçlanır. Uygulamanızda bakım hazırlık mantığı sınayabilir ve uygulamanız için kullanıcı tarafından başlatılan bakım hazırlayabilirsiniz.

Bir olay türüne sahip bir VM yeniden başlatma durumunda `Reboot` zamanlandı. Bir VM türüne sahip bir olay dağıtmanız durumunda `Redeploy` zamanlandı.

> [!NOTE] 
> Şu anda, aynı anda en fazla 100 kullanıcı tarafından başlatılan bakım işlemleri zamanlanabilir.

> [!NOTE] 
> Şu anda zamanlanmış olayları sonuçları kullanıcı tarafından başlatılan bakım yapılandırılabilir değildir. Yapılandırılabilirlik gelecekteki bir sürümde planlanmaktadır.

## <a name="use-the-api"></a>API kullanın

### <a name="query-for-events"></a>Olaylar için sorgu
Aşağıdaki çağrıyı yaparak zamanlanmış olaylar için sorgulama yapabilirsiniz:

#### <a name="bash"></a>Bash
```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-08-01
```

Bir yanıt zamanlanmış olaylar dizisini içerir. Boş bir dizi şu anda hiçbir olay zamanlandığını anlamına gelir.
Durumda Zamanlanmış olaylar olduğu yanıtı olaylar dizisini içerir. 
```
{
    "DocumentIncarnation": {IncarnationID},
    "Events": [
        {
            "EventId": {eventID},
            "EventType": "Reboot" | "Redeploy" | "Freeze",
            "ResourceType": "VirtualMachine",
            "Resources": [{resourceName}],
            "EventStatus": "Scheduled" | "Started",
            "NotBefore": {timeInUTC},              
        }
    ]
}
```

### <a name="event-properties"></a>Olay Özellikleri
|Özellik  |  Açıklama |
| - | - |
| Olay Kimliği | Bu olay için genel benzersiz tanımlayıcı. <br><br> Örnek: <br><ul><li>602d9444-d2cd-49c7-8624-8643e7171297  |
| Olay türü | Bu olaya neden olan etkisi. <br><br> Değerler: <br><ul><li> `Freeze`: VM birkaç saniye duraklatmak için zamanlandı. CPU askıya alındı, ancak bellek, açık dosyalar ya da ağ bağlantıları üzerinde hiçbir etkisi yoktur. <li>`Reboot`: VM yeniden başlatma için zamanlanır. (Kalıcı olmayan bellek kaybolur.) <li>`Redeploy`: VM başka bir düğüme taşımak üzere zamanlandı. (Kısa ömürlü diskleri kaybolur.) |
| ResourceType | Bu olay etkiler kaynak türü. <br><br> Değerler: <ul><li>`VirtualMachine`|
| Kaynaklar| Bu olay etkiler kaynakların listesi. Listenin en fazla bir makinelerden içeren garanti [güncelleştirme etki alanı](manage-availability.md), ancak tüm makinelerde UD içermeyebilir. <br><br> Örnek: <br><ul><li> ["FrontEnd_IN_0", "BackEnd_IN_0"] |
| EventStatus | Bu olay durumu. <br><br> Değerler: <ul><li>`Scheduled`: Bu olay belirtilen süre sonra başlayacak şekilde zamanlanırsa `NotBefore` özelliği.<li>`Started`: Bu olay başlatıldı.</ul> Hayır `Completed` veya benzer durumu hiç sağlanır. Olayın sona erdiğinde olay artık döndürülür.
| NotBefore| Daha sonra bu olay başlangıç saati. <br><br> Örnek: <br><ul><li> 2016-09-19T18:29:47Z  |

### <a name="event-scheduling"></a>Olay planlama
Her olay zamanlanmış bir minimum süre gelecekte olay türüne bağlı. Bu süre bir olayın içinde yansıtılır `NotBefore` özelliği. 

|Olay türü  | Minimum dikkat edin |
| - | - |
| Dondurma| 15 dakika |
| Yeniden başlatma | 15 dakika |
| Yeniden dağıtım | 10 dakika |

### <a name="start-an-event"></a>Bir olayı Başlat 

Yaklaşan olay öğrenin ve mantığınızı normal olarak kapatmak için Son'u sonra yaparak bekleyen olay onaylayabilirsiniz bir `POST` çağrısı ile meta veri hizmetine `EventId`. Bu çağrı için Azure minimum bildirim kısaltabilir gösterir (uygunsa) süresi. 

Aşağıdaki JSON örneği bekleniyor `POST` iste gövde. İstek listesi içermelidir `StartRequests`. Her `StartRequest` içeren `EventId` hızlandırmak istediğiniz olayı için:
```
{
    "StartRequests" : [
        {
            "EventId": {EventId}
        }
    ]
}
```

#### <a name="bash-sample"></a>Bash örnek
```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-08-01
```

> [!NOTE] 
> Bir olay aktarımının sağlayan tüm devam etmek olay `Resources` olay bildirir yalnızca VM durumunda. Bu nedenle, ilk makine olarak kadar basit olabilir bildirim koordine etmek için bir kılavuz seçmediğiniz seçebileceğiniz `Resources` alan.

## <a name="python-sample"></a>Python örneği 

Aşağıdaki örnek, zamanlanmış olaylar için meta veri hizmeti sorgular ve her bekleyen olay onaylar:

```python
#!/usr/bin/python

import json
import urllib2
import socket
import sys

metadata_url = "http://169.254.169.254/metadata/scheduledevents?api-version=2017-08-01"
headers = "{Metadata:true}"
this_host = socket.gethostname()

def get_scheduled_events():
   req = urllib2.Request(metadata_url)
   req.add_header('Metadata', 'true')
   resp = urllib2.urlopen(req)
   data = json.loads(resp.read())
   return data

def handle_scheduled_events(data):
    for evt in data['Events']:
        eventid = evt['EventId']
        status = evt['EventStatus']
        resources = evt['Resources']
        eventtype = evt['EventType']
        resourcetype = evt['ResourceType']
        notbefore = evt['NotBefore'].replace(" ","_")
        if this_host in resources:
            print "+ Scheduled Event. This host " + this_host + " is scheduled for " + eventtype + " not before " + notbefore
            # Add logic for handling events here


def main():
   data = get_scheduled_events()
   handle_scheduled_events(data)

if __name__ == '__main__':
  main()
  sys.exit(0)
```

## <a name="next-steps"></a>Sonraki adımlar 
- Zamanlanmış olayları kod örnekleri gözden [Azure örneği meta verileri zamanlanmış olayları Github deposunu](https://github.com/Azure-Samples/virtual-machines-scheduled-events-discover-endpoint-for-non-vnet-vm).
- Daha fazla kullanılabilir olan API hakkında bilgi edinin [örneği meta veri hizmeti](instance-metadata-service.md).
- Hakkında bilgi edinin [planlı bakım için Linux sanal makineleri azure'da](planned-maintenance.md).
