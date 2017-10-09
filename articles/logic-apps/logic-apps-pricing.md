---
title: aaaPricing & Fatura - Azure Logic Apps | Microsoft Docs
description: "Fiyatlandırma ve faturalama Azure mantıksal uygulamaları için nasıl çalıştığını öğrenin."
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: f8f528f5-51c5-4006-b571-54ef74532f32
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: LADocs; klam
ms.openlocfilehash: fa10cbbf7657afba7fadb7c76817b7a5e4af7b42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-pricing-model"></a>Logic Apps fiyatlandırma modeli
Azure mantıksal uygulamaları tooscale sağlar ve tümleştirme iş akışları hello bulutta yürütün.  Faturalama ve fiyatlandırma planı Logic Apps için hello ilgili ayrıntılar verilmiştir.
## <a name="consumption-pricing"></a>Tüketim fiyatlandırma
Yeni oluşturulan Logic Apps tüketim planını kullanın. Merhaba Logic Apps tüketim fiyatlandırma modeli ile yalnızca, kullanım için ödeme yaparsınız.  Logic Apps tüketim planı kullanırken kısıtlanan değil.
Bir mantıksal uygulama örneğini'nın çalıştırılmasıyla yürütülen tüm eylemler ölçülen.
### <a name="what-are-action-executions"></a>Eylem yürütmeleri nelerdir?
Her bir mantıksal uygulama tanımını tooconnectors ve çağrıları toonative Eylemler tetikleyiciler, koşullar, her döngü için kapsamı döngüler kadar gibi denetim akışı adımlarını içeren bir eylemi çağırır adımdır.
Tetikleyiciler tasarlanmış tooinstantiate bir mantıksal uygulama yeni bir örneğini belirli bir olay gerçekleştiğinde olan özel eylemlerdir.  Merhaba mantıksal uygulama nasıl ölçülen etkileyebilecek Tetikleyiciler için birkaç farklı davranışlar vardır.
* **Yoklama tetikleyici** – bir mantıksal uygulama örneğini oluşturmak için hello ölçütlerini karşılayan bir ileti alıncaya kadar Bu tetikleyici sürekli bir uç nokta yoklar.  Merhaba yoklama aralığı hello mantığı Uygulama Tasarımcısı hello tetikleyici içinde yapılandırılabilir.  Bir mantıksal uygulama örneğini oluşturmaz olsa bile her yoklama isteği bir eylem yürütme olarak sayılır.
* **Web kancası tetikleyici** – Bu tetikleyici istemci toosend için belirli bir noktadaki bir istek bekler.  Bir eylem yürütme olarak toohello Web kancası endpoint sayar her isteği gönderdi. Merhaba istek ve hello HTTP Web kancası tetikleyici her iki Web kancası Tetikleyicileri markalarıdır.
* **Yineleme tetikleyici** – Bu tetikleyici hello tetikleyici yapılandırılmış hello yinelenme aralığını temel hello mantıksal uygulama örneğini oluşturur.  Örneğin, bir yineleme tetikleyici yapılandırılmış toorun üç günde veya hatta dakikada olabilir.

Tetikleyici yürütmeleri hello Logic Apps kaynak dikey penceresinde hello tetikleyici Geçmiş bölümü görülebilir.

Yürütülen, tüm eylemler bunlar başarılı veya başarısız bir eylem yürütme olarak ölçülen.  Tooa koşulu karşılanmadı atlandı eylem veya hello mantıksal uygulama tamamlanmadan önce sonlandırıldığından yürütme kaydetmedi Eylemler eylem yürütmeleri sayılmaz.

Döngüler içinde yürütülen eylemler hello döngü tekrarında sayılır.  Örneğin, tek bir işlemde bir her bir döngü için 10 öğelerin listesini yineleme sayılır hello sayısı (1) hello Döngüdeki Eylemler hello sayısı ile çarpılır (10) hello listedeki öğeleri olarak hello başlatma hello döngüsü için artı , bu örnekte, olacak (10 * 1) + 1 = 11 eylem yürütmeleri.
Devre dışı Logic Apps örneği yeni örnek bulunamaz ve bu nedenle, devre dışı sırasında değil ücretlendirilirsiniz.  Bir mantıksal uygulama devre dışı bıraktıktan sonra tamamen devre dışı bırakılıyor önce hello örnekleri tooquiesce biraz zaman alabileceğini dikkatli olun.
### <a name="integration-account-usage"></a>Tümleştirme hesabı kullanımı
Tüketim tabanlı kullanımı dahil olduğu bir [tümleştirme hesabını](logic-apps-enterprise-integration-create-integration-account.md) keşfi, geliştirme ve sınama amacıyla toouse hello izin vermek için [B2B/EDI](logic-apps-enterprise-integration-b2b.md) ve [XML işleme](logic-apps-enterprise-integration-xml.md)Logic Apps özelliklerini hiçbir ek ücret ödemeden. Bir hesap bölge başına maksimum mümkün toocreate olan ve too10 anlaşmalar ve 25 eşlemeleri depolamak. Şemalar, sertifikalar ve iş ortakları sınırsız sahip ve gerektiği kadar karşıya yükleyebilirsiniz.

Ayrıca toohello eklenmesi tümleştirme hesapları tüketimi ile standart tümleştirme hesapları bu sınırlar olmadan ve bizim standart Logic Apps SLA de oluşturabilirsiniz. Daha fazla bilgi için bkz: [Azure fiyatlandırma](https://azure.microsoft.com/pricing/details/logic-apps).

## <a name="app-service-plans"></a>App Service planları
Bir uygulama hizmeti planı başvuran daha önce oluşturduğunuz mantıksal uygulamalar olarak toobehave önce devam eder. Merhaba belirlenen günlük yürütmeleri aşıldığında hello eylem yürütme ölçer kullanarak faturalandırılır sonra ancak seçilen hello plana bağlı olarak, kısıtlanan.
Bir uygulama hizmeti planı toobe açıkça hello mantıksal uygulama ile ilişkili olmayan, kendi içinde aboneliğiniz EA müşteriler hello dahil edilen miktarlar avantajı alın.  Örneğin, standart bir uygulama hizmeti planı varsa, EA aboneliğinizi ve bir mantıksal uygulama aynı abonelik hello sonra (bkz. aşağıdaki tablonun) günde 10.000 eylem yürütmeleri için ücretlendirilmezsiniz. 

App Service planları ve onların günlük izin verilen eylem yürütmeleri:
|  | Serbest / / temel paylaşılan | Standart | Premium |
| --- | --- | --- | --- |
| Gün başına eylem yürütmeleri |200 |10,000 |50,000 |
### <a name="convert-from-app-service-plan-pricing-tooconsumption"></a>Uygulama hizmeti planına tooConsumption fiyatlandırma Dönüştür
kendisiyle ilişkili bir uygulama hizmeti planı sahip bir mantıksal uygulama toochange tooa tüketim modelini, Kaldır hello başvuru toohello App Service planı hello mantıksal uygulama tanımında.  Bu değişikliği bir çağrı tooa PowerShell cmdlet'iyle yapılabilir:`Set-AzureRmLogicApp -ResourceGroupName ‘rgname’ -Name ‘wfname’ –UseConsumptionModel -Force`
## <a name="pricing"></a>Fiyatlandırma
Fiyatlandırma ayrıntıları için bkz: [Logic Apps fiyatlandırma](https://azure.microsoft.com/pricing/details/logic-apps).

## <a name="next-steps"></a>Sonraki adımlar
* [Logic Apps genel bakış][whatis]
* [İlk mantıksal uygulamanızı oluşturma][create]

[pricing]: https://azure.microsoft.com/pricing/details/logic-apps/
[whatis]: logic-apps-what-are-logic-apps.md
[create]: logic-apps-create-a-logic-app.md

