---
title: "Jenkins CI/CD Azure kapsayıcı Hizmeti'nde Kubernetes ile | Microsoft Docs"
description: "Dağıtıp Kubernetes Azure kapsayıcı Hizmeti'nde bir kapsayıcılı uygulamasını yükseltme Jenkins CI/CD işlemine otomatikleştirme"
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
ms.openlocfilehash: 2078d0694fc4dd6e83ecd2792588b4254980cd78
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a><span data-ttu-id="8cbac-104">Azure kapsayıcı hizmeti ve Kubernetes Jenkins tümleştirme</span><span class="sxs-lookup"><span data-stu-id="8cbac-104">Jenkins integration with Azure Container Service and Kubernetes</span></span> 
<span data-ttu-id="8cbac-105">Bu öğreticide, Azure kapsayıcı hizmeti Jenkins platformu kullanılarak Kubernetes çok kapsayıcı uygulamasına, sürekli tümleştirme ayarlamak için işlem size rehberlik eder.</span><span class="sxs-lookup"><span data-stu-id="8cbac-105">In this tutorial, we walk through the process to set up continuous integration of a multi-container application into Azure Container Service Kubernetes using the Jenkins platform.</span></span> <span data-ttu-id="8cbac-106">İş akışı Docker hub'a kapsayıcı görüntüyü güncelleştirir ve dağıtımı sunumu kullanarak Kubernetes pod'ları yükseltir.</span><span class="sxs-lookup"><span data-stu-id="8cbac-106">The workflow updates the container image in Docker Hub and upgrades the Kubernetes pods using a deployment rollout.</span></span> 

## <a name="high-level-process"></a><span data-ttu-id="8cbac-107">Yüksek düzeyli işlem</span><span class="sxs-lookup"><span data-stu-id="8cbac-107">High level process</span></span>
<span data-ttu-id="8cbac-108">Bu makalede ayrıntılı temel adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8cbac-108">The basic steps detailed in this article are:</span></span> 
- <span data-ttu-id="8cbac-109">Kapsayıcı Hizmeti'nde bir Kubernetes küme yükleyin</span><span class="sxs-lookup"><span data-stu-id="8cbac-109">Install a Kubernetes cluster in Container Service</span></span>
- <span data-ttu-id="8cbac-110">Jenkins ayarlayın ve kapsayıcı hizmeti erişimi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8cbac-110">Set up Jenkins and configure access to Container Service</span></span>
- <span data-ttu-id="8cbac-111">Jenkins iş akışı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8cbac-111">Create a Jenkins workflow</span></span>
- <span data-ttu-id="8cbac-112">CI/CD işlemi uçtan uca test edin</span><span class="sxs-lookup"><span data-stu-id="8cbac-112">Test the CI/CD process end to end</span></span>

## <a name="install-a-kubernetes-cluster"></a><span data-ttu-id="8cbac-113">Kubernetes küme yükleyin</span><span class="sxs-lookup"><span data-stu-id="8cbac-113">Install a Kubernetes cluster</span></span>
    
<span data-ttu-id="8cbac-114">Aşağıdaki adımları kullanarak Azure kapsayıcı hizmeti Kubernetes kümede dağıtın.</span><span class="sxs-lookup"><span data-stu-id="8cbac-114">Deploy the Kubernetes cluster in Azure Container Service using the following steps.</span></span> <span data-ttu-id="8cbac-115">Tam belgelerine bulunduğu [burada](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="8cbac-115">Full documentation is located [here](container-service-kubernetes-walkthrough.md).</span></span>

### <a name="step-1-create-a-resource-group"></a><span data-ttu-id="8cbac-116">1. adım: bir kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="8cbac-116">Step 1: Create a resource group</span></span>
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-the-cluster"></a><span data-ttu-id="8cbac-117">Adım 2: küme dağıtma</span><span class="sxs-lookup"><span data-stu-id="8cbac-117">Step 2: Deploy the cluster</span></span>
> [!NOTE]
> <span data-ttu-id="8cbac-118">Aşağıdaki adımları ~/.ssh klasöründe bulunan yerel bir SSH ortak anahtarı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8cbac-118">The following steps require a local SSH public key stored in the ~/.ssh folder.</span></span>
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

## <a name="set-up-jenkins-and-configure-access-to-container-service"></a><span data-ttu-id="8cbac-119">Jenkins ayarlayın ve kapsayıcı hizmeti erişimi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8cbac-119">Set up Jenkins and configure access to Container Service</span></span>

### <a name="step-1-install-jenkins"></a><span data-ttu-id="8cbac-120">1. adım: Jenkins yükleme</span><span class="sxs-lookup"><span data-stu-id="8cbac-120">Step 1: Install Jenkins</span></span>
1. <span data-ttu-id="8cbac-121">Ubuntu 16.04 ile bir Azure VM oluşturma LTS.</span><span class="sxs-lookup"><span data-stu-id="8cbac-121">Create an Azure VM with Ubuntu 16.04 LTS.</span></span>  <span data-ttu-id="8cbac-122">Sonraki adımlarda yerel makinenizde bash kullanarak bu VM bağlanmak gerekli olduğundan, 'kimlik doğrulama türü' 'SSH ortak anahtarını' olarak ayarlayın ve ~/.ssh klasörünüzde yerel olarak depolanan SSH ortak anahtarını yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="8cbac-122">Since later in the steps you will need to connect to this VM using bash on your local machine, set the 'Authentication type' to 'SSH public key' and paste the SSH public key that is stored locally in your ~/.ssh folder.</span></span>  <span data-ttu-id="8cbac-123">Ayrıca, 'kullanıcı adı' not alın bu kullanıcı adı Jenkins panoyu görüntülemek için gerekli olduğundan, belirttiğiniz ve daha sonraki adımlarda Jenkins VM bağlanmak için.</span><span class="sxs-lookup"><span data-stu-id="8cbac-123">Also, take note of the 'User name' that you specify since this user name will be needed to view the Jenkins dashboard and for connecting to the Jenkins VM in later steps.</span></span>
2. <span data-ttu-id="8cbac-124">Jenkins yüklemeniz [yönergeleri](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span><span class="sxs-lookup"><span data-stu-id="8cbac-124">Install Jenkins via these [instructions](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span></span> <span data-ttu-id="8cbac-125">Daha ayrıntılı bir öğretici altındadır [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span><span class="sxs-lookup"><span data-stu-id="8cbac-125">A more detailed tutorial is at [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span></span>
3. <span data-ttu-id="8cbac-126">Yerel makinenizde Jenkins panoyu görüntülemek için bağlantı noktası 8080 bağlantı noktası 8080 erişimi veren bir gelen kuralı ekleyerek izin vermek için Azure ağ güvenlik grubu güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="8cbac-126">To view the Jenkins dashboard on your local machine, update the Azure network security group to allow port 8080 by adding an inbound rule that allows access to port 8080.</span></span>  <span data-ttu-id="8cbac-127">Alternatif olarak, şu komutu çalıştırarak bağlantı noktası iletme Kurulum:`ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span><span class="sxs-lookup"><span data-stu-id="8cbac-127">Alternatively, you may setup port forwarding by running this command: `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span></span>
4. <span data-ttu-id="8cbac-128">Genel IP giderek tarayıcı kullanarak Jenkins sunucunuza bağlanmak (http:// < your_jenkins_public_ip >: 8080) ve ilk yönetici parolası ile ilk kez Jenkins Pano kilidini açın.</span><span class="sxs-lookup"><span data-stu-id="8cbac-128">Connect to your Jenkins server using the browser by navigating to the public IP (http://<your_jenkins_public_ip>:8080) and unlock the Jenkins dashboard for the first time with the initial admin password.</span></span>  <span data-ttu-id="8cbac-129">Yönetici parolası Jenkins VM üzerinde /var/lib/jenkins/secrets/initialAdminPassword konumunda depolanır.</span><span class="sxs-lookup"><span data-stu-id="8cbac-129">The admin password is stored at /var/lib/jenkins/secrets/initialAdminPassword on the Jenkins VM.</span></span>  <span data-ttu-id="8cbac-130">Jenkins VM içine SSH için bu parolayı almak için kolay bir yoludur.: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span><span class="sxs-lookup"><span data-stu-id="8cbac-130">An easy way to get this password is to SSH into the Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="8cbac-131">Ardından, çalıştırın: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span><span class="sxs-lookup"><span data-stu-id="8cbac-131">Next, run: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span></span>
5. <span data-ttu-id="8cbac-132">Docker bu Jenkins makinesine yükleyin [yönergeleri](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span><span class="sxs-lookup"><span data-stu-id="8cbac-132">Install Docker on the Jenkins machine via these [instructions](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span></span> <span data-ttu-id="8cbac-133">Bu Jenkins işleri çalıştırılacak Docker komut sağlar.</span><span class="sxs-lookup"><span data-stu-id="8cbac-133">This allows for Docker commands to be run in Jenkins jobs.</span></span>
6. <span data-ttu-id="8cbac-134">Docker uç noktasına erişmek Jenkins izin vermek için Docker izinlerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8cbac-134">Configure Docker permissions to allow Jenkins to access the Docker endpoint.</span></span>

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. <span data-ttu-id="8cbac-135">Yükleme `kubectl` CLI Jenkins üzerinde.</span><span class="sxs-lookup"><span data-stu-id="8cbac-135">Install `kubectl` CLI on Jenkins.</span></span> <span data-ttu-id="8cbac-136">Daha fazla ayrıntı altındadır [yükleme ve kubectl ayarlama](https://kubernetes.io/docs/tasks/kubectl/install/).</span><span class="sxs-lookup"><span data-stu-id="8cbac-136">More details are at [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>  <span data-ttu-id="8cbac-137">Jenkins işleri 'kubectl' Kubernetes kümesine dağıtmak ve yönetmek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="8cbac-137">Jenkins jobs will use 'kubectl' to manage and deploy to the Kubernetes cluster.</span></span>

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-to-the-kubernetes-cluster"></a><span data-ttu-id="8cbac-138">2. adım: Kubernetes kümesine erişimi ayarlama</span><span class="sxs-lookup"><span data-stu-id="8cbac-138">Step 2: Set up access to the Kubernetes cluster</span></span>

> [!NOTE]
> <span data-ttu-id="8cbac-139">Aşağıdaki adımlar işlemi gerçekleştirmek için birden çok yaklaşım vardır.</span><span class="sxs-lookup"><span data-stu-id="8cbac-139">There are multiple approaches to accomplishing the following steps.</span></span> <span data-ttu-id="8cbac-140">Sizin için en kolay yaklaşım kullanın.</span><span class="sxs-lookup"><span data-stu-id="8cbac-140">Use the approach that is easiest for you.</span></span>
>

1. <span data-ttu-id="8cbac-141">Kopya `kubectl` yapılandırma dosyası Jenkins makineye böylece Jenkins işleri Kubernetes kümesine erişimi.</span><span class="sxs-lookup"><span data-stu-id="8cbac-141">Copy the `kubectl` config file to the Jenkins machine so that Jenkins jobs have access to the Kubernetes cluster.</span></span> <span data-ttu-id="8cbac-142">Bu yönergeler, kullandığınız varsayılır bash Jenkins VM daha farklı bir makineden ve yerel bir SSH ortak anahtarı makinenin ~/.ssh klasöründe depolanır.</span><span class="sxs-lookup"><span data-stu-id="8cbac-142">These instructions assume that you are using bash from a different machine than the Jenkins VM and that a local SSH public key is stored in the machine's ~/.ssh folder.</span></span>

```bash
export KUBE_MASTER=<your_cluster_master_fqdn>
export JENKINS_USER=<your_jenkins_user>
export JENKINS_SERVER=<your_jenkins_public_ip>
sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir -m 777 /home/$JENKINS_USER/.kube/ \
&& sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir /var/lib/jenkins/.kube/ \
&& sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config $JENKINS_USER@$JENKINS_SERVER:~/.kube/config \
&& sudo ssh -i ~/.ssh/id_rsa $JENKINS_USER@$JENKINS_SERVER sudo cp /home/$JENKINS_USER/.kube/config /var/lib/jenkins/.kube/config \
```
        
2. <span data-ttu-id="8cbac-143">Jenkins Kubernetes küme erişilebilir olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="8cbac-143">Validate from Jenkins that the Kubernetes cluster is accessible.</span></span>  <span data-ttu-id="8cbac-144">Bu, SSH Jenkins VM'de oturum yapmak için: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span><span class="sxs-lookup"><span data-stu-id="8cbac-144">To do this, SSH into the Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="8cbac-145">Ardından, Jenkins başarıyla kümenize bağlanmak doğrulayın: `kubectl cluster-info`.</span><span class="sxs-lookup"><span data-stu-id="8cbac-145">Next, verify Jenkins can successfully connect to your cluster: `kubectl cluster-info`.</span></span>
    

## <a name="create-a-jenkins-workflow"></a><span data-ttu-id="8cbac-146">Jenkins iş akışı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8cbac-146">Create a Jenkins workflow</span></span>

### <a name="prerequisites"></a><span data-ttu-id="8cbac-147">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8cbac-147">Prerequisites</span></span>

- <span data-ttu-id="8cbac-148">Kod deposu için GitHub hesabı.</span><span class="sxs-lookup"><span data-stu-id="8cbac-148">GitHub account for code repo.</span></span>
- <span data-ttu-id="8cbac-149">Depolamak ve görüntülerini güncelleştirmek için docker hub'a hesabı.</span><span class="sxs-lookup"><span data-stu-id="8cbac-149">Docker Hub account to store and update images.</span></span>
- <span data-ttu-id="8cbac-150">Yeniden ve güncelleştirilmiş kapsayıcılı uygulama.</span><span class="sxs-lookup"><span data-stu-id="8cbac-150">Containerized application that can be rebuilt and updated.</span></span> <span data-ttu-id="8cbac-151">Bu örnek kapsayıcı uygulaması Golang içinde yazılmış kullanabilirsiniz: https://github.com/chzbrgr71/go-web</span><span class="sxs-lookup"><span data-stu-id="8cbac-151">You can use this sample container app written in Golang: https://github.com/chzbrgr71/go-web</span></span> 

> [!NOTE]
> <span data-ttu-id="8cbac-152">Kendi GitHub hesabı aşağıdaki adımlar gerçekleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="8cbac-152">The following steps must be performed in your own GitHub account.</span></span> <span data-ttu-id="8cbac-153">Yukarıdaki depoyu kopyalama çekinmeyin ancak Jenkins erişmek ve Web kancalarını yapılandırmak için kendi hesabı kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8cbac-153">Feel free to clone the above repo, but you must use your own account to configure the webhooks and Jenkins access.</span></span>
>

### <a name="step-1-deploy-initial-v1-of-application"></a><span data-ttu-id="8cbac-154">1. adım: uygulamanın ilk v1 dağıtma</span><span class="sxs-lookup"><span data-stu-id="8cbac-154">Step 1: Deploy initial v1 of application</span></span>
1. <span data-ttu-id="8cbac-155">Aşağıdaki komutlarla Geliştirici makineden uygulaması oluşturma.</span><span class="sxs-lookup"><span data-stu-id="8cbac-155">Build the app from the developer machine with the following commands.</span></span> <span data-ttu-id="8cbac-156">Değiştir `myrepo` kendi değerlerinizle.</span><span class="sxs-lookup"><span data-stu-id="8cbac-156">Replace `myrepo` with your own.</span></span>
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. <span data-ttu-id="8cbac-157">Görüntü Docker hub'a iletin.</span><span class="sxs-lookup"><span data-stu-id="8cbac-157">Push image to Docker Hub.</span></span>

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. <span data-ttu-id="8cbac-158">Kubernetes kümeye dağıtın.</span><span class="sxs-lookup"><span data-stu-id="8cbac-158">Deploy to the Kubernetes cluster.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="8cbac-159">Düzen `go-web.yaml` kapsayıcı görüntü ve depo güncelleştirmek için dosya.</span><span class="sxs-lookup"><span data-stu-id="8cbac-159">Edit the `go-web.yaml` file to update your container image and repo.</span></span>
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a><span data-ttu-id="8cbac-160">2. adım: Jenkins sistem yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8cbac-160">Step 2: Configure Jenkins system</span></span>
1. <span data-ttu-id="8cbac-161">Tıklatın **Jenkins yönetmek** > **sistem yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="8cbac-161">Click **Manage Jenkins** > **Configure System**.</span></span>
2. <span data-ttu-id="8cbac-162">Altında **GitHub**seçin **GitHub Sunucu Ekle**.</span><span class="sxs-lookup"><span data-stu-id="8cbac-162">Under **GitHub**, select **Add GitHub Server**.</span></span>
3. <span data-ttu-id="8cbac-163">Bırakın **API URL** varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="8cbac-163">Leave **API URL** as default.</span></span>
4. <span data-ttu-id="8cbac-164">Altında **kimlik bilgileri**, Jenkins kimlik bilgilerini kullanarak eklemek **gizli metin**.</span><span class="sxs-lookup"><span data-stu-id="8cbac-164">Under **Credentials**, add a Jenkins credential using **Secret text**.</span></span> <span data-ttu-id="8cbac-165">GitHub kullanıcı hesap ayarlarınızda yapılandırılmış GitHub kişisel erişim belirteçleri kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="8cbac-165">We recommend using GitHub personal access tokens, which are configured in your GitHub user account settings.</span></span> <span data-ttu-id="8cbac-166">Bunun hakkında daha fazla ayrıntı [burada.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span><span class="sxs-lookup"><span data-stu-id="8cbac-166">More details on this [here.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span></span>
5. <span data-ttu-id="8cbac-167">Tıklatın **Bağlantıyı Sına** bunu doğru şekilde yapılandırılmış emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="8cbac-167">Click **Test connection** to ensure this is configured correctly.</span></span>
6. <span data-ttu-id="8cbac-168">Altında **genel özellikleri**, bir ortam değişkeni ekleyin `DOCKER_HUB` ve Docker hub'a parolanızı girin.</span><span class="sxs-lookup"><span data-stu-id="8cbac-168">Under **Global Properties**, add an environment variable `DOCKER_HUB` and provide your Docker Hub password.</span></span> <span data-ttu-id="8cbac-169">(Bu gösteride kullanışlıdır ancak bir üretim senaryosu daha güvenli bir yöntem gerektirir.)</span><span class="sxs-lookup"><span data-stu-id="8cbac-169">(This is useful in this demo, but a production scenario would require a more secure approach.)</span></span>
7. <span data-ttu-id="8cbac-170">Kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8cbac-170">Save.</span></span>

![Jenkins GitHub erişim](./media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-the-jenkins-workflow"></a><span data-ttu-id="8cbac-172">3. adım: Jenkins iş akışı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8cbac-172">Step 3: Create the Jenkins workflow</span></span>
1. <span data-ttu-id="8cbac-173">Jenkins öğesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8cbac-173">Create a Jenkins item.</span></span>
2. <span data-ttu-id="8cbac-174">Bir ad girin (örneğin, "Web'de Git") seçip **Freestyle proje**.</span><span class="sxs-lookup"><span data-stu-id="8cbac-174">Provide a name (for example, "go-web") and select **Freestyle Project**.</span></span> 
3. <span data-ttu-id="8cbac-175">Denetleme **GitHub proje** ve GitHub depo URL'si sağlayın.</span><span class="sxs-lookup"><span data-stu-id="8cbac-175">Check **GitHub project** and provide the URL to your GitHub repo.</span></span>
4. <span data-ttu-id="8cbac-176">İçinde **kaynak kodu Yönetimi**, GitHub deposuna URL ve kimlik bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="8cbac-176">In **Source Code Management**, provide the GitHub repo URL and credentials.</span></span> 
5. <span data-ttu-id="8cbac-177">Ekleme bir **derleme adımı** türü **Kabuk yürütme** ve aşağıdaki metni kullanın:</span><span class="sxs-lookup"><span data-stu-id="8cbac-177">Add a **Build Step** of type **Execute shell** and use the following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. <span data-ttu-id="8cbac-178">Başka bir tane eklemek **derleme adımı** türü **Kabuk yürütme** ve aşağıdaki metni kullanın:</span><span class="sxs-lookup"><span data-stu-id="8cbac-178">Add another **Build Step** of type **Execute shell** and use the following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Jenkins derleme adımları](./media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. <span data-ttu-id="8cbac-180">Jenkins öğeyi kaydetmek ve test **şimdi yapı**.</span><span class="sxs-lookup"><span data-stu-id="8cbac-180">Save the Jenkins item and test with **Build Now**.</span></span>

### <a name="step-4-connect-github-webhook"></a><span data-ttu-id="8cbac-181">4. adım: GitHub Web kancası bağlanma</span><span class="sxs-lookup"><span data-stu-id="8cbac-181">Step 4: Connect GitHub webhook</span></span>
1. <span data-ttu-id="8cbac-182">Oluşturduğunuz Jenkins öğeyi tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="8cbac-182">In the Jenkins item you created, click **Configure**.</span></span>
2. <span data-ttu-id="8cbac-183">Altında **yapı tetikleyicileri**seçin **GITScm yoklama için GitHub kanca tetikleyici** ve **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="8cbac-183">Under **Build Triggers**, select **GitHub hook trigger for GITScm polling** and **Save**.</span></span> <span data-ttu-id="8cbac-184">Bu, GitHub Web kancası otomatik olarak yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="8cbac-184">This automatically configures the GitHub webhook.</span></span>
3. <span data-ttu-id="8cbac-185">Web Git, GitHub deposuna içinde tıklatın **ayarlar > Web Kancalarını**.</span><span class="sxs-lookup"><span data-stu-id="8cbac-185">In your GitHub repo for go-web, click **Settings > Webhooks**.</span></span>
4. <span data-ttu-id="8cbac-186">Jenkins Web kancası URL'si başarıyla eklendiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="8cbac-186">Verify that the Jenkins webhook URL was added successfully.</span></span> <span data-ttu-id="8cbac-187">URL "github-Web kancası" bitmelidir.</span><span class="sxs-lookup"><span data-stu-id="8cbac-187">The URL should end in "github-webhook".</span></span>

![Jenkins Web kancası yapılandırma](./media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-the-cicd-process-end-to-end"></a><span data-ttu-id="8cbac-189">CI/CD işlemi uçtan uca test edin</span><span class="sxs-lookup"><span data-stu-id="8cbac-189">Test the CI/CD process end to end</span></span>

1. <span data-ttu-id="8cbac-190">Depodaki ve anında iletme/eşitlemesi için kod GitHub deposuyla güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="8cbac-190">Update code for the repo and push/synch with the GitHub repository.</span></span>
2. <span data-ttu-id="8cbac-191">Jenkins konsolundan denetleyin **yapı geçmiş** ve iş çalıştırıldığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="8cbac-191">From the Jenkins console, check the **Build History** and validate that the job has run.</span></span> <span data-ttu-id="8cbac-192">Ayrıntıları görmek için görünümü konsol çıkışı.</span><span class="sxs-lookup"><span data-stu-id="8cbac-192">View console output to see details.</span></span>
3. <span data-ttu-id="8cbac-193">Kubernetes yükseltilmiş dağıtım ayrıntılarını görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="8cbac-193">From Kubernetes, view details of the upgraded deployment:</span></span>

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a><span data-ttu-id="8cbac-194">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8cbac-194">Next steps</span></span>

- <span data-ttu-id="8cbac-195">Azure kapsayıcı kayıt defteri dağıtın ve güvenli bir depoda görüntüleri saklamak.</span><span class="sxs-lookup"><span data-stu-id="8cbac-195">Deploy Azure Container Registry and store images in a secure repository.</span></span> <span data-ttu-id="8cbac-196">Bkz: [Azure kapsayıcı kayıt defteri belgeleri](https://docs.microsoft.com/azure/container-registry).</span><span class="sxs-lookup"><span data-stu-id="8cbac-196">See [Azure Container Registry docs](https://docs.microsoft.com/azure/container-registry).</span></span>
- <span data-ttu-id="8cbac-197">Yan yana dağıtım ve otomatikleştirilmiş testleri Jenkins içeren daha karmaşık bir iş akışı oluşturma.</span><span class="sxs-lookup"><span data-stu-id="8cbac-197">Build a more complex workflow that includes side-by-side deployment and automated tests in Jenkins.</span></span>
- <span data-ttu-id="8cbac-198">CI/CD Jenkins ve Kubernetes hakkında daha fazla bilgi için bkz: [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span><span class="sxs-lookup"><span data-stu-id="8cbac-198">For more information about CI/CD with Jenkins and Kubernetes, see the [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span></span>
