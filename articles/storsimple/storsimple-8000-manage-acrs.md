---
title: "StorSimple erişim denetimi kayıtları yönetme | Microsoft Docs"
description: "Erişim denetimi kayıtları (ACRs) barındıran bir birime bağlanabilir belirlemek için StorSimple cihazında nasıl kullanılacağını açıklar."
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
ms.date: 05/31/2017
ms.author: alkohli
ms.openlocfilehash: 9173e34f889ce1c082b20bb382cb6ca9a03dd797
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-access-control-records"></a><span data-ttu-id="3eab3-103">Erişim denetimi kayıtları yönetmek için StorSimple Yöneticisi hizmetini kullanma</span><span class="sxs-lookup"><span data-stu-id="3eab3-103">Use the StorSimple Manager service to manage access control records</span></span>

## <a name="overview"></a><span data-ttu-id="3eab3-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="3eab3-104">Overview</span></span>
<span data-ttu-id="3eab3-105">Erişim denetimi kayıtları (ACRs), StorSimple cihaz üzerindeki bir birimi hangi ana bilgisayarların bağlanabileceği belirtmenize olanak verir.</span><span class="sxs-lookup"><span data-stu-id="3eab3-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple device.</span></span> <span data-ttu-id="3eab3-106">ACRs belirli bir birimi ayarlayın ve ana bilgisayarların iSCSI nitelikli adlar (IQN'ler) içerir.</span><span class="sxs-lookup"><span data-stu-id="3eab3-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="3eab3-107">Bir ana bilgisayara bir birime bağlanmaya çalıştığında, cihaz IQN adının bu birimde ACR ilişkili ve bir eşleşme varsa, ardından bağlantı kurulur denetler.</span><span class="sxs-lookup"><span data-stu-id="3eab3-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name and if there is a match, then the connection is established.</span></span> <span data-ttu-id="3eab3-108">Erişim denetimi kayıtları **yapılandırma** StorSimple cihaz Yöneticisi hizmeti dikey pencerenize bölümünü konak karşılık gelen IQN'ler ile tüm erişim denetimi kayıtları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="3eab3-108">The access control records in the **Configuration** section of your StorSimple Device Manager service blade display all the access control records with the corresponding IQNs of the hosts.</span></span>

<span data-ttu-id="3eab3-109">Bu öğretici ACR ile ilgili aşağıdaki ortak görevler açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="3eab3-109">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="3eab3-110">Bir erişim denetimi kaydı ekleme</span><span class="sxs-lookup"><span data-stu-id="3eab3-110">Add an access control record</span></span>
* <span data-ttu-id="3eab3-111">Bir erişim denetimi kaydı Düzenle</span><span class="sxs-lookup"><span data-stu-id="3eab3-111">Edit an access control record</span></span>
* <span data-ttu-id="3eab3-112">Bir erişim denetimi kaydını sil</span><span class="sxs-lookup"><span data-stu-id="3eab3-112">Delete an access control record</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="3eab3-113">Bir ACR bir birime atarken, bu birim bozuk olabilir çünkü birim aynı anda birden fazla kümelenmemiş ana bilgisayar tarafından erişmediğinden dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="3eab3-113">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span>
> * <span data-ttu-id="3eab3-114">Bir ACR bir birimden silerken, silme, okuma-yazma kesilme neden olabilir çünkü karşılık gelen ana birim eriştiğini değil emin olun.</span><span class="sxs-lookup"><span data-stu-id="3eab3-114">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>

## <a name="get-the-iqn"></a><span data-ttu-id="3eab3-115">IQN'sini Al</span><span class="sxs-lookup"><span data-stu-id="3eab3-115">Get the IQN</span></span>

<span data-ttu-id="3eab3-116">Windows Server 2012 çalıştıran bir Windows konağının IQN'sini almak için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="3eab3-116">Perform the following steps to get the IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a><span data-ttu-id="3eab3-117">Bir erişim denetimi kaydı ekleme</span><span class="sxs-lookup"><span data-stu-id="3eab3-117">Add an access control record</span></span>
<span data-ttu-id="3eab3-118">Kullandığınız **yapılandırma** ACRs eklemek için StorSimple cihaz Yöneticisi hizmeti dikey bölümde.</span><span class="sxs-lookup"><span data-stu-id="3eab3-118">You use the **Configuration** section in the StorSimple Device Manager service blade to add ACRs.</span></span> <span data-ttu-id="3eab3-119">Genellikle, bir birimle bir ACR ilişkilendireceğiniz.</span><span class="sxs-lookup"><span data-stu-id="3eab3-119">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="3eab3-120">Bir ACR eklemek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="3eab3-120">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-acr"></a><span data-ttu-id="3eab3-121">Bir ACR eklemek için</span><span class="sxs-lookup"><span data-stu-id="3eab3-121">To add an ACR</span></span>

1. <span data-ttu-id="3eab3-122">StorSimple cihaz Yöneticisi hizmetinize gidin, hizmet adına çift tıklayın ve ardından içinde **yapılandırma** 'yi tıklatın **erişim denetimi kayıtları**.</span><span class="sxs-lookup"><span data-stu-id="3eab3-122">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="3eab3-123">İçinde **erişim denetimi kayıtları** dikey penceresinde tıklatın **+ ACR eklemek**.</span><span class="sxs-lookup"><span data-stu-id="3eab3-123">In the **Access control records** blade, click **+ Add ACR**.</span></span>

    ![ACR Ekle'yi tıklatın](./media/storsimple-8000-manage-acrs/createacr1.png)

3. <span data-ttu-id="3eab3-125">İçinde **eklemek ACR** dikey penceresinde, aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="3eab3-125">In the **Add ACR** blade, do the following steps:</span></span>

    1. <span data-ttu-id="3eab3-126">Bir ad verin sağlayın.</span><span class="sxs-lookup"><span data-stu-id="3eab3-126">Supply a name for your ACR.</span></span>
    
    2. <span data-ttu-id="3eab3-127">Windows Server konağınızda altında IQN adını sağlayın **iSCSI başlatıcısı adı (IQN)**.</span><span class="sxs-lookup"><span data-stu-id="3eab3-127">Provide the IQN name of your Windows Server host under **iSCSI Initiator Name (IQN)**.</span></span>

    3. <span data-ttu-id="3eab3-128">Tıklatın **Ekle** ACR oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="3eab3-128">Click **Add** to create the ACR.</span></span>

        ![ACR Ekle'yi tıklatın](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  <span data-ttu-id="3eab3-130">Yeni eklenen ACR ACRs Tablo listesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="3eab3-130">The newly added ACR will display in the tabular listing of ACRs.</span></span>

    ![ACR Ekle'yi tıklatın](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a><span data-ttu-id="3eab3-132">Bir erişim denetimi kaydı Düzenle</span><span class="sxs-lookup"><span data-stu-id="3eab3-132">Edit an access control record</span></span>
<span data-ttu-id="3eab3-133">Kullandığınız **yapılandırma** ACRs düzenlemek için StorSimple cihaz Yöneticisi hizmeti dikey bölümde.</span><span class="sxs-lookup"><span data-stu-id="3eab3-133">You use the **Configuration** section in the StorSimple Device Manager service blade to edit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="3eab3-134">Şu anda kullanımda olmayan ACRs değiştirmeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="3eab3-134">It is recommended that you modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="3eab3-135">Şu anda kullanılmakta olan bir birimi ile ilişkili bir ACR düzenlemek için önce birim çevrimdışı duruma getirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3eab3-135">To edit an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>

<span data-ttu-id="3eab3-136">Bir ACR düzenlemek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="3eab3-136">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-access-control-record"></a><span data-ttu-id="3eab3-137">Bir erişim denetimi kaydını düzenlemek için</span><span class="sxs-lookup"><span data-stu-id="3eab3-137">To edit an access control record</span></span>
1.  <span data-ttu-id="3eab3-138">StorSimple cihaz Yöneticisi hizmetinize gidin, hizmet adına çift tıklayın ve ardından içinde **yapılandırma** 'yi tıklatın **erişim denetimi kayıtları**.</span><span class="sxs-lookup"><span data-stu-id="3eab3-138">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>

    ![Erişim denetimi kayıtları gidin](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="3eab3-140">Erişim denetimi kayıtları Tablo listesi, tıklayın ve değiştirmek istediğiniz ACR seçin.</span><span class="sxs-lookup"><span data-stu-id="3eab3-140">In the tabular listing of the access control records, click and select the ACR that you wish to modify.</span></span>

    ![Erişim denetimi kayıtları düzenleme](./media/storsimple-8000-manage-acrs/editacr1.png)

3. <span data-ttu-id="3eab3-142">İçinde **düzenleme erişim denetimi kaydı** dikey penceresinde, başka bir ana bilgisayara karşılık gelen farklı bir IQN sağlayın.</span><span class="sxs-lookup"><span data-stu-id="3eab3-142">In the **Edit access control record** blade, provide a different IQN corresponding to another host.</span></span>

    ![Erişim denetimi kayıtları düzenleme](./media/storsimple-8000-manage-acrs/editacr2.png)

4. <span data-ttu-id="3eab3-144">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3eab3-144">Click **Save**.</span></span> <span data-ttu-id="3eab3-145">Onayınız istendiğinde **Evet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3eab3-145">When prompted for confirmation, click **Yes**.</span></span> 

    ![Erişim denetimi kayıtları düzenleme](./media/storsimple-8000-manage-acrs/editacr3.png)

5. <span data-ttu-id="3eab3-147">ACR güncelleştirildiğinde size bildirilir.</span><span class="sxs-lookup"><span data-stu-id="3eab3-147">You are notified when the ACR is updated.</span></span> <span data-ttu-id="3eab3-148">Tablo listeleme ayrıca değişikliği yansıtacak şekilde güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="3eab3-148">The tabular listing also updates to reflect the change.</span></span>

   
## <a name="delete-an-access-control-record"></a><span data-ttu-id="3eab3-149">Bir erişim denetimi kaydını sil</span><span class="sxs-lookup"><span data-stu-id="3eab3-149">Delete an access control record</span></span>
<span data-ttu-id="3eab3-150">Kullandığınız **yapılandırma** ACRs silmek için StorSimple cihaz Yöneticisi hizmeti dikey bölümde.</span><span class="sxs-lookup"><span data-stu-id="3eab3-150">You use the **Configuration** section in the StorSimple Device Manager service blade to delete ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="3eab3-151">Şu anda kullanımda olmayan ACRs silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3eab3-151">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="3eab3-152">Şu anda kullanılmakta olan bir birimi ile ilişkili bir ACR silmek için önce birim çevrimdışı duruma getirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3eab3-152">To delete an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>

<span data-ttu-id="3eab3-153">Bir erişim denetimi kaydını silmek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="3eab3-153">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="3eab3-154">Bir erişim denetimi kaydını silmek için</span><span class="sxs-lookup"><span data-stu-id="3eab3-154">To delete an access control record</span></span>
1.  <span data-ttu-id="3eab3-155">StorSimple cihaz Yöneticisi hizmetinize gidin, hizmet adına çift tıklayın ve ardından içinde **yapılandırma** 'yi tıklatın **erişim denetimi kayıtları**.</span><span class="sxs-lookup"><span data-stu-id="3eab3-155">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>

    ![Erişim denetimi kayıtları gidin](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="3eab3-157">Erişim denetimi kayıtları Tablo listesi, tıklayın ve silmek istediğiniz ACR seçin.</span><span class="sxs-lookup"><span data-stu-id="3eab3-157">In the tabular listing of the access control records, click and select the ACR that you wish to delete.</span></span>

    ![Erişim denetimi kayıtları gidin](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. <span data-ttu-id="3eab3-159">Bağlam menüsü çağırma ve seçmek için sağ **silmek**.</span><span class="sxs-lookup"><span data-stu-id="3eab3-159">Right-click to invoke the context menu and select **Delete**.</span></span>

    ![Erişim denetimi kayıtları gidin](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. <span data-ttu-id="3eab3-161">Onaylamanız istendiğinde, bilgileri gözden geçirin ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="3eab3-161">When prompted for confirmation, review the information and then click **Delete**.</span></span>

    ![Erişim denetimi kayıtları gidin](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. <span data-ttu-id="3eab3-163">Silme işlemi tamamlandığında size bildirilir.</span><span class="sxs-lookup"><span data-stu-id="3eab3-163">You are notified when the deletion completes.</span></span> <span data-ttu-id="3eab3-164">Sekmeli liste silme yansıtacak şekilde güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="3eab3-164">The tabular listing is updated to reflect the deletion.</span></span>

    ![Erişim denetimi kayıtları gidin](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a><span data-ttu-id="3eab3-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3eab3-166">Next steps</span></span>
* <span data-ttu-id="3eab3-167">Daha fazla bilgi edinmek [StorSimple birimlerini yönetme](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="3eab3-167">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span>
* <span data-ttu-id="3eab3-168">Daha fazla bilgi edinmek [StorSimple Cihazınızı yönetmek için StorSimple Yöneticisi hizmetini kullanma](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="3eab3-168">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

