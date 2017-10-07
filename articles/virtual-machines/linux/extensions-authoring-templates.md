---
title: "Linux VM uzantıları aaaAuthoring şablonlarıyla | Microsoft Docs"
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
ms.openlocfilehash: b797e442d8706956bbc06c5be611a2b0119055d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a>Linux VM uzantıları ile Azure Resource Manager şablonları yazma
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

Azure CLI üzerinden commnad aşağıdaki hello çalıştırın:

      Azure VM extension list

Bu komut döndürür hello Yayımcı adı, uzantı adı ve sürümü aşağıdaki olarak:

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

Bu üç özellik çok harita "publisher", "tür" ve "typeHandlerVersion" hello şablon parçacığı yukarıda sırasıyla içinde.

> [!NOTE]
> Her zaman, önerilen toouse hello son uzantısı sürüm tooget en güncelleştirilmiş hello işlevselliğini gerçekleşir.
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a>Merhaba uzantısı yapılandırma parametreleri için Hello Şeması Tanımlama
Sonraki adım bir uzantı şablon yazma ile Merhaba yapılandırma parametreleri sağlamak için tooidentify hello biçimidir. Her bir uzantı kendi parametreleri kümesini destekler.

Linux uzantıları için örnek yapılandırması sırasında toolook tıklatın hello belgelerine bakın [Linux eExtensions örnekleri](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Lütfen tooget VM uzantıları ile tam olarak tam bir şablon aşağıdaki toohello bakın.

[Bir Linux VM özel betik uzantısı](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

Merhaba şablon yazma sonra hello Azure CLI kullanarak dağıtabilirsiniz.

