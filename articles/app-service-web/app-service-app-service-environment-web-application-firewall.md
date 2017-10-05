---
title: "Bir Web uygulaması Güvenlik Duvarı (WAF) için uygulama hizmeti ortamını yapılandırma"
description: "Uygulama hizmeti ortamınızı önünde bir web uygulaması güvenlik duvarı yapılandırmayı öğrenin."
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
ms.openlocfilehash: 3e9e9fa4ddab60a467e8aa793ec0ca269b0bc4e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a><span data-ttu-id="4e0a5-103">Bir Web uygulaması Güvenlik Duvarı (WAF) için uygulama hizmeti ortamını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4e0a5-103">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="4e0a5-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="4e0a5-104">Overview</span></span>
<span data-ttu-id="4e0a5-105">Web uygulaması güvenlik duvarı ister [Barracuda WAF Azure](https://www.barracuda.com/programs/azure) üzerinde kullanılabilir [Azure Marketi](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) güvenli SQL eklemelerini, siteler arası komut dosyası, kötü amaçlı yazılım yüklemeleri engellemek için gelen web trafiği incelemek tarafından web uygulamalarınızın & uygulama DDoS ve diğer saldırılara yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-105">Web application firewalls like the [Barracuda WAF for Azure](https://www.barracuda.com/programs/azure) that is available on the [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) helps secure your web applications by inspecting inbound web traffic to block SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks.</span></span> <span data-ttu-id="4e0a5-106">Ayrıca arka uç web sunucularından yanıtları veri kaybını önleme (DLP) inceler.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-106">It also inspects the responses from the back-end web servers for Data Loss Prevention (DLP).</span></span> <span data-ttu-id="4e0a5-107">Yalıtım ve App Service ortamları tarafından sağlanan ek ölçeklendirme birlikte, bu kötü amaçlı istekleri ve yüksek hacimli trafik dayanacak gereken iş kritik web uygulamalarını barındırmasını ideal bir ortam sağlar.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-107">Combined with the isolation and additional scaling provided by App Service Environments, this provides an ideal environment to host business critical web applications that need to withstand malicious requests and high volume traffic.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a><span data-ttu-id="4e0a5-108">Kurulum</span><span class="sxs-lookup"><span data-stu-id="4e0a5-108">Setup</span></span>
<span data-ttu-id="4e0a5-109">Biz yapılandırmak için bu belgenin böylece yalnızca WAF gelen trafiği uygulama hizmeti ortamı erişebilir ve çevre ağından erişilebilir olmaz Barracuda WAF örneklerini bizim uygulama hizmeti ortamı arkasında birden fazla yük dengeli.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-109">For this document we will configure our App Service Environment behind multiple load balanced instances of Barracuda WAF so that only traffic from the WAF can reach the App Service Environment and it will not be accessible from the DMZ.</span></span> <span data-ttu-id="4e0a5-110">Biz de Azure Traffic Manager Azure veri merkezlerinde ve bölgeler arasında yük dengelemesi için bizim Barracuda WAF örnekler önünde sahip olur.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-110">We will also have Azure Traffic Manager in front of our Barracuda WAF instances to load balance across Azure data centers and regions.</span></span> <span data-ttu-id="4e0a5-111">Kurulum üst düzey bir diyagramını ne aşağıda gösterilen gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-111">A high level diagram of the setup would look like what is shown below.</span></span>

![Mimari][Architecture] 

> <span data-ttu-id="4e0a5-113">Not: girişiyle [ILB desteklemek için uygulama hizmeti ortamı](app-service-environment-with-internal-load-balancer.md), çevre ağından erişilemeyen ve yalnızca özel ağa kullanılabilir olması için ana yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-113">Note: With the introduction of [ILB support for App Service Environment](app-service-environment-with-internal-load-balancer.md), you can configure the ASE to be inaccessible from the DMZ and only be available to the private network.</span></span> 
> 
> 

## <a name="configuring-your-app-service-environment"></a><span data-ttu-id="4e0a5-114">Uygulama hizmeti ortamınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4e0a5-114">Configuring your App Service Environment</span></span>
<span data-ttu-id="4e0a5-115">Bir uygulama hizmeti ortamı yapılandırmak için de başvurabilirsiniz [Belgelerimizi](app-service-web-how-to-create-an-app-service-environment.md) konu hakkında.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-115">To configure an App Service Environment refer to [our documentation](app-service-web-how-to-create-an-app-service-environment.md) on the subject.</span></span> <span data-ttu-id="4e0a5-116">Oluşturulan bir uygulama hizmeti ortamı olduktan sonra oluşturabileceğiniz [Web Apps](app-service-web-overview.md), [API uygulamaları](../app-service-api/app-service-api-apps-why-best-platform.md) ve [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) Bu ortamdaki tüm biz yapılandırmak bir sonraki bölümde WAF arkasında korunur.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-116">Once you have an App Service Environment created, you can create [Web Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) in this environment that will all be protected behind the WAF we configure in the next section.</span></span>

## <a name="configuring-your-barracuda-waf-cloud-service"></a><span data-ttu-id="4e0a5-117">Barracuda WAF bulut hizmetini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4e0a5-117">Configuring your Barracuda WAF Cloud Service</span></span>
<span data-ttu-id="4e0a5-118">Barracuda sahip bir [ayrıntılı makale](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) kendi WAF azure'da bir sanal makinede dağıtma.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-118">Barracuda has a [detailed article](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) on deploying its WAF on a virtual machine in Azure.</span></span> <span data-ttu-id="4e0a5-119">Ancak bu yönergeleri izleyerek, aynı bulut hizmetine en az 2 WAF örneği VM dağıtmak istediğiniz artıklık istediğiniz ve tek hata noktası tanıtmak değil çünkü.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-119">But because we want redundancy and not introduce a single point of failure, you want to deploy at least 2 WAF instance VMs into the same Cloud Service when following these instructions.</span></span>

### <a name="adding-endpoints-to-cloud-service"></a><span data-ttu-id="4e0a5-120">Bulut hizmeti için uç noktaları ekleme</span><span class="sxs-lookup"><span data-stu-id="4e0a5-120">Adding Endpoints to Cloud Service</span></span>
<span data-ttu-id="4e0a5-121">2 veya daha fazla WAF VM bulut hizmetiniz örnekleri sonra kullanabileceğiniz [Azure portal](https://portal.azure.com/) aşağıdaki resimde gösterildiği gibi uygulamanız tarafından kullanılan HTTP ve HTTPS uç noktalarını eklemek için.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-121">Once you have 2 or more WAF VM instances in your Cloud Service you can use the [Azure portal](https://portal.azure.com/) to add HTTP and HTTPS endpoints that are used by your application as shown in the image below.</span></span>

![Uç noktasını yapılandırma][ConfigureEndpoint]

<span data-ttu-id="4e0a5-123">Uygulamalarınız diğer uç noktaları kullanıyorsa, bu da bu listeye eklemek emin olun.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-123">If your applications use other endpoints, make sure to add those to this list as well.</span></span> 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a><span data-ttu-id="4e0a5-124">Barracuda WAF kendi Yönetim Portalı üzerinden yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4e0a5-124">Configuring Barracuda WAF through its Management Portal</span></span>
<span data-ttu-id="4e0a5-125">Barracuda WAF TCP bağlantı noktası 8000 kendi Yönetim Portalı aracılığıyla yapılandırması için kullanır.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-125">Barracuda WAF uses TCP Port 8000 for configuration through its management portal.</span></span> <span data-ttu-id="4e0a5-126">Biz WAF VM'ler birden çok örneğini olduğundan adımlar burada her bir VM örneği için yinelemeniz gerekecek.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-126">Since we have multiple instances of the WAF VMs you will need to repeat the steps here for each VM instance.</span></span> 

> <span data-ttu-id="4e0a5-127">Not: WAF yapılandırmayla tamamladıktan sonra tüm WAF, WAF güvenli tutmak için Vm'leriniz TCP/8000 endpoint kaldırın.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-127">Note: Once you are done with WAF configuration, remove the TCP/8000 endpoint from all your WAF VMs to keep your WAF secure.</span></span>
> 
> 

<span data-ttu-id="4e0a5-128">Yönetim uç nokta Barracuda WAF yapılandırmak için aşağıdaki resimde gösterildiği gibi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-128">Add the management endpoint as shown in the image below to configure your Barracuda WAF.</span></span>

![Yönetim uç nokta ekleyin][AddManagementEndpoint]

<span data-ttu-id="4e0a5-130">Bulut hizmetinizi yönetim noktadaki gözatmak için bir tarayıcı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-130">Use a browser to browse to the management endpoint on your Cloud Service.</span></span> <span data-ttu-id="4e0a5-131">Bulut hizmetinizi test.cloudapp.net çağrılırsa, bu uç nokta için http://test.cloudapp.net:8000 göz atarak erişir.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-131">If your Cloud Service is called test.cloudapp.net, you would access this endpoint by browsing to http://test.cloudapp.net:8000.</span></span> <span data-ttu-id="4e0a5-132">Bir oturum açma sayfası görmelisiniz aşağıdaki gibi WAF VM kurulumu aşamasında belirtilen kimlik bilgilerini kullanarak oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-132">You should see a login page like below that you can login using credentials you specified in the WAF VM setup phase.</span></span>

![Yönetim oturum açma sayfası][ManagementLoginPage]

<span data-ttu-id="4e0a5-134">Bir kez, oturum açma WAF koruma hakkında temel istatistikleri sunacaktır aşağıdaki görüntü birinde olarak bir Pano görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-134">Once you login you should see a dashboard as the one in the image below that will present basic statistics about the WAF protection.</span></span>

![Yönetim Panosu][ManagementDashboard]

<span data-ttu-id="4e0a5-136">Hizmetler sekmesinde tıklatarak, sizin WAF koruduğu hizmetler için yapılandırma olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-136">Clicking on the Services tab will let you configure your WAF for services it is protecting.</span></span> <span data-ttu-id="4e0a5-137">Barracuda WAF yapılandırma hakkında daha fazla ayrıntı için başvurabilirsiniz [kendi belgelerine](https://techlib.barracuda.com/waf/getstarted1).</span><span class="sxs-lookup"><span data-stu-id="4e0a5-137">For more details on configuring your Barracuda WAF you can consult [their documentation](https://techlib.barracuda.com/waf/getstarted1).</span></span> <span data-ttu-id="4e0a5-138">Bir Azure Web uygulaması aşağıdaki örnekte HTTP ve HTTPS trafiğini hizmet veren yapılandırıldı.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-138">In the example below an Azure Web App serving traffic on HTTP and HTTPS has been configured.</span></span>

![Yönetim Hizmetleri Ekle][ManagementAddServices]

> <span data-ttu-id="4e0a5-140">Not: uygulamalarınızı nasıl yapılandırılır ve hangi özelliklerin uygulama hizmeti ortamı'nda kullanıldığını bağlı olarak, örneğin, 80 ve 443 dışındaki bağlantı noktaları trafiği için TCP iletmek gerekir, bir Web uygulaması için IP SSL Kurulum varsa.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-140">Note: Depending on how your applications are configured and what features are being used in your App Service Environment, you will need to forward traffic for TCP ports other than 80 and 443, e.g. if you have IP SSL setup for a Web App.</span></span> <span data-ttu-id="4e0a5-141">Uygulama hizmeti ortamlarında kullanılan ağ bağlantı noktalarının listesi için lütfen bakın [denetim gelen trafiği belgelerine'nın](app-service-app-service-environment-control-inbound-traffic.md) ağ bağlantı noktaları bölümü.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-141">For a list of network ports used in App Service Environments, please refer to [Control Inbound Traffic documentation's](app-service-app-service-environment-control-inbound-traffic.md) Network Ports section.</span></span>
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a><span data-ttu-id="4e0a5-142">Microsoft Azure trafik Yöneticisi (isteğe bağlı) yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4e0a5-142">Configuring Microsoft Azure Traffic Manager (OPTIONAL)</span></span>
<span data-ttu-id="4e0a5-143">Yüklemek istediğiniz uygulamanız birden çok bölgede kullanılabilir ise arkasına Bakiye [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4e0a5-143">If your application is available in multiple regions, then you would want to load balance them behind [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span></span> <span data-ttu-id="4e0a5-144">Bir uç nokta olarak ekleyebilirsiniz Bunu yapmak için [Klasik Azure portalı](https://manage.azure.com) aşağıdaki resimde gösterildiği gibi WAF için bulut hizmeti adı trafik Yöneticisi profili kullanarak.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-144">To do so you can add an endpoint in the [Azure classic portal](https://manage.azure.com) using the Cloud Service name for your WAF in the Traffic Manager profile as shown in the image below.</span></span> 

![Trafik Yöneticisi uç noktası][TrafficManagerEndpoint]

<span data-ttu-id="4e0a5-146">Uygulamanızın kimlik doğrulaması gerektiriyorsa, herhangi bir kimlik doğrulaması ping işlemi yapmak için trafik Yöneticisi'için uygulamanızın kullanılabilirlik için gerektirmeyen bazı kaynak olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-146">If your application requires authentication, ensure you have some resource that doesn't require any authentication for Traffic Manager to ping for the availability of your application.</span></span> <span data-ttu-id="4e0a5-147">URL Yapılandır bölümünde yapılandırabilirsiniz [Klasik Azure portalı](https://manage.azure.com) aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-147">You can configure the URL under the Configure section on the [Azure classic portal](https://manage.azure.com) as shown below.</span></span>

![Traffic Manager'ı yapılandırma][ConfigureTrafficManager]

<span data-ttu-id="4e0a5-149">Trafik Yöneticisi ping uygulamanıza, WAF iletmek için Kurulum Web sitesi Çevirileri, Barracuda WAF aşağıdaki örnekte gösterildiği gibi uygulamanız için trafiği iletmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-149">To forward the Traffic Manager pings from your WAF to your application, you need to setup Website Translations on your Barracuda WAF to forward traffic to your application as shown in the example below.</span></span>

![Web sitesi çevirileri][WebsiteTranslations]

## <a name="securing-traffic-to-app-service-environment-using-network-security-groups-nsg"></a><span data-ttu-id="4e0a5-151">Ağ güvenlik grupları (NSG) kullanarak uygulama hizmeti ortamı için trafiğinin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="4e0a5-151">Securing Traffic to App Service Environment Using Network Security Groups (NSG)</span></span>
<span data-ttu-id="4e0a5-152">İzleyin [denetim gelen trafiği belgelerine](app-service-app-service-environment-control-inbound-traffic.md) trafiği yalnızca bulut hizmetinizin VIP adresi kullanarak uygulama hizmeti ortamınızı WAF kısıtlama hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-152">Follow the [Control Inbound Traffic documentation](app-service-app-service-environment-control-inbound-traffic.md) for details on restricting traffic to your App Service Environment from the WAF only by using the VIP address of your Cloud Service.</span></span> <span data-ttu-id="4e0a5-153">Burada, TCP bağlantı noktası 80 bu görevi gerçekleştirmek için bir örnek Powershell komut verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-153">Here's a sample Powershell command for performing this task for TCP port 80.</span></span>

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

<span data-ttu-id="4e0a5-154">SourceAddressPrefix WAF'ın bulut hizmeti ile sanal IP adresi (VIP) değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-154">Replace the SourceAddressPrefix with the Virtual IP Address (VIP) of your WAF's Cloud Service.</span></span>

> <span data-ttu-id="4e0a5-155">Not: silin ve bulut hizmeti yeniden oluştururken, bulut hizmetinizin VIP değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-155">Note: The VIP of your Cloud Service will change when you delete and re-create the Cloud Service.</span></span> <span data-ttu-id="4e0a5-156">Bunu yaptıktan sonra IP adresi ağ kaynak grubunda güncelleştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="4e0a5-156">Make sure to update the IP address in the Network Resource group once you do so.</span></span> 
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
