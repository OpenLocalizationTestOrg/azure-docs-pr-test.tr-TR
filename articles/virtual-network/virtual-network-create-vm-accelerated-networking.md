---
title: "bir Azure sanal makinesi hızlandırılmış ağ aaaCreate | Microsoft Docs"
description: "Bilgi nasıl toocreate hızlandırılmış ağ sahip bir sanal makine."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 241362891bfe083ab32c2f558be54f63f87c0693
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a>Hızlandırılmış ağ ile bir sanal makine oluşturun

Bu öğreticide, bilgi nasıl toocreate hızlandırılmış ağ ile bir Azure sanal makine (VM). Windows için ve belirli Linux dağıtımları için genel Önizleme GA hızlandırılmış ağdır. Hızlandırılmış ağ tek köklü g/ç Sanallaştırması (SR-IOV) tooa VM, ağ performansını önemli ölçüde geliştirme sağlar. Bu yüksek performanslı yolu gecikme, değişim ve hello zorlu ağ iş yükleri desteklenen VM türler ile kullanmak için CPU kullanımını azaltma hello datapath hello konaktan atlar. Resim gösterir iletişimi ile ve hızlandırılmış ağ olmadan iki sanal makine (VM) arasında aşağıdaki hello:

![Karşılaştırma](./media/virtual-network-create-vm-accelerated-networking/image1.png)

Hızlandırılmış ağ olmadan hello VM ve dışındaki tüm ağ trafiğini hello konak ve sanal anahtar hello çapraz geçiş gerekir. Hello sanal anahtarı tüm ilke zorunluluğu sağlar, örneğin ağ güvenlik grubu olarak denetim listeleri, yalıtım ve diğer ağ sanallaştırılmış Hizmetleri toonetwork trafiğinin erişim. Merhaba okuma sanal anahtarları hakkında daha fazla toolearn [Hyper-V ağ sanallaştırma ve sanal anahtar](https://technet.microsoft.com/library/jj945275.aspx) makalesi.

Hızlandırılmış ağ ile ağ trafiğini hello VM'in ağ arabiriminin (NIC) ulaştığında ve ardından toohello VM iletilir. Sanal anahtar hello tüm ağ ilkeleri hızlandırılmış ağ Boşaltılan ve donanım uygulanan olmadan uygular. Donanım etkinleştirir hello NIC tooforward ilkesinde uygulama ağ trafiği doğrudan toohello hello ana uygulanan tüm hello İlkesi korurken hello konak ve sanal anahtar hello atlayarak VM.

Merhaba hızlandırılmış ağ yararları yalnızca toohello üzerinde etkin VM geçerlidir. İsteğe bağlı olarak Hello en iyi sonuçlar için ideal tooenable olan en az iki VM bu özelliğe bağlı toohello aynı Azure sanal ağ (VNet). Sanal ağlar veya içi bağlantı üzerinden iletişim kurarken, bu özellik en az etki toooverall gecikme vardır.

> [!WARNING]
> Genel Önizleme kullanılabilirliği ve güvenilirliği gibi özelliklere aynı düzeyde olan hello olmayabilir bu Linux genel kullanılabilirlik sürümü. Merhaba özelliği desteklenmiyor, yetenekleri kısıtlı ve tüm Azure konumlarda kullanılamayabilir. Merhaba en güncel bildirimleri için kullanılabilirlik ve bu özellik durumunu hello Azure Virtual Network güncelleştirmeleri sayfasında denetleyin.

## <a name="benefits"></a>Avantajlar
* **Düşük gecikme / saniye başına daha yüksek paket (pps):** kaldırma hello sanal anahtardan hello datapath hello ana bilgisayar ilke işleme için paketler harcadığınız hello zamanı kaldırır ve artar hello hello VM içinde işlenen paket sayısı.
* **Değişim azaltılmış:** sanal anahtar hello uygulanan toobe gereken ilke miktarını ve hello işlem yaptığını hello iş yükü hello CPU, üzerinde işlem bağlıdır. Hello ilkesi zorlama toohello donanım yük boşaltma, paketleri toohello hello konak tooVM iletişim ve tüm yazılım kesmelerini ve bağlam kaldırma VM anahtarları doğrudan sunarak bu değişkenlik kaldırır.
* **Düşük CPU kullanımı:** Bypassing hello sanal anahtarda hello ana ağ trafiğini işlemek için CPU kullanımı tooless yol açar.

## <a name="Limitations"></a>Sınırlamaları
Bu özelliği kullanırken aşağıdaki sınırlamalar hello mevcuttur:

* **Ağ arabirimi oluşturma:** hızlandırılmış ağ yalnızca yeni bir NIC için etkinleştirilmesi Varolan bir NIC için etkinleştirilemez
* **VM oluşturma:** etkin hızlandırılmış ağ ile bir NIC yalnızca VM oluşturulan hello zaman ekli tooa VM olması olabilir. Merhaba NIC VM varolan ekli tooan olamaz.
* **Bölgeler:** Windows VM hızlandırılmış ağ iletişimi ile birlikte, çoğu Azure bölgelerde sunulur. Linux VM'ler hızlandırılmış ağ ile birden çok bölgede sunulur. Bu özellik kullanılabilir hello bölgeleri genişletme. Aşağıda hello Azure sanal ağı güncelleştirmeleri blog hello en son bilgiler için bkz.   
* **Desteklenen işletim sistemleri:** Windows: Microsoft Windows Server 2012 R2 Datacenter ve Windows Server 2016. Linux: Ubuntu Server 16.04 LTS çekirdek 4.4.0-77 veya sonrası, SLES 12 SP2, RHEL 7.3 ve CentOS 7.3 (yayımlanmış "Standart dışı Wave yazılım").
* **VM boyutu:** genel amaçlı ve en az sekiz çekirdeği ile işlem iyileştirilmiş örnek boyutları. Daha fazla bilgi için bkz: Merhaba [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ve [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM boyutları makaleleri. Merhaba desteklenen VM örneği boyutlarının kümesi hello gelecekteki genişletilir.
* **Dağıtım Azure Resource Manager (ARM) aracılığıyla yalnızca:** hızlandırılmış ağ ASM/RDFE aracılığıyla dağıtımı için kullanılabilir değil.

Değişiklikleri toothese sınırlamalar hello duyurdu [Azure sanal ağı güncelleştirir](https://azure.microsoft.com/updates/accelerated-networking-in-preview) sayfası.

## <a name="create-a-windows-vm"></a>Windows VM oluşturma
Hello Azure portalında veya Azure kullanabilirsiniz [PowerShell](#windows-powershell) toocreate hello VM.

### <a name="windows-portal"></a>Portal

1. Bir Internet tarayıcısından hello Azure açın [portal](https://portal.azure.com) ve Azure ile oturum [hesap](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Zaten bir hesabınız yoksa, için kaydolabilirsiniz bir [ücretsiz deneme sürümü](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Merhaba Portalı'nda tıklatın **+ yeni** > **işlem** > **Windows Server 2016 Datacenter**. 
3. Merhaba, **Windows Server 2016 Datacenter** görünür, dikey bırakın *Resource Manager* altında seçilen **dağıtım modeli seçin**, tıklatıp **oluştur** .
4. Merhaba, **Temelleri** görünür, dikey hello aşağıdaki değerleri girin, varsayılan seçenekleri kalan hello bırakın veya seçin ya da kendi değerlerinizi girin ve hello'ı tıklatın **Tamam** düğmesi:

    |Ayar|Değer|
    |---|---|
    |Ad|MyVm|
    |Kaynak grubu|Bırakın **Yeni Oluştur** seçili ve girin *MyResourceGroup*|
    |Konum|Batı ABD 2|

    Yeni tooAzure değilseniz, hakkında daha fazla bilgi [kaynak grupları](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [abonelikleri](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), ve [konumları](https://azure.microsoft.com/regions) (tooas bölgeler adlandırılır da olduğu).
5. Merhaba, **bir boyutu seçin** görünür, dikey girin *8* hello içinde **Minimum çekirdek** kutusuna ve ardından **tümünü görüntülemek**.
6. Tıklatın **DS4_V2 standart**, veya desteklenen herhangi bir VM, hello ardından **seçin** düğmesi.
7. Merhaba, **ayarları** görünür, dikey olarak tüm ayarları bırakın-dışında tıklatın ise **etkin** altında **ağ hızlandırılmış**, hello'ye tıklayın **Tamam** düğmesi. **Not:** önceki adımlarda hello listelenmeyen değerleri VM boyutu, işletim sistemi veya konumu için seçtiğiniz, [sınırlamalar](#Limitations) bu makalenin bölümüne **hızlandırılmış ağ**görünür değil.
8. Merhaba, **Özet** görünür, dikey tıklayın hello **Tamam** düğmesi. Azure hello VM oluşturma başlatır. VM oluşturmak birkaç dakika sürer.
9. tooinstall hello için Windows ağ sürücüsü hızlandırılmış, tam hello adımları hello [Windows'u yapılandırma](#configure-windows) bu makalenin.

### <a name="windows-powershell"></a>PowerShell
1. Hello Azure PowerShell Hello en son sürümünü yüklemek [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modülü. Yeni tooAzure PowerShell değilseniz, hello okuma [Azure PowerShell genel bakış](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) makalesi.
2. Windows Başlat hello düğmesini tıklatarak bir PowerShell oturumu Başlat yazarak **powershell**, ardından **PowerShell** hello Arama sonuçlarından.
3. Merhaba, PowerShell penceresinde girin `login-azurermaccount` Azure oturum komutu toosign [hesap](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Zaten bir hesabınız yoksa, için kaydolabilirsiniz bir [ücretsiz deneme sürümü](https://azure.microsoft.com/offers/ms-azr-0044p).
4. Tarayıcınızda komut dosyası izleyen hello kopyalayın:
    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Windows `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName MicrosoftWindowsServer `
      -Offer WindowsServer `
      -Skus 2016-Datacenter `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. PowerShell pencerenize toopaste hello komut dosyasını sağ tıklatın ve, yürütülmekte başlatın. Bir kullanıcı adı ve parolası istenir. Bu kimlik bilgileri toolog toohello VM hello sonraki adımda tooit bağlanırken kullanın. Merhaba komut başarısız olursa ve değerleri hello komut yürütülmeden önce değiştirilen VM boyutu, işletim sistemi için kullanılan hello değerlerini onaylayın ve konum hello listelenen [sınırlamalar](#Limitations) bu makalenin.
6. tooinstall hello için Windows ağ sürücüsü hızlandırılmış, tam hello adımları hello [Windows'u yapılandırma](#configure-windows) bu makalenin.

### <a name="configure-windows"></a>Windows yapılandırma
Azure'da hello VM oluşturduktan sonra Windows hello hızlandırılmış ağ sürücüsü yüklemeniz gerekir. Aşağıdaki adımları hello tamamlamadan önce bir Windows VM ile hızlandırılmış ağ ya da hello kullanarak oluşturduğunuz gerekir [portal](#windows-portal) veya [PowerShell](#windows-powershell) bu makaledeki adımları. 

1. Bir Internet tarayıcısından hello Azure açın [portal](https://portal.azure.com) ve Azure ile oturum [hesap](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Zaten bir hesabınız yoksa, için kaydolabilirsiniz bir [ücretsiz deneme sürümü](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Merhaba metni içeren hello kutusunda *arama kaynakları* hello Azure portal hello üstünde yazın *MyVm*. Zaman **MyVm** görünür hello arama sonuçlarında tıklatın.
3. Merhaba, **MyVm** görünür, dikey tıklayın hello **Bağlan** hello sol üst köşesindeki hello dikey düğmesini. **Not:** varsa **oluşturma** hello altında görülebilir **Bağlan** düğmesi, Azure henüz tamamlanmadı hello VM oluşturma. Tıklatın **Bağlan** yalnızca artık gördükten sonra **oluşturma** hello altında **Bağlan** düğmesi.
4. Tarayıcı toodownload hello izin **MyVm.rdp** dosya.  Yüklendikten sonra hello dosya tooopen'ı tıklatın. 
5. Merhaba tıklatın **Bağlan** hello düğmesini **Uzak Masaüstü Bağlantısı** görünür, o hello hello uzak bağlantının yayımcısının belirlenemedi bildiren kutusu.
6. Hello içinde **Windows Güvenlik** görünen kutusu **daha fazla seçenek**, ardından **farklı bir hesap kullanın**. Merhaba kullanıcı adı ve 4. adımda girdiğiniz parola girin ve ardından hello **Tamam** düğmesi.
7. Merhaba tıklatın **Evet** görünür, hello hello uzak bilgisayarın kimliği doğrulanamıyor bildiren hello Uzak Masaüstü Bağlantısı kutusundaki düğmesi.
8. Merhaba Windows Başlat düğmesine sağ tıklatın ve **Aygıt Yöneticisi'ni**. Merhaba genişletin **ağ bağdaştırıcıları** düğümü. Bu hello onaylayın **Mellanox ConnectX-3 sanal işlev Ethernet bağdaştırıcısı** hello resim aşağıdaki gösterildiği gibi görünür:
   
    ![Cihaz Yöneticisi](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. Hızlandırılmış ağ, VM için etkinleştirilmiştir.

## <a name="create-a-linux-vm"></a>Linux VM oluşturma
Hello Azure portalında veya Azure kullanabilirsiniz [PowerShell](#linux-powershell) toocreate bir Ubuntu veya SLES VM. RHEL ve CentOS VM'ler için farklı bir iş akışı yok.  Merhaba yönergelere bakın.

### <a name="linux-portal"></a>Portal
1. Merhaba, 1-5 adımlarını izleyerek Linux Önizleme için ağ hızlandırılmış hello kaydolun [PowerShell bir Linux VM - oluşturma](#linux-powershell) bu makalenin.  Merhaba portalında hello Önizleme için kaydedilemiyor.
2. 1-8 içinde hello adımları tamamlayın [bir Windows VM - oluşturma portal](#windows-portal) bu makalenin. 2. adımda tıklatın **Ubuntu Server 16.04 LTS** yerine **Windows Server 2016 Datacenter**. Üretim dağıtımları için ya da kullanabilirsiniz ancak bu öğretici için toouse bir SSH anahtarı yerine bir parola seçin. Varsa **ağ hızlandırılmış** 7. adımını hello tamamladığınızda görünmez [bir Windows VM - oluşturma portal](#windows-portal) bölümünde bu makalede, büyük olasılıkla hello aşağıdaki nedenlerden biri için:
    - Henüz hello Önizleme için kayıtlı değil. Kayıt durumu olduğunu onaylayın **kayıtlı**hello 4 adımda açıklandığı gibi [Powershell bir Linux VM - oluşturma](#linux-powershell) bu makalenin. **Not:** hello hızlandırılmış katıldıysanız Windows VM'ler için Önizleme (buna ait hiçbir uzun gerekli tooregister toouse hızlandırılmış Windows VM'ler için ağ), ağ, otomatik olarak Merhaba hızlandırılmış kayıtlı olmayan için ağ Linux VM'ler Önizleme. Linux VM'ler tooparticipate da Önizleme için hello hızlandırılmış ağ için kaydetmeniz gerekir.
    - Bir VM boyutu, işletim sistemi veya hello listelenen konum seçmediniz [sınırlamalar](#limitations) bu makalenin.
3. Linux için tooinstall hello hızlandırılmış ağ sürücüsü, tam hello adımları hello [yapılandırma Linux](#configure-linux) bu makalenin.

### <a name="linux-powershell"></a>PowerShell

>[!WARNING]
>Bir abonelikte hızlandırılmış ağ ile Linux VM'ler oluşturmak ve ardından toocreate hello hızlandırılmış ağ ile bir Windows VM çalışırsanız aynı abonelik hello Windows VM oluşturma başarısız olabilir. Bu önizleme sırasında ayrı Aboneliklerde hızlandırılmış ağ ile Linux ve Windows VM'ler test önerilir.
>

1. Hello Azure PowerShell Hello en son sürümünü yüklemek [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modülü. Yeni tooAzure PowerShell değilseniz, hello okuma [Azure PowerShell genel bakış](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) makalesi.
2. Windows Başlat hello düğmesini tıklatarak bir PowerShell oturumu Başlat yazarak **powershell**, ardından **PowerShell** hello Arama sonuçlarından.
3. Merhaba, PowerShell penceresinde girin `login-azurermaccount` Azure oturum komutu toosign [hesap](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Zaten bir hesabınız yoksa, için kaydolabilirsiniz bir [ücretsiz deneme sürümü](https://azure.microsoft.com/offers/ms-azr-0044p).
4. Azure için ağ hızlandırılmış hello kaydolun hello aşağıdaki adımları tamamlayarak önizleme:
    - Bir e-posta çok gönderme[ axnpreview@microsoft.com ](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) Azure abonelik kimliği ve kullanım. Aboneliğiniz etkinleştirilecek hakkında Microsoft'tan bir e-posta onayı için lütfen bekleyin.
    - Merhaba Önizleme için kayıtlı komutu tooconfirm aşağıdaki hello girin:
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        Adım 5 kadar ile devam etmeyin **kayıtlı** hello hello önceki komutu girdikten sonra çıktısı görüntülenir. Devam etmeden önce çıktı hello aşağıdaki gibi çıktı benzemelidir:
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      >Merhaba hızlandırılmış katıldıysanız Windows VM'ler için Önizleme (buna ait hiçbir uzun gerekli tooregister toouse hızlandırılmış Windows VM'ler için ağ), ağ, otomatik olarak Merhaba hızlandırılmış kayıtlı olmayan Linux VM'ler Önizleme için ağ. Linux VM'ler tooparticipate da Önizleme için hello hızlandırılmış ağ için kaydetmeniz gerekir.
      >
5. Tarayıcınızda komut dosyası Ubuntu veya SLES istendiği gibi değiştirerek aşağıdaki hello kopyalayın.  Yeniden Redhat ve CentOS aşağıda açıklanan farklı bir iş akışı vardır:

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define hello new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Linux `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName Canonical `
      -Offer UbuntuServer `
      -Skus 16.04-LTS `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk -Name $OSDiskName `
      -VhdUri $OSDiskUri `
      -CreateOption FromImage 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. PowerShell pencerenize toopaste hello komut dosyasını sağ tıklatın ve, yürütülmekte başlatın. Bir kullanıcı adı ve parolası istenir. Bu kimlik bilgileri toolog toohello VM hello sonraki adımda tooit bağlanırken kullanın. Merhaba komut başarısız olursa, onaylayın:
    - 4. adımda açıklandığı gibi hello Önizleme için kayıtlı
    - VM boyutu, işletim sistemi türü veya konumu değerlerinin hello komut yürütülmeden önce değiştirdiğiniz varsa, hello değerleri hello listelenen [sınırlamalar](#Limitations) bu makalenin.
7. Linux için tooinstall hello hızlandırılmış ağ sürücüsü, tam hello adımları hello [yapılandırma Linux](#configure-linux) bu makalenin.

### <a name="configure-linux"></a>Linux yapılandırın

Azure'da hello VM oluşturduktan sonra Linux için hello hızlandırılmış ağ sürücüsü yüklemeniz gerekir. Aşağıdaki adımları hello tamamlamadan önce bir Linux VM ile hızlandırılmış ağ ya da hello kullanarak oluşturduğunuz gerekir [portal](#linux-portal) veya [PowerShell](#linux-powershell) bu makaledeki adımları. 

1. Bir Internet tarayıcısından hello Azure açın [portal](https://portal.azure.com) ve Azure ile oturum [hesap](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Zaten bir hesabınız yoksa, için kaydolabilirsiniz bir [ücretsiz deneme sürümü](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Merhaba portal, toohello sağındaki hello hello üstündeki *arama kaynakları* çubuğu, hello tıklatın **> _** simgesi toostart Bash bulut Kabuğu (Önizleme). Merhaba Bash bulut Kabuk bölmesi hello altındaki hello portal ve birkaç saniye sonra görünür sunan bir  **username@Azure:~ $** istemi. Bilgisayar, yerine hello bulut Kabuk SSH toohello VM kullanabilirsiniz ancak bu öğreticideki yönergeler hello hello bulut Kabuk kullanmakta olduğunuz varsayılır.
3. Merhaba portal Hello üstünde hello metin içeren hello kutusunda *arama kaynakları*, türü *MyVm*. Zaman **MyVm** görünür hello arama sonuçlarında tıklatın.
4. Merhaba, **MyVm** görünür, dikey tıklayın hello **Bağlan** hello sol üst köşesindeki hello dikey düğmesini. **Not:** varsa **oluşturma** hello altında görülebilir **Bağlan** düğmesi, Azure henüz tamamlanmadı hello VM oluşturma. Tıklatın **Bağlan** yalnızca artık gördükten sonra **oluşturma** hello altında **Bağlan** düğmesi.
5. Azure açılır tooenter hello bildiren bir kutusu `ssh adminuser@<ipaddress>`. ENTER hello bulut Kabuğu (veya onu görünen hello kutusundan adım 4 kopyalayın ve toohello bulut Kabuğu'nda yapıştırın), bu komutta ENTER tuşuna basın.
6. ENTER **Evet** toohello soru soran, toocontinue bağlanmak, isterseniz, ENTER tuşuna basın.
7. Merhaba VM oluştururken girdiğiniz hello parola girin. Gördüğünüz toohello VM, bir kez başarıyla oturum bir adminuser@MyVm:~ $ istemi. Şimdi toohello VM hello bulut kabuk oturumu aracılığıyla kaydedilir. **Not:** 10 dakika işlem yapılmadıktan sonra bulut Kabuk oturumları zaman aşımına uğrar.

Bu noktada, hello yönergeleri kullanmakta olduğunuz hello dağıtım göre farklılık gösterir. 

#### <a name="ubuntusles"></a>Ubuntu/SLES

1. Merhaba satırına girin `uname -r` ve hello sürümü için onaylayın:

    * Ubuntu olan "4.4.0-77-generic," veya daha büyük
    * SLES "4.4.59-92.20-default" olan veya daha büyük

2. Merhaba standart ağ Vnıc hızlandırılmış hello ağ Vnıc arasındaki bono izleyin çalışan hello komutlarıyla oluşturun. Hello hello bono ağ trafiği üzerinde bazı yapılandırma değişikliklerinin kesilmemesini sağlar ancak hızlandırılmış ağ Vnıc gerçekleştirme daha yüksek ağ trafiği kullanır.
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. 60 saniye duraklatmak sonra çalışan hello betik sonra hello VM yeniden başlatılır.
4. Bir kez VM yeniden hello yeniden tooit adımları 5-7'yi yeniden tamamlanıyor.
5. Merhaba çalıştırmak `ifconfig` komut ve bond0 gündeme ve hello arabirimi yukarı gösteren onaylayın. 
 
 >[!NOTE]
      >Hızlandırılmış ağ kullanan uygulamalar hello iletişim kurması gerekir *bond0* arabirim, *eth0*.  Genel kullanılabilirlik hızlandırılmış ağ erişmeden önce hello arabirim adı değişebilir.

#### <a name="rhelcentos"></a>RHEL/CentOS

Red Hat Enterprise Linux veya CentOS 7.3 VM oluşturma tooload hello en son sürücülere SR-IOV ve hello sanal işlev (VF) sürücüsünün hello ağ kartı için gereken bazı ek adımlar gerektirir. Merhaba hello yönergeleri ilk aşaması kullanılan toomake olabilir görüntünün bir veya daha fazla sanal hello sürücüleri önceden yüklenmiş olan makine hazırlar.

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a>Aşama bir: Red Hat Enterprise Linux veya CentOS 7.3 temel görüntü hazırlayın. 

1.  Bir olmayan - SRLOV CentOS 7.3 VM Azure sağlama

2.  LIS 4.2.2 yükleyin:
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  Yapılandırma dosyaları indirme
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  Bu VM yetkisini kaldırma

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  Azure portalından, bu VM'yi durdurun; ve tooVM'ın "disk" gidin, hello OSDisk'ın VHD URİ'si yakalayın. Bu URI hello temel görüntünün VHD adını ve kendi depolama hesabını içerir. 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a>İki aşama: sağlama yeni sanal makineleri Azure üzerinde

1.  Sağlama ile yeni AzureRMVMConfig dayalı yeni VM'ler kullanarak temel görüntü bir hello vNIC üzerinde etkin AcceleratedNetworking ile evrede VHD hello:

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
     -Name $RgName `
     -Location $Location

    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
     -Name MySubnet `
     -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
     -ResourceGroupName $RgName `
     -Location $Location `
     -Name MyVnet `
     -AddressPrefix 10.0.0.0/16 `
     -Subnet $Subnet
    
    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
     -Name MyPublicIp `
     -ResourceGroupName $RgName `
     -Location $Location `
     -AllocationMethod Static
    
    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify hello base image's VHD URI (from phase one step 5). 
    # Note: hello storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need tooreplace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for hello location from which hello new image binary large object (BLOB) is copied toostart hello virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential
    
    # Create a custom virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
     -VMName MyVM -VMSize Standard_DS4_v2 | `
    Set-AzureRmVMOperatingSystem `
     -Linux `
     -ComputerName myVM `
     -Credential $Cred | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk `
     -Name $OsDiskName `
     -SourceImageUri $sourceUri `
     -VhdUri $destOsDiskUri `
     -CreateOption FromImage `
     -Linux
    
    # Create hello virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  Yukarı VM'ler önyükleme sonra "tarafından lspci" Merhaba VF aygıt denetleyin ve hello Mellanox girişi denetleyin. Örneğin, biz bu öğede hello lspci çıktı görmeniz gerekir:
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  Merhaba bağlama betiği tarafından çalıştırın:

    ```bash
    sudo bondvf.sh
    ```

4.  Yeniden başlatma yeni VM'ler hello:

    ```bash
    sudo reboot
    ```

Merhaba VM hello hızlandırılmış ağ yolu etkin ve yapılandırılmış bond0 ile başlamanız gerekir.  Çalıştırma `ifconfig` tooconfirm.
