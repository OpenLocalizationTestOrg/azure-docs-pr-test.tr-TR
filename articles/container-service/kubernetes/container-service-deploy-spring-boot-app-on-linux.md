---
title: "aaaDeploy Linux Azure kapsayıcı Hizmeti'nde bir yay önyükleme Web uygulaması | Microsoft Docs"
description: "Bu öğreticide, ancak Microsoft Azure'da hello adımları toodeploy yay önyükleme uygulama Linux web uygulaması olarak açıklanmaktadır."
services: container-service
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: container-service
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 2c44be1c7f66a38f48239001f0be9e90c7e6edef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-linux-in-hello-azure-container-service"></a><span data-ttu-id="ce5ef-103">Linux'ta hello Azure kapsayıcı hizmeti bir yay önyükleme uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="ce5ef-103">Deploy a Spring Boot application on Linux in hello Azure Container Service</span></span>

<span data-ttu-id="ce5ef-104">Merhaba  **[yay Framework]**  Java geliştiriciler kuruluş düzeyinde uygulamalar oluşturmanıza yardımcı olan bir açık kaynaklı bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-104">hello **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="ce5ef-105">Yerleşik hello daha popüler projelerden biri üzerinde üst o platformudur [yay önyükleme], tek başına Java uygulamaları oluşturmak için basitleştirilmiş bir yaklaşım sağlar.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="ce5ef-106">**[Docker]**  olan geliştiricilere yardımcı açık kaynak çözümleri otomatikleştirmek hello dağıtım, ölçeklendirme ve kapsayıcılarında çalışan kendi uygulamalarını yönetimi.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-106">**[Docker]** is open-source solutions that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="ce5ef-107">Bu öğretici Docker toodevelop kullanarak kılavuzluk ve hello bir yay önyükleme uygulama tooa Linux ana dağıtma [Azure kapsayıcı Hizmeti'ni (ACS)].</span><span class="sxs-lookup"><span data-stu-id="ce5ef-107">This tutorial walks you through using Docker toodevelop and deploy a Spring Boot application tooa Linux host in hello [Azure Container Service (ACS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce5ef-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ce5ef-108">Prerequisites</span></span>

<span data-ttu-id="ce5ef-109">Sipariş toocomplete hello adımlarda Bu öğreticide, Önkoşullar aşağıdaki toohave hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="ce5ef-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="ce5ef-110">Bir Azure aboneliği; bir Azure aboneliği zaten sahip değilseniz, etkinleştirebilir, [MSDN abone Avantajlarınızı] veya kaydolun bir [ücretsiz Azure hesabı].</span><span class="sxs-lookup"><span data-stu-id="ce5ef-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="ce5ef-111">Merhaba [Azure komut satırı arabirimi (CLI)].</span><span class="sxs-lookup"><span data-stu-id="ce5ef-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="ce5ef-112">Güncel bir [Java Geliştirme Seti (JDK)].</span><span class="sxs-lookup"><span data-stu-id="ce5ef-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="ce5ef-113">Apache'nın [Maven] aracını (sürüm 3) yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="ce5ef-114">A [Git] istemci.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-114">A [Git] client.</span></span>
* <span data-ttu-id="ce5ef-115">A [Docker] istemci.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="ce5ef-116">Toohello sanallaştırma gereksinimleri Bu öğreticinin bir sanal makinede bu makalede hello adımları izleyin olamaz; sanallaştırma özellikleri etkin bir fiziksel bilgisayar kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="ce5ef-117">Hello yay önyükleme Docker Başlarken web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="ce5ef-117">Create hello Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="ce5ef-118">Merhaba aşağıdaki adımlar, gerekli toocreate basit bir yay önyükleme web uygulaması ve yerel olarak test hello adımlarda size yol.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-118">hello following steps walk you through hello steps that are required toocreate a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="ce5ef-119">Bir komut istemi açın ve yerel dizin toohold uygulama ve değişiklik toothat dizin oluşturun; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ce5ef-119">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="ce5ef-120">--ya da--</span><span class="sxs-lookup"><span data-stu-id="ce5ef-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="ce5ef-121">Kopya hello [Docker Başlarken yay önyüklemede] örnek proje hello dizinine oluşturduğunuz; örneğin:</span><span class="sxs-lookup"><span data-stu-id="ce5ef-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="ce5ef-122">Dizin tamamlandı toohello proje Değiştir; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ce5ef-122">Change directory toohello completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="ce5ef-123">Maven kullanarak hello JAR dosyasını oluşturun; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ce5ef-123">Build hello JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="ce5ef-124">Merhaba web uygulaması oluşturulduktan sonra dizin toohello değiştirmek `target` burada hello JAR dosyasını bulunur ve hello web uygulaması; başlangıç dizini örneğin:</span><span class="sxs-lookup"><span data-stu-id="ce5ef-124">Once hello web app has been created, change directory toohello `target` directory where hello JAR file is located and start hello web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="ce5ef-125">Merhaba web uygulaması, bir web tarayıcısı kullanarak yerel olarak tooit göz atarak sınayın.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-125">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="ce5ef-126">Varsa, örneğin, curl kullanılabilir ve hello Tomcat sunucu toorun bağlantı noktası 80 üzerinde yapılandırılmış:</span><span class="sxs-lookup"><span data-stu-id="ce5ef-126">For example, if you have curl available and you configured hello Tomcat server toorun on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="ce5ef-127">Görüntülenen iletiden hello görmeniz gerekir: **Docker Merhaba Dünya!**</span><span class="sxs-lookup"><span data-stu-id="ce5ef-127">You should see hello following message displayed: **Hello Docker World!**</span></span>

   ![Örnek uygulamayı yerel olarak göz atın][SB01]

## <a name="create-an-azure-container-registry-toouse-as-a-private-docker-registry"></a><span data-ttu-id="ce5ef-129">Bir Azure kapsayıcı kayıt defteri toouse özel bir Docker kayıt defteri oluşturma</span><span class="sxs-lookup"><span data-stu-id="ce5ef-129">Create an Azure Container Registry toouse as a Private Docker Registry</span></span>

<span data-ttu-id="ce5ef-130">Merhaba aşağıdaki adımlar hello Azure portal toocreate Azure kapsayıcı kayıt defteri kullanılarak üzerinden yol.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-130">hello following steps walk you through using hello Azure portal toocreate an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="ce5ef-131">Hello Azure portal yerine toouse hello Azure CLI istiyorsanız hello adımları [hello Azure CLI 2.0 kullanarak özel bir Docker kapsayıcısı kayıt](../../container-registry/container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ce5ef-131">If you want toouse hello Azure CLI instead of hello Azure portal, follow hello steps in [Create a private Docker container registry using hello Azure CLI 2.0](../../container-registry/container-registry-get-started-azure-cli.md).</span></span>
>

1. <span data-ttu-id="ce5ef-132">Toohello Gözat [Azure portal] ve oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-132">Browse toohello [Azure portal] and sign in.</span></span>

   <span data-ttu-id="ce5ef-133">Hello Azure portalı üzerinde tooyour hesabında oturum açtıktan sonra hello hello adımları takip edebilirsiniz [hello Azure portal kullanarak özel bir Docker kapsayıcısı kayıt] hello için adımlara hello açıklanır makale artırmak amacıyla expediency biri.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-133">Once you have signed in tooyour account on hello Azure portal, you can follow hello steps in hello [Create a private Docker container registry using hello Azure portal] article, which are paraphrased in hello following steps for hello sake of expediency.</span></span>

1. <span data-ttu-id="ce5ef-134">Merhaba menü simgesini **+ yeni**, ardından **kapsayıcıları**ve ardından **Azure kapsayıcı kayıt defteri**.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-134">Click hello menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Yeni bir Azure kapsayıcı kayıt defteri oluşturma][AR01]

1. <span data-ttu-id="ce5ef-136">Hello Azure kapsayıcı kayıt defteri şablonu için başlangıç bilgileri sayfası görüntülendiğinde tıklayın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-136">When hello information page for hello Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Yeni bir Azure kapsayıcı kayıt defteri oluşturma][AR02]

1. <span data-ttu-id="ce5ef-138">Ne zaman hello **oluşturma kapsayıcı kayıt defteri** sayfası görüntülenirse, girin, **kayıt defteri adı** ve **kaynak grubu**, seçin **etkinleştirmek** için Merhaba **yönetici kullanıcı**ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-138">When hello **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for hello **Admin user**, and then click **Create**.</span></span>

   ![Azure kapsayıcı kayıt defteri ayarlarını yapılandırma][AR03]

1. <span data-ttu-id="ce5ef-140">Kapsayıcı kaydınız oluşturulduktan sonra tooyour kapsayıcı kayıt defterinde hello Azure portalına gidin ve ardından **erişim tuşları**.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-140">Once your container registry has been created, navigate tooyour container registry in hello Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="ce5ef-141">Merhaba kullanıcı adı ve parola hello sonraki adımlar için not edin.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-141">Take note of hello username and password for hello next steps.</span></span>

   ![Azure kapsayıcı kayıt defteri erişim tuşları][AR04]

## <a name="configure-maven-toouse-your-azure-container-registry-access-keys"></a><span data-ttu-id="ce5ef-143">Azure kapsayıcı kayıt defteri erişim tuşlarınızı Maven toouse yapılandırın</span><span class="sxs-lookup"><span data-stu-id="ce5ef-143">Configure Maven toouse your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="ce5ef-144">Maven yüklemenizi toohello yapılandırma dizinine gidin ve açmak hello *settings.xml* dosyasını bir metin düzenleyicisiyle.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-144">Navigate toohello configuration directory for your Maven installation and open hello *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="ce5ef-145">Azure kapsayıcı kayıt defteri erişim ayarlarınız hello önceki Bu öğretici toohello bölümünden eklemek `<servers>` hello koleksiyonunda *settings.xml* dosya; örneğin:</span><span class="sxs-lookup"><span data-stu-id="ce5ef-145">Add your Azure Container Registry access settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="ce5ef-146">Yay önyükleme uygulamanız için tamamlandı toohello proje dizinine gidin (örneğin: "*C:\SpringBoot\gs-spring-boot-docker\complete*"veya"*/users/robert/SpringBoot/gs-spring-boot-docker / tam*") ve açık hello *pom.xml* dosyasını bir metin düzenleyicisiyle.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-146">Navigate toohello completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="ce5ef-147">Güncelleştirme hello `<properties>` hello koleksiyonunda *pom.xml* hello oturum açma sunucusu değeri bir dosyayla, Azure kapsayıcı kayıt defteri hello önceki bölümdeki Bu öğreticinin; örneğin:</span><span class="sxs-lookup"><span data-stu-id="ce5ef-147">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry from hello previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="ce5ef-148">Güncelleştirme hello `<plugins>` hello koleksiyonunda *pom.xml* , hello şekilde dosya `<plugin>` hello oturum açma sunucusu adresi ve kayıt defteri adı için bu öğreticinin önceki bölümdeki hello Azure kapsayıcı kayıt içerir.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-148">Update hello `<plugins>` collection in hello *pom.xml* file so that hello `<plugin>` contains hello login server address and registry name for your Azure Container Registry from hello previous section of this tutorial.</span></span> <span data-ttu-id="ce5ef-149">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ce5ef-149">For example:</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. <span data-ttu-id="ce5ef-150">Yay önyükleme uygulamanız için tamamlandı toohello proje dizinine gidin ve komut toorebuild Merhaba uygulaması aşağıdaki hello çalıştırın ve hello kapsayıcı tooyour Azure kapsayıcı kayıt defteri gönderme:</span><span class="sxs-lookup"><span data-stu-id="ce5ef-150">Navigate toohello completed project directory for your Spring Boot application and run hello following command toorebuild hello application and push hello container tooyour Azure Container Registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> <span data-ttu-id="ce5ef-151">Docker kapsayıcısı tooAzure Ftp'den, Docker kapsayıcısı başarıyla oluşturuldu olsa bile, hello aşağıdaki benzer tooone bir hata iletisi alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ce5ef-151">When you are pushing your Docker container tooAzure, you may receive an error message that is similar tooone of hello following even though your Docker container was created successfully:</span></span>
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="ce5ef-152">Bu durumda, tooyour hello Docker komut satırından Azure hesabı toosign gerekebilir; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ce5ef-152">If this happens, you may need toosign in tooyour Azure account from hello Docker command line; for example:</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="ce5ef-153">Ardından, kapsayıcı hello komut satırından anında; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ce5ef-153">You can then push your container from hello command line; for example:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="ce5ef-154">Linux kapsayıcı görüntünüzü kullanarak Azure App Service'te bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="ce5ef-154">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="ce5ef-155">Toohello Gözat [Azure portal] ve oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-155">Browse toohello [Azure portal] and sign in.</span></span>

1. <span data-ttu-id="ce5ef-156">Merhaba menü simgesini **+ yeni**, ardından **Web + mobil**ve ardından **Linux üzerinde Web uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-156">Click hello menu icon for **+ New**, then click **Web + Mobile**, and then click **Web App on Linux**.</span></span>
   
   ![Hello Azure portalında yeni bir web uygulaması oluşturma][LX01]

1. <span data-ttu-id="ce5ef-158">Ne zaman hello **Linux üzerinde Web uygulaması** sayfası görüntülenirse, aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="ce5ef-158">When hello **Web App on Linux** page is displayed, enter hello following information:</span></span>

   <span data-ttu-id="ce5ef-159">a.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-159">a.</span></span> <span data-ttu-id="ce5ef-160">Hello için benzersiz bir ad girin **uygulama adı**; örneğin: "*wingtiptoyslinux*."</span><span class="sxs-lookup"><span data-stu-id="ce5ef-160">Enter a unique name for hello **App name**; for example: "*wingtiptoyslinux*."</span></span>

   <span data-ttu-id="ce5ef-161">b.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-161">b.</span></span> <span data-ttu-id="ce5ef-162">Seçin, **abonelik** hello aşağı açılan listeden.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-162">Choose your **Subscription** from hello drop-down list.</span></span>

   <span data-ttu-id="ce5ef-163">c.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-163">c.</span></span> <span data-ttu-id="ce5ef-164">Var olan seçin **kaynak grubu**, veya bir ad toocreate yeni bir kaynak grubu belirtin.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-164">Choose an existing **Resource Group**, or specify a name toocreate a new resource group.</span></span>

   <span data-ttu-id="ce5ef-165">d.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-165">d.</span></span> <span data-ttu-id="ce5ef-166">Tıklatın **yapılandırma kapsayıcısı** ve aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="ce5ef-166">Click **Configure container** and enter hello following information:</span></span>

      * <span data-ttu-id="ce5ef-167">Seçin **özel kayıt defteri**.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-167">Choose **Private registry**.</span></span>

      * <span data-ttu-id="ce5ef-168">**Görüntü ve isteğe bağlı etiket**: daha önce; Örneğin, kapsayıcı adı belirtin: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span><span class="sxs-lookup"><span data-stu-id="ce5ef-168">**Image and optional tag**: Specify your container name from earlier; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span></span>

      * <span data-ttu-id="ce5ef-169">**Sunucu URL'si**: kayıt defteri URL'den belirtin önceki; örneğin: "*https://wingtiptoysregistry.azurecr.io*"</span><span class="sxs-lookup"><span data-stu-id="ce5ef-169">**Server URL**: Specify your registry URL from earlier; for example: "*https://wingtiptoysregistry.azurecr.io*"</span></span>

      * <span data-ttu-id="ce5ef-170">**Oturum açma kullanıcı** ve **parola**: oturum açma kimlik bilgilerinizi belirtin, **erişim tuşları** önceki adımlarda kullanılan.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-170">**Login username** and **Password**: Specify your login credentials from your **Access Keys** that you used in previous steps.</span></span>
   
   <span data-ttu-id="ce5ef-171">e.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-171">e.</span></span> <span data-ttu-id="ce5ef-172">Tüm bilgileri yukarıda hello girdikten sonra tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-172">Once you have entered all of hello above information, click **OK**.</span></span>

   ![Web uygulaması ayarlarını yapılandır][LX02]

1. <span data-ttu-id="ce5ef-174">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-174">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="ce5ef-175">Azure hello standart bağlantı noktaları 80 veya 8080 üzerinde çalışan Internet istekleri tooembedded Tomcat sunucusunu otomatik olarak eşlenir.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-175">Azure will automatically map Internet requests tooembedded Tomcat server that is running on hello standard ports of 80 or 8080.</span></span> <span data-ttu-id="ce5ef-176">Ancak, özel bir bağlantı noktası üzerinde katıştırılmış Tomcat sunucu toorun yapılandırdıysanız, tooadd katıştırılmış Tomcat sunucunuz için başlangıç bağlantı noktası tanımlayan bir ortam değişken tooyour web uygulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-176">However, if you configured your embedded Tomcat server toorun on a custom port, you need tooadd an environment variable tooyour web app that defines hello port for your embedded Tomcat server.</span></span> <span data-ttu-id="ce5ef-177">toodo, bu nedenle, hello aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="ce5ef-177">toodo so, use hello following steps:</span></span>
>
> 1. <span data-ttu-id="ce5ef-178">Toohello Gözat [Azure portal] ve oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-178">Browse toohello [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="ce5ef-179">Merhaba simgesini **uygulama hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-179">Click hello icon for **App Services**.</span></span> <span data-ttu-id="ce5ef-180">(Aşağıdaki hello görüntü #1 öğesinde bakın.)</span><span class="sxs-lookup"><span data-stu-id="ce5ef-180">(See item #1 in hello image below.)</span></span>
>
> 3. <span data-ttu-id="ce5ef-181">Web uygulamanızı hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-181">Select your web app from hello list.</span></span> <span data-ttu-id="ce5ef-182">(Aşağıdaki hello görüntü #2 öğe.)</span><span class="sxs-lookup"><span data-stu-id="ce5ef-182">(Item #2 in hello image below.)</span></span>
>
> 4. <span data-ttu-id="ce5ef-183">Tıklatın **uygulama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-183">Click **Application Settings**.</span></span> <span data-ttu-id="ce5ef-184">(Aşağıdaki hello görüntü #3 öğe.)</span><span class="sxs-lookup"><span data-stu-id="ce5ef-184">(Item #3 in hello image below.)</span></span>
>
> 5. <span data-ttu-id="ce5ef-185">Merhaba, **uygulama ayarları** bölümünde, adlı yeni bir ortam değişkeni ekleyin **bağlantı noktası** ve hello değeri için özel bağlantı noktası numarası girin.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-185">In hello **App settings** section, add a new environment variable named **PORT** and enter your custom port number for hello value.</span></span> <span data-ttu-id="ce5ef-186">(Aşağıdaki hello görüntü #4 öğe.)</span><span class="sxs-lookup"><span data-stu-id="ce5ef-186">(Item #4 in hello image below.)</span></span>
>
> 6. <span data-ttu-id="ce5ef-187">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-187">Click **Save**.</span></span> <span data-ttu-id="ce5ef-188">(Aşağıdaki hello görüntü #5 öğe.)</span><span class="sxs-lookup"><span data-stu-id="ce5ef-188">(Item #5 in hello image below.)</span></span>
>
> ![Özel bir bağlantı noktası hello Azure portalına kaydediliyor][LX03]
>

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

## <a name="next-steps"></a><span data-ttu-id="ce5ef-190">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ce5ef-190">Next steps</span></span>

<span data-ttu-id="ce5ef-191">Azure üzerinde yay önyükleme uygulamalarında kullanma hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="ce5ef-191">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="ce5ef-192">Yay önyükleme uygulama toohello Azure App Service'e dağıtma</span><span class="sxs-lookup"><span data-stu-id="ce5ef-192">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="ce5ef-193">Hello Azure kapsayıcı hizmeti Kubernetes kümesinde yay önyükleme uygulamasını dağıtma</span><span class="sxs-lookup"><span data-stu-id="ce5ef-193">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="ce5ef-194">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi] ve hello [Visual Studio Team Services için Java Araçları].</span><span class="sxs-lookup"><span data-stu-id="ce5ef-194">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="ce5ef-195">Docker örnek proje üzerinde hello yay önyükleme hakkında daha fazla ayrıntı için bkz: [Docker Başlarken yay önyüklemede].</span><span class="sxs-lookup"><span data-stu-id="ce5ef-195">For further details about hello Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="ce5ef-196">Hello kendi yay önyükleme uygulamaları ile çalışmaya başlama hakkında bilgi için bkz: **yay Initializr** https://start.spring.io/ adresindeki.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-196">For help with getting started with your own Spring Boot applications, see hello **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="ce5ef-197">Basit bir yay önyükleme uygulaması oluşturma ile çalışmaya başlama hakkında daha fazla bilgi için hello yay Initializr https://start.spring.io/ adresindeki bakın.</span><span class="sxs-lookup"><span data-stu-id="ce5ef-197">For more information about getting started with creating a simple Spring Boot application, see hello Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="ce5ef-198">Toouse özel Docker Azure ile nasıl görüntüler için ek örnekler için bkz: [Linux Azure Web uygulaması için özel bir Docker görüntü kullanarak].</span><span class="sxs-lookup"><span data-stu-id="ce5ef-198">For additional examples for how toouse custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Azure komut satırı arabirimi (CLI)]: /cli/azure/overview
[Azure kapsayıcı Hizmeti'ni (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[hello Azure portal kullanarak özel bir Docker kapsayıcısı kayıt]: /azure/container-registry/container-registry-get-started-portal
[Linux Azure Web uygulaması için özel bir Docker görüntü kullanarak]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[ücretsiz Azure hesabı]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Geliştirme Seti (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Visual Studio Team Services için Java Araçları]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN abone Avantajlarınızı]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[yay önyükleme]: http://projects.spring.io/spring-boot/
[Docker Başlarken yay önyüklemede]: https://github.com/spring-guides/gs-spring-boot-docker
[yay Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-linux/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-linux/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-linux/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-linux/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-linux/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-linux/AR04.png

[LX01]: ./media/container-service-deploy-spring-boot-app-on-linux/LX01.png
[LX02]: ./media/container-service-deploy-spring-boot-app-on-linux/LX02.png
[LX03]: ./media/container-service-deploy-spring-boot-app-on-linux/LX03.png
