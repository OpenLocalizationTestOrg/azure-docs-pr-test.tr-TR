---
title: aaaEncode AS2 iletileri - Azure Logic Apps | Microsoft Docs
description: "Nasıl toouse hello AS2 Kodlayıcısı hello Kurumsal tümleştirme paketi ile Azure mantıksal uygulamaları için"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 332fb9e3-576c-4683-bd10-d177a0ebe9a3
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 2b372c416512ffa9ea5dc50ce0f767bfd8aefbc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>AS2 iletileri için Azure Logic Apps Enterprise Integration Pack Merhaba ile kodlayın.

tooestablish güvenlik ve güvenilirlik iletileri aktarımı sırasında hello kodlamak AS2 ileti bağlayıcı kullanın. Bu bağlayıcı, dijital imza, şifreleme ve onayları aracılığıyla ileti Disposition bildirimler (hangi toosupport inkar için de müşteri adayları MDN), sağlar.

## <a name="before-you-start"></a>Başlamadan önce

Gereksinim duyduğunuz hello öğeleri şöyledir:

* Bir Azure hesabı; oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free)
* Bir [tümleştirme hesabını](logic-apps-enterprise-integration-create-integration-account.md) , daha önce tanımlanan ve Azure aboneliğinizle ilişkili. Bir tümleştirme hesap toouse hello kodlamak AS2 ileti Bağlayıcısı olması gerekir.
* En az iki [ortakları](logic-apps-enterprise-integration-partners.md) tümleştirme hesabınızda zaten tanımlanmış
* Bir [AS2 sözleşmesi](logic-apps-enterprise-integration-as2.md) tümleştirme hesabınızda tanımlanan zaten

## <a name="encode-as2-messages"></a>AS2 iletileri kodlama

1. [Mantıksal uygulama oluşturma](logic-apps-create-a-logic-app.md).

2. bir istek tetikleyici gibi mantıksal uygulamanızı başlatmak için bir tetikleyici eklemelisiniz hello kodlamak AS2 ileti bağlayıcı tetikleyiciler, sahip değil. Hello mantığı Uygulama Tasarımcısı, tetikleyici ekleyin ve sonra bir eylem tooyour mantıksal uygulama ekleyin.

3.  Merhaba arama kutusuna "AS2" filtreniz için girin. Seçin **AS2 - kodlamak AS2 ileti**.
   
    !["AS2" için arama](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. Tooyour tümleştirme hesabını daha önce herhangi bir bağlantısı oluşturmadıysanız, istenir toocreate şimdi bu bağlantı. Bağlantınızı adlandırın ve hello tümleştirme hesabı tooconnect istediğinizi seçin. 
   
    ![bağlantı toointegration hesabı oluşturma](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    Bir yıldız işareti özelliklerle gereklidir.

    | Özellik | Ayrıntılar |
    | --- | --- |
    | Bağlantı adı * |Bağlantınız için herhangi bir ad girin. |
    | Tümleştirme hesabını * |Tümleştirme hesabınız için bir ad girin. Tümleştirme hesabı ve mantıksal uygulamanızı hello olduğundan emin olun aynı Azure konumu. |

5.  İşiniz bittiğinde, bağlantı ayrıntılarınızı benzer toothis örnek görünmelidir. bağlantı oluşturma toofinish seçin **oluşturma**.
   
    ![Tümleştirme bağlantı ayrıntıları](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. Bu örnekte gösterildiği gibi bağlantınızı oluşturulduktan sonra ayrıntılarını sağlamak **AS2-gelen**, **AS2 tooidentifiers** sözleşmenizde, yapılandırılan ve **gövde**, olduğu Merhaba ileti yükü.
   
    ![zorunlu alanlar sağlayın](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a>AS2 Kodlayıcı ayrıntıları

Merhaba kodlamak AS2 Bağlayıcısı, şu görevleri gerçekleştirir: 

* AS2/HTTP üstbilgileri uygular
* İletiler (yapılandırılmışsa) giden işaretleri
* Giden iletileri şifreler (yapılandırıldıysa)
* Merhaba iletisi (yapılandırılmışsa) sıkıştırır

## <a name="try-this-sample"></a>Bu örnek deneyin

bir tam olarak işlevsel mantığı uygulamasını ve örnek AS2 senaryo dağıtma tootry bkz hello [AS2 mantıksal uygulama şablonu ve senaryo](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).

## <a name="view-hello-swagger"></a>Görünüm hello swagger
Merhaba bkz [ayrıntıları swagger](/connectors/as2/). 

## <a name="next-steps"></a>Sonraki adımlar
[Merhaba Enterprise Integration Pack hakkında daha fazla bilgi](logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin") 

