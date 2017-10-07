---
title: "aaaDiagnostics aracı tootroubleshoot StorSimple 8000 cihaz | Microsoft Docs"
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
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: e8b7fdbc44d2533973b63da841335ba73ba0014b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-diagnostics-tool-tootroubleshoot-8000-series-device-issues"></a><span data-ttu-id="4cf63-103">Merhaba StorSimple Tanılama Aracı tootroubleshoot 8000 serisi aygıt sorunları kullanın</span><span class="sxs-lookup"><span data-stu-id="4cf63-103">Use hello StorSimple Diagnostics Tool tootroubleshoot 8000 series device issues</span></span>

## <a name="overview"></a><span data-ttu-id="4cf63-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="4cf63-104">Overview</span></span>

<span data-ttu-id="4cf63-105">Merhaba StorSimple Tanılama aracı sorunları ilgili toosystem, performans, ağ ve donanım bileşen durumu StorSimple cihazı için tanılar.</span><span class="sxs-lookup"><span data-stu-id="4cf63-105">hello StorSimple Diagnostics tool diagnoses issues related toosystem, performance, network, and hardware component health for a StorSimple device.</span></span> <span data-ttu-id="4cf63-106">Merhaba Tanılama aracı çeşitli senaryolarda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-106">hello diagnostics tool can be used in various scenarios.</span></span> <span data-ttu-id="4cf63-107">Bu senaryolar iş yükü planlama, StorSimple cihazını dağıtma, hello ağ ortamı değerlendirmek ve işletimsel aygıt hello performansını belirleme içerir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-107">These scenarios include workload planning, deploying a StorSimple device, assessing hello network environment, and determining hello performance of an operational device.</span></span> <span data-ttu-id="4cf63-108">Bu makalede hello Tanılama Aracı genel bir bakış sağlar ve hello aracı StorSimple cihazı ile nasıl kullanılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="4cf63-108">This article provides an overview of hello diagnostics tool and describes how hello tool can be used with a StorSimple device.</span></span>

<span data-ttu-id="4cf63-109">Merhaba Tanılama Aracı öncelikle StorSimple 8000 serisi şirket içi cihazlar için (8100 ve 8600) yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-109">hello diagnostics tool is primarily intended for StorSimple 8000 series on-premises devices (8100 and 8600).</span></span>

## <a name="run-diagnostics-tool"></a><span data-ttu-id="4cf63-110">Tanılama aracını çalıştırın</span><span class="sxs-lookup"><span data-stu-id="4cf63-110">Run diagnostics tool</span></span>

<span data-ttu-id="4cf63-111">Bu araç, StorSimple cihazınızın hello Windows PowerShell arabirimi çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-111">This tool can be run via hello Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="4cf63-112">Cihazınızı yerel arabiriminin tooaccess hello iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="4cf63-112">There are two ways tooaccess hello local interface of your device:</span></span>

* <span data-ttu-id="4cf63-113">[Kullanım PuTTY tooconnect toohello cihaz seri konsoluna](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="4cf63-113">[Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
* <span data-ttu-id="4cf63-114">[Merhaba aracı hello Windows PowerShell aracılığıyla StorSimple için uzaktan erişim](storsimple-remote-connect.md).</span><span class="sxs-lookup"><span data-stu-id="4cf63-114">[Remotely access hello tool via hello Windows PowerShell for StorSimple](storsimple-remote-connect.md).</span></span>

<span data-ttu-id="4cf63-115">Bu makalede, toohello cihaz seri konsoluna PuTTY üzerinden bağlı olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="4cf63-115">In this article, we assume that you have connected toohello device serial console via PuTTY.</span></span>

#### <a name="toorun-hello-diagnostics-tool"></a><span data-ttu-id="4cf63-116">toorun hello Tanılama Aracı</span><span class="sxs-lookup"><span data-stu-id="4cf63-116">toorun hello diagnostics tool</span></span>

<span data-ttu-id="4cf63-117">Toohello Windows PowerShell arabirimi hello cihaz bağlandıktan sonra aşağıdaki adımları toorun hello cmdlet hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="4cf63-117">Once you have connected toohello Windows PowerShell interface of hello device, perform hello following steps toorun hello cmdlet.</span></span>
1. <span data-ttu-id="4cf63-118">Merhaba adımları izleyerek toohello cihaz seri konsoluna oturum [kullanım PuTTY tooconnect toohello cihaz seri konsoluna](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="4cf63-118">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>

2. <span data-ttu-id="4cf63-119">Merhaba aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="4cf63-119">Type hello following command:</span></span>

    `Invoke-HcsDiagnostics`

    <span data-ttu-id="4cf63-120">Merhaba kapsam parametresi belirtilmezse, hello cmdlet'i tüm hello tanılama testleri yürütür.</span><span class="sxs-lookup"><span data-stu-id="4cf63-120">If hello scope parameter is not specified, hello cmdlet executes all hello diagnostic tests.</span></span> <span data-ttu-id="4cf63-121">Bu testler, sistem, donanım bileşen durumu, ağ ve performans içerir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-121">These tests include system, hardware component health, network, and performance.</span></span> 
    
    <span data-ttu-id="4cf63-122">belirli test yalnızca toorun hello kapsam parametresi belirtin.</span><span class="sxs-lookup"><span data-stu-id="4cf63-122">toorun only a specific test, specify hello scope parameter.</span></span> <span data-ttu-id="4cf63-123">Örneğin, toorun yalnızca hello ağ testi türü</span><span class="sxs-lookup"><span data-stu-id="4cf63-123">For instance, toorun only hello network test, type</span></span>

    `Invoke-HcsDiagnostics -Scope Network`

3. <span data-ttu-id="4cf63-124">Seçin ve kopyalayın hello çıktı hello PuTTY ' daha fazla çözümleme için bir metin dosyasına penceresi.</span><span class="sxs-lookup"><span data-stu-id="4cf63-124">Select and copy hello output from hello PuTTY window into a text file for further analysis.</span></span>

## <a name="scenarios-toouse-hello-diagnostics-tool"></a><span data-ttu-id="4cf63-125">Senaryolar toouse hello Tanılama Aracı</span><span class="sxs-lookup"><span data-stu-id="4cf63-125">Scenarios toouse hello diagnostics tool</span></span>

<span data-ttu-id="4cf63-126">Merhaba Tanılama Aracı tootroubleshoot hello ağ, performans, sistem ve donanım hello sisteminin durumunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="4cf63-126">Use hello diagnostics tool tootroubleshoot hello network, performance, system, and hardware health of hello system.</span></span> <span data-ttu-id="4cf63-127">Bazı olası senaryolar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4cf63-127">Here are some possible scenarios:</span></span>

* <span data-ttu-id="4cf63-128">**Cihaz çevrimdışı** -bilgisayarınızı StorSimple 8000 serisi cihaz çevrimdışı.</span><span class="sxs-lookup"><span data-stu-id="4cf63-128">**Device offline** - Your StorSimple 8000 series device is offline.</span></span> <span data-ttu-id="4cf63-129">Ancak, hello Windows PowerShell arabiriminden hem hello denetleyicileri ve çalışıyor olduğunu görünüyor.</span><span class="sxs-lookup"><span data-stu-id="4cf63-129">However, from hello Windows PowerShell interface, it seems that both hello controllers are up and running.</span></span>
    * <span data-ttu-id="4cf63-130">Bu aracı kullanabilirsiniz toothen hello ağ durumu belirleyin.</span><span class="sxs-lookup"><span data-stu-id="4cf63-130">You can use this tool toothen determine hello network state.</span></span>
         
         > [!NOTE]
         > <span data-ttu-id="4cf63-131">Bu aracı tooassess performans ve ağ ayarlarını hello kayıt (veya Kurulum Sihirbazı yapılandırma) önce bir cihazda kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="4cf63-131">Do not use this tool tooassess performance and network settings on a device before hello registration (or configuring via setup wizard).</span></span> <span data-ttu-id="4cf63-132">Geçerli bir IP toohello aygıt Kurulum Sihirbazı'nı ve kayıt sırasında atanır.</span><span class="sxs-lookup"><span data-stu-id="4cf63-132">A valid IP is assigned toohello device during setup wizard and registration.</span></span> <span data-ttu-id="4cf63-133">Bu cmdlet, donanım durumunu ve sistem için kayıtlı değil, bir cihaz çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4cf63-133">You can run this cmdlet, on a device that is not registered, for hardware health and system.</span></span> <span data-ttu-id="4cf63-134">Merhaba kapsam parametresi, örneğin kullanın:</span><span class="sxs-lookup"><span data-stu-id="4cf63-134">Use hello scope parameter, for example:</span></span>
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* <span data-ttu-id="4cf63-135">**Sürekli cihaz sorunlarını** -toopersist göründüğü cihaz sorunları yaşamaktadır.</span><span class="sxs-lookup"><span data-stu-id="4cf63-135">**Persistent device issues** - You are experiencing device issues that seem toopersist.</span></span> <span data-ttu-id="4cf63-136">Örneğin, kayıt başarısız oluyor.</span><span class="sxs-lookup"><span data-stu-id="4cf63-136">For instance, registration is failing.</span></span> <span data-ttu-id="4cf63-137">Başarıyla kayıtlı ve işlem bir süreliğine Hello cihaz olduktan sonra aynı zamanda aygıt sorunları yaşıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-137">You could also be experiencing device issues after hello device is successfully registered and operational for a while.</span></span>
    * <span data-ttu-id="4cf63-138">Bu durumda, bir hizmet isteği Microsoft Support oturum açmadan önce ön gidermek için bu aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4cf63-138">In this case, use this tool for preliminary troubleshooting before you log a service request with Microsoft Support.</span></span> <span data-ttu-id="4cf63-139">Bu aracı ve yakalama hello bu aracın çıktısının çalıştırmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="4cf63-139">We recommend that you run this tool and capture hello output of this tool.</span></span> <span data-ttu-id="4cf63-140">Ardından, bu çıkış tooSupport tooexpedite giderme sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-140">You can then provide this output tooSupport tooexpedite troubleshooting.</span></span>
    * <span data-ttu-id="4cf63-141">Donanım bileşeni veya küme hataları varsa, bir destek isteği oturum açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-141">If there are any hardware component or cluster failures, you should log in a Support request.</span></span>

* <span data-ttu-id="4cf63-142">**Düşük cihaz performans** -bilgisayarınızı StorSimple cihaz yavaş.</span><span class="sxs-lookup"><span data-stu-id="4cf63-142">**Low device performance** - Your StorSimple device is slow.</span></span>
    * <span data-ttu-id="4cf63-143">Bu durumda, bu cmdlet kapsam parametre kümesi tooperformance ile çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4cf63-143">In this case, run this cmdlet with scope parameter set tooperformance.</span></span> <span data-ttu-id="4cf63-144">Merhaba çıkış analiz edin.</span><span class="sxs-lookup"><span data-stu-id="4cf63-144">Analyze hello output.</span></span> <span data-ttu-id="4cf63-145">Okuma-yazma gecikmeleri hello bulutunu alın.</span><span class="sxs-lookup"><span data-stu-id="4cf63-145">You get hello cloud read-write latencies.</span></span> <span data-ttu-id="4cf63-146">Kullanım hello gecikmeleri en fazla ulaşılabilir hedefi olarak hello iç veri işleme için bazı ek faktörü ve hello sistemde hello iş yükleri dağıtmak bildirdi.</span><span class="sxs-lookup"><span data-stu-id="4cf63-146">Use hello reported latencies as maximum achievable target, factor in some overhead for hello internal data processing, and then deploy hello workloads on hello system.</span></span> <span data-ttu-id="4cf63-147">Daha fazla bilgi için çok Git[hello ağ tootroubleshoot aygıt performansını test etme kullanmak](#network-test).</span><span class="sxs-lookup"><span data-stu-id="4cf63-147">For more information, go too[Use hello network test tootroubleshoot device performance](#network-test).</span></span>


## <a name="diagnostics-test-and-sample-outputs"></a><span data-ttu-id="4cf63-148">Tanılama test ve örnek çıkış</span><span class="sxs-lookup"><span data-stu-id="4cf63-148">Diagnostics test and sample outputs</span></span>

### <a name="hardware-test"></a><span data-ttu-id="4cf63-149">Donanım sınaması</span><span class="sxs-lookup"><span data-stu-id="4cf63-149">Hardware test</span></span>

<span data-ttu-id="4cf63-150">Bu test hello donanım bileşenleri, hello USM bellenim ve sisteminizde çalışan hello disk bellenim hello durumunu belirler.</span><span class="sxs-lookup"><span data-stu-id="4cf63-150">This test determines hello status of hello hardware components, hello USM firmware, and hello disk firmware running on your system.</span></span>

* <span data-ttu-id="4cf63-151">bildirilen hello donanım bileşenleri başarısız hello test bu bileşenleridir veya hello sistemde mevcut değil.</span><span class="sxs-lookup"><span data-stu-id="4cf63-151">hello hardware components reported are those components that failed hello test or are not present in hello system.</span></span>
* <span data-ttu-id="4cf63-152">Merhaba USM bellenim ve disk bellenim sürümleri hello denetleyici 0, denetleyici 1 için bildirilen ve sisteminizdeki paylaşılan bileşenleri.</span><span class="sxs-lookup"><span data-stu-id="4cf63-152">hello USM firmware and disk firmware versions are reported for hello Controller 0, Controller 1, and shared components in your system.</span></span> <span data-ttu-id="4cf63-153">Donanım bileşenleri tam listesi için aşağıdaki adrese gidin:</span><span class="sxs-lookup"><span data-stu-id="4cf63-153">For a complete list of hardware components, go to:</span></span>

    * [<span data-ttu-id="4cf63-154">Birincil muhafazada bileşenleri</span><span class="sxs-lookup"><span data-stu-id="4cf63-154">Components in primary enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [<span data-ttu-id="4cf63-155">EBOD muhafazası bileşenleri</span><span class="sxs-lookup"><span data-stu-id="4cf63-155">Components in EBOD enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> <span data-ttu-id="4cf63-156">Merhaba donanım sınaması başarısız bileşenleri bildirirse [Microsoft Support olan hizmet isteği oturum](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="4cf63-156">If hello hardware test reports failed components, [log in a service request with Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a><span data-ttu-id="4cf63-157">8100 cihazda donanım testi örnek çıktısı</span><span class="sxs-lookup"><span data-stu-id="4cf63-157">Sample output of hardware test run on an 8100 device</span></span>

<span data-ttu-id="4cf63-158">Burada, StorSimple 8100 cihazınız dosyasından örnek çıktı verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-158">Here is a sample output from a StorSimple 8100 device.</span></span> <span data-ttu-id="4cf63-159">Merhaba 8100 model aygıtı hello EBOD muhafazası mevcut değil.</span><span class="sxs-lookup"><span data-stu-id="4cf63-159">In hello 8100 model device, hello EBOD enclosure is not present.</span></span> <span data-ttu-id="4cf63-160">Bu nedenle, hello EBOD denetleyicisi bileşenleri raporlanmaz.</span><span class="sxs-lookup"><span data-stu-id="4cf63-160">Hence, hello EBOD controller components are not reported.</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Hardware
Running hardware diagnostics ...
--------------------------------------------------
Hardware components failed or not present
----------------------

           Type           State      Controller           Index     EnclosureId
           ----           -----      ----------           -----     -----------
...rVipResource      NotPresent            None               1            None
...rVipResource      NotPresent            None               2            None
...rVipResource      NotPresent            None               3            None
...rVipResource      NotPresent            None               4            None
...rVipResource      NotPresent            None               5            None
...rVipResource      NotPresent            None               6            None
...rVipResource      NotPresent            None               7            None
...rVipResource      NotPresent            None               8            None
...rVipResource      NotPresent            None               9            None
...rVipResource      NotPresent            None              10            None
...rVipResource      NotPresent            None              11            None

Firmware information
----------------------
TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

--------------------------------------------------
```

### <a name="system-test"></a><span data-ttu-id="4cf63-161">Sistem test</span><span class="sxs-lookup"><span data-stu-id="4cf63-161">System test</span></span>

<span data-ttu-id="4cf63-162">Bu test hello sistem bilgileri, hello güncelleştirmelere, hello küme bilgilerini ve hello hizmet bilgileri, cihazınız için raporlar.</span><span class="sxs-lookup"><span data-stu-id="4cf63-162">This test reports hello system information, hello updates available, hello cluster information, and hello service information for your device.</span></span>

* <span data-ttu-id="4cf63-163">Merhaba sistem bilgileri hello modeli, cihaz seri numarasını, saat dilimi, denetleyici durumu ve hello sistem üzerinde çalışan hello ayrıntılı yazılım sürüm içerir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-163">hello system information includes hello model, device serial number, time zone, controller status, and hello detailed software version running on hello system.</span></span> <span data-ttu-id="4cf63-164">çeşitli sistem parametreleri hello çıkış olarak bildirilen Git çok toounderstand hello[sistem bilgileri yorumlama](#appendix-interpreting-system-information).</span><span class="sxs-lookup"><span data-stu-id="4cf63-164">toounderstand hello various system parameters reported as hello output, go too[Interpreting system information](#appendix-interpreting-system-information).</span></span>

* <span data-ttu-id="4cf63-165">Merhaba güncelleştirme kullanılabilirlik raporları hello normal ve Bakım modu kullanılabilir olup olmadığını ve ilişkili paket adları.</span><span class="sxs-lookup"><span data-stu-id="4cf63-165">hello update availability reports whether hello regular and maintenance modes are available and their associated package names.</span></span> <span data-ttu-id="4cf63-166">Varsa `RegularUpdates` ve `MaintenanceModeUpdates` olan `false`, bu hello güncelleştirmeleri kullanılabilir olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-166">If `RegularUpdates` and `MaintenanceModeUpdates` are `false`, this indicates that hello updates are not available.</span></span> <span data-ttu-id="4cf63-167">Cihazınız güncel olduğundan.</span><span class="sxs-lookup"><span data-stu-id="4cf63-167">Your device is up-to-date.</span></span>
* <span data-ttu-id="4cf63-168">Hello küme bilgilerini tüm hello HCS küme gruplarını ve bunlarla ilgili durumlar hello bilgiler çeşitli mantıksal bileşenleri içerir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-168">hello cluster information contains hello information on various logical components of all hello HCS cluster groups and their respective statuses.</span></span> <span data-ttu-id="4cf63-169">Bu bölümdeki çevrimdışı küme grubu hello raporunun görürseniz [Microsoft Support başvurun](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="4cf63-169">If you see an offline cluster group in this section of hello report, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="4cf63-170">Merhaba hizmet bilgileri hello adları ve tüm hello HCS durumları ve, cihazda çalışan CIS hizmetleri içerir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-170">hello service information includes hello names and statuses of all hello HCS and CiS services running on your device.</span></span> <span data-ttu-id="4cf63-171">Bu bilgiler hello aygıt sorun giderme amacıyla Microsoft Support hello için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="4cf63-171">This information is helpful for hello Microsoft Support in troubleshooting hello device issue.</span></span>

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a><span data-ttu-id="4cf63-172">Örnek çıktı sistemi test 8100 cihazda çalıştırın</span><span class="sxs-lookup"><span data-stu-id="4cf63-172">Sample output of system test run on an 8100 device</span></span>

<span data-ttu-id="4cf63-173">Örnek bir çıktı hello sistem test 8100 cihazda çalıştırın, burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-173">Here is a sample output of hello system test run on an 8100 device.</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope System
Running system diagnostics ...
--------------------------------------------------

System information
----------------------
Controller0:

InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                : (UTC-08:00) Pacific Time (US & Canada)
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : Disabled
FipsMode                : Enabled

Controller1:
InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                :
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : HttpsAndHttpEnabled
FipsMode                : Enabled

Update availability
----------------------
RegularUpdates              : False
MaintenanceModeUpdates      : False
RegularUpdatesTitle         : {}
MaintenanceModeUpdatesTitle : {}

Cluster information
----------------------
Name                          State OwnerGroup
----                          ----- ----------
ApplicationHostRLUA           Online HCS Cluster Group
Data0v4                       Online HCS Cluster Group
HCS Vnic Resource             Online HCS Cluster Group
hcs_cloud_connectivity_...    Online HCS Cluster Group
hcs_controller_replacement    Online HCS Cluster Group
hcs_datapath_service          Online HCS Cluster Group
hcs_management_servic         Online HCS Cluster Group
hcs_nvram_service             Online HCS Cluster Group
hcs_passive_datapath          Online HCS Passive Cluster Group
hcs_platform_service          Online HCS Cluster Group
hcs_saas_agent_service        Online HCS Cluster Group
HddDataClusterDisk            Online HCS Cluster Group
HddMgmtClusterDisk            Online HCS Cluster Group
HddReplClusterDisk            Online HCS Cluster Group
iSCSI Target Server           Online HCS Cluster Group
NvramClusterDisk              Online HCS Cluster Group
SSAdminRLUA                   Online HCS Cluster Group
SsdDataClusterDisk            Online HCS Cluster Group
SsdNvramClusterDisk           Online HCS Cluster Group

Service information
----------------------
Name                                          Status DisplayName
----                                          ------ -----------
CiSAgentSvc                                   Stopped CiS Service Agent
hcs_cloud_connectivity_...                    Running hcs_cloud_connectivity...
hcs_controller_replacement                    Running HCS Controller Replace...
hcs_datapath_service                          Running HCS Datapath Service
hcs_management_service                        Running HCS Management Service
hcs_minishell                                 Running hcs_minishell
HCS_NVRAM_Service                             Running HCS NVRAM Service
hcs_passive_datapath                          Stopped HCS Passive Datapath S...
hcs_platform_service                          Running HCS Platform Monitor S...
hcs_saas_agent_service                        Running hcs_saas_agent_service
hcs_startup                                   Stopped hcs_startup
--------------------------------------------------
```

### <a name="network-test"></a><span data-ttu-id="4cf63-174">Ağ sınaması</span><span class="sxs-lookup"><span data-stu-id="4cf63-174">Network test</span></span>

<span data-ttu-id="4cf63-175">Bu test hello ağ arabirimleri, bağlantı noktaları, DNS ve NTP sunucu bağlantısı, SSL sertifikasını, depolama hesabının kimlik bilgilerini, bağlantı toohello güncelleştirme sunucuları ve web proxy bağlantısı, StorSimple Cihazınızda hello durumunu doğrular.</span><span class="sxs-lookup"><span data-stu-id="4cf63-175">This test validates hello status of hello network interfaces, ports, DNS and NTP server connectivity, SSL certificate, storage account credentials, connectivity toohello Update servers, and web proxy connectivity on your StorSimple device.</span></span>

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a><span data-ttu-id="4cf63-176">Örnek çıktı ağın test yalnızca DATA0 etkinleştirildiğinde</span><span class="sxs-lookup"><span data-stu-id="4cf63-176">Sample output of network test when only DATA0 is enabled</span></span>

<span data-ttu-id="4cf63-177">Burada, örnek bir çıktı hello 8100 cihazın verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-177">Here is a sample output of hello 8100 device.</span></span> <span data-ttu-id="4cf63-178">Merhaba çıktıda görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4cf63-178">You can see in hello output that:</span></span>
* <span data-ttu-id="4cf63-179">Yalnızca veri 0 ve 1 DATA ağ arabirimleri etkin ve yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="4cf63-179">Only DATA 0 and DATA 1 network interfaces are enabled and configured.</span></span>
* <span data-ttu-id="4cf63-180">Veri 2-5 hello Portalı'nda etkin değil.</span><span class="sxs-lookup"><span data-stu-id="4cf63-180">DATA 2 - 5 are not enabled in hello portal.</span></span>
* <span data-ttu-id="4cf63-181">Merhaba DNS sunucu yapılandırması geçerli değil ve hello aygıt üzerinden hello DNS sunucusuna bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-181">hello DNS server configuration is valid and hello device can connect via hello DNS server.</span></span>
* <span data-ttu-id="4cf63-182">Merhaba NTP sunucusu bağlantısı de uygundur.</span><span class="sxs-lookup"><span data-stu-id="4cf63-182">hello NTP server connectivity is also fine.</span></span>
* <span data-ttu-id="4cf63-183">80 ve 443 numaralı bağlantı noktalarını açın.</span><span class="sxs-lookup"><span data-stu-id="4cf63-183">Ports 80 and 443 are open.</span></span> <span data-ttu-id="4cf63-184">Ancak, 9354 bağlantı engellenir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-184">However, port 9354 is blocked.</span></span> <span data-ttu-id="4cf63-185">Merhaba üzerinde temel [sistem ağ gereksinimleri](storsimple-system-requirements.md), tooopen hello service bus iletişim için bu bağlantı noktası gerekir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-185">Based on hello [system network requirements](storsimple-system-requirements.md), you need tooopen this port for hello service bus communication.</span></span>
* <span data-ttu-id="4cf63-186">Merhaba SSL sertifika geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="4cf63-186">hello SSL certification is valid.</span></span>
* <span data-ttu-id="4cf63-187">Merhaba aygıtı toohello depolama hesabı bağlayın: _myss8000storageacct_.</span><span class="sxs-lookup"><span data-stu-id="4cf63-187">hello device can connect toohello storage account: _myss8000storageacct_.</span></span>
* <span data-ttu-id="4cf63-188">Merhaba bağlantı tooUpdate sunucuları geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-188">hello connectivity tooUpdate servers is valid.</span></span>
* <span data-ttu-id="4cf63-189">Merhaba web proxy, bu aygıtta yapılandırılmamış.</span><span class="sxs-lookup"><span data-stu-id="4cf63-189">hello web proxy is not configured on this device.</span></span>

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a><span data-ttu-id="4cf63-190">Örnek çıktı DATA0 ve Veri1 etkin olduğunda ağ testi</span><span class="sxs-lookup"><span data-stu-id="4cf63-190">Sample output of network test when DATA0 and DATA1 are enabled</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Network
Running network diagnostics ....
--------------------------------------------------
Validating networks .....
Name                Entity              Result              Details
----                ------              ------              -------
Network interface   Data0               Valid
Network interface   Data1               Valid
Network interface   Data2               Not enabled
Network interface   Data3               Not enabled
Network interface   Data4               Not enabled
Network interface   Data5               Not enabled
DNS                 10.222.118.154      Valid
NTP                 time.windows.com    Valid
Port                80                  Open
Port                443                 Open
Port                9354                Blocked
SSL certificate     https://myss8000... Valid
Storage account ... myss8000storageacct Valid
URL                 http://download.... Valid
URL                 http://download.... Valid
Web proxy                               Not enabled         Web proxy is not...
--------------------------------------------------
```

### <a name="performance-test"></a><span data-ttu-id="4cf63-191">Performans testi</span><span class="sxs-lookup"><span data-stu-id="4cf63-191">Performance test</span></span>

<span data-ttu-id="4cf63-192">Bu test hello bulut performans hello bulut okuma-yazma gecikmeleri cihazınız için aracılığıyla bildirir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-192">This test reports hello cloud performance via hello cloud read-write latencies for your device.</span></span> <span data-ttu-id="4cf63-193">Bu araç, kullanılan tooestablish ile StorSimple elde edebilirsiniz hello bulut performansının taban çizgisini olabilir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-193">This tool can be used tooestablish a baseline of hello cloud performance that you can achieve with StorSimple.</span></span> <span data-ttu-id="4cf63-194">bağlantınız için alabileceğiniz hello aracı raporları hello en yüksek performans (okuma-yazma gecikme için en iyi Durum senaryosu).</span><span class="sxs-lookup"><span data-stu-id="4cf63-194">hello tool reports hello maximum performance (best case scenario for read-write latencies) that you can get for your connection.</span></span>

<span data-ttu-id="4cf63-195">Merhaba aracı hello maksimum ulaşılabilir performans raporları gibi biz kullanabilirsiniz hello dağıtırken hedefleri iş yükleri hello olarak okuma-yazma gecikmeleri bildirdi.</span><span class="sxs-lookup"><span data-stu-id="4cf63-195">As hello tool reports hello maximum achievable performance, we can use hello reported read-write latencies as targets when deploying hello workloads.</span></span>

<span data-ttu-id="4cf63-196">Merhaba test hello aygıtta hello farklı bir birim türleriyle ilişkili hello kabarcık boyutları benzetimini yapar.</span><span class="sxs-lookup"><span data-stu-id="4cf63-196">hello test simulates hello blob sizes associated with hello different volume types on hello device.</span></span> <span data-ttu-id="4cf63-197">Normal katmanlı ve yerel olarak sabitlenmiş birimlerin yedekleri, 64 KB blob boyutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="4cf63-197">Regular tiered and backups of locally pinned volumes use a 64 KB blob size.</span></span> <span data-ttu-id="4cf63-198">Arşiv seçeneği işaretli olan katmanlı birimler 512 KB blob veri boyutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="4cf63-198">Tiered volumes with archive option checked use 512 KB blob data size.</span></span> <span data-ttu-id="4cf63-199">Cihazınız varsa, katmanlı ve yerel olarak sabitlenmiş birimleri yapılandırılmış, veri boyutu çalıştırmak yalnızca hello test karşılık gelen too64 KB blob.</span><span class="sxs-lookup"><span data-stu-id="4cf63-199">If your device has tiered and locally pinned volumes configured, only hello test corresponding too64 KB blob data size is run.</span></span>

<span data-ttu-id="4cf63-200">toouse bu aracı, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="4cf63-200">toouse this tool, perform hello following steps:</span></span>

1.  <span data-ttu-id="4cf63-201">İlk olarak, katmanlı birimleri ve katmanlı birimlerin bir karışımını işaretli arşivlenmiş seçeneğiyle oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4cf63-201">First, create a mix of tiered volumes and tiered volumes with archived option checked.</span></span> <span data-ttu-id="4cf63-202">Bu eylemin hello aracı hello testleri 64 KB ve 512 KB için kabarcık boyutları gerçekleştirilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="4cf63-202">This action ensures that hello tool runs hello tests for both 64 KB and 512 KB blob sizes.</span></span>

2. <span data-ttu-id="4cf63-203">Oluşturulan ve hello birimleri yapılandırdıktan sonra hello cmdlet'ini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4cf63-203">Run hello cmdlet after you have created and configured hello volumes.</span></span> <span data-ttu-id="4cf63-204">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="4cf63-204">Type:</span></span>

    `Invoke-HcsDiagnostics -Scope Performance`

3. <span data-ttu-id="4cf63-205">Merhaba aracı tarafından raporlanan hello okuma-yazma gecikmeleri not edin.</span><span class="sxs-lookup"><span data-stu-id="4cf63-205">Make a note of hello read-write latencies reported by hello tool.</span></span> <span data-ttu-id="4cf63-206">Bu test hello sonuçları raporlar önce birkaç dakika toorun alabilir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-206">This test can take several minutes toorun before it reports hello results.</span></span>

4. <span data-ttu-id="4cf63-207">Merhaba bağlantı gecikme olması durumunda tüm hello altında aralığı beklenen sonra hello hello aracı tarafından raporlanan gecikme maksimum ulaşılabilir hedefi hello iş yükleri dağıtırken kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-207">If hello connection latencies are all under hello expected range, then hello latencies reported by hello tool can be used as maximum achievable target when deploying hello workloads.</span></span> <span data-ttu-id="4cf63-208">İç veri işleme için bazı ek faktörü.</span><span class="sxs-lookup"><span data-stu-id="4cf63-208">Factor in some overhead for internal data processing.</span></span>

    <span data-ttu-id="4cf63-209">Merhaba okuma-yazma gecikmeleri tarafından bildirilen varsa hello Tanılama Aracı yüksek şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4cf63-209">If hello read-write latencies reported by hello diagnostics tool are high:</span></span>

    1. <span data-ttu-id="4cf63-210">Storage Analytics blob Hizmetleri için yapılandırma ve hello çıktı toounderstand hello gecikmeleri hello Azure depolama hesabı için analiz edin.</span><span class="sxs-lookup"><span data-stu-id="4cf63-210">Configure Storage Analytics for blob services and analyze hello output toounderstand hello latencies for hello Azure storage account.</span></span> <span data-ttu-id="4cf63-211">Ayrıntılı yönergeler için çok Git[etkinleştirme ve Storage Analytics yapılandırma](../storage/common/storage-enable-and-view-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="4cf63-211">For detailed instructions, go too[enable and configure Storage Analytics](../storage/common/storage-enable-and-view-metrics.md).</span></span> <span data-ttu-id="4cf63-212">Bu gecikme süreleri de yüksek ve karşılaştırılabilir toohello numaraları hello StorSimple Tanılama Aracı ' alınan varsa, Azure depolama olan hizmet isteği toolog gerekir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-212">If those latencies are also high and comparable toohello numbers you received from hello StorSimple Diagnostics tool, then you need toolog a service request with Azure storage.</span></span>

    2. <span data-ttu-id="4cf63-213">Merhaba depolama hesabı gecikmeleri düşükse, ağınızdaki herhangi gecikmesi sorunları, ağ yöneticisi tooinvestigate başvurun.</span><span class="sxs-lookup"><span data-stu-id="4cf63-213">If hello storage account latencies are low, contact your network administrator tooinvestigate any latency issues in your network.</span></span>

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a><span data-ttu-id="4cf63-214">Örnek çıktı performans testi 8100 cihazda çalıştırın</span><span class="sxs-lookup"><span data-stu-id="4cf63-214">Sample output of performance test run on an 8100 device</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Performance
Running performance diagnostics...
--------------------------------------------------
Cloud performance: writing blobs
Cloud write latency: 194 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: reading blobs..
Cloud read latency: 544 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: writing blobs.
Cloud write latency: 369 ms using credential 'myss8000storageacct', blob size '512KB'
Cloud performance: reading blobs...
Cloud read latency: 4924 ms using credential 'myss8000storageacct', blob size '512KB'
--------------------------------------------------
Controller0>
```

## <a name="appendix-interpreting-system-information"></a><span data-ttu-id="4cf63-215">Ek: Sistem bilgileri yorumlama</span><span class="sxs-lookup"><span data-stu-id="4cf63-215">Appendix: interpreting system information</span></span>

<span data-ttu-id="4cf63-216">Merhaba sistem bilgileri çeşitli Windows PowerShell parametreleri Eşle hangi hello açıklayan bir tablo aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-216">Here is a table describing what hello various Windows PowerShell parameters in hello system information map to.</span></span> 

| <span data-ttu-id="4cf63-217">PowerShell parametresi</span><span class="sxs-lookup"><span data-stu-id="4cf63-217">PowerShell Parameter</span></span>    | <span data-ttu-id="4cf63-218">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4cf63-218">Description</span></span>  |
|-------------------------|------------------|
| <span data-ttu-id="4cf63-219">Örnek Kimliği</span><span class="sxs-lookup"><span data-stu-id="4cf63-219">Instance ID</span></span>             | <span data-ttu-id="4cf63-220">Benzersiz bir tanımlayıcı her denetleyici yok veya bir GUID ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="4cf63-220">Every controller has a unique identifier or a GUID associated with it.</span></span>|
| <span data-ttu-id="4cf63-221">Ad</span><span class="sxs-lookup"><span data-stu-id="4cf63-221">Name</span></span>                    | <span data-ttu-id="4cf63-222">Merhaba hello Azure portal cihaz dağıtımı sırasında yapılandırılan hello cihazın kolay adı.</span><span class="sxs-lookup"><span data-stu-id="4cf63-222">hello friendly name of hello device as configured through hello Azure portal during device deployment.</span></span> <span data-ttu-id="4cf63-223">Merhaba varsayılan kolay hello cihaz seri numarasını adıdır.</span><span class="sxs-lookup"><span data-stu-id="4cf63-223">hello default friendly name is hello device serial number.</span></span> |
| <span data-ttu-id="4cf63-224">modeli</span><span class="sxs-lookup"><span data-stu-id="4cf63-224">Model</span></span>                   | <span data-ttu-id="4cf63-225">StorSimple 8000 serisi Cihazınızı Hello modeli.</span><span class="sxs-lookup"><span data-stu-id="4cf63-225">hello model of your StorSimple 8000 series device.</span></span> <span data-ttu-id="4cf63-226">Merhaba modeli 8100 veya 8600 olabilir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-226">hello model can be 8100 or 8600.</span></span>|
| <span data-ttu-id="4cf63-227">seri numarası</span><span class="sxs-lookup"><span data-stu-id="4cf63-227">SerialNumber</span></span>            | <span data-ttu-id="4cf63-228">Merhaba cihaz seri numarasını hello fabrikada atanır ve 15 karakterden uzun.</span><span class="sxs-lookup"><span data-stu-id="4cf63-228">hello device serial number is assigned at hello factory and is 15 characters long.</span></span> <span data-ttu-id="4cf63-229">Örneğin, 8600 SHX0991003G44HT gösterir:</span><span class="sxs-lookup"><span data-stu-id="4cf63-229">For instance, 8600-SHX0991003G44HT indicates:</span></span><br> <span data-ttu-id="4cf63-230">8600 – hello aygıt modelidir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-230">8600 – Is hello device model.</span></span><br><span data-ttu-id="4cf63-231">SHX – hello site ürettiğini.</span><span class="sxs-lookup"><span data-stu-id="4cf63-231">SHX – Is hello manufacturing site.</span></span><br> <span data-ttu-id="4cf63-232">0991003 - belirli bir ürün var.</span><span class="sxs-lookup"><span data-stu-id="4cf63-232">0991003 - Is a specific product.</span></span> <br> <span data-ttu-id="4cf63-233">G44HT hello son 5 basamakların toocreate benzersiz seri numaraları artar.</span><span class="sxs-lookup"><span data-stu-id="4cf63-233">G44HT- hello last 5 digits are incremented toocreate unique serial numbers.</span></span> <span data-ttu-id="4cf63-234">Bu ardışık olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-234">This may not be a sequential set.</span></span>|
| <span data-ttu-id="4cf63-235">saat dilimi</span><span class="sxs-lookup"><span data-stu-id="4cf63-235">TimeZone</span></span>                | <span data-ttu-id="4cf63-236">hello Azure portalına cihaz dağıtımı sırasında yapılandırılan Hello aygıt saat dilimi.</span><span class="sxs-lookup"><span data-stu-id="4cf63-236">hello device time zone as configured in hello Azure portal during device deployment.</span></span>|
| <span data-ttu-id="4cf63-237">CurrentController</span><span class="sxs-lookup"><span data-stu-id="4cf63-237">CurrentController</span></span>       | <span data-ttu-id="4cf63-238">StorSimple Cihazınızı bağlı toothrough hello Windows PowerShell arabirimi olan hello denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="4cf63-238">hello controller that you are connected toothrough hello Windows PowerShell interface of your StorSimple device.</span></span>|
| <span data-ttu-id="4cf63-239">ActiveController</span><span class="sxs-lookup"><span data-stu-id="4cf63-239">ActiveController</span></span>        | <span data-ttu-id="4cf63-240">Cihazınızda etkin olduğunda ve ağ ve disk hello işlemleri denetleme hello denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="4cf63-240">hello controller that is active on your device and is controlling all hello network and disk operations.</span></span> <span data-ttu-id="4cf63-241">Bu denetleyici 0 veya denetleyici 1 olabilir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-241">This can be Controller 0 or Controller 1.</span></span>  |
| <span data-ttu-id="4cf63-242">Controller0Status</span><span class="sxs-lookup"><span data-stu-id="4cf63-242">Controller0Status</span></span>       | <span data-ttu-id="4cf63-243">Denetleyici 0 aygıtınızda Hello durumu.</span><span class="sxs-lookup"><span data-stu-id="4cf63-243">hello status of Controller 0 on your device.</span></span> <span data-ttu-id="4cf63-244">Merhaba denetleyicisi durumunu normal, kurtarma modunda veya erişilemiyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-244">hello controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="4cf63-245">Controller1Status</span><span class="sxs-lookup"><span data-stu-id="4cf63-245">Controller1Status</span></span>       | <span data-ttu-id="4cf63-246">Denetleyici 1 Hello durumu, Cihazınızda.</span><span class="sxs-lookup"><span data-stu-id="4cf63-246">hello status of Controller 1 on your device.</span></span>  <span data-ttu-id="4cf63-247">Merhaba denetleyicisi durumunu normal, kurtarma modunda veya erişilemiyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-247">hello controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="4cf63-248">SystemMode</span><span class="sxs-lookup"><span data-stu-id="4cf63-248">SystemMode</span></span>              | <span data-ttu-id="4cf63-249">StorSimple Cihazınızı genel durumunu hello.</span><span class="sxs-lookup"><span data-stu-id="4cf63-249">hello overall status of your StorSimple device.</span></span> <span data-ttu-id="4cf63-250">Merhaba Aygıt durumu normal, olabilir Bakım veya yetkisi alınmış (hello Azure portal toodeactivated karşılık gelir).</span><span class="sxs-lookup"><span data-stu-id="4cf63-250">hello device status can be normal, maintenance, or decommissioned (corresponds toodeactivated in hello Azure portal).</span></span>|
| <span data-ttu-id="4cf63-251">FriendlySoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="4cf63-251">FriendlySoftwareVersion</span></span> | <span data-ttu-id="4cf63-252">toohello aygıt yazılım sürümü karşılık gelen hello kolay dizesi.</span><span class="sxs-lookup"><span data-stu-id="4cf63-252">hello friendly string that corresponds toohello device software version.</span></span> <span data-ttu-id="4cf63-253">Güncelleştirme 4 ile çalışan bir sistem için hello kolay yazılım sürüm StorSimple 8000 serisi güncelleştirme 4.0 olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4cf63-253">For a system running Update 4, hello friendly software version would be StorSimple 8000 Series Update 4.0.</span></span>|
| <span data-ttu-id="4cf63-254">HcsSoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="4cf63-254">HcsSoftwareVersion</span></span>      | <span data-ttu-id="4cf63-255">Merhaba HCS yazılım sürümü, cihazda çalışan.</span><span class="sxs-lookup"><span data-stu-id="4cf63-255">hello HCS software version running on your device.</span></span> <span data-ttu-id="4cf63-256">Örneği için hello HCS yazılım sürüm karşılık gelen tooStorSimple 8000 serisi güncelleştirme 4.0 sürümünün 6.3.9600.17820.</span><span class="sxs-lookup"><span data-stu-id="4cf63-256">For instance, hello HCS software version corresponding tooStorSimple 8000 Series Update 4.0 is 6.3.9600.17820.</span></span> |
| <span data-ttu-id="4cf63-257">ApiVersion</span><span class="sxs-lookup"><span data-stu-id="4cf63-257">ApiVersion</span></span>              | <span data-ttu-id="4cf63-258">Merhaba Windows PowerShell API'si hello HCS cihazı Hello yazılım sürümü.</span><span class="sxs-lookup"><span data-stu-id="4cf63-258">hello software version of hello Windows PowerShell API of hello HCS device.</span></span>|
| <span data-ttu-id="4cf63-259">VhdVersion</span><span class="sxs-lookup"><span data-stu-id="4cf63-259">VhdVersion</span></span>              | <span data-ttu-id="4cf63-260">cihaz hello hello Fabrika görüntüsünden Hello yazılımı sürümü ile birlikte gelen.</span><span class="sxs-lookup"><span data-stu-id="4cf63-260">hello software version of hello factory image that hello device was shipped with.</span></span> <span data-ttu-id="4cf63-261">Ardından, cihaz toofactory Varsayılanları sıfırlarsanız, bu yazılım sürümü çalışır.</span><span class="sxs-lookup"><span data-stu-id="4cf63-261">If you reset your device toofactory defaults, then it runs this software version.</span></span>|
| <span data-ttu-id="4cf63-262">OSVersion</span><span class="sxs-lookup"><span data-stu-id="4cf63-262">OSVersion</span></span>               | <span data-ttu-id="4cf63-263">Merhaba cihazda çalışan hello Windows Server işletim sisteminin Hello yazılım sürümü.</span><span class="sxs-lookup"><span data-stu-id="4cf63-263">hello software version of hello Windows Server operating system running on hello device.</span></span> <span data-ttu-id="4cf63-264">Merhaba StorSimple cihazı too6.3.9600 karşılık gelen Windows Server 2012 R2 hello temel alır.</span><span class="sxs-lookup"><span data-stu-id="4cf63-264">hello StorSimple device is based off hello Windows Server 2012 R2 that corresponds too6.3.9600.</span></span>|
| <span data-ttu-id="4cf63-265">CisAgentVersion</span><span class="sxs-lookup"><span data-stu-id="4cf63-265">CisAgentVersion</span></span>         | <span data-ttu-id="4cf63-266">StorSimple Cihazınızda çalıştıran CIS aracınızı Hello sürüm.</span><span class="sxs-lookup"><span data-stu-id="4cf63-266">hello version for your Cis agent running on your StorSimple device.</span></span> <span data-ttu-id="4cf63-267">Bu aracı, Azure'da çalışan hello StorSimple Yöneticisi hizmetiyle iletişim yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="4cf63-267">This agent helps communicate with hello StorSimple Manager service running in Azure.</span></span>|
| <span data-ttu-id="4cf63-268">MdsAgentVersion</span><span class="sxs-lookup"><span data-stu-id="4cf63-268">MdsAgentVersion</span></span>         | <span data-ttu-id="4cf63-269">StorSimple Cihazınızda çalıştıran hello sürüm karşılık gelen toohello Mds Aracısı.</span><span class="sxs-lookup"><span data-stu-id="4cf63-269">hello version corresponding toohello Mds agent running on your StorSimple device.</span></span> <span data-ttu-id="4cf63-270">Bu aracı veri toohello taşır izleme ve Tanılama Hizmeti (MDS).</span><span class="sxs-lookup"><span data-stu-id="4cf63-270">This agent moves data toohello Monitoring and Diagnostics Service (MDS).</span></span>|
| <span data-ttu-id="4cf63-271">Lsisas2Version</span><span class="sxs-lookup"><span data-stu-id="4cf63-271">Lsisas2Version</span></span>          | <span data-ttu-id="4cf63-272">Sürüm karşılık gelen toohello LSI sürücüleri, StorSimple Cihazınızda hello.</span><span class="sxs-lookup"><span data-stu-id="4cf63-272">hello version corresponding toohello LSI drivers on your StorSimple device.</span></span>|
| <span data-ttu-id="4cf63-273">Kapasite</span><span class="sxs-lookup"><span data-stu-id="4cf63-273">Capacity</span></span>                | <span data-ttu-id="4cf63-274">Merhaba aygıt bayt cinsinden toplam kapasitesini Hello.</span><span class="sxs-lookup"><span data-stu-id="4cf63-274">hello total capacity of hello device in bytes.</span></span>|
| <span data-ttu-id="4cf63-275">RemoteManagementMode</span><span class="sxs-lookup"><span data-stu-id="4cf63-275">RemoteManagementMode</span></span>    | <span data-ttu-id="4cf63-276">Merhaba aygıt kendi Windows PowerShell arabirimi uzaktan yönetilebilir olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-276">Indicates whether hello device can be remotely managed via its Windows PowerShell interface.</span></span> |
| <span data-ttu-id="4cf63-277">FipsMode</span><span class="sxs-lookup"><span data-stu-id="4cf63-277">FipsMode</span></span>                | <span data-ttu-id="4cf63-278">Cihazınızda Hello Amerika Birleşik Devletleri Federal Bilgi İşleme Standardı (FIPS) modunun etkinleştirilip etkinleştirilmeyeceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-278">Indicates whether hello United States Federal Information Processing Standard (FIPS) mode is enabled on your device.</span></span> <span data-ttu-id="4cf63-279">Merhaba FIPS 140 standardı, gizli verilerin hello koruma için BİZE Federal hükümeti bilgisayar sistemleri tarafından kullanım için onaylanan şifreleme algoritmalarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="4cf63-279">hello FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for hello protection of sensitive data.</span></span> <span data-ttu-id="4cf63-280">Güncelleştirme 4 veya üstünü çalıştıran cihazlar için FIPS modunda varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="4cf63-280">For devices running Update 4 or later, FIPS mode is enabled by default.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4cf63-281">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4cf63-281">Next steps</span></span>

* <span data-ttu-id="4cf63-282">Merhaba öğrenin [hello Invoke-HcsDiagnostics cmdlet sözdizimi](https://technet.microsoft.com/library/mt795371.aspx).</span><span class="sxs-lookup"><span data-stu-id="4cf63-282">Learn hello [syntax of hello Invoke-HcsDiagnostics cmdlet](https://technet.microsoft.com/library/mt795371.aspx).</span></span>

* <span data-ttu-id="4cf63-283">Hakkında daha fazla çok bilgi[dağıtım sorunlarını giderme](storsimple-troubleshoot-deployment.md) , StorSimple Cihazınızda.</span><span class="sxs-lookup"><span data-stu-id="4cf63-283">Learn more about how too[troubleshoot deployment issues](storsimple-troubleshoot-deployment.md) on your StorSimple device.</span></span>
