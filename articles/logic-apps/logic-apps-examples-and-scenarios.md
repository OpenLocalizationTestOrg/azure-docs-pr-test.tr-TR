---
title: aaaExamples & ortak senaryolar - Azure Logic Apps | Microsoft Docs
description: "Logic apps örnekler, senaryoları ve öğreticiler ile ilgili daha fazla bilgi edinin"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: e06311bc-29eb-49df-9273-1f05bbb2395c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/9/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 17caa8539ec6a57726b9c6c07a71fb74caa07ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="examples-and-common-scenarios-for-azure-logic-apps"></a>Örnekler ve Azure mantıksal uygulamaları için genel senaryolar

hakkında daha fazla bilgi toohelp Merhaba birçok desenleri ve Azure Logic Apps özelliklerini, yayın örnekleri ve senaryoları şunlardır.

## <a name="key-scenarios-for-logic-apps"></a>Logic apps yönelik temel senaryolar

Azure mantıksal uygulamaları dayanıklı orchestration ve farklı hizmetler için tümleştirme sağlar. Merhaba Logic Apps hizmeti "sunucusuz", Ölçek veya örnekleri hakkında tooworry yok - toodo sahip olduğunuz tüm şekilde hello iş akışı (tetikleyici ve Eylemler) tanımlayın. Merhaba temel platform ölçek, kullanılabilirlik ve performans işler. İhtiyaç duyacağınız toocoordinate birden çok Eylemler, her senaryo mükemmel kullanım örneği Azure Logic Apps için özellikle birden çok sistem üzerinde değil. Bazı desenleri ve örnekleri aşağıda verilmiştir.

## <a name="respond-tootriggers-and-extend-actions"></a>Tootriggers yanıt ve Eylemler genişletme

Her mantıksal uygulama tetikleyici ile başlar. Örneğin, iş akışınızı bir zamanlama olayı, el ile çağırma veya bir dış sistemden bir olay gibi başlatabilirsiniz hello "bir dosya tooan FTP sunucusu eklendiğinde" tetikleyicisi. Azure mantıksal uygulamaları, şu anda şirket içi SAP tooMicrosoft Bilişsel hizmetler arasında değişen 100'den kullanıma hazır bağlayıcıları destekler. Sistemler ve bağlayıcılar yayımlanmamış hizmetler için mantıksal uygulamalar da genişletebilirsiniz.

* [Özel Tetikleyicileri veya eylemler oluşturun](../logic-apps/logic-apps-create-api-app.md)
* [İş akışı çalışmaya uzun süre çalışan eylemlerini ayarlama](../logic-apps/logic-apps-create-api-app.md)
* [Tooexternal olayları ve eylemleri ile Web kancalarını yanıt](../logic-apps/logic-apps-create-api-app.md)
* [Çağrı, tetikleyici veya zaman uyumlu yanıtları tooHTTP istekleri iş akışlarıyla iç içe](../logic-apps/logic-apps-http-endpoint.md)
* [Öğretici: tooTwilio SMS kancalarını yanıt ve metin yanıt gönderme](https://channel9.msdn.com/Blogs/Windows-Azure/Azure-Logic-Apps-Walkthrough-Webhook-Functions-and-an-SMS-Bot)
* [Öğretici: dakika Logic Apps ve Power BI ile derleme olarak AI destekli bir Sosyal Panosu](http://aka.ms/logicappsdemo)

## <a name="error-handling-logging-and-control-flow-capabilities"></a>Hata işleme, günlüğe kaydetme ve denetim akışı özellikleri

Logic apps koşullar, anahtarları, döngüler ve kapsamları gibi gelişmiş denetim akışı için zengin özellikleri içerir. tooensure dayanıklı çözümler, hata ve özel durum, iş akışlarında işleme de uygulayabilirsiniz. Bildirim ve iş akışı çalışma durumu için tanılama günlükleri için Azure mantıksal uygulamaları izleme ve uyarılar de sağlar.

* [Switch deyimleri ile farklı eylemler gerçekleştirme](../logic-apps/logic-apps-switch-case.md)
* [Diziler ve koleksiyonlarla döngüler ve mantıksal uygulamalar'toplu işlem öğeleri](../logic-apps/logic-apps-loops-and-scopes.md)
* [Yazar hata ve özel durum bir iş akışında işleme](../logic-apps/logic-apps-exception-handling.md)
* [İzleme, günlüğe kaydetme ve mevcut mantıksal uygulamaları için uyarıları Aç](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [İzleme ve tanılama günlük kaydı mantığı uygulamaları oluştururken Aç](../logic-apps/logic-apps-monitor-your-logic-apps-oms.md)
* [Kullanım örneği: sağlık şirket mantığı uygulama özel durum HL7 FHIR iş akışları için işleme nasıl kullanır](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)

## <a name="deploy-and-manage-logic-apps"></a>Mantıksal uygulamaları dağıtma ve yönetme

Tam olarak geliştirmek ve logic apps Visual Studio, Visual Studio Team Services veya diğer kaynak denetimi ve otomatik derleme araçları ile dağıtın. toosupport dağıtım iş akışları ve kaynak şablonu bağımlı bağlantıları için logic apps Azure kaynak dağıtım şablonları kullanın. Visual Studio Araçları, sürüm oluşturma için toosource denetiminde denetleyebilirsiniz bu şablonları otomatik olarak oluşturur.

* [Bir otomatik dağıtım şablonu oluşturma](../logic-apps/logic-apps-create-deploy-template.md)
* [Derleme ve logic apps Visual Studio'dan dağıtma](../logic-apps/logic-apps-deploy-from-vs.md)
* [Mantıksal uygulamalarınızı Hello durumunu izleme](../logic-apps/logic-apps-monitor-your-logic-apps.md)

## <a name="content-types-conversions-and-transformations-within-a-run"></a>İçerik türleri, dönüştürme ve çalışması içinde dönüşümleri

Erişim, dönüştürme ve hello Azure Logic Apps içinde birçok işlevini hello kullanarak birden çok içerik türleri dönüştürme [iş akışı tanımlama dili](http://aka.ms/logicappsdocs). Örneğin, dize, JSON ve XML arasında ile Merhaba dönüştürebilirsiniz `@json()` ve `@xml()` iş akışı ifadeler. Merhaba Logic Apps altyapısı içerik türleri toosupport içerik aktarım hizmetleri arasında kayıpsız bir şekilde korur.

* [JSON olmayan içerik türleri işlemek](../logic-apps/logic-apps-content-type.md)gibi `application/xml`, `application/octet-stream`, ve`multipart/formdata`
* [İş akışı ifadeleri logic apps içinde nasıl çalışır](../logic-apps/logic-apps-author-definitions.md)
* [Başvuru: Azure mantıksal uygulamaları iş akışı tanımlama dili](http://aka.ms/logicappsdocs)

## <a name="other-integrations-and-capabilities"></a>Diğer tümleştirmeler ve özellikleri

Logic apps, Azure işlevleri, Azure API Management, Azure App Services ve özel HTTP uç noktaları, örneğin, REST ve SOAP gibi birçok Hizmetleri ile tümleştirme de sunar.

* [Gerçek zamanlı sosyal Pano Azure sunucusuz ile oluşturma](../logic-apps/logic-apps-scenario-social-serverless.md)
* [Mantığı uygulamalardan Azure işlevlerini çağırma](../logic-apps/logic-apps-azure-functions.md)
* [Senaryo: Tetikleyici logic apps ile Azure işlevleri](../logic-apps/logic-apps-scenario-function-sb-trigger.md)
* [Blog: Çağrı mantığı uygulamalardan SOAP uç noktası](https://blogs.msdn.microsoft.com/logicapps/2016/04/07/using-soap-services-with-logic-apps/)

## <a name="end-to-end-scenarios"></a>Uçtan uca senaryolar

* [Teknik İnceleme: Kurumsal tümleştirme uçtan uca servis talebi yönetimi Logic Apps gibi Azure hizmetleriyle](https://aka.ms/enterprise-integration-e2e-case-management-utilities-logic-apps)

## <a name="next-steps"></a>Sonraki adımlar

- [Hataları ve logic apps içinde özel durumları işleme](../logic-apps/logic-apps-exception-handling.md)
- [Merhaba iş akışı tanımlama dili ile yazar iş akışı tanımları](../logic-apps/logic-apps-author-definitions.md)
- [Biz Azure mantıksal uygulamaları nasıl geliştirmek için açıklamalar, sorular, geri bildirim veya önerileri gönderme](https://feedback.azure.com/forums/287593-logic-apps)