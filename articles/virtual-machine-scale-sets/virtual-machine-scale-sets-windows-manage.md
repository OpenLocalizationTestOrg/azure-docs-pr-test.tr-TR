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
# <a name="manage-virtual-machines-in-a-virtual-machine-scale-set"></a>Bir sanal makine ölçek kümesindeki sanal makineleri yönetme
Bu makale toomanage sanal makineler, sanal makine ölçek kümesindeki Hello görevleri kullanın.

Bir sanal makine ölçek kümesindeki yönetme ile ilgili hello görevlerin çoğunu hello örnek kimliği toomanage istediğiniz hello makinenin bilmeniz gerekir. Kullanabileceğiniz [Azure kaynak Gezgini](https://resources.azure.com) ölçek kümesindeki bir sanal makinenin toofind hello örnek kimliği. Kaynak Gezgini tooverify hello işiniz hello görevlerin durumunu de kullanabilirsiniz.

Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) hello Azure PowerShell'in en son sürümünü yükleme, aboneliğinizi seçme ve tooyour hesabında imzalama hakkında bilgi.

## <a name="display-information-about-a-scale-set"></a>Ölçek kümesi hakkındaki bilgileri görüntüleme
Başvurulan tooas hello örnek görünümünü de olduğu ölçek kümesini hakkında genel bilgi alabilirsiniz. Ya da hello ölçek kümesindeki hello kaynakları hakkındaki bilgiler gibi daha ayrıntılı bilgi alabilirsiniz.

Hello adı veya kaynak grubu ve ayarlayın ve ardından hello komutunu çalıştırmanız Ölçek değerleri tırnak içine alınmış hello değiştirin:

    Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"

Şunun gibi döndürür:

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

Kaynak grubu ve ölçek kümesinin hello adla değerleri tırnak içine alınmış hello değiştirin. Değiştir  *#*  ile hello örneği tanımlayıcısı hello sanal makinesinin hakkında tooget bilgi almak istediğiniz ve ardından çalıştırın:

    Get-AzureRmVmssVM -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

Bu örnek şöyle döndürür:

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

## <a name="start-a-virtual-machine-in-a-scale-set"></a>Ölçek kümesindeki bir sanal makineyi Başlat
Kaynak grubu ve ölçek kümesinin hello adla değerleri tırnak içine alınmış hello değiştirin. Değiştir  *#*  hello tanımlayıcıyla hello sanal makinesinin toostart istediğiniz ve ardından çalıştırın:

    Start-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

Kaynak Gezgini'nde hello durumunun hello örneğinin olduğunu görebiliriz **çalıştıran**:

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

Hello - InstanceId parametresi kullanılarak değil ayarlanır hello ölçeğinde tüm hello sanal makineleri başlatın.

## <a name="stop-a-virtual-machine-in-a-scale-set"></a>Ölçek kümesindeki sanal makineyi durdurma
Kaynak grubu ve ölçek kümesinin hello adla değerleri tırnak içine alınmış hello değiştirin. Değiştir  *#*  hello tanımlayıcıyla hello sanal makinesinin toostop istediğiniz ve ardından çalıştırın:

    Stop-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

Kaynak Gezgini'nde hello durumunun hello örneğinin olduğunu görebiliriz **serbest**:

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

bir sanal makine toostop değil, serbest bırakma, hello - StayProvisioned parametresini kullanın. Merhaba - InstanceId parametresi kullanılarak değil ayarlanır hello tüm hello sanal makinelerin durdurabilirsiniz.

## <a name="restart-a-virtual-machine-in-a-scale-set"></a>Ölçek kümesindeki bir sanal makineyi yeniden başlatın
Kaynak grubu ve hello ölçek kümesini hello adıyla değerleri tırnak içine alınmış hello değiştirin. Değiştir  *#*  hello tanımlayıcıyla hello sanal makinesinin toorestart istediğiniz ve ardından çalıştırın:

    Restart-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

Merhaba - InstanceId parametresi kullanılarak değil ayarlanır hello içindeki tüm hello sanal makineleri yeniden başlatabilirsiniz.

## <a name="remove-a-virtual-machine-from-a-scale-set"></a>Ölçek kümesindeki bir sanal makineyi kaldırma
Kaynak grubu ve hello ölçek kümesini hello adıyla değerleri tırnak içine alınmış hello değiştirin. Değiştir  *#*  hello tanımlayıcıyla hello sanal makinesinin tooremove istediğiniz ve ardından çalıştırın:  

    Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name" -InstanceId #

Merhaba - InstanceId parametre kullanmayan hello sanal makine ölçek kümesi aynı anda kaldırabilirsiniz.

## <a name="change-hello-capacity-of-a-scale-set"></a>Ölçek kümesini Hello kapasitesini değiştirme
Ekleyebilir veya hello kapasite hello kümesinin değiştirerek sanal makineleri kaldırın. Toochange, toobe istediğiniz ve ardından hello yeni kapasiteye sahip hello ölçek kümesini güncelleştir kümesi hello kapasite toowhat istediğiniz hello ölçek kümesini Al. Bu komutlarda, kaynak grubu ve hello ölçek kümesini hello adıyla değerleri tırnak içine alınmış hello değiştirin.

    $vmss = Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
    $vmss.sku.capacity = 5
    Update-AzureRmVmss -ResourceGroupName "resource group name" -Name "scale set name" -VirtualMachineScaleSet $vmss 

Sanal makineler hello ölçek kümesinden kaldırıyorsanız hello sanal makineleri hello yüksek kimlikleri ilk kaldırılır.

