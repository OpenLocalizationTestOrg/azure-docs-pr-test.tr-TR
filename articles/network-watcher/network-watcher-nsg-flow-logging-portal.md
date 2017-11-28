---
title: "Azure Ağ İzleyicisi ile aaaManage ağ güvenlik grubu akış günlükleri | Microsoft Docs"
description: "Bu sayfayı toomanage ağ güvenlik grubu akış Azure Ağ İzleyicisi'ni nasıl günlüğe yazacağını açıklar"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 01606cbf-d70b-40ad-bc1d-f03bb642e0af
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fb250337ab9d1a0c0d0d3569c00bc221dd102a3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-group-flow-logs-in-hello-azure-portal"></a><span data-ttu-id="add29-103">Ağ güvenlik grubu akış günlükleri hello Azure portalı Yönet</span><span class="sxs-lookup"><span data-stu-id="add29-103">Manage network security group flow logs in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="add29-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="add29-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="add29-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="add29-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="add29-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="add29-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="add29-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="add29-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="add29-108">REST API</span><span class="sxs-lookup"><span data-stu-id="add29-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="add29-109">Ağ güvenlik grubu akış günlükleri, giriş ve çıkış IP trafiği bir ağ güvenlik grubu aracılığıyla tooview bilgilerini sağlayan Ağ İzleyicisi özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="add29-109">Network security group flow logs are a feature of Network Watcher that enables you tooview information about ingress and egress IP traffic through a network security group.</span></span> <span data-ttu-id="add29-110">Bu akış günlükleri JSON biçiminde yazılmıştır ve önemli bilgiler sağlayan dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="add29-110">These flow logs are written in JSON format and provide important information, including:</span></span> 

- <span data-ttu-id="add29-111">Giden ve gelen akış kuralı başına temelinde.</span><span class="sxs-lookup"><span data-stu-id="add29-111">Outbound and inbound flows on a per-rule basis.</span></span>
- <span data-ttu-id="add29-112">Merhaba akış hello NIC uygular.</span><span class="sxs-lookup"><span data-stu-id="add29-112">hello NIC that hello flow applies to.</span></span>
- <span data-ttu-id="add29-113">5-tanımlama grubu hello akış (kaynak/hedef IP, kaynak/hedef bağlantı noktası, protokol) hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="add29-113">5-tuple information about hello flow (source/destination IP, source/destination port, protocol).</span></span>
- <span data-ttu-id="add29-114">Trafik izin verilen veya reddedilen hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="add29-114">Information about whether traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="add29-115">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="add29-115">Before you begin</span></span>

<span data-ttu-id="add29-116">Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi örneği oluşturmayı](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="add29-116">This scenario assumes you have already followed hello steps in [Create a Network Watcher instance](network-watcher-create.md).</span></span> <span data-ttu-id="add29-117">Merhaba senaryo aynı zamanda bir sahip olduğunuz geçerli bir sanal makine ile bir kaynak grubu varsayar.</span><span class="sxs-lookup"><span data-stu-id="add29-117">hello scenario also assumes that a you have a resource group with a valid virtual machine.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="add29-118">Öngörüler sağlayıcısını Kaydet</span><span class="sxs-lookup"><span data-stu-id="add29-118">Register Insights provider</span></span>

<span data-ttu-id="add29-119">Akış günlüğü toowork başarıyla hello **Microsoft.ınsights** sağlayıcı kaydedilmelidir.</span><span class="sxs-lookup"><span data-stu-id="add29-119">For flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="add29-120">tooregister hello sağlayıcısı, aşağıdaki adımları gerçekleştirin hello:</span><span class="sxs-lookup"><span data-stu-id="add29-120">tooregister hello provider, take hello following steps:</span></span> 

1. <span data-ttu-id="add29-121">Çok Git**abonelikleri**ve ardından istediğiniz tooenable akış günlükleri hello abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="add29-121">Go too**Subscriptions**, and then select hello subscription for which you want tooenable flow logs.</span></span> 
2. <span data-ttu-id="add29-122">Merhaba üzerinde **abonelik** dikey penceresinde, select **kaynak sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="add29-122">On hello **Subscription** blade, select **Resource Providers**.</span></span> 
3. <span data-ttu-id="add29-123">Ara sağlayıcılarının hello listesini ve o hello doğrulayın **Microsoft.ınsights** sağlayıcı kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="add29-123">Look at hello list of providers, and verify that hello **microsoft.insights** provider is registered.</span></span> <span data-ttu-id="add29-124">Aksi takdirde, ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="add29-124">If not, then select **Register**.</span></span>

![Görünüm sağlayıcıları][providers]

## <a name="enable-flow-logs"></a><span data-ttu-id="add29-126">Akış günlükleri etkinleştir</span><span class="sxs-lookup"><span data-stu-id="add29-126">Enable flow logs</span></span>

<span data-ttu-id="add29-127">Bu adımları bir ağ güvenlik grubu akışı açtığında etkinleştirme hello işlemi uygulayın.</span><span class="sxs-lookup"><span data-stu-id="add29-127">These steps take you through hello process of enabling flow logs on a network security group.</span></span>

### <a name="step-1"></a><span data-ttu-id="add29-128">1. Adım</span><span class="sxs-lookup"><span data-stu-id="add29-128">Step 1</span></span>

<span data-ttu-id="add29-129">Tooa Ağ İzleyicisi örneğine gidin ve ardından **NSG akış günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="add29-129">Go tooa Network Watcher instance, and then select **NSG Flow logs**.</span></span>

![Akış günlükleri genel bakış][1]

### <a name="step-2"></a><span data-ttu-id="add29-131">2. Adım</span><span class="sxs-lookup"><span data-stu-id="add29-131">Step 2</span></span>

<span data-ttu-id="add29-132">Bir ağ güvenlik grubu hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="add29-132">Select a network security group from hello list.</span></span>

![Akış günlükleri genel bakış][2]

### <a name="step-3"></a><span data-ttu-id="add29-134">3. Adım</span><span class="sxs-lookup"><span data-stu-id="add29-134">Step 3</span></span> 

<span data-ttu-id="add29-135">Merhaba üzerinde **akışı günlüklerinin ayarları** dikey penceresinde hello durumu çok Ayarla**üzerinde**ve ardından bir depolama hesabı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="add29-135">On hello **Flow logs settings** blade, set hello status too**On**, and then configure a storage account.</span></span>  <span data-ttu-id="add29-136">İşiniz bittiğinde seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="add29-136">When you're done, select **OK**.</span></span> <span data-ttu-id="add29-137">Ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="add29-137">Then select **Save**.</span></span>

![Akış günlükleri genel bakış][3]

## <a name="download-flow-logs"></a><span data-ttu-id="add29-139">Akış günlükleri indirmek</span><span class="sxs-lookup"><span data-stu-id="add29-139">Download flow logs</span></span>

<span data-ttu-id="add29-140">Akış günlükleri, bir depolama hesabında kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="add29-140">Flow logs are saved in a storage account.</span></span> <span data-ttu-id="add29-141">Akış günlükleri tooview karşıdan bunları.</span><span class="sxs-lookup"><span data-stu-id="add29-141">Download your flow logs tooview them.</span></span>

### <a name="step-1"></a><span data-ttu-id="add29-142">1. Adım</span><span class="sxs-lookup"><span data-stu-id="add29-142">Step 1</span></span>

<span data-ttu-id="add29-143">toodownload akış günlükleri, seçin **akış günlükleri yapılandırılan depolama hesaplarından indirebilirsiniz**.</span><span class="sxs-lookup"><span data-stu-id="add29-143">toodownload flow logs, select **You can download flow logs from configured storage accounts**.</span></span> <span data-ttu-id="add29-144">Bu adım hangi günlükleri toodownload seçebileceğiniz tooa depolama hesabı görünümüne alır.</span><span class="sxs-lookup"><span data-stu-id="add29-144">This step takes you tooa storage account view where you can choose which logs toodownload.</span></span>

![Akış günlükleri ayarlarını][4]

### <a name="step-2"></a><span data-ttu-id="add29-146">2. Adım</span><span class="sxs-lookup"><span data-stu-id="add29-146">Step 2</span></span>

<span data-ttu-id="add29-147">Toohello doğru depolama hesabına gidin.</span><span class="sxs-lookup"><span data-stu-id="add29-147">Go toohello correct storage account.</span></span> <span data-ttu-id="add29-148">Ardından **kapsayıcıları** > **Öngörüler günlük networksecuritygroupflowevent**.</span><span class="sxs-lookup"><span data-stu-id="add29-148">Then select **Containers** > **insights-log-networksecuritygroupflowevent**.</span></span>

![Akış günlükleri ayarlarını][5]

### <a name="step-3"></a><span data-ttu-id="add29-150">3. Adım</span><span class="sxs-lookup"><span data-stu-id="add29-150">Step 3</span></span>

<span data-ttu-id="add29-151">Merhaba akış günlüğü toohello konumuna gidin, onu seçin ve ardından **karşıdan**.</span><span class="sxs-lookup"><span data-stu-id="add29-151">Go toohello location of hello flow log, select it, and then select **Download**.</span></span>

![Akış günlükleri ayarlarını][6]

<span data-ttu-id="add29-153">Merhaba günlük hello yapısı hakkında daha fazla bilgi için ziyaret [ağ güvenlik grubu akışı günlüğü genel bakış](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="add29-153">For information about hello structure of hello log, visit [Network security group flow log overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="add29-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="add29-154">Next steps</span></span>

<span data-ttu-id="add29-155">Nasıl çok öğrenin[NSG akış günlüklerinizi Powerbı ile görselleştirme](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="add29-155">Learn how too[visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
