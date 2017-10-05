---
title: "Azure CLI komut dosyası örneği - ölçek ACS küme | Microsoft Docs"
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
ms.openlocfilehash: 0ea2c73436e650fdb37535538baccc565369fa9d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-an-azure-container-service-cluster"></a><span data-ttu-id="8f12c-104">Bir Azure kapsayıcı hizmeti kümesini ölçeklendirin</span><span class="sxs-lookup"><span data-stu-id="8f12c-104">Scale an Azure Container Service Cluster</span></span>

<span data-ttu-id="8f12c-105">Bu örnek ölçekler ve Azure kapsayıcı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="8f12c-105">This sample scales and Azure Container Service.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="8f12c-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="8f12c-106">Sample script</span></span>

```azurecli
az acs scale --resource-group myResourceGroup --name myK8SCluster --new-agent-count 5
```

## <a name="clean-up-deployment"></a><span data-ttu-id="8f12c-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="8f12c-107">Clean up deployment</span></span> 

<span data-ttu-id="8f12c-108">Kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8f12c-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="8f12c-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="8f12c-109">Script explanation</span></span>

<span data-ttu-id="8f12c-110">Bu komut dosyası dağıtımı oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="8f12c-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="8f12c-111">Komut belirli belgeleri tablo bağlanan her öğe.</span><span class="sxs-lookup"><span data-stu-id="8f12c-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8f12c-112">Komut</span><span class="sxs-lookup"><span data-stu-id="8f12c-112">Command</span></span> | <span data-ttu-id="8f12c-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="8f12c-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8f12c-114">az acs ölçek</span><span class="sxs-lookup"><span data-stu-id="8f12c-114">az acs scale</span></span>](/cli/azure/acs#scale) | <span data-ttu-id="8f12c-115">Bir ACS küme ölçeklendirme.</span><span class="sxs-lookup"><span data-stu-id="8f12c-115">Scale an ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8f12c-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8f12c-116">Next steps</span></span>

<span data-ttu-id="8f12c-117">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8f12c-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8f12c-118">Ek Azure kapsayıcı hizmeti CLI kod örnekleri bulunabilir [Azure kapsayıcı hizmeti belgeleri](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8f12c-118">Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).</span></span>

