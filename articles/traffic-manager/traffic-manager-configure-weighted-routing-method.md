---
title: "aaaConfigure ağırlıklı hepsini bir kez deneme trafik yönlendirme yöntemini Azure trafik Yöneticisi'ni kullanarak | Microsoft Docs"
description: "Bu makalede, nasıl tooload Bakiye trafik Yöneticisi'nde bir hepsini bir kez deneme yöntemiyle trafiği açıklanmaktadır."
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
ms.openlocfilehash: 7e2866ead0b2b653845435dd420a763c5e175f4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-weighted-traffic-routing-method-in-traffic-manager"></a><span data-ttu-id="1e268-103">Trafik Yöneticisi'nde hello ağırlıklı trafik yönlendirme yöntemini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1e268-103">Configure hello weighted traffic routing method in Traffic Manager</span></span>

<span data-ttu-id="1e268-104">Genel bir trafik yönlendirme yöntemini desen tooprovide bulut Hizmetleri ve Web siteleri ve trafik tooeach hepsini biçimde Gönder aynı uç noktaların kümesi olur.</span><span class="sxs-lookup"><span data-stu-id="1e268-104">A common traffic routing method pattern is tooprovide a set of identical endpoints, which include cloud services and websites, and send traffic tooeach in a round-robin fashion.</span></span> <span data-ttu-id="1e268-105">Aşağıdaki adımları hello anahat nasıl tooconfigure bu türü trafik yönlendirme metodu.</span><span class="sxs-lookup"><span data-stu-id="1e268-105">hello following steps outline how tooconfigure this type of traffic routing method.</span></span>

> [!NOTE]
> <span data-ttu-id="1e268-106">Azure Web siteleri zaten hepsini bir kez deneme yük dengeleme veri merkezi (bölge olarak da bilinir) içindeki Web siteleri için işlevsellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="1e268-106">Azure Websites already provide round-robin load balancing functionality for websites within a datacenter (also known as a region).</span></span> <span data-ttu-id="1e268-107">Trafik Yöneticisi toospecify hepsini bir kez deneme trafik yönlendirme yöntemini Web siteleri için farklı veri merkezlerinde sağlar.</span><span class="sxs-lookup"><span data-stu-id="1e268-107">Traffic Manager allows you toospecify round-robin traffic routing method for websites in different datacenters.</span></span>

## <a name="tooconfigure-hello-weighted-traffic-routing-method"></a><span data-ttu-id="1e268-108">tooconfigure ağırlıklı hello trafik yönlendirme yöntemi</span><span class="sxs-lookup"><span data-stu-id="1e268-108">tooconfigure hello weighted traffic routing method</span></span>

1. <span data-ttu-id="1e268-109">Toohello içinde bir tarayıcıdan oturum [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1e268-109">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="1e268-110">Henüz bir hesabınız yoksa, [bir aylık ücretsiz denemeye](https://azure.microsoft.com/free/) kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e268-110">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="1e268-111">Merhaba Hello portal'ın arama çubuğunda arama **Traffic Manager profillerini** ve tooconfigure hello yönlendirme yöntemi için istediğiniz hello profilinin adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1e268-111">In hello portal’s search bar, search for hello **Traffic Manager profiles** and then click hello profile name that you want tooconfigure hello routing method for.</span></span>
3. <span data-ttu-id="1e268-112">Merhaba, **trafik Yöneticisi profili** dikey penceresinde, hem bulut Hizmetleri hello ve tooinclude yapılandırmanızda istediğiniz Web siteleri mevcut olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="1e268-112">In hello **Traffic Manager profile** blade, verify that both hello cloud services and websites that you want tooinclude in your configuration are present.</span></span>
4. <span data-ttu-id="1e268-113">Merhaba, **ayarları** 'yi tıklatın **yapılandırma**ve hello **yapılandırma** dikey penceresinde, aşağıdaki gibi tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="1e268-113">In hello **Settings** section, click **Configuration**, and in hello **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="1e268-114">İçin **yönlendirme yöntemi ayarları trafiği**, hello trafik yönlendirme yöntemini olduğundan emin olun **Weighted**.</span><span class="sxs-lookup"><span data-stu-id="1e268-114">For **traffic routing method settings**, verify that hello traffic routing method is **Weighted**.</span></span> <span data-ttu-id="1e268-115">Değilse, **Weighted** hello aşağı açılan listeden.</span><span class="sxs-lookup"><span data-stu-id="1e268-115">If it is not, click **Weighted** from hello dropdown list.</span></span>
    2. <span data-ttu-id="1e268-116">Set hello **uç nokta izleme ayarları** aynı şekilde bu profili içindeki tüm her uç noktası için:</span><span class="sxs-lookup"><span data-stu-id="1e268-116">Set hello **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="1e268-117">Select hello uygun **Protokolü**ve hello belirtin **bağlantı noktası** numarası.</span><span class="sxs-lookup"><span data-stu-id="1e268-117">Select hello appropriate **Protocol**, and specify hello **Port** number.</span></span> 
        2. <span data-ttu-id="1e268-118">İçin **yolu** eğik yazın  */* .</span><span class="sxs-lookup"><span data-stu-id="1e268-118">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="1e268-119">toomonitor uç noktaları, yol ve dosya adı belirtmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="1e268-119">toomonitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="1e268-120">Bir eğik çizgi "/" Merhaba göreli yolu geçerli bir girişi ve o hello dosyadır hello kök dizininde (varsayılan) anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="1e268-120">A forward slash "/" is a valid entry for hello relative path and implies that hello file is in hello root directory (default).</span></span>
        3. <span data-ttu-id="1e268-121">Merhaba hello sayfanın en üstünde, tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="1e268-121">At hello top of hello page, click **Save**.</span></span>
5. <span data-ttu-id="1e268-122">Merhaba değişiklikleri yapılandırmanızda gibi test edin:</span><span class="sxs-lookup"><span data-stu-id="1e268-122">Test hello changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="1e268-123">Hello portal'ın arama çubuğunda hello trafik Yöneticisi profili adını arayın ve görüntülenen o hello hello sonuçlarında hello trafik Yöneticisi profiline tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1e268-123">In hello portal’s search bar, search for hello Traffic Manager profile name and click hello Traffic Manager profile in hello results that hello displayed.</span></span>
    2.  <span data-ttu-id="1e268-124">Merhaba, **trafik Yöneticisi** profil dikey penceresinde, tıklatın **genel bakış**.</span><span class="sxs-lookup"><span data-stu-id="1e268-124">In hello **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="1e268-125">Merhaba **trafik Yöneticisi profili** dikey penceresinde, yeni oluşturulan Traffic Manager profilinizin hello DNS adını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="1e268-125">hello **Traffic Manager profile** blade displays hello DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="1e268-126">Bu herhangi (örneğin, göre bir web tarayıcısı kullanarak tooit gezinme) istemcileri yönlendirilen tooget toohello sağ uç nokta hello yönlendirme türü tarafından belirlendiği şekilde tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1e268-126">This can be used by any clients (for example,by navigating tooit using a web browser) tooget routed toohello right endpoint as determined by hello routing type.</span></span> <span data-ttu-id="1e268-127">Bu durumda tüm istekleri yönlendirilir hepsini şekilde her bir uç nokta.</span><span class="sxs-lookup"><span data-stu-id="1e268-127">In this case all requests are routed each endpoint in a round-robin fashion.</span></span>
6. <span data-ttu-id="1e268-128">Traffic Manager profilinizin çalışma sonra şirket etki alanı adı toohello trafik yöneticisi etki alanı adı, yetkili DNS sunucusu toopoint hello DNS kaydını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="1e268-128">Once your Traffic Manager profile is working, edit hello DNS record on your authoritative DNS server toopoint your company domain name toohello Traffic Manager domain name.</span></span>

![Trafik Yöneticisi'ni kullanarak ağırlıklı trafik yönlendirme yöntemini yapılandırma][1]

## <a name="next-steps"></a><span data-ttu-id="1e268-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1e268-130">Next steps</span></span>

- <span data-ttu-id="1e268-131">Hakkında bilgi edinin [öncelik trafik yönlendirme yöntemini](traffic-manager-configure-priority-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="1e268-131">Learn about [priority traffic routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="1e268-132">Hakkında bilgi edinin [performans trafik yönlendirme yöntemini](traffic-manager-configure-performance-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="1e268-132">Learn about [performance traffic routing method](traffic-manager-configure-performance-routing-method.md).</span></span>
- <span data-ttu-id="1e268-133">Hakkında bilgi edinin [coğrafi yönlendirme yöntemi](traffic-manager-configure-geographic-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="1e268-133">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="1e268-134">Nasıl çok öğrenin[test trafik Yöneticisi Ayarları](traffic-manager-testing-settings.md).</span><span class="sxs-lookup"><span data-stu-id="1e268-134">Learn how too[test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-weighted-routing-method/traffic-manager-weighted-routing-method.png
