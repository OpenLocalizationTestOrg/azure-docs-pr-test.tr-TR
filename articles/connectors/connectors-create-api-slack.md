---
title: "Azure mantıksal uygulamalarınızı aaaUse hello kayma bağlayıcı | Microsoft Docs"
description: "Mantıksal uygulamalarınızı tooSlack Bağlan"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 234cad64-b13d-4494-ae78-18b17119ba24
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 6599d7b69d2147425c9fab978c5d0f93e5605f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-slack-connector"></a>Merhaba Slack Bağlayıcısı ile çalışmaya başlama
Slack, ekibinizin tüm yazışmalarını anında aranabilecek ve gittiğiniz her yerden ulaşılabilecek bir yerde toplayan bir ekip iletişim aracıdır. 

Bir mantıksal uygulama artık oluşturarak başlama; bkz: [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="create-a-connection-tooslack"></a>Bir bağlantı tooSlack oluşturma
toouse hello Slack bağlayıcı, önce oluşturduğunuz bir **bağlantı** sonra hello Ayrıntılar için bu özellikleri sağlar: 

| Özellik | Gerekli | Açıklama |
| --- | --- | --- |
| Belirteç |Evet |Slack kimlik bilgilerini sağlayın |

Bu adımları toosign kayma ve hello kayma tam hello yapılandırmasını izleyin **bağlantı** mantığı uygulamanıza:

1. Seçin **yineleme**
2. Seçin bir **sıklığı** ve girin bir **aralığı**
3. Seçin **Eylem Ekle**  
   ![Kayma yapılandırın][1]  
4. Kayma hello arama kutusuna girin ve hello adında boşluk içeren tüm girişleri için hello arama tooreturn bekleyin
5. Seçin **Slack'e - posta iletisi**
6. Seçin **tooSlack içinde oturum**:  
   ![Kayma yapılandırın][2]
7. Slack kimlik bilgileri toosign tooauthorize hello uygulamada sağlayın    
   ![Kayma yapılandırın][3]  
8. Yeniden yönlendirilen tooyour kuruluşunuzun oturum açma sayfasında olması. **Yetki** Slack toointeract mantıksal uygulamanızı ile:      
   ![Kayma yapılandırın][5] 
9. Hello yetkilendirme tamamlandıktan sonra yeniden yönlendirilen tooyour mantığı uygulama toocomplete olması, hello yapılandırarak **Slack - tüm iletileri Al** bölüm. Diğer tetikleyiciler ve gereken eylemleri ekleyin.  
   ![Kayma yapılandırın][6]
10. Seçerek çalışmanızı kaydedin **kaydetmek** hello menü çubuğunda yukarıdaki.

## <a name="connector-specific-details"></a>Bağlayıcı özgü ayrıntıları

Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/slack/).

## <a name="more-connectors"></a>Daha fazla bağlayıcılar
Toohello dönün [API'leri listesi](apis-list.md).

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
