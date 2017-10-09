---
title: "İlk Bakış: Azure sanal makinelerini bir yedekleme kasasıyla yedekleme | Microsoft Belgeleri"
description: "Azure VM'ler tooa yedekleme kasası yukarı Hello Klasik portal tooback kullanın. Bu öğretici hello yedekleme kasası oluşturma, hello Vm'leri kaydetme, yedekleme ilkesi oluşturma ve hello ilk yedekleme işini çalıştırma dahil olmak üzere tüm aşamalar açıklanmaktadır."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 722820dc-b65f-425c-a9e5-c1946e896a87
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;
ms.openlocfilehash: 77700e69eab9faccbc7ef923e1eb4e1f97be75d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a><span data-ttu-id="cdd2a-104">İlk bakış: Azure sanal makinelerini yedekleme</span><span class="sxs-lookup"><span data-stu-id="cdd2a-104">First look: Backing up Azure virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cdd2a-105">VM'leri bir kurtarma hizmetleri kasasıyla koruma</span><span class="sxs-lookup"><span data-stu-id="cdd2a-105">Protect VMs with a recovery services vault</span></span>](backup-azure-vms-first-look-arm.md)
> * [<span data-ttu-id="cdd2a-106">Azure VM'lerini yedekleme kasasıyla koruma</span><span class="sxs-lookup"><span data-stu-id="cdd2a-106">Protect Azure VMs with a backup vault</span></span>](backup-azure-vms-first-look.md)
>
>

<span data-ttu-id="cdd2a-107">Bu öğretici bir Azure sanal makine (VM) tooa yedekleme kasasına Azure yedekleme için hello adımlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-107">This tutorial takes you through hello steps for backing up an Azure virtual machine (VM) tooa backup vault in Azure.</span></span> <span data-ttu-id="cdd2a-108">Bu makalede hello Klasik modeli veya VM'lerin yedeklenmesi için Service Manager dağıtım modeli açıklanır.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-108">This article describes hello classic model or Service Manager deployment model, for backing up VMs.</span></span> <span data-ttu-id="cdd2a-109">Merhaba aşağıdaki adımlar yalnızca hello Klasik portalında oluşturulan tooBackup kasalarını geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-109">hello following steps apply only tooBackup vaults created in hello classic portal.</span></span> <span data-ttu-id="cdd2a-110">Microsoft, yeni dağıtımlar için hello Resource Manager modelini kullanarak önerir.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-110">Microsoft recommends using hello Resource Manager model for new deployments.</span></span>

<span data-ttu-id="cdd2a-111">Tooa kaynak grubuna ait bir VM tooa kurtarma Hizmetleri kasasına yedekleme ilgilendiğiniz olup [ilk bakış: koruma Vm'leri bir kurtarma Hizmetleri kasası ile](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="cdd2a-111">If you are interested in backing up a VM tooa Recovery Services vault that belongs tooa Resource Group, see [First look: Protect VMs with a recovery services vault](backup-azure-vms-first-look-arm.md).</span></span>

<span data-ttu-id="cdd2a-112">toosuccessfully tamamlamak hello aşağıdaki öğreticide, şu önkoşulların bulunması gerekir:</span><span class="sxs-lookup"><span data-stu-id="cdd2a-112">toosuccessfully complete hello following tutorial, these prerequisites must exist:</span></span>

* <span data-ttu-id="cdd2a-113">Azure aboneliğinizde bir VM oluşturmuş olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-113">You have created a VM in your Azure subscription.</span></span>
* <span data-ttu-id="cdd2a-114">Merhaba VM bağlantı tooAzure genel IP adresleri vardır.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-114">hello VM has connectivity tooAzure public IP addresses.</span></span> <span data-ttu-id="cdd2a-115">Ek bilgi için bkz. [Ağ bağlantısı](backup-azure-vms-prepare.md#network-connectivity).</span><span class="sxs-lookup"><span data-stu-id="cdd2a-115">For additional information, see [Network connectivity](backup-azure-vms-prepare.md#network-connectivity).</span></span>


> [!NOTE]
> <span data-ttu-id="cdd2a-116">Azure'da kaynak oluşturmaya ve kaynaklarla çalışmaya yönelik iki dağıtım modeli mevcuttur: [Resource Manager ve Klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="cdd2a-116">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="cdd2a-117">Bu öğretici için hello Klasik Portalı'nda oluşturulan sanal makineleri ile kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-117">This tutorial is for use with virtual machines created in hello classic portal.</span></span>
>
>

## <a name="create-a-backup-vault"></a><span data-ttu-id="cdd2a-118">Yedekleme kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="cdd2a-118">Create a backup vault</span></span>
<span data-ttu-id="cdd2a-119">Bir yedekleme kasası tüm hello yedeklemeleri ve zaman içinde oluşturulan kurtarma noktalarını depolayan bir varlıktır.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-119">A backup vault is an entity that stores all hello backups and recovery points that have been created over time.</span></span> <span data-ttu-id="cdd2a-120">Merhaba yedekleme kasası, yedeklenmekte olan uygulanan toohello sanal makineleri hello yedekleme ilkeleri de içerir.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-120">hello backup vault also contains hello backup policies that are applied toohello virtual machines being backed up.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cdd2a-121">Mart 2017'dan başlayarak, hello Klasik portal toocreate yedekleme kasaları artık kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-121">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
> <span data-ttu-id="cdd2a-122">Yedekleme kasalarını tooRecovery Hizmetleri kasaları yükseltebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-122">You can upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="cdd2a-123">Ayrıntılar için hello makalesine bakın [kurtarma Hizmetleri kasası bir yedekleme kasası tooa yükseltme](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="cdd2a-123">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="cdd2a-124">Microsoft tooupgrade önerir tooRecovery Hizmetleri kasalarının yedekleme kasaları.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-124">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="cdd2a-125">15 Ekim 2017 sonra PowerShell toocreate yedekleme kasaları kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-125">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="cdd2a-126">**1 Kasım 2017’ye kadar**:</span><span class="sxs-lookup"><span data-stu-id="cdd2a-126">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="cdd2a-127">Kalan tüm yedekleme kasaları otomatik olarak yükseltilen tooRecovery Hizmetleri kasalarının olacaktır.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-127">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="cdd2a-128">Mümkün tooaccess hello Klasik Portalı'nda, yedekleme verilerinizi olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-128">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="cdd2a-129">Bunun yerine, hello Azure portal tooaccess kurtarma Hizmetleri kasalarının, yedekleme verilerinizi kullanın.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-129">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="discover-and-register-azure-virtual-machines"></a><span data-ttu-id="cdd2a-130">Azure sanal makinelerini bulma ve kaydetme</span><span class="sxs-lookup"><span data-stu-id="cdd2a-130">Discover and Register Azure virtual machines</span></span>
<span data-ttu-id="cdd2a-131">Merhaba VM'yi bir kasaya kaydetmeden önce yeni Vm'leri hello bulma işlemi tooidentify çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-131">Before registering hello VM with a vault, run hello discovery process tooidentify any new VMs.</span></span> <span data-ttu-id="cdd2a-132">Bu hello bulut hizmeti adı ve hello bölge gibi ek bilgilerle birlikte hello Abonelikteki sanal makinelerin listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-132">This returns a list of virtual machines in hello subscription, along with additional information like hello cloud service name and hello region.</span></span>

1. <span data-ttu-id="cdd2a-133">İçinde toohello oturum [Klasik Azure portalı](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="cdd2a-133">Sign in toohello [Azure Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="cdd2a-134">Hello Klasik Azure portalı, tıklatın **kurtarma Hizmetleri** tooopen hello kurtarma Hizmetleri kasalarının listesi.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-134">In hello Azure classic portal, click **Recovery Services** tooopen hello list of Recovery Services vaults.</span></span>
    <span data-ttu-id="cdd2a-135">![İş yükünü seçme](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span><span class="sxs-lookup"><span data-stu-id="cdd2a-135">![Select workload](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span></span>
3. <span data-ttu-id="cdd2a-136">Kasa Hello listeden hello kasa tooback VM yukarı seçin.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-136">From hello list of vaults, select hello vault tooback up a VM.</span></span>

    <span data-ttu-id="cdd2a-137">Kasanızı seçtiğinizde hello açılır **Hızlı Başlangıç** sayfası</span><span class="sxs-lookup"><span data-stu-id="cdd2a-137">When you select your vault, it opens in hello **Quick Start** page</span></span>
4. <span data-ttu-id="cdd2a-138">Merhaba kasa menüsünden tıklatın **kayıtlı öğeler**.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-138">From hello vault menu, click **Registered Items**.</span></span>

    ![İş yükünü seçme](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. <span data-ttu-id="cdd2a-140">Merhaba gelen **türü** menüsünde, select **Azure sanal makine**.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-140">From hello **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![İş yükünü seçme](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="cdd2a-142">Tıklatın **bulma** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-142">Click **DISCOVER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="cdd2a-143">![Bul düğmesi](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="cdd2a-143">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="cdd2a-144">Merhaba sanal makinelerin tabloya alınması nedeniyle sırada hello bulma işlemi birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-144">hello discovery process may take a few minutes while hello virtual machines are being tabulated.</span></span> <span data-ttu-id="cdd2a-145">Merhaba ekranın alt kısmındaki hello işleminin çalıştığını bilmeniz olanak sağlayan hello bir bildirim yoktur.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-145">There is a notification at hello bottom of hello screen that lets you know that hello process is running.</span></span>

    ![VM'leri bulma](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="cdd2a-147">Merhaba işlemi tamamlandığında hello bildirim değiştirir.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-147">hello notification changes when hello process is complete.</span></span>

    ![Bulma işlemi bitti](./media/backup-azure-vms-first-look/discovery-complete.png)
7. <span data-ttu-id="cdd2a-149">Tıklatın **KAYDETMEK** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-149">Click **REGISTER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="cdd2a-150">![Kaydet düğmesi](./media/backup-azure-vms-first-look/register-icon.png)</span><span class="sxs-lookup"><span data-stu-id="cdd2a-150">![Register button](./media/backup-azure-vms-first-look/register-icon.png)</span></span>
8. <span data-ttu-id="cdd2a-151">Merhaba, **öğeleri Kaydet** kısayol menüsü, select hello sanal makineleri tooregister istiyor.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-151">In hello **Register Items** shortcut menu, select hello virtual machines that you want tooregister.</span></span>

   > [!TIP]
   > <span data-ttu-id="cdd2a-152">Birden çok sanal makine aynı anda kaydedilebilir.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-152">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="cdd2a-153">Seçtiğiniz her sanal makine için bir iş oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-153">A job is created for each virtual machine that you've selected.</span></span>
9. <span data-ttu-id="cdd2a-154">Tıklatın **işi görüntüle** hello bildirim toogo toohello içinde **işleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-154">Click **View Job** in hello notification toogo toohello **Jobs** page.</span></span>

    ![İşi kaydetme](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="cdd2a-156">Merhaba sanal makine hello hello kayıt işleminin hello durumu ile birlikte kayıtlı öğeler listesinde de görünür.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-156">hello virtual machine also appears in hello list of registered items, along with hello status of hello registration operation.</span></span>

    ![Kayıt durumu 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="cdd2a-158">Merhaba işlemi tamamlandığında hello tooreflect hello durumuna *kayıtlı* durumu.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-158">When hello operation completes, hello status changes tooreflect hello *registered* state.</span></span>

    ![Kayıt durumu 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a><span data-ttu-id="cdd2a-160">Merhaba VM Aracısı hello sanal makineye yükleme</span><span class="sxs-lookup"><span data-stu-id="cdd2a-160">Install hello VM Agent on hello virtual machine</span></span>
<span data-ttu-id="cdd2a-161">Hello Azure VM Aracısı hello hello yedekleme uzantısını toowork Azure sanal makinesine yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-161">hello Azure VM Agent must be installed on hello Azure virtual machine for hello Backup extension toowork.</span></span> <span data-ttu-id="cdd2a-162">VM hello Azure galerisinde oluşturduysanız hello VM Aracısı VM hello üzerinde zaten; çok atlayabilirsiniz[Vm'lerinizi koruma](backup-azure-vms-first-look.md#create-the-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="cdd2a-162">If your VM was created from hello Azure gallery, hello VM Agent is already present on hello VM; you can skip too[protecting your VMs](backup-azure-vms-first-look.md#create-the-backup-policy).</span></span>

<span data-ttu-id="cdd2a-163">VM'NİZİN bir şirket içi merkezinden geçişi sağlandıysa hello VM VM aracısının yüklü hello büyük olasılıkla yok.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-163">If your VM migrated from an on-premises datacenter, hello VM probably does not have hello VM Agent installed.</span></span> <span data-ttu-id="cdd2a-164">Devam etmeden tooprotect hello VM önce hello sanal makinedeki hello VM aracısı yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-164">You must install hello VM Agent on hello virtual machine before proceeding tooprotect hello VM.</span></span> <span data-ttu-id="cdd2a-165">VM Aracısı yükleme konusunda ayrıntılı adımlar hello hello bakın [hello Vm'leri yedekleme makalesinin VM Aracısı bölümü](backup-azure-vms-prepare.md#vm-agent).</span><span class="sxs-lookup"><span data-stu-id="cdd2a-165">For detailed steps on installing hello VM Agent, see hello [VM Agent section of hello Backup VMs article](backup-azure-vms-prepare.md#vm-agent).</span></span>

## <a name="create-hello-backup-policy"></a><span data-ttu-id="cdd2a-166">Merhaba yedekleme ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="cdd2a-166">Create hello backup policy</span></span>
<span data-ttu-id="cdd2a-167">Merhaba ilk yedekleme işini tetiklemeden önce yedekleme anlık görüntülerinin alınma hello zamanlamasını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-167">Before you trigger hello initial backup job, set hello schedule when backup snapshots are taken.</span></span> <span data-ttu-id="cdd2a-168">Yedekleme anlık görüntülerinin alınır ve bu anlık görüntülerin süre hello hello zamanla korunur, yedekleme İlkesi hello'dır.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-168">hello schedule when backup snapshots are taken, and hello length of time those snapshots are retained, is hello backup policy.</span></span> <span data-ttu-id="cdd2a-169">Merhaba bekletme bilgileri, üst öğe son rotasyon düzenini temel alır.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-169">hello retention information is based on Grandfather-father-son backup rotation scheme.</span></span>

1. <span data-ttu-id="cdd2a-170">Toohello yedekleme kasasında gidin **kurtarma Hizmetleri** hello Klasik Azure portalı ve tıklatın **kayıtlı öğeler**.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-170">Navigate toohello backup vault under **Recovery Services** in hello Azure Classic portal, and  click **Registered Items**.</span></span>
2. <span data-ttu-id="cdd2a-171">Seçin **Azure sanal makine** hello açılan menüsünden.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-171">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![Portalda iş yükünü seçme](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="cdd2a-173">Tıklatın **koruma** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-173">Click **PROTECT** at hello bottom of hello page.</span></span>
    <span data-ttu-id="cdd2a-174">![Koru'ya tıklama](./media/backup-azure-vms-first-look/protect-icon.png)</span><span class="sxs-lookup"><span data-stu-id="cdd2a-174">![Click Protect](./media/backup-azure-vms-first-look/protect-icon.png)</span></span>

    <span data-ttu-id="cdd2a-175">Merhaba **öğeleri koruma Sihirbazı'nı** görünür ve listeler *yalnızca* kayıtlı ve korumalı sanal makineler.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-175">hello **Protect Items wizard** appears and lists *only* virtual machines that are registered and not protected.</span></span>

    ![Korumayı ölçekli olarak yapılandırma](./media/backup-azure-vms/protect-at-scale.png)
4. <span data-ttu-id="cdd2a-177">Merhaba sanal makineleri tooprotect istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-177">Select hello virtual machines that you want tooprotect.</span></span>

    <span data-ttu-id="cdd2a-178">Merhaba iki veya daha fazla sanal makinelerle varsa aynı adı, kullanım hello bulut hizmeti toodistinguish hello sanal makineler arasında.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-178">If there are two or more virtual machines with hello same name, use hello Cloud Service toodistinguish between hello virtual machines.</span></span>
5. <span data-ttu-id="cdd2a-179">Merhaba üzerinde **korumasını yapılandırma** menü mevcut bir ilkeyi seçin veya yeni bir ilke tooprotect tanımladığınız hello sanal makineler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-179">On hello **Configure protection** menu select an existing policy or create a new policy tooprotect hello virtual machines that you identified.</span></span>

    <span data-ttu-id="cdd2a-180">Yeni yedekleme kasaları hello kasayla ilişkili bir varsayılan ilke içerir.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-180">New Backup vaults have a default policy associated with hello vault.</span></span> <span data-ttu-id="cdd2a-181">Bu ilke her Akşam günlük bir anlık alır ve hello günlük anlık görüntü 30 gün süreyle tutulur.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-181">This policy takes a daily snapshot each evening, and hello daily snapshot is retained for 30 days.</span></span> <span data-ttu-id="cdd2a-182">Her bir yedekleme ilkesi, kendisiyle ilişkili birden çok sanal makineye sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-182">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="cdd2a-183">Ancak, hello sanal makine yalnızca aynı anda bir ilkeyle ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-183">However, hello virtual machine can only be associated with one policy at a time.</span></span>

    ![Yeni ilke ile koruma](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="cdd2a-185">Bir yedekleme İlkesi hello zamanlanmış yedeklemeler için bir bekletme düzeni içerir.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-185">A backup policy includes a retention scheme for hello scheduled backups.</span></span> <span data-ttu-id="cdd2a-186">Mevcut bir yedekleme İlkesi seçerseniz, hello sonraki adımda oluşturulamıyor toomodify hello bekletme seçenekleri olacaktır.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-186">If you select an existing backup policy, you will be unable toomodify hello retention options in hello next step.</span></span>
   >
   >
6. <span data-ttu-id="cdd2a-187">Üzerinde **bekletme aralığı** tanımlamak hello hello belirli yedekleme noktaları için günlük, haftalık, aylık ve yıllık kapsam.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-187">On **Retention Range** define hello daily, weekly, monthly, and yearly scope for hello specific backup points.</span></span>

    ![Sanal makine, kurtarma noktası ile yedeklenir](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="cdd2a-189">Bekletme İlkesi hello uzun bir yedeklemenin depolanacağı süreyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-189">Retention policy specifies hello length of time for storing a backup.</span></span> <span data-ttu-id="cdd2a-190">Merhaba yedeklemenin ne zaman göre farklı bekletme ilkeleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-190">You can specify different retention policies based on when hello backup is taken.</span></span>
7. <span data-ttu-id="cdd2a-191">Tıklatın **işleri** tooview hello listesi **korumayı Yapılandır** işler.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-191">Click **Jobs** tooview hello list of **Configure Protection** jobs.</span></span>

    ![Korumayı yapılandır işi](./media/backup-azure-vms/protect-configureprotection.png)

    <span data-ttu-id="cdd2a-193">Merhaba ilkeyi belirlediğinize göre toohello sonraki adıma gidin ve hello ilk yedeklemeyi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-193">Now that you've established hello policy, go toohello next step and run hello initial backup.</span></span>

## <a name="initial-backup"></a><span data-ttu-id="cdd2a-194">İlk yedekleme</span><span class="sxs-lookup"><span data-stu-id="cdd2a-194">Initial backup</span></span>
<span data-ttu-id="cdd2a-195">Bir sanal makineye sahip bir ilke korunduktan sonra bu ilişkiyi hello üzerinde görüntüleyebilirsiniz **korunan öğeler** sekmesi. Merhaba ilk yedekleme, hello gerçekleşene kadar **koruma durumu** olarak gösterir **korumalı - (ilk yedekleme bekleniyor)**.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-195">Once a virtual machine has been protected with a policy, you can view that relationship on hello **Protected Items** tab. Until hello initial backup occurs, hello **Protection Status** shows as **Protected - (pending initial backup)**.</span></span> <span data-ttu-id="cdd2a-196">Varsayılan olarak, ilk zamanlanmış yedekleme hello hello olan *ilk yedekleme*.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-196">By default, hello first scheduled backup is hello *initial backup*.</span></span>

![Yedekleme beklemede](./media/backup-azure-vms-first-look/protection-pending-border.png)

<span data-ttu-id="cdd2a-198">toostart hello ilk yedeklemeyi şimdi:</span><span class="sxs-lookup"><span data-stu-id="cdd2a-198">toostart hello initial backup now:</span></span>

1. <span data-ttu-id="cdd2a-199">Merhaba üzerinde **korunan öğeler** sayfasında, **Şimdi Yedekle** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-199">On hello **Protected Items** page, click **Backup Now** at hello bottom of hello page.</span></span>
    <span data-ttu-id="cdd2a-200">![Şimdi Yedekle simgesi](./media/backup-azure-vms-first-look/backup-now-icon.png)</span><span class="sxs-lookup"><span data-stu-id="cdd2a-200">![Backup Now icon](./media/backup-azure-vms-first-look/backup-now-icon.png)</span></span>

    <span data-ttu-id="cdd2a-201">Hello Azure Backup hizmeti hello ilk yedekleme işlemi için bir yedekleme işi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-201">hello Azure Backup service creates a backup job for hello initial backup operation.</span></span>
2. <span data-ttu-id="cdd2a-202">Hello tıklatın **işleri** sekmesini tooview hello işlerin listesi.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-202">Click hello **Jobs** tab tooview hello list of jobs.</span></span>

    ![Yedekleme devam ediyor](./media/backup-azure-vms-first-look/protect-inprogress.png)

    <span data-ttu-id="cdd2a-204">İlk yedekleme tamamlandığında, hello hello hello sanal makinenin durumunu **korunan öğeler** sekmesi *korumalı*.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-204">When initial backup is complete, hello status of hello virtual machine in hello **Protected Items** tab is *Protected*.</span></span>

    ![Sanal makine, kurtarma noktası ile yedeklenir](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > <span data-ttu-id="cdd2a-206">Sanal makineleri yedekleme işlemi, yerel bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-206">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="cdd2a-207">Sanal makineleri başka bir bölgede bir bölge tooa yedekleme Kasası'ndan yedekleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-207">You cannot back up virtual machines from one region tooa backup vault in another region.</span></span> <span data-ttu-id="cdd2a-208">Bu nedenle, yedeklenen toobe gereken VM'lerin bulunduğu her Azure bölgesi için bu bölgede en az bir yedekleme kasası oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-208">So, for every Azure region that has VMs that need toobe backed up, at least one backup vault must be created in that region.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="cdd2a-209">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cdd2a-209">Next steps</span></span>
<span data-ttu-id="cdd2a-210">Bir VM'yi başarıyla yedeklediğinize göre, sonraki birkaç adım ilginizi çekebilir.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-210">Now that you have successfully backed up a VM, there are several next steps that could be of interest.</span></span> <span data-ttu-id="cdd2a-211">Merhaba en mantıklı toofamiliarize kendiniz veri tooa VM geri yükleme ile bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-211">hello most logical step is toofamiliarize yourself with restoring data tooa VM.</span></span> <span data-ttu-id="cdd2a-212">Ancak, anlamanıza yardımcı olacak yönetim görevleri vardır nasıl tookeep verilerinizi güvenli ve maliyetleri en aza indirin.</span><span class="sxs-lookup"><span data-stu-id="cdd2a-212">However, there are management tasks that will help you understand how tookeep your data safe and minimize costs.</span></span>

* [<span data-ttu-id="cdd2a-213">Sanal makinelerinizi yönetme ve izleme</span><span class="sxs-lookup"><span data-stu-id="cdd2a-213">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="cdd2a-214">Sanal makineleri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="cdd2a-214">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
* [<span data-ttu-id="cdd2a-215">Sorun giderme rehberi</span><span class="sxs-lookup"><span data-stu-id="cdd2a-215">Troubleshooting guidance</span></span>](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a><span data-ttu-id="cdd2a-216">Sorularınız mı var?</span><span class="sxs-lookup"><span data-stu-id="cdd2a-216">Questions?</span></span>
<span data-ttu-id="cdd2a-217">Sorularınız varsa veya herhangi bir özellik varsa dahil, toosee istediğiniz [Geri bildirimlerinizi bize gönderin](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="cdd2a-217">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>
