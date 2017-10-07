---
title: "aaaAzure CLI komut dosyası örneği ile toplu işi - | Microsoft Docs"
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
ms.openlocfilehash: f73a7cb341e550fd1c92f92201e20b27fa20d238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a><span data-ttu-id="36faa-103">Azure CLI ile Azure batch işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="36faa-103">Running jobs on Azure Batch with Azure CLI</span></span>

<span data-ttu-id="36faa-104">Bu komut dosyası toplu iş oluşturur ve bir dizi görevleri toohello iş ekler.</span><span class="sxs-lookup"><span data-stu-id="36faa-104">This script creates a Batch job and adds a series of tasks toohello job.</span></span> <span data-ttu-id="36faa-105">Ayrıca gösterir nasıl toomonitor bir işi ve görevleri.</span><span class="sxs-lookup"><span data-stu-id="36faa-105">It also demonstrates how toomonitor a job and its tasks.</span></span> <span data-ttu-id="36faa-106">Son olarak, nasıl tooquery hello Batch hizmeti hello işin görevler hakkında bilgi için verimli bir şekilde gösterir.</span><span class="sxs-lookup"><span data-stu-id="36faa-106">Finally, it shows how tooquery hello Batch service efficiently for information about hello job's tasks.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36faa-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="36faa-107">Prerequisites</span></span>

- <span data-ttu-id="36faa-108">Yükleme hello hello sağlanan hello yönergeleri kullanarak Azure CLI [Azure CLI Yükleme Kılavuzu'na](https://docs.microsoft.com/cli/azure/install-azure-cli)zaten yapmadıysanız,.</span><span class="sxs-lookup"><span data-stu-id="36faa-108">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="36faa-109">Zaten yoksa, bir toplu işlem hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="36faa-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="36faa-110">Bkz: [hello Azure CLI ile bir toplu işlem hesabı oluşturun](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) bir hesap oluşturan bir örnek komut dosyası için.</span><span class="sxs-lookup"><span data-stu-id="36faa-110">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="36faa-111">Henüz yapmadıysanız, bir uygulama toorun başlangıç görevden yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="36faa-111">Configure an application toorun from a start task if you haven't yet done so.</span></span> <span data-ttu-id="36faa-112">Bkz: [uygulamaları tooAzure Azure CLI ile toplu ekleme](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) bir uygulama oluşturur ve bir uygulama paketi tooAzure yükler bir örnek komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="36faa-112">See [Adding applications tooAzure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package tooAzure.</span></span>
- <span data-ttu-id="36faa-113">Hangi hello üzerinde iş çalıştırılır havuzunu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="36faa-113">Configure a pool on which hello job will run.</span></span> <span data-ttu-id="36faa-114">Bkz: [Azure CLI ile yönetme Azure Batch havuzları](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) bir bulut hizmet yapılandırması veya bir sanal makine yapılandırması ile bir havuz oluşturur bir örnek komut dosyası için.</span><span class="sxs-lookup"><span data-stu-id="36faa-114">See [Managing Azure Batch pools with Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) for a sample script that creates a pool with either a Cloud Service Configuration or a Virtual Machine Configuration.</span></span>

## <a name="sample-script"></a><span data-ttu-id="36faa-115">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="36faa-115">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]

## <a name="clean-up-job"></a><span data-ttu-id="36faa-116">İş temizleme</span><span class="sxs-lookup"><span data-stu-id="36faa-116">Clean up job</span></span>

<span data-ttu-id="36faa-117">Örnek betik yukarıdaki hello çalıştırdıktan sonra iş ve tüm görevleri komutu tooremove aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="36faa-117">After you run hello above sample script, run hello following command tooremove the job and all of its tasks.</span></span> <span data-ttu-id="36faa-118">Merhaba havuzu ayrı ayrı silinmiş toobe gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="36faa-118">Note that hello pool will need toobe deleted separately.</span></span> <span data-ttu-id="36faa-119">Bkz: [Azure CLI ile yönetme Azure Batch havuzları](./batch-cli-sample-manage-pool.md) oluşturma ve havuzların silinmesi hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="36faa-119">See [Managing Azure Batch pools with Azure CLI](./batch-cli-sample-manage-pool.md) for more information on creating and deleting pools.</span></span>

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a><span data-ttu-id="36faa-120">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="36faa-120">Script explanation</span></span>

<span data-ttu-id="36faa-121">Bu komut dosyası, bir toplu işi ve görevleri komutları toocreate aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="36faa-121">This script uses hello following commands toocreate a Batch job and tasks.</span></span> <span data-ttu-id="36faa-122">Her komut hello tablosundaki toocommand özgü belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="36faa-122">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="36faa-123">Komut</span><span class="sxs-lookup"><span data-stu-id="36faa-123">Command</span></span> | <span data-ttu-id="36faa-124">Notlar</span><span class="sxs-lookup"><span data-stu-id="36faa-124">Notes</span></span> |
|---|---|
| [<span data-ttu-id="36faa-125">az toplu işlem hesabı oturum açma</span><span class="sxs-lookup"><span data-stu-id="36faa-125">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="36faa-126">Toplu işlem hesabı karşı kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="36faa-126">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="36faa-127">az toplu işlem işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="36faa-127">az batch job create</span></span>](https://docs.microsoft.com/cli/azure/batch/job#create) | <span data-ttu-id="36faa-128">Bir toplu işi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="36faa-128">Creates a Batch job.</span></span>  |
| [<span data-ttu-id="36faa-129">az toplu işi ayarlama</span><span class="sxs-lookup"><span data-stu-id="36faa-129">az batch job set</span></span>](https://docs.microsoft.com/cli/azure/batch/job#set) | <span data-ttu-id="36faa-130">Toplu iş özelliklerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="36faa-130">Updates properties of a Batch job.</span></span>  |
| [<span data-ttu-id="36faa-131">az toplu işi Göster</span><span class="sxs-lookup"><span data-stu-id="36faa-131">az batch job show</span></span>](https://docs.microsoft.com/cli/azure/batch/job#show) | <span data-ttu-id="36faa-132">Belirtilen toplu iş ayrıntılarını alır.</span><span class="sxs-lookup"><span data-stu-id="36faa-132">Retrieves details of a specified Batch job.</span></span>  |
| [<span data-ttu-id="36faa-133">az toplu görev oluşturma</span><span class="sxs-lookup"><span data-stu-id="36faa-133">az batch task create</span></span>](https://docs.microsoft.com/cli/azure/batch/task#create) | <span data-ttu-id="36faa-134">Toplu Görev toohello belirtilen ekler.</span><span class="sxs-lookup"><span data-stu-id="36faa-134">Adds a task toohello specified Batch job.</span></span>  |
| [<span data-ttu-id="36faa-135">az toplu görev Göster</span><span class="sxs-lookup"><span data-stu-id="36faa-135">az batch task show</span></span>](https://docs.microsoft.com/cli/azure/batch/task#show) | <span data-ttu-id="36faa-136">Merhaba görevden alır hello ayrıntılarını toplu işlem belirtildi.</span><span class="sxs-lookup"><span data-stu-id="36faa-136">Retrieves hello details of a task from hello specified Batch job.</span></span>  |
| [<span data-ttu-id="36faa-137">az toplu görev listesi</span><span class="sxs-lookup"><span data-stu-id="36faa-137">az batch task list</span></span>](https://docs.microsoft.com/cli/azure/batch/task#list) | <span data-ttu-id="36faa-138">Merhaba belirtilen işlemle ilişkili hello görevleri listeler.</span><span class="sxs-lookup"><span data-stu-id="36faa-138">Lists hello tasks associated with hello specified job.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="36faa-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="36faa-139">Next steps</span></span>

<span data-ttu-id="36faa-140">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="36faa-140">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="36faa-141">Ek toplu CLI kod örnekleri hello bulunabilir [Azure Batch CLI belgelerine](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="36faa-141">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
