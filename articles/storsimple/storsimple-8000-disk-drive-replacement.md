---
title: "bir disk sürücüsü bir StorSimple 8000 serisi cihazda aaaReplace | Microsoft Docs"
description: "Nasıl tooreplace bir disk sürücüsü bir StorSimple birincil muhafaza veya EBOD muhafazası açıklanmaktadır."
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
ms.openlocfilehash: 09c1bf5e97adf54a609a868e921351bc63e00a83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-8000-series-device"></a><span data-ttu-id="68cf7-103">StorSimple 8000 serisi Cihazınızı disk sürücüsünde değiştirin</span><span class="sxs-lookup"><span data-stu-id="68cf7-103">Replace a disk drive on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="68cf7-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="68cf7-104">Overview</span></span>
<span data-ttu-id="68cf7-105">Bu öğretici nasıl kaldırın ve bir hatalı çalışan veya başarısız sabit disk sürücüsünde bir Microsoft Azure StorSimple cihaz Değiştir açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="68cf7-105">This tutorial explains how you can remove and replace a malfunctioning or failed hard disk drive on a Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="68cf7-106">tooreplace bir disk sürücüsü, şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="68cf7-106">tooreplace a disk drive, you need to:</span></span>

* <span data-ttu-id="68cf7-107">Merhaba antitamper kilit disengage</span><span class="sxs-lookup"><span data-stu-id="68cf7-107">Disengage hello antitamper lock</span></span>
* <span data-ttu-id="68cf7-108">Merhaba disk sürücüsünü Kaldır</span><span class="sxs-lookup"><span data-stu-id="68cf7-108">Remove hello disk drive</span></span>
* <span data-ttu-id="68cf7-109">Merhaba değiştirme disk sürücüsü yükleyin</span><span class="sxs-lookup"><span data-stu-id="68cf7-109">Install hello replacement disk drive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="68cf7-110">Bir disk sürücüsü değiştirme ve kaldırma gözden önce hello güvenlik bilgileri [StorSimple donanım bileşeni değiştirme](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="68cf7-110">Before removing and replacing a disk drive, review hello safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>
 

## <a name="disengage-hello-antitamper-lock"></a><span data-ttu-id="68cf7-111">Merhaba antitamper kilit disengage</span><span class="sxs-lookup"><span data-stu-id="68cf7-111">Disengage hello antitamper lock</span></span>
<span data-ttu-id="68cf7-112">Bu yordam nasıl hello antitamper kilitleri, StorSimple Cihazınızda hello disk sürücüleri değiştirdiğinizde boşta veya açıklar.</span><span class="sxs-lookup"><span data-stu-id="68cf7-112">This procedure explains how hello antitamper locks on your StorSimple device can be engaged or disengaged when you replace hello disk drives.</span></span> <span data-ttu-id="68cf7-113">Hello antitamper kilitleri hello sürücü taşıyıcı tanıtıcılarını donatılmıştır ve küçük açıklığı hello tanıtıcının hello Mandal bölümdeki aracılığıyla erişilir.</span><span class="sxs-lookup"><span data-stu-id="68cf7-113">hello antitamper locks are fitted in hello drive carrier handles, and they are accessed through a small aperture in hello latch section of hello handle.</span></span> <span data-ttu-id="68cf7-114">Sürücüleri hello kilitleri kümesi kilitli toohello konumu ile sağlanır.</span><span class="sxs-lookup"><span data-stu-id="68cf7-114">Drives are supplied with hello locks set toohello locked position.</span></span>

#### <a name="toounlock-hello-antitamper-lock"></a><span data-ttu-id="68cf7-115">toounlock hello antitamper Kilitle</span><span class="sxs-lookup"><span data-stu-id="68cf7-115">toounlock hello antitamper lock</span></span>
1. <span data-ttu-id="68cf7-116">Dikkatli bir şekilde hello tanıtıcı içinde hello açıklığı ve onun yuva hello lock tuşunun (Microsoft sağlanan bir "tamperproof" T10 tornavida) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="68cf7-116">Carefully insert hello lock key (a "tamperproof" T10 screwdriver that Microsoft provided) into hello aperture in hello handle and into its socket.</span></span> 
   
   <span data-ttu-id="68cf7-117">Merhaba antitamper kilidi etkinleştirilmişse, hello kırmızı göstergesi hello açıklığı görünür olur.</span><span class="sxs-lookup"><span data-stu-id="68cf7-117">If hello antitamper lock is activated, hello red indicator is visible in hello aperture.</span></span>
  
    ![Kilitli disk sürücüsü](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    <span data-ttu-id="68cf7-119">**Şekil 1** koruma yetkisiz değiştirmeye karşı kilit gerçekleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="68cf7-119">**Figure 1** Anti-tamper lock engaged</span></span>
   
   | <span data-ttu-id="68cf7-120">Etiket</span><span class="sxs-lookup"><span data-stu-id="68cf7-120">Label</span></span> | <span data-ttu-id="68cf7-121">Açıklama</span><span class="sxs-lookup"><span data-stu-id="68cf7-121">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="68cf7-122">1</span><span class="sxs-lookup"><span data-stu-id="68cf7-122">1</span></span> |<span data-ttu-id="68cf7-123">Gösterge açıklığı</span><span class="sxs-lookup"><span data-stu-id="68cf7-123">Indicator aperture</span></span> |
   | <span data-ttu-id="68cf7-124">2</span><span class="sxs-lookup"><span data-stu-id="68cf7-124">2</span></span> |<span data-ttu-id="68cf7-125">Antitamper Kilitle</span><span class="sxs-lookup"><span data-stu-id="68cf7-125">Antitamper lock</span></span> |
2. <span data-ttu-id="68cf7-126">Merhaba kırmızı göstergesi hello açıklığı hello anahtarı yukarıda görünür değil kadar hello anahtar anticlockwise yönde döndürün.</span><span class="sxs-lookup"><span data-stu-id="68cf7-126">Rotate hello key in an anticlockwise direction until hello red indicator is not visible in hello aperture above hello key.</span></span>
3. <span data-ttu-id="68cf7-127">Başlangıç anahtarı kaldırın.</span><span class="sxs-lookup"><span data-stu-id="68cf7-127">Remove hello key.</span></span>
   
    ![Kilidi açılmış disk sürücüsü](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    <span data-ttu-id="68cf7-129">**Şekil 2** kilitli değil disk sürücüsü</span><span class="sxs-lookup"><span data-stu-id="68cf7-129">**Figure 2** Unlocked disk drive</span></span>
4. <span data-ttu-id="68cf7-130">Merhaba disk sürücüsü artık kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="68cf7-130">hello disk drive can now be removed.</span></span>

<span data-ttu-id="68cf7-131">Ters tooengage hello kilit Hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="68cf7-131">Follow hello steps in reverse tooengage hello lock.</span></span>

## <a name="remove-hello-disk-drive"></a><span data-ttu-id="68cf7-132">Merhaba disk sürücüsünü Kaldır</span><span class="sxs-lookup"><span data-stu-id="68cf7-132">Remove hello disk drive</span></span>
<span data-ttu-id="68cf7-133">StorSimple Cihazınızı bir RAID 10 benzeri depolama alanları yapılandırmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="68cf7-133">Your StorSimple device supports a RAID 10-like storage spaces configuration.</span></span> <span data-ttu-id="68cf7-134">Bu, başarısız olan bir diski, katı hal sürücüsü (SSD) normal olarak çalışabilir veya sabit disk sürücüsü (HDD) anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="68cf7-134">This implies that it can operate normally with one failed disk, solid-state drive (SSD), or hard disk drive (HDD).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="68cf7-135">Sisteminizde birden fazla başarısız disk varsa, birden fazla SSD veya HDD herhangi bir noktada hello sisteminden zamanında kaldırmayın.</span><span class="sxs-lookup"><span data-stu-id="68cf7-135">If your system has more than one failed disk, do not remove more than one SSD or HDD from hello system at any point in time.</span></span> <span data-ttu-id="68cf7-136">Bunun yapılması, veri kaybına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="68cf7-136">Doing so could result in loss of data.</span></span>
> * <span data-ttu-id="68cf7-137">Daha önce bir SSD bulunan bir yuvada SSD yerine koyun emin olun.</span><span class="sxs-lookup"><span data-stu-id="68cf7-137">Make sure that you place a replacement SSD in a slot that previously contained an SSD.</span></span> <span data-ttu-id="68cf7-138">Benzer şekilde, daha önce bir HDD bulunan bir yuvada değiştirme HDD yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="68cf7-138">Similarly, place a replacement HDD in a slot that previously contained an HDD.</span></span>
> * <span data-ttu-id="68cf7-139">Hello Azure portal, yuva 0'dan – numaralandırılır 11.</span><span class="sxs-lookup"><span data-stu-id="68cf7-139">In hello Azure portal, slots are numbered from 0 – 11.</span></span> <span data-ttu-id="68cf7-140">Hello portal 2 yuvasındaki bir disk, hello aygıtta başarısız olduğunu gösteriyorsa bu nedenle, başarısız olan diskin hello hello üçüncü yuvasındaki hello üstten sol arayın.</span><span class="sxs-lookup"><span data-stu-id="68cf7-140">Therefore, if hello portal shows that a disk in slot 2 has failed, on hello device, look for hello failed disk in hello third slot from hello top left.</span></span>
> 
> 

<span data-ttu-id="68cf7-141">Sürücüleri kaldırılır ve hello sistem çalışırken değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="68cf7-141">Drives can be removed and replaced while hello system is operating.</span></span>

#### <a name="tooremove-a-drive"></a><span data-ttu-id="68cf7-142">tooremove bir sürücü</span><span class="sxs-lookup"><span data-stu-id="68cf7-142">tooremove a drive</span></span>
1. <span data-ttu-id="68cf7-143">tooidentify hello başarısız diskte, hello Azure portalına gidin tooyour aygıt **ayarlar > donanım durumu**.</span><span class="sxs-lookup"><span data-stu-id="68cf7-143">tooidentify hello failed disk, in hello Azure portal, go tooyour device **Settings > Hardware health**.</span></span> <span data-ttu-id="68cf7-144">Bir disk hello birincil muhafazada ve/veya bir EBOD muhafazası (8600 model kullanıyorsanız) içinde başarısız olabileceğinden altında hello disklerin hello durumu bakmak **paylaşılan bileşenleri** ve altında **EBOD paylaşılan bileşenleri** .</span><span class="sxs-lookup"><span data-stu-id="68cf7-144">Because a disk can fail in hello primary enclosure and/or in an EBOD enclosure (if you are using a 8600 model), look at hello status of hello disks under **Shared components** and under **EBOD shared components**.</span></span> <span data-ttu-id="68cf7-145">Başarısız disk ya da muhafazada kırmızı bir duruma sahip gösterilir.</span><span class="sxs-lookup"><span data-stu-id="68cf7-145">A failed disk in either enclosure will be shown with a red status.</span></span>
2. <span data-ttu-id="68cf7-146">Merhaba sürücüleri hello birincil muhafaza veya hello EBOD muhafazası hello önüne bulun.</span><span class="sxs-lookup"><span data-stu-id="68cf7-146">Locate hello drives in hello front of hello primary enclosure or hello EBOD enclosure.</span></span> 
3. <span data-ttu-id="68cf7-147">Merhaba disk kilidi ise toohello sonraki adıma geçin.</span><span class="sxs-lookup"><span data-stu-id="68cf7-147">If hello disk is unlocked, proceed toohello next step.</span></span> <span data-ttu-id="68cf7-148">Merhaba disk kilitliyse hello yordamı izleyerek kilidini [hello antitamper kilit Disengage](#disengage-the-antitamper-lock).</span><span class="sxs-lookup"><span data-stu-id="68cf7-148">If hello disk is locked, unlock it by following hello procedure in [Disengage hello antitamper lock](#disengage-the-antitamper-lock).</span></span>
4. <span data-ttu-id="68cf7-149">Tuşuna hello siyah hello sürücü taşıyıcı modülünü Mandal ve hello sürücü taşıyıcı tanıtıcı çekerek out ve hello kasa hello Önden çıkartın.</span><span class="sxs-lookup"><span data-stu-id="68cf7-149">Press hello black latch on hello drive carrier module and pull hello drive carrier handle out and away from hello front of hello chassis.</span></span>
   
    ![Disk sürücüsü işleyici bırakılıyor](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    <span data-ttu-id="68cf7-151">**Şekil 3** gönderilirler hello sürücüsü işleyici</span><span class="sxs-lookup"><span data-stu-id="68cf7-151">**Figure 3** Releasing hello drive handle</span></span>
5. <span data-ttu-id="68cf7-152">Merhaba sürücü taşıyıcı tanıtıcı tam olarak genişletildiğinde hello sürücü taşıyıcı hello gövdeden kaydırın.</span><span class="sxs-lookup"><span data-stu-id="68cf7-152">When hello drive carrier handle is fully extended, slide hello drive carrier out of hello chassis.</span></span> 
   
    ![Disk sürücüsünden kayan disk](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    <span data-ttu-id="68cf7-154">**Şekil 4** hello disk sürücüsü hello taşıyıcı dışında kayan</span><span class="sxs-lookup"><span data-stu-id="68cf7-154">**Figure 4** Sliding hello disk drive out of hello carrier</span></span>

## <a name="install-hello-replacement-disk-drive"></a><span data-ttu-id="68cf7-155">Merhaba değiştirme disk sürücüsü yükleyin</span><span class="sxs-lookup"><span data-stu-id="68cf7-155">Install hello replacement disk drive</span></span>
<span data-ttu-id="68cf7-156">Bir sürücü StorSimple Cihazınızı başarısız oldu ve kaldırıldı sonra bu yordamı tooreplace izleyin, yeni bir sürücüye sahip.</span><span class="sxs-lookup"><span data-stu-id="68cf7-156">After a drive has failed in your StorSimple device and you have removed it, follow this procedure tooreplace it with a new drive.</span></span>

#### <a name="tooinsert-a-drive"></a><span data-ttu-id="68cf7-157">tooinsert bir sürücü</span><span class="sxs-lookup"><span data-stu-id="68cf7-157">tooinsert a drive</span></span>
1. <span data-ttu-id="68cf7-158">Merhaba sürücü taşıyıcı tanıtıcı tam olarak genişletilmiş, hello görüntü aşağıdaki gösterildiği gibi emin olun.</span><span class="sxs-lookup"><span data-stu-id="68cf7-158">Ensure hello drive carrier handle is fully extended, as shown in hello following image.</span></span>
   
    ![İşleyicisi genişletilmiş disk sürücüsü](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    <span data-ttu-id="68cf7-160">**Şekil 5** işleyicisi genişletilmiş sürücü</span><span class="sxs-lookup"><span data-stu-id="68cf7-160">**Figure 5** Drive with handle extended</span></span>
2. <span data-ttu-id="68cf7-161">Merhaba sürücü taşıyıcı tüm hello şekilde hello kasaya kaydırın.</span><span class="sxs-lookup"><span data-stu-id="68cf7-161">Slide hello drive carrier all hello way into hello chassis.</span></span>
   
    ![Disk sürücüsü taşıyıcı kayan diskine](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    <span data-ttu-id="68cf7-163">**Şekil 6** hareketli hello sürücü taşıyıcı hello kasa içine</span><span class="sxs-lookup"><span data-stu-id="68cf7-163">**Figure 6**  Sliding hello drive carrier into hello chassis</span></span>
3. <span data-ttu-id="68cf7-164">Hello sürücü taşıyıcı eklenen, Kapat hello sürücü taşıyıcı tanıtıcısıyla hello sürücü taşıyıcı tanıtıcı kilitli bir konumda tutturur kadar hello kasa içine devam ediliyor toopush hello sürücü taşıyıcı oluştu.</span><span class="sxs-lookup"><span data-stu-id="68cf7-164">With hello drive carrier inserted, close hello drive carrier handle while continuing toopush hello drive carrier into hello chassis, until hello drive carrier handle snaps into a locked position.</span></span>
4. <span data-ttu-id="68cf7-165">Microsoft (tamperproof Torx tornavida) toosecure hello taşıyıcı tanıtıcıyla yerine hello kilit Vidayı Çeyrek Aç yönünde kapatarak sağlanan hello lock tuşunun kullanın.</span><span class="sxs-lookup"><span data-stu-id="68cf7-165">Use hello lock key that was provided by Microsoft (tamperproof Torx screwdriver) toosecure hello carrier handle into place by turning hello lock screw a quarter turn clockwise.</span></span>
5. <span data-ttu-id="68cf7-166">Merhaba değiştirme başarılı oldu ve hello sürücü çalışır durumda olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="68cf7-166">Verify that hello replacement was successful and hello drive is operational.</span></span> <span data-ttu-id="68cf7-167">Hello Azure portalına erişmek ve çok gidin**ayarları** > **donanım durumu**.</span><span class="sxs-lookup"><span data-stu-id="68cf7-167">Access hello Azure portal and navigate too**Settings** > **Hardware health**.</span></span> <span data-ttu-id="68cf7-168">Altında **paylaşılan bileşenleri** veya **EBOD paylaşılan bileşenleri**, hello sürücü durumu sağlıklı olduğunu gösteren yeşil.</span><span class="sxs-lookup"><span data-stu-id="68cf7-168">Under **Shared components** or **EBOD shared components**, hello drive status should be green, indicating that it is healthy.</span></span>
<!---Loc Comment: It seems it should say "Device settings > Hardware health" instead of "Settings > Hardware health"---->
   
   > [!NOTE]
   > <span data-ttu-id="68cf7-169">Bunu hello disk durumu tooturn birkaç saat sonra hello değiştirme yeşil sürebilir.</span><span class="sxs-lookup"><span data-stu-id="68cf7-169">It may take several hours for hello disk status tooturn green after hello replacement.</span></span>
  
## <a name="next-steps"></a><span data-ttu-id="68cf7-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="68cf7-170">Next steps</span></span>
<span data-ttu-id="68cf7-171">Daha fazla bilgi edinmek [StorSimple donanım bileşeni değiştirme](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="68cf7-171">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

