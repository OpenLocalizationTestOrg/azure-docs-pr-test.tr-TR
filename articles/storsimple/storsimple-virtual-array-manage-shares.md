---
title: "StorSimple sanal dizinin paylaşımlarını yönetmek | Microsoft Docs"
description: "StorSimple cihaz Yöneticisi'ni açıklar ve bunu, StorSimple sanal dizisindeki paylaşımlarını yönetmek için nasıl kullanılacağını açıklar."
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
ms.openlocfilehash: e5c62689de36baa175001f5f4f70d87568876ef0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-manage-shares-on-the-storsimple-virtual-array"></a><span data-ttu-id="d017a-103">StorSimple sanal dizisindeki paylaşımlarını yönetmek için StorSimple cihaz Yöneticisi hizmetini kullanma</span><span class="sxs-lookup"><span data-stu-id="d017a-103">Use the StorSimple Device Manager service to manage shares on the StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="d017a-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="d017a-104">Overview</span></span>

<span data-ttu-id="d017a-105">Bu öğretici StorSimple cihaz Yöneticisi hizmeti oluşturmak ve StorSimple sanal dizinizi paylaşımlarında yönetmek için nasıl kullanılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="d017a-105">This tutorial explains how to use the StorSimple Device Manager service to create and manage shares on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="d017a-106">StorSimple cihaz Yöneticisi hizmeti, StorSimple çözümünüzün bir tek web arabiriminden yönetmenizi sağlayan Azure portalında bir uzantısıdır.</span><span class="sxs-lookup"><span data-stu-id="d017a-106">The StorSimple Device Manager service is an extension in the Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="d017a-107">Paylaşımları ve birimler yönetmeye ek olarak, StorSimple cihaz Yöneticisi hizmeti görüntülemek ve cihazları yönetmek, uyarıları görüntülemek, yedekleme ilkelerini yönetmek ve yedekleme kataloğu yönetmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d017a-107">In addition to managing shares and volumes, you can use the StorSimple Device Manager service to view and manage devices, view alerts, manage backup policies, and manage the backup catalog.</span></span>

## <a name="share-types"></a><span data-ttu-id="d017a-108">Paylaşım türleri</span><span class="sxs-lookup"><span data-stu-id="d017a-108">Share Types</span></span>

<span data-ttu-id="d017a-109">StorSimple paylaşımları olabilir:</span><span class="sxs-lookup"><span data-stu-id="d017a-109">StorSimple shares can be:</span></span>

* <span data-ttu-id="d017a-110">**Yerel olarak sabitlenmiş**: bu paylaşımlar verileri her zaman dizi kalmasını ve buluta dağıtılmamasını.</span><span class="sxs-lookup"><span data-stu-id="d017a-110">**Locally pinned**: Data in these shares stays on the array at all times and does not spill to the cloud.</span></span>
* <span data-ttu-id="d017a-111">**Katmanlı**: bu paylaşımlar verileri buluta sığdırmaya.</span><span class="sxs-lookup"><span data-stu-id="d017a-111">**Tiered**: Data in these shares can spill to the cloud.</span></span> <span data-ttu-id="d017a-112">Katmanlı bir paylaşımı oluşturduğunuzda, alanın % 10'yaklaşık yerel katmanında sağlanır ve alan % 90'ını bulutta sağlanır.</span><span class="sxs-lookup"><span data-stu-id="d017a-112">When you create a tiered share, approximately 10 % of the space is provisioned on the local tier and 90 % of the space is provisioned in the cloud.</span></span> <span data-ttu-id="d017a-113">Örneğin, 1 TB paylaşımı sağlanan, 100 GB yerel alanında bulunması ve 900 GB bulutta kullanılabilir zaman veri katmanları.</span><span class="sxs-lookup"><span data-stu-id="d017a-113">For example, if you provisioned a 1 TB share, 100 GB would reside in the local space and 900 GB would be used in the cloud when the data tiers.</span></span> <span data-ttu-id="d017a-114">Bu, sırayla cihazda yerel alana çalıştırırsanız, (% 10 yerel katmanda gereken kullanılamaz çünkü), bir katmanlı paylaşımı sağlayamazsınız olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="d017a-114">This in turn implies that if you run out of all the local space on the device, you cannot provision a tiered share (because the 10 % required on the local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="d017a-115">Sağlanan kapasite</span><span class="sxs-lookup"><span data-stu-id="d017a-115">Provisioned capacity</span></span>

<span data-ttu-id="d017a-116">Her bir paylaşım türü için maksimum sağlanan kapasite için aşağıdaki tabloya bakın.</span><span class="sxs-lookup"><span data-stu-id="d017a-116">Refer to the following table for maximum provisioned capacity for each share type.</span></span>

| <span data-ttu-id="d017a-117">**Sınır tanımlayıcısı**</span><span class="sxs-lookup"><span data-stu-id="d017a-117">**Limit identifier**</span></span> | <span data-ttu-id="d017a-118">**Sınırı**</span><span class="sxs-lookup"><span data-stu-id="d017a-118">**Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="d017a-119">Katmanlı bir paylaşımı en küçük boyut</span><span class="sxs-lookup"><span data-stu-id="d017a-119">Minimum size of a tiered share</span></span> |<span data-ttu-id="d017a-120">500 GB</span><span class="sxs-lookup"><span data-stu-id="d017a-120">500 GB</span></span> |
| <span data-ttu-id="d017a-121">Katmanlı bir paylaşımı en büyük boyutu</span><span class="sxs-lookup"><span data-stu-id="d017a-121">Maximum size of a tiered share</span></span> |<span data-ttu-id="d017a-122">20 TB</span><span class="sxs-lookup"><span data-stu-id="d017a-122">20 TB</span></span> |
| <span data-ttu-id="d017a-123">Yerel olarak sabitlenmiş bir paylaşımı en küçük boyut</span><span class="sxs-lookup"><span data-stu-id="d017a-123">Minimum size of a locally pinned share</span></span> |<span data-ttu-id="d017a-124">50 GB</span><span class="sxs-lookup"><span data-stu-id="d017a-124">50 GB</span></span> |
| <span data-ttu-id="d017a-125">Yerel olarak sabitlenmiş bir paylaşımı en büyük boyutu</span><span class="sxs-lookup"><span data-stu-id="d017a-125">Maximum size of a locally pinned share</span></span> |<span data-ttu-id="d017a-126">2 TB</span><span class="sxs-lookup"><span data-stu-id="d017a-126">2 TB</span></span> |

## <a name="the-shares-blade"></a><span data-ttu-id="d017a-127">Paylaşımlar dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="d017a-127">The Shares blade</span></span>

<span data-ttu-id="d017a-128">**Paylaşımları** StorSimple hizmeti Özet dikey menüsünde belirli bir StorSimple dizi depolama paylaşımları listesini görüntüler ve bunları yönetmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d017a-128">The **Shares** menu on your StorSimple service summary blade displays the list of storage shares on a given StorSimple array and allows you to manage them.</span></span>

![Paylaşımlar dikey penceresi](./media/storsimple-virtual-array-manage-shares/shares-blade.png)

<span data-ttu-id="d017a-130">Bir paylaşım öznitelikleri bir dizi oluşur:</span><span class="sxs-lookup"><span data-stu-id="d017a-130">A share consists of a series of attributes:</span></span>

* <span data-ttu-id="d017a-131">**Paylaşım adı** – benzersiz olmalı ve Paylaşım tanımlamanıza yardımcı olan açıklayıcı bir ad.</span><span class="sxs-lookup"><span data-stu-id="d017a-131">**Share Name** – A descriptive name that must be unique and helps identify the share.</span></span>
* <span data-ttu-id="d017a-132">**Durum** – çevrimiçi veya çevrimdışı olabilir.</span><span class="sxs-lookup"><span data-stu-id="d017a-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="d017a-133">Bir paylaşım çevrimdışıysa, paylaşımın kullanıcılar buna erişebilir olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="d017a-133">If a share is offline, users of the share will not be able to access it.</span></span>
* <span data-ttu-id="d017a-134">**Tür** – paylaşım olup olmadığını belirten **katmanlı** (varsayılan) veya **yerel olarak sabitlenmiş**.</span><span class="sxs-lookup"><span data-stu-id="d017a-134">**Type** – Indicates whether the share is **Tiered** (the default) or **Locally pinned**.</span></span>
* <span data-ttu-id="d017a-135">**Kapasite** – toplam paylaşımında depolanan veri miktarını karşılaştırıldığında kullanılan veri miktarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="d017a-135">**Capacity** – specifies the amount of data used as compared to the total amount of data that can be stored on the share.</span></span>
* <span data-ttu-id="d017a-136">**Açıklama** – paylaşım açıklamak yardımcı olan isteğe bağlı bir ayar.</span><span class="sxs-lookup"><span data-stu-id="d017a-136">**Description** – An optional setting that helps describe the share.</span></span>
* <span data-ttu-id="d017a-137">**İzinleri** -Windows Explorer ile yönetilebilir paylaşımı için NTFS izinleri.</span><span class="sxs-lookup"><span data-stu-id="d017a-137">**Permissions** - The NTFS permissions to the share that can be managed through Windows Explorer.</span></span>
* <span data-ttu-id="d017a-138">**Yedekleme** – StorSimple sanal dizisi tüm paylaşımlar yedekleme için otomatik olarak etkinleştirilmiş durumda.</span><span class="sxs-lookup"><span data-stu-id="d017a-138">**Backup** – In case of the StorSimple Virtual Array, all shares are automatically enabled for backup.</span></span>

![Paylaşımlar ayrıntıları](./media/storsimple-virtual-array-manage-shares/share-details.png)

<span data-ttu-id="d017a-140">Aşağıdaki görevleri gerçekleştirmek için Bu öğreticide yönergeleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="d017a-140">Use the instructions in this tutorial to perform the following tasks:</span></span>

* <span data-ttu-id="d017a-141">Paylaşım Ekle</span><span class="sxs-lookup"><span data-stu-id="d017a-141">Add a share</span></span>
* <span data-ttu-id="d017a-142">Bir paylaşımı değiştirme</span><span class="sxs-lookup"><span data-stu-id="d017a-142">Modify a share</span></span>
* <span data-ttu-id="d017a-143">Bir paylaşım çevrimdışı duruma getirin</span><span class="sxs-lookup"><span data-stu-id="d017a-143">Take a share offline</span></span>
* <span data-ttu-id="d017a-144">Bir paylaşımı silme</span><span class="sxs-lookup"><span data-stu-id="d017a-144">Delete a share</span></span>

## <a name="add-a-share"></a><span data-ttu-id="d017a-145">Paylaşım Ekle</span><span class="sxs-lookup"><span data-stu-id="d017a-145">Add a share</span></span>

1. <span data-ttu-id="d017a-146">StorSimple hizmeti Özet dikey penceresinden tıklayın **+ Ekle paylaşımı** komut çubuğundan.</span><span class="sxs-lookup"><span data-stu-id="d017a-146">From the StorSimple service summary blade, click **+ Add share** from the command bar.</span></span> <span data-ttu-id="d017a-147">Bu açılır **Ekle paylaşımı** dikey.</span><span class="sxs-lookup"><span data-stu-id="d017a-147">This opens up the **Add share** blade.</span></span>

    ![Paylaşım Ekle](./media/storsimple-virtual-array-manage-shares/add-share.png)

2. <span data-ttu-id="d017a-149">İçinde **Ekle paylaşımı** dikey penceresinde aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="d017a-149">In the **Add share** blade, do the following:</span></span>
   
    1. <span data-ttu-id="d017a-150">İçinde **paylaşım adı** alanında, paylaşımınıza için benzersiz bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="d017a-150">In the **Share name** field, enter a unique name for your share.</span></span> <span data-ttu-id="d017a-151">Adı 3 ile 127 karakter içeren bir dize olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d017a-151">The name must be a string that contains 3 to 127 characters.</span></span>

    2. <span data-ttu-id="d017a-152">İsteğe bağlı bir **açıklama** paylaşımı için.</span><span class="sxs-lookup"><span data-stu-id="d017a-152">An optional **Description** for the share.</span></span> <span data-ttu-id="d017a-153">Açıklama, paylaşım sahiplerini tanımlamaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d017a-153">The description will help identify the share owners.</span></span>

    3. <span data-ttu-id="d017a-154">İçinde **türü** açılır listesinde, oluşturulup oluşturulmayacağını belirtin bir **katmanlı** veya **yerel olarak sabitlenmiş** paylaşın.</span><span class="sxs-lookup"><span data-stu-id="d017a-154">In the **Type** dropdown list, specify whether to create a **Tiered** or **Locally pinned** share.</span></span> <span data-ttu-id="d017a-155">Yerel GARANTİLERİN, düşük gecikme ve yüksek performansın gerektiği iş yükleri için seçin **Paylaşımı'yerel olarak sabitlenmiş**.</span><span class="sxs-lookup"><span data-stu-id="d017a-155">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned share**.</span></span> <span data-ttu-id="d017a-156">Diğer tüm veriler için seçin **katmanlı** paylaşın.</span><span class="sxs-lookup"><span data-stu-id="d017a-156">For all other data, select **Tiered** share.</span></span>

    4. <span data-ttu-id="d017a-157">İçinde **kapasite** alanında, paylaşımı boyutunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="d017a-157">In the **Capacity** field, specify the size of the share.</span></span> <span data-ttu-id="d017a-158">Katmanlı bir paylaşımı, 500 GB ile 20 TB arasında olmalıdır ve yerel olarak sabitlenmiş bir paylaşımı, 50 GB ile 2 TB arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d017a-158">A tiered share must be between 500 GB and 20 TB and a locally pinned share must be between 50 GB and 2 TB.</span></span>

    5. <span data-ttu-id="d017a-159">İçinde **kümesine varsayılan tam izinleri** alanında, kullanıcı ya da bu paylaşıma erişim grubu için izinleri atayın.</span><span class="sxs-lookup"><span data-stu-id="d017a-159">In the **Set default full permissions to** field, assign the permissions to the user, or the group that is accessing this share.</span></span> <span data-ttu-id="d017a-160">Kullanıcı veya kullanıcı grubunun adını belirtin  _john@contoso.com_  biçimi.</span><span class="sxs-lookup"><span data-stu-id="d017a-160">Specify the name of the user or the user group in _john@contoso.com_ format.</span></span> <span data-ttu-id="d017a-161">Bu paylaşımlar erişmek yönetici ayrıcalıkları izin vermek için bir kullanıcı grubu (yerine tek bir kullanıcı) kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="d017a-161">We recommend that you use a user group (instead of a single user) to allow admin privileges to access these shares.</span></span> <span data-ttu-id="d017a-162">İzinlerini burada atadıktan sonra bu izinleri değiştirmek için dosya Gezgini'ni kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d017a-162">After you have assigned the permissions here, you can then use File Explorer to modify these permissions.</span></span>
3. <span data-ttu-id="d017a-163">Paylaşımınıza yapılandırma tamamladığınızda tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="d017a-163">When you've finished configuring your share, click **Create**.</span></span> <span data-ttu-id="d017a-164">Belirtilen ayarlarla bir paylaşımı oluşturulur ve bir bildirim görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d017a-164">A share will be created with the specified settings and you will see a notification.</span></span> <span data-ttu-id="d017a-165">Varsayılan olarak, yedekleme paylaşım için etkin.</span><span class="sxs-lookup"><span data-stu-id="d017a-165">By default, backup will be enabled for the share.</span></span>
4. <span data-ttu-id="d017a-166">Paylaşım başarıyla oluşturulduğunu doğrulamak için şu adrese gidin **paylaşımları** dikey.</span><span class="sxs-lookup"><span data-stu-id="d017a-166">To confirm that the share was successfully created, go to the **Shares** blade.</span></span> <span data-ttu-id="d017a-167">Listelenen paylaşımına görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d017a-167">You should see the share listed.</span></span>
   
    ![Paylaşımı oluşturma başarılı](./media/storsimple-virtual-array-manage-shares/share-success.png)

## <a name="modify-a-share"></a><span data-ttu-id="d017a-169">Bir paylaşımı değiştirme</span><span class="sxs-lookup"><span data-stu-id="d017a-169">Modify a share</span></span>

<span data-ttu-id="d017a-170">Paylaşımın açıklaması değiştirmeniz gerektiğinde bir paylaşımı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d017a-170">Modify a share when you need to change the description of the share.</span></span> <span data-ttu-id="d017a-171">Paylaşımı oluşturulduktan sonra başka bir paylaşım özellikleri değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="d017a-171">No other share properties can be modified once the share is created.</span></span>

#### <a name="to-modify-a-share"></a><span data-ttu-id="d017a-172">Bir paylaşım değiştirmek için</span><span class="sxs-lookup"><span data-stu-id="d017a-172">To modify a share</span></span>

1. <span data-ttu-id="d017a-173">Gelen **paylaşımları** değiştirmenizi istiyor paylaşımın bulunduğu sanal dizinin StorSimple hizmeti Özet dikey ayarı seçin.</span><span class="sxs-lookup"><span data-stu-id="d017a-173">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish you to modify resides.</span></span>
2. <span data-ttu-id="d017a-174">**Seçin** geçerli açıklamasını görüntülemek ve değiştirmek için paylaşımı.</span><span class="sxs-lookup"><span data-stu-id="d017a-174">**Select** the share to view the current description and modify it.</span></span>
3. <span data-ttu-id="d017a-175">Tıklayarak yaptığınız değişiklikleri kaydetmek **kaydetmek** komut çubuğu.</span><span class="sxs-lookup"><span data-stu-id="d017a-175">Save your changes by clicking the **Save** command bar.</span></span> <span data-ttu-id="d017a-176">Belirtilen ayarlarınızı uygulanır ve bir bildirim görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d017a-176">Your specified settings will be applied and you will see a notification.</span></span>
   
    ![ <span data-ttu-id="d017a-177">Paylaşım Düzenle</span><span class="sxs-lookup"><span data-stu-id="d017a-177">Edit share</span></span>](./media/storsimple-virtual-array-manage-shares/share-edit.png)

## <a name="take-a-share-offline"></a><span data-ttu-id="d017a-178">Bir paylaşım çevrimdışı duruma getirin</span><span class="sxs-lookup"><span data-stu-id="d017a-178">Take a share offline</span></span>

<span data-ttu-id="d017a-179">Değiştirmek veya silmek planlama yaparken bir paylaşımı çevrimdışına gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="d017a-179">You may need to take a share offline when you are planning to modify it or delete it.</span></span> <span data-ttu-id="d017a-180">Bir paylaşım çevrimdışı olduğunda okuma-yazma erişimi için kullanılabilir değildir.</span><span class="sxs-lookup"><span data-stu-id="d017a-180">When a share is offline, it is not available for read-write access.</span></span> <span data-ttu-id="d017a-181">Cihaz yanı sıra konak paylaşımı çevrimdışı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d017a-181">You will need to take the share offline on the host as well as on the device.</span></span>

#### <a name="to-take-a-share-offline"></a><span data-ttu-id="d017a-182">Bir paylaşım çevrimdışına almak için</span><span class="sxs-lookup"><span data-stu-id="d017a-182">To take a share offline</span></span>

1. <span data-ttu-id="d017a-183">Söz konusu paylaşımı çevrimdışı duruma getirmeden önce kullanımda olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="d017a-183">Make sure that the share in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="d017a-184">Paylaşım, aşağıdaki adımları gerçekleştirerek dizi çevrimdışı gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d017a-184">Take the share on the array offline by performing the following steps:</span></span>
   
    1. <span data-ttu-id="d017a-185">Gelen **paylaşımları** StorSimple hizmeti Özet dikey ayarı, çevrimdışı duruma getirmenizi istiyor paylaşımın bulunduğu sanal dizinin seçin.</span><span class="sxs-lookup"><span data-stu-id="d017a-185">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish you to take offline resides.</span></span>

    2. <span data-ttu-id="d017a-186">**Seçin** tıklatın ve Paylaşım **...**  (Alternatif olarak bu satırı sağ) ve bağlam menüsünden seçin **çevrimdışına**.</span><span class="sxs-lookup"><span data-stu-id="d017a-186">**Select** the share and Click **...** (alternately right-click in this row) and from the context menu, select **Take offline**.</span></span>
     
        ![Çevrimdışı paylaşımı](./media/storsimple-virtual-array-manage-shares/shares-offline.png)

    3. <span data-ttu-id="d017a-188">Bilgileri gözden **çevrimdışına** dikey ve işlemin onaylamış olursunuz.</span><span class="sxs-lookup"><span data-stu-id="d017a-188">Review the information in the **Take offline** blade and confirm your acceptance of the operation.</span></span> <span data-ttu-id="d017a-189">Tıklatın **çevrimdışına** paylaşım çevrimdışı duruma getirmek için.</span><span class="sxs-lookup"><span data-stu-id="d017a-189">Click **Take offline** to take the share offline.</span></span> <span data-ttu-id="d017a-190">İşlem devam ettiğinden, bir bildirim görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d017a-190">You will see a notification of the operation in progress.</span></span>

    4. <span data-ttu-id="d017a-191">Paylaşım başarıyla çevrimdışı duruma olduğunu doğrulamak için Git **paylaşımları** dikey.</span><span class="sxs-lookup"><span data-stu-id="d017a-191">To confirm that the share was successfully taken offline, go to the **Shares** blade.</span></span> <span data-ttu-id="d017a-192">Paylaşım durumu çevrimdışı olarak görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d017a-192">You should see the status of the share as offline.</span></span>

## <a name="delete-a-share"></a><span data-ttu-id="d017a-193">Bir paylaşımı silme</span><span class="sxs-lookup"><span data-stu-id="d017a-193">Delete a share</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d017a-194">Yalnızca çevrimdışı ise, bir paylaşım silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d017a-194">You can delete a share only if it is offline.</span></span>


<span data-ttu-id="d017a-195">Bir paylaşımı silmek için aşağıdaki adımları tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="d017a-195">Complete the following steps to delete a share.</span></span>

#### <a name="to-delete-a-share"></a><span data-ttu-id="d017a-196">Bir paylaşımı silmek için</span><span class="sxs-lookup"><span data-stu-id="d017a-196">To delete a share</span></span>

1. <span data-ttu-id="d017a-197">Gelen **paylaşımları** StorSimple hizmeti Özet dikey ayarı, silmek istediğiniz paylaşımı bulunduğu sanal dizinin seçin.</span><span class="sxs-lookup"><span data-stu-id="d017a-197">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish to delete resides.</span></span>
2. <span data-ttu-id="d017a-198">**Seçin** tıklatın ve Paylaşım **...**  (Alternatif olarak bu satırı sağ) ve bağlam menüsünden seçin **silmek**.</span><span class="sxs-lookup"><span data-stu-id="d017a-198">**Select** the share and Click **...** (alternately right-click in this row) and from the context menu, select **Delete**.</span></span>
   
    ![Paylaşımı silin](./media/storsimple-virtual-array-manage-shares/share-delete.png)
3. <span data-ttu-id="d017a-200">Silmek istediğiniz paylaşımı durumunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="d017a-200">Check the status of the share you want to delete.</span></span> <span data-ttu-id="d017a-201">Silmek istediğiniz paylaşımı çevrimdışı durumda değilse, onu önce çevrimdışına.</span><span class="sxs-lookup"><span data-stu-id="d017a-201">If the share you want to delete is not offline, take it offline first.</span></span> <span data-ttu-id="d017a-202">Adımları [bir paylaşımı çevrimdışına](#take-a-share-offline).</span><span class="sxs-lookup"><span data-stu-id="d017a-202">Follow the steps in [Take a share offline](#take-a-share-offline).</span></span>
4. <span data-ttu-id="d017a-203">İçinde onaylamanız istendiğinde **silmek** dikey penceresinde, onay kabul etmek ve tıklatın **silmek**.</span><span class="sxs-lookup"><span data-stu-id="d017a-203">When prompted for confirmation in the **Delete** blade, accept the confirmation and click **Delete**.</span></span> <span data-ttu-id="d017a-204">Paylaşım şimdi silinecek ve **paylaşımları** dikey paylaşımları Sanal dizi güncelleştirilmiş listesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="d017a-204">The share will now be deleted and the **Shares** blade shows the updated list of shares within the virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d017a-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d017a-205">Next steps</span></span>
<span data-ttu-id="d017a-206">Bilgi edinmek için nasıl [bir StorSimple paylaşımı kopyalama](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="d017a-206">Learn how to [clone a StorSimple share](storsimple-virtual-array-clone.md).</span></span>

