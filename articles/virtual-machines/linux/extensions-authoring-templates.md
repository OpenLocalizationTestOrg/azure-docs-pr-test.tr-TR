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
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a><span data-ttu-id="c14c0-103">Linux VM uzantıları ile Azure Resource Manager şablonları yazma</span><span class="sxs-lookup"><span data-stu-id="c14c0-103">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="c14c0-104">Azure CLI üzerinden aşağıdaki commnad çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c14c0-104">From Azure CLI, run the following commnad:</span></span>

      Azure VM extension list

<span data-ttu-id="c14c0-105">Bu komut, yayımcı adı, uzantı adı ve sürümü aşağıdaki olarak döndürür:</span><span class="sxs-lookup"><span data-stu-id="c14c0-105">This command returns the publisher name, extension name and version as following:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="c14c0-106">"Publisher", "tür" ve "typeHandlerVersion" sırasıyla yukarıdaki şablonu parçacığında bulunan üç bu özellikleri eşleyin.</span><span class="sxs-lookup"><span data-stu-id="c14c0-106">These three properties map to "publisher", "type", and "typeHandlerVersion" respectively in the above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="c14c0-107">Bu her zaman en son uzantısı sürüm en güncel işlevselliğini kazanması için kullanılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="c14c0-107">It's always recommended to use the latest extension version to get the most updated functionality.</span></span>
> 
> 

## <a name="identifying-the-schema-for-the-extension-configuration-parameters"></a><span data-ttu-id="c14c0-108">Şema uzantısı yapılandırma parametreleri için tanımlama</span><span class="sxs-lookup"><span data-stu-id="c14c0-108">Identifying the schema for the extension configuration parameters</span></span>
<span data-ttu-id="c14c0-109">Bir uzantı şablon yazma ile sonraki adım, yapılandırma parametreleri sağlamak için biçimi belirlemektir.</span><span class="sxs-lookup"><span data-stu-id="c14c0-109">The next step with authoring an extension template is to identify the format for providing configuration parameters.</span></span> <span data-ttu-id="c14c0-110">Her bir uzantı kendi parametreleri kümesini destekler.</span><span class="sxs-lookup"><span data-stu-id="c14c0-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="c14c0-111">Linux uzantıları için örnek yapılandırmaları bakmak için belgelere bakın tıklatın [Linux eExtensions örnekleri](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c14c0-111">To look at sample configurations for Linux extensions, click the documentation for see [Linux eExtensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="c14c0-112">Lütfen VM uzantıları ile tam olarak tam bir şablon almak için aşağıdakini bakın.</span><span class="sxs-lookup"><span data-stu-id="c14c0-112">Please refer to the following to get a fully complete template with VM Extensions.</span></span>

[<span data-ttu-id="c14c0-113">Bir Linux VM özel betik uzantısı</span><span class="sxs-lookup"><span data-stu-id="c14c0-113">Custom script extension on a Linux VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

<span data-ttu-id="c14c0-114">Şablon yazma sonra Azure CLI kullanarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c14c0-114">After authoring the template, you can deploy it using the Azure CLI.</span></span>

