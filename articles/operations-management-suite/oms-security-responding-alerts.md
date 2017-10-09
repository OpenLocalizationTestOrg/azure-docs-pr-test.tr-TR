---
title: "aaaMonitoring ve yanıt tooSecurity uyarıları Operations Management Suite güvenlik ve denetim çözüm | Microsoft Docs"
description: "Bu belge, toouse hello tehdit Intelligence seçeneği OMS güvenlik ve denetim toomonitor kullanılabilir yardımcı olur ve toosecurity uyarıları yanıt."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 7d45a32b-1341-4bb5-a436-1f42a8a2590a
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/13/2017
ms.author: yurid
ms.openlocfilehash: 3d92b6809b7bd934c889afc119e5e34ff2b85f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-responding-toosecurity-alerts-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="f5c5d-103">İzleme ve yanıt toosecurity uyarıları Operations Management Suite güvenlik ve denetim çözümü</span><span class="sxs-lookup"><span data-stu-id="f5c5d-103">Monitoring and responding toosecurity alerts in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="f5c5d-104">Bu belge hello tehdit Intelligence seçeneği OMS güvenlik ve denetim toomonitor kullanılabilir kullanın ve toosecurity uyarıları yanıt yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="f5c5d-104">This document helps you use hello threat intelligence option available in OMS Security and Audit toomonitor and respond toosecurity alerts.</span></span>

## <a name="what-is-oms"></a><span data-ttu-id="f5c5d-105">OMS nedir?</span><span class="sxs-lookup"><span data-stu-id="f5c5d-105">What is OMS?</span></span>
<span data-ttu-id="f5c5d-106">Microsoft Operations Management Suite (OMS) Microsoft'un bulut yönetmek ve şirket içi korumak ve altyapı bulut yardımcı olan BT yönetim çözümü dayalıdır.</span><span class="sxs-lookup"><span data-stu-id="f5c5d-106">Microsoft Operations Management Suite (OMS) is Microsoft's cloud based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="f5c5d-107">OMS hakkında daha fazla bilgi için hello makaleyi okuyun [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).</span><span class="sxs-lookup"><span data-stu-id="f5c5d-107">For more information about OMS, read hello article [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).</span></span>

## <a name="threat-intelligence"></a><span data-ttu-id="f5c5d-108">Tehdit bilgileri</span><span class="sxs-lookup"><span data-stu-id="f5c5d-108">Threat intelligence</span></span>
<span data-ttu-id="f5c5d-109">Kullanıcıların geniş kapsamlı erişime toohello ağına sahip ve çok çeşitli aygıtları tooconnect toocorporate verileri kullanan bir kuruluş ortamında, etkin olarak kaynaklarınızı izlemek ve toosecurity olayları hızla yanıt zorunludur.</span><span class="sxs-lookup"><span data-stu-id="f5c5d-109">In an enterprise environment where users have broad access toohello network and use a variety of devices tooconnect toocorporate data, it is imperative that you can actively monitor your resources and quickly respond toosecurity incidents.</span></span> <span data-ttu-id="f5c5d-110">Belirli tehditlere değil yükseltmek bazı siber güvenlik uyarıları çünkü hello güvenlik yaşam döngüsü açısından önemli ya da teknik geleneksel güvenlik denetimleri tarafından tanımlanan kuşkulu etkinlikleri budur.</span><span class="sxs-lookup"><span data-stu-id="f5c5d-110">This is particular important from hello security lifecycle perspective because some cybersecurity threats may not raise alerts or suspicious activities that can be identified by traditional security technical controls.</span></span> 

<span data-ttu-id="f5c5d-111">Hello kullanarak **tehdit bilgileri** seçeneği kullanılabilir OMS güvenlik ve denetim, BT yöneticileri güvenlik tehditlerine karşı hello ortamında, örneğin tanımlamak, belirli bir bilgisayarın parçası olup olmadığını belirleyebilmek bir [ botnet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection).</span><span class="sxs-lookup"><span data-stu-id="f5c5d-111">By using hello **Threat Intelligence** option available in OMS Security and Audit, IT administrators can identify security threats against hello environment, for example, identify if a particular computer is part of a [botnet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection).</span></span> <span data-ttu-id="f5c5d-112">Saldırganlar bu bilgisayar toohello komut ve denetim gizlice bağlandığında kötü amaçlı yazılım yapacağıyla yüklediğinizde bilgisayarlar çoğunlukla düğümler olabilir.</span><span class="sxs-lookup"><span data-stu-id="f5c5d-112">Computers can become nodes in a botnet when attackers illicitly install malware that secretly connects this computer toohello command and control.</span></span> <span data-ttu-id="f5c5d-113">Yeraltı iletişim kanalları, gelen gibi olası tehditler tanımlayabilirsiniz [darknet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection_honeypots_darkents).</span><span class="sxs-lookup"><span data-stu-id="f5c5d-113">It can also identify potential threats coming from underground communication channels, such as [darknet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection_honeypots_darkents).</span></span> 

<span data-ttu-id="f5c5d-114">Sipariş toobuild Microsoft içinde birden fazla kaynaktan gelen veri OMS güvenlik ve denetim bu tehdit bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="f5c5d-114">In order toobuild this threat intelligence, OMS Security and Audit use data coming from multiple sources within Microsoft.</span></span> <span data-ttu-id="f5c5d-115">OMS güvenlik ve denetim verileri bu tooidentify olası tehditlere karşı ortamınızın özelliğinden yararlanır.</span><span class="sxs-lookup"><span data-stu-id="f5c5d-115">OMS Security and Audit will leverage this data tooidentify potential threats against your environment.</span></span>

<span data-ttu-id="f5c5d-116">Merhaba tehdit bilgileri bölmesinde üç ana seçenekleri ile oluşur:</span><span class="sxs-lookup"><span data-stu-id="f5c5d-116">hello Threat Intelligence pane is composed by three major options:</span></span>

* <span data-ttu-id="f5c5d-117">Giden kötü amaçlı trafiğe sahip sunucular</span><span class="sxs-lookup"><span data-stu-id="f5c5d-117">Servers with outbound malicious traffic</span></span>
* <span data-ttu-id="f5c5d-118">Algılanan tehditler türleri</span><span class="sxs-lookup"><span data-stu-id="f5c5d-118">Detected threats types</span></span>
* <span data-ttu-id="f5c5d-119">Tehdit bilgileri haritası</span><span class="sxs-lookup"><span data-stu-id="f5c5d-119">Threat intelligence map</span></span>

> [!NOTE]
> <span data-ttu-id="f5c5d-120">Tüm bu seçenekler genel bakış için okuma [Operations Management Suite güvenlik ve denetim çözümü ile çalışmaya başlama](oms-security-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="f5c5d-120">for an overview of all these options, read [Getting started with Operations Management Suite Security and Audit Solution](oms-security-getting-started.md).</span></span>
> 
> 

### <a name="responding-toosecurity-alerts"></a><span data-ttu-id="f5c5d-121">Yanıt veren toosecurity uyarıları</span><span class="sxs-lookup"><span data-stu-id="f5c5d-121">Responding toosecurity alerts</span></span>
<span data-ttu-id="f5c5d-122">Merhaba adımlardan biri bir [güvenlik olay yanıtlama](https://technet.microsoft.com/library/cc512623.aspx) tooidentify hello önem derecesi hello güvenliğinin aşılmasına sistemleri bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="f5c5d-122">One of hello steps of a [security incident response](https://technet.microsoft.com/library/cc512623.aspx) process is tooidentify hello severity of hello compromise system(s).</span></span> <span data-ttu-id="f5c5d-123">Bu aşamada hello aşağıdaki görevleri gerçekleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="f5c5d-123">In this phase you should perform hello following tasks:</span></span>

* <span data-ttu-id="f5c5d-124">Merhaba saldırı Hello yapısını belirleme</span><span class="sxs-lookup"><span data-stu-id="f5c5d-124">Determine hello nature of hello attack</span></span>
* <span data-ttu-id="f5c5d-125">Merhaba saldırı başlangıç noktasını belirler</span><span class="sxs-lookup"><span data-stu-id="f5c5d-125">Determine hello attack point of origin</span></span>
* <span data-ttu-id="f5c5d-126">Merhaba saldırı Hello amacı belirler.</span><span class="sxs-lookup"><span data-stu-id="f5c5d-126">Determine hello intent of hello attack.</span></span> <span data-ttu-id="f5c5d-127">Özellikle kuruluş tooacquire belirli bilgilerinizi yönlendirilmiş hello saldırı, veya rastgele bekliyordu?</span><span class="sxs-lookup"><span data-stu-id="f5c5d-127">Was hello attack specifically directed at your organization tooacquire specific information, or was it random?</span></span>
* <span data-ttu-id="f5c5d-128">Aşılmış hello sistemleri belirle</span><span class="sxs-lookup"><span data-stu-id="f5c5d-128">Identify hello systems that have been compromised</span></span>
* <span data-ttu-id="f5c5d-129">Erişilen ve bu dosyaların hello duyarlılık belirlemek hello dosyaları belirlemek</span><span class="sxs-lookup"><span data-stu-id="f5c5d-129">Identify hello files that have been accessed and determine hello sensitivity of those files</span></span>

<span data-ttu-id="f5c5d-130">Yararlanabileceğiniz **tehdit bilgileri** bu görevleri ile OMS güvenlik ve denetim çözüm toohelp bilgileri.</span><span class="sxs-lookup"><span data-stu-id="f5c5d-130">You can leverage **Threat Intelligence** information in OMS Security and Audit solution toohelp with these tasks.</span></span> <span data-ttu-id="f5c5d-131">Merhaba tooaccess aşağıda bu adımları **tehdit bilgileri** seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="f5c5d-131">Follow hello steps below tooaccess this **Threat Intelligence** options:</span></span>

1. <span data-ttu-id="f5c5d-132">Merhaba, **Microsoft Operations Management Suite** ana Pano tıklatın **güvenlik ve Denetim** döşeme.</span><span class="sxs-lookup"><span data-stu-id="f5c5d-132">In hello **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
   
    ![Güvenlik ve Denetim](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. <span data-ttu-id="f5c5d-134">Merhaba, **güvenlik ve Denetim** panoyu hello görürsünüz **tehdit bilgileri** aşağıda gösterildiği gibi hello sağ seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="f5c5d-134">In hello **Security and Audit** dashboard, you will see hello **Threat Intelligence** options in hello right, as shown below:</span></span>
   
    ![Tehdit Intel](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig2-ga.png)

<span data-ttu-id="f5c5d-136">Bu üç kutucuklar hello geçerli tehditleri genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="f5c5d-136">These three tiles will give you an overview of hello current threats.</span></span> <span data-ttu-id="f5c5d-137">Merhaba, **giden kötü amaçlı trafiği sunucusuyla** (içinde veya ağınızın dışında) izlemekte olduğunuz herhangi bir bilgisayarda ise mümkün tooidentify olur yani gönderen kötü amaçlı trafiği toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="f5c5d-137">In hello **Server with outbound malicious traffic** you will be able tooidentify if there is any computer that you are monitoring (inside or outside of your network) that is sending malicious traffic toohello Internet.</span></span> 

<span data-ttu-id="f5c5d-138">Merhaba **algılanan tehdit türlerini** döşeme "hello joker" geçerli hello tehditleri özetini gösterir, bu kutucuğa tıkladığınızda bu tehditler hakkında daha fazla ayrıntı Göster aşağıdaki görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="f5c5d-138">hello **Detected threat types** tile shows a summary of hello threats that are current “in hello wild”, if you click on this tile you will see more details about these threats as show below:</span></span>

![Algılanan tehdit türleri](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig3.png)

<span data-ttu-id="f5c5d-140">Tıklayarak her tehdit hakkında daha fazla bilgi ayıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f5c5d-140">You can extract more information about each threat by clicking on it.</span></span> <span data-ttu-id="f5c5d-141">Aşağıdaki örnek Hello Botnet hakkında daha fazla ayrıntı gösterir:</span><span class="sxs-lookup"><span data-stu-id="f5c5d-141">hello example below shows more details about Botnet:</span></span>

![bir tehdit hakkında daha fazla ayrıntı](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig4.png)

<span data-ttu-id="f5c5d-143">Merhaba'den itibaren bu bölümde açıklandığı gibi bu bilgileri bir olay yanıtlama çalışması sırasında çok kullanışlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f5c5d-143">As described in hello beginning of this section, this information can be very useful during an incident response case.</span></span> <span data-ttu-id="f5c5d-144">Bu aynı zamanda bir adli araştırma sırasında toofind hello kaynak hangi sistem aşılmış ve zaman çizelgesi hello hello saldırı, ihtiyaç duyacağınız önemli olabilir.</span><span class="sxs-lookup"><span data-stu-id="f5c5d-144">It can also be important during a forensic investigation, where you need toofind hello source of hello attack, which system was compromised and hello timeline.</span></span> <span data-ttu-id="f5c5d-145">Bu raporda, kolayca belirleyebilir hello saldırı hakkında bazı önemli ayrıntıları gibi: Merhaba kaynak hello saldırı, aşılmış yerel IP hello ve hello hello bağlantı geçerli oturum durumu.</span><span class="sxs-lookup"><span data-stu-id="f5c5d-145">In this report you can easily identify some key details about hello attack, such as: hello source of hello attack, hello local IP that was compromised and hello current session state of hello connection.</span></span> 

<span data-ttu-id="f5c5d-146">Merhaba **tehdit Intelligence harita** kötü amaçlı trafiği olan tooidentify hello geçerli konumlarına Merhaba Dünya çevresinde yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="f5c5d-146">hello **threat intelligence map** will help you tooidentify hello current locations around hello globe that have malicious traffic.</span></span> <span data-ttu-id="f5c5d-147">Turuncu (gelen) ve bu okları birini tıklatırsanız, hello trafiği yönünü tanımlayan kırmızı (giden) oklar bu haritadaki, aşağıda gösterildiği gibi tehdit ve hello trafiği yönünü hello türünü gösterir:</span><span class="sxs-lookup"><span data-stu-id="f5c5d-147">There are orange (incoming) and red (outgoing) arrows in this map that identify hello traffic direction, if you click in one of these arrows, it will show hello type of threat and hello traffic direction as shown below:</span></span>

![Tehdit bilgisi haritası](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig5.png)

> [!NOTE]
> <span data-ttu-id="f5c5d-149">Toouse bu özellik bir olay yanıtlama sırasında işleminin nasıl hello sunu izleyerek Tanıtımı görebilirsiniz [Operations Management Suite kullanarak destekli araştırma ile Veri Merkezi güvenlik tehditleri azaltmak](https://myignite.microsoft.com/videos/5000) Microsoft Ignite teslim.</span><span class="sxs-lookup"><span data-stu-id="f5c5d-149">You can see a demonstration on how toouse this capability during an incident response process by watching hello presentation [Mitigate datacenter security threats with guided investigation using Operations Management Suite](https://myignite.microsoft.com/videos/5000) delivered at Microsoft Ignite.</span></span>
> 

### <a name="responding-toodistinct-malicious-ip-accessed"></a><span data-ttu-id="f5c5d-150">Erişilen kötü amaçlı IP toodistinct yanıt</span><span class="sxs-lookup"><span data-stu-id="f5c5d-150">Responding toodistinct malicious IP accessed</span></span>
<span data-ttu-id="f5c5d-151">Bazı senaryolarda, izlenen bir bilgisayardan erişilen olası bir kötü amaçlı IP ile karşılaşabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f5c5d-151">In some scenarios, you may notice a potential malicious IP that was accessed from one monitored computer:</span></span>

![Tehdit bilgisi haritası](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

<span data-ttu-id="f5c5d-153">Bu uyarı ve diğerleri içinde Merhaba aynı kategoride, OMS güvenlik yararlanarak oluşturulan [Microsoft tehdit bilgileri](https://youtu.be/O4WtxgUrDc8).</span><span class="sxs-lookup"><span data-stu-id="f5c5d-153">This alert and others within hello same category, are generated via OMS Security by leveraging [Microsoft Threat Intelligence](https://youtu.be/O4WtxgUrDc8).</span></span> <span data-ttu-id="f5c5d-154">Merhaba tehdit bilgileri veri Microsoft tarafından toplanan yanı sıra başında tehdit Intelligence sağlayıcılardan satın.</span><span class="sxs-lookup"><span data-stu-id="f5c5d-154">hello Threat Intelligence data is collected by Microsoft as well as purchased from leading threat intelligence providers.</span></span> <span data-ttu-id="f5c5d-155">Bu veriler, sık sık güncelleştirilir ve toofast taşıma tehditleri uyarlanan.</span><span class="sxs-lookup"><span data-stu-id="f5c5d-155">This data is updated frequently and adapted toofast-moving threats.</span></span> <span data-ttu-id="f5c5d-156">Tooits yapısı, bu güvenlik bilgileri sırasında diğer kaynakları ile birleştirilmelidir [araştırma](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) bir güvenlik uyarısı.</span><span class="sxs-lookup"><span data-stu-id="f5c5d-156">Due tooits nature, it should be combined with other sources of security information while [investigating](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) a security alert.</span></span> 

## <a name="customize-alerts-received-via-e-mail"></a><span data-ttu-id="f5c5d-157">E-posta yoluyla alınan uyarıları özelleştirme</span><span class="sxs-lookup"><span data-stu-id="f5c5d-157">Customize alerts received via e-mail</span></span>

<span data-ttu-id="f5c5d-158">Güvenlik Uyarıları OMS güvenliği tarafından tetiklendiğinde, kuruluşunuzda hangi kullanıcıların bildirilecek özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f5c5d-158">You can customize which users in your organization will be notified when security alerts are triggered by OMS Security.</span></span> <span data-ttu-id="f5c5d-159">Bu seçenek altında genel bakış kullanılabilir / ayarları OMS Pano hello:</span><span class="sxs-lookup"><span data-stu-id="f5c5d-159">This option is available under Overview / Settings at hello OMS dashboard:</span></span>

![E-posta](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig7.png)

## <a name="see-also"></a><span data-ttu-id="f5c5d-161">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="f5c5d-161">See also</span></span>
<span data-ttu-id="f5c5d-162">Bu belgede, nasıl öğrenilen toouse hello **tehdit bilgileri** OMS güvenlik ve denetim çözüm toorespond toosecurity uyarıları seçeneği.</span><span class="sxs-lookup"><span data-stu-id="f5c5d-162">In this document, you learned how toouse hello **Threat Intelligence** option in OMS Security and Audit solution toorespond toosecurity alerts.</span></span> <span data-ttu-id="f5c5d-163">toolearn OMS güvenlik hakkında daha fazla bilgi makaleleri aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="f5c5d-163">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="f5c5d-164">Operations Management Suite'e (OMS) genel bakış</span><span class="sxs-lookup"><span data-stu-id="f5c5d-164">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="f5c5d-165">Operations Management Suite güvenlik ve denetim çözümü ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="f5c5d-165">Getting started with Operations Management Suite Security and Audit Solution</span></span>](oms-security-getting-started.md)
* [<span data-ttu-id="f5c5d-166">Operations Management Suite Güvenlik ve Denetim Çözümünde Kaynakları İzleme</span><span class="sxs-lookup"><span data-stu-id="f5c5d-166">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

