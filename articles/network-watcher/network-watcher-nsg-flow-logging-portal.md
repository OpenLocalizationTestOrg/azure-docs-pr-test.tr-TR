---
title: "Ağ güvenlik grubu akış günlükleri Azure Ağ İzleyicisi ile yönetme | Microsoft Docs"
description: "Bu sayfa, ağ güvenlik grubu akış günlüklerine Azure Ağ İzleyicisi'ni yönetmek açıklanmaktadır"
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
ms.openlocfilehash: 41cb5ffab9bd3a3bed75ffdb6a7383ca1690f810
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-group-flow-logs-in-the-azure-portal"></a><span data-ttu-id="a8e1c-103">Ağ güvenlik grubu akış günlükleri Azure portalında Yönet</span><span class="sxs-lookup"><span data-stu-id="a8e1c-103">Manage network security group flow logs in the Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a8e1c-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="a8e1c-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="a8e1c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a8e1c-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="a8e1c-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a8e1c-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="a8e1c-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a8e1c-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="a8e1c-108">REST API</span><span class="sxs-lookup"><span data-stu-id="a8e1c-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="a8e1c-109">Ağ güvenlik grubu akış günlükleri, giriş ve çıkış IP trafiği bir ağ güvenlik grubu ile ilgili bilgileri görüntülemek sağlayan Ağ İzleyicisi özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-109">Network security group flow logs are a feature of Network Watcher that enables you to view information about ingress and egress IP traffic through a network security group.</span></span> <span data-ttu-id="a8e1c-110">Bu akış günlükleri JSON biçiminde yazılmıştır ve önemli bilgiler sağlayan dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="a8e1c-110">These flow logs are written in JSON format and provide important information, including:</span></span> 

- <span data-ttu-id="a8e1c-111">Giden ve gelen akış kuralı başına temelinde.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-111">Outbound and inbound flows on a per-rule basis.</span></span>
- <span data-ttu-id="a8e1c-112">Akış uygulandığı NIC.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-112">The NIC that the flow applies to.</span></span>
- <span data-ttu-id="a8e1c-113">5-tanımlama grubu (kaynak/hedef IP, kaynak/hedef bağlantı noktası, protokol) akışı hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-113">5-tuple information about the flow (source/destination IP, source/destination port, protocol).</span></span>
- <span data-ttu-id="a8e1c-114">Trafik izin verilen veya reddedilen hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-114">Information about whether traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a8e1c-115">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="a8e1c-115">Before you begin</span></span>

<span data-ttu-id="a8e1c-116">Bu senaryo zaten izlediğiniz adımlarda varsayar [bir Ağ İzleyicisi örneği oluşturmayı](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="a8e1c-116">This scenario assumes you have already followed the steps in [Create a Network Watcher instance](network-watcher-create.md).</span></span> <span data-ttu-id="a8e1c-117">Senaryo aynı zamanda bir olduğu geçerli bir sanal makine ile bir kaynak grubu varsayılır.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-117">The scenario also assumes that a you have a resource group with a valid virtual machine.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="a8e1c-118">Öngörüler sağlayıcısını Kaydet</span><span class="sxs-lookup"><span data-stu-id="a8e1c-118">Register Insights provider</span></span>

<span data-ttu-id="a8e1c-119">Başarılı bir şekilde çalışması için günlük akışı **Microsoft.ınsights** sağlayıcı kaydedilmelidir.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-119">For flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="a8e1c-120">Sağlayıcıyı kaydetmek için aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="a8e1c-120">To register the provider, take the following steps:</span></span> 

1. <span data-ttu-id="a8e1c-121">Git **abonelikleri**ve akış günlükleri etkinleştirmek istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-121">Go to **Subscriptions**, and then select the subscription for which you want to enable flow logs.</span></span> 
2. <span data-ttu-id="a8e1c-122">Üzerinde **abonelik** dikey penceresinde, select **kaynak sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-122">On the **Subscription** blade, select **Resource Providers**.</span></span> 
3. <span data-ttu-id="a8e1c-123">Ara sağlayıcılar listesi ve doğrulayın **Microsoft.ınsights** sağlayıcı kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-123">Look at the list of providers, and verify that the **microsoft.insights** provider is registered.</span></span> <span data-ttu-id="a8e1c-124">Aksi takdirde, ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-124">If not, then select **Register**.</span></span>

![Görünüm sağlayıcıları][providers]

## <a name="enable-flow-logs"></a><span data-ttu-id="a8e1c-126">Akış günlükleri etkinleştir</span><span class="sxs-lookup"><span data-stu-id="a8e1c-126">Enable flow logs</span></span>

<span data-ttu-id="a8e1c-127">Bu adımları bir ağ güvenlik grubu akışı açtığında etkinleştirme işlemi uygulayın.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-127">These steps take you through the process of enabling flow logs on a network security group.</span></span>

### <a name="step-1"></a><span data-ttu-id="a8e1c-128">1. Adım</span><span class="sxs-lookup"><span data-stu-id="a8e1c-128">Step 1</span></span>

<span data-ttu-id="a8e1c-129">Ağ İzleyicisi örneğine gidin ve ardından **NSG akış günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-129">Go to a Network Watcher instance, and then select **NSG Flow logs**.</span></span>

![Akış günlükleri genel bakış][1]

### <a name="step-2"></a><span data-ttu-id="a8e1c-131">2. Adım</span><span class="sxs-lookup"><span data-stu-id="a8e1c-131">Step 2</span></span>

<span data-ttu-id="a8e1c-132">Bir ağ güvenlik grubu listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-132">Select a network security group from the list.</span></span>

![Akış günlükleri genel bakış][2]

### <a name="step-3"></a><span data-ttu-id="a8e1c-134">3. Adım</span><span class="sxs-lookup"><span data-stu-id="a8e1c-134">Step 3</span></span> 

<span data-ttu-id="a8e1c-135">Üzerinde **akışı günlüklerinin ayarları** dikey penceresinde ayarlanmış durumu **üzerinde**ve ardından bir depolama hesabı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-135">On the **Flow logs settings** blade, set the status to **On**, and then configure a storage account.</span></span>  <span data-ttu-id="a8e1c-136">İşiniz bittiğinde seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-136">When you're done, select **OK**.</span></span> <span data-ttu-id="a8e1c-137">Ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-137">Then select **Save**.</span></span>

![Akış günlükleri genel bakış][3]

## <a name="download-flow-logs"></a><span data-ttu-id="a8e1c-139">Akış günlükleri indirmek</span><span class="sxs-lookup"><span data-stu-id="a8e1c-139">Download flow logs</span></span>

<span data-ttu-id="a8e1c-140">Akış günlükleri, bir depolama hesabında kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-140">Flow logs are saved in a storage account.</span></span> <span data-ttu-id="a8e1c-141">Bunları görüntülemek için akış günlüklerinizi indirin.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-141">Download your flow logs to view them.</span></span>

### <a name="step-1"></a><span data-ttu-id="a8e1c-142">1. Adım</span><span class="sxs-lookup"><span data-stu-id="a8e1c-142">Step 1</span></span>

<span data-ttu-id="a8e1c-143">Akış günlükleri indirmek için seçin **akış günlükleri yapılandırılan depolama hesaplarından indirebilirsiniz**.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-143">To download flow logs, select **You can download flow logs from configured storage accounts**.</span></span> <span data-ttu-id="a8e1c-144">Bu adım hangi günlükleri indirmek için seçebileceğiniz bir depolama hesabı görünümüne alır.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-144">This step takes you to a storage account view where you can choose which logs to download.</span></span>

![Akış günlükleri ayarlarını][4]

### <a name="step-2"></a><span data-ttu-id="a8e1c-146">2. Adım</span><span class="sxs-lookup"><span data-stu-id="a8e1c-146">Step 2</span></span>

<span data-ttu-id="a8e1c-147">Doğru depolama hesabınıza gidin.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-147">Go to the correct storage account.</span></span> <span data-ttu-id="a8e1c-148">Ardından **kapsayıcıları** > **Öngörüler günlük networksecuritygroupflowevent**.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-148">Then select **Containers** > **insights-log-networksecuritygroupflowevent**.</span></span>

![Akış günlükleri ayarlarını][5]

### <a name="step-3"></a><span data-ttu-id="a8e1c-150">3. Adım</span><span class="sxs-lookup"><span data-stu-id="a8e1c-150">Step 3</span></span>

<span data-ttu-id="a8e1c-151">Akış günlüğü konuma seçin ve ardından Git **karşıdan**.</span><span class="sxs-lookup"><span data-stu-id="a8e1c-151">Go to the location of the flow log, select it, and then select **Download**.</span></span>

![Akış günlükleri ayarlarını][6]

<span data-ttu-id="a8e1c-153">Günlük yapısı hakkında daha fazla bilgi için [ağ güvenlik grubu akışı günlüğü genel bakış](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a8e1c-153">For information about the structure of the log, visit [Network security group flow log overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8e1c-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a8e1c-154">Next steps</span></span>

<span data-ttu-id="a8e1c-155">Bilgi edinmek için nasıl [NSG akış günlüklerinizi Powerbı ile görselleştirme](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="a8e1c-155">Learn how to [visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
