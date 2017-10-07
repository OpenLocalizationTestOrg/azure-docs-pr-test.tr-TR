---
title: "aaaCreate bir Azure sanal makine ölçek kümesi | Microsoft Docs"
description: "Oluşturun ve Azure CLI, PowerShell, şablon veya Visual Studio ile ayarlanmış bir Linux veya Windows Azure sanal makine ölçek dağıtın."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 07/21/2017
ms.author: adegeo
ms.openlocfilehash: 73de25c1dd2424e64655b3accfea848926e72f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-a-virtual-machine-scale-set"></a>Oluşturma ve bir sanal makine ölçek kümesini dağıtma
Sanal makine ölçek kümeleri sizin için toodeploy kolaylaştırır ve aynı sanal makineleri bir küme olarak yönetin. Ölçek kümeleri ölçekte uygulamalar için yüksek oranda ölçeklenebilir ve özelleştirilebilir bilgi işlem katmanını sağlar ve Windows platform görüntüleri, Linux platform görüntüleri, özel resimler ve uzantıları destekler. Ölçek kümeleri hakkında daha fazla bilgi için bkz: [sanal makine ölçek kümeleri](virtual-machine-scale-sets-overview.md).

Bu öğretici, bir sanal makine ölçek toocreate nasıl ayarlanacağını gösterir. **olmadan** hello Azure portal kullanarak. Nasıl toouse hello Azure portal hakkında daha fazla bilgi için bkz: [nasıl toocreate hello Azure portal ile bir sanal makine ölçek kümesi](virtual-machine-scale-sets-portal-create.md).

>[!NOTE]
>Azure Resource Manager kaynakları hakkında daha fazla bilgi için bkz: [Azure Resource Manager ve klasik dağıtım](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="sign-in-tooazure"></a>İçinde tooAzure oturum

Azure CLI 2.0 veya Azure PowerShell toocreate ölçek kullanıyorsanız, ayarlanırsa, ilk tooyour Abonelikteki toosign gerekir.

Ayarlama, tooinstall ve oturum açma tooAzure Azure CLI veya PowerShell ile nasıl görürüm hakkında daha fazla bilgi için [Azure CLI 2.0 ile çalışmaya başlama](/cli/azure/get-started-with-azure-cli.md) veya [Azure PowerShell cmdlet'leri kullanmaya başlama](/powershell/azure/overview).

```azurecli
az login
```

```powershell
Login-AzureRmAccount
```

## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Önce hello sanal makine ölçek kümesi bir kaynak grubu ile ilişkili toocreate gerekir.

```azurecli
az group create --location westus2 --name MyResourceGroup1
```

```powershell
New-AzureRmResourceGroup -Location westus2 -Name MyResourceGroup1
```

## <a name="create-from-azure-cli"></a>Azure CLI üzerinden oluşturma

Azure CLI ile en az çaba ile ayarlanmış bir sanal makine ölçek oluşturabilirsiniz. Varsayılan değerleri atlarsanız, bunlar sizin için sağlanır. Örneğin, herhangi bir sanal ağ bilgi belirtmezseniz, bir sanal ağ sizin için oluşturulur. Bölümleri aşağıdaki hello atlarsanız, bunlar sizin için oluşturulur: 
- Bir yük dengeleyici
- Bir sanal ağ
- Bir ortak IP adresi

Merhaba sanal makine ölçek kümesi üzerinde toouse istediğiniz sanal makine görüntüsü seçme Merhaba, birkaç seçeneğiniz vardır:

- URN  
bir kaynak tanıtıcısı Hello:  
**Win2012R2Datacenter**

- URN diğer adı  
kolay adı bir URN Hello:  
**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**

- Özel kaynak kimliği  
Merhaba yolu tooan Azure kaynağı:  
**/Subscriptions/Subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.COMPUTE/images/MyImage**

- Web kaynağı  
Merhaba yolu tooan HTTP URI:  
**http://contoso.BLOB.Core.Windows.NET/vhds/osdiskimage.vhd**

>[!TIP]
>Kullanılabilir görüntülerle listesini almak `az vm image list`.

toocreate bir sanal makine ölçek kümesi, hello aşağıdakileri belirtin:

- Kaynak grubu 
- Ad
- İşletim sistemi görüntüsü
- Kimlik doğrulama bilgileri 
 
Aşağıdaki örnek hello (Bu adım birkaç dakika sürebilir) temel sanal makine ölçek kümesi oluşturur.

```azurecli
az vmss create --resource-group MyResourceGroup1 --name MyScaleSet --image UbuntuLTS --authentication-type password --admin-username azureuser --admin-password P@ssw0rd!
```

Merhaba komut bittikten sonra oluşturulan ayarlayın, sanal makine ölçek şimdi sahip olur. Tooit bağlanabilmesi tooget hello hello sanal makinenin IP adresini gerekebilir. Komutu aşağıdaki hello ile çok sayıda hello sanal makine (Merhaba IP adresi dahil) hakkında farklı bilgi elde edebilirsiniz. 

```azurecli
az vmss list-instance-connection-info --resource-group MyResourceGroup1 --name MyScaleSet
```

## <a name="create-from-powershell"></a>Powershell'den oluşturma

Azure CLI'den daha karmaşık toouse powershell'dir. Azure CLI ağla ilgili kaynaklar (örneğin, yük Dengeleyiciler, IP adresleri ve sanal ağları) için varsayılan sağlarken, PowerShell desteklemez. PowerShell ile bir görüntü başvuran bir biraz daha çok karmaşıktır. Cmdlet aşağıdaki hello ile görüntüleri alabilirsiniz:

1. Get-AzureRMVMImagePublisher
2. Get-AzureRMVMImageOffer
3. Get-AzureRmVMImageSku

Merhaba cmdlet'leri iş sırayla yöneltilen. Merhaba nasıl tooget tüm görüntüleri bir örnek şudur **Batı ABD 2** hello ada sahip bir yayımcı bölgesiyle **microsoft** da.

```powershell
Get-AzureRMVMImagePublisher -Location WestUS2 | Where-Object PublisherName -Like *microsoft* | Get-AzureRMVMImageOffer | Get-AzureRmVMImageSku | Select-Object PublisherName, Offer, Skus
```

```
PublisherName              Offer                    Skus
-------------              -----                    ----
microsoft-ads              linux-data-science-vm    linuxdsvm
microsoft-ads              standard-data-science-vm standard-data-science-vm
MicrosoftAzureSiteRecovery Process-Server           Windows-2012-R2-Datacenter
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Enterprise
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Standard
MicrosoftBizTalkServer     BizTalk-Server           2016-Developer
MicrosoftBizTalkServer     BizTalk-Server           2016-Enterprise
...
```

bir sanal makine ölçek kümesi oluşturmak için hello iş akışı aşağıdaki gibidir:

1. Merhaba ölçek kümesi hakkında bilgi içeren bir yapılandırma nesnesi oluşturun.
2. Başvuru hello temel işletim sistemi görüntüsü.
3. Merhaba işletim sistemi ayarlarını yapılandırın: kimlik doğrulaması, VM adı ön ekini ve kullanıcı/geçirin.
4. Ağ yapılandırın.
5. Merhaba ölçek kümesi oluşturun.

Bu örnek, Windows Server 2016 sahip bir bilgisayar için temel bir iki örnekli ölçek oluşturur.

```powershell
# Resource group name from above
$rg = "MyResourceGroup1"
$location = "WestUS2"

# Create a config object
$vmssConfig = New-AzureRmVmssConfig -Location $location -SkuCapacity 2 -SkuName Standard_A0  -UpgradePolicyMode Automatic

# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig -ImageReferencePublisher MicrosoftWindowsServer -ImageReferenceOffer WindowsServer -ImageReferenceSku 2016-Datacenter -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig -AdminUsername azureuser -AdminPassword P@ssw0rd! -ComputerNamePrefix myvmssvm

# Create hello virtual network resources

## Basics
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name "my-subnet" -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name "my-network" -ResourceGroupName $rg -Location $location -AddressPrefix 10.0.0.0/16 -Subnet $subnet

## Load balancer
$publicIP = New-AzureRmPublicIpAddress -Name "PublicIP" -ResourceGroupName $rg -Location $location -AllocationMethod Static -DomainNameLabel "myuniquedomain"
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontend" -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
$probe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
$inboundNATRule1= New-AzureRmLoadBalancerRuleConfig -Name "webserver" -FrontendIpConfiguration $frontendIP -Protocol Tcp -FrontendPort 80 -BackendPort 80 -IdleTimeoutInMinutes 15 -Probe $probe -BackendAddressPool $backendPool
$inboundNATPool1 = New-AzureRmLoadBalancerInboundNatPoolConfig -Name "RDP" -FrontendIpConfigurationId $frontendIP.Id -Protocol TCP -FrontendPortRangeStart 53380 -FrontendPortRangeEnd 53390 -BackendPort 3389

New-AzureRmLoadBalancer -ResourceGroupName $rg -Name "LB1" -Location $location -FrontendIpConfiguration $frontendIP -LoadBalancingRule $inboundNATRule1 -InboundNatPool $inboundNATPool1 -BackendAddressPool $backendPool -Probe $probe

## IP address config
$ipConfig = New-AzureRmVmssIpConfig -Name "my-ipaddress" -LoadBalancerBackendAddressPoolsId $backendPool.Id -SubnetId $vnet.Subnets[0].Id -LoadBalancerInboundNatPoolsId $inboundNATPool1.Id

# Attach hello virtual network toohello IP object
Add-AzureRmVmssNetworkInterfaceConfiguration -VirtualMachineScaleSet $vmssConfig -Name "network-config" -Primary $true -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss -ResourceGroupName $rg -Name "MyScaleSet1" -VirtualMachineScaleSet $vmssConfig
```

### <a name="using-a-custom-virtual-machine-image"></a>Bir özel sanal makine görüntüsü kullanma
Bir sanal makine görüntüsü hello Galerisi'nden başvuran yerine kendi özel görüntünüzü kümeden bir ölçek oluşturuyorsanız hello _kümesi AzureRmVmssStorageProfile_ komutu şuna benzeyebilir:
```PowerShell
Set-AzureRmVmssStorageProfile -OsDiskCreateOption FromImage -ManagedDisk PremiumLRS -OsDiskCaching "None" -OsDiskOsType Linux -ImageReferenceId (Get-AzureRmImage -ImageName $VMImage -ResourceGroupName $rg).id
```

## <a name="create-from-a-template"></a>Şablondan oluşturma

Bir Azure Resource Manager şablonu kullanarak bir sanal makine ölçek dağıtabilirsiniz. Kendi şablonunuzu oluşturun ya da bir hello kullan [şablonu deposu](https://azure.microsoft.com/resources/templates/?term=vmss). Bu şablonlar dağıtılabilir doğrudan tooyour Azure aboneliği.

>[!NOTE]
>toocreate kendi şablonunuzu bir JSON metin dosyası oluşturun. Hakkında genel bilgi için toocreate ve şablonu özelleştirme bkz [Azure Resource Manager şablonları](../azure-resource-manager/resource-group-authoring-templates.md).

Örnek şablon kullanılabilir [github'da](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set). Nasıl bkz: toocreate ve örnek, kullanma hakkında daha fazla bilgi için [en uygun ölçek kümesini](.\virtual-machine-scale-sets-mvss-start.md).

## <a name="create-from-visual-studio"></a>Visual Studio'dan oluşturma

Visual Studio ile bir Azure kaynak grubu projesi oluşturun ve şablon tooit bir sanal makine ölçek kümesi ekleyin. Tooimport isteyip istemediğinizi seçebilirsiniz, GitHub veya hello Azure Web uygulama Galerisi. Bir dağıtım PowerShell komut dosyası ayrıca sizin için oluşturulur. Daha fazla bilgi için bkz: [nasıl toocreate Visual Studio ile bir sanal makine ölçek kümesi](virtual-machine-scale-sets-vs-create.md).

## <a name="create-from-hello-azure-portal"></a>Azure portal Hello oluşturma

Hello Azure portal tooquickly ölçek kümesi oluştur kullanışlı bir yol sağlar. Daha fazla bilgi için bkz: [nasıl toocreate hello Azure portal ile bir sanal makine ölçek kümesi](virtual-machine-scale-sets-portal-create.md).

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla bilgi edinmek [veri diskleri](virtual-machine-scale-sets-attached-disks.md).

Nasıl çok öğrenin[uygulamalarınızı yönetmek](virtual-machine-scale-sets-deploy-app.md).
