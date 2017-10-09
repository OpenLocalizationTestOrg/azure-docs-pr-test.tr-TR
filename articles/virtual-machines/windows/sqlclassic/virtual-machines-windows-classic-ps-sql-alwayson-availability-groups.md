---
title: "aaaConfigure hello Always On kullanılabilirlik grubu PowerShell kullanarak Azure VM'de | Microsoft Docs"
description: "Bu öğretici hello Klasik dağıtım modeliyle oluşturulan kaynakları kullanır. Azure PowerShell toocreate Always On kullanılabilirlik grubu kullanın."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a4e2f175-fe56-4218-86c7-a43fb916cc64
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: d4a27e203b2ff299adebec2b010c03422459b3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-always-on-availability-group-on-an-azure-vm-with-powershell"></a><span data-ttu-id="3a0fa-104">PowerShell ile Azure VM'de Hello Always On kullanılabilirlik grubu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3a0fa-104">Configure hello Always On availability group on an Azure VM with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3a0fa-105">Klasik: kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="3a0fa-105">Classic: UI</span></span>](../classic/portal-sql-alwayson-availability-groups.md)
> * <span data-ttu-id="3a0fa-106">[Klasik: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span><span class="sxs-lookup"><span data-stu-id="3a0fa-106">[Classic: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span></span><br/>

<span data-ttu-id="3a0fa-107">Başlamadan önce Azure resource manager modelinde bu görevi tamamlamak olduğunu göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-107">Before you begin, consider that you can now complete this task in Azure resource manager model.</span></span> <span data-ttu-id="3a0fa-108">Azure resource manager modeli yeni dağıtımlar için öneririz.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-108">We recommend Azure resource manager model for new deployments.</span></span> <span data-ttu-id="3a0fa-109">Bkz: [SQL Server Always On kullanılabilirlik grupları'Azure sanal makinelerinde](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3a0fa-109">See [SQL Server Always On availability groups on Azure virtual machines](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3a0fa-110">En yeni dağıtımların hello Resource Manager modelini kullanmasını öneririz.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-110">We recommend that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="3a0fa-111">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3a0fa-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3a0fa-112">Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-112">This article covers using hello classic deployment model.</span></span>

<span data-ttu-id="3a0fa-113">Azure sanal makineleri (VM'ler) Veritabanı yöneticileri toolower hello maliyeti yüksek kullanılabilirlik SQL Server sistem yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-113">Azure virtual machines (VMs) can help database administrators toolower hello cost of a high-availability SQL Server system.</span></span> <span data-ttu-id="3a0fa-114">Bu öğretici nasıl tooimplement bir kullanılabilirlik grubu SQL Server Always On uçtan uca bir Azure ortamı içindeki kullanarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-114">This tutorial shows you how tooimplement an availability group by using SQL Server Always On end-to-end inside an Azure environment.</span></span> <span data-ttu-id="3a0fa-115">Başlangıç Öğreticisi Hello sonunda, Azure, SQL Server Always On çözümünüz öğeleri aşağıdaki Merhaba oluşur:</span><span class="sxs-lookup"><span data-stu-id="3a0fa-115">At hello end of hello tutorial, your SQL Server Always On solution in Azure will consist of hello following elements:</span></span>

* <span data-ttu-id="3a0fa-116">Bir ön uç dahil olmak üzere birden çok alt ağı ve bir arka uç alt ağ içeren bir sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-116">A virtual network that contains multiple subnets, including a front-end and a back-end subnet.</span></span>
* <span data-ttu-id="3a0fa-117">Bir Active Directory etki alanı ile etki alanı denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-117">A domain controller with an Active Directory domain.</span></span>
* <span data-ttu-id="3a0fa-118">Dağıtılan toohello arka uç alt ağı ve Active Directory etki alanına katılmış toohello olan iki SQL Server Vm'lerinin.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-118">Two SQL Server VMs that are deployed toohello back-end subnet and joined toohello Active Directory domain.</span></span>
* <span data-ttu-id="3a0fa-119">Üç düğümlü Windows Yük devretme kümesi hello düğüm çoğunluğu çekirdek modeli.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-119">A three-node Windows failover cluster with hello Node Majority quorum model.</span></span>
* <span data-ttu-id="3a0fa-120">Bir kullanılabilirlik veritabanının bir kullanılabilirlik grubu iki synchronous-commit çoğaltmalarından ile.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-120">An availability group with two synchronous-commit replicas of an availability database.</span></span>

<span data-ttu-id="3a0fa-121">Bu senaryo olduğunda, düşük maliyet veya diğer etkenlere bağlı için değil, Azure üzerinde kendi Basitlik için iyi bir seçimdir.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-121">This scenario is a good choice for its simplicity on Azure, not for its cost-effectiveness or other factors.</span></span> <span data-ttu-id="3a0fa-122">Örneğin, VM'ler hello sayısı iki çoğaltma kullanılabilirlik grubu toosave için işlem saatlerinde azure'da hello etki alanı denetleyicisi hello çekirdek dosya paylaşım tanığı bir iki düğümlü yük devretme kümesi olarak kullanarak en aza indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-122">For example, you can minimize hello number of VMs for a two-replica availability group toosave on compute hours in Azure by using hello domain controller as hello quorum file share witness in a two-node failover cluster.</span></span> <span data-ttu-id="3a0fa-123">Bu yöntem yapılandırma yukarıda hello birinden tarafından hello VM sayısını azaltır.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-123">This method reduces hello VM count by one from hello above configuration.</span></span>

<span data-ttu-id="3a0fa-124">Bu öğreticide gerekli tooset hello ayarlama adımları hello tooshow her adımı hello ayrıntılarını elaborating olmadan çözüm, yukarıda açıklanan amaçlar.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-124">This tutorial is intended tooshow you hello steps that are required tooset up hello described solution above, without elaborating on hello details of each step.</span></span> <span data-ttu-id="3a0fa-125">İsteğe bağlı olarak Hello GUI yapılandırma adımları, PowerShell tootake komut dosyası kullanan sağlanması bu nedenle, yerine hızlı bir şekilde ile her adımı.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-125">Therefore, instead of providing hello GUI configuration steps, it uses PowerShell scripting tootake you quickly through each step.</span></span> <span data-ttu-id="3a0fa-126">Bu öğretici hello aşağıdakileri varsayar:</span><span class="sxs-lookup"><span data-stu-id="3a0fa-126">This tutorial assumes hello following:</span></span>

* <span data-ttu-id="3a0fa-127">Bir Azure hesabı hello sanal makine abonelik zaten var.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-127">You already have an Azure account with hello virtual machine subscription.</span></span>
* <span data-ttu-id="3a0fa-128">Merhaba yüklediğiniz [Azure PowerShell cmdlet'lerini](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3a0fa-128">You've installed hello [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>
* <span data-ttu-id="3a0fa-129">Always On kullanılabilirlik grupları şirket içi çözümler için sağlam bir anlayış zaten var.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-129">You already have a solid understanding of Always On availability groups for on-premises solutions.</span></span> <span data-ttu-id="3a0fa-130">Daha fazla bilgi için bkz: [Always On kullanılabilirlik grupları (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="3a0fa-130">For more information, see [Always On availability groups (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span></span>

## <a name="connect-tooyour-azure-subscription-and-create-hello-virtual-network"></a><span data-ttu-id="3a0fa-131">Tooyour Azure aboneliğini bağlama ve hello sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="3a0fa-131">Connect tooyour Azure subscription and create hello virtual network</span></span>
1. <span data-ttu-id="3a0fa-132">Bir PowerShell penceresinde, yerel bilgisayarınızda hello Azure modülü içe ayarları dosyası tooyour makine yayımlama hello indirin ve indirilen hello yayımlama ayarlarını içeri aktararak, PowerShell oturumu tooyour Azure aboneliği bağlanın.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-132">In a PowerShell window on your local computer, import hello Azure module, download hello publishing settings file tooyour machine, and connect your PowerShell session tooyour Azure subscription by importing hello downloaded publishing settings.</span></span>

        Import-Module "C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\Azure\Azure.psd1"
        Get-AzurePublishSettingsFile
        Import-AzurePublishSettingsFile <publishsettingsfilepath>

    <span data-ttu-id="3a0fa-133">Merhaba **Get-AzurePublishSettingsFile** komutu otomatik olarak Azure yönetim sertifikasıyla oluşturur ve tooyour makine indirir.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-133">hello **Get-AzurePublishSettingsFile** command automatically generates a management certificate with Azure and downloads it tooyour machine.</span></span> <span data-ttu-id="3a0fa-134">Bir tarayıcı otomatik olarak açılır ve istendiğinde tooenter hello Microsoft hesap kimlik bilgilerini Azure aboneliğiniz için demektir.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-134">A browser is automatically opened, and you're prompted tooenter hello Microsoft account credentials for your Azure subscription.</span></span> <span data-ttu-id="3a0fa-135">indirilen hello **.publishsettings** dosyası, Azure aboneliğinizin toomanage gereken tüm hello bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-135">hello downloaded **.publishsettings** file contains all hello information that you need toomanage your Azure subscription.</span></span> <span data-ttu-id="3a0fa-136">Bu dosya tooa yerel dizin kaydedildikten sonra bunu hello kullanarak içeri **Import-AzurePublishSettingsFile** komutu.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-136">After saving this file tooa local directory, import it by using hello **Import-AzurePublishSettingsFile** command.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3a0fa-137">Merhaba .publishsettings dosyasını Azure Abonelikleriniz ve hizmetleri kullanılan tooadminister (kodlanmamış), kimlik bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-137">hello .publishsettings file contains your credentials (unencoded) that are used tooadminister your Azure subscriptions and services.</span></span> <span data-ttu-id="3a0fa-138">Bu dosya için güvenlik en iyi uygulama Hello olan toostore (örneğin, klasöründe hello Libraries\Documents), kaynak dizinlerinizi dışında geçici olarak ve hello içeri aktarma tamamlandıktan sonra silin.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-138">hello security best practice for this file is toostore it temporarily outside your source directories (for example, in hello Libraries\Documents folder), and then delete it after hello import has finished.</span></span> <span data-ttu-id="3a0fa-139">Erişim toohello .publishsettings dosyasını kazanır kötü niyetli bir kullanıcı düzenleme, oluşturma ve Azure hizmetlerinizi silin.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-139">A malicious user who gains access toohello .publishsettings file can edit, create, and delete your Azure services.</span></span>

2. <span data-ttu-id="3a0fa-140">Bir dizi bulut BT altyapısı toocreate kullanacağınız değişkenleri tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-140">Define a series of variables that you'll use toocreate your cloud IT infrastructure.</span></span>

        $location = "West US"
        $affinityGroupName = "ContosoAG"
        $affinityGroupDescription = "Contoso SQL HADR Affinity Group"
        $affinityGroupLabel = "IaaS BI Affinity Group"
        $networkConfigPath = "C:\scripts\Network.netcfg"
        $virtualNetworkName = "ContosoNET"
        $storageAccountName = "<uniquestorageaccountname>"
        $storageAccountLabel = "Contoso SQL HADR Storage Account"
        $storageAccountContainer = "https://" + $storageAccountName + ".blob.core.windows.net/vhds/"
        $winImageName = (Get-AzureVMImage | where {$_.Label -like "Windows Server 2008 R2 SP1*"} | sort PublishedDate -Descending)[0].ImageName
        $sqlImageName = (Get-AzureVMImage | where {$_.Label -like "SQL Server 2012 SP1 Enterprise*"} | sort PublishedDate -Descending)[0].ImageName
        $dcServerName = "ContosoDC"
        $dcServiceName = "<uniqueservicename>"
        $availabilitySetName = "SQLHADR"
        $vmAdminUser = "AzureAdmin"
        $vmAdminPassword = "Contoso!000"
        $workingDir = "c:\scripts\"

    <span data-ttu-id="3a0fa-141">Komutlarınızı daha sonra başarılı olur tooensure aşağıdaki dikkat toohello ödeme:</span><span class="sxs-lookup"><span data-stu-id="3a0fa-141">Pay attention toohello following tooensure that your commands will succeed later:</span></span>

   * <span data-ttu-id="3a0fa-142">Değişkenleri **$storageAccountName** ve **$dcServiceName** oldukları için benzersiz olmalıdır tooidentify bulut depolama hesabı ve bulut sunucusu, sırasıyla hello Internet üzerinde kullanılan.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-142">Variables **$storageAccountName** and **$dcServiceName** must be unique because they're used tooidentify your cloud storage account and cloud server, respectively, on hello Internet.</span></span>
   * <span data-ttu-id="3a0fa-143">Merhaba değişkenleri belirtir adları **$affinityGroupName** ve **$virtualNetworkName** daha sonra kullanacağınız hello sanal ağ yapılandırması belgede yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-143">hello names that you specify for variables **$affinityGroupName** and **$virtualNetworkName** are configured in hello virtual network configuration document that you'll use later.</span></span>
   * <span data-ttu-id="3a0fa-144">**$sqlImageName** , SQL Server 2012 Service Pack 1 Enterprise Edition içeren hello VM görüntüsü güncelleştirilmiş hello adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-144">**$sqlImageName** specifies hello updated name of hello VM image that contains SQL Server 2012 Service Pack 1 Enterprise Edition.</span></span>
   * <span data-ttu-id="3a0fa-145">Basitleştirmek için **Contoso! 000** olduğundan, hello aynı hello tüm Öğreticisi kullanılan parola.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-145">For simplicity, **Contoso!000** is hello same password that's used throughout hello entire tutorial.</span></span>

3. <span data-ttu-id="3a0fa-146">Bir benzeşim grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-146">Create an affinity group.</span></span>

        New-AzureAffinityGroup `
            -Name $affinityGroupName `
            -Location $location `
            -Description $affinityGroupDescription `
            -Label $affinityGroupLabel

4. <span data-ttu-id="3a0fa-147">Bir yapılandırma dosyasını içeri aktararak bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-147">Create a virtual network by importing a configuration file.</span></span>

        Set-AzureVNetConfig `
            -ConfigurationPath $networkConfigPath

    <span data-ttu-id="3a0fa-148">XML belgesi aşağıdaki hello Hello yapılandırma dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-148">hello configuration file contains hello following XML document.</span></span> <span data-ttu-id="3a0fa-149">Kısaca, adlı bir sanal ağ belirtir **ContosoNET** hello benzeşim adlı grubundaki **ContosoAG**.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-149">In brief, it specifies a virtual network called **ContosoNET** in hello affinity group called **ContosoAG**.</span></span> <span data-ttu-id="3a0fa-150">Merhaba adres alanına sahip **10.10.0.0/16** ve iki alt ağa sahip **10.10.1.0/24** ve **10.10.2.0/24**, olan hello ön alt ağı ve geri alt ağ, sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-150">It has hello address space **10.10.0.0/16** and has two subnets, **10.10.1.0/24** and **10.10.2.0/24**, which are hello front subnet and back subnet, respectively.</span></span> <span data-ttu-id="3a0fa-151">Burada, Microsoft SharePoint gibi istemci uygulamalarını yerleştirebilirsiniz Hello ön alt ağıdır.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-151">hello front subnet is where you can place client applications such as Microsoft SharePoint.</span></span> <span data-ttu-id="3a0fa-152">Merhaba SQL Server Vm'lerinin nereye Hello geri alt ağıdır.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-152">hello back subnet is where you'll place hello SQL Server VMs.</span></span> <span data-ttu-id="3a0fa-153">Merhaba değiştirirseniz **$affinityGroupName** ve **$virtualNetworkName** değişkenleri daha önce de değiştirmelisiniz adları karşılık gelen hello.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-153">If you change hello **$affinityGroupName** and **$virtualNetworkName** variables earlier, you must also change hello corresponding names below.</span></span>

        <NetworkConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <Dns />
            <VirtualNetworkSites>
              <VirtualNetworkSite name="ContosoNET" AffinityGroup="ContosoAG">
                <AddressSpace>
                  <AddressPrefix>10.10.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="Front">
                    <AddressPrefix>10.10.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="Back">
                    <AddressPrefix>10.10.2.0/24</AddressPrefix>
                  </Subnet>
                </Subnets>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

5. <span data-ttu-id="3a0fa-154">Merhaba benzeşim oluşturulur ve aboneliğinizde hello geçerli depolama hesabı olarak ayarlanmış grubu ile ilişkili bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-154">Create a storage account that's associated with hello affinity group that you created, and set it as hello current storage account in your subscription.</span></span>

        New-AzureStorageAccount `
            -StorageAccountName $storageAccountName `
            -Label $storageAccountLabel `
            -AffinityGroup $affinityGroupName
        Set-AzureSubscription `
            -SubscriptionName (Get-AzureSubscription).SubscriptionName `
            -CurrentStorageAccount $storageAccountName

6. <span data-ttu-id="3a0fa-155">Merhaba etki alanı denetleyicisi sunucusuna hello yeni bulut hizmeti ve kullanılabilirlik kümesinde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-155">Create hello domain controller server in hello new cloud service and availability set.</span></span>

        New-AzureVMConfig `
            -Name $dcServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$dcServerName.vhd" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -Windows `
                -DisableAutomaticUpdates `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword |
                New-AzureVM `
                    -ServiceName $dcServiceName `
                    –AffinityGroup $affinityGroupName `
                    -VNetName $virtualNetworkName

    <span data-ttu-id="3a0fa-156">Bu piped komutları şeyleri hello:</span><span class="sxs-lookup"><span data-stu-id="3a0fa-156">These piped commands do hello following things:</span></span>

   * <span data-ttu-id="3a0fa-157">**AzureVMConfig yeni** bir VM yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-157">**New-AzureVMConfig** creates a VM configuration.</span></span>
   * <span data-ttu-id="3a0fa-158">**Ekleme AzureProvisioningConfig** verir hello bir tek başına Windows server'ın yapılandırma parametreleri.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-158">**Add-AzureProvisioningConfig** gives hello configuration parameters of a standalone Windows server.</span></span>
   * <span data-ttu-id="3a0fa-159">**Ekleme AzureDataDisk** seçenek kümesi tooNone önbelleğe alma hello ile Active Directory verilerini depolamak için kullanacağınız hello veri diski ekler.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-159">**Add-AzureDataDisk** adds hello data disk that you'll use for storing Active Directory data, with hello caching option set tooNone.</span></span>
   * <span data-ttu-id="3a0fa-160">**Yeni-AzureVM** yeni bir bulut hizmeti ve oluşturur Yeni Azure VM hello yeni bulut hizmeti ile Merhaba.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-160">**New-AzureVM** creates a new cloud service and creates hello new Azure VM in hello new cloud service.</span></span>

7. <span data-ttu-id="3a0fa-161">Tam olarak sağlanan hello yeni VM toobe için bekleyin ve hello Uzak Masaüstü dosyası tooyour çalışma dizini indirin.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-161">Wait for hello new VM toobe fully provisioned, and download hello remote desktop file tooyour working directory.</span></span> <span data-ttu-id="3a0fa-162">Merhaba yeni Azure VM uzun süre tooprovision aldığından hello `while` döngünün devam toopoll kullanıma hazır olana kadar yeni VM hello.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-162">Because hello new Azure VM takes a long time tooprovision, hello `while` loop continues toopoll hello new VM until it's ready for use.</span></span>

        $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName

        While ($VMStatus.InstanceStatus -ne "ReadyRole")
        {
            write-host "Waiting for " $VMStatus.Name "... Current Status = " $VMStatus.InstanceStatus
            Start-Sleep -Seconds 15
            $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName
        }

        Get-AzureRemoteDesktopFile `
            -ServiceName $dcServiceName `
            -Name $dcServerName `
            -LocalPath "$workingDir$dcServerName.rdp"

<span data-ttu-id="3a0fa-163">Merhaba etki alanı denetleyici sunucusu artık başarıyla kaynak sağlandı.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-163">hello domain controller server is now successfully provisioned.</span></span> <span data-ttu-id="3a0fa-164">Ardından, bu etki alanı denetleyicisi sunucusuna hello Active Directory etki alanı yapılandıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-164">Next, you'll configure hello Active Directory domain on this domain controller server.</span></span> <span data-ttu-id="3a0fa-165">Yerel bilgisayarınızda Hello PowerShell penceresini açık bırakın.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-165">Leave hello PowerShell window open on your local computer.</span></span> <span data-ttu-id="3a0fa-166">Kullanacağınız yeniden sonraki toocreate hello iki SQL Server VM.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-166">You'll use it again later toocreate hello two SQL Server VMs.</span></span>

## <a name="configure-hello-domain-controller"></a><span data-ttu-id="3a0fa-167">Merhaba etki alanı denetleyicisini Yapılandır</span><span class="sxs-lookup"><span data-stu-id="3a0fa-167">Configure hello domain controller</span></span>
1. <span data-ttu-id="3a0fa-168">Merhaba Uzak Masaüstü dosyası başlatarak toohello etki alanı denetleyicisi sunucusuna bağlanın.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-168">Connect toohello domain controller server by launching hello remote desktop file.</span></span> <span data-ttu-id="3a0fa-169">Merhaba makine yöneticisinin AzureAdmin kullanıcı adı ve parolası kullanmak **Contoso! 000**, oluşturduğunuzda belirttiğiniz yeni VM hello.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-169">Use hello machine administrator’s username AzureAdmin and password **Contoso!000**, which you specified when you created hello new VM.</span></span>
2. <span data-ttu-id="3a0fa-170">Yönetici modunda bir PowerShell penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-170">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="3a0fa-171">Merhaba aşağıdaki komutu çalıştırarak **DCPROMO. EXE** hello yukarı komutu tooset **corp.contoso.com** M sürücüsü hello veri dizinleri ile etki alanı.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-171">Run hello following **DCPROMO.EXE** command tooset up hello **corp.contoso.com** domain, with hello data directories on drive M.</span></span>

        dcpromo.exe `
            /unattend `
            /ReplicaOrNewDomain:Domain `
            /NewDomain:Forest `
            /NewDomainDNSName:corp.contoso.com `
            /ForestLevel:4 `
            /DomainNetbiosName:CORP `
            /DomainLevel:4 `
            /InstallDNS:Yes `
            /ConfirmGc:Yes `
            /CreateDNSDelegation:No `
            /DatabasePath:"C:\Windows\NTDS" `
            /LogPath:"C:\Windows\NTDS" `
            /SYSVOLPath:"C:\Windows\SYSVOL" `
            /SafeModeAdminPassword:"Contoso!000"

    <span data-ttu-id="3a0fa-172">Merhaba VM Hello komut bittikten sonra otomatik olarak yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-172">After hello command finishes, hello VM restarts automatically.</span></span>

4. <span data-ttu-id="3a0fa-173">Merhaba Uzak Masaüstü dosyası başlatarak toohello etki alanı denetleyicisi sunucusuna yeniden bağlanın.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-173">Connect toohello domain controller server again by launching hello remote desktop file.</span></span> <span data-ttu-id="3a0fa-174">Bu süre olarak oturum açın **CORP\Administrator**.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-174">This time, sign in as **CORP\Administrator**.</span></span>
5. <span data-ttu-id="3a0fa-175">Yönetici modunda bir PowerShell penceresi açın ve komut aşağıdaki hello kullanarak hello Active Directory PowerShell modülünü içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="3a0fa-175">Open a PowerShell window in administrator mode, and import hello Active Directory PowerShell module by using hello following command:</span></span>

        Import-Module ActiveDirectory

6. <span data-ttu-id="3a0fa-176">Aşağıdaki komutları tooadd üç kullanıcılar toohello etki alanı hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-176">Run hello following commands tooadd three users toohello domain.</span></span>

        $pwd = ConvertTo-SecureString "Contoso!000" -AsPlainText -Force
        New-ADUser `
            -Name 'Install' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc1' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc2' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true

    <span data-ttu-id="3a0fa-177">**CORP\Install** kullanılan tooconfigure her şeyi olan ilgili toohello SQL Sunucu hizmeti örneği, hello yük devretme kümesi ve hello kullanılabilirlik grubu.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-177">**CORP\Install** is used tooconfigure everything related toohello SQL Server service instances, hello failover cluster, and hello availability group.</span></span> <span data-ttu-id="3a0fa-178">**CORP\SQLSvc1** ve **CORP\SQLSvc2** hello SQL Server hizmet hesabı olarak hello iki SQL Server VM'ler için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-178">**CORP\SQLSvc1** and **CORP\SQLSvc2** are used as hello SQL Server service accounts for hello two SQL Server VMs.</span></span>
7. <span data-ttu-id="3a0fa-179">Ardından, çalışma hello aşağıdaki komutları toogive **CORP\Install** hello hello etki alanındaki izinleri toocreate bilgisayar nesneleri.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-179">Next, run hello following commands toogive **CORP\Install** hello permissions toocreate computer objects in hello domain.</span></span>

        Cd ad:
        $sid = new-object System.Security.Principal.SecurityIdentifier (Get-ADUser "Install").SID
        $guid = new-object Guid bf967a86-0de6-11d0-a285-00aa003049e2
        $ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid,"CreateChild","Allow",$guid,"All"
        $corp = Get-ADObject -Identity "DC=corp,DC=contoso,DC=com"
        $acl = Get-Acl $corp
        $acl.AddAccessRule($ace1)
        Set-Acl -Path "DC=corp,DC=contoso,DC=com" -AclObject $acl

    <span data-ttu-id="3a0fa-180">Merhaba yukarıda belirtilen GUID hello GUID hello bilgisayar nesnesi türü için ' dir.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-180">hello GUID specified above is hello GUID for hello computer object type.</span></span> <span data-ttu-id="3a0fa-181">Merhaba **CORP\Install** hesabının gerekir hello **tüm özellikleri oku** ve **bilgisayar nesneleri oluşturma** izin toocreate hello etkin doğrudan hello yük devretme için nesneleri Küme.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-181">hello **CORP\Install** account needs hello **Read All Properties** and **Create Computer Objects** permission toocreate hello Active Direct objects for hello failover cluster.</span></span> <span data-ttu-id="3a0fa-182">Merhaba **tüm özellikleri oku** izni zaten verilen tooCORP\Install varsayılan olarak, yani toogrant gerekiyor mu, açıkça.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-182">hello **Read All Properties** permission is already given tooCORP\Install by default, so you don't need toogrant it explicitly.</span></span> <span data-ttu-id="3a0fa-183">İzinler hakkında daha fazla bilgi toocreate hello yük devretme küme gerektiği için bkz: [yük devretme kümesi adım adım Kılavuzu: Active Directory hesaplarını yapılandırma](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="3a0fa-183">For more information on permissions that are needed toocreate hello failover cluster, see [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).</span></span>

    <span data-ttu-id="3a0fa-184">Active Directory ve hello kullanıcı nesneleri yapılandırma bitirdikten sonra iki SQL Server VM oluşturun ve bunları toothis etki alanına katılma.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-184">Now that you've finished configuring Active Directory and hello user objects, you'll create two SQL Server VMs and join them toothis domain.</span></span>

## <a name="create-hello-sql-server-vms"></a><span data-ttu-id="3a0fa-185">Merhaba SQL Server Vm'lerinin oluşturma</span><span class="sxs-lookup"><span data-stu-id="3a0fa-185">Create hello SQL Server VMs</span></span>
1. <span data-ttu-id="3a0fa-186">Yerel bilgisayarınızda açık toouse hello PowerShell penceresi devam edin.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-186">Continue toouse hello PowerShell window that's open on your local computer.</span></span> <span data-ttu-id="3a0fa-187">Ek değişkenler aşağıdaki hello tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="3a0fa-187">Define hello following additional variables:</span></span>

        $domainName= "corp"
        $FQDN = "corp.contoso.com"
        $subnetName = "Back"
        $sqlServiceName = "<uniqueservicename>"
        $quorumServerName = "ContosoQuorum"
        $sql1ServerName = "ContosoSQL1"
        $sql2ServerName = "ContosoSQL2"
        $availabilitySetName = "SQLHADR"
        $dataDiskSize = 100
        $dnsSettings = New-AzureDns -Name "ContosoBackDNS" -IPAddress "10.10.0.4"

    <span data-ttu-id="3a0fa-188">Merhaba IP adresi **10.10.0.4** toohello genellikle atanan hello oluşturduğunuz ilk VM **10.10.0.0/16** Azure sanal ağınızın alt ağ.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-188">hello IP address **10.10.0.4** is typically assigned toohello first VM that you create in hello **10.10.0.0/16** subnet of your Azure virtual network.</span></span> <span data-ttu-id="3a0fa-189">Bu etki alanı denetleyicisi sunucunuzun hello adresini çalıştırarak olduğunu doğrulamalısınız **IPCONFIG**.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-189">You should verify that this is hello address of your domain controller server by running **IPCONFIG**.</span></span>
2. <span data-ttu-id="3a0fa-190">Yöneltilen komutları toocreate hello önce aşağıdaki çalışma hello hello yük devretme kümesinde, VM adlı **ContosoQuorum**:</span><span class="sxs-lookup"><span data-stu-id="3a0fa-190">Run hello following piped commands toocreate hello first VM in hello failover cluster, named **ContosoQuorum**:</span></span>

        New-AzureVMConfig `
            -Name $quorumServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$quorumServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    New-AzureVM `
                        -ServiceName $sqlServiceName `
                        –AffinityGroup $affinityGroupName `
                        -VNetName $virtualNetworkName `
                        -DnsSettings $dnsSettings

    <span data-ttu-id="3a0fa-191">Yukarıdaki hello komutu ilgili Hello aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="3a0fa-191">Note hello following regarding hello command above:</span></span>

   * <span data-ttu-id="3a0fa-192">**AzureVMConfig yeni** hello istenen kullanılabilirlik kümesi adı ile bir VM yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-192">**New-AzureVMConfig** creates a VM configuration with hello desired availability set name.</span></span> <span data-ttu-id="3a0fa-193">Merhaba sonraki VM'ler ile Merhaba aynı oluşturulacak kullanılabilirlik kümesi adı birleştirilmiş böylece toohello aynı kullanılabilirlik kümesi.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-193">hello subsequent VMs will be created with hello same availability set name so that they're joined toohello same availability set.</span></span>
   * <span data-ttu-id="3a0fa-194">**Ekleme AzureProvisioningConfig** birleştirmeler hello oluşturduğunuz VM toohello Active Directory etki alanı.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-194">**Add-AzureProvisioningConfig** joins hello VM toohello Active Directory domain that you created.</span></span>
   * <span data-ttu-id="3a0fa-195">**Set-AzureSubnet** hello geri alt ağda yer hello VM.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-195">**Set-AzureSubnet** places hello VM in hello back subnet.</span></span>
   * <span data-ttu-id="3a0fa-196">**Yeni-AzureVM** yeni bir bulut hizmeti ve oluşturur Yeni Azure VM hello yeni bulut hizmeti ile Merhaba.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-196">**New-AzureVM** creates a new cloud service and creates hello new Azure VM in hello new cloud service.</span></span> <span data-ttu-id="3a0fa-197">Merhaba **DnsSettings** parametresi belirtir hello DNS sunucu hello hello yeni bulut hizmetindeki sunucular için başlangıç IP adresi **10.10.0.4**.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-197">hello **DnsSettings** parameter specifies that hello DNS server for hello servers in hello new cloud service has hello IP address **10.10.0.4**.</span></span> <span data-ttu-id="3a0fa-198">Başlangıç IP adresi hello etki alanı denetleyici sunucusu budur.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-198">This is hello IP address of hello domain controller server.</span></span> <span data-ttu-id="3a0fa-199">Bu parametre gerekli tooenable hello hello bulut hizmeti toojoin toohello Active Directory etki alanındaki yeni VM'ler başarıyla.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-199">This parameter is needed tooenable hello new VMs in hello cloud service toojoin toohello Active Directory domain successfully.</span></span> <span data-ttu-id="3a0fa-200">Merhaba VM sağlanır ve hello VM toohello Active Directory etki alanına katılma sonra bu parametre olmadan, el ile Merhaba IPv4 ayarları VM toouse hello etki alanı denetleyicisi sunucunuzda hello birincil DNS sunucusu olarak ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-200">Without this parameter, you must manually set hello IPv4 settings in your VM toouse hello domain controller server as hello primary DNS server after hello VM is provisioned, and then join hello VM toohello Active Directory domain.</span></span>
3. <span data-ttu-id="3a0fa-201">Çalışma hello yöneltilen aşağıdaki komutları adlı toocreate hello SQL Server Vm'lerinin **ContosoSQL1** ve **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-201">Run hello following piped commands toocreate hello SQL Server VMs, named **ContosoSQL1** and **ContosoSQL2**.</span></span>

        # Create ContosoSQL1...
        New-AzureVMConfig `
            -Name $sql1ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql1ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 1 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

        # Create ContosoSQL2...
        New-AzureVMConfig `
            -Name $sql2ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql2ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 2 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

    <span data-ttu-id="3a0fa-202">Yukarıdaki hello komutları ilgili Hello aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="3a0fa-202">Note hello following regarding hello commands above:</span></span>

   * <span data-ttu-id="3a0fa-203">**AzureVMConfig yeni** kullandığı hello hello etki alanı denetleyici sunucusu olarak aynı kullanılabilirlik kümesi adı ve kullandığı hello hello sanal makine Galerisi SQL Server 2012 Service Pack 1 Enterprise Edition görüntüde.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-203">**New-AzureVMConfig** uses hello same availability set name as hello domain controller server, and uses hello SQL Server 2012 Service Pack 1 Enterprise Edition image in hello virtual machine gallery.</span></span> <span data-ttu-id="3a0fa-204">Ayrıca, işletim sistemi disk tooread (hiçbir yazma önbelleğini) önbelleğe alma yalnızca hello ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-204">It also sets hello operating system disk tooread-caching only (no write caching).</span></span> <span data-ttu-id="3a0fa-205">Toohello VM eklemek ve okuma ile yapılandırmak veya önbelleğe alma yazma olduğunu hello veritabanı dosyaları tooa ayrı veri diski yükseltmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-205">We recommend that you migrate hello database files tooa separate data disk that you attach toohello VM, and configure it with no read or write caching.</span></span> <span data-ttu-id="3a0fa-206">Ancak, hello sonraki en iyi, kaldırılamıyor çünkü tooremove hello işletim sistemi diskte yazma önbelleğini hello işletim sistemi disk üzerinde okuma şeydir.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-206">However, hello next best thing is tooremove write caching on hello operating system disk because you can't remove read caching on hello operating system disk.</span></span>
   * <span data-ttu-id="3a0fa-207">**Ekleme AzureProvisioningConfig** birleştirmeler hello oluşturduğunuz VM toohello Active Directory etki alanı.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-207">**Add-AzureProvisioningConfig** joins hello VM toohello Active Directory domain that you created.</span></span>
   * <span data-ttu-id="3a0fa-208">**Set-AzureSubnet** hello geri alt ağda yer hello VM.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-208">**Set-AzureSubnet** places hello VM in hello back subnet.</span></span>
   * <span data-ttu-id="3a0fa-209">**Ekleme AzureEndpoint** istemci uygulamalarının bu SQL Server Hizmetleri örnekleri hello Internet üzerinde erişebilmesi için erişim uç noktaları ekler.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-209">**Add-AzureEndpoint** adds access endpoints so that client applications can access these SQL Server services instances on hello Internet.</span></span> <span data-ttu-id="3a0fa-210">Farklı bağlantı noktaları tooContosoSQL1 ve ContosoSQL2 verilir.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-210">Different ports are given tooContosoSQL1 and ContosoSQL2.</span></span>
   * <span data-ttu-id="3a0fa-211">**Yeni-AzureVM** oluşturur Yeni SQL Server VM hello hello aynı ContosoQuorum bulut hizmeti.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-211">**New-AzureVM** creates hello new SQL Server VM in hello same cloud service as ContosoQuorum.</span></span> <span data-ttu-id="3a0fa-212">Aynı bulut hizmetine olmalarını istiyorsanız içinde toobe hello hello VM'ler koymanız gerekir hello aynı kullanılabilirlik kümesi.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-212">You must place hello VMs in hello same cloud service if you want them toobe in hello same availability set.</span></span>
4. <span data-ttu-id="3a0fa-213">Her VM toodownload ve tam olarak sağlanan her VM toobe için Uzak Masaüstü dosyası tooyour çalışma dizini bekleyin.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-213">Wait for each VM toobe fully provisioned and for each VM toodownload its remote desktop file tooyour working directory.</span></span> <span data-ttu-id="3a0fa-214">Merhaba `for` döngü döngüleri hello üç yeni VM'ler ve bunların her biri için hello komutları hello en üst düzey süslü ayraç içinde yürütür.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-214">hello `for` loop cycles through hello three new VMs and executes hello commands inside hello top-level curly brackets for each of them.</span></span>

        Foreach ($VM in $VMs = Get-AzureVM -ServiceName $sqlServiceName)
        {
            write-host "Waiting for " $VM.Name "..."

            # Loop until hello VM status is "ReadyRole"
            While ($VM.InstanceStatus -ne "ReadyRole")
            {
                write-host "  Current Status = " $VM.InstanceStatus
                Start-Sleep -Seconds 15
                $VM = Get-AzureVM -ServiceName $VM.ServiceName -Name $VM.InstanceName
            }

            write-host "  Current Status = " $VM.InstanceStatus

            # Download remote desktop file
            Get-AzureRemoteDesktopFile -ServiceName $VM.ServiceName -Name $VM.InstanceName -LocalPath "$workingDir$($VM.InstanceName).rdp"
        }

    <span data-ttu-id="3a0fa-215">Merhaba SQL Server Vm'lerinin şimdi sağlanır ve çalışıyor, ancak bunlar varsayılan seçeneklerle SQL Server ile birlikte yüklenen.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-215">hello SQL Server VMs are now provisioned and running, but they're installed with SQL Server with default options.</span></span>

## <a name="initialize-hello-failover-cluster-vms"></a><span data-ttu-id="3a0fa-216">Merhaba yük devretme kümesi sanal makineleri Başlat</span><span class="sxs-lookup"><span data-stu-id="3a0fa-216">Initialize hello failover cluster VMs</span></span>
<span data-ttu-id="3a0fa-217">Bu bölümde, hello yük devretme kümesi ve hello SQL Server yüklemesi kullanacağınız toomodify hello üç sunucu gerekir.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-217">In this section, you need toomodify hello three servers that you'll use in hello failover cluster and hello SQL Server installation.</span></span> <span data-ttu-id="3a0fa-218">Bu avantajlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="3a0fa-218">Specifically:</span></span>

* <span data-ttu-id="3a0fa-219">Tüm sunucuları: tooinstall hello gereksinim **Yük Devretme Kümelemesi** özelliği.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-219">All servers: You need tooinstall hello **Failover Clustering** feature.</span></span>
* <span data-ttu-id="3a0fa-220">Tüm sunucuları: tooadd gerek **CORP\Install** hello makine olarak **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-220">All servers: You need tooadd **CORP\Install** as hello machine **administrator**.</span></span>
* <span data-ttu-id="3a0fa-221">ContosoSQL1 ve yalnızca ContosoSQL2: tooadd gerek **CORP\Install** olarak bir **sysadmin** hello varsayılan veritabanı rolü.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-221">ContosoSQL1 and ContosoSQL2 only: You need tooadd **CORP\Install** as a **sysadmin** role in hello default database.</span></span>
* <span data-ttu-id="3a0fa-222">ContosoSQL1 ve yalnızca ContosoSQL2: tooadd gerek **NT AUTHORITY\SYSTEM** bir ile oturum açma aşağıdaki izinleri hello olarak:</span><span class="sxs-lookup"><span data-stu-id="3a0fa-222">ContosoSQL1 and ContosoSQL2 only: You need tooadd **NT AUTHORITY\System** as a sign-in with hello following permissions:</span></span>

  * <span data-ttu-id="3a0fa-223">Herhangi bir kullanılabilirlik grubu Değiştir</span><span class="sxs-lookup"><span data-stu-id="3a0fa-223">Alter any availability group</span></span>
  * <span data-ttu-id="3a0fa-224">SQL bağlantı</span><span class="sxs-lookup"><span data-stu-id="3a0fa-224">Connect SQL</span></span>
  * <span data-ttu-id="3a0fa-225">VIEW server state</span><span class="sxs-lookup"><span data-stu-id="3a0fa-225">View server state</span></span>
* <span data-ttu-id="3a0fa-226">ContosoSQL1 ve yalnızca ContosoSQL2: Merhaba **TCP** Protokolü hello SQL Server VM üzerinde zaten etkin.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-226">ContosoSQL1 and ContosoSQL2 only: hello **TCP** protocol is already enabled on hello SQL Server VM.</span></span> <span data-ttu-id="3a0fa-227">Ancak, yine tooopen hello Güvenlik Duvarı için SQL Server'ın uzaktan erişim gerekir.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-227">However, you still need tooopen hello firewall for remote access of SQL Server.</span></span>

<span data-ttu-id="3a0fa-228">Şimdi, hazır toostart demektir.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-228">Now, you're ready toostart.</span></span> <span data-ttu-id="3a0fa-229">İle başlayarak **ContosoQuorum**, hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="3a0fa-229">Beginning with **ContosoQuorum**, follow hello steps below:</span></span>

1. <span data-ttu-id="3a0fa-230">Çok bağlanmak**ContosoQuorum** hello Uzak Masaüstü dosyaları başlatmasını tarafından.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-230">Connect too**ContosoQuorum** by launching hello remote desktop files.</span></span> <span data-ttu-id="3a0fa-231">Merhaba makine yöneticisinin kullanıcı adı kullanma **AzureAdmin** ve parola **Contoso! 000**, hello VM'ler oluşturduğunuzda belirttiğiniz.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-231">Use hello machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created hello VMs.</span></span>
2. <span data-ttu-id="3a0fa-232">Merhaba bilgisayarlar başarıyla çok birleştirilmiş olan doğrulayın**corp.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-232">Verify that hello computers have been successfully joined too**corp.contoso.com**.</span></span>
3. <span data-ttu-id="3a0fa-233">Devam etmeden önce hello otomatik başlatma görevlerini çalıştıran hello SQL Server yükleme toofinish bekleyin.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-233">Wait for hello SQL Server installation toofinish running hello automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="3a0fa-234">Yönetici modunda bir PowerShell penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-234">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="3a0fa-235">Merhaba Windows Yük Devretme Kümelemesi özelliğini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-235">Install hello Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="3a0fa-236">Ekleme **CORP\Install** yerel yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-236">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="3a0fa-237">ContosoQuorum dışında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-237">Sign out of ContosoQuorum.</span></span> <span data-ttu-id="3a0fa-238">Bu sunucu ile artık bitirdiniz.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-238">You're done with this server now.</span></span>

        logoff.exe

<span data-ttu-id="3a0fa-239">Ardından, başlatma **ContosoSQL1** ve **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-239">Next, initialize **ContosoSQL1** and **ContosoSQL2**.</span></span> <span data-ttu-id="3a0fa-240">Her iki SQL Server VM'ler için aynı olan hello aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-240">Follow hello steps below, which are identical for both SQL Server VMs.</span></span>

1. <span data-ttu-id="3a0fa-241">Toohello iki SQL Server Vm'lerinin hello Uzak Masaüstü dosyaları başlatarak bağlayın.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-241">Connect toohello two SQL Server VMs by launching hello remote desktop files.</span></span> <span data-ttu-id="3a0fa-242">Merhaba makine yöneticisinin kullanıcı adı kullanma **AzureAdmin** ve parola **Contoso! 000**, hello VM'ler oluşturduğunuzda belirttiğiniz.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-242">Use hello machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created hello VMs.</span></span>
2. <span data-ttu-id="3a0fa-243">Merhaba bilgisayarlar başarıyla çok birleştirilmiş olan doğrulayın**corp.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-243">Verify that hello computers have been successfully joined too**corp.contoso.com**.</span></span>
3. <span data-ttu-id="3a0fa-244">Devam etmeden önce hello otomatik başlatma görevlerini çalıştıran hello SQL Server yükleme toofinish bekleyin.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-244">Wait for hello SQL Server installation toofinish running hello automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="3a0fa-245">Yönetici modunda bir PowerShell penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-245">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="3a0fa-246">Merhaba Windows Yük Devretme Kümelemesi özelliğini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-246">Install hello Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="3a0fa-247">Ekleme **CORP\Install** yerel yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-247">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="3a0fa-248">SQL Server PowerShell sağlayıcısı Hello içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-248">Import hello SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy -Execution RemoteSigned -Force
        Import-Module -Name "sqlps" -DisableNameChecking
8. <span data-ttu-id="3a0fa-249">Ekleme **CORP\Install** hello varsayılan SQL Server örneği için hello sysadmin rolü olarak.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-249">Add **CORP\Install** as hello sysadmin role for hello default SQL Server instance.</span></span>

        net localgroup administrators "CORP\Install" /Add
        Invoke-SqlCmd -Query "EXEC sp_addsrvrolemember 'CORP\Install', 'sysadmin'" -ServerInstance "."
9. <span data-ttu-id="3a0fa-250">Ekleme **NT AUTHORITY\SYSTEM** bir oturum açma yukarıda açıklanan hello üç izinlerle olarak.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-250">Add **NT AUTHORITY\System** as a sign-in with hello three permissions described above.</span></span>

        Invoke-SqlCmd -Query "CREATE LOGIN [NT AUTHORITY\SYSTEM] FROM WINDOWS" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT ALTER ANY AVAILABILITY GROUP too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT CONNECT SQL too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT VIEW SERVER STATE too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
10. <span data-ttu-id="3a0fa-251">SQL Server'ın uzaktan erişim için Hello Güvenlik Duvarı'nı açın.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-251">Open hello firewall for remote access of SQL Server.</span></span>

         netsh advfirewall firewall add rule name='SQL Server (TCP-In)' program='C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe' dir=in action=allow protocol=TCP
11. <span data-ttu-id="3a0fa-252">Her iki VM dışında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-252">Sign out of both VMs.</span></span>

         logoff.exe

<span data-ttu-id="3a0fa-253">Son olarak, hazır tooconfigure hello kullanılabilirlik grubu demektir.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-253">Finally, you're ready tooconfigure hello availability group.</span></span> <span data-ttu-id="3a0fa-254">Tüm hello çalışacak hello SQL Server PowerShell sağlayıcısı tooperform kullanacağınız **ContosoSQL1**.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-254">You'll use hello SQL Server PowerShell Provider tooperform all of hello work on **ContosoSQL1**.</span></span>

## <a name="configure-hello-availability-group"></a><span data-ttu-id="3a0fa-255">Merhaba kullanılabilirlik grubunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3a0fa-255">Configure hello availability group</span></span>
1. <span data-ttu-id="3a0fa-256">Çok bağlanmak**ContosoSQL1** hello Uzak Masaüstü dosyaları başlatmasını tarafından yeniden.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-256">Connect too**ContosoSQL1** again by launching hello remote desktop files.</span></span> <span data-ttu-id="3a0fa-257">Yerine Hello makine hesabı kullanarak oturum açma kullanarak oturum açın **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-257">Instead of signing in by using hello machine account, sign in by using **CORP\Install**.</span></span>
2. <span data-ttu-id="3a0fa-258">Yönetici modunda bir PowerShell penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-258">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="3a0fa-259">Değişkenleri aşağıdaki hello tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="3a0fa-259">Define hello following variables:</span></span>

        $server1 = "ContosoSQL1"
        $server2 = "ContosoSQL2"
        $serverQuorum = "ContosoQuorum"
        $acct1 = "CORP\SQLSvc1"
        $acct2 = "CORP\SQLSvc2"
        $password = "Contoso!000"
        $clusterName = "Cluster1"
        $timeout = New-Object System.TimeSpan -ArgumentList 0, 0, 30
        $db = "MyDB1"
        $backupShare = "\\$server1\backup"
        $quorumShare = "\\$server1\quorum"
        $ag = "AG1"
4. <span data-ttu-id="3a0fa-260">SQL Server PowerShell sağlayıcısı Hello içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-260">Import hello SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy RemoteSigned -Force
        Import-Module "sqlps" -DisableNameChecking
5. <span data-ttu-id="3a0fa-261">Merhaba SQL Server hizmet hesabını ContosoSQL1 tooCORP\SQLSvc1 değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-261">Change hello SQL Server service account for ContosoSQL1 tooCORP\SQLSvc1.</span></span>

        $wmi1 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server1
        $wmi1.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct1,$password)}
        $svc1 = Get-Service -ComputerName $server1 -Name 'MSSQLSERVER'
        $svc1.Stop()
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc1.Start();
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
6. <span data-ttu-id="3a0fa-262">Merhaba SQL Server hizmet hesabını ContosoSQL2 tooCORP\SQLSvc2 değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-262">Change hello SQL Server service account for ContosoSQL2 tooCORP\SQLSvc2.</span></span>

        $wmi2 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server2
        $wmi2.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct2,$password)}
        $svc2 = Get-Service -ComputerName $server2 -Name 'MSSQLSERVER'
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
7. <span data-ttu-id="3a0fa-263">Karşıdan **CreateAzureFailoverCluster.ps1** gelen [Always On kullanılabilirlik grupları Azure VM'de yük devretme kümesi oluşturma](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello yerel çalışma dizini.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-263">Download **CreateAzureFailoverCluster.ps1** from [Create Failover Cluster for Always On Availability Groups in Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello local working directory.</span></span> <span data-ttu-id="3a0fa-264">Bir işlev yük devretme kümesi oluşturma bu komut dosyası toohelp kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-264">You'll use this script toohelp you create a functional failover cluster.</span></span> <span data-ttu-id="3a0fa-265">Windows Yük Devretme Kümelemesi hello Azure ile nasıl etkileşim hakkında önemli bilgiler için ağ için bkz: [Azure Virtual Machines'de SQL Server için yüksek kullanılabilirlik ve olağanüstü durum kurtarma](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3a0fa-265">For important information on how Windows Failover Clustering interacts with hello Azure network, see [High availability and disaster recovery for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>
8. <span data-ttu-id="3a0fa-266">Tooyour çalışma dizini değiştirin ve indirilen hello komut dosyasıyla hello yük devretme kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-266">Change tooyour working directory and create hello failover cluster with hello downloaded script.</span></span>

        Set-ExecutionPolicy Unrestricted -Force
        .\CreateAzureFailoverCluster.ps1 -ClusterName "$clusterName" -ClusterNode "$server1","$server2","$serverQuorum"
9. <span data-ttu-id="3a0fa-267">Always On kullanılabilirlik grupları'hello varsayılan SQL Server örnekleri için etkinleştirmek **ContosoSQL1** ve **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-267">Enable Always On availability groups for hello default SQL Server instances on **ContosoSQL1** and **ContosoSQL2**.</span></span>

        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server1\Default `
            -Force
        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server2\Default `
            -NoServiceRestart
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
10. <span data-ttu-id="3a0fa-268">Bir yedekleme dizini oluşturmak ve hello SQL Server hizmeti hesapları için izinler verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-268">Create a backup directory and grant permissions for hello SQL Server service accounts.</span></span> <span data-ttu-id="3a0fa-269">Bu dizin tooprepare hello kullanılabilirlik veritabanı hello ikincil kopyada kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-269">You'll use this directory tooprepare hello availability database on hello secondary replica.</span></span>

         $backup = "C:\backup"
         New-Item $backup -ItemType directory
         net share backup=$backup "/grant:$acct1,FULL" "/grant:$acct2,FULL"
         icacls.exe "$backup" /grant:r ("$acct1" + ":(OI)(CI)F") ("$acct2" + ":(OI)(CI)F")
11. <span data-ttu-id="3a0fa-270">Bir veritabanı oluşturma **ContosoSQL1** adlı **MyDB1**, hem tam yedekleme hem de bir günlük yedeklemesi alın ve bunları geri **ContosoSQL2** hello ile **ile NORECOVERY** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-270">Create a database on **ContosoSQL1** called **MyDB1**, take both a full backup and a log backup, and restore them on **ContosoSQL2** with hello **WITH NORECOVERY** option.</span></span>

         Invoke-SqlCmd -Query "CREATE database $db"
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server1
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server1 -BackupAction Log
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server2 -NoRecovery
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server2 -RestoreAction Log -NoRecovery
12. <span data-ttu-id="3a0fa-271">SQL Server Vm'lerinin hello üzerinde Hello kullanılabilirlik grubunun uç noktaları oluşturun ve hello uygun izinlere hello uç noktalarda ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-271">Create hello availability group endpoints on hello SQL Server VMs and set hello proper permissions on hello endpoints.</span></span>

         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server1\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"
         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server2\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"

         Invoke-SqlCmd -Query "CREATE LOGIN [$acct2] FROM WINDOWS" -ServerInstance $server1
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct2]" -ServerInstance $server1
         Invoke-SqlCmd -Query "CREATE LOGIN [$acct1] FROM WINDOWS" -ServerInstance $server2
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct1]" -ServerInstance $server2
13. <span data-ttu-id="3a0fa-272">Merhaba kullanılabilirlik çoğaltmalarının oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-272">Create hello availability replicas.</span></span>

         $primaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server1 `
             -EndpointURL "TCP://$server1.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
         $secondaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server2 `
             -EndpointURL "TCP://$server2.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
14. <span data-ttu-id="3a0fa-273">Son olarak, hello kullanılabilirlik grubu ve birleştirme hello ikincil çoğaltma toohello kullanılabilirlik grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-273">Finally, create hello availability group and join hello secondary replica toohello availability group.</span></span>

         New-SqlAvailabilityGroup `
             -Name $ag `
             -Path "SQLSERVER:\SQL\$server1\Default" `
             -AvailabilityReplica @($primaryReplica,$secondaryReplica) `
             -Database $db
         Join-SqlAvailabilityGroup `
             -Path "SQLSERVER:\SQL\$server2\Default" `
             -Name $ag
         Add-SqlAvailabilityDatabase `
             -Path "SQLSERVER:\SQL\$server2\Default\AvailabilityGroups\$ag" `
             -Database $db

## <a name="next-steps"></a><span data-ttu-id="3a0fa-274">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3a0fa-274">Next steps</span></span>
<span data-ttu-id="3a0fa-275">Artık başarıyla SQL Server Always On Azure'da bir kullanılabilirlik grubu oluşturarak uyguladık.</span><span class="sxs-lookup"><span data-stu-id="3a0fa-275">You've now successfully implemented SQL Server Always On by creating an availability group in Azure.</span></span> <span data-ttu-id="3a0fa-276">Bu kullanılabilirlik grubu için bir dinleyici tooconfigure bkz [Azure'da Always On kullanılabilirlik grupları için bir ILB dinleyicisi yapılandırın](../classic/ps-sql-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="3a0fa-276">tooconfigure a listener for this availability group, see [Configure an ILB listener for Always On availability groups in Azure](../classic/ps-sql-int-listener.md).</span></span>

<span data-ttu-id="3a0fa-277">Azure'da SQL Server kullanma hakkında diğer bilgi için bkz: [Azure virtual machines'de SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3a0fa-277">For other information about using SQL Server in Azure, see [SQL Server on Azure virtual machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
