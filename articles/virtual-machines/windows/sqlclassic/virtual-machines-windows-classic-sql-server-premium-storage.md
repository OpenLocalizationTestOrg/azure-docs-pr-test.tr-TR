---
title: SQL Server ile Azure Premium Storage kullanma | Microsoft Docs
description: "Bu makale Klasik dağıtım modeli kullanılarak oluşturulmuş kaynaklarını kullanır ve Azure sanal makinelerde çalışan SQL Server ile Azure Premium Storage kullanma hakkında yönergeler sağlar."
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
ms.openlocfilehash: 6790db207fc7ec8a4b1546ef07c97ef30abe9513
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-premium-storage-with-sql-server-on-virtual-machines"></a><span data-ttu-id="2889a-103">Sanal Makineler’de SQL Server ile Azure Premium Depolama kullanma</span><span class="sxs-lookup"><span data-stu-id="2889a-103">Use Azure Premium Storage with SQL Server on Virtual Machines</span></span>
## <a name="overview"></a><span data-ttu-id="2889a-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="2889a-104">Overview</span></span>
<span data-ttu-id="2889a-105">[Azure Premium Storage](../../../storage/common/storage-premium-storage.md) düşük gecikme süresi ve yüksek verimlilik GÇ sağlayan depolama gelecek nesil.</span><span class="sxs-lookup"><span data-stu-id="2889a-105">[Azure Premium Storage](../../../storage/common/storage-premium-storage.md) is the next generation of storage that provides low latency and high throughput IO.</span></span> <span data-ttu-id="2889a-106">Anahtar g/ç yoğun iş yükleri, Iaas üzerinde SQL Server gibi en iyi şekilde çalışır [sanal makineleri](https://azure.microsoft.com/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="2889a-106">It works best for key IO intensive workloads, such as SQL Server on IaaS [Virtual Machines](https://azure.microsoft.com/services/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2889a-107">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2889a-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="2889a-108">Bu makalede, Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="2889a-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="2889a-109">Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="2889a-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="2889a-110">Bu makale, planlama ve Premium depolama kullanmak için SQL Server çalıştıran bir sanal makine geçirmek için yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="2889a-110">This article provides planning and guidance for migrating a Virtual Machine running SQL Server to use Premium Storage.</span></span> <span data-ttu-id="2889a-111">Bu, Azure altyapı (ağ, depolama) ve Konuk Windows VM adımları içerir.</span><span class="sxs-lookup"><span data-stu-id="2889a-111">This includes Azure infrastructure (networking, storage) and guest Windows VM steps.</span></span> <span data-ttu-id="2889a-112">Örnekte [ek](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) PowerShell ile geliştirilmiş yerel SSD depolama yararlanmak için daha büyük sanal makineleri taşımak nasıl tam kapsamlı bir uçtan uca geçişini gösterir.</span><span class="sxs-lookup"><span data-stu-id="2889a-112">The example in the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) shows a full comprehensive end to end migration of how to move larger VMs to take advantage of improved local SSD storage with PowerShell.</span></span>

<span data-ttu-id="2889a-113">Uçtan uca işlemi kullanılarak Azure Premium Storage IAAS Vm'leri üzerinde SQL Server ile anlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="2889a-113">It is important to understand the end-to-end process of utilizing Azure Premium Storage with SQL Server on IAAS VMs.</span></span> <span data-ttu-id="2889a-114">Buna aşağıdakiler dahildir:</span><span class="sxs-lookup"><span data-stu-id="2889a-114">This includes:</span></span>

* <span data-ttu-id="2889a-115">Premium depolama kullanmak için Önkoşullar kimliği.</span><span class="sxs-lookup"><span data-stu-id="2889a-115">Identification of the prerequisites to use Premium Storage.</span></span>
* <span data-ttu-id="2889a-116">SQL Server Iaas üzerinde yeni dağıtımlar için Premium depolama alanına dağıtma örnekleri.</span><span class="sxs-lookup"><span data-stu-id="2889a-116">Examples of deploying SQL Server on IaaS to Premium Storage for new deployments.</span></span>
* <span data-ttu-id="2889a-117">Geçirme varolan dağıtımları, hem tek başına sunucular hem de SQL Always On kullanılabilirlik grupları kullanarak dağıtımları örnekleri.</span><span class="sxs-lookup"><span data-stu-id="2889a-117">Examples of migrating existing deployments, both stand-alone servers and deployments using SQL Always On Availability Groups.</span></span>
* <span data-ttu-id="2889a-118">Olası geçiş yaklaşıyor.</span><span class="sxs-lookup"><span data-stu-id="2889a-118">Possible migration approaches.</span></span>
* <span data-ttu-id="2889a-119">Mevcut bir Always On uygulamasına yükseltme için Azure, Windows ve SQL Server adımlar gösteren baştan sona tam örnek.</span><span class="sxs-lookup"><span data-stu-id="2889a-119">Full end-to-end example showing Azure, Windows, and SQL Server steps for the migration of an existing Always On implementation.</span></span>

<span data-ttu-id="2889a-120">Azure Virtual Machines'de SQL Server üzerinde daha fazla bilgi için bkz: [Azure Virtual Machines'de SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2889a-120">For more background information on SQL Server in Azure Virtual Machines, see [SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

<span data-ttu-id="2889a-121">**Yazar:** Daniel Sol **Teknik İnceleme:** Haluk Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz'e.</span><span class="sxs-lookup"><span data-stu-id="2889a-121">**Author:** Daniel Sol **Technical Reviewers:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span></span>

## <a name="prerequisites-for-premium-storage"></a><span data-ttu-id="2889a-122">Premium depolama için Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="2889a-122">Prerequisites for Premium Storage</span></span>
<span data-ttu-id="2889a-123">Premium depolama kullanmak için birkaç önkoşul vardır.</span><span class="sxs-lookup"><span data-stu-id="2889a-123">There are several prerequisites for using Premium Storage.</span></span>

### <a name="machine-size"></a><span data-ttu-id="2889a-124">Makine boyutu</span><span class="sxs-lookup"><span data-stu-id="2889a-124">Machine size</span></span>
<span data-ttu-id="2889a-125">Premium depolama kullanmak için DS serisi sanal makineler (VM) kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2889a-125">For using Premium Storage you will need to use DS series Virtual Machines (VM).</span></span> <span data-ttu-id="2889a-126">Bulut hizmetinizde önce DS serisi makineler kullanmadıysanız, var olan VM silme, ekli diskleri tutmak ve ardından yeni bir bulut hizmeti VM DS * rol boyutu olarak yeniden oluşturmadan önce oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2889a-126">If you have not used DS Series machines in your cloud service before, you must delete the existing VM, keep the attached disks, and then create a new cloud service before recreating the VM as DS* role size.</span></span> <span data-ttu-id="2889a-127">Sanal makine boyutları hakkında daha fazla bilgi için bkz: [sanal makine ve bulut hizmeti boyutları Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2889a-127">For more information on Virtual Machine sizes, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="cloud-services"></a><span data-ttu-id="2889a-128">Bulut hizmetleri</span><span class="sxs-lookup"><span data-stu-id="2889a-128">Cloud services</span></span>
<span data-ttu-id="2889a-129">Yeni bir bulut hizmetinde oluşturduğunuzda, DS * VM'ler yalnızca Premium Storage ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2889a-129">You can only use DS* VMs with Premium Storage when they are created in a new cloud service.</span></span> <span data-ttu-id="2889a-130">Azure'da SQL Server Always On kullanıyorsanız, her zaman üzerinde dinleyicisi bulut hizmetiyle ilişkili Azure iç veya dış yük dengeleyici IP adresine başvurur.</span><span class="sxs-lookup"><span data-stu-id="2889a-130">If you are using SQL Server Always On in Azure, the Always On Listener will refer to the Azure Internal or External Load Balancer IP address that is associated with a cloud service.</span></span> <span data-ttu-id="2889a-131">Bu makalede, bu senaryoda kullanılabilirliğini korurken geçirmek nasıl odaklanır.</span><span class="sxs-lookup"><span data-stu-id="2889a-131">This article focuses on how to migrate while maintaining availability in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="2889a-132">DS * serisi yeni bulut hizmeti dağıtılmış ilk VM olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2889a-132">A DS* Series must be the first VM that is deployed to the new Cloud Service.</span></span>
>
>

### <a name="regional-vnets"></a><span data-ttu-id="2889a-133">Bölgesel sanal ağlar</span><span class="sxs-lookup"><span data-stu-id="2889a-133">Regional VNETS</span></span>
<span data-ttu-id="2889a-134">DS * VM'ler için sanal ağ (Bölgesel olması için sanal makineleri barındırdığı VNET) yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2889a-134">For DS* VMs you must configure the Virtual Network (VNET) hosting your VMs to be regional.</span></span> <span data-ttu-id="2889a-135">Bu "widens" VNET diğer kümelerde sağlanması ve aralarında iletişim sağlamak daha büyük sanal makineleri izin vermektir.</span><span class="sxs-lookup"><span data-stu-id="2889a-135">This “widens” the VNET is to allow the larger VMs to be provisioned in other clusters and allow communication between them.</span></span> <span data-ttu-id="2889a-136">Oysa "dar" VNET ilk sonuçlarını gösterir aşağıdaki ekran görüntüsünde vurgulanan konumda bölgesel sanal ağlara gösterir.</span><span class="sxs-lookup"><span data-stu-id="2889a-136">In the following screenshot, the highlighted Location shows regional VNETs, whereas the first result shows a “narrow” VNET.</span></span>

![RegionalVNET][1]

<span data-ttu-id="2889a-138">Bölgesel bir sanal ağ geçirmek için Microsoft destek bileti oluşturabilir, Microsoft bir değişiklik, ardından bölgesel sanal ağlar için geçiş işlemini tamamlamak için ağ yapılandırmasını AffinityGroup özelliğinde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2889a-138">You can raise a Microsoft support ticket to migrate to a regional VNET, Microsoft will make a change, then to complete the migration to regional VNETs, change the property AffinityGroup in the network configuration.</span></span> <span data-ttu-id="2889a-139">İlk ağ yapılandırmasını PowerShell'de dışarı aktarmak ve ardından Değiştir **AffinityGroup** özelliğinde **VirtualNetworkSite** öğesi ile bir **konumu** özelliği.</span><span class="sxs-lookup"><span data-stu-id="2889a-139">First export the Network Configuration in PowerShell, and then replace the **AffinityGroup** property in the **VirtualNetworkSite** element with a **Location** property.</span></span> <span data-ttu-id="2889a-140">Belirtin `Location = XXXX` burada `XXXX` bir Azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="2889a-140">Specify `Location = XXXX` where `XXXX` is an Azure region.</span></span> <span data-ttu-id="2889a-141">Ardından yeni yapılandırmasını alın.</span><span class="sxs-lookup"><span data-stu-id="2889a-141">Then import the new configuration.</span></span>

<span data-ttu-id="2889a-142">Örneğin, aşağıdaki VNET yapılandırmasını dikkate:</span><span class="sxs-lookup"><span data-stu-id="2889a-142">For example, considering the following VNET configuration:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" AffinityGroup="AzureSQLNetwork">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

<span data-ttu-id="2889a-143">Bunu Batı Avrupa'da bölgesel bir sanal ağ taşımak için yapılandırma aşağıdaki gibi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="2889a-143">To move this to a regional VNET in West Europe, change the configuration to the following:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" Location="West Europe">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

### <a name="storage-accounts"></a><span data-ttu-id="2889a-144">Depolama hesapları</span><span class="sxs-lookup"><span data-stu-id="2889a-144">Storage accounts</span></span>
<span data-ttu-id="2889a-145">Premium Storage için yapılandırılan yeni bir depolama hesabı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2889a-145">You will need to create a new storage account that is configured for Premium Storage.</span></span> <span data-ttu-id="2889a-146">DS * serisi VM kullanırken VHD'ler Premium ve standart depolama hesaplarından ekleyebilirsiniz ancak Premium depolama kullanımını tek tek VHD'ler üzerinde depolama hesabında ayarlandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2889a-146">Note that the use of Premium Storage is set at the storage account, not on individual VHDs, however when using a DS* Series VM you can attach VHD’s from Premium and Standard Storage accounts.</span></span> <span data-ttu-id="2889a-147">Premium depolama hesabına OS VHD'yi yerleştirmek istemiyorsanız bu düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2889a-147">You may consider this if you do not want to place the OS VHD on to the Premium Storage account.</span></span>

<span data-ttu-id="2889a-148">Aşağıdaki **yeni AzureStorageAccountPowerShell** "Premium_LRS" komutunu **türü** bir Premium depolama hesabı oluşturur:</span><span class="sxs-lookup"><span data-stu-id="2889a-148">The following **New-AzureStorageAccountPowerShell** command with the "Premium_LRS" **Type** creates a Premium Storage Account:</span></span>

    $newstorageaccountname = "danpremstor"
    New-AzureStorageAccount -StorageAccountName $newstorageaccountname -Location "West Europe" -Type "Premium_LRS"   

### <a name="vhds-cache-settings"></a><span data-ttu-id="2889a-149">VHD'ler önbellek ayarları</span><span class="sxs-lookup"><span data-stu-id="2889a-149">VHDs Cache Settings</span></span>
<span data-ttu-id="2889a-150">Premium depolama hesabı parçası olan diskleri oluşturma arasındaki temel fark disk önbelleği ayardır.</span><span class="sxs-lookup"><span data-stu-id="2889a-150">The main difference between creating disks that are part of a Premium Storage account is the disk cache setting.</span></span> <span data-ttu-id="2889a-151">SQL Server veri birimi, diskler için kullanmanız önerilir '**okuma önbelleği**'.</span><span class="sxs-lookup"><span data-stu-id="2889a-151">For SQL Server Data volume disks it is recommended that you use ‘**Read Caching**’.</span></span> <span data-ttu-id="2889a-152">İşlem günlük birimleri için disk önbellek ayarı ayarlanmalı '**hiçbiri**'.</span><span class="sxs-lookup"><span data-stu-id="2889a-152">For Transaction log volumes, the disk cache setting should be set to ‘**None**’.</span></span> <span data-ttu-id="2889a-153">Bu öneriler standart depolama hesapları için farklıdır.</span><span class="sxs-lookup"><span data-stu-id="2889a-153">This is different from the recommendations for Standard Storage accounts.</span></span>

<span data-ttu-id="2889a-154">Önbellek ayarını VHD'leri bağlandıktan sonra değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="2889a-154">Once the VHDs have been attached, the cache setting cannot be altered.</span></span> <span data-ttu-id="2889a-155">Ayırma ve VHD güncelleştirilmiş önbellek ayarı ile yeniden iliştirin gereksiniminiz olacaktır.</span><span class="sxs-lookup"><span data-stu-id="2889a-155">You would need to detach and reattach the VHD with an updated cache setting.</span></span>

### <a name="windows-storage-spaces"></a><span data-ttu-id="2889a-156">Windows depolama alanları</span><span class="sxs-lookup"><span data-stu-id="2889a-156">Windows storage spaces</span></span>
<span data-ttu-id="2889a-157">Kullanabileceğiniz [Windows depolama alanları](https://technet.microsoft.com/library/hh831739.aspx) önceki standart depolama ile yaptığınız gibi bu, zaten depolama alanları kullanan bir VM geçirmeye olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="2889a-157">You can use [Windows Storage Spaces](https://technet.microsoft.com/library/hh831739.aspx) as you did with previous Standard Storage, this will allow you to migrate a VM that is already utilizing Storage Spaces.</span></span> <span data-ttu-id="2889a-158">Örnekte [ek](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (adım 9 ve iletme) ayıklayın ve birden çok ekli VHD'yle bir VM'yi almak amacıyla Powershell kodu gösterir.</span><span class="sxs-lookup"><span data-stu-id="2889a-158">The example in [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (step 9 and forward) demonstrates the Powershell code to extract and import a VM with multiple attached VHDs.</span></span>

<span data-ttu-id="2889a-159">Depolama havuzları verimliliği artırmak ve gecikme süresini azaltmak için standart Azure depolama hesabıyla kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="2889a-159">Storage Pools were used with Standard Azure storage account to enhance throughput and reduce latency.</span></span> <span data-ttu-id="2889a-160">Yeni dağıtımlar için Premium depolama ile depolama havuzlarını testinde değeri bulabilirsiniz, ancak depolama kuruluma ek karmaşıklık ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2889a-160">You might find value in testing Storage Pools with Premium Storage for new deployments, but they do add additional complexity with storage setup.</span></span>

#### <a name="how-to-find-which-azure-virtual-disks-map-to-storage-pools"></a><span data-ttu-id="2889a-161">Depolama havuzları için hangi Azure sanal diskler haritanın bulma</span><span class="sxs-lookup"><span data-stu-id="2889a-161">How to find which Azure Virtual Disks map to storage pools</span></span>
<span data-ttu-id="2889a-162">Ekli VHD'ler için farklı önbellek ayarı öneriler olarak VHD'leri bir Premium depolama hesabına kopyalamak karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2889a-162">As there are different cache setting recommendations for attached VHDs, you might decide to copy the VHDs to a Premium Storage account.</span></span> <span data-ttu-id="2889a-163">Ancak, bunları yeni DS serisi VM bağladığınızda, önbellek ayarlarını değiştirme gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="2889a-163">However, when you reattach them to the new DS series VM, you might need to alter the cache settings.</span></span> <span data-ttu-id="2889a-164">Premium depolama SQL veri dosyalarını ve günlük dosyaları (yerine her ikisini de içeren tek bir VHD) için ayrı VHD'leri olduğunda önerilen önbellek ayarları uygulamak daha basittir.</span><span class="sxs-lookup"><span data-stu-id="2889a-164">It is simpler to apply the Premium Storage recommended cache settings when you have separate VHDs for the SQL Data files and log files (rather than a single VHD that contains both).</span></span>

> [!NOTE]
> <span data-ttu-id="2889a-165">SQL Server veri ve günlük dosyaları aynı birimde varsa, önbelleğe alma seçeneği, veritabanı iş yükleri için g/ç erişimi desenleri bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="2889a-165">If you have SQL Server data and log files on the same volume, the caching option you choose depends on the IO access patterns for your database workloads.</span></span> <span data-ttu-id="2889a-166">Yalnızca test hangi önbelleğe alma bu senaryo için en iyi seçenektir personeline gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="2889a-166">Only testing can demonstrate which caching option is best for this scenario.</span></span>
>
>

<span data-ttu-id="2889a-167">Windows depolama alanları, birden çok VHD bakmak gerekir hale kullanıyorsanız, ancak VHD'ler ekli tanımlamak için özgün belirli hangi havuzda böylece, daha sonra önbellek ayarları ayarlayabilirsiniz betiklerdir uygun şekilde her disk için.</span><span class="sxs-lookup"><span data-stu-id="2889a-167">However, if you are using Windows Storage Spaces which are made up of multiple VHDs you will need to look at your original scripts to identify which attached VHDs are in what specific pool, so you can then set the cache settings accordingly for each disk.</span></span>

<span data-ttu-id="2889a-168">Özgün komut dosyasını, depolama havuzuna VHD'ler eşleştiren göstermek kullanılabilir değilse, disk/depolama havuzu eşlemesini belirlemek için aşağıdaki adımları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2889a-168">If you do not have original script available to show you which VHDs map to the storage pool, you can use the following steps to determine the disk/storage pool mapping.</span></span>

<span data-ttu-id="2889a-169">Her disk için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="2889a-169">For each disk, use the following steps:</span></span>

1. <span data-ttu-id="2889a-170">VM diskleri listesini alın iliştirilmiş **Get-AzureVM** komutu:</span><span class="sxs-lookup"><span data-stu-id="2889a-170">Get list of disks attached to VM with the **Get-AzureVM** command:</span></span>

    <span data-ttu-id="2889a-171">Get-AzureVM - ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span><span class="sxs-lookup"><span data-stu-id="2889a-171">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span></span>
2. <span data-ttu-id="2889a-172">LUN ve Diskname unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2889a-172">Note the Diskname and LUN.</span></span>

    ![DisknameAndLUN][2]
3. <span data-ttu-id="2889a-174">Uzak Masaüstü VM başlatın.</span><span class="sxs-lookup"><span data-stu-id="2889a-174">Remote desktop into the VM.</span></span> <span data-ttu-id="2889a-175">Ardından **Bilgisayar Yönetimi** | **Aygıt Yöneticisi'ni** | **Disk sürücüleri**.</span><span class="sxs-lookup"><span data-stu-id="2889a-175">Then go to **Computer Management** | **Device Manager** | **Disk Drives**.</span></span> <span data-ttu-id="2889a-176">Her 'Microsoft sanal disklerin' özelliklerine bakmak</span><span class="sxs-lookup"><span data-stu-id="2889a-176">Look at the properties of each of the ‘Microsoft Virtual Disks’</span></span>

    ![VirtualDiskProperties][3]
4. <span data-ttu-id="2889a-178">LUN numarası burada VHD'yi VM'e eklerken belirttiğiniz LUN numarası başvurudur.</span><span class="sxs-lookup"><span data-stu-id="2889a-178">The LUN number here is a reference to the LUN number you specify when attaching the VHD to the VM.</span></span>
5. <span data-ttu-id="2889a-179">'Microsoft sanal diski' gitmek için **ayrıntıları** sekmesi, sonra **özelliği** listesi, Git **sürücü anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="2889a-179">For the ‘Microsoft Virtual Disk’ go to the **Details** tab, then in the **Property** list, go to **Driver Key**.</span></span> <span data-ttu-id="2889a-180">İçinde **değeri**, Not **uzaklığı**, aşağıdaki ekran görüntüsü 0002 olduğu.</span><span class="sxs-lookup"><span data-stu-id="2889a-180">In the **Value**, note the **Offset**, which is 0002 in the following screenshot.</span></span> <span data-ttu-id="2889a-181">Depolama havuzu başvuran PhysicalDisk2 0002 gösterir.</span><span class="sxs-lookup"><span data-stu-id="2889a-181">The 0002 denotes the PhysicalDisk2 that the storage pool references.</span></span>

    ![VirtualDiskPropertyDetails][4]
6. <span data-ttu-id="2889a-183">Her depolama havuzu için ilişkili diskler dökün:</span><span class="sxs-lookup"><span data-stu-id="2889a-183">For each storage pool, dump out the associated disks:</span></span>

    <span data-ttu-id="2889a-184">Get-StoragePool - FriendlyName AMS1pooldata | Get-PhysicalDisk</span><span class="sxs-lookup"><span data-stu-id="2889a-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span></span>

    ![GetStoragePool][5]

<span data-ttu-id="2889a-186">Kullanabileceğiniz artık ilişkilendirmek için bu bilgileri VHD'ler fiziksel diskleri depolama havuzları bağlı.</span><span class="sxs-lookup"><span data-stu-id="2889a-186">Now you can use this information to associate attached VHDs to Physical Disks in Storage Pools.</span></span>

<span data-ttu-id="2889a-187">Depolama ayırma ve bunları üzerinden bir Premium depolama alanına kopyalanmaya havuzlarındaki fiziksel disklere VHD'ler eşledikten sonra bunları ile doğru önbellek ayarı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2889a-187">Once you have mapped VHDs to Physical Disks in Storage Pools you can then detach and copy them over to a Premium Storage account, then attach them with the correct cache setting.</span></span> <span data-ttu-id="2889a-188">Lütfen örnekte bkz [ek](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), 8-12 arası adımları.</span><span class="sxs-lookup"><span data-stu-id="2889a-188">Please see the example in the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), steps 8 through 12.</span></span> <span data-ttu-id="2889a-189">Bu adımlar, bir VM ekli VHD disk yapılandırmasını bir CSV dosyasına ayıklamak, VHD'leri kopyalama, disk yapılandırma önbelleği ayarlarını değiştirme ve son olarak VM eklenen tüm diskler ile VM DS serisi olarak yeniden dağıtın gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="2889a-189">These steps show how to extract a VM-attached VHD disk configuration to a CSV file, copy the VHDs, alter the disk configuration cache settings, and finally redeploy the VM as a DS series VM with all the attached disks.</span></span>

### <a name="vm-storage-bandwidth-and-vhd-storage-throughput"></a><span data-ttu-id="2889a-190">VM depolama bant genişliği ve VHD depolama üretilen iş</span><span class="sxs-lookup"><span data-stu-id="2889a-190">VM storage bandwidth and VHD storage throughput</span></span>
<span data-ttu-id="2889a-191">Depolama performansı miktarı belirtilen DS * VM boyutu ve VHD boyutlarına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="2889a-191">The amount of storage performance depends on the DS* VM size specified and the VHD sizes.</span></span> <span data-ttu-id="2889a-192">VM'ler farklı kesintileri eklenebilecek VHD'ler sayısı ve en yüksek bant genişliği (MB/sn) destekleyecek sahiptir.</span><span class="sxs-lookup"><span data-stu-id="2889a-192">The VMs have different allowances for the number of VHDs that can be attached and the maximum bandwidth they will support (MB/s).</span></span> <span data-ttu-id="2889a-193">Belirli bir bant numaraları için bkz: [sanal makine ve bulut hizmeti boyutları Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2889a-193">For the specific bandwidth numbers, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="2889a-194">Daha fazla IOPS ile büyük disk boyutları elde edilir.</span><span class="sxs-lookup"><span data-stu-id="2889a-194">Increased IOPS are achieved with larger disk sizes.</span></span> <span data-ttu-id="2889a-195">Geçiş yolunuz hakkında düşünürken, düşünmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="2889a-195">You should consider this when you think about your migration path.</span></span> <span data-ttu-id="2889a-196">Ayrıntılar için [IOPS ve Disk türleri için tabloya bakın](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="2889a-196">For details, [see the table for IOPS and Disk Types](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span></span>

<span data-ttu-id="2889a-197">Son olarak, VM'ye bağlı tüm diskler için destekleyecek farklı en fazla disk bant genişlikleri sahip göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="2889a-197">Finally, consider that VMs have different maximum disk bandwidths they will support for all disks attached.</span></span> <span data-ttu-id="2889a-198">Yüksek yük altında bu VM rol boyutu için kullanılabilen en fazla disk bant genişliği saturate.</span><span class="sxs-lookup"><span data-stu-id="2889a-198">Under high load, you could saturate the maximum disk bandwidth available for that VM role size.</span></span> <span data-ttu-id="2889a-199">Örneğin bir Standard_DS14 512 MB/sn kadar destekler; Bu nedenle, üç P30 disklerinde disk bant genişliği VM saturate.</span><span class="sxs-lookup"><span data-stu-id="2889a-199">For example a Standard_DS14 will support up to 512MB/s; therefore, with three P30 disks you could saturate the disk bandwidth of the VM.</span></span> <span data-ttu-id="2889a-200">Ancak bu örnekte, üretilen iş sınırı okuma ve yazma g/ç işlemine bağlı karışımı aştı.</span><span class="sxs-lookup"><span data-stu-id="2889a-200">But in this example, the throughput limit could be exceeded depending on the mix of read and write IOs.</span></span>

## <a name="new-deployments"></a><span data-ttu-id="2889a-201">Yeni dağıtımlar</span><span class="sxs-lookup"><span data-stu-id="2889a-201">New deployments</span></span>
<span data-ttu-id="2889a-202">SQL Server Vm'lerinin Premium depolama alanına nasıl dağıtabileceğiniz sonraki iki bölümde gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="2889a-202">The next two sections demonstrate how you can deploy SQL Server VMs to Premium Storage.</span></span> <span data-ttu-id="2889a-203">Önceden belirtildiği gibi mutlaka Premium depolama OS diske yerleştirmek gerekmez.</span><span class="sxs-lookup"><span data-stu-id="2889a-203">As mentioned before, you do not necessarily need to place the OS disk onto Premium storage.</span></span> <span data-ttu-id="2889a-204">Yoğun g/ç iş yükleri üzerinde işletim sistemi VHD'yi yerleştirmek amaçlanıyorsa bu yapmayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2889a-204">You might choose to do this if you are intending to place any intensive IO workloads on the OS VHD.</span></span>

<span data-ttu-id="2889a-205">İlk örnek, var olan Azure galeri görüntüleri kullanılarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="2889a-205">The first example demonstrates utilizing existing Azure Gallery Images.</span></span> <span data-ttu-id="2889a-206">İkinci örnek var olan bir standart depolama hesabında sahip özel bir VM görüntüsü kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="2889a-206">The second example shows how to use a custom VM image that you have in an existing Standard storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="2889a-207">Bu örnekler, bölgesel bir sanal ağ zaten oluşturduğunuzu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="2889a-207">These examples assume that you have already created a Regional VNET.</span></span>
>
>

### <a name="create-a-new-vm-with-premium-storage-with-gallery-image"></a><span data-ttu-id="2889a-208">Premium depolama galeri görüntüsü ile birlikte yeni bir VM oluşturun</span><span class="sxs-lookup"><span data-stu-id="2889a-208">Create a new VM with Premium Storage with Gallery Image</span></span>
<span data-ttu-id="2889a-209">Aşağıdaki örnek, işletim sistemi VHD premium depolama üzerine yerleştirin ve Premium depolama VHD'yi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="2889a-209">The example below shows how to place the OS VHD onto premium storage and attach Premium Storage VHDs.</span></span> <span data-ttu-id="2889a-210">Ancak, aynı zamanda bir standart depolama hesabı işletim sistemi diski yerleştirin ve ardından bir Premium depolama hesabında bulunan VHD ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2889a-210">However, you can also place the OS disk in a Standard Storage account and then attach VHDs that reside in a Premium Storage account.</span></span> <span data-ttu-id="2889a-211">Her iki senaryoyu gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="2889a-211">Both scenarios are demonstrated.</span></span>

    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Set up subscription
    Set-AzureSubscription -SubscriptionName $mysubscription
    Select-AzureSubscription -SubscriptionName $mysubscription -Current  

#### <a name="step-1-create-a-premium-storage-account"></a><span data-ttu-id="2889a-212">1. adım: bir Premium depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2889a-212">Step 1: Create a Premium Storage Account</span></span>
    #Create Premium Storage account, note Type
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  


#### <a name="step-2-create-a-new-cloud-service"></a><span data-ttu-id="2889a-213">2. adım: yeni bir bulut hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="2889a-213">Step 2: Create a New Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-reserve-a-cloud-service-vip-optional"></a><span data-ttu-id="2889a-214">3. adım: (isteğe bağlı) bir bulut hizmeti VIP ayırma</span><span class="sxs-lookup"><span data-stu-id="2889a-214">Step 3: Reserve a Cloud Service VIP (Optional)</span></span>
    #check exisitng reserved VIP
    Get-AzureReservedIP

    $reservedVIPName = “sqlcloudVIP”
    New-AzureReservedIP –ReservedIPName $reservedVIPName –Label $reservedVIPName –Location $location

#### <a name="step-4-create-a-vm-container"></a><span data-ttu-id="2889a-215">4. adım: bir VM kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2889a-215">Step 4: Create a VM Container</span></span>
    #Generate storage keys for later
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    ##Generate storage acc contexts
    $xioContext = New-AzureStorageContext –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary   

    #Create container
    $containerName = 'vhds'
    New-AzureStorageContainer -Name $containerName -Context $xioContext

#### <a name="step-5-placing-os-vhd-on-standard-or-premium-storage"></a><span data-ttu-id="2889a-216">5. adım: İşletim sistemi VHD standart veya Premium Storage yerleştirme</span><span class="sxs-lookup"><span data-stu-id="2889a-216">Step 5: Placing OS VHD on Standard or Premium Storage</span></span>
    #NOTE: Set up subscription and default storage account which will be used to place the OS VHD in

    #If you want to place the OS VHD Premium Storage Account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $newxiostorageaccountname  

    #If you wanted to place the OS VHD Standard Storage Account but attach Premium Storage VHDs then you would run this instead:
    $standardstorageaccountname = "danstdams"

    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $standardstorageaccountname

#### <a name="step-6-create-vm"></a><span data-ttu-id="2889a-217">6. adım: VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="2889a-217">Step 6: Create VM</span></span>
    #Get list of available SQL Server Images from the Azure Image Gallery.
    $galleryImage = Get-AzureVMImage | where-object {$_.ImageName -like "*SQL*2014*Enterprise*"}
    $image = $galleryImage.ImageName

    #Set up Machine Specific Information
    $vmName = "dsDan1"
    $vnet = "dansvnetwesteur"
    $subnet = "SQL"
    $ipaddr = "192.168.0.8"

    #Remember to change to DS series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "mycomplexpwd4*"

    #Create VM Config
    $vmConfigsl = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $image  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Add Data and Log Disks to VM Config
    #Note the size specified ‘-DiskSizeInGB 1023’, this will attach 2 x P30 Premium Storage Disk Type
    #Utilising the Premium Storage enabled Storage account

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


### <a name="create-a-new-vm-to-use-premium-storage-with-a-custom-image"></a><span data-ttu-id="2889a-218">Premium depolama ile özel bir görüntü kullanmak için yeni bir VM oluşturun</span><span class="sxs-lookup"><span data-stu-id="2889a-218">Create a new VM to use Premium Storage with a custom image</span></span>
<span data-ttu-id="2889a-219">Bu senaryo, bir standart depolama hesabında bulunan var olan özelleştirilmiş görüntüleri sahip olduğu gösterir.</span><span class="sxs-lookup"><span data-stu-id="2889a-219">This scenario demonstrates where you have existing customized images that reside in a Standard Storage account.</span></span> <span data-ttu-id="2889a-220">Premium depolama OS VHD eklemek istediğiniz belirtildiği gibi standart depolama hesabı, var olan görüntüyü kopyalamak ve kullanılabilmesi için önce bunları Premium depolama alanına aktarmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="2889a-220">As mentioned if you want to place the OS VHD on Premium Storage you will need to copy the image that exists in the Standard Storage account and transfer them to a Premium Storage before it can be used.</span></span> <span data-ttu-id="2889a-221">Bir görüntü şirket içi, yapabilecekleriniz varsa da doğrudan Premium depolama hesabına kopyalamak için bu yöntemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="2889a-221">If you have an image on-premises, you can also use this method to copy that directly to the Premium Storage account.</span></span>

#### <a name="step-1-create-storage-account"></a><span data-ttu-id="2889a-222">Adım 1: Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2889a-222">Step 1: Create Storage Account</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Standard Storage account
    $origstorageaccountname = "danstdams"

#### <a name="step-2-create-cloud-service"></a><span data-ttu-id="2889a-223">2. adım, bulut hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="2889a-223">Step 2 Create Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-use-existing-image"></a><span data-ttu-id="2889a-224">3. adım: Mevcut görüntü kullanın</span><span class="sxs-lookup"><span data-stu-id="2889a-224">Step 3: Use existing image</span></span>
<span data-ttu-id="2889a-225">Varolan bir görüntü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2889a-225">You can use an existing image.</span></span> <span data-ttu-id="2889a-226">Veya, [var olan bir makine görüntüsünü ele](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2889a-226">Or, you can [take an image of an existing machine](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="2889a-227">Görüntü, DS * makinenin olması gerekmez. makine unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2889a-227">Note the machine you image does not have to be DS* machine.</span></span> <span data-ttu-id="2889a-228">Görüntü olduktan sonra aşağıdaki adımlar, Premium Storage hesabıyla kopyalamak nasıl gösterir. **başlangıç AzureStorageBlobCopy** PowerShell komutunu.</span><span class="sxs-lookup"><span data-stu-id="2889a-228">Once you have the image, the following steps show how to copy it to the Premium Storage account with the **Start-AzureStorageBlobCopy** PowerShell commandlet.</span></span>

    #Get storage account keys:
    #Standard Storage account
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    #Premium Storage account
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Set up contexts for the storage accounts:
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $destContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

#### <a name="step-4-copy-blob-between-storage-accounts"></a><span data-ttu-id="2889a-229">4. adım: Kopyalama Blob Depolama hesapları arasında</span><span class="sxs-lookup"><span data-stu-id="2889a-229">Step 4: Copy Blob between Storage Accounts</span></span>
    #Get Image VHD
    $myImageVHD = "dansoldonorsql2k14-os-2015-04-15.vhd"
    $containerName = 'vhds'

    #Copy Blob between accounts
    $blob = Start-AzureStorageBlobCopy -SrcBlob $myImageVHD -SrcContainer $containerName `
    -DestContainer vhds -Destblob "prem-$myImageVHD" `
    -Context $origContext -DestContext $destContext  

#### <a name="step-5-regularly-check-copy-status"></a><span data-ttu-id="2889a-230">5. adım: Kopyalama durumu düzenli olarak kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="2889a-230">Step 5: Regularly check copy status:</span></span>
    $blob | Get-AzureStorageBlobCopyState

#### <a name="step-6-add-image-disk-to-azure-disk-repository-in-subscription"></a><span data-ttu-id="2889a-231">6. adım: Azure disk abonelik deposunda görüntü disk ekleyin</span><span class="sxs-lookup"><span data-stu-id="2889a-231">Step 6: Add Image disk to Azure disk Repository in Subscription</span></span>
    $imageMediaLocation = $destContext.BlobEndPoint+"/"+$myImageVHD
    $newimageName = "prem"+"dansoldonorsql2k14"

    Add-AzureVMImage -ImageName $newimageName -MediaLocation $imageMediaLocation

> [!NOTE]
> <span data-ttu-id="2889a-232">Başarı durum raporu olsa da, bir disk kira hatası hala alabilir bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2889a-232">You may find that even though the status reports as success, you could still get a disk lease error.</span></span> <span data-ttu-id="2889a-233">Bu durumda, yaklaşık 10 dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="2889a-233">In this case, wait about 10 minutes.</span></span>
>
>

#### <a name="step-7--build-the-vm"></a><span data-ttu-id="2889a-234">7. adım: VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="2889a-234">Step 7:  Build the VM</span></span>
<span data-ttu-id="2889a-235">Burada görüntünüzü ve iki Premium depolama VHD'leri VM oluşturuyorsanız:</span><span class="sxs-lookup"><span data-stu-id="2889a-235">Here you are building the VM from your image and attaching two Premium Storage VHDs:</span></span>

    $newimageName = "prem"+"dansoldonorsql2k14"
    #Set up Machine Specific Information
    $vmName = "dansolchild"
    $vnet = "westeur"
    $subnet = "Clients"
    $ipaddr = "192.168.0.41"

    #This will need to be a new cloud service
    $destcloudsvc = "danregsvcamsxio2"

    #Use to DS Series VM
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

## <a name="existing-deployments-that-do-not-use-always-on-availability-groups"></a><span data-ttu-id="2889a-236">Always On kullanılabilirlik grupları kullanmayın var olan dağıtımlar</span><span class="sxs-lookup"><span data-stu-id="2889a-236">Existing deployments that do not use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="2889a-237">Var olan dağıtımlar için önce bkz [Önkoşullar](#prerequisites-for-premium-storage) bölümüne.</span><span class="sxs-lookup"><span data-stu-id="2889a-237">For existing deployments, first see the [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="2889a-238">Always On kullanılabilirlik grupları hem de kullanmayın SQL Server dağıtımları için farklı noktalar vardır.</span><span class="sxs-lookup"><span data-stu-id="2889a-238">There are different considerations for SQL Server deployments that do not use Always On Availability Groups and those that do.</span></span> <span data-ttu-id="2889a-239">Her zaman açık kullanmıyorsanız ve var olan bir tek başına SQL Server yüklüyse, yeni bir bulut hizmeti ve depolama hesabı kullanarak Premium depolama alanına yükseltebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2889a-239">If you are not using Always On and have an existing standalone SQL Server, you can upgrade to Premium Storage by using a new cloud service and storage account.</span></span> <span data-ttu-id="2889a-240">Aşağıdaki seçenekleri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="2889a-240">Consider the following options:</span></span>

* <span data-ttu-id="2889a-241">**Yeni bir SQL Server VM oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="2889a-241">**Create a new SQL Server VM**.</span></span> <span data-ttu-id="2889a-242">Yeni dağıtımlarda belirtildiği gibi yeni bir SQL Server bir Premium depolama hesabını kullanan VM oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2889a-242">You can create a new SQL Server VM that uses a Premium Storage account, as documented in New Deployments.</span></span> <span data-ttu-id="2889a-243">Ardından yedekleme ve SQL Server yapılandırma ve kullanıcı veritabanlarını geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2889a-243">Then backup and restore your SQL Server configuration and user databases.</span></span> <span data-ttu-id="2889a-244">Uygulama dahili veya harici erişiliyor, yeni SQL Server başvurmak için güncelleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2889a-244">The application will need to be updated to reference the new SQL Server if it is being accessed internally or externally.</span></span> <span data-ttu-id="2889a-245">Yan yana (SxS) SQL Server Geçiş yaptığınız gibi 'dışı db' tüm nesneleri kopyalamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="2889a-245">You would need to copy all ‘out of db’ objects as if you were doing a Side by Side (SxS) SQL Server migration.</span></span> <span data-ttu-id="2889a-246">Bu, oturum açma bilgileri, sertifikalar ve bağlantılı sunucular gibi nesneleri içerir.</span><span class="sxs-lookup"><span data-stu-id="2889a-246">This includes objects such as logins, certificates, and linked servers.</span></span>
* <span data-ttu-id="2889a-247">**Mevcut bir SQL Server VM'yi geçirme**.</span><span class="sxs-lookup"><span data-stu-id="2889a-247">**Migrate an existing SQL Server VM**.</span></span> <span data-ttu-id="2889a-248">Bu SQL Server VM çevrimdışı duruma almayı gerektirir ve ardından yeni bir bulut hizmeti aktarma, tüm bağlı VHD Premium Storage hesabına kopyalama içerir.</span><span class="sxs-lookup"><span data-stu-id="2889a-248">This will require taking the SQL Server VM offline, then transferring it to a new cloud service, which includes copying all of its attached VHDs to the Premium Storage account.</span></span> <span data-ttu-id="2889a-249">VM çevrimiçi olduğunda, uygulamanın önce sunucu ana bilgisayar adı olarak başvurur.</span><span class="sxs-lookup"><span data-stu-id="2889a-249">When the VM comes online, the application will reference the server host name as before.</span></span> <span data-ttu-id="2889a-250">Performans özellikleri mevcut disk boyutunu etkiler unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2889a-250">Be aware that the size of the existing disk will affect the performance characteristics.</span></span> <span data-ttu-id="2889a-251">Örneğin, 400 GB disk için bir P20 yuvarlanan.</span><span class="sxs-lookup"><span data-stu-id="2889a-251">For example, a 400 GB disk gets rounded up to a P20.</span></span> <span data-ttu-id="2889a-252">DS serisi VM olarak VM oluşturun ve Premium depolama VHD'yi ihtiyaç duyduğunuz boyutu/performans belirtimi, bu disk performansı gerektirmez biliyorsanız.</span><span class="sxs-lookup"><span data-stu-id="2889a-252">If you know that you do not require that disk performance, then you could recreate the VM as a DS Series VM, and attach Premium Storage VHDs of the size/performance specification you require.</span></span> <span data-ttu-id="2889a-253">Ardından detach ve SQL DB dosyaları yeniden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2889a-253">Then you could detach and reattach the SQL DB files.</span></span>

> [!NOTE]
> <span data-ttu-id="2889a-254">Boyutuna bağlı olarak boyutu bilincinde olmanız gereken VHD diskleri kopyalama Premium depolama diskini türüne anlamına gelir, bunların içine kalan, bu disk performans belirtimi belirler.</span><span class="sxs-lookup"><span data-stu-id="2889a-254">When copying the VHD disks you should be aware of the size, depending on the size will mean what Premium Storage Disk type they fall into, this determines disk performance specification.</span></span> <span data-ttu-id="2889a-255">Round Azure olacak kadar yakın disk boyutu, 400 GB disk varsa, bu bir P20 yuvarlanır şekilde.</span><span class="sxs-lookup"><span data-stu-id="2889a-255">Azure will round up to the nearest disk size, so if you have a 400GB disk, this will be rounded up to a P20.</span></span> <span data-ttu-id="2889a-256">Varolan GÇ gereksinimlerinize OS VHD'nin bağlı olarak, bu bir Premium depolama hesabına geçirmek gerekmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="2889a-256">Depending on your existing IO requirements of the OS VHD, you might not need to migrate this to a Premium Storage account.</span></span>
>
>

<span data-ttu-id="2889a-257">SQL Server'ınızdaki dışarıdan erişiliyorsa, bulut hizmet VIP'de değiştirir.</span><span class="sxs-lookup"><span data-stu-id="2889a-257">If your SQL Server is accessed externally, then the cloud service VIP will change.</span></span> <span data-ttu-id="2889a-258">Güncelleştirme uç noktaları, ACL'ler ve DNS ayarlarını gerekir.</span><span class="sxs-lookup"><span data-stu-id="2889a-258">You will also have to update end points, ACLs, and DNS settings.</span></span>

## <a name="existing-deployments-that-use-always-on-availability-groups"></a><span data-ttu-id="2889a-259">Always On kullanılabilirlik grupları kullanan var olan dağıtımlar</span><span class="sxs-lookup"><span data-stu-id="2889a-259">Existing deployments that use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="2889a-260">Var olan dağıtımlar için önce bkz [Önkoşullar](#prerequisites-for-premium-storage) bölümüne.</span><span class="sxs-lookup"><span data-stu-id="2889a-260">For existing deployments, first see the [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="2889a-261">Başlangıçta bu bölümde biz nasıl her zaman açık Azure ağ ile etkileşim sırasında arar.</span><span class="sxs-lookup"><span data-stu-id="2889a-261">Initially in this section we will look at how Always On interacts with Azure Networking.</span></span> <span data-ttu-id="2889a-262">Biz sonra geçişleri iki senaryo için aşağı çalışmamasına neden olur: Burada miktar kapalı kalma süresi izin geçişler ve burada gerekir ulaşmanıza en düşük kapalı kalma geçişleri.</span><span class="sxs-lookup"><span data-stu-id="2889a-262">We will then break down migrations in to two scenarios: migrations where some downtime can be tolerated and migrations where you must achieve minimal downtime.</span></span>

<span data-ttu-id="2889a-263">Bir dinleyici sanal bir DNS adı bir veya daha fazla SQL Server'lar arasında paylaşılan bir IP adresi ile birlikte kaydeden şirket içi SQL Server Always On kullanılabilirlik grupları kullanın.</span><span class="sxs-lookup"><span data-stu-id="2889a-263">On-premises SQL Server Always On Availability Groups use a Listener on-premises that registers a virtual DNS name along with an IP address that is shared between one or more SQL Servers.</span></span> <span data-ttu-id="2889a-264">İstemciler bağlandığında birincil SQL Server dinleyici IP üzerinden yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="2889a-264">When clients connect they are routed through the listener IP to the Primary SQL Server.</span></span> <span data-ttu-id="2889a-265">Bu, o anda üzerinde her zaman IP kaynağına sahip sunucusudur.</span><span class="sxs-lookup"><span data-stu-id="2889a-265">This is the server that owns the Always On IP resource at that time.</span></span>

![Üzerinde DeploymentsUseAlways][6]

<span data-ttu-id="2889a-267">Microsoft Azure VM'de bir NIC atanan tek bir IP adresi olabilir, bu nedenle aynı şirket olarak Soyutlama Katmanı elde etmek için Azure iç/dış yük dengeleyici (ILB/ELB) atanan IP adresini kullanır.</span><span class="sxs-lookup"><span data-stu-id="2889a-267">In Microsoft Azure you can have only one IP address assigned to a NIC on the VM, so in order to achieve the same layer of abstraction as on-premises, Azure utilizes the IP address that is assigned to the Internal/External Load Balancers (ILB/ELB).</span></span> <span data-ttu-id="2889a-268">Sunucular arasında paylaşılan IP kaynağı aynı IP ILB/ELB olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="2889a-268">The IP resource that is shared between the servers is set to the same IP as the ILB/ELB.</span></span> <span data-ttu-id="2889a-269">Bu DNS yayımlanır ve istemci trafiğini birincil SQL Server çoğaltma ILB/ELB geçirilir.</span><span class="sxs-lookup"><span data-stu-id="2889a-269">This is published in the DNS, and client traffic is passed through the ILB/ELB to the Primary SQL Server replica.</span></span> <span data-ttu-id="2889a-270">ILB/ELB üzerinde her zaman IP kaynağı araştırma araştırmalar kullandığından SQL sunucusu olan birincil bilir.</span><span class="sxs-lookup"><span data-stu-id="2889a-270">The ILB/ELB knows which SQL Server is primary since it uses probes to probe the Always On IP resource.</span></span> <span data-ttu-id="2889a-271">Önceki örnekte, ELB/ILB tarafından başvurulan bir uç nokta sahip her bir düğüm araştırmaları, hangisi yanıt birincil SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2889a-271">In the previous example, it probes each node that has an endpoint referenced by the ELB/ILB, whichever responds is the Primary SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="2889a-272">ILB ve ELB her ikisi de belirli Azure bulut hizmeti için atanmış olan, bu nedenle tüm Azure bulut geçişte büyük olasılıkla yük dengeleyici IP değiştirecek anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="2889a-272">The ILB and ELB are both assigned to a particular Azure cloud service, therefore any cloud migration in Azure will most likely mean that the Load Balancer IP will change.</span></span>
>
>

### <a name="migrating-always-on-deployments-that-can-allow-some-downtime"></a><span data-ttu-id="2889a-273">Miktar kapalı kalma süresi sağlayan geçirme her zaman açık dağıtımları</span><span class="sxs-lookup"><span data-stu-id="2889a-273">Migrating Always On deployments that can allow some downtime</span></span>
<span data-ttu-id="2889a-274">Bazı kesintiler izin her zaman açık dağıtımları geçirmek için iki strateji vardır:</span><span class="sxs-lookup"><span data-stu-id="2889a-274">There are two strategies to migrate Always On deployments that allow for some downtime:</span></span>

1. <span data-ttu-id="2889a-275">**Daha fazla ikincil çoğaltmaları mevcut her zaman üzerinde kümeye Ekle**</span><span class="sxs-lookup"><span data-stu-id="2889a-275">**Add more secondary replicas to an existing Always On Cluster**</span></span>
2. <span data-ttu-id="2889a-276">**Yeni bir her zaman üzerinde kümeye geçirme**</span><span class="sxs-lookup"><span data-stu-id="2889a-276">**Migrate to a new Always On Cluster**</span></span>

#### <a name="1-add-more-secondary-replicas-to-an-existing-always-on-cluster"></a><span data-ttu-id="2889a-277">1. Daha fazla ikincil çoğaltmaları mevcut her zaman üzerinde kümeye Ekle</span><span class="sxs-lookup"><span data-stu-id="2889a-277">1. Add more Secondary Replicas to an Existing Always On Cluster</span></span>
<span data-ttu-id="2889a-278">Her zaman üzerindeki kullanılabilirlik grubu için daha fazla ikincil kopya eklemek için bir strateji kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2889a-278">One strategy is to add more secondaries to the Always On Availability Group.</span></span> <span data-ttu-id="2889a-279">Bunları yeni bir bulut hizmeti eklemek ve Yeni Yük Dengeleyici IP dinleyicisi güncelleştirmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="2889a-279">You need to add these into a new cloud service and update the listener with the new load balancer IP.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="2889a-280">Kapalı kalma süresi noktalar:</span><span class="sxs-lookup"><span data-stu-id="2889a-280">Points of downtime:</span></span>
* <span data-ttu-id="2889a-281">Küme doğrulama.</span><span class="sxs-lookup"><span data-stu-id="2889a-281">Cluster Validation.</span></span>
* <span data-ttu-id="2889a-282">Her zaman açık yük test etme için yeni ikincil öğe.</span><span class="sxs-lookup"><span data-stu-id="2889a-282">Testing Always On failovers for New Secondaries.</span></span>

<span data-ttu-id="2889a-283">VM içindeki Windows depolama havuzu için daha yüksek g/ç işleme kullanıyorsanız, ardından bu tam bir küme doğrulama sırasında çevrimdışına alınır.</span><span class="sxs-lookup"><span data-stu-id="2889a-283">If you are using Windows Storage Pools within the VM for higher IO throughput, then these will be taken offline during a Full Cluster Validation.</span></span> <span data-ttu-id="2889a-284">Kümeye düğüm eklemek için doğrulama testi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="2889a-284">The validation test is required when you add nodes to the cluster.</span></span> <span data-ttu-id="2889a-285">Bu ne kadar bu devam, yaklaşık bir saat almak için temsili bir test ortamında test etmeniz gerekir böylece testi çalıştırmak için geçen süre farklılık gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="2889a-285">The time it takes to run the test can vary, so you should test this in your representative test environment to get an approximate time of how long this will take.</span></span>

<span data-ttu-id="2889a-286">Burada el ile yük devretme ve test chaos beklendiği gibi her zaman üzerinde yüksek kullanılabilirlik işlevleri sağlamak için yeni eklenen düğümlerine gerçekleştirebileceğiniz zaman hazırlamanız.</span><span class="sxs-lookup"><span data-stu-id="2889a-286">You should provision time where you can perform manual failover and chaos testing on the newly added nodes to ensure Always On High Availability functions as expected.</span></span>

![DeploymentUseAlways On2][7]

> [!NOTE]
> <span data-ttu-id="2889a-288">Depolama havuzlarını kullanıldığı SQL Server'ın tüm örneklerini durması gerektiğini doğrulama çalıştırılmadan önce.</span><span class="sxs-lookup"><span data-stu-id="2889a-288">You should stop all instances of SQL Server where the Storage Pools are used before the Validation runs.</span></span>
>
> ##### <a name="high-level-steps"></a><span data-ttu-id="2889a-289">Üst düzey adımlar</span><span class="sxs-lookup"><span data-stu-id="2889a-289">High-level steps</span></span>
>

1. <span data-ttu-id="2889a-290">İki yeni SQL sunucusuna bağlı Premium depolama ile yeni bulut hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2889a-290">Create two new SQL Servers in new cloud service with attached Premium Storage.</span></span>
2. <span data-ttu-id="2889a-291">TAM yedeklemeler kopyalayın ve geri yükleme ile **NORECOVERY**.</span><span class="sxs-lookup"><span data-stu-id="2889a-291">Copy over FULL backups and restore with **NORECOVERY**.</span></span>
3. <span data-ttu-id="2889a-292">'Dışında kullanıcı DB' oturumları vb. gibi bağımlı nesnelere kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="2889a-292">Copy over ‘out of user DB’ dependent objects, such as logins etc.</span></span>
4. <span data-ttu-id="2889a-293">Yeni bir yeni iç yük dengeleyici'nı (ILB) oluşturun veya bir dış yük dengeleyici (ELB) kullanın ve ardından her iki yeni düğümde yük dengeli uç noktaları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2889a-293">Create new a new Internal Load Balancer (ILB) or use an External Load Balancer (ELB), and then set up Load Balanced Endpoints on both new nodes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2889a-294">Devam etmeden önce tüm düğümleri doğru uç nokta yapılandırması sahip denetleyin</span><span class="sxs-lookup"><span data-stu-id="2889a-294">Check all Nodes have the correct Endpoint configuration before you continue</span></span>
   >
   >
5. <span data-ttu-id="2889a-295">SQL Server kullanıcı/uygulama erişimi (depolama havuzlarını kullanıyorsanız) durdurun.</span><span class="sxs-lookup"><span data-stu-id="2889a-295">Stop User/Application Access to the SQL Server (if using Storage Pools).</span></span>
6. <span data-ttu-id="2889a-296">SQL Server motoru Hizmetleri tüm düğümler üzerinde (depolama havuzlarını kullanıyorsanız) durdurun.</span><span class="sxs-lookup"><span data-stu-id="2889a-296">Stop SQL Server Engine Services on All Nodes (if using Storage Pools).</span></span>
7. <span data-ttu-id="2889a-297">Küme ve tam doğrulama çalıştırmak için yeni düğümler ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2889a-297">Add new Nodes to cluster and run full validation.</span></span>
8. <span data-ttu-id="2889a-298">Doğrulama başarılı olduktan sonra tüm SQL Server hizmetlerini başlatın.</span><span class="sxs-lookup"><span data-stu-id="2889a-298">Once Validation is successful, start all SQL Server Services.</span></span>
9. <span data-ttu-id="2889a-299">İşlem günlüklerini yedekleme ve kullanıcı veritabanlarını geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2889a-299">Backup Transaction logs, and restore user databases.</span></span>
10. <span data-ttu-id="2889a-300">Yeni düğümler her zaman üzerinde kullanılabilirlik grubuna ekleyin ve çoğaltma içine yerleştirin **zaman uyumlu**.</span><span class="sxs-lookup"><span data-stu-id="2889a-300">Add new nodes into the Always On Availability Group and place replication into **Synchronous**.</span></span>
11. <span data-ttu-id="2889a-301">Çok siteli örnekte dayalı her zaman açık olan yeni bulut hizmeti ILB/ELB PowerShell aracılığıyla IP adresi kaynağı ekleyin [ek](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="2889a-301">Add the IP address resource of the new Cloud Service ILB/ELB through PowerShell for Always On based on the Multi-site example in the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span> <span data-ttu-id="2889a-302">Windows Kümelemesi içinde ayarlamak **olası sahipler** , **IP adresi** eski yeni düğümler için kaynak.</span><span class="sxs-lookup"><span data-stu-id="2889a-302">In Windows clustering, set the **Possible owners** of the **IP Address** resource to the new nodes old.</span></span> <span data-ttu-id="2889a-303">'Ekleme IP adresi kaynağı aynı alt ağda bulunan' bölümüne bakın [ek](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="2889a-303">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
12. <span data-ttu-id="2889a-304">Yeni düğümlerinden biri için yük devretme.</span><span class="sxs-lookup"><span data-stu-id="2889a-304">Failover to one of the new nodes.</span></span>
13. <span data-ttu-id="2889a-305">Yeni düğümler otomatik yük devretme iş ortakları ve test yük devretme olun.</span><span class="sxs-lookup"><span data-stu-id="2889a-305">Make the new nodes Auto Failover Partners and test failovers.</span></span>
14. <span data-ttu-id="2889a-306">Özgün düğüm kullanılabilirlik grubundan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2889a-306">Remove original nodes from Availability Group.</span></span>

##### <a name="advantages"></a><span data-ttu-id="2889a-307">Avantajları</span><span class="sxs-lookup"><span data-stu-id="2889a-307">Advantages</span></span>
* <span data-ttu-id="2889a-308">Yeni SQL sunucuları olabilir (SQL Server ve uygulama) için her zaman açık eklenmeden önce test.</span><span class="sxs-lookup"><span data-stu-id="2889a-308">New SQL Servers can be tested (SQL Server and Application) before they are added to Always On.</span></span>
* <span data-ttu-id="2889a-309">VM boyutunu değiştirin ve depolama tam gereksinimlerinizi özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2889a-309">You can change the VM size and customize the storage to your exact requirements.</span></span> <span data-ttu-id="2889a-310">Ancak, tüm SQL dosya yolları aynı tutmak yararlı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="2889a-310">However, it would be beneficial to keep all the SQL file paths the same.</span></span>
* <span data-ttu-id="2889a-311">İkincil çoğaltmaları DB yedeklemeleri aktarımını başladığında kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2889a-311">You can control when the transfer of the DB backups to the Secondary Replicas are started.</span></span> <span data-ttu-id="2889a-312">Bu Azure kullanmaktan farklıdır **başlangıç AzureStorageBlobCopy** komutunu, zaman uyumsuz bir kopya olduğundan VHD'ler, kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="2889a-312">This differs from using Azure **Start-AzureStorageBlobCopy** commandlet to copy VHDs, because that is an asynchronous copy.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="2889a-313">Olumsuz yönleri</span><span class="sxs-lookup"><span data-stu-id="2889a-313">Disadvantages</span></span>
* <span data-ttu-id="2889a-314">Windows depolama havuzlarını kullanırken var. küme kapalı kalma süresi yeni ek düğüm için tam küme doğrulama sırasında</span><span class="sxs-lookup"><span data-stu-id="2889a-314">When using Windows Storage Pools, there is Cluster downtime during the Full Cluster Validation for the new additional nodes.</span></span>
* <span data-ttu-id="2889a-315">SQL Server sürümü ve ikincil çoğaltmaları varolan sayısına bağlı olarak mevcut ikinciller kaldırmadan daha fazla ikincil çoğaltmaları eklemeniz mümkün olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="2889a-315">Depending on the SQL Server Version and the existing number of secondary replicas, you might not be able to add more secondary replicas without removing existing secondaries.</span></span>
* <span data-ttu-id="2889a-316">İkincil kopya ayarı uzun SQL veri aktarımı zamandan olabilir.</span><span class="sxs-lookup"><span data-stu-id="2889a-316">There could be long SQL data transfer time while setting up the secondaries.</span></span>
* <span data-ttu-id="2889a-317">Yoktur ek maliyet geçiş sırasında paralel olarak çalışan yeni makineler varken.</span><span class="sxs-lookup"><span data-stu-id="2889a-317">There is additional cost during migration while you have new machines running in parallel.</span></span>

#### <a name="2-migrate-to-a-new-always-on-cluster"></a><span data-ttu-id="2889a-318">2. Yeni bir her zaman üzerinde kümeye geçirme</span><span class="sxs-lookup"><span data-stu-id="2889a-318">2. Migrate to a new Always On Cluster</span></span>
<span data-ttu-id="2889a-319">Başka bir yepyeni her zaman üzerinde Küme yepyeni düğümleriyle yeni bulut hizmeti oluşturmak ve kullanmak için istemcileri yeniden yönlendirmek için stratejidir.</span><span class="sxs-lookup"><span data-stu-id="2889a-319">Another strategy is to create a brand new Always On Cluster with brand new nodes in new cloud service and then redirect the clients to use it.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="2889a-320">Kapalı kalma süresi noktaları</span><span class="sxs-lookup"><span data-stu-id="2889a-320">Points of downtime</span></span>
<span data-ttu-id="2889a-321">Uygulamaların ve kullanıcıların yeni her zaman açık dinleyici için aktardığınızda kapalı kalma süresi yok.</span><span class="sxs-lookup"><span data-stu-id="2889a-321">There is downtime when you transfer applications and users to the new Always On listener.</span></span> <span data-ttu-id="2889a-322">Kapalı kalma süresi bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="2889a-322">The downtime depends on:</span></span>

* <span data-ttu-id="2889a-323">Son işlem günlüğü yedeklemeleri yeni sunucularda veritabanlarını geri yüklemek için geçen süre.</span><span class="sxs-lookup"><span data-stu-id="2889a-323">The time taken to restore final transaction log backups to databases on new servers.</span></span>
* <span data-ttu-id="2889a-324">Her zaman açık dinleyici kullanmak için istemci uygulamaları güncelleştirmek için geçen süre.</span><span class="sxs-lookup"><span data-stu-id="2889a-324">The time taken to update client applications to use new Always On listener.</span></span>

##### <a name="advantages"></a><span data-ttu-id="2889a-325">Avantajları</span><span class="sxs-lookup"><span data-stu-id="2889a-325">Advantages</span></span>
* <span data-ttu-id="2889a-326">SQL Server, gerçek bir üretim ortamına sınayabilirsiniz ve işletim sistemi derleme değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="2889a-326">You can test the actual production environment, SQL Server, and OS build changes.</span></span>
* <span data-ttu-id="2889a-327">Depolama özelleştirmek ve potansiyel olarak VM boyutunu azaltmak için seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="2889a-327">You have the option to customize the storage and to potentially reduce size of VM.</span></span> <span data-ttu-id="2889a-328">Bu maliyet azalmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="2889a-328">This could result in cost reduction.</span></span>
* <span data-ttu-id="2889a-329">Bu işlem sırasında SQL Server yapı veya sürüm güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2889a-329">You can update your SQL Server build or version during this process.</span></span> <span data-ttu-id="2889a-330">Ayrıca, işletim sistemi yükseltme yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2889a-330">You can also upgrade the Operating System.</span></span>
* <span data-ttu-id="2889a-331">Önceki her zaman üzerinde Küme düz geri alma hedef olarak davranamaz.</span><span class="sxs-lookup"><span data-stu-id="2889a-331">The previous Always On Cluster can act as a solid rollback target.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="2889a-332">Olumsuz yönleri</span><span class="sxs-lookup"><span data-stu-id="2889a-332">Disadvantages</span></span>
* <span data-ttu-id="2889a-333">Eşzamanlı olarak çalıştıran her iki her zaman açık kümeler istiyorsanız dinleyicisi DNS adını değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2889a-333">You need to change the DNS name of the listener if you want both Always On clusters running simultaneously.</span></span> <span data-ttu-id="2889a-334">Bu, istemci uygulama dizeleri yeni dinleyici adı yansıtmalıdır gibi yönetim ek yükü geçişi sırasında ekler.</span><span class="sxs-lookup"><span data-stu-id="2889a-334">This adds administration overhead during the migration as client application strings must reflect the new Listener name.</span></span>
* <span data-ttu-id="2889a-335">Bunları olabildiğince geçişten önce son eşitleme gereksinimlerini en aza indirmek mümkün olduğunca yakın tutmak için iki ortam arasında eşitleme mekanizması uygulamalıdır.</span><span class="sxs-lookup"><span data-stu-id="2889a-335">You must implement a synchronization mechanism between the two environments to keep them as close as possible to minimize the final synchronization requirements before migration.</span></span>
* <span data-ttu-id="2889a-336">Var. çalıştıran yeni ortam varken maliyet geçiş sırasında eklenir.</span><span class="sxs-lookup"><span data-stu-id="2889a-336">There is added cost during migration while you have the new environment running.</span></span>

### <a name="migrating-always-on-deployments-for-minimal-downtime"></a><span data-ttu-id="2889a-337">Geçirme her zaman şirket dağıtımları için en az kapalı kalma süresi</span><span class="sxs-lookup"><span data-stu-id="2889a-337">Migrating Always On Deployments for minimal downtime</span></span>
<span data-ttu-id="2889a-338">En düşük kapalı kalma için her zaman açık geçirme dağıtımlar için iki strateji vardır:</span><span class="sxs-lookup"><span data-stu-id="2889a-338">There are two strategies for migrating Always On deployments for minimal downtime:</span></span>

1. <span data-ttu-id="2889a-339">**Var olan bir ikincil kullanma: tek siteli**</span><span class="sxs-lookup"><span data-stu-id="2889a-339">**Utilize an Existing Secondary: Single-Site**</span></span>
2. <span data-ttu-id="2889a-340">**Var olan ikincil çoğaltmalar kullanma: çok siteli**</span><span class="sxs-lookup"><span data-stu-id="2889a-340">**Utilize Existing Secondary Replica(s): Multi-Site**</span></span>

#### <a name="1-utilize-an-existing-secondary-single-site"></a><span data-ttu-id="2889a-341">1. Var olan bir ikincil kullanma: tek siteli</span><span class="sxs-lookup"><span data-stu-id="2889a-341">1. Utilize an existing secondary: Single-Site</span></span>
<span data-ttu-id="2889a-342">Mevcut bir buluta ikincil alın ve geçerli bulut hizmetinden kaldırmak için en az kapalı kalma süresi için bir strateji etmektir.</span><span class="sxs-lookup"><span data-stu-id="2889a-342">One strategy for minimal downtime is to take an existing cloud secondary and remove it from the current cloud service.</span></span> <span data-ttu-id="2889a-343">Ardından yeni Premium depolama hesabı VHD'leri kopyalayın ve VM yeni bulut hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2889a-343">Then copy the VHDs to the new Premium Storage account, and create the VM in the new cloud service.</span></span> <span data-ttu-id="2889a-344">Ardından Yük Devretme Kümelemesi ve dinleyicisinde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="2889a-344">Then update the listener in clustering and failover.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="2889a-345">Kapalı kalma süresi noktaları</span><span class="sxs-lookup"><span data-stu-id="2889a-345">Points of downtime</span></span>
* <span data-ttu-id="2889a-346">Yük dengeli uç nokta ile son düğümü güncelleştirdiğinizde kapalı kalma süresi yok.</span><span class="sxs-lookup"><span data-stu-id="2889a-346">There is downtime when you update the final node with the Load Balanced endpoint.</span></span>
* <span data-ttu-id="2889a-347">İstemci/DNS yapılandırmanıza bağlı olarak, istemci yeniden bağlanmayı gecikebilir.</span><span class="sxs-lookup"><span data-stu-id="2889a-347">Your client reconnection might be delayed depending on your client/DNS configuration.</span></span>
* <span data-ttu-id="2889a-348">IP adreslerini değiştirilecek üzerinde her zaman küme grubu çevrimdışı bırakmayı seçerseniz ek kapalı kalma süresi yok.</span><span class="sxs-lookup"><span data-stu-id="2889a-348">There is additional downtime if you choose to take the Always On Cluster group offline to swap out the IP addresses.</span></span> <span data-ttu-id="2889a-349">Bu, bir veya bağımlılık ve olası sahipleri için eklenen IP adresi kaynağı kullanarak önleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2889a-349">You can avoid this by using an OR dependency and Possible Owners for the added IP Address resource.</span></span> <span data-ttu-id="2889a-350">'Ekleme IP adresi kaynağı aynı alt ağda bulunan' bölümüne bakın [ek](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="2889a-350">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>

> [!NOTE]
> <span data-ttu-id="2889a-351">İçinde bir her zaman üzerinde yük devretme ortağı olarak partake için eklenen düğümünü istediğinizde Azure noktayla dengeli yük ayarlamak için bir başvuru eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2889a-351">When you want the added node to partake in as an Always On Failover Partner, you need to add an Azure Endpoint with a reference to the Load Balanced Set.</span></span> <span data-ttu-id="2889a-352">Çalıştırdığınızda **Ekle AzureEndpoint** Bunu yapmak için komutu, kalmasına geçerli bağlantıları'nı açın, ancak dinleyici için yeni bağlantı edemeyecek yük dengeleyici güncelleştirdi kadar kurulacak.</span><span class="sxs-lookup"><span data-stu-id="2889a-352">When you run the **Add-AzureEndpoint** command to do this, current connections to remain open, but new connections to the listener will not be able to be established until the load balancer has updated.</span></span> <span data-ttu-id="2889a-353">Bu test görüldü Son 90 120seconds için bu test edilmelidir.</span><span class="sxs-lookup"><span data-stu-id="2889a-353">In testing this was seen to last 90-120seconds, this should be tested.</span></span>
>
>

##### <a name="advantages"></a><span data-ttu-id="2889a-354">Avantajları</span><span class="sxs-lookup"><span data-stu-id="2889a-354">Advantages</span></span>
* <span data-ttu-id="2889a-355">Hiçbir ek maliyet geçiş sırasında ücrete.</span><span class="sxs-lookup"><span data-stu-id="2889a-355">No extra cost incurred during migration.</span></span>
* <span data-ttu-id="2889a-356">Bire bir geçiş.</span><span class="sxs-lookup"><span data-stu-id="2889a-356">A one-to-one migration.</span></span>
* <span data-ttu-id="2889a-357">Azaltılan karmaşıklık.</span><span class="sxs-lookup"><span data-stu-id="2889a-357">Reduced complexity.</span></span>
* <span data-ttu-id="2889a-358">Premium depolama SKU'ları için daha yüksek IOPS sağlar.</span><span class="sxs-lookup"><span data-stu-id="2889a-358">Allows for increased IOPS from Premium Storage SKUs.</span></span> <span data-ttu-id="2889a-359">Diskler sanal makineden ayrılmış ve yeni bulut hizmeti kopyalanan bir 3. taraf aracı yüksek kapatma sağlar VHD boyutunu artırmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2889a-359">When the disks are detached from the VM and copied to the new cloud service, a 3rd party tool can be used to increase the VHD size, which provides higher throughputs.</span></span> <span data-ttu-id="2889a-360">VHD boyutları artırmak için bu bkz [forum tartışmasına](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span><span class="sxs-lookup"><span data-stu-id="2889a-360">For increasing VHD sizes, see this [forum discussion](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="2889a-361">Olumsuz yönleri</span><span class="sxs-lookup"><span data-stu-id="2889a-361">Disadvantages</span></span>
* <span data-ttu-id="2889a-362">Geçiş sırasında HA ve DR kaybı yoktur.</span><span class="sxs-lookup"><span data-stu-id="2889a-362">There is a temporary loss of HA and DR during migration.</span></span>
* <span data-ttu-id="2889a-363">1:1 geçiş olarak Vm'leriniz downsize mümkün olmayabilir, böylece VHD'ler, sayısı destekleyeceği en az bir VM boyutu kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2889a-363">As this is a 1:1 migration, you will have to use a minimum VM size that will support your number of VHDs, so you might not be able to downsize your VMs.</span></span>
* <span data-ttu-id="2889a-364">Bu senaryo Azure kullanırsınız **başlangıç AzureStorageBlobCopy** zaman uyumsuz komutunu.</span><span class="sxs-lookup"><span data-stu-id="2889a-364">This scenario would use the Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="2889a-365">Kopya tamamlanma hiçbir SLA yoktur.</span><span class="sxs-lookup"><span data-stu-id="2889a-365">There is no SLA on copy completion.</span></span> <span data-ttu-id="2889a-366">Bu bekleme aktarmak için veri miktarına bağlıdır sırasındaki bağlıdır sırada kopyaları süresi olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="2889a-366">The time of the copies varies, while this depends on wait in queue it will also depend on the amount of data to transfer.</span></span> <span data-ttu-id="2889a-367">Başka bir bölgede Premium Storage destekleyen başka bir Azure veri merkezi aktarımı yayınlanıyorsa kopyalama süresini artırır.</span><span class="sxs-lookup"><span data-stu-id="2889a-367">The copy time increases if the transfer is going to another Azure data center that supports Premium Storage in another region.</span></span> <span data-ttu-id="2889a-368">2 düğümleri varsa, kopyalama testinde uzun sürdüğünde durumunda olası azaltma göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="2889a-368">If you just have 2 nodes, consider a possible mitigation in case the copy takes longer than in testing.</span></span> <span data-ttu-id="2889a-369">Bu Aşağıdaki fikirler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="2889a-369">This could include the following ideas.</span></span>
  * <span data-ttu-id="2889a-370">Bir geçici 3 SQL Server düğümü HA için üzerinde anlaşılan kapalı kalma süresi ile geçişten önce ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2889a-370">Add a temporary 3rd SQL Server node for HA before the migration with agreed downtime.</span></span>
  * <span data-ttu-id="2889a-371">Azure zamanlanmış bakım dışında geçiş çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2889a-371">Run the migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="2889a-372">Küme çekirdeğini doğru yapılandırılmış olun.</span><span class="sxs-lookup"><span data-stu-id="2889a-372">Ensure you have configured your cluster quorum correctly.</span></span>  

##### <a name="high-level-steps"></a><span data-ttu-id="2889a-373">Üst düzey adımlar</span><span class="sxs-lookup"><span data-stu-id="2889a-373">High-level steps</span></span>
<span data-ttu-id="2889a-374">Bu belgede bir tam, uçtan uca bir örnek, gösterilmemiştir ancak [ek](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) bunu gerçekleştirmek için de ayrıntıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="2889a-374">This document does not demonstrate a complete end to end example, however the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) provides details that can be leveraged to perform this.</span></span>

![MinimalDowntime][8]

* <span data-ttu-id="2889a-376">Disk yapılandırmasını toplamak ve düğüm kaldırmak (ekli VHD'ler silmeyin).</span><span class="sxs-lookup"><span data-stu-id="2889a-376">Gather disk configuration, and remove the node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="2889a-377">Premium depolama hesabı oluşturma ve standart depolama hesabından VHD'ler kopyalayın</span><span class="sxs-lookup"><span data-stu-id="2889a-377">Create a Premium Storage account and copy VHDs from the Standard Storage account</span></span>
* <span data-ttu-id="2889a-378">Yeni bulut hizmeti oluşturun ve bu bulut Hizmeti'nde SQL2 VM yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="2889a-378">Create new cloud service and redeploy the SQL2 VM in that cloud service.</span></span> <span data-ttu-id="2889a-379">Kopyalanan özgün işletim sistemi VHD kullanarak ve kopyalanan VHD'leri VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2889a-379">Create the VM using the copied original OS VHD and attaching the copied VHDs.</span></span>
* <span data-ttu-id="2889a-380">ILB yapılandırma / ELB ve uç noktalar ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2889a-380">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="2889a-381">Dinleyici ya da güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="2889a-381">Update Listener by either:</span></span>
  * <span data-ttu-id="2889a-382">Her zaman üzerindeki grubu çevrimdışına almak ve yeni ILB ile her zaman üzerinde dinleyicisi güncelleştirme / ELB IP adresi.</span><span class="sxs-lookup"><span data-stu-id="2889a-382">Taking the Always On Group offline and updating the Always On Listener with new ILB / ELB IP address.</span></span>
  * <span data-ttu-id="2889a-383">Veya IP adresi kaynağı, yeni bulut hizmeti ILB/ELB PowerShell aracılığıyla Windows Kümeleme içine ekleme.</span><span class="sxs-lookup"><span data-stu-id="2889a-383">Or adding the IP address resource of new Cloud Service ILB/ELB through PowerShell into Windows clustering.</span></span> <span data-ttu-id="2889a-384">Ardından IP adresi kaynağının olası sahipler SQL2, geçirilen düğüme ve bu ağ adı veya bağımlılık olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2889a-384">Then set the Possible owners of the IP Address resource to the migrated node, SQL2, and set this as OR dependency in the Network Name.</span></span> <span data-ttu-id="2889a-385">'Ekleme IP adresi kaynağı aynı alt ağda bulunan' bölümüne bakın [ek](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="2889a-385">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
* <span data-ttu-id="2889a-386">DNS yapılandırması/yayma istemcilere denetleyin.</span><span class="sxs-lookup"><span data-stu-id="2889a-386">Check DNS configuration/propogation to the clients.</span></span>
* <span data-ttu-id="2889a-387">SQL1 VM'yi geçirmek ve 2-4 arası adımlar gidin.</span><span class="sxs-lookup"><span data-stu-id="2889a-387">Migrate SQL1 VM, and go through steps 2 – 4.</span></span>
* <span data-ttu-id="2889a-388">Adımları 5ii kullanıyorsanız, SQL1 eklenen IP adres kaynağı için olası sahip olarak ardından ekleyin</span><span class="sxs-lookup"><span data-stu-id="2889a-388">If using steps 5ii, then add SQL1 as a Possible Owner for the added IP Address Resource</span></span>
* <span data-ttu-id="2889a-389">Test yük devretmeleri.</span><span class="sxs-lookup"><span data-stu-id="2889a-389">Test failovers.</span></span>

#### <a name="2-utilize-existing-secondary-replicas-multi-site"></a><span data-ttu-id="2889a-390">2. Var olan ikincil çoğaltmalar kullanma: çok siteli</span><span class="sxs-lookup"><span data-stu-id="2889a-390">2. Utilize existing secondary replica(s): Multi-Site</span></span>
<span data-ttu-id="2889a-391">Birden fazla Azure veri merkezinde (DC) düğümleriniz varsa veya karma bir ortamınız varsa, daha sonra her zaman açık yapılandırma bu ortamda kapalı kalma süresini en aza indirmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2889a-391">If you have nodes in more than one Azure datacenter (DC) or if you have a hybrid environment, then you can use an Always On configuration in this environment to minimize downtime.</span></span>

<span data-ttu-id="2889a-392">Şirket içi veya ikincil Azure DC ve ardından üzerinden SQL Server Yük devretme için zaman uyumlu için her zaman açık eşitleme değiştirmek için bir yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="2889a-392">The approach is to change the Always On synchronization to Synchronous for the on-premises or secondary Azure DC, and then failover over to that SQL Server.</span></span> <span data-ttu-id="2889a-393">Ardından VHD'leri Premium depolama alanına kopyalanmaya ve makineyi yeni bir bulut hizmetinde yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="2889a-393">Then copy the VHDs to a Premium Storage account, and redeploy the machine into a new cloud service.</span></span> <span data-ttu-id="2889a-394">Dinleyici güncelleştirin ve geri dönecek.</span><span class="sxs-lookup"><span data-stu-id="2889a-394">Update the listener, and then fail back.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="2889a-395">Kapalı kalma süresi noktaları</span><span class="sxs-lookup"><span data-stu-id="2889a-395">Points of downtime</span></span>
<span data-ttu-id="2889a-396">Kapalı kalma süresi alternatif DC ve geri yük devretme için zaman oluşur.</span><span class="sxs-lookup"><span data-stu-id="2889a-396">The downtime consists of the time to failover to the alternative DC and back.</span></span> <span data-ttu-id="2889a-397">Ayrıca, istemci/DNS yapılandırmasına bağlıdır ve istemci yeniden bağlanmayı gecikebilir.</span><span class="sxs-lookup"><span data-stu-id="2889a-397">It also depends on your client/DNS configuration and your client reconnection may be delayed.</span></span>
<span data-ttu-id="2889a-398">Aşağıdaki örnekte, her zaman açık bir karma yapılandırmasının göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="2889a-398">Consider the following example of a hybrid Always On configuration:</span></span>

![MultiSite1][9]

##### <a name="advantages"></a><span data-ttu-id="2889a-400">Avantajları</span><span class="sxs-lookup"><span data-stu-id="2889a-400">Advantages</span></span>
* <span data-ttu-id="2889a-401">Mevcut altyapısını kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="2889a-401">You can utilize existing infrastructure.</span></span>
* <span data-ttu-id="2889a-402">Azure depolama, DR Azure DC üzerinde önceden yükseltmeniz seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="2889a-402">You have the option to pre-upgrade the Azure storage on the DR Azure DC first.</span></span>
* <span data-ttu-id="2889a-403">DR Azure DC depolaması yeniden.</span><span class="sxs-lookup"><span data-stu-id="2889a-403">The DR Azure DC storage can be reconfigured.</span></span>
* <span data-ttu-id="2889a-404">Yük devretme sınaması işlemlerini hariç geçiş sırasında en az iki yük devretme işlemlerini yoktur.</span><span class="sxs-lookup"><span data-stu-id="2889a-404">There is a minimum of two failovers during migration, excluding test failovers.</span></span>
* <span data-ttu-id="2889a-405">Yedekleme ile SQL Server verilerini taşımak ve geri yüklemek gerekmez.</span><span class="sxs-lookup"><span data-stu-id="2889a-405">You do not need to move SQL Server data with backup and restore.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="2889a-406">Olumsuz yönleri</span><span class="sxs-lookup"><span data-stu-id="2889a-406">Disadvantages</span></span>
* <span data-ttu-id="2889a-407">SQL Server istemci erişimi bağlı olarak olabilir daha yüksek gecikme süresi SQL Server uygulamaya alternatif bir DC'nin çalışırken.</span><span class="sxs-lookup"><span data-stu-id="2889a-407">Depending on client access to SQL Server, there might be increased latency when SQL Server is running in an alternative DC to the application.</span></span>
* <span data-ttu-id="2889a-408">VHD'ler kopyalama zaman Premium Depolama'ya uzun olabilir.</span><span class="sxs-lookup"><span data-stu-id="2889a-408">The copy time of VHDs to Premium storage could be long.</span></span> <span data-ttu-id="2889a-409">Bu kullanılabilirlik grubunda düğüm tutulup tutulmayacağını üzerinde kararınızı etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="2889a-409">This might affect your decision on whether to keep the node in the Availability Group.</span></span> <span data-ttu-id="2889a-410">Bu, işlem günlüğünde çoğaltılmamış işlemlerini saklamak birincil düğüm gerekeceğinden günlük yoğun iş yükleri geçiş sırasında çalışan gerekli olduğunda için göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="2889a-410">Consider this for when log intensive work loads are running during the migration is required, since the Primary node will have to keep the unreplicated transactions in its transaction log.</span></span> <span data-ttu-id="2889a-411">Bu nedenle bu önemli oranda artma.</span><span class="sxs-lookup"><span data-stu-id="2889a-411">Therefore this could grow significantly.</span></span>
* <span data-ttu-id="2889a-412">Bu senaryo Azure kullanırsınız **başlangıç AzureStorageBlobCopy** zaman uyumsuz komutunu.</span><span class="sxs-lookup"><span data-stu-id="2889a-412">This scenario would use the Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="2889a-413">Tamamlanma hiçbir SLA yoktur.</span><span class="sxs-lookup"><span data-stu-id="2889a-413">There is no SLA on completion.</span></span> <span data-ttu-id="2889a-414">Bu sıradaki bekleme bağlıdır sırada kopyaları süre değişir aktarmak için veri miktarına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="2889a-414">The time of the copies varies, while this depends on wait in queue, it will also depend on the amount of data to transfer.</span></span> <span data-ttu-id="2889a-415">Bu nedenle 2 veri merkezinizde yalnızca bir düğüme sahip, kopya testinde uzun sürdüğünde durumda azaltma adımlarını gerçekleştirmesi gereken.</span><span class="sxs-lookup"><span data-stu-id="2889a-415">Therefore you just have one node in your 2nd data center, you should take mitigation steps in case the copy takes longer than in testing.</span></span> <span data-ttu-id="2889a-416">Bu Aşağıdaki fikirler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="2889a-416">This could include the following ideas.</span></span>
  * <span data-ttu-id="2889a-417">Geçici bir 2 SQL düğüm HA için üzerinde anlaşılan kapalı kalma süresi ile geçişten önce ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2889a-417">Add a temporary 2nd SQL node for HA before the migration with agreed downtime.</span></span>
  * <span data-ttu-id="2889a-418">Azure zamanlanmış bakım dışında geçiş çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2889a-418">Run the migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="2889a-419">Küme çekirdeğini doğru yapılandırılmış olun.</span><span class="sxs-lookup"><span data-stu-id="2889a-419">Ensure you have configured your cluster quorum correctly.</span></span>

<span data-ttu-id="2889a-420">Bu senaryo, yüklemenizi belgelenmiş ve en yüksek disk önbellek ayarlarını değişiklik yapmak için depolama nasıl eşlenen bilmeniz varsayar.</span><span class="sxs-lookup"><span data-stu-id="2889a-420">This scenario assumes that you have documented your install and know how the storage is mapped in order to make changes for optimal disk cache settings.</span></span>

##### <a name="high-level-steps"></a><span data-ttu-id="2889a-421">Üst düzey adımlar</span><span class="sxs-lookup"><span data-stu-id="2889a-421">High-level steps</span></span>
![Multisite2][10]

* <span data-ttu-id="2889a-423">Şirket içi / Azure DC SQL Server birincil alternatif ve diğer otomatik yük devretme iş ortağı (AFP) olun.</span><span class="sxs-lookup"><span data-stu-id="2889a-423">Make the on-premises / alternate Azure DC the SQL Server Primary, and make it the other Auto Failover Partner (AFP).</span></span>
* <span data-ttu-id="2889a-424">SQL2 disk yapılandırma bilgilerini toplamak ve düğüm kaldırmak (ekli VHD'ler silmeyin).</span><span class="sxs-lookup"><span data-stu-id="2889a-424">Gather disk configuration information from SQL2, and remove the node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="2889a-425">Premium depolama hesabı oluşturma ve standart depolama hesabından VHD'ler kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="2889a-425">Create a Premium Storage account and copy VHDs from the Standard Storage account.</span></span>
* <span data-ttu-id="2889a-426">Yeni bir bulut hizmeti oluşturun ve kendi prim depolama diskleri ekli SQL2 VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2889a-426">Create a new cloud service and create the SQL2 VM with its Premiums Storage disks attached.</span></span>
* <span data-ttu-id="2889a-427">ILB yapılandırma / ELB ve uç noktalar ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2889a-427">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="2889a-428">Yeni ILB ile her zaman üzerinde dinleyicisi güncelleştirme / ELB IP adresi ve test yük devretme.</span><span class="sxs-lookup"><span data-stu-id="2889a-428">Update the Always On Listener with new ILB / ELB IP address and test failover.</span></span>
* <span data-ttu-id="2889a-429">DNS yapılandırmasını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="2889a-429">Check the DNS configuration.</span></span>
* <span data-ttu-id="2889a-430">AFP SQL2 için değiştirmek ve SQL1 geçirmek ve 2 – 5 adımlarını gidin.</span><span class="sxs-lookup"><span data-stu-id="2889a-430">Change the AFP to SQL2, and then migrate SQL1 and go through steps 2 – 5.</span></span>
* <span data-ttu-id="2889a-431">Test yük devretmeleri.</span><span class="sxs-lookup"><span data-stu-id="2889a-431">Test failovers.</span></span>
* <span data-ttu-id="2889a-432">SQL1 ve SQL2 AFP geçiş</span><span class="sxs-lookup"><span data-stu-id="2889a-432">Switch the AFP back to SQL1 and SQL2</span></span>

## <a name="appendix-migrating-a-multisite-always-on-cluster-to-premium-storage"></a><span data-ttu-id="2889a-433">Ek: bir çoklu site küme her zaman açık Premium depolama alanına geçirme</span><span class="sxs-lookup"><span data-stu-id="2889a-433">Appendix: Migrating a Multisite Always On Cluster to Premium Storage</span></span>
<span data-ttu-id="2889a-434">Bu konunun geri kalanında, her zaman açık bir çok siteli küme Premium depolama alanına dönüştürme ayrıntılı bir örnek sağlar.</span><span class="sxs-lookup"><span data-stu-id="2889a-434">The remainder of this topic provides a detailed example of converting a multi-site Always On cluster to Premium storage.</span></span> <span data-ttu-id="2889a-435">Bu ayrıca dinleyicisi bir dış yük dengeleyici (ELB) kullanarak bir iç yük dengeleyici (ILB) dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="2889a-435">It also converts the Listener from using an external load balancer (ELB) to an internal load balancer (ILB).</span></span>

### <a name="environment"></a><span data-ttu-id="2889a-436">Ortam</span><span class="sxs-lookup"><span data-stu-id="2889a-436">Environment</span></span>
* <span data-ttu-id="2889a-437">Windows 2k 12 / SQL 2k 12</span><span class="sxs-lookup"><span data-stu-id="2889a-437">Windows 2k12 / SQL 2k12</span></span>
* <span data-ttu-id="2889a-438">SP 1 DB dosyaları</span><span class="sxs-lookup"><span data-stu-id="2889a-438">1 DB Files on SP</span></span>
* <span data-ttu-id="2889a-439">Düğüm başına depolama havuzları x 2</span><span class="sxs-lookup"><span data-stu-id="2889a-439">2 x Storage Pools per Node</span></span>

![Appendix1][11]

### <a name="vm"></a><span data-ttu-id="2889a-441">VM:</span><span class="sxs-lookup"><span data-stu-id="2889a-441">VM:</span></span>
<span data-ttu-id="2889a-442">Bu örnekte, biz ILB için bir ELB taşıma göstermek için adımıdır.</span><span class="sxs-lookup"><span data-stu-id="2889a-442">In this example we are going to demonstrate moving from an ELB to ILB.</span></span> <span data-ttu-id="2889a-443">Bunun için geçiş sırasında geçiş yapma gösterecek şekilde ELB ILB önce mevcut değildi.</span><span class="sxs-lookup"><span data-stu-id="2889a-443">ELB was available before ILB, so this shows how to switch to this during the migration.</span></span>

![Appendix2][12]

### <a name="pre-steps-connect-to-subscription"></a><span data-ttu-id="2889a-445">Öncesi adımları: Aboneliğine bağlanma</span><span class="sxs-lookup"><span data-stu-id="2889a-445">Pre Steps: Connect to Subscription</span></span>
    Add-AzureAccount

    #Set up subscription
    Get-AzureSubscription

#### <a name="step-1-create-new-storage-account-and-cloud-service"></a><span data-ttu-id="2889a-446">1. adım: Yeni depolama hesabı oluşturun ve bulut hizmeti</span><span class="sxs-lookup"><span data-stu-id="2889a-446">Step 1: Create New Storage Account and Cloud Service</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Storage accounts
    #current storage account where the vm to migrate resides
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

#### <a name="step-2-increase-the-permitted-failures-on-resources-optional"></a><span data-ttu-id="2889a-447">2. adım: izin verilen hataları kaynaklar üzerinde artırın<Optional></span><span class="sxs-lookup"><span data-stu-id="2889a-447">Step 2: Increase the permitted failures on resources <Optional></span></span>
<span data-ttu-id="2889a-448">Her zaman üzerinde kullanılabilirlik grubuna ait bazı kaynaklar üzerinde sınırlar vardır, Küme hizmetinin kaynak grubunu yeniden başlatmaya çalışacak bir dönemde oluşabilir kaç hatalarda.</span><span class="sxs-lookup"><span data-stu-id="2889a-448">On certain resources that belong to your Always On Availability Group there are limits on how many failures that can occur in a period, where the cluster service will attempt to restart the resource group.</span></span> <span data-ttu-id="2889a-449">Bu sınıra yakın alabilirsiniz makineler kapatma tarafından el ile yük devretme ve tetikleyici yük devretme veritabanınız yoksa bu yana bu yordamı taramasını adımında, bu artırmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="2889a-449">It is recommended you increase this whilst you are walking through this procedure, since if you don’t manually failover and trigger failovers by shutting down machines you can get close to this limit.</span></span>

<span data-ttu-id="2889a-450">Yük Devretme Kümesi Yöneticisi'nde bunun için hata indirimi çift akıllıca her zaman açık kaynak grubunun özelliklerini gidin:</span><span class="sxs-lookup"><span data-stu-id="2889a-450">It would be prudent to double the failure allowance, to do this in Failover Cluster Manager, go to the Properties of the Always On resource group:</span></span>

![Appendix3][13]

<span data-ttu-id="2889a-452">En fazla hata sayısı için 6 değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2889a-452">Change the Maximum Failures to 6.</span></span>

#### <a name="step-3-addition-ip-address-resource-for-cluster-group-optional"></a><span data-ttu-id="2889a-453">3. adım: Ek IP adresi kaynağı küme grubu için<Optional></span><span class="sxs-lookup"><span data-stu-id="2889a-453">Step 3: Addition IP Address resource for Cluster Group <Optional></span></span>
<span data-ttu-id="2889a-454">Küme grubu için tek bir IP adresi varsa ve bu bulut alt ağına hizalanır, yanlışlıkla tüm küme düğümlerine bulutta bulunan bu ağ sonra küme IP kaynağı çevrimdışına ve küme ağ adı çevrimiçine mümkün olmaz kaybolacağını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2889a-454">If you have only one IP address for the Cluster Group and this is aligned to the cloud subnet, beware, if you accidentally take offline all cluster nodes in the cloud on that network then the Cluster IP resource and Cluster Network Name will not be able to come online.</span></span> <span data-ttu-id="2889a-455">Bu durumunda, güncelleştirmelerinin diğer küme kaynaklarını engeller.</span><span class="sxs-lookup"><span data-stu-id="2889a-455">In the event of this it will prevent updates to other cluster resources.</span></span>

#### <a name="step-4-dns-configuration"></a><span data-ttu-id="2889a-456">4. adım: DNS yapılandırması</span><span class="sxs-lookup"><span data-stu-id="2889a-456">Step 4: DNS configuration</span></span>
<span data-ttu-id="2889a-457">Bir kesintisiz uygulamak için nasıl DNS yüklenmekte olan geçiş bağlıdır kullanılan ve güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="2889a-457">To implement a smooth transition depends on how DNS is being utilized and updated.</span></span>
<span data-ttu-id="2889a-458">Her zaman açık yüklendiğinde, bir Windows Küme kaynak grubu oluşturur yük devretme kümesi Yöneticisi'ni açın, göreceğiniz en az üç kaynaklara sahip olur, belgenin başvurduğu iki şunlardır:</span><span class="sxs-lookup"><span data-stu-id="2889a-458">When Always On is installed, it creates a Windows Cluster Resource group, if you open Failover Cluster Manager, you will see that at a minimum it will have three resources, the two that the document refers to are:</span></span>

* <span data-ttu-id="2889a-459">Sanal ağ adına (VNN) – budur DNS adı istemci bağlanmak için SQL sunucuları her zaman açık aracılığıyla bağlanmak istediğinizde.</span><span class="sxs-lookup"><span data-stu-id="2889a-459">Virtual Network Name (VNN) – This is the DNS name that client connect to when wanting to connect to SQL Servers via Always On.</span></span>
* <span data-ttu-id="2889a-460">IP adresi kaynağı – bu VNN ile ilişkili IP adresidir, birden fazla olabilir ve çok siteli bir yapılandırma her site/alt ağda bir IP adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="2889a-460">IP Address Resource – This is the IP address that associated with the VNN, you can have more than one, and in a multisite configuration you will have an IP address per site/subnet.</span></span>

<span data-ttu-id="2889a-461">IP adresi ilişkili SQL Server, SQL Server sürücüsü dinleyicisi ile ilişkili DNS kayıtlarını almak ve her zaman açık bağlanmaya istemcisi bağlanma, aşağıda Biz bu etkileyebilir bazı etkenler tartışın.</span><span class="sxs-lookup"><span data-stu-id="2889a-461">When connecting to SQL Server, the SQL Server Client driver will retrieve the DNS records associated with the listener and try to connect to each Always On associated IP address, below we discuss some factors that can influence this.</span></span>

<span data-ttu-id="2889a-462">Dinleyici adıyla ilişkili eşzamanlı DNS kayıtlarını sayısı yalnızca ilişkili IP adresleri sayısına bağlıdır, ancak ' de yük devretme kümelemesi için her zaman açık VNN kaynak RegisterAllIpProviders'setting.</span><span class="sxs-lookup"><span data-stu-id="2889a-462">The number of concurrent DNS records that are associated with the listener name depends not only on the number of IP addresses associated, but the ‘RegisterAllIpProviders’setting in Failover Clustering for the Always ON VNN resource.</span></span>

<span data-ttu-id="2889a-463">Azure'da her zaman açık dağıttığınızda IP adreslerini ve dinleyicisi oluşturmak için farklı adımlar vardır, 1 'RegisterAllIpProviders' el ile yapılandırmanız gerekir, bu burada 1 olarak ayarlayın her zaman açık bir şirket içi dağıtımına farklı.</span><span class="sxs-lookup"><span data-stu-id="2889a-463">When you deploy Always On in Azure there are different steps to create the Listener and IP Addresses, you have to manually configure the ‘RegisterAllIpProviders’ to 1, this is different to an on-premises Always On deployment where it is already set to 1.</span></span>

<span data-ttu-id="2889a-464">'RegisterAllIpProviders' 0 ise, ardından yalnızca bir DNS kaydı DNS'de dinleyicisi ile ilişkili görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="2889a-464">If ‘RegisterAllIpProviders’ is 0, then you will only see one DNS record in DNS associated with the Listener:</span></span>

![Appendix4][14]

<span data-ttu-id="2889a-466">'RegisterAllIpProviders' 1 ise:</span><span class="sxs-lookup"><span data-stu-id="2889a-466">If ‘RegisterAllIpProviders’ is 1:</span></span>

![Appendix5][15]

<span data-ttu-id="2889a-468">Aşağıdaki kodu dökümü VNN ayarları ve sizin için dinleyici çevrimdışı neden alma VNN çevrimdışına alın ve tekrar çevrimiçi kapatma gerekir değişikliğin etkili olması için Not Lütfen istemci bağlantı kesintisi.</span><span class="sxs-lookup"><span data-stu-id="2889a-468">The code below will dump out the VNN settings and set it for you, please note, for the change to take effect you will need to take the VNN offline and turn it back online, this taking the Listener offline causing client connectivity disruption.</span></span>

    ##Always On Listener Name
    $ListenerName = "Mylistener"
    ##Get AlwaysOn Network Name Settings
    Get-ClusterResource $ListenerName| Get-ClusterParameter
    ##Set RegisterAllProvidersIP
    Get-ClusterResource $ListenerName| Set-ClusterParameter RegisterAllProvidersIP  1

<span data-ttu-id="2889a-469">Bir sonraki geçiş adımda, her zaman açık dinleyici bir yük dengeleyici başvuran güncelleştirilmiş IP adresi ile güncellemeniz gerekir bu bir IP adresi kaynak temizleme ve ayrıca içerecektir.</span><span class="sxs-lookup"><span data-stu-id="2889a-469">In a later migration step you will need to update the Always On listener with an updated IP address that will reference a load balancer, this will involve an IP Address resource removal and addition.</span></span> <span data-ttu-id="2889a-470">IP Güncelleştirme tamamlandıktan sonra yeni IP adresini DNS bölgesinde güncelleştirildi ve istemcilerin kendi yerel DNS önbelleği güncelleştirdiğiniz emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2889a-470">After the IP update, you need to ensure the new IP address has been updated in DNS Zone and that the clients are updating their local DNS cache.</span></span>

<span data-ttu-id="2889a-471">Neler DNS bölge aktarma hakkında geçiş sırasında uygulama yeniden gibi zaman olacaktır dikkate almanız gerekir, istemciler farklı ağında bulunan ve farklı bir DNS sunucusu başvuru, en az bölge aktarım zamanını herhangi biri tarafından kısıtlı Dinleyici için yeni IP adresi.</span><span class="sxs-lookup"><span data-stu-id="2889a-471">If your clients reside in a different network segment and reference a different DNS server, you need to consider what happens about DNS Zone Transfer during the migration, as the application reconnect time will be constrained by at least the Zone Transfer Time of any new IP addresses for the listener.</span></span> <span data-ttu-id="2889a-472">Burada zaman sınırlaması altında olup olmadığını ele almaktadır ve Windows ekipleriniz ile bir artımlı bölge aktarımı zorlama test ve ayrıca DNS ana bilgisayar kaydı bir alt yaşam süresi (TTL için) put, böylece istemciler güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="2889a-472">If you are under time constraint here, you should discuss and test forcing an incremental zone transfer with your Windows teams, and also put the DNS host record to a lower Time To Live (TTL), so the clients update.</span></span> <span data-ttu-id="2889a-473">Daha fazla bilgi için bkz: [artımlı bölge aktarımlarının](https://technet.microsoft.com/library/cc958973.aspx) ve [başlangıç DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span><span class="sxs-lookup"><span data-stu-id="2889a-473">For more information, see [Incremental Zone Transfers](https://technet.microsoft.com/library/cc958973.aspx) and [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span></span>

<span data-ttu-id="2889a-474">Varsayılan olarak, azure'da her zaman açık dinleyici ile ilişkili DNS kaydının TTL 1200 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="2889a-474">By default the TTL for DNS Record that is associated with the Listener in Always On in Azure is 1200 seconds.</span></span> <span data-ttu-id="2889a-475">İstemcilerin emin olmak için geçiş sırasında kısıtlaması kendi DNS güncelleştirilmiş IP adresiyle için dinleyici güncelleştirdiğinizde altında olması durumunda bu azaltmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2889a-475">You may wish to reduce this if you are under time constraint during your migration to ensure the clients update their DNS with the updated IP address for the listener.</span></span> <span data-ttu-id="2889a-476">Bakın ve VNN yapılandırma döküm alma yapılandırmasını değiştirin:</span><span class="sxs-lookup"><span data-stu-id="2889a-476">You can see and modify the configuration by dumping out the configuration of the VNN:</span></span>

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"
    #Look at HostRecordTTL
    Get-ClusterResource $ListenerName| Get-ClusterParameter

    #Set HostRecordTTL Examples
    Get-ClusterResource $ListenerName| Set-ClusterParameter -Name "HostRecordTTL" 120

<span data-ttu-id="2889a-477">Lütfen, daha düşük 'HostRecordTTL', daha yüksek bir DNS trafik miktarı gerçekleşecek unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2889a-477">Please note, the lower the ‘HostRecordTTL’, a higher amount of DNS traffic will occur.</span></span>

##### <a name="client-application-settings"></a><span data-ttu-id="2889a-478">İstemci uygulama ayarları</span><span class="sxs-lookup"><span data-stu-id="2889a-478">Client application settings</span></span>
<span data-ttu-id="2889a-479">SQL istemci uygulamanız .net 4.5 destekliyorsa SQLClient sonra kullanabileceğiniz ' MULTISUBNETFAILOVER = TRUE' anahtar sözcüğü, bu önerilir daha hızlı bağlantı SQL her zaman üzerindeki kullanılabilirlik grubu için yük devretme sırasında verdiğinden uygulanacak.</span><span class="sxs-lookup"><span data-stu-id="2889a-479">If your SQL client application supports the .Net 4.5 SQLClient, then you can use ‘MULTISUBNETFAILOVER=TRUE’ keyword, this is recommended to be applied as it allows for faster connection to SQL Always On Availability Group during failover.</span></span> <span data-ttu-id="2889a-480">Her zaman açık dinleyici paralel ile ilişkili tüm IP adreslerini aracılığıyla numaralandırır ve yük devretme sırasında daha agresif bir TCP bağlantı yeniden deneme hızı gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="2889a-480">It enumerates through all IP addresses associated with the Always On listener in parallel, and performs a more aggressive TCP connection retry speed during a failover.</span></span>

<span data-ttu-id="2889a-481">Yukarıdaki ayarlarla ilgili daha fazla bilgi için lütfen bkz [MultiSubnetFailover anahtar sözcüğü ve ilişkili özellikleri](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span><span class="sxs-lookup"><span data-stu-id="2889a-481">For more information regarding the settings above, please see [MultiSubnetFailover Keyword and Associated Features](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span></span> <span data-ttu-id="2889a-482">Ayrıca bkz. [SqlClient yüksek kullanılabilirlik, olağanüstü durum kurtarma desteği](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="2889a-482">Also see [SqlClient Support for High Availability, Disaster Recovery](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span></span>

#### <a name="step-5-cluster-quorum-settings"></a><span data-ttu-id="2889a-483">5. adım: Küme çekirdek ayarlarını</span><span class="sxs-lookup"><span data-stu-id="2889a-483">Step 5: Cluster quorum settings</span></span>
<span data-ttu-id="2889a-484">Aynı anda en az bir SQL Server çıkışı sürüyor olacak şekilde, dosya paylaşım tanığı (FSW) 2 düğümleri ile kullanıyorsanız, küme çekirdek ayarı değiştirmelisiniz, düğüm çoğunluğu izin vermek ve dinamik oy kullanmak için çekirdek ayarlamanız gerekir , ve bu tek bir düğüm durumu kalır izin vermektir.</span><span class="sxs-lookup"><span data-stu-id="2889a-484">As you are going to be taking out at least one SQL Server down at a time, you should modify the cluster quorum setting, if using File Share Witness (FSW) with 2 nodes, you should set the quorum to allow node majority and utilize dynamic voting, and this is to allow for a single node to remain standing.</span></span>

    Set-ClusterQuorum -NodeMajority  

<span data-ttu-id="2889a-485">Küme çekirdeği yapılandırma ve yönetme hakkında daha fazla bilgi için lütfen bkz [yapılandırmak ve bir Windows Server 2012 yük devretme kümesinde çekirdeği yönetmek](https://technet.microsoft.com/library/jj612870.aspx).</span><span class="sxs-lookup"><span data-stu-id="2889a-485">For more information on managing and configuring the cluster quorum, please see [Configure and Manage the Quorum in a Windows Server 2012 Failover Cluster](https://technet.microsoft.com/library/jj612870.aspx).</span></span>

#### <a name="step-6-extract-existing-endpoints-and-acls"></a><span data-ttu-id="2889a-486">6. adım: Mevcut uç noktalar ACL ayıklayıp</span><span class="sxs-lookup"><span data-stu-id="2889a-486">Step 6: Extract Existing Endpoints and ACLs</span></span>
    #GET Endpoint info
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureEndpoint
    #GET ACL Rules for Each EP, this example is for the Always On Endpoint
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureAclConfig -EndpointName "myAOEndPoint-LB"  

<span data-ttu-id="2889a-487">Bu bir metin dosyasına kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2889a-487">Save these to a text file.</span></span>

#### <a name="step-7-change-failover-partners-and-replication-modes"></a><span data-ttu-id="2889a-488">7. adım: Yük devretme iş ortakları ve çoğaltma modları değiştirme</span><span class="sxs-lookup"><span data-stu-id="2889a-488">Step 7: Change Failover Partners and Replication Modes</span></span>
<span data-ttu-id="2889a-489">2'den fazla SQL sunucuları varsa, başka bir DC ya da şirket içi başka bir ikincil yük devretme 'zaman 'uyumlu değiştirme ve bir otomatik yük devretme iş ortağı (AFP) olun, değişiklik yapmadan adımında HA korumak için budur.</span><span class="sxs-lookup"><span data-stu-id="2889a-489">If you have more than 2 SQL Servers, you should change the failover of another secondary in another DC or on-premises to ‘Synchronous’ and make it an Automatic Failover Partner (AFP), this is so you maintain HA whilst you are making changes.</span></span> <span data-ttu-id="2889a-490">Bunu TSQL yapabilirsiniz ancak SSMS değiştirin:</span><span class="sxs-lookup"><span data-stu-id="2889a-490">You can do this through TSQL of modify though SSMS:</span></span>

![Appendix6][16]

#### <a name="step-8-remove-secondary-vm-from-cloud-service"></a><span data-ttu-id="2889a-492">8. adım: İkincil VM bulut hizmetinden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2889a-492">Step 8: Remove Secondary VM from cloud service</span></span>
<span data-ttu-id="2889a-493">Bir bulut ikincil düğüm ilk olarak, geçirmek planlama gereken şu anda birincil ise, el ile bir yük devretme başlatın.</span><span class="sxs-lookup"><span data-stu-id="2889a-493">You should be planning to migrate a cloud secondary node first, if this is currently primary, you should initiate a manual failover.</span></span>

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

    #Check disk config, make sure below returns the disks associated with the VM
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machibe is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild to new cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-9-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="2889a-494">9. adım: önbelleğe alma ayarları CSV dosyasındaki disk değiştirin ve kaydedin</span><span class="sxs-lookup"><span data-stu-id="2889a-494">Step 9: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="2889a-495">Veri birimleri için bu READONLY ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2889a-495">For data volumes these should be set to READONLY.</span></span>

<span data-ttu-id="2889a-496">TLOG birimler için bunların hiçbiri olarak ayarlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2889a-496">For TLOG volumes these should be set to NONE.</span></span>

![Appendix7][17]

#### <a name="step-10-copy-vhds"></a><span data-ttu-id="2889a-498">10. adım: Kopyalama VHD'leri</span><span class="sxs-lookup"><span data-stu-id="2889a-498">Step 10: Copy VHDS</span></span>
    #Ensure you have created the container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContext

    ####DISK COPYING####
    #Get disks from csv, get settings for each VHDs and copy to Premium Storage accoun
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



<span data-ttu-id="2889a-499">Premium depolama hesabı VHD'ler kopya durumunu denetleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2889a-499">You can check the copy status of the VHDs to the Premium Storage account:</span></span>

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

<span data-ttu-id="2889a-501">Bunların tümü başarılı kaydedilir kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="2889a-501">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="2889a-502">Tek tek bloblar için daha fazla bilgi için:</span><span class="sxs-lookup"><span data-stu-id="2889a-502">For information for individual blobs:</span></span>

    Get-AzureStorageBlobCopyState -Blob "blobname.vhd" -Container $containerName -Context $xioContext

#### <a name="step-11-register-os-disk"></a><span data-ttu-id="2889a-503">11. adım: Kayıt işletim sistemi diski</span><span class="sxs-lookup"><span data-stu-id="2889a-503">Step 11: Register OS disk</span></span>
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

#### <a name="step-12-import-secondary-into-new-cloud-service"></a><span data-ttu-id="2889a-504">12. adım: yeni bulut hizmetinde ikincil alma</span><span class="sxs-lookup"><span data-stu-id="2889a-504">Step 12: Import secondary into new cloud service</span></span>
<span data-ttu-id="2889a-505">Aşağıdaki kodu aynı zamanda eklenen seçeneğini burada kullanan makine aktarıp retainable VIP kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2889a-505">The code below also uses the added option here you can import the machine and use the retainable VIP.</span></span>

    #Build VM Config
    $ipaddr = "192.168.0.5"
    #Remember to change to XIO
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

    ###Attaching disks to a VM during a deploy to a new cloud service and new storage account is different from just attaching VHDs to just a redeploy in a new cloud service
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)

#### <a name="step-13-create-ilb-on-new-cloud-svc-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="2889a-506">13. adım: Yük eklemek ILB yeni bulut Svc üzerinde oluşturma dengeli uç noktaları ve ACL'leri</span><span class="sxs-lookup"><span data-stu-id="2889a-506">Step 13: Create ILB on New Cloud Svc, Add Load Balanced Endpoints and ACLs</span></span>
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

#### <a name="step-14-update-always-on"></a><span data-ttu-id="2889a-507">14. adım: Her zaman üzerinde güncelleştir</span><span class="sxs-lookup"><span data-stu-id="2889a-507">Step 14: Update Always On</span></span>
    #Code to be executed on a Cluster Node
    $ClusterNetworkNameAmsterdam = "Cluster Network 2" # the azure cluster subnet network name
    $newCloudServiceIPAmsterdam = "192.168.0.25" # IP address of your cloud service

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"


    Add-ClusterResource "IP Address $newCloudServiceIPAmsterdam" -ResourceType "IP Address" -Group $AGName -ErrorAction Stop |  Set-ClusterParameter -Multiple @{"Address"="$newCloudServiceIPAmsterdam";"ProbePort"="59999";SubnetMask="255.255.255.255";"Network"=$ClusterNetworkNameAmsterdam;"OverrideAddressMatch"=1;"EnableDhcp"=0} -ErrorAction Stop

    #set dependancy and NETBIOS, then remove old IP address

    #set NETBIOS, then remove old IP address
    Get-ClusterGroup $AGName | Get-ClusterResource -Name "IP Address $newCloudServiceIPAmsterdam" | Set-ClusterParameter -Name EnableNetBIOS -Value 0

    #set dependency to Listener (OR Dependency) and delete previous IP Address resource that references:

    #Make sure no static records in DNS

![Appendix9][19]

<span data-ttu-id="2889a-509">Artık eski bulut hizmeti IP adresini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2889a-509">Now remove the old cloud service IP Address.</span></span>

![Appendix10][20]

#### <a name="step-15-dns-update-check"></a><span data-ttu-id="2889a-511">15. adım: DNS güncelleştirme denetimi</span><span class="sxs-lookup"><span data-stu-id="2889a-511">Step 15: DNS update check</span></span>
<span data-ttu-id="2889a-512">Şimdi DNS sunucuları, SQL Server istemci ağlarda denetimi ve kümeleme eklenen IP adresi için ek ana bilgisayar kaydı ekledi emin olun.</span><span class="sxs-lookup"><span data-stu-id="2889a-512">You should now check DNS Servers on your SQL Server client networks and make sure that clustering has added the extra host record for the added IP address.</span></span> <span data-ttu-id="2889a-513">Bu DNS sunucuları güncelleştirilmemiş, DNS bölge aktarımı zorlama göz önünde bulundurun ve istemcilerin emin var. alt hem her zaman üzerinde IP adreslerini çözümleyemedi, otomatik DNS çoğaltmanın tamamlanmasını bekleyin gerek yoktur bu.</span><span class="sxs-lookup"><span data-stu-id="2889a-513">If those DNS servers have not updated, consider forcing a DNS Zone transfer and ensure that the clients in there subnet are able to resolve to both Always On IP Addresses, this is so you do not need to wait for automatic DNS replication.</span></span>

#### <a name="step-16-reconfigure-always-on"></a><span data-ttu-id="2889a-514">16. adım: Her zaman yeniden yapılandırın</span><span class="sxs-lookup"><span data-stu-id="2889a-514">Step 16: Reconfigure Always On</span></span>
<span data-ttu-id="2889a-515">Bu noktada tam olarak şirket içi düğümle yeniden eşitleyin ve zaman uyumlu çoğaltma düğüme geçiş ve AFP yapmak için geçirilen bu düğüm için ikincil bekleyin.</span><span class="sxs-lookup"><span data-stu-id="2889a-515">At this point you wait for the secondary that node that was migrated to fully resynchronize with the on-premises node and switch to synchronous replication node and make it the AFP.</span></span>  

#### <a name="step-17-migrate-second-node"></a><span data-ttu-id="2889a-516">17. adım: ikinci düğümü geçirme</span><span class="sxs-lookup"><span data-stu-id="2889a-516">Step 17: Migrate second node</span></span>
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

    #Drop machine and rebuild to new cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-18-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="2889a-517">Adım 18: önbelleğe alma ayarları CSV dosyasındaki disk değiştirin ve kaydedin</span><span class="sxs-lookup"><span data-stu-id="2889a-517">Step 18: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="2889a-518">Veri birimleri için bu READONLY ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2889a-518">For data volumes these should be set to READONLY.</span></span>

<span data-ttu-id="2889a-519">TLOG birimler için bunların hiçbiri olarak ayarlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2889a-519">For TLOG volumes these should be set to NONE.</span></span>

![Appendix11][21]

#### <a name="step-19-create-new-independent-storage-account-for-secondary-node"></a><span data-ttu-id="2889a-521">19. adım: İkincil düğüm için yeni bağımsız depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2889a-521">Step 19: Create New Independent Storage Account for Secondary Node</span></span>
    $newxiostorageaccountnamenode2 = "danspremsams2"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountnamenode2 -Location $location -Type "Premium_LRS"  

    #Reset the storage account src if node 1 in a different storage account
    $origstorageaccountname2nd = "danstdams2"

    #Generate storage keys for later
    $xiostoragenode2 = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountnamenode2

    #Generate storage acc contexts
    $xioContextnode2 = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountnamenode2 -StorageAccountKey $xiostoragenode2.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

#### <a name="step-20-copy-vhds"></a><span data-ttu-id="2889a-522">20. adım: Kopyalama VHD'leri</span><span class="sxs-lookup"><span data-stu-id="2889a-522">Step 20: Copy VHDS</span></span>
    #Ensure you have created the container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContextnode2  

    ####DISK COPYING####
    ##get disks from csv, get settings for each VHDs and copy to Premium Storage accoun
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


<span data-ttu-id="2889a-523">Tüm VHD'leri için VHD kopya durumunu denetleyebilirsiniz: ForEach ($disk $diskobjects içinde) {$lun $disk =. LUN $vhdname $disk.vhdname $cacheoption = $disk =. HostCaching $disklabel $disk =. Disketiketi $diskName $disk =. DiskName</span><span class="sxs-lookup"><span data-stu-id="2889a-523">You can check the VHD copy status for all VHDs: ForEach ($disk in $diskobjects) { $lun = $disk.Lun $vhdname = $disk.vhdname $cacheoption = $disk.HostCaching $disklabel = $disk.DiskLabel $diskName = $disk.DiskName</span></span>

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContextnode2
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix12][22]

<span data-ttu-id="2889a-525">Bunların tümü başarılı kaydedilir kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="2889a-525">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="2889a-526">Tek tek bloblar için daha fazla bilgi için:</span><span class="sxs-lookup"><span data-stu-id="2889a-526">For information for individual blobs:</span></span>

    #Check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContextnode2

#### <a name="step-21-register-os-disk"></a><span data-ttu-id="2889a-527">21. adım: Kayıt işletim sistemi diski</span><span class="sxs-lookup"><span data-stu-id="2889a-527">Step 21: Register OS disk</span></span>
    #change storage account to the new XIO storage account
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

    #Join to existing Avaiability Set

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

    ###This is different to just a straight cloud service change
    #note if you do not have a disk label the command below will fail, populate as required.
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet -Verbose

#### <a name="step-22-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="2889a-528">22. adım: Yük ekleme dengeli uç noktaları ve ACL'leri</span><span class="sxs-lookup"><span data-stu-id="2889a-528">Step 22: Add Load Balanced Endpoints and ACLs</span></span>
    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM


    #STOP!!! CHECK in the Azure portal or Machine Endpoints through PowerShell that these Endpoints are created!

    #SET ACLs or Azure Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

#### <a name="step-23-test-failover"></a><span data-ttu-id="2889a-529">23. adım: Yük devretme sınaması</span><span class="sxs-lookup"><span data-stu-id="2889a-529">Step 23: Test failover</span></span>
<span data-ttu-id="2889a-530">Artık her zaman açık şirket içi düğümle eşitleyin, zaman uyumlu çoğaltma moduna yerleştirileceği ve onu eşitlenene kadar bekleyin geçirilen düğüm izin vermemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="2889a-530">You should now let the migrated node synchronize with the on-premises Always On node, place it in to synchronous replication mode and wait until it is synchronized.</span></span> <span data-ttu-id="2889a-531">Ardından AFP olduğu bir şirket içi yük devretmeyi ilk düğümü geçirildi.</span><span class="sxs-lookup"><span data-stu-id="2889a-531">Then failover from on-prem to the first node migrated, which is the AFP.</span></span> <span data-ttu-id="2889a-532">Çalıştıktan sonra son geçirilen düğüm AFP değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2889a-532">Once that has worked, change the last migrated node to the AFP.</span></span>

<span data-ttu-id="2889a-533">Test yük devretmeleri tüm düğümler arasında ve olarak yük devretme iş emin olmak için chaos testleri bekleniyordu ancak ve zamanında manor çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2889a-533">You should test failovers between all nodes and run though chaos tests to ensure failovers work as expected and in a timely manor.</span></span>

#### <a name="step-24-put-back-cluster-quorum-settings--dns-ttl--failover-pntrs--sync-settings"></a><span data-ttu-id="2889a-534">24. adım: geri küme çekirdek ayarlarını Put / DNS TTL / yük devretme Pntrs / eşitleme ayarları</span><span class="sxs-lookup"><span data-stu-id="2889a-534">Step 24: Put back cluster quorum settings / DNS TTL / Failover Pntrs / Sync Settings</span></span>
##### <a name="adding-ip-address-resource-on-same-subnet"></a><span data-ttu-id="2889a-535">Aynı alt ağdaki IP adresi kaynağı ekleme</span><span class="sxs-lookup"><span data-stu-id="2889a-535">Adding IP Address Resource on Same Subnet</span></span>
<span data-ttu-id="2889a-536">Yalnızca 2 SQL sunucuları var ve yeni bir bulut hizmeti geçirmek istediğiniz ancak aynı alt ağda tutmak istediğiniz özgün her zaman üzerinde IP adresini silin ve yeni IP adresi eklemek için dinleyici çevrimdışı duruma getirmeden önleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2889a-536">If you have only 2 SQL Servers and want to migrate them to a new cloud service, but want to keep them on the same subnet, you can avoid taking the listener offline to delete the original Always On IP Address and add the New IP Address.</span></span> <span data-ttu-id="2889a-537">Başka bir alt ağ için sanal makineleri geçiriyorsanız olacaktır gibi alt başvurur bir ek küme ağı Bunu yapmak gerekmez.</span><span class="sxs-lookup"><span data-stu-id="2889a-537">If you are migrating the VMs to another subnet you will not need to do this as there will be an additional cluster network that will reference that subnet.</span></span>

<span data-ttu-id="2889a-538">Geçirilen ikincil getirildi ve yeni IP adresi kaynak yük devretme varolan birincil önce yeni bulut hizmeti için eklenen sonra bu küme Yük Devretme Yöneticisi içinden adımları izlemesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="2889a-538">Once you have brought up the migrated secondary and added in the new IP Address resource for the new cloud service before failover the existing Primary, you should take these steps within the Cluster Failover Manager:</span></span>

<span data-ttu-id="2889a-539">IP adresi eklemek için bkz: [ek](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), 14. adım.</span><span class="sxs-lookup"><span data-stu-id="2889a-539">To add in IP Address, see the [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), step 14.</span></span>

1. <span data-ttu-id="2889a-540">Geçerli IP adresi kaynağı için 'Varolan birincil SQL Server' için olası sahibi aşağıdaki örnekte, 'dansqlams4' değiştirin:</span><span class="sxs-lookup"><span data-stu-id="2889a-540">For the current IP Address resource, change the possible owner to ‘Existing Primary SQL Server’, in the example below, ‘dansqlams4’:</span></span>

    ![Appendix13][23]
2. <span data-ttu-id="2889a-542">Yeni IP adresi kaynağı için 'Geçirildi ikincil SQL Server', aşağıdaki örnekte, 'dansqlams5' için olası sahip değiştirin:</span><span class="sxs-lookup"><span data-stu-id="2889a-542">For the new IP Address resource, change the possible owner to ‘Migrated secondary SQL Server’, in the example below, ‘dansqlams5’:</span></span>

    ![Appendix14][24]
3. <span data-ttu-id="2889a-544">Son düğümü geçirildiğinde bu düğümü olası sahip olarak eklenir böylece olası sahipler düzenlenmesi gerekir ve bu ayarlandıktan sonra Yük devretme kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2889a-544">Once this is set you can failover, and when the last node is migrated the Possible Owners should be edited so that node is added as a Possible Owner:</span></span>

    ![Appendix15][25]

## <a name="additional-resources"></a><span data-ttu-id="2889a-546">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="2889a-546">Additional resources</span></span>
* [<span data-ttu-id="2889a-547">Azure Premium depolama</span><span class="sxs-lookup"><span data-stu-id="2889a-547">Azure Premium Storage</span></span>](../../../storage/common/storage-premium-storage.md)
* [<span data-ttu-id="2889a-548">Sanal Makineler</span><span class="sxs-lookup"><span data-stu-id="2889a-548">Virtual Machines</span></span>](https://azure.microsoft.com/services/virtual-machines/)
* [<span data-ttu-id="2889a-549">Azure sanal makinelerde SQL Server</span><span class="sxs-lookup"><span data-stu-id="2889a-549">SQL Server in Azure Virtual Machines</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

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
