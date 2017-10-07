---
title: "Microsoft Azure sanal makineler, bulut Hizmetleri ve Web uygulamaları otomatik ölçeklendirme aaaOverview | Microsoft Docs"
description: "Microsoft Azure otomatik ölçeklendirme genel bakış. TooVirtual makineler, bulut Hizmetleri ve Web uygulamaları için geçerlidir."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 74bf03be-e658-4239-a214-c12424b53e4c
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2016
ms.author: robb
ms.openlocfilehash: ef68b722ea22c4149a7d7a89c5855ba761db9247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-autoscale-in-microsoft-azure-virtual-machines-cloud-services-and-web-apps"></a>Microsoft Azure sanal makineler, bulut Hizmetleri ve Web uygulamaları otomatik ölçeklendirme genel bakış
Bu makalede hangi Microsoft Azure otomatik ölçeklendirme, onun avantajlarını olduğu ve bunu kullanarak tooget nasıl başlatılacağını açıklar.  

Azure İzleyici otomatik ölçeklendirme uygular yalnızca çok[sanal makine ölçek kümeleri](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [bulut Hizmetleri](https://azure.microsoft.com/services/cloud-services/), ve [uygulama hizmeti - Web Apps](https://azure.microsoft.com/services/app-service/web/).

> [!NOTE]
> Azure iki otomatik ölçeklendirme yöntemlerine sahiptir. Otomatik ölçeklendirme daha eski bir sürümü tooVirtual makineler (kullanılabilirlik kümeleri) uygulanır. Bu özellik sınırlı destek ve geçirme toovirtual makine ölçek kümesi daha hızlı ve daha güvenilir otomatik ölçeklendirme desteği öneririz. Bu makalede nasıl toouse hello eski teknolojiyi bağlantı dahil edilir.  
>
>

## <a name="what-is-autoscale"></a>Otomatik ölçeklendirme nedir?
Otomatik ölçeklendirme toohave hello doğru miktarda toohandle hello yük uygulamanızı üzerinde çalışan kaynakları sağlar. Toohandle artışlar yüklemek ve ayrıca boşta durduğunu kaynakları kaldırarak paradan tasarruf tooadd kaynaklar sağlar. Ekleme örnekleri toorun minimum ve maksimum sayısını belirtin veya otomatik olarak bir dizi kurala göre sanal makineleri kaldırın. Bir minimum yapar emin olması, uygulamanızın her zaman bile herhangi bir yük altında çalışıyor. Maksimum sahip saatlik maliyet, toplam olası sınırlar. Oluşturduğunuz kurallarını kullanarak bu iki uç nokta arasında otomatik olarak ölçeklendirin.

 ![Otomatik ölçeklendirme açıklanmıştır. Sanal makineleri ekleyip](./media/monitoring-overview-autoscale/AutoscaleConcept.png)

Bir veya daha fazla otomatik ölçeklendirme eylemi Kural koşulu karşılandığında tetiklenir. Ekleme ve sanal makineleri kaldırın veya başka eylemler gerçekleştirebilir. Merhaba aşağıdaki kavramsal diyagram bu işlemi gösterilmektedir.  

 ![Otomatik ölçeklendirme Akış Diyagramı](./media/monitoring-overview-autoscale/Autoscale_Overview_v4.png)

Merhaba aşağıdaki açıklama hello önceki diyagramda toohello parçalarını geçerlidir.   

## <a name="resource-metrics"></a>Kaynak ölçümleri
Kaynak ölçümleri yayma, bu ölçümleri daha sonra kuralları tarafından işlenir. Ölçümleri farklı yöntemler sunulur.
Web uygulamaları ve bulut Hizmetleri için telemetri doğrudan hello Azure Altyapısı ' gelir ancak sanal makine ölçek kümeleri telemetri verilerini Azure Tanılama aracı kullanın. Bazı yaygın olarak kullanılan istatistik CPU kullanımı, bellek kullanımı, iş parçacığı sayıları, kuyruk uzunluğu ve disk kullanımını içerir. Kullanabileceğiniz hangi telemetri verilerini bir listesi için bkz: [otomatik ölçeklendirme ortak ölçümleri](insights-autoscale-common-metrics.md).

## <a name="custom-metrics"></a>Özel ölçümleri
Uygulamaları yayma kendi özel ölçümleri da kullanabilirsiniz. Uygulamaları toosend ölçümleri tooApplication mi ölçümleri toomake kararların yararlanabilirsiniz Öngörüler yapılandırdıysanız tooscale veya değil. 

## <a name="time"></a>Zaman
Zamanlama tabanlı kuralları UTC üzerinde temel alır. Kuralları ayarladığınız ayarlarken, saat dilimini düzgün şekilde ayarlamalısınız.  

## <a name="rules"></a>Kurallar
yalnızca bir otomatik ölçeklendirme kural Hello diyagramda gösterilmektedir, ancak bunların kaç sahip olabilir. Durumunuz için gerektiği gibi karmaşık çakışan kurallar oluşturabilirsiniz.  Kural türlerini içerir  

* **Ölçüm tabanlı** -Örneğin, CPU kullanımı % 50 ' olduğunda bu eylemi gerçekleştirin.
* **Zamana bağlı** - Örneğin, tetikleyici bir Web kancası her 8: 00 belirli bir saat diliminde Cumartesi.

Ölçüm tabanlı kurallar uygulama yük ölçmek ve eklemek veya bu yüküne göre sanal makineleri kaldırın. Zamanlama tabanlı kuralları, tooscale yükleme saat desenleri görmek ve olası yük artışı önce tooscale istediğiniz veya düşüş ortaya çıktığında izin verir.  

## <a name="actions-and-automation"></a>Eylemler ve Otomasyon
Kurallar, bir veya daha fazla tür eylemlerin tetikleyebilir.

* **Ölçek** -ölçek VM'ler veya uzaklaştırma
* **E-posta** -e-posta toosubscription yöneticileri, ortak yöneticilere ve/veya belirttiğiniz ek e-posta adresini Gönder
* **Web kancası otomatikleştirmek** -birden çok karmaşık eylem içinde veya Azure dışında tetikleyebilir Web kancalarını çağırın. Azure içinde bir Azure Otomasyonu runbook, Azure işlevi veya Azure mantıksal uygulama başlatabilirsiniz. Azure dışında örnek üçüncü taraf URL kayma ve Twilio gibi hizmetleri içerir.

## <a name="autoscale-settings"></a>Otomatik ölçeklendirme ayarları
Otomatik ölçeklendirme kullanmak hello aşağıdaki terimleri ve yapısı.

- Bir **otomatik ölçeklendirme ayarı** hello otomatik ölçeklendirme altyapısı toodetermine tarafından mı okuma tooscale yukarı veya aşağı. Bu bir veya daha fazla profiller, hello hedef kaynak ve bildirim ayarları hakkında bilgi içerir.

    - Bir **otomatik ölçeklendirme profili** a: birleşimidir

        - **Kapasite ayarı**hello minimum, maksimum gösterir ve örnek sayısı için varsayılan değerler.
        - **Kural kümesi**, her biri bir tetikleyici (saat veya Metrik) ve bir ölçek eylemi (yukarı veya aşağı) içerir.
        - **Yineleme**, ne zaman otomatik ölçeklendirme bu profili yürürlüğe koymak gösterir.

        Farklı çakışan gereksinimleri care of tootake izin birden çok profil olabilir. Örneğin, gün veya hello haftanın günlerini farklı saatler için farklı ölçeklendirme profili olabilir.

    - A **bildirim ayarı** otomatik ölçeklendirme olay hello otomatik ölçeklendirme ayarının profilleri birinin hello ölçütlerine göre oluştuğunda hangi bildirimleri gerçekleşmesi gerektiğini tanımlar. Otomatik ölçeklendirme, bir veya daha fazla e-posta adresleri bildir veya çağrıları tooone ya da daha fazla Web kancası olun.


![Azure otomatik ölçeklendirme ayarı, profil ve kural yapısı](./media/monitoring-overview-autoscale/AzureResourceManagerRuleStructure3.png)

Merhaba yapılandırılabilir alanları ve açıklamalarının tam listesi hello kullanılabilir [otomatik ölçeklendirme REST API](https://msdn.microsoft.com/library/dn931928.aspx).

Kod örnekleri için bkz:

* [VM ölçek kümesi için Resource Manager şablonları kullanarak gelişmiş otomatik ölçeklendirme yapılandırma](insights-advanced-autoscale-virtual-machine-scale-sets.md)  
* [Otomatik ölçeklendirme REST API'si](https://msdn.microsoft.com/library/dn931953.aspx)

## <a name="horizontal-vs-vertical-scaling"></a>Yatay vs dikey ölçekleme
Otomatik ölçeklendirme yalnızca yatay artışı ("out") veya ("içinde") azaltmak VM örnekleri hello sayısını ölçeklendirir.  Yatay VM'ler toohandle iş yükünün olası binlerce toorun izin verdiği ölçüde bulut durumda daha esnektir.

Buna karşılık, dikey ölçekleme farklıdır. Bu tutar hello VM'ler ile aynı sayıda ancak yapar hello VM'ler daha fazla ("yukarı") veya ("kapalı") güçlü daha az. Güç, bellek, CPU hızı, disk alanı vb. ölçülür.  Dikey ölçekleme daha fazla sınırlamaları vardır. Hızla bir üst sınır İsabetli ve bölgeye göre farklılık gösterebilir büyük donanım hello kullanılabilirliğine bağlıdır. Ayrıca genellikle ölçeklendirme dikey VM toostop gerektirir ve yeniden başlatın.

Daha fazla bilgi için bkz: [Azure Automation ile Azure sanal makine dikey olarak ölçeklendirmek](../virtual-machines/linux/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="methods-of-access"></a>Erişim yöntemleri
Otomatik ölçeklendirme ayarlayabilirsiniz.

* [Azure portal](insights-how-to-scale.md)
* [PowerShell](insights-powershell-samples.md#create-and-manage-autoscale-settings)
* [Platformlar arası komut satırı arabirimi (CLI)](insights-cli-samples.md#autoscale)
* [Azure monitör REST API'si](https://msdn.microsoft.com/library/azure/dn931953.aspx)

## <a name="supported-services-for-autoscale"></a>Otomatik ölçeklendirme için desteklenen hizmetler
| Hizmet | Şema & belgeleri |
| --- | --- |
| Web Apps |[Web uygulamaları ölçeklendirme](insights-how-to-scale.md) |
| Cloud Services |[Otomatik ölçeklendirme bir bulut hizmeti](../cloud-services/cloud-services-how-to-scale.md) |
| Sanal makineler: Klasik |[Klasik sanal makine kullanılabilirlik kümeleri ölçeklendirme](https://blogs.msdn.microsoft.com/kaevans/2015/02/20/autoscaling-azurevirtual-machines/) |
| Sanal makineler: Windows ölçek kümeleri |[Sanal makine ölçek ölçeklendirme Windows ayarlar](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) |
| Sanal makineler: Linux ölçek ayarlar |[Sanal makine ölçek ölçeklendirme Linux ayarlar](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) |
| Sanal makineler: Windows örneği |[VM ölçek kümesi için Resource Manager şablonları kullanarak gelişmiş otomatik ölçeklendirme yapılandırma](insights-advanced-autoscale-virtual-machine-scale-sets.md) |

## <a name="next-steps"></a>Sonraki adımlar
otomatik ölçeklendirme, hakkında daha fazla toolearn otomatik ölçeklendirme izlenecek yollar daha önce listelenen hello kullanın veya kaynakları aşağıdaki toohello bakın:

* [Azure İzleyici otomatik ölçeklendirme ortak ölçümleri](insights-autoscale-common-metrics.md)
* [Azure İzleyici otomatik ölçeklendirme için en iyi yöntemler](insights-autoscale-best-practices.md)
* [Otomatik ölçeklendirme eylemleri toosend e-posta ve Web kancası uyarı bildirimleri kullanın](insights-autoscale-to-webhook-email.md)
* [Otomatik ölçeklendirme REST API'si](https://msdn.microsoft.com/library/dn931953.aspx)
* [Sorun giderme sanal makine ölçek kümeleri otomatik ölçeklendirme](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)
