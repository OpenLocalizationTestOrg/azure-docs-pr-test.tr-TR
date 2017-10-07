---
title: kullanarak bir Linux VM Klasik aaaCreate hello Azure CLI 1.0 | Microsoft Docs
description: "Nasıl toocreate hello Azure CLI 1.0 kullanarak Linux sanal makine hello Klasik dağıtım modeli öğrenin"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: f8071a2e-ed91-4f77-87d9-519a37e5364f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 5c3c54e5d1444a79e8e609c76d04a3a621c8d03f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-classic-linux-vm-with-hello-azure-cli-10"></a>Nasıl tooCreate klasik bir Linux VM ile bir hello Azure CLI 1.0
> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Merhaba Resource Manager sürümü için bkz: [burada](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Bu konuda nasıl toocreate Linux sanal hello Azure CLI 1.0 kullanarak makine (VM) hello Klasik dağıtım modeli açıklanmaktadır. Merhaba kullanılabilir Linux görüntüden kullanırız **GÖRÜNTÜLERİ** Azure üzerinde. Hello Azure CLI 1.0 komutları diğerlerinin yanı sıra yapılandırma seçeneklerinin aşağıdaki hello verin:

* Merhaba VM tooa sanal ağa bağlanma
* Merhaba VM tooan mevcut bulut hizmeti ekleme
* Merhaba VM tooan var olan depolama hesabı ekleme
* Merhaba VM tooan kullanılabilirlik kümesi veya Konum ekleme

> [!IMPORTANT]
> Ana bilgisayar adı veya şirket içi bağlantılar kurma tarafından doğrudan tooit bağlanabilmesi için bir sanal ağ, VM toouse istiyorsanız, hello VM oluşturduğunuzda hello sanal ağ belirttiğinizden emin olun. Yalnızca hello VM oluşturduğunuzda bir VM yapılandırılmış toojoin sanal bir ağ olabilir. Sanal ağlar hakkında daha fazla bilgi için bkz: [Azure Virtual Network'e genel bakış](http://go.microsoft.com/fwlink/p/?LinkID=294063).
> 
> 

## <a name="how-toocreate-a-linux-vm-using-hello-classic-deployment-model"></a>Nasıl toocreate kullanarak Linux VM bir hello Klasik dağıtım modeli
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]

