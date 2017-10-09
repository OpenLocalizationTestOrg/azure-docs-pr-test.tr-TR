---
title: bir SQL Server sanal makinesi (Klasik) Azure PowerShell'de aaaCreate | Microsoft Docs
description: "Bir Azure VM ile SQL Server sanal makineye Galerisi görüntüleri oluşturmak için adımlar ve PowerShell komut dosyaları sağlar. Bu konuda hello Klasik dağıtım modunu kullanır."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: b73be387-9323-4e08-be53-6e5928e3786e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: b14d5d9bc192fa0a21126395ee20ffd06b3bf47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a><span data-ttu-id="131e0-104">Azure PowerShell (Klasik) kullanarak bir SQL Server sanal makine sağlama</span><span class="sxs-lookup"><span data-stu-id="131e0-104">Provision a SQL Server virtual machine using Azure PowerShell (Classic)</span></span>

<span data-ttu-id="131e0-105">Bu makalede, nasıl toocreate kullanarak SQL Server sanal makine azure'da hello için PowerShell cmdlet'leri adımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="131e0-105">This article provides steps for how toocreate a SQL Server virtual machine in Azure by using hello PowerShell cmdlets.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="131e0-106">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="131e0-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="131e0-107">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="131e0-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="131e0-108">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="131e0-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="131e0-109">Merhaba Resource Manager sürümü bu konu için bkz: [Azure PowerShell Kaynak Yöneticisi'ni kullanarak bir SQL Server sanal makine sağlama](../sql/virtual-machines-windows-ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="131e0-109">For hello Resource Manager version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Resource Manager](../sql/virtual-machines-windows-ps-sql-create.md).</span></span>

### <a name="install-and-configure-powershell"></a><span data-ttu-id="131e0-110">PowerShell'i yükleme ve yapılandırma:</span><span class="sxs-lookup"><span data-stu-id="131e0-110">Install and configure PowerShell:</span></span>
1. <span data-ttu-id="131e0-111">Bir Azure hesabınız yoksa, [Azure ücretsiz deneme](https://azure.microsoft.com/pricing/free-trial/)yi ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="131e0-111">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
2. <span data-ttu-id="131e0-112">[Merhaba en son Azure PowerShell komutlarını yükleyip](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="131e0-112">[Download and install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>
3. <span data-ttu-id="131e0-113">Windows PowerShell'i başlatın ve tooyour Azure aboneliği ile Merhaba bağlamak **Add-AzureAccount** komutu.</span><span class="sxs-lookup"><span data-stu-id="131e0-113">Start Windows PowerShell, and connect it tooyour Azure subscription with hello **Add-AzureAccount** command.</span></span>

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a><span data-ttu-id="131e0-114">Azure bölgesi hedef belirleme</span><span class="sxs-lookup"><span data-stu-id="131e0-114">Determine your target Azure region</span></span>

<span data-ttu-id="131e0-115">SQL Server sanal makineniz, belirli bir Azure bölgesinde bulunan bir bulut hizmetinde barındırılan.</span><span class="sxs-lookup"><span data-stu-id="131e0-115">Your SQL Server Virtual Machine will be hosted in a cloud service that resides a specific Azure region.</span></span> <span data-ttu-id="131e0-116">Merhaba aşağıdaki adımlar, toodetermine bölgeye, depolama hesabı ve hello öğretici hello kalanı için kullanılacak bulut hizmeti yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="131e0-116">hello following steps help you toodetermine your region, storage account, and cloud service that will be used for hello rest of hello tutorial.</span></span>

1. <span data-ttu-id="131e0-117">SQL Server VM'nize toouse toohost istediğiniz hello veri merkezini belirler.</span><span class="sxs-lookup"><span data-stu-id="131e0-117">Determine hello data center that you want toouse toohost your SQL Server VM.</span></span> <span data-ttu-id="131e0-118">PowerShell komutunu aşağıdaki hello kullanılabilir bölge adlarının bir listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="131e0-118">hello following PowerShell command displays a list of available region names.</span></span>

   ```powershell
   (Get-AzureLocation).Name
   ```

2. <span data-ttu-id="131e0-119">Tercih edilen konumunuz tanımladıktan sonra adlı bir değişken ayarlamak **$dcLocation** toothat bölge.</span><span class="sxs-lookup"><span data-stu-id="131e0-119">Once you've identified your preferred location, set a variable named **$dcLocation** toothat region.</span></span> <span data-ttu-id="131e0-120">Örneğin, aşağıdaki komut kümelerini hello bölge çok hello "Doğu ABD":</span><span class="sxs-lookup"><span data-stu-id="131e0-120">For example, hello following command sets hello region too"East US":</span></span>

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a><span data-ttu-id="131e0-121">Abonelik ve depolama hesabınızı ayarlama</span><span class="sxs-lookup"><span data-stu-id="131e0-121">Set your subscription and storage account</span></span>

1. <span data-ttu-id="131e0-122">Merhaba hello yeni sanal makine için kullanacağınız Azure aboneliği belirler.</span><span class="sxs-lookup"><span data-stu-id="131e0-122">Determine hello Azure subscription you will use for hello new virtual machine.</span></span>

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. <span data-ttu-id="131e0-123">Hedef Azure aboneliği toohello Ata **$subscr** değişkeni.</span><span class="sxs-lookup"><span data-stu-id="131e0-123">Assign your target Azure subscription toohello **$subscr** variable.</span></span> <span data-ttu-id="131e0-124">Sonra geçerli bir Azure aboneliğinizin ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="131e0-124">Then set this as your current Azure subscription.</span></span>

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. <span data-ttu-id="131e0-125">Var olan depolama hesapları için denetleyin.</span><span class="sxs-lookup"><span data-stu-id="131e0-125">Then check for existing storage accounts.</span></span> <span data-ttu-id="131e0-126">Merhaba aşağıdaki betiği seçilen bölgenizde mevcut tüm depolama hesapları görüntüler:</span><span class="sxs-lookup"><span data-stu-id="131e0-126">hello following script displays all storage accounts that exist in your chosen region:</span></span>

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > <span data-ttu-id="131e0-127">İlk yeni bir depolama hesabı gerekiyorsa, bir küçük tüm depolama hesabı adı aşağıdaki örneğine hello olduğu gibi hello yeni AzureStorageAccount komutuyla oluşturun:`New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span><span class="sxs-lookup"><span data-stu-id="131e0-127">If you require a new storage account, first create an all-lower-case storage account name with hello New-AzureStorageAccount command as in hello following example: `New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span></span>

4. <span data-ttu-id="131e0-128">Merhaba hedef depolama hesabı adı toohello Ata **$staccount**.</span><span class="sxs-lookup"><span data-stu-id="131e0-128">Assign hello target storage account name toohello **$staccount**.</span></span> <span data-ttu-id="131e0-129">Ardından **Set-AzureSubscription** tooset hello aboneliği ve geçerli depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="131e0-129">Then use **Set-AzureSubscription** tooset hello subscription and current storage account.</span></span>

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a><span data-ttu-id="131e0-130">Bir SQL Server sanal makine görüntüsü seçin</span><span class="sxs-lookup"><span data-stu-id="131e0-130">Select a SQL Server virtual machine image</span></span>

1. <span data-ttu-id="131e0-131">Kullanılabilir SQL Server sanal makine görüntüleri hello galerisinden hello listesi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="131e0-131">Find out hello list of available SQL Server virtual machines images from hello gallery.</span></span> <span data-ttu-id="131e0-132">Tüm bu görüntüleri bir **ImageFamily** "SQL" ile başlayan özelliği.</span><span class="sxs-lookup"><span data-stu-id="131e0-132">These images all have an **ImageFamily** property that starts with "SQL".</span></span> <span data-ttu-id="131e0-133">Merhaba aşağıdaki SQL Server'ın önceden yüklü görüntüler hello görüntü ailesi kullanılabilir tooyou sorgu.</span><span class="sxs-lookup"><span data-stu-id="131e0-133">hello following query displays hello image family available tooyou that have SQL Server preinstalled.</span></span>

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. <span data-ttu-id="131e0-134">Merhaba sanal makine görüntüsü ailesi bulduğunuzda, bu ailesinde birden fazla yayımlanan görüntü olabilir.</span><span class="sxs-lookup"><span data-stu-id="131e0-134">When you find hello  virtual machine image family, there could be multiple published images in this family.</span></span> <span data-ttu-id="131e0-135">Kullanım hello aşağıdaki betiği toofind hello son yayımlanan için sanal makine görüntü adı seçilen görüntü ailenize (gibi **Windows Server 2012 R2'de SQL Server 2016 RTM Enterprise**):</span><span class="sxs-lookup"><span data-stu-id="131e0-135">Use hello following script toofind hello latest published virtual machine image name for your selected image family (such as **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2**):</span></span>

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-hello-virtual-machine"></a><span data-ttu-id="131e0-136">Merhaba sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="131e0-136">Create hello virtual machine</span></span>

<span data-ttu-id="131e0-137">Son olarak, PowerShell ile Merhaba sanal makine oluşturun:</span><span class="sxs-lookup"><span data-stu-id="131e0-137">Finally, create hello virtual machine with PowerShell:</span></span>

1. <span data-ttu-id="131e0-138">Bir bulut oluşturmak hizmet toohost hello yeni VM.</span><span class="sxs-lookup"><span data-stu-id="131e0-138">Create a cloud service toohost hello new VM.</span></span> <span data-ttu-id="131e0-139">Bu da olası toouse var olan bir bulut hizmetini yerine olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="131e0-139">Note that it is also possible toouse an existing cloud service instead.</span></span> <span data-ttu-id="131e0-140">Yeni bir değişken oluşturmak **$svcname** hello bulut hizmeti hello kısa adı.</span><span class="sxs-lookup"><span data-stu-id="131e0-140">Create a new variable **$svcname** with hello short name of hello cloud service.</span></span>

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. <span data-ttu-id="131e0-141">Merhaba sanal makine adı ve bir boyut belirtin.</span><span class="sxs-lookup"><span data-stu-id="131e0-141">Specify hello virtual machine name and a size.</span></span> <span data-ttu-id="131e0-142">Sanal makine boyutları hakkında daha fazla bilgi için bkz: [Azure için sanal makine boyutlarını](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="131e0-142">For more information about virtual machine sizes, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see hello link toohello other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. <span data-ttu-id="131e0-143">Merhaba yerel yönetici hesabı ve parolası belirtin.</span><span class="sxs-lookup"><span data-stu-id="131e0-143">Specify hello local administrator account and password.</span></span>

   ```powershell
   $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. <span data-ttu-id="131e0-144">Komut dosyası toocreate hello sanal makine aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="131e0-144">Run hello following script toocreate hello virtual machine.</span></span>

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> <span data-ttu-id="131e0-145">Merhaba ek açıklama ve yapılandırma seçenekleri için bkz **komut kümesini yapı** bölümüne [kullanım Azure PowerShell toocreate ve Windows tabanlı sanal makineleri önceden](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="131e0-145">For additional explanation and configuration options, see hello **Build your command set** section in [Use Azure PowerShell toocreate and preconfigure Windows-based Virtual Machines](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="example-powershell-script"></a><span data-ttu-id="131e0-146">Örnek PowerShell komut dosyası</span><span class="sxs-lookup"><span data-stu-id="131e0-146">Example PowerShell script</span></span>

<span data-ttu-id="131e0-147">Merhaba aşağıdaki komut dosyası sağlar oluşturur tam bir komut dosyası örneği bir **Windows Server 2012 R2'de SQL Server 2016 RTM Enterprise** sanal makine.</span><span class="sxs-lookup"><span data-stu-id="131e0-147">hello following script provides an example of a complete script that creates a **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2** virtual machine.</span></span> <span data-ttu-id="131e0-148">Bu komut dosyası kullanırsanız, bu konunun önceki adımlarda hello göre hello ilk değişkenlerini özelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="131e0-148">If you use this script, you must customize hello initial variables based on hello previous steps in this topic.</span></span>

```powershell
# Customize these variables based on your settings and requirements:
$dcLocation = "East US"
$subscr="mysubscription"
$staccount="mystorageaccount"
$family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
$svcname = "mycloudservice"
$vmname="myvirtualmachine"
$vmsize="A5"

# Set hello current subscription and storage account
# Comment out hello New-AzureStorageAccount line if hello account already exists
Select-AzureSubscription -SubscriptionName $subscr –Current
New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

# Select hello most recent VM image in this image family:
$image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

# Create hello new cloud service; comment out this line if cloud service exists already:
New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

# Create hello VM config:
$vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

# Set administrator credentials:
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

# Create hello SQL Server VM:
New-AzureVM –ServiceName $svcname -VMs $vm1
```

## <a name="connect-with-remote-desktop"></a><span data-ttu-id="131e0-149">İle Uzak Masaüstü Bağlantısı</span><span class="sxs-lookup"><span data-stu-id="131e0-149">Connect with remote desktop</span></span>

1. <span data-ttu-id="131e0-150">Merhaba RDP dosyalarını hello geçerli kullanıcının belgenin klasör toolaunch bu sanal makineleri toocomplete Kurulum oluşturun:</span><span class="sxs-lookup"><span data-stu-id="131e0-150">Create hello RDP files in hello current user's document folder toolaunch these virtual machines toocomplete setup:</span></span>

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. <span data-ttu-id="131e0-151">Merhaba belgeleri dizininde hello RDP dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="131e0-151">In hello documents directory, launch hello RDP file.</span></span> <span data-ttu-id="131e0-152">Merhaba yönetici kullanıcı adı ve parola daha önce sağlanan bağlantı (örneğin, kullanıcı adınızı VMAdmin olduysa, "\VMAdmin" Merhaba kullanıcı belirtin ve hello parola).</span><span class="sxs-lookup"><span data-stu-id="131e0-152">Connect with hello administrator user name and password provided earlier (for example, if your user name was VMAdmin, specify "\VMAdmin" as hello user and provide hello password).</span></span>

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-hello-configuration-of-hello-sql-server-machine-for-remote-access"></a><span data-ttu-id="131e0-153">Uzaktan erişim için SQL Server makinesinde hello tam hello yapılandırması</span><span class="sxs-lookup"><span data-stu-id="131e0-153">Complete hello configuration of hello SQL Server Machine for remote access</span></span>

<span data-ttu-id="131e0-154">Toohello makinede Uzak Masaüstü ile oturum sonra SQL Server'ın hello yönergelere göre yapılandırma [bir Azure VM'de SQL Server bağlantısı yapılandırma adımları](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="131e0-154">After logging on toohello machine with remote desktop, configure SQL Server based on hello instructions in [Steps for configuring SQL Server connectivity in an Azure VM](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

## <a name="next-steps"></a><span data-ttu-id="131e0-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="131e0-155">Next steps</span></span>

<span data-ttu-id="131e0-156">Hello PowerShell ile sanal makinelerin sağlamaya yönelik ek yönergeler bulabilirsiniz [virtual machines belgeleri](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="131e0-156">You can find additional instructions for provisioning virtual machines with PowerShell in hello [virtual machines documentation](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="131e0-157">Çoğu durumda, hello sonraki toomigrate adımdır veritabanları toothis yeni SQL Server VM.</span><span class="sxs-lookup"><span data-stu-id="131e0-157">In many cases, hello next step is toomigrate your databases toothis new SQL Server VM.</span></span> <span data-ttu-id="131e0-158">Veritabanı geçiş yönergeleri için bkz [veritabanı tooSQL bir Azure VM sunucuda geçiş](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="131e0-158">For database migration guidance, see [Migrating a Database tooSQL Server on an Azure VM](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="131e0-159">Ayrıca hello Azure portal toocreate SQL sanal makineleri kullanmak istiyorsanız bkz [Azure üzerinde bir SQL Server sanal makine sağlama](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="131e0-159">If you're also interested in using hello Azure portal toocreate SQL Virtual Machines, see [Provisioning a SQL Server Virtual Machine on Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="131e0-160">Merhaba portal size kullanarak VM'ler oluşturur yetenekte hello Klasik modeli bu PowerShell konuda kullanılan yerine önerilen Resource Manager modeli hello bu hello öğretici unutmayın.</span><span class="sxs-lookup"><span data-stu-id="131e0-160">Note that hello tutorial that walks you through hello portal creates VMs using hello recommended Resource Manager model, rather than hello classic model used in this PowerShell topic.</span></span>

<span data-ttu-id="131e0-161">Ayrıca toothese kaynakları gözden geçirmenizi öneririz [toorunning Azure Virtual Machines'de SQL Server ilgili diğer konular](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="131e0-161">In addition toothese resources, we recommend that you review [other topics related toorunning SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
