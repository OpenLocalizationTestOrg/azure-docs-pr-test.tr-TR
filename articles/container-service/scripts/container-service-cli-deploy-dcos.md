---
title: "Azure CLI örnek komut dosyası - ACS DC/OS kümesi oluşturun. | Microsoft Docs"
description: "Azure CLI örnek komut dosyası - ACS DC/OS kümesi oluşturma"
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
ms.openlocfilehash: 4efd7dea04fd3486f875e57737e438c966872dd4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="80b63-104">Bir Azure kapsayıcı hizmeti DC/OS kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="80b63-104">Create an Azure Container Service DC/OS Cluster</span></span>

<span data-ttu-id="80b63-105">Bu örnek DCOS çalıştıran bir Azure kapsayıcı hizmeti kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="80b63-105">This sample creates an Azure Container Service cluster running DCOS.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="80b63-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="80b63-106">Sample script</span></span>

```azurecli
az group create --name myResourceGroup --location eastus

az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

## <a name="clean-up-deployment"></a><span data-ttu-id="80b63-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="80b63-107">Clean up deployment</span></span> 

<span data-ttu-id="80b63-108">Kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="80b63-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="80b63-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="80b63-109">Script explanation</span></span>

<span data-ttu-id="80b63-110">Bu komut dosyası dağıtımı oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="80b63-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="80b63-111">Komut belirli belgeleri tablo bağlanan her öğe.</span><span class="sxs-lookup"><span data-stu-id="80b63-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="80b63-112">Komut</span><span class="sxs-lookup"><span data-stu-id="80b63-112">Command</span></span> | <span data-ttu-id="80b63-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="80b63-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="80b63-114">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="80b63-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="80b63-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="80b63-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="80b63-116">acs az oluşturma</span><span class="sxs-lookup"><span data-stu-id="80b63-116">az acs create</span></span>](https://docs.microsoft.com/cli/azure/acs#create) | <span data-ttu-id="80b63-117">Oluşturur ve ACS küme.</span><span class="sxs-lookup"><span data-stu-id="80b63-117">Creates and ACS cluster.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="80b63-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="80b63-118">Next steps</span></span>

<span data-ttu-id="80b63-119">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="80b63-119">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="80b63-120">Ek Azure kapsayıcı hizmeti CLI kod örnekleri bulunabilir [Azure kapsayıcı hizmeti belgeleri](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="80b63-120">Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).</span></span>