---
title: "Jenkins ile azure'da geliştirme işlem hattı oluşturma | Microsoft Docs"
description: "Her kod tamamlama Github'dan çeker ve uygulamanızı çalıştırmak için yeni bir Docker kapsayıcısı derlemeler Azure'da Jenkins sanal makine oluşturma hakkında bilgi edinin"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: d9849b5e061dd7f2ae0744a3522dc2eb1fb37035
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-create-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a><span data-ttu-id="912f0-103">Jenkins, GitHub ve Docker ile azure'da bir Linux VM üzerinde bir geliştirme altyapısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="912f0-103">How to create a development infrastructure on a Linux VM in Azure with Jenkins, GitHub, and Docker</span></span>
<span data-ttu-id="912f0-104">Uygulama geliştirme, derleme ve test aşaması otomatikleştirmek için sürekli tümleştirme ve dağıtım (CI/CD) ardışık düzen kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="912f0-104">To automate the build and test phase of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="912f0-105">Bu öğreticide, Azure VM temelinde CI/CD işlem hattı oluşturmak için nasıl dahil:</span><span class="sxs-lookup"><span data-stu-id="912f0-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="912f0-106">Jenkins VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="912f0-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="912f0-107">Yükleme ve Jenkins yapılandırma</span><span class="sxs-lookup"><span data-stu-id="912f0-107">Install and configure Jenkins</span></span>
> * <span data-ttu-id="912f0-108">GitHub ile Jenkins arasında Web kancası tümleştirme oluşturma</span><span class="sxs-lookup"><span data-stu-id="912f0-108">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="912f0-109">Oluşturma ve GitHub yürütme Jenkins yapı işlerden tetikler</span><span class="sxs-lookup"><span data-stu-id="912f0-109">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="912f0-110">Uygulamanız için Docker görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="912f0-110">Create a Docker image for your app</span></span>
> * <span data-ttu-id="912f0-111">Yeni Docker görüntü ve uygulamayı çalıştıran güncelleştirmeleri GitHub yürütme yapı doğrulayın</span><span class="sxs-lookup"><span data-stu-id="912f0-111">Verify GitHub commits build new Docker image and updates running app</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="912f0-112">Yüklemek ve CLI yerel olarak kullanmak seçerseniz, Bu öğretici, Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="912f0-112">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="912f0-113">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="912f0-113">Run `az --version` to find the version.</span></span> <span data-ttu-id="912f0-114">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="912f0-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-jenkins-instance"></a><span data-ttu-id="912f0-115">Jenkins örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="912f0-115">Create Jenkins instance</span></span>
<span data-ttu-id="912f0-116">Önceki bir öğretici içinde [Linux sanal bir makinede ilk önyükleme özelleştirmek nasıl](tutorial-automate-vm-deployment.md), bulut init VM özelleştirmesiyle otomatikleştirmek öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="912f0-116">In a previous tutorial on [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how to automate VM customization with cloud-init.</span></span> <span data-ttu-id="912f0-117">Bu öğretici bir bulut init dosya Jenkins ve Docker bir VM yüklemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="912f0-117">This tutorial uses a cloud-init file to install Jenkins and Docker on a VM.</span></span> 

<span data-ttu-id="912f0-118">Geçerli kabuğunuzu adlı bir dosya oluşturun *bulut init.txt* ve aşağıdaki yapılandırma yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="912f0-118">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="912f0-119">Örneğin, yerel makinenizde olmayan bulut kabuğunda dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="912f0-119">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="912f0-120">Girin `sensible-editor cloud-init-jenkins.txt` dosyası oluşturun ve kullanılabilir düzenleyicileri listesini görmek için.</span><span class="sxs-lookup"><span data-stu-id="912f0-120">Enter `sensible-editor cloud-init-jenkins.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="912f0-121">Tüm bulut init dosyanın doğru şekilde kopyalandığından emin olun özellikle ilk satırı:</span><span class="sxs-lookup"><span data-stu-id="912f0-121">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
write_files:
  - path: /etc/systemd/system/docker.service.d/docker.conf
    content: |
      [Service]
        ExecStart=
        ExecStart=/usr/bin/dockerd
  - path: /etc/docker/daemon.json
    content: |
      {
        "hosts": ["fd://","tcp://127.0.0.1:2375"]
      }
runcmd:
  - wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -
  - sh -c 'echo deb http://pkg.jenkins-ci.org/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
  - apt-get update && apt-get install jenkins -y
  - curl -sSL https://get.docker.com/ | sh
  - usermod -aG docker azureuser
  - usermod -aG docker jenkins
  - service jenkins restart
```

<span data-ttu-id="912f0-122">Bir VM oluşturmadan önce bir kaynak grubuyla oluşturmanız [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="912f0-122">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="912f0-123">Aşağıdaki örnek, bir kaynak grubu oluşturur *myResourceGroupJenkins* içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="912f0-123">The following example creates a resource group named *myResourceGroupJenkins* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

<span data-ttu-id="912f0-124">Şimdi bir VM oluşturmak [az vm oluşturma](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="912f0-124">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="912f0-125">Kullanım `--custom-data` bulut init yapılandırma dosyanızda geçirmek için parametre.</span><span class="sxs-lookup"><span data-stu-id="912f0-125">Use the `--custom-data` parameter to pass in your cloud-init config file.</span></span> <span data-ttu-id="912f0-126">Tam yolunu belirtmeniz *bulut init jenkins.txt* mevcut çalışma dizininizi dışında dosyasını kaydettiyseniz.</span><span class="sxs-lookup"><span data-stu-id="912f0-126">Provide the full path to *cloud-init-jenkins.txt* if you saved the file outside of your present working directory.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

<span data-ttu-id="912f0-127">Oluşturulan ve yapılandırılacak VM için birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="912f0-127">It takes a few minutes for the VM to be created and configured.</span></span>

<span data-ttu-id="912f0-128">VM ulaşmak web trafiğine izin vermek için kullanın [az vm Aç-port](/cli/azure/vm#open-port) bağlantı noktasını açmak için *8080* Jenkins trafiği ve bağlantı noktası için *1337* bir örnek uygulamayı çalıştırmak için kullanılan Node.js uygulaması için:</span><span class="sxs-lookup"><span data-stu-id="912f0-128">To allow web traffic to reach your VM, use [az vm open-port](/cli/azure/vm#open-port) to open port *8080* for Jenkins traffic and port *1337* for the Node.js app that is used to run a sample app:</span></span>

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a><span data-ttu-id="912f0-129">Jenkins yapılandırın</span><span class="sxs-lookup"><span data-stu-id="912f0-129">Configure Jenkins</span></span>
<span data-ttu-id="912f0-130">Jenkins örneğinizi erişmek için VM genel IP adresi alın:</span><span class="sxs-lookup"><span data-stu-id="912f0-130">To access your Jenkins instance, obtain the public IP address of your VM:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="912f0-131">Güvenlik nedeniyle, Jenkins yüklemeyi başlatmak için VM üzerindeki bir metin dosyasında depolanan ilk yönetici parolasını girmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="912f0-131">For security purposes, you need to enter the initial admin password that is stored in a text file on your VM to start the Jenkins install.</span></span> <span data-ttu-id="912f0-132">SSH, VM için önceki adımda elde edilen ortak IP adresi kullanın:</span><span class="sxs-lookup"><span data-stu-id="912f0-132">Use the public IP address obtained in the previous step to SSH to your VM:</span></span>

```bash
ssh azureuser@<publicIps>
```

<span data-ttu-id="912f0-133">Görünüm `initialAdminPassword` , Jenkins yükleyin ve onu kopyalamak için:</span><span class="sxs-lookup"><span data-stu-id="912f0-133">View the `initialAdminPassword` for your Jenkins install and copy it:</span></span>

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

<span data-ttu-id="912f0-134">Dosya henüz kullanılabilir durumda değilse, Jenkins ve Docker yüklemeyi tamamlamak bulut başlatma birkaç dakika daha bekleyin.</span><span class="sxs-lookup"><span data-stu-id="912f0-134">If the file isn't available yet, wait a couple more minutes for cloud-init to complete the Jenkins and Docker install.</span></span>

<span data-ttu-id="912f0-135">Şimdi bir web tarayıcısı açın ve gidin `http://<publicIps>:8080`.</span><span class="sxs-lookup"><span data-stu-id="912f0-135">Now open a web browser and go to `http://<publicIps>:8080`.</span></span> <span data-ttu-id="912f0-136">İlk Jenkins Kurulum aşağıdaki gibi tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="912f0-136">Complete the initial Jenkins setup as follows:</span></span>

- <span data-ttu-id="912f0-137">Girin *initialAdminPassword* VM önceki adımda elde.</span><span class="sxs-lookup"><span data-stu-id="912f0-137">Enter the *initialAdminPassword* obtained from the VM in the previous step.</span></span>
- <span data-ttu-id="912f0-138">Tıklatın **yüklemek için eklentileri seçin**</span><span class="sxs-lookup"><span data-stu-id="912f0-138">Click **Select plugins to install**</span></span>
- <span data-ttu-id="912f0-139">Arama *GitHub* üstte metin kutusunda seçin *GitHub eklentisi*, ardından **yükleyin**</span><span class="sxs-lookup"><span data-stu-id="912f0-139">Search for *GitHub* in the text box across the top, select the *GitHub plugin*, then click **Install**</span></span>
- <span data-ttu-id="912f0-140">Jenkins kullanıcı hesabı oluşturmak için istediğiniz gibi formu doldurun.</span><span class="sxs-lookup"><span data-stu-id="912f0-140">To create a Jenkins user account, fill out the form as desired.</span></span> <span data-ttu-id="912f0-141">Güvenlik açısından bakıldığında, varsayılan yönetici hesabıyla etmeden yerine bu ilk Jenkins kullanıcı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="912f0-141">From a security perspective, you should create this first Jenkins user rather than continuing as the default admin account.</span></span>
- <span data-ttu-id="912f0-142">Tamamlandığında tıklatarak **Jenkins kullanmaya başlama**</span><span class="sxs-lookup"><span data-stu-id="912f0-142">When finished, click **Start using Jenkins**</span></span>


## <a name="create-github-webhook"></a><span data-ttu-id="912f0-143">GitHub Web kancası oluşturma</span><span class="sxs-lookup"><span data-stu-id="912f0-143">Create GitHub webhook</span></span>
<span data-ttu-id="912f0-144">GitHub ile tümleştirme yapılandırmak için açın [Node.js Hello World örnek uygulaması](https://github.com/Azure-Samples/nodejs-docs-hello-world) Azure örneklerinden depoyu gelen.</span><span class="sxs-lookup"><span data-stu-id="912f0-144">To configure the integration with GitHub, open the [Node.js Hello World sample app](https://github.com/Azure-Samples/nodejs-docs-hello-world) from the Azure samples repo.</span></span> <span data-ttu-id="912f0-145">Kendi GitHub hesabınızda depoyu çatallaştırma için tıklatın **çatalı** sağ üst köşesindeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="912f0-145">To fork the repo to your own GitHub account, click the **Fork** button in the top right-hand corner.</span></span>

<span data-ttu-id="912f0-146">Oluşturduğunuz çatalı içinde bir Web kancası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="912f0-146">Create a webhook inside the fork you created:</span></span>

- <span data-ttu-id="912f0-147">Tıklatın **ayarları**seçeneğini belirleyip **tümleştirmeler & Hizmetleri** sol taraftaki.</span><span class="sxs-lookup"><span data-stu-id="912f0-147">Click **Settings**, then select **Integrations & services** on the left-hand side.</span></span>
- <span data-ttu-id="912f0-148">Tıklatın **Hizmet Ekle**, enter *Jenkins* filtre kutusuna.</span><span class="sxs-lookup"><span data-stu-id="912f0-148">Click **Add service**, then enter *Jenkins* in filter box.</span></span>
- <span data-ttu-id="912f0-149">Seçin *Jenkins (GitHub eklentisi)*</span><span class="sxs-lookup"><span data-stu-id="912f0-149">Select *Jenkins (GitHub plugin)*</span></span>
- <span data-ttu-id="912f0-150">İçin **Jenkins kanca URL**, girin `http://<publicIps>:8080/github-webhook/`.</span><span class="sxs-lookup"><span data-stu-id="912f0-150">For the **Jenkins hook URL**, enter `http://<publicIps>:8080/github-webhook/`.</span></span> <span data-ttu-id="912f0-151">Sondaki eklediğinizden emin olun /</span><span class="sxs-lookup"><span data-stu-id="912f0-151">Make sure you include the trailing /</span></span>
- <span data-ttu-id="912f0-152">Tıklatın **Hizmet Ekle**</span><span class="sxs-lookup"><span data-stu-id="912f0-152">Click **Add service**</span></span>

![GitHub Web kancası, forked deposuna ekleme](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a><span data-ttu-id="912f0-154">Jenkins işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="912f0-154">Create Jenkins job</span></span>
<span data-ttu-id="912f0-155">Bir olay Jenkins yanıt kodu yürütme gibi Github'da sağlamak için Jenkins işi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="912f0-155">To have Jenkins respond to an event in GitHub such as committing code, create a Jenkins job.</span></span> 

<span data-ttu-id="912f0-156">Jenkins siteniz tıklatın **yeni işleri oluşturmak** giriş sayfasından:</span><span class="sxs-lookup"><span data-stu-id="912f0-156">In your Jenkins website, click **Create new jobs** from the home page:</span></span>

- <span data-ttu-id="912f0-157">Girin *HelloWorld* iş adı olarak.</span><span class="sxs-lookup"><span data-stu-id="912f0-157">Enter *HelloWorld* as job name.</span></span> <span data-ttu-id="912f0-158">Seçin **Serbest stilde proje**seçeneğini belirleyip **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="912f0-158">Choose **Freestyle project**, then select **OK**.</span></span>
- <span data-ttu-id="912f0-159">Altında **genel** bölümünde, select **GitHub** proje ve çatallanmış depodaki URL'nizi girin *https://github.com/iainfoulds/nodejs-docs-hello-world*</span><span class="sxs-lookup"><span data-stu-id="912f0-159">Under the **General** section, select **GitHub** project and enter your forked repo URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world*</span></span>
- <span data-ttu-id="912f0-160">Altında **kaynak kodu Yönetimi** bölümünde, select **Git**, forked depodaki girin *.git* URL gibi *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span><span class="sxs-lookup"><span data-stu-id="912f0-160">Under the **Source code management** section, select **Git**, enter your forked repo *.git* URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span></span>
- <span data-ttu-id="912f0-161">Altında **yapı tetikleyicileri** bölümünde, select **GITscm yoklama için GitHub kanca tetikleyici**.</span><span class="sxs-lookup"><span data-stu-id="912f0-161">Under the **Build Triggers** section, select **GitHub hook trigger for GITscm polling**.</span></span>
- <span data-ttu-id="912f0-162">Altında **yapı** bölümünde, seçin **Ekle derleme adımı**.</span><span class="sxs-lookup"><span data-stu-id="912f0-162">Under the **Build** section, choose **Add build step**.</span></span> <span data-ttu-id="912f0-163">Seçin **Kabuk yürütme**, enter `echo "Testing"` içinde komut penceresine.</span><span class="sxs-lookup"><span data-stu-id="912f0-163">Select **Execute shell**, then enter `echo "Testing"` in to command window.</span></span>
- <span data-ttu-id="912f0-164">Tıklatın **kaydetmek** işleri pencerenin altındaki.</span><span class="sxs-lookup"><span data-stu-id="912f0-164">Click **Save** at the bottom of the jobs window.</span></span>


## <a name="test-github-integration"></a><span data-ttu-id="912f0-165">Test GitHub tümleştirme</span><span class="sxs-lookup"><span data-stu-id="912f0-165">Test GitHub integration</span></span>
<span data-ttu-id="912f0-166">Jenkins GitHub tümleşme test etmek için bir değişiklik, çatalı uygulayın.</span><span class="sxs-lookup"><span data-stu-id="912f0-166">To test the GitHub integration with Jenkins, commit a change in your fork.</span></span> 

<span data-ttu-id="912f0-167">Geri Github'da web kullanıcı Arabirimi, forked depoyu seçin ve ardından **index.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="912f0-167">Back in GitHub web UI, select your forked repo, and then click the **index.js** file.</span></span> <span data-ttu-id="912f0-168">Satır 6 okunacak şekilde bu dosyayı düzenlemek için Kalem simgesine tıklayın:</span><span class="sxs-lookup"><span data-stu-id="912f0-168">Click the pencil icon to edit this file so line 6 reads:</span></span>

```nodejs
response.end("Hello World!");
```

<span data-ttu-id="912f0-169">Değişikliklerinizi kaydetmek için tıklatın **değişiklikleri** altındaki düğmesini.</span><span class="sxs-lookup"><span data-stu-id="912f0-169">To commit your changes, click the **Commit changes** button at the bottom.</span></span>

<span data-ttu-id="912f0-170">Jenkins içinde altında yeni bir yapı başlatır **yapı geçmiş** iş sayfanızı sol alt köşesindeki bölümü.</span><span class="sxs-lookup"><span data-stu-id="912f0-170">In Jenkins, a new build starts under the **Build history** section of the bottom left-hand corner of your job page.</span></span> <span data-ttu-id="912f0-171">Yapı numarası bağlantısına tıklayın ve **konsol çıkış** sol boyutu.</span><span class="sxs-lookup"><span data-stu-id="912f0-171">Click the build number link and select **Console output** on the left-hand size.</span></span> <span data-ttu-id="912f0-172">Jenkins alan, kodunuzun Github'dan çekildiğinde adımları görüntüleyebilir ve yapı eylemi ileti çıkaran `Testing` Konsolu'na.</span><span class="sxs-lookup"><span data-stu-id="912f0-172">You can view the steps Jenkins takes as your code is pulled from GitHub and the build action outputs the message `Testing` to the console.</span></span> <span data-ttu-id="912f0-173">Github'da, her bir işleme yapıldığında Web kancası için Jenkins ulaştığında ve bu şekilde yeni bir derlemeyi tetiklemeyi.</span><span class="sxs-lookup"><span data-stu-id="912f0-173">Each time a commit is made in GitHub, the webhook reaches out to Jenkins and trigger a new build in this way.</span></span>


## <a name="define-docker-build-image"></a><span data-ttu-id="912f0-174">Docker derleme görüntüyü tanımlayın</span><span class="sxs-lookup"><span data-stu-id="912f0-174">Define Docker build image</span></span>
<span data-ttu-id="912f0-175">GitHub yürütme üzerinde göre çalışan Node.js uygulaması görmenizi sağlar uygulamayı çalıştırmak için Docker görüntüsünü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="912f0-175">To see the Node.js app running based on your GitHub commits, lets build a Docker image to run the app.</span></span> <span data-ttu-id="912f0-176">Görüntü uygulamanın çalıştığı kapsayıcı yapılandırma tanımlayan bir Dockerfile yerleşik olarak bulunur.</span><span class="sxs-lookup"><span data-stu-id="912f0-176">The image is built from a Dockerfile that defines how to configure the container that runs the app.</span></span> 

<span data-ttu-id="912f0-177">Bir önceki adımda oluşturduğunuz iş sonra adlı Jenkins çalışma dizini için VM SSH bağlantısı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="912f0-177">From the SSH connection to your VM, change to the Jenkins workspace directory named after the job you created in a previous step.</span></span> <span data-ttu-id="912f0-178">Bizim örneğimizde, adlandırılması *HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="912f0-178">In our example, that was named *HelloWorld*.</span></span>

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

<span data-ttu-id="912f0-179">Bu çalışma alanı dizindeki bir dosya oluşturmak `sudo sensible-editor Dockerfile` ve aşağıdaki içeriğini yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="912f0-179">Create a file with in this workspace directory with `sudo sensible-editor Dockerfile` and paste the following contents.</span></span> <span data-ttu-id="912f0-180">Tüm Dockerfile doğru şekilde kopyalandığından emin olun özellikle ilk satırı:</span><span class="sxs-lookup"><span data-stu-id="912f0-180">Make sure that the whole Dockerfile is copied correctly, especially the first line:</span></span>

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

<span data-ttu-id="912f0-181">Alpine Linux kullanarak temel Node.js görüntü, Hello World uygulama çalıştıran çıkarır bağlantı noktası 1337 sonra uygulama dosyalarını kopyalar ve onu başlatır bu Dockerfile kullanır.</span><span class="sxs-lookup"><span data-stu-id="912f0-181">This Dockerfile uses the base Node.js image using Alpine Linux, exposes port 1337 that the Hello World app runs on, then copies the app files and initializes it.</span></span>


## <a name="create-jenkins-build-rules"></a><span data-ttu-id="912f0-182">Jenkins derleme kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="912f0-182">Create Jenkins build rules</span></span>
<span data-ttu-id="912f0-183">Önceki adımda, bir ileti konsola çıktı temel bir Jenkins yapı kuralı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="912f0-183">In a previous step, you created a basic Jenkins build rule that output a message to the console.</span></span> <span data-ttu-id="912f0-184">Bizim Dockerfile kullanın ve uygulamayı çalıştırmak için derleme adımı oluşturmak olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="912f0-184">Lets create the build step to use our Dockerfile and run the app.</span></span>

<span data-ttu-id="912f0-185">Geri Jenkins örneğinizi içinde bir önceki adımda oluşturduğunuz işi seçin.</span><span class="sxs-lookup"><span data-stu-id="912f0-185">Back in your Jenkins instance, select the job you created in a previous step.</span></span> <span data-ttu-id="912f0-186">Tıklatın **yapılandırma** aşağı kaydırın ve sol taraftaki **yapı** bölümü:</span><span class="sxs-lookup"><span data-stu-id="912f0-186">Click **Configure** on the left-hand side and scroll down to the **Build** section:</span></span>

- <span data-ttu-id="912f0-187">Var olan kaldırmak `echo "Test"` adım oluşturma.</span><span class="sxs-lookup"><span data-stu-id="912f0-187">Remove your existing `echo "Test"` build step.</span></span> <span data-ttu-id="912f0-188">Varolan derleme adımı kutusu sağ üst köşesinde bulunan kırmızı çarpı'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="912f0-188">Click the red cross on the top right-hand corner of the existing build step box.</span></span>
- <span data-ttu-id="912f0-189">Tıklatın **Ekle derleme adımı**seçeneğini belirleyip **Kabuk yürütme**</span><span class="sxs-lookup"><span data-stu-id="912f0-189">Click **Add build step**, then select **Execute shell**</span></span>
- <span data-ttu-id="912f0-190">İçinde **komutu** kutusunda, aşağıdaki Docker komutları girin, ardından seçin **kaydetmek**:</span><span class="sxs-lookup"><span data-stu-id="912f0-190">In the **Command** box, enter the following Docker commands, then select **Save**:</span></span>

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

<span data-ttu-id="912f0-191">Docker derleme adımları imaj ve Jenkins ile yapı numarası görüntüleri bir geçmişini sağlamak için etiketi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="912f0-191">The Docker build steps create an image and tag it with the Jenkins build number so you can maintain a history of images.</span></span> <span data-ttu-id="912f0-192">Uygulamayı çalıştıran herhangi bir varolan kapsayıcıdaki durdurulur ve sonra kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="912f0-192">Any existing containers running the app are stopped and then removed.</span></span> <span data-ttu-id="912f0-193">Yeni bir kapsayıcı görüntüsünü kullanarak başlatılır ve Node.js uygulamanızı github'da son işlemeleri göre çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="912f0-193">A new container is then started using the image and runs your Node.js app based on the latest commits in GitHub.</span></span>


## <a name="test-your-pipeline"></a><span data-ttu-id="912f0-194">İşlem hattınızı test</span><span class="sxs-lookup"><span data-stu-id="912f0-194">Test your pipeline</span></span>
<span data-ttu-id="912f0-195">Eylem tüm ardışık görmek için Düzenle *index.js* , forked GitHub deposuna dosya yeniden ve tıklayın **Commit değişiklik**.</span><span class="sxs-lookup"><span data-stu-id="912f0-195">To see the whole pipeline in action, edit the *index.js* file in your forked GitHub repo again and click **Commit change**.</span></span> <span data-ttu-id="912f0-196">Jenkins için GitHub Web kancası üzerinde dayalı yeni bir iş başlatır.</span><span class="sxs-lookup"><span data-stu-id="912f0-196">A new job starts in Jenkins based on the webhook for GitHub.</span></span> <span data-ttu-id="912f0-197">Docker görüntü oluşturma ve yeni bir kapsayıcı uygulamanızı başlatmak için birkaç saniye sürer.</span><span class="sxs-lookup"><span data-stu-id="912f0-197">It takes a few seconds to create the Docker image and start your app in a new container.</span></span>

<span data-ttu-id="912f0-198">Gerekirse, VM genel IP adresi yeniden alın:</span><span class="sxs-lookup"><span data-stu-id="912f0-198">If needed, obtain the public IP address of your VM again:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="912f0-199">Bir web tarayıcısı açın ve girin `http://<publicIps>:1337`.</span><span class="sxs-lookup"><span data-stu-id="912f0-199">Open a web browser and enter `http://<publicIps>:1337`.</span></span> <span data-ttu-id="912f0-200">Node.js uygulamanızı görüntülenir ve en son işlemeleri GitHub çatalı içinde aşağıdaki gibi yansıtır:</span><span class="sxs-lookup"><span data-stu-id="912f0-200">Your Node.js app is displayed and reflects the latest commits in your GitHub fork as follows:</span></span>

![Çalışan Node.js uygulaması](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

<span data-ttu-id="912f0-202">Artık başka bir düzenleme yapın *index.js* dosya Github'da ve değişikliği uygulayın.</span><span class="sxs-lookup"><span data-stu-id="912f0-202">Now make another edit to the *index.js* file in GitHub and commit the change.</span></span> <span data-ttu-id="912f0-203">İş Jenkins içinde tamamlanması birkaç saniye bekleyin, sonra da yeni bir kapsayıcı şu şekilde çalışan, uygulamanın güncelleştirilmiş sürümünü görmek için web tarayıcınızı yenileyin:</span><span class="sxs-lookup"><span data-stu-id="912f0-203">Wait a few seconds for the job to complete in Jenkins, then refresh your web browser to see the updated version of your app running in a new container as follows:</span></span>

![Başka bir GitHub yürütme sonrasında çalışan Node.js uygulaması](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a><span data-ttu-id="912f0-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="912f0-205">Next steps</span></span>
<span data-ttu-id="912f0-206">Bu öğreticide, bir Jenkins yapı her kod tamamlama çalıştırın ve uygulamanızı test etmek için Docker kapsayıcısı dağıtmak için GitHub yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="912f0-206">In this tutorial, you configured GitHub to run a Jenkins build job on each code commit and then deploy a Docker container to test your app.</span></span> <span data-ttu-id="912f0-207">Size nasıl öğrenilen için:</span><span class="sxs-lookup"><span data-stu-id="912f0-207">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="912f0-208">Jenkins VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="912f0-208">Create a Jenkins VM</span></span>
> * <span data-ttu-id="912f0-209">Yükleme ve Jenkins yapılandırma</span><span class="sxs-lookup"><span data-stu-id="912f0-209">Install and configure Jenkins</span></span>
> * <span data-ttu-id="912f0-210">GitHub ile Jenkins arasında Web kancası tümleştirme oluşturma</span><span class="sxs-lookup"><span data-stu-id="912f0-210">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="912f0-211">Oluşturma ve GitHub yürütme Jenkins yapı işlerden tetikler</span><span class="sxs-lookup"><span data-stu-id="912f0-211">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="912f0-212">Uygulamanız için Docker görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="912f0-212">Create a Docker image for your app</span></span>
> * <span data-ttu-id="912f0-213">Yeni Docker görüntü ve uygulamayı çalıştıran güncelleştirmeleri GitHub yürütme yapı doğrulayın</span><span class="sxs-lookup"><span data-stu-id="912f0-213">Verify GitHub commits build new Docker image and updates running app</span></span>

<span data-ttu-id="912f0-214">Jenkins Visual Studio Team Services ile tümleştirme hakkında daha fazla bilgi için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="912f0-214">Advance to the next tutorial to learn more about how to integrate Jenkins with Visual Studio Team Services.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="912f0-215">Jenkins ve Team Services ile uygulamaları dağıtma</span><span class="sxs-lookup"><span data-stu-id="912f0-215">Deploy apps with Jenkins and Team Services</span></span>](tutorial-build-deploy-jenkins.md)