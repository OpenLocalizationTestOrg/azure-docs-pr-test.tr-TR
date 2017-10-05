---
title: "StorSimple sanal dizinin aygıt Özet dikey | Microsoft Docs"
description: "Cihaz Özet dikey StorSimple Aygıt Yöneticisi'ni açıklar ve StorSimple sanal dizinizi sağlığını izlemek için kullanımı açıklanmaktadır."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: a13c1ea7-6428-4234-84a6-0ebf51670a85
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: manuaery
ms.openlocfilehash: 35413d597c3b6b1c7600241a78572b63f982d175
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-device-summary-blade-for-storsimple-device-manager-connected-to-storsimple-virtual-array"></a><span data-ttu-id="786e7-103">StorSimple sanal dizisine kullan cihaz Özet dikey için StorSimple Aygıt Yöneticisi'ni bağlı</span><span class="sxs-lookup"><span data-stu-id="786e7-103">Use the device summary blade for StorSimple Device Manager connected to StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="786e7-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="786e7-104">Overview</span></span>

<span data-ttu-id="786e7-105">StorSimple Aygıt Yöneticisi'ni aygıt dikey penceresinde, sistem yöneticisinin dikkat etmeniz gereken bu cihaz sorunları vurgulayan bir StorSimple sanal bir verilen StorSimple cihaz Yöneticisi ile kayıtlı dizi Özet görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="786e7-105">The StorSimple Device Manager device blade provides a summary view of a StorSimple Virtual Array that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="786e7-106">Bu öğretici aygıt Özet dikey tanıtır, içerik ve işlevi açıklanmaktadır ve bu dikey pencereden gerçekleştirebileceğiniz görevleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="786e7-106">This tutorial introduces the device summary blade, explains the content and function, and describes the tasks that you can perform from this blade.</span></span>

<span data-ttu-id="786e7-107">Cihaz Özet dikey penceresinde aşağıdaki bilgileri görüntüler:</span><span class="sxs-lookup"><span data-stu-id="786e7-107">The device summary blade displays the following information:</span></span>

![Cihaz Pano](./media/storsimple-virtual-array-device-summary/device-blade.png)



## <a name="management"></a><span data-ttu-id="786e7-109">Yönetim</span><span class="sxs-lookup"><span data-stu-id="786e7-109">Management</span></span>

<span data-ttu-id="786e7-110">StorSimple cihaz dikey penceresinde, StorSimple Cihazınızı yönetmek için seçenekler bakın.</span><span class="sxs-lookup"><span data-stu-id="786e7-110">In the StorSimple device blade, you see the options for managing your StorSimple device.</span></span> <span data-ttu-id="786e7-111">Dikey ve sol tarafındaki üstte yönetimi komutları bakın.</span><span class="sxs-lookup"><span data-stu-id="786e7-111">You see the management commands across the top of the blade and on the left side.</span></span> <span data-ttu-id="786e7-112">Paylaşımlar veya birimler, ekleme veya güncelleştirme ya da sanal dizinizi başarısız için bu seçenekleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="786e7-112">Use these options to add shares or volumes, or update or fail over your virtual array.</span></span>

<span data-ttu-id="786e7-113">Essentials alanı durumu, model, yazılım sürümü yanı sıra bir bağlantı gibi önemli özelliklerinden bazıları yakalar **Web kullanıcı arabirimini** dizi.</span><span class="sxs-lookup"><span data-stu-id="786e7-113">The essentials area captures some of the important properties such as, the status, model, software version as well as a link to the **Web UI** of the array.</span></span> <span data-ttu-id="786e7-114">Bir iç ağda olup olmadıklarını, doğrudan başlatabilirsiniz [yerel web kullanıcı Arabirimi](storsimple-ova-web-ui-admin.md) sanal dizinizi yönetmek için.</span><span class="sxs-lookup"><span data-stu-id="786e7-114">If you are on an internal network, you can directly launch the [local web UI](storsimple-ova-web-ui-admin.md) to administer your virtual array.</span></span>

![Cihaz temelleri](./media/storsimple-virtual-array-device-summary/device-essentials.png)

## <a name="storsimple-device-summary"></a><span data-ttu-id="786e7-116">StorSimple cihazı özeti</span><span class="sxs-lookup"><span data-stu-id="786e7-116">StorSimple device summary</span></span>

* <span data-ttu-id="786e7-117">**Uyarıları** kutucuğu uyarı önem derecesine göre gruplandırılmış dizinizi sanal için tüm etkin uyarıları görüntüsünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="786e7-117">The **Alerts** tile provides a snapshot of all the active alerts for your virtual array, grouped by alert severity.</span></span> <span data-ttu-id="786e7-118">Açmak için kutucuğa tıklayın **uyarıları** dikey ve ardından herhangi dahil olmak üzere, bu uyarı hakkında ek ayrıntıları görüntülemek için bir bireysel uyarı önerilen eylemler.</span><span class="sxs-lookup"><span data-stu-id="786e7-118">Click the tile to open the **Alerts** blade and then click an individual alert to view additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="786e7-119">Sorunu çözerseniz uyarı işaretini kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="786e7-119">You can also clear the alert if the issue has been resolved.</span></span>

* <span data-ttu-id="786e7-120">**Kapasite** kutucuğu toplam depolama alanı kullanılabilir göre sanal cihaz için aynı üzerinden sağlanan ve kalan birincil depolama görüntüler.</span><span class="sxs-lookup"><span data-stu-id="786e7-120">The **Capacity** tile displays the primary storage that is provisioned and remaining across the virtual device relative to the total storage available for the same.</span></span> <span data-ttu-id="786e7-121">**Sağlanan** hazır ve kullanım için ayrılan depolama alanı miktarını başvurduğu **kalan** bu aygıt arasında sağlanabilir kalan kapasite başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="786e7-121">**Provisioned** refers to the amount of storage that is prepared and allocated for use, **Remaining** refers to the remaining capacity that can be provisioned across this device.</span></span> <span data-ttu-id="786e7-122">**Kalan katmanlı** kapasitesi ise bulut dahil olmak üzere sağlanabilir kullanılabilir kapasite sırada **kalan yerel** olduğundan bu sanal dizinin bağlı diskler kalan kapasitesi.</span><span class="sxs-lookup"><span data-stu-id="786e7-122">The **Remaining Tiered** capacity is the available capacity that can be provisioned including cloud, while the **Remaining Local** is the capacity remaining on the disks attached to this virtual array.</span></span>

* <span data-ttu-id="786e7-123">İçinde **kullanım** grafik, son 7 gün içindeki, varsayılan süre tüketilen bulut depolama yanı sıra sanal dizinizi kullanılan birincil depolama görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="786e7-123">In the **Usage** chart, you can view the primary storage used across your virtual array, as well as the cloud storage consumed  over the past 7 days, the default time period.</span></span> <span data-ttu-id="786e7-124">Kullanım **Düzenle** farklı zaman ölçeği seçmek için sağ üst köşedeki grafik seçeneği.</span><span class="sxs-lookup"><span data-stu-id="786e7-124">Use the **Edit** option in the top-right corner of the chart to choose a different time scale.</span></span>

* <span data-ttu-id="786e7-125">**Paylaşımları** veya **birimleri** kutucuğu paylaşımları veya duruma göre gruplanmış Cihazınızı birimlerin sayısı özetini sağlar.</span><span class="sxs-lookup"><span data-stu-id="786e7-125">The **Shares** or **Volumes** tile provides a summary of the number of shares or volumes in your device grouped by status.</span></span> <span data-ttu-id="786e7-126">Açmak için kutucuğa tıklayın **paylaşımları** veya **birimleri** listesinde dikey ve bir tek paylaşım veya onun özelliklerini görüntülemek veya değiştirmek için birimi'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="786e7-126">Click the tile to open the **Shares**  or **Volumes** list blade, and then click on an individual share or volume to view or modify its properties.</span></span> <span data-ttu-id="786e7-127">Daha fazla bilgi için bkz: nasıl yapılır [paylaşımlarını yönetmek](storsimple-virtual-array-manage-shares.md) veya [birimleri yönetme](storsimple-virtual-array-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="786e7-127">For more information, see how to [manage shares](storsimple-virtual-array-manage-shares.md) or [manage volumes](storsimple-virtual-array-manage-volumes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="786e7-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="786e7-128">Next steps</span></span>
<span data-ttu-id="786e7-129">Şunları nasıl yapacağınızı öğrenin:</span><span class="sxs-lookup"><span data-stu-id="786e7-129">Learn how to:</span></span>
- [<span data-ttu-id="786e7-130">Bir StorSimple sanal dizisinde paylaşımlarını yönetmek</span><span class="sxs-lookup"><span data-stu-id="786e7-130">Manage shares on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-shares.md)
    
- [<span data-ttu-id="786e7-131">Bir StorSimple sanal dizisinde birimleri yönetme</span><span class="sxs-lookup"><span data-stu-id="786e7-131">Manage volumes on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-volumes.md)

