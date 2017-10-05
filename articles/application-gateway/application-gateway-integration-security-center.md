---
title: "Azure Güvenlik Merkezi ile uygulama ağ geçidi tümleştirme | Microsoft Docs"
description: "Bu sayfa, uygulama ağ geçidi Azure Güvenlik Merkezi ile nasıl tümleştirildiği bilgi sağlar."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: e5ea5cf9-3b41-4b85-a12c-e758bff7f3ec
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 06/07/2017
ms.author: gwallace
ms.openlocfilehash: 737cdff3140be68cf9d6d396b470dd09c65c52f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a><span data-ttu-id="e52c5-103">Uygulama ağ geçidi ve Azure Güvenlik Merkezi arasında tümleştirme genel bakış</span><span class="sxs-lookup"><span data-stu-id="e52c5-103">Overview of integration between Application Gateway and Azure Security Center</span></span>

<span data-ttu-id="e52c5-104">Uygulama ağ geçidi ve Güvenlik Merkezi, web uygulaması kaynaklarınızı korumanıza nasıl yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="e52c5-104">Learn how Application Gateway and Security Center help protect your web application resources.</span></span> <span data-ttu-id="e52c5-105">Uygulama ağ geçidi web uygulaması Güvenlik Duvarı (WAF) ile tümleşir [Güvenlik Merkezi](../security-center/security-center-intro.md) önlemek için sorunsuz bir görünümünü sağlamak için algılamak ve korumasız web uygulamaları, ortamınızdaki tehditlere yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="e52c5-105">Application gateway web application firewall (WAF) integrates with [Security Center](../security-center/security-center-intro.md) to provide a seamless view to prevent, detect and respond to threats to unprotected web applications in your environment.</span></span>

## <a name="overview"></a><span data-ttu-id="e52c5-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="e52c5-106">Overview</span></span>

<span data-ttu-id="e52c5-107">Uygulama ağ geçidi WAF Güvenlik Merkezi'nde açığından yararlanma girişimi ve güvenlik açıkları web uygulamaları korumak için önerilir.</span><span class="sxs-lookup"><span data-stu-id="e52c5-107">Application Gateway WAF is a recommendation in Security Center for protecting web applications from exploits and vulnerabilities.</span></span> <span data-ttu-id="e52c5-108">WAF tarafından korunmayan etkin web kaynakları Güvenlik Merkezi'nde yüksek önem derecesi öneriler göster.</span><span class="sxs-lookup"><span data-stu-id="e52c5-108">Web enabled resources that are not protected by WAF show in the security center as high severity recommendations.</span></span> <span data-ttu-id="e52c5-109">Web uygulaması güvenlik duvarı için öneriler üzerinde gösterilen **genel bakış** sayfasında **uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e52c5-109">Recommendations for web application firewalls are shown on the **Overview** page, under **Applications**.</span></span>

![Güvenlik Merkezi ile tümleştirme][1]

<span data-ttu-id="e52c5-111">İlgili web uygulaması güvenlik duvarı öneri ayrıntılarını gösteren yeni bir dikey pencere açılır herhangi bir önerimiz'yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e52c5-111">Clicking any recommendations regarding web application firewall opens a new blade showing the details of the recommendation.</span></span>

## <a name="add-a-web-application-firewall-to-an-existing-resource"></a><span data-ttu-id="e52c5-112">Mevcut bir kaynağı bir web uygulaması güvenlik duvarı ekleme</span><span class="sxs-lookup"><span data-stu-id="e52c5-112">Add a web application firewall to an existing resource</span></span>

<span data-ttu-id="e52c5-113">Gidin **daha Hizmetleri** > **güvenlik + kimlik** > **Güvenlik Merkezi** ve **Güvenlik Merkezi - genel bakış** dikey penceresinde tıklatın **uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e52c5-113">Navigate to **More Services** > **Security + Identity** > **Security Center** and on the **Security Center - Overview** blade, click **Applications**.</span></span> <span data-ttu-id="e52c5-114">Üzerinde **Güvenlik Merkezi - uygulamaları** dikey penceresinde, tablo, Güvenlik Merkezi, aboneliğinizde algıladı uygulamaların bir listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="e52c5-114">On the **Security Center - Applications** blade, the table contains a list of applications that Security Center detected in your subscription.</span></span>

![Web uygulamaları][3]

<span data-ttu-id="e52c5-116">Kritik bir sorunu web uygulamasıyla tıklayarak, get **uygulama güvenlik durumu** dikey.</span><span class="sxs-lookup"><span data-stu-id="e52c5-116">By clicking on a web application with a critical issue, you get the **Application security health** blade.</span></span> <span data-ttu-id="e52c5-117">Aşağıdaki resimde, bir web uygulaması güvenlik duvarı tarafından korumalı olmayan web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="e52c5-117">In the image below, the web application that is not protected by a web application firewall.</span></span> 

![korumalı web kaynakları][2]

<span data-ttu-id="e52c5-119">Tıklatın **bir web uygulaması güvenlik duvarı ekleme** altında **önerileri** açmak için **bir Web uygulaması güvenlik duvarı ekleme** dikey.</span><span class="sxs-lookup"><span data-stu-id="e52c5-119">Click **Add a web application firewall** under **Recommendations** to open the **Add a Web Application Firewall** blade.</span></span>

<span data-ttu-id="e52c5-120">Olmayan mevcut bir uygulama ağ geçidi, veya yeni bir tane oluşturmak istediğiniz varsa, tıklatın **Yeni Oluştur** ve **yeni Web uygulaması güvenlik duvarı oluşturma** dikey penceresinde ve tıklatın **Microsoft - uygulama ağ geçidi**.</span><span class="sxs-lookup"><span data-stu-id="e52c5-120">If you do not have an existing Application Gateway, or want to create a new one, click **Create New** and on the **Create a new Web Application Firewall** blade, and click **Microsoft - Application Gateway**.</span></span> <span data-ttu-id="e52c5-121">Bu uygulama ağ geçidi oluşturmak için adımlara götürür.</span><span class="sxs-lookup"><span data-stu-id="e52c5-121">This takes you through the steps to create an application gateway.</span></span> <span data-ttu-id="e52c5-122">Bu noktada, bu kaynak bir web uygulaması güvenlik duvarı tarafından korunduğunu şimdi Güvenlik Merkezi korumalı bir kaynağın izler, web uygulamanızın eklenir.</span><span class="sxs-lookup"><span data-stu-id="e52c5-122">At this point, your web application is added as a protected resource, Security Center now tracks that this resource is protected by a web application firewall.</span></span> <span data-ttu-id="e52c5-123">Bu, arka uç havuzu üye olarak eklemez.</span><span class="sxs-lookup"><span data-stu-id="e52c5-123">This does not add it as a backend pool member.</span></span>

<span data-ttu-id="e52c5-124">Mevcut bir uygulama ağ geçidi varsa, bunun altında seçebilirsiniz **var olan çözümünü kullanma**</span><span class="sxs-lookup"><span data-stu-id="e52c5-124">If you have an existing application gateway, you can choose it under **Use existing solution**</span></span>

![Web uygulaması güvenlik duvarı Ekle dikey penceresi][4]

<span data-ttu-id="e52c5-126">Bir web uygulaması Güvenlik Merkezi aracılığıyla bir uygulama ağ geçidi için bir arka uç havuzu üye olarak kaynak eklemez ekleme, bu uygulama ağ geçidi kaynağı doğrudan yapılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e52c5-126">Adding a web application to an application gateway through Security Center does not add the resource as a backend pool member, this must be done on the application gateway resource directly.</span></span>

## <a name="add-a-resource-to-an-existing-web-application-firewall"></a><span data-ttu-id="e52c5-127">Bir kaynak için var olan bir web uygulaması güvenlik duvarı ekleyin</span><span class="sxs-lookup"><span data-stu-id="e52c5-127">Add a resource to an existing web application firewall</span></span>

<span data-ttu-id="e52c5-128">Gidin **daha Hizmetleri** > **güvenlik + kimlik** > **Güvenlik Merkezi** ve **Güvenlik Merkezi - genel bakış** dikey penceresinde tıklatın **iş ortağı çözümleri**.</span><span class="sxs-lookup"><span data-stu-id="e52c5-128">Navigate to **More Services** > **Security + Identity** > **Security Center** and on the **Security Center - Overview** blade, click **Partner solutions**.</span></span> <span data-ttu-id="e52c5-129">Var olan Güvenlik Merkezi kullanan bir uygulama ağ geçitleri Göster **iş ortağı çözümleri** dikey.</span><span class="sxs-lookup"><span data-stu-id="e52c5-129">Existing Security Center aware application gateways show in the **Partner Solutions** blade.</span></span>

![iş ortağı çözümleri][7]

<span data-ttu-id="e52c5-131">Tıklatın **bağlantı uygulaması** açmak için **bağlantı uygulamaları** dikey penceresinde, burada, belirtilen olduğundan seçeneklerini mevcut uygulamaları seçin.</span><span class="sxs-lookup"><span data-stu-id="e52c5-131">Click **Link app** to open the **Link Applications** blade, here you are given the options to select existing applications.</span></span> <span data-ttu-id="e52c5-132">Koruma ve uygulamaları seçmek **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="e52c5-132">Choose the applications to protect and click **OK**.</span></span> <span data-ttu-id="e52c5-133">Bu web uygulaması uygulama ağ geçidi arka uç havuzuna eklemez.</span><span class="sxs-lookup"><span data-stu-id="e52c5-133">This does not add the web application to the backend pool of the application gateway.</span></span> <span data-ttu-id="e52c5-134">Güvenlik Merkezi izlemek için bu kaynakları korumalı bir kaynak olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e52c5-134">This sets the resources as a protected resource so Security Center can track it.</span></span> <span data-ttu-id="e52c5-135">Kaynak arka uç havuzu üye olarak eklemek için bu uygulama ağ geçidi tıklayabilirsiniz geçerli dikey penceresinden yapılmalıdır **çözüm konsolunu** uygulama ağ geçidi kaynağı'na, web uygulaması arka uç havuzuna ekleyebileceğiniz gerçekleştirilecek.</span><span class="sxs-lookup"><span data-stu-id="e52c5-135">To add the resource as a backend pool member, this must be done on the application gateway, from the current blade you can click **Solution console** to be taken to the application gateway resource where you can add the web application to the backend pool.</span></span>

![iş ortağı çözümleri uygulamaları][6]

## <a name="finalize-configuration"></a><span data-ttu-id="e52c5-137">Yapılandırma Sonlandır</span><span class="sxs-lookup"><span data-stu-id="e52c5-137">Finalize configuration</span></span>

<span data-ttu-id="e52c5-138">Güvenlik Merkezi, bir uygulama ağ geçidi korunan bir kaynağa olarak eklenen uygulamalar izler.</span><span class="sxs-lookup"><span data-stu-id="e52c5-138">Security Center tracks applications added to an application gateway as a protected resource.</span></span>  <span data-ttu-id="e52c5-139">Bu kaynak izler ve onu bir uygulama ağ geçidi tarafından korunmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="e52c5-139">It monitors the health of this resource and ensures that it is protected by an application gateway.</span></span> <span data-ttu-id="e52c5-140">Özel IP, genel IP veya NIC, sanal makinenin uygulama ağ geçidi arka uç havuzuna eklemek için sonraki adım olacaktır.</span><span class="sxs-lookup"><span data-stu-id="e52c5-140">The next step is to add the private IP, public IP, or NIC of your virtual machine to the backend pool of the application gateway.</span></span> <span data-ttu-id="e52c5-141">Bu, ek bir öneri yapılana kadar **uygulama korumayı Sonlandır** kaynağı eklenene kadar gösterilir.</span><span class="sxs-lookup"><span data-stu-id="e52c5-141">Until this is done an additional recommendation of **Finalize application protection** is shown until the resource is added.</span></span>

![Web uygulaması güvenlik duvarı Ekle dikey penceresi][5]

## <a name="security-alerts"></a><span data-ttu-id="e52c5-143">Güvenlik Uyarıları</span><span class="sxs-lookup"><span data-stu-id="e52c5-143">Security Alerts</span></span>

<span data-ttu-id="e52c5-144">Güvenlik Merkezi içinde gitmek **ALGILAMA** > **güvenlik uyarıları**.</span><span class="sxs-lookup"><span data-stu-id="e52c5-144">Within Security Center navigate to **DETECTION** > **Security Alerts**.</span></span>  <span data-ttu-id="e52c5-145">Burada, uygulama ağ geçitleri için WAF uyarıları bulun.</span><span class="sxs-lookup"><span data-stu-id="e52c5-145">Here you find WAF alerts for your application gateways.</span></span> <span data-ttu-id="e52c5-146">Uyarıları WAF kural tarafından bölünür.</span><span class="sxs-lookup"><span data-stu-id="e52c5-146">Alerts are broken down by WAF rule.</span></span>

![Güvenlik Uyarıları][8]

<span data-ttu-id="e52c5-148">Bir kural tıklatarak uyarıların bir listesi için bu belirli WAF kuralı sağlar.</span><span class="sxs-lookup"><span data-stu-id="e52c5-148">Clicking an rule will provide a list of alerts for that specific WAF rule.</span></span> <span data-ttu-id="e52c5-149">Her uyarı bulma hakkında ek ayrıntılar gösterir.</span><span class="sxs-lookup"><span data-stu-id="e52c5-149">Each alert shows additional details on the finding.</span></span> <span data-ttu-id="e52c5-150">Uygulama ağ geçidi için bağlantı ayrıntıları sağlayın.</span><span class="sxs-lookup"><span data-stu-id="e52c5-150">The details provide a link to the application gateway.</span></span>
 
![Uyarı ayrıntıları][9]

## <a name="next-steps"></a><span data-ttu-id="e52c5-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e52c5-152">Next steps</span></span>

<span data-ttu-id="e52c5-153">Web uygulaması güvenlik duvarı var olan bir uygulama ağ geçidi'nı etkinleştirme hakkında bilgi için [oluştur veya güncelleştir web uygulaması güvenlik duvarı ile Azure uygulama ağ geçidi](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span><span class="sxs-lookup"><span data-stu-id="e52c5-153">To learn how to enable web application firewall on an existing application gateway, visit [Create or update an Azure Application Gateway with web application firewall](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span></span>

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png