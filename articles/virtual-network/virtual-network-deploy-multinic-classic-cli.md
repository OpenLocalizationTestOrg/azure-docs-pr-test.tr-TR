---
title: "aaaCreate birden çok NIC - Azure CLI 1.0'yle bir VM'yi (Klasik) | Microsoft Docs"
description: "Nasıl toocreate (Klasik) kullanarak birden çok NIC ile VM hello Azure komut satırı arabirimi (CLI) 1.0 öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b436e41e-866c-439f-a7c7-7b4b041725ef
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 181bfb28027caff33410ca94744e79206a2a0d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="eca4d-103">Hello Azure CLI 1.0 kullanarak birden çok NIC ile VM (Klasik) oluşturun</span><span class="sxs-lookup"><span data-stu-id="eca4d-103">Create a VM (Classic) with multiple NICs using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="eca4d-104">Sanal makineler (VM'ler) oluşturma ve birden çok ağ arabirimlerine (NIC'ler) tooeach, VM'lerin ekleyin.</span><span class="sxs-lookup"><span data-stu-id="eca4d-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="eca4d-105">Birden çok NIC NIC'ler arasında trafik türlerini ayrılması etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="eca4d-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="eca4d-106">Örneğin, bir başka yalnızca iç kaynakları ile iletişim kurar değil sırada NIC hello Internet ile iletişim kurabileceği toohello Internet bağlı.</span><span class="sxs-lookup"><span data-stu-id="eca4d-106">For example, one NIC might communicate with hello Internet, while another communicates only with internal resources not connected toohello Internet.</span></span> <span data-ttu-id="eca4d-107">Merhaba özelliği tooseparate ağ trafiği birden çok NIC boyunca uygulama sunma ve WAN iyileştirmesi çözümleri gibi birçok ağ sanal uygulamaları için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="eca4d-107">hello ability tooseparate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eca4d-108">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="eca4d-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="eca4d-109">Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="eca4d-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="eca4d-110">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="eca4d-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="eca4d-111">Bilgi nasıl tooperform hello kullanarak şu adımları [Resource Manager dağıtım modeli](virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="eca4d-111">Learn how tooperform these steps using hello [Resource Manager deployment model](virtual-network-deploy-multinic-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="eca4d-112">Merhaba aşağıdaki adımları kullanın adlı bir kaynak grubu *IaaSStory* hello WEB sunucuları ve bir kaynak grubu için adlı *IaaSStory arka uç* hello DB sunucuları için.</span><span class="sxs-lookup"><span data-stu-id="eca4d-112">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eca4d-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="eca4d-113">Prerequisites</span></span>
<span data-ttu-id="eca4d-114">DB sunucuları hello oluşturabilmeniz için önce toocreate hello gerekir *IaaSStory* hello gereken tüm kaynakların bu senaryo için kaynak grubuyla.</span><span class="sxs-lookup"><span data-stu-id="eca4d-114">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="eca4d-115">Bu kaynaklar, tam izleyin adımları hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="eca4d-115">toocreate these resources, complete hello steps that follow.</span></span> <span data-ttu-id="eca4d-116">Merhaba hello adımları izleyerek bir sanal ağ oluşturma [bir sanal ağ oluşturma](virtual-networks-create-vnet-classic-cli.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="eca4d-116">Create a virtual network by following hello steps in hello [Create a virtual network](virtual-networks-create-vnet-classic-cli.md) article.</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="deploy-hello-back-end-vms"></a><span data-ttu-id="eca4d-117">Merhaba arka uç dağıtmak VM'ler</span><span class="sxs-lookup"><span data-stu-id="eca4d-117">Deploy hello back-end VMs</span></span>
<span data-ttu-id="eca4d-118">Merhaba arka uç VM'ler kaynakları aşağıdaki hello hello oluşturulmasına bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="eca4d-118">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="eca4d-119">**Veri diskleri için depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="eca4d-119">**Storage account for data disks**.</span></span> <span data-ttu-id="eca4d-120">Daha iyi performans için premium depolama hesabı gerektirir katı hal sürücüsü (SSD) teknolojisi hello veritabanı sunucularında hello veri diski kullanır.</span><span class="sxs-lookup"><span data-stu-id="eca4d-120">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="eca4d-121">Emin hello toosupport premium depolama dağıttığınız Azure konumu olun.</span><span class="sxs-lookup"><span data-stu-id="eca4d-121">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="eca4d-122">**NIC**.</span><span class="sxs-lookup"><span data-stu-id="eca4d-122">**NICs**.</span></span> <span data-ttu-id="eca4d-123">Her VM veritabanı erişimi için iki NIC gerekir ve yönetimi için bir tane.</span><span class="sxs-lookup"><span data-stu-id="eca4d-123">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="eca4d-124">**Kullanılabilirlik kümesi**.</span><span class="sxs-lookup"><span data-stu-id="eca4d-124">**Availability set**.</span></span> <span data-ttu-id="eca4d-125">Tüm veritabanı sunucuları tooa tek kullanılabilirlik kümesi eklenir, tooensure hello VM'ler en az biri hazır ve çalışır bakımı sırasında.</span><span class="sxs-lookup"><span data-stu-id="eca4d-125">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="eca4d-126">1. adım - kodunuzu Başlat</span><span class="sxs-lookup"><span data-stu-id="eca4d-126">Step 1 - Start your script</span></span>
<span data-ttu-id="eca4d-127">Kullanılan hello tam bash komut dosyası indirebilirsiniz [burada](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span><span class="sxs-lookup"><span data-stu-id="eca4d-127">You can download hello full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span></span> <span data-ttu-id="eca4d-128">Aşağıdaki adımları toochange hello betik toowork ortamınızdaki hello tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="eca4d-128">Complete hello following steps toochange hello script toowork in your environment:</span></span>

1. <span data-ttu-id="eca4d-129">Değiştirme hello değişkenlerin değerleri yukarıda dağıtılmış varolan kaynak grubunuz göre hello aşağıdaki [Önkoşullar](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="eca4d-129">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    location="useast2"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    ```
2. <span data-ttu-id="eca4d-130">Merhaba değerlerini değiştirin arka uç dağıtımınız için toouse istediğiniz hello değişkenleri aşağıdaki hello değerlerine göre.</span><span class="sxs-lookup"><span data-stu-id="eca4d-130">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```azurecli
    backendCSName="IaaSStory-Backend"
    prmStorageAccountName="iaasstoryprmstorage"
    image="0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskPrefix="db"
    dataDiskName="datadisk"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="eca4d-131">2. adım - Vm'leriniz için gerekli kaynakları oluşturma</span><span class="sxs-lookup"><span data-stu-id="eca4d-131">Step 2 - Create necessary resources for your VMs</span></span>
1. <span data-ttu-id="eca4d-132">Tüm arka uç VM'ler için yeni bir bulut hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="eca4d-132">Create a new cloud service for all backend VMs.</span></span> <span data-ttu-id="eca4d-133">Bildirim hello hello kullanımını `$backendCSName` hello kaynak grubu adı için değişken ve `$location` hello Azure bölgesi için.</span><span class="sxs-lookup"><span data-stu-id="eca4d-133">Notice hello use of hello `$backendCSName` variable for hello resource group name, and `$location` for hello Azure region.</span></span>

    ```azurecli
    azure service create --serviceName $backendCSName \
        --location $location
    ```

2. <span data-ttu-id="eca4d-134">Premium depolama hesabı hello işletim sistemi için ve veri diskleri toobe sizin tarafından VM'ler kullanılan oluşturun.</span><span class="sxs-lookup"><span data-stu-id="eca4d-134">Create a premium storage account for hello OS and data disks toobe used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --location $location \
        --type PLRS
    ```

### <a name="step-3---create-vms-with-multiple-nics"></a><span data-ttu-id="eca4d-135">3. adım - VMs birden çok NIC ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="eca4d-135">Step 3 - Create VMs with multiple NICs</span></span>
1. <span data-ttu-id="eca4d-136">Döngü toocreate üzerinde hello göre birden çok VM Başlat `numberOfVMs` değişkenleri.</span><span class="sxs-lookup"><span data-stu-id="eca4d-136">Start a loop toocreate multiple VMs, based on hello `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="eca4d-137">Her bir VM hello adını ve her bir hello iki NIC IP adresi belirtin.</span><span class="sxs-lookup"><span data-stu-id="eca4d-137">For each VM, specify hello name and IP address of each of hello two NICs.</span></span>

    ```azurecli
    nic1Name=$vmNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x

    nic2Name=$vmNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    ```

3. <span data-ttu-id="eca4d-138">Merhaba VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="eca4d-138">Create hello VM.</span></span> <span data-ttu-id="eca4d-139">Fark hello hello kullanımını `--nic-config` adı, alt ağ ve IP adresi ile tüm NIC listesini içeren parametresi.</span><span class="sxs-lookup"><span data-stu-id="eca4d-139">Notice hello usage of hello `--nic-config` parameter, containing a list of all NICs with name, subnet, and IP address.</span></span>

    ```azurecli
    azure vm create $backendCSName $image $username $password \
        --connect $backendCSName \
        --vm-name $vmNamePrefix$suffixNumber \
        --vm-size $vmSize \
        --availability-set $avSetName \
        --blob-url $prmStorageAccountName.blob.core.windows.net/vhds/$osDiskName$suffixNumber.vhd \
        --virtual-network-name $vnetName \
        --subnet-names $backendSubnetName \
        --nic-config $nic1Name:$backendSubnetName:$ipAddress1::,$nic2Name:$backendSubnetName:$ipAddress2::
    ```

4. <span data-ttu-id="eca4d-140">Her bir VM, iki veri diski oluşturun.</span><span class="sxs-lookup"><span data-stu-id="eca4d-140">For each VM, create two data disks.</span></span>

    ```azurecli
    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-1.vhd

    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-2.vhd
    done
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="eca4d-141">Adım 4 - çalışma hello komut dosyası</span><span class="sxs-lookup"><span data-stu-id="eca4d-141">Step 4 - Run hello script</span></span>
<span data-ttu-id="eca4d-142">İndirilen ve hello betik hello betik toocreate hello geri çalıştırmak gereksinimlerinize göre değişti birden çok NIC içeren veritabanı VM'ler sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="eca4d-142">Now that you downloaded and changed hello script based on your needs, run hello script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="eca4d-143">Komut dosyanızı kaydedin ve çalıştırın, **Bash** terminal.</span><span class="sxs-lookup"><span data-stu-id="eca4d-143">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="eca4d-144">Merhaba ilk çıktısı, aşağıda gösterildiği gibi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="eca4d-144">You will see hello initial output, as shown below.</span></span>

        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name IaaSStory-Backend
        info:    service create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM

2. <span data-ttu-id="eca4d-145">Birkaç dakika sonra hello yürütme sona erer ve hello rest aşağıda gösterildiği gibi hello çıktısını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="eca4d-145">After a few minutes, hello execution will end and you will see hello rest of hello output as shown below.</span></span>

        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM
        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
