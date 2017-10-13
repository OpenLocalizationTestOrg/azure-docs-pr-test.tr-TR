---
title: "Tümleştirme hesap yapı meta verileri - Azure mantıksal uygulamaları yönetme | Microsoft Docs"
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
ms.openlocfilehash: 28bb8296ddd820ec5aa9793dc0928b4b1e67bf6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a>Tümleştirme hesapları logic apps için yapı meta verilerini yönetme

Bu meta veri çalışma zamanı sırasında mantıksal uygulamanızı almak ve tümleştirme hesaplarında yapıları için özel meta verileri tanımlayın. Örneğin, iş ortakları, anlaşmalar, şemalar ve haritalar gibi yapıları için meta veri belirtebilirsiniz - tüm anahtar-değer çiftleri kullanarak meta verileri depolama. Şu anda kullanıcı Arabirimi aracılığıyla meta veri yapıları oluşturulamıyor, ancak meta verileri oluşturmak için REST API'ler kullanabilirsiniz. Oluşturduğunuzda ya da bir iş ortağı, anlaşma ya da şema Azure portalında seçin meta veri eklemek için **JSON olarak Düzenle**. Logic apps içinde yapı meta verilerini almak için tümleştirme hesap yapı arama özelliğini kullanabilirsiniz.

## <a name="add-metadata-to-artifacts-in-integration-accounts"></a>Meta veri yapıları tümleştirme hesapları ekleyin

1. Oluşturma bir [tümleştirme hesabını](logic-apps-enterprise-integration-create-integration-account.md).

2. Örneğin bir yapı tümleştirme hesabınıza ekleyin, bir [iş ortağı](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [sözleşmesi](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), veya [şema](logic-apps-enterprise-integration-schemas.md).

3.  Yapıyı seçin, **JSON olarak Düzenle**ve meta veri ayrıntılarını girin.

    ![Meta veri girin](media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a>Logic apps için yapılardan meta veri alma

1. Oluşturma bir [mantıksal uygulama](logic-apps-create-a-logic-app.md).

2. Oluşturma bir [mantıksal uygulamanızı bir bağlantıdan tümleştirme hesabınıza](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app). 

3. Mantıksal Uygulama Tasarımcısı'nda bir tetikleyici gibi ekleme *isteği* veya *HTTP* mantığı uygulamanıza.

4.  Seçin **sonraki adım** > **Eylem Ekle**. Arama *tümleştirme* bulun ve ardından **tümleştirme hesabı - tümleştirme hesap yapı arama**.

    ![Tümleştirme hesap yapı arama seçin](media/logic-apps-enterprise-integration-metadata/image2.png)

5. Seçin **yapay nesne türü**ve sağlamak **yapı adı**.

    ![Yapay nesne türü seçin ve yapı adı belirtin](media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a>Örnek: Alma ortak meta veriler

İş ortağı meta veri olan bu `routingUrl` ayrıntıları:

![İş ortağı "routingURL" meta veri bulma](media/logic-apps-enterprise-integration-metadata/image6.png)

1. Mantıksal uygulamanızı, tetikleyici eklemek bir **tümleştirme hesabı - tümleştirme hesap yapı arama** için iş ortağınızla için eylem ve bir **HTTP**.

    ![Tetikleyici, yapı arama ve "HTTP" mantıksal uygulamanızı ekleme](media/logic-apps-enterprise-integration-metadata/image4.png)

2. URI'yi almak için mantığı uygulamanız için kod görünümüne gidin. Mantıksal uygulama tanımını bu örnekteki gibi görünmelidir:

    ![Arama arama](media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a>Sonraki adımlar
* [Anlaşmaları hakkında daha fazla bilgi](logic-apps-enterprise-integration-agreements.md "Kurumsal tümleştirme anlaşmaları hakkında bilgi edinin")  
