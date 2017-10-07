---
title: "aaaDiagnose hataları - Azure Logic Apps | Microsoft Docs"
description: "Ortak yolları toounderstand logic apps nerede başarısız oluyor"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: a6727ebd-39bd-4298-9e68-2ae98738576e
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 46d318625820034c95e6df3a71ab84c58f076dd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-logic-app-failures"></a>Mantıksal uygulama hatalarını tanılama
Sorunları veya hatalar logic apps ile karşılaşırsanız, var olan birkaç yaklaşımlar burada hello hataları'ten gelen daha iyi anlamanıza yardımcı olabilir.  

## <a name="azure-portal-tools"></a>Azure portal araçları
Hello Azure portal birçok araçları toodiagnose her mantıksal uygulama her adımında sağlar.

### <a name="trigger-history"></a>Tetikleyici geçmişi

Her mantıksal uygulama en az bir tetikleyici sahiptir. Uygulamaları tetikleme olmayan fark ederseniz hello tetikleyici geçmişi daha fazla bilgi için ilk arayın. Merhaba mantığı app'ss ana dikey penceresinde hello tetikleyici geçmişi erişebilir.

![Merhaba tetikleyici geçmişi bulma][1]

Merhaba tetikleyici geçmişi mantıksal uygulamanızı yapılan tüm tetikleyici girişimleri listeler. Merhaba ayrıntılara, özellikle her tetikleyici girişimi toodrill tıklatabilirsiniz, herhangi bir girdi veya tetikleyici girişimi hello çıkışları oluşturulabilir. Başarısız Tetikleyicileri bulursanız, hello tetikleyici girişimi seçip hello **çıkışları** oluşturulan tüm hata iletilerini, örneğin, geçerli olmayan FTP için kimlik bilgilerini tooreview bağlantı.

Merhaba farklı durumlarını görebilirsiniz şunlardır:

* **Atlanan**. Merhaba uç noktası sorgulu toocheck verileri için olan ve hiçbir veri yoktu bir yanıt aldı.
* **Başarılı bir şekilde**. Merhaba tetikleyici verileri kullanılabilir bir yanıt aldı. Bu durum, el ile bir tetikleyici, yineleme tetikleyici ya da bir yoklama tetikleyici neden olabilir. Bu durum genellikle tarafından hello eşlik **Fired** durumu, bir koşul veya SplitOn komutu memnun değildi kod görünümünde olup olmadığını olmayabilir ancak.
* **Başarısız**. Bir hata oluştu.

#### <a name="start-a-trigger-manually"></a>Bir tetikleyici el ile başlatın

Kullanılabilir bir tetikleyicinin hemen hello sonraki yinelemesi beklemeden hello mantığı uygulama toocheck istiyorsanız, **Tetik Seç** hello ana dikey tooforce onay üzerinde. Örneğin, Dropbox tetikleyiciyle bu bağlantıyı tıklatarak yeni dosyalarda hello iş akışı tooimmediately yoklama Dropbox neden olur.

### <a name="run-history"></a>çalıştırma geçmişi

Her Mazotlu tetikleyici çalıştırılmasıyla sonuçlanır. Merhaba iş akışı sırasında neler olduğunu anlamanıza yardımcı olabilecek birçok ayrıntılarını içeren hello ana dikey penceresinden çalışma bilgilere erişebilir.

![Merhaba çalıştırma geçmişi bulma][2]

Bir çalışma durumlarını izleyen hello birini görüntüler:

* **Başarılı bir şekilde**. Tüm eylemleri başarılı oldu. Bir hata oluştu, bu hata oluştu. daha sonra hello iş akışında bir eylem tarafından işlendi. Diğer bir deyişle, hello hatası toorun başarısız eylemden sonra ayarlanmış bir eylem yürütüldü.
* **Başarısız**. En az bir eylemin hello iş akışı daha sonra bir eylemi tarafından işlenmedi bir hata vardı.
* **İptal**. Merhaba iş akışının çalıştığı ancak iptal isteği aldı.
* **Çalışan**. Merhaba iş akışı şu anda çalışıyor. Bu durum, daraltılmış iş akışları için ya da hello planı fiyatlandırma geçerli nedeniyle oluşabilir. Ayrıntılar için bkz [fiyatlandırma sayfası hello eylem sınırları](https://azure.microsoft.com/pricing/details/app-service/plans/). Tanılama (çalıştırma geçmişi hello altında görünür hello grafikleri) yapılandırma gerçekleşecek herhangi bir kısıtlama olayı hakkında bilgi de sağlayabilirsiniz.

Çalışma geçmişinize bakıldığında, daha fazla ayrıntı için ayrıntıya inebilir.  

#### <a name="trigger-outputs"></a>Tetikleyici çıkarır

Tetikleyici hello tetikleyiciyle gelen hello verileri göster çıkarır. Bu çıktılar tüm özellikleri beklendiği gibi döndürülen olup olmadığını belirlemenize yardımcı olabilir.

> [!NOTE]
> Anlamadığınız herhangi bir içerik görürseniz, nasıl Azure Logic Apps öğrenin [farklı içerik türlerini işleme](../logic-apps/logic-apps-content-type.md).
> 

![Tetikleyici çıkışı örnekleri][3]

#### <a name="action-inputs-and-outputs"></a>Eylem girişleri ve çıkışları

Merhaba giriş ve bir eylem alınan çıkış inebilir. Bu verilerin hello boyutu ve şekli ilgili hello çıktıların anlamak için ve ayrıca oluşturulmuş olabilir herhangi bir hata iletisi bulmak için yararlıdır.

![Eylem girişleri ve çıkışları][4]

## <a name="debug-workflow-runtime"></a>İş akışı çalışma zamanı hata ayıklama

Hello girişleri, çıkış ve bir çalışma Tetikleyicileri izleme ile birlikte hata ayıklamaya yardımcı bazı adımları tooa iş akışı ekleyebilirsiniz. 
[RequestBin](http://requestb.in) bir iş akışında bir adım olarak ekleyebileceğiniz güçlü bir araçtır. RequestBin kullanarak, bir HTTP isteği denetçisi toodetermine hello tam boyutunu, Şekil ve bir HTTP istek biçimini ayarlayabilirsiniz. Bir RequestBin oluşturun ve bir mantıksal uygulama HTTP POST eylemiyle tootest, örneğin istediğiniz gövdesi içeriği, bir ifade veya başka bir adım çıkış hello URL yapıştırın. Merhaba mantıksal uygulama çalıştırmak sonra hello isteği hello Logic Apps altyapısı, oluşturulan zaman nasıl oluşturulduğu, RequestBin toosee yenileyebilirsiniz.

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
