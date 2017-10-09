---
title: "Azure olay hub'ları ayrılmış kapasitesi aaaOverview | Microsoft Docs"
description: "Microsoft Azure olay hub'ları ayrılmış kapasite genel bakış."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: sethm;babanisa
ms.openlocfilehash: 79c09975e5c0a6d4729c8f836576770abaaf322e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-event-hubs-dedicated"></a>Ayrılmış Event Hubs'a genel bakış

*Olay hub'ları ayrılmış* kapasite tek Kiracı dağıtımları hello sahip müşteriler için zorlu gereksinimleri sunar. Tam ölçekli olarak Azure Event Hubs'a giriş için saniye başına veya tam olarak dayanıklı depolama ve alt ikinci gecikme süresi ile telemetri too2 GB saniye başına 2 milyondan olaylar. Bu işlem tarafından da etkinleştirir tümleşik çözüm gerçek zamanlı ve toplu olarak aynı sistem hello. Olay hub'ları hello Sunumda dahil arşiv ile gerçek zamanlı ve toplu tabanlı ardışık düzen destekleyen tek bir akış sağlayarak çözümünüzü hello karmaşıklığını azaltabilir.

Merhaba aşağıdaki tabloda hello kullanılabilir hizmet katmanları olay hub'larını karşılaştırır. Merhaba olay hub'ları ayrılmış Sabit aylık fiyat, standart ve temel çoğu özelliklerini fiyatlandırma karşılaştırılan toousage bir tekliftir. Merhaba ayrılmış katmanı hello standart planı ancak yoğun iş yükleri sahip müşteriler için Kurumsal ölçek kapasiteli hello özellikleri sunar. 

| Özellik | Temel | Standart | Adanmış |
| --- |:---:|:---:|:---:|
| Giriş olayları | Milyon olayları ödeme | Milyon olayları ödeme | Dahil |
| İşleme birimi (1 MB/sn giriş, çıkış 2 MB/sn) | Saat başına ödeme | Saat başına ödeme | Dahil |
| İleti Boyutu | 256 KB | 256 KB | 1 MB |
| Yayımcı ilkeleri | Yok | Evet | Evet |     
| Tüketici grupları | 1 - varsayılan | 20 | 20 |
| İleti yeniden yürütme | Evet | Evet | Evet |
| En fazla üretilen iş birimi | 20 | 20 (esnek too100)  | 1 CU≈200 |
| Aracılı bağlantılar | 100 dahil | 1.000 dahil | 100 dahil K |
| Ek Aracılı bağlantılar | Yok | Evet | Evet |
| İleti Saklama | 1 gün dahil | 1 gün dahil | Yukarı too7 gün dahil |
| Arşiv (Önizleme) | Yok   | Saat başına ödeme | Dahil |

## <a name="benefits-of-event-hubs-dedicated-capacity"></a>Olay hub'ları ayrılmış kapasite yararları

Olay hub'ları ayrılmış kullanırken aşağıdaki yararları hello kullanılabilir:

* Etkisiz diğer kiracıdan ile barındırma tek bir kiracı.
* İleti boyutu artar too1 MB karşılaştırıldığında gibi standart ve temel too256 KB.
* Yinelenebilir performans her zaman.
* Garantili kapasite toomeet, veri bloğu gerekiyor.
* Saniye başına milyon giriş olayları too2 sağlayan ölçeklenebilir 1 ile 8 kapasite birimlerinin (CU) – arasında.
  * Ö her CU yaklaşık 200 üretilen iş birimleri (TU) hello eşdeğer burada sağlayabilir hub olay ayrılmış için hello ölçek yönetin.
* Sıfır Bakım: biz Yük Dengeleme, işletim sistemi güncelleştirmeleri, güvenlik yamaları ve bölümleme yönetin.
* Aylık fiyatlandırma sabit.

Olay hub'ları ayrılmış hello verimlilik sınırlamaları hello standart sunumun bazıları da kaldırır. Üretilen iş birimleri temel ve standart katmanları, saniye başına ikinci ya da 1 MB TU ve çift çıkış miktarı başına giriş başına too1000 olay entitle. Merhaba ayrılmış ölçek sunumunun herhangi bir kısıtlama üzerinde giriş yok ve çıkış olay sayar. Bu sınırlar, olay hub'ları satın hello kapasitesini işleme hello tarafından yönetilir.

Bu hizmeti hello en büyük telemetri kullanıcılar hedeflenen ve bir kurumsal anlaşma ile kullanılabilir toocustomers.

## <a name="how-tooonboard"></a>Nasıl tooonboard

Merhaba platform olay hub'ları adanmış bir Kurumsal Anlaşma ö farklı boyutlarda ile sunulur. Her CU yaklaşık 200 üretilen iş birimleri hello eşdeğer sağlar. Kapasite yukarı veya aşağı hello ay toomeet gereksinimlerinizi ekleyerek veya kaldırarak ö ölçekleme yapabilirsiniz. Merhaba sizin için uygun olan olay hub'ları ürün ekibi tooget hello esnek dağıtım öğesinden daha uygulamalı ekleme yaşar hello ayrılmış planı benzersizdir. 

## <a name="next-steps"></a>Sonraki adımlar
Microsoft satış temsilcisi veya Microsoft Support tooget ek kapasitesi hakkında ayrıntılı olay hub'ları ayrılmış başvurun. Event Hubs hakkında daha fazla, bağlantılar aşağıdaki hello ziyaret ederek de öğrenebilirsiniz:

Fiyatlandırma hakkında ayrıntılı bilgi için bağlantılar aşağıdaki hello ziyaret edin:

- [Olay hub'ları ayrılmış fiyatlandırma](https://azure.microsoft.com/pricing/details/event-hubs/). Ayrıca, Microsoft satış temsilcisi veya Microsoft Support tooget ek kapasitesi hakkında ayrıntılı olay hub'ları ayrılmış başvurabilirsiniz.
- Merhaba [olay hub'ları SSS](event-hubs-faq.md) fiyatlandırma bilgileri içerir ve Event Hubs hakkında sık sorulan bazı sorular yanıtlanmaktadır. 
