---
title: "aaaReplace StorSimple 8000 serisi aygıtınızda PCM | Microsoft Docs"
description: "Nasıl güç ve soğutma Modülü (PCM), StorSimple Cihazınızda tooremove ve Değiştir hello açıklar"
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
ms.date: 06/02/2017
ms.author: alkohli
ms.openlocfilehash: 474fd09787c5361a81efda4de74356027ac60f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a><span data-ttu-id="f0f95-103">StorSimple Cihazınızda güç ve soğutma modülü değiştirin</span><span class="sxs-lookup"><span data-stu-id="f0f95-103">Replace a Power and Cooling Module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="f0f95-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f0f95-104">Overview</span></span>
<span data-ttu-id="f0f95-105">Merhaba güç ve soğutma Modülü (PCM) Microsoft Azure StorSimple Cihazınızı içinde oluşan bir güç ve soğutma fanları hello birincil ve ebod denetlenir.</span><span class="sxs-lookup"><span data-stu-id="f0f95-105">hello Power and Cooling Module (PCM) in your Microsoft Azure StorSimple device consists of a power supply and cooling fans that are controlled through hello primary and EBOD enclosures.</span></span> <span data-ttu-id="f0f95-106">Her kasa için sertifikalı PCM, yalnızca bir model yok.</span><span class="sxs-lookup"><span data-stu-id="f0f95-106">There is only one model of PCM that is certified for each enclosure.</span></span> <span data-ttu-id="f0f95-107">Merhaba birincil muhafaza 764 W PCM için sertifikalı ve hello EBOD muhafazası 580 W PCM için sertifikalıdır.</span><span class="sxs-lookup"><span data-stu-id="f0f95-107">hello primary enclosure is certified for a 764 W PCM and hello EBOD enclosure is certified for a 580 W PCM.</span></span> <span data-ttu-id="f0f95-108">Merhaba PCMs hello birincil muhafaza ve hello EBOD muhafazası farklı olsa da hello değiştirme yordamı aynıdır.</span><span class="sxs-lookup"><span data-stu-id="f0f95-108">Although hello PCMs for hello primary enclosure and hello EBOD enclosure are different, hello replacement procedure is identical.</span></span>

<span data-ttu-id="f0f95-109">Bu öğretici açıklar nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="f0f95-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="f0f95-110">Bir PCM Kaldır</span><span class="sxs-lookup"><span data-stu-id="f0f95-110">Remove a PCM</span></span>
* <span data-ttu-id="f0f95-111">PCM yenisini yükleyin</span><span class="sxs-lookup"><span data-stu-id="f0f95-111">Install a replacement PCM</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f0f95-112">Kaldırma ve bir PCM değiştirme gözden önce hello güvenlik bilgileri [StorSimple donanım bileşeni değiştirme](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="f0f95-112">Before removing and replacing a PCM, review hello safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="before-you-replace-a-pcm"></a><span data-ttu-id="f0f95-113">Bir PCM değiştirmeden önce</span><span class="sxs-lookup"><span data-stu-id="f0f95-113">Before you replace a PCM</span></span>
<span data-ttu-id="f0f95-114">Önemli sorunları, PCM değiştirmeden önce aşağıdaki Merhaba dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="f0f95-114">Be aware of hello following important issues before you replace your PCM:</span></span>

* <span data-ttu-id="f0f95-115">Merhaba güç, sağlarsanız PCM başarısız olursa hello hello hatalı modül yüklü bırakır, ancak hello güç kablosu kaldırın.</span><span class="sxs-lookup"><span data-stu-id="f0f95-115">If hello power supply of hello PCM fails, leave hello faulty module installed, but remove hello power cord.</span></span> <span data-ttu-id="f0f95-116">Merhaba fan hello muhafaza tooreceive gücünden devam ve tooprovide uygun soğutma devam edin.</span><span class="sxs-lookup"><span data-stu-id="f0f95-116">hello fan will continue tooreceive power from hello enclosure and continue tooprovide proper cooling.</span></span> <span data-ttu-id="f0f95-117">Merhaba fan başarısız olursa, hello PCM hemen yerini toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0f95-117">If hello fan fails, hello PCM needs toobe replaced immediately.</span></span>
* <span data-ttu-id="f0f95-118">Merhaba PCM kaldırmadan önce hello güç PCM hello hello ana anahtarı (var olduğunda) kapatarak veya fiziksel olarak hello güç kablosu kaldırarak bağlantısını kesin.</span><span class="sxs-lookup"><span data-stu-id="f0f95-118">Before removing hello PCM, disconnect hello power from hello PCM by turning off hello main switch (where present) or by physically removing hello power cord.</span></span> <span data-ttu-id="f0f95-119">Bu güç kapatma uyaran bir uyarı tooyour sistemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="f0f95-119">This provides a warning tooyour system that a power shutdown is imminent.</span></span>
* <span data-ttu-id="f0f95-120">Değiştirme hello önce hatalı PCM emin olun için diğer PCM işlevseldir bu hello sistem işlemi devam eder.</span><span class="sxs-lookup"><span data-stu-id="f0f95-120">Make sure that hello other PCM is functional for continued system operation before replacing hello faulty PCM.</span></span> <span data-ttu-id="f0f95-121">Hatalı PCM tarafından tam olarak işlevsel bir PCM mümkün olan en kısa sürede değiştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="f0f95-121">A faulty PCM must be replaced by a fully operational PCM as soon as possible.</span></span>
* <span data-ttu-id="f0f95-122">Yalnızca birkaç dakika toocomplete PCM modülü değiştirme alır, ancak başarısız hello PCM tooprevent aşırı kaldırmanın 10 dakika içinde tamamlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0f95-122">PCM module replacement takes only few minutes toocomplete, but it must be completed within 10 minutes of removing hello failed PCM tooprevent overheating.</span></span>
* <span data-ttu-id="f0f95-123">Not Hello fabrikası'ndan sevk hello değiştirme 764 W PCM modülleri hello yedek pil modülü içermez.</span><span class="sxs-lookup"><span data-stu-id="f0f95-123">Note that hello replacement 764 W PCM modules shipped from hello factory do not contain hello backup battery module.</span></span> <span data-ttu-id="f0f95-124">Hatalı PCM'den tooremove hello pil gerekir ve hello değiştirme modülü önceki tooperforming hello değiştirme yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="f0f95-124">You will need tooremove hello battery from your faulty PCM and then insert it into hello replacement module prior tooperforming hello replacement.</span></span> <span data-ttu-id="f0f95-125">Daha fazla bilgi için bkz. nasıl çok[kaldırın ve bir yedek pil Modül Ekle](storsimple-8000-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="f0f95-125">For more information, see how too[remove and insert a backup battery module](storsimple-8000-battery-replacement.md).</span></span>

## <a name="remove-a-pcm"></a><span data-ttu-id="f0f95-126">Bir PCM Kaldır</span><span class="sxs-lookup"><span data-stu-id="f0f95-126">Remove a PCM</span></span>
<span data-ttu-id="f0f95-127">Microsoft Azure StorSimple Cihazınızı hazır tooremove güç ve soğutma Modülü (PCM) olduğunda bu yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="f0f95-127">Follow these instructions when you are ready tooremove a Power and Cooling Module (PCM) from your Microsoft Azure StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="f0f95-128">PCM kaldırmadan önce doğru değiştirme (764 W hello birincil kasası için) veya 580 W hello EBOD muhafazası için sahip olduğunuzu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f0f95-128">Before you remove your PCM, verify that you have a correct replacement (764 W for hello primary enclosure or 580 W for hello EBOD enclosure).</span></span>

#### <a name="tooremove-a-pcm"></a><span data-ttu-id="f0f95-129">tooremove bir PCM</span><span class="sxs-lookup"><span data-stu-id="f0f95-129">tooremove a PCM</span></span>
1. <span data-ttu-id="f0f95-130">Hello Klasik Azure portalı, tıklatın **ayarlar > İzleyici > donanım durumu**.</span><span class="sxs-lookup"><span data-stu-id="f0f95-130">In hello Azure classic portal, click **Settings > Monitor > Hardware health**.</span></span> <span data-ttu-id="f0f95-131">Merhaba altındaki hello PCM bileşenlerinin durumunu denetleme **paylaşılan bileşenleri** PCM başarısız oldu tooidentify:</span><span class="sxs-lookup"><span data-stu-id="f0f95-131">Check hello status of hello PCM components under **Shared components** tooidentify which PCM has failed:</span></span>
   
   * <span data-ttu-id="f0f95-132">Güç kaynağı PCM 0 olarak başarısız olursa, durumunu hello **güç kaynağı PCM 0'ın** kırmızı olur.</span><span class="sxs-lookup"><span data-stu-id="f0f95-132">If a power supply in PCM 0 has failed, hello status of **Power Supply in PCM 0** will be red.</span></span>
   * <span data-ttu-id="f0f95-133">Güç kaynağı PCM 1'de başarısız olursa, durumunu hello **güç kaynağı PCM 1** kırmızı olur.</span><span class="sxs-lookup"><span data-stu-id="f0f95-133">If a power supply in PCM 1 has failed, hello status of **Power Supply in PCM 1** will be red.</span></span>
   * <span data-ttu-id="f0f95-134">Merhaba fan PCM 1'de başarısız olursa, ya da durumunu hello **PCM 0 0 soğutma** veya **PCM 0 için 1 soğutma** kırmızı olur.</span><span class="sxs-lookup"><span data-stu-id="f0f95-134">If hello fan in PCM 1 has failed, hello status of either **Cooling 0 for PCM 0** or **Cooling 1 for PCM 0** will be red.</span></span>
2. <span data-ttu-id="f0f95-135">Merhaba üzerinde başarısız PCM geri hello birincil kasası hello bulun.</span><span class="sxs-lookup"><span data-stu-id="f0f95-135">Locate hello failed PCM on hello back of hello primary enclosure.</span></span> <span data-ttu-id="f0f95-136">8600 model çalıştırıyorsanız, hello birincil muhafaza hello sistem birimi kimlik numarası hello ön panelini LED ekranda gösterilen bakarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="f0f95-136">If you are running an 8600 model, identify hello primary enclosure by looking at hello System Unit Identification Number shown on hello front panel LED display.</span></span> <span data-ttu-id="f0f95-137">Merhaba birimi hello birincil muhafaza görüntülenen kimliği varsayılan **00**, birim kimliği görüntülenen EBOD muhafazası hello üzerinde hello varsayılan iken **01**.</span><span class="sxs-lookup"><span data-stu-id="f0f95-137">hello default Unit ID displayed on hello primary enclosure is **00**, whereas hello default Unit ID displayed on hello EBOD enclosure is **01**.</span></span> <span data-ttu-id="f0f95-138">Merhaba Aşağıdaki diyagramda ve tablo hello ön panelini hello LED görüntüsünün açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f0f95-138">hello following diagram and table explain hello front panel of hello LED display.</span></span>
   
    ![Ön OPS panelindeki sistem kimliği](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     <span data-ttu-id="f0f95-140">**Şekil 1** hello aygıt ön panelini</span><span class="sxs-lookup"><span data-stu-id="f0f95-140">**Figure 1** Front panel of hello device</span></span>  
   
   | <span data-ttu-id="f0f95-141">Etiket</span><span class="sxs-lookup"><span data-stu-id="f0f95-141">Label</span></span> | <span data-ttu-id="f0f95-142">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0f95-142">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="f0f95-143">1</span><span class="sxs-lookup"><span data-stu-id="f0f95-143">1</span></span> |<span data-ttu-id="f0f95-144">Sessiz düğmesi</span><span class="sxs-lookup"><span data-stu-id="f0f95-144">Mute button</span></span> |
   | <span data-ttu-id="f0f95-145">2</span><span class="sxs-lookup"><span data-stu-id="f0f95-145">2</span></span> |<span data-ttu-id="f0f95-146">Sistem gücü</span><span class="sxs-lookup"><span data-stu-id="f0f95-146">System power</span></span> |
   | <span data-ttu-id="f0f95-147">3</span><span class="sxs-lookup"><span data-stu-id="f0f95-147">3</span></span> |<span data-ttu-id="f0f95-148">Modül hatası</span><span class="sxs-lookup"><span data-stu-id="f0f95-148">Module fault</span></span> |
   | <span data-ttu-id="f0f95-149">4</span><span class="sxs-lookup"><span data-stu-id="f0f95-149">4</span></span> |<span data-ttu-id="f0f95-150">Mantıksal hatası</span><span class="sxs-lookup"><span data-stu-id="f0f95-150">Logical fault</span></span> |
   | <span data-ttu-id="f0f95-151">5</span><span class="sxs-lookup"><span data-stu-id="f0f95-151">5</span></span> |<span data-ttu-id="f0f95-152">Birim kimliği görüntüleme</span><span class="sxs-lookup"><span data-stu-id="f0f95-152">Unit ID display</span></span> |
3. <span data-ttu-id="f0f95-153">Merhaba birincil muhafaza arkasına hello gösterge LED'lerinin İzleme hello de kullanılabilir tooidentify hello hatalı PCM.</span><span class="sxs-lookup"><span data-stu-id="f0f95-153">hello monitoring indicator LEDs in hello back of hello primary enclosure can also be used tooidentify hello faulty PCM.</span></span> <span data-ttu-id="f0f95-154">Diyagram ve toounderstand nasıl tablo hello aşağıdakilere bakın toouse hello LED'leri toolocate hello hatalı PCM.</span><span class="sxs-lookup"><span data-stu-id="f0f95-154">See hello following diagram and table toounderstand how toouse hello LEDs toolocate hello faulty PCM.</span></span> <span data-ttu-id="f0f95-155">Örneğin, karşılık gelen toohello hello varsa neden **Fan başarısız** olan aydınlatma, hello fan başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="f0f95-155">For example, if hello LED corresponding toohello **Fan Fail** is lit, hello fan has failed.</span></span> <span data-ttu-id="f0f95-156">Merhaba, karşılık gelen çok benzer şekilde, neden**AC başarısız** olan aydınlatma, hello güç kaynağı başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="f0f95-156">Likewise, if hello LED corresponding too**AC Fail** is lit, hello power supply has failed.</span></span> 
   
    ![Cihaz PCM izleme gösterge LED'leri devre kartı](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     <span data-ttu-id="f0f95-158">**Şekil 2** geri of PCM LED'leri göstergesi</span><span class="sxs-lookup"><span data-stu-id="f0f95-158">**Figure 2** Back of PCM with indicator LEDs</span></span>
   
   | <span data-ttu-id="f0f95-159">Etiket</span><span class="sxs-lookup"><span data-stu-id="f0f95-159">Label</span></span> | <span data-ttu-id="f0f95-160">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0f95-160">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="f0f95-161">1</span><span class="sxs-lookup"><span data-stu-id="f0f95-161">1</span></span> |<span data-ttu-id="f0f95-162">AC güç kesintisi</span><span class="sxs-lookup"><span data-stu-id="f0f95-162">AC power failure</span></span> |
   | <span data-ttu-id="f0f95-163">2</span><span class="sxs-lookup"><span data-stu-id="f0f95-163">2</span></span> |<span data-ttu-id="f0f95-164">Fan hatası</span><span class="sxs-lookup"><span data-stu-id="f0f95-164">Fan failure</span></span> |
   | <span data-ttu-id="f0f95-165">3</span><span class="sxs-lookup"><span data-stu-id="f0f95-165">3</span></span> |<span data-ttu-id="f0f95-166">Pil hatası</span><span class="sxs-lookup"><span data-stu-id="f0f95-166">Battery fault</span></span> |
   | <span data-ttu-id="f0f95-167">4</span><span class="sxs-lookup"><span data-stu-id="f0f95-167">4</span></span> |<span data-ttu-id="f0f95-168">PCM TAMAM</span><span class="sxs-lookup"><span data-stu-id="f0f95-168">PCM OK</span></span> |
   | <span data-ttu-id="f0f95-169">5</span><span class="sxs-lookup"><span data-stu-id="f0f95-169">5</span></span> |<span data-ttu-id="f0f95-170">DC Güç kesintisi</span><span class="sxs-lookup"><span data-stu-id="f0f95-170">DC power failure</span></span> |
   | <span data-ttu-id="f0f95-171">6</span><span class="sxs-lookup"><span data-stu-id="f0f95-171">6</span></span> |<span data-ttu-id="f0f95-172">Sağlıklı pil</span><span class="sxs-lookup"><span data-stu-id="f0f95-172">Battery healthy</span></span> |
4. <span data-ttu-id="f0f95-173">Merhaba StorSimple cihaz toolocate başarısız hello PCM modülü arkasına hello diyagramı aşağıdaki toohello bakın.</span><span class="sxs-lookup"><span data-stu-id="f0f95-173">Refer toohello following diagram of hello back of hello StorSimple device toolocate hello failed PCM module.</span></span> <span data-ttu-id="f0f95-174">PCM 0 hello solda ve PCM 1 hello doğru.</span><span class="sxs-lookup"><span data-stu-id="f0f95-174">PCM 0 is on hello left and PCM 1 is on hello right.</span></span> <span data-ttu-id="f0f95-175">izleyen hello tablo hello modülleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="f0f95-175">hello table that follows explains hello modules.</span></span>
   
     ![Aygıt birincil muhafaza modüllerinin devre kartı](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     <span data-ttu-id="f0f95-177">**Şekil 3** eklenti modülleri aygıtla arkasına</span><span class="sxs-lookup"><span data-stu-id="f0f95-177">**Figure 3** Back of device with plug-in modules</span></span> 
   
   | <span data-ttu-id="f0f95-178">Etiket</span><span class="sxs-lookup"><span data-stu-id="f0f95-178">Label</span></span> | <span data-ttu-id="f0f95-179">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0f95-179">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="f0f95-180">1</span><span class="sxs-lookup"><span data-stu-id="f0f95-180">1</span></span> |<span data-ttu-id="f0f95-181">PCM 0</span><span class="sxs-lookup"><span data-stu-id="f0f95-181">PCM 0</span></span> |
   | <span data-ttu-id="f0f95-182">2</span><span class="sxs-lookup"><span data-stu-id="f0f95-182">2</span></span> |<span data-ttu-id="f0f95-183">PCM 1</span><span class="sxs-lookup"><span data-stu-id="f0f95-183">PCM 1</span></span> |
   | <span data-ttu-id="f0f95-184">3</span><span class="sxs-lookup"><span data-stu-id="f0f95-184">3</span></span> |<span data-ttu-id="f0f95-185">Denetleyici 0</span><span class="sxs-lookup"><span data-stu-id="f0f95-185">Controller 0</span></span> |
   | <span data-ttu-id="f0f95-186">4</span><span class="sxs-lookup"><span data-stu-id="f0f95-186">4</span></span> |<span data-ttu-id="f0f95-187">Denetleyici 1</span><span class="sxs-lookup"><span data-stu-id="f0f95-187">Controller 1</span></span> |
5. <span data-ttu-id="f0f95-188">Kapatma kapalı hatalı PCM hello ve hello güç kaynağı kablosunun bağlantısını kesin.</span><span class="sxs-lookup"><span data-stu-id="f0f95-188">Turn off hello faulty PCM and disconnect hello power supply cord.</span></span> <span data-ttu-id="f0f95-189">Merhaba PCM şimdi kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f0f95-189">You can now remove hello PCM.</span></span>
6. <span data-ttu-id="f0f95-190">Merhaba Mandal ve PCM işlemek, Flash ve erişebildiğinizden arasında hello hello tarafında kavramak ve birlikte tooopen hello tanıtıcı sığdırması.</span><span class="sxs-lookup"><span data-stu-id="f0f95-190">Grasp hello latch and hello side of hello PCM handle between your thumb and forefinger, and squeeze them together tooopen hello handle.</span></span>
   
    ![PCM tanıtıcısı açılıyor](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    <span data-ttu-id="f0f95-192">**Şekil 4** açılış hello PCM işleme</span><span class="sxs-lookup"><span data-stu-id="f0f95-192">**Figure 4** Opening hello PCM handle</span></span>
7. <span data-ttu-id="f0f95-193">Tutamacı hello işlemek ve hello PCM kaldırın.</span><span class="sxs-lookup"><span data-stu-id="f0f95-193">Grip hello handle and remove hello PCM.</span></span>
   
    ![Cihaz PCM'i kaldırılıyor](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    <span data-ttu-id="f0f95-195">**Şekil 5** kaldırma hello PCM</span><span class="sxs-lookup"><span data-stu-id="f0f95-195">**Figure 5** Removing hello PCM</span></span>

## <a name="install-a-replacement-pcm"></a><span data-ttu-id="f0f95-196">PCM yenisini yükleyin</span><span class="sxs-lookup"><span data-stu-id="f0f95-196">Install a replacement PCM</span></span>
<span data-ttu-id="f0f95-197">Bu yönergeler tooinstall PCM StorSimple Cihazınızı içinde izleyin.</span><span class="sxs-lookup"><span data-stu-id="f0f95-197">Follow these instructions tooinstall a PCM in your StorSimple device.</span></span> <span data-ttu-id="f0f95-198">Merhaba yedek pil modülü önceki tooinstalling hello değiştirme (yalnızca W PCMs too764 geçerlidir) PCM eklediğiniz emin olun.</span><span class="sxs-lookup"><span data-stu-id="f0f95-198">Ensure that you have inserted hello backup battery module prior tooinstalling hello replacement PCM (applies too764 W PCMs only).</span></span> <span data-ttu-id="f0f95-199">Daha fazla bilgi için bkz. nasıl çok[kaldırın ve bir yedek pil Modül Ekle](storsimple-8000-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="f0f95-199">For more information, see how too[remove and insert a backup battery module](storsimple-8000-battery-replacement.md).</span></span>

#### <a name="tooinstall-a-pcm"></a><span data-ttu-id="f0f95-200">tooinstall bir PCM</span><span class="sxs-lookup"><span data-stu-id="f0f95-200">tooinstall a PCM</span></span>
1. <span data-ttu-id="f0f95-201">Bu kutu için hello doğru değiştirme PCM sahip olduğunuzu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f0f95-201">Verify that you have hello correct replacement PCM for this enclosure.</span></span> <span data-ttu-id="f0f95-202">764 W PCM Hello birincil muhafaza gerekir ve hello EBOD muhafazası 580 W PCM gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="f0f95-202">hello primary enclosure needs a 764 W PCM and hello EBOD enclosure needs a 580 W PCM.</span></span> <span data-ttu-id="f0f95-203">Toouse çalışmamalısınız hello birincil muhafazada 580 W PCM hello veya hello EBOD muhafazası içinde 764 W PCM hello.</span><span class="sxs-lookup"><span data-stu-id="f0f95-203">You should not attempt toouse hello 580 W PCM in hello Primary enclosure, or hello 764 W PCM in hello EBOD enclosure.</span></span> <span data-ttu-id="f0f95-204">Görüntü aşağıdaki hello burada hello bu bilgileri etiket yani tooidentify toohello PCM yapıştırılmış gösterir.</span><span class="sxs-lookup"><span data-stu-id="f0f95-204">hello following image shows where tooidentify this information on hello label that is affixed toohello PCM.</span></span>
   
    ![Cihaz PCM etiketi](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    <span data-ttu-id="f0f95-206">**Şekil 6** PCM etiketi</span><span class="sxs-lookup"><span data-stu-id="f0f95-206">**Figure 6** PCM label</span></span>
2. <span data-ttu-id="f0f95-207">Özellikle dikkat toohello bağlayıcılar ödeme zarar toohello kasası için denetleyin.</span><span class="sxs-lookup"><span data-stu-id="f0f95-207">Check for damage toohello enclosure, paying particular attention toohello connectors.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="f0f95-208">**Tüm bağlayıcı PIN'ler Bükülü hello modülü yüklemeyin.**</span><span class="sxs-lookup"><span data-stu-id="f0f95-208">**Do not install hello module if any connector pins are bent.**</span></span>
   > 
   > 
3. <span data-ttu-id="f0f95-209">PCM işlemek hello hello konumu, slayt hello hello muhafaza modüle açın.</span><span class="sxs-lookup"><span data-stu-id="f0f95-209">With hello PCM handle in hello open position, slide hello module into hello enclosure.</span></span>
   
    ![Cihaz PCM'i yükleniyor](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    <span data-ttu-id="f0f95-211">**Şekil 7** yükleme hello PCM</span><span class="sxs-lookup"><span data-stu-id="f0f95-211">**Figure 7** Installing hello PCM</span></span>
4. <span data-ttu-id="f0f95-212">Merhaba PCM tanıtıcısı el ile kapatın.</span><span class="sxs-lookup"><span data-stu-id="f0f95-212">Manually close hello PCM handle.</span></span> <span data-ttu-id="f0f95-213">Merhaba tanıtıcı Mandal prosese gibi bir tıklama sesi.</span><span class="sxs-lookup"><span data-stu-id="f0f95-213">You should hear a click as hello handle latch engages.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f0f95-214">Bağlayıcı PIN'ler hello tooensure gerçekleştiriliyor, hello tutamacı hello mandalı bırakılıyor olmadan hafifçe tug.</span><span class="sxs-lookup"><span data-stu-id="f0f95-214">tooensure that hello connector pins have engaged, you can gently tug on hello handle without releasing hello latch.</span></span> <span data-ttu-id="f0f95-215">Out Hello PCM slayt, hello bağlayıcılar gerçekleştiriliyor önce o hello Mandal kapatıldı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="f0f95-215">If hello PCM slides out, it implies that hello latch was closed before hello connectors engaged.</span></span>
   
5. <span data-ttu-id="f0f95-216">Merhaba güç kabloları toohello güç kaynağı ve toohello PCM bağlayın.</span><span class="sxs-lookup"><span data-stu-id="f0f95-216">Connect hello power cables toohello power source and toohello PCM.</span></span>
6. <span data-ttu-id="f0f95-217">Merhaba yükü Tahliye bales güvenli hale getirin.</span><span class="sxs-lookup"><span data-stu-id="f0f95-217">Secure hello strain relief bales.</span></span>
7. <span data-ttu-id="f0f95-218">PCM Hello üzerinde etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f0f95-218">Turn on hello PCM.</span></span>
8. <span data-ttu-id="f0f95-219">Hello değiştirme işleminin başarılı olduğunu doğrulayın: hello StorSimple Aygıt Yöneticisi'ni hizmetinizin Azure portal, tooyour aygıt gidin ve ardından çok**Ayarları > İzleyici > donanım durumu**.</span><span class="sxs-lookup"><span data-stu-id="f0f95-219">Verify that hello replacement was successful: in hello Azure portal of your StorSimple Device Manager service, navigate tooyour device and then too**Settings > Monitor > Hardware health**.</span></span> <span data-ttu-id="f0f95-220">Merhaba altında **paylaşılan bileşenleri**, hello PCM hello durumu yeşil.</span><span class="sxs-lookup"><span data-stu-id="f0f95-220">Under hello **Shared components**, hello status of hello PCM should be green.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f0f95-221">Merhaba değiştirme PCM toocompletely başlatma için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="f0f95-221">It may take a few minutes for hello replacement PCM toocompletely initialize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0f95-222">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f0f95-222">Next steps</span></span>
<span data-ttu-id="f0f95-223">Daha fazla bilgi edinmek [StorSimple donanım bileşeni değiştirme](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="f0f95-223">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

