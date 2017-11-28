---
title: "aaaAzure CLI komut dosyası örneği - ACS Linux Kubernetes küme oluşturma | Microsoft Docs"
description: "Azure CLI örnek komut dosyası - ACS Linux Kubernetes kümesi oluşturma"
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
ms.openlocfilehash: cf3798ea8b08e3fc32acb35dabab4b2fbea179dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-container-service-kubernetes-linux-cluster"></a><span data-ttu-id="04c8c-104">Bir Azure kapsayıcı hizmeti Kubernetes Linux kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="04c8c-104">Create an Azure Container Service Kubernetes Linux Cluster</span></span>

<span data-ttu-id="04c8c-105">Bu örnek için Linux tabanlı kapsayıcılar Kubernetes çalıştıran bir Azure kapsayıcı hizmeti kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="04c8c-105">This sample creates an Azure Container Service cluster running Kubernetes for Linux based containers.</span></span>

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="04c8c-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="04c8c-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type kubernetes \
  --resource-group myResourceGroup \
  --name myK8SCluster \
  --generate-ssh-keys
```

## <a name="clean-up-deployment"></a><span data-ttu-id="04c8c-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="04c8c-107">Clean up deployment</span></span> 

<span data-ttu-id="04c8c-108">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="04c8c-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="04c8c-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="04c8c-109">Script explanation</span></span>

<span data-ttu-id="04c8c-110">Bu komut dosyası komutları toocreate hello dağıtım aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="04c8c-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="04c8c-111">Merhaba tablosundaki her öğesi toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="04c8c-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="04c8c-112">Komut</span><span class="sxs-lookup"><span data-stu-id="04c8c-112">Command</span></span> | <span data-ttu-id="04c8c-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="04c8c-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="04c8c-114">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="04c8c-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="04c8c-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="04c8c-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="04c8c-116">acs az oluşturma</span><span class="sxs-lookup"><span data-stu-id="04c8c-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="04c8c-117">Oluşturur ve ACS küme.</span><span class="sxs-lookup"><span data-stu-id="04c8c-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="04c8c-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="04c8c-118">Next steps</span></span>

<span data-ttu-id="04c8c-119">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="04c8c-119">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="04c8c-120">Ek Azure kapsayıcı hizmeti CLI kod örnekleri hello bulunabilir [Azure kapsayıcı hizmeti belgeleri](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="04c8c-120">Additional Azure Container Service CLI script samples can be found in hello [Azure Container Service documentation](../cli-samples.md).</span></span>

