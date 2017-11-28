---
title: "SQL Server 2016 Azure sanal makineler için yedekleme v2 otomatik | Microsoft Docs"
description: "SQL Server 2016 Azure'da çalışan sanal makineler için otomatik yedekleme özelliğini açıklar. Bu makalede, Resource Manager kullanarak VM'ler için özeldir."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: ebd23868-821c-475b-b867-06d4a2e310c7
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/05/2017
ms.author: jroth
ms.openlocfilehash: e7e14b0243f82c672392d5ab4bb6aca01156465b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="automated-backup-v2-for-sql-server-2016-azure-virtual-machines-resource-manager"></a><span data-ttu-id="364f0-104">SQL Server 2016 Azure sanal makineleri için (Resource Manager) yedekleme v2 otomatik</span><span class="sxs-lookup"><span data-stu-id="364f0-104">Automated Backup v2 for SQL Server 2016 Azure Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="364f0-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="364f0-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="364f0-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="364f0-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="364f0-107">Otomatik yedekleme v2 otomatik olarak yapılandırır [yönetilen Microsoft Azure yedekleme](https://msdn.microsoft.com/library/dn449496.aspx) Azure VM'de SQL Server 2016 Standard, Enterprise veya Geliştirici sürümlerini çalıştıran tüm mevcut ve yeni veritabanları için.</span><span class="sxs-lookup"><span data-stu-id="364f0-107">Automated Backup v2 automatically configures [Managed Backup to Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2016 Standard, Enterprise, or Developer editions.</span></span> <span data-ttu-id="364f0-108">Bu, dayanıklı Azure blob depolama alanını normal veritabanı yedeklemeleri yapılandırmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="364f0-108">This enables you to configure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="364f0-109">Otomatik yedekleme v2 bağımlı [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="364f0-109">Automated Backup v2 depends on the [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="364f0-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="364f0-110">Prerequisites</span></span>
<span data-ttu-id="364f0-111">Otomatik yedekleme v2 kullanmak için aşağıdaki önkoşulları gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="364f0-111">To use Automated Backup v2, review the following prerequisites:</span></span>

<span data-ttu-id="364f0-112">**İşletim sistemi**:</span><span class="sxs-lookup"><span data-stu-id="364f0-112">**Operating System**:</span></span>

- <span data-ttu-id="364f0-113">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="364f0-113">Windows Server 2012 R2</span></span>
- <span data-ttu-id="364f0-114">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="364f0-114">Windows Server 2016</span></span>

<span data-ttu-id="364f0-115">**SQL Server sürümü/yayını**:</span><span class="sxs-lookup"><span data-stu-id="364f0-115">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="364f0-116">SQL Server 2016 Standard</span><span class="sxs-lookup"><span data-stu-id="364f0-116">SQL Server 2016 Standard</span></span>
- <span data-ttu-id="364f0-117">SQL Server 2016 Enterprise</span><span class="sxs-lookup"><span data-stu-id="364f0-117">SQL Server 2016 Enterprise</span></span>
- <span data-ttu-id="364f0-118">SQL Server 2016 Developer</span><span class="sxs-lookup"><span data-stu-id="364f0-118">SQL Server 2016 Developer</span></span>

> [!IMPORTANT]
> <span data-ttu-id="364f0-119">Otomatik yedekleme v2 SQL Server 2016 ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="364f0-119">Automated Backup v2 works with SQL Server 2016.</span></span> <span data-ttu-id="364f0-120">SQL Server 2014 kullanıyorsanız, veritabanlarını yedeklemek için otomatik yedekleme v1 kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="364f0-120">If you are using SQL Server 2014, you can use Automated Backup v1 to back up your databases.</span></span> <span data-ttu-id="364f0-121">Daha fazla bilgi için bkz: [otomatik yedekleme SQL Server 2014 Azure Virtual Machines için](virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="364f0-121">For more information, see [Automated Backup for SQL Server 2014 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span></span>

<span data-ttu-id="364f0-122">**Veritabanı yapılandırması**:</span><span class="sxs-lookup"><span data-stu-id="364f0-122">**Database configuration**:</span></span>

- <span data-ttu-id="364f0-123">Hedef veritabanlarına tam kurtarma modeli kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="364f0-123">Target databases must use the full recovery model.</span></span> <span data-ttu-id="364f0-124">Daha fazla tam kurtarma modeli etkisi hakkında yedekleme hakkında bilgi için [yedekleme altında tam kurtarma modeli](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="364f0-124">For more information about the impact of the full recovery model on backups, see [Backup Under the Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="364f0-125">Sistem veritabanlarının tam kurtarma modelini kullanmak zorunda değil.</span><span class="sxs-lookup"><span data-stu-id="364f0-125">System databases do not have to use full recovery model.</span></span> <span data-ttu-id="364f0-126">Ancak, Model veya MSDB için alınacak günlük yedekleri gerektiriyorsa, tam kurtarma modeli kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="364f0-126">However, if you require log backups to be taken for Model or MSDB, you must use full recovery model.</span></span>
- <span data-ttu-id="364f0-127">Hedef veritabanlarına varsayılan SQL Server örneğinde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="364f0-127">Target databases must be on the default SQL Server instance.</span></span> <span data-ttu-id="364f0-128">SQL Server Iaas uzantısı adlandırılmış örnekleri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="364f0-128">The SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="364f0-129">**Azure dağıtım modeli**:</span><span class="sxs-lookup"><span data-stu-id="364f0-129">**Azure deployment model**:</span></span>

- <span data-ttu-id="364f0-130">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="364f0-130">Resource Manager</span></span>

> [!NOTE]
> <span data-ttu-id="364f0-131">Otomatik yedekleme kullanır **SQL Server Iaas Aracısı uzantısı**.</span><span class="sxs-lookup"><span data-stu-id="364f0-131">Automated Backup relies on the **SQL Server IaaS Agent Extension**.</span></span> <span data-ttu-id="364f0-132">Geçerli SQL sanal makineye Galerisi görüntülerini varsayılan olarak bu uzantı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="364f0-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="364f0-133">Daha fazla bilgi için bkz: [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="364f0-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="364f0-134">Ayarlar</span><span class="sxs-lookup"><span data-stu-id="364f0-134">Settings</span></span>
<span data-ttu-id="364f0-135">Aşağıdaki tabloda otomatik yedekleme v2 için yapılandırılabilir seçenekler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="364f0-135">The following table describes the options that can be configured for Automated Backup v2.</span></span> <span data-ttu-id="364f0-136">Gerçek yapılandırma adımları Azure portalında veya Azure Windows PowerShell komutlarını kullanmadığınıza bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="364f0-136">The actual configuration steps vary depending on whether you use the Azure portal or Azure Windows PowerShell commands.</span></span>

### <a name="basic-settings"></a><span data-ttu-id="364f0-137">Temel ayarlar</span><span class="sxs-lookup"><span data-stu-id="364f0-137">Basic Settings</span></span>

| <span data-ttu-id="364f0-138">Ayar</span><span class="sxs-lookup"><span data-stu-id="364f0-138">Setting</span></span> | <span data-ttu-id="364f0-139">Aralık (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="364f0-139">Range (Default)</span></span> | <span data-ttu-id="364f0-140">Açıklama</span><span class="sxs-lookup"><span data-stu-id="364f0-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364f0-141">**Otomatik Yedekleme**</span><span class="sxs-lookup"><span data-stu-id="364f0-141">**Automated Backup**</span></span> | <span data-ttu-id="364f0-142">Etkinleştir/devre dışı bırak (devre dışı)</span><span class="sxs-lookup"><span data-stu-id="364f0-142">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="364f0-143">Etkinleştirir veya SQL Server 2016 Standard veya Enterprise çalıştıran bir Azure VM için otomatik yedekleme devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="364f0-143">Enables or disables Automated Backup for an Azure VM running SQL Server 2016 Standard or Enterprise.</span></span> |
| <span data-ttu-id="364f0-144">**Saklama süresi**</span><span class="sxs-lookup"><span data-stu-id="364f0-144">**Retention Period**</span></span> | <span data-ttu-id="364f0-145">1-30 gün (30 gün)</span><span class="sxs-lookup"><span data-stu-id="364f0-145">1-30 days (30 days)</span></span> | <span data-ttu-id="364f0-146">Yedeklemeleri tutulacağı gün sayısı.</span><span class="sxs-lookup"><span data-stu-id="364f0-146">The number of days to retain backups.</span></span> |
| <span data-ttu-id="364f0-147">**Depolama hesabı**</span><span class="sxs-lookup"><span data-stu-id="364f0-147">**Storage Account**</span></span> | <span data-ttu-id="364f0-148">Azure depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="364f0-148">Azure storage account</span></span> | <span data-ttu-id="364f0-149">Blob depolama alanına otomatik yedekleme dosyalarını depolamak için kullanılacak bir Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="364f0-149">An Azure storage account to use for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="364f0-150">Bir kapsayıcı tüm yedekleme dosyalarını depolamak için bu konumda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="364f0-150">A container is created at this location to store all backup files.</span></span> <span data-ttu-id="364f0-151">Yedekleme dosyası adlandırma kuralı, tarih, saat ve veritabanı GUID'si içerir.</span><span class="sxs-lookup"><span data-stu-id="364f0-151">The backup file naming convention includes the date, time, and database GUID.</span></span> |
| <span data-ttu-id="364f0-152">**Şifreleme**</span><span class="sxs-lookup"><span data-stu-id="364f0-152">**Encryption**</span></span> |<span data-ttu-id="364f0-153">Etkinleştir/devre dışı bırak (devre dışı)</span><span class="sxs-lookup"><span data-stu-id="364f0-153">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="364f0-154">Etkinleştirir veya şifreleme devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="364f0-154">Enables or disables encryption.</span></span> <span data-ttu-id="364f0-155">Şifreleme etkinleştirildiğinde, yedeklemeyi geri yüklemek için kullanılan sertifikaları aynı belirtilen depolama hesabında bulunan **automaticbackup** aynı adlandırma kuralını kullanarak kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="364f0-155">When encryption is enabled, the certificates used to restore the backup are located in the specified storage account in the same **automaticbackup** container using the same naming convention.</span></span> <span data-ttu-id="364f0-156">Parola değişirse, bu parola ile yeni bir sertifika oluşturulur, ancak önceki yedekleri geri yüklemek için eski sertifika kalır.</span><span class="sxs-lookup"><span data-stu-id="364f0-156">If the password changes, a new certificate is generated with that password, but the old certificate remains to restore prior backups.</span></span> |
| <span data-ttu-id="364f0-157">**Parola**</span><span class="sxs-lookup"><span data-stu-id="364f0-157">**Password**</span></span> |<span data-ttu-id="364f0-158">Parola metin</span><span class="sxs-lookup"><span data-stu-id="364f0-158">Password text</span></span> | <span data-ttu-id="364f0-159">Şifreleme anahtarları için bir parola.</span><span class="sxs-lookup"><span data-stu-id="364f0-159">A password for encryption keys.</span></span> <span data-ttu-id="364f0-160">Yalnızca budur şifreleme etkin olup olmadığını gerekli.</span><span class="sxs-lookup"><span data-stu-id="364f0-160">This is only required if encryption is enabled.</span></span> <span data-ttu-id="364f0-161">Şifrelenmiş bir yedeklemeyi geri yüklemek için doğru parolayı ve yedeğin alındığı anda kullanılan ilgili sertifika olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="364f0-161">In order to restore an encrypted backup, you must have the correct password and related certificate that was used at the time the backup was taken.</span></span> |

### <a name="advanced-settings"></a><span data-ttu-id="364f0-162">Gelişmiş ayarlar</span><span class="sxs-lookup"><span data-stu-id="364f0-162">Advanced Settings</span></span>

| <span data-ttu-id="364f0-163">Ayar</span><span class="sxs-lookup"><span data-stu-id="364f0-163">Setting</span></span> | <span data-ttu-id="364f0-164">Aralık (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="364f0-164">Range (Default)</span></span> | <span data-ttu-id="364f0-165">Açıklama</span><span class="sxs-lookup"><span data-stu-id="364f0-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364f0-166">**Sistem Veritabanı Yedeklemeleri**</span><span class="sxs-lookup"><span data-stu-id="364f0-166">**System Database Backups**</span></span> | <span data-ttu-id="364f0-167">Etkinleştir/devre dışı bırak (devre dışı)</span><span class="sxs-lookup"><span data-stu-id="364f0-167">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="364f0-168">Etkinleştirildiğinde, bu özellik ayrıca sistem veritabanlarını yedekleyin: Master, MSDB ve Model.</span><span class="sxs-lookup"><span data-stu-id="364f0-168">When enabled, this feature will also back up the system databases: Master, MSDB, and Model.</span></span> <span data-ttu-id="364f0-169">MSDB ve modeli veritabanları için alınacak günlük yedekleri istiyorsanız, bunlar tam kurtarma modunda olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="364f0-169">For the MSDB and Model databases, verify that they are in full recovery mode if you want log backups to be taken.</span></span> <span data-ttu-id="364f0-170">Günlük yedeklemeler için ana hiçbir zaman alınır.</span><span class="sxs-lookup"><span data-stu-id="364f0-170">Log backups are never taken for Master.</span></span> <span data-ttu-id="364f0-171">Ve yedekleme TempDB için alınır.</span><span class="sxs-lookup"><span data-stu-id="364f0-171">And no backups are taken for TempDB.</span></span> |
| <span data-ttu-id="364f0-172">**Yedekleme zamanlaması**</span><span class="sxs-lookup"><span data-stu-id="364f0-172">**Backup Schedule**</span></span> | <span data-ttu-id="364f0-173">El ile otomatik / (otomatik)</span><span class="sxs-lookup"><span data-stu-id="364f0-173">Manual/Automated (Automated)</span></span> | <span data-ttu-id="364f0-174">Varsayılan olarak, günlük büyüme tabanlı Yedekleme zamanlaması otomatik olarak belirlenir.</span><span class="sxs-lookup"><span data-stu-id="364f0-174">By default, the backup schedule will be automatically determined based on the log growth.</span></span> <span data-ttu-id="364f0-175">El ile yedekleme zamanlaması yedeklemeler için zaman penceresini belirtmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="364f0-175">Manual backup schedule allows the user to specify the time window for backups.</span></span> <span data-ttu-id="364f0-176">Bu durumda, yedeklemeler her zaman sadece belirtilen sıklığı ve belirli bir günde, belirtilen zaman penceresi sırasında gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="364f0-176">In this case, backups will only ever take place at the specified frequency and during the specified time window of a given day.</span></span> |
| <span data-ttu-id="364f0-177">**Tam yedekleme sıklığı**</span><span class="sxs-lookup"><span data-stu-id="364f0-177">**Full backup frequency**</span></span> | <span data-ttu-id="364f0-178">Günlük/Haftalık</span><span class="sxs-lookup"><span data-stu-id="364f0-178">Daily/Weekly</span></span> | <span data-ttu-id="364f0-179">Tam yedeklemelerinin sıklığını.</span><span class="sxs-lookup"><span data-stu-id="364f0-179">Frequency of full backups.</span></span> <span data-ttu-id="364f0-180">Her iki durumda da, sonraki zamanlanmış zaman penceresi sırasında tam yedeklemeler başlar.</span><span class="sxs-lookup"><span data-stu-id="364f0-180">In both cases, full backups will begin during the next scheduled time window.</span></span> <span data-ttu-id="364f0-181">Haftalık seçili olduğunda, yedeklemelerin tüm veritabanları başarıyla yedeklediyseniz kadar birden fazla gün kapsayabilir.</span><span class="sxs-lookup"><span data-stu-id="364f0-181">When weekly is selected, backups could span multiple days until all databases have successfully backed up.</span></span> |
| <span data-ttu-id="364f0-182">**Tam yedekleme başlangıç saati**</span><span class="sxs-lookup"><span data-stu-id="364f0-182">**Full backup start time**</span></span> | <span data-ttu-id="364f0-183">00:00 – 23:00 (01:00)</span><span class="sxs-lookup"><span data-stu-id="364f0-183">00:00 – 23:00 (01:00)</span></span> | <span data-ttu-id="364f0-184">Başlangıç sırasında tam yedeklemeler gerçekleştirilebildiği belirli bir gün zamanı.</span><span class="sxs-lookup"><span data-stu-id="364f0-184">Start time of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="364f0-185">**Tam yedekleme zaman penceresi**</span><span class="sxs-lookup"><span data-stu-id="364f0-185">**Full backup time window**</span></span> | <span data-ttu-id="364f0-186">1 – 23 saat (1 saat)</span><span class="sxs-lookup"><span data-stu-id="364f0-186">1 – 23 hours (1 hour)</span></span> | <span data-ttu-id="364f0-187">Belirli bir günde sırasında tam yedeklemeler gerçekleştirilebildiği zaman penceresinin süresi.</span><span class="sxs-lookup"><span data-stu-id="364f0-187">Duration of the time window of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="364f0-188">**Günlük yedekleme sıklığı**</span><span class="sxs-lookup"><span data-stu-id="364f0-188">**Log backup frequency**</span></span> | <span data-ttu-id="364f0-189">5 – 60 dakika (60 dakika)</span><span class="sxs-lookup"><span data-stu-id="364f0-189">5 – 60 minutes (60 minutes)</span></span> | <span data-ttu-id="364f0-190">Günlük yedekleme sıklığı.</span><span class="sxs-lookup"><span data-stu-id="364f0-190">Frequency of log backups.</span></span> |

## <a name="understanding-full-backup-frequency"></a><span data-ttu-id="364f0-191">Tam yedekleme sıklığını anlama</span><span class="sxs-lookup"><span data-stu-id="364f0-191">Understanding full backup frequency</span></span>
<span data-ttu-id="364f0-192">Günlük ve haftalık tam yedeklemeler arasındaki farkı anlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="364f0-192">It is important to understand the difference between daily and weekly full backups.</span></span> <span data-ttu-id="364f0-193">Bu çaba içinde iki örnek senaryolar üzerinden size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="364f0-193">In this effort, we will walk through two example scenarios.</span></span>

### <a name="scenario-1-weekly-backups"></a><span data-ttu-id="364f0-194">Senaryo 1: Haftalık yedekleri</span><span class="sxs-lookup"><span data-stu-id="364f0-194">Scenario 1: Weekly backups</span></span>
<span data-ttu-id="364f0-195">Çok büyük veritabanları sayısını içeren bir SQL Server VM var.</span><span class="sxs-lookup"><span data-stu-id="364f0-195">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="364f0-196">Pazartesi günü, aşağıdaki ayarlarla otomatik yedekleme v2 etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="364f0-196">On Monday, you enable Automated Backup v2 with the following settings:</span></span>

- <span data-ttu-id="364f0-197">Yedekleme zamanlaması: **el ile**</span><span class="sxs-lookup"><span data-stu-id="364f0-197">Backup schedule: **Manual**</span></span>
- <span data-ttu-id="364f0-198">Tam yedekleme sıklığını: **haftalık**</span><span class="sxs-lookup"><span data-stu-id="364f0-198">Full backup frequency: **Weekly**</span></span>
- <span data-ttu-id="364f0-199">Tam yedekleme başlangıç saati: **01:00**</span><span class="sxs-lookup"><span data-stu-id="364f0-199">Full backup start time: **01:00**</span></span>
- <span data-ttu-id="364f0-200">Tam yedekleme zaman penceresi: **1 saat**</span><span class="sxs-lookup"><span data-stu-id="364f0-200">Full backup time window: **1 hour**</span></span>

<span data-ttu-id="364f0-201">Bu, sonraki kullanılabilir Yedekleme penceresi 1 saat 1 sabah Salı olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="364f0-201">This means that the next available backup window is Tuesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="364f0-202">O anda aynı anda veritabanlarınızı bir yedekleme otomatik yedekleme başlar.</span><span class="sxs-lookup"><span data-stu-id="364f0-202">At that time, Automated Backup will begin backing up your databases one at a time.</span></span> <span data-ttu-id="364f0-203">Bu senaryoda, veritabanlarınızı tam yedeklemeler için ilk birkaç veritabanlarını tamamlayacak yeterli büyüklükte.</span><span class="sxs-lookup"><span data-stu-id="364f0-203">In this scenario, your databases are large enough that full backups will complete for the first couple databases.</span></span> <span data-ttu-id="364f0-204">Ancak, bir saat sonra tüm veritabanları yedeklendi.</span><span class="sxs-lookup"><span data-stu-id="364f0-204">However, after one hour not all of the databases have been backed up.</span></span>

<span data-ttu-id="364f0-205">Bu durumda, sonraki gün, 1 saat 1 sabah Çarşamba kalan veritabanlarını yedekleme otomatik yedekleme başlar.</span><span class="sxs-lookup"><span data-stu-id="364f0-205">When this happens, Automated Backup will begin backing up the remaining databases the next day, Wednesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="364f0-206">Bu süre içinde tüm veritabanları yedeklenmiş, sonraki gün aynı zamanda yeniden deneyecek.</span><span class="sxs-lookup"><span data-stu-id="364f0-206">If not all databases have been backed up in that time, it will try again the next day at the same time.</span></span> <span data-ttu-id="364f0-207">Tüm veritabanları başarıyla yedeklendi kadar devam eder.</span><span class="sxs-lookup"><span data-stu-id="364f0-207">This will continue until all databases have been successfully backed up.</span></span>

<span data-ttu-id="364f0-208">Salı yeniden ulaştıktan sonra bir kez daha tüm veritabanlarını yedekleme otomatik yedekleme başlar.</span><span class="sxs-lookup"><span data-stu-id="364f0-208">Once it reaches Tuesday again, Automated Backup will begin backing up all databases once again.</span></span>

<span data-ttu-id="364f0-209">Bu senaryo, otomatik yedekleme yalnızca belirtilen zaman penceresi içinde çalışır ve her veritabanı haftada bir kez yukarı yedeklenen gösterir.</span><span class="sxs-lookup"><span data-stu-id="364f0-209">This scenario shows that Automated Backup will only operate within the specified time window, and each database will be backed up once per week.</span></span> <span data-ttu-id="364f0-210">Bu, aynı zamanda birden fazla gün burada tüm yedeklemeler tek bir gün içinde tamamlanmasını olanaklı değil durumda kapsanacak yedeklemeler için olası olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="364f0-210">This also shows that it is possible for backups to span multiple days in the case where it is not possible to complete all backups in a single day.</span></span>

### <a name="scenario-2-daily-backups"></a><span data-ttu-id="364f0-211">Senaryo 2: Günlük yedeklemeler</span><span class="sxs-lookup"><span data-stu-id="364f0-211">Scenario 2: Daily backups</span></span>
<span data-ttu-id="364f0-212">Çok büyük veritabanları sayısını içeren bir SQL Server VM var.</span><span class="sxs-lookup"><span data-stu-id="364f0-212">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="364f0-213">Pazartesi günü, aşağıdaki ayarlarla otomatik yedekleme v2 etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="364f0-213">On Monday, you enable Automated Backup v2 with the following settings:</span></span>

- <span data-ttu-id="364f0-214">Yedekleme zamanlaması: el ile</span><span class="sxs-lookup"><span data-stu-id="364f0-214">Backup schedule: Manual</span></span>
- <span data-ttu-id="364f0-215">Tam yedekleme sıklığını: günlük</span><span class="sxs-lookup"><span data-stu-id="364f0-215">Full backup frequency: Daily</span></span>
- <span data-ttu-id="364f0-216">Tam yedekleme başlangıç saati: 22:00</span><span class="sxs-lookup"><span data-stu-id="364f0-216">Full backup start time: 22:00</span></span>
- <span data-ttu-id="364f0-217">Tam yedekleme zaman penceresi: 6 saat</span><span class="sxs-lookup"><span data-stu-id="364f0-217">Full backup time window: 6 hours</span></span>

<span data-ttu-id="364f0-218">Başka bir deyişle, sonraki kullanılabilir Yedekleme penceresi 10 PM 6 saat boyunca Pazartesi altındadır.</span><span class="sxs-lookup"><span data-stu-id="364f0-218">This means that the next available backup window is Monday at 10 PM for 6 hours.</span></span> <span data-ttu-id="364f0-219">O anda aynı anda veritabanlarınızı bir yedekleme otomatik yedekleme başlar.</span><span class="sxs-lookup"><span data-stu-id="364f0-219">At that time, Automated Backup will begin backing up your databases one at a time.</span></span>

<span data-ttu-id="364f0-220">Ardından, 6 saat boyunca 10 Salı günü, tüm veritabanlarının tam yedeklemeler yeniden başlatılacak.</span><span class="sxs-lookup"><span data-stu-id="364f0-220">Then, on Tuesday at 10 for 6 hours, full backups of all databases will start again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="364f0-221">Günlük yedeklemeler zamanlarken, bu süre içinde tüm veritabanları yedeklenebilir emin olmak için geniş zaman penceresi zamanlama önerilir.</span><span class="sxs-lookup"><span data-stu-id="364f0-221">When scheduling daily backups, it is recommended that you schedule a wide time window to ensure all databases can be backed up within this time.</span></span> <span data-ttu-id="364f0-222">Büyük miktarda veri yedeklemek için sahip olduğu durumda bu durum özellikle önemlidir.</span><span class="sxs-lookup"><span data-stu-id="364f0-222">This is especially important in the case where you have a large amount of data to back up.</span></span>

## <a name="configuration-in-the-portal"></a><span data-ttu-id="364f0-223">Portal Yapılandırması</span><span class="sxs-lookup"><span data-stu-id="364f0-223">Configuration in the Portal</span></span>

<span data-ttu-id="364f0-224">Otomatik yedekleme v2 sağlama sırasında veya var olan SQL Server 2016 VM'ler için yapılandırmak için Azure portalını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="364f0-224">You can use the Azure portal to configure Automated Backup v2 during provisioning or for existing SQL Server 2016 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="364f0-225">Yeni sanal makineleri</span><span class="sxs-lookup"><span data-stu-id="364f0-225">New VMs</span></span>

<span data-ttu-id="364f0-226">Resource Manager dağıtım modelinde yeni bir SQL Server 2016 sanal makine oluşturduğunuzda, otomatik yedekleme v2 yapılandırmak için Azure Portalı'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="364f0-226">Use the Azure portal to configure Automated Backup v2 when you create a new SQL Server 2016 Virtual Machine in the Resource Manager deployment model.</span></span> 

<span data-ttu-id="364f0-227">İçinde **SQL Server ayarları** dikey penceresinde, select **otomatik yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="364f0-227">In the **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="364f0-228">Aşağıdaki Azure portal ekran görüntüsü gösterildiği **SQL otomatik yedekleme** dikey.</span><span class="sxs-lookup"><span data-stu-id="364f0-228">The following Azure portal screenshot shows the **SQL Automated Backup** blade.</span></span>

![Azure portalında SQL otomatik yedekleme yapılandırması](./media/virtual-machines-windows-sql-automated-backup-v2/automated-backup-blade.png)

> [!NOTE]
> <span data-ttu-id="364f0-230">Otomatik yedekleme v2 varsayılan olarak devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="364f0-230">Automated Backup v2 is disabled by default.</span></span>

<span data-ttu-id="364f0-231">Bağlam için tam üzerinde konusuna [azure'da bir SQL Server sanal makine sağlama](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="364f0-231">For context, see the complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="364f0-232">Var olan sanal makineleri</span><span class="sxs-lookup"><span data-stu-id="364f0-232">Existing VMs</span></span>

<span data-ttu-id="364f0-233">Var olan SQL Server sanal makineler için SQL Server sanal makine seçin.</span><span class="sxs-lookup"><span data-stu-id="364f0-233">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="364f0-234">Ardından **SQL Server yapılandırma** bölümünü **ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="364f0-234">Then select the **SQL Server configuration** section of the **Settings** blade.</span></span>

![Var olan VM'ler için SQL otomatik yedekleme](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration.png)

<span data-ttu-id="364f0-236">İçinde **SQL Server yapılandırma** dikey penceresinde tıklatın **Düzenle** otomatik yedekleme bölümdeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="364f0-236">In the **SQL Server configuration** blade, click the **Edit** button in the Automated backup section.</span></span>

![SQL otomatik yedekleme var olan VM'ler için yapılandırma](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration-edit.png)

<span data-ttu-id="364f0-238">Tamamlandığında, tıklatın **Tamam** alt düğmesinde **SQL Server yapılandırma** yaptığınız değişiklikleri kaydetmek için dikey.</span><span class="sxs-lookup"><span data-stu-id="364f0-238">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span></span>

<span data-ttu-id="364f0-239">Otomatik yedekleme ilk kez etkinleştirirseniz, Azure SQL Server Iaas Aracısı arka planda yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="364f0-239">If you are enabling Automated Backup for the first time, Azure configures the SQL Server IaaS Agent in the background.</span></span> <span data-ttu-id="364f0-240">Bu süre boyunca, Azure portalında otomatik yedekleme yapılandırıldığını gösterilmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="364f0-240">During this time, the Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="364f0-241">Aracının yüklü, yapılandırılmış birkaç dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="364f0-241">Wait several minutes for the agent to be installed, configured.</span></span> <span data-ttu-id="364f0-242">Bundan sonra Azure portal'ı yeni ayarları yansıtır.</span><span class="sxs-lookup"><span data-stu-id="364f0-242">After that the Azure portal will reflect the new settings.</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="364f0-243">PowerShell ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="364f0-243">Configuration with PowerShell</span></span>

<span data-ttu-id="364f0-244">Otomatik yedekleme v2 yapılandırmak için PowerShell kullanın.</span><span class="sxs-lookup"><span data-stu-id="364f0-244">You can use PowerShell to configure Automated Backup v2.</span></span> <span data-ttu-id="364f0-245">Başlamadan önce şunları yapmalısınız:</span><span class="sxs-lookup"><span data-stu-id="364f0-245">Before you begin, you must:</span></span>

- <span data-ttu-id="364f0-246">[En son Azure PowerShell'i yükleyip](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="364f0-246">[Download and install the latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="364f0-247">Windows PowerShell'i açın ve hesabınızla ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="364f0-247">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="364f0-248">Bu adımları izleyerek yapabilirsiniz [aboneliğinizi yapılandırma](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) bölümüne sağlama.</span><span class="sxs-lookup"><span data-stu-id="364f0-248">You can do this by following the steps in the [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of the provisioning topic.</span></span>

### <a name="install-the-sql-iaas-extension"></a><span data-ttu-id="364f0-249">SQL Iaas uzantısını yükleyin</span><span class="sxs-lookup"><span data-stu-id="364f0-249">Install the SQL IaaS Extension</span></span>
<span data-ttu-id="364f0-250">Bir SQL Server sanal makine Azure portalından sağlanan, SQL Server Iaas uzantısı zaten yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="364f0-250">If you provisioned a SQL Server virtual machine from the Azure portal, the SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="364f0-251">Bu VM için çağırarak yüklü olup olmadığını belirlemek **Get-AzureRmVM** komutu ve inceleyerek **uzantıları** özelliği.</span><span class="sxs-lookup"><span data-stu-id="364f0-251">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining the **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions 
```

<span data-ttu-id="364f0-252">SQL Server Iaas Aracısı uzantısı yüklediyseniz, "Sqlıaasagent" veya "SQLIaaSExtension" olarak listelenen görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="364f0-252">If the SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="364f0-253">**ProvisioningState** için uzantı "Başarılı" göstermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="364f0-253">**ProvisioningState** for the extension should also show “Succeeded”.</span></span> 

<span data-ttu-id="364f0-254">Bu yüklü değil veya sağlanacak başarısız olursa, aşağıdaki komutla yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="364f0-254">If it is not installed or failed to be provisioned, you can install it with the following command.</span></span> <span data-ttu-id="364f0-255">VM adı ve kaynak grubuna ek olarak, ayrıca bölgeyi belirtmeniz gerekir (**$region**), VM bulunur.</span><span class="sxs-lookup"><span data-stu-id="364f0-255">In addition to the VM name and resource group, you must also specify the region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region 
```

### <span data-ttu-id="364f0-256"><a id="verifysettings"></a>Geçerli ayarlarını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="364f0-256"><a id="verifysettings"></a> Verify current settings</span></span>
<span data-ttu-id="364f0-257">Sağlama işlemi sırasında otomatik yedekleme etkinleştirilirse, geçerli yapılandırmanızı denetlemek için PowerShell'i kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="364f0-257">If you enabled automated backup during provisioning, you can use PowerShell to check your current configuration.</span></span> <span data-ttu-id="364f0-258">Çalıştırma **Get-AzureRmVMSqlServerExtension** komut ve inceleyin **AutoBackupSettings** özelliği:</span><span class="sxs-lookup"><span data-stu-id="364f0-258">Run the **Get-AzureRmVMSqlServerExtension** command and examine the **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="364f0-259">Çıktı aşağıdakine benzer almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="364f0-259">You should get output similar to the following:</span></span>

```
Enable                      : True
EnableEncryption            : False
RetentionPeriod             : 30
StorageUrl                  : https://test.blob.core.windows.net/
StorageAccessKey            :  
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : Manual
FullBackupFrequency         : WEEKLY
FullBackupStartTime         : 2
FullBackupWindowHours       : 2
LogBackupFrequency          : 60
```

<span data-ttu-id="364f0-260">Çıktı gösteriyorsa **etkinleştirmek** ayarlanır **yanlış**, otomatik yedeklemeyi etkinleştirmek sahip.</span><span class="sxs-lookup"><span data-stu-id="364f0-260">If your output shows that **Enable** is set to **False**, then you have to enable automated backup.</span></span> <span data-ttu-id="364f0-261">İyi haber etkinleştirin ve aynı şekilde otomatik yedeklemeyi yapılandırın ' dir.</span><span class="sxs-lookup"><span data-stu-id="364f0-261">The good news is that you enable and configure Automated Backup in the same way.</span></span> <span data-ttu-id="364f0-262">Bu bilgi için sonraki bölüme bakın.</span><span class="sxs-lookup"><span data-stu-id="364f0-262">See the next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="364f0-263">Hemen bir değişiklik yaptıktan sonra ayarlarını denetleyin, eski yapılandırma değerlerini geri alırsınız mümkündür.</span><span class="sxs-lookup"><span data-stu-id="364f0-263">If you check the settings immediately after making a change, it is possible that you will get back the old configuration values.</span></span> <span data-ttu-id="364f0-264">Birkaç dakika bekleyin ve yeniden değişikliklerinizi uygulandığından emin olmak için ayarları kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="364f0-264">Wait a few minutes and check the settings again to make sure that your changes were applied.</span></span>

### <a name="configure-automated-backup-v2"></a><span data-ttu-id="364f0-265">Otomatik yedekleme v2 yapılandırın</span><span class="sxs-lookup"><span data-stu-id="364f0-265">Configure Automated Backup v2</span></span>
<span data-ttu-id="364f0-266">Otomatik yedekleme de, yapılandırma ve davranış herhangi bir zamanda değiştirmek sağlamak için PowerShell kullanın.</span><span class="sxs-lookup"><span data-stu-id="364f0-266">You can use PowerShell to enable Automated Backup as well as to modify its configuration and behavior at any time.</span></span> 

<span data-ttu-id="364f0-267">İlk olarak, seçin veya yedekleme dosyaları için bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="364f0-267">First, select or create a storage account for the backup files.</span></span> <span data-ttu-id="364f0-268">Aşağıdaki komut dosyasını bir depolama hesabı seçer veya henüz yoksa oluşturur.</span><span class="sxs-lookup"><span data-stu-id="364f0-268">The following script selects a storage account or creates it if it does not exist.</span></span>

```powershell
$storage_accountname = “yourstorageaccount”
$storage_resourcegroupname = $resourcegroupname

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region } 
```

> [!NOTE]
> <span data-ttu-id="364f0-269">Otomatik yedekleme premium depolama alanına depolanmasını yedeklemeleri desteklemez, ancak Premium depolama kullanan VM diskleri yedeklemelerden alabilir.</span><span class="sxs-lookup"><span data-stu-id="364f0-269">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="364f0-270">Ardından **yeni AzureRmVMSqlServerAutoBackupConfig** Azure depolama hesabında yedeklemelerini depolamak için otomatik yedekleme v2 ayarlarını etkinleştirme ve yapılandırma için komutu.</span><span class="sxs-lookup"><span data-stu-id="364f0-270">Then use the **New-AzureRmVMSqlServerAutoBackupConfig** command to enable and configure the Automated Backup v2 settings to store backups in the Azure storage account.</span></span> <span data-ttu-id="364f0-271">Bu örnekte, yedeklemeler için 10 gün tutacak şekilde ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="364f0-271">In this example, the backups are set to be retained for 10 days.</span></span> <span data-ttu-id="364f0-272">Sistem Veritabanı Yedeklemeleri etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="364f0-272">System database backups are enabled.</span></span> <span data-ttu-id="364f0-273">Tam yedeklemeler için haftalık iki saat 20:00 başlayarak bir zaman penceresi ile zamanlanır.</span><span class="sxs-lookup"><span data-stu-id="364f0-273">Full backups are scheduled for weekly with a time window starting at 20:00 for two hours.</span></span> <span data-ttu-id="364f0-274">Günlük yedeklemeler için 30 dakikada zamanlanır.</span><span class="sxs-lookup"><span data-stu-id="364f0-274">Log backups are scheduled for every 30 minutes.</span></span> <span data-ttu-id="364f0-275">İkinci komut **kümesi AzureRmVMSqlServerExtension**, bu ayarlarla belirtilen Azure VM güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="364f0-275">The second command, **Set-AzureRmVMSqlServerExtension**, updates the specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname 
```

<span data-ttu-id="364f0-276">Yüklemek ve SQL Server Iaas aracısı yapılandırmak için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="364f0-276">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span> 

<span data-ttu-id="364f0-277">Şifrelemeyi etkinleştirmek için geçirmek için önceki komut dosyasını değiştirin **EnableEncryption** parametresi için bir parola (güvenli dize) ile birlikte **CertificatePassword** parametresi.</span><span class="sxs-lookup"><span data-stu-id="364f0-277">To enable encryption, modify the previous script to pass the **EnableEncryption** parameter along with a password (secure string) for the **CertificatePassword** parameter.</span></span> <span data-ttu-id="364f0-278">Aşağıdaki komut dosyası, önceki örnekte otomatik yedekleme ayarlarını etkinleştirir ve şifreleme ekler.</span><span class="sxs-lookup"><span data-stu-id="364f0-278">The following script enables the Automated Backup settings in the previous example and adds encryption.</span></span>

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="364f0-279">Ayarlarınızı uygulandığını doğrulamak için [otomatik yedekleme yapılandırması doğrulayın](#verifysettings).</span><span class="sxs-lookup"><span data-stu-id="364f0-279">To confirm your settings are applied, [verify the Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="364f0-280">Otomatik yedekleme devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="364f0-280">Disable Automated Backup</span></span>
<span data-ttu-id="364f0-281">Otomatik yedekleme devre dışı bırakmak için olmadan aynı komut dosyasını Çalıştır **-etkinleştirmek** parametresi **yeni AzureRmVMSqlServerAutoBackupConfig** komutu.</span><span class="sxs-lookup"><span data-stu-id="364f0-281">To disable Automated Backup, run the same script without the **-Enable** parameter to the **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="364f0-282">Yokluğu **-etkinleştirmek** parametresi sinyalleri özelliğini devre dışı bırakmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="364f0-282">The absence of the **-Enable** parameter signals the command to disable the feature.</span></span> <span data-ttu-id="364f0-283">Yüklemesine gibi otomatik yedekleme devre dışı bırakmak için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="364f0-283">As with installation, it can take several minutes to disable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="364f0-284">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="364f0-284">Example script</span></span>
<span data-ttu-id="364f0-285">Aşağıdaki betik etkinleştirmek ve VM için otomatik yedekleme yapılandırmak için özelleştirebileceğiniz değişkenleri kümesinin sağlar.</span><span class="sxs-lookup"><span data-stu-id="364f0-285">The following script provides a set of variables that you can customize to enable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="364f0-286">Sizin durumunuzda, gereksinimlerinize göre betiğini özelleştirme gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="364f0-286">In your case, you might need to customize the script based on your requirements.</span></span> <span data-ttu-id="364f0-287">Örneğin, sistem veritabanlarını yedekleme devre dışı bırakır veya şifrelemeyi etkinleştirmek istiyorsanız değişiklik etmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="364f0-287">For example, you would have to make changes if you wanted to disable the backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10
$backupscheduletype = "Manual"
$fullbackupfrequency = "Weekly"
$fullbackupstarthour = "20"
$fullbackupwindow = "2"
$logbackupfrequency = "30"

# ResourceGroupName is the resource group which is hosting the VM where you are deploying the SQL IaaS Extension 

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account to store the backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType $backupscheduletype -FullBackupFrequency $fullbackupfrequency `
    -FullBackupStartHour $fullbackupstarthour -FullBackupWindowInHours $fullbackupwindow `
    -LogBackupFrequencyInMinutes $logbackupfrequency

# Apply the Automated Backup settings to the VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="364f0-288">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="364f0-288">Next steps</span></span>
<span data-ttu-id="364f0-289">Otomatik yedekleme v2 yönetilen yedekleme Azure Vm'lerinde yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="364f0-289">Automated Backup v2 configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="364f0-290">İçin önemlidir [yönetilen yedekleme belgelerini gözden](https://msdn.microsoft.com/library/dn449496.aspx) davranışı ve etkilerini anlamak için.</span><span class="sxs-lookup"><span data-stu-id="364f0-290">So it is important to [review the documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) to understand the behavior and implications.</span></span>

<span data-ttu-id="364f0-291">Ek yedekleme bulmak ve Azure vm'lerinde SQL Server Kılavuzu şu konuda geri yükleyebilirsiniz: [yedekleme ve geri yükleme Azure Virtual Machines'de SQL Server için](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="364f0-291">You can find additional backup and restore guidance for SQL Server on Azure VMs in the following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="364f0-292">Diğer kullanılabilir Otomasyon görevler hakkında daha fazla bilgi için bkz: [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="364f0-292">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="364f0-293">Azure Vm'lerinde SQL Server çalıştırma hakkında daha fazla bilgi için bkz: [Azure sanal makinelere genel bakış SQL Server'da](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="364f0-293">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

