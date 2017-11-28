---
title: aaaDeactivate ve Microsoft Azure StorSimple sanal dizinin silme | Microsoft Docs
description: "Açıklar nasıl tooremove StorSimple cihazı hizmetinden önce devre dışı bırakma ve silme."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: a929f5bc-03e2-4b01-b925-973db236f19f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: b1f3ddb5822d19965739777e238af19b507df984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a><span data-ttu-id="c08ad-103">Devre dışı bırakın ve bir StorSimple sanal dizi Sil</span><span class="sxs-lookup"><span data-stu-id="c08ad-103">Deactivate and delete a StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="c08ad-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="c08ad-104">Overview</span></span>

<span data-ttu-id="c08ad-105">StorSimple sanal dizinin devre dışı bıraktığınızda, hello cihaz ve hello karşılık gelen StorSimple cihaz Yöneticisi hizmeti arasındaki hello bağlantıyı kesmek.</span><span class="sxs-lookup"><span data-stu-id="c08ad-105">When you deactivate a StorSimple Virtual Array, you break hello connection between hello device and hello corresponding StorSimple Device Manager service.</span></span> <span data-ttu-id="c08ad-106">Bu öğretici açıklar nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="c08ad-106">This tutorial explains how to:</span></span>

* <span data-ttu-id="c08ad-107">Bir cihazı devre dışı</span><span class="sxs-lookup"><span data-stu-id="c08ad-107">Deactivate a device</span></span> 
* <span data-ttu-id="c08ad-108">Devre dışı bırakılmış bir aygıtı silme</span><span class="sxs-lookup"><span data-stu-id="c08ad-108">Delete a deactivated device</span></span>

<span data-ttu-id="c08ad-109">Bu makalede Hello bilgiler tooStorSimple sanal diziler yalnızca geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="c08ad-109">hello information in this article applies tooStorSimple Virtual Arrays only.</span></span> <span data-ttu-id="c08ad-110">8000 serisi hakkında daha fazla bilgi için toohow çok gidin[bir cihazı silmek veya devre dışı bırakma](storsimple-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="c08ad-110">For information on 8000 series, go toohow too[deactivate or delete a device](storsimple-deactivate-and-delete-device.md).</span></span>

## <a name="when-toodeactivate"></a><span data-ttu-id="c08ad-111">Zaman toodeactivate?</span><span class="sxs-lookup"><span data-stu-id="c08ad-111">When toodeactivate?</span></span>

<span data-ttu-id="c08ad-112">Devre dışı bırakma kalıcı bir işlemdir ve geri alınamaz.</span><span class="sxs-lookup"><span data-stu-id="c08ad-112">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="c08ad-113">Merhaba StorSimple cihaz Yöneticisi hizmeti ile yeniden devre dışı bırakılmış bir aygıt kaydedilemiyor.</span><span class="sxs-lookup"><span data-stu-id="c08ad-113">You cannot register a deactivated device with hello StorSimple Device Manager service again.</span></span> <span data-ttu-id="c08ad-114">Toodeactivate ihtiyacınız ve senaryoları aşağıdaki hello StorSimple sanal dizisinde silin:</span><span class="sxs-lookup"><span data-stu-id="c08ad-114">You may need toodeactivate and delete a StorSimple Virtual Array in hello following scenarios:</span></span>

* <span data-ttu-id="c08ad-115">**Planlanan yük devretme** : Cihazınızı çevrimiçi olduğundan ve Cihazınızı toofail planlayın.</span><span class="sxs-lookup"><span data-stu-id="c08ad-115">**Planned failover** : Your device is online and you plan toofail over your device.</span></span> <span data-ttu-id="c08ad-116">Tooupgrade tooa büyük cihaz planlıyorsanız, Cihazınızı toofail gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="c08ad-116">If you are planning tooupgrade tooa larger device, you may need toofail over your device.</span></span> <span data-ttu-id="c08ad-117">Merhaba veri sahipliği aktarılır ve hello yük devretme işlemi tamamlandıktan sonra hello kaynak cihaz otomatik olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="c08ad-117">After hello data ownership is transferred and hello failover is complete, hello source device is automatically deleted.</span></span>
* <span data-ttu-id="c08ad-118">**Planlanmamış yük devretme** : Cihazınızı çevrimdışıysa ve hello aygıt üzerinden toofail gerekir.</span><span class="sxs-lookup"><span data-stu-id="c08ad-118">**Unplanned failover** : Your device is offline and you need toofail over hello device.</span></span> <span data-ttu-id="c08ad-119">Bu senaryo, aşağı birincil Cihazınızı hello veri merkezinde bir kesinti olduğunda ve bir olağanüstü durum sırasında ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="c08ad-119">This scenario may occur during a disaster when there is an outage in hello datacenter and your primary device is down.</span></span> <span data-ttu-id="c08ad-120">Merhaba aygıt tooa ikincil aygıt üzerinden toofail planlayın.</span><span class="sxs-lookup"><span data-stu-id="c08ad-120">You plan toofail over hello device tooa secondary device.</span></span> <span data-ttu-id="c08ad-121">Merhaba veri sahipliği aktarılır ve hello yük devretme işlemi tamamlandıktan sonra hello kaynak cihaz otomatik olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="c08ad-121">After hello data ownership is transferred and hello failover is complete, hello source device is automatically deleted.</span></span>
* <span data-ttu-id="c08ad-122">**Yetkisini** : toodecommission hello aygıt istiyor.</span><span class="sxs-lookup"><span data-stu-id="c08ad-122">**Decommission** : You want toodecommission hello device.</span></span> <span data-ttu-id="c08ad-123">Bu toofirst gerektirir hello aygıt devre dışı bırakın ve ardından silin.</span><span class="sxs-lookup"><span data-stu-id="c08ad-123">This requires you toofirst deactivate hello device and then delete it.</span></span> <span data-ttu-id="c08ad-124">Bir aygıtı devre dışı bıraktığınızda, yerel olarak depolanan tüm verileri artık erişemez.</span><span class="sxs-lookup"><span data-stu-id="c08ad-124">When you deactivate a device, you can no longer access any data that is stored locally.</span></span> <span data-ttu-id="c08ad-125">Merhaba bulutta depolanan erişim ve kurtarma hello veriler yalnızca kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c08ad-125">You can only access and recover hello data stored in hello cloud.</span></span> <span data-ttu-id="c08ad-126">Tookeep hello aygıt verilerini sonra devre dışı bırakmayı planlıyorsanız, bir cihazın devre dışı bırakmadan önce tüm verilerinizin bulut anlık görüntüsü almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c08ad-126">If you plan tookeep hello device data after deactivation, then you should take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="c08ad-127">Bu bulut anlık görüntüsü toorecover sağlayan tüm verileri daha sonraki bir aşamada hello.</span><span class="sxs-lookup"><span data-stu-id="c08ad-127">This cloud snapshot allows you toorecover all hello data at a later stage.</span></span>

## <a name="deactivate-a-device"></a><span data-ttu-id="c08ad-128">Bir cihazı devre dışı</span><span class="sxs-lookup"><span data-stu-id="c08ad-128">Deactivate a device</span></span>

<span data-ttu-id="c08ad-129">toodeactivate Cihazınızı hello aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="c08ad-129">toodeactivate your device, perform hello following steps.</span></span>

#### <a name="toodeactivate-hello-device"></a><span data-ttu-id="c08ad-130">toodeactivate hello cihaz</span><span class="sxs-lookup"><span data-stu-id="c08ad-130">toodeactivate hello device</span></span>

1. <span data-ttu-id="c08ad-131">Hizmetiniz, çok Git**Yönetim > aygıtları**.</span><span class="sxs-lookup"><span data-stu-id="c08ad-131">In your service, go too**Management > Devices**.</span></span> <span data-ttu-id="c08ad-132">Merhaba, **aygıtları** dikey penceresinde, tıklatın ve select hello aygıt toodeactivate istiyor.</span><span class="sxs-lookup"><span data-stu-id="c08ad-132">In hello **Devices** blade, click and select hello device that you wish toodeactivate.</span></span>
   
    ![Aygıt toodeactivate seçin](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. <span data-ttu-id="c08ad-134">İçinde **cihaz Pano** dikey penceresinde tıklatın **... Daha fazla** ve hello listesinden **etkinliğini**.</span><span class="sxs-lookup"><span data-stu-id="c08ad-134">In your **Device dashboard** blade, click **… More** and from hello list, select **Deactivate**.</span></span>
   
    ![Tıklatın devre dışı bırakma](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. <span data-ttu-id="c08ad-136">Merhaba, **etkinliğini** dikey penceresinde, tür hello aygıt adı ve ardından **etkinliğini**.</span><span class="sxs-lookup"><span data-stu-id="c08ad-136">In hello **Deactivate** blade, type hello device name and then click **Deactivate**.</span></span> 
   
    ![Onayla devre dışı bırakma](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    <span data-ttu-id="c08ad-138">Merhaba işlemi başlar devre dışı bırakın ve birkaç dakika toocomplete alır.</span><span class="sxs-lookup"><span data-stu-id="c08ad-138">hello deactivate process starts and takes a few minutes toocomplete.</span></span>
   
    ![Devam eden devre dışı bırakma](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. <span data-ttu-id="c08ad-140">Devre dışı bırakma sonra cihazların Merhaba listesini yeniler.</span><span class="sxs-lookup"><span data-stu-id="c08ad-140">After deactivation, hello list of devices refreshes.</span></span>
   
    ![Tam devre dışı bırakma](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    <span data-ttu-id="c08ad-142">Bu cihaz artık silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c08ad-142">You can now delete this device.</span></span>

## <a name="delete-hello-device"></a><span data-ttu-id="c08ad-143">Merhaba aygıtı silme</span><span class="sxs-lookup"><span data-stu-id="c08ad-143">Delete hello device</span></span>

<span data-ttu-id="c08ad-144">Bir aygıtın toobe ilk devre dışı bırakılan toodelete onu.</span><span class="sxs-lookup"><span data-stu-id="c08ad-144">A device has toobe first deactivated toodelete it.</span></span> <span data-ttu-id="c08ad-145">Bir cihazı silme hello aygıtları bağlı toohello hizmet listesinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="c08ad-145">Deleting a device removes it from hello list of devices connected toohello service.</span></span> <span data-ttu-id="c08ad-146">Merhaba hizmeti artık silinen hello aygıt yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c08ad-146">hello service can then no longer manage hello deleted device.</span></span> <span data-ttu-id="c08ad-147">Merhaba veri Hello cihaz ile ilişkili ancak hello bulutta kalır.</span><span class="sxs-lookup"><span data-stu-id="c08ad-147">hello data associated with hello device however remains in hello cloud.</span></span> <span data-ttu-id="c08ad-148">Bu veriler, ardından ücretler tahakkuk.</span><span class="sxs-lookup"><span data-stu-id="c08ad-148">This data then accrues charges.</span></span>

<span data-ttu-id="c08ad-149">toodelete hello aygıt hello aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="c08ad-149">toodelete hello device, perform hello following steps.</span></span>

#### <a name="toodelete-hello-device"></a><span data-ttu-id="c08ad-150">toodelete hello cihaz</span><span class="sxs-lookup"><span data-stu-id="c08ad-150">toodelete hello device</span></span>

1. <span data-ttu-id="c08ad-151">StorSimple Aygıt Yöneticisi'nde çok Git**Yönetim > aygıtları**.</span><span class="sxs-lookup"><span data-stu-id="c08ad-151">In your StorSimple Device Manager, go too**Management > Devices**.</span></span> <span data-ttu-id="c08ad-152">Merhaba, **aygıtları** dikey penceresinde toodelete istediğiniz devre dışı bırakılan bir cihaz seçin.</span><span class="sxs-lookup"><span data-stu-id="c08ad-152">In hello **Devices** blade, select a deactivated device that you wish toodelete.</span></span>
2. <span data-ttu-id="c08ad-153">Merhaba, **cihaz Pano** dikey penceresinde tıklatın **... Daha fazla** ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="c08ad-153">In hello **Device dashboard** blade, click **… More** and then click **Delete**.</span></span>
   
   ![Aygıt toodelete seçin](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. <span data-ttu-id="c08ad-155">Merhaba, **silmek** dikey penceresinde, tür hello adını aygıt tooconfirm hello silme ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="c08ad-155">In hello **Delete** blade, type hello name of your device tooconfirm hello deletion and then click **Delete**.</span></span> <span data-ttu-id="c08ad-156">Silme hello aygıt hello aygıtla ilişkilendirilen hello bulut verilerini silmez.</span><span class="sxs-lookup"><span data-stu-id="c08ad-156">Deleting hello device does not delete hello cloud data associated with hello device.</span></span> 
   
   ![Silmeyi onayla](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. <span data-ttu-id="c08ad-158">Merhaba silme işlemi başlatır ve birkaç dakika toocomplete alır.</span><span class="sxs-lookup"><span data-stu-id="c08ad-158">hello deletion starts and takes a few minutes toocomplete.</span></span>
   
   ![Silme sürüyor](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    <span data-ttu-id="c08ad-160">Merhaba cihaz silindikten sonra cihazların Merhaba güncelleştirilmiş listesini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c08ad-160">After hello device is deleted, you can view hello updated list of devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c08ad-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c08ad-161">Next steps</span></span>

* <span data-ttu-id="c08ad-162">Hakkında bilgi için üzerinde toofail Git çok[yük devretme ve olağanüstü durum kurtarma, StorSimple sanal dizinin](storsimple-virtual-array-failover-dr.md).</span><span class="sxs-lookup"><span data-stu-id="c08ad-162">For information on how toofail over, go too[Failover and disaster recovery of your StorSimple Virtual Array](storsimple-virtual-array-failover-dr.md).</span></span>

* <span data-ttu-id="c08ad-163">toolearn toouse hello StorSimple cihaz Yöneticisi hizmeti, Git çok nasıl hakkında daha fazla bilgi[kullanın, StorSimple sanal dizinizi StorSimple cihaz Yöneticisi hizmeti tooadminister hello](storsimple-virtual-array-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="c08ad-163">toolearn more about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md).</span></span> 

