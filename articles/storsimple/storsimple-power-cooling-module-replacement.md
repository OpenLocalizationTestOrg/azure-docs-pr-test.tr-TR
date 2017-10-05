---
title: "StorSimple Cihazınızda PCM Değiştir | Microsoft Docs"
description: "Kaldırdığınızda ve değiştirdiğinizde güç ve soğutma Modülü (PCM), StorSimple Cihazınızda açıklanmaktadır"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 24a158cb-0b79-4908-bb5a-431e48760f6a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: 2a956de58b279a013913631a077d7b03c6327f72
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a><span data-ttu-id="36781-103">StorSimple Cihazınızda güç ve soğutma modülü değiştirin</span><span class="sxs-lookup"><span data-stu-id="36781-103">Replace a Power and Cooling Module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="36781-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="36781-104">Overview</span></span>
<span data-ttu-id="36781-105">Güç ve soğutma Modülü (PCM) Microsoft Azure StorSimple Cihazınızı içinde oluşan bir güç ve soğutma fanları birincil ve EBOD kutularının denetlenir.</span><span class="sxs-lookup"><span data-stu-id="36781-105">The Power and Cooling Module (PCM) in your Microsoft Azure StorSimple device consists of a power supply and cooling fans that are controlled through the primary and EBOD enclosures.</span></span> <span data-ttu-id="36781-106">Her kasa için sertifikalı PCM, yalnızca bir model yok.</span><span class="sxs-lookup"><span data-stu-id="36781-106">There is only one model of PCM that is certified for each enclosure.</span></span> <span data-ttu-id="36781-107">Birincil muhafaza 764 W PCM için sertifikalı ve EBOD muhafazası 580 W PCM için sertifikalıdır.</span><span class="sxs-lookup"><span data-stu-id="36781-107">The primary enclosure is certified for a 764 W PCM and the EBOD enclosure is certified for a 580 W PCM.</span></span> <span data-ttu-id="36781-108">Birincil muhafaza ve EBOD muhafazası PCMs farklı olmasına rağmen değiştirme yordamı aynıdır.</span><span class="sxs-lookup"><span data-stu-id="36781-108">Although the PCMs for the primary enclosure and the EBOD enclosure are different, the replacement procedure is identical.</span></span>

<span data-ttu-id="36781-109">Bu öğretici açıklar nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="36781-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="36781-110">Bir PCM Kaldır</span><span class="sxs-lookup"><span data-stu-id="36781-110">Remove a PCM</span></span>
* <span data-ttu-id="36781-111">PCM yenisini yükleyin</span><span class="sxs-lookup"><span data-stu-id="36781-111">Install a replacement PCM</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36781-112">Kaldırma ve bir PCM değiştirme gözden önce güvenlik bilgileri [StorSimple donanım bileşeni değiştirme](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="36781-112">Before removing and replacing a PCM, review the safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="before-you-replace-a-pcm"></a><span data-ttu-id="36781-113">Bir PCM değiştirmeden önce</span><span class="sxs-lookup"><span data-stu-id="36781-113">Before you replace a PCM</span></span>
<span data-ttu-id="36781-114">PCM değiştirmeden önce aşağıdaki önemli sorunları dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="36781-114">Be aware of the following important issues before you replace your PCM:</span></span>

* <span data-ttu-id="36781-115">Güç kaynağı PCM biri başarısız olursa, hatalı modül yüklü bırakın, ancak güç kablosu kaldırın.</span><span class="sxs-lookup"><span data-stu-id="36781-115">If the power supply of the PCM fails, leave the faulty module installed, but remove the power cord.</span></span> <span data-ttu-id="36781-116">Fan muhafaza güç almak ve uygun soğutma sağlamaya devam devam eder.</span><span class="sxs-lookup"><span data-stu-id="36781-116">The fan will continue to receive power from the enclosure and continue to provide proper cooling.</span></span> <span data-ttu-id="36781-117">Fan başarısız olursa, PCM hemen değiştirilmesi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="36781-117">If the fan fails, the PCM needs to be replaced immediately.</span></span>
* <span data-ttu-id="36781-118">PCM kaldırmadan önce güç PCM'den ana anahtarı (var olduğunda) kapatarak veya fiziksel olarak güç kablosu kaldırarak bağlantısını kesin.</span><span class="sxs-lookup"><span data-stu-id="36781-118">Before removing the PCM, disconnect the power from the PCM by turning off the main switch (where present) or by physically removing the power cord.</span></span> <span data-ttu-id="36781-119">Bu, bir uyarı sistem bir güç kapatma olup sağlar.</span><span class="sxs-lookup"><span data-stu-id="36781-119">This provides a warning to your system that a power shutdown is imminent.</span></span>
* <span data-ttu-id="36781-120">Diğer PCM hatalı PCM değiştirme önce devam eden sistem işlemi için işlevsel olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="36781-120">Make sure that the other PCM is functional for continued system operation before replacing the faulty PCM.</span></span> <span data-ttu-id="36781-121">Hatalı PCM tarafından tam olarak işlevsel bir PCM mümkün olan en kısa sürede değiştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="36781-121">A faulty PCM must be replaced by a fully operational PCM as soon as possible.</span></span>
* <span data-ttu-id="36781-122">PCM modülü değiştirme tamamlamak için yalnızca birkaç dakika sürer ancak aşırı önlemek için başarısız PCM kaldırmanın 10 dakika içinde tamamlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="36781-122">PCM module replacement takes only few minutes to complete, but it must be completed within 10 minutes of removing the failed PCM to prevent overheating.</span></span>
* <span data-ttu-id="36781-123">Not fabrikası'ndan sevk değiştirme 764 W PCM modülleri yedek pil modülü içermez.</span><span class="sxs-lookup"><span data-stu-id="36781-123">Note that the replacement 764 W PCM modules shipped from the factory do not contain the backup battery module.</span></span> <span data-ttu-id="36781-124">Hatalı PCM'den pil kaldırın ve değiştirme gerçekleştirmeden önce değiştirme Modülü Ekle gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="36781-124">You will need to remove the battery from your faulty PCM and then insert it into the replacement module prior to performing the replacement.</span></span> <span data-ttu-id="36781-125">Daha fazla bilgi için bkz: nasıl yapılır [kaldırın ve bir yedek pil Modül Ekle](storsimple-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="36781-125">For more information, see how to [remove and insert a backup battery module](storsimple-battery-replacement.md).</span></span>

## <a name="remove-a-pcm"></a><span data-ttu-id="36781-126">Bir PCM Kaldır</span><span class="sxs-lookup"><span data-stu-id="36781-126">Remove a PCM</span></span>
<span data-ttu-id="36781-127">Microsoft Azure StorSimple cihazınızın güç ve soğutma Modülü (PCM) kaldırmak hazır olduğunuzda bu yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="36781-127">Follow these instructions when you are ready to remove a Power and Cooling Module (PCM) from your Microsoft Azure StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="36781-128">PCM kaldırmadan önce doğru değiştirme (764 W birincil kasası için) veya 580 W EBOD muhafazası için sahip olduğunuzu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="36781-128">Before you remove your PCM, verify that you have a correct replacement (764 W for the primary enclosure or 580 W for the EBOD enclosure).</span></span>
> 
> 

#### <a name="to-remove-a-pcm"></a><span data-ttu-id="36781-129">Bir PCM kaldırmak için</span><span class="sxs-lookup"><span data-stu-id="36781-129">To remove a PCM</span></span>
1. <span data-ttu-id="36781-130">Klasik Azure portalında tıklatın **aygıtları** > **Bakım** > **donanım durum**.</span><span class="sxs-lookup"><span data-stu-id="36781-130">In the Azure classic portal, click **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="36781-131">Altındaki PCM bileşenlerinin durumunu denetleme **paylaşılan bileşenleri** hangi PCM başarısız oldu tanımlamak için:</span><span class="sxs-lookup"><span data-stu-id="36781-131">Check the status of the PCM components under **Shared Components** to identify which PCM has failed:</span></span>
   
   * <span data-ttu-id="36781-132">Güç kaynağı PCM 0'ın başarısız olduysa, durumunu **güç kaynağı PCM 0'ın** kırmızı olur.</span><span class="sxs-lookup"><span data-stu-id="36781-132">If a power supply in PCM 0 has failed, the status of **Power Supply in PCM 0** will be red.</span></span>
   * <span data-ttu-id="36781-133">Güç kaynağı PCM 1 başarısız olduysa, durumunu **güç kaynağı PCM 1** kırmızı olur.</span><span class="sxs-lookup"><span data-stu-id="36781-133">If a power supply in PCM 1 has failed, the status of **Power Supply in PCM 1** will be red.</span></span>
   * <span data-ttu-id="36781-134">Fan PCM 1 başarısız oldu, ya da durumunu **PCM 0 0 soğutma** veya **PCM 0 için 1 soğutma** kırmızı olur.</span><span class="sxs-lookup"><span data-stu-id="36781-134">If the fan in PCM 1 has failed, the status of either **Cooling 0 for PCM 0** or **Cooling 1 for PCM 0** will be red.</span></span>
2. <span data-ttu-id="36781-135">Birincil muhafaza arkasında başarısız PCM bulun.</span><span class="sxs-lookup"><span data-stu-id="36781-135">Locate the failed PCM on the back of the primary enclosure.</span></span> <span data-ttu-id="36781-136">8600 model çalıştırıyorsanız, sistem birimi tanımlayıcısı ön panelini LED Ekran numarasına bakarak birincil muhafaza tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="36781-136">If you are running an 8600 model, identify the primary enclosure by looking at the System Unit Identification Number shown on the front panel LED display.</span></span> <span data-ttu-id="36781-137">Birim üzerinde birincil muhafaza görüntülenen kodu varsayılandır **00**, varsayılan birim üzerinde EBOD muhafazası görüntülenen kodu iken **01**.</span><span class="sxs-lookup"><span data-stu-id="36781-137">The default Unit ID displayed on the primary enclosure is **00**, whereas the default Unit ID displayed on the EBOD enclosure is **01**.</span></span> <span data-ttu-id="36781-138">Aşağıdaki diyagram ve tablo LED Ekran ön panelini açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="36781-138">The following diagram and table explain the front panel of the LED display.</span></span>
   
    ![Ön OPS panelindeki sistem kimliği](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     <span data-ttu-id="36781-140">**Şekil 1** cihazın ön panel</span><span class="sxs-lookup"><span data-stu-id="36781-140">**Figure 1** Front panel of the device</span></span>  
   
   | <span data-ttu-id="36781-141">Etiket</span><span class="sxs-lookup"><span data-stu-id="36781-141">Label</span></span> | <span data-ttu-id="36781-142">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36781-142">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="36781-143">1</span><span class="sxs-lookup"><span data-stu-id="36781-143">1</span></span> |<span data-ttu-id="36781-144">Sessiz düğmesi</span><span class="sxs-lookup"><span data-stu-id="36781-144">Mute button</span></span> |
   | <span data-ttu-id="36781-145">2</span><span class="sxs-lookup"><span data-stu-id="36781-145">2</span></span> |<span data-ttu-id="36781-146">Sistem gücü</span><span class="sxs-lookup"><span data-stu-id="36781-146">System power</span></span> |
   | <span data-ttu-id="36781-147">3</span><span class="sxs-lookup"><span data-stu-id="36781-147">3</span></span> |<span data-ttu-id="36781-148">Modül hatası</span><span class="sxs-lookup"><span data-stu-id="36781-148">Module fault</span></span> |
   | <span data-ttu-id="36781-149">4</span><span class="sxs-lookup"><span data-stu-id="36781-149">4</span></span> |<span data-ttu-id="36781-150">Mantıksal hatası</span><span class="sxs-lookup"><span data-stu-id="36781-150">Logical fault</span></span> |
   | <span data-ttu-id="36781-151">5</span><span class="sxs-lookup"><span data-stu-id="36781-151">5</span></span> |<span data-ttu-id="36781-152">Birim kimliği görüntüleme</span><span class="sxs-lookup"><span data-stu-id="36781-152">Unit ID display</span></span> |
3. <span data-ttu-id="36781-153">Birincil muhafaza arkasında izleme gösterge LED'leri hatalı PCM tanımlamak için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="36781-153">The monitoring indicator LEDs in the back of the primary enclosure can also be used to identify the faulty PCM.</span></span> <span data-ttu-id="36781-154">Aşağıdaki diyagram ve LED'leri hatalı PCM bulmak için nasıl kullanılacağını anlamak için tablosuna bakın.</span><span class="sxs-lookup"><span data-stu-id="36781-154">See the following diagram and table to understand how to use the LEDs to locate the faulty PCM.</span></span> <span data-ttu-id="36781-155">Örneğin, varsa LED karşılık gelen **Fan başarısız** olan aydınlatma, fan başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="36781-155">For example, if the LED corresponding to the **Fan Fail** is lit, the fan has failed.</span></span> <span data-ttu-id="36781-156">Benzer şekilde, varsa LED karşılık gelen **AC başarısız** olan aydınlatma, güç kaynağı başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="36781-156">Likewise, if the LED corresponding to **AC Fail** is lit, the power supply has failed.</span></span> 
   
    ![Cihaz PCM izleme gösterge LED'leri devre kartı](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     <span data-ttu-id="36781-158">**Şekil 2** geri of PCM LED'leri göstergesi</span><span class="sxs-lookup"><span data-stu-id="36781-158">**Figure 2** Back of PCM with indicator LEDs</span></span>
   
   | <span data-ttu-id="36781-159">Etiket</span><span class="sxs-lookup"><span data-stu-id="36781-159">Label</span></span> | <span data-ttu-id="36781-160">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36781-160">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="36781-161">1</span><span class="sxs-lookup"><span data-stu-id="36781-161">1</span></span> |<span data-ttu-id="36781-162">AC güç kesintisi</span><span class="sxs-lookup"><span data-stu-id="36781-162">AC power failure</span></span> |
   | <span data-ttu-id="36781-163">2</span><span class="sxs-lookup"><span data-stu-id="36781-163">2</span></span> |<span data-ttu-id="36781-164">Fan hatası</span><span class="sxs-lookup"><span data-stu-id="36781-164">Fan failure</span></span> |
   | <span data-ttu-id="36781-165">3</span><span class="sxs-lookup"><span data-stu-id="36781-165">3</span></span> |<span data-ttu-id="36781-166">Pil hatası</span><span class="sxs-lookup"><span data-stu-id="36781-166">Battery fault</span></span> |
   | <span data-ttu-id="36781-167">4</span><span class="sxs-lookup"><span data-stu-id="36781-167">4</span></span> |<span data-ttu-id="36781-168">PCM TAMAM</span><span class="sxs-lookup"><span data-stu-id="36781-168">PCM OK</span></span> |
   | <span data-ttu-id="36781-169">5</span><span class="sxs-lookup"><span data-stu-id="36781-169">5</span></span> |<span data-ttu-id="36781-170">DC Güç kesintisi</span><span class="sxs-lookup"><span data-stu-id="36781-170">DC power failure</span></span> |
   | <span data-ttu-id="36781-171">6</span><span class="sxs-lookup"><span data-stu-id="36781-171">6</span></span> |<span data-ttu-id="36781-172">Sağlıklı pil</span><span class="sxs-lookup"><span data-stu-id="36781-172">Battery healthy</span></span> |
4. <span data-ttu-id="36781-173">Başarısız PCM modülü bulmak için StorSimple cihazı arkası aşağıdaki diyagrama bakın.</span><span class="sxs-lookup"><span data-stu-id="36781-173">Refer to the following diagram of the back of the StorSimple device to locate the failed PCM module.</span></span> <span data-ttu-id="36781-174">PCM 0 solda ve PCM 1 sağ tarafta.</span><span class="sxs-lookup"><span data-stu-id="36781-174">PCM 0 is on the left and PCM 1 is on the right.</span></span> <span data-ttu-id="36781-175">Aşağıdaki tabloda modülleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="36781-175">The table that follows explains the modules.</span></span>
   
     ![Aygıt birincil muhafaza modüllerinin devre kartı](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     <span data-ttu-id="36781-177">**Şekil 3** eklenti modülleri aygıtla arkasına</span><span class="sxs-lookup"><span data-stu-id="36781-177">**Figure 3** Back of device with plug-in modules</span></span> 
   
   | <span data-ttu-id="36781-178">Etiket</span><span class="sxs-lookup"><span data-stu-id="36781-178">Label</span></span> | <span data-ttu-id="36781-179">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36781-179">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="36781-180">1</span><span class="sxs-lookup"><span data-stu-id="36781-180">1</span></span> |<span data-ttu-id="36781-181">PCM 0</span><span class="sxs-lookup"><span data-stu-id="36781-181">PCM 0</span></span> |
   | <span data-ttu-id="36781-182">2</span><span class="sxs-lookup"><span data-stu-id="36781-182">2</span></span> |<span data-ttu-id="36781-183">PCM 1</span><span class="sxs-lookup"><span data-stu-id="36781-183">PCM 1</span></span> |
   | <span data-ttu-id="36781-184">3</span><span class="sxs-lookup"><span data-stu-id="36781-184">3</span></span> |<span data-ttu-id="36781-185">Denetleyici 0</span><span class="sxs-lookup"><span data-stu-id="36781-185">Controller 0</span></span> |
   | <span data-ttu-id="36781-186">4</span><span class="sxs-lookup"><span data-stu-id="36781-186">4</span></span> |<span data-ttu-id="36781-187">Denetleyici 1</span><span class="sxs-lookup"><span data-stu-id="36781-187">Controller 1</span></span> |
5. <span data-ttu-id="36781-188">Hatalı PCM devre dışı bırakma ve güç kaynağı kablosunun bağlantısını kesebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36781-188">Turn off the faulty PCM and disconnect the power supply cord.</span></span> <span data-ttu-id="36781-189">PCM şimdi kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36781-189">You can now remove the PCM.</span></span>
6. <span data-ttu-id="36781-190">Mandal ve Flash erişebildiğinizden arasındaki PCM tanıtıcısı tarafında kavramak ve bunları birlikte tanıtıcı açmak için sığdırması.</span><span class="sxs-lookup"><span data-stu-id="36781-190">Grasp the latch and the side of the PCM handle between your thumb and forefinger, and squeeze them together to open the handle.</span></span>
   
    ![PCM tanıtıcısı açılıyor](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    <span data-ttu-id="36781-192">**Şekil 4** PCM tanıtıcısı açma</span><span class="sxs-lookup"><span data-stu-id="36781-192">**Figure 4** Opening the PCM handle</span></span>
7. <span data-ttu-id="36781-193">Tanıtıcı kavramayın ve PCM kaldırın.</span><span class="sxs-lookup"><span data-stu-id="36781-193">Grip the handle and remove the PCM.</span></span>
   
    ![Cihaz PCM'i kaldırılıyor](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    <span data-ttu-id="36781-195">**Şekil 5** PCM kaldırma</span><span class="sxs-lookup"><span data-stu-id="36781-195">**Figure 5** Removing the PCM</span></span>

## <a name="install-a-replacement-pcm"></a><span data-ttu-id="36781-196">PCM yenisini yükleyin</span><span class="sxs-lookup"><span data-stu-id="36781-196">Install a replacement PCM</span></span>
<span data-ttu-id="36781-197">StorSimple Cihazınızı bir PCM yüklemek için bu yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="36781-197">Follow these instructions to install a PCM in your StorSimple device.</span></span> <span data-ttu-id="36781-198">Değiştirme (764 W PCMs için yalnızca geçerlidir) PCM yüklemeden önce yedek pil modülü eklediğiniz emin olun.</span><span class="sxs-lookup"><span data-stu-id="36781-198">Ensure that you have inserted the backup battery module prior to installing the replacement PCM (applies to 764 W PCMs only).</span></span> <span data-ttu-id="36781-199">Daha fazla bilgi için bkz: nasıl yapılır [kaldırın ve bir yedek pil Modül Ekle](storsimple-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="36781-199">For more information, see how to [remove and insert a backup battery module](storsimple-battery-replacement.md).</span></span>

#### <a name="to-install-a-pcm"></a><span data-ttu-id="36781-200">Bir PCM yüklemek için</span><span class="sxs-lookup"><span data-stu-id="36781-200">To install a PCM</span></span>
1. <span data-ttu-id="36781-201">Bu kutu doğru yerini PCM sahip olduğunuzu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="36781-201">Verify that you have the correct replacement PCM for this enclosure.</span></span> <span data-ttu-id="36781-202">764 W PCM birincil muhafaza gerekir ve EBOD muhafazası 580 W PCM gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="36781-202">The primary enclosure needs a 764 W PCM and the EBOD enclosure needs a 580 W PCM.</span></span> <span data-ttu-id="36781-203">Birincil muhafazada 580 W PCM veya EBOD muhafazada 764 W PCM kullanmaya çalışmamalısınız.</span><span class="sxs-lookup"><span data-stu-id="36781-203">You should not attempt to use the 580 W PCM in the Primary enclosure, or the 764 W PCM in the EBOD enclosure.</span></span> <span data-ttu-id="36781-204">Aşağıdaki resimde bu bilgileri PCM yapıştırılmış etiketini tanımlamak nereye gösterir.</span><span class="sxs-lookup"><span data-stu-id="36781-204">The following image shows where to identify this information on the label that is affixed to the PCM.</span></span>
   
    ![Cihaz PCM etiketi](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    <span data-ttu-id="36781-206">**Şekil 6** PCM etiketi</span><span class="sxs-lookup"><span data-stu-id="36781-206">**Figure 6** PCM label</span></span>
2. <span data-ttu-id="36781-207">Bağlayıcılar için belirli dikkat kasası hasara karşı denetleyin.</span><span class="sxs-lookup"><span data-stu-id="36781-207">Check for damage to the enclosure, paying particular attention to the connectors.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="36781-208">**Bağlayıcı PIN'ler Bükülü durumunda modülünü yüklemeyin.**</span><span class="sxs-lookup"><span data-stu-id="36781-208">**Do not install the module if any connector pins are bent.**</span></span>
   > 
   > 
3. <span data-ttu-id="36781-209">Açık konumda PCM tanıtıcısı ile modülün kasası kaydırın.</span><span class="sxs-lookup"><span data-stu-id="36781-209">With the PCM handle in the open position, slide the module into the enclosure.</span></span>
   
    ![Cihaz PCM'i yükleniyor](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    <span data-ttu-id="36781-211">**Şekil 7** PCM yükleme</span><span class="sxs-lookup"><span data-stu-id="36781-211">**Figure 7** Installing the PCM</span></span>
4. <span data-ttu-id="36781-212">PCM tanıtıcısı el ile kapatın.</span><span class="sxs-lookup"><span data-stu-id="36781-212">Manually close the PCM handle.</span></span> <span data-ttu-id="36781-213">Tanıtıcı Mandal prosese gibi bir tıklama sesi.</span><span class="sxs-lookup"><span data-stu-id="36781-213">You should hear a click as the handle latch engages.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="36781-214">Bağlayıcı PIN'ler gerçekleştiriliyor olmak için hafifçe mandalı bırakılıyor olmadan tutamacı tug.</span><span class="sxs-lookup"><span data-stu-id="36781-214">To ensure that the connector pins have engaged, you can gently tug on the handle without releasing the latch.</span></span> <span data-ttu-id="36781-215">Out PCM slayt, bağlayıcıları gerçekleştiriliyor önce Mandal kapatıldı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="36781-215">If the PCM slides out, it implies that the latch was closed before the connectors engaged.</span></span>
   > 
   > 
5. <span data-ttu-id="36781-216">Güç kablolarını güç kaynağı ve PCM bağlayın.</span><span class="sxs-lookup"><span data-stu-id="36781-216">Connect the power cables to the power source and to the PCM.</span></span>
6. <span data-ttu-id="36781-217">Yükü Tahliye bales güvenli hale getirin.</span><span class="sxs-lookup"><span data-stu-id="36781-217">Secure the strain relief bales.</span></span> 
7. <span data-ttu-id="36781-218">Üzerinde PCM açın.</span><span class="sxs-lookup"><span data-stu-id="36781-218">Turn on the PCM.</span></span>
8. <span data-ttu-id="36781-219">Değiştirme başarılı olduğunu doğrulayın: Klasik Azure portalında, StorSimple Yöneticisi hizmeti, gitmek **aygıtları** > **Bakım** > **donanım durum**.</span><span class="sxs-lookup"><span data-stu-id="36781-219">Verify that the replacement was successful: in the Azure classic portal of your StorSimple Manager service, navigate to **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="36781-220">Altında **paylaşılan bileşenleri**, PCM durumu yeşil olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="36781-220">Under **Shared Components**, the status of the PCM should be green.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="36781-221">Değiştirme PCM tamamen başlatmak için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="36781-221">It may take a few minutes for the replacement PCM to completely initialize.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="36781-222">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="36781-222">Next steps</span></span>
<span data-ttu-id="36781-223">Daha fazla bilgi edinmek [StorSimple donanım bileşeni değiştirme](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="36781-223">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

