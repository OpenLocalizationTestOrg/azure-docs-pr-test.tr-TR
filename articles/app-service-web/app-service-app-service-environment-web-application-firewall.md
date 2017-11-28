---
title: "aaaConfiguring uygulama hizmeti ortamı bir Web uygulaması Güvenlik Duvarı (WAF)"
description: "Tooconfigure bir web uygulaması uygulama hizmeti ortamınızı önünde nasıl Güvenlik Duvarı hakkında bilgi edinin."
services: app-service\web
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: a2101291-83ba-4169-98a2-2c0ed9a65e8d
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: naziml
ms.openlocfilehash: 0fcf62aea871751c9d4f294d2d24df2186fc0e7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a><span data-ttu-id="0eab6-103">Bir Web uygulaması Güvenlik Duvarı (WAF) için uygulama hizmeti ortamını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0eab6-103">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="0eab6-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="0eab6-104">Overview</span></span>
<span data-ttu-id="0eab6-105">Web uygulaması güvenlik duvarı hello gibi [Barracuda WAF Azure](https://www.barracuda.com/programs/azure) hello üzerinde kullanılabilir [Azure Marketi](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) yardımcı olur, gelen web trafiği tooblock SQL inceleyerek, web uygulamalarınızı güvenli eklemelerini, siteler arası komut dosyası, kötü amaçlı yazılım yüklemeleri ve uygulama DDoS ve diğer saldırılara.</span><span class="sxs-lookup"><span data-stu-id="0eab6-105">Web application firewalls like hello [Barracuda WAF for Azure](https://www.barracuda.com/programs/azure) that is available on hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) helps secure your web applications by inspecting inbound web traffic tooblock SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks.</span></span> <span data-ttu-id="0eab6-106">Ayrıca hello yanıtları hello arka uç web sunucularından veri kaybını önleme (DLP) inceler.</span><span class="sxs-lookup"><span data-stu-id="0eab6-106">It also inspects hello responses from hello back-end web servers for Data Loss Prevention (DLP).</span></span> <span data-ttu-id="0eab6-107">Merhaba yalıtım ve App Service ortamları tarafından sağlanan ek ölçeklendirme birlikte, bu toowithstand kötü amaçlı istekleri ve yüksek hacimli trafik gerek toohost iş kritik web uygulamaları ideal bir ortam sağlar.</span><span class="sxs-lookup"><span data-stu-id="0eab6-107">Combined with hello isolation and additional scaling provided by App Service Environments, this provides an ideal environment toohost business critical web applications that need toowithstand malicious requests and high volume traffic.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a><span data-ttu-id="0eab6-108">Kurulum</span><span class="sxs-lookup"><span data-stu-id="0eab6-108">Setup</span></span>
<span data-ttu-id="0eab6-109">Biz yapılandırmak için bu belgenin böylece yalnızca hello WAF gelen trafiği hello uygulama hizmeti ortamı erişebilir ve DMZ hello erişilebilir olmaz Barracuda WAF örneklerini bizim uygulama hizmeti ortamı arkasında birden fazla yük dengeli.</span><span class="sxs-lookup"><span data-stu-id="0eab6-109">For this document we will configure our App Service Environment behind multiple load balanced instances of Barracuda WAF so that only traffic from hello WAF can reach hello App Service Environment and it will not be accessible from hello DMZ.</span></span> <span data-ttu-id="0eab6-110">Azure veri merkezlerinde ve bölgeler arasında biz de bizim Barracuda WAF örnekleri tooload Bakiye önünde Azure Traffic Manager gerekir.</span><span class="sxs-lookup"><span data-stu-id="0eab6-110">We will also have Azure Traffic Manager in front of our Barracuda WAF instances tooload balance across Azure data centers and regions.</span></span> <span data-ttu-id="0eab6-111">Merhaba Kurulum üst düzey bir diyagramını ne aşağıda gösterilen gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="0eab6-111">A high level diagram of hello setup would look like what is shown below.</span></span>

![Mimari][Architecture] 

> <span data-ttu-id="0eab6-113">Not: ile Merhaba giriş [ILB desteklemek için uygulama hizmeti ortamı](app-service-environment-with-internal-load-balancer.md), hello ana toobe DMZ hello erişilemez yapılandırabilir ve yalnızca kullanılabilir toohello özel ağ olabilir.</span><span class="sxs-lookup"><span data-stu-id="0eab6-113">Note: With hello introduction of [ILB support for App Service Environment](app-service-environment-with-internal-load-balancer.md), you can configure hello ASE toobe inaccessible from hello DMZ and only be available toohello private network.</span></span> 
> 
> 

## <a name="configuring-your-app-service-environment"></a><span data-ttu-id="0eab6-114">Uygulama hizmeti ortamınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0eab6-114">Configuring your App Service Environment</span></span>
<span data-ttu-id="0eab6-115">bir uygulama hizmeti ortamı tooconfigure başvurmak çok[Belgelerimizi](app-service-web-how-to-create-an-app-service-environment.md) hello konu üzerinde.</span><span class="sxs-lookup"><span data-stu-id="0eab6-115">tooconfigure an App Service Environment refer too[our documentation](app-service-web-how-to-create-an-app-service-environment.md) on hello subject.</span></span> <span data-ttu-id="0eab6-116">Oluşturulan bir uygulama hizmeti ortamı olduktan sonra oluşturabileceğiniz [Web Apps](app-service-web-overview.md), [API uygulamaları](../app-service-api/app-service-api-apps-why-best-platform.md) ve [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) Bu ortamdaki tüm hello WAF korunur biz Merhaba sonraki bölümde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0eab6-116">Once you have an App Service Environment created, you can create [Web Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) in this environment that will all be protected behind hello WAF we configure in hello next section.</span></span>

## <a name="configuring-your-barracuda-waf-cloud-service"></a><span data-ttu-id="0eab6-117">Barracuda WAF bulut hizmetini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0eab6-117">Configuring your Barracuda WAF Cloud Service</span></span>
<span data-ttu-id="0eab6-118">Barracuda sahip bir [ayrıntılı makale](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) kendi WAF azure'da bir sanal makinede dağıtma.</span><span class="sxs-lookup"><span data-stu-id="0eab6-118">Barracuda has a [detailed article](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) on deploying its WAF on a virtual machine in Azure.</span></span> <span data-ttu-id="0eab6-119">Ancak biz artıklık istediğiniz ve tek hata noktası tanıtmak değil çünkü toodeploy en az 2 WAF örneğine VM'ler hello istediğiniz aynı bulut bu yönergeleri izleyerek hizmet.</span><span class="sxs-lookup"><span data-stu-id="0eab6-119">But because we want redundancy and not introduce a single point of failure, you want toodeploy at least 2 WAF instance VMs into hello same Cloud Service when following these instructions.</span></span>

### <a name="adding-endpoints-toocloud-service"></a><span data-ttu-id="0eab6-120">Uç noktaları tooCloud hizmet ekleme</span><span class="sxs-lookup"><span data-stu-id="0eab6-120">Adding Endpoints tooCloud Service</span></span>
<span data-ttu-id="0eab6-121">2 veya daha fazla WAF VM bulut hizmetiniz örnekleri sonra hello kullanarak [Azure portal](https://portal.azure.com/) hello resimde gösterildiği gibi uygulamanız tarafından kullanılan tooadd HTTP ve HTTPS uç noktaları.</span><span class="sxs-lookup"><span data-stu-id="0eab6-121">Once you have 2 or more WAF VM instances in your Cloud Service you can use hello [Azure portal](https://portal.azure.com/) tooadd HTTP and HTTPS endpoints that are used by your application as shown in hello image below.</span></span>

![Uç noktasını yapılandırma][ConfigureEndpoint]

<span data-ttu-id="0eab6-123">Uygulamalarınız diğer uç noktaları kullanıyorsa, bu toothis listesi de emin tooadd olun.</span><span class="sxs-lookup"><span data-stu-id="0eab6-123">If your applications use other endpoints, make sure tooadd those toothis list as well.</span></span> 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a><span data-ttu-id="0eab6-124">Barracuda WAF kendi Yönetim Portalı üzerinden yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0eab6-124">Configuring Barracuda WAF through its Management Portal</span></span>
<span data-ttu-id="0eab6-125">Barracuda WAF TCP bağlantı noktası 8000 kendi Yönetim Portalı aracılığıyla yapılandırması için kullanır.</span><span class="sxs-lookup"><span data-stu-id="0eab6-125">Barracuda WAF uses TCP Port 8000 for configuration through its management portal.</span></span> <span data-ttu-id="0eab6-126">Merhaba WAF VM'ler birden çok örneğini sahibiz bu yana her bir VM örneği için burada toorepeat hello adımları gerekir.</span><span class="sxs-lookup"><span data-stu-id="0eab6-126">Since we have multiple instances of hello WAF VMs you will need toorepeat hello steps here for each VM instance.</span></span> 

> <span data-ttu-id="0eab6-127">Not: WAF yapılandırmayla tamamladıktan sonra hello TCP/8000 uç noktası, tüm WAF VM'ler tookeep güvenli, WAF kaldırın.</span><span class="sxs-lookup"><span data-stu-id="0eab6-127">Note: Once you are done with WAF configuration, remove hello TCP/8000 endpoint from all your WAF VMs tookeep your WAF secure.</span></span>
> 
> 

<span data-ttu-id="0eab6-128">Barracuda WAF hello görüntü tooconfigure aşağıda gösterildiği gibi hello yönetim uç noktası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0eab6-128">Add hello management endpoint as shown in hello image below tooconfigure your Barracuda WAF.</span></span>

![Yönetim uç nokta ekleyin][AddManagementEndpoint]

<span data-ttu-id="0eab6-130">Bir tarayıcı toobrowse toohello yönetim uç bulut hizmetinizde kullanın.</span><span class="sxs-lookup"><span data-stu-id="0eab6-130">Use a browser toobrowse toohello management endpoint on your Cloud Service.</span></span> <span data-ttu-id="0eab6-131">Bulut hizmetinizi test.cloudapp.net çağrılırsa, bu uç noktaya toohttp://test.cloudapp.net:8000 göz atarak erişir.</span><span class="sxs-lookup"><span data-stu-id="0eab6-131">If your Cloud Service is called test.cloudapp.net, you would access this endpoint by browsing toohttp://test.cloudapp.net:8000.</span></span> <span data-ttu-id="0eab6-132">Bir oturum açma sayfası görmelisiniz aşağıdaki gibi hello WAF VM kurulumu aşamasında belirtilen kimlik bilgilerini kullanarak oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="0eab6-132">You should see a login page like below that you can login using credentials you specified in hello WAF VM setup phase.</span></span>

![Yönetim oturum açma sayfası][ManagementLoginPage]

<span data-ttu-id="0eab6-134">Bir kez hello bir Pano görürsünüz, oturum açma hello görüntü aşağıdan birinde hello WAF koruma hakkında temel istatistikleri sunacaktır.</span><span class="sxs-lookup"><span data-stu-id="0eab6-134">Once you login you should see a dashboard as hello one in hello image below that will present basic statistics about hello WAF protection.</span></span>

![Yönetim Panosu][ManagementDashboard]

<span data-ttu-id="0eab6-136">Merhaba Hizmetleri sekmesini tıklatarak, sizin WAF koruduğu hizmetler için yapılandırma olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="0eab6-136">Clicking on hello Services tab will let you configure your WAF for services it is protecting.</span></span> <span data-ttu-id="0eab6-137">Barracuda WAF yapılandırma hakkında daha fazla ayrıntı için başvurabilirsiniz [kendi belgelerine](https://techlib.barracuda.com/waf/getstarted1).</span><span class="sxs-lookup"><span data-stu-id="0eab6-137">For more details on configuring your Barracuda WAF you can consult [their documentation](https://techlib.barracuda.com/waf/getstarted1).</span></span> <span data-ttu-id="0eab6-138">Bir Azure Web uygulaması aşağıda hello örnekte HTTP ve HTTPS trafiğini hizmet veren yapılandırıldı.</span><span class="sxs-lookup"><span data-stu-id="0eab6-138">In hello example below an Azure Web App serving traffic on HTTP and HTTPS has been configured.</span></span>

![Yönetim Hizmetleri Ekle][ManagementAddServices]

> <span data-ttu-id="0eab6-140">Not: uygulamalarınızı nasıl yapılandırılır ve hangi özelliklerin uygulama hizmeti ortamı'nda kullanıldığını bağlı olarak, tooforward trafiği 80 ve 443 dışındaki TCP bağlantı noktaları için örneğin gerekir bir Web uygulaması için IP SSL Kurulum varsa.</span><span class="sxs-lookup"><span data-stu-id="0eab6-140">Note: Depending on how your applications are configured and what features are being used in your App Service Environment, you will need tooforward traffic for TCP ports other than 80 and 443, e.g. if you have IP SSL setup for a Web App.</span></span> <span data-ttu-id="0eab6-141">Uygulama hizmeti ortamlarında kullanılan ağ bağlantı noktalarının listesi için lütfen çok bakın[denetim gelen trafiği belgelerine'nın](app-service-app-service-environment-control-inbound-traffic.md) ağ bağlantı noktaları bölümü.</span><span class="sxs-lookup"><span data-stu-id="0eab6-141">For a list of network ports used in App Service Environments, please refer too[Control Inbound Traffic documentation's](app-service-app-service-environment-control-inbound-traffic.md) Network Ports section.</span></span>
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a><span data-ttu-id="0eab6-142">Microsoft Azure trafik Yöneticisi (isteğe bağlı) yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0eab6-142">Configuring Microsoft Azure Traffic Manager (OPTIONAL)</span></span>
<span data-ttu-id="0eab6-143">Uygulamanız birden çok bölgede kullanılabilir sonra tooload Bakiye istersiniz arkasında bunları [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0eab6-143">If your application is available in multiple regions, then you would want tooload balance them behind [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span></span> <span data-ttu-id="0eab6-144">bir uç nokta hello ekleyebilmek toodo [Klasik Azure portalı](https://manage.azure.com) hello resimde gösterildiği gibi hello trafik Yöneticisi profili, WAF hello bulut hizmeti adını kullanarak.</span><span class="sxs-lookup"><span data-stu-id="0eab6-144">toodo so you can add an endpoint in hello [Azure classic portal](https://manage.azure.com) using hello Cloud Service name for your WAF in hello Traffic Manager profile as shown in hello image below.</span></span> 

![Trafik Yöneticisi uç noktası][TrafficManagerEndpoint]

<span data-ttu-id="0eab6-146">Uygulamanızın kimlik doğrulaması gerektiriyorsa, trafik Yöneticisi tooping uygulamanızın hello kullanılabilirlik için herhangi bir kimlik doğrulaması gerektirmeyen bazı kaynak olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="0eab6-146">If your application requires authentication, ensure you have some resource that doesn't require any authentication for Traffic Manager tooping for hello availability of your application.</span></span> <span data-ttu-id="0eab6-147">Merhaba üzerinde hello URL hello yapılandırma bölümüne altında yapılandırabilirsiniz [Klasik Azure portalı](https://manage.azure.com) aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="0eab6-147">You can configure hello URL under hello Configure section on hello [Azure classic portal](https://manage.azure.com) as shown below.</span></span>

![Traffic Manager'ı yapılandırma][ConfigureTrafficManager]

<span data-ttu-id="0eab6-149">tooforward hello trafik Yöneticisi ping WAF tooyour uygulamanızdan toosetup Web sitesi çevirileri hello aşağıdaki örnekte gösterildiği gibi Barracuda WAF tooforward trafiği tooyour uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0eab6-149">tooforward hello Traffic Manager pings from your WAF tooyour application, you need toosetup Website Translations on your Barracuda WAF tooforward traffic tooyour application as shown in hello example below.</span></span>

![Web sitesi çevirileri][WebsiteTranslations]

## <a name="securing-traffic-tooapp-service-environment-using-network-security-groups-nsg"></a><span data-ttu-id="0eab6-151">Trafik tooApp hizmet ortamı kullanarak ağ güvenlik grupları (NSG) güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="0eab6-151">Securing Traffic tooApp Service Environment Using Network Security Groups (NSG)</span></span>
<span data-ttu-id="0eab6-152">Merhaba izleyin [denetim gelen trafiği belgelerine](app-service-app-service-environment-control-inbound-traffic.md) yalnızca bulut hizmetinizin hello VIP adresi kullanarak kısıtlama Ayrıntılar tooyour uygulama hizmeti ortamı hello WAF gelen trafik için.</span><span class="sxs-lookup"><span data-stu-id="0eab6-152">Follow hello [Control Inbound Traffic documentation](app-service-app-service-environment-control-inbound-traffic.md) for details on restricting traffic tooyour App Service Environment from hello WAF only by using hello VIP address of your Cloud Service.</span></span> <span data-ttu-id="0eab6-153">Burada, TCP bağlantı noktası 80 bu görevi gerçekleştirmek için bir örnek Powershell komut verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0eab6-153">Here's a sample Powershell command for performing this task for TCP port 80.</span></span>

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

<span data-ttu-id="0eab6-154">Merhaba SourceAddressPrefix hello WAF's bulut hizmetinin sanal IP adresi (VIP) ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0eab6-154">Replace hello SourceAddressPrefix with hello Virtual IP Address (VIP) of your WAF's Cloud Service.</span></span>

> <span data-ttu-id="0eab6-155">Not: silin ve hello bulut hizmeti yeniden oluştururken hello VIP bulut hizmetinizin değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0eab6-155">Note: hello VIP of your Cloud Service will change when you delete and re-create hello Cloud Service.</span></span> <span data-ttu-id="0eab6-156">Yapma emin tooupdate başlangıç IP adresi Bunu yaptıktan sonra hello ağ kaynak grubunda.</span><span class="sxs-lookup"><span data-stu-id="0eab6-156">Make sure tooupdate hello IP address in hello Network Resource group once you do so.</span></span> 
> 
> 

<!-- IMAGES -->
[Architecture]: ./media/app-service-app-service-environment-web-application-firewall/Architecture.png
[ConfigureEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureEndpoint.png
[AddManagementEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/AddManagementEndpoint.png
[ManagementAddServices]: ./media/app-service-app-service-environment-web-application-firewall/ManagementAddServices.png
[ManagementDashboard]: ./media/app-service-app-service-environment-web-application-firewall/ManagementDashboard.png
[ManagementLoginPage]: ./media/app-service-app-service-environment-web-application-firewall/ManagementLoginPage.png
[TrafficManagerEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/TrafficManagerEndpoint.png
[ConfigureTrafficManager]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureTrafficManager.png
[WebsiteTranslations]: ./media/app-service-app-service-environment-web-application-firewall/WebsiteTranslations.png
