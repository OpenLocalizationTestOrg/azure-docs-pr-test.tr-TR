---
title: "Azure DC/OS kümesi için aaaFile paylaşım | Microsoft Docs"
description: "Oluşturma ve bir dosya paylaşımı tooa DC/OS kümesi Azure kapsayıcı Hizmeti'nde bağlama"
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service
keywords: "Docker, kapsayıcıları, mikro hizmetler, Mesos, Azure, dosya paylaşımı, CIFS"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: d18090d414a3e00202ccde442ac9b865d74f1e34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-mount-a-file-share-tooa-dcos-cluster"></a><span data-ttu-id="5e00e-104">Oluşturma ve bir dosya paylaşımı tooa DC/OS kümesi bağlama</span><span class="sxs-lookup"><span data-stu-id="5e00e-104">Create and mount a file share tooa DC/OS cluster</span></span>
<span data-ttu-id="5e00e-105">Bu öğretici, nasıl bir dosya Azure'da paylaşma ve her bir aracı ve ana bağlama toocreate hello DC/OS kümesi ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="5e00e-105">This tutorial details how toocreate a file share in Azure and mount it on each agent and master of hello DC/OS cluster.</span></span> <span data-ttu-id="5e00e-106">Bir dosya paylaşımı ayarını daha kolay tooshare dosyaları, küme yapılandırması, erişim, günlükler ve daha fazla gibi içinde kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="5e00e-106">Setting up a file share makes it easier tooshare files across your cluster such as configuration, access, logs, and more.</span></span> <span data-ttu-id="5e00e-107">Bu öğreticide görevleri aşağıdaki hello tamamlanır:</span><span class="sxs-lookup"><span data-stu-id="5e00e-107">hello following tasks are completed in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5e00e-108">Azure Storage hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5e00e-108">Create an Azure storage account</span></span>
> * <span data-ttu-id="5e00e-109">Dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5e00e-109">Create a file share</span></span>
> * <span data-ttu-id="5e00e-110">Merhaba DC/OS kümesinde Hello paylaşımını bağlama</span><span class="sxs-lookup"><span data-stu-id="5e00e-110">Mount hello share in hello DC/OS cluster</span></span>

<span data-ttu-id="5e00e-111">Bir ACS DC/küme toocomplete hello bu öğreticideki adımlar işletim sistemi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5e00e-111">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="5e00e-112">Gerekirse, [bu komut dosyası örneği](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) sizin için bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5e00e-112">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="5e00e-113">Bu öğretici hello Azure CLI Sürüm 2.0.4 gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="5e00e-113">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="5e00e-114">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="5e00e-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="5e00e-115">Tooupgrade gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5e00e-115">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-a-file-share-on-microsoft-azure"></a><span data-ttu-id="5e00e-116">Microsoft Azure üzerinde bir dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5e00e-116">Create a file share on Microsoft Azure</span></span>

<span data-ttu-id="5e00e-117">Bir ACS DC/OS kümesi ile Azure dosya paylaşımının kullanmadan önce hello depolama hesabı ve dosya paylaşımı oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5e00e-117">Before using an Azure file share with an ACS DC/OS cluster, hello storage account and file share must be created.</span></span> <span data-ttu-id="5e00e-118">Komut dosyası, toocreate hello depolama ve dosya paylaşımını aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5e00e-118">Run hello following script toocreate hello storage and file share.</span></span> <span data-ttu-id="5e00e-119">Thoes, ortamınızdan ile Merhaba parametreleri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="5e00e-119">Update hello parameters with thoes from your environment.</span></span>

```azurecli-interactive
# Change these four parameters
DCOS_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
DCOS_PERS_RESOURCE_GROUP=myResourceGroup
DCOS_PERS_LOCATION=eastus
DCOS_PERS_SHARE_NAME=dcosshare

# Create hello storage account with hello parameters
az storage account create -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -l $DCOS_PERS_LOCATION --sku Standard_LRS

# Export hello connection string as an environment variable, this is used when creating hello Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -o tsv`

# Create hello share
az storage share create -n $DCOS_PERS_SHARE_NAME
```

## <a name="mount-hello-share-in-your-cluster"></a><span data-ttu-id="5e00e-120">Kümenizdeki Hello paylaşımını bağlama</span><span class="sxs-lookup"><span data-stu-id="5e00e-120">Mount hello share in your cluster</span></span>

<span data-ttu-id="5e00e-121">Ardından, dosya paylaşımı gereksinimlerini toobe, küme içindeki her sanal makineye bağlı hello.</span><span class="sxs-lookup"><span data-stu-id="5e00e-121">Next, hello file share needs toobe mounted on every virtual machine inside your cluster.</span></span> <span data-ttu-id="5e00e-122">Bu görev hello CIFS aracı/protokolü kullanılarak tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="5e00e-122">This task is completed using hello cifs tool/protocol.</span></span> <span data-ttu-id="5e00e-123">Merhaba bağlama işlemi, her bir düğümde hello kümenin veya hello kümedeki her düğümde karşı bir komut dosyası çalıştırarak el ile tamamlanabilir.</span><span class="sxs-lookup"><span data-stu-id="5e00e-123">hello mount operation can be completed manually on each node of hello cluster, or by running a script against each node in hello cluster.</span></span>

<span data-ttu-id="5e00e-124">Bu örnekte, iki komut dosyaları çalıştırılır, bir toomount hello Azure hello DC/OS kümesi her düğümde paylaşım ve ikinci toorun bu komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="5e00e-124">In this example, two scripts are run, one toomount hello Azure file share, and a second toorun this script on each node of hello DC/OS cluster.</span></span>

<span data-ttu-id="5e00e-125">İlk olarak, hello Azure depolama hesabı adı ve erişim anahtarı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="5e00e-125">First, hello Azure storage account name, and access key are needed.</span></span> <span data-ttu-id="5e00e-126">Bu bilgiler aşağıdaki komutları tooget hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5e00e-126">Run hello following commands tooget this information.</span></span> <span data-ttu-id="5e00e-127">Not her biri, bir sonraki adımda bu değerler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5e00e-127">Take note of each, these values are used in a later step.</span></span>

<span data-ttu-id="5e00e-128">Depolama hesabı adı:</span><span class="sxs-lookup"><span data-stu-id="5e00e-128">Storage account name:</span></span>

```azurecli-interactive
STORAGE_ACCT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCT
```

<span data-ttu-id="5e00e-129">Depolama hesabının erişim anahtarı:</span><span class="sxs-lookup"><span data-stu-id="5e00e-129">Storage account access key:</span></span>

```azurecli-interactive
az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCT --query "[0].value" -o tsv
```

<span data-ttu-id="5e00e-130">Ardından, hello DC/OS ana ve bir değişkende saklayın hello FQDN'sini alın.</span><span class="sxs-lookup"><span data-stu-id="5e00e-130">Next, get hello FQDN of hello DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="5e00e-131">Özel anahtar toohello ana düğümünüz kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="5e00e-131">Copy your private key toohello master node.</span></span> <span data-ttu-id="5e00e-132">Bu anahtar gerekli toocreate olan bir ssh bağlantısı hello kümedeki tüm düğümlerle birlikte.</span><span class="sxs-lookup"><span data-stu-id="5e00e-132">This key is needed toocreate an ssh connection with all nodes in hello cluster.</span></span> <span data-ttu-id="5e00e-133">Varsayılan olmayan bir değer hello kümesi oluştururken kullanıldıysa hello kullanıcı adını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="5e00e-133">Update hello user name if a non-default value was used when creating hello cluster.</span></span> 

```azurecli-interactive
scp ~/.ssh/id_rsa azureuser@$FQDN:~/.ssh
```

<span data-ttu-id="5e00e-134">Bir SSH bağlantısı hello Yöneticisi (ya da hello ilk ana) DC/OS tabanlı kümenizin oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5e00e-134">Create an SSH connection with hello master (or hello first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="5e00e-135">Varsayılan olmayan bir değer hello kümesi oluştururken kullanıldıysa hello kullanıcı adını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="5e00e-135">Update hello user name if a non-default value was used when creating hello cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="5e00e-136">Adlı bir dosya oluşturun **cifsMount.sh**, kopya hello izleyerek içeriği içine.</span><span class="sxs-lookup"><span data-stu-id="5e00e-136">Create a file named **cifsMount.sh**, and copy hello following contents into it.</span></span> 

<span data-ttu-id="5e00e-137">Bu komut dosyası kullanılan toomount hello Azure dosya paylaşımıdır.</span><span class="sxs-lookup"><span data-stu-id="5e00e-137">This script is used toomount hello Azure file share.</span></span> <span data-ttu-id="5e00e-138">Güncelleştirme hello `STORAGE_ACCT_NAME` ve `ACCESS_KEY` hello bilgi değişkenlerle toplanan daha önce.</span><span class="sxs-lookup"><span data-stu-id="5e00e-138">Update hello `STORAGE_ACCT_NAME` and `ACCESS_KEY` variables with hello information collected earlier.</span></span>

```azurecli-interactive
#!/bin/bash

# Azure storage account name and access key
STORAGE_ACCT_NAME=mystorageaccount
ACCESS_KEY=mystorageaccountKey

# Install hello cifs utils, should be already installed
sudo apt-get update && sudo apt-get -y install cifs-utils

# Create hello local folder that will contain our share
if [ ! -d "/mnt/share/dcosshare" ]; then sudo mkdir -p "/mnt/share/dcosshare" ; fi

# Mount hello share under hello previous local folder created
sudo mount -t cifs //$STORAGE_ACCT_NAME.file.core.windows.net/dcosshare /mnt/share/dcosshare -o vers=3.0,username=$STORAGE_ACCT_NAME,password=$ACCESS_KEY,dir_mode=0777,file_mode=0777
```
<span data-ttu-id="5e00e-139">Adlı ikinci bir dosya oluşturun **getNodesRunScript.sh** ve hello dosyasına kopyalama hello aşağıdaki içeriği.</span><span class="sxs-lookup"><span data-stu-id="5e00e-139">Create a second file named **getNodesRunScript.sh** and copy hello following contents into hello file.</span></span> 

<span data-ttu-id="5e00e-140">Bu komut tüm küme düğümlerine bulur ve hello çalıştırır **cifsMount.sh** her komut dosyası toomount hello dosya paylaşımı.</span><span class="sxs-lookup"><span data-stu-id="5e00e-140">This script discovers all cluster nodes, and then runs hello **cifsMount.sh** script toomount hello file share on each.</span></span>

```azurecli-interactive
#!/bin/bash

# Install jq used for hello next command
sudo apt-get install jq -y

# Get hello IP address of each node using hello mesos API and store it inside a file called nodes
curl http://leader.mesos:1050/system/health/v1/nodes | jq '.nodes[].host_ip' | sed 's/\"//g' | sed '/172/d' > nodes

# From hello previous file created, run our script toomount our share on each node
cat nodes | while read line
do
  ssh `whoami`@$line -o StrictHostKeyChecking=no < ./cifsMount.sh
  done
```

<span data-ttu-id="5e00e-141">Merhaba betik toomount hello Azure dosya paylaşımı hello kümenin tüm düğümlerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5e00e-141">Run hello script toomount hello Azure file share on all nodes of hello cluster.</span></span>

```azurecli-interactive
sh ./getNodesRunScript.sh
```  

<span data-ttu-id="5e00e-142">Merhaba dosya paylaşımı artık adresindeki erişilebilen `/mnt/share/dcosshare` hello kümenin her bir düğümde.</span><span class="sxs-lookup"><span data-stu-id="5e00e-142">hello file share is now accessible at `/mnt/share/dcosshare` on each node of hello cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e00e-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5e00e-143">Next steps</span></span>

<span data-ttu-id="5e00e-144">Bu öğreticide Azure dosya paylaşımı hello adımları kullanarak yapılan kullanılabilir tooa DC/OS kümesi oluştu:</span><span class="sxs-lookup"><span data-stu-id="5e00e-144">In this tutorial an Azure file share was made available tooa DC/OS cluster using hello steps:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5e00e-145">Azure Storage hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5e00e-145">Create an Azure storage account</span></span>
> * <span data-ttu-id="5e00e-146">Dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5e00e-146">Create a file share</span></span>
> * <span data-ttu-id="5e00e-147">Merhaba DC/OS kümesinde Hello paylaşımını bağlama</span><span class="sxs-lookup"><span data-stu-id="5e00e-147">Mount hello share in hello DC/OS cluster</span></span>

<span data-ttu-id="5e00e-148">Azure kapsayıcı kayıt defteri DC/OS Azure ile tümleştirme hakkında toohello sonraki öğretici toolearn ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="5e00e-148">Advance toohello next tutorial toolearn about integrating an Azure Container Registry with DC/OS in Azure.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="5e00e-149">Uygulamalarda yük dengeleme gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="5e00e-149">Load balance applications</span></span>](container-service-dcos-acr.md)