---
title: "Windows bilgisayarları Azure günlük Analizi'ne bağlamak | Microsoft Docs"
description: "Bu makalede, özelleştirilmiş bir sürümünü Microsoft İzleme Aracısı'nı (MMA) kullanarak şirket içi altyapınızda Windows bilgisayarları günlük analizi hizmetine bağlanmak için gereken adımları gösterir."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 932f7b8c-485c-40c1-98e3-7d4c560876d2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 48a0eaeb10d406d551c9e5870edde06809bd7544
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-windows-computers-to-the-log-analytics-service-in-azure"></a><span data-ttu-id="3f5d2-103">Windows bilgisayarları Azure günlük analizi hizmetine bağlanın</span><span class="sxs-lookup"><span data-stu-id="3f5d2-103">Connect Windows computers to the Log Analytics service in Azure</span></span>

<span data-ttu-id="3f5d2-104">Bu makalede Windows bilgisayarları şirket içi altyapınızda OMS çalışma alanları için özelleştirilmiş bir sürümünü Microsoft İzleme Aracısı'nı (MMA) kullanarak bağlanmak için gereken adımları gösterir.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-104">This article shows the steps to connect Windows computers in your on-premises infrastructure to OMS workspaces by using a customized version of the Microsoft Monitoring Agent (MMA).</span></span> <span data-ttu-id="3f5d2-105">Yükleme ve yerleşik sırayla veri göndermek için günlük analizi hizmeti görüntülemek ve bu veriler üzerinde hareket için bunları istediğiniz tüm bilgisayarların için aracıları bağlanmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-105">You need to install and connect agents for all of the computers that you want to onboard in order for them to send data to the Log Analytics service and to view and act on that data.</span></span> <span data-ttu-id="3f5d2-106">Her bir aracı birden çok çalışma alanına bildirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-106">Each agent can report to multiple workspaces.</span></span>

<span data-ttu-id="3f5d2-107">Kurulum, komut satırı kullanılarak aracıları yükleyebilirsiniz veya ile istenen durum yapılandırması (DSC) Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-107">You can install agents using Setup, command line, or with Desired State Configuration (DSC) in Azure Automation.</span></span>  

>[!NOTE]
<span data-ttu-id="3f5d2-108">Azure'da çalışan sanal makineler için yükleme kullanarak basitleştirebilirsiniz [sanal makine uzantısı](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="3f5d2-108">For virtual machines running in Azure, you can simplify installation by using the [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="3f5d2-109">Internet bağlantısı olan bilgisayarlarda aracı için OMS veri göndermek için Internet bağlantısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-109">On computers with Internet connectivity, the agent uses the connection to the Internet to send data to OMS.</span></span> <span data-ttu-id="3f5d2-110">Internet bağlantısına sahip olmayan bilgisayarlar için bir proxy sunucu kullanabilirsiniz veya [OMS ağ geçidi](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="3f5d2-110">For computers that do not have Internet connectivity, you can use a proxy or the [OMS Gateway](log-analytics-oms-gateway.md).</span></span>

<span data-ttu-id="3f5d2-111">Windows bilgisayarları için OMS bağlanma üç basit adımları kullanarak basittir:</span><span class="sxs-lookup"><span data-stu-id="3f5d2-111">Connecting your Windows computers to OMS is straightforward using three simple steps:</span></span>

1. <span data-ttu-id="3f5d2-112">OMS Portalı'ndan aracı kurulum dosyasını indirin</span><span class="sxs-lookup"><span data-stu-id="3f5d2-112">Download the agent setup file from the OMS portal</span></span>
2. <span data-ttu-id="3f5d2-113">Seçtiğiniz yöntemi kullanarak aracı yükleme</span><span class="sxs-lookup"><span data-stu-id="3f5d2-113">Install the agent using the method you choose</span></span>
3. <span data-ttu-id="3f5d2-114">Aracı yapılandırma veya gerekiyorsa, ek çalışma alanları ekleme</span><span class="sxs-lookup"><span data-stu-id="3f5d2-114">Configure the agent or add additional workspaces, if necessary</span></span>

<span data-ttu-id="3f5d2-115">Yüklü ve aracıları yapılandırdıktan sonra aşağıdaki diyagramda, Windows bilgisayarları ve OMS arasındaki ilişkiyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-115">The following diagram shows the relationship between your Windows computers and OMS after you’ve installed and configured agents.</span></span>

![OMS doğrudan Aracısı diyagramı](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

<span data-ttu-id="3f5d2-117">BT güvenlik ilkelerinizi bilgisayarları Internet'e bağlanmak için ağınızdaki izin vermiyorsa, OMS ağ geçidine bağlanmak üzere, bilgisayarlarınız yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-117">If your IT security policies do not allow computers on your network to connect to the Internet, you can configure your computers to connect to the OMS Gateway.</span></span> <span data-ttu-id="3f5d2-118">Daha fazla bilgi ve sunucularınızı OMS hizmetine bir OMS ağ geçidi üzerinden iletişim kurmak için yapılandırma adımları için bkz: [OMS ağ geçidini kullanarak OMS bilgisayarları bağlamak](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="3f5d2-118">For more information and steps on how to configure your servers to communicate through an OMS Gateway to the OMS service, see [Connect computers to OMS using the OMS Gateway](log-analytics-oms-gateway.md).</span></span>

## <a name="system-requirements-and-required-configuration"></a><span data-ttu-id="3f5d2-119">Sistem gereksinimleri ve gerekli yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3f5d2-119">System requirements and required configuration</span></span>
<span data-ttu-id="3f5d2-120">Yükleyip aracıları dağıtmak için önce belirtilen gereksinimleri karşıladığından emin olmak için aşağıdaki ayrıntıları gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-120">Before you install or deploy agents, review the following details to ensure you meet the requirements.</span></span>

- <span data-ttu-id="3f5d2-121">Yalnızca Windows Server 2008 SP 1 veya sonrasını çalıştıran bilgisayarlar veya Windows 7 SP1 OMS MMA yükleyebilirsiniz ya da daha sonra.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-121">You can only install the OMS MMA on computers running Windows Server 2008 SP 1 or later or Windows 7 SP1 or later.</span></span>
- <span data-ttu-id="3f5d2-122">Bir Azure aboneliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-122">You need an Azure subscription.</span></span>  <span data-ttu-id="3f5d2-123">Daha fazla bilgi için bkz: [günlük Analytics ile çalışmaya başlama](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3f5d2-123">For more information, see [Get started with Log Analytics](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="3f5d2-124">Her Windows bilgisayarı HTTPS kullanarak Internet'e veya OMS ağ geçidi bağlanabilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-124">Each Windows computer must be able to connect to the Internet using HTTPS or to the OMS Gateway.</span></span> <span data-ttu-id="3f5d2-125">Bu bağlantıyı doğrudan OMS ağ geçidi veya proxy aracılığıyla olabilir.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-125">This connection can be direct, via a proxy, or through the OMS Gateway.</span></span>
- <span data-ttu-id="3f5d2-126">Tek başına bilgisayarların, sunucuların ve sanal makinelerin OMS MMA yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-126">You can install the OMS MMA on stand-alone computers, servers, and virtual machines.</span></span> <span data-ttu-id="3f5d2-127">İçin OMS Azure barındırılan sanal makinelere bağlanmak istiyorsanız, bkz: [bağlanmak Azure sanal makineleri için günlük analizi](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="3f5d2-127">If you want to connect Azure-hosted virtual machines to OMS, see [Connect Azure virtual machines to Log Analytics](log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="3f5d2-128">Aracı çeşitli kaynaklar için TCP bağlantı noktası 443 kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-128">The agent needs to use TCP port 443 for various resources.</span></span>

### <a name="network"></a><span data-ttu-id="3f5d2-129">Ağ</span><span class="sxs-lookup"><span data-stu-id="3f5d2-129">Network</span></span>

<span data-ttu-id="3f5d2-130">Windows aracılarının bağlanmak ve OMS hizmete kaydolmak etki alanı URL'lerin ve bağlantı noktası numaraları gibi ağ kaynaklarına erişimi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-130">For Windows agents to connect to and register with the OMS service, they must have access to network resources, including the port numbers and domain URLs.</span></span>

- <span data-ttu-id="3f5d2-131">Proxy sunucuları için, aracı ayarlarında uygun proxy sunucusu kaynaklarının yapılandırıldığından emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-131">For proxy servers, you need to ensure that the appropriate proxy server resources are configured in agent settings.</span></span>
- <span data-ttu-id="3f5d2-132">Internet'e erişimi kısıtlamak, güvenlik duvarları için siz veya ağ mühendisleri için OMS erişime izin vermek için güvenlik duvarını yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-132">For firewalls that restrict access to the Internet, you or your networking engineers need to configure your firewall to permit access to OMS.</span></span> <span data-ttu-id="3f5d2-133">Aracı ayarlarında bir işlem yapılması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-133">No action is needed in agent settings.</span></span>

<span data-ttu-id="3f5d2-134">Aşağıdaki tabloda iletişim için gereken kaynaklar gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-134">The following table shows resources needed for communication.</span></span>

>[!NOTE]
><span data-ttu-id="3f5d2-135">Aşağıdaki kaynaklardan bazıları, operasyonel Öngörüler, günlük analizi için önceki bir ad olduğu gerekeceğinden buraya.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-135">Some of the following resources mention Operational Insights, which was a previous name for Log Analytics.</span></span>

| <span data-ttu-id="3f5d2-136">Aracı Kaynağı</span><span class="sxs-lookup"><span data-stu-id="3f5d2-136">Agent Resource</span></span> | <span data-ttu-id="3f5d2-137">Bağlantı Noktaları</span><span class="sxs-lookup"><span data-stu-id="3f5d2-137">Ports</span></span> | <span data-ttu-id="3f5d2-138">HTTPS denetlemesini atlama</span><span class="sxs-lookup"><span data-stu-id="3f5d2-138">Bypass HTTPS inspection</span></span> |
|---|---|---|
| <span data-ttu-id="3f5d2-139">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="3f5d2-139">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="3f5d2-140">443</span><span class="sxs-lookup"><span data-stu-id="3f5d2-140">443</span></span> | <span data-ttu-id="3f5d2-141">Evet</span><span class="sxs-lookup"><span data-stu-id="3f5d2-141">Yes</span></span> |
| <span data-ttu-id="3f5d2-142">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="3f5d2-142">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="3f5d2-143">443</span><span class="sxs-lookup"><span data-stu-id="3f5d2-143">443</span></span> | <span data-ttu-id="3f5d2-144">Evet</span><span class="sxs-lookup"><span data-stu-id="3f5d2-144">Yes</span></span> |
| <span data-ttu-id="3f5d2-145">*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="3f5d2-145">*.blob.core.windows.net</span></span> | <span data-ttu-id="3f5d2-146">443</span><span class="sxs-lookup"><span data-stu-id="3f5d2-146">443</span></span> | <span data-ttu-id="3f5d2-147">Evet</span><span class="sxs-lookup"><span data-stu-id="3f5d2-147">Yes</span></span> |
| <span data-ttu-id="3f5d2-148">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="3f5d2-148">*.azure-automation.net</span></span> | <span data-ttu-id="3f5d2-149">443</span><span class="sxs-lookup"><span data-stu-id="3f5d2-149">443</span></span> | <span data-ttu-id="3f5d2-150">Evet</span><span class="sxs-lookup"><span data-stu-id="3f5d2-150">Yes</span></span> |



## <a name="download-the-agent-setup-file-from-oms"></a><span data-ttu-id="3f5d2-151">OMS Aracısı kurulum dosyasını indirin</span><span class="sxs-lookup"><span data-stu-id="3f5d2-151">Download the agent setup file from OMS</span></span>
1. <span data-ttu-id="3f5d2-152">OMS portalında üzerinde **genel bakış** sayfasında, **ayarları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-152">In the OMS portal, on the **Overview** page, click the **Settings** tile.</span></span>  <span data-ttu-id="3f5d2-153">Tıklatın **bağlı kaynakları** üst sekmesini.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-153">Click the **Connected Sources** tab at the top.</span></span>  
    <span data-ttu-id="3f5d2-154">![Bağlı kaynaklar sekmesi](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span><span class="sxs-lookup"><span data-stu-id="3f5d2-154">![Connected Sources tab](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span></span>
2. <span data-ttu-id="3f5d2-155">Tıklatın **Windows sunucuları** ve ardından **Windows Aracısı indirme** kurulum dosyasını karşıdan yüklemek için bilgisayarınızın işlemci türü için uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-155">Click **Windows Servers** and then click **Download Windows Agent** applicable to your computer processor type to download the setup file.</span></span>
3. <span data-ttu-id="3f5d2-156">Sağ tarafındaki **çalışma alanı kimliği**Kopyala simgesine tıklayın ve kodu Not Defteri'ne yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-156">On the right of **Workspace ID**, click the copy icon and paste the ID into Notepad.</span></span>
4. <span data-ttu-id="3f5d2-157">Sağ tarafındaki **birincil anahtar**Kopyala simgesine ve anahtarı Not Defteri'ne yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-157">On the right of **Primary Key**, click the copy icon and paste the key into Notepad.</span></span>     

## <a name="install-the-agent-using-setup"></a><span data-ttu-id="3f5d2-158">Kurulumu kullanarak aracı yükleme</span><span class="sxs-lookup"><span data-stu-id="3f5d2-158">Install the agent using setup</span></span>
1. <span data-ttu-id="3f5d2-159">Yönetmek istediğiniz bir bilgisayara aracı yüklemek için Kurulumu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-159">Run Setup to install the agent on a computer that you want to manage.</span></span>
2. <span data-ttu-id="3f5d2-160">Hoş Geldiniz sayfasında, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-160">On the Welcome page, click **Next**.</span></span>
3. <span data-ttu-id="3f5d2-161">Lisans koşulları sayfasında, lisans okuyun ve ardından **ediyorum**.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-161">On the License Terms page, read the license and then click **I Agree**.</span></span>
4. <span data-ttu-id="3f5d2-162">Hedef klasör sayfasında, değiştirmek veya varsayılan yükleme klasörünü ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-162">On the Destination Folder page, change or keep the default installation folder and then click **Next**.</span></span>
5. <span data-ttu-id="3f5d2-163">Aracı Kur seçenekleri sayfasında Azure günlük analizi (OMS için), Operations Manager Aracısı bağlanmayı seçebilirsiniz veya aracı daha sonra yapılandırmak istiyorsanız seçimleri boş bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-163">On the Agent Setup Options page, you can choose to connect the agent to Azure Log Analytics (OMS), Operations Manager, or you can leave the choices blank if you want to configure the agent later.</span></span> <span data-ttu-id="3f5d2-164">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-164">Click **Next**.</span></span>   
    - <span data-ttu-id="3f5d2-165">Azure günlük analizi (OMS) bağlanmak seçerseniz, yapıştırma **çalışma alanı kimliği** ve **çalışma alanı anahtarı (birincil anahtar)** önceki yordamda Not Defteri'ne kopyalanan ve ardından **sonraki** .</span><span class="sxs-lookup"><span data-stu-id="3f5d2-165">If you chose to connect to Azure Log Analytics (OMS), paste the **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in the previous procedure and then click **Next**.</span></span>  
        <span data-ttu-id="3f5d2-166">![Çalışma alanı kimliği ve birincil anahtar yapıştırın](./media/log-analytics-windows-agents/connect-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="3f5d2-166">![paste Workspace ID and Primary Key](./media/log-analytics-windows-agents/connect-workspace.png)</span></span>
    - <span data-ttu-id="3f5d2-167">Operations Manager'e Bağla seçerseniz, yazın **yönetim grubu adı**, **Management Server** adı ve **yönetim sunucusu bağlantı noktası**ve ardından **Sonraki**.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-167">If you chose to connect to Operations Manager, type the **Management Group Name**, **Management Server** name, and **Management Server Port**, and then click **Next**.</span></span> <span data-ttu-id="3f5d2-168">Aracı eylem hesabı sayfasında, yerel sistem hesabı veya bir yerel etki alanı hesabı seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-168">On the Agent Action Account page, choose either the Local System account or a local domain account and then click **Next**.</span></span>  
        <span data-ttu-id="3f5d2-169">![Yönetim grubu Yapılandırması](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![aracı eylem hesabı](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span><span class="sxs-lookup"><span data-stu-id="3f5d2-169">![management group configuration](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span></span>

6. <span data-ttu-id="3f5d2-170">Hazır sayfasında Yükle seçimlerinizi gözden geçirin ve ardından **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-170">On the Ready to Install page, review your choices and then click **Install**.</span></span>
7. <span data-ttu-id="3f5d2-171">Yapılandırması başarıyla tamamlandı sayfasında, **son**.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-171">On the Configuration completed successfully page, click **Finish**.</span></span>
8. <span data-ttu-id="3f5d2-172">Tamamlandığında, **Microsoft İzleme Aracısı** görünür **Denetim Masası**.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-172">When complete, the **Microsoft Monitoring Agent** appears in **Control Panel**.</span></span> <span data-ttu-id="3f5d2-173">Vardır, yapılandırmanızı gözden geçirin ve aracı Operational Insights (OMS için) bağlı olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-173">You can review your configuration there and verify that the agent is connected to Operational Insights (OMS).</span></span> <span data-ttu-id="3f5d2-174">Bildiren bir ileti aracısı için OMS bağlıyken görüntüler: **Microsoft Monitoring Agent Microsoft Operations Management Suite hizmetine başarıyla bağlandı.**</span><span class="sxs-lookup"><span data-stu-id="3f5d2-174">When connected to OMS, the agent displays a message stating: **The Microsoft Monitoring Agent has successfully connected to the Microsoft Operations Management Suite service.**</span></span>

## <a name="configure-proxy-settings"></a><span data-ttu-id="3f5d2-175">Proxy ayarlarını yapılandır</span><span class="sxs-lookup"><span data-stu-id="3f5d2-175">Configure proxy settings</span></span>

<span data-ttu-id="3f5d2-176">Denetim Masası'nı kullanarak Microsoft İzleme Aracısı'na ilişkin ara sunucu ayarlarını yapılandırmak için aşağıdaki yordamı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-176">You can use the following procedure to configure proxy settings for the Microsoft Monitoring Agent using Control Panel.</span></span> <span data-ttu-id="3f5d2-177">Her sunucu için bu yordamı kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-177">You need to use this procedure for each server.</span></span> <span data-ttu-id="3f5d2-178">Yapılandırmanız gereken birden çok sunucu olması durumunda, bu işlemi otomatikleştirmek için bir betik kullanmak sizin için daha kolay olabilir.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-178">If you have many servers that you need to configure, you might find it easier to use a script to automate this process.</span></span> <span data-ttu-id="3f5d2-179">Bu durumda, bir sonraki [Microsoft İzleme Aracısı için ara sunucu ayarlarını betik kullanarak yapılandırma](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script) yordamına bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-179">If so, see the next procedure [To configure proxy settings for the Microsoft Monitoring Agent using a script](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span></span>

### <a name="to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-control-panel"></a><span data-ttu-id="3f5d2-180">Denetim Masası'nı kullanarak Microsoft İzleme Aracısı için ara sunucu ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3f5d2-180">To configure proxy settings for the Microsoft Monitoring Agent using Control Panel</span></span>
1. <span data-ttu-id="3f5d2-181">**Denetim Masası**'nı açın.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-181">Open **Control Panel**.</span></span>
2. <span data-ttu-id="3f5d2-182">**Microsoft İzleme Aracısı**'nı açın.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-182">Open **Microsoft Monitoring Agent**.</span></span>
3. <span data-ttu-id="3f5d2-183">**Ara Sunucu Ayarları** sekmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-183">Click the **Proxy Settings** tab.</span></span>  
    <span data-ttu-id="3f5d2-184">![ara sunucu ayarları sekmesi](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span><span class="sxs-lookup"><span data-stu-id="3f5d2-184">![proxy settings tab](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span></span>
4. <span data-ttu-id="3f5d2-185">**Ara sunucu kullan**'ı seçin ve gerekiyorsa gösterilen örneğe benzer şekilde URL ile bağlantı noktasını yazın.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-185">Select **Use a proxy server** and type the URL and port number, if one is needed, similar to the example shown.</span></span> <span data-ttu-id="3f5d2-186">Ara sunucunuz kimlik doğrulaması gerektiriyorsa ara sunucuya erişmek için kullanıcı adını ve parolayı yazın.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-186">If your proxy server requires authentication, type the username and password to access the proxy server.</span></span>


### <a name="verify-agent-connectivity-to-oms"></a><span data-ttu-id="3f5d2-187">OMS Aracısı bağlanabildiğini doğrulayın</span><span class="sxs-lookup"><span data-stu-id="3f5d2-187">Verify agent connectivity to OMS</span></span>

<span data-ttu-id="3f5d2-188">Kolayca aracılarınızı aşağıdaki yordamı kullanarak OMS ile iletişim kuran olup olmadığını doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="3f5d2-188">You can easily verify whether your agents are communicating with OMS using the following procedure:</span></span>

1.  <span data-ttu-id="3f5d2-189">Windows aracısı içeren bir bilgisayarda, Denetim Masası açın.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-189">On the computer with the Windows agent, open Control Panel.</span></span>
2.  <span data-ttu-id="3f5d2-190">Microsoft Monitoring Agent'ı açın.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-190">Open Microsoft Monitoring Agent.</span></span>
3.  <span data-ttu-id="3f5d2-191">Azure günlük analizi (OMS) sekmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-191">Click the Azure Log Analytics (OMS) tab.</span></span>
4.  <span data-ttu-id="3f5d2-192">Durum sütununda aracı Operations Management Suite hizmetine başarıyla bağlandı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-192">In the Status column, you should see that the agent connected successfully to the Operations Management Suite service.</span></span>

![bağlı aracı](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script"></a><span data-ttu-id="3f5d2-194">Betik kullanarak Microsoft İzleme Aracısı için ara sunucu ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3f5d2-194">To configure proxy settings for the Microsoft Monitoring Agent using a script</span></span>
<span data-ttu-id="3f5d2-195">Aşağıdaki örneği kopyalayın, ortamınıza özgü bilgilerle güncelleştirin, bir PS1 dosya adı uzantısıyla kaydedin ve ardından betiği doğrudan OMS hizmetine bağlanan her bilgisayardan çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-195">Copy the following sample, update it with information specific to your environment, save it with a PS1 file name extension, and then run the script on each computer that connects directly to the OMS service.</span></span>

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get the Health Service configuration object.  We need to determine if we
    #have the right update rollup with the API we need.  If not, no need to run the rest of the script.
    $healthServiceSettings = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'

    $proxyMethod = $healthServiceSettings | Get-Member -Name 'SetProxyInfo'

    if (!$proxyMethod)
    {
         Write-Output 'Health Service proxy API not present, will not update settings.'
         return
    }

    Write-Output "Clearing proxy settings."
    $healthServiceSettings.SetProxyInfo('', '', '')

    $ProxyUserName = $cred.username

    Write-Output "Setting proxy to $ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-the-agent-using-the-command-line"></a><span data-ttu-id="3f5d2-196">Komut satırını kullanarak aracı yükleme</span><span class="sxs-lookup"><span data-stu-id="3f5d2-196">Install the agent using the command line</span></span>
- <span data-ttu-id="3f5d2-197">Değiştirin ve ardından komut satırını kullanarak aracı yüklemek için aşağıdaki örneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-197">Modify and then use the following example to install the agent using the command line.</span></span> <span data-ttu-id="3f5d2-198">Örneğin, tam olarak sessiz yükleme gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-198">The example performs a fully silent installation.</span></span>

    >[!NOTE]
    <span data-ttu-id="3f5d2-199">Bir aracıyı yükseltmek istiyorsanız, betik API'si günlük analizi kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-199">If you want to upgrade an agent, you need to use the Log Analytics scripting API.</span></span> <span data-ttu-id="3f5d2-200">Bir aracıyı yükseltmek için sonraki bölüme bakın.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-200">See the next section to upgrade an agent.</span></span>

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

<span data-ttu-id="3f5d2-201">Aracının IExpress kullanarak kendi ayıklayıcısı kullandığı `/c` komutu.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-201">The agent uses IExpress as its self-extractor using the `/c` command.</span></span> <span data-ttu-id="3f5d2-202">Komut satırı anahtarları adresindeki görebilirsiniz [IExpress komut satırı anahtarları](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) ve örnek gereksinimlerinize uyacak şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-202">You can see the command-line switches at [Command-line switches for IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) and then update the example to suit your needs.</span></span>

|<span data-ttu-id="3f5d2-203">MMA özgü seçenekleri</span><span class="sxs-lookup"><span data-stu-id="3f5d2-203">MMA-specific options</span></span>                   |<span data-ttu-id="3f5d2-204">Notlar</span><span class="sxs-lookup"><span data-stu-id="3f5d2-204">Notes</span></span>         |
|---------------------------------------|--------------|
|<span data-ttu-id="3f5d2-205">ADD_OPINSIGHTS_WORKSPACE</span><span class="sxs-lookup"><span data-stu-id="3f5d2-205">ADD_OPINSIGHTS_WORKSPACE</span></span>               | <span data-ttu-id="3f5d2-206">1 = çalışma alanına bildirmeye Aracısı Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3f5d2-206">1 = Configure the agent to report to a workspace</span></span>                |
|<span data-ttu-id="3f5d2-207">OPINSIGHTS_WORKSPACE_ID</span><span class="sxs-lookup"><span data-stu-id="3f5d2-207">OPINSIGHTS_WORKSPACE_ID</span></span>                | <span data-ttu-id="3f5d2-208">Eklemek için çalışma alanı kimliği (GUID) çalışma alanı için</span><span class="sxs-lookup"><span data-stu-id="3f5d2-208">Workspace Id (guid) for the workspace to add</span></span>                    |
|<span data-ttu-id="3f5d2-209">OPINSIGHTS_WORKSPACE_KEY</span><span class="sxs-lookup"><span data-stu-id="3f5d2-209">OPINSIGHTS_WORKSPACE_KEY</span></span>               | <span data-ttu-id="3f5d2-210">Başlangıçta çalışma alanıyla kimliğini doğrulamak için kullanılan çalışma alanı anahtarı</span><span class="sxs-lookup"><span data-stu-id="3f5d2-210">Workspace key used to initially authenticate with the workspace</span></span> |
|<span data-ttu-id="3f5d2-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span><span class="sxs-lookup"><span data-stu-id="3f5d2-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span></span>  | <span data-ttu-id="3f5d2-212">Çalışma alanı bulunduğu bulut ortamını belirtin</span><span class="sxs-lookup"><span data-stu-id="3f5d2-212">Specify the cloud environment where the workspace is located</span></span> <br> <span data-ttu-id="3f5d2-213">0 = azure ticari bulut (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="3f5d2-213">0 = Azure commercial cloud (default)</span></span> <br> <span data-ttu-id="3f5d2-214">1 azure kamu =</span><span class="sxs-lookup"><span data-stu-id="3f5d2-214">1 = Azure Government</span></span> |
|<span data-ttu-id="3f5d2-215">OPINSIGHTS_PROXY_URL</span><span class="sxs-lookup"><span data-stu-id="3f5d2-215">OPINSIGHTS_PROXY_URL</span></span>               | <span data-ttu-id="3f5d2-216">Kullanılacak proxy için URI</span><span class="sxs-lookup"><span data-stu-id="3f5d2-216">URI for the proxy to use</span></span> |
|<span data-ttu-id="3f5d2-217">OPINSIGHTS_PROXY_USERNAME</span><span class="sxs-lookup"><span data-stu-id="3f5d2-217">OPINSIGHTS_PROXY_USERNAME</span></span>               | <span data-ttu-id="3f5d2-218">Kimliği doğrulanmış bir proxy sunucusuna erişmek için kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="3f5d2-218">Username to access an authenticated proxy</span></span> |
|<span data-ttu-id="3f5d2-219">OPINSIGHTS_PROXY_PASSWORD</span><span class="sxs-lookup"><span data-stu-id="3f5d2-219">OPINSIGHTS_PROXY_PASSWORD</span></span>               | <span data-ttu-id="3f5d2-220">Kimliği doğrulanmış bir proxy sunucusuna erişmek için parola</span><span class="sxs-lookup"><span data-stu-id="3f5d2-220">Password to access an authenticated proxy</span></span> |

>[!NOTE]
<span data-ttu-id="3f5d2-221">IExpress komut satırı uzunluğunu basarsa önlemek için yapılandırılmış hiçbir çalışma ile aracıyı yükleyin ve çalışma alanı için yapılandırmayı ayarlamak için bir komut dosyası kullanın.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-221">To avoid hitting the command-line length limit of IExpress, install the agent with no workspace configured and then use a script to set configuration for the workspace.</span></span>

>[!NOTE]
<span data-ttu-id="3f5d2-222">Alırsanız bir `Command line option syntax error.` kullanırken `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parametresi, aşağıdaki geçici çözüm kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3f5d2-222">If you get a `Command line option syntax error.` when using the `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parameter, you can use the following workaround:</span></span>
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a><span data-ttu-id="3f5d2-223">Bir komut dosyası kullanarak bir çalışma alanı Ekle</span><span class="sxs-lookup"><span data-stu-id="3f5d2-223">Add a workspace using a script</span></span>
<span data-ttu-id="3f5d2-224">Aşağıdaki örnek ile günlük analizi aracı komut dosyası API kullanarak bir çalışma alanı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3f5d2-224">Add a workspace using the Log Analytics agent scripting API with the following example:</span></span>

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

<span data-ttu-id="3f5d2-225">Bir çalışma alanı Azure ABD devlet kurumları için eklemek için aşağıdaki komut dosyası örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="3f5d2-225">To add a workspace in Azure for US Government, use the following script sample:</span></span>
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
<span data-ttu-id="3f5d2-226">Komut satırı veya komut dosyasını önceden yüklemek veya aracısını yapılandırmak için kullandığınız varsa `EnableAzureOperationalInsights` tarafından değiştirildi `AddCloudWorkspace`.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-226">If you've used the command line or script previously to install or configure the agent, `EnableAzureOperationalInsights` was replaced by `AddCloudWorkspace`.</span></span>

## <a name="install-the-agent-using-dsc-in-azure-automation"></a><span data-ttu-id="3f5d2-227">Azure Otomasyonu'nda DSC kullanarak aracı yükleme</span><span class="sxs-lookup"><span data-stu-id="3f5d2-227">Install the agent using DSC in Azure Automation</span></span>

<span data-ttu-id="3f5d2-228">Azure Otomasyonu'nda DSC kullanarak aracıyı yüklemek için aşağıdaki komut dosyası örneği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-228">You can use the following script example to install the agent using DSC in Azure Automation.</span></span> <span data-ttu-id="3f5d2-229">Örnek tarafından tanımlanan 64-bit aracı yükler `URI` değeri.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-229">The example installs the 64-bit agent, identified by the `URI` value.</span></span> <span data-ttu-id="3f5d2-230">URI değerini değiştirerek 32-bit sürümünü de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-230">You can also use the 32-bit version by replacing the URI value.</span></span> <span data-ttu-id="3f5d2-231">URI'ler için her iki sürümü vardır:</span><span class="sxs-lookup"><span data-stu-id="3f5d2-231">The URIs for both versions are:</span></span>

- <span data-ttu-id="3f5d2-232">Windows 64-bit Aracısı - https://go.microsoft.com/fwlink/?LinkId=828603</span><span class="sxs-lookup"><span data-stu-id="3f5d2-232">Windows 64-bit agent - https://go.microsoft.com/fwlink/?LinkId=828603</span></span>
- <span data-ttu-id="3f5d2-233">Windows 32-bit Aracısı - https://go.microsoft.com/fwlink/?LinkId=828604</span><span class="sxs-lookup"><span data-stu-id="3f5d2-233">Windows 32-bit agent - https://go.microsoft.com/fwlink/?LinkId=828604</span></span>


>[!NOTE]
<span data-ttu-id="3f5d2-234">Bu yordam ve komut dosyası örneği var olan bir aracıyı yükseltmez.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-234">This procedure and script example will not upgrade an existing agent.</span></span>

1. <span data-ttu-id="3f5d2-235">İçeri aktarma xPSDesiredStateConfiguration DSC modülünden [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) Azure Otomasyonu içine.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-235">Import the xPSDesiredStateConfiguration DSC Module from [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) into Azure Automation.</span></span>  
2.  <span data-ttu-id="3f5d2-236">İçin Azure Otomasyonu değişken varlıkları oluşturma *OPSINSIGHTS_WS_ID* ve *OPSINSIGHTS_WS_KEY*.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-236">Create Azure Automation variable assets for *OPSINSIGHTS_WS_ID* and *OPSINSIGHTS_WS_KEY*.</span></span> <span data-ttu-id="3f5d2-237">Ayarlama *OPSINSIGHTS_WS_ID* OMS günlük analizi çalışma alanı kimliği ve kümesi *OPSINSIGHTS_WS_KEY* çalışma alanınızın birincil anahtarı.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-237">Set *OPSINSIGHTS_WS_ID* to your OMS Log Analytics workspace ID and set *OPSINSIGHTS_WS_KEY* to the primary key of your workspace.</span></span>
3.  <span data-ttu-id="3f5d2-238">Aşağıdaki komut dosyasını kullanın ve MMAgent.ps1 Kaydet</span><span class="sxs-lookup"><span data-stu-id="3f5d2-238">Use the following script and save it as MMAgent.ps1</span></span>
4.  <span data-ttu-id="3f5d2-239">Değiştirin ve ardından Azure Otomasyonu'nda DSC kullanarak aracıyı yüklemek için aşağıdaki örneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-239">Modify and then use the following example to install the agent using DSC in Azure Automation.</span></span> <span data-ttu-id="3f5d2-240">MMAgent.ps1 Azure Otomasyon arabirimi veya cmdlet'ini kullanarak Azure Automation'a aktarabilir.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-240">Import MMAgent.ps1 into Azure Automation by using the Azure Automation interface or cmdlet.</span></span>
5.  <span data-ttu-id="3f5d2-241">Bir düğüm yapılandırması atayın.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-241">Assign a node to the configuration.</span></span> <span data-ttu-id="3f5d2-242">15 dakika içinde düğüm yapılandırmasını denetler ve MMA düğüme gönderilir.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-242">Within 15 minutes, the node checks its configuration and the MMA is pushed to the node.</span></span>

```PowerShell
Configuration MMAgent
{
    $OIPackageLocalPath = "C:\MMASetup-AMD64.exe"
    $OPSINSIGHTS_WS_ID = Get-AutomationVariable -Name "OPSINSIGHTS_WS_ID"
    $OPSINSIGHTS_WS_KEY = Get-AutomationVariable -Name "OPSINSIGHTS_WS_KEY"


    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    Node OMSnode {
        Service OIService
        {
            Name = "HealthService"
            State = "Running"
            DependsOn = "[Package]OI"
        }

        xRemoteFile OIPackage {
            Uri = "https://go.microsoft.com/fwlink/?LinkId=828603"
            DestinationPath = $OIPackageLocalPath
        }

        Package OI {
            Ensure = "Present"
            Path  = $OIPackageLocalPath
            Name = "Microsoft Monitoring Agent"
            ProductId = "8A7F2C51-4C7D-4BFD-9014-91D11F24AAE2"
            Arguments = '/C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=' + $OPSINSIGHTS_WS_ID + ' OPINSIGHTS_WORKSPACE_KEY=' + $OPSINSIGHTS_WS_KEY + ' AcceptEndUserLicenseAgreement=1"'
            DependsOn = "[xRemoteFile]OIPackage"
        }
    }
}


```

### <a name="get-the-latest-productid-value"></a><span data-ttu-id="3f5d2-243">En son ProductID değeri Al</span><span class="sxs-lookup"><span data-stu-id="3f5d2-243">Get the latest ProductId value</span></span>

<span data-ttu-id="3f5d2-244">`ProductId value` MMAgent.ps1 komut dosyası her aracı sürümü için benzersizdir.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-244">The `ProductId value` in the MMAgent.ps1 script is unique to each agent version.</span></span> <span data-ttu-id="3f5d2-245">Her bir aracının güncelleştirilmiş bir sürümü yayımlandığında, ProductID değerini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-245">When an updated version of each agent is published, the ProductId value changes.</span></span> <span data-ttu-id="3f5d2-246">Bu nedenle, ProductID gelecekte değiştiğinde, basit bir komut dosyası kullanarak aracı sürümü bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-246">So, when the ProductId changes in the future, you can find the agent version using a simple script.</span></span> <span data-ttu-id="3f5d2-247">Bir test sunucusunda yüklü Aracısı'nın en son sürümünü çalıştırdıktan sonra yüklü ProductID değeri almak için aşağıdaki komut dosyasını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-247">After you have the latest agent version installed on a test server, you can use the following script to get the installed ProductId value.</span></span> <span data-ttu-id="3f5d2-248">En son ProductID değerini kullanarak, MMAgent.ps1 komut dosyasındaki değeri güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-248">Using the latest ProductId value, you can update the value in the MMAgent.ps1 script.</span></span>

```PowerShell
$InstalledApplications  = Get-ChildItem hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall


foreach ($Application in $InstalledApplications)

{

     $Key = Get-ItemProperty $Application.PSPath

     if ($Key.DisplayName -eq "Microsoft Monitoring Agent")

     {

        $Key.DisplayName

        Write-Output ("Product ID is: " + $Key.PSChildName.Substring(1,$Key.PSChildName.Length -2))

     }

}  
```

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a><span data-ttu-id="3f5d2-249">Bir aracı el ile yapılandırma veya ek çalışma alanları ekleme</span><span class="sxs-lookup"><span data-stu-id="3f5d2-249">Configure an agent manually or add additional workspaces</span></span>
<span data-ttu-id="3f5d2-250">Aracıları yüklediyseniz bunları yapılandırmadı ancak veya birden çok çalışma alanına bildirmeye Aracısı istiyorsanız, bir aracı etkinleştirmek veya onu yeniden yapılandırmak için aşağıdaki bilgileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-250">If you've installed agents but did not configure them or if you want the agent to report to multiple workspaces, you can use the following information to enable an agent or reconfigure it.</span></span> <span data-ttu-id="3f5d2-251">Aracısı'nı yapılandırdıktan sonra Aracı hizmeti ile kaydeder ve gerekli yapılandırma bilgilerini ve çözüm bilgileri içeren yönetim paketleri alır.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-251">After you've configured the agent, it will register with the agent service and will get necessary configuration information and management packs that contain solution information.</span></span>

1. <span data-ttu-id="3f5d2-252">Microsoft İzleme Aracısı yükledikten sonra açmak **Denetim Masası**.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-252">After you've installed the Microsoft Monitoring Agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="3f5d2-253">Açık **Microsoft İzleme Aracısı** ve ardından **Azure günlük analizi (OMS)** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-253">Open **Microsoft Monitoring Agent** and then click the **Azure Log Analytics (OMS)** tab.</span></span>   
3. <span data-ttu-id="3f5d2-254">Tıklatın **Ekle** açmak için **günlük analizi çalışma alanı Ekle** kutusu.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-254">Click **Add** to open the **Add a Log Analytics Workspace** box.</span></span>
4. <span data-ttu-id="3f5d2-255">Yapıştır **çalışma alanı kimliği** ve **çalışma alanı anahtarı (birincil anahtar)** ekleyin ve ardından istediğiniz çalışma alanı için bir önceki yordamda Not Defteri'ne kopyaladığınız **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-255">Paste the **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in a previous procedure for the workspace that you want to add and then click **OK**.</span></span>  
    <span data-ttu-id="3f5d2-256">![Operasyonel Öngörüler yapılandırın](./media/log-analytics-windows-agents/add-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="3f5d2-256">![configure Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span></span>

<span data-ttu-id="3f5d2-257">Aracı tarafından izlenen bilgisayarlardan veriler toplandıktan sonra OMS tarafından izlenen bilgisayarların sayısını OMS portalında görünür **bağlı kaynakları** sekmesinde **ayarları** olarak **sunucuları Bağlı**.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-257">After data is collected from computers monitored by the agent, the number of computers monitored by OMS will appear in the OMS portal on the **Connected Sources** tab in **Settings** as **Servers Connected**.</span></span>


## <a name="to-disable-an-agent"></a><span data-ttu-id="3f5d2-258">Bir aracı devre dışı bırakmak için</span><span class="sxs-lookup"><span data-stu-id="3f5d2-258">To disable an agent</span></span>
1. <span data-ttu-id="3f5d2-259">Aracıyı yükledikten sonra açmak **Denetim Masası**.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-259">After installing the agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="3f5d2-260">Microsoft Monitoring Agent'ı açın ve ardından **Azure günlük analizi (OMS)** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-260">Open Microsoft Monitoring Agent and then click the **Azure Log Analytics (OMS)** tab.</span></span>
3. <span data-ttu-id="3f5d2-261">Bir çalışma alanını seçin ve ardından **kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-261">Select a workspace and then click **Remove**.</span></span> <span data-ttu-id="3f5d2-262">Bu adım için diğer çalışma alanları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-262">Repeat this step for all other workspaces.</span></span>


## <a name="optionally-configure-agents-to-report-to-an-operations-manager-management-group"></a><span data-ttu-id="3f5d2-263">İsteğe bağlı olarak, bir Operations Manager yönetim grubu için rapor aracıları yapılandırın</span><span class="sxs-lookup"><span data-stu-id="3f5d2-263">Optionally, configure agents to report to an Operations Manager management group</span></span>

<span data-ttu-id="3f5d2-264">BT altyapınızın Operations Manager'ı kullanırsanız, MMA aracı Operations Manager aracısı olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-264">If you use Operations Manager in your IT infrastructure, you can also use the MMA agent as an Operations Manager agent.</span></span>

### <a name="to-configure-mma-agents-to-report-to-an-operations-manager-management-group"></a><span data-ttu-id="3f5d2-265">Bir Operations Manager yönetim grubu için rapor için MMA aracıları yapılandırmak için</span><span class="sxs-lookup"><span data-stu-id="3f5d2-265">To configure MMA agents to report to an Operations Manager management group</span></span>
1.  <span data-ttu-id="3f5d2-266">Aracının yüklü olduğu bilgisayarda açın **Denetim Masası**.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-266">On the computer where the agent is installed, open **Control Panel**.</span></span>  
2.  <span data-ttu-id="3f5d2-267">Açık **Microsoft İzleme Aracısı** ve ardından **Operations Manager** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-267">Open **Microsoft Monitoring Agent** and then click the **Operations Manager** tab.</span></span>  
    <span data-ttu-id="3f5d2-268">![Microsoft İzleme Aracısı Operations Manager sekmesi](./media/log-analytics-windows-agents/om-mg01.png)</span><span class="sxs-lookup"><span data-stu-id="3f5d2-268">![Microsoft Monitoring Agent Operations Manager tab](./media/log-analytics-windows-agents/om-mg01.png)</span></span>
3.  <span data-ttu-id="3f5d2-269">Operations Manager sunucularınızın Active Directory ile tümleştirme varsa, tıklatın **yönetim grubu atamalarını AD DS'den otomatik olarak güncelleştir**.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-269">If your Operations Manager servers have integration with Active Directory, click **Automatically update management group assignments from AD DS**.</span></span>
4.  <span data-ttu-id="3f5d2-270">Tıklatın **Ekle** açmak için **bir yönetim grubu Ekle** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-270">Click **Add** to open the **Add a Management Group** dialog box.</span></span>  
    <span data-ttu-id="3f5d2-271">![Microsoft İzleme Aracısı Yönetim Grubu Ekle](./media/log-analytics-windows-agents/oms-mma-om02.png)</span><span class="sxs-lookup"><span data-stu-id="3f5d2-271">![Microsoft Monitoring Agent Add a Management Group](./media/log-analytics-windows-agents/oms-mma-om02.png)</span></span>
5.  <span data-ttu-id="3f5d2-272">İçinde **yönetim grubu adı** kutusuna, yönetim grubunuzun adını yazın.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-272">In **Management group name** box, type the name of your management group.</span></span>
6.  <span data-ttu-id="3f5d2-273">İçinde **birincil yönetim sunucusu** birincil yönetim sunucusunun bilgisayar adını yazın.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-273">In the **Primary management server** box, type the computer name of the primary management server.</span></span>
7.  <span data-ttu-id="3f5d2-274">İçinde **yönetim sunucusu bağlantı noktası** TCP bağlantı noktası numarasını yazın.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-274">In the **Management server port** box, type the TCP port number.</span></span>
8.  <span data-ttu-id="3f5d2-275">Altında **aracı eylem hesabı**, yerel sistem hesabı veya bir yerel etki alanı hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-275">Under **Agent Action Account**, choose either the Local System account or a local domain account.</span></span>
9.  <span data-ttu-id="3f5d2-276">Tıklatın **Tamam** kapatmak için **bir yönetim grubu Ekle** iletişim kutusunu ve ardından **Tamam** kapatmak için **Microsoft Monitoring Agent özellikleri** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="3f5d2-276">Click **OK** to close the **Add a Management Group** dialog box and then click **OK** to close the **Microsoft Monitoring Agent Properties** dialog box.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3f5d2-277">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3f5d2-277">Next steps</span></span>

- <span data-ttu-id="3f5d2-278">İşlev eklemek ve veri toplamak için bkz. [Çözüm Galerisinden Log Analytics çözümleri ekleme](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="3f5d2-278">[Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md) to add functionality and gather data.</span></span>
