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
# <a name="create-and-mount-a-file-share-tooa-dcos-cluster"></a>Oluşturma ve bir dosya paylaşımı tooa DC/OS kümesi bağlama
Bu öğretici, nasıl bir dosya Azure'da paylaşma ve her bir aracı ve ana bağlama toocreate hello DC/OS kümesi ayrıntıları. Bir dosya paylaşımı ayarını daha kolay tooshare dosyaları, küme yapılandırması, erişim, günlükler ve daha fazla gibi içinde kolaylaştırır. Bu öğreticide görevleri aşağıdaki hello tamamlanır:

> [!div class="checklist"]
> * Azure Storage hesabı oluşturma
> * Dosya paylaşımı oluşturma
> * Merhaba DC/OS kümesinde Hello paylaşımını bağlama

Bir ACS DC/küme toocomplete hello bu öğreticideki adımlar işletim sistemi gerekir. Gerekirse, [bu komut dosyası örneği](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) sizin için bir tane oluşturabilirsiniz.

Bu öğretici hello Azure CLI Sürüm 2.0.4 gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooupgrade gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-a-file-share-on-microsoft-azure"></a>Microsoft Azure üzerinde bir dosya paylaşımı oluşturma

Bir ACS DC/OS kümesi ile Azure dosya paylaşımının kullanmadan önce hello depolama hesabı ve dosya paylaşımı oluşturulması gerekir. Komut dosyası, toocreate hello depolama ve dosya paylaşımını aşağıdaki hello çalıştırın. Thoes, ortamınızdan ile Merhaba parametreleri güncelleştirin.

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

## <a name="mount-hello-share-in-your-cluster"></a>Kümenizdeki Hello paylaşımını bağlama

Ardından, dosya paylaşımı gereksinimlerini toobe, küme içindeki her sanal makineye bağlı hello. Bu görev hello CIFS aracı/protokolü kullanılarak tamamlanır. Merhaba bağlama işlemi, her bir düğümde hello kümenin veya hello kümedeki her düğümde karşı bir komut dosyası çalıştırarak el ile tamamlanabilir.

Bu örnekte, iki komut dosyaları çalıştırılır, bir toomount hello Azure hello DC/OS kümesi her düğümde paylaşım ve ikinci toorun bu komut dosyası.

İlk olarak, hello Azure depolama hesabı adı ve erişim anahtarı gereklidir. Bu bilgiler aşağıdaki komutları tooget hello çalıştırın. Not her biri, bir sonraki adımda bu değerler kullanılır.

Depolama hesabı adı:

```azurecli-interactive
STORAGE_ACCT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCT
```

Depolama hesabının erişim anahtarı:

```azurecli-interactive
az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCT --query "[0].value" -o tsv
```

Ardından, hello DC/OS ana ve bir değişkende saklayın hello FQDN'sini alın.

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

Özel anahtar toohello ana düğümünüz kopyalayın. Bu anahtar gerekli toocreate olan bir ssh bağlantısı hello kümedeki tüm düğümlerle birlikte. Varsayılan olmayan bir değer hello kümesi oluştururken kullanıldıysa hello kullanıcı adını güncelleştirin. 

```azurecli-interactive
scp ~/.ssh/id_rsa azureuser@$FQDN:~/.ssh
```

Bir SSH bağlantısı hello Yöneticisi (ya da hello ilk ana) DC/OS tabanlı kümenizin oluşturun. Varsayılan olmayan bir değer hello kümesi oluştururken kullanıldıysa hello kullanıcı adını güncelleştirin.

```azurecli-interactive
ssh azureuser@$FQDN
```

Adlı bir dosya oluşturun **cifsMount.sh**, kopya hello izleyerek içeriği içine. 

Bu komut dosyası kullanılan toomount hello Azure dosya paylaşımıdır. Güncelleştirme hello `STORAGE_ACCT_NAME` ve `ACCESS_KEY` hello bilgi değişkenlerle toplanan daha önce.

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
Adlı ikinci bir dosya oluşturun **getNodesRunScript.sh** ve hello dosyasına kopyalama hello aşağıdaki içeriği. 

Bu komut tüm küme düğümlerine bulur ve hello çalıştırır **cifsMount.sh** her komut dosyası toomount hello dosya paylaşımı.

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

Merhaba betik toomount hello Azure dosya paylaşımı hello kümenin tüm düğümlerinde çalıştırın.

```azurecli-interactive
sh ./getNodesRunScript.sh
```  

Merhaba dosya paylaşımı artık adresindeki erişilebilen `/mnt/share/dcosshare` hello kümenin her bir düğümde.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide Azure dosya paylaşımı hello adımları kullanarak yapılan kullanılabilir tooa DC/OS kümesi oluştu:

> [!div class="checklist"]
> * Azure Storage hesabı oluşturma
> * Dosya paylaşımı oluşturma
> * Merhaba DC/OS kümesinde Hello paylaşımını bağlama

Azure kapsayıcı kayıt defteri DC/OS Azure ile tümleştirme hakkında toohello sonraki öğretici toolearn ilerleyin.  

> [!div class="nextstepaction"]
> [Uygulamalarda yük dengeleme gerçekleştirme](container-service-dcos-acr.md)