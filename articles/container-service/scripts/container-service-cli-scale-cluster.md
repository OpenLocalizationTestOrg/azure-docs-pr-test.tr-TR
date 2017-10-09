---
title: "aaaAzure CLI komut dosyası örneği - bir ACS küme ölçeklendirin | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - ölçek ACS küme"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Container’lar, Mikro hizmetler, Kumernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: nepeters
ms.openlocfilehash: b1c214d7cca615257ec8cd6e9993cd15f694289b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-an-azure-container-service-cluster"></a><span data-ttu-id="2e4a9-104">Bir Azure kapsayıcı hizmeti kümesini ölçeklendirin</span><span class="sxs-lookup"><span data-stu-id="2e4a9-104">Scale an Azure Container Service Cluster</span></span>

<span data-ttu-id="2e4a9-105">Bu örnek ölçekler ve Azure kapsayıcı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="2e4a9-105">This sample scales and Azure Container Service.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2e4a9-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="2e4a9-106">Sample script</span></span>

```azurecli
az acs scale --resource-group myResourceGroup --name myK8SCluster --new-agent-count 5
```

## <a name="clean-up-deployment"></a><span data-ttu-id="2e4a9-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="2e4a9-107">Clean up deployment</span></span> 

<span data-ttu-id="2e4a9-108">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="2e4a9-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="2e4a9-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="2e4a9-109">Script explanation</span></span>

<span data-ttu-id="2e4a9-110">Bu komut dosyası komutları toocreate hello dağıtım aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="2e4a9-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="2e4a9-111">Merhaba tablosundaki her öğesi toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="2e4a9-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2e4a9-112">Komut</span><span class="sxs-lookup"><span data-stu-id="2e4a9-112">Command</span></span> | <span data-ttu-id="2e4a9-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="2e4a9-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2e4a9-114">az acs ölçek</span><span class="sxs-lookup"><span data-stu-id="2e4a9-114">az acs scale</span></span>](/cli/azure/acs#scale) | <span data-ttu-id="2e4a9-115">Bir ACS küme ölçeklendirme.</span><span class="sxs-lookup"><span data-stu-id="2e4a9-115">Scale an ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2e4a9-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2e4a9-116">Next steps</span></span>

<span data-ttu-id="2e4a9-117">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2e4a9-117">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2e4a9-118">Ek Azure kapsayıcı hizmeti CLI kod örnekleri hello bulunabilir [Azure kapsayıcı hizmeti belgeleri](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2e4a9-118">Additional Azure Container Service CLI script samples can be found in hello [Azure Container Service documentation](../cli-samples.md).</span></span>

