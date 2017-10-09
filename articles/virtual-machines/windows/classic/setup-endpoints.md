---
title: "Klasik Windows VM üzerindeki uç noktaları yukarı aaaSet | Microsoft Docs"
description: "Hello Azure Klasik portalı tooallow iletişimi azure'da Windows sanal makine ile bir Windows VM için uç noktalar yukarı tooset öğrenin."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 8afc21c2-d3fb-43a3-acce-aa06be448bb6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: e817076f16d3a245a8d19add7b2f2cf5e3baa17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a>Nasıl tooset azure'da klasik bir Windows sanal makine üzerindeki uç noktaları ayarlama
Tüm Windows Azure'da hello Klasik dağıtım modeli kullanarak oluşturduğunuz sanal makine otomatik olarak diğer sanal makineler ile özel ağ kanalı üzerinden iletişim kurabilir aynı bulut hizmeti ya da sanal ağ hello. Ancak, hello Internet veya diğer sanal ağlardaki bilgisayarlar uç noktaları toodirect hello gelen ağ trafiğini tooa sanal makine gerektirir. Bu makalede ayrıca kullanılabilir [Linux sanal makineleri](../../linux/classic/setup-endpoints.md).

> [!IMPORTANT]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.

Merhaba, **Resource Manager** dağıtım modeli, uç noktalar kullanılarak yapılandırılmış olan **ağ güvenlik grupları (Nsg'ler)**. Daha fazla bilgi için bkz: [izin dış erişim tooyour VM kullanarak hello Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Hello Azure portalında Windows sanal makine oluşturduğunuzda, Uzak Masaüstü ve Windows PowerShell uzaktan iletişim için olanlar gibi ortak uç noktaları genellikle sizin için otomatik olarak oluşturulur. Merhaba sanal makine oluşturulurken veya daha sonra gerektikçe ek uç noktaları yapılandırabilirsiniz.

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a>Sonraki adımlar
* toouse bir Azure PowerShell cmdlet tooset bir VM uç noktası yukarı bkz [Ekle AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).
* toouse Azure PowerShell cmdlet toomanage bir uç noktasındaki ACL bkz [yönetme erişim denetim listeleri (ACL'ler) uç noktaları için PowerShell kullanarak](../../../virtual-network/virtual-networks-acl-powershell.md).
* Merhaba Resource Manager dağıtım modelinde bir sanal makine oluşturduysanız, Azure PowerShell kullanabileceğine[ağ güvenlik grupları oluşturma](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol trafiği toohello VM.
