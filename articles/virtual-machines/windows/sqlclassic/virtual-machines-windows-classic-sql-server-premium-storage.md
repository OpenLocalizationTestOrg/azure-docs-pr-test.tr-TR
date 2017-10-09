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
# <a name="use-azure-premium-storage-with-sql-server-on-virtual-machines"></a><span data-ttu-id="050e8-103">Sanal Makineler’de SQL Server ile Azure Premium Depolama kullanma</span><span class="sxs-lookup"><span data-stu-id="050e8-103">Use Azure Premium Storage with SQL Server on Virtual Machines</span></span>
## <a name="overview"></a><span data-ttu-id="050e8-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="050e8-104">Overview</span></span>
<span data-ttu-id="050e8-105">[Azure Premium Storage](../../../storage/common/storage-premium-storage.md) olan hello nesil düşük gecikme süresi ve yüksek verimlilik GÇ sağlayan depolama.</span><span class="sxs-lookup"><span data-stu-id="050e8-105">[Azure Premium Storage](../../../storage/common/storage-premium-storage.md) is hello next generation of storage that provides low latency and high throughput IO.</span></span> <span data-ttu-id="050e8-106">Anahtar g/ç yoğun iş yükleri, Iaas üzerinde SQL Server gibi en iyi şekilde çalışır [sanal makineleri](https://azure.microsoft.com/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="050e8-106">It works best for key IO intensive workloads, such as SQL Server on IaaS [Virtual Machines](https://azure.microsoft.com/services/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="050e8-107">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="050e8-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="050e8-108">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="050e8-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="050e8-109">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="050e8-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="050e8-110">Bu makale, planlama ve SQL Server toouse Premium depolama çalışan bir sanal makine geçirmek için yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="050e8-110">This article provides planning and guidance for migrating a Virtual Machine running SQL Server toouse Premium Storage.</span></span> <span data-ttu-id="050e8-111">Bu, Azure altyapı (ağ, depolama) ve Konuk Windows VM adımları içerir.</span><span class="sxs-lookup"><span data-stu-id="050e8-111">This includes Azure infrastructure (networking, storage) and guest Windows VM steps.</span></span> <span data-ttu-id="050e8-112">Merhaba Hello örnekte [ek](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) nasıl toomove büyük VM'ler tootake avantajı, geliştirilmiş, tam kapsamlı son tooend geçiş yerel gösterir SSD depolama PowerShell ile.</span><span class="sxs-lookup"><span data-stu-id="050e8-112">hello example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) shows a full comprehensive end tooend migration of how toomove larger VMs tootake advantage of improved local SSD storage with PowerShell.</span></span>

<span data-ttu-id="050e8-113">Bu önemli toounderstand hello uçtan uca kullanılarak Azure Premium Storage IAAS Vm'leri üzerinde SQL Server ile işlemidir.</span><span class="sxs-lookup"><span data-stu-id="050e8-113">It is important toounderstand hello end-to-end process of utilizing Azure Premium Storage with SQL Server on IAAS VMs.</span></span> <span data-ttu-id="050e8-114">Buna aşağıdakiler dahildir:</span><span class="sxs-lookup"><span data-stu-id="050e8-114">This includes:</span></span>

* <span data-ttu-id="050e8-115">Merhaba Önkoşullar toouse Premium depolama kimliği.</span><span class="sxs-lookup"><span data-stu-id="050e8-115">Identification of hello prerequisites toouse Premium Storage.</span></span>
* <span data-ttu-id="050e8-116">Yeni dağıtımlar için Iaas tooPremium depolama üzerinde SQL Server'ı dağıtma örnekleri.</span><span class="sxs-lookup"><span data-stu-id="050e8-116">Examples of deploying SQL Server on IaaS tooPremium Storage for new deployments.</span></span>
* <span data-ttu-id="050e8-117">Geçirme varolan dağıtımları, hem tek başına sunucular hem de SQL Always On kullanılabilirlik grupları kullanarak dağıtımları örnekleri.</span><span class="sxs-lookup"><span data-stu-id="050e8-117">Examples of migrating existing deployments, both stand-alone servers and deployments using SQL Always On Availability Groups.</span></span>
* <span data-ttu-id="050e8-118">Olası geçiş yaklaşıyor.</span><span class="sxs-lookup"><span data-stu-id="050e8-118">Possible migration approaches.</span></span>
* <span data-ttu-id="050e8-119">Azure, Windows ve SQL Server adımları hello geçişi için mevcut bir Always On uygulamasına gösteren baştan sona tam örnek.</span><span class="sxs-lookup"><span data-stu-id="050e8-119">Full end-to-end example showing Azure, Windows, and SQL Server steps for hello migration of an existing Always On implementation.</span></span>

<span data-ttu-id="050e8-120">Azure Virtual Machines'de SQL Server üzerinde daha fazla bilgi için bkz: [Azure Virtual Machines'de SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="050e8-120">For more background information on SQL Server in Azure Virtual Machines, see [SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

<span data-ttu-id="050e8-121">**Yazar:** Daniel Sol **Teknik İnceleme:** Haluk Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz'e.</span><span class="sxs-lookup"><span data-stu-id="050e8-121">**Author:** Daniel Sol **Technical Reviewers:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span></span>

## <a name="prerequisites-for-premium-storage"></a><span data-ttu-id="050e8-122">Premium depolama için Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="050e8-122">Prerequisites for Premium Storage</span></span>
<span data-ttu-id="050e8-123">Premium depolama kullanmak için birkaç önkoşul vardır.</span><span class="sxs-lookup"><span data-stu-id="050e8-123">There are several prerequisites for using Premium Storage.</span></span>

### <a name="machine-size"></a><span data-ttu-id="050e8-124">Makine boyutu</span><span class="sxs-lookup"><span data-stu-id="050e8-124">Machine size</span></span>
<span data-ttu-id="050e8-125">Premium depolama kullanmak için toouse DS serisi sanal makineler (VM) gerekir.</span><span class="sxs-lookup"><span data-stu-id="050e8-125">For using Premium Storage you will need toouse DS series Virtual Machines (VM).</span></span> <span data-ttu-id="050e8-126">Bulut hizmetinizde önce DS serisi makineler kullanmadıysanız VM varolan hello silmek, bağlı hello diskleri tutmak ve ardından yeni bir bulut hizmeti hello VM DS * rol boyutu olarak yeniden oluşturmadan önce oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="050e8-126">If you have not used DS Series machines in your cloud service before, you must delete hello existing VM, keep hello attached disks, and then create a new cloud service before recreating hello VM as DS* role size.</span></span> <span data-ttu-id="050e8-127">Sanal makine boyutları hakkında daha fazla bilgi için bkz: [sanal makine ve bulut hizmeti boyutları Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="050e8-127">For more information on Virtual Machine sizes, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="cloud-services"></a><span data-ttu-id="050e8-128">Bulut hizmetleri</span><span class="sxs-lookup"><span data-stu-id="050e8-128">Cloud services</span></span>
<span data-ttu-id="050e8-129">Yeni bir bulut hizmetinde oluşturduğunuzda, DS * VM'ler yalnızca Premium Storage ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="050e8-129">You can only use DS* VMs with Premium Storage when they are created in a new cloud service.</span></span> <span data-ttu-id="050e8-130">Azure'da SQL Server Always On kullanıyorsanız hello üzerinde her zaman dinleyicisi bulut hizmetiyle ilişkili toohello Azure iç veya dış yük dengeleyici IP adresini bakın.</span><span class="sxs-lookup"><span data-stu-id="050e8-130">If you are using SQL Server Always On in Azure, hello Always On Listener will refer toohello Azure Internal or External Load Balancer IP address that is associated with a cloud service.</span></span> <span data-ttu-id="050e8-131">Bu makalede odaklanılmaktadır Bu senaryoda kullanılabilirliği korurken toomigrate.</span><span class="sxs-lookup"><span data-stu-id="050e8-131">This article focuses on how toomigrate while maintaining availability in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="050e8-132">Dağıtılan toohello olan ilk VM DS * serisi hello yeni bulut hizmeti.</span><span class="sxs-lookup"><span data-stu-id="050e8-132">A DS* Series must be hello first VM that is deployed toohello new Cloud Service.</span></span>
>
>

### <a name="regional-vnets"></a><span data-ttu-id="050e8-133">Bölgesel sanal ağlar</span><span class="sxs-lookup"><span data-stu-id="050e8-133">Regional VNETS</span></span>
<span data-ttu-id="050e8-134">DS * VM'ler için hello sanal ağ (Bölgesel, VM'ler toobe barındırma VNET) yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="050e8-134">For DS* VMs you must configure hello Virtual Network (VNET) hosting your VMs toobe regional.</span></span> <span data-ttu-id="050e8-135">Bu "widens" Merhaba VNET diğer kümelerde sağlanan tooallow hello büyük VM'ler toobe olduğu ve bunların arasındaki iletişimi izin verir.</span><span class="sxs-lookup"><span data-stu-id="050e8-135">This “widens” hello VNET is tooallow hello larger VMs toobe provisioned in other clusters and allow communication between them.</span></span> <span data-ttu-id="050e8-136">Oysa "dar" VNET Hello ilk sonuçlarını gösterir ekran aşağıdaki hello hello vurgulanan konumu bölgesel sanal ağlara gösterir.</span><span class="sxs-lookup"><span data-stu-id="050e8-136">In hello following screenshot, hello highlighted Location shows regional VNETs, whereas hello first result shows a “narrow” VNET.</span></span>

![RegionalVNET][1]

<span data-ttu-id="050e8-138">Bir Microsoft destek bileti toomigrate tooa yükseltebilirsiniz bölgesel sanal ağ, Microsoft yapacak bir değişiklik toocomplete hello geçiş tooregional sanal ağlar, değiştirin ardından hello ağ yapılandırmasında hello özelliği AffinityGroup.</span><span class="sxs-lookup"><span data-stu-id="050e8-138">You can raise a Microsoft support ticket toomigrate tooa regional VNET, Microsoft will make a change, then toocomplete hello migration tooregional VNETs, change hello property AffinityGroup in hello network configuration.</span></span> <span data-ttu-id="050e8-139">İlk hello PowerShell'de ağ yapılandırmasını dışarı aktarma ve hello yerine **AffinityGroup** hello özelliğinde **VirtualNetworkSite** öğesi ile bir **konumu** özellik.</span><span class="sxs-lookup"><span data-stu-id="050e8-139">First export hello Network Configuration in PowerShell, and then replace hello **AffinityGroup** property in hello **VirtualNetworkSite** element with a **Location** property.</span></span> <span data-ttu-id="050e8-140">Belirtin `Location = XXXX` burada `XXXX` bir Azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="050e8-140">Specify `Location = XXXX` where `XXXX` is an Azure region.</span></span> <span data-ttu-id="050e8-141">Ardından hello yeni yapılandırmasını alın.</span><span class="sxs-lookup"><span data-stu-id="050e8-141">Then import hello new configuration.</span></span>

<span data-ttu-id="050e8-142">Örneğin, VNET yapılandırmasını aşağıdaki hello dikkate:</span><span class="sxs-lookup"><span data-stu-id="050e8-142">For example, considering hello following VNET configuration:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" AffinityGroup="AzureSQLNetwork">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

<span data-ttu-id="050e8-143">toomove bu tooa Batı Avrupa'da bölgesel sanal ağ aşağıdaki hello yapılandırma toohello değiştirin:</span><span class="sxs-lookup"><span data-stu-id="050e8-143">toomove this tooa regional VNET in West Europe, change hello configuration toohello following:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" Location="West Europe">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

### <a name="storage-accounts"></a><span data-ttu-id="050e8-144">Depolama hesapları</span><span class="sxs-lookup"><span data-stu-id="050e8-144">Storage accounts</span></span>
<span data-ttu-id="050e8-145">Toocreate Premium Storage için yapılandırılan yeni bir depolama hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="050e8-145">You will need toocreate a new storage account that is configured for Premium Storage.</span></span> <span data-ttu-id="050e8-146">DS * serisi VM kullanırken VHD'ler Premium ve standart depolama hesaplarından ekleyebilirsiniz ancak Premium Storage hello kullan değil, tek tek VHD'ler hello depolama hesabında ayarlandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="050e8-146">Note that hello use of Premium Storage is set at hello storage account, not on individual VHDs, however when using a DS* Series VM you can attach VHD’s from Premium and Standard Storage accounts.</span></span> <span data-ttu-id="050e8-147">Premium depolama hesabı toohello üzerinde tooplace hello OS VHD istemiyorsanız bu düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="050e8-147">You may consider this if you do not want tooplace hello OS VHD on toohello Premium Storage account.</span></span>

<span data-ttu-id="050e8-148">Merhaba aşağıdaki **yeni AzureStorageAccountPowerShell** hello "Premium_LRS" komutunu **türü** bir Premium depolama hesabı oluşturur:</span><span class="sxs-lookup"><span data-stu-id="050e8-148">hello following **New-AzureStorageAccountPowerShell** command with hello "Premium_LRS" **Type** creates a Premium Storage Account:</span></span>

    $newstorageaccountname = "danpremstor"
    New-AzureStorageAccount -StorageAccountName $newstorageaccountname -Location "West Europe" -Type "Premium_LRS"   

### <a name="vhds-cache-settings"></a><span data-ttu-id="050e8-149">VHD'ler önbellek ayarları</span><span class="sxs-lookup"><span data-stu-id="050e8-149">VHDs Cache Settings</span></span>
<span data-ttu-id="050e8-150">Premium depolama hesabı parçası olan diskleri oluşturma arasındaki temel fark hello hello disk önbelleği ayardır.</span><span class="sxs-lookup"><span data-stu-id="050e8-150">hello main difference between creating disks that are part of a Premium Storage account is hello disk cache setting.</span></span> <span data-ttu-id="050e8-151">SQL Server veri birimi, diskler için kullanmanız önerilir '**okuma önbelleği**'.</span><span class="sxs-lookup"><span data-stu-id="050e8-151">For SQL Server Data volume disks it is recommended that you use ‘**Read Caching**’.</span></span> <span data-ttu-id="050e8-152">İşlem günlük birimleri için hello disk önbellek ayarı çok ayarlanmalıdır '**hiçbiri**'.</span><span class="sxs-lookup"><span data-stu-id="050e8-152">For Transaction log volumes, hello disk cache setting should be set too‘**None**’.</span></span> <span data-ttu-id="050e8-153">Bu, standart depolama hesapları için hello önerilerden farklıdır.</span><span class="sxs-lookup"><span data-stu-id="050e8-153">This is different from hello recommendations for Standard Storage accounts.</span></span>

<span data-ttu-id="050e8-154">Merhaba VHD'ler bağlandıktan sonra hello önbellek ayarı değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="050e8-154">Once hello VHDs have been attached, hello cache setting cannot be altered.</span></span> <span data-ttu-id="050e8-155">Toodetach ihtiyacınız ve hello VHD güncelleştirilmiş önbellek ayarı ile yeniden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="050e8-155">You would need toodetach and reattach hello VHD with an updated cache setting.</span></span>

### <a name="windows-storage-spaces"></a><span data-ttu-id="050e8-156">Windows depolama alanları</span><span class="sxs-lookup"><span data-stu-id="050e8-156">Windows storage spaces</span></span>
<span data-ttu-id="050e8-157">Kullanabileceğiniz [Windows depolama alanları](https://technet.microsoft.com/library/hh831739.aspx) önceki standart depolama ile yaptığınız gibi bu, toomigrate zaten depolama alanları kullanan bir VM olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="050e8-157">You can use [Windows Storage Spaces](https://technet.microsoft.com/library/hh831739.aspx) as you did with previous Standard Storage, this will allow you toomigrate a VM that is already utilizing Storage Spaces.</span></span> <span data-ttu-id="050e8-158">Merhaba örnekte [ek](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) Powershell kodu tooextract hello ve birden çok ekli VHD'yle bir VM'yi alma (adım 9 ve ileriye doğru) gösterir.</span><span class="sxs-lookup"><span data-stu-id="050e8-158">hello example in [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (step 9 and forward) demonstrates hello Powershell code tooextract and import a VM with multiple attached VHDs.</span></span>

<span data-ttu-id="050e8-159">Depolama havuzları standart Azure depolama hesabı tooenhance işleme ile kullanılan ve gecikme süresini azaltmak.</span><span class="sxs-lookup"><span data-stu-id="050e8-159">Storage Pools were used with Standard Azure storage account tooenhance throughput and reduce latency.</span></span> <span data-ttu-id="050e8-160">Yeni dağıtımlar için Premium depolama ile depolama havuzlarını testinde değeri bulabilirsiniz, ancak depolama kuruluma ek karmaşıklık ekleyin.</span><span class="sxs-lookup"><span data-stu-id="050e8-160">You might find value in testing Storage Pools with Premium Storage for new deployments, but they do add additional complexity with storage setup.</span></span>

#### <a name="how-toofind-which-azure-virtual-disks-map-toostorage-pools"></a><span data-ttu-id="050e8-161">Nasıl toofind hangi Azure sanal disklerin eşleme toostorage havuzları</span><span class="sxs-lookup"><span data-stu-id="050e8-161">How toofind which Azure Virtual Disks map toostorage pools</span></span>
<span data-ttu-id="050e8-162">Ekli VHD'ler için farklı önbellek ayarı öneriler olarak toocopy hello VHD'ler tooa Premium depolama hesabı karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="050e8-162">As there are different cache setting recommendations for attached VHDs, you might decide toocopy hello VHDs tooa Premium Storage account.</span></span> <span data-ttu-id="050e8-163">Ancak, bunları toohello yeni DS serisi VM bağladığınızda tooalter hello önbellek ayarları gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="050e8-163">However, when you reattach them toohello new DS series VM, you might need tooalter hello cache settings.</span></span> <span data-ttu-id="050e8-164">Premium depolama hello SQL veri dosyalarını ve günlük dosyaları (yerine her ikisini de içeren tek bir VHD) için ayrı VHD'leri olduğunda önbellek ayarları önerilen daha basit tooapply hello olur.</span><span class="sxs-lookup"><span data-stu-id="050e8-164">It is simpler tooapply hello Premium Storage recommended cache settings when you have separate VHDs for hello SQL Data files and log files (rather than a single VHD that contains both).</span></span>

> [!NOTE]
> <span data-ttu-id="050e8-165">SQL Server veri ve günlük dosyalarını hello g/ç erişimi desenleri veritabanı iş yükleri için aynı birimi seçeneği önbelleğe alma hello bağlıdır hello varsa.</span><span class="sxs-lookup"><span data-stu-id="050e8-165">If you have SQL Server data and log files on hello same volume, hello caching option you choose depends on hello IO access patterns for your database workloads.</span></span> <span data-ttu-id="050e8-166">Yalnızca test hangi önbelleğe alma bu senaryo için en iyi seçenektir personeline gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="050e8-166">Only testing can demonstrate which caching option is best for this scenario.</span></span>
>
>

<span data-ttu-id="050e8-167">Ancak, birden çok VHD toolook adresindeki gerekir hale Windows depolama alanları kullanıyorsanız VHD'ler eklenmiş özgün komut dosyaları tooidentify olan belirli hangi havuzda böylece, ardından hello önbellek ayarları ayarlayabilirsiniz uygun şekilde her disk için.</span><span class="sxs-lookup"><span data-stu-id="050e8-167">However, if you are using Windows Storage Spaces which are made up of multiple VHDs you will need toolook at your original scripts tooidentify which attached VHDs are in what specific pool, so you can then set hello cache settings accordingly for each disk.</span></span>

<span data-ttu-id="050e8-168">Özgün komut kullanılabilir tooshow yoksa hangi VHD'ler eşleme toohello depolama havuzu, aşağıdaki adımları toodetermine hello disk/depolama havuzu eşlemesini hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="050e8-168">If you do not have original script available tooshow you which VHDs map toohello storage pool, you can use hello following steps toodetermine hello disk/storage pool mapping.</span></span>

<span data-ttu-id="050e8-169">Her disk için hello aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="050e8-169">For each disk, use hello following steps:</span></span>

1. <span data-ttu-id="050e8-170">Disklerin listesini alın bağlı hello ile tooVM **Get-AzureVM** komutu:</span><span class="sxs-lookup"><span data-stu-id="050e8-170">Get list of disks attached tooVM with hello **Get-AzureVM** command:</span></span>

    <span data-ttu-id="050e8-171">Get-AzureVM - ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span><span class="sxs-lookup"><span data-stu-id="050e8-171">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span></span>
2. <span data-ttu-id="050e8-172">Merhaba Diskname ve LUN unutmayın.</span><span class="sxs-lookup"><span data-stu-id="050e8-172">Note hello Diskname and LUN.</span></span>

    ![DisknameAndLUN][2]
3. <span data-ttu-id="050e8-174">Uzak Masaüstü hello VM başlatın.</span><span class="sxs-lookup"><span data-stu-id="050e8-174">Remote desktop into hello VM.</span></span> <span data-ttu-id="050e8-175">Çok Git**Bilgisayar Yönetimi** | **Aygıt Yöneticisi'ni** | **Disk sürücüleri**.</span><span class="sxs-lookup"><span data-stu-id="050e8-175">Then go too**Computer Management** | **Device Manager** | **Disk Drives**.</span></span> <span data-ttu-id="050e8-176">Her bir hello 'Microsoft sanal diskler' Hello özelliklerine bakmak</span><span class="sxs-lookup"><span data-stu-id="050e8-176">Look at hello properties of each of hello ‘Microsoft Virtual Disks’</span></span>

    ![VirtualDiskProperties][3]
4. <span data-ttu-id="050e8-178">Merhaba LUN sayısı burada hello VHD toohello VM eklerken belirttiğiniz bir başvuru toohello LUN sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="050e8-178">hello LUN number here is a reference toohello LUN number you specify when attaching hello VHD toohello VM.</span></span>
5. <span data-ttu-id="050e8-179">Toohello 'Microsoft sanal diski' Hello için Git **ayrıntıları** sekmesinde, ardından hello **özelliği** listesinde, çok Git**sürücü anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="050e8-179">For hello ‘Microsoft Virtual Disk’ go toohello **Details** tab, then in hello **Property** list, go too**Driver Key**.</span></span> <span data-ttu-id="050e8-180">Merhaba, **değeri**, Not hello **uzaklığı**, ekran aşağıdaki hello 0002 olduğu.</span><span class="sxs-lookup"><span data-stu-id="050e8-180">In hello **Value**, note hello **Offset**, which is 0002 in hello following screenshot.</span></span> <span data-ttu-id="050e8-181">Merhaba 0002 depolama havuzu başvuruları hello hello PhysicalDisk2 gösterir.</span><span class="sxs-lookup"><span data-stu-id="050e8-181">hello 0002 denotes hello PhysicalDisk2 that hello storage pool references.</span></span>

    ![VirtualDiskPropertyDetails][4]
6. <span data-ttu-id="050e8-183">Her depolama havuzu için disklerin hello çıkışı döküm ilişkili:</span><span class="sxs-lookup"><span data-stu-id="050e8-183">For each storage pool, dump out hello associated disks:</span></span>

    <span data-ttu-id="050e8-184">Get-StoragePool - FriendlyName AMS1pooldata | Get-PhysicalDisk</span><span class="sxs-lookup"><span data-stu-id="050e8-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span></span>

    ![GetStoragePool][5]

<span data-ttu-id="050e8-186">Kullanabileceğiniz artık bu bilgileri tooassociate VHD'ler tooPhysical diskleri depolama havuzları bağlı.</span><span class="sxs-lookup"><span data-stu-id="050e8-186">Now you can use this information tooassociate attached VHDs tooPhysical Disks in Storage Pools.</span></span>

<span data-ttu-id="050e8-187">VHD'ler tooPhysical diskleri depolama havuzları ayırmak ve Premium depolama hesabı tooa kopyalama eşledikten sonra bunları hello doğru önbellek ayarı ile ekleyin.</span><span class="sxs-lookup"><span data-stu-id="050e8-187">Once you have mapped VHDs tooPhysical Disks in Storage Pools you can then detach and copy them over tooa Premium Storage account, then attach them with hello correct cache setting.</span></span> <span data-ttu-id="050e8-188">Lütfen hello hello örnekte bkz [ek](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), 8-12 arası adımları.</span><span class="sxs-lookup"><span data-stu-id="050e8-188">Please see hello example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), steps 8 through 12.</span></span> <span data-ttu-id="050e8-189">Bu adımları nasıl tooextract bir VM ekli VHD disk yapılandırma tooa CSV dosyası hello VHD'ler kopyalayın, hello disk yapılandırma önbelleği ayarlarını değiştirme ve tüm hello ile DS serisi VM diskleri bağlı olarak hello VM son olarak dağıtmanız gösterir.</span><span class="sxs-lookup"><span data-stu-id="050e8-189">These steps show how tooextract a VM-attached VHD disk configuration tooa CSV file, copy hello VHDs, alter hello disk configuration cache settings, and finally redeploy hello VM as a DS series VM with all hello attached disks.</span></span>

### <a name="vm-storage-bandwidth-and-vhd-storage-throughput"></a><span data-ttu-id="050e8-190">VM depolama bant genişliği ve VHD depolama üretilen iş</span><span class="sxs-lookup"><span data-stu-id="050e8-190">VM storage bandwidth and VHD storage throughput</span></span>
<span data-ttu-id="050e8-191">DS * VM boyutu belirtildi ve VHD boyutları hello hello üzerinde Hello depolama performansı bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="050e8-191">hello amount of storage performance depends on hello DS* VM size specified and hello VHD sizes.</span></span> <span data-ttu-id="050e8-192">Merhaba VM'ler eklenebilecek ve en yüksek bant genişliği (MB/sn) destekleyecek hello VHD'ler hello sayısı için farklı kesintileri vardır.</span><span class="sxs-lookup"><span data-stu-id="050e8-192">hello VMs have different allowances for hello number of VHDs that can be attached and hello maximum bandwidth they will support (MB/s).</span></span> <span data-ttu-id="050e8-193">Merhaba belirli bir bant numaraları için bkz: [sanal makine ve bulut hizmeti boyutları Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="050e8-193">For hello specific bandwidth numbers, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="050e8-194">Daha fazla IOPS ile büyük disk boyutları elde edilir.</span><span class="sxs-lookup"><span data-stu-id="050e8-194">Increased IOPS are achieved with larger disk sizes.</span></span> <span data-ttu-id="050e8-195">Geçiş yolunuz hakkında düşünürken, düşünmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="050e8-195">You should consider this when you think about your migration path.</span></span> <span data-ttu-id="050e8-196">Ayrıntılar için [IOPS ve Disk türleri için bkz: hello tablosu](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="050e8-196">For details, [see hello table for IOPS and Disk Types](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span></span>

<span data-ttu-id="050e8-197">Son olarak, VM'ye bağlı tüm diskler için destekleyecek farklı en fazla disk bant genişlikleri sahip göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="050e8-197">Finally, consider that VMs have different maximum disk bandwidths they will support for all disks attached.</span></span> <span data-ttu-id="050e8-198">Yüksek yük altında hello en fazla disk kullanılabilir bant genişliği bu VM rol boyutu için saturate.</span><span class="sxs-lookup"><span data-stu-id="050e8-198">Under high load, you could saturate hello maximum disk bandwidth available for that VM role size.</span></span> <span data-ttu-id="050e8-199">Örneğin bir Standard_DS14 too512MB/s destekler; Bu nedenle, üç P30 disklerle hello disk bant genişliği hello VM saturate.</span><span class="sxs-lookup"><span data-stu-id="050e8-199">For example a Standard_DS14 will support up too512MB/s; therefore, with three P30 disks you could saturate hello disk bandwidth of hello VM.</span></span> <span data-ttu-id="050e8-200">Ancak bu örnekte, hello üretilen iş sınırı hello karışımını okuma ve yazma g/ç işlemine bağlı olarak aştı.</span><span class="sxs-lookup"><span data-stu-id="050e8-200">But in this example, hello throughput limit could be exceeded depending on hello mix of read and write IOs.</span></span>

## <a name="new-deployments"></a><span data-ttu-id="050e8-201">Yeni dağıtımlar</span><span class="sxs-lookup"><span data-stu-id="050e8-201">New deployments</span></span>
<span data-ttu-id="050e8-202">SQL Server Vm'lerinin tooPremium depolama nasıl dağıtabileceğiniz Hello sonraki iki bölümde gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="050e8-202">hello next two sections demonstrate how you can deploy SQL Server VMs tooPremium Storage.</span></span> <span data-ttu-id="050e8-203">Önceden belirtildiği gibi Premium depolama üzerine tooplace hello işletim sistemi diski mutlaka gerekmez.</span><span class="sxs-lookup"><span data-stu-id="050e8-203">As mentioned before, you do not necessarily need tooplace hello OS disk onto Premium storage.</span></span> <span data-ttu-id="050e8-204">Tooplace OS VHD hello üzerinde hiçbir yoğun g/ç iş yükleri amaçlanıyorsa, bu toodo seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="050e8-204">You might choose toodo this if you are intending tooplace any intensive IO workloads on hello OS VHD.</span></span>

<span data-ttu-id="050e8-205">var olan Azure galeri görüntüleri kullanılarak Merhaba ilk örneği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="050e8-205">hello first example demonstrates utilizing existing Azure Gallery Images.</span></span> <span data-ttu-id="050e8-206">Merhaba ikinci örnek nasıl toouse özel bir VM görüntüsü, gösterir var olan bir standart depolama hesabına sahip.</span><span class="sxs-lookup"><span data-stu-id="050e8-206">hello second example shows how toouse a custom VM image that you have in an existing Standard storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="050e8-207">Bu örnekler, bölgesel bir sanal ağ zaten oluşturduğunuzu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="050e8-207">These examples assume that you have already created a Regional VNET.</span></span>
>
>

### <a name="create-a-new-vm-with-premium-storage-with-gallery-image"></a><span data-ttu-id="050e8-208">Premium depolama galeri görüntüsü ile birlikte yeni bir VM oluşturun</span><span class="sxs-lookup"><span data-stu-id="050e8-208">Create a new VM with Premium Storage with Gallery Image</span></span>
<span data-ttu-id="050e8-209">Merhaba örnekte nasıl tooplace OS VHD premium depolama hello ve Premium depolama VHD'yi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="050e8-209">hello example below shows how tooplace hello OS VHD onto premium storage and attach Premium Storage VHDs.</span></span> <span data-ttu-id="050e8-210">Ancak, aynı zamanda bir standart depolama hesabında hello işletim sistemi diski yerleştirin ve ardından bir Premium depolama hesabında bulunan VHD ekleyin.</span><span class="sxs-lookup"><span data-stu-id="050e8-210">However, you can also place hello OS disk in a Standard Storage account and then attach VHDs that reside in a Premium Storage account.</span></span> <span data-ttu-id="050e8-211">Her iki senaryoyu gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="050e8-211">Both scenarios are demonstrated.</span></span>

    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Set up subscription
    Set-AzureSubscription -SubscriptionName $mysubscription
    Select-AzureSubscription -SubscriptionName $mysubscription -Current  

#### <a name="step-1-create-a-premium-storage-account"></a><span data-ttu-id="050e8-212">1. adım: bir Premium depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="050e8-212">Step 1: Create a Premium Storage Account</span></span>
    #Create Premium Storage account, note Type
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  


#### <a name="step-2-create-a-new-cloud-service"></a><span data-ttu-id="050e8-213">2. adım: yeni bir bulut hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="050e8-213">Step 2: Create a New Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-reserve-a-cloud-service-vip-optional"></a><span data-ttu-id="050e8-214">3. adım: (isteğe bağlı) bir bulut hizmeti VIP ayırma</span><span class="sxs-lookup"><span data-stu-id="050e8-214">Step 3: Reserve a Cloud Service VIP (Optional)</span></span>
    #check exisitng reserved VIP
    Get-AzureReservedIP

    $reservedVIPName = “sqlcloudVIP”
    New-AzureReservedIP –ReservedIPName $reservedVIPName –Label $reservedVIPName –Location $location

#### <a name="step-4-create-a-vm-container"></a><span data-ttu-id="050e8-215">4. adım: bir VM kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="050e8-215">Step 4: Create a VM Container</span></span>
    #Generate storage keys for later
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    ##Generate storage acc contexts
    $xioContext = New-AzureStorageContext –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary   

    #Create container
    $containerName = 'vhds'
    New-AzureStorageContainer -Name $containerName -Context $xioContext

#### <a name="step-5-placing-os-vhd-on-standard-or-premium-storage"></a><span data-ttu-id="050e8-216">5. adım: İşletim sistemi VHD standart veya Premium Storage yerleştirme</span><span class="sxs-lookup"><span data-stu-id="050e8-216">Step 5: Placing OS VHD on Standard or Premium Storage</span></span>
    #NOTE: Set up subscription and default storage account which will be used tooplace hello OS VHD in

    #If you want tooplace hello OS VHD Premium Storage Account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $newxiostorageaccountname  

    #If you wanted tooplace hello OS VHD Standard Storage Account but attach Premium Storage VHDs then you would run this instead:
    $standardstorageaccountname = "danstdams"

    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $standardstorageaccountname

#### <a name="step-6-create-vm"></a><span data-ttu-id="050e8-217">6. adım: VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="050e8-217">Step 6: Create VM</span></span>
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


### <a name="create-a-new-vm-toouse-premium-storage-with-a-custom-image"></a><span data-ttu-id="050e8-218">Yeni bir VM toouse Premium depolama ile özel bir görüntü oluşturun</span><span class="sxs-lookup"><span data-stu-id="050e8-218">Create a new VM toouse Premium Storage with a custom image</span></span>
<span data-ttu-id="050e8-219">Bu senaryo, bir standart depolama hesabında bulunan var olan özelleştirilmiş görüntüleri sahip olduğu gösterir.</span><span class="sxs-lookup"><span data-stu-id="050e8-219">This scenario demonstrates where you have existing customized images that reside in a Standard Storage account.</span></span> <span data-ttu-id="050e8-220">Tooplace hello OS VHD istiyorsanız belirtildiği gibi Premium toocopy gerekir depolama hello standart depolama hesabı mevcut görüntü hello ve kullanılabilmesi için önce bunları tooa Premium depolama aktarın.</span><span class="sxs-lookup"><span data-stu-id="050e8-220">As mentioned if you want tooplace hello OS VHD on Premium Storage you will need toocopy hello image that exists in hello Standard Storage account and transfer them tooa Premium Storage before it can be used.</span></span> <span data-ttu-id="050e8-221">Bir görüntü şirket içi, yapabilecekleriniz varsa bu yöntem toocopy de doğrudan toohello Premium depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="050e8-221">If you have an image on-premises, you can also use this method toocopy that directly toohello Premium Storage account.</span></span>

#### <a name="step-1-create-storage-account"></a><span data-ttu-id="050e8-222">Adım 1: Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="050e8-222">Step 1: Create Storage Account</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Standard Storage account
    $origstorageaccountname = "danstdams"

#### <a name="step-2-create-cloud-service"></a><span data-ttu-id="050e8-223">2. adım, bulut hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="050e8-223">Step 2 Create Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-use-existing-image"></a><span data-ttu-id="050e8-224">3. adım: Mevcut görüntü kullanın</span><span class="sxs-lookup"><span data-stu-id="050e8-224">Step 3: Use existing image</span></span>
<span data-ttu-id="050e8-225">Varolan bir görüntü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="050e8-225">You can use an existing image.</span></span> <span data-ttu-id="050e8-226">Veya, [var olan bir makine görüntüsünü ele](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="050e8-226">Or, you can [take an image of an existing machine](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="050e8-227">Not hello makine, görüntü toobe DS * makine yok.</span><span class="sxs-lookup"><span data-stu-id="050e8-227">Note hello machine you image does not have toobe DS* machine.</span></span> <span data-ttu-id="050e8-228">Merhaba görüntüsünü oluşturduktan sonra adımları Göster nasıl aşağıdaki hello toocopy onu toohello hello Premium Storage hesabıyla **başlangıç AzureStorageBlobCopy** PowerShell komutunu.</span><span class="sxs-lookup"><span data-stu-id="050e8-228">Once you have hello image, hello following steps show how toocopy it toohello Premium Storage account with hello **Start-AzureStorageBlobCopy** PowerShell commandlet.</span></span>

    #Get storage account keys:
    #Standard Storage account
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    #Premium Storage account
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Set up contexts for hello storage accounts:
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $destContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

#### <a name="step-4-copy-blob-between-storage-accounts"></a><span data-ttu-id="050e8-229">4. adım: Kopyalama Blob Depolama hesapları arasında</span><span class="sxs-lookup"><span data-stu-id="050e8-229">Step 4: Copy Blob between Storage Accounts</span></span>
    #Get Image VHD
    $myImageVHD = "dansoldonorsql2k14-os-2015-04-15.vhd"
    $containerName = 'vhds'

    #Copy Blob between accounts
    $blob = Start-AzureStorageBlobCopy -SrcBlob $myImageVHD -SrcContainer $containerName `
    -DestContainer vhds -Destblob "prem-$myImageVHD" `
    -Context $origContext -DestContext $destContext  

#### <a name="step-5-regularly-check-copy-status"></a><span data-ttu-id="050e8-230">5. adım: Kopyalama durumu düzenli olarak kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="050e8-230">Step 5: Regularly check copy status:</span></span>
    $blob | Get-AzureStorageBlobCopyState

#### <a name="step-6-add-image-disk-tooazure-disk-repository-in-subscription"></a><span data-ttu-id="050e8-231">6. adım: Resim disk tooAzure disk deposu abonelikte ekleyin.</span><span class="sxs-lookup"><span data-stu-id="050e8-231">Step 6: Add Image disk tooAzure disk Repository in Subscription</span></span>
    $imageMediaLocation = $destContext.BlobEndPoint+"/"+$myImageVHD
    $newimageName = "prem"+"dansoldonorsql2k14"

    Add-AzureVMImage -ImageName $newimageName -MediaLocation $imageMediaLocation

> [!NOTE]
> <span data-ttu-id="050e8-232">Merhaba durumu başarılı raporları olsa da, bir disk kira hatası hala alabilir bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="050e8-232">You may find that even though hello status reports as success, you could still get a disk lease error.</span></span> <span data-ttu-id="050e8-233">Bu durumda, yaklaşık 10 dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="050e8-233">In this case, wait about 10 minutes.</span></span>
>
>

#### <a name="step-7--build-hello-vm"></a><span data-ttu-id="050e8-234">7. adım: hello VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="050e8-234">Step 7:  Build hello VM</span></span>
<span data-ttu-id="050e8-235">Burada görüntünüzü ve iki Premium depolama VHD'leri hello VM oluşturuyorsanız:</span><span class="sxs-lookup"><span data-stu-id="050e8-235">Here you are building hello VM from your image and attaching two Premium Storage VHDs:</span></span>

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

## <a name="existing-deployments-that-do-not-use-always-on-availability-groups"></a><span data-ttu-id="050e8-236">Always On kullanılabilirlik grupları kullanmayın var olan dağıtımlar</span><span class="sxs-lookup"><span data-stu-id="050e8-236">Existing deployments that do not use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="050e8-237">Var olan dağıtımlar için öncelikle hello görmek [Önkoşullar](#prerequisites-for-premium-storage) bölümüne.</span><span class="sxs-lookup"><span data-stu-id="050e8-237">For existing deployments, first see hello [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="050e8-238">Always On kullanılabilirlik grupları hem de kullanmayın SQL Server dağıtımları için farklı noktalar vardır.</span><span class="sxs-lookup"><span data-stu-id="050e8-238">There are different considerations for SQL Server deployments that do not use Always On Availability Groups and those that do.</span></span> <span data-ttu-id="050e8-239">Her zaman açık kullanmıyorsanız ve var olan bir tek başına SQL Server yüklüyse, yeni bir bulut hizmeti ve depolama hesabı kullanarak tooPremium depolama yükseltebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="050e8-239">If you are not using Always On and have an existing standalone SQL Server, you can upgrade tooPremium Storage by using a new cloud service and storage account.</span></span> <span data-ttu-id="050e8-240">Seçenekler aşağıdaki hello göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="050e8-240">Consider hello following options:</span></span>

* <span data-ttu-id="050e8-241">**Yeni bir SQL Server VM oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="050e8-241">**Create a new SQL Server VM**.</span></span> <span data-ttu-id="050e8-242">Yeni dağıtımlarda belirtildiği gibi yeni bir SQL Server bir Premium depolama hesabını kullanan VM oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="050e8-242">You can create a new SQL Server VM that uses a Premium Storage account, as documented in New Deployments.</span></span> <span data-ttu-id="050e8-243">Ardından yedekleme ve SQL Server yapılandırma ve kullanıcı veritabanlarını geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="050e8-243">Then backup and restore your SQL Server configuration and user databases.</span></span> <span data-ttu-id="050e8-244">Merhaba uygulama güncelleştirilmiş toobe gerekir tooreference hello yeni SQL Server dahili veya harici erişiliyor durumunda.</span><span class="sxs-lookup"><span data-stu-id="050e8-244">hello application will need toobe updated tooreference hello new SQL Server if it is being accessed internally or externally.</span></span> <span data-ttu-id="050e8-245">Yan yana (SxS) SQL Server Geçiş yaptığınız gibi 'dışı db' tüm nesneleri toocopy gerekir.</span><span class="sxs-lookup"><span data-stu-id="050e8-245">You would need toocopy all ‘out of db’ objects as if you were doing a Side by Side (SxS) SQL Server migration.</span></span> <span data-ttu-id="050e8-246">Bu, oturum açma bilgileri, sertifikalar ve bağlantılı sunucular gibi nesneleri içerir.</span><span class="sxs-lookup"><span data-stu-id="050e8-246">This includes objects such as logins, certificates, and linked servers.</span></span>
* <span data-ttu-id="050e8-247">**Mevcut bir SQL Server VM'yi geçirme**.</span><span class="sxs-lookup"><span data-stu-id="050e8-247">**Migrate an existing SQL Server VM**.</span></span> <span data-ttu-id="050e8-248">Bu SQL Server VM hello çevrimdışı duruma getirmeden sonra tüm bağlı kendi VHD'ler toohello Premium depolama hesabı kopyalama içeren tooa yeni bulut hizmeti, aktarma gerektirir.</span><span class="sxs-lookup"><span data-stu-id="050e8-248">This will require taking hello SQL Server VM offline, then transferring it tooa new cloud service, which includes copying all of its attached VHDs toohello Premium Storage account.</span></span> <span data-ttu-id="050e8-249">Merhaba VM çevrimiçi olduğunda Merhaba uygulaması Itanium tabanlı sistemler için hello sunucu ana bilgisayar adı olarak önce başvurur.</span><span class="sxs-lookup"><span data-stu-id="050e8-249">When hello VM comes online, hello application will reference hello server host name as before.</span></span> <span data-ttu-id="050e8-250">Merhaba hello mevcut disk boyutunu hello performans özellikleri etkiler unutmayın.</span><span class="sxs-lookup"><span data-stu-id="050e8-250">Be aware that hello size of hello existing disk will affect hello performance characteristics.</span></span> <span data-ttu-id="050e8-251">Örneğin, 400 GB disk P20 tooa yuvarlanmasını.</span><span class="sxs-lookup"><span data-stu-id="050e8-251">For example, a 400 GB disk gets rounded up tooa P20.</span></span> <span data-ttu-id="050e8-252">Hello VM DS serisi VM olarak yeniden oluşturun ve Premium depolama VHD'yi ihtiyaç duyduğunuz hello boyutu/performans belirtimi, bu disk performansı gerektirmez biliyorsanız.</span><span class="sxs-lookup"><span data-stu-id="050e8-252">If you know that you do not require that disk performance, then you could recreate hello VM as a DS Series VM, and attach Premium Storage VHDs of hello size/performance specification you require.</span></span> <span data-ttu-id="050e8-253">Ardından detach ve hello SQL DB dosyaları yeniden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="050e8-253">Then you could detach and reattach hello SQL DB files.</span></span>

> [!NOTE]
> <span data-ttu-id="050e8-254">Hello boyutuna bağlı olarak hello boyutu bilincinde olmanız gereken hello VHD diskleri kopyalama Premium depolama diskini türüne anlamına gelir, bunların içine kalan, bu disk performans belirtimi belirler.</span><span class="sxs-lookup"><span data-stu-id="050e8-254">When copying hello VHD disks you should be aware of hello size, depending on hello size will mean what Premium Storage Disk type they fall into, this determines disk performance specification.</span></span> <span data-ttu-id="050e8-255">Disk en yakın toohello yukarı yuvarlayın Azure boyutu, 400 GB disk varsa, bu P20 tooa yuvarlanacağı şekilde.</span><span class="sxs-lookup"><span data-stu-id="050e8-255">Azure will round up toohello nearest disk size, so if you have a 400GB disk, this will be rounded up tooa P20.</span></span> <span data-ttu-id="050e8-256">Varolan g/ç gereksinimleri hello OS VHD bağlı olarak, size toomigrate bu tooa Premium depolama hesabı gerekmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="050e8-256">Depending on your existing IO requirements of hello OS VHD, you might not need toomigrate this tooa Premium Storage account.</span></span>
>
>

<span data-ttu-id="050e8-257">SQL Server'ınızdaki dışarıdan erişiliyorsa hello bulut hizmeti VIP değiştirir.</span><span class="sxs-lookup"><span data-stu-id="050e8-257">If your SQL Server is accessed externally, then hello cloud service VIP will change.</span></span> <span data-ttu-id="050e8-258">Tooupdate uç noktaları, ACL'ler ve DNS sahip olur ayarlar.</span><span class="sxs-lookup"><span data-stu-id="050e8-258">You will also have tooupdate end points, ACLs, and DNS settings.</span></span>

## <a name="existing-deployments-that-use-always-on-availability-groups"></a><span data-ttu-id="050e8-259">Always On kullanılabilirlik grupları kullanan var olan dağıtımlar</span><span class="sxs-lookup"><span data-stu-id="050e8-259">Existing deployments that use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="050e8-260">Var olan dağıtımlar için öncelikle hello görmek [Önkoşullar](#prerequisites-for-premium-storage) bölümüne.</span><span class="sxs-lookup"><span data-stu-id="050e8-260">For existing deployments, first see hello [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="050e8-261">Başlangıçta bu bölümde biz nasıl her zaman açık Azure ağ ile etkileşim sırasında arar.</span><span class="sxs-lookup"><span data-stu-id="050e8-261">Initially in this section we will look at how Always On interacts with Azure Networking.</span></span> <span data-ttu-id="050e8-262">Biz sonra geçişleri tootwo senaryolarda aşağı çalışmamasına neden olur: Burada miktar kapalı kalma süresi izin geçişler ve burada gerekir ulaşmanıza en düşük kapalı kalma geçişleri.</span><span class="sxs-lookup"><span data-stu-id="050e8-262">We will then break down migrations in tootwo scenarios: migrations where some downtime can be tolerated and migrations where you must achieve minimal downtime.</span></span>

<span data-ttu-id="050e8-263">Bir dinleyici sanal bir DNS adı bir veya daha fazla SQL Server'lar arasında paylaşılan bir IP adresi ile birlikte kaydeden şirket içi SQL Server Always On kullanılabilirlik grupları kullanın.</span><span class="sxs-lookup"><span data-stu-id="050e8-263">On-premises SQL Server Always On Availability Groups use a Listener on-premises that registers a virtual DNS name along with an IP address that is shared between one or more SQL Servers.</span></span> <span data-ttu-id="050e8-264">İstemciler bağlandığında bunlar hello dinleyici IP toohello birincil SQL Server yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="050e8-264">When clients connect they are routed through hello listener IP toohello Primary SQL Server.</span></span> <span data-ttu-id="050e8-265">Bu, o anda hello üzerinde her zaman IP kaynağı sahip hello sunucusudur.</span><span class="sxs-lookup"><span data-stu-id="050e8-265">This is hello server that owns hello Always On IP resource at that time.</span></span>

![Üzerinde DeploymentsUseAlways][6]

<span data-ttu-id="050e8-267">Microsoft Azure'da hello VM üzerinde tek bir IP adresi atanmış tooa NIC bu nedenle, sipariş tooachieve Merhaba aynı şirket içi olarak Soyutlama Katmanı, Azure toohello iç/dış yük dengeleyici (ILB/ELB) atanan başlangıç IP adresi kullanan olabilir.</span><span class="sxs-lookup"><span data-stu-id="050e8-267">In Microsoft Azure you can have only one IP address assigned tooa NIC on hello VM, so in order tooachieve hello same layer of abstraction as on-premises, Azure utilizes hello IP address that is assigned toohello Internal/External Load Balancers (ILB/ELB).</span></span> <span data-ttu-id="050e8-268">Merhaba sunucular arasında paylaşılan hello IP kaynağı toohello ayarlanmış aynı IP hello ILB/ELB olarak.</span><span class="sxs-lookup"><span data-stu-id="050e8-268">hello IP resource that is shared between hello servers is set toohello same IP as hello ILB/ELB.</span></span> <span data-ttu-id="050e8-269">Bu hello DNS yayınlanırsa ve istemci trafiğini hello ILB/ELB toohello birincil SQL Server çoğaltma ile aktarılır.</span><span class="sxs-lookup"><span data-stu-id="050e8-269">This is published in hello DNS, and client traffic is passed through hello ILB/ELB toohello Primary SQL Server replica.</span></span> <span data-ttu-id="050e8-270">Merhaba ILB/ELB araştırmalar tooprobe hello üzerinde her zaman IP kaynağı kullandığından SQL sunucusu olan birincil bilir.</span><span class="sxs-lookup"><span data-stu-id="050e8-270">hello ILB/ELB knows which SQL Server is primary since it uses probes tooprobe hello Always On IP resource.</span></span> <span data-ttu-id="050e8-271">Merhaba önceki örnekte ELB/ILB hello tarafından başvurulan bir uç nokta sahip her bir düğüm araştırmaları, hangisi yanıt birincil SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="050e8-271">In hello previous example, it probes each node that has an endpoint referenced by hello ELB/ILB, whichever responds is hello Primary SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="050e8-272">Merhaba ILB ve ELB her ikisi de tooa belirli Azure bulut hizmeti atanır, bu nedenle tüm Azure bulut geçişte büyük olasılıkla yük dengeleyici IP değiştirecek bu hello anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="050e8-272">hello ILB and ELB are both assigned tooa particular Azure cloud service, therefore any cloud migration in Azure will most likely mean that hello Load Balancer IP will change.</span></span>
>
>

### <a name="migrating-always-on-deployments-that-can-allow-some-downtime"></a><span data-ttu-id="050e8-273">Miktar kapalı kalma süresi sağlayan geçirme her zaman açık dağıtımları</span><span class="sxs-lookup"><span data-stu-id="050e8-273">Migrating Always On deployments that can allow some downtime</span></span>
<span data-ttu-id="050e8-274">Bazı kesintiler izin toomigrate her zaman açık dağıtımlar iki strateji vardır:</span><span class="sxs-lookup"><span data-stu-id="050e8-274">There are two strategies toomigrate Always On deployments that allow for some downtime:</span></span>

1. <span data-ttu-id="050e8-275">**Daha fazla ikincil çoğaltmaları tooan üzerinde her zaman küme varolan Ekle**</span><span class="sxs-lookup"><span data-stu-id="050e8-275">**Add more secondary replicas tooan existing Always On Cluster**</span></span>
2. <span data-ttu-id="050e8-276">**Tooa geçirmek yeni her zaman üzerinde Küme**</span><span class="sxs-lookup"><span data-stu-id="050e8-276">**Migrate tooa new Always On Cluster**</span></span>

#### <a name="1-add-more-secondary-replicas-tooan-existing-always-on-cluster"></a><span data-ttu-id="050e8-277">1. Daha fazla ikincil çoğaltmaları tooan ekleme varolan her zaman üzerinde Küme</span><span class="sxs-lookup"><span data-stu-id="050e8-277">1. Add more Secondary Replicas tooan Existing Always On Cluster</span></span>
<span data-ttu-id="050e8-278">Bir strateji tooadd daha fazla ikincil kopya toohello her zaman üzerindeki kullanılabilirlik grubu değil.</span><span class="sxs-lookup"><span data-stu-id="050e8-278">One strategy is tooadd more secondaries toohello Always On Availability Group.</span></span> <span data-ttu-id="050e8-279">Merhaba dinleyicisi hello Yeni Yük Dengeleyici IP ile güncelleştirin ve bunları yeni bir bulut hizmeti tooadd gerekir.</span><span class="sxs-lookup"><span data-stu-id="050e8-279">You need tooadd these into a new cloud service and update hello listener with hello new load balancer IP.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="050e8-280">Kapalı kalma süresi noktalar:</span><span class="sxs-lookup"><span data-stu-id="050e8-280">Points of downtime:</span></span>
* <span data-ttu-id="050e8-281">Küme doğrulama.</span><span class="sxs-lookup"><span data-stu-id="050e8-281">Cluster Validation.</span></span>
* <span data-ttu-id="050e8-282">Her zaman açık yük test etme için yeni ikincil öğe.</span><span class="sxs-lookup"><span data-stu-id="050e8-282">Testing Always On failovers for New Secondaries.</span></span>

<span data-ttu-id="050e8-283">Windows depolama havuzları için daha yüksek g/ç işleme hello VM içinde kullanıyorsanız, ardından bu tam bir küme doğrulama sırasında çevrimdışına alınır.</span><span class="sxs-lookup"><span data-stu-id="050e8-283">If you are using Windows Storage Pools within hello VM for higher IO throughput, then these will be taken offline during a Full Cluster Validation.</span></span> <span data-ttu-id="050e8-284">düğümleri toohello küme eklediğinizde hello doğrulama testi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="050e8-284">hello validation test is required when you add nodes toohello cluster.</span></span> <span data-ttu-id="050e8-285">Bu ne kadar bu devam, yaklaşık bir saat, temsili test ortamı tooget sınamalısınız şekilde hello süresini toorun hello test farklılık gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="050e8-285">hello time it takes toorun hello test can vary, so you should test this in your representative test environment tooget an approximate time of how long this will take.</span></span>

<span data-ttu-id="050e8-286">Burada el ile yük devretme gerçekleştirebilirsiniz ve beklendiği gibi hello üzerinde yeni test chaos eklenen düğümleri tooensure her zaman üzerinde yüksek kullanılabilirlik işlevleri zaman hazırlamanız.</span><span class="sxs-lookup"><span data-stu-id="050e8-286">You should provision time where you can perform manual failover and chaos testing on hello newly added nodes tooensure Always On High Availability functions as expected.</span></span>

![DeploymentUseAlways On2][7]

> [!NOTE]
> <span data-ttu-id="050e8-288">Merhaba doğrulama çalışmadan önce hello depolama havuzları kullanıldığı SQL Server'ın tüm örneklerini durdurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="050e8-288">You should stop all instances of SQL Server where hello Storage Pools are used before hello Validation runs.</span></span>
>
> ##### <a name="high-level-steps"></a><span data-ttu-id="050e8-289">Üst düzey adımlar</span><span class="sxs-lookup"><span data-stu-id="050e8-289">High-level steps</span></span>
>

1. <span data-ttu-id="050e8-290">İki yeni SQL sunucusuna bağlı Premium depolama ile yeni bulut hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="050e8-290">Create two new SQL Servers in new cloud service with attached Premium Storage.</span></span>
2. <span data-ttu-id="050e8-291">TAM yedeklemeler kopyalayın ve geri yükleme ile **NORECOVERY**.</span><span class="sxs-lookup"><span data-stu-id="050e8-291">Copy over FULL backups and restore with **NORECOVERY**.</span></span>
3. <span data-ttu-id="050e8-292">'Dışında kullanıcı DB' oturumları vb. gibi bağımlı nesnelere kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="050e8-292">Copy over ‘out of user DB’ dependent objects, such as logins etc.</span></span>
4. <span data-ttu-id="050e8-293">Yeni bir yeni iç yük dengeleyici'nı (ILB) oluşturun veya bir dış yük dengeleyici (ELB) kullanın ve ardından her iki yeni düğümde yük dengeli uç noktaları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="050e8-293">Create new a new Internal Load Balancer (ILB) or use an External Load Balancer (ELB), and then set up Load Balanced Endpoints on both new nodes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="050e8-294">Devam etmeden önce tüm düğümleri hello doğru uç nokta yapılandırması sahip denetleyin</span><span class="sxs-lookup"><span data-stu-id="050e8-294">Check all Nodes have hello correct Endpoint configuration before you continue</span></span>
   >
   >
5. <span data-ttu-id="050e8-295">Kullanıcı/uygulama erişimi toohello SQL Server (depolama havuzlarını kullanıyorsanız) durdurun.</span><span class="sxs-lookup"><span data-stu-id="050e8-295">Stop User/Application Access toohello SQL Server (if using Storage Pools).</span></span>
6. <span data-ttu-id="050e8-296">SQL Server motoru Hizmetleri tüm düğümler üzerinde (depolama havuzlarını kullanıyorsanız) durdurun.</span><span class="sxs-lookup"><span data-stu-id="050e8-296">Stop SQL Server Engine Services on All Nodes (if using Storage Pools).</span></span>
7. <span data-ttu-id="050e8-297">Yeni düğümler toocluster ekleyin ve tam doğrulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="050e8-297">Add new Nodes toocluster and run full validation.</span></span>
8. <span data-ttu-id="050e8-298">Doğrulama başarılı olduktan sonra tüm SQL Server hizmetlerini başlatın.</span><span class="sxs-lookup"><span data-stu-id="050e8-298">Once Validation is successful, start all SQL Server Services.</span></span>
9. <span data-ttu-id="050e8-299">İşlem günlüklerini yedekleme ve kullanıcı veritabanlarını geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="050e8-299">Backup Transaction logs, and restore user databases.</span></span>
10. <span data-ttu-id="050e8-300">Hello her zaman üzerindeki kullanılabilirlik grubu yeni düğümleri eklemek ve çoğaltma içine yerleştirin **zaman uyumlu**.</span><span class="sxs-lookup"><span data-stu-id="050e8-300">Add new nodes into hello Always On Availability Group and place replication into **Synchronous**.</span></span>
11. <span data-ttu-id="050e8-301">Merhaba IP Ekle hello adresi kaynağı yeni bulut hizmeti ILB/ELB her zaman açık için PowerShell aracılığıyla hello çok siteli hello örnekte temel [ek](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="050e8-301">Add hello IP address resource of hello new Cloud Service ILB/ELB through PowerShell for Always On based on hello Multi-site example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span> <span data-ttu-id="050e8-302">Windows Kümelemesi içinde hello ayarlamak **olası sahipler** Merhaba, **IP adresi** kaynak toohello yeni düğümler eski.</span><span class="sxs-lookup"><span data-stu-id="050e8-302">In Windows clustering, set hello **Possible owners** of hello **IP Address** resource toohello new nodes old.</span></span> <span data-ttu-id="050e8-303">Merhaba Hello 'Aynı alt ağdaki IP adresi kaynağı ekleme' bölümüne bakın [ek](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="050e8-303">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
12. <span data-ttu-id="050e8-304">Yük devretme tooone hello yeni düğüm.</span><span class="sxs-lookup"><span data-stu-id="050e8-304">Failover tooone of hello new nodes.</span></span>
13. <span data-ttu-id="050e8-305">Yeni düğümler otomatik yük devretme ortakları Hello yapın ve test yük devretmeleri.</span><span class="sxs-lookup"><span data-stu-id="050e8-305">Make hello new nodes Auto Failover Partners and test failovers.</span></span>
14. <span data-ttu-id="050e8-306">Özgün düğüm kullanılabilirlik grubundan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="050e8-306">Remove original nodes from Availability Group.</span></span>

##### <a name="advantages"></a><span data-ttu-id="050e8-307">Avantajları</span><span class="sxs-lookup"><span data-stu-id="050e8-307">Advantages</span></span>
* <span data-ttu-id="050e8-308">Yeni SQL sunucuları olabilir (SQL Server ve uygulama) üzerinde tooAlways eklenmeden önce test.</span><span class="sxs-lookup"><span data-stu-id="050e8-308">New SQL Servers can be tested (SQL Server and Application) before they are added tooAlways On.</span></span>
* <span data-ttu-id="050e8-309">Merhaba VM boyutunu değiştirmek ve hello depolama tooyour tam gereksinimleri özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="050e8-309">You can change hello VM size and customize hello storage tooyour exact requirements.</span></span> <span data-ttu-id="050e8-310">Ancak, yararlı tookeep olacaktır tüm hello SQL dosya yolları aynı hello.</span><span class="sxs-lookup"><span data-stu-id="050e8-310">However, it would be beneficial tookeep all hello SQL file paths hello same.</span></span>
* <span data-ttu-id="050e8-311">Merhaba DB yedeklemeleri toohello ikincil çoğaltmaları hello aktarımını başladığında kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="050e8-311">You can control when hello transfer of hello DB backups toohello Secondary Replicas are started.</span></span> <span data-ttu-id="050e8-312">Bu Azure kullanmaktan farklıdır **başlangıç AzureStorageBlobCopy** komutunu toocopy VHD'ler, zaman uyumsuz bir kopya olduğundan.</span><span class="sxs-lookup"><span data-stu-id="050e8-312">This differs from using Azure **Start-AzureStorageBlobCopy** commandlet toocopy VHDs, because that is an asynchronous copy.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="050e8-313">Olumsuz yönleri</span><span class="sxs-lookup"><span data-stu-id="050e8-313">Disadvantages</span></span>
* <span data-ttu-id="050e8-314">Windows depolama havuzlarını kullanırken var. küme kapalı kalma süresi hello yeni ek düğüm için hello tam küme doğrulama sırasında</span><span class="sxs-lookup"><span data-stu-id="050e8-314">When using Windows Storage Pools, there is Cluster downtime during hello Full Cluster Validation for hello new additional nodes.</span></span>
* <span data-ttu-id="050e8-315">Merhaba SQL Server sürümü ve hello varolan ikincil çoğaltmaların sayısı bağlı olarak, olabilirsiniz varolan ikinciller kaldırma olmadan daha fazla ikincil çoğaltmaları mümkün tooadd olabilir.</span><span class="sxs-lookup"><span data-stu-id="050e8-315">Depending on hello SQL Server Version and hello existing number of secondary replicas, you might not be able tooadd more secondary replicas without removing existing secondaries.</span></span>
* <span data-ttu-id="050e8-316">Merhaba ikinciller ayarı uzun SQL veri aktarımı zamandan olabilir.</span><span class="sxs-lookup"><span data-stu-id="050e8-316">There could be long SQL data transfer time while setting up hello secondaries.</span></span>
* <span data-ttu-id="050e8-317">Yoktur ek maliyet geçiş sırasında paralel olarak çalışan yeni makineler varken.</span><span class="sxs-lookup"><span data-stu-id="050e8-317">There is additional cost during migration while you have new machines running in parallel.</span></span>

#### <a name="2-migrate-tooa-new-always-on-cluster"></a><span data-ttu-id="050e8-318">2. Tooa geçirmek yeni her zaman üzerinde Küme</span><span class="sxs-lookup"><span data-stu-id="050e8-318">2. Migrate tooa new Always On Cluster</span></span>
<span data-ttu-id="050e8-319">Başka bir toocreate yepyeni her zaman üzerinde Küme yepyeni düğümlerle yeni bulut hizmeti ve sonra yeniden yönlendirme hello istemcileri toouse stratejidir onu.</span><span class="sxs-lookup"><span data-stu-id="050e8-319">Another strategy is toocreate a brand new Always On Cluster with brand new nodes in new cloud service and then redirect hello clients toouse it.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="050e8-320">Kapalı kalma süresi noktaları</span><span class="sxs-lookup"><span data-stu-id="050e8-320">Points of downtime</span></span>
<span data-ttu-id="050e8-321">Uygulamaların ve kullanıcıların toohello yeni her zaman açık dinleyici aktardığınızda kapalı kalma süresi yok.</span><span class="sxs-lookup"><span data-stu-id="050e8-321">There is downtime when you transfer applications and users toohello new Always On listener.</span></span> <span data-ttu-id="050e8-322">Merhaba kapalı kalma süresi bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="050e8-322">hello downtime depends on:</span></span>

* <span data-ttu-id="050e8-323">yeni sunucularda toorestore son işlem günlüğü yedeklemeleri toodatabases geçen hello süre.</span><span class="sxs-lookup"><span data-stu-id="050e8-323">hello time taken toorestore final transaction log backups toodatabases on new servers.</span></span>
* <span data-ttu-id="050e8-324">Merhaba geçen süre tooupdate istemci uygulamaları toouse yeni her zaman açık dinleyici.</span><span class="sxs-lookup"><span data-stu-id="050e8-324">hello time taken tooupdate client applications toouse new Always On listener.</span></span>

##### <a name="advantages"></a><span data-ttu-id="050e8-325">Avantajları</span><span class="sxs-lookup"><span data-stu-id="050e8-325">Advantages</span></span>
* <span data-ttu-id="050e8-326">Merhaba gerçek üretim ortamında, SQL Server sınayabilirsiniz ve işletim sistemi derleme değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="050e8-326">You can test hello actual production environment, SQL Server, and OS build changes.</span></span>
* <span data-ttu-id="050e8-327">Merhaba seçeneği toocustomize hello depolama sahip ve toopotentially VM boyutunu azaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="050e8-327">You have hello option toocustomize hello storage and toopotentially reduce size of VM.</span></span> <span data-ttu-id="050e8-328">Bu maliyet azalmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="050e8-328">This could result in cost reduction.</span></span>
* <span data-ttu-id="050e8-329">Bu işlem sırasında SQL Server yapı veya sürüm güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="050e8-329">You can update your SQL Server build or version during this process.</span></span> <span data-ttu-id="050e8-330">Ayrıca hello işletim sistemi yükseltme yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="050e8-330">You can also upgrade hello Operating System.</span></span>
* <span data-ttu-id="050e8-331">Merhaba önceki her zaman üzerinde Küme düz geri alma hedef olarak davranamaz.</span><span class="sxs-lookup"><span data-stu-id="050e8-331">hello previous Always On Cluster can act as a solid rollback target.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="050e8-332">Olumsuz yönleri</span><span class="sxs-lookup"><span data-stu-id="050e8-332">Disadvantages</span></span>
* <span data-ttu-id="050e8-333">Eşzamanlı olarak çalıştıran her iki her zaman açık kümeler istiyorsanız hello dinleyici toochange hello DNS adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="050e8-333">You need toochange hello DNS name of hello listener if you want both Always On clusters running simultaneously.</span></span> <span data-ttu-id="050e8-334">Bu, istemci uygulama dizeleri hello yeni dinleyici adı yansıtmalıdır gibi yönetim ek yükü hello geçiş sırasında ekler.</span><span class="sxs-lookup"><span data-stu-id="050e8-334">This adds administration overhead during hello migration as client application strings must reflect hello new Listener name.</span></span>
* <span data-ttu-id="050e8-335">Eşitleme mekanizması olarak olası toominimize hello son eşitleme gereksinimleri geçişten önce yakın hello iki ortamları tookeep arasında uygulamalıdır.</span><span class="sxs-lookup"><span data-stu-id="050e8-335">You must implement a synchronization mechanism between hello two environments tookeep them as close as possible toominimize hello final synchronization requirements before migration.</span></span>
* <span data-ttu-id="050e8-336">Var. hello yeni ortam çalıştıran varken maliyet geçiş sırasında eklenir.</span><span class="sxs-lookup"><span data-stu-id="050e8-336">There is added cost during migration while you have hello new environment running.</span></span>

### <a name="migrating-always-on-deployments-for-minimal-downtime"></a><span data-ttu-id="050e8-337">Geçirme her zaman şirket dağıtımları için en az kapalı kalma süresi</span><span class="sxs-lookup"><span data-stu-id="050e8-337">Migrating Always On Deployments for minimal downtime</span></span>
<span data-ttu-id="050e8-338">En düşük kapalı kalma için her zaman açık geçirme dağıtımlar için iki strateji vardır:</span><span class="sxs-lookup"><span data-stu-id="050e8-338">There are two strategies for migrating Always On deployments for minimal downtime:</span></span>

1. <span data-ttu-id="050e8-339">**Var olan bir ikincil kullanma: tek siteli**</span><span class="sxs-lookup"><span data-stu-id="050e8-339">**Utilize an Existing Secondary: Single-Site**</span></span>
2. <span data-ttu-id="050e8-340">**Var olan ikincil çoğaltmalar kullanma: çok siteli**</span><span class="sxs-lookup"><span data-stu-id="050e8-340">**Utilize Existing Secondary Replica(s): Multi-Site**</span></span>

#### <a name="1-utilize-an-existing-secondary-single-site"></a><span data-ttu-id="050e8-341">1. Var olan bir ikincil kullanma: tek siteli</span><span class="sxs-lookup"><span data-stu-id="050e8-341">1. Utilize an existing secondary: Single-Site</span></span>
<span data-ttu-id="050e8-342">En az kapalı kalma süresi için bir strateji tootake ikincil mevcut bir buluta olan ve hello geçerli bulut hizmetinden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="050e8-342">One strategy for minimal downtime is tootake an existing cloud secondary and remove it from hello current cloud service.</span></span> <span data-ttu-id="050e8-343">Merhaba VHD'ler toohello yeni Premium depolama hesabı kopyalayın ve hello VM hello yeni bulut hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="050e8-343">Then copy hello VHDs toohello new Premium Storage account, and create hello VM in hello new cloud service.</span></span> <span data-ttu-id="050e8-344">Ardından Yük Devretme Kümelemesi ve dinleyicisinde hello güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="050e8-344">Then update hello listener in clustering and failover.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="050e8-345">Kapalı kalma süresi noktaları</span><span class="sxs-lookup"><span data-stu-id="050e8-345">Points of downtime</span></span>
* <span data-ttu-id="050e8-346">Merhaba yük dengeli uç noktasıyla hello son düğümü güncelleştirdiğinizde kapalı kalma süresi yok.</span><span class="sxs-lookup"><span data-stu-id="050e8-346">There is downtime when you update hello final node with hello Load Balanced endpoint.</span></span>
* <span data-ttu-id="050e8-347">İstemci/DNS yapılandırmanıza bağlı olarak, istemci yeniden bağlanmayı gecikebilir.</span><span class="sxs-lookup"><span data-stu-id="050e8-347">Your client reconnection might be delayed depending on your client/DNS configuration.</span></span>
* <span data-ttu-id="050e8-348">Tootake hello üzerinde her zaman küme grubu çevrimdışı tooswap hello IP adreslerini çıkışı seçerseniz ek kapalı kalma süresi yok.</span><span class="sxs-lookup"><span data-stu-id="050e8-348">There is additional downtime if you choose tootake hello Always On Cluster group offline tooswap out hello IP addresses.</span></span> <span data-ttu-id="050e8-349">Bu bir OR bağımlılığının kullanarak önlemek ve IP adresi kaynağı hello için olası sahipleri eklenir.</span><span class="sxs-lookup"><span data-stu-id="050e8-349">You can avoid this by using an OR dependency and Possible Owners for hello added IP Address resource.</span></span> <span data-ttu-id="050e8-350">Merhaba Hello 'Aynı alt ağdaki IP adresi kaynağı ekleme' bölümüne bakın [ek](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="050e8-350">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>

> [!NOTE]
> <span data-ttu-id="050e8-351">Bir her zaman üzerinde yük devretme ortağı olarak, eklenen düğümle toopartake hello istediğinizde tooadd Azure noktayla bir başvuru toohello yük dengeli kümesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="050e8-351">When you want hello added node toopartake in as an Always On Failover Partner, you need tooadd an Azure Endpoint with a reference toohello Load Balanced Set.</span></span> <span data-ttu-id="050e8-352">Merhaba çalıştırdığınızda **Ekle AzureEndpoint** toodo açık Bu, geçerli bağlantıları tooremain komutu, ancak yeni bağlantıları toohello dinleyicisi hello yük dengeleyici güncelleştirdi kadar kurulan mümkün toobe olmayacak.</span><span class="sxs-lookup"><span data-stu-id="050e8-352">When you run hello **Add-AzureEndpoint** command toodo this, current connections tooremain open, but new connections toohello listener will not be able toobe established until hello load balancer has updated.</span></span> <span data-ttu-id="050e8-353">Sınama sırasında görülen toolast 90-120seconds, bu, bu test edilmelidir.</span><span class="sxs-lookup"><span data-stu-id="050e8-353">In testing this was seen toolast 90-120seconds, this should be tested.</span></span>
>
>

##### <a name="advantages"></a><span data-ttu-id="050e8-354">Avantajları</span><span class="sxs-lookup"><span data-stu-id="050e8-354">Advantages</span></span>
* <span data-ttu-id="050e8-355">Hiçbir ek maliyet geçiş sırasında ücrete.</span><span class="sxs-lookup"><span data-stu-id="050e8-355">No extra cost incurred during migration.</span></span>
* <span data-ttu-id="050e8-356">Bire bir geçiş.</span><span class="sxs-lookup"><span data-stu-id="050e8-356">A one-to-one migration.</span></span>
* <span data-ttu-id="050e8-357">Azaltılan karmaşıklık.</span><span class="sxs-lookup"><span data-stu-id="050e8-357">Reduced complexity.</span></span>
* <span data-ttu-id="050e8-358">Premium depolama SKU'ları için daha yüksek IOPS sağlar.</span><span class="sxs-lookup"><span data-stu-id="050e8-358">Allows for increased IOPS from Premium Storage SKUs.</span></span> <span data-ttu-id="050e8-359">Aracı diskleri VM hello ayrılmış ve toohello yeni bulut hizmeti, kopyalanan hello bir 3. taraf daha yüksek kapatma sağlar kullanılan tooincrease hello VHD boyutu olabilir.</span><span class="sxs-lookup"><span data-stu-id="050e8-359">When hello disks are detached from hello VM and copied toohello new cloud service, a 3rd party tool can be used tooincrease hello VHD size, which provides higher throughputs.</span></span> <span data-ttu-id="050e8-360">VHD boyutları artırmak için bu bkz [forum tartışmasına](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span><span class="sxs-lookup"><span data-stu-id="050e8-360">For increasing VHD sizes, see this [forum discussion](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="050e8-361">Olumsuz yönleri</span><span class="sxs-lookup"><span data-stu-id="050e8-361">Disadvantages</span></span>
* <span data-ttu-id="050e8-362">Geçiş sırasında HA ve DR kaybı yoktur.</span><span class="sxs-lookup"><span data-stu-id="050e8-362">There is a temporary loss of HA and DR during migration.</span></span>
* <span data-ttu-id="050e8-363">1:1 geçiş olarak mümkün toodownsize olmayabilir böylece VHD'ler, sayısı, sanal makineleri destekleyecek en az bir VM boyutu toouse sahip olur.</span><span class="sxs-lookup"><span data-stu-id="050e8-363">As this is a 1:1 migration, you will have toouse a minimum VM size that will support your number of VHDs, so you might not be able toodownsize your VMs.</span></span>
* <span data-ttu-id="050e8-364">Bu senaryo hello Azure kullanırsınız **başlangıç AzureStorageBlobCopy** zaman uyumsuz komutunu.</span><span class="sxs-lookup"><span data-stu-id="050e8-364">This scenario would use hello Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="050e8-365">Kopya tamamlanma hiçbir SLA yoktur.</span><span class="sxs-lookup"><span data-stu-id="050e8-365">There is no SLA on copy completion.</span></span> <span data-ttu-id="050e8-366">Bu veri tootransfer hello miktarına bağlıdır sırasındaki bekleme bağlıdır sırada hello kopyaları hello süresi olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="050e8-366">hello time of hello copies varies, while this depends on wait in queue it will also depend on hello amount of data tootransfer.</span></span> <span data-ttu-id="050e8-367">başka bir bölgede Premium Storage destekleyen Azure veri merkezine tooanother Hello aktarımı edecekse hello kopyalama süresini artırır.</span><span class="sxs-lookup"><span data-stu-id="050e8-367">hello copy time increases if hello transfer is going tooanother Azure data center that supports Premium Storage in another region.</span></span> <span data-ttu-id="050e8-368">2 düğümleri varsa, olası azaltma hello kopyalama testinde uzun sürdüğünde durumda göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="050e8-368">If you just have 2 nodes, consider a possible mitigation in case hello copy takes longer than in testing.</span></span> <span data-ttu-id="050e8-369">Bu fikir aşağıdaki hello içerebilir.</span><span class="sxs-lookup"><span data-stu-id="050e8-369">This could include hello following ideas.</span></span>
  * <span data-ttu-id="050e8-370">Bir geçici 3 SQL Server düğümü HA için üzerinde anlaşılan kapalı kalma süresi ile Merhaba geçişten önce ekleyin.</span><span class="sxs-lookup"><span data-stu-id="050e8-370">Add a temporary 3rd SQL Server node for HA before hello migration with agreed downtime.</span></span>
  * <span data-ttu-id="050e8-371">Azure zamanlanmış bakım dışında Hello geçiş çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="050e8-371">Run hello migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="050e8-372">Küme çekirdeğini doğru yapılandırılmış olun.</span><span class="sxs-lookup"><span data-stu-id="050e8-372">Ensure you have configured your cluster quorum correctly.</span></span>  

##### <a name="high-level-steps"></a><span data-ttu-id="050e8-373">Üst düzey adımlar</span><span class="sxs-lookup"><span data-stu-id="050e8-373">High-level steps</span></span>
<span data-ttu-id="050e8-374">Bu belge tam son tooend örnek gösterilmemiştir ancak hello [ek](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) bu çevrelerini tooperform olabilir ayrıntıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="050e8-374">This document does not demonstrate a complete end tooend example, however hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) provides details that can be leveraged tooperform this.</span></span>

![MinimalDowntime][8]

* <span data-ttu-id="050e8-376">Toplama disk yapılandırma ve kaldırma hello düğümü (ekli VHD'ler silmeyin).</span><span class="sxs-lookup"><span data-stu-id="050e8-376">Gather disk configuration, and remove hello node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="050e8-377">Premium depolama hesabı oluşturma ve standart depolama hesabı hello VHD'ler kopyalayın</span><span class="sxs-lookup"><span data-stu-id="050e8-377">Create a Premium Storage account and copy VHDs from hello Standard Storage account</span></span>
* <span data-ttu-id="050e8-378">Yeni bulut hizmeti oluşturun ve bu bulut Hizmeti'nde hello SQL2 VM yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="050e8-378">Create new cloud service and redeploy hello SQL2 VM in that cloud service.</span></span> <span data-ttu-id="050e8-379">Merhaba VM oluşturma hello kullanarak özgün işletim sistemi VHD kopyalanan ve kopyalanan VHD hello ekleniyor.</span><span class="sxs-lookup"><span data-stu-id="050e8-379">Create hello VM using hello copied original OS VHD and attaching hello copied VHDs.</span></span>
* <span data-ttu-id="050e8-380">ILB yapılandırma / ELB ve uç noktalar ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="050e8-380">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="050e8-381">Dinleyici ya da güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="050e8-381">Update Listener by either:</span></span>
  * <span data-ttu-id="050e8-382">Merhaba üzerindeki her zaman grubu alma, çevrimdışı ve güncelleştirme her zaman üzerinde dinleyicisi yeni ILB ile Merhaba / ELB IP adresi.</span><span class="sxs-lookup"><span data-stu-id="050e8-382">Taking hello Always On Group offline and updating hello Always On Listener with new ILB / ELB IP address.</span></span>
  * <span data-ttu-id="050e8-383">Veya başlangıç IP adresi kaynağı'Windows Kümeleme içine, yeni bulut hizmeti ILB/ELB PowerShell aracılığıyla ekleme.</span><span class="sxs-lookup"><span data-stu-id="050e8-383">Or adding hello IP address resource of new Cloud Service ILB/ELB through PowerShell into Windows clustering.</span></span> <span data-ttu-id="050e8-384">Ardından kümesi hello olası sahipler hello IP adresi kaynak toohello düğümü, SQL2, geçiş ve bu hello ağ adı veya bağımlılıkla olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="050e8-384">Then set hello Possible owners of hello IP Address resource toohello migrated node, SQL2, and set this as OR dependency in hello Network Name.</span></span> <span data-ttu-id="050e8-385">Merhaba Hello 'Aynı alt ağdaki IP adresi kaynağı ekleme' bölümüne bakın [ek](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="050e8-385">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
* <span data-ttu-id="050e8-386">DNS yapılandırması/yayma toohello istemcileri denetleyin.</span><span class="sxs-lookup"><span data-stu-id="050e8-386">Check DNS configuration/propogation toohello clients.</span></span>
* <span data-ttu-id="050e8-387">SQL1 VM'yi geçirmek ve 2-4 arası adımlar gidin.</span><span class="sxs-lookup"><span data-stu-id="050e8-387">Migrate SQL1 VM, and go through steps 2 – 4.</span></span>
* <span data-ttu-id="050e8-388">IP adresi kaynağının olası sahip hello için eklenen adımları 5ii kullanıyorsanız, ardından SQL1 ekleyin</span><span class="sxs-lookup"><span data-stu-id="050e8-388">If using steps 5ii, then add SQL1 as a Possible Owner for hello added IP Address Resource</span></span>
* <span data-ttu-id="050e8-389">Test yük devretmeleri.</span><span class="sxs-lookup"><span data-stu-id="050e8-389">Test failovers.</span></span>

#### <a name="2-utilize-existing-secondary-replicas-multi-site"></a><span data-ttu-id="050e8-390">2. Var olan ikincil çoğaltmalar kullanma: çok siteli</span><span class="sxs-lookup"><span data-stu-id="050e8-390">2. Utilize existing secondary replica(s): Multi-Site</span></span>
<span data-ttu-id="050e8-391">Birden fazla Azure veri merkezinde (DC) düğümleriniz varsa veya karma bir ortamınız varsa, bu ortam toominimize kapalı kalma süresi her zaman açık yapılandırması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="050e8-391">If you have nodes in more than one Azure datacenter (DC) or if you have a hybrid environment, then you can use an Always On configuration in this environment toominimize downtime.</span></span>

<span data-ttu-id="050e8-392">Merhaba toochange hello her zaman açık eşitleme tooSynchronous hello şirket içi veya ikincil Azure DC ve yük devretme için SQL Server toothat yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="050e8-392">hello approach is toochange hello Always On synchronization tooSynchronous for hello on-premises or secondary Azure DC, and then failover over toothat SQL Server.</span></span> <span data-ttu-id="050e8-393">Merhaba VHD'ler tooa Premium depolama hesabı kopyalayın ve hello makineyi yeni bir bulut hizmetinde yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="050e8-393">Then copy hello VHDs tooa Premium Storage account, and redeploy hello machine into a new cloud service.</span></span> <span data-ttu-id="050e8-394">Merhaba dinleyicisi güncelleştirin ve geri dönecek.</span><span class="sxs-lookup"><span data-stu-id="050e8-394">Update hello listener, and then fail back.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="050e8-395">Kapalı kalma süresi noktaları</span><span class="sxs-lookup"><span data-stu-id="050e8-395">Points of downtime</span></span>
<span data-ttu-id="050e8-396">Merhaba kapalı kalma süresi başlangıç zamanı toofailover toohello alternatif DC ve geri oluşur.</span><span class="sxs-lookup"><span data-stu-id="050e8-396">hello downtime consists of hello time toofailover toohello alternative DC and back.</span></span> <span data-ttu-id="050e8-397">Ayrıca, istemci/DNS yapılandırmasına bağlıdır ve istemci yeniden bağlanmayı gecikebilir.</span><span class="sxs-lookup"><span data-stu-id="050e8-397">It also depends on your client/DNS configuration and your client reconnection may be delayed.</span></span>
<span data-ttu-id="050e8-398">Her zaman açık bir karma yapılandırma örneği aşağıdaki hello göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="050e8-398">Consider hello following example of a hybrid Always On configuration:</span></span>

![MultiSite1][9]

##### <a name="advantages"></a><span data-ttu-id="050e8-400">Avantajları</span><span class="sxs-lookup"><span data-stu-id="050e8-400">Advantages</span></span>
* <span data-ttu-id="050e8-401">Mevcut altyapısını kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="050e8-401">You can utilize existing infrastructure.</span></span>
* <span data-ttu-id="050e8-402">Öncelikle hello DR Azure DC üzerinde hello seçeneği toopre yükseltme hello Azure depolama olması.</span><span class="sxs-lookup"><span data-stu-id="050e8-402">You have hello option toopre-upgrade hello Azure storage on hello DR Azure DC first.</span></span>
* <span data-ttu-id="050e8-403">Merhaba DR Azure DC depolama yeniden.</span><span class="sxs-lookup"><span data-stu-id="050e8-403">hello DR Azure DC storage can be reconfigured.</span></span>
* <span data-ttu-id="050e8-404">Yük devretme sınaması işlemlerini hariç geçiş sırasında en az iki yük devretme işlemlerini yoktur.</span><span class="sxs-lookup"><span data-stu-id="050e8-404">There is a minimum of two failovers during migration, excluding test failovers.</span></span>
* <span data-ttu-id="050e8-405">Değil toomove SQL Server veri yedekleme ile gerekiyor ve geri yükleme.</span><span class="sxs-lookup"><span data-stu-id="050e8-405">You do not need toomove SQL Server data with backup and restore.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="050e8-406">Olumsuz yönleri</span><span class="sxs-lookup"><span data-stu-id="050e8-406">Disadvantages</span></span>
* <span data-ttu-id="050e8-407">İstemci erişim tooSQL bağlı olarak sunucu olabilir daha yüksek gecikme süresi SQL Server alternatif bir DC toohello uygulamada çalışırken.</span><span class="sxs-lookup"><span data-stu-id="050e8-407">Depending on client access tooSQL Server, there might be increased latency when SQL Server is running in an alternative DC toohello application.</span></span>
* <span data-ttu-id="050e8-408">Merhaba kopyalama zamanı VHD'ler tooPremium depolama uzun olabilir.</span><span class="sxs-lookup"><span data-stu-id="050e8-408">hello copy time of VHDs tooPremium storage could be long.</span></span> <span data-ttu-id="050e8-409">Bu olup olmadığını tookeep hello hello kullanılabilirlik grubu düğümü üzerinde kararınızı etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="050e8-409">This might affect your decision on whether tookeep hello node in hello Availability Group.</span></span> <span data-ttu-id="050e8-410">Bu işlem günlüğünde çoğaltılmamış işlemleri hello tookeep hello birincil düğüm gerekeceğinden günlük yoğun iş yükleri hello geçiş sırasında çalışan gerekli olduğunda için göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="050e8-410">Consider this for when log intensive work loads are running during hello migration is required, since hello Primary node will have tookeep hello unreplicated transactions in its transaction log.</span></span> <span data-ttu-id="050e8-411">Bu nedenle bu önemli oranda artma.</span><span class="sxs-lookup"><span data-stu-id="050e8-411">Therefore this could grow significantly.</span></span>
* <span data-ttu-id="050e8-412">Bu senaryo hello Azure kullanırsınız **başlangıç AzureStorageBlobCopy** zaman uyumsuz komutunu.</span><span class="sxs-lookup"><span data-stu-id="050e8-412">This scenario would use hello Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="050e8-413">Tamamlanma hiçbir SLA yoktur.</span><span class="sxs-lookup"><span data-stu-id="050e8-413">There is no SLA on completion.</span></span> <span data-ttu-id="050e8-414">Bu sıradaki bekleme bağlıdır sırada hello zaman hello kopyaları, değişir hello veri tootransfer miktarına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="050e8-414">hello time of hello copies varies, while this depends on wait in queue, it will also depend on hello amount of data tootransfer.</span></span> <span data-ttu-id="050e8-415">Bu nedenle 2 veri merkezinizde yalnızca bir düğüme sahip, hello kopyalama testinde uzun sürdüğünde durumda azaltma adımlarını sürer.</span><span class="sxs-lookup"><span data-stu-id="050e8-415">Therefore you just have one node in your 2nd data center, you should take mitigation steps in case hello copy takes longer than in testing.</span></span> <span data-ttu-id="050e8-416">Bu fikir aşağıdaki hello içerebilir.</span><span class="sxs-lookup"><span data-stu-id="050e8-416">This could include hello following ideas.</span></span>
  * <span data-ttu-id="050e8-417">Geçici bir 2 SQL düğüm HA için üzerinde anlaşılan kapalı kalma süresi ile Merhaba geçişten önce ekleyin.</span><span class="sxs-lookup"><span data-stu-id="050e8-417">Add a temporary 2nd SQL node for HA before hello migration with agreed downtime.</span></span>
  * <span data-ttu-id="050e8-418">Azure zamanlanmış bakım dışında Hello geçiş çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="050e8-418">Run hello migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="050e8-419">Küme çekirdeğini doğru yapılandırılmış olun.</span><span class="sxs-lookup"><span data-stu-id="050e8-419">Ensure you have configured your cluster quorum correctly.</span></span>

<span data-ttu-id="050e8-420">Bu senaryo, yüklemenizi belgelenmiş ve en yüksek disk önbelleği ayarları için sipariş toomake değişiklikleri hello depolama nasıl eşlenen bilmeniz varsayar.</span><span class="sxs-lookup"><span data-stu-id="050e8-420">This scenario assumes that you have documented your install and know how hello storage is mapped in order toomake changes for optimal disk cache settings.</span></span>

##### <a name="high-level-steps"></a><span data-ttu-id="050e8-421">Üst düzey adımlar</span><span class="sxs-lookup"><span data-stu-id="050e8-421">High-level steps</span></span>
![Multisite2][10]

* <span data-ttu-id="050e8-423">Şirket içi hello / Azure DC hello SQL Server birincil alternatif ve diğer otomatik yük devretme iş ortağı (AFP) hello hale olun.</span><span class="sxs-lookup"><span data-stu-id="050e8-423">Make hello on-premises / alternate Azure DC hello SQL Server Primary, and make it hello other Auto Failover Partner (AFP).</span></span>
* <span data-ttu-id="050e8-424">SQL2 ve Kaldır hello düğümü (ekli VHD'ler silmeyin) disk yapılandırma bilgilerini toplayın.</span><span class="sxs-lookup"><span data-stu-id="050e8-424">Gather disk configuration information from SQL2, and remove hello node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="050e8-425">Premium depolama hesabı oluşturma ve standart depolama hesabı hello VHD'ler kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="050e8-425">Create a Premium Storage account and copy VHDs from hello Standard Storage account.</span></span>
* <span data-ttu-id="050e8-426">Yeni bir bulut hizmeti oluşturun ve kendi prim depolama diskleri ekli hello SQL2 VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="050e8-426">Create a new cloud service and create hello SQL2 VM with its Premiums Storage disks attached.</span></span>
* <span data-ttu-id="050e8-427">ILB yapılandırma / ELB ve uç noktalar ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="050e8-427">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="050e8-428">Güncelleştirme hello her zaman üzerinde dinleyicisi yeni ILB ile / ELB IP adresi ve test yük devretme.</span><span class="sxs-lookup"><span data-stu-id="050e8-428">Update hello Always On Listener with new ILB / ELB IP address and test failover.</span></span>
* <span data-ttu-id="050e8-429">Merhaba DNS yapılandırmasını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="050e8-429">Check hello DNS configuration.</span></span>
* <span data-ttu-id="050e8-430">Merhaba AFP tooSQL2 değiştirin ve ardından SQL1 geçirmek ve 2 – 5 adımlarını gidin.</span><span class="sxs-lookup"><span data-stu-id="050e8-430">Change hello AFP tooSQL2, and then migrate SQL1 and go through steps 2 – 5.</span></span>
* <span data-ttu-id="050e8-431">Test yük devretmeleri.</span><span class="sxs-lookup"><span data-stu-id="050e8-431">Test failovers.</span></span>
* <span data-ttu-id="050e8-432">Merhaba AFP geri tooSQL1 ve SQL2 geçiş yapma</span><span class="sxs-lookup"><span data-stu-id="050e8-432">Switch hello AFP back tooSQL1 and SQL2</span></span>

## <a name="appendix-migrating-a-multisite-always-on-cluster-toopremium-storage"></a><span data-ttu-id="050e8-433">Ek: çoklu site her zaman üzerinde Küme tooPremium depolama birimi geçirme</span><span class="sxs-lookup"><span data-stu-id="050e8-433">Appendix: Migrating a Multisite Always On Cluster tooPremium Storage</span></span>
<span data-ttu-id="050e8-434">Bu konuda Hello geri kalanı bir çoklu site her zaman açık küme tooPremium depolama dönüştürme ayrıntılı bir örnek sağlar.</span><span class="sxs-lookup"><span data-stu-id="050e8-434">hello remainder of this topic provides a detailed example of converting a multi-site Always On cluster tooPremium storage.</span></span> <span data-ttu-id="050e8-435">Ayrıca, bir dış yük dengeleyici (ELB) tooan iç yük dengeleyici (ILB) kullanarak hello dinleyicisi da dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="050e8-435">It also converts hello Listener from using an external load balancer (ELB) tooan internal load balancer (ILB).</span></span>

### <a name="environment"></a><span data-ttu-id="050e8-436">Ortam</span><span class="sxs-lookup"><span data-stu-id="050e8-436">Environment</span></span>
* <span data-ttu-id="050e8-437">Windows 2k 12 / SQL 2k 12</span><span class="sxs-lookup"><span data-stu-id="050e8-437">Windows 2k12 / SQL 2k12</span></span>
* <span data-ttu-id="050e8-438">SP 1 DB dosyaları</span><span class="sxs-lookup"><span data-stu-id="050e8-438">1 DB Files on SP</span></span>
* <span data-ttu-id="050e8-439">Düğüm başına depolama havuzları x 2</span><span class="sxs-lookup"><span data-stu-id="050e8-439">2 x Storage Pools per Node</span></span>

![Appendix1][11]

### <a name="vm"></a><span data-ttu-id="050e8-441">VM:</span><span class="sxs-lookup"><span data-stu-id="050e8-441">VM:</span></span>
<span data-ttu-id="050e8-442">Bu örnekte, biz ELB tooILB taşıma toodemonstrate adımıdır.</span><span class="sxs-lookup"><span data-stu-id="050e8-442">In this example we are going toodemonstrate moving from an ELB tooILB.</span></span> <span data-ttu-id="050e8-443">Bu geçiş sırasında tooswitch toothis nasıl hello gösterecek şekilde ELB ILB önce mevcut değildi.</span><span class="sxs-lookup"><span data-stu-id="050e8-443">ELB was available before ILB, so this shows how tooswitch toothis during hello migration.</span></span>

![Appendix2][12]

### <a name="pre-steps-connect-toosubscription"></a><span data-ttu-id="050e8-445">Öncesi adımları: tooSubscription Bağlan</span><span class="sxs-lookup"><span data-stu-id="050e8-445">Pre Steps: Connect tooSubscription</span></span>
    Add-AzureAccount

    #Set up subscription
    Get-AzureSubscription

#### <a name="step-1-create-new-storage-account-and-cloud-service"></a><span data-ttu-id="050e8-446">1. adım: Yeni depolama hesabı oluşturun ve bulut hizmeti</span><span class="sxs-lookup"><span data-stu-id="050e8-446">Step 1: Create New Storage Account and Cloud Service</span></span>
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

#### <a name="step-2-increase-hello-permitted-failures-on-resources-optional"></a><span data-ttu-id="050e8-447">2. adım: kaynakları hataları izin artış hello<Optional></span><span class="sxs-lookup"><span data-stu-id="050e8-447">Step 2: Increase hello permitted failures on resources <Optional></span></span>
<span data-ttu-id="050e8-448">Tooyour her zaman üzerindeki kullanılabilirlik grubu ait bazı kaynaklar burada hello Küme hizmeti toorestart hello kaynak grubu çalışacak bir dönemde oluşabilir kaç hatalarda sınırları vardır.</span><span class="sxs-lookup"><span data-stu-id="050e8-448">On certain resources that belong tooyour Always On Availability Group there are limits on how many failures that can occur in a period, where hello cluster service will attempt toorestart hello resource group.</span></span> <span data-ttu-id="050e8-449">El ile yapmazsanız makineleri kapatılıyor tarafından yük devretme ve tetikleyici yük devretme Kapat toothis sınırı alabilirsiniz beri bu yordamı taramasını adımında, bu artırmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="050e8-449">It is recommended you increase this whilst you are walking through this procedure, since if you don’t manually failover and trigger failovers by shutting down machines you can get close toothis limit.</span></span>

<span data-ttu-id="050e8-450">Bu akıllıca toodouble hello hatası indirimi toodo yük devretme kümesi Yöneticisi'nde bunun olması, toohello hello her zaman açık kaynak grubunun özelliklerini gidin:</span><span class="sxs-lookup"><span data-stu-id="050e8-450">It would be prudent toodouble hello failure allowance, toodo this in Failover Cluster Manager, go toohello Properties of hello Always On resource group:</span></span>

![Appendix3][13]

<span data-ttu-id="050e8-452">Merhaba en fazla hata sayısı too6 değiştirin.</span><span class="sxs-lookup"><span data-stu-id="050e8-452">Change hello Maximum Failures too6.</span></span>

#### <a name="step-3-addition-ip-address-resource-for-cluster-group-optional"></a><span data-ttu-id="050e8-453">3. adım: Ek IP adresi kaynağı küme grubu için<Optional></span><span class="sxs-lookup"><span data-stu-id="050e8-453">Step 3: Addition IP Address resource for Cluster Group <Optional></span></span>
<span data-ttu-id="050e8-454">Yanlışlıkla hello bulut tüm küme düğümlerinde ağ sonra hello küme IP kaynak ve küme ağ adı mümkün toocome olmaz çevrimdışına varsa hello küme grubu için yalnızca bir IP adresi vardır ve bu hizalanmış toohello bulut alt yer alıyorsa, dikkatli olun Çevrimiçi.</span><span class="sxs-lookup"><span data-stu-id="050e8-454">If you have only one IP address for hello Cluster Group and this is aligned toohello cloud subnet, beware, if you accidentally take offline all cluster nodes in hello cloud on that network then hello Cluster IP resource and Cluster Network Name will not be able toocome online.</span></span> <span data-ttu-id="050e8-455">Hello engeller Bu olay tooother küme kaynaklarını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="050e8-455">In hello event of this it will prevent updates tooother cluster resources.</span></span>

#### <a name="step-4-dns-configuration"></a><span data-ttu-id="050e8-456">4. adım: DNS yapılandırması</span><span class="sxs-lookup"><span data-stu-id="050e8-456">Step 4: DNS configuration</span></span>
<span data-ttu-id="050e8-457">sorunsuz bir geçiş bağlıdır nasıl DNS yüklenmekte olan tooimplement kullanılan ve güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="050e8-457">tooimplement a smooth transition depends on how DNS is being utilized and updated.</span></span>
<span data-ttu-id="050e8-458">Her zaman açık yüklendiğinde, bir Windows Küme kaynak grubu oluşturur yük devretme kümesi Yöneticisi'ni açın, göreceğiniz en az üç kaynaklara sahip olur, hello belge hello iki tooare başvuruyor:</span><span class="sxs-lookup"><span data-stu-id="050e8-458">When Always On is installed, it creates a Windows Cluster Resource group, if you open Failover Cluster Manager, you will see that at a minimum it will have three resources, hello two that hello document refers tooare:</span></span>

* <span data-ttu-id="050e8-459">Sanal ağ adına (VNN) – budur hello DNS adı istemci tooconnect tooSQL sunucularına her zaman açık aracılığıyla isteyen toowhen bağlanın.</span><span class="sxs-lookup"><span data-stu-id="050e8-459">Virtual Network Name (VNN) – This is hello DNS name that client connect toowhen wanting tooconnect tooSQL Servers via Always On.</span></span>
* <span data-ttu-id="050e8-460">IP adresi kaynağı – budur hello VNN hello ile ilişkili IP adresi, birden fazla olabilir ve çok siteli bir yapılandırma her site/alt ağda bir IP adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="050e8-460">IP Address Resource – This is hello IP address that associated with hello VNN, you can have more than one, and in a multisite configuration you will have an IP address per site/subnet.</span></span>

<span data-ttu-id="050e8-461">Bağlantı tooSQL sunucu, hello SQL Server istemci sürücüsü hello dinleyicisi ile ilişkili hello DNS kayıtlarını almak ve tooconnect tooeach deneyin Always On IP adresi ilişkili, aşağıda bu etkileyebilir bazı etkenler aşağıdakiler ele.</span><span class="sxs-lookup"><span data-stu-id="050e8-461">When connecting tooSQL Server, hello SQL Server Client driver will retrieve hello DNS records associated with hello listener and try tooconnect tooeach Always On associated IP address, below we discuss some factors that can influence this.</span></span>

<span data-ttu-id="050e8-462">Merhaba hello dinleyicisi adıyla ilişkili eşzamanlı DNS kayıtlarının sayısı yalnızca hello ilişkili IP adreslerinin sayısı, aynı hello bağlıdır ' de Yük Devretme Kümelemesi hello her zaman açık VNN kaynak için RegisterAllIpProviders'setting.</span><span class="sxs-lookup"><span data-stu-id="050e8-462">hello number of concurrent DNS records that are associated with hello listener name depends not only on hello number of IP addresses associated, but hello ‘RegisterAllIpProviders’setting in Failover Clustering for hello Always ON VNN resource.</span></span>

<span data-ttu-id="050e8-463">Azure'da her zaman açık dağıttığınızda farklı adımlar toocreate hello dinleyicisi ve IP adresleri vardır, hello 'RegisterAllIpProviders' too1 yapılandırma toomanually sahip, bu her zaman açık farklı tooan şirket içi dağıtım nerede too1 ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="050e8-463">When you deploy Always On in Azure there are different steps toocreate hello Listener and IP Addresses, you have toomanually configure hello ‘RegisterAllIpProviders’ too1, this is different tooan on-premises Always On deployment where it is already set too1.</span></span>

<span data-ttu-id="050e8-464">'RegisterAllIpProviders' 0 ise, ardından yalnızca bir DNS kaydı DNS'de dinleyicisi hello ile ilişkili görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="050e8-464">If ‘RegisterAllIpProviders’ is 0, then you will only see one DNS record in DNS associated with hello Listener:</span></span>

![Appendix4][14]

<span data-ttu-id="050e8-466">'RegisterAllIpProviders' 1 ise:</span><span class="sxs-lookup"><span data-stu-id="050e8-466">If ‘RegisterAllIpProviders’ is 1:</span></span>

![Appendix5][15]

<span data-ttu-id="050e8-468">Aşağıdaki Hello kod hello VNN ayarları dökümü ve sizin için lütfen hello için Not Değiştir tootake etkisi tootake hello VNN çevrimdışı ve çevrimiçi geri dönüş gerekir, bu alma hello dinleyicisi çevrimdışı neden olan istemci bağlantı kesintisi.</span><span class="sxs-lookup"><span data-stu-id="050e8-468">hello code below will dump out hello VNN settings and set it for you, please note, for hello change tootake effect you will need tootake hello VNN offline and turn it back online, this taking hello Listener offline causing client connectivity disruption.</span></span>

    ##Always On Listener Name
    $ListenerName = "Mylistener"
    ##Get AlwaysOn Network Name Settings
    Get-ClusterResource $ListenerName| Get-ClusterParameter
    ##Set RegisterAllProvidersIP
    Get-ClusterResource $ListenerName| Set-ClusterParameter RegisterAllProvidersIP  1

<span data-ttu-id="050e8-469">Bu bir IP adresi kaynak temizleme ve ayrıca gerektireceğini, bir sonraki geçiş adımda tooupdate hello her zaman açık dinleyici bir yük dengeleyici başvurur güncelleştirilmiş bir IP adresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="050e8-469">In a later migration step you will need tooupdate hello Always On listener with an updated IP address that will reference a load balancer, this will involve an IP Address resource removal and addition.</span></span> <span data-ttu-id="050e8-470">Merhaba IP güncelleştirmeden sonra tooensure başlangıç IP adresi DNS bölgesinde güncelleştirildi ve hello istemciler kendi yerel DNS önbelleği güncelleştirdiğiniz yeni da gerekir.</span><span class="sxs-lookup"><span data-stu-id="050e8-470">After hello IP update, you need tooensure hello new IP address has been updated in DNS Zone and that hello clients are updating their local DNS cache.</span></span>

<span data-ttu-id="050e8-471">İstemcilerinizi farklı ağ kesimdeki bulunur ve farklı bir DNS sunucusu başvuru isterseniz ne olur DNS bölge aktarma hakkında hello geçiş sırasında hello uygulama yeniden gibi zaman kısıtlı tooconsider gereksinim tarafından en az hello bölge aktarım zamanını tüm yeni IP adresleri hello dinleyici için.</span><span class="sxs-lookup"><span data-stu-id="050e8-471">If your clients reside in a different network segment and reference a different DNS server, you need tooconsider what happens about DNS Zone Transfer during hello migration, as hello application reconnect time will be constrained by at least hello Zone Transfer Time of any new IP addresses for hello listener.</span></span> <span data-ttu-id="050e8-472">Burada zaman sınırlaması altında olup olmadığını ele almaktadır ve Windows ekipleriniz ile bir artımlı bölge aktarımı zorlama test ve ayrıca hello DNS konumuna ana bilgisayar kaydı tooa alt süresi tooLive (TTL), güncelleştirme hello istemciler için.</span><span class="sxs-lookup"><span data-stu-id="050e8-472">If you are under time constraint here, you should discuss and test forcing an incremental zone transfer with your Windows teams, and also put hello DNS host record tooa lower Time tooLive (TTL), so hello clients update.</span></span> <span data-ttu-id="050e8-473">Daha fazla bilgi için bkz: [artımlı bölge aktarımlarının](https://technet.microsoft.com/library/cc958973.aspx) ve [başlangıç DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span><span class="sxs-lookup"><span data-stu-id="050e8-473">For more information, see [Incremental Zone Transfers](https://technet.microsoft.com/library/cc958973.aspx) and [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span></span>

<span data-ttu-id="050e8-474">Varsayılan hello hello Azure'nın her zaman açık dinleyicisinde ile ilişkili DNS kaydının TTL tarafından 1200 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="050e8-474">By default hello TTL for DNS Record that is associated with hello Listener in Always On in Azure is 1200 seconds.</span></span> <span data-ttu-id="050e8-475">Merhaba dinleyici için kendi DNS güncelleştirilmiş hello IP adresi, geçiş tooensure hello istemcileri güncelleştirme sırasında zaman sınırlaması altında olduğunda bu tooreduce isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="050e8-475">You may wish tooreduce this if you are under time constraint during your migration tooensure hello clients update their DNS with hello updated IP address for hello listener.</span></span> <span data-ttu-id="050e8-476">Bakın ve hello VNN hello yapılandırma dökme tarafından hello yapılandırmasını değiştirin:</span><span class="sxs-lookup"><span data-stu-id="050e8-476">You can see and modify hello configuration by dumping out hello configuration of hello VNN:</span></span>

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"
    #Look at HostRecordTTL
    Get-ClusterResource $ListenerName| Get-ClusterParameter

    #Set HostRecordTTL Examples
    Get-ClusterResource $ListenerName| Set-ClusterParameter -Name "HostRecordTTL" 120

<span data-ttu-id="050e8-477">Lütfen hello alt hello 'HostRecordTTL', daha yüksek bir DNS trafik miktarı oluşacaktır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="050e8-477">Please note, hello lower hello ‘HostRecordTTL’, a higher amount of DNS traffic will occur.</span></span>

##### <a name="client-application-settings"></a><span data-ttu-id="050e8-478">İstemci uygulama ayarları</span><span class="sxs-lookup"><span data-stu-id="050e8-478">Client application settings</span></span>
<span data-ttu-id="050e8-479">.Net 4.5, SQL istemci uygulamanın desteklediği hello varsa SQLClient sonra kullanabileceğiniz ' MULTISUBNETFAILOVER = TRUE' anahtar sözcüğü, bu daha hızlı bağlantı tooSQL her zaman üzerindeki kullanılabilirlik grubu için yük devretme sırasında verdiğinden uygulanan toobe önerilir.</span><span class="sxs-lookup"><span data-stu-id="050e8-479">If your SQL client application supports hello .Net 4.5 SQLClient, then you can use ‘MULTISUBNETFAILOVER=TRUE’ keyword, this is recommended toobe applied as it allows for faster connection tooSQL Always On Availability Group during failover.</span></span> <span data-ttu-id="050e8-480">Merhaba her zaman açık dinleyici paralel ile ilişkili tüm IP adreslerini aracılığıyla numaralandırır ve yük devretme sırasında daha agresif bir TCP bağlantı yeniden deneme hızı gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="050e8-480">It enumerates through all IP addresses associated with hello Always On listener in parallel, and performs a more aggressive TCP connection retry speed during a failover.</span></span>

<span data-ttu-id="050e8-481">Yukarıdaki hello ayarlarla ilgili daha fazla bilgi için lütfen bkz [MultiSubnetFailover anahtar sözcüğü ve ilişkili özellikleri](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span><span class="sxs-lookup"><span data-stu-id="050e8-481">For more information regarding hello settings above, please see [MultiSubnetFailover Keyword and Associated Features](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span></span> <span data-ttu-id="050e8-482">Ayrıca bkz. [SqlClient yüksek kullanılabilirlik, olağanüstü durum kurtarma desteği](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="050e8-482">Also see [SqlClient Support for High Availability, Disaster Recovery](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span></span>

#### <a name="step-5-cluster-quorum-settings"></a><span data-ttu-id="050e8-483">5. adım: Küme çekirdek ayarlarını</span><span class="sxs-lookup"><span data-stu-id="050e8-483">Step 5: Cluster quorum settings</span></span>
<span data-ttu-id="050e8-484">Aynı anda en az bir SQL Server kullanıma alma toobe kalacaklarını gibi dosya paylaşım tanığı (FSW) ile 2 düğümleri kullanarak hello çekirdek tooallow düğüm çoğunluğu ayarlamak ve dinamik oy kullanmasına ve bu tooallow için ise hello küme çekirdek ayarı değiştirmelisiniz bir tek düğümlü tooremain konumu.</span><span class="sxs-lookup"><span data-stu-id="050e8-484">As you are going toobe taking out at least one SQL Server down at a time, you should modify hello cluster quorum setting, if using File Share Witness (FSW) with 2 nodes, you should set hello quorum tooallow node majority and utilize dynamic voting, and this is tooallow for a single node tooremain standing.</span></span>

    Set-ClusterQuorum -NodeMajority  

<span data-ttu-id="050e8-485">Yönetme ve hello küme çekirdek yapılandırması hakkında daha fazla bilgi için lütfen bkz [bir Windows Server 2012 yük devretme kümesinde çekirdeği yapılandırma ve yönetme hello](https://technet.microsoft.com/library/jj612870.aspx).</span><span class="sxs-lookup"><span data-stu-id="050e8-485">For more information on managing and configuring hello cluster quorum, please see [Configure and Manage hello Quorum in a Windows Server 2012 Failover Cluster](https://technet.microsoft.com/library/jj612870.aspx).</span></span>

#### <a name="step-6-extract-existing-endpoints-and-acls"></a><span data-ttu-id="050e8-486">6. adım: Mevcut uç noktalar ACL ayıklayıp</span><span class="sxs-lookup"><span data-stu-id="050e8-486">Step 6: Extract Existing Endpoints and ACLs</span></span>
    #GET Endpoint info
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureEndpoint
    #GET ACL Rules for Each EP, this example is for hello Always On Endpoint
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureAclConfig -EndpointName "myAOEndPoint-LB"  

<span data-ttu-id="050e8-487">Bu tooa metin dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="050e8-487">Save these tooa text file.</span></span>

#### <a name="step-7-change-failover-partners-and-replication-modes"></a><span data-ttu-id="050e8-488">7. adım: Yük devretme iş ortakları ve çoğaltma modları değiştirme</span><span class="sxs-lookup"><span data-stu-id="050e8-488">Step 7: Change Failover Partners and Replication Modes</span></span>
<span data-ttu-id="050e8-489">2'den fazla SQL sunucunuz varsa, başka bir DC başka bir ikincil hello yük devretme değiştirmeniz veya şirket içi too'Synchronous ve bir otomatik yük devretme iş ortağı (AFP) olun, değişiklik yapmadan adımında HA korumak için bu.</span><span class="sxs-lookup"><span data-stu-id="050e8-489">If you have more than 2 SQL Servers, you should change hello failover of another secondary in another DC or on-premises too‘Synchronous’ and make it an Automatic Failover Partner (AFP), this is so you maintain HA whilst you are making changes.</span></span> <span data-ttu-id="050e8-490">Bunu TSQL yapabilirsiniz ancak SSMS değiştirin:</span><span class="sxs-lookup"><span data-stu-id="050e8-490">You can do this through TSQL of modify though SSMS:</span></span>

![Appendix6][16]

#### <a name="step-8-remove-secondary-vm-from-cloud-service"></a><span data-ttu-id="050e8-492">8. adım: İkincil VM bulut hizmetinden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="050e8-492">Step 8: Remove Secondary VM from cloud service</span></span>
<span data-ttu-id="050e8-493">Toomigrate bulut ikincil düğüme planlama yapmanız gereken ilk olarak, bu şu anda birincil ise, el ile bir yük devretme başlatın.</span><span class="sxs-lookup"><span data-stu-id="050e8-493">You should be planning toomigrate a cloud secondary node first, if this is currently primary, you should initiate a manual failover.</span></span>

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

#### <a name="step-9-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="050e8-494">9. adım: önbelleğe alma ayarları CSV dosyasındaki disk değiştirin ve kaydedin</span><span class="sxs-lookup"><span data-stu-id="050e8-494">Step 9: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="050e8-495">Veri birimleri için bu tooREADONLY ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="050e8-495">For data volumes these should be set tooREADONLY.</span></span>

<span data-ttu-id="050e8-496">TLOG birimleri için bu tooNONE ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="050e8-496">For TLOG volumes these should be set tooNONE.</span></span>

![Appendix7][17]

#### <a name="step-10-copy-vhds"></a><span data-ttu-id="050e8-498">10. adım: Kopyalama VHD'leri</span><span class="sxs-lookup"><span data-stu-id="050e8-498">Step 10: Copy VHDS</span></span>
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



<span data-ttu-id="050e8-499">Merhaba kopyalama hello VHD'ler toohello Premium depolama hesabı durumunu denetleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="050e8-499">You can check hello copy status of hello VHDs toohello Premium Storage account:</span></span>

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

<span data-ttu-id="050e8-501">Bunların tümü başarılı kaydedilir kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="050e8-501">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="050e8-502">Tek tek bloblar için daha fazla bilgi için:</span><span class="sxs-lookup"><span data-stu-id="050e8-502">For information for individual blobs:</span></span>

    Get-AzureStorageBlobCopyState -Blob "blobname.vhd" -Container $containerName -Context $xioContext

#### <a name="step-11-register-os-disk"></a><span data-ttu-id="050e8-503">11. adım: Kayıt işletim sistemi diski</span><span class="sxs-lookup"><span data-stu-id="050e8-503">Step 11: Register OS disk</span></span>
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

#### <a name="step-12-import-secondary-into-new-cloud-service"></a><span data-ttu-id="050e8-504">12. adım: yeni bulut hizmetinde ikincil alma</span><span class="sxs-lookup"><span data-stu-id="050e8-504">Step 12: Import secondary into new cloud service</span></span>
<span data-ttu-id="050e8-505">Merhaba kodu aynı zamanda eklenen kullanır hello aşağıda seçeneği Burada, hello makine aktarıp hello retainable VIP kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="050e8-505">hello code below also uses hello added option here you can import hello machine and use hello retainable VIP.</span></span>

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

#### <a name="step-13-create-ilb-on-new-cloud-svc-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="050e8-506">13. adım: Yük eklemek ILB yeni bulut Svc üzerinde oluşturma dengeli uç noktaları ve ACL'leri</span><span class="sxs-lookup"><span data-stu-id="050e8-506">Step 13: Create ILB on New Cloud Svc, Add Load Balanced Endpoints and ACLs</span></span>
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

#### <a name="step-14-update-always-on"></a><span data-ttu-id="050e8-507">14. adım: Her zaman üzerinde güncelleştir</span><span class="sxs-lookup"><span data-stu-id="050e8-507">Step 14: Update Always On</span></span>
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

<span data-ttu-id="050e8-509">Şimdi hello eski bulut hizmeti IP adresini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="050e8-509">Now remove hello old cloud service IP Address.</span></span>

![Appendix10][20]

#### <a name="step-15-dns-update-check"></a><span data-ttu-id="050e8-511">15. adım: DNS güncelleştirme denetimi</span><span class="sxs-lookup"><span data-stu-id="050e8-511">Step 15: DNS update check</span></span>
<span data-ttu-id="050e8-512">Şimdi DNS sunucuları, SQL Server istemci ağlarda denetlemeniz ve gerekir kümeleme hello eklenmiş olduğundan emin olun ek ana bilgisayar kaydı hello için eklenen IP adresi.</span><span class="sxs-lookup"><span data-stu-id="050e8-512">You should now check DNS Servers on your SQL Server client networks and make sure that clustering has added hello extra host record for hello added IP address.</span></span> <span data-ttu-id="050e8-513">Bu DNS sunucuları gerçekleştirmediyseniz hello orada alt ağdaki istemcilerin olduğundan mümkün tooresolve tooboth her zaman IP adresleri üzerindeki ve otomatik DNS çoğaltma için toowait gerek yoktur bu olduğundan emin ve DNS bölge aktarımı zorlama düşünün.</span><span class="sxs-lookup"><span data-stu-id="050e8-513">If those DNS servers have not updated, consider forcing a DNS Zone transfer and ensure that hello clients in there subnet are able tooresolve tooboth Always On IP Addresses, this is so you do not need toowait for automatic DNS replication.</span></span>

#### <a name="step-16-reconfigure-always-on"></a><span data-ttu-id="050e8-514">16. adım: Her zaman yeniden yapılandırın</span><span class="sxs-lookup"><span data-stu-id="050e8-514">Step 16: Reconfigure Always On</span></span>
<span data-ttu-id="050e8-515">Bu noktada hello geçirilen toofully olan bu düğüme hello şirket içi düğümle ve yeniden eşitleyin ve toosynchronous çoğaltma düğümü geçiş hello AFP olun ikincil bekleyin.</span><span class="sxs-lookup"><span data-stu-id="050e8-515">At this point you wait for hello secondary that node that was migrated toofully resynchronize with hello on-premises node and switch toosynchronous replication node and make it hello AFP.</span></span>  

#### <a name="step-17-migrate-second-node"></a><span data-ttu-id="050e8-516">17. adım: ikinci düğümü geçirme</span><span class="sxs-lookup"><span data-stu-id="050e8-516">Step 17: Migrate second node</span></span>
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

#### <a name="step-18-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="050e8-517">Adım 18: önbelleğe alma ayarları CSV dosyasındaki disk değiştirin ve kaydedin</span><span class="sxs-lookup"><span data-stu-id="050e8-517">Step 18: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="050e8-518">Veri birimleri için bu tooREADONLY ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="050e8-518">For data volumes these should be set tooREADONLY.</span></span>

<span data-ttu-id="050e8-519">TLOG birimleri için bu tooNONE ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="050e8-519">For TLOG volumes these should be set tooNONE.</span></span>

![Appendix11][21]

#### <a name="step-19-create-new-independent-storage-account-for-secondary-node"></a><span data-ttu-id="050e8-521">19. adım: İkincil düğüm için yeni bağımsız depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="050e8-521">Step 19: Create New Independent Storage Account for Secondary Node</span></span>
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

#### <a name="step-20-copy-vhds"></a><span data-ttu-id="050e8-522">20. adım: Kopyalama VHD'leri</span><span class="sxs-lookup"><span data-stu-id="050e8-522">Step 20: Copy VHDS</span></span>
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


<span data-ttu-id="050e8-523">Tüm VHD'leri için hello VHD kopya durumunu denetleyebilirsiniz: ForEach ($disk $diskobjects içinde) {$lun $disk =. LUN $vhdname $disk.vhdname $cacheoption = $disk =. HostCaching $disklabel $disk =. Disketiketi $diskName $disk =. DiskName</span><span class="sxs-lookup"><span data-stu-id="050e8-523">You can check hello VHD copy status for all VHDs: ForEach ($disk in $diskobjects) { $lun = $disk.Lun $vhdname = $disk.vhdname $cacheoption = $disk.HostCaching $disklabel = $disk.DiskLabel $diskName = $disk.DiskName</span></span>

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContextnode2
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix12][22]

<span data-ttu-id="050e8-525">Bunların tümü başarılı kaydedilir kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="050e8-525">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="050e8-526">Tek tek bloblar için daha fazla bilgi için:</span><span class="sxs-lookup"><span data-stu-id="050e8-526">For information for individual blobs:</span></span>

    #Check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContextnode2

#### <a name="step-21-register-os-disk"></a><span data-ttu-id="050e8-527">21. adım: Kayıt işletim sistemi diski</span><span class="sxs-lookup"><span data-stu-id="050e8-527">Step 21: Register OS disk</span></span>
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

#### <a name="step-22-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="050e8-528">22. adım: Yük ekleme dengeli uç noktaları ve ACL'leri</span><span class="sxs-lookup"><span data-stu-id="050e8-528">Step 22: Add Load Balanced Endpoints and ACLs</span></span>
    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM


    #STOP!!! CHECK in hello Azure portal or Machine Endpoints through PowerShell that these Endpoints are created!

    #SET ACLs or Azure Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

#### <a name="step-23-test-failover"></a><span data-ttu-id="050e8-529">23. adım: Yük devretme sınaması</span><span class="sxs-lookup"><span data-stu-id="050e8-529">Step 23: Test failover</span></span>
<span data-ttu-id="050e8-530">Artık her zaman açık hello şirket içi düğümle eşitleyin, toosynchronous çoğaltma modunda yerleştirin ve onu eşitlenene kadar bekleyin hello geçirilen düğüm izin vermemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="050e8-530">You should now let hello migrated node synchronize with hello on-premises Always On node, place it in toosynchronous replication mode and wait until it is synchronized.</span></span> <span data-ttu-id="050e8-531">Ardından hello AFP olduğu bir şirket içi toohello ilk düğümü yük devretmeyi geçirildi.</span><span class="sxs-lookup"><span data-stu-id="050e8-531">Then failover from on-prem toohello first node migrated, which is hello AFP.</span></span> <span data-ttu-id="050e8-532">Çalıştıktan sonra değişiklik hello son düğümü toohello AFP geçirildi.</span><span class="sxs-lookup"><span data-stu-id="050e8-532">Once that has worked, change hello last migrated node toohello AFP.</span></span>

<span data-ttu-id="050e8-533">Test yük devretmeleri tüm düğümler arasında ve chaos testleri olarak tooensure yerine iş bekleniyordu ancak ve zamanında manor çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="050e8-533">You should test failovers between all nodes and run though chaos tests tooensure failovers work as expected and in a timely manor.</span></span>

#### <a name="step-24-put-back-cluster-quorum-settings--dns-ttl--failover-pntrs--sync-settings"></a><span data-ttu-id="050e8-534">24. adım: geri küme çekirdek ayarlarını Put / DNS TTL / yük devretme Pntrs / eşitleme ayarları</span><span class="sxs-lookup"><span data-stu-id="050e8-534">Step 24: Put back cluster quorum settings / DNS TTL / Failover Pntrs / Sync Settings</span></span>
##### <a name="adding-ip-address-resource-on-same-subnet"></a><span data-ttu-id="050e8-535">Aynı alt ağdaki IP adresi kaynağı ekleme</span><span class="sxs-lookup"><span data-stu-id="050e8-535">Adding IP Address Resource on Same Subnet</span></span>
<span data-ttu-id="050e8-536">Yalnızca 2 SQL sunucunuz varsa ve toomigrate istediğiniz bunları tooa yeni bulut hizmeti, ancak tookeep istediğiniz üzerlerinde Merhaba aynı alt ağ, hello dinleyicisi her zaman çevrimdışı toodelete hello özgün IP adresinde almaktan kaçının ve hello yeni IP adresini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="050e8-536">If you have only 2 SQL Servers and want toomigrate them tooa new cloud service, but want tookeep them on hello same subnet, you can avoid taking hello listener offline toodelete hello original Always On IP Address and add hello New IP Address.</span></span> <span data-ttu-id="050e8-537">Merhaba VM'ler tooanother alt ağı olacaktır gibi alt başvurur bir ek küme ağı, toodo bu ihtiyacınız olmadığından geçiriyorsanız.</span><span class="sxs-lookup"><span data-stu-id="050e8-537">If you are migrating hello VMs tooanother subnet you will not need toodo this as there will be an additional cluster network that will reference that subnet.</span></span>

<span data-ttu-id="050e8-538">Getirdiğiniz sonra hello ikincil geçiş ve yük devretme hello önce var olan birincil hello yeni IP adresi kaynak hello yeni bulut hizmeti için eklenen, hello küme Yük Devretme Yöneticisi içinde şu adımları uygulamanız:</span><span class="sxs-lookup"><span data-stu-id="050e8-538">Once you have brought up hello migrated secondary and added in hello new IP Address resource for hello new cloud service before failover hello existing Primary, you should take these steps within hello Cluster Failover Manager:</span></span>

<span data-ttu-id="050e8-539">tooadd IP adresini bakın hello [ek](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), 14. adım.</span><span class="sxs-lookup"><span data-stu-id="050e8-539">tooadd in IP Address, see hello [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), step 14.</span></span>

1. <span data-ttu-id="050e8-540">Hello olası sahip too'Existing birincil SQL Server Hello geçerli IP adresi kaynağı için Değiştir ', 'dansqlams4' aşağıda hello örnekte:</span><span class="sxs-lookup"><span data-stu-id="050e8-540">For hello current IP Address resource, change hello possible owner too‘Existing Primary SQL Server’, in hello example below, ‘dansqlams4’:</span></span>

    ![Appendix13][23]
2. <span data-ttu-id="050e8-542">Merhaba olası sahip too'Migrated Hello yeni IP adresi kaynağı için değiştirme ikincil SQL Server', 'dansqlams5' aşağıda hello örnekte:</span><span class="sxs-lookup"><span data-stu-id="050e8-542">For hello new IP Address resource, change hello possible owner too‘Migrated secondary SQL Server’, in hello example below, ‘dansqlams5’:</span></span>

    ![Appendix14][24]
3. <span data-ttu-id="050e8-544">Merhaba son düğümü geçirildiğinde bu düğümü olası sahip olarak eklenir şekilde hello olası sahipler düzenlenmesi gerekir ve bu ayarlandıktan sonra Yük devretme kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="050e8-544">Once this is set you can failover, and when hello last node is migrated hello Possible Owners should be edited so that node is added as a Possible Owner:</span></span>

    ![Appendix15][25]

## <a name="additional-resources"></a><span data-ttu-id="050e8-546">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="050e8-546">Additional resources</span></span>
* [<span data-ttu-id="050e8-547">Azure Premium depolama</span><span class="sxs-lookup"><span data-stu-id="050e8-547">Azure Premium Storage</span></span>](../../../storage/common/storage-premium-storage.md)
* [<span data-ttu-id="050e8-548">Sanal Makineler</span><span class="sxs-lookup"><span data-stu-id="050e8-548">Virtual Machines</span></span>](https://azure.microsoft.com/services/virtual-machines/)
* [<span data-ttu-id="050e8-549">Azure sanal makinelerde SQL Server</span><span class="sxs-lookup"><span data-stu-id="050e8-549">SQL Server in Azure Virtual Machines</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

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
