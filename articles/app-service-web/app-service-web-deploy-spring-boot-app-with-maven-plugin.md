---
title: "Azure Web Apps toodeploy yay önyükleme uygulama tooAzure aaaHow toouse Merhaba Maven eklentisi"
description: "Nasıl toouse hello Maven eklentisi için Azure Web Apps toodeploy yay önyükleme uygulama tooAzure öğrenin."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 376fe90fe20621e15d7c9856214937c78b66026a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-tooazure"></a><span data-ttu-id="b2d62-103">Nasıl toouse hello Maven eklentisi için Azure Web Apps toodeploy yay önyükleme uygulama tooAzure</span><span class="sxs-lookup"><span data-stu-id="b2d62-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app tooAzure</span></span>

<span data-ttu-id="b2d62-104">Merhaba [Azure Web uygulamaları için Maven eklentisi](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) için [Apache Maven](http://maven.apache.org/) Maven projelerine Azure App Service'in sorunsuz tümleştirme sağlar ve geliştiriciler toodeploy web uygulamaları için hello işlemini kolaylaştırır Uygulama hizmeti tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b2d62-104">hello [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service into Maven projects, and streamlines hello process for developers toodeploy web apps tooAzure App Service.</span></span>

<span data-ttu-id="b2d62-105">Bu makalede Azure Web Apps toodeploy hello Maven eklentisi kullanarak bir örnek yay önyükleme uygulama tooAzure uygulama hizmetleri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b2d62-105">This article demonstrates using hello Maven Plugin for Azure Web Apps toodeploy a sample Spring Boot application tooAzure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="b2d62-106">Hello Azure Web uygulamaları için Maven eklentisi şu anda önizleme olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b2d62-106">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="b2d62-107">Ek özellikler hello gelecek için planlanan olsa da, şimdilik yalnızca FTP Yayımlama, desteklenir.</span><span class="sxs-lookup"><span data-stu-id="b2d62-107">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="b2d62-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b2d62-108">Prerequisites</span></span>

<span data-ttu-id="b2d62-109">Sipariş toocomplete hello adımlarda Bu öğreticide, Önkoşullar aşağıdaki toohave hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="b2d62-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="b2d62-110">Bir Azure aboneliği; bir Azure aboneliği zaten sahip değilseniz, etkinleştirebilir, [MSDN abone Avantajlarınızı] veya kaydolun bir [ücretsiz Azure hesabı].</span><span class="sxs-lookup"><span data-stu-id="b2d62-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="b2d62-111">Merhaba [Azure komut satırı arabirimi (CLI)].</span><span class="sxs-lookup"><span data-stu-id="b2d62-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="b2d62-112">Güncel [Java Geliştirme Seti (JDK)], 1,7 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="b2d62-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="b2d62-113">Apache'nın [Maven] aracını (sürüm 3) yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="b2d62-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="b2d62-114">A [Git] istemci.</span><span class="sxs-lookup"><span data-stu-id="b2d62-114">A [Git] client.</span></span>

## <a name="clone-hello-sample-spring-boot-web-app"></a><span data-ttu-id="b2d62-115">Kopya hello örnek yay önyükleme web uygulaması</span><span class="sxs-lookup"><span data-stu-id="b2d62-115">Clone hello sample Spring Boot web app</span></span>

<span data-ttu-id="b2d62-116">Bu bölümde, tamamlanmış bir yay önyükleme uygulama kopyalama ve yerel olarak test.</span><span class="sxs-lookup"><span data-stu-id="b2d62-116">In this section, you clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="b2d62-117">Bir komut istemi veya terminal penceresi açın ve yerel dizin toohold yay önyükleme uygulama ve değişiklik toothat dizin oluşturun; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b2d62-117">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="b2d62-118">--ya da--</span><span class="sxs-lookup"><span data-stu-id="b2d62-118">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="b2d62-119">Kopya hello [yay önyükleme Başlarken] örnek proje hello dizinine oluşturduğunuz; örneğin:</span><span class="sxs-lookup"><span data-stu-id="b2d62-119">Clone hello [Spring Boot Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. <span data-ttu-id="b2d62-120">Dizin tamamlandı toohello proje Değiştir; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b2d62-120">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="b2d62-121">Maven kullanarak hello JAR dosyasını oluşturun; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b2d62-121">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="b2d62-122">Merhaba web uygulaması oluşturduğunuzda Maven kullanarak hello web uygulaması başlatın; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b2d62-122">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="b2d62-123">Merhaba web uygulaması, bir web tarayıcısı kullanarak yerel olarak tooit göz atarak sınayın.</span><span class="sxs-lookup"><span data-stu-id="b2d62-123">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="b2d62-124">Örneğin, hello curl kullanılabilir varsa, aşağıdaki komutu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b2d62-124">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="b2d62-125">Görüntülenen iletiden hello görmeniz gerekir: **Tebrikler İlkbahar önyüklemesinden!**</span><span class="sxs-lookup"><span data-stu-id="b2d62-125">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="b2d62-126">Bir Azure hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2d62-126">Create an Azure service principal</span></span>

<span data-ttu-id="b2d62-127">Bu bölümde, bir Azure web uygulaması tooAzure dağıtırken Maven eklentisi kullanır hello hizmet sorumlusu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b2d62-127">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your web app tooAzure.</span></span>

1. <span data-ttu-id="b2d62-128">Bir komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="b2d62-128">Open a command prompt.</span></span>

1. <span data-ttu-id="b2d62-129">Azure CLI kullanarak Azure hesabınızda oturum hello:</span><span class="sxs-lookup"><span data-stu-id="b2d62-129">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="b2d62-130">Oturum açma Hello yönergeleri toocomplete hello süreci izleyin.</span><span class="sxs-lookup"><span data-stu-id="b2d62-130">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="b2d62-131">Bir Azure hizmet sorumlusu oluşturun:</span><span class="sxs-lookup"><span data-stu-id="b2d62-131">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="b2d62-132">Burada `uuuuuuuu` hello kullanıcı adı ve `pppppppp` hello hizmet sorumlusu hello parolası.</span><span class="sxs-lookup"><span data-stu-id="b2d62-132">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="b2d62-133">Azure aşağıdaki örneğine hello benzer JSON ile yanıt verir:</span><span class="sxs-lookup"><span data-stu-id="b2d62-133">Azure responds with JSON that resembles hello following example:</span></span>
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="b2d62-134">Web uygulaması tooAzure hello Maven eklentisi toodeploy yapılandırdığınızda bu JSON yanıt hello değerleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="b2d62-134">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your web app tooAzure.</span></span> <span data-ttu-id="b2d62-135">Merhaba `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, ve `tttttttt` olan yer tutucu değerlerini olduğunuz isteğe bağlı olarak bu örnek toomake daha kolay toomap kullanılan, Maven yapılandırdığınızda bu değerleri tootheir ilgili öğeleri `settings.xml` hello sonraki dosyayı bölüm.</span><span class="sxs-lookup"><span data-stu-id="b2d62-135">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a><span data-ttu-id="b2d62-136">Maven toouse, Azure hizmet sorumlusu yapılandırın</span><span class="sxs-lookup"><span data-stu-id="b2d62-136">Configure Maven toouse your Azure service principal</span></span>

<span data-ttu-id="b2d62-137">Bu bölümde, web uygulaması tooAzure dağıtırken Maven kullanan, Azure hizmet asıl tooconfigure hello kimlik doğrulamasını hello değerleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="b2d62-137">In this section, you use hello values from your Azure service principal tooconfigure hello authentication that Maven uses when deploying your web app tooAzure.</span></span>

1. <span data-ttu-id="b2d62-138">Maven açmak `settings.xml` dosyasını bir metin düzenleyicisinde; bu dosya yolunda hello örnekler aşağıdaki gibi olabilir:</span><span class="sxs-lookup"><span data-stu-id="b2d62-138">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="b2d62-139">Azure hizmet asıl ayarlarınızı hello önceki Bu öğretici toohello bölümünden eklemek `<servers>` hello koleksiyonunda *settings.xml* dosya; örneğin:</span><span class="sxs-lookup"><span data-stu-id="b2d62-139">Add your Azure service principal settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   <span data-ttu-id="b2d62-140">Konumlar:</span><span class="sxs-lookup"><span data-stu-id="b2d62-140">Where:</span></span>
   <span data-ttu-id="b2d62-141">Öğesi</span><span class="sxs-lookup"><span data-stu-id="b2d62-141">Element</span></span> | <span data-ttu-id="b2d62-142">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b2d62-142">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="b2d62-143">Web uygulaması tooAzure dağıttığınızda, Maven toolook, güvenlik ayarlarını kullanan benzersiz bir ad belirtir.</span><span class="sxs-lookup"><span data-stu-id="b2d62-143">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="b2d62-144">Merhaba içeren `appId` hizmet sorumlusu değeri.</span><span class="sxs-lookup"><span data-stu-id="b2d62-144">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="b2d62-145">Merhaba içeren `tenant` hizmet sorumlusu değeri.</span><span class="sxs-lookup"><span data-stu-id="b2d62-145">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="b2d62-146">Merhaba içeren `password` hizmet sorumlusu değeri.</span><span class="sxs-lookup"><span data-stu-id="b2d62-146">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="b2d62-147">Olan hello hedef Azure bulut ortamı tanımlar `AZURE` Bu örnekte.</span><span class="sxs-lookup"><span data-stu-id="b2d62-147">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="b2d62-148">(Tam bir listesi ortamlarının hello kullanılabilir [Azure Web uygulamaları için Maven eklentisi] belgeleri)</span><span class="sxs-lookup"><span data-stu-id="b2d62-148">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="b2d62-149">Kaydet ve Kapat hello *settings.xml* dosya.</span><span class="sxs-lookup"><span data-stu-id="b2d62-149">Save and close hello *settings.xml* file.</span></span>

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-tooazure"></a><span data-ttu-id="b2d62-150">İsteğe bağlı:, pom.xml web uygulama tooAzure dağıtmadan önce özelleştirme</span><span class="sxs-lookup"><span data-stu-id="b2d62-150">OPTIONAL: Customize your pom.xml before deploying your web app tooAzure</span></span>

<span data-ttu-id="b2d62-151">Açık hello `pom.xml` dosyasını bir metin düzenleyicisinde yay önyükleme uygulamanız için ve hello bulun `<plugin>` öğesi için `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="b2d62-151">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="b2d62-152">Bu öğe aşağıdaki örneğine hello benzemelidir:</span><span class="sxs-lookup"><span data-stu-id="b2d62-152">This element should resemble hello following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-web-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>ftp</deploymentType>
         <resources>
            <resource>
               <directory>${project.basedir}/target</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>*.jar</include>
               </includes>
            </resource>
            <resource>
               <directory>${project.basedir}</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>web.config</include>
               </includes>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="b2d62-153">Merhaba Maven eklentisi için değiştirebileceğiniz birkaç değer vardır ve bu öğelerin her biri için ayrıntılı bir açıklama hello kullanılabilir [Azure Web uygulamaları için Maven eklentisi] belgeleri.</span><span class="sxs-lookup"><span data-stu-id="b2d62-153">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="b2d62-154">Denirse, bu makaledeki vurgulama değer olan birkaç değerleri vardır:</span><span class="sxs-lookup"><span data-stu-id="b2d62-154">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="b2d62-155">Öğesi</span><span class="sxs-lookup"><span data-stu-id="b2d62-155">Element</span></span> | <span data-ttu-id="b2d62-156">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b2d62-156">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="b2d62-157">Merhaba Hello sürümünü belirtir [Azure Web uygulamaları için Maven eklentisi].</span><span class="sxs-lookup"><span data-stu-id="b2d62-157">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="b2d62-158">Hello listelenen hello sürüm denetlemelisiniz [Maven merkezi depo](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) kullanmakta olduğunuz tooensure hello en son sürümü.</span><span class="sxs-lookup"><span data-stu-id="b2d62-158">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="b2d62-159">Merhaba kimlik doğrulama bilgilerini içeren bu örnekte Azure belirtir bir `<serverId>` içeren öğeyi `azure-auth`; Maven Maven içinde bu değer toolook hello Azure hizmet asıl değerleri kullanan *settings.xml* bu makalenin önceki bölümde tanımlanan dosya.</span><span class="sxs-lookup"><span data-stu-id="b2d62-159">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="b2d62-160">Olan hello hedef kaynak grubu belirtir `maven-plugin` Bu örnekte.</span><span class="sxs-lookup"><span data-stu-id="b2d62-160">Specifies hello target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="b2d62-161">Merhaba kaynak grubu, zaten yoksa, dağıtım sırasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b2d62-161">hello resource group is created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="b2d62-162">Web uygulamanız için Hello hedef adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="b2d62-162">Specifies hello target name for your web app.</span></span> <span data-ttu-id="b2d62-163">Bu örnekte hello hedef adıdır `maven-web-app-${maven.build.timestamp}`, hello burada `${maven.build.timestamp}` soneki, bu örnek tooavoid çakışması eklenir.</span><span class="sxs-lookup"><span data-stu-id="b2d62-163">In this example, hello target name is `maven-web-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="b2d62-164">(Merhaba zaman damgası isteğe bağlıdır; hello uygulama adı için benzersiz bir dize belirtin.)</span><span class="sxs-lookup"><span data-stu-id="b2d62-164">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="b2d62-165">Olan bu örnekte hello hedef bölgesi belirtir `westus`.</span><span class="sxs-lookup"><span data-stu-id="b2d62-165">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="b2d62-166">(Tam bir liste hello olan [Azure Web uygulamaları için Maven eklentisi] belgelerine.)</span><span class="sxs-lookup"><span data-stu-id="b2d62-166">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<javaVersion>` | <span data-ttu-id="b2d62-167">Web uygulamanız için Hello Java Çalışma zamanı sürümü belirler.</span><span class="sxs-lookup"><span data-stu-id="b2d62-167">Specifies hello Java runtime version for your web app.</span></span> <span data-ttu-id="b2d62-168">(Tam bir liste hello olan [Azure Web uygulamaları için Maven eklentisi] belgelerine.)</span><span class="sxs-lookup"><span data-stu-id="b2d62-168">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<deploymentType>` | <span data-ttu-id="b2d62-169">Web uygulamanız için dağıtım türünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="b2d62-169">Specifies deployment type for your web app.</span></span> <span data-ttu-id="b2d62-170">Şu an yalnızca `ftp` desteklenir, ancak diğer dağıtım türlerinde geliştirme desteği.</span><span class="sxs-lookup"><span data-stu-id="b2d62-170">For now, only `ftp` is supported, although support for other deployment types is in development.</span></span>
`<resources>` | <span data-ttu-id="b2d62-171">Kaynakları ve web uygulama tooAzure dağıtırken Maven kullanan hedef konumları belirtir.</span><span class="sxs-lookup"><span data-stu-id="b2d62-171">Specifies resources and target destinations which Maven uses when deploying your web app tooAzure.</span></span> <span data-ttu-id="b2d62-172">Bu örnekte, iki `<resource>` öğelerini belirtmek Maven hello ve web uygulaması için hello JAR dosyasını dağıtacağınız *web.config* hello yay önyükleme proje dosyasından.</span><span class="sxs-lookup"><span data-stu-id="b2d62-172">In this example, two `<resource>` elements specify that Maven will deploy hello JAR file for your web app and hello *web.config* file from hello Spring Boot project.</span></span>

## <a name="build-and-deploy-your-web-app-tooazure"></a><span data-ttu-id="b2d62-173">Derleme ve web uygulama tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="b2d62-173">Build and deploy your web app tooAzure</span></span>

<span data-ttu-id="b2d62-174">Bölümler, bu makalenin önceki hello tüm hello ayarlarını yapılandırdıktan sonra hazır toodeploy olan web uygulaması tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b2d62-174">Once you have configured all of hello settings in hello preceding sections of this article, you are ready toodeploy your web app tooAzure.</span></span> <span data-ttu-id="b2d62-175">toodo, bu nedenle, hello aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="b2d62-175">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="b2d62-176">Merhaba komut istemi veya daha önce kullandığınız terminal penceresinden, tüm değişiklikleri toohello yaptıysanız Maven kullanarak hello JAR dosyasını yeniden *pom.xml* dosya; örneğin:</span><span class="sxs-lookup"><span data-stu-id="b2d62-176">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="b2d62-177">Web uygulaması tooAzure Maven kullanarak dağıtabilirsiniz; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b2d62-177">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="b2d62-178">Maven web uygulama tooAzure dağıtacağınız; Merhaba web uygulaması zaten mevcut değilse oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b2d62-178">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

<span data-ttu-id="b2d62-179">Web dağıtıldığında mümkün toomanage olacaktır hello kullanarak [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="b2d62-179">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="b2d62-180">Web uygulamanızı listelenen **uygulama hizmetleri**:</span><span class="sxs-lookup"><span data-stu-id="b2d62-180">Your web app will be listed in **App Services**:</span></span>

   ![Azure portalında uygulama hizmetleri listelenen web uygulaması][AP01]

* <span data-ttu-id="b2d62-182">Ve web uygulamanızı hello listelenir URL hello **genel bakış** web uygulamanız için:</span><span class="sxs-lookup"><span data-stu-id="b2d62-182">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

   ![Web uygulamanız için Hello URL belirleme][AP02]

<!--
##  OPTIONAL: Configure hello embedded Tomcat server toorun on a different port

hello embedded Tomcat server in hello sample Spring Boot application is configured toorun on port 8080 by default. However, if you want toorun hello embedded Tomcat server toorun on a different port, such as port 80 for local testing, you can configure hello port by using hello following steps.

1. Go toohello *resources* directory (or create hello directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open hello *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify hello **server** setting so that hello server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close hello *application.yml* file.
-->

## <a name="next-steps"></a><span data-ttu-id="b2d62-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b2d62-184">Next steps</span></span>

<span data-ttu-id="b2d62-185">Bu makalede ele alınan çeşitli teknolojiler hello hakkında daha fazla bilgi makaleleri aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="b2d62-185">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="b2d62-186">[Azure Web uygulamaları için Maven eklentisi]</span><span class="sxs-lookup"><span data-stu-id="b2d62-186">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="b2d62-187">TooAzure hello Azure CLI gelen oturum</span><span class="sxs-lookup"><span data-stu-id="b2d62-187">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="b2d62-188">Nasıl toouse hello Maven eklentisi için Azure Web Apps toodeploy kapsayıcılı yay önyükleme uygulama tooAzure</span><span class="sxs-lookup"><span data-stu-id="b2d62-188">How toouse hello Maven Plugin for Azure Web Apps toodeploy a containerized Spring Boot app tooAzure</span></span>](app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin.md)

* [<span data-ttu-id="b2d62-189">Bir Azure hizmet sorumlusu Azure CLI 2.0 ile oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b2d62-189">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="b2d62-190">Maven ayarları başvurusu</span><span class="sxs-lookup"><span data-stu-id="b2d62-190">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure komut satırı arabirimi (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[ücretsiz Azure hesabı]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN abone Avantajlarınızı]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[yay önyükleme Başlarken]: https://github.com/microsoft/gs-spring-boot
[Spring Framework]: https://spring.io/
[Azure Web uygulamaları için Maven eklentisi]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP02.png
