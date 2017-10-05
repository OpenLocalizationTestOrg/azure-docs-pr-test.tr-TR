---
title: "Azure Service Fabric Linux Java uygulamanızda Jenkins aracılığıyla sürekli derleme ve tümleştirme | Microsoft Docs"
description: "Azure Service Fabric Linux Java uygulamanızda Jenkins aracılığıyla sürekli derleme ve tümleştirme"
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: saysa
ms.openlocfilehash: d9372407540d903acca5b1639a2d9ceb0bf3c571
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-jenkins-to-build-and-deploy-your-linux-java-application"></a><span data-ttu-id="28327-103">Jenkins kullanarak Linux java uygulamanızı derleme ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="28327-103">Use Jenkins to build and deploy your Linux Java application</span></span>
<span data-ttu-id="28327-104">Jenkins, uygulamanızın sürekli tümleştirme ve dağıtımı için yaygın olarak kullanılan bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="28327-104">Jenkins is a popular tool for continuous integration and deployment of your apps.</span></span> <span data-ttu-id="28327-105">Jenkins kullanarak Azure Service Fabric uygulamanızı derleme ve dağıtma işlemi aşağıda açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="28327-105">Here's how to build and deploy your Azure Service Fabric application by using Jenkins.</span></span>

## <a name="general-prerequisites"></a><span data-ttu-id="28327-106">Genel önkoşullar</span><span class="sxs-lookup"><span data-stu-id="28327-106">General prerequisites</span></span>
- <span data-ttu-id="28327-107">Git’i yerel olarak yükleyin.</span><span class="sxs-lookup"><span data-stu-id="28327-107">Have Git installed locally.</span></span> <span data-ttu-id="28327-108">İşletim sisteminize uygun Git sürümünü, [Git indirme sayfasından](https://git-scm.com/downloads) yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28327-108">You can install the appropriate Git version from [the Git downloads page](https://git-scm.com/downloads), based on your operating system.</span></span> <span data-ttu-id="28327-109">Yeni bir Git kullanıcısıysanız, daha fazla bilgi almak için [Git belgelerine](https://git-scm.com/docs) bakın.</span><span class="sxs-lookup"><span data-stu-id="28327-109">If you are new to Git, learn more about it from the [Git documentation](https://git-scm.com/docs).</span></span>
- <span data-ttu-id="28327-110">Service Fabric için kullanışlı Jenkins eklentisini edinin.</span><span class="sxs-lookup"><span data-stu-id="28327-110">Have the Service Fabric Jenkins plug-in handy.</span></span> <span data-ttu-id="28327-111">Eklentiyi [Service Fabric indirmeleri](https://servicefabricdownloads.blob.core.windows.net/jenkins/serviceFabric.hpi) sayfasından indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28327-111">You can download it from [Service Fabric downloads](https://servicefabricdownloads.blob.core.windows.net/jenkins/serviceFabric.hpi).</span></span>

## <a name="set-up-jenkins-inside-a-service-fabric-cluster"></a><span data-ttu-id="28327-112">Jenkins’i bir Service Fabric kümesi içinde ayarlama</span><span class="sxs-lookup"><span data-stu-id="28327-112">Set up Jenkins inside a Service Fabric cluster</span></span>

<span data-ttu-id="28327-113">Jenkins’i bir Service Fabric kümesinin içinde veya dışında ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28327-113">You can set up Jenkins either inside or outside a Service Fabric cluster.</span></span> <span data-ttu-id="28327-114">Aşağıdaki bölümlerde, bir küme içinde kapsayıcı örneğinin durumunu kaydetmek için Azure storage hesabı kullanırken nasıl ayarlanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="28327-114">The following sections show how to set it up inside a cluster while using an Azure storage account to save the state of the container instance.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="28327-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="28327-115">Prerequisites</span></span>
1. <span data-ttu-id="28327-116">Bir Service Fabric Linux kümesini hazır bulundurun.</span><span class="sxs-lookup"><span data-stu-id="28327-116">Have a Service Fabric Linux cluster ready.</span></span> <span data-ttu-id="28327-117">Azure portalından oluşturulmuş bir Service Fabric kümesinde Docker zaten yüklüdür.</span><span class="sxs-lookup"><span data-stu-id="28327-117">A Service Fabric cluster created from the Azure portal already has Docker installed.</span></span> <span data-ttu-id="28327-118">Kümeyi yerel olarak çalıştırıyorsanız, ``docker info`` komutunu kullanarak Docker’ın yüklü olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="28327-118">If you are running the cluster locally, check if Docker is installed by using the command ``docker info``.</span></span> <span data-ttu-id="28327-119">Yüklü değilse, aşağıdaki komutları kullanarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="28327-119">If it is not installed, install it accordingly by using the following commands:</span></span>

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```
2. <span data-ttu-id="28327-120">Aşağıdaki adımları kullanarak, Service Fabric kapsayıcı uygulamasının kümeye dağıtılmasını sağlayın:</span><span class="sxs-lookup"><span data-stu-id="28327-120">Have the Service Fabric container application deployed on the cluster, by using the following steps:</span></span>

  ```sh
git clone https://github.com/Azure-Samples/service-fabric-java-getting-started.git
cd service-fabric-java-getting-started/Services/JenkinsDocker/
```

3. <span data-ttu-id="28327-121">Azure depolama dosya Jenkins kapsayıcı örneğinin durumunu kalıcı hale getirmek istediğiniz paylaşımı, Bağlan seçeneği ayrıntılarını gerekir.</span><span class="sxs-lookup"><span data-stu-id="28327-121">You need the connect option details of the Azure storage file-share, where you want to persist the state of the Jenkins container instance.</span></span> <span data-ttu-id="28327-122">Aynı Microsoft Azure portalını kullanıyorsanız, lütfen adımları - bir Azure depolama hesabı deyin oluşturma ``sfjenkinsstorage1``.</span><span class="sxs-lookup"><span data-stu-id="28327-122">If you are using the Microsoft Azure portal for the same, please follow the steps - Create an Azure storage account, say ``sfjenkinsstorage1``.</span></span> <span data-ttu-id="28327-123">Oluşturma bir **dosya paylaşımı** bu depolama hesabı altında söyleyin ``sfjenkins``.</span><span class="sxs-lookup"><span data-stu-id="28327-123">Create a **File Share** under that storage account, say ``sfjenkins``.</span></span> <span data-ttu-id="28327-124">Tıklayın **Bağlan** Not ve dosya paylaşımı için değerleri altında görüntüler **Linux bağlanma**, deyin bu gibi aşağıdaki gibi - görünür</span><span class="sxs-lookup"><span data-stu-id="28327-124">Click on **Connect** for the file-share and note the values it displays under **Connecting from Linux**, say this would look like as follows -</span></span>
```sh
sudo mount -t cifs //sfjenkinsstorage1.file.core.windows.net/sfjenkins [mount point] -o vers=3.0,username=sfjenkinsstorage1,password=<storage_key>,dir_mode=0777,file_mode=0777
```

4. <span data-ttu-id="28327-125">Yer tutucu değerlerini güncelleştirmek ```setupentrypoint.sh``` karşılık gelen azure depolama ayrıntılarla komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="28327-125">Update the placeholder values in the ```setupentrypoint.sh``` script with corresponding azure-storage details.</span></span>
```sh
vi JenkinsSF/JenkinsOnSF/Code/setupentrypoint.sh
```
<span data-ttu-id="28327-126">Değiştir ``[REMOTE_FILE_SHARE_LOCATION]`` değerle ``//sfjenkinsstorage1.file.core.windows.net/sfjenkins`` 3 yukarıdaki noktası Bağlan çıktısından.</span><span class="sxs-lookup"><span data-stu-id="28327-126">Replace ``[REMOTE_FILE_SHARE_LOCATION]`` with the value ``//sfjenkinsstorage1.file.core.windows.net/sfjenkins`` from the output of the connect in point 3 above.</span></span>
<span data-ttu-id="28327-127">Değiştir ``[FILE_SHARE_CONNECT_OPTIONS_STRING]`` değerle ``vers=3.0,username=sfjenkinsstorage1,password=GB2NPUCQY9LDGeG9Bci5dJV91T6SrA7OxrYBUsFHyueR62viMrC6NIzyQLCKNz0o7pepGfGY+vTa9gxzEtfZHw==,dir_mode=0777,file_mode=0777`` noktasından Yukarıdaki 3.</span><span class="sxs-lookup"><span data-stu-id="28327-127">Replace ``[FILE_SHARE_CONNECT_OPTIONS_STRING]`` with the value ``vers=3.0,username=sfjenkinsstorage1,password=GB2NPUCQY9LDGeG9Bci5dJV91T6SrA7OxrYBUsFHyueR62viMrC6NIzyQLCKNz0o7pepGfGY+vTa9gxzEtfZHw==,dir_mode=0777,file_mode=0777`` from point 3 above.</span></span>

5. <span data-ttu-id="28327-128">Kümeye bağlanın ve kapsayıcı uygulamayı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="28327-128">Connect to the cluster and install the container application.</span></span>
```azurecli
sfctl cluster select --endpoint http://PublicIPorFQDN:19080   # cluster connect command
bash Scripts/install.sh
```
<span data-ttu-id="28327-129">Bu işlem, kümeye bir Jenkins kapsayıcısı yükler ve küme, Service Fabric Explorer kullanılarak izlenebilir.</span><span class="sxs-lookup"><span data-stu-id="28327-129">This installs a Jenkins container on the cluster, and can be monitored by using the Service Fabric Explorer.</span></span>

### <a name="steps"></a><span data-ttu-id="28327-130">Adımlar</span><span class="sxs-lookup"><span data-stu-id="28327-130">Steps</span></span>
1. <span data-ttu-id="28327-131">Tarayıcınızdan ``http://PublicIPorFQDN:8081`` sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="28327-131">From your browser, go to ``http://PublicIPorFQDN:8081``.</span></span> <span data-ttu-id="28327-132">Bu işlem, oturum açmak için gereken ilk yönetici parolasının yolunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="28327-132">It provides the path of the initial admin password required to sign in.</span></span> <span data-ttu-id="28327-133">Jenkins’i yönetici kullanıcı olarak kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28327-133">You can continue to use Jenkins as an admin user.</span></span> <span data-ttu-id="28327-134">Ya da ilk yönetici hesabıyla oturum açtıktan sonra kullanıcı oluşturabilir ve değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28327-134">Or you can create and change the user, after you sign in with the initial admin account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="28327-135">Kümeyi oluştururken uygulamanın uç nokta bağlantı noktası olarak 8081 bağlantı noktasının belirtildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="28327-135">Ensure that the 8081 port is specified as the application endpoint port while you are creating the cluster.</span></span>
   >

2. <span data-ttu-id="28327-136">``docker ps -a`` kullanarak kapsayıcı örneğinin kimliğini alın.</span><span class="sxs-lookup"><span data-stu-id="28327-136">Get the container instance ID by using ``docker ps -a``.</span></span>
3. <span data-ttu-id="28327-137">Kapsayıcıda Güvenli Kabuk (SSH) oturumunu açın ve Jenkins portalında gösterilen yolu yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="28327-137">Secure Shell (SSH) sign in to the container, and paste the path you were shown on the Jenkins portal.</span></span> <span data-ttu-id="28327-138">Örneğin, portalda `PATH_TO_INITIAL_ADMIN_PASSWORD` yolu gösteriliyorsa aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="28327-138">For example, if in the portal it shows the path `PATH_TO_INITIAL_ADMIN_PASSWORD`, run the following:</span></span>

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash   # This takes you inside Docker shell
  cat PATH_TO_INITIAL_ADMIN_PASSWORD
  ```

4. <span data-ttu-id="28327-139">[Yeni bir SSH anahtarı oluşturma ve SSH aracısına ekleme](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/) bölümünde anlatılan adımları kullanarak, GitHub’ı Jenkins ile çalışacak şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="28327-139">Set up GitHub to work with Jenkins, by using the steps mentioned in [Generating a new SSH key and adding it to the SSH agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).</span></span>
    * <span data-ttu-id="28327-140">GitHub’dan sağlanan yönergeleri kullanarak SSH anahtarını oluşturun ve depoyu barındıran GitHub hesabına SSH anahtarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="28327-140">Use the instructions provided by GitHub to generate the SSH key, and to add the SSH key to the GitHub account that is hosting your repository.</span></span>
    * <span data-ttu-id="28327-141">Önceki bağlantıda belirtilen komutları Jenkins Docker kabuğunda (ana bilgisayarınızda değil) çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="28327-141">Run the commands mentioned in the preceding link in the Jenkins Docker shell (and not on your host).</span></span>
    * <span data-ttu-id="28327-142">Ana bilgisayarınızdan Jenkins kabuğunda oturum açmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="28327-142">To sign in to the Jenkins shell from your host, use the following command:</span></span>

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
  ```

## <a name="set-up-jenkins-outside-a-service-fabric-cluster"></a><span data-ttu-id="28327-143">Jenkins’i Service Fabric kümesi dışında ayarlama</span><span class="sxs-lookup"><span data-stu-id="28327-143">Set up Jenkins outside a Service Fabric cluster</span></span>

<span data-ttu-id="28327-144">Jenkins’i bir Service Fabric kümesinin içinde veya dışında ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28327-144">You can set up Jenkins either inside or outside of a Service Fabric cluster.</span></span> <span data-ttu-id="28327-145">Aşağıdaki bölümlerde, kümenin dışında nasıl ayarlandığı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="28327-145">The following sections show how to set it up outside a cluster.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="28327-146">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="28327-146">Prerequisites</span></span>
<span data-ttu-id="28327-147">Docker’ın yüklü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="28327-147">You need to have Docker installed.</span></span> <span data-ttu-id="28327-148">Terminalden Docker yüklemek için aşağıdaki komutlar kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="28327-148">The following commands can be used to install Docker from the terminal:</span></span>

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```

<span data-ttu-id="28327-149">Şimdi terminalde ``docker info`` çalıştırdığınızda, çıktıda Docker hizmetinin çalıştığını göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="28327-149">Now when you run ``docker info`` in the terminal, you should see in the output that the Docker service is running.</span></span>

### <a name="steps"></a><span data-ttu-id="28327-150">Adımlar</span><span class="sxs-lookup"><span data-stu-id="28327-150">Steps</span></span>
  1. <span data-ttu-id="28327-151">Service Fabric Jenkins kapsayıcı görüntüsünü çekin: ``docker pull raunakpandya/jenkins:v1``</span><span class="sxs-lookup"><span data-stu-id="28327-151">Pull the Service Fabric Jenkins container image: ``docker pull raunakpandya/jenkins:v1``</span></span>
  2. <span data-ttu-id="28327-152">Kapsayıcı görüntüsünü çalıştırın:``docker run -itd -p 8080:8080 raunakpandya/jenkins:v1``</span><span class="sxs-lookup"><span data-stu-id="28327-152">Run the container image: ``docker run -itd -p 8080:8080 raunakpandya/jenkins:v1``</span></span>
  3. <span data-ttu-id="28327-153">Kapsayıcı görüntüsü örneğinin kimliğini alın.</span><span class="sxs-lookup"><span data-stu-id="28327-153">Get the ID of the container image instance.</span></span> <span data-ttu-id="28327-154">``docker ps –a`` komutuyla tüm Docker kapsayıcılarını listeleyebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="28327-154">You can list all the Docker containers with the command ``docker ps –a``</span></span>
  4. <span data-ttu-id="28327-155">Aşağıdaki adımları kullanarak Jenkins portalında oturum açın:</span><span class="sxs-lookup"><span data-stu-id="28327-155">Sign in to the Jenkins portal by using the following steps:</span></span>

    * ```sh
    docker exec [first-four-digits-of-container-ID] cat /var/jenkins_home/secrets/initialAdminPassword
    ```
    <span data-ttu-id="28327-156">Kapsayıcı kimliği 2d24a73b5964 ise, 2d24 kullanın.</span><span class="sxs-lookup"><span data-stu-id="28327-156">If container ID is 2d24a73b5964, use 2d24.</span></span>
    * <span data-ttu-id="28327-157">``http://<HOST-IP>:8080`` olan bu parola, portaldan Jenkins panosunda oturum açmak için gereklidir</span><span class="sxs-lookup"><span data-stu-id="28327-157">This password is required for signing in to the Jenkins dashboard from portal, which is ``http://<HOST-IP>:8080``</span></span>
    * <span data-ttu-id="28327-158">İlk defa oturum açtıktan sonra, kendi kullanıcı hesabınızı oluşturabilir ve bunu gelecekteki amaçlar için kullanabilirsiniz veya yönetici hesabını kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28327-158">After you sign in for the first time, you can create your own user account and use that for future purposes, or you can continue to use the administrator account.</span></span> <span data-ttu-id="28327-159">Bir kullanıcı oluşturduktan sonra, bu kullanıcıyla devam etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="28327-159">After you create a user, you need to continue with that.</span></span>
  5. <span data-ttu-id="28327-160">[Yeni bir SSH anahtarı oluşturma ve SSH aracısına ekleme](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/) bölümünde anlatılan adımları kullanarak, GitHub’ı Jenkins ile çalışacak şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="28327-160">Set up GitHub to work with Jenkins, by using the steps mentioned in [Generating a new SSH key and adding it to the SSH agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).</span></span>
        * <span data-ttu-id="28327-161">GitHub’dan sağlanan yönergeleri kullanarak SSH anahtarını oluşturun ve depoyu barındıran GitHub hesabına SSH anahtarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="28327-161">Use the instructions provided by GitHub to generate the SSH key, and to add the SSH key to the GitHub account that is hosting the repository.</span></span>
        * <span data-ttu-id="28327-162">Önceki bağlantıda belirtilen komutları Jenkins Docker kabuğunda (ana bilgisayarınızda değil) çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="28327-162">Run the commands mentioned in the preceding link in the Jenkins Docker shell (and not on your host).</span></span>
      * <span data-ttu-id="28327-163">Ana bilgisayarınızdan Jenkins kabuğunda oturum açmak için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="28327-163">To sign in to the Jenkins shell from your host, use the following commands:</span></span>

      ```sh
      docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
      ```

<span data-ttu-id="28327-164">Jenkins kapsayıcı görüntüsünün barındırıldığı küme veya makinede genel kullanıma yönelik bir IP bulunduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="28327-164">Ensure that the cluster or machine where the Jenkins container image is hosted has a public-facing IP.</span></span> <span data-ttu-id="28327-165">Bunun olması, Jenkins örneğinin GitHub'dan bildirimler almasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="28327-165">This enables the Jenkins instance to receive notifications from GitHub.</span></span>

## <a name="install-the-service-fabric-jenkins-plug-in-from-the-portal"></a><span data-ttu-id="28327-166">Portaldan Service Fabric Jenkins eklentisini yükleme</span><span class="sxs-lookup"><span data-stu-id="28327-166">Install the Service Fabric Jenkins plug-in from the portal</span></span>

1. <span data-ttu-id="28327-167">Şuraya gidin: ``http://PublicIPorFQDN:8081``</span><span class="sxs-lookup"><span data-stu-id="28327-167">Go to ``http://PublicIPorFQDN:8081``</span></span>
2. <span data-ttu-id="28327-168">Jenkins panosundan **Jenkins’i Yönet** > **Eklentileri Yönet** > **Gelişmiş**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="28327-168">From the Jenkins dashboard, select **Manage Jenkins** > **Manage Plugins** > **Advanced**.</span></span>
<span data-ttu-id="28327-169">Burada, bir eklentiyi karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28327-169">Here, you can upload a plug-in.</span></span> <span data-ttu-id="28327-170">**Dosya seç** seçeneğini belirleyin, ardından önkoşullar altında indirmiş olduğunuz **serviceFabric.hpi** dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="28327-170">Select **Choose file**, and then select the **serviceFabric.hpi** file, which you downloaded under prerequisites.</span></span> <span data-ttu-id="28327-171">**Karşıya Yükle**’yi seçtiğinizde Jenkins, eklentiyi otomatik olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="28327-171">When you select **Upload**, Jenkins automatically installs the plug-in.</span></span> <span data-ttu-id="28327-172">Yeniden başlatma isteniyorsa izin verin.</span><span class="sxs-lookup"><span data-stu-id="28327-172">Allow a restart if requested.</span></span>

## <a name="create-and-configure-a-jenkins-job"></a><span data-ttu-id="28327-173">Bir Jenkins işi oluşturma ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="28327-173">Create and configure a Jenkins job</span></span>

1. <span data-ttu-id="28327-174">Panodan **yeni öğe** oluşturun.</span><span class="sxs-lookup"><span data-stu-id="28327-174">Create a **new item** from dashboard.</span></span>
2. <span data-ttu-id="28327-175">Bir öğe adını girin (örneğin, **MyJob**).</span><span class="sxs-lookup"><span data-stu-id="28327-175">Enter an item name (for example, **MyJob**).</span></span> <span data-ttu-id="28327-176">**Serbest stil proje**’yi seçip **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="28327-176">Select **free-style project**, and click **OK**.</span></span>
3. <span data-ttu-id="28327-177">İş sayfasına gidip **Yapılandır** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="28327-177">Go the job page, and click **Configure**.</span></span>

   <span data-ttu-id="28327-178">a.</span><span class="sxs-lookup"><span data-stu-id="28327-178">a.</span></span> <span data-ttu-id="28327-179">Genel bölümündeki **GitHub projesi** altında, GitHub projenizin URL'sini belirtin.</span><span class="sxs-lookup"><span data-stu-id="28327-179">In the general section, under **GitHub project**, specify your GitHub project URL.</span></span> <span data-ttu-id="28327-180">Bu URL, Jenkins sürekli tümleştirme, sürekli dağıtım (CI/CD) akışı ile tümleştirmek istediğiniz Service Fabric Java uygulamasını barındırır (örneğin, ``https://github.com/sayantancs/SFJenkins``).</span><span class="sxs-lookup"><span data-stu-id="28327-180">This URL hosts the Service Fabric Java application that you want to integrate with the Jenkins continuous integration, continuous deployment (CI/CD) flow (for example, ``https://github.com/sayantancs/SFJenkins``).</span></span>

   <span data-ttu-id="28327-181">b.</span><span class="sxs-lookup"><span data-stu-id="28327-181">b.</span></span> <span data-ttu-id="28327-182">**Kaynak Kodu Yönetimi** bölümünde **Git**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="28327-182">Under the **Source Code Management** section, select **Git**.</span></span> <span data-ttu-id="28327-183">Jenkins CI/CD akışıyla tümleştirmek istediğiniz Service Fabric Java uygulamasını barındıran deponun URL'sini belirtin (örneğin, ``https://github.com/sayantancs/SFJenkins.git``).</span><span class="sxs-lookup"><span data-stu-id="28327-183">Specify the repository URL that hosts the Service Fabric Java application that you want to integrate with the Jenkins CI/CD flow (for example, ``https://github.com/sayantancs/SFJenkins.git``).</span></span> <span data-ttu-id="28327-184">Ayrıca, burada hangi dalın derleneceğini belirtebilirsiniz (örneğin, **/master**).</span><span class="sxs-lookup"><span data-stu-id="28327-184">Also, you can specify here which branch to build (for example, **/master**).</span></span>
4. <span data-ttu-id="28327-185">*GitHub*’ınızı (depoyu barındıran) Jenkins ile konuşabilecek şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="28327-185">Configure your *GitHub* (which is hosting the repository) so that it is able to talk to Jenkins.</span></span> <span data-ttu-id="28327-186">Aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="28327-186">Use the following steps:</span></span>

   <span data-ttu-id="28327-187">a.</span><span class="sxs-lookup"><span data-stu-id="28327-187">a.</span></span> <span data-ttu-id="28327-188">GitHub depo sayfanıza gidin.</span><span class="sxs-lookup"><span data-stu-id="28327-188">Go to your GitHub repository page.</span></span> <span data-ttu-id="28327-189">**Ayarlar** > **Tümleştirmeler ve Hizmetler** öğesine gidin.</span><span class="sxs-lookup"><span data-stu-id="28327-189">Go to **Settings** > **Integrations and Services**.</span></span>

   <span data-ttu-id="28327-190">b.</span><span class="sxs-lookup"><span data-stu-id="28327-190">b.</span></span> <span data-ttu-id="28327-191">**Hizmet Ekle**’yi seçin, **Jenkins** yazın ve **Jenkins-GitHub eklentisi**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="28327-191">Select **Add Service**, type **Jenkins**, and select the **Jenkins-GitHub plugin**.</span></span>

   <span data-ttu-id="28327-192">c.</span><span class="sxs-lookup"><span data-stu-id="28327-192">c.</span></span> <span data-ttu-id="28327-193">Jenkins web kancası URL'nizi girin (varsayılan olarak, ``http://<PublicIPorFQDN>:8081/github-webhook/`` olmalıdır).</span><span class="sxs-lookup"><span data-stu-id="28327-193">Enter your Jenkins webhook URL (by default, it should be ``http://<PublicIPorFQDN>:8081/github-webhook/``).</span></span> <span data-ttu-id="28327-194">**Hizmet ekle/güncelleştir** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="28327-194">Click **add/update service**.</span></span>

   <span data-ttu-id="28327-195">d.</span><span class="sxs-lookup"><span data-stu-id="28327-195">d.</span></span> <span data-ttu-id="28327-196">Jenkins örneğinize bir test olayı gönderilir.</span><span class="sxs-lookup"><span data-stu-id="28327-196">A test event is sent to your Jenkins instance.</span></span> <span data-ttu-id="28327-197">GitHub’da web kancasının yanında yeşil renkli bir onay işareti görürsünüz ve projeniz derlenir.</span><span class="sxs-lookup"><span data-stu-id="28327-197">You should see a green check by the webhook in GitHub, and your project will build.</span></span>

   <span data-ttu-id="28327-198">e.</span><span class="sxs-lookup"><span data-stu-id="28327-198">e.</span></span> <span data-ttu-id="28327-199">**Derleme Tetikleyicileri** bölümünde, istediğiniz derleme seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="28327-199">Under the **Build Triggers** section, select which build option you want.</span></span> <span data-ttu-id="28327-200">Bu örnekte, depoda bazı itmeler gerçekleştiğinde derleme tetiklemeyi istersiniz.</span><span class="sxs-lookup"><span data-stu-id="28327-200">For this example, you want to trigger a build whenever some push to the repository happens.</span></span> <span data-ttu-id="28327-201">Bu nedenle **GITScm yoklaması için GitHub kanca tetikleyicisi**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="28327-201">So you select **GitHub hook trigger for GITScm polling**.</span></span> <span data-ttu-id="28327-202">(Daha önce bu seçenek **GitHub’a bir değişiklik uygulandığında derle** olarak adlandırılıyordu.)</span><span class="sxs-lookup"><span data-stu-id="28327-202">(Previously, this option was called **Build when a change is pushed to GitHub**.)</span></span>

   <span data-ttu-id="28327-203">f.</span><span class="sxs-lookup"><span data-stu-id="28327-203">f.</span></span> <span data-ttu-id="28327-204">**Derleme bölümü** altında, **Derleme adımı ekle** açılır listesinden **Gradle Betiğini Çağır** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="28327-204">Under the **Build section**, from the drop-down **Add build step**, select the option **Invoke Gradle Script**.</span></span> <span data-ttu-id="28327-205">Açılan pencere öğesinde, uygulamanız için **Kök derleme betiği** yolunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="28327-205">In the widget that comes, specify the path to **Root build script** for your application.</span></span> <span data-ttu-id="28327-206">Belirtilen yoldan build.gradle’ı alır ve buna göre çalışır.</span><span class="sxs-lookup"><span data-stu-id="28327-206">It picks up build.gradle from the path specified, and works accordingly.</span></span> <span data-ttu-id="28327-207">``MyActor`` adlı bir proje oluşturursanız (Eclipse eklentisini veya Yeoman oluşturucuyu kullanarak), kök derleme betiği ``${WORKSPACE}/MyActor`` içermelidir.</span><span class="sxs-lookup"><span data-stu-id="28327-207">If you create a project named ``MyActor`` (using the Eclipse plug-in or Yeoman generator), the root build script should contain ``${WORKSPACE}/MyActor``.</span></span> <span data-ttu-id="28327-208">Bunun nasıl göründüğüne ilişkin bir örnek için aşağıdaki ekran görüntüsüne bakın:</span><span class="sxs-lookup"><span data-stu-id="28327-208">See the following screenshot for an example of what this looks like:</span></span>

    ![Service Fabric Jenkins Derleme eylemi][build-step]

   <span data-ttu-id="28327-210">g.</span><span class="sxs-lookup"><span data-stu-id="28327-210">g.</span></span> <span data-ttu-id="28327-211">**Derleme Sonrası Eylemler** açılır listesinden **Service Fabric Projesini Dağıt**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="28327-211">From the **Post-Build Actions** drop-down, select **Deploy Service Fabric Project**.</span></span> <span data-ttu-id="28327-212">Burada, Jenkins tarafından derlenen Service Fabric uygulamasının dağıtılacağı kümenin ayrıntılarını sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="28327-212">Here you need to provide cluster details where the Jenkins compiled Service Fabric application would be deployed.</span></span> <span data-ttu-id="28327-213">Uygulamayı dağıtmak için kullanılan ek uygulama ayrıntıları da sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28327-213">You can also provide additional application details used to deploy the application.</span></span> <span data-ttu-id="28327-214">Bunun nasıl göründüğüne ilişkin bir örnek için aşağıdaki ekran görüntüsüne bakın:</span><span class="sxs-lookup"><span data-stu-id="28327-214">See the following screenshot for an example of what this looks like:</span></span>

    ![Service Fabric Jenkins Derleme eylemi][post-build-step]

   > [!NOTE]
   > <span data-ttu-id="28327-216">Burada küme, Jenkins kapsayıcı görüntüsünü dağıtmak için Service Fabric kullandığınız durumda Jenkins kapsayıcı uygulamasını barındıran kümeyle aynı olabilir.</span><span class="sxs-lookup"><span data-stu-id="28327-216">The cluster here could be same as the one hosting the Jenkins container application, in case you are using Service Fabric to deploy the Jenkins container image.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="28327-217">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="28327-217">Next steps</span></span>
<span data-ttu-id="28327-218">GitHub ve Jenkins yapılandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="28327-218">GitHub and Jenkins are now configured.</span></span> <span data-ttu-id="28327-219">https://github.com/sayantancs/SFJenkins depo örneğinde, ``MyActor`` projenizde bazı örnek değişiklikler yapmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="28327-219">Consider making some sample change in your ``MyActor`` project in the repository example, https://github.com/sayantancs/SFJenkins.</span></span> <span data-ttu-id="28327-220">Değişikliklerinizi uzak ``master`` dalına (veya birlikte çalışmak üzere yapılandırdığınız herhangi bir dala) gönderin.</span><span class="sxs-lookup"><span data-stu-id="28327-220">Push your changes to a remote ``master`` branch (or any branch that you have configured to work with).</span></span> <span data-ttu-id="28327-221">Bunun yapılması, yapılandırmış olduğunuz ``MyJob`` Jenkins işini tetikler.</span><span class="sxs-lookup"><span data-stu-id="28327-221">This triggers the Jenkins job, ``MyJob``, that you configured.</span></span> <span data-ttu-id="28327-222">Bu işlem GitHub’dan değişiklikleri getirir, derler ve derleme sonrası eylemlerde belirttiğiniz küme uç noktasına uygulamayı dağıtır.</span><span class="sxs-lookup"><span data-stu-id="28327-222">It fetches the changes from GitHub, builds them, and deploys the application to the cluster endpoint you specified in post-build actions.</span></span>  

  <!-- Images -->
  [build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/build-step.png
  [post-build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/post-build-step.png
