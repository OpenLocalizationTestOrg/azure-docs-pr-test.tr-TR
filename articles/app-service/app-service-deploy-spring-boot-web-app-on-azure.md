---
title: "aaaDeploy yay önyükleme uygulama toohello Azure App Service | Microsoft Docs"
description: "Bu öğretici, başlangıç adımları toodeploy hello yay önyükleme Başlarken web uygulama tooAzure uygulama hizmeti aracılığıyla geliştiricilerin yol gösterecektir."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.openlocfilehash: 69f9c4903fd740125194402cdb4b4db46a1f2773
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-toohello-azure-app-service"></a><span data-ttu-id="aba80-103">Yay önyükleme uygulama toohello Azure App Service'e dağıtma</span><span class="sxs-lookup"><span data-stu-id="aba80-103">Deploy a Spring Boot Application toohello Azure App Service</span></span>

<span data-ttu-id="aba80-104">Merhaba  **[yay Framework]**  Java geliştiriciler kuruluş düzeyinde uygulamalar oluşturmanıza yardımcı olan bir açık kaynak çözümüdür ve bu platformu üzerine kurulmuştur hello daha popüler projeleri biridir [Yay önyükleme], tek başına Java uygulamaları oluşturmak için basitleştirilmiş bir yaklaşım sağlar.</span><span class="sxs-lookup"><span data-stu-id="aba80-104">hello **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications, and one of hello more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="aba80-105">Bu öğretici ancak hello örnek yay önyükleme Başlarken web uygulaması oluşturma ve çok dağıtma anlatılır[Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="aba80-105">This tutorial will walk you though creating hello sample Spring Boot Getting Started web app and deploying it too[Azure App Service].</span></span>

### <a name="prerequisites"></a><span data-ttu-id="aba80-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="aba80-106">Prerequisites</span></span>

<span data-ttu-id="aba80-107">Sipariş toocomplete hello adımlarda Bu öğreticide, toohave hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="aba80-107">In order toocomplete hello steps in this tutorial, you need toohave hello following:</span></span>

* <span data-ttu-id="aba80-108">Bir Azure aboneliği; bir Azure aboneliği zaten sahip değilseniz, etkinleştirebilir, [MSDN abone Avantajlarınızı] veya kaydolun bir [ücretsiz Azure hesabı].</span><span class="sxs-lookup"><span data-stu-id="aba80-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="aba80-109">Güncel bir [Java Geliştirme Seti (JDK)].</span><span class="sxs-lookup"><span data-stu-id="aba80-109">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="aba80-110">Apache'nın [Maven] aracını (sürüm 3) yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="aba80-110">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="aba80-111">A [Git] istemci.</span><span class="sxs-lookup"><span data-stu-id="aba80-111">A [Git] client.</span></span>

## <a name="create-hello-spring-boot-getting-started-web-app"></a><span data-ttu-id="aba80-112">Merhaba yay önyükleme Başlarken web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="aba80-112">Create hello Spring Boot Getting Started web app</span></span>

<span data-ttu-id="aba80-113">Merhaba aşağıdaki adımlar, gerekli toocreate basit bir yay önyükleme web uygulaması ve yerel olarak test hello adımlarda size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="aba80-113">hello following steps will walk you through hello steps that are required toocreate a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="aba80-114">Bir komut istemi açın ve yerel dizin toohold uygulama ve değişiklik toothat dizin oluşturun; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="aba80-114">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="aba80-115">--ya da--</span><span class="sxs-lookup"><span data-stu-id="aba80-115">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="aba80-116">Kopya hello [yay önyükleme Başlarken] örnek proje hello dizinine yeni oluşturduğunuz; örneğin:</span><span class="sxs-lookup"><span data-stu-id="aba80-116">Clone hello [Spring Boot Getting Started] sample project into hello directory you just created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. <span data-ttu-id="aba80-117">Dizin tamamlandı toohello proje Değiştir; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="aba80-117">Change directory toohello completed project; for example:</span></span>
   ```
   cd gs-spring-boot
   cd complete
   ```

1. <span data-ttu-id="aba80-118">Maven kullanarak hello JAR dosyasını oluşturun; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="aba80-118">Build hello JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="aba80-119">Merhaba web uygulaması oluşturulduktan sonra dizin toohello JAR dosyasını değiştirin ve hello web uygulaması başlatın; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="aba80-119">Once hello web app has been created, change directory toohello JAR file and start hello web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. <span data-ttu-id="aba80-120">Bir web tarayıcısı kullanarak toohttp://localhost:8080 göz atarak Hello web uygulaması test veya curl kullanılabilir varsa aşağıdaki örneğine hello gibi hello sözdizimini kullanın:</span><span class="sxs-lookup"><span data-stu-id="aba80-120">Test hello web app by browsing toohttp://localhost:8080 using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="aba80-121">Görüntülenen iletiden hello görmeniz gerekir: **Tebrikler İlkbahar önyüklemesinden!**</span><span class="sxs-lookup"><span data-stu-id="aba80-121">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Örnek uygulaması Gözat][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a><span data-ttu-id="aba80-123">Java ile kullanmak için bir Azure web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="aba80-123">Create an Azure web app for use with Java</span></span>

<span data-ttu-id="aba80-124">Aşağıdaki adımları hello Azure Web uygulaması başlangıç adımları toocreate yol, Java için gerekli hello ayarlarını yapılandırmak ve FTP kimlik bilgilerinizi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="aba80-124">hello following steps will walk you through hello steps toocreate an Azure Web App, configure hello required settings for Java, and configure your FTP credentials.</span></span>

1. <span data-ttu-id="aba80-125">Toohello Gözat [Azure portal] ve oturum açın.</span><span class="sxs-lookup"><span data-stu-id="aba80-125">Browse toohello [Azure portal] and log in.</span></span>

1. <span data-ttu-id="aba80-126">Hello Azure portalı üzerinde hesabınızda oturum açtıktan sonra hello menü simgesini **uygulama hizmetleri**:</span><span class="sxs-lookup"><span data-stu-id="aba80-126">Once you have logged into your account on hello Azure portal, click hello menu icon for **App Services**:</span></span>
   
   ![Azure portalına][AZ01]

1. <span data-ttu-id="aba80-128">Ne zaman hello **uygulama hizmetleri** sayfası görüntülenirse, tıklatın **+ Ekle** toocreate yeni bir uygulama hizmeti.</span><span class="sxs-lookup"><span data-stu-id="aba80-128">When hello **App Services** page is displayed, click **+ Add** toocreate a new App Service.</span></span>

   ![Uygulama hizmeti oluşturma][AZ02]

1. <span data-ttu-id="aba80-130">Web uygulama şablonları Hello listesi gösterildiğinde, hello hello bağlantısına tıklayın temel Microsoft Web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="aba80-130">When hello list of web app templates is displayed, click hello link for hello basic Microsoft Web App.</span></span>

   ![Web Uygulama Şablonları][AZ03]

1. <span data-ttu-id="aba80-132">Merhaba Web uygulaması şablonu için başlangıç bilgileri sayfası görüntülendiğinde tıklayın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="aba80-132">When hello information page for hello Web App template is displayed, click **Create**.</span></span>

   ![Web Uygulaması Oluşturma][AZ04]

1. <span data-ttu-id="aba80-134">Web uygulamanız için benzersiz bir ad sağlayın ve herhangi bir ek ayarları belirtin ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="aba80-134">Provide a unique name for your web app and specify any additional settings, and then **Create**.</span></span>

   ![Web uygulaması ayarları oluşturma][AZ05]

1. <span data-ttu-id="aba80-136">Web uygulamanız oluşturulduktan sonra hello menü simgesini **uygulama hizmetleri**ve yeni oluşturulan web uygulamanız'ye tıklayın:</span><span class="sxs-lookup"><span data-stu-id="aba80-136">Once your web app has been created, click hello menu icon for **App Services**, and then click your newly-created web app:</span></span>

   ![Liste Web uygulamaları][AZ06]

1. <span data-ttu-id="aba80-138">Web uygulamanızı görüntülendiğinde hello Java Sürüm hello aşağıdaki adımları kullanarak belirtin:</span><span class="sxs-lookup"><span data-stu-id="aba80-138">When your web app is displayed, specify hello Java version by using hello following steps:</span></span>

   <span data-ttu-id="aba80-139">a.</span><span class="sxs-lookup"><span data-stu-id="aba80-139">a.</span></span> <span data-ttu-id="aba80-140">Merhaba tıklatın **uygulama ayarları** menü öğesi.</span><span class="sxs-lookup"><span data-stu-id="aba80-140">Click hello **Application Settings** menu item.</span></span>

   <span data-ttu-id="aba80-141">b.</span><span class="sxs-lookup"><span data-stu-id="aba80-141">b.</span></span> <span data-ttu-id="aba80-142">Seçin **Java 8** hello Java sürümü için.</span><span class="sxs-lookup"><span data-stu-id="aba80-142">Choose **Java 8** for hello Java version.</span></span>

   <span data-ttu-id="aba80-143">c.</span><span class="sxs-lookup"><span data-stu-id="aba80-143">c.</span></span> <span data-ttu-id="aba80-144">Seçin **Newest** hello alt Java Sürüm için.</span><span class="sxs-lookup"><span data-stu-id="aba80-144">Choose **Newest** for hello minor Java version.</span></span>

   <span data-ttu-id="aba80-145">d.</span><span class="sxs-lookup"><span data-stu-id="aba80-145">d.</span></span> <span data-ttu-id="aba80-146">Seçin **yeni Tomcat 8.5** hello web kapsayıcısı için.</span><span class="sxs-lookup"><span data-stu-id="aba80-146">Choose **Newest Tomcat 8.5** for hello web container.</span></span> <span data-ttu-id="aba80-147">(Aslında bu kapsayıcı kullanılmaz; Azure hello kapsayıcı yay önyükleme uygulamanızdan kullanır.)</span><span class="sxs-lookup"><span data-stu-id="aba80-147">(This container will not actually be used; Azure will use hello container from your Spring Boot application.)</span></span>

   <span data-ttu-id="aba80-148">e.</span><span class="sxs-lookup"><span data-stu-id="aba80-148">e.</span></span> <span data-ttu-id="aba80-149">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="aba80-149">Click **Save**.</span></span>

   ![Uygulama ayarları][AZ07]

1. <span data-ttu-id="aba80-151">FTP dağıtım kimlik bilgilerinizi hello aşağıdaki adımları kullanarak belirtin:</span><span class="sxs-lookup"><span data-stu-id="aba80-151">Specify your FTP deployment credentials by using hello following steps:</span></span>

   <span data-ttu-id="aba80-152">a.</span><span class="sxs-lookup"><span data-stu-id="aba80-152">a.</span></span> <span data-ttu-id="aba80-153">Merhaba tıklatın **dağıtım kimlik bilgileri** menü öğesi.</span><span class="sxs-lookup"><span data-stu-id="aba80-153">Click hello **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="aba80-154">b.</span><span class="sxs-lookup"><span data-stu-id="aba80-154">b.</span></span> <span data-ttu-id="aba80-155">Kullanıcı adı ve parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="aba80-155">Specify your username and password.</span></span>

   <span data-ttu-id="aba80-156">c.</span><span class="sxs-lookup"><span data-stu-id="aba80-156">c.</span></span> <span data-ttu-id="aba80-157">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="aba80-157">Click **Save**.</span></span>

   ![Dağıtım kimlik bilgilerini belirtin][AZ08]

1. <span data-ttu-id="aba80-159">FTP bağlantı bilgileri hello aşağıdaki adımları kullanarak Al:</span><span class="sxs-lookup"><span data-stu-id="aba80-159">Retrieve your FTP connection information by using hello following steps:</span></span>

   <span data-ttu-id="aba80-160">a.</span><span class="sxs-lookup"><span data-stu-id="aba80-160">a.</span></span> <span data-ttu-id="aba80-161">Merhaba tıklatın **dağıtım kimlik bilgileri** menü öğesi.</span><span class="sxs-lookup"><span data-stu-id="aba80-161">Click hello **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="aba80-162">b.</span><span class="sxs-lookup"><span data-stu-id="aba80-162">b.</span></span> <span data-ttu-id="aba80-163">Tam FTP kullanıcı adı ve URL kopyalayın ve bunları hello için bu öğreticinin sonraki bölümde kaydedin.</span><span class="sxs-lookup"><span data-stu-id="aba80-163">Copy your full FTP username and URL and save them for hello next section of this tutorial.</span></span>

   ![FTP URL ve kimlik bilgileri][AZ09]

## <a name="deploy-your-spring-boot-web-app-tooazure"></a><span data-ttu-id="aba80-165">Yay önyükleme web uygulama tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="aba80-165">Deploy your Spring Boot web app tooAzure</span></span>

<span data-ttu-id="aba80-166">Aşağıdaki adımları hello yay önyükleme web uygulama tooAzure hello adımları toodeploy yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="aba80-166">hello following steps will walk you through hello steps toodeploy your Spring Boot web app tooAzure.</span></span>

1. <span data-ttu-id="aba80-167">Windows Not Defteri gibi bir metin düzenleyicide açın ve yeni bir belgeye metin aşağıdaki hello yapıştırın, ardından hello dosyası olarak kaydetmeniz *web.config*:</span><span class="sxs-lookup"><span data-stu-id="aba80-167">Open a text editor such as Windows Notepad and paste hello following text into a new document, then save hello file as *web.config*:</span></span>
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <configuration>
     <system.webServer>
       <handlers>
         <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
       </handlers>
       <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
           arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\gs-spring-boot-0.1.0.jar&quot;">
       </httpPlatform>
     </system.webServer>
   </configuration>
   ```

1. <span data-ttu-id="aba80-168">Merhaba kaydettikten sonra *web.config* dosya tooyour sistemi, tooyour web uygulaması hello URL, kullanıcı adı ve bölüm bu öğreticinin önceki hello paroladan kullanarak FTP aracılığıyla bağlanır.</span><span class="sxs-lookup"><span data-stu-id="aba80-168">After you have saved hello *web.config* file tooyour system, connect tooyour web app via FTP using hello URL, username, and password from hello preceding section of this tutorial.</span></span> <span data-ttu-id="aba80-169">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="aba80-169">For example:</span></span>
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. <span data-ttu-id="aba80-170">Web uygulamanızın hello Uzak dizin toohello kök klasörünü Değiştir (olduğu anda */site/wwwroot*), ardından yay önyükleme uygulamanızdan hello JAR dosyasını kopyalayın ve hello *web.config* daha önce gelen.</span><span class="sxs-lookup"><span data-stu-id="aba80-170">Change hello remote directory toohello root folder of your web app, (which is at */site/wwwroot*), then copy hello JAR file from your Spring Boot application and hello *web.config* from earlier.</span></span> <span data-ttu-id="aba80-171">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="aba80-171">For example:</span></span>
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. <span data-ttu-id="aba80-172">JAR dağıttıktan sonra ve *web.config* dosyaları tooyour web uygulaması, toorestart hello Azure portal kullanarak web uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="aba80-172">After you have deployed your JAR and *web.config* files tooyour web app, you need toorestart your web app using hello Azure portal:</span></span>

   ![][AZ10]

1. <span data-ttu-id="aba80-173">Bir web tarayıcısı kullanarak tooyour web uygulamanızın URL'sine göz atarak Hello web uygulaması test veya curl kullanılabilir varsa aşağıdaki örneğine hello gibi hello sözdizimini kullanın:</span><span class="sxs-lookup"><span data-stu-id="aba80-173">Test hello web app by browsing tooyour web app's URL using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. <span data-ttu-id="aba80-174">Görüntülenen iletiden hello görmeniz gerekir: **Tebrikler İlkbahar önyüklemesinden!**</span><span class="sxs-lookup"><span data-stu-id="aba80-174">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Örnek uygulaması Gözat][SB02]

## <a name="next-steps"></a><span data-ttu-id="aba80-176">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aba80-176">Next steps</span></span>

<span data-ttu-id="aba80-177">Azure üzerinde yay önyükleme uygulamalarında kullanma hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="aba80-177">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="aba80-178">Linux üzerinde bir yay önyükleme uygulamasının hello Azure kapsayıcı hizmeti dağıtma</span><span class="sxs-lookup"><span data-stu-id="aba80-178">Deploy a Spring Boot Application on Linux in hello Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md)

* [<span data-ttu-id="aba80-179">Hello Azure kapsayıcı hizmeti Kubernetes kümesinde yay önyükleme uygulamasını dağıtma</span><span class="sxs-lookup"><span data-stu-id="aba80-179">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="aba80-180">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi] ve hello [Visual Studio Team Services için Java Araçları].</span><span class="sxs-lookup"><span data-stu-id="aba80-180">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="aba80-181">FTP kullanarak depoying web apps tooAzure hakkında ek bilgi için bkz: [, uygulama tooAzure uygulama FTP/S kullanarak hizmeti dağıtmak].</span><span class="sxs-lookup"><span data-stu-id="aba80-181">For additional information about depoying web apps tooAzure using FTP, see [Deploy your app tooAzure App Service using FTP/S].</span></span>

<span data-ttu-id="aba80-182">Merhaba yay önyükleme örnek proje hakkında daha fazla ayrıntı için bkz: [yay önyükleme Başlarken].</span><span class="sxs-lookup"><span data-stu-id="aba80-182">For further details about hello Spring Boot sample project, see [Spring Boot Getting Started].</span></span>

<span data-ttu-id="aba80-183">Hello kendi yay önyükleme uygulamaları ile çalışmaya başlama hakkında bilgi için bkz: **yay Initializr** https://start.spring.io/ adresindeki.</span><span class="sxs-lookup"><span data-stu-id="aba80-183">For help with getting started with your own Spring Boot applications, see hello **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="aba80-184">Web uygulamanız için ek ayarlarını yapılandırma hakkında daha fazla bilgi için bkz: [Azure App Service'te web uygulamalarını yapılandırma].</span><span class="sxs-lookup"><span data-stu-id="aba80-184">For more information about configuring additional settings for your web app, see [Configure web apps in Azure App Service].</span></span>

<!-- URL List -->

[Azure App Service]: https://azure.microsoft.com/services/app-service/
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Azure App Service'te web uygulamalarını yapılandırma]: /azure/app-service-web/web-sites-configure
[, uygulama tooAzure uygulama FTP/S kullanarak hizmeti dağıtmak]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp
[ücretsiz Azure hesabı]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Geliştirme Seti (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Visual Studio Team Services için Java Araçları]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN abone Avantajlarınızı]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Yay önyükleme]: http://projects.spring.io/spring-boot/
[yay önyükleme Başlarken]: https://github.com/spring-guides/gs-spring-boot
[yay Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB01.png
[SB02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB02.png

[AZ01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ01.png
[AZ02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ02.png
[AZ03]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ03.png
[AZ04]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ04.png
[AZ05]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ05.png
[AZ06]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ06.png
[AZ07]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ07.png
[AZ08]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ08.png
[AZ09]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ09.png
[AZ10]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ10.png
