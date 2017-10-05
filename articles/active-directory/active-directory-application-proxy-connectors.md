---
title: "Klasik portal Azure AD uygulaması Proxy bağlayıcılar | Microsoft Docs"
description: "Azure AD uygulama proxy'si bağlayıcılarını grupları oluşturmak ve yönetmek nasıl ele alınmaktadır."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b283796a-9679-4c79-b703-802bb850f65d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: fc65c4053c45d9c16c62ee0fe65924133a4bb94a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a><span data-ttu-id="10a1f-103">Ayrı ağlarda ve konumları bağlayıcı gruplarını kullanarak uygulama yayımlama</span><span class="sxs-lookup"><span data-stu-id="10a1f-103">Publish applications on separate networks and locations using connector groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="10a1f-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="10a1f-104">Azure portal</span></span>](active-directory-application-proxy-connectors-azure-portal.md)
> * [<span data-ttu-id="10a1f-105">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="10a1f-105">Azure classic portal</span></span>](active-directory-application-proxy-connectors.md)
>
>

<span data-ttu-id="10a1f-106">Bağlayıcı grupları dahil olmak üzere çeşitli senaryolar için kullanışlıdır:</span><span class="sxs-lookup"><span data-stu-id="10a1f-106">Connector groups are useful for various scenarios, including:</span></span>

* <span data-ttu-id="10a1f-107">Birden çok birbirine bağlı veri merkezleri siteleriyle.</span><span class="sxs-lookup"><span data-stu-id="10a1f-107">Sites with multiple interconnected datacenters.</span></span> <span data-ttu-id="10a1f-108">Bu durumda, veri merkezi çapraz bağlantıları pahalı ve yavaş olduğundan veri merkezi içinde kadar trafiği mümkün olduğunca tutmak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="10a1f-108">In this case, you want to keep as much traffic within the datacenter as possible because cross-datacenter links are expensive and slow.</span></span> <span data-ttu-id="10a1f-109">Bağlayıcılar veri merkezi içinde bulunan uygulamalar sunmak için her veri merkezinde dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10a1f-109">You can deploy connectors in each datacenter to serve only the applications that reside within the datacenter.</span></span> <span data-ttu-id="10a1f-110">Bu yaklaşım, veri merkezi çapraz bağlantıları en aza indirir ve kullanıcılarınız için tamamen saydam bir deneyim sağlar.</span><span class="sxs-lookup"><span data-stu-id="10a1f-110">This approach minimizes cross-datacenter links and provides an entirely transparent experience to your users.</span></span>
* <span data-ttu-id="10a1f-111">Ana Kurumsal ağın parçası olmayan yalıtılmış ağlarda yüklü uygulamaları yönetme.</span><span class="sxs-lookup"><span data-stu-id="10a1f-111">Managing applications installed on isolated networks that are not part of the main corporate network.</span></span> <span data-ttu-id="10a1f-112">Ayrıca ağa uygulamalarını yalıtmak için yalıtılmış ağlarda ayrılmış bağlayıcılar yüklemek için bağlayıcı gruplarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10a1f-112">You can use connector groups to install dedicated connectors on isolated networks to also isolate applications to the network.</span></span>
* <span data-ttu-id="10a1f-113">Bulut erişimi için Iaas üzerinde yüklü uygulamalar için bağlayıcı grupları güvenli erişim tüm uygulamalar için ortak bir hizmet sağlar.</span><span class="sxs-lookup"><span data-stu-id="10a1f-113">For applications installed on IaaS for cloud access, connector groups provide a common service to secure the access to all the apps.</span></span> <span data-ttu-id="10a1f-114">Bağlayıcı gruplar şirket ağınızda ek bağımlılık oluşturun veya uygulama deneyimi parçalara yok.</span><span class="sxs-lookup"><span data-stu-id="10a1f-114">Connector groups don't create additional dependency on your corporate network, or fragment the app experience.</span></span> <span data-ttu-id="10a1f-115">Bağlayıcılar, her bulut veri merkezinde yüklü ve bu ağda bulunan uygulamalar sunar.</span><span class="sxs-lookup"><span data-stu-id="10a1f-115">Connectors can be installed on every cloud datacenter and serve only applications that reside in this network.</span></span> <span data-ttu-id="10a1f-116">Yüksek kullanılabilirlik elde etmek için birkaç bağlayıcı yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10a1f-116">You can install several connectors to achieve high availability.</span></span>
* <span data-ttu-id="10a1f-117">İçinde belirli bağlayıcılar orman dağıtılabilir ve belirli uygulamaları sunmaya ayarlamak Çoklu orman ortamları için destek.</span><span class="sxs-lookup"><span data-stu-id="10a1f-117">Support for multi-forest environments in which specific connectors can be deployed per forest and set to serve specific applications.</span></span>
* <span data-ttu-id="10a1f-118">Bağlayıcı grupları için ana site ya da yük devretme algılamak için olağanüstü durum kurtarma sitelerdeki veya yedekleme olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="10a1f-118">Connector groups can be used in Disaster Recovery sites to either detect failover or as backup for the main site.</span></span>
* <span data-ttu-id="10a1f-119">Bağlayıcı grupları, birden çok şirket tek bir kiracı hizmet vermek için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="10a1f-119">Connector groups can also be used to serve multiple companies from a single tenant.</span></span>

## <a name="prerequisite-create-your-connectors"></a><span data-ttu-id="10a1f-120">Önkoşul: oluşturma, bağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="10a1f-120">Prerequisite: Create your connectors</span></span>
<span data-ttu-id="10a1f-121">Bağlayıcılar grubuna [birden çok bağlayıcı yükleme](active-directory-application-proxy-enable.md), ardından ad ve gruplandırın.</span><span class="sxs-lookup"><span data-stu-id="10a1f-121">To group your connectors, [install multiple connectors](active-directory-application-proxy-enable.md), then name and group them.</span></span> <span data-ttu-id="10a1f-122">Son olarak belirli uygulamalarla atamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="10a1f-122">Finally you have to assign them to specific apps.</span></span>

## <a name="step-1-create-connector-groups"></a><span data-ttu-id="10a1f-123">1. adım: bağlayıcı grupları oluşturma</span><span class="sxs-lookup"><span data-stu-id="10a1f-123">Step 1: Create connector groups</span></span>
<span data-ttu-id="10a1f-124">İstediğiniz sayıda bağlayıcı grupları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10a1f-124">You can create as many connector groups as you want.</span></span> <span data-ttu-id="10a1f-125">Bağlayıcı grubu oluşturma, Klasik Azure portalında gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="10a1f-125">Connector group creation is accomplished in the Azure classic portal.</span></span>

1. <span data-ttu-id="10a1f-126">Dizininizi seçin ve tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="10a1f-126">Select your directory and click **Configure**.</span></span>  
    <span data-ttu-id="10a1f-127">![Uygulama proxy'si, yapılandırma ekran görüntüsü - bağlayıcı gruplarının Yönet'e tıklayın](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span><span class="sxs-lookup"><span data-stu-id="10a1f-127">![Application proxy, configure screenshot - click manage connector groups](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span></span>
2. <span data-ttu-id="10a1f-128">Uygulama proxy'si altında tıklatın **bağlayıcı grupları yönet** ve grubun bir ad verip bir bağlayıcı grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="10a1f-128">Under Application Proxy, click **Manage Connector Groups** and create a connector group by giving the group a name.</span></span>  
    <span data-ttu-id="10a1f-129">![Uygulama Ara sunucusu Bağlayıcısı ekran görüntüsü - ad yeni grup gruplar](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span><span class="sxs-lookup"><span data-stu-id="10a1f-129">![Application proxy connector groups screenshot - name new group](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span></span>

## <a name="step-2-assign-connectors-to-your-groups"></a><span data-ttu-id="10a1f-130">2. adım: bağlayıcılar, gruplara atayın.</span><span class="sxs-lookup"><span data-stu-id="10a1f-130">Step 2: Assign connectors to your groups</span></span>
<span data-ttu-id="10a1f-131">Bağlayıcı grupları oluşturulduktan sonra uygun gruba bağlayıcıları taşıyın.</span><span class="sxs-lookup"><span data-stu-id="10a1f-131">Once the connector groups are created, move the connectors to the appropriate group.</span></span>

1. <span data-ttu-id="10a1f-132">Altında **uygulama proxy'si**, tıklatın **yönetmek Bağlayıcılar**.</span><span class="sxs-lookup"><span data-stu-id="10a1f-132">Under **Application Proxy**, click **Manage Connectors**.</span></span>
2. <span data-ttu-id="10a1f-133">Altında **grup**, her bağlayıcı için istediğiniz grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="10a1f-133">Under **Group**, select the group you want for each connector.</span></span> <span data-ttu-id="10a1f-134">Bu bağlayıcılar yeni Grup etkinleşmesi için en fazla 10 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="10a1f-134">It might take the connectors up to 10 minutes to become active in the new group.</span></span>  
    <span data-ttu-id="10a1f-135">![Uygulama proxy'si bağlayıcılar ekran görüntüsü - açılır menüsünden grubunu seçin](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span><span class="sxs-lookup"><span data-stu-id="10a1f-135">![Application proxy connectors screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span></span>

## <a name="step-3-assign-applications-to-your-connector-groups"></a><span data-ttu-id="10a1f-136">3. adım: uygulamaları bağlayıcı gruplarınıza atayın</span><span class="sxs-lookup"><span data-stu-id="10a1f-136">Step 3: Assign applications to your connector groups</span></span>
<span data-ttu-id="10a1f-137">Her uygulama, hizmet verdiği bağlayıcı gruba ayarlamak için son adım olacaktır.</span><span class="sxs-lookup"><span data-stu-id="10a1f-137">The last step is to set each application to the connector group that serves it.</span></span>

1. <span data-ttu-id="10a1f-138">Dizininizde, Azure Klasik Portalı'ndaki, önce gruba atamak istediğiniz uygulamayı seçin **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="10a1f-138">In the Azure classic portal, in your directory, select the Application you want to assign to the group and click **Configure**.</span></span>
2. <span data-ttu-id="10a1f-139">Altında **bağlayıcı grup**, kullanmak için uygulamayı istediğiniz grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="10a1f-139">Under **Connector group**, select the group you want the application to use.</span></span> <span data-ttu-id="10a1f-140">Bu değişikliği hemen uygulanır.</span><span class="sxs-lookup"><span data-stu-id="10a1f-140">This change is immediately applied.</span></span>  
    <span data-ttu-id="10a1f-141">![Uygulama proxy Bağlayıcısı Grup ekran görüntüsü - açılır menüsünden grubunu seçin](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span><span class="sxs-lookup"><span data-stu-id="10a1f-141">![Application proxy connector group screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span></span>

## <a name="see-also"></a><span data-ttu-id="10a1f-142">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="10a1f-142">See also</span></span>
* [<span data-ttu-id="10a1f-143">Uygulama Ara sunucusunu etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="10a1f-143">Enable Application Proxy</span></span>](active-directory-application-proxy-enable.md)
* [<span data-ttu-id="10a1f-144">Çoklu oturum açmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="10a1f-144">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="10a1f-145">Koşullu erişimi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="10a1f-145">Enable conditional access</span></span>](active-directory-application-proxy-conditional-access.md)
* [<span data-ttu-id="10a1f-146">Uygulama Ara sunucusu ile ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="10a1f-146">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)

<span data-ttu-id="10a1f-147">En yeni haberler ve güncelleştirmeler için [Uygulama Ara Sunucusu bloguna](http://blogs.technet.com/b/applicationproxyblog/) göz atın</span><span class="sxs-lookup"><span data-stu-id="10a1f-147">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
