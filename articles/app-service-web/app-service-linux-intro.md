---
title: "aaaIntroduction tooAzure Linux üzerinde Web uygulaması | Microsoft Docs"
description: "Linux üzerinde Azure Web uygulaması hakkında bilgi edinin."
keywords: Azure uygulama hizmeti, linux, oss
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: bc85eff6-bbdf-410a-93dc-0f1222796676
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 43b9865ade251909a77429eb3e18fe0bcaac3bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-web-app-on-linux"></a>Giriş tooAzure Linux üzerinde Web uygulaması

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>Genel Bakış
Müşterilerin Web uygulaması için desteklenen uygulama yığınları Linux toohost web uygulamalarını Linux üzerinde yerel olarak kullanabilirsiniz. Merhaba aşağıdaki bölümde şu anda desteklenen hello uygulama yığınları listelenmektedir. 

## <a name="features"></a>Özellikler
Web uygulaması Linux üzerinde şu anda uygulama yığınları aşağıdaki hello destekler:

* Node.js
    * 4.4
    * 4.5
    * 6.2
    * 6.6
    * 6.9
    * 6.10
    * 6.11
    * 8.0
    * 8.1
* PHP
    * 5.6
    * 7.0
* .NET core
    * 1.0
    * 1.1
* Ruby
    * 2.3

Müşterilerin kendi uygulamalarında kullanarak dağıtabilirsiniz:

* FTP
* Yerel Git
* GitHub
* Bitbucket

Uygulama ölçeklendirme için:

* Müşterilerin web uygulamaları yukarı ve aşağı App Service planlarına hello katmanını değiştirerek ölçeği
* Müşterilerin uygulamalarının ölçekleme ve birden çok uygulama örneğini hello sınırlar içinde kendi SKU çalıştırın

Kudu için bazı hello temel işlevlerini:

* Ortamlar
* Dağıtımlar
* Temel konsol
* SSH

Devops için:

* Hazırlık ortamları
* ACR ve DockerHub CI/CD

## <a name="limitations"></a>Sınırlamalar
Hello Azure portal Linux üzerinde Web uygulaması için şu anda iş yalnızca özelliklerini gösterir ve hello rest gizler. Daha fazla özellik etkinleştirme gibi hello portalda görünür olacaktır.

Sanal ağ tümleştirmesinin, Azure Active Directory/üçüncü taraf kimlik doğrulama veya Kudu site uzantıları gibi bazı özellikler henüz kullanılabilir değil. Bu özellikler kullanılabilir olduktan sonra bizim belgelerini ve blogu hello değişiklikler hakkında güncelleştireceğiz.

Bu genel önizlemesi şu anda yalnızca bölgeleri aşağıdaki hello kullanılabilir:

* Batı ABD
* Doğu ABD
* Batı Avrupa
* Kuzey Avrupa
* Orta Güney ABD
* Orta Kuzey ABD
* Güneydoğu Asya
* Doğu Asya
* Avustralya Doğu
* Japonya Doğu
* Güney Brezilya
* Güney Hindistan

Web uygulamaları Linux'ta hello ayrılmış uygulama hizmeti planlarında yalnızca desteklenir ve ücretsiz veya paylaşılan bir katmanı yok. Ayrıca, Linux olmayan uygulama hizmeti planında Linux web uygulaması oluşturamıyor normal ve Linux web uygulamaları için uygulama hizmeti planları karşılıklı olarak birbirini dışlar.

Web uygulamaları Linux üzerinde oluşturulan, Linux olmayan web uygulamaları hello içermeyen bir kaynak grubunda aynı bölgede.

## <a name="troubleshooting"></a>Sorun giderme ##

Uygulamanızı toostart başarısız veya uygulamanızdan toocheck hello günlük istediğiniz, Docker hello LogFiles dizinde oturum hello denetleyin. SCM siteniz veya FTP aracılığıyla bu dizine erişebilir.
toolog hello `stdout` ve `stderr` tooenable gerekir, kapsayıcıdan **Docker kapsayıcısı günlük** altında **tanılama günlükleri**.

![Günlüğü etkinleştirme][2]

![Kudu tooview Docker günlüklerini kullanma][1]

Merhaba SCM sitesinden erişebilirsiniz **Gelişmiş Araçlar** hello içinde **geliştirme araçları** menüsü.

## <a name="next-steps"></a>Sonraki adımlar
Uygulama hizmeti Linux'ta kullanmaya bağlantılar tooget aşağıdaki hello bakın. Hakkında sorular ve sorunları nakledebilirsiniz [forumumuzda](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).

* [Linux üzerinde Azure Web uygulaması için nasıl toouse özel Docker görüntü](app-service-linux-using-custom-docker-image.md)
* [Linux üzerinde Azure Web uygulamasında Node.js için PM2 Yapılandırması'nı kullanarak](app-service-linux-using-nodejs-pm2.md)
* [.NET Core Linux Azure App Service Web uygulamasında kullanma](app-service-linux-using-dotnetcore.md)
* [Azure App Service Web uygulaması Linux'ta Ruby kullanma](app-service-linux-ruby-get-started.md)
* [Azure App Service Web uygulaması Linux SSS](app-service-linux-faq.md)
* [Linux üzerinde Azure Web uygulaması için SSH desteği](./app-service-linux-ssh-support.md)
* [Hazırlık Azure App Service ortamları ayarlama](./web-sites-staged-publishing.md)
* [Docker hub'a sürekli dağıtım Linux Azure Web uygulaması](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png