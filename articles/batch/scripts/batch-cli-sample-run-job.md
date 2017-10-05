---
title: "Azure CLI komut dosyası örneği ile toplu işi - | Microsoft Docs"
description: "Azure CLI komut dosyası örneği ile toplu işi-"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: 5fe1e3595d9459e60b2fd54d6f17f6822731f453
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a><span data-ttu-id="c0390-103">Azure CLI ile Azure batch işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c0390-103">Running jobs on Azure Batch with Azure CLI</span></span>

<span data-ttu-id="c0390-104">Bu komut dosyası toplu iş oluşturur ve bir dizi görev projeye ekler.</span><span class="sxs-lookup"><span data-stu-id="c0390-104">This script creates a Batch job and adds a series of tasks to the job.</span></span> <span data-ttu-id="c0390-105">Ayrıca, bir işi ve görevleri izleme gösterir.</span><span class="sxs-lookup"><span data-stu-id="c0390-105">It also demonstrates how to monitor a job and its tasks.</span></span> <span data-ttu-id="c0390-106">Son olarak, Batch hizmeti iş görevler hakkında bilgi için verimli bir şekilde sorgulama gösterir.</span><span class="sxs-lookup"><span data-stu-id="c0390-106">Finally, it shows how to query the Batch service efficiently for information about the job's tasks.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0390-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c0390-107">Prerequisites</span></span>

- <span data-ttu-id="c0390-108">Sağlanan yönergeleri kullanarak Azure CLI yükleme [Azure CLI Yükleme Kılavuzu'na](https://docs.microsoft.com/cli/azure/install-azure-cli)zaten yapmadıysanız,.</span><span class="sxs-lookup"><span data-stu-id="c0390-108">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="c0390-109">Zaten yoksa, bir toplu işlem hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c0390-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="c0390-110">Bkz: [Azure CLI ile bir toplu işlem hesabı oluşturun](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) bir hesap oluşturan bir örnek komut dosyası için.</span><span class="sxs-lookup"><span data-stu-id="c0390-110">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="c0390-111">Henüz yapmadıysanız bir başlangıç görevi çalıştırmak için bir uygulamayı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c0390-111">Configure an application to run from a start task if you haven't yet done so.</span></span> <span data-ttu-id="c0390-112">Bkz: [Azure CLI ile Azure Batch uygulamalarına ekleme](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) bir uygulama oluşturur ve Azure'a bir uygulama paketi yükler bir örnek komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="c0390-112">See [Adding applications to Azure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package to Azure.</span></span>
- <span data-ttu-id="c0390-113">İşin çalışacağı havuzunu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c0390-113">Configure a pool on which the job will run.</span></span> <span data-ttu-id="c0390-114">Bkz: [Azure CLI ile yönetme Azure Batch havuzları](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) bir bulut hizmet yapılandırması veya bir sanal makine yapılandırması ile bir havuz oluşturur bir örnek komut dosyası için.</span><span class="sxs-lookup"><span data-stu-id="c0390-114">See [Managing Azure Batch pools with Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) for a sample script that creates a pool with either a Cloud Service Configuration or a Virtual Machine Configuration.</span></span>

## <a name="sample-script"></a><span data-ttu-id="c0390-115">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="c0390-115">Sample script</span></span>

<span data-ttu-id="c0390-116">[!code-azurecli[Ana](../../../cli_scripts/batch/run-job/run-job.sh "iş")]</span><span class="sxs-lookup"><span data-stu-id="c0390-116">[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]</span></span>

## <a name="clean-up-job"></a><span data-ttu-id="c0390-117">İş temizleme</span><span class="sxs-lookup"><span data-stu-id="c0390-117">Clean up job</span></span>

<span data-ttu-id="c0390-118">Yukarıdaki örnek komut dosyasını çalıştırdıktan sonra iş ve tüm görevleri kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c0390-118">After you run the above sample script, run the following command to remove the job and all of its tasks.</span></span> <span data-ttu-id="c0390-119">Havuz ayrı olarak silinmesi gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c0390-119">Note that the pool will need to be deleted separately.</span></span> <span data-ttu-id="c0390-120">Bkz: [Azure CLI ile yönetme Azure Batch havuzları](./batch-cli-sample-manage-pool.md) oluşturma ve havuzların silinmesi hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="c0390-120">See [Managing Azure Batch pools with Azure CLI](./batch-cli-sample-manage-pool.md) for more information on creating and deleting pools.</span></span>

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a><span data-ttu-id="c0390-121">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="c0390-121">Script explanation</span></span>

<span data-ttu-id="c0390-122">Bu komut dosyasını aşağıdaki komutları bir toplu işi ve görevleri oluşturmak üzere kullanır.</span><span class="sxs-lookup"><span data-stu-id="c0390-122">This script uses the following commands to create a Batch job and tasks.</span></span> <span data-ttu-id="c0390-123">Komut özgü belgelere Tablo bağlantıları her komut.</span><span class="sxs-lookup"><span data-stu-id="c0390-123">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="c0390-124">Komut</span><span class="sxs-lookup"><span data-stu-id="c0390-124">Command</span></span> | <span data-ttu-id="c0390-125">Notlar</span><span class="sxs-lookup"><span data-stu-id="c0390-125">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c0390-126">az toplu işlem hesabı oturum açma</span><span class="sxs-lookup"><span data-stu-id="c0390-126">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="c0390-127">Toplu işlem hesabı karşı kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="c0390-127">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="c0390-128">az toplu işlem işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c0390-128">az batch job create</span></span>](https://docs.microsoft.com/cli/azure/batch/job#create) | <span data-ttu-id="c0390-129">Bir toplu işi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c0390-129">Creates a Batch job.</span></span>  |
| [<span data-ttu-id="c0390-130">az toplu işi ayarlama</span><span class="sxs-lookup"><span data-stu-id="c0390-130">az batch job set</span></span>](https://docs.microsoft.com/cli/azure/batch/job#set) | <span data-ttu-id="c0390-131">Toplu iş özelliklerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="c0390-131">Updates properties of a Batch job.</span></span>  |
| [<span data-ttu-id="c0390-132">az toplu işi Göster</span><span class="sxs-lookup"><span data-stu-id="c0390-132">az batch job show</span></span>](https://docs.microsoft.com/cli/azure/batch/job#show) | <span data-ttu-id="c0390-133">Belirtilen toplu iş ayrıntılarını alır.</span><span class="sxs-lookup"><span data-stu-id="c0390-133">Retrieves details of a specified Batch job.</span></span>  |
| [<span data-ttu-id="c0390-134">az toplu görev oluşturma</span><span class="sxs-lookup"><span data-stu-id="c0390-134">az batch task create</span></span>](https://docs.microsoft.com/cli/azure/batch/task#create) | <span data-ttu-id="c0390-135">Belirtilen toplu iş bir görev ekler.</span><span class="sxs-lookup"><span data-stu-id="c0390-135">Adds a task to the specified Batch job.</span></span>  |
| [<span data-ttu-id="c0390-136">az toplu görev Göster</span><span class="sxs-lookup"><span data-stu-id="c0390-136">az batch task show</span></span>](https://docs.microsoft.com/cli/azure/batch/task#show) | <span data-ttu-id="c0390-137">Bir görev ayrıntılarını ve belirtilen toplu işinden alır.</span><span class="sxs-lookup"><span data-stu-id="c0390-137">Retrieves the details of a task from the specified Batch job.</span></span>  |
| [<span data-ttu-id="c0390-138">az toplu görev listesi</span><span class="sxs-lookup"><span data-stu-id="c0390-138">az batch task list</span></span>](https://docs.microsoft.com/cli/azure/batch/task#list) | <span data-ttu-id="c0390-139">Belirtilen işlemle ilişkili görevleri listeler.</span><span class="sxs-lookup"><span data-stu-id="c0390-139">Lists the tasks associated with the specified job.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="c0390-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c0390-140">Next steps</span></span>

<span data-ttu-id="c0390-141">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c0390-141">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c0390-142">Ek toplu CLI kod örnekleri bulunabilir [Azure Batch CLI belgelerine](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c0390-142">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
