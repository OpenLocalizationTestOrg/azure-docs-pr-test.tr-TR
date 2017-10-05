---
title: "Devre dışı bırakın ve bir StorSimple 8000 serisi aygıtı silme | Microsoft Docs"
description: "StorSimple cihazı hizmetinden önce devre dışı bırakma ve silme kaldırmayı açıklar."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: 3c00867a29cf8343a57e74e2aabe3971ae6837af
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="deactivate-and-delete-a-storsimple-device"></a><span data-ttu-id="d961e-103">Devre dışı bırakın ve bir StorSimple cihazı Sil</span><span class="sxs-lookup"><span data-stu-id="d961e-103">Deactivate and delete a StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="d961e-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="d961e-104">Overview</span></span>

<span data-ttu-id="d961e-105">Bu makalede, devre dışı bırakın ve bir StorSimple cihaz Yöneticisi hizmetine bağlı bir StorSimple cihazı silmek açıklar.</span><span class="sxs-lookup"><span data-stu-id="d961e-105">This article describes how to deactivate and delete a StorSimple device that is connected to a StorSimple Device Manager service.</span></span> <span data-ttu-id="d961e-106">Bu makalede yer alan yönergeleri StorSimple bulut cihazları dahil olmak üzere yalnızca StorSimple 8000 serisi cihazlar için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d961e-106">The guidance in this article applies only to StorSimple 8000 series devices including the StorSimple Cloud Appliances.</span></span> <span data-ttu-id="d961e-107">Bir StorSimple sanal dizisi kullanıyorsanız, geçin [devre dışı bırakma ve silme StorSimple sanal dizinin](storsimple-virtual-array-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="d961e-107">If you are using a StorSimple Virtual Array, then go to [Deactivate and delete a StorSimple Virtual Array](storsimple-virtual-array-deactivate-and-delete-device.md).</span></span>

<span data-ttu-id="d961e-108">Cihaz ve karşılık gelen StorSimple cihaz Yöneticisi hizmeti arasındaki bağlantı devre dışı bırakma sunucularının.</span><span class="sxs-lookup"><span data-stu-id="d961e-108">Deactivation severs the connection between the device and the corresponding StorSimple Device Manager service.</span></span> <span data-ttu-id="d961e-109">Hizmet dışına StorSimple cihazı (örneğin, değiştirme veya Cihazınızı yükseltmek veya StorSimple artık kullanıyorsanız) almak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d961e-109">You may wish to take a StorSimple device out of service (for example, if you are replacing or upgrading your device or if you are no longer using StorSimple).</span></span> <span data-ttu-id="d961e-110">Öyleyse, silebilmek için önce cihazın devre dışı bırakılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d961e-110">If so, you need to deactivate the device before you can delete it.</span></span>

<span data-ttu-id="d961e-111">Bir aygıtı devre dışı bıraktığınızda, cihazda yerel olarak depolanan tüm verileri artık erişilebilir değil.</span><span class="sxs-lookup"><span data-stu-id="d961e-111">When you deactivate a device, any data that was stored locally on the device is no longer accessible.</span></span> <span data-ttu-id="d961e-112">Yalnızca bulutta depolanan cihaz ile ilişkili verileri kurtarılabilir.</span><span class="sxs-lookup"><span data-stu-id="d961e-112">Only the data associated with the device that was stored in the cloud can be recovered.</span></span>

> [!WARNING]
> <span data-ttu-id="d961e-113">Devre dışı bırakma kalıcı bir işlemdir ve geri alınamaz.</span><span class="sxs-lookup"><span data-stu-id="d961e-113">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="d961e-114">Fabrika ayarlarına sıfırlama sürece devre dışı bırakılan bir cihaz StorSimple cihaz Yöneticisi hizmeti ile kaydedilemedi.</span><span class="sxs-lookup"><span data-stu-id="d961e-114">A deactivated device cannot be registered with the StorSimple Device Manager service unless it is reset to factory defaults.</span></span>
>
> <span data-ttu-id="d961e-115">İşlem siler, cihazda yerel olarak depolanan tüm verileri fabrika ayarlarına sıfırlayamaz.</span><span class="sxs-lookup"><span data-stu-id="d961e-115">The factory reset process deletes all the data that was stored locally on your device.</span></span> <span data-ttu-id="d961e-116">Bu nedenle, bir aygıtı devre dışı bırakmadan önce tüm verilerinizi bir bulut anlık görüntüsünü gerekir.</span><span class="sxs-lookup"><span data-stu-id="d961e-116">Therefore, you must take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="d961e-117">Bu bulut anlık görüntüsü, daha sonraki bir aşamada tüm verileri kurtarmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="d961e-117">This cloud snapshot allows you to recover all the data at a later stage.</span></span>

<span data-ttu-id="d961e-118">Bu öğretici okuduktan sonra aşağıdakileri gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d961e-118">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="d961e-119">Bir cihazı devre dışı bırakmak ve verileri silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d961e-119">Deactivate a device and delete the data.</span></span>
* <span data-ttu-id="d961e-120">Bir aygıtı devre dışı bırakın ve verileri korur.</span><span class="sxs-lookup"><span data-stu-id="d961e-120">Deactivate a device and retain the data.</span></span>

> [!NOTE]
> <span data-ttu-id="d961e-121">Bir StorSimple fiziksel cihazı veya Bulut uygulaması devre dışı bırakmadan önce durdurmak veya istemciler ve bu cihazda bağımlı konakları silin.</span><span class="sxs-lookup"><span data-stu-id="d961e-121">Before you deactivate a StorSimple physical device or cloud appliance, stop or delete clients and hosts that depend on that device.</span></span>


## <a name="deactivate-and-delete-data"></a><span data-ttu-id="d961e-122">Devre dışı bırakın ve verileri silme</span><span class="sxs-lookup"><span data-stu-id="d961e-122">Deactivate and delete data</span></span>

<span data-ttu-id="d961e-123">Cihaz tamamen silme ilgilendiğiniz ve cihazdaki verilerin korumak istemiyorsanız, aşağıdaki adımları tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="d961e-123">If you are interested in deleting the device completely and do not want to retain the data on the device, then complete the following steps.</span></span>

#### <a name="to-deactivate-the-device-and-delete-the-data"></a><span data-ttu-id="d961e-124">Aygıt devre dışı bırak ve veri silmek için</span><span class="sxs-lookup"><span data-stu-id="d961e-124">To deactivate the device and delete the data</span></span>

1. <span data-ttu-id="d961e-125">Bir aygıtı devre dışı bırakmadan önce tüm birim silmeniz gerekir aygıtla ilişkili kapsayıcıları (ve birimleri).</span><span class="sxs-lookup"><span data-stu-id="d961e-125">Before you deactivate a device, you must delete all the volume containers (and the volumes) associated with the device.</span></span> <span data-ttu-id="d961e-126">Birim kapsayıcıları, ilişkili yedeklemelerinizi yalnızca sildikten sonra silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d961e-126">You can delete volume containers only after you have deleted the associated backups.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d961e-127">Bir StorSimple fiziksel cihazı veya Bulut uygulaması devre dışı bırakmadan önce silinen birim kapsayıcısı verileri gerçekten aygıttan silindiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="d961e-127">Before you deactivate a StorSimple physical device or cloud appliance, ensure that the data from the deleted volume container is actually deleted from the device.</span></span> <span data-ttu-id="d961e-128">Bulut tüketim grafikleri izleyebilirsiniz ve sildiğiniz yedeklemeleri nedeniyle bırakma bulut kullanımı gördüğünüzde, daha sonra aygıt devre dışı bırakmak için geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d961e-128">You can monitor the cloud consumption charts and when you see the cloud usage drop because of the backups you have deleted, then you can proceed to deactivate the device.</span></span> <span data-ttu-id="d961e-129">Bu açılan oluşmadan önce aygıt devre dışı bırakırsanız, veri depolama hesabında stranded ve ücretler tahakkuk.</span><span class="sxs-lookup"><span data-stu-id="d961e-129">If you deactivate the device before this drop occurs, the data is stranded in the storage account and accrues charges.</span></span>

2. <span data-ttu-id="d961e-130">Cihaz şu şekilde devre dışı bırakın:</span><span class="sxs-lookup"><span data-stu-id="d961e-130">Deactivate the device as follows:</span></span>
   
   1. <span data-ttu-id="d961e-131">StorSimple Cihaz Yöneticisi hizmetinize gidin ve **Cihazlar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d961e-131">Go to your StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="d961e-132">İçinde **aygıtları** dikey penceresinde, devre dışı bırakmak istediğiniz cihazı seçin sağ tıklatın ve ardından **etkinliğini**.</span><span class="sxs-lookup"><span data-stu-id="d961e-132">In the **Devices** blade, select the device that you wish to deactivate, right-click, and then click **Deactivate**.</span></span>

        ![StorSimple cihazı devre dışı bırakma](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. <span data-ttu-id="d961e-134">İçinde **etkinliğini** dikey penceresinde, onaylamak için aygıt adı yazın ve ardından **etkinliğini**.</span><span class="sxs-lookup"><span data-stu-id="d961e-134">In the **Deactivate** blade, type the device name to confirm and then click **Deactivate**.</span></span> <span data-ttu-id="d961e-135">Devre dışı bırakma işlemi başlatılır ve tamamlanması birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="d961e-135">The deactivate process starts and takes a few minutes to complete.</span></span>

        ![StorSimple cihazı devre dışı bırakma](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)

3. <span data-ttu-id="d961e-137">Devre dışı bırakma sonra cihaz tamamen silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d961e-137">After deactivation, you can delete the device completely.</span></span> <span data-ttu-id="d961e-138">Bir cihazı silme hizmete bağlı aygıtlar listesinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="d961e-138">Deleting a device removes it from the list of devices connected to the service.</span></span> <span data-ttu-id="d961e-139">Hizmeti, silinen cihaz artık yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d961e-139">The service can then no longer manage the deleted device.</span></span> <span data-ttu-id="d961e-140">Cihazı silmek için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="d961e-140">Use the following steps to delete the device:</span></span>
   
   1. <span data-ttu-id="d961e-141">StorSimple Cihaz Yöneticisi hizmetinize gidin ve **Cihazlar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d961e-141">Go to your StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="d961e-142">İçinde **aygıtları** dikey penceresinde, silmek istediğiniz devre dışı bırakılan cihazı seçin sağ tıklatın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="d961e-142">In the **Devices** blade, select the deactivated device that you wish to delete, right-click, and then click **Delete**.</span></span>

        ![StorSimple cihazı devre dışı bırakma](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. <span data-ttu-id="d961e-144">İçinde **silmek** dikey penceresinde, onaylamak için aygıt adı yazın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="d961e-144">In the **Delete** blade, type the device name to confirm and then click **Delete**.</span></span> <span data-ttu-id="d961e-145">Silme işlemini tamamlamak için birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="d961e-145">The deletion takes a few minutes to complete.</span></span>

        ![StorSimple cihazı devre dışı bırakma](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. <span data-ttu-id="d961e-147">Silme işlemi başarıyla tamamlandıktan sonra size bildirilir.</span><span class="sxs-lookup"><span data-stu-id="d961e-147">After the deletion is successfully complete, you are notified.</span></span> <span data-ttu-id="d961e-148">Aygıt listesi ayrıca silme yansıtacak şekilde güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="d961e-148">The device list also updates to reflect the deletion.</span></span>

## <a name="deactivate-and-retain-data"></a><span data-ttu-id="d961e-149">Devre dışı bırakın ve verileri tut</span><span class="sxs-lookup"><span data-stu-id="d961e-149">Deactivate and retain data</span></span>

<span data-ttu-id="d961e-150">Cihaz silme ilginizi çekiyor mu, ancak verileri korumak istiyorsanız, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="d961e-150">If you are interested in deleting the device but want to retain the data, then complete the following steps:</span></span>

#### <a name="to-deactivate-a-device-and-retain-the-data"></a><span data-ttu-id="d961e-151">Bir cihazı devre dışı bırakmak ve verileri korumak için</span><span class="sxs-lookup"><span data-stu-id="d961e-151">To deactivate a device and retain the data</span></span>
1. <span data-ttu-id="d961e-152">Aygıt devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="d961e-152">Deactivate the device.</span></span> <span data-ttu-id="d961e-153">Tüm birim kapsayıcıları ve cihaz anlık görüntüleri olarak kalır.</span><span class="sxs-lookup"><span data-stu-id="d961e-153">All the volume containers and the snapshots of the device remain.</span></span>
   
   1. <span data-ttu-id="d961e-154">StorSimple Cihaz Yöneticisi hizmetinize gidin ve **Cihazlar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d961e-154">Go to your StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="d961e-155">İçinde **aygıtları** dikey penceresinde, devre dışı bırakmak istediğiniz cihazı seçin sağ tıklatın ve ardından **etkinliğini**.</span><span class="sxs-lookup"><span data-stu-id="d961e-155">In the **Devices** blade, select the device that you wish to deactivate, right-click, and then click **Deactivate**.</span></span>

         ![StorSimple cihazı devre dışı bırakma](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. <span data-ttu-id="d961e-157">İçinde **etkinliğini** dikey penceresinde, onaylamak için aygıt adı yazın ve ardından **etkinliğini**.</span><span class="sxs-lookup"><span data-stu-id="d961e-157">In the **Deactivate** blade, type the device name to confirm and then click **Deactivate**.</span></span> <span data-ttu-id="d961e-158">Devre dışı bırakma işlemi başlatılır ve tamamlanması birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="d961e-158">The deactivate process starts and takes a few minutes to complete.</span></span>

         ![StorSimple cihazı devre dışı bırakma](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)
2. <span data-ttu-id="d961e-160">Şimdi birim kapsayıcıları ve ilişkili anlık görüntüleri üzerinden başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="d961e-160">You can now fail over the volume containers and the associated snapshots.</span></span> <span data-ttu-id="d961e-161">Yordamlar için Git [StorSimple cihazınız için yük devretme ve olağanüstü durum kurtarma](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="d961e-161">For procedures, go to [Failover and disaster recovery for your StorSimple device](storsimple-8000-device-failover-disaster-recovery.md).</span></span>
3. <span data-ttu-id="d961e-162">Devre dışı bırakma ve yük devretme aygıtı tamamen silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d961e-162">After deactivation and failover, you can delete the device completely.</span></span> <span data-ttu-id="d961e-163">Bir cihazı silme hizmete bağlı aygıtlar listesinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="d961e-163">Deleting a device removes it from the list of devices connected to the service.</span></span> <span data-ttu-id="d961e-164">Hizmeti, silinen cihaz artık yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d961e-164">The service can then no longer manage the deleted device.</span></span> <span data-ttu-id="d961e-165">Cihazı silmek için aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="d961e-165">To delete the device, complete the following steps:</span></span>
   
   1. <span data-ttu-id="d961e-166">StorSimple Cihaz Yöneticisi hizmetinize gidin ve **Cihazlar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d961e-166">Go to your StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="d961e-167">İçinde **aygıtları** dikey penceresinde, silmek istediğiniz devre dışı bırakılan cihazı seçin sağ tıklatın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="d961e-167">In the **Devices** blade, select the deactivated device that you wish to delete, right-click, and then click **Delete**.</span></span>

       ![StorSimple cihazı devre dışı bırakma](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. <span data-ttu-id="d961e-169">İçinde **silmek** dikey penceresinde, onaylamak için aygıt adı yazın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="d961e-169">In the **Delete** blade, type the device name to confirm and then click **Delete**.</span></span> <span data-ttu-id="d961e-170">Silme işlemini tamamlamak için birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="d961e-170">The deletion takes a few minutes to complete.</span></span>

       ![StorSimple cihazı devre dışı bırakma](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. <span data-ttu-id="d961e-172">Silme işlemi başarıyla tamamlandıktan sonra size bildirilir.</span><span class="sxs-lookup"><span data-stu-id="d961e-172">After the deletion is successfully complete, you are notified.</span></span> <span data-ttu-id="d961e-173">Aygıt listesi ayrıca silme yansıtacak şekilde güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="d961e-173">The device list also updates to reflect the deletion.</span></span>

     
## <a name="deactivate-and-delete-a-cloud-appliance"></a><span data-ttu-id="d961e-174">Devre dışı bırakın ve bir bulut uygulaması Sil</span><span class="sxs-lookup"><span data-stu-id="d961e-174">Deactivate and delete a cloud appliance</span></span>

<span data-ttu-id="d961e-175">Bir StorSimple bulut uygulaması için devre dışı bırakma portalından kaldırır ve sanal makine ve hazırlandığında oluşturulan kaynakları siler.</span><span class="sxs-lookup"><span data-stu-id="d961e-175">For a StorSimple Cloud Appliance, deactivation from the portal deallocates and deletes the virtual machine, and the resources created when it was provisioned.</span></span> <span data-ttu-id="d961e-176">Bulut gereci devre dışı bırakıldıktan sonra, önceki durumuna geri yüklenemez.</span><span class="sxs-lookup"><span data-stu-id="d961e-176">After the cloud appliance is deactivated, it cannot be restored to its previous state.</span></span>

![StorSimple bulut uygulaması devre dışı bırakma](./media/storsimple-8000-deactivate-and-delete-device/deactivate7.png)

<span data-ttu-id="d961e-178">Aşağıdaki eylemleri sonuçlarında devre dışı bırakma:</span><span class="sxs-lookup"><span data-stu-id="d961e-178">Deactivation results in the following actions:</span></span>

* <span data-ttu-id="d961e-179">StorSimple bulut uygulaması hizmetten kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="d961e-179">The StorSimple Cloud Appliance is removed from the service.</span></span>
* <span data-ttu-id="d961e-180">StorSimple bulut uygulaması için sanal makine silinir.</span><span class="sxs-lookup"><span data-stu-id="d961e-180">The virtual machine for the StorSimple Cloud Appliance is deleted.</span></span>
* <span data-ttu-id="d961e-181">İşletim sistemi diski ve StorSimple bulut uygulaması için oluşturulan veri diskleri kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="d961e-181">The OS disk and data disks created for the StorSimple Cloud Appliance are removed.</span></span>
* <span data-ttu-id="d961e-182">Barındırılan hizmet ve sağlama işlemi sırasında oluşturulan sanal ağ korunur.</span><span class="sxs-lookup"><span data-stu-id="d961e-182">The hosted service and Virtual Network that were created during provisioning are retained.</span></span> <span data-ttu-id="d961e-183">Bu varlıklar kullanmıyorsanız, bunları el ile silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d961e-183">If you are not using these entities, you should delete them manually.</span></span>
* <span data-ttu-id="d961e-184">StorSimple bulut uygulaması tarafından oluşturulan bulut anlık görüntüleri korunur.</span><span class="sxs-lookup"><span data-stu-id="d961e-184">Cloud snapshots created by the StorSimple Cloud Appliance are retained.</span></span>

<span data-ttu-id="d961e-185">Bulut uygulaması devre dışı bırakıldıktan sonra aygıt listesinden silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d961e-185">After the cloud appliance is deactivated, you can delete it from the list of devices.</span></span> <span data-ttu-id="d961e-186">Devre dışı bırakılmış aygıt, sağ tıklatın ve ardından seçin **silmek**.</span><span class="sxs-lookup"><span data-stu-id="d961e-186">Select the deactivated device, right-click, and then click **Delete**.</span></span> <span data-ttu-id="d961e-187">StorSimple, cihaz silindikten sonra ve aygıtları güncelleştirmelerinin listesini bildirir.</span><span class="sxs-lookup"><span data-stu-id="d961e-187">StorSimple notifies you once the device is deleted and the list of devices updates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d961e-188">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d961e-188">Next steps</span></span>

* <span data-ttu-id="d961e-189">Devre dışı bırakılan cihazı fabrika varsayılan ayarlarına geri yüklemek için şu adrese gidin [cihazı fabrika varsayılan ayarlarına sıfırlama](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="d961e-189">To restore the deactivated device to factory defaults, go to [Reset the device to factory default settings](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
* <span data-ttu-id="d961e-190">Teknik destek için [Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="d961e-190">For technical assistance, [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="d961e-191">StorSimple cihaz Yöneticisi hizmetini kullanma hakkında daha fazla bilgi için şuraya gidin [StorSimple Cihazınızı yönetmek için StorSimple cihaz Yöneticisi hizmetini kullanma](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="d961e-191">To learn more about how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

