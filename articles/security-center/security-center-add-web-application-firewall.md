---
title: "Azure Güvenlik Merkezi'nde bir web uygulaması güvenlik duvarı aaaAdd | Microsoft Docs"
description: "Bu belge size nasıl tooimplement hello Azure Güvenlik Merkezi önerilerini gösterir. ** bir web uygulaması güvenlik duvarı ** ekleyin ve ** uygulama koruma ** sonlandır."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 8f56139a-4466-48ac-90fb-86d002cf8242
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: terrylan
ms.openlocfilehash: bff0aa2a5c6e0dde23396f93de52abe295053581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-web-application-firewall-in-azure-security-center"></a><span data-ttu-id="a609a-103">Azure Güvenlik Merkezi'nde bir web uygulaması güvenlik duvarı ekleme</span><span class="sxs-lookup"><span data-stu-id="a609a-103">Add a web application firewall in Azure Security Center</span></span>
<span data-ttu-id="a609a-104">Azure Güvenlik Merkezi, web uygulamalarınızı Microsoft iş ortağı toosecure bir web uygulaması Güvenlik Duvarı (WAF) eklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="a609a-104">Azure Security Center may recommend that you add a web application firewall (WAF) from a Microsoft partner toosecure your web applications.</span></span> <span data-ttu-id="a609a-105">Bu belge, nasıl bir örnek üzerinden anlatan tooapply Bu öneri.</span><span class="sxs-lookup"><span data-stu-id="a609a-105">This document walks you through an example of how tooapply this recommendation.</span></span>

<span data-ttu-id="a609a-106">WAF öneri açık gelen web bağlantı noktaları (80,443) içeren bir ilişkili ağ güvenlik grubu olan tüm genel kullanıma yönelik IP'si için (örnek düzeyinde IP veya yük dengeli IP) gösterilir.</span><span class="sxs-lookup"><span data-stu-id="a609a-106">A WAF recommendation is shown for any public facing IP (either Instance Level IP or Load Balanced IP) that has an associated network security group with open inbound web ports (80,443).</span></span>

<span data-ttu-id="a609a-107">Güvenlik Merkezi WAF toohelp provizyon sanal makineler ve uygulama hizmeti ortamı, web uygulamalarınızı hedefleyen saldırılara karşı korumaya önerir.</span><span class="sxs-lookup"><span data-stu-id="a609a-107">Security Center recommends that you provision a WAF toohelp defend against attacks targeting your web applications on virtual machines and on App Service Environment.</span></span> <span data-ttu-id="a609a-108">Uygulama hizmeti ortamı (ana) olan bir [Premium](https://azure.microsoft.com/pricing/details/app-service/) hizmet planı seçeneği Azure App Service, güvenli bir şekilde Azure App Service uygulamalarını çalıştırmak için tam yalıtılmış ve ayrılmış bir ortam sağlar.</span><span class="sxs-lookup"><span data-stu-id="a609a-108">An App Service Environment (ASE) is a [Premium](https://azure.microsoft.com/pricing/details/app-service/) service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps.</span></span> <span data-ttu-id="a609a-109">toolearn ana, hakkında daha fazla bilgi görmek hello [uygulama hizmeti ortamı belgeleri](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="a609a-109">toolearn more about ASE, see hello [App Service Environment Documentation](../app-service/app-service-app-service-environments-readme.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a609a-110">Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="a609a-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="a609a-111">Bu belge hakkında adım adım kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="a609a-111">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="a609a-112">Merhaba öneriyi uygulamayı</span><span class="sxs-lookup"><span data-stu-id="a609a-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="a609a-113">Merhaba, **önerileri** dikey penceresinde, select **güvenli web uygulaması Güvenlik Duvarı'nı kullanarak web uygulamasına**.</span><span class="sxs-lookup"><span data-stu-id="a609a-113">In hello **Recommendations** blade, select **Secure web application using web application firewall**.</span></span>
   <span data-ttu-id="a609a-114">![Güvenli web uygulaması][1]</span><span class="sxs-lookup"><span data-stu-id="a609a-114">![Secure web Application][1]</span></span>
2. <span data-ttu-id="a609a-115">Merhaba, **web uygulaması Güvenlik Duvarı'nı kullanarak web uygulamalarınızı güvenli** dikey penceresinde, bir web uygulaması seçin.</span><span class="sxs-lookup"><span data-stu-id="a609a-115">In hello **Secure your web applications using web application firewall** blade, select a web application.</span></span> <span data-ttu-id="a609a-116">Merhaba **bir Web uygulaması güvenlik duvarı ekleme** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="a609a-116">hello **Add a Web Application Firewall** blade opens.</span></span>
   <span data-ttu-id="a609a-117">![Web uygulaması güvenlik duvarı ekleme][2]</span><span class="sxs-lookup"><span data-stu-id="a609a-117">![Add a web application firewall][2]</span></span>
3. <span data-ttu-id="a609a-118">Varsa mevcut bir web uygulaması güvenlik duvarı toouse seçebilir veya yeni bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a609a-118">You can choose toouse an existing web application firewall if available or you can create a new one.</span></span> <span data-ttu-id="a609a-119">Bu örnekte, yok hiçbir varolan WAFs bir WAF oluşturuyoruz şekilde.</span><span class="sxs-lookup"><span data-stu-id="a609a-119">In this example, there are no existing WAFs available so we create a WAF.</span></span>
4. <span data-ttu-id="a609a-120">toocreate bir WAF hello tümleşik ortakları listesinden bir çözümü seçin.</span><span class="sxs-lookup"><span data-stu-id="a609a-120">toocreate a WAF, select a solution from hello list of integrated partners.</span></span> <span data-ttu-id="a609a-121">Bu örnekte, biz seçin **Barracuda Web uygulaması güvenlik duvarı**.</span><span class="sxs-lookup"><span data-stu-id="a609a-121">In this example, we select **Barracuda Web Application Firewall**.</span></span>
5. <span data-ttu-id="a609a-122">Merhaba **Barracuda Web uygulaması güvenlik duvarı** dikey pencere açılır hello iş ortağı çözümü hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a609a-122">hello **Barracuda Web Application Firewall** blade opens providing you information about hello partner solution.</span></span> <span data-ttu-id="a609a-123">Seçin **oluşturma** hello bilgi dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="a609a-123">Select **Create** in hello information blade.</span></span>

   ![Güvenlik Duvarı bilgileri dikey penceresi][3]

6. <span data-ttu-id="a609a-125">Merhaba **yeni Web uygulaması güvenlik duvarı** dikey penceresi açılır ve sizi gerçekleştirebileceğiniz **VM Yapılandırması** sağlamak ve adımlarını **WAF bilgi**.</span><span class="sxs-lookup"><span data-stu-id="a609a-125">hello **New Web Application Firewall** blade opens, where you can perform **VM Configuration** steps and provide **WAF Information**.</span></span> <span data-ttu-id="a609a-126">Seçin **VM Yapılandırması**.</span><span class="sxs-lookup"><span data-stu-id="a609a-126">Select **VM Configuration**.</span></span>
7. <span data-ttu-id="a609a-127">Merhaba, **VM Yapılandırması** dikey penceresinde gerekli toospin çalıştıran hello sanal makineyi hello WAF bilgileri girin.</span><span class="sxs-lookup"><span data-stu-id="a609a-127">In hello **VM Configuration** blade, you enter information required toospin up hello virtual machine that runs hello WAF.</span></span>
   <span data-ttu-id="a609a-128">![VM yapılandırması][4]</span><span class="sxs-lookup"><span data-stu-id="a609a-128">![VM configuration][4]</span></span>
8. <span data-ttu-id="a609a-129">Toohello iade **yeni Web uygulaması güvenlik duvarı** dikey penceresinde ve select **WAF bilgi**.</span><span class="sxs-lookup"><span data-stu-id="a609a-129">Return toohello **New Web Application Firewall** blade and select **WAF Information**.</span></span> <span data-ttu-id="a609a-130">Merhaba, **WAF bilgi** dikey penceresinde hello WAF kendisini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a609a-130">In hello **WAF Information** blade, you configure hello WAF itself.</span></span> <span data-ttu-id="a609a-131">7. adım, hangi hello WAF çalıştırır ve 8. adım sağlar tooprovision hello WAF kendisini tooconfigure hello sanal makine sağlar.</span><span class="sxs-lookup"><span data-stu-id="a609a-131">Step 7 allows you tooconfigure hello virtual machine on which hello WAF runs and step 8 enables you tooprovision hello WAF itself.</span></span>

## <a name="finalize-application-protection"></a><span data-ttu-id="a609a-132">Uygulama korumayı Sonlandır</span><span class="sxs-lookup"><span data-stu-id="a609a-132">Finalize application protection</span></span>
1. <span data-ttu-id="a609a-133">Toohello iade **önerileri** dikey.</span><span class="sxs-lookup"><span data-stu-id="a609a-133">Return toohello **Recommendations** blade.</span></span> <span data-ttu-id="a609a-134">Adlı hello WAF oluşturduktan sonra yeni bir giriş oluşturulan **uygulama korumayı Sonlandır**.</span><span class="sxs-lookup"><span data-stu-id="a609a-134">A new entry was generated after you created hello WAF, called **Finalize application protection**.</span></span> <span data-ttu-id="a609a-135">Bu giriş, Merhaba uygulaması koruyabilmeniz için gerçekten hello WAF hello Azure sanal ağ içinde yukarı bağlantı kabloları toocomplete hello işlemi gereksinim bilmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a609a-135">This entry lets you know that you need toocomplete hello process of actually wiring up hello WAF within hello Azure Virtual Network so that it can protect hello application.</span></span>

   ![Uygulama korumayı Sonlandır][5]

2. <span data-ttu-id="a609a-137">Seçin **uygulama korumayı Sonlandır**.</span><span class="sxs-lookup"><span data-stu-id="a609a-137">Select **Finalize application protection**.</span></span> <span data-ttu-id="a609a-138">Yeni bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="a609a-138">A new blade opens.</span></span> <span data-ttu-id="a609a-139">Yönlendirdi trafiği toohave gerektiren bir web uygulaması olduğunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a609a-139">You can see that there is a web application that needs toohave its traffic rerouted.</span></span>
3. <span data-ttu-id="a609a-140">Merhaba web uygulaması seçin.</span><span class="sxs-lookup"><span data-stu-id="a609a-140">Select hello web application.</span></span> <span data-ttu-id="a609a-141">Merhaba web uygulaması güvenlik duvarı Kurulumu Tamamlanıyor için adımları sağlayan bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="a609a-141">A blade opens that gives you steps for finalizing hello web application firewall setup.</span></span> <span data-ttu-id="a609a-142">Merhaba adımları tamamlayın ve ardından **trafiği kısıtlamak**.</span><span class="sxs-lookup"><span data-stu-id="a609a-142">Complete hello steps, and then select **Restrict traffic**.</span></span> <span data-ttu-id="a609a-143">Güvenlik Merkezi, ardından sizin için kablolama yukarı hello.</span><span class="sxs-lookup"><span data-stu-id="a609a-143">Security Center then does hello wiring-up for you.</span></span>

   ![Trafiği kısıtlama][6]

> [!NOTE]
> <span data-ttu-id="a609a-145">Bu uygulamalar tooyour varolan WAF dağıtımlar ekleyerek, birden çok web uygulamasına Güvenlik Merkezi'nde koruyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a609a-145">You can protect multiple web applications in Security Center by adding these applications tooyour existing WAF deployments.</span></span>
>
>

<span data-ttu-id="a609a-146">Bu WAF Hello günlüklerinden artık tam olarak tümleşiktir.</span><span class="sxs-lookup"><span data-stu-id="a609a-146">hello logs from that WAF are now fully integrated.</span></span> <span data-ttu-id="a609a-147">Güvenlik Merkezi otomatik olarak toplamak ve böylece bu önemli güvenlik uyarıları tooyou yüzey hello günlüklerini analiz başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a609a-147">Security Center can start automatically gathering and analyzing hello logs so that it can surface important security alerts tooyou.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a609a-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a609a-148">Next steps</span></span>
<span data-ttu-id="a609a-149">Bu belge size nasıl tooimplement hello Güvenlik Merkezi öneri "Ekleme bir web uygulaması." gösterdi.</span><span class="sxs-lookup"><span data-stu-id="a609a-149">This document showed you how tooimplement hello Security Center recommendation "Add a web application."</span></span> <span data-ttu-id="a609a-150">bir web uygulaması güvenlik duvarı yapılandırma hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="a609a-150">toolearn more about configuring a web application firewall, see hello following:</span></span>

* [<span data-ttu-id="a609a-151">Bir Web uygulaması Güvenlik Duvarı (WAF) için uygulama hizmeti ortamını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a609a-151">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>](../app-service-web/app-service-app-service-environment-web-application-firewall.md)

<span data-ttu-id="a609a-152">Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="a609a-152">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="a609a-153">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="a609a-153">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="a609a-154">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) --nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="a609a-154">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="a609a-155">[Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) --öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.</span><span class="sxs-lookup"><span data-stu-id="a609a-155">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="a609a-156">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="a609a-156">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="a609a-157">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) --hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a609a-157">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="a609a-158">[Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) --Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a609a-158">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-add-web-application-firewall/secure-web-application.png
[2]:./media/security-center-add-web-application-firewall/add-a-waf.png
[3]: ./media/security-center-add-web-application-firewall/info-blade.png
[4]: ./media/security-center-add-web-application-firewall/select-vm-config.png
[5]: ./media/security-center-add-web-application-firewall/finalize-waf.png
[6]: ./media/security-center-add-web-application-firewall/restrict-traffic.png
