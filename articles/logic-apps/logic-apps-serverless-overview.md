---
title: Azure sunucusuz, aaaOverview | Microsoft Docs
description: "Güçlü çözümler altyapısıyla ilgili toothink gerek kalmadan hello bulutta oluşturun."
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 7c9c09d96e472edd1631892982ac60aae97342a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-serverless-with-functions-and-logic-apps"></a>Azure işlevleri ve Logic Apps ile sunucusuz genel bakış

Sunucusuz uygulamaları geliştirme hızını artış, gerekli kod ve Basitlik ölçekli azalma avantajları sunar.  Bu makalede sunucusuz çözümleri ve Azure sunucusuz teklifleri hello farklı öznitelikler gider.

## <a name="what-is-serverless"></a>Sunucusuz nedir?

Sunucusuz sunucu yok - yalnızca hello Geliştirici sunucuları hakkında tooworry yok anlamına gelmez.  Geleneksel uygulama geliştirme büyük bir bölümünü ölçeklendirme, barındırma ve çözümleri toomeet hello taleplerini hello uygulama izleme çevresinde sorulara yanıt verilmesi.  Sunucusuz ile bu soruları hello çözümün bir parçası dikkate.  Ayrıca, sunucusuz uygulamaları tüketim tabanlı bir plana göre faturalandırılır.  Merhaba uygulaması hiçbir zaman kullanılırsa, bir ücret hiçbir zaman oluşur.  Bu özellikleri geliştiricilerin izin toofocus hello iş mantığı hello çözümün üzerinde güvenmeyin.

Sunucusuz geçici azure'da Hello çekirdek Hizmetler [Azure işlevleri](https://azure.microsoft.com/services/functions/) ve [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).  Bu çözümlerin hem de hello ilkeler yukarıdaki izleyin ve geliştiricilerin çok az kod toobuild sağlam bulut uygulamalarıyla olanak sağlar.

## <a name="what-are-azure-functions"></a>Azure işlevleri nelerdir?

Azure işlevleri hello bulutta kolayca kodu veya "işlevleri" küçük parçalarını çalıştırmak için bir çözüm olur. Bu tam bir uygulama veya hello altyapı toorun hakkında endişelenmeden elinizdeki hello sorun için ihtiyacınız yalnızca hello kod yazabilirsiniz. Geliştirme işlevlerini daha da verimli hale getirebilir ve C#, F #, Node.js, Python veya PHP gibi tercih ettiğiniz geliştirme dilini kullanabilirsiniz. Yalnızca kodunuzun çalıştığı hello zaman için ödeme ve gerektiğinde Azure ölçeklendirir.

Toojump sağ istediğiniz ve Azure işlevlerini kullanmaya başlamak, başlayın [ilk Azure işlevinizi oluşturma](../azure-functions/functions-create-first-azure-function.md). Merhaba işlevler hakkında daha fazla teknik bilgi arıyorsanız bkz [Geliştirici Başvurusu](../azure-functions/functions-reference.md).

## <a name="what-are-azure-logic-apps"></a>Azure Logic Apps nedir?

Azure mantıksal uygulamaları şekilde toosimplify sağlar ve ölçeklenebilir tümleştirmeler ve iş akışları hello bulutta uygular. Görsel Tasarımcı toomodel sağlar ve bir iş akışının adı verilen adımları bir dizi olarak işleminizi otomatikleştirmek.  Vardır [birçok Bağlayıcılar](../connectors/apis-list.md) Bulut ve şirket içi hizmetler arasında tooquickly sunucusuz uygulama tooother API'leri bağlanın.  Bir mantıksal uygulama tetikleyicisi'yle ('bir hesap tooDynamics CRM eklendiğinde' like) başlar ve tetikleme birçok birleşimleri Eylemler, dönüştürme ve koşul mantığı başladıktan sonra.  Özellikle bir dış sistem veya API ile etkileşim hello işlem gerektirdiğinde, bir işlemde - farklı Azure işlevleri yönetme olduğunda, Logic Apps harika bir seçim kullanır.

tooget Logic Apps ile başlatıldı, başlayın [ilk mantıksal uygulamanızı oluşturma](logic-apps-create-a-logic-app.md).  Merhaba Logic Apps hakkında daha fazla teknik bilgi arıyorsanız bkz [Geliştirici Başvurusu](logic-apps-workflow-actions-triggers.md).

## <a name="how-can-i-build-and-deploy-serverless-applications-in-azure"></a>Nasıl derleme ve Azure sunucusuz uygulamalar dağıtmak?

Azure, geliştirme, dağıtımı ve sunucusuz uygulamaların Yönetimi zengin birtakım araçlar sağlar.  Uygulamaları doğrudan hello Azure portal veya ile oluşturulabilen [Visual Studio'dan tooling](logic-apps-serverless-get-started-vs.md).  Bir uygulama geliştirilen bir kez olabilir [anında dağıtılan](logic-apps-create-deploy-template.md).  Azure sunucusuz uygulamaları için izleme de sağlar.  Bu izleme hello Azure portal, hello API veya SDK aracılığıyla veya tümleşik araç tooOMS ve Application Insights ile erişilebilir.

## <a name="next-steps"></a>Sonraki adımlar

* [Visual Studio'da sunucusuz bir uygulama oluşturmaya başlayın](logic-apps-serverless-get-started-vs.md)
* [Bir müşteri öngörüleri Panosu sunucusuz ile oluşturma](logic-apps-scenario-social-serverless.md)
* [Bir dağıtım şablonu için bir mantıksal uygulama oluşturma](logic-apps-create-deploy-template.md)