---
title: "Microsoft Azure StorSimple 8000 serisi aygıt aaaReplace pilde | Microsoft Docs"
description: "Nasıl tooremove, değiştirin ve StorSimple Cihazınızı hello yedek pil modülünü bakımını açıklar."
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
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: 5ac767807e6c3fd817d8d522629db2aceaac9bdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="b5b09-103">StorSimple Cihazınızda Hello yedek pil modülü değiştirin</span><span class="sxs-lookup"><span data-stu-id="b5b09-103">Replace hello backup battery module on your StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="b5b09-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b5b09-104">Overview</span></span>
<span data-ttu-id="b5b09-105">Merhaba birincil muhafaza güç ve soğutma Modülü (PCM), Microsoft Azure StorSimple Cihazınızda bir ek pil paketi vardır.</span><span class="sxs-lookup"><span data-stu-id="b5b09-105">hello primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="b5b09-106">Bu paketi güç sunar, böylece AC güç toohello birincil muhafaza kaybı ise hello StorSimple Cihazınızı veri kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b5b09-106">This pack provides power so that hello StorSimple device can save data if there is loss of AC power toohello primary enclosure.</span></span> <span data-ttu-id="b5b09-107">Başvurulan tooas hello bu pil paketidir *yedek pil Modülü*.</span><span class="sxs-lookup"><span data-stu-id="b5b09-107">This battery pack is referred tooas hello *backup battery module*.</span></span> <span data-ttu-id="b5b09-108">Merhaba yedek pil modülü var. yalnızca StorSimple Cihazınızı birincil muhafazada hello için (Merhaba EBOD muhafazası bir yedek pil modül içermiyor).</span><span class="sxs-lookup"><span data-stu-id="b5b09-108">hello backup battery module exists only for hello primary enclosure in your StorSimple device (hello EBOD enclosure does not contain a backup battery module).</span></span>

<span data-ttu-id="b5b09-109">Bu öğretici açıklar nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="b5b09-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="b5b09-110">Merhaba yedek pil modülünü Kaldır</span><span class="sxs-lookup"><span data-stu-id="b5b09-110">Remove hello backup battery module</span></span>
* <span data-ttu-id="b5b09-111">Yeni bir yedek pil modülünü yükleme</span><span class="sxs-lookup"><span data-stu-id="b5b09-111">Install a new backup battery module</span></span>
* <span data-ttu-id="b5b09-112">Merhaba yedek pil modülü koru</span><span class="sxs-lookup"><span data-stu-id="b5b09-112">Maintain hello backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b5b09-113">Kaldırma ve bir yedek pil modül değiştirme gözden önce hello hello güvenlik bilgileri [giriş tooStorSimple donanım bileşeni değiştirme](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="b5b09-113">Before removing and replacing a backup battery module, review hello safety information in hello [Introduction tooStorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="remove-hello-backup-battery-module"></a><span data-ttu-id="b5b09-114">Merhaba yedek pil modülünü Kaldır</span><span class="sxs-lookup"><span data-stu-id="b5b09-114">Remove hello backup battery module</span></span>
<span data-ttu-id="b5b09-115">Merhaba yedek pil StorSimple cihazınız için bir alan değiştirebilen birim modülüdür.</span><span class="sxs-lookup"><span data-stu-id="b5b09-115">hello backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="b5b09-116">Merhaba PCM yüklenmeden önce hello pil modülü kendi özgün paketleme depolanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b5b09-116">Before it is installed in hello PCM, hello battery module should be stored in its original packaging.</span></span> <span data-ttu-id="b5b09-117">Aşağıdaki adımları tooremove hello yedek pil hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="b5b09-117">Perform hello following steps tooremove hello backup battery.</span></span>

#### <a name="tooremove-hello-backup-battery-module"></a><span data-ttu-id="b5b09-118">tooremove hello yedek pil Modülü</span><span class="sxs-lookup"><span data-stu-id="b5b09-118">tooremove hello backup battery module</span></span>
1. <span data-ttu-id="b5b09-119">Hello Azure portal, tooyour StorSimple cihaz Yöneticisi hizmeti dikey penceresine gidin.</span><span class="sxs-lookup"><span data-stu-id="b5b09-119">In hello Azure portal, go tooyour StorSimple Device Manager service blade.</span></span> <span data-ttu-id="b5b09-120">Çok Git**aygıtları** ve cihazların Merhaba listeden Cihazınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="b5b09-120">Go too**Devices** and then select your device from hello list of devices.</span></span> <span data-ttu-id="b5b09-121">Çok gidin**İzleyici** > **donanım durumu**.</span><span class="sxs-lookup"><span data-stu-id="b5b09-121">Navigate too**Monitor** > **Hardware health**.</span></span> <span data-ttu-id="b5b09-122">Altında **paylaşılan bileşenleri**, hello pil hello durum öğesine bakın.</span><span class="sxs-lookup"><span data-stu-id="b5b09-122">Under **Shared Components**, look at hello status of hello battery.</span></span>
2. <span data-ttu-id="b5b09-123">Hangi hello pil başarısız oldu hello PCM tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="b5b09-123">Identify hello PCM in which hello battery has failed.</span></span> <span data-ttu-id="b5b09-124">Şekil 1'hello StorSimple cihazı arkasına hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="b5b09-124">Figure 1 shows hello back of hello StorSimple device.</span></span>
   
    ![Aygıt birincil muhafaza modüllerinin devre kartı](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="b5b09-126">**Şekil 1** PCM ve denetleyici modülleri gösteren birincil cihaz arkasına</span><span class="sxs-lookup"><span data-stu-id="b5b09-126">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="b5b09-127">Etiket</span><span class="sxs-lookup"><span data-stu-id="b5b09-127">Label</span></span> | <span data-ttu-id="b5b09-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b5b09-128">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="b5b09-129">1</span><span class="sxs-lookup"><span data-stu-id="b5b09-129">1</span></span> |<span data-ttu-id="b5b09-130">PCM 0</span><span class="sxs-lookup"><span data-stu-id="b5b09-130">PCM 0</span></span> |
   | <span data-ttu-id="b5b09-131">2</span><span class="sxs-lookup"><span data-stu-id="b5b09-131">2</span></span> |<span data-ttu-id="b5b09-132">PCM 1</span><span class="sxs-lookup"><span data-stu-id="b5b09-132">PCM 1</span></span> |
   | <span data-ttu-id="b5b09-133">3</span><span class="sxs-lookup"><span data-stu-id="b5b09-133">3</span></span> |<span data-ttu-id="b5b09-134">Denetleyici 0</span><span class="sxs-lookup"><span data-stu-id="b5b09-134">Controller 0</span></span> |
   | <span data-ttu-id="b5b09-135">4</span><span class="sxs-lookup"><span data-stu-id="b5b09-135">4</span></span> |<span data-ttu-id="b5b09-136">Denetleyici 1</span><span class="sxs-lookup"><span data-stu-id="b5b09-136">Controller 1</span></span> |
   
    <span data-ttu-id="b5b09-137">Gösterge izleme hello numarası 3 hello Şekil 2'de gösterildiği gibi çok karşılık gelen PCM üzerinde 0 neden**pil hataya** aydınlatma.</span><span class="sxs-lookup"><span data-stu-id="b5b09-137">As shown by number 3 in hello Figure 2, hello monitoring indicator LED on PCM 0 that corresponds too**Battery Fault** should be lit.</span></span>
   
    ![Cihaz PCM izleme gösterge LED'lerinin devre kartı](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="b5b09-139">**Şekil 2** geri of PCM gösteren hello gösterge LED'lerinin izleme</span><span class="sxs-lookup"><span data-stu-id="b5b09-139">**Figure 2** Back of PCM showing hello monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="b5b09-140">Etiket</span><span class="sxs-lookup"><span data-stu-id="b5b09-140">Label</span></span> | <span data-ttu-id="b5b09-141">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b5b09-141">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="b5b09-142">1</span><span class="sxs-lookup"><span data-stu-id="b5b09-142">1</span></span> |<span data-ttu-id="b5b09-143">AC güç kesintisi</span><span class="sxs-lookup"><span data-stu-id="b5b09-143">AC power failure</span></span> |
   | <span data-ttu-id="b5b09-144">2</span><span class="sxs-lookup"><span data-stu-id="b5b09-144">2</span></span> |<span data-ttu-id="b5b09-145">Fan hatası</span><span class="sxs-lookup"><span data-stu-id="b5b09-145">Fan failure</span></span> |
   | <span data-ttu-id="b5b09-146">3</span><span class="sxs-lookup"><span data-stu-id="b5b09-146">3</span></span> |<span data-ttu-id="b5b09-147">Pil hatası</span><span class="sxs-lookup"><span data-stu-id="b5b09-147">Battery fault</span></span> |
   | <span data-ttu-id="b5b09-148">4</span><span class="sxs-lookup"><span data-stu-id="b5b09-148">4</span></span> |<span data-ttu-id="b5b09-149">PCM TAMAM</span><span class="sxs-lookup"><span data-stu-id="b5b09-149">PCM OK</span></span> |
   | <span data-ttu-id="b5b09-150">5</span><span class="sxs-lookup"><span data-stu-id="b5b09-150">5</span></span> |<span data-ttu-id="b5b09-151">DC Güç kesintisi</span><span class="sxs-lookup"><span data-stu-id="b5b09-151">DC power failure</span></span> |
   | <span data-ttu-id="b5b09-152">6</span><span class="sxs-lookup"><span data-stu-id="b5b09-152">6</span></span> |<span data-ttu-id="b5b09-153">Sağlıklı pil</span><span class="sxs-lookup"><span data-stu-id="b5b09-153">Battery healthy</span></span> |
3. <span data-ttu-id="b5b09-154">başarısız bir pil ile tooremove hello PCM izleyin hello adımlarda [bir PCM kaldırmak](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span><span class="sxs-lookup"><span data-stu-id="b5b09-154">tooremove hello PCM with a failed battery, follow hello steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="b5b09-155">Hello PCM kaldırıldı, yükseltme ve döndürme hello pil modülü yukarı hello aşağıdaki şekilde gösterildiği gibi işler ve tooremove hello pil çeker.</span><span class="sxs-lookup"><span data-stu-id="b5b09-155">With hello PCM removed, lift and rotate hello battery module handle upward as indicated in hello following figure, and pull it up tooremove hello battery.</span></span>
   
    ![PCM'den pil çıkarılıyor](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="b5b09-157">**Şekil 3** hello pil hello PCM ' kaldırma</span><span class="sxs-lookup"><span data-stu-id="b5b09-157">**Figure 3** Removing hello battery from hello PCM</span></span>
5. <span data-ttu-id="b5b09-158">Merhaba modülü paketleme hello değiştirilebilen birimine yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="b5b09-158">Place hello module in hello field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="b5b09-159">Uygun Bakım ve işleme için hello arızalı ünite tooMicrosoft döndürür.</span><span class="sxs-lookup"><span data-stu-id="b5b09-159">Return hello defective unit tooMicrosoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="b5b09-160">Yeni bir yedek pil modülünü yükleme</span><span class="sxs-lookup"><span data-stu-id="b5b09-160">Install a new backup battery module</span></span>
<span data-ttu-id="b5b09-161">Aşağıdaki adımları tooinstall hello değiştirme pil modülünde hello PCM StorSimple cihazınızın hello birincil muhafazada hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="b5b09-161">Perform hello following steps tooinstall hello replacement battery module in hello PCM in hello primary enclosure of your StorSimple device.</span></span>

#### <a name="tooinstall-hello-battery-module"></a><span data-ttu-id="b5b09-162">tooinstall hello pil Modülü</span><span class="sxs-lookup"><span data-stu-id="b5b09-162">tooinstall hello battery module</span></span>
1. <span data-ttu-id="b5b09-163">Merhaba yedek pil modülü hello uygun hello PCM yönde yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="b5b09-163">Place hello backup battery module in hello proper orientation in hello PCM.</span></span>
2. <span data-ttu-id="b5b09-164">Merhaba pil modülü aşağı tuşuna tüm hello yolu tooseat hello bağlayıcı işleyin.</span><span class="sxs-lookup"><span data-stu-id="b5b09-164">Press down hello battery module handle all hello way tooseat hello connector.</span></span>
3. <span data-ttu-id="b5b09-165">Değiştir hello yönergeleri izleyerek hello birincil muhafazada PCM hello [güç ve soğutma modülü StorSimple Cihazınızda Değiştir](storsimple-power-cooling-module-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="b5b09-165">Replace hello PCM in hello primary enclosure by following hello guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="b5b09-166">Merhaba değiştirme tamamlandıktan sonra Git tooyour cihaz ve çok Git**İzleyici** > **donanım durumu** hello Azure portal'ın.</span><span class="sxs-lookup"><span data-stu-id="b5b09-166">After hello replacement is complete, go tooyour device and then go too**Monitor** > **Hardware health** in hello Azure portal.</span></span> <span data-ttu-id="b5b09-167">Merhaba pil toomake hello yüklemenin başarılı olduğunu emin Hello durumunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b5b09-167">Verify hello status of hello battery toomake sure that hello installation was successful.</span></span> <span data-ttu-id="b5b09-168">Yeşil durum hello pil sağlıklı olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="b5b09-168">A green status indicates that hello battery is healthy.</span></span>

## <a name="maintain-hello-backup-battery-module"></a><span data-ttu-id="b5b09-169">Merhaba yedek pil modülü koru</span><span class="sxs-lookup"><span data-stu-id="b5b09-169">Maintain hello backup battery module</span></span>
<span data-ttu-id="b5b09-170">StorSimple Cihazınızı hello yedek pil modülü güç kaybı olayı sırasında güç toohello denetleyicisi sunar.</span><span class="sxs-lookup"><span data-stu-id="b5b09-170">In your StorSimple device, hello backup battery module provides power toohello controller during a power loss event.</span></span> <span data-ttu-id="b5b09-171">Merhaba StorSimple cihaz toosave kritik verilerin önceki tooshutting aşağı denetimli bir biçimde izin verir.</span><span class="sxs-lookup"><span data-stu-id="b5b09-171">It allows hello StorSimple device toosave critical data prior tooshutting down in a controlled manner.</span></span> <span data-ttu-id="b5b09-172">Merhaba PCMs içinde iki tam dolu pil ile Merhaba sistem iki ardışık kaybı olayları işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="b5b09-172">With two fully charged batteries in hello PCMs, hello system can handle two consecutive loss events.</span></span>

<span data-ttu-id="b5b09-173">Hello Azure portal, hello **donanım durumu** hello altında **İzleyici** dikey penceresinde hello pil arızalı ya da hello son yaşam yaklaşan gösterir.</span><span class="sxs-lookup"><span data-stu-id="b5b09-173">In hello Azure portal, hello **Hardware health** under hello **Monitor** blade indicates whether hello battery is malfunctioning or hello end-of-life is approaching.</span></span> <span data-ttu-id="b5b09-174">Merhaba pil durumu tarafından belirtilir **PCM 0 pil** veya **pil PCM 1** altında **paylaşılan bileşenleri**.</span><span class="sxs-lookup"><span data-stu-id="b5b09-174">hello battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="b5b09-175">Bu dikey gösterecek bir **DEGRADED** ömrü sonu yaklaşan için durum ve **başarısız** ömrü son ulaştı.</span><span class="sxs-lookup"><span data-stu-id="b5b09-175">This blade will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span>

> [!NOTE]
> <span data-ttu-id="b5b09-176">Merhaba pil raporlama yapabilir **başarısız** , yalnızca gerektiği zaman toobe ücretlendirilir.</span><span class="sxs-lookup"><span data-stu-id="b5b09-176">hello battery can report **FAILED** when it simply needs toobe charged.</span></span>


<span data-ttu-id="b5b09-177">Merhaba, **DEGRADED** durumu görünür, aşağıdaki eylemin hello öneririz:</span><span class="sxs-lookup"><span data-stu-id="b5b09-177">If hello **DEGRADED** state appears, we recommend hello following course of action:</span></span>

* <span data-ttu-id="b5b09-178">Merhaba sistem son güç kaybı karşılaşmış veya hello piller düzenli bakım altında.</span><span class="sxs-lookup"><span data-stu-id="b5b09-178">hello system may have experienced a recent power loss or hello batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="b5b09-179">Devam etmeden önce 12 saat Hello sistem gözlemleyin.</span><span class="sxs-lookup"><span data-stu-id="b5b09-179">Observe hello system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="b5b09-180">Merhaba durum hala ise **DEGRADED** denetleyicileri ve PCMs çalıştıran, sürekli bağlantı tooAC güç hello ile 12 saat sonra hello sonra değiştirilen toobe pil gerekir.</span><span class="sxs-lookup"><span data-stu-id="b5b09-180">If hello state is still **DEGRADED** after 12 hours of continuous connection tooAC power with hello controllers and PCMs running, then hello battery needs toobe replaced.</span></span> <span data-ttu-id="b5b09-181">Lütfen [Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md) yedek yedek pil modülü için.</span><span class="sxs-lookup"><span data-stu-id="b5b09-181">Please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="b5b09-182">Merhaba durumu Tamam 12 saat sonra olursa, hello pil işlevseldir ve yalnızca bir bakım ücret gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b5b09-182">If hello state becomes OK after 12 hours, hello battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="b5b09-183">Değil yapıldıysa ilişkili kaybına AC gücü ve hello PCM açık olduğundan ve tooAC güç bağlı, hello pil yerini toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="b5b09-183">If there has not been an associated loss of AC power and hello PCM is turned on and connected tooAC power, hello battery needs toobe replaced.</span></span> <span data-ttu-id="b5b09-184">[Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md) tooorder bir yedek yedek pil modül.</span><span class="sxs-lookup"><span data-stu-id="b5b09-184">[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) tooorder a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b5b09-185">Merhaba Dispose toonational ve bölgesel düzenlemelere göre pil başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="b5b09-185">Dispose of hello failed battery according toonational and regional regulations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5b09-186">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b5b09-186">Next steps</span></span>
<span data-ttu-id="b5b09-187">Daha fazla bilgi edinmek [StorSimple donanım bileşeni değiştirme](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="b5b09-187">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

