---
title: "Mantıksal uygulamalarınızı aaaAdd hello Office 365 Outlook connector | Microsoft Docs"
description: "Office 365 ile Office 365 Bağlayıcısı tooenable etkileşimi ile mantıksal uygulamalar oluşturun. Örneğin: oluşturma, düzenleme ve kişiler ve takvim öğeleri güncelleştirme."
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2f6cc2c-bba2-493a-b0ba-841785462a80
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 86a573c9c54701de3d3f0500d19eaf545e0710ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-office-365-outlook-connector"></a>Merhaba Office 365 Outlook Bağlayıcısı ile çalışmaya başlama
Merhaba Office 365 Outlook Bağlayıcısı, Office 365'te Outlook ile etkileşim sağlar. Bu bağlayıcı toocreate, düzenleme, güncelleştirme kişiler ve takvim öğeleri kullanın ve ayrıca almak, Gönder ve tooemail yanıt.

Office 365 Outlook ile:

* Office 365 içinde Hello e-posta ve Takvim özellikleri kullanarak, iş akışı oluşturma. 
* Kullanım toostart olduğunda yeni e-posta, Takvim öğesi güncelleştirildiğinde, iş akışınızı ve daha fazlasını tetikler.
* Eylemler toosend bir e-posta kullanın, yeni bir takvim olayı ve daha fazlasını oluşturun. Salesforce (tetikleyici) yeni bir nesne olduğunda, örneğin, bir e-posta Gönder tooyour Office 365 Outlook (bir eylem). 

Bu konuda nasıl toouse hello bir mantıksal uygulama Office 365 Outlook connector gösterir ve ayrıca listeleri tetikleyiciler ve Eylemler hello.

> [!NOTE]
> Merhaba makalenin bu sürümü tooLogic uygulamaları genel kullanılabilirlik (GA) uygulanır.
> 
> 

Logic Apps hakkında daha fazla toolearn bkz [logic apps nedir](../logic-apps/logic-apps-what-are-logic-apps.md) ve [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toooffice-365"></a>TooOffice 365 Bağlan
Mantıksal uygulamanızı herhangi bir hizmete erişebilmesi için önce oluşturduğunuz bir *bağlantı* toohello hizmet. Bağlantı bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar. Örneğin, tooconnect tooOffice 365 Outlook, ilk ihtiyacınız bir Office 365 *bağlantı*. toocreate bir bağlantı için tooconnect istediğiniz tooaccess hello hizmet normalde kullandığınız hello kimlik bilgilerini girin. Bu nedenle Office 365 Outlook ile Merhaba kimlik bilgilerini tooyour Office 365 hesabı toocreate hello bağlantısı girin.

## <a name="create-hello-connection"></a>Merhaba bağlantısı oluşturma
> [!INCLUDE [Steps toocreate a connection tooOffice 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a>Bir tetikleyici kullanın
Bir tetikleyici bir mantıksal uygulama tanımlı kullanılan toostart hello iş akışı olabilecek bir olaydır. Tetikleyiciler "Merhaba hizmet bir aralığı ve istediğiniz sıklığı yoklama". [Tetikleyiciler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Merhaba mantıksal uygulama içinde "office 365" tooget hello Tetikleyicileri listesini yazın:  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. Seçin **Office 365 yaklaşan bir olay yakında başlatırken Outlook -**. Bir bağlantı zaten varsa, bir takvim hello aşağı açılan listeden seçin.
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    İçinde istendiğinde toosign varsa, hello oturum ayrıntıları toocreate hello bağlantısında girin. [Merhaba bağlantı oluşturmak](connectors-create-api-office365-outlook.md#create-the-connection) bu konudaki hello adımlar listelenmektedir. 
   
   > [!NOTE]
   > Bu örnekte, bir takvim olay güncelleştirildiğinde hello mantıksal uygulama çalışır. Bu tetikleyici toosee hello sonuçlarını bir kısa mesaj gönderir başka bir eylem ekleyin. Örneğin, hello Twilio ekleyin *ileti gönder* hello olduğunda Takvim olay metinleri 15 dakika içinde başlangıç eylem. 
   > 
   > 
3. Select hello **Düzenle** düğmesine tıklayın ve ayarlama hello **sıklığı** ve **aralığı** değerleri. Örneğin, 15 dakikada bir hello tetikleyici toopoll istiyorsanız, ardından hello ayarlayın **sıklığı** çok**Minute**ve kümesi hello **aralığı** çok**15**. 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. **Kaydet** değişikliklerinizi (sol üst köşesindeki hello araç). Mantıksal uygulamanızı kaydedilir ve otomatik olarak etkinleştirilir.

## <a name="use-an-action"></a>Bir eylem kullanın
Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir. [Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Merhaba artı işaretini seçin. Birkaç seçeneğiniz bkz: **Eylem Ekle**, **bir koşul eklemek**, veya hello **daha fazla** seçenekleri.
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. Seçin **Eylem Ekle**.
3. Merhaba metin kutusuna "office 365" tooget tüm hello kullanılabilir eylemlerin bir listesini yazın.
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. Bizim örneğimizde seçin **Office 365 Outlook - kişi oluşturma**. Bir bağlantı zaten varsa, hello seçin **klasörü kimliği**, **verilen ad**ve diğer özellikleri:  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    Merhaba bağlantı bilgilerini istenirse, hello ayrıntıları toocreate hello bağlantısı girin. [Merhaba bağlantı oluşturmak](connectors-create-api-office365-outlook.md#create-the-connection) bu konuda bu özellikleri açıklar. 
   
   > [!NOTE]
   > Bu örnekte, Office 365 Outlook içinde yeni bir kişi oluşturun. Başka bir tetikleyici toocreate hello kişi çıktısını kullanabilirsiniz. Örneğin, SalesForce hello ekleyin *bir nesne oluşturulduğunda* tetikleyici. Merhaba Office 365 Outlook eklemek *kişi oluşturma* hello SalesForce kullandığı eylem toocreate hello yeni yeni kişi Office 365'te alanları. 
   > 
   > 
5. **Kaydet** değişikliklerinizi (sol üst köşesindeki hello araç). Mantıksal uygulamanızı kaydedilir ve otomatik olarak etkinleştirilir.

## <a name="connector-specific-details"></a>Bağlayıcı özgü ayrıntıları

Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/office365connector/). 

## <a name="next-steps"></a>Sonraki Adımlar
[Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md). Araştır Logic Apps içinde kullanılabilir diğer bağlayıcıları hello bizim [API'leri listesi](apis-list.md).

