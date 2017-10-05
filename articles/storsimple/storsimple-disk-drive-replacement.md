---
title: "StorSimple cihazı disk sürücüsünde Değiştir | Microsoft Docs"
description: "StorSimple birincil muhafaza veya EBOD muhafazası disk sürücüsünde Değiştir açıklanmaktadır."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 98890d36-b613-40fd-994e-330dd907a8a1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 0659ab9d304dbfcce72e8c3c79edad68e70b9630
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-device"></a><span data-ttu-id="027b3-103">StorSimple Cihazınızı disk sürücüsünde değiştirin</span><span class="sxs-lookup"><span data-stu-id="027b3-103">Replace a disk drive on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="027b3-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="027b3-104">Overview</span></span>
<span data-ttu-id="027b3-105">Bu öğretici nasıl kaldırın ve bir hatalı çalışan veya başarısız sabit disk sürücüsünde bir Microsoft Azure StorSimple cihaz Değiştir açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="027b3-105">This tutorial explains how you can remove and replace a malfunctioning or failed hard disk drive on a Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="027b3-106">Bir disk sürücüsü değiştirmek için aktarmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="027b3-106">To replace a disk drive, you need to:</span></span>

* <span data-ttu-id="027b3-107">Antitamper kilit disengage</span><span class="sxs-lookup"><span data-stu-id="027b3-107">Disengage the antitamper lock</span></span>
* <span data-ttu-id="027b3-108">Disk sürücüsünü Kaldır</span><span class="sxs-lookup"><span data-stu-id="027b3-108">Remove the disk drive</span></span>
* <span data-ttu-id="027b3-109">Değiştirme disk sürücüsü yükleyin</span><span class="sxs-lookup"><span data-stu-id="027b3-109">Install the replacement disk drive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="027b3-110">Bir disk sürücüsü değiştirme ve kaldırma gözden önce güvenlik bilgileri [StorSimple donanım bileşeni değiştirme](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="027b3-110">Before removing and replacing a disk drive, review the safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="disengage-the-antitamper-lock"></a><span data-ttu-id="027b3-111">Antitamper kilit disengage</span><span class="sxs-lookup"><span data-stu-id="027b3-111">Disengage the antitamper lock</span></span>
<span data-ttu-id="027b3-112">Bu yordam, nasıl, StorSimple Cihazınızda antitamper kilitler disk sürücülerini değiştirdiğinizde boşta veya açıklar.</span><span class="sxs-lookup"><span data-stu-id="027b3-112">This procedure explains how the antitamper locks on your StorSimple device can be engaged or disengaged when you replace the disk drives.</span></span> <span data-ttu-id="027b3-113">Antitamper kilitler sürücü taşıyıcı tanıtıcılarını donatılmıştır ve küçük açıklığı tanıtıcının Mandal bölümdeki aracılığıyla erişilir.</span><span class="sxs-lookup"><span data-stu-id="027b3-113">The antitamper locks are fitted in the drive carrier handles, and they are accessed through a small aperture in the latch section of the handle.</span></span> <span data-ttu-id="027b3-114">Sürücüleri kilitli konumu ayarlayın kilitleri ile sağlanır.</span><span class="sxs-lookup"><span data-stu-id="027b3-114">Drives are supplied with the locks set to the locked position.</span></span>

#### <a name="to-unlock-the-antitamper-lock"></a><span data-ttu-id="027b3-115">Antitamper kilitleme kilidini açmak için</span><span class="sxs-lookup"><span data-stu-id="027b3-115">To unlock the antitamper lock</span></span>
1. <span data-ttu-id="027b3-116">Dikkatle tanıtıcı açıklığı ve onun yuva lock tuşunun (Microsoft sağlanan bir "tamperproof" T10 tornavida) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="027b3-116">Carefully insert the lock key (a "tamperproof" T10 screwdriver that Microsoft provided) into the aperture in the handle and into its socket.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="027b3-117">Antitamper kilidi etkinleştirilmişse, kırmızı gösterge açıklığı görünür olur.</span><span class="sxs-lookup"><span data-stu-id="027b3-117">If the antitamper lock is activated, the red indicator is visible in the aperture.</span></span>
   > 
   > 
   
    ![Kilitli disk sürücüsü](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    <span data-ttu-id="027b3-119">**Şekil 1** koruma yetkisiz değiştirmeye karşı kilit gerçekleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="027b3-119">**Figure 1** Anti-tamper lock engaged</span></span>
   
   | <span data-ttu-id="027b3-120">Etiket</span><span class="sxs-lookup"><span data-stu-id="027b3-120">Label</span></span> | <span data-ttu-id="027b3-121">Açıklama</span><span class="sxs-lookup"><span data-stu-id="027b3-121">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="027b3-122">1</span><span class="sxs-lookup"><span data-stu-id="027b3-122">1</span></span> |<span data-ttu-id="027b3-123">Gösterge açıklığı</span><span class="sxs-lookup"><span data-stu-id="027b3-123">Indicator aperture</span></span> |
   | <span data-ttu-id="027b3-124">2</span><span class="sxs-lookup"><span data-stu-id="027b3-124">2</span></span> |<span data-ttu-id="027b3-125">Antitamper Kilitle</span><span class="sxs-lookup"><span data-stu-id="027b3-125">Antitamper lock</span></span> |
2. <span data-ttu-id="027b3-126">Kırmızı gösterge açıklığı anahtarı yukarıda görünür değil kadar anticlockwise yönü anahtarında döndürün.</span><span class="sxs-lookup"><span data-stu-id="027b3-126">Rotate the key in an anticlockwise direction until the red indicator is not visible in the aperture above the key.</span></span>
3. <span data-ttu-id="027b3-127">Anahtarı kaldırın.</span><span class="sxs-lookup"><span data-stu-id="027b3-127">Remove the key.</span></span>
   
    ![Kilidi açılmış disk sürücüsü](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    <span data-ttu-id="027b3-129">**Şekil 2** kilitli değil disk sürücüsü</span><span class="sxs-lookup"><span data-stu-id="027b3-129">**Figure 2** Unlocked disk drive</span></span>
4. <span data-ttu-id="027b3-130">Disk sürücüsü artık kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="027b3-130">The disk drive can now be removed.</span></span>

<span data-ttu-id="027b3-131">Kilidi bulunmaya ters'ndaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="027b3-131">Follow the steps in reverse to engage the lock.</span></span>

## <a name="remove-the-disk-drive"></a><span data-ttu-id="027b3-132">Disk sürücüsünü Kaldır</span><span class="sxs-lookup"><span data-stu-id="027b3-132">Remove the disk drive</span></span>
<span data-ttu-id="027b3-133">StorSimple Cihazınızı bir RAID 10 benzeri depolama alanları yapılandırmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="027b3-133">Your StorSimple device supports a RAID 10-like storage spaces configuration.</span></span> <span data-ttu-id="027b3-134">Bu, başarısız olan bir diski, katı hal sürücüsü (SSD) normal olarak çalışabilir veya sabit disk sürücüsü (HDD) anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="027b3-134">This implies that it can operate normally with one failed disk, solid-state drive (SSD), or hard disk drive (HDD).</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="027b3-135">Sisteminizde birden fazla başarısız disk varsa, birden fazla SSD veya HDD herhangi bir noktada sisteminden zamanında kaldırmayın.</span><span class="sxs-lookup"><span data-stu-id="027b3-135">If your system has more than one failed disk, do not remove more than one SSD or HDD from the system at any point in time.</span></span> <span data-ttu-id="027b3-136">Bunun yapılması, veri kaybına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="027b3-136">Doing so could result in loss of data.</span></span>
> * <span data-ttu-id="027b3-137">Daha önce bir SSD bulunan bir yuvada SSD yerine koyun emin olun.</span><span class="sxs-lookup"><span data-stu-id="027b3-137">Make sure that you place a replacement SSD in a slot that previously contained an SSD.</span></span> <span data-ttu-id="027b3-138">Benzer şekilde, daha önce bir HDD bulunan bir yuvada değiştirme HDD yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="027b3-138">Similarly, place a replacement HDD in a slot that previously contained an HDD.</span></span>
> * <span data-ttu-id="027b3-139">Klasik Azure portalında yuva 0'dan – numaralandırılır 11.</span><span class="sxs-lookup"><span data-stu-id="027b3-139">In the Azure classic portal, slots are numbered from 0 – 11.</span></span> <span data-ttu-id="027b3-140">Portal bir disk 2 yuvadaki, cihazda başarısız olduğunu gösterirse bu nedenle, üçüncü yuvasındaki başarısız disk sol üstten arayın.</span><span class="sxs-lookup"><span data-stu-id="027b3-140">Therefore, if the portal shows that a disk in slot 2 has failed, on the device, look for the failed disk in the third slot from the top left.</span></span>
> 
> 

<span data-ttu-id="027b3-141">Sürücüleri kaldırılır ve işletim sistemi sırasında değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="027b3-141">Drives can be removed and replaced while the system is operating.</span></span>

#### <a name="to-remove-a-drive"></a><span data-ttu-id="027b3-142">Bir sürücüyü kaldırmak için</span><span class="sxs-lookup"><span data-stu-id="027b3-142">To remove a drive</span></span>
1. <span data-ttu-id="027b3-143">Azure Klasik portalında başarısız diski tanımlamak için Git **aygıtları** > **Bakım** > **donanım durum**.</span><span class="sxs-lookup"><span data-stu-id="027b3-143">To identify the failed disk, in the Azure classic portal, go to **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="027b3-144">Bir disk birincil muhafazada ve/veya bir EBOD muhafazası (8600 model kullanıyorsanız) içinde başarısız olabileceğinden altında disklerin durumunu bakmak **paylaşılan bileşenleri** ve altında **EBOD muhafazası paylaşılan bileşenleri**.</span><span class="sxs-lookup"><span data-stu-id="027b3-144">Because a disk can fail in the primary enclosure and/or in an EBOD enclosure (if you are using a 8600 model), look at the status of the disks under **Shared Components** and under **EBOD enclosure Shared Components**.</span></span> <span data-ttu-id="027b3-145">Başarısız disk ya da muhafazada kırmızı bir duruma sahip gösterilir.</span><span class="sxs-lookup"><span data-stu-id="027b3-145">A failed disk in either enclosure will be shown with a red status.</span></span>
2. <span data-ttu-id="027b3-146">Birincil muhafaza veya EBOD muhafazası önündeki sürücüleri bulun.</span><span class="sxs-lookup"><span data-stu-id="027b3-146">Locate the drives in the front of the primary enclosure or the EBOD enclosure.</span></span> 
3. <span data-ttu-id="027b3-147">Kilidi diskse, sonraki adıma geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="027b3-147">If the disk is unlocked, proceed to the next step.</span></span> <span data-ttu-id="027b3-148">Disk kilitliyse, aşağıdaki yordamı kullanarak kilidini [antitamper kilit Disengage](#disengage-the-antitamper-lock).</span><span class="sxs-lookup"><span data-stu-id="027b3-148">If the disk is locked, unlock it by following the procedure in [Disengage the antitamper lock](#disengage-the-antitamper-lock).</span></span>
4. <span data-ttu-id="027b3-149">Sürücü taşıyıcı modülünü siyah Mandal basın ve sürücü taşıyıcı tanıtıcı çekerek out ve kasa Önden çıkartın.</span><span class="sxs-lookup"><span data-stu-id="027b3-149">Press the black latch on the drive carrier module and pull the drive carrier handle out and away from the front of the chassis.</span></span> 
   
    ![Disk sürücüsü işleyici bırakılıyor](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    <span data-ttu-id="027b3-151">**Şekil 3** sürücüsü işleyici bırakılıyor</span><span class="sxs-lookup"><span data-stu-id="027b3-151">**Figure 3** Releasing the drive handle</span></span>
5. <span data-ttu-id="027b3-152">Sürücü taşıyıcı tanıtıcı tam olarak genişletildiğinde gövdeden sürücü taşıyıcı kaydırın.</span><span class="sxs-lookup"><span data-stu-id="027b3-152">When the drive carrier handle is fully extended, slide the drive carrier out of the chassis.</span></span> 
   
    ![Disk sürücüsünden kayan disk](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    <span data-ttu-id="027b3-154">**Şekil 4** taşıyıcı dışında disk sürücüsü kayan</span><span class="sxs-lookup"><span data-stu-id="027b3-154">**Figure 4** Sliding the disk drive out of the carrier</span></span>

## <a name="install-the-replacement-disk-drive"></a><span data-ttu-id="027b3-155">Değiştirme disk sürücüsü yükleyin</span><span class="sxs-lookup"><span data-stu-id="027b3-155">Install the replacement disk drive</span></span>
<span data-ttu-id="027b3-156">Bir sürücü StorSimple Cihazınızı başarısız oldu ve kaldırıldı sonra yeni bir sürücüyle değiştirmek için bu yordamı izleyin.</span><span class="sxs-lookup"><span data-stu-id="027b3-156">After a drive has failed in your StorSimple device and you have removed it, follow this procedure to replace it with a new drive.</span></span>

#### <a name="to-insert-a-drive"></a><span data-ttu-id="027b3-157">Bir sürücü eklemek için</span><span class="sxs-lookup"><span data-stu-id="027b3-157">To insert a drive</span></span>
1. <span data-ttu-id="027b3-158">Sürücü taşıyıcı tanıtıcı tam olarak genişletilmiş, aşağıdaki görüntüde gösterildiği gibi emin olun.</span><span class="sxs-lookup"><span data-stu-id="027b3-158">Ensure the drive carrier handle is fully extended, as shown in the following image.</span></span>
   
    ![İşleyicisi genişletilmiş disk sürücüsü](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    <span data-ttu-id="027b3-160">**Şekil 5** işleyicisi genişletilmiş sürücü</span><span class="sxs-lookup"><span data-stu-id="027b3-160">**Figure 5** Drive with handle extended</span></span>
2. <span data-ttu-id="027b3-161">Sürücü taşıyıcı tüm kasaya kaydırın.</span><span class="sxs-lookup"><span data-stu-id="027b3-161">Slide the drive carrier all the way into the chassis.</span></span> 
   
    ![Disk sürücüsü taşıyıcı kayan diskine](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    <span data-ttu-id="027b3-163">**Şekil 6** sürücü taşıyıcı kaydırarak gövdeye yerleştirme</span><span class="sxs-lookup"><span data-stu-id="027b3-163">**Figure 6**  Sliding the drive carrier into the chassis</span></span>
3. <span data-ttu-id="027b3-164">Sürücü taşıyıcı eklenen sürücü taşıyıcı tanıtıcı kilitli bir konumda tutturur kadar sürücü taşıyıcı kasaya göndermek devam ederken sürücü taşıyıcı tanıtıcı kapatın.</span><span class="sxs-lookup"><span data-stu-id="027b3-164">With the drive carrier inserted, close the drive carrier handle while continuing to push the drive carrier into the chassis, until the drive carrier handle snaps into a locked position.</span></span>
4. <span data-ttu-id="027b3-165">Taşıyıcı tanıtıcı güvenli hale getirmek için Microsoft tarafından (tamperproof Torx tornavida) sağlanan lock tuşunun kilit Vidayı Çeyrek Aç yönünde kapatarak yerine kullanın.</span><span class="sxs-lookup"><span data-stu-id="027b3-165">Use the lock key that was provided by Microsoft (tamperproof Torx screwdriver) to secure the carrier handle into place by turning the lock screw a quarter turn clockwise.</span></span>
5. <span data-ttu-id="027b3-166">Değiştirme başarılı oldu ve sürücü, Klasik Azure portalına erişme ve giderek tarafından çalışır durumda olduğunu doğrulayın **Bakım** > **donanım durum**.</span><span class="sxs-lookup"><span data-stu-id="027b3-166">Verify that the replacement was successful and the drive is operational by accessing the Azure classic portal and navigating to **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="027b3-167">Altında **paylaşılan bileşenleri** veya **EBOD muhafazası paylaşılan bileşenleri**, sürücü durumu sağlıklı olduğunu gösteren yeşil olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="027b3-167">Under **Shared Components** or **EBOD enclosure Shared Components**, the drive status should be green, indicating that it is healthy.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="027b3-168">Disk durumunun değiştirme işleminden yeşile birkaç saat sürebilir.</span><span class="sxs-lookup"><span data-stu-id="027b3-168">It may take several hours for the disk status to turn green after the replacement.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="027b3-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="027b3-169">Next steps</span></span>
<span data-ttu-id="027b3-170">Daha fazla bilgi edinmek [StorSimple donanım bileşeni değiştirme](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="027b3-170">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

