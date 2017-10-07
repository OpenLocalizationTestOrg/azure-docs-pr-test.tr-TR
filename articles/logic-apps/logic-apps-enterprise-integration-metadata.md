---
title: "aaaManage tümleştirme Azure Logic Apps yapı meta verileri - hesap | Microsoft Docs"
description: "Ekleme veya yapı meta veri tümleştirme hesaplarından Azure Logic Apps için alma"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 11/21/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8de71bffa9f9975d5409716b2208fa6c3a9545d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a>Tümleştirme hesapları logic apps için yapı meta verilerini yönetme

Bu meta veri çalışma zamanı sırasında mantıksal uygulamanızı almak ve tümleştirme hesaplarında yapıları için özel meta verileri tanımlayın. Örneğin, iş ortakları, anlaşmalar, şemalar ve haritalar gibi yapıları için meta veri belirtebilirsiniz - tüm anahtar-değer çiftleri kullanarak meta verileri depolama. Şu anda kullanıcı Arabirimi aracılığıyla meta veri yapıları oluşturulamıyor, ancak REST API'leri toocreate meta verileri kullanabilirsiniz. oluşturduğunuzda ya da bir iş ortağı, anlaşma ya da şema hello Azure portal seçin tooadd meta veri seçin **JSON olarak Düzenle**. tooretrieve yapı logic apps meta verileri, hello tümleştirme hesap yapı arama özelliğini kullanabilirsiniz.

## <a name="add-metadata-tooartifacts-in-integration-accounts"></a>Meta veri tooartifacts tümleştirme hesapları ekleme

1. Oluşturma bir [tümleştirme hesabını](logic-apps-enterprise-integration-create-integration-account.md).

2. Örneğin bir yapı tooyour tümleştirme hesap ekleyin, bir [iş ortağı](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [sözleşmesi](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), veya [şema](logic-apps-enterprise-integration-schemas.md).

3.  Merhaba yapı seçin, **JSON olarak Düzenle**ve meta veri ayrıntılarını girin.

    ![Meta veri girin](media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a>Logic apps için yapılardan meta veri alma

1. Oluşturma bir [mantıksal uygulama](logic-apps-create-a-logic-app.md).

2. Oluşturma bir [mantığı uygulama tooyour tümleştirme hesabınızı bağlantısından](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app). 

3. Mantıksal Uygulama Tasarımcısı'nda bir tetikleyici gibi ekleme *isteği* veya *HTTP* tooyour mantıksal uygulama.

4.  Seçin **sonraki adım** > **Eylem Ekle**. Arama *tümleştirme* bulun ve ardından **tümleştirme hesabı - tümleştirme hesap yapı arama**.

    ![Tümleştirme hesap yapı arama seçin](media/logic-apps-enterprise-integration-metadata/image2.png)

5. Select hello **yapay nesne türü**ve hello sağlamak **yapı adı**.

    ![Yapay nesne türü seçin ve yapı adı belirtin](media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a>Örnek: Alma ortak meta veriler

İş ortağı meta veri olan bu `routingUrl` ayrıntıları:

![İş ortağı "routingURL" meta veri bulma](media/logic-apps-enterprise-integration-metadata/image6.png)

1. Mantıksal uygulamanızı, tetikleyici eklemek bir **tümleştirme hesabı - tümleştirme hesap yapı arama** için iş ortağınızla için eylem ve bir **HTTP**.

    ![Tetikleyici, yapı arama ve "HTTP" tooyour mantıksal uygulama Ekle](media/logic-apps-enterprise-integration-metadata/image4.png)

2. tooretrieve hello URI, mantıksal uygulamanız için Görünüm tooCode gidin. Mantıksal uygulama tanımını bu örnekteki gibi görünmelidir:

    ![Arama arama](media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a>Sonraki adımlar
* [Anlaşmaları hakkında daha fazla bilgi](logic-apps-enterprise-integration-agreements.md "Kurumsal tümleştirme anlaşmaları hakkında bilgi edinin")  
