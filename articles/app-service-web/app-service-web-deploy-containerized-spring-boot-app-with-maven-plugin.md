---
title: "Azure Web Apps toodeploy kapsayıcılı yay önyükleme uygulama tooAzure aaaHow toouse Merhaba Maven eklentisi"
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
ms.openlocfilehash: e7e760d4ef5bd4c92a4126a50a2b12e5c8f2b4a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-containerized-spring-boot-app-tooazure"></a><span data-ttu-id="c4a8a-103">Nasıl toouse hello Maven eklentisi için Azure Web Apps toodeploy kapsayıcılı yay önyükleme uygulama tooAzure</span><span class="sxs-lookup"><span data-stu-id="c4a8a-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a containerized Spring Boot app tooAzure</span></span>

<span data-ttu-id="c4a8a-104">Merhaba [Azure Web uygulamaları için Maven eklentisi](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) için [Apache Maven](http://maven.apache.org/) Maven projelerine Azure App Service'in sorunsuz tümleştirme sağlar ve geliştiriciler toodeploy web uygulamaları için hello işlemini kolaylaştırır Uygulama hizmeti tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-104">hello [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service  into Maven projects, and streamlines hello process for developers toodeploy web apps tooAzure App Service .</span></span>

<span data-ttu-id="c4a8a-105">Bu makalede Azure Web Apps toodeploy hello Maven eklentisi kullanarak bir örnek yay önyükleme uygulama Docker kapsayıcısı tooAzure uygulama hizmetleri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-105">This article demonstrates using hello Maven Plugin for Azure Web Apps toodeploy a sample Spring Boot application in a Docker container tooAzure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="c4a8a-106">Hello Azure Web uygulamaları için Maven eklentisi şu anda önizleme olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-106">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="c4a8a-107">Ek özellikler hello gelecek için planlanan olsa da, şimdilik yalnızca FTP Yayımlama, desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-107">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="c4a8a-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c4a8a-108">Prerequisites</span></span>

<span data-ttu-id="c4a8a-109">Sipariş toocomplete hello adımlarda Bu öğreticide, Önkoşullar aşağıdaki toohave hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="c4a8a-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="c4a8a-110">Bir Azure aboneliği; bir Azure aboneliği zaten sahip değilseniz, etkinleştirebilir, [MSDN abone Avantajlarınızı] veya kaydolun bir [ücretsiz Azure hesabı].</span><span class="sxs-lookup"><span data-stu-id="c4a8a-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="c4a8a-111">Merhaba [Azure komut satırı arabirimi (CLI)].</span><span class="sxs-lookup"><span data-stu-id="c4a8a-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="c4a8a-112">Güncel [Java Geliştirme Seti (JDK)], 1,7 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="c4a8a-113">Apache'nın [Maven] aracını (sürüm 3) yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="c4a8a-114">A [Git] istemci.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-114">A [Git] client.</span></span>
* <span data-ttu-id="c4a8a-115">A [Docker] istemci.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="c4a8a-116">Toohello sanallaştırma gereksinimleri Bu öğreticinin bir sanal makinede bu makalede hello adımları izleyin olamaz; sanallaştırma özellikleri etkin bir fiziksel bilgisayar kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="c4a8a-117">Docker web uygulaması üzerinde kopya hello örnek yay önyükleme</span><span class="sxs-lookup"><span data-stu-id="c4a8a-117">Clone hello sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="c4a8a-118">Bu bölümde kapsayıcılı yay önyükleme uygulama kopyalamak ve yerel olarak test.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-118">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="c4a8a-119">Bir komut istemi veya terminal penceresi açın ve yerel dizin toohold yay önyükleme uygulama ve değişiklik toothat dizin oluşturun; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="c4a8a-119">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="c4a8a-120">--ya da--</span><span class="sxs-lookup"><span data-stu-id="c4a8a-120">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="c4a8a-121">Kopya hello [Docker Başlarken yay önyüklemede] örnek proje hello dizinine oluşturduğunuz; örneğin:</span><span class="sxs-lookup"><span data-stu-id="c4a8a-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="c4a8a-122">Dizin tamamlandı toohello proje Değiştir; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="c4a8a-122">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="c4a8a-123">Maven kullanarak hello JAR dosyasını oluşturun; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="c4a8a-123">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="c4a8a-124">Merhaba web uygulaması oluşturduğunuzda Maven kullanarak hello web uygulaması başlatın; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="c4a8a-124">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="c4a8a-125">Merhaba web uygulaması, bir web tarayıcısı kullanarak yerel olarak tooit göz atarak sınayın.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-125">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="c4a8a-126">Örneğin, hello curl kullanılabilir varsa, aşağıdaki komutu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c4a8a-126">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="c4a8a-127">Görüntülenen iletiden hello görmeniz gerekir: **Docker Hello World**</span><span class="sxs-lookup"><span data-stu-id="c4a8a-127">You should see hello following message displayed: **Hello Docker World**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="c4a8a-128">Bir Azure hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="c4a8a-128">Create an Azure service principal</span></span>

<span data-ttu-id="c4a8a-129">Bu bölümde, Azure kapsayıcı tooAzure dağıtırken Maven eklentisi kullanır hello hizmet sorumlusu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-129">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="c4a8a-130">Bir komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-130">Open a command prompt.</span></span>

1. <span data-ttu-id="c4a8a-131">Azure CLI kullanarak Azure hesabınızda oturum hello:</span><span class="sxs-lookup"><span data-stu-id="c4a8a-131">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="c4a8a-132">Oturum açma Hello yönergeleri toocomplete hello süreci izleyin.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-132">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="c4a8a-133">Bir Azure hizmet sorumlusu oluşturun:</span><span class="sxs-lookup"><span data-stu-id="c4a8a-133">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="c4a8a-134">Burada `uuuuuuuu` hello kullanıcı adı ve `pppppppp` hello hizmet sorumlusu hello parolası.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-134">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="c4a8a-135">Azure aşağıdaki örneğine hello benzer JSON ile yanıt verir:</span><span class="sxs-lookup"><span data-stu-id="c4a8a-135">Azure responds with JSON that resembles hello following example:</span></span>
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
   > <span data-ttu-id="c4a8a-136">Kapsayıcı tooAzure hello Maven eklentisi toodeploy yapılandırdığınızda bu JSON yanıt hello değerleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-136">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your container tooAzure.</span></span> <span data-ttu-id="c4a8a-137">Merhaba `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, ve `tttttttt` olan yer tutucu değerlerini olduğunuz isteğe bağlı olarak bu örnek toomake daha kolay toomap kullanılan, Maven yapılandırdığınızda bu değerleri tootheir ilgili öğeleri `settings.xml` hello sonraki dosyayı bölüm.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-137">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a><span data-ttu-id="c4a8a-138">Maven toouse, Azure hizmet sorumlusu yapılandırın</span><span class="sxs-lookup"><span data-stu-id="c4a8a-138">Configure Maven toouse your Azure service principal</span></span>

<span data-ttu-id="c4a8a-139">Bu bölümde, Maven kapsayıcı tooAzure dağıtırken kullanacağı, Azure hizmet asıl tooconfigure hello kimlik doğrulamasını hello değerleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-139">In this section, you use hello values from your Azure service principal tooconfigure hello authentication that Maven will use when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="c4a8a-140">Maven açmak `settings.xml` dosyasını bir metin düzenleyicisinde; bu dosya yolunda hello örnekler aşağıdaki gibi olabilir:</span><span class="sxs-lookup"><span data-stu-id="c4a8a-140">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="c4a8a-141">Azure hizmet asıl ayarlarınızı hello önceki Bu öğretici toohello bölümünden eklemek `<servers>` hello koleksiyonunda *settings.xml* dosya; örneğin:</span><span class="sxs-lookup"><span data-stu-id="c4a8a-141">Add your Azure service principal settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="c4a8a-142">Konumlar:</span><span class="sxs-lookup"><span data-stu-id="c4a8a-142">Where:</span></span>
   <span data-ttu-id="c4a8a-143">Öğesi</span><span class="sxs-lookup"><span data-stu-id="c4a8a-143">Element</span></span> | <span data-ttu-id="c4a8a-144">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c4a8a-144">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="c4a8a-145">Web uygulaması tooAzure dağıttığınızda, Maven toolook, güvenlik ayarlarını kullanan benzersiz bir ad belirtir.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-145">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="c4a8a-146">Merhaba içeren `appId` hizmet sorumlusu değeri.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-146">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="c4a8a-147">Merhaba içeren `tenant` hizmet sorumlusu değeri.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-147">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="c4a8a-148">Merhaba içeren `password` hizmet sorumlusu değeri.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-148">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="c4a8a-149">Olan hello hedef Azure bulut ortamı tanımlar `AZURE` Bu örnekte.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-149">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="c4a8a-150">(Tam bir listesi ortamlarının hello kullanılabilir [Azure Web uygulamaları için Maven eklentisi] belgeleri)</span><span class="sxs-lookup"><span data-stu-id="c4a8a-150">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="c4a8a-151">Kaydet ve Kapat hello *settings.xml* dosya.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-151">Save and close hello *settings.xml* file.</span></span>

## <a name="optional-deploy-your-local-docker-file-toodocker-hub"></a><span data-ttu-id="c4a8a-152">İsteğe bağlı: yerel, Docker dosya tooDocker hub'ı dağıtma</span><span class="sxs-lookup"><span data-stu-id="c4a8a-152">OPTIONAL: Deploy your local Docker file tooDocker Hub</span></span>

<span data-ttu-id="c4a8a-153">Docker hesabınız varsa, Docker kapsayıcısı görüntüsünü yerel olarak oluşturabilirsiniz ve tooDocker Hub gönderme.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-153">If you have a Docker account, you can build your Docker container image locally and push it tooDocker Hub.</span></span> <span data-ttu-id="c4a8a-154">toodo, bu nedenle, hello aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-154">toodo so, use hello following steps.</span></span>

1. <span data-ttu-id="c4a8a-155">Açık hello `pom.xml` dosyasını bir metin düzenleyicisinde yay önyükleme uygulamanız için.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-155">Open hello `pom.xml` file for your Spring Boot application in a text editor.</span></span>

1. <span data-ttu-id="c4a8a-156">Merhaba bulun `<imageName>` hello alt öğesi `<containerSettings>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-156">Locate hello `<imageName>` child element of hello `<containerSettings>` element.</span></span>

1. <span data-ttu-id="c4a8a-157">Güncelleştirme hello `${docker.image.prefix}` Docker hesap adınızı değerle:</span><span class="sxs-lookup"><span data-stu-id="c4a8a-157">Update hello `${docker.image.prefix}` value with your Docker account name:</span></span>
   ```xml
   <containerSettings>
      <imageName>mydockeraccountname/${project.artifactId}</imageName>
   </containerSettings>
   ```

1. <span data-ttu-id="c4a8a-158">Dağıtım yöntemleri aşağıdaki hello birini seçin:</span><span class="sxs-lookup"><span data-stu-id="c4a8a-158">Choose one of hello following deployment methods:</span></span>

   * <span data-ttu-id="c4a8a-159">Kapsayıcı görüntünüzü Maven ile yerel olarak oluşturun ve ardından Docker toopush, kapsayıcı tooDocker Hub kullanın:</span><span class="sxs-lookup"><span data-stu-id="c4a8a-159">Build your container image locally with Maven, and then use Docker toopush your container tooDocker Hub:</span></span>
      ```shell
      mvn clean package docker:build
      docker push
      ```
   
   * <span data-ttu-id="c4a8a-160">Merhaba varsa [Maven için Docker eklentisi] yüklü, otomatik olarak oluşturabilir ve kullanarak, kapsayıcı görüntü tooDocker Hub hello `-DpushImage` parametre:</span><span class="sxs-lookup"><span data-stu-id="c4a8a-160">If you have hello [Docker plugin for Maven] installed, you can automatically build and your container image tooDocker Hub by using hello `-DpushImage` parameter:</span></span>
      ```shell
      mvn clean package docker:build -DpushImage
      ```

## <a name="optional-customize-your-pomxml-before-deploying-your-container-tooazure"></a><span data-ttu-id="c4a8a-161">İsteğe bağlı:, pom.xml kapsayıcı tooAzure dağıtmadan önce özelleştirme</span><span class="sxs-lookup"><span data-stu-id="c4a8a-161">OPTIONAL: Customize your pom.xml before deploying your container tooAzure</span></span>

<span data-ttu-id="c4a8a-162">Açık hello `pom.xml` dosyasını bir metin düzenleyicisinde yay önyükleme uygulamanız için ve hello bulun `<plugin>` öğesi için `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-162">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="c4a8a-163">Bu öğe aşağıdaki örneğine hello benzemelidir:</span><span class="sxs-lookup"><span data-stu-id="c4a8a-163">This element should resemble hello following example:</span></span>

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
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="c4a8a-164">Merhaba Maven eklentisi için değiştirebileceğiniz birkaç değer vardır ve bu öğelerin her biri için ayrıntılı bir açıklama hello kullanılabilir [Azure Web uygulamaları için Maven eklentisi] belgeleri.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-164">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="c4a8a-165">Denirse, bu makaledeki vurgulama değer olan birkaç değerleri vardır:</span><span class="sxs-lookup"><span data-stu-id="c4a8a-165">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="c4a8a-166">Öğesi</span><span class="sxs-lookup"><span data-stu-id="c4a8a-166">Element</span></span> | <span data-ttu-id="c4a8a-167">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c4a8a-167">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="c4a8a-168">Merhaba Hello sürümünü belirtir [Azure Web uygulamaları için Maven eklentisi].</span><span class="sxs-lookup"><span data-stu-id="c4a8a-168">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="c4a8a-169">Hello listelenen hello sürüm denetlemelisiniz [Maven merkezi depo](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) kullanmakta olduğunuz tooensure hello en son sürümü.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-169">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="c4a8a-170">Merhaba kimlik doğrulama bilgilerini içeren bu örnekte Azure belirtir bir `<serverId>` içeren öğeyi `azure-auth`; Maven Maven içinde bu değer toolook hello Azure hizmet asıl değerleri kullanan *settings.xml* bu makalenin önceki bölümde tanımlanan dosya.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-170">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="c4a8a-171">Olan hello hedef kaynak grubu belirtir `maven-plugin` Bu örnekte.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-171">Specifies hello target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="c4a8a-172">zaten yoksa, dağıtım sırasında hello kaynak grubu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-172">hello resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="c4a8a-173">Web uygulamanız için Hello hedef adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-173">Specifies hello target name for your web app.</span></span> <span data-ttu-id="c4a8a-174">Bu örnekte hello hedef adıdır `maven-linux-app-${maven.build.timestamp}`, hello burada `${maven.build.timestamp}` soneki, bu örnek tooavoid çakışması eklenir.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-174">In this example, hello target name is `maven-linux-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="c4a8a-175">(Merhaba zaman damgası isteğe bağlıdır; hello uygulama adı için benzersiz bir dize belirtin.)</span><span class="sxs-lookup"><span data-stu-id="c4a8a-175">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="c4a8a-176">Olan bu örnekte hello hedef bölgesi belirtir `westus`.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-176">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="c4a8a-177">(Tam bir liste hello olan [Azure Web uygulamaları için Maven eklentisi] belgelerine.)</span><span class="sxs-lookup"><span data-stu-id="c4a8a-177">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<appSettings>` | <span data-ttu-id="c4a8a-178">Web uygulaması tooAzure dağıtırken Maven toouse benzersiz ayarlarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-178">Specifies any unique settings for Maven toouse when deploying your web app tooAzure.</span></span> <span data-ttu-id="c4a8a-179">Bu örnekte, bir `<property>` öğesi içeren bir ad/değer çifti alt öğelerinin uygulamanızı hello bağlantı noktasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-179">In this example, a `<property>` element contains a name/value pair of child elements that specify hello port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="c4a8a-180">Hello ayarları toochange hello bağlantı noktası numarasını bu örnekte yalnızca gerekli olan hello varsayılandan hello noktası değiştirilirken.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-180">hello settings toochange hello port number in this example are only necessary when you are changing hello port from hello default.</span></span>
>

## <a name="build-and-deploy-your-container-tooazure"></a><span data-ttu-id="c4a8a-181">Derleme ve kapsayıcı tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="c4a8a-181">Build and deploy your container tooAzure</span></span>

<span data-ttu-id="c4a8a-182">Bölümler, bu makalenin önceki hello tüm hello ayarlarını yapılandırdıktan sonra hazır toodeploy olan kapsayıcı tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-182">Once you have configured all of hello settings in hello preceding sections of this article, you are ready toodeploy your container tooAzure.</span></span> <span data-ttu-id="c4a8a-183">toodo, bu nedenle, hello aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="c4a8a-183">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="c4a8a-184">Merhaba komut istemi veya daha önce kullandığınız terminal penceresinden, tüm değişiklikleri toohello yaptıysanız Maven kullanarak hello JAR dosyasını yeniden *pom.xml* dosya; örneğin:</span><span class="sxs-lookup"><span data-stu-id="c4a8a-184">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="c4a8a-185">Web uygulaması tooAzure Maven kullanarak dağıtabilirsiniz; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="c4a8a-185">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="c4a8a-186">Maven web uygulama tooAzure dağıtacağınız; Merhaba web uygulaması zaten mevcut değilse oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-186">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="c4a8a-187">Varsa hello belirten hello bölge `<region>` öğesi, *pom.xml* dağıtımınızı başlattığınızda dosya sunucuları yeterli yok, aşağıdaki örnek bir hata benzer toohello görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c4a8a-187">If hello region which you specify in hello `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar toohello following example:</span></span>
>
> ```
> [INFO] Start deploying tooWeb App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed tooexecute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> <span data-ttu-id="c4a8a-188">Bu durumda, başka bir bölgeye ve yeniden çalıştırın, uygulamanızın Maven komutunu toodeploy hello belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-188">If this happens, you can specify another region and re-run hello Maven command toodeploy your application.</span></span>
>
>

<span data-ttu-id="c4a8a-189">Web dağıtıldığında mümkün toomanage olacaktır hello kullanarak [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="c4a8a-189">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="c4a8a-190">Web uygulamanızı listelenen **uygulama hizmetleri**:</span><span class="sxs-lookup"><span data-stu-id="c4a8a-190">Your web app will be listed in **App Services**:</span></span>

   ![Azure portalında uygulama hizmetleri listelenen web uygulaması][AP01]

* <span data-ttu-id="c4a8a-192">Ve web uygulamanızı hello listelenir URL hello **genel bakış** web uygulamanız için:</span><span class="sxs-lookup"><span data-stu-id="c4a8a-192">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c4a8a-194">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c4a8a-194">Next steps</span></span>

<span data-ttu-id="c4a8a-195">Bu makalede ele alınan çeşitli teknolojiler hello hakkında daha fazla bilgi makaleleri aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="c4a8a-195">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="c4a8a-196">[Azure Web uygulamaları için Maven eklentisi]</span><span class="sxs-lookup"><span data-stu-id="c4a8a-196">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="c4a8a-197">TooAzure hello Azure CLI gelen oturum</span><span class="sxs-lookup"><span data-stu-id="c4a8a-197">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="c4a8a-198">Nasıl toouse hello Maven eklentisi için Azure Web Apps toodeploy yay önyükleme uygulama tooAzure uygulama hizmeti</span><span class="sxs-lookup"><span data-stu-id="c4a8a-198">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app tooAzure App Service </span></span>](app-service-web-deploy-spring-boot-app-with-maven-plugin.md)

* [<span data-ttu-id="c4a8a-199">Bir Azure hizmet sorumlusu Azure CLI 2.0 ile oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c4a8a-199">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="c4a8a-200">Maven ayarları başvurusu</span><span class="sxs-lookup"><span data-stu-id="c4a8a-200">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="c4a8a-201">[Maven için Docker eklentisi]</span><span class="sxs-lookup"><span data-stu-id="c4a8a-201">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[Azure komut satırı arabirimi (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Docker]: https://www.docker.com/
[Maven için Docker eklentisi]: https://github.com/spotify/docker-maven-plugin
[ücretsiz Azure hesabı]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN abone Avantajlarınızı]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Docker Başlarken yay önyüklemede]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Azure Web uygulamaları için Maven eklentisi]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP02.png
