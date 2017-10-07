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
# <a name="modify-local-network-gateway-settings-using-powershell"></a>PowerShell kullanarak yerel ağ geçidi ayarlarını değiştirme

Bazen yerel ağ geçidinizin AddressPrefix veya Gatewayıpaddress hello ayarlarını değiştirin. Bu makale size nasıl gösterir toomodify yerel ağ geçidi ayarlarınızı. Liste aşağıdaki hello farklı bir seçeneği seçerek farklı bir yöntem kullanarak bu ayarları değiştirebilirsiniz:

> [!div class="op_single_selector"]
> * [Azure portal](vpn-gateway-modify-local-network-gateway-portal.md)
> * [PowerShell](vpn-gateway-modify-local-network-gateway.md)
> * [Azure CLI](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <a name="before"></a>Başlamadan önce

Merhaba hello Azure Resource Manager PowerShell cmdlet'lerinin en son sürümünü yükleyin. Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azureps-cmdlets-docs) hello PowerShell cmdlet'lerini yükleme hakkında daha fazla bilgi.

## <a name="ipaddprefix"></a>IP adres öneklerini değiştirme

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <a name="gwip"></a>Merhaba ağ geçidi IP adresini değiştirme

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a>Sonraki adımlar

Ağ geçidi bağlantınızı doğrulayabilirsiniz. Bkz: [bir ağ geçidi bağlantısını doğrulama](vpn-gateway-verify-connection-resource-manager.md).