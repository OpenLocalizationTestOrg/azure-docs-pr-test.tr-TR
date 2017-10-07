---
title: "aaaUse hello Logic Apps içinde SharePoint sunucusu Bağlayıcısı | Microsoft Docs"
description: "Merhaba hello SharePoint sunucusu Bağlayıcısı Logic apps kullanmaya başlama"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 0238a060-d592-4719-b7a2-26064c437a1a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 3b814f42611e4971ff5c94ae3b021829217911dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sharepoint-connector"></a>Merhaba SharePoint Bağlayıcısı ile çalışmaya başlama
Merhaba SharePoint bağlayıcı SharePoint'te bir şekilde toowork listeleriyle sağlar.

Bir mantıksal uygulama oluşturarak başlama; bkz: [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="create-a-connection-toosharepoint"></a>Bir bağlantı tooSharePoint oluşturma
toouse Merhaba SharePoint bağlayıcı, önce oluşturduğunuz bir **bağlantı** sonra hello Ayrıntılar için bu özellikleri sağlar: 

| Özellik | Gerekli | Açıklama |
| --- | --- | --- |
| Belirteç |Evet |SharePoint kimlik bilgilerini sağlayın |

tooconnect çok**SharePoint**, kimlik (kullanıcı adı ve parola, akıllı kart kimlik bilgileri, vb.) tooSharePoint girin. Kimlik doğruladınız sonra mantıksal uygulamanızı toouse hello SharePoint bağlayıcı devam edebilirsiniz. 

Merhaba Tasarımcısı mantıksal uygulamanızı karşın, bu adımları toosign SharePoint toocreate hello bağlantısına takip **bağlantı** mantıksal uygulamanızı kullanmak için:

1. SharePoint hello arama kutusuna girin ve SharePoint ile tüm girişleri hello adında hello arama tooreturn için bekleyin:   
   ![SharePoint'i yapılandırma][1]  
2. Seçin **bir dosya oluşturulduğunda SharePoint -**   
3. Seçin **tooSharePoint içinde oturum**:   
   ![SharePoint'i yapılandırma][2]    
4. SharePoint ile SharePoint kimlik bilgileri toosign tooauthenticate içinde sağlayın   
   ![SharePoint'i yapılandırma][3]     
5. Merhaba kimlik doğrulama tamamlandıktan sonra yeniden yönlendirilen tooyour mantığı uygulama toocomplete olacaktır, SharePoint yapılandırarak **bir dosya oluşturulduğunda** iletişim.          
   ![SharePoint'i yapılandırma][4]  
6. Daha sonra diğer tetikleyiciler ve Eylemler mantıksal uygulamanızı toocomplete gerektiğini de ekleyebilirsiniz.   
7. Seçerek çalışmanızı kaydedin **kaydetmek** hello menü çubuğunda yukarıdaki.  

## <a name="connector-specific-details"></a>Bağlayıcı özgü ayrıntıları

Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/sharepoint/).

## <a name="more-connectors"></a>Daha fazla bağlayıcılar
Toohello dönün [API'leri listesi](apis-list.md).

[1]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png
