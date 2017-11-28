---
title: "Ağ güvenlik grubu akış günlükleri Azure Ağ İzleyicisi - Azure CLI aaaManage | Microsoft Docs"
description: "Bu sayfayı nasıl toomanage ağ güvenlik grubu akış Azure CLI ile Azure Ağ İzleyicisi kaydeder açıklar"
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
ms.openlocfilehash: 2d0b02e7d0a5a9ab20beb491d49a5747f976a079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli"></a><span data-ttu-id="0c6ab-103">Azure CLI ile ağ güvenlik grubu akış günlüklerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0c6ab-103">Configuring Network Security Group Flow logs with Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="0c6ab-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="0c6ab-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="0c6ab-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0c6ab-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="0c6ab-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0c6ab-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="0c6ab-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0c6ab-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="0c6ab-108">REST API</span><span class="sxs-lookup"><span data-stu-id="0c6ab-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="0c6ab-109">Ağ güvenlik grubu akış günlükleri, giriş ve çıkış IP trafiği bir ağ güvenlik grubu aracılığıyla tooview bilgilerini sağlayan Ağ İzleyicisi özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="0c6ab-109">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="0c6ab-110">Bu akış günlükleri json biçiminde yazılmıştır ve giden Göster gelen akış kuralı başına temelinde hello NIC hello akış uygular, 5-tanımlama grubu ilgili bilgilere hello akış (kaynak/hedef IP, kaynak/hedef bağlantı noktası, Protokolü) ve hello varsa trafiğine izin veya engellendi.</span><span class="sxs-lookup"><span data-stu-id="0c6ab-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="0c6ab-111">Bu makalede bizim nesil CLI hello kaynak yönetimi dağıtım modeli için Azure CLI 2.0, Windows, Mac ve Linux için kullanılabilir olduğu kullanır.</span><span class="sxs-lookup"><span data-stu-id="0c6ab-111">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="0c6ab-112">Bu makaledeki adımları tooperform Merhaba, çok ihtiyacınız[hello Azure komut satırı arabirimi Mac, Linux ve Windows (Azure CLI) için yükleme](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="0c6ab-112">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="0c6ab-113">Öngörüler sağlayıcısını Kaydet</span><span class="sxs-lookup"><span data-stu-id="0c6ab-113">Register Insights provider</span></span>

<span data-ttu-id="0c6ab-114">Merhaba başarıyla günlük toowork akış için sırayla **Microsoft.ınsights** sağlayıcı kaydedilmelidir.</span><span class="sxs-lookup"><span data-stu-id="0c6ab-114">In order for flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="0c6ab-115">Merhaba, emin değilseniz **Microsoft.ınsights** sağlayıcısıdır kayıtlı, çalışma hello aşağıdaki komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="0c6ab-115">If you are not sure if hello **Microsoft.Insights** provider is registered, run hello following script.</span></span>

```azurecli
az provider register --namespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="0c6ab-116">Ağ güvenlik grubu etkinleştirmek akış günlükleri</span><span class="sxs-lookup"><span data-stu-id="0c6ab-116">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="0c6ab-117">Merhaba komut tooenable akış günlükleri aşağıdaki örneğine hello gösterilir:</span><span class="sxs-lookup"><span data-stu-id="0c6ab-117">hello command tooenable flow logs is shown in hello following example:</span></span>

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled true --nsg nsgName --storage-account storageAccountName
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="0c6ab-118">Ağ güvenlik grubu devre dışı akış günlükleri</span><span class="sxs-lookup"><span data-stu-id="0c6ab-118">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="0c6ab-119">Örnek toodisable akış günlükleri aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="0c6ab-119">Use hello following example toodisable flow logs:</span></span>

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled false --nsg nsgName
```

## <a name="download-a-flow-log"></a><span data-ttu-id="0c6ab-120">Akış günlüğü indirin</span><span class="sxs-lookup"><span data-stu-id="0c6ab-120">Download a Flow log</span></span>

<span data-ttu-id="0c6ab-121">Akış günlüğü Hello depolama konumuna oluşturma sırasında tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="0c6ab-121">hello storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="0c6ab-122">Bu akış kaydedilen günlükler tooa depolama hesabıdır burada indirilebilir Microsoft Azure Storage Gezgini uygun aracı tooaccess: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="0c6ab-122">A convenient tool tooaccess these flow logs saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="0c6ab-123">Bir depolama hesabı belirtilirse, paket yakalama dosyalarını tooa depolama hesabı konumu aşağıdaki hello kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="0c6ab-123">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="0c6ab-124">Merhaba günlük hello yapısı hakkında bilgi için ziyaret [ağ güvenlik grubu akış günlüğüne genel bakış](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="0c6ab-124">For information about hello structure of hello log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c6ab-125">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="0c6ab-125">Next Steps</span></span>

<span data-ttu-id="0c6ab-126">Nasıl çok öğrenin[NSG akış günlüklerinizi Powerbı ile Görselleştirme](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="0c6ab-126">Learn how too[Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="0c6ab-127">Nasıl çok öğrenin[NSG akış günlüklerinizi açık kaynaklı araçları ile Görselleştirme](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="0c6ab-127">Learn how too[Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
