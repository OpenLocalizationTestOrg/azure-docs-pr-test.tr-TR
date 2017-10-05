---
title: "Devre dışı bırakın ve bir StorSimple cihazı silmek | Microsoft Docs"
description: "StorSimple cihazı hizmetinden önce devre dışı bırakma ve silme kaldırmayı açıklar."
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 155cda38-c5ae-45dc-b7e8-6444494afc9e
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c000a642aa088ac80cc7077453b87e9a47f96900
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deactivate-and-delete-a-storsimple-8000-series-device-via-storsimple-manager-service"></a><span data-ttu-id="3f37e-103">Devre dışı bırakın ve StorSimple Yöneticisi hizmeti üzerinden bir StorSimple 8000 serisi aygıtı silme</span><span class="sxs-lookup"><span data-stu-id="3f37e-103">Deactivate and delete a StorSimple 8000 series device via StorSimple Manager service</span></span>
## <a name="overview"></a><span data-ttu-id="3f37e-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="3f37e-104">Overview</span></span>
<span data-ttu-id="3f37e-105">Hizmet dışına StorSimple cihazı (örneğin, değiştirme veya Cihazınızı yükseltmek veya StorSimple artık kullanıyorsanız) almak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f37e-105">You may wish to take a StorSimple device out of service (for example, if you are replacing or upgrading your device or if you are no longer using StorSimple).</span></span> <span data-ttu-id="3f37e-106">Bu durumda, silebilmek için önce cihazın devre dışı bırakılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f37e-106">If this is the case, you will need to deactivate the device before you can delete it.</span></span> <span data-ttu-id="3f37e-107">Devre dışı bırakma, aygıt ve karşılık gelen StorSimple Yöneticisi hizmeti arasındaki bağlantı sunucularının.</span><span class="sxs-lookup"><span data-stu-id="3f37e-107">Deactivating severs the connection between the device and the corresponding StorSimple Manager service.</span></span> <span data-ttu-id="3f37e-108">Bu öğretici, bir StorSimple cihazı ilk onu devre dışı bırakma ve silme hizmetten kaldırmak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3f37e-108">This tutorial explains how to remove a StorSimple device from service by first deactivating it and then deleting it.</span></span> 

<span data-ttu-id="3f37e-109">Bir aygıtı devre dışı bıraktığınızda, cihazda yerel olarak depolanan tüm verileri artık erişilebilir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3f37e-109">When you deactivate a device, any data that was stored locally on the device will no longer be accessible.</span></span> <span data-ttu-id="3f37e-110">Yalnızca bulutta depolanan cihaz ile ilişkili verileri kurtarılabilir.</span><span class="sxs-lookup"><span data-stu-id="3f37e-110">Only the data associated with the device that was stored in the cloud can be recovered.</span></span>  

> [!WARNING]
> <span data-ttu-id="3f37e-111">Devre dışı bırakma kalıcı bir işlemdir ve geri alınamaz.</span><span class="sxs-lookup"><span data-stu-id="3f37e-111">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="3f37e-112">Varsayılan fabrika ayarlarına sıfırlama işlemi ilk sürece StorSimple Yöneticisi hizmetiyle devre dışı bırakılan bir cihaz kaydedilemez.</span><span class="sxs-lookup"><span data-stu-id="3f37e-112">A deactivated device cannot be registered with the StorSimple Manager service unless it is first reset to the default factory settings.</span></span> 
> 
> <span data-ttu-id="3f37e-113">İşlem siler, cihazda yerel olarak depolanan tüm verileri fabrika ayarlarına sıfırlayamaz.</span><span class="sxs-lookup"><span data-stu-id="3f37e-113">The factory reset process deletes all the data that was stored locally on your device.</span></span> <span data-ttu-id="3f37e-114">Bu nedenle, bir cihazın devre dışı bırakmadan önce tüm verilerinizi bir bulut anlık görüntüsünü gereklidir.</span><span class="sxs-lookup"><span data-stu-id="3f37e-114">Therefore, it is essential that you take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="3f37e-115">Bu, daha sonraki bir aşamada tüm verileri kurtarmak olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="3f37e-115">This will allow you to recover all the data at a later stage.</span></span>
> 
> 

<span data-ttu-id="3f37e-116">Bu öğretici açıklar nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="3f37e-116">This tutorial explains how to:</span></span>

* <span data-ttu-id="3f37e-117">Bir aygıtı devre dışı bırakın ve verileri silme</span><span class="sxs-lookup"><span data-stu-id="3f37e-117">Deactivate a device and delete the data</span></span>
* <span data-ttu-id="3f37e-118">Bir aygıtı devre dışı bırakın ve verileri tut</span><span class="sxs-lookup"><span data-stu-id="3f37e-118">Deactivate a device and retain the data</span></span>

<span data-ttu-id="3f37e-119">Ayrıca açıklar nasıl devre dışı bırakma ve silme StorSimple sanal cihazlar üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="3f37e-119">It also explains how deactivation and deletion works on a StorSimple virtual device.</span></span>

> [!NOTE]
> <span data-ttu-id="3f37e-120">StorSimple fiziksel veya sanal aygıt devre dışı bırakmadan önce istemciler ve bu cihazda bağımlı konakları silin veya durdurmak emin olun.</span><span class="sxs-lookup"><span data-stu-id="3f37e-120">Before you deactivate a StorSimple physical or virtual device, make sure to stop or delete clients and hosts that depend on that device.</span></span>
> 
> 

## <a name="deactivate-and-delete-data"></a><span data-ttu-id="3f37e-121">Devre dışı bırakın ve verileri silme</span><span class="sxs-lookup"><span data-stu-id="3f37e-121">Deactivate and delete data</span></span>
<span data-ttu-id="3f37e-122">Cihaz tamamen silme ilgilendiğiniz ve cihazdaki verilerin korumak istemiyorsanız, aşağıdaki adımları tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="3f37e-122">If you are interested in deleting the device completely and do not want to retain the data on the device, then complete the following steps.</span></span>

#### <a name="to-deactivate-the-device-and-delete-the-data"></a><span data-ttu-id="3f37e-123">Aygıt devre dışı bırak ve veri silmek için</span><span class="sxs-lookup"><span data-stu-id="3f37e-123">To deactivate the device and delete the data</span></span>
1. <span data-ttu-id="3f37e-124">Bir aygıtı devre dışı bırakma önce tüm birim silmeniz gerekir aygıtla ilişkili kapsayıcıları (ve birimleri).</span><span class="sxs-lookup"><span data-stu-id="3f37e-124">Prior to deactivating a device, you must delete all the volume containers (and the volumes) associated with the device.</span></span> <span data-ttu-id="3f37e-125">Birim kapsayıcıları, ilişkili yedeklemelerinizi yalnızca sildikten sonra silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f37e-125">You can delete volume containers only after you have deleted the associated backups.</span></span>
2. <span data-ttu-id="3f37e-126">Cihaz şu şekilde devre dışı bırakın:</span><span class="sxs-lookup"><span data-stu-id="3f37e-126">Deactivate the device as follows:</span></span>
   
   1. <span data-ttu-id="3f37e-127">StorSimple Yöneticisi hizmetine **aygıtları** sayfasında, sayfanın alt kısmındaki devre dışı bırakın ve istediğiniz cihazı seçin **etkinliğini**.</span><span class="sxs-lookup"><span data-stu-id="3f37e-127">On the StorSimple Manager service **Devices** page, select the device that you wish to deactivate and, at the bottom of the page, click **Deactivate**.</span></span>
   2. <span data-ttu-id="3f37e-128">Bir onay iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="3f37e-128">A confirmation message will appear.</span></span> <span data-ttu-id="3f37e-129">Tıklatın **Evet** devam etmek için.</span><span class="sxs-lookup"><span data-stu-id="3f37e-129">Click **Yes** to continue.</span></span> <span data-ttu-id="3f37e-130">Devre dışı bırakma işlemi başlatmak ve tamamlanması birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="3f37e-130">The deactivate process will start and take a few minutes to complete.</span></span>
3. <span data-ttu-id="3f37e-131">Devre dışı bırakma sonra cihaz tamamen silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f37e-131">After deactivation, you can delete the device completely.</span></span> <span data-ttu-id="3f37e-132">Bir cihazı silme hizmete bağlı aygıtlar listesinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="3f37e-132">Deleting a device removes it from the list of devices connected to the service.</span></span> <span data-ttu-id="3f37e-133">Hizmeti, silinen cihaz artık yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f37e-133">The service can then no longer manage the deleted device.</span></span> <span data-ttu-id="3f37e-134">Cihazı silmek için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="3f37e-134">Use the following steps to delete the device:</span></span>
   
   1. <span data-ttu-id="3f37e-135">StorSimple Yöneticisi hizmetine **aygıtları** sayfasında, silmek istediğiniz devre dışı bırakılan bir cihaz seçin.</span><span class="sxs-lookup"><span data-stu-id="3f37e-135">On the StorSimple Manager service **Devices** page, select a deactivated device that you wish to delete.</span></span>
   2. <span data-ttu-id="3f37e-136">Sayfada alta tıklatın **silmek**.</span><span class="sxs-lookup"><span data-stu-id="3f37e-136">On the bottom on the page, click **Delete**.</span></span>
   3. <span data-ttu-id="3f37e-137">Onayınız istenir.</span><span class="sxs-lookup"><span data-stu-id="3f37e-137">You will be prompted for confirmation.</span></span> <span data-ttu-id="3f37e-138">Tıklatın **Evet** devam etmek için.</span><span class="sxs-lookup"><span data-stu-id="3f37e-138">Click **Yes** to continue.</span></span>
      
      <span data-ttu-id="3f37e-139">Cihazın silinmesi birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="3f37e-139">It may take a few minutes for the device to be deleted.</span></span>

## <a name="deactivate-and-retain-data"></a><span data-ttu-id="3f37e-140">Devre dışı bırakın ve verileri tut</span><span class="sxs-lookup"><span data-stu-id="3f37e-140">Deactivate and retain data</span></span>
<span data-ttu-id="3f37e-141">Cihaz silme ilginizi çekiyor mu, ancak verileri korumak istiyorsanız, aşağıdaki adımları tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="3f37e-141">If you are interested in deleting the device but want to retain the data, then complete the following steps.</span></span>

#### <a name="to-deactivate-a-device-and-retain-the-data"></a><span data-ttu-id="3f37e-142">Bir cihazı devre dışı bırakmak ve verileri korumak için</span><span class="sxs-lookup"><span data-stu-id="3f37e-142">To deactivate a device and retain the data</span></span>
1. <span data-ttu-id="3f37e-143">Aygıt devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="3f37e-143">Deactivate the device.</span></span> <span data-ttu-id="3f37e-144">Tüm birim kapsayıcıları ve anlık görüntüleri cihazın kalır.</span><span class="sxs-lookup"><span data-stu-id="3f37e-144">All the volume containers and the snapshots of the device will remain.</span></span>
   
   1. <span data-ttu-id="3f37e-145">StorSimple Yöneticisi hizmetine **aygıtları** sayfasında, sayfanın alt kısmındaki devre dışı bırakın ve istediğiniz cihazı seçin **etkinliğini**.</span><span class="sxs-lookup"><span data-stu-id="3f37e-145">On the StorSimple Manager service **Devices** page, select the device that you wish to deactivate and, at the bottom of the page, click **Deactivate**.</span></span>
   2. <span data-ttu-id="3f37e-146">Bir onay iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="3f37e-146">A confirmation message will appear.</span></span> <span data-ttu-id="3f37e-147">Tıklatın **Evet** devam etmek için.</span><span class="sxs-lookup"><span data-stu-id="3f37e-147">Click **Yes** to continue.</span></span> <span data-ttu-id="3f37e-148">Devre dışı bırakma işlemi başlatmak ve tamamlanması birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="3f37e-148">The deactivate process will start and take a few minutes to complete.</span></span>
2. <span data-ttu-id="3f37e-149">Şimdi birim kapsayıcıları ve ilişkili anlık görüntüleri üzerinden başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="3f37e-149">You can now fail over the volume containers and the associated snapshots.</span></span> <span data-ttu-id="3f37e-150">Yordamlar için Git [StorSimple cihazınız için yük devretme ve olağanüstü durum kurtarma](storsimple-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="3f37e-150">For procedures, go to [Failover and disaster recovery for your StorSimple device](storsimple-device-failover-disaster-recovery.md).</span></span>
3. <span data-ttu-id="3f37e-151">Devre dışı bırakma ve yük devretme aygıtı tamamen silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f37e-151">After deactivation and failover, you can delete the device completely.</span></span> <span data-ttu-id="3f37e-152">Bir cihazı silme hizmete bağlı aygıtlar listesinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="3f37e-152">Deleting a device removes it from the list of devices connected to the service.</span></span> <span data-ttu-id="3f37e-153">Hizmeti, silinen cihaz artık yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f37e-153">The service can then no longer manage the deleted device.</span></span> <span data-ttu-id="3f37e-154">Cihazı silmek için aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="3f37e-154">Complete the following steps to delete the device:</span></span>
   
   1. <span data-ttu-id="3f37e-155">StorSimple Yöneticisi hizmetine **aygıtları** sayfasında, silmek istediğiniz devre dışı bırakılan bir cihaz seçin.</span><span class="sxs-lookup"><span data-stu-id="3f37e-155">On the StorSimple Manager service **Devices** page, select a deactivated device that you wish to delete.</span></span>
   2. <span data-ttu-id="3f37e-156">Sayfada alta tıklatın **silmek**.</span><span class="sxs-lookup"><span data-stu-id="3f37e-156">On the bottom on the page, click **Delete**.</span></span>
   3. <span data-ttu-id="3f37e-157">Onayınız istenir.</span><span class="sxs-lookup"><span data-stu-id="3f37e-157">You will be prompted for confirmation.</span></span> <span data-ttu-id="3f37e-158">Tıklatın **Evet** devam etmek için.</span><span class="sxs-lookup"><span data-stu-id="3f37e-158">Click **Yes** to continue.</span></span>
      
      <span data-ttu-id="3f37e-159">Cihazın silinmesi birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="3f37e-159">It may take a few minutes for the device to be deleted.</span></span>

## <a name="deactivate-and-delete-a-virtual-device"></a><span data-ttu-id="3f37e-160">Devre dışı bırakın ve sanal cihazı Sil</span><span class="sxs-lookup"><span data-stu-id="3f37e-160">Deactivate and delete a virtual device</span></span>
<span data-ttu-id="3f37e-161">StorSimple sanal cihaz için devre dışı bırakma sanal makineyi kaldırır.</span><span class="sxs-lookup"><span data-stu-id="3f37e-161">For a StorSimple virtual device, deactivation deallocates the virtual machine.</span></span> <span data-ttu-id="3f37e-162">Ardından, sanal makine ve hazırlandığında oluşturulan kaynakları silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f37e-162">You can then delete the virtual machine and the resources created when it was provisioned.</span></span> <span data-ttu-id="3f37e-163">Sanal cihaz devre dışı bırakıldıktan sonra, önceki durumuna geri yüklenemez.</span><span class="sxs-lookup"><span data-stu-id="3f37e-163">After the virtual device is deactivated, it cannot be restored to its previous state.</span></span> 

<span data-ttu-id="3f37e-164">Aşağıdaki eylemleri sonuçlarında devre dışı bırakma:</span><span class="sxs-lookup"><span data-stu-id="3f37e-164">Deactivation results in the following actions:</span></span>

* <span data-ttu-id="3f37e-165">StorSimple sanal cihaz kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="3f37e-165">The StorSimple virtual device is removed.</span></span>
* <span data-ttu-id="3f37e-166">OSDisk ve StorSimple sanal cihaz için oluşturulan veri diskleri kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="3f37e-166">The OSDisk and Data Disks created for the StorSimple virtual device are removed.</span></span>
* <span data-ttu-id="3f37e-167">Barındırılan hizmet ve sağlama işlemi sırasında oluşturulan sanal ağ korunur.</span><span class="sxs-lookup"><span data-stu-id="3f37e-167">The Hosted Service and Virtual Network that were created during provisioning are retained.</span></span> <span data-ttu-id="3f37e-168">Bu varlıklar kullanmıyorsanız, bunları el ile silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f37e-168">If you are not using these entities, you should delete them manually.</span></span>
* <span data-ttu-id="3f37e-169">StorSimple sanal cihaz tarafından oluşturulan bulut anlık görüntüleri korunur.</span><span class="sxs-lookup"><span data-stu-id="3f37e-169">Cloud snapshots created by the StorSimple virtual device are retained.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f37e-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3f37e-170">Next steps</span></span>
* <span data-ttu-id="3f37e-171">Devre dışı bırakılan cihazı fabrika varsayılan ayarlarına geri yüklemek için şu adrese gidin [cihazı fabrika varsayılan ayarlarına sıfırlama](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="3f37e-171">To restore the deactivated device to factory defaults, go to [Reset the device to factory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
* <span data-ttu-id="3f37e-172">Teknik destek için [Microsoft Support başvurun](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="3f37e-172">For technical assistance, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="3f37e-173">StorSimple Yöneticisi hizmetini kullanma hakkında daha fazla bilgi için şuraya gidin [StorSimple Cihazınızı yönetmek için StorSimple Yöneticisi hizmetini kullanma](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="3f37e-173">To learn more about how to use the StorSimple Manager service, go to [Use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span> 

