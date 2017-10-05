---
title: "Azure Ağ İzleyicisi - Azure portal ile bağlantısını kontrol edin. | Microsoft Docs"
description: "Bu sayfayı Ağ İzleyicisi Azure portalını kullanarak bağlantı denetimi kullanımı açıklanmaktadır"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: gwallace
ms.openlocfilehash: 84774d0f40e06a819ca6de6cf0be68e17ba474e4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-the-azure-portal"></a><span data-ttu-id="fad97-103">Azure portalını kullanarak Azure Ağ İzleyicisi ile bağlantısını denetleyin</span><span class="sxs-lookup"><span data-stu-id="fad97-103">Check connectivity with Azure Network Watcher using the Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="fad97-104">Portal</span><span class="sxs-lookup"><span data-stu-id="fad97-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="fad97-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fad97-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="fad97-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="fad97-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="fad97-107">Azure REST API'si</span><span class="sxs-lookup"><span data-stu-id="fad97-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="fad97-108">Bir doğrudan belirli bir uç noktası TCP bağlantısı bir sanal makineden oluşturulan olmadığını doğrulamak için bağlantı kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="fad97-108">Learn how to use connectivity to verify if a direct TCP connection from a virtual machine to a given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fad97-109">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="fad97-109">Before you begin</span></span>

<span data-ttu-id="fad97-110">Bu makalede, aşağıdaki kaynaklara sahip olduğunuz varsayılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="fad97-110">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="fad97-111">Ağ İzleyicisi bağlantı denetlemek istediğiniz bölgede bir örneği.</span><span class="sxs-lookup"><span data-stu-id="fad97-111">An instance of Network Watcher in the region you want to check connectivity.</span></span>

* <span data-ttu-id="fad97-112">Sanal makineler ile bağlantılarını denetlemek için.</span><span class="sxs-lookup"><span data-stu-id="fad97-112">Virtual machines to check connectivity with.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fad97-113">Bağlantı onay gerektiren bir sanal makine uzantısı `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="fad97-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="fad97-114">Bir Windows VM uzantısı yüklemek için ziyaret [Windows için Azure Ağ İzleyicisi Aracısı sanal makine uzantısı](../virtual-machines/windows/extensions-nwa.md) ve Linux VM ziyaret edin: [Linux için Azure Ağ İzleyicisi Aracısı sanal makine uzantısı](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="fad97-114">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="check-connectivity-to-a-virtual-machine"></a><span data-ttu-id="fad97-115">Bir sanal makineye bağlantısını kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="fad97-115">Check connectivity to a virtual machine</span></span>

<span data-ttu-id="fad97-116">Bu örnekte, bağlantı noktası 80 üzerinden bir hedef sanal makine bağlantısı denetler.</span><span class="sxs-lookup"><span data-stu-id="fad97-116">This example checks connectivity to a destination virtual machine over port 80.</span></span>

<span data-ttu-id="fad97-117">Ağ İzleyicisi gidin ve tıklayın **bağlantı denetimi (Önizleme)**.</span><span class="sxs-lookup"><span data-stu-id="fad97-117">Navigate to your Network Watcher and click **Connectivity check (Preview)**.</span></span> <span data-ttu-id="fad97-118">Bağlantısını denetlemek için sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="fad97-118">Select the virtual machine to check connectivity from.</span></span> <span data-ttu-id="fad97-119">İçinde **hedef** bölümü seçin **bir sanal makine seçin** ve doğru sanal makine ve test etmek için bağlantı noktası seçin.</span><span class="sxs-lookup"><span data-stu-id="fad97-119">In the **Destination** section choose **Select a virtual machine** and choose the correct virtual machine and port to test.</span></span>

<span data-ttu-id="fad97-120">Tıkladığınızda **denetleyin**, belirtilen bağlantı noktası sanal makineleri arasındaki bağlantıyı denetlenir.</span><span class="sxs-lookup"><span data-stu-id="fad97-120">Once you click **Check**, the connectivity between the virtual machines on the port specified are checked.</span></span> <span data-ttu-id="fad97-121">Örnekte, hedef VM erişilemiyor, atlama listesi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="fad97-121">In the example, the destination VM is unreachable, a listing of hops are shown.</span></span>

![Bir sanal makine için denetim bağlantı sonuçları][1]

## <a name="check-remote-endpoint-connectivity"></a><span data-ttu-id="fad97-123">Uzak uç noktada bağlantısını kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="fad97-123">Check remote endpoint connectivity</span></span>

<span data-ttu-id="fad97-124">Bağlantısını ve uzak uç nokta için gecikme süresini denetlemek için seçin **el ile belirt** radyo düğmesini **hedef** bölümünde, url ve bağlantı noktasını girin ve tıklatın **denetleyin**.</span><span class="sxs-lookup"><span data-stu-id="fad97-124">To check the connectivity and latency to a remote endpoint, choose the **Specify manually** radio button in the **Destination** section, input the url and the port and click **Check**.</span></span>  <span data-ttu-id="fad97-125">Bu, Web siteleri ve depolama uç noktaları gibi uzak uç noktalar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fad97-125">This is used for remote endpoints like websites and storage endpoints.</span></span>

![Bir web sitesi için bağlantı sonuçları denetleyin][2]

## <a name="next-steps"></a><span data-ttu-id="fad97-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fad97-127">Next steps</span></span>

<span data-ttu-id="fad97-128">Sanal makine uyarılarla paket yakalamaları görüntüleyerek otomatikleştirmeyi öğrenin [bir uyarı tetiklenen paket yakalama oluşturma](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="fad97-128">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="fad97-129">Belirli trafik içinde veya dışında VM ziyaret ederek izin verilip verilmediğini Bul [denetleyin IP akış doğrulayın](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="fad97-129">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png
