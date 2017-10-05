---
title: "Azure üzerinde bir Windows VM oluşturmanın farklı yolları | Microsoft Docs"
description: "Resource Manager ile Windows sanal makine oluşturmanın farklı yollarını listeler."
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
ms.openlocfilehash: 5e51c49aac01a22d86c7c1a12b2f2ca7ddc056bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="different-ways-to-create-a-windows-virtual-machine"></a>Windows sanal makine oluşturmanın farklı yolları

Azure sanal makineleri farklı kullanıcılar ve amaçlar için uygundur çünkü bir sanal makine oluşturmanın farklı yollarını sunar. Başka bir deyişle, sanal makine ve nasıl oluşturulduğu hakkında bazı seçim yapmanız gerekir. Bu makale için yönergeler bu seçimlere ve bağlantıları bir özetini verir.

## <a name="azure-portal"></a>Azure portalına
Özellikle, yalnızca Azure ile başlıyorsanız Azure portalını kullanarak bir sanal makine denemek için basit bir yoludur. 

[Portalı kullanarak Windows çalıştıran sanal makine oluşturma](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a>Şablon
Sanal makinelerin, kaynakların bileşimini gerekir (bir kullanılabilirlik gibi ayarlar ve depolama hesapları). Dağıtma ve her bir kaynağın ayrı ayrı yönetmek yerine, dağıtır ve tüm kaynakları tek ve eşgüdümlü bir işlemle sağlayan bir Azure Resource Manager şablonu oluşturabilirsiniz.

* [Resource Manager şablonu kullanarak Windows sanal makine oluşturma](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a>Azure PowerShell
Bir komut kabuğunda çalışma tercih ederseniz, Azure PowerShell'i kullanabilirsiniz.

* [PowerShell kullanarak Windows VM oluşturma](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a>Visual Studio
Visual Studio oluşturmak, yönetmek ve Visual Studio ve Azure SDK'sı için Azure Araçları ile sanal makineleri dağıtmak için kullanın.

[Visual Studio için Azure Araçları](https://www.visualstudio.com/features/azure-tools-vs)

