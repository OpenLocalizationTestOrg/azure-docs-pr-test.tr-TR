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
# <a name="modify-local-network-gateway-settings-using-hello-azure-cli"></a>Hello Azure CLI kullanarak yerel ağ geçidi ayarlarını değiştirme

Bazen yerel ağ geçidi adres ön eki veya ağ geçidi IP adresi hello ayarlarını değiştirin. Bu makale size nasıl gösterir toomodify yerel ağ geçidi ayarlarınızı. Liste aşağıdaki hello farklı bir seçeneği seçerek farklı bir yöntem kullanarak bu ayarları değiştirebilirsiniz:

> [!div class="op_single_selector"]
> * [Azure portal](vpn-gateway-modify-local-network-gateway-portal.md)
> * [PowerShell](vpn-gateway-modify-local-network-gateway.md)
> * [Azure CLI](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <a name="before"></a>Başlamadan önce

Merhaba hello CLI komutları (2.0 veya üstü) en son sürümünü yükleyin. Merhaba CLI komutları yükleme hakkında daha fazla bilgi için bkz: [Azure CLI 2.0 yükleme](https://docs.microsoft.com/cli/azure/install-azure-cli).

[!INCLUDE [CLI-login](../../includes/vpn-gateway-cli-login-include.md)]

## <a name="ipaddprefix"></a>IP adres öneklerini değiştirme

[!INCLUDE [modify-prefix](../../includes/vpn-gateway-modify-ip-prefix-cli-include.md)]

## <a name="gwip"></a>Merhaba ağ geçidi IP adresini değiştirme

[!INCLUDE [modify-gateway-IP](../../includes/vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

## <a name="next-steps"></a>Sonraki adımlar

Ağ geçidi bağlantınızı doğrulayabilirsiniz. Bkz: [bir ağ geçidi bağlantısını doğrulama](vpn-gateway-verify-connection-resource-manager.md).

