---
title: "Azure sanal makineleri Klasik dağıtılan tooa yedekleme kasası yukarı aaaBack | Microsoft Docs"
description: "Bul kaydetmek ve sanal makinelerinizi Azure sanal makine yedeklemesi için bu yordamları ile yedekleyin."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "sanal makine yedeklemesi; sanal makineyi geri; Yedekleme ve olağanüstü durum kurtarma; VM yedekleme"
ms.assetid: c0ab5469-65fd-4af5-ae9b-f5d183f82ce8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 048e32d9b2bd5bdd7a125225a71a6d805bb4fbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a><span data-ttu-id="e9525-104">Azure sanal makineleri yedeklemek (Klasik portalı)</span><span class="sxs-lookup"><span data-stu-id="e9525-104">Back up Azure virtual machines (classic portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e9525-105">Sanal makineleri tooRecovery Hizmetleri kasasını yedekleyin</span><span class="sxs-lookup"><span data-stu-id="e9525-105">Back up VMs tooRecovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="e9525-106">Sanal makineleri tooBackup kasasını yedekleyin</span><span class="sxs-lookup"><span data-stu-id="e9525-106">Back up VMs tooBackup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="e9525-107">Bu makale, Klasik dağıtılan Azure sanal makine (VM) tooa yedekleme kasasını yedekleme için hello yordamlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="e9525-107">This article provides hello procedures for backing up a Classic-deployed Azure virtual machine (VM) tooa Backup vault.</span></span> <span data-ttu-id="e9525-108">Bir Azure sanal makinesini yedeklenmeden önce tootake care, gereken bazı görevler vardır.</span><span class="sxs-lookup"><span data-stu-id="e9525-108">There are a few tasks you need tootake care of before you can back up an Azure virtual machine.</span></span> <span data-ttu-id="e9525-109">Bunu, tam hello zaten yapmadıysanız [Önkoşullar](backup-azure-vms-prepare.md) tooprepare, VM'lerin yedeklenmesi için ortamınızı.</span><span class="sxs-lookup"><span data-stu-id="e9525-109">If you haven't already done so, complete hello [prerequisites](backup-azure-vms-prepare.md) tooprepare your environment for backing up your VMs.</span></span>

<span data-ttu-id="e9525-110">Ek bilgi için üzerinde hello makalelerine bakın [azure'da VM yedekleme altyapınızı planlama](backup-azure-vms-introduction.md) ve [Azure sanal makineleri](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="e9525-110">For additional information, see hello articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

> [!NOTE]
> <span data-ttu-id="e9525-111">Azure'da kaynak oluşturmaya ve kaynaklarla çalışmaya yönelik iki dağıtım modeli mevcuttur: [Resource Manager ve Klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e9525-111">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e9525-112">Bir yedekleme kasası yalnızca klasik dağıtılan VM'ler koruyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9525-112">A Backup vault can only protect Classic-deployed VMs.</span></span> <span data-ttu-id="e9525-113">Resource Manager tarafından dağıtılan Vm'leri bir yedekleme kasası ile koruyamazsınız.</span><span class="sxs-lookup"><span data-stu-id="e9525-113">You cannot protect Resource Manager-deployed VMs with a Backup vault.</span></span> <span data-ttu-id="e9525-114">Bkz: [VM'ler tooRecovery Hizmetleri kasasına yedekleme](backup-azure-arm-vms.md) kurtarma Hizmetleri ile çalışma hakkında ayrıntılar için kasaları.</span><span class="sxs-lookup"><span data-stu-id="e9525-114">See [Back up VMs tooRecovery Services vault](backup-azure-arm-vms.md) for details on working with Recovery Services vaults.</span></span>
>
>

<span data-ttu-id="e9525-115">Azure sanal makineleri yedekleme üç anahtar adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="e9525-115">Backing up Azure virtual machines involves three key steps:</span></span>

![Üç adımı tooback Azure Iaas sanal ayarlama](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> <span data-ttu-id="e9525-117">Sanal makineleri yedekleme işlemi, yerel bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="e9525-117">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="e9525-118">Başka bir bölgede bir bölge tooa yedekleme kasasında sanal makineleri yedekleyin olamaz.</span><span class="sxs-lookup"><span data-stu-id="e9525-118">You cannot back up virtual machines in one region tooa backup vault in another region.</span></span> <span data-ttu-id="e9525-119">Her Azure bölgesinde bir yedekleme kasası oluşturmanız gerekir böylece yedeklenecek VM'ler olduğu.</span><span class="sxs-lookup"><span data-stu-id="e9525-119">So, you must create a backup vault in each Azure region, where there are VMs that will be backed up.</span></span>
>
> [!IMPORTANT]
> <span data-ttu-id="e9525-120">Mart 2017'dan başlayarak, hello Klasik portal toocreate yedekleme kasaları artık kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9525-120">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
> <span data-ttu-id="e9525-121">Şimdi, yedekleme kasaları tooRecovery Hizmetleri kasaları yükseltebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9525-121">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="e9525-122">Ayrıntılar için hello makalesine bakın [kurtarma Hizmetleri kasası bir yedekleme kasası tooa yükseltme](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="e9525-122">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="e9525-123">Microsoft tooupgrade önerir tooRecovery Hizmetleri kasalarının yedekleme kasaları.</span><span class="sxs-lookup"><span data-stu-id="e9525-123">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="e9525-124">15 Ekim 2017 sonra PowerShell toocreate yedekleme kasaları kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="e9525-124">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="e9525-125">**1 Kasım 2017’ye kadar**:</span><span class="sxs-lookup"><span data-stu-id="e9525-125">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="e9525-126">Kalan tüm yedekleme kasaları otomatik olarak yükseltilen tooRecovery Hizmetleri kasalarının olacaktır.</span><span class="sxs-lookup"><span data-stu-id="e9525-126">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="e9525-127">Mümkün tooaccess hello Klasik Portalı'nda, yedekleme verilerinizi olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="e9525-127">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="e9525-128">Bunun yerine, hello Azure portal tooaccess kurtarma Hizmetleri kasalarının, yedekleme verilerinizi kullanın.</span><span class="sxs-lookup"><span data-stu-id="e9525-128">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="step-1---discover-azure-virtual-machines"></a><span data-ttu-id="e9525-129">1. adım - Azure sanal makineleri Bul</span><span class="sxs-lookup"><span data-stu-id="e9525-129">Step 1 - Discover Azure virtual machines</span></span>
<span data-ttu-id="e9525-130">Yeni sanal makineleri (VM'ler) eklenen toohello aboneliklere kaydetmeden önce tanımlanır tooensure hello bulma işlemini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e9525-130">tooensure any new virtual machines (VMs) added toohello subscription are identified before registering, run hello discovery process.</span></span> <span data-ttu-id="e9525-131">Merhaba işlem sorgularında Azure hello ek bilgilerle birlikte hello Abonelikteki sanal makinelerin listesini hello bulut hizmeti adı ve hello bölge gibi.</span><span class="sxs-lookup"><span data-stu-id="e9525-131">hello process queries Azure for hello list of virtual machines in hello subscription, along with additional information like hello cloud service name and hello region.</span></span>

1. <span data-ttu-id="e9525-132">İçinde toohello oturum [Klasik portal](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="e9525-132">Sign in toohello [Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="e9525-133">Azure Hizmetleri Hello listesinde tıklayın **kurtarma Hizmetleri** tooopen hello yedekleme ve Site kurtarma kasalarının listesi.</span><span class="sxs-lookup"><span data-stu-id="e9525-133">In hello list of Azure services, click **Recovery Services** tooopen hello list of Backup and Site Recovery vaults.</span></span>
    <span data-ttu-id="e9525-134">![Açık kasası listesi](./media/backup-azure-vms/choose-vault-list.png)</span><span class="sxs-lookup"><span data-stu-id="e9525-134">![Open vault list](./media/backup-azure-vms/choose-vault-list.png)</span></span>
3. <span data-ttu-id="e9525-135">Yedekleme kasaları Hello listesinde hello kasa tooback VM yukarı seçin.</span><span class="sxs-lookup"><span data-stu-id="e9525-135">In hello list of Backup vaults, select hello vault tooback up a VM.</span></span>

    <span data-ttu-id="e9525-136">Bu ise yeni bir kasa hello portalı toohello açılır **Hızlı Başlangıç** sayfası.</span><span class="sxs-lookup"><span data-stu-id="e9525-136">If this is a new vault hello portal opens toohello **Quick Start** page.</span></span>

    ![Kayıtlı Öğeler menüsünü açın](./media/backup-azure-vms/vault-quick-start.png)

    <span data-ttu-id="e9525-138">Merhaba kasası önceden yapılandırılmışsa hello portalı en son kullanılan toohello menüsü açılır.</span><span class="sxs-lookup"><span data-stu-id="e9525-138">If hello vault has previously been configured, hello portal opens toohello most recently used menu.</span></span>
4. <span data-ttu-id="e9525-139">Merhaba kasa menüsünden (Merhaba sayfanın en üstündeki hello) tıklatın **kayıtlı öğeler**.</span><span class="sxs-lookup"><span data-stu-id="e9525-139">From hello vault menu (at hello top of hello page), click **Registered Items**.</span></span>

    ![Kayıtlı Öğeler menüsünü açın](./media/backup-azure-vms/vault-menu.png)
5. <span data-ttu-id="e9525-141">Merhaba gelen **türü** menüsünde, select **Azure sanal makine**.</span><span class="sxs-lookup"><span data-stu-id="e9525-141">From hello **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![İş yükünü seçme](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="e9525-143">Tıklatın **bulma** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="e9525-143">Click **DISCOVER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="e9525-144">![Bul düğmesi](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="e9525-144">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="e9525-145">Merhaba sanal makinelerin tabloya alınması nedeniyle sırada hello bulma işlemi birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="e9525-145">hello discovery process may take a few minutes while hello virtual machines are being tabulated.</span></span> <span data-ttu-id="e9525-146">Merhaba ekranın alt kısmındaki hello işleminin çalıştığını bilmeniz olanak sağlayan hello bir bildirim yoktur.</span><span class="sxs-lookup"><span data-stu-id="e9525-146">There is a notification at hello bottom of hello screen that lets you know that hello process is running.</span></span>

    ![VM'leri bulma](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="e9525-148">Merhaba işlemi tamamlandığında hello bildirim değiştirir.</span><span class="sxs-lookup"><span data-stu-id="e9525-148">hello notification changes when hello process is complete.</span></span> <span data-ttu-id="e9525-149">Merhaba bulma işlemi hello sanal makineleri bulamadı, ilk hello VM'ler mevcut emin olun.</span><span class="sxs-lookup"><span data-stu-id="e9525-149">If hello discovery process did not find hello virtual machines, first ensure hello VMs exist.</span></span> <span data-ttu-id="e9525-150">Hello VM'ler yoksa, hello VM'ler olan içinde hello aynı olun bölge hello yedekleme kasası olarak.</span><span class="sxs-lookup"><span data-stu-id="e9525-150">If hello VMs exist, ensure hello VMs are in hello same region as hello backup vault.</span></span> <span data-ttu-id="e9525-151">Merhaba, VM'ler var olduğundan ve aynı bölgede Merhaba, hello VM'ler değil zaten kayıtlı tooa yedekleme kasası olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e9525-151">If hello VMs exist and are in hello same region, ensure hello VMs are not already registered tooa backup vault.</span></span> <span data-ttu-id="e9525-152">Bir VM atanan tooa yedekleme kasası varsa şu atanan kullanılabilir toobe tooother yedekleme kasalarını değil.</span><span class="sxs-lookup"><span data-stu-id="e9525-152">If a VM is assigned tooa backup vault it is not available toobe assigned tooother backup vaults.</span></span>

    ![Bulma işlemi bitti](./media/backup-azure-vms/discovery-complete.png)

    <span data-ttu-id="e9525-154">Merhaba yeni öğeler bulunan sonra tooStep 2 gidin ve Vm'lerinizi kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e9525-154">Once you have discovered hello new items, go tooStep 2 and register your VMs.</span></span>

## <a name="step-2---register-azure-virtual-machines"></a><span data-ttu-id="e9525-155">2. adım - kayıt Azure sanal makineler</span><span class="sxs-lookup"><span data-stu-id="e9525-155">Step 2 - Register Azure virtual machines</span></span>
<span data-ttu-id="e9525-156">Bir Azure sanal makinesi tooassociate kaydetmek hello Azure Backup hizmeti ile.</span><span class="sxs-lookup"><span data-stu-id="e9525-156">You register an Azure virtual machine tooassociate it with hello Azure Backup service.</span></span> <span data-ttu-id="e9525-157">Bu genellikle tek seferlik bir etkinliktir.</span><span class="sxs-lookup"><span data-stu-id="e9525-157">This is typically a one-time activity.</span></span>

1. <span data-ttu-id="e9525-158">Toohello yedekleme kasasında gidin **kurtarma Hizmetleri** de Azure portal hello ve ardından **kayıtlı öğeler**.</span><span class="sxs-lookup"><span data-stu-id="e9525-158">Navigate toohello backup vault under **Recovery Services** in hello Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="e9525-159">Seçin **Azure sanal makine** hello açılan menüsünden.</span><span class="sxs-lookup"><span data-stu-id="e9525-159">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![İş yükünü seçme](./media/backup-azure-vms/discovery-select-workload.png)
3. <span data-ttu-id="e9525-161">Tıklatın **KAYDETMEK** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="e9525-161">Click **REGISTER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="e9525-162">![Kaydet düğmesi](./media/backup-azure-vms/register-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="e9525-162">![Register button](./media/backup-azure-vms/register-button-only.png)</span></span>
4. <span data-ttu-id="e9525-163">Merhaba, **öğeleri Kaydet** kısayol menüsü, select hello sanal makineleri tooregister istiyor.</span><span class="sxs-lookup"><span data-stu-id="e9525-163">In hello **Register Items** shortcut menu, select hello virtual machines that you want tooregister.</span></span> <span data-ttu-id="e9525-164">İki veya daha fazla sanal makinelerle varsa aynı hello adı, aralarında hello bulut hizmeti toodistinguish kullanın.</span><span class="sxs-lookup"><span data-stu-id="e9525-164">If there are two or more virtual machines with hello same name, use hello cloud service toodistinguish between them.</span></span>

   > [!TIP]
   > <span data-ttu-id="e9525-165">Birden çok sanal makine aynı anda kaydedilebilir.</span><span class="sxs-lookup"><span data-stu-id="e9525-165">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="e9525-166">Seçtiğiniz her sanal makine için bir iş oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e9525-166">A job is created for each virtual machine that you've selected.</span></span>
5. <span data-ttu-id="e9525-167">Tıklatın **işi görüntüle** hello bildirim toogo toohello içinde **işleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="e9525-167">Click **View Job** in hello notification toogo toohello **Jobs** page.</span></span>

    ![İşi kaydetme](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="e9525-169">Merhaba sanal makine hello hello kayıt işleminin hello durumu ile birlikte kayıtlı öğeler listesinde de görünür.</span><span class="sxs-lookup"><span data-stu-id="e9525-169">hello virtual machine also appears in hello list of registered items, along with hello status of hello registration operation.</span></span>

    ![Kayıt durumu 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="e9525-171">Merhaba işlemi tamamlandığında hello tooreflect hello durumuna *kayıtlı* durumu.</span><span class="sxs-lookup"><span data-stu-id="e9525-171">When hello operation completes, hello status changes tooreflect hello *registered* state.</span></span>

    ![Kayıt durumu 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a><span data-ttu-id="e9525-173">3. adım - Azure sanal makinelerini koruma</span><span class="sxs-lookup"><span data-stu-id="e9525-173">Step 3 - Protect Azure virtual machines</span></span>
<span data-ttu-id="e9525-174">Şimdi hello sanal makine için bir yedekleme ve bekletme ilkesi ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9525-174">Now you can set up a backup and retention policy for hello virtual machine.</span></span> <span data-ttu-id="e9525-175">Tek bir kullanarak birden çok sanal makineler korunabilir eylem koruyun.</span><span class="sxs-lookup"><span data-stu-id="e9525-175">Multiple virtual machines can be protected by using a single protect action.</span></span>

<span data-ttu-id="e9525-176">Mayıs 2015 ile birlikte gelir sonra oluşturulan azure yedekleme kasaları varsayılan bir ilke hello kasaya yerleşiktir.</span><span class="sxs-lookup"><span data-stu-id="e9525-176">Azure Backup vaults created after May 2015 come with a default policy built into hello vault.</span></span> <span data-ttu-id="e9525-177">Bu varsayılan ilke, varsayılan saklama 30 gün ve bir kez günlük yedekleme zamanlaması ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="e9525-177">This default policy comes with a default retention of 30 days and a once-daily backup schedule.</span></span>

1. <span data-ttu-id="e9525-178">Toohello yedekleme kasasında gidin **kurtarma Hizmetleri** de Azure portal hello ve ardından **kayıtlı öğeler**.</span><span class="sxs-lookup"><span data-stu-id="e9525-178">Navigate toohello backup vault under **Recovery Services** in hello Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="e9525-179">Seçin **Azure sanal makine** hello açılan menüsünden.</span><span class="sxs-lookup"><span data-stu-id="e9525-179">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![Portalda iş yükünü seçme](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="e9525-181">Tıklatın **koruma** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="e9525-181">Click **PROTECT** at hello bottom of hello page.</span></span>

    <span data-ttu-id="e9525-182">Merhaba **öğeleri koruma Sihirbazı'nı** görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e9525-182">hello **Protect Items wizard** appears.</span></span> <span data-ttu-id="e9525-183">Merhaba sihirbaz yalnızca kayıtlı ve korumalı sanal makineleri listeler.</span><span class="sxs-lookup"><span data-stu-id="e9525-183">hello wizard only lists virtual machines that are registered and not protected.</span></span> <span data-ttu-id="e9525-184">Merhaba sanal makineleri tooprotect istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="e9525-184">Select hello virtual machines that you want tooprotect.</span></span>

    <span data-ttu-id="e9525-185">İki veya daha fazla sanal makinelerle varsa aynı hello adı, hello bulut hizmeti toodistinguish hello sanal makineler arasında kullanın.</span><span class="sxs-lookup"><span data-stu-id="e9525-185">If there are two or more virtual machines with hello same name, use hello cloud service toodistinguish between hello virtual machines.</span></span>

   > [!TIP]
   > <span data-ttu-id="e9525-186">Bir seferde birden fazla sanal makineyi koruyabilir.</span><span class="sxs-lookup"><span data-stu-id="e9525-186">You can protect multiple virtual machines at one time.</span></span>
   >
   >

    ![Korumayı ölçekli olarak yapılandırma](./media/backup-azure-vms/protect-at-scale.png)

4. <span data-ttu-id="e9525-188">Seçin bir **yedekleme zamanlaması** tooback seçtiğiniz hello sanal makineleri ayarlama.</span><span class="sxs-lookup"><span data-stu-id="e9525-188">Choose a **backup schedule** tooback up hello virtual machines that you've selected.</span></span> <span data-ttu-id="e9525-189">Var olan ilkeleri kümesinden seçin veya yeni bir tane tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="e9525-189">You can pick from an existing set of policies or define a new one.</span></span>

    <span data-ttu-id="e9525-190">Her bir yedekleme ilkesi, kendisiyle ilişkili birden çok sanal makineye sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="e9525-190">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="e9525-191">Ancak, hello sanal makine yalnızca zamanında verilen herhangi bir noktada bir ilkesiyle ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="e9525-191">However, hello virtual machine can only be associated with one policy at any given point in time.</span></span>

    ![Yeni ilke ile koruma](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="e9525-193">Bir yedekleme İlkesi hello zamanlanmış yedeklemeler için bir bekletme düzeni içerir.</span><span class="sxs-lookup"><span data-stu-id="e9525-193">A backup policy includes a retention scheme for hello scheduled backups.</span></span> <span data-ttu-id="e9525-194">Mevcut bir yedekleme İlkesi seçerseniz, hello hello sonraki adımda bekletme seçeneklerini değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9525-194">If you select an existing backup policy, you cannot modify hello retention options in hello next step.</span></span>
   >
   >

5. <span data-ttu-id="e9525-195">Seçin bir **bekletme aralığı** tooassociate hello yedeklemeleri ile.</span><span class="sxs-lookup"><span data-stu-id="e9525-195">Choose a **retention range** tooassociate with hello backups.</span></span>

    ![Esnek bekletme ile koruma](./media/backup-azure-vms/policy-retention.png)

    <span data-ttu-id="e9525-197">Bekletme İlkesi hello uzun bir yedeklemenin depolanacağı süreyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="e9525-197">Retention policy specifies hello length of time for storing a backup.</span></span> <span data-ttu-id="e9525-198">Merhaba yedeklemenin ne zaman göre farklı bekletme ilkeleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9525-198">You can specify different retention policies based on when hello backup is taken.</span></span> <span data-ttu-id="e9525-199">Örneğin, (işletimsel kurtarma noktası olarak hizmet veren) günlük mü bir yedekleme noktası 90 gün boyunca korunması.</span><span class="sxs-lookup"><span data-stu-id="e9525-199">For example, a backup point taken daily (which serves as an operational recovery point) might be preserved for 90 days.</span></span> <span data-ttu-id="e9525-200">Buna karşılık, her üç aylık dönem (Denetim amacıyla) hello sonunda alınan bir yedekleme noktasının birçok ay veya yıl korunur toobe gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="e9525-200">In comparison, a backup point taken at hello end of each quarter (for audit purposes) may need toobe preserved for many months or years.</span></span>

    ![Sanal makine, kurtarma noktası ile yedeklenir](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="e9525-202">Bu örnek görüntüde:</span><span class="sxs-lookup"><span data-stu-id="e9525-202">In this example image:</span></span>

   * <span data-ttu-id="e9525-203">**Günlük Bekletme İlkesi**: günlük alınan yedeklemeler 30 gün süreyle depolanır.</span><span class="sxs-lookup"><span data-stu-id="e9525-203">**Daily retention policy**: Backups taken daily are stored for 30 days.</span></span>
   * <span data-ttu-id="e9525-204">**Haftalık Bekletme İlkesi**: her hafta Pazar günü alınan yedeklemeler 104 hafta boyunca korunur.</span><span class="sxs-lookup"><span data-stu-id="e9525-204">**Weekly retention policy**: Backups taken every week on Sunday are preserved for 104 weeks.</span></span>
   * <span data-ttu-id="e9525-205">**Aylık Bekletme İlkesi**: hello üzerinde her ayın son Pazar alınan yedeklemeler için 120 ayda korunur.</span><span class="sxs-lookup"><span data-stu-id="e9525-205">**Monthly retention policy**: Backups taken on hello last Sunday of each month are preserved for 120 months.</span></span>
   * <span data-ttu-id="e9525-206">**Yıllık Bekletme İlkesi**: hello üzerinde her Ocak ilk Pazar alınan yedeklemeler için 99 yıla korunur.</span><span class="sxs-lookup"><span data-stu-id="e9525-206">**Yearly retention policy**: Backups taken on hello first Sunday of every January are preserved for 99 years.</span></span>

     <span data-ttu-id="e9525-207">Bir iş tooconfigure hello koruma ilkesi oluşturulur ve seçtiğiniz her bir sanal makine için hello sanal makineleri toothat İlkesi ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="e9525-207">A job is created tooconfigure hello protection policy and associate hello virtual machines toothat policy for each virtual machine that you've selected.</span></span>
6. <span data-ttu-id="e9525-208">tooview hello listesi **korumayı Yapılandır** hello kasa menüsünden işleri tıklatın **işleri** seçip **korumayı Yapılandır** hello gelen **işlemi**  filtre.</span><span class="sxs-lookup"><span data-stu-id="e9525-208">tooview hello list of **Configure Protection** jobs, from hello vaults menu, click **Jobs** and select **Configure Protection** from hello **Operation** filter.</span></span>

    ![Korumayı yapılandır işi](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a><span data-ttu-id="e9525-210">İlk yedekleme</span><span class="sxs-lookup"><span data-stu-id="e9525-210">Initial backup</span></span>
<span data-ttu-id="e9525-211">Merhaba sanal makine bir ilke ile korunuyor sonra hello altında görünür **korunan öğeler** hello durumunu sekmesiyle *korumalı - (ilk yedekleme bekleniyor)*.</span><span class="sxs-lookup"><span data-stu-id="e9525-211">Once hello virtual machine is protected with a policy, it shows up under hello **Protected Items** tab with hello status of *Protected - (pending initial backup)*.</span></span> <span data-ttu-id="e9525-212">Varsayılan olarak, ilk zamanlanmış yedekleme hello hello olan *ilk yedekleme*.</span><span class="sxs-lookup"><span data-stu-id="e9525-212">By default, hello first scheduled backup is hello *initial backup*.</span></span>

<span data-ttu-id="e9525-213">koruma yapılandırma hemen sonra tootrigger hello ilk yedekleme:</span><span class="sxs-lookup"><span data-stu-id="e9525-213">tootrigger hello initial backup immediately after configuring protection:</span></span>

1. <span data-ttu-id="e9525-214">Merhaba hello sonundaki **korunan öğeler** sayfasında, **Şimdi Yedekle**.</span><span class="sxs-lookup"><span data-stu-id="e9525-214">At hello bottom of hello **Protected Items** page, click **Backup Now**.</span></span>

    <span data-ttu-id="e9525-215">Hello Azure Backup hizmeti hello ilk yedekleme işlemi için bir yedekleme işi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e9525-215">hello Azure Backup service creates a backup job for hello initial backup operation.</span></span>
2. <span data-ttu-id="e9525-216">Hello tıklatın **işleri** sekmesini tooview hello işlerin listesi.</span><span class="sxs-lookup"><span data-stu-id="e9525-216">Click hello **Jobs** tab tooview hello list of jobs.</span></span>

    ![Yedekleme devam ediyor](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> <span data-ttu-id="e9525-218">Merhaba yedekleme işlemi sırasında bir komut toohello yedekleme uzantısına tüm işleri yazma ve tutarlı bir anlık görüntüsünü her sanal makine tooflush hello Azure Backup hizmeti verir.</span><span class="sxs-lookup"><span data-stu-id="e9525-218">During hello backup operation, hello Azure Backup service issues a command toohello backup extension in each virtual machine tooflush all write jobs and take a consistent snapshot.</span></span>
>
>

<span data-ttu-id="e9525-219">Merhaba ilk yedekleme tamamlandığında, hello hello hello sanal makinenin durumunu **korunan öğeler** sekmesi *korumalı*.</span><span class="sxs-lookup"><span data-stu-id="e9525-219">When hello initial backup finishes, hello status of hello virtual machine in hello **Protected Items** tab is *Protected*.</span></span>

![Sanal makine, kurtarma noktası ile yedeklenir](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a><span data-ttu-id="e9525-221">Yedekleme durumu ve ayrıntıları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="e9525-221">Viewing backup status and details</span></span>
<span data-ttu-id="e9525-222">Korumalı sonra hello hello sanal makine sayısı da artar. **Pano** Özet sayfası.</span><span class="sxs-lookup"><span data-stu-id="e9525-222">Once protected, hello virtual machine count also increases in hello **Dashboard** page summary.</span></span> <span data-ttu-id="e9525-223">Merhaba **Pano** sayfası hello son 24 olan saat işlerden hello sayısını da gösterir *başarılı*, sahip *başarısız*ve *devam eden*.</span><span class="sxs-lookup"><span data-stu-id="e9525-223">hello **Dashboard** page also shows hello number of jobs from hello last 24 hours that were *successful*, have *failed*, and are *in progress*.</span></span> <span data-ttu-id="e9525-224">Merhaba üzerinde **işleri** sayfasında, hello kullanın **durum**, **işlemi**, veya **gelen** ve **için** menüleri toofilter Merhaba işler.</span><span class="sxs-lookup"><span data-stu-id="e9525-224">On hello **Jobs** page, use hello **Status**, **Operation**, or **From** and **To** menus toofilter hello jobs.</span></span>

![Pano sayfasındaki yedekleme durumu](./media/backup-azure-vms/dashboard-protectedvms.png)

<span data-ttu-id="e9525-226">Merhaba Pano değerleri her 24 saatte bir yenilenir.</span><span class="sxs-lookup"><span data-stu-id="e9525-226">Values in hello dashboard are refreshed once every 24 hours.</span></span>

## <a name="troubleshooting-errors"></a><span data-ttu-id="e9525-227">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="e9525-227">Troubleshooting errors</span></span>
<span data-ttu-id="e9525-228">Sanal makineniz yedekleme sırasında sorunları içine çalıştırırsanız hello Ara [VM sorun giderme makalesi](backup-azure-vms-troubleshoot.md) Yardım.</span><span class="sxs-lookup"><span data-stu-id="e9525-228">If you run into issues while backing up your virtual machine, look at hello [VM     troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9525-229">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e9525-229">Next steps</span></span>
* [<span data-ttu-id="e9525-230">Sanal makinelerinizi yönetme ve izleme</span><span class="sxs-lookup"><span data-stu-id="e9525-230">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="e9525-231">Sanal makineleri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="e9525-231">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
