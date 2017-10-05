---
title: "Bir StorSimple EBOD denetleyicisi Değiştir | Microsoft Docs"
description: "Bir StorSimple 8600 model Cihazınızı biri veya her ikisi EBOD denetleyicilerinde kaldırdığınızda ve açıklanmaktadır."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8cbfa507-1a56-4e24-99dd-7db9abd3b850
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 23d819ddc3bbcbaf2847cdcc9191407ead0ff43d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a><span data-ttu-id="a953f-103">EBOD denetleyicisi, StorSimple Cihazınızda değiştirin</span><span class="sxs-lookup"><span data-stu-id="a953f-103">Replace an EBOD controller on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="a953f-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="a953f-104">Overview</span></span>
<span data-ttu-id="a953f-105">Bu öğretici, hatalı bir EBOD Denetleyici Modülü, Microsoft Azure StorSimple Cihazınızda Değiştir açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a953f-105">This tutorial explains how to replace a faulty EBOD controller module on your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="a953f-106">EBOD Denetleyici Modülü değiştirmek için aktarmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a953f-106">To replace an EBOD controller module, you need to:</span></span>

* <span data-ttu-id="a953f-107">Hatalı EBOD denetleyicisi Kaldır</span><span class="sxs-lookup"><span data-stu-id="a953f-107">Remove the faulty EBOD controller</span></span>
* <span data-ttu-id="a953f-108">Yeni bir EBOD denetleyicisi yükleme</span><span class="sxs-lookup"><span data-stu-id="a953f-108">Install a new EBOD controller</span></span>

<span data-ttu-id="a953f-109">Başlamadan önce aşağıdaki bilgileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="a953f-109">Consider the following information before you begin:</span></span>

* <span data-ttu-id="a953f-110">Boş EBOD modülleri tüm kullanılmayan yuvaları eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a953f-110">Blank EBOD modules must be inserted into all unused slots.</span></span> <span data-ttu-id="a953f-111">Bir yuva açık olarak bırakılırsa muhafaza düzgün seyrek erişimli değil.</span><span class="sxs-lookup"><span data-stu-id="a953f-111">The enclosure will not cool properly if a slot is left open.</span></span>
* <span data-ttu-id="a953f-112">EBOD denetleyicisi hot Swap ve yerini veya kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="a953f-112">The EBOD controller is hot-swappable and can be removed or replaced.</span></span> <span data-ttu-id="a953f-113">Yenisini elde edene kadar başarısız bir modül kaldırmayın.</span><span class="sxs-lookup"><span data-stu-id="a953f-113">Do not remove a failed module until you have a replacement.</span></span> <span data-ttu-id="a953f-114">Değiştirme işlemini başlattığınızda, 10 dakika içinde bitmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a953f-114">When you initiate the replacement process, you must finish it within 10 minutes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a953f-115">Kaldırın veya herhangi bir StorSimple bileşeni değiştirmek denemeden önce gözden geçirmenizi emin olun [güvenliği simgesi kuralları](storsimple-safety.md#safety-icon-conventions) ve diğer [güvenlik önlemlerini](storsimple-safety.md).</span><span class="sxs-lookup"><span data-stu-id="a953f-115">Before attempting to remove or replace any StorSimple component, make sure that you review the [safety icon conventions](storsimple-safety.md#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span></span>
> 
> 

## <a name="remove-an-ebod-controller"></a><span data-ttu-id="a953f-116">EBOD denetleyicisi Kaldır</span><span class="sxs-lookup"><span data-stu-id="a953f-116">Remove an EBOD controller</span></span>
<span data-ttu-id="a953f-117">StorSimple Cihazınızı başarısız EBOD denetleyicisi modülünde değiştirmeden önce bir EBOD denetleyici modülü etkin ve çalışıyor olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a953f-117">Before replacing the failed EBOD controller module in your StorSimple device, make sure that the other EBOD controller module is active and running.</span></span> <span data-ttu-id="a953f-118">Aşağıdaki yordamı ve tabloyu EBOD denetleyicisi modülün nasıl kaldırılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a953f-118">The following procedure and table explain how to remove the EBOD controller module.</span></span>

#### <a name="to-remove-an-ebod-module"></a><span data-ttu-id="a953f-119">EBOD modülünü kaldırmak için</span><span class="sxs-lookup"><span data-stu-id="a953f-119">To remove an EBOD module</span></span>
1. <span data-ttu-id="a953f-120">Azure Klasik Portalı'nı açın.</span><span class="sxs-lookup"><span data-stu-id="a953f-120">Open the Azure classic portal.</span></span>
2. <span data-ttu-id="a953f-121">Gidin **aygıtları** > **Bakım** > **donanım durum**, doğrulayın active EBOD denetleyicisi LED durumu Modül yeşil ve başarısız EBOD Denetleyici Modülü LED kırmızı.</span><span class="sxs-lookup"><span data-stu-id="a953f-121">Navigate to **Devices** > **Maintenance** > **Hardware Status**, and verify that the status of the LED for the active EBOD controller module is green and the LED for the failed EBOD controller module is red.</span></span>
3. <span data-ttu-id="a953f-122">Cihaz arkasındaki başarısız EBOD Denetleyici Modülü bulun.</span><span class="sxs-lookup"><span data-stu-id="a953f-122">Locate the failed EBOD controller module at the back of the device.</span></span>
4. <span data-ttu-id="a953f-123">Sistem dışı EBOD modülü çıkarmadan önce EBOD Denetleyici Modülü denetleyicisine bağlanmak kabloları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="a953f-123">Remove the cables that connect the EBOD controller module to the controller before taking the EBOD module out of the system.</span></span>
5. <span data-ttu-id="a953f-124">Denetleyiciye bağlı EBOD Denetleyici Modülü tam SAS bağlantı noktasını not edin.</span><span class="sxs-lookup"><span data-stu-id="a953f-124">Make a note of the exact SAS port of the EBOD controller module that was connected to the controller.</span></span> <span data-ttu-id="a953f-125">EBOD modülü değiştirdikten sonra sistem bu yapılandırmayı geri yüklemek için gerekli.</span><span class="sxs-lookup"><span data-stu-id="a953f-125">You will be required to restore the system to this configuration after you replace the EBOD module.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="a953f-126">Genellikle, bu olarak etiketli bağlantı noktası A olacaktır **içinde ana bilgisayar** Aşağıdaki diyagramda.</span><span class="sxs-lookup"><span data-stu-id="a953f-126">Typically, this will be Port A, which is labeled as **Host in** in the following diagram.</span></span>
   > 
   > 
   
    ![Devre kartı olarak EBOD denetleyicisi](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     <span data-ttu-id="a953f-128">**Şekil 1** geri of EBOD Modülü</span><span class="sxs-lookup"><span data-stu-id="a953f-128">**Figure 1** Back of EBOD module</span></span>
   
   | <span data-ttu-id="a953f-129">Etiket</span><span class="sxs-lookup"><span data-stu-id="a953f-129">Label</span></span> | <span data-ttu-id="a953f-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a953f-130">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="a953f-131">1</span><span class="sxs-lookup"><span data-stu-id="a953f-131">1</span></span> |<span data-ttu-id="a953f-132">Hata Işığı</span><span class="sxs-lookup"><span data-stu-id="a953f-132">Fault LED</span></span> |
   | <span data-ttu-id="a953f-133">2</span><span class="sxs-lookup"><span data-stu-id="a953f-133">2</span></span> |<span data-ttu-id="a953f-134">Güç ışığı</span><span class="sxs-lookup"><span data-stu-id="a953f-134">Power LED</span></span> |
   | <span data-ttu-id="a953f-135">3</span><span class="sxs-lookup"><span data-stu-id="a953f-135">3</span></span> |<span data-ttu-id="a953f-136">SAS Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="a953f-136">SAS connectors</span></span> |
   | <span data-ttu-id="a953f-137">4</span><span class="sxs-lookup"><span data-stu-id="a953f-137">4</span></span> |<span data-ttu-id="a953f-138">SAS LED'leri</span><span class="sxs-lookup"><span data-stu-id="a953f-138">SAS LEDs</span></span> |
   | <span data-ttu-id="a953f-139">5</span><span class="sxs-lookup"><span data-stu-id="a953f-139">5</span></span> |<span data-ttu-id="a953f-140">Yalnızca Fabrika kullanımı için seri bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="a953f-140">Serial ports for factory use only</span></span> |
   | <span data-ttu-id="a953f-141">6</span><span class="sxs-lookup"><span data-stu-id="a953f-141">6</span></span> |<span data-ttu-id="a953f-142">(Ana), bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="a953f-142">Port A (Host in)</span></span> |
   | <span data-ttu-id="a953f-143">7</span><span class="sxs-lookup"><span data-stu-id="a953f-143">7</span></span> |<span data-ttu-id="a953f-144">Bağlantı noktası B (ana bilgisayarı devre dışı)</span><span class="sxs-lookup"><span data-stu-id="a953f-144">Port B (Host out)</span></span> |
   | <span data-ttu-id="a953f-145">8</span><span class="sxs-lookup"><span data-stu-id="a953f-145">8</span></span> |<span data-ttu-id="a953f-146">Bağlantı noktası C (yalnızca Fabrika kullanın)</span><span class="sxs-lookup"><span data-stu-id="a953f-146">Port C (Factory use only)</span></span> |

## <a name="install-a-new-ebod-controller"></a><span data-ttu-id="a953f-147">Yeni bir EBOD denetleyicisi yükleme</span><span class="sxs-lookup"><span data-stu-id="a953f-147">Install a new EBOD controller</span></span>
<span data-ttu-id="a953f-148">Aşağıdaki yordamı ve tabloyu StorSimple Cihazınızı EBOD Denetleyici Modülü yükleneceği açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a953f-148">The following procedure and table explain how to install an EBOD controller module in your StorSimple device.</span></span>

#### <a name="to-install-an-ebod-controller"></a><span data-ttu-id="a953f-149">EBOD denetleyicisi yüklemek için</span><span class="sxs-lookup"><span data-stu-id="a953f-149">To install an EBOD controller</span></span>
1. <span data-ttu-id="a953f-150">EBOD aygıt arabirimi bağlayıcıya özellikle hasara karşı denetleyin.</span><span class="sxs-lookup"><span data-stu-id="a953f-150">Check the EBOD device for damage, especially to the interface connector.</span></span> <span data-ttu-id="a953f-151">Tüm PIN'ler Bükülü yeni EBOD denetleyicisi yüklemeyin.</span><span class="sxs-lookup"><span data-stu-id="a953f-151">Do not install the new EBOD controller if any pins are bent.</span></span>
2. <span data-ttu-id="a953f-152">Mandal devreye kadar açık konumda tutma ile modülü muhafaza kaydırın.</span><span class="sxs-lookup"><span data-stu-id="a953f-152">With the latches in the open position, slide the module into the enclosure until the latches engage.</span></span>
   
    ![EBOD denetleyicisi yükleniyor](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    <span data-ttu-id="a953f-154">**Şekil 2** EBOD denetleyici modülü yükleniyor</span><span class="sxs-lookup"><span data-stu-id="a953f-154">**Figure 2**  Installing the EBOD controller module</span></span>
3. <span data-ttu-id="a953f-155">Mandal kapatın.</span><span class="sxs-lookup"><span data-stu-id="a953f-155">Close the latch.</span></span> <span data-ttu-id="a953f-156">Mandal prosese gibi bir tıklama sesi.</span><span class="sxs-lookup"><span data-stu-id="a953f-156">You should hear a click as the latch engages.</span></span>
   
    ![EBOD mandalı bırakılıyor](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    <span data-ttu-id="a953f-158">**Şekil 3** EBOD modülü mandalı kapatılıyor</span><span class="sxs-lookup"><span data-stu-id="a953f-158">**Figure 3**  Closing the EBOD module latch</span></span>
4. <span data-ttu-id="a953f-159">Kabloları yeniden bağlanın.</span><span class="sxs-lookup"><span data-stu-id="a953f-159">Reconnect the cables.</span></span> <span data-ttu-id="a953f-160">Değiştirme önce mevcut tam yapılandırmasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="a953f-160">Use the exact configuration that was present before the replacement.</span></span> <span data-ttu-id="a953f-161">Aşağıdaki diyagramda ve tablo kabloları bağlanma hakkında ayrıntılı bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="a953f-161">See the following diagram and table for details about how to connect the cables.</span></span>
   
    ![Kabloyla 4U cihazınızın güç bağlantısını yapma](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    <span data-ttu-id="a953f-163">**Şekil 4**.</span><span class="sxs-lookup"><span data-stu-id="a953f-163">**Figure 4**.</span></span> <span data-ttu-id="a953f-164">Yeniden bağlanan kabloları</span><span class="sxs-lookup"><span data-stu-id="a953f-164">Reconnecting cables</span></span>
   
   | <span data-ttu-id="a953f-165">Etiket</span><span class="sxs-lookup"><span data-stu-id="a953f-165">Label</span></span> | <span data-ttu-id="a953f-166">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a953f-166">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="a953f-167">1</span><span class="sxs-lookup"><span data-stu-id="a953f-167">1</span></span> |<span data-ttu-id="a953f-168">Birincil kasası</span><span class="sxs-lookup"><span data-stu-id="a953f-168">Primary enclosure</span></span> |
   | <span data-ttu-id="a953f-169">2</span><span class="sxs-lookup"><span data-stu-id="a953f-169">2</span></span> |<span data-ttu-id="a953f-170">PCM 0</span><span class="sxs-lookup"><span data-stu-id="a953f-170">PCM 0</span></span> |
   | <span data-ttu-id="a953f-171">3</span><span class="sxs-lookup"><span data-stu-id="a953f-171">3</span></span> |<span data-ttu-id="a953f-172">PCM 1</span><span class="sxs-lookup"><span data-stu-id="a953f-172">PCM 1</span></span> |
   | <span data-ttu-id="a953f-173">4</span><span class="sxs-lookup"><span data-stu-id="a953f-173">4</span></span> |<span data-ttu-id="a953f-174">Denetleyici 0</span><span class="sxs-lookup"><span data-stu-id="a953f-174">Controller 0</span></span> |
   | <span data-ttu-id="a953f-175">5</span><span class="sxs-lookup"><span data-stu-id="a953f-175">5</span></span> |<span data-ttu-id="a953f-176">Denetleyici 1</span><span class="sxs-lookup"><span data-stu-id="a953f-176">Controller 1</span></span> |
   | <span data-ttu-id="a953f-177">6</span><span class="sxs-lookup"><span data-stu-id="a953f-177">6</span></span> |<span data-ttu-id="a953f-178">EBOD denetleyici 0</span><span class="sxs-lookup"><span data-stu-id="a953f-178">EBOD controller 0</span></span> |
   | <span data-ttu-id="a953f-179">7</span><span class="sxs-lookup"><span data-stu-id="a953f-179">7</span></span> |<span data-ttu-id="a953f-180">EBOD Denetleyici 1</span><span class="sxs-lookup"><span data-stu-id="a953f-180">EBOD controller 1</span></span> |
   | <span data-ttu-id="a953f-181">8</span><span class="sxs-lookup"><span data-stu-id="a953f-181">8</span></span> |<span data-ttu-id="a953f-182">EBOD muhafazası</span><span class="sxs-lookup"><span data-stu-id="a953f-182">EBOD enclosure</span></span> |
   | <span data-ttu-id="a953f-183">9</span><span class="sxs-lookup"><span data-stu-id="a953f-183">9</span></span> |<span data-ttu-id="a953f-184">Güç Dağıtım birimleri</span><span class="sxs-lookup"><span data-stu-id="a953f-184">Power Distribution Units</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a953f-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a953f-185">Next steps</span></span>
<span data-ttu-id="a953f-186">Daha fazla bilgi edinmek [StorSimple donanım bileşeni değiştirme](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="a953f-186">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

