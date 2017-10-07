---
title: "StorSimple sanal dizinin aaaManage paylaşır | Microsoft Docs"
description: "Merhaba StorSimple Aygıt Yöneticisi'ni tanımlar ve açıklar nasıl toouse, StorSimple sanal dizinizi toomanage paylaşımlarında."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: 0a799c83-fde5-4f3f-af0e-67535d1882b6
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 9b57d7ec7c0b7de5a22e1b816daa8852d0f32a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-shares-on-hello-storsimple-virtual-array"></a><span data-ttu-id="f92ce-103">StorSimple sanal dizinin hello üzerinde Hello StorSimple cihaz Yöneticisi hizmeti toomanage paylaşımları kullanın</span><span class="sxs-lookup"><span data-stu-id="f92ce-103">Use hello StorSimple Device Manager service toomanage shares on hello StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="f92ce-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f92ce-104">Overview</span></span>

<span data-ttu-id="f92ce-105">Bu öğretici nasıl toouse StorSimple cihaz Yöneticisi hizmeti toocreate hello ve StorSimple sanal dizinizi paylaşımlarında yönetmek açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f92ce-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage shares on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="f92ce-106">Merhaba StorSimple cihaz Yöneticisi hizmeti hello StorSimple çözümünüzün bir tek web arabiriminden yönetmenizi sağlayan Azure portalı bir uzantıdır.</span><span class="sxs-lookup"><span data-stu-id="f92ce-106">hello StorSimple Device Manager service is an extension in hello Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="f92ce-107">Toplama toomanaging paylaşımları ve birimler, hello StorSimple cihaz Yöneticisi hizmeti tooview kullanın ve cihazları yönetmek, uyarıları görüntüleyebilir, yedekleme ilkelerini yönetme ve hello yedekleme kataloğunu yönetir.</span><span class="sxs-lookup"><span data-stu-id="f92ce-107">In addition toomanaging shares and volumes, you can use hello StorSimple Device Manager service tooview and manage devices, view alerts, manage backup policies, and manage hello backup catalog.</span></span>

## <a name="share-types"></a><span data-ttu-id="f92ce-108">Paylaşım türleri</span><span class="sxs-lookup"><span data-stu-id="f92ce-108">Share Types</span></span>

<span data-ttu-id="f92ce-109">StorSimple paylaşımları olabilir:</span><span class="sxs-lookup"><span data-stu-id="f92ce-109">StorSimple shares can be:</span></span>

* <span data-ttu-id="f92ce-110">**Yerel olarak sabitlenmiş**: bu paylaşımlar verileri her zaman hello dizisinde kalır ve toohello buluta dağıtılmamasını.</span><span class="sxs-lookup"><span data-stu-id="f92ce-110">**Locally pinned**: Data in these shares stays on hello array at all times and does not spill toohello cloud.</span></span>
* <span data-ttu-id="f92ce-111">**Katmanlı**: bu paylaşımlar verilerde toohello bulut sığdırmaya.</span><span class="sxs-lookup"><span data-stu-id="f92ce-111">**Tiered**: Data in these shares can spill toohello cloud.</span></span> <span data-ttu-id="f92ce-112">Katmanlı bir paylaşımı oluşturduğunuzda, hello alanın % 10'yaklaşık hello yerel katmanında sağlanır ve hello alanı % 90'ını hello bulutta sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f92ce-112">When you create a tiered share, approximately 10 % of hello space is provisioned on hello local tier and 90 % of hello space is provisioned in hello cloud.</span></span> <span data-ttu-id="f92ce-113">Örneğin, 1 TB paylaşımı sağlanan, 100 GB hello yerel alan bulunması ve 900 GB hello bulutta kullanılacak ne zaman veri katmanlarını hello.</span><span class="sxs-lookup"><span data-stu-id="f92ce-113">For example, if you provisioned a 1 TB share, 100 GB would reside in hello local space and 900 GB would be used in hello cloud when hello data tiers.</span></span> <span data-ttu-id="f92ce-114">Bu, sırayla hello cihazda tüm hello yerel alana çalıştırırsanız (Merhaba % 10 hello yerel katmanı kullanılamaz gerektirdiğinden), katmanlı bir paylaşım sağlayamazsınız olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="f92ce-114">This in turn implies that if you run out of all hello local space on hello device, you cannot provision a tiered share (because hello 10 % required on hello local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="f92ce-115">Sağlanan kapasite</span><span class="sxs-lookup"><span data-stu-id="f92ce-115">Provisioned capacity</span></span>

<span data-ttu-id="f92ce-116">Aşağıdaki tablonun her paylaşım türü için en fazla sağlanan kapasite toohello bakın.</span><span class="sxs-lookup"><span data-stu-id="f92ce-116">Refer toohello following table for maximum provisioned capacity for each share type.</span></span>

| <span data-ttu-id="f92ce-117">**Sınır tanımlayıcısı**</span><span class="sxs-lookup"><span data-stu-id="f92ce-117">**Limit identifier**</span></span> | <span data-ttu-id="f92ce-118">**Sınırı**</span><span class="sxs-lookup"><span data-stu-id="f92ce-118">**Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="f92ce-119">Katmanlı bir paylaşımı en küçük boyut</span><span class="sxs-lookup"><span data-stu-id="f92ce-119">Minimum size of a tiered share</span></span> |<span data-ttu-id="f92ce-120">500 GB</span><span class="sxs-lookup"><span data-stu-id="f92ce-120">500 GB</span></span> |
| <span data-ttu-id="f92ce-121">Katmanlı bir paylaşımı en büyük boyutu</span><span class="sxs-lookup"><span data-stu-id="f92ce-121">Maximum size of a tiered share</span></span> |<span data-ttu-id="f92ce-122">20 TB</span><span class="sxs-lookup"><span data-stu-id="f92ce-122">20 TB</span></span> |
| <span data-ttu-id="f92ce-123">Yerel olarak sabitlenmiş bir paylaşımı en küçük boyut</span><span class="sxs-lookup"><span data-stu-id="f92ce-123">Minimum size of a locally pinned share</span></span> |<span data-ttu-id="f92ce-124">50 GB</span><span class="sxs-lookup"><span data-stu-id="f92ce-124">50 GB</span></span> |
| <span data-ttu-id="f92ce-125">Yerel olarak sabitlenmiş bir paylaşımı en büyük boyutu</span><span class="sxs-lookup"><span data-stu-id="f92ce-125">Maximum size of a locally pinned share</span></span> |<span data-ttu-id="f92ce-126">2 TB</span><span class="sxs-lookup"><span data-stu-id="f92ce-126">2 TB</span></span> |

## <a name="hello-shares-blade"></a><span data-ttu-id="f92ce-127">Merhaba paylaşımları dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="f92ce-127">hello Shares blade</span></span>

<span data-ttu-id="f92ce-128">Merhaba **paylaşımları** StorSimple hizmeti Özet dikey menüsünde belirli bir StorSimple dizi depolama paylaşımları hello listesini görüntüler ve toomanage sağlayan bunları.</span><span class="sxs-lookup"><span data-stu-id="f92ce-128">hello **Shares** menu on your StorSimple service summary blade displays hello list of storage shares on a given StorSimple array and allows you toomanage them.</span></span>

![Paylaşımlar dikey penceresi](./media/storsimple-virtual-array-manage-shares/shares-blade.png)

<span data-ttu-id="f92ce-130">Bir paylaşım öznitelikleri bir dizi oluşur:</span><span class="sxs-lookup"><span data-stu-id="f92ce-130">A share consists of a series of attributes:</span></span>

* <span data-ttu-id="f92ce-131">**Paylaşım adı** – benzersiz olmalı ve hello paylaşımı tanımlamanıza yardımcı olan açıklayıcı bir ad.</span><span class="sxs-lookup"><span data-stu-id="f92ce-131">**Share Name** – A descriptive name that must be unique and helps identify hello share.</span></span>
* <span data-ttu-id="f92ce-132">**Durum** – çevrimiçi veya çevrimdışı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f92ce-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="f92ce-133">Bir paylaşım çevrimdışı olduğunda, kullanıcılar hello paylaşımının mümkün tooaccess olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="f92ce-133">If a share is offline, users of hello share will not be able tooaccess it.</span></span>
* <span data-ttu-id="f92ce-134">**Tür** – hello paylaşımı olup olmadığını belirten **katmanlı** (Merhaba varsayılan) veya **yerel olarak sabitlenmiş**.</span><span class="sxs-lookup"><span data-stu-id="f92ce-134">**Type** – Indicates whether hello share is **Tiered** (hello default) or **Locally pinned**.</span></span>
* <span data-ttu-id="f92ce-135">**Kapasite** – hello karşılaştırılan toohello toplam hello paylaşımında depolanan veri miktarını olarak kullanılan veri miktarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="f92ce-135">**Capacity** – specifies hello amount of data used as compared toohello total amount of data that can be stored on hello share.</span></span>
* <span data-ttu-id="f92ce-136">**Açıklama** – hello paylaşımı açıklamak yardımcı olan isteğe bağlı bir ayar.</span><span class="sxs-lookup"><span data-stu-id="f92ce-136">**Description** – An optional setting that helps describe hello share.</span></span>
* <span data-ttu-id="f92ce-137">**İzinleri** -Windows Explorer ile yönetilebilir hello NTFS izinleri toohello paylaşımı.</span><span class="sxs-lookup"><span data-stu-id="f92ce-137">**Permissions** - hello NTFS permissions toohello share that can be managed through Windows Explorer.</span></span>
* <span data-ttu-id="f92ce-138">**Yedekleme** – hello StorSimple sanal dizinin tüm paylaşımlar yedekleme için otomatik olarak etkinleştirilmiş durumda.</span><span class="sxs-lookup"><span data-stu-id="f92ce-138">**Backup** – In case of hello StorSimple Virtual Array, all shares are automatically enabled for backup.</span></span>

![Paylaşımlar ayrıntıları](./media/storsimple-virtual-array-manage-shares/share-details.png)

<span data-ttu-id="f92ce-140">Bu öğretici tooperform hello görevleri aşağıdaki Hello yönergeleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="f92ce-140">Use hello instructions in this tutorial tooperform hello following tasks:</span></span>

* <span data-ttu-id="f92ce-141">Paylaşım Ekle</span><span class="sxs-lookup"><span data-stu-id="f92ce-141">Add a share</span></span>
* <span data-ttu-id="f92ce-142">Bir paylaşımı değiştirme</span><span class="sxs-lookup"><span data-stu-id="f92ce-142">Modify a share</span></span>
* <span data-ttu-id="f92ce-143">Bir paylaşım çevrimdışı duruma getirin</span><span class="sxs-lookup"><span data-stu-id="f92ce-143">Take a share offline</span></span>
* <span data-ttu-id="f92ce-144">Bir paylaşımı silme</span><span class="sxs-lookup"><span data-stu-id="f92ce-144">Delete a share</span></span>

## <a name="add-a-share"></a><span data-ttu-id="f92ce-145">Paylaşım Ekle</span><span class="sxs-lookup"><span data-stu-id="f92ce-145">Add a share</span></span>

1. <span data-ttu-id="f92ce-146">Merhaba StorSimple hizmeti Özet dikey penceresinden, tıklayın **+ Ekle paylaşımı** hello komut çubuğundan.</span><span class="sxs-lookup"><span data-stu-id="f92ce-146">From hello StorSimple service summary blade, click **+ Add share** from hello command bar.</span></span> <span data-ttu-id="f92ce-147">Merhaba açılır **Ekle paylaşımı** dikey.</span><span class="sxs-lookup"><span data-stu-id="f92ce-147">This opens up hello **Add share** blade.</span></span>

    ![Paylaşım Ekle](./media/storsimple-virtual-array-manage-shares/add-share.png)

2. <span data-ttu-id="f92ce-149">Merhaba, **Ekle paylaşımı** dikey penceresinde, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="f92ce-149">In hello **Add share** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="f92ce-150">Merhaba, **paylaşım adı** alanında, paylaşımınıza için benzersiz bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="f92ce-150">In hello **Share name** field, enter a unique name for your share.</span></span> <span data-ttu-id="f92ce-151">Merhaba adı 3 too127 karakter içeren bir dize olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f92ce-151">hello name must be a string that contains 3 too127 characters.</span></span>

    2. <span data-ttu-id="f92ce-152">İsteğe bağlı bir **açıklama** hello paylaşımı için.</span><span class="sxs-lookup"><span data-stu-id="f92ce-152">An optional **Description** for hello share.</span></span> <span data-ttu-id="f92ce-153">Merhaba açıklama hello paylaşım sahiplerini tanımlamaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="f92ce-153">hello description will help identify hello share owners.</span></span>

    3. <span data-ttu-id="f92ce-154">Merhaba, **türü** açılır listesinde, belirleyin olup olmadığını toocreate bir **katmanlı** veya **yerel olarak sabitlenmiş** paylaşın.</span><span class="sxs-lookup"><span data-stu-id="f92ce-154">In hello **Type** dropdown list, specify whether toocreate a **Tiered** or **Locally pinned** share.</span></span> <span data-ttu-id="f92ce-155">Yerel GARANTİLERİN, düşük gecikme ve yüksek performansın gerektiği iş yükleri için seçin **Paylaşımı'yerel olarak sabitlenmiş**.</span><span class="sxs-lookup"><span data-stu-id="f92ce-155">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned share**.</span></span> <span data-ttu-id="f92ce-156">Diğer tüm veriler için seçin **katmanlı** paylaşın.</span><span class="sxs-lookup"><span data-stu-id="f92ce-156">For all other data, select **Tiered** share.</span></span>

    4. <span data-ttu-id="f92ce-157">Merhaba, **kapasite** alanında, hello hello paylaşımı boyutunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="f92ce-157">In hello **Capacity** field, specify hello size of hello share.</span></span> <span data-ttu-id="f92ce-158">Katmanlı bir paylaşımı, 500 GB ile 20 TB arasında olmalıdır ve yerel olarak sabitlenmiş bir paylaşımı, 50 GB ile 2 TB arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f92ce-158">A tiered share must be between 500 GB and 20 TB and a locally pinned share must be between 50 GB and 2 TB.</span></span>

    5. <span data-ttu-id="f92ce-159">Merhaba, **kümesine varsayılan tam izinleri** alan, hello izinleri toohello kullanıcı veya bu paylaşıma erişen hello grubuna atayın.</span><span class="sxs-lookup"><span data-stu-id="f92ce-159">In hello **Set default full permissions to** field, assign hello permissions toohello user, or hello group that is accessing this share.</span></span> <span data-ttu-id="f92ce-160">Merhaba kullanıcı veya hello kullanıcı grubunda Hello adını belirtin  _john@contoso.com_  biçimi.</span><span class="sxs-lookup"><span data-stu-id="f92ce-160">Specify hello name of hello user or hello user group in _john@contoso.com_ format.</span></span> <span data-ttu-id="f92ce-161">Bir kullanıcı grubu (yerine tek bir kullanıcı) tooallow yönetici ayrıcalıkları tooaccess bu paylaşımları kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="f92ce-161">We recommend that you use a user group (instead of a single user) tooallow admin privileges tooaccess these shares.</span></span> <span data-ttu-id="f92ce-162">Merhaba izinlerini burada atadıktan sonra bu izinleri dosya Gezgini toomodify sonra kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f92ce-162">After you have assigned hello permissions here, you can then use File Explorer toomodify these permissions.</span></span>
3. <span data-ttu-id="f92ce-163">Paylaşımınıza yapılandırma tamamladığınızda tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="f92ce-163">When you've finished configuring your share, click **Create**.</span></span> <span data-ttu-id="f92ce-164">Bir paylaşımı ile belirtilen hello oluşturulacak ayarları ve bir bildirim görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="f92ce-164">A share will be created with hello specified settings and you will see a notification.</span></span> <span data-ttu-id="f92ce-165">Varsayılan olarak, yedekleme hello paylaşımı için etkin.</span><span class="sxs-lookup"><span data-stu-id="f92ce-165">By default, backup will be enabled for hello share.</span></span>
4. <span data-ttu-id="f92ce-166">Paylaşım hello tooconfirm edildi başarıyla oluşturuldu, Git toohello **paylaşımları** dikey.</span><span class="sxs-lookup"><span data-stu-id="f92ce-166">tooconfirm that hello share was successfully created, go toohello **Shares** blade.</span></span> <span data-ttu-id="f92ce-167">Listelenen paylaşmak hello görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f92ce-167">You should see hello share listed.</span></span>
   
    ![Paylaşımı oluşturma başarılı](./media/storsimple-virtual-array-manage-shares/share-success.png)

## <a name="modify-a-share"></a><span data-ttu-id="f92ce-169">Bir paylaşımı değiştirme</span><span class="sxs-lookup"><span data-stu-id="f92ce-169">Modify a share</span></span>

<span data-ttu-id="f92ce-170">Merhaba paylaşımı toochange hello açıklama gerektiğinde bir paylaşımı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f92ce-170">Modify a share when you need toochange hello description of hello share.</span></span> <span data-ttu-id="f92ce-171">Merhaba paylaşımı oluşturulduktan sonra başka bir paylaşım özellikleri değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="f92ce-171">No other share properties can be modified once hello share is created.</span></span>

#### <a name="toomodify-a-share"></a><span data-ttu-id="f92ce-172">toomodify bir paylaşımı</span><span class="sxs-lookup"><span data-stu-id="f92ce-172">toomodify a share</span></span>

1. <span data-ttu-id="f92ce-173">Merhaba gelen **paylaşımları** seçin istediğinizden, toomodify paylaşımı üzerinde hangi hello bulunduğu sanal dizinin hello hello StorSimple hizmeti Özet dikey ayarı.</span><span class="sxs-lookup"><span data-stu-id="f92ce-173">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish you toomodify resides.</span></span>
2. <span data-ttu-id="f92ce-174">**Seçin** hello paylaşımı tooview hello geçerli açıklama ve değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f92ce-174">**Select** hello share tooview hello current description and modify it.</span></span>
3. <span data-ttu-id="f92ce-175">Merhaba tıklayarak yaptığınız değişiklikleri kaydetmek **kaydetmek** komut çubuğu.</span><span class="sxs-lookup"><span data-stu-id="f92ce-175">Save your changes by clicking hello **Save** command bar.</span></span> <span data-ttu-id="f92ce-176">Belirtilen ayarlarınızı uygulanır ve bir bildirim görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="f92ce-176">Your specified settings will be applied and you will see a notification.</span></span>
   
    ![ <span data-ttu-id="f92ce-177">Paylaşım Düzenle</span><span class="sxs-lookup"><span data-stu-id="f92ce-177">Edit share</span></span>](./media/storsimple-virtual-array-manage-shares/share-edit.png)

## <a name="take-a-share-offline"></a><span data-ttu-id="f92ce-178">Bir paylaşım çevrimdışı duruma getirin</span><span class="sxs-lookup"><span data-stu-id="f92ce-178">Take a share offline</span></span>

<span data-ttu-id="f92ce-179">Toomodify veya delete planlarken tootake çevrimdışı bir paylaşımı gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="f92ce-179">You may need tootake a share offline when you are planning toomodify it or delete it.</span></span> <span data-ttu-id="f92ce-180">Bir paylaşım çevrimdışı olduğunda okuma-yazma erişimi için kullanılabilir değildir.</span><span class="sxs-lookup"><span data-stu-id="f92ce-180">When a share is offline, it is not available for read-write access.</span></span> <span data-ttu-id="f92ce-181">Tootake hello paylaşımı çevrimdışı hello aygıt yanı sıra hello ana bilgisayar gerekir.</span><span class="sxs-lookup"><span data-stu-id="f92ce-181">You will need tootake hello share offline on hello host as well as on hello device.</span></span>

#### <a name="tootake-a-share-offline"></a><span data-ttu-id="f92ce-182">tootake çevrimdışı bir paylaşımı</span><span class="sxs-lookup"><span data-stu-id="f92ce-182">tootake a share offline</span></span>

1. <span data-ttu-id="f92ce-183">Söz konusu hello paylaşan çevrimdışı duruma getirmeden önce kullanımda olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="f92ce-183">Make sure that hello share in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="f92ce-184">Merhaba paylaşımı hello aşağıdaki adımları gerçekleştirerek çevrimdışı hello dizisinde alın:</span><span class="sxs-lookup"><span data-stu-id="f92ce-184">Take hello share on hello array offline by performing hello following steps:</span></span>
   
    1. <span data-ttu-id="f92ce-185">Merhaba gelen **paylaşımları** seçin istediğinizden, çevrimdışı tootake paylaşımı üzerinde hangi hello bulunduğu sanal dizinin hello hello StorSimple hizmeti Özet dikey ayarı.</span><span class="sxs-lookup"><span data-stu-id="f92ce-185">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish you tootake offline resides.</span></span>

    2. <span data-ttu-id="f92ce-186">**Seçin** hello paylaşım ve tıklatın **...**  (Alternatif olarak bu satırı sağ) ve hello bağlam menüsünden seçin **çevrimdışına**.</span><span class="sxs-lookup"><span data-stu-id="f92ce-186">**Select** hello share and Click **...** (alternately right-click in this row) and from hello context menu, select **Take offline**.</span></span>
     
        ![Çevrimdışı paylaşımı](./media/storsimple-virtual-array-manage-shares/shares-offline.png)

    3. <span data-ttu-id="f92ce-188">Merhaba hello bilgileri gözden **çevrimdışına** dikey ve hello işleminin onaylamış olursunuz.</span><span class="sxs-lookup"><span data-stu-id="f92ce-188">Review hello information in hello **Take offline** blade and confirm your acceptance of hello operation.</span></span> <span data-ttu-id="f92ce-189">Tıklatın **çevrimdışına** tootake hello çevrimdışı paylaşımı.</span><span class="sxs-lookup"><span data-stu-id="f92ce-189">Click **Take offline** tootake hello share offline.</span></span> <span data-ttu-id="f92ce-190">Merhaba işlem devam ettiğinden, bir bildirim görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="f92ce-190">You will see a notification of hello operation in progress.</span></span>

    4. <span data-ttu-id="f92ce-191">Paylaşım hello tooconfirm çevrimdışı, Git toohello başarıyla alındığı **paylaşımları** dikey.</span><span class="sxs-lookup"><span data-stu-id="f92ce-191">tooconfirm that hello share was successfully taken offline, go toohello **Shares** blade.</span></span> <span data-ttu-id="f92ce-192">Çevrimdışı olarak hello paylaşımı hello durumunu görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f92ce-192">You should see hello status of hello share as offline.</span></span>

## <a name="delete-a-share"></a><span data-ttu-id="f92ce-193">Bir paylaşımı silme</span><span class="sxs-lookup"><span data-stu-id="f92ce-193">Delete a share</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f92ce-194">Yalnızca çevrimdışı ise, bir paylaşım silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f92ce-194">You can delete a share only if it is offline.</span></span>


<span data-ttu-id="f92ce-195">Aşağıdaki adımları toodelete bir paylaşımı hello tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="f92ce-195">Complete hello following steps toodelete a share.</span></span>

#### <a name="toodelete-a-share"></a><span data-ttu-id="f92ce-196">toodelete bir paylaşımı</span><span class="sxs-lookup"><span data-stu-id="f92ce-196">toodelete a share</span></span>

1. <span data-ttu-id="f92ce-197">Merhaba gelen **paylaşımları** seçin hangi hello paylaşımında istediğiniz toodelete bulunduğu sanal dizinin hello hello StorSimple hizmeti Özet dikey ayarı.</span><span class="sxs-lookup"><span data-stu-id="f92ce-197">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish toodelete resides.</span></span>
2. <span data-ttu-id="f92ce-198">**Seçin** hello paylaşım ve tıklatın **...**  (Alternatif olarak bu satırı sağ) ve hello bağlam menüsünden seçin **silmek**.</span><span class="sxs-lookup"><span data-stu-id="f92ce-198">**Select** hello share and Click **...** (alternately right-click in this row) and from hello context menu, select **Delete**.</span></span>
   
    ![Paylaşımı silin](./media/storsimple-virtual-array-manage-shares/share-delete.png)
3. <span data-ttu-id="f92ce-200">Merhaba durumunu denetlemek hello payı toodelete istiyor.</span><span class="sxs-lookup"><span data-stu-id="f92ce-200">Check hello status of hello share you want toodelete.</span></span> <span data-ttu-id="f92ce-201">Merhaba paylaşımı toodelete istediğiniz çevrimdışı durumda değilse, onu önce çevrimdışına.</span><span class="sxs-lookup"><span data-stu-id="f92ce-201">If hello share you want toodelete is not offline, take it offline first.</span></span> <span data-ttu-id="f92ce-202">Merhaba adımları [bir paylaşımı çevrimdışına](#take-a-share-offline).</span><span class="sxs-lookup"><span data-stu-id="f92ce-202">Follow hello steps in [Take a share offline](#take-a-share-offline).</span></span>
4. <span data-ttu-id="f92ce-203">Merhaba onaylamanız istendiğinde **silmek** dikey penceresinde hello onay kabul edin ve tıklatın **silmek**.</span><span class="sxs-lookup"><span data-stu-id="f92ce-203">When prompted for confirmation in hello **Delete** blade, accept hello confirmation and click **Delete**.</span></span> <span data-ttu-id="f92ce-204">Merhaba paylaşım şimdi silinecek ve hello **paylaşımları** dikey penceresinde hello sanal dizi paylaşımlarının hello güncelleştirilmiş listesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="f92ce-204">hello share will now be deleted and hello **Shares** blade shows hello updated list of shares within hello virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f92ce-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f92ce-205">Next steps</span></span>
<span data-ttu-id="f92ce-206">Nasıl çok öğrenin[bir StorSimple paylaşımı kopyalama](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="f92ce-206">Learn how too[clone a StorSimple share](storsimple-virtual-array-clone.md).</span></span>

