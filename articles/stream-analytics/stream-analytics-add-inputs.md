---
title: "aaaAdd veri tooyour akış analizi işleri giriş | Microsoft Docs"
description: "Nasıl bir veri kaynağı tooyour Stream Analytics yukarı toohook iş Blog depolama verileri olay hub'ları veya başvuru olarak akış veri girişten öğrenin."
keywords: "veri akış girişi, veri"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: 
ms.assetid: 9e59bd24-2a80-4ecb-b6b2-309a07c70bcd
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 674000268fcdf9bc000af3e2f166cb66f1366922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-tooa-stream-analytics-job"></a>Akış veri girişi veya başvuru veri tooa Stream Analytics işi ekleme
Nasıl bir veri kaynağı tooyour Stream Analytics yukarı toohook işi olay hub'ları veya başvuru verileri Blob depolama biriminden olarak akış veri girişten öğrenin.

Azure Stream Analytics işleri bağlı tooone veri girişi veya daha fazla bilgi, her biri tanımlayan bir bağlantı tooan mevcut veri kaynağı olabilir. Toothat veri kaynağına gönderilen veri gibi hello akış analizi işi tarafından tüketilen ve gerçek zamanlı veri akışı olarak işlenir. Akış Analizi ile birinci sınıf tümleştirme sahip [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) ve [Azure Blob Depolama](../storage/blobs/storage-dotnet-how-to-use-blobs.md) hem içinde hem de hello işin abonelik dışında.

Bu makalede bir hello adımdır [Stream Analytics öğrenme yolu](/documentation/learning-paths/stream-analytics/).

## <a name="data-input-streaming-data-and-reference-data"></a>Veri girişi: akış veri ve başvuru verileri
İki farklı Stream Analytics girdi vardır: veri akışlarını ve başvuru verileri.

* **Veri akışları**: akış analizi işleri, tüketilen ve hello iş tarafından dönüştürülmüş en az bir veri akışı giriş toobe içermelidir. Azure Blob Depolama ve Azure Event Hubs veri akışı giriş kaynağı olarak desteklenir. Azure Event Hubs kullanılan toocollect olay bağlı aygıtları, hizmetler ve uygulamalar akışlarıdır. Azure Blob Depolama toplu veri akışı olarak alma için bir giriş kaynağı kullanılabilir.  
* **Başvuru verileri**: akış analizi, ikinci bir yardımcı giriş çağrılan başvuru veri türünü destekler.  Hareketli karşılıklı toodata bu verileri statik veya yavaşlamasının değiştirme.  Genellikle, göz atmayı ve veri akışlarını toocreate daha zengin bir veri kümesi ile bağıntıları gerçekleştirmek için kullanılır.  Azure Blob Depolama şu anda yalnızca desteklenen hello giriş başvuru verileri kaynağıdır.  

bir giriş tooyour Stream Analytics işi tooadd:

1. Hello Azure portal'ı tıklatın **girişleri** ve ardından **bir giriş eklemek** Stream Analytics işi.
   
    ![Klasik Azure portalı - bir giriş ekleyin.](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    Hello Azure portal tıklatın hello **girişleri** döşeme Stream Analytics işinde.  
   
    ![Azure portal - veri girişi ekleyin.](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. Merhaba giriş Hello türünü belirtin: ya da **veri akışı** veya **başvuru verileri**.
   
    ![Merhaba doğru veri girişi, akışı veya başvuru ekleme](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![Merhaba doğru veri girişi, akışı veya başvuru ekleme](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. Bir veri akış girişine oluşturuyorsanız, hello giriş için hello kaynak türünü belirtin.  Bu adım, yalnızca depolama birimi şu anda desteklenen Blob olarak başvuru verileri oluşturma sırasında atlanabilir.
   
    ![Veri akışı veri girişi ekleme](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![Veri akışı veri girişi ekleme](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. Bu giriş, giriş diğer adı kutusunu hello için kolay bir ad sağlayın.  Bu ad, işin bir sorguyu daha sonra toorefer toohello giriş olarak kullanılır.
   
    Merhaba gerekli bağlantı özelliklerini tooconnect tooyour veri kaynağının Hello kalan doldurun. Bu alanlar giriş ve kaynak türü türüne göre değişir ve ayrıntılı olarak tanımlanan [burada](stream-analytics-create-a-job.md).  
   
    ![Olay hub'ı veri girişi ekleme](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. Merhaba giriş verisi Hello serileştirme ayarları belirtin:
   
   * sorgularınızın beklediğiniz hello şekilde çalıştığından emin toomake belirtin hello **olayı seri hale getirme biçimi** gelen veri.  Desteklenen serileştirme biçimleri, JSON, CSV ve Avro olacaktır.
   * Merhaba doğrulayın **kodlama** hello veriler için.  UTF-8 hello kodlama biçimi şu anda yalnızca desteklenir. ' dir.
     
     ![Merhaba veri girişi için veri seri hale getirme ayarları](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![Merhaba veri girişi için veri seri hale getirme ayarları](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. Merhaba giriş oluşturmayı tamamladıktan sonra Stream Analytics toohello giriş kaynağına bağlanabildiğinizi doğrular.  Merhaba bildirim hub'hello bağlantıyı Test Et işlemi hello durumunu görüntüleyebilirsiniz.
   
    ![Giriş veri akış hello bağlantıyı sınayın](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![Giriş veri akış hello bağlantıyı sınayın](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a>Veri girişleri akış ile ilgili yardım alın
Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.

## <a name="next-steps"></a>Sonraki adımlar
* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)

