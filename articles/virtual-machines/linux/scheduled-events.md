---
title: "aaaScheduled Azure Linux VM'ler için olayları | Microsoft Docs"
description: "Hello Azure meta veri hizmeti için Linux sanal makineleri kullanarak zamanlanmış olayları."
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
ms.openlocfilehash: e153c8854725330acefd67d0ef542f6149170a7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-linux-vms"></a>Azure meta veri hizmeti: Linux VM'ler zamanlanmış olaylar (Önizleme)

> [!NOTE] 
> Önizlemeler kullanılabilir tooyou toohello kullanım koşullarını kabul ediyorum hello koşula yapılır. Daha fazla bilgi için bkz. [Microsoft Azure Önizlemeleri için Microsoft Azure Ek Kullanım Koşulları](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).
>

Zamanlanmış olaylar biridir hello alt Servisleri hello Azure meta veri hizmeti altında. Yaklaşan olayları ile ilgili bilgiler görünmesini sorumludur (örneğin, yeniden başlatma) uygulamanız için hazırlamak ve sınırlamak için kesintisi. PaaS ve Iaas dahil olmak üzere tüm Azure sanal makine türleri için kullanılabilir. Zamanlanmış olaylar toominimize hello etkisi bir olay, sanal makine zaman tooperform önleyici görevlerinizi sağlar. 

Zamanlanmış olaylar hem Windows hem de Linux VM'ler için kullanılabilir. Windows zamanlanan olaylar hakkında daha fazla bilgi için bkz: [zamanlanmış olaylar için Windows Vm'lerini](../windows/scheduled-events.md).

## <a name="why-scheduled-events"></a>Neden zamanlanmış olayları?

Zamanlanmış olaylarla hizmetinizde toolimit hello etkisini platform intiated Bakım veya kullanıcı tarafından başlatılan Eylemler adımlar atabilirsiniz. 

Çoğaltma teknikleri toomaintain durumu kullanın, çok örnekli iş yükleri arasında birden çok örneği gerçekleştiği savunmasız toooutages olabilir. Bu tür kayıpları, pahalı görevler (örneğin, yeniden dizinler) veya çoğaltma kaybına neden olabilir. 

Diğer birçok durumda hello genel hizmet kullanılabilirliği kapama dizisi gibi gerçekleştirerek iyileştirilebilir (el ile yük devretme) hello kümedeki görevleri tooother VM'ler yeniden atama veya hello kaldırılması Tamamlanıyor (veya iptal etme) yürütülen işlemler, Sanal makine bir ağ yük dengeleyici havuzundan. 

Burada, yönetici yaklaşan bir olay hakkında bilgilendirmek veya böyle bir olay günlüğü yardımcı hello bakım yapılabilirliğini hello bulutta barındırılan uygulamalar geliştirme durumlar vardır.

Azure meta veri hizmeti yüzeyleri zamanlanmış olayları hello aşağıdaki durumlarda kullanın:
-   Başlatılan platform Bakım (örneğin, ana bilgisayar işletim sistemi dağıtımı)
-   Kullanıcı tarafından başlatılan çağrıları (örneğin, kullanıcı yeniden başlatma veya yeniden dağıtır VM)


## <a name="hello-basics"></a>Merhaba temelleri  

Azure meta veri hizmeti REST uç noktasını hello VM içinde erişilebilir kullanarak sanal makineleri çalıştırma hakkında bilgi gösterir. Böylece VM hello dışında gösterilmeyen hello bilgi yönlendirilemeyen bir IP kullanılabilir.

### <a name="scope"></a>Kapsam
Zamanlanmış olaylar ortaya tooall sanal makineler bir bulut hizmetinde veya bir kullanılabilirlik kümesindeki sanal makineleri tooall verilmiştir. Sonuç olarak, hello denetlemelisiniz `Resources` VM'ler etkilenen toobe kalacaklarını hello olay tooidentify alanındaki. 

### <a name="discovering-hello-endpoint"></a>Merhaba endpoint keşfetme
Bir sanal makine bir sanal ağ (VNet) içinde oluşturulduğu burada hello durumda hello meta veri hizmeti bir statik yönlendirilemeyen bir IP, kullanılabilir `169.254.169.254`.
İlave bir mantık gerekli toodiscover hello uç nokta toouse ise Hello sanal makine bulut Hizmetleri ve klasik sanal makineleri için hello varsayılan durumlar bir sanal ağ içinde oluşturulmaz. Toothis örnek toolearn nasıl çok başvuran[hello konak uç noktası bulunamadı](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).

### <a name="versioning"></a>Sürüm oluşturma 
Merhaba örneği meta veri hizmeti sürümü tutulan ' dir. Sürümleri zorunludur ve hello geçerli sürümü `2017-03-01`.

> [!NOTE] 
> Önceki Önizleme sürümleri {son} hello api sürümü desteklenen zamanlanmış olaylar. Bu biçim artık desteklenmemektedir ve hello gelecekteki kullanım dışı kalacaktır.

### <a name="using-headers"></a>Üst bilgileri kullanma
Merhaba meta veri hizmeti sorguladığınızda hello üstbilgi sağlamalısınız `Metadata: true` tooensure hello talep istemeden yönlendirilmeyen.

### <a name="enabling-scheduled-events"></a>Zamanlanmış olayları etkinleştirme
Merhaba zamanlanmış olaylar, istekte ilk kez Azure örtük olarak hello özelliği, sanal makinenizde sağlar. Sonuç olarak, ilk çağrısında tootwo dakika yukarı Gecikmeli yanıt beklemelisiniz.

### <a name="user-initiated-maintenance"></a>Kullanıcı tarafından başlatılan bakım
Sanal makine Bakımı hello Azure portal, API, CLI, aracılığıyla kullanıcı tarafından başlatılan veya PowerShell zamanlanmış bir olayı sonuçlanır. Bu, uygulamanızda tootest hello bakım hazırlık mantığı sağlar ve kullanıcı tarafından başlatılan bakım için uygulama tooprepare sağlar.

Bir sanal makinenin yeniden başlatılması zamanlar türüne sahip bir olay `Reboot`. Bir sanal makineyi dağıtarak zamanlar türüne sahip bir olay `Redeploy`.

> [!NOTE] 
> Şu anda en fazla 10 kullanıcı tarafından başlatılan bakım işlemleri aynı anda zamanlanabilir. Bu sınır zamanlanmış olayları genel kullanılabilirlik önce rahat olmalıdır.

> [!NOTE] 
> Şu anda zamanlanmış olayları kaynaklanan kullanıcı tarafından başlatılan bakım yapılandırılabilir değildir. Yapılandırılabilirlik gelecekteki bir sürümde planlanmaktadır.

## <a name="using-hello-api"></a>Merhaba API'yi kullanma

### <a name="query-for-events"></a>Olaylar için sorgu
Zamanlanmış olaylar için çağrı hello aşağıdakileri yaparak sorgulayabilirsiniz:

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

Bir yanıt zamanlanmış olaylar dizisini içerir. Boş bir dizi var. şu anda zamanlanmış bir olay yok demektir.
Merhaba durumda Zamanlanmış olaylar olduğu hello yanıt olaylar dizisini içerir: 
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
| Olay türü | Bu olaya neden olan etkisi. <br><br> Değerler: <br><ul><li> `Freeze`: hello sanal makine için birkaç saniye zamanlanmış toopause değil. Merhaba CPU askıya alındı, ancak bellek, açık dosyalar veya ağ bağlantıları üzerinde hiçbir etkisi yoktur. <li>`Reboot`: sanal makine için yeniden başlatma Zamanlanmış Başlangıç (kalıcı olmayan bellek kaybolur). <li>`Redeploy`: hello sanal makine olan zamanlanmış toomove tooanother düğümü (kısa ömürlü diskleri kaybolur). |
| ResourceType | Bu olay etkiler kaynak türü. <br><br> Değerler: <ul><li>`VirtualMachine`|
| Kaynaklar| Bu olay etkiler kaynakların listesi. Bu toocontain makineler en fazla bir garanti [güncelleştirme etki alanı](manage-availability.md), hello UD tüm makinelerde içerebilir ancak. <br><br> Örnek: <br><ul><li> ["FrontEnd_IN_0", "BackEnd_IN_0"] |
| Olay durumu | Bu olay durumu. <br><br> Değerler: <ul><li>`Scheduled`: Bu olay hello belirtilen başlangıç saati zamanlanmış toostart sonradır `NotBefore` özelliği.<li>`Started`: Bu olay başlatıldı.</ul> Hayır `Completed` veya benzer durumu hiç sağlanır; hello olay, artık hello olay tamamlandığında döndürülecek.
| NotBefore| Süre geçtikten sonra bu olay başlayabilir. <br><br> Örnek: <br><ul><li> 2016-09-19T18:29:47Z  |

### <a name="event-scheduling"></a>Olay planlama
Her olay zamanlanmış bir minimum süreyi hello gelecekteki olay türüne bağlı. Bu süre bir olayın içinde yansıtılır `NotBefore` özelliği. 

|Olay türü  | Minimum dikkat edin |
| - | - |
| Dondurma| 15 dakika |
| Yeniden başlatma | 15 dakika |
| Yeniden dağıtım | 10 dakika |

### <a name="starting-an-event"></a>Bir olayı başlatılıyor 

Yaklaşan olay öğrenilen ve normal olarak kapatmak için mantığınızı tamamlandı sonra yaparak hello bekleyen olay onaylayabilirsiniz bir `POST` çağrısı toohello meta veri hizmeti ile Merhaba `EventId`. Bu hello minimum bildirim kısaltabilir tooAzure gösterir (uygunsa) süresi. 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> Bir olay aktarımının verir hello olay tooproceed tüm `Resources` hello olayda hello olay kabul ettikten sanal makine yalnızca hello. Bu nedenle hello ilk makine hello olarak basit bir kılavuz toocoordinate hello bildirim tooelect tercih edebilirsiniz `Resources` alan.




## <a name="python-sample"></a>Python örneği 

Merhaba aşağıdaki örnek sorgularda zamanlanmış olaylar için meta veri hizmeti hello ve her bekleyen olay onaylar.

```python
#!/usr/bin/python

import json
import urllib2
import socket
import sys

metadata_url = "http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01"
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
            print "+ Scheduled Event. This host is scheduled for " + eventype + " not before " + notbefore
            # Add logic for handling events here

def main():
   data = get_scheduled_events()
   handle_scheduled_events(data)
   
if __name__ == '__main__':
  main()
  sys.exit(0)
```

## <a name="next-steps"></a>Sonraki adımlar 

- Merhaba hello kullanılabilir API'ler hakkında daha fazla bilgiyi [örneği meta veri hizmeti](instance-metadata-service.md).
- Hakkında bilgi edinin [planlı bakım için Linux sanal makineleri azure'da](planned-maintenance.md).
