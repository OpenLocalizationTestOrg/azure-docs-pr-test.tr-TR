---
title: "Ağ güvenlik grubu akış günlükleri Azure Ağ İzleyicisi - Azure CLI 1.0 aaaManage | Microsoft Docs"
description: "Bu sayfayı toomanage ağ güvenlik grubu akış Azure Ağ İzleyicisi Azure CLI 1.0 ile nasıl kaydeder açıklar"
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
ms.openlocfilehash: 2535eea665a99cffe7569a8d976333435f946a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli-10"></a><span data-ttu-id="19b4f-103">Azure CLI 1.0 ile ağ güvenlik grubu akış günlüklerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="19b4f-103">Configuring Network Security Group Flow logs with Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="19b4f-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="19b4f-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="19b4f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="19b4f-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="19b4f-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="19b4f-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="19b4f-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="19b4f-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="19b4f-108">REST API</span><span class="sxs-lookup"><span data-stu-id="19b4f-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="19b4f-109">Ağ güvenlik grubu akış günlükleri, giriş ve çıkış IP trafiği bir ağ güvenlik grubu aracılığıyla tooview bilgilerini sağlayan Ağ İzleyicisi özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="19b4f-109">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="19b4f-110">Bu akış günlükleri json biçiminde yazılmıştır ve giden Göster gelen akış kuralı başına temelinde hello NIC hello akış uygular, 5-tanımlama grubu ilgili bilgilere hello akış (kaynak/hedef IP, kaynak/hedef bağlantı noktası, Protokolü) ve hello varsa trafiğine izin veya engellendi.</span><span class="sxs-lookup"><span data-stu-id="19b4f-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="19b4f-111">Bu makalede, platformlar arası Azure CLI 1.0, Windows, Mac ve Linux için kullanılabilir olduğu kullanır.</span><span class="sxs-lookup"><span data-stu-id="19b4f-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="19b4f-112">Ağ İzleyicisi, CLI desteği şu anda Azure CLI 1.0 kullanır.</span><span class="sxs-lookup"><span data-stu-id="19b4f-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="19b4f-113">Öngörüler sağlayıcısını Kaydet</span><span class="sxs-lookup"><span data-stu-id="19b4f-113">Register Insights provider</span></span>

<span data-ttu-id="19b4f-114">Merhaba başarıyla günlük toowork akış için sırayla **Microsoft.ınsights** sağlayıcı kaydedilmelidir.</span><span class="sxs-lookup"><span data-stu-id="19b4f-114">In order for flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="19b4f-115">Merhaba, emin değilseniz **Microsoft.ınsights** sağlayıcısıdır kayıtlı, çalışma hello aşağıdaki komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="19b4f-115">If you are not sure if hello **Microsoft.Insights** provider is registered, run hello following script.</span></span>

```azurecli
azure provider register --namespace Microsoft.Insights --subscription <subscriptionid>
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="19b4f-116">Ağ güvenlik grubu etkinleştirmek akış günlükleri</span><span class="sxs-lookup"><span data-stu-id="19b4f-116">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="19b4f-117">Merhaba komut tooenable akış günlükleri aşağıdaki örneğine hello gösterilir:</span><span class="sxs-lookup"><span data-stu-id="19b4f-117">hello command tooenable flow logs is shown in hello following example:</span></span>

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e true
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="19b4f-118">Ağ güvenlik grubu devre dışı akış günlükleri</span><span class="sxs-lookup"><span data-stu-id="19b4f-118">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="19b4f-119">Örnek toodisable akış günlükleri aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="19b4f-119">Use hello following example toodisable flow logs:</span></span>

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e false
```

## <a name="download-a-flow-log"></a><span data-ttu-id="19b4f-120">Akış günlüğü indirin</span><span class="sxs-lookup"><span data-stu-id="19b4f-120">Download a Flow log</span></span>

<span data-ttu-id="19b4f-121">Akış günlüğü Hello depolama konumuna oluşturma sırasında tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="19b4f-121">hello storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="19b4f-122">Bu akış kaydedilen günlükler tooa depolama hesabıdır burada indirilebilir Microsoft Azure Storage Gezgini uygun aracı tooaccess: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="19b4f-122">A convenient tool tooaccess these flow logs saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="19b4f-123">Bir depolama hesabı belirtilirse, paket yakalama dosyalarını tooa depolama hesabı konumu aşağıdaki hello kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="19b4f-123">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="19b4f-124">Merhaba günlük hello yapısı hakkında bilgi için ziyaret [ağ güvenlik grubu akış günlüğüne genel bakış](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="19b4f-124">For information about hello structure of hello log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="19b4f-125">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="19b4f-125">Next Steps</span></span>

<span data-ttu-id="19b4f-126">Nasıl çok öğrenin[NSG akış günlüklerinizi Powerbı ile Görselleştirme](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="19b4f-126">Learn how too[Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="19b4f-127">Nasıl çok öğrenin[NSG akış günlüklerinizi açık kaynaklı araçları ile Görselleştirme](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="19b4f-127">Learn how too[Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
