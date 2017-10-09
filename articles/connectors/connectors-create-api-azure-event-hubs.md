---
title: "Azure mantıksal uygulamaları için Azure Event Hubs ile Olay İzleyicisi yukarı aaaSet | Microsoft Docs"
description: "Veri akışları tooreceive olaylarını izlemek ve Azure Logic Apps ile Azure Event Hubs için olayları Gönder"
services: logic-apps
keywords: "veri akışı, olay izleme, olay hub'ları"
author: ecfan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: estfan; LADocs
ms.openlocfilehash: 4aad2c2ac1134b4d4d440019b4773559e49be122
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-receive-and-send-events-with-hello-event-hubs-connector"></a>İzleme, gönderip hello olay hub'ları bağlayıcı olayları

Olay İzleyici yukarı tooset mantıksal uygulamanızı olayları algılamak, olayları alabilir ve olayları, böylece tooan bağlanmak [Azure olay hub'ı](https://azure.microsoft.com/services/event-hubs) mantığı uygulamanızdan. Daha fazla bilgi edinmek [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).

## <a name="requirements"></a>Gereksinimler

* Toohave sahip bir [olay hub'ları ad alanı ve olay hub'ı](../event-hubs/event-hubs-create.md) azure'da. Bilgi [nasıl toocreate bir olay hub'ları ad alanı ve olay hub'ı](../event-hubs/event-hubs-create.md). 

* toouse [tüm bağlayıcıların](https://docs.microsoft.com/azure/connectors/apis-list) mantıksal uygulamanızı toocreate bir mantıksal uygulama öncelikle olması. Bilgi [nasıl toocreate bir mantıksal uygulama](../logic-apps/logic-apps-create-a-logic-app.md).

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-hello-connection-string"></a>Olay hub'ları ad alanı izinleri denetleyin ve hello bağlantı dizesini bulun

Logic app tooaccess için herhangi bir hizmet, toocreate sahip bir [ *bağlantı* ](./connectors-overview.md) yapmadıysanız mantığı uygulama ve hello hizmetiniz arasında. Bu bağlantı mantığı uygulama tooaccess verilerinizi yetkilendirir.
İçin logic app tooaccess toohave sahip olay Hub'ınızı **Yönet** izinleri ve Event Hubs ad alanınız için hello bağlantı dizesi.

toocheck izinleri ve get hello bağlantı dizesi, aşağıdaki adımları izleyin.

1.  İçinde toohello oturum [Azure portal](https://portal.azure.com "Azure portal"). 

2.  Tooyour olay hub'ları Git *ad alanı*, belirli olay hub'ı hello değil. Merhaba ad alanı dikey penceresinde, altında **ayarları**, seçin **paylaşılan erişim ilkeleri**. Altında **talep**, sahip olduğunuz onay **Yönet** bu ad alanı için izinleri.

    ![Olay hub'ı ad alanınız için izinleri yönetme](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  Merhaba olay hub'ları ad alanı, toocopy hello bağlantı dizesini seçin **RootManageSharedAccessKey**. Sonraki tooyour birincil anahtar bağlantı dizesi, hello Kopyala düğmesini seçin.

    ![Olay hub'ları ad alanı bağlantı dizesini kopyalayın](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > tooconfirm bağlantı dizenizi olay hub'ları ad alanınız ile veya belirli bir Event Hub ile ilişkili olup olmadığını denetleyin hello hello bağlantı dizesi `EntityPath` parametresi. Bu parametre bulursanız, hello bağlantı dizesi belirli olay hub için "varlığı" ve hello doğru dize toouse mantıksal uygulamanızı sahip değil.

4.  Şimdi bir olay hub'ları tetikleyici veya eylem tooyour mantıksal uygulama ekledikten sonra kimlik bilgileri istendiğinde, tooyour olay hub'ları ad bağlanabilir. Bağlantınızı bir ad verin, kopyalanır ve seçin hello bağlantı dizesi girin **oluşturma**.

    ![Olay hub'ları ad alanı için bağlantı dizesi girin](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    Bağlantınızı oluşturduktan sonra hello bağlantı adı hello olay hub'ları tetikleyici veya eylem görüntülenmesi gerekir. 
    Daha sonra devam edebilirsiniz ile Merhaba mantıksal uygulamanızı diğer adımları.

    ![Oluşturulan olay hub'ları ad alanı bağlantı](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a>Yeni olaylar olay Hub'ınızı aldığında, iş akışı Başlat

A [ *tetikleyici* ](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) mantıksal uygulamanızı bir iş akışı başlatır bir olaydır. Yeni olaylar tooyour olay hub'ı gönderildiğinde bir iş akışını başlatmak için bu olay algılar hello tetikleyici eklemek için aşağıdaki adımları izleyin.

1.  Merhaba, [Azure portal](https://portal.azure.com "Azure portal"), Git tooyour var olan mantıksal uygulama'ı ya da boş mantıksal uygulama oluşturma.

2.  Merhaba arama kutusuna hello mantığı Uygulama Tasarımcısı için `event hubs` filtreniz için. Bu tetikleyici seçin: **zaman olayların Event Hub'ında kullanılabilir**

    ![Olay Hub'ınızı yeni olayların ne zaman alan için tetikleyici seçin](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    Bir bağlantı tooyour olay hub'ları ad alanı zaten sahip değilseniz, istenir toocreate şimdi bu bağlantı. Bağlantınızı bir ad verin ve Event Hubs ad alanınız için hello bağlantı dizesi girin. 
    Gerekirse, bilgi [nasıl toofind bağlantı dizenizi](#permissions-connection-string).

    ![Olay hub'ları ad alanı için bağlantı dizesi girin](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    Merhaba bağlantı oluşturduktan sonra hello ayarlarını hello **bir olay gerçekleştiğinde bir olay Hub'ındaki kullanılabilir** tetikleyici görünür.

    ![Olay Hub'ınızı yeni olayların ne zaman alan için tetikleyici ayarları](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  Adını girin veya hello için hello toomonitor istediğiniz olay hub'ı seçin. Merhaba sıklığı ve toocheck hello olay hub'ı hangi sıklıkta güncelleştirileceğini aralığını seçin.

    > [!TIP]
    > toooptionally olayları okumak için bir tüketici grubu seçin, **Gelişmiş Seçenekleri Göster**. 

    ![Olay hub'ı veya tüketici grubu belirtin](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    Şimdi bir tetikleyici toostart bir iş akışı mantığı uygulamanız için ayarladığınız. 
    Olay hub'ı ayarladığınız hello zamanlamaya göre hello belirtilen mantıksal uygulamanızı denetler. 
    Uygulamanızı hello olay hub'ı yeni olaylar bulursa, hello tetikleyici diğer eylemler veya tetikleyicileri mantıksal uygulamanızı çalışır.

## <a name="send-events-tooyour-event-hub-from-your-logic-app"></a>Olayları tooyour olay hub'ı mantıksal uygulamanızı Gönder

[*Eylem*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts), mantıksal uygulama iş akışınız tarafından gerçekleştirilen bir görevdir. Bir tetikleyici tooyour mantıksal uygulama ekledikten sonra Bu tetikleyici tarafından oluşturulan verilerle bir eylem tooperform işlemleri ekleyebilirsiniz. toosend mantığı uygulamanızdan olay tooyour olay hub'ı şu adımları izleyin.

1.  Mantıksal Uygulama Tasarımcısı'nda mantığı uygulama tetikleyici altında seçin **yeni adım** > **Eylem Ekle**.

    !["Yeni adım" sonra "Eylem Ekle" seçin](./media/connectors-create-api-azure-event-hubs/add-action.png)

    Şimdi Bul ve bir eylem tooperform seçin. 
    Bu örnek için herhangi bir eylem seçebilmenize rağmen hello olay hub'ları eylem toosend olayları istiyoruz.

2.  Merhaba arama kutusuna `event hubs` filtreniz için.
Bu eylem seçin: **gönderme olayı**

    !["Event Hubs - gönderme olayı" seçin eylemi](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  Merhaba Event Hub'ın toosend hello olay istediğiniz hello adı gibi hello olayı için gerekli hello ayrıntılarını girin. Bu olay için içeriği gibi hello olay hakkında isteğe bağlı diğer ayrıntılarını girin.

    > [!TIP]
    > toooptionally belirtin hello olay hub'ı bölüm nerede toosend hello olayı seçin **Gelişmiş Seçenekleri Göster**. 

    ![Olay hub'ı adı ve isteğe bağlı olay ayrıntılarını girin](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  Yaptığınız değişiklikleri kaydedin.

    ![Mantıksal uygulamanızı kaydetme](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    Bir eylem toosend olaylarını mantıksal uygulamanızı şimdi ayarladınız. 

## <a name="connector-specific-details"></a>Bağlayıcı özgü ayrıntıları

Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/eventhubs/). 

## <a name="get-help"></a>Yardım alın

tooask sorular, soruları ve diğer Azure mantıksal uygulamaları kullanıcıların gittiğini, bkz: ziyaret hello [Azure Logic Apps Forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp Logic Apps ve bağlayıcılar geliştirmek, oy veya hello fikir gönderme [Logic Apps kullanıcı geri bildirim sitesi](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Sonraki adımlar

*  [Azure mantıksal uygulamaları için diğer bağlayıcıları Bul](./apis-list.md)