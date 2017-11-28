---
title: Otomatik yedekleme SQL Server sanal makineleri (Klasik) | Microsoft Docs
description: "Resource Manager kullanarak Azure sanal makineleri olarak çalışan SQL Server için otomatik yedekleme özelliğini açıklar. "
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 3333e830-8a60-42f5-9f44-8e02e9868d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: f7664291c2f45c422d52f682d08dbb67ab32b099
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="automated-backup-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="fac4a-103">Azure sanal makinelerde (Klasik) SQL Server için otomatik yedekleme</span><span class="sxs-lookup"><span data-stu-id="fac4a-103">Automated Backup for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fac4a-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fac4a-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="fac4a-105">Klasik</span><span class="sxs-lookup"><span data-stu-id="fac4a-105">Classic</span></span>](../classic/sql-automated-backup.md)
> 
> 

<span data-ttu-id="fac4a-106">Otomatik yedekleme otomatik olarak yapılandırır [yönetilen Microsoft Azure yedekleme](https://msdn.microsoft.com/library/dn449496.aspx) SQL Server 2014 Standard veya Enterprise çalıştıran bir Azure VM üzerindeki tüm mevcut ve yeni veritabanları için.</span><span class="sxs-lookup"><span data-stu-id="fac4a-106">Automated Backup automatically configures [Managed Backup to Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="fac4a-107">Bu, dayanıklı Azure blob depolama alanını normal veritabanı yedeklemeleri yapılandırmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="fac4a-107">This enables you to configure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="fac4a-108">Otomatik yedekleme bağımlı [SQL Server Iaas Aracısı uzantısı](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fac4a-108">Automated Backup depends on the [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="fac4a-109">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fac4a-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fac4a-110">Bu makalede, Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="fac4a-110">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="fac4a-111">Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="fac4a-111">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="fac4a-112">Bu makalede Resource Manager sürümünü görüntülemek için bkz: [otomatik yedekleme SQL Server Azure sanal makineleri Kaynak Yöneticisi'nde](../sql/virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="fac4a-112">To view the Resource Manager version of this article, see [Automated Backup for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fac4a-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fac4a-113">Prerequisites</span></span>
<span data-ttu-id="fac4a-114">Otomatik yedekleme kullanmak için aşağıdaki önkoşulları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="fac4a-114">To use Automated Backup, consider the following prerequisites:</span></span>

<span data-ttu-id="fac4a-115">**İşletim sistemi**:</span><span class="sxs-lookup"><span data-stu-id="fac4a-115">**Operating System**:</span></span>

* <span data-ttu-id="fac4a-116">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="fac4a-116">Windows Server 2012</span></span>
* <span data-ttu-id="fac4a-117">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="fac4a-117">Windows Server 2012 R2</span></span>
* <span data-ttu-id="fac4a-118">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="fac4a-118">Windows Server 2016</span></span>

<span data-ttu-id="fac4a-119">**SQL Server sürümü/yayını**:</span><span class="sxs-lookup"><span data-stu-id="fac4a-119">**SQL Server version/edition**:</span></span>

* <span data-ttu-id="fac4a-120">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="fac4a-120">SQL Server 2014 Standard</span></span>
* <span data-ttu-id="fac4a-121">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="fac4a-121">SQL Server 2014 Enterprise</span></span>

> [!NOTE]
> <span data-ttu-id="fac4a-122">SQL Server 2016 için otomatik yedekleme henüz desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="fac4a-122">SQL Server 2016 is not yet supported for Automated Backup.</span></span>
> 
> 

<span data-ttu-id="fac4a-123">**Veritabanı yapılandırması**:</span><span class="sxs-lookup"><span data-stu-id="fac4a-123">**Database configuration**:</span></span>

* <span data-ttu-id="fac4a-124">Hedef veritabanlarına tam kurtarma modeli kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fac4a-124">Target databases must use the full recovery model.</span></span>

<span data-ttu-id="fac4a-125">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="fac4a-125">**Azure PowerShell**:</span></span>

* <span data-ttu-id="fac4a-126">[En son Azure PowerShell komutlarını yüklemek](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fac4a-126">[Install the latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="fac4a-127">**SQL Server Iaas uzantısı**:</span><span class="sxs-lookup"><span data-stu-id="fac4a-127">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="fac4a-128">[SQL Server Iaas uzantısını yükleyin](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="fac4a-128">[Install the SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="fac4a-129">Ayarlar</span><span class="sxs-lookup"><span data-stu-id="fac4a-129">Settings</span></span>
<span data-ttu-id="fac4a-130">Aşağıdaki tabloda otomatik yedekleme için yapılandırılmış seçenekler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="fac4a-130">The following table describes the options that can be configured for Automated Backup.</span></span> <span data-ttu-id="fac4a-131">Klasik VM'ler için bu ayarları yapılandırmak için PowerShell kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fac4a-131">For classic VMs, you must use PowerShell to configure these settings.</span></span>

| <span data-ttu-id="fac4a-132">Ayar</span><span class="sxs-lookup"><span data-stu-id="fac4a-132">Setting</span></span> | <span data-ttu-id="fac4a-133">Aralık (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="fac4a-133">Range (Default)</span></span> | <span data-ttu-id="fac4a-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fac4a-134">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fac4a-135">**Otomatik Yedekleme**</span><span class="sxs-lookup"><span data-stu-id="fac4a-135">**Automated Backup**</span></span> |<span data-ttu-id="fac4a-136">Etkinleştir/devre dışı bırak (devre dışı)</span><span class="sxs-lookup"><span data-stu-id="fac4a-136">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="fac4a-137">Etkinleştirir veya SQL Server 2014 Standard veya Enterprise çalıştıran bir Azure VM için otomatik yedekleme devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="fac4a-137">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="fac4a-138">**Saklama süresi**</span><span class="sxs-lookup"><span data-stu-id="fac4a-138">**Retention Period**</span></span> |<span data-ttu-id="fac4a-139">1-30 gün (30 gün)</span><span class="sxs-lookup"><span data-stu-id="fac4a-139">1-30 days (30 days)</span></span> |<span data-ttu-id="fac4a-140">Bir yedekleme saklanacağı gün sayısı.</span><span class="sxs-lookup"><span data-stu-id="fac4a-140">The number of days to retain a backup.</span></span> |
| <span data-ttu-id="fac4a-141">**Depolama hesabı**</span><span class="sxs-lookup"><span data-stu-id="fac4a-141">**Storage Account**</span></span> |<span data-ttu-id="fac4a-142">Azure depolama hesabı (belirtilen VM için oluşturulan depolama hesabı)</span><span class="sxs-lookup"><span data-stu-id="fac4a-142">Azure storage account (the storage account created for the specified VM)</span></span> |<span data-ttu-id="fac4a-143">Blob depolama alanına otomatik yedekleme dosyalarını depolamak için kullanılacak bir Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="fac4a-143">An Azure storage account to use for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="fac4a-144">Bir kapsayıcı tüm yedekleme dosyalarını depolamak için bu konumda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="fac4a-144">A container is created at this location to store all backup files.</span></span> <span data-ttu-id="fac4a-145">Yedekleme dosyası adlandırma kuralı, tarih, saat ve makine adını içerir.</span><span class="sxs-lookup"><span data-stu-id="fac4a-145">The backup file naming convention includes the date, time, and machine name.</span></span> |
| <span data-ttu-id="fac4a-146">**Şifreleme**</span><span class="sxs-lookup"><span data-stu-id="fac4a-146">**Encryption**</span></span> |<span data-ttu-id="fac4a-147">Etkinleştir/devre dışı bırak (devre dışı)</span><span class="sxs-lookup"><span data-stu-id="fac4a-147">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="fac4a-148">Etkinleştirir veya şifreleme devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="fac4a-148">Enables or disables encryption.</span></span> <span data-ttu-id="fac4a-149">Şifreleme etkinleştirildiğinde, yedekleme geri yüklemek için kullanılan sertifikaları belirtilen depolama hesabının aynı adlandırma kuralını kullanarak aynı automaticbackup kapsayıcısında bulunur.</span><span class="sxs-lookup"><span data-stu-id="fac4a-149">When encryption is enabled, the certificates used to restore the backup are located in the specified storage account in the same automaticbackup container using the same naming convention.</span></span> <span data-ttu-id="fac4a-150">Parola değişirse, bu parola ile yeni bir sertifika oluşturulur, ancak önceki yedekleri geri yüklemek için eski sertifika kalır.</span><span class="sxs-lookup"><span data-stu-id="fac4a-150">If the password changes, a new certificate is generated with that password, but the old certificate remains to restore prior backups.</span></span> |
| <span data-ttu-id="fac4a-151">**Parola**</span><span class="sxs-lookup"><span data-stu-id="fac4a-151">**Password**</span></span> |<span data-ttu-id="fac4a-152">Parola metin (yok)</span><span class="sxs-lookup"><span data-stu-id="fac4a-152">Password text (None)</span></span> |<span data-ttu-id="fac4a-153">Şifreleme anahtarları için bir parola.</span><span class="sxs-lookup"><span data-stu-id="fac4a-153">A password for encryption keys.</span></span> <span data-ttu-id="fac4a-154">Yalnızca budur şifreleme etkin olup olmadığını gerekli.</span><span class="sxs-lookup"><span data-stu-id="fac4a-154">This is only required if encryption is enabled.</span></span> <span data-ttu-id="fac4a-155">Şifrelenmiş bir yedeklemeyi geri yüklemek için doğru parolayı ve yedeğin alındığı anda kullanılan ilgili sertifika olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fac4a-155">In order to restore an encrypted backup, you must have the correct password and related certificate that was used at the time the backup was taken.</span></span> | <span data-ttu-id="fac4a-156">**Yedekleme sistem veritabanları**</span><span class="sxs-lookup"><span data-stu-id="fac4a-156">**Backup system databases**</span></span> | <span data-ttu-id="fac4a-157">Etkinleştir/devre dışı bırak (devre dışı)</span><span class="sxs-lookup"><span data-stu-id="fac4a-157">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="fac4a-158">Master, Model ve MSDB tam yedekleme gerçekleştirin</span><span class="sxs-lookup"><span data-stu-id="fac4a-158">Take full backups of Master, Model, and MSDB</span></span> |
| <span data-ttu-id="fac4a-159">**Yedekleme zamanlaması yapılandırma**</span><span class="sxs-lookup"><span data-stu-id="fac4a-159">**Configure backup schedule**</span></span> | <span data-ttu-id="fac4a-160">El ile otomatik / (otomatik)</span><span class="sxs-lookup"><span data-stu-id="fac4a-160">Manual/Automated (Automated)</span></span> | <span data-ttu-id="fac4a-161">Seçin **otomatik** otomatik olarak tam alıp Günlük büyüme üzerinde bağlı olarak yedeklemeler oturum.</span><span class="sxs-lookup"><span data-stu-id="fac4a-161">Select **Automated** to automatically take full and log backups based on log growth.</span></span> <span data-ttu-id="fac4a-162">Seçin **el ile** tam zamanlama belirtmek için ve günlük yedekleri.</span><span class="sxs-lookup"><span data-stu-id="fac4a-162">Select **Manual** to specify the schedule for full and log backups.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="fac4a-163">PowerShell ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fac4a-163">Configuration with PowerShell</span></span>
<span data-ttu-id="fac4a-164">Aşağıdaki PowerShell örnekte otomatik yedekleme için mevcut bir SQL Server 2014 VM'yi yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="fac4a-164">In the following PowerShell example, Automated Backup is configured for an existing SQL Server 2014 VM.</span></span> <span data-ttu-id="fac4a-165">**Yeni AzureVMSqlServerAutoBackupConfig** komut $storageaccount değişkeni tarafından belirtilen Azure depolama hesabındaki yedeklemelerini depolamak için otomatik yedekleme ayarlarını yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="fac4a-165">The **New-AzureVMSqlServerAutoBackupConfig** command configures the Automated Backup settings to store backups in the Azure storage account specified by the $storageaccount variable.</span></span> <span data-ttu-id="fac4a-166">Bu yedeklemeler 10 gün boyunca saklanır.</span><span class="sxs-lookup"><span data-stu-id="fac4a-166">These backups will be retained for 10 days.</span></span> <span data-ttu-id="fac4a-167">**Kümesi AzureVMSqlServerExtension** komutu bu ayarlarla belirtilen Azure VM güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="fac4a-167">The **Set-AzureVMSqlServerExtension** command updates the specified Azure VM with these settings.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="fac4a-168">Yüklemek ve SQL Server Iaas aracısı yapılandırmak için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="fac4a-168">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

<span data-ttu-id="fac4a-169">Şifrelemeyi etkinleştirmek için EnableEncryption parametresi CertificatePassword parametresi için bir parola (güvenli dize) ile birlikte geçirmek için önceki komut dosyasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="fac4a-169">To enable encryption, modify the previous script to pass the EnableEncryption parameter along with a password (secure string) for the CertificatePassword parameter.</span></span> <span data-ttu-id="fac4a-170">Aşağıdaki komut dosyası, önceki örnekte otomatik yedekleme ayarlarını etkinleştirir ve şifreleme ekler.</span><span class="sxs-lookup"><span data-stu-id="fac4a-170">The following script enables the Automated Backup settings in the previous example and adds encryption.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="fac4a-171">Otomatik yedekleme devre dışı bırakmak için olmadan aynı komut dosyasını Çalıştır **-etkinleştirmek** parametresi **yeni AzureVMSqlServerAutoBackupConfig**.</span><span class="sxs-lookup"><span data-stu-id="fac4a-171">To disable automatic backup, run the same script without the **-Enable** parameter to the **New-AzureVMSqlServerAutoBackupConfig**.</span></span> <span data-ttu-id="fac4a-172">Yüklemesine gibi otomatik yedekleme devre dışı bırakmak için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="fac4a-172">As with installation, it can take several minutes to disable Automated Backup.</span></span>

> [!NOTE]
> <span data-ttu-id="fac4a-173">Önceden yapılandırılmış yönetilen Yedekleme ayarlarını devre dışı bırakma ve SQL Server Iaas aracısı kaldırma kaldırmaz.</span><span class="sxs-lookup"><span data-stu-id="fac4a-173">Disabling and uninstalling the SQL Server IaaS Agent does not remove the previously configured Managed Backup settings.</span></span> <span data-ttu-id="fac4a-174">Devre dışı bırakma veya SQL Server Iaas Aracısı kaldırmadan önce otomatik yedekleme devre dışı bırakmalısınız.</span><span class="sxs-lookup"><span data-stu-id="fac4a-174">You should disable Automated Backup before disabling or uninstalling the SQL Server IaaS Agent.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="fac4a-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fac4a-175">Next steps</span></span>
<span data-ttu-id="fac4a-176">Otomatik yedekleme yönetilen yedekleme Azure Vm'lerinde yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="fac4a-176">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="fac4a-177">İçin önemlidir [yönetilen yedekleme belgelerini gözden](https://msdn.microsoft.com/library/dn449496.aspx) davranışı ve etkilerini anlamak için.</span><span class="sxs-lookup"><span data-stu-id="fac4a-177">So it is important to [review the documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) to understand the behavior and implications.</span></span>

<span data-ttu-id="fac4a-178">Ek yedekleme bulmak ve Azure vm'lerinde SQL Server Kılavuzu şu konuda geri yükleyebilirsiniz: [yedekleme ve geri yükleme Azure Virtual Machines'de SQL Server için](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fac4a-178">You can find additional backup and restore guidance for SQL Server on Azure VMs in the following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="fac4a-179">Diğer kullanılabilir Otomasyon görevler hakkında daha fazla bilgi için bkz: [SQL Server Iaas Aracısı uzantısı](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="fac4a-179">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="fac4a-180">Azure Vm'lerinde SQL Server çalıştırma hakkında daha fazla bilgi için bkz: [Azure sanal makinelere genel bakış SQL Server'da](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fac4a-180">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

