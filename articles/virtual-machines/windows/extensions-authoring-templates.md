---
title: "Windows VM uzantıları ile aaaAuthoring şablonları | Microsoft Docs"
description: "Windows VM'ler için uzantılı Azure Resource Manager şablonları yazma hakkında bilgi edinin"
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 418dd1f7-ded8-45ab-9a5a-a59d245e2555
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: c5156cb3859f7ff86bebda942150d268e57d6486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a>Windows VM uzantıları ile Azure Resource Manager şablonları yazma
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

Azure PowerShell hello aşağıdaki Azure PowerShell cmdlet'ini çalıştırın:

      Get-AzureVMAvailableExtension


Bu cmdlet hello Yayımcı adı, uzantı adı ve sürümü gibi döndürür:

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

Örnek yapılandırması için Windows uzantıları adresindeki toolook bkz [Windows uzantıları örnekleri](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Lütfen tooget VM uzantıları ile tam olarak tam bir şablon aşağıdaki toohello bakın.

[Bir Windows VM özel betik uzantısı](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

Merhaba şablon yazma sonra Azure PowerShell kullanarak dağıtabilirsiniz.

