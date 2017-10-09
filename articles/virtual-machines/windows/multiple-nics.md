---
title: "aaaCreate ve Windows birden çok NIC kullanan azure'da Vm'leri yönetmek | Microsoft Docs"
description: "Bilgi nasıl toocreate ve Azure PowerShell veya Resource Manager şablonları kullanarak birden çok NIC ekli tooit sahip bir Windows VM yönetin."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 9bff5b6d-79ac-476b-a68f-6f8754768413
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: c3c7d7569aca6f047238146d84b2ffccf05d4079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a>Oluşturma ve birden çok NIC sahip olan bir Windows sanal makine yönetme
Azure sanal makineleri (VM'ler) birden çok sanal ağ arabirimi kartlarıyla (NIC) bağlı toothem olabilir. Yaygın bir senaryo toohave farklı alt ağlar için ön uç ve arka uç bağlantısı olan veya ayrılmış bir ağ tooa izleme veya yedekleme çözümü. Bu makalede nasıl tooit toocreate birden çok NIC sahip bir VM ekli ayrıntıları verilmektedir. Da bilgi nasıl tooadd veya kaldırma NIC var olan bir VM'den. Farklı [VM boyutları](sizes.md) NIC'ler değişen çok sayıda desteği, bu nedenle, VM buna göre boyutu.

Ayrıntılı bilgi için kendi PowerShell komut dosyaları içinde birden çok NIC toocreate nasıl görürüm dahil olmak üzere [birden çok NIC VM'ler dağıtma](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).

## <a name="prerequisites"></a>Ön koşullar
Merhaba sahip olduğunuzdan emin olun [yüklenmiş ve yapılandırılmış en son Azure PowerShell sürüm](/powershell/azure/overview).

Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin. Örnek parametre adlarında *myResourceGroup*, *myVnet*, ve *myVM*.


## <a name="create-a-vm-with-multiple-nics"></a>Birden çok NIC ile VM oluşturma
İlk olarak, bir kaynak grubu oluşturun. Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *EastUs* konumu:

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a>Sanal ağ ve alt ağlar oluşturun
Yaygın bir senaryo için sanal ağ toohave olan iki veya daha fazla alt ağ. Bir alt ağ ön uç trafiği için arka uç trafiği için diğer hello olabilir. tooconnect tooboth alt ağlar, daha sonra VM birden çok NIC kullanın.

1. İle iki sanal ağ alt ağları tanımlamak [yeni AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig). Merhaba aşağıdaki örnek tanımlar hello alt ağlar için *mySubnetFrontEnd* ve *mySubnetBackEnd*:

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. Sanal ağ ve alt ağları ile oluşturmak [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur *myVnet*:

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a>Birden çok NIC oluşturun
İki NIC ile oluşturma [yeni AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface). Bir NIC toohello ön uç alt ağı ve bir NIC toohello arka uç alt ekleyin. Merhaba aşağıdaki örnekte oluşturur adlı NIC'ler *myNic1* ve *myNic2*:

```powershell
$frontEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetFrontEnd'}
$myNic1 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic1" `
    -Location "EastUs" `
    -SubnetId $frontEnd.Id

$backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}
$myNic2 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic2" `
    -Location "EastUs" `
    -SubnetId $backEnd.Id
```

Genellikle ayrıca oluşturduğunuz bir [ağ güvenlik grubu](../../virtual-network/virtual-networks-nsg.md) veya [yük dengeleyici](../../load-balancer/load-balancer-overview.md) toohelp yönetmek ve Vm'leriniz arasında trafiği dağıtın. Merhaba [birden çok NIC VM ayrıntılı](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) makale, bir ağ güvenlik grubu oluşturma ve NIC atama size kılavuzluk eder.

### <a name="create-hello-virtual-machine"></a>Merhaba sanal makine oluşturma
Şimdi toobuild VM yapılandırmanızı başlatın. Her VM boyutu hello toplam sayısı tooa VM ekleyebilirsiniz NIC'ler için bir sınırı vardır. Daha fazla bilgi için bkz: [Windows VM boyutları](sizes.md).

1. VM kimlik bilgilerini toohello ayarlamak `$cred` şekilde değişkeni:

    ```powershell
    $cred = Get-Credential
    ```

2. VM ile tanımlama [AzureRmVMConfig yeni](/powershell/module/azurerm.compute/new-azurermvmconfig). Merhaba aşağıdaki örnek tanımlar adlı bir VM'den *myVM* ve ikiden fazla NIC'ler destekleyen bir VM boyutu kullanır (*Standard_DS3_v2*):

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. VM yapılandırmanızı Hello kalan oluşturma [kümesi AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) ve [kümesi AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage). Aşağıdaki örnek hello bir Windows Server 2016 VM oluşturur:

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig `
        -Windows `
        -ComputerName "myVM" `
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig `
        -PublisherName "MicrosoftWindowsServer" `
        -Offer "WindowsServer" `
        -Skus "2016-Datacenter" `
        -Version "latest"
   ```

4. Daha önce oluşturduğunuz ile Merhaba iki NIC ekleme [Ekle AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. Son olarak, VM oluşturma [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-tooan-existing-vm"></a>VM varolan bir NIC tooan Ekle
VM varolan bir sanal NIC tooan hello VM ayırması tooadd eklemek sanal NIC hello sonra hello VM başlatın.

1. Deallocate VM ile Merhaba [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm). Merhaba aşağıdaki örnek kaldırır hello adlı VM *myVM* içinde *myResourceGroup*:

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. Merhaba VM Hello varolan yapılandırmasını almak ile [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm). Merhaba aşağıdaki örnek alır bilgi hello adlı VM için *myVM* içinde *myResourceGroup*:

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. Merhaba aşağıdaki örnekte oluşturur ile sanal bir NIC'ye [yeni AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) adlı *myNic3* , çok bağlı*mySubnetBackEnd*. Sanal NIC durumda hello bağlı toohello adlı VM *myVM* içinde *myResourceGroup* ile [Ekle AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

    ```powershell
    # Get info for hello back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get hello ID of hello new virtual NIC and add tooVM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a>Birincil sanal NIC
    Merhaba multi-NIC VM Nıc'lerde birini toobe birincil gerekir. Aşağıdakilerden birini varolan sanal NIC hello hello üzerinde VM zaten birincil olarak ayarlanmış, bu adımı atlayabilirsiniz. Merhaba aşağıdaki örnekte iki sanal NIC VM üzerinde mevcut şimdi tooadd istediğiniz varsayar ve ilk NIC hello (`[0]`) hello birincil olarak:
        
    ```powershell
    # List existing NICs on hello VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 toobe primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update hello VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. Başlangıç VM ile Merhaba [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a>Bir NIC var olan bir sanal makineden kaldırın
sanal bir NIC'ye tooremove var olan bir VM'den hello VM serbest bırakma, hello Kaldır sanal NIC sonra Başlangıç hello VM.

1. Deallocate VM ile Merhaba [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm). Merhaba aşağıdaki örnek kaldırır hello adlı VM *myVM* içinde *myResourceGroup*:

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. Merhaba VM Hello varolan yapılandırmasını almak ile [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm). Merhaba aşağıdaki örnek alır bilgi hello adlı VM için *myVM* içinde *myResourceGroup*:

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. NIC kaldırma ile Merhaba hakkında bilgi almak [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface). Merhaba aşağıdaki örnek bilgilerini alır *myNic3*:

    ```powershell
    # List existing NICs on hello VM if you need toodetermine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. Kaldırma NIC ile Merhaba [Kaldır AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) ve ardından güncelleştirme VM ile Merhaba [güncelleştirme-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm). Merhaba aşağıdaki örnek kaldırır *myNic3* ile alınan `$nicId` adım önceki hello içinde:

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. Başlangıç VM ile Merhaba [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a>Birden çok NIC ile şablonları oluşturma
Azure Resource Manager şablonları bir şekilde toocreate birden çok NIC oluşturma gibi dağıtım işlemi sırasında birden fazla örneğini bir kaynak sağlayın. Resource Manager şablonları bildirim temelli JSON dosyaları toodefine ortamınız kullanın. Daha fazla bilgi için bkz: [genel bakış Azure Kaynak Yöneticisi'nin](../../azure-resource-manager/resource-group-overview.md). Kullanabileceğiniz *kopya* toospecify hello örnekleri toocreate sayısı:

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

Daha fazla bilgi için bkz: [kullanarak birden çok örneği oluşturma *kopya*](../../resource-group-create-multiple.md). 

Aynı zamanda `copyIndex()` tooappend bir numara tooa kaynak adı. Daha sonra oluşturabilirsiniz *myNic1*, *MyNic2* ve benzeri. Merhaba aşağıdaki kodda hello dizin değeri ekleyerek bir örnek gösterilmektedir:

```json
"name": "[concat('myNic', copyIndex())]", 
```

Tam örnek okuyabilirsiniz [Resource Manager şablonları kullanarak birden çok NIC oluşturma](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).

## <a name="next-steps"></a>Sonraki adımlar
Gözden geçirme [Windows VM boyutları](sizes.md) zaman çalıştığınız toocreate birden çok NIC sahip bir VM. Dikkat toohello en fazla sayıda her VM boyutu destekleyen NIC ücret ödersiniz. 


