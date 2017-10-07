---
title: "Merhaba VPN ağ geçidi IP adresi ve Hello yerel ağ geçidi IP adresi öneklerini değiştirme | Azure | Portal | Microsoft Docs"
description: "Bu makalede hello Azure portal kullanarak yerel ağ geçidinizin IP adresi ön eklerini değiştirme aracılığıyla anlatılmaktadır."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: cherylmc
ms.openlocfilehash: 001df7b748ccc234d87aab3501a4f0e4ddfe60f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-hello-azure-portal"></a><span data-ttu-id="d9b50-103">Hello Azure portal kullanarak yerel ağ geçidi ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="d9b50-103">Modify local network gateway settings using hello Azure portal</span></span>

<span data-ttu-id="d9b50-104">Bazen yerel ağ geçidinizin AddressPrefix veya Gatewayıpaddress hello ayarlarını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d9b50-104">Sometimes hello settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="d9b50-105">Bu makale size nasıl gösterir toomodify yerel ağ geçidi ayarlarınızı.</span><span class="sxs-lookup"><span data-stu-id="d9b50-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="d9b50-106">Liste aşağıdaki hello farklı bir seçeneği seçerek farklı bir yöntem kullanarak bu ayarları değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d9b50-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d9b50-107">Azure portal</span><span class="sxs-lookup"><span data-stu-id="d9b50-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="d9b50-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9b50-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="d9b50-109">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d9b50-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <span data-ttu-id="d9b50-110"><a name="ipaddprefix"></a>IP adres öneklerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="d9b50-110"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

<span data-ttu-id="d9b50-111">IP adresi öneklerini değiştirirken, yerel ağ geçidinizin bir bağlantı olup hello adımları takip ettiğiniz bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="d9b50-111">When you modify IP address prefixes, hello steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <span data-ttu-id="d9b50-112"><a name="gwip"></a>Merhaba ağ geçidi IP adresini değiştirme</span><span class="sxs-lookup"><span data-stu-id="d9b50-112"><a name="gwip"></a>Modify hello gateway IP address</span></span>

<span data-ttu-id="d9b50-113">Tooconnect toohas istediğiniz hello VPN cihazının genel IP adresini değiştirdiyseniz, değişiklik toomodify hello yerel ağ geçidi tooreflect gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9b50-113">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="d9b50-114">Merhaba ortak IP adresini değiştirirseniz, yerel ağ geçidinizin bir bağlantı olup hello adımları takip ettiğiniz bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="d9b50-114">When you change hello public IP address, hello steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a><span data-ttu-id="d9b50-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d9b50-115">Next steps</span></span>

<span data-ttu-id="d9b50-116">Ağ geçidi bağlantınızı doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9b50-116">You can verify your gateway connection.</span></span> <span data-ttu-id="d9b50-117">Bkz: [bir ağ geçidi bağlantısını doğrulama](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="d9b50-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>