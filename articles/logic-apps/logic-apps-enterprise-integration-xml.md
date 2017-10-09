---
title: "XML ile aaaWorking iletiler, iş akışlarında - Azure Logic Apps | Microsoft Docs"
description: "İşlem, doğrulama, dönüştürme ve XML zenginleştirmek mantıksal uygulamalar ve iş tooscenarios kullanarak iletileri hello Kurumsal tümleştirme paketi"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 47672dc4-1caa-44e5-b8cb-68ec3a76b7dc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 02/27/2017
ms.author: LADocs; mandia
ms.openlocfilehash: f90ae89fef0a4bd17286adbce398e573940bb790
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="validate-and-transform-xml-encode-and-decode-flat-files-and-enrich-messages-features-in-logic-apps"></a>Doğrulama ve XML dönüştürme, kodlama ve düz dosyalar kod çözme ve logic apps iletilerin özelliklerinde zenginleştirmek

Logic apps'ı kullanarak, gönderme ve alma hello özelliği tooprocess XML iletileri sahip. Bu özellik Enterprise Integration Pack Merhaba ile dahil edilir. Bu kullanıcılara bir BizTalk Server arka plana sahip hello Enterprise Integration Pack benzer yeteneklerini tootransform sağlar ve iletileri doğrulamak, düz dosyalarla ve bile XPath tooenrich kullanın veya belirli özellikleri iletiden ayıklar. 

Yeni toothis alanı olan kullanıcılar bu özellikler, iş akışı içinde iletileri işleminin nasıl genişletin. İşletmeler için senaryoda ve hello Kurumsal tümleştirme paketi tooenhance kullanabilirsiniz belirli XML şemaları ile çalışma, örneğin, nasıl şirketiniz bu iletileri işler. 

Merhaba Kurumsal tümleştirme paketi içerir: 

* [XML doğrulaması](logic-apps-enterprise-integration-xml-validation.md "XML ileti doğrulama hakkında daha fazla bilgi") -gelen veya giden XML iletisine belirli bir şemaya karşı doğrulama.
* [XML dönüştürme](../logic-apps/logic-apps-enterprise-integration-transform.md "XML ileti dönüşümleri ve eşlemeleri hakkında bilgi edinin") - Dönüştür veya XML iletisine, gereksinimleri veya bir iş ortağı hello gereksinimlerine göre özelleştirin.
* [Düz dosya kodlama ve kod çözme düz dosya](logic-apps-enterprise-integration-flatfile.md "düz dosya kodlama/kod çözme hakkında bilgi edinin") - kodlamak veya düz dosyadır kodunu çözer. Örneğin, SAP kabul eder ve düz dosya biçiminde IDOC dosyaları gönderir. Birçok tümleştirme platformda Logic Apps dahil olmak üzere, XML iletileri oluşturun. Bu nedenle, kullandığı hello düz dosya Kodlayıcısı çok "XML dosyalarını tooflat dönüştürmeniz" bir mantıksal uygulama oluşturabilirsiniz. 
* [XPath](https://msdn.microsoft.com/library/mt643789.aspx) - bir ileti zenginleştirmek ve belirli özellikler hello iletiden ayıklayın. Kullanım hello özellikleri tooroute hello ileti tooa hedef veya aracı bir uç nokta ayıklanan sonra kullanabilirsiniz.

## <a name="try-it-out"></a>Deneyin
[Tam olarak işlevsel mantıksal uygulama dağıtma ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (GitHub örneği) Azure Logic Apps içinde hello XML özelliklerini kullanarak.

## <a name="learn-more"></a>Daha fazla bilgi edinin
[Merhaba Enterprise Integration Pack hakkında daha fazla bilgi](../logic-apps/logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin")
