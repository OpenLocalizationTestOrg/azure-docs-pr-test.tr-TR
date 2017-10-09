---
title: "aaaUpdate StorSimple Cihazınızı | Microsoft Docs"
description: "Toouse hello StorSimple güncelleştirme nasıl özelliği tooinstall normal ve Bakım modu güncelleştirmeleri ve düzeltmeleri açıklanmaktadır."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 786059f5-2a38-4105-941d-0860ce4ac515
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: v-sharos
ms.openlocfilehash: 05acf05c8fc89bbb4343f67ad103235bbe3dba0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-storsimple-8000-series-device"></a><span data-ttu-id="54865-103">StorSimple 8000 serisi Cihazınızı güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="54865-103">Update your StorSimple 8000 Series device</span></span>
## <a name="overview"></a><span data-ttu-id="54865-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="54865-104">Overview</span></span>
<span data-ttu-id="54865-105">Merhaba StorSimple güncelleştirmeleri özellikleri izin tooeasily StorSimple cihazınız güncel tutun.</span><span class="sxs-lookup"><span data-stu-id="54865-105">hello StorSimple updates features allow you tooeasily keep your StorSimple device up-to-date.</span></span> <span data-ttu-id="54865-106">Merhaba güncelleştirme türüne bağlı olarak, güncelleştirmeleri toohello aygıt hello Windows PowerShell arabirimi üzerinden veya hello Klasik Azure Portalı aracılığıyla uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54865-106">Depending on hello update type, you can apply updates toohello device via hello Azure classic portal or via hello Windows PowerShell interface.</span></span> <span data-ttu-id="54865-107">Bu öğretici hello güncelleştirme türlerini açıklar ve nasıl tooinstall her biri.</span><span class="sxs-lookup"><span data-stu-id="54865-107">This tutorial describes hello update types and how tooinstall each of them.</span></span>

<span data-ttu-id="54865-108">Cihaz güncelleştirmeleri iki tür uygulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="54865-108">You can apply two types of device updates:</span></span> 

* <span data-ttu-id="54865-109">Normal (veya Normal modda) güncelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="54865-109">Regular (or Normal mode) updates</span></span>
* <span data-ttu-id="54865-110">Bakım modu güncelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="54865-110">Maintenance mode updates</span></span>

<span data-ttu-id="54865-111">Merhaba Klasik Azure portalı veya Windows PowerShell aracılığıyla düzenli olarak güncelleştirmeleri yükleyebilirsiniz; Ancak, Windows PowerShell tooinstall Bakım modu güncelleştirmeleri kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="54865-111">You can install regular updates via hello Azure classic portal or Windows PowerShell; however, you must use Windows PowerShell tooinstall Maintenance mode updates.</span></span> 

<span data-ttu-id="54865-112">Ayrıca, aşağıda açıklanan her güncelleştirme türüdür.</span><span class="sxs-lookup"><span data-stu-id="54865-112">Each update type is described separately, below.</span></span>

### <a name="regular-updates"></a><span data-ttu-id="54865-113">Düzenli olarak güncelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="54865-113">Regular updates</span></span>
<span data-ttu-id="54865-114">Normal hello cihaz Normal modda olduğunda, yüklenebilen benzer güncelleştirmelerdir.</span><span class="sxs-lookup"><span data-stu-id="54865-114">Regular updates are non-disruptive updates that can be installed when hello device is in Normal mode.</span></span> <span data-ttu-id="54865-115">Bu güncelleştirmeler hello Microsoft Update Web sitesini tooeach aygıt denetleyicisi uygulanır.</span><span class="sxs-lookup"><span data-stu-id="54865-115">These updates are applied through hello Microsoft Update website tooeach device controller.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="54865-116">Denetleyici yük devretmesi hello güncelleştirme işlemi sırasında ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="54865-116">A controller failover may occur during hello update process.</span></span> <span data-ttu-id="54865-117">Ancak, bu sistem kullanılabilirliğini veya işlem etkilemez.</span><span class="sxs-lookup"><span data-stu-id="54865-117">However, this will not affect system availability or operation.</span></span>
> 
> 

* <span data-ttu-id="54865-118">Nasıl tooinstall normal hello Klasik Azure portalı güncelleştirmeleri hakkında daha fazla bilgi için bkz: [hello Klasik Azure Portalı aracılığıyla normal güncelleştirmelerini yükleme](#install-regular-updates-via-the-azure-classic-portal).</span><span class="sxs-lookup"><span data-stu-id="54865-118">For details on how tooinstall regular updates via hello Azure classic portal, see [Install regular updates via hello Azure classic portal](#install-regular-updates-via-the-azure-classic-portal).</span></span>
* <span data-ttu-id="54865-119">StorSimple için Windows PowerShell aracılığıyla düzenli olarak güncelleştirmeleri de yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54865-119">You can also install regular updates via Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="54865-120">Ayrıntılar için bkz [StorSimple için Windows PowerShell aracılığıyla normal güncelleştirmelerini yükleme](#install-regular-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="54865-120">For details, see [Install regular updates via Windows PowerShell for StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span></span>

### <a name="maintenance-mode-updates"></a><span data-ttu-id="54865-121">Bakım modu güncelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="54865-121">Maintenance mode updates</span></span>
<span data-ttu-id="54865-122">Bakım modu kesintiye uğratan disk bellenim yükseltmeleri gibi güncelleştirmelerdir.</span><span class="sxs-lookup"><span data-stu-id="54865-122">Maintenance Mode updates are disruptive updates such as disk firmware upgrades.</span></span> <span data-ttu-id="54865-123">Bu güncelleştirmeler bakım moduna hello aygıt toobe gerektirir.</span><span class="sxs-lookup"><span data-stu-id="54865-123">These updates require hello device toobe put into Maintenance mode.</span></span> <span data-ttu-id="54865-124">Ayrıntılar için bkz [2. adım: girin Bakım modu](#step2).</span><span class="sxs-lookup"><span data-stu-id="54865-124">For details, see [Step 2: Enter Maintenance mode](#step2).</span></span> <span data-ttu-id="54865-125">Hello Azure Klasik portalı tooinstall Bakım modu güncelleştirmelerini kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="54865-125">You cannot use hello Azure classic portal tooinstall Maintenance mode updates.</span></span> <span data-ttu-id="54865-126">Bunun yerine, StorSimple için Windows PowerShell kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="54865-126">Instead, you must use Windows PowerShell for StorSimple.</span></span> 

<span data-ttu-id="54865-127">Güncelleştirme biçimini tooinstall Bakım modu hakkında daha fazla bilgi için bkz [yükleme Bakım modu güncelleştirmeleri StorSimple için Windows PowerShell aracılığıyla](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="54865-127">For details on how tooinstall Maintenance mode updates, see [Install Maintenance mode updates via Windows PowerShell for StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54865-128">Bakım modu güncelleştirmeleri olmalıdır tooeach denetleyicisi ayrı olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="54865-128">Maintenance mode updates must be applied separately tooeach controller.</span></span> 
> 
> 

## <a name="install-regular-updates-via-hello-azure-classic-portal"></a><span data-ttu-id="54865-129">Merhaba Klasik Azure Portalı aracılığıyla düzenli olarak güncelleştirmeleri yükle</span><span class="sxs-lookup"><span data-stu-id="54865-129">Install regular updates via hello Azure classic portal</span></span>
<span data-ttu-id="54865-130">Hello Azure Klasik portalı tooapply güncelleştirmeleri tooyour StorSimple cihazı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54865-130">You can use hello Azure classic portal tooapply updates tooyour StorSimple device.</span></span>

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="54865-131">StorSimple için Windows PowerShell aracılığıyla düzenli olarak güncelleştirmeleri yükle</span><span class="sxs-lookup"><span data-stu-id="54865-131">Install regular updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="54865-132">Alternatif olarak, StorSimple tooapply normal (Normal modda) güncelleştirmeleri için Windows PowerShell'i kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54865-132">Alternatively, you can use Windows PowerShell for StorSimple tooapply regular (Normal mode) updates.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54865-133">StorSimple için Windows PowerShell kullanarak düzenli olarak güncelleştirmeleri yükleyebilirsiniz, ancak düzenli olarak güncelleştirmeleri hello Klasik Azure Portalı aracılığıyla yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="54865-133">Although you can install regular updates using Windows PowerShell for StorSimple, we strongly recommend that you install regular updates through hello Azure classic portal.</span></span> <span data-ttu-id="54865-134">Güncelleştirme 1'den başlayarak, ön denetimleri gerçekleştirilen önceki tooinstalling güncelleştirmeleri hello portalından olacaktır.</span><span class="sxs-lookup"><span data-stu-id="54865-134">Beginning with Update 1, pre-checks will be performed prior tooinstalling updates from hello portal.</span></span> <span data-ttu-id="54865-135">Bu ön denetimleri hatalarını önüne geçer ve daha sorunsuz bir deneyim emin olun.</span><span class="sxs-lookup"><span data-stu-id="54865-135">These pre-checks will preempt failures and ensure a smoother experience.</span></span> 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="54865-136">StorSimple için Windows PowerShell aracılığıyla Bakım modu güncelleştirmeleri yükle</span><span class="sxs-lookup"><span data-stu-id="54865-136">Install Maintenance mode updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="54865-137">StorSimple tooapply Bakım modu güncelleştirmeleri tooyour StorSimple cihazı için Windows PowerShell kullanın.</span><span class="sxs-lookup"><span data-stu-id="54865-137">You use Windows PowerShell for StorSimple tooapply Maintenance mode updates tooyour StorSimple device.</span></span> <span data-ttu-id="54865-138">Tüm g/ç istekleri bu modda duraklatıldı.</span><span class="sxs-lookup"><span data-stu-id="54865-138">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="54865-139">Geçici olmayan rasgele erişim belleği (NVRAM) veya hizmet kümeleme hello gibi hizmetleri de durdurulur.</span><span class="sxs-lookup"><span data-stu-id="54865-139">Services such as non-volatile random access memory (NVRAM) or hello clustering service are also stopped.</span></span> <span data-ttu-id="54865-140">Girin ya da bu modundan çıkmak hem denetleyicileri yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="54865-140">Both controllers are rebooted when you enter or exit this mode.</span></span> <span data-ttu-id="54865-141">Bu mod çıktığınızda, tüm hello Hizmetleri devam eder ve iyi durumda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="54865-141">When you exit this mode, all hello services will resume and should be healthy.</span></span> <span data-ttu-id="54865-142">(Bu işlem birkaç dakika sürebilir.)</span><span class="sxs-lookup"><span data-stu-id="54865-142">(This may take a few minutes.)</span></span>

<span data-ttu-id="54865-143">Tooapply Bakım modu güncelleştirmeleri gerekiyorsa, yüklenmesi gereken güncelleştirmelerin yüklü olduğundan hello Klasik Azure Portalı aracılığıyla bir uyarı alırsınız.</span><span class="sxs-lookup"><span data-stu-id="54865-143">If you need tooapply Maintenance mode updates, you will receive an alert through hello Azure classic portal that you have updates that must be installed.</span></span> <span data-ttu-id="54865-144">Bu uyarı StorSimple tooinstall hello güncelleştirmeleri için Windows PowerShell kullanma yönergeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="54865-144">This alert will include instructions for using Windows PowerShell for StorSimple tooinstall hello updates.</span></span> <span data-ttu-id="54865-145">Cihazınızı güncelleştirmeden sonra kullanım hello aynı yordamı toochange hello aygıt tooRegular modu.</span><span class="sxs-lookup"><span data-stu-id="54865-145">After you update your device, use hello same procedure toochange hello device tooRegular mode.</span></span> <span data-ttu-id="54865-146">Adım adım yönergeler için bkz: [4. adım: çıkış Bakım modu](#step4).</span><span class="sxs-lookup"><span data-stu-id="54865-146">For step-by-step instructions, see [Step 4: Exit Maintenance mode](#step4).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="54865-147">Bakım modu girmeden önce hello denetleyerek hem de cihaz denetleyicilerinin sağlıklı olduğunu doğrula **donanım durumu** hello üzerinde **Bakım** hello Klasik Azure portalı sayfasında.</span><span class="sxs-lookup"><span data-stu-id="54865-147">Before entering Maintenance mode, verify that both device controllers are healthy by checking hello **Hardware Status** on hello **Maintenance** page in hello Azure classic portal.</span></span> <span data-ttu-id="54865-148">Merhaba denetleyicisi iyi durumda değil, Microsoft Support hello sonraki adımlar için başvurun.</span><span class="sxs-lookup"><span data-stu-id="54865-148">If hello controller is not healthy, contact Microsoft Support for hello next steps.</span></span> <span data-ttu-id="54865-149">Daha fazla bilgi için Microsoft Support tooContact gidin.</span><span class="sxs-lookup"><span data-stu-id="54865-149">For more information, go tooContact Microsoft Support.</span></span> 
> * <span data-ttu-id="54865-150">Bakım modunda olduğunda tooapply gereken bir denetleyicisine ilk güncelleştirme hello ve ardından üzerindeki diğer denetleyicisi hello.</span><span class="sxs-lookup"><span data-stu-id="54865-150">When you are in Maintenance mode, you need tooapply hello update first on one controller and then on hello other controller.</span></span>
> 
> 

### <a name="step-1-connect-toohello-serial-console-a-namestep1"></a><span data-ttu-id="54865-151">1. adım: toohello seri konsol bağlantısı<a name="step1"></span><span class="sxs-lookup"><span data-stu-id="54865-151">Step 1: Connect toohello serial console <a name="step1"></span></span>
<span data-ttu-id="54865-152">İlk olarak, seri konsol PuTTY tooaccess hello gibi bir uygulama kullanın.</span><span class="sxs-lookup"><span data-stu-id="54865-152">First, use an application such as PuTTY tooaccess hello serial console.</span></span> <span data-ttu-id="54865-153">Merhaba aşağıdaki yordam açıklanmaktadır nasıl toouse PuTTY tooconnect toohello seri konsol.</span><span class="sxs-lookup"><span data-stu-id="54865-153">hello following procedure explains how toouse PuTTY tooconnect toohello serial console.</span></span>

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a><span data-ttu-id="54865-154">2. adım: Bakım modu girin<a name="step2"></span><span class="sxs-lookup"><span data-stu-id="54865-154">Step 2: Enter Maintenance mode <a name="step2"></span></span>
<span data-ttu-id="54865-155">Toohello konsol bağlandıktan sonra güncelleştirmelerinin tooinstall olup olmadığını belirlemek ve Bakım modu tooinstall girin bunları.</span><span class="sxs-lookup"><span data-stu-id="54865-155">After you connect toohello console, determine whether there are updates tooinstall, and enter Maintenance mode tooinstall them.</span></span>

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a><span data-ttu-id="54865-156">3. adım: güncellemelerinizi yükleme<a name="step3"></span><span class="sxs-lookup"><span data-stu-id="54865-156">Step 3: Install your updates <a name="step3"></span></span>
<span data-ttu-id="54865-157">Ardından, güncelleştirmelerinizi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="54865-157">Next, install your updates.</span></span>

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a><span data-ttu-id="54865-158">4. adım: Çıkış Bakım modu<a name="step4"></span><span class="sxs-lookup"><span data-stu-id="54865-158">Step 4: Exit Maintenance mode <a name="step4"></span></span>
<span data-ttu-id="54865-159">Son olarak, bakım modundan çıkın.</span><span class="sxs-lookup"><span data-stu-id="54865-159">Finally, exit Maintenance mode.</span></span>

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="54865-160">StorSimple için Windows PowerShell aracılığıyla düzeltmeleri yükleme</span><span class="sxs-lookup"><span data-stu-id="54865-160">Install hotfixes via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="54865-161">Microsoft Azure StorSimple güncelleştirmeleri, paylaşılan bir klasörden düzeltmeleri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="54865-161">Unlike updates for Microsoft Azure StorSimple, hotfixes are installed from a shared folder.</span></span> <span data-ttu-id="54865-162">Güncelleştirmelerinde olduğu gibi düzeltmeler iki tür vardır:</span><span class="sxs-lookup"><span data-stu-id="54865-162">As with updates, there are two types of hotfixes:</span></span> 

* <span data-ttu-id="54865-163">Normal düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="54865-163">Regular hotfixes</span></span> 
* <span data-ttu-id="54865-164">Bakım modu düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="54865-164">Maintenance mode hotfixes</span></span>  

<span data-ttu-id="54865-165">Merhaba aşağıdaki yordamlar açıklamaktadır nasıl toouse Windows PowerShell StorSimple tooinstall normal ve Bakım modu düzeltmeler.</span><span class="sxs-lookup"><span data-stu-id="54865-165">hello following procedures explain how toouse Windows PowerShell for StorSimple tooinstall regular and Maintenance mode hotfixes.</span></span>

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-tooupdates-if-you-perform-a-factory-reset-of-hello-device"></a><span data-ttu-id="54865-166">Merhaba aygıtın bir Fabrika gerçekleştirirseniz tooupdates sıfırlama ne olur?</span><span class="sxs-lookup"><span data-stu-id="54865-166">What happens tooupdates if you perform a factory reset of hello device?</span></span>
<span data-ttu-id="54865-167">Bir aygıt toofactory ayarlarını sıfırla ise, tüm hello güncelleştirmeleri kaybolur.</span><span class="sxs-lookup"><span data-stu-id="54865-167">If a device is reset toofactory settings, then all hello updates are lost.</span></span> <span data-ttu-id="54865-168">Merhaba Fabrika sıfırlaması cihaz kayıtlı yapılandırıldıktan sonra StorSimple için toomanually hello Klasik Azure portalı ve/veya Windows PowerShell aracılığıyla güncelleştirmeleri yükleme gerekir.</span><span class="sxs-lookup"><span data-stu-id="54865-168">After hello factory-reset device is registered and configured, you will need toomanually install updates through hello Azure classic portal and/or Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="54865-169">Fabrika sıfırlaması hakkında daha fazla bilgi için bkz: [hello aygıt toofactory varsayılan ayarlara](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="54865-169">For more information about factory reset, see [Reset hello device toofactory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>

## <a name="next-steps"></a><span data-ttu-id="54865-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="54865-170">Next steps</span></span>
* <span data-ttu-id="54865-171">Daha fazla bilgi edinmek [StorSimple Cihazınızı StorSimple tooadminister için Windows PowerShell kullanarak](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="54865-171">Learn more about [using Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="54865-172">Daha fazla bilgi edinmek [kullanarak, StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="54865-172">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

