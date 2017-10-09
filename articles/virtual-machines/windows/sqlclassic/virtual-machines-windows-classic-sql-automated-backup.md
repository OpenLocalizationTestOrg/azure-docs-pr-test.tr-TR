---
title: "aaaAutomated yedekleme için SQL Server sanal makineler (Klasik) | Microsoft Docs"
description: "SQL Server Kaynak Yöneticisi'ni kullanarak Azure sanal makinelerde çalışan Hello otomatik yedekleme özelliğini açıklar. "
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
ms.openlocfilehash: 5d8f0412578c2d86edc6e54093a5da4891d3847e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="9a55f-103">Azure sanal makinelerde (Klasik) SQL Server için otomatik yedekleme</span><span class="sxs-lookup"><span data-stu-id="9a55f-103">Automated Backup for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9a55f-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9a55f-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="9a55f-105">Klasik</span><span class="sxs-lookup"><span data-stu-id="9a55f-105">Classic</span></span>](../classic/sql-automated-backup.md)
> 
> 

<span data-ttu-id="9a55f-106">Otomatik yedekleme otomatik olarak yapılandırır [yönetilen yedekleme tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) SQL Server 2014 Standard veya Enterprise çalıştıran bir Azure VM üzerindeki tüm mevcut ve yeni veritabanları için.</span><span class="sxs-lookup"><span data-stu-id="9a55f-106">Automated Backup automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="9a55f-107">Bu, dayanıklı Azure blob depolama alanını tooconfigure normal veritabanı yedeklemeleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="9a55f-107">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="9a55f-108">Otomatik yedekleme bağlıdır hello üzerinde [SQL Server Iaas Aracısı uzantısı](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9a55f-108">Automated Backup depends on hello [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="9a55f-109">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9a55f-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9a55f-110">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="9a55f-110">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="9a55f-111">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="9a55f-111">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="9a55f-112">Bu makalenin tooview hello Resource Manager sürümü bkz [otomatik yedekleme SQL Server Azure sanal makineleri Kaynak Yöneticisi'nde](../sql/virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="9a55f-112">tooview hello Resource Manager version of this article, see [Automated Backup for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a55f-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9a55f-113">Prerequisites</span></span>
<span data-ttu-id="9a55f-114">toouse otomatik yedekleme önkoşulları aşağıdaki hello göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="9a55f-114">toouse Automated Backup, consider hello following prerequisites:</span></span>

<span data-ttu-id="9a55f-115">**İşletim sistemi**:</span><span class="sxs-lookup"><span data-stu-id="9a55f-115">**Operating System**:</span></span>

* <span data-ttu-id="9a55f-116">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="9a55f-116">Windows Server 2012</span></span>
* <span data-ttu-id="9a55f-117">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="9a55f-117">Windows Server 2012 R2</span></span>
* <span data-ttu-id="9a55f-118">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="9a55f-118">Windows Server 2016</span></span>

<span data-ttu-id="9a55f-119">**SQL Server sürümü/yayını**:</span><span class="sxs-lookup"><span data-stu-id="9a55f-119">**SQL Server version/edition**:</span></span>

* <span data-ttu-id="9a55f-120">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="9a55f-120">SQL Server 2014 Standard</span></span>
* <span data-ttu-id="9a55f-121">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="9a55f-121">SQL Server 2014 Enterprise</span></span>

> [!NOTE]
> <span data-ttu-id="9a55f-122">SQL Server 2016 için otomatik yedekleme henüz desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="9a55f-122">SQL Server 2016 is not yet supported for Automated Backup.</span></span>
> 
> 

<span data-ttu-id="9a55f-123">**Veritabanı yapılandırması**:</span><span class="sxs-lookup"><span data-stu-id="9a55f-123">**Database configuration**:</span></span>

* <span data-ttu-id="9a55f-124">Hedef veritabanlarına hello tam kurtarma modeli kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a55f-124">Target databases must use hello full recovery model.</span></span>

<span data-ttu-id="9a55f-125">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="9a55f-125">**Azure PowerShell**:</span></span>

* <span data-ttu-id="9a55f-126">[Merhaba en son Azure PowerShell komutlarını yüklemek](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9a55f-126">[Install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="9a55f-127">**SQL Server Iaas uzantısı**:</span><span class="sxs-lookup"><span data-stu-id="9a55f-127">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="9a55f-128">[SQL Server Iaas uzantısı Hello yüklemek](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="9a55f-128">[Install hello SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="9a55f-129">Ayarlar</span><span class="sxs-lookup"><span data-stu-id="9a55f-129">Settings</span></span>
<span data-ttu-id="9a55f-130">Merhaba aşağıdaki tabloda otomatik yedekleme için yapılandırılmış hello seçenekleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9a55f-130">hello following table describes hello options that can be configured for Automated Backup.</span></span> <span data-ttu-id="9a55f-131">Klasik VM'ler için bu ayarları PowerShell tooconfigure kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a55f-131">For classic VMs, you must use PowerShell tooconfigure these settings.</span></span>

| <span data-ttu-id="9a55f-132">Ayar</span><span class="sxs-lookup"><span data-stu-id="9a55f-132">Setting</span></span> | <span data-ttu-id="9a55f-133">Aralık (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="9a55f-133">Range (Default)</span></span> | <span data-ttu-id="9a55f-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9a55f-134">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9a55f-135">**Otomatik Yedekleme**</span><span class="sxs-lookup"><span data-stu-id="9a55f-135">**Automated Backup**</span></span> |<span data-ttu-id="9a55f-136">Etkinleştir/devre dışı bırak (devre dışı)</span><span class="sxs-lookup"><span data-stu-id="9a55f-136">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="9a55f-137">Etkinleştirir veya SQL Server 2014 Standard veya Enterprise çalıştıran bir Azure VM için otomatik yedekleme devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="9a55f-137">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="9a55f-138">**Saklama süresi**</span><span class="sxs-lookup"><span data-stu-id="9a55f-138">**Retention Period**</span></span> |<span data-ttu-id="9a55f-139">1-30 gün (30 gün)</span><span class="sxs-lookup"><span data-stu-id="9a55f-139">1-30 days (30 days)</span></span> |<span data-ttu-id="9a55f-140">gün tooretain bir yedekleme Hello sayısı.</span><span class="sxs-lookup"><span data-stu-id="9a55f-140">hello number of days tooretain a backup.</span></span> |
| <span data-ttu-id="9a55f-141">**Depolama hesabı**</span><span class="sxs-lookup"><span data-stu-id="9a55f-141">**Storage Account**</span></span> |<span data-ttu-id="9a55f-142">Azure depolama hesabı (Merhaba VM belirtilen için oluşturulan hello depolama hesabı)</span><span class="sxs-lookup"><span data-stu-id="9a55f-142">Azure storage account (hello storage account created for hello specified VM)</span></span> |<span data-ttu-id="9a55f-143">Blob depolama alanına otomatik yedekleme dosyalarını depolamak için bir Azure depolama hesabı toouse.</span><span class="sxs-lookup"><span data-stu-id="9a55f-143">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="9a55f-144">Bir kapsayıcı sırasında bu konumu toostore tüm yedekleme dosyaları oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9a55f-144">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="9a55f-145">Merhaba yedekleme dosyası adlandırma hello tarih, saat ve makine adını içerir.</span><span class="sxs-lookup"><span data-stu-id="9a55f-145">hello backup file naming convention includes hello date, time, and machine name.</span></span> |
| <span data-ttu-id="9a55f-146">**Şifreleme**</span><span class="sxs-lookup"><span data-stu-id="9a55f-146">**Encryption**</span></span> |<span data-ttu-id="9a55f-147">Etkinleştir/devre dışı bırak (devre dışı)</span><span class="sxs-lookup"><span data-stu-id="9a55f-147">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="9a55f-148">Etkinleştirir veya şifreleme devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="9a55f-148">Enables or disables encryption.</span></span> <span data-ttu-id="9a55f-149">Şifreleme etkinleştirildiğinde, depolama hesabı kullanılan toorestore hello yedekleme hello bulunan hello sertifikaları belirtilen hello aynı adlandırma kuralı hello kapsayıcı kullanarak automaticbackup aynı.</span><span class="sxs-lookup"><span data-stu-id="9a55f-149">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same automaticbackup container using hello same naming convention.</span></span> <span data-ttu-id="9a55f-150">Merhaba parola değişirse, bu parola ile yeni bir sertifika oluşturulur, ancak toorestore önceki yedeklemeleri hello eski sertifika kalır.</span><span class="sxs-lookup"><span data-stu-id="9a55f-150">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="9a55f-151">**Parola**</span><span class="sxs-lookup"><span data-stu-id="9a55f-151">**Password**</span></span> |<span data-ttu-id="9a55f-152">Parola metin (yok)</span><span class="sxs-lookup"><span data-stu-id="9a55f-152">Password text (None)</span></span> |<span data-ttu-id="9a55f-153">Şifreleme anahtarları için bir parola.</span><span class="sxs-lookup"><span data-stu-id="9a55f-153">A password for encryption keys.</span></span> <span data-ttu-id="9a55f-154">Yalnızca budur şifreleme etkin olup olmadığını gerekli.</span><span class="sxs-lookup"><span data-stu-id="9a55f-154">This is only required if encryption is enabled.</span></span> <span data-ttu-id="9a55f-155">Sipariş toorestore şifreli bir yedekleme hello doğru parolayı ve hello yedeğin alındığı hello zamanında kullanılan ilgili sertifika olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9a55f-155">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> | <span data-ttu-id="9a55f-156">**Yedekleme sistem veritabanları**</span><span class="sxs-lookup"><span data-stu-id="9a55f-156">**Backup system databases**</span></span> | <span data-ttu-id="9a55f-157">Etkinleştir/devre dışı bırak (devre dışı)</span><span class="sxs-lookup"><span data-stu-id="9a55f-157">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="9a55f-158">Master, Model ve MSDB tam yedekleme gerçekleştirin</span><span class="sxs-lookup"><span data-stu-id="9a55f-158">Take full backups of Master, Model, and MSDB</span></span> |
| <span data-ttu-id="9a55f-159">**Yedekleme zamanlaması yapılandırma**</span><span class="sxs-lookup"><span data-stu-id="9a55f-159">**Configure backup schedule**</span></span> | <span data-ttu-id="9a55f-160">El ile otomatik / (otomatik)</span><span class="sxs-lookup"><span data-stu-id="9a55f-160">Manual/Automated (Automated)</span></span> | <span data-ttu-id="9a55f-161">Seçin **otomatik** tooautomatically tam alabilir ve oturum Günlük büyüme üzerinde bağlı olarak yedeklemeler.</span><span class="sxs-lookup"><span data-stu-id="9a55f-161">Select **Automated** tooautomatically take full and log backups based on log growth.</span></span> <span data-ttu-id="9a55f-162">Seçin **el ile** tam toospecify hello zamanlamasını ve günlük yedekleri.</span><span class="sxs-lookup"><span data-stu-id="9a55f-162">Select **Manual** toospecify hello schedule for full and log backups.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="9a55f-163">PowerShell ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9a55f-163">Configuration with PowerShell</span></span>
<span data-ttu-id="9a55f-164">Aşağıdaki PowerShell örneğine hello otomatik yedekleme için mevcut bir SQL Server 2014 VM'yi yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="9a55f-164">In hello following PowerShell example, Automated Backup is configured for an existing SQL Server 2014 VM.</span></span> <span data-ttu-id="9a55f-165">Merhaba **yeni AzureVMSqlServerAutoBackupConfig** komut hello $storageaccount değişkeni tarafından belirtilen hello Azure depolama hesabında hello otomatik yedekleme ayarlarını toostore yedeklemeler yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="9a55f-165">hello **New-AzureVMSqlServerAutoBackupConfig** command configures hello Automated Backup settings toostore backups in hello Azure storage account specified by hello $storageaccount variable.</span></span> <span data-ttu-id="9a55f-166">Bu yedeklemeler 10 gün boyunca saklanır.</span><span class="sxs-lookup"><span data-stu-id="9a55f-166">These backups will be retained for 10 days.</span></span> <span data-ttu-id="9a55f-167">Merhaba **kümesi AzureVMSqlServerExtension** güncelleştirmeleri hello Azure VM bu ayarlarla belirtilen komutu.</span><span class="sxs-lookup"><span data-stu-id="9a55f-167">hello **Set-AzureVMSqlServerExtension** command updates hello specified Azure VM with these settings.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="9a55f-168">Birkaç dakika tooinstall alın ve hello SQL Server Iaas Aracısı Yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="9a55f-168">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="9a55f-169">tooenable şifreleme hello önceki betik toopass hello EnableEncryption parametresi bir parola (güvenli dize) ile birlikte hello CertificatePassword parametresi için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9a55f-169">tooenable encryption, modify hello previous script toopass hello EnableEncryption parameter along with a password (secure string) for hello CertificatePassword parameter.</span></span> <span data-ttu-id="9a55f-170">Merhaba aşağıdaki betiği hello önceki örnekte hello otomatik yedekleme ayarlarını etkinleştirir ve şifreleme ekler.</span><span class="sxs-lookup"><span data-stu-id="9a55f-170">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="9a55f-171">toodisable otomatik yedekleme hello aynı komut dosyası çalıştırma hello **-etkinleştirmek** parametresi toohello **yeni AzureVMSqlServerAutoBackupConfig**.</span><span class="sxs-lookup"><span data-stu-id="9a55f-171">toodisable automatic backup, run hello same script without hello **-Enable** parameter toohello **New-AzureVMSqlServerAutoBackupConfig**.</span></span> <span data-ttu-id="9a55f-172">Yüklemesine gibi birkaç dakika toodisable otomatik yedekleme alabilir.</span><span class="sxs-lookup"><span data-stu-id="9a55f-172">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

> [!NOTE]
> <span data-ttu-id="9a55f-173">Önceden yapılandırılmış hello yönetilen Yedekleme ayarlarını devre dışı bırakma ve hello SQL Server Iaas aracısı kaldırma kaldırmaz.</span><span class="sxs-lookup"><span data-stu-id="9a55f-173">Disabling and uninstalling hello SQL Server IaaS Agent does not remove hello previously configured Managed Backup settings.</span></span> <span data-ttu-id="9a55f-174">Devre dışı bırakma veya SQL Server Iaas Aracısı hello kaldırmadan önce otomatik yedekleme devre dışı bırakmalısınız.</span><span class="sxs-lookup"><span data-stu-id="9a55f-174">You should disable Automated Backup before disabling or uninstalling hello SQL Server IaaS Agent.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="9a55f-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9a55f-175">Next steps</span></span>
<span data-ttu-id="9a55f-176">Otomatik yedekleme yönetilen yedekleme Azure Vm'lerinde yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="9a55f-176">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="9a55f-177">Çok önemlidir[yönetilen yedekleme hello belgelerini gözden geçirin](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello davranışı ve etkileri.</span><span class="sxs-lookup"><span data-stu-id="9a55f-177">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="9a55f-178">Ek yedekleme bulmak ve izleyen konu hello Azure Vm'lerde SQL Server için kılavuzunda geri yükleyebilirsiniz: [yedekleme ve geri yükleme Azure Virtual Machines'de SQL Server için](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9a55f-178">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="9a55f-179">Diğer kullanılabilir Otomasyon görevler hakkında daha fazla bilgi için bkz: [SQL Server Iaas Aracısı uzantısı](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="9a55f-179">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="9a55f-180">Azure Vm'lerinde SQL Server çalıştırma hakkında daha fazla bilgi için bkz: [Azure sanal makinelere genel bakış SQL Server'da](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9a55f-180">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

