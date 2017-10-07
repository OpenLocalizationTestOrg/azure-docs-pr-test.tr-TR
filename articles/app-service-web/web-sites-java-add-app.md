---
title: "aaaAdd bir Java uygulaması tooAzure App Service Web Apps"
description: "Bu öğreticide tooadd bir sayfa veya uygulama tooyour örneği zaten Azure App Service Web Apps toouse Java nasıl yapılandırılacağı gösterilmiştir."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9b46528b-e2d0-4f26-b8d7-af94bd8c31ef
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 2feb464b2933921ad2887779a6b7589634e2e2f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-java-application-tooazure-app-service-web-apps"></a>Java uygulama tooAzure App Service Web Apps ekleme
Java web uygulamanıza başlatıldıktan sonra [Azure App Service] [ Azure App Service] adresinde belgelenen gibi [Azure App Service'te bir Java web uygulaması oluşturma](web-sites-java-get-started.md), koyarak uygulamanızı karşıya yükleyebilirsiniz Başlangıç olarak, WAR **webapps** klasör.

Gezinti yolu toohello hello **webapps** klasör Web Apps örneğinizi nasıl ayarladığınıza göre değişir.

* Web uygulamanızı hello Azure Marketi kullanarak ayarlarsanız, yol toohello hello **webapps** klasördür hello formunda **d:\home\site\wwwroot\bin\application\_server\webapps**, burada **uygulama\_server** hello hello uygulama sunucusu Web Apps Örneğiniz için yürürlükte adıdır. 
* Web uygulamanızı hello Azure yapılandırma kullanıcı Arabirimi kullanarak ayarlarsanız, yol toohello hello **webapps** klasördür hello formunda **d:\home\site\wwwroot\webapps**. 

Uygulama ya da dahil olmak üzere web sayfaları, kaynak denetimi tooupload kullanabileceğinizi unutmayın [sürekli tümleştirme senaryolarına](app-service-continuous-deployment.md). FTP, ayrıca uygulama veya web sayfalarından karşıya yükleme için bir seçenektir; FTP üzerinden uygulamalarınızı dağıtma hakkında daha fazla bilgi için bkz: [, uygulama tooAzure uygulama hizmeti dağıtmak].

Tomcat web uygulamaları için Not: WAR dosyası toohello yüklediğiniz sonra **webapps** klasörü, hello Tomcat uygulama sunucusu bunu eklemiş ve otomatik olarak algılar. Dosyaları (dışında WAR dosyaları) toohello kök dizini kopyalarsanız, hello uygulama sunucusu bu dosyaları kullanılmadan önce yeniden toobe gerektiğine dikkat edin. Azure üzerinde çalışan hello Tomcat Java web uygulamaları için Hello autoload işlevselliği eklenmekte olan yeni bir WAR dosyası üzerinde temel ya da yeni dosya veya dizinlerin eklenen toohello **webapps** klasör. 

<a name="see-also"></a>

## <a name="see-also"></a>Ayrıca Bkz.
Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi].

[Application-insights-App-insights-Java-Get-Started](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[, uygulama tooAzure uygulama hizmeti dağıtmak]: ./web-sites-deploy.md
