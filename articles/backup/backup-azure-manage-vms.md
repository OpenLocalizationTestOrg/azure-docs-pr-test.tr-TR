---
title: "aaaManage Resource Manager tarafından dağıtılan sanal makine yedeklerini | Microsoft Docs"
description: "Bilgi nasıl toomanage ve İzleyici Resource Manager tarafından dağıtılan sanal makine yedekleme"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: f3050283-d60f-472d-b464-cb844e70d67e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: trinadhk;markgal
ms.openlocfilehash: 241fc4b2a29c5cd8b8b0ee8efbf8ba4e96c6a7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-machine-backups"></a><span data-ttu-id="bc2a8-103">Azure sanal makine yedeklemelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="bc2a8-103">Manage Azure virtual machine backups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bc2a8-104">Azure VM yedeklemeleri yönetme</span><span class="sxs-lookup"><span data-stu-id="bc2a8-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="bc2a8-105">Klasik VM yedeklemeleri yönetme</span><span class="sxs-lookup"><span data-stu-id="bc2a8-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="bc2a8-106">Bu makalede VM yedekleri yönetmeyle ilgili yönergeler sağlar ve hello yedekleme uyarıları bilgi hello portal panosunda kullanılabilir açıklar.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-106">This article provides guidance on managing VM backups, and explains hello backup alerts information available in hello portal dashboard.</span></span> <span data-ttu-id="bc2a8-107">Bu makalede Hello yönerge toousing Vm'leri kurtarma Hizmetleri kasaları ile geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-107">hello guidance in this article applies toousing VMs with Recovery Services vaults.</span></span> <span data-ttu-id="bc2a8-108">Bu makalede hello sanal makinelerin oluşturulmasını kapsamaz ya da onu açıklayan nasıl tooprotect sanal makineler.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-108">This article does not cover hello creation of virtual machines, nor does it explain how tooprotect virtual machines.</span></span> <span data-ttu-id="bc2a8-109">Azure Resource Manager tarafından dağıtılan Vm'leri Azure kurtarma Hizmetleri kasası ile koruma öncü için bkz: [ilk bakış: geri kurtarma Hizmetleri kasası VM'ler tooa yukarı](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="bc2a8-109">For a primer on protecting Azure Resource Manager-deployed VMs in Azure with a Recovery Services vault, see [First look: Back up VMs tooa Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span>

## <a name="manage-vaults-and-protected-virtual-machines"></a><span data-ttu-id="bc2a8-110">Kasa ve korumalı sanal makineleri yönetme</span><span class="sxs-lookup"><span data-stu-id="bc2a8-110">Manage vaults and protected virtual machines</span></span>
<span data-ttu-id="bc2a8-111">Hello Azure portal, kasa hello dahil olmak üzere ilgili erişim tooinformation hello kurtarma Hizmetleri kasa Panosu sağlar:</span><span class="sxs-lookup"><span data-stu-id="bc2a8-111">In hello Azure portal, hello Recovery Services vault dashboard provides access tooinformation about hello vault including:</span></span>

* <span data-ttu-id="bc2a8-112">Ayrıca hello en son geri yükleme noktası olan yedekleme anlık görüntüsü, hello en son < br\></span><span class="sxs-lookup"><span data-stu-id="bc2a8-112">hello most recent backup snapshot, which is also hello latest restore point <br\></span></span>
* <span data-ttu-id="bc2a8-113">Yedekleme İlkesi merhaba < br\></span><span class="sxs-lookup"><span data-stu-id="bc2a8-113">hello backup policy <br\></span></span>
* <span data-ttu-id="bc2a8-114">tüm yedekleme anlık görüntülerinin boyutunu toplam < br\></span><span class="sxs-lookup"><span data-stu-id="bc2a8-114">total size of all backup snapshots <br\></span></span>
* <span data-ttu-id="bc2a8-115">Merhaba kasası ile korunan sanal makineler sayısı < br\></span><span class="sxs-lookup"><span data-stu-id="bc2a8-115">number of virtual machines that are protected with hello vault <br\></span></span>

<span data-ttu-id="bc2a8-116">Bir sanal makine yedekleme ile çok sayıda yönetim görevi hello kasası hello panosunda açma ile başlar.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-116">Many management tasks with a virtual machine backup begin with opening hello vault in hello dashboard.</span></span> <span data-ttu-id="bc2a8-117">Ancak, birden çok öğe (veya birden çok VM) hakkında belirli bir VM, tooview ayrıntıları açmak kullanılan tooprotect kasalarını olabileceğinden hello kasa öğesi Panosu.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-117">However, because vaults can be used tooprotect multiple items (or multiple VMs), tooview details about a particular VM, open hello vault item dashboard.</span></span> <span data-ttu-id="bc2a8-118">Merhaba aşağıdaki yordamda nasıl gösterilmektedir tooopen hello *kasa Panosu* ve toohello devam *kasa öğesi Panosu*.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-118">hello following procedure shows you how tooopen hello *vault dashboard* and then continue toohello *vault item dashboard*.</span></span> <span data-ttu-id="bc2a8-119">Nasıl tooadd kasası hello öğesi toohello kasa çıkışı Azure Pano hello PIN toodashboard komutunu kullanarak noktası ve her iki yordamı "ipuçları" yoktur.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-119">There are "tips" in both procedures that point out how tooadd hello vault and vault item toohello Azure dashboard by using hello Pin toodashboard command.</span></span> <span data-ttu-id="bc2a8-120">PIN toodashboard öğe veya kısayol toohello kasa oluşturma yoludur.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-120">Pin toodashboard is a way of creating a shortcut toohello vault or item.</span></span> <span data-ttu-id="bc2a8-121">Ayrıca, sık kullanılan komutlar hello kısayoldan yürütebilir.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-121">You can also execute common commands from hello shortcut.</span></span>

> [!TIP]
> <span data-ttu-id="bc2a8-122">Birden çok panolar varsa ve dikey pencere açılır hello Koyu mavi kaydırıcı hello penceresi tooslide hello geri ve İleri Azure Pano hello altındaki kullanın.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-122">If you have multiple dashboards and blades open, use hello dark-blue slider at hello bottom of hello window tooslide hello Azure dashboard back and forth.</span></span>
>
>

![Kaydırıcı ile tam görünümü](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-hello-dashboard"></a><span data-ttu-id="bc2a8-124">Kurtarma Hizmetleri kasası hello panosunda açın:</span><span class="sxs-lookup"><span data-stu-id="bc2a8-124">Open a Recovery Services vault in hello dashboard:</span></span>
1. <span data-ttu-id="bc2a8-125">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bc2a8-125">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="bc2a8-126">Merhaba Hub menüsünde **Gözat** ve kaynakları hello listesinde yazın **kurtarma Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-126">On hello Hub menu, click **Browse** and in hello list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="bc2a8-127">Yazmaya başladığınızda liste filtreleri, girişinize göre hello.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-127">As you begin typing, hello list filters based on your input.</span></span> <span data-ttu-id="bc2a8-128">**Kurtarma Hizmetleri kasası** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-128">Click **Recovery Services vault**.</span></span>

    ![Kurtarma Hizmetleri Kasası oluşturma 1. adım](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    <span data-ttu-id="bc2a8-130">Merhaba kurtarma Hizmetleri kasalarının listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-130">hello list of Recovery Services vaults are displayed.</span></span>

    ![<span data-ttu-id="bc2a8-131">Liste kurtarma Hizmetleri kasaları</span><span class="sxs-lookup"><span data-stu-id="bc2a8-131">List of Recovery Services vaults</span></span> ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > <span data-ttu-id="bc2a8-132">Kasa toohello Azure Pano sabitlerseniz hello Azure portal'ı açtığınızda, kasa hemen erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-132">If you pin a vault toohello Azure Dashboard, that vault is immediately accessible when you open hello Azure portal.</span></span> <span data-ttu-id="bc2a8-133">toopin hello kasa listesinde, bir kasa toohello Panosu hello kasası sağ tıklatın ve seçin **PIN toodashboard**.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-133">toopin a vault toohello dashboard, in hello vault list, right-click hello vault, and select **Pin toodashboard**.</span></span>
   >
   >
3. <span data-ttu-id="bc2a8-134">Kasa Hello listeden hello kasa tooopen kendi Pano seçin.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-134">From hello list of vaults, select hello vault tooopen its dashboard.</span></span> <span data-ttu-id="bc2a8-135">Merhaba kasası, hello kasa panosunu ve hello seçtiğinizde **ayarları** dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-135">When you select hello vault, hello vault dashboard and hello **Settings** blade open.</span></span> <span data-ttu-id="bc2a8-136">Görüntü aşağıdaki hello hello **Contoso kasa** Pano vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-136">In hello following image, hello **Contoso-vault** dashboard is highlighted.</span></span>

    ![Kasa panosunu ve ayarlar dikey penceresi açın](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a><span data-ttu-id="bc2a8-138">Kasa öğesi panosunu açın</span><span class="sxs-lookup"><span data-stu-id="bc2a8-138">Open a vault item dashboard</span></span>
<span data-ttu-id="bc2a8-139">Merhaba önceki yordamda hello kasa panosu açılır.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-139">In hello previous procedure you opened hello vault dashboard.</span></span> <span data-ttu-id="bc2a8-140">tooopen hello kasa öğesi Panosu:</span><span class="sxs-lookup"><span data-stu-id="bc2a8-140">tooopen hello vault item dashboard:</span></span>

1. <span data-ttu-id="bc2a8-141">Merhaba üzerinde hello kasa panosunda **yedekleme öğeleri** döşeme, tıklatın **Azure sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-141">In hello vault dashboard, on hello **Backup Items** tile, click **Azure Virtual Machines**.</span></span>

    ![Yedekleme öğeleri Aç döşeme](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    <span data-ttu-id="bc2a8-143">Merhaba **yedekleme öğeleri** dikey penceresinde hello son yedekleme işi her öğe için listelenir.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-143">hello **Backup Items** blade lists hello last backup job for each item.</span></span> <span data-ttu-id="bc2a8-144">Bu örnekte, bir bu kasası tarafından korunan sanal makinenin, demovm-markgal yoktur.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-144">In this example, there is one virtual machine, demovm-markgal, protected by this vault.</span></span>  

    ![Yedekleme öğeleri döşeme](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > <span data-ttu-id="bc2a8-146">Erişim Kolaylığı için bir kasa öğesi toohello Azure Pano sabitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-146">For ease of access, you can pin a vault item toohello Azure Dashboard.</span></span> <span data-ttu-id="bc2a8-147">toopin hello kasası öğe listesi, sağ hello öğesini seçip bir kasa öğesi **PIN toodashboard**.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-147">toopin a vault item, in hello vault item list, right-click hello item and select **Pin toodashboard**.</span></span>
   >
   >
2. <span data-ttu-id="bc2a8-148">Merhaba, **yedekleme öğeleri** dikey penceresinde hello öğesi tooopen hello kasası öğesi panosunu'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-148">In hello **Backup Items** blade, click hello item tooopen hello vault item dashboard.</span></span>

    ![Yedekleme öğeleri döşeme](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    <span data-ttu-id="bc2a8-150">Merhaba kasası öğesi panosunu ve kendi **ayarları** dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-150">hello vault item dashboard and its **Settings** blade open.</span></span>

    ![Ayarlar dikey penceresi ile yedekleme öğeleri Panosu](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    <span data-ttu-id="bc2a8-152">Merhaba kasası öğe panodan gibi birçok önemli yönetim görevleri gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bc2a8-152">From hello vault item dashboard, you can accomplish many key management tasks, such as:</span></span>

   * <span data-ttu-id="bc2a8-153">ilkeleri değiştirebilir veya yeni bir yedekleme ilkesi oluşturabilirsiniz < br\></span><span class="sxs-lookup"><span data-stu-id="bc2a8-153">change policies or create a new backup policy<br\></span></span>
   * <span data-ttu-id="bc2a8-154">geri yükleme noktaları görüntülemek ve tutarlılık durumlarına bakın < br\></span><span class="sxs-lookup"><span data-stu-id="bc2a8-154">view restore points, and see their consistency state <br\></span></span>
   * <span data-ttu-id="bc2a8-155">İsteğe bağlı bir sanal makinenin yedeğini < br\></span><span class="sxs-lookup"><span data-stu-id="bc2a8-155">on-demand backup of a virtual machine <br\></span></span>
   * <span data-ttu-id="bc2a8-156">sanal makineler korunmasını durdurmayı < br\></span><span class="sxs-lookup"><span data-stu-id="bc2a8-156">stop protecting virtual machines <br\></span></span>
   * <span data-ttu-id="bc2a8-157">bir sanal makine korumayı sürdürmek < br\></span><span class="sxs-lookup"><span data-stu-id="bc2a8-157">resume protection of a virtual machine <br\></span></span>
   * <span data-ttu-id="bc2a8-158">Yedekleme verilerini (veya kurtarma noktası) silme < br\></span><span class="sxs-lookup"><span data-stu-id="bc2a8-158">delete a backup data (or recovery point) <br\></span></span>
   * <span data-ttu-id="bc2a8-159">[Yedekleme diskleri geri](backup-azure-arm-restore-vms.md#restore-backed-up-disks) < br\></span><span class="sxs-lookup"><span data-stu-id="bc2a8-159">[restore backup disks](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span></span>

<span data-ttu-id="bc2a8-160">Yordamları izleyerek hello için başlangıç noktası hello hello kasası öğesi panosunu ' dir.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-160">For hello following procedures, hello starting point is hello vault item dashboard.</span></span>

## <a name="manage-backup-policies"></a><span data-ttu-id="bc2a8-161">Yedekleme ilkelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="bc2a8-161">Manage backup policies</span></span>
1. <span data-ttu-id="bc2a8-162">Merhaba üzerinde [kasa öğesi Panosu](backup-azure-manage-vms.md#open-a-vault-item-dashboard), tıklatın **tüm ayarları** tooopen hello **ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-162">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **All Settings** tooopen hello **Settings** blade.</span></span>

    ![Yedekleme İlkesi dikey penceresi](./media/backup-azure-manage-vms/all-settings-button.png)
2. <span data-ttu-id="bc2a8-164">Merhaba üzerinde **ayarları** dikey penceresinde tıklatın **yedekleme İlkesi** tooopen o dikey.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-164">On hello **Settings** blade, click **Backup policy** tooopen that blade.</span></span>

    <span data-ttu-id="bc2a8-165">Merhaba dikey penceresinde hello yedekleme sıklığı ve bekletme aralığı ayrıntıları gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-165">On hello blade, hello backup frequency and retention range details are shown.</span></span>

    ![Yedekleme İlkesi dikey penceresi](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. <span data-ttu-id="bc2a8-167">Merhaba gelen **yedekleme ilkesi seçin** menüsü:</span><span class="sxs-lookup"><span data-stu-id="bc2a8-167">From hello **Choose backup policy** menu:</span></span>

   * <span data-ttu-id="bc2a8-168">toochange ilkeleri, başka bir ilke seçin ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-168">toochange policies, select a different policy and click **Save**.</span></span> <span data-ttu-id="bc2a8-169">Merhaba yeni ilke hemen uygulanan toohello kasası olur.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-169">hello new policy is immediately applied toohello vault.</span></span> <span data-ttu-id="bc2a8-170">< br\></span><span class="sxs-lookup"><span data-stu-id="bc2a8-170"><br\></span></span>
   * <span data-ttu-id="bc2a8-171">toocreate bir ilke seçin **Yeni Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-171">toocreate a policy, select **Create New**.</span></span>

     ![Sanal makine yedekleme](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     <span data-ttu-id="bc2a8-173">Bir yedekleme ilkesi oluşturma ile ilgili yönergeler için bkz: [yedekleme ilkesi tanımlama](backup-azure-manage-vms.md#defining-a-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="bc2a8-173">For instructions on creating a backup policy, see [Defining a backup policy](backup-azure-manage-vms.md#defining-a-backup-policy).</span></span>

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> <span data-ttu-id="bc2a8-174">Yedekleme ilkelerini yönetirken emin toofollow hello olun [en iyi uygulamalar](backup-azure-vms-introduction.md#best-practices) en iyi yedekleme performansı</span><span class="sxs-lookup"><span data-stu-id="bc2a8-174">While managing backup policies, make sure toofollow hello [best practices](backup-azure-vms-introduction.md#best-practices) for optimal backup performance</span></span>
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="bc2a8-175">Bir sanal makinenin talep üzerine yedekleme</span><span class="sxs-lookup"><span data-stu-id="bc2a8-175">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="bc2a8-176">Koruma için yapılandırıldıktan sonra isteğe bağlı bir sanal makine yedekleme devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-176">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="bc2a8-177">Merhaba ilk yedekleme bekleme durumundaysa, talep üzerine yedekleme kurtarma Hizmetleri kasası hello hello sanal makinenin tam bir kopyasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-177">If hello initial backup is pending, on-demand backup creates a full copy of hello virtual machine in hello Recovery Services vault.</span></span> <span data-ttu-id="bc2a8-178">Merhaba ilk yedekleme tamamlandığında, bir talep üzerine yedekleme değişiklikleri hello önceki anlık görüntüden, toohello kurtarma Hizmetleri kasası yalnızca gönderin.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-178">If hello initial backup is completed, an on-demand backup will only send changes from hello previous snapshot, toohello Recovery Services vault.</span></span> <span data-ttu-id="bc2a8-179">Diğer bir deyişle, sonraki yedeklemeleri her zaman artımlı.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-179">That is, subsequent backups are always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="bc2a8-180">bir talep üzerine yedekleme için Hello bekletme aralığı hello günlük yedekleme noktası hello İlkesi'nde belirtilen hello bekletme değerdir.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-180">hello retention range for an on-demand backup is hello retention value specified for hello Daily backup point in hello policy.</span></span> <span data-ttu-id="bc2a8-181">Hiçbir günlük yedekleme noktası seçtiyseniz hello haftalık yedekleme noktası kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-181">If no Daily backup point is selected, then hello weekly backup point is used.</span></span>
>
>

<span data-ttu-id="bc2a8-182">bir sanal makinenin yedeğini tootrigger isteğe bağlı:</span><span class="sxs-lookup"><span data-stu-id="bc2a8-182">tootrigger an on-demand backup of a virtual machine:</span></span>

* <span data-ttu-id="bc2a8-183">Merhaba üzerinde [kasa öğesi Panosu](backup-azure-manage-vms.md#open-a-vault-item-dashboard), tıklatın **Şimdi Yedekle**.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-183">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Backup now**.</span></span>

    ![Yedekleme şimdi düğmesi](./media/backup-azure-manage-vms/backup-now-button.png)

    <span data-ttu-id="bc2a8-185">Merhaba portal toostart talep üzerine yedekleme işi istediğiniz emin olur.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-185">hello portal makes sure that you want toostart an on-demand backup job.</span></span> <span data-ttu-id="bc2a8-186">Tıklatın **Evet** toostart hello yedekleme işi.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-186">Click **Yes** toostart hello backup job.</span></span>

    ![Yedekleme şimdi düğmesi](./media/backup-azure-manage-vms/backup-now-check.png)

    <span data-ttu-id="bc2a8-188">Merhaba yedekleme işi, bir kurtarma noktası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-188">hello backup job creates a recovery point.</span></span> <span data-ttu-id="bc2a8-189">Merhaba bekletme aralığı hello kurtarma noktası olan hello hello sanal makineyle ilişkili hello İlkesi'nde belirtilen bekletme aralığı ile aynı.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-189">hello retention range of hello recovery point is hello same as retention range specified in hello policy associated with hello virtual machine.</span></span> <span data-ttu-id="bc2a8-190">tootrack hello ilerleme hello kasa panosunda, hello işi için tıklatın hello **yedekleme işlerini** döşeme.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-190">tootrack hello progress for hello job, in hello vault dashboard, click hello **Backup Jobs** tile.</span></span>  

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="bc2a8-191">Sanal makineleri koruma Durdur</span><span class="sxs-lookup"><span data-stu-id="bc2a8-191">Stop protecting virtual machines</span></span>
<span data-ttu-id="bc2a8-192">Bir sanal makine koruma toostop seçerseniz, tooretain hello kurtarma noktaları isteyip istemediğinizi istenir.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-192">If you choose toostop protecting a virtual machine, you are asked if you want tooretain hello recovery points.</span></span> <span data-ttu-id="bc2a8-193">Toostop koruma sanal makineleri iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="bc2a8-193">There are two ways toostop protecting virtual machines:</span></span>

* <span data-ttu-id="bc2a8-194">sonraki tüm yedekleme işleri durdurun ve tüm kurtarma noktalarını silin veya</span><span class="sxs-lookup"><span data-stu-id="bc2a8-194">stop all future backup jobs and delete all recovery points, or</span></span>
* <span data-ttu-id="bc2a8-195">sonraki tüm yedekleme işleri durdurmak, ancak kurtarma noktaları hello bırakın</span><span class="sxs-lookup"><span data-stu-id="bc2a8-195">stop all future backup jobs but leave hello recovery points</span></span> <br/>

<span data-ttu-id="bc2a8-196">Depolama birimindeki kurtarma noktaları hello bırakarak ile ilişkili bir maliyeti yoktur.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-196">There is a cost associated with leaving hello recovery points in storage.</span></span> <span data-ttu-id="bc2a8-197">Ancak, Kurtarma noktaları hello bırakarak hello yararı hello sanal makineyi daha sonra geri isterseniz olur.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-197">However, hello benefit of leaving hello recovery points is you can restore hello virtual machine later, if desired.</span></span> <span data-ttu-id="bc2a8-198">Kurtarma noktaları hello bırakarak hakkında bilgi için hello maliyeti, hello bkz [fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="bc2a8-198">For information about hello cost of leaving hello recovery points, see hello  [pricing details](https://azure.microsoft.com/pricing/details/backup/).</span></span> <span data-ttu-id="bc2a8-199">Tüm kurtarma noktalarının toodelete seçerseniz, hello sanal makine geri yükleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-199">If you choose toodelete all recovery points, you cannot restore hello virtual machine.</span></span>

<span data-ttu-id="bc2a8-200">bir sanal makine için korumayı toostop:</span><span class="sxs-lookup"><span data-stu-id="bc2a8-200">toostop protection for a virtual machine:</span></span>

1. <span data-ttu-id="bc2a8-201">Merhaba üzerinde [kasa öğesi Panosu](backup-azure-manage-vms.md#open-a-vault-item-dashboard), tıklatın **Dur yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-201">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Stop backup**.</span></span>

    ![Yedek düğmesini Durdur](./media/backup-azure-manage-vms/stop-backup-button.png)

    <span data-ttu-id="bc2a8-203">Merhaba Durdur yedekleme dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-203">hello Stop Backup blade opens.</span></span>

    ![Yedekleme dikey penceresini Durdur](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. <span data-ttu-id="bc2a8-205">Merhaba üzerinde **durdurmak yedekleme** dikey penceresinde tooretain ya da delete yedekleme verilerini hello olup olmadığını seçin.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-205">On hello **Stop Backup** blade, choose whether tooretain or delete hello backup data.</span></span> <span data-ttu-id="bc2a8-206">Merhaba bilgileri kutusunda seçiminizi hakkında ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-206">hello information box provides details about your choice.</span></span>

    ![Korumayı Durdur](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. <span data-ttu-id="bc2a8-208">Tooretain hello yedekleme verilerini seçerseniz, toostep 4 atlayın.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-208">If you chose tooretain hello backup data, skip toostep 4.</span></span> <span data-ttu-id="bc2a8-209">Toodelete yedekleme verilerini seçerseniz, toostop hello yedekleme işleri istediğiniz ve hello kurtarma noktaları - hello öğesinin tür hello adı silme onaylayın.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-209">If you chose toodelete backup data, confirm that you want toostop hello backup jobs and delete hello recovery points - type hello name of hello item.</span></span>

    ![Doğrulama Durdur](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="bc2a8-211">Merhaba öğesinin adını emin değilseniz, hello ünlem işareti tooview hello adın üzerine gelin.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-211">If you aren't sure of hello item name, hover over hello exclamation mark tooview hello name.</span></span> <span data-ttu-id="bc2a8-212">Ayrıca, hello hello öğesi altında adıdır **durdurmak yedekleme** hello dikey penceresinde hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-212">Also, hello name of hello item is under **Stop Backup** at hello top of hello blade.</span></span>
4. <span data-ttu-id="bc2a8-213">İsteğe bağlı olarak sağlayan bir **neden** veya **açıklama**.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-213">Optionally provide a **Reason** or **Comment**.</span></span>
5. <span data-ttu-id="bc2a8-214">Merhaba geçerli öğenin toostop hello yedekleme işini tıklatın ![Dur yedekleme düğmesi](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span><span class="sxs-lookup"><span data-stu-id="bc2a8-214">toostop hello backup job for hello current item, click  ![Stop backup button](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span></span>

    <span data-ttu-id="bc2a8-215">Bir bildirim iletisi, hello yedekleme işleri durduruldu bilmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-215">A notification message lets you know hello backup jobs have been stopped.</span></span>

    ![Durdurma onaylayın](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a><span data-ttu-id="bc2a8-217">Bir sanal makine korumayı Sürdür</span><span class="sxs-lookup"><span data-stu-id="bc2a8-217">Resume protection of a virtual machine</span></span>
<span data-ttu-id="bc2a8-218">Merhaba, **yedekleme verileri koru** seçeneği seçildi hello sanal makine için korumayı durduğunda olası tooresume koruma olur.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-218">If hello **Retain Backup Data** option was chosen when protection for hello virtual machine was stopped, then it is possible tooresume protection.</span></span> <span data-ttu-id="bc2a8-219">Merhaba, **yedekleme verilerini Sil** seçeneği seçildi, ardından hello sanal makine için koruma devam edemiyor.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-219">If hello **Delete Backup Data** option was chosen, then protection for hello virtual machine cannot resume.</span></span>

<span data-ttu-id="bc2a8-220">Merhaba sanal makine için tooresume koruma</span><span class="sxs-lookup"><span data-stu-id="bc2a8-220">tooresume protection for hello virtual machine</span></span>

1. <span data-ttu-id="bc2a8-221">Merhaba üzerinde [kasa öğesi Panosu](backup-azure-manage-vms.md#open-a-vault-item-dashboard), tıklatın **yedeklemeyi Sürdür**.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-221">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Resume backup**.</span></span>

    ![Korumayı Sürdür](./media/backup-azure-manage-vms/resume-backup-button.png)

    <span data-ttu-id="bc2a8-223">Merhaba yedekleme İlkesi dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-223">hello Backup Policy blade opens.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bc2a8-224">Merhaba sanal makine yeniden korurken, başka bir ilke ile sanal makine başlangıçta korunan hello ilkesinden seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-224">When re-protecting hello virtual machine, you can choose a different policy than hello policy with which virtual machine was protected initially.</span></span>
   >
   >
2. <span data-ttu-id="bc2a8-225">Merhaba adımları [yedekleme ilkelerini yönetme](backup-azure-manage-vms.md#manage-backup-policies) tooassign hello İlkesi hello sanal makine için.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-225">Follow hello steps in [Manage backup policies](backup-azure-manage-vms.md#manage-backup-policies) tooassign hello policy for hello virtual machine.</span></span>

    <span data-ttu-id="bc2a8-226">Merhaba yedekleme ilkesi uygulanan toohello sanal makine eklendiğinde, iletiden hello bakın.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-226">Once hello backup policy is applied toohello virtual machine, you see hello following message.</span></span>

    ![Başarıyla korumalı VM](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a><span data-ttu-id="bc2a8-228">Yedekleme verilerini sil</span><span class="sxs-lookup"><span data-stu-id="bc2a8-228">Delete Backup data</span></span>
<span data-ttu-id="bc2a8-229">Başlangıç sırasında sanal makine ile ilişkili hello yedekleme verileri silebilirsiniz **Dur yedekleme** işi, veya hello sonra yedekleme işi tamamlandı zaman.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-229">You can delete hello backup data associated with a virtual machine during hello **Stop backup** job, or anytime after hello backup job has completed.</span></span> <span data-ttu-id="bc2a8-230">Faydalı toowait gün veya hafta hello kurtarma noktaları silmeden önce bile olabilir.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-230">It may even be beneficial toowait days or weeks before deleting hello recovery points.</span></span> <span data-ttu-id="bc2a8-231">Kurtarma noktaları, yedek verileri silerken geri farklı olarak, belirli bir kurtarma noktaları toodelete seçemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-231">Unlike restoring recovery points, when deleting backup data, you cannot choose specific recovery points toodelete.</span></span> <span data-ttu-id="bc2a8-232">Yedek verilerinizin toodelete seçerseniz, hello öğeyle ilişkili tüm kurtarma noktalarını silin.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-232">If you choose toodelete your backup data, you delete all recovery points associated with hello item.</span></span>

<span data-ttu-id="bc2a8-233">Merhaba aşağıdaki yordamı hello yedekleme işi hello sanal makinenin durdurulmuş veya devre dışı varsayar.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-233">hello following procedure assumes hello Backup job for hello virtual machine has been stopped or disabled.</span></span> <span data-ttu-id="bc2a8-234">Merhaba yedekleme işini devre dışı bırakıldığında hello **yedeklemeyi Sürdür** ve **Delete yedekleme** hello kasası öğesi panosunda seçenekleri mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-234">Once hello Backup job is disabled, hello **Resume backup** and **Delete backup** options are available in hello vault item dashboard.</span></span>

![Devam ettirme ve silme düğmeleri](./media/backup-azure-manage-vms/resume-delete-buttons.png)

<span data-ttu-id="bc2a8-236">Merhaba sahip bir sanal makine yedekleme verileri toodelete *yedekleme devre dışı*:</span><span class="sxs-lookup"><span data-stu-id="bc2a8-236">toodelete backup data on a virtual machine with hello *Backup disabled*:</span></span>

1. <span data-ttu-id="bc2a8-237">Merhaba üzerinde [kasa öğesi Panosu](backup-azure-manage-vms.md#open-a-vault-item-dashboard), tıklatın **Delete yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-237">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Delete backup**.</span></span>

    ![VM türü](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    <span data-ttu-id="bc2a8-239">Merhaba **yedekleme verilerini Sil** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-239">hello **Delete Backup Data** blade opens.</span></span>

    ![VM türü](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. <span data-ttu-id="bc2a8-241">Tür hello adı hello öğesi tooconfirm toodelete hello kurtarma noktaları istiyor.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-241">Type hello name of hello item tooconfirm you want toodelete hello recovery points.</span></span>

    ![Doğrulama Durdur](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="bc2a8-243">Merhaba öğesinin adını emin değilseniz, hello ünlem işareti tooview hello adın üzerine gelin.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-243">If you aren't sure of hello item name, hover over hello exclamation mark tooview hello name.</span></span> <span data-ttu-id="bc2a8-244">Ayrıca, hello hello öğesi altında adıdır **yedekleme verilerini Sil** hello dikey penceresinde hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-244">Also, hello name of hello item is under **Delete Backup Data** at hello top of hello blade.</span></span>
3. <span data-ttu-id="bc2a8-245">İsteğe bağlı olarak sağlayan bir **neden** veya **açıklama**.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-245">Optionally provide a **Reason** or **Comment**.</span></span>
4. <span data-ttu-id="bc2a8-246">hello geçerli öğe için toodelete hello yedekleme verileri tıklatın ![Dur yedekleme düğmesi](./media/backup-azure-manage-vms/delete-button.png)</span><span class="sxs-lookup"><span data-stu-id="bc2a8-246">toodelete hello backup data for hello current item, click  ![Stop backup button](./media/backup-azure-manage-vms/delete-button.png)</span></span>

    <span data-ttu-id="bc2a8-247">Bir bildirim iletisi, hello yedekleme verileri silinir bilmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="bc2a8-247">A notification message lets you know hello backup data has been deleted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc2a8-248">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bc2a8-248">Next steps</span></span>
<span data-ttu-id="bc2a8-249">Bir sanal makine bir kurtarma noktasından yeniden oluşturma hakkında daha fazla bilgi için kullanıma [geri Azure Vm'leri](backup-azure-restore-vms.md).</span><span class="sxs-lookup"><span data-stu-id="bc2a8-249">For information on re-creating a virtual machine from a recovery point, check out [Restore Azure VMs](backup-azure-restore-vms.md).</span></span> <span data-ttu-id="bc2a8-250">Sanal makinelerinizi koruma bilgi gerekirse bkz [ilk bakış: geri kurtarma Hizmetleri kasası VM'ler tooa yukarı](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="bc2a8-250">If you need information on protecting your virtual machines, see [First look: Back up VMs tooa Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span> <span data-ttu-id="bc2a8-251">Olayları izleme hakkında daha fazla bilgi için bkz: [izlemek için Azure sanal makine yedeklerini uyarıları](backup-azure-monitor-vms.md).</span><span class="sxs-lookup"><span data-stu-id="bc2a8-251">For information on monitoring events, see [Monitor alerts for Azure virtual machine backups](backup-azure-monitor-vms.md).</span></span>
