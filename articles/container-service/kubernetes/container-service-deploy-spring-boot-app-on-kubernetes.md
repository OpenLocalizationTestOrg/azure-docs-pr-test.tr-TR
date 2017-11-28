---
title: "aaaDeploy Kubernetes Azure kapsayıcı Hizmeti'nde bir yay önyükleme uygulamasını | Microsoft Docs"
description: "Bu öğretici Microsoft Azure üzerinde bir Kubernetes kümede ancak hello adımları toodeploy yay önyükleme uygulama anlatılmaktadır."
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
ms.openlocfilehash: 2bf9df459f874a1f478f43cdd29992d86c370837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-hello-azure-container-service"></a><span data-ttu-id="9e2d4-103">Hello Azure kapsayıcı hizmeti Kubernetes kümesinde yay önyükleme uygulamasını dağıtma</span><span class="sxs-lookup"><span data-stu-id="9e2d4-103">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>

<span data-ttu-id="9e2d4-104">Merhaba  **[yay Framework]**  , Java geliştiricilerinin web, mobil ve API uygulamaları oluşturma yardımcı olan bir popüler açık kaynak çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-104">hello **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="9e2d4-105">Bu öğretici kullanılarak oluşturulmuş bir örnek uygulama kullanır [yay önyükleme], kuralı güdümlü bir yaklaşım yay tooget kullanma çalışmaya hızla.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring tooget started quickly.</span></span>

<span data-ttu-id="9e2d4-106">**[Kubernetes]**  ve  **[Docker]**  olan, geliştiricilerin açık kaynak çözümleri otomatikleştirmek hello dağıtım, ölçeklendirme ve çalışan kendi uygulamalarını Yönetimi kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-106">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate hello deployment, scaling, and management of their applications  running in containers.</span></span>

<span data-ttu-id="9e2d4-107">Bu öğretici, bu iki yaygın olarak kullanılan, açık kaynak teknolojisi toodevelop birleştirme olsa açıklanmaktadır ve yay önyükleme uygulama tooMicrosoft Azure dağıtın.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-107">This tutorial walks you though combining these two popular, open-source technologies toodevelop and deploy a Spring Boot application tooMicrosoft Azure.</span></span> <span data-ttu-id="9e2d4-108">Daha belirgin olarak kullandığınız  *[yay önyükleme]*  uygulama geliştirme için  *[Kubernetes]*  kapsayıcı dağıtım ve hello [Azure kapsayıcı Hizmeti'ni (ACS)] toohost uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-108">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and hello [Azure Container Service (ACS)] toohost your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="9e2d4-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9e2d4-109">Prerequisites</span></span>

* <span data-ttu-id="9e2d4-110">Bir Azure aboneliği; bir Azure aboneliği zaten sahip değilseniz, etkinleştirebilir, [MSDN abone Avantajlarınızı] veya kaydolun bir [ücretsiz Azure hesabı].</span><span class="sxs-lookup"><span data-stu-id="9e2d4-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="9e2d4-111">Merhaba [Azure komut satırı arabirimi (CLI)].</span><span class="sxs-lookup"><span data-stu-id="9e2d4-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="9e2d4-112">Güncel bir [Java Geliştirme Seti (JDK)].</span><span class="sxs-lookup"><span data-stu-id="9e2d4-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="9e2d4-113">Apache'nın [Maven] aracını (sürüm 3) yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="9e2d4-114">A [Git] istemci.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-114">A [Git] client.</span></span>
* <span data-ttu-id="9e2d4-115">A [Docker] istemci.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="9e2d4-116">Toohello sanallaştırma gereksinimleri Bu öğreticinin bir sanal makinede bu makalede hello adımları izleyin olamaz; sanallaştırma özellikleri etkin bir fiziksel bilgisayar kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="9e2d4-117">Hello yay önyükleme Docker Başlarken web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="9e2d4-117">Create hello Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="9e2d4-118">Aşağıdaki adımları hello yay önyükleme web uygulaması oluşturma ve yerel olarak test size yol.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-118">hello following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="9e2d4-119">Bir komut istemi açın ve yerel dizin toohold uygulama ve değişiklik toothat dizin oluşturun; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="9e2d4-119">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="9e2d4-120">--ya da--</span><span class="sxs-lookup"><span data-stu-id="9e2d4-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="9e2d4-121">Kopya hello [Docker Başlarken yay önyüklemede] örnek proje hello dizine.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="9e2d4-122">Dizin tamamlandı toohello proje değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-122">Change directory toohello completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="9e2d4-123">Maven toobuild ve çalışma hello örnek uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-123">Use Maven toobuild and run hello sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="9e2d4-124">Test hello web uygulaması toohttp://localhost:8080 gözatarak veya hello aşağıdaki `curl` komutu:</span><span class="sxs-lookup"><span data-stu-id="9e2d4-124">Test hello web app by browsing toohttp://localhost:8080, or with hello following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="9e2d4-125">Görüntülenen iletiden hello görmeniz gerekir: **Docker Hello World**</span><span class="sxs-lookup"><span data-stu-id="9e2d4-125">You should see hello following message displayed: **Hello Docker World**</span></span>

   ![Örnek uygulamayı yerel olarak göz atın][SB01]

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a><span data-ttu-id="9e2d4-127">Azure kapsayıcı hello Azure CLI kullanarak bir kayıt oluşturun</span><span class="sxs-lookup"><span data-stu-id="9e2d4-127">Create an Azure Container Registry using hello Azure CLI</span></span>

1. <span data-ttu-id="9e2d4-128">Bir komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-128">Open a command prompt.</span></span>

1. <span data-ttu-id="9e2d4-129">Azure hesabı tooyour oturum:</span><span class="sxs-lookup"><span data-stu-id="9e2d4-129">Log in tooyour Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="9e2d4-130">Bu öğreticide kullanılan Azure kaynaklarını hello için bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-130">Create a resource group for hello Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="9e2d4-131">Bir özel Azure kapsayıcı kayıt defteri hello kaynak grubunda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-131">Create a private Azure container registry in hello resource group.</span></span> <span data-ttu-id="9e2d4-132">Başlangıç Öğreticisi hello örnek uygulaması Docker görüntü toothis kayıt defteri daha sonraki adımlarda olarak iter.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-132">hello tutorial pushes hello sample app as a Docker image toothis registry in later steps.</span></span> <span data-ttu-id="9e2d4-133">Değiştir `wingtiptoysregistry` kayıt için benzersiz bir ad ile.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-133">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-toohello-container-registry"></a><span data-ttu-id="9e2d4-134">Uygulama toohello kapsayıcı kaydınız bildirme</span><span class="sxs-lookup"><span data-stu-id="9e2d4-134">Push your app toohello container registry</span></span>

1. <span data-ttu-id="9e2d4-135">Maven yüklemenizi toohello yapılandırma dizinine gidin (varsayılan ~/.m2/ veya C:\Users\username\.m2) ve açık hello *settings.xml* dosyasını bir metin düzenleyicisiyle.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-135">Navigate toohello configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open hello *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="9e2d4-136">Kapsayıcı kaydınız Hello parolasını hello Azure CLI ' alın.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-136">Retrieve hello password for your container registry from hello Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="9e2d4-137">Azure kapsayıcı kayıt kimliği ve parolası tooa yeni Ekle `<server>` hello koleksiyonunda *settings.xml* dosya.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-137">Add your Azure Container Registry id and password tooa new `<server>` collection in hello *settings.xml* file.</span></span>
<span data-ttu-id="9e2d4-138">Merhaba `id` ve `username` hello kayıt defteri hello adı.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-138">hello `id` and `username` are hello name of hello registry.</span></span> <span data-ttu-id="9e2d4-139">Kullanım hello `password` değerinden (tırnaklar olmadan) hello önceki komutu.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-139">Use hello `password` value from hello previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="9e2d4-140">Yay önyükleme uygulamanız için tamamlandı toohello proje dizinine gidin (örneğin, "*C:\SpringBoot\gs-spring-boot-docker\complete*"veya"*/users/robert/SpringBoot/gs-spring-boot-docker / tam*") ve açık hello *pom.xml* dosyasını bir metin düzenleyicisiyle.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-140">Navigate toohello completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="9e2d4-141">Güncelleştirme hello `<properties>` hello koleksiyonunda *pom.xml* hello oturum açma sunucusu değeri bir dosyayla Azure kapsayıcı kayıt için.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-141">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="9e2d4-142">Güncelleştirme hello `<plugins>` hello koleksiyonunda *pom.xml* , hello şekilde dosya `<plugin>` hello oturum açma sunucusu adresi ve kayıt defteri adı için Azure kapsayıcı kayıt içerir.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-142">Update hello `<plugins>` collection in hello *pom.xml* file so that hello `<plugin>` contains hello login server address and registry name for your Azure Container Registry.</span></span>

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

1. <span data-ttu-id="9e2d4-143">Yay önyükleme uygulamanız için tamamlandı toohello proje dizinine gidin ve komut toobuild hello Docker kapsayıcısı ve anında iletme hello görüntü toohello kayıt defteri aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9e2d4-143">Navigate toohello completed project directory for your Spring Boot application and run hello following command toobuild hello Docker container and push hello image toohello registry:</span></span>

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  <span data-ttu-id="9e2d4-144">Maven hello görüntü tooAzure iter kurarken, benzer tooone hello aşağıdaki hata iletisini alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9e2d4-144">You may receive an error message that is similar tooone of hello following when Maven pushes hello image tooAzure:</span></span>
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="9e2d4-145">Bu hata alırsanız, hello Docker komut satırından tooAzure oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-145">If you get this error, log in tooAzure from hello Docker command line.</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="9e2d4-146">Ardından, kapsayıcı gönderin:</span><span class="sxs-lookup"><span data-stu-id="9e2d4-146">Then push your container:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-hello-azure-cli"></a><span data-ttu-id="9e2d4-147">Kubernetes küme üzerinde ACS hello Azure CLI kullanarak oluşturma</span><span class="sxs-lookup"><span data-stu-id="9e2d4-147">Create a Kubernetes Cluster on ACS using hello Azure CLI</span></span>

1. <span data-ttu-id="9e2d4-148">Azure kapsayıcı Hizmeti'nde bir Kubernetes kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-148">Create a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="9e2d4-149">Merhaba aşağıdaki komut oluşturur bir *kubernetes* hello kümede *wingtiptoys kubernetes* kaynak grubu ile *wingtiptoys containerservice* hello kümesi olarak ad ve *wingtiptoys kubernetes* hello DNS öneki olarak:</span><span class="sxs-lookup"><span data-stu-id="9e2d4-149">hello following command creates a *kubernetes* cluster in hello *wingtiptoys-kubernetes* resource group, with *wingtiptoys-containerservice* as hello cluster name, and *wingtiptoys-kubernetes* as hello DNS prefix:</span></span>
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   <span data-ttu-id="9e2d4-150">Bu komut zaman alabilir toocomplete.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-150">This command may take a while toocomplete.</span></span>

1. <span data-ttu-id="9e2d4-151">Yükleme `kubectl` hello Azure CLI kullanarak.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-151">Install `kubectl` using hello Azure CLI.</span></span> <span data-ttu-id="9e2d4-152">Linux kullanıcıları bu komutla tooprefix olabilir `sudo` hello Kubernetes CLI çok dağıtır beri`/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-152">Linux users may have tooprefix this command with `sudo` since it deploys hello Kubernetes CLI too`/usr/local/bin`.</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

1. <span data-ttu-id="9e2d4-153">Merhaba Kubernetes web arabiriminden kümenizi yönetebilirsiniz hello küme yapılandırma bilgilerini karşıdan yüklemek ve `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-153">Download hello cluster configuration information so you can manage your cluster from hello Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-hello-image-tooyour-kubernetes-cluster"></a><span data-ttu-id="9e2d4-154">Merhaba görüntü tooyour Kubernetes kümesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="9e2d4-154">Deploy hello image tooyour Kubernetes cluster</span></span>

<span data-ttu-id="9e2d4-155">Merhaba uygulamasını kullanarak bu öğreticinin dağıtır `kubectl`, ardından hello Kubernetes web arabirimi üzerinden tooexplore hello dağıtımına izin.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-155">This tutorial deploys hello app using `kubectl`, then allow you tooexplore hello deployment through hello Kubernetes web interface.</span></span>

### <a name="deploy-with-hello-kubernetes-web-interface"></a><span data-ttu-id="9e2d4-156">Merhaba Kubernetes web arabirimiyle dağıtma</span><span class="sxs-lookup"><span data-stu-id="9e2d4-156">Deploy with hello Kubernetes web interface</span></span>

1. <span data-ttu-id="9e2d4-157">Bir komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-157">Open a command prompt.</span></span>

1. <span data-ttu-id="9e2d4-158">Merhaba yapılandırma Web sitesi Kubernetes kümeniz için varsayılan tarayıcınızda açın:</span><span class="sxs-lookup"><span data-stu-id="9e2d4-158">Open hello configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. <span data-ttu-id="9e2d4-159">Merhaba Kubernetes yapılandırma Web tarayıcınızda oturum açtığında, hello çok bağlantısı**kapsayıcılı uygulamasını dağıtmak**:</span><span class="sxs-lookup"><span data-stu-id="9e2d4-159">When hello Kubernetes configuration website opens in your browser, click hello link too**deploy a containerized app**:</span></span>

   ![Kubernetes yapılandırma Web sitesi][KB01]

1. <span data-ttu-id="9e2d4-161">Ne zaman hello **kapsayıcılı uygulamasını dağıtmak** sayfası görüntülenirse, aşağıdaki seçenekleri şu hello belirtin:</span><span class="sxs-lookup"><span data-stu-id="9e2d4-161">When hello **Deploy a containerized app** page is displayed, specify hello following options:</span></span>

   <span data-ttu-id="9e2d4-162">a.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-162">a.</span></span> <span data-ttu-id="9e2d4-163">Seçin **aşağıda uygulama ayrıntılarını belirtin**.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-163">Select **Specify app details below**.</span></span>

   <span data-ttu-id="9e2d4-164">b.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-164">b.</span></span> <span data-ttu-id="9e2d4-165">Hello için yay önyükleme uygulama adınızı girin **uygulama adı**; örneğin: "*gs yay önyükleme docker*".</span><span class="sxs-lookup"><span data-stu-id="9e2d4-165">Enter your Spring Boot application name for hello **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="9e2d4-166">c.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-166">c.</span></span> <span data-ttu-id="9e2d4-167">Merhaba, oturum açma sunucusu ve kapsayıcı görüntüden daha önce girin **kapsayıcı görüntü**; örneğin: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span><span class="sxs-lookup"><span data-stu-id="9e2d4-167">Enter your login server and container image from earlier for hello **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="9e2d4-168">d.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-168">d.</span></span> <span data-ttu-id="9e2d4-169">Seçin **dış** hello için **hizmet**.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-169">Choose **External** for hello **Service**.</span></span>

   <span data-ttu-id="9e2d4-170">e.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-170">e.</span></span> <span data-ttu-id="9e2d4-171">İç ve dış bağlantı noktaları hello belirtin **bağlantı noktası** ve **hedef bağlantı noktası** metin kutuları.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-171">Specify your external and internal ports in hello **Port** and **Target port** text boxes.</span></span>

   ![Kubernetes yapılandırma Web sitesi][KB02]


1. <span data-ttu-id="9e2d4-173">Tıklatın **dağıtma** toodeploy hello kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-173">Click **Deploy** toodeploy hello container.</span></span>

   ![Kapsayıcı dağıtma][KB05]

1. <span data-ttu-id="9e2d4-175">Uygulamanız dağıtıldıktan sonra altında listelenen yay önyükleme uygulamanızı görürsünüz **Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-175">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Kubernetes Hizmetleri][KB06]

1. <span data-ttu-id="9e2d4-177">Merhaba bağlantısına tıklarsanız **dış uç noktalar**, Azure üzerinde çalışan yay önyükleme uygulamanızı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-177">If you click hello link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Kubernetes Hizmetleri][KB07]

   ![Azure ile ilgili örnek uygulaması Gözat][SB02]


### <a name="deploy-with-kubectl"></a><span data-ttu-id="9e2d4-180">Kubectl ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="9e2d4-180">Deploy with kubectl</span></span>

1. <span data-ttu-id="9e2d4-181">Bir komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-181">Open a command prompt.</span></span>

1. <span data-ttu-id="9e2d4-182">Hello kullanarak, kapsayıcı hello Kubernetes kümede çalışmasını `kubectl run` komutu.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-182">Run your container in hello Kubernetes cluster by using hello `kubectl run` command.</span></span> <span data-ttu-id="9e2d4-183">Bir hizmet adı uygulamanızı Kubernetes ve hello tam görüntü adı verin.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-183">Give a service name for your app in Kubernetes and hello full image name.</span></span> <span data-ttu-id="9e2d4-184">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="9e2d4-184">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="9e2d4-185">Bu komutta:</span><span class="sxs-lookup"><span data-stu-id="9e2d4-185">In this command:</span></span>

   * <span data-ttu-id="9e2d4-186">Merhaba kapsayıcı adı `gs-spring-boot-docker` hemen sonra hello belirtilen `run` komutu</span><span class="sxs-lookup"><span data-stu-id="9e2d4-186">hello container name `gs-spring-boot-docker` is specified immediately after hello `run` command</span></span>

   * <span data-ttu-id="9e2d4-187">Merhaba `--image` parametresi belirtir hello birleştirilmiş oturum açma sunucusu ve görüntü adı olarak`wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span><span class="sxs-lookup"><span data-stu-id="9e2d4-187">hello `--image` parameter specifies hello combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="9e2d4-188">Harici olarak hello kullanarak Kubernetes kümenizi kullanıma `kubectl expose` komutu.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-188">Expose your Kubernetes cluster externally by using hello `kubectl expose` command.</span></span> <span data-ttu-id="9e2d4-189">Genel kullanıma yönelik TCP bağlantı noktası kullanılan tooaccess hello uygulama ve uygulamanızı dinlediği hello iç hedef bağlantı noktası Merhaba, hizmet adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-189">Specify your service name, hello public-facing TCP port used tooaccess hello app, and hello internal target port your app listens on.</span></span> <span data-ttu-id="9e2d4-190">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="9e2d4-190">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="9e2d4-191">Bu komutta:</span><span class="sxs-lookup"><span data-stu-id="9e2d4-191">In this command:</span></span>

   * <span data-ttu-id="9e2d4-192">Merhaba kapsayıcı adı `gs-spring-boot-docker` hemen sonra hello belirtilen `expose deployment` komutu</span><span class="sxs-lookup"><span data-stu-id="9e2d4-192">hello container name `gs-spring-boot-docker` is specified immediately after hello `expose deployment` command</span></span>

   * <span data-ttu-id="9e2d4-193">Merhaba `--type` parametresi, o hello kümesi kullanan yük dengeleyici belirtir</span><span class="sxs-lookup"><span data-stu-id="9e2d4-193">hello `--type` parameter specifies that hello cluster uses load balancer</span></span>

   * <span data-ttu-id="9e2d4-194">Merhaba `--port` parametresi hello genel kullanıma yönelik TCP bağlantı noktası 80 belirtir.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-194">hello `--port` parameter specifies hello public-facing TCP port of 80.</span></span> <span data-ttu-id="9e2d4-195">Merhaba uygulamanın bu bağlantı noktasına erişim.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-195">You access hello app on this port.</span></span>

   * <span data-ttu-id="9e2d4-196">Merhaba `--target-port` parametresi hello iç TCP bağlantı noktası 8080 belirtir.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-196">hello `--target-port` parameter specifies hello internal TCP port of 8080.</span></span> <span data-ttu-id="9e2d4-197">Merhaba yük dengeleyici, bu bağlantı noktasında istekleri tooyour uygulama iletir.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-197">hello load balancer forwards requests tooyour app on this port.</span></span>

1. <span data-ttu-id="9e2d4-198">Merhaba uygulama dağıtıldıktan sonra toohello küme hello dış IP adresi sorgulamak ve web tarayıcınızda açın:</span><span class="sxs-lookup"><span data-stu-id="9e2d4-198">Once hello app is deployed toohello cluster, query hello external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Azure ile ilgili örnek uygulaması Gözat][SB02]


## <a name="next-steps"></a><span data-ttu-id="9e2d4-200">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9e2d4-200">Next steps</span></span>

<span data-ttu-id="9e2d4-201">Azure üzerinde yay önyükleme kullanma hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="9e2d4-201">For more information about using Spring Boot on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="9e2d4-202">Yay önyükleme uygulama toohello Azure App Service'e dağıtma</span><span class="sxs-lookup"><span data-stu-id="9e2d4-202">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="9e2d4-203">Linux'ta hello Azure kapsayıcı hizmeti bir yay önyükleme uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="9e2d4-203">Deploy a Spring Boot application on Linux in hello Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-linux.md)

<span data-ttu-id="9e2d4-204">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi] ve hello [Visual Studio Team Services için Java Araçları].</span><span class="sxs-lookup"><span data-stu-id="9e2d4-204">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="9e2d4-205">Docker örnek proje hello yay önyükleme hakkında daha fazla bilgi için bkz: [Docker Başlarken yay önyüklemede].</span><span class="sxs-lookup"><span data-stu-id="9e2d4-205">For more information about hello Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="9e2d4-206">Aşağıdaki bağlantılar hello yay önyükleme uygulamaları oluşturma hakkında ek bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="9e2d4-206">hello following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="9e2d4-207">Basit bir yay önyükleme uygulama oluşturma hakkında daha fazla bilgi için hello yay Initializr https://start.spring.io/ adresindeki bakın.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-207">For more information about creating a simple Spring Boot application, see hello Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="9e2d4-208">Merhaba aşağıdaki bağlantılar Kubernetes Azure ile kullanma hakkında ek bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="9e2d4-208">hello following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="9e2d4-209">Kapsayıcı hizmeti Kubernetes kümede kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="9e2d4-209">Get started with a Kubernetes cluster in Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [<span data-ttu-id="9e2d4-210">Kubernetes web kullanıcı Arabirimi Azure kapsayıcı hizmeti ile Merhaba kullanma</span><span class="sxs-lookup"><span data-stu-id="9e2d4-210">Using hello Kubernetes web UI with Azure Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

<span data-ttu-id="9e2d4-211">Kubernetes komut satırı arabirimini kullanma hakkında daha fazla bilgi hello kullanılabilir **kubectl** adresindeki Kullanıcı Kılavuzu'na <https://kubernetes.io/docs/user-guide/kubectl/>.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-211">More information about using Kubernetes command-line interface is available in hello **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="9e2d4-212">Merhaba Kubernetes Web sitesi özel kayıt defterleri görüntüleri görüşmeniz çeşitli makaleler vardır:</span><span class="sxs-lookup"><span data-stu-id="9e2d4-212">hello Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="9e2d4-213">[Hizmet yapılandırma pod'ları için hesapları]</span><span class="sxs-lookup"><span data-stu-id="9e2d4-213">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="9e2d4-214">[Ad alanları]</span><span class="sxs-lookup"><span data-stu-id="9e2d4-214">[Namespaces]</span></span>
* <span data-ttu-id="9e2d4-215">[Özel bir kayıt defterinden görüntüyü çekme]</span><span class="sxs-lookup"><span data-stu-id="9e2d4-215">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="9e2d4-216">Toouse özel Docker Azure ile nasıl görüntüler için ek örnekler için bkz: [Linux Azure Web uygulaması için özel bir Docker görüntü kullanarak].</span><span class="sxs-lookup"><span data-stu-id="9e2d4-216">For additional examples for how toouse custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Azure komut satırı arabirimi (CLI)]: /cli/azure/overview
[Azure kapsayıcı Hizmeti'ni (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Linux Azure Web uygulaması için özel bir Docker görüntü kullanarak]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[ücretsiz Azure hesabı]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Geliştirme Seti (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Visual Studio Team Services için Java Araçları]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[MSDN abone Avantajlarınızı]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[yay önyükleme]: http://projects.spring.io/spring-boot/
[Docker Başlarken yay önyüklemede]: https://github.com/spring-guides/gs-spring-boot-docker
[yay Framework]: https://spring.io/
[Hizmet yapılandırma pod'ları için hesapları]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
[Ad alanları]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[Özel bir kayıt defterinden görüntüyü çekme]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR04.png

[KB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB01.png
[KB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB02.png
[KB03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB03.png
[KB04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB04.png
[KB05]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB05.png
[KB06]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB06.png
[KB07]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB07.png
