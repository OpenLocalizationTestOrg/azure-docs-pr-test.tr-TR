---
title: aaaAbout Azure App Service'de Mobile Apps
description: "App Service mobile apps tooyour Kurumsal getirir Hello avantajları hakkında bilgi edinin."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: 4e96cb9d-a632-4cf6-8219-0810d8ade3f9
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-multiple
ms.devlang: na
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: ab96af11c3df196acfb9ecec1339e7f6093c7066
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started"> </a>Azure Uygulama Hizmetinde Mobile Apps Hakkında
Azure Uygulama Hizmeti, profesyonel geliştiricilere yönelik tam olarak yönetilen bir [hizmet olarak platform](https://azure.microsoft.com/overview/what-is-paas/) (PaaS) teklifidir. Merhaba hizmet tooweb, mobil ve tümleştirme senaryoları zengin bir özellikler kümesi getirir. 

Azure App Service Mobile Apps özelliğini Merhaba, Kurumsal geliştiriciler ve yüksek düzeyde ölçeklenebilir ve genel olarak kullanılabilir sistem tümleştiricileri mobil uygulama geliştirme platformu sunar.

![Mobile Apps özelliklerine görsel bir genel bakış](./media/app-service-mobile-value-prop/overview.png)

## <a name="why-mobile-apps"></a>Neden Mobile Apps?
Merhaba Mobile Apps özelliği ile şunları yapabilirsiniz:

* **Yerel ve platformlar arası uygulamaları oluşturma**: Hem yerel iOS, Android ve Windows uygulamaları hem de platformlar arası Xamarin veya Cordova (Phonegap) uygulamaları oluştururken yerel SDK'ları kullanarak App Service’in avantajlarından faydalanabilirsiniz.
* **Tooyour Kurumsal sistemler bağlanmak**: hello Mobile Apps özelliğini ile Kurumsal oturum açma dakika cinsinden ekleyebilir ve tooyour Kurumsal şirket içi bağlanmak veya Bulut kaynaklarına.
* **Veri Eşitleme ile çevrimdışı kullanılmaya hazır uygulamalar oluşturma**: Çevrimdışı Çalış uygulamalar oluşturarak, mobil iş gücünüzü üretken olun ve bağlantı tüm kurumsal veri kaynaklarınız varsa Mobile Apps toosync veri hello arka planda kullanın veya yazılım (SaaS) API'leri hizmet olarak.
* **Anında iletme bildirimleri toomillions saniye cinsinden**: herhangi bir cihazda anında iletme bildirimleriyle müşterilerinizle kişiselleştirilmiş tootheir gereksinimlerini ve başlangıç saati doğru olduğunda gönderilen göster.

## <a name="mobile-apps-features"></a>Mobile Apps özellikleri
özellikler aşağıdaki hello önemli toocloud etkin mobil geliştirme şunlardır:

* **Kimlik doğrulama ve yetkilendirme**: Azure Active Directory dahil, sürekli büyüyen bir kurumsal kimlik sağlayıcısı listesinden ve Facebook, Google, Twitter ve Microsoft Hesabı gibi sosyal sağlayıcılardan seçim yapın. Mobile Apps tüm sağlayıcılar için bir OAuth 2.0 hizmeti sunar. Ayrıca, sağlayıcıya özgü işlevselliği hello kimlik sağlayıcısı için SDK hello tümleştirebilirsiniz.

    [Kimlik doğrulama özelliklerimiz] hakkında daha fazlasını keşfedin.

* **Veri erişimi**: mobil uygulamaları tooAzure SQL veritabanı veya bir şirket içi SQL server bağlantılı içeren bir mobil kullanımı kolay OData v3 veri kaynağı sağlar. Bu hizmet, [Azure Tablo depolama], MongoDB ve [Azure Cosmos DB]’nin yanı sıra Office 365 ve Salesforce.com gibi SaaS API’si sağlayıcıları dahil, diğer NoSQL ve SQL veri sağlayıcılarıyla kolayca tümleştirmenizi sağlayarak Entity Framework’ü temel alabilir.

* **Çevrimdışı eşitleme**: İstemci SDK ile çevrimdışı bir veri kümesini çalışması kolay toobuild sağlam ve esnek mobil uygulamalar kolaylaştırır. Bu veri kümesini verilerle çakışma çözümü desteği dahil olmak üzere otomatik olarak hello arka uç, eşitleyebilirsiniz.

  [veri özellikleri] hakkında daha fazlasını keşfedin.

* **Anında iletme bildirimleri**: İstemci SDK tümleştirmenize sorunsuz bir şekilde hello kayıt özelliklerini Azure Notification Hubs ile anında iletme bildirimleri toomillions kullanıcı aynı anda gönderebilmek için.

  [anında iletme bildirimi özellikleri] hakkında daha fazlasını keşfedin.

* **İstemci SDK'ları**: Yerel geliştirmeyi ([iOS], [Android] ve [Windows]), platformlar arası geliştirmeyi ([Xamarin.iOS ve Xamarin.Android], [Xamarin.Forms]) ve karma uygulama geliştirmeyi ([Apache Cordova]) kapsayan SDK'ların eksiksiz bir kümesini sunuyoruz  Her istemci SDK’sı ile bir MIT lisansı ile birlikte sunulur ve açık kaynaklıdır.

## <a name="azure-app-service-features"></a>Azure Uygulama Hizmeti özellikleri
Platform özellikleri aşağıdaki hello mobil üretim siteleri için yararlıdır:

* **Otomatik ölçeklendirmeyi**: uygulama hizmeti ile kolaylıkla ölçeği veya toohandle, gelen müşteri yükünü ölçeklendirin. El ile Merhaba sayısını ve boyutunu VM'ler seçin veya yükleme ya da zamanlama temelinden, mobil uygulama arka ucu otomatik ölçeklendirmeyi tooscale ayarlayın.

  [Otomatik ölçeklendirme] hakkında daha fazlasını keşfedin.

* **Hazırlık ortamları**: App Service, yeni arka ucun daha büyük bir DevOps planının parçası olarak test olan A/B testini ve yerinde hazırlanmasını gerçekleştirmenizi sağlayarak, sitenizin birden fazla sürümünü çalıştırabilir.

  [hazırlık ortamları] hakkında daha fazlasını keşfedin.

* **Sürekli dağıtım**: App Service, SCM sisteminizin tooa dalı ileterek arka uç yeni bir sürümü otomatik olarak dağıtabilmek için ortak tedarik zinciri yönetimi (SCM) sistemleri ile tümleştirebilir.

  [dağıtım seçenekleri] hakkında daha fazlasını keşfedin.

* **Sanal ağ**: App Service, sanal ağ, Azure ExpressRoute ya da karma bağlantılar kullanarak tooon içi kaynaklara bağlanabilir.

  [karma bağlantılar], [sanal ağlar], ve [ExpressRoute] hakkında daha fazlasını keşfedin.

* **Yalıtılmış ve ayrılmış ortamlar**: App Service, Azure Uygulama Hizmeti uygulamalarını yüksek ölçekte güvenli bir şekilde çalıştırılmaları için tam yalıtılmış ve ayrılmış bir ortamda çalıştırılabilir. Bu ortam, büyük ölçekli, yalıtım veya güvenli ağ erişimi gerektiren uygulama iş yükleri için idealdir.

  [App Service ortamları] hakkında daha fazlasını öğrenin.

## <a name="next-steps"></a>Sonraki adımlar

Azure uygulama hizmetinde tam hello mobil uygulamaları ile çalışmaya tooget [Başlarken] Öğreticisi. Başlangıç Öğreticisi hello temelleri mobil geri bitiş oluşturan ve istemci tercih ettiğiniz kapsar. Ayrıca kimlik doğrulama, çevrimdışı eşitleme ve anında iletme bildirimlerini tümleştirme konularını ele alır. Başlangıç Öğreticisi birden çok kez kez her istemci uygulaması için tamamlayabilirsiniz.

Mobile Apps hakkında daha fazla bilgi için [öğrenme haritamızı] gözden geçirin.
Hello Azure App Service platformu hakkında daha fazla bilgi için bkz: [Azure App Service].

<!-- URLs. -->
[Migrate your mobile service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[Azure App Service]: ../app-service/app-service-value-prop-what-is.md
[Başlarken]: app-service-mobile-ios-get-started.md
[Azure Tablo depolama]:../cosmos-db/table-storage-how-to-use-dotnet.md
[Azure Cosmos DB]: ../cosmos-db/documentdb-get-started.md
[Kimlik doğrulama özelliklerimiz]: ./app-service-mobile-auth.md
[veri özellikleri]: ./app-service-mobile-offline-data-sync.md
[anında iletme bildirimi özellikleri]: ../notification-hubs/notification-hubs-push-notification-overview.md
[iOS]: ./app-service-mobile-ios-how-to-use-client-library.md
[Android]: ./app-service-mobile-android-how-to-use-client-library.md
[Windows]: ./app-service-mobile-dotnet-how-to-use-client-library.md
[Xamarin.iOS ve Xamarin.Android]: ./app-service-mobile-dotnet-how-to-use-client-library.md
[Xamarin.Forms]: ./app-service-mobile-xamarin-forms-get-started.md
[Apache Cordova]: ./app-service-mobile-cordova-how-to-use-client-library.md
[Otomatik ölçeklendirme]: ../app-service-web/web-sites-scale.md
[hazırlık ortamları]: ../app-service-web/web-sites-staged-publishing.md
[dağıtım seçenekleri]: ../app-service-web/web-sites-deploy.md
[karma bağlantılar]: ../app-service-web/web-sites-hybrid-connection-get-started.md
[sanal ağlar]: ../app-service-web/web-sites-integrate-with-vnet.md
[ExpressRoute]: ../app-service-web/app-service-app-service-environment-network-configuration-expressroute.md
[App Service ortamları]: ../app-service-web/app-service-app-service-environment-intro.md
[öğrenme haritamızı]: https://azure.microsoft.com/en-us/documentation/learning-paths/appservice-mobileapps/
