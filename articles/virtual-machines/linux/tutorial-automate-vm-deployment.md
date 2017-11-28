---
title: "ilk önyükleme azure'da bir Linux VM aaaCustomize | Microsoft Docs"
description: "Nasıl toouse bulut başlatma ve anahtar kasası toocustomze Linux VM'ler hello ilk kez bunlar Azure'da önyükleme öğrenin"
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
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 280189723ac0205226f9c0068bd605da13249ace
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-linux-virtual-machine-on-first-boot"></a><span data-ttu-id="c58c8-103">Nasıl toocustomize Linux sanal bir makinede ilk önyükleme</span><span class="sxs-lookup"><span data-stu-id="c58c8-103">How toocustomize a Linux virtual machine on first boot</span></span>
<span data-ttu-id="c58c8-104">Önceki bir öğreticide, nasıl öğrenilen tooSSH tooa sanal makine (VM) ve NGINX el ile yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c58c8-104">In a previous tutorial, you learned how tooSSH tooa virtual machine (VM) and manually install NGINX.</span></span> <span data-ttu-id="c58c8-105">hızlı ve tutarlı bir şekilde, tür Otomasyon toocreate VM'ler genellikle istenen.</span><span class="sxs-lookup"><span data-stu-id="c58c8-105">toocreate VMs in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="c58c8-106">Ortak bir yaklaşım toocustomize ilk önyüklemede VM toouse olan [bulut init](https://cloudinit.readthedocs.io).</span><span class="sxs-lookup"><span data-stu-id="c58c8-106">A common approach toocustomize a VM on first boot is toouse [cloud-init](https://cloudinit.readthedocs.io).</span></span> <span data-ttu-id="c58c8-107">Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c58c8-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c58c8-108">Bir bulut init yapılandırma dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="c58c8-108">Create a cloud-init config file</span></span>
> * <span data-ttu-id="c58c8-109">Bir bulut init dosyası kullanan bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="c58c8-109">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="c58c8-110">Merhaba VM oluşturulduktan sonra çalışan bir Node.js uygulaması görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="c58c8-110">View a running Node.js app after hello VM is created</span></span>
> * <span data-ttu-id="c58c8-111">Anahtar kasası toosecurely deposu sertifikaları kullanma</span><span class="sxs-lookup"><span data-stu-id="c58c8-111">Use Key Vault toosecurely store certificates</span></span>
> * <span data-ttu-id="c58c8-112">Güvenli NGINX dağıtımlarında bulut init otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="c58c8-112">Automate secure deployments of NGINX with cloud-init</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c58c8-113">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="c58c8-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="c58c8-114">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="c58c8-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="c58c8-115">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c58c8-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  



## <a name="cloud-init-overview"></a><span data-ttu-id="c58c8-116">Bulut init genel bakış</span><span class="sxs-lookup"><span data-stu-id="c58c8-116">Cloud-init overview</span></span>
<span data-ttu-id="c58c8-117">[Bulut init](https://cloudinit.readthedocs.io) yaygın olarak kullanılan bir yaklaşım toocustomize hello için ilk kez önyükleme bir Linux VM aynıdır.</span><span class="sxs-lookup"><span data-stu-id="c58c8-117">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach toocustomize a Linux VM as it boots for hello first time.</span></span> <span data-ttu-id="c58c8-118">Bulut init tooinstall paketleri ve dosyaları veya tooconfigure kullanıcılar ve güvenlik yazma kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c58c8-118">You can use cloud-init tooinstall packages and write files, or tooconfigure users and security.</span></span> <span data-ttu-id="c58c8-119">Bulut init hello ilk önyükleme işlemi sırasında çalışırken, hiçbir ek adımlar vardır veya aracıları tooapply yapılandırmanız gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="c58c8-119">As cloud-init runs during hello initial boot process, there are no additional steps or required agents tooapply your configuration.</span></span>

<span data-ttu-id="c58c8-120">Bulut init dağıtımları üzerinde de çalışır.</span><span class="sxs-lookup"><span data-stu-id="c58c8-120">Cloud-init also works across distributions.</span></span> <span data-ttu-id="c58c8-121">Örneğin, kullanmadığınız **get apt yükleme** veya **yum yükleme** tooinstall bir paket.</span><span class="sxs-lookup"><span data-stu-id="c58c8-121">For example, you don't use **apt-get install** or **yum install** tooinstall a package.</span></span> <span data-ttu-id="c58c8-122">Bunun yerine, paketleri tooinstall listesi tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c58c8-122">Instead you can define a list of packages tooinstall.</span></span> <span data-ttu-id="c58c8-123">Bulut init hello Yerel Paket yönetim aracı için seçtiğiniz hello distro otomatik olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="c58c8-123">Cloud-init automatically uses hello native package management tool for hello distro you select.</span></span>

<span data-ttu-id="c58c8-124">Bizim ortakları tooget bulut dahil başlatma çalışmak ve çalışma tooAzure sağladıkları hello görüntülerinde duyuyoruz.</span><span class="sxs-lookup"><span data-stu-id="c58c8-124">We are working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span> <span data-ttu-id="c58c8-125">Aşağıdaki tablonun hello hello geçerli bulut init kullanılabilirlik Azure platform görüntüleri özetlenmektedir:</span><span class="sxs-lookup"><span data-stu-id="c58c8-125">hello following table outlines hello current cloud-init availability on Azure platform images:</span></span>

| <span data-ttu-id="c58c8-126">Diğer ad</span><span class="sxs-lookup"><span data-stu-id="c58c8-126">Alias</span></span> | <span data-ttu-id="c58c8-127">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="c58c8-127">Publisher</span></span> | <span data-ttu-id="c58c8-128">Sunduğu</span><span class="sxs-lookup"><span data-stu-id="c58c8-128">Offer</span></span> | <span data-ttu-id="c58c8-129">SKU</span><span class="sxs-lookup"><span data-stu-id="c58c8-129">SKU</span></span> | <span data-ttu-id="c58c8-130">Sürüm</span><span class="sxs-lookup"><span data-stu-id="c58c8-130">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="c58c8-131">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="c58c8-131">UbuntuLTS</span></span> |<span data-ttu-id="c58c8-132">Canonical</span><span class="sxs-lookup"><span data-stu-id="c58c8-132">Canonical</span></span> |<span data-ttu-id="c58c8-133">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="c58c8-133">UbuntuServer</span></span> |<span data-ttu-id="c58c8-134">16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="c58c8-134">16.04-LTS</span></span> |<span data-ttu-id="c58c8-135">en son</span><span class="sxs-lookup"><span data-stu-id="c58c8-135">latest</span></span> |
| <span data-ttu-id="c58c8-136">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="c58c8-136">UbuntuLTS</span></span> |<span data-ttu-id="c58c8-137">Canonical</span><span class="sxs-lookup"><span data-stu-id="c58c8-137">Canonical</span></span> |<span data-ttu-id="c58c8-138">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="c58c8-138">UbuntuServer</span></span> |<span data-ttu-id="c58c8-139">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="c58c8-139">14.04.5-LTS</span></span> |<span data-ttu-id="c58c8-140">en son</span><span class="sxs-lookup"><span data-stu-id="c58c8-140">latest</span></span> |
| <span data-ttu-id="c58c8-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="c58c8-141">CoreOS</span></span> |<span data-ttu-id="c58c8-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="c58c8-142">CoreOS</span></span> |<span data-ttu-id="c58c8-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="c58c8-143">CoreOS</span></span> |<span data-ttu-id="c58c8-144">Dengeli</span><span class="sxs-lookup"><span data-stu-id="c58c8-144">Stable</span></span> |<span data-ttu-id="c58c8-145">en son</span><span class="sxs-lookup"><span data-stu-id="c58c8-145">latest</span></span> |


## <a name="create-cloud-init-config-file"></a><span data-ttu-id="c58c8-146">Bulut init yapılandırma dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="c58c8-146">Create cloud-init config file</span></span>
<span data-ttu-id="c58c8-147">Eylem toosee bulut başlatma NGINX yükler ve basit bir 'Hello World' Node.js uygulaması çalıştıran bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c58c8-147">toosee cloud-init in action, create a VM that installs NGINX and runs a simple 'Hello World' Node.js app.</span></span> <span data-ttu-id="c58c8-148">Bulut init yapılandırma aşağıdaki hello hello gerekli paketleri yükler, bir Node.js uygulaması oluşturur sonra başlatmak ve hello uygulama başlatır.</span><span class="sxs-lookup"><span data-stu-id="c58c8-148">hello following cloud-init configuration installs hello required packages, creates a Node.js app, then initialize and starts hello app.</span></span>

<span data-ttu-id="c58c8-149">Geçerli kabuğunuzu adlı bir dosya oluşturun *bulut init.txt* Yapıştır hello izleyerek yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="c58c8-149">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="c58c8-150">Örneğin, yerel makinenizde değil hello bulut Kabuk hello dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c58c8-150">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="c58c8-151">İstediğiniz herhangi bir düzenleyicisini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c58c8-151">You can use any editor you wish.</span></span> <span data-ttu-id="c58c8-152">Girin `sensible-editor cloud-init.txt` toocreate hello dosya ve kullanılabilir düzenleyicileri listesini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c58c8-152">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="c58c8-153">Merhaba tüm bulut init dosyanın doğru şekilde kopyalandığından emin olun, özellikle ilk satırı hello:</span><span class="sxs-lookup"><span data-stu-id="c58c8-153">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

<span data-ttu-id="c58c8-154">Bulut init yapılandırma seçenekleri hakkında daha fazla bilgi için bkz: [bulut init yapılandırma örnekleri](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span><span class="sxs-lookup"><span data-stu-id="c58c8-154">For more information about cloud-init configuration options, see [cloud-init config examples](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="c58c8-155">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="c58c8-155">Create virtual machine</span></span>
<span data-ttu-id="c58c8-156">Bir VM oluşturmadan önce bir kaynak grubuyla oluşturmanız [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="c58c8-156">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="c58c8-157">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroupAutomate* hello içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="c58c8-157">hello following example creates a resource group named *myResourceGroupAutomate* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

<span data-ttu-id="c58c8-158">Şimdi bir VM oluşturmak [az vm oluşturma](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="c58c8-158">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="c58c8-159">Kullanım hello `--custom-data` parametresi toopass bulut init yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="c58c8-159">Use hello `--custom-data` parameter toopass in your cloud-init config file.</span></span> <span data-ttu-id="c58c8-160">Merhaba tam yolu toohello sağlamak *bulut init.txt* mevcut çalışma dizininizi dışında hello dosyasını kaydettiyseniz yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="c58c8-160">Provide hello full path toohello *cloud-init.txt* config if you saved hello file outside of your present working directory.</span></span> <span data-ttu-id="c58c8-161">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myAutomatedVM*:</span><span class="sxs-lookup"><span data-stu-id="c58c8-161">hello following example creates a VM named *myAutomatedVM*:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="c58c8-162">Oluşturulan, hello VM toobe birkaç dakika sürer hello paketleri tooinstall ve hello uygulama toostart.</span><span class="sxs-lookup"><span data-stu-id="c58c8-162">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="c58c8-163">Hello Azure CLI toohello istemi döndükten sonra toorun devam arka plan görevleri vardır.</span><span class="sxs-lookup"><span data-stu-id="c58c8-163">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="c58c8-164">Başka bir birkaç hello uygulamaya erişmek için dakika olabilir.</span><span class="sxs-lookup"><span data-stu-id="c58c8-164">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="c58c8-165">Merhaba VM oluşturduğunuzda hello not edin `publicIpAddress` hello Azure CLI tarafından görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c58c8-165">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="c58c8-166">Kullanılan tooaccess hello Node.js uygulaması bir web tarayıcısı aracılığıyla adresidir.</span><span class="sxs-lookup"><span data-stu-id="c58c8-166">This address is used tooaccess hello Node.js app via a web browser.</span></span>

<span data-ttu-id="c58c8-167">açık bağlantı noktası 80 hello Internet gelen ile VM'nizi tooallow web trafiği tooreach [az vm Aç-port](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="c58c8-167">tooallow web traffic tooreach your VM, open port 80 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a><span data-ttu-id="c58c8-168">Test web uygulaması</span><span class="sxs-lookup"><span data-stu-id="c58c8-168">Test web app</span></span>
<span data-ttu-id="c58c8-169">Bir web tarayıcısı açın ve girin artık *http://<publicIpAddress>*  hello adres çubuğundaki.</span><span class="sxs-lookup"><span data-stu-id="c58c8-169">Now you can open a web browser and enter *http://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="c58c8-170">Kendi ortak sağlamak hello VM IP adresinden oluşturma işlemi.</span><span class="sxs-lookup"><span data-stu-id="c58c8-170">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="c58c8-171">Node.js uygulamanızı aşağıdaki örneğine hello olduğu gibi görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="c58c8-171">Your Node.js app is displayed as in hello following example:</span></span>

![Çalışan NGINX sitesini görüntüle](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a><span data-ttu-id="c58c8-173">Anahtar kasası sertifikaları Ekle</span><span class="sxs-lookup"><span data-stu-id="c58c8-173">Inject certificates from Key Vault</span></span>
<span data-ttu-id="c58c8-174">Bu isteğe bağlı bir bölüm nasıl güvenli bir şekilde Azure anahtar kasası sertifikaları depolamak ve hello VM dağıtımı sırasında Ekle gösterir.</span><span class="sxs-lookup"><span data-stu-id="c58c8-174">This optional section shows how you can securely store certificates in Azure Key Vault and inject them during hello VM deployment.</span></span> <span data-ttu-id="c58c8-175">Merhaba sertifikaları içeren özel bir görüntü kullanarak yerine desteklenmiş, bu işlem hello en güncel sertifikaları tooa VM ilk önyüklemede eklenmiş sağlar.</span><span class="sxs-lookup"><span data-stu-id="c58c8-175">Rather than using a custom image that includes hello certificates baked-in, this process ensures that hello most up-to-date certificates are injected tooa VM on first boot.</span></span> <span data-ttu-id="c58c8-176">Merhaba işlemi sırasında hiçbir zaman hello sertifika hello Azure platformu bırakır veya bir komut dosyası, komut satırı geçmiş veya şablonda sunulur.</span><span class="sxs-lookup"><span data-stu-id="c58c8-176">During hello process, hello certificate never leaves hello Azure platform or is exposed in a script, command-line history, or template.</span></span>

<span data-ttu-id="c58c8-177">Azure anahtar kasası, şifreleme anahtarlarını ve gizli anahtarları, sertifikalar veya parolaları gibi koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="c58c8-177">Azure Key Vault safeguards cryptographic keys and secrets, such as certificates or passwords.</span></span> <span data-ttu-id="c58c8-178">Anahtar kasası hello anahtar yönetimi işlemini kolaylaştırmaya yardımcı olur ve erişmek ve veri şifreleme anahtarları toomaintain denetimini etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="c58c8-178">Key Vault helps streamline hello key management process and enables you toomaintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="c58c8-179">Bu senaryo bazı anahtar kasası kavramları toocreate ve bir sertifika kullan sunar, ancak konusunda kapsamlı bir genel bakış değil toouse anahtar kasası.</span><span class="sxs-lookup"><span data-stu-id="c58c8-179">This scenario introduces some Key Vault concepts toocreate and use a certificate, though is not an exhaustive overview on how toouse Key Vault.</span></span>

<span data-ttu-id="c58c8-180">Aşağıdaki adımları hello nasıl göster:</span><span class="sxs-lookup"><span data-stu-id="c58c8-180">hello following steps show how you can:</span></span>

- <span data-ttu-id="c58c8-181">Azure anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="c58c8-181">Create an Azure Key Vault</span></span>
- <span data-ttu-id="c58c8-182">Oluşturmak veya bir sertifika toohello anahtar kasası karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="c58c8-182">Generate or upload a certificate toohello Key Vault</span></span>
- <span data-ttu-id="c58c8-183">Merhaba sertifika tooinject tooa VM içinde bir gizli anahtar oluşturma</span><span class="sxs-lookup"><span data-stu-id="c58c8-183">Create a secret from hello certificate tooinject in tooa VM</span></span>
- <span data-ttu-id="c58c8-184">Bir VM oluşturun ve hello sertifika Ekle</span><span class="sxs-lookup"><span data-stu-id="c58c8-184">Create a VM and inject hello certificate</span></span>

### <a name="create-an-azure-key-vault"></a><span data-ttu-id="c58c8-185">Azure anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="c58c8-185">Create an Azure Key Vault</span></span>
<span data-ttu-id="c58c8-186">İlk olarak, bir anahtar kasası ile oluşturma [az keyvault oluşturma](/cli/azure/keyvault#create) ve bir VM dağıttığınızda kullanım için etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c58c8-186">First, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="c58c8-187">Her anahtar kasası benzersiz bir ad gerektirir ve tüm küçük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c58c8-187">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="c58c8-188">Değiştir *mykeyvault* kendi benzersiz bir anahtar kasası ad örnekle aşağıdaki hello içinde:</span><span class="sxs-lookup"><span data-stu-id="c58c8-188">Replace *mykeyvault* in hello following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a><span data-ttu-id="c58c8-189">Sertifika oluşturmak ve anahtar kasasına depolamak</span><span class="sxs-lookup"><span data-stu-id="c58c8-189">Generate certificate and store in Key Vault</span></span>
<span data-ttu-id="c58c8-190">Üretim kullanımı için güvenilen bir sağlayıcı tarafından imzalanmış geçerli bir sertifika almanız gerekir [az keyvault sertifika alma](/cli/azure/keyvault/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="c58c8-190">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/keyvault/certificate#import).</span></span> <span data-ttu-id="c58c8-191">Bu öğretici için hello aşağıdaki örnek otomatik olarak imzalanan bir sertifika ile nasıl oluşturabileceğiniz gösterir [az keyvault sertifika oluştur](/cli/azure/keyvault/certificate#create) hello varsayılan sertifika ilkesi kullanır:</span><span class="sxs-lookup"><span data-stu-id="c58c8-191">For this tutorial, hello following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/keyvault/certificate#create) that uses hello default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a><span data-ttu-id="c58c8-192">VM ile kullanmak için sertifika hazırlama</span><span class="sxs-lookup"><span data-stu-id="c58c8-192">Prepare certificate for use with VM</span></span>
<span data-ttu-id="c58c8-193">toouse hello sertifika hello VM sırasında işlem oluşturma, sertifikanızla hello kimliği elde [az keyvault gizli listesi sürümleri](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="c58c8-193">toouse hello certificate during hello VM create process, obtain hello ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="c58c8-194">Merhaba VM hello sertifika gereken belirli bir biçim tooinject önyüklemede, bu nedenle dönüştürmeden hello sertifikayla [az vm biçimi-gizli](/cli/azure/vm#format-secret).</span><span class="sxs-lookup"><span data-stu-id="c58c8-194">hello VM needs hello certificate in a certain format tooinject it on boot, so convert hello certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="c58c8-195">Aşağıdaki örnek hello hello kullanım kolaylığı için bu komutları toovariables hello çıktısını sonraki adımlar atar:</span><span class="sxs-lookup"><span data-stu-id="c58c8-195">hello following example assigns hello output of these commands toovariables for ease of use in hello next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-toosecure-nginx"></a><span data-ttu-id="c58c8-196">Bulut init config toosecure NGINX oluşturma</span><span class="sxs-lookup"><span data-stu-id="c58c8-196">Create cloud-init config toosecure NGINX</span></span>
<span data-ttu-id="c58c8-197">VM, sertifikaları oluşturduğunuzda ve anahtarlar, korumalı hello depolanır */var/lib/waagent/* dizin.</span><span class="sxs-lookup"><span data-stu-id="c58c8-197">When you create a VM, certificates and keys are stored in hello protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="c58c8-198">tooautomate ekleme hello sertifika toohello VM ve NGINX yapılandırma, güncelleştirilmiş bulut init config hello önceki örnekteki kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c58c8-198">tooautomate adding hello certificate toohello VM and configuring NGINX, you can use an updated cloud-init config from hello previous example.</span></span>

<span data-ttu-id="c58c8-199">Adlı bir dosya oluşturun *bulut init secured.txt* Yapıştır hello izleyerek yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="c58c8-199">Create a file named *cloud-init-secured.txt* and paste hello following configuration.</span></span> <span data-ttu-id="c58c8-200">Yeniden hello bulut Kabuğu'nu kullanırsanız, hello bulut init yapılandırma dosyası yok ve yerel makinenizde değil oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c58c8-200">Again, if you use hello Cloud Shell, create hello cloud-init config file there and not on your local machine.</span></span> <span data-ttu-id="c58c8-201">Kullanım `sensible-editor cloud-init-secured.txt` toocreate hello dosya ve kullanılabilir düzenleyicileri listesini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c58c8-201">Use `sensible-editor cloud-init-secured.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="c58c8-202">Merhaba tüm bulut init dosyanın doğru şekilde kopyalandığından emin olun, özellikle ilk satırı hello:</span><span class="sxs-lookup"><span data-stu-id="c58c8-202">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-secure-vm"></a><span data-ttu-id="c58c8-203">Güvenli VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="c58c8-203">Create secure VM</span></span>
<span data-ttu-id="c58c8-204">Şimdi bir VM oluşturmak [az vm oluşturma](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="c58c8-204">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="c58c8-205">Merhaba sertifika verileri ile Merhaba anahtar Kasası'nı eklenen `--secrets` parametresi.</span><span class="sxs-lookup"><span data-stu-id="c58c8-205">hello certificate data is injected from Key Vault with hello `--secrets` parameter.</span></span> <span data-ttu-id="c58c8-206">Merhaba önceki örnekte olduğu gibi aynı zamanda hello bulut init config hello ile geçirdiğiniz `--custom-data` parametre:</span><span class="sxs-lookup"><span data-stu-id="c58c8-206">As in hello previous example, you also pass in hello cloud-init config with hello `--custom-data` parameter:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-secured.txt \
    --secrets "$vm_secret"
```

<span data-ttu-id="c58c8-207">Oluşturulan, hello VM toobe birkaç dakika sürer hello paketleri tooinstall ve hello uygulama toostart.</span><span class="sxs-lookup"><span data-stu-id="c58c8-207">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="c58c8-208">Hello Azure CLI toohello istemi döndükten sonra toorun devam arka plan görevleri vardır.</span><span class="sxs-lookup"><span data-stu-id="c58c8-208">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="c58c8-209">Başka bir birkaç hello uygulamaya erişmek için dakika olabilir.</span><span class="sxs-lookup"><span data-stu-id="c58c8-209">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="c58c8-210">Merhaba VM oluşturduğunuzda hello not edin `publicIpAddress` hello Azure CLI tarafından görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c58c8-210">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="c58c8-211">Kullanılan tooaccess hello Node.js uygulaması bir web tarayıcısı aracılığıyla adresidir.</span><span class="sxs-lookup"><span data-stu-id="c58c8-211">This address is used tooaccess hello Node.js app via a web browser.</span></span>

<span data-ttu-id="c58c8-212">açık bağlantı noktası 443 hello Internet gelen ile VM'nizi tooallow güvenli web trafiği tooreach [az vm Aç-port](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="c58c8-212">tooallow secure web traffic tooreach your VM, open port 443 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a><span data-ttu-id="c58c8-213">Test güvenli web uygulaması</span><span class="sxs-lookup"><span data-stu-id="c58c8-213">Test secure web app</span></span>
<span data-ttu-id="c58c8-214">Bir web tarayıcısı açın ve girin artık *https://<publicIpAddress>*  hello adres çubuğundaki.</span><span class="sxs-lookup"><span data-stu-id="c58c8-214">Now you can open a web browser and enter *https://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="c58c8-215">Kendi ortak sağlamak hello VM IP adresinden oluşturma işlemi.</span><span class="sxs-lookup"><span data-stu-id="c58c8-215">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="c58c8-216">Kendinden imzalı bir sertifika kullanılması durumunda hello güvenlik uyarısı kabul edin:</span><span class="sxs-lookup"><span data-stu-id="c58c8-216">Accept hello security warning if you used a self-signed certificate:</span></span>

![Web tarayıcısı güvenlik uyarısını kabul edin](./media/tutorial-automate-vm-deployment/browser-warning.png)

<span data-ttu-id="c58c8-218">Güvenli NGINX siteniz ve Node.js uygulaması ardından aşağıdaki örneğine hello olduğu gibi görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="c58c8-218">Your secured NGINX site and Node.js app is then displayed as in hello following example:</span></span>

![Çalışan güvenli NGINX sitesini görüntüle](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="c58c8-220">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c58c8-220">Next steps</span></span>
<span data-ttu-id="c58c8-221">Bu öğreticide, VM'ler ilk önyüklemesi bulut init ile yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="c58c8-221">In this tutorial, you configured VMs on first boot with cloud-init.</span></span> <span data-ttu-id="c58c8-222">Şunları öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="c58c8-222">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c58c8-223">Bir bulut init yapılandırma dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="c58c8-223">Create a cloud-init config file</span></span>
> * <span data-ttu-id="c58c8-224">Bir bulut init dosyası kullanan bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="c58c8-224">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="c58c8-225">Merhaba VM oluşturulduktan sonra çalışan bir Node.js uygulaması görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="c58c8-225">View a running Node.js app after hello VM is created</span></span>
> * <span data-ttu-id="c58c8-226">Anahtar kasası toosecurely deposu sertifikaları kullanma</span><span class="sxs-lookup"><span data-stu-id="c58c8-226">Use Key Vault toosecurely store certificates</span></span>
> * <span data-ttu-id="c58c8-227">Güvenli NGINX dağıtımlarında bulut init otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="c58c8-227">Automate secure deployments of NGINX with cloud-init</span></span>

<span data-ttu-id="c58c8-228">Toohello sonraki öğretici toolearn nasıl ilerlemek toocreate özel VM görüntüler.</span><span class="sxs-lookup"><span data-stu-id="c58c8-228">Advance toohello next tutorial toolearn how toocreate custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c58c8-229">Özel VM görüntüleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="c58c8-229">Create custom VM images</span></span>](./tutorial-custom-images.md)
