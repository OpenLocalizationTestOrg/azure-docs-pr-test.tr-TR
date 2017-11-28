---
title: Azure yedekleme sunucusu v2 ile Modern yedekleme depolama aaaUse | Microsoft Docs
description: "Azure yedekleme sunucusu v2 hello yeni özellikler hakkında bilgi edinin. Bu makalede nasıl tooupgrade yedekleme sunucusu yüklemenizi."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: b2a1ed27a6a682bd611fea1d2df9ef93314404e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-storage-tooazure-backup-server-v2"></a><span data-ttu-id="c8565-104">Depolama tooAzure yedekleme sunucusu v2 ekleme</span><span class="sxs-lookup"><span data-stu-id="c8565-104">Add storage tooAzure Backup Server v2</span></span>

<span data-ttu-id="c8565-105">Azure yedekleme sunucusu v2 System Center 2016 veri koruma Yöneticisi Modern yedekleme depolama ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="c8565-105">Azure Backup Server v2 comes with System Center 2016 Data Protection Manager Modern Backup Storage.</span></span> <span data-ttu-id="c8565-106">Modern yedekleme depolama alanı yüzde 50, üç kez daha hızlı ve daha verimli depolama yedeklemeler depolama alanından tasarruf etmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="c8565-106">Modern Backup Storage offers storage savings of 50 percent, backups that are three times faster, and more efficient storage.</span></span> <span data-ttu-id="c8565-107">Ayrıca, iş yükü algılayan depolama sunar.</span><span class="sxs-lookup"><span data-stu-id="c8565-107">It also offers workload-aware storage.</span></span> 

> [!NOTE]
> <span data-ttu-id="c8565-108">toouse Modern yedekleme depolama, Windows Server 2016 yedekleme sunucusu v2 çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8565-108">toouse Modern Backup Storage, you must run Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="c8565-109">Windows Server'ın önceki bir sürümünü yedekleme sunucusu v2 çalıştırırsanız, Azure yedekleme sunucusu Modern yedekleme depolama yararlanamaz.</span><span class="sxs-lookup"><span data-stu-id="c8565-109">If you run Backup Server v2 on an earlier version of Windows Server, Azure Backup Server can't take advantage of Modern Backup Storage.</span></span> <span data-ttu-id="c8565-110">Bunun yerine, yedekleme sunucusu v1 ile yaptığı gibi iş yüklerini korur.</span><span class="sxs-lookup"><span data-stu-id="c8565-110">Instead, it protects workloads as it does with Backup Server v1.</span></span> <span data-ttu-id="c8565-111">Merhaba yedekleme sunucusu sürümü daha fazla bilgi için bkz: [koruma matris](backup-mabs-protection-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="c8565-111">For more information, see hello Backup Server version [protection matrix](backup-mabs-protection-matrix.md).</span></span>

## <a name="volumes-in-backup-server-v2"></a><span data-ttu-id="c8565-112">Yedek sunucu v2 birimleri</span><span class="sxs-lookup"><span data-stu-id="c8565-112">Volumes in Backup Server v2</span></span>

<span data-ttu-id="c8565-113">Yedek sunucu v2 depolama birimleri kabul eder.</span><span class="sxs-lookup"><span data-stu-id="c8565-113">Backup Server v2 accepts storage volumes.</span></span> <span data-ttu-id="c8565-114">Bir birim eklediğinizde, yedekleme sunucusu hello birim tooResilient dosya Modern yedekleme depolama gerektiren sistemi (ReFS) biçimlendirir.</span><span class="sxs-lookup"><span data-stu-id="c8565-114">When you add a volume, Backup Server formats hello volume tooResilient File System (ReFS), which Modern Backup Storage requires.</span></span> <span data-ttu-id="c8565-115">tooadd bir birim ve tooexpand daha sonra gerekirse, bu iş akışı kullanmanızı öneririz:</span><span class="sxs-lookup"><span data-stu-id="c8565-115">tooadd a volume, and tooexpand it later if you need to, we suggest that you use this workflow:</span></span>

1.  <span data-ttu-id="c8565-116">Bir VM üzerinde yedekleme sunucusu v2 ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c8565-116">Set up Backup Server v2 on a VM.</span></span>
2.  <span data-ttu-id="c8565-117">Bir depolama havuzunda bir sanal disk üzerinde bir birim oluşturun:</span><span class="sxs-lookup"><span data-stu-id="c8565-117">Create a volume on a virtual disk in a storage pool:</span></span>
    1.  <span data-ttu-id="c8565-118">Bir disk tooa depolama havuzunu ekleyin ve Basit Düzen sanal disk oluşturma.</span><span class="sxs-lookup"><span data-stu-id="c8565-118">Add a disk tooa storage pool and create a virtual disk with simple layout.</span></span>
    2.  <span data-ttu-id="c8565-119">Ek bir disk ekleyin ve hello sanal diski genişletme.</span><span class="sxs-lookup"><span data-stu-id="c8565-119">Add any additional disks, and extend hello virtual disk.</span></span>
    3.  <span data-ttu-id="c8565-120">Birim üzerindeki hello sanal diski oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c8565-120">Create volumes on hello virtual disk.</span></span>
3.  <span data-ttu-id="c8565-121">Merhaba birimleri tooBackup sunucu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c8565-121">Add hello volumes tooBackup Server.</span></span>
4.  <span data-ttu-id="c8565-122">İş yükü algılayan depolama yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c8565-122">Configure workload-aware storage.</span></span>

## <a name="create-a-volume-for-modern-backup-storage"></a><span data-ttu-id="c8565-123">Modern yedekleme depolama bir birim oluşturun</span><span class="sxs-lookup"><span data-stu-id="c8565-123">Create a volume for Modern Backup Storage</span></span>

<span data-ttu-id="c8565-124">Yedekleme sunucusu v2 birimlerle kullanarak disk depolaması, depolama üzerinde denetim tutmanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="c8565-124">Using Backup Server v2 with volumes as disk storage can help you maintain control over storage.</span></span> <span data-ttu-id="c8565-125">Bir birim, tek bir disk olabilir.</span><span class="sxs-lookup"><span data-stu-id="c8565-125">A volume can be a single disk.</span></span> <span data-ttu-id="c8565-126">Ancak, hello tooextend depolama gelecekteki istiyorsanız, depolama alanları kullanılarak oluşturulan bir disk dışında bir birim oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c8565-126">However, if you want tooextend storage in hello future, create a volume out of a disk created by using storage spaces.</span></span> <span data-ttu-id="c8565-127">Yedekleme depolaması için tooexpand hello birim istiyorsanız bu yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="c8565-127">This can help if you want tooexpand hello volume for backup storage.</span></span> <span data-ttu-id="c8565-128">Bu bölümde, bu kurulum ile bir birim oluşturmak için en iyi yöntemler sunar.</span><span class="sxs-lookup"><span data-stu-id="c8565-128">This section offers best practices for creating a volume with this setup.</span></span>

1. <span data-ttu-id="c8565-129">Sunucu Yöneticisi'nde seçin **dosya ve depolama hizmetleri** > **birimleri** > **depolama havuzları**.</span><span class="sxs-lookup"><span data-stu-id="c8565-129">In Server Manager, select **File and Storage Services** > **Volumes** > **Storage Pools**.</span></span> <span data-ttu-id="c8565-130">Altında **FİZİKSEL DİSKLER**seçin **yeni depolama havuzu**.</span><span class="sxs-lookup"><span data-stu-id="c8565-130">Under **PHYSICAL DISKS**, select **New Storage Pool**.</span></span> 

    ![Yeni bir depolama havuzu oluşturma](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. <span data-ttu-id="c8565-132">Merhaba, **görevleri** açılan kutusunda **Yeni Sanal Disk**.</span><span class="sxs-lookup"><span data-stu-id="c8565-132">In hello **TASKS** drop-down box, select **New Virtual Disk**.</span></span>

    ![Sanal disk ekleme](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. <span data-ttu-id="c8565-134">Merhaba depolama havuzunu seçin ve ardından **Fiziksel Disk Ekle**.</span><span class="sxs-lookup"><span data-stu-id="c8565-134">Select hello storage pool, and then select **Add Physical Disk**.</span></span>

    ![Fiziksel disk ekleme](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. <span data-ttu-id="c8565-136">Merhaba fiziksel diski seçin ve ardından **sanal diski Genişlet**.</span><span class="sxs-lookup"><span data-stu-id="c8565-136">Select hello physical disk, and then select **Extend Virtual Disk**.</span></span>

    ![Merhaba sanal diski Genişlet](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. <span data-ttu-id="c8565-138">Merhaba sanal diski seçin ve ardından **yeni birim**.</span><span class="sxs-lookup"><span data-stu-id="c8565-138">Select hello virtual disk, and then select **New Volume**.</span></span>

    ![Yeni bir birim oluşturun](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. <span data-ttu-id="c8565-140">Merhaba, **hello sunucu ve disk seçin** iletişim, select hello sunucu ve hello yeni disk.</span><span class="sxs-lookup"><span data-stu-id="c8565-140">In hello **Select hello server and disk** dialog, select hello server and hello new disk.</span></span> <span data-ttu-id="c8565-141">Ardından, seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="c8565-141">Then, select **Next**.</span></span>

    ![Merhaba sunucu ve disk seçin](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-toobackup-server-disk-storage"></a><span data-ttu-id="c8565-143">Birimleri tooBackup Server disk depolama ekleme</span><span class="sxs-lookup"><span data-stu-id="c8565-143">Add volumes tooBackup Server disk storage</span></span>

<span data-ttu-id="c8565-144">tooadd hello bir birim tooBackup sunucu **Yönetim** bölmesinde hello depolama yeniden tarayın ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="c8565-144">tooadd a volume tooBackup Server, in hello **Management** pane, rescan hello storage, and then select **Add**.</span></span> <span data-ttu-id="c8565-145">Tüm hello birimler kullanılabilir toobe yedekleme sunucusu depolama alanına eklenen listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c8565-145">A list of all hello volumes available toobe added for Backup Server Storage appears.</span></span> <span data-ttu-id="c8565-146">Kullanılabilir birimleri toohello seçili birimlerin listesini eklendikten sonra bunları yönetmek bir kolay ad toohelp verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8565-146">After available volumes are added toohello list of selected volumes, you can give them a friendly name toohelp you manage them.</span></span> <span data-ttu-id="c8565-147">Yedekleme sunucusu Modern yedekleme depolama hello yararları kullanabilmek için bu birimleri tooReFS seçin tooformat **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="c8565-147">tooformat these volumes tooReFS so Backup Server can use hello benefits of Modern Backup Storage, select **OK**.</span></span>

![Kullanılabilir birimleri ekleyin](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a><span data-ttu-id="c8565-149">İş yükü algılayan depolama alanı ayarlama</span><span class="sxs-lookup"><span data-stu-id="c8565-149">Set up workload-aware storage</span></span>

<span data-ttu-id="c8565-150">İş yükü uyumlu depolama ile tercihen belirli türdeki iş yüklerini depolama hello birimleri seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8565-150">With workload-aware storage, you can select hello volumes that preferentially store certain kinds of workloads.</span></span> <span data-ttu-id="c8565-151">Örneğin, çok sayıda sık, yüksek hacimli yedeklemeler gerektiren ikinci (IOPS) toostore yalnızca hello iş yükleri başına girdi/çıktı işlemleri destekleyen pahalı birimler ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8565-151">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) toostore only hello workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="c8565-152">SQL Server ile işlem günlükleri örneğidir.</span><span class="sxs-lookup"><span data-stu-id="c8565-152">An example is SQL Server with transaction logs.</span></span> <span data-ttu-id="c8565-153">Toolow maliyetli birimleri VM'ler gibi daha az sıklıkta yedeklenen diğer iş yükleri yedeklenebilir.</span><span class="sxs-lookup"><span data-stu-id="c8565-153">Other workloads that are backed up less frequently, like VMs, can be backed up toolow-cost volumes.</span></span>

### <a name="update-dpmdiskstorage"></a><span data-ttu-id="c8565-154">Güncelleştirme DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="c8565-154">Update-DPMDiskStorage</span></span>

<span data-ttu-id="c8565-155">Data Protection Manager sunucusunda hello depolama havuzundaki bir birimin hello özelliklerini güncelleştiren güncelleştirme-DPMDiskStorage hello PowerShell cmdlet'ini kullanarak iş yükü algılayan depolama alanı ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8565-155">You can set up workload-aware storage by using hello PowerShell cmdlet Update-DPMDiskStorage, which updates hello properties of a volume in hello storage pool on a Data Protection Manager server.</span></span>

<span data-ttu-id="c8565-156">Sözdizimi:</span><span class="sxs-lookup"><span data-stu-id="c8565-156">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
<span data-ttu-id="c8565-157">Merhaba aşağıdaki ekran görüntüsü hello güncelleştirme DPMDiskStorage cmdlet hello PowerShell penceresinde gösterir.</span><span class="sxs-lookup"><span data-stu-id="c8565-157">hello following screenshot shows hello Update-DPMDiskStorage cmdlet in hello PowerShell window.</span></span>

![Merhaba hello PowerShell penceresinde güncelleştirme DPMDiskStorage komutu](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

<span data-ttu-id="c8565-159">PowerShell kullanarak yaptığınız hello değişiklikler hello yedekleme Sunucu Yöneticisi konsolu yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="c8565-159">hello changes you make by using PowerShell are reflected in hello Backup Server Administrator Console.</span></span>

![Diskleri ve birimleri hello Yönetici Konsolu](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a><span data-ttu-id="c8565-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c8565-161">Next steps</span></span>
<span data-ttu-id="c8565-162">Yedekleme sunucusu yükledikten sonra bilgi nasıl tooprepare sunucunuz veya bir iş yükü korumaya başlamak.</span><span class="sxs-lookup"><span data-stu-id="c8565-162">After you install Backup Server, learn how tooprepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="c8565-163">Yedekleme sunucusu iş yükleri hazırlama</span><span class="sxs-lookup"><span data-stu-id="c8565-163">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="c8565-164">Bir VMware sunucusu yedekleme sunucusu tooback kullanın</span><span class="sxs-lookup"><span data-stu-id="c8565-164">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="c8565-165">SQL Server Yedekleme Sunucusu tooback kullanın</span><span class="sxs-lookup"><span data-stu-id="c8565-165">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)

