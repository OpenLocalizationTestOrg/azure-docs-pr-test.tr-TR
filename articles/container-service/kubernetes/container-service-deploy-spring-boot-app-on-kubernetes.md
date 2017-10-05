---
title: "Azure kapsayıcı Hizmeti'nde Kubernetes bir yay önyükleme uygulamasını dağıtma | Microsoft Docs"
description: "Bu öğreticide, Microsoft Azure üzerinde bir Kubernetes yay önyükleme uygulamada dağıtma adımları küme olsa size yol gösterir."
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
ms.openlocfilehash: 7f726436b2d459b8c16abb02e07de099abfd8974
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-container-service"></a><span data-ttu-id="c0d80-103">Azure Container Service’te bir Kubernetes Kümesi üzerinde Spring Boot Uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="c0d80-103">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>

<span data-ttu-id="c0d80-104"> **[Yay Framework]**  , Java geliştiricilerinin web, mobil ve API uygulamaları oluşturma yardımcı olan bir popüler açık kaynak çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="c0d80-104">The **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="c0d80-105">Bu öğretici kullanılarak oluşturulmuş bir örnek uygulama kullanır [yay önyükleme], kuralı güdümlü bir yaklaşım yay hızlıca başlamak için kullanma.</span><span class="sxs-lookup"><span data-stu-id="c0d80-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring to get started quickly.</span></span>

<span data-ttu-id="c0d80-106">**[Kubernetes]**  ve  **[Docker]**  olan, geliştiricilerin açık kaynak çözümleri otomatikleştirmek dağıtım, ölçeklendirme ve çalışan kendi uygulamalarını Yönetimi kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="c0d80-106">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate the deployment, scaling, and management of their applications  running in containers.</span></span>

<span data-ttu-id="c0d80-107">Bu öğreticide, geliştirmek ve Microsoft Azure yay önyükleme uygulama dağıtmak için bu iki yaygın olarak kullanılan, açık kaynaklı teknolojiler birleştirme olsa açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c0d80-107">This tutorial walks you though combining these two popular, open-source technologies to develop and deploy a Spring Boot application to Microsoft Azure.</span></span> <span data-ttu-id="c0d80-108">Daha belirgin olarak kullandığınız  *[yay önyükleme]*  uygulama geliştirme için  *[Kubernetes]*  kapsayıcı dağıtım ve [ Azure kapsayıcı Hizmeti'ni (ACS)] uygulamanızı barındırmak için.</span><span class="sxs-lookup"><span data-stu-id="c0d80-108">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and the [Azure Container Service (ACS)] to host your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c0d80-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c0d80-109">Prerequisites</span></span>

* <span data-ttu-id="c0d80-110">Bir Azure aboneliği; bir Azure aboneliği zaten sahip değilseniz, etkinleştirebilir, [MSDN abone Avantajlarınızı] veya kaydolun bir [ücretsiz Azure hesabı].</span><span class="sxs-lookup"><span data-stu-id="c0d80-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="c0d80-111">[Azure komut satırı arabirimi (CLI)].</span><span class="sxs-lookup"><span data-stu-id="c0d80-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="c0d80-112">Güncel bir [Java Geliştirme Seti (JDK)].</span><span class="sxs-lookup"><span data-stu-id="c0d80-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="c0d80-113">Apache'nın [Maven] aracını (sürüm 3) yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="c0d80-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="c0d80-114">A [Git] istemci.</span><span class="sxs-lookup"><span data-stu-id="c0d80-114">A [Git] client.</span></span>
* <span data-ttu-id="c0d80-115">A [Docker] istemci.</span><span class="sxs-lookup"><span data-stu-id="c0d80-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="c0d80-116">Bu öğretici sanallaştırma gereksinimleri nedeniyle, bir sanal makinede bu makaledeki adımları izleyin olamaz; sanallaştırma özellikleri etkin bir fiziksel bilgisayar kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0d80-116">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="c0d80-117">Yay önyükleme Docker Başlarken web uygulaması oluştur</span><span class="sxs-lookup"><span data-stu-id="c0d80-117">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="c0d80-118">Aşağıdaki adımlar yay önyükleme web uygulaması oluşturma ve yerel olarak test size yol.</span><span class="sxs-lookup"><span data-stu-id="c0d80-118">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="c0d80-119">Bir komut istemi açın ve uygulamanızı tutun ve bu dizine değiştirmek için yerel bir dizin oluşturun; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="c0d80-119">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="c0d80-120">--ya da--</span><span class="sxs-lookup"><span data-stu-id="c0d80-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="c0d80-121">Kopya [Docker Başlarken yay önyüklemede] örnek proje dizine.</span><span class="sxs-lookup"><span data-stu-id="c0d80-121">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="c0d80-122">Projeyi Dizin Değiştir.</span><span class="sxs-lookup"><span data-stu-id="c0d80-122">Change directory to the completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="c0d80-123">Derleme ve örnek uygulamayı çalıştırma için Maven kullanın.</span><span class="sxs-lookup"><span data-stu-id="c0d80-123">Use Maven to build and run the sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="c0d80-124">Web uygulaması http://localhost: 8080 veya aşağıdaki göz atarak test `curl` komutu:</span><span class="sxs-lookup"><span data-stu-id="c0d80-124">Test the web app by browsing to http://localhost:8080, or with the following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="c0d80-125">Aşağıdaki ileti görürsünüz: **Hello Docker World**</span><span class="sxs-lookup"><span data-stu-id="c0d80-125">You should see the following message displayed: **Hello Docker World**</span></span>

   ![Örnek uygulamayı yerel olarak göz atın][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="c0d80-127">Azure CLI kullanarak bir Azure kapsayıcı kayıt defteri oluşturma</span><span class="sxs-lookup"><span data-stu-id="c0d80-127">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="c0d80-128">Bir komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="c0d80-128">Open a command prompt.</span></span>

1. <span data-ttu-id="c0d80-129">Azure hesabınızda oturum açın:</span><span class="sxs-lookup"><span data-stu-id="c0d80-129">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="c0d80-130">Bu öğreticide kullanılan Azure kaynakları için bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c0d80-130">Create a resource group for the Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="c0d80-131">Bir özel Azure kapsayıcı kayıt defteri kaynak grubunu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c0d80-131">Create a private Azure container registry in the resource group.</span></span> <span data-ttu-id="c0d80-132">Öğreticinin daha sonraki adımlarda bu kayıt defteri için Docker görüntüsü olarak örnek uygulaması iter.</span><span class="sxs-lookup"><span data-stu-id="c0d80-132">The tutorial pushes the sample app as a Docker image to this registry in later steps.</span></span> <span data-ttu-id="c0d80-133">Değiştir `wingtiptoysregistry` kayıt için benzersiz bir ad ile.</span><span class="sxs-lookup"><span data-stu-id="c0d80-133">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry"></a><span data-ttu-id="c0d80-134">Uygulamanız için kapsayıcı kayıt itme</span><span class="sxs-lookup"><span data-stu-id="c0d80-134">Push your app to the container registry</span></span>

1. <span data-ttu-id="c0d80-135">Maven yüklemeniz için yapılandırma dizinine gidin (varsayılan ~/.m2/ veya C:\Users\username\.m2) ve açık *settings.xml* dosyasını bir metin düzenleyicisiyle.</span><span class="sxs-lookup"><span data-stu-id="c0d80-135">Navigate to the configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="c0d80-136">Kapsayıcı kaydınız parolasını Azure CLI üzerinden alır.</span><span class="sxs-lookup"><span data-stu-id="c0d80-136">Retrieve the password for your container registry from the Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="c0d80-137">Azure kapsayıcı kayıt defteri kimliğinizi ve parolanızı yeni bir ekleme `<server>` koleksiyonunda *settings.xml* dosya.</span><span class="sxs-lookup"><span data-stu-id="c0d80-137">Add your Azure Container Registry id and password to a new `<server>` collection in the *settings.xml* file.</span></span>
<span data-ttu-id="c0d80-138">`id` Ve `username` kayıt adı.</span><span class="sxs-lookup"><span data-stu-id="c0d80-138">The `id` and `username` are the name of the registry.</span></span> <span data-ttu-id="c0d80-139">Kullanım `password` değerinden (tırnaklar olmadan) önceki komutu.</span><span class="sxs-lookup"><span data-stu-id="c0d80-139">Use the `password` value from the previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="c0d80-140">Yay önyükleme uygulamanız için projeyi dizinine gidin (örneğin, "*C:\SpringBoot\gs-spring-boot-docker\complete*"veya"*/users/robert/SpringBoot/gs-spring-boot-docker/complete* ") ve açın *pom.xml* dosyasını bir metin düzenleyicisiyle.</span><span class="sxs-lookup"><span data-stu-id="c0d80-140">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="c0d80-141">Güncelleştirme `<properties>` koleksiyonunda *pom.xml* Azure kapsayıcı kayıt için oturum açma sunucusu değerle dosyası.</span><span class="sxs-lookup"><span data-stu-id="c0d80-141">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="c0d80-142">Güncelleştirme `<plugins>` koleksiyonunda *pom.xml* dosya böylece `<plugin>` Azure kapsayıcı kayıt için oturum açma sunucusu adresi ve kayıt defteri adını içerir.</span><span class="sxs-lookup"><span data-stu-id="c0d80-142">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry.</span></span>

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

1. <span data-ttu-id="c0d80-143">Yay önyükleme uygulamanız için projeyi dizinine gidin ve Docker kapsayıcısı oluşturmak ve kayıt defterine görüntü gönderme için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c0d80-143">Navigate to the completed project directory for your Spring Boot application and run the following command to build the Docker container and push the image to the registry:</span></span>

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  <span data-ttu-id="c0d80-144">Maven görüntü Azure'a iter, aşağıdakilerden birini benzer bir hata iletisini alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c0d80-144">You may receive an error message that is similar to one of the following when Maven pushes the image to Azure:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="c0d80-145">Bu hata alırsanız, Azure için Docker komut satırından oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c0d80-145">If you get this error, log in to Azure from the Docker command line.</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="c0d80-146">Ardından, kapsayıcı gönderin:</span><span class="sxs-lookup"><span data-stu-id="c0d80-146">Then push your container:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-the-azure-cli"></a><span data-ttu-id="c0d80-147">Üzerinde Azure CLI kullanarak ACS Kubernetes küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="c0d80-147">Create a Kubernetes Cluster on ACS using the Azure CLI</span></span>

1. <span data-ttu-id="c0d80-148">Azure kapsayıcı Hizmeti'nde bir Kubernetes kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c0d80-148">Create a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="c0d80-149">Aşağıdaki komut oluşturur bir *kubernetes* kümesi *wingtiptoys kubernetes* kaynak grubu ile *wingtiptoys containerservice* küme adı olarak ve *wingtiptoys kubernetes* DNS öneki:</span><span class="sxs-lookup"><span data-stu-id="c0d80-149">The following command creates a *kubernetes* cluster in the *wingtiptoys-kubernetes* resource group, with *wingtiptoys-containerservice* as the cluster name, and *wingtiptoys-kubernetes* as the DNS prefix:</span></span>
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   <span data-ttu-id="c0d80-150">Bu komutun tamamlanması biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="c0d80-150">This command may take a while to complete.</span></span>

1. <span data-ttu-id="c0d80-151">Yükleme `kubectl` Azure CLI kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c0d80-151">Install `kubectl` using the Azure CLI.</span></span> <span data-ttu-id="c0d80-152">Linux kullanıcıları bu komutla önek gerekebilir `sudo` Kubernetes CLI dağıtır beri `/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="c0d80-152">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

1. <span data-ttu-id="c0d80-153">Kubernetes web arabiriminden kümenizi yönetebilirsiniz küme yapılandırma bilgilerini karşıdan yüklemek ve `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="c0d80-153">Download the cluster configuration information so you can manage your cluster from the Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a><span data-ttu-id="c0d80-154">Yansıma Kubernetes kümeye dağıtma</span><span class="sxs-lookup"><span data-stu-id="c0d80-154">Deploy the image to your Kubernetes cluster</span></span>

<span data-ttu-id="c0d80-155">Uygulamasını kullanarak bu öğreticinin dağıtır `kubectl`, Kubernetes web arabirimi aracılığıyla keşfetmeniz için izin.</span><span class="sxs-lookup"><span data-stu-id="c0d80-155">This tutorial deploys the app using `kubectl`, then allow you to explore the deployment through the Kubernetes web interface.</span></span>

### <a name="deploy-with-the-kubernetes-web-interface"></a><span data-ttu-id="c0d80-156">Kubernetes web arabirimiyle dağıtma</span><span class="sxs-lookup"><span data-stu-id="c0d80-156">Deploy with the Kubernetes web interface</span></span>

1. <span data-ttu-id="c0d80-157">Bir komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="c0d80-157">Open a command prompt.</span></span>

1. <span data-ttu-id="c0d80-158">Yapılandırma Web sitesi Kubernetes kümeniz için varsayılan tarayıcınızda açın:</span><span class="sxs-lookup"><span data-stu-id="c0d80-158">Open the configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. <span data-ttu-id="c0d80-159">Kubernetes yapılandırma Web tarayıcınızda oturum açtığında, bağlantısını tıklatın **kapsayıcılı uygulamasını dağıtmak**:</span><span class="sxs-lookup"><span data-stu-id="c0d80-159">When the Kubernetes configuration website opens in your browser, click the link to **deploy a containerized app**:</span></span>

   ![Kubernetes yapılandırma Web sitesi][KB01]

1. <span data-ttu-id="c0d80-161">Zaman **kapsayıcılı uygulamasını dağıtmak** sayfası görüntülenirse, aşağıdaki seçenekleri belirtin:</span><span class="sxs-lookup"><span data-stu-id="c0d80-161">When the **Deploy a containerized app** page is displayed, specify the following options:</span></span>

   <span data-ttu-id="c0d80-162">a.</span><span class="sxs-lookup"><span data-stu-id="c0d80-162">a.</span></span> <span data-ttu-id="c0d80-163">Seçin **aşağıda uygulama ayrıntılarını belirtin**.</span><span class="sxs-lookup"><span data-stu-id="c0d80-163">Select **Specify app details below**.</span></span>

   <span data-ttu-id="c0d80-164">b.</span><span class="sxs-lookup"><span data-stu-id="c0d80-164">b.</span></span> <span data-ttu-id="c0d80-165">Yay önyükleme uygulama adınızı girin **uygulama adı**; örneğin: "*gs yay önyükleme docker*".</span><span class="sxs-lookup"><span data-stu-id="c0d80-165">Enter your Spring Boot application name for the **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="c0d80-166">c.</span><span class="sxs-lookup"><span data-stu-id="c0d80-166">c.</span></span> <span data-ttu-id="c0d80-167">Oturum açma sunucusu ve kapsayıcı görüntünüze için daha önce girin **kapsayıcı görüntü**; örneğin: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span><span class="sxs-lookup"><span data-stu-id="c0d80-167">Enter your login server and container image from earlier for the **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="c0d80-168">d.</span><span class="sxs-lookup"><span data-stu-id="c0d80-168">d.</span></span> <span data-ttu-id="c0d80-169">Seçin **dış** için **hizmet**.</span><span class="sxs-lookup"><span data-stu-id="c0d80-169">Choose **External** for the **Service**.</span></span>

   <span data-ttu-id="c0d80-170">e.</span><span class="sxs-lookup"><span data-stu-id="c0d80-170">e.</span></span> <span data-ttu-id="c0d80-171">İç ve dış bağlantı noktaları belirtin **bağlantı noktası** ve **hedef bağlantı noktası** metin kutuları.</span><span class="sxs-lookup"><span data-stu-id="c0d80-171">Specify your external and internal ports in the **Port** and **Target port** text boxes.</span></span>

   ![Kubernetes yapılandırma Web sitesi][KB02]


1. <span data-ttu-id="c0d80-173">Tıklatın **dağıtma** kapsayıcıyı dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="c0d80-173">Click **Deploy** to deploy the container.</span></span>

   ![Kapsayıcı dağıtma][KB05]

1. <span data-ttu-id="c0d80-175">Uygulamanız dağıtıldıktan sonra altında listelenen yay önyükleme uygulamanızı görürsünüz **Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="c0d80-175">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Kubernetes Hizmetleri][KB06]

1. <span data-ttu-id="c0d80-177">Bağlantısına tıklarsanız **dış uç noktalar**, Azure üzerinde çalışan yay önyükleme uygulamanızı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0d80-177">If you click the link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Kubernetes Hizmetleri][KB07]

   ![Azure ile ilgili örnek uygulaması Gözat][SB02]


### <a name="deploy-with-kubectl"></a><span data-ttu-id="c0d80-180">Kubectl ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="c0d80-180">Deploy with kubectl</span></span>

1. <span data-ttu-id="c0d80-181">Bir komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="c0d80-181">Open a command prompt.</span></span>

1. <span data-ttu-id="c0d80-182">Kullanarak, kapsayıcı Kubernetes kümede çalışmasını `kubectl run` komutu.</span><span class="sxs-lookup"><span data-stu-id="c0d80-182">Run your container in the Kubernetes cluster by using the `kubectl run` command.</span></span> <span data-ttu-id="c0d80-183">Uygulamanızı Kubernetes için hizmet adı ve tam görüntü adı verin.</span><span class="sxs-lookup"><span data-stu-id="c0d80-183">Give a service name for your app in Kubernetes and the full image name.</span></span> <span data-ttu-id="c0d80-184">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="c0d80-184">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="c0d80-185">Bu komutta:</span><span class="sxs-lookup"><span data-stu-id="c0d80-185">In this command:</span></span>

   * <span data-ttu-id="c0d80-186">Kapsayıcı adı `gs-spring-boot-docker` hemen sonra belirtilen `run` komutu</span><span class="sxs-lookup"><span data-stu-id="c0d80-186">The container name `gs-spring-boot-docker` is specified immediately after the `run` command</span></span>

   * <span data-ttu-id="c0d80-187">`--image` Parametresi, birleştirilmiş oturum açma sunucusu ve görüntü adı olarak belirtir`wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span><span class="sxs-lookup"><span data-stu-id="c0d80-187">The `--image` parameter specifies the combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="c0d80-188">Harici olarak kullanarak Kubernetes kümenizi kullanıma `kubectl expose` komutu.</span><span class="sxs-lookup"><span data-stu-id="c0d80-188">Expose your Kubernetes cluster externally by using the `kubectl expose` command.</span></span> <span data-ttu-id="c0d80-189">Hizmet adı, uygulamaya erişmek için kullanılan genel kullanıma yönelik TCP bağlantı noktası ve uygulamanızı dinlediği iç hedef bağlantı noktası belirtin.</span><span class="sxs-lookup"><span data-stu-id="c0d80-189">Specify your service name, the public-facing TCP port used to access the app, and the internal target port your app listens on.</span></span> <span data-ttu-id="c0d80-190">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="c0d80-190">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="c0d80-191">Bu komutta:</span><span class="sxs-lookup"><span data-stu-id="c0d80-191">In this command:</span></span>

   * <span data-ttu-id="c0d80-192">Kapsayıcı adı `gs-spring-boot-docker` hemen sonra belirtilen `expose deployment` komutu</span><span class="sxs-lookup"><span data-stu-id="c0d80-192">The container name `gs-spring-boot-docker` is specified immediately after the `expose deployment` command</span></span>

   * <span data-ttu-id="c0d80-193">`--type` Parametresi, kümenin yük dengeleyici kullandığını belirtir</span><span class="sxs-lookup"><span data-stu-id="c0d80-193">The `--type` parameter specifies that the cluster uses load balancer</span></span>

   * <span data-ttu-id="c0d80-194">`--port` Parametresi, genel kullanıma yönelik TCP bağlantı noktası 80 belirtir.</span><span class="sxs-lookup"><span data-stu-id="c0d80-194">The `--port` parameter specifies the public-facing TCP port of 80.</span></span> <span data-ttu-id="c0d80-195">Uygulamanın bu bağlantı noktasına erişim.</span><span class="sxs-lookup"><span data-stu-id="c0d80-195">You access the app on this port.</span></span>

   * <span data-ttu-id="c0d80-196">`--target-port` Parametresi, 8080 iç TCP bağlantı noktasını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c0d80-196">The `--target-port` parameter specifies the internal TCP port of 8080.</span></span> <span data-ttu-id="c0d80-197">Yük Dengeleyici, bu bağlantı noktasında uygulamanıza isteklerini iletir.</span><span class="sxs-lookup"><span data-stu-id="c0d80-197">The load balancer forwards requests to your app on this port.</span></span>

1. <span data-ttu-id="c0d80-198">Kümeye uygulama dağıtıldığında, dış IP adresine sorgulamak ve web tarayıcınızda açın:</span><span class="sxs-lookup"><span data-stu-id="c0d80-198">Once the app is deployed to the cluster, query the external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Azure ile ilgili örnek uygulaması Gözat][SB02]


## <a name="next-steps"></a><span data-ttu-id="c0d80-200">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c0d80-200">Next steps</span></span>

<span data-ttu-id="c0d80-201">Azure üzerinde yay önyükleme kullanma hakkında daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="c0d80-201">For more information about using Spring Boot on Azure, see the following articles:</span></span>

* [<span data-ttu-id="c0d80-202">Yay önyükleme uygulamasını Azure App Service'e dağıtma</span><span class="sxs-lookup"><span data-stu-id="c0d80-202">Deploy a Spring Boot Application to the Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="c0d80-203">Azure kapsayıcı Hizmeti'nde Linux'ta yay önyükleme uygulamasını dağıtma</span><span class="sxs-lookup"><span data-stu-id="c0d80-203">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-linux.md)

<span data-ttu-id="c0d80-204">Azure’u Java ile kullanma hakkında daha fazla bilgi edinmek için bkz. [Azure Java Geliştirici Merkezi] ve [Visual Studio Team Services için Java Araçları].</span><span class="sxs-lookup"><span data-stu-id="c0d80-204">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="c0d80-205">Docker örnek proje yay önyükleme hakkında daha fazla bilgi için bkz: [Docker Başlarken yay önyüklemede].</span><span class="sxs-lookup"><span data-stu-id="c0d80-205">For more information about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="c0d80-206">Aşağıdaki bağlantılar yay önyükleme uygulamaları oluşturma hakkında ek bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="c0d80-206">The following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="c0d80-207">Basit bir yay önyükleme uygulama oluşturma hakkında daha fazla bilgi için https://start.spring.io/ adresindeki yay Initializr bakın.</span><span class="sxs-lookup"><span data-stu-id="c0d80-207">For more information about creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="c0d80-208">Aşağıdaki bağlantılar Kubernetes Azure ile kullanma hakkında ek bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="c0d80-208">The following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="c0d80-209">Kapsayıcı hizmeti Kubernetes kümede kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="c0d80-209">Get started with a Kubernetes cluster in Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [<span data-ttu-id="c0d80-210">Azure kapsayıcı hizmeti ile Kubernetes web kullanıcı arabirimini kullanma</span><span class="sxs-lookup"><span data-stu-id="c0d80-210">Using the Kubernetes web UI with Azure Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

<span data-ttu-id="c0d80-211">Kubernetes komut satırı arabirimini kullanma hakkında daha fazla bilgi bulunur **kubectl** adresindeki Kullanıcı Kılavuzu'na <https://kubernetes.io/docs/user-guide/kubectl/>.</span><span class="sxs-lookup"><span data-stu-id="c0d80-211">More information about using Kubernetes command-line interface is available in the **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="c0d80-212">Kubernetes Web sitesi özel kayıt defterleri görüntüleri görüşmeniz çeşitli makaleler vardır:</span><span class="sxs-lookup"><span data-stu-id="c0d80-212">The Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="c0d80-213">[Hizmet yapılandırma pod'ları için hesapları]</span><span class="sxs-lookup"><span data-stu-id="c0d80-213">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="c0d80-214">[Ad alanları]</span><span class="sxs-lookup"><span data-stu-id="c0d80-214">[Namespaces]</span></span>
* <span data-ttu-id="c0d80-215">[Özel bir kayıt defterinden görüntüyü çekme]</span><span class="sxs-lookup"><span data-stu-id="c0d80-215">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="c0d80-216">Azure ile özel Docker görüntülerinizi kullanımı için ek örnekler için bkz: [Linux Azure Web uygulaması için özel bir Docker görüntü kullanarak].</span><span class="sxs-lookup"><span data-stu-id="c0d80-216">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

<span data-ttu-id="c0d80-217">[Azure komut satırı arabirimi (CLI)]: /cli/azure/overview</span><span class="sxs-lookup"><span data-stu-id="c0d80-217">[Azure Command-Line Interface (CLI)]: /cli/azure/overview</span></span>
<span data-ttu-id="c0d80-218">[ Azure kapsayıcı Hizmeti'ni (ACS)]: https://azure.microsoft.com/services/container-service/</span><span class="sxs-lookup"><span data-stu-id="c0d80-218">[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/</span></span>
<span data-ttu-id="c0d80-219">[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="c0d80-219">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
<span data-ttu-id="c0d80-220">[Linux Azure Web uygulaması için özel bir Docker görüntü kullanarak]: /azure/app-service-web/app-service-linux-using-custom-docker-image</span><span class="sxs-lookup"><span data-stu-id="c0d80-220">[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image</span></span>
<span data-ttu-id="c0d80-221">[Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="c0d80-221">[Docker]: https://www.docker.com/</span></span>
<span data-ttu-id="c0d80-222">[ücretsiz Azure hesabı]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="c0d80-222">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="c0d80-223">[Git]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="c0d80-223">[Git]: https://github.com/</span></span>
<span data-ttu-id="c0d80-224">[Java Geliştirme Seti (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span><span class="sxs-lookup"><span data-stu-id="c0d80-224">[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span></span>
<span data-ttu-id="c0d80-225">[Visual Studio Team Services için Java Araçları]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="c0d80-225">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>
<span data-ttu-id="c0d80-226">[Kubernetes]: https://kubernetes.io/</span><span class="sxs-lookup"><span data-stu-id="c0d80-226">[Kubernetes]: https://kubernetes.io/</span></span>
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
<span data-ttu-id="c0d80-227">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="c0d80-227">[Maven]: http://maven.apache.org/</span></span>
<span data-ttu-id="c0d80-228">[MSDN abone Avantajlarınızı]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="c0d80-228">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
<span data-ttu-id="c0d80-229">[yay önyükleme]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="c0d80-229">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="c0d80-230">[Docker Başlarken yay önyüklemede]: https://github.com/spring-guides/gs-spring-boot-docker</span><span class="sxs-lookup"><span data-stu-id="c0d80-230">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker</span></span>
<span data-ttu-id="c0d80-231">[Yay Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="c0d80-231">[Spring Framework]: https://spring.io/</span></span>
<span data-ttu-id="c0d80-232">[Hizmet yapılandırma pod'ları için hesapları]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/</span><span class="sxs-lookup"><span data-stu-id="c0d80-232">[Configuring Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/</span></span>
<span data-ttu-id="c0d80-233">[Ad alanları]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/</span><span class="sxs-lookup"><span data-stu-id="c0d80-233">[Namespaces]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/</span></span>
<span data-ttu-id="c0d80-234">[Özel bir kayıt defterinden görüntüyü çekme]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/</span><span class="sxs-lookup"><span data-stu-id="c0d80-234">[Pulling an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/</span></span>

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
