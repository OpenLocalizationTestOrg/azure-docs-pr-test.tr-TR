---
title: "aaaAutomated yedekleme SQL Server 2014 Azure Virtual Machines için | Microsoft Docs"
description: "SQL Server 2014 Azure'da çalışan VM'ler için Hello otomatik yedekleme özelliğini açıklar. Bu makalede hello Kaynak Yöneticisi'ni kullanarak belirli tooVMs ' dir."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: bdc63fd1-db49-4e76-87d5-b5c6a890e53c
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: c6803d8ef9f80e44a2f87918d87e099f1b562483
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a><span data-ttu-id="ee55f-104">SQL Server 2014 sanal makineler (Resource Manager) için otomatik yedekleme</span><span class="sxs-lookup"><span data-stu-id="ee55f-104">Automated Backup for SQL Server 2014 Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ee55f-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="ee55f-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="ee55f-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="ee55f-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="ee55f-107">Otomatik yedekleme otomatik olarak yapılandırır [yönetilen yedekleme tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) SQL Server 2014 Standard veya Enterprise çalıştıran bir Azure VM üzerindeki tüm mevcut ve yeni veritabanları için.</span><span class="sxs-lookup"><span data-stu-id="ee55f-107">Automated Backup automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="ee55f-108">Bu, dayanıklı Azure blob depolama alanını tooconfigure normal veritabanı yedeklemeleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="ee55f-108">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="ee55f-109">Otomatik yedekleme bağlıdır hello üzerinde [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="ee55f-109">Automated Backup depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="ee55f-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ee55f-110">Prerequisites</span></span>
<span data-ttu-id="ee55f-111">toouse otomatik yedekleme önkoşulları aşağıdaki hello göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="ee55f-111">toouse Automated Backup, consider hello following prerequisites:</span></span>

<span data-ttu-id="ee55f-112">**İşletim sistemi**:</span><span class="sxs-lookup"><span data-stu-id="ee55f-112">**Operating System**:</span></span>

- <span data-ttu-id="ee55f-113">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="ee55f-113">Windows Server 2012</span></span>
- <span data-ttu-id="ee55f-114">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="ee55f-114">Windows Server 2012 R2</span></span>
- <span data-ttu-id="ee55f-115">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="ee55f-115">Windows Server 2016</span></span>

<span data-ttu-id="ee55f-116">**SQL Server sürümü/yayını**:</span><span class="sxs-lookup"><span data-stu-id="ee55f-116">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="ee55f-117">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="ee55f-117">SQL Server 2014 Standard</span></span>
- <span data-ttu-id="ee55f-118">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="ee55f-118">SQL Server 2014 Enterprise</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee55f-119">Otomatik yedekleme SQL Server 2014 ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="ee55f-119">Automated Backup works with SQL Server 2014.</span></span> <span data-ttu-id="ee55f-120">SQL Server 2016 kullanıyorsanız, veritabanlarınızı otomatik yedekleme v2 tooback kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee55f-120">If you are using SQL Server 2016, you can use Automated Backup v2 tooback up your databases.</span></span> <span data-ttu-id="ee55f-121">Daha fazla bilgi için bkz: [otomatik yedekleme v2 SQL Server 2016 Azure Virtual Machines için](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="ee55f-121">For more information, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="ee55f-122">**Veritabanı yapılandırması**:</span><span class="sxs-lookup"><span data-stu-id="ee55f-122">**Database configuration**:</span></span>

- <span data-ttu-id="ee55f-123">Hedef veritabanlarına hello tam kurtarma modeli kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee55f-123">Target databases must use hello full recovery model.</span></span> <span data-ttu-id="ee55f-124">Daha fazla bilgi hello tam kurtarma modeli için hello etkisi hakkında yedeklemeleri üzerinde [yedekleme altında tam kurtarma modeli hello](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="ee55f-124">For more information about hello impact of hello full recovery model on backups, see [Backup Under hello Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="ee55f-125">Hedef veritabanlarına hello varsayılan SQL Server örneğinde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee55f-125">Target databases must be on hello default SQL Server instance.</span></span> <span data-ttu-id="ee55f-126">SQL Server Iaas uzantısı Hello adlandırılmış örnekleri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="ee55f-126">hello SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="ee55f-127">**Azure dağıtım modeli**:</span><span class="sxs-lookup"><span data-stu-id="ee55f-127">**Azure deployment model**:</span></span>

- <span data-ttu-id="ee55f-128">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ee55f-128">Resource Manager</span></span>

<span data-ttu-id="ee55f-129">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="ee55f-129">**Azure PowerShell**:</span></span>

- <span data-ttu-id="ee55f-130">[Merhaba en son Azure PowerShell komutlarını yüklemek](/powershell/azure/overview) tooconfigure PowerShell ile otomatik yedekleme planlıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="ee55f-130">[Install hello latest Azure PowerShell commands](/powershell/azure/overview) if you plan tooconfigure Automated Backup with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="ee55f-131">Otomatik yedekleme hello üzerinde SQL Server Iaas Aracısı uzantısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="ee55f-131">Automated Backup relies on hello SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="ee55f-132">Geçerli SQL sanal makineye Galerisi görüntülerini varsayılan olarak bu uzantı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ee55f-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="ee55f-133">Daha fazla bilgi için bkz: [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="ee55f-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="ee55f-134">Ayarlar</span><span class="sxs-lookup"><span data-stu-id="ee55f-134">Settings</span></span>

<span data-ttu-id="ee55f-135">Merhaba aşağıdaki tabloda otomatik yedekleme için yapılandırılmış hello seçenekleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ee55f-135">hello following table describes hello options that can be configured for Automated Backup.</span></span> <span data-ttu-id="ee55f-136">Merhaba gerçek yapılandırma adımlarını hello Azure portalında veya Azure Windows PowerShell komutlarını kullanmadığınıza bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="ee55f-136">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="ee55f-137">Ayar</span><span class="sxs-lookup"><span data-stu-id="ee55f-137">Setting</span></span> | <span data-ttu-id="ee55f-138">Aralık (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="ee55f-138">Range (Default)</span></span> | <span data-ttu-id="ee55f-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee55f-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ee55f-140">**Otomatik Yedekleme**</span><span class="sxs-lookup"><span data-stu-id="ee55f-140">**Automated Backup**</span></span> | <span data-ttu-id="ee55f-141">Etkinleştir/devre dışı bırak (devre dışı)</span><span class="sxs-lookup"><span data-stu-id="ee55f-141">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="ee55f-142">Etkinleştirir veya SQL Server 2014 Standard veya Enterprise çalıştıran bir Azure VM için otomatik yedekleme devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="ee55f-142">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="ee55f-143">**Saklama süresi**</span><span class="sxs-lookup"><span data-stu-id="ee55f-143">**Retention Period**</span></span> | <span data-ttu-id="ee55f-144">1-30 gün (30 gün)</span><span class="sxs-lookup"><span data-stu-id="ee55f-144">1-30 days (30 days)</span></span> | <span data-ttu-id="ee55f-145">gün tooretain bir yedekleme Hello sayısı.</span><span class="sxs-lookup"><span data-stu-id="ee55f-145">hello number of days tooretain a backup.</span></span> |
| <span data-ttu-id="ee55f-146">**Depolama hesabı**</span><span class="sxs-lookup"><span data-stu-id="ee55f-146">**Storage Account**</span></span> | <span data-ttu-id="ee55f-147">Azure depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="ee55f-147">Azure storage account</span></span> | <span data-ttu-id="ee55f-148">Blob depolama alanına otomatik yedekleme dosyalarını depolamak için bir Azure depolama hesabı toouse.</span><span class="sxs-lookup"><span data-stu-id="ee55f-148">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="ee55f-149">Bir kapsayıcı sırasında bu konumu toostore tüm yedekleme dosyaları oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ee55f-149">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="ee55f-150">Merhaba yedekleme dosyası adlandırma hello tarih, saat ve makine adını içerir.</span><span class="sxs-lookup"><span data-stu-id="ee55f-150">hello backup file naming convention includes hello date, time, and machine name.</span></span> |
| <span data-ttu-id="ee55f-151">**Şifreleme**</span><span class="sxs-lookup"><span data-stu-id="ee55f-151">**Encryption**</span></span> | <span data-ttu-id="ee55f-152">Etkinleştir/devre dışı bırak (devre dışı)</span><span class="sxs-lookup"><span data-stu-id="ee55f-152">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="ee55f-153">Etkinleştirir veya şifreleme devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="ee55f-153">Enables or disables encryption.</span></span> <span data-ttu-id="ee55f-154">Şifreleme etkinleştirildiğinde, hello kullanılan sertifikaları toorestore hello yedekleme bulunur hello belirtilen depolama hesabı hello aynı `automaticbackup` bir kapsayıcı kullanılarak hello aynı adlandırma kuralı.</span><span class="sxs-lookup"><span data-stu-id="ee55f-154">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same `automaticbackup` container using hello same naming convention.</span></span> <span data-ttu-id="ee55f-155">Merhaba parola değişirse, bu parola ile yeni bir sertifika oluşturulur, ancak toorestore önceki yedeklemeleri hello eski sertifika kalır.</span><span class="sxs-lookup"><span data-stu-id="ee55f-155">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="ee55f-156">**Parola**</span><span class="sxs-lookup"><span data-stu-id="ee55f-156">**Password**</span></span> | <span data-ttu-id="ee55f-157">Parola metin</span><span class="sxs-lookup"><span data-stu-id="ee55f-157">Password text</span></span> | <span data-ttu-id="ee55f-158">Şifreleme anahtarları için bir parola.</span><span class="sxs-lookup"><span data-stu-id="ee55f-158">A password for encryption keys.</span></span> <span data-ttu-id="ee55f-159">Yalnızca budur şifreleme etkin olup olmadığını gerekli.</span><span class="sxs-lookup"><span data-stu-id="ee55f-159">This is only required if encryption is enabled.</span></span> <span data-ttu-id="ee55f-160">Sipariş toorestore şifreli bir yedekleme hello doğru parolayı ve hello yedeğin alındığı hello zamanında kullanılan ilgili sertifika olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ee55f-160">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> |

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="ee55f-161">Merhaba Portal Yapılandırması</span><span class="sxs-lookup"><span data-stu-id="ee55f-161">Configuration in hello Portal</span></span>

<span data-ttu-id="ee55f-162">Hello Azure portal tooconfigure otomatik yedekleme sağlama sırasında veya var olan SQL Server 2014 VM'ler için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee55f-162">You can use hello Azure portal tooconfigure Automated Backup during provisioning or for existing SQL Server 2014 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="ee55f-163">Yeni sanal makineleri</span><span class="sxs-lookup"><span data-stu-id="ee55f-163">New VMs</span></span>

<span data-ttu-id="ee55f-164">Merhaba Resource Manager dağıtım modelinde yeni bir SQL Server 2014 sanal makine oluşturduğunuzda hello Azure portal tooconfigure otomatik yedekleme kullanın.</span><span class="sxs-lookup"><span data-stu-id="ee55f-164">Use hello Azure portal tooconfigure Automated Backup when you create a new SQL Server 2014 Virtual Machine in hello Resource Manager deployment model.</span></span>

<span data-ttu-id="ee55f-165">Merhaba, **SQL Server ayarları** dikey penceresinde, select **otomatik yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="ee55f-165">In hello **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="ee55f-166">Merhaba aşağıdaki Azure portal ekran görüntüsü gösterir hello **SQL otomatik yedekleme** dikey.</span><span class="sxs-lookup"><span data-stu-id="ee55f-166">hello following Azure portal screenshot shows hello **SQL Automated Backup** blade.</span></span>

![Azure portalında SQL otomatik yedekleme yapılandırması](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

<span data-ttu-id="ee55f-168">Bağlam için hello tam üzerinde konusuna [azure'da bir SQL Server sanal makine sağlama](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="ee55f-168">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="ee55f-169">Var olan sanal makineleri</span><span class="sxs-lookup"><span data-stu-id="ee55f-169">Existing VMs</span></span>

<span data-ttu-id="ee55f-170">Var olan SQL Server sanal makineler için SQL Server sanal makine seçin.</span><span class="sxs-lookup"><span data-stu-id="ee55f-170">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="ee55f-171">Merhaba seçip **SQL Server yapılandırma** hello bölümünü **ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="ee55f-171">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![Var olan VM'ler için SQL otomatik yedekleme](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

<span data-ttu-id="ee55f-173">Merhaba, **SQL Server yapılandırma** dikey penceresinde hello tıklatın **Düzenle** hello düğmesini otomatik yedekleme bölümü.</span><span class="sxs-lookup"><span data-stu-id="ee55f-173">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated backup section.</span></span>

![SQL otomatik yedekleme var olan VM'ler için yapılandırma](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

<span data-ttu-id="ee55f-175">Tamamlandığında, hello tıklatın **Tamam** hello hello alt düğmesinde **SQL Server yapılandırma** dikey toosave değişikliklerinizi.</span><span class="sxs-lookup"><span data-stu-id="ee55f-175">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="ee55f-176">Otomatik yedekleme hello için ilk kez etkinleştiriyorsanız Azure hello SQL Server Iaas Aracısı hello arka planda yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="ee55f-176">If you are enabling Automated Backup for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="ee55f-177">Bu süre boyunca hello Azure portal otomatik yedekleme yapılandırıldığını gösterilmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="ee55f-177">During this time, hello Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="ee55f-178">Merhaba Aracısı toobe yüklü, birkaç dakika bekleyin yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="ee55f-178">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="ee55f-179">Bu hello sonra Azure portalı hello yeni ayarları yansıtır.</span><span class="sxs-lookup"><span data-stu-id="ee55f-179">After that hello Azure portal will reflect hello new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="ee55f-180">Otomatik yedekleme bir şablon kullanarak da yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee55f-180">You can also configure Automated Backup using a template.</span></span> <span data-ttu-id="ee55f-181">Daha fazla bilgi için bkz: [otomatik yedekleme için Azure Hızlı Başlangıç şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span><span class="sxs-lookup"><span data-stu-id="ee55f-181">For more information, see [Azure quickstart template for Automated Backup](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="ee55f-182">PowerShell ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ee55f-182">Configuration with PowerShell</span></span>

<span data-ttu-id="ee55f-183">PowerShell tooconfigure otomatik yedekleme kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee55f-183">You can use PowerShell tooconfigure Automated Backup.</span></span> <span data-ttu-id="ee55f-184">Başlamadan önce şunları yapmalısınız:</span><span class="sxs-lookup"><span data-stu-id="ee55f-184">Before you begin, you must:</span></span>

- <span data-ttu-id="ee55f-185">[Karşıdan yükleme ve en son Azure PowerShell hello](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="ee55f-185">[Download and install hello latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="ee55f-186">Windows PowerShell'i açın ve hesabınızla ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee55f-186">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="ee55f-187">Merhaba hello adımları izleyerek bunu yapabilirsiniz [aboneliğinizi yapılandırma](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) konu sağlama hello bölümü.</span><span class="sxs-lookup"><span data-stu-id="ee55f-187">You can do this by following hello steps in hello [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of hello provisioning topic.</span></span>

### <a name="install-hello-sql-iaas-extension"></a><span data-ttu-id="ee55f-188">Merhaba SQL Iaas uzantısı yükleyin</span><span class="sxs-lookup"><span data-stu-id="ee55f-188">Install hello SQL IaaS Extension</span></span>
<span data-ttu-id="ee55f-189">SQL Server sanal makineden hello Azure portal sağlanan, hello SQL Server Iaas uzantısı zaten yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ee55f-189">If you provisioned a SQL Server virtual machine from hello Azure portal, hello SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="ee55f-190">Bu VM için çağırarak yüklü olup olmadığını belirlemek **Get-AzureRmVM** komutu ve hello inceleyerek **uzantıları** özelliği.</span><span class="sxs-lookup"><span data-stu-id="ee55f-190">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining hello **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions
```

<span data-ttu-id="ee55f-191">SQL Server Iaas Aracısı uzantısı Hello yüklediyseniz, "Sqlıaasagent" veya "SQLIaaSExtension" olarak listelenen görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee55f-191">If hello SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="ee55f-192">**ProvisioningState** için hello uzantısı "Başarılı" göstermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee55f-192">**ProvisioningState** for hello extension should also show “Succeeded”.</span></span>

<span data-ttu-id="ee55f-193">Yüklü değil ya da sağlanan toobe başarısız olursa, komutu aşağıdaki hello ile yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee55f-193">If it is not installed or failed toobe provisioned, you can install it with hello following command.</span></span> <span data-ttu-id="ee55f-194">Toplama toohello VM adını ve kaynak grubunda de hello bölge belirtmeniz gerekir (**$region**), VM bulunur.</span><span class="sxs-lookup"><span data-stu-id="ee55f-194">In addition toohello VM name and resource group, you must also specify hello region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region
```

### <span data-ttu-id="ee55f-195"><a id="verifysettings"></a>Geçerli ayarlarını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="ee55f-195"><a id="verifysettings"></a> Verify current settings</span></span>

<span data-ttu-id="ee55f-196">Sağlama işlemi sırasında otomatik yedekleme etkinleştirilirse, geçerli yapılandırmanızı PowerShell toocheck kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee55f-196">If you enabled automated backup during provisioning, you can use PowerShell toocheck your current configuration.</span></span> <span data-ttu-id="ee55f-197">Merhaba çalıştırmak **Get-AzureRmVMSqlServerExtension** komut ve hello inceleyin **AutoBackupSettings** özelliği:</span><span class="sxs-lookup"><span data-stu-id="ee55f-197">Run hello **Get-AzureRmVMSqlServerExtension** command and examine hello **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="ee55f-198">Çıktı benzer toohello aşağıdaki almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ee55f-198">You should get output similar toohello following:</span></span>

```
Enable                      : False
EnableEncryption            : False
RetentionPeriod             : -1
StorageUrl                  : NOTSET
StorageAccessKey            : 
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : 
FullBackupFrequency         : 
FullBackupStartTime         : 
FullBackupWindowHours       : 
LogBackupFrequency          : 
```

<span data-ttu-id="ee55f-199">Çıktı gösteriyorsa **etkinleştirmek** çok ayarlanır**yanlış**, tooenable otomatik yedekleme sahip.</span><span class="sxs-lookup"><span data-stu-id="ee55f-199">If your output shows that **Enable** is set too**False**, then you have tooenable automated backup.</span></span> <span data-ttu-id="ee55f-200">Merhaba iyi haber etkinleştirme ve otomatik yedekleme hello yapılandırma olan şekilde.</span><span class="sxs-lookup"><span data-stu-id="ee55f-200">hello good news is that you enable and configure Automated Backup in hello same way.</span></span> <span data-ttu-id="ee55f-201">Bu bilgi Hello sonraki bölüme bakın.</span><span class="sxs-lookup"><span data-stu-id="ee55f-201">See hello next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="ee55f-202">Hemen bir değişiklik yaptıktan sonra hello ayarlarını denetleyin, hello eski yapılandırma değerlerini geri alırsınız mümkündür.</span><span class="sxs-lookup"><span data-stu-id="ee55f-202">If you check hello settings immediately after making a change, it is possible that you will get back hello old configuration values.</span></span> <span data-ttu-id="ee55f-203">Birkaç dakika bekleyin ve hello ayarlarını kontrol edin yeniden değişikliklerinizi uygulandığından emin toomake.</span><span class="sxs-lookup"><span data-stu-id="ee55f-203">Wait a few minutes and check hello settings again toomake sure that your changes were applied.</span></span>

### <a name="configure-automated-backup"></a><span data-ttu-id="ee55f-204">Otomatik yedeklemeyi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="ee55f-204">Configure Automated Backup</span></span>
<span data-ttu-id="ee55f-205">Toomodify yanı sıra PowerShell tooenable otomatik yedekleme yapılandırması ve davranış herhangi bir zamanda kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee55f-205">You can use PowerShell tooenable Automated Backup as well as toomodify its configuration and behavior at any time.</span></span>

<span data-ttu-id="ee55f-206">İlk olarak, seçin veya yedekleme dosyalarını hello için bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ee55f-206">First, select or create a storage account for hello backup files.</span></span> <span data-ttu-id="ee55f-207">Merhaba aşağıdaki komut dosyasını bir depolama hesabı seçer veya henüz yoksa oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ee55f-207">hello following script selects a storage account or creates it if it does not exist.</span></span>

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
> <span data-ttu-id="ee55f-208">Otomatik yedekleme premium depolama alanına depolanmasını yedeklemeleri desteklemez, ancak Premium depolama kullanan VM diskleri yedeklemelerden alabilir.</span><span class="sxs-lookup"><span data-stu-id="ee55f-208">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="ee55f-209">Merhaba kullanmak **yeni AzureRmVMSqlServerAutoBackupConfig** komut tooenable ve hello otomatik yedekleme ayarlarını toostore yedeklemeler hello Azure depolama hesabı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ee55f-209">Then use hello **New-AzureRmVMSqlServerAutoBackupConfig** command tooenable and configure hello Automated Backup settings toostore backups in hello Azure storage account.</span></span> <span data-ttu-id="ee55f-210">Bu örnekte, 10 gün boyunca tutulur toobe hello yedeklemeleri ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="ee55f-210">In this example, hello backups are set toobe retained for 10 days.</span></span> <span data-ttu-id="ee55f-211">Merhaba ikinci komut, **kümesi AzureRmVMSqlServerExtension**, güncelleştirmelerinin hello Azure VM bu ayarlarla belirtilen.</span><span class="sxs-lookup"><span data-stu-id="ee55f-211">hello second command, **Set-AzureRmVMSqlServerExtension**, updates hello specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="ee55f-212">Birkaç dakika tooinstall alın ve hello SQL Server Iaas Aracısı Yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="ee55f-212">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="ee55f-213">Diğer ayarları için **yeni AzureRmVMSqlServerAutoBackupConfig** yalnızca tooSQL Server 2016 ve otomatik yedekleme v2 geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="ee55f-213">There are other settings for **New-AzureRmVMSqlServerAutoBackupConfig** that apply only tooSQL Server 2016 and Automated Backup v2.</span></span> <span data-ttu-id="ee55f-214">SQL Server 2014 hello ayarları aşağıdaki desteklemiyor: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**,  **FullBackupStartHour**, **FullBackupWindowInHours**, ve **LogBackupFrequencyInMinutes**.</span><span class="sxs-lookup"><span data-stu-id="ee55f-214">SQL Server 2014 does not support hello following settings: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**, **FullBackupStartHour**, **FullBackupWindowInHours**, and **LogBackupFrequencyInMinutes**.</span></span> <span data-ttu-id="ee55f-215">Bu ayarları bir SQL Server 2014 sanal makinede tooconfigure çalışırsanız, bir hata, ancak hello ayarları uygulanmamış.</span><span class="sxs-lookup"><span data-stu-id="ee55f-215">If you attempt tooconfigure these settings on a SQL Server 2014 virtual machine, there is no error, but hello settings do not get applied.</span></span> <span data-ttu-id="ee55f-216">Bu ayarları bir SQL Server 2016 sanal makinede toouse istiyorsanız, bkz: [otomatik yedekleme v2 SQL Server 2016 Azure Virtual Machines için](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="ee55f-216">If you want toouse these settings on a SQL Server 2016 virtual machine, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="ee55f-217">tooenable şifreleme hello önceki betik toopass hello değiştirme **EnableEncryption** parametresi hello için bir parola (güvenli dize) ile birlikte **CertificatePassword** parametresi.</span><span class="sxs-lookup"><span data-stu-id="ee55f-217">tooenable encryption, modify hello previous script toopass hello **EnableEncryption** parameter along with a password (secure string) for hello **CertificatePassword** parameter.</span></span> <span data-ttu-id="ee55f-218">Merhaba aşağıdaki betiği hello önceki örnekte hello otomatik yedekleme ayarlarını etkinleştirir ve şifreleme ekler.</span><span class="sxs-lookup"><span data-stu-id="ee55f-218">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="ee55f-219">ayarlarınızı uygulanır, tooconfirm [hello otomatik yedekleme yapılandırması doğrulayın](#verifysettings).</span><span class="sxs-lookup"><span data-stu-id="ee55f-219">tooconfirm your settings are applied, [verify hello Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="ee55f-220">Otomatik yedekleme devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="ee55f-220">Disable Automated Backup</span></span>

<span data-ttu-id="ee55f-221">Otomatik yedekleme, hello aynı komut dosyası çalıştırma hello toodisable **-etkinleştirmek** parametresi toohello **yeni AzureRmVMSqlServerAutoBackupConfig** komutu.</span><span class="sxs-lookup"><span data-stu-id="ee55f-221">toodisable Automated Backup, run hello same script without hello **-Enable** parameter toohello **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="ee55f-222">Merhaba hello yokluğu **-etkinleştirmek** parametresi sinyalleri hello komutu toodisable hello özelliği.</span><span class="sxs-lookup"><span data-stu-id="ee55f-222">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span> <span data-ttu-id="ee55f-223">Yüklemesine gibi birkaç dakika toodisable otomatik yedekleme alabilir.</span><span class="sxs-lookup"><span data-stu-id="ee55f-223">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="ee55f-224">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="ee55f-224">Example script</span></span>

<span data-ttu-id="ee55f-225">Merhaba aşağıdaki komut dosyası değişkenleri kümesinin tooenable özelleştirebilir ve VM için otomatik yedeklemeyi yapılandırın sağlar.</span><span class="sxs-lookup"><span data-stu-id="ee55f-225">hello following script provides a set of variables that you can customize tooenable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="ee55f-226">Sizin durumunuzda, gereksinimlerinize göre toocustomize hello komut dosyası gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="ee55f-226">In your case, you might need toocustomize hello script based on your requirements.</span></span> <span data-ttu-id="ee55f-227">Örneğin, sistem veritabanlarının toodisable hello yedekleme istediyseniz toomake değişikliklerinin veya şifrelemeyi etkinleştirmeniz.</span><span class="sxs-lookup"><span data-stu-id="ee55f-227">For example, you would have toomake changes if you wanted toodisable hello backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10

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
    -ResourceGroupName $storage_resourcegroupname

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="ee55f-228">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ee55f-228">Next steps</span></span>

<span data-ttu-id="ee55f-229">Otomatik yedekleme yönetilen yedekleme Azure Vm'lerinde yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="ee55f-229">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="ee55f-230">Çok önemlidir[yönetilen yedekleme hello belgelerini gözden geçirin](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello davranışı ve etkileri.</span><span class="sxs-lookup"><span data-stu-id="ee55f-230">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="ee55f-231">Ek yedekleme bulmak ve izleyen konu hello Azure Vm'lerde SQL Server için kılavuzunda geri yükleyebilirsiniz: [yedekleme ve geri yükleme Azure Virtual Machines'de SQL Server için](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="ee55f-231">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="ee55f-232">Diğer kullanılabilir Otomasyon görevler hakkında daha fazla bilgi için bkz: [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="ee55f-232">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="ee55f-233">Azure Vm'lerinde SQL Server çalıştırma hakkında daha fazla bilgi için bkz: [Azure sanal makinelere genel bakış SQL Server'da](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ee55f-233">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

