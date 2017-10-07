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
# <a name="add-a-java-application-tooazure-app-service-web-apps"></a><span data-ttu-id="7101c-103">Java uygulama tooAzure App Service Web Apps ekleme</span><span class="sxs-lookup"><span data-stu-id="7101c-103">Add a Java application tooAzure App Service Web Apps</span></span>
<span data-ttu-id="7101c-104">Java web uygulamanıza başlatıldıktan sonra [Azure App Service] [ Azure App Service] adresinde belgelenen gibi [Azure App Service'te bir Java web uygulaması oluşturma](web-sites-java-get-started.md), koyarak uygulamanızı karşıya yükleyebilirsiniz Başlangıç olarak, WAR **webapps** klasör.</span><span class="sxs-lookup"><span data-stu-id="7101c-104">Once you have initialized your Java web app in [Azure App Service][Azure App Service] as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md), you can upload your application by placing your WAR in hello **webapps** folder.</span></span>

<span data-ttu-id="7101c-105">Gezinti yolu toohello hello **webapps** klasör Web Apps örneğinizi nasıl ayarladığınıza göre değişir.</span><span class="sxs-lookup"><span data-stu-id="7101c-105">hello navigation path toohello **webapps** folder differs based on how you set up your Web Apps instance.</span></span>

* <span data-ttu-id="7101c-106">Web uygulamanızı hello Azure Marketi kullanarak ayarlarsanız, yol toohello hello **webapps** klasördür hello formunda **d:\home\site\wwwroot\bin\application\_server\webapps**, burada **uygulama\_server** hello hello uygulama sunucusu Web Apps Örneğiniz için yürürlükte adıdır.</span><span class="sxs-lookup"><span data-stu-id="7101c-106">If you set up your web app by using hello Azure Marketplace, hello path toohello **webapps** folder is in hello form **d:\home\site\wwwroot\bin\application\_server\webapps**, where **application\_server** is hello name of hello application server in effect for your Web Apps instance.</span></span> 
* <span data-ttu-id="7101c-107">Web uygulamanızı hello Azure yapılandırma kullanıcı Arabirimi kullanarak ayarlarsanız, yol toohello hello **webapps** klasördür hello formunda **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="7101c-107">If you set up your web app by using hello Azure configuration UI, hello path toohello **webapps** folder is in hello form **d:\home\site\wwwroot\webapps**.</span></span> 

<span data-ttu-id="7101c-108">Uygulama ya da dahil olmak üzere web sayfaları, kaynak denetimi tooupload kullanabileceğinizi unutmayın [sürekli tümleştirme senaryolarına](app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="7101c-108">Note that you can use source control tooupload your application or web pages, including [continuous integration scenarios](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="7101c-109">FTP, ayrıca uygulama veya web sayfalarından karşıya yükleme için bir seçenektir; FTP üzerinden uygulamalarınızı dağıtma hakkında daha fazla bilgi için bkz: [, uygulama tooAzure uygulama hizmeti dağıtmak].</span><span class="sxs-lookup"><span data-stu-id="7101c-109">FTP is also an option for uploading your application or web pages; for more information about deploying your applications over FTP, see [Deploy your app tooAzure App Service].</span></span>

<span data-ttu-id="7101c-110">Tomcat web uygulamaları için Not: WAR dosyası toohello yüklediğiniz sonra **webapps** klasörü, hello Tomcat uygulama sunucusu bunu eklemiş ve otomatik olarak algılar.</span><span class="sxs-lookup"><span data-stu-id="7101c-110">Note for Tomcat web apps: Once you've uploaded your WAR file toohello **webapps** folder, hello Tomcat application server will detect that you've added it and will automatically load it.</span></span> <span data-ttu-id="7101c-111">Dosyaları (dışında WAR dosyaları) toohello kök dizini kopyalarsanız, hello uygulama sunucusu bu dosyaları kullanılmadan önce yeniden toobe gerektiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="7101c-111">Note that if you copy files (other than WAR files) toohello ROOT directory, hello application server will need toobe restarted before those files are used.</span></span> <span data-ttu-id="7101c-112">Azure üzerinde çalışan hello Tomcat Java web uygulamaları için Hello autoload işlevselliği eklenmekte olan yeni bir WAR dosyası üzerinde temel ya da yeni dosya veya dizinlerin eklenen toohello **webapps** klasör.</span><span class="sxs-lookup"><span data-stu-id="7101c-112">hello autoload functionality for hello Tomcat Java web apps running on Azure is based on a new WAR file being added, or new files or directories added toohello **webapps** folder.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="7101c-113">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="7101c-113">See Also</span></span>
<span data-ttu-id="7101c-114">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi].</span><span class="sxs-lookup"><span data-stu-id="7101c-114">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

[<span data-ttu-id="7101c-115">Application-insights-App-insights-Java-Get-Started</span><span class="sxs-lookup"><span data-stu-id="7101c-115">application-insights-app-insights-java-get-started</span></span>](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[, uygulama tooAzure uygulama hizmeti dağıtmak]: ./web-sites-deploy.md
