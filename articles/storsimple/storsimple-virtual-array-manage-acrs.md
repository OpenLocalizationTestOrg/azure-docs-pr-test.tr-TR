---
title: "StorSimple sanal dizini aaaManage erişim denetimi kayıtları | Microsoft Docs"
description: "Hangi ana bilgisayarların hello StorSimple sanal dizinin tooa birimde bağlanabilir (ACRs) toodetermine toomanage erişim denetimi kayıtları nasıl açıklar."
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
ms.openlocfilehash: 608fdf72413761ce3c9c4bf297a748489c415685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-access-control-records-for-storsimple-virtual-array"></a><span data-ttu-id="0e7ea-103">StorSimple sanal dizisi için Aygıt Yöneticisi'ni StorSimple toomanage erişim denetimi kayıtları</span><span class="sxs-lookup"><span data-stu-id="0e7ea-103">Use StorSimple Device Manager toomanage access control records for StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="0e7ea-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="0e7ea-104">Overview</span></span>

<span data-ttu-id="0e7ea-105">Erişim denetimi kayıtları (ACRs) hangi ana bilgisayarların hello StorSimple sanal dizinin (olarak da bilinen hello StorSimple şirket içi sanal cihaz) tooa birimde bağlanabilir toospecify izin verin.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple Virtual Array (also known as hello StorSimple on-premises virtual device).</span></span> <span data-ttu-id="0e7ea-106">ACRs tooa belirli birimi ayarlayın ve hello iSCSI içeren hello konakların nitelikli adlar (IQN'ler).</span><span class="sxs-lookup"><span data-stu-id="0e7ea-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="0e7ea-107">Bir konak tooconnect tooa birim çalıştığında, hello aygıt hello hello IQN adının bu birimde ilişkili ACR denetler ve bir eşleşme varsa, ardından hello bağlantı kurulur.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name, and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="0e7ea-108">Merhaba **erişim denetimi kayıtları** dikey penceresinde hello içinde **yapılandırma** Aygıt Yöneticisi'ni hizmetinizi bölümünü hello ana IQN'ler karşılık gelen hello ile tüm hello erişim denetimi kayıtları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-108">hello **Access control records** blade within hello **Configuration** section of your Device Manager service displays all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

![Erişim denetimi kayıtlarını yönetme](./media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

<span data-ttu-id="0e7ea-110">Bu öğretici ortak ACR ilgili görevleri aşağıdaki hello açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="0e7ea-110">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="0e7ea-111">Merhaba IQN'sini Al</span><span class="sxs-lookup"><span data-stu-id="0e7ea-111">Get hello IQN</span></span>
* <span data-ttu-id="0e7ea-112">Bir erişim denetimi kaydı ekleme</span><span class="sxs-lookup"><span data-stu-id="0e7ea-112">Add an access control record</span></span>
* <span data-ttu-id="0e7ea-113">Bir erişim denetimi kaydı Düzenle</span><span class="sxs-lookup"><span data-stu-id="0e7ea-113">Edit an access control record</span></span>
* <span data-ttu-id="0e7ea-114">Bir erişim denetimi kaydını sil</span><span class="sxs-lookup"><span data-stu-id="0e7ea-114">Delete an access control record</span></span>

> [!IMPORTANT]
> 
> * <span data-ttu-id="0e7ea-115">ACR tooa birim atarken bu hello birim bozuk olabilir çünkü hello birim aynı anda birden fazla kümelenmemiş ana bilgisayar tarafından erişmediğinden dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-115">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>
> * <span data-ttu-id="0e7ea-116">Bir ACR bir birimden silerken okuma-yazma kesilme hello silinmesine neden çünkü hello karşılık gelen barındıran hello birime erişimde değil emin olun.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-116">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>


## <a name="get-hello-iqn"></a><span data-ttu-id="0e7ea-117">Merhaba IQN'sini Al</span><span class="sxs-lookup"><span data-stu-id="0e7ea-117">Get hello IQN</span></span>

<span data-ttu-id="0e7ea-118">Aşağıdaki adımları tooget hello Windows Server 2012 çalıştıran bir Windows konağının IQN'sini hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-118">Perform hello following steps tooget hello IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a><span data-ttu-id="0e7ea-119">Bir ACR ekleme</span><span class="sxs-lookup"><span data-stu-id="0e7ea-119">Add an ACR</span></span>

<span data-ttu-id="0e7ea-120">Kullandığınız **erişim denetimi kayıtları** dikey penceresinde hello içinde **yapılandırma** StorSimple cihaz Yöneticisi hizmeti tooadd ACRs bölümü.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-120">You use **Access control records** blade within hello **Configuration** section of your StorSimple Device Manager service tooadd ACRs.</span></span> <span data-ttu-id="0e7ea-121">Genellikle, bir ACR tek bir birim ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-121">Typically, you associate one ACR with one volume.</span></span>

<span data-ttu-id="0e7ea-122">Bir birim bir ACR ilişkilendirme hakkında daha fazla bilgi için çok Git[birim Ekle](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="0e7ea-122">For information about associating an ACR with a volume, go too[add a volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0e7ea-123">ACR tooa birim atarken bu hello birim bozuk olabilir çünkü hello birim aynı anda birden fazla kümelenmemiş ana bilgisayar tarafından erişmediğinden dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-123">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>


<span data-ttu-id="0e7ea-124">Aşağıdaki adımları tooadd bir ACR hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-124">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-acr"></a><span data-ttu-id="0e7ea-125">tooadd bir ACR</span><span class="sxs-lookup"><span data-stu-id="0e7ea-125">tooadd an ACR</span></span>

1. <span data-ttu-id="0e7ea-126">Merhaba hizmet giriş sayfasında hizmetinizi seçin, hello hizmet adını ve ardından içinde hello çift **yapılandırma** 'yi tıklatın **erişim denetimi kayıtları**.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-126">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="0e7ea-127">Merhaba, **erişim denetimi kayıtları** dikey penceresinde tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-127">In hello **Access control records** blade, click **Add**.</span></span>
3. <span data-ttu-id="0e7ea-128">Merhaba, **eklemek ACR** dikey penceresinde, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="0e7ea-128">In hello **Add ACR** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="0e7ea-129">ACR’nize bir **Ad** verin.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-129">Supply a **Name** for your ACR.</span></span>
    
    2. <span data-ttu-id="0e7ea-130">Altında **iSCSI başlatıcısı adı**, Windows ana bilgisayarınız hello IQN adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-130">Under **iSCSI Initiator Name**, provide hello IQN name of your Windows host.</span></span> <span data-ttu-id="0e7ea-131">tooget Merhaba, Windows Server konağının IQN'ini hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="0e7ea-131">tooget hello IQN of your Windows Server host, do hello following:</span></span>
   
    3. <span data-ttu-id="0e7ea-132">Merhaba Microsoft iSCSI başlatıcısını Windows konağında başlatın.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-132">Start hello Microsoft iSCSI initiator on your Windows host.</span></span> <span data-ttu-id="0e7ea-133">Merhaba iSCSI başlatıcısı Özellikleri penceresinde hello **yapılandırma** sekmesinde seçin ve hello hello dize kopyalama **Başlatıcı adı** alan.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-133">In hello iSCSI Initiator Properties window, on hello **Configuration** tab, select and copy hello string from hello **Initiator Name** field.</span></span>
    <span data-ttu-id="0e7ea-134">Bu dize hello Yapıştır **IQN** hello alanındaki **eklemek ACR** dikey.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-134">Paste this string in hello **IQN** field in hello **Add ACR** blade.</span></span>
   
    6. <span data-ttu-id="0e7ea-135">Tıklatın **Ekle** tooadd hello ACR.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-135">Click **Add** tooadd hello ACR.</span></span>  
   
        ![Erişim denetimi kayıtları ekleyin](./media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. <span data-ttu-id="0e7ea-137">Sekmeli liste hello güncelleştirilmiş tooreflect bu ektir.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-137">hello tabular listing is updated tooreflect this addition.</span></span>

## <a name="edit-an-acr"></a><span data-ttu-id="0e7ea-138">Bir ACR Düzenle</span><span class="sxs-lookup"><span data-stu-id="0e7ea-138">Edit an ACR</span></span>

<span data-ttu-id="0e7ea-139">Merhaba kullandığınız **erişim denetimi kayıtları** dikey penceresinde hello içinde **yapılandırma** Aygıt Yöneticisi'ni hizmetinizi hello Azure portal tooedit ACRs bölümü.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-139">You use hello **Access control records** blade within hello **Configuration** section of your Device Manager service in hello Azure portal tooedit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="0e7ea-140">Şu anda kullanımda bir ACR değiştirmemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-140">You should not modify an ACR that is currently in use.</span></span> <span data-ttu-id="0e7ea-141">şu anda kullanımda olan bir birime bir ACR ilişkili tooedit, ilk hello birim çevrimdışı duruma.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-141">tooedit an ACR associated with a volume that is currently in use, you should first take hello volume offline.</span></span>


<span data-ttu-id="0e7ea-142">Aşağıdaki adımları tooedit bir ACR hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-142">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-acr"></a><span data-ttu-id="0e7ea-143">tooedit bir ACR</span><span class="sxs-lookup"><span data-stu-id="0e7ea-143">tooedit an ACR</span></span>

1. <span data-ttu-id="0e7ea-144">Merhaba hizmet giriş sayfasında hizmetinizi seçin, hello hizmet adını ve ardından içinde hello çift **yapılandırma** bölümünde **erişim denetimi kayıtları**.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-144">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, **Access control records**.</span></span>
2. <span data-ttu-id="0e7ea-145">Merhaba, **erişim denetimi kayıtları** dikey penceresinde, hello erişim denetimi kayıtları, Tablo listesini hello hello toomodify istediğiniz ACR çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-145">In hello **Access control records** blade, from hello tabular listing of hello access control records, double-click hello ACR that you wish toomodify.</span></span>
3. <span data-ttu-id="0e7ea-146">Merhaba, **düzenleme erişim denetimi kayıtları** dikey penceresinde, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="0e7ea-146">In hello **Edit access control records** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="0e7ea-147">Merhaba IQN hello ACR sağlayın.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-147">Supply hello IQN for hello ACR.</span></span>
   
    2. <span data-ttu-id="0e7ea-148">Tıklatın **kaydetmek** hello dikey toosave hello üstünde hello ACR değiştirdi.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-148">Click **Save** at hello top of hello blade toosave hello modified ACR.</span></span> <span data-ttu-id="0e7ea-149">Onay iletisi aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="0e7ea-149">You see hello following confirmation message:</span></span>
   
        ![Erişim denetimi kayıtları düzenleme](./media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a><span data-ttu-id="0e7ea-151">Bir erişim denetimi kaydını sil</span><span class="sxs-lookup"><span data-stu-id="0e7ea-151">Delete an access control record</span></span>

<span data-ttu-id="0e7ea-152">Merhaba kullandığınız **yapılandırma** hello Azure portal toodelete ACRs sayfasında.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-152">You use hello **Configuration** page in hello Azure portal toodelete ACRs.</span></span>

> [!NOTE]
> 
> * <span data-ttu-id="0e7ea-153">Şu anda kullanımda bir ACR silmemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-153">You should not delete an ACR that is currently in use.</span></span> <span data-ttu-id="0e7ea-154">şu anda kullanımda olan bir birime bir ACR ilişkili toodelete, ilk hello birim çevrimdışı duruma.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-154">toodelete an ACR associated with a volume that is currently in use, you should first take hello volume offline.</span></span>
> * <span data-ttu-id="0e7ea-155">Bir ACR bir birimden silerken okuma-yazma kesilme hello silinmesine neden çünkü hello karşılık gelen barındıran hello birime erişimde değil emin olun.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-155">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>


<span data-ttu-id="0e7ea-156">Aşağıdaki adımları toodelete bir erişim denetimi kaydı hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-156">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="0e7ea-157">toodelete bir erişim denetimi kaydı</span><span class="sxs-lookup"><span data-stu-id="0e7ea-157">toodelete an access control record</span></span>

1. <span data-ttu-id="0e7ea-158">Merhaba hizmet giriş sayfasında hizmetinizi seçin, hello hizmet adını ve ardından içinde hello çift **yapılandırma** bölümünde **erişim denetimi kayıtları**.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-158">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, **Access control records**.</span></span>

2. <span data-ttu-id="0e7ea-159">Merhaba, **erişim denetimi kayıtları** dikey penceresinde, hello erişim denetimi kayıtları, Tablo listesini hello hello toodelete istediğiniz ACR çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-159">In hello **Access control records** blade, from hello tabular listing of hello access control records, double-click hello ACR that you wish toodelete.</span></span>

3. <span data-ttu-id="0e7ea-160">Merhaba düzenleme erişim denetimi kayıtları dikey penceresinde tıklayın **silmek**.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-160">In hello Edit access control records blade, click **Delete**.</span></span>
   
    ![ACRS Sil](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. <span data-ttu-id="0e7ea-162">Onayınız istendiğinde tıklatın **silmek** toocontinue hello silme işlemi ile.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-162">When prompted for confirmation, click **Delete** toocontinue with hello deletion.</span></span> <span data-ttu-id="0e7ea-163">Merhaba tablo güncelleştirilmiş tooreflect hello silme listedir.</span><span class="sxs-lookup"><span data-stu-id="0e7ea-163">hello tabular listing is updated tooreflect hello deletion.</span></span>
   
   ![Uyarı iletisi](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a><span data-ttu-id="0e7ea-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0e7ea-165">Next steps</span></span>

* <span data-ttu-id="0e7ea-166">Daha fazla bilgi edinmek [birimleri ekleme ve ACRs yapılandırma](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="0e7ea-166">Learn more about [adding volumes and configuring ACRs](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

