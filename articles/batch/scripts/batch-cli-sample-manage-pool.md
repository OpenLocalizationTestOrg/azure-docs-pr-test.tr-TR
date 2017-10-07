---
title: "aaaAzure CLI komut dosyası örneği - toplu havuzlarını yönetme | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - Batch havuzlarında yönetme"
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
ms.openlocfilehash: 6c9ca9515565aff42752231a080943be8e4c810b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a><span data-ttu-id="26bdf-103">Azure Batch havuzları Azure CLI ile yönetme</span><span class="sxs-lookup"><span data-stu-id="26bdf-103">Managing Azure Batch pools with Azure CLI</span></span>

<span data-ttu-id="26bdf-104">Bu komut dosyası hello hello Azure CLI toocreate kullanılabilen araçların bazıları gösterir ve hello Azure Batch hizmeti işlem düğümlerine havuzlarını Yönet.</span><span class="sxs-lookup"><span data-stu-id="26bdf-104">These script demonstrates some of hello tools available in hello Azure CLI toocreate and manage pools of compute nodes in hello Azure Batch service.</span></span>

> [!NOTE]
> <span data-ttu-id="26bdf-105">Bu örnek komutlarda Hello Azure sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="26bdf-105">hello commands in this sample create Azure virtual machines.</span></span> <span data-ttu-id="26bdf-106">VM'ler çalıştıran ücretleri tooyour hesabı tahakkuk.</span><span class="sxs-lookup"><span data-stu-id="26bdf-106">Running VMs will accrue charges tooyour account.</span></span> <span data-ttu-id="26bdf-107">toominimize bu ücretlerden silin hello VM'ler çalışan hello örnek bitirdiğinizde.</span><span class="sxs-lookup"><span data-stu-id="26bdf-107">toominimize these charges, delete hello VMs once you're done running hello sample.</span></span> <span data-ttu-id="26bdf-108">Bkz: [havuzları temiz](#clean-up-pools).</span><span class="sxs-lookup"><span data-stu-id="26bdf-108">See [Clean up pools](#clean-up-pools).</span></span>

<span data-ttu-id="26bdf-109">Batch havuzları, bulut Hizmetleri Yapılandırması (yalnızca Windows) veya bir sanal makine yapılandırma (Windows ve Linux) iki şekilde yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="26bdf-109">Batch pools can be configured in two ways, either with a Cloud Services configuration (Windows only), or a Virtual Machine configuration (Windows and Linux).</span></span> <span data-ttu-id="26bdf-110">Aşağıdaki örnek komut Hello nasıl toocreate hem yapılandırmalarla havuzları gösterir.</span><span class="sxs-lookup"><span data-stu-id="26bdf-110">hello sample scripts below show how toocreate pools with both configurations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26bdf-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="26bdf-111">Prerequisites</span></span>

- <span data-ttu-id="26bdf-112">Yükleme hello hello sağlanan hello yönergeleri kullanarak Azure CLI [Azure CLI Yükleme Kılavuzu'na](https://docs.microsoft.com/cli/azure/install-azure-cli)zaten yapmadıysanız,.</span><span class="sxs-lookup"><span data-stu-id="26bdf-112">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="26bdf-113">Zaten yoksa, bir toplu işlem hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="26bdf-113">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="26bdf-114">Bkz: [hello Azure CLI ile bir toplu işlem hesabı oluşturun](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) bir hesap oluşturan bir örnek komut dosyası için.</span><span class="sxs-lookup"><span data-stu-id="26bdf-114">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="26bdf-115">Henüz yapmadıysanız, bir uygulama toorun başlangıç görevden yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="26bdf-115">Configure an application toorun from a start task if you haven't yet done so.</span></span> <span data-ttu-id="26bdf-116">Bkz: [uygulamaları tooAzure Azure CLI ile toplu ekleme](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) bir uygulama oluşturur ve bir uygulama paketi tooAzure yükler bir örnek komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="26bdf-116">See [Adding applications tooAzure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package tooAzure.</span></span>

## <a name="pool-with-cloud-service-configuration-sample-script"></a><span data-ttu-id="26bdf-117">Bulut hizmeti yapılandırma örnek komut dosyası havuzuyla</span><span class="sxs-lookup"><span data-stu-id="26bdf-117">Pool with cloud service configuration sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]

## <a name="pool-with-virtual-machine-configuration-sample-script"></a><span data-ttu-id="26bdf-118">Sanal makine yapılandırma örnek betiği havuzuyla</span><span class="sxs-lookup"><span data-stu-id="26bdf-118">Pool with virtual machine configuration sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]

## <a name="clean-up-pools"></a><span data-ttu-id="26bdf-119">Havuzları Temizle</span><span class="sxs-lookup"><span data-stu-id="26bdf-119">Clean up pools</span></span>

<span data-ttu-id="26bdf-120">Örnek betik yukarıdaki hello çalıştırdıktan sonra komutu toodelete hello havuzları aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="26bdf-120">After you run hello above sample script, run hello following command toodelete hello pools.</span></span>
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a><span data-ttu-id="26bdf-121">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="26bdf-121">Script explanation</span></span>

<span data-ttu-id="26bdf-122">Bu komut dosyası komutları toocreate aşağıdaki hello kullanır ve Batch havuzları arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="26bdf-122">This script uses hello following commands toocreate and manipulate Batch pools.</span></span>
<span data-ttu-id="26bdf-123">Her komut hello tablosundaki toocommand özgü belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="26bdf-123">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="26bdf-124">Komut</span><span class="sxs-lookup"><span data-stu-id="26bdf-124">Command</span></span> | <span data-ttu-id="26bdf-125">Notlar</span><span class="sxs-lookup"><span data-stu-id="26bdf-125">Notes</span></span> |
|---|---|
| [<span data-ttu-id="26bdf-126">az toplu işlem hesabı oturum açma</span><span class="sxs-lookup"><span data-stu-id="26bdf-126">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="26bdf-127">Toplu işlem hesabı karşı kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="26bdf-127">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="26bdf-128">az toplu uygulama Özet listesi</span><span class="sxs-lookup"><span data-stu-id="26bdf-128">az batch application summary list</span></span>](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | <span data-ttu-id="26bdf-129">Merhaba toplu işlem hesabı Hello kullanılabilir uygulamaları listeleyin.</span><span class="sxs-lookup"><span data-stu-id="26bdf-129">List hello available applications in hello Batch account.</span></span>  |
| [<span data-ttu-id="26bdf-130">az batch havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="26bdf-130">az batch pool create</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#create) | <span data-ttu-id="26bdf-131">Sanal makineleri havuzu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="26bdf-131">Create a pool of VMs.</span></span>  |
| [<span data-ttu-id="26bdf-132">az batch havuzu ayarlama</span><span class="sxs-lookup"><span data-stu-id="26bdf-132">az batch pool set</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#set) | <span data-ttu-id="26bdf-133">Bir havuz özelliklerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="26bdf-133">Update properties of a pool.</span></span>  |
| [<span data-ttu-id="26bdf-134">az batch havuzu düğüm Aracısı SKU listesi</span><span class="sxs-lookup"><span data-stu-id="26bdf-134">az batch pool node-agent-skus list</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | <span data-ttu-id="26bdf-135">Liste kullanılabilir düğüm Aracısı SKU'ları ve görüntü bilgileri.</span><span class="sxs-lookup"><span data-stu-id="26bdf-135">List available node agent SKUs and image information.</span></span>  |
| [<span data-ttu-id="26bdf-136">az batch havuzu yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="26bdf-136">az batch pool resize</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#resize) | <span data-ttu-id="26bdf-137">Yeniden boyutlandırma hello sayısı, sanal makineleri hello çalışan havuzu belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="26bdf-137">Resize hello number of running VMs in hello specified pool.</span></span>  |
| [<span data-ttu-id="26bdf-138">az batch havuzu Göster</span><span class="sxs-lookup"><span data-stu-id="26bdf-138">az batch pool show</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#show) | <span data-ttu-id="26bdf-139">Bir havuzu Hello özelliklerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="26bdf-139">Display hello properties of a pool.</span></span>  |
| [<span data-ttu-id="26bdf-140">az batch havuzu silme</span><span class="sxs-lookup"><span data-stu-id="26bdf-140">az batch pool delete</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#delete) | <span data-ttu-id="26bdf-141">Belirtilen hello silme havuzu.</span><span class="sxs-lookup"><span data-stu-id="26bdf-141">Delete hello specified pool.</span></span>  |
| [<span data-ttu-id="26bdf-142">az batch havuzu otomatik ölçeklendirme etkinleştir</span><span class="sxs-lookup"><span data-stu-id="26bdf-142">az batch pool autoscale enable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | <span data-ttu-id="26bdf-143">Bir havuz üzerinde otomatik ölçeklendirmeyi etkinleştirmek ve bir formül uygulayın.</span><span class="sxs-lookup"><span data-stu-id="26bdf-143">Enable auto-scaling on a pool and apply a formula.</span></span>  |
| [<span data-ttu-id="26bdf-144">az batch havuzu otomatik ölçeklendirme devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="26bdf-144">az batch pool autoscale disable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | <span data-ttu-id="26bdf-145">Bir havuz üzerinde otomatik ölçeklendirme devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="26bdf-145">Disable auto-scaling on a pool.</span></span>  |
| [<span data-ttu-id="26bdf-146">az toplu işlem düğüm listesi</span><span class="sxs-lookup"><span data-stu-id="26bdf-146">az batch node list</span></span>](https://docs.microsoft.com/cli/azure/batch/node#list) | <span data-ttu-id="26bdf-147">Tüm liste hello hello işlem düğümünde belirtilen havuzu.</span><span class="sxs-lookup"><span data-stu-id="26bdf-147">List all hello compute node in hello specified pool.</span></span>  |
| [<span data-ttu-id="26bdf-148">az toplu düğümü yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="26bdf-148">az batch node reboot</span></span>](https://docs.microsoft.com/cli/azure/batch/node#reboot) | <span data-ttu-id="26bdf-149">Merhaba belirtilen işlem düğümü yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="26bdf-149">Reboot hello specified compute node.</span></span>  |
| [<span data-ttu-id="26bdf-150">az toplu düğümü Sil</span><span class="sxs-lookup"><span data-stu-id="26bdf-150">az batch node delete</span></span>](https://docs.microsoft.com/cli/azure/batch/node#delete) | <span data-ttu-id="26bdf-151">Delete listelenen hello hello düğümlerden havuzu belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="26bdf-151">Delete hello listed nodes from hello specified pool.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="26bdf-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="26bdf-152">Next steps</span></span>

<span data-ttu-id="26bdf-153">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="26bdf-153">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="26bdf-154">Ek toplu CLI kod örnekleri hello bulunabilir [Azure Batch CLI belgelerine](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="26bdf-154">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>

