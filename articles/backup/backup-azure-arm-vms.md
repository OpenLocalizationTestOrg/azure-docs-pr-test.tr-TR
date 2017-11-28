---
title: Azure Vm'leri yedekleme | Microsoft Docs
description: "Bul, kaydetme ve Azure sanal makineleri bir kurtarma Hizmetleri kasasına yedekleme."
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
ms.openlocfilehash: 40983a3de104238d09b976b5fcf2419da42c1bba
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="back-up-azure-virtual-machines-to-a-recovery-services-vault"></a><span data-ttu-id="b56c6-104">Azure sanal makinelerini bir Kurtarma Hizmetleri kasasına yedekleme</span><span class="sxs-lookup"><span data-stu-id="b56c6-104">Back up Azure virtual machines to a Recovery Services vault</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b56c6-105">Vm'leri kurtarma Hizmetleri kasasına yedekleme</span><span class="sxs-lookup"><span data-stu-id="b56c6-105">Back up VMs to Recovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="b56c6-106">Yedekleme Kasası'na Vm'leri yedekleme</span><span class="sxs-lookup"><span data-stu-id="b56c6-106">Back up VMs to Backup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="b56c6-107">Bu makalede Azure Vm'leri (Resource Manager tarafından dağıtılan ve klasik dağıtılan) bir kurtarma Hizmetleri kasasına yedekleme konusunda ayrıntılı olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b56c6-107">This article details how to back up Azure VMs (both Resource Manager-deployed and Classic-deployed) to a Recovery Services vault.</span></span> <span data-ttu-id="b56c6-108">İşlerin çoğunu VM'lerin yedeklenmesi için hazırlık olur.</span><span class="sxs-lookup"><span data-stu-id="b56c6-108">Most of the work for backing up VMs is the preparation.</span></span> <span data-ttu-id="b56c6-109">Yedeklemek veya VM korumak için önce tamamlamanız gereken [Önkoşullar](backup-azure-arm-vms-prepare.md) Vm'lerinizi koruma için ortamınızı hazırlamak için.</span><span class="sxs-lookup"><span data-stu-id="b56c6-109">Before you can back up or protect a VM, you must complete the [prerequisites](backup-azure-arm-vms-prepare.md) to prepare your environment for protecting your VMs.</span></span> <span data-ttu-id="b56c6-110">Sonra önkoşulları tamamladıktan sonra VM anlık görüntülerini almak için yedekleme işlemi başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b56c6-110">Once you have completed the prerequisites, then you can initiate the backup operation to take snapshots of your VM.</span></span>


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

<span data-ttu-id="b56c6-111">Daha fazla bilgi için üzerinde makalelerine bakın [azure'da VM yedekleme altyapınızı planlama](backup-azure-vms-introduction.md) ve [Azure sanal makineleri](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="b56c6-111">For more information, see the articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

## <a name="triggering-the-backup-job"></a><span data-ttu-id="b56c6-112">Yedekleme işini tetiklemeden</span><span class="sxs-lookup"><span data-stu-id="b56c6-112">Triggering the backup job</span></span>
<span data-ttu-id="b56c6-113">Kurtarma Hizmetleri kasası ile ilişkili yedekleme İlkesi, Yedekleme işleminin ne sıklıkta ve ne zaman çalışması tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b56c6-113">The backup policy associated with the Recovery Services vault defines how often and when the backup operation runs.</span></span> <span data-ttu-id="b56c6-114">Varsayılan olarak, ilk zamanlanmış yedekleme ilk yedeklemedir.</span><span class="sxs-lookup"><span data-stu-id="b56c6-114">By default, the first scheduled backup is the initial backup.</span></span> <span data-ttu-id="b56c6-115">İlk yedekleme gerçekleştirilene kadar, **Yedekleme İşleri** dikey penceresindeki Son Yedekleme Durumu **Uyarı (ilk yedekleme bekleme)** olarak gösterilir.</span><span class="sxs-lookup"><span data-stu-id="b56c6-115">Until the initial backup occurs, the Last Backup Status on the **Backup Jobs** blade shows as **Warning(initial backup pending)**.</span></span>

![Yedekleme beklemede](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

<span data-ttu-id="b56c6-117">İlk yedeklemeniz kısa süre içinde başlamazsa **Şimdi Yedekle** seçeneğini çalıştırmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="b56c6-117">Unless your initial backup is due to begin soon, it is recommended that you run **Back up Now**.</span></span> <span data-ttu-id="b56c6-118">Aşağıdaki yordam kasa panodan başlatır.</span><span class="sxs-lookup"><span data-stu-id="b56c6-118">The following procedure starts from the vault dashboard.</span></span> <span data-ttu-id="b56c6-119">Bu yordam, tüm önkoşullar tamamladıktan sonra ilk yedekleme işini çalıştırmak için görev yapar.</span><span class="sxs-lookup"><span data-stu-id="b56c6-119">This procedure serves for running the initial backup job after you have completed all prerequisites.</span></span> <span data-ttu-id="b56c6-120">İlk yedekleme işini zaten çalıştırıldıysa, bu yordam kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="b56c6-120">If the initial backup job has already been run, this procedure is not available.</span></span> <span data-ttu-id="b56c6-121">İlişkili yedekleme İlkesi bir sonraki yedekleme işi belirler.</span><span class="sxs-lookup"><span data-stu-id="b56c6-121">The associated backup policy determines the next backup job.</span></span>  

<span data-ttu-id="b56c6-122">İlk yedekleme işini çalıştırmak için:</span><span class="sxs-lookup"><span data-stu-id="b56c6-122">To run the initial backup job:</span></span>

1. <span data-ttu-id="b56c6-123">Kasa panosunda **Yedekleme Öğeleri** altındaki sayıya veya **Yedekleme Öğeleri** kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b56c6-123">On the vault dashboard, click the number under **Backup Items**, or click the **Backup Items** tile.</span></span> <br/><span data-ttu-id="b56c6-124">
  ![Ayarlar simgesi](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span><span class="sxs-lookup"><span data-stu-id="b56c6-124">
![Settings icon](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span></span>

  <span data-ttu-id="b56c6-125">**Yedekleme Öğeleri** dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="b56c6-125">The **Backup Items** blade opens.</span></span>

  ![Öğeleri yedekleme](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. <span data-ttu-id="b56c6-127">**Yedekleme Öğeleri** dikey penceresinde öğeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="b56c6-127">On the **Backup Items** blade, select the item.</span></span>

  ![Ayarlar simgesi](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  <span data-ttu-id="b56c6-129">**Yedekleme Öğeleri** listesi açılır.</span><span class="sxs-lookup"><span data-stu-id="b56c6-129">The **Backup Items** list opens.</span></span> <br/>

  ![Tetiklenmiş yedekleme işi](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. <span data-ttu-id="b56c6-131">**Yedekleme Öğeleri** listesinde üç noktaya **...** tıklayarak Bağlam menüsünü açın.</span><span class="sxs-lookup"><span data-stu-id="b56c6-131">On the **Backup Items** list, click the ellipses **...** to open the Context menu.</span></span>

  ![Bağlam menüsü](./media/backup-azure-vms-first-look-arm/context-menu.png)

  <span data-ttu-id="b56c6-133">Bağlam menüsü görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b56c6-133">The Context menu appears.</span></span>

  ![Bağlam menüsü](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. <span data-ttu-id="b56c6-135">Bağlam menüsünde **Şimdi yedekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b56c6-135">On the Context menu, click **Backup now**.</span></span>

  ![Bağlam menüsü](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  <span data-ttu-id="b56c6-137">Şimdi Yedekle dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="b56c6-137">The Backup Now blade opens.</span></span>

  ![Şimdi Yedekle dikey penceresi](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. <span data-ttu-id="b56c6-139">Şimdi Yedekle dikey penceresinde, takvim simgesine tıklayın, bu kurtarma noktasının korunduğu son günü seçmek için Takvim denetimlerini kullanın ve **Yedekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b56c6-139">On the Backup Now blade, click the calendar icon, use the calendar control to select the last day this recovery point is retained, and click **Backup**.</span></span>

  ![Şimdi Yedekle kurtarma noktasının korunduğu son günü ayarlayın](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  <span data-ttu-id="b56c6-141">Dağıtım bildirimleri, yedekleme işinin tetiklendiğini ve Yedekleme işleri sayfasında işin ilerleme durumunu izleyebileceğinizi bilmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b56c6-141">Deployment notifications let you know the backup job has been triggered, and that you can monitor the progress of the job on the Backup jobs page.</span></span> <span data-ttu-id="b56c6-142">VM’nizin boyutuna bağlı olarak, ilk yedeklemenin oluşturulması biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="b56c6-142">Depending on the size of your VM, creating the initial backup may take a while.</span></span>

6. <span data-ttu-id="b56c6-143">İlk yedekleme durumunu izlemek için kasa panosunda **Yedekleme İşleri** kutucuğunda **Devam eden**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b56c6-143">To view or track the status of the initial backup, on the vault dashboard, on the **Backup Jobs** tile click **In progress**.</span></span>

  ![Yedekleme İşleri kutucuğu](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  <span data-ttu-id="b56c6-145">Yedekleme İşleri dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="b56c6-145">The Backup Jobs blade opens.</span></span>

  ![Yedekleme İşleri kutucuğu](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  <span data-ttu-id="b56c6-147">**Yedekleme işleri** dikey penceresinde tüm işlerin durumunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b56c6-147">In the **Backup jobs** blade, you can see the status of all jobs.</span></span> <span data-ttu-id="b56c6-148">VM’niz için yedekleme işinin devam edip etmediğini veya bitip bitmediğini kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="b56c6-148">Check if the backup job for your VM is still in progress, or if it has finished.</span></span> <span data-ttu-id="b56c6-149">Yedekleme işi tamamlandığında, durum *Tamamlandı* olur.</span><span class="sxs-lookup"><span data-stu-id="b56c6-149">When a backup job is finished, the status is *Completed*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="b56c6-150">Azure Backup hizmeti, yedekleme işleminin parçası olarak, her VM'deki yedekleme uzantısına tüm yazma işlemlerini boşaltmaya ve tutarlı bir anlık görüntü almaya yönelik bir komut verir.</span><span class="sxs-lookup"><span data-stu-id="b56c6-150">As a part of the backup operation, the Azure Backup service issues a command to the backup extension in each VM to flush all writes and take a consistent snapshot.</span></span>
  >
  >

## <a name="troubleshooting-errors"></a><span data-ttu-id="b56c6-151">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="b56c6-151">Troubleshooting errors</span></span>
<span data-ttu-id="b56c6-152">Sanal makineniz yedekleme sırasında sorunları içine çalıştırırsanız bkz [VM sorun giderme makalesi](backup-azure-vms-troubleshoot.md) Yardım.</span><span class="sxs-lookup"><span data-stu-id="b56c6-152">If you run into issues while backing up your virtual machine, see the [VM troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b56c6-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b56c6-153">Next steps</span></span>
<span data-ttu-id="b56c6-154">VM korumalı, VM yönetim görevleri ve sanal makineleri geri yükleme hakkında bilgi edinmek için aşağıdaki makalelere bakın.</span><span class="sxs-lookup"><span data-stu-id="b56c6-154">Now that you have protected your VM, see the following articles to learn about VM management tasks, and how to restore VMs.</span></span>

* [<span data-ttu-id="b56c6-155">Sanal makinelerinizi yönetme ve izleme</span><span class="sxs-lookup"><span data-stu-id="b56c6-155">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="b56c6-156">Sanal makineleri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="b56c6-156">Restore virtual machines</span></span>](backup-azure-arm-restore-vms.md)
