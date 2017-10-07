---
title: "aaaAzure hızlı başlangıç - Windows VM CLI oluşturun | Microsoft Docs"
description: "Hızlı bir şekilde toocreate bir Windows sanal makineleri hello Azure CLI ile bilgi edinin."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 029bdecec219b12b80b958ceeedda214f1b13149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="81c8b-103">Hello Azure CLI ile Windows sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="81c8b-103">Create a Windows virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="81c8b-104">Hello Azure CLI kullanılan toocreate olan ve hello komut satırından veya komut dosyalarında Azure kaynaklarını yönetin.</span><span class="sxs-lookup"><span data-stu-id="81c8b-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="81c8b-105">Windows Server 2016 çalışan bir sanal makine Hello Azure CLI toodeploy kullanarak bu kılavuzu ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="81c8b-105">This guide details using hello Azure CLI toodeploy a virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="81c8b-106">Dağıtım tamamlandıktan sonra biz toohello sunucusuna bağlanmak ve IIS yükleyin.</span><span class="sxs-lookup"><span data-stu-id="81c8b-106">Once deployment is complete, we connect toohello server and install IIS.</span></span>

<span data-ttu-id="81c8b-107">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="81c8b-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="81c8b-108">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu hızlı başlangıç hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="81c8b-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="81c8b-109">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="81c8b-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="81c8b-110">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="81c8b-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="81c8b-111">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="81c8b-111">Create a resource group</span></span>

<span data-ttu-id="81c8b-112">[az group create](/cli/azure/group#create) ile bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="81c8b-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="81c8b-113">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="81c8b-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="81c8b-114">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu.</span><span class="sxs-lookup"><span data-stu-id="81c8b-114">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="81c8b-115">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="81c8b-115">Create virtual machine</span></span>

<span data-ttu-id="81c8b-116">[az vm create](/cli/azure/vm#create) ile bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="81c8b-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> 

<span data-ttu-id="81c8b-117">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVM*.</span><span class="sxs-lookup"><span data-stu-id="81c8b-117">hello following example creates a VM named *myVM*.</span></span> <span data-ttu-id="81c8b-118">Bu örnekte *azureuser* bir yönetici kullanıcı adı ve *myPassword12* hello parola olarak.</span><span class="sxs-lookup"><span data-stu-id="81c8b-118">This example uses *azureuser* for an administrative user name and *myPassword12* as hello password.</span></span> <span data-ttu-id="81c8b-119">Bu değerleri toosomething uygun tooyour ortamı güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="81c8b-119">Update these values toosomething appropriate tooyour environment.</span></span> <span data-ttu-id="81c8b-120">Bu değerleri, bir bağlantı ile Merhaba sanal makine oluştururken gereklidir.</span><span class="sxs-lookup"><span data-stu-id="81c8b-120">These values are needed when creating a connection with hello virtual machine.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12
```

<span data-ttu-id="81c8b-121">Merhaba VM oluşturduğunuzda hello Azure CLI örnek aşağıdaki bilgileri benzer toohello gösterir.</span><span class="sxs-lookup"><span data-stu-id="81c8b-121">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="81c8b-122">Merhaba not edin `publicIpAaddress`.</span><span class="sxs-lookup"><span data-stu-id="81c8b-122">Take note of hello `publicIpAaddress`.</span></span> <span data-ttu-id="81c8b-123">Kullanılan tooaccess hello VM adresidir.</span><span class="sxs-lookup"><span data-stu-id="81c8b-123">This address is used tooaccess hello VM.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="81c8b-124">Web trafiği için 80 numaralı bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="81c8b-124">Open port 80 for web traffic</span></span> 

<span data-ttu-id="81c8b-125">Varsayılan olarak, Azure'da dağıtılan tooWindows sanal makineleri yalnızca RDP bağlantılara izin verilir.</span><span class="sxs-lookup"><span data-stu-id="81c8b-125">By default only RDP connections are allowed in tooWindows virtual machines deployed in Azure.</span></span> <span data-ttu-id="81c8b-126">Bu VM toobe bir Web sunucusu olacaksa, hello Internet gelen tooopen bağlantı noktası 80 gerekir.</span><span class="sxs-lookup"><span data-stu-id="81c8b-126">If this VM is going toobe a webserver, you need tooopen port 80 from hello Internet.</span></span> <span data-ttu-id="81c8b-127">Kullanım hello [az vm Aç-port](/cli/azure/vm#open-port) komutu tooopen hello istenen bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="81c8b-127">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
 ```azurecli-interactive  
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```


## <a name="connect-toovirtual-machine"></a><span data-ttu-id="81c8b-128">Toovirtual makineyi bağlayın</span><span class="sxs-lookup"><span data-stu-id="81c8b-128">Connect toovirtual machine</span></span>

<span data-ttu-id="81c8b-129">Kullanım hello aşağıdaki hello sanal makineyle Uzak Masaüstü oturumu toocreate komutu.</span><span class="sxs-lookup"><span data-stu-id="81c8b-129">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="81c8b-130">Başlangıç IP adresi hello genel IP adresi, sanal makine ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="81c8b-130">Replace hello IP address with hello public IP address of your virtual machine.</span></span> <span data-ttu-id="81c8b-131">İstendiğinde, hello sanal makine oluşturulurken kullanılan hello kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="81c8b-131">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```bash 
mstsc /v:<Public IP Address>
```

## <a name="install-iis-using-powershell"></a><span data-ttu-id="81c8b-132">PowerShell kullanarak IIS yükleme</span><span class="sxs-lookup"><span data-stu-id="81c8b-132">Install IIS using PowerShell</span></span>

<span data-ttu-id="81c8b-133">Toohello Azure VM'de oturum, tek satırlık bir PowerShell tooinstall IIS kullanın ve hello yerel güvenlik duvarı kuralı tooallow web trafiği etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="81c8b-133">Now that you have logged in toohello Azure VM, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="81c8b-134">PowerShell komut istemini açın ve hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="81c8b-134">Open a PowerShell prompt and run hello following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="81c8b-135">Görünüm hello IIS Karşılama sayfası</span><span class="sxs-lookup"><span data-stu-id="81c8b-135">View hello IIS welcome page</span></span>

<span data-ttu-id="81c8b-136">IIS yüklü ve bağlantı noktası 80, VM'den hello Internet üzerinde şimdi açık ile seçim tooview hello varsayılan IIS Karşılama sayfasını bir web tarayıcısı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81c8b-136">With IIS installed and port 80 now open on your VM from hello Internet, you can use a web browser of your choice tooview hello default IIS welcome page.</span></span> <span data-ttu-id="81c8b-137">Toovisit hello varsayılan sayfa belgelenen emin toouse hello genel IP adresi olabilir.</span><span class="sxs-lookup"><span data-stu-id="81c8b-137">Be sure toouse hello public IP address you documented above toovisit hello default page.</span></span> 

![Varsayılan IIS sitesi](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="81c8b-139">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="81c8b-139">Clean up resources</span></span>

<span data-ttu-id="81c8b-140">Artık gerektiğinde Merhaba kullanabilirsiniz [az grubu Sil](/cli/azure/group#delete) tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="81c8b-140">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="81c8b-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="81c8b-141">Next steps</span></span>

<span data-ttu-id="81c8b-142">Bu hızlı başlangıçta basit bir sanal makine ve bir ağ güvenlik grubu kuralı dağıtıp, bir web sunucusu yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="81c8b-142">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="81c8b-143">Azure sanal makinelerde hakkında daha fazla toolearn toohello öğretici Windows VM'ler için devam edin.</span><span class="sxs-lookup"><span data-stu-id="81c8b-143">toolearn more about Azure virtual machines, continue toohello tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="81c8b-144">Azure Windows sanal makine öğreticileri</span><span class="sxs-lookup"><span data-stu-id="81c8b-144">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
