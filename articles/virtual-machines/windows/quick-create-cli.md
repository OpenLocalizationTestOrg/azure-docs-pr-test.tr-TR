---
title: "Azure Hızlı Başlangıç - Windows VM CLI oluşturma | Microsoft Docs"
description: "Azure CLI ile Windows sanal makinesi oluşturmayı hızlı bir şekilde öğrenin."
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
ms.openlocfilehash: fcb2f1389b3434d0d2e3145217e54ceb2326b969
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-windows-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="b9aa3-103">Azure CLI ile Windows sanal makinesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="b9aa3-103">Create a Windows virtual machine with the Azure CLI</span></span>

<span data-ttu-id="b9aa3-104">Azure CLI, komut satırından veya betik içindeki Azure kaynaklarını oluşturmak ve yönetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="b9aa3-105">Bu kılavuzda Windows Server 2016 çalıştıran bir sanal makineyi Azure CLI kullanarak dağıtma işleminin ayrıntıları verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-105">This guide details using the Azure CLI to deploy a virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="b9aa3-106">Dağıtım tamamlandıktan sonra sunucuya bağlanılır ve IIS yüklenir.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-106">Once deployment is complete, we connect to the server and install IIS.</span></span>

<span data-ttu-id="b9aa3-107">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b9aa3-108">CLI'yi yerel olarak yükleyip kullanmayı seçerseniz bu hızlı başlangıç için Azure CLI 2.0.4 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-108">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="b9aa3-109">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="b9aa3-110">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b9aa3-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="b9aa3-111">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="b9aa3-111">Create a resource group</span></span>

<span data-ttu-id="b9aa3-112">[az group create](/cli/azure/group#create) ile bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="b9aa3-113">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="b9aa3-114">Aşağıdaki örnek *eastus* konumunda *myResourceGroup* adlı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-114">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="b9aa3-115">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="b9aa3-115">Create virtual machine</span></span>

<span data-ttu-id="b9aa3-116">[az vm create](/cli/azure/vm#create) ile bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> 

<span data-ttu-id="b9aa3-117">Aşağıdaki örnekte *myVM* adlı bir VM oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-117">The following example creates a VM named *myVM*.</span></span> <span data-ttu-id="b9aa3-118">Bu örnekte yönetici kullanıcı için *azureuser* kullanıcı adı ve *myPassword12* parolası kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-118">This example uses *azureuser* for an administrative user name and *myPassword12* as the password.</span></span> <span data-ttu-id="b9aa3-119">Bu değerleri ortamınız için uygun olan bir değerle güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-119">Update these values to something appropriate to your environment.</span></span> <span data-ttu-id="b9aa3-120">Bu değerler, sanal makine ile bağlantı oluştururken gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-120">These values are needed when creating a connection with the virtual machine.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12
```

<span data-ttu-id="b9aa3-121">VM oluşturulduğunda Azure CLI, aşağıdaki örneğe benzer bilgiler gösterir.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-121">When the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="b9aa3-122">`publicIpAaddress` değerini not edin.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-122">Take note of the `publicIpAaddress`.</span></span> <span data-ttu-id="b9aa3-123">Bu adres, VM’ye erişmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-123">This address is used to access the VM.</span></span>

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

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="b9aa3-124">Web trafiği için 80 numaralı bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="b9aa3-124">Open port 80 for web traffic</span></span> 

<span data-ttu-id="b9aa3-125">Varsayılan olarak, Azure’a dağıtılmış Windows sanal makinelerinde yalnızca RDP bağlantılarına izin verilir.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-125">By default only RDP connections are allowed in to Windows virtual machines deployed in Azure.</span></span> <span data-ttu-id="b9aa3-126">Bu VM bir web sunucusu olacaksa, İnternet’ten 80 numaralı bağlantı noktasını açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-126">If this VM is going to be a webserver, you need to open port 80 from the Internet.</span></span> <span data-ttu-id="b9aa3-127">İstediğiniz bağlantı noktasını açmak için [az vm open-port](/cli/azure/vm#open-port) komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-127">Use the [az vm open-port](/cli/azure/vm#open-port) command to open the desired port.</span></span>  
 
 ```azurecli-interactive  
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```


## <a name="connect-to-virtual-machine"></a><span data-ttu-id="b9aa3-128">Sanal makineye bağlanma</span><span class="sxs-lookup"><span data-stu-id="b9aa3-128">Connect to virtual machine</span></span>

<span data-ttu-id="b9aa3-129">Sanal makine bir uzak masaüstü oturumu oluşturmak için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-129">Use the following command to create a remote desktop session with the virtual machine.</span></span> <span data-ttu-id="b9aa3-130">IP adresini, sanal makinenizin genel IP adresi ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-130">Replace the IP address with the public IP address of your virtual machine.</span></span> <span data-ttu-id="b9aa3-131">İstendiğinde, sanal makine oluşturulurken kullanılan kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-131">When prompted, enter the credentials used when creating the virtual machine.</span></span>

```bash 
mstsc /v:<Public IP Address>
```

## <a name="install-iis-using-powershell"></a><span data-ttu-id="b9aa3-132">PowerShell kullanarak IIS yükleme</span><span class="sxs-lookup"><span data-stu-id="b9aa3-132">Install IIS using PowerShell</span></span>

<span data-ttu-id="b9aa3-133">Azure VM’de oturum açtıktan sonra tek bir PowerShell satırı kullanarak IIS yükleyebilir ve web trafiğine izin vermek üzere yerel güvenlik duvarı kuralını etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-133">Now that you have logged in to the Azure VM, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.</span></span> <span data-ttu-id="b9aa3-134">Bir PowerShell istemi açın ve şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b9aa3-134">Open a PowerShell prompt and run the following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="b9aa3-135">IIS karşılama sayfasını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="b9aa3-135">View the IIS welcome page</span></span>

<span data-ttu-id="b9aa3-136">Sanal makinenizde İnternet’ten IIS yüklenmiş ve bağlantı noktası 80 açık olduğunda, varsayılan IIS karşılama sayfasını görüntülemek için seçtiğiniz bir web tarayıcısını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-136">With IIS installed and port 80 now open on your VM from the Internet, you can use a web browser of your choice to view the default IIS welcome page.</span></span> <span data-ttu-id="b9aa3-137">Varsayılan sayfayı ziyaret etmek için yukarıda belgelediğiniz genel IP adresini kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-137">Be sure to use the public IP address you documented above to visit the default page.</span></span> 

![Varsayılan IIS sitesi](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="b9aa3-139">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="b9aa3-139">Clean up resources</span></span>

<span data-ttu-id="b9aa3-140">Artık gerekli değilse, [az group delete](/cli/azure/group#delete) komutunu kullanarak kaynak grubunu, VM’yi ve tüm ilgili kaynakları kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-140">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="b9aa3-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b9aa3-141">Next steps</span></span>

<span data-ttu-id="b9aa3-142">Bu hızlı başlangıçta basit bir sanal makine ve bir ağ güvenlik grubu kuralı dağıtıp, bir web sunucusu yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-142">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="b9aa3-143">Azure sanal makineleri hakkında daha fazla bilgi için Windows VM’lerine yönelik öğreticiye geçin.</span><span class="sxs-lookup"><span data-stu-id="b9aa3-143">To learn more about Azure virtual machines, continue to the tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b9aa3-144">Azure Windows sanal makine öğreticileri</span><span class="sxs-lookup"><span data-stu-id="b9aa3-144">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
