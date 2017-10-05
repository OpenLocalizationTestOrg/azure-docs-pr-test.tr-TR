---
title: "Yay önyükleme uygulamasını Azure App Service'e dağıtma | Microsoft Docs"
description: "Bu öğretici yay önyükleme Başlarken web uygulamasını Azure App Service'e dağıtmak için geliştiricilere adımlarında yol gösterir."
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
ms.openlocfilehash: 0c388862d927a1492745832225c686670c071f86
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-spring-boot-application-to-the-azure-app-service"></a><span data-ttu-id="01744-103">Azure Uygulama Hizmeti’ne Spring Boot Uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="01744-103">Deploy a Spring Boot Application to the Azure App Service</span></span>

<span data-ttu-id="01744-104"> **[Yay Framework]**  Java geliştiriciler kuruluş düzeyinde uygulamalar oluşturmanıza yardımcı olan bir açık kaynak çözümüdür ve bu platformu üzerine kurulmuştur daha popüler projeleri biri [yay önyükleme], tek başına Java uygulamaları oluşturmak için basitleştirilmiş bir yaklaşım sağlar.</span><span class="sxs-lookup"><span data-stu-id="01744-104">The **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications, and one of the more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="01744-105">Bu öğretici ancak örnek yay önyükleme Başlarken web uygulaması oluşturma ve dağıttıktan anlatılır [Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="01744-105">This tutorial will walk you though creating the sample Spring Boot Getting Started web app and deploying it to [Azure App Service].</span></span>

### <a name="prerequisites"></a><span data-ttu-id="01744-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="01744-106">Prerequisites</span></span>

<span data-ttu-id="01744-107">Bu öğreticiyi tamamlamak için aşağıdakilere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="01744-107">In order to complete the steps in this tutorial, you need to have the following:</span></span>

* <span data-ttu-id="01744-108">Bir Azure aboneliği; bir Azure aboneliği zaten sahip değilseniz, etkinleştirebilir, [MSDN abone Avantajlarınızı] veya kaydolun bir [ücretsiz Azure hesabı].</span><span class="sxs-lookup"><span data-stu-id="01744-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="01744-109">Güncel bir [Java Geliştirme Seti (JDK)].</span><span class="sxs-lookup"><span data-stu-id="01744-109">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="01744-110">Apache'nın [Maven] aracını (sürüm 3) yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="01744-110">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="01744-111">A [Git] istemci.</span><span class="sxs-lookup"><span data-stu-id="01744-111">A [Git] client.</span></span>

## <a name="create-the-spring-boot-getting-started-web-app"></a><span data-ttu-id="01744-112">Yay önyükleme Başlarken web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="01744-112">Create the Spring Boot Getting Started web app</span></span>

<span data-ttu-id="01744-113">Aşağıdaki adımlar, basit bir yay önyükleme web uygulaması oluşturma ve yerel olarak test etmek için gereken adımlarda size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="01744-113">The following steps will walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="01744-114">Bir komut istemi açın ve uygulamanızı tutun ve bu dizine değiştirmek için yerel bir dizin oluşturun; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="01744-114">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="01744-115">--ya da--</span><span class="sxs-lookup"><span data-stu-id="01744-115">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="01744-116">Kopya [yay önyükleme Başlarken] örnek proje yeni oluşturduğunuz; dizine örneğin:</span><span class="sxs-lookup"><span data-stu-id="01744-116">Clone the [Spring Boot Getting Started] sample project into the directory you just created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. <span data-ttu-id="01744-117">Projeyi Dizin Değiştir; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="01744-117">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot
   cd complete
   ```

1. <span data-ttu-id="01744-118">Maven kullanarak JAR dosyasını oluşturun; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="01744-118">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="01744-119">Web uygulaması oluşturulduktan sonra JAR dosyasına dizini değiştirin ve web uygulaması başlatın; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="01744-119">Once the web app has been created, change directory to the JAR file and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. <span data-ttu-id="01744-120">Web uygulaması http://localhost: 8080 bir web tarayıcısı kullanarak göz atarak test veya curl kullanılabilir varsa aşağıdaki örnekteki gibi sözdizimini kullanın:</span><span class="sxs-lookup"><span data-stu-id="01744-120">Test the web app by browsing to http://localhost:8080 using a web browser, or use the syntax like the following example if you have curl available:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="01744-121">Aşağıdaki ileti görürsünüz: **Tebrikler İlkbahar önyüklemesinden!**</span><span class="sxs-lookup"><span data-stu-id="01744-121">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Örnek uygulaması Gözat][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a><span data-ttu-id="01744-123">Java ile kullanmak için bir Azure web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="01744-123">Create an Azure web app for use with Java</span></span>

<span data-ttu-id="01744-124">Aşağıdaki adımlar bir Azure Web uygulaması oluşturma, Java için gereken ayarları yapılandırın ve FTP kimlik bilgilerinizi yapılandırma adımlarında size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="01744-124">The following steps will walk you through the steps to create an Azure Web App, configure the required settings for Java, and configure your FTP credentials.</span></span>

1. <span data-ttu-id="01744-125">Gözat [Azure portal] ve oturum açın.</span><span class="sxs-lookup"><span data-stu-id="01744-125">Browse to the [Azure portal] and log in.</span></span>

1. <span data-ttu-id="01744-126">Azure portalındaki hesabınızda oturum açtıktan sonra menü simgesini **uygulama hizmetleri**:</span><span class="sxs-lookup"><span data-stu-id="01744-126">Once you have logged into your account on the Azure portal, click the menu icon for **App Services**:</span></span>
   
   ![Azure portalına][AZ01]

1. <span data-ttu-id="01744-128">Zaman **uygulama hizmetleri** sayfası görüntülenirse, tıklatın **+ Ekle** yeni bir uygulama hizmeti oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="01744-128">When the **App Services** page is displayed, click **+ Add** to create a new App Service.</span></span>

   ![Uygulama hizmeti oluşturma][AZ02]

1. <span data-ttu-id="01744-130">Web uygulama şablonları görüntülendiğinde, temel Microsoft Web uygulaması için bağlantıyı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="01744-130">When the list of web app templates is displayed, click the link for the basic Microsoft Web App.</span></span>

   ![Web Uygulama Şablonları][AZ03]

1. <span data-ttu-id="01744-132">Bilgi sayfası Web uygulaması şablonu görüntülenen için tıklattığınızda **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="01744-132">When the information page for the Web App template is displayed, click **Create**.</span></span>

   ![Web Uygulaması Oluşturma][AZ04]

1. <span data-ttu-id="01744-134">Web uygulamanız için benzersiz bir ad sağlayın ve herhangi bir ek ayarları belirtin ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="01744-134">Provide a unique name for your web app and specify any additional settings, and then **Create**.</span></span>

   ![Web uygulaması ayarları oluşturma][AZ05]

1. <span data-ttu-id="01744-136">Web uygulamanız oluşturulduktan sonra menü simgesini **uygulama hizmetleri**ve yeni oluşturulan web uygulamanız'ye tıklayın:</span><span class="sxs-lookup"><span data-stu-id="01744-136">Once your web app has been created, click the menu icon for **App Services**, and then click your newly-created web app:</span></span>

   ![Liste Web uygulamaları][AZ06]

1. <span data-ttu-id="01744-138">Web uygulamanızı görüntülendiğinde, aşağıdaki adımları kullanarak Java sürümü belirtin:</span><span class="sxs-lookup"><span data-stu-id="01744-138">When your web app is displayed, specify the Java version by using the following steps:</span></span>

   <span data-ttu-id="01744-139">a.</span><span class="sxs-lookup"><span data-stu-id="01744-139">a.</span></span> <span data-ttu-id="01744-140">Tıklatın **uygulama ayarları** menü öğesi.</span><span class="sxs-lookup"><span data-stu-id="01744-140">Click the **Application Settings** menu item.</span></span>

   <span data-ttu-id="01744-141">b.</span><span class="sxs-lookup"><span data-stu-id="01744-141">b.</span></span> <span data-ttu-id="01744-142">Seçin **Java 8** Java sürümü için.</span><span class="sxs-lookup"><span data-stu-id="01744-142">Choose **Java 8** for the Java version.</span></span>

   <span data-ttu-id="01744-143">c.</span><span class="sxs-lookup"><span data-stu-id="01744-143">c.</span></span> <span data-ttu-id="01744-144">Seçin **Newest** alt Java Sürüm için.</span><span class="sxs-lookup"><span data-stu-id="01744-144">Choose **Newest** for the minor Java version.</span></span>

   <span data-ttu-id="01744-145">d.</span><span class="sxs-lookup"><span data-stu-id="01744-145">d.</span></span> <span data-ttu-id="01744-146">Seçin **yeni Tomcat 8.5** web kapsayıcısı için.</span><span class="sxs-lookup"><span data-stu-id="01744-146">Choose **Newest Tomcat 8.5** for the web container.</span></span> <span data-ttu-id="01744-147">(Aslında bu kapsayıcı kullanılmaz; Azure kapsayıcı yay önyükleme uygulamanızdan kullanır.)</span><span class="sxs-lookup"><span data-stu-id="01744-147">(This container will not actually be used; Azure will use the container from your Spring Boot application.)</span></span>

   <span data-ttu-id="01744-148">e.</span><span class="sxs-lookup"><span data-stu-id="01744-148">e.</span></span> <span data-ttu-id="01744-149">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01744-149">Click **Save**.</span></span>

   ![Uygulama ayarları][AZ07]

1. <span data-ttu-id="01744-151">Aşağıdaki adımları kullanarak, FTP dağıtımı kimlik bilgileri belirtin:</span><span class="sxs-lookup"><span data-stu-id="01744-151">Specify your FTP deployment credentials by using the following steps:</span></span>

   <span data-ttu-id="01744-152">a.</span><span class="sxs-lookup"><span data-stu-id="01744-152">a.</span></span> <span data-ttu-id="01744-153">Tıklatın **dağıtım kimlik bilgileri** menü öğesi.</span><span class="sxs-lookup"><span data-stu-id="01744-153">Click the **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="01744-154">b.</span><span class="sxs-lookup"><span data-stu-id="01744-154">b.</span></span> <span data-ttu-id="01744-155">Kullanıcı adı ve parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="01744-155">Specify your username and password.</span></span>

   <span data-ttu-id="01744-156">c.</span><span class="sxs-lookup"><span data-stu-id="01744-156">c.</span></span> <span data-ttu-id="01744-157">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01744-157">Click **Save**.</span></span>

   ![Dağıtım kimlik bilgilerini belirtin][AZ08]

1. <span data-ttu-id="01744-159">Aşağıdaki adımları kullanarak FTP bağlantı bilgileri alın:</span><span class="sxs-lookup"><span data-stu-id="01744-159">Retrieve your FTP connection information by using the following steps:</span></span>

   <span data-ttu-id="01744-160">a.</span><span class="sxs-lookup"><span data-stu-id="01744-160">a.</span></span> <span data-ttu-id="01744-161">Tıklatın **dağıtım kimlik bilgileri** menü öğesi.</span><span class="sxs-lookup"><span data-stu-id="01744-161">Click the **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="01744-162">b.</span><span class="sxs-lookup"><span data-stu-id="01744-162">b.</span></span> <span data-ttu-id="01744-163">Tam FTP kullanıcı adı ve URL kopyalayın ve Bu öğretici için sonraki bölüme kaydedin.</span><span class="sxs-lookup"><span data-stu-id="01744-163">Copy your full FTP username and URL and save them for the next section of this tutorial.</span></span>

   ![FTP URL ve kimlik bilgileri][AZ09]

## <a name="deploy-your-spring-boot-web-app-to-azure"></a><span data-ttu-id="01744-165">Yay önyükleme web uygulamanızı Azure'a dağıtma</span><span class="sxs-lookup"><span data-stu-id="01744-165">Deploy your Spring Boot web app to Azure</span></span>

<span data-ttu-id="01744-166">Aşağıdaki adımları yay önyükleme web uygulamanızı Azure'a dağıtmak için adımlarda size yol gösterecek.</span><span class="sxs-lookup"><span data-stu-id="01744-166">The following steps will walk you through the steps to deploy your Spring Boot web app to Azure.</span></span>

1. <span data-ttu-id="01744-167">Windows Not Defteri gibi bir metin düzenleyicide açın ve aşağıdaki metni yeni bir belgeye yapıştırın ve ardından dosyayı farklı Kaydet *web.config*:</span><span class="sxs-lookup"><span data-stu-id="01744-167">Open a text editor such as Windows Notepad and paste the following text into a new document, then save the file as *web.config*:</span></span>
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

1. <span data-ttu-id="01744-168">Kaydettiğiniz sonra *web.config* dosya sistemi için bu öğreticinin önceki bölümünden URL, kullanıcı adı ve parola kullanarak FTP üzerinden web uygulamanıza bağlayın.</span><span class="sxs-lookup"><span data-stu-id="01744-168">After you have saved the *web.config* file to your system, connect to your web app via FTP using the URL, username, and password from the preceding section of this tutorial.</span></span> <span data-ttu-id="01744-169">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="01744-169">For example:</span></span>
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. <span data-ttu-id="01744-170">Uzak dizin, web uygulamanızın kök klasörüne değiştirme (olduğu anda */site/wwwroot*), ardından yay önyükleme uygulamanızdan JAR dosyasını kopyalamanız ve *web.config* daha önce gelen.</span><span class="sxs-lookup"><span data-stu-id="01744-170">Change the remote directory to the root folder of your web app, (which is at */site/wwwroot*), then copy the JAR file from your Spring Boot application and the *web.config* from earlier.</span></span> <span data-ttu-id="01744-171">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="01744-171">For example:</span></span>
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. <span data-ttu-id="01744-172">JAR dağıttıktan sonra ve *web.config* dosyaları web uygulamanız için Azure Portalı'nı kullanarak, web uygulaması yeniden vermeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="01744-172">After you have deployed your JAR and *web.config* files to your web app, you need to restart your web app using the Azure portal:</span></span>

   ![][AZ10]

1. <span data-ttu-id="01744-173">Web uygulaması bir web tarayıcısı kullanarak, web uygulamanızın URL'sine göz atarak test veya curl kullanılabilir varsa aşağıdaki örnekteki gibi sözdizimini kullanın:</span><span class="sxs-lookup"><span data-stu-id="01744-173">Test the web app by browsing to your web app's URL using a web browser, or use the syntax like the following example if you have curl available:</span></span>
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. <span data-ttu-id="01744-174">Aşağıdaki ileti görürsünüz: **Tebrikler İlkbahar önyüklemesinden!**</span><span class="sxs-lookup"><span data-stu-id="01744-174">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Örnek uygulaması Gözat][SB02]

## <a name="next-steps"></a><span data-ttu-id="01744-176">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="01744-176">Next steps</span></span>

<span data-ttu-id="01744-177">Azure üzerinde yay önyükleme uygulamalarında kullanma hakkında daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="01744-177">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="01744-178">Azure kapsayıcı Hizmeti'nde Linux'ta yay önyükleme uygulamasını dağıtma</span><span class="sxs-lookup"><span data-stu-id="01744-178">Deploy a Spring Boot Application on Linux in the Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md)

* [<span data-ttu-id="01744-179">Azure kapsayıcı hizmeti Kubernetes kümesinde yay önyükleme uygulamasını dağıtma</span><span class="sxs-lookup"><span data-stu-id="01744-179">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="01744-180">Azure’u Java ile kullanma hakkında daha fazla bilgi edinmek için bkz. [Azure Java Geliştirici Merkezi] ve [Visual Studio Team Services için Java Araçları].</span><span class="sxs-lookup"><span data-stu-id="01744-180">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="01744-181">FTP kullanarak Azure depoying web uygulamaları hakkında ek bilgi için bkz [FTP/S kullanarak Azure App Service için uygulamanızı dağıtma].</span><span class="sxs-lookup"><span data-stu-id="01744-181">For additional information about depoying web apps to Azure using FTP, see [Deploy your app to Azure App Service using FTP/S].</span></span>

<span data-ttu-id="01744-182">Yay önyükleme örnek proje hakkında daha fazla ayrıntı için bkz: [yay önyükleme Başlarken].</span><span class="sxs-lookup"><span data-stu-id="01744-182">For further details about the Spring Boot sample project, see [Spring Boot Getting Started].</span></span>

<span data-ttu-id="01744-183">Kendi yay önyükleme uygulamaları ile çalışmaya başlama hakkında bilgi için bkz: **yay Initializr** https://start.spring.io/ adresindeki.</span><span class="sxs-lookup"><span data-stu-id="01744-183">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="01744-184">Web uygulamanız için ek ayarlarını yapılandırma hakkında daha fazla bilgi için bkz: [Azure App Service'te web uygulamalarını yapılandırma].</span><span class="sxs-lookup"><span data-stu-id="01744-184">For more information about configuring additional settings for your web app, see [Configure web apps in Azure App Service].</span></span>

<!-- URL List -->

<span data-ttu-id="01744-185">[Azure App Service]: https://azure.microsoft.com/services/app-service/</span><span class="sxs-lookup"><span data-stu-id="01744-185">[Azure App Service]: https://azure.microsoft.com/services/app-service/</span></span>
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
<span data-ttu-id="01744-186">[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="01744-186">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="01744-187">[Azure portal]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="01744-187">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="01744-188">[Azure App Service'te web uygulamalarını yapılandırma]: /azure/app-service-web/web-sites-configure</span><span class="sxs-lookup"><span data-stu-id="01744-188">[Configure web apps in Azure App Service]: /azure/app-service-web/web-sites-configure</span></span>
<span data-ttu-id="01744-189">[FTP/S kullanarak Azure App Service için uygulamanızı dağıtma]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp</span><span class="sxs-lookup"><span data-stu-id="01744-189">[Deploy your app to Azure App Service using FTP/S]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp</span></span>
<span data-ttu-id="01744-190">[ücretsiz Azure hesabı]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="01744-190">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="01744-191">[Git]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="01744-191">[Git]: https://github.com/</span></span>
<span data-ttu-id="01744-192">[Java Geliştirme Seti (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span><span class="sxs-lookup"><span data-stu-id="01744-192">[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span></span>
<span data-ttu-id="01744-193">[Visual Studio Team Services için Java Araçları]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="01744-193">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>
<span data-ttu-id="01744-194">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="01744-194">[Maven]: http://maven.apache.org/</span></span>
<span data-ttu-id="01744-195">[MSDN abone Avantajlarınızı]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="01744-195">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
<span data-ttu-id="01744-196">[yay önyükleme]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="01744-196">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="01744-197">[yay önyükleme Başlarken]: https://github.com/spring-guides/gs-spring-boot</span><span class="sxs-lookup"><span data-stu-id="01744-197">[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot</span></span>
<span data-ttu-id="01744-198">[Yay Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="01744-198">[Spring Framework]: https://spring.io/</span></span>

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
