---
title: "Microsoft Azure StorSimple 8000 serisi aygıt pilde Değiştir | Microsoft Docs"
description: "Kaldırmak için değiştirin ve StorSimple Cihazınızda yedek pil modülü korumak açıklar."
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
ms.openlocfilehash: 174a3163082594ea6a49b7f5a78857848f8f0566
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="replace-the-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="21c69-103">StorSimple Cihazınızda yedek pil modülü değiştirin</span><span class="sxs-lookup"><span data-stu-id="21c69-103">Replace the backup battery module on your StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="21c69-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="21c69-104">Overview</span></span>
<span data-ttu-id="21c69-105">Birincil muhafaza güç ve soğutma Modülü (PCM), Microsoft Azure StorSimple Cihazınızda bir ek pil paketi vardır.</span><span class="sxs-lookup"><span data-stu-id="21c69-105">The primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="21c69-106">Bu paketi güç sunar, böylece birincil kasası AC güç kaybı ise StorSimple cihazı veri kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21c69-106">This pack provides power so that the StorSimple device can save data if there is loss of AC power to the primary enclosure.</span></span> <span data-ttu-id="21c69-107">Bu pil paketi olarak adlandırılır *yedek pil Modülü*.</span><span class="sxs-lookup"><span data-stu-id="21c69-107">This battery pack is referred to as the *backup battery module*.</span></span> <span data-ttu-id="21c69-108">Yedek pil modülü yalnızca StorSimple Cihazınızı (EBOD muhafazası bir yedek pil modül içermiyor) birincil muhafazada yok.</span><span class="sxs-lookup"><span data-stu-id="21c69-108">The backup battery module exists only for the primary enclosure in your StorSimple device (the EBOD enclosure does not contain a backup battery module).</span></span>

<span data-ttu-id="21c69-109">Bu öğretici açıklar nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="21c69-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="21c69-110">Yedek pil modülünü Kaldır</span><span class="sxs-lookup"><span data-stu-id="21c69-110">Remove the backup battery module</span></span>
* <span data-ttu-id="21c69-111">Yeni bir yedek pil modülünü yükleme</span><span class="sxs-lookup"><span data-stu-id="21c69-111">Install a new backup battery module</span></span>
* <span data-ttu-id="21c69-112">Yedek pil modülü koru</span><span class="sxs-lookup"><span data-stu-id="21c69-112">Maintain the backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21c69-113">Kaldırma ve bir yedek pil modül değiştirme gözden önce güvenlik bilgileri [StorSimple donanım bileşeni değiştirme giriş](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="21c69-113">Before removing and replacing a backup battery module, review the safety information in the [Introduction to StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="remove-the-backup-battery-module"></a><span data-ttu-id="21c69-114">Yedek pil modülünü Kaldır</span><span class="sxs-lookup"><span data-stu-id="21c69-114">Remove the backup battery module</span></span>
<span data-ttu-id="21c69-115">Bir alan değiştirebilen birim StorSimple cihazınız için yedek pil modülüdür.</span><span class="sxs-lookup"><span data-stu-id="21c69-115">The backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="21c69-116">PCM yüklenmeden önce pil modülü kendi özgün paketleme depolanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="21c69-116">Before it is installed in the PCM, the battery module should be stored in its original packaging.</span></span> <span data-ttu-id="21c69-117">Yedek pil kaldırmak için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="21c69-117">Perform the following steps to remove the backup battery.</span></span>

#### <a name="to-remove-the-backup-battery-module"></a><span data-ttu-id="21c69-118">Yedek pil modülünü kaldırmak için</span><span class="sxs-lookup"><span data-stu-id="21c69-118">To remove the backup battery module</span></span>
1. <span data-ttu-id="21c69-119">Azure portalında StorSimple cihaz Yöneticisi hizmeti dikey penceresine gidin.</span><span class="sxs-lookup"><span data-stu-id="21c69-119">In the Azure portal, go to your StorSimple Device Manager service blade.</span></span> <span data-ttu-id="21c69-120">Git **aygıtları** ve ardından Cihazınızı aygıtları listesinden seçin.</span><span class="sxs-lookup"><span data-stu-id="21c69-120">Go to **Devices** and then select your device from the list of devices.</span></span> <span data-ttu-id="21c69-121">Gidin **İzleyici** > **donanım durumu**.</span><span class="sxs-lookup"><span data-stu-id="21c69-121">Navigate to **Monitor** > **Hardware health**.</span></span> <span data-ttu-id="21c69-122">Altında **paylaşılan bileşenleri**, pil durum öğesine bakın.</span><span class="sxs-lookup"><span data-stu-id="21c69-122">Under **Shared Components**, look at the status of the battery.</span></span>
2. <span data-ttu-id="21c69-123">Pil başarısız oldu PCM tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="21c69-123">Identify the PCM in which the battery has failed.</span></span> <span data-ttu-id="21c69-124">Şekil 1, StorSimple cihazı arkası gösterir.</span><span class="sxs-lookup"><span data-stu-id="21c69-124">Figure 1 shows the back of the StorSimple device.</span></span>
   
    ![Aygıt birincil muhafaza modüllerinin devre kartı](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="21c69-126">**Şekil 1** PCM ve denetleyici modülleri gösteren birincil cihaz arkasına</span><span class="sxs-lookup"><span data-stu-id="21c69-126">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="21c69-127">Etiket</span><span class="sxs-lookup"><span data-stu-id="21c69-127">Label</span></span> | <span data-ttu-id="21c69-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21c69-128">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="21c69-129">1</span><span class="sxs-lookup"><span data-stu-id="21c69-129">1</span></span> |<span data-ttu-id="21c69-130">PCM 0</span><span class="sxs-lookup"><span data-stu-id="21c69-130">PCM 0</span></span> |
   | <span data-ttu-id="21c69-131">2</span><span class="sxs-lookup"><span data-stu-id="21c69-131">2</span></span> |<span data-ttu-id="21c69-132">PCM 1</span><span class="sxs-lookup"><span data-stu-id="21c69-132">PCM 1</span></span> |
   | <span data-ttu-id="21c69-133">3</span><span class="sxs-lookup"><span data-stu-id="21c69-133">3</span></span> |<span data-ttu-id="21c69-134">Denetleyici 0</span><span class="sxs-lookup"><span data-stu-id="21c69-134">Controller 0</span></span> |
   | <span data-ttu-id="21c69-135">4</span><span class="sxs-lookup"><span data-stu-id="21c69-135">4</span></span> |<span data-ttu-id="21c69-136">Denetleyici 1</span><span class="sxs-lookup"><span data-stu-id="21c69-136">Controller 1</span></span> |
   
    <span data-ttu-id="21c69-137">Sayı 3 Şekil 2'de gösterildiği gibi izleme gösterge ÖNCÜLÜK karşılık gelen PCM 0 üzerinde **pil hataya** aydınlatma.</span><span class="sxs-lookup"><span data-stu-id="21c69-137">As shown by number 3 in the Figure 2, the monitoring indicator LED on PCM 0 that corresponds to **Battery Fault** should be lit.</span></span>
   
    ![Cihaz PCM izleme gösterge LED'lerinin devre kartı](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="21c69-139">**Şekil 2** geri of PCM izleme gösterge LED'leri gösterme</span><span class="sxs-lookup"><span data-stu-id="21c69-139">**Figure 2** Back of PCM showing the monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="21c69-140">Etiket</span><span class="sxs-lookup"><span data-stu-id="21c69-140">Label</span></span> | <span data-ttu-id="21c69-141">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21c69-141">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="21c69-142">1</span><span class="sxs-lookup"><span data-stu-id="21c69-142">1</span></span> |<span data-ttu-id="21c69-143">AC güç kesintisi</span><span class="sxs-lookup"><span data-stu-id="21c69-143">AC power failure</span></span> |
   | <span data-ttu-id="21c69-144">2</span><span class="sxs-lookup"><span data-stu-id="21c69-144">2</span></span> |<span data-ttu-id="21c69-145">Fan hatası</span><span class="sxs-lookup"><span data-stu-id="21c69-145">Fan failure</span></span> |
   | <span data-ttu-id="21c69-146">3</span><span class="sxs-lookup"><span data-stu-id="21c69-146">3</span></span> |<span data-ttu-id="21c69-147">Pil hatası</span><span class="sxs-lookup"><span data-stu-id="21c69-147">Battery fault</span></span> |
   | <span data-ttu-id="21c69-148">4</span><span class="sxs-lookup"><span data-stu-id="21c69-148">4</span></span> |<span data-ttu-id="21c69-149">PCM TAMAM</span><span class="sxs-lookup"><span data-stu-id="21c69-149">PCM OK</span></span> |
   | <span data-ttu-id="21c69-150">5</span><span class="sxs-lookup"><span data-stu-id="21c69-150">5</span></span> |<span data-ttu-id="21c69-151">DC Güç kesintisi</span><span class="sxs-lookup"><span data-stu-id="21c69-151">DC power failure</span></span> |
   | <span data-ttu-id="21c69-152">6</span><span class="sxs-lookup"><span data-stu-id="21c69-152">6</span></span> |<span data-ttu-id="21c69-153">Sağlıklı pil</span><span class="sxs-lookup"><span data-stu-id="21c69-153">Battery healthy</span></span> |
3. <span data-ttu-id="21c69-154">Başarısız pille PCM kaldırmak için adımları [bir PCM kaldırmak](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span><span class="sxs-lookup"><span data-stu-id="21c69-154">To remove the PCM with a failed battery, follow the steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="21c69-155">Kaldırılan PCM ile kaldırın ve aşağıdaki çizimde gösterildiği gibi pil modül işleyiciyi Yukarı Döndür ve pil Kaldır kadar çekme.</span><span class="sxs-lookup"><span data-stu-id="21c69-155">With the PCM removed, lift and rotate the battery module handle upward as indicated in the following figure, and pull it up to remove the battery.</span></span>
   
    ![PCM'den pil çıkarılıyor](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="21c69-157">**Şekil 3** PCM'den pil çıkarılıyor</span><span class="sxs-lookup"><span data-stu-id="21c69-157">**Figure 3** Removing the battery from the PCM</span></span>
5. <span data-ttu-id="21c69-158">Paketleme alan değiştirebilen birim modülünde yer.</span><span class="sxs-lookup"><span data-stu-id="21c69-158">Place the module in the field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="21c69-159">Arızalı ünite uygun Bakım ve işleme için Microsoft'a döndürür.</span><span class="sxs-lookup"><span data-stu-id="21c69-159">Return the defective unit to Microsoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="21c69-160">Yeni bir yedek pil modülünü yükleme</span><span class="sxs-lookup"><span data-stu-id="21c69-160">Install a new backup battery module</span></span>
<span data-ttu-id="21c69-161">StorSimple cihazınızın birincil muhafazada PCM değiştirme pil modülünü yüklemek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="21c69-161">Perform the following steps to install the replacement battery module in the PCM in the primary enclosure of your StorSimple device.</span></span>

#### <a name="to-install-the-battery-module"></a><span data-ttu-id="21c69-162">Pil modülünü yüklemek için</span><span class="sxs-lookup"><span data-stu-id="21c69-162">To install the battery module</span></span>
1. <span data-ttu-id="21c69-163">Yedek pil modülü PCM uygun yönde yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="21c69-163">Place the backup battery module in the proper orientation in the PCM.</span></span>
2. <span data-ttu-id="21c69-164">Bu süreç boyunca tüm bağlayıcı oturak için pil modül işleyiciyi basın.</span><span class="sxs-lookup"><span data-stu-id="21c69-164">Press down the battery module handle all the way to seat the connector.</span></span>
3. <span data-ttu-id="21c69-165">Yönergeleri izleyerek birincil muhafazada PCM Değiştir [güç ve soğutma modülü StorSimple Cihazınızda Değiştir](storsimple-power-cooling-module-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="21c69-165">Replace the PCM in the primary enclosure by following the guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="21c69-166">Bu değişiklik tamamlandıktan sonra aygıtınıza gidin ve gidin **İzleyici** > **donanım durumu** Azure portalında.</span><span class="sxs-lookup"><span data-stu-id="21c69-166">After the replacement is complete, go to your device and then go to **Monitor** > **Hardware health** in the Azure portal.</span></span> <span data-ttu-id="21c69-167">Yüklemenin başarılı olduğunu emin olmak için pil durumunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="21c69-167">Verify the status of the battery to make sure that the installation was successful.</span></span> <span data-ttu-id="21c69-168">Yeşil durum pil sağlıklı olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="21c69-168">A green status indicates that the battery is healthy.</span></span>

## <a name="maintain-the-backup-battery-module"></a><span data-ttu-id="21c69-169">Yedek pil modülü koru</span><span class="sxs-lookup"><span data-stu-id="21c69-169">Maintain the backup battery module</span></span>
<span data-ttu-id="21c69-170">StorSimple Cihazınızı yedek pil modülü güç kaybı olayı sırasında denetleyiciye güç sağlar.</span><span class="sxs-lookup"><span data-stu-id="21c69-170">In your StorSimple device, the backup battery module provides power to the controller during a power loss event.</span></span> <span data-ttu-id="21c69-171">Denetimli bir biçimde kapatmadan önce kritik verileri kaydetmek StorSimple cihazı sağlar.</span><span class="sxs-lookup"><span data-stu-id="21c69-171">It allows the StorSimple device to save critical data prior to shutting down in a controlled manner.</span></span> <span data-ttu-id="21c69-172">İki tam dolu pilleri ile PCMs, iki ardışık kaybı olay sistem işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="21c69-172">With two fully charged batteries in the PCMs, the system can handle two consecutive loss events.</span></span>

<span data-ttu-id="21c69-173">Azure portalında **donanım durumu** altında **İzleyici** dikey pil arızalı ya da son yaşam yaklaştığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="21c69-173">In the Azure portal, the **Hardware health** under the **Monitor** blade indicates whether the battery is malfunctioning or the end-of-life is approaching.</span></span> <span data-ttu-id="21c69-174">Pil durumu belirtilir **PCM 0 pil** veya **pil PCM 1** altında **paylaşılan bileşenleri**.</span><span class="sxs-lookup"><span data-stu-id="21c69-174">The battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="21c69-175">Bu dikey gösterecek bir **DEGRADED** ömrü sonu yaklaşan için durum ve **başarısız** ömrü son ulaştı.</span><span class="sxs-lookup"><span data-stu-id="21c69-175">This blade will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span>

> [!NOTE]
> <span data-ttu-id="21c69-176">Pil raporlayabilirsiniz **başarısız** , yalnızca gerektiği zaman uygulanacak.</span><span class="sxs-lookup"><span data-stu-id="21c69-176">The battery can report **FAILED** when it simply needs to be charged.</span></span>


<span data-ttu-id="21c69-177">Varsa **DEGRADED** durumu görünür, eylem aşağıdaki seyri öneririz:</span><span class="sxs-lookup"><span data-stu-id="21c69-177">If the **DEGRADED** state appears, we recommend the following course of action:</span></span>

* <span data-ttu-id="21c69-178">Sistem son güç kaybı karşılaşmış veya piller düzenli bakım altında.</span><span class="sxs-lookup"><span data-stu-id="21c69-178">The system may have experienced a recent power loss or the batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="21c69-179">Devam etmeden önce 12 saat sistem gözlemleyin.</span><span class="sxs-lookup"><span data-stu-id="21c69-179">Observe the system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="21c69-180">Durum hala ise **DEGRADED** AC sürekli bağlantı 12 saatlik denetleyicileri ve çalışan PCMs ile güç sonra sonra pil değiştirilmesi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="21c69-180">If the state is still **DEGRADED** after 12 hours of continuous connection to AC power with the controllers and PCMs running, then the battery needs to be replaced.</span></span> <span data-ttu-id="21c69-181">Lütfen [Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md) yedek yedek pil modülü için.</span><span class="sxs-lookup"><span data-stu-id="21c69-181">Please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="21c69-182">Durumu Tamam 12 saat sonra olursa, pil işlevseldir ve yalnızca bir bakım ücret gereklidir.</span><span class="sxs-lookup"><span data-stu-id="21c69-182">If the state becomes OK after 12 hours, the battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="21c69-183">Ayrıca bir ilişkili AC güç kaybı değil açıldı ve PCM açık ve AC güç kaynağına bağlı, pil değiştirilmesi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="21c69-183">If there has not been an associated loss of AC power and the PCM is turned on and connected to AC power, the battery needs to be replaced.</span></span> <span data-ttu-id="21c69-184">[Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md) bir yedek yedek pil modül sıralamak için.</span><span class="sxs-lookup"><span data-stu-id="21c69-184">[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) to order a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21c69-185">Ulusal ve bölgesel düzenlemeleri göre başarısız pil Dispose.</span><span class="sxs-lookup"><span data-stu-id="21c69-185">Dispose of the failed battery according to national and regional regulations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21c69-186">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="21c69-186">Next steps</span></span>
<span data-ttu-id="21c69-187">Daha fazla bilgi edinmek [StorSimple donanım bileşeni değiştirme](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="21c69-187">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

