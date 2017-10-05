---
title: "Azure App Service'te, Yük Dengeleme için trafik Yöneticisi kullanan bir web uygulaması için bir özel etki alanı adı yapılandırın."
description: "Bir özel etki alanı adı için bir web uygulamasını Azure App Service'te, Yük Dengeleme için trafik Yöneticisi'ni içerir."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 0f96c0e7-0901-489b-a95a-e3b66ca0a1c2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 5f099201d9018a6f8577cb3daf127d09560fb94b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a><span data-ttu-id="b40a6-103">Trafik Yöneticisi'ni kullanarak Azure App Service içinde bir web uygulaması için bir özel etki alanı adı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b40a6-103">Configuring a custom domain name for a web app in Azure App Service using Traffic Manager</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

<span data-ttu-id="b40a6-104">Bu makalede Yük Dengeleme için trafik Yöneticisi kullanan bir özel etki alanı adı Azure App Service ile kullanmak için genel yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="b40a6-104">This article provides generic instructions for using a custom domain name with Azure App Service that use Traffic Manager for load balancing.</span></span>

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="b40a6-105">DNS kayıtlarını anlama</span><span class="sxs-lookup"><span data-stu-id="b40a6-105">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a><span data-ttu-id="b40a6-106">Web uygulamalarınızı Standart mod için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b40a6-106">Configure your web apps for standard mode</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="b40a6-107">Özel etki alanınız için DNS kaydı ekleyin</span><span class="sxs-lookup"><span data-stu-id="b40a6-107">Add a DNS record for your custom domain</span></span>
> [!NOTE]
> <span data-ttu-id="b40a6-108">Azure App Service Web Apps aracılığıyla etki alanı satın aldıktan sonra aşağıdaki adımları atlayın ve son adımına başvurmak [Web uygulamaları için etki alanı satın](custom-dns-web-site-buydomains-web-app.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="b40a6-108">If you have purchased domain through Azure App Service Web Apps then skip following steps and refer to the final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md) article.</span></span>
> 
> 

<span data-ttu-id="b40a6-109">Özel etki alanınızı Azure App Service'in web uygulamasında ilişkilendirmek için yeni bir giriş DNS tabloda özel etki alanınız için etki alanı adınızı satın alınan etki alanı kayıt şirketi tarafından sağlanan araçları kullanarak eklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="b40a6-109">To associate your custom domain with a web app in Azure App Service, you must add a new entry in the DNS table for your custom domain by using tools provided by the domain registrar that you purchased your domain name from.</span></span> <span data-ttu-id="b40a6-110">Bulun ve DNS araçları kullanmak için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="b40a6-110">Use the following steps to locate and use the DNS tools.</span></span>

1. <span data-ttu-id="b40a6-111">Etki alanı kayıt şirketinizdeki hesabınızda oturum açın ve DNS kayıtlarını yönetme için bir sayfa arayın.</span><span class="sxs-lookup"><span data-stu-id="b40a6-111">Sign in to your account at your domain registrar, and look for a page for managing DNS records.</span></span> <span data-ttu-id="b40a6-112">Bağlantıları veya olarak etiketli sitesinin alanları arayın **etki alanı adı**, **DNS**, veya **adı sunucu yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="b40a6-112">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="b40a6-113">Bu sayfaya bir bağlantı genellikle bulunabilir hesap bilgilerinizi görüntülemek ve bir bağlantı gibi arayan **My etki alanları**.</span><span class="sxs-lookup"><span data-stu-id="b40a6-113">Often a link to this page can be found be viewing your account information, and then looking for a link such as **My domains**.</span></span>
2. <span data-ttu-id="b40a6-114">Etki alanı adınız için Yönetim sayfasında bulduktan sonra DNS kaydını düzenlemek izin veren bir bağlantı için bakın.</span><span class="sxs-lookup"><span data-stu-id="b40a6-114">Once you have found the management page for your domain name, look for a link that allows you to edit the DNS records.</span></span> <span data-ttu-id="b40a6-115">Bu olarak listelenebilir bir **bölge dosyası**, **DNS kayıtlarını**, ya da farklı bir **Gelişmiş** yapılandırma bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="b40a6-115">This might be listed as a **Zone file**, **DNS Records**, or as an **Advanced** configuration link.</span></span>
   
   * <span data-ttu-id="b40a6-116">Sayfa büyük olasılıkla zaten oluşturulmuş, bir giriş ilişkilendirme gibi birkaç kayıtları vardır '**@**'veya'\*' bir 'etki alanı park' sayfasıyla.</span><span class="sxs-lookup"><span data-stu-id="b40a6-116">The page will most likely have a few records already created, such as an entry associating '**@**' or '\*' with a 'domain parking' page.</span></span> <span data-ttu-id="b40a6-117">Ayrıca ortak alt etki alanları için kayıtları gibi içerebilir **www**.</span><span class="sxs-lookup"><span data-stu-id="b40a6-117">It may also contain records for common sub-domains such as **www**.</span></span>
   * <span data-ttu-id="b40a6-118">Sayfa Bahsediyor **CNAME kayıtları**, veya bir kayıt türü seçmek için aşağı açılan sağlayın.</span><span class="sxs-lookup"><span data-stu-id="b40a6-118">The page will mention **CNAME records**, or provide a drop-down to select a record type.</span></span> <span data-ttu-id="b40a6-119">Bu ayrıca diğer kayıtları gibi bahsedebilir **A kayıtlarını** ve **MX kayıtları**.</span><span class="sxs-lookup"><span data-stu-id="b40a6-119">It may also mention other records such as **A records** and **MX records**.</span></span> <span data-ttu-id="b40a6-120">Bazı durumlarda, CNAME kayıtları diğer adlarına göre gibi çağrılacak bir **diğer ad kaydı**.</span><span class="sxs-lookup"><span data-stu-id="b40a6-120">In some cases, CNAME records will be called by other names such as an **Alias Record**.</span></span>
   * <span data-ttu-id="b40a6-121">Sayfa ayrıca izin alanları olacaktır **harita** gelen bir **ana bilgisayar adı** veya **etki alanı adı** başka bir etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="b40a6-121">The page will also have fields that allow you to **map** from a **Host name** or **Domain name** to another domain name.</span></span>
3. <span data-ttu-id="b40a6-122">Her kayıt şirketi ayrıntılarını değişir, ancak genel eşledikten *gelen* özel etki alanı adınızı (gibi **contoso.com**,) *için* trafik yöneticisi etki alanı adı (**contoso.trafficmanager.net**) web uygulamanız için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b40a6-122">While the specifics of each registrar vary, in general you map *from* your custom domain name (such as **contoso.com**,) *to* the Traffic Manager domain name (**contoso.trafficmanager.net**) that is used for your web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b40a6-123">Alternatif olarak, bir kayıt zaten kullanımda ve uygulamalarınızı erken önlem bağlamak gerekiyorsa, ek bir CNAME kaydı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b40a6-123">Alternatively, if a record is already in use and you need to preemptively bind your apps to it, you can create an additional CNAME record.</span></span> <span data-ttu-id="b40a6-124">Örneğin, erken önlem bağlamak için **www.contoso.com** web uygulamanız için bir CNAME kayıt oluşturma **awverify.www** için **contoso.trafficmanager.net**.</span><span class="sxs-lookup"><span data-stu-id="b40a6-124">For example, to preemptively bind **www.contoso.com** to your web app, create a CNAME record from **awverify.www** to **contoso.trafficmanager.net**.</span></span> <span data-ttu-id="b40a6-125">Ardından "www.contoso.com", "www" CNAME kaydı değiştirmeden, Web uygulamanızın ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b40a6-125">You can then add "www.contoso.com" to your Web App without changing the "www" CNAME record.</span></span> <span data-ttu-id="b40a6-126">Daha fazla bilgi için bkz: [özel bir etki alanındaki bir web uygulaması oluşturma DNS kayıtlarını][CREATEDNS].</span><span class="sxs-lookup"><span data-stu-id="b40a6-126">For more information, see [Create DNS records for a web app in a custom domain][CREATEDNS].</span></span>
   > 
   > 
4. <span data-ttu-id="b40a6-127">Ekleme veya kayıt şirketinizdeki DNS kayıtlarını değiştirme tamamladıktan sonra değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b40a6-127">Once you have finished adding or modifying DNS records at your registrar, save the changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a><span data-ttu-id="b40a6-128">Trafik Yöneticisi'ni etkinleştir</span><span class="sxs-lookup"><span data-stu-id="b40a6-128">Enable Traffic Manager</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="b40a6-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b40a6-129">Next steps</span></span>
<span data-ttu-id="b40a6-130">Daha fazla bilgi için bkz. [Node.js Geliştirici Merkezi](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="b40a6-130">For more information, see the [Node.js Developer Center](/develop/nodejs/).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
