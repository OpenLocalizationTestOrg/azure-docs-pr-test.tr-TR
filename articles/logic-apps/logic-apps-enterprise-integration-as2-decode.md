---
title: aaaDecode AS2 iletileri - Azure Logic Apps | Microsoft Docs
description: "Nasıl toouse hello AS2 Çözücü'hello Kurumsal tümleştirme paketi de Azure mantıksal uygulamaları için"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 2406e5ec68e0906700fad97d60cb83ef0d106cd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>AS2 iletileri Enterprise Integration Pack Merhaba ile Azure mantıksal uygulamaları için kod çözme 

tooestablish güvenlik ve güvenilirlik iletileri aktarımı sırasında hello kod çözme AS2 ileti bağlayıcı kullanın. Bu bağlayıcı, dijital imza, şifre çözme ve onayları ileti Disposition bildirimler (MDN) aracılığıyla sağlar.

## <a name="before-you-start"></a>Başlamadan önce

Gereksinim duyduğunuz hello öğeleri şöyledir:

* Bir Azure hesabı; oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free)
* Bir [tümleştirme hesabını](logic-apps-enterprise-integration-create-integration-account.md) , daha önce tanımlanan ve Azure aboneliğinizle ilişkili. Bir tümleştirme hesap toouse hello kod çözme AS2 ileti Bağlayıcısı olması gerekir.
* En az iki [ortakları](logic-apps-enterprise-integration-partners.md) tümleştirme hesabınızda zaten tanımlanmış
* Bir [AS2 sözleşmesi](logic-apps-enterprise-integration-as2.md) tümleştirme hesabınızda tanımlanan zaten

## <a name="decode-as2-messages"></a>AS2 iletileri kod çözme

1. [Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).

2. bir istek tetikleyici gibi mantıksal uygulamanızı başlatmak için bir tetikleyici eklemelisiniz hello kod çözme AS2 ileti bağlayıcı tetikleyiciler, sahip değil. Hello mantığı Uygulama Tasarımcısı, tetikleyici ekleyin ve sonra bir eylem tooyour mantıksal uygulama ekleyin.

3.  Merhaba arama kutusuna "AS2" filtreniz için girin. Seçin **AS2 - kod çözme AS2 ileti**.
   
    !["AS2" için arama](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. Tooyour tümleştirme hesabını daha önce herhangi bir bağlantısı oluşturmadıysanız, istenir toocreate şimdi bu bağlantı. Bağlantınızı adlandırın ve hello tümleştirme hesabı tooconnect istediğinizi seçin.
   
    ![Tümleştirme bağlantısı oluşturma](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    Bir yıldız işareti özelliklerle gereklidir.

    | Özellik | Ayrıntılar |
    | --- | --- |
    | Bağlantı adı * |Bağlantınız için herhangi bir ad girin. |
    | Tümleştirme hesabını * |Tümleştirme hesabınız için bir ad girin. Tümleştirme hesabı ve mantıksal uygulamanızı hello olduğundan emin olun aynı Azure konumu. |

5.  İşiniz bittiğinde, bağlantı ayrıntılarınızı benzer toothis örnek görünmelidir. bağlantı oluşturma toofinish seçin **oluşturma**.

    ![Tümleştirme bağlantı ayrıntıları](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. Bu örnekte gösterildiği gibi bağlantınızı oluşturulduktan sonra Seç **gövde** ve **üstbilgileri** çıkışları hello istek.
   
    ![oluşturulan tümleştirme bağlantı](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    Örneğin:

    ![Gövde ve üstbilgileri isteği çıkışlarından seçin](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a>AS2 decoder ayrıntıları

Merhaba kod çözme AS2 Bağlayıcısı, şu görevleri gerçekleştirir: 

* AS2/HTTP üstbilgileri işler
* (Yapılandırılmışsa) Hello imzayı doğrular
* Merhaba iletileri (yapılandırılmışsa) şifresini çözer.
* Merhaba iletisi (yapılandırılmışsa) açar
* Alınan MDN hello özgün giden iletiyle çözümler
* Güncelleştirmeleri ve hello takası veritabanındaki kayıtları karşılık gelen
* AS2 durumu raporlama için kayıtları Yazar
* Merhaba çıkış yükü içeriği base64 ile kodlanmış olan
* Bir MDN gereklidir ve olup hello MDN zaman uyumlu olması gerekir veya AS2 sözleşmesi zaman uyumsuz yapılandırmasını temel alarak belirler
* (Sözleşmesi yapılandırmalarını temel alan) zaman uyumlu veya zaman uyumsuz bir MDN oluşturur
* Merhaba MDN üzerinde Hello bağıntı belirteçleri ve özelliklerini ayarlar

## <a name="try-this-sample"></a>Bu örnek deneyin

bir tam olarak işlevsel mantığı uygulamasını ve örnek AS2 senaryo dağıtma tootry bkz hello [AS2 mantıksal uygulama şablonu ve senaryo](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).

## <a name="view-hello-swagger"></a>Görünüm hello swagger
Merhaba bkz [ayrıntıları swagger](/connectors/as2/). 

## <a name="next-steps"></a>Sonraki adımlar
[Merhaba Enterprise Integration Pack hakkında daha fazla bilgi edinin](logic-apps-enterprise-integration-overview.md) 

