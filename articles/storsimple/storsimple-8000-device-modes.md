---
title: aaaChange StorSimple cihaz modunu | Microsoft Docs
description: "Merhaba StorSimple cihaz modlarını tanımlar ve açıklar nasıl StorSimple toochange için Windows PowerShell toouse hello aygıt modu."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 058ca6cc38954bce3679cc21b39d341b10cb4dfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-device-mode-on-your-storsimple-device"></a><span data-ttu-id="b479c-103">StorSimple Cihazınızda hello aygıt modu Değiştir</span><span class="sxs-lookup"><span data-stu-id="b479c-103">Change hello device mode on your StorSimple device</span></span>

<span data-ttu-id="b479c-104">Bu makale, StorSimple Cihazınızı çalışabilir çeşitli modlar hello kısa bir açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="b479c-104">This article provides a brief description of hello various modes in which your StorSimple device can operate.</span></span> <span data-ttu-id="b479c-105">StorSimple Cihazınızı üç modda çalışabilir: normal, Bakım ve kurtarma.</span><span class="sxs-lookup"><span data-stu-id="b479c-105">Your StorSimple device can function in three modes: normal, maintenance, and recovery.</span></span>

<span data-ttu-id="b479c-106">Bu makaleyi okuduktan sonra şunları öğrenmiş olacaksınız:</span><span class="sxs-lookup"><span data-stu-id="b479c-106">After reading this article, you will know:</span></span>

* <span data-ttu-id="b479c-107">Hangi hello StorSimple cihaz modlar</span><span class="sxs-lookup"><span data-stu-id="b479c-107">What hello StorSimple device modes are</span></span>
* <span data-ttu-id="b479c-108">Hangi modun çıkışı toofigure hello StorSimple cihazı nasıl bulunduğu</span><span class="sxs-lookup"><span data-stu-id="b479c-108">How toofigure out which mode hello StorSimple device is in</span></span>
* <span data-ttu-id="b479c-109">Nasıl normal toomaintenance modundan toochange ve *tersi*</span><span class="sxs-lookup"><span data-stu-id="b479c-109">How toochange from normal toomaintenance mode and *vice versa*</span></span>

<span data-ttu-id="b479c-110">Yönetim görevleri yukarıda Hello yalnızca StorSimple cihazınızın hello Windows PowerShell arabirimi gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="b479c-110">hello above management tasks can only be performed via hello Windows PowerShell interface of your StorSimple device.</span></span>

## <a name="about-storsimple-device-modes"></a><span data-ttu-id="b479c-111">StorSimple cihaz modları hakkında</span><span class="sxs-lookup"><span data-stu-id="b479c-111">About StorSimple device modes</span></span>

<span data-ttu-id="b479c-112">StorSimple Cihazınızı normal, Bakım veya kurtarma modunda çalışır.</span><span class="sxs-lookup"><span data-stu-id="b479c-112">Your StorSimple device can operate in normal, maintenance, or recovery mode.</span></span> <span data-ttu-id="b479c-113">Bu modların her birinde kısaca aşağıda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b479c-113">Each of these modes is briefly described below.</span></span>

### <a name="normal-mode"></a><span data-ttu-id="b479c-114">Normal modda</span><span class="sxs-lookup"><span data-stu-id="b479c-114">Normal mode</span></span>

<span data-ttu-id="b479c-115">Bu, hello normal çalışma modu için tam olarak yapılandırılmış bir StorSimple cihazı olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="b479c-115">This is defined as hello normal operational mode for a fully configured StorSimple device.</span></span> <span data-ttu-id="b479c-116">Varsayılan olarak, Cihazınızı normal modda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b479c-116">By default, your device should be in normal mode.</span></span>

### <a name="maintenance-mode"></a><span data-ttu-id="b479c-117">Bakım modu</span><span class="sxs-lookup"><span data-stu-id="b479c-117">Maintenance mode</span></span>

<span data-ttu-id="b479c-118">Bazen hello StorSimple cihazı bakım moduna geçirildi toobe gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="b479c-118">Sometimes hello StorSimple device may need toobe placed into maintenance mode.</span></span> <span data-ttu-id="b479c-119">Bu mod hello cihazda tooperform bakım izin verir ve bu toodisk bellenim ilgili gibi kesintiye uğratan güncelleştirmeleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b479c-119">This mode allows you tooperform maintenance on hello device and install disruptive updates, such as those related toodisk firmware.</span></span>

<span data-ttu-id="b479c-120">StorSimple için yalnızca hello Windows PowerShell aracılığıyla bakım moduna hello sistem koyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b479c-120">You can put hello system into maintenance mode only via hello Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="b479c-121">Tüm g/ç istekleri bu modda duraklatıldı.</span><span class="sxs-lookup"><span data-stu-id="b479c-121">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="b479c-122">Geçici olmayan rasgele erişim belleği (NVRAM) veya hizmet kümeleme hello gibi hizmetleri de durdurulur.</span><span class="sxs-lookup"><span data-stu-id="b479c-122">Services such as non-volatile random access memory (NVRAM) or hello clustering service are also stopped.</span></span> <span data-ttu-id="b479c-123">Girin ya da bu modundan çıkmak hem hello denetleyicileri yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="b479c-123">Both hello controllers are restarted when you enter or exit this mode.</span></span> <span data-ttu-id="b479c-124">Hello Bakım modu çıktığınızda, tüm hello Hizmetleri devam eder ve iyi durumda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b479c-124">When you exit hello maintenance mode, all hello services will resume and should be healthy.</span></span> <span data-ttu-id="b479c-125">Bu birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="b479c-125">This may take a few minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="b479c-126">**Bakım modu yalnızca düzgün çalışan bir aygıtta desteklenir. İçinde bir veya iki hello denetleyicilerinin çalışmıyor bir aygıtta desteklenmiyor.**</span><span class="sxs-lookup"><span data-stu-id="b479c-126">**Maintenance mode is only supported on a properly functioning device. It is not supported on a device in which one or both of hello controllers are not functioning.**</span></span>


### <a name="recovery-mode"></a><span data-ttu-id="b479c-127">Kurtarma moduna</span><span class="sxs-lookup"><span data-stu-id="b479c-127">Recovery mode</span></span>

<span data-ttu-id="b479c-128">Kurtarma moduna "Ağ desteği ile Windows güvenli modda" olarak tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="b479c-128">Recovery mode can be described as "Windows Safe Mode with network support".</span></span> <span data-ttu-id="b479c-129">Kurtarma moduna hello Microsoft Support ekibi prosese ve bunları tooperform tanılama hello sistemde sağlar.</span><span class="sxs-lookup"><span data-stu-id="b479c-129">Recovery mode engages hello Microsoft Support team and allows them tooperform diagnostics on hello system.</span></span> <span data-ttu-id="b479c-130">Merhaba birincil kurtarma moduna tooretrieve hello sistem günlüklerini hedefidir.</span><span class="sxs-lookup"><span data-stu-id="b479c-130">hello primary goal of recovery mode is tooretrieve hello system logs.</span></span>

<span data-ttu-id="b479c-131">Sisteminizi kurtarma moduna girer, sonraki adımlar için Microsoft Support başvurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b479c-131">If your system goes into recovery mode, you should contact Microsoft Support for next steps.</span></span> <span data-ttu-id="b479c-132">Daha fazla bilgi için çok Git[Microsoft Destek birimine başvurun](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="b479c-132">For more information, go too[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b479c-133">**Kurtarma modunda hello aygıt yerleştirilemiyor. Merhaba aygıt hatalı bir durumda, kurtarma moduna tooget hello aygıt Microsoft Support personeli inceleyebilirsiniz onu bir duruma çalışır.**</span><span class="sxs-lookup"><span data-stu-id="b479c-133">**You cannot place hello device in recovery mode. If hello device is in a bad state, recovery mode tries tooget hello device into a state in which Microsoft Support personnel can examine it.**</span></span>

## <a name="determine-storsimple-device-mode"></a><span data-ttu-id="b479c-134">StorSimple cihaz modunu belirler</span><span class="sxs-lookup"><span data-stu-id="b479c-134">Determine StorSimple device mode</span></span>

#### <a name="toodetermine-hello-current-device-mode"></a><span data-ttu-id="b479c-135">toodetermine hello geçerli aygıt modu</span><span class="sxs-lookup"><span data-stu-id="b479c-135">toodetermine hello current device mode</span></span>

1. <span data-ttu-id="b479c-136">Merhaba adımları izleyerek toohello cihaz seri konsoluna oturum [kullanım PuTTY tooconnect toohello cihaz seri konsoluna](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="b479c-136">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="b479c-137">Merhaba başlık iletisi hello seri konsol menüsünde hello cihazın bakın.</span><span class="sxs-lookup"><span data-stu-id="b479c-137">Look at hello banner message in hello serial console menu of hello device.</span></span> <span data-ttu-id="b479c-138">Bu ileti açıkça hello cihazın Bakım veya kurtarma modunda olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="b479c-138">This message explicitly indicates whether hello device is in maintenance or recovery mode.</span></span> <span data-ttu-id="b479c-139">Selamlama iletisine toohello sistem modu ilgili belirli bir bilgi içermiyorsa hello aygıt normal modda çalışır.</span><span class="sxs-lookup"><span data-stu-id="b479c-139">If hello message does not contain any specific information pertaining toohello system mode, hello device is in normal mode.</span></span>

## <a name="change-hello-storsimple-device-mode"></a><span data-ttu-id="b479c-140">Merhaba StorSimple cihaz modunu değiştirme</span><span class="sxs-lookup"><span data-stu-id="b479c-140">Change hello StorSimple device mode</span></span>

<span data-ttu-id="b479c-141">Merhaba StorSimple cihazı bakım modundan (normal modda) tooperform bakım yerleştirin veya Bakım modu güncelleştirmeleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b479c-141">You can place hello StorSimple device into maintenance mode (from normal mode) tooperform maintenance or install maintenance mode updates.</span></span> <span data-ttu-id="b479c-142">Aşağıdaki yordamlar tooenter veya çıkış Bakım modu hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="b479c-142">Perform hello following procedures tooenter or exit maintenance mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b479c-143">Bakım modu girmeden önce hello erişerek her iki cihaz denetleyicilerinin sağlıklı olduğunu doğrula **Aygıt Ayarları > donanım durumu** aygıtınızın hello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="b479c-143">Before entering maintenance mode, verify that both device controllers are healthy by accessing hello **Device settings > Hardware health** for your device in hello Azure portal.</span></span> <span data-ttu-id="b479c-144">Bir veya iki hello denetleyicisi iyi durumda olmayan, Microsoft Support hello sonraki adımlar için başvurun.</span><span class="sxs-lookup"><span data-stu-id="b479c-144">If one or both hello controllers are not healthy, contact Microsoft Support for hello next steps.</span></span> <span data-ttu-id="b479c-145">Daha fazla bilgi için çok Git[Microsoft Destek birimine başvurun](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="b479c-145">For more information, go too[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>
 

#### <a name="tooenter-maintenance-mode"></a><span data-ttu-id="b479c-146">tooenter Bakım modu</span><span class="sxs-lookup"><span data-stu-id="b479c-146">tooenter maintenance mode</span></span>

1. <span data-ttu-id="b479c-147">Merhaba adımları izleyerek toohello cihaz seri konsoluna oturum [kullanım PuTTY tooconnect toohello cihaz seri konsoluna](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="b479c-147">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="b479c-148">Merhaba seri konsol menüsünde seçeneği 1, **oturum oturum tam erişim**.</span><span class="sxs-lookup"><span data-stu-id="b479c-148">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="b479c-149">İstendiğinde, hello sağlayın **cihaz Yöneticisi parolası**.</span><span class="sxs-lookup"><span data-stu-id="b479c-149">When prompted, provide hello **device administrator password**.</span></span> <span data-ttu-id="b479c-150">Merhaba varsayılan parola: `Password1`.</span><span class="sxs-lookup"><span data-stu-id="b479c-150">hello default password is: `Password1`.</span></span>
3. <span data-ttu-id="b479c-151">Merhaba komut istemine yazın</span><span class="sxs-lookup"><span data-stu-id="b479c-151">At hello command prompt, type</span></span> 
   
    `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="b479c-152">Bu Bakım modu bildiren bir uyarı iletisi tüm g/ç istekleri kesintiye ve hello bağlantı toohello Azure portal sever ve onaylamanız istenir görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b479c-152">You will see a warning message telling you that maintenance mode will disrupt all I/O requests and sever hello connection toohello Azure portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="b479c-153">Tür **Y** tooenter Bakım modu.</span><span class="sxs-lookup"><span data-stu-id="b479c-153">Type **Y** tooenter maintenance mode.</span></span>
5. <span data-ttu-id="b479c-154">Hem denetleyicileri yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="b479c-154">Both controllers will restart.</span></span> <span data-ttu-id="b479c-155">Merhaba yeniden başlatma tamamlandıktan sonra hello seri konsol başlık hello aygıt bakım modunda olduğundan belirtir.</span><span class="sxs-lookup"><span data-stu-id="b479c-155">When hello restart is complete, hello serial console banner will indicate that hello device is in maintenance mode.</span></span> <span data-ttu-id="b479c-156">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b479c-156">A sample output is shown below.</span></span>

```
    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Controller0>Enter-HcsMaintenanceMode
    Checking device state...

    In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>

```

#### <a name="tooexit-maintenance-mode"></a><span data-ttu-id="b479c-157">tooexit Bakım modu</span><span class="sxs-lookup"><span data-stu-id="b479c-157">tooexit maintenance mode</span></span>

1. <span data-ttu-id="b479c-158">Toohello cihaz seri konsoluna oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b479c-158">Log on toohello device serial console.</span></span> <span data-ttu-id="b479c-159">Cihazınızı bakım modunda olduğundan hello başlık iletisi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b479c-159">Verify from hello banner message that your device is in maintenance mode.</span></span>
2. <span data-ttu-id="b479c-160">Merhaba komut satırına aşağıdakini yazın:</span><span class="sxs-lookup"><span data-stu-id="b479c-160">At hello command prompt, type:</span></span>
   
    `Exit-HcsMaintenanceMode`
3. <span data-ttu-id="b479c-161">Bir uyarı iletisi ve bir onay iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b479c-161">A warning message and a confirmation message will appear.</span></span> <span data-ttu-id="b479c-162">Tür **Y** tooexit Bakım modu.</span><span class="sxs-lookup"><span data-stu-id="b479c-162">Type **Y** tooexit maintenance mode.</span></span>
4. <span data-ttu-id="b479c-163">Hem denetleyicileri yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="b479c-163">Both controllers will restart.</span></span> <span data-ttu-id="b479c-164">Merhaba yeniden başlatma tamamlandıktan sonra hello seri konsol başlık hello aygıtın normal modda gösterir.</span><span class="sxs-lookup"><span data-stu-id="b479c-164">When hello restart is complete, hello serial console banner indicates that hello device is in normal mode.</span></span> <span data-ttu-id="b479c-165">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b479c-165">A sample output is shown below.</span></span>

```
    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0
    ---------------------------------------------------------------

    Controller0>Exit-HcsMaintenanceMode
    Checking device state...

    Before exiting maintenance mode, ensure that any updates that are required on both controllers have been applied. Failure tooinstall on each controller could result in data corruption. Exiting maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooexit maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Active
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>
```

## <a name="next-steps"></a><span data-ttu-id="b479c-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b479c-166">Next steps</span></span>

<span data-ttu-id="b479c-167">Nasıl çok öğrenin[normal ve Bakım modu güncelleştirmeleri uygulamak](storsimple-update-device.md) , StorSimple Cihazınızda.</span><span class="sxs-lookup"><span data-stu-id="b479c-167">Learn how too[apply normal and maintenance mode updates](storsimple-update-device.md) on your StorSimple device.</span></span>

