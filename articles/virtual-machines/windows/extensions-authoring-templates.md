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
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a><span data-ttu-id="4bdd0-103">Windows VM uzantıları ile Azure Resource Manager şablonları yazma</span><span class="sxs-lookup"><span data-stu-id="4bdd0-103">Authoring Azure Resource Manager templates with Windows VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="4bdd0-104">Azure PowerShell hello aşağıdaki Azure PowerShell cmdlet'ini çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4bdd0-104">From Azure PowerShell, run hello following Azure PowerShell cmdlet:</span></span>

      Get-AzureVMAvailableExtension


<span data-ttu-id="4bdd0-105">Bu cmdlet hello Yayımcı adı, uzantı adı ve sürümü gibi döndürür:</span><span class="sxs-lookup"><span data-stu-id="4bdd0-105">This cmdlet returns hello publisher name, extension name, and version as follows:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="4bdd0-106">Bu üç özellik çok harita "publisher", "tür" ve "typeHandlerVersion" hello şablon parçacığı yukarıda sırasıyla içinde.</span><span class="sxs-lookup"><span data-stu-id="4bdd0-106">These three properties map too"publisher", "type", and "typeHandlerVersion" respectively in hello above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="4bdd0-107">Her zaman, önerilen toouse hello son uzantısı sürüm tooget en güncelleştirilmiş hello işlevselliğini gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="4bdd0-107">It's always recommended toouse hello latest extension version tooget hello most updated functionality.</span></span>
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a><span data-ttu-id="4bdd0-108">Merhaba uzantısı yapılandırma parametreleri için Hello Şeması Tanımlama</span><span class="sxs-lookup"><span data-stu-id="4bdd0-108">Identifying hello schema for hello extension configuration parameters</span></span>
<span data-ttu-id="4bdd0-109">Sonraki adım bir uzantı şablon yazma ile Merhaba yapılandırma parametreleri sağlamak için tooidentify hello biçimidir.</span><span class="sxs-lookup"><span data-stu-id="4bdd0-109">hello next step with authoring an extension template is tooidentify hello format for providing configuration parameters.</span></span> <span data-ttu-id="4bdd0-110">Her bir uzantı kendi parametreleri kümesini destekler.</span><span class="sxs-lookup"><span data-stu-id="4bdd0-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="4bdd0-111">Örnek yapılandırması için Windows uzantıları adresindeki toolook bkz [Windows uzantıları örnekleri](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4bdd0-111">toolook at sample configurations for Windows extensions, see [Windows extensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="4bdd0-112">Lütfen tooget VM uzantıları ile tam olarak tam bir şablon aşağıdaki toohello bakın.</span><span class="sxs-lookup"><span data-stu-id="4bdd0-112">Please refer toohello following tooget a fully complete template with VM extensions.</span></span>

[<span data-ttu-id="4bdd0-113">Bir Windows VM özel betik uzantısı</span><span class="sxs-lookup"><span data-stu-id="4bdd0-113">Custom Script Extension on a Windows VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

<span data-ttu-id="4bdd0-114">Merhaba şablon yazma sonra Azure PowerShell kullanarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4bdd0-114">After authoring hello template, you can deploy it using Azure PowerShell.</span></span>

