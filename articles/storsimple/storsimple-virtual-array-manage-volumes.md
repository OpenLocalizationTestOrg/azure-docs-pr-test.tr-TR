---
title: StorSimple sanal dizinin aaaManage birimlerde | Microsoft Docs
description: "Merhaba StorSimple Aygıt Yöneticisi'ni tanımlar ve açıklar nasıl toouse, StorSimple sanal dizinizi toomanage birimlerde."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: caa6a26b-b7ba-4a05-b092-1a79450225cf
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 46aa6d7508b3e62f75a3b78ed73302b88320a0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-service-toomanage-volumes-on-hello-storsimple-virtual-array"></a><span data-ttu-id="acdb5-103">Aygıt Yöneticisi'ni StorSimple hizmet toomanage hello StorSimple sanal dizinin birimlerde</span><span class="sxs-lookup"><span data-stu-id="acdb5-103">Use StorSimple Device Manager service toomanage volumes on hello StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="acdb5-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="acdb5-104">Overview</span></span>

<span data-ttu-id="acdb5-105">Bu öğretici nasıl toouse StorSimple cihaz Yöneticisi hizmeti toocreate hello ve StorSimple sanal dizinizi birimlerde yönetmek açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="acdb5-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage volumes on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="acdb5-106">Merhaba StorSimple cihaz Yöneticisi hizmeti hello StorSimple çözümünüzün bir tek web arabiriminden yönetmenizi sağlayan Azure portalı bir uzantıdır.</span><span class="sxs-lookup"><span data-stu-id="acdb5-106">hello StorSimple Device Manager service is an extension in hello Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="acdb5-107">Toplama toomanaging paylaşımları ve birimler, hello StorSimple cihaz Yöneticisi hizmeti tooview kullanın ve cihazları yönetmek, uyarıları görüntülemek ve görüntüleyebilir ve yedekleme ilkeleri ve hello yedekleme kataloğu yönetin.</span><span class="sxs-lookup"><span data-stu-id="acdb5-107">In addition toomanaging shares and volumes, you can use hello StorSimple Device Manager service tooview and manage devices, view alerts, and view and manage backup policies and hello backup catalog.</span></span>

## <a name="volume-types"></a><span data-ttu-id="acdb5-108">Birim türleri</span><span class="sxs-lookup"><span data-stu-id="acdb5-108">Volume Types</span></span>

<span data-ttu-id="acdb5-109">StorSimple birimlerini olabilir:</span><span class="sxs-lookup"><span data-stu-id="acdb5-109">StorSimple volumes can be:</span></span>

* <span data-ttu-id="acdb5-110">**Yerel olarak sabitlenmiş**: Bu birimlerdeki veriler her zaman hello dizisinde kalır ve toohello buluta dağıtılmamasını.</span><span class="sxs-lookup"><span data-stu-id="acdb5-110">**Locally pinned**: Data in these volumes stays on hello array at all times and does not spill toohello cloud.</span></span>
* <span data-ttu-id="acdb5-111">**Katmanlı**: Bu birimlerdeki veriler toohello bulut sığdırmaya.</span><span class="sxs-lookup"><span data-stu-id="acdb5-111">**Tiered**: Data in these volumes can spill toohello cloud.</span></span> <span data-ttu-id="acdb5-112">Katmanlı birim oluşturduğunuzda, hello alanın % 10'yaklaşık hello yerel katmanında sağlanır ve % 90'hello alanı hello bulutta sağlanır.</span><span class="sxs-lookup"><span data-stu-id="acdb5-112">When you create a tiered volume, approximately 10 % of hello space is provisioned on hello local tier and 90 % of hello space is provisioned in hello cloud.</span></span> <span data-ttu-id="acdb5-113">Örneğin, 1 TB birim sağlanan, 100 GB hello yerel alan bulunması ve 900 GB hello bulutta kullanılacak ne zaman veri katmanlarını hello.</span><span class="sxs-lookup"><span data-stu-id="acdb5-113">For example, if you provisioned a 1 TB volume, 100 GB would reside in hello local space and 900 GB would be used in hello cloud when hello data tiers.</span></span> <span data-ttu-id="acdb5-114">Bu, sırayla hello cihazda tüm hello yerel alana çalıştırırsanız (Merhaba % 10 hello yerel katmanı kullanılamaz gerektirdiğinden), katmanlı birim sağlayamazsınız olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="acdb5-114">This in turn implies that if you run out of all hello local space on hello device, you cannot provision a tiered volume (because hello 10 % required on hello local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="acdb5-115">Sağlanan kapasite</span><span class="sxs-lookup"><span data-stu-id="acdb5-115">Provisioned capacity</span></span>
<span data-ttu-id="acdb5-116">Aşağıdaki tabloda her bir birim türü için en fazla sağlanan kapasite toohello bakın.</span><span class="sxs-lookup"><span data-stu-id="acdb5-116">Refer toohello following table for maximum provisioned capacity for each volume type.</span></span>

| <span data-ttu-id="acdb5-117">**Sınır tanımlayıcısı**</span><span class="sxs-lookup"><span data-stu-id="acdb5-117">**Limit identifier**</span></span>                                       | <span data-ttu-id="acdb5-118">**Sınırı**</span><span class="sxs-lookup"><span data-stu-id="acdb5-118">**Limit**</span></span>     |
|------------------------------------------------------------|---------------|
| <span data-ttu-id="acdb5-119">Katmanlı birim en küçük boyut</span><span class="sxs-lookup"><span data-stu-id="acdb5-119">Minimum size of a tiered volume</span></span>                            | <span data-ttu-id="acdb5-120">500 GB</span><span class="sxs-lookup"><span data-stu-id="acdb5-120">500 GB</span></span>        |
| <span data-ttu-id="acdb5-121">Katmanlı birim en büyük boyutu</span><span class="sxs-lookup"><span data-stu-id="acdb5-121">Maximum size of a tiered volume</span></span>                            | <span data-ttu-id="acdb5-122">5 TB</span><span class="sxs-lookup"><span data-stu-id="acdb5-122">5 TB</span></span>          |
| <span data-ttu-id="acdb5-123">Yerel olarak sabitlenmiş bir birim en küçük boyut</span><span class="sxs-lookup"><span data-stu-id="acdb5-123">Minimum size of a locally pinned volume</span></span>                    | <span data-ttu-id="acdb5-124">50 GB</span><span class="sxs-lookup"><span data-stu-id="acdb5-124">50 GB</span></span>         |
| <span data-ttu-id="acdb5-125">Yerel olarak sabitlenmiş bir birim en büyük boyutu</span><span class="sxs-lookup"><span data-stu-id="acdb5-125">Maximum size of a locally pinned volume</span></span>                    | <span data-ttu-id="acdb5-126">500 GB</span><span class="sxs-lookup"><span data-stu-id="acdb5-126">500 GB</span></span>        |

## <a name="hello-volumes-blade"></a><span data-ttu-id="acdb5-127">Merhaba birimleri dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="acdb5-127">hello Volumes blade</span></span>
<span data-ttu-id="acdb5-128">Merhaba **birimleri** StorSimple hizmeti Özet dikey menüsünde belirli bir StorSimple dizi depolama birimleri hello listesini görüntüler ve toomanage sağlayan bunları.</span><span class="sxs-lookup"><span data-stu-id="acdb5-128">hello **Volumes** menu on your StorSimple service summary blade displays hello list of storage volumes on a given StorSimple array and allows you toomanage them.</span></span>

![Birimleri dikey penceresi](./media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

<span data-ttu-id="acdb5-130">Bir birim öznitelikleri bir dizi oluşur:</span><span class="sxs-lookup"><span data-stu-id="acdb5-130">A volume consists of a series of attributes:</span></span>

* <span data-ttu-id="acdb5-131">**Birim adı** – benzersiz olmalı ve hello birim tanımlamanıza yardımcı olan açıklayıcı bir ad.</span><span class="sxs-lookup"><span data-stu-id="acdb5-131">**Volume Name** – A descriptive name that must be unique and helps identify hello volume.</span></span>
* <span data-ttu-id="acdb5-132">**Durum** – çevrimiçi veya çevrimdışı olabilir.</span><span class="sxs-lookup"><span data-stu-id="acdb5-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="acdb5-133">Bir birim çevrimdışıysa, erişim toouse hello birim izin görünür tooinitiators (sunucu) değil.</span><span class="sxs-lookup"><span data-stu-id="acdb5-133">If a volume is offline, it is not visible tooinitiators (servers) that are allowed access toouse hello volume.</span></span>
* <span data-ttu-id="acdb5-134">**Tür** – hello birim olup olmadığını belirten **katmanlı** (Merhaba varsayılan) veya **yerel olarak sabitlenmiş**.</span><span class="sxs-lookup"><span data-stu-id="acdb5-134">**Type** – Indicates whether hello volume is **Tiered** (hello default) or **Locally pinned**.</span></span>
* <span data-ttu-id="acdb5-135">**Kapasite** – hello karşılaştırılan toohello toplam hello Başlatıcı (sunucu) tarafından depolanan veri miktarını olarak kullanılan veri miktarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="acdb5-135">**Capacity** – specifies hello amount of data used as compared toohello total amount of data that can be stored by hello initiator (server).</span></span>
* <span data-ttu-id="acdb5-136">**Yedekleme** – durumda hello StorSimple sanal dizinin tüm birimleri otomatik olarak yedekleme için etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="acdb5-136">**Backup** – In case of hello StorSimple Virtual Array, all volumes are automatically enabled for backup.</span></span>
* <span data-ttu-id="acdb5-137">**Bağlı Konaklar** – erişim toothis birim izin hello başlatıcıları (Sunucuları) belirtir.</span><span class="sxs-lookup"><span data-stu-id="acdb5-137">**Connected hosts** – Specifies hello initiators (servers) that are allowed access toothis volume.</span></span>

![Birimleri ayrıntıları](./media/storsimple-virtual-array-manage-volumes/volume-details.png)

<span data-ttu-id="acdb5-139">Bu öğretici tooperform hello görevleri aşağıdaki Hello yönergeleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="acdb5-139">Use hello instructions in this tutorial tooperform hello following tasks:</span></span>

* <span data-ttu-id="acdb5-140">Birim Ekle</span><span class="sxs-lookup"><span data-stu-id="acdb5-140">Add a volume</span></span>
* <span data-ttu-id="acdb5-141">Bir birim değiştirme</span><span class="sxs-lookup"><span data-stu-id="acdb5-141">Modify a volume</span></span>
* <span data-ttu-id="acdb5-142">Bir birim çevrimdışı duruma getirin</span><span class="sxs-lookup"><span data-stu-id="acdb5-142">Take a volume offline</span></span>
* <span data-ttu-id="acdb5-143">Bir birim Sil</span><span class="sxs-lookup"><span data-stu-id="acdb5-143">Delete a volume</span></span>

## <a name="add-a-volume"></a><span data-ttu-id="acdb5-144">Birim Ekle</span><span class="sxs-lookup"><span data-stu-id="acdb5-144">Add a volume</span></span>

1. <span data-ttu-id="acdb5-145">Merhaba StorSimple hizmeti Özet dikey penceresinden, tıklayın **+ Add birim** hello komut çubuğundan.</span><span class="sxs-lookup"><span data-stu-id="acdb5-145">From hello StorSimple service summary blade, click **+ Add volume** from hello command bar.</span></span> <span data-ttu-id="acdb5-146">Merhaba açılır **birim ekleme** dikey.</span><span class="sxs-lookup"><span data-stu-id="acdb5-146">This opens up hello **Add volume** blade.</span></span>
   
    ![Birim ekle](./media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. <span data-ttu-id="acdb5-148">Merhaba, **birim ekleme** dikey penceresinde, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="acdb5-148">In hello **Add volume** blade, do hello following:</span></span>
   
   * <span data-ttu-id="acdb5-149">Merhaba, **birim adı** alanında, biriminiz için benzersiz bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="acdb5-149">In hello **Volume name** field, enter a unique name for your volume.</span></span> <span data-ttu-id="acdb5-150">Merhaba adı 3 too127 karakter içeren bir dize olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="acdb5-150">hello name must be a string that contains 3 too127 characters.</span></span>
   * <span data-ttu-id="acdb5-151">Merhaba, **türü** açılır listesinde, belirleyin olup olmadığını toocreate bir **katmanlı** veya **yerel olarak sabitlenmiş** birim.</span><span class="sxs-lookup"><span data-stu-id="acdb5-151">In hello **Type** dropdown list, specify whether toocreate a **Tiered** or **Locally pinned** volume.</span></span> <span data-ttu-id="acdb5-152">Yerel GARANTİLERİN, düşük gecikme ve yüksek performansın gerektiği iş yükleri için seçin **birim'yerel olarak sabitlenmiş**.</span><span class="sxs-lookup"><span data-stu-id="acdb5-152">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned volume**.</span></span> <span data-ttu-id="acdb5-153">Diğer tüm veriler için seçin **katmanlı** birim.</span><span class="sxs-lookup"><span data-stu-id="acdb5-153">For all other data, select **Tiered** volume.</span></span>
   * <span data-ttu-id="acdb5-154">Merhaba, **kapasite** alanında, hello hello birimin boyutunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="acdb5-154">In hello **Capacity** field, specify hello size of hello volume.</span></span> <span data-ttu-id="acdb5-155">Katmanlı birim 500 GB ile 5 TB arasında olmalıdır ve yerel olarak sabitlenmiş bir birim 50 GB ve 500 GB arasında olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="acdb5-155">A tiered volume must be between 500 GB and 5 TB and a locally pinned volume must be between 50 GB and 500 GB.</span></span>
   * * <span data-ttu-id="acdb5-156">Tıklatın **bağlı Konaklar**, tooconnect toothis birim istediğiniz ve ardından bir erişim denetimi kaydı (ACR) karşılık gelen toohello iSCSI başlatıcısı seçin **seçin**.</span><span class="sxs-lookup"><span data-stu-id="acdb5-156">Click **Connected hosts**, select an access control record (ACR) corresponding toohello iSCSI initiator that you want tooconnect toothis volume, and then click **Select**.</span></span>
3. <span data-ttu-id="acdb5-157">Yeni bir bağlı konak tooadd tıklatın **yeni Ekle**, hello ana bilgisayarı ve onun iSCSI için bir ad girin tam adını (IQN) ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="acdb5-157">tooadd a new connected host, click **Add new**, enter a name for hello host and its iSCSI Qualified Name (IQN), and then click **Add**.</span></span>
   
    ![Birim ekle](./media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. <span data-ttu-id="acdb5-159">Biriminiz yapılandırma tamamladığınızda tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="acdb5-159">When you've finished configuring your volume, click **Create**.</span></span> <span data-ttu-id="acdb5-160">Bir birim belirtilen hello ile oluşturulacak ayarlar ve aynı hello hello başarılı oluşturulmasını bir bildirim görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="acdb5-160">A volume will be created with hello specified settings and you will see a notification on hello successful creation of hello same.</span></span> <span data-ttu-id="acdb5-161">Varsayılan olarak yedekleme hello birim için etkin.</span><span class="sxs-lookup"><span data-stu-id="acdb5-161">By default backup will be enabled for hello volume.</span></span>
5. <span data-ttu-id="acdb5-162">Birim hello tooconfirm edildi başarıyla oluşturuldu, Git toohello **birimleri** dikey.</span><span class="sxs-lookup"><span data-stu-id="acdb5-162">tooconfirm that hello volume was successfully created, go toohello **Volumes** blade.</span></span> <span data-ttu-id="acdb5-163">Listelenen hello birim görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="acdb5-163">You should see hello volume listed.</span></span>
   
    ![Birim oluşturma başarılı](./media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a><span data-ttu-id="acdb5-165">Bir birim değiştirme</span><span class="sxs-lookup"><span data-stu-id="acdb5-165">Modify a volume</span></span>

<span data-ttu-id="acdb5-166">Merhaba birime erişmek toochange hello konakları gerektiğinde bir birim değiştirin.</span><span class="sxs-lookup"><span data-stu-id="acdb5-166">Modify a volume when you need toochange hello hosts that access hello volume.</span></span> <span data-ttu-id="acdb5-167">Merhaba birim oluşturulduktan sonra hello biriminin diğer öznitelikleri değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="acdb5-167">hello other attributes of a volume cannot be modified once hello volume has been created.</span></span>

#### <a name="toomodify-a-volume"></a><span data-ttu-id="acdb5-168">toomodify bir birim</span><span class="sxs-lookup"><span data-stu-id="acdb5-168">toomodify a volume</span></span>

1. <span data-ttu-id="acdb5-169">Merhaba gelen **birimleri** seçin istediğinizden, toomodify birim üzerinde hangi hello bulunduğu sanal dizinin hello hello StorSimple hizmeti Özet dikey ayarı.</span><span class="sxs-lookup"><span data-stu-id="acdb5-169">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you toomodify resides.</span></span>
2. <span data-ttu-id="acdb5-170">**Seçin** hello birimi ve'ı tıklatın **bağlı Konaklar** tooview hello şu anda bağlı ana bilgisayar ve tooa farklı sunucu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="acdb5-170">**Select** hello volume and click **Connected hosts** tooview hello currently connected host and modify it tooa different server.</span></span>
   
    ![Toplu düzenleme](./media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. <span data-ttu-id="acdb5-172">Merhaba tıklayarak yaptığınız değişiklikleri kaydetmek **kaydetmek** komut çubuğu.</span><span class="sxs-lookup"><span data-stu-id="acdb5-172">Save your changes by clicking hello **Save** command bar.</span></span> <span data-ttu-id="acdb5-173">Belirtilen ayarlarınızı uygulanır ve bir bildirim görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="acdb5-173">Your specified settings will be applied and you will see a notification.</span></span>

## <a name="take-a-volume-offline"></a><span data-ttu-id="acdb5-174">Bir birim çevrimdışı duruma getirin</span><span class="sxs-lookup"><span data-stu-id="acdb5-174">Take a volume offline</span></span>

<span data-ttu-id="acdb5-175">Toomodify veya delete planlarken tootake çevrimdışı bir birim gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="acdb5-175">You may need tootake a volume offline when you are planning toomodify it or delete it.</span></span> <span data-ttu-id="acdb5-176">Bir birim çevrimdışı olduğunda okuma-yazma erişimi için kullanılabilir değildir.</span><span class="sxs-lookup"><span data-stu-id="acdb5-176">When a volume is offline, it is not available for read-write access.</span></span> <span data-ttu-id="acdb5-177">Tootake hello birim çevrimdışı hello aygıt yanı sıra hello ana bilgisayar gerekir.</span><span class="sxs-lookup"><span data-stu-id="acdb5-177">You will need tootake hello volume offline on hello host as well as on hello device.</span></span>

#### <a name="tootake-a-volume-offline"></a><span data-ttu-id="acdb5-178">tootake çevrimdışı bir birim</span><span class="sxs-lookup"><span data-stu-id="acdb5-178">tootake a volume offline</span></span>

1. <span data-ttu-id="acdb5-179">Söz konusu Hello birim çevrimdışı duruma getirmeden önce kullanımda olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="acdb5-179">Make sure that hello volume in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="acdb5-180">Çevrimdışı Hello birim hello konakta ilk alın.</span><span class="sxs-lookup"><span data-stu-id="acdb5-180">Take hello volume offline on hello host first.</span></span> <span data-ttu-id="acdb5-181">Bu, olası tüm hello birimdeki veri bozulması riskini ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="acdb5-181">This eliminates any potential risk of data corruption on hello volume.</span></span> <span data-ttu-id="acdb5-182">Belirli adımlar için işletim sistemi için toohello yönergeler bakın.</span><span class="sxs-lookup"><span data-stu-id="acdb5-182">For specific steps, refer toohello instructions for your host operating system.</span></span>
3. <span data-ttu-id="acdb5-183">Hello konak Hello birimde çevrimdışıysa, hello birim çevrimdışı hello dizisinde hello aşağıdaki adımları gerçekleştirerek başlatıldıktan sonra:</span><span class="sxs-lookup"><span data-stu-id="acdb5-183">After hello volume on hello host is offline, take hello volume on hello array  offline by performing hello following steps:</span></span>
   
   * <span data-ttu-id="acdb5-184">Merhaba gelen **birimleri** seçin istediğinizden, çevrimdışı tootake birim üzerinde hangi hello bulunduğu sanal dizinin hello hello StorSimple hizmeti Özet dikey ayarı.</span><span class="sxs-lookup"><span data-stu-id="acdb5-184">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you tootake offline resides.</span></span>
   * <span data-ttu-id="acdb5-185">**Seçin** hello birim ve tıklayın **...**  (Alternatif olarak bu satırı sağ) ve hello bağlam menüsünden seçin **çevrimdışına**.</span><span class="sxs-lookup"><span data-stu-id="acdb5-185">**Select** hello volume and click **...** (alternately right-click in this row) and from hello context menu, select **Take offline**.</span></span>
     
        ![Çevrimdışı birim](./media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * <span data-ttu-id="acdb5-187">Merhaba hello bilgileri gözden **çevrimdışına** dikey ve hello işleminin onaylamış olursunuz.</span><span class="sxs-lookup"><span data-stu-id="acdb5-187">Review hello information in hello **Take offline** blade and confirm your acceptance of hello operation.</span></span> <span data-ttu-id="acdb5-188">Tıklatın **çevrimdışına** tootake hello çevrimdışı birim.</span><span class="sxs-lookup"><span data-stu-id="acdb5-188">Click **Take offline** tootake hello volume offline.</span></span> <span data-ttu-id="acdb5-189">Merhaba işlem devam ettiğinden, bir bildirim görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="acdb5-189">You will see a notification of hello operation in progress.</span></span>
   * <span data-ttu-id="acdb5-190">Merhaba birimi başarıyla çevrimdışı duruma tooconfirm Git toohello **birimleri** dikey.</span><span class="sxs-lookup"><span data-stu-id="acdb5-190">tooconfirm that hello volume was successfully taken offline, go toohello **Volumes** blade.</span></span> <span data-ttu-id="acdb5-191">Merhaba birimin hello durumu çevrimdışı olarak görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="acdb5-191">You should see hello status of hello volume as offline.</span></span>
     
       ![Çevrimdışı birim onayı](./media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a><span data-ttu-id="acdb5-193">Bir birim Sil</span><span class="sxs-lookup"><span data-stu-id="acdb5-193">Delete a volume</span></span>

> [!IMPORTANT]
> <span data-ttu-id="acdb5-194">Yalnızca çevrimdışı ise, bir birim silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acdb5-194">You can delete a volume only if it is offline.</span></span>
> 
> 

<span data-ttu-id="acdb5-195">Aşağıdaki adımları toodelete bir birim hello tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="acdb5-195">Complete hello following steps toodelete a volume.</span></span>

#### <a name="toodelete-a-volume"></a><span data-ttu-id="acdb5-196">toodelete bir birim</span><span class="sxs-lookup"><span data-stu-id="acdb5-196">toodelete a volume</span></span>

1. <span data-ttu-id="acdb5-197">Merhaba gelen **birimleri** seçin istediğinizden, toodelete birim üzerinde hangi hello bulunduğu sanal dizinin hello hello StorSimple hizmeti Özet dikey ayarı.</span><span class="sxs-lookup"><span data-stu-id="acdb5-197">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you toodelete resides.</span></span>
2. <span data-ttu-id="acdb5-198">**Seçin** hello birim ve tıklayın **...**  (Alternatif olarak bu satırı sağ) ve hello bağlam menüsünden seçin **silmek**.</span><span class="sxs-lookup"><span data-stu-id="acdb5-198">**Select** hello volume and click **...** (alternately right-click in this row) and from hello context menu, select **Delete**.</span></span>
   
    ![Birim Sil](./media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. <span data-ttu-id="acdb5-200">Merhaba durumunu denetlemek hello hacmi toodelete istiyor.</span><span class="sxs-lookup"><span data-stu-id="acdb5-200">Check hello status of hello volume you want toodelete.</span></span> <span data-ttu-id="acdb5-201">Merhaba birim toodelete istediğiniz çevrimdışı durumda değilse, bunu çevrimdışı ilk, aşağıdaki hello adımlar [bir birim çevrimdışına](#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="acdb5-201">If hello volume you want toodelete is not offline, take it offline first, following hello steps in [Take a volume offline](#take-a-volume-offline).</span></span>
4. <span data-ttu-id="acdb5-202">Merhaba onaylamanız istendiğinde **silmek** dikey penceresinde hello onay kabul edin ve tıklatın **silmek**.</span><span class="sxs-lookup"><span data-stu-id="acdb5-202">When prompted for confirmation in hello **Delete** blade, accept hello confirmation and click **Delete**.</span></span> <span data-ttu-id="acdb5-203">Merhaba birim artık silinecek ve hello **birimleri** dikey penceresinde hello sanal dizi birimlerin hello güncelleştirilmiş listesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="acdb5-203">hello volume will now be deleted and hello **Volumes** blade will show hello updated list of volumes within hello virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="acdb5-204">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="acdb5-204">Next steps</span></span>

<span data-ttu-id="acdb5-205">Nasıl çok öğrenin[bir StorSimple biriminin kopyalama](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="acdb5-205">Learn how too[clone a StorSimple volume](storsimple-virtual-array-clone.md).</span></span>

