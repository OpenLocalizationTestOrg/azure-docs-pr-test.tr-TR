---
title: "Microsoft Azure StorSimple cihaz pilde Değiştir | Microsoft Docs"
description: "Kaldırmak için değiştirin ve StorSimple Cihazınızda yedek pil modülü korumak açıklar."
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
ms.openlocfilehash: f8b89b3f6851ec9ee0570f551b5407419fdba2d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="replace-the-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="7700d-103">StorSimple Cihazınızda yedek pil modülü değiştirin</span><span class="sxs-lookup"><span data-stu-id="7700d-103">Replace the backup battery module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="7700d-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="7700d-104">Overview</span></span>
<span data-ttu-id="7700d-105">Birincil muhafaza güç ve soğutma Modülü (PCM), Microsoft Azure StorSimple Cihazınızda bir ek pil paketi vardır.</span><span class="sxs-lookup"><span data-stu-id="7700d-105">The primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="7700d-106">Bu paketi güç sunar, böylece birincil kasası AC güç kaybı ise StorSimple cihazı veri kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7700d-106">This pack provides power so that the StorSimple device can save data if there is loss of AC power to the primary enclosure.</span></span> <span data-ttu-id="7700d-107">Bu pil paketi olarak adlandırılır *yedek pil Modülü*.</span><span class="sxs-lookup"><span data-stu-id="7700d-107">This battery pack is referred to as the *backup battery module*.</span></span> <span data-ttu-id="7700d-108">Yedek pil modülü yalnızca StorSimple Cihazınızı (EBOD muhafazası bir yedek pil modül içermiyor) birincil muhafazada yok.</span><span class="sxs-lookup"><span data-stu-id="7700d-108">The backup battery module exists only for the primary enclosure in your StorSimple device (the EBOD enclosure does not contain a backup battery module).</span></span> 

<span data-ttu-id="7700d-109">Bu öğretici açıklar nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="7700d-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="7700d-110">Yedek pil modülünü Kaldır</span><span class="sxs-lookup"><span data-stu-id="7700d-110">Remove the backup battery module</span></span> 
* <span data-ttu-id="7700d-111">Yeni bir yedek pil modülünü yükleme</span><span class="sxs-lookup"><span data-stu-id="7700d-111">Install a new backup battery module</span></span>
* <span data-ttu-id="7700d-112">Yedek pil modülü koru</span><span class="sxs-lookup"><span data-stu-id="7700d-112">Maintain the backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7700d-113">Kaldırma ve bir yedek pil modül değiştirme gözden önce güvenlik bilgileri [StorSimple donanım bileşeni değiştirme giriş](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="7700d-113">Before removing and replacing a backup battery module, review the safety information in the [Introduction to StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-the-backup-battery-module"></a><span data-ttu-id="7700d-114">Yedek pil modülünü Kaldır</span><span class="sxs-lookup"><span data-stu-id="7700d-114">Remove the backup battery module</span></span>
<span data-ttu-id="7700d-115">Bir alan değiştirebilen birim StorSimple cihazınız için yedek pil modülüdür.</span><span class="sxs-lookup"><span data-stu-id="7700d-115">The backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="7700d-116">PCM yüklenmeden önce pil modülü kendi özgün paketleme depolanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7700d-116">Before it is installed in the PCM, the battery module should be stored in its original packaging.</span></span> <span data-ttu-id="7700d-117">Yedek pil kaldırmak için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="7700d-117">Perform the following steps to remove the backup battery.</span></span>

#### <a name="to-remove-the-backup-battery-module"></a><span data-ttu-id="7700d-118">Yedek pil modülünü kaldırmak için</span><span class="sxs-lookup"><span data-stu-id="7700d-118">To remove the backup battery module</span></span>
1. <span data-ttu-id="7700d-119">Klasik Azure portalında Git **aygıtları** > **Bakım** > **donanım durum**.</span><span class="sxs-lookup"><span data-stu-id="7700d-119">In the Azure classic portal, go to **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="7700d-120">Altında **paylaşılan bileşenleri**, pil durum öğesine bakın.</span><span class="sxs-lookup"><span data-stu-id="7700d-120">Under **Shared Components**, look at the status of the battery.</span></span>
2. <span data-ttu-id="7700d-121">Pil başarısız oldu PCM tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="7700d-121">Identify the PCM in which the battery has failed.</span></span> <span data-ttu-id="7700d-122">Şekil 1, StorSimple cihazı arkası gösterir.</span><span class="sxs-lookup"><span data-stu-id="7700d-122">Figure 1 shows the back of the StorSimple device.</span></span>
   
    ![Aygıt birincil muhafaza modüllerinin devre kartı](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="7700d-124">**Şekil 1** PCM ve denetleyici modülleri gösteren birincil cihaz arkasına</span><span class="sxs-lookup"><span data-stu-id="7700d-124">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="7700d-125">Etiket</span><span class="sxs-lookup"><span data-stu-id="7700d-125">Label</span></span> | <span data-ttu-id="7700d-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7700d-126">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="7700d-127">1</span><span class="sxs-lookup"><span data-stu-id="7700d-127">1</span></span> |<span data-ttu-id="7700d-128">PCM 0</span><span class="sxs-lookup"><span data-stu-id="7700d-128">PCM 0</span></span> |
   | <span data-ttu-id="7700d-129">2</span><span class="sxs-lookup"><span data-stu-id="7700d-129">2</span></span> |<span data-ttu-id="7700d-130">PCM 1</span><span class="sxs-lookup"><span data-stu-id="7700d-130">PCM 1</span></span> |
   | <span data-ttu-id="7700d-131">3</span><span class="sxs-lookup"><span data-stu-id="7700d-131">3</span></span> |<span data-ttu-id="7700d-132">Denetleyici 0</span><span class="sxs-lookup"><span data-stu-id="7700d-132">Controller 0</span></span> |
   | <span data-ttu-id="7700d-133">4</span><span class="sxs-lookup"><span data-stu-id="7700d-133">4</span></span> |<span data-ttu-id="7700d-134">Denetleyici 1</span><span class="sxs-lookup"><span data-stu-id="7700d-134">Controller 1</span></span> |
   
    <span data-ttu-id="7700d-135">Sayı 3 Şekil 2'de gösterildiği gibi izleme gösterge ÖNCÜLÜK karşılık gelen PCM 0 üzerinde **pil hataya** aydınlatma.</span><span class="sxs-lookup"><span data-stu-id="7700d-135">As shown by number 3 in the Figure 2, the monitoring indicator LED on PCM 0 that corresponds to **Battery Fault** should be lit.</span></span>
   
    ![Cihaz PCM izleme gösterge LED'lerinin devre kartı](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="7700d-137">**Şekil 2** geri of PCM izleme gösterge LED'leri gösterme</span><span class="sxs-lookup"><span data-stu-id="7700d-137">**Figure 2** Back of PCM showing the monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="7700d-138">Etiket</span><span class="sxs-lookup"><span data-stu-id="7700d-138">Label</span></span> | <span data-ttu-id="7700d-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7700d-139">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="7700d-140">1</span><span class="sxs-lookup"><span data-stu-id="7700d-140">1</span></span> |<span data-ttu-id="7700d-141">AC güç kesintisi</span><span class="sxs-lookup"><span data-stu-id="7700d-141">AC power failure</span></span> |
   | <span data-ttu-id="7700d-142">2</span><span class="sxs-lookup"><span data-stu-id="7700d-142">2</span></span> |<span data-ttu-id="7700d-143">Fan hatası</span><span class="sxs-lookup"><span data-stu-id="7700d-143">Fan failure</span></span> |
   | <span data-ttu-id="7700d-144">3</span><span class="sxs-lookup"><span data-stu-id="7700d-144">3</span></span> |<span data-ttu-id="7700d-145">Pil hatası</span><span class="sxs-lookup"><span data-stu-id="7700d-145">Battery fault</span></span> |
   | <span data-ttu-id="7700d-146">4</span><span class="sxs-lookup"><span data-stu-id="7700d-146">4</span></span> |<span data-ttu-id="7700d-147">PCM TAMAM</span><span class="sxs-lookup"><span data-stu-id="7700d-147">PCM OK</span></span> |
   | <span data-ttu-id="7700d-148">5</span><span class="sxs-lookup"><span data-stu-id="7700d-148">5</span></span> |<span data-ttu-id="7700d-149">DC Güç kesintisi</span><span class="sxs-lookup"><span data-stu-id="7700d-149">DC power failure</span></span> |
   | <span data-ttu-id="7700d-150">6</span><span class="sxs-lookup"><span data-stu-id="7700d-150">6</span></span> |<span data-ttu-id="7700d-151">Sağlıklı pil</span><span class="sxs-lookup"><span data-stu-id="7700d-151">Battery healthy</span></span> |
3. <span data-ttu-id="7700d-152">Başarısız pille PCM kaldırmak için adımları [bir PCM kaldırmak](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span><span class="sxs-lookup"><span data-stu-id="7700d-152">To remove the PCM with a failed battery, follow the steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="7700d-153">Kaldırılan PCM ile kaldırın ve aşağıdaki çizimde gösterildiği gibi pil modül işleyiciyi Yukarı Döndür ve pil Kaldır kadar çekme.</span><span class="sxs-lookup"><span data-stu-id="7700d-153">With the PCM removed, lift and rotate the battery module handle upward as indicated in the following figure, and pull it up to remove the battery.</span></span>
   
    ![PCM'den pil çıkarılıyor](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="7700d-155">**Şekil 3** PCM'den pil çıkarılıyor</span><span class="sxs-lookup"><span data-stu-id="7700d-155">**Figure 3** Removing the battery from the PCM</span></span>
5. <span data-ttu-id="7700d-156">Paketleme alan değiştirebilen birim modülünde yer.</span><span class="sxs-lookup"><span data-stu-id="7700d-156">Place the module in the field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="7700d-157">Arızalı ünite uygun Bakım ve işleme için Microsoft'a döndürür.</span><span class="sxs-lookup"><span data-stu-id="7700d-157">Return the defective unit to Microsoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="7700d-158">Yeni bir yedek pil modülünü yükleme</span><span class="sxs-lookup"><span data-stu-id="7700d-158">Install a new backup battery module</span></span>
<span data-ttu-id="7700d-159">StorSimple cihazınızın birincil muhafazada PCM değiştirme pil modülünü yüklemek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="7700d-159">Perform the following steps to install the replacement battery module in the PCM in the primary enclosure of your StorSimple device.</span></span>

#### <a name="to-install-the-battery-module"></a><span data-ttu-id="7700d-160">Pil modülünü yüklemek için</span><span class="sxs-lookup"><span data-stu-id="7700d-160">To install the battery module</span></span>
1. <span data-ttu-id="7700d-161">Yedek pil modülü PCM uygun yönde yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="7700d-161">Place the backup battery module in the proper orientation in the PCM.</span></span>
2. <span data-ttu-id="7700d-162">Bu süreç boyunca tüm bağlayıcı oturak için pil modül işleyiciyi basın.</span><span class="sxs-lookup"><span data-stu-id="7700d-162">Press down the battery module handle all the way to seat the connector.</span></span>
3. <span data-ttu-id="7700d-163">Yönergeleri izleyerek birincil muhafazada PCM Değiştir [güç ve soğutma modülü StorSimple Cihazınızda Değiştir](storsimple-power-cooling-module-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="7700d-163">Replace the PCM in the primary enclosure by following the guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="7700d-164">Bu değişiklik tamamlandıktan sonra Git **aygıtları** > **Bakım** > **donanım durum** Klasik Azure portalındaki.</span><span class="sxs-lookup"><span data-stu-id="7700d-164">After the replacement is complete, go to **Devices** > **Maintenance** > **Hardware Status** in the Azure classic portal.</span></span> <span data-ttu-id="7700d-165">Yüklemenin başarılı olduğunu emin olmak için pil durumunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="7700d-165">Verify the status of the battery to make sure that the installation was successful.</span></span> <span data-ttu-id="7700d-166">Yeşil durum pil sağlıklı olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="7700d-166">A green status indicates that the battery is healthy.</span></span>

## <a name="maintain-the-backup-battery-module"></a><span data-ttu-id="7700d-167">Yedek pil modülü koru</span><span class="sxs-lookup"><span data-stu-id="7700d-167">Maintain the backup battery module</span></span>
<span data-ttu-id="7700d-168">StorSimple Cihazınızı yedek pil modülü güç kaybı olayı sırasında denetleyiciye güç sağlar.</span><span class="sxs-lookup"><span data-stu-id="7700d-168">In your StorSimple device, the backup battery module provides power to the controller during a power loss event.</span></span> <span data-ttu-id="7700d-169">Denetimli bir biçimde kapatmadan önce kritik verileri kaydetmek StorSimple cihazı sağlar.</span><span class="sxs-lookup"><span data-stu-id="7700d-169">It allows the StorSimple device to save critical data prior to shutting down in a controlled manner.</span></span> <span data-ttu-id="7700d-170">İki tam dolu pilleri ile PCMs, iki ardışık kaybı olay sistem işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="7700d-170">With two fully charged batteries in the PCMs, the system can handle two consecutive loss events.</span></span>

<span data-ttu-id="7700d-171">Azure Klasik portalında **donanım durumu** üzerinde **Bakım** sayfa pil arızalı ya da son yaşam yaklaştığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="7700d-171">In the Azure classic portal, the **Hardware Status** on the **Maintenance** page indicates whether the battery is malfunctioning or the end-of-life is approaching.</span></span> <span data-ttu-id="7700d-172">Pil durumu belirtilir **PCM 0 pil** veya **pil PCM 1** altında **paylaşılan bileşenleri**.</span><span class="sxs-lookup"><span data-stu-id="7700d-172">The battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="7700d-173">Bu sayfada gösterilir bir **DEGRADED** ömrü sonu yaklaşan için durum ve **başarısız** ömrü son ulaştı.</span><span class="sxs-lookup"><span data-stu-id="7700d-173">This page will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span> 

> [!NOTE]
> <span data-ttu-id="7700d-174">Pil raporlayabilirsiniz **başarısız** , yalnızca gerektiği zaman uygulanacak.</span><span class="sxs-lookup"><span data-stu-id="7700d-174">The battery can report **FAILED** when it simply needs to be charged.</span></span>
> 
> 

<span data-ttu-id="7700d-175">Varsa **DEGRADED** durumu görünür, eylem aşağıdaki seyri öneririz:</span><span class="sxs-lookup"><span data-stu-id="7700d-175">If the **DEGRADED** state appears, we recommend the following course of action:</span></span>

* <span data-ttu-id="7700d-176">Sistem son güç kaybı karşılaşmış veya piller düzenli bakım altında.</span><span class="sxs-lookup"><span data-stu-id="7700d-176">The system may have experienced a recent power loss or the batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="7700d-177">Devam etmeden önce 12 saat sistem gözlemleyin.</span><span class="sxs-lookup"><span data-stu-id="7700d-177">Observe the system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="7700d-178">Durum hala ise **DEGRADED** AC sürekli bağlantı 12 saatlik denetleyicileri ve çalışan PCMs ile güç sonra sonra pil değiştirilmesi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="7700d-178">If the state is still **DEGRADED** after 12 hours of continuous connection to AC power with the controllers and PCMs running, then the battery needs to be replaced.</span></span> <span data-ttu-id="7700d-179">Lütfen [Microsoft Support başvurun](storsimple-contact-microsoft-support.md) yedek yedek pil modülü için.</span><span class="sxs-lookup"><span data-stu-id="7700d-179">Please [contact Microsoft Support](storsimple-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="7700d-180">Durumu Tamam 12 saat sonra olursa, pil işlevseldir ve yalnızca bir bakım ücret gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7700d-180">If the state becomes OK after 12 hours, the battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="7700d-181">Ayrıca bir ilişkili AC güç kaybı değil açıldı ve PCM açık ve AC güç kaynağına bağlı, pil değiştirilmesi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="7700d-181">If there has not been an associated loss of AC power and the PCM is turned on and connected to AC power, the battery needs to be replaced.</span></span> <span data-ttu-id="7700d-182">[Microsoft Support başvurun](storsimple-contact-microsoft-support.md) bir yedek yedek pil modül sıralamak için.</span><span class="sxs-lookup"><span data-stu-id="7700d-182">[Contact Microsoft Support](storsimple-contact-microsoft-support.md) to order a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7700d-183">Ulusal ve bölgesel düzenlemeleri göre başarısız pil Dispose.</span><span class="sxs-lookup"><span data-stu-id="7700d-183">Dispose of the failed battery according to national and regional regulations.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="7700d-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7700d-184">Next steps</span></span>
<span data-ttu-id="7700d-185">Daha fazla bilgi edinmek [StorSimple donanım bileşeni değiştirme](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="7700d-185">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

