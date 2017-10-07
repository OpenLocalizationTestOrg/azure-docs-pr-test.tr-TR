---
title: "aaaCreate Linux Azure için sanal makine ölçek kümeleri | Microsoft Docs"
description: "Bir sanal makine ölçek kümesini kullanarak Linux VM'ler üzerinde yüksek oranda kullanılabilir bir uygulama oluşturun ve dağıtın"
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.openlocfilehash: 00dd81043f9be46ef2dc6dfe97eefdb20944ee13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a><span data-ttu-id="008a8-103">Bir sanal makine ölçek kümesi oluşturma ve Linux üzerinde yüksek oranda kullanılabilir bir uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="008a8-103">Create a Virtual Machine Scale Set and deploy a highly available app on Linux</span></span>
<span data-ttu-id="008a8-104">Bir sanal makine ölçek kümesi toodeploy sağlar ve aynı, otomatik ölçeklendirme sanal makineler kümesi yönetin.</span><span class="sxs-lookup"><span data-stu-id="008a8-104">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="008a8-105">Merhaba hello ölçek kümesindeki VM'lerin sayısını elle ölçeklendirme ya da CPU kullanımı, bellek isteğe bağlı veya ağ trafiğini dayalı kurallar tooautoscale tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="008a8-105">You can scale hello number of VMs in hello scale set manually, or define rules tooautoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="008a8-106">Bu öğreticide, Azure üzerinde ayarlanmış bir sanal makine ölçek dağıtın.</span><span class="sxs-lookup"><span data-stu-id="008a8-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="008a8-107">Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="008a8-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="008a8-108">Bulut init toocreate bir uygulama tooscale kullanın</span><span class="sxs-lookup"><span data-stu-id="008a8-108">Use cloud-init toocreate an app tooscale</span></span>
> * <span data-ttu-id="008a8-109">Bir sanal makine ölçek kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="008a8-109">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="008a8-110">Artırma veya azaltma hello ölçek kümesi örneği sayısı</span><span class="sxs-lookup"><span data-stu-id="008a8-110">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="008a8-111">Ölçek kümesi örnekleri için bağlantı bilgileri görüntüle</span><span class="sxs-lookup"><span data-stu-id="008a8-111">View connection info for scale set instances</span></span>
> * <span data-ttu-id="008a8-112">Veri diskleri bir ölçek kümesinde kullanın</span><span class="sxs-lookup"><span data-stu-id="008a8-112">Use data disks in a scale set</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="008a8-113">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="008a8-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="008a8-114">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="008a8-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="008a8-115">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="008a8-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="scale-set-overview"></a><span data-ttu-id="008a8-116">Ölçek kümesi'ne genel bakış</span><span class="sxs-lookup"><span data-stu-id="008a8-116">Scale Set overview</span></span>
<span data-ttu-id="008a8-117">Bir sanal makine ölçek kümesi toodeploy sağlar ve aynı, otomatik ölçeklendirme sanal makineler kümesi yönetin.</span><span class="sxs-lookup"><span data-stu-id="008a8-117">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="008a8-118">Ölçek, hakkında hello önceki öğreticide çok öğrenilen bu kullanım hello aynı bileşenleri ayarlar[yüksek oranda kullanılabilir sanal makineleri oluşturmak](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="008a8-118">Scale sets use hello same components as you learned about in hello previous tutorial too[Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="008a8-119">VM ölçek kümesindeki bir kullanılabilirlik kümesi ve mantığı arıza ve güncelleştirme etki alanları arasında dağıtılan oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="008a8-119">VMs in a scale set are created in an availability set and distributed across logic fault and update domains.</span></span>

<span data-ttu-id="008a8-120">VM ölçek kümesindeki gerektiği şekilde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="008a8-120">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="008a8-121">Otomatik ölçeklendirme kurallarını toocontrol tanımladığınız nasıl ve ne zaman VM'ler eklenir veya hello ölçek kümesinden kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="008a8-121">You define autoscale rules toocontrol how and when VMs are added or removed from hello scale set.</span></span> <span data-ttu-id="008a8-122">Bu kurallar temel alınarak ölçümleri CPU yükünü, bellek kullanımı veya ağ trafiğini gibi tetikleyebilir.</span><span class="sxs-lookup"><span data-stu-id="008a8-122">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="008a8-123">Ölçek too1, Azure platform görüntüsü kullandığınızda 000 VM'ler desteği ayarlar.</span><span class="sxs-lookup"><span data-stu-id="008a8-123">Scale sets support up too1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="008a8-124">Üretim iş yükleri için çok isteyebilir[özel bir VM görüntüsü oluşturma](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="008a8-124">For production workloads, you may wish too[Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="008a8-125">Özel görüntü kullanırken ayarlayın ölçeğinde too100 Vm'leri yedekleme oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="008a8-125">You can create up too100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-tooscale"></a><span data-ttu-id="008a8-126">Bir uygulama tooscale oluşturma</span><span class="sxs-lookup"><span data-stu-id="008a8-126">Create an app tooscale</span></span>
<span data-ttu-id="008a8-127">Üretim kullanımı için çok isteyebilir[özel bir VM görüntüsü oluşturma](tutorial-custom-images.md) uygulamanızın yüklenmiş ve yapılandırılmış içerir.</span><span class="sxs-lookup"><span data-stu-id="008a8-127">For production use, you may wish too[Create a custom VM image](tutorial-custom-images.md) that includes your application installed and configured.</span></span> <span data-ttu-id="008a8-128">Bu öğretici için ilk önyükleme tooquickly Vm'lerinde ölçeği eylemini Ayarla bkz hello özelleştirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="008a8-128">For this tutorial, lets customize hello VMs on first boot tooquickly see a scale set in action.</span></span>

<span data-ttu-id="008a8-129">Bir önceki öğreticide öğrenilen [nasıl toocustomize Linux sanal bir makinede ilk önyükleme](tutorial-automate-vm-deployment.md) bulut init ile.</span><span class="sxs-lookup"><span data-stu-id="008a8-129">In a previous tutorial, you learned [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md) with cloud-init.</span></span> <span data-ttu-id="008a8-130">Kullanabileceğiniz aynı bulut init yapılandırma dosyası tooinstall NGINX hello ve basit bir 'Hello World' Node.js uygulaması çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="008a8-130">You can use hello same cloud-init configuration file tooinstall NGINX and run a simple 'Hello World' Node.js app.</span></span> 

<span data-ttu-id="008a8-131">Geçerli kabuğunuzu adlı bir dosya oluşturun *bulut init.txt* Yapıştır hello izleyerek yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="008a8-131">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="008a8-132">Örneğin, yerel makinenizde değil hello bulut Kabuk hello dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="008a8-132">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="008a8-133">Girin `sensible-editor cloud-init.txt` toocreate hello dosya ve kullanılabilir düzenleyicileri listesini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="008a8-133">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="008a8-134">Merhaba tüm bulut init dosyanın doğru şekilde kopyalandığından emin olun, özellikle ilk satırı hello:</span><span class="sxs-lookup"><span data-stu-id="008a8-134">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

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


## <a name="create-a-scale-set"></a><span data-ttu-id="008a8-135">Bir ölçek kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="008a8-135">Create a scale set</span></span>
<span data-ttu-id="008a8-136">Ölçek kümesini oluşturmadan önce bir kaynak grubuyla oluşturmanız [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="008a8-136">Before you can create a scale set, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="008a8-137">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroupScaleSet* hello içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="008a8-137">hello following example creates a resource group named *myResourceGroupScaleSet* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

<span data-ttu-id="008a8-138">Şimdi bir sanal makine ölçek kümesi oluşturmak [az vmss oluşturma](/cli/azure/vmss#create).</span><span class="sxs-lookup"><span data-stu-id="008a8-138">Now create a virtual machine scale set with [az vmss create](/cli/azure/vmss#create).</span></span> <span data-ttu-id="008a8-139">Merhaba aşağıdaki örnekte oluşturur ölçeği adlandırılmış Ayarla *myScaleSet*hello bulut init dosya toocustomize hello VM kullanır ve mevcut SSH anahtarları oluşturur:</span><span class="sxs-lookup"><span data-stu-id="008a8-139">hello following example creates a scale set named *myScaleSet*, uses hello cloud-init file toocustomize hello VM, and generates SSH keys if they do not exist:</span></span>

```azurecli-interactive 
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image UbuntuLTS \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

<span data-ttu-id="008a8-140">Birkaç dakika toocreate alır ve tüm hello ölçek kümesi kaynakları ve VM'ler yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="008a8-140">It takes a few minutes toocreate and configure all hello scale set resources and VMs.</span></span> <span data-ttu-id="008a8-141">Hello Azure CLI toohello istemi döndükten sonra toorun devam arka plan görevleri vardır.</span><span class="sxs-lookup"><span data-stu-id="008a8-141">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="008a8-142">Başka bir birkaç hello uygulamaya erişmek için dakika olabilir.</span><span class="sxs-lookup"><span data-stu-id="008a8-142">It may be another couple of minutes before you can access hello app.</span></span>


## <a name="allow-web-traffic"></a><span data-ttu-id="008a8-143">Web trafiği izin ver</span><span class="sxs-lookup"><span data-stu-id="008a8-143">Allow web traffic</span></span>
<span data-ttu-id="008a8-144">Bir yük dengeleyici hello sanal makine ölçek kümesinin bir parçası olarak otomatik olarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="008a8-144">A load balancer was created automatically as part of hello virtual machine scale set.</span></span> <span data-ttu-id="008a8-145">Merhaba yük dengeleyici trafiği yük dengeleyici kuralları kullanarak tanımlanan VM'ler kümesi arasında dağıtır.</span><span class="sxs-lookup"><span data-stu-id="008a8-145">hello load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="008a8-146">Yük Dengeleyici kavramları ve hello sonraki öğreticide yapılandırma hakkında daha fazla bilgiyi [nasıl tooload Bakiye azure'daki sanal makinelerde](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="008a8-146">You can learn more about load balancer concepts and configuration in hello next tutorial, [How tooload balance virtual machines in Azure](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="008a8-147">tooallow trafiği tooreach hello web uygulaması, bir kural oluştururken [az ağ lb kuralı oluşturma](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="008a8-147">tooallow traffic tooreach hello web app, create a rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="008a8-148">Merhaba aşağıdaki örnek adlı bir kural oluşturur *myLoadBalancerRuleWeb*:</span><span class="sxs-lookup"><span data-stu-id="008a8-148">hello following example creates a rule named *myLoadBalancerRuleWeb*:</span></span>

```azurecli-interactive 
az network lb rule create \
  --resource-group myResourceGroupScaleSet \
  --name myLoadBalancerRuleWeb \
  --lb-name myScaleSetLB \
  --backend-pool-name myScaleSetLBBEPool \
  --backend-port 80 \
  --frontend-ip-name loadBalancerFrontEnd \
  --frontend-port 80 \
  --protocol tcp
```

## <a name="test-your-app"></a><span data-ttu-id="008a8-149">Uygulamanızı test etme</span><span class="sxs-lookup"><span data-stu-id="008a8-149">Test your app</span></span>
<span data-ttu-id="008a8-150">toosee Node.js uygulamanızı hello Web'de elde hello genel IP adresi, yük dengeleyici ile [az ağ ortak IP Göster](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="008a8-150">toosee your Node.js app on hello web, obtain hello public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="008a8-151">Merhaba aşağıdaki örnek alacağı için başlangıç IP adresi *myScaleSetLBPublicIP* hello ölçek kümesinin bir parçası olarak oluşturulan:</span><span class="sxs-lookup"><span data-stu-id="008a8-151">hello following example obtains hello IP address for *myScaleSetLBPublicIP* created as part of hello scale set:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="008a8-152">Tooa web tarayıcısında Hello genel IP adresi girin.</span><span class="sxs-lookup"><span data-stu-id="008a8-152">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="008a8-153">VM bu hello yük dengeleyici dağıtılmış trafiği hello hello ana dahil olmak üzere Hello uygulama görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="008a8-153">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic to:</span></span>

![Çalışan Node.js uygulaması](./media/tutorial-create-vmss/running-nodejs-app.png)

<span data-ttu-id="008a8-155">toosee hello ölçeği, eylemde ayarla, zorla yenileme web tarayıcısı toosee hello yük dengeleyici, uygulamanızı çalıştıran tüm hello VM'ler arasında trafiği dağıtın.</span><span class="sxs-lookup"><span data-stu-id="008a8-155">toosee hello scale set in action, you can force-refresh your web browser toosee hello load balancer distribute traffic across all hello VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="008a8-156">Yönetim görevleri</span><span class="sxs-lookup"><span data-stu-id="008a8-156">Management tasks</span></span>
<span data-ttu-id="008a8-157">Merhaba ölçek kümesini Hello yaşam döngüsü boyunca toorun gerekebilir bir veya daha fazla yönetim görevleri.</span><span class="sxs-lookup"><span data-stu-id="008a8-157">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="008a8-158">Ayrıca, çeşitli yaşam döngüsü görevleri otomatikleştiren toocreate komut dosyaları isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="008a8-158">Additionally, you may want toocreate scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="008a8-159">Hello Azure CLI 2.0 hızlı şekilde toodo bu görevleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="008a8-159">hello Azure CLI 2.0 provides a quick way toodo those tasks.</span></span> <span data-ttu-id="008a8-160">Birkaç ortak görevler şunlardır.</span><span class="sxs-lookup"><span data-stu-id="008a8-160">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="008a8-161">Görünüm VM ölçek kümesindeki</span><span class="sxs-lookup"><span data-stu-id="008a8-161">View VMs in a scale set</span></span>
<span data-ttu-id="008a8-162">tooview, Ölçek çalışan sanal makineler listesi ayarlayabilir, kullanabilir [az vmss listesi-örneklerini](/cli/azure/vmss#list-instances) gibi:</span><span class="sxs-lookup"><span data-stu-id="008a8-162">tooview a list of VMs running in your scale set, use [az vmss list-instances](/cli/azure/vmss#list-instances) as follows:</span></span>

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

<span data-ttu-id="008a8-163">Merhaba, benzer toohello aşağıdaki örneğine çıktı:</span><span class="sxs-lookup"><span data-stu-id="008a8-163">hello output is similar toohello following example:</span></span>

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="008a8-164">Artırma veya azaltma VM örnekleri</span><span class="sxs-lookup"><span data-stu-id="008a8-164">Increase or decrease VM instances</span></span>
<span data-ttu-id="008a8-165">toosee hello örnek sayısı, şu anda bir ölçek kümesindeki, kullanın [az vmss Göster](/cli/azure/vmss#show) ve sorgulayın *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="008a8-165">toosee hello number of instances you currently have in a scale set, use [az vmss show](/cli/azure/vmss#show) and query on *sku.capacity*:</span></span>

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

<span data-ttu-id="008a8-166">Daha sonra el ile artırabilir veya sanal makineler kümesi hello ölçeğinde hello sayısını azaltmak [az vmss ölçek](/cli/azure/vmss#scale).</span><span class="sxs-lookup"><span data-stu-id="008a8-166">You can then manually increase or decrease hello number of virtual machines in hello scale set with [az vmss scale](/cli/azure/vmss#scale).</span></span> <span data-ttu-id="008a8-167">Merhaba aşağıdaki örnek hello sayısını VM'ler, ölçeği çok ayarla ayarlar*5*:</span><span class="sxs-lookup"><span data-stu-id="008a8-167">hello following example sets hello number of VMs in your scale set too*5*:</span></span>

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

<span data-ttu-id="008a8-168">Otomatik ölçeklendirme kurallarını, ağ trafiğini veya CPU kullanımı gibi yanıt toodemand nasıl tooscale yukarı veya aşağı hello sayısında VM'ler, Ölçek kümesindeki tanımlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="008a8-168">Autoscale rules let you define how tooscale up or down hello number of VMs in your scale set in response toodemand such as network traffic or CPU usage.</span></span> <span data-ttu-id="008a8-169">Şu anda, bu kurallar Azure CLI 2. 0'olarak ayarlanamaz.</span><span class="sxs-lookup"><span data-stu-id="008a8-169">Currently, these rules cannot be set in Azure CLI 2.0.</span></span> <span data-ttu-id="008a8-170">Kullanım hello [Azure portal](https://portal.azure.com) tooconfigure otomatik ölçeklendirme.</span><span class="sxs-lookup"><span data-stu-id="008a8-170">Use hello [Azure portal](https://portal.azure.com) tooconfigure autoscale.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="008a8-171">Bağlantı bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="008a8-171">Get connection info</span></span>
<span data-ttu-id="008a8-172">tooobtain bağlantı bilgilerini hakkında ölçek kümeleri VM'ler Merhaba, kullanın [az vmss listesi-örnek-bağlantı-bilgisi](/cli/azure/vmss#list-instance-connection-info).</span><span class="sxs-lookup"><span data-stu-id="008a8-172">tooobtain connection information about hello VMs in your scale sets, use [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info).</span></span> <span data-ttu-id="008a8-173">Bu komut, SSH ile tooconnect sağlayan her bir VM için hello ortak IP adresi ve bağlantı noktası çıkarır:</span><span class="sxs-lookup"><span data-stu-id="008a8-173">This command outputs hello public IP address and port for each VM that allows you tooconnect with SSH:</span></span>

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a><span data-ttu-id="008a8-174">Veri diskleri ölçek kümeleri ile kullanma</span><span class="sxs-lookup"><span data-stu-id="008a8-174">Use data disks with scale sets</span></span>
<span data-ttu-id="008a8-175">Oluşturun ve veri diskleri ölçek kümeleri ile kullanın.</span><span class="sxs-lookup"><span data-stu-id="008a8-175">You can create and use data disks with scale sets.</span></span> <span data-ttu-id="008a8-176">Önceki bir öğreticide, nasıl çok öğrenilen[yönetmek Azure diskleri](tutorial-manage-disks.md) anahatları en iyi yöntemler ve veri diskleri hello işletim sistemi disk yerine uygulamaları oluşturmak için performans iyileştirmeleri hello.</span><span class="sxs-lookup"><span data-stu-id="008a8-176">In a previous tutorial, you learned how too[Manage Azure disks](tutorial-manage-disks.md) that outlines hello best practices and performance improvements for building apps on data disks rather than hello OS disk.</span></span>

### <a name="create-scale-set-with-data-disks"></a><span data-ttu-id="008a8-177">Veri diskleri ile ölçek kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="008a8-177">Create scale set with data disks</span></span>
<span data-ttu-id="008a8-178">bir ölçek ayarlamak ve veri diskleri ekleme toocreate eklemek hello `--data-disk-sizes-gb` parametresi toohello [az vmss oluşturma](/cli/azure/vmss#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="008a8-178">toocreate a scale set and attach data disks, add hello `--data-disk-sizes-gb` parameter toohello [az vmss create](/cli/azure/vmss#create) command.</span></span> <span data-ttu-id="008a8-179">Merhaba aşağıdaki örnekte oluşturur kümesiyle bir ölçek *50*Gb veri diskleri ekli tooeach örneği:</span><span class="sxs-lookup"><span data-stu-id="008a8-179">hello following example creates a scale set with *50*Gb data disks attached tooeach instance:</span></span>

```azurecli-interactive 
az vmss create \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetDisks \
    --image UbuntuLTS \
    --upgrade-policy-mode automatic \
    --custom-data cloud-init.txt \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50
```

<span data-ttu-id="008a8-180">Ölçek kümesindeki örnekleri kaldırıldığında, eklenen veri disklerini de kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="008a8-180">When instances are removed from a scale set, any attached data disks are also removed.</span></span>

### <a name="add-data-disks"></a><span data-ttu-id="008a8-181">Veri diski Ekle</span><span class="sxs-lookup"><span data-stu-id="008a8-181">Add data disks</span></span>
<span data-ttu-id="008a8-182">bir veri diski tooinstances, Ölçek tooadd ayarlayabilir, kullanabilir [az vmss diskini](/cli/azure/vmss/disk#attach).</span><span class="sxs-lookup"><span data-stu-id="008a8-182">tooadd a data disk tooinstances in your scale set, use [az vmss disk attach](/cli/azure/vmss/disk#attach).</span></span> <span data-ttu-id="008a8-183">Merhaba aşağıdaki örnek, bir *50*Gb disk tooeach örneği:</span><span class="sxs-lookup"><span data-stu-id="008a8-183">hello following example adds a *50*Gb disk tooeach instance:</span></span>

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a><span data-ttu-id="008a8-184">Veri diskleri ayırma</span><span class="sxs-lookup"><span data-stu-id="008a8-184">Detach data disks</span></span>
<span data-ttu-id="008a8-185">bir veri diski tooinstances, Ölçek tooremove ayarlayabilir, kullanabilir [az vmss disk ayırma](/cli/azure/vmss/disk#detach).</span><span class="sxs-lookup"><span data-stu-id="008a8-185">tooremove a data disk tooinstances in your scale set, use [az vmss disk detach](/cli/azure/vmss/disk#detach).</span></span> <span data-ttu-id="008a8-186">Merhaba aşağıdaki örnek kaldırır hello veri diski LUN değerine *2* her örneğinden:</span><span class="sxs-lookup"><span data-stu-id="008a8-186">hello following example removes hello data disk at LUN *2* from each instance:</span></span>

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a><span data-ttu-id="008a8-187">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="008a8-187">Next steps</span></span>
<span data-ttu-id="008a8-188">Bu öğreticide, bir sanal makine ölçek kümesi oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="008a8-188">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="008a8-189">Şunları öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="008a8-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="008a8-190">Bulut init toocreate bir uygulama tooscale kullanın</span><span class="sxs-lookup"><span data-stu-id="008a8-190">Use cloud-init toocreate an app tooscale</span></span>
> * <span data-ttu-id="008a8-191">Bir sanal makine ölçek kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="008a8-191">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="008a8-192">Artırma veya azaltma hello ölçek kümesi örneği sayısı</span><span class="sxs-lookup"><span data-stu-id="008a8-192">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="008a8-193">Ölçek kümesi örnekleri için bağlantı bilgileri görüntüle</span><span class="sxs-lookup"><span data-stu-id="008a8-193">View connection info for scale set instances</span></span>
> * <span data-ttu-id="008a8-194">Veri diskleri bir ölçek kümesinde kullanın</span><span class="sxs-lookup"><span data-stu-id="008a8-194">Use data disks in a scale set</span></span>

<span data-ttu-id="008a8-195">Toohello sonraki öğretici toolearn Yük Dengeleme sanal makineler için kavramları hakkında daha fazla ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="008a8-195">Advance toohello next tutorial toolearn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="008a8-196">Sanal makinelerin yük dengelemesini</span><span class="sxs-lookup"><span data-stu-id="008a8-196">Load balance virtual machines</span></span>](tutorial-load-balancer.md)