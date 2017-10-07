---
title: aaaValidate XML - Azure Logic Apps | Microsoft Docs
description: "Enterprise Integration Pack Merhaba kullanarak Azure Logic Apps ile B2B senaryoları için şemalarda XML doğrulama"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: d700588f-2d8a-4c92-93eb-e1e6e250e760
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 81f662d0ddf908657b54de8af0a75fff55782ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-for-enterprise-integration"></a>XML için Kurumsal tümleştirme doğrula

Genellikle B2B senaryolarda anlaşmanın hello ortakları veri işleme başlamadan önce bunlar exchange Merhaba iletileri geçerli emin olmanız gerekir. Önceden tanımlanmış bir şemayla belgeleri hello Enterprise Integration Pack hello kullan hello XML doğrulama bağlayıcı kullanarak doğrulayabilirsiniz.

## <a name="validate-a-document-with-hello-xml-validation-connector"></a>Bir belgeyi hello XML doğrulama Bağlayıcısı ile doğrula

1. Bir mantıksal uygulama oluşturma ve [bağlantı hello uygulama toohello tümleştirme hesabını](../logic-apps/logic-apps-enterprise-integration-accounts.md "toolink bir tümleştirme hesap tooa mantıksal uygulama öğrenin") XML verileri doğrulamak için toouse istediğiniz hello şeması vardır.

2. Ekleme bir **isteği - olduğunda bir HTTP isteği alındığında** tetikleyici tooyour mantıksal uygulama.

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. tooadd hello **XML doğrulama** eylemi seçin **Eylem Ekle**.

4. Tüm Eylemler toohello istediğiniz bir hello toofilter girin *xml* hello arama kutusuna. Seçin **XML doğrulama**.

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. toospecify hello toovalidate, istediğiniz XML içeriği seçin **içerik**.

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. Merhaba gövde etiket hello toovalidate istediğiniz içeriği seçin.

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. Merhaba önceki doğrulamak için toouse istediğiniz toospecify hello şema *içerik* giriş, seçin **şema adı**.

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. Çalışmanızı kaydedin  

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

Şimdi, doğrulama Bağlayıcısı'nı ayarlama ile yapılır. Gerçek dünya uygulamada toostore doğrulanmış hello veri SalesForce gibi bir satır iş kolu (LOB) uygulamasında isteyebilirsiniz. toosend doğrulanmış çıktı tooSalesforce Merhaba, bir eylem ekleyin.

tootest doğrulama eyleminizi bir istek toohello HTTP uç noktası olun.

## <a name="next-steps"></a>Sonraki adımlar
[Merhaba Enterprise Integration Pack hakkında daha fazla bilgi](../logic-apps/logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin")   

