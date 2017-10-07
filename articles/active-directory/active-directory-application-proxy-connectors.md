---
title: "aaaClassic portal Azure AD uygulaması Proxy bağlayıcılar | Microsoft Docs"
description: "Kapak nasıl toocreate ve Azure AD uygulama proxy'si bağlayıcılarını gruplarını yönetin."
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
ms.openlocfilehash: 43559b0f4ffc3c7dbbf00901e89ac276d01796e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a><span data-ttu-id="f3305-103">Ayrı ağlarda ve konumları bağlayıcı gruplarını kullanarak uygulama yayımlama</span><span class="sxs-lookup"><span data-stu-id="f3305-103">Publish applications on separate networks and locations using connector groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f3305-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="f3305-104">Azure portal</span></span>](active-directory-application-proxy-connectors-azure-portal.md)
> * [<span data-ttu-id="f3305-105">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="f3305-105">Azure classic portal</span></span>](active-directory-application-proxy-connectors.md)
>
>

<span data-ttu-id="f3305-106">Bağlayıcı grupları dahil olmak üzere çeşitli senaryolar için kullanışlıdır:</span><span class="sxs-lookup"><span data-stu-id="f3305-106">Connector groups are useful for various scenarios, including:</span></span>

* <span data-ttu-id="f3305-107">Birden çok birbirine bağlı veri merkezleri siteleriyle.</span><span class="sxs-lookup"><span data-stu-id="f3305-107">Sites with multiple interconnected datacenters.</span></span> <span data-ttu-id="f3305-108">Veri Merkezi çapraz bağlantıları pahalı ve yavaş olduğundan bu durumda, tookeep hello datacenter içindeki kadar trafiği mümkün olduğunca istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="f3305-108">In this case, you want tookeep as much traffic within hello datacenter as possible because cross-datacenter links are expensive and slow.</span></span> <span data-ttu-id="f3305-109">Bağlayıcılar uygulamalarında hello veri merkezi içinde bulunan her veri merkezi tooserve yalnızca hello dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3305-109">You can deploy connectors in each datacenter tooserve only hello applications that reside within hello datacenter.</span></span> <span data-ttu-id="f3305-110">Bu yaklaşım, veri merkezi çapraz bağlantıları en aza indirir ve tooyour kullanıcılar tamamen saydam bir deneyim sağlar.</span><span class="sxs-lookup"><span data-stu-id="f3305-110">This approach minimizes cross-datacenter links and provides an entirely transparent experience tooyour users.</span></span>
* <span data-ttu-id="f3305-111">Merhaba ana Kurumsal ağın parçası olmayan yalıtılmış ağlarda yüklü uygulamaları yönetme.</span><span class="sxs-lookup"><span data-stu-id="f3305-111">Managing applications installed on isolated networks that are not part of hello main corporate network.</span></span> <span data-ttu-id="f3305-112">Yalıtılmış ağlarda tooalso yalıtmaya uygulamaları toohello ağda bağlayıcı grupları ayrılmış tooinstall bağlayıcılar kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3305-112">You can use connector groups tooinstall dedicated connectors on isolated networks tooalso isolate applications toohello network.</span></span>
* <span data-ttu-id="f3305-113">Bulut erişimi için Iaas üzerinde yüklü uygulamalar için bağlayıcı grupları, bir ortak hizmet toosecure hello erişim tooall hello uygulamalar sağlar.</span><span class="sxs-lookup"><span data-stu-id="f3305-113">For applications installed on IaaS for cloud access, connector groups provide a common service toosecure hello access tooall hello apps.</span></span> <span data-ttu-id="f3305-114">Bağlayıcı gruplar şirket ağınızda ek bağımlılık oluşturun veya hello uygulama deneyimi parçalara yok.</span><span class="sxs-lookup"><span data-stu-id="f3305-114">Connector groups don't create additional dependency on your corporate network, or fragment hello app experience.</span></span> <span data-ttu-id="f3305-115">Bağlayıcılar, her bulut veri merkezinde yüklü ve bu ağda bulunan uygulamalar sunar.</span><span class="sxs-lookup"><span data-stu-id="f3305-115">Connectors can be installed on every cloud datacenter and serve only applications that reside in this network.</span></span> <span data-ttu-id="f3305-116">Birkaç bağlayıcılar tooachieve yüksek kullanılabilirlik yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3305-116">You can install several connectors tooachieve high availability.</span></span>
* <span data-ttu-id="f3305-117">İçinde belirli bağlayıcılar orman dağıtılabilir ve tooserve belirli uygulamaları birden çok orman ortamlarına desteği.</span><span class="sxs-lookup"><span data-stu-id="f3305-117">Support for multi-forest environments in which specific connectors can be deployed per forest and set tooserve specific applications.</span></span>
* <span data-ttu-id="f3305-118">Bağlayıcı grupları tooeither yük devretme algılamak veya yedekleme için olarak hello ana olağanüstü durum kurtarma sitede kullanılabilir site.</span><span class="sxs-lookup"><span data-stu-id="f3305-118">Connector groups can be used in Disaster Recovery sites tooeither detect failover or as backup for hello main site.</span></span>
* <span data-ttu-id="f3305-119">Bağlayıcı grupları için de birden çok şirketler tek bir kiracı tarafından kullanılan tooserve olabilir.</span><span class="sxs-lookup"><span data-stu-id="f3305-119">Connector groups can also be used tooserve multiple companies from a single tenant.</span></span>

## <a name="prerequisite-create-your-connectors"></a><span data-ttu-id="f3305-120">Önkoşul: oluşturma, bağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="f3305-120">Prerequisite: Create your connectors</span></span>
<span data-ttu-id="f3305-121">toogroup, bağlayıcılar [birden çok bağlayıcı yükleme](active-directory-application-proxy-enable.md), ardından ad ve gruplandırın.</span><span class="sxs-lookup"><span data-stu-id="f3305-121">toogroup your connectors, [install multiple connectors](active-directory-application-proxy-enable.md), then name and group them.</span></span> <span data-ttu-id="f3305-122">Son olarak tooassign olması bunları toospecific uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="f3305-122">Finally you have tooassign them toospecific apps.</span></span>

## <a name="step-1-create-connector-groups"></a><span data-ttu-id="f3305-123">1. adım: bağlayıcı grupları oluşturma</span><span class="sxs-lookup"><span data-stu-id="f3305-123">Step 1: Create connector groups</span></span>
<span data-ttu-id="f3305-124">İstediğiniz sayıda bağlayıcı grupları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3305-124">You can create as many connector groups as you want.</span></span> <span data-ttu-id="f3305-125">Bağlayıcı grup oluşturma hello Klasik Azure portalı gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="f3305-125">Connector group creation is accomplished in hello Azure classic portal.</span></span>

1. <span data-ttu-id="f3305-126">Dizininizi seçin ve tıklatın **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="f3305-126">Select your directory and click **Configure**.</span></span>  
    <span data-ttu-id="f3305-127">![Uygulama proxy'si, yapılandırma ekran görüntüsü - bağlayıcı gruplarının Yönet'e tıklayın](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span><span class="sxs-lookup"><span data-stu-id="f3305-127">![Application proxy, configure screenshot - click manage connector groups](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span></span>
2. <span data-ttu-id="f3305-128">Uygulama proxy'si altında tıklatın **bağlayıcı grupları yönet** ve hello Grup bir ad verip bir bağlayıcı grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f3305-128">Under Application Proxy, click **Manage Connector Groups** and create a connector group by giving hello group a name.</span></span>  
    <span data-ttu-id="f3305-129">![Uygulama Ara sunucusu Bağlayıcısı ekran görüntüsü - ad yeni grup gruplar](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span><span class="sxs-lookup"><span data-stu-id="f3305-129">![Application proxy connector groups screenshot - name new group](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span></span>

## <a name="step-2-assign-connectors-tooyour-groups"></a><span data-ttu-id="f3305-130">2. adım: bağlayıcıları tooyour grupları atama</span><span class="sxs-lookup"><span data-stu-id="f3305-130">Step 2: Assign connectors tooyour groups</span></span>
<span data-ttu-id="f3305-131">Merhaba bağlayıcı grupları oluşturulduktan sonra hello bağlayıcılar toohello uygun Grup taşıyın.</span><span class="sxs-lookup"><span data-stu-id="f3305-131">Once hello connector groups are created, move hello connectors toohello appropriate group.</span></span>

1. <span data-ttu-id="f3305-132">Altında **uygulama proxy'si**, tıklatın **yönetmek Bağlayıcılar**.</span><span class="sxs-lookup"><span data-stu-id="f3305-132">Under **Application Proxy**, click **Manage Connectors**.</span></span>
2. <span data-ttu-id="f3305-133">Altında **grup**seçin her bağlayıcı için istediğiniz hello grubu.</span><span class="sxs-lookup"><span data-stu-id="f3305-133">Under **Group**, select hello group you want for each connector.</span></span> <span data-ttu-id="f3305-134">Merhaba yeni grubunda active too10 dakika toobecome hello bağlayıcılar alabilir.</span><span class="sxs-lookup"><span data-stu-id="f3305-134">It might take hello connectors up too10 minutes toobecome active in hello new group.</span></span>  
    <span data-ttu-id="f3305-135">![Uygulama proxy'si bağlayıcılar ekran görüntüsü - açılır menüsünden grubunu seçin](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span><span class="sxs-lookup"><span data-stu-id="f3305-135">![Application proxy connectors screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span></span>

## <a name="step-3-assign-applications-tooyour-connector-groups"></a><span data-ttu-id="f3305-136">3. adım: uygulama tooyour bağlayıcı grupları atama</span><span class="sxs-lookup"><span data-stu-id="f3305-136">Step 3: Assign applications tooyour connector groups</span></span>
<span data-ttu-id="f3305-137">Merhaba son adımı tooset sunduğu her uygulama toohello bağlayıcı grubudur.</span><span class="sxs-lookup"><span data-stu-id="f3305-137">hello last step is tooset each application toohello connector group that serves it.</span></span>

1. <span data-ttu-id="f3305-138">Select hello dizininizde, Klasik Azure portalı içinde tooassign toohello Grup istediğiniz uygulama hello **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="f3305-138">In hello Azure classic portal, in your directory, select hello Application you want tooassign toohello group and click **Configure**.</span></span>
2. <span data-ttu-id="f3305-139">Altında **bağlayıcı grup**seçin istediğiniz uygulama toouse hello hello grubu.</span><span class="sxs-lookup"><span data-stu-id="f3305-139">Under **Connector group**, select hello group you want hello application toouse.</span></span> <span data-ttu-id="f3305-140">Bu değişikliği hemen uygulanır.</span><span class="sxs-lookup"><span data-stu-id="f3305-140">This change is immediately applied.</span></span>  
    <span data-ttu-id="f3305-141">![Uygulama proxy Bağlayıcısı Grup ekran görüntüsü - açılır menüsünden grubunu seçin](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span><span class="sxs-lookup"><span data-stu-id="f3305-141">![Application proxy connector group screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span></span>

## <a name="see-also"></a><span data-ttu-id="f3305-142">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="f3305-142">See also</span></span>
* [<span data-ttu-id="f3305-143">Uygulama Ara sunucusunu etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="f3305-143">Enable Application Proxy</span></span>](active-directory-application-proxy-enable.md)
* [<span data-ttu-id="f3305-144">Çoklu oturum açmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="f3305-144">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="f3305-145">Koşullu erişimi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="f3305-145">Enable conditional access</span></span>](active-directory-application-proxy-conditional-access.md)
* [<span data-ttu-id="f3305-146">Uygulama Ara sunucusu ile ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="f3305-146">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)

<span data-ttu-id="f3305-147">Merhaba en son haberler ve güncelleştirmeler için hello denetleyin [uygulama ara sunucusu bloguna](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="f3305-147">For hello latest news and updates, check out hello [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
