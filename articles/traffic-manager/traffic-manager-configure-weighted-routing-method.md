---
title: "Azure trafik Yöneticisi'ni kullanarak ağırlıklı hepsini bir kez deneme trafik yönlendirme yöntemini yapılandırma | Microsoft Docs"
description: "Bu makalede, trafik Yöneticisi'nde bir hepsini bir kez deneme yöntemiyle Bakiye trafiği Yük Dengelemesi açıklanmaktadır"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 6dca6de1-18f7-4962-bd98-6055771fab22
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: kumud
ms.openlocfilehash: 7aa4c9120d44ff1b3e59a57090ea04e3f8021fc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-weighted-traffic-routing-method-in-traffic-manager"></a><span data-ttu-id="f858a-103">Trafik Yöneticisi'nde ağırlıklı trafik yönlendirme yöntemini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f858a-103">Configure the weighted traffic routing method in Traffic Manager</span></span>

<span data-ttu-id="f858a-104">Bulut Hizmetleri ve Web siteleri içeren aynı uç noktaların kümesi sağlar ve her bir hepsini şekilde trafiği göndermek için genel bir trafik yönlendirme yöntemini desen var.</span><span class="sxs-lookup"><span data-stu-id="f858a-104">A common traffic routing method pattern is to provide a set of identical endpoints, which include cloud services and websites, and send traffic to each in a round-robin fashion.</span></span> <span data-ttu-id="f858a-105">Aşağıdaki adımlar bu tür trafik yönlendirme yöntemini yapılandırma konusunda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f858a-105">The following steps outline how to configure this type of traffic routing method.</span></span>

> [!NOTE]
> <span data-ttu-id="f858a-106">Azure Web siteleri zaten hepsini bir kez deneme yük dengeleme veri merkezi (bölge olarak da bilinir) içindeki Web siteleri için işlevsellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="f858a-106">Azure Websites already provide round-robin load balancing functionality for websites within a datacenter (also known as a region).</span></span> <span data-ttu-id="f858a-107">Trafik Yöneticisi, Web siteleri için hepsini bir kez deneme trafik yönlendirme yöntemini farklı veri merkezlerinde belirtmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="f858a-107">Traffic Manager allows you to specify round-robin traffic routing method for websites in different datacenters.</span></span>

## <a name="to-configure-the-weighted-traffic-routing-method"></a><span data-ttu-id="f858a-108">Ağırlıklı trafik yönlendirme yöntemini yapılandırmak için</span><span class="sxs-lookup"><span data-stu-id="f858a-108">To configure the weighted traffic routing method</span></span>

1. <span data-ttu-id="f858a-109">Bir tarayıcıdan [Azure portalında](http://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="f858a-109">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="f858a-110">Henüz bir hesabınız yoksa, [bir aylık ücretsiz denemeye](https://azure.microsoft.com/free/) kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f858a-110">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="f858a-111">Portal'ın arama çubuğunda arama **Traffic Manager profillerini** ve ardından yönlendirme yöntemi için yapılandırmak istediğiniz profil adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f858a-111">In the portal’s search bar, search for the **Traffic Manager profiles** and then click the profile name that you want to configure the routing method for.</span></span>
3. <span data-ttu-id="f858a-112">İçinde **trafik Yöneticisi profili** dikey penceresinde bulut Hizmetleri ve yapılandırmanızda dahil etmek istediğiniz Web siteleri bulunduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f858a-112">In the **Traffic Manager profile** blade, verify that both the cloud services and websites that you want to include in your configuration are present.</span></span>
4. <span data-ttu-id="f858a-113">İçinde **ayarları** 'yi tıklatın **yapılandırma**hem de **yapılandırma** dikey penceresinde, aşağıdaki gibi tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="f858a-113">In the **Settings** section, click **Configuration**, and in the **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="f858a-114">İçin **yönlendirme yöntemi ayarları trafiği**, trafik yönlendirme yöntemini olduğundan emin olun **Weighted**.</span><span class="sxs-lookup"><span data-stu-id="f858a-114">For **traffic routing method settings**, verify that the traffic routing method is **Weighted**.</span></span> <span data-ttu-id="f858a-115">Değilse, **Weighted** aşağı açılan listeden.</span><span class="sxs-lookup"><span data-stu-id="f858a-115">If it is not, click **Weighted** from the dropdown list.</span></span>
    2. <span data-ttu-id="f858a-116">Ayarlama **uç nokta izleme ayarları** aynı şekilde bu profili içindeki tüm her uç noktası için:</span><span class="sxs-lookup"><span data-stu-id="f858a-116">Set the **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="f858a-117">Uygun seçin **Protokolü**ve belirtin **bağlantı noktası** numarası.</span><span class="sxs-lookup"><span data-stu-id="f858a-117">Select the appropriate **Protocol**, and specify the **Port** number.</span></span> 
        2. <span data-ttu-id="f858a-118">İçin **yolu** eğik yazın  */* .</span><span class="sxs-lookup"><span data-stu-id="f858a-118">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="f858a-119">Uç noktaları izlemek için bir yol ve dosya adı belirtmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="f858a-119">To monitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="f858a-120">Bir eğik çizgi "/" göreli yolu için geçerli bir giriş ve dosyasının kök dizininde (varsayılan) olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="f858a-120">A forward slash "/" is a valid entry for the relative path and implies that the file is in the root directory (default).</span></span>
        3. <span data-ttu-id="f858a-121">Sayfanın üstündeki **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="f858a-121">At the top of the page, click **Save**.</span></span>
5. <span data-ttu-id="f858a-122">Değişiklikleri yapılandırmanızda gibi test edin:</span><span class="sxs-lookup"><span data-stu-id="f858a-122">Test the changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="f858a-123">Portal'ın arama çubuğunda aramak için trafik Yöneticisi profil adı ve sonuçları trafik Yöneticisi profiline tıklayın, görüntülenen.</span><span class="sxs-lookup"><span data-stu-id="f858a-123">In the portal’s search bar, search for the Traffic Manager profile name and click the Traffic Manager profile in the results that the displayed.</span></span>
    2.  <span data-ttu-id="f858a-124">İçinde **trafik Yöneticisi** profil dikey penceresinde, tıklatın **genel bakış**.</span><span class="sxs-lookup"><span data-stu-id="f858a-124">In the **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="f858a-125">**Trafik Yöneticisi profili** dikey penceresinde, yeni oluşturulan Traffic Manager profilinizin DNS adını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f858a-125">The **Traffic Manager profile** blade displays the DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="f858a-126">Tüm istemciler tarafından bu kullanılabilir (örneğin, bir web tarayıcısı kullanarak giderek) sağ uç noktası olarak yönlendirilen için yönlendirme türü tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="f858a-126">This can be used by any clients (for example,by navigating to it using a web browser) to get routed to the right endpoint as determined by the routing type.</span></span> <span data-ttu-id="f858a-127">Bu durumda tüm istekleri yönlendirilir hepsini şekilde her bir uç nokta.</span><span class="sxs-lookup"><span data-stu-id="f858a-127">In this case all requests are routed each endpoint in a round-robin fashion.</span></span>
6. <span data-ttu-id="f858a-128">Traffic Manager profilinizin çalışma sonra şirketinizin etki alanı adını Traffic Manager etki alanı adına işaret edecek şekilde yetkili DNS sunucunuzdaki DNS kaydını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="f858a-128">Once your Traffic Manager profile is working, edit the DNS record on your authoritative DNS server to point your company domain name to the Traffic Manager domain name.</span></span>

![Trafik Yöneticisi'ni kullanarak ağırlıklı trafik yönlendirme yöntemini yapılandırma][1]

## <a name="next-steps"></a><span data-ttu-id="f858a-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f858a-130">Next steps</span></span>

- <span data-ttu-id="f858a-131">Hakkında bilgi edinin [öncelik trafik yönlendirme yöntemini](traffic-manager-configure-priority-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="f858a-131">Learn about [priority traffic routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="f858a-132">Hakkında bilgi edinin [performans trafik yönlendirme yöntemini](traffic-manager-configure-performance-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="f858a-132">Learn about [performance traffic routing method](traffic-manager-configure-performance-routing-method.md).</span></span>
- <span data-ttu-id="f858a-133">Hakkında bilgi edinin [coğrafi yönlendirme yöntemi](traffic-manager-configure-geographic-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="f858a-133">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="f858a-134">Bilgi edinmek için nasıl [test trafik Yöneticisi Ayarları](traffic-manager-testing-settings.md).</span><span class="sxs-lookup"><span data-stu-id="f858a-134">Learn how to [test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-weighted-routing-method/traffic-manager-weighted-routing-method.png
