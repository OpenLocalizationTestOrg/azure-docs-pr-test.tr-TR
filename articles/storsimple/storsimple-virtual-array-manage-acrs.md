---
title: "StorSimple sanal dizi için erişim denetim kayıtlarını yönetme | Microsoft Docs"
description: "StorSimple sanal dizinin bir birimde hangi ana bilgisayarların bağlanabileceği belirlemek için erişim denetim kayıtlarının (ACRs) nasıl yönetildiğini açıklar."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e154bb4f-faab-4d92-a593-900c3ddc9595
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2ce65aa4efba735305208f7a6d761bc2814d1b8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-device-manager-to-manage-access-control-records-for-storsimple-virtual-array"></a><span data-ttu-id="944a0-103">StorSimple sanal dizi için erişim denetimi kayıtları yönetmek için StorSimple cihaz Yöneticisi'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="944a0-103">Use StorSimple Device Manager to manage access control records for StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="944a0-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="944a0-104">Overview</span></span>

<span data-ttu-id="944a0-105">Erişim denetimi kayıtları (ACRs), StorSimple sanal dizinin (olarak da bilinen StorSimple şirket içi sanal aygıtı) bir birimde hangi ana bilgisayarların bağlanabileceği belirtmenize olanak verir.</span><span class="sxs-lookup"><span data-stu-id="944a0-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple Virtual Array (also known as the StorSimple on-premises virtual device).</span></span> <span data-ttu-id="944a0-106">ACRs belirli bir birimi ayarlayın ve ana bilgisayarların iSCSI nitelikli adlar (IQN'ler) içerir.</span><span class="sxs-lookup"><span data-stu-id="944a0-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="944a0-107">Bir ana bilgisayara bir birime bağlanmaya çalıştığında, cihaz IQN adının bu birimde ilişkili ACR denetler ve bir eşleşme varsa, ardından bağlantı kurulur.</span><span class="sxs-lookup"><span data-stu-id="944a0-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name, and if there is a match, then the connection is established.</span></span> <span data-ttu-id="944a0-108">**Erişim denetimi kayıtları** içinde dikey **yapılandırma** Aygıt Yöneticisi'ni hizmetinizi bölümünü konak karşılık gelen IQN'ler ile tüm erişim denetimi kayıtları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="944a0-108">The **Access control records** blade within the **Configuration** section of your Device Manager service displays all the access control records with the corresponding IQNs of the hosts.</span></span>

![Erişim denetimi kayıtlarını yönetme](./media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

<span data-ttu-id="944a0-110">Bu öğretici ACR ile ilgili aşağıdaki ortak görevler açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="944a0-110">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="944a0-111">IQN'sini Al</span><span class="sxs-lookup"><span data-stu-id="944a0-111">Get the IQN</span></span>
* <span data-ttu-id="944a0-112">Bir erişim denetimi kaydı ekleme</span><span class="sxs-lookup"><span data-stu-id="944a0-112">Add an access control record</span></span>
* <span data-ttu-id="944a0-113">Bir erişim denetimi kaydı Düzenle</span><span class="sxs-lookup"><span data-stu-id="944a0-113">Edit an access control record</span></span>
* <span data-ttu-id="944a0-114">Bir erişim denetimi kaydını sil</span><span class="sxs-lookup"><span data-stu-id="944a0-114">Delete an access control record</span></span>

> [!IMPORTANT]
> 
> * <span data-ttu-id="944a0-115">Bir ACR bir birime atarken, bu birim bozuk olabilir çünkü birim aynı anda birden fazla kümelenmemiş ana bilgisayar tarafından erişmediğinden dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="944a0-115">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span>
> * <span data-ttu-id="944a0-116">Bir ACR bir birimden silerken, silme, okuma-yazma kesilme neden olabilir çünkü karşılık gelen ana birim eriştiğini değil emin olun.</span><span class="sxs-lookup"><span data-stu-id="944a0-116">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>


## <a name="get-the-iqn"></a><span data-ttu-id="944a0-117">IQN'sini Al</span><span class="sxs-lookup"><span data-stu-id="944a0-117">Get the IQN</span></span>

<span data-ttu-id="944a0-118">Windows Server 2012 çalıştıran bir Windows konağının IQN'sini almak için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="944a0-118">Perform the following steps to get the IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a><span data-ttu-id="944a0-119">Bir ACR ekleme</span><span class="sxs-lookup"><span data-stu-id="944a0-119">Add an ACR</span></span>

<span data-ttu-id="944a0-120">Kullandığınız **erişim denetimi kayıtları** içinde dikey **yapılandırma** StorSimple Aygıt Yöneticisi'ni hizmetinizin ACRs eklemek için bölüm.</span><span class="sxs-lookup"><span data-stu-id="944a0-120">You use **Access control records** blade within the **Configuration** section of your StorSimple Device Manager service to add ACRs.</span></span> <span data-ttu-id="944a0-121">Genellikle, bir ACR tek bir birim ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="944a0-121">Typically, you associate one ACR with one volume.</span></span>

<span data-ttu-id="944a0-122">Bir birim bir ACR ilişkilendirme hakkında daha fazla bilgi için Git [birim Ekle](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="944a0-122">For information about associating an ACR with a volume, go to [add a volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="944a0-123">Bir ACR bir birime atarken, bu birim bozuk olabilir çünkü birim aynı anda birden fazla kümelenmemiş ana bilgisayar tarafından erişmediğinden dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="944a0-123">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span>


<span data-ttu-id="944a0-124">Bir ACR eklemek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="944a0-124">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-acr"></a><span data-ttu-id="944a0-125">Bir ACR eklemek için</span><span class="sxs-lookup"><span data-stu-id="944a0-125">To add an ACR</span></span>

1. <span data-ttu-id="944a0-126">Hizmet giriş sayfasında hizmetinizi seçin, hizmet adına çift tıklayın ve ardından içinde **yapılandırma** 'yi tıklatın **erişim denetimi kayıtları**.</span><span class="sxs-lookup"><span data-stu-id="944a0-126">On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="944a0-127">İçinde **erişim denetimi kayıtları** dikey penceresinde tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="944a0-127">In the **Access control records** blade, click **Add**.</span></span>
3. <span data-ttu-id="944a0-128">İçinde **eklemek ACR** dikey penceresinde aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="944a0-128">In the **Add ACR** blade, do the following:</span></span>
   
    1. <span data-ttu-id="944a0-129">ACR’nize bir **Ad** verin.</span><span class="sxs-lookup"><span data-stu-id="944a0-129">Supply a **Name** for your ACR.</span></span>
    
    2. <span data-ttu-id="944a0-130">Altında **iSCSI başlatıcısı adı**, Windows ana bilgisayarınız IQN adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="944a0-130">Under **iSCSI Initiator Name**, provide the IQN name of your Windows host.</span></span> <span data-ttu-id="944a0-131">Windows Server konağının IQN'sini almak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="944a0-131">To get the IQN of your Windows Server host, do the following:</span></span>
   
    3. <span data-ttu-id="944a0-132">Microsoft iSCSI başlatıcısını Windows konağında başlatın.</span><span class="sxs-lookup"><span data-stu-id="944a0-132">Start the Microsoft iSCSI initiator on your Windows host.</span></span> <span data-ttu-id="944a0-133">İSCSI Başlatıcı Özellikleri penceresinde üzerinde **yapılandırma** sekmesinde seçin ve dizeden kopyalama **Başlatıcı adı** alan.</span><span class="sxs-lookup"><span data-stu-id="944a0-133">In the iSCSI Initiator Properties window, on the **Configuration** tab, select and copy the string from the **Initiator Name** field.</span></span>
    <span data-ttu-id="944a0-134">Bu dizesini yapıştırabilir **IQN** alanındaki **eklemek ACR** dikey.</span><span class="sxs-lookup"><span data-stu-id="944a0-134">Paste this string in the **IQN** field in the **Add ACR** blade.</span></span>
   
    6. <span data-ttu-id="944a0-135">Tıklatın **Ekle** ACR eklemek için.</span><span class="sxs-lookup"><span data-stu-id="944a0-135">Click **Add** to add the ACR.</span></span>  
   
        ![Erişim denetimi kayıtları ekleyin](./media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. <span data-ttu-id="944a0-137">Sekmeli liste, bu toplama yansıtacak şekilde güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="944a0-137">The tabular listing is updated to reflect this addition.</span></span>

## <a name="edit-an-acr"></a><span data-ttu-id="944a0-138">Bir ACR Düzenle</span><span class="sxs-lookup"><span data-stu-id="944a0-138">Edit an ACR</span></span>

<span data-ttu-id="944a0-139">Kullandığınız **erişim denetimi kayıtları** içinde dikey **yapılandırma** Aygıt Yöneticisi'ni hizmetinizi ACRs düzenlemek için Azure portalında bölümü.</span><span class="sxs-lookup"><span data-stu-id="944a0-139">You use the **Access control records** blade within the **Configuration** section of your Device Manager service in the Azure portal to edit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="944a0-140">Şu anda kullanımda bir ACR değiştirmemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="944a0-140">You should not modify an ACR that is currently in use.</span></span> <span data-ttu-id="944a0-141">Şu anda kullanılmakta olan bir birimi ile ilişkili bir ACR düzenlemek için önce birim çevrimdışı duruma.</span><span class="sxs-lookup"><span data-stu-id="944a0-141">To edit an ACR associated with a volume that is currently in use, you should first take the volume offline.</span></span>


<span data-ttu-id="944a0-142">Bir ACR düzenlemek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="944a0-142">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-acr"></a><span data-ttu-id="944a0-143">Bir ACR düzenlemek için</span><span class="sxs-lookup"><span data-stu-id="944a0-143">To edit an ACR</span></span>

1. <span data-ttu-id="944a0-144">Hizmet giriş sayfasında hizmetinizi seçin, hizmet adına çift tıklayın ve ardından içinde **yapılandırma** bölümünde **erişim denetimi kayıtları**.</span><span class="sxs-lookup"><span data-stu-id="944a0-144">On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, **Access control records**.</span></span>
2. <span data-ttu-id="944a0-145">İçinde **erişim denetimi kayıtları** dikey penceresinde, erişim denetimi kayıtları Tablo listesini değiştirmek istediğiniz ACR çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="944a0-145">In the **Access control records** blade, from the tabular listing of the access control records, double-click the ACR that you wish to modify.</span></span>
3. <span data-ttu-id="944a0-146">İçinde **düzenleme erişim denetimi kayıtları** dikey penceresinde aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="944a0-146">In the **Edit access control records** blade, do the following:</span></span>
   
    1. <span data-ttu-id="944a0-147">IQN için ACR sağlayın.</span><span class="sxs-lookup"><span data-stu-id="944a0-147">Supply the IQN for the ACR.</span></span>
   
    2. <span data-ttu-id="944a0-148">Tıklatın **kaydetmek** değiştirilmiş ACR kaydetmek için dikey pencerenin üstündeki.</span><span class="sxs-lookup"><span data-stu-id="944a0-148">Click **Save** at the top of the blade to save the modified ACR.</span></span> <span data-ttu-id="944a0-149">Aşağıdaki onay iletisini görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="944a0-149">You see the following confirmation message:</span></span>
   
        ![Erişim denetimi kayıtları düzenleme](./media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a><span data-ttu-id="944a0-151">Bir erişim denetimi kaydını sil</span><span class="sxs-lookup"><span data-stu-id="944a0-151">Delete an access control record</span></span>

<span data-ttu-id="944a0-152">Kullandığınız **yapılandırma** ACRs silmek için Azure portalında sayfası.</span><span class="sxs-lookup"><span data-stu-id="944a0-152">You use the **Configuration** page in the Azure portal to delete ACRs.</span></span>

> [!NOTE]
> 
> * <span data-ttu-id="944a0-153">Şu anda kullanımda bir ACR silmemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="944a0-153">You should not delete an ACR that is currently in use.</span></span> <span data-ttu-id="944a0-154">Şu anda kullanılmakta olan bir birimi ile ilişkili bir ACR silmek için önce birim çevrimdışı duruma.</span><span class="sxs-lookup"><span data-stu-id="944a0-154">To delete an ACR associated with a volume that is currently in use, you should first take the volume offline.</span></span>
> * <span data-ttu-id="944a0-155">Bir ACR bir birimden silerken, silme, okuma-yazma kesilme neden olabilir çünkü karşılık gelen ana birim eriştiğini değil emin olun.</span><span class="sxs-lookup"><span data-stu-id="944a0-155">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>


<span data-ttu-id="944a0-156">Bir erişim denetimi kaydını silmek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="944a0-156">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="944a0-157">Bir erişim denetimi kaydını silmek için</span><span class="sxs-lookup"><span data-stu-id="944a0-157">To delete an access control record</span></span>

1. <span data-ttu-id="944a0-158">Hizmet giriş sayfasında hizmetinizi seçin, hizmet adına çift tıklayın ve ardından içinde **yapılandırma** bölümünde **erişim denetimi kayıtları**.</span><span class="sxs-lookup"><span data-stu-id="944a0-158">On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, **Access control records**.</span></span>

2. <span data-ttu-id="944a0-159">İçinde **erişim denetimi kayıtları** dikey penceresinde, erişim denetimi kayıtları Tablo listesini silmek istediğiniz ACR çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="944a0-159">In the **Access control records** blade, from the tabular listing of the access control records, double-click the ACR that you wish to delete.</span></span>

3. <span data-ttu-id="944a0-160">Düzen erişim denetimi kayıtları dikey tıklayın **silmek**.</span><span class="sxs-lookup"><span data-stu-id="944a0-160">In the Edit access control records blade, click **Delete**.</span></span>
   
    ![ACRS Sil](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. <span data-ttu-id="944a0-162">Onayınız istendiğinde tıklatın **silmek** silme işlemine devam etmek için.</span><span class="sxs-lookup"><span data-stu-id="944a0-162">When prompted for confirmation, click **Delete** to continue with the deletion.</span></span> <span data-ttu-id="944a0-163">Sekmeli liste silme yansıtacak şekilde güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="944a0-163">The tabular listing is updated to reflect the deletion.</span></span>
   
   ![Uyarı iletisi](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a><span data-ttu-id="944a0-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="944a0-165">Next steps</span></span>

* <span data-ttu-id="944a0-166">Daha fazla bilgi edinmek [birimleri ekleme ve ACRs yapılandırma](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="944a0-166">Learn more about [adding volumes and configuring ACRs](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

