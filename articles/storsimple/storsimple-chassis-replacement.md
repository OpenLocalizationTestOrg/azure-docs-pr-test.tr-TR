---
title: "StorSimple 8000 serisi aygıtta kasa Değiştir | Microsoft Docs"
description: "StorSimple birincil muhafaza veya EBOD muhafazası için kasa kaldırdığınızda ve açıklar."
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
ms.openlocfilehash: 5295c5dd039b1d4746ebaaf90372932e4c3e7c26
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="replace-the-chassis-on-your-storsimple-device"></a><span data-ttu-id="8c163-103">Kasa, StorSimple Cihazınızda değiştirin</span><span class="sxs-lookup"><span data-stu-id="8c163-103">Replace the chassis on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="8c163-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="8c163-104">Overview</span></span>
<span data-ttu-id="8c163-105">Bu öğretici, kaldırmak ve StorSimple 8000 serisi aygıtta bir kasa Değiştir açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8c163-105">This tutorial explains how to remove and replace a chassis in a StorSimple 8000 series device.</span></span> <span data-ttu-id="8c163-106">8600 çift muhafaza aygıt (iki kasa) iken StorSimple 8100 model bir tek kasası (bir kasa), aygıttır.</span><span class="sxs-lookup"><span data-stu-id="8c163-106">The StorSimple 8100 model is a single enclosure device (one chassis), whereas the 8600 is a dual enclosure device (two chassis).</span></span> <span data-ttu-id="8c163-107">8600 model için büyük olasılıkla aygıtı başarısız iki kasa vardır: birincil muhafaza veya EBOD muhafazası kasa için Kasa.</span><span class="sxs-lookup"><span data-stu-id="8c163-107">For an 8600 model, there are potentially two chassis that could fail in the device: the chassis for the primary enclosure or the chassis for the EBOD enclosure.</span></span>

<span data-ttu-id="8c163-108">Her iki durumda da, Microsoft tarafından sevk değiştirme kasa boştur.</span><span class="sxs-lookup"><span data-stu-id="8c163-108">In either case, the replacement chassis that is shipped by Microsoft is empty.</span></span> <span data-ttu-id="8c163-109">Hiçbir güç ve soğutma modülleri (PCMs) denetleyicisi modülleri, katı hal disk sürücüleri (SSD), sabit disk sürücülerinin (HDD'ler) ya da EBOD modülleri dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="8c163-109">No Power and Cooling Modules (PCMs), controller modules, solid state disk drives (SSDs), hard disk drives (HDDs), or EBOD modules will be included.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8c163-110">Kasa değiştirme ve kaldırma gözden önce güvenlik bilgileri [StorSimple donanım bileşeni değiştirme](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="8c163-110">Before removing and replacing the chassis, review the safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-the-chassis"></a><span data-ttu-id="8c163-111">Kasa Kaldır</span><span class="sxs-lookup"><span data-stu-id="8c163-111">Remove the chassis</span></span>
<span data-ttu-id="8c163-112">Kasa, StorSimple Cihazınızda kaldırmak için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="8c163-112">Perform the following steps to remove the chassis on your StorSimple device.</span></span>

#### <a name="to-remove-a-chassis"></a><span data-ttu-id="8c163-113">Bir kasa kaldırmak için</span><span class="sxs-lookup"><span data-stu-id="8c163-113">To remove a chassis</span></span>
1. <span data-ttu-id="8c163-114">StorSimple cihazı kapatmak ve güç kaynaklardan gelen bağlantısı kesilmiş emin olun.</span><span class="sxs-lookup"><span data-stu-id="8c163-114">Make sure that the StorSimple device is shut down and disconnected from all the power sources.</span></span>
2. <span data-ttu-id="8c163-115">Tüm ağ ve SAS kabloları varsa kaldırın.</span><span class="sxs-lookup"><span data-stu-id="8c163-115">Remove all the network and SAS cables, if applicable.</span></span>
3. <span data-ttu-id="8c163-116">Birim raf kaldırın.</span><span class="sxs-lookup"><span data-stu-id="8c163-116">Remove the unit from the rack.</span></span>
4. <span data-ttu-id="8c163-117">Her sürücü kaldırın ve, bunlar kaldırılır yuvaları unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8c163-117">Remove each of the drives and note the slots from which they are removed.</span></span> <span data-ttu-id="8c163-118">Daha fazla bilgi için bkz: [disk sürücüsünü Kaldır](storsimple-disk-drive-replacement.md#remove-the-disk-drive).</span><span class="sxs-lookup"><span data-stu-id="8c163-118">For more information, see [Remove the disk drive](storsimple-disk-drive-replacement.md#remove-the-disk-drive).</span></span>
5. <span data-ttu-id="8c163-119">(Bu başarısız kasa ise) EBOD muhafazası üzerinde EBOD denetleyicisi modülleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="8c163-119">On the EBOD enclosure (if this is the chassis that failed), remove the EBOD controller modules.</span></span> <span data-ttu-id="8c163-120">Daha fazla bilgi için bkz: [EBOD denetleyicisi kaldırmak](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller).</span><span class="sxs-lookup"><span data-stu-id="8c163-120">For more information, see [Remove an EBOD controller](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller).</span></span> 
   
    <span data-ttu-id="8c163-121">(Bu başarısız kasa ise) birincil kasada denetleyicilerini kaldırın ve bunlar kaldırılan yuvaları not edin.</span><span class="sxs-lookup"><span data-stu-id="8c163-121">On the primary enclosure (if this is the chassis that failed), remove the controllers and note the slots from which they are removed.</span></span> <span data-ttu-id="8c163-122">Daha fazla bilgi için bkz: [bir denetleyici kaldırmak](storsimple-controller-replacement.md#remove-a-controller).</span><span class="sxs-lookup"><span data-stu-id="8c163-122">For more information, see [Remove a controller](storsimple-controller-replacement.md#remove-a-controller).</span></span>

## <a name="install-the-chassis"></a><span data-ttu-id="8c163-123">Kasa yükleyin</span><span class="sxs-lookup"><span data-stu-id="8c163-123">Install the chassis</span></span>
<span data-ttu-id="8c163-124">StorSimple Cihazınızda kasaya yüklemek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="8c163-124">Perform the following steps to install the chassis on your StorSimple device.</span></span>

#### <a name="to-install-a-chassis"></a><span data-ttu-id="8c163-125">Bir kasaya yüklemek için</span><span class="sxs-lookup"><span data-stu-id="8c163-125">To install a chassis</span></span>
1. <span data-ttu-id="8c163-126">Raf kasaya bağlayın.</span><span class="sxs-lookup"><span data-stu-id="8c163-126">Mount the chassis in the rack.</span></span> <span data-ttu-id="8c163-127">Daha fazla bilgi için bkz: [rafa monte StorSimple 8100 aygıt](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) veya [rafa monte StorSimple 8600 aygıt](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="8c163-127">For more information, see [Rack-mount your StorSimple 8100 device](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) or [Rack-mount your StorSimple 8600 device](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span></span>
2. <span data-ttu-id="8c163-128">Kasa rafa monte sonra bunlar daha önce yüklü aynı konumlarda denetleyicisi modüllerini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8c163-128">After the chassis is mounted in the rack, install the controller modules in the same positions that they were previously installed in.</span></span>
3. <span data-ttu-id="8c163-129">Aynı konum ve bunlar daha önce yüklü yuvaları sürücüleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8c163-129">Install the drives in the same positions and slots that they were previously installed in.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8c163-130">SSD yuvalarında ilk yükleyin ve HDD yükleyin öneririz.</span><span class="sxs-lookup"><span data-stu-id="8c163-130">We recommend that you install the SSDs in the slots first, and then install the HDDs.</span></span>
   > 
   > 
4. <span data-ttu-id="8c163-131">Raf ve yüklenen bileşenlerle aygıtla Cihazınızı bağlamak için uygun güç kaynakları ve aygıtı açın.</span><span class="sxs-lookup"><span data-stu-id="8c163-131">With the device mounted in the rack and the components installed, connect your device to the appropriate power sources, and turn on the device.</span></span> <span data-ttu-id="8c163-132">Ayrıntılar için bkz [StorSimple 8100 cihazınız kablo](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) veya [StorSimple 8600 model Cihazınızı kablo](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="8c163-132">For details, see [Cable your StorSimple 8100 device](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) or [Cable your StorSimple 8600 device](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c163-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8c163-133">Next steps</span></span>
<span data-ttu-id="8c163-134">Daha fazla bilgi edinmek [StorSimple donanım bileşeni değiştirme](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="8c163-134">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

