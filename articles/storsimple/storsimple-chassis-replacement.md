---
title: "StorSimple 8000 serisi aygıtta aaaReplace kasa | Microsoft Docs"
description: "StorSimple birincil muhafaza veya EBOD muhafazası için kasa tooremove ve Değiştir nasıl hello açıklar."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 537659ed-4c46-49c1-b1e4-186262f2542d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: f8576d63520a6f7d3267180d2a68d4fc38fd48fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-chassis-on-your-storsimple-device"></a><span data-ttu-id="23eeb-103">StorSimple Cihazınızda Hello kasa değiştirin</span><span class="sxs-lookup"><span data-stu-id="23eeb-103">Replace hello chassis on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="23eeb-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="23eeb-104">Overview</span></span>
<span data-ttu-id="23eeb-105">Bu öğretici açıklar nasıl tooremove ve StorSimple 8000 serisi aygıtta bir kasa değiştirin.</span><span class="sxs-lookup"><span data-stu-id="23eeb-105">This tutorial explains how tooremove and replace a chassis in a StorSimple 8000 series device.</span></span> <span data-ttu-id="23eeb-106">Merhaba 8600 çift muhafaza aygıt (iki kasa) iken hello StorSimple 8100 model bir tek kasası (bir kasa), aygıttır.</span><span class="sxs-lookup"><span data-stu-id="23eeb-106">hello StorSimple 8100 model is a single enclosure device (one chassis), whereas hello 8600 is a dual enclosure device (two chassis).</span></span> <span data-ttu-id="23eeb-107">8600 model için büyük olasılıkla hello aygıtı başarısız iki kasa vardır: Merhaba hello birincil kasası için Kasa ya da hello EBOD muhafazası hello Kasa.</span><span class="sxs-lookup"><span data-stu-id="23eeb-107">For an 8600 model, there are potentially two chassis that could fail in hello device: hello chassis for hello primary enclosure or hello chassis for hello EBOD enclosure.</span></span>

<span data-ttu-id="23eeb-108">Her iki durumda da, Microsoft tarafından sevk hello değiştirme kasa boştur.</span><span class="sxs-lookup"><span data-stu-id="23eeb-108">In either case, hello replacement chassis that is shipped by Microsoft is empty.</span></span> <span data-ttu-id="23eeb-109">Hiçbir güç ve soğutma modülleri (PCMs) denetleyicisi modülleri, katı hal disk sürücüleri (SSD), sabit disk sürücülerinin (HDD'ler) ya da EBOD modülleri dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="23eeb-109">No Power and Cooling Modules (PCMs), controller modules, solid state disk drives (SSDs), hard disk drives (HDDs), or EBOD modules will be included.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="23eeb-110">Merhaba kasa, değiştirme ve kaldırma gözden önce hello güvenlik bilgileri [StorSimple donanım bileşeni değiştirme](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="23eeb-110">Before removing and replacing hello chassis, review hello safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-hello-chassis"></a><span data-ttu-id="23eeb-111">Merhaba kasa Kaldır</span><span class="sxs-lookup"><span data-stu-id="23eeb-111">Remove hello chassis</span></span>
<span data-ttu-id="23eeb-112">StorSimple Cihazınızda adımları tooremove hello kasa aşağıdaki hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="23eeb-112">Perform hello following steps tooremove hello chassis on your StorSimple device.</span></span>

#### <a name="tooremove-a-chassis"></a><span data-ttu-id="23eeb-113">tooremove bir kasa</span><span class="sxs-lookup"><span data-stu-id="23eeb-113">tooremove a chassis</span></span>
1. <span data-ttu-id="23eeb-114">Merhaba StorSimple cihaz kapatılır ve tüm hello güç kaynaklardan bağlantısı kesilmiş emin olun.</span><span class="sxs-lookup"><span data-stu-id="23eeb-114">Make sure that hello StorSimple device is shut down and disconnected from all hello power sources.</span></span>
2. <span data-ttu-id="23eeb-115">Tüm hello ağ ve SAS kabloları varsa kaldırın.</span><span class="sxs-lookup"><span data-stu-id="23eeb-115">Remove all hello network and SAS cables, if applicable.</span></span>
3. <span data-ttu-id="23eeb-116">Merhaba birimi hello raf kaldırın.</span><span class="sxs-lookup"><span data-stu-id="23eeb-116">Remove hello unit from hello rack.</span></span>
4. <span data-ttu-id="23eeb-117">Her hello sürücüleri kaldırın ve hello yuvaları, bunlar kaldırılır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="23eeb-117">Remove each of hello drives and note hello slots from which they are removed.</span></span> <span data-ttu-id="23eeb-118">Daha fazla bilgi için bkz: [kaldırmak hello disk sürücüsü](storsimple-disk-drive-replacement.md#remove-the-disk-drive).</span><span class="sxs-lookup"><span data-stu-id="23eeb-118">For more information, see [Remove hello disk drive](storsimple-disk-drive-replacement.md#remove-the-disk-drive).</span></span>
5. <span data-ttu-id="23eeb-119">Hello (Bu başarısız hello kasa ise) EBOD muhafazası, hello EBOD denetleyicisi modülleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="23eeb-119">On hello EBOD enclosure (if this is hello chassis that failed), remove hello EBOD controller modules.</span></span> <span data-ttu-id="23eeb-120">Daha fazla bilgi için bkz: [EBOD denetleyicisi kaldırmak](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller).</span><span class="sxs-lookup"><span data-stu-id="23eeb-120">For more information, see [Remove an EBOD controller](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller).</span></span> 
   
    <span data-ttu-id="23eeb-121">Hello (Bu başarısız hello kasa ise) birincil muhafaza hello denetleyicilerini kaldırın ve hello yuvaları, bunlar kaldırılır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="23eeb-121">On hello primary enclosure (if this is hello chassis that failed), remove hello controllers and note hello slots from which they are removed.</span></span> <span data-ttu-id="23eeb-122">Daha fazla bilgi için bkz: [bir denetleyici kaldırmak](storsimple-controller-replacement.md#remove-a-controller).</span><span class="sxs-lookup"><span data-stu-id="23eeb-122">For more information, see [Remove a controller](storsimple-controller-replacement.md#remove-a-controller).</span></span>

## <a name="install-hello-chassis"></a><span data-ttu-id="23eeb-123">Merhaba kasa yükleyin</span><span class="sxs-lookup"><span data-stu-id="23eeb-123">Install hello chassis</span></span>
<span data-ttu-id="23eeb-124">StorSimple Cihazınızda adımları tooinstall hello kasa aşağıdaki hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="23eeb-124">Perform hello following steps tooinstall hello chassis on your StorSimple device.</span></span>

#### <a name="tooinstall-a-chassis"></a><span data-ttu-id="23eeb-125">tooinstall bir kasa</span><span class="sxs-lookup"><span data-stu-id="23eeb-125">tooinstall a chassis</span></span>
1. <span data-ttu-id="23eeb-126">Merhaba kasa hello dolapta bağlayın.</span><span class="sxs-lookup"><span data-stu-id="23eeb-126">Mount hello chassis in hello rack.</span></span> <span data-ttu-id="23eeb-127">Daha fazla bilgi için bkz: [rafa monte StorSimple 8100 aygıt](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) veya [rafa monte StorSimple 8600 aygıt](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="23eeb-127">For more information, see [Rack-mount your StorSimple 8100 device](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) or [Rack-mount your StorSimple 8600 device](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span></span>
2. <span data-ttu-id="23eeb-128">Merhaba kasa hello rafa monte sonra hello denetleyicisi modülleri aynı daha önce de yüklendikleri konumlandırır hello yükleyin.</span><span class="sxs-lookup"><span data-stu-id="23eeb-128">After hello chassis is mounted in hello rack, install hello controller modules in hello same positions that they were previously installed in.</span></span>
3. <span data-ttu-id="23eeb-129">Yükleme Merhaba, daha önce de yüklendikleri aynı yerleştirir ve yuvası hello sürücüleri.</span><span class="sxs-lookup"><span data-stu-id="23eeb-129">Install hello drives in hello same positions and slots that they were previously installed in.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="23eeb-130">Merhaba SSD hello yuvalarında yüklemeniz ve ardından hello HDD yükleyin öneririz.</span><span class="sxs-lookup"><span data-stu-id="23eeb-130">We recommend that you install hello SSDs in hello slots first, and then install hello HDDs.</span></span>
   > 
   > 
4. <span data-ttu-id="23eeb-131">Merhaba ile cihaz hello rafa monte ve hello bileşenlerinin yüklü olması, aygıt toohello uygun güç kaynaklarınız bağlanmak ve hello aygıtı açın.</span><span class="sxs-lookup"><span data-stu-id="23eeb-131">With hello device mounted in hello rack and hello components installed, connect your device toohello appropriate power sources, and turn on hello device.</span></span> <span data-ttu-id="23eeb-132">Ayrıntılar için bkz [StorSimple 8100 cihazınız kablo](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) veya [StorSimple 8600 model Cihazınızı kablo](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="23eeb-132">For details, see [Cable your StorSimple 8100 device](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) or [Cable your StorSimple 8600 device](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span></span>

## <a name="next-steps"></a><span data-ttu-id="23eeb-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="23eeb-133">Next steps</span></span>
<span data-ttu-id="23eeb-134">Daha fazla bilgi edinmek [StorSimple donanım bileşeni değiştirme](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="23eeb-134">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

