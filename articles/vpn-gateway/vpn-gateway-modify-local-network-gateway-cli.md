---
title: "Yerel ağ geçidi IP adresi öneklerini ve VPN ağ geçidi IP adresini değiştirme | Azure | CLI | Microsoft Docs"
description: "Bu makalede Azure CLI kullanarak yerel ağ geçidinizin IP adresi ön eklerini değiştirme aracılığıyla anlatılmaktadır."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c7db48f-d09a-44e7-836f-1fb6930389df
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: cherylmc
ms.openlocfilehash: 7db1ad970ebb93d46d5a861f9a9b27bf121531a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="modify-local-network-gateway-settings-using-the-azure-cli"></a><span data-ttu-id="41536-103">Azure CLI kullanarak yerel ağ geçidi ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="41536-103">Modify local network gateway settings using the Azure CLI</span></span>

<span data-ttu-id="41536-104">Bazen yerel ağ geçidi adres ön eki veya ağ geçidi IP adresi ayarlarını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="41536-104">Sometimes the settings for your local network gateway Address Prefix or Gateway IP Address change.</span></span> <span data-ttu-id="41536-105">Bu makalede, yerel ağ geçidi ayarlarınızı değiştirmek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="41536-105">This article shows you how to modify your local network gateway settings.</span></span> <span data-ttu-id="41536-106">Aşağıdaki listeden farklı bir seçeneği seçerek farklı bir yöntem kullanarak bu ayarları değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="41536-106">You can also modify these settings using a different method by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="41536-107">Azure portal</span><span class="sxs-lookup"><span data-stu-id="41536-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="41536-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="41536-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="41536-109">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="41536-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="41536-110"><a name="before"></a>Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="41536-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="41536-111">CLI komutları (2.0 veya üstü) en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="41536-111">Install the latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="41536-112">CLI komutlarını yükleme hakkında bilgi için bkz. [Azure CLI 2.0’ı yükleme](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="41536-112">For information about installing the CLI commands, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

[!INCLUDE [CLI-login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="41536-113"><a name="ipaddprefix"></a>IP adres öneklerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="41536-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [modify-prefix](../../includes/vpn-gateway-modify-ip-prefix-cli-include.md)]

## <span data-ttu-id="41536-114"><a name="gwip"></a>Ağ geçidi IP adresini değiştirme</span><span class="sxs-lookup"><span data-stu-id="41536-114"><a name="gwip"></a>Modify the gateway IP address</span></span>

[!INCLUDE [modify-gateway-IP](../../includes/vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="41536-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="41536-115">Next steps</span></span>

<span data-ttu-id="41536-116">Ağ geçidi bağlantınızı doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41536-116">You can verify your gateway connection.</span></span> <span data-ttu-id="41536-117">Bkz: [bir ağ geçidi bağlantısını doğrulama](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="41536-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

