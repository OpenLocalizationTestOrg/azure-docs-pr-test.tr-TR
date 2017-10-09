---
title: "aaaCreate ve Windows sanal makineleri yönetme hello Azure PowerShell Modülü | Microsoft Docs"
description: "Öğretici - oluşturma ve yönetme Windows VM ile birlikte hello Azure PowerShell Modülü"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 20adcb673ef4de683e6ad82d048a9625a1dc838c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-with-hello-azure-powershell-module"></a>Oluşturma ve yönetme Windows VM'ler ile Azure PowerShell modülü hello

Azure sanal makineler tam olarak yapılandırılabilir ve esnek bir bilgi işlem ortamı sağlar. Bu öğretici, bir VM boyutu seçerek, bir VM görüntüsü seçme ve bir VM dağıtma gibi temel Azure sanal makine dağıtım öğeleri kapsar. Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:

> [!div class="checklist"]
> * Oluştur ve tooa VM Bağlan
> * Seçin ve VM görüntüleri kullanmak
> * Görüntüleme ve belirli VM boyutları kullanma
> * VM’yi yeniden boyutlandırma
> * Görüntüleyin ve VM durumunu anlamak

Bu öğretici hello Azure PowerShell modülü 3,6 veya sonraki bir sürümü gerektiriyor. Çalıştırma ` Get-Module -ListAvailable AzureRM` toofind hello sürümü. Tooupgrade gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).

## <a name="create-resource-group"></a>Kaynak grubu oluşturma

Bir kaynak grubu ile Merhaba oluşturmak [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) komutu. 

Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır. Bir kaynak grubu bir sanal makine önce oluşturulması gerekir. Bu örnekte, bir kaynak grubu adında *myResourceGroupVM* hello oluşturulan *EastUS* bölge. 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupVM -Location EastUS
```

Merhaba kaynak grubu oluştururken veya değiştirirken Bu öğretici görülebilir bir VM belirtilir.

## <a name="create-virtual-machine"></a>Sanal makine oluşturma

Bir sanal makineye bağlı tooa sanal ağ olmalıdır. Bir ağ arabirimi kartı bir ortak IP adresi kullanarak hello sanal makine ile iletişim kurar.

### <a name="create-virtual-network"></a>Sanal ağ oluşturma

Bir alt ağ ile oluşturma [yeni AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
```

Bir sanal ağ ile oluşturma [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 ` 
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a>Ortak IP adresi oluştur

Bir ortak IP adresiyle oluşturma [yeni AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):

```powershell
$pip = New-AzureRmPublicIpAddress ` 
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS ` 
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a>Ağ arabirimi kartı oluşturun

Bir ağ arabirimi kartı ile oluşturma [yeni AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroupVM  `
  -Location EastUS `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a>Ağ güvenlik grubu oluşturun

Bir Azure [ağ güvenlik grubu](../../virtual-network/virtual-networks-nsg.md) (NSG) bir veya daha çok sanal makineler için gelen ve giden trafik denetler. Ağ güvenlik grubu kurallarının izin verin veya belirli bir bağlantı noktası veya bağlantı noktası aralığı ağ trafiği engelle. Önceden tanımlanmış bir kaynakta kaynaklanan trafiğin yalnızca bir sanal makineyle iletişim kurabilmesi için bu kurallar kaynak adres öneki de içerir. yüklemekte olduğunuz tooaccess hello IIS Web sunucusu, gelen bir NSG kuralı eklemeniz gerekir.

toocreate gelen bir NSG kuralı kullanmak [Ekle AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig). Merhaba aşağıdaki örnek adlı bir NSG kuralı oluşturur *myNSGRule* bağlantı noktası açar *3389* hello sanal makine için:

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1000 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 3389 `
  -Access Allow
```

NSG Hello kullanarak oluşturduğunuz *myNSGRule* ile [yeni AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupVM `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRule
```

Merhaba NSG toohello alt ağ ile Merhaba sanal ağındaki Ekle [kümesi AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -VirtualNetwork $vnet `
    -NetworkSecurityGroup $nsg `
    -AddressPrefix 192.168.1.0/24
```

Güncelleştirme hello sanal ağ ile [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a>Sanal makine oluşturma

Bir sanal makine oluştururken, işletim sistemi görüntüsü, disk boyutlandırma ve yönetici kimlik bilgileri gibi birkaç seçenek bulunur. Bu örnekte, bir sanal makine adı ile oluşturulan *myVM* çalışan hello en son sürümünü Windows Server 2016 Datacenter.

Merhaba kullanıcı adı ve parola ile Merhaba sanal makinede hello yönetici hesabı için gerekli ayarlama [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Merhaba sanal makine için ilk yapılandırma Hello oluşturmak [yeni AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

Merhaba işletim sistemi bilgileri toohello sanal makine yapılandırmasıyla eklemek [kümesi AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):

```powershell
$vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM `
    -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

Hello görüntü bilgileri toohello sanal makine yapılandırmasıyla eklemek [kümesi AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
```

Merhaba işletim sistemi disk ayarları toohello sanal makine yapılandırmasıyla eklemek [kümesi AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):

```powershell
$vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
```

Toohello sanal makine yapılandırmasıyla daha önce oluşturduğunuz Ekle hello ağ arabirim kartı [Ekle AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

Merhaba sanal makineyle oluşturmak [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroupVM -Location EastUS -VM $vm
```

## <a name="connect-toovm"></a>TooVM Bağlan

Merhaba dağıtım tamamlandıktan sonra bir Uzak Masaüstü Bağlantısı ile Merhaba sanal makine oluşturun.

Aşağıdaki komutları tooreturn hello genel IP adresi hello sanal makinenin hello çalıştırın. Tarayıcı tootest web bağlantınızı bir sonraki adımda ile tooit bağlanabilmesi için bu IP adresini not alın.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupVM  | Select IpAddress
```

Kullanım hello aşağıdaki hello sanal makineyle Uzak Masaüstü oturumu toocreate komutu. Başlangıç IP adresi ile hello yerine *Publicıpaddress* sanal makinenizin. İstendiğinde, hello sanal makine oluşturulurken kullanılan hello kimlik bilgilerini girin.

```powershell
mstsc /v:<publicIpAddress>
```

## <a name="understand-vm-images"></a>VM görüntüleri anlama

Hello Azure Market kullanılan toocreate yeni bir sanal makine olabilecek çok sayıda sanal makine görüntülerini içerir. Merhaba önceki adımlarda, bir sanal makine hello Windows Server 2016-Datacenter görüntüsü kullanılarak oluşturuldu. Bu adımda, ayrıca yeni VM'ler için temel olarak kullanabilirsiniz diğer Windows görüntüleri için kullanılan toosearch hello Market hello PowerShell modülüdür. Bu işlem hello yayımcı, teklif ve hello görüntü adı (Sku) bulma oluşur. 

Kullanım hello [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) komutu tooreturn görüntü yayımcıların listesini.  

```powersehll
Get-AzureRmVMImagePublisher -Location "EastUS"
```

Kullanım hello [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn görüntü teklifleri listesi. Bu komutla, liste hello belirtilen yayımcı üzerinde filtrelenmiş hello döndürdü. 

```powershell
Get-AzureRmVMImageOffer -Location "EastUS" -PublisherName "MicrosoftWindowsServer"
```

```powershell
Offer             PublisherName          Location
-----             -------------          -------- 
Windows-HUB       MicrosoftWindowsServer EastUS 
WindowsServer     MicrosoftWindowsServer EastUS   
WindowsServer-HUB MicrosoftWindowsServer EastUS   
```

Merhaba [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) komutu ardından filtre uygulayarak hello yayımcı ve teklif adı tooreturn üzerinde resim adları listesi.

```powershell
Get-AzureRmVMImageSku -Location "EastUS" -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer"
```

```powershell
Skus                            Offer         PublisherName          Location
----                            -----         -------------          --------
2008-R2-SP1                     WindowsServer MicrosoftWindowsServer EastUS  
2008-R2-SP1-BYOL                WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter-BYOL            WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter              WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter-BYOL         WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-Server-Core     WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-with-Containers WindowsServer MicrosoftWindowsServer EastUS  
2016-Nano-Server                WindowsServer MicrosoftWindowsServer EastUS
```

Bu bilgiler kullanılan toodeploy belirli bir görüntü ile VM olabilir. Bu örnek hello görüntü adı hello VM nesnesinde ayarlar. Tam dağıtım adımları için bu öğreticideki toohello önceki örneklerde bakın.

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter-with-Containers `
    -Version latest
```

## <a name="understand-vm-sizes"></a>VM boyutları anlama

Bir sanal makine boyutu, kullanılabilir toohello sanal makine yapılan işlem kaynaklarını CPU, GPU ve bellek gibi hello miktarını belirler. Sanal makineler hello beklediğiniz için iş yükü boyutu ile uygun oluşturulan toobe gerekir. İş yükü artarsa, var olan bir sanal makine yeniden boyutlandırılabilir.

### <a name="vm-sizes"></a>VM boyutları

Aşağıdaki tablonun hello boyutları kullanım örneklerine kategorilere ayırır.  

| Tür                     | Boyutlar           |    Açıklama       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| Genel amaçlı         |DSv2, Dv2, DS, D, Av2, A0-7| Dengeli CPU bellekten. Geliştirme için ideal / test ve küçük toomedium uygulamaları ve verileri çözümler.  |
| İşlem için iyileştirilmiş      | FS, F             | Yüksek CPU bellekten. Orta düzey trafik uygulamalar, ağ uygulamaları ve toplu işlemler için iyidir.        |
| Bellek için iyileştirilmiş       | GS, G, DSv2, DS, Dv2, D   | Yüksek bellek için-çekirdek. İlişkisel veritabanları, Orta toolarge önbellekleri ve bellek içi analizi için mükemmel.                 |
| Depolama için iyileştirilmiş       | Ls                | Yüksek disk aktarım hızı ve GÇ. Büyük Veri, SQL ve NoSQL veritabanları için ideal.                                                         |
| GPU           | NV, NC            | Yoğun Grafik işleme ve video düzenleme için hedeflenen özel VM'ler.       |
| Yüksek performans | H, A8-11          | Bizim en güçlü CPU VM'ler isteğe bağlı yüksek verimlilik ağ arabirimlerine (RDMA) sahip. 


### <a name="find-available-vm-sizes"></a>Kullanılabilir VM boyutları Bul

toosee VM listesi boyutları kullanılabilen belirli bir bölgede, hello kullan [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) komutu.

```powershell
Get-AzureRmVMSize -Location EastUS
```

## <a name="resize-a-vm"></a>VM’yi yeniden boyutlandırma

Bir VM dağıtıldıktan sonra onu yeniden boyutlandırılan tooincrease olması veya kaynak ayırma azaltın.

Merhaba istenen boyuta hello geçerli VM kümede kullanılabilir durumdaysa bir VM'yi yeniden boyutlandırılırken önce denetleyin. Merhaba [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) komut boyutlarının listesini döndürür. 

```powershell
Get-AzureRmVMSize -ResourceGroupName myResourceGroupVM -VMName myVM 
```

Merhaba boyutu kullanılabilir isterseniz, hello işlemi sırasında yeniden başlatılıncaya kadar ancak hello VM bir gücü açma durumundan yeniden boyutlandırılabilir.

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM 
$vm.HardwareProfile.VmSize = "Standard_D4"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
```

Merhaba istenen boyut hello geçerli kümede hello VM hello yeniden boyutlandırma önce işlemi serbest toobe oluşabilir gereksinimlerini değildir. , Hello VM geri açık olduğundan, hello geçici diskteki tüm verilerin kaldırılır ve hello genel IP adresi statik bir IP adresi kullanılmadığı sürece değiştirdiğinizde unutmayın. 

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM
$vm.HardwareProfile.VmSize = "Standard_F4s"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
Start-AzureRmVM -ResourceGroupName myResourceGroupVM  -Name $vm.name
```

## <a name="vm-power-states"></a>VM güç durumları

Bir Azure VM birçok güç durumlarını birine sahip. Bu durum hello hiper yönetici hello açısından hello VM hello geçerli durumunu temsil eder. 

### <a name="power-states"></a>Güç durumları

| Güç durumu | Açıklama
|----|----|
| Başlangıç | Merhaba sanal makinenin başlatıldığı gösterir. |
| Çalışıyor | Merhaba sanal makinenin çalışmadığını gösterir. |
| Durduruluyor | Bu hello sanal makinenin durdurulması gösterir. | 
| Durduruldu | Bu hello sanal makine durdurulduğunda gösterir. Sanal makineleri hello durdurulmuş durumda hala bilgi işlem ücretleri olduğunu unutmayın.  |
| Ayırmayı kaldırma | Merhaba sanal makinenin serbest gösterir. |
| Serbest bırakıldı | Merhaba sanal makinenin hello hiper yönetici hello denetim düzlemi hala kullanılabilir ancak tamamen kaldırılması gösterir. Merhaba Deallocated durumu içindeki sanal makineler bilgi işlem ücretleri değil. |
| - | Merhaba güç hello sanal makinenin durumunu bilinmediğini gösterir. |

### <a name="find-power-state"></a>Güç durumu Bul

belirli bir VM, kullanım hello tooretrieve hello durumu [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) komutu. Emin toospecify bir sanal makine ve kaynak grubu için geçerli bir ad olabilir. 

```powershell
Get-AzureRmVM `
    -ResourceGroupName myResourceGroup `
    -Name myVM `
    -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}
```

Çıktı:

```powershell
Status
------
PowerState/running
```

## <a name="management-tasks"></a>Yönetim görevleri

Bir sanal makine Hello yaşam döngüsü sırasında başlatma, durdurma veya bir sanal makine silme gibi yönetim görevleri toorun isteyebilirsiniz. Ayrıca, toocreate, komut dosyaları tooautomate yineleyen veya karmaşık görevleri isteyebilirsiniz. Azure PowerShell kullanarak, birçok ortak yönetim görevlerinin hello komut satırından veya komut dosyalarında çalıştırabilirsiniz.

### <a name="stop-virtual-machine"></a>Sanal makineyi durdurma

Durdurun ve bir sanal makineyle ayırması [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
```

Sağlanan durumdaki tookeep hello sanal makine istiyorsanız hello - StayProvisioned parametresini kullanın.

### <a name="start-virtual-machine"></a>Sanal makineyi Başlat

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroupVM -Name myVM
```

### <a name="delete-resource-group"></a>Kaynak grubunu silme

Bir kaynak grubunu silme içinde içerdiği tüm kaynaklar da siler.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupVM -Force
```

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, temel VM oluşturmayı ve yönetmeyi nasıl gibi hakkında öğrenilen:

> [!div class="checklist"]
> * Oluştur ve tooa VM Bağlan
> * Seçin ve VM görüntüleri kullanmak
> * Görüntüleme ve belirli VM boyutları kullanma
> * VM’yi yeniden boyutlandırma
> * Görüntüleyin ve VM durumunu anlamak

Toohello sonraki öğretici toolearn VM disklerle ilgili ilerleyin.  

> [!div class="nextstepaction"]
> [Oluşturma ve yönetme VM diskleri](./tutorial-manage-data-disk.md)
