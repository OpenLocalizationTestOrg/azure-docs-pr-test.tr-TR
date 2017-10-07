---
title: "aaaConnecting güvenlik ürünleri toohello Operations Management Suite (OMS) güvenlik ve denetim çözümü | Microsoft Docs"
description: "Bu belge, tooconnect Yönetim Paketi güvenlik ve denetim ortak olay biçimini kullanarak çözüm güvenlik ürünleri tooOperations yardımcı olur."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 46eee484-e078-4bad-8c89-c88a3508f6aa
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 0f4b372d0379987c4e249628a3c8d52733be65c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-your-security-products-toohello-operations-management-suite-oms-security-and-audit-solution"></a><span data-ttu-id="33308-103">Güvenlik ürünleri toohello Operations Management Suite (OMS) güvenlik ve denetim çözümü bağlanma</span><span class="sxs-lookup"><span data-stu-id="33308-103">Connecting your security products toohello Operations Management Suite (OMS) Security and Audit Solution</span></span> 
<span data-ttu-id="33308-104">Bu belgede güvenlik ürünlerinizi hello OMS güvenlik ve denetim çözümü bağlanmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="33308-104">This document helps you connect your security products into hello OMS Security and Audit Solution.</span></span> <span data-ttu-id="33308-105">Aşağıdaki kaynaklar hello desteklenir:</span><span class="sxs-lookup"><span data-stu-id="33308-105">hello following sources are supported:</span></span>

- <span data-ttu-id="33308-106">Common Event Format (CEF) olayları</span><span class="sxs-lookup"><span data-stu-id="33308-106">Common Event Format (CEF) events</span></span>
- <span data-ttu-id="33308-107">Cisco ASA olayları</span><span class="sxs-lookup"><span data-stu-id="33308-107">Cisco ASA events</span></span>


## <a name="what-is-cef"></a><span data-ttu-id="33308-108">CEF nedir?</span><span class="sxs-lookup"><span data-stu-id="33308-108">What is CEF?</span></span>
<span data-ttu-id="33308-109">Ortak olay biçimi (CEF) endüstri standardı bir biçime Syslog iletileri, çok sayıda güvenlik satıcılar tooallow olay birlikte çalışabilirliğini farklı platformlar tarafından kullanılan en üstünde ' dir.</span><span class="sxs-lookup"><span data-stu-id="33308-109">Common Event Format (CEF) is an industry standard format on top of Syslog messages, used by many security vendors tooallow event interoperability among different platforms.</span></span> <span data-ttu-id="33308-110">OMS güvenlik ve denetim çözüm veri alımı tooconnect etkinleştirir olduğunda CEF güvenlik ürünlerinizi OMS güvenliği ile kullanma desteği.</span><span class="sxs-lookup"><span data-stu-id="33308-110">OMS Security and Audit Solution support data ingestion using CEF, which enables you tooconnect your security products with OMS Security.</span></span> 

<span data-ttu-id="33308-111">Veri kaynağı tooOMS bağlanarak bu platform parçası olan özellikler aşağıdaki hello mümkün tootake avantajı şunlardır:</span><span class="sxs-lookup"><span data-stu-id="33308-111">By connecting your data source tooOMS, you are able tootake advantage of hello following capabilities that are part of this platform:</span></span>

- <span data-ttu-id="33308-112">Arama ve Bağıntı</span><span class="sxs-lookup"><span data-stu-id="33308-112">Search & Correlation</span></span>
- <span data-ttu-id="33308-113">Denetim</span><span class="sxs-lookup"><span data-stu-id="33308-113">Auditing</span></span>
- <span data-ttu-id="33308-114">Uyarı</span><span class="sxs-lookup"><span data-stu-id="33308-114">Alert</span></span>
- <span data-ttu-id="33308-115">Tehdit Bilgisi</span><span class="sxs-lookup"><span data-stu-id="33308-115">Threat Intelligence</span></span>
- <span data-ttu-id="33308-116">Önemli sorunlar</span><span class="sxs-lookup"><span data-stu-id="33308-116">Notable Issues</span></span>

## <a name="collection-of-security-solution-logs"></a><span data-ttu-id="33308-117">Güvenlik çözümü günlüklerinin toplanması</span><span class="sxs-lookup"><span data-stu-id="33308-117">Collection of security solution logs</span></span>

<span data-ttu-id="33308-118">OMS Security, CEF kullanarak Syslog’lar ve [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/) günlükleri üzerinden günlüklerin toplanmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="33308-118">OMS Security supports collection of logs using CEF over Syslogs and [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/) logs.</span></span> <span data-ttu-id="33308-119">Bu örnekte, hello (Merhaba günlükleri oluşturur bilgisayar) ng syslog arka plan programı çalıştıran bir Linux bilgisayar kaynaktır ve OMS güvenlik hello hedefidir.</span><span class="sxs-lookup"><span data-stu-id="33308-119">In this example, hello source (computer that generates hello logs) is a Linux computer running syslog-ng daemon and hello target is OMS Security.</span></span> <span data-ttu-id="33308-120">Aşağıdaki tooperform hello gerekir tooprepare hello Linux bilgisayarı görevler:</span><span class="sxs-lookup"><span data-stu-id="33308-120">tooprepare hello Linux computer you will need tooperform hello following tasks:</span></span>

- <span data-ttu-id="33308-121">Merhaba OMS aracısı veya üzeri Linux, sürüm 1.2.0-25 için indirin.</span><span class="sxs-lookup"><span data-stu-id="33308-121">Download hello OMS Agent for Linux, version 1.2.0-25 or above.</span></span>
- <span data-ttu-id="33308-122">Merhaba bölümü izleyin **Hızlı Yükleme Kılavuzu** gelen [bu makalede](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall ve yerleşik hello Aracısı tooyour çalışma.</span><span class="sxs-lookup"><span data-stu-id="33308-122">Follow hello section **Quick Install Guide** from [this article](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall and onboard hello agent tooyour workspace.</span></span>

<span data-ttu-id="33308-123">Genellikle, hello Aracısı hangi hello günlükleri birinde üretilen hello bilgisayardan farklı bir bilgisayara yüklenir.</span><span class="sxs-lookup"><span data-stu-id="33308-123">Typically, hello agent is installed on a different computer from hello one on which hello logs are generated.</span></span> <span data-ttu-id="33308-124">İletme hello günlükleri toohello aracı makine genellikle aşağıdaki adımları hello gerektirir:</span><span class="sxs-lookup"><span data-stu-id="33308-124">Forwarding hello logs toohello agent machine will usually require hello following steps:</span></span>

- <span data-ttu-id="33308-125">Ürün/makine tooforward hello gerekli olayları toohello syslog arka plan programı (rsyslog veya syslog ng) günlüğü hello hello aracı makinede yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="33308-125">Configure hello logging product/machine tooforward hello required events toohello syslog daemon (rsyslog or syslog-ng) on hello agent machine.</span></span>
- <span data-ttu-id="33308-126">Uzaktaki sistemden Merhaba aracı makine tooreceive iletileri Hello syslog arka plan etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="33308-126">Enable hello syslog daemon on hello agent machine tooreceive messages from a remote system.</span></span>

<span data-ttu-id="33308-127">Merhaba aracı makinede hello olayları hello syslog arka plan programı toolocal UDP bağlantı noktasından 25226 gönderilen toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="33308-127">On hello agent machine, hello events need toobe sent from hello syslog daemon toolocal UDP port 25226.</span></span> <span data-ttu-id="33308-128">Merhaba Aracısı, bu bağlantı noktasına gelen olaylar için dinliyor.</span><span class="sxs-lookup"><span data-stu-id="33308-128">hello agent is listening for incoming events on this port.</span></span> <span data-ttu-id="33308-129">Merhaba, (yerel ayarlarınızı hello yapılandırma toofit değiştirebilirsiniz) hello yerel sistem toohello Aracısı'ndan tüm olayları göndermek için örnek bir yapılandırma aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="33308-129">hello following is an example configuration for sending all events from hello local system toohello agent (you can modify hello configuration toofit your local settings):</span></span>

1. <span data-ttu-id="33308-130">Açık hello terminal penceresi ve Git toohello directory */etc/syslog-ng /*</span><span class="sxs-lookup"><span data-stu-id="33308-130">Open hello terminal window, and go toohello directory */etc/syslog-ng/*</span></span> 
2. <span data-ttu-id="33308-131">Yeni bir dosya oluşturun *güvenlik config omsagent.conf* ve içeriği aşağıdaki hello ekleyin: OMS_facility local4 =</span><span class="sxs-lookup"><span data-stu-id="33308-131">Create a new file *security-config-omsagent.conf* and add hello following content:  OMS_facility = local4</span></span>
    
    <span data-ttu-id="33308-132">filter f_local4_oms { facility(local4); };</span><span class="sxs-lookup"><span data-stu-id="33308-132">filter f_local4_oms { facility(local4); };</span></span>

    <span data-ttu-id="33308-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span><span class="sxs-lookup"><span data-stu-id="33308-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span></span>

    <span data-ttu-id="33308-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span><span class="sxs-lookup"><span data-stu-id="33308-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span></span>
    
3. <span data-ttu-id="33308-135">Merhaba dosya indirme *security_events.conf* ve yerleştirin */etc/opt/microsoft/omsagent/conf/omsagent.d/* hello OMS Aracısı bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="33308-135">Download hello file *security_events.conf* and place at */etc/opt/microsoft/omsagent/conf/omsagent.d/* in hello OMS Agent computer.</span></span>
4. <span data-ttu-id="33308-136">Merhaba toorestart hello syslog arka plan programı aşağıdaki komutu yazın: *syslog ng çalıştırmak için:*</span><span class="sxs-lookup"><span data-stu-id="33308-136">Type hello command below toorestart hello syslog daemon:  *For syslog-ng run:*</span></span>
    
    ```
    sudo service rsyslog restart
    ```

    <span data-ttu-id="33308-137">*For rsyslog run:*</span><span class="sxs-lookup"><span data-stu-id="33308-137">*For rsyslog run:*</span></span>
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. <span data-ttu-id="33308-138">Toorestart hello OMS aracısı aşağıdaki Hello komutunu yazın:</span><span class="sxs-lookup"><span data-stu-id="33308-138">Type hello command below toorestart hello OMS Agent:</span></span>

    <span data-ttu-id="33308-139">*For syslog-ng run:*</span><span class="sxs-lookup"><span data-stu-id="33308-139">*For syslog-ng run:*</span></span>
    
    ```
    sudo service omsagent restart
    ```

    <span data-ttu-id="33308-140">*For rsyslog run:*</span><span class="sxs-lookup"><span data-stu-id="33308-140">*For rsyslog run:*</span></span>
    
    ```
    systemctl restart omsagent
    ```
6. <span data-ttu-id="33308-141">Merhaba aşağıdaki komutu yazın ve hello OMS Aracısı günlüğünde hatalar yoktur hello sonuç tooconfirm gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="33308-141">Type hello command below and review hello result tooconfirm that there are no errors in hello OMS Agent log:</span></span>

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a><span data-ttu-id="33308-142">Toplanan güvenlik olaylarını gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="33308-142">Reviewing collected security events</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

<span data-ttu-id="33308-143">Merhaba yapılandırma bittikten sonra hello güvenlik olayı OMS güvenliği tarafından alınan toobe başlar.</span><span class="sxs-lookup"><span data-stu-id="33308-143">After hello configuration is over, hello security event will start toobe ingested by OMS Security.</span></span> <span data-ttu-id="33308-144">toovisualize bu olayları, açık hello günlük arama hello komutunu yazın *türü CommonSecurityLog =* hello arama alanı ve ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="33308-144">toovisualize those events, open hello Log Search, type hello command *Type=CommonSecurityLog* in hello search field and press ENTER.</span></span> <span data-ttu-id="33308-145">Merhaba aşağıdaki örnek hello sonucunu bu komut gösterir, bu durumda OMS güvenlik zaten güvenlik günlüklerini birden çok satıcılardan alınan olduğunu dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="33308-145">hello following example shows hello result of this command, notice that in this case OMS Security already ingested security logs from multiple vendors:</span></span>
   
![OMS Güvenlik ve Denetim Temeli Değerlendirmesi](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

<span data-ttu-id="33308-147">Tek tek bir satıcı için örneğin, çevrimiçi Cisco günlüklerini toovisualize, türü bu arama iyileştirebilirsiniz: *türü CommonSecurityLog DeviceVendor = Cisco =*.</span><span class="sxs-lookup"><span data-stu-id="33308-147">You can refine this search for one single vendor, for example, toovisualize online Cisco logs, type: *Type=CommonSecurityLog DeviceVendor=Cisco*.</span></span> <span data-ttu-id="33308-148">Merhaba "CommonSecurityLog", "Özel uzantısının" olsun veya olmasın, başka bir uzantı sırasında hello temel extensios de dahil olmak üzere herhangi bir olduğunda CEF başlığını eklenecek için "Ekuzantılar" alanına alanları önceden tanımlanmış.</span><span class="sxs-lookup"><span data-stu-id="33308-148">hello “CommonSecurityLog” has predefined fields for any CEF header including hello basic extensios, while any other extension whether it’s “Custom Extension” or not, will be inserted into "AdditionalExtensions" field.</span></span> <span data-ttu-id="33308-149">Merhaba özel alanlar özellik ayrılmış tooget alanlardan bunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33308-149">You can use hello Custom Fields feature tooget dedicated fields from it.</span></span> 

### <a name="accessing-computers-missing-baseline-assessment"></a><span data-ttu-id="33308-150">Temel değerlendirmesi eksik bilgisayarlara erişim</span><span class="sxs-lookup"><span data-stu-id="33308-150">Accessing computers missing baseline assessment</span></span>
<span data-ttu-id="33308-151">OMS hello etki alanı üyesi temel profil tooWindows Server 2012 R2'in Windows Server 2008 R2'de destekler.</span><span class="sxs-lookup"><span data-stu-id="33308-151">OMS supports hello domain member baseline profile on Windows Server 2008 R2 up tooWindows Server 2012 R2.</span></span> <span data-ttu-id="33308-152">Windows Server 2016 temeli, henüz tamamlanmamıştır ve yayımlandıktan hemen sonra eklenecektir.</span><span class="sxs-lookup"><span data-stu-id="33308-152">Windows Server 2016 baseline isn’t final yet and will be added as soon as it is published.</span></span> <span data-ttu-id="33308-153">OMS güvenlik ve denetim temel değerlendirmesi taranan tüm diğer işletim sistemlerinin hello altında görünür **temeli değerlendirme eksik olan bilgisayarlar** bölümü.</span><span class="sxs-lookup"><span data-stu-id="33308-153">All other operating systems scanned via OMS Security and Audit baseline assessment appear under hello **Computers missing baseline assessment** section.</span></span>

## <a name="see-also"></a><span data-ttu-id="33308-154">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="33308-154">See also</span></span>
<span data-ttu-id="33308-155">Bu belgede, nasıl öğrenilen tooconnect olduğunda CEF çözüm tooOMS.</span><span class="sxs-lookup"><span data-stu-id="33308-155">In this document, you learned how tooconnect your CEF solution tooOMS.</span></span> <span data-ttu-id="33308-156">toolearn OMS güvenlik hakkında daha fazla bilgi makaleleri aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="33308-156">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="33308-157">Operations Management Suite'e (OMS) genel bakış</span><span class="sxs-lookup"><span data-stu-id="33308-157">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="33308-158">İzleme ve yanıt tooSecurity uyarıları Operations Management Suite güvenlik ve denetim çözümü</span><span class="sxs-lookup"><span data-stu-id="33308-158">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="33308-159">Operations Management Suite Güvenlik ve Denetim Çözümünde Kaynakları İzleme</span><span class="sxs-lookup"><span data-stu-id="33308-159">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

