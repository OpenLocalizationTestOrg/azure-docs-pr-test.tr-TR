---
title: "Otomatik ölçeklendirme Azure sanal makine ölçek kümeleri ile genel bakış | Microsoft Docs"
description: "Bir Azure sanal makinesi ölçeği performans veya sabit bir zamanlama tabanlı Ayarla otomatik olarak ölçeklendirebilirsiniz farklı yolları hakkında bilgi edinin"
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: jeconnoc
editor: 
tags: azure-resource-manager
ms.assetid: d29a3385-179e-4331-a315-daa7ea5701df
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/19/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 868523a3aca441a47218297be2ce9f9e46dd84a1
ms.sourcegitcommit: 2d1153d625a7318d7b12a6493f5a2122a16052e0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/20/2017
---
# <a name="overview-of-autoscale-with-azure-virtual-machine-scale-sets"></a>Otomatik ölçeklendirme Azure sanal makine ölçek ile genel bakış ayarlar
Bir Azure sanal makine ölçek kümesini otomatik olarak artırın veya uygulamanızı çalıştıran VM örneği sayısını azaltın. Bu otomatik ve esnek davranışı izlemek ve uygulamanızın performansını en iyi duruma getirmek için yönetim yükünü azaltır. Bir pozitif müşteri deneyimi için en düşük düzeyde kabul edilebilir performans tanımlayan kurallar oluşturun. Bu tanımlanmış eşikleri karşılandığında, otomatik ölçeklendirme kurallarını ölçek kümesi kapasitesi ayarlamak için adımları uygulayın. Ayrıca, Ölçek kümesinde kapasitesini kez sabit azaltın veya otomatik olarak artırmak için olayları zamanlayabilirsiniz. Bu makale, hangi performansını ölçümleri kullanılabilen genel bir bakış ve hangi eylemleri otomatik ölçeklendirme gerçekleştirebilirsiniz sağlar.


## <a name="benefits-of-autoscale"></a>Otomatik ölçeklendirme yararları
Uygulama talep artarsa, Ölçek VM örnekleri üzerindeki yük artar ayarlayın. Bu artan yükün tutarlı, ise yalnızca kısa isteğe bağlı yerine, Ölçek kümesi VM örnekleri sayısını artırmak için otomatik ölçeklendirme kuralları yapılandırabilirsiniz.

Bu VM örnekleri oluşturulur ve uygulamalarınızı dağıtılan bunlara trafiğini yük dengeleyici üzerinden dağıtmak ölçek kümesini başlar. CPU veya bellek, uygulama yük belirli bir eşiğin ne kadar süreyle karşılamalıdır ve ölçek eklemek için kaç VM örnekleri kümesi gibi izlemek için hangi ölçümleri denetler.

Bir akşam veya hafta sonu, uygulamayı isteğe bağlı azaltabilir. Bu azalmasına yükü bir süre boyunca tutarlı ise, Ölçek kümesi VM örnekleri sayısını azaltmak için otomatik ölçeklendirme kuralları yapılandırabilirsiniz. Bu ölçek eylemi geçerli talebi karşılamak için gerekli örnek sayısı yalnızca çalışacak şekilde ayarlayın, Ölçek çalıştırmak için maliyeti azaltır.


## <a name="use-host-based-metrics"></a>Ana bilgisayar tabanlı ölçümleri kullanın
Kullanılabilir bu yerleşik ana ölçümleri, VM örneklerinden otomatik ölçeklendirme kurallar oluşturabilirsiniz. Ana ölçümleri yüklemek veya ek aracıları ve veri koleksiyonları yapılandırmak zorunda kalmadan ayarlamak ölçeğinde VM örnekleri performansını görünürlük sağlar. Bu ölçümleri kullanmak otomatik ölçeklendirme kurallarını out veya yanıt CPU kullanımı, bellek isteğe bağlı veya disk erişimi için VM örneği sayısı ölçeklendirebilirsiniz.

Konak tabanlı ölçümleri kullanan otomatik ölçeklendirme kuralları aşağıdaki araçlarla oluşturulabilir:

- [Azure portal](virtual-machine-scale-sets-autoscale-portal.md)
- [Azure PowerShell](virtual-machine-scale-sets-autoscale-powershell.md)
- [Azure CLI 2.0](virtual-machine-scale-sets-autoscale-cli.md)

Daha ayrıntılı performans ölçümleri kullanan otomatik ölçeklendirme kuralları oluşturmak için şunları yapabilirsiniz [Azure tanılama uzantısını yükleyip](#in-guest-vm-metrics-with-the-azure-diagnostics-extension) VM örneklerinde veya [uygulama kullanımınız App Insights yapılandırma](#application-level-metrics-with-app-insights).

Ana bilgisayar tabanlı ölçümleri kullanan otomatik ölçeklendirme kurallarını Konuk VM ölçümleri Azure tanılama uzantısını ve App Insights ile aşağıdaki yapılandırma ayarlarını kullanabilirsiniz.

### <a name="metric-sources"></a>Ölçüm kaynakları
Otomatik ölçeklendirme kurallarını ölçümleri aşağıdaki kaynaklardan birini kullanabilirsiniz:

| Ölçüm kaynağı        | Kullanım örneği                                                                                                                     |
|----------------------|------------------------------------------------------------------------------------------------------------------------------|
| Geçerli ölçek kümesi    | Ana bilgisayar tabanlı ölçümleri, yüklenmedi veya Yapılandırılmadı ek aracıları gerektirmez.                                  |
| Depolama hesabı      | Azure tanılama uzantısını performans ölçümleri sonra otomatik ölçeklendirme kurallarını tetiklemek için kullanılan Azure depolama alanına yazar. |
| Hizmet veri yolu kuyruğu    | Uygulamanızı veya diğer bileşenleri Tetikleyici kuralları Azure Service Bus kuyruğuna iletileri iletebilir.                   |
| Application Insights | Uygulamanızdaki ölçümleri doğrudan uygulama üzerinden akışlarını yüklü bir izleme paketi.                         |


### <a name="autoscale-rule-criteria"></a>Otomatik ölçeklendirme kural ölçütleri
Otomatik ölçeklendirme kuralları oluşturduğunuzda aşağıdaki ana bilgisayar tabanlı ölçümleri kullanılabilir. Azure tanılama uzantısı veya App Insights kullanıyorsanız, izlemek ve otomatik ölçeklendirme kuralları ile kullanmak üzere hangi ölçümlerini tanımlayın.

| Ölçüm adı               |
|---------------------------|
| CPU yüzdesi            |
| Ağ içine                |
| Ağ dışına               |
| Disk okuma bayt           |
| Disk yazma bayt          |
| Disk okuma işlemleri/sn  |
| Disk yazma işlemi/sn |
| CPU kredi kaldı     |
| Kullanılan CPU KREDİLERİ      |

Belirli bir metrik izlemek için otomatik ölçeklendirme kuralları oluşturduğunuzda, kural aşağıdaki ölçümleri toplama eylemlerden birini arayın:

| Toplama türü |
|------------------|
| Ortalama          |
| Minimum          |
| Maksimum          |
| Toplam            |
| Son             |
| Sayı            |

Otomatik ölçeklendirme kurallarını ölçümleri tanımlı eşiğiniz karşı aşağıdaki işleçleri biri ile karşılaştırıldığında daha sonra tetiklenen:

| işleci                 |
|--------------------------|
| Şu değerden fazla:             |
| Büyüktür veya eşittir |
| Şu değerden az:                |
| Küçük veya eşit    |
| Eşit                 |
| Eşit değil             |


### <a name="actions-when-rules-trigger"></a>Kuralları tetiklemek zaman Eylemler
Otomatik ölçeklendirme kural tetikleyicileri, Ölçek kümesini otomatik olarak aşağıdaki yollardan biriyle ölçeklendirebilirsiniz:

| Ölçeklendirme işlemi     | Kullanım örneği                                                                                                                               |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| Sayıya göre artırma   | VM örnekleri oluşturmak için sabit sayısı. VM'ler daha az sayıda ölçek kümeleri yararlıdır.                                           |
| Yüzde Artır | Yüzde tabanlı bir artış VM örnekleri. Büyük ölçek için iyi olduğu sabit bir artış belirgin şekilde performansını artırabilir değil ayarlar. |
| Artış sayısı   | İstenen en büyük bir miktarını ulaşmak için birçok VM örnekleri gerektiği şekilde oluşturun.                                                            |
| Azaltma sayısı   | VM örnekleri kaldırmak için sabit sayısı. VM'ler daha az sayıda ölçek kümeleri yararlıdır.                                           |
| Yüzde Azalt | Yüzde tabanlı bir düşüş VM örnekleri. Büyük ölçek için iyi olduğu sabit bir artış belirgin şekilde kaynak tüketimini ve maliyetleri azaltabilir değil ayarlar. |
| Azaltma sayısı   | İstenen minimum tutar ulaşmak için birçok VM örnekleri gerektiği şekilde kaldırın.                                                            |


## <a name="in-guest-vm-metrics-with-the-azure-diagnostics-extension"></a>Azure tanılama uzantısını ile Konuk VM ölçümleri
Azure tanılama uzantısını VM örneği içinde çalıştıran bir aracıdır. Aracısı'nı izler ve performans ölçümleri Azure depolama alanına kaydeder. Bu performans ölçümleri gibi VM durumu hakkında daha ayrıntılı bilgi içeren *AverageReadTime* diskler için veya *PercentIdleTime* CPU için. VM performans, yalnızca CPU kullanımı veya bellek tüketimi yüzdesi, daha ayrıntılı olarak hakkında farkındalık üzerinde temel alan otomatik ölçeklendirme kurallar oluşturabilir.

Azure tanılama uzantısını kullanmak için VM örnekleri için Azure storage hesapları oluşturmanız, Azure Tanılama aracı yükleme ardından VM'ler akış belirli performans sayaçlarını depolama hesabı için yapılandırın.

Daha fazla bilgi için Azure tanılama uzantısını [Linux VM](../virtual-machines/linux/diagnostic-extension.md) veya [Windows VM](../virtual-machines/windows/ps-extensions-diagnostics.md) için etkinleştirme makalelerini inceleyebilirsiniz.


## <a name="application-level-metrics-with-app-insights"></a>Uygulama düzeyi ölçümlerini App Insights ile
Uygulamalarınızın performansını artırmak için daha fazla görünürlük kazanmak için Application Insights kullanabilirsiniz. Uygulama izler ve Azure'a telemetri gönderir, uygulamanızdaki bir küçük araçları paketini yükleyin. Sayfa yükleme performansı, uygulamanızın yanıt süreleri gibi ölçümlerini izleyebilir ve oturum sayar. Bu uygulama ölçümleri, müşteri deneyimini etkileyebilecek eyleme dönüştürülebilir Öngörüler üzerinde temel kurallarını tetiklemek ayrıntılı ve katıştırılmış düzeyinde otomatik ölçeklendirme kuralları oluşturmak için kullanılabilir.

App Insights hakkında daha fazla bilgi için bkz. [Application Insights nedir?](../application-insights/app-insights-overview.md).


## <a name="scheduled-autoscale"></a>Zamanlanmış otomatik ölçeklendirme
Zamanlamada göre otomatik ölçeklendirme kuralları da oluşturabilirsiniz. Bu zamanlama tabanlı kuralları otomatik olarak VM örnek sayısı kez sabit ölçek izin verir. Performans tabanlı kurallarla otomatik ölçeklendirme kurallarını tetikleyici önce uygulamayı üzerinde bir performans etkisi olabilir ve yeni VM örnekleri sağlanır. Bu tür isteğe bağlı öngörüyorsanız, ek VM örnekleri sağlanan ve ek müşteri kullanın ve uygulama talep için hazır.

Aşağıdaki örnekler, zamanlama tabanlı otomatik ölçeklendirme kurallarını kullanımını yararlanabilir senaryolar şunlardır:

- Ne zaman müşteri talebini artırır iş gününün başlangıcında VM örneği sayısını otomatik olarak ölçeklendirin. İş günü sonunda, uygulama kullanımı düşük olduğunda kaynak maliyetleri günde en aza indirmek için VM örneği sayısını otomatik olarak ölçeklendirin.
- Otomatik olarak bir bölüm bir uygulama yoğun olarak ayın veya mali döngüsü belirli bölümlerine kullanıyorsa, bunların ek taleplerini karşılamak için VM örnek sayısını ölçeklendirmek.
- Pazarlama olay, yükseltme veya tatil satış olduğunda beklenen Müşteri talebi öncesinde VM örneklerinin sayısını otomatik olarak ölçeklendirebilirsiniz. 


## <a name="next-steps"></a>Sonraki adımlar
Ana bilgisayar tabanlı ölçümleri aşağıdaki araçlardan birini kullanın otomatik ölçeklendirme kurallar oluşturabilirsiniz:

- [Azure portal](virtual-machine-scale-sets-autoscale-portal.md)
- [Azure PowerShell](virtual-machine-scale-sets-autoscale-powershell.md)
- [Azure CLI 2.0](virtual-machine-scale-sets-autoscale-cli.md)

Bu genel bakışta otomatik ölçeklendirme kurallarını yatay olarak ölçekleme ve artırmak veya azaltmak için nasıl kullanılacağını ayrıntılı *numarası* , Ölçek VM örnekleri kümesi. Ayrıca dikey olarak artırmak veya azaltmak VM örneği için ölçeklendirmek *boyutu*. Daha fazla bilgi için bkz: [dikey otomatik ölçeklendirme sanal makine ölçek kümeleri ile](virtual-machine-scale-sets-vertical-scale-reprovision.md).

Üzerindeki VM örneklerinize yönetme hakkında daha fazla bilgi için bkz: [Yönet sanal makine ölçek ayarlar Azure PowerShell ile](virtual-machine-scale-sets-windows-manage.md).

Tetikleyici, otomatik ölçeklendirme kurallarını taktirde uyarı oluşturma konusunda bilgi almak için bkz: [e-posta ve Web kancası Azure İzleyicisi'nde uyarı bildirimleri göndermek için otomatik ölçeklendirme eylemlerini kullanmak](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md). Ayrıca [e-posta ve Web kancası Azure İzleyicisi'nde uyarı bildirimleri göndermek için kullanım denetim günlüklerini](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md).