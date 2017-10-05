---
title: "Dosya Paylaşımı için Azure DC/OS kümesi | Microsoft Docs"
description: "Oluşturma ve Azure kapsayıcı hizmeti DC/OS kümesinde bir dosya paylaşımını bağlama"
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
ms.openlocfilehash: 549b52bfb0a0268f754da26c6a374b267861f6d0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-and-mount-a-file-share-to-a-dcos-cluster"></a><span data-ttu-id="24249-104">Oluşturma ve DC/OS kümesi için bir dosya paylaşımını bağlama</span><span class="sxs-lookup"><span data-stu-id="24249-104">Create and mount a file share to a DC/OS cluster</span></span>
<span data-ttu-id="24249-105">Bu öğretici Azure'da bir dosya paylaşımı oluşturun ve her bir aracı ve DC/OS kümesi ana bağlamak nasıl ayrıntılarını verir.</span><span class="sxs-lookup"><span data-stu-id="24249-105">This tutorial details how to create a file share in Azure and mount it on each agent and master of the DC/OS cluster.</span></span> <span data-ttu-id="24249-106">Bir dosya paylaşımı ayarlama, küme yapılandırması, erişim, günlükler ve daha fazla gibi içinde dosya paylaşmak üzere kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="24249-106">Setting up a file share makes it easier to share files across your cluster such as configuration, access, logs, and more.</span></span> <span data-ttu-id="24249-107">Bu öğreticide aşağıdaki görevler tamamlanır:</span><span class="sxs-lookup"><span data-stu-id="24249-107">The following tasks are completed in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="24249-108">Azure Storage hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="24249-108">Create an Azure storage account</span></span>
> * <span data-ttu-id="24249-109">Dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="24249-109">Create a file share</span></span>
> * <span data-ttu-id="24249-110">DC/OS kümesinde paylaşımını bağlama</span><span class="sxs-lookup"><span data-stu-id="24249-110">Mount the share in the DC/OS cluster</span></span>

<span data-ttu-id="24249-111">Bu öğreticide adımları tamamlamak için bir ACS DC/OS kümesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="24249-111">You need an ACS DC/OS cluster to complete the steps in this tutorial.</span></span> <span data-ttu-id="24249-112">Gerekirse, [bu komut dosyası örneği](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) sizin için bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24249-112">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="24249-113">Bu öğretici, Azure CLI 2.0.4 veya sonraki bir sürümü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="24249-113">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="24249-114">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="24249-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="24249-115">Yükseltme gerekiyorsa, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="24249-115">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-a-file-share-on-microsoft-azure"></a><span data-ttu-id="24249-116">Microsoft Azure üzerinde bir dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="24249-116">Create a file share on Microsoft Azure</span></span>

<span data-ttu-id="24249-117">Bir ACS DC/OS kümesi ile Azure dosya paylaşımının kullanmadan önce depolama hesabı ve dosya paylaşımı oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="24249-117">Before using an Azure file share with an ACS DC/OS cluster, the storage account and file share must be created.</span></span> <span data-ttu-id="24249-118">Depolama ve dosya paylaşımı oluşturmak için aşağıdaki betiği çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="24249-118">Run the following script to create the storage and file share.</span></span> <span data-ttu-id="24249-119">Parametreler, ortamınızdan thoes ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="24249-119">Update the parameters with thoes from your environment.</span></span>

```azurecli-interactive
# Change these four parameters
DCOS_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
DCOS_PERS_RESOURCE_GROUP=myResourceGroup
DCOS_PERS_LOCATION=eastus
DCOS_PERS_SHARE_NAME=dcosshare

# Create the storage account with the parameters
az storage account create -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -l $DCOS_PERS_LOCATION --sku Standard_LRS

# Export the connection string as an environment variable, this is used when creating the Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -o tsv`

# Create the share
az storage share create -n $DCOS_PERS_SHARE_NAME
```

## <a name="mount-the-share-in-your-cluster"></a><span data-ttu-id="24249-120">Kümenizdeki paylaşımını bağlama</span><span class="sxs-lookup"><span data-stu-id="24249-120">Mount the share in your cluster</span></span>

<span data-ttu-id="24249-121">Ardından, dosya paylaşımı, küme içindeki her sanal makineye bağlı gerekir.</span><span class="sxs-lookup"><span data-stu-id="24249-121">Next, the file share needs to be mounted on every virtual machine inside your cluster.</span></span> <span data-ttu-id="24249-122">Bu görev CIFS aracı/protokolü kullanılarak tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="24249-122">This task is completed using the cifs tool/protocol.</span></span> <span data-ttu-id="24249-123">Bağlama işlemi, her bir düğümde kümenin veya kümedeki her düğümde karşı bir komut dosyası çalıştırarak el ile tamamlanabilir.</span><span class="sxs-lookup"><span data-stu-id="24249-123">The mount operation can be completed manually on each node of the cluster, or by running a script against each node in the cluster.</span></span>

<span data-ttu-id="24249-124">Bu örnekte, iki komut dosyaları çalıştırılır, bir Azure dosya paylaşımı ve DC/OS kümesi her düğümde bu komut dosyasını çalıştırmak için ikinci bir bağlama.</span><span class="sxs-lookup"><span data-stu-id="24249-124">In this example, two scripts are run, one to mount the Azure file share, and a second to run this script on each node of the DC/OS cluster.</span></span>

<span data-ttu-id="24249-125">İlk olarak, Azure depolama hesabı adı ve erişim anahtarı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="24249-125">First, the Azure storage account name, and access key are needed.</span></span> <span data-ttu-id="24249-126">Bu bilgileri almak için aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="24249-126">Run the following commands to get this information.</span></span> <span data-ttu-id="24249-127">Not her biri, bir sonraki adımda bu değerler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="24249-127">Take note of each, these values are used in a later step.</span></span>

<span data-ttu-id="24249-128">Depolama hesabı adı:</span><span class="sxs-lookup"><span data-stu-id="24249-128">Storage account name:</span></span>

```azurecli-interactive
STORAGE_ACCT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCT
```

<span data-ttu-id="24249-129">Depolama hesabının erişim anahtarı:</span><span class="sxs-lookup"><span data-stu-id="24249-129">Storage account access key:</span></span>

```azurecli-interactive
az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCT --query "[0].value" -o tsv
```

<span data-ttu-id="24249-130">Ardından, DC/OS asıl FQDN'sini almak ve bir değişkende saklayın.</span><span class="sxs-lookup"><span data-stu-id="24249-130">Next, get the FQDN of the DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="24249-131">Özel anahtarınızı ana düğüme kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="24249-131">Copy your private key to the master node.</span></span> <span data-ttu-id="24249-132">Bu anahtar oluşturmak için gereken bir ssh bağlantısı kümedeki tüm düğümlerle.</span><span class="sxs-lookup"><span data-stu-id="24249-132">This key is needed to create an ssh connection with all nodes in the cluster.</span></span> <span data-ttu-id="24249-133">Varsayılan olmayan bir değer kümesi oluştururken kullanılan kullanıcı adını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="24249-133">Update the user name if a non-default value was used when creating the cluster.</span></span> 

```azurecli-interactive
scp ~/.ssh/id_rsa azureuser@$FQDN:~/.ssh
```

<span data-ttu-id="24249-134">Bir SSH bağlantısı asıl (veya ilk ana) DC/OS tabanlı kümenizin ile oluşturun.</span><span class="sxs-lookup"><span data-stu-id="24249-134">Create an SSH connection with the master (or the first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="24249-135">Varsayılan olmayan bir değer kümesi oluştururken kullanılan kullanıcı adını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="24249-135">Update the user name if a non-default value was used when creating the cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="24249-136">Adlı bir dosya oluşturun **cifsMount.sh**ve aşağıdaki içeriği buraya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="24249-136">Create a file named **cifsMount.sh**, and copy the following contents into it.</span></span> 

<span data-ttu-id="24249-137">Bu komut dosyası ve Azure dosya paylaşımı bağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="24249-137">This script is used to mount the Azure file share.</span></span> <span data-ttu-id="24249-138">Güncelleştirme `STORAGE_ACCT_NAME` ve `ACCESS_KEY` bilgileri değişkenlerle toplanan daha önce.</span><span class="sxs-lookup"><span data-stu-id="24249-138">Update the `STORAGE_ACCT_NAME` and `ACCESS_KEY` variables with the information collected earlier.</span></span>

```azurecli-interactive
#!/bin/bash

# Azure storage account name and access key
STORAGE_ACCT_NAME=mystorageaccount
ACCESS_KEY=mystorageaccountKey

# Install the cifs utils, should be already installed
sudo apt-get update && sudo apt-get -y install cifs-utils

# Create the local folder that will contain our share
if [ ! -d "/mnt/share/dcosshare" ]; then sudo mkdir -p "/mnt/share/dcosshare" ; fi

# Mount the share under the previous local folder created
sudo mount -t cifs //$STORAGE_ACCT_NAME.file.core.windows.net/dcosshare /mnt/share/dcosshare -o vers=3.0,username=$STORAGE_ACCT_NAME,password=$ACCESS_KEY,dir_mode=0777,file_mode=0777
```
<span data-ttu-id="24249-139">Adlı ikinci bir dosya oluşturun **getNodesRunScript.sh** ve aşağıdaki içeriği dosyaya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="24249-139">Create a second file named **getNodesRunScript.sh** and copy the following contents into the file.</span></span> 

<span data-ttu-id="24249-140">Bu komut tüm küme düğümlerine bulur ve ardından çalıştırır **cifsMount.sh** her dosya paylaşımını bağlama için komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="24249-140">This script discovers all cluster nodes, and then runs the **cifsMount.sh** script to mount the file share on each.</span></span>

```azurecli-interactive
#!/bin/bash

# Install jq used for the next command
sudo apt-get install jq -y

# Get the IP address of each node using the mesos API and store it inside a file called nodes
curl http://leader.mesos:1050/system/health/v1/nodes | jq '.nodes[].host_ip' | sed 's/\"//g' | sed '/172/d' > nodes

# From the previous file created, run our script to mount our share on each node
cat nodes | while read line
do
  ssh `whoami`@$line -o StrictHostKeyChecking=no < ./cifsMount.sh
  done
```

<span data-ttu-id="24249-141">Azure dosya paylaşımı kümenin tüm düğümlerinde bağlamak için komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="24249-141">Run the script to mount the Azure file share on all nodes of the cluster.</span></span>

```azurecli-interactive
sh ./getNodesRunScript.sh
```  

<span data-ttu-id="24249-142">Dosya Paylaşımı artık adresindeki erişilebilen `/mnt/share/dcosshare` kümedeki her düğümde.</span><span class="sxs-lookup"><span data-stu-id="24249-142">The file share is now accessible at `/mnt/share/dcosshare` on each node of the cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24249-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="24249-143">Next steps</span></span>

<span data-ttu-id="24249-144">Bu öğreticide Azure dosya paylaşımı adımları kullanarak bir DC/OS kümesi sunulmuştur:</span><span class="sxs-lookup"><span data-stu-id="24249-144">In this tutorial an Azure file share was made available to a DC/OS cluster using the steps:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="24249-145">Azure Storage hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="24249-145">Create an Azure storage account</span></span>
> * <span data-ttu-id="24249-146">Dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="24249-146">Create a file share</span></span>
> * <span data-ttu-id="24249-147">DC/OS kümesinde paylaşımını bağlama</span><span class="sxs-lookup"><span data-stu-id="24249-147">Mount the share in the DC/OS cluster</span></span>

<span data-ttu-id="24249-148">Azure kapsayıcı kayıt defteri DC/OS Azure ile tümleştirme hakkında bilgi edinmek için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="24249-148">Advance to the next tutorial to learn about integrating an Azure Container Registry with DC/OS in Azure.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="24249-149">Uygulamalarda yük dengeleme gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="24249-149">Load balance applications</span></span>](container-service-dcos-acr.md)