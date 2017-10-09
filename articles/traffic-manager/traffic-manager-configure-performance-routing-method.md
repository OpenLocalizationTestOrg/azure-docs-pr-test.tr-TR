---
title: "aaaConfigure performans trafik yönlendirme yöntemini Azure trafik Yöneticisi'ni kullanarak | Microsoft Docs"
description: "Bu makalede, nasıl tooconfigure trafik Yöneticisi tooroute trafiği toohello bitiş noktası ile düşük gecikme açıklanmaktadır."
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
ms.openlocfilehash: d0ccd4c9de411844c6f36068859265244f4aa52b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-performance-traffic-routing-method"></a><span data-ttu-id="c81f9-103">Merhaba performans trafik yönlendirme yöntemini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c81f9-103">Configure hello performance traffic routing method</span></span>

<span data-ttu-id="c81f9-104">Merhaba performans trafik yönlendirme yöntemini hello hello istemcinin ağdan en düşük gecikme süresi ile toodirect trafiği toohello uç noktası sağlar.</span><span class="sxs-lookup"><span data-stu-id="c81f9-104">hello Performance traffic routing method allows you toodirect traffic toohello endpoint with hello lowest latency from hello client's network.</span></span> <span data-ttu-id="c81f9-105">Genellikle coğrafi uzaklığı en yakın hello hello datacenter hello en düşük gecikme süresine sahip olur.</span><span class="sxs-lookup"><span data-stu-id="c81f9-105">Typically, hello datacenter with hello lowest latency is hello closest in geographic distance.</span></span> <span data-ttu-id="c81f9-106">Bu trafik yönlendirme yöntemini ağ yapılandırmasında gerçek zamanlı değişiklikleri hesaba veya yük.</span><span class="sxs-lookup"><span data-stu-id="c81f9-106">This traffic routing method cannot account for real-time changes in network configuration or load.</span></span>

##  <a name="tooconfigure-performance-routing-method"></a><span data-ttu-id="c81f9-107">tooconfigure performans yönlendirme yöntemi</span><span class="sxs-lookup"><span data-stu-id="c81f9-107">tooconfigure performance routing method</span></span>

1. <span data-ttu-id="c81f9-108">Toohello içinde bir tarayıcıdan oturum [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c81f9-108">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="c81f9-109">Henüz bir hesabınız yoksa, [bir aylık ücretsiz denemeye](https://azure.microsoft.com/free/) kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c81f9-109">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="c81f9-110">Merhaba Hello portal'ın arama çubuğunda arama **Traffic Manager profillerini** ve tooconfigure hello yönlendirme yöntemi için istediğiniz hello profilinin adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="c81f9-110">In hello portal’s search bar, search for hello **Traffic Manager profiles** and then click hello profile name that you want tooconfigure hello routing method for.</span></span>
3. <span data-ttu-id="c81f9-111">Merhaba, **trafik Yöneticisi profili** dikey penceresinde, hem bulut Hizmetleri hello ve tooinclude yapılandırmanızda istediğiniz Web siteleri mevcut olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c81f9-111">In hello **Traffic Manager profile** blade, verify that both hello cloud services and websites that you want tooinclude in your configuration are present.</span></span>
4. <span data-ttu-id="c81f9-112">Merhaba, **ayarları** 'yi tıklatın **yapılandırma**ve hello **yapılandırma** dikey penceresinde, aşağıdaki gibi tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="c81f9-112">In hello **Settings** section, click **Configuration**, and in hello **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="c81f9-113">İçin **yönlendirme yöntemi ayarları trafiği**, için **yönlendirme yöntemi** seçin **performans**.</span><span class="sxs-lookup"><span data-stu-id="c81f9-113">For **traffic routing method settings**, for **Routing method** select **Performance**.</span></span>
    2. <span data-ttu-id="c81f9-114">Set hello **uç nokta izleme ayarları** aynı şekilde bu profili içindeki tüm her uç noktası için:</span><span class="sxs-lookup"><span data-stu-id="c81f9-114">Set hello **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="c81f9-115">Select hello uygun **Protokolü**ve hello belirtin **bağlantı noktası** numarası.</span><span class="sxs-lookup"><span data-stu-id="c81f9-115">Select hello appropriate **Protocol**, and specify hello **Port** number.</span></span> 
        2. <span data-ttu-id="c81f9-116">İçin **yolu** eğik yazın  */* .</span><span class="sxs-lookup"><span data-stu-id="c81f9-116">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="c81f9-117">toomonitor uç noktaları, yol ve dosya adı belirtmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="c81f9-117">toomonitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="c81f9-118">Bir eğik çizgi "/" Merhaba göreli yolu geçerli bir girişi ve o hello dosyadır hello kök dizininde (varsayılan) anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="c81f9-118">A forward slash "/" is a valid entry for hello relative path and implies that hello file is in hello root directory (default).</span></span>
        3. <span data-ttu-id="c81f9-119">Merhaba hello sayfanın en üstünde, tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="c81f9-119">At hello top of hello page, click **Save**.</span></span>
5.  <span data-ttu-id="c81f9-120">Merhaba değişiklikleri yapılandırmanızda gibi test edin:</span><span class="sxs-lookup"><span data-stu-id="c81f9-120">Test hello changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="c81f9-121">Hello portal'ın arama çubuğunda hello trafik Yöneticisi profili adını arayın ve görüntülenen o hello hello sonuçlarında hello trafik Yöneticisi profiline tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c81f9-121">In hello portal’s search bar, search for hello Traffic Manager profile name and click hello Traffic Manager profile in hello results that hello displayed.</span></span>
    2.  <span data-ttu-id="c81f9-122">Merhaba, **trafik Yöneticisi** profil dikey penceresinde, tıklatın **genel bakış**.</span><span class="sxs-lookup"><span data-stu-id="c81f9-122">In hello **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="c81f9-123">Merhaba **trafik Yöneticisi profili** dikey penceresinde, yeni oluşturulan Traffic Manager profilinizin hello DNS adını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="c81f9-123">hello **Traffic Manager profile** blade displays hello DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="c81f9-124">Bu herhangi (örneğin, göre bir web tarayıcısı kullanarak tooit gezinme) istemcileri yönlendirilen tooget toohello sağ uç nokta hello yönlendirme türü tarafından belirlendiği şekilde tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c81f9-124">This can be used by any clients (for example, by navigating tooit using a web browser) tooget routed toohello right endpoint as determined by hello routing type.</span></span> <span data-ttu-id="c81f9-125">Bu durumda tüm istekleri hello hello istemcinin ağdan en düşük gecikme süresine sahip yönlendirilmiş toohello uç nokta var.</span><span class="sxs-lookup"><span data-stu-id="c81f9-125">In this case all requests are routed toohello endpoint with hello lowest latency from hello client's network.</span></span>
6. <span data-ttu-id="c81f9-126">Traffic Manager profilinizin çalışma sonra şirket etki alanı adı toohello trafik yöneticisi etki alanı adı, yetkili DNS sunucusu toopoint hello DNS kaydını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="c81f9-126">Once your Traffic Manager profile is working, edit hello DNS record on your authoritative DNS server toopoint your company domain name toohello Traffic Manager domain name.</span></span>

![Trafik Yöneticisi'ni kullanarak performans trafik yönlendirme yöntemini yapılandırma][1]

## <a name="next-steps"></a><span data-ttu-id="c81f9-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c81f9-128">Next steps</span></span>

- <span data-ttu-id="c81f9-129">Hakkında bilgi edinin [ağırlıklı trafik yönlendirme yöntemini](traffic-manager-configure-weighted-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="c81f9-129">Learn about [weighted traffic routing method](traffic-manager-configure-weighted-routing-method.md).</span></span>
- <span data-ttu-id="c81f9-130">Hakkında bilgi edinin [öncelik yönlendirme yöntemi](traffic-manager-configure-priority-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="c81f9-130">Learn about [priority routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="c81f9-131">Hakkında bilgi edinin [coğrafi yönlendirme yöntemi](traffic-manager-configure-geographic-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="c81f9-131">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="c81f9-132">Nasıl çok öğrenin[test trafik Yöneticisi Ayarları](traffic-manager-testing-settings.md).</span><span class="sxs-lookup"><span data-stu-id="c81f9-132">Learn how too[test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-performance-routing-method/traffic-manager-performance-routing-method.png