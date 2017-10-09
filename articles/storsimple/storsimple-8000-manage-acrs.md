---
title: "StorSimple aaaManage erişim denetimi kayıtları | Microsoft Docs"
description: "Hangi ana bilgisayarların hello StorSimple cihazı tooa birimde bağlanabilir (ACRs) toodetermine toouse erişim denetimi kayıtları nasıl açıklar."
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
ms.openlocfilehash: cf532206e2c0bc49da853663ba34ae993ec2981d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a><span data-ttu-id="8ed80-103">Merhaba StorSimple Yöneticisi hizmet toomanage erişim denetimi kayıtları kullanın</span><span class="sxs-lookup"><span data-stu-id="8ed80-103">Use hello StorSimple Manager service toomanage access control records</span></span>

## <a name="overview"></a><span data-ttu-id="8ed80-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="8ed80-104">Overview</span></span>
<span data-ttu-id="8ed80-105">Erişim denetimi kayıtları (ACRs) hangi ana bilgisayarların hello StorSimple cihazı tooa birimde bağlanabilir toospecify izin verin.</span><span class="sxs-lookup"><span data-stu-id="8ed80-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple device.</span></span> <span data-ttu-id="8ed80-106">ACRs tooa belirli birimi ayarlayın ve hello iSCSI içeren hello konakların nitelikli adlar (IQN'ler).</span><span class="sxs-lookup"><span data-stu-id="8ed80-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="8ed80-107">Bir konak tooconnect tooa birim çalıştığında hello aygıt hello IQN adı ve bir eşleşmesi durumunda hello bağlantı kurulur bu birimde ACR ilişkili hello denetler.</span><span class="sxs-lookup"><span data-stu-id="8ed80-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="8ed80-108">Merhaba hello erişim denetimi kayıtları **yapılandırma** StorSimple cihaz Yöneticisi hizmeti dikey pencerenize bölümünü hello ana IQN'ler karşılık gelen hello ile tüm hello erişim denetimi kayıtları görüntülemek.</span><span class="sxs-lookup"><span data-stu-id="8ed80-108">hello access control records in hello **Configuration** section of your StorSimple Device Manager service blade display all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

<span data-ttu-id="8ed80-109">Bu öğretici ortak ACR ilgili görevleri aşağıdaki hello açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="8ed80-109">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="8ed80-110">Bir erişim denetimi kaydı ekleme</span><span class="sxs-lookup"><span data-stu-id="8ed80-110">Add an access control record</span></span>
* <span data-ttu-id="8ed80-111">Bir erişim denetimi kaydı Düzenle</span><span class="sxs-lookup"><span data-stu-id="8ed80-111">Edit an access control record</span></span>
* <span data-ttu-id="8ed80-112">Bir erişim denetimi kaydını sil</span><span class="sxs-lookup"><span data-stu-id="8ed80-112">Delete an access control record</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="8ed80-113">ACR tooa birim atarken bu hello birim bozuk olabilir çünkü hello birim aynı anda birden fazla kümelenmemiş ana bilgisayar tarafından erişmediğinden dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="8ed80-113">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>
> * <span data-ttu-id="8ed80-114">Bir ACR bir birimden silerken okuma-yazma kesilme hello silinmesine neden çünkü hello karşılık gelen barındıran hello birime erişimde değil emin olun.</span><span class="sxs-lookup"><span data-stu-id="8ed80-114">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>

## <a name="get-hello-iqn"></a><span data-ttu-id="8ed80-115">Merhaba IQN'sini Al</span><span class="sxs-lookup"><span data-stu-id="8ed80-115">Get hello IQN</span></span>

<span data-ttu-id="8ed80-116">Aşağıdaki adımları tooget hello Windows Server 2012 çalıştıran bir Windows konağının IQN'sini hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="8ed80-116">Perform hello following steps tooget hello IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a><span data-ttu-id="8ed80-117">Bir erişim denetimi kaydı ekleme</span><span class="sxs-lookup"><span data-stu-id="8ed80-117">Add an access control record</span></span>
<span data-ttu-id="8ed80-118">Merhaba kullandığınız **yapılandırma** hello StorSimple cihaz Yöneticisi hizmeti dikey tooadd ACRs bölümünde.</span><span class="sxs-lookup"><span data-stu-id="8ed80-118">You use hello **Configuration** section in hello StorSimple Device Manager service blade tooadd ACRs.</span></span> <span data-ttu-id="8ed80-119">Genellikle, bir birimle bir ACR ilişkilendireceğiniz.</span><span class="sxs-lookup"><span data-stu-id="8ed80-119">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="8ed80-120">Aşağıdaki adımları tooadd bir ACR hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="8ed80-120">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-acr"></a><span data-ttu-id="8ed80-121">tooadd bir ACR</span><span class="sxs-lookup"><span data-stu-id="8ed80-121">tooadd an ACR</span></span>

1. <span data-ttu-id="8ed80-122">Tooyour StorSimple cihaz Yöneticisi hizmeti gidin, hello hizmet adını ve ardından içinde hello çift **yapılandırma** 'yi tıklatın **erişim denetimi kayıtları**.</span><span class="sxs-lookup"><span data-stu-id="8ed80-122">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="8ed80-123">Merhaba, **erişim denetimi kayıtları** dikey penceresinde tıklatın **+ ACR eklemek**.</span><span class="sxs-lookup"><span data-stu-id="8ed80-123">In hello **Access control records** blade, click **+ Add ACR**.</span></span>

    ![ACR Ekle'yi tıklatın](./media/storsimple-8000-manage-acrs/createacr1.png)

3. <span data-ttu-id="8ed80-125">Merhaba, **eklemek ACR** dikey penceresinde, adımları hello:</span><span class="sxs-lookup"><span data-stu-id="8ed80-125">In hello **Add ACR** blade, do hello following steps:</span></span>

    1. <span data-ttu-id="8ed80-126">Bir ad verin sağlayın.</span><span class="sxs-lookup"><span data-stu-id="8ed80-126">Supply a name for your ACR.</span></span>
    
    2. <span data-ttu-id="8ed80-127">Windows Server konağınızda altında Hello IQN adını sağlayın **iSCSI başlatıcısı adı (IQN)**.</span><span class="sxs-lookup"><span data-stu-id="8ed80-127">Provide hello IQN name of your Windows Server host under **iSCSI Initiator Name (IQN)**.</span></span>

    3. <span data-ttu-id="8ed80-128">Tıklatın **Ekle** toocreate hello ACR.</span><span class="sxs-lookup"><span data-stu-id="8ed80-128">Click **Add** toocreate hello ACR.</span></span>

        ![ACR Ekle'yi tıklatın](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  <span data-ttu-id="8ed80-130">Merhaba, yeni ACR hello tablo ACRs listesinde görüntülenir eklendi.</span><span class="sxs-lookup"><span data-stu-id="8ed80-130">hello newly added ACR will display in hello tabular listing of ACRs.</span></span>

    ![ACR Ekle'yi tıklatın](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a><span data-ttu-id="8ed80-132">Bir erişim denetimi kaydı Düzenle</span><span class="sxs-lookup"><span data-stu-id="8ed80-132">Edit an access control record</span></span>
<span data-ttu-id="8ed80-133">Merhaba kullandığınız **yapılandırma** hello StorSimple cihaz Yöneticisi hizmeti dikey tooedit ACRs bölümünde.</span><span class="sxs-lookup"><span data-stu-id="8ed80-133">You use hello **Configuration** section in hello StorSimple Device Manager service blade tooedit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="8ed80-134">Şu anda kullanımda olmayan ACRs değiştirmeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="8ed80-134">It is recommended that you modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="8ed80-135">şu anda kullanımda olan bir birime bir ACR ilişkili tooedit, ilk hello birim çevrimdışı duruma getirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ed80-135">tooedit an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>

<span data-ttu-id="8ed80-136">Aşağıdaki adımları tooedit bir ACR hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="8ed80-136">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-access-control-record"></a><span data-ttu-id="8ed80-137">tooedit bir erişim denetimi kaydı</span><span class="sxs-lookup"><span data-stu-id="8ed80-137">tooedit an access control record</span></span>
1.  <span data-ttu-id="8ed80-138">Tooyour StorSimple cihaz Yöneticisi hizmeti gidin, hello hizmet adını ve ardından içinde hello çift **yapılandırma** 'yi tıklatın **erişim denetimi kayıtları**.</span><span class="sxs-lookup"><span data-stu-id="8ed80-138">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>

    ![Tooaccess denetim kayıtları gidin](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="8ed80-140">Hello tablo hello erişim denetimi kayıtları listesi,'ı tıklatın ve hello toomodify istediğiniz ACR seçin.</span><span class="sxs-lookup"><span data-stu-id="8ed80-140">In hello tabular listing of hello access control records, click and select hello ACR that you wish toomodify.</span></span>

    ![Erişim denetimi kayıtları düzenleme](./media/storsimple-8000-manage-acrs/editacr1.png)

3. <span data-ttu-id="8ed80-142">Merhaba, **düzenleme erişim denetimi kaydı** dikey penceresinde, farklı bir IQN karşılık gelen tooanother konak sağlayın.</span><span class="sxs-lookup"><span data-stu-id="8ed80-142">In hello **Edit access control record** blade, provide a different IQN corresponding tooanother host.</span></span>

    ![Erişim denetimi kayıtları düzenleme](./media/storsimple-8000-manage-acrs/editacr2.png)

4. <span data-ttu-id="8ed80-144">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8ed80-144">Click **Save**.</span></span> <span data-ttu-id="8ed80-145">Onayınız istendiğinde **Evet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8ed80-145">When prompted for confirmation, click **Yes**.</span></span> 

    ![Erişim denetimi kayıtları düzenleme](./media/storsimple-8000-manage-acrs/editacr3.png)

5. <span data-ttu-id="8ed80-147">Merhaba ACR güncelleştirildiğinde size bildirilir.</span><span class="sxs-lookup"><span data-stu-id="8ed80-147">You are notified when hello ACR is updated.</span></span> <span data-ttu-id="8ed80-148">Merhaba sekmeli liste tooreflect hello değişiklik de güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="8ed80-148">hello tabular listing also updates tooreflect hello change.</span></span>

   
## <a name="delete-an-access-control-record"></a><span data-ttu-id="8ed80-149">Bir erişim denetimi kaydını sil</span><span class="sxs-lookup"><span data-stu-id="8ed80-149">Delete an access control record</span></span>
<span data-ttu-id="8ed80-150">Merhaba kullandığınız **yapılandırma** hello StorSimple cihaz Yöneticisi hizmeti dikey toodelete ACRs bölümünde.</span><span class="sxs-lookup"><span data-stu-id="8ed80-150">You use hello **Configuration** section in hello StorSimple Device Manager service blade toodelete ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="8ed80-151">Şu anda kullanımda olmayan ACRs silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ed80-151">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="8ed80-152">şu anda kullanımda olan bir birime bir ACR ilişkili toodelete, ilk hello birim çevrimdışı duruma getirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ed80-152">toodelete an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>

<span data-ttu-id="8ed80-153">Aşağıdaki adımları toodelete bir erişim denetimi kaydı hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="8ed80-153">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="8ed80-154">toodelete bir erişim denetimi kaydı</span><span class="sxs-lookup"><span data-stu-id="8ed80-154">toodelete an access control record</span></span>
1.  <span data-ttu-id="8ed80-155">Tooyour StorSimple cihaz Yöneticisi hizmeti gidin, hello hizmet adını ve ardından içinde hello çift **yapılandırma** 'yi tıklatın **erişim denetimi kayıtları**.</span><span class="sxs-lookup"><span data-stu-id="8ed80-155">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>

    ![Tooaccess denetim kayıtları gidin](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="8ed80-157">Hello tablo hello erişim denetimi kayıtları listesi,'ı tıklatın ve hello toodelete istediğiniz ACR seçin.</span><span class="sxs-lookup"><span data-stu-id="8ed80-157">In hello tabular listing of hello access control records, click and select hello ACR that you wish toodelete.</span></span>

    ![Tooaccess denetim kayıtları gidin](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. <span data-ttu-id="8ed80-159">Tooinvoke hello bağlam menüsü sağ tıklatıp **silmek**.</span><span class="sxs-lookup"><span data-stu-id="8ed80-159">Right-click tooinvoke hello context menu and select **Delete**.</span></span>

    ![Tooaccess denetim kayıtları gidin](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. <span data-ttu-id="8ed80-161">Onayınız istendiğinde hello bilgileri gözden geçirin ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="8ed80-161">When prompted for confirmation, review hello information and then click **Delete**.</span></span>

    ![Tooaccess denetim kayıtları gidin](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. <span data-ttu-id="8ed80-163">Merhaba silme işlemi tamamlandığında size bildirilir.</span><span class="sxs-lookup"><span data-stu-id="8ed80-163">You are notified when hello deletion completes.</span></span> <span data-ttu-id="8ed80-164">Merhaba tablo güncelleştirilmiş tooreflect hello silme listedir.</span><span class="sxs-lookup"><span data-stu-id="8ed80-164">hello tabular listing is updated tooreflect hello deletion.</span></span>

    ![Tooaccess denetim kayıtları gidin](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a><span data-ttu-id="8ed80-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8ed80-166">Next steps</span></span>
* <span data-ttu-id="8ed80-167">Daha fazla bilgi edinmek [StorSimple birimlerini yönetme](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="8ed80-167">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span>
* <span data-ttu-id="8ed80-168">Daha fazla bilgi edinmek [kullanarak, StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="8ed80-168">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

