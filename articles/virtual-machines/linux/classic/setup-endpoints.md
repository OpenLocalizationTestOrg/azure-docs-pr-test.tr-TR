---
title: "uç noktaları klasik bir Linux VM üzerinde yukarı aaaSet | Microsoft Docs"
description: "Hello Azure Klasik portalı tooallow iletişimi azure'da bir Linux sanal makine ile bir Linux VM için uç noktalar yukarı tooset öğrenin"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f3749738-1109-4a1d-8635-40e4bd220e91
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: 1c959d10dd1e20228fa4a20e1cc0205c1d12f185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a>Nasıl tooset bir Linux Klasik sanal makinede Azure uç noktaları ayarlama
Azure'da hello Klasik dağıtım modeli kullanarak oluşturduğunuz tüm Linux sanal makineleri otomatik olarak hello içindeki diğer sanal makinelerle özel ağ kanalı üzerinden aynı hizmet veya sanal ağ bulut iletişim kurabilir. Ancak, hello Internet veya diğer sanal ağlardaki bilgisayarlar uç noktaları toodirect hello gelen ağ trafiğini tooa sanal makine gerektirir. Bu makalede ayrıca kullanılabilir [Windows sanal makineleri](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

> [!IMPORTANT]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.

Merhaba, **Resource Manager** dağıtım modeli, uç noktalar kullanılarak yapılandırılmış olan **ağ güvenlik grupları (Nsg'ler)**. Daha fazla bilgi için bkz: [bağlantı noktalarını ve uç noktaları açmadan](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Hello Azure portal Linux sanal makine oluşturduğunuzda, bir uç nokta için güvenli Kabuk (SSH) genellikle sizin için otomatik olarak oluşturulur. Merhaba sanal makine oluşturulurken veya daha sonra gerektikçe ek uç noktaları yapılandırabilirsiniz.

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a>Sonraki adımlar
* Hello kullanarak bir VM uç noktası oluşturabilirsiniz [Azure komut satırı arabirimi](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2). Merhaba çalıştırmak **azure vm uç noktası oluşturma** komutu.
* Merhaba Resource Manager dağıtım modelinde bir sanal makine oluşturduysanız, Resource Manager moduna hello Azure CLI kullanabileceğine[ağ güvenlik grupları oluşturma](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol trafiği toohello VM.
