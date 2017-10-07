---
title: "aaaAzure CLI komut dosyası örneği - toplu işleminde bir uygulama ekleyin | Microsoft Docs"
description: "Azure CLI toplu işleminde bir uygulama eklemek örnek - komut dosyası"
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
ms.openlocfilehash: cb33b3a7b30610011b19954a987995cc5f0257c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-applications-tooazure-batch-with-azure-cli"></a><span data-ttu-id="a2231-103">Uygulamaları tooAzure Azure CLI ile toplu ekleme</span><span class="sxs-lookup"><span data-stu-id="a2231-103">Adding applications tooAzure Batch with Azure CLI</span></span>

<span data-ttu-id="a2231-104">Bu komut dosyası gösterilmektedir nasıl tooset bir Azure Batch havuzu ya da görev ile kullanmak için bir uygulama ayarlama.</span><span class="sxs-lookup"><span data-stu-id="a2231-104">This script demonstrates how tooset up an application for use with an Azure Batch pool or task.</span></span> <span data-ttu-id="a2231-105">bir uygulama yukarı tooset paketini bir .zip dosyasına tüm bağımlılıkları ile birlikte, yürütülebilir.</span><span class="sxs-lookup"><span data-stu-id="a2231-105">tooset up an application, package your executable, together with any dependencies, into a .zip file.</span></span> <span data-ttu-id="a2231-106">İçinde bu örnek hello yürütülebilir zip dosyası olarak adlandırılır ' my-uygulama-exe.zip'.</span><span class="sxs-lookup"><span data-stu-id="a2231-106">In this example hello executable zip file is called 'my-application-exe.zip'.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2231-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a2231-107">Prerequisites</span></span>

- <span data-ttu-id="a2231-108">Yükleme hello hello sağlanan hello yönergeleri kullanarak Azure CLI [Azure CLI Yükleme Kılavuzu'na](https://docs.microsoft.com/cli/azure/install-azure-cli)zaten yapmadıysanız,.</span><span class="sxs-lookup"><span data-stu-id="a2231-108">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="a2231-109">Zaten yoksa, bir toplu işlem hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a2231-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="a2231-110">Bkz: [hello Azure CLI ile bir toplu işlem hesabı oluşturun](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) bir hesap oluşturan bir örnek komut dosyası için.</span><span class="sxs-lookup"><span data-stu-id="a2231-110">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>

## <a name="sample-script"></a><span data-ttu-id="a2231-111">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="a2231-111">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]

## <a name="clean-up-application"></a><span data-ttu-id="a2231-112">Uygulamayı oluşturan Temizle</span><span class="sxs-lookup"><span data-stu-id="a2231-112">Clean up application</span></span>

<span data-ttu-id="a2231-113">Örnek betik yukarıdaki hello çalıştırdıktan sonra aşağıdaki komutları tooremove hello uygulama ve onun karşıya yüklenen uygulama paketleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a2231-113">After you run hello above sample script, run hello following commands tooremove the application and all of its uploaded application packages.</span></span>

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a><span data-ttu-id="a2231-114">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="a2231-114">Script explanation</span></span>

<span data-ttu-id="a2231-115">Bu komut dosyası, bir uygulama ve bir uygulama paketini karşıya yükleme komutları toocreate aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="a2231-115">This script uses hello following commands toocreate an application and upload an application package.</span></span>
<span data-ttu-id="a2231-116">Her komut hello tablosundaki toocommand özgü belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="a2231-116">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="a2231-117">Komut</span><span class="sxs-lookup"><span data-stu-id="a2231-117">Command</span></span> | <span data-ttu-id="a2231-118">Notlar</span><span class="sxs-lookup"><span data-stu-id="a2231-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a2231-119">az batch uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="a2231-119">az batch application create</span></span>](https://docs.microsoft.com/cli/azure/batch/application#create) | <span data-ttu-id="a2231-120">Bir uygulama oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a2231-120">Creates an application.</span></span>  |
| [<span data-ttu-id="a2231-121">az toplu uygulama ayarlama</span><span class="sxs-lookup"><span data-stu-id="a2231-121">az batch application set</span></span>](https://docs.microsoft.com/cli/azure/batch/application#set) | <span data-ttu-id="a2231-122">Bir uygulamanın özelliklerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="a2231-122">Updates properties of an application.</span></span>  |
| [<span data-ttu-id="a2231-123">az toplu uygulama paketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="a2231-123">az batch application package create</span></span>](https://docs.microsoft.com/cli/azure/batch/application/package#create) | <span data-ttu-id="a2231-124">Belirtilen bir uygulama paketi toohello ekler uygulama.</span><span class="sxs-lookup"><span data-stu-id="a2231-124">Adds an application package toohello specified application.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="a2231-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a2231-125">Next steps</span></span>

<span data-ttu-id="a2231-126">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a2231-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a2231-127">Ek toplu CLI kod örnekleri hello bulunabilir [Azure Batch CLI belgelerine](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a2231-127">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
