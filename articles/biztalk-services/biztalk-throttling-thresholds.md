---
title: "BizTalk Services azaltma hakkında aaaLearn | Microsoft Docs"
description: "Eşikleri azaltma ve BizTalk Services için çalışma zamanı davranışlarını kaynaklanan hakkında bilgi edinin. Azaltma, bellek kullanımı ve ileti sayısını temel alır. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: f6663cf2-cda4-4bac-855e-27d2ad5c4fa4
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 46c8806c3a1f4eeb793f721f849771e0ec155197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-throttling"></a>BizTalk Services: Azaltma

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Azure BizTalk Services uygulayan iki koşullara göre hizmet azaltma: bellek kullanımı ve hello işleme eşzamanlı ileti sayısı. Bu konuda daraltma eşikleri hello listeler ve azaltma bir koşul oluştuğunda hello çalışma zamanı davranışını tanımlar.

## <a name="throttling-thresholds"></a>Daraltma eşikleri
Aşağıdaki tabloda hello azaltma kaynak ve eşikleri hello:

|  | Açıklama | Düşük eşik | Yüksek eşiği |
| --- | --- | --- | --- |
| Bellek |Toplam sistem bellek kullanılabilir/PageFileBytes yüzdesi. <p><p>Toplam kullanılabilir PageFileBytes yaklaşık 2 kez hello RAM hello sisteminin olur. |60% |70% |
| İleti işleme |Aynı anda işlenen ileti sayısı |40 * çekirdek sayısı |100 * çekirdek sayısı |

Bir üst Eşiğe ulaşıldığında, Azure BizTalk Services toothrottle başlatır. Merhaba düşük Eşiğe ulaşıldığında azaltma durdurur. Örneğin, hizmetiniz %65 sistem bellek kullanıyor. Bu durumda, hello hizmet kısıtlama yok. Hizmetinizi % 70 sistem belleği kullanarak başlatır. Bu durumda, hello hizmeti kısıtlar ve toothrottle hello hizmeti, % 60 (düşük eşik) sistem belleği kullanır kadar devam eder.

Azure BizTalk Services durumunu (daraltılmış durumu karşılaştırması normal durum) azaltma hello ve süresini azaltma hello izler.

## <a name="runtime-behavior"></a>Çalışma zamanı davranışı
Azure BizTalk Services azaltma durumuna girdiğinde, hello şunlar olur:

* Azaltma rol örneğidir. Örneğin:<br/>
  RoleInstanceA azaltma. RoleInstanceB azaltma değil. Bu durumda, RoleInstanceB iletilerinde beklendiği gibi işlenir. RoleInstanceA iletilerinde atılır ve hello aşağıdaki hata ile başarısız:<br/><br/>
  **Sunucu meşgul. Lütfen yeniden deneyin.**<br/><br/>
* Herhangi bir çekme kaynağına etmeyin yoklamak veya bir ileti indirin. Örneğin:<br/>
  Ardışık iletilerin bir dış FTP kaynaktan çeker. Merhaba çekme yapılması hello rol örneği azaltma bir duruma alır. Bu durumda, azaltma hello rol örneği durdurur kadar ek iletilerin indirilmesi hello ardışık düzen durdurur.
* Merhaba istemci selamlama iletisine yeniden gönderebilirsiniz şekilde yanıt toohello istemci gönderilir.
* Merhaba azaltma çözülene kadar beklemeniz gerekir. Özellikle, Hello düşük eşik ulaşılana kadar beklemelisiniz.

## <a name="important-notes"></a>Önemli Notlar
* Azaltma devre dışı bırakılamaz.
* Daraltma eşikleri değiştirilemez.
* Azaltma, sistem genelinde uygulanır.
* Yerleşik azaltma Hello Azure SQL veritabanı sunucusuna da sahiptir.

## <a name="additional-azure-biztalk-services-topics"></a>Ek Azure BizTalk Services konuları
* [Hello Azure BizTalk Services SDK'sını yükleme](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [Öğretici: Azure BizTalk Hizmetleri](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [I Başlat'ı kullanarak Azure BizTalk Services SDK'sı nasıl hello](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Azure BizTalk Hizmetleri](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a>Ayrıca Bkz.
* [BizTalk Services: Geliştirici, temel, standart ve Premium sürümler grafiği](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [BizTalk Services: Klasik portalı kullanarak Azure hazırlama](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [BizTalk Services: Durum Grafiğini hazırlama](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [BizTalk Services: Pano, İzleyici ve Ölçek sekmeleri](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [BizTalk Services: Yedekleme ve Geri Yükleme](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [BizTalk Services: Verenin Adı ve Verenin Anahtarı](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

