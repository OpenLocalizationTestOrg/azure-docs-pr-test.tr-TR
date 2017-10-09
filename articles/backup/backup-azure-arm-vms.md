---
title: Azure Vm'leri yedekleme aaaBack | Microsoft Docs
description: "Bul kaydolun ve Azure sanal makineleri tooa kurtarma Hizmetleri kasasını yedekleyin."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "sanal makine yedeklemesi; sanal makineyi geri; Yedekleme ve olağanüstü durum kurtarma; ARM vm yedekleme"
ms.assetid: 5c68481d-7be3-4e68-b87c-0961c267053e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: trinadhk;jimpark;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a204a42726450a7fd89b5563a786b5070578b113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-tooa-recovery-services-vault"></a><span data-ttu-id="e9b78-104">Geri Azure sanal makinelerini tooa kurtarma Hizmetleri kasası</span><span class="sxs-lookup"><span data-stu-id="e9b78-104">Back up Azure virtual machines tooa Recovery Services vault</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e9b78-105">Sanal makineleri tooRecovery Hizmetleri kasasını yedekleyin</span><span class="sxs-lookup"><span data-stu-id="e9b78-105">Back up VMs tooRecovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="e9b78-106">Sanal makineleri tooBackup kasasını yedekleyin</span><span class="sxs-lookup"><span data-stu-id="e9b78-106">Back up VMs tooBackup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="e9b78-107">Bu makalede nasıl tooback yukarı Azure VM'ler (Resource Manager tarafından dağıtılan ve klasik dağıtılan) tooa kurtarma Hizmetleri kasası ayrıntıları verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e9b78-107">This article details how tooback up Azure VMs (both Resource Manager-deployed and Classic-deployed) tooa Recovery Services vault.</span></span> <span data-ttu-id="e9b78-108">Vm'leri yedekleme için hello çalışmanın çoğu hello hazırlık olur.</span><span class="sxs-lookup"><span data-stu-id="e9b78-108">Most of hello work for backing up VMs is hello preparation.</span></span> <span data-ttu-id="e9b78-109">Yedeklemek veya VM koruma önce hello tamamlamalısınız [Önkoşullar](backup-azure-arm-vms-prepare.md) tooprepare Vm'lerinizi koruma için ortamınızı.</span><span class="sxs-lookup"><span data-stu-id="e9b78-109">Before you can back up or protect a VM, you must complete hello [prerequisites](backup-azure-arm-vms-prepare.md) tooprepare your environment for protecting your VMs.</span></span> <span data-ttu-id="e9b78-110">Merhaba önkoşulları tamamladıktan sonra hello yedekleme işlemi tootake VM anlık görüntülerini işlemi başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9b78-110">Once you have completed hello prerequisites, then you can initiate hello backup operation tootake snapshots of your VM.</span></span>


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

<span data-ttu-id="e9b78-111">Daha fazla bilgi için üzerinde hello makalelerine bakın [azure'da VM yedekleme altyapınızı planlama](backup-azure-vms-introduction.md) ve [Azure sanal makineleri](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="e9b78-111">For more information, see hello articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

## <a name="triggering-hello-backup-job"></a><span data-ttu-id="e9b78-112">Tetikleyici hello yedekleme işi</span><span class="sxs-lookup"><span data-stu-id="e9b78-112">Triggering hello backup job</span></span>
<span data-ttu-id="e9b78-113">Kurtarma Hizmetleri kasası hello ile ilişkili hello yedekleme İlkesi hello Yedekleme işleminin ne sıklıkta ve ne zaman çalışması tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e9b78-113">hello backup policy associated with hello Recovery Services vault defines how often and when hello backup operation runs.</span></span> <span data-ttu-id="e9b78-114">Varsayılan olarak, ilk zamanlanmış yedekleme hello hello ilk yedeklemedir.</span><span class="sxs-lookup"><span data-stu-id="e9b78-114">By default, hello first scheduled backup is hello initial backup.</span></span> <span data-ttu-id="e9b78-115">Merhaba ilk yedekleme gerçekleşene kadar son yedekleme durumu hello üzerinde hello **yedekleme işleri** dikey gösterildiğinden **uyarı (ilk yedekleme bekleme)**.</span><span class="sxs-lookup"><span data-stu-id="e9b78-115">Until hello initial backup occurs, hello Last Backup Status on hello **Backup Jobs** blade shows as **Warning(initial backup pending)**.</span></span>

![Yedekleme beklemede](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

<span data-ttu-id="e9b78-117">İlk yedeklemeniz son olmadığı sürece toobegin yakında önerilir, çalıştırmanız **Şimdi Yedekle**.</span><span class="sxs-lookup"><span data-stu-id="e9b78-117">Unless your initial backup is due toobegin soon, it is recommended that you run **Back up Now**.</span></span> <span data-ttu-id="e9b78-118">Merhaba aşağıdaki yordamı hello kasası panodan başlatır.</span><span class="sxs-lookup"><span data-stu-id="e9b78-118">hello following procedure starts from hello vault dashboard.</span></span> <span data-ttu-id="e9b78-119">Bu yordam, tüm önkoşullar tamamladıktan sonra hello ilk yedekleme işini çalıştırmak için görev yapar.</span><span class="sxs-lookup"><span data-stu-id="e9b78-119">This procedure serves for running hello initial backup job after you have completed all prerequisites.</span></span> <span data-ttu-id="e9b78-120">Merhaba ilk yedekleme işi zaten çalıştırıldıysa, bu yordam kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="e9b78-120">If hello initial backup job has already been run, this procedure is not available.</span></span> <span data-ttu-id="e9b78-121">Merhaba ilişkili yedekleme İlkesi hello sonraki yedekleme işini belirler.</span><span class="sxs-lookup"><span data-stu-id="e9b78-121">hello associated backup policy determines hello next backup job.</span></span>  

<span data-ttu-id="e9b78-122">toorun hello ilk yedekleme işini:</span><span class="sxs-lookup"><span data-stu-id="e9b78-122">toorun hello initial backup job:</span></span>

1. <span data-ttu-id="e9b78-123">Merhaba kasa Panosu üzerinde hello numarasını altında tıklatın **yedekleme öğeleri**, veya hello **yedekleme öğeleri** döşeme.</span><span class="sxs-lookup"><span data-stu-id="e9b78-123">On hello vault dashboard, click hello number under **Backup Items**, or click hello **Backup Items** tile.</span></span> <br/><span data-ttu-id="e9b78-124">
  ![Ayarlar simgesi](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span><span class="sxs-lookup"><span data-stu-id="e9b78-124">
![Settings icon](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span></span>

  <span data-ttu-id="e9b78-125">Merhaba **yedekleme öğeleri** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="e9b78-125">hello **Backup Items** blade opens.</span></span>

  ![Öğeleri yedekleme](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. <span data-ttu-id="e9b78-127">Merhaba üzerinde **yedekleme öğeleri** dikey penceresinde, select hello öğesi.</span><span class="sxs-lookup"><span data-stu-id="e9b78-127">On hello **Backup Items** blade, select hello item.</span></span>

  ![Ayarlar simgesi](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  <span data-ttu-id="e9b78-129">Merhaba **yedekleme öğeleri** listesi açılır.</span><span class="sxs-lookup"><span data-stu-id="e9b78-129">hello **Backup Items** list opens.</span></span> <br/>

  ![Tetiklenmiş yedekleme işi](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. <span data-ttu-id="e9b78-131">Merhaba üzerinde **yedekleme öğeleri** listesinde, hello üç noktaya tıklayın **...**  tooopen hello bağlam menüsü.</span><span class="sxs-lookup"><span data-stu-id="e9b78-131">On hello **Backup Items** list, click hello ellipses **...** tooopen hello Context menu.</span></span>

  ![Bağlam menüsü](./media/backup-azure-vms-first-look-arm/context-menu.png)

  <span data-ttu-id="e9b78-133">Merhaba bağlam menüsü görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e9b78-133">hello Context menu appears.</span></span>

  ![Bağlam menüsü](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. <span data-ttu-id="e9b78-135">Merhaba bağlam menüsünde **Şimdi Yedekle**.</span><span class="sxs-lookup"><span data-stu-id="e9b78-135">On hello Context menu, click **Backup now**.</span></span>

  ![Bağlam menüsü](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  <span data-ttu-id="e9b78-137">Merhaba Şimdi Yedekle dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="e9b78-137">hello Backup Now blade opens.</span></span>

  ![Merhaba Şimdi Yedekle dikey gösterir](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. <span data-ttu-id="e9b78-139">Merhaba Şimdi Yedekle dikey penceresinde hello takvim simgesini tıklatın, hello Takvim denetimi tooselect hello bu kurtarma noktası korunur ve tıklatın son günü kullanın **yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="e9b78-139">On hello Backup Now blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>

  ![set hello son gün hello Şimdi Yedekle kurtarma noktası korunur](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  <span data-ttu-id="e9b78-141">Dağıtım bildirimleri hello yedekleme işi tetiklenir ve hello işinin ilerleme durumunu hello hello yedekleme işleri sayfasında izleyebilirsiniz size bildirmek.</span><span class="sxs-lookup"><span data-stu-id="e9b78-141">Deployment notifications let you know hello backup job has been triggered, and that you can monitor hello progress of hello job on hello Backup jobs page.</span></span> <span data-ttu-id="e9b78-142">VM Hello boyutuna bağlı olarak, hello ilk yedek oluşturulması biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="e9b78-142">Depending on hello size of your VM, creating hello initial backup may take a while.</span></span>

6. <span data-ttu-id="e9b78-143">Merhaba üzerinde hello kasa Panosu üzerinde hello ilk yedekleme tooview veya iz hello durumunu **yedekleme işleri** döşeme tıklatın **devam eden**.</span><span class="sxs-lookup"><span data-stu-id="e9b78-143">tooview or track hello status of hello initial backup, on hello vault dashboard, on hello **Backup Jobs** tile click **In progress**.</span></span>

  ![Yedekleme İşleri kutucuğu](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  <span data-ttu-id="e9b78-145">Merhaba yedekleme işleri dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="e9b78-145">hello Backup Jobs blade opens.</span></span>

  ![Yedekleme İşleri kutucuğu](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  <span data-ttu-id="e9b78-147">Merhaba, **yedekleme işleri** dikey penceresinde hello tüm işlerin durumunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9b78-147">In hello **Backup jobs** blade, you can see hello status of all jobs.</span></span> <span data-ttu-id="e9b78-148">Merhaba, VM için yedekleme işi devam ediyor veya sona erdi kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="e9b78-148">Check if hello backup job for your VM is still in progress, or if it has finished.</span></span> <span data-ttu-id="e9b78-149">Bir yedekleme işi tamamlandığında, hello durumudur *tamamlandı*.</span><span class="sxs-lookup"><span data-stu-id="e9b78-149">When a backup job is finished, hello status is *Completed*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e9b78-150">Merhaba Yedekleme işleminin bir parçası olarak bir komut toohello yedekleme uzantısına tüm yazar ve tutarlı bir anlık görüntüsünü her VM tooflush hello Azure Backup hizmeti verir.</span><span class="sxs-lookup"><span data-stu-id="e9b78-150">As a part of hello backup operation, hello Azure Backup service issues a command toohello backup extension in each VM tooflush all writes and take a consistent snapshot.</span></span>
  >
  >

## <a name="troubleshooting-errors"></a><span data-ttu-id="e9b78-151">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="e9b78-151">Troubleshooting errors</span></span>
<span data-ttu-id="e9b78-152">Sanal makineniz yedekleme sırasında sorunları içine çalıştırırsanız hello bkz [VM sorun giderme makalesi](backup-azure-vms-troubleshoot.md) Yardım.</span><span class="sxs-lookup"><span data-stu-id="e9b78-152">If you run into issues while backing up your virtual machine, see hello [VM troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9b78-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e9b78-153">Next steps</span></span>
<span data-ttu-id="e9b78-154">VM korumalı, makaleler toolearn VM yönetim görevleri hakkında aşağıdaki hello bakın ve nasıl toorestore VM'ler.</span><span class="sxs-lookup"><span data-stu-id="e9b78-154">Now that you have protected your VM, see hello following articles toolearn about VM management tasks, and how toorestore VMs.</span></span>

* [<span data-ttu-id="e9b78-155">Sanal makinelerinizi yönetme ve izleme</span><span class="sxs-lookup"><span data-stu-id="e9b78-155">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="e9b78-156">Sanal makineleri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="e9b78-156">Restore virtual machines</span></span>](backup-azure-arm-restore-vms.md)
