---
title: "bir grubun veya koleksiyonun - Azure mantıksal uygulamaları olarak aaaBatch işlem iletilerinin | Microsoft Docs"
description: "Toplu işleme logic apps içinde ileti gönderme ve alma"
keywords: "Batch, toplu işlem"
author: jonfancey
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/7/2017
ms.author: LADocs; estfan; jonfan
ms.openlocfilehash: 2603db71ee0659d5b6bf5ce3d32f1b0d13c34194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="send-receive-and-batch-process-messages-in-logic-apps"></a>Gönderme, alma ve logic apps işlem iletileri toplu

tooprocess iletileri gruplarında birlikte, veri öğeleri ya da iletileri tooa gönderebilir *toplu*ve ardından bu öğeleri toplu iş olarak işlem. Bu yaklaşım, toomake emin veri öğelerini birlikte işlenir ve belirli bir şekilde gruplama istediğinizde yararlıdır. 

Hello kullanarak toplu iş olarak öğeleri alma mantıksal uygulamalar oluşturabileceğiniz **toplu** tetikleyici. Daha sonra hello kullanarak öğeleri tooa toplu iş gönderme logic apps oluşturabilirsiniz **toplu** eylem.

Bu konu, bu görevleri gerçekleştirerek toplu bir çözümü nasıl oluşturabilirsiniz gösterir: 

* [Alan ve öğeleri toplu iş olarak toplayan bir mantıksal uygulama oluşturma](#batch-receiver). Merhaba alıcı mantıksal uygulama serbest bırakır ve öğelerini işler önce bu "toplu alıcı" mantıksal uygulama hello toplu ad ve sürüm ölçütlerini toomeet belirtir. 

* [Öğeleri tooa toplu gönderen bir mantıksal uygulama oluşturma](#batch-sender). Bu "toplu gönderen" mantıksal uygulama yeri belirtir var olan bir toplu alıcı mantığı uygulamaya olmalıdır toosend öğeleri. Ayrıca, bir müşteri numarası gibi benzersiz bir anahtar belirtin, çok "Bölüm" veya bölmek, bu anahtarı temel alt kümeler halinde hello hedef toplu. Böylece, tüm öğeleri aynı anahtarla toplanan ve birlikte işlenebilir. 

## <a name="requirements"></a>Gereksinimler

toofollow Bu örnekte, bu öğeler gerekir:

* Azure aboneliği. Bir aboneliğiniz yoksa [ücretsiz bir Azure hesabı ile başlayabilirsiniz](https://azure.microsoft.com/free/). Ya da [Kullandıkça Öde aboneliğine kaydolabilirsiniz](https://azure.microsoft.com/pricing/purchase-options/).

* Hakkındaki temel bilgileri [nasıl toocreate mantıksal uygulamalar](../logic-apps/logic-apps-create-a-logic-app.md) 

* Herhangi bir e-posta hesabı [Azure mantıksal uygulamaları tarafından desteklenen e-posta sağlayıcısı](../connectors/apis-list.md)

<a name="batch-receiver"></a>

## <a name="create-logic-apps-that-receive-messages-as-a-batch"></a>Toplu iş olarak iletilerini mantıksal uygulamalar oluşturma

İletileri tooa toplu göndermeden önce hello ile bir "toplu alıcı" mantıksal uygulama oluşturmanız gerekir **toplu** tetikleyici. Bu şekilde hello gönderen mantıksal uygulama oluşturduğunuzda, bu alıcı mantıksal uygulama seçebilirsiniz. Merhaba alıcısı için hello toplu işlem adı, sürüm ölçütlerini ve diğer ayarları belirtin. 

Gönderen logic apps alıcı logic apps tooknow hello Gönderenler hakkında herhangi bir şey gerekmez ancak burada toosend öğe, bilmeniz.

1. Merhaba, [Azure portal](https://portal.azure.com), bu ada sahip bir mantıksal uygulama oluşturma: "BatchReceiver" 

2. Logic Apps Tasarımcısı'nda hello eklemek **toplu** , logic app iş akışınızı başlatır tetikleyici. Merhaba arama kutusuna "toplu", filtre olarak girin. Bu tetikleyici seçin: **toplu – toplu iletileri**

   ![Toplu tetikleyicisi ekleyin](./media/logic-apps-batch-process-send-receive-messages/add-batch-receiver-trigger.png)

3. Merhaba toplu işlem için bir ad sağlayın ve hello toplu, örneğin serbest ölçütlerini belirtin:

   * **Toplu işlemi adı**: Bu örnekte "TestBatch" olan hello kullanılan ad tooidentify hello toplu işlem.
   * **İleti sayısı**: Merhaba iletileri toohold sayısı toplu iş olarak bu örnekte, "5" olan işlenmek üzere serbest bırakmadan önce.

   ![Toplu iş tetikleyici ayrıntılarını sağlayın](./media/logic-apps-batch-process-send-receive-messages/receive-batch-trigger-details.png)

4. Merhaba toplu tetikleyici başlatıldığında, bir e-posta gönderen başka bir eylem ekleyin. Her zaman hello toplu beş öğelerine sahip, hello mantıksal uygulama bir e-posta gönderir.

   1. Merhaba toplu tetikleyici altında seçin **+ yeni adım** > **Eylem Ekle**.

   2. Merhaba arama kutusuna "e-posta", filtre olarak girin.
   E-posta sağlayıcınız üzerinde bağlı olarak, bir e-posta Bağlayıcısı'nı seçin.
   
      Örneğin, bir iş veya Okul hesabınız varsa, hello Office 365 Outlook bağlayıcıyı seçin. 
      Gmail hesabınız varsa, hello Gmail Bağlayıcısı'nı seçin.

   3. Bu eylem, bağlayıcı için seçin:  **{*e-posta sağlayıcısı*}-bir e-posta ** Gönder

      Örneğin:

      ![E-posta sağlayıcınız için "bir e-posta Gönder" eylemini seçin](./media/logic-apps-batch-process-send-receive-messages/add-send-email-action.png)

5. E-posta sağlayıcınız için daha önce bir bağlantı oluşturmadıysanız, istendiğinde kimlik doğrulaması için e-posta kimlik bilgilerinizi sağlayın. Daha fazla bilgi edinmek [e-posta kimlik bilgilerinizi kimlik doğrulaması](../logic-apps/logic-apps-create-a-logic-app.md).

6. Yeni eklediğiniz hello eylemin Hello özellikleri ayarlayın.

   * Merhaba, **için** kutusuna, hello alıcının e-posta adresi girin. 
   Test amacıyla, kendi e-posta adresini kullanabilirsiniz.

   * Merhaba, **konu** kutusunda, hello zaman **dinamik içerik** seçin hello listesi görüntülenir, **bölüm adı** alan.

     !["Bölüm adı" Hello "Dinamik içerik" listeden seçin](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details.png)

     Bir sonraki bölümde böler hedef toplu içine mantıksal hello benzersiz bölüm anahtarı iletiler gönderebilir toowhere ayarlar belirtebilirsiniz. 
     Her küme hello gönderen mantıksal uygulama tarafından oluşturulan benzersiz bir numara vardır. 
     Bu özelliği, tek bir toplu iş ile birden çok alt kümelerini kullanın ve her alt sağladığınız hello adıyla tanımlamak olanak sağlar.

   * Merhaba, **gövde** kutusunda, hello zaman **dinamik içerik** seçin hello listesi görüntülenir, **ileti kimliği** alan.

     !["Body" için "İleti kimliği" seçin](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details-for-each.png)

     Merhaba giriş hello gönderme e-posta eylemi için bir dizi olduğundan hello Tasarımcısı otomatik olarak ekler bir **her** döngü hello geçici **bir e-posta Gönder** eylem. 
     Bu döngü hello toplu işteki her öğe hello iç eylemi gerçekleştirir. 
     Bu nedenle, hello toplu tetikleyici kümesi toofive öğeleri ile her zaman hello tetikleyici harekete beş e-postaları alır.

7.  Bir toplu alıcı mantıksal uygulama oluşturduğunuza göre mantıksal uygulamanızı kaydedin.

    ![Mantıksal uygulamanızı kaydetme](./media/logic-apps-batch-process-send-receive-messages/save-batch-receiver-logic-app.png)

<a name="batch-sender"></a>

## <a name="create-logic-apps-that-send-messages-tooa-batch"></a>İletileri tooa yığını gönderme mantıksal uygulamalar oluşturma

Şimdi hello alıcı mantıksal uygulama tarafından tanımlanan öğeleri toohello yığını gönderme bir veya daha fazla mantıksal uygulamalar oluşturun. Merhaba gönderen için hello alıcı mantıksal uygulama ve toplu işlem adı, ileti içeriği ve diğer ayarları belirtin. İsteğe bağlı olarak bu anahtarla alt kümelerini toocollect öğeleri benzersiz bir bölüm anahtarı toodivide hello toplu sağlayabilir.

Gönderen logic apps alıcı logic apps tooknow hello Gönderenler hakkında herhangi bir şey gerekmez ancak burada toosend öğe, bilmeniz.

1. Bu ada sahip başka bir mantıksal uygulama oluşturma: "BatchSender"

   1. Merhaba arama kutusuna "recurrence", filtre olarak girin. 
   Bu tetikleyici seçin: **çizelgesi - yineleme**

      ![Merhaba "Yinelemeyi Zamanla" tetikleyicisi ekleyin](./media/logic-apps-batch-process-send-receive-messages/add-schedule-trigger-batch-receiver.png)

   2. Merhaba sıklık ve aralığı toorun hello gönderen mantıksal uygulama dakikada ayarlayın.

      ![Sıklık ve aralığı yinelenme tetikleyici için ayarlayın](./media/logic-apps-batch-process-send-receive-messages/recurrence-trigger-batch-receiver-details.png)

2. İletileri tooa toplu göndermek için yeni bir adımı ekleyin.

   1. Merhaba yinelenme tetikleyici altında seçin **+ yeni adım** > **Eylem Ekle**.

   2. Merhaba arama kutusuna "toplu", filtre olarak girin. 

   3. Bu eylem seçin: **Gönder iletileri toobatch – toplu tetikleyici Logic Apps akışıyla seçin**

      !["İletileri toobatch Gönder"'i seçin](./media/logic-apps-batch-process-send-receive-messages/send-messages-batch-action.png)

   4. Şimdi bir eylemi olarak artık görünen daha önce oluşturduğunuz "BatchReceiver" mantıksal uygulamanızı seçin.

      !["Toplu alıcı" mantıksal uygulama seçin](./media/logic-apps-batch-process-send-receive-messages/send-batch-select-batch-receiver.png)

      > [!NOTE]
      > Merhaba liste toplu Tetikleyicileri sahip herhangi bir mantıksal uygulamalar da gösterir.

3. Merhaba toplu özellikleri ayarlayın.

   * **Toplu işlemi adı**: "TestBatch" Bu örnekte ve çalışma zamanında doğrulanır hello alıcı mantıksal uygulama tarafından tanımlanan hello toplu işlem adı.

     > [!IMPORTANT]
     > Merhaba alıcı mantıksal uygulama tarafından belirtilen hello toplu adıyla eşleşmelidir hello toplu adı değiştirmemeniz emin olun.
     > Değişen hello Tpl hello gönderen mantığı uygulama toofail neden olur.

   * **İleti içeriği**: Merhaba toosend istediğiniz ileti içeriği. 
   Bu örnekte, eklemeleri iletisine hello toohello toplu iş gönderme içerik geçerli tarih ve saat hello bu deyim ekleyin:

     1. Ne zaman hello **dinamik içerik** listesi görüntülenir, seçin **ifade**. 
     2. Merhaba ifade girin **utcnow()**ve seçin **Tamam**. 

        !["İletisi içeriği", "İfadesi" seçin. "Utcnow()" girin.](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details.png)

4. Şimdi hello toplu işlemi için bir bölüm ayarlayın. Hello "BatchReceiver" eylemini seçin **Gelişmiş Seçenekleri Göster**.

   * **Bölüm adı**: hello hedef toplu bölme için bir isteğe bağlı benzersiz bir bölüm anahtarı toouse. Bu örnekte, bir ile beş arasında rastgele bir sayı oluşturan bir deyim ekleyin.
   
     1. Ne zaman hello **dinamik içerik** listesi görüntülenir, seçin **ifade**.
     2. Bu ifade girin: **rand(1,6)**

        ![Hedef toplu işlemi için bir bölüm ayarlama](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-partition-advanced-options.png)

        Bu **rand** işlevi bir ile beş arasında bir sayı oluşturur. 
        Bu nedenle, bu toplu Bu ifade dinamik olarak ayarlayan beş numaralı, bölümlemesinde.

   * **İleti kimliği**: isteğe bağlı ileti tanımlayıcısı ve boş olduğunda oluşturulan bir GUID. 
   Bu örnekte, bu kutuyu boş bırakın.

5. Mantıksal uygulamanızı kaydedin. Gönderen mantıksal uygulamanızı şimdi benzer toothis örnek görünür:

   ![Gönderen mantıksal uygulamanızı kaydetme](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details-finished.png)

## <a name="test-your-logic-apps"></a>Mantıksal uygulamalarınızı test etme

tootest, çözüm, toplu işleme için bir kaç dakika çalıştıran logic apps bırakın. Bir süre sonra grupları beş e-postaları almaya başlayın, tüm hello ile aynı anahtar bölüm.

BatchSender mantıksal uygulamanızı dakikada çalışır, bir ile beş arasında rastgele bir sayı oluşturur ve iletileri gönderildiği hello bölüm anahtarı hello hedef toplu olarak oluşturulan bu numarayı kullanır. Merhaba toplu hello ile beş öğelerine sahip her zaman aynı bölüm anahtarı, BatchReceiver mantıksal uygulamanızı başlatılır ve her ileti için posta gönderir.

> [!IMPORTANT]
> Bitirdiğinizde test, hello BatchSender mantığı uygulama toostop iletileri gönderme devre dışı bırakın ve gelen aşırı kaçının emin olun.

## <a name="next-steps"></a>Sonraki adımlar

* [JSON kullanarak mantıksal uygulama tanımları oluşturma](../logic-apps/logic-apps-author-definitions.md)
* [Visual Studio'da Azure Logic Apps ve işlevleri ile sunucusuz bir uygulama oluşturun](../logic-apps/logic-apps-serverless-get-started-vs.md)
* [Özel durum işleme ve logic apps için hata günlüğü](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
