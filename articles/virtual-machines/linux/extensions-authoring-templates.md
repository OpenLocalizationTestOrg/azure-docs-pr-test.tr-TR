---
title: "Linux VM uzantıları şablonlarıyla geliştirme | Microsoft Docs"
description: "Linux VM'ler için uzantılı Azure Resource Manager şablonları yazma hakkında bilgi edinin"
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 322f8f0b-6697-4acb-b5f3-b3f58d28358b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 8b017306474670bf8dde1440128e16ec35146f24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a>Linux VM uzantıları ile Azure Resource Manager şablonları yazma
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

Azure CLI üzerinden aşağıdaki commnad çalıştırın:

      Azure VM extension list

Bu komut, yayımcı adı, uzantı adı ve sürümü aşağıdaki olarak döndürür:

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

"Publisher", "tür" ve "typeHandlerVersion" sırasıyla yukarıdaki şablonu parçacığında bulunan üç bu özellikleri eşleyin.

> [!NOTE]
> Bu her zaman en son uzantısı sürüm en güncel işlevselliğini kazanması için kullanılması önerilir.
> 
> 

## <a name="identifying-the-schema-for-the-extension-configuration-parameters"></a>Şema uzantısı yapılandırma parametreleri için tanımlama
Bir uzantı şablon yazma ile sonraki adım, yapılandırma parametreleri sağlamak için biçimi belirlemektir. Her bir uzantı kendi parametreleri kümesini destekler.

Linux uzantıları için örnek yapılandırmaları bakmak için belgelere bakın tıklatın [Linux eExtensions örnekleri](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Lütfen VM uzantıları ile tam olarak tam bir şablon almak için aşağıdakini bakın.

[Bir Linux VM özel betik uzantısı](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

Şablon yazma sonra Azure CLI kullanarak dağıtabilirsiniz.

