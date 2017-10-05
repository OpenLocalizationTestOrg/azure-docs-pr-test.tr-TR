---
title: "StorSimple cihaz modunu değiştirme | Microsoft Docs"
description: "StorSimple cihaz modlarını tanımlar ve StorSimple için Windows PowerShell aygıt modunu değiştirmek için nasıl kullanılacağını açıklar."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: e9d7d277-8a2f-45eb-9fef-355486e14cbc
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2016
ms.author: alkohli
ms.openlocfilehash: 33c65bf2eecff3914f3227c76f7d638a4507e1f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-device-mode-on-your-storsimple-device"></a><span data-ttu-id="c394b-103">StorSimple Cihazınızda aygıt modunu değiştirme</span><span class="sxs-lookup"><span data-stu-id="c394b-103">Change the device mode on your StorSimple device</span></span>
<span data-ttu-id="c394b-104">Bu makale, StorSimple Cihazınızı çalışabilir çeşitli modlar kısa bir açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="c394b-104">This article provides a brief description of the various modes in which your StorSimple device can operate.</span></span> <span data-ttu-id="c394b-105">StorSimple Cihazınızı üç modda çalışabilir: normal, Bakım ve kurtarma.</span><span class="sxs-lookup"><span data-stu-id="c394b-105">Your StorSimple device can function in three modes: normal, maintenance, and recovery.</span></span> 

<span data-ttu-id="c394b-106">Bu makaleyi okuduktan sonra şunları öğrenmiş olacaksınız:</span><span class="sxs-lookup"><span data-stu-id="c394b-106">After reading this article, you will know:</span></span>

* <span data-ttu-id="c394b-107">StorSimple cihaz modu</span><span class="sxs-lookup"><span data-stu-id="c394b-107">What the StorSimple device modes are</span></span>
* <span data-ttu-id="c394b-108">StorSimple cihazı hangi modu anlamak nasıl kullanılıyor</span><span class="sxs-lookup"><span data-stu-id="c394b-108">How to figure out which mode the StorSimple device is in</span></span>
* <span data-ttu-id="c394b-109">Bakım modu normal arasında değiştirme ve *tersi*</span><span class="sxs-lookup"><span data-stu-id="c394b-109">How to change from normal to maintenance mode and *vice versa*</span></span>

<span data-ttu-id="c394b-110">Yukarıdaki yönetim görevlerini yalnızca StorSimple Cihazınızı Windows PowerShell arabirimi gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="c394b-110">The above management tasks can only be performed via the Windows PowerShell interface of your StorSimple device.</span></span>

## <a name="about-storsimple-device-modes"></a><span data-ttu-id="c394b-111">StorSimple cihaz modları hakkında</span><span class="sxs-lookup"><span data-stu-id="c394b-111">About StorSimple device modes</span></span>
<span data-ttu-id="c394b-112">StorSimple Cihazınızı normal, Bakım veya kurtarma modunda çalışır.</span><span class="sxs-lookup"><span data-stu-id="c394b-112">Your StorSimple device can operate in normal, maintenance, or recovery mode.</span></span> <span data-ttu-id="c394b-113">Bu modların her birinde kısaca aşağıda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c394b-113">Each of these modes is briefly described below.</span></span>

### <a name="normal-mode"></a><span data-ttu-id="c394b-114">Normal modda</span><span class="sxs-lookup"><span data-stu-id="c394b-114">Normal mode</span></span>
<span data-ttu-id="c394b-115">Bu, normal işlem modu için tam olarak yapılandırılmış bir StorSimple cihazı olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="c394b-115">This is defined as the normal operational mode for a fully configured StorSimple device.</span></span> <span data-ttu-id="c394b-116">Varsayılan olarak, Cihazınızı normal modda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c394b-116">By default, your device should be in normal mode.</span></span>

### <a name="maintenance-mode"></a><span data-ttu-id="c394b-117">Bakım modu</span><span class="sxs-lookup"><span data-stu-id="c394b-117">Maintenance mode</span></span>
<span data-ttu-id="c394b-118">Bazen StorSimple cihazı bakım moduna alındığında gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="c394b-118">Sometimes the StorSimple device may need to be placed into maintenance mode.</span></span> <span data-ttu-id="c394b-119">Bu mod cihaz üzerinde bakım gerçekleştirmek ve disk yazılımla ilgili olanlar gibi kesintiye uğratan güncelleştirmeleri yüklemenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="c394b-119">This mode allows you to perform maintenance on the device and install disruptive updates, such as those related to disk firmware.</span></span>

<span data-ttu-id="c394b-120">StorSimple için Windows PowerShell aracılığıyla yalnızca bakım moduna sistem koyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c394b-120">You can put the system into maintenance mode only via the Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="c394b-121">Tüm g/ç istekleri bu modda duraklatıldı.</span><span class="sxs-lookup"><span data-stu-id="c394b-121">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="c394b-122">Geçici olmayan rasgele erişim belleği (NVRAM) gibi hizmetleri veya Küme hizmeti de durdurulur.</span><span class="sxs-lookup"><span data-stu-id="c394b-122">Services such as non-volatile random access memory (NVRAM) or the clustering service are also stopped.</span></span> <span data-ttu-id="c394b-123">İki denetleyiciye girin ya da bu modundan çıkmak yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="c394b-123">Both the controllers are restarted when you enter or exit this mode.</span></span> <span data-ttu-id="c394b-124">Bakım modu çıktığınızda, tüm hizmetleri devam eder ve iyi durumda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c394b-124">When you exit the maintenance mode, all the services will resume and should be healthy.</span></span> <span data-ttu-id="c394b-125">Bu birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="c394b-125">This may take a few minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="c394b-126">**Bakım modu yalnızca düzgün çalışan bir aygıtta desteklenir. İçinde bir veya iki denetleyicilerinin çalışmıyor bir aygıtta desteklenmiyor.**
> </span><span class="sxs-lookup"><span data-stu-id="c394b-126">**Maintenance mode is only supported on a properly functioning device. It is not supported on a device in which one or both of the controllers are not functioning.**
</span></span></br>
> 
> 

### <a name="recovery-mode"></a><span data-ttu-id="c394b-127">Kurtarma moduna</span><span class="sxs-lookup"><span data-stu-id="c394b-127">Recovery mode</span></span>
<span data-ttu-id="c394b-128">Kurtarma moduna "Ağ desteği ile Windows güvenli modda" olarak tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="c394b-128">Recovery mode can be described as "Windows Safe Mode with network support".</span></span> <span data-ttu-id="c394b-129">Kurtarma moduna Microsoft Support ekibi prosese ve bunları sistemde tanılama işlemleri gerçekleştirmek sağlar.</span><span class="sxs-lookup"><span data-stu-id="c394b-129">Recovery mode engages the Microsoft Support team and allows them to perform diagnostics on the system.</span></span> <span data-ttu-id="c394b-130">Birincil kurtarma modunda sistem günlüklerini hedefidir.</span><span class="sxs-lookup"><span data-stu-id="c394b-130">The primary goal of recovery mode is to retrieve the system logs.</span></span>

<span data-ttu-id="c394b-131">Sisteminizi kurtarma moduna girer, sonraki adımlar için Microsoft Support başvurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c394b-131">If your system goes into recovery mode, you should contact Microsoft Support for next steps.</span></span> <span data-ttu-id="c394b-132">Daha fazla bilgi için Git [Microsoft Destek birimine başvurun](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="c394b-132">For more information, go to [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c394b-133">**Cihaz kurtarma modunda yerleştirilemiyor. Aygıt hatalı bir durumda, cihaz Microsoft Support personeli inceleyebilirsiniz onu bir duruma getirmek kurtarma modunda çalışır.**</span><span class="sxs-lookup"><span data-stu-id="c394b-133">**You cannot place the device in recovery mode. If the device is in a bad state, recovery mode tries to get the device into a state in which Microsoft Support personnel can examine it.**</span></span>
> 
> 

## <a name="determine-storsimple-device-mode"></a><span data-ttu-id="c394b-134">StorSimple cihaz modunu belirler</span><span class="sxs-lookup"><span data-stu-id="c394b-134">Determine StorSimple device mode</span></span>
#### <a name="to-determine-the-current-device-mode"></a><span data-ttu-id="c394b-135">Geçerli cihaz modu belirlemek için</span><span class="sxs-lookup"><span data-stu-id="c394b-135">To determine the current device mode</span></span>
1. <span data-ttu-id="c394b-136">İçindeki adımları izleyerek cihaz seri konsoluna oturum [kullan cihaz seri konsoluna bağlanmak için PuTTY](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="c394b-136">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="c394b-137">Cihaz seri konsol menüsünde başlık iletisi bakın.</span><span class="sxs-lookup"><span data-stu-id="c394b-137">Look at the banner message in the serial console menu of the device.</span></span> <span data-ttu-id="c394b-138">Bu ileti, açıkça cihazın Bakım veya kurtarma modunda olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="c394b-138">This message explicitly indicates whether the device is in maintenance or recovery mode.</span></span> <span data-ttu-id="c394b-139">İleti sistemi moduna ilgili belirli bir bilgi içermiyorsa, cihaz normal modda çalışır.</span><span class="sxs-lookup"><span data-stu-id="c394b-139">If the message does not contain any specific information pertaining to the system mode, the device is in normal mode.</span></span>

## <a name="change-the-storsimple-device-mode"></a><span data-ttu-id="c394b-140">StorSimple cihaz modunu değiştirme</span><span class="sxs-lookup"><span data-stu-id="c394b-140">Change the StorSimple device mode</span></span>
<span data-ttu-id="c394b-141">StorSimple cihazı Bakımı yap veya Bakım modu güncelleştirmeleri yüklemek için (modundan normal) bakım moduna yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c394b-141">You can place the StorSimple device into maintenance mode (from normal mode) to perform maintenance or install maintenance mode updates.</span></span> <span data-ttu-id="c394b-142">Girin veya bakım modundan çıkmak için aşağıdaki yordamları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="c394b-142">Perform the following procedures to enter or exit maintenance mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c394b-143">Bakım modu girmeden önce erişerek her iki cihaz denetleyicilerinin sağlıklı olduğunu doğrula **donanım durum** üzerinde **Bakım** Klasik Azure portalındaki sayfası.</span><span class="sxs-lookup"><span data-stu-id="c394b-143">Before entering maintenance mode, verify that both device controllers are healthy by accessing the **Hardware Status** on the **Maintenance** page in the Azure classic portal.</span></span> <span data-ttu-id="c394b-144">Bir veya iki denetleyicileri sağlıklı emin değilseniz, sonraki adımlar için Microsoft Support başvurun.</span><span class="sxs-lookup"><span data-stu-id="c394b-144">If one or both the controllers are not healthy, contact Microsoft Support for the next steps.</span></span> <span data-ttu-id="c394b-145">Daha fazla bilgi için Git [Microsoft Destek birimine başvurun](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="c394b-145">For more information, go to [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
> 
> 

#### <a name="to-enter-maintenance-mode"></a><span data-ttu-id="c394b-146">Bakım modu girmek için</span><span class="sxs-lookup"><span data-stu-id="c394b-146">To enter maintenance mode</span></span>
1. <span data-ttu-id="c394b-147">İçindeki adımları izleyerek cihaz seri konsoluna oturum [kullan cihaz seri konsoluna bağlanmak için PuTTY](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="c394b-147">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="c394b-148">Seri konsol menüsünde seçeneği 1, **oturum oturum tam erişim**.</span><span class="sxs-lookup"><span data-stu-id="c394b-148">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="c394b-149">İstendiğinde, sağlayın **cihaz Yöneticisi parolası**.</span><span class="sxs-lookup"><span data-stu-id="c394b-149">When prompted, provide the **device administrator password**.</span></span> <span data-ttu-id="c394b-150">Varsayılan parola: `Password1`.</span><span class="sxs-lookup"><span data-stu-id="c394b-150">The default password is: `Password1`.</span></span>
3. <span data-ttu-id="c394b-151">Komut istemine yazın</span><span class="sxs-lookup"><span data-stu-id="c394b-151">At the command prompt, type</span></span> 
   
    `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="c394b-152">Bakım modu tüm g/ç istekleri kesintiye ve klasik Azure portalı bağlantısı sever ve onaylamanız istenir bildiren bir uyarı iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c394b-152">You will see a warning message telling you that maintenance mode will disrupt all I/O requests and sever the connection to the Azure classic portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="c394b-153">Tür **Y** bakım moduna girmek için.</span><span class="sxs-lookup"><span data-stu-id="c394b-153">Type **Y** to enter maintenance mode.</span></span>
5. <span data-ttu-id="c394b-154">Hem denetleyicileri yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="c394b-154">Both controllers will restart.</span></span> <span data-ttu-id="c394b-155">Yeniden başlatma tamamlandıktan sonra aygıtın bakım modunda olduğunu gösteren başka bir ileti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c394b-155">When the restart is complete, another message will appear indicating that the device is in maintenance mode.</span></span>

#### <a name="to-exit-maintenance-mode"></a><span data-ttu-id="c394b-156">Bakım modundan çıkmak için</span><span class="sxs-lookup"><span data-stu-id="c394b-156">To exit maintenance mode</span></span>
1. <span data-ttu-id="c394b-157">Cihaz seri konsoluna oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c394b-157">Log on to the device serial console.</span></span> <span data-ttu-id="c394b-158">Cihazınızı bakım modunda olduğundan başlık iletisi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c394b-158">Verify from the banner message that your device is in maintenance mode.</span></span>
2. <span data-ttu-id="c394b-159">Komut istemine yazın:</span><span class="sxs-lookup"><span data-stu-id="c394b-159">At the command prompt, type:</span></span>
   
    `Exit-HcsMaintenanceMode`
3. <span data-ttu-id="c394b-160">Bir uyarı iletisi ve bir onay iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c394b-160">A warning message and a confirmation message will appear.</span></span> <span data-ttu-id="c394b-161">Tür **Y** bakım modundan çıkmak için.</span><span class="sxs-lookup"><span data-stu-id="c394b-161">Type **Y** to exit maintenance mode.</span></span>
4. <span data-ttu-id="c394b-162">Hem denetleyicileri yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="c394b-162">Both controllers will restart.</span></span> <span data-ttu-id="c394b-163">Yeniden başlatma tamamlandıktan sonra aygıtın normal modda olduğunu gösteren başka bir ileti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c394b-163">When the restart is complete, another message will appear indicating that the device is in normal mode.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c394b-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c394b-164">Next steps</span></span>
<span data-ttu-id="c394b-165">Bilgi edinmek için nasıl [normal ve Bakım modu güncelleştirmeleri uygulamak](storsimple-update-device.md) , StorSimple Cihazınızda.</span><span class="sxs-lookup"><span data-stu-id="c394b-165">Learn how to [apply normal and maintenance mode updates](storsimple-update-device.md) on your StorSimple device.</span></span>

