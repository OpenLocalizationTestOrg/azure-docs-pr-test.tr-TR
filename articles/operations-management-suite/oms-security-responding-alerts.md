---
title: "İzleme ve Operations Management Suite güvenlik ve denetim çözümü güvenlik uyarılarını yanıtlama | Microsoft Docs"
description: "Bu belge, güvenlik uyarılarını yanıtlama ve izlemek için OMS güvenlik ve denetim kullanılabilir tehdit Intelligence seçeneği kullanmak için yardımcı olur."
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
ms.openlocfilehash: 0cf9b83d7023641ec445a59a5e61d3da038695fa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-and-responding-to-security-alerts-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="814a9-103">İzleme ve Operations Management Suite güvenlik ve denetim çözüm güvenlik uyarılarını yanıtlama</span><span class="sxs-lookup"><span data-stu-id="814a9-103">Monitoring and responding to security alerts in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="814a9-104">Bu belge, izlemek ve güvenlik uyarılarını yanıtlama OMS güvenlik ve denetim kullanılabilir tehdit Intelligence seçeneği kullanmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="814a9-104">This document helps you use the threat intelligence option available in OMS Security and Audit to monitor and respond to security alerts.</span></span>

## <a name="what-is-oms"></a><span data-ttu-id="814a9-105">OMS nedir?</span><span class="sxs-lookup"><span data-stu-id="814a9-105">What is OMS?</span></span>
<span data-ttu-id="814a9-106">Microsoft Operations Management Suite (OMS) Microsoft'un bulut yönetmek ve şirket içi korumak ve altyapı bulut yardımcı olan BT yönetim çözümü dayalıdır.</span><span class="sxs-lookup"><span data-stu-id="814a9-106">Microsoft Operations Management Suite (OMS) is Microsoft's cloud based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="814a9-107">OMS hakkında daha fazla bilgi için bkz. [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).</span><span class="sxs-lookup"><span data-stu-id="814a9-107">For more information about OMS, read the article [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).</span></span>

## <a name="threat-intelligence"></a><span data-ttu-id="814a9-108">Tehdit bilgileri</span><span class="sxs-lookup"><span data-stu-id="814a9-108">Threat intelligence</span></span>
<span data-ttu-id="814a9-109">Kullanıcıların geniş ağ erişimi ve şirket verilerine bağlanmak için çeşitli aygıtlardan kullanmak bir kuruluş ortamında, etkin olarak kaynaklarınızı izlemek ve hızlı bir şekilde güvenlik olaylarına yanıt zorunludur.</span><span class="sxs-lookup"><span data-stu-id="814a9-109">In an enterprise environment where users have broad access to the network and use a variety of devices to connect to corporate data, it is imperative that you can actively monitor your resources and quickly respond to security incidents.</span></span> <span data-ttu-id="814a9-110">Belirli tehditlere değil yükseltmek bazı siber güvenlik uyarıları çünkü güvenlik yaşam döngüsü açısından önemli ya da teknik geleneksel güvenlik denetimleri tarafından tanımlanan kuşkulu etkinlikleri budur.</span><span class="sxs-lookup"><span data-stu-id="814a9-110">This is particular important from the security lifecycle perspective because some cybersecurity threats may not raise alerts or suspicious activities that can be identified by traditional security technical controls.</span></span> 

<span data-ttu-id="814a9-111">Kullanarak **tehdit bilgileri** seçeneği kullanılabilir OMS güvenlik ve denetim, BT yöneticileri ortam güvenlik tehditlerinden örneğin tanımlamak, belirli bir bilgisayarın parçası olup olmadığını belirleyebilmek bir [ botnet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection).</span><span class="sxs-lookup"><span data-stu-id="814a9-111">By using the **Threat Intelligence** option available in OMS Security and Audit, IT administrators can identify security threats against the environment, for example, identify if a particular computer is part of a [botnet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection).</span></span> <span data-ttu-id="814a9-112">Bilgisayar korsanları yasa dışı yollarla bu bilgisayarı bir komut veya denetime bağlayan kökü amaçlı bir yazılım yüklediklerinde, bilgisayarlar botnette düğümlere dönüşür.</span><span class="sxs-lookup"><span data-stu-id="814a9-112">Computers can become nodes in a botnet when attackers illicitly install malware that secretly connects this computer to the command and control.</span></span> <span data-ttu-id="814a9-113">Yeraltı iletişim kanalları, gelen gibi olası tehditler tanımlayabilirsiniz [darknet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection_honeypots_darkents).</span><span class="sxs-lookup"><span data-stu-id="814a9-113">It can also identify potential threats coming from underground communication channels, such as [darknet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection_honeypots_darkents).</span></span> 

<span data-ttu-id="814a9-114">Bu tehdit bilgileri oluşturmak için Microsoft içindeki birden fazla kaynaktan gelen veri OMS güvenlik ve denetim kullanın.</span><span class="sxs-lookup"><span data-stu-id="814a9-114">In order to build this threat intelligence, OMS Security and Audit use data coming from multiple sources within Microsoft.</span></span> <span data-ttu-id="814a9-115">OMS güvenlik ve Denetim olası tehditlere karşı ortamınızın tanımlamak için bu verileri özelliğinden yararlanır.</span><span class="sxs-lookup"><span data-stu-id="814a9-115">OMS Security and Audit will leverage this data to identify potential threats against your environment.</span></span>

<span data-ttu-id="814a9-116">Tehdit Bilgileri bölmesi üç ana seçenekten oluşur:</span><span class="sxs-lookup"><span data-stu-id="814a9-116">The Threat Intelligence pane is composed by three major options:</span></span>

* <span data-ttu-id="814a9-117">Giden kötü amaçlı trafiğe sahip sunucular</span><span class="sxs-lookup"><span data-stu-id="814a9-117">Servers with outbound malicious traffic</span></span>
* <span data-ttu-id="814a9-118">Algılanan tehditler türleri</span><span class="sxs-lookup"><span data-stu-id="814a9-118">Detected threats types</span></span>
* <span data-ttu-id="814a9-119">Tehdit bilgileri haritası</span><span class="sxs-lookup"><span data-stu-id="814a9-119">Threat intelligence map</span></span>

> [!NOTE]
> <span data-ttu-id="814a9-120">Tüm bu seçenekler genel bakış için okuma [Operations Management Suite güvenlik ve denetim çözümü ile çalışmaya başlama](oms-security-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="814a9-120">for an overview of all these options, read [Getting started with Operations Management Suite Security and Audit Solution](oms-security-getting-started.md).</span></span>
> 
> 

### <a name="responding-to-security-alerts"></a><span data-ttu-id="814a9-121">Güvenlik uyarılara yanıt verme</span><span class="sxs-lookup"><span data-stu-id="814a9-121">Responding to security alerts</span></span>
<span data-ttu-id="814a9-122">Adımlardan biri bir [güvenlik olay yanıtlama](https://technet.microsoft.com/library/cc512623.aspx) işlemdir güvenliğinin aşılmasına sistemleri önemini belirlemek için.</span><span class="sxs-lookup"><span data-stu-id="814a9-122">One of the steps of a [security incident response](https://technet.microsoft.com/library/cc512623.aspx) process is to identify the severity of the compromise system(s).</span></span> <span data-ttu-id="814a9-123">Bu aşamada aşağıdaki görevleri gerçekleştirmeniz:</span><span class="sxs-lookup"><span data-stu-id="814a9-123">In this phase you should perform the following tasks:</span></span>

* <span data-ttu-id="814a9-124">Saldırının yapısını belirleme</span><span class="sxs-lookup"><span data-stu-id="814a9-124">Determine the nature of the attack</span></span>
* <span data-ttu-id="814a9-125">Saldırının kaynak noktasını belirleme</span><span class="sxs-lookup"><span data-stu-id="814a9-125">Determine the attack point of origin</span></span>
* <span data-ttu-id="814a9-126">Saldırının amacını belirleme.</span><span class="sxs-lookup"><span data-stu-id="814a9-126">Determine the intent of the attack.</span></span> <span data-ttu-id="814a9-127">Saldırı kuruluşunuza özellikle belirli bilgileri elde etme amacıyla mı yapıldı yoksa rastgele bir saldırı mıydı?</span><span class="sxs-lookup"><span data-stu-id="814a9-127">Was the attack specifically directed at your organization to acquire specific information, or was it random?</span></span>
* <span data-ttu-id="814a9-128">Gizliliği tehlikeye girmiş sistemleri tanımlayın</span><span class="sxs-lookup"><span data-stu-id="814a9-128">Identify the systems that have been compromised</span></span>
* <span data-ttu-id="814a9-129">Erişilen ve bu dosyaları duyarlılığını belirlemek dosyaları belirle</span><span class="sxs-lookup"><span data-stu-id="814a9-129">Identify the files that have been accessed and determine the sensitivity of those files</span></span>

<span data-ttu-id="814a9-130">Yararlanabileceğiniz **tehdit bilgileri** bu görevleri yardımcı olması için OMS güvenlik ve denetim çözüm bilgileri.</span><span class="sxs-lookup"><span data-stu-id="814a9-130">You can leverage **Threat Intelligence** information in OMS Security and Audit solution to help with these tasks.</span></span> <span data-ttu-id="814a9-131">Erişim sağlamak için aşağıdaki adımları izleyin **tehdit bilgileri** seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="814a9-131">Follow the steps below to access this **Threat Intelligence** options:</span></span>

1. <span data-ttu-id="814a9-132">**Microsoft Operations Management Suite** ana panosunda, **Güvenlik ve Denetim** kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="814a9-132">In the **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
   
    ![Güvenlik ve Denetim](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. <span data-ttu-id="814a9-134">İçinde **güvenlik ve Denetim** panoyu görürsünüz **tehdit bilgileri** aşağıda gösterildiği gibi sağ seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="814a9-134">In the **Security and Audit** dashboard, you will see the **Threat Intelligence** options in the right, as shown below:</span></span>
   
    ![Tehdit Intel](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig2-ga.png)

<span data-ttu-id="814a9-136">Bu üç kutucuklar size geçerli tehditleri genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="814a9-136">These three tiles will give you an overview of the current threats.</span></span> <span data-ttu-id="814a9-137">İçinde **giden kötü amaçlı trafiği sunucusuyla** izlemekte olduğunuz herhangi bir bilgisayarda ise belirlemek mümkün olacaktır (içinde veya ağınızın dışında), kötü amaçlı trafiğin Internet'e gönderiyor.</span><span class="sxs-lookup"><span data-stu-id="814a9-137">In the **Server with outbound malicious traffic** you will be able to identify if there is any computer that you are monitoring (inside or outside of your network) that is sending malicious traffic to the Internet.</span></span> 

<span data-ttu-id="814a9-138">**Algılanan tehdit türlerini** döşeme "içinde joker" geçerli tehditleri özetini gösterir, bu kutucuğa tıkladığınızda bu tehditler hakkında daha fazla ayrıntı Göster aşağıdaki görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="814a9-138">The **Detected threat types** tile shows a summary of the threats that are current “in the wild”, if you click on this tile you will see more details about these threats as show below:</span></span>

![Algılanan tehdit türleri](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig3.png)

<span data-ttu-id="814a9-140">Tıklayarak her tehdit hakkında daha fazla bilgi ayıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="814a9-140">You can extract more information about each threat by clicking on it.</span></span> <span data-ttu-id="814a9-141">Aşağıdaki örnek, Botnet hakkında daha fazla ayrıntı gösterir:</span><span class="sxs-lookup"><span data-stu-id="814a9-141">The example below shows more details about Botnet:</span></span>

![bir tehdit hakkında daha fazla ayrıntı](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig4.png)

<span data-ttu-id="814a9-143">Bu bölüm başına içinde açıklandığı gibi bu bilgileri bir olay yanıtlama çalışması sırasında çok kullanışlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="814a9-143">As described in the beginning of this section, this information can be very useful during an incident response case.</span></span> <span data-ttu-id="814a9-144">Bunu ayrıca bir adli araştırma sırasında nerede kaynağını ve saldırı, hangi sistem aşılmış zaman çizelgesi bulmanız gereken önemli olabilir.</span><span class="sxs-lookup"><span data-stu-id="814a9-144">It can also be important during a forensic investigation, where you need to find the source of the attack, which system was compromised and the timeline.</span></span> <span data-ttu-id="814a9-145">Bu raporda, kolayca belirleyebilir saldırı hakkında bazı önemli ayrıntıları gibi: kaynağı saldırı, aşılmış yerel IP ve bağlantı geçerli oturum durumu.</span><span class="sxs-lookup"><span data-stu-id="814a9-145">In this report you can easily identify some key details about the attack, such as: the source of the attack, the local IP that was compromised and the current session state of the connection.</span></span> 

<span data-ttu-id="814a9-146">**Tehdit Intelligence harita** kötü amaçlı trafiği, mevcut konumları dünya belirlemenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="814a9-146">The **threat intelligence map** will help you to identify the current locations around the globe that have malicious traffic.</span></span> <span data-ttu-id="814a9-147">Turuncu (gelen) ve bu okları birini tıklatırsanız, trafiği yönünü tanımlayan kırmızı (giden) okları bu haritadaki tehdit ve aşağıda gösterildiği gibi trafik yönü türünü gösterir:</span><span class="sxs-lookup"><span data-stu-id="814a9-147">There are orange (incoming) and red (outgoing) arrows in this map that identify the traffic direction, if you click in one of these arrows, it will show the type of threat and the traffic direction as shown below:</span></span>

![Tehdit bilgisi haritası](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig5.png)

> [!NOTE]
> <span data-ttu-id="814a9-149">Sunu izleyerek bir olay yanıtlama işlemi sırasında bu özelliği kullanmak hakkında bir tanıtım bakın [Operations Management Suite kullanarak destekli araştırma ile Veri Merkezi güvenlik tehditleri azaltmak](https://myignite.microsoft.com/videos/5000) Microsoft Ignite teslim.</span><span class="sxs-lookup"><span data-stu-id="814a9-149">You can see a demonstration on how to use this capability during an incident response process by watching the presentation [Mitigate datacenter security threats with guided investigation using Operations Management Suite](https://myignite.microsoft.com/videos/5000) delivered at Microsoft Ignite.</span></span>
> 

### <a name="responding-to-distinct-malicious-ip-accessed"></a><span data-ttu-id="814a9-150">Erişilen ayrı kötü amaçlı IP yanıt</span><span class="sxs-lookup"><span data-stu-id="814a9-150">Responding to distinct malicious IP accessed</span></span>
<span data-ttu-id="814a9-151">Bazı senaryolarda, izlenen bir bilgisayardan erişilen olası bir kötü amaçlı IP ile karşılaşabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="814a9-151">In some scenarios, you may notice a potential malicious IP that was accessed from one monitored computer:</span></span>

![Tehdit bilgisi haritası](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

<span data-ttu-id="814a9-153">Bu uyarı ve aynı kategoride bulunan diğer uyarılar OMS Güvenliği aracılığıyla, [Microsoft Tehdit Bilgileri](https://youtu.be/O4WtxgUrDc8)'nden yararlanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="814a9-153">This alert and others within the same category, are generated via OMS Security by leveraging [Microsoft Threat Intelligence](https://youtu.be/O4WtxgUrDc8).</span></span> <span data-ttu-id="814a9-154">Microsoft tarafından toplananların yanı sıra önde gelen tehdit bilgisi sağlayıcılarından satın alınan Tehdit Bilgisi verileri de bulunur.</span><span class="sxs-lookup"><span data-stu-id="814a9-154">The Threat Intelligence data is collected by Microsoft as well as purchased from leading threat intelligence providers.</span></span> <span data-ttu-id="814a9-155">Bu veriler sıklıkla güncelleştirilir ve hızlı hareket eden tehditlere uyarlanır.</span><span class="sxs-lookup"><span data-stu-id="814a9-155">This data is updated frequently and adapted to fast-moving threats.</span></span> <span data-ttu-id="814a9-156">Doğası gereği bu verilerin, bir güvenlik uyarısını [araştırma](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) sürecinde diğer güvenlik bilgisi kaynaklarıyla birleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="814a9-156">Due to its nature, it should be combined with other sources of security information while [investigating](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) a security alert.</span></span> 

## <a name="customize-alerts-received-via-e-mail"></a><span data-ttu-id="814a9-157">E-posta yoluyla alınan uyarıları özelleştirme</span><span class="sxs-lookup"><span data-stu-id="814a9-157">Customize alerts received via e-mail</span></span>

<span data-ttu-id="814a9-158">Güvenlik Uyarıları OMS güvenliği tarafından tetiklendiğinde, kuruluşunuzda hangi kullanıcıların bildirilecek özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="814a9-158">You can customize which users in your organization will be notified when security alerts are triggered by OMS Security.</span></span> <span data-ttu-id="814a9-159">Bu seçenek altında genel bakış kullanılabilir / OMS Pano ayarları:</span><span class="sxs-lookup"><span data-stu-id="814a9-159">This option is available under Overview / Settings at the OMS dashboard:</span></span>

![E-posta](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig7.png)

## <a name="see-also"></a><span data-ttu-id="814a9-161">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="814a9-161">See also</span></span>
<span data-ttu-id="814a9-162">Bu belgede, kullanılacak öğrendiniz **tehdit bilgileri** güvenlik uyarılarını yanıtlama için OMS güvenlik ve denetim çözümde seçeneği.</span><span class="sxs-lookup"><span data-stu-id="814a9-162">In this document, you learned how to use the **Threat Intelligence** option in OMS Security and Audit solution to respond to security alerts.</span></span> <span data-ttu-id="814a9-163">OMS Güvenlik hakkında daha fazla bilgi edinmek için şu makalelere göz atın:</span><span class="sxs-lookup"><span data-stu-id="814a9-163">To learn more about OMS Security, see the following articles:</span></span>

* [<span data-ttu-id="814a9-164">Operations Management Suite'e (OMS) genel bakış</span><span class="sxs-lookup"><span data-stu-id="814a9-164">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="814a9-165">Operations Management Suite güvenlik ve denetim çözümü ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="814a9-165">Getting started with Operations Management Suite Security and Audit Solution</span></span>](oms-security-getting-started.md)
* [<span data-ttu-id="814a9-166">Operations Management Suite Güvenlik ve Denetim Çözümünde Kaynakları İzleme</span><span class="sxs-lookup"><span data-stu-id="814a9-166">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

