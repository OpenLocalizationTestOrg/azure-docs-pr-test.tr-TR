---
title: "StorSimple Cihazınızı güncelleştirin | Microsoft Docs"
description: "StorSimple güncelleştirme özelliğini normal ve Bakım modu güncelleştirmeleri ve düzeltmeleri yüklemeniz için nasıl kullanılacağını açıklar."
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
ms.openlocfilehash: 8490110942741b049b6d44ac93697303cef40e8a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="update-your-storsimple-8000-series-device"></a><span data-ttu-id="585ad-103">StorSimple 8000 serisi Cihazınızı güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="585ad-103">Update your StorSimple 8000 Series device</span></span>
## <a name="overview"></a><span data-ttu-id="585ad-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="585ad-104">Overview</span></span>
<span data-ttu-id="585ad-105">StorSimple güncelleştirme özellikler kolayca StorSimple cihazınız güncel tutmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="585ad-105">The StorSimple updates features allow you to easily keep your StorSimple device up-to-date.</span></span> <span data-ttu-id="585ad-106">Güncelleştirme türüne bağlı olarak, Windows PowerShell arabirimi üzerinden veya Klasik Azure Portalı aracılığıyla aygıta güncelleştirmelerini uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="585ad-106">Depending on the update type, you can apply updates to the device via the Azure classic portal or via the Windows PowerShell interface.</span></span> <span data-ttu-id="585ad-107">Bu öğretici, güncelleştirme türlerini ve bunların her birine yüklemek açıklar.</span><span class="sxs-lookup"><span data-stu-id="585ad-107">This tutorial describes the update types and how to install each of them.</span></span>

<span data-ttu-id="585ad-108">Cihaz güncelleştirmeleri iki tür uygulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="585ad-108">You can apply two types of device updates:</span></span> 

* <span data-ttu-id="585ad-109">Normal (veya Normal modda) güncelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="585ad-109">Regular (or Normal mode) updates</span></span>
* <span data-ttu-id="585ad-110">Bakım modu güncelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="585ad-110">Maintenance mode updates</span></span>

<span data-ttu-id="585ad-111">Klasik Azure portalı veya Windows PowerShell aracılığıyla düzenli olarak güncelleştirmeleri yükleyebilirsiniz; Ancak, Bakım modu güncelleştirmeleri yüklemek için Windows PowerShell kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="585ad-111">You can install regular updates via the Azure classic portal or Windows PowerShell; however, you must use Windows PowerShell to install Maintenance mode updates.</span></span> 

<span data-ttu-id="585ad-112">Ayrıca, aşağıda açıklanan her güncelleştirme türüdür.</span><span class="sxs-lookup"><span data-stu-id="585ad-112">Each update type is described separately, below.</span></span>

### <a name="regular-updates"></a><span data-ttu-id="585ad-113">Düzenli olarak güncelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="585ad-113">Regular updates</span></span>
<span data-ttu-id="585ad-114">Normal cihaz Normal modda olduğunda, yüklenebilen benzer güncelleştirmelerdir.</span><span class="sxs-lookup"><span data-stu-id="585ad-114">Regular updates are non-disruptive updates that can be installed when the device is in Normal mode.</span></span> <span data-ttu-id="585ad-115">Bu güncelleştirmeleri Microsoft Update Web sitesi aracılığıyla her aygıt denetleyiciye uygulanır.</span><span class="sxs-lookup"><span data-stu-id="585ad-115">These updates are applied through the Microsoft Update website to each device controller.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="585ad-116">Denetleyici yük devretmesi güncelleştirme işlemi sırasında ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="585ad-116">A controller failover may occur during the update process.</span></span> <span data-ttu-id="585ad-117">Ancak, bu sistem kullanılabilirliğini veya işlem etkilemez.</span><span class="sxs-lookup"><span data-stu-id="585ad-117">However, this will not affect system availability or operation.</span></span>
> 
> 

* <span data-ttu-id="585ad-118">Klasik Azure Portalı aracılığıyla normal güncelleştirmelerinin nasıl yükleneceği hakkında daha fazla bilgi için bkz: [Klasik Azure Portalı aracılığıyla normal güncelleştirmelerini yükleme](#install-regular-updates-via-the-azure-classic-portal).</span><span class="sxs-lookup"><span data-stu-id="585ad-118">For details on how to install regular updates via the Azure classic portal, see [Install regular updates via the Azure classic portal](#install-regular-updates-via-the-azure-classic-portal).</span></span>
* <span data-ttu-id="585ad-119">StorSimple için Windows PowerShell aracılığıyla düzenli olarak güncelleştirmeleri de yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="585ad-119">You can also install regular updates via Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="585ad-120">Ayrıntılar için bkz [StorSimple için Windows PowerShell aracılığıyla normal güncelleştirmelerini yükleme](#install-regular-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="585ad-120">For details, see [Install regular updates via Windows PowerShell for StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span></span>

### <a name="maintenance-mode-updates"></a><span data-ttu-id="585ad-121">Bakım modu güncelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="585ad-121">Maintenance mode updates</span></span>
<span data-ttu-id="585ad-122">Bakım modu kesintiye uğratan disk bellenim yükseltmeleri gibi güncelleştirmelerdir.</span><span class="sxs-lookup"><span data-stu-id="585ad-122">Maintenance Mode updates are disruptive updates such as disk firmware upgrades.</span></span> <span data-ttu-id="585ad-123">Bu güncelleştirmeler bakım moduna aygıta gerektirir.</span><span class="sxs-lookup"><span data-stu-id="585ad-123">These updates require the device to be put into Maintenance mode.</span></span> <span data-ttu-id="585ad-124">Ayrıntılar için bkz [2. adım: girin Bakım modu](#step2).</span><span class="sxs-lookup"><span data-stu-id="585ad-124">For details, see [Step 2: Enter Maintenance mode](#step2).</span></span> <span data-ttu-id="585ad-125">Bakım modu güncelleştirmeleri yüklemek için Azure Klasik portalı kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="585ad-125">You cannot use the Azure classic portal to install Maintenance mode updates.</span></span> <span data-ttu-id="585ad-126">Bunun yerine, StorSimple için Windows PowerShell kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="585ad-126">Instead, you must use Windows PowerShell for StorSimple.</span></span> 

<span data-ttu-id="585ad-127">Bakım modu güncelleştirmelerinin nasıl yükleneceği hakkında daha fazla bilgi için bkz: [yükleme Bakım modu güncelleştirmeleri StorSimple için Windows PowerShell aracılığıyla](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="585ad-127">For details on how to install Maintenance mode updates, see [Install Maintenance mode updates via Windows PowerShell for StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="585ad-128">Bakım modu güncelleştirmeleri ayrı ayrı her denetleyiciye uygulanmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="585ad-128">Maintenance mode updates must be applied separately to each controller.</span></span> 
> 
> 

## <a name="install-regular-updates-via-the-azure-classic-portal"></a><span data-ttu-id="585ad-129">Klasik Azure Portalı aracılığıyla düzenli olarak güncelleştirmeleri yükle</span><span class="sxs-lookup"><span data-stu-id="585ad-129">Install regular updates via the Azure classic portal</span></span>
<span data-ttu-id="585ad-130">StorSimple Cihazınızı güncelleştirmeleri uygulamak için Klasik Azure portalını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="585ad-130">You can use the Azure classic portal to apply updates to your StorSimple device.</span></span>

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="585ad-131">StorSimple için Windows PowerShell aracılığıyla düzenli olarak güncelleştirmeleri yükle</span><span class="sxs-lookup"><span data-stu-id="585ad-131">Install regular updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="585ad-132">Alternatif olarak, normal (Normal modda) güncelleştirmeleri uygulamak için StorSimple için Windows PowerShell'i kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="585ad-132">Alternatively, you can use Windows PowerShell for StorSimple to apply regular (Normal mode) updates.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="585ad-133">StorSimple için Windows PowerShell kullanarak düzenli olarak güncelleştirmeleri yükleyebilmenize rağmen Klasik Azure Portalı aracılığıyla düzenli olarak güncelleştirmeleri yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="585ad-133">Although you can install regular updates using Windows PowerShell for StorSimple, we strongly recommend that you install regular updates through the Azure classic portal.</span></span> <span data-ttu-id="585ad-134">Güncelleştirme 1'den başlayarak, ön denetimleri portaldan güncelleştirmeleri yüklemeden önce gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="585ad-134">Beginning with Update 1, pre-checks will be performed prior to installing updates from the portal.</span></span> <span data-ttu-id="585ad-135">Bu ön denetimleri hatalarını önüne geçer ve daha sorunsuz bir deneyim emin olun.</span><span class="sxs-lookup"><span data-stu-id="585ad-135">These pre-checks will preempt failures and ensure a smoother experience.</span></span> 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="585ad-136">StorSimple için Windows PowerShell aracılığıyla Bakım modu güncelleştirmeleri yükle</span><span class="sxs-lookup"><span data-stu-id="585ad-136">Install Maintenance mode updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="585ad-137">StorSimple Cihazınızı Bakım modu güncelleştirmeleri uygulamak için StorSimple için Windows PowerShell kullanın.</span><span class="sxs-lookup"><span data-stu-id="585ad-137">You use Windows PowerShell for StorSimple to apply Maintenance mode updates to your StorSimple device.</span></span> <span data-ttu-id="585ad-138">Tüm g/ç istekleri bu modda duraklatıldı.</span><span class="sxs-lookup"><span data-stu-id="585ad-138">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="585ad-139">Geçici olmayan rasgele erişim belleği (NVRAM) gibi hizmetleri veya Küme hizmeti de durdurulur.</span><span class="sxs-lookup"><span data-stu-id="585ad-139">Services such as non-volatile random access memory (NVRAM) or the clustering service are also stopped.</span></span> <span data-ttu-id="585ad-140">Girin ya da bu modundan çıkmak hem denetleyicileri yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="585ad-140">Both controllers are rebooted when you enter or exit this mode.</span></span> <span data-ttu-id="585ad-141">Bu mod çıktığınızda, tüm hizmetleri devam eder ve iyi durumda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="585ad-141">When you exit this mode, all the services will resume and should be healthy.</span></span> <span data-ttu-id="585ad-142">(Bu işlem birkaç dakika sürebilir.)</span><span class="sxs-lookup"><span data-stu-id="585ad-142">(This may take a few minutes.)</span></span>

<span data-ttu-id="585ad-143">Bakım modu güncelleştirmeleri uygulamak gerekiyorsa, Klasik Azure Portalı aracılığıyla yüklenmesi gereken güncelleştirmelerin yüklü olduğundan uyarı alırsınız.</span><span class="sxs-lookup"><span data-stu-id="585ad-143">If you need to apply Maintenance mode updates, you will receive an alert through the Azure classic portal that you have updates that must be installed.</span></span> <span data-ttu-id="585ad-144">Bu uyarı güncelleştirmeleri yüklemek için StorSimple için Windows PowerShell kullanma yönergeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="585ad-144">This alert will include instructions for using Windows PowerShell for StorSimple to install the updates.</span></span> <span data-ttu-id="585ad-145">Cihazınızı güncelleştirdikten sonra aygıtın normal moduna geçmek için aynı yordamı kullanın.</span><span class="sxs-lookup"><span data-stu-id="585ad-145">After you update your device, use the same procedure to change the device to Regular mode.</span></span> <span data-ttu-id="585ad-146">Adım adım yönergeler için bkz: [4. adım: çıkış Bakım modu](#step4).</span><span class="sxs-lookup"><span data-stu-id="585ad-146">For step-by-step instructions, see [Step 4: Exit Maintenance mode](#step4).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="585ad-147">Bakım modu girmeden önce denetleyerek hem de cihaz denetleyicilerinin sağlıklı olduğunu doğrula **donanım durum** üzerinde **Bakım** Klasik Azure portalındaki sayfası.</span><span class="sxs-lookup"><span data-stu-id="585ad-147">Before entering Maintenance mode, verify that both device controllers are healthy by checking the **Hardware Status** on the **Maintenance** page in the Azure classic portal.</span></span> <span data-ttu-id="585ad-148">Denetleyicisi iyi durumda değil, Microsoft Support sonraki adımlar için başvurun.</span><span class="sxs-lookup"><span data-stu-id="585ad-148">If the controller is not healthy, contact Microsoft Support for the next steps.</span></span> <span data-ttu-id="585ad-149">Daha fazla bilgi için ilgili kişi Microsoft Desteği'ne gidin.</span><span class="sxs-lookup"><span data-stu-id="585ad-149">For more information, go to Contact Microsoft Support.</span></span> 
> * <span data-ttu-id="585ad-150">Bakım modunda olduğunda, önce bir denetleyici ve ardından diğer denetleyici güncelleştirmesini gerekir.</span><span class="sxs-lookup"><span data-stu-id="585ad-150">When you are in Maintenance mode, you need to apply the update first on one controller and then on the other controller.</span></span>
> 
> 

### <a name="step-1-connect-to-the-serial-console-a-namestep1"></a><span data-ttu-id="585ad-151">1. adım: seri konsoluna Bağlan<a name="step1"></span><span class="sxs-lookup"><span data-stu-id="585ad-151">Step 1: Connect to the serial console <a name="step1"></span></span>
<span data-ttu-id="585ad-152">İlk olarak, seri konsoluna erişmek için PuTTY gibi bir uygulama kullanın.</span><span class="sxs-lookup"><span data-stu-id="585ad-152">First, use an application such as PuTTY to access the serial console.</span></span> <span data-ttu-id="585ad-153">Aşağıdaki yordamda, seri konsoluna bağlanmak için PuTTY kullanın açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="585ad-153">The following procedure explains how to use PuTTY to connect to the serial console.</span></span>

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a><span data-ttu-id="585ad-154">2. adım: Bakım modu girin<a name="step2"></span><span class="sxs-lookup"><span data-stu-id="585ad-154">Step 2: Enter Maintenance mode <a name="step2"></span></span>
<span data-ttu-id="585ad-155">Konsola bağlandıktan sonra yüklemek ve bunları yüklemek için bakım moduna girmek için güncelleştirmeler olup olmadığını belirleyin.</span><span class="sxs-lookup"><span data-stu-id="585ad-155">After you connect to the console, determine whether there are updates to install, and enter Maintenance mode to install them.</span></span>

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a><span data-ttu-id="585ad-156">3. adım: güncellemelerinizi yükleme<a name="step3"></span><span class="sxs-lookup"><span data-stu-id="585ad-156">Step 3: Install your updates <a name="step3"></span></span>
<span data-ttu-id="585ad-157">Ardından, güncelleştirmelerinizi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="585ad-157">Next, install your updates.</span></span>

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a><span data-ttu-id="585ad-158">4. adım: Çıkış Bakım modu<a name="step4"></span><span class="sxs-lookup"><span data-stu-id="585ad-158">Step 4: Exit Maintenance mode <a name="step4"></span></span>
<span data-ttu-id="585ad-159">Son olarak, bakım modundan çıkın.</span><span class="sxs-lookup"><span data-stu-id="585ad-159">Finally, exit Maintenance mode.</span></span>

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="585ad-160">StorSimple için Windows PowerShell aracılığıyla düzeltmeleri yükleme</span><span class="sxs-lookup"><span data-stu-id="585ad-160">Install hotfixes via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="585ad-161">Microsoft Azure StorSimple güncelleştirmeleri, paylaşılan bir klasörden düzeltmeleri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="585ad-161">Unlike updates for Microsoft Azure StorSimple, hotfixes are installed from a shared folder.</span></span> <span data-ttu-id="585ad-162">Güncelleştirmelerinde olduğu gibi düzeltmeler iki tür vardır:</span><span class="sxs-lookup"><span data-stu-id="585ad-162">As with updates, there are two types of hotfixes:</span></span> 

* <span data-ttu-id="585ad-163">Normal düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="585ad-163">Regular hotfixes</span></span> 
* <span data-ttu-id="585ad-164">Bakım modu düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="585ad-164">Maintenance mode hotfixes</span></span>  

<span data-ttu-id="585ad-165">Aşağıdaki yordamlarda, StorSimple için Windows PowerShell normal ve Bakım modu düzeltmeleri yüklemeniz için nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="585ad-165">The following procedures explain how to use Windows PowerShell for StorSimple to install regular and Maintenance mode hotfixes.</span></span>

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-to-updates-if-you-perform-a-factory-reset-of-the-device"></a><span data-ttu-id="585ad-166">Bir cihazı fabrika ayarlarına gerçekleştirmek güncelleştirmeleri ne olur?</span><span class="sxs-lookup"><span data-stu-id="585ad-166">What happens to updates if you perform a factory reset of the device?</span></span>
<span data-ttu-id="585ad-167">Bir cihazı fabrika ayarlarına sıfırlarsanız tüm güncelleştirmeler kaybolur.</span><span class="sxs-lookup"><span data-stu-id="585ad-167">If a device is reset to factory settings, then all the updates are lost.</span></span> <span data-ttu-id="585ad-168">Fabrika sıfırlaması cihaz kayıtlı yapılandırıldıktan sonra Klasik Azure portalı ve/veya Windows PowerShell aracılığıyla güncelleştirmeleri StorSimple için el ile yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="585ad-168">After the factory-reset device is registered and configured, you will need to manually install updates through the Azure classic portal and/or Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="585ad-169">Fabrika sıfırlaması hakkında daha fazla bilgi için bkz: [cihazı fabrika varsayılan ayarlarına sıfırlama](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="585ad-169">For more information about factory reset, see [Reset the device to factory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>

## <a name="next-steps"></a><span data-ttu-id="585ad-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="585ad-170">Next steps</span></span>
* <span data-ttu-id="585ad-171">Daha fazla bilgi edinmek [StorSimple Cihazınızı yönetmek için StorSimple için Windows PowerShell kullanarak](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="585ad-171">Learn more about [using Windows PowerShell for StorSimple to administer your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="585ad-172">Daha fazla bilgi edinmek [StorSimple Cihazınızı yönetmek için StorSimple Yöneticisi hizmetini kullanma](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="585ad-172">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

