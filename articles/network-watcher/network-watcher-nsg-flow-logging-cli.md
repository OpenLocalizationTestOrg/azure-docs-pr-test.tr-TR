---
title: "Ağ güvenlik grubu akış günlükleri Azure Ağ İzleyicisi - Azure CLI ile yönetme | Microsoft Docs"
description: "Bu sayfa, Azure CLI ile Azure Ağ İzleyicisi ağ güvenlik grubu akış günlüklerine yönetmek açıklanmaktadır"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2dfc3112-8294-4357-b2f8-f81840da67d3
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d5a8aa0cd274132798a0d8484a950926761dae7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli"></a><span data-ttu-id="ab93b-103">Azure CLI ile ağ güvenlik grubu akış günlüklerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ab93b-103">Configuring Network Security Group Flow logs with Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="ab93b-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="ab93b-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="ab93b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab93b-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="ab93b-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="ab93b-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="ab93b-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ab93b-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="ab93b-108">REST API</span><span class="sxs-lookup"><span data-stu-id="ab93b-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="ab93b-109">Ağ güvenlik grubu akış günlükleri, giriş ve çıkış IP trafiği bir ağ güvenlik grubu ile ilgili bilgileri görüntülemek izin veren bir Ağ İzleyicisi özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="ab93b-109">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="ab93b-110">Bu akış günlükleri json biçiminde yazılır ve Kural başına temelinde, akış uygulanır, akış (kaynak/hedef IP, kaynak/hedef bağlantı noktası, Protokolü), 5-tanımlama grubu bilgilerini NIC giden ve gelen akışları gösterir ve trafiğe izin verilen veya reddedilen.</span><span class="sxs-lookup"><span data-stu-id="ab93b-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

<span data-ttu-id="ab93b-111">Bu makalede, Windows, Mac ve Linux için kullanılabilir olduğu, kaynak yönetimi için dağıtım modelini, Azure CLI 2.0 bizim nesil CLI kullanılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ab93b-111">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="ab93b-112">Bu makaledeki adımları gerçekleştirmek için gerek [Mac, Linux ve Windows (Azure CLI) için Azure komut satırı arabirimini yükleyin](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="ab93b-112">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="ab93b-113">Öngörüler sağlayıcısını Kaydet</span><span class="sxs-lookup"><span data-stu-id="ab93b-113">Register Insights provider</span></span>

<span data-ttu-id="ab93b-114">Başarılı bir şekilde çalışması için günlük akışı sırayla **Microsoft.ınsights** sağlayıcı kaydedilmelidir.</span><span class="sxs-lookup"><span data-stu-id="ab93b-114">In order for flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="ab93b-115">Emin değilseniz, **Microsoft.ınsights** sağlayıcısı kayıtlı, aşağıdaki komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ab93b-115">If you are not sure if the **Microsoft.Insights** provider is registered, run the following script.</span></span>

```azurecli
az provider register --namespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="ab93b-116">Ağ güvenlik grubu etkinleştirmek akış günlükleri</span><span class="sxs-lookup"><span data-stu-id="ab93b-116">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="ab93b-117">Akış günlükleri etkinleştirmek için komutu aşağıdaki örnekte gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ab93b-117">The command to enable flow logs is shown in the following example:</span></span>

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled true --nsg nsgName --storage-account storageAccountName
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="ab93b-118">Ağ güvenlik grubu devre dışı akış günlükleri</span><span class="sxs-lookup"><span data-stu-id="ab93b-118">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="ab93b-119">Akış günlükleri devre dışı bırakmak için aşağıdaki örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="ab93b-119">Use the following example to disable flow logs:</span></span>

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled false --nsg nsgName
```

## <a name="download-a-flow-log"></a><span data-ttu-id="ab93b-120">Akış günlüğü indirin</span><span class="sxs-lookup"><span data-stu-id="ab93b-120">Download a Flow log</span></span>

<span data-ttu-id="ab93b-121">Akış günlüğü depolama konumunu, oluşturma sırasında tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="ab93b-121">The storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="ab93b-122">Bir depolama hesabına kaydedilen bu akış günlüklerine erişmek için kullanışlı bir burada indirilebilir Microsoft Azure Storage Gezgini araçtır: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="ab93b-122">A convenient tool to access these flow logs saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="ab93b-123">Bir depolama hesabı belirtilirse, paket yakalama dosyaları şu konumda bir depolama hesabına kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="ab93b-123">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="ab93b-124">Günlük yapısı hakkında bilgi için ziyaret [ağ güvenlik grubu akış günlüğüne genel bakış](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="ab93b-124">For information about the structure of the log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab93b-125">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="ab93b-125">Next Steps</span></span>

<span data-ttu-id="ab93b-126">Bilgi edinmek için nasıl [NSG akış günlüklerinizi Powerbı ile Görselleştirme](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="ab93b-126">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="ab93b-127">Bilgi edinmek için nasıl [NSG akış günlüklerinizi açık kaynaklı araçları ile Görselleştirme](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="ab93b-127">Learn how to [Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
