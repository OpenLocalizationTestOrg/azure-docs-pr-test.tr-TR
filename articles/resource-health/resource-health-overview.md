---
title: "aaaAzure kaynak sistem durumu genel bakış | Microsoft Docs"
description: "Azure kaynak durumu genel bakış"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: resource-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 06/01/2016
ms.author: BernardoAMunoz
ms.openlocfilehash: b920241b2f64a0695ba2c32e9ccb0c2c3739986d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-overview"></a>Azure kaynak sistem durumu genel bakış
 
Kaynak Durumu, bir Azure sorunu kaynaklarınızı etkilediğinde bunu tanılamanıza ve destek almanıza yardımcı olur. Merhaba geçerli ve geçmiş kaynaklarınızın sistem durumunu hakkında bilgilendirir ve sorunları azaltmaya yardımcı olur. Kaynak Durumu, Azure hizmet sorunları ile ilgili yardıma ihtiyacınız olduğunda teknik destek sağlar.

Oysa [Azure durum](https://status.azure.com) Azure müşterilerine geniş bir dizi etkileyen hizmeti sorunları hakkında bilgilendirir, kaynak durumu hello kaynaklarınızın sistem durumunu içeren bir kişiselleştirilmiş Pano sağlar. Kaynak durumu gösterir, hello sürekli kaynaklarınızı hello kullanılamaz tooAzure hizmet sorunlarını süresi geçti. Bir SLA ihlal varsa bu, toounderstand basit kolaylaştırır. 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a>Bir kaynak olarak kabul ve kaynak sağlıklı olup olmadığını karar nasıl kaynak durumu mu?
Örneğin bir Azure hizmeti aracılığıyla Azure Resource Manager tarafından sunulan bir kaynak türünün bir örneği bir kaynaktır: bir sanal makine, bir web uygulaması veya bir SQL veritabanı.

Kaynak durumu üzerinde bir kaynak sağlıklı olup olmadığını hello farklı Azure Hizmetleri tooassess tarafından gösterilen sinyalleri kullanır. Bir kaynak sağlıksız ise, kaynak durumu ek bilgi toodetermine hello hello sorunun kaynağını analiz eder. Ayrıca, Microsoft toofix hello sorunu veya tooaddress hello yapabileceğiniz işlemlerde hello sorununun nedeni ne sürüyor eylemleri tanımlar. 

Gözden geçirme hello tam kaynak türleri ve sistem durumu denetimleri listesi [Azure kaynak durumu](resource-health-checks-resource-types.md) sistem durumu nasıl değerlendirildiği hakkında ek bilgi.

## <a name="health-status-provided-by-resource-health"></a>Kaynak durumu tarafından sağlanan sistem durumu
bir kaynağın Hello sistem durumlarını izleyen hello biridir:

### <a name="available"></a>Kullanılabilir
Merhaba hizmet hello kaynak hello durumunu etkileyen herhangi bir olayı algılamadı. Burada hello kaynak kurtarıldı Planlanmamış kapalı kalma süresi sırasında hello son durumlarda görürsünüz: 24 saat hello **kısa süre önce kurtarıldıysa** bildirim.

![Kaynak sistem durumu kullanılabilir sanal makine](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a>Kullanılamıyor
Merhaba hizmeti devam eden platform veya hello kaynak hello sağlığını etkileyen olmayan platform olayı algıladı.

#### <a name="platform-events"></a>Platform olayları
Bu olaylar, birden çok hello Azure altyapı bileşenleri tarafından tetiklenen ve hem planlı bakım gibi zamanlanmış Eylemler ve planlanmamış ana bilgisayar yeniden başlatma gibi beklenmeyen olaylar içerir.

Kaynak durumu hello olay hello kurtarma işlemi ek ayrıntılar sağlar ve etkin bir Microsoft sözleşmesi destek yüklü olmasa bile, toocontact desteği sağlar.

![Kaynak durumu kullanılamıyor sanal makine tooplatform olay süresi](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a>Platform olmayan olaylar
Bu olaylar, örneğin bir sanal makineyi durdurmak veya bağlantıları tooa Redis önbelleği hello sayısının ulaşmasını kullanıcılar tarafından gerçekleştirilen eylemler tarafından tetiklenir.

![Kaynak durumu kullanılamıyor sanal makine toonon platform olayı nedeniyle](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a>Bilinmeyen
Bu sistem durumu, kaynak durumu 10 dakikadan bu kaynak hakkındaki bilgileri almadığını gösterir. Bu durum hello kaynak hello durumunun kesin bir gösterge olmamasına karşın, bir sorun giderme işlemi hello önemli veri noktası verilmiştir:
* Merhaba kaynak hello kaynak beklenen hello durumu çalışıyorsa, tooAvailable birkaç dakika sonra güncelleştirin.
* Merhaba kaynak sorunlarla karşılaşıyorsanız, hello bilinmeyen durumu hello kaynak hello Platform bir olay tarafından etkilenen önerebilir.

![Kaynak sistem durumu bilinmeyen sanal makine](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a>Yanlış bir durum raporu
Herhangi bir noktada hello geçerli sistem durumu hatalı olduğunu düşünüyorsanız, bize tıklayarak bildiğiniz **yanlış sistem durumu raporu**. Burada bir Azure sorundan etkilenen durumlarda hello kaynak sistem durumu dikey toocontact Destek'ten öneririz. 

![Kaynak durumu rapor yanlış durumu](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a>Geçmiş bilgileri
Geçmiş durumu verilerinin too14 günleri tıklatarak erişebilirsiniz **geçmişini görüntüleme** hello kaynak sistem durumu dikey. 

![Kaynak durumu rapor geçmişi](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a>Başlarken
tooopen bir kaynak için kaynak durumu
1.  Hello Azure portalında oturum açın.
2.  Tooyour kaynak gidin.
3.  Merhaba kaynak menüsünü Hello sol tarafta bulunan **kaynak durumu**.

![Kaynak dikey penceresinden açık kaynak durumu](./media/resource-health-overview/from-resource-blade.png)

Kaynak durumu tıklatarak da erişebilirsiniz **daha fazla hizmet**, yazarak **kaynak durumu** filtre metin kutusu tooopen hello içinde **Yardım + Destek** dikey. Son olarak tıklatın [ **kaynak durumu**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).

![Daha fazla hizmetinden açık kaynak durumu](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a>Sonraki adımlar

Bu kaynaklar toolearn kaynak durumu hakkında daha fazla gözden geçirin:
-  [Kaynak türleri ve sistem durumu denetler Azure kaynak durumu](resource-health-checks-resource-types.md)
-  [Azure kaynak durumu hakkında sık sorulan sorular](resource-health-faq.md)




