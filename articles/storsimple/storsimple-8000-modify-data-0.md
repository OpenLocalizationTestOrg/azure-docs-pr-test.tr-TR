---
title: "Veri 0 değiştirme StorSimple 8000 serisi cihazın ayarlarının | Microsoft Docs"
description: "StorSimple için Windows PowerShell, StorSimple Cihazınızda DATA 0 ağ arabirimindeki yeniden yapılandırmak için nasıl kullanılacağını öğrenin."
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
ms.openlocfilehash: 90df43e22f17fd32fe642514df098b72700e77af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="modify-the-data-0-network-interface-settings-on-your-storsimple-8000-series-device"></a><span data-ttu-id="a86d6-103">StorSimple 8000 serisi aygıtınızda veri 0 ağ arabirimi ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="a86d6-103">Modify the DATA 0 network interface settings on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="a86d6-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="a86d6-104">Overview</span></span>

<span data-ttu-id="a86d6-105">Microsoft Azure StorSimple Cihazınızı veri 5 0 verilerden altı ağ arabirimi bulunur.</span><span class="sxs-lookup"><span data-stu-id="a86d6-105">Your Microsoft Azure StorSimple device has six network interfaces, from DATA 0 to DATA 5.</span></span> <span data-ttu-id="a86d6-106">DATA 0 arabirimi her zaman Windows PowerShell arabirimi veya seri Konsolu yapılandırılır ve otomatik olarak bulut etkindir.</span><span class="sxs-lookup"><span data-stu-id="a86d6-106">The DATA 0 interface is always configured through the Windows PowerShell interface or the serial console, and is automatically cloud-enabled.</span></span> <span data-ttu-id="a86d6-107">Azure Portalı aracılığıyla DATA 0 ağ arabirimindeki yapılandıramayacağınızı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a86d6-107">Note that you cannot configure DATA 0 network interface through the Azure portal.</span></span>

<span data-ttu-id="a86d6-108">Arabirim ilk sırasında Kurulum Sihirbazı ile yapılandırılmış veri 0 StorSimple cihaz dağıtımına başlangıç.</span><span class="sxs-lookup"><span data-stu-id="a86d6-108">The DATA 0 interface is first configured through the setup wizard during initial deployment of the StorSimple device.</span></span> <span data-ttu-id="a86d6-109">Cihaz bir işlemsel modunda olduğunda veri 0 yeniden yapılandırmanız gerekebilir ayarlar.</span><span class="sxs-lookup"><span data-stu-id="a86d6-109">When the device is in an operational mode, you may need to reconfigure DATA 0 settings.</span></span> <span data-ttu-id="a86d6-110">Bu öğreticide, veri 0 değiştirmek için iki yöntem ağ ayarlarını, StorSimple için ile hem de Windows PowerShell sağlar.</span><span class="sxs-lookup"><span data-stu-id="a86d6-110">This tutorial provides two methods to modify DATA 0 network settings, both through Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="a86d6-111">Bu öğretici okuduktan sonra aşağıdakileri gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a86d6-111">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="a86d6-112">Veri 0 değiştirme Ağ Kurulum Sihirbazı'nı ayarlama</span><span class="sxs-lookup"><span data-stu-id="a86d6-112">Modify DATA 0 network setting through the setup wizard</span></span>
* <span data-ttu-id="a86d6-113">Veri 0 ağ ayarları'nda değiştirme `Set-HcsNetInterface` cmdlet'i</span><span class="sxs-lookup"><span data-stu-id="a86d6-113">Modify DATA 0 network settings through the `Set-HcsNetInterface` cmdlet</span></span>

## <a name="modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="a86d6-114">Kurulum Sihirbazı aracılığıyla veri 0 ağ ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="a86d6-114">Modify DATA 0 network settings through setup wizard</span></span>
<span data-ttu-id="a86d6-115">StorSimple Cihazınızı Windows PowerShell arabirimine bağlanılırken ve Kurulum Sihirbazı'nı oturumunu başlatmasını veri 0 ağ ayarlarını yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a86d6-115">You can reconfigure DATA 0 network settings by connecting to the Windows PowerShell interface of your StorSimple device and launching a setup wizard session.</span></span> <span data-ttu-id="a86d6-116">Veri 0 değiştirmek için aşağıdaki adımları gerçekleştirin ayarları:</span><span class="sxs-lookup"><span data-stu-id="a86d6-116">Perform the following steps to modify DATA 0 settings:</span></span>

#### <a name="to-modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="a86d6-117">Kurulum Sihirbazı aracılığıyla veri 0 ağ ayarlarını değiştirmek için</span><span class="sxs-lookup"><span data-stu-id="a86d6-117">To modify DATA 0 network settings through setup wizard</span></span>
1. <span data-ttu-id="a86d6-118">Seri konsol menüsünde seçeneği 1, **oturum oturum tam erişim**.</span><span class="sxs-lookup"><span data-stu-id="a86d6-118">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="a86d6-119">İstendiğinde sağlamak **cihaz Yöneticisi parolası**.</span><span class="sxs-lookup"><span data-stu-id="a86d6-119">When prompted provide the **device administrator password**.</span></span> <span data-ttu-id="a86d6-120">Varsayılan parola `Password1`.</span><span class="sxs-lookup"><span data-stu-id="a86d6-120">The default password is `Password1`.</span></span>
2. <span data-ttu-id="a86d6-121">Komut istemine yazın:</span><span class="sxs-lookup"><span data-stu-id="a86d6-121">At the command prompt, type:</span></span>
   
    `Invoke-HcsSetupWizard`
3. <span data-ttu-id="a86d6-122">Veri 0 yapılandırmak için Kurulum Sihirbazı görünür aygıtınızın arabirimi.</span><span class="sxs-lookup"><span data-stu-id="a86d6-122">A setup wizard appears to help configure the DATA 0 interface of your device.</span></span> <span data-ttu-id="a86d6-123">IP adresi, ağ geçidi ve ağ maskesi için yeni değerleri sağlayın.</span><span class="sxs-lookup"><span data-stu-id="a86d6-123">Provide new values for the IP address, gateway, and netmask.</span></span>

> [!NOTE]
> <span data-ttu-id="a86d6-124">Sabit IP'leri denetleyicileri aracılığıyla yapılandırılması gerekir **ağ ayarlarını** StorSimple cihazı Azure portalında dikey.</span><span class="sxs-lookup"><span data-stu-id="a86d6-124">The fixed controllers IPs will need to be reconfigured through the **Network settings** blade of the StorSimple device in the Azure portal.</span></span> <span data-ttu-id="a86d6-125">Daha fazla bilgi için Git [ağ arabirimleri değiştirme](storsimple-8000-modify-device-config.md#modify-network-interfaces).</span><span class="sxs-lookup"><span data-stu-id="a86d6-125">For more information, go to [Modify network interfaces](storsimple-8000-modify-device-config.md#modify-network-interfaces).</span></span>

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="a86d6-126">Set-HcsNetInterface cmdlet'i aracılığıyla veri 0 ağ ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="a86d6-126">Modify DATA 0 network settings through Set-HcsNetInterface cmdlet</span></span>
<span data-ttu-id="a86d6-127">DATA 0 ağ arabirimi olan kullanılarak yeniden yapılandırmak için alternatif bir yolu `Set-HcsNetInterface` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="a86d6-127">An alternate way to reconfigure DATA 0 network interface is through the use of the `Set-HcsNetInterface` cmdlet.</span></span> <span data-ttu-id="a86d6-128">Cmdlet StorSimple Cihazınızı Windows PowerShell arabiriminden yürütülür.</span><span class="sxs-lookup"><span data-stu-id="a86d6-128">The cmdlet is executed from the Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="a86d6-129">Bu yordamı kullanırken, denetleyici IP'leri sabit de burada yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="a86d6-129">When using this procedure, the controller fixed IPs can also be configured here.</span></span> <span data-ttu-id="a86d6-130">Veri 0 değiştirmek için aşağıdaki adımları gerçekleştirin ayarları:</span><span class="sxs-lookup"><span data-stu-id="a86d6-130">Perform the following steps to modify the DATA 0 settings:</span></span> 

#### <a name="to-modify-data-0-network-settings-through-the-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="a86d6-131">Set-HcsNetInterface cmdlet'i aracılığıyla veri 0 ağ ayarlarını değiştirmek için</span><span class="sxs-lookup"><span data-stu-id="a86d6-131">To modify DATA 0 network settings through the Set-HcsNetInterface cmdlet</span></span>
1. <span data-ttu-id="a86d6-132">Seri konsol menüsünde seçeneği 1, **oturum oturum tam erişim**.</span><span class="sxs-lookup"><span data-stu-id="a86d6-132">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="a86d6-133">İstendiğinde cihaz Yöneticisi parolasını verin.</span><span class="sxs-lookup"><span data-stu-id="a86d6-133">When prompted provide the device administrator password.</span></span> <span data-ttu-id="a86d6-134">Varsayılan parola `Password1`.</span><span class="sxs-lookup"><span data-stu-id="a86d6-134">The default password is `Password1`.</span></span>
2. <span data-ttu-id="a86d6-135">Komut istemine yazın:</span><span class="sxs-lookup"><span data-stu-id="a86d6-135">At the command prompt, type:</span></span>
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    <span data-ttu-id="a86d6-136">Açılı ayraç içinde veri 0 için aşağıdaki değerleri yazın:</span><span class="sxs-lookup"><span data-stu-id="a86d6-136">In the angled brackets, type the following values for DATA 0:</span></span>
   
   * <span data-ttu-id="a86d6-137">IPv4 adresi</span><span class="sxs-lookup"><span data-stu-id="a86d6-137">IPv4 address</span></span>
   * <span data-ttu-id="a86d6-138">IPv4 ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="a86d6-138">IPv4 gateway</span></span>
   * <span data-ttu-id="a86d6-139">IPv4 alt ağ maskesi</span><span class="sxs-lookup"><span data-stu-id="a86d6-139">IPv4 subnet mask</span></span>
   * <span data-ttu-id="a86d6-140">Denetleyici 0 sabit IPv4 adresi</span><span class="sxs-lookup"><span data-stu-id="a86d6-140">Fixed IPv4 address for Controller 0</span></span>
   * <span data-ttu-id="a86d6-141">Denetleyici 1 için sabit IPv4 adresi</span><span class="sxs-lookup"><span data-stu-id="a86d6-141">Fixed IPv4 address for Controller 1</span></span>
     
     <span data-ttu-id="a86d6-142">Bu cmdlet kullanımı hakkında daha fazla bilgi için Git [StorSimple cmdlet başvurusu için Windows PowerShell](https://technet.microsoft.com/library/dn688161.aspx).</span><span class="sxs-lookup"><span data-stu-id="a86d6-142">For more information on the use of this cmdlet, go to [Windows PowerShell for StorSimple cmdlet reference](https://technet.microsoft.com/library/dn688161.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a86d6-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a86d6-143">Next steps</span></span>
* <span data-ttu-id="a86d6-144">Ağ arabirimleri veri 0 dışında yapılandırmak için kullanabileceğiniz [Azure portalında ağ ayarlarını yapılandırma](storsimple-8000-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="a86d6-144">To configure network interfaces other than DATA 0, you can use the [Configure network settings in the Azure portal](storsimple-8000-modify-device-config.md).</span></span> 
* <span data-ttu-id="a86d6-145">Ağ arabirimleri yapılandırırken herhangi bir sorunla karşılaşırsanız, başvurmak [dağıtım sorunlarını giderme](storsimple-troubleshoot-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="a86d6-145">If you experience any issues when configuring your network interfaces, refer to [Troubleshoot deployment issues](storsimple-troubleshoot-deployment.md).</span></span>

