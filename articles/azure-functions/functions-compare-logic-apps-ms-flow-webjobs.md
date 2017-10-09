---
title: "Akış, Logic Apps, İşlevler ve Web işleri arasında aaaChoose | Microsoft Docs"
description: "Karşılaştır ve karşıtlık Microsoft bulut tümleştirme hizmetlerinin hello ve kullanması gereken hangi hizmetlere karar verin."
services: functions,app-service\logic
documentationcenter: na
author: cephalin
manager: wpickett
tags: 
keywords: "Microsoft akışı, akış, logic apps, azure işlevleri, İşlevler, azure webjobs, Web işleri, olay işleme, dinamik işlem sunucusuz mimarisi"
ms.assetid: e9ccf7ad-efc4-41af-b9d3-584957b1515d
ms.service: functions
ms.devlang: multiple
ms.topic: overview
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/03/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 6becc1e389698e517924b18295dac4375542d524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="choose-between-flow-logic-apps-functions-and-webjobs"></a>Flow, Logic Apps, Functions ve WebJobs arasında seçim yapma
Bu makalede karşılaştırır ve tüm tümleştirme sorunları ve iş süreçlerini otomasyonunu çözebilir hello Microsoft bulut hizmetlerinde aşağıdaki hello farklılık gösterir:

* [Microsoft Akış](https://flow.microsoft.com/)
* [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/)
* [Azure İşlevleri](https://azure.microsoft.com/services/functions/)
* [Azure uygulama hizmeti Web işleri](../app-service-web/web-sites-create-web-jobs.md)

Tüm bu hizmetleri "yapıştırma farklı sistemleri birbirine" yararlı olur. Bunlar tüm giriş, Eylemler, koşullar ve çıkış tanımlayabilirsiniz. Bunların her biri bir zamanlama veya tetikleyici çalıştırabilirsiniz. Ancak, her hizmetin benzersiz bir değer kümesi ekler ve bunları karşılaştırma "hangi hizmet hello en iyi olduğu?" sorusunu değil Ancak bir "hangi hizmetin en iyisidir bu durum için uygun?" Genellikle, bu hizmetleri birlikte toorapidly ölçeklenebilir, tam özellikli tümleştirme çözümü derleme hello en iyi yoludur.

<a name="flow"></a>

## <a name="flow-vs-logic-apps"></a>Akış vs. Logic Apps
Her ikisi de olduklarından Azure mantıksal uygulamaları ve Microsoft Flow birlikte aşağıdakiler ele *yapılandırma ilk* ve iş akışları kolay toobuild işlemlerini kolaylaştırır ve çeşitli SaaS ve kurumsal tümleştirme tümleştirme hizmetleri uygulamalar. 

* Akış Logic Apps en üstünde oluşturulmuştur
* Merhaba sahip oldukları aynı iş akışı Tasarımcısı
* [Bağlayıcılar](../connectors/apis-list.md) bir iş hello diğer çalışabilir

Akışlar güçlendirir tüm office çalışan tooperform basit tümleştirmeler (örn. SMS için önemli e-postaları alması) aracılığıyla geliştiricilerin giderek olmadan veya BT. Üzerindeki diğer yandan Merhaba, Logic Apps kuruluş düzeyinde DevOps ve güvenlik uygulamalarını gerekli olduğu Gelişmiş ya da kritik tümleştirmeler (örneğin B2B işlemler) etkinleştirebilirsiniz. Karmaşıklık mesai bir iş akışı toogrow için tipik olarak. Buna uygun olarak, başta bir akış başlayın sonra gerektiği gibi tooa mantıksal uygulama dönüştürmek.

Merhaba aşağıdaki tabloda akış veya Logic Apps belirli bir tümleştirme için en iyi olduğunu belirlemenize yardımcı olur.

|  | Akış | Logic Apps |
| --- | --- | --- |
| Hedef kitle |Office çalışanlarının, iş kullanıcılarının |BT uzmanları, geliştiricilerin |
| Senaryolar |Self Servis |Kritik |
| Tasarım aracı |Tarayıcı içi ve mobil uygulama, yalnızca kullanıcı Arabirimi |Tarayıcı içi ve [Visual Studio](../logic-apps/logic-apps-deploy-from-vs.md), [kod görünümü](../logic-apps/logic-apps-author-definitions.md) kullanılabilir |
| DevOps |Geçici, üretimde geliştirin |Kaynak denetimi, test, destek otomasyon ve yönetilebilirlik, [Azure kaynak yönetimi](../logic-apps/logic-apps-arm-provision.md) |
| Yönetici deneyimi |[https://Flow.microsoft.com](https://flow.microsoft.com) |[https://Portal.Azure.com](https://portal.azure.com) |
| Güvenlik |Standart uygulamalar: [veri egemenliği](https://wikipedia.org/wiki/Technological_Sovereignty), [bekleyen şifreleme](https://wikipedia.org/wiki/Data_at_rest#Encryption) hassas verileri için vb.. |Azure güvenlik güvencesi: [Azure güvenlik](https://www.microsoft.com/trustcenter/Security/AzureSecurity), [Güvenlik Merkezi](https://azure.microsoft.com/services/security-center/), [denetim günlüklerini](https://azure.microsoft.com/blog/azure-audit-logs-ux-refresh/)ve daha fazlası. |

<a name="function"></a>

## <a name="functions-vs-webjobs"></a>İşlevler vs. WebJobs
Her ikisi de olduklarından Azure işlevleri ve Azure App Service Web işleri birlikte aşağıdakiler ele *kod ilk* tümleştirme hizmetleri ve geliştiricileri için tasarlanmıştır. Bunlar toorun komut dosyası veya yanıt toovarious olaylarını kodda parçası gibi etkinleştirmeniz [yeni depolama BLOB'lar](functions-bindings-storage.md) veya [bir Web kancası isteği](functions-bindings-http-webhook.md). Kendi benzerlikler şunlardır: 

* Her ikisi de yerleşik [Azure App Service](../app-service/app-service-value-prop-what-is.md) ve özellikleri gibi keyfini [kaynak denetimi](../app-service-web/app-service-continuous-deployment.md), [kimlik doğrulaması](../app-service/app-service-authentication-overview.md), ve [izleme](../app-service-web/web-sites-monitor.md).
* Her ikisi de Geliştirici odaklı hizmetleridir.
* Hem standart komut ve programlama dilleri destekler.
* Hem NuGet ve NPM'yi destek sahiptir.

İşlevler var. hello doğal WebJobs evrimi hello en iyi şeyler Web işleri hakkında alır ve bunlar üzerine artırır Merhaba geliştirmeleri içerir: 

* Kolaylaştırılmış geliştirme, test ve hello tarayıcıda doğrudan kod çalıştırın.
* Daha fazla Azure ve 3. taraf hizmetleri ile dahili tümleştirmeyi ister [GitHub Web kancası](https://developer.github.com/webhooks/creating/).
* Kullanım başına ödeme, hiçbir gerek toopay için bir [uygulama hizmeti planı](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
* Otomatik, [dinamik ölçeklendirme](functions-scale.md).
* Uygulama hizmeti, uygulama hizmeti planı üzerinde hala olası (kullanılan kaynaklar avantajlarından tootake) çalıştıran varolan müşteriler için.
* Logic Apps ile tümleştirme.

Aşağıdaki tablonun hello hello farklarını işlevlerini ve Web işleri özetlenmektedir:

|  | İşlevler | WebJobs |
| --- | --- | --- |
| Ölçeklendirme |Configurationless ölçeklendirme |Uygulama hizmeti planı ile ölçeklendirin |
| Fiyatlandırma |Kullanım başına ödeme ya da uygulama hizmeti planının bir parçası |Uygulama hizmeti planının bir parçası |
| Çalışma türü |tetiklenen, zamanlanmış (Zamanlayıcı tetikleyicisi tarafından) |tetiklenen, sürekli, zamanlanmış |
| Tetikleyici olayları |[Zamanlayıcı](functions-bindings-timer.md), [Azure Cosmos DB](functions-bindings-documentdb.md), [Azure Event Hubs](functions-bindings-event-hubs.md), [HTTP/Web (GitHub, Slack'e) kancası](functions-bindings-http-webhook.md), [Azure App Service Mobile Apps](functions-bindings-mobile-apps.md), [Azure Notification Hubs](functions-bindings-notification-hubs.md), [Azure Service Bus](functions-bindings-service-bus.md), [Azure depolama](functions-bindings-storage.md) |[Azure depolama](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), [Azure hizmet veri yolu](../app-service-web/websites-dotnet-webjobs-sdk-service-bus.md) |
| Tarayıcı içi geliştirme |Desteklenen | Desteklenmiyor |
| Komut penceresi |Deneysel |Desteklenen |
| PowerShell |Deneysel |Desteklenen |
| C# |Desteklenen |Desteklenen |
| F# |Desteklenen |Desteklenmiyor |
| Bash |Deneysel |Desteklenen |
| PHP |Deneysel |Desteklenen |
| Python |Deneysel |Desteklenen |
| JavaScript |Desteklenen |Desteklenen |

Olup toouse işlevleri veya Web işleri sonuçta ne zaten App Service ile yaptığınız üzerinde bağlıdır. Toorun kod parçacıkları istediğiniz bir uygulama hizmeti uygulaması varsa ve toomanage isterseniz bunları bir araya Merhaba aynı DevOps ortamı, Web işleri kullanmanız gerekir. Diğer Azure Hizmetleri veya hatta 3. taraf uygulamaları için toorun kod parçacıkları istediğiniz ya da çok tümleştirme kod parçacıkları, uygulama hizmeti uygulamalardan ayrı ayrı yönetmek istiyorsanız veya bir mantıksal uygulama, kod parçacıkları toocall istiyorsanız, tüm avantajlarından yararlanmak İşlevler Hello geliştirmeleri.  

<a name="together"></a>

## <a name="flow-logic-apps-and-functions-together"></a>Akış, Logic Apps ve işlevleri birlikte
Daha önce belirtildiği gibi en uygun tooyou hizmetidir sizin durumunuza bağlıdır. 

* Basit iş iyileştirme için daha sonra akışı kullanın.
* Tümleştirme senaryonuz için akışı çok gelişmiş veya DevOps özellikleri ve güvenlik compliances gerekirse, Logic Apps kullanın.
* Tümleştirme senaryonuz bir adımda, yüksek oranda özel dönüştürme veya özel bir kod gerektiriyorsa, bir işlev uygulaması yazma ve bir eylem mantıksal uygulamanızı olarak bir işlev tetikler.

Bir mantıksal uygulama bir akışı çağırabilirsiniz. Ayrıca, bir mantıksal uygulama ve bir mantıksal uygulama işlevinde bir işlevde çağırabilirsiniz. Akış, Logic Apps ve işlevleri arasında Hello tümleştirme tooimprove mesai devam edin. Şeyin bir hizmet oluşturmak ve diğer hizmetleri hello kullanın. Bu nedenle, bu üç teknolojileri yaptığınız tüm Yatırımlar faydalı olur.

## <a name="next-steps"></a>Sonraki Adımlar
Her hello Hizmetleri ile ilk akış, mantıksal uygulama, işlev uygulaması veya Web işi oluşturarak başlayın. Aşağıdaki bağlantılar hello birini tıklatın:

* [Microsoft Flow kullanmaya başlama](https://flow.microsoft.com/en-us/documentation/getting-started/)
* [Mantıksal uygulama oluşturun.](../logic-apps/logic-apps-create-a-logic-app.md)
* [İlk Azure İşlevinizi oluşturma](functions-create-first-azure-function.md)
* [Visual Studio kullanarak Web İşleri’ni dağıtma](../app-service-web/websites-dotnet-deploy-webjobs.md)

Veya bağlantılar aşağıdaki hello ile bu tümleştirme hizmetleri hakkında daha fazla bilgi alın:

* [Yararlanmayı Azure işlevleri & Christopher Yılmaz tarafından tümleştirme senaryoları için Azure uygulama hizmeti](http://www.biztalk360.com/integrate-2016-resources/leveraging-azure-functions-azure-app-service-integration-scenarios/)
* [Charles Lamanna tarafından basit yapılan tümleştirmeler](http://www.biztalk360.com/integrate-2016-resources/integrations-made-simple/)
* [Logic Apps canlı Web yayını](http://aka.ms/logicappslive)
* [Microsoft Akış sık sorulan sorular](https://flow.microsoft.com/documentation/frequently-asked-questions/)
* [Azure Web işleri belge kaynakları](../app-service-web/websites-webjobs-resources.md)

