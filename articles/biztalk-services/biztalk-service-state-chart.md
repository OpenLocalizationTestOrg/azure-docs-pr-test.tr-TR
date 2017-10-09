---
title: "farklı durumları ya da BizTalk Services durumları izin aaaTasks | Microsoft Docs"
description: "Merhaba Eylemler/işlemleri farklı MABS durumunda izin: durdurmak, Başlat, yeniden başlatın, askıya alma, sürdürme, Sil, ölçeklendirme, Yukarı yapılandırma ve yedekleme güncelleştirme"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: aea738f3-ec76-4099-a41b-e17fea9e252f
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/08/2016
ms.author: mandia
ms.openlocfilehash: 643307ba6fa9b05c82b867912feab249c42b65dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-you-can-and-cant-do-using-hello-biztalk-service-state"></a>Neleri olabilir ve kullanarak yapamazsınız hello BizTalk hizmeti durumu

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Merhaba geçerli durumunu hello BizTalk hizmeti bağlı olarak, ya da BizTalk hizmeti hello üzerinde gerçekleştirilemiyor işlem vardır.

Örneğin, yeni bir BizTalk hizmeti hello Klasik Azure Portalı'nda sağlayın. Başarıyla tamamlandığında, BizTalk hizmeti hello bulunduğu `active` durumu. Merhaba etkin durumda durdurmak, askıya alma ve hello BizTalk hizmeti silin. Hello BizTalk Hizmeti Durdur ve durdurma başarısız olduysa hello BizTalk hizmeti gider tooa `StopFailed` durumu. Merhaba, `StopFailed` durumunda, hello BizTalk hizmeti yeniden. Sürdür'gibi izin verilmeyen bir işlem denerseniz aşağıdaki hata hello oluşur:

`Operation not allowed`

## <a name="view-hello-possible-states"></a>Görünüm hello olası durumlar

Merhaba aşağıdaki tablolarını listeleme hello işlemleri veya hello BizTalk hizmeti belirli bir durumda olduğunda yapılabilir eylemler. Bir ✔ hello işleme durumundayken bu izin anlamına gelir. Boş bir girdiyi hello o durumda gerçekleştirilemiyor anlamına gelir.

| Hizmet durumu | Başlatma | Durdur | Yeniden Başlatma | Askıya alma | Sürdür | Sil | Ölçek | Güncelleştirme <br/> Yapılandırma | Backup |
| --- | --- | --- | --- | --- | --- | --- |--- | --- | --- |
| Etkin |  | ✔ | ✔ | ✔ |  | ✔ |✔ |✔ |✔ |
| Devre dışı |  |  |  |  |  | ✔ | |  |  | 
| askıya alındı |  |  |  |  | ✔ | ✔ | |  | ✔ |
| Durduruldu | ✔ |  | ✔ |  |  | ✔ | |  | ✔ |
| Hizmet güncelleştirmesi başarısız oldu |  |  |  |  |  | ✔ | |  |  | 
| DisableFailed |  |  |  |  |  | ✔ | |  |  | 
| EnableFailed |  |  |  |  |  | ✔ | |  |  | 
| StartFailed <br/> StopFailed <br/> RestartFailed | ✔ | ✔ | ✔ |  |  | ✔ | | ✔ | |
| SuspendedFailed <br/> ResumeFailed|  |  |  | ✔ | ✔ | ✔ | |  |  | 
| CreatedFailed <br/> RestoreFailed |  |  |  |  |  | ✔ | |  |  | 
| ConfigUpdateFailed  |  |  | ✔ |  |  | ✔ | |✔ | |
| ScaleFailed |  |  |  |  |  | ✔ |✔ | |  |  | 



## <a name="see-also"></a>Ayrıca Bkz.
* [Merhaba Klasik Azure portalını kullanarak BizTalk hizmeti oluşturma](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [BizTalk Services hello Pano, İzleyici ve ölçek sekmeleri yapabilecekleriniz](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [Merhaba geliştirici, temel, standart ve Premium sürümlerinde BizTalk Services ile Al](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [Nasıl tooback ayarlama ve BizTalk hizmeti geri yükleme](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [BizTalk Services'da açıklandığı azaltma](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>
* [BizTalk hizmetiniz için Hello Service Bus ve erişim denetimi verenin adı ve verenin anahtar değerlerini alma](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>
* [I Başlat'ı kullanarak Azure BizTalk Services SDK'sı nasıl hello](http://go.microsoft.com/fwlink/p/?LinkID=302335)

