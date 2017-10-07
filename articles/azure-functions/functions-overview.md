---
title: "aaaAzure işlevlerine genel bakış | Microsoft Docs"
description: "Anlamak nasıl toouse Azure işlevleri toooptimize zaman uyumsuz iş yüklerini dakika."
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: "azure işlevleri, işlevler, olay işleme, web kancaları, dinamik işlem, sunucusuz mimari"
ms.assetid: 01d6ca9f-ca3f-44fa-b0b9-7ffee115acd4
ms.service: functions
ms.devlang: multiple
ms.topic: overview
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/27/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 668f9055a007fee662a4c7ec774d3c0a1d847800
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-functions"></a>Bir giriş tooAzure işlevleri  
Azure işlevleri hello bulutta kolayca kodu veya "işlevleri" küçük parçalarını çalıştırmak için bir çözüm olur. Bu tam bir uygulama veya hello altyapı toorun hakkında endişelenmeden elinizdeki hello sorun için ihtiyacınız yalnızca hello kod yazabilirsiniz. İşlevler geliştirme sürecinizi daha da verimli hale getirebilir ve tercih ettiğiniz geliştirme dilini (C#, F#, Node.js, Python veya PHP gibi) kullanabilirsiniz. Yalnızca kodunuzun çalıştığı hello zaman için ödeme ve gerektiğinde Azure tooscale güven. Azure İşlevleri, Microsoft Azure'da sunucusuz uygulamalar geliştirmenizi sağlar.

Bu konu başlığında, Azure İşlevlerine üst düzey bir genel bakış sağlanmıştır. Toojump sağ istediğiniz ve Azure işlevlerini kullanmaya başlamak, başlayın [ilk Azure işlevinizi oluşturma](functions-create-first-azure-function.md). Merhaba işlevler hakkında daha fazla teknik bilgi arıyorsanız bkz [Geliştirici Başvurusu](functions-reference.md).

## <a name="features"></a>Özellikler
Azure İşlevlerinin önemli özelliklerinden bazıları şunlardır:

* **Dil seçimi** - C#, F#, Node.js, Python, PHP, batch, bash veya herhangi bir yürütülebilir dosya kullanarak işlevleri yazın.
* **Ödeme-kullanım başına fiyatlandırma modeli** - ödeme Merhaba yalnızca kodunuzu çalıştırmaya harcanan zaman. Merhaba seçeneğinde planlama tüketim Hello barındırma bkz [fiyatlandırma bölümünde](#pricing).  
* **Kendi bağımlılıklarınızı getirin** - İşlevler NuGet ve NPM'yi desteklediğinden, sık kullandığınız kitaplıklarınızı kullanabilirsiniz.  
* **Tümleşik güvenlik** - Azure Active Directory, Facebook, Google, Twitter ve Microsoft Hesabı gibi OAuth sağlayıcılarıyla HTTP tetiklemeli işlevleri koruyun.  
* **Basitleştirilmiş tümleştirme** - Azure hizmetlerini ve yazılım olarak hizmet (SaaS) tekliflerini kolayca kullanın. Merhaba bkz [tümleştirme bölümüne](#integrations) bazı örnekler için.  
* **Esnek geliştirme** - işlevlerinizi doğrudan hello Portalı'nda kod veya sürekli tümleştirme kurup ve kodunuzu GitHub, Visual Studio Team Services ve diğer aracılığıyla dağıtma [desteklenen geliştirme araçları](../app-service-web/web-sites-deploy.md#deploy-using-an-ide).  
* **Açık kaynak** -hello işlevleri çalışma zamanı açık kaynaklı ve [github'da](https://github.com/azure/azure-webjobs-sdk-script).  

## <a name="what-can-i-do-with-functions"></a>İşlevler ile ne yapabilirim?
Azure işlevleri; verileri işleme için harika bir çözümdür, çalışma sistemlerini tümleştirme-in-interneti (IOT) hello ve basit API'ler ve mikro hizmetler oluşturma. İşlevler bir zamanlamaya göre toorun istediğiniz herhangi bir görevi veya görüntü veya sıra işleme, dosya bakımı gibi görevleri için göz önünde bulundurun. 

İşlev şablonları tooget hello aşağıdakileri de dahil olmak üzere önemli senaryolara giriş sağlar:

* **BlobTrigger** -Azure Storage bloblarını toocontainers eklendiğinde. Görüntüyü yeniden boyutlandırmak için bu işlevi kullanabilirsiniz.
* **EventHubTrigger** -tooevents teslim tooan Azure olay hub'ı yanıt. Uygulama izleme, kullanıcı deneyiminde veya iş akışı işlemede ve Nesnelerin İnterneti (IoT) senaryolarında özellikle kullanışlıdır.
* **Genel web kancası** - Web kancalarını destekleyen herhangi bir hizmetten web kancası HTTP isteklerini işler.
* **GitHub Web kancası** -GitHub depolarınızda gerçekleşen yanıt tooevents. Örnek olarak bkz. [Bir web kancası veya API işlevi oluşturma](functions-create-a-web-hook-or-api-function.md).
* **HTTPTrigger** -bir HTTP isteği kullanarak kodunuzun yürütülmesini hello tetikler.
* **QueueTrigger** -bir Azure Storage kuyruğuna geldiklerinde toomessages yanıt. Bir örnek için bkz: [tooan Azure hizmeti bağlar bir Azure işlevi oluşturma](functions-create-an-azure-connected-function.md).
* **ServiceBusQueueTrigger** -Azure Hizmetleri veya hizmetleri dinleme toomessage kuyrukları ile şirket içi, kod tooother bağlanın. 
* **ServiceBusTopicTrigger** -Azure Hizmetleri veya hizmetleri tootopics abone olarak şirket içi, kod tooother bağlanın. 
* **TimerTrigger** - Önceden tanımlanmış bir zamanlamaya göre temizleme veya diğer toplu işlem görevlerini yürütür. Örnek olarak bkz. [Olay işleme işlevi oluşturma](functions-create-an-event-processing-function.md).

Azure işlevleri destekler *Tetikleyicileri*, hangi toostart yürütme, kodunuzu yollarıdır ve *bağlamaları*, hangi olan yollar toosimplify kodlama için girdi ve çıktı verileri. Merhaba tetikleyiciler ve Azure işlevlerinin sağladığı bağlamaları ayrıntılı açıklaması için bkz: [Azure işlevleri Tetikleyicileri ve bağlamaları Geliştirici Başvurusu](functions-triggers-bindings.md).

## <a name="integrations"></a>Tümleştirmeler
Azure İşlevleri, çeşitli Azure ve üçüncü taraf hizmetleri ile tümleştirilebilir. Bu hizmetler, işlevinizi tetikleyip yürütmeyi başlatabilir ya da kodunuz için giriş ve çıkış görevi görebilir. Merhaba aşağıdaki hizmet tümleştirmeleri Azure işlevleri tarafından desteklenir. 

* Azure Cosmos DB
* Azure Event Hubs 
* Azure Mobile Apps (tablolar)
* Azure Notification Hubs
* Azure Service Bus (kuyruklar ve konu başlıkları)
* Azure Storage (blob, kuyruklar ve tablolar) 
* GitHub (web kancaları)
* Şirket içi (Service Bus kullanarak)
* Twilio (SMS mesajları)

## <a name="pricing"></a>İşlevlerin maliyeti ne kadardır?
Azure işlevleri planları fiyatlandırma iki tür vardır, hello gereksinimlerine en uygun birini seçin: 

* **Tüketim planı** - işleviniz çalıştığında, Azure tüm hello gerekli hesaplama kaynaklarını sağlar. Kaynak yönetimi hakkında tooworry yoktur ve yalnızca kodunuzun çalıştığı hello zaman için ödeme yaparsınız. 
* **App Service planı** - İşlevlerinizi web, mobil ve API uygulamalarınız gibi çalıştırın. Diğer uygulamalar için uygulama hizmeti kullanıyor olmanız halinde işlevlerinizi hello aynı hiçbir ek ücret planı çalıştırabilirsiniz. 

Tüm fiyatlandırma ayrıntıları hello üzerinde kullanılabilir [işlevler Fiyatlandırma sayfasında](https://azure.microsoft.com/pricing/details/functions/). İşlevlerinizi ölçeklendirme hakkında daha fazla bilgi için bkz: [nasıl tooscale Azure işlevleri](functions-scale.md).

## <a name="next-steps"></a>Sonraki Adımlar
* [İlk Azure İşlevinizi oluşturma](functions-create-first-azure-function.md)  
  Hemen ve hello Azure işlevleri hızlı başlangıcını kullanarak ilk işlevinizi oluşturun. 
* [Azure İşlevleri geliştirici başvurusu](functions-reference.md)  
  İşlevleri kodlamak ve tetikleyicileri ve bağlamaları tanımlamak için hello Azure işlevleri çalışma zamanı ve başvurusu hakkında daha fazla teknik bilgi sağlar.
* [Azure İşlevlerini test etme](functions-test-a-function.md)  
  İşlevlerinizi test etmek için çeşitli araçları ve teknikleri açıklar.
* [Nasıl tooscale Azure işlevleri](functions-scale.md)  
  Merhaba tüketim barındırma planı ve nasıl toochoose hello doğru planın dahil olmak üzere Azure işlevlerinde kullanılabilen hizmet planlarını açıklanır. 
* [Azure Uygulama Hizmeti hakkında daha fazla bilgi edinin](../app-service/app-service-value-prop-what-is.md)  
  Azure işlevleri hello Azure App Service platformu dağıtımlar, ortam değişkenleri ve tanılama gibi temel işlevler için yararlanır. 

