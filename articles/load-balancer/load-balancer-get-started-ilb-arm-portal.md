---
title: "bir iç yük dengeleyici - Azure portalında aaaCreate | Microsoft Docs"
description: "Nasıl toocreate bir dahili yük dengeleyici kaynak hello Azure portal kullanarak Yöneticisi'nde öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ac14fb9-8d14-4892-bfe6-8bc74c48ae2c
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 80124217a84857b542eb41cb814ec97234176dd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-in-hello-azure-portal"></a><span data-ttu-id="859f7-103">Bir iç yük dengeleyici hello Azure portal oluşturma</span><span class="sxs-lookup"><span data-stu-id="859f7-103">Create an Internal load balancer in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="859f7-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="859f7-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="859f7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="859f7-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="859f7-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="859f7-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="859f7-107">Şablon</span><span class="sxs-lookup"><span data-stu-id="859f7-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="859f7-108">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="859f7-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="859f7-109">Bu makalede, kullanarak yer almaktadır hello yerine çoğu yeni dağıtımlar için Microsoft önerir hello Resource Manager dağıtım modeli [Klasik dağıtım modeli](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="859f7-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a><span data-ttu-id="859f7-110">Azure portalını kullanarak iç yük dengeleyici oluşturmaya başlama</span><span class="sxs-lookup"><span data-stu-id="859f7-110">Get started creating an Internal load balancer using Azure portal</span></span>

<span data-ttu-id="859f7-111">Hello Azure Portalı ' adımları toocreate bir iç yük dengeleyici aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="859f7-111">Use hello following steps toocreate an internal load balancer from hello Azure Portal.</span></span>

1. <span data-ttu-id="859f7-112">Bir tarayıcı açın, toohello gidin [Azure portal](http://portal.azure.com)ve Azure hesabınızla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="859f7-112">Open a browser, navigate toohello [Azure portal](http://portal.azure.com), and sign in with your Azure account.</span></span>
2. <span data-ttu-id="859f7-113">Merhaba üst sol taraftaki hello ekranının, tıklatın **yeni** > **ağ** > **yük dengeleyici**.</span><span class="sxs-lookup"><span data-stu-id="859f7-113">In hello upper left hand side of hello screen, click **New** > **Networking** > **Load balancer**.</span></span>
3. <span data-ttu-id="859f7-114">Merhaba, **oluşturma yük dengeleyici** dikey penceresinde girin bir **adı** , yük dengeleyici için.</span><span class="sxs-lookup"><span data-stu-id="859f7-114">In hello **Create load balancer** blade, enter a **Name** for your load balancer.</span></span>
4. <span data-ttu-id="859f7-115">**Düzen** bölümünde **İç**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="859f7-115">Under **Scheme**, click **Internal**.</span></span>
5. <span data-ttu-id="859f7-116">Tıklatın **sanal ağ**, ve ardından istediğiniz yere toocreate hello yük dengeleyici sanal ağ seçin hello.</span><span class="sxs-lookup"><span data-stu-id="859f7-116">Click **Virtual network**, and then select hello virtual network where you want toocreate hello load balancer.</span></span>

   > [!NOTE]
   > <span data-ttu-id="859f7-117">Merhaba sanal ağ toouse istediğiniz görmüyorsanız hello denetleyin **konumu** hello yük dengeleyicisi kullanıyorsanız ve uygun şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="859f7-117">If you do not see hello virtual network you want toouse, check hello **Location** you are using for hello load balancer, and change it accordingly.</span></span>

6. <span data-ttu-id="859f7-118">Tıklatın **alt**ve ardından istediğiniz yere toocreate hello yük dengeleyici hello alt ağ seçin.</span><span class="sxs-lookup"><span data-stu-id="859f7-118">Click **Subnet**, and then select hello subnet where you want toocreate hello load balancer.</span></span>
7. <span data-ttu-id="859f7-119">Altında **IP adresi ataması**, tıklayın **dinamik** veya **statik**veya başlangıç IP adresi sabit hello yük dengeleyici toobe için (statik) isteyip istemediğinizi bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="859f7-119">Under **IP address assignment**, click either **Dynamic** or **Static**, depending on whether you want hello IP address for hello load balancer toobe fixed (static) or not.</span></span>

   > [!NOTE]
   > <span data-ttu-id="859f7-120">Statik bir IP adresi toouse seçerseniz, hello yük dengeleyici için bir adres tooprovide gerekir.</span><span class="sxs-lookup"><span data-stu-id="859f7-120">If you select toouse a static IP address, you will have tooprovide an address for hello load balancer.</span></span>

8. <span data-ttu-id="859f7-121">Altında **kaynak grubu** hello hello yük dengeleyici için yeni bir kaynak grubu adını belirtin ya da tıklatın **Varolanı seç** ve varolan bir kaynak grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="859f7-121">Under **Resource group** either specify hello name of a new resource group for hello load balancer, or click **select existing** and select an existing resource group.</span></span>
9. <span data-ttu-id="859f7-122">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="859f7-122">Click **Create**.</span></span>

## <a name="configure-load-balancing-rules"></a><span data-ttu-id="859f7-123">Yük dengeleme kurallarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="859f7-123">Configure load balancing rules</span></span>

<span data-ttu-id="859f7-124">Merhaba sonra Yük Dengeleyici oluşturma, toohello yük dengeleyici kaynak tooconfigure gidin.</span><span class="sxs-lookup"><span data-stu-id="859f7-124">After hello load balancer creation, navigate toohello load balancer resource tooconfigure it.</span></span>
<span data-ttu-id="859f7-125">Tooconfigure önce bir arka uç adres havuzu ve bir araştırma Yük Dengeleme kuralı yapılandırmadan önce gerekir.</span><span class="sxs-lookup"><span data-stu-id="859f7-125">You need tooconfigure first a back-end address pool and a probe before configuring a load balancing rule.</span></span>

### <a name="step-1-configure-a-back-end-pool"></a><span data-ttu-id="859f7-126">1. Adım: Arka uç havuzu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="859f7-126">Step 1: Configure a back-end pool</span></span>

1. <span data-ttu-id="859f7-127">Hello Azure portal'ı tıklatın **Gözat** > **yük dengeleyici**, yukarıda oluşturduğunuz hello yük dengeleyici'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="859f7-127">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="859f7-128">Merhaba, **ayarları** dikey penceresinde tıklatın **arka uç havuzları**.</span><span class="sxs-lookup"><span data-stu-id="859f7-128">In hello **Settings** blade, click **Backend pools**.</span></span>
3. <span data-ttu-id="859f7-129">Merhaba, **arka uç adres havuzlarında** dikey penceresinde tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="859f7-129">In hello **Backend address pools** blade, click **Add**.</span></span>
4. <span data-ttu-id="859f7-130">Merhaba, **arka uç havuzu ekleme** dikey penceresinde girin bir **adı** hello arka uç havuzu ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="859f7-130">In hello **Add backend pool** blade, enter a **Name** for hello backend pool, and then click **OK**.</span></span>

### <a name="step-2-configure-a-probe"></a><span data-ttu-id="859f7-131">2. Adım: Araştırma yapılandırma</span><span class="sxs-lookup"><span data-stu-id="859f7-131">Step 2: Configure a probe</span></span>

1. <span data-ttu-id="859f7-132">Hello Azure portal'ı tıklatın **Gözat** > **yük dengeleyici**, yukarıda oluşturduğunuz hello yük dengeleyici'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="859f7-132">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="859f7-133">Merhaba, **ayarları** dikey penceresinde tıklatın **yoklamaları**.</span><span class="sxs-lookup"><span data-stu-id="859f7-133">In hello **Settings** blade, click **Probes**.</span></span>
3. <span data-ttu-id="859f7-134">Merhaba, **yoklamaları** dikey penceresinde tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="859f7-134">In hello **Probes**  blade, click **Add**.</span></span>
4. <span data-ttu-id="859f7-135">Merhaba, **Ekle araştırma** dikey penceresinde girin bir **adı** hello araştırma için.</span><span class="sxs-lookup"><span data-stu-id="859f7-135">In hello **Add probe** blade, enter a **Name** for hello probe.</span></span>
5. <span data-ttu-id="859f7-136">**Protokol**’ün altında **HTTP** (web siteleri için) veya **TCP** (diğer TCP tabanlı uygulamalar için) seçin.</span><span class="sxs-lookup"><span data-stu-id="859f7-136">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="859f7-137">Altında **bağlantı noktası**, başlangıç bağlantı noktası toouse hello araştırma erişirken belirtin.</span><span class="sxs-lookup"><span data-stu-id="859f7-137">Under **Port**, specify hello port toouse when accessing hello probe.</span></span>
7. <span data-ttu-id="859f7-138">Altında **yolu** (HTTP için yalnızca araştırmalarının), hello yolu toouse bir araştırma belirtin.</span><span class="sxs-lookup"><span data-stu-id="859f7-138">Under **Path** (for HTTP probes only), specify hello path toouse as a probe.</span></span>
8. <span data-ttu-id="859f7-139">Altında **aralığı** ne sıklıkta tooprobe hello uygulama belirtin.</span><span class="sxs-lookup"><span data-stu-id="859f7-139">Under **Interval** specify how frequently tooprobe hello application.</span></span>
9. <span data-ttu-id="859f7-140">Altında **sağlıksız durum eşiği**, hello arka uç sanal makine olarak sağlıksız olarak işaretlenmiş önce kaç tane denemeleri başarısız belirtin.</span><span class="sxs-lookup"><span data-stu-id="859f7-140">Under **Unhealthy threshold**, specify how many attempts should fail before hello backend virtual machine is marked as unhealthy.</span></span>
10. <span data-ttu-id="859f7-141">Tıklatın **Tamam** toocreate araştırma.</span><span class="sxs-lookup"><span data-stu-id="859f7-141">Click **OK** toocreate probe.</span></span>

### <a name="step-3-configure-load-balancing-rules"></a><span data-ttu-id="859f7-142">3. Adım: Yük dengeleme kurallarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="859f7-142">Step 3: Configure load balancing rules</span></span>

1. <span data-ttu-id="859f7-143">Hello Azure portal'ı tıklatın **Gözat** > **yük dengeleyici**, yukarıda oluşturduğunuz hello yük dengeleyici'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="859f7-143">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="859f7-144">Merhaba, **ayarları** dikey penceresinde tıklatın **Yük Dengeleme kuralları**.</span><span class="sxs-lookup"><span data-stu-id="859f7-144">In hello **Settings** blade, click **Load balancing rules**.</span></span>
3. <span data-ttu-id="859f7-145">Merhaba, **Yük Dengeleme kuralları** dikey penceresinde tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="859f7-145">In hello **Load balancing rules** blade, click **Add**.</span></span>
4. <span data-ttu-id="859f7-146">Merhaba, **Ekle Yük Dengeleme kuralını** dikey penceresinde girin bir **adı** hello kuralı için.</span><span class="sxs-lookup"><span data-stu-id="859f7-146">In hello **Add load balancing rule** blade, enter a **Name** for hello rule.</span></span>
5. <span data-ttu-id="859f7-147">**Protokol**’ün altında **HTTP** (web siteleri için) veya **TCP** (diğer TCP tabanlı uygulamalar için) seçin.</span><span class="sxs-lookup"><span data-stu-id="859f7-147">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="859f7-148">Altında **bağlantı noktası**, başlangıç bağlantı noktası istemcileri bağlama tooin hello yük dengeleyici belirtin.</span><span class="sxs-lookup"><span data-stu-id="859f7-148">Under **Port**, specify hello port clients connect tooin hello load balancer.</span></span>
7. <span data-ttu-id="859f7-149">Altında **arka uç bağlantı noktası**, başlangıç bağlantı noktası toobe hello arka uç havuzunda kullanılan belirtin (genellikle hello yük dengeleyici bağlantı noktası ve hello arka uç bağlantı noktası olan hello aynı).</span><span class="sxs-lookup"><span data-stu-id="859f7-149">Under **Backend port**, specify hello port toobe used in hello backend pool (usually, hello load balancer port and hello backend port are hello same).</span></span>
8. <span data-ttu-id="859f7-150">Altında **arka uç havuzu**seçin hello arka uç havuzu, yukarıda oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="859f7-150">Under **Backend pool**, select hello backend pool you created above.</span></span>
9. <span data-ttu-id="859f7-151">Altında **oturum kalıcılığını**, oturumlar toopersist istediğiniz yöntemini seçin.</span><span class="sxs-lookup"><span data-stu-id="859f7-151">Under **Session persistence**, select how you want sessions toopersist.</span></span>
10. <span data-ttu-id="859f7-152">Altında **boşta kalma zaman aşımı (dakika)**, hello boşta kalma zaman aşımı belirtin.</span><span class="sxs-lookup"><span data-stu-id="859f7-152">Under **Idle timeout (minutes)**, specify hello idle timeout.</span></span>
11. <span data-ttu-id="859f7-153">**Kayan IP (doğrudan sunucu dönüşü)** bölümünde **Devre dışı** veya **Etkin**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="859f7-153">Under **Floating IP (direct server return)**, click **Disabled** or **Enabled**.</span></span>
12. <span data-ttu-id="859f7-154">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="859f7-154">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="859f7-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="859f7-155">Next steps</span></span>

[<span data-ttu-id="859f7-156">Yük dengeleyici dağıtım modu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="859f7-156">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="859f7-157">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="859f7-157">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

