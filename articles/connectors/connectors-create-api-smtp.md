---
title: "Azure mantıksal uygulamaları aaaSMTP Bağlayıcısı | Microsoft Docs"
description: "Logic apps ile Azure uygulama hizmeti oluşturun. TooSMTP toosend e-posta bağlayın."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d4141c08-88d7-4e59-a757-c06d0dc74300
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 36bb836851014d24f2e069fda8376ad7a08c943b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-smtp-connector"></a>Merhaba SMTP Bağlayıcısı ile çalışmaya başlama
TooSMTP toosend e-posta bağlayın.

toouse [tüm bağlayıcıların](apis-list.md), toocreate bir mantıksal uygulama ilk gerekir. Tarafından başlayabiliriz [şimdi mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toosmtp"></a>TooSMTP Bağlan
Mantıksal uygulamanızı herhangi bir hizmet erişebilmeniz için önce toocreate ilk gerekiyor bir *bağlantı* toohello hizmet. A [bağlantı](connectors-overview.md) bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar. Örneğin, tooconnect tooSMTP önce bir SMTP gerekir *bağlantı*. toocreate bir bağlantı için connect tooaccess hello hizmeti normalde kullandığınız hello kimlik bilgilerini girin. Bu nedenle, hello SMTP örnekte hello kimlik bilgilerini tooyour bağlantı adı, SMTP sunucu adresleri ve kullanıcı oturum açma bilgileri toocreate hello bağlantı tooSMTP girin.  

### <a name="create-a-connection-toosmtp"></a>Bir bağlantı tooSMTP oluşturma
> [!INCLUDE [Steps toocreate a connection tooSMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a>Bir SMTP tetikleyicisi kullanın
Bir tetikleyici bir mantıksal uygulama tanımlı kullanılan toostart hello iş akışı olabilecek bir olaydır. [Tetikleyiciler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

SMTP kendi, tetikleyici olmadığından bu örnekte, hello kullanacağız **bir nesne oluşturulduğunda Salesforce -** tetikleyici. Salesforce'ta yeni bir nesne oluşturulduğunda, bu tetikleyici etkinleştirir. Sağlayacak şekilde her bir yeni sağlama Salesforce içinde oluşturulur Bizim örneğimizde, bunu yaparız bir *e-posta Gönder* eylem oluşur oluşturulmakta hello yeni müşteri adayına ilişkin bir bildirim ile Merhaba SMTP bağlayıcısı aracılığıyla.

1. Girin *salesforce* hello arama kutusuna hello logic apps tasarımcısında hello seçip **bir nesne oluşturulduğunda Salesforce -** tetikleyici.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. Merhaba **bir nesne oluşturulduğunda** denetim görüntülenir.
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. Select hello **nesne türü** seçip *neden* nesneleri hello listesinden. Bu adımda, her bir yeni sağlama Salesforce'ta oluşturulduğunda, mantıksal uygulamanızı uyarır tetikleyici oluşturmakta olduğunuz belirten.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. Merhaba tetikleyici oluşturuldu.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a>SMTP eylemi kullanın
Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir. [Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

Merhaba tetikleyici eklendi, yeni sağlama Salesforce'ta oluşturulduğunda gerçekleşir bu adımları tooadd SMTP eylemi izleyin.

1. Seçin **+ yeni adım** tooadd hello eylem istediğinizi tootake yeni bir sağlama oluşturulduğunda.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. Seçin **Eylem Ekle**. Bu açılır hello arama kutusu için herhangi bir işlem, arayabileceğiniz tootake ister.  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. Girin *smtp* Eylemler ilgili tooSMTP toosearch.  
4. Seçin **SMTP - e-posta Gönder** hello yeni sağlama oluşturulduğunda eylem tootake hello gibi. Merhaba eylem denetim bloğu açılır. Daha önce yapmadıysanız seçerseniz, smtp bağlantı tooestablish hello Tasarımcı bloğunda gerekir.  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. İstenen e-posta bilgilerinizi hello giriş **SMTP - e-posta Gönder** bloğu.  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. İş akışınızı sipariş tooactivate kaydedin.  

## <a name="connector-specific-details"></a>Bağlayıcı özgü ayrıntıları

Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/smtpconnector/).

## <a name="more-connectors"></a>Daha fazla bağlayıcılar
Toohello dönün [API'leri listesi](apis-list.md).
