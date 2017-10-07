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
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a><span data-ttu-id="d2b1d-103">Linux VM uzantıları ile Azure Resource Manager şablonları yazma</span><span class="sxs-lookup"><span data-stu-id="d2b1d-103">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="d2b1d-104">Azure CLI üzerinden commnad aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d2b1d-104">From Azure CLI, run hello following commnad:</span></span>

      Azure VM extension list

<span data-ttu-id="d2b1d-105">Bu komut döndürür hello Yayımcı adı, uzantı adı ve sürümü aşağıdaki olarak:</span><span class="sxs-lookup"><span data-stu-id="d2b1d-105">This command returns hello publisher name, extension name and version as following:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="d2b1d-106">Bu üç özellik çok harita "publisher", "tür" ve "typeHandlerVersion" hello şablon parçacığı yukarıda sırasıyla içinde.</span><span class="sxs-lookup"><span data-stu-id="d2b1d-106">These three properties map too"publisher", "type", and "typeHandlerVersion" respectively in hello above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="d2b1d-107">Her zaman, önerilen toouse hello son uzantısı sürüm tooget en güncelleştirilmiş hello işlevselliğini gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="d2b1d-107">It's always recommended toouse hello latest extension version tooget hello most updated functionality.</span></span>
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a><span data-ttu-id="d2b1d-108">Merhaba uzantısı yapılandırma parametreleri için Hello Şeması Tanımlama</span><span class="sxs-lookup"><span data-stu-id="d2b1d-108">Identifying hello schema for hello extension configuration parameters</span></span>
<span data-ttu-id="d2b1d-109">Sonraki adım bir uzantı şablon yazma ile Merhaba yapılandırma parametreleri sağlamak için tooidentify hello biçimidir.</span><span class="sxs-lookup"><span data-stu-id="d2b1d-109">hello next step with authoring an extension template is tooidentify hello format for providing configuration parameters.</span></span> <span data-ttu-id="d2b1d-110">Her bir uzantı kendi parametreleri kümesini destekler.</span><span class="sxs-lookup"><span data-stu-id="d2b1d-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="d2b1d-111">Linux uzantıları için örnek yapılandırması sırasında toolook tıklatın hello belgelerine bakın [Linux eExtensions örnekleri](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d2b1d-111">toolook at sample configurations for Linux extensions, click hello documentation for see [Linux eExtensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="d2b1d-112">Lütfen tooget VM uzantıları ile tam olarak tam bir şablon aşağıdaki toohello bakın.</span><span class="sxs-lookup"><span data-stu-id="d2b1d-112">Please refer toohello following tooget a fully complete template with VM Extensions.</span></span>

[<span data-ttu-id="d2b1d-113">Bir Linux VM özel betik uzantısı</span><span class="sxs-lookup"><span data-stu-id="d2b1d-113">Custom script extension on a Linux VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

<span data-ttu-id="d2b1d-114">Merhaba şablon yazma sonra hello Azure CLI kullanarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d2b1d-114">After authoring hello template, you can deploy it using hello Azure CLI.</span></span>

