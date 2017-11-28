---
title: "aaaManage ve İzleyici Azure sanal makine yedeklerini | Microsoft Docs"
description: "Yedeklemeleri nasıl toomanage ve izleyici bir Azure sanal makine öğrenin"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 4372944e-d33a-4f6a-bd5f-d04af2842713
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: trinadhk;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cb95e0b3760c96f7fd563c42cb4c635553f48957
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-common-azure-backup-jobs-and-trigger-alerts-in-hello-classic-portal"></a><span data-ttu-id="76199-103">Ortak Azure yedekleme işleri ve tetikleyici uyarıları hello Klasik portalda yönetin</span><span class="sxs-lookup"><span data-stu-id="76199-103">Manage common Azure Backup jobs and trigger alerts in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="76199-104">Azure VM yedeklemeleri yönetme</span><span class="sxs-lookup"><span data-stu-id="76199-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="76199-105">Klasik VM yedeklemeleri yönetme</span><span class="sxs-lookup"><span data-stu-id="76199-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="76199-106">Bu makale ortak yönetim ve izleme görevlerini Azure'da korunan Klasik modeli sanal makineler için hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="76199-106">This article provides information about common management and monitoring tasks for Classic-model virtual machines protected in Azure.</span></span>  

> [!NOTE]
> <span data-ttu-id="76199-107">Azure'da kaynak oluşturmaya ve kaynaklarla çalışmaya yönelik iki dağıtım modeli mevcuttur: [Resource Manager ve Klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="76199-107">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="76199-108">Bkz: [Azure sanal makineleri yedeklemek, ortam tooback hazırlama](backup-azure-vms-prepare.md) Klasik dağıtımı ile çalışma hakkında ayrıntılar için model VM'ler.</span><span class="sxs-lookup"><span data-stu-id="76199-108">See [Prepare your environment tooback up Azure virtual machines](backup-azure-vms-prepare.md) for details on working with Classic deployment model VMs.</span></span>
>
> [!IMPORTANT]
><span data-ttu-id="76199-109">Mart 2017'dan başlayarak, hello Klasik portal toocreate yedekleme kasaları artık kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76199-109">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
>
> <span data-ttu-id="76199-110">Şimdi, yedekleme kasaları tooRecovery Hizmetleri kasaları yükseltebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76199-110">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="76199-111">Ayrıntılar için hello makalesine bakın [kurtarma Hizmetleri kasası bir yedekleme kasası tooa yükseltme](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="76199-111">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="76199-112">Microsoft tooupgrade önerir tooRecovery Hizmetleri kasalarının yedekleme kasaları.</span><span class="sxs-lookup"><span data-stu-id="76199-112">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="76199-113">15 Ekim 2017 sonra PowerShell toocreate yedekleme kasaları kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="76199-113">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="76199-114">**1 Kasım 2017’ye kadar**:</span><span class="sxs-lookup"><span data-stu-id="76199-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="76199-115">Kalan tüm yedekleme kasaları otomatik olarak yükseltilen tooRecovery Hizmetleri kasalarının olacaktır.</span><span class="sxs-lookup"><span data-stu-id="76199-115">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="76199-116">Mümkün tooaccess hello Klasik Portalı'nda, yedekleme verilerinizi olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="76199-116">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="76199-117">Bunun yerine, hello Azure portal tooaccess kurtarma Hizmetleri kasalarının, yedekleme verilerinizi kullanın.</span><span class="sxs-lookup"><span data-stu-id="76199-117">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>

## <a name="manage-protected-virtual-machines"></a><span data-ttu-id="76199-118">Korumalı sanal makineleri yönetme</span><span class="sxs-lookup"><span data-stu-id="76199-118">Manage protected virtual machines</span></span>
<span data-ttu-id="76199-119">toomanage korunan sanal makineler:</span><span class="sxs-lookup"><span data-stu-id="76199-119">toomanage protected virtual machines:</span></span>

1. <span data-ttu-id="76199-120">tooview ve bir sanal makineye tıklayın için hello Yedekleme ayarlarını yönetmeyi **korunan öğeler** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="76199-120">tooview and manage backup settings for a virtual machine click hello **Protected Items** tab.</span></span>
2. <span data-ttu-id="76199-121">Korumalı öğe toosee hello hello adını tıklatın **yedekleme ayrıntıları** sekmesinde hello son yedekleme hakkında bilgi gösterir.</span><span class="sxs-lookup"><span data-stu-id="76199-121">Click on hello name of a protected item toosee hello **Backup Details** tab, which shows you information about hello last backup.</span></span>

    ![Sanal makine yedekleme](./media/backup-azure-manage-vms/backup-vmdetails.png)
3. <span data-ttu-id="76199-123">tooview ve bir sanal makineye tıklayın için hello yedekleme İlkesi ayarları yönetmek **ilkeleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="76199-123">tooview and manage backup policy settings for a virtual machine click hello **Policies** tab.</span></span>

    ![Sanal Makine ilkesi](./media/backup-azure-manage-vms/manage-policy-settings.png)

    <span data-ttu-id="76199-125">Merhaba **yedekleme ilkeleri** sekmesinde varolan ilke hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="76199-125">hello **Backup Policies** tab shows you hello existing policy.</span></span> <span data-ttu-id="76199-126">Gerektiği şekilde değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76199-126">You can modify as needed.</span></span> <span data-ttu-id="76199-127">Toocreate yeni bir ilke gerekiyorsa tıklatın **oluşturma** hello üzerinde **ilkeleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="76199-127">If you need toocreate a new policy click **Create** on hello **Policies** page.</span></span> <span data-ttu-id="76199-128">Tooremove istiyorsanız, bir ilke, kendisiyle ilişkilendirilmiş herhangi bir sanal makine olmamalıdır olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="76199-128">Note that if you want tooremove a policy it shouldn't have any virtual machines associated with it.</span></span>

    ![Sanal Makine ilkesi](./media/backup-azure-manage-vms/backup-vmpolicy.png)
4. <span data-ttu-id="76199-130">Merhaba üzerinde bir sanal makine için Eylemler veya durumu hakkında daha fazla bilgi edinebilirsiniz **işleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="76199-130">You can get more information about actions or status for a virtual machine on hello **Jobs** page.</span></span> <span data-ttu-id="76199-131">Bir işi hello listesi tooget daha fazla ayrıntı veya filtre işleri belirli bir sanal makine için tıklayın.</span><span class="sxs-lookup"><span data-stu-id="76199-131">Click a job in hello list tooget more details, or filter jobs for a specific virtual machine.</span></span>

    ![İşler](./media/backup-azure-manage-vms/backup-job.png)

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="76199-133">Bir sanal makinenin talep üzerine yedekleme</span><span class="sxs-lookup"><span data-stu-id="76199-133">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="76199-134">Koruma için yapılandırıldıktan sonra isteğe bağlı bir sanal makine yedekleme devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="76199-134">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="76199-135">Merhaba ilk yedekleme bekleme durumundaysa hello sanal makine için talep üzerine yedekleme Azure yedekleme kasasında hello sanal makinenin tam bir kopyasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="76199-135">If hello initial backup is pending for hello virtual machine, on-demand backup will create a full copy of hello virtual machine in Azure backup vault.</span></span> <span data-ttu-id="76199-136">İlk yedekleme tamamlandığında, gönderme değişikliklerden önceki yedekleme tooAzure yedekleme yani kasa yalnızca talep üzerine yedekleme her zaman artımlıdır.</span><span class="sxs-lookup"><span data-stu-id="76199-136">If first backup is completed, on-demand backup will only send changes from previous backup tooAzure backup vault i.e. it is always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="76199-137">Bir talep üzerine yedekleme bekletme aralığını, yedekleme İlkesi karşılık gelen toohello VM içinde günlük bekletme için belirtilen tooretention değer ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="76199-137">Retention range of an on-demand backup is set tooretention value specified for Daily retention in backup policy corresponding toohello VM.</span></span>  
>
>

<span data-ttu-id="76199-138">bir sanal makinenin yedeğini tootake isteğe bağlı:</span><span class="sxs-lookup"><span data-stu-id="76199-138">tootake an on-demand backup of a virtual machine:</span></span>

1. <span data-ttu-id="76199-139">Toohello gidin **korunan öğeler** sayfasından seçim yapıp **Azure sanal makine** olarak **türü** (henüz seçili değilse) ve tıklayın **seçin**düğmesi.</span><span class="sxs-lookup"><span data-stu-id="76199-139">Navigate toohello **Protected Items** page and select **Azure Virtual Machine** as **Type** (if not already selected) and click on **Select** button.</span></span>

    ![VM türü](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="76199-141">Tootake isteğe bağlı yedekleme istediğiniz ve tıklayın Hello sanal makine seçin **şimdi yedek** hello altındaki hello sayfasının düğmesini.</span><span class="sxs-lookup"><span data-stu-id="76199-141">Select hello virtual machine on which you want tootake an on-demand backup and click on **Backup Now** button at hello bottom of hello page.</span></span>

    ![Şimdi Yedekle](./media/backup-azure-manage-vms/backup-now.png)

    <span data-ttu-id="76199-143">Bu seçili hello sanal makineye bir yedekleme işi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="76199-143">This will create a backup job on hello selected virtual machine.</span></span> <span data-ttu-id="76199-144">Bu iş oluşturulan kurtarma noktası bekletme aralığı hello sanal makineyle ilişkili hello İlkesi'nde belirtilen aynı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="76199-144">Retention range of recovery point created through this job will be same as that specified in hello policy associated with hello virtual machine.</span></span>

    ![Yedekleme işi oluşturma](./media/backup-azure-manage-vms/creating-job.png)

   > [!NOTE]
   > <span data-ttu-id="76199-146">içine hello sanal makinede aşağı ayrıntıya bir sanal makineyle ilişkili tooview hello İlkesi **korunan öğeler** sayfası ve Git toobackup ilke sekmesi.</span><span class="sxs-lookup"><span data-stu-id="76199-146">tooview hello policy associated with a virtual machine, drill down into virtual machine in hello **Protected Items** page and go toobackup policy tab.</span></span>
   >
   >
3. <span data-ttu-id="76199-147">Merhaba işi oluşturulduktan sonra tıklatabilirsiniz **işi görüntüle** hello bildirim toosee hello karşılık gelen iş hello işleri sayfasında çubuğu düğmesini.</span><span class="sxs-lookup"><span data-stu-id="76199-147">Once hello job is created, you can click on **View job** button in hello toast bar toosee hello corresponding job in hello jobs page.</span></span>

    ![Yedekleme işi oluşturuldu](./media/backup-azure-manage-vms/created-job.png)
4. <span data-ttu-id="76199-149">Merhaba iş başarıyla tamamlandıktan sonra bir kurtarma noktası kullanabileceğiniz oluşturulacak toorestore hello sanal makine.</span><span class="sxs-lookup"><span data-stu-id="76199-149">After successful completion of hello job, a recovery point will be created which you can use toorestore hello virtual machine.</span></span> <span data-ttu-id="76199-150">Bu ayrıca hello kurtarma noktası sütun değeri 1'tarafından artırır **korunan öğeler** sayfası.</span><span class="sxs-lookup"><span data-stu-id="76199-150">This will also increment hello recovery point column value by 1 in **Protected Items** page.</span></span>

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="76199-151">Sanal makineleri koruma Durdur</span><span class="sxs-lookup"><span data-stu-id="76199-151">Stop protecting virtual machines</span></span>
<span data-ttu-id="76199-152">Seçenekler aşağıdaki hello ile Merhaba gelecekteki bir sanal makine yedeklerini toostop seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="76199-152">You can choose toostop hello future backups of a virtual machine with hello following options:</span></span>

* <span data-ttu-id="76199-153">Azure yedekleme kasasında sanal makineyle ilişkili yedekleme verilerini korur</span><span class="sxs-lookup"><span data-stu-id="76199-153">Retain backup data associated with virtual machine in Azure Backup vault</span></span>
* <span data-ttu-id="76199-154">Sanal makine ile ilişkili yedekleme verilerini sil</span><span class="sxs-lookup"><span data-stu-id="76199-154">Delete backup data associated with virtual machine</span></span>

<span data-ttu-id="76199-155">Sanal makine ile ilişkili tooretain yedekleme verilerini seçtiyseniz, hello yedekleme verilerini toorestore hello sanal makine kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76199-155">If you have selected tooretain backup data associated with virtual machine, you can use hello backup data toorestore hello virtual machine.</span></span> <span data-ttu-id="76199-156">Bu tür sanal makineler için ayrıntıları fiyatlandırma için tıklatın [burada](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="76199-156">For pricing details for such virtual machines, click [here](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="76199-157">bir sanal makine için korumayı tooStop:</span><span class="sxs-lookup"><span data-stu-id="76199-157">tooStop protection for a virtual machine:</span></span>

1. <span data-ttu-id="76199-158">Çok gidin**korunan öğeler** sayfasından seçim yapıp **Azure sanal makinesi** (henüz seçili değilse) hello filtre türü ve'ı tıklatın **seçin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="76199-158">Navigate too**Protected Items** page and select **Azure virtual machine** as hello filter type (if not already selected) and click on **Select** button.</span></span>

    ![VM türü](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="76199-160">Merhaba sanal makineyi seçin ve tıklayın **korumayı Durdur** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="76199-160">Select hello virtual machine and click on **Stop Protection** at hello bottom of hello page.</span></span>

    ![Korumayı Durdur](./media/backup-azure-manage-vms/stop-protection.png)
3. <span data-ttu-id="76199-162">Varsayılan olarak, Azure Backup hello sanal makineyle ilişkili hello yedekleme verileri silmez.</span><span class="sxs-lookup"><span data-stu-id="76199-162">By default, Azure Backup doesn’t delete hello backup data associated with hello virtual machine.</span></span>

    ![Durdurma onaylayın](./media/backup-azure-manage-vms/confirm-stop-protection.png)

    <span data-ttu-id="76199-164">Toodelete yedekleme verilerini istiyorsanız hello onay kutusunu seçin.</span><span class="sxs-lookup"><span data-stu-id="76199-164">If you want toodelete backup data, select hello check box.</span></span>

    ![Onay kutusu](./media/backup-azure-manage-vms/checkbox.png)

    <span data-ttu-id="76199-166">Lütfen hello yedeklemeyi durdurma nedeni seçin.</span><span class="sxs-lookup"><span data-stu-id="76199-166">Please select a reason for stopping hello backup.</span></span> <span data-ttu-id="76199-167">Bu isteğe bağlı olmakla birlikte, bir nedeni sağlama hello görüşler Azure Backup toowork yardımcı olmak ve hello müşteri senaryoları öncelik.</span><span class="sxs-lookup"><span data-stu-id="76199-167">While this is optional, providing a reason will help Azure Backup toowork on hello feedback and prioritize hello customer scenarios.</span></span>
4. <span data-ttu-id="76199-168">Tıklayın **gönderme** düğmesini toosubmit hello **korumayı** işi.</span><span class="sxs-lookup"><span data-stu-id="76199-168">Click on **Submit** button toosubmit hello **Stop protection** job.</span></span> <span data-ttu-id="76199-169">Tıklayın **işi görüntüle** toosee hello karşılık gelen hello işinde **işleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="76199-169">Click on **View Job** toosee hello corresponding hello job in **Jobs** page.</span></span>

    ![Korumayı Durdur](./media/backup-azure-manage-vms/stop-protect-success.png)

    <span data-ttu-id="76199-171">Değil seçtiyseniz **Delete ilişkilendirilmiş yedekleme verileri** sırasında seçeneği **korumayı Durdur** sihirbazını sonra post iş tamamlandığında, koruma durumu değişir çok**koruması durdurulmuş**.</span><span class="sxs-lookup"><span data-stu-id="76199-171">If you have not selected **Delete associated backup data** option during **Stop Protection** wizard, then post job completion, protection status changes too**Protection Stopped**.</span></span> <span data-ttu-id="76199-172">açıkça silinene kadar hello verileri Azure yedekleme ile kalır.</span><span class="sxs-lookup"><span data-stu-id="76199-172">hello data remains with Azure Backup until it is explicitly deleted.</span></span> <span data-ttu-id="76199-173">Hello hello sanal makine seçerek hello verileri her zaman silebilir **korunan öğeler** sayfa ve tıklayarak **silmek**.</span><span class="sxs-lookup"><span data-stu-id="76199-173">You can always delete hello data by selecting hello virtual machine in hello **Protected Items** page and clicking **Delete**.</span></span>

    ![Durdurulan koruma](./media/backup-azure-manage-vms/protection-stopped-status.png)

    <span data-ttu-id="76199-175">Merhaba seçtiyseniz **Delete ilişkilendirilmiş yedekleme verileri** seçeneği, hello sanal makine hello parçası olmayacaktır **korunan öğeler** sayfası.</span><span class="sxs-lookup"><span data-stu-id="76199-175">If you have selected hello **Delete associated backup data** option, hello virtual machine won’t be part of hello **Protected Items** page.</span></span>

## <a name="re-protect-virtual-machine"></a><span data-ttu-id="76199-176">Sanal makine yeniden koruma</span><span class="sxs-lookup"><span data-stu-id="76199-176">Re-protect Virtual machine</span></span>
<span data-ttu-id="76199-177">Merhaba seçmediyseniz **ilişkilendirme yedekleme verileri silmek** seçeneğini **korumayı Durdur**, hello sanal makine izleyerek yeniden Koruyabileceğiniz hello adımları benzer toobacking yukarı kayıtlı sanal makineler.</span><span class="sxs-lookup"><span data-stu-id="76199-177">If you have not selected hello **Delete associate backup data** option in **Stop Protection**, you can re-protect hello virtual machine by following hello steps similar toobacking up registered virtual machines.</span></span> <span data-ttu-id="76199-178">Korumalı, bu sanal makine korunur yedek veri önceki toostop korumasına sahip olur ve sonra kurtarma noktaları oluşturulur sonra yeniden koruyun.</span><span class="sxs-lookup"><span data-stu-id="76199-178">Once protected, this virtual machine will have backup data retained prior toostop protection and recovery points created after re-protect.</span></span>

<span data-ttu-id="76199-179">Yeniden koruma sonra hello sanal makinenin koruma durumu çok değiştirilecek**korumalı** varsa Kurtarma noktaları önceki çok**korumayı Durdur**.</span><span class="sxs-lookup"><span data-stu-id="76199-179">After re-protect, hello virtual machine’s protection status will be changed too**Protected** if there are recovery points prior too**Stop Protection**.</span></span>

  ![Korunmuş VM](./media/backup-azure-manage-vms/reprotected-status.png)

> [!NOTE]
> <span data-ttu-id="76199-181">Merhaba sanal makine yeniden korurken, başka bir ilke ile sanal makine başlangıçta korunan hello ilkesinden seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76199-181">When re-protecting hello virtual machine, you can choose a different policy than hello policy with which virtual machine was protected initially.</span></span>
>
>

## <a name="unregister-virtual-machines"></a><span data-ttu-id="76199-182">Sanal makineler kaydı</span><span class="sxs-lookup"><span data-stu-id="76199-182">Unregister virtual machines</span></span>
<span data-ttu-id="76199-183">Merhaba yedekleme kasası tooremove hello sanal makineden istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="76199-183">If you want tooremove hello virtual machine from hello backup vault:</span></span>

1. <span data-ttu-id="76199-184">Tıklatın hello üzerinde **UNREGISTER** hello altındaki hello sayfasının düğmesini.</span><span class="sxs-lookup"><span data-stu-id="76199-184">Click on hello **UNREGISTER** button at hello bottom of hello page.</span></span>

    ![Korumayı devre dışı bırakın](./media/backup-azure-manage-vms/unregister-button.png)

    <span data-ttu-id="76199-186">Bir bildirim hello onaylamanızı isteyen hello ekranının altında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="76199-186">A toast notification will appear at hello bottom of hello screen requesting confirmation.</span></span> <span data-ttu-id="76199-187">Tıklatın **Evet** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="76199-187">Click **YES** toocontinue.</span></span>

    ![Korumayı devre dışı bırakın](./media/backup-azure-manage-vms/confirm-unregister.png)

## <a name="delete-backup-data"></a><span data-ttu-id="76199-189">Yedekleme verilerini sil</span><span class="sxs-lookup"><span data-stu-id="76199-189">Delete Backup data</span></span>
<span data-ttu-id="76199-190">Ya da bir sanal makineyle ilişkili hello yedekleme verileri silebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="76199-190">You can delete hello backup data associated with a virtual machine, either:</span></span>

* <span data-ttu-id="76199-191">Korumayı Durdur işini sırasında</span><span class="sxs-lookup"><span data-stu-id="76199-191">During Stop Protection Job</span></span>
* <span data-ttu-id="76199-192">Bir sanal makinede durdurma sonra iş tamamlandı</span><span class="sxs-lookup"><span data-stu-id="76199-192">After a stop protection job is completed on a virtual machine</span></span>

<span data-ttu-id="76199-193">hello olan bir sanal makine, yedekleme verilerini toodelete *koruması durdurulmuş* durumu başarılı şekilde tamamlandığını sonrası bir **durdurmak yedekleme** iş:</span><span class="sxs-lookup"><span data-stu-id="76199-193">toodelete backup data on a virtual machine, which is in hello *Protection Stopped* state post successful completion of a **Stop Backup** job:</span></span>

1. <span data-ttu-id="76199-194">Toohello gidin **korunan öğeler** sayfasından seçim yapıp **Azure sanal makine** olarak *türü* hello tıklatıp **seçin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="76199-194">Navigate toohello **Protected Items** page and select **Azure Virtual Machine** as *type* and click hello **Select** button.</span></span>

    ![VM türü](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="76199-196">Merhaba sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="76199-196">Select hello virtual machine.</span></span> <span data-ttu-id="76199-197">Merhaba sanal makine olacak **koruması durdurulmuş** durumu.</span><span class="sxs-lookup"><span data-stu-id="76199-197">hello virtual machine will be in **Protection Stopped** state.</span></span>

    ![Koruma durduruldu](./media/backup-azure-manage-vms/protection-stopped-b.png)
3. <span data-ttu-id="76199-199">Merhaba tıklatın **silmek** hello altındaki hello sayfasının düğmesini.</span><span class="sxs-lookup"><span data-stu-id="76199-199">Click hello **DELETE** button at hello bottom of hello page.</span></span>

    ![Yedek Sil](./media/backup-azure-manage-vms/delete-backup.png)
4. <span data-ttu-id="76199-201">Merhaba, **yedekleme verileri Sil** Sihirbazı'nı (önemle önerilir) yedekleme verilerini silmek için bir neden seçin ve tıklatın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="76199-201">In hello **Delete backup data** wizard, select a reason for deleting backup data (highly recommended) and click **Submit**.</span></span>

    ![Yedekleme verilerini sil](./media/backup-azure-manage-vms/delete-backup-data.png)
5. <span data-ttu-id="76199-203">Bu, seçilen sanal makinenin iş toodelete yedekleme verilerini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="76199-203">This will create a job toodelete backup data of selected virtual machine.</span></span> <span data-ttu-id="76199-204">Tıklatın **işi görüntüle** toosee karşılık gelen iş işleri sayfasında.</span><span class="sxs-lookup"><span data-stu-id="76199-204">Click **View job** toosee corresponding job in Jobs page.</span></span>

    ![Veri silme başarılı](./media/backup-azure-manage-vms/delete-data-success.png)

    <span data-ttu-id="76199-206">Merhaba iş tamamlandıktan sonra karşılık gelen toohello sanal makine kaldırılacak girişi hello **korunan öğeler** sayfası.</span><span class="sxs-lookup"><span data-stu-id="76199-206">Once hello job is completed, hello entry corresponding toohello virtual machine will be removed from **Protected items** page.</span></span>

## <a name="dashboard"></a><span data-ttu-id="76199-207">Pano</span><span class="sxs-lookup"><span data-stu-id="76199-207">Dashboard</span></span>
<span data-ttu-id="76199-208">Merhaba üzerinde **Pano** sayfa Azure sanal makineler, depolama ve hello son 24 saat ilişkili işleri hakkındaki bilgileri gözden geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76199-208">On hello **Dashboard** page you can review information about Azure virtual machines, their storage, and jobs associated with them in hello last 24 hours.</span></span> <span data-ttu-id="76199-209">Yedekleme durumu ve ilişkili yedekleme hataları görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76199-209">You can view backup status and any associated backup errors.</span></span>

![Pano](./media/backup-azure-manage-vms/dashboard-protectedvms.png)

> [!NOTE]
> <span data-ttu-id="76199-211">Merhaba Pano değerleri her 24 saatte bir yenilenir.</span><span class="sxs-lookup"><span data-stu-id="76199-211">Values in hello dashboard are refreshed once every 24 hours.</span></span>
>
>

## <a name="auditing-operations"></a><span data-ttu-id="76199-212">Denetim işlemleri</span><span class="sxs-lookup"><span data-stu-id="76199-212">Auditing Operations</span></span>
<span data-ttu-id="76199-213">Azure backup hello "tam olarak hangi yönetim işlemlerini hello yedekleme kasası üzerinde gerçekleştirilen kolay toosee kolaylaştırarak hello müşteri tarafından tetiklenen işlem günlüklerinin" yedekleme işlemleri incelenmesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="76199-213">Azure backup provides review of hello "operation logs" of backup operations triggered by hello customer making it easy toosee exactly what management operations were performed on hello backup vault.</span></span> <span data-ttu-id="76199-214">İşlem günlükleri proje harika Sonrası-Değerlendirme etkinleştirmek ve hello yedekleme işlemleri için destek denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76199-214">Operations logs enable great post-mortem and audit support for hello backup operations.</span></span>

<span data-ttu-id="76199-215">hello işlem aşağıdaki işlem günlüklerine kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="76199-215">hello following operations are logged in Operation logs:</span></span>

* <span data-ttu-id="76199-216">Kaydolma</span><span class="sxs-lookup"><span data-stu-id="76199-216">Register</span></span>
* <span data-ttu-id="76199-217">Kaydı Kaldır</span><span class="sxs-lookup"><span data-stu-id="76199-217">Unregister</span></span>
* <span data-ttu-id="76199-218">Koruma yapılandırma</span><span class="sxs-lookup"><span data-stu-id="76199-218">Configure protection</span></span>
* <span data-ttu-id="76199-219">Yedekleme (Bu her ikisi de talep üzerine yedekleme BackupNow aracılığıyla yanı sıra zamanlanmış)</span><span class="sxs-lookup"><span data-stu-id="76199-219">Backup ( Both scheduled as well as on-demand backup through BackupNow)</span></span>
* <span data-ttu-id="76199-220">Geri Yükleme</span><span class="sxs-lookup"><span data-stu-id="76199-220">Restore</span></span>
* <span data-ttu-id="76199-221">Korumayı Durdur</span><span class="sxs-lookup"><span data-stu-id="76199-221">Stop protection</span></span>
* <span data-ttu-id="76199-222">Yedekleme verilerini sil</span><span class="sxs-lookup"><span data-stu-id="76199-222">Delete backup data</span></span>
* <span data-ttu-id="76199-223">İlke ekleme</span><span class="sxs-lookup"><span data-stu-id="76199-223">Add policy</span></span>
* <span data-ttu-id="76199-224">İlkeyi Sil</span><span class="sxs-lookup"><span data-stu-id="76199-224">Delete policy</span></span>
* <span data-ttu-id="76199-225">Güncelleştirme ilkesi</span><span class="sxs-lookup"><span data-stu-id="76199-225">Update policy</span></span>
* <span data-ttu-id="76199-226">İşi iptal et</span><span class="sxs-lookup"><span data-stu-id="76199-226">Cancel job</span></span>

<span data-ttu-id="76199-227">tooview işlemi karşılık gelen tooa yedekleme kasası kaydeder:</span><span class="sxs-lookup"><span data-stu-id="76199-227">tooview operation logs corresponding tooa backup vault:</span></span>

1. <span data-ttu-id="76199-228">Çok gidin**Yönetim Hizmetleri** Azure portalında ve hello ardından **işlem günlükleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="76199-228">Navigate too**Management services** in Azure portal, and then click hello **Operation Logs** tab.</span></span>

    ![İşlem günlükleri](./media/backup-azure-manage-vms/ops-logs.png)
2. <span data-ttu-id="76199-230">Merhaba filtreleri seçin **yedekleme** olarak *türü* ve hello yedekleme kasasının adını belirtin *hizmet adı* ve tıklayın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="76199-230">In hello filters, select **Backup** as *Type* and specify hello backup vault name in *service name* and click on **Submit**.</span></span>

    ![İşlem günlükleri filtresi](./media/backup-azure-manage-vms/ops-logs-filter.png)
3. <span data-ttu-id="76199-232">Merhaba işlem günlükleri, herhangi bir işlem seçin ve tıklatın **ayrıntıları** toosee ayrıntıları karşılık gelen tooan işlemi.</span><span class="sxs-lookup"><span data-stu-id="76199-232">In hello operations logs, select any operation and click  **Details** toosee details corresponding tooan operation.</span></span>

    ![İşlem günlükleri getirme ayrıntıları](./media/backup-azure-manage-vms/ops-logs-details.png)

    <span data-ttu-id="76199-234">Merhaba **ayrıntıları Sihirbazı** hello işlemi tetiklenen, iş kimliği, üzerinde bu işlemi tetiklenir ve hello işlem başlatışınızda kaynak hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="76199-234">hello **Details wizard** contains information about hello operation triggered, job Id, resource on which this operation is triggered, and start time of hello operation.</span></span>

    ![İşlem ayrıntıları](./media/backup-azure-manage-vms/ops-logs-details-window.png)

## <a name="alert-notifications"></a><span data-ttu-id="76199-236">Uyarı bildirimleri</span><span class="sxs-lookup"><span data-stu-id="76199-236">Alert notifications</span></span>
<span data-ttu-id="76199-237">Portalda hello işleri için özel uyarı bildirimleri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76199-237">You can get custom alert notifications for hello jobs in portal.</span></span> <span data-ttu-id="76199-238">Bu işlem günlüklerini olaylarına PowerShell'i dayalı olarak uyarı kuralları tanımlayarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="76199-238">This is achieved by defining PowerShell-based alert rules on operational logs events.</span></span> <span data-ttu-id="76199-239">Kullanmanızı öneririz *PowerShell sürüm 1.3.0 veya yukarıdaki*.</span><span class="sxs-lookup"><span data-stu-id="76199-239">We recommend using *PowerShell version 1.3.0 or above*.</span></span>

<span data-ttu-id="76199-240">toodefine özel bildirim tooalert yedekleme hataları için bir örnek komut gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="76199-240">toodefine a custom notification tooalert for backup failures, a sample command will look like:</span></span>

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.Backup/backupVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/microsoft.backupbvtd2/BackupVault/trinadhVault -Actions $actionEmail
```

<span data-ttu-id="76199-241">**ResourceId**: Bu işlem günlükleri açılır penceresinden bölümde açıklandığı gibi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76199-241">**ResourceId**: You can get this from Operations Logs popup as described in above section.</span></span> <span data-ttu-id="76199-242">ResourceUri bir işlemin ayrıntıları açılan penceresinde hello ResourceId toobe Bu cmdlet için sağlanan ' dir.</span><span class="sxs-lookup"><span data-stu-id="76199-242">ResourceUri in details popup window of an operation is hello ResourceId toobe supplied for this cmdlet.</span></span>

<span data-ttu-id="76199-243">**OperationName**: Bu hello biçimi olacaktır "Microsoft.Backup/backupvault/<EventName>" EventName kayıt, Unregister, ConfigureProtection, yedekleme, geri yükleme, StopProtection, DeleteBackupData, biri olduğu CreateProtectionPolicy, DeleteProtectionPolicy, UpdateProtectionPolicy</span><span class="sxs-lookup"><span data-stu-id="76199-243">**OperationName**: This will be of hello format "Microsoft.Backup/backupvault/<EventName>" where EventName is one of Register,Unregister,ConfigureProtection,Backup,Restore,StopProtection,DeleteBackupData,CreateProtectionPolicy,DeleteProtectionPolicy,UpdateProtectionPolicy</span></span>

<span data-ttu-id="76199-244">**Durum**: değerlerini olduğunuz-başlatıldı, desteklenen başarılı ve başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="76199-244">**Status**: Supported values are- Started, Succeeded and Failed.</span></span>

<span data-ttu-id="76199-245">**Kaynak grubu**: ResourceGroup hello kaynağın işlemi başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="76199-245">**ResourceGroup**:ResourceGroup of hello resource on which operation is triggered.</span></span> <span data-ttu-id="76199-246">Bu ResourceId değeri elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76199-246">You can obtain this from ResourceId value.</span></span> <span data-ttu-id="76199-247">Alanlar arasında değer */resourceGroups/* ve */providers/* içinde ResourceId değeri hello ResourceGroup değeridir.</span><span class="sxs-lookup"><span data-stu-id="76199-247">Value between fields */resourceGroups/* and */providers/* in ResourceId value is hello value for ResourceGroup.</span></span>

<span data-ttu-id="76199-248">**Ad**: hello uyarı kuralı adı.</span><span class="sxs-lookup"><span data-stu-id="76199-248">**Name**: Name of hello Alert Rule.</span></span>

<span data-ttu-id="76199-249">**CustomEmail**: hello özel e-posta adresi toowhich toosend uyarı bildirimi istediğiniz belirtin</span><span class="sxs-lookup"><span data-stu-id="76199-249">**CustomEmail**: Specify hello custom email address toowhich you want toosend alert notification</span></span>

<span data-ttu-id="76199-250">**SendToServiceOwners**: Bu seçenek uyarı bildirimi tooall yöneticileri ve ortak Yöneticiler hello aboneliğin gönderir.</span><span class="sxs-lookup"><span data-stu-id="76199-250">**SendToServiceOwners**: This option sends alert notification tooall administrators and co-administrators of hello subscription.</span></span> <span data-ttu-id="76199-251">İçinde kullanılabilir **yeni AzureRmAlertRuleEmail** cmdlet'i</span><span class="sxs-lookup"><span data-stu-id="76199-251">It can be used in **New-AzureRmAlertRuleEmail** cmdlet</span></span>

### <a name="limitations-on-alerts"></a><span data-ttu-id="76199-252">Uyarıları sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="76199-252">Limitations on Alerts</span></span>
<span data-ttu-id="76199-253">Olay tabanlı uyarılara tabi toohello aşağıdaki sınırlamalar vardır:</span><span class="sxs-lookup"><span data-stu-id="76199-253">Event-based alerts are subjected toohello following limitations:</span></span>

1. <span data-ttu-id="76199-254">Tüm sanal makinelerde hello yedekleme kasasında uyarıları tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="76199-254">Alerts are triggered on all virtual machines in hello backup vault.</span></span> <span data-ttu-id="76199-255">Sanal makineler bir yedekleme kasasına belirli kümesi için tooget uyarıları özelleştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="76199-255">You cannot customize it tooget alerts for specific set of virtual machines in a backup vault.</span></span>
2. <span data-ttu-id="76199-256">Bu özelliğin önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="76199-256">This feature is in Preview.</span></span> [<span data-ttu-id="76199-257">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="76199-257">Learn more</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. <span data-ttu-id="76199-258">Gelen uyarılar alırsınız "alerts-noreply@mail.windowsazure.com".</span><span class="sxs-lookup"><span data-stu-id="76199-258">You will receive alerts from "alerts-noreply@mail.windowsazure.com".</span></span> <span data-ttu-id="76199-259">Şu anda hello e-posta gönderen değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="76199-259">Currently you can't modify hello email sender.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76199-260">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="76199-260">Next steps</span></span>
* [<span data-ttu-id="76199-261">Azure sanal makineleri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="76199-261">Restore Azure VMs</span></span>](backup-azure-restore-vms.md)
