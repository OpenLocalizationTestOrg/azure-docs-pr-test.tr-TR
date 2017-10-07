---
title: bir SQL Server sanal makinesine (Resource Manager) Azure PowerShell'de aaaCreate | Microsoft Docs
description: "Bir Azure VM ile SQL Server sanal makineye Galerisi görüntüleri oluşturmak için adımlar ve PowerShell komut dosyaları sağlar."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 98d50dd8-48ad-444f-9031-5378d8270d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/17/2017
ms.author: jroth
ms.openlocfilehash: 2b8cb8f69ff9894a95eab617816a60c8674eeefa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a>Azure PowerShell (Resource Manager) kullanarak bir SQL Server sanal makine sağlama
> [!div class="op_single_selector"]
> * [Portal](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a>Genel Bakış
Bu öğreticide, tek bir Azure sanal makine kullanarak toocreate nasıl hello gösterilir **Azure Resource Manager** Azure PowerShell cmdlet'lerini kullanarak dağıtım modeli. Bu öğreticide, tek bir disk sürücüsü bir görüntüden hello SQL Galerisi kullanarak tek bir sanal makine oluşturacağız. Merhaba depolama, ağ ve hello sanal makine tarafından kullanılacak olan işlem kaynakları için yeni sağlayıcıları oluşturacağız. Tüm bu kaynaklar için varolan sağlayıcıları varsa, bunun yerine bu sağlayıcılardan kullanabilirsiniz.

Bu konunun Klasik sürümü hello varsa bkz [Klasik Azure PowerShell kullanarak bir SQL Server sanal makine sağlama](../classic/ps-sql-create.md).

## <a name="prerequisites"></a>Ön koşullar
Bu öğretici için ihtiyacınız vardır:

* Bir Azure hesabı ve başlamadan önce abonelik. Yoksa, kaydolun bir [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/).
* [Azure PowerShell)](/powershell/azure/overview), en düşük sürüm 1.4.0 veya üzeri (sürüm 1.5.0 kullanılarak yazılmış Bu öğretici).
  * tooretrieve sürümü, türü **Azure Get-Module - listavailable birlikte**.

## <a name="configure-your-subscription"></a>Aboneliğinizi yapılandırın
Windows PowerShell'i açın ve aşağıdaki cmdlet'i hello çalıştırarak erişim tooyour Azure hesabı oluşturun. Bir oturum açma ekranı tooenter kimlik bilgilerinizi sunulur. Kullanım hello aynı e-posta ve parola toosign toohello Azure portalını kullanın.

    Add-AzureRmAccount

Başarıyla oturum açtıktan sonra bazı bilgiler imzalı içinde hello Subscriptionıd içeren ekran görürsünüz. Merhaba abonelik tooa farklı bir abonelik değiştirmediğiniz sürece, Bu öğretici için hello kaynakların oluşturulacağını budur. Birden çok SubscriptionIds varsa, aşağıdaki cmdlet'i tooreturn hello, SubscriptionIds tümünün listesini çalıştırın:

    Get-AzureRmSubscription

toochange tooanother Subscriptionıd, cmdlet istenen Subscriptionıd ile aşağıdaki hello çalıştırın.

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a>Görüntü değişkenleri tanımlayın
toosimplify kullanılabilirliğini ve bu öğreticinin tamamlanan hello betikten anlayış, biz bir dizi değişken tanımlayarak başlar. Uygun gördüğünüz ancak adlandırma kısıtlamaları ilgili tooname uzunlukları ve özel karakterler sağlanan hello değerlerini değiştirirken dikkatli olun gibi hello parametre değerlerini değiştirin.

### <a name="location-and-resource-group"></a>Konum ve kaynak grubu
Hello hello sanal makine için diğer kaynaklar oluşturacak iki değişkenleri toodefine hello veri bölgesi ve hello kaynak grubunu kullanın.

İstediğiniz şekilde değiştirin ve sonra bu değişkenleri cmdlet'leri tooinitialize aşağıdaki hello yürütün.

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a>Depolama özellikleri
Değişkenleri toodefine hello depolama hesabı ve hello türü hello sanal makine tarafından kullanılan depolama toobe aşağıdaki hello kullanın.

İstediğiniz şekilde değiştirin ve sonra bu değişkenleri cmdlet tooinitialize aşağıdaki hello yürütün. Bu örnekte, biz kullanıyoruz Not [Premium depolama](../../../storage/common/storage-premium-storage.md), üretim iş yükleri için önerilir. Bu kılavuz ve diğer öneriler hakkında daha fazla bilgi için bkz: [Azure Virtual Machines'de SQL Server için performans en iyi uygulamaları](virtual-machines-windows-sql-performance.md).

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a>Ağ Özellikleri
Aşağıdaki değişkenler toodefine hello ağ arabirimi, hello TCP/IP'yi ayırma yöntemi, hello sanal ağ adı, hello sanal alt ağ adı, başlangıç IP adresi aralığı hello sanal ağ için başlangıç IP adresi aralığı hello alt ağı ve hello için hello kullanın Genel etki alanı adı etiketi toobe hello ağında hello sanal makine tarafından kullanılan.

İstediğiniz şekilde değiştirin ve sonra bu değişkenleri cmdlet tooinitialize aşağıdaki hello yürütün.

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a>Sanal makine özellikleri
Değişkenleri toodefine hello sanal makine adı, hello bilgisayar adı, hello sanal makine boyutu ve hello işletim sistemi disk adı hello sanal makine için aşağıdaki hello kullanın.

İstediğiniz şekilde değiştirin ve sonra bu değişkenleri cmdlet tooinitialize aşağıdaki hello yürütün.

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a>Görüntü Özellikleri
Değişkenleri toodefine hello görüntü toouse hello sanal makine için aşağıdaki hello kullanın. Bu örnekte, hello SQL Server 2016 Enterprise görüntü kullanılır.

İstediğiniz şekilde değiştirin ve sonra bu değişkenleri cmdlet tooinitialize aşağıdaki hello yürütün.

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

SQL Server görüntüsü tekliflerinin hello Get-AzureRmVMImageOffer komutuyla tam bir liste alabilir dikkat edin:

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

Ve hello SKU'ları hello Get-AzureRmVMImageSku komutuyla bir sunum için kullanılabilir görebilirsiniz. Merhaba aşağıdaki komut gösterir tüm SKU'ları Merhaba kullanılabilir **SQL2014SP1 WS2012R2** sunar.

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma
Merhaba Resource Manager dağıtım modeli ile oluşturduğunuz hello ilk hello kaynak grubu nesnesidir. Merhaba kullanacağız [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet toocreate bir Azure kaynak grubu ve kaynaklarına hello kaynakla grup adını ve konumunu daha önce başlatılmış hello değişkenleri tarafından tanımlanmış.

Cmdlet toocreate aşağıdaki hello yeni kaynak grubunuz yürütün.

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a>Depolama hesabı oluşturma
Merhaba sanal makine hello işletim sistemi diski ve hello SQL Server veri ve günlük dosyaları için depolama kaynaklarını gerektirir. Kolaylık olması için tek bir disk için her ikisini de oluşturacağız. Daha sonra hello kullanarak ek diskleri iliştirebilirsiniz [Ekle-Azure diski](/powershell/module/azure/add-azuredisk) cmdlet'ini tooplace, SQL Server verilerini sıralama ve günlük dosyalarını adanmış diskler üzerinde. Merhaba kullanacağız [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet toocreate standart depolama hesabı yeni kaynak grubunuz ve hello depolama hesabı adı, depolama Sku adı ve konumu hello değişkenleri kullanılarak tanımlanan aldığınız daha önce başlatıldı.

Cmdlet toocreate aşağıdaki hello yeni depolama hesabınız yürütün.

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a>Ağ kaynakları oluşturun
ağ kaynaklarının sayısını Hello sanal makine için ağ bağlantısı gerektirir.

* Her sanal makine bir sanal ağ gerektirir.
* Bir sanal ağ en az bir alt ağ tanımlanmış olması gerekir.
* Bir ağ arabirimi genel veya özel bir IP adresi ile tanımlanması gerekir.

### <a name="create-a-virtual-network-subnet-configuration"></a>Bir sanal ağ alt ağ yapılandırması oluştur
Biz bizim sanal ağ için bir alt ağ yapılandırması oluşturarak başlar. Bizim öğretici için hello kullanarak bir varsayılan alt ağ oluşturacağız [yeni AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet'i. Daha önce başlatılmış hello değişkenleri kullanılarak tanımlanan hello alt ağ ad ve adres ön eki ile sanal ağ alt ağı yapılandırmamızın oluşturacağız.

> [!NOTE]
> Bu cmdlet kullanılarak hello sanal ağ alt ağ yapılandırması ek özelliklerini tanımlayabilirsiniz, ancak hello Bu öğretici kapsamında değildir.
>
>

Merhaba cmdlet toocreate aşağıdaki sanal alt ağ yapılandırmanızı yürütün.

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a>Sanal ağ oluşturma
Ardından, hello kullanarak bizim sanal ağ oluşturacağız [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet'i. Merhaba adını, konumunu ve daha önce başlatılmış hello değişkenleri kullanma ve hello önceki adımda tanımlanan hello alt ağ yapılandırması kullanma tanımlanan adres öneki ile yeni, kaynak grubundaki bizim sanal ağ oluşturacağız.

Cmdlet toocreate aşağıdaki hello sanal ağınızı yürütün.

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-hello-public-ip-address"></a>Merhaba ortak IP adresi oluştur
Tanımlanan bizim sanal ağ sahibiz, bağlantı toohello sanal makine için bir IP adresi tooconfigure ihtiyacımız var. Bu öğretici için dinamik IP adresi toosupport Internet bağlantısını kullanarak genel bir IP adresi oluşturacağız. Merhaba kullanacağız [yeni AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate hello genel IP adresi hello kaynak grubu oluşturulan prevously ve hello adını, konumunu, ayırma yöntemi ve hello kullanılarak tanımlanmış DNS etki alanı adı etiketi daha önce başlatılmış değişkenleri.

> [!NOTE]
> Bu cmdlet kullanılarak hello ortak IP adresinin ek özellikler tanımlayabilirsiniz, ancak hello ilk Bu öğretici kapsamında değildir. Statik adresi ile özel bir adres veya adresi de oluşturabilir, ancak, aynı zamanda hello Bu öğretici kapsamında değildir.
>
>

Cmdlet toocreate aşağıdaki hello ortak IP adresi yürütün.

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-hello-network-interface"></a>Merhaba ağ arabirimi oluştur
Şimdi, sanal makinenin kullanacağı hazır toocreate hello ağ arabirimi duyuyoruz. Merhaba kullanacağız [yeni AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet toocreate bizim ağ arabirimi hello kaynak grubunda daha önce oluşturduğunuz ve hello adını, konumunu, alt ağ ve genel IP adresi ile önceden tanımlanmış.

Cmdlet toocreate aşağıdaki Merhaba, ağ arabiriminin yürütün.

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a>Bir VM nesnesine yapılandırın
Biz tanımlanan depolama ve ağ kaynaklarına sahip olduğunuza göre hello sanal makine için hazır toodefine işlem kaynakları duyuyoruz. Bizim öğretici için size hello sanal makine boyutu ve çeşitli işletim sistemi özelliklerini belirtin, daha önce oluşturduğumuz hello ağ arabirimi belirtin, blob depolama alanını tanımlayın ve hello işletim sistemi diski belirtin.

### <a name="create-hello-vm-object"></a>Merhaba VM nesnesi oluşturun
Biz hello sanal makine boyutu belirterek başlar. Bu öğretici için size bir DS13 belirlersiniz. Merhaba kullanacağız [yeni AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet toocreate hello adı daha önce başlatılmış hello değişkenleri kullanılarak tanımlanan boyutu ile yapılandırılabilir sanal makine nesnesi.

Cmdlet toocreate hello sanal makine nesnesini aşağıdaki hello yürütün.

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-toohold-hello-name-and-password-for-hello-local-administrator-credentials"></a>Bir kimlik bilgisi nesnesi toohold hello adı ve parola hello yerel yönetici kimlik bilgileri oluşturun
Merhaba hello sanal makine için işletim sistemi özelliklerini ayarlayabilmeniz için önce kimliğinizi toosupply hello kimlik hello yerel yönetici hesabı için güvenli bir dize gerekiyor. tooaccomplish bunu hello kullanacağız [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet'i.

Cmdlet aşağıdaki hello yürütün ve hello Windows PowerShell kimlik bilgisi isteği penceresinde hello hello Windows sanal makinesinde yerel yönetici hesabı için hello adı ve parola toouse yazın.

    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."

### <a name="set-hello-operating-system-properties-for-hello-virtual-machine"></a>Merhaba hello sanal makine için işletim sistemi özelliklerini ayarlama
Artık hazır tooset hello sanal makinenin işletim sistemi özellikleri bulunur. Merhaba kullanacağız [kümesi AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) işletim sistemi olarak Windows, cmdlet tooset hello türü gerektiren hello [sanal makine aracısını](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) yüklü toobe belirtin, hello cmdlet'i otomatik sağlar Güncelleştirme ve hello sanal makine adı, hello bilgisayar adı ve daha önce başlatılmış hello değişkenler kullanarak hello kimlik bilgilerini ayarlayın.

Aşağıdaki cmdlet'i tooset hello işletim sistemi özelliklere sanal makineniz için hello yürütün.

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-hello-network-interface-toohello-virtual-machine"></a>Merhaba ağ arabirimi toohello sanal makine ekleyin
Ardından, daha önce toohello sanal makine oluşturduğumuz hello ağ arabirimi ekleyeceğiz. Merhaba kullanacağız [Ekle AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) daha önce tanımlanan hello ağ arabirimi değişkeni kullanarak cmdlet tooadd hello ağ arabirimi.

Cmdlet tooset hello ağ arabirimi sanal makineniz için aşağıdaki hello yürütün.

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-hello-blob-storage-location-for-hello-disk-toobe-used-by-hello-virtual-machine"></a>Merhaba sanal makine tarafından kullanılan hello disk toobe için Hello blob depolama konumu ayarlayın
Ardından, daha önce tanımlanan hello değişkenleri kullanarak hello sanal makine tarafından kullanılan hello disk toobe için hello blob depolama konumu ayarlarız.

Cmdlet tooset hello blob depolama konumu aşağıdaki hello yürütün.

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-hello-operating-system-disk-properties-for-hello-virtual-machine"></a>Merhaba işletim sistemi hello sanal makine disk özelliklerini ayarlama
Ardından, biz hello işletim sistemi hello sanal makine için disk özelliklerini ayarlar. Merhaba kullanacağız [kümesi AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) hello sanal makine için işletim sistemini hello cmdlet toospecify görüntüden tooread yalnızca önbelleğe alma tooset gelen (SQL Server üzerinde hello yüklendiği aynı disk) ve tanımlayın Merhaba sanal makine adı ve daha önce tanımladığımız hello değişkenleri kullanılarak tanımlanan hello işletim sistemi diski.

Aşağıdaki cmdlet'i tooset hello işletim sistemi disk özelliklere sanal makineniz için hello yürütün.

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-hello-platform-image-for-hello-virtual-machine"></a>Merhaba sanal makine için Hello platform görüntüsü belirtin
Bizim son yapılandırma adımı toospecify hello platform görüntüsü bizim sanal makine için ' dir. Merhaba en son SQL Server 2016 CTP görüntü öğreticimizi için kullanıyoruz. Merhaba kullanacağız [kümesi AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet toouse daha önce tanımlanan hello değişkenleri tarafından tanımlandığı şekilde bu görüntü.

Cmdlet toospecify hello platform görüntüsü sanal makineniz için aşağıdaki hello yürütün.

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-hello-sql-vm"></a>Merhaba SQL VM oluşturma
Şimdi hello yapılandırma adımlarını tamamladıktan hazır toocreate hello sanal makine demektir. Merhaba kullanacağız [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) biz tanımladığınız hello değişkenleri kullanarak cmdlet toocreate hello sanal makine.

Cmdlet toocreate aşağıdaki hello sanal makineniz yürütün.

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

Merhaba sanal makine oluşturulur. Merhaba depolama hesabı hello sanal makinenin disk için belirtilen çünkü standart depolama hesabı için önyükleme tanılaması oluşturduğunuz bildirim premium depolama hesabı anlamına gelmektedir.

Bu makinenin hello Azure Portal toosee görüntüleyebiliyorum [ortak IP adresini ve tam etki alanı adını](virtual-machines-windows-portal-sql-server-provision.md).

## <a name="example-script"></a>Örnek komut dosyası
Merhaba aşağıdaki betiği hello tam PowerShell komut dosyası Bu öğretici için içerir. Kurulum hello Azure aboneliği toouse hello ile zaten sahip olduğunuzu varsayar **Add-AzureRmAccount** ve **Select-AzureRmSubscription** komutları.

    # Variables
    ## Global
    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"
    ## Storage
    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

    ## Network
    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $TCPIPAllocationMethod = "Dynamic"
    $DomainName = "sqlvm1"

    ##Compute
    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

    ##Image
    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

    # Resource Group
    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

    # Storage
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

    # Network
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix
    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig
    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName
    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

    # Compute
    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize
    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."
    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate #-TimeZone = $TimeZone
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

    # Image
    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

    ## Create hello VM in Azure
    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

## <a name="next-steps"></a>Sonraki adımlar
Merhaba sanal makine oluşturulduktan sonra RDP ve Kurulum bağlantısı kullanarak hazır tooconnect toohello sanal makine olursunuz. Daha fazla bilgi için bkz: [tooa Azure (Kaynak Yöneticisi) üzerinde SQL Server sanal makinesine bağlanmak](virtual-machines-windows-sql-connect.md).

