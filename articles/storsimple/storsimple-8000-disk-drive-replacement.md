---
title: "Bir disk sürücüsü bir StorSimple 8000 serisi cihazda Değiştir | Microsoft Docs"
description: "StorSimple birincil muhafaza veya EBOD muhafazası disk sürücüsünde Değiştir açıklanmaktadır."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 073/2017
ms.author: alkohli
ms.openlocfilehash: bb259b626ecd4dcbaa8f1c465f1ece4516aa8881
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-8000-series-device"></a><span data-ttu-id="98e16-103">StorSimple 8000 serisi Cihazınızı disk sürücüsünde değiştirin</span><span class="sxs-lookup"><span data-stu-id="98e16-103">Replace a disk drive on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="98e16-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="98e16-104">Overview</span></span>
<span data-ttu-id="98e16-105">Bu öğretici nasıl kaldırın ve bir hatalı çalışan veya başarısız sabit disk sürücüsünde bir Microsoft Azure StorSimple cihaz Değiştir açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="98e16-105">This tutorial explains how you can remove and replace a malfunctioning or failed hard disk drive on a Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="98e16-106">Bir disk sürücüsü değiştirmek için aktarmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="98e16-106">To replace a disk drive, you need to:</span></span>

* <span data-ttu-id="98e16-107">Antitamper kilit disengage</span><span class="sxs-lookup"><span data-stu-id="98e16-107">Disengage the antitamper lock</span></span>
* <span data-ttu-id="98e16-108">Disk sürücüsünü Kaldır</span><span class="sxs-lookup"><span data-stu-id="98e16-108">Remove the disk drive</span></span>
* <span data-ttu-id="98e16-109">Değiştirme disk sürücüsü yükleyin</span><span class="sxs-lookup"><span data-stu-id="98e16-109">Install the replacement disk drive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98e16-110">Bir disk sürücüsü değiştirme ve kaldırma gözden önce güvenlik bilgileri [StorSimple donanım bileşeni değiştirme](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="98e16-110">Before removing and replacing a disk drive, review the safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>
 

## <a name="disengage-the-antitamper-lock"></a><span data-ttu-id="98e16-111">Antitamper kilit disengage</span><span class="sxs-lookup"><span data-stu-id="98e16-111">Disengage the antitamper lock</span></span>
<span data-ttu-id="98e16-112">Bu yordam, nasıl, StorSimple Cihazınızda antitamper kilitler disk sürücülerini değiştirdiğinizde boşta veya açıklar.</span><span class="sxs-lookup"><span data-stu-id="98e16-112">This procedure explains how the antitamper locks on your StorSimple device can be engaged or disengaged when you replace the disk drives.</span></span> <span data-ttu-id="98e16-113">Antitamper kilitler sürücü taşıyıcı tanıtıcılarını donatılmıştır ve küçük açıklığı tanıtıcının Mandal bölümdeki aracılığıyla erişilir.</span><span class="sxs-lookup"><span data-stu-id="98e16-113">The antitamper locks are fitted in the drive carrier handles, and they are accessed through a small aperture in the latch section of the handle.</span></span> <span data-ttu-id="98e16-114">Sürücüleri kilitli konumu ayarlayın kilitleri ile sağlanır.</span><span class="sxs-lookup"><span data-stu-id="98e16-114">Drives are supplied with the locks set to the locked position.</span></span>

#### <a name="to-unlock-the-antitamper-lock"></a><span data-ttu-id="98e16-115">Antitamper kilitleme kilidini açmak için</span><span class="sxs-lookup"><span data-stu-id="98e16-115">To unlock the antitamper lock</span></span>
1. <span data-ttu-id="98e16-116">Dikkatle tanıtıcı açıklığı ve onun yuva lock tuşunun (Microsoft sağlanan bir "tamperproof" T10 tornavida) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="98e16-116">Carefully insert the lock key (a "tamperproof" T10 screwdriver that Microsoft provided) into the aperture in the handle and into its socket.</span></span> 
   
   <span data-ttu-id="98e16-117">Antitamper kilidi etkinleştirilmişse, kırmızı gösterge açıklığı görünür olur.</span><span class="sxs-lookup"><span data-stu-id="98e16-117">If the antitamper lock is activated, the red indicator is visible in the aperture.</span></span>
  
    ![Kilitli disk sürücüsü](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    <span data-ttu-id="98e16-119">**Şekil 1** koruma yetkisiz değiştirmeye karşı kilit gerçekleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="98e16-119">**Figure 1** Anti-tamper lock engaged</span></span>
   
   | <span data-ttu-id="98e16-120">Etiket</span><span class="sxs-lookup"><span data-stu-id="98e16-120">Label</span></span> | <span data-ttu-id="98e16-121">Açıklama</span><span class="sxs-lookup"><span data-stu-id="98e16-121">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="98e16-122">1</span><span class="sxs-lookup"><span data-stu-id="98e16-122">1</span></span> |<span data-ttu-id="98e16-123">Gösterge açıklığı</span><span class="sxs-lookup"><span data-stu-id="98e16-123">Indicator aperture</span></span> |
   | <span data-ttu-id="98e16-124">2</span><span class="sxs-lookup"><span data-stu-id="98e16-124">2</span></span> |<span data-ttu-id="98e16-125">Antitamper Kilitle</span><span class="sxs-lookup"><span data-stu-id="98e16-125">Antitamper lock</span></span> |
2. <span data-ttu-id="98e16-126">Kırmızı gösterge açıklığı anahtarı yukarıda görünür değil kadar anticlockwise yönü anahtarında döndürün.</span><span class="sxs-lookup"><span data-stu-id="98e16-126">Rotate the key in an anticlockwise direction until the red indicator is not visible in the aperture above the key.</span></span>
3. <span data-ttu-id="98e16-127">Anahtarı kaldırın.</span><span class="sxs-lookup"><span data-stu-id="98e16-127">Remove the key.</span></span>
   
    ![Kilidi açılmış disk sürücüsü](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    <span data-ttu-id="98e16-129">**Şekil 2** kilitli değil disk sürücüsü</span><span class="sxs-lookup"><span data-stu-id="98e16-129">**Figure 2** Unlocked disk drive</span></span>
4. <span data-ttu-id="98e16-130">Disk sürücüsü artık kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="98e16-130">The disk drive can now be removed.</span></span>

<span data-ttu-id="98e16-131">Kilidi bulunmaya ters'ndaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="98e16-131">Follow the steps in reverse to engage the lock.</span></span>

## <a name="remove-the-disk-drive"></a><span data-ttu-id="98e16-132">Disk sürücüsünü Kaldır</span><span class="sxs-lookup"><span data-stu-id="98e16-132">Remove the disk drive</span></span>
<span data-ttu-id="98e16-133">StorSimple Cihazınızı bir RAID 10 benzeri depolama alanları yapılandırmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="98e16-133">Your StorSimple device supports a RAID 10-like storage spaces configuration.</span></span> <span data-ttu-id="98e16-134">Bu, başarısız olan bir diski, katı hal sürücüsü (SSD) normal olarak çalışabilir veya sabit disk sürücüsü (HDD) anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="98e16-134">This implies that it can operate normally with one failed disk, solid-state drive (SSD), or hard disk drive (HDD).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="98e16-135">Sisteminizde birden fazla başarısız disk varsa, birden fazla SSD veya HDD herhangi bir noktada sisteminden zamanında kaldırmayın.</span><span class="sxs-lookup"><span data-stu-id="98e16-135">If your system has more than one failed disk, do not remove more than one SSD or HDD from the system at any point in time.</span></span> <span data-ttu-id="98e16-136">Bunun yapılması, veri kaybına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="98e16-136">Doing so could result in loss of data.</span></span>
> * <span data-ttu-id="98e16-137">Daha önce bir SSD bulunan bir yuvada SSD yerine koyun emin olun.</span><span class="sxs-lookup"><span data-stu-id="98e16-137">Make sure that you place a replacement SSD in a slot that previously contained an SSD.</span></span> <span data-ttu-id="98e16-138">Benzer şekilde, daha önce bir HDD bulunan bir yuvada değiştirme HDD yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="98e16-138">Similarly, place a replacement HDD in a slot that previously contained an HDD.</span></span>
> * <span data-ttu-id="98e16-139">Azure portalında yuva 0'dan – numaralandırılır 11.</span><span class="sxs-lookup"><span data-stu-id="98e16-139">In the Azure portal, slots are numbered from 0 – 11.</span></span> <span data-ttu-id="98e16-140">Portal bir disk 2 yuvadaki, cihazda başarısız olduğunu gösterirse bu nedenle, üçüncü yuvasındaki başarısız disk sol üstten arayın.</span><span class="sxs-lookup"><span data-stu-id="98e16-140">Therefore, if the portal shows that a disk in slot 2 has failed, on the device, look for the failed disk in the third slot from the top left.</span></span>
> 
> 

<span data-ttu-id="98e16-141">Sürücüleri kaldırılır ve işletim sistemi sırasında değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="98e16-141">Drives can be removed and replaced while the system is operating.</span></span>

#### <a name="to-remove-a-drive"></a><span data-ttu-id="98e16-142">Bir sürücüyü kaldırmak için</span><span class="sxs-lookup"><span data-stu-id="98e16-142">To remove a drive</span></span>
1. <span data-ttu-id="98e16-143">Azure portalında başarısız diski tanımlamak için aygıtınıza Git **ayarlar > donanım durumu**.</span><span class="sxs-lookup"><span data-stu-id="98e16-143">To identify the failed disk, in the Azure portal, go to your device **Settings > Hardware health**.</span></span> <span data-ttu-id="98e16-144">Bir disk birincil muhafazada ve/veya bir EBOD muhafazası (8600 model kullanıyorsanız) içinde başarısız olabileceğinden altında disklerin durumunu bakmak **paylaşılan bileşenleri** ve altında **EBOD paylaşılan bileşenleri**.</span><span class="sxs-lookup"><span data-stu-id="98e16-144">Because a disk can fail in the primary enclosure and/or in an EBOD enclosure (if you are using a 8600 model), look at the status of the disks under **Shared components** and under **EBOD shared components**.</span></span> <span data-ttu-id="98e16-145">Başarısız disk ya da muhafazada kırmızı bir duruma sahip gösterilir.</span><span class="sxs-lookup"><span data-stu-id="98e16-145">A failed disk in either enclosure will be shown with a red status.</span></span>
2. <span data-ttu-id="98e16-146">Birincil muhafaza veya EBOD muhafazası önündeki sürücüleri bulun.</span><span class="sxs-lookup"><span data-stu-id="98e16-146">Locate the drives in the front of the primary enclosure or the EBOD enclosure.</span></span> 
3. <span data-ttu-id="98e16-147">Kilidi diskse, sonraki adıma geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98e16-147">If the disk is unlocked, proceed to the next step.</span></span> <span data-ttu-id="98e16-148">Disk kilitliyse, aşağıdaki yordamı kullanarak kilidini [antitamper kilit Disengage](#disengage-the-antitamper-lock).</span><span class="sxs-lookup"><span data-stu-id="98e16-148">If the disk is locked, unlock it by following the procedure in [Disengage the antitamper lock](#disengage-the-antitamper-lock).</span></span>
4. <span data-ttu-id="98e16-149">Sürücü taşıyıcı modülünü siyah Mandal basın ve sürücü taşıyıcı tanıtıcı çekerek out ve kasa Önden çıkartın.</span><span class="sxs-lookup"><span data-stu-id="98e16-149">Press the black latch on the drive carrier module and pull the drive carrier handle out and away from the front of the chassis.</span></span>
   
    ![Disk sürücüsü işleyici bırakılıyor](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    <span data-ttu-id="98e16-151">**Şekil 3** sürücüsü işleyici bırakılıyor</span><span class="sxs-lookup"><span data-stu-id="98e16-151">**Figure 3** Releasing the drive handle</span></span>
5. <span data-ttu-id="98e16-152">Sürücü taşıyıcı tanıtıcı tam olarak genişletildiğinde gövdeden sürücü taşıyıcı kaydırın.</span><span class="sxs-lookup"><span data-stu-id="98e16-152">When the drive carrier handle is fully extended, slide the drive carrier out of the chassis.</span></span> 
   
    ![Disk sürücüsünden kayan disk](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    <span data-ttu-id="98e16-154">**Şekil 4** taşıyıcı dışında disk sürücüsü kayan</span><span class="sxs-lookup"><span data-stu-id="98e16-154">**Figure 4** Sliding the disk drive out of the carrier</span></span>

## <a name="install-the-replacement-disk-drive"></a><span data-ttu-id="98e16-155">Değiştirme disk sürücüsü yükleyin</span><span class="sxs-lookup"><span data-stu-id="98e16-155">Install the replacement disk drive</span></span>
<span data-ttu-id="98e16-156">Bir sürücü StorSimple Cihazınızı başarısız oldu ve kaldırıldı sonra yeni bir sürücüyle değiştirmek için bu yordamı izleyin.</span><span class="sxs-lookup"><span data-stu-id="98e16-156">After a drive has failed in your StorSimple device and you have removed it, follow this procedure to replace it with a new drive.</span></span>

#### <a name="to-insert-a-drive"></a><span data-ttu-id="98e16-157">Bir sürücü eklemek için</span><span class="sxs-lookup"><span data-stu-id="98e16-157">To insert a drive</span></span>
1. <span data-ttu-id="98e16-158">Sürücü taşıyıcı tanıtıcı tam olarak genişletilmiş, aşağıdaki görüntüde gösterildiği gibi emin olun.</span><span class="sxs-lookup"><span data-stu-id="98e16-158">Ensure the drive carrier handle is fully extended, as shown in the following image.</span></span>
   
    ![İşleyicisi genişletilmiş disk sürücüsü](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    <span data-ttu-id="98e16-160">**Şekil 5** işleyicisi genişletilmiş sürücü</span><span class="sxs-lookup"><span data-stu-id="98e16-160">**Figure 5** Drive with handle extended</span></span>
2. <span data-ttu-id="98e16-161">Sürücü taşıyıcı tüm kasaya kaydırın.</span><span class="sxs-lookup"><span data-stu-id="98e16-161">Slide the drive carrier all the way into the chassis.</span></span>
   
    ![Disk sürücüsü taşıyıcı kayan diskine](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    <span data-ttu-id="98e16-163">**Şekil 6** sürücü taşıyıcı kaydırarak gövdeye yerleştirme</span><span class="sxs-lookup"><span data-stu-id="98e16-163">**Figure 6**  Sliding the drive carrier into the chassis</span></span>
3. <span data-ttu-id="98e16-164">Sürücü taşıyıcı eklenen sürücü taşıyıcı tanıtıcı kilitli bir konumda tutturur kadar sürücü taşıyıcı kasaya göndermek devam ederken sürücü taşıyıcı tanıtıcı kapatın.</span><span class="sxs-lookup"><span data-stu-id="98e16-164">With the drive carrier inserted, close the drive carrier handle while continuing to push the drive carrier into the chassis, until the drive carrier handle snaps into a locked position.</span></span>
4. <span data-ttu-id="98e16-165">Taşıyıcı tanıtıcı güvenli hale getirmek için Microsoft tarafından (tamperproof Torx tornavida) sağlanan lock tuşunun kilit Vidayı Çeyrek Aç yönünde kapatarak yerine kullanın.</span><span class="sxs-lookup"><span data-stu-id="98e16-165">Use the lock key that was provided by Microsoft (tamperproof Torx screwdriver) to secure the carrier handle into place by turning the lock screw a quarter turn clockwise.</span></span>
5. <span data-ttu-id="98e16-166">Değiştirme başarılı olduğunu ve sürücünün çalışır durumda olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="98e16-166">Verify that the replacement was successful and the drive is operational.</span></span> <span data-ttu-id="98e16-167">Azure portalına erişmek ve gidin **ayarları** > **donanım durumu**.</span><span class="sxs-lookup"><span data-stu-id="98e16-167">Access the Azure portal and navigate to **Settings** > **Hardware health**.</span></span> <span data-ttu-id="98e16-168">Altında **paylaşılan bileşenleri** veya **EBOD paylaşılan bileşenleri**, sürücü durumu sağlıklı olduğunu gösteren yeşil olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="98e16-168">Under **Shared components** or **EBOD shared components**, the drive status should be green, indicating that it is healthy.</span></span>
<!---Loc Comment: It seems it should say "Device settings > Hardware health" instead of "Settings > Hardware health"---->
   
   > [!NOTE]
   > <span data-ttu-id="98e16-169">Disk durumunun değiştirme işleminden yeşile birkaç saat sürebilir.</span><span class="sxs-lookup"><span data-stu-id="98e16-169">It may take several hours for the disk status to turn green after the replacement.</span></span>
  
## <a name="next-steps"></a><span data-ttu-id="98e16-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="98e16-170">Next steps</span></span>
<span data-ttu-id="98e16-171">Daha fazla bilgi edinmek [StorSimple donanım bileşeni değiştirme](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="98e16-171">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

