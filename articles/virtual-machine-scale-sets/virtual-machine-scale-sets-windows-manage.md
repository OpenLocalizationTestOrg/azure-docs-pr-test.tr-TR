---
title: "Sanal makine ölçek kümesindeki sanal makineleri aaaManage | Microsoft Docs"
description: "Sanal makineler Azure PowerShell kullanarak bir sanal makine ölçek yönetin."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d35fa77a-de96-4ccd-a332-eb181d1f4273
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 7d848729c0fc708bd596b61feb528cf4bf4bafd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="f44ef-103">Bir sanal makine ölçek kümesindeki sanal makineleri yönetme</span><span class="sxs-lookup"><span data-stu-id="f44ef-103">Manage virtual machines in a virtual machine scale set</span></span>
<span data-ttu-id="f44ef-104">Bu makale toomanage sanal makineler, sanal makine ölçek kümesindeki Hello görevleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="f44ef-104">Use hello tasks in this article toomanage virtual machines in your virtual machine scale set.</span></span>

<span data-ttu-id="f44ef-105">Bir sanal makine ölçek kümesindeki yönetme ile ilgili hello görevlerin çoğunu hello örnek kimliği toomanage istediğiniz hello makinenin bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f44ef-105">Most of hello tasks that involve managing a virtual machine in a scale set require that you know hello instance ID of hello machine that you want toomanage.</span></span> <span data-ttu-id="f44ef-106">Kullanabileceğiniz [Azure kaynak Gezgini](https://resources.azure.com) ölçek kümesindeki bir sanal makinenin toofind hello örnek kimliği.</span><span class="sxs-lookup"><span data-stu-id="f44ef-106">You can use [Azure Resource Explorer](https://resources.azure.com) toofind hello instance ID of a virtual machine in a scale set.</span></span> <span data-ttu-id="f44ef-107">Kaynak Gezgini tooverify hello işiniz hello görevlerin durumunu de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f44ef-107">You also use Resource Explorer tooverify hello status of hello tasks that you finish.</span></span>

<span data-ttu-id="f44ef-108">Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) hello Azure PowerShell'in en son sürümünü yükleme, aboneliğinizi seçme ve tooyour hesabında imzalama hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="f44ef-108">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>

## <a name="display-information-about-a-scale-set"></a><span data-ttu-id="f44ef-109">Ölçek kümesi hakkındaki bilgileri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="f44ef-109">Display information about a scale set</span></span>
<span data-ttu-id="f44ef-110">Başvurulan tooas hello örnek görünümünü de olduğu ölçek kümesini hakkında genel bilgi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f44ef-110">You can get general information about a scale set, which is also referred tooas hello instance view.</span></span> <span data-ttu-id="f44ef-111">Ya da hello ölçek kümesindeki hello kaynakları hakkındaki bilgiler gibi daha ayrıntılı bilgi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f44ef-111">Or, you can get more specific information, such as information about hello resources in hello scale set.</span></span>

<span data-ttu-id="f44ef-112">Hello adı veya kaynak grubu ve ayarlayın ve ardından hello komutunu çalıştırmanız Ölçek değerleri tırnak içine alınmış hello değiştirin:</span><span class="sxs-lookup"><span data-stu-id="f44ef-112">Replace hello quoted values with hello name or your resource group and scale set and then run hello command:</span></span>

    Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"

<span data-ttu-id="f44ef-113">Şunun gibi döndürür:</span><span class="sxs-lookup"><span data-stu-id="f44ef-113">It returns something like this:</span></span>

    Id                                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/myvmss1
    Name                                        : myvmss1
    Type                                        : Microsoft.Compute/virtualMachineScaleSets
    Location                                    : centralus
    Sku                                         :
      Name                                      : Standard_A0
      Tier                                      : Standard
      Capacity                                  : 3
    UpgradePolicy                               :
      Mode                                      : Manual
    VirtualMachineProfile                       :
      OsProfile                                 :
        ComputerNamePrefix                      : vmss1
        AdminUsername                           : admin1
        WindowsConfiguration                    :
          ProvisionVMAgent                      : True
          EnableAutomaticUpdates                : True
    StorageProfile                              :
      ImageReference                            :
        Publisher                               : MicrosoftWindowsServer
        Offer                                   : WindowsServer
        Sku                                     : 2012-R2-Datacenter
        Version                                 : latest
      OsDisk                                    :
        Name                                    : vmssosdisk
        Caching                                 : ReadOnly
        CreateOption                            : FromImage
        VhdContainers[0]                        : https://astore.blob.core.windows.net/vmss
        VhdContainers[1]                        : https://gstore.blob.core.windows.net/vmss
        VhdContainers[2]                        : https://mstore.blob.core.windows.net/vmss
        VhdContainers[3]                        : https://sstore.blob.core.windows.net/vmss
        VhdContainers[4]                        : https://ystore.blob.core.windows.net/vmss
    NetworkProfile                              :
      NetworkInterfaceConfigurations[0]         :
        Name                                    : mync1
        Primary                                 : True
        IpConfigurations[0]                     :
          Name                                  : ip1
          Subnet                                :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/virtualNetworks/myvn1/subnets/mysn1
          LoadBalancerBackendAddressPools[0]    :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/backendAddressPools/bepool1
        LoadBalancerInboundNatPools[0]          :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/inboundNatPools/natpool1
    ExtensionProfile                            :
      Extensions[0]                             :
        Name                                    : Microsoft.Insights.VMDiagnosticsSettings
        Publisher                               : Microsoft.Azure.Diagnostics
        Type                                    : IaaSDiagnostics
        TypeHandlerVersion                      : 1.5
        AutoUpgradeMinorVersion                 : True
        Settings                                : {"xmlCfg":"...","storageAccount":"astore"}
    ProvisioningState                           : Succeeded

<span data-ttu-id="f44ef-114">Kaynak grubu ve ölçek kümesinin hello adla değerleri tırnak içine alınmış hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f44ef-114">Replace hello quoted values with hello name of your resource group and scale set.</span></span> <span data-ttu-id="f44ef-115">Değiştir  *#*  ile hello örneği tanımlayıcısı hello sanal makinesinin hakkında tooget bilgi almak istediğiniz ve ardından çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f44ef-115">Replace *#* with hello instance identifier of hello virtual machine that you want tooget information about and then run it:</span></span>

    Get-AzureRmVmssVM -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="f44ef-116">Bu örnek şöyle döndürür:</span><span class="sxs-lookup"><span data-stu-id="f44ef-116">It returns something like this example:</span></span>

    Id                            : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/
                                    virtualMachineScaleSets/myvmss1/virtualMachines/0
    Name                          : myvmss1_0
    Type                          : Microsoft.Compute/virtualMachineScaleSets/virtualMachines
    Location                      : centralus
    InstanceId                    : 0
    Sku                           :
      Name                        : Standard_A0
      Tier                        : Standard
    LatestModelApplied            : True
    StorageProfile                :
      ImageReference              :
        Publisher                 : MicrosoftWindowsServer
        Offer                     : WindowsServer
        Sku                       : 2012-R2-Datacenter
        Version                   : 4.0.20160617
      OsDisk                      :
        OsType                    : Windows
        Name                      : vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8
        Vhd                       :
          Uri                     : https://astore.blob.core.windows.net/vmss/vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8.vhd
        Caching                   : ReadOnly
        CreateOption              : FromImage
    OsProfile                     :
      ComputerName                : myvmss1-0
      AdminUsername               : admin1
      WindowsConfiguration        :
        ProvisionVMAgent          : True
        EnableAutomaticUpdates    : True
    NetworkProfile                :
      NetworkInterfaces[0]        :
        Id                        : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/
                                    myvmss1/virtualMachines/0/networkInterfaces/mync1
    ProvisioningState             : Succeeded
    Resources[0]                  :
      Id                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachines/
                                    myvmss1_0/extensions/Microsoft.Insights.VMDiagnosticsSettings
      Name                        : Microsoft.Insights.VMDiagnosticsSettings
      Type                        : Microsoft.Compute/virtualMachines/extensions
      Location                    : centralus
      Publisher                   : Microsoft.Azure.Diagnostics
      VirtualMachineExtensionType : IaaSDiagnostics
      TypeHandlerVersion          : 1.5
      AutoUpgradeMinorVersion     : True
      Settings                    : {"xmlCfg":"...","storageAccount":"astore"}
      ProvisioningState           : Succeeded

## <a name="start-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="f44ef-117">Ölçek kümesindeki bir sanal makineyi Başlat</span><span class="sxs-lookup"><span data-stu-id="f44ef-117">Start a virtual machine in a scale set</span></span>
<span data-ttu-id="f44ef-118">Kaynak grubu ve ölçek kümesinin hello adla değerleri tırnak içine alınmış hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f44ef-118">Replace hello quoted values with hello name of your resource group and scale set.</span></span> <span data-ttu-id="f44ef-119">Değiştir  *#*  hello tanımlayıcıyla hello sanal makinesinin toostart istediğiniz ve ardından çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f44ef-119">Replace *#* with hello identifier of hello virtual machine that you want toostart and then run it:</span></span>

    Start-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="f44ef-120">Kaynak Gezgini'nde hello durumunun hello örneğinin olduğunu görebiliriz **çalıştıran**:</span><span class="sxs-lookup"><span data-stu-id="f44ef-120">In Resource Explorer, we can see that hello status of hello instance is **running**:</span></span>

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T02:10:08.0730839+00:00"
      },
      {
        "code": "PowerState/running",
        "level": "Info",
        "displayStatus": "VM running"
      }
    ]

<span data-ttu-id="f44ef-121">Hello - InstanceId parametresi kullanılarak değil ayarlanır hello ölçeğinde tüm hello sanal makineleri başlatın.</span><span class="sxs-lookup"><span data-stu-id="f44ef-121">You can start all hello virtual machines in hello scale set by not using hello -InstanceId parameter.</span></span>

## <a name="stop-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="f44ef-122">Ölçek kümesindeki sanal makineyi durdurma</span><span class="sxs-lookup"><span data-stu-id="f44ef-122">Stop a virtual machine in a scale set</span></span>
<span data-ttu-id="f44ef-123">Kaynak grubu ve ölçek kümesinin hello adla değerleri tırnak içine alınmış hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f44ef-123">Replace hello quoted values with hello name of your resource group and scale set.</span></span> <span data-ttu-id="f44ef-124">Değiştir  *#*  hello tanımlayıcıyla hello sanal makinesinin toostop istediğiniz ve ardından çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f44ef-124">Replace *#* with hello identifier of hello virtual machine that you want toostop and then run it:</span></span>

    Stop-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="f44ef-125">Kaynak Gezgini'nde hello durumunun hello örneğinin olduğunu görebiliriz **serbest**:</span><span class="sxs-lookup"><span data-stu-id="f44ef-125">In Resource Explorer, we can see that hello status of hello instance is **deallocated**:</span></span>

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T01:25:17.8792929+00:00"
      },
      {
        "code": "PowerState/deallocated",
        "level": "Info",
        "displayStatus": "VM deallocated"
      }
    ]

<span data-ttu-id="f44ef-126">bir sanal makine toostop değil, serbest bırakma, hello - StayProvisioned parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f44ef-126">toostop a virtual machine and not deallocate it, use hello -StayProvisioned parameter.</span></span> <span data-ttu-id="f44ef-127">Merhaba - InstanceId parametresi kullanılarak değil ayarlanır hello tüm hello sanal makinelerin durdurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f44ef-127">You can stop all hello virtual machines in hello set by not using hello -InstanceId parameter.</span></span>

## <a name="restart-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="f44ef-128">Ölçek kümesindeki bir sanal makineyi yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="f44ef-128">Restart a virtual machine in a scale set</span></span>
<span data-ttu-id="f44ef-129">Kaynak grubu ve hello ölçek kümesini hello adıyla değerleri tırnak içine alınmış hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f44ef-129">Replace hello quoted values with hello name of your resource group and hello scale set.</span></span> <span data-ttu-id="f44ef-130">Değiştir  *#*  hello tanımlayıcıyla hello sanal makinesinin toorestart istediğiniz ve ardından çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f44ef-130">Replace *#* with hello identifier of hello virtual machine that you want toorestart and then run it:</span></span>

    Restart-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="f44ef-131">Merhaba - InstanceId parametresi kullanılarak değil ayarlanır hello içindeki tüm hello sanal makineleri yeniden başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f44ef-131">You can restart all hello virtual machines in hello set by not using hello -InstanceId parameter.</span></span>

## <a name="remove-a-virtual-machine-from-a-scale-set"></a><span data-ttu-id="f44ef-132">Ölçek kümesindeki bir sanal makineyi kaldırma</span><span class="sxs-lookup"><span data-stu-id="f44ef-132">Remove a virtual machine from a scale set</span></span>
<span data-ttu-id="f44ef-133">Kaynak grubu ve hello ölçek kümesini hello adıyla değerleri tırnak içine alınmış hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f44ef-133">Replace hello quoted values with hello name of your resource group and hello scale set.</span></span> <span data-ttu-id="f44ef-134">Değiştir  *#*  hello tanımlayıcıyla hello sanal makinesinin tooremove istediğiniz ve ardından çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f44ef-134">Replace *#* with hello identifier of hello virtual machine that you want tooremove and then run it:</span></span>  

    Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="f44ef-135">Merhaba - InstanceId parametre kullanmayan hello sanal makine ölçek kümesi aynı anda kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f44ef-135">You can remove hello virtual machine scale set all at once by not using hello -InstanceId parameter.</span></span>

## <a name="change-hello-capacity-of-a-scale-set"></a><span data-ttu-id="f44ef-136">Ölçek kümesini Hello kapasitesini değiştirme</span><span class="sxs-lookup"><span data-stu-id="f44ef-136">Change hello capacity of a scale set</span></span>
<span data-ttu-id="f44ef-137">Ekleyebilir veya hello kapasite hello kümesinin değiştirerek sanal makineleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="f44ef-137">You can add or remove virtual machines by changing hello capacity of hello set.</span></span> <span data-ttu-id="f44ef-138">Toochange, toobe istediğiniz ve ardından hello yeni kapasiteye sahip hello ölçek kümesini güncelleştir kümesi hello kapasite toowhat istediğiniz hello ölçek kümesini Al.</span><span class="sxs-lookup"><span data-stu-id="f44ef-138">Get hello scale set that you want toochange, set hello capacity toowhat you want it toobe, and then update hello scale set with hello new capacity.</span></span> <span data-ttu-id="f44ef-139">Bu komutlarda, kaynak grubu ve hello ölçek kümesini hello adıyla değerleri tırnak içine alınmış hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f44ef-139">In these commands, replace hello quoted values with hello name of your resource group and hello scale set.</span></span>

    $vmss = Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
    $vmss.sku.capacity = 5
    Update-AzureRmVmss -ResourceGroupName "resource group name" -Name "scale set name" -VirtualMachineScaleSet $vmss 

<span data-ttu-id="f44ef-140">Sanal makineler hello ölçek kümesinden kaldırıyorsanız hello sanal makineleri hello yüksek kimlikleri ilk kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="f44ef-140">If you are removing virtual machines from hello scale set, hello virtual machines with hello highest ids are removed first.</span></span>

