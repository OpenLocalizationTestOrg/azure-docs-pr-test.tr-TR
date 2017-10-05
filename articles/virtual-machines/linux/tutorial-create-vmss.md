---
title: "Linux Azure için sanal makine ölçek kümeleri oluşturma | Microsoft Docs"
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
ms.openlocfilehash: 2b8d519e11f70eda164bd8f6e131a3989f242ab0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a><span data-ttu-id="aa27c-103">Bir sanal makine ölçek kümesi oluşturma ve Linux üzerinde yüksek oranda kullanılabilir bir uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="aa27c-103">Create a Virtual Machine Scale Set and deploy a highly available app on Linux</span></span>
<span data-ttu-id="aa27c-104">Bir sanal makine ölçek kümesini dağıtmak ve aynı, otomatik ölçeklendirme sanal makineler kümesi yönetmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="aa27c-104">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="aa27c-105">Ölçek kümesindeki VM'lerin sayısını elle ölçeklendirme ya da CPU kullanımı, bellek isteğe bağlı veya ağ trafiğini göre otomatik ölçeklendirme kurallarını tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aa27c-105">You can scale the number of VMs in the scale set manually, or define rules to autoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="aa27c-106">Bu öğreticide, Azure üzerinde ayarlanmış bir sanal makine ölçek dağıtın.</span><span class="sxs-lookup"><span data-stu-id="aa27c-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="aa27c-107">Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="aa27c-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aa27c-108">Bulut init ölçeklendirmek için bir uygulama oluşturmak için kullanın</span><span class="sxs-lookup"><span data-stu-id="aa27c-108">Use cloud-init to create an app to scale</span></span>
> * <span data-ttu-id="aa27c-109">Bir sanal makine ölçek kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="aa27c-109">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="aa27c-110">Artırma veya azaltma ölçek kümesindeki örnek sayısı</span><span class="sxs-lookup"><span data-stu-id="aa27c-110">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="aa27c-111">Ölçek kümesi örnekleri için bağlantı bilgileri görüntüle</span><span class="sxs-lookup"><span data-stu-id="aa27c-111">View connection info for scale set instances</span></span>
> * <span data-ttu-id="aa27c-112">Veri diskleri bir ölçek kümesinde kullanın</span><span class="sxs-lookup"><span data-stu-id="aa27c-112">Use data disks in a scale set</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="aa27c-113">Yüklemek ve CLI yerel olarak kullanmak seçerseniz, Bu öğretici, Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="aa27c-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="aa27c-114">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="aa27c-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="aa27c-115">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="aa27c-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="scale-set-overview"></a><span data-ttu-id="aa27c-116">Ölçek kümesi'ne genel bakış</span><span class="sxs-lookup"><span data-stu-id="aa27c-116">Scale Set overview</span></span>
<span data-ttu-id="aa27c-117">Bir sanal makine ölçek kümesini dağıtmak ve aynı, otomatik ölçeklendirme sanal makineler kümesi yönetmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="aa27c-117">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="aa27c-118">Ölçek kümeleri kullanan aynı bileşenleri, ilgili önceki öğreticide öğrenilen [yüksek oranda kullanılabilir sanal makineleri oluşturmak](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="aa27c-118">Scale sets use the same components as you learned about in the previous tutorial to [Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="aa27c-119">VM ölçek kümesindeki bir kullanılabilirlik kümesi ve mantığı arıza ve güncelleştirme etki alanları arasında dağıtılan oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="aa27c-119">VMs in a scale set are created in an availability set and distributed across logic fault and update domains.</span></span>

<span data-ttu-id="aa27c-120">VM ölçek kümesindeki gerektiği şekilde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="aa27c-120">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="aa27c-121">Nasıl ve ne zaman VM'ler eklendiğinde veya kaldırıldığında ölçek kümesi denetlemek için otomatik ölçeklendirme kurallarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="aa27c-121">You define autoscale rules to control how and when VMs are added or removed from the scale set.</span></span> <span data-ttu-id="aa27c-122">Bu kurallar temel alınarak ölçümleri CPU yükünü, bellek kullanımı veya ağ trafiğini gibi tetikleyebilir.</span><span class="sxs-lookup"><span data-stu-id="aa27c-122">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="aa27c-123">Bir Azure platform görüntüsü kullandığınızda ölçek 1.000 VM'ler kadar destek ayarlar.</span><span class="sxs-lookup"><span data-stu-id="aa27c-123">Scale sets support up to 1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="aa27c-124">Üretim iş yükleri için istediğiniz [özel bir VM görüntüsü oluşturma](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="aa27c-124">For production workloads, you may wish to [Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="aa27c-125">Özel görüntü kullanırken ayarlayın bir ölçek en fazla 100 sanal makineleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aa27c-125">You can create up to 100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-to-scale"></a><span data-ttu-id="aa27c-126">Ölçeklendirmek için uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="aa27c-126">Create an app to scale</span></span>
<span data-ttu-id="aa27c-127">Üretim kullanımı için istediğiniz [özel bir VM görüntüsü oluşturma](tutorial-custom-images.md) uygulamanızın yüklenmiş ve yapılandırılmış içerir.</span><span class="sxs-lookup"><span data-stu-id="aa27c-127">For production use, you may wish to [Create a custom VM image](tutorial-custom-images.md) that includes your application installed and configured.</span></span> <span data-ttu-id="aa27c-128">Bu öğretici için hızlı şekilde ölçeği eylemini Ayarla görmek için sanal makinelerin ilk önyükleme özelleştirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="aa27c-128">For this tutorial, lets customize the VMs on first boot to quickly see a scale set in action.</span></span>

<span data-ttu-id="aa27c-129">Bir önceki öğreticide öğrenilen [Linux sanal bir makinede ilk önyükleme özelleştirmek nasıl](tutorial-automate-vm-deployment.md) bulut init ile.</span><span class="sxs-lookup"><span data-stu-id="aa27c-129">In a previous tutorial, you learned [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md) with cloud-init.</span></span> <span data-ttu-id="aa27c-130">NGINX yüklemek ve basit bir 'Hello World' Node.js uygulaması çalıştırmak için aynı bulut init yapılandırma dosyası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aa27c-130">You can use the same cloud-init configuration file to install NGINX and run a simple 'Hello World' Node.js app.</span></span> 

<span data-ttu-id="aa27c-131">Geçerli kabuğunuzu adlı bir dosya oluşturun *bulut init.txt* ve aşağıdaki yapılandırma yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="aa27c-131">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="aa27c-132">Örneğin, yerel makinenizde olmayan bulut kabuğunda dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="aa27c-132">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="aa27c-133">Girin `sensible-editor cloud-init.txt` dosyası oluşturun ve kullanılabilir düzenleyicileri listesini görmek için.</span><span class="sxs-lookup"><span data-stu-id="aa27c-133">Enter `sensible-editor cloud-init.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="aa27c-134">Tüm bulut init dosyanın doğru şekilde kopyalandığından emin olun özellikle ilk satırı:</span><span class="sxs-lookup"><span data-stu-id="aa27c-134">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

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


## <a name="create-a-scale-set"></a><span data-ttu-id="aa27c-135">Bir ölçek kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="aa27c-135">Create a scale set</span></span>
<span data-ttu-id="aa27c-136">Ölçek kümesini oluşturmadan önce bir kaynak grubuyla oluşturmanız [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="aa27c-136">Before you can create a scale set, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="aa27c-137">Aşağıdaki örnek, bir kaynak grubu oluşturur *myResourceGroupScaleSet* içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="aa27c-137">The following example creates a resource group named *myResourceGroupScaleSet* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

<span data-ttu-id="aa27c-138">Şimdi bir sanal makine ölçek kümesi oluşturmak [az vmss oluşturma](/cli/azure/vmss#create).</span><span class="sxs-lookup"><span data-stu-id="aa27c-138">Now create a virtual machine scale set with [az vmss create](/cli/azure/vmss#create).</span></span> <span data-ttu-id="aa27c-139">Aşağıdaki örnek, ölçeği adlandırılmış Ayarla oluşturur *myScaleSet*VM özelleştirmek için bulut init dosyasını kullanır ve bunlar yoksa SSH anahtarları oluşturur:</span><span class="sxs-lookup"><span data-stu-id="aa27c-139">The following example creates a scale set named *myScaleSet*, uses the cloud-init file to customize the VM, and generates SSH keys if they do not exist:</span></span>

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

<span data-ttu-id="aa27c-140">Oluşturun ve tüm sanal makineleri ve ölçek kümesi kaynakları yapılandırmak için birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="aa27c-140">It takes a few minutes to create and configure all the scale set resources and VMs.</span></span> <span data-ttu-id="aa27c-141">Azure CLI sorusu döndükten sonra çalışmaya devam arka plan görevleri vardır.</span><span class="sxs-lookup"><span data-stu-id="aa27c-141">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="aa27c-142">Başka bir birkaç uygulamaya erişmek için dakika olabilir.</span><span class="sxs-lookup"><span data-stu-id="aa27c-142">It may be another couple of minutes before you can access the app.</span></span>


## <a name="allow-web-traffic"></a><span data-ttu-id="aa27c-143">Web trafiği izin ver</span><span class="sxs-lookup"><span data-stu-id="aa27c-143">Allow web traffic</span></span>
<span data-ttu-id="aa27c-144">Bir yük dengeleyici sanal makine ölçek kümesinin bir parçası olarak otomatik olarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="aa27c-144">A load balancer was created automatically as part of the virtual machine scale set.</span></span> <span data-ttu-id="aa27c-145">Yük Dengeleyici trafiği yük dengeleyici kuralları kullanarak tanımlanan VM'ler kümesi arasında dağıtır.</span><span class="sxs-lookup"><span data-stu-id="aa27c-145">The load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="aa27c-146">Yük Dengeleyici kavramları ve sonraki öğreticide yapılandırma hakkında daha fazla bilgiyi [sanal makinelerin azure'da yük dengelemesini nasıl](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="aa27c-146">You can learn more about load balancer concepts and configuration in the next tutorial, [How to load balance virtual machines in Azure](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="aa27c-147">Web uygulamasına ulaşması trafiğine izin vermek için bir kural oluştururken [az ağ lb kuralını](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="aa27c-147">To allow traffic to reach the web app, create a rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="aa27c-148">Aşağıdaki örnek, adında bir kural oluşturur *myLoadBalancerRuleWeb*:</span><span class="sxs-lookup"><span data-stu-id="aa27c-148">The following example creates a rule named *myLoadBalancerRuleWeb*:</span></span>

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

## <a name="test-your-app"></a><span data-ttu-id="aa27c-149">Uygulamanızı test etme</span><span class="sxs-lookup"><span data-stu-id="aa27c-149">Test your app</span></span>
<span data-ttu-id="aa27c-150">Node.js uygulamanızı Web'de görmek için yük dengeleyici ile genel IP adresi elde [az ağ ortak IP Göster](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="aa27c-150">To see your Node.js app on the web, obtain the public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="aa27c-151">Aşağıdaki örnek IP adresi alacağı *myScaleSetLBPublicIP* ölçek kümesinin bir parçası olarak oluşturulan:</span><span class="sxs-lookup"><span data-stu-id="aa27c-151">The following example obtains the IP address for *myScaleSetLBPublicIP* created as part of the scale set:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="aa27c-152">Ortak IP adresini bir web tarayıcısına girin.</span><span class="sxs-lookup"><span data-stu-id="aa27c-152">Enter the public IP address in to a web browser.</span></span> <span data-ttu-id="aa27c-153">Ana bilgisayar trafiği için yük dengeleyici dağıtılmış VM adını dahil olmak üzere uygulama gösterilir:</span><span class="sxs-lookup"><span data-stu-id="aa27c-153">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to:</span></span>

![Çalışan Node.js uygulaması](./media/tutorial-create-vmss/running-nodejs-app.png)

<span data-ttu-id="aa27c-155">Eylem kümesini görmek için zorla uygulamanızı çalıştıran tüm VM'ler arasında trafiği dağıtmak yük dengeleyici görmek için web tarayıcınızın yenileme.</span><span class="sxs-lookup"><span data-stu-id="aa27c-155">To see the scale set in action, you can force-refresh your web browser to see the load balancer distribute traffic across all the VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="aa27c-156">Yönetim görevleri</span><span class="sxs-lookup"><span data-stu-id="aa27c-156">Management tasks</span></span>
<span data-ttu-id="aa27c-157">Ölçek kümesini yaşam döngüsü boyunca, bir veya daha fazla yönetim görevleri çalıştırmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="aa27c-157">Throughout the lifecycle of the scale set, you may need to run one or more management tasks.</span></span> <span data-ttu-id="aa27c-158">Ayrıca, çeşitli yaşam döngüsü görevleri otomatikleştiren komut dosyaları oluşturmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aa27c-158">Additionally, you may want to create scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="aa27c-159">Azure CLI 2.0, bu görevleri gerçekleştirmek için hızlı bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="aa27c-159">The Azure CLI 2.0 provides a quick way to do those tasks.</span></span> <span data-ttu-id="aa27c-160">Birkaç ortak görevler şunlardır.</span><span class="sxs-lookup"><span data-stu-id="aa27c-160">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="aa27c-161">Görünüm VM ölçek kümesindeki</span><span class="sxs-lookup"><span data-stu-id="aa27c-161">View VMs in a scale set</span></span>
<span data-ttu-id="aa27c-162">Ölçek kümesinde çalışan sanal makineler listesini görüntülemek için kullanın [az vmss listesi-örneklerini](/cli/azure/vmss#list-instances) gibi:</span><span class="sxs-lookup"><span data-stu-id="aa27c-162">To view a list of VMs running in your scale set, use [az vmss list-instances](/cli/azure/vmss#list-instances) as follows:</span></span>

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

<span data-ttu-id="aa27c-163">Çıktı aşağıdaki örneğe benzer:</span><span class="sxs-lookup"><span data-stu-id="aa27c-163">The output is similar to the following example:</span></span>

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="aa27c-164">Artırma veya azaltma VM örnekleri</span><span class="sxs-lookup"><span data-stu-id="aa27c-164">Increase or decrease VM instances</span></span>
<span data-ttu-id="aa27c-165">Ölçek kümesindeki şu anda sahip örneklerinin sayısını görmek için [az vmss Göster](/cli/azure/vmss#show) ve sorgulayın *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="aa27c-165">To see the number of instances you currently have in a scale set, use [az vmss show](/cli/azure/vmss#show) and query on *sku.capacity*:</span></span>

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

<span data-ttu-id="aa27c-166">Daha sonra el ile artırabilir veya sanal makine ölçek kümesi sayısını azaltmak [az vmss ölçek](/cli/azure/vmss#scale).</span><span class="sxs-lookup"><span data-stu-id="aa27c-166">You can then manually increase or decrease the number of virtual machines in the scale set with [az vmss scale](/cli/azure/vmss#scale).</span></span> <span data-ttu-id="aa27c-167">Aşağıdaki örnek VM'lerin sayısını ayarlamak, Ölçek ayarlar *5*:</span><span class="sxs-lookup"><span data-stu-id="aa27c-167">The following example sets the number of VMs in your scale set to *5*:</span></span>

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

<span data-ttu-id="aa27c-168">Otomatik ölçeklendirme kurallarını, yukarı veya aşağı VM'lerin sayısını yanıt ağ trafiğini veya CPU kullanımı gibi isteğe bağlı olarak ayarlamak, Ölçek ölçeklendirme tanımlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="aa27c-168">Autoscale rules let you define how to scale up or down the number of VMs in your scale set in response to demand such as network traffic or CPU usage.</span></span> <span data-ttu-id="aa27c-169">Şu anda, bu kurallar Azure CLI 2. 0'olarak ayarlanamaz.</span><span class="sxs-lookup"><span data-stu-id="aa27c-169">Currently, these rules cannot be set in Azure CLI 2.0.</span></span> <span data-ttu-id="aa27c-170">Kullanım [Azure portal](https://portal.azure.com) otomatik ölçeklendirme yapılandırmak için.</span><span class="sxs-lookup"><span data-stu-id="aa27c-170">Use the [Azure portal](https://portal.azure.com) to configure autoscale.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="aa27c-171">Bağlantı bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="aa27c-171">Get connection info</span></span>
<span data-ttu-id="aa27c-172">Ölçek kümesindeki sanal makineleri bağlantı bilgilerini almak için kullanın [az vmss listesi-örnek-bağlantı-bilgisi](/cli/azure/vmss#list-instance-connection-info).</span><span class="sxs-lookup"><span data-stu-id="aa27c-172">To obtain connection information about the VMs in your scale sets, use [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info).</span></span> <span data-ttu-id="aa27c-173">Bu komut, SSH ile bağlanmanıza olanak sağlayan her bir VM için genel IP adresi ve bağlantı noktası çıkarır:</span><span class="sxs-lookup"><span data-stu-id="aa27c-173">This command outputs the public IP address and port for each VM that allows you to connect with SSH:</span></span>

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a><span data-ttu-id="aa27c-174">Veri diskleri ölçek kümeleri ile kullanma</span><span class="sxs-lookup"><span data-stu-id="aa27c-174">Use data disks with scale sets</span></span>
<span data-ttu-id="aa27c-175">Oluşturun ve veri diskleri ölçek kümeleri ile kullanın.</span><span class="sxs-lookup"><span data-stu-id="aa27c-175">You can create and use data disks with scale sets.</span></span> <span data-ttu-id="aa27c-176">Bir önceki öğreticide öğrenilen nasıl [yönetmek Azure diskleri](tutorial-manage-disks.md) en iyi uygulamalar ve işletim sistemi diski yerine veri diskleri uygulamaları oluşturmaya yönelik performans geliştirmeleri özetler.</span><span class="sxs-lookup"><span data-stu-id="aa27c-176">In a previous tutorial, you learned how to [Manage Azure disks](tutorial-manage-disks.md) that outlines the best practices and performance improvements for building apps on data disks rather than the OS disk.</span></span>

### <a name="create-scale-set-with-data-disks"></a><span data-ttu-id="aa27c-177">Veri diskleri ile ölçek kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="aa27c-177">Create scale set with data disks</span></span>
<span data-ttu-id="aa27c-178">Ölçek kümesi oluşturmak ve veri diskleri eklemek için Ekle `--data-disk-sizes-gb` parametresi [az vmss oluşturma](/cli/azure/vmss#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="aa27c-178">To create a scale set and attach data disks, add the `--data-disk-sizes-gb` parameter to the [az vmss create](/cli/azure/vmss#create) command.</span></span> <span data-ttu-id="aa27c-179">Aşağıdaki örnek, bir ölçek kümesi oluşturur *50*Gb veri disklerinin her örneğine eklenmiş:</span><span class="sxs-lookup"><span data-stu-id="aa27c-179">The following example creates a scale set with *50*Gb data disks attached to each instance:</span></span>

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

<span data-ttu-id="aa27c-180">Ölçek kümesindeki örnekleri kaldırıldığında, eklenen veri disklerini de kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="aa27c-180">When instances are removed from a scale set, any attached data disks are also removed.</span></span>

### <a name="add-data-disks"></a><span data-ttu-id="aa27c-181">Veri diski Ekle</span><span class="sxs-lookup"><span data-stu-id="aa27c-181">Add data disks</span></span>
<span data-ttu-id="aa27c-182">Örnekler, Ölçek kümesindeki bir veri diski eklemek için kullanın [az vmss diskini](/cli/azure/vmss/disk#attach).</span><span class="sxs-lookup"><span data-stu-id="aa27c-182">To add a data disk to instances in your scale set, use [az vmss disk attach](/cli/azure/vmss/disk#attach).</span></span> <span data-ttu-id="aa27c-183">Aşağıdaki örnek, bir *50*Gb disk her örneği için:</span><span class="sxs-lookup"><span data-stu-id="aa27c-183">The following example adds a *50*Gb disk to each instance:</span></span>

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a><span data-ttu-id="aa27c-184">Veri diskleri ayırma</span><span class="sxs-lookup"><span data-stu-id="aa27c-184">Detach data disks</span></span>
<span data-ttu-id="aa27c-185">Ölçek kümesindeki bir veri diski örneklerine kaldırmak için kullanın [az vmss disk ayırma](/cli/azure/vmss/disk#detach).</span><span class="sxs-lookup"><span data-stu-id="aa27c-185">To remove a data disk to instances in your scale set, use [az vmss disk detach](/cli/azure/vmss/disk#detach).</span></span> <span data-ttu-id="aa27c-186">Aşağıdaki örnek veri diski LUN değerine kaldırır *2* her örneğinden:</span><span class="sxs-lookup"><span data-stu-id="aa27c-186">The following example removes the data disk at LUN *2* from each instance:</span></span>

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a><span data-ttu-id="aa27c-187">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aa27c-187">Next steps</span></span>
<span data-ttu-id="aa27c-188">Bu öğreticide, bir sanal makine ölçek kümesi oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="aa27c-188">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="aa27c-189">Size nasıl öğrenilen için:</span><span class="sxs-lookup"><span data-stu-id="aa27c-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aa27c-190">Bulut init ölçeklendirmek için bir uygulama oluşturmak için kullanın</span><span class="sxs-lookup"><span data-stu-id="aa27c-190">Use cloud-init to create an app to scale</span></span>
> * <span data-ttu-id="aa27c-191">Bir sanal makine ölçek kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="aa27c-191">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="aa27c-192">Artırma veya azaltma ölçek kümesindeki örnek sayısı</span><span class="sxs-lookup"><span data-stu-id="aa27c-192">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="aa27c-193">Ölçek kümesi örnekleri için bağlantı bilgileri görüntüle</span><span class="sxs-lookup"><span data-stu-id="aa27c-193">View connection info for scale set instances</span></span>
> * <span data-ttu-id="aa27c-194">Veri diskleri bir ölçek kümesinde kullanın</span><span class="sxs-lookup"><span data-stu-id="aa27c-194">Use data disks in a scale set</span></span>

<span data-ttu-id="aa27c-195">Yük Dengeleme sanal makineler için kavramları hakkında daha fazla bilgi için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="aa27c-195">Advance to the next tutorial to learn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aa27c-196">Sanal makinelerin yük dengelemesini</span><span class="sxs-lookup"><span data-stu-id="aa27c-196">Load balance virtual machines</span></span>](tutorial-load-balancer.md)