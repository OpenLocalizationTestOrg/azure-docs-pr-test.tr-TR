---
title: "aaaConnect Windows bilgisayarları tooAzure günlük analizi | Microsoft Docs"
description: "Bu makalede, hello Microsoft İzleme Aracısı'nı (MMA) özelleştirilmiş bir sürümünü kullanarak, şirket içi altyapı toohello günlük analizi hizmeti hello adımları tooconnect hello Windows bilgisayarları gösterir."
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
ms.openlocfilehash: 7e15f9eeb0440bd2f6557d7215df701526e4f9aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-computers-toohello-log-analytics-service-in-azure"></a><span data-ttu-id="0c24e-103">Windows bilgisayarları toohello günlük analizi hizmeti Azure connect</span><span class="sxs-lookup"><span data-stu-id="0c24e-103">Connect Windows computers toohello Log Analytics service in Azure</span></span>

<span data-ttu-id="0c24e-104">Bu makalede hello adımları tooconnect Windows bilgisayarları şirket içi altyapı tooOMS alanlarınızı hello Microsoft İzleme Aracısı'nı (MMA) özelleştirilmiş bir sürümünü kullanarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="0c24e-104">This article shows hello steps tooconnect Windows computers in your on-premises infrastructure tooOMS workspaces by using a customized version of hello Microsoft Monitoring Agent (MMA).</span></span> <span data-ttu-id="0c24e-105">Tüm bunları sırayla tooonboard toosend veri toohello günlük analizi hizmeti ve tooview ve bu verileri act istediğiniz hello bilgisayarları için aracıları bağlanmak ve tooinstall gerekir.</span><span class="sxs-lookup"><span data-stu-id="0c24e-105">You need tooinstall and connect agents for all of hello computers that you want tooonboard in order for them toosend data toohello Log Analytics service and tooview and act on that data.</span></span> <span data-ttu-id="0c24e-106">Her bir aracının toomultiple çalışma alanları bildirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c24e-106">Each agent can report toomultiple workspaces.</span></span>

<span data-ttu-id="0c24e-107">Kurulum, komut satırı kullanılarak aracıları yükleyebilirsiniz veya ile istenen durum yapılandırması (DSC) Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="0c24e-107">You can install agents using Setup, command line, or with Desired State Configuration (DSC) in Azure Automation.</span></span>  

>[!NOTE]
<span data-ttu-id="0c24e-108">Azure'da çalışan sanal makineler için yükleme hello kullanarak basitleştirebilirsiniz [sanal makine uzantısı](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="0c24e-108">For virtual machines running in Azure, you can simplify installation by using hello [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="0c24e-109">Internet bağlantısı olan bilgisayarlarda hello Aracısı hello bağlantı toohello Internet toosend veri tooOMS kullanır.</span><span class="sxs-lookup"><span data-stu-id="0c24e-109">On computers with Internet connectivity, hello agent uses hello connection toohello Internet toosend data tooOMS.</span></span> <span data-ttu-id="0c24e-110">Internet bağlantısına sahip olmayan bilgisayarlar için bir proxy veya hello kullanabilirsiniz [OMS ağ geçidi](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="0c24e-110">For computers that do not have Internet connectivity, you can use a proxy or hello [OMS Gateway](log-analytics-oms-gateway.md).</span></span>

<span data-ttu-id="0c24e-111">Windows bilgisayarları tooOMS bağlanma üç basit adımları kullanarak basittir:</span><span class="sxs-lookup"><span data-stu-id="0c24e-111">Connecting your Windows computers tooOMS is straightforward using three simple steps:</span></span>

1. <span data-ttu-id="0c24e-112">Merhaba OMS Portalı'ndan Hello Aracısı kurulum dosyasını indirin</span><span class="sxs-lookup"><span data-stu-id="0c24e-112">Download hello agent setup file from hello OMS portal</span></span>
2. <span data-ttu-id="0c24e-113">Seçtiğiniz hello yöntemi kullanarak hello aracı yükleme</span><span class="sxs-lookup"><span data-stu-id="0c24e-113">Install hello agent using hello method you choose</span></span>
3. <span data-ttu-id="0c24e-114">Gerekirse ek çalışma alanları ekleyin veya Hello Aracısı Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0c24e-114">Configure hello agent or add additional workspaces, if necessary</span></span>

<span data-ttu-id="0c24e-115">yüklü ve aracıları yapılandırdıktan sonra hello Aşağıdaki diyagramda hello arasındaki ilişkiyi Windows bilgisayarları ve OMS gösterir.</span><span class="sxs-lookup"><span data-stu-id="0c24e-115">hello following diagram shows hello relationship between your Windows computers and OMS after you’ve installed and configured agents.</span></span>

![OMS doğrudan Aracısı diyagramı](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

<span data-ttu-id="0c24e-117">BT güvenlik ilkeleri, ağ tooconnect toohello Internet bilgisayarları izin vermiyorsa, bilgisayarları tooconnect toohello OMS ağ geçidi yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c24e-117">If your IT security policies do not allow computers on your network tooconnect toohello Internet, you can configure your computers tooconnect toohello OMS Gateway.</span></span> <span data-ttu-id="0c24e-118">Daha fazla bilgi ve tooconfigure, sunucuları toocommunicate bir OMS ağ geçidi toohello OMS hizmeti aracılığıyla nasıl görürüm adımlar [hello OMS ağ geçidi kullanarak bilgisayarları tooOMS bağlanmak](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="0c24e-118">For more information and steps on how tooconfigure your servers toocommunicate through an OMS Gateway toohello OMS service, see [Connect computers tooOMS using hello OMS Gateway](log-analytics-oms-gateway.md).</span></span>

## <a name="system-requirements-and-required-configuration"></a><span data-ttu-id="0c24e-119">Sistem gereksinimleri ve gerekli yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0c24e-119">System requirements and required configuration</span></span>
<span data-ttu-id="0c24e-120">Yükleyip aracıları dağıtmak için önce hello gereksinimleri karşılaması ayrıntıları tooensure aşağıdaki hello gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="0c24e-120">Before you install or deploy agents, review hello following details tooensure you meet hello requirements.</span></span>

- <span data-ttu-id="0c24e-121">Yalnızca Windows Server 2008 SP 1 veya sonrasını çalıştıran bilgisayarlar veya Windows 7 SP1 hello OMS MMA yükleyebilirsiniz ya da daha sonra.</span><span class="sxs-lookup"><span data-stu-id="0c24e-121">You can only install hello OMS MMA on computers running Windows Server 2008 SP 1 or later or Windows 7 SP1 or later.</span></span>
- <span data-ttu-id="0c24e-122">Bir Azure aboneliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="0c24e-122">You need an Azure subscription.</span></span>  <span data-ttu-id="0c24e-123">Daha fazla bilgi için bkz: [günlük Analytics ile çalışmaya başlama](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0c24e-123">For more information, see [Get started with Log Analytics](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="0c24e-124">Her Windows bilgisayarı mümkün tooconnect toohello Internet olmalıdır HTTPS veya toohello OMS ağ geçidi kullanarak.</span><span class="sxs-lookup"><span data-stu-id="0c24e-124">Each Windows computer must be able tooconnect toohello Internet using HTTPS or toohello OMS Gateway.</span></span> <span data-ttu-id="0c24e-125">Bu bağlantıyı doğrudan hello OMS ağ geçidi veya proxy aracılığıyla olabilir.</span><span class="sxs-lookup"><span data-stu-id="0c24e-125">This connection can be direct, via a proxy, or through hello OMS Gateway.</span></span>
- <span data-ttu-id="0c24e-126">Tek başına bilgisayarların, sunucuların ve sanal makinelerin hello OMS MMA yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c24e-126">You can install hello OMS MMA on stand-alone computers, servers, and virtual machines.</span></span> <span data-ttu-id="0c24e-127">Tooconnect Azure barındırılan sanal makineleri tooOMS istiyorsanız, bkz: [bağlanmak Azure sanal makineleri tooLog Analytics](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="0c24e-127">If you want tooconnect Azure-hosted virtual machines tooOMS, see [Connect Azure virtual machines tooLog Analytics](log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="0c24e-128">Merhaba aracının toouse TCP bağlantı noktası 443 çeşitli kaynaklar için gerekir.</span><span class="sxs-lookup"><span data-stu-id="0c24e-128">hello agent needs toouse TCP port 443 for various resources.</span></span>

### <a name="network"></a><span data-ttu-id="0c24e-129">Ağ</span><span class="sxs-lookup"><span data-stu-id="0c24e-129">Network</span></span>

<span data-ttu-id="0c24e-130">Hello bağlantı noktası numaraları ve etki alanı URL'leri dahil erişim toonetwork kaynakları hello OMS hizmetiyle Windows aracıları tooconnect tooand kayıt için olmaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="0c24e-130">For Windows agents tooconnect tooand register with hello OMS service, they must have access toonetwork resources, including hello port numbers and domain URLs.</span></span>

- <span data-ttu-id="0c24e-131">Proxy sunucuları için uygun proxy sunucu kaynakları Aracısı ayarlarında yapılandırılan hello tooensure gerekir.</span><span class="sxs-lookup"><span data-stu-id="0c24e-131">For proxy servers, you need tooensure that hello appropriate proxy server resources are configured in agent settings.</span></span>
- <span data-ttu-id="0c24e-132">Erişim toohello Internet kısıtlamak, güvenlik duvarları için siz veya ağ mühendisleri, güvenlik duvarı toopermit erişim tooOMS tooconfigure gerekir.</span><span class="sxs-lookup"><span data-stu-id="0c24e-132">For firewalls that restrict access toohello Internet, you or your networking engineers need tooconfigure your firewall toopermit access tooOMS.</span></span> <span data-ttu-id="0c24e-133">Aracı ayarlarında bir işlem yapılması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="0c24e-133">No action is needed in agent settings.</span></span>

<span data-ttu-id="0c24e-134">Aşağıdaki tablonun hello iletişimi için gerekli kaynakları gösterir.</span><span class="sxs-lookup"><span data-stu-id="0c24e-134">hello following table shows resources needed for communication.</span></span>

>[!NOTE]
><span data-ttu-id="0c24e-135">Bazı kaynaklar aşağıdaki Merhaba, operasyonel Öngörüler, günlük analizi için önceki bir ad olduğu gerekeceğinden buraya.</span><span class="sxs-lookup"><span data-stu-id="0c24e-135">Some of hello following resources mention Operational Insights, which was a previous name for Log Analytics.</span></span>

| <span data-ttu-id="0c24e-136">Aracı Kaynağı</span><span class="sxs-lookup"><span data-stu-id="0c24e-136">Agent Resource</span></span> | <span data-ttu-id="0c24e-137">Bağlantı Noktaları</span><span class="sxs-lookup"><span data-stu-id="0c24e-137">Ports</span></span> | <span data-ttu-id="0c24e-138">HTTPS denetlemesini atlama</span><span class="sxs-lookup"><span data-stu-id="0c24e-138">Bypass HTTPS inspection</span></span> |
|---|---|---|
| <span data-ttu-id="0c24e-139">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="0c24e-139">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="0c24e-140">443</span><span class="sxs-lookup"><span data-stu-id="0c24e-140">443</span></span> | <span data-ttu-id="0c24e-141">Evet</span><span class="sxs-lookup"><span data-stu-id="0c24e-141">Yes</span></span> |
| <span data-ttu-id="0c24e-142">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="0c24e-142">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="0c24e-143">443</span><span class="sxs-lookup"><span data-stu-id="0c24e-143">443</span></span> | <span data-ttu-id="0c24e-144">Evet</span><span class="sxs-lookup"><span data-stu-id="0c24e-144">Yes</span></span> |
| <span data-ttu-id="0c24e-145">*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="0c24e-145">*.blob.core.windows.net</span></span> | <span data-ttu-id="0c24e-146">443</span><span class="sxs-lookup"><span data-stu-id="0c24e-146">443</span></span> | <span data-ttu-id="0c24e-147">Evet</span><span class="sxs-lookup"><span data-stu-id="0c24e-147">Yes</span></span> |
| <span data-ttu-id="0c24e-148">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="0c24e-148">*.azure-automation.net</span></span> | <span data-ttu-id="0c24e-149">443</span><span class="sxs-lookup"><span data-stu-id="0c24e-149">443</span></span> | <span data-ttu-id="0c24e-150">Evet</span><span class="sxs-lookup"><span data-stu-id="0c24e-150">Yes</span></span> |



## <a name="download-hello-agent-setup-file-from-oms"></a><span data-ttu-id="0c24e-151">OMS Hello Aracısı kurulum dosyasını indirin</span><span class="sxs-lookup"><span data-stu-id="0c24e-151">Download hello agent setup file from OMS</span></span>
1. <span data-ttu-id="0c24e-152">Merhaba OMS portalında, hello **genel bakış** hello sayfasında, **ayarları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="0c24e-152">In hello OMS portal, on hello **Overview** page, click hello **Settings** tile.</span></span>  <span data-ttu-id="0c24e-153">Merhaba tıklatın **bağlı kaynakları** sekmesini hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="0c24e-153">Click hello **Connected Sources** tab at hello top.</span></span>  
    <span data-ttu-id="0c24e-154">![Bağlı kaynaklar sekmesi](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span><span class="sxs-lookup"><span data-stu-id="0c24e-154">![Connected Sources tab](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span></span>
2. <span data-ttu-id="0c24e-155">Tıklatın **Windows sunucuları** ve ardından **Windows Aracısı indirme** geçerli tooyour bilgisayar işlemci türü toodownload hello kurulum dosyası.</span><span class="sxs-lookup"><span data-stu-id="0c24e-155">Click **Windows Servers** and then click **Download Windows Agent** applicable tooyour computer processor type toodownload hello setup file.</span></span>
3. <span data-ttu-id="0c24e-156">Merhaba sağında üzerinde **çalışma alanı kimliği**hello Kopyala simgesine tıklayın ve hello kimliği Not Defteri'ne yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="0c24e-156">On hello right of **Workspace ID**, click hello copy icon and paste hello ID into Notepad.</span></span>
4. <span data-ttu-id="0c24e-157">Merhaba sağında üzerinde **birincil anahtar**hello Kopyala simgesine tıklayın ve başlangıç anahtarı Not Defteri'ne yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="0c24e-157">On hello right of **Primary Key**, click hello copy icon and paste hello key into Notepad.</span></span>     

## <a name="install-hello-agent-using-setup"></a><span data-ttu-id="0c24e-158">Kurulumu kullanarak hello aracı yükleme</span><span class="sxs-lookup"><span data-stu-id="0c24e-158">Install hello agent using setup</span></span>
1. <span data-ttu-id="0c24e-159">Kurulum tooinstall hello Aracısı toomanage istediğiniz bir bilgisayarda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0c24e-159">Run Setup tooinstall hello agent on a computer that you want toomanage.</span></span>
2. <span data-ttu-id="0c24e-160">Merhaba Hoş Geldiniz sayfasında, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="0c24e-160">On hello Welcome page, click **Next**.</span></span>
3. <span data-ttu-id="0c24e-161">Merhaba lisans koşulları sayfasında, hello lisans okuyun ve ardından **ediyorum**.</span><span class="sxs-lookup"><span data-stu-id="0c24e-161">On hello License Terms page, read hello license and then click **I Agree**.</span></span>
4. <span data-ttu-id="0c24e-162">Merhaba hedef klasörü sayfasında, değiştirmek veya hello varsayılan yükleme klasörünü ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="0c24e-162">On hello Destination Folder page, change or keep hello default installation folder and then click **Next**.</span></span>
5. <span data-ttu-id="0c24e-163">Hello aracı Kur seçenekleri sayfasında, tooconnect hello Aracısı tooAzure günlük analizi (OMS), Operations Manager'ı seçin veya tooconfigure hello aracının daha sonra isterseniz hello seçimler boş bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c24e-163">On hello Agent Setup Options page, you can choose tooconnect hello agent tooAzure Log Analytics (OMS), Operations Manager, or you can leave hello choices blank if you want tooconfigure hello agent later.</span></span> <span data-ttu-id="0c24e-164">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0c24e-164">Click **Next**.</span></span>   
    - <span data-ttu-id="0c24e-165">Tooconnect tooAzure günlük analizi (OMS) seçerseniz, hello Yapıştır **çalışma alanı kimliği** ve **çalışma alanı anahtarı (birincil anahtar)** hello önceki yordamda Not Defteri'ne kopyalanan ve ardından  **Sonraki**.</span><span class="sxs-lookup"><span data-stu-id="0c24e-165">If you chose tooconnect tooAzure Log Analytics (OMS), paste hello **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in hello previous procedure and then click **Next**.</span></span>  
        <span data-ttu-id="0c24e-166">![Çalışma alanı kimliği ve birincil anahtar yapıştırın](./media/log-analytics-windows-agents/connect-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="0c24e-166">![paste Workspace ID and Primary Key](./media/log-analytics-windows-agents/connect-workspace.png)</span></span>
    - <span data-ttu-id="0c24e-167">Tooconnect tooOperations Yöneticisi'ni seçerseniz, hello yazın **yönetim grubu adı**, **Management Server** adı ve **yönetim sunucusu bağlantı noktası**ve ardından **Sonraki**.</span><span class="sxs-lookup"><span data-stu-id="0c24e-167">If you chose tooconnect tooOperations Manager, type hello **Management Group Name**, **Management Server** name, and **Management Server Port**, and then click **Next**.</span></span> <span data-ttu-id="0c24e-168">Merhaba aracı eylem hesabı sayfada hello yerel sistem hesabı veya yerel etki alanı hesabı seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="0c24e-168">On hello Agent Action Account page, choose either hello Local System account or a local domain account and then click **Next**.</span></span>  
        <span data-ttu-id="0c24e-169">![Yönetim grubu Yapılandırması](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![aracı eylem hesabı](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span><span class="sxs-lookup"><span data-stu-id="0c24e-169">![management group configuration](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span></span>

6. <span data-ttu-id="0c24e-170">Merhaba hazır tooInstall sayfasında, seçimlerinizi gözden geçirin ve ardından **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="0c24e-170">On hello Ready tooInstall page, review your choices and then click **Install**.</span></span>
7. <span data-ttu-id="0c24e-171">Yapılandırma başarıyla tamamlandı hello üzerinde sayfasında, **son**.</span><span class="sxs-lookup"><span data-stu-id="0c24e-171">On hello Configuration completed successfully page, click **Finish**.</span></span>
8. <span data-ttu-id="0c24e-172">Tamamlandığında, hello **Microsoft İzleme Aracısı** görünür **Denetim Masası**.</span><span class="sxs-lookup"><span data-stu-id="0c24e-172">When complete, hello **Microsoft Monitoring Agent** appears in **Control Panel**.</span></span> <span data-ttu-id="0c24e-173">Vardır, yapılandırmanızı gözden geçirin ve bu hello aracı bağlı tooOperational Öngörüler (OMS) olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="0c24e-173">You can review your configuration there and verify that hello agent is connected tooOperational Insights (OMS).</span></span> <span data-ttu-id="0c24e-174">Aracı bağlı tooOMS hello belirten bir ileti görüntülenir: **hello Microsoft İzleme Aracısı toohello Microsoft Operations Management Suite hizmeti başarıyla bağlandı.**</span><span class="sxs-lookup"><span data-stu-id="0c24e-174">When connected tooOMS, hello agent displays a message stating: **hello Microsoft Monitoring Agent has successfully connected toohello Microsoft Operations Management Suite service.**</span></span>

## <a name="configure-proxy-settings"></a><span data-ttu-id="0c24e-175">Proxy ayarlarını yapılandır</span><span class="sxs-lookup"><span data-stu-id="0c24e-175">Configure proxy settings</span></span>

<span data-ttu-id="0c24e-176">Yordam tooconfigure proxy ayarlarını hello Microsoft Monitoring Agent Denetim Masası'nı kullanarak aşağıdaki hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c24e-176">You can use hello following procedure tooconfigure proxy settings for hello Microsoft Monitoring Agent using Control Panel.</span></span> <span data-ttu-id="0c24e-177">Her sunucu için bu yordamı toouse gerekir.</span><span class="sxs-lookup"><span data-stu-id="0c24e-177">You need toouse this procedure for each server.</span></span> <span data-ttu-id="0c24e-178">Çok sayıda sunucuya tooconfigure gereksiniminiz varsa, daha kolay toouse bir komut dosyası tooautomate bulabileceğiniz bu işlem.</span><span class="sxs-lookup"><span data-stu-id="0c24e-178">If you have many servers that you need tooconfigure, you might find it easier toouse a script tooautomate this process.</span></span> <span data-ttu-id="0c24e-179">Bu durumda, hello sonraki yordama bakın [tooconfigure hello betik kullanarak Microsoft İzleme Aracısı için proxy ayarlarını](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span><span class="sxs-lookup"><span data-stu-id="0c24e-179">If so, see hello next procedure [tooconfigure proxy settings for hello Microsoft Monitoring Agent using a script](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span></span>

### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-control-panel"></a><span data-ttu-id="0c24e-180">Microsoft Monitoring Agent Denetim Masası'nı kullanarak hello için tooconfigure proxy ayarları</span><span class="sxs-lookup"><span data-stu-id="0c24e-180">tooconfigure proxy settings for hello Microsoft Monitoring Agent using Control Panel</span></span>
1. <span data-ttu-id="0c24e-181">**Denetim Masası**'nı açın.</span><span class="sxs-lookup"><span data-stu-id="0c24e-181">Open **Control Panel**.</span></span>
2. <span data-ttu-id="0c24e-182">**Microsoft İzleme Aracısı**'nı açın.</span><span class="sxs-lookup"><span data-stu-id="0c24e-182">Open **Microsoft Monitoring Agent**.</span></span>
3. <span data-ttu-id="0c24e-183">Merhaba tıklatın **Proxy ayarlarını** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="0c24e-183">Click hello **Proxy Settings** tab.</span></span>  
    <span data-ttu-id="0c24e-184">![ara sunucu ayarları sekmesi](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span><span class="sxs-lookup"><span data-stu-id="0c24e-184">![proxy settings tab](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span></span>
4. <span data-ttu-id="0c24e-185">Seçin **bir proxy sunucu kullanacak** hello URL'sini yazın ve bağlantı noktası numarası, gerekli, benzer toohello örnekte gösterilen ise.</span><span class="sxs-lookup"><span data-stu-id="0c24e-185">Select **Use a proxy server** and type hello URL and port number, if one is needed, similar toohello example shown.</span></span> <span data-ttu-id="0c24e-186">Proxy sunucusu kimlik doğrulaması gerektiriyorsa, hello kullanıcı adı ve parola tooaccess hello proxy sunucusu yazın.</span><span class="sxs-lookup"><span data-stu-id="0c24e-186">If your proxy server requires authentication, type hello username and password tooaccess hello proxy server.</span></span>


### <a name="verify-agent-connectivity-toooms"></a><span data-ttu-id="0c24e-187">Aracı bağlantısı tooOMS doğrulayın</span><span class="sxs-lookup"><span data-stu-id="0c24e-187">Verify agent connectivity tooOMS</span></span>

<span data-ttu-id="0c24e-188">Kolayca aracılarınızı hello aşağıdaki yordamı kullanarak OMS ile iletişim kuran olup olmadığını doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="0c24e-188">You can easily verify whether your agents are communicating with OMS using hello following procedure:</span></span>

1.  <span data-ttu-id="0c24e-189">Merhaba Windows Aracısı ile Merhaba bilgisayarda Denetim Masası açın.</span><span class="sxs-lookup"><span data-stu-id="0c24e-189">On hello computer with hello Windows agent, open Control Panel.</span></span>
2.  <span data-ttu-id="0c24e-190">Microsoft Monitoring Agent'ı açın.</span><span class="sxs-lookup"><span data-stu-id="0c24e-190">Open Microsoft Monitoring Agent.</span></span>
3.  <span data-ttu-id="0c24e-191">Hello Azure günlük analizi (OMS) sekmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0c24e-191">Click hello Azure Log Analytics (OMS) tab.</span></span>
4.  <span data-ttu-id="0c24e-192">Merhaba Durum sütununda bu hello aracı toohello Operations Management Suite hizmeti başarıyla bağlandı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0c24e-192">In hello Status column, you should see that hello agent connected successfully toohello Operations Management Suite service.</span></span>

![bağlı aracı](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-a-script"></a><span data-ttu-id="0c24e-194">Merhaba betik kullanarak Microsoft Monitoring Agent için tooconfigure proxy ayarları</span><span class="sxs-lookup"><span data-stu-id="0c24e-194">tooconfigure proxy settings for hello Microsoft Monitoring Agent using a script</span></span>
<span data-ttu-id="0c24e-195">Aşağıdaki örnek, bilgi belirli tooyour ortamıyla güncelleştirme, bir PS1 dosya adı uzantısıyla kaydedin ve ardından hello betik toohello OMS hizmetine doğrudan bağlanan her bilgisayarda çalıştırın hello kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="0c24e-195">Copy hello following sample, update it with information specific tooyour environment, save it with a PS1 file name extension, and then run hello script on each computer that connects directly toohello OMS service.</span></span>

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get hello Health Service configuration object.  We need toodetermine if we
    #have hello right update rollup with hello API we need.  If not, no need toorun hello rest of hello script.
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

    Write-Output "Setting proxy too$ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-hello-agent-using-hello-command-line"></a><span data-ttu-id="0c24e-196">Merhaba komut satırını kullanarak hello aracı yükleme</span><span class="sxs-lookup"><span data-stu-id="0c24e-196">Install hello agent using hello command line</span></span>
- <span data-ttu-id="0c24e-197">Değiştirebilirsiniz ve hello komut satırını kullanarak örnek tooinstall hello aracı aşağıdaki hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c24e-197">Modify and then use hello following example tooinstall hello agent using hello command line.</span></span> <span data-ttu-id="0c24e-198">Merhaba örnek tam olarak sessiz yükleme gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="0c24e-198">hello example performs a fully silent installation.</span></span>

    >[!NOTE]
    <span data-ttu-id="0c24e-199">Bir aracı tooupgrade istiyorsanız, toouse hello günlük analizi gerekir betik API'si.</span><span class="sxs-lookup"><span data-stu-id="0c24e-199">If you want tooupgrade an agent, you need toouse hello Log Analytics scripting API.</span></span> <span data-ttu-id="0c24e-200">Merhaba sonraki bölümde tooupgrade bir aracı bakın.</span><span class="sxs-lookup"><span data-stu-id="0c24e-200">See hello next section tooupgrade an agent.</span></span>

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

<span data-ttu-id="0c24e-201">Merhaba Aracısı'nın kullandığı IExpress kendi ayıklayıcısı hello kullanarak `/c` komutu.</span><span class="sxs-lookup"><span data-stu-id="0c24e-201">hello agent uses IExpress as its self-extractor using hello `/c` command.</span></span> <span data-ttu-id="0c24e-202">Merhaba komut satırı anahtarları adresindeki görebilirsiniz [IExpress komut satırı anahtarları](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) ve ardından güncelleştirme hello örnek toosuit gereksinimlerinizi.</span><span class="sxs-lookup"><span data-stu-id="0c24e-202">You can see hello command-line switches at [Command-line switches for IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) and then update hello example toosuit your needs.</span></span>

|<span data-ttu-id="0c24e-203">MMA özgü seçenekleri</span><span class="sxs-lookup"><span data-stu-id="0c24e-203">MMA-specific options</span></span>                   |<span data-ttu-id="0c24e-204">Notlar</span><span class="sxs-lookup"><span data-stu-id="0c24e-204">Notes</span></span>         |
|---------------------------------------|--------------|
|<span data-ttu-id="0c24e-205">ADD_OPINSIGHTS_WORKSPACE</span><span class="sxs-lookup"><span data-stu-id="0c24e-205">ADD_OPINSIGHTS_WORKSPACE</span></span>               | <span data-ttu-id="0c24e-206">1 = Yapılandır hello Aracısı tooreport tooa çalışma alanı</span><span class="sxs-lookup"><span data-stu-id="0c24e-206">1 = Configure hello agent tooreport tooa workspace</span></span>                |
|<span data-ttu-id="0c24e-207">OPINSIGHTS_WORKSPACE_ID</span><span class="sxs-lookup"><span data-stu-id="0c24e-207">OPINSIGHTS_WORKSPACE_ID</span></span>                | <span data-ttu-id="0c24e-208">Merhaba çalışma tooadd için çalışma alanı kimliği (GUID)</span><span class="sxs-lookup"><span data-stu-id="0c24e-208">Workspace Id (guid) for hello workspace tooadd</span></span>                    |
|<span data-ttu-id="0c24e-209">OPINSIGHTS_WORKSPACE_KEY</span><span class="sxs-lookup"><span data-stu-id="0c24e-209">OPINSIGHTS_WORKSPACE_KEY</span></span>               | <span data-ttu-id="0c24e-210">Çalışma alanı anahtarı kullanılan tooinitially hello çalışma ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="0c24e-210">Workspace key used tooinitially authenticate with hello workspace</span></span> |
|<span data-ttu-id="0c24e-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span><span class="sxs-lookup"><span data-stu-id="0c24e-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span></span>  | <span data-ttu-id="0c24e-212">Merhaba çalışma bulunduğu hello bulut ortamını belirtin</span><span class="sxs-lookup"><span data-stu-id="0c24e-212">Specify hello cloud environment where hello workspace is located</span></span> <br> <span data-ttu-id="0c24e-213">0 = azure ticari bulut (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="0c24e-213">0 = Azure commercial cloud (default)</span></span> <br> <span data-ttu-id="0c24e-214">1 azure kamu =</span><span class="sxs-lookup"><span data-stu-id="0c24e-214">1 = Azure Government</span></span> |
|<span data-ttu-id="0c24e-215">OPINSIGHTS_PROXY_URL</span><span class="sxs-lookup"><span data-stu-id="0c24e-215">OPINSIGHTS_PROXY_URL</span></span>               | <span data-ttu-id="0c24e-216">Merhaba proxy toouse için URI</span><span class="sxs-lookup"><span data-stu-id="0c24e-216">URI for hello proxy toouse</span></span> |
|<span data-ttu-id="0c24e-217">OPINSIGHTS_PROXY_USERNAME</span><span class="sxs-lookup"><span data-stu-id="0c24e-217">OPINSIGHTS_PROXY_USERNAME</span></span>               | <span data-ttu-id="0c24e-218">Kullanıcı adı tooaccess doğrulanmış bir proxy</span><span class="sxs-lookup"><span data-stu-id="0c24e-218">Username tooaccess an authenticated proxy</span></span> |
|<span data-ttu-id="0c24e-219">OPINSIGHTS_PROXY_PASSWORD</span><span class="sxs-lookup"><span data-stu-id="0c24e-219">OPINSIGHTS_PROXY_PASSWORD</span></span>               | <span data-ttu-id="0c24e-220">Parola tooaccess doğrulanmış bir proxy</span><span class="sxs-lookup"><span data-stu-id="0c24e-220">Password tooaccess an authenticated proxy</span></span> |

>[!NOTE]
<span data-ttu-id="0c24e-221">tooavoid basarsa hello komut satırı uzunluğunu IExpress, yapılandırılmış hiçbir çalışma alanıyla hello aracısı yükleyin ve ardından bir betik tooset yapılandırmasını hello çalışma alanı için kullanın.</span><span class="sxs-lookup"><span data-stu-id="0c24e-221">tooavoid hitting hello command-line length limit of IExpress, install hello agent with no workspace configured and then use a script tooset configuration for hello workspace.</span></span>

>[!NOTE]
<span data-ttu-id="0c24e-222">Alırsanız bir `Command line option syntax error.` hello kullanırken `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parametresi, geçici çözüm aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0c24e-222">If you get a `Command line option syntax error.` when using hello `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parameter, you can use hello following workaround:</span></span>
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a><span data-ttu-id="0c24e-223">Bir komut dosyası kullanarak bir çalışma alanı Ekle</span><span class="sxs-lookup"><span data-stu-id="0c24e-223">Add a workspace using a script</span></span>
<span data-ttu-id="0c24e-224">Aşağıdaki örneğine hello ile Merhaba günlük analizi aracı komut dosyası API kullanarak bir çalışma alanı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0c24e-224">Add a workspace using hello Log Analytics agent scripting API with hello following example:</span></span>

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

<span data-ttu-id="0c24e-225">tooadd Azure ABD devlet kurumları, komut dosyası örneği aşağıdaki kullanım hello için çalışma:</span><span class="sxs-lookup"><span data-stu-id="0c24e-225">tooadd a workspace in Azure for US Government, use hello following script sample:</span></span>
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
<span data-ttu-id="0c24e-226">Sütun hello komut satırı kullandıysanız, daha önce tooinstall komut dosyası veya hello Aracısı'nı yapılandırma `EnableAzureOperationalInsights` tarafından değiştirildi `AddCloudWorkspace`.</span><span class="sxs-lookup"><span data-stu-id="0c24e-226">If you've used hello command line or script previously tooinstall or configure hello agent, `EnableAzureOperationalInsights` was replaced by `AddCloudWorkspace`.</span></span>

## <a name="install-hello-agent-using-dsc-in-azure-automation"></a><span data-ttu-id="0c24e-227">Azure Otomasyonu'nda DSC kullanarak hello aracı yükleme</span><span class="sxs-lookup"><span data-stu-id="0c24e-227">Install hello agent using DSC in Azure Automation</span></span>

<span data-ttu-id="0c24e-228">Azure Otomasyonu'nda DSC kullanarak betik örnek tooinstall hello aracısını aşağıdaki hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c24e-228">You can use hello following script example tooinstall hello agent using DSC in Azure Automation.</span></span> <span data-ttu-id="0c24e-229">Merhaba örneği yükler hello hello tarafından tanımlanan 64-bit Aracısı `URI` değeri.</span><span class="sxs-lookup"><span data-stu-id="0c24e-229">hello example installs hello 64-bit agent, identified by hello `URI` value.</span></span> <span data-ttu-id="0c24e-230">Merhaba URI değerini değiştirerek hello 32-bit sürümünü de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c24e-230">You can also use hello 32-bit version by replacing hello URI value.</span></span> <span data-ttu-id="0c24e-231">Merhaba URI'ler iki sürümü vardır:</span><span class="sxs-lookup"><span data-stu-id="0c24e-231">hello URIs for both versions are:</span></span>

- <span data-ttu-id="0c24e-232">Windows 64-bit Aracısı - https://go.microsoft.com/fwlink/?LinkId=828603</span><span class="sxs-lookup"><span data-stu-id="0c24e-232">Windows 64-bit agent - https://go.microsoft.com/fwlink/?LinkId=828603</span></span>
- <span data-ttu-id="0c24e-233">Windows 32-bit Aracısı - https://go.microsoft.com/fwlink/?LinkId=828604</span><span class="sxs-lookup"><span data-stu-id="0c24e-233">Windows 32-bit agent - https://go.microsoft.com/fwlink/?LinkId=828604</span></span>


>[!NOTE]
<span data-ttu-id="0c24e-234">Bu yordam ve komut dosyası örneği var olan bir aracıyı yükseltmez.</span><span class="sxs-lookup"><span data-stu-id="0c24e-234">This procedure and script example will not upgrade an existing agent.</span></span>

1. <span data-ttu-id="0c24e-235">Merhaba xPSDesiredStateConfiguration DSC modülü içe gelen [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) Azure Otomasyonu içine.</span><span class="sxs-lookup"><span data-stu-id="0c24e-235">Import hello xPSDesiredStateConfiguration DSC Module from [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) into Azure Automation.</span></span>  
2.  <span data-ttu-id="0c24e-236">İçin Azure Otomasyonu değişken varlıkları oluşturma *OPSINSIGHTS_WS_ID* ve *OPSINSIGHTS_WS_KEY*.</span><span class="sxs-lookup"><span data-stu-id="0c24e-236">Create Azure Automation variable assets for *OPSINSIGHTS_WS_ID* and *OPSINSIGHTS_WS_KEY*.</span></span> <span data-ttu-id="0c24e-237">Ayarlama *OPSINSIGHTS_WS_ID* tooyour OMS günlük analizi çalışma alanı kimliği ve *OPSINSIGHTS_WS_KEY* çalışma alanınızın toohello birincil anahtar.</span><span class="sxs-lookup"><span data-stu-id="0c24e-237">Set *OPSINSIGHTS_WS_ID* tooyour OMS Log Analytics workspace ID and set *OPSINSIGHTS_WS_KEY* toohello primary key of your workspace.</span></span>
3.  <span data-ttu-id="0c24e-238">Aşağıdaki komut dosyası ve MMAgent.ps1 Kaydet hello kullanın</span><span class="sxs-lookup"><span data-stu-id="0c24e-238">Use hello following script and save it as MMAgent.ps1</span></span>
4.  <span data-ttu-id="0c24e-239">Değiştirebilirsiniz ve Azure Otomasyonu'nda DSC kullanarak örnek tooinstall hello aracısını aşağıdaki hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c24e-239">Modify and then use hello following example tooinstall hello agent using DSC in Azure Automation.</span></span> <span data-ttu-id="0c24e-240">MMAgent.ps1 hello Azure Otomasyon arabirimi veya cmdlet'ini kullanarak Azure Automation'a aktarabilir.</span><span class="sxs-lookup"><span data-stu-id="0c24e-240">Import MMAgent.ps1 into Azure Automation by using hello Azure Automation interface or cmdlet.</span></span>
5.  <span data-ttu-id="0c24e-241">Bir düğüm toohello yapılandırması atayın.</span><span class="sxs-lookup"><span data-stu-id="0c24e-241">Assign a node toohello configuration.</span></span> <span data-ttu-id="0c24e-242">15 dakika içinde hello düğüm yapılandırmasını denetler ve hello MMA toohello düğümü gönderilir.</span><span class="sxs-lookup"><span data-stu-id="0c24e-242">Within 15 minutes, hello node checks its configuration and hello MMA is pushed toohello node.</span></span>

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

### <a name="get-hello-latest-productid-value"></a><span data-ttu-id="0c24e-243">Merhaba son ProductID değerini alın</span><span class="sxs-lookup"><span data-stu-id="0c24e-243">Get hello latest ProductId value</span></span>

<span data-ttu-id="0c24e-244">Merhaba `ProductId value` hello MMAgent.ps1 betik benzersiz tooeach Aracısı sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="0c24e-244">hello `ProductId value` in hello MMAgent.ps1 script is unique tooeach agent version.</span></span> <span data-ttu-id="0c24e-245">Her bir aracının güncelleştirilmiş bir sürümü yayımlandığında, hello ProductID değerini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="0c24e-245">When an updated version of each agent is published, hello ProductId value changes.</span></span> <span data-ttu-id="0c24e-246">Bu nedenle, Hello ProductID hello gelecekteki değiştiğinde, basit bir komut dosyası kullanarak hello aracı sürümü bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c24e-246">So, when hello ProductId changes in hello future, you can find hello agent version using a simple script.</span></span> <span data-ttu-id="0c24e-247">Bir test sunucusunda yüklü hello en son aracı sürümü aldıktan sonra aşağıdaki komut dosyası tooget yüklü hello ProductID değeri hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c24e-247">After you have hello latest agent version installed on a test server, you can use hello following script tooget hello installed ProductId value.</span></span> <span data-ttu-id="0c24e-248">Merhaba son ProductID değerini kullanarak hello MMAgent.ps1 betik hello değerinde güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c24e-248">Using hello latest ProductId value, you can update hello value in hello MMAgent.ps1 script.</span></span>

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

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a><span data-ttu-id="0c24e-249">Bir aracı el ile yapılandırma veya ek çalışma alanları ekleme</span><span class="sxs-lookup"><span data-stu-id="0c24e-249">Configure an agent manually or add additional workspaces</span></span>
<span data-ttu-id="0c24e-250">Aracıları yüklediyseniz bunları yapılandırmadı ancak veya hello Aracısı tooreport toomultiple çalışma alanları istiyorsanız, bilgi tooenable bir aracı aşağıdaki hello kullanın ya da yeniden yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0c24e-250">If you've installed agents but did not configure them or if you want hello agent tooreport toomultiple workspaces, you can use hello following information tooenable an agent or reconfigure it.</span></span> <span data-ttu-id="0c24e-251">Merhaba Aracısı yapılandırdıktan sonra hello Aracısı hizmeti ile kaydeder ve gerekli yapılandırma bilgilerini ve çözüm bilgileri içeren yönetim paketleri alır.</span><span class="sxs-lookup"><span data-stu-id="0c24e-251">After you've configured hello agent, it will register with hello agent service and will get necessary configuration information and management packs that contain solution information.</span></span>

1. <span data-ttu-id="0c24e-252">Merhaba Microsoft İzleme Aracısı yükledikten sonra açmak **Denetim Masası**.</span><span class="sxs-lookup"><span data-stu-id="0c24e-252">After you've installed hello Microsoft Monitoring Agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="0c24e-253">Açık **Microsoft İzleme Aracısı** ve hello ardından **Azure günlük analizi (OMS)** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="0c24e-253">Open **Microsoft Monitoring Agent** and then click hello **Azure Log Analytics (OMS)** tab.</span></span>   
3. <span data-ttu-id="0c24e-254">Tıklatın **Ekle** tooopen hello **günlük analizi çalışma alanı Ekle** kutusu.</span><span class="sxs-lookup"><span data-stu-id="0c24e-254">Click **Add** tooopen hello **Add a Log Analytics Workspace** box.</span></span>
4. <span data-ttu-id="0c24e-255">Yapıştır hello **çalışma alanı kimliği** ve **çalışma alanı anahtarı (birincil anahtar)** tooadd istediğiniz ve ardından hello çalışma alanı için bir önceki yordamda Not Defteri'ne kopyalanan **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="0c24e-255">Paste hello **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in a previous procedure for hello workspace that you want tooadd and then click **OK**.</span></span>  
    <span data-ttu-id="0c24e-256">![Operasyonel Öngörüler yapılandırın](./media/log-analytics-windows-agents/add-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="0c24e-256">![configure Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span></span>

<span data-ttu-id="0c24e-257">Merhaba aracısı tarafından izlenen bilgisayarlardan toplanan veriler sonra OMS tarafından izlenen bilgisayarlar hello sayısı hello hello OMS portalında görünür **bağlı kaynakları** sekmesinde **ayarları** olarak  **Bağlı olan sunucuları**.</span><span class="sxs-lookup"><span data-stu-id="0c24e-257">After data is collected from computers monitored by hello agent, hello number of computers monitored by OMS will appear in hello OMS portal on hello **Connected Sources** tab in **Settings** as **Servers Connected**.</span></span>


## <a name="toodisable-an-agent"></a><span data-ttu-id="0c24e-258">toodisable bir aracı</span><span class="sxs-lookup"><span data-stu-id="0c24e-258">toodisable an agent</span></span>
1. <span data-ttu-id="0c24e-259">Merhaba aracıyı yükledikten sonra açmak **Denetim Masası**.</span><span class="sxs-lookup"><span data-stu-id="0c24e-259">After installing hello agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="0c24e-260">Microsoft Monitoring Agent'ı açın ve hello ardından **Azure günlük analizi (OMS)** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="0c24e-260">Open Microsoft Monitoring Agent and then click hello **Azure Log Analytics (OMS)** tab.</span></span>
3. <span data-ttu-id="0c24e-261">Bir çalışma alanını seçin ve ardından **kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="0c24e-261">Select a workspace and then click **Remove**.</span></span> <span data-ttu-id="0c24e-262">Bu adım için diğer çalışma alanları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="0c24e-262">Repeat this step for all other workspaces.</span></span>


## <a name="optionally-configure-agents-tooreport-tooan-operations-manager-management-group"></a><span data-ttu-id="0c24e-263">İsteğe bağlı olarak, aracıları tooreport tooan Operations Manager yönetim grubunu yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0c24e-263">Optionally, configure agents tooreport tooan Operations Manager management group</span></span>

<span data-ttu-id="0c24e-264">BT altyapınızın Operations Manager'ı kullanırsanız, hello MMA aracı Operations Manager aracısı olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c24e-264">If you use Operations Manager in your IT infrastructure, you can also use hello MMA agent as an Operations Manager agent.</span></span>

### <a name="tooconfigure-mma-agents-tooreport-tooan-operations-manager-management-group"></a><span data-ttu-id="0c24e-265">tooconfigure MMA aracıları tooreport tooan Operations Manager yönetim grubu</span><span class="sxs-lookup"><span data-stu-id="0c24e-265">tooconfigure MMA agents tooreport tooan Operations Manager management group</span></span>
1.  <span data-ttu-id="0c24e-266">Merhaba Aracısı yüklendiği hello bilgisayarda açın **Denetim Masası**.</span><span class="sxs-lookup"><span data-stu-id="0c24e-266">On hello computer where hello agent is installed, open **Control Panel**.</span></span>  
2.  <span data-ttu-id="0c24e-267">Açık **Microsoft İzleme Aracısı** ve hello ardından **Operations Manager** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="0c24e-267">Open **Microsoft Monitoring Agent** and then click hello **Operations Manager** tab.</span></span>  
    <span data-ttu-id="0c24e-268">![Microsoft İzleme Aracısı Operations Manager sekmesi](./media/log-analytics-windows-agents/om-mg01.png)</span><span class="sxs-lookup"><span data-stu-id="0c24e-268">![Microsoft Monitoring Agent Operations Manager tab](./media/log-analytics-windows-agents/om-mg01.png)</span></span>
3.  <span data-ttu-id="0c24e-269">Operations Manager sunucularınızın Active Directory ile tümleştirme varsa, tıklatın **yönetim grubu atamalarını AD DS'den otomatik olarak güncelleştir**.</span><span class="sxs-lookup"><span data-stu-id="0c24e-269">If your Operations Manager servers have integration with Active Directory, click **Automatically update management group assignments from AD DS**.</span></span>
4.  <span data-ttu-id="0c24e-270">Tıklatın **Ekle** tooopen hello **bir yönetim grubu Ekle** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="0c24e-270">Click **Add** tooopen hello **Add a Management Group** dialog box.</span></span>  
    <span data-ttu-id="0c24e-271">![Microsoft İzleme Aracısı Yönetim Grubu Ekle](./media/log-analytics-windows-agents/oms-mma-om02.png)</span><span class="sxs-lookup"><span data-stu-id="0c24e-271">![Microsoft Monitoring Agent Add a Management Group](./media/log-analytics-windows-agents/oms-mma-om02.png)</span></span>
5.  <span data-ttu-id="0c24e-272">İçinde **yönetim grubu adı** kutusu, yönetim grubunuzun türü hello adı.</span><span class="sxs-lookup"><span data-stu-id="0c24e-272">In **Management group name** box, type hello name of your management group.</span></span>
6.  <span data-ttu-id="0c24e-273">Merhaba, **birincil yönetim sunucusu** kutusu, türü hello hello birincil yönetim sunucusunun bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="0c24e-273">In hello **Primary management server** box, type hello computer name of hello primary management server.</span></span>
7.  <span data-ttu-id="0c24e-274">Merhaba, **yönetim sunucusu bağlantı noktası** kutusunda türü hello TCP bağlantı noktası numarası.</span><span class="sxs-lookup"><span data-stu-id="0c24e-274">In hello **Management server port** box, type hello TCP port number.</span></span>
8.  <span data-ttu-id="0c24e-275">Altında **aracı eylem hesabı**, hello yerel sistem hesabı veya yerel etki alanı hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="0c24e-275">Under **Agent Action Account**, choose either hello Local System account or a local domain account.</span></span>
9.  <span data-ttu-id="0c24e-276">Tıklatın **Tamam** tooclose hello **bir yönetim grubu Ekle** iletişim kutusunu ve ardından **Tamam** tooclose hello **Microsoft Monitoring Agent özellikleri**iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="0c24e-276">Click **OK** tooclose hello **Add a Management Group** dialog box and then click **OK** tooclose hello **Microsoft Monitoring Agent Properties** dialog box.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0c24e-277">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0c24e-277">Next steps</span></span>

- <span data-ttu-id="0c24e-278">[Günlük analizi çözümleri Çözümleri Galerisi hello eklemek](log-analytics-add-solutions.md) tooadd işlevselliği ve toplama verileri.</span><span class="sxs-lookup"><span data-stu-id="0c24e-278">[Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md) tooadd functionality and gather data.</span></span>
