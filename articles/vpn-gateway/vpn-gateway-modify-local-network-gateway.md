---
title: "Merhaba VPN ağ geçidi IP adresi ve Hello yerel ağ geçidi IP adresi öneklerini değiştirme | Azure | PowerShell | Microsoft Docs"
description: "Bu makalede, PowerShell kullanarak yerel ağ geçidinizin IP adresi ön eklerini değiştirme aracılığıyla açıklanmaktadır."
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
ms.openlocfilehash: 1353598b39a97fae9bdb424505a5ae2560482654
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-powershell"></a><span data-ttu-id="e3ea6-103">PowerShell kullanarak yerel ağ geçidi ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="e3ea6-103">Modify local network gateway settings using PowerShell</span></span>

<span data-ttu-id="e3ea6-104">Bazen yerel ağ geçidinizin AddressPrefix veya Gatewayıpaddress hello ayarlarını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e3ea6-104">Sometimes hello settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="e3ea6-105">Bu makale size nasıl gösterir toomodify yerel ağ geçidi ayarlarınızı.</span><span class="sxs-lookup"><span data-stu-id="e3ea6-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="e3ea6-106">Liste aşağıdaki hello farklı bir seçeneği seçerek farklı bir yöntem kullanarak bu ayarları değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e3ea6-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e3ea6-107">Azure portal</span><span class="sxs-lookup"><span data-stu-id="e3ea6-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="e3ea6-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3ea6-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="e3ea6-109">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e3ea6-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="e3ea6-110"><a name="before"></a>Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="e3ea6-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="e3ea6-111">Merhaba hello Azure Resource Manager PowerShell cmdlet'lerinin en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e3ea6-111">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="e3ea6-112">Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azureps-cmdlets-docs) hello PowerShell cmdlet'lerini yükleme hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="e3ea6-112">See [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing hello PowerShell cmdlets.</span></span>

## <span data-ttu-id="e3ea6-113"><a name="ipaddprefix"></a>IP adres öneklerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="e3ea6-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="e3ea6-114"><a name="gwip"></a>Merhaba ağ geçidi IP adresini değiştirme</span><span class="sxs-lookup"><span data-stu-id="e3ea6-114"><a name="gwip"></a>Modify hello gateway IP address</span></span>

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="e3ea6-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e3ea6-115">Next steps</span></span>

<span data-ttu-id="e3ea6-116">Ağ geçidi bağlantınızı doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e3ea6-116">You can verify your gateway connection.</span></span> <span data-ttu-id="e3ea6-117">Bkz: [bir ağ geçidi bağlantısını doğrulama](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e3ea6-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>