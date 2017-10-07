---
title: "Azure Güvenlik Merkezi ile ağ geçidi tümleştirme aaaApplication | Microsoft Docs"
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
ms.openlocfilehash: 6f6ace105e84c01f525ab02938e81ce040c5c9d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a><span data-ttu-id="305fd-103">Uygulama ağ geçidi ve Azure Güvenlik Merkezi arasında tümleştirme genel bakış</span><span class="sxs-lookup"><span data-stu-id="305fd-103">Overview of integration between Application Gateway and Azure Security Center</span></span>

<span data-ttu-id="305fd-104">Uygulama ağ geçidi ve Güvenlik Merkezi, web uygulaması kaynaklarınızı korumanıza nasıl yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="305fd-104">Learn how Application Gateway and Security Center help protect your web application resources.</span></span> <span data-ttu-id="305fd-105">Uygulama ağ geçidi web uygulaması Güvenlik Duvarı (WAF) ile tümleşir [Güvenlik Merkezi](../security-center/security-center-intro.md) tooprovide sorunsuz görünüm tooprevent algılamak ve toothreats toounprotected web uygulamaları, ortamınızdaki yanıt.</span><span class="sxs-lookup"><span data-stu-id="305fd-105">Application gateway web application firewall (WAF) integrates with [Security Center](../security-center/security-center-intro.md) tooprovide a seamless view tooprevent, detect and respond toothreats toounprotected web applications in your environment.</span></span>

## <a name="overview"></a><span data-ttu-id="305fd-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="305fd-106">Overview</span></span>

<span data-ttu-id="305fd-107">Uygulama ağ geçidi WAF Güvenlik Merkezi'nde açığından yararlanma girişimi ve güvenlik açıkları web uygulamaları korumak için önerilir.</span><span class="sxs-lookup"><span data-stu-id="305fd-107">Application Gateway WAF is a recommendation in Security Center for protecting web applications from exploits and vulnerabilities.</span></span> <span data-ttu-id="305fd-108">WAF tarafından korunmayan etkin web kaynakları hello Güvenlik Merkezi'nde yüksek önem derecesi öneriler göster.</span><span class="sxs-lookup"><span data-stu-id="305fd-108">Web enabled resources that are not protected by WAF show in hello security center as high severity recommendations.</span></span> <span data-ttu-id="305fd-109">Web uygulaması güvenlik duvarı için öneriler hello üzerinde gösterilen **genel bakış** sayfasında **uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="305fd-109">Recommendations for web application firewalls are shown on hello **Overview** page, under **Applications**.</span></span>

![Güvenlik Merkezi ile tümleştirme][1]

<span data-ttu-id="305fd-111">Web uygulaması güvenlik duvarı ile ilgili herhangi bir önerimiz tıklatarak hello öneri hello ayrıntılarını gösteren yeni bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="305fd-111">Clicking any recommendations regarding web application firewall opens a new blade showing hello details of hello recommendation.</span></span>

## <a name="add-a-web-application-firewall-tooan-existing-resource"></a><span data-ttu-id="305fd-112">Web uygulaması güvenlik duvarı tooan mevcut kaynak ekleyin</span><span class="sxs-lookup"><span data-stu-id="305fd-112">Add a web application firewall tooan existing resource</span></span>

<span data-ttu-id="305fd-113">Çok gidin**daha Hizmetleri** > **güvenlik + kimlik** > **Güvenlik Merkezi** ve hello **Güvenlik Merkezi - genel bakış**  dikey penceresinde tıklatın **uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="305fd-113">Navigate too**More Services** > **Security + Identity** > **Security Center** and on hello **Security Center - Overview** blade, click **Applications**.</span></span> <span data-ttu-id="305fd-114">Merhaba üzerinde **Güvenlik Merkezi - uygulamaları** dikey penceresinde hello tablo, Güvenlik Merkezi, aboneliğinizde algıladı uygulamaların bir listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="305fd-114">On hello **Security Center - Applications** blade, hello table contains a list of applications that Security Center detected in your subscription.</span></span>

![Web uygulamaları][3]

<span data-ttu-id="305fd-116">Kritik bir sorunu web uygulamasıyla tıklayarak, hello alma **uygulama güvenlik durumu** dikey.</span><span class="sxs-lookup"><span data-stu-id="305fd-116">By clicking on a web application with a critical issue, you get hello **Application security health** blade.</span></span> <span data-ttu-id="305fd-117">Merhaba resimde, bir web uygulaması güvenlik duvarı tarafından korumalı olmayan web uygulaması hello.</span><span class="sxs-lookup"><span data-stu-id="305fd-117">In hello image below, hello web application that is not protected by a web application firewall.</span></span> 

![korumalı web kaynakları][2]

<span data-ttu-id="305fd-119">Tıklatın **bir web uygulaması güvenlik duvarı ekleme** altında **önerileri** tooopen hello **bir Web uygulaması güvenlik duvarı ekleme** dikey.</span><span class="sxs-lookup"><span data-stu-id="305fd-119">Click **Add a web application firewall** under **Recommendations** tooopen hello **Add a Web Application Firewall** blade.</span></span>

<span data-ttu-id="305fd-120">Olmayan mevcut bir uygulama ağ geçidi sahip ya da toocreate yeni bir tane yoksa, tıklatın **Yeni Oluştur** ve hello **yeni Web uygulaması güvenlik duvarı oluşturma** dikey penceresinde ve tıklatın **Microsoft - Uygulama ağ geçidi**.</span><span class="sxs-lookup"><span data-stu-id="305fd-120">If you do not have an existing Application Gateway, or want toocreate a new one, click **Create New** and on hello **Create a new Web Application Firewall** blade, and click **Microsoft - Application Gateway**.</span></span> <span data-ttu-id="305fd-121">Merhaba adımları toocreate bir uygulama ağ geçidi alır.</span><span class="sxs-lookup"><span data-stu-id="305fd-121">This takes you through hello steps toocreate an application gateway.</span></span> <span data-ttu-id="305fd-122">Bu noktada, bu kaynak bir web uygulaması güvenlik duvarı tarafından korunduğunu şimdi Güvenlik Merkezi korumalı bir kaynağın izler, web uygulamanızın eklenir.</span><span class="sxs-lookup"><span data-stu-id="305fd-122">At this point, your web application is added as a protected resource, Security Center now tracks that this resource is protected by a web application firewall.</span></span> <span data-ttu-id="305fd-123">Bu, arka uç havuzu üye olarak eklemez.</span><span class="sxs-lookup"><span data-stu-id="305fd-123">This does not add it as a backend pool member.</span></span>

<span data-ttu-id="305fd-124">Mevcut bir uygulama ağ geçidi varsa, bunun altında seçebilirsiniz **var olan çözümünü kullanma**</span><span class="sxs-lookup"><span data-stu-id="305fd-124">If you have an existing application gateway, you can choose it under **Use existing solution**</span></span>

![Web uygulaması güvenlik duvarı Ekle dikey penceresi][4]

<span data-ttu-id="305fd-126">Bir web uygulaması tooan uygulama ağ geçidi Güvenlik Merkezi aracılığıyla arka uç havuzu üye olarak hello kaynak eklemez ekleme, bu hello uygulama ağ geçidi kaynağı üzerinde doğrudan yapılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="305fd-126">Adding a web application tooan application gateway through Security Center does not add hello resource as a backend pool member, this must be done on hello application gateway resource directly.</span></span>

## <a name="add-a-resource-tooan-existing-web-application-firewall"></a><span data-ttu-id="305fd-127">Bir kaynak tooan varolan web uygulaması güvenlik duvarı ekleme</span><span class="sxs-lookup"><span data-stu-id="305fd-127">Add a resource tooan existing web application firewall</span></span>

<span data-ttu-id="305fd-128">Çok gidin**daha Hizmetleri** > **güvenlik + kimlik** > **Güvenlik Merkezi** ve hello **Güvenlik Merkezi - genel bakış**  dikey penceresinde tıklatın **iş ortağı çözümleri**.</span><span class="sxs-lookup"><span data-stu-id="305fd-128">Navigate too**More Services** > **Security + Identity** > **Security Center** and on hello **Security Center - Overview** blade, click **Partner solutions**.</span></span> <span data-ttu-id="305fd-129">Var olan Güvenlik Merkezi kullanan bir uygulama ağ geçitleri Göster hello **iş ortağı çözümleri** dikey.</span><span class="sxs-lookup"><span data-stu-id="305fd-129">Existing Security Center aware application gateways show in hello **Partner Solutions** blade.</span></span>

![iş ortağı çözümleri][7]

<span data-ttu-id="305fd-131">Tıklatın **bağlantı uygulaması** tooopen hello **bağlantı uygulamaları** dikey penceresinde, burada, belirtilen olduğundan hello seçenekleri tooselect var olan uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="305fd-131">Click **Link app** tooopen hello **Link Applications** blade, here you are given hello options tooselect existing applications.</span></span> <span data-ttu-id="305fd-132">Merhaba uygulamaları tooprotect seçin ve tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="305fd-132">Choose hello applications tooprotect and click **OK**.</span></span> <span data-ttu-id="305fd-133">Bu, başlangıç web uygulaması toohello arka uç havuzu hello uygulama ağ geçidi eklemez.</span><span class="sxs-lookup"><span data-stu-id="305fd-133">This does not add hello web application toohello backend pool of hello application gateway.</span></span> <span data-ttu-id="305fd-134">Güvenlik Merkezi izlemek için bu hello kaynakları korumalı bir kaynak olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="305fd-134">This sets hello resources as a protected resource so Security Center can track it.</span></span> <span data-ttu-id="305fd-135">tooadd hello kaynak bir arka uç havuzu üye olarak bu hello uygulama ağ geçidinde yapılmalıdır, hello geçerli dikey penceresinden tıklayabilirsiniz **çözüm konsolunu** hello web, ekleyebileceğiniz toohello uygulama ağ geçidi kaynağı gerçekleştirilecek toobe Uygulama toohello arka uç havuzu.</span><span class="sxs-lookup"><span data-stu-id="305fd-135">tooadd hello resource as a backend pool member, this must be done on hello application gateway, from hello current blade you can click **Solution console** toobe taken toohello application gateway resource where you can add hello web application toohello backend pool.</span></span>

![iş ortağı çözümleri uygulamaları][6]

## <a name="finalize-configuration"></a><span data-ttu-id="305fd-137">Yapılandırma Sonlandır</span><span class="sxs-lookup"><span data-stu-id="305fd-137">Finalize configuration</span></span>

<span data-ttu-id="305fd-138">Güvenlik Merkezi parçaları uygulamaları tooan uygulama ağ geçidi korumalı bir kaynağın eklendi.</span><span class="sxs-lookup"><span data-stu-id="305fd-138">Security Center tracks applications added tooan application gateway as a protected resource.</span></span>  <span data-ttu-id="305fd-139">Bu kaynak hello durumunu izler ve onu bir uygulama ağ geçidi tarafından korunmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="305fd-139">It monitors hello health of this resource and ensures that it is protected by an application gateway.</span></span> <span data-ttu-id="305fd-140">Hello sonraki tooadd hello özel IP, genel IP veya NIC, sanal makine toohello arka uç havuzunun hello uygulama ağ geçidi adımdır.</span><span class="sxs-lookup"><span data-stu-id="305fd-140">hello next step is tooadd hello private IP, public IP, or NIC of your virtual machine toohello backend pool of hello application gateway.</span></span> <span data-ttu-id="305fd-141">Bu, ek bir öneri yapılana kadar **uygulama korumayı Sonlandır** hello kaynağı eklenene kadar gösterilir.</span><span class="sxs-lookup"><span data-stu-id="305fd-141">Until this is done an additional recommendation of **Finalize application protection** is shown until hello resource is added.</span></span>

![Web uygulaması güvenlik duvarı Ekle dikey penceresi][5]

## <a name="security-alerts"></a><span data-ttu-id="305fd-143">Güvenlik Uyarıları</span><span class="sxs-lookup"><span data-stu-id="305fd-143">Security Alerts</span></span>

<span data-ttu-id="305fd-144">Güvenlik Merkezi içinde çok gidin**ALGILAMA** > **güvenlik uyarıları**.</span><span class="sxs-lookup"><span data-stu-id="305fd-144">Within Security Center navigate too**DETECTION** > **Security Alerts**.</span></span>  <span data-ttu-id="305fd-145">Burada, uygulama ağ geçitleri için WAF uyarıları bulun.</span><span class="sxs-lookup"><span data-stu-id="305fd-145">Here you find WAF alerts for your application gateways.</span></span> <span data-ttu-id="305fd-146">Uyarıları WAF kural tarafından bölünür.</span><span class="sxs-lookup"><span data-stu-id="305fd-146">Alerts are broken down by WAF rule.</span></span>

![Güvenlik Uyarıları][8]

<span data-ttu-id="305fd-148">Bir kural tıklatarak uyarıların bir listesi için bu belirli WAF kuralı sağlar.</span><span class="sxs-lookup"><span data-stu-id="305fd-148">Clicking an rule will provide a list of alerts for that specific WAF rule.</span></span> <span data-ttu-id="305fd-149">Her uyarı hello bulma hakkında ek ayrıntılar gösterir.</span><span class="sxs-lookup"><span data-stu-id="305fd-149">Each alert shows additional details on hello finding.</span></span> <span data-ttu-id="305fd-150">bir bağlantı toohello uygulama ağ geçidi Hello ayrıntıları sağlayın.</span><span class="sxs-lookup"><span data-stu-id="305fd-150">hello details provide a link toohello application gateway.</span></span>
 
![Uyarı ayrıntıları][9]

## <a name="next-steps"></a><span data-ttu-id="305fd-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="305fd-152">Next steps</span></span>

<span data-ttu-id="305fd-153">nasıl tooenable web uygulaması Güvenlik Duvarı'nı var olan bir uygulama ağ geçidi ziyaret toolearn [oluştur veya güncelleştir web uygulaması güvenlik duvarı ile Azure uygulama ağ geçidi](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span><span class="sxs-lookup"><span data-stu-id="305fd-153">toolearn how tooenable web application firewall on an existing application gateway, visit [Create or update an Azure Application Gateway with web application firewall](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span></span>

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png