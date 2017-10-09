---
title: SQL Server ile Azure Premium Storage aaaUse | Microsoft Docs
description: "Bu makalede hello Klasik dağıtım modeli kullanılarak oluşturulmuş kaynaklarını kullanır ve Azure sanal makinelerde çalışan SQL Server ile Azure Premium Storage kullanma hakkında yönergeler sağlar."
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 7ccf99d7-7cce-4e3d-bbab-21b751ab0e88
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/01/2017
ms.author: jroth
ms.openlocfilehash: 393ea2020b39ea686302ae632e1049935c24af00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-premium-storage-with-sql-server-on-virtual-machines"></a>Sanal Makineler’de SQL Server ile Azure Premium Depolama kullanma
## <a name="overview"></a>Genel Bakış
[Azure Premium Storage](../../../storage/common/storage-premium-storage.md) olan hello nesil düşük gecikme süresi ve yüksek verimlilik GÇ sağlayan depolama. Anahtar g/ç yoğun iş yükleri, Iaas üzerinde SQL Server gibi en iyi şekilde çalışır [sanal makineleri](https://azure.microsoft.com/services/virtual-machines/).

> [!IMPORTANT]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.

Bu makale, planlama ve SQL Server toouse Premium depolama çalışan bir sanal makine geçirmek için yönergeler sağlar. Bu, Azure altyapı (ağ, depolama) ve Konuk Windows VM adımları içerir. Merhaba Hello örnekte [ek](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) nasıl toomove büyük VM'ler tootake avantajı, geliştirilmiş, tam kapsamlı son tooend geçiş yerel gösterir SSD depolama PowerShell ile.

Bu önemli toounderstand hello uçtan uca kullanılarak Azure Premium Storage IAAS Vm'leri üzerinde SQL Server ile işlemidir. Buna aşağıdakiler dahildir:

* Merhaba Önkoşullar toouse Premium depolama kimliği.
* Yeni dağıtımlar için Iaas tooPremium depolama üzerinde SQL Server'ı dağıtma örnekleri.
* Geçirme varolan dağıtımları, hem tek başına sunucular hem de SQL Always On kullanılabilirlik grupları kullanarak dağıtımları örnekleri.
* Olası geçiş yaklaşıyor.
* Azure, Windows ve SQL Server adımları hello geçişi için mevcut bir Always On uygulamasına gösteren baştan sona tam örnek.

Azure Virtual Machines'de SQL Server üzerinde daha fazla bilgi için bkz: [Azure Virtual Machines'de SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

**Yazar:** Daniel Sol **Teknik İnceleme:** Haluk Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz'e.

## <a name="prerequisites-for-premium-storage"></a>Premium depolama için Önkoşullar
Premium depolama kullanmak için birkaç önkoşul vardır.

### <a name="machine-size"></a>Makine boyutu
Premium depolama kullanmak için toouse DS serisi sanal makineler (VM) gerekir. Bulut hizmetinizde önce DS serisi makineler kullanmadıysanız VM varolan hello silmek, bağlı hello diskleri tutmak ve ardından yeni bir bulut hizmeti hello VM DS * rol boyutu olarak yeniden oluşturmadan önce oluşturmanız gerekir. Sanal makine boyutları hakkında daha fazla bilgi için bkz: [sanal makine ve bulut hizmeti boyutları Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="cloud-services"></a>Bulut hizmetleri
Yeni bir bulut hizmetinde oluşturduğunuzda, DS * VM'ler yalnızca Premium Storage ile kullanabilirsiniz. Azure'da SQL Server Always On kullanıyorsanız hello üzerinde her zaman dinleyicisi bulut hizmetiyle ilişkili toohello Azure iç veya dış yük dengeleyici IP adresini bakın. Bu makalede odaklanılmaktadır Bu senaryoda kullanılabilirliği korurken toomigrate.

> [!NOTE]
> Dağıtılan toohello olan ilk VM DS * serisi hello yeni bulut hizmeti.
>
>

### <a name="regional-vnets"></a>Bölgesel sanal ağlar
DS * VM'ler için hello sanal ağ (Bölgesel, VM'ler toobe barındırma VNET) yapılandırmanız gerekir. Bu "widens" Merhaba VNET diğer kümelerde sağlanan tooallow hello büyük VM'ler toobe olduğu ve bunların arasındaki iletişimi izin verir. Oysa "dar" VNET Hello ilk sonuçlarını gösterir ekran aşağıdaki hello hello vurgulanan konumu bölgesel sanal ağlara gösterir.

![RegionalVNET][1]

Bir Microsoft destek bileti toomigrate tooa yükseltebilirsiniz bölgesel sanal ağ, Microsoft yapacak bir değişiklik toocomplete hello geçiş tooregional sanal ağlar, değiştirin ardından hello ağ yapılandırmasında hello özelliği AffinityGroup. İlk hello PowerShell'de ağ yapılandırmasını dışarı aktarma ve hello yerine **AffinityGroup** hello özelliğinde **VirtualNetworkSite** öğesi ile bir **konumu** özellik. Belirtin `Location = XXXX` burada `XXXX` bir Azure bölgesi. Ardından hello yeni yapılandırmasını alın.

Örneğin, VNET yapılandırmasını aşağıdaki hello dikkate:

    <VirtualNetworkSite name="danAzureSQLnet" AffinityGroup="AzureSQLNetwork">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

toomove bu tooa Batı Avrupa'da bölgesel sanal ağ aşağıdaki hello yapılandırma toohello değiştirin:

    <VirtualNetworkSite name="danAzureSQLnet" Location="West Europe">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

### <a name="storage-accounts"></a>Depolama hesapları
Toocreate Premium Storage için yapılandırılan yeni bir depolama hesabı gerekir. DS * serisi VM kullanırken VHD'ler Premium ve standart depolama hesaplarından ekleyebilirsiniz ancak Premium Storage hello kullan değil, tek tek VHD'ler hello depolama hesabında ayarlandığını unutmayın. Premium depolama hesabı toohello üzerinde tooplace hello OS VHD istemiyorsanız bu düşünebilirsiniz.

Merhaba aşağıdaki **yeni AzureStorageAccountPowerShell** hello "Premium_LRS" komutunu **türü** bir Premium depolama hesabı oluşturur:

    $newstorageaccountname = "danpremstor"
    New-AzureStorageAccount -StorageAccountName $newstorageaccountname -Location "West Europe" -Type "Premium_LRS"   

### <a name="vhds-cache-settings"></a>VHD'ler önbellek ayarları
Premium depolama hesabı parçası olan diskleri oluşturma arasındaki temel fark hello hello disk önbelleği ayardır. SQL Server veri birimi, diskler için kullanmanız önerilir '**okuma önbelleği**'. İşlem günlük birimleri için hello disk önbellek ayarı çok ayarlanmalıdır '**hiçbiri**'. Bu, standart depolama hesapları için hello önerilerden farklıdır.

Merhaba VHD'ler bağlandıktan sonra hello önbellek ayarı değiştirilemez. Toodetach ihtiyacınız ve hello VHD güncelleştirilmiş önbellek ayarı ile yeniden ekleyin.

### <a name="windows-storage-spaces"></a>Windows depolama alanları
Kullanabileceğiniz [Windows depolama alanları](https://technet.microsoft.com/library/hh831739.aspx) önceki standart depolama ile yaptığınız gibi bu, toomigrate zaten depolama alanları kullanan bir VM olanak tanır. Merhaba örnekte [ek](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) Powershell kodu tooextract hello ve birden çok ekli VHD'yle bir VM'yi alma (adım 9 ve ileriye doğru) gösterir.

Depolama havuzları standart Azure depolama hesabı tooenhance işleme ile kullanılan ve gecikme süresini azaltmak. Yeni dağıtımlar için Premium depolama ile depolama havuzlarını testinde değeri bulabilirsiniz, ancak depolama kuruluma ek karmaşıklık ekleyin.

#### <a name="how-toofind-which-azure-virtual-disks-map-toostorage-pools"></a>Nasıl toofind hangi Azure sanal disklerin eşleme toostorage havuzları
Ekli VHD'ler için farklı önbellek ayarı öneriler olarak toocopy hello VHD'ler tooa Premium depolama hesabı karar verebilirsiniz. Ancak, bunları toohello yeni DS serisi VM bağladığınızda tooalter hello önbellek ayarları gerekebilir. Premium depolama hello SQL veri dosyalarını ve günlük dosyaları (yerine her ikisini de içeren tek bir VHD) için ayrı VHD'leri olduğunda önbellek ayarları önerilen daha basit tooapply hello olur.

> [!NOTE]
> SQL Server veri ve günlük dosyalarını hello g/ç erişimi desenleri veritabanı iş yükleri için aynı birimi seçeneği önbelleğe alma hello bağlıdır hello varsa. Yalnızca test hangi önbelleğe alma bu senaryo için en iyi seçenektir personeline gösterebilir.
>
>

Ancak, birden çok VHD toolook adresindeki gerekir hale Windows depolama alanları kullanıyorsanız VHD'ler eklenmiş özgün komut dosyaları tooidentify olan belirli hangi havuzda böylece, ardından hello önbellek ayarları ayarlayabilirsiniz uygun şekilde her disk için.

Özgün komut kullanılabilir tooshow yoksa hangi VHD'ler eşleme toohello depolama havuzu, aşağıdaki adımları toodetermine hello disk/depolama havuzu eşlemesini hello kullanabilirsiniz.

Her disk için hello aşağıdaki adımları kullanın:

1. Disklerin listesini alın bağlı hello ile tooVM **Get-AzureVM** komutu:

    Get-AzureVM - ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk
2. Merhaba Diskname ve LUN unutmayın.

    ![DisknameAndLUN][2]
3. Uzak Masaüstü hello VM başlatın. Çok Git**Bilgisayar Yönetimi** | **Aygıt Yöneticisi'ni** | **Disk sürücüleri**. Her bir hello 'Microsoft sanal diskler' Hello özelliklerine bakmak

    ![VirtualDiskProperties][3]
4. Merhaba LUN sayısı burada hello VHD toohello VM eklerken belirttiğiniz bir başvuru toohello LUN sayısıdır.
5. Toohello 'Microsoft sanal diski' Hello için Git **ayrıntıları** sekmesinde, ardından hello **özelliği** listesinde, çok Git**sürücü anahtarı**. Merhaba, **değeri**, Not hello **uzaklığı**, ekran aşağıdaki hello 0002 olduğu. Merhaba 0002 depolama havuzu başvuruları hello hello PhysicalDisk2 gösterir.

    ![VirtualDiskPropertyDetails][4]
6. Her depolama havuzu için disklerin hello çıkışı döküm ilişkili:

    Get-StoragePool - FriendlyName AMS1pooldata | Get-PhysicalDisk

    ![GetStoragePool][5]

Kullanabileceğiniz artık bu bilgileri tooassociate VHD'ler tooPhysical diskleri depolama havuzları bağlı.

VHD'ler tooPhysical diskleri depolama havuzları ayırmak ve Premium depolama hesabı tooa kopyalama eşledikten sonra bunları hello doğru önbellek ayarı ile ekleyin. Lütfen hello hello örnekte bkz [ek](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), 8-12 arası adımları. Bu adımları nasıl tooextract bir VM ekli VHD disk yapılandırma tooa CSV dosyası hello VHD'ler kopyalayın, hello disk yapılandırma önbelleği ayarlarını değiştirme ve tüm hello ile DS serisi VM diskleri bağlı olarak hello VM son olarak dağıtmanız gösterir.

### <a name="vm-storage-bandwidth-and-vhd-storage-throughput"></a>VM depolama bant genişliği ve VHD depolama üretilen iş
DS * VM boyutu belirtildi ve VHD boyutları hello hello üzerinde Hello depolama performansı bağlıdır. Merhaba VM'ler eklenebilecek ve en yüksek bant genişliği (MB/sn) destekleyecek hello VHD'ler hello sayısı için farklı kesintileri vardır. Merhaba belirli bir bant numaraları için bkz: [sanal makine ve bulut hizmeti boyutları Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Daha fazla IOPS ile büyük disk boyutları elde edilir. Geçiş yolunuz hakkında düşünürken, düşünmelisiniz. Ayrıntılar için [IOPS ve Disk türleri için bkz: hello tablosu](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).

Son olarak, VM'ye bağlı tüm diskler için destekleyecek farklı en fazla disk bant genişlikleri sahip göz önünde bulundurun. Yüksek yük altında hello en fazla disk kullanılabilir bant genişliği bu VM rol boyutu için saturate. Örneğin bir Standard_DS14 too512MB/s destekler; Bu nedenle, üç P30 disklerle hello disk bant genişliği hello VM saturate. Ancak bu örnekte, hello üretilen iş sınırı hello karışımını okuma ve yazma g/ç işlemine bağlı olarak aştı.

## <a name="new-deployments"></a>Yeni dağıtımlar
SQL Server Vm'lerinin tooPremium depolama nasıl dağıtabileceğiniz Hello sonraki iki bölümde gösterilmektedir. Önceden belirtildiği gibi Premium depolama üzerine tooplace hello işletim sistemi diski mutlaka gerekmez. Tooplace OS VHD hello üzerinde hiçbir yoğun g/ç iş yükleri amaçlanıyorsa, bu toodo seçebilirsiniz.

var olan Azure galeri görüntüleri kullanılarak Merhaba ilk örneği gösterilmektedir. Merhaba ikinci örnek nasıl toouse özel bir VM görüntüsü, gösterir var olan bir standart depolama hesabına sahip.

> [!NOTE]
> Bu örnekler, bölgesel bir sanal ağ zaten oluşturduğunuzu varsayalım.
>
>

### <a name="create-a-new-vm-with-premium-storage-with-gallery-image"></a>Premium depolama galeri görüntüsü ile birlikte yeni bir VM oluşturun
Merhaba örnekte nasıl tooplace OS VHD premium depolama hello ve Premium depolama VHD'yi gösterilir. Ancak, aynı zamanda bir standart depolama hesabında hello işletim sistemi diski yerleştirin ve ardından bir Premium depolama hesabında bulunan VHD ekleyin. Her iki senaryoyu gösterilmiştir.

    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Set up subscription
    Set-AzureSubscription -SubscriptionName $mysubscription
    Select-AzureSubscription -SubscriptionName $mysubscription -Current  

#### <a name="step-1-create-a-premium-storage-account"></a>1. adım: bir Premium depolama hesabı oluşturma
    #Create Premium Storage account, note Type
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  


#### <a name="step-2-create-a-new-cloud-service"></a>2. adım: yeni bir bulut hizmeti oluşturma
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-reserve-a-cloud-service-vip-optional"></a>3. adım: (isteğe bağlı) bir bulut hizmeti VIP ayırma
    #check exisitng reserved VIP
    Get-AzureReservedIP

    $reservedVIPName = “sqlcloudVIP”
    New-AzureReservedIP –ReservedIPName $reservedVIPName –Label $reservedVIPName –Location $location

#### <a name="step-4-create-a-vm-container"></a>4. adım: bir VM kapsayıcı oluşturma
    #Generate storage keys for later
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    ##Generate storage acc contexts
    $xioContext = New-AzureStorageContext –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary   

    #Create container
    $containerName = 'vhds'
    New-AzureStorageContainer -Name $containerName -Context $xioContext

#### <a name="step-5-placing-os-vhd-on-standard-or-premium-storage"></a>5. adım: İşletim sistemi VHD standart veya Premium Storage yerleştirme
    #NOTE: Set up subscription and default storage account which will be used tooplace hello OS VHD in

    #If you want tooplace hello OS VHD Premium Storage Account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $newxiostorageaccountname  

    #If you wanted tooplace hello OS VHD Standard Storage Account but attach Premium Storage VHDs then you would run this instead:
    $standardstorageaccountname = "danstdams"

    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $standardstorageaccountname

#### <a name="step-6-create-vm"></a>6. adım: VM oluşturma
    #Get list of available SQL Server Images from hello Azure Image Gallery.
    $galleryImage = Get-AzureVMImage | where-object {$_.ImageName -like "*SQL*2014*Enterprise*"}
    $image = $galleryImage.ImageName

    #Set up Machine Specific Information
    $vmName = "dsDan1"
    $vnet = "dansvnetwesteur"
    $subnet = "SQL"
    $ipaddr = "192.168.0.8"

    #Remember toochange tooDS series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "mycomplexpwd4*"

    #Create VM Config
    $vmConfigsl = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $image  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Add Data and Log Disks tooVM Config
    #Note hello size specified ‘-DiskSizeInGB 1023’, this will attach 2 x P30 Premium Storage Disk Type
    #Utilising hello Premium Storage enabled Storage account

    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-data1.vhd"
    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "logDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-log1.vhd"

    #Create VM
    $vmConfigsl  | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)  

    #Add RDP Endpoint
    $EndpointNameRDPInt = "3389"
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Add-AzureEndpoint -Name "EndpointNameRDP" -Protocol "TCP" -PublicPort "53385" -LocalPort $EndpointNameRDPInt  | Update-AzureVM

    #Check VHD storage account, these should be in $newxiostorageaccountname
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Get-AzureDataDisk
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName |Get-AzureOSDisk


### <a name="create-a-new-vm-toouse-premium-storage-with-a-custom-image"></a>Yeni bir VM toouse Premium depolama ile özel bir görüntü oluşturun
Bu senaryo, bir standart depolama hesabında bulunan var olan özelleştirilmiş görüntüleri sahip olduğu gösterir. Tooplace hello OS VHD istiyorsanız belirtildiği gibi Premium toocopy gerekir depolama hello standart depolama hesabı mevcut görüntü hello ve kullanılabilmesi için önce bunları tooa Premium depolama aktarın. Bir görüntü şirket içi, yapabilecekleriniz varsa bu yöntem toocopy de doğrudan toohello Premium depolama hesabı.

#### <a name="step-1-create-storage-account"></a>Adım 1: Depolama hesabı oluşturma
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Standard Storage account
    $origstorageaccountname = "danstdams"

#### <a name="step-2-create-cloud-service"></a>2. adım, bulut hizmeti oluşturma
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-use-existing-image"></a>3. adım: Mevcut görüntü kullanın
Varolan bir görüntü kullanabilirsiniz. Veya, [var olan bir makine görüntüsünü ele](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Not hello makine, görüntü toobe DS * makine yok. Merhaba görüntüsünü oluşturduktan sonra adımları Göster nasıl aşağıdaki hello toocopy onu toohello hello Premium Storage hesabıyla **başlangıç AzureStorageBlobCopy** PowerShell komutunu.

    #Get storage account keys:
    #Standard Storage account
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    #Premium Storage account
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Set up contexts for hello storage accounts:
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $destContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

#### <a name="step-4-copy-blob-between-storage-accounts"></a>4. adım: Kopyalama Blob Depolama hesapları arasında
    #Get Image VHD
    $myImageVHD = "dansoldonorsql2k14-os-2015-04-15.vhd"
    $containerName = 'vhds'

    #Copy Blob between accounts
    $blob = Start-AzureStorageBlobCopy -SrcBlob $myImageVHD -SrcContainer $containerName `
    -DestContainer vhds -Destblob "prem-$myImageVHD" `
    -Context $origContext -DestContext $destContext  

#### <a name="step-5-regularly-check-copy-status"></a>5. adım: Kopyalama durumu düzenli olarak kontrol edin:
    $blob | Get-AzureStorageBlobCopyState

#### <a name="step-6-add-image-disk-tooazure-disk-repository-in-subscription"></a>6. adım: Resim disk tooAzure disk deposu abonelikte ekleyin.
    $imageMediaLocation = $destContext.BlobEndPoint+"/"+$myImageVHD
    $newimageName = "prem"+"dansoldonorsql2k14"

    Add-AzureVMImage -ImageName $newimageName -MediaLocation $imageMediaLocation

> [!NOTE]
> Merhaba durumu başarılı raporları olsa da, bir disk kira hatası hala alabilir bulabilirsiniz. Bu durumda, yaklaşık 10 dakika bekleyin.
>
>

#### <a name="step-7--build-hello-vm"></a>7. adım: hello VM oluşturma
Burada görüntünüzü ve iki Premium depolama VHD'leri hello VM oluşturuyorsanız:

    $newimageName = "prem"+"dansoldonorsql2k14"
    #Set up Machine Specific Information
    $vmName = "dansolchild"
    $vnet = "westeur"
    $subnet = "Clients"
    $ipaddr = "192.168.0.41"

    #This will need toobe a new cloud service
    $destcloudsvc = "danregsvcamsxio2"

    #Use tooDS Series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS3"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "theM)stC0mplexP@ssw0rd!”


    #Create VM Config
    $vmConfigsl2 = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $newimageName  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-Datadisk-1.vhd"
    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "LogDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-logdisk-1.vhd"



    $vmConfigsl2 | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet

## <a name="existing-deployments-that-do-not-use-always-on-availability-groups"></a>Always On kullanılabilirlik grupları kullanmayın var olan dağıtımlar
> [!NOTE]
> Var olan dağıtımlar için öncelikle hello görmek [Önkoşullar](#prerequisites-for-premium-storage) bölümüne.
>
>

Always On kullanılabilirlik grupları hem de kullanmayın SQL Server dağıtımları için farklı noktalar vardır. Her zaman açık kullanmıyorsanız ve var olan bir tek başına SQL Server yüklüyse, yeni bir bulut hizmeti ve depolama hesabı kullanarak tooPremium depolama yükseltebilirsiniz. Seçenekler aşağıdaki hello göz önünde bulundurun:

* **Yeni bir SQL Server VM oluşturmak**. Yeni dağıtımlarda belirtildiği gibi yeni bir SQL Server bir Premium depolama hesabını kullanan VM oluşturabilirsiniz. Ardından yedekleme ve SQL Server yapılandırma ve kullanıcı veritabanlarını geri yükleyin. Merhaba uygulama güncelleştirilmiş toobe gerekir tooreference hello yeni SQL Server dahili veya harici erişiliyor durumunda. Yan yana (SxS) SQL Server Geçiş yaptığınız gibi 'dışı db' tüm nesneleri toocopy gerekir. Bu, oturum açma bilgileri, sertifikalar ve bağlantılı sunucular gibi nesneleri içerir.
* **Mevcut bir SQL Server VM'yi geçirme**. Bu SQL Server VM hello çevrimdışı duruma getirmeden sonra tüm bağlı kendi VHD'ler toohello Premium depolama hesabı kopyalama içeren tooa yeni bulut hizmeti, aktarma gerektirir. Merhaba VM çevrimiçi olduğunda Merhaba uygulaması Itanium tabanlı sistemler için hello sunucu ana bilgisayar adı olarak önce başvurur. Merhaba hello mevcut disk boyutunu hello performans özellikleri etkiler unutmayın. Örneğin, 400 GB disk P20 tooa yuvarlanmasını. Hello VM DS serisi VM olarak yeniden oluşturun ve Premium depolama VHD'yi ihtiyaç duyduğunuz hello boyutu/performans belirtimi, bu disk performansı gerektirmez biliyorsanız. Ardından detach ve hello SQL DB dosyaları yeniden ekleyin.

> [!NOTE]
> Hello boyutuna bağlı olarak hello boyutu bilincinde olmanız gereken hello VHD diskleri kopyalama Premium depolama diskini türüne anlamına gelir, bunların içine kalan, bu disk performans belirtimi belirler. Disk en yakın toohello yukarı yuvarlayın Azure boyutu, 400 GB disk varsa, bu P20 tooa yuvarlanacağı şekilde. Varolan g/ç gereksinimleri hello OS VHD bağlı olarak, size toomigrate bu tooa Premium depolama hesabı gerekmeyebilir.
>
>

SQL Server'ınızdaki dışarıdan erişiliyorsa hello bulut hizmeti VIP değiştirir. Tooupdate uç noktaları, ACL'ler ve DNS sahip olur ayarlar.

## <a name="existing-deployments-that-use-always-on-availability-groups"></a>Always On kullanılabilirlik grupları kullanan var olan dağıtımlar
> [!NOTE]
> Var olan dağıtımlar için öncelikle hello görmek [Önkoşullar](#prerequisites-for-premium-storage) bölümüne.
>
>

Başlangıçta bu bölümde biz nasıl her zaman açık Azure ağ ile etkileşim sırasında arar. Biz sonra geçişleri tootwo senaryolarda aşağı çalışmamasına neden olur: Burada miktar kapalı kalma süresi izin geçişler ve burada gerekir ulaşmanıza en düşük kapalı kalma geçişleri.

Bir dinleyici sanal bir DNS adı bir veya daha fazla SQL Server'lar arasında paylaşılan bir IP adresi ile birlikte kaydeden şirket içi SQL Server Always On kullanılabilirlik grupları kullanın. İstemciler bağlandığında bunlar hello dinleyici IP toohello birincil SQL Server yönlendirilir. Bu, o anda hello üzerinde her zaman IP kaynağı sahip hello sunucusudur.

![Üzerinde DeploymentsUseAlways][6]

Microsoft Azure'da hello VM üzerinde tek bir IP adresi atanmış tooa NIC bu nedenle, sipariş tooachieve Merhaba aynı şirket içi olarak Soyutlama Katmanı, Azure toohello iç/dış yük dengeleyici (ILB/ELB) atanan başlangıç IP adresi kullanan olabilir. Merhaba sunucular arasında paylaşılan hello IP kaynağı toohello ayarlanmış aynı IP hello ILB/ELB olarak. Bu hello DNS yayınlanırsa ve istemci trafiğini hello ILB/ELB toohello birincil SQL Server çoğaltma ile aktarılır. Merhaba ILB/ELB araştırmalar tooprobe hello üzerinde her zaman IP kaynağı kullandığından SQL sunucusu olan birincil bilir. Merhaba önceki örnekte ELB/ILB hello tarafından başvurulan bir uç nokta sahip her bir düğüm araştırmaları, hangisi yanıt birincil SQL Server hello.

> [!NOTE]
> Merhaba ILB ve ELB her ikisi de tooa belirli Azure bulut hizmeti atanır, bu nedenle tüm Azure bulut geçişte büyük olasılıkla yük dengeleyici IP değiştirecek bu hello anlamına gelir.
>
>

### <a name="migrating-always-on-deployments-that-can-allow-some-downtime"></a>Miktar kapalı kalma süresi sağlayan geçirme her zaman açık dağıtımları
Bazı kesintiler izin toomigrate her zaman açık dağıtımlar iki strateji vardır:

1. **Daha fazla ikincil çoğaltmaları tooan üzerinde her zaman küme varolan Ekle**
2. **Tooa geçirmek yeni her zaman üzerinde Küme**

#### <a name="1-add-more-secondary-replicas-tooan-existing-always-on-cluster"></a>1. Daha fazla ikincil çoğaltmaları tooan ekleme varolan her zaman üzerinde Küme
Bir strateji tooadd daha fazla ikincil kopya toohello her zaman üzerindeki kullanılabilirlik grubu değil. Merhaba dinleyicisi hello Yeni Yük Dengeleyici IP ile güncelleştirin ve bunları yeni bir bulut hizmeti tooadd gerekir.

##### <a name="points-of-downtime"></a>Kapalı kalma süresi noktalar:
* Küme doğrulama.
* Her zaman açık yük test etme için yeni ikincil öğe.

Windows depolama havuzları için daha yüksek g/ç işleme hello VM içinde kullanıyorsanız, ardından bu tam bir küme doğrulama sırasında çevrimdışına alınır. düğümleri toohello küme eklediğinizde hello doğrulama testi gereklidir. Bu ne kadar bu devam, yaklaşık bir saat, temsili test ortamı tooget sınamalısınız şekilde hello süresini toorun hello test farklılık gösterebilir.

Burada el ile yük devretme gerçekleştirebilirsiniz ve beklendiği gibi hello üzerinde yeni test chaos eklenen düğümleri tooensure her zaman üzerinde yüksek kullanılabilirlik işlevleri zaman hazırlamanız.

![DeploymentUseAlways On2][7]

> [!NOTE]
> Merhaba doğrulama çalışmadan önce hello depolama havuzları kullanıldığı SQL Server'ın tüm örneklerini durdurmanız gerekir.
>
> ##### <a name="high-level-steps"></a>Üst düzey adımlar
>

1. İki yeni SQL sunucusuna bağlı Premium depolama ile yeni bulut hizmeti oluşturun.
2. TAM yedeklemeler kopyalayın ve geri yükleme ile **NORECOVERY**.
3. 'Dışında kullanıcı DB' oturumları vb. gibi bağımlı nesnelere kopyalayın.
4. Yeni bir yeni iç yük dengeleyici'nı (ILB) oluşturun veya bir dış yük dengeleyici (ELB) kullanın ve ardından her iki yeni düğümde yük dengeli uç noktaları ayarlayın.

   > [!NOTE]
   > Devam etmeden önce tüm düğümleri hello doğru uç nokta yapılandırması sahip denetleyin
   >
   >
5. Kullanıcı/uygulama erişimi toohello SQL Server (depolama havuzlarını kullanıyorsanız) durdurun.
6. SQL Server motoru Hizmetleri tüm düğümler üzerinde (depolama havuzlarını kullanıyorsanız) durdurun.
7. Yeni düğümler toocluster ekleyin ve tam doğrulamayı çalıştırın.
8. Doğrulama başarılı olduktan sonra tüm SQL Server hizmetlerini başlatın.
9. İşlem günlüklerini yedekleme ve kullanıcı veritabanlarını geri yükleyin.
10. Hello her zaman üzerindeki kullanılabilirlik grubu yeni düğümleri eklemek ve çoğaltma içine yerleştirin **zaman uyumlu**.
11. Merhaba IP Ekle hello adresi kaynağı yeni bulut hizmeti ILB/ELB her zaman açık için PowerShell aracılığıyla hello çok siteli hello örnekte temel [ek](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage). Windows Kümelemesi içinde hello ayarlamak **olası sahipler** Merhaba, **IP adresi** kaynak toohello yeni düğümler eski. Merhaba Hello 'Aynı alt ağdaki IP adresi kaynağı ekleme' bölümüne bakın [ek](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).
12. Yük devretme tooone hello yeni düğüm.
13. Yeni düğümler otomatik yük devretme ortakları Hello yapın ve test yük devretmeleri.
14. Özgün düğüm kullanılabilirlik grubundan kaldırın.

##### <a name="advantages"></a>Avantajları
* Yeni SQL sunucuları olabilir (SQL Server ve uygulama) üzerinde tooAlways eklenmeden önce test.
* Merhaba VM boyutunu değiştirmek ve hello depolama tooyour tam gereksinimleri özelleştirebilirsiniz. Ancak, yararlı tookeep olacaktır tüm hello SQL dosya yolları aynı hello.
* Merhaba DB yedeklemeleri toohello ikincil çoğaltmaları hello aktarımını başladığında kontrol edebilirsiniz. Bu Azure kullanmaktan farklıdır **başlangıç AzureStorageBlobCopy** komutunu toocopy VHD'ler, zaman uyumsuz bir kopya olduğundan.

##### <a name="disadvantages"></a>Olumsuz yönleri
* Windows depolama havuzlarını kullanırken var. küme kapalı kalma süresi hello yeni ek düğüm için hello tam küme doğrulama sırasında
* Merhaba SQL Server sürümü ve hello varolan ikincil çoğaltmaların sayısı bağlı olarak, olabilirsiniz varolan ikinciller kaldırma olmadan daha fazla ikincil çoğaltmaları mümkün tooadd olabilir.
* Merhaba ikinciller ayarı uzun SQL veri aktarımı zamandan olabilir.
* Yoktur ek maliyet geçiş sırasında paralel olarak çalışan yeni makineler varken.

#### <a name="2-migrate-tooa-new-always-on-cluster"></a>2. Tooa geçirmek yeni her zaman üzerinde Küme
Başka bir toocreate yepyeni her zaman üzerinde Küme yepyeni düğümlerle yeni bulut hizmeti ve sonra yeniden yönlendirme hello istemcileri toouse stratejidir onu.

##### <a name="points-of-downtime"></a>Kapalı kalma süresi noktaları
Uygulamaların ve kullanıcıların toohello yeni her zaman açık dinleyici aktardığınızda kapalı kalma süresi yok. Merhaba kapalı kalma süresi bağlıdır:

* yeni sunucularda toorestore son işlem günlüğü yedeklemeleri toodatabases geçen hello süre.
* Merhaba geçen süre tooupdate istemci uygulamaları toouse yeni her zaman açık dinleyici.

##### <a name="advantages"></a>Avantajları
* Merhaba gerçek üretim ortamında, SQL Server sınayabilirsiniz ve işletim sistemi derleme değişiklikleri.
* Merhaba seçeneği toocustomize hello depolama sahip ve toopotentially VM boyutunu azaltabilirsiniz. Bu maliyet azalmasına neden olabilir.
* Bu işlem sırasında SQL Server yapı veya sürüm güncelleştirebilirsiniz. Ayrıca hello işletim sistemi yükseltme yapabilirsiniz.
* Merhaba önceki her zaman üzerinde Küme düz geri alma hedef olarak davranamaz.

##### <a name="disadvantages"></a>Olumsuz yönleri
* Eşzamanlı olarak çalıştıran her iki her zaman açık kümeler istiyorsanız hello dinleyici toochange hello DNS adı gerekir. Bu, istemci uygulama dizeleri hello yeni dinleyici adı yansıtmalıdır gibi yönetim ek yükü hello geçiş sırasında ekler.
* Eşitleme mekanizması olarak olası toominimize hello son eşitleme gereksinimleri geçişten önce yakın hello iki ortamları tookeep arasında uygulamalıdır.
* Var. hello yeni ortam çalıştıran varken maliyet geçiş sırasında eklenir.

### <a name="migrating-always-on-deployments-for-minimal-downtime"></a>Geçirme her zaman şirket dağıtımları için en az kapalı kalma süresi
En düşük kapalı kalma için her zaman açık geçirme dağıtımlar için iki strateji vardır:

1. **Var olan bir ikincil kullanma: tek siteli**
2. **Var olan ikincil çoğaltmalar kullanma: çok siteli**

#### <a name="1-utilize-an-existing-secondary-single-site"></a>1. Var olan bir ikincil kullanma: tek siteli
En az kapalı kalma süresi için bir strateji tootake ikincil mevcut bir buluta olan ve hello geçerli bulut hizmetinden kaldırın. Merhaba VHD'ler toohello yeni Premium depolama hesabı kopyalayın ve hello VM hello yeni bulut hizmeti oluşturun. Ardından Yük Devretme Kümelemesi ve dinleyicisinde hello güncelleştirin.

##### <a name="points-of-downtime"></a>Kapalı kalma süresi noktaları
* Merhaba yük dengeli uç noktasıyla hello son düğümü güncelleştirdiğinizde kapalı kalma süresi yok.
* İstemci/DNS yapılandırmanıza bağlı olarak, istemci yeniden bağlanmayı gecikebilir.
* Tootake hello üzerinde her zaman küme grubu çevrimdışı tooswap hello IP adreslerini çıkışı seçerseniz ek kapalı kalma süresi yok. Bu bir OR bağımlılığının kullanarak önlemek ve IP adresi kaynağı hello için olası sahipleri eklenir. Merhaba Hello 'Aynı alt ağdaki IP adresi kaynağı ekleme' bölümüne bakın [ek](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).

> [!NOTE]
> Bir her zaman üzerinde yük devretme ortağı olarak, eklenen düğümle toopartake hello istediğinizde tooadd Azure noktayla bir başvuru toohello yük dengeli kümesi gerekir. Merhaba çalıştırdığınızda **Ekle AzureEndpoint** toodo açık Bu, geçerli bağlantıları tooremain komutu, ancak yeni bağlantıları toohello dinleyicisi hello yük dengeleyici güncelleştirdi kadar kurulan mümkün toobe olmayacak. Sınama sırasında görülen toolast 90-120seconds, bu, bu test edilmelidir.
>
>

##### <a name="advantages"></a>Avantajları
* Hiçbir ek maliyet geçiş sırasında ücrete.
* Bire bir geçiş.
* Azaltılan karmaşıklık.
* Premium depolama SKU'ları için daha yüksek IOPS sağlar. Aracı diskleri VM hello ayrılmış ve toohello yeni bulut hizmeti, kopyalanan hello bir 3. taraf daha yüksek kapatma sağlar kullanılan tooincrease hello VHD boyutu olabilir. VHD boyutları artırmak için bu bkz [forum tartışmasına](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).

##### <a name="disadvantages"></a>Olumsuz yönleri
* Geçiş sırasında HA ve DR kaybı yoktur.
* 1:1 geçiş olarak mümkün toodownsize olmayabilir böylece VHD'ler, sayısı, sanal makineleri destekleyecek en az bir VM boyutu toouse sahip olur.
* Bu senaryo hello Azure kullanırsınız **başlangıç AzureStorageBlobCopy** zaman uyumsuz komutunu. Kopya tamamlanma hiçbir SLA yoktur. Bu veri tootransfer hello miktarına bağlıdır sırasındaki bekleme bağlıdır sırada hello kopyaları hello süresi olarak değişir. başka bir bölgede Premium Storage destekleyen Azure veri merkezine tooanother Hello aktarımı edecekse hello kopyalama süresini artırır. 2 düğümleri varsa, olası azaltma hello kopyalama testinde uzun sürdüğünde durumda göz önünde bulundurun. Bu fikir aşağıdaki hello içerebilir.
  * Bir geçici 3 SQL Server düğümü HA için üzerinde anlaşılan kapalı kalma süresi ile Merhaba geçişten önce ekleyin.
  * Azure zamanlanmış bakım dışında Hello geçiş çalıştırın.
  * Küme çekirdeğini doğru yapılandırılmış olun.  

##### <a name="high-level-steps"></a>Üst düzey adımlar
Bu belge tam son tooend örnek gösterilmemiştir ancak hello [ek](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) bu çevrelerini tooperform olabilir ayrıntıları sağlar.

![MinimalDowntime][8]

* Toplama disk yapılandırma ve kaldırma hello düğümü (ekli VHD'ler silmeyin).
* Premium depolama hesabı oluşturma ve standart depolama hesabı hello VHD'ler kopyalayın
* Yeni bulut hizmeti oluşturun ve bu bulut Hizmeti'nde hello SQL2 VM yeniden dağıtın. Merhaba VM oluşturma hello kullanarak özgün işletim sistemi VHD kopyalanan ve kopyalanan VHD hello ekleniyor.
* ILB yapılandırma / ELB ve uç noktalar ekleyebilirsiniz.
* Dinleyici ya da güncelleştirin:
  * Merhaba üzerindeki her zaman grubu alma, çevrimdışı ve güncelleştirme her zaman üzerinde dinleyicisi yeni ILB ile Merhaba / ELB IP adresi.
  * Veya başlangıç IP adresi kaynağı'Windows Kümeleme içine, yeni bulut hizmeti ILB/ELB PowerShell aracılığıyla ekleme. Ardından kümesi hello olası sahipler hello IP adresi kaynak toohello düğümü, SQL2, geçiş ve bu hello ağ adı veya bağımlılıkla olarak ayarlayın. Merhaba Hello 'Aynı alt ağdaki IP adresi kaynağı ekleme' bölümüne bakın [ek](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).
* DNS yapılandırması/yayma toohello istemcileri denetleyin.
* SQL1 VM'yi geçirmek ve 2-4 arası adımlar gidin.
* IP adresi kaynağının olası sahip hello için eklenen adımları 5ii kullanıyorsanız, ardından SQL1 ekleyin
* Test yük devretmeleri.

#### <a name="2-utilize-existing-secondary-replicas-multi-site"></a>2. Var olan ikincil çoğaltmalar kullanma: çok siteli
Birden fazla Azure veri merkezinde (DC) düğümleriniz varsa veya karma bir ortamınız varsa, bu ortam toominimize kapalı kalma süresi her zaman açık yapılandırması kullanabilirsiniz.

Merhaba toochange hello her zaman açık eşitleme tooSynchronous hello şirket içi veya ikincil Azure DC ve yük devretme için SQL Server toothat yaklaşımdır. Merhaba VHD'ler tooa Premium depolama hesabı kopyalayın ve hello makineyi yeni bir bulut hizmetinde yeniden dağıtın. Merhaba dinleyicisi güncelleştirin ve geri dönecek.

##### <a name="points-of-downtime"></a>Kapalı kalma süresi noktaları
Merhaba kapalı kalma süresi başlangıç zamanı toofailover toohello alternatif DC ve geri oluşur. Ayrıca, istemci/DNS yapılandırmasına bağlıdır ve istemci yeniden bağlanmayı gecikebilir.
Her zaman açık bir karma yapılandırma örneği aşağıdaki hello göz önünde bulundurun:

![MultiSite1][9]

##### <a name="advantages"></a>Avantajları
* Mevcut altyapısını kullanabilir.
* Öncelikle hello DR Azure DC üzerinde hello seçeneği toopre yükseltme hello Azure depolama olması.
* Merhaba DR Azure DC depolama yeniden.
* Yük devretme sınaması işlemlerini hariç geçiş sırasında en az iki yük devretme işlemlerini yoktur.
* Değil toomove SQL Server veri yedekleme ile gerekiyor ve geri yükleme.

##### <a name="disadvantages"></a>Olumsuz yönleri
* İstemci erişim tooSQL bağlı olarak sunucu olabilir daha yüksek gecikme süresi SQL Server alternatif bir DC toohello uygulamada çalışırken.
* Merhaba kopyalama zamanı VHD'ler tooPremium depolama uzun olabilir. Bu olup olmadığını tookeep hello hello kullanılabilirlik grubu düğümü üzerinde kararınızı etkileyebilir. Bu işlem günlüğünde çoğaltılmamış işlemleri hello tookeep hello birincil düğüm gerekeceğinden günlük yoğun iş yükleri hello geçiş sırasında çalışan gerekli olduğunda için göz önünde bulundurun. Bu nedenle bu önemli oranda artma.
* Bu senaryo hello Azure kullanırsınız **başlangıç AzureStorageBlobCopy** zaman uyumsuz komutunu. Tamamlanma hiçbir SLA yoktur. Bu sıradaki bekleme bağlıdır sırada hello zaman hello kopyaları, değişir hello veri tootransfer miktarına bağlıdır. Bu nedenle 2 veri merkezinizde yalnızca bir düğüme sahip, hello kopyalama testinde uzun sürdüğünde durumda azaltma adımlarını sürer. Bu fikir aşağıdaki hello içerebilir.
  * Geçici bir 2 SQL düğüm HA için üzerinde anlaşılan kapalı kalma süresi ile Merhaba geçişten önce ekleyin.
  * Azure zamanlanmış bakım dışında Hello geçiş çalıştırın.
  * Küme çekirdeğini doğru yapılandırılmış olun.

Bu senaryo, yüklemenizi belgelenmiş ve en yüksek disk önbelleği ayarları için sipariş toomake değişiklikleri hello depolama nasıl eşlenen bilmeniz varsayar.

##### <a name="high-level-steps"></a>Üst düzey adımlar
![Multisite2][10]

* Şirket içi hello / Azure DC hello SQL Server birincil alternatif ve diğer otomatik yük devretme iş ortağı (AFP) hello hale olun.
* SQL2 ve Kaldır hello düğümü (ekli VHD'ler silmeyin) disk yapılandırma bilgilerini toplayın.
* Premium depolama hesabı oluşturma ve standart depolama hesabı hello VHD'ler kopyalayın.
* Yeni bir bulut hizmeti oluşturun ve kendi prim depolama diskleri ekli hello SQL2 VM oluşturun.
* ILB yapılandırma / ELB ve uç noktalar ekleyebilirsiniz.
* Güncelleştirme hello her zaman üzerinde dinleyicisi yeni ILB ile / ELB IP adresi ve test yük devretme.
* Merhaba DNS yapılandırmasını denetleyin.
* Merhaba AFP tooSQL2 değiştirin ve ardından SQL1 geçirmek ve 2 – 5 adımlarını gidin.
* Test yük devretmeleri.
* Merhaba AFP geri tooSQL1 ve SQL2 geçiş yapma

## <a name="appendix-migrating-a-multisite-always-on-cluster-toopremium-storage"></a>Ek: çoklu site her zaman üzerinde Küme tooPremium depolama birimi geçirme
Bu konuda Hello geri kalanı bir çoklu site her zaman açık küme tooPremium depolama dönüştürme ayrıntılı bir örnek sağlar. Ayrıca, bir dış yük dengeleyici (ELB) tooan iç yük dengeleyici (ILB) kullanarak hello dinleyicisi da dönüştürür.

### <a name="environment"></a>Ortam
* Windows 2k 12 / SQL 2k 12
* SP 1 DB dosyaları
* Düğüm başına depolama havuzları x 2

![Appendix1][11]

### <a name="vm"></a>VM:
Bu örnekte, biz ELB tooILB taşıma toodemonstrate adımıdır. Bu geçiş sırasında tooswitch toothis nasıl hello gösterecek şekilde ELB ILB önce mevcut değildi.

![Appendix2][12]

### <a name="pre-steps-connect-toosubscription"></a>Öncesi adımları: tooSubscription Bağlan
    Add-AzureAccount

    #Set up subscription
    Get-AzureSubscription

#### <a name="step-1-create-new-storage-account-and-cloud-service"></a>1. adım: Yeni depolama hesabı oluşturun ve bulut hizmeti
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Storage accounts
    #current storage account where hello vm toomigrate resides
    $origstorageaccountname = "danstdams"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Generate storage keys for later
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Generate storage acc contexts
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $xioContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $origstorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #CREATE NEW CLOUD SVC
    $vnet = "dansvnetwesteur"

    ##Existing cloud service
    $sourceSvc="dansolSrcAms"

    ##Create new cloud service
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location

#### <a name="step-2-increase-hello-permitted-failures-on-resources-optional"></a>2. adım: kaynakları hataları izin artış hello<Optional>
Tooyour her zaman üzerindeki kullanılabilirlik grubu ait bazı kaynaklar burada hello Küme hizmeti toorestart hello kaynak grubu çalışacak bir dönemde oluşabilir kaç hatalarda sınırları vardır. El ile yapmazsanız makineleri kapatılıyor tarafından yük devretme ve tetikleyici yük devretme Kapat toothis sınırı alabilirsiniz beri bu yordamı taramasını adımında, bu artırmanız önerilir.

Bu akıllıca toodouble hello hatası indirimi toodo yük devretme kümesi Yöneticisi'nde bunun olması, toohello hello her zaman açık kaynak grubunun özelliklerini gidin:

![Appendix3][13]

Merhaba en fazla hata sayısı too6 değiştirin.

#### <a name="step-3-addition-ip-address-resource-for-cluster-group-optional"></a>3. adım: Ek IP adresi kaynağı küme grubu için<Optional>
Yanlışlıkla hello bulut tüm küme düğümlerinde ağ sonra hello küme IP kaynak ve küme ağ adı mümkün toocome olmaz çevrimdışına varsa hello küme grubu için yalnızca bir IP adresi vardır ve bu hizalanmış toohello bulut alt yer alıyorsa, dikkatli olun Çevrimiçi. Hello engeller Bu olay tooother küme kaynaklarını güncelleştirir.

#### <a name="step-4-dns-configuration"></a>4. adım: DNS yapılandırması
sorunsuz bir geçiş bağlıdır nasıl DNS yüklenmekte olan tooimplement kullanılan ve güncelleştirildi.
Her zaman açık yüklendiğinde, bir Windows Küme kaynak grubu oluşturur yük devretme kümesi Yöneticisi'ni açın, göreceğiniz en az üç kaynaklara sahip olur, hello belge hello iki tooare başvuruyor:

* Sanal ağ adına (VNN) – budur hello DNS adı istemci tooconnect tooSQL sunucularına her zaman açık aracılığıyla isteyen toowhen bağlanın.
* IP adresi kaynağı – budur hello VNN hello ile ilişkili IP adresi, birden fazla olabilir ve çok siteli bir yapılandırma her site/alt ağda bir IP adresine sahip.

Bağlantı tooSQL sunucu, hello SQL Server istemci sürücüsü hello dinleyicisi ile ilişkili hello DNS kayıtlarını almak ve tooconnect tooeach deneyin Always On IP adresi ilişkili, aşağıda bu etkileyebilir bazı etkenler aşağıdakiler ele.

Merhaba hello dinleyicisi adıyla ilişkili eşzamanlı DNS kayıtlarının sayısı yalnızca hello ilişkili IP adreslerinin sayısı, aynı hello bağlıdır ' de Yük Devretme Kümelemesi hello her zaman açık VNN kaynak için RegisterAllIpProviders'setting.

Azure'da her zaman açık dağıttığınızda farklı adımlar toocreate hello dinleyicisi ve IP adresleri vardır, hello 'RegisterAllIpProviders' too1 yapılandırma toomanually sahip, bu her zaman açık farklı tooan şirket içi dağıtım nerede too1 ayarlayın.

'RegisterAllIpProviders' 0 ise, ardından yalnızca bir DNS kaydı DNS'de dinleyicisi hello ile ilişkili görürsünüz:

![Appendix4][14]

'RegisterAllIpProviders' 1 ise:

![Appendix5][15]

Aşağıdaki Hello kod hello VNN ayarları dökümü ve sizin için lütfen hello için Not Değiştir tootake etkisi tootake hello VNN çevrimdışı ve çevrimiçi geri dönüş gerekir, bu alma hello dinleyicisi çevrimdışı neden olan istemci bağlantı kesintisi.

    ##Always On Listener Name
    $ListenerName = "Mylistener"
    ##Get AlwaysOn Network Name Settings
    Get-ClusterResource $ListenerName| Get-ClusterParameter
    ##Set RegisterAllProvidersIP
    Get-ClusterResource $ListenerName| Set-ClusterParameter RegisterAllProvidersIP  1

Bu bir IP adresi kaynak temizleme ve ayrıca gerektireceğini, bir sonraki geçiş adımda tooupdate hello her zaman açık dinleyici bir yük dengeleyici başvurur güncelleştirilmiş bir IP adresi gerekir. Merhaba IP güncelleştirmeden sonra tooensure başlangıç IP adresi DNS bölgesinde güncelleştirildi ve hello istemciler kendi yerel DNS önbelleği güncelleştirdiğiniz yeni da gerekir.

İstemcilerinizi farklı ağ kesimdeki bulunur ve farklı bir DNS sunucusu başvuru isterseniz ne olur DNS bölge aktarma hakkında hello geçiş sırasında hello uygulama yeniden gibi zaman kısıtlı tooconsider gereksinim tarafından en az hello bölge aktarım zamanını tüm yeni IP adresleri hello dinleyici için. Burada zaman sınırlaması altında olup olmadığını ele almaktadır ve Windows ekipleriniz ile bir artımlı bölge aktarımı zorlama test ve ayrıca hello DNS konumuna ana bilgisayar kaydı tooa alt süresi tooLive (TTL), güncelleştirme hello istemciler için. Daha fazla bilgi için bkz: [artımlı bölge aktarımlarının](https://technet.microsoft.com/library/cc958973.aspx) ve [başlangıç DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).

Varsayılan hello hello Azure'nın her zaman açık dinleyicisinde ile ilişkili DNS kaydının TTL tarafından 1200 saniyedir. Merhaba dinleyici için kendi DNS güncelleştirilmiş hello IP adresi, geçiş tooensure hello istemcileri güncelleştirme sırasında zaman sınırlaması altında olduğunda bu tooreduce isteyebilir. Bakın ve hello VNN hello yapılandırma dökme tarafından hello yapılandırmasını değiştirin:

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"
    #Look at HostRecordTTL
    Get-ClusterResource $ListenerName| Get-ClusterParameter

    #Set HostRecordTTL Examples
    Get-ClusterResource $ListenerName| Set-ClusterParameter -Name "HostRecordTTL" 120

Lütfen hello alt hello 'HostRecordTTL', daha yüksek bir DNS trafik miktarı oluşacaktır unutmayın.

##### <a name="client-application-settings"></a>İstemci uygulama ayarları
.Net 4.5, SQL istemci uygulamanın desteklediği hello varsa SQLClient sonra kullanabileceğiniz ' MULTISUBNETFAILOVER = TRUE' anahtar sözcüğü, bu daha hızlı bağlantı tooSQL her zaman üzerindeki kullanılabilirlik grubu için yük devretme sırasında verdiğinden uygulanan toobe önerilir. Merhaba her zaman açık dinleyici paralel ile ilişkili tüm IP adreslerini aracılığıyla numaralandırır ve yük devretme sırasında daha agresif bir TCP bağlantı yeniden deneme hızı gerçekleştirir.

Yukarıdaki hello ayarlarla ilgili daha fazla bilgi için lütfen bkz [MultiSubnetFailover anahtar sözcüğü ve ilişkili özellikleri](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover). Ayrıca bkz. [SqlClient yüksek kullanılabilirlik, olağanüstü durum kurtarma desteği](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).

#### <a name="step-5-cluster-quorum-settings"></a>5. adım: Küme çekirdek ayarlarını
Aynı anda en az bir SQL Server kullanıma alma toobe kalacaklarını gibi dosya paylaşım tanığı (FSW) ile 2 düğümleri kullanarak hello çekirdek tooallow düğüm çoğunluğu ayarlamak ve dinamik oy kullanmasına ve bu tooallow için ise hello küme çekirdek ayarı değiştirmelisiniz bir tek düğümlü tooremain konumu.

    Set-ClusterQuorum -NodeMajority  

Yönetme ve hello küme çekirdek yapılandırması hakkında daha fazla bilgi için lütfen bkz [bir Windows Server 2012 yük devretme kümesinde çekirdeği yapılandırma ve yönetme hello](https://technet.microsoft.com/library/jj612870.aspx).

#### <a name="step-6-extract-existing-endpoints-and-acls"></a>6. adım: Mevcut uç noktalar ACL ayıklayıp
    #GET Endpoint info
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureEndpoint
    #GET ACL Rules for Each EP, this example is for hello Always On Endpoint
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureAclConfig -EndpointName "myAOEndPoint-LB"  

Bu tooa metin dosyasını kaydedin.

#### <a name="step-7-change-failover-partners-and-replication-modes"></a>7. adım: Yük devretme iş ortakları ve çoğaltma modları değiştirme
2'den fazla SQL sunucunuz varsa, başka bir DC başka bir ikincil hello yük devretme değiştirmeniz veya şirket içi too'Synchronous ve bir otomatik yük devretme iş ortağı (AFP) olun, değişiklik yapmadan adımında HA korumak için bu. Bunu TSQL yapabilirsiniz ancak SSMS değiştirin:

![Appendix6][16]

#### <a name="step-8-remove-secondary-vm-from-cloud-service"></a>8. adım: İkincil VM bulut hizmetinden kaldırın.
Toomigrate bulut ikincil düğüme planlama yapmanız gereken ilk olarak, bu şu anda birincil ise, el ile bir yük devretme başlatın.

    $vmNameToMigrate="dansqlams2"

    #Check machine status
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Shutdown secondary VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM


    #Extract disk configuration

    ##Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk config, make sure below returns hello disks associated with hello VM
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machibe is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-9-change-disk-caching-settings-in-csv-file-and-save"></a>9. adım: önbelleğe alma ayarları CSV dosyasındaki disk değiştirin ve kaydedin
Veri birimleri için bu tooREADONLY ayarlanmalıdır.

TLOG birimleri için bu tooNONE ayarlanmalıdır.

![Appendix7][17]

#### <a name="step-10-copy-vhds"></a>10. adım: Kopyalama VHD'leri
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContext

    ####DISK COPYING####
    #Get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname.blob.core.windows.net/vhds/$vhdname" `
    -SrcContext $origContext `
    -DestContainer $containerName `
    -DestBlob $vhdname `
    -DestContext $xioContext
       }



Merhaba kopyalama hello VHD'ler toohello Premium depolama hesabı durumunu denetleyebilirsiniz:

    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContext
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix8][18]

Bunların tümü başarılı kaydedilir kadar bekleyin.

Tek tek bloblar için daha fazla bilgi için:

    Get-AzureStorageBlobCopyState -Blob "blobname.vhd" -Container $containerName -Context $xioContext

#### <a name="step-11-register-os-disk"></a>11. adım: Kayıt işletim sistemi diski
    #Change storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

#### <a name="step-12-import-secondary-into-new-cloud-service"></a>12. adım: yeni bulut hizmetinde ikincil alma
Merhaba kodu aynı zamanda eklenen kullanır hello aşağıda seçeneği Burada, hello makine aktarıp hello retainable VIP kullanabilirsiniz.

    #Build VM Config
    $ipaddr = "192.168.0.5"
    #Remember toochange tooXIO
    $newInstanceSize = "Standard_DS13"
    $subnet = "SQL"

    #Create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###Attaching disks tooa VM during a deploy tooa new cloud service and new storage account is different from just attaching VHDs toojust a redeploy in a new cloud service
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)

#### <a name="step-13-create-ilb-on-new-cloud-svc-add-load-balanced-endpoints-and-acls"></a>13. adım: Yük eklemek ILB yeni bulut Svc üzerinde oluşturma dengeli uç noktaları ve ACL'leri
    #Check for existing ILB
    GET-AzureInternalLoadBalancer -ServiceName $destcloudsvc

    $ilb="sqlIntIlbDest"
    $subnet = "SQL"
    $IP="192.168.0.25"
    Add-AzureInternalLoadBalancer -ServiceName $destcloudsvc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP

    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM

    #SET Azure ACLs or Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

    ####WAIT FOR FULL AlwaysOn RESYNCRONISATION!!!!!!!!!#####

#### <a name="step-14-update-always-on"></a>14. adım: Her zaman üzerinde güncelleştir
    #Code toobe executed on a Cluster Node
    $ClusterNetworkNameAmsterdam = "Cluster Network 2" # hello azure cluster subnet network name
    $newCloudServiceIPAmsterdam = "192.168.0.25" # IP address of your cloud service

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"


    Add-ClusterResource "IP Address $newCloudServiceIPAmsterdam" -ResourceType "IP Address" -Group $AGName -ErrorAction Stop |  Set-ClusterParameter -Multiple @{"Address"="$newCloudServiceIPAmsterdam";"ProbePort"="59999";SubnetMask="255.255.255.255";"Network"=$ClusterNetworkNameAmsterdam;"OverrideAddressMatch"=1;"EnableDhcp"=0} -ErrorAction Stop

    #set dependancy and NETBIOS, then remove old IP address

    #set NETBIOS, then remove old IP address
    Get-ClusterGroup $AGName | Get-ClusterResource -Name "IP Address $newCloudServiceIPAmsterdam" | Set-ClusterParameter -Name EnableNetBIOS -Value 0

    #set dependency tooListener (OR Dependency) and delete previous IP Address resource that references:

    #Make sure no static records in DNS

![Appendix9][19]

Şimdi hello eski bulut hizmeti IP adresini kaldırın.

![Appendix10][20]

#### <a name="step-15-dns-update-check"></a>15. adım: DNS güncelleştirme denetimi
Şimdi DNS sunucuları, SQL Server istemci ağlarda denetlemeniz ve gerekir kümeleme hello eklenmiş olduğundan emin olun ek ana bilgisayar kaydı hello için eklenen IP adresi. Bu DNS sunucuları gerçekleştirmediyseniz hello orada alt ağdaki istemcilerin olduğundan mümkün tooresolve tooboth her zaman IP adresleri üzerindeki ve otomatik DNS çoğaltma için toowait gerek yoktur bu olduğundan emin ve DNS bölge aktarımı zorlama düşünün.

#### <a name="step-16-reconfigure-always-on"></a>16. adım: Her zaman yeniden yapılandırın
Bu noktada hello geçirilen toofully olan bu düğüme hello şirket içi düğümle ve yeniden eşitleyin ve toosynchronous çoğaltma düğümü geçiş hello AFP olun ikincil bekleyin.  

#### <a name="step-17-migrate-second-node"></a>17. adım: ikinci düğümü geçirme
    $vmNameToMigrate="dansqlams1"

    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Get endpoint information
    $endpoint = Get-AzureVM -ServiceName $sourceSvc  -Name $vmNameToMigrate | Get-AzureEndpoint

    #Shutdown VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM

    #Get disk config

    #Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk configuration
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machine is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-18-change-disk-caching-settings-in-csv-file-and-save"></a>Adım 18: önbelleğe alma ayarları CSV dosyasındaki disk değiştirin ve kaydedin
Veri birimleri için bu tooREADONLY ayarlanmalıdır.

TLOG birimleri için bu tooNONE ayarlanmalıdır.

![Appendix11][21]

#### <a name="step-19-create-new-independent-storage-account-for-secondary-node"></a>19. adım: İkincil düğüm için yeni bağımsız depolama hesabı oluşturma
    $newxiostorageaccountnamenode2 = "danspremsams2"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountnamenode2 -Location $location -Type "Premium_LRS"  

    #Reset hello storage account src if node 1 in a different storage account
    $origstorageaccountname2nd = "danstdams2"

    #Generate storage keys for later
    $xiostoragenode2 = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountnamenode2

    #Generate storage acc contexts
    $xioContextnode2 = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountnamenode2 -StorageAccountKey $xiostoragenode2.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

#### <a name="step-20-copy-vhds"></a>20. adım: Kopyalama VHD'leri
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContextnode2  

    ####DISK COPYING####
    ##get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname2nd.blob.core.windows.net/vhds/$vhdname" `
        -SrcContext $origContext `
        -DestContainer $containerName `
        -DestBlob $vhdname `
        -DestContext $xioContextnode2
       }

    #Check for copy progress

    #check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContext


Tüm VHD'leri için hello VHD kopya durumunu denetleyebilirsiniz: ForEach ($disk $diskobjects içinde) {$lun $disk =. LUN $vhdname $disk.vhdname $cacheoption = $disk =. HostCaching $disklabel $disk =. Disketiketi $diskName $disk =. DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContextnode2
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix12][22]

Bunların tümü başarılı kaydedilir kadar bekleyin.

Tek tek bloblar için daha fazla bilgi için:

    #Check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContextnode2

#### <a name="step-21-register-os-disk"></a>21. adım: Kayıt işletim sistemi diski
    #change storage account toohello new XIO storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

    #Build VM Config
    $ipaddr = "192.168.0.4"
    $newInstanceSize = "Standard_DS13"

    #Join tooexisting Avaiability Set

    #Build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###This is different toojust a straight cloud service change
    #note if you do not have a disk label hello command below will fail, populate as required.
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet -Verbose

#### <a name="step-22-add-load-balanced-endpoints-and-acls"></a>22. adım: Yük ekleme dengeli uç noktaları ve ACL'leri
    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM


    #STOP!!! CHECK in hello Azure portal or Machine Endpoints through PowerShell that these Endpoints are created!

    #SET ACLs or Azure Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

#### <a name="step-23-test-failover"></a>23. adım: Yük devretme sınaması
Artık her zaman açık hello şirket içi düğümle eşitleyin, toosynchronous çoğaltma modunda yerleştirin ve onu eşitlenene kadar bekleyin hello geçirilen düğüm izin vermemelisiniz. Ardından hello AFP olduğu bir şirket içi toohello ilk düğümü yük devretmeyi geçirildi. Çalıştıktan sonra değişiklik hello son düğümü toohello AFP geçirildi.

Test yük devretmeleri tüm düğümler arasında ve chaos testleri olarak tooensure yerine iş bekleniyordu ancak ve zamanında manor çalıştırmanız gerekir.

#### <a name="step-24-put-back-cluster-quorum-settings--dns-ttl--failover-pntrs--sync-settings"></a>24. adım: geri küme çekirdek ayarlarını Put / DNS TTL / yük devretme Pntrs / eşitleme ayarları
##### <a name="adding-ip-address-resource-on-same-subnet"></a>Aynı alt ağdaki IP adresi kaynağı ekleme
Yalnızca 2 SQL sunucunuz varsa ve toomigrate istediğiniz bunları tooa yeni bulut hizmeti, ancak tookeep istediğiniz üzerlerinde Merhaba aynı alt ağ, hello dinleyicisi her zaman çevrimdışı toodelete hello özgün IP adresinde almaktan kaçının ve hello yeni IP adresini ekleyin. Merhaba VM'ler tooanother alt ağı olacaktır gibi alt başvurur bir ek küme ağı, toodo bu ihtiyacınız olmadığından geçiriyorsanız.

Getirdiğiniz sonra hello ikincil geçiş ve yük devretme hello önce var olan birincil hello yeni IP adresi kaynak hello yeni bulut hizmeti için eklenen, hello küme Yük Devretme Yöneticisi içinde şu adımları uygulamanız:

tooadd IP adresini bakın hello [ek](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), 14. adım.

1. Hello olası sahip too'Existing birincil SQL Server Hello geçerli IP adresi kaynağı için Değiştir ', 'dansqlams4' aşağıda hello örnekte:

    ![Appendix13][23]
2. Merhaba olası sahip too'Migrated Hello yeni IP adresi kaynağı için değiştirme ikincil SQL Server', 'dansqlams5' aşağıda hello örnekte:

    ![Appendix14][24]
3. Merhaba son düğümü geçirildiğinde bu düğümü olası sahip olarak eklenir şekilde hello olası sahipler düzenlenmesi gerekir ve bu ayarlandıktan sonra Yük devretme kullanabilirsiniz:

    ![Appendix15][25]

## <a name="additional-resources"></a>Ek kaynaklar
* [Azure Premium depolama](../../../storage/common/storage-premium-storage.md)
* [Sanal Makineler](https://azure.microsoft.com/services/virtual-machines/)
* [Azure sanal makinelerde SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

<!-- IMAGES -->
[1]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/1_VNET_Portal.png
[2]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/2_Diskname_Lun.png
[3]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/3_Virtual_Disk_Properties.png
[4]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/4_Virtual_Disk_Properties_Details.png
[5]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/5_Get_Storage_Pool.png
[6]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/6_Deployments_Always_On.png
[7]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/7_Add_More_Secondaries.png
[8]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/8_Use_Existing_Secondary_Single_Site.png
[9]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site.png
[10]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site_b.png
[11]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_01.png
[12]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_02.png
[13]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_03.png
[14]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_04.png
[15]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_05.png
[16]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_06.png
[17]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_07.png
[18]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_08.png
[19]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_09.png
[20]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_10.png
[21]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_11.png
[22]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_12.png
[23]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_13.png
[24]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_14.png
[25]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_15.png
