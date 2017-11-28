---
title: "aaaCreate Jenkins ile azure'da geliştirme ardışık | Microsoft Docs"
description: "Nasıl toocreate Jenkins sanal makine github'dan çeken her kodunda kaydetmek ve yeni bir Docker kapsayıcısı toorun derlemeler Azure'da uygulamanızı öğrenin"
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
ms.openlocfilehash: c079e3c9186c9da0a3e51e1823215779c565e0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a><span data-ttu-id="bcaa4-103">Nasıl toocreate Jenkins, GitHub ve Docker ile azure'da bir Linux VM üzerinde geliştirme altyapısı</span><span class="sxs-lookup"><span data-stu-id="bcaa4-103">How toocreate a development infrastructure on a Linux VM in Azure with Jenkins, GitHub, and Docker</span></span>
<span data-ttu-id="bcaa4-104">tooautomate hello yapı ve test aşaması uygulama geliştirme, bir sürekli tümleştirme ve dağıtım (CI/CD) ardışık düzen kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-104">tooautomate hello build and test phase of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="bcaa4-105">Bu öğreticide, Azure VM temelinde CI/CD işlem hattı oluşturmak için nasıl dahil:</span><span class="sxs-lookup"><span data-stu-id="bcaa4-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bcaa4-106">Jenkins VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="bcaa4-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="bcaa4-107">Yükleme ve Jenkins yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bcaa4-107">Install and configure Jenkins</span></span>
> * <span data-ttu-id="bcaa4-108">GitHub ile Jenkins arasında Web kancası tümleştirme oluşturma</span><span class="sxs-lookup"><span data-stu-id="bcaa4-108">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="bcaa4-109">Oluşturma ve GitHub yürütme Jenkins yapı işlerden tetikler</span><span class="sxs-lookup"><span data-stu-id="bcaa4-109">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="bcaa4-110">Uygulamanız için Docker görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="bcaa4-110">Create a Docker image for your app</span></span>
> * <span data-ttu-id="bcaa4-111">Yeni Docker görüntü ve uygulamayı çalıştıran güncelleştirmeleri GitHub yürütme yapı doğrulayın</span><span class="sxs-lookup"><span data-stu-id="bcaa4-111">Verify GitHub commits build new Docker image and updates running app</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="bcaa4-112">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="bcaa4-113">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="bcaa4-114">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bcaa4-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-jenkins-instance"></a><span data-ttu-id="bcaa4-115">Jenkins örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="bcaa4-115">Create Jenkins instance</span></span>
<span data-ttu-id="bcaa4-116">Önceki bir öğretici içinde [nasıl toocustomize Linux sanal bir makinede ilk önyükleme](tutorial-automate-vm-deployment.md), size nasıl öğrenilen tooautomate VM özelleştirme bulut init ile.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-116">In a previous tutorial on [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with cloud-init.</span></span> <span data-ttu-id="bcaa4-117">Bu öğretici, bir VM üzerinde bir bulut init dosya tooinstall Jenkins ve Docker kullanır.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-117">This tutorial uses a cloud-init file tooinstall Jenkins and Docker on a VM.</span></span> 

<span data-ttu-id="bcaa4-118">Geçerli kabuğunuzu adlı bir dosya oluşturun *bulut init.txt* Yapıştır hello izleyerek yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-118">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="bcaa4-119">Örneğin, yerel makinenizde değil hello bulut Kabuk hello dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-119">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="bcaa4-120">Girin `sensible-editor cloud-init-jenkins.txt` toocreate hello dosya ve kullanılabilir düzenleyicileri listesini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-120">Enter `sensible-editor cloud-init-jenkins.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="bcaa4-121">Merhaba tüm bulut init dosyanın doğru şekilde kopyalandığından emin olun, özellikle ilk satırı hello:</span><span class="sxs-lookup"><span data-stu-id="bcaa4-121">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

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

<span data-ttu-id="bcaa4-122">Bir VM oluşturmadan önce bir kaynak grubuyla oluşturmanız [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="bcaa4-122">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="bcaa4-123">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroupJenkins* hello içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="bcaa4-123">hello following example creates a resource group named *myResourceGroupJenkins* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

<span data-ttu-id="bcaa4-124">Şimdi bir VM oluşturmak [az vm oluşturma](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="bcaa4-124">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="bcaa4-125">Kullanım hello `--custom-data` parametresi toopass bulut init yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-125">Use hello `--custom-data` parameter toopass in your cloud-init config file.</span></span> <span data-ttu-id="bcaa4-126">Merhaba tam yol çok sağlamak*bulut init jenkins.txt* mevcut çalışma dizininizi dışında hello dosyasını kaydettiyseniz.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-126">Provide hello full path too*cloud-init-jenkins.txt* if you saved hello file outside of your present working directory.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

<span data-ttu-id="bcaa4-127">Oluşturulan ve yapılandırılan hello VM toobe birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-127">It takes a few minutes for hello VM toobe created and configured.</span></span>

<span data-ttu-id="bcaa4-128">tooallow web trafiği tooreach kullanım VM'nizi [az vm Aç-port](/cli/azure/vm#open-port) tooopen bağlantı noktası *8080* Jenkins trafiği ve bağlantı noktası için *1337* kullanılan toorun örnek bir uygulama olan hello Node.js uygulaması için:</span><span class="sxs-lookup"><span data-stu-id="bcaa4-128">tooallow web traffic tooreach your VM, use [az vm open-port](/cli/azure/vm#open-port) tooopen port *8080* for Jenkins traffic and port *1337* for hello Node.js app that is used toorun a sample app:</span></span>

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a><span data-ttu-id="bcaa4-129">Jenkins yapılandırın</span><span class="sxs-lookup"><span data-stu-id="bcaa4-129">Configure Jenkins</span></span>
<span data-ttu-id="bcaa4-130">tooaccess, Jenkins örneği, VM'yi hello genel IP adresi edinin:</span><span class="sxs-lookup"><span data-stu-id="bcaa4-130">tooaccess your Jenkins instance, obtain hello public IP address of your VM:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="bcaa4-131">Güvenlik nedeniyle, Jenkins yüklemek, VM toostart hello üzerindeki bir metin dosyasında depolanan tooenter hello ilk yönetici parolası gerekir.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-131">For security purposes, you need tooenter hello initial admin password that is stored in a text file on your VM toostart hello Jenkins install.</span></span> <span data-ttu-id="bcaa4-132">Merhaba önceki adım tooSSH tooyour içinde VM elde hello ortak IP adresini kullan:</span><span class="sxs-lookup"><span data-stu-id="bcaa4-132">Use hello public IP address obtained in hello previous step tooSSH tooyour VM:</span></span>

```bash
ssh azureuser@<publicIps>
```

<span data-ttu-id="bcaa4-133">Görünüm hello `initialAdminPassword` , Jenkins yükleyin ve onu kopyalamak için:</span><span class="sxs-lookup"><span data-stu-id="bcaa4-133">View hello `initialAdminPassword` for your Jenkins install and copy it:</span></span>

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

<span data-ttu-id="bcaa4-134">Merhaba dosya henüz kullanılabilir durumda değilse, bulut init toocomplete hello Jenkins ve Docker yükleme için birkaç dakika daha bekleyin.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-134">If hello file isn't available yet, wait a couple more minutes for cloud-init toocomplete hello Jenkins and Docker install.</span></span>

<span data-ttu-id="bcaa4-135">Şimdi bir web tarayıcısı açın ve çok Git`http://<publicIps>:8080`.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-135">Now open a web browser and go too`http://<publicIps>:8080`.</span></span> <span data-ttu-id="bcaa4-136">Merhaba ilk Jenkins Kurulum aşağıdaki gibi tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="bcaa4-136">Complete hello initial Jenkins setup as follows:</span></span>

- <span data-ttu-id="bcaa4-137">Merhaba girin *initialAdminPassword* hello VM hello önceki adımda elde.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-137">Enter hello *initialAdminPassword* obtained from hello VM in hello previous step.</span></span>
- <span data-ttu-id="bcaa4-138">Tıklatın **eklentileri tooinstall seçin**</span><span class="sxs-lookup"><span data-stu-id="bcaa4-138">Click **Select plugins tooinstall**</span></span>
- <span data-ttu-id="bcaa4-139">Arama *GitHub* hello metin kutusunda hello üstte hello seçin *GitHub eklentisi*, ardından **yükleyin**</span><span class="sxs-lookup"><span data-stu-id="bcaa4-139">Search for *GitHub* in hello text box across hello top, select hello *GitHub plugin*, then click **Install**</span></span>
- <span data-ttu-id="bcaa4-140">toocreate Jenkins kullanıcı hesabını istediğiniz gibi hello formu doldurun.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-140">toocreate a Jenkins user account, fill out hello form as desired.</span></span> <span data-ttu-id="bcaa4-141">Güvenlik açısından bakıldığında, hello varsayılan yönetici hesabı olarak etmeden yerine bu ilk Jenkins kullanıcı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-141">From a security perspective, you should create this first Jenkins user rather than continuing as hello default admin account.</span></span>
- <span data-ttu-id="bcaa4-142">Tamamlandığında tıklatarak **Jenkins kullanmaya başlama**</span><span class="sxs-lookup"><span data-stu-id="bcaa4-142">When finished, click **Start using Jenkins**</span></span>


## <a name="create-github-webhook"></a><span data-ttu-id="bcaa4-143">GitHub Web kancası oluşturma</span><span class="sxs-lookup"><span data-stu-id="bcaa4-143">Create GitHub webhook</span></span>
<span data-ttu-id="bcaa4-144">GitHub, açık hello ile tooconfigure hello tümleştirme [Node.js Hello World örnek uygulaması](https://github.com/Azure-Samples/nodejs-docs-hello-world) hello Azure örneklerinden depodaki gelen.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-144">tooconfigure hello integration with GitHub, open hello [Node.js Hello World sample app](https://github.com/Azure-Samples/nodejs-docs-hello-world) from hello Azure samples repo.</span></span> <span data-ttu-id="bcaa4-145">toofork hello depodaki tooyour GitHub hesabı sahibi, hello tıklatın **çatalı** hello üst sağ köşesindeki düğmesini.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-145">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>

<span data-ttu-id="bcaa4-146">Oluşturduğunuz hello çatalı içinde bir Web kancası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="bcaa4-146">Create a webhook inside hello fork you created:</span></span>

- <span data-ttu-id="bcaa4-147">Tıklatın **ayarları**seçeneğini belirleyip **tümleştirmeler & Hizmetleri** hello sol taraftaki.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-147">Click **Settings**, then select **Integrations & services** on hello left-hand side.</span></span>
- <span data-ttu-id="bcaa4-148">Tıklatın **Hizmet Ekle**, enter *Jenkins* filtre kutusuna.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-148">Click **Add service**, then enter *Jenkins* in filter box.</span></span>
- <span data-ttu-id="bcaa4-149">Seçin *Jenkins (GitHub eklentisi)*</span><span class="sxs-lookup"><span data-stu-id="bcaa4-149">Select *Jenkins (GitHub plugin)*</span></span>
- <span data-ttu-id="bcaa4-150">Hello için **Jenkins kanca URL**, girin `http://<publicIps>:8080/github-webhook/`.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-150">For hello **Jenkins hook URL**, enter `http://<publicIps>:8080/github-webhook/`.</span></span> <span data-ttu-id="bcaa4-151">Merhaba sondaki eklediğinizden emin olun /</span><span class="sxs-lookup"><span data-stu-id="bcaa4-151">Make sure you include hello trailing /</span></span>
- <span data-ttu-id="bcaa4-152">Tıklatın **Hizmet Ekle**</span><span class="sxs-lookup"><span data-stu-id="bcaa4-152">Click **Add service**</span></span>

![GitHub Web kancası çatallanmış tooyour depo Ekle](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a><span data-ttu-id="bcaa4-154">Jenkins işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="bcaa4-154">Create Jenkins job</span></span>
<span data-ttu-id="bcaa4-155">kod yürütme gibi toohave Jenkins yanıt tooan olay github'da Jenkins iş oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-155">toohave Jenkins respond tooan event in GitHub such as committing code, create a Jenkins job.</span></span> 

<span data-ttu-id="bcaa4-156">Jenkins siteniz tıklatın **yeni işleri oluşturmak** hello giriş sayfasından:</span><span class="sxs-lookup"><span data-stu-id="bcaa4-156">In your Jenkins website, click **Create new jobs** from hello home page:</span></span>

- <span data-ttu-id="bcaa4-157">Girin *HelloWorld* iş adı olarak.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-157">Enter *HelloWorld* as job name.</span></span> <span data-ttu-id="bcaa4-158">Seçin **Serbest stilde proje**seçeneğini belirleyip **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-158">Choose **Freestyle project**, then select **OK**.</span></span>
- <span data-ttu-id="bcaa4-159">Merhaba altında **genel** bölümünde, select **GitHub** proje ve çatallanmış depodaki URL'nizi girin *https://github.com/iainfoulds/nodejs-docs-hello-world*</span><span class="sxs-lookup"><span data-stu-id="bcaa4-159">Under hello **General** section, select **GitHub** project and enter your forked repo URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world*</span></span>
- <span data-ttu-id="bcaa4-160">Merhaba altında **kaynak kodu Yönetimi** bölümünde, select **Git**, forked depodaki girin *.git* URL gibi *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span><span class="sxs-lookup"><span data-stu-id="bcaa4-160">Under hello **Source code management** section, select **Git**, enter your forked repo *.git* URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span></span>
- <span data-ttu-id="bcaa4-161">Merhaba altında **yapı tetikleyicileri** bölümünde, select **GITscm yoklama için GitHub kanca tetikleyici**.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-161">Under hello **Build Triggers** section, select **GitHub hook trigger for GITscm polling**.</span></span>
- <span data-ttu-id="bcaa4-162">Merhaba altında **yapı** bölümünde, seçin **Ekle derleme adımı**.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-162">Under hello **Build** section, choose **Add build step**.</span></span> <span data-ttu-id="bcaa4-163">Seçin **Kabuk yürütme**, enter `echo "Testing"` toocommand penceresinde.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-163">Select **Execute shell**, then enter `echo "Testing"` in toocommand window.</span></span>
- <span data-ttu-id="bcaa4-164">Tıklatın **kaydetmek** hello altındaki hello işler penceresi.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-164">Click **Save** at hello bottom of hello jobs window.</span></span>


## <a name="test-github-integration"></a><span data-ttu-id="bcaa4-165">Test GitHub tümleştirme</span><span class="sxs-lookup"><span data-stu-id="bcaa4-165">Test GitHub integration</span></span>
<span data-ttu-id="bcaa4-166">tootest hello Jenkins, GitHub tümleştirme, çatalı değişikliği uygulayın.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-166">tootest hello GitHub integration with Jenkins, commit a change in your fork.</span></span> 

<span data-ttu-id="bcaa4-167">Geri Github'da web kullanıcı Arabirimi, forked depoyu seçin ve hello ardından **index.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-167">Back in GitHub web UI, select your forked repo, and then click hello **index.js** file.</span></span> <span data-ttu-id="bcaa4-168">Satır 6 okunacak şekilde hello Kurşun Kalem simgesini tooedit bu dosyayı tıklatın:</span><span class="sxs-lookup"><span data-stu-id="bcaa4-168">Click hello pencil icon tooedit this file so line 6 reads:</span></span>

```nodejs
response.end("Hello World!");
```

<span data-ttu-id="bcaa4-169">toocommit yaptığınız değişiklikleri tıklatın hello **değişiklikleri** hello altındaki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-169">toocommit your changes, click hello **Commit changes** button at hello bottom.</span></span>

<span data-ttu-id="bcaa4-170">Jenkins içinde yeni bir yapı altında hello başlatır **yapı geçmiş** hello sol alt köşesindeki iş sayfanızı bölümü.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-170">In Jenkins, a new build starts under hello **Build history** section of hello bottom left-hand corner of your job page.</span></span> <span data-ttu-id="bcaa4-171">Merhaba yapı numarası bağlantısına ve Seç'i tıklatın **konsol çıkış** hello sol boyutu.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-171">Click hello build number link and select **Console output** on hello left-hand size.</span></span> <span data-ttu-id="bcaa4-172">Jenkins alır, kodunuzu GitHub ve hello yapı eylemi çıkışları hello iletiden çekildiğinde hello adımları görüntüleyebilirsiniz `Testing` toohello konsol.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-172">You can view hello steps Jenkins takes as your code is pulled from GitHub and hello build action outputs hello message `Testing` toohello console.</span></span> <span data-ttu-id="bcaa4-173">Github'da, her bir işleme yapıldığında hello Web kancası tooJenkins ulaştığında ve bu şekilde yeni bir derlemeyi tetiklemeyi.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-173">Each time a commit is made in GitHub, hello webhook reaches out tooJenkins and trigger a new build in this way.</span></span>


## <a name="define-docker-build-image"></a><span data-ttu-id="bcaa4-174">Docker derleme görüntüyü tanımlayın</span><span class="sxs-lookup"><span data-stu-id="bcaa4-174">Define Docker build image</span></span>
<span data-ttu-id="bcaa4-175">toosee hello Node.js uygulaması, GitHub yürütme üzerinde temelinde çalışmasına olanak tanır bir Docker görüntü toorun hello uygulaması oluşturma.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-175">toosee hello Node.js app running based on your GitHub commits, lets build a Docker image toorun hello app.</span></span> <span data-ttu-id="bcaa4-176">Merhaba görüntü nasıl tooconfigure hello hello uygulamanın çalıştığı kapsayıcı tanımlayan bir Dockerfile yerleşik olarak bulunur.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-176">hello image is built from a Dockerfile that defines how tooconfigure hello container that runs hello app.</span></span> 

<span data-ttu-id="bcaa4-177">Merhaba SSH bağlantı tooyour VM, bir önceki adımda oluşturduğunuz hello iş sonra adlı toohello Jenkins çalışma dizini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-177">From hello SSH connection tooyour VM, change toohello Jenkins workspace directory named after hello job you created in a previous step.</span></span> <span data-ttu-id="bcaa4-178">Bizim örneğimizde, adlandırılması *HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-178">In our example, that was named *HelloWorld*.</span></span>

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

<span data-ttu-id="bcaa4-179">Bu çalışma alanı dizindeki bir dosya oluşturmak `sudo sensible-editor Dockerfile` Yapıştır hello izleyerek içeriği.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-179">Create a file with in this workspace directory with `sudo sensible-editor Dockerfile` and paste hello following contents.</span></span> <span data-ttu-id="bcaa4-180">Tüm Dockerfile olduğundan bu hello özellikle hello ilk satırı doğru şekilde kopyalandığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="bcaa4-180">Make sure that hello whole Dockerfile is copied correctly, especially hello first line:</span></span>

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

<span data-ttu-id="bcaa4-181">Bu Dockerfile hello Alpine Linux kullanarak temel Node.js görüntü kullanır, Hello World uygulama hello çıkarır bağlantı 1337 çalışan sonra hello uygulama dosyaları kopyalar ve onu başlatır.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-181">This Dockerfile uses hello base Node.js image using Alpine Linux, exposes port 1337 that hello Hello World app runs on, then copies hello app files and initializes it.</span></span>


## <a name="create-jenkins-build-rules"></a><span data-ttu-id="bcaa4-182">Jenkins derleme kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="bcaa4-182">Create Jenkins build rules</span></span>
<span data-ttu-id="bcaa4-183">Önceki adımda, bir ileti toohello konsol çıktısı temel bir Jenkins yapı kuralı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-183">In a previous step, you created a basic Jenkins build rule that output a message toohello console.</span></span> <span data-ttu-id="bcaa4-184">Bizim Dockerfile Hello derleme adımı toouse oluşturma ve hello uygulama çalıştırma olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-184">Lets create hello build step toouse our Dockerfile and run hello app.</span></span>

<span data-ttu-id="bcaa4-185">Geri Jenkins örneğinizi içinde bir önceki adımda oluşturduğunuz hello işi seçin.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-185">Back in your Jenkins instance, select hello job you created in a previous step.</span></span> <span data-ttu-id="bcaa4-186">Tıklatın **yapılandırma** hello taraftaki ve toohello aşağı kaydırın **yapı** bölümü:</span><span class="sxs-lookup"><span data-stu-id="bcaa4-186">Click **Configure** on hello left-hand side and scroll down toohello **Build** section:</span></span>

- <span data-ttu-id="bcaa4-187">Var olan kaldırmak `echo "Test"` adım oluşturma.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-187">Remove your existing `echo "Test"` build step.</span></span> <span data-ttu-id="bcaa4-188">Merhaba kırmızı çapraz ya hello üst sağ köşesinde hello varolan derleme adımı kutusu üzerinde'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-188">Click hello red cross on hello top right-hand corner of hello existing build step box.</span></span>
- <span data-ttu-id="bcaa4-189">Tıklatın **Ekle derleme adımı**seçeneğini belirleyip **Kabuk yürütme**</span><span class="sxs-lookup"><span data-stu-id="bcaa4-189">Click **Add build step**, then select **Execute shell**</span></span>
- <span data-ttu-id="bcaa4-190">Merhaba, **komutu** kutusunda, Docker komutları aşağıdaki hello girin, ardından seçin **kaydetmek**:</span><span class="sxs-lookup"><span data-stu-id="bcaa4-190">In hello **Command** box, enter hello following Docker commands, then select **Save**:</span></span>

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

<span data-ttu-id="bcaa4-191">Merhaba Docker derleme adımları imaj ve hello Jenkins ile yapı numarası görüntüleri bir geçmişini sağlamak için etiketi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-191">hello Docker build steps create an image and tag it with hello Jenkins build number so you can maintain a history of images.</span></span> <span data-ttu-id="bcaa4-192">Merhaba uygulamayı çalıştıran herhangi bir varolan kapsayıcıdaki durdurulur ve sonra kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-192">Any existing containers running hello app are stopped and then removed.</span></span> <span data-ttu-id="bcaa4-193">Merhaba görüntü kullanmaya ve hello son yürütme github'da göre Node.js uygulamanızı çalıştıran yeni bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-193">A new container is then started using hello image and runs your Node.js app based on hello latest commits in GitHub.</span></span>


## <a name="test-your-pipeline"></a><span data-ttu-id="bcaa4-194">İşlem hattınızı test</span><span class="sxs-lookup"><span data-stu-id="bcaa4-194">Test your pipeline</span></span>
<span data-ttu-id="bcaa4-195">Eylem içinde toosee hello tüm ardışık Düzenle hello *index.js* , forked GitHub deposuna dosya yeniden ve'ı tıklatın **Commit değişiklik**.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-195">toosee hello whole pipeline in action, edit hello *index.js* file in your forked GitHub repo again and click **Commit change**.</span></span> <span data-ttu-id="bcaa4-196">Jenkins için GitHub hello Web kancası dayalı yeni bir iş başlatır.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-196">A new job starts in Jenkins based on hello webhook for GitHub.</span></span> <span data-ttu-id="bcaa4-197">Toocreate hello Docker görüntü birkaç saniye sürer ve yeni bir kapsayıcı uygulamanızı başlatın.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-197">It takes a few seconds toocreate hello Docker image and start your app in a new container.</span></span>

<span data-ttu-id="bcaa4-198">Gerekirse, hello genel IP adresi, bir VM'nin yeniden alın:</span><span class="sxs-lookup"><span data-stu-id="bcaa4-198">If needed, obtain hello public IP address of your VM again:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="bcaa4-199">Bir web tarayıcısı açın ve girin `http://<publicIps>:1337`.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-199">Open a web browser and enter `http://<publicIps>:1337`.</span></span> <span data-ttu-id="bcaa4-200">Node.js uygulamanızı görüntülenir ve GitHub çatalı içinde hello son yürütme gibi yansıtır:</span><span class="sxs-lookup"><span data-stu-id="bcaa4-200">Your Node.js app is displayed and reflects hello latest commits in your GitHub fork as follows:</span></span>

![Çalışan Node.js uygulaması](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

<span data-ttu-id="bcaa4-202">Artık başka bir düzen toohello olun *index.js* GitHub ve yürütme hello değişiklik dosyasında.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-202">Now make another edit toohello *index.js* file in GitHub and commit hello change.</span></span> <span data-ttu-id="bcaa4-203">Merhaba iş toocomplete Jenkins, birkaç saniye bekleyin, sonra da web tarayıcı toosee hello güncelleştirilmiş sürümü yeni bir kapsayıcı şu şekilde çalışan, uygulamanızın yenileyin:</span><span class="sxs-lookup"><span data-stu-id="bcaa4-203">Wait a few seconds for hello job toocomplete in Jenkins, then refresh your web browser toosee hello updated version of your app running in a new container as follows:</span></span>

![Başka bir GitHub yürütme sonrasında çalışan Node.js uygulaması](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a><span data-ttu-id="bcaa4-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bcaa4-205">Next steps</span></span>
<span data-ttu-id="bcaa4-206">Bu öğreticide her kod tamamlama GitHub toorun Jenkins derleme işi yapılandırılmış ve Docker kapsayıcısı tootest uygulamanızı dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-206">In this tutorial, you configured GitHub toorun a Jenkins build job on each code commit and then deploy a Docker container tootest your app.</span></span> <span data-ttu-id="bcaa4-207">Size nasıl öğrenilen için:</span><span class="sxs-lookup"><span data-stu-id="bcaa4-207">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bcaa4-208">Jenkins VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="bcaa4-208">Create a Jenkins VM</span></span>
> * <span data-ttu-id="bcaa4-209">Yükleme ve Jenkins yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bcaa4-209">Install and configure Jenkins</span></span>
> * <span data-ttu-id="bcaa4-210">GitHub ile Jenkins arasında Web kancası tümleştirme oluşturma</span><span class="sxs-lookup"><span data-stu-id="bcaa4-210">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="bcaa4-211">Oluşturma ve GitHub yürütme Jenkins yapı işlerden tetikler</span><span class="sxs-lookup"><span data-stu-id="bcaa4-211">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="bcaa4-212">Uygulamanız için Docker görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="bcaa4-212">Create a Docker image for your app</span></span>
> * <span data-ttu-id="bcaa4-213">Yeni Docker görüntü ve uygulamayı çalıştıran güncelleştirmeleri GitHub yürütme yapı doğrulayın</span><span class="sxs-lookup"><span data-stu-id="bcaa4-213">Verify GitHub commits build new Docker image and updates running app</span></span>

<span data-ttu-id="bcaa4-214">Toohello sonraki öğretici toolearn hakkında daha fazla ilerletmek toointegrate Jenkins Visual Studio Team Services ile.</span><span class="sxs-lookup"><span data-stu-id="bcaa4-214">Advance toohello next tutorial toolearn more about how toointegrate Jenkins with Visual Studio Team Services.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bcaa4-215">Jenkins ve Team Services ile uygulamaları dağıtma</span><span class="sxs-lookup"><span data-stu-id="bcaa4-215">Deploy apps with Jenkins and Team Services</span></span>](tutorial-build-deploy-jenkins.md)