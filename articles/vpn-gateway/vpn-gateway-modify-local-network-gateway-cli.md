---
title: "Merhaba VPN ağ geçidi IP adresi ve Hello yerel ağ geçidi IP adresi öneklerini değiştirme | Azure | CLI | Microsoft Docs"
description: "Bu makalede hello Azure CLI kullanarak yerel ağ geçidinizin IP adresi ön eklerini değiştirme aracılığıyla anlatılmaktadır."
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
ms.openlocfilehash: 4b8bbf3e9d3d42ac2d12f87360fa0a4134c57a21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-hello-azure-cli"></a><span data-ttu-id="23f01-103">Hello Azure CLI kullanarak yerel ağ geçidi ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="23f01-103">Modify local network gateway settings using hello Azure CLI</span></span>

<span data-ttu-id="23f01-104">Bazen yerel ağ geçidi adres ön eki veya ağ geçidi IP adresi hello ayarlarını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="23f01-104">Sometimes hello settings for your local network gateway Address Prefix or Gateway IP Address change.</span></span> <span data-ttu-id="23f01-105">Bu makale size nasıl gösterir toomodify yerel ağ geçidi ayarlarınızı.</span><span class="sxs-lookup"><span data-stu-id="23f01-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="23f01-106">Liste aşağıdaki hello farklı bir seçeneği seçerek farklı bir yöntem kullanarak bu ayarları değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="23f01-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="23f01-107">Azure portal</span><span class="sxs-lookup"><span data-stu-id="23f01-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="23f01-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="23f01-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="23f01-109">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="23f01-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="23f01-110"><a name="before"></a>Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="23f01-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="23f01-111">Merhaba hello CLI komutları (2.0 veya üstü) en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="23f01-111">Install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="23f01-112">Merhaba CLI komutları yükleme hakkında daha fazla bilgi için bkz: [Azure CLI 2.0 yükleme](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="23f01-112">For information about installing hello CLI commands, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

[!INCLUDE [CLI-login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="23f01-113"><a name="ipaddprefix"></a>IP adres öneklerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="23f01-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [modify-prefix](../../includes/vpn-gateway-modify-ip-prefix-cli-include.md)]

## <span data-ttu-id="23f01-114"><a name="gwip"></a>Merhaba ağ geçidi IP adresini değiştirme</span><span class="sxs-lookup"><span data-stu-id="23f01-114"><a name="gwip"></a>Modify hello gateway IP address</span></span>

[!INCLUDE [modify-gateway-IP](../../includes/vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="23f01-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="23f01-115">Next steps</span></span>

<span data-ttu-id="23f01-116">Ağ geçidi bağlantınızı doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23f01-116">You can verify your gateway connection.</span></span> <span data-ttu-id="23f01-117">Bkz: [bir ağ geçidi bağlantısını doğrulama](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="23f01-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

