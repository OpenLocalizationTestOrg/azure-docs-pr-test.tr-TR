---
title: "Veri 0 aaaModify StorSimple 8000 serisi cihazın ayarlarının | Microsoft Docs"
description: "Bilgi nasıl StorSimple tooreconfigure için Windows PowerShell toouse hello DATA 0 ağ arabirimindeki, StorSimple Cihazınızda."
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
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: 2d3bdd3675017be86def45a81d94b6c03fc61da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-data-0-network-interface-settings-on-your-storsimple-8000-series-device"></a><span data-ttu-id="46473-103">StorSimple 8000 serisi aygıtınızda Hello veri 0 ağ arabirimi ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="46473-103">Modify hello DATA 0 network interface settings on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="46473-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="46473-104">Overview</span></span>

<span data-ttu-id="46473-105">Microsoft Azure StorSimple Cihazınızı veri 0'dan altı ağ arabirimi bulunur tooDATA 5.</span><span class="sxs-lookup"><span data-stu-id="46473-105">Your Microsoft Azure StorSimple device has six network interfaces, from DATA 0 tooDATA 5.</span></span> <span data-ttu-id="46473-106">Merhaba arabirimi daima hello Windows PowerShell arabirimi veya hello seri Konsolu yapılandırılır ve otomatik olarak bulut etkindir veri 0.</span><span class="sxs-lookup"><span data-stu-id="46473-106">hello DATA 0 interface is always configured through hello Windows PowerShell interface or hello serial console, and is automatically cloud-enabled.</span></span> <span data-ttu-id="46473-107">DATA 0 ağ arabirimindeki hello Azure portal aracılığıyla yapılandıramayacağınızı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="46473-107">Note that you cannot configure DATA 0 network interface through hello Azure portal.</span></span>

<span data-ttu-id="46473-108">Merhaba DATA 0 arabirimi, ilk hello Kurulumu Sihirbazı aracılığıyla hello StorSimple cihazı ilk dağıtım sırasında yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="46473-108">hello DATA 0 interface is first configured through hello setup wizard during initial deployment of hello StorSimple device.</span></span> <span data-ttu-id="46473-109">Merhaba aygıt bir işlemsel modundayken tooreconfigure veri 0 gerekebilir ayarlar.</span><span class="sxs-lookup"><span data-stu-id="46473-109">When hello device is in an operational mode, you may need tooreconfigure DATA 0 settings.</span></span> <span data-ttu-id="46473-110">Bu öğretici toomodify veri 0 ağ ayarları, StorSimple için Windows PowerShell aracılığıyla her ikisi de iki yöntem sunar.</span><span class="sxs-lookup"><span data-stu-id="46473-110">This tutorial provides two methods toomodify DATA 0 network settings, both through Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="46473-111">Bu öğretici okuduktan sonra aşağıdakileri gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="46473-111">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="46473-112">Veri 0 değiştirme ağ ayarını hello Kurulum Sihirbazı'nı kullanarak</span><span class="sxs-lookup"><span data-stu-id="46473-112">Modify DATA 0 network setting through hello setup wizard</span></span>
* <span data-ttu-id="46473-113">Veri 0 ağ ayarları'nda hello değiştirmek `Set-HcsNetInterface` cmdlet'i</span><span class="sxs-lookup"><span data-stu-id="46473-113">Modify DATA 0 network settings through hello `Set-HcsNetInterface` cmdlet</span></span>

## <a name="modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="46473-114">Kurulum Sihirbazı aracılığıyla veri 0 ağ ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="46473-114">Modify DATA 0 network settings through setup wizard</span></span>
<span data-ttu-id="46473-115">StorSimple cihazınızın toohello Windows PowerShell arabirimi bağlanma ve Kurulum Sihirbazı'nı oturumunu başlatmasını veri 0 ağ ayarlarını yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46473-115">You can reconfigure DATA 0 network settings by connecting toohello Windows PowerShell interface of your StorSimple device and launching a setup wizard session.</span></span> <span data-ttu-id="46473-116">Gerçekleştirme adımları toomodify veri 0 aşağıdaki hello ayarları:</span><span class="sxs-lookup"><span data-stu-id="46473-116">Perform hello following steps toomodify DATA 0 settings:</span></span>

#### <a name="toomodify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="46473-117">Kurulum Sihirbazı aracılığıyla toomodify veri 0 ağ ayarları</span><span class="sxs-lookup"><span data-stu-id="46473-117">toomodify DATA 0 network settings through setup wizard</span></span>
1. <span data-ttu-id="46473-118">Merhaba seri konsol menüsünde seçeneği 1, **oturum oturum tam erişim**.</span><span class="sxs-lookup"><span data-stu-id="46473-118">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="46473-119">İstendiğinde hello sağlamak **cihaz Yöneticisi parolası**.</span><span class="sxs-lookup"><span data-stu-id="46473-119">When prompted provide hello **device administrator password**.</span></span> <span data-ttu-id="46473-120">Merhaba varsayılan parola `Password1`.</span><span class="sxs-lookup"><span data-stu-id="46473-120">hello default password is `Password1`.</span></span>
2. <span data-ttu-id="46473-121">Merhaba komut satırına aşağıdakini yazın:</span><span class="sxs-lookup"><span data-stu-id="46473-121">At hello command prompt, type:</span></span>
   
    `Invoke-HcsSetupWizard`
3. <span data-ttu-id="46473-122">Kurulum Sihirbazı'nı toohelp görünür hello veri 0 yapılandırma aygıtınızın arabirimi.</span><span class="sxs-lookup"><span data-stu-id="46473-122">A setup wizard appears toohelp configure hello DATA 0 interface of your device.</span></span> <span data-ttu-id="46473-123">Başlangıç IP adresi, ağ geçidi ve ağ maskesi için yeni değerleri sağlayın.</span><span class="sxs-lookup"><span data-stu-id="46473-123">Provide new values for hello IP address, gateway, and netmask.</span></span>

> [!NOTE]
> <span data-ttu-id="46473-124">Sabit IP'leri hello yeniden toobe gerekir denetleyicileri hello **ağ ayarlarını** hello StorSimple cihazı hello Azure portal dikey.</span><span class="sxs-lookup"><span data-stu-id="46473-124">hello fixed controllers IPs will need toobe reconfigured through hello **Network settings** blade of hello StorSimple device in hello Azure portal.</span></span> <span data-ttu-id="46473-125">Daha fazla bilgi için çok Git[ağ arabirimleri değiştirme](storsimple-8000-modify-device-config.md#modify-network-interfaces).</span><span class="sxs-lookup"><span data-stu-id="46473-125">For more information, go too[Modify network interfaces](storsimple-8000-modify-device-config.md#modify-network-interfaces).</span></span>

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="46473-126">Set-HcsNetInterface cmdlet'i aracılığıyla veri 0 ağ ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="46473-126">Modify DATA 0 network settings through Set-HcsNetInterface cmdlet</span></span>
<span data-ttu-id="46473-127">Alternatif bir yol tooreconfigure veri 0 ağ arabirimi hello hello kullanımla `Set-HcsNetInterface` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="46473-127">An alternate way tooreconfigure DATA 0 network interface is through hello use of hello `Set-HcsNetInterface` cmdlet.</span></span> <span data-ttu-id="46473-128">Merhaba cmdlet hello Windows PowerShell arabiriminden StorSimple Cihazınızı yürütülür.</span><span class="sxs-lookup"><span data-stu-id="46473-128">hello cmdlet is executed from hello Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="46473-129">Bu yordam kullanılırken hello denetleyicisi sabit IP'leri de burada yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="46473-129">When using this procedure, hello controller fixed IPs can also be configured here.</span></span> <span data-ttu-id="46473-130">Gerçekleştirme adımları toomodify hello veri 0 aşağıdaki hello ayarları:</span><span class="sxs-lookup"><span data-stu-id="46473-130">Perform hello following steps toomodify hello DATA 0 settings:</span></span> 

#### <a name="toomodify-data-0-network-settings-through-hello-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="46473-131">Merhaba Set-HcsNetInterface cmdlet'i toomodify veri 0 ağ ayarları</span><span class="sxs-lookup"><span data-stu-id="46473-131">toomodify DATA 0 network settings through hello Set-HcsNetInterface cmdlet</span></span>
1. <span data-ttu-id="46473-132">Merhaba seri konsol menüsünde seçeneği 1, **oturum oturum tam erişim**.</span><span class="sxs-lookup"><span data-stu-id="46473-132">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="46473-133">İstendiğinde hello cihaz Yöneticisi parolasını verin.</span><span class="sxs-lookup"><span data-stu-id="46473-133">When prompted provide hello device administrator password.</span></span> <span data-ttu-id="46473-134">Merhaba varsayılan parola `Password1`.</span><span class="sxs-lookup"><span data-stu-id="46473-134">hello default password is `Password1`.</span></span>
2. <span data-ttu-id="46473-135">Merhaba komut satırına aşağıdakini yazın:</span><span class="sxs-lookup"><span data-stu-id="46473-135">At hello command prompt, type:</span></span>
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    <span data-ttu-id="46473-136">Merhaba açılı ayraç DATA 0 için değerleri aşağıdaki hello yazın:</span><span class="sxs-lookup"><span data-stu-id="46473-136">In hello angled brackets, type hello following values for DATA 0:</span></span>
   
   * <span data-ttu-id="46473-137">IPv4 adresi</span><span class="sxs-lookup"><span data-stu-id="46473-137">IPv4 address</span></span>
   * <span data-ttu-id="46473-138">IPv4 ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="46473-138">IPv4 gateway</span></span>
   * <span data-ttu-id="46473-139">IPv4 alt ağ maskesi</span><span class="sxs-lookup"><span data-stu-id="46473-139">IPv4 subnet mask</span></span>
   * <span data-ttu-id="46473-140">Denetleyici 0 sabit IPv4 adresi</span><span class="sxs-lookup"><span data-stu-id="46473-140">Fixed IPv4 address for Controller 0</span></span>
   * <span data-ttu-id="46473-141">Denetleyici 1 için sabit IPv4 adresi</span><span class="sxs-lookup"><span data-stu-id="46473-141">Fixed IPv4 address for Controller 1</span></span>
     
     <span data-ttu-id="46473-142">Bu cmdlet hello kullanımı hakkında daha fazla bilgi için çok Git[StorSimple cmdlet başvurusu için Windows PowerShell](https://technet.microsoft.com/library/dn688161.aspx).</span><span class="sxs-lookup"><span data-stu-id="46473-142">For more information on hello use of this cmdlet, go too[Windows PowerShell for StorSimple cmdlet reference](https://technet.microsoft.com/library/dn688161.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="46473-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="46473-143">Next steps</span></span>
* <span data-ttu-id="46473-144">Veri 0 dışında tooconfigure ağ arabirimleri, kullanabileceğiniz hello [hello Azure portal ağ ayarlarını yapılandırma](storsimple-8000-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="46473-144">tooconfigure network interfaces other than DATA 0, you can use hello [Configure network settings in hello Azure portal](storsimple-8000-modify-device-config.md).</span></span> 
* <span data-ttu-id="46473-145">Ağ arabirimleri yapılandırırken herhangi bir sorunla karşılaşırsanız, çok başvuran[dağıtım sorunlarını giderme](storsimple-troubleshoot-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="46473-145">If you experience any issues when configuring your network interfaces, refer too[Troubleshoot deployment issues](storsimple-troubleshoot-deployment.md).</span></span>

