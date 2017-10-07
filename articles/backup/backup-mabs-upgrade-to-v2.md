---
title: Azure yedekleme sunucusu v2 aaaInstall | Microsoft Docs
description: "Azure yedekleme sunucusu v2, VM'ler, dosyalar ve klasörler, iş yükleri ve daha fazla korunması için geliştirilmiş yedekleme özellikleri sunar. Bilgi nasıl tooinstall veya yükseltme tooAzure yedekleme sunucusu v2."
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
ms.openlocfilehash: 5b1699dadd3a173f1c0ef91a1a600bc5e12f20ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-azure-backup-server-v2"></a><span data-ttu-id="8b9e0-104">Azure Backup sunucusu v2 yükleyin</span><span class="sxs-lookup"><span data-stu-id="8b9e0-104">Install Azure Backup Server v2</span></span>

<span data-ttu-id="8b9e0-105">Azure yedekleme sunucusu sanal makineleri (VM'ler), iş yükleri, dosyaları ve klasörleri ve daha fazla korunmasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-105">Azure Backup Server helps protect your virtual machines (VMs), workloads, files and folders, and more.</span></span> <span data-ttu-id="8b9e0-106">Azure yedekleme sunucusu v2 üzerinde Azure yedekleme sunucusu v1 oluşturur ve v1 kullanılabilir değil yeni özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-106">Azure Backup Server v2 builds on Azure Backup Server v1, and gives you new features that are not available in v1.</span></span> <span data-ttu-id="8b9e0-107">Özellikler v1 ve v2 arasındaki karşılaştırması için bkz: [Azure yedekleme sunucusu koruma matris](backup-mabs-protection-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="8b9e0-107">For a comparison of features between v1 and v2, see [Azure Backup Server protection matrix](backup-mabs-protection-matrix.md).</span></span> 

<span data-ttu-id="8b9e0-108">Merhaba ek yedekleme sunucusu v2 olarak yedekleme sunucusu v1'den yükseltme özellikleridir.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-108">hello additional features in Backup Server v2 are an upgrade from Backup Server v1.</span></span> <span data-ttu-id="8b9e0-109">Ancak, yedekleme sunucusu v1 yedekleme sunucusu v2 yüklemek için bir önkoşul değil.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-109">However, Backup Server v1 is not a prerequisite for installing Backup Server v2.</span></span> <span data-ttu-id="8b9e0-110">Yedekleme sunucusu v1 tooBackup sunucu v2'den tooupgrade istiyorsanız, yedekleme sunucusu v2 hello yedekleme sunucusu koruma sunucusuna yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-110">If you want tooupgrade from Backup Server v1 tooBackup Server v2, install Backup Server v2 on hello Backup Server protection server.</span></span> <span data-ttu-id="8b9e0-111">Var olan yedekleme sunucusu ayarlarınızı değişmeden kalır.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-111">Your existing Backup Server settings remain intact.</span></span>

<span data-ttu-id="8b9e0-112">Windows Server 2012 R2 veya Windows Server 2016 yedekleme sunucusu v2 yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-112">You can install Backup Server v2 on Windows Server 2012 R2 or Windows Server 2016.</span></span> <span data-ttu-id="8b9e0-113">yeni özelliklerden tootake ister System Center 2016 veri koruma Yöneticisi Modern yedekleme depolama, Windows Server 2016 yedekleme sunucusu v2 yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-113">tootake advantage of new features like System Center 2016 Data Protection Manager Modern Backup Storage, you must install Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="8b9e0-114">Tooor yükleme yedekleme sunucusu v2 yükseltmeden önce hello hakkında okuyun [yükleme önkoşulları](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="8b9e0-114">Before you upgrade tooor install Backup Server v2, read about hello [installation prerequisites](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span></span>

> [!NOTE]
> <span data-ttu-id="8b9e0-115">Azure yedekleme sunucusu hello sahip System Center Data Protection Manager olarak temel aynı kodu.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-115">Azure Backup Server has hello same code base as System Center Data Protection Manager.</span></span> <span data-ttu-id="8b9e0-116">Yedek sunucu v1 eşdeğer tooData Protection Manager 2012 R2 ve yedekleme sunucusu v2 eşdeğer tooData Protection Manager 2016 şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-116">Backup Server v1 is equivalent tooData Protection Manager 2012 R2, and Backup Server v2 is equivalent tooData Protection Manager 2016.</span></span> <span data-ttu-id="8b9e0-117">Bu makalede, bazen hello Data Protection Manager belge başvurur.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-117">This article occasionally references hello Data Protection Manager documentation.</span></span>
>
>

## <a name="upgrade-backup-server-toov2"></a><span data-ttu-id="8b9e0-118">Yedekleme sunucusu toov2 yükseltme</span><span class="sxs-lookup"><span data-stu-id="8b9e0-118">Upgrade Backup Server toov2</span></span>
<span data-ttu-id="8b9e0-119">Yedekleme sunucusu v1 tooBackup sunucu v2'den tooupgrade hello gerekli güncelleştirmeleri yüklemenizi sahip olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="8b9e0-119">tooupgrade from Backup Server v1 tooBackup Server v2, make sure your installation has hello required updates:</span></span>

- <span data-ttu-id="8b9e0-120">[Merhaba koruma aracılarını güncelleştirme](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) üzerinde hello korumalı sunucuları.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-120">[Update hello protection agents](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) on hello protected servers.</span></span>
- <span data-ttu-id="8b9e0-121">Windows Server 2012 R2 tooWindows Server 2016 yükseltin.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-121">Upgrade Windows Server 2012 R2 tooWindows Server 2016.</span></span>
- <span data-ttu-id="8b9e0-122">Azure yedekleme sunucusu uzak yönetici tüm üretim sunucularında yükseltin.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-122">Upgrade Azure Backup Server Remote Administrator on all production servers.</span></span>
- <span data-ttu-id="8b9e0-123">Üretim sunucunuzu yeniden başlatmanıza gerek kalmadan yedeklemeleri toocontinue ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-123">Ensure that backups are set toocontinue without restarting your production server.</span></span>


### <a name="upgrade-steps-for-backup-server-v2"></a><span data-ttu-id="8b9e0-124">Yedekleme sunucusu v2 yükseltme adımları</span><span class="sxs-lookup"><span data-stu-id="8b9e0-124">Upgrade steps for Backup Server v2</span></span>

1. <span data-ttu-id="8b9e0-125">Merhaba İndirme Merkezi olarak [hello yükseltme yükleyici indirmek](https://go.microsoft.com/fwlink/?LinkId=626082).</span><span class="sxs-lookup"><span data-stu-id="8b9e0-125">In hello Download Center, [download hello upgrade installer](https://go.microsoft.com/fwlink/?LinkId=626082).</span></span>

2. <span data-ttu-id="8b9e0-126">Merhaba Kurulum Sihirbazı'nı ayıkladıktan sonra olduğundan emin olun **setup.exe yürütme** seçili ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-126">After you extract hello setup wizard, make sure that **Execute setup.exe** is selected, and then select **Finish**.</span></span>

  ![Kurulum Yükleyici - Çalıştır kurulum](./media/backup-mabs-upgrade-to-v2/run-setup.png)

3. <span data-ttu-id="8b9e0-128">Merhaba Microsoft Azure Yedekleme Sunucusu Sihirbazı'nda altında **yükleme**seçin **Microsoft Azure yedekleme sunucusu**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-128">In hello Microsoft Azure Backup Server wizard, under **Install**, select **Microsoft Azure Backup Server**.</span></span>

  ![Kurulum Yükleyici - Select yükleme](./media/backup-mabs-upgrade-to-v2/mabs-installer-s1.png)

4. <span data-ttu-id="8b9e0-130">Merhaba üzerinde **Hoş Geldiniz** sayfasında hello uyarılarını gözden geçirin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-130">On hello **Welcome** page, review hello warnings, and then select **Next**.</span></span>

  ![Kurulum Yükleyici - Karşılama sayfası](./media/backup-mabs-upgrade-to-v2/mabs-installer-s2.png)

5. <span data-ttu-id="8b9e0-132">Merhaba Kurulum Sihirbazı'nı önkoşul denetimleri toomake ortamınızı yükseltebilirsiniz emin gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-132">hello setup wizard performs prerequisite checks toomake sure your environment can upgrade.</span></span> <span data-ttu-id="8b9e0-133">Merhaba üzerinde **önkoşul denetler** sayfasında, **denetleyin**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-133">On hello **Prerequisite Checks** page, select **Check**.</span></span>

  ![Kurulum Yükleyici - önkoşul denetler sayfası](./media/backup-mabs-upgrade-to-v2/mabs-installer-s3-perform-checks.png)

6. <span data-ttu-id="8b9e0-135">Ortamınız önkoşul denetimleri hello geçmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-135">Your environment must pass hello prerequisite checks.</span></span> <span data-ttu-id="8b9e0-136">Ortamınızı hello denetimleri geçmiyor hello sorunlara dikkat edin ve düzeltin.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-136">If your environment doesn't pass hello checks, note hello issues and fix them.</span></span> <span data-ttu-id="8b9e0-137">Ardından, seçin **yeniden denetle**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-137">Then, select **Check Again**.</span></span> <span data-ttu-id="8b9e0-138">Merhaba önkoşul denetimlerini geçemedi sonra seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-138">After you pass hello prerequisite checks, select **Next**.</span></span>

  ![Kurulum Yükleyici - yeniden denetle düğmesi](./media/backup-mabs-upgrade-to-v2/mabs-installer-s4-pass-checks.png)

7. <span data-ttu-id="8b9e0-140">Merhaba üzerinde **SQL ayarlarını** sayfasında hello SQL yüklemeniz için ilgili seçeneği seçin ve ardından **denetle ve Yükle**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-140">On hello **SQL Settings** page, select hello relevant option for your SQL installation, and then select **Check and Install**.</span></span>

  ![Kurulum Yükleyici - SQL Ayarları sayfası](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5-sql-settings.png)

  <span data-ttu-id="8b9e0-142">Merhaba denetimleri birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-142">hello checks might take a few minutes.</span></span> <span data-ttu-id="8b9e0-143">Tamamlanan, select hello denetimleri olduğunda **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-143">When hello checks are finished, select **Next**.</span></span>

  ![Kurulum Yükleyici - SQL ayarlarını denetleyin ve Yükle düğmesini](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5a-check-and fix-settings.png)

8. <span data-ttu-id="8b9e0-145">Merhaba üzerinde **yükleme ayarları** sayfasında, yedekleme sunucusu yüklü olduğu herhangi bir değişiklik toohello konumu ya da toohello karalama konumu olun.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-145">On hello **Installation Settings** page, make any changes toohello location where Backup Server is installed, or toohello Scratch Location.</span></span> <span data-ttu-id="8b9e0-146">Seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-146">Select **Next**.</span></span>

  ![Kurulum Yükleyici - yükleme ayarları sayfası](./media/backup-mabs-upgrade-to-v2/mabs-installer-s6-installation-settings.png)

9. <span data-ttu-id="8b9e0-148">toofinish hello Kurulum Sihirbazı'nı seçin **son**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-148">toofinish hello setup wizard, select **Finish**.</span></span>

  ![Kurulum Yükleyici - bitiş](./media/backup-mabs-upgrade-to-v2/run-setup.png)



## <a name="add-storage-for-modern-backup-storage"></a><span data-ttu-id="8b9e0-150">Modern yedekleme depolama için depolama ekleme</span><span class="sxs-lookup"><span data-stu-id="8b9e0-150">Add storage for Modern Backup Storage</span></span>

<span data-ttu-id="8b9e0-151">tooimprove yedekleme depolama verimliliği, yedekleme sunucusuna v2 birimler için destek ekler.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-151">tooimprove backup storage efficiency, Backup Server v2 adds support for volumes.</span></span> <span data-ttu-id="8b9e0-152">Yedekleme sunucusu v1 gibi yedekleme sunucusu v2 diskleri destekler.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-152">Like Backup Server v1, Backup Server v2 supports disks.</span></span>

### <a name="add-volumes-and-disks"></a><span data-ttu-id="8b9e0-153">Birimler ve diskleri ekleme</span><span class="sxs-lookup"><span data-stu-id="8b9e0-153">Add volumes and disks</span></span>
<span data-ttu-id="8b9e0-154">Windows Server 2016 yedekleme sunucusu v2 çalıştırırsanız, birimleri toostore yedekleme verilerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-154">If you run Backup Server v2 on Windows Server 2016, you can use volumes toostore backup data.</span></span> <span data-ttu-id="8b9e0-155">Birimleri depolama alanından tasarruf etmenizi ve daha hızlı yedekleme sunar.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-155">Volumes offer storage savings and faster backups.</span></span> <span data-ttu-id="8b9e0-156">Birimleri yeni tooBackup sunucusu olduğundan, bunları eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-156">Because volumes are new tooBackup Server, you must add them.</span></span> 

<span data-ttu-id="8b9e0-157">Bir birim tooBackup sunucusu eklediğinizde, hello birim kolay bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-157">When you add a volume tooBackup Server, you can give hello volume a friendly name.</span></span> <span data-ttu-id="8b9e0-158">Merhaba tıklatın **kolay ad** sütun hello hacmi tooname istiyor.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-158">Click hello **Friendly Name** column of hello volume you want tooname.</span></span> <span data-ttu-id="8b9e0-159">Gerekirse, hello adı daha sonra değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-159">You can change hello name later, if necessary.</span></span> <span data-ttu-id="8b9e0-160">Ayrıca PowerShell tooadd kullanın veya birimler için kolay adlar değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-160">You also can use PowerShell tooadd or change friendly names for volumes.</span></span>

<span data-ttu-id="8b9e0-161">Merhaba Yönetici Konsolu biriminde tooadd:</span><span class="sxs-lookup"><span data-stu-id="8b9e0-161">tooadd a volume in hello Administrator Console:</span></span>

1. <span data-ttu-id="8b9e0-162">Hello Azure yedekleme Sunucu Yöneticisi konsolu, seçin **Yönetim** > **Disk Depolama** > **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-162">In hello Azure Backup Server Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![Açık hello Disk Depolama Alanı Ekle Sihirbazı](./media//backup-mabs-upgrade-to-v2/open-add-disk-storage-wizard.png)

    <span data-ttu-id="8b9e0-164">Merhaba Disk Depolama Alanı Ekle Sihirbazı açılır.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-164">This opens hello Add Disk Storage wizard.</span></span>

2. <span data-ttu-id="8b9e0-165">Merhaba üzerinde **Disk Depolama Alanı Ekle** sayfasında hello **kullanılabilir birimleri** kutusunda, bir birim seçin ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-165">On hello **Add Disk Storage** page, in hello **Available volumes** box, select a volume, and then select **Add**.</span></span>
3. <span data-ttu-id="8b9e0-166">Merhaba, **seçili birimleri** kutusuna hello birim için kolay bir ad girin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-166">In hello **Selected volumes** box, enter a friendly name for hello volume, and then select **OK**.</span></span>

      ![Disk depolama alanı Ekle Sihirbazı - birim ekleme](./media/backup-mabs-upgrade-to-v2/add-volume.png)

  <span data-ttu-id="8b9e0-168">Tooadd bir disk istiyorsanız hello disk eski depolama olan tooa koruma grubuna ait olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-168">If you want tooadd a disk, hello disk must belong tooa protection group that has legacy storage.</span></span> <span data-ttu-id="8b9e0-169">Bu diskleri yalnızca bu koruma grupları için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-169">These disks can only be used for these protection groups.</span></span> <span data-ttu-id="8b9e0-170">Yedekleme sunucusu eski koruma kaynakları yoksa, hello disk listelenmiyor.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-170">If Backup Server doesn't have sources that have legacy protection, hello disk isn't listed.</span></span>

  <span data-ttu-id="8b9e0-171">Diskleri ekleme hakkında daha fazla bilgi için bkz: [diskleri tooincrease eski depolama ekleme](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span><span class="sxs-lookup"><span data-stu-id="8b9e0-171">For more information about adding disks, see [Adding disks tooincrease legacy storage](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span></span> <span data-ttu-id="8b9e0-172">Kolay bir ad bir disk veremez.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-172">You can't give a disk a friendly name.</span></span>


### <a name="assign-workloads-toovolumes"></a><span data-ttu-id="8b9e0-173">İş yükleri toovolumes atayın</span><span class="sxs-lookup"><span data-stu-id="8b9e0-173">Assign workloads toovolumes</span></span>

<span data-ttu-id="8b9e0-174">Yedekleme Server'da hangi iş yüklerini toowhich birimleri atanan belirtin.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-174">In Backup Server, you specify which workloads are assigned toowhich volumes.</span></span> <span data-ttu-id="8b9e0-175">Örneğin, çok sayıda sık, yüksek hacimli yedeklemeler gerektiren ikinci (IOPS) toostore yalnızca iş yükleri başına girdi/çıktı işlemleri destekleyen pahalı birimler ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-175">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) toostore only workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="8b9e0-176">SQL Server ile işlem günlükleri örneğidir.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-176">An example is SQL Server with transaction logs.</span></span>

#### <a name="update-dpmdiskstorage"></a><span data-ttu-id="8b9e0-177">Güncelleştirme DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="8b9e0-177">Update-DPMDiskStorage</span></span>

<span data-ttu-id="8b9e0-178">Yedekleme sunucusu hello depolama havuzundaki bir birimin tooupdate hello özelliklerini hello PowerShell cmdlet'ini güncelleştirme DPMDiskStorage kullanın.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-178">tooupdate hello properties of a volume in hello storage pool in Backup Server, use hello PowerShell cmdlet Update-DPMDiskStorage.</span></span>

<span data-ttu-id="8b9e0-179">Sözdizimi:</span><span class="sxs-lookup"><span data-stu-id="8b9e0-179">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

<span data-ttu-id="8b9e0-180">PowerShell kullanarak yaptığınız tüm değişiklikler hello UI yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-180">All changes that you make by using PowerShell are reflected in hello UI.</span></span>


## <a name="protect-data-sources"></a><span data-ttu-id="8b9e0-181">Veri kaynaklarını korumak</span><span class="sxs-lookup"><span data-stu-id="8b9e0-181">Protect data sources</span></span>
<span data-ttu-id="8b9e0-182">veri kaynaklarını koruma toobegin, bir koruma grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-182">toobegin protecting data sources, create a protection group.</span></span> <span data-ttu-id="8b9e0-183">adımları Vurgu değişiklikler veya eklemeler toohello yeni koruma grubu Sihirbazı'nı aşağıdaki hello.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-183">hello following steps highlight changes or additions toohello New Protection Group wizard.</span></span>

<span data-ttu-id="8b9e0-184">bir koruma grubu toocreate:</span><span class="sxs-lookup"><span data-stu-id="8b9e0-184">toocreate a protection group:</span></span>

1. <span data-ttu-id="8b9e0-185">Hello yedekleme Sunucu Yöneticisi konsolu, seçin **koruma**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-185">In hello Backup Server Administrator Console, select **Protection**.</span></span>

2. <span data-ttu-id="8b9e0-186">Merhaba araç şeridinde seçin **yeni**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-186">On hello tool ribbon, select **New**.</span></span>

    <span data-ttu-id="8b9e0-187">Merhaba yeni koruma grubu oluşturma Sihirbazı açılır.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-187">This opens hello Create New Protection Group wizard.</span></span>

  ![Yeni koruma grubu oluşturma Sihirbazı](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-1.png)

3. <span data-ttu-id="8b9e0-189">Merhaba üzerinde **Hoş Geldiniz** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-189">On hello **Welcome** page, select **Next**.</span></span>
4. <span data-ttu-id="8b9e0-190">Merhaba üzerinde **koruma grubu türünü seçin** sayfasında, hello toocreate istediğiniz ve ardından koruma grubu türünü seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-190">On hello **Select Protection Group Type** page, select hello type of protection group you want toocreate, and then select **Next**.</span></span>

  ![Koruma grubu seç türü sayfası](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-2.png)

5. <span data-ttu-id="8b9e0-192">Merhaba üzerinde **grup üyelerini seçin** sayfasında hello **kullanılabilir üyeler** bölmesinde, koruma aracılarını listelenen hello üyeleriyle.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-192">On hello **Select Group Members** page, in hello **Available members** pane, hello members with protection agents are listed.</span></span> <span data-ttu-id="8b9e0-193">Bu örnekte, D:\ birimi seçin ve E:\ ve bunları toohello Ekle **seçili üyeleri** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-193">For this example, select volume D:\ and E:\ and add them toohello **Selected members** pane.</span></span> <span data-ttu-id="8b9e0-194">Seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-194">Select **Next**.</span></span>

  ![Grup Seç üyeleri sayfası](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-3.png)

6. <span data-ttu-id="8b9e0-196">Merhaba üzerinde **veri koruma yöntemini seçin** want bir **koruma grubu adı**hello koruma yöntemini seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-196">On hello **Select Data Protection Method** page, enter a **Protection group name**, select hello protection method, and then select **Next**.</span></span> <span data-ttu-id="8b9e0-197">Kısa vadeli koruma istiyorsanız hello seçmelisiniz **Disk** yedekleme yöntemi.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-197">If you want short-term protection, you must select hello **Disk** backup method.</span></span>

  ![Veri koruma yöntemini sayfa seçin](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-4.png)

7. <span data-ttu-id="8b9e0-199">Merhaba üzerinde **kısa vadeli hedefleri belirtin** sayfası, select hello ayrıntılarını **bekletme aralığı** ve **eşitleme sıklığı**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-199">On hello **Specify Short-Term Goals** page, select hello details for **Retention range** and **Synchronization frequency**.</span></span> <span data-ttu-id="8b9e0-200">Ardından, seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-200">Then, select **Next**.</span></span> <span data-ttu-id="8b9e0-201">Kurtarma noktalarının ne zaman çekildiği, select için isteğe bağlı olarak, toochange hello zamanlama **Değiştir**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-201">Optionally, toochange hello schedule for when recovery points are taken, select **Modify**.</span></span>

  ![Kısa vadeli hedefleri sayfasında belirtin](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-5.png)

8. <span data-ttu-id="8b9e0-203">Merhaba üzerinde **Disk Depolaması ayırmasını gözden** sayfasında, seçtiğiniz hello veri kaynakları ile ilgili ayrıntıları, boyutu ve sağlanan hello alanı toobe değerleri gözden geçirin ve hello hedef depolama birimi.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-203">On hello **Review Disk Storage Allocation** page, review details about hello data sources you selected, their size, and  values for hello space toobe provisioned and hello target storage volume.</span></span>

  ![Gözden geçirme Disk Depolaması ayırması sayfası](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-6.png)

  <span data-ttu-id="8b9e0-205">Depolama birimleri hello iş yükü birim ayırma (PowerShell kullanarak ayarlayın) dayanır ve kullanılabilir depolama alanı hello.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-205">Storage volumes are based on hello workload volume allocation (set by using PowerShell) and hello available storage.</span></span> <span data-ttu-id="8b9e0-206">Merhaba depolama birimleri hello açılan menüsünde diğer birimleri'i seçerek değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-206">You can change hello storage volumes by selecting other volumes in hello drop-down menu.</span></span> <span data-ttu-id="8b9e0-207">Merhaba değeri değiştirirseniz **hedef depolama**, hello için değer **kullanılabilir disk depolama** altında tooreflect değerleri dinamik olarak değişir **boş alan** ve **Underprovisioned alanı**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-207">If you change hello value for **Target Storage**, hello value for **Available disk storage** dynamically changes tooreflect values under **Free Space** and **Underprovisioned Space**.</span></span>

  <span data-ttu-id="8b9e0-208">Merhaba veri kaynakları planlı olarak büyüyecek, hello için değer hello **Underprovisioned alanı** sütununda **kullanılabilir disk depolama** hello gerekli olan ek depolama alanı miktarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-208">If hello data sources grow as planned, hello value for hello **Underprovisioned Space** column in **Available disk storage** reflects hello amount of additional storage that's needed.</span></span> <span data-ttu-id="8b9e0-209">Bu değer toohelp planı kesintisiz yedeklemeler için depolama alanı ihtiyaçlarınızı kullanın.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-209">Use this value toohelp plan your storage needs for smooth backups.</span></span> <span data-ttu-id="8b9e0-210">Merhaba değer sıfırsa hello öngörülebilir gelecekte depolama alanı hiçbir olası sorunları vardır.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-210">If hello value is zero, there are no potential problems with storage in hello foreseeable future.</span></span> <span data-ttu-id="8b9e0-211">Merhaba değer sıfır dışındaki bir sayı ise, ayrılmış yeterli depolama alanı yok (sizin koruma İlkesi ve hello veri boyutuna, korumalı üyeleri göre).</span><span class="sxs-lookup"><span data-stu-id="8b9e0-211">If hello value is a number other than zero, you do not have sufficient storage allocated  (based on your protection policy and hello data size of your protected members).</span></span>

  ![Eksik yüklenmiş disk depolama](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-7.png)

   <span data-ttu-id="8b9e0-213">koruma grubu, tam hello Sihirbazı'nı oluşturma toofinish.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-213">toofinish creating your protection group, complete hello wizard.</span></span>

## <a name="migrate-legacy-storage-toomodern-backup-storage"></a><span data-ttu-id="8b9e0-214">Eski depolama tooModern yedekleme depolama geçirme</span><span class="sxs-lookup"><span data-stu-id="8b9e0-214">Migrate legacy storage tooModern Backup Storage</span></span>
<span data-ttu-id="8b9e0-215">Yedekleme sunucusu v2 tooor yükleme ve yükseltme hello işletim sistemi tooWindows Server 2016 yükselttikten sonra koruma grupları toouse Modern yedekleme depolama güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-215">After you upgrade tooor install Backup Server v2 and upgrade hello operating system tooWindows Server 2016, update your protection groups toouse Modern Backup Storage.</span></span> <span data-ttu-id="8b9e0-216">Varsayılan olarak, koruma grupları değiştirilmez.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-216">By default, protection groups are not changed.</span></span> <span data-ttu-id="8b9e0-217">Bunlar başlangıçta kurulmuş gibi toofunction devam eder.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-217">They continue toofunction as they were initially set up.</span></span> 

<span data-ttu-id="8b9e0-218">Koruma grupları toouse Modern yedekleme depolama güncelleştirme isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-218">Updating protection groups toouse Modern Backup Storage is optional.</span></span> <span data-ttu-id="8b9e0-219">hello kullanarak tüm veri kaynaklarının korumasını durdurun tooupdate hello koruma grubu, veri seçeneği korur.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-219">tooupdate hello protection group, stop protection of all data sources by using hello retain data option.</span></span> <span data-ttu-id="8b9e0-220">Ardından, hello veri kaynakları tooa yeni koruma grubu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-220">Then, add hello data sources tooa new protection group.</span></span>

1. <span data-ttu-id="8b9e0-221">Hello Yöneticisi konsolu, hello seçin **koruma** özelliği.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-221">In hello Administrator Console, select hello **Protection** feature.</span></span> <span data-ttu-id="8b9e0-222">Merhaba, **koruma grubu üyesi** listesinde, hello üye sağ tıklayın ve ardından **üyenin korumasını Durdur**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-222">In hello **Protection Group Member** list, right-click hello member, and then select **Stop protection of member**.</span></span>

  ![Üyenin korumasını Durdur](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

2. <span data-ttu-id="8b9e0-224">Merhaba, **grubundan** iletişim kutusu, gözden geçirme hello kullanılan disk alanı ve hello kullanılabilir boş alanı hello depolama havuzu için.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-224">In hello **Remove from Group** dialog box, review hello used disk space and hello available free space for hello storage pool.</span></span> <span data-ttu-id="8b9e0-225">Hello varsayılan tooleave hello kurtarma noktaları hello diskteki ve bunların ilişkili bekletme ilkesi başına tooexpire izin.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-225">hello default is tooleave hello recovery points on hello disk and allow them tooexpire per their associated retention policy.</span></span> <span data-ttu-id="8b9e0-226">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-226">Click **OK**.</span></span>

  <span data-ttu-id="8b9e0-227">Merhaba tooimmediately dönüş hello kullanılan disk alanı toohello boş depolama havuzunu istiyorsanız seçin **diskteki çoğaltmayı Sil** onay kutusu toodelete hello yedekleme verileri (ve kurtarma noktaları) Bu üye ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-227">If you want tooimmediately return hello used disk space toohello free storage pool, select hello **Delete replica on disk** check box toodelete hello backup data (and recovery points) associated with that member.</span></span>

  ![Grup iletişim kutusundan Kaldır](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. <span data-ttu-id="8b9e0-229">Modern yedekleme depolama kullanan bir koruma grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-229">Create a protection group that uses Modern Backup Storage.</span></span> <span data-ttu-id="8b9e0-230">Merhaba korunmayan veri kaynaklarını içerir.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-230">Include hello unprotected data sources.</span></span>


## <a name="add-disks-tooincrease-legacy-storage"></a><span data-ttu-id="8b9e0-231">Diskleri tooincrease eski depolama ekleme</span><span class="sxs-lookup"><span data-stu-id="8b9e0-231">Add disks tooincrease legacy storage</span></span>

<span data-ttu-id="8b9e0-232">Yedekleme sunucusu ile toouse eski depolama istiyorsanız tooadd diskleri tooincrease eski depolama gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-232">If you want toouse legacy storage with Backup Server, you might need tooadd disks tooincrease legacy storage.</span></span> 

<span data-ttu-id="8b9e0-233">tooadd disk depolaması:</span><span class="sxs-lookup"><span data-stu-id="8b9e0-233">tooadd disk storage:</span></span>

1. <span data-ttu-id="8b9e0-234">Hello Yöneticisi konsolu, seçin **Yönetim** > **Disk Depolama** > **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-234">In hello Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![Disk depolama iletişim ekleyin](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

4. <span data-ttu-id="8b9e0-236">Merhaba, **Disk Depolama Alanı Ekle** iletişim kutusunda **eklemek diskleri**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-236">In hello **Add Disk Storage** dialog, select **Add disks**.</span></span>

5. <span data-ttu-id="8b9e0-237">Kullanılabilir diskler Hello listesinde tooadd, select istediğiniz hello diskleri seçin **Ekle**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-237">In hello list of available disks, select hello disks you want tooadd, select **Add**, and then select **OK**.</span></span>

## <a name="update-hello-data-protection-manager-protection-agent"></a><span data-ttu-id="8b9e0-238">Merhaba Data Protection Manager koruma aracısını güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="8b9e0-238">Update hello Data Protection Manager protection agent</span></span>

<span data-ttu-id="8b9e0-239">Yedek sunucu hello System Center Data Protection Manager koruma Aracısı güncelleştirmeleri için kullanır.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-239">Backup Server uses hello System Center Data Protection Manager protection agent for updates.</span></span> <span data-ttu-id="8b9e0-240">Bağlı toohello ağ bir koruma Aracısı yükseltme yapıyorsanız, hello Data Protection Manager Yönetici Konsolu toocomplete bağlı aracı yükseltme kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-240">If you are upgrading a protection agent that is not connected toohello network, you cannot use hello Data Protection Manager Administrator Console toocomplete a connected agent upgrade.</span></span> <span data-ttu-id="8b9e0-241">Etkin olmayan etki alanı ortamında hello koruma aracısını yükseltmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-241">You must upgrade hello protection agent in a nonactive domain environment.</span></span> <span data-ttu-id="8b9e0-242">Merhaba istemci bilgisayara bağlı toohello ağ olana kadar bu hello koruma Aracısı güncelleştirmesi Data Protection Manager Yönetici Konsolu gösterilir hello beklemede.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-242">Until hello client computer is connected toohello network, hello Data Protection Manager Administrator Console shows that hello protection agent update is pending.</span></span>

<span data-ttu-id="8b9e0-243">Merhaba aşağıdaki bölümlerde nasıl tooupdate koruma aracılarını bağlı istemci bilgisayarları ve bağlı olmayan istemci bilgisayarlar için.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-243">hello following sections describe how tooupdate protection agents for client computers that are connected and client computers that are not connected.</span></span>

### <a name="update-a-protection-agent-for-a-connected-client-computer"></a><span data-ttu-id="8b9e0-244">Bağlantılı bir istemci bilgisayarda koruma aracısını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="8b9e0-244">Update a protection agent for a connected client computer</span></span>

1. <span data-ttu-id="8b9e0-245">Hello yedekleme Sunucu Yöneticisi konsolu, seçin **Yönetim** > **aracıları**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-245">In hello Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="8b9e0-246">Merhaba görüntü bölmesinde tooupdate hello koruma Aracısı istediğiniz hello istemci bilgisayarları seçin.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-246">In hello display pane, select hello client computers for which you want tooupdate hello protection agent.</span></span>

  > [!NOTE]
  > <span data-ttu-id="8b9e0-247">Merhaba **aracı güncelleştirmeleri** sütun gösteren bir koruma Aracısı güncelleştirmesi her korumalı bilgisayar için kullanılabilir olduğunda.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-247">hello **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="8b9e0-248">Merhaba, **Eylemler** bölmesi, hello **güncelleştirme** eylem, yalnızca korumalı bir bilgisayarın seçili olduğundan ve kullanılabilir güncelleştirmeler olduğunda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-248">In hello **Actions** pane, hello **Update** action is available only when a protected computer is selected and updates are available.</span></span>
  >
  >

3. <span data-ttu-id="8b9e0-249">tooinstall koruma aracılarını hello içinde hello seçili bilgisayarlara güncelleştirilmiş **Eylemler** bölmesinde, **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-249">tooinstall updated protection agents on hello selected computers, in hello **Actions** pane, select **Update**.</span></span>

### <a name="update-a-protection-agent-on-a-client-computer-that-is-not-connected"></a><span data-ttu-id="8b9e0-250">Bağlı olmayan bir istemci bilgisayarda koruma aracısını güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="8b9e0-250">Update a protection agent on a client computer that is not connected</span></span>

1. <span data-ttu-id="8b9e0-251">Hello yedekleme Sunucu Yöneticisi konsolu, seçin **Yönetim** > **aracıları**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-251">In hello Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="8b9e0-252">Merhaba görüntü bölmesinde tooupdate hello koruma Aracısı istediğiniz hello istemci bilgisayarları seçin.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-252">In hello display pane, select hello client computers for which you want tooupdate hello protection agent.</span></span>

  > [!NOTE]
   > <span data-ttu-id="8b9e0-253">Merhaba **aracı güncelleştirmeleri** sütun gösteren bir koruma Aracısı güncelleştirmesi her korumalı bilgisayar için kullanılabilir olduğunda.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-253">hello **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="8b9e0-254">Merhaba, **Eylemler** bölmesi, hello **güncelleştirme** eylemi kullanılabilir değil korumalı bir bilgisayar seçildiğinde kullanılabilir güncelleştirme yoksa.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-254">In hello **Actions** pane, hello **Update** action is not available when a protected computer is selected unless updates are available.</span></span>
  >
  >

3. <span data-ttu-id="8b9e0-255">tooinstall koruma aracılarını select hello seçili bilgisayarlara güncelleştirilmiş **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-255">tooinstall updated protection agents on hello selected computers, select **Update**.</span></span>

4. <span data-ttu-id="8b9e0-256">Merhaba bilgisayar bağlı toohello ağ kadar toohello ağ olmayan bir istemci bilgisayara bağlı için hello **aracı durumu** sütun durumunu gösterir **güncelleştirme Beklemede**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-256">For a client computer that is not connected toohello network, until hello computer is connected toohello network, hello **Agent Status** column shows a status of **Update Pending**.</span></span>

  <span data-ttu-id="8b9e0-257">Bir istemci bilgisayara bağlı toohello ağ sonra hello **aracı güncelleştirmeleri** sütun hello istemci bilgisayar için bir durumu gösterir **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-257">After a client computer is connected toohello network, hello **Agent Updates** column for hello client computer shows a status of **Updating**.</span></span>
  
### <a name="move-legacy-protection-groups-from-old-version-and-sync-hello-new-version-with-azure"></a><span data-ttu-id="8b9e0-258">Eski sürümünü ve Azure ile eşitleme hello yeni sürümü eski koruma grupları taşıma</span><span class="sxs-lookup"><span data-stu-id="8b9e0-258">Move legacy Protection groups from old version and sync hello new version with Azure</span></span>

<span data-ttu-id="8b9e0-259">Azure yedekleme sunucusu ve hello işletim sistemi hem de güncelleştirilmiştir verdikten sonra hazır tooprotect Modern yedekleme depolama kullanarak yeni veri kaynakları demektir.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-259">Once Azure Backup Server and hello OS are both updated, you are ready tooprotect new data sources using Modern Backup Storage.</span></span> <span data-ttu-id="8b9e0-260">Ancak zaten korumalı veri kaynakları şekilde Azure yedekleme sunucusu olan, ancak tüm yeni koruması Modern yedekleme depolama kullanacak şekilde hello eski korumalı toobe devam eder.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-260">However already protected data sources will continue toobe protected in hello legacy way as they were in Azure Backup Server but all new protection will use Modern Backup Storage.</span></span>

<span data-ttu-id="8b9e0-261">Aşağıdaki adımları toomigrate veri koruma tooModern yedekleme depolama eski modundan kaynaklarıdır.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-261">Below steps are toomigrate data sources from legacy  mode of protection tooModern backup storage.</span></span>

<span data-ttu-id="8b9e0-262">• Hello yeni birimlerin toohello DPM depolama havuzu ekleyin ve isterseniz kolay adlarını ve veri kaynağı etiketleri atayın.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-262">• Add hello new volume(s) toohello DPM storage pool and assign friendly names and data source tags if desired.</span></span>
<span data-ttu-id="8b9e0-263">• Eski modda durdurma hello veri kaynakları ve "Korumalı verileri Koru" olan her veri kaynağı için.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-263">• For each data source that is in legacy mode, stop protection of hello data sources and “Retain Protected Data”.</span></span>  <span data-ttu-id="8b9e0-264">Bu kurtarma eski kurtarma noktaları geçişten sonra olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-264">This will allow recovery of old recovery points after migration.</span></span>

<span data-ttu-id="8b9e0-265">• Yeni PG oluşturun ve yeni biçimi kullanarak depolanan toobe olan hello veri kaynaklarını seçin.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-265">• Create a new PG and select hello data sources that are toobe stored using new format.</span></span>
<span data-ttu-id="8b9e0-266">• DPM Modern yedekleme depolama birimi yerel olarak hello hello eski yedekleme depolama biriminden çoğaltma kopyasını yapın.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-266">• DPM will do a replica copy from hello legacy backup storage into hello Modern Backup Storage volume locally.</span></span>
<span data-ttu-id="8b9e0-267">Not: Bu görülür tüm yeni eşitleme ve kurtarma noktalarını sonra Modern yedekleme depolama alanında depolanacak kurtarma sonrası işlemi iş • olarak.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-267">Note: This will be seen as a post-recovery operation job • All new sync and recovery points will then be stored in Modern Backup Storage.</span></span>
<span data-ttu-id="8b9e0-268">Süresi dolacak ve sonunda hello disk alanını boşaltmanız • eski kurtarma noktalarını kullanıma ayıklanır.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-268">• Old recovery points will be pruned out as they expire and eventually free up hello disk space.</span></span>
<span data-ttu-id="8b9e0-269">Tüm hello eski birimleri hello eski depolama biriminden, hello disk silindikten sonra • Azure yedekleme ve hello sistemden kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-269">• Once all hello legacy volumes are deleted from hello old storage, hello disk can be removed from Azure backup and hello system.</span></span>
<span data-ttu-id="8b9e0-270">• Hello Azure DPMDB yedeklemesini alın.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-270">• Take a backup of hello  Azure DPMDB.</span></span>

<span data-ttu-id="8b9e0-271">2. Kısım:-Önemli öğeleri > merhaba yeni sunucu, aynı adlı hello özgün Azure yedekleme sunucusu toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-271">Part 2: -Important items> hello new server will need toobe named same as hello original Azure Backup server.</span></span> <span data-ttu-id="8b9e0-272">Toouse eski depolama havuzu istiyorsanız ve DPMDB tooretain kurtarma noktaları - geri toobe ihtiyaç duyacağınız DPMDB yedeklemesini olmalıdır hello yeni Azure yedekleme sunucusu hello adı değiştirilemiyor</span><span class="sxs-lookup"><span data-stu-id="8b9e0-272">You cannot change hello name of hello new Azure backup server if you want toouse old storage pool and DPMDB tooretain recovery points -Must have backup of DPMDB  as it will need toobe restored</span></span>

1) <span data-ttu-id="8b9e0-273">Kapatma özgün Azure yedekleme sunucusu hello veya devre dışı hello kablo alır.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-273">Shutdown hello original Azure backup server or take it off hello wire.</span></span>
2) <span data-ttu-id="8b9e0-274">Merhaba makine hesabının active Directory'de sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-274">Reset hello machine account in active directory.</span></span>
3) <span data-ttu-id="8b9e0-275">Yeni bir makine ve hello özgün Azure yedekleme sunucusu olarak aynı makine adı hello adı Server 2016 yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-275">Install Server 2016 on new machine and name it hello same machine name as hello original Azure Backup server.</span></span>
4) <span data-ttu-id="8b9e0-276">Merhaba etki alanına katılma</span><span class="sxs-lookup"><span data-stu-id="8b9e0-276">Join hello Domain</span></span>
5) <span data-ttu-id="8b9e0-277">Azure yedekleme sunucusu V2 yükleyin (taşıma DPM depolama havuzu diskleri eski sunucu ve içeri aktarma)</span><span class="sxs-lookup"><span data-stu-id="8b9e0-277">Install Azure Backup server V2 (Move DPM Storage pool disks from old server and import)</span></span>
6) <span data-ttu-id="8b9e0-278">Merhaba Kısım 2 sonundan itibaren geçen DPMDB geri yükleme</span><span class="sxs-lookup"><span data-stu-id="8b9e0-278">Restore hello DPMDB taken from end of part 2</span></span>
7) <span data-ttu-id="8b9e0-279">Merhaba depolama hello özgün yedekleme sunucusu toohello yeni sunucudan ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8b9e0-279">Attach hello storage from hello original backup server toohello new server.</span></span>
8) <span data-ttu-id="8b9e0-280">DPMDB hello SQL geri yükleme</span><span class="sxs-lookup"><span data-stu-id="8b9e0-280">From SQL Restore hello DPMDB</span></span>
9) <span data-ttu-id="8b9e0-281">Yönetici komut satırından yeni sunucu cd tooMicrosoft Azure yedekleme konumu ve depo klasörüne yükleyin</span><span class="sxs-lookup"><span data-stu-id="8b9e0-281">From admin command line on new server cd tooMicrosoft Azure Backup install location and bin folder</span></span>

<span data-ttu-id="8b9e0-282">Yol örnek: C:\windows\system32 > cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span><span class="sxs-lookup"><span data-stu-id="8b9e0-282">Path example: C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span></span>
<span data-ttu-id="8b9e0-283">tooAzure yedekleme çalıştırmak DPMSYNC-SYNC</span><span class="sxs-lookup"><span data-stu-id="8b9e0-283">tooAzure backup Run DPMSYNC -SYNC</span></span>

10) <span data-ttu-id="8b9e0-284">Dpmsync aracını çalıştırın-eşitleme Not hello eskilerle, taşıma yerine yeni diskler toohello DPM depolama havuzu eklediyseniz ardından çalıştırın DPMSYNC - reallocatereplica öğesini</span><span class="sxs-lookup"><span data-stu-id="8b9e0-284">Run DPMSYNC -SYNC Note If you have added NEW disks toohello DPM Storage pool instead of moving hello old ones, then run DPMSYNC -Reallocatereplica</span></span>

## <a name="new-powershell-cmdlets-in-v2"></a><span data-ttu-id="8b9e0-285">V2 yeni PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="8b9e0-285">New PowerShell cmdlets in v2</span></span>

<span data-ttu-id="8b9e0-286">Azure yedekleme sunucusu v2 yüklediğinizde, iki yeni cmdlet'leri kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="8b9e0-286">When you install Azure Backup Server v2, two new cmdlets are available:</span></span> 
* [<span data-ttu-id="8b9e0-287">Bağlama DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="8b9e0-287">Mount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787159.aspx)
* [<span data-ttu-id="8b9e0-288">Çıkarma DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="8b9e0-288">Dismount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787158.aspx)

## <a name="next-steps"></a><span data-ttu-id="8b9e0-289">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8b9e0-289">Next steps</span></span>

<span data-ttu-id="8b9e0-290">Bilgi nasıl tooprepare sunucunuz veya bir iş yükü korumaya başlamak:</span><span class="sxs-lookup"><span data-stu-id="8b9e0-290">Learn how tooprepare your server or begin protecting a workload:</span></span>
- [<span data-ttu-id="8b9e0-291">Yedekleme sunucusu iş yükleri hazırlama</span><span class="sxs-lookup"><span data-stu-id="8b9e0-291">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="8b9e0-292">Bir VMware sunucusu yedekleme sunucusu tooback kullanın</span><span class="sxs-lookup"><span data-stu-id="8b9e0-292">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="8b9e0-293">SQL Server Yedekleme Sunucusu tooback kullanın</span><span class="sxs-lookup"><span data-stu-id="8b9e0-293">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="8b9e0-294">Yedekleme sunucusu ile modern yedekleme depolama alanı kullanın</span><span class="sxs-lookup"><span data-stu-id="8b9e0-294">Use Modern Backup Storage with Backup Server</span></span>](backup-mabs-add-storage.md)

