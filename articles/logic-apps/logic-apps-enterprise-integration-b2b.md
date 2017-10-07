---
title: aaaCreate B2B solutions - Azure Logic Apps | Microsoft Docs
description: "Merhaba Enterprise Integration Pack Merhaba B2B özelliklerini kullanarak logic apps içinde veri alma"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 20fc3722-6f8b-402f-b391-b84e9df6fcff
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8f01318a0415d81c37b216f9b991c060edec2053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="receive-data-in-logic-apps-with-hello-b2b-features-in-hello-enterprise-integration-pack"></a>Logic apps hello Enterprise Integration Pack Merhaba B2B özellikleri ile veri alma

İş ortakları ve anlaşmaları olan bir tümleştirme hesap oluşturduktan sonra hazır toocreate iş toobusiness (B2B) iş akışı mantığı uygulamanızla hello için olduğunuz [Kurumsal tümleştirme paketi](logic-apps-enterprise-integration-overview.md).

## <a name="prerequisites"></a>Ön koşullar

toouse hello AS2 ve X12 Eylemler, bir kurumsal tümleştirme hesabınızın olması gerekir. Bilgi [nasıl toocreate bir kurumsal tümleştirme hesap](../logic-apps/logic-apps-enterprise-integration-accounts.md).

## <a name="create-a-logic-app-with-b2b-connectors"></a>İle B2B bağlayıcılar mantıksal uygulama oluşturma

Merhaba AS2 ve X12 kullanan bu adımları toocreate bir B2B mantıksal uygulama izleyin ticari ortak Eylemler tooreceive verileri:

1. Ardından bir mantıksal uygulama oluşturma [uygulama tooyour tümleştirme hesabınızı bağlama](../logic-apps/logic-apps-enterprise-integration-accounts.md).

2. Ekleme bir **isteği - olduğunda bir HTTP isteği alındığında** tetikleyici tooyour mantıksal uygulama.

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. tooadd hello **kod çözme AS2** eylem, select **Eylem Ekle**.

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. toofilter tüm eylemler toohello istediğiniz birini girin hello word **as2** hello arama kutusuna.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. Select hello **AS2 - kod çözme AS2 ileti** eylem.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. Merhaba eklemek **gövde** giriş olarak toouse istiyor. Bu örnekte, hello Tetikleyicileri mantıksal uygulama hello hello HTTP istek gövdesi seçin. Merhaba hello üstbilgilerinde girdi bir ifade girin veya **ÜSTBİLGİLERİ** alan:

    @triggerOutputs() ['üst bilgileri']

7. Gerekli hello eklemek **üstbilgileri** hello HTTP istek üst bilgilerinde bulabilirsiniz AS2 için. Bu örnekte, bu tetikleyici hello mantıksal uygulama hello üstbilgilerini hello HTTP isteğini seçin.

8. Şimdi hello kod çözme X12 ileti eylemi ekleyin. Seçin **Eylem Ekle**.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. toofilter tüm eylemler toohello istediğiniz birini girin hello word **x12** hello arama kutusuna.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. Select hello **X12-X12 kod çözme ileti** eylem.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. Şimdi hello giriş toothis eylem belirtmeniz gerekir. Bu giriş hello önceki AS2 eylemin hello çıktısını olabilir.

    Merhaba gerçek ileti içerik bir JSON nesnesinde ve base64 ile kodlanmış, olduğundan, bir ifade hello giriş olarak belirtmeniz gerekir. 
    Merhaba ifadesinde aşağıdaki hello girin **X12 DÜZ dosya iletisi tooDECODE** giriş alanı:
    
    @base64ToString(body('Decode_AS2_message')? ['AS2Message']? ['Content'])

    Şimdi toodecode hello X12 veri öğeleri bir JSON nesnesinde çıkış ve iş ortağı ticaret hello alınan adımlar ekleyin. 
    Veri hello toonotify hello iş ortağı alındı, hello bir HTTP yanıt uygulamada AS2 ileti değerlendirme bildirim (MDN) içeren bir yanıtı geri gönderebilirsiniz.

12. tooadd hello **yanıt** eylemi seçin **Eylem Ekle**.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. toofilter tüm eylemler toohello istediğiniz birini girin hello word **yanıt** hello arama kutusuna.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. Select hello **yanıt** eylem.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. tooaccess hello MDN hello hello çıktısından **kod çözme X12 ileti** eylem, kümesi hello yanıt **gövde** Bu ifade ile alan:

    @base64ToString(body('Decode_AS2_message')? ['OutgoingMdn']? ['Content'])

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. Çalışmanızı kaydedin.

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

Şimdi yapılır B2B mantıksal uygulamanızı ayarlama. Gerçek dünya uygulamada toostore hello kodunu çözdü X12 isteyebilirsiniz satır iş kolu (LOB) uygulaması veya veri deposuna verileri. tooconnect kendi iş KOLU uygulamalarınızı ve mantıksal uygulamanızı bu API'leri kullanın, daha fazla eylemler ekleyebilir veya özel API'ları yazma.

## <a name="features-and-use-cases"></a>Özellikleri ve kullanım örnekleri

* Merhaba AS2 ve X12 Eylemler kodlanacağını ve logic apps içinde endüstri standardı protokoller kullanarak ticaret ortakları arasında veri değişimi bırakın.
* Ticari ortaklar tooexchange veriler ile veya olmadan birbirine AS2 ve X12 kullanabilirsiniz.
* Hello B2B Eylemler iş ortakları ve anlaşmaları tümleştirme hesabınızı kolayca oluşturun ve bir mantıksal uygulama kullanmasına yardımcı olur.
* Mantıksal uygulamanızı diğer eylemler ile genişlettiğinizde, gönderebilir ve diğer uygulamalarla SalesForce gibi hizmetler arasında veri alırsınız.

## <a name="learn-more"></a>Daha fazla bilgi edinin
[Merhaba Enterprise Integration Pack hakkında daha fazla bilgi edinin](logic-apps-enterprise-integration-overview.md)
