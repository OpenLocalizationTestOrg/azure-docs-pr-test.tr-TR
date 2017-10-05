---
title: "İlk önyükleme azure'da bir Linux VM özelleştirme | Microsoft Docs"
description: "Bulut Init ve anahtar kasası customze Linux VM'ler için Azure'da önyükleme ilk kez kullanmayı öğrenin"
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
ms.openlocfilehash: 6adf4e43aa80c28c6f5f8d8a071966323ba85723
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-customize-a-linux-virtual-machine-on-first-boot"></a><span data-ttu-id="2db1e-103">İlk önyükleme Linux sanal makine özelleştirme</span><span class="sxs-lookup"><span data-stu-id="2db1e-103">How to customize a Linux virtual machine on first boot</span></span>
<span data-ttu-id="2db1e-104">Bir önceki öğreticide öğrenilen nasıl NGINX SSH bir sanal makine (VM) ve el ile yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2db1e-104">In a previous tutorial, you learned how to SSH to a virtual machine (VM) and manually install NGINX.</span></span> <span data-ttu-id="2db1e-105">VM'ler hızlı ve tutarlı bir şekilde oluşturmak için tür Otomasyon genellikle istendiğini.</span><span class="sxs-lookup"><span data-stu-id="2db1e-105">To create VMs in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="2db1e-106">İlk önyükleme bir VM özelleştirmek için ortak bir yaklaşım kullanmaktır [bulut init](https://cloudinit.readthedocs.io).</span><span class="sxs-lookup"><span data-stu-id="2db1e-106">A common approach to customize a VM on first boot is to use [cloud-init](https://cloudinit.readthedocs.io).</span></span> <span data-ttu-id="2db1e-107">Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2db1e-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2db1e-108">Bir bulut init yapılandırma dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="2db1e-108">Create a cloud-init config file</span></span>
> * <span data-ttu-id="2db1e-109">Bir bulut init dosyası kullanan bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="2db1e-109">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="2db1e-110">VM oluşturulduktan sonra çalışan bir Node.js uygulaması görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="2db1e-110">View a running Node.js app after the VM is created</span></span>
> * <span data-ttu-id="2db1e-111">Sertifikaları güvenli bir şekilde anahtar kasası kullanın</span><span class="sxs-lookup"><span data-stu-id="2db1e-111">Use Key Vault to securely store certificates</span></span>
> * <span data-ttu-id="2db1e-112">Güvenli NGINX dağıtımlarında bulut init otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="2db1e-112">Automate secure deployments of NGINX with cloud-init</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2db1e-113">Yüklemek ve CLI yerel olarak kullanmak seçerseniz, Bu öğretici, Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="2db1e-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="2db1e-114">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2db1e-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="2db1e-115">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2db1e-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  



## <a name="cloud-init-overview"></a><span data-ttu-id="2db1e-116">Bulut init genel bakış</span><span class="sxs-lookup"><span data-stu-id="2db1e-116">Cloud-init overview</span></span>
<span data-ttu-id="2db1e-117">[Bulut init](https://cloudinit.readthedocs.io) ilk kez önyükleme gibi bir Linux VM özelleştirmek için yaygın olarak kullanılan bir yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="2db1e-117">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach to customize a Linux VM as it boots for the first time.</span></span> <span data-ttu-id="2db1e-118">Bulut init paketleri yüklemek ve dosyaları yazma veya kullanıcılar ve güvenlik yapılandırmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2db1e-118">You can use cloud-init to install packages and write files, or to configure users and security.</span></span> <span data-ttu-id="2db1e-119">Bulut init ilk önyükleme işlemi sırasında çalışırken, ek adımlar veya yapılandırmanızı uygulamak için gerekli aracıların yok.</span><span class="sxs-lookup"><span data-stu-id="2db1e-119">As cloud-init runs during the initial boot process, there are no additional steps or required agents to apply your configuration.</span></span>

<span data-ttu-id="2db1e-120">Bulut init dağıtımları üzerinde de çalışır.</span><span class="sxs-lookup"><span data-stu-id="2db1e-120">Cloud-init also works across distributions.</span></span> <span data-ttu-id="2db1e-121">Örneğin, kullanmadığınız **get apt yükleme** veya **yum yükleme** bir paketi yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="2db1e-121">For example, you don't use **apt-get install** or **yum install** to install a package.</span></span> <span data-ttu-id="2db1e-122">Bunun yerine, yüklemek için paketlerin listesini tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2db1e-122">Instead you can define a list of packages to install.</span></span> <span data-ttu-id="2db1e-123">Bulut init otomatik olarak seçtiğiniz distro için yerel paket Yönetim Aracı'nı kullanır.</span><span class="sxs-lookup"><span data-stu-id="2db1e-123">Cloud-init automatically uses the native package management tool for the distro you select.</span></span>

<span data-ttu-id="2db1e-124">Bulut dahil ve Azure'a sağladıkları görüntülerinde çalışma başlatma almak için ortaklarımızın ile çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="2db1e-124">We are working with our partners to get cloud-init included and working in the images that they provide to Azure.</span></span> <span data-ttu-id="2db1e-125">Aşağıdaki tabloda Azure platform görüntüleri geçerli bulut init kullanılabilirliğine özetlenmektedir:</span><span class="sxs-lookup"><span data-stu-id="2db1e-125">The following table outlines the current cloud-init availability on Azure platform images:</span></span>

| <span data-ttu-id="2db1e-126">Diğer ad</span><span class="sxs-lookup"><span data-stu-id="2db1e-126">Alias</span></span> | <span data-ttu-id="2db1e-127">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="2db1e-127">Publisher</span></span> | <span data-ttu-id="2db1e-128">Sunduğu</span><span class="sxs-lookup"><span data-stu-id="2db1e-128">Offer</span></span> | <span data-ttu-id="2db1e-129">SKU</span><span class="sxs-lookup"><span data-stu-id="2db1e-129">SKU</span></span> | <span data-ttu-id="2db1e-130">Sürüm</span><span class="sxs-lookup"><span data-stu-id="2db1e-130">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="2db1e-131">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="2db1e-131">UbuntuLTS</span></span> |<span data-ttu-id="2db1e-132">Canonical</span><span class="sxs-lookup"><span data-stu-id="2db1e-132">Canonical</span></span> |<span data-ttu-id="2db1e-133">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="2db1e-133">UbuntuServer</span></span> |<span data-ttu-id="2db1e-134">16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="2db1e-134">16.04-LTS</span></span> |<span data-ttu-id="2db1e-135">en son</span><span class="sxs-lookup"><span data-stu-id="2db1e-135">latest</span></span> |
| <span data-ttu-id="2db1e-136">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="2db1e-136">UbuntuLTS</span></span> |<span data-ttu-id="2db1e-137">Canonical</span><span class="sxs-lookup"><span data-stu-id="2db1e-137">Canonical</span></span> |<span data-ttu-id="2db1e-138">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="2db1e-138">UbuntuServer</span></span> |<span data-ttu-id="2db1e-139">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="2db1e-139">14.04.5-LTS</span></span> |<span data-ttu-id="2db1e-140">en son</span><span class="sxs-lookup"><span data-stu-id="2db1e-140">latest</span></span> |
| <span data-ttu-id="2db1e-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="2db1e-141">CoreOS</span></span> |<span data-ttu-id="2db1e-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="2db1e-142">CoreOS</span></span> |<span data-ttu-id="2db1e-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="2db1e-143">CoreOS</span></span> |<span data-ttu-id="2db1e-144">Dengeli</span><span class="sxs-lookup"><span data-stu-id="2db1e-144">Stable</span></span> |<span data-ttu-id="2db1e-145">en son</span><span class="sxs-lookup"><span data-stu-id="2db1e-145">latest</span></span> |


## <a name="create-cloud-init-config-file"></a><span data-ttu-id="2db1e-146">Bulut init yapılandırma dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="2db1e-146">Create cloud-init config file</span></span>
<span data-ttu-id="2db1e-147">Bulut-init uygulamada görmek için NGINX yükler ve bir basit 'Hello World' Node.js uygulaması çalıştıran bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2db1e-147">To see cloud-init in action, create a VM that installs NGINX and runs a simple 'Hello World' Node.js app.</span></span> <span data-ttu-id="2db1e-148">Aşağıdaki bulut init yapılandırma gerekli paketleri yükler, bir Node.js uygulaması oluşturur sonra başlatmak ve uygulamayı başlatır.</span><span class="sxs-lookup"><span data-stu-id="2db1e-148">The following cloud-init configuration installs the required packages, creates a Node.js app, then initialize and starts the app.</span></span>

<span data-ttu-id="2db1e-149">Geçerli kabuğunuzu adlı bir dosya oluşturun *bulut init.txt* ve aşağıdaki yapılandırma yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="2db1e-149">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="2db1e-150">Örneğin, yerel makinenizde olmayan bulut kabuğunda dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2db1e-150">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="2db1e-151">İstediğiniz herhangi bir düzenleyicisini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2db1e-151">You can use any editor you wish.</span></span> <span data-ttu-id="2db1e-152">Girin `sensible-editor cloud-init.txt` dosyası oluşturun ve kullanılabilir düzenleyicileri listesini görmek için.</span><span class="sxs-lookup"><span data-stu-id="2db1e-152">Enter `sensible-editor cloud-init.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="2db1e-153">Tüm bulut init dosyanın doğru şekilde kopyalandığından emin olun özellikle ilk satırı:</span><span class="sxs-lookup"><span data-stu-id="2db1e-153">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

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

<span data-ttu-id="2db1e-154">Bulut init yapılandırma seçenekleri hakkında daha fazla bilgi için bkz: [bulut init yapılandırma örnekleri](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span><span class="sxs-lookup"><span data-stu-id="2db1e-154">For more information about cloud-init configuration options, see [cloud-init config examples](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="2db1e-155">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="2db1e-155">Create virtual machine</span></span>
<span data-ttu-id="2db1e-156">Bir VM oluşturmadan önce bir kaynak grubuyla oluşturmanız [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="2db1e-156">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="2db1e-157">Aşağıdaki örnek, bir kaynak grubu oluşturur *myResourceGroupAutomate* içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="2db1e-157">The following example creates a resource group named *myResourceGroupAutomate* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

<span data-ttu-id="2db1e-158">Şimdi bir VM oluşturmak [az vm oluşturma](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="2db1e-158">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="2db1e-159">Kullanım `--custom-data` bulut init yapılandırma dosyanızda geçirmek için parametre.</span><span class="sxs-lookup"><span data-stu-id="2db1e-159">Use the `--custom-data` parameter to pass in your cloud-init config file.</span></span> <span data-ttu-id="2db1e-160">Tam yolunu belirtmeniz *bulut init.txt* mevcut çalışma dizininizi dışında dosyasını kaydettiyseniz yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="2db1e-160">Provide the full path to the *cloud-init.txt* config if you saved the file outside of your present working directory.</span></span> <span data-ttu-id="2db1e-161">Aşağıdaki örnek, adlandırılmış bir VM'nin oluşturur *myAutomatedVM*:</span><span class="sxs-lookup"><span data-stu-id="2db1e-161">The following example creates a VM named *myAutomatedVM*:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="2db1e-162">Oluşturulacak VM, yüklemek için paketleri ve uygulamayı başlatmak için birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="2db1e-162">It takes a few minutes for the VM to be created, the packages to install, and the app to start.</span></span> <span data-ttu-id="2db1e-163">Azure CLI sorusu döndükten sonra çalışmaya devam arka plan görevleri vardır.</span><span class="sxs-lookup"><span data-stu-id="2db1e-163">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="2db1e-164">Başka bir birkaç uygulamaya erişmek için dakika olabilir.</span><span class="sxs-lookup"><span data-stu-id="2db1e-164">It may be another couple of minutes before you can access the app.</span></span> <span data-ttu-id="2db1e-165">VM oluşturduğunuzda not edin `publicIpAddress` Azure CLI tarafından görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="2db1e-165">When the VM has been created, take note of the `publicIpAddress` displayed by the Azure CLI.</span></span> <span data-ttu-id="2db1e-166">Bu adres, Node.js uygulaması bir web tarayıcısı aracılığıyla erişmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2db1e-166">This address is used to access the Node.js app via a web browser.</span></span>

<span data-ttu-id="2db1e-167">Bağlantı noktası 80 Internet'ten açın, VM ulaşmak web trafiğe izin verecek şekilde [az vm Aç-port](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="2db1e-167">To allow web traffic to reach your VM, open port 80 from the Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a><span data-ttu-id="2db1e-168">Test web uygulaması</span><span class="sxs-lookup"><span data-stu-id="2db1e-168">Test web app</span></span>
<span data-ttu-id="2db1e-169">Bir web tarayıcısı açın ve girin artık *http://<publicIpAddress>*  adres çubuğundaki.</span><span class="sxs-lookup"><span data-stu-id="2db1e-169">Now you can open a web browser and enter *http://<publicIpAddress>* in the address bar.</span></span> <span data-ttu-id="2db1e-170">Kendi ortak sağlamak VM IP adresinden oluşturma işlemi.</span><span class="sxs-lookup"><span data-stu-id="2db1e-170">Provide your own public IP address from the VM create process.</span></span> <span data-ttu-id="2db1e-171">Node.js uygulamanızı aşağıdaki örnekte olduğu gibi görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="2db1e-171">Your Node.js app is displayed as in the following example:</span></span>

![Çalışan NGINX sitesini görüntüle](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a><span data-ttu-id="2db1e-173">Anahtar kasası sertifikaları Ekle</span><span class="sxs-lookup"><span data-stu-id="2db1e-173">Inject certificates from Key Vault</span></span>
<span data-ttu-id="2db1e-174">Bu isteğe bağlı bir bölüm nasıl güvenli bir şekilde Azure anahtar kasası sertifikaları depolamak ve VM dağıtımı sırasında Ekle gösterir.</span><span class="sxs-lookup"><span data-stu-id="2db1e-174">This optional section shows how you can securely store certificates in Azure Key Vault and inject them during the VM deployment.</span></span> <span data-ttu-id="2db1e-175">Sertifikaları içeren özel bir görüntü kullanarak yerine desteklenmiş, bu işlem en güncel sertifikaları ilk önyükleme üzerinde bir VM eklenmiş sağlar.</span><span class="sxs-lookup"><span data-stu-id="2db1e-175">Rather than using a custom image that includes the certificates baked-in, this process ensures that the most up-to-date certificates are injected to a VM on first boot.</span></span> <span data-ttu-id="2db1e-176">İşlemi sırasında sertifika hiçbir zaman Azure platformu bırakır veya bir komut dosyası, komut satırı geçmiş veya şablonda sunulur.</span><span class="sxs-lookup"><span data-stu-id="2db1e-176">During the process, the certificate never leaves the Azure platform or is exposed in a script, command-line history, or template.</span></span>

<span data-ttu-id="2db1e-177">Azure anahtar kasası, şifreleme anahtarlarını ve gizli anahtarları, sertifikalar veya parolaları gibi koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="2db1e-177">Azure Key Vault safeguards cryptographic keys and secrets, such as certificates or passwords.</span></span> <span data-ttu-id="2db1e-178">Anahtar kasası anahtar yönetimi işlemini kolaylaştırmaya yardımcı olur ve erişmek ve veri şifreleme anahtarları denetim kurmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="2db1e-178">Key Vault helps streamline the key management process and enables you to maintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="2db1e-179">Bu senaryo oluşturmak ve bir sertifika kullanmak için bazı anahtar kasası kavramları tanıtır, ancak anahtar kasası kullanma hakkında ayrıntılı bir genel bakış değildir.</span><span class="sxs-lookup"><span data-stu-id="2db1e-179">This scenario introduces some Key Vault concepts to create and use a certificate, though is not an exhaustive overview on how to use Key Vault.</span></span>

<span data-ttu-id="2db1e-180">Aşağıdaki adımlar, nasıl gösterir:</span><span class="sxs-lookup"><span data-stu-id="2db1e-180">The following steps show how you can:</span></span>

- <span data-ttu-id="2db1e-181">Azure anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="2db1e-181">Create an Azure Key Vault</span></span>
- <span data-ttu-id="2db1e-182">Oluşturmak veya bir sertifika anahtar Kasası'na Karşıya Yükle</span><span class="sxs-lookup"><span data-stu-id="2db1e-182">Generate or upload a certificate to the Key Vault</span></span>
- <span data-ttu-id="2db1e-183">Bir VM içinde eklemesine sertifikasından gizli anahtar oluşturma</span><span class="sxs-lookup"><span data-stu-id="2db1e-183">Create a secret from the certificate to inject in to a VM</span></span>
- <span data-ttu-id="2db1e-184">Bir VM oluşturun ve sertifika Ekle</span><span class="sxs-lookup"><span data-stu-id="2db1e-184">Create a VM and inject the certificate</span></span>

### <a name="create-an-azure-key-vault"></a><span data-ttu-id="2db1e-185">Azure anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="2db1e-185">Create an Azure Key Vault</span></span>
<span data-ttu-id="2db1e-186">İlk olarak, bir anahtar kasası ile oluşturma [az keyvault oluşturma](/cli/azure/keyvault#create) ve bir VM dağıttığınızda kullanım için etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2db1e-186">First, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="2db1e-187">Her anahtar kasası benzersiz bir ad gerektirir ve tüm küçük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2db1e-187">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="2db1e-188">Değiştir *mykeyvault* aşağıdaki örnekte kendi benzersiz bir anahtar kasası ad ile:</span><span class="sxs-lookup"><span data-stu-id="2db1e-188">Replace *mykeyvault* in the following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a><span data-ttu-id="2db1e-189">Sertifika oluşturmak ve anahtar kasasına depolamak</span><span class="sxs-lookup"><span data-stu-id="2db1e-189">Generate certificate and store in Key Vault</span></span>
<span data-ttu-id="2db1e-190">Üretim kullanımı için güvenilen bir sağlayıcı tarafından imzalanmış geçerli bir sertifika almanız gerekir [az keyvault sertifika alma](/cli/azure/keyvault/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="2db1e-190">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/keyvault/certificate#import).</span></span> <span data-ttu-id="2db1e-191">Bu öğretici için aşağıdaki örnek, otomatik olarak imzalanan bir sertifika ile nasıl oluşturabileceğiniz gösterir [az keyvault sertifika oluştur](/cli/azure/keyvault/certificate#create) varsayılan sertifika ilkesi kullanır:</span><span class="sxs-lookup"><span data-stu-id="2db1e-191">For this tutorial, the following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/keyvault/certificate#create) that uses the default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a><span data-ttu-id="2db1e-192">VM ile kullanmak için sertifika hazırlama</span><span class="sxs-lookup"><span data-stu-id="2db1e-192">Prepare certificate for use with VM</span></span>
<span data-ttu-id="2db1e-193">VM sırasında sertifikayı kullanmak üzere işlem oluşturma, sertifikanızla kimliği elde [az keyvault gizli listesi sürümleri](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="2db1e-193">To use the certificate during the VM create process, obtain the ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="2db1e-194">VM önyüklemede ekleme, böylece sertifikayla dönüştürmek için belirli bir biçimde sertifikanın gerekir [az vm biçimi-gizli](/cli/azure/vm#format-secret).</span><span class="sxs-lookup"><span data-stu-id="2db1e-194">The VM needs the certificate in a certain format to inject it on boot, so convert the certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="2db1e-195">Aşağıdaki örnek sonraki adımlarda kullanım kolaylığı için değişkenleri bu komutların çıktısı atar:</span><span class="sxs-lookup"><span data-stu-id="2db1e-195">The following example assigns the output of these commands to variables for ease of use in the next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-to-secure-nginx"></a><span data-ttu-id="2db1e-196">NGINX güvenli hale getirmek için bulut init yapılandırma oluşturma</span><span class="sxs-lookup"><span data-stu-id="2db1e-196">Create cloud-init config to secure NGINX</span></span>
<span data-ttu-id="2db1e-197">VM, sertifikaları oluşturduğunuzda ve anahtarlar depolanır korumalı içinde */var/lib/waagent/* dizin.</span><span class="sxs-lookup"><span data-stu-id="2db1e-197">When you create a VM, certificates and keys are stored in the protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="2db1e-198">Sertifika VM ekleme ve NGINX yapılandırma otomatikleştirmek için güncelleştirilmiş bulut init config önceki örnekten kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2db1e-198">To automate adding the certificate to the VM and configuring NGINX, you can use an updated cloud-init config from the previous example.</span></span>

<span data-ttu-id="2db1e-199">Adlı bir dosya oluşturun *bulut init secured.txt* ve aşağıdaki yapılandırma yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="2db1e-199">Create a file named *cloud-init-secured.txt* and paste the following configuration.</span></span> <span data-ttu-id="2db1e-200">Yeniden bulut Kabuğu'nu kullanırsanız, bulut init yapılandırma dosyası yok ve yerel makinenizde değil oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2db1e-200">Again, if you use the Cloud Shell, create the cloud-init config file there and not on your local machine.</span></span> <span data-ttu-id="2db1e-201">Kullanım `sensible-editor cloud-init-secured.txt` dosyası oluşturun ve kullanılabilir düzenleyicileri listesini görmek için.</span><span class="sxs-lookup"><span data-stu-id="2db1e-201">Use `sensible-editor cloud-init-secured.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="2db1e-202">Tüm bulut init dosyanın doğru şekilde kopyalandığından emin olun özellikle ilk satırı:</span><span class="sxs-lookup"><span data-stu-id="2db1e-202">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

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

### <a name="create-secure-vm"></a><span data-ttu-id="2db1e-203">Güvenli VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="2db1e-203">Create secure VM</span></span>
<span data-ttu-id="2db1e-204">Şimdi bir VM oluşturmak [az vm oluşturma](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="2db1e-204">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="2db1e-205">Sertifika verileri ile anahtar Kasası'ndan eklenen `--secrets` parametresi.</span><span class="sxs-lookup"><span data-stu-id="2db1e-205">The certificate data is injected from Key Vault with the `--secrets` parameter.</span></span> <span data-ttu-id="2db1e-206">Önceki örnekte olduğu gibi aynı zamanda bulut init config ile geçirdiğiniz `--custom-data` parametre:</span><span class="sxs-lookup"><span data-stu-id="2db1e-206">As in the previous example, you also pass in the cloud-init config with the `--custom-data` parameter:</span></span>

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

<span data-ttu-id="2db1e-207">Oluşturulacak VM, yüklemek için paketleri ve uygulamayı başlatmak için birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="2db1e-207">It takes a few minutes for the VM to be created, the packages to install, and the app to start.</span></span> <span data-ttu-id="2db1e-208">Azure CLI sorusu döndükten sonra çalışmaya devam arka plan görevleri vardır.</span><span class="sxs-lookup"><span data-stu-id="2db1e-208">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="2db1e-209">Başka bir birkaç uygulamaya erişmek için dakika olabilir.</span><span class="sxs-lookup"><span data-stu-id="2db1e-209">It may be another couple of minutes before you can access the app.</span></span> <span data-ttu-id="2db1e-210">VM oluşturduğunuzda not edin `publicIpAddress` Azure CLI tarafından görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="2db1e-210">When the VM has been created, take note of the `publicIpAddress` displayed by the Azure CLI.</span></span> <span data-ttu-id="2db1e-211">Bu adres, Node.js uygulaması bir web tarayıcısı aracılığıyla erişmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2db1e-211">This address is used to access the Node.js app via a web browser.</span></span>

<span data-ttu-id="2db1e-212">VM ulaşmak güvenli web trafiği izin vermek için 443 numaralı bağlantı noktasını Internet'ten gelen ile açmayı [az vm Aç-port](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="2db1e-212">To allow secure web traffic to reach your VM, open port 443 from the Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a><span data-ttu-id="2db1e-213">Test güvenli web uygulaması</span><span class="sxs-lookup"><span data-stu-id="2db1e-213">Test secure web app</span></span>
<span data-ttu-id="2db1e-214">Bir web tarayıcısı açın ve girin artık *https://<publicIpAddress>*  adres çubuğundaki.</span><span class="sxs-lookup"><span data-stu-id="2db1e-214">Now you can open a web browser and enter *https://<publicIpAddress>* in the address bar.</span></span> <span data-ttu-id="2db1e-215">Kendi ortak sağlamak VM IP adresinden oluşturma işlemi.</span><span class="sxs-lookup"><span data-stu-id="2db1e-215">Provide your own public IP address from the VM create process.</span></span> <span data-ttu-id="2db1e-216">Kendinden imzalı bir sertifika kullanılması durumunda güvenlik uyarısı kabul edin:</span><span class="sxs-lookup"><span data-stu-id="2db1e-216">Accept the security warning if you used a self-signed certificate:</span></span>

![Web tarayıcısı güvenlik uyarısını kabul edin](./media/tutorial-automate-vm-deployment/browser-warning.png)

<span data-ttu-id="2db1e-218">Güvenli NGINX siteniz ve Node.js uygulaması ardından aşağıdaki örnekte olduğu gibi görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="2db1e-218">Your secured NGINX site and Node.js app is then displayed as in the following example:</span></span>

![Çalışan güvenli NGINX sitesini görüntüle](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="2db1e-220">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2db1e-220">Next steps</span></span>
<span data-ttu-id="2db1e-221">Bu öğreticide, VM'ler ilk önyüklemesi bulut init ile yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="2db1e-221">In this tutorial, you configured VMs on first boot with cloud-init.</span></span> <span data-ttu-id="2db1e-222">Size nasıl öğrenilen için:</span><span class="sxs-lookup"><span data-stu-id="2db1e-222">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2db1e-223">Bir bulut init yapılandırma dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="2db1e-223">Create a cloud-init config file</span></span>
> * <span data-ttu-id="2db1e-224">Bir bulut init dosyası kullanan bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="2db1e-224">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="2db1e-225">VM oluşturulduktan sonra çalışan bir Node.js uygulaması görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="2db1e-225">View a running Node.js app after the VM is created</span></span>
> * <span data-ttu-id="2db1e-226">Sertifikaları güvenli bir şekilde anahtar kasası kullanın</span><span class="sxs-lookup"><span data-stu-id="2db1e-226">Use Key Vault to securely store certificates</span></span>
> * <span data-ttu-id="2db1e-227">Güvenli NGINX dağıtımlarında bulut init otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="2db1e-227">Automate secure deployments of NGINX with cloud-init</span></span>

<span data-ttu-id="2db1e-228">Özel VM görüntüleri oluşturma hakkında bilgi almak için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="2db1e-228">Advance to the next tutorial to learn how to create custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2db1e-229">Özel VM görüntüleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="2db1e-229">Create custom VM images</span></span>](./tutorial-custom-images.md)
