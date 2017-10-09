---
title: bir StorSimple 8600 EBOD denetleyicisi aaaReplace | Microsoft Docs
description: "Açıklar nasıl tooremove ve StorSimple 8600 model Cihazınızı biri veya her ikisi EBOD denetleyicilerinde değiştirin."
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
ms.openlocfilehash: 8343ed6f48ae97fc9204452f85e1936bfb1d6919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a><span data-ttu-id="2e567-103">EBOD denetleyicisi, StorSimple Cihazınızda değiştirin</span><span class="sxs-lookup"><span data-stu-id="2e567-103">Replace an EBOD controller on your StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="2e567-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="2e567-104">Overview</span></span>
<span data-ttu-id="2e567-105">Bu öğretici açıklar nasıl tooreplace hatalı EBOD Denetleyici Modülü, Microsoft Azure StorSimple Cihazınızda.</span><span class="sxs-lookup"><span data-stu-id="2e567-105">This tutorial explains how tooreplace a faulty EBOD controller module on your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="2e567-106">EBOD Denetleyici Modülü tooreplace, şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="2e567-106">tooreplace an EBOD controller module, you need to:</span></span>

* <span data-ttu-id="2e567-107">Merhaba hatalı EBOD denetleyicisi Kaldır</span><span class="sxs-lookup"><span data-stu-id="2e567-107">Remove hello faulty EBOD controller</span></span>
* <span data-ttu-id="2e567-108">Yeni bir EBOD denetleyicisi yükleme</span><span class="sxs-lookup"><span data-stu-id="2e567-108">Install a new EBOD controller</span></span>

<span data-ttu-id="2e567-109">Başlamadan önce aşağıdaki bilgilerle hello göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="2e567-109">Consider hello following information before you begin:</span></span>

* <span data-ttu-id="2e567-110">Boş EBOD modülleri tüm kullanılmayan yuvaları eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e567-110">Blank EBOD modules must be inserted into all unused slots.</span></span> <span data-ttu-id="2e567-111">bir yuva açık olarak bırakılırsa hello muhafaza düzgün seyrek erişimli değil.</span><span class="sxs-lookup"><span data-stu-id="2e567-111">hello enclosure will not cool properly if a slot is left open.</span></span>
* <span data-ttu-id="2e567-112">Merhaba EBOD denetleyicisi hot Swap ve yerini veya kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="2e567-112">hello EBOD controller is hot-swappable and can be removed or replaced.</span></span> <span data-ttu-id="2e567-113">Yenisini elde edene kadar başarısız bir modül kaldırmayın.</span><span class="sxs-lookup"><span data-stu-id="2e567-113">Do not remove a failed module until you have a replacement.</span></span> <span data-ttu-id="2e567-114">Merhaba değiştirme işlemini başlattığınızda, 10 dakika içinde bitmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e567-114">When you initiate hello replacement process, you must finish it within 10 minutes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2e567-115">Tooremove denemeden önce veya herhangi bir StorSimple bileşeni değiştirin, hello gözden emin olun [güvenliği simgesi kuralları](storsimple-safety.md#safety-icon-conventions) ve diğer [güvenlik önlemlerini](storsimple-safety.md).</span><span class="sxs-lookup"><span data-stu-id="2e567-115">Before attempting tooremove or replace any StorSimple component, make sure that you review hello [safety icon conventions](storsimple-safety.md#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span></span>

## <a name="remove-an-ebod-controller"></a><span data-ttu-id="2e567-116">EBOD denetleyicisi Kaldır</span><span class="sxs-lookup"><span data-stu-id="2e567-116">Remove an EBOD controller</span></span>
<span data-ttu-id="2e567-117">EBOD denetleyicisi StorSimple Cihazınızı modülünde Hello değiştirme başarısız oldu önce o hello emin olun diğer EBOD denetleyici modülü etkin ve çalışır durumda.</span><span class="sxs-lookup"><span data-stu-id="2e567-117">Before replacing hello failed EBOD controller module in your StorSimple device, make sure that hello other EBOD controller module is active and running.</span></span> <span data-ttu-id="2e567-118">Merhaba aşağıdaki yordamı ve tabloyu nasıl tooremove hello EBOD Denetleyici Modülü açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="2e567-118">hello following procedure and table explain how tooremove hello EBOD controller module.</span></span>

#### <a name="tooremove-an-ebod-module"></a><span data-ttu-id="2e567-119">tooremove EBOD Modülü</span><span class="sxs-lookup"><span data-stu-id="2e567-119">tooremove an EBOD module</span></span>
1. <span data-ttu-id="2e567-120">Açık hello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="2e567-120">Open hello Azure portal.</span></span>
2. <span data-ttu-id="2e567-121">Tooyour aygıt gidin ve çok gidin**ayarları** > **donanım durumu**ve hello etkin EBOD Denetleyici Modülü yeşil ve Merhaba LED başarısız hello için o hello LED hello durumunu doğrulayın EBOD Denetleyici Modülü kırmızı olur.</span><span class="sxs-lookup"><span data-stu-id="2e567-121">Go tooyour device and navigate too**Settings** > **Hardware health**, and verify that hello status of hello LED for hello active EBOD controller module is green and hello LED for hello failed EBOD controller module is red.</span></span>
3. <span data-ttu-id="2e567-122">Merhaba cihaz arkasına hello adresindeki başarısız hello EBOD Denetleyici Modülü bulun.</span><span class="sxs-lookup"><span data-stu-id="2e567-122">Locate hello failed EBOD controller module at hello back of hello device.</span></span>
4. <span data-ttu-id="2e567-123">Merhaba EBOD modülü hello sistem dışı çıkarmadan önce hello EBOD denetleyicisi modülü toohello denetleyicisi bağlanmak hello kabloları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2e567-123">Remove hello cables that connect hello EBOD controller module toohello controller before taking hello EBOD module out of hello system.</span></span>
5. <span data-ttu-id="2e567-124">Merhaba tam SAS bağlantı noktasına bağlı toohello denetleyicisi olduğundan hello EBOD Denetleyici Modülü not edin.</span><span class="sxs-lookup"><span data-stu-id="2e567-124">Make a note of hello exact SAS port of hello EBOD controller module that was connected toohello controller.</span></span> <span data-ttu-id="2e567-125">Merhaba EBOD modülü değiştirdikten sonra gerekli toorestore hello sistem toothis yapılandırması olacaktır.</span><span class="sxs-lookup"><span data-stu-id="2e567-125">You will be required toorestore hello system toothis configuration after you replace hello EBOD module.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2e567-126">Genellikle, bu olarak etiketli bağlantı noktası A olacaktır **içinde ana bilgisayar** diyagramı aşağıdaki hello içinde.</span><span class="sxs-lookup"><span data-stu-id="2e567-126">Typically, this will be Port A, which is labeled as **Host in** in hello following diagram.</span></span>
   
    ![Devre kartı olarak EBOD denetleyicisi](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     <span data-ttu-id="2e567-128">**Şekil 1** geri of EBOD Modülü</span><span class="sxs-lookup"><span data-stu-id="2e567-128">**Figure 1** Back of EBOD module</span></span>
   
   | <span data-ttu-id="2e567-129">Etiket</span><span class="sxs-lookup"><span data-stu-id="2e567-129">Label</span></span> | <span data-ttu-id="2e567-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2e567-130">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="2e567-131">1</span><span class="sxs-lookup"><span data-stu-id="2e567-131">1</span></span> |<span data-ttu-id="2e567-132">Hata Işığı</span><span class="sxs-lookup"><span data-stu-id="2e567-132">Fault LED</span></span> |
   | <span data-ttu-id="2e567-133">2</span><span class="sxs-lookup"><span data-stu-id="2e567-133">2</span></span> |<span data-ttu-id="2e567-134">Güç ışığı</span><span class="sxs-lookup"><span data-stu-id="2e567-134">Power LED</span></span> |
   | <span data-ttu-id="2e567-135">3</span><span class="sxs-lookup"><span data-stu-id="2e567-135">3</span></span> |<span data-ttu-id="2e567-136">SAS Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="2e567-136">SAS connectors</span></span> |
   | <span data-ttu-id="2e567-137">4</span><span class="sxs-lookup"><span data-stu-id="2e567-137">4</span></span> |<span data-ttu-id="2e567-138">SAS LED'leri</span><span class="sxs-lookup"><span data-stu-id="2e567-138">SAS LEDs</span></span> |
   | <span data-ttu-id="2e567-139">5</span><span class="sxs-lookup"><span data-stu-id="2e567-139">5</span></span> |<span data-ttu-id="2e567-140">Yalnızca Fabrika kullanımı için seri bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="2e567-140">Serial ports for factory use only</span></span> |
   | <span data-ttu-id="2e567-141">6</span><span class="sxs-lookup"><span data-stu-id="2e567-141">6</span></span> |<span data-ttu-id="2e567-142">(Ana), bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="2e567-142">Port A (Host in)</span></span> |
   | <span data-ttu-id="2e567-143">7</span><span class="sxs-lookup"><span data-stu-id="2e567-143">7</span></span> |<span data-ttu-id="2e567-144">Bağlantı noktası B (ana bilgisayarı devre dışı)</span><span class="sxs-lookup"><span data-stu-id="2e567-144">Port B (Host out)</span></span> |
   | <span data-ttu-id="2e567-145">8</span><span class="sxs-lookup"><span data-stu-id="2e567-145">8</span></span> |<span data-ttu-id="2e567-146">Bağlantı noktası C (yalnızca Fabrika kullanın)</span><span class="sxs-lookup"><span data-stu-id="2e567-146">Port C (Factory use only)</span></span> |

## <a name="install-a-new-ebod-controller"></a><span data-ttu-id="2e567-147">Yeni bir EBOD denetleyicisi yükleme</span><span class="sxs-lookup"><span data-stu-id="2e567-147">Install a new EBOD controller</span></span>
<span data-ttu-id="2e567-148">Merhaba aşağıdaki yordamı ve tabloyu açıklayan nasıl tooinstall bir StorSimple Cihazınızı EBOD denetleyicisi modülünde.</span><span class="sxs-lookup"><span data-stu-id="2e567-148">hello following procedure and table explain how tooinstall an EBOD controller module in your StorSimple device.</span></span>

#### <a name="tooinstall-an-ebod-controller"></a><span data-ttu-id="2e567-149">tooinstall EBOD denetleyicisi</span><span class="sxs-lookup"><span data-stu-id="2e567-149">tooinstall an EBOD controller</span></span>
1. <span data-ttu-id="2e567-150">Merhaba EBOD aygıt zarar, özellikle toohello arabirimi bağlayıcı için denetleyin.</span><span class="sxs-lookup"><span data-stu-id="2e567-150">Check hello EBOD device for damage, especially toohello interface connector.</span></span> <span data-ttu-id="2e567-151">Tüm PIN'ler Bükülü hello yeni EBOD denetleyicisi yüklemeyin.</span><span class="sxs-lookup"><span data-stu-id="2e567-151">Do not install hello new EBOD controller if any pins are bent.</span></span>
2. <span data-ttu-id="2e567-152">Merhaba tutma hello içinde konumu, slayt hello hello tutma devreye kadar hello muhafaza modüle açın.</span><span class="sxs-lookup"><span data-stu-id="2e567-152">With hello latches in hello open position, slide hello module into hello enclosure until hello latches engage.</span></span>
   
    ![EBOD denetleyicisi yükleniyor](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    <span data-ttu-id="2e567-154">**Şekil 2** yükleme hello EBOD Denetleyici Modülü</span><span class="sxs-lookup"><span data-stu-id="2e567-154">**Figure 2**  Installing hello EBOD controller module</span></span>
3. <span data-ttu-id="2e567-155">Kapat hello Mandal.</span><span class="sxs-lookup"><span data-stu-id="2e567-155">Close hello latch.</span></span> <span data-ttu-id="2e567-156">Merhaba Mandal prosese gibi bir tıklama sesi.</span><span class="sxs-lookup"><span data-stu-id="2e567-156">You should hear a click as hello latch engages.</span></span>
   
    ![EBOD mandalı bırakılıyor](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    <span data-ttu-id="2e567-158">**Şekil 3** hello EBOD modülü mandalı kapatılıyor</span><span class="sxs-lookup"><span data-stu-id="2e567-158">**Figure 3**  Closing hello EBOD module latch</span></span>
4. <span data-ttu-id="2e567-159">Merhaba kabloları yeniden bağlanın.</span><span class="sxs-lookup"><span data-stu-id="2e567-159">Reconnect hello cables.</span></span> <span data-ttu-id="2e567-160">Merhaba değiştirme önce mevcut hello tam yapılandırmasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="2e567-160">Use hello exact configuration that was present before hello replacement.</span></span> <span data-ttu-id="2e567-161">Diyagram aşağıdaki hello bakın ve tablo hakkında ayrıntılar için tooconnect hello kabloları.</span><span class="sxs-lookup"><span data-stu-id="2e567-161">See hello following diagram and table for details about how tooconnect hello cables.</span></span>
   
    ![Kabloyla 4U cihazınızın güç bağlantısını yapma](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    <span data-ttu-id="2e567-163">**Şekil 4**.</span><span class="sxs-lookup"><span data-stu-id="2e567-163">**Figure 4**.</span></span> <span data-ttu-id="2e567-164">Yeniden bağlanan kabloları</span><span class="sxs-lookup"><span data-stu-id="2e567-164">Reconnecting cables</span></span>
   
   | <span data-ttu-id="2e567-165">Etiket</span><span class="sxs-lookup"><span data-stu-id="2e567-165">Label</span></span> | <span data-ttu-id="2e567-166">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2e567-166">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="2e567-167">1</span><span class="sxs-lookup"><span data-stu-id="2e567-167">1</span></span> |<span data-ttu-id="2e567-168">Birincil kasası</span><span class="sxs-lookup"><span data-stu-id="2e567-168">Primary enclosure</span></span> |
   | <span data-ttu-id="2e567-169">2</span><span class="sxs-lookup"><span data-stu-id="2e567-169">2</span></span> |<span data-ttu-id="2e567-170">PCM 0</span><span class="sxs-lookup"><span data-stu-id="2e567-170">PCM 0</span></span> |
   | <span data-ttu-id="2e567-171">3</span><span class="sxs-lookup"><span data-stu-id="2e567-171">3</span></span> |<span data-ttu-id="2e567-172">PCM 1</span><span class="sxs-lookup"><span data-stu-id="2e567-172">PCM 1</span></span> |
   | <span data-ttu-id="2e567-173">4</span><span class="sxs-lookup"><span data-stu-id="2e567-173">4</span></span> |<span data-ttu-id="2e567-174">Denetleyici 0</span><span class="sxs-lookup"><span data-stu-id="2e567-174">Controller 0</span></span> |
   | <span data-ttu-id="2e567-175">5</span><span class="sxs-lookup"><span data-stu-id="2e567-175">5</span></span> |<span data-ttu-id="2e567-176">Denetleyici 1</span><span class="sxs-lookup"><span data-stu-id="2e567-176">Controller 1</span></span> |
   | <span data-ttu-id="2e567-177">6</span><span class="sxs-lookup"><span data-stu-id="2e567-177">6</span></span> |<span data-ttu-id="2e567-178">EBOD denetleyici 0</span><span class="sxs-lookup"><span data-stu-id="2e567-178">EBOD controller 0</span></span> |
   | <span data-ttu-id="2e567-179">7</span><span class="sxs-lookup"><span data-stu-id="2e567-179">7</span></span> |<span data-ttu-id="2e567-180">EBOD Denetleyici 1</span><span class="sxs-lookup"><span data-stu-id="2e567-180">EBOD controller 1</span></span> |
   | <span data-ttu-id="2e567-181">8</span><span class="sxs-lookup"><span data-stu-id="2e567-181">8</span></span> |<span data-ttu-id="2e567-182">EBOD muhafazası</span><span class="sxs-lookup"><span data-stu-id="2e567-182">EBOD enclosure</span></span> |
   | <span data-ttu-id="2e567-183">9</span><span class="sxs-lookup"><span data-stu-id="2e567-183">9</span></span> |<span data-ttu-id="2e567-184">Güç Dağıtım birimleri</span><span class="sxs-lookup"><span data-stu-id="2e567-184">Power Distribution Units</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2e567-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2e567-185">Next steps</span></span>
<span data-ttu-id="2e567-186">Daha fazla bilgi edinmek [StorSimple donanım bileşeni değiştirme](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="2e567-186">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

