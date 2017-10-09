---
title: "aaaJenkins CI/CD Azure kapsayıcı Hizmeti'nde Kubernetes ile | Microsoft Docs"
description: "Tooautomate bir CI/CD işleminin nasıl Jenkins toodeploy ve Kubernetes Azure kapsayıcı Hizmeti'nde bir kapsayıcılı uygulamasını yükseltme"
services: container-service
documentationcenter: 
author: chzbrgr71
manager: johny
editor: 
tags: acs, azure-container-service, jenkins
keywords: "Docker, kapsayıcıları, Kubernetes, Azure, Jenkins"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: briar
ms.custom: mvc
ms.openlocfilehash: e00e13bf06619bed73e82878777e55458ea3dd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a><span data-ttu-id="f5d18-104">Azure kapsayıcı hizmeti ve Kubernetes Jenkins tümleştirme</span><span class="sxs-lookup"><span data-stu-id="f5d18-104">Jenkins integration with Azure Container Service and Kubernetes</span></span> 
<span data-ttu-id="f5d18-105">Bu öğreticide, biz hello işlem tooset sürekli tümleştirme çok kapsayıcı uygulamasının Azure kapsayıcı hizmeti hello Jenkins platformu kullanılarak Kubernetes yol.</span><span class="sxs-lookup"><span data-stu-id="f5d18-105">In this tutorial, we walk through hello process tooset up continuous integration of a multi-container application into Azure Container Service Kubernetes using hello Jenkins platform.</span></span> <span data-ttu-id="f5d18-106">Merhaba iş akışı Docker hub'a hello kapsayıcı görüntüyü güncelleştirir ve dağıtımı sunumu kullanarak hello Kubernetes pod'ları yükseltir.</span><span class="sxs-lookup"><span data-stu-id="f5d18-106">hello workflow updates hello container image in Docker Hub and upgrades hello Kubernetes pods using a deployment rollout.</span></span> 

## <a name="high-level-process"></a><span data-ttu-id="f5d18-107">Yüksek düzeyli işlem</span><span class="sxs-lookup"><span data-stu-id="f5d18-107">High level process</span></span>
<span data-ttu-id="f5d18-108">Bu makalede ayrıntılı hello temel adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f5d18-108">hello basic steps detailed in this article are:</span></span> 
- <span data-ttu-id="f5d18-109">Kapsayıcı Hizmeti'nde bir Kubernetes küme yükleyin</span><span class="sxs-lookup"><span data-stu-id="f5d18-109">Install a Kubernetes cluster in Container Service</span></span>
- <span data-ttu-id="f5d18-110">Jenkins ayarlama ve erişimi tooContainer hizmetini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f5d18-110">Set up Jenkins and configure access tooContainer Service</span></span>
- <span data-ttu-id="f5d18-111">Jenkins iş akışı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f5d18-111">Create a Jenkins workflow</span></span>
- <span data-ttu-id="f5d18-112">Merhaba CI/CD işlemi son tooend test</span><span class="sxs-lookup"><span data-stu-id="f5d18-112">Test hello CI/CD process end tooend</span></span>

## <a name="install-a-kubernetes-cluster"></a><span data-ttu-id="f5d18-113">Kubernetes küme yükleyin</span><span class="sxs-lookup"><span data-stu-id="f5d18-113">Install a Kubernetes cluster</span></span>
    
<span data-ttu-id="f5d18-114">Merhaba Kubernetes hello aşağıdaki adımları kullanarak Azure kapsayıcı hizmeti kümesinde dağıtın.</span><span class="sxs-lookup"><span data-stu-id="f5d18-114">Deploy hello Kubernetes cluster in Azure Container Service using hello following steps.</span></span> <span data-ttu-id="f5d18-115">Tam belgelerine bulunduğu [burada](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="f5d18-115">Full documentation is located [here](container-service-kubernetes-walkthrough.md).</span></span>

### <a name="step-1-create-a-resource-group"></a><span data-ttu-id="f5d18-116">1. adım: bir kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="f5d18-116">Step 1: Create a resource group</span></span>
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-hello-cluster"></a><span data-ttu-id="f5d18-117">2. adım: hello küme dağıtma</span><span class="sxs-lookup"><span data-stu-id="f5d18-117">Step 2: Deploy hello cluster</span></span>
> [!NOTE]
> <span data-ttu-id="f5d18-118">Merhaba aşağıdaki adımları hello ~/.ssh klasöründe bulunan yerel bir SSH ortak anahtarı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f5d18-118">hello following steps require a local SSH public key stored in hello ~/.ssh folder.</span></span>
>

```azurecli
RESOURCE_GROUP=my-resource-group
DNS_PREFIX=some-unique-value
CLUSTER_NAME=any-acs-cluster-name

az acs create \
--orchestrator-type=kubernetes \
--resource-group $RESOURCE_GROUP \
--name=$CLUSTER_NAME \
--dns-prefix=$DNS_PREFIX \
--ssh-key-value ~/.ssh/id_rsa.pub \
--admin-username=azureuser \
--master-count=1 \
--agent-count=5 \
--agent-vm-size=Standard_D1_v2
```

## <a name="set-up-jenkins-and-configure-access-toocontainer-service"></a><span data-ttu-id="f5d18-119">Jenkins ayarlama ve erişimi tooContainer hizmetini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f5d18-119">Set up Jenkins and configure access tooContainer Service</span></span>

### <a name="step-1-install-jenkins"></a><span data-ttu-id="f5d18-120">1. adım: Jenkins yükleme</span><span class="sxs-lookup"><span data-stu-id="f5d18-120">Step 1: Install Jenkins</span></span>
1. <span data-ttu-id="f5d18-121">Ubuntu 16.04 ile bir Azure VM oluşturma LTS.</span><span class="sxs-lookup"><span data-stu-id="f5d18-121">Create an Azure VM with Ubuntu 16.04 LTS.</span></span>  <span data-ttu-id="f5d18-122">Hello sonraki adımlar bu yana tooconnect toothis VM kullanarak kümesi hello 'Kimlik doğrulama türü' too'SSH ortak anahtar, yerel makinenize bash ' ve ~/.ssh klasörünüzde yerel olarak depolanan Yapıştır hello SSH ortak anahtarı.</span><span class="sxs-lookup"><span data-stu-id="f5d18-122">Since later in hello steps you will need tooconnect toothis VM using bash on your local machine, set hello 'Authentication type' too'SSH public key' and paste hello SSH public key that is stored locally in your ~/.ssh folder.</span></span>  <span data-ttu-id="f5d18-123">Ayrıca, bu kullanıcı adı gerekli tooview hello Jenkins Pano olacağından ve daha sonraki adımlarda toohello Jenkins VM bağlama belirtin hello 'User name' not edin.</span><span class="sxs-lookup"><span data-stu-id="f5d18-123">Also, take note of hello 'User name' that you specify since this user name will be needed tooview hello Jenkins dashboard and for connecting toohello Jenkins VM in later steps.</span></span>
2. <span data-ttu-id="f5d18-124">Jenkins yüklemeniz [yönergeleri](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span><span class="sxs-lookup"><span data-stu-id="f5d18-124">Install Jenkins via these [instructions](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span></span> <span data-ttu-id="f5d18-125">Daha ayrıntılı bir öğretici altındadır [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span><span class="sxs-lookup"><span data-stu-id="f5d18-125">A more detailed tutorial is at [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span></span>
3. <span data-ttu-id="f5d18-126">tooview Jenkins Pano yerel makinenizde Merhaba, erişim tooport 8080 izin veren bir gelen kuralı ekleyerek hello Azure ağ güvenlik grubu tooallow bağlantı noktası 8080 güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="f5d18-126">tooview hello Jenkins dashboard on your local machine, update hello Azure network security group tooallow port 8080 by adding an inbound rule that allows access tooport 8080.</span></span>  <span data-ttu-id="f5d18-127">Alternatif olarak, şu komutu çalıştırarak bağlantı noktası iletme Kurulum:`ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span><span class="sxs-lookup"><span data-stu-id="f5d18-127">Alternatively, you may setup port forwarding by running this command: `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span></span>
4. <span data-ttu-id="f5d18-128">Toohello genel IP giderek Hello tarayıcı kullanarak tooyour Jenkins sunucusuna (http:// < your_jenkins_public_ip >: 8080) ve hello hello Jenkins panosunu hello ilk yönetici parolası ile ilk kez kilidini açın.</span><span class="sxs-lookup"><span data-stu-id="f5d18-128">Connect tooyour Jenkins server using hello browser by navigating toohello public IP (http://<your_jenkins_public_ip>:8080) and unlock hello Jenkins dashboard for hello first time with hello initial admin password.</span></span>  <span data-ttu-id="f5d18-129">Merhaba yönetici parolası hello Jenkins VM üzerinde /var/lib/jenkins/secrets/initialAdminPassword konumunda depolanır.</span><span class="sxs-lookup"><span data-stu-id="f5d18-129">hello admin password is stored at /var/lib/jenkins/secrets/initialAdminPassword on hello Jenkins VM.</span></span>  <span data-ttu-id="f5d18-130">Bu paroladır tooSSH içine bir kolay bir yolu tooget Jenkins VM hello: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span><span class="sxs-lookup"><span data-stu-id="f5d18-130">An easy way tooget this password is tooSSH into hello Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="f5d18-131">Ardından, çalıştırın: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span><span class="sxs-lookup"><span data-stu-id="f5d18-131">Next, run: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span></span>
5. <span data-ttu-id="f5d18-132">Bunlar aracılığıyla hello Jenkins makinenize Docker yüklemek [yönergeleri](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span><span class="sxs-lookup"><span data-stu-id="f5d18-132">Install Docker on hello Jenkins machine via these [instructions](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span></span> <span data-ttu-id="f5d18-133">Docker komutları toobe Jenkins işlerini çalıştırmak için bu sağlar.</span><span class="sxs-lookup"><span data-stu-id="f5d18-133">This allows for Docker commands toobe run in Jenkins jobs.</span></span>
6. <span data-ttu-id="f5d18-134">Docker izinleri tooallow Jenkins tooaccess hello Docker uç noktasını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f5d18-134">Configure Docker permissions tooallow Jenkins tooaccess hello Docker endpoint.</span></span>

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. <span data-ttu-id="f5d18-135">Yükleme `kubectl` CLI Jenkins üzerinde.</span><span class="sxs-lookup"><span data-stu-id="f5d18-135">Install `kubectl` CLI on Jenkins.</span></span> <span data-ttu-id="f5d18-136">Daha fazla ayrıntı altındadır [yükleme ve kubectl ayarlama](https://kubernetes.io/docs/tasks/kubectl/install/).</span><span class="sxs-lookup"><span data-stu-id="f5d18-136">More details are at [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>  <span data-ttu-id="f5d18-137">Jenkins işleri 'kubectl' toomanage kullanabilir ve toohello Kubernetes küme dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f5d18-137">Jenkins jobs will use 'kubectl' toomanage and deploy toohello Kubernetes cluster.</span></span>

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-toohello-kubernetes-cluster"></a><span data-ttu-id="f5d18-138">2. adım: erişim toohello Kubernetes kümesi</span><span class="sxs-lookup"><span data-stu-id="f5d18-138">Step 2: Set up access toohello Kubernetes cluster</span></span>

> [!NOTE]
> <span data-ttu-id="f5d18-139">Aşağıdaki adımları birden çok yaklaşımlar tooaccomplishing hello vardır.</span><span class="sxs-lookup"><span data-stu-id="f5d18-139">There are multiple approaches tooaccomplishing hello following steps.</span></span> <span data-ttu-id="f5d18-140">Sizin için en kolayıdır hello yaklaşımı kullanın.</span><span class="sxs-lookup"><span data-stu-id="f5d18-140">Use hello approach that is easiest for you.</span></span>
>

1. <span data-ttu-id="f5d18-141">Kopya hello `kubectl` Jenkins, böylece Jenkins işleri erişim toohello Kubernetes küme makine yapılandırma dosyası toohello.</span><span class="sxs-lookup"><span data-stu-id="f5d18-141">Copy hello `kubectl` config file toohello Jenkins machine so that Jenkins jobs have access toohello Kubernetes cluster.</span></span> <span data-ttu-id="f5d18-142">Bu yönergeleri varsayar Jenkins VM hello olandan farklı bir makineden bash kullanıyorsanız ve yerel bir SSH ortak anahtarını hello makinenin ~/.ssh klasöründe depolanır.</span><span class="sxs-lookup"><span data-stu-id="f5d18-142">These instructions assume that you are using bash from a different machine than hello Jenkins VM and that a local SSH public key is stored in hello machine's ~/.ssh folder.</span></span>

```bash
export KUBE_MASTER=<your_cluster_master_fqdn>
export JENKINS_USER=<your_jenkins_user>
export JENKINS_SERVER=<your_jenkins_public_ip>
sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir -m 777 /home/$JENKINS_USER/.kube/ \
&& sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir /var/lib/jenkins/.kube/ \
&& sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config $JENKINS_USER@$JENKINS_SERVER:~/.kube/config \
&& sudo ssh -i ~/.ssh/id_rsa $JENKINS_USER@$JENKINS_SERVER sudo cp /home/$JENKINS_USER/.kube/config /var/lib/jenkins/.kube/config \
```
        
2. <span data-ttu-id="f5d18-143">Bu hello Kubernetes Jenkins doğrulama kümedir erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="f5d18-143">Validate from Jenkins that hello Kubernetes cluster is accessible.</span></span>  <span data-ttu-id="f5d18-144">toodo hello Jenkins VM içine bu, SSH: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span><span class="sxs-lookup"><span data-stu-id="f5d18-144">toodo this, SSH into hello Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="f5d18-145">Ardından, Jenkins tooyour küme başarıyla bağlanabilir doğrulayın: `kubectl cluster-info`.</span><span class="sxs-lookup"><span data-stu-id="f5d18-145">Next, verify Jenkins can successfully connect tooyour cluster: `kubectl cluster-info`.</span></span>
    

## <a name="create-a-jenkins-workflow"></a><span data-ttu-id="f5d18-146">Jenkins iş akışı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f5d18-146">Create a Jenkins workflow</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f5d18-147">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f5d18-147">Prerequisites</span></span>

- <span data-ttu-id="f5d18-148">Kod deposu için GitHub hesabı.</span><span class="sxs-lookup"><span data-stu-id="f5d18-148">GitHub account for code repo.</span></span>
- <span data-ttu-id="f5d18-149">Toostore ve güncelleştirme docker hub'a hesabı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f5d18-149">Docker Hub account toostore and update images.</span></span>
- <span data-ttu-id="f5d18-150">Yeniden ve güncelleştirilmiş kapsayıcılı uygulama.</span><span class="sxs-lookup"><span data-stu-id="f5d18-150">Containerized application that can be rebuilt and updated.</span></span> <span data-ttu-id="f5d18-151">Bu örnek kapsayıcı uygulaması Golang içinde yazılmış kullanabilirsiniz: https://github.com/chzbrgr71/go-web</span><span class="sxs-lookup"><span data-stu-id="f5d18-151">You can use this sample container app written in Golang: https://github.com/chzbrgr71/go-web</span></span> 

> [!NOTE]
> <span data-ttu-id="f5d18-152">Merhaba aşağıdaki adımlarda kendi GitHub hesabınızda gerçekleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="f5d18-152">hello following steps must be performed in your own GitHub account.</span></span> <span data-ttu-id="f5d18-153">Depodaki, yukarıda ücretsiz tooclone hello eşitleyerek ancak Jenkins erişmek ve kendi hesabı tooconfigure hello kancalarını kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f5d18-153">Feel free tooclone hello above repo, but you must use your own account tooconfigure hello webhooks and Jenkins access.</span></span>
>

### <a name="step-1-deploy-initial-v1-of-application"></a><span data-ttu-id="f5d18-154">1. adım: uygulamanın ilk v1 dağıtma</span><span class="sxs-lookup"><span data-stu-id="f5d18-154">Step 1: Deploy initial v1 of application</span></span>
1. <span data-ttu-id="f5d18-155">Merhaba uygulama hello Geliştirici makineden komutları aşağıdaki hello ile oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f5d18-155">Build hello app from hello developer machine with hello following commands.</span></span> <span data-ttu-id="f5d18-156">Değiştir `myrepo` kendi değerlerinizle.</span><span class="sxs-lookup"><span data-stu-id="f5d18-156">Replace `myrepo` with your own.</span></span>
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. <span data-ttu-id="f5d18-157">Görüntü tooDocker Hub iletin.</span><span class="sxs-lookup"><span data-stu-id="f5d18-157">Push image tooDocker Hub.</span></span>

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. <span data-ttu-id="f5d18-158">Toohello Kubernetes küme dağıtın.</span><span class="sxs-lookup"><span data-stu-id="f5d18-158">Deploy toohello Kubernetes cluster.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="f5d18-159">Merhaba Düzenle `go-web.yaml` tooupdate kapsayıcı görüntü ve depo dosya.</span><span class="sxs-lookup"><span data-stu-id="f5d18-159">Edit hello `go-web.yaml` file tooupdate your container image and repo.</span></span>
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a><span data-ttu-id="f5d18-160">2. adım: Jenkins sistem yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f5d18-160">Step 2: Configure Jenkins system</span></span>
1. <span data-ttu-id="f5d18-161">Tıklatın **Jenkins yönetmek** > **sistem yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="f5d18-161">Click **Manage Jenkins** > **Configure System**.</span></span>
2. <span data-ttu-id="f5d18-162">Altında **GitHub**seçin **GitHub Sunucu Ekle**.</span><span class="sxs-lookup"><span data-stu-id="f5d18-162">Under **GitHub**, select **Add GitHub Server**.</span></span>
3. <span data-ttu-id="f5d18-163">Bırakın **API URL** varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="f5d18-163">Leave **API URL** as default.</span></span>
4. <span data-ttu-id="f5d18-164">Altında **kimlik bilgileri**, Jenkins kimlik bilgilerini kullanarak eklemek **gizli metin**.</span><span class="sxs-lookup"><span data-stu-id="f5d18-164">Under **Credentials**, add a Jenkins credential using **Secret text**.</span></span> <span data-ttu-id="f5d18-165">GitHub kullanıcı hesap ayarlarınızda yapılandırılmış GitHub kişisel erişim belirteçleri kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="f5d18-165">We recommend using GitHub personal access tokens, which are configured in your GitHub user account settings.</span></span> <span data-ttu-id="f5d18-166">Bunun hakkında daha fazla ayrıntı [burada.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span><span class="sxs-lookup"><span data-stu-id="f5d18-166">More details on this [here.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span></span>
5. <span data-ttu-id="f5d18-167">Tıklatın **Bağlantıyı Sına** tooensure bu doğru yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="f5d18-167">Click **Test connection** tooensure this is configured correctly.</span></span>
6. <span data-ttu-id="f5d18-168">Altında **genel özellikleri**, bir ortam değişkeni ekleyin `DOCKER_HUB` ve Docker hub'a parolanızı girin.</span><span class="sxs-lookup"><span data-stu-id="f5d18-168">Under **Global Properties**, add an environment variable `DOCKER_HUB` and provide your Docker Hub password.</span></span> <span data-ttu-id="f5d18-169">(Bu gösteride kullanışlıdır ancak bir üretim senaryosu daha güvenli bir yöntem gerektirir.)</span><span class="sxs-lookup"><span data-stu-id="f5d18-169">(This is useful in this demo, but a production scenario would require a more secure approach.)</span></span>
7. <span data-ttu-id="f5d18-170">Kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f5d18-170">Save.</span></span>

![Jenkins GitHub erişim](./media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-hello-jenkins-workflow"></a><span data-ttu-id="f5d18-172">3. adım: Merhaba Jenkins iş akışı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f5d18-172">Step 3: Create hello Jenkins workflow</span></span>
1. <span data-ttu-id="f5d18-173">Jenkins öğesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f5d18-173">Create a Jenkins item.</span></span>
2. <span data-ttu-id="f5d18-174">Bir ad girin (örneğin, "Web'de Git") seçip **Freestyle proje**.</span><span class="sxs-lookup"><span data-stu-id="f5d18-174">Provide a name (for example, "go-web") and select **Freestyle Project**.</span></span> 
3. <span data-ttu-id="f5d18-175">Denetleme **GitHub proje** ve hello URL tooyour GitHub deposuna sağlayın.</span><span class="sxs-lookup"><span data-stu-id="f5d18-175">Check **GitHub project** and provide hello URL tooyour GitHub repo.</span></span>
4. <span data-ttu-id="f5d18-176">İçinde **kaynak kodu Yönetimi**, hello GitHub deposuna URL ve kimlik bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="f5d18-176">In **Source Code Management**, provide hello GitHub repo URL and credentials.</span></span> 
5. <span data-ttu-id="f5d18-177">Ekleme bir **derleme adımı** türü **Kabuk yürütme** ve kullanım hello aşağıdaki metin:</span><span class="sxs-lookup"><span data-stu-id="f5d18-177">Add a **Build Step** of type **Execute shell** and use hello following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. <span data-ttu-id="f5d18-178">Başka bir tane eklemek **derleme adımı** türü **Kabuk yürütme** ve kullanım hello aşağıdaki metin:</span><span class="sxs-lookup"><span data-stu-id="f5d18-178">Add another **Build Step** of type **Execute shell** and use hello following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Jenkins derleme adımları](./media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. <span data-ttu-id="f5d18-180">Merhaba Jenkins öğeyi kaydetmek ve test **şimdi yapı**.</span><span class="sxs-lookup"><span data-stu-id="f5d18-180">Save hello Jenkins item and test with **Build Now**.</span></span>

### <a name="step-4-connect-github-webhook"></a><span data-ttu-id="f5d18-181">4. adım: GitHub Web kancası bağlanma</span><span class="sxs-lookup"><span data-stu-id="f5d18-181">Step 4: Connect GitHub webhook</span></span>
1. <span data-ttu-id="f5d18-182">Merhaba Jenkins öğeyi oluşturduğunuz tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="f5d18-182">In hello Jenkins item you created, click **Configure**.</span></span>
2. <span data-ttu-id="f5d18-183">Altında **yapı tetikleyicileri**seçin **GITScm yoklama için GitHub kanca tetikleyici** ve **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="f5d18-183">Under **Build Triggers**, select **GitHub hook trigger for GITScm polling** and **Save**.</span></span> <span data-ttu-id="f5d18-184">Bu, hello GitHub Web kancası otomatik olarak yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="f5d18-184">This automatically configures hello GitHub webhook.</span></span>
3. <span data-ttu-id="f5d18-185">Web Git, GitHub deposuna içinde tıklatın **ayarlar > Web Kancalarını**.</span><span class="sxs-lookup"><span data-stu-id="f5d18-185">In your GitHub repo for go-web, click **Settings > Webhooks**.</span></span>
4. <span data-ttu-id="f5d18-186">Bu hello Jenkins Web kancası URL'si başarıyla eklendi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f5d18-186">Verify that hello Jenkins webhook URL was added successfully.</span></span> <span data-ttu-id="f5d18-187">Merhaba URL "github-Web kancası" bitmelidir.</span><span class="sxs-lookup"><span data-stu-id="f5d18-187">hello URL should end in "github-webhook".</span></span>

![Jenkins Web kancası yapılandırma](./media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-hello-cicd-process-end-tooend"></a><span data-ttu-id="f5d18-189">Merhaba CI/CD işlemi son tooend test</span><span class="sxs-lookup"><span data-stu-id="f5d18-189">Test hello CI/CD process end tooend</span></span>

1. <span data-ttu-id="f5d18-190">Merhaba depodaki ve anında iletme/eşitlemesi için kod hello GitHub deposuyla güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="f5d18-190">Update code for hello repo and push/synch with hello GitHub repository.</span></span>
2. <span data-ttu-id="f5d18-191">Merhaba Jenkins konsolundan hello denetleyin **yapı geçmiş** ve o hello doğrulama işi çalıştıktan.</span><span class="sxs-lookup"><span data-stu-id="f5d18-191">From hello Jenkins console, check hello **Build History** and validate that hello job has run.</span></span> <span data-ttu-id="f5d18-192">Konsol çıkış toosee ayrıntıları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="f5d18-192">View console output toosee details.</span></span>
3. <span data-ttu-id="f5d18-193">Kubernetes hello ayrıntılarını görüntüleme dağıtım yükseltme:</span><span class="sxs-lookup"><span data-stu-id="f5d18-193">From Kubernetes, view details of hello upgraded deployment:</span></span>

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a><span data-ttu-id="f5d18-194">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f5d18-194">Next steps</span></span>

- <span data-ttu-id="f5d18-195">Azure kapsayıcı kayıt defteri dağıtın ve güvenli bir depoda görüntüleri saklamak.</span><span class="sxs-lookup"><span data-stu-id="f5d18-195">Deploy Azure Container Registry and store images in a secure repository.</span></span> <span data-ttu-id="f5d18-196">Bkz: [Azure kapsayıcı kayıt defteri belgeleri](https://docs.microsoft.com/azure/container-registry).</span><span class="sxs-lookup"><span data-stu-id="f5d18-196">See [Azure Container Registry docs](https://docs.microsoft.com/azure/container-registry).</span></span>
- <span data-ttu-id="f5d18-197">Yan yana dağıtım ve otomatikleştirilmiş testleri Jenkins içeren daha karmaşık bir iş akışı oluşturma.</span><span class="sxs-lookup"><span data-stu-id="f5d18-197">Build a more complex workflow that includes side-by-side deployment and automated tests in Jenkins.</span></span>
- <span data-ttu-id="f5d18-198">Merhaba CI/CD Jenkins ve Kubernetes hakkında daha fazla bilgi için bkz: [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span><span class="sxs-lookup"><span data-stu-id="f5d18-198">For more information about CI/CD with Jenkins and Kubernetes, see hello [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span></span>
