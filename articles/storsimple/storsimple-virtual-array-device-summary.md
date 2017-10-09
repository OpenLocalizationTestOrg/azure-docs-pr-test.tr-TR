---
title: "aaaStorSimple sanal dizinin aygıt Özet dikey | Microsoft Docs"
description: "StorSimple cihaz yöneticisinin Hello aygıt Özet dikey tanımlar ve açıklar nasıl toouse, StorSimple sanal dizinizi toomonitor hello durumunu."
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
ms.openlocfilehash: 3649eaac8a924a772f310a809ddf9706e912157a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-summary-blade-for-storsimple-device-manager-connected-toostorsimple-virtual-array"></a><span data-ttu-id="64315-103">Kullanım hello aygıt Özet dikey için StorSimple Aygıt Yöneticisi'ni tooStorSimple sanal dizinin bağlı</span><span class="sxs-lookup"><span data-stu-id="64315-103">Use hello device summary blade for StorSimple Device Manager connected tooStorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="64315-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="64315-104">Overview</span></span>

<span data-ttu-id="64315-105">Merhaba StorSimple Aygıt Yöneticisi'ni aygıt dikey, sistem yöneticisinin dikkat etmeniz gereken bu cihaz sorunları vurgulayan bir StorSimple sanal bir verilen StorSimple cihaz Yöneticisi ile kayıtlı dizi Özet görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="64315-105">hello StorSimple Device Manager device blade provides a summary view of a StorSimple Virtual Array that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="64315-106">Bu öğretici hello aygıt Özet dikey tanıtır, hello içerik ve işlevi açıklanmaktadır ve bu dikey pencereden gerçekleştirebileceğiniz hello görevleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="64315-106">This tutorial introduces hello device summary blade, explains hello content and function, and describes hello tasks that you can perform from this blade.</span></span>

<span data-ttu-id="64315-107">Merhaba aygıt Özet dikey penceresinde aşağıdaki bilgilerle hello görüntüler:</span><span class="sxs-lookup"><span data-stu-id="64315-107">hello device summary blade displays hello following information:</span></span>

![Cihaz Pano](./media/storsimple-virtual-array-device-summary/device-blade.png)



## <a name="management"></a><span data-ttu-id="64315-109">Yönetim</span><span class="sxs-lookup"><span data-stu-id="64315-109">Management</span></span>

<span data-ttu-id="64315-110">Merhaba StorSimple cihaz dikey penceresinde hello seçenekleri StorSimple Cihazınızı yönetmek için bkz.</span><span class="sxs-lookup"><span data-stu-id="64315-110">In hello StorSimple device blade, you see hello options for managing your StorSimple device.</span></span> <span data-ttu-id="64315-111">Merhaba üstte hello dikey ve hello sol tarafında hello yönetimi komutları bakın.</span><span class="sxs-lookup"><span data-stu-id="64315-111">You see hello management commands across hello top of hello blade and on hello left side.</span></span> <span data-ttu-id="64315-112">Bu seçenekler tooadd paylaşımları veya birimler kullanmak, güncelleştirmek veya sanal dizinizi başarısız.</span><span class="sxs-lookup"><span data-stu-id="64315-112">Use these options tooadd shares or volumes, or update or fail over your virtual array.</span></span>

<span data-ttu-id="64315-113">Merhaba essentials alanı gibi hello önemli özellikleri, hello durumu, model, yazılım sürümü yanı sıra bağlantı toohello bazıları yakalar **Web kullanıcı arabirimini** hello dizisi.</span><span class="sxs-lookup"><span data-stu-id="64315-113">hello essentials area captures some of hello important properties such as, hello status, model, software version as well as a link toohello **Web UI** of hello array.</span></span> <span data-ttu-id="64315-114">Bir iç ağda olup olmadıklarını hello doğrudan başlatabilirsiniz [yerel web kullanıcı Arabirimi](storsimple-ova-web-ui-admin.md) tooadminister sanal dizinizi.</span><span class="sxs-lookup"><span data-stu-id="64315-114">If you are on an internal network, you can directly launch hello [local web UI](storsimple-ova-web-ui-admin.md) tooadminister your virtual array.</span></span>

![Cihaz temelleri](./media/storsimple-virtual-array-device-summary/device-essentials.png)

## <a name="storsimple-device-summary"></a><span data-ttu-id="64315-116">StorSimple cihazı özeti</span><span class="sxs-lookup"><span data-stu-id="64315-116">StorSimple device summary</span></span>

* <span data-ttu-id="64315-117">Merhaba **uyarıları** kutucuğu uyarı önem derecesine göre gruplandırılmış dizinizi sanal için bir anlık görüntüsünü tüm hello etkin uyarıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="64315-117">hello **Alerts** tile provides a snapshot of all hello active alerts for your virtual array, grouped by alert severity.</span></span> <span data-ttu-id="64315-118">Merhaba döşeme tooopen hello tıklatın **uyarıları** dikey ve ardından tek bir uyarı tooview ek herhangi dahil olmak üzere Bu uyarıyla ilgili ayrıntılar önerilen eylemler.</span><span class="sxs-lookup"><span data-stu-id="64315-118">Click hello tile tooopen hello **Alerts** blade and then click an individual alert tooview additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="64315-119">Merhaba sorunu çözerseniz hello uyarı işaretini kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64315-119">You can also clear hello alert if hello issue has been resolved.</span></span>

* <span data-ttu-id="64315-120">Merhaba **kapasite** sağlanmış döşeme görüntüler hello birincil depolama ve hello sanal aygıt göreli toohello toplam depolama alanı için kullanılabilir arasında kalan hello aynı.</span><span class="sxs-lookup"><span data-stu-id="64315-120">hello **Capacity** tile displays hello primary storage that is provisioned and remaining across hello virtual device relative toohello total storage available for hello same.</span></span> <span data-ttu-id="64315-121">**Sağlanan** toohello hazırlanmış ve kullanım için ayrılan depolama alanı miktarını başvuruyor **kalan** bu cihaz sağlanan kapasite kalan toohello başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="64315-121">**Provisioned** refers toohello amount of storage that is prepared and allocated for use, **Remaining** refers toohello remaining capacity that can be provisioned across this device.</span></span> <span data-ttu-id="64315-122">Merhaba **kalan katmanlı** kapasitesi ise hello sırasında bulut dahil olmak üzere sağlanabilir hello kullanılabilir kapasite **kalan yerel** hello disklerde kalan hello kapasitesi eklenmiş sanal toothis dizi.</span><span class="sxs-lookup"><span data-stu-id="64315-122">hello **Remaining Tiered** capacity is hello available capacity that can be provisioned including cloud, while hello **Remaining Local** is hello capacity remaining on hello disks attached toothis virtual array.</span></span>

* <span data-ttu-id="64315-123">Merhaba, **kullanım** grafiği, sanal dizinin yanı sıra arasında hello son 7 gün, hello varsayılan süre tüketilen hello bulut depolama kullanılan birincil depolama hello görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64315-123">In hello **Usage** chart, you can view hello primary storage used across your virtual array, as well as hello cloud storage consumed  over hello past 7 days, hello default time period.</span></span> <span data-ttu-id="64315-124">Kullanım hello **Düzenle** farklı zaman ölçeği hello sağ üst köşesinde hello grafik toochoose seçeneği.</span><span class="sxs-lookup"><span data-stu-id="64315-124">Use hello **Edit** option in hello top-right corner of hello chart toochoose a different time scale.</span></span>

* <span data-ttu-id="64315-125">Merhaba **paylaşımları** veya **birimleri** kutucuğu hello sayısı paylaşımları veya birimler duruma göre gruplanmış aygıtınızdaki özetini sağlar.</span><span class="sxs-lookup"><span data-stu-id="64315-125">hello **Shares** or **Volumes** tile provides a summary of hello number of shares or volumes in your device grouped by status.</span></span> <span data-ttu-id="64315-126">Merhaba döşeme tooopen hello tıklatın **paylaşımları** veya **birimleri** listesi dikey penceresinde üzerinde tek tek bir paylaşımı veya birimi tooview'ı tıklatın veya özelliklerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="64315-126">Click hello tile tooopen hello **Shares**  or **Volumes** list blade, and then click on an individual share or volume tooview or modify its properties.</span></span> <span data-ttu-id="64315-127">Daha fazla bilgi için bkz. nasıl çok[paylaşımlarını yönetmek](storsimple-virtual-array-manage-shares.md) veya [birimleri yönetme](storsimple-virtual-array-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="64315-127">For more information, see how too[manage shares](storsimple-virtual-array-manage-shares.md) or [manage volumes](storsimple-virtual-array-manage-volumes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="64315-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="64315-128">Next steps</span></span>
<span data-ttu-id="64315-129">Şunları nasıl yapacağınızı öğrenin:</span><span class="sxs-lookup"><span data-stu-id="64315-129">Learn how to:</span></span>
- [<span data-ttu-id="64315-130">Bir StorSimple sanal dizisinde paylaşımlarını yönetmek</span><span class="sxs-lookup"><span data-stu-id="64315-130">Manage shares on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-shares.md)
    
- [<span data-ttu-id="64315-131">Bir StorSimple sanal dizisinde birimleri yönetme</span><span class="sxs-lookup"><span data-stu-id="64315-131">Manage volumes on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-volumes.md)

