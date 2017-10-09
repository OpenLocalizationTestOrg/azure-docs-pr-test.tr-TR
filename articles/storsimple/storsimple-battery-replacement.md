---
title: Microsoft Azure StorSimple cihaz aaaReplace pilde | Microsoft Docs
description: "Nasıl tooremove, değiştirin ve StorSimple Cihazınızı hello yedek pil modülünü bakımını açıklar."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3c8a6654-4826-4883-aad8-75f332347c53
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 542774a5f451ec7ad2bd442f88598df318d8b285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="982df-103">StorSimple Cihazınızda Hello yedek pil modülü değiştirin</span><span class="sxs-lookup"><span data-stu-id="982df-103">Replace hello backup battery module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="982df-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="982df-104">Overview</span></span>
<span data-ttu-id="982df-105">Merhaba birincil muhafaza güç ve soğutma Modülü (PCM), Microsoft Azure StorSimple Cihazınızda bir ek pil paketi vardır.</span><span class="sxs-lookup"><span data-stu-id="982df-105">hello primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="982df-106">Bu paketi güç sunar, böylece AC güç toohello birincil muhafaza kaybı ise hello StorSimple Cihazınızı veri kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="982df-106">This pack provides power so that hello StorSimple device can save data if there is loss of AC power toohello primary enclosure.</span></span> <span data-ttu-id="982df-107">Başvurulan tooas hello bu pil paketidir *yedek pil Modülü*.</span><span class="sxs-lookup"><span data-stu-id="982df-107">This battery pack is referred tooas hello *backup battery module*.</span></span> <span data-ttu-id="982df-108">Merhaba yedek pil modülü var. yalnızca StorSimple Cihazınızı birincil muhafazada hello için (Merhaba EBOD muhafazası bir yedek pil modül içermiyor).</span><span class="sxs-lookup"><span data-stu-id="982df-108">hello backup battery module exists only for hello primary enclosure in your StorSimple device (hello EBOD enclosure does not contain a backup battery module).</span></span> 

<span data-ttu-id="982df-109">Bu öğretici açıklar nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="982df-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="982df-110">Merhaba yedek pil modülünü Kaldır</span><span class="sxs-lookup"><span data-stu-id="982df-110">Remove hello backup battery module</span></span> 
* <span data-ttu-id="982df-111">Yeni bir yedek pil modülünü yükleme</span><span class="sxs-lookup"><span data-stu-id="982df-111">Install a new backup battery module</span></span>
* <span data-ttu-id="982df-112">Merhaba yedek pil modülü koru</span><span class="sxs-lookup"><span data-stu-id="982df-112">Maintain hello backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="982df-113">Kaldırma ve bir yedek pil modül değiştirme gözden önce hello hello güvenlik bilgileri [giriş tooStorSimple donanım bileşeni değiştirme](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="982df-113">Before removing and replacing a backup battery module, review hello safety information in hello [Introduction tooStorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-hello-backup-battery-module"></a><span data-ttu-id="982df-114">Merhaba yedek pil modülünü Kaldır</span><span class="sxs-lookup"><span data-stu-id="982df-114">Remove hello backup battery module</span></span>
<span data-ttu-id="982df-115">Merhaba yedek pil StorSimple cihazınız için bir alan değiştirebilen birim modülüdür.</span><span class="sxs-lookup"><span data-stu-id="982df-115">hello backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="982df-116">Merhaba PCM yüklenmeden önce hello pil modülü kendi özgün paketleme depolanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="982df-116">Before it is installed in hello PCM, hello battery module should be stored in its original packaging.</span></span> <span data-ttu-id="982df-117">Aşağıdaki adımları tooremove hello yedek pil hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="982df-117">Perform hello following steps tooremove hello backup battery.</span></span>

#### <a name="tooremove-hello-backup-battery-module"></a><span data-ttu-id="982df-118">tooremove hello yedek pil Modülü</span><span class="sxs-lookup"><span data-stu-id="982df-118">tooremove hello backup battery module</span></span>
1. <span data-ttu-id="982df-119">Buna Klasik Azure portalı Merhaba, çok Git**aygıtları** > **Bakım** > **donanım durum**.</span><span class="sxs-lookup"><span data-stu-id="982df-119">In hello Azure classic portal, go too**Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="982df-120">Altında **paylaşılan bileşenleri**, hello pil hello durum öğesine bakın.</span><span class="sxs-lookup"><span data-stu-id="982df-120">Under **Shared Components**, look at hello status of hello battery.</span></span>
2. <span data-ttu-id="982df-121">Hangi hello pil başarısız oldu hello PCM tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="982df-121">Identify hello PCM in which hello battery has failed.</span></span> <span data-ttu-id="982df-122">Şekil 1'hello StorSimple cihazı arkasına hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="982df-122">Figure 1 shows hello back of hello StorSimple device.</span></span>
   
    ![Aygıt birincil muhafaza modüllerinin devre kartı](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="982df-124">**Şekil 1** PCM ve denetleyici modülleri gösteren birincil cihaz arkasına</span><span class="sxs-lookup"><span data-stu-id="982df-124">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="982df-125">Etiket</span><span class="sxs-lookup"><span data-stu-id="982df-125">Label</span></span> | <span data-ttu-id="982df-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="982df-126">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="982df-127">1</span><span class="sxs-lookup"><span data-stu-id="982df-127">1</span></span> |<span data-ttu-id="982df-128">PCM 0</span><span class="sxs-lookup"><span data-stu-id="982df-128">PCM 0</span></span> |
   | <span data-ttu-id="982df-129">2</span><span class="sxs-lookup"><span data-stu-id="982df-129">2</span></span> |<span data-ttu-id="982df-130">PCM 1</span><span class="sxs-lookup"><span data-stu-id="982df-130">PCM 1</span></span> |
   | <span data-ttu-id="982df-131">3</span><span class="sxs-lookup"><span data-stu-id="982df-131">3</span></span> |<span data-ttu-id="982df-132">Denetleyici 0</span><span class="sxs-lookup"><span data-stu-id="982df-132">Controller 0</span></span> |
   | <span data-ttu-id="982df-133">4</span><span class="sxs-lookup"><span data-stu-id="982df-133">4</span></span> |<span data-ttu-id="982df-134">Denetleyici 1</span><span class="sxs-lookup"><span data-stu-id="982df-134">Controller 1</span></span> |
   
    <span data-ttu-id="982df-135">Gösterge izleme hello numarası 3 hello Şekil 2'de gösterildiği gibi çok karşılık gelen PCM üzerinde 0 neden**pil hataya** aydınlatma.</span><span class="sxs-lookup"><span data-stu-id="982df-135">As shown by number 3 in hello Figure 2, hello monitoring indicator LED on PCM 0 that corresponds too**Battery Fault** should be lit.</span></span>
   
    ![Cihaz PCM izleme gösterge LED'lerinin devre kartı](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="982df-137">**Şekil 2** geri of PCM gösteren hello gösterge LED'lerinin izleme</span><span class="sxs-lookup"><span data-stu-id="982df-137">**Figure 2** Back of PCM showing hello monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="982df-138">Etiket</span><span class="sxs-lookup"><span data-stu-id="982df-138">Label</span></span> | <span data-ttu-id="982df-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="982df-139">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="982df-140">1</span><span class="sxs-lookup"><span data-stu-id="982df-140">1</span></span> |<span data-ttu-id="982df-141">AC güç kesintisi</span><span class="sxs-lookup"><span data-stu-id="982df-141">AC power failure</span></span> |
   | <span data-ttu-id="982df-142">2</span><span class="sxs-lookup"><span data-stu-id="982df-142">2</span></span> |<span data-ttu-id="982df-143">Fan hatası</span><span class="sxs-lookup"><span data-stu-id="982df-143">Fan failure</span></span> |
   | <span data-ttu-id="982df-144">3</span><span class="sxs-lookup"><span data-stu-id="982df-144">3</span></span> |<span data-ttu-id="982df-145">Pil hatası</span><span class="sxs-lookup"><span data-stu-id="982df-145">Battery fault</span></span> |
   | <span data-ttu-id="982df-146">4</span><span class="sxs-lookup"><span data-stu-id="982df-146">4</span></span> |<span data-ttu-id="982df-147">PCM TAMAM</span><span class="sxs-lookup"><span data-stu-id="982df-147">PCM OK</span></span> |
   | <span data-ttu-id="982df-148">5</span><span class="sxs-lookup"><span data-stu-id="982df-148">5</span></span> |<span data-ttu-id="982df-149">DC Güç kesintisi</span><span class="sxs-lookup"><span data-stu-id="982df-149">DC power failure</span></span> |
   | <span data-ttu-id="982df-150">6</span><span class="sxs-lookup"><span data-stu-id="982df-150">6</span></span> |<span data-ttu-id="982df-151">Sağlıklı pil</span><span class="sxs-lookup"><span data-stu-id="982df-151">Battery healthy</span></span> |
3. <span data-ttu-id="982df-152">başarısız bir pil ile tooremove hello PCM izleyin hello adımlarda [bir PCM kaldırmak](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span><span class="sxs-lookup"><span data-stu-id="982df-152">tooremove hello PCM with a failed battery, follow hello steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="982df-153">Hello PCM kaldırıldı, yükseltme ve döndürme hello pil modülü yukarı hello aşağıdaki şekilde gösterildiği gibi işler ve tooremove hello pil çeker.</span><span class="sxs-lookup"><span data-stu-id="982df-153">With hello PCM removed, lift and rotate hello battery module handle upward as indicated in hello following figure, and pull it up tooremove hello battery.</span></span>
   
    ![PCM'den pil çıkarılıyor](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="982df-155">**Şekil 3** hello pil hello PCM ' kaldırma</span><span class="sxs-lookup"><span data-stu-id="982df-155">**Figure 3** Removing hello battery from hello PCM</span></span>
5. <span data-ttu-id="982df-156">Merhaba modülü paketleme hello değiştirilebilen birimine yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="982df-156">Place hello module in hello field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="982df-157">Uygun Bakım ve işleme için hello arızalı ünite tooMicrosoft döndürür.</span><span class="sxs-lookup"><span data-stu-id="982df-157">Return hello defective unit tooMicrosoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="982df-158">Yeni bir yedek pil modülünü yükleme</span><span class="sxs-lookup"><span data-stu-id="982df-158">Install a new backup battery module</span></span>
<span data-ttu-id="982df-159">Aşağıdaki adımları tooinstall hello değiştirme pil modülünde hello PCM StorSimple cihazınızın hello birincil muhafazada hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="982df-159">Perform hello following steps tooinstall hello replacement battery module in hello PCM in hello primary enclosure of your StorSimple device.</span></span>

#### <a name="tooinstall-hello-battery-module"></a><span data-ttu-id="982df-160">tooinstall hello pil Modülü</span><span class="sxs-lookup"><span data-stu-id="982df-160">tooinstall hello battery module</span></span>
1. <span data-ttu-id="982df-161">Merhaba yedek pil modülü hello uygun hello PCM yönde yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="982df-161">Place hello backup battery module in hello proper orientation in hello PCM.</span></span>
2. <span data-ttu-id="982df-162">Merhaba pil modülü aşağı tuşuna tüm hello yolu tooseat hello bağlayıcı işleyin.</span><span class="sxs-lookup"><span data-stu-id="982df-162">Press down hello battery module handle all hello way tooseat hello connector.</span></span>
3. <span data-ttu-id="982df-163">Değiştir hello yönergeleri izleyerek hello birincil muhafazada PCM hello [güç ve soğutma modülü StorSimple Cihazınızda Değiştir](storsimple-power-cooling-module-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="982df-163">Replace hello PCM in hello primary enclosure by following hello guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="982df-164">Merhaba değiştirme tamamlandıktan sonra çok Git**aygıtları** > **Bakım** > **donanım durum** hello Klasik Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="982df-164">After hello replacement is complete, go too**Devices** > **Maintenance** > **Hardware Status** in hello Azure classic portal.</span></span> <span data-ttu-id="982df-165">Merhaba pil toomake hello yüklemenin başarılı olduğunu emin Hello durumunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="982df-165">Verify hello status of hello battery toomake sure that hello installation was successful.</span></span> <span data-ttu-id="982df-166">Yeşil durum hello pil sağlıklı olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="982df-166">A green status indicates that hello battery is healthy.</span></span>

## <a name="maintain-hello-backup-battery-module"></a><span data-ttu-id="982df-167">Merhaba yedek pil modülü koru</span><span class="sxs-lookup"><span data-stu-id="982df-167">Maintain hello backup battery module</span></span>
<span data-ttu-id="982df-168">StorSimple Cihazınızı hello yedek pil modülü güç kaybı olayı sırasında güç toohello denetleyicisi sunar.</span><span class="sxs-lookup"><span data-stu-id="982df-168">In your StorSimple device, hello backup battery module provides power toohello controller during a power loss event.</span></span> <span data-ttu-id="982df-169">Merhaba StorSimple cihaz toosave kritik verilerin önceki tooshutting aşağı denetimli bir biçimde izin verir.</span><span class="sxs-lookup"><span data-stu-id="982df-169">It allows hello StorSimple device toosave critical data prior tooshutting down in a controlled manner.</span></span> <span data-ttu-id="982df-170">Merhaba PCMs içinde iki tam dolu pil ile Merhaba sistem iki ardışık kaybı olayları işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="982df-170">With two fully charged batteries in hello PCMs, hello system can handle two consecutive loss events.</span></span>

<span data-ttu-id="982df-171">Hello Klasik Azure portalı, hello **donanım durumu** hello üzerinde **Bakım** sayfa hello pil arızalı ya da hello son yaşam yaklaştığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="982df-171">In hello Azure classic portal, hello **Hardware Status** on hello **Maintenance** page indicates whether hello battery is malfunctioning or hello end-of-life is approaching.</span></span> <span data-ttu-id="982df-172">Merhaba pil durumu tarafından belirtilir **PCM 0 pil** veya **pil PCM 1** altında **paylaşılan bileşenleri**.</span><span class="sxs-lookup"><span data-stu-id="982df-172">hello battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="982df-173">Bu sayfada gösterilir bir **DEGRADED** ömrü sonu yaklaşan için durum ve **başarısız** ömrü son ulaştı.</span><span class="sxs-lookup"><span data-stu-id="982df-173">This page will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span> 

> [!NOTE]
> <span data-ttu-id="982df-174">Merhaba pil raporlama yapabilir **başarısız** , yalnızca gerektiği zaman toobe ücretlendirilir.</span><span class="sxs-lookup"><span data-stu-id="982df-174">hello battery can report **FAILED** when it simply needs toobe charged.</span></span>
> 
> 

<span data-ttu-id="982df-175">Merhaba, **DEGRADED** durumu görünür, aşağıdaki eylemin hello öneririz:</span><span class="sxs-lookup"><span data-stu-id="982df-175">If hello **DEGRADED** state appears, we recommend hello following course of action:</span></span>

* <span data-ttu-id="982df-176">Merhaba sistem son güç kaybı karşılaşmış veya hello piller düzenli bakım altında.</span><span class="sxs-lookup"><span data-stu-id="982df-176">hello system may have experienced a recent power loss or hello batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="982df-177">Devam etmeden önce 12 saat Hello sistem gözlemleyin.</span><span class="sxs-lookup"><span data-stu-id="982df-177">Observe hello system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="982df-178">Merhaba durum hala ise **DEGRADED** denetleyicileri ve PCMs çalıştıran, sürekli bağlantı tooAC güç hello ile 12 saat sonra hello sonra değiştirilen toobe pil gerekir.</span><span class="sxs-lookup"><span data-stu-id="982df-178">If hello state is still **DEGRADED** after 12 hours of continuous connection tooAC power with hello controllers and PCMs running, then hello battery needs toobe replaced.</span></span> <span data-ttu-id="982df-179">Lütfen [Microsoft Support başvurun](storsimple-contact-microsoft-support.md) yedek yedek pil modülü için.</span><span class="sxs-lookup"><span data-stu-id="982df-179">Please [contact Microsoft Support](storsimple-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="982df-180">Merhaba durumu Tamam 12 saat sonra olursa, hello pil işlevseldir ve yalnızca bir bakım ücret gereklidir.</span><span class="sxs-lookup"><span data-stu-id="982df-180">If hello state becomes OK after 12 hours, hello battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="982df-181">Değil yapıldıysa ilişkili kaybına AC gücü ve hello PCM açık olduğundan ve tooAC güç bağlı, hello pil yerini toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="982df-181">If there has not been an associated loss of AC power and hello PCM is turned on and connected tooAC power, hello battery needs toobe replaced.</span></span> <span data-ttu-id="982df-182">[Microsoft Support başvurun](storsimple-contact-microsoft-support.md) tooorder bir yedek yedek pil modül.</span><span class="sxs-lookup"><span data-stu-id="982df-182">[Contact Microsoft Support](storsimple-contact-microsoft-support.md) tooorder a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="982df-183">Merhaba Dispose toonational ve bölgesel düzenlemelere göre pil başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="982df-183">Dispose of hello failed battery according toonational and regional regulations.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="982df-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="982df-184">Next steps</span></span>
<span data-ttu-id="982df-185">Daha fazla bilgi edinmek [StorSimple donanım bileşeni değiştirme](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="982df-185">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

