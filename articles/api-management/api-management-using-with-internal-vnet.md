---
title: "İç sanal ağ ile aaaHow toouse Azure API Management | Microsoft Docs"
description: "Bilgi nasıl toosetup ve iç sanal ağında Azure API Management yapılandırın."
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: 
ms.assetid: dac28ccf-2550-45a5-89cf-192d87369bc3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 8d25de14e0c0bebe7ba7b47ca432ea4e45dde312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a><span data-ttu-id="e7bdb-103">Azure API Management hizmeti iç sanal ağ ile kullanma</span><span class="sxs-lookup"><span data-stu-id="e7bdb-103">Using Azure API Management service with Internal Virtual Network</span></span>
<span data-ttu-id="e7bdb-104">Azure sanal ağlar (Vnet'ler), API Management API'leri hello Internet üzerinde erişilebilir yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-104">With Azure Virtual Networks (VNETs), API Management can manage APIs not accessible on hello Internet.</span></span> <span data-ttu-id="e7bdb-105">VPN teknolojileri çeşitli kullanılabilir toomake hello bağlantısı olan ve API Management hello VNET içindeki iki ana modu dağıtılabilir:</span><span class="sxs-lookup"><span data-stu-id="e7bdb-105">A number of VPN technologies are available toomake hello connection and API Management can be deployed in two main modes inside hello VNET:</span></span>
* <span data-ttu-id="e7bdb-106">Dış</span><span class="sxs-lookup"><span data-stu-id="e7bdb-106">External</span></span>
* <span data-ttu-id="e7bdb-107">İç</span><span class="sxs-lookup"><span data-stu-id="e7bdb-107">Internal</span></span>

## <span data-ttu-id="e7bdb-108"><a name="overview"> </a>Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="e7bdb-108"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="e7bdb-109">API Management bir iç sanal ağ modunda dağıtıldığında, tüm hello hizmet uç noktaları (ağ geçidi, Geliştirici Portalı, yayımcı portalında, doğrudan yönetim ve Git) yalnızca erişimini denetleyen bir sanal ağ içinde görünür.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-109">When API Management is deployed in an Internal Virtual network mode, all hello service endpoints (gateway, developer portal, publisher portal, direct management and Git) are only visible inside a Virtual network that you control access to.</span></span> <span data-ttu-id="e7bdb-110">Merhaba hizmet uç noktaları hiçbiri hello ortak DNS sunucusu üzerinde kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-110">None of hello service endpoints are registered on hello Public DNS Server.</span></span>

<span data-ttu-id="e7bdb-111">İç modunda API Yönetimi'ni kullanarak aşağıdaki senaryolar hello elde edebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e7bdb-111">Using API Management in Internal mode, you can achieve hello following scenarios</span></span>
* <span data-ttu-id="e7bdb-112">Güvenli bir şekilde, özel veri merkezinizde erişilebilir siteden siteye veya ExpressRoute VPN bağlantıları kullanarak dışında 3. taraflar tarafından barındırılan API'ler olun.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-112">Securely make APIs hosted in your private datacenter accessible by 3rd parties outside of it using Site-to-Site or ExpressRoute VPN connections.</span></span>
* <span data-ttu-id="e7bdb-113">Karma bulut senaryolarında, bulut tabanlı API'ler ve ortak ağ geçidi üzerinden şirket içi API'leri göstererek etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-113">Enable hybrid cloud scenarios by exposing your cloud-based APIs and on-prem APIs through a common gateway.</span></span>
* <span data-ttu-id="e7bdb-114">Tek bir ağ geçidi uç noktası kullanarak birden çok coğrafi konumda barındırılan Apı'lerinizi yönetin.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-114">Manage your APIs hosted in multiple geographic locations using a single Gateway endpoint.</span></span> 

## <span data-ttu-id="e7bdb-115"><a name="enable-vpn"></a>Bir API Management iç sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="e7bdb-115"><a name="enable-vpn"> </a>Creating an API Management in Internal Virtual network</span></span>
<span data-ttu-id="e7bdb-116">Merhaba iç sanal ağ içinde API Management hizmeti bir iç yük Balancer(ILB) barındırılır.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-116">hello API Management service in Internal Virtual network is hosted behind an Internal Load Balancer(ILB).</span></span> <span data-ttu-id="e7bdb-117">Merhaba hello ILB'nin IP adresi olduğundan hello [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) aralık.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-117">hello IP Address of hello ILB is in hello [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) range.</span></span>  

### <a name="enable-vnet-connection-using-azure-portal"></a><span data-ttu-id="e7bdb-118">Azure portalını kullanarak VNET bağlantıyı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="e7bdb-118">Enable VNET connection using Azure portal</span></span>
<span data-ttu-id="e7bdb-119">İlk hello adımları izleyerek hello API Management hizmeti oluşturma [oluşturma API Management hizmeti][Create API Management service].</span><span class="sxs-lookup"><span data-stu-id="e7bdb-119">First create hello API Management service by following hello steps [Create API Management service][Create API Management service].</span></span> <span data-ttu-id="e7bdb-120">Bir sanal ağ içinde dağıtılan sonra Kurulum API Management toobe.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-120">Then set-up API Management toobe deployed inside a Virtual network.</span></span>

![Menü APIM iç sanal ağ içinde ayarlama][api-management-using-internal-vnet-menu]

<span data-ttu-id="e7bdb-122">Merhaba dağıtım başarılı olduktan sonra Başlangıç panosunda hello hizmetinizin iç sanal IP adresi görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-122">After hello deployment succeeds, you should see hello Internal Virtual IP Address of your service on hello dashboard.</span></span>

![API Yönetim Panosu iç yapılandırılmış VNET ile][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a><span data-ttu-id="e7bdb-124">PowerShell cmdlet'lerini kullanarak VNET bağlantıyı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="e7bdb-124">Enable VNET connection using Powershell cmdlets</span></span>
<span data-ttu-id="e7bdb-125">VNET bağlantısı hello PowerShell cmdlet'lerini kullanarak etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-125">You can also enable VNET connectivity using hello PowerShell cmdlets.</span></span>

* <span data-ttu-id="e7bdb-126">**Bir sanal ağ içinde bir API Management hizmeti oluşturma**: hello cmdlet'ini kullanın [yeni AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate bir Azure API Management hizmet içinde bir VNET ve toouse hello iç VNET türünü yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-126">**Create an API Management service inside a VNET**: Use hello cmdlet [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate an Azure API Management service inside a VNET and configure it toouse hello Internal VNET type.</span></span>

* <span data-ttu-id="e7bdb-127">**VNET içinde varolan bir API Management hizmetini dağıtma**: hello cmdlet'ini kullanın [güncelleştirme AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove var olan bir Azure API Management hizmet içinde bir sanal ağ ve toouse yapılandırın İç sanal ağ türü.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-127">**Deploy an existing API Management service inside a VNET**: Use hello cmdlet [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove an existing Azure API Management service inside a Virtual network and configure it toouse Internal VNET type.</span></span>

## <span data-ttu-id="e7bdb-128"><a name="apim-dns-configuration"></a>DNS yapılandırması</span><span class="sxs-lookup"><span data-stu-id="e7bdb-128"><a name="apim-dns-configuration"></a>DNS configuration</span></span>
<span data-ttu-id="e7bdb-129">API Management dış sanal ağ modunda kullanılırken, DNS Azure tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-129">When using API Management in External Virtual network mode, DNS is managed by Azure.</span></span> <span data-ttu-id="e7bdb-130">İç sanal ağ modu için kendi DNS toomanage sahip.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-130">For Internal Virtual network mode, you have toomanage your own DNS.</span></span>

> [!NOTE]
> <span data-ttu-id="e7bdb-131">API Management hizmeti, IP adreslerini gelen toorequests dinlemez.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-131">API Management service does not listen toorequests coming on IP addresses.</span></span> <span data-ttu-id="e7bdb-132">Yalnızca toorequests toohello (içeren ağ geçidi, Geliştirici Portalı, yayımcı portalı, doğrudan yönetim uç noktası ve git) kendi hizmet uç noktaları üzerinde yapılandırılmış Hostname yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-132">It only responds toorequests toohello Hostname configured on its service endpoints (which includes gateway, developer portal, publisher Portal, direct management endpoint, and git).</span></span>

### <a name="access-on-default-host-names"></a><span data-ttu-id="e7bdb-133">Varsayılan ana bilgisayar adlarını erişimi:</span><span class="sxs-lookup"><span data-stu-id="e7bdb-133">Access on default host names:</span></span>
<span data-ttu-id="e7bdb-134">Bir API Management hizmeti, örneğin "contoso" adlı ortak Azure bulutta oluşturduğunuzda hello aşağıdaki hizmet uç noktaları varsayılan olarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-134">When you create an API Management service in public Azure cloud, named "contoso" for example, hello following service endpoints are configured by default.</span></span>

>   <span data-ttu-id="e7bdb-135">Ağ Geçidi / Proxy - contoso.azure api.net</span><span class="sxs-lookup"><span data-stu-id="e7bdb-135">Gateway / Proxy - contoso.azure-api.net</span></span>

> <span data-ttu-id="e7bdb-136">Yayımcı portalı ve Geliştirici Portalı - contoso.portal.azure api.net</span><span class="sxs-lookup"><span data-stu-id="e7bdb-136">Publisher Portal and Developer Portal - contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="e7bdb-137">Doğrudan yönetim uç noktası - contoso.management.azure api.net</span><span class="sxs-lookup"><span data-stu-id="e7bdb-137">Direct Management Endpoint - contoso.management.azure-api.net</span></span>

>   <span data-ttu-id="e7bdb-138">GIT - contoso.scm.azure api.net</span><span class="sxs-lookup"><span data-stu-id="e7bdb-138">GIT - contoso.scm.azure-api.net</span></span>

<span data-ttu-id="e7bdb-139">tooaccess bu API Management hizmet uç noktaları API Management dağıtıldığı bir bağlı alt toohello sanal ağ içinde bir sanal makine oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-139">tooaccess these API Management service endpoints, you can create a Virtual Machine in a subnet connected toohello Virtual network in which API Management is deployed.</span></span> <span data-ttu-id="e7bdb-140">Yapabileceğiniz Hello iç sanal IP adresi hizmetiniz için 10.0.0.5 olduğunu varsayarak, ana bilgisayar dosyası eşleme (% SystemDrive%\drivers\etc\hosts) gibi hello:</span><span class="sxs-lookup"><span data-stu-id="e7bdb-140">Assuming hello Internal Virtual IP Address for your service is 10.0.0.5, you can do hello hosts file mapping (%SystemDrive%\drivers\etc\hosts) as follows:</span></span>

> <span data-ttu-id="e7bdb-141">10.0.0.5 contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="e7bdb-141">10.0.0.5    contoso.azure-api.net</span></span>

> <span data-ttu-id="e7bdb-142">10.0.0.5 contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="e7bdb-142">10.0.0.5    contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="e7bdb-143">10.0.0.5 contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="e7bdb-143">10.0.0.5    contoso.management.azure-api.net</span></span>

> <span data-ttu-id="e7bdb-144">10.0.0.5 contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="e7bdb-144">10.0.0.5    contoso.scm.azure-api.net</span></span>

<span data-ttu-id="e7bdb-145">Daha sonra oluşturulan sanal makinenin hello tüm hello hizmet uç noktalarına erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-145">You can then access all hello service endpoints from hello Virtual Machine you created.</span></span> <span data-ttu-id="e7bdb-146">Bir özel DNS sunucusu bir sanal ağda kullanıyorsanız, ayrıca bir DNS kayıtları oluşturmak ve bu uç noktaların her yerden erişim, sanal ağınıza.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-146">If using a Custom DNS server in a Virtual network, you can also create A DNS records and access these endpoints from anywhere in your Virtual network.</span></span> 

### <a name="access-on-custom-domain-names"></a><span data-ttu-id="e7bdb-147">Özel etki alanı adlarını erişimi:</span><span class="sxs-lookup"><span data-stu-id="e7bdb-147">Access on custom domain names:</span></span>
<span data-ttu-id="e7bdb-148">Tooaccess hello API Management hizmeti hello varsayılan ana bilgisayar adlarıyla istemiyorsanız, tüm hizmet uç noktalarınızı gibi özel etki alanı adları ayarlayabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e7bdb-148">If you don’t want tooaccess hello API Management service with hello default host names, you can setup custom domain names for all your service endpoints like below</span></span>

![API Management için özel etki alanı ayarlama][api-management-custom-domain-name]

<span data-ttu-id="e7bdb-150">Sonra yalnızca sanal ağınızın içinde erişilebilir olan bu uç noktalar, DNS sunucusu tooaccess A kayıtlarını oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7bdb-150">Then you can create A records in your DNS Server tooaccess these endpoints which are only accessible from within your Virtual network.</span></span>

## <span data-ttu-id="e7bdb-151"><a name="related-content"></a>İlgili içerik</span><span class="sxs-lookup"><span data-stu-id="e7bdb-151"><a name="related-content"> </a>Related content</span></span>
* <span data-ttu-id="e7bdb-152">[VNET içinde APIM kurma sırasında ortak ağ yapılandırma sorunları][Common Network Configuration Issues]</span><span class="sxs-lookup"><span data-stu-id="e7bdb-152">[Common Network configuration issues while setting up APIM in VNET][Common Network Configuration Issues]</span></span>
* [<span data-ttu-id="e7bdb-153">Sanal ağ ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="e7bdb-153">Virtual Network faqs</span></span>](../virtual-network/virtual-networks-faq.md)
* [<span data-ttu-id="e7bdb-154">DNS kaydında A oluşturma</span><span class="sxs-lookup"><span data-stu-id="e7bdb-154">Creating A record in DNS</span></span>](https://msdn.microsoft.com/en-us/library/bb727018.aspx)

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
