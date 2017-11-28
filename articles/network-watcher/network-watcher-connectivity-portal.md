---
title: "Azure Ağ İzleyicisi - Azure portal ile aaaCheck bağlantısı | Microsoft Docs"
description: "Bu sayfayı nasıl toouse bağlantısını denetleyin Ağ İzleyicisi Merhaba Azure portal kullanarak açıklar"
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
ms.openlocfilehash: ef6ecccd688f06f70003a5b59771c15bcbe8f3e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a><span data-ttu-id="34e98-103">Hello Azure portal kullanarak Azure Ağ İzleyicisi ile bağlantısını denetleyin</span><span class="sxs-lookup"><span data-stu-id="34e98-103">Check connectivity with Azure Network Watcher using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="34e98-104">Portal</span><span class="sxs-lookup"><span data-stu-id="34e98-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="34e98-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="34e98-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="34e98-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="34e98-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="34e98-107">Azure REST API'si</span><span class="sxs-lookup"><span data-stu-id="34e98-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="34e98-108">Toouse bağlantı tooverify doğrudan TCP bağlantısı, uç nokta verilen bir sanal makine tooa nasıl kurulabilir öğrenin.</span><span class="sxs-lookup"><span data-stu-id="34e98-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="34e98-109">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="34e98-109">Before you begin</span></span>

<span data-ttu-id="34e98-110">Bu makalede, kaynakları aşağıdaki hello olduğu varsayılır:</span><span class="sxs-lookup"><span data-stu-id="34e98-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="34e98-111">Bir örneği toocheck bağlantı istediğiniz Ağ İzleyicisinin hello bölgede.</span><span class="sxs-lookup"><span data-stu-id="34e98-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="34e98-112">Sanal makineler toocheck bağlantısına sahip.</span><span class="sxs-lookup"><span data-stu-id="34e98-112">Virtual machines toocheck connectivity with.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34e98-113">Bağlantı onay gerektiren bir sanal makine uzantısı `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="34e98-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="34e98-114">Bir Windows VM Hello uzantısı yüklemek için ziyaret [Windows için Azure Ağ İzleyicisi Aracısı sanal makine uzantısı](../virtual-machines/windows/extensions-nwa.md) ve Linux VM ziyaret edin: [Azure Ağ İzleyicisi Aracısı sanal makine uzantısı Linuxiçin](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="34e98-114">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="34e98-115">Bağlantı tooa sanal makine kontrol edin</span><span class="sxs-lookup"><span data-stu-id="34e98-115">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="34e98-116">Bu örnekte, bağlantı noktası 80 üzerinden bağlantı tooa hedef sanal makine denetler.</span><span class="sxs-lookup"><span data-stu-id="34e98-116">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

<span data-ttu-id="34e98-117">Ağ İzleyicisi tooyour gidin ve tıklayın **bağlantı denetimi (Önizleme)**.</span><span class="sxs-lookup"><span data-stu-id="34e98-117">Navigate tooyour Network Watcher and click **Connectivity check (Preview)**.</span></span> <span data-ttu-id="34e98-118">Merhaba sanal makine toocheck bağlantısını seçin.</span><span class="sxs-lookup"><span data-stu-id="34e98-118">Select hello virtual machine toocheck connectivity from.</span></span> <span data-ttu-id="34e98-119">Merhaba, **hedef** bölümü seçin **bir sanal makine seçin** hello doğru sanal makine ve bağlantı noktası tootest seçin.</span><span class="sxs-lookup"><span data-stu-id="34e98-119">In hello **Destination** section choose **Select a virtual machine** and choose hello correct virtual machine and port tootest.</span></span>

<span data-ttu-id="34e98-120">Tıkladığınızda **denetleyin**, belirtilen başlangıç bağlantı noktası hello sanal makineler arasında hello bağlantı denetlenir.</span><span class="sxs-lookup"><span data-stu-id="34e98-120">Once you click **Check**, hello connectivity between hello virtual machines on hello port specified are checked.</span></span> <span data-ttu-id="34e98-121">Merhaba örnekte hello hedef VM erişilemiyor, atlama listesi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="34e98-121">In hello example, hello destination VM is unreachable, a listing of hops are shown.</span></span>

![Bir sanal makine için denetim bağlantı sonuçları][1]

## <a name="check-remote-endpoint-connectivity"></a><span data-ttu-id="34e98-123">Uzak uç noktada bağlantısını kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="34e98-123">Check remote endpoint connectivity</span></span>

<span data-ttu-id="34e98-124">toocheck hello bağlantısı ve gecikme tooa uzak uç nokta, seçim hello **el ile belirtin** hello radyo düğmesini **hedef** bölümünde, giriş hello url ve başlangıç bağlantı noktası ve tıklatın **denetleyin** .</span><span class="sxs-lookup"><span data-stu-id="34e98-124">toocheck hello connectivity and latency tooa remote endpoint, choose hello **Specify manually** radio button in hello **Destination** section, input hello url and hello port and click **Check**.</span></span>  <span data-ttu-id="34e98-125">Bu, Web siteleri ve depolama uç noktaları gibi uzak uç noktalar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="34e98-125">This is used for remote endpoints like websites and storage endpoints.</span></span>

![Bir web sitesi için bağlantı sonuçları denetleyin][2]

## <a name="next-steps"></a><span data-ttu-id="34e98-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="34e98-127">Next steps</span></span>

<span data-ttu-id="34e98-128">Nasıl sanal makine uyarılarla tooautomate paket görüntüleyerek yakalar öğrenin [bir uyarı tetiklenen paket yakalama oluşturma](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="34e98-128">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="34e98-129">Belirli trafik içinde veya dışında VM ziyaret ederek izin verilip verilmediğini Bul [denetleyin IP akış doğrulayın](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="34e98-129">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png
