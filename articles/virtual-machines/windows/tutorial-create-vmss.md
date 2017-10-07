---
title: "bir sanal makine ölçek kümeleri için Windows Azure aaaCreate | Microsoft Docs"
description: "Windows sanal makine ölçek kümesini kullanarak sanal makineleri üzerinde yüksek oranda kullanılabilir bir uygulama oluşturun ve dağıtın"
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
ms.devlang: 
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: a3914571005c28a492c069d880992630851afae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-windows"></a>Bir sanal makine ölçek kümesi oluşturma ve yüksek oranda kullanılabilir bir Windows uygulamasını dağıtma
Bir sanal makine ölçek kümesi toodeploy sağlar ve aynı, otomatik ölçeklendirme sanal makineler kümesi yönetin. Merhaba hello ölçek kümesindeki VM'lerin sayısını elle ölçeklendirme ya da CPU kullanımı, bellek isteğe bağlı veya ağ trafiğini dayalı kurallar tooautoscale tanımlayabilirsiniz. Bu öğreticide, Azure üzerinde ayarlanmış bir sanal makine ölçek dağıtın. Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:

> [!div class="checklist"]
> * Merhaba özel betik uzantısının toodefine bir IIS site tooscale kullanın
> * Ölçek kümesi için bir yük dengeleyici oluşturma
> * Bir sanal makine ölçek kümesi oluşturma
> * Artırma veya azaltma hello ölçek kümesi örneği sayısı
> * Otomatik ölçeklendirme kuralları oluşturma

Bu öğretici hello Azure PowerShell modülü 3,6 veya sonraki bir sürümü gerektiriyor. Çalıştırma ` Get-Module -ListAvailable AzureRM` toofind hello sürümü. Tooupgrade gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).


## <a name="scale-set-overview"></a>Ölçek kümesi'ne genel bakış
Ölçek kümeleri kullanan benzer kavram, hakkında hello önceki öğreticide çok öğrenilen[yüksek oranda kullanılabilir sanal makineleri oluşturmak](tutorial-availability-sets.md). VM ölçek kümesindeki bir kullanılabilirlik kümesindeki sanal makineleri gibi arıza ve güncelleştirme etki alanları arasında dağıtılır.

VM ölçek kümesindeki gerektiği şekilde oluşturulur. Otomatik ölçeklendirme kurallarını toocontrol tanımladığınız nasıl ve ne zaman VM'ler eklenir veya hello ölçek kümesinden kaldırılır. Bu kurallar temel alınarak ölçümleri CPU yükünü, bellek kullanımı veya ağ trafiğini gibi tetikleyebilir.

Ölçek too1, Azure platform görüntüsü kullandığınızda 000 VM'ler desteği ayarlar. Önemli yükleme veya VM özelleştirme gereksinimleri ile iş yükleri için çok isteyebilir[özel bir VM görüntüsü oluşturma](tutorial-custom-images.md). Özel görüntü kullanırken ayarlayın ölçeğinde too100 Vm'leri yedekleme oluşturabilirsiniz.


## <a name="create-an-app-tooscale"></a>Bir uygulama tooscale oluşturma
Ölçek kümesini oluşturmadan önce bir kaynak grubuyla oluşturmanız [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroupAutomate* hello içinde *EastUS* konumu:

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupScaleSet -Location EastUS
```

Önceki bir öğreticide, nasıl çok öğrenilen[otomatikleştirmek VM Yapılandırması](tutorial-automate-vm-deployment.md) kullanarak hello özel betik uzantısı. Ölçek kümesi yapılandırması oluşturun, sonra özel betik uzantısının tooinstall uygulamak ve IIS yapılandırma:

```powershell
# Create a config object
$vmssConfig = New-AzureRmVmssConfig `
    -Location EastUS `
    -SkuCapacity 2 `
    -SkuName Standard_DS2 `
    -UpgradePolicyMode Automatic

# Define hello script for your Custom Script Extension toorun
$publicSettings = @{
    "fileUris" = (,"https://raw.githubusercontent.com/iainfoulds/azure-samples/master/automate-iis.ps1");
    "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File automate-iis.ps1"
}

# Use Custom Script Extension tooinstall IIS and configure basic website
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig `
    -Name "customScript" `
    -Publisher "Microsoft.Compute" `
    -Type "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -Setting $publicSettings
```

## <a name="create-scale-load-balancer"></a>Ölçek yük dengeleyici oluşturma
Bir Azure yük dengeleyici gelen trafiği sağlıklı VM'ler arasında dağıtarak yüksek kullanılabilirlik sağlayan bir katman 4 (TCP, UDP) yük dengeleyicidir. Bir yük dengeleyici durum araştırması her VM üzerinde belirli bir bağlantı noktasını izler ve yalnızca trafik tooan dağıtır işletimsel VM. Daha fazla bilgi için hello sonraki öğretici bakın [nasıl tooload Bakiye Windows sanal makineleri](tutorial-load-balancer.md).

Bir ortak IP adresi ve bağlantı noktası 80 üzerinde web trafiği dağıtan bir yük dengeleyicisi oluşturun:

```powershell
# Create a public IP address
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupScaleSet `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP

# Create a frontend and backend IP pool
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool

# Create hello load balancer
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool

# Create a load balancer health probe on port 80
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2

# Create a load balancer rule toodistribute traffic on port 80
Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80

# Update hello load balancer configuration
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="create-a-scale-set"></a>Bir ölçek kümesi oluşturma
Şimdi bir sanal makine ölçek kümesi oluşturmak [yeni AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm). Merhaba aşağıdaki örnekte oluşturur ölçeği adlandırılmış Ayarla *myScaleSet*:

```powershell
# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig `
  -ImageReferencePublisher MicrosoftWindowsServer `
  -ImageReferenceOffer WindowsServer `
  -ImageReferenceSku 2016-Datacenter `
  -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig `
  -AdminUsername azureuser `
  -AdminPassword P@ssword! `
  -ComputerNamePrefix myVM

# Create hello virtual network resources
$subnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name "mySubnet" `
  -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName "myResourceGroupScaleSet" `
  -Name "myVnet" `
  -Location "EastUS" `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $subnet
$ipConfig = New-AzureRmVmssIpConfig `
  -Name "myIPConfig" `
  -LoadBalancerBackendAddressPoolsId $lb.BackendAddressPools[0].Id `
  -SubnetId $vnet.Subnets[0].Id

# Attach hello virtual network toohello config object
Add-AzureRmVmssNetworkInterfaceConfiguration `
  -VirtualMachineScaleSet $vmssConfig `
  -Name "network-config" `
  -Primary $true `
  -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myScaleSet `
  -VirtualMachineScaleSet $vmssConfig
```

Birkaç dakika toocreate alır ve tüm hello ölçek kümesi kaynakları ve VM'ler yapılandırın.


## <a name="test-your-app"></a>Uygulamanızı test etme
toosee, IIS Web sitesi eylem elde hello genel IP adresi, yük dengeleyici ile [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Merhaba aşağıdaki örnek alacağı için başlangıç IP adresi *myPublicIP* hello ölçek kümesinin bir parçası olarak oluşturulan:

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupScaleSet -Name myPublicIP | select IpAddress
```

Tooa web tarayıcısında Hello genel IP adresi girin. VM bu hello yük dengeleyici dağıtılmış trafiği hello hello ana dahil olmak üzere Hello uygulama görüntülenir:

![Çalışan IIS sitesi](./media/tutorial-create-vmss/running-iis-site.png)

toosee hello ölçeği, eylemde ayarla, zorla yenileme web tarayıcısı toosee hello yük dengeleyici, uygulamanızı çalıştıran tüm hello VM'ler arasında trafiği dağıtın.


## <a name="management-tasks"></a>Yönetim görevleri
Merhaba ölçek kümesini Hello yaşam döngüsü boyunca toorun gerekebilir bir veya daha fazla yönetim görevleri. Ayrıca, çeşitli yaşam döngüsü görevleri otomatikleştiren toocreate komut dosyaları isteyebilirsiniz. Azure PowerShell Bu görevleri hızlı şekilde toodo sağlar. Birkaç ortak görevler şunlardır.

### <a name="view-vms-in-a-scale-set"></a>Görünüm VM ölçek kümesindeki
tooview, Ölçek çalışan sanal makineler listesi ayarlayabilir, kullanabilir [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) gibi:

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Loop through hello instanaces in your scale set
for ($i=1; $i -le ($scaleset.Sku.Capacity - 1); $i++) {
    Get-AzureRmVmssVM -ResourceGroupName myResourceGroupScaleSet `
      -VMScaleSetName myScaleSet `
      -InstanceId $i
}
```


### <a name="increase-or-decrease-vm-instances"></a>Artırma veya azaltma VM örnekleri
toosee hello örnek sayısı, şu anda bir ölçek kümesindeki, kullanın [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) ve sorgulayın *sku.capacity*:

```powershell
Get-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -VMScaleSetName myScaleSet | `
    Select -ExpandProperty Sku
```

Daha sonra el ile artırabilir veya sanal makineler kümesi hello ölçeğinde hello sayısını azaltmak [güncelleştirme AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss). Merhaba aşağıdaki örnek hello sayısını VM'ler, ölçeği çok ayarla ayarlar*5*:

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Set and update hello capacity of your scale set
$scaleset.sku.capacity = 5
Update-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -Name myScaleSet `
    -VirtualMachineScaleSet $scaleset
```

Alır örneği sayısı birkaç dakika tooupdate hello belirttiyseniz, Ölçek kümesi.


### <a name="configure-autoscale-rules"></a>Otomatik ölçeklendirme kurallarını yapılandırma
El ile Merhaba örnek sayısı, Ölçek ölçeklendirmesini Ayarla yerine otomatik ölçeklendirme kurallarını tanımlayın. Bu kurallar, Ölçek durumlarda ayarlayın ve buna göre ölçümleri ve tanımladığınız eşikleri göre yanıt hello izleyin. Hello ortalama CPU yükü 5 dakikalık bir süre içinde % 60'den büyük olduğunda aşağıdaki örneğine hello tarafından hello örneklerinin sayısını ölçeklendirir. Merhaba ortalama CPU yükü daha sonra 5 dakikalık bir süre içinde % 30 düşerse hello örnekleri içinde bir örneği tarafından ölçeklenir:

```powershell
# Define your scale set information
$mySubscriptionId = (Get-AzureRmSubscription).Id
$myResourceGroup = "myResourceGroupScaleSet"
$myScaleSet = "myScaleSet"
$myLocation = "East US"

# Create a scale up rule tooincrease hello number instances after 60% average CPU usage exceeded for a 5 minute period
$myRuleScaleUp = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator GreaterThan `
  -MetricStatistic Average `
  -Threshold 60 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Increase `
  -ScaleActionValue 1

# Create a scale down rule toodecrease hello number of instances after 30% average CPU usage over a 5 minute period
$myRuleScaleDown = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator LessThan `
  -MetricStatistic Average `
  -Threshold 30 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Decrease `
  -ScaleActionValue 1

# Create a scale profile with your scale up and scale down rules
$myScaleProfile = New-AzureRmAutoscaleProfile `
  -DefaultCapacity 2  `
  -MaximumCapacity 10 `
  -MinimumCapacity 2 `
  -Rules $myRuleScaleUp,$myRuleScaleDown `
  -Name "autoprofile"

# Apply hello autoscale rules
Add-AzureRmAutoscaleSetting `
  -Location $myLocation `
  -Name "autosetting" `
  -ResourceGroup $myResourceGroup `
  -TargetResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -AutoscaleProfiles $myScaleProfile
```


## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, bir sanal makine ölçek kümesi oluşturuldu. Şunları öğrendiniz:

> [!div class="checklist"]
> * Merhaba özel betik uzantısının toodefine bir IIS site tooscale kullanın
> * Ölçek kümesi için bir yük dengeleyici oluşturma
> * Bir sanal makine ölçek kümesi oluşturma
> * Artırma veya azaltma hello ölçek kümesi örneği sayısı
> * Otomatik ölçeklendirme kuralları oluşturma

Toohello sonraki öğretici toolearn Yük Dengeleme sanal makineler için kavramları hakkında daha fazla ilerleyin.

> [!div class="nextstepaction"]
> [Sanal makinelerin yük dengelemesini](tutorial-load-balancer.md)
