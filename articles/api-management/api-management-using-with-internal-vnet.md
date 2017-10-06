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
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a>Azure API Management hizmeti iç sanal ağ ile kullanma
Azure sanal ağlar (Vnet'ler), API Management API'leri hello Internet üzerinde erişilebilir yönetebilirsiniz. VPN teknolojileri çeşitli kullanılabilir toomake hello bağlantısı olan ve API Management hello VNET içindeki iki ana modu dağıtılabilir:
* Dış
* İç

## <a name="overview"> </a>Genel Bakış
API Management bir iç sanal ağ modunda dağıtıldığında, tüm hello hizmet uç noktaları (ağ geçidi, Geliştirici Portalı, yayımcı portalında, doğrudan yönetim ve Git) yalnızca erişimini denetleyen bir sanal ağ içinde görünür. Merhaba hizmet uç noktaları hiçbiri hello ortak DNS sunucusu üzerinde kaydedilir.

İç modunda API Yönetimi'ni kullanarak aşağıdaki senaryolar hello elde edebilirsiniz
* Güvenli bir şekilde, özel veri merkezinizde erişilebilir siteden siteye veya ExpressRoute VPN bağlantıları kullanarak dışında 3. taraflar tarafından barındırılan API'ler olun.
* Karma bulut senaryolarında, bulut tabanlı API'ler ve ortak ağ geçidi üzerinden şirket içi API'leri göstererek etkinleştirin.
* Tek bir ağ geçidi uç noktası kullanarak birden çok coğrafi konumda barındırılan Apı'lerinizi yönetin. 

## <a name="enable-vpn"></a>Bir API Management iç sanal ağ oluşturma
Merhaba iç sanal ağ içinde API Management hizmeti bir iç yük Balancer(ILB) barındırılır. Merhaba hello ILB'nin IP adresi olduğundan hello [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) aralık.  

### <a name="enable-vnet-connection-using-azure-portal"></a>Azure portalını kullanarak VNET bağlantıyı etkinleştir
İlk hello adımları izleyerek hello API Management hizmeti oluşturma [oluşturma API Management hizmeti][Create API Management service]. Bir sanal ağ içinde dağıtılan sonra Kurulum API Management toobe.

![Menü APIM iç sanal ağ içinde ayarlama][api-management-using-internal-vnet-menu]

Merhaba dağıtım başarılı olduktan sonra Başlangıç panosunda hello hizmetinizin iç sanal IP adresi görmeniz gerekir.

![API Yönetim Panosu iç yapılandırılmış VNET ile][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a>PowerShell cmdlet'lerini kullanarak VNET bağlantıyı etkinleştir
VNET bağlantısı hello PowerShell cmdlet'lerini kullanarak etkinleştirebilirsiniz.

* **Bir sanal ağ içinde bir API Management hizmeti oluşturma**: hello cmdlet'ini kullanın [yeni AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate bir Azure API Management hizmet içinde bir VNET ve toouse hello iç VNET türünü yapılandırın.

* **VNET içinde varolan bir API Management hizmetini dağıtma**: hello cmdlet'ini kullanın [güncelleştirme AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove var olan bir Azure API Management hizmet içinde bir sanal ağ ve toouse yapılandırın İç sanal ağ türü.

## <a name="apim-dns-configuration"></a>DNS yapılandırması
API Management dış sanal ağ modunda kullanılırken, DNS Azure tarafından yönetilir. İç sanal ağ modu için kendi DNS toomanage sahip.

> [!NOTE]
> API Management hizmeti, IP adreslerini gelen toorequests dinlemez. Yalnızca toorequests toohello (içeren ağ geçidi, Geliştirici Portalı, yayımcı portalı, doğrudan yönetim uç noktası ve git) kendi hizmet uç noktaları üzerinde yapılandırılmış Hostname yanıt verir.

### <a name="access-on-default-host-names"></a>Varsayılan ana bilgisayar adlarını erişimi:
Bir API Management hizmeti, örneğin "contoso" adlı ortak Azure bulutta oluşturduğunuzda hello aşağıdaki hizmet uç noktaları varsayılan olarak yapılandırılır.

>   Ağ Geçidi / Proxy - contoso.azure api.net

> Yayımcı portalı ve Geliştirici Portalı - contoso.portal.azure api.net

> Doğrudan yönetim uç noktası - contoso.management.azure api.net

>   GIT - contoso.scm.azure api.net

tooaccess bu API Management hizmet uç noktaları API Management dağıtıldığı bir bağlı alt toohello sanal ağ içinde bir sanal makine oluşturabilirsiniz. Yapabileceğiniz Hello iç sanal IP adresi hizmetiniz için 10.0.0.5 olduğunu varsayarak, ana bilgisayar dosyası eşleme (% SystemDrive%\drivers\etc\hosts) gibi hello:

> 10.0.0.5 contoso.azure-api.net

> 10.0.0.5 contoso.portal.azure-api.net

> 10.0.0.5 contoso.management.azure-api.net

> 10.0.0.5 contoso.scm.azure-api.net

Daha sonra oluşturulan sanal makinenin hello tüm hello hizmet uç noktalarına erişebilirsiniz. Bir özel DNS sunucusu bir sanal ağda kullanıyorsanız, ayrıca bir DNS kayıtları oluşturmak ve bu uç noktaların her yerden erişim, sanal ağınıza. 

### <a name="access-on-custom-domain-names"></a>Özel etki alanı adlarını erişimi:
Tooaccess hello API Management hizmeti hello varsayılan ana bilgisayar adlarıyla istemiyorsanız, tüm hizmet uç noktalarınızı gibi özel etki alanı adları ayarlayabilirsiniz

![API Management için özel etki alanı ayarlama][api-management-custom-domain-name]

Sonra yalnızca sanal ağınızın içinde erişilebilir olan bu uç noktalar, DNS sunucusu tooaccess A kayıtlarını oluşturabilirsiniz.

## <a name="related-content"></a>İlgili içerik
* [VNET içinde APIM kurma sırasında ortak ağ yapılandırma sorunları][Common Network Configuration Issues]
* [Sanal ağ ile ilgili SSS](../virtual-network/virtual-networks-faq.md)
* [DNS kaydında A oluşturma](https://msdn.microsoft.com/en-us/library/bb727018.aspx)

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
