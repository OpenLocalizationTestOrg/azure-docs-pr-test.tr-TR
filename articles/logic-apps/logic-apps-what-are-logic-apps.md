---
title: "aaaConnect uygulamaları ve iş akışları ile - Azure Logic Apps veri tümleştirme | Microsoft Docs"
description: "Azure Logic Apps ile uygulamaları bağlayıp verileri tümleştirerek iş akışları oluşturun ve işlemleri otomatik hale getirin."
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 07765c05-72a6-4169-a8ab-f6420bfbaf07
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/23/2017
ms.author: klam
ms.openlocfilehash: 53d4e165bb2205ddd56c1950719389725267ddea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-logic-apps"></a>Logic Apps nedir?
Logic Apps şekilde toosimplify sağlayın ve ölçeklenebilir tümleştirme ve iş akışları hello bulutta uygular. Görsel Tasarımcı toomodel sağlar ve işleminizi iş akışı olarak bilinen adımları bir dizi olarak otomatikleştirmek.  Vardır [birçok Bağlayıcılar](../connectors/apis-list.md) hizmetler ve protokoller hello Bulut ve şirket içi tooquickly arasında tümleştirme.  Bir mantıksal uygulama tetikleyicisi'yle ('bir hesap tooDynamics CRM eklendiğinde' like) başlar ve sonra Eylemler, dönüştürme ve koşul mantığı birçok birleşimleri tetikleme başlayabilirsiniz.

Logic Apps kullanmanın yararları hello hello şunları içerir:  

* Kolay toounderstand tasarım araçlarını kullanarak karmaşık işlemlere tasarlayarak zaman kaydetme
* Desenleri ve iş akışları sorunsuz bir şekilde uygulanması, aksi takdirde kodda zor tooimplement olacaktır
* Şablonlardan hızlı bir şekilde çalışmaya başlama
* Mantıksal uygulamanızı kendi özel API'leriniz, kodunuz ve eylemlerinizle özelleştirme
* Bağlanma ve şirket farklı sistemleri senkronize ve bulut hello
* BizTalk server, API Management, Azure İşlevleri ve Azure Service Bus’ı birinci sınıf tümleştirme desteği ile derleme

Logic Apps olan tam olarak yönetilen iPaaS (hizmet olarak Platform tümleştirme) geliştiriciler değil barındırma, ölçeklenebilirlik, kullanılabilirlik ve yönetim oluşturma konusunda toohave tooworry izin verme.  Logic Apps toomeet talebi otomatik olarak ölçeklendirir.

![Akış uygulama tasarımcısı](media/logic-apps-what-are-logic-apps/LogicAppCapture2.png)

Daha önce bahsedildiği gibi Logic Apps ile iş süreçlerini otomatik hale getirebilirsiniz. Aşağıda birkaç örnek verilmiştir:  

* Karşıya yüklenen dosyaların tooan FTP sunucusu Azure depolama alanına taşıma
* Şirket işi ve bulut sistemlerinde siparişleri işleme ve yönlendirme
* Belirli bir konuda hakkında tüm tweetler izlemek, hello düşünceleri çözümlemek ve uyarıları ve izleme gerek öğeleri için Görevler oluşturun.

Bunlar gibi senaryoların tümü hello görsel tasarımcı ve tek satırlık bir kod yazmayı olmadan yapılandırılabilir. [Mantıksal uygulamanızı derlemeye][create] hemen başlayın.  Mantıksal uygulama yazıldıktan sonra birden fazla ortam ve bölgeye [hızlı bir şekilde dağıtılabilir ve yeniden yapılandırılabilir](../logic-apps/logic-apps-create-deploy-template.md).

## <a name="why-logic-apps"></a>Logic Apps neden kullanılmalıdır?
Logic Apps hızı ve ölçeklenebilirlik hello Kurumsal tümleştirme alanına getirir.  Merhaba hello Tasarımcısı çeşitli kullanılabilir tetikleyiciler ve Eylemler ve güçlü Yönetim Araçları'nın kullanım kolaylığı olun zamankinden daha basit Apı'lerinizi merkezileştirme.  İşletmeler digitalization doğru ilerlerken, Logic Apps tooconnect eski ve modern sistemleri birlikte sağlar.

Ayrıca, ile bizim [kuruluş tümleştirme hesabı] [ biztalk] toomature tümleştirme senaryolarına hello gücünü ölçeklendirebilirsiniz bir [XML ileti] [ xml], [ticari ortak Yönetimi][tpm]ve daha fazlası.

* **Kolay toouse Tasarım araçları** -Logic Apps tasarlanmış uçtan uca hello tarayıcıda veya Visual Studio Araçları ile olabilir. Tetikleyiciden - GitHub sorunu oluşturulan bir basit zamanlama toowhen başlayın. Daha sonra Eylemler hello zengin bağlayıcı galerisini kullanarak herhangi bir sayıda yönetirler.
* **API'ları kolayca bağlanabilir** -kolay toodescribe olan oluşturma görevlerinin bile olan kod zor tooimplement. Logic Apps farklı sistemleri kolay tooconnect kolaylaştırır. Bulut çözüm pazarlama tooconnect istediğiniz tooyour şirket içi faturalama sistemi? API'ler ve sistemleri ile bir kurumsal hizmet veri yolu üzerinden ileti toocentralize istiyorsunuz? Logic apps hello hızlı ve en güvenilir yolu toodeliver çözümleri toothese sorunlardır.
* **Şablonlardan hızlıca başlayın** -başlamanıza toohelp sunulmuştur bir [Şablon Galerisi] [ templates] olanak tanıyacak şekilde toorapidly bazı yaygın çözümleri oluşturun. Gelen B2B çözümlerini toosimple SaaS bağlantısına, Gelişmiş ve hatta birkaç olan 'eğlencelik için' - hello galeri hello en hızlı yolu tooget Logic Apps hello güç ile başlatıldı.
* **Desteklenmiş genişletilebilirlik** -ihtiyacınız hello bağlayıcı göremiyorum? Logic Apps API'leri ve kod tasarlanmış toowork olur; kolayca, kendi API uygulaması toouse özel bir bağlayıcı olarak oluşturabilir veya çağırmak bir [Azure işlevi](https://functions.azure.com) tooexecute parçacıkları talep kodu. 
* **Gerçek tümleştirme gücü** - Basitten başlayın ve gerektikçe büyütün. Logic Apps, BizTalk, gereksinim duydukları Microsoft'un sektör başında tümleştirme çözüm tooenable tümleştirme uzmanları toobuild hello çözümleri hello gücünü kolayca yararlanabilirsiniz. Merhaba hakkında daha fazla bilgi [Kurumsal tümleştirme paketi](../logic-apps/logic-apps-enterprise-integration-overview.md).

## <a name="logic-app-concepts"></a>Mantıksal Uygulama Kavramları
Merhaba hello Logic Apps deneyimini oluşturan hello temel parçalar bazıları verilmiştir. 

* **İş akışı** -Logic Apps İş süreçlerinizi grafiksel toomodel bir dizi adım veya bir iş akışı sağlar.
* **Bağlayıcılar yönetilen** -logic apps toodata ve hizmetlerine erişmek. Yönetilen bağlayıcıların özellikle tooaid oluşturulur, verilerinizle çalışırken tooand bağlanırken. Bağlayıcılar anda kullanılabilen Hello listesini [yönetilen bağlayıcıların][managedapis].
* **Tetikleyiciler** - Bazı Yönetilen Bağlayıcılar tetikleyici olarak da hareket edebilir. Bir tetikleyici bir e-posta veya Azure Storage hesabınızdaki bir değişiklik hello varış gibi belirli bir olaya göre bir iş akışının yeni bir örneğini başlatır.
* **Eylemler** -hello tetikleyici bir iş akışında bir eylem çağrıldıktan sonra her adımı. Her eylem genellikle yönetilen Bağlayıcısı veya özel API uygulamaları tooan işlemi eşler.
* **Enterprise Integration Pack** - Daha gelişmiş tümleştirme senaryoları için Logic Apps, BizTalk özelliklerini içerir. BizTalk, Microsoft'un sektör lideri tümleştirme platformudur. Merhaba Enterprise Integration Pack bağlayıcılar izin tooeasily doğrulama, dönüştürme ve tooyour mantıksal uygulama iş akışlarında daha fazla bilgi içerir.

## <a name="getting-started"></a>Başlarken
* Logic Apps ile başlatılan tooget izleyin hello [mantıksal uygulama oluşturma] [ create] Öğreticisi.  
* [Sık rastlanan örnekleri ve senaryoları inceleyin](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Logic Apps ile iş süreçlerini otomatik hale getirebilirsiniz](http://channel9.msdn.com/Events/Build/2016/T694) 
* [Bilgi nasıl tooIntegrate sistemlerinizi Logic Apps ile](http://channel9.msdn.com/Events/Build/2016/P462)

[biztalk]: logic-apps-enterprise-integration-accounts.md
[appservice]: ../app-service/app-service-value-prop-what-is.md
[create]: logic-apps-create-a-logic-app.md
[managedapis]: ../connectors/apis-list.md
[tpm]: logic-apps-enterprise-integration-accounts.md
[xml]: logic-apps-enterprise-integration-b2b.md
[templates]: logic-apps-use-logic-app-templates.md
