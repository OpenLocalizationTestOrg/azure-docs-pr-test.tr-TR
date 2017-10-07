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
# <a name="modify-local-network-gateway-settings-using-hello-azure-portal"></a>Hello Azure portal kullanarak yerel ağ geçidi ayarlarını değiştirme

Bazen yerel ağ geçidinizin AddressPrefix veya Gatewayıpaddress hello ayarlarını değiştirin. Bu makale size nasıl gösterir toomodify yerel ağ geçidi ayarlarınızı. Liste aşağıdaki hello farklı bir seçeneği seçerek farklı bir yöntem kullanarak bu ayarları değiştirebilirsiniz:

> [!div class="op_single_selector"]
> * [Azure portal](vpn-gateway-modify-local-network-gateway-portal.md)
> * [PowerShell](vpn-gateway-modify-local-network-gateway.md)
> * [Azure CLI](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <a name="ipaddprefix"></a>IP adres öneklerini değiştirme

IP adresi öneklerini değiştirirken, yerel ağ geçidinizin bir bağlantı olup hello adımları takip ettiğiniz bağlıdır.

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <a name="gwip"></a>Merhaba ağ geçidi IP adresini değiştirme

Tooconnect toohas istediğiniz hello VPN cihazının genel IP adresini değiştirdiyseniz, değişiklik toomodify hello yerel ağ geçidi tooreflect gerekir. Merhaba ortak IP adresini değiştirirseniz, yerel ağ geçidinizin bir bağlantı olup hello adımları takip ettiğiniz bağlıdır.

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a>Sonraki adımlar

Ağ geçidi bağlantınızı doğrulayabilirsiniz. Bkz: [bir ağ geçidi bağlantısını doğrulama](vpn-gateway-verify-connection-resource-manager.md).