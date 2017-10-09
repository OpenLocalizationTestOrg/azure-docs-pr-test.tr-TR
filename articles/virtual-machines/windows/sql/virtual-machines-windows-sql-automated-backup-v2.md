---
title: "aaaAutomated yedekleme v2 için SQL Server 2016 Azure sanal makineleri | Microsoft Docs"
description: "SQL Server 2016 Azure'da çalışan VM'ler için Hello otomatik yedekleme özelliğini açıklar. Bu makalede hello Kaynak Yöneticisi'ni kullanarak belirli tooVMs ' dir."
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
ms.openlocfilehash: a322792fb22c76bfa74fafb711b8b1927a6e2b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-v2-for-sql-server-2016-azure-virtual-machines-resource-manager"></a><span data-ttu-id="745ae-104">SQL Server 2016 Azure sanal makineleri için (Resource Manager) yedekleme v2 otomatik</span><span class="sxs-lookup"><span data-stu-id="745ae-104">Automated Backup v2 for SQL Server 2016 Azure Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="745ae-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="745ae-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="745ae-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="745ae-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="745ae-107">Otomatik yedekleme v2 otomatik olarak yapılandırır [yönetilen yedekleme tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) Azure VM'de SQL Server 2016 Standard, Enterprise veya Geliştirici sürümlerini çalıştıran tüm mevcut ve yeni veritabanları için.</span><span class="sxs-lookup"><span data-stu-id="745ae-107">Automated Backup v2 automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2016 Standard, Enterprise, or Developer editions.</span></span> <span data-ttu-id="745ae-108">Bu, dayanıklı Azure blob depolama alanını tooconfigure normal veritabanı yedeklemeleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="745ae-108">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="745ae-109">Otomatik yedekleme v2 bağlıdır hello üzerinde [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="745ae-109">Automated Backup v2 depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="745ae-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="745ae-110">Prerequisites</span></span>
<span data-ttu-id="745ae-111">toouse otomatik yedekleme v2 hello aşağıdaki önkoşulları gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="745ae-111">toouse Automated Backup v2, review hello following prerequisites:</span></span>

<span data-ttu-id="745ae-112">**İşletim sistemi**:</span><span class="sxs-lookup"><span data-stu-id="745ae-112">**Operating System**:</span></span>

- <span data-ttu-id="745ae-113">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="745ae-113">Windows Server 2012 R2</span></span>
- <span data-ttu-id="745ae-114">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="745ae-114">Windows Server 2016</span></span>

<span data-ttu-id="745ae-115">**SQL Server sürümü/yayını**:</span><span class="sxs-lookup"><span data-stu-id="745ae-115">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="745ae-116">SQL Server 2016 Standard</span><span class="sxs-lookup"><span data-stu-id="745ae-116">SQL Server 2016 Standard</span></span>
- <span data-ttu-id="745ae-117">SQL Server 2016 Enterprise</span><span class="sxs-lookup"><span data-stu-id="745ae-117">SQL Server 2016 Enterprise</span></span>
- <span data-ttu-id="745ae-118">SQL Server 2016 Developer</span><span class="sxs-lookup"><span data-stu-id="745ae-118">SQL Server 2016 Developer</span></span>

> [!IMPORTANT]
> <span data-ttu-id="745ae-119">Otomatik yedekleme v2 SQL Server 2016 ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="745ae-119">Automated Backup v2 works with SQL Server 2016.</span></span> <span data-ttu-id="745ae-120">SQL Server 2014 kullanıyorsanız, veritabanlarınızı otomatik yedekleme v1 tooback kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="745ae-120">If you are using SQL Server 2014, you can use Automated Backup v1 tooback up your databases.</span></span> <span data-ttu-id="745ae-121">Daha fazla bilgi için bkz: [otomatik yedekleme SQL Server 2014 Azure Virtual Machines için](virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="745ae-121">For more information, see [Automated Backup for SQL Server 2014 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span></span>

<span data-ttu-id="745ae-122">**Veritabanı yapılandırması**:</span><span class="sxs-lookup"><span data-stu-id="745ae-122">**Database configuration**:</span></span>

- <span data-ttu-id="745ae-123">Hedef veritabanlarına hello tam kurtarma modeli kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="745ae-123">Target databases must use hello full recovery model.</span></span> <span data-ttu-id="745ae-124">Daha fazla bilgi hello tam kurtarma modeli için hello etkisi hakkında yedeklemeleri üzerinde [yedekleme altında tam kurtarma modeli hello](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="745ae-124">For more information about hello impact of hello full recovery model on backups, see [Backup Under hello Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="745ae-125">Sistem veritabanlarının toouse tam kurtarma modeli yok.</span><span class="sxs-lookup"><span data-stu-id="745ae-125">System databases do not have toouse full recovery model.</span></span> <span data-ttu-id="745ae-126">Ancak, günlük yedekleri toobe Model veya MSDB alınan ihtiyacınız varsa, tam kurtarma modeli kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="745ae-126">However, if you require log backups toobe taken for Model or MSDB, you must use full recovery model.</span></span>
- <span data-ttu-id="745ae-127">Hedef veritabanlarına hello varsayılan SQL Server örneğinde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="745ae-127">Target databases must be on hello default SQL Server instance.</span></span> <span data-ttu-id="745ae-128">SQL Server Iaas uzantısı Hello adlandırılmış örnekleri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="745ae-128">hello SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="745ae-129">**Azure dağıtım modeli**:</span><span class="sxs-lookup"><span data-stu-id="745ae-129">**Azure deployment model**:</span></span>

- <span data-ttu-id="745ae-130">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="745ae-130">Resource Manager</span></span>

> [!NOTE]
> <span data-ttu-id="745ae-131">Otomatik yedekleme dayanır hello üzerinde **SQL Server Iaas Aracısı uzantısı**.</span><span class="sxs-lookup"><span data-stu-id="745ae-131">Automated Backup relies on hello **SQL Server IaaS Agent Extension**.</span></span> <span data-ttu-id="745ae-132">Geçerli SQL sanal makineye Galerisi görüntülerini varsayılan olarak bu uzantı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="745ae-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="745ae-133">Daha fazla bilgi için bkz: [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="745ae-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="745ae-134">Ayarlar</span><span class="sxs-lookup"><span data-stu-id="745ae-134">Settings</span></span>
<span data-ttu-id="745ae-135">Merhaba aşağıdaki tabloda otomatik yedekleme v2 için yapılandırılabilir hello seçenekleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="745ae-135">hello following table describes hello options that can be configured for Automated Backup v2.</span></span> <span data-ttu-id="745ae-136">Merhaba gerçek yapılandırma adımlarını hello Azure portalında veya Azure Windows PowerShell komutlarını kullanmadığınıza bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="745ae-136">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

### <a name="basic-settings"></a><span data-ttu-id="745ae-137">Temel ayarlar</span><span class="sxs-lookup"><span data-stu-id="745ae-137">Basic Settings</span></span>

| <span data-ttu-id="745ae-138">Ayar</span><span class="sxs-lookup"><span data-stu-id="745ae-138">Setting</span></span> | <span data-ttu-id="745ae-139">Aralık (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="745ae-139">Range (Default)</span></span> | <span data-ttu-id="745ae-140">Açıklama</span><span class="sxs-lookup"><span data-stu-id="745ae-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="745ae-141">**Otomatik Yedekleme**</span><span class="sxs-lookup"><span data-stu-id="745ae-141">**Automated Backup**</span></span> | <span data-ttu-id="745ae-142">Etkinleştir/devre dışı bırak (devre dışı)</span><span class="sxs-lookup"><span data-stu-id="745ae-142">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="745ae-143">Etkinleştirir veya SQL Server 2016 Standard veya Enterprise çalıştıran bir Azure VM için otomatik yedekleme devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="745ae-143">Enables or disables Automated Backup for an Azure VM running SQL Server 2016 Standard or Enterprise.</span></span> |
| <span data-ttu-id="745ae-144">**Saklama süresi**</span><span class="sxs-lookup"><span data-stu-id="745ae-144">**Retention Period**</span></span> | <span data-ttu-id="745ae-145">1-30 gün (30 gün)</span><span class="sxs-lookup"><span data-stu-id="745ae-145">1-30 days (30 days)</span></span> | <span data-ttu-id="745ae-146">gün tooretain yedeklemeler Hello sayısı.</span><span class="sxs-lookup"><span data-stu-id="745ae-146">hello number of days tooretain backups.</span></span> |
| <span data-ttu-id="745ae-147">**Depolama hesabı**</span><span class="sxs-lookup"><span data-stu-id="745ae-147">**Storage Account**</span></span> | <span data-ttu-id="745ae-148">Azure depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="745ae-148">Azure storage account</span></span> | <span data-ttu-id="745ae-149">Blob depolama alanına otomatik yedekleme dosyalarını depolamak için bir Azure depolama hesabı toouse.</span><span class="sxs-lookup"><span data-stu-id="745ae-149">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="745ae-150">Bir kapsayıcı sırasında bu konumu toostore tüm yedekleme dosyaları oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="745ae-150">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="745ae-151">Merhaba yedekleme dosyası adlandırma hello tarih, saat ve veritabanı GUID'si içerir.</span><span class="sxs-lookup"><span data-stu-id="745ae-151">hello backup file naming convention includes hello date, time, and database GUID.</span></span> |
| <span data-ttu-id="745ae-152">**Şifreleme**</span><span class="sxs-lookup"><span data-stu-id="745ae-152">**Encryption**</span></span> |<span data-ttu-id="745ae-153">Etkinleştir/devre dışı bırak (devre dışı)</span><span class="sxs-lookup"><span data-stu-id="745ae-153">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="745ae-154">Etkinleştirir veya şifreleme devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="745ae-154">Enables or disables encryption.</span></span> <span data-ttu-id="745ae-155">Şifreleme etkinleştirildiğinde, hello kullanılan sertifikaları toorestore hello yedekleme bulunur hello belirtilen depolama hesabı hello aynı **automaticbackup** bir kapsayıcı kullanılarak hello aynı adlandırma kuralı.</span><span class="sxs-lookup"><span data-stu-id="745ae-155">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same **automaticbackup** container using hello same naming convention.</span></span> <span data-ttu-id="745ae-156">Merhaba parola değişirse, bu parola ile yeni bir sertifika oluşturulur, ancak toorestore önceki yedeklemeleri hello eski sertifika kalır.</span><span class="sxs-lookup"><span data-stu-id="745ae-156">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="745ae-157">**Parola**</span><span class="sxs-lookup"><span data-stu-id="745ae-157">**Password**</span></span> |<span data-ttu-id="745ae-158">Parola metin</span><span class="sxs-lookup"><span data-stu-id="745ae-158">Password text</span></span> | <span data-ttu-id="745ae-159">Şifreleme anahtarları için bir parola.</span><span class="sxs-lookup"><span data-stu-id="745ae-159">A password for encryption keys.</span></span> <span data-ttu-id="745ae-160">Yalnızca budur şifreleme etkin olup olmadığını gerekli.</span><span class="sxs-lookup"><span data-stu-id="745ae-160">This is only required if encryption is enabled.</span></span> <span data-ttu-id="745ae-161">Sipariş toorestore şifreli bir yedekleme hello doğru parolayı ve hello yedeğin alındığı hello zamanında kullanılan ilgili sertifika olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="745ae-161">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> |

### <a name="advanced-settings"></a><span data-ttu-id="745ae-162">Gelişmiş ayarlar</span><span class="sxs-lookup"><span data-stu-id="745ae-162">Advanced Settings</span></span>

| <span data-ttu-id="745ae-163">Ayar</span><span class="sxs-lookup"><span data-stu-id="745ae-163">Setting</span></span> | <span data-ttu-id="745ae-164">Aralık (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="745ae-164">Range (Default)</span></span> | <span data-ttu-id="745ae-165">Açıklama</span><span class="sxs-lookup"><span data-stu-id="745ae-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="745ae-166">**Sistem Veritabanı Yedeklemeleri**</span><span class="sxs-lookup"><span data-stu-id="745ae-166">**System Database Backups**</span></span> | <span data-ttu-id="745ae-167">Etkinleştir/devre dışı bırak (devre dışı)</span><span class="sxs-lookup"><span data-stu-id="745ae-167">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="745ae-168">Etkinleştirildiğinde, bu özellik ayrıca hello sistem veritabanlarını yedekleyin: Master, MSDB ve Model.</span><span class="sxs-lookup"><span data-stu-id="745ae-168">When enabled, this feature will also back up hello system databases: Master, MSDB, and Model.</span></span> <span data-ttu-id="745ae-169">Merhaba MSDB ve modeli veritabanları için günlük yedekleri toobe gerçekleştirilecek istiyorsanız, bunların tam kurtarma modunda olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="745ae-169">For hello MSDB and Model databases, verify that they are in full recovery mode if you want log backups toobe taken.</span></span> <span data-ttu-id="745ae-170">Günlük yedeklemeler için ana hiçbir zaman alınır.</span><span class="sxs-lookup"><span data-stu-id="745ae-170">Log backups are never taken for Master.</span></span> <span data-ttu-id="745ae-171">Ve yedekleme TempDB için alınır.</span><span class="sxs-lookup"><span data-stu-id="745ae-171">And no backups are taken for TempDB.</span></span> |
| <span data-ttu-id="745ae-172">**Yedekleme zamanlaması**</span><span class="sxs-lookup"><span data-stu-id="745ae-172">**Backup Schedule**</span></span> | <span data-ttu-id="745ae-173">El ile otomatik / (otomatik)</span><span class="sxs-lookup"><span data-stu-id="745ae-173">Manual/Automated (Automated)</span></span> | <span data-ttu-id="745ae-174">Varsayılan olarak, hello Günlük büyüme üzerinde temel hello yedekleme zamanlaması otomatik olarak belirlenir.</span><span class="sxs-lookup"><span data-stu-id="745ae-174">By default, hello backup schedule will be automatically determined based on hello log growth.</span></span> <span data-ttu-id="745ae-175">El ile yedekleme zamanlaması hello kullanıcı toospecify hello zaman penceresi için yedeklemeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="745ae-175">Manual backup schedule allows hello user toospecify hello time window for backups.</span></span> <span data-ttu-id="745ae-176">Bu durumda, yedeklemeler yalnızca şimdiye kadar sürer hello yerinde sıklığı belirtilen ve belirli bir günde zaman penceresi sırasında hello belirtilen.</span><span class="sxs-lookup"><span data-stu-id="745ae-176">In this case, backups will only ever take place at hello specified frequency and during hello specified time window of a given day.</span></span> |
| <span data-ttu-id="745ae-177">**Tam yedekleme sıklığı**</span><span class="sxs-lookup"><span data-stu-id="745ae-177">**Full backup frequency**</span></span> | <span data-ttu-id="745ae-178">Günlük/Haftalık</span><span class="sxs-lookup"><span data-stu-id="745ae-178">Daily/Weekly</span></span> | <span data-ttu-id="745ae-179">Tam yedeklemelerinin sıklığını.</span><span class="sxs-lookup"><span data-stu-id="745ae-179">Frequency of full backups.</span></span> <span data-ttu-id="745ae-180">Her iki durumda da, tam yedeklemeler hello sonraki zamanlanmış zaman penceresi sırasında başlar.</span><span class="sxs-lookup"><span data-stu-id="745ae-180">In both cases, full backups will begin during hello next scheduled time window.</span></span> <span data-ttu-id="745ae-181">Haftalık seçili olduğunda, yedeklemelerin tüm veritabanları başarıyla yedeklediyseniz kadar birden fazla gün kapsayabilir.</span><span class="sxs-lookup"><span data-stu-id="745ae-181">When weekly is selected, backups could span multiple days until all databases have successfully backed up.</span></span> |
| <span data-ttu-id="745ae-182">**Tam yedekleme başlangıç saati**</span><span class="sxs-lookup"><span data-stu-id="745ae-182">**Full backup start time**</span></span> | <span data-ttu-id="745ae-183">00:00 – 23:00 (01:00)</span><span class="sxs-lookup"><span data-stu-id="745ae-183">00:00 – 23:00 (01:00)</span></span> | <span data-ttu-id="745ae-184">Başlangıç sırasında tam yedeklemeler gerçekleştirilebildiği belirli bir gün zamanı.</span><span class="sxs-lookup"><span data-stu-id="745ae-184">Start time of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="745ae-185">**Tam yedekleme zaman penceresi**</span><span class="sxs-lookup"><span data-stu-id="745ae-185">**Full backup time window**</span></span> | <span data-ttu-id="745ae-186">1 – 23 saat (1 saat)</span><span class="sxs-lookup"><span data-stu-id="745ae-186">1 – 23 hours (1 hour)</span></span> | <span data-ttu-id="745ae-187">Hangi sırasında tam yedeklemeler gerçekleştirilebildiği belirli bir gün hello zaman penceresinin süresi.</span><span class="sxs-lookup"><span data-stu-id="745ae-187">Duration of hello time window of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="745ae-188">**Günlük yedekleme sıklığı**</span><span class="sxs-lookup"><span data-stu-id="745ae-188">**Log backup frequency**</span></span> | <span data-ttu-id="745ae-189">5 – 60 dakika (60 dakika)</span><span class="sxs-lookup"><span data-stu-id="745ae-189">5 – 60 minutes (60 minutes)</span></span> | <span data-ttu-id="745ae-190">Günlük yedekleme sıklığı.</span><span class="sxs-lookup"><span data-stu-id="745ae-190">Frequency of log backups.</span></span> |

## <a name="understanding-full-backup-frequency"></a><span data-ttu-id="745ae-191">Tam yedekleme sıklığını anlama</span><span class="sxs-lookup"><span data-stu-id="745ae-191">Understanding full backup frequency</span></span>
<span data-ttu-id="745ae-192">Bu önemli toounderstand hello günlük ve haftalık tam yedeklemeler arasındaki farktır.</span><span class="sxs-lookup"><span data-stu-id="745ae-192">It is important toounderstand hello difference between daily and weekly full backups.</span></span> <span data-ttu-id="745ae-193">Bu çaba içinde iki örnek senaryolar üzerinden size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="745ae-193">In this effort, we will walk through two example scenarios.</span></span>

### <a name="scenario-1-weekly-backups"></a><span data-ttu-id="745ae-194">Senaryo 1: Haftalık yedekleri</span><span class="sxs-lookup"><span data-stu-id="745ae-194">Scenario 1: Weekly backups</span></span>
<span data-ttu-id="745ae-195">Çok büyük veritabanları sayısını içeren bir SQL Server VM var.</span><span class="sxs-lookup"><span data-stu-id="745ae-195">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="745ae-196">Pazartesi günü, ayarlar aşağıdaki hello ile otomatik yedekleme v2 etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="745ae-196">On Monday, you enable Automated Backup v2 with hello following settings:</span></span>

- <span data-ttu-id="745ae-197">Yedekleme zamanlaması: **el ile**</span><span class="sxs-lookup"><span data-stu-id="745ae-197">Backup schedule: **Manual**</span></span>
- <span data-ttu-id="745ae-198">Tam yedekleme sıklığını: **haftalık**</span><span class="sxs-lookup"><span data-stu-id="745ae-198">Full backup frequency: **Weekly**</span></span>
- <span data-ttu-id="745ae-199">Tam yedekleme başlangıç saati: **01:00**</span><span class="sxs-lookup"><span data-stu-id="745ae-199">Full backup start time: **01:00**</span></span>
- <span data-ttu-id="745ae-200">Tam yedekleme zaman penceresi: **1 saat**</span><span class="sxs-lookup"><span data-stu-id="745ae-200">Full backup time window: **1 hour**</span></span>

<span data-ttu-id="745ae-201">Bu, o hello sonraki kullanılabilir Yedekleme penceresi 1 saat 1 sabah Salı olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="745ae-201">This means that hello next available backup window is Tuesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="745ae-202">O anda aynı anda veritabanlarınızı bir yedekleme otomatik yedekleme başlar.</span><span class="sxs-lookup"><span data-stu-id="745ae-202">At that time, Automated Backup will begin backing up your databases one at a time.</span></span> <span data-ttu-id="745ae-203">Bu senaryoda, veritabanlarınızı tam yedeklemeler için ilk birkaç veritabanları hello tamamlayacak yeterli büyüklükte.</span><span class="sxs-lookup"><span data-stu-id="745ae-203">In this scenario, your databases are large enough that full backups will complete for hello first couple databases.</span></span> <span data-ttu-id="745ae-204">Ancak, bir saat sonra tüm hello veritabanları yedeklendi.</span><span class="sxs-lookup"><span data-stu-id="745ae-204">However, after one hour not all of hello databases have been backed up.</span></span>

<span data-ttu-id="745ae-205">Bu durumda, sonraki gün, 1 saat 1 sabah Çarşamba veritabanları hello kalan hello yedekleme otomatik yedekleme başlar.</span><span class="sxs-lookup"><span data-stu-id="745ae-205">When this happens, Automated Backup will begin backing up hello remaining databases hello next day, Wednesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="745ae-206">Bu süre içinde tüm veritabanları yedeklenmiş, yeniden hello sonraki gün aynı hello deneyecek zaman.</span><span class="sxs-lookup"><span data-stu-id="745ae-206">If not all databases have been backed up in that time, it will try again hello next day at hello same time.</span></span> <span data-ttu-id="745ae-207">Tüm veritabanları başarıyla yedeklendi kadar devam eder.</span><span class="sxs-lookup"><span data-stu-id="745ae-207">This will continue until all databases have been successfully backed up.</span></span>

<span data-ttu-id="745ae-208">Salı yeniden ulaştıktan sonra bir kez daha tüm veritabanlarını yedekleme otomatik yedekleme başlar.</span><span class="sxs-lookup"><span data-stu-id="745ae-208">Once it reaches Tuesday again, Automated Backup will begin backing up all databases once again.</span></span>

<span data-ttu-id="745ae-209">Bu senaryo, otomatik yedekleme yalnızca hello belirtilen zaman penceresi içinde çalışır ve her veritabanı haftada bir kez yukarı yedeklenen gösterir.</span><span class="sxs-lookup"><span data-stu-id="745ae-209">This scenario shows that Automated Backup will only operate within hello specified time window, and each database will be backed up once per week.</span></span> <span data-ttu-id="745ae-210">Bu, ayrıca yedeklemeler toospan hello birden çok gün servis talebi için burada olası toocomplete değil tüm yedeklemeler tek bir günde, olası olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="745ae-210">This also shows that it is possible for backups toospan multiple days in hello case where it is not possible toocomplete all backups in a single day.</span></span>

### <a name="scenario-2-daily-backups"></a><span data-ttu-id="745ae-211">Senaryo 2: Günlük yedeklemeler</span><span class="sxs-lookup"><span data-stu-id="745ae-211">Scenario 2: Daily backups</span></span>
<span data-ttu-id="745ae-212">Çok büyük veritabanları sayısını içeren bir SQL Server VM var.</span><span class="sxs-lookup"><span data-stu-id="745ae-212">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="745ae-213">Pazartesi günü, ayarlar aşağıdaki hello ile otomatik yedekleme v2 etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="745ae-213">On Monday, you enable Automated Backup v2 with hello following settings:</span></span>

- <span data-ttu-id="745ae-214">Yedekleme zamanlaması: el ile</span><span class="sxs-lookup"><span data-stu-id="745ae-214">Backup schedule: Manual</span></span>
- <span data-ttu-id="745ae-215">Tam yedekleme sıklığını: günlük</span><span class="sxs-lookup"><span data-stu-id="745ae-215">Full backup frequency: Daily</span></span>
- <span data-ttu-id="745ae-216">Tam yedekleme başlangıç saati: 22:00</span><span class="sxs-lookup"><span data-stu-id="745ae-216">Full backup start time: 22:00</span></span>
- <span data-ttu-id="745ae-217">Tam yedekleme zaman penceresi: 6 saat</span><span class="sxs-lookup"><span data-stu-id="745ae-217">Full backup time window: 6 hours</span></span>

<span data-ttu-id="745ae-218">Bu, o hello sonraki kullanılabilir Yedekleme penceresi 10 PM 6 saat boyunca Pazartesi altındadır anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="745ae-218">This means that hello next available backup window is Monday at 10 PM for 6 hours.</span></span> <span data-ttu-id="745ae-219">O anda aynı anda veritabanlarınızı bir yedekleme otomatik yedekleme başlar.</span><span class="sxs-lookup"><span data-stu-id="745ae-219">At that time, Automated Backup will begin backing up your databases one at a time.</span></span>

<span data-ttu-id="745ae-220">Ardından, 6 saat boyunca 10 Salı günü, tüm veritabanlarının tam yedeklemeler yeniden başlatılacak.</span><span class="sxs-lookup"><span data-stu-id="745ae-220">Then, on Tuesday at 10 for 6 hours, full backups of all databases will start again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="745ae-221">Günlük yedeklemeler zamanlarken, tüm veritabanları, bu süre içinde yedeklenebilir geniş zaman penceresi tooensure zamanla tavsiye edilir.</span><span class="sxs-lookup"><span data-stu-id="745ae-221">When scheduling daily backups, it is recommended that you schedule a wide time window tooensure all databases can be backed up within this time.</span></span> <span data-ttu-id="745ae-222">Bu, özellikle çok miktarda veri tooback sahip olduğu yukarı hello durumda önemlidir.</span><span class="sxs-lookup"><span data-stu-id="745ae-222">This is especially important in hello case where you have a large amount of data tooback up.</span></span>

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="745ae-223">Merhaba Portal Yapılandırması</span><span class="sxs-lookup"><span data-stu-id="745ae-223">Configuration in hello Portal</span></span>

<span data-ttu-id="745ae-224">Hello Azure portal tooconfigure otomatik yedekleme v2 sağlama sırasında veya var olan SQL Server 2016 VM'ler için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="745ae-224">You can use hello Azure portal tooconfigure Automated Backup v2 during provisioning or for existing SQL Server 2016 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="745ae-225">Yeni sanal makineleri</span><span class="sxs-lookup"><span data-stu-id="745ae-225">New VMs</span></span>

<span data-ttu-id="745ae-226">Merhaba Resource Manager dağıtım modelinde yeni bir SQL Server 2016 sanal makine oluşturduğunuzda hello Azure portal tooconfigure otomatik yedekleme v2 kullanın.</span><span class="sxs-lookup"><span data-stu-id="745ae-226">Use hello Azure portal tooconfigure Automated Backup v2 when you create a new SQL Server 2016 Virtual Machine in hello Resource Manager deployment model.</span></span> 

<span data-ttu-id="745ae-227">Merhaba, **SQL Server ayarları** dikey penceresinde, select **otomatik yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="745ae-227">In hello **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="745ae-228">Merhaba aşağıdaki Azure portal ekran görüntüsü gösterir hello **SQL otomatik yedekleme** dikey.</span><span class="sxs-lookup"><span data-stu-id="745ae-228">hello following Azure portal screenshot shows hello **SQL Automated Backup** blade.</span></span>

![Azure portalında SQL otomatik yedekleme yapılandırması](./media/virtual-machines-windows-sql-automated-backup-v2/automated-backup-blade.png)

> [!NOTE]
> <span data-ttu-id="745ae-230">Otomatik yedekleme v2 varsayılan olarak devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="745ae-230">Automated Backup v2 is disabled by default.</span></span>

<span data-ttu-id="745ae-231">Bağlam için hello tam üzerinde konusuna [azure'da bir SQL Server sanal makine sağlama](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="745ae-231">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="745ae-232">Var olan sanal makineleri</span><span class="sxs-lookup"><span data-stu-id="745ae-232">Existing VMs</span></span>

<span data-ttu-id="745ae-233">Var olan SQL Server sanal makineler için SQL Server sanal makine seçin.</span><span class="sxs-lookup"><span data-stu-id="745ae-233">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="745ae-234">Merhaba seçip **SQL Server yapılandırma** hello bölümünü **ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="745ae-234">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![Var olan VM'ler için SQL otomatik yedekleme](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration.png)

<span data-ttu-id="745ae-236">Merhaba, **SQL Server yapılandırma** dikey penceresinde hello tıklatın **Düzenle** hello düğmesini otomatik yedekleme bölümü.</span><span class="sxs-lookup"><span data-stu-id="745ae-236">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated backup section.</span></span>

![SQL otomatik yedekleme var olan VM'ler için yapılandırma](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration-edit.png)

<span data-ttu-id="745ae-238">Tamamlandığında, hello tıklatın **Tamam** hello hello alt düğmesinde **SQL Server yapılandırma** dikey toosave değişikliklerinizi.</span><span class="sxs-lookup"><span data-stu-id="745ae-238">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="745ae-239">Otomatik yedekleme hello için ilk kez etkinleştiriyorsanız Azure hello SQL Server Iaas Aracısı hello arka planda yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="745ae-239">If you are enabling Automated Backup for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="745ae-240">Bu süre boyunca hello Azure portal otomatik yedekleme yapılandırıldığını gösterilmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="745ae-240">During this time, hello Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="745ae-241">Merhaba Aracısı toobe yüklü, birkaç dakika bekleyin yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="745ae-241">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="745ae-242">Bu hello sonra Azure portalı hello yeni ayarları yansıtır.</span><span class="sxs-lookup"><span data-stu-id="745ae-242">After that hello Azure portal will reflect hello new settings.</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="745ae-243">PowerShell ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="745ae-243">Configuration with PowerShell</span></span>

<span data-ttu-id="745ae-244">PowerShell tooconfigure otomatik yedekleme v2 kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="745ae-244">You can use PowerShell tooconfigure Automated Backup v2.</span></span> <span data-ttu-id="745ae-245">Başlamadan önce şunları yapmalısınız:</span><span class="sxs-lookup"><span data-stu-id="745ae-245">Before you begin, you must:</span></span>

- <span data-ttu-id="745ae-246">[Karşıdan yükleme ve en son Azure PowerShell hello](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="745ae-246">[Download and install hello latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="745ae-247">Windows PowerShell'i açın ve hesabınızla ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="745ae-247">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="745ae-248">Merhaba hello adımları izleyerek bunu yapabilirsiniz [aboneliğinizi yapılandırma](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) konu sağlama hello bölümü.</span><span class="sxs-lookup"><span data-stu-id="745ae-248">You can do this by following hello steps in hello [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of hello provisioning topic.</span></span>

### <a name="install-hello-sql-iaas-extension"></a><span data-ttu-id="745ae-249">Merhaba SQL Iaas uzantısı yükleyin</span><span class="sxs-lookup"><span data-stu-id="745ae-249">Install hello SQL IaaS Extension</span></span>
<span data-ttu-id="745ae-250">SQL Server sanal makineden hello Azure portal sağlanan, hello SQL Server Iaas uzantısı zaten yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="745ae-250">If you provisioned a SQL Server virtual machine from hello Azure portal, hello SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="745ae-251">Bu VM için çağırarak yüklü olup olmadığını belirlemek **Get-AzureRmVM** komutu ve hello inceleyerek **uzantıları** özelliği.</span><span class="sxs-lookup"><span data-stu-id="745ae-251">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining hello **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions 
```

<span data-ttu-id="745ae-252">SQL Server Iaas Aracısı uzantısı Hello yüklediyseniz, "Sqlıaasagent" veya "SQLIaaSExtension" olarak listelenen görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="745ae-252">If hello SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="745ae-253">**ProvisioningState** için hello uzantısı "Başarılı" göstermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="745ae-253">**ProvisioningState** for hello extension should also show “Succeeded”.</span></span> 

<span data-ttu-id="745ae-254">Yüklü değil ya da sağlanan toobe başarısız olursa, komutu aşağıdaki hello ile yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="745ae-254">If it is not installed or failed toobe provisioned, you can install it with hello following command.</span></span> <span data-ttu-id="745ae-255">Toplama toohello VM adını ve kaynak grubunda de hello bölge belirtmeniz gerekir (**$region**), VM bulunur.</span><span class="sxs-lookup"><span data-stu-id="745ae-255">In addition toohello VM name and resource group, you must also specify hello region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region 
```

### <span data-ttu-id="745ae-256"><a id="verifysettings"></a>Geçerli ayarlarını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="745ae-256"><a id="verifysettings"></a> Verify current settings</span></span>
<span data-ttu-id="745ae-257">Sağlama işlemi sırasında otomatik yedekleme etkinleştirilirse, geçerli yapılandırmanızı PowerShell toocheck kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="745ae-257">If you enabled automated backup during provisioning, you can use PowerShell toocheck your current configuration.</span></span> <span data-ttu-id="745ae-258">Merhaba çalıştırmak **Get-AzureRmVMSqlServerExtension** komut ve hello inceleyin **AutoBackupSettings** özelliği:</span><span class="sxs-lookup"><span data-stu-id="745ae-258">Run hello **Get-AzureRmVMSqlServerExtension** command and examine hello **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="745ae-259">Çıktı benzer toohello aşağıdaki almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="745ae-259">You should get output similar toohello following:</span></span>

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

<span data-ttu-id="745ae-260">Çıktı gösteriyorsa **etkinleştirmek** çok ayarlanır**yanlış**, tooenable otomatik yedekleme sahip.</span><span class="sxs-lookup"><span data-stu-id="745ae-260">If your output shows that **Enable** is set too**False**, then you have tooenable automated backup.</span></span> <span data-ttu-id="745ae-261">Merhaba iyi haber etkinleştirme ve otomatik yedekleme hello yapılandırma olan şekilde.</span><span class="sxs-lookup"><span data-stu-id="745ae-261">hello good news is that you enable and configure Automated Backup in hello same way.</span></span> <span data-ttu-id="745ae-262">Bu bilgi Hello sonraki bölüme bakın.</span><span class="sxs-lookup"><span data-stu-id="745ae-262">See hello next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="745ae-263">Hemen bir değişiklik yaptıktan sonra hello ayarlarını denetleyin, hello eski yapılandırma değerlerini geri alırsınız mümkündür.</span><span class="sxs-lookup"><span data-stu-id="745ae-263">If you check hello settings immediately after making a change, it is possible that you will get back hello old configuration values.</span></span> <span data-ttu-id="745ae-264">Birkaç dakika bekleyin ve hello ayarlarını kontrol edin yeniden değişikliklerinizi uygulandığından emin toomake.</span><span class="sxs-lookup"><span data-stu-id="745ae-264">Wait a few minutes and check hello settings again toomake sure that your changes were applied.</span></span>

### <a name="configure-automated-backup-v2"></a><span data-ttu-id="745ae-265">Otomatik yedekleme v2 yapılandırın</span><span class="sxs-lookup"><span data-stu-id="745ae-265">Configure Automated Backup v2</span></span>
<span data-ttu-id="745ae-266">Toomodify yanı sıra PowerShell tooenable otomatik yedekleme yapılandırması ve davranış herhangi bir zamanda kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="745ae-266">You can use PowerShell tooenable Automated Backup as well as toomodify its configuration and behavior at any time.</span></span> 

<span data-ttu-id="745ae-267">İlk olarak, seçin veya yedekleme dosyalarını hello için bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="745ae-267">First, select or create a storage account for hello backup files.</span></span> <span data-ttu-id="745ae-268">Merhaba aşağıdaki komut dosyasını bir depolama hesabı seçer veya henüz yoksa oluşturur.</span><span class="sxs-lookup"><span data-stu-id="745ae-268">hello following script selects a storage account or creates it if it does not exist.</span></span>

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
> <span data-ttu-id="745ae-269">Otomatik yedekleme premium depolama alanına depolanmasını yedeklemeleri desteklemez, ancak Premium depolama kullanan VM diskleri yedeklemelerden alabilir.</span><span class="sxs-lookup"><span data-stu-id="745ae-269">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="745ae-270">Merhaba kullanmak **yeni AzureRmVMSqlServerAutoBackupConfig** komut tooenable ve hello Azure depolama hesabında hello otomatik yedekleme v2 ayarları toostore yedeklemelerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="745ae-270">Then use hello **New-AzureRmVMSqlServerAutoBackupConfig** command tooenable and configure hello Automated Backup v2 settings toostore backups in hello Azure storage account.</span></span> <span data-ttu-id="745ae-271">Bu örnekte, 10 gün boyunca tutulur toobe hello yedeklemeleri ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="745ae-271">In this example, hello backups are set toobe retained for 10 days.</span></span> <span data-ttu-id="745ae-272">Sistem Veritabanı Yedeklemeleri etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="745ae-272">System database backups are enabled.</span></span> <span data-ttu-id="745ae-273">Tam yedeklemeler için haftalık iki saat 20:00 başlayarak bir zaman penceresi ile zamanlanır.</span><span class="sxs-lookup"><span data-stu-id="745ae-273">Full backups are scheduled for weekly with a time window starting at 20:00 for two hours.</span></span> <span data-ttu-id="745ae-274">Günlük yedeklemeler için 30 dakikada zamanlanır.</span><span class="sxs-lookup"><span data-stu-id="745ae-274">Log backups are scheduled for every 30 minutes.</span></span> <span data-ttu-id="745ae-275">Merhaba ikinci komut, **kümesi AzureRmVMSqlServerExtension**, güncelleştirmelerinin hello Azure VM bu ayarlarla belirtilen.</span><span class="sxs-lookup"><span data-stu-id="745ae-275">hello second command, **Set-AzureRmVMSqlServerExtension**, updates hello specified Azure VM with these settings.</span></span>

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

<span data-ttu-id="745ae-276">Birkaç dakika tooinstall alın ve hello SQL Server Iaas Aracısı Yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="745ae-276">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span> 

<span data-ttu-id="745ae-277">tooenable şifreleme hello önceki betik toopass hello değiştirme **EnableEncryption** parametresi hello için bir parola (güvenli dize) ile birlikte **CertificatePassword** parametresi.</span><span class="sxs-lookup"><span data-stu-id="745ae-277">tooenable encryption, modify hello previous script toopass hello **EnableEncryption** parameter along with a password (secure string) for hello **CertificatePassword** parameter.</span></span> <span data-ttu-id="745ae-278">Merhaba aşağıdaki betiği hello önceki örnekte hello otomatik yedekleme ayarlarını etkinleştirir ve şifreleme ekler.</span><span class="sxs-lookup"><span data-stu-id="745ae-278">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

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

<span data-ttu-id="745ae-279">ayarlarınızı uygulanır, tooconfirm [hello otomatik yedekleme yapılandırması doğrulayın](#verifysettings).</span><span class="sxs-lookup"><span data-stu-id="745ae-279">tooconfirm your settings are applied, [verify hello Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="745ae-280">Otomatik yedekleme devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="745ae-280">Disable Automated Backup</span></span>
<span data-ttu-id="745ae-281">Otomatik yedekleme, hello aynı komut dosyası çalıştırma hello toodisable **-etkinleştirmek** parametresi toohello **yeni AzureRmVMSqlServerAutoBackupConfig** komutu.</span><span class="sxs-lookup"><span data-stu-id="745ae-281">toodisable Automated Backup, run hello same script without hello **-Enable** parameter toohello **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="745ae-282">Merhaba hello yokluğu **-etkinleştirmek** parametresi sinyalleri hello komutu toodisable hello özelliği.</span><span class="sxs-lookup"><span data-stu-id="745ae-282">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span> <span data-ttu-id="745ae-283">Yüklemesine gibi birkaç dakika toodisable otomatik yedekleme alabilir.</span><span class="sxs-lookup"><span data-stu-id="745ae-283">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="745ae-284">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="745ae-284">Example script</span></span>
<span data-ttu-id="745ae-285">Merhaba aşağıdaki komut dosyası değişkenleri kümesinin tooenable özelleştirebilir ve VM için otomatik yedeklemeyi yapılandırın sağlar.</span><span class="sxs-lookup"><span data-stu-id="745ae-285">hello following script provides a set of variables that you can customize tooenable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="745ae-286">Sizin durumunuzda, gereksinimlerinize göre toocustomize hello komut dosyası gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="745ae-286">In your case, you might need toocustomize hello script based on your requirements.</span></span> <span data-ttu-id="745ae-287">Örneğin, sistem veritabanlarının toodisable hello yedekleme istediyseniz toomake değişikliklerinin veya şifrelemeyi etkinleştirmeniz.</span><span class="sxs-lookup"><span data-stu-id="745ae-287">For example, you would have toomake changes if you wanted toodisable hello backup of system databases or enable encryption.</span></span>

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

# ResourceGroupName is hello resource group which is hosting hello VM where you are deploying hello SQL IaaS Extension 

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account toostore hello backups

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

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="745ae-288">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="745ae-288">Next steps</span></span>
<span data-ttu-id="745ae-289">Otomatik yedekleme v2 yönetilen yedekleme Azure Vm'lerinde yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="745ae-289">Automated Backup v2 configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="745ae-290">Çok önemlidir[yönetilen yedekleme hello belgelerini gözden geçirin](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello davranışı ve etkileri.</span><span class="sxs-lookup"><span data-stu-id="745ae-290">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="745ae-291">Ek yedekleme bulmak ve izleyen konu hello Azure Vm'lerde SQL Server için kılavuzunda geri yükleyebilirsiniz: [yedekleme ve geri yükleme Azure Virtual Machines'de SQL Server için](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="745ae-291">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="745ae-292">Diğer kullanılabilir Otomasyon görevler hakkında daha fazla bilgi için bkz: [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="745ae-292">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="745ae-293">Azure Vm'lerinde SQL Server çalıştırma hakkında daha fazla bilgi için bkz: [Azure sanal makinelere genel bakış SQL Server'da](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="745ae-293">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

