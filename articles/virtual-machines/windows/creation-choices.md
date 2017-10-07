---
title: "aaaDifferent yolları toocreate Azure Windows VM | Microsoft Docs"
description: "Merhaba farklı şekillerde toocreate Resource Manager ile Windows sanal makine listeler."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 809ba8f4-b54e-43c5-bbe3-8e710c49971f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2928d4daa9b44c4d3a5083092a82c9a7f7c69fae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-windows-virtual-machine"></a>Farklı şekillerde toocreate Windows sanal makine

Sanal makineler farklı kullanıcılar ve amaçlar için uygundur çünkü azure sanal makine farklı şekillerde toocreate sunar. Bu hello sanal makine hakkında bazı seçenekler toomake gerektiği anlamına gelir ve nasıl toocreate onu. Bu makalede, bu seçenek bir özetini verir ve tooinstructions bağlar.

## <a name="azure-portal"></a>Azure portalına
Özellikle, yalnızca Azure ile başlıyorsanız hello Azure portal kullanarak basit bir yol tootry bir sanal makine çıkışı değildir. 

[Hello portal kullanarak Windows çalıştıran bir sanal makine oluşturma](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a>Şablon
Sanal makinelerin, kaynakların bileşimini gerekir (bir kullanılabilirlik gibi ayarlar ve depolama hesapları). Dağıtma ve her bir kaynağın ayrı ayrı yönetmek yerine, dağıtır ve tüm hello kaynakları tek ve eşgüdümlü bir işlemle sağlayan bir Azure Resource Manager şablonu oluşturabilirsiniz.

* [Resource Manager şablonu kullanarak Windows sanal makine oluşturma](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a>Azure PowerShell
Bir komut kabuğunda çalışma tercih ederseniz, Azure PowerShell'i kullanabilirsiniz.

* [PowerShell kullanarak Windows VM oluşturma](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a>Visual Studio
Visual Studio toobuild kullanın, Yönet'i ve VM'ler hello Azure Araçları ile Visual Studio için dağıtmak ve Azure SDK'sı hello.

[Visual Studio için Azure Araçları](https://www.visualstudio.com/features/azure-tools-vs)

