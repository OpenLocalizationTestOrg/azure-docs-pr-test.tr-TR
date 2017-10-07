---
title: "aaaAdministration ve BizTalk Services Geliştirme görev listesinde | Microsoft Docs"
description: "Planlama ve iş Azure BizTalk Services dağıtmak için yardımcı."
services: biztalk-services
documentationcenter: 
author: msftman
manager: erikre
editor: 
ms.assetid: 0ab70b5b-1a88-4ba5-b329-ec51b785010e
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2016
ms.author: deonhe
ms.openlocfilehash: 544c6b23fcbc2267598b713dbe1626699099d181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="administration-and-development-task-list-in-biztalk-services"></a>Yönetim ve geliştirme görev listesinde BizTalk Hizmetleri

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

## <a name="getting-started"></a>Başlarken
Microsoft Azure BizTalk Services ile çalışırken, çeşitli şirket içi ve bulut tabanlı bileşenleri tooconsider vardır. başlatıldı, tooget işlem akışı aşağıdaki hello göz önünde bulundurun:  

| Adım | Kimin sorumlu olduğunu | Görev | İlgili bağlantılar |
| --- | --- | --- | --- |
| 1. |Yönetici |Merhaba bir Microsoft hesabı veya kurumsal bir hesap kullanarak Microsoft Azure aboneliği oluşturma |[Klasik Azure Portalı](http://go.microsoft.com/fwlink/p/?LinkID=213885) |
| 2. |Yönetici |Oluşturun veya bir BizTalk hizmeti sağlanamadı. |[Klasik Azure portalını kullanarak BizTalk hizmeti oluşturma](http://go.microsoft.com/fwlink/p/?LinkID=302280) |
| 3. |Yönetici |Siz veya şirketinizin BizTalk Services Dağıtımı kaydetme |[Kaydetme ve hello BizTalk Services portalı üzerinde bir BizTalk hizmeti dağıtımı güncelleştiriliyor](https://msdn.microsoft.com/library/azure/hh689837.aspx) |
| 4. |Yönetici |Merhaba uygulaması BizTalk bağdaştırıcı hizmeti tooconnect tooan şirket içi iş kolu (LOB) sistemine kullanır veya bir kuyruk veya konu hedef kullanıyorsa geçerlidir.  Hello Azure hizmet veri yolu Namespace oluşturun. Bu ad alanı, hizmet veri yolu verenin adı ve hizmet veri yolu verenin anahtarı değerlerini toohello Geliştirici verin. |[Nasıl yapılır: oluşturmak veya bir hizmet veri yolu hizmet Namespace değiştirmek](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md) ve [alma verenin adı ve verenin anahtarı değerleri](biztalk-issuer-name-issuer-key.md) |
| 5. |Geliştirici |Merhaba SDK yükleyin ve Visual Studio'da hello BizTalk hizmeti projesi oluşturun. |[Azure BizTalk Services SDK'sı yükleme](https://msdn.microsoft.com/library/azure/hh689760.aspx) ve [Azure üzerinde zengin Mesajlaşma uç noktaları oluşturma](https://msdn.microsoft.com/library/azure/hh689766.aspx) |
| 6. |Geliştirici |BizTalk hizmeti Azure üzerinde barındırılan, BizTalk hizmeti proje tooyour dağıtın. |[Dağıtma ve hello BizTalk Services projesi yenileme](https://msdn.microsoft.com/library/azure/hh689881.aspx) |
| 7. |Yönetici |EDI kullanıyorsanız geçerlidir.  İş ortakları ekleyin ve Microsoft Azure BizTalk Services portalı hello üzerinde anlaşmaları oluşturun. Bir sözleşme oluşturduğunuzda hello Köprüsü ve/veya hello Geliştirici toohello sözleşmesi ayarları tarafından oluşturulan dönüşümler ekleyebilirsiniz. |[BizTalk Hizmetleri portalında EDI, AS2 ve EDIFACT yapılandırma](https://msdn.microsoft.com/library/azure/hh689853.aspx) |
| 8. |Yönetici |Hello Klasik Azure portalı kullanarak, performans ölçümleri de dahil olmak üzere, BizTalk hizmetinize hello durumunu izleyin. |[BizTalk Services: Pano, İzleyici ve Ölçek sekmeleri](http://go.microsoft.com/fwlink/p/?LinkID=302281) |
| 9. |Yönetici |Merhaba Microsoft Azure BizTalk Services Portalı'nı kullanarak, BizTalk Services ve izleme iletilerini hello köprüsü dosyaları tarafından işlenen olarak kullanılan hello yapıları yönetin. |[Merhaba BizTalk Services portalı kullanma](https://msdn.microsoft.com/library/azure/dn874043.aspx) |
| 10. |Yönetici |Bir yedekleme planı tooback yukarı hello BizTalk hizmeti oluşturun. |[İş devamlılığı ve olağanüstü durum kurtarma BizTalk Hizmetleri](https://msdn.microsoft.com/library/azure/dn509557.aspx) |

## <a name="next-steps"></a>Sonraki Adımlar
[Öğreticiler ve örnekler](https://msdn.microsoft.com/library/azure/hh689895.aspx)

[Visual Studio'da Hello projesi oluşturma](https://msdn.microsoft.com/library/azure/hh689811.aspx)

[Azure BizTalk Services SDK'sını yükleyin](https://msdn.microsoft.com/library/azure/hh689760.aspx)

## <a name="concepts"></a>Kavramlar
[Visual Studio'da Hello projesi oluşturma](https://msdn.microsoft.com/library/azure/hh689811.aspx)  
[EDI, AS2 ve EDIFACT Mesajlaşma (iş tooBusiness)](https://msdn.microsoft.com/library/azure/hh689898.aspx)  

## <a name="other-resources"></a>Diğer Kaynaklar
[Kaynak ve hedef köprüsü Mesajlaşma uç noktaları ekleme](https://msdn.microsoft.com/library/azure/hh689877.aspx)  
[İleti eşlemeleri ve dönüşümler oluşturmak ve bilgi edinin](https://msdn.microsoft.com/library/azure/hh689905.aspx)  
[Merhaba BizTalk bağdaştırıcı hizmeti (BAS) kullanma](https://msdn.microsoft.com/library/azure/hh689889.aspx)  
[Azure BizTalk Hizmetleri](http://go.microsoft.com/fwlink/p/?LinkID=303664)

