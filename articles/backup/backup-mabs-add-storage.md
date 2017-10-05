---
title: "Modern yedekleme depolama ile Azure yedekleme sunucusu v2 kullanın | Microsoft Docs"
description: "Azure yedekleme sunucusu v2'deki yeni özellikler hakkında bilgi edinin. Bu makalede, yedekleme sunucusu yüklemenizi yükseltmek açıklar."
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
ms.openlocfilehash: 751b9b495fd368dff1f72429707f5f33a0ccb569
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="add-storage-to-azure-backup-server-v2"></a><span data-ttu-id="27148-104">Azure yedekleme sunucusu v2 depolama ekleme</span><span class="sxs-lookup"><span data-stu-id="27148-104">Add storage to Azure Backup Server v2</span></span>

<span data-ttu-id="27148-105">Azure yedekleme sunucusu v2 System Center 2016 veri koruma Yöneticisi Modern yedekleme depolama ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="27148-105">Azure Backup Server v2 comes with System Center 2016 Data Protection Manager Modern Backup Storage.</span></span> <span data-ttu-id="27148-106">Modern yedekleme depolama alanı yüzde 50, üç kez daha hızlı ve daha verimli depolama yedeklemeler depolama alanından tasarruf etmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="27148-106">Modern Backup Storage offers storage savings of 50 percent, backups that are three times faster, and more efficient storage.</span></span> <span data-ttu-id="27148-107">Ayrıca, iş yükü algılayan depolama sunar.</span><span class="sxs-lookup"><span data-stu-id="27148-107">It also offers workload-aware storage.</span></span> 

> [!NOTE]
> <span data-ttu-id="27148-108">Modern yedekleme depolama kullanmak için Windows Server 2016 yedekleme sunucusu v2 çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="27148-108">To use Modern Backup Storage, you must run Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="27148-109">Windows Server'ın önceki bir sürümünü yedekleme sunucusu v2 çalıştırırsanız, Azure yedekleme sunucusu Modern yedekleme depolama yararlanamaz.</span><span class="sxs-lookup"><span data-stu-id="27148-109">If you run Backup Server v2 on an earlier version of Windows Server, Azure Backup Server can't take advantage of Modern Backup Storage.</span></span> <span data-ttu-id="27148-110">Bunun yerine, yedekleme sunucusu v1 ile yaptığı gibi iş yüklerini korur.</span><span class="sxs-lookup"><span data-stu-id="27148-110">Instead, it protects workloads as it does with Backup Server v1.</span></span> <span data-ttu-id="27148-111">Daha fazla bilgi için bkz: yedekleme sunucu sürümü [koruma matris](backup-mabs-protection-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="27148-111">For more information, see the Backup Server version [protection matrix](backup-mabs-protection-matrix.md).</span></span>

## <a name="volumes-in-backup-server-v2"></a><span data-ttu-id="27148-112">Yedek sunucu v2 birimleri</span><span class="sxs-lookup"><span data-stu-id="27148-112">Volumes in Backup Server v2</span></span>

<span data-ttu-id="27148-113">Yedek sunucu v2 depolama birimleri kabul eder.</span><span class="sxs-lookup"><span data-stu-id="27148-113">Backup Server v2 accepts storage volumes.</span></span> <span data-ttu-id="27148-114">Bir birim eklediğinizde, yedekleme sunucusu dayanıklı dosya Modern yedekleme depolama gerektiren sistemi (ReFS) birimine biçimlendirir.</span><span class="sxs-lookup"><span data-stu-id="27148-114">When you add a volume, Backup Server formats the volume to Resilient File System (ReFS), which Modern Backup Storage requires.</span></span> <span data-ttu-id="27148-115">Bir birim eklemek ve gerekirse daha sonra genişletmek için bu iş akışı kullanmanızı öneririz:</span><span class="sxs-lookup"><span data-stu-id="27148-115">To add a volume, and to expand it later if you need to, we suggest that you use this workflow:</span></span>

1.  <span data-ttu-id="27148-116">Bir VM üzerinde yedekleme sunucusu v2 ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="27148-116">Set up Backup Server v2 on a VM.</span></span>
2.  <span data-ttu-id="27148-117">Bir depolama havuzunda bir sanal disk üzerinde bir birim oluşturun:</span><span class="sxs-lookup"><span data-stu-id="27148-117">Create a volume on a virtual disk in a storage pool:</span></span>
    1.  <span data-ttu-id="27148-118">Bir depolama havuzuna bir disk ekleyin ve Basit Düzen sanal diski oluşturun.</span><span class="sxs-lookup"><span data-stu-id="27148-118">Add a disk to a storage pool and create a virtual disk with simple layout.</span></span>
    2.  <span data-ttu-id="27148-119">Tüm ek disk ekleyin ve sanal diski genişletme.</span><span class="sxs-lookup"><span data-stu-id="27148-119">Add any additional disks, and extend the virtual disk.</span></span>
    3.  <span data-ttu-id="27148-120">Birim üzerindeki sanal diski oluşturun.</span><span class="sxs-lookup"><span data-stu-id="27148-120">Create volumes on the virtual disk.</span></span>
3.  <span data-ttu-id="27148-121">Birimleri yedekleme sunucusuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="27148-121">Add the volumes to Backup Server.</span></span>
4.  <span data-ttu-id="27148-122">İş yükü algılayan depolama yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="27148-122">Configure workload-aware storage.</span></span>

## <a name="create-a-volume-for-modern-backup-storage"></a><span data-ttu-id="27148-123">Modern yedekleme depolama bir birim oluşturun</span><span class="sxs-lookup"><span data-stu-id="27148-123">Create a volume for Modern Backup Storage</span></span>

<span data-ttu-id="27148-124">Yedekleme sunucusu v2 birimlerle kullanarak disk depolaması, depolama üzerinde denetim tutmanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="27148-124">Using Backup Server v2 with volumes as disk storage can help you maintain control over storage.</span></span> <span data-ttu-id="27148-125">Bir birim, tek bir disk olabilir.</span><span class="sxs-lookup"><span data-stu-id="27148-125">A volume can be a single disk.</span></span> <span data-ttu-id="27148-126">Ancak, depolama gelecekte genişletmek istiyorsanız, depolama alanları kullanılarak oluşturulan bir disk dışında bir birim oluşturun.</span><span class="sxs-lookup"><span data-stu-id="27148-126">However, if you want to extend storage in the future, create a volume out of a disk created by using storage spaces.</span></span> <span data-ttu-id="27148-127">Yedekleme depolama birimi genişletmek istiyorsanız, bu yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="27148-127">This can help if you want to expand the volume for backup storage.</span></span> <span data-ttu-id="27148-128">Bu bölümde, bu kurulum ile bir birim oluşturmak için en iyi yöntemler sunar.</span><span class="sxs-lookup"><span data-stu-id="27148-128">This section offers best practices for creating a volume with this setup.</span></span>

1. <span data-ttu-id="27148-129">Sunucu Yöneticisi'nde seçin **dosya ve depolama hizmetleri** > **birimleri** > **depolama havuzları**.</span><span class="sxs-lookup"><span data-stu-id="27148-129">In Server Manager, select **File and Storage Services** > **Volumes** > **Storage Pools**.</span></span> <span data-ttu-id="27148-130">Altında **FİZİKSEL DİSKLER**seçin **yeni depolama havuzu**.</span><span class="sxs-lookup"><span data-stu-id="27148-130">Under **PHYSICAL DISKS**, select **New Storage Pool**.</span></span> 

    ![Yeni bir depolama havuzu oluşturma](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. <span data-ttu-id="27148-132">İçinde **görevleri** açılan kutusunda **Yeni Sanal Disk**.</span><span class="sxs-lookup"><span data-stu-id="27148-132">In the **TASKS** drop-down box, select **New Virtual Disk**.</span></span>

    ![Sanal disk ekleme](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. <span data-ttu-id="27148-134">Depolama havuzunu seçin ve ardından **Fiziksel Disk Ekle**.</span><span class="sxs-lookup"><span data-stu-id="27148-134">Select the storage pool, and then select **Add Physical Disk**.</span></span>

    ![Fiziksel disk ekleme](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. <span data-ttu-id="27148-136">Fiziksel diski seçin ve ardından **sanal diski Genişlet**.</span><span class="sxs-lookup"><span data-stu-id="27148-136">Select the physical disk, and then select **Extend Virtual Disk**.</span></span>

    ![Sanal diski Genişlet](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. <span data-ttu-id="27148-138">Sanal diski seçin ve ardından **yeni birim**.</span><span class="sxs-lookup"><span data-stu-id="27148-138">Select the virtual disk, and then select **New Volume**.</span></span>

    ![Yeni bir birim oluşturun](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. <span data-ttu-id="27148-140">İçinde **sunucu ve disk seçin** iletişim, sunucusu ve yeni diski seçin.</span><span class="sxs-lookup"><span data-stu-id="27148-140">In the **Select the server and disk** dialog, select the server and the new disk.</span></span> <span data-ttu-id="27148-141">Ardından, seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="27148-141">Then, select **Next**.</span></span>

    ![Sunucu ve disk seçin](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-to-backup-server-disk-storage"></a><span data-ttu-id="27148-143">Birimleri yedekleme sunucusu disk depolama alanına ekleme</span><span class="sxs-lookup"><span data-stu-id="27148-143">Add volumes to Backup Server disk storage</span></span>

<span data-ttu-id="27148-144">Bir birim yedekleme sunucusuna eklemek için **Yönetim** bölmesinde, depolama birimini yeniden tarayın ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="27148-144">To add a volume to Backup Server, in the **Management** pane, rescan the storage, and then select **Add**.</span></span> <span data-ttu-id="27148-145">Yedekleme sunucusu depolama alanına eklemek kullanılabilir tüm birimleri listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="27148-145">A list of all the volumes available to be added for Backup Server Storage appears.</span></span> <span data-ttu-id="27148-146">Kullanılabilir birimleri, seçilen birimleri listesine eklendikten sonra bunları yönetmenize yardımcı olmak için bir kolay ad verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27148-146">After available volumes are added to the list of selected volumes, you can give them a friendly name to help you manage them.</span></span> <span data-ttu-id="27148-147">Yedekleme sunucusu Modern yedekleme depolama yararları kullanabilmek için bu birimleri ReFS için biçimlendirmek için **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="27148-147">To format these volumes to ReFS so Backup Server can use the benefits of Modern Backup Storage, select **OK**.</span></span>

![Kullanılabilir birimleri ekleyin](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a><span data-ttu-id="27148-149">İş yükü algılayan depolama alanı ayarlama</span><span class="sxs-lookup"><span data-stu-id="27148-149">Set up workload-aware storage</span></span>

<span data-ttu-id="27148-150">İş yükü uyumlu depolama ile tercihen belirli türdeki iş yüklerini depolayan birimleri seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27148-150">With workload-aware storage, you can select the volumes that preferentially store certain kinds of workloads.</span></span> <span data-ttu-id="27148-151">Örneğin, sık kullanılan, yüksek hacimli yedeklemeler gerektiren iş yüklerini depolamak için çok sayıda giriş/çıkış işlemi (IOPS) saniyede destekleyen pahalı birimler ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27148-151">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) to store only the workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="27148-152">SQL Server ile işlem günlükleri örneğidir.</span><span class="sxs-lookup"><span data-stu-id="27148-152">An example is SQL Server with transaction logs.</span></span> <span data-ttu-id="27148-153">Sanal makineleri gibi daha az sıklıkta yedeklenen diğer iş yükleri için düşük maliyetli birimler yedeklenebilir.</span><span class="sxs-lookup"><span data-stu-id="27148-153">Other workloads that are backed up less frequently, like VMs, can be backed up to low-cost volumes.</span></span>

### <a name="update-dpmdiskstorage"></a><span data-ttu-id="27148-154">Güncelleştirme DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="27148-154">Update-DPMDiskStorage</span></span>

<span data-ttu-id="27148-155">Data Protection Manager sunucusundaki depolama havuzunda birim özelliklerini güncelleştiren güncelleştirme-DPMDiskStorage PowerShell cmdlet'ini kullanarak, iş yükü algılayan depolama alanı ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27148-155">You can set up workload-aware storage by using the PowerShell cmdlet Update-DPMDiskStorage, which updates the properties of a volume in the storage pool on a Data Protection Manager server.</span></span>

<span data-ttu-id="27148-156">Sözdizimi:</span><span class="sxs-lookup"><span data-stu-id="27148-156">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
<span data-ttu-id="27148-157">Aşağıdaki ekran görüntüsünde PowerShell penceresinde güncelleştirme DPMDiskStorage cmdlet'i gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="27148-157">The following screenshot shows the Update-DPMDiskStorage cmdlet in the PowerShell window.</span></span>

![PowerShell penceresinde güncelleştirme DPMDiskStorage komutu](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

<span data-ttu-id="27148-159">PowerShell kullanarak yaptığınız değişiklikler yedekleme sunucu Yönetici konsolunda yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="27148-159">The changes you make by using PowerShell are reflected in the Backup Server Administrator Console.</span></span>

![Diskleri ve birimleri Yönetici konsolunda](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a><span data-ttu-id="27148-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="27148-161">Next steps</span></span>
<span data-ttu-id="27148-162">Yedekleme sunucusu yükledikten sonra sunucunuzu hazırlama ya da bir iş yükü korumaya başlamak öğrenin.</span><span class="sxs-lookup"><span data-stu-id="27148-162">After you install Backup Server, learn how to prepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="27148-163">Yedekleme sunucusu iş yükleri hazırlama</span><span class="sxs-lookup"><span data-stu-id="27148-163">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="27148-164">VMware sunucusunu yedeklemek için yedekleme sunucusu kullanın</span><span class="sxs-lookup"><span data-stu-id="27148-164">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="27148-165">SQL Server için yedekleme sunucusu kullanın</span><span class="sxs-lookup"><span data-stu-id="27148-165">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)

