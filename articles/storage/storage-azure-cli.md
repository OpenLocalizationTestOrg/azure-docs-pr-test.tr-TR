---
title: aaaUsing hello Azure Storage ile Azure CLI 2.0 | Microsoft Docs
description: "Nasıl toouse Azure komut satırı arabirimi (Azure CLI) 2.0 ile Azure depolama toocreate hello ve depolama hesaplarını yönetme ve Azure BLOB'ları ve dosyalar ile çalışırken öğrenin. Hello Azure CLI 2.0 Python içinde yazılmış platformlar arası bir araçtır."
services: storage
documentationcenter: na
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 06/02/2017
ms.author: marsma
ms.openlocfilehash: 38402373dcd87f1ef05471a02353c77d58f1a9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-20-with-azure-storage"></a><span data-ttu-id="755c4-104">Hello Azure CLI 2.0 Azure Storage ile kullanma</span><span class="sxs-lookup"><span data-stu-id="755c4-104">Using hello Azure CLI 2.0 with Azure Storage</span></span>

<span data-ttu-id="755c4-105">Merhaba açık kaynak, platformlar arası Azure CLI 2.0 hello Azure platformu ile çalışmak için bir komut kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="755c4-105">hello open-source, cross-platform Azure CLI 2.0 provides a set of commands for working with hello Azure platform.</span></span> <span data-ttu-id="755c4-106">Aynı işlevselliği bulunan hello hello çoğunu sağlayan [Azure portal](https://portal.azure.com), zengin veri erişimi de dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="755c4-106">It provides much of hello same functionality found in hello [Azure portal](https://portal.azure.com), including rich data access.</span></span>

<span data-ttu-id="755c4-107">Bu kılavuzda, nasıl gösteriyoruz toouse hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform çeşitli görevleri Azure depolama hesabınızdaki kaynaklara ile çalışma.</span><span class="sxs-lookup"><span data-stu-id="755c4-107">In this guide, we show you how toouse hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform several tasks working with resources in your Azure Storage account.</span></span> <span data-ttu-id="755c4-108">İndirin ve yükleyin veya bu kılavuzu kullanmadan önce hello CLI 2.0 toohello en son sürümüne yükseltmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="755c4-108">We recommend that you download and install or upgrade toohello latest version of hello CLI 2.0 before using this guide.</span></span>

<span data-ttu-id="755c4-109">Başlangıç Kılavuzu'nda Hello örnekler hello Bash kabuğunda Ubuntu üzerinde hello kullanımını varsayar ancak diğer platformlar benzer şekilde gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="755c4-109">hello examples in hello guide assume hello use of hello Bash shell on Ubuntu, but other platforms should perform similarly.</span></span> 

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a><span data-ttu-id="755c4-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="755c4-110">Prerequisites</span></span>
<span data-ttu-id="755c4-111">Bu kılavuz, Azure Storage hello temel kavramlarını anladığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="755c4-111">This guide assumes that you understand hello basic concepts of Azure Storage.</span></span> <span data-ttu-id="755c4-112">Aşağıda Azure ve hello depolama hizmeti için belirtilen mümkün toosatisfy hello hesap oluşturma gerekliliklerini olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="755c4-112">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Storage service.</span></span>

### <a name="accounts"></a><span data-ttu-id="755c4-113">Hesaplar</span><span class="sxs-lookup"><span data-stu-id="755c4-113">Accounts</span></span>
* <span data-ttu-id="755c4-114">**Azure hesabı**: zaten bir Azure aboneliğiniz yoksa [ücretsiz bir Azure hesabı oluşturma](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="755c4-114">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="755c4-115">**Storage hesabı**: Bkz. [Azure Storage hesapları hakkında](../storage/storage-create-storage-account.md) sayfası, [Storage hesabı oluşturma](../storage/storage-create-storage-account.md#create-a-storage-account) bölümü.</span><span class="sxs-lookup"><span data-stu-id="755c4-115">**Storage account**: See [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/storage-create-storage-account.md).</span></span>

### <a name="install-hello-azure-cli-20"></a><span data-ttu-id="755c4-116">Hello Azure CLI 2.0 yükleyin</span><span class="sxs-lookup"><span data-stu-id="755c4-116">Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="755c4-117">Karşıdan yükleyip hello Azure CLI 2.0 özetlenen hello yönergeleri izleyerek [Azure CLI 2.0 yükleme](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="755c4-117">Download and install hello Azure CLI 2.0 by following hello instructions outlined in [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

> [!TIP]
> <span data-ttu-id="755c4-118">Merhaba yüklemesiyle konusunda sorun yaşıyorsanız, hello denetleyin [yükleme sorunlarını giderme](/cli/azure/install-az-cli2#installation-troubleshooting) hello makale ve hello bölümünü [yükleme sorun giderme](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) github'da Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="755c4-118">If you have trouble with hello installation, check out hello [Installation Troubleshooting](/cli/azure/install-az-cli2#installation-troubleshooting) section of hello article, and hello [Install Troubleshooting](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guide on GitHub.</span></span>
>

## <a name="working-with-hello-cli"></a><span data-ttu-id="755c4-119">CLI Hello ile çalışma</span><span class="sxs-lookup"><span data-stu-id="755c4-119">Working with hello CLI</span></span>

<span data-ttu-id="755c4-120">Hello CLI yükledikten sonra hello kullanarak `az` , komut satırı arabirimi (Bash, Terminal, komut istemi) tooaccess hello Azure CLI komutlarda komutu.</span><span class="sxs-lookup"><span data-stu-id="755c4-120">Once you've installed hello CLI, you can use hello `az` command in your command-line interface (Bash, Terminal, Command Prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="755c4-121">Türü hello `az` komutu toosee hello temel komutları (örnek çıktı aşağıdaki hello kesildi) tam listesi:</span><span class="sxs-lookup"><span data-stu-id="755c4-121">Type hello `az` command toosee a full list of hello base commands (hello following example output has been truncated):</span></span>

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome toohello cool new Azure CLI!

Here are hello base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

<span data-ttu-id="755c4-122">Komut satırı arabirimi hello bağlamını `az storage --help` toolist hello `storage` alt grupları komutu.</span><span class="sxs-lookup"><span data-stu-id="755c4-122">In your command-line interface, execute hello command `az storage --help` toolist hello `storage` command subgroups.</span></span> <span data-ttu-id="755c4-123">Merhaba alt grupları Hello açıklamalarını depolama kaynaklarla çalışmak için Azure CLI sağlar hello işlevselliği hello genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="755c4-123">hello descriptions of hello subgroups provide an overview of hello functionality hello Azure CLI provides for working with your storage resources.</span></span>

```
Group
    az storage: Durable, highly available, and massively scalable cloud storage.

Subgroups:
    account  : Manage storage accounts.
    blob     : Object storage for unstructured data.
    container: Manage blob storage containers.
    cors     : Manage Storage service Cross-Origin Resource Sharing (CORS).
    directory: Manage file storage directories.
    entity   : Manage table storage entities.
    file     : File shares that use hello standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues tooeffectively scale applications according tootraffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-hello-cli-tooyour-azure-subscription"></a><span data-ttu-id="755c4-124">Merhaba CLI tooyour Azure aboneliğine bağlanma</span><span class="sxs-lookup"><span data-stu-id="755c4-124">Connect hello CLI tooyour Azure subscription</span></span>

<span data-ttu-id="755c4-125">toowork hello kaynaklarla, Azure aboneliğinizin ilk oturum açmalısınız tooyour içinde Azure hesabı `az login`.</span><span class="sxs-lookup"><span data-stu-id="755c4-125">toowork with hello resources in your Azure subscription, you must first log in tooyour Azure account with `az login`.</span></span> <span data-ttu-id="755c4-126">Oturum açabilir birkaç yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="755c4-126">There are several ways you can log in:</span></span>

* <span data-ttu-id="755c4-127">**Etkileşimli oturum açma**:`az login`</span><span class="sxs-lookup"><span data-stu-id="755c4-127">**Interactive login**: `az login`</span></span>
* <span data-ttu-id="755c4-128">**Kullanıcı adı ve parolayla oturum**:`az login -u johndoe@contoso.com -p VerySecret`</span><span class="sxs-lookup"><span data-stu-id="755c4-128">**Log in with user name and password**: `az login -u johndoe@contoso.com -p VerySecret`</span></span>
  * <span data-ttu-id="755c4-129">Bu, Microsoft hesapları veya çok faktörlü kimlik doğrulamasını kullanan ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="755c4-129">This doesn't work with Microsoft accounts or accounts that use multi-factor authentication.</span></span>
* <span data-ttu-id="755c4-130">**Bir hizmet sorumlusu oturum oturum**:`az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="755c4-130">**Log in with a service principal**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span></span>

## <a name="azure-cli-20-sample-script"></a><span data-ttu-id="755c4-131">Azure CLI 2.0 örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="755c4-131">Azure CLI 2.0 sample script</span></span>

<span data-ttu-id="755c4-132">Ardından, biz ile Azure Storage kaynaklarını birkaç temel Azure CLI 2.0 komutları toointeract sorunları küçük Kabuk betiği çalışmak.</span><span class="sxs-lookup"><span data-stu-id="755c4-132">Next, we'll work with a small shell script that issues a few basic Azure CLI 2.0 commands toointeract with Azure Storage resources.</span></span> <span data-ttu-id="755c4-133">Merhaba komut dosyası ilk depolama hesabınızı yeni bir kapsayıcı oluşturur ve sonra var olan bir dosya (blob) olarak toothat kapsayıcı yükler.</span><span class="sxs-lookup"><span data-stu-id="755c4-133">hello script first creates a new container in your storage account, then uploads an existing file (as a blob) toothat container.</span></span> <span data-ttu-id="755c4-134">Merhaba kapsayıcıdaki tüm blob'lara listeler ve son olarak, yerel bilgisayarınızda belirttiğiniz hello dosya tooa hedef indirir.</span><span class="sxs-lookup"><span data-stu-id="755c4-134">It then lists all blobs in hello container, and finally, downloads hello file tooa destination on your local computer that you specify.</span></span>

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating hello container..."
az storage container create --name $container_name

echo "Uploading hello file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing hello blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading hello file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

<span data-ttu-id="755c4-135">**Yapılandırma ve hello komut dosyası çalıştırma**</span><span class="sxs-lookup"><span data-stu-id="755c4-135">**Configure and run hello script**</span></span>

1. <span data-ttu-id="755c4-136">Sık kullandığınız metin düzenleyicisinde açın, sonra kopyalayın ve komut dosyası hello düzenleyicisine önceki hello yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="755c4-136">Open your favorite text editor, then copy and paste hello preceding script into hello editor.</span></span>

2. <span data-ttu-id="755c4-137">Ardından, hello komut dosyanızın değişken tooreflect yapılandırma ayarlarınızı güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="755c4-137">Next, update hello script's variables tooreflect your configuration settings.</span></span> <span data-ttu-id="755c4-138">Belirtilen değerler aşağıdaki hello değiştirin:</span><span class="sxs-lookup"><span data-stu-id="755c4-138">Replace hello following values as specified:</span></span>

   * <span data-ttu-id="755c4-139">**\<storage_account_name\>**  hello depolama hesabınızın adını.</span><span class="sxs-lookup"><span data-stu-id="755c4-139">**\<storage_account_name\>** hello name of your storage account.</span></span>
   * <span data-ttu-id="755c4-140">**\<storage_account_key\>**  hello birincil veya ikincil erişim anahtarını depolama hesabınız için.</span><span class="sxs-lookup"><span data-stu-id="755c4-140">**\<storage_account_key\>** hello primary or secondary access key for your storage account.</span></span>
   * <span data-ttu-id="755c4-141">**\<container_name\>**  bir ad hello "azure-CLI-örnek-container" gibi yeni kapsayıcı toocreate.</span><span class="sxs-lookup"><span data-stu-id="755c4-141">**\<container_name\>** A name hello new container toocreate, such as "azure-cli-sample-container".</span></span>
   * <span data-ttu-id="755c4-142">**\<blob_name\>**  hello kapsayıcısında hello hedef blob için bir ad.</span><span class="sxs-lookup"><span data-stu-id="755c4-142">**\<blob_name\>** A name for hello destination blob in hello container.</span></span>
   * <span data-ttu-id="755c4-143">**\<file_to_upload\>**  yol toosmall dosyası yerel bilgisayarınızda gibi hello "~ / images/HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="755c4-143">**\<file_to_upload\>** hello path toosmall file on your local computer, such as "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="755c4-144">**\<destination_file\>**  hedef dosya yolu gibi hello "~ / downloadedImage.png".</span><span class="sxs-lookup"><span data-stu-id="755c4-144">**\<destination_file\>** hello destination file path, such as "~/downloadedImage.png".</span></span>

3. <span data-ttu-id="755c4-145">Merhaba gerekli değişkenleri güncelleştirdikten sonra hello komut dosyasını kaydedin ve düzenleyicinizi çıkın.</span><span class="sxs-lookup"><span data-stu-id="755c4-145">After you've updated hello necessary variables, save hello script and exit your editor.</span></span> <span data-ttu-id="755c4-146">Merhaba sonraki adımlar varsayın kodunuzu adlı **my_storage_sample.sh**.</span><span class="sxs-lookup"><span data-stu-id="755c4-146">hello next steps assume you've named your script **my_storage_sample.sh**.</span></span>

4. <span data-ttu-id="755c4-147">Merhaba komut dosyası yürütülebilir, olarak gerekiyorsa işaretleyin:`chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="755c4-147">Mark hello script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>

5. <span data-ttu-id="755c4-148">Merhaba betiğini yürütün.</span><span class="sxs-lookup"><span data-stu-id="755c4-148">Execute hello script.</span></span> <span data-ttu-id="755c4-149">Örneğin, Bash içinde:`./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="755c4-149">For example, in Bash: `./my_storage_sample.sh`</span></span>

<span data-ttu-id="755c4-150">Çıktı benzer toohello aşağıdakilere bakın ve hello gerekir  **\<destination_file\>**  hello belirtilen komut dosyası yerel bilgisayarınızda görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="755c4-150">You should see output similar toohello following, and hello **\<destination_file\>** you specified in hello script should appear on your local computer.</span></span>

```
Creating hello container...
{
  "created": true
}
Uploading hello file...
Percent complete: %100.0
Listing hello blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading hello file...
Name
---------
README.md
Done
```

> [!TIP]
> <span data-ttu-id="755c4-151">Merhaba önceki çıktı olarak **tablo** biçimi.</span><span class="sxs-lookup"><span data-stu-id="755c4-151">hello preceding output is in **table** format.</span></span> <span data-ttu-id="755c4-152">Hangi hello belirterek biçimi toouse çıktı belirtebilirsiniz `--output` CLI komutlarınızı değişkeninde veya genel kullanarak ayarlayın `az configure`.</span><span class="sxs-lookup"><span data-stu-id="755c4-152">You can specify which output format toouse by specifying hello `--output` argument in your CLI commands, or set it globally using `az configure`.</span></span>
>

## <a name="manage-storage-accounts"></a><span data-ttu-id="755c4-153">Depolama hesaplarını yönetme</span><span class="sxs-lookup"><span data-stu-id="755c4-153">Manage storage accounts</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="755c4-154">Yeni depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="755c4-154">Create a new storage account</span></span>
<span data-ttu-id="755c4-155">toouse Azure depolama, depolama hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="755c4-155">toouse Azure Storage, you need a storage account.</span></span> <span data-ttu-id="755c4-156">Bilgisayarınızı çok yapılandırdıktan sonra yeni bir Azure depolama hesabı oluşturabilirsiniz[tooyour abonelik bağlanmak](#connect-to-your-azure-subscription).</span><span class="sxs-lookup"><span data-stu-id="755c4-156">You can create a new Azure Storage account after you've configured your computer too[connect tooyour subscription](#connect-to-your-azure-subscription).</span></span>

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* <span data-ttu-id="755c4-157">`--location`[Gerekli]: konum.</span><span class="sxs-lookup"><span data-stu-id="755c4-157">`--location` [Required]: Location.</span></span> <span data-ttu-id="755c4-158">Örneğin, "Batı ABD".</span><span class="sxs-lookup"><span data-stu-id="755c4-158">For example, "West US".</span></span>
* <span data-ttu-id="755c4-159">`--name`[Gerekli]: hello depolama hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="755c4-159">`--name` [Required]: hello storage account name.</span></span> <span data-ttu-id="755c4-160">Merhaba adı 3 too24 karakterden oluşmalı ve yalnızca küçük harf alfasayısal karakterler kullanın.</span><span class="sxs-lookup"><span data-stu-id="755c4-160">hello name must be 3 too24 characters in length, and use only lowercase alphanumeric characters.</span></span>
* <span data-ttu-id="755c4-161">`--resource-group`[Gerekli]: kaynak grubunun adı.</span><span class="sxs-lookup"><span data-stu-id="755c4-161">`--resource-group` [Required]: Name of resource group.</span></span>
* <span data-ttu-id="755c4-162">`--sku`[Gerekli]: depolama hesabı SKU hello.</span><span class="sxs-lookup"><span data-stu-id="755c4-162">`--sku` [Required]: hello storage account SKU.</span></span> <span data-ttu-id="755c4-163">İzin verilen değerler:</span><span class="sxs-lookup"><span data-stu-id="755c4-163">Allowed values:</span></span>
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a><span data-ttu-id="755c4-164">Varsayılan Azure depolama hesabı ortam değişkenlerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="755c4-164">Set default Azure storage account environment variables</span></span>
<span data-ttu-id="755c4-165">Azure aboneliğinizde birden çok depolama hesabı olabilir.</span><span class="sxs-lookup"><span data-stu-id="755c4-165">You can have multiple storage accounts in your Azure subscription.</span></span> <span data-ttu-id="755c4-166">bunlardan birini tooselect tüm sonraki depolama toouse komutlar, bu ortam değişkenleri ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="755c4-166">tooselect one of them toouse for all subsequent storage commands, you can set these environment variables:</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="755c4-167">Başka bir şekilde tooset varsayılan depolama hesabı bağlantı dizesi kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="755c4-167">Another way tooset a default storage account is by using a connection string.</span></span> <span data-ttu-id="755c4-168">İlk olarak, hello hello bağlantı dizesi alma `show-connection-string` komutu:</span><span class="sxs-lookup"><span data-stu-id="755c4-168">First, get hello connection string with hello `show-connection-string` command:</span></span>

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

<span data-ttu-id="755c4-169">Ardından kopya hello çıkış bağlantı dizesi ve ayarlama hello `AZURE_STORAGE_CONNECTION_STRING` ortam değişkeni (tooenclose hello bağlantı dizesi tırnak gerekebilir):</span><span class="sxs-lookup"><span data-stu-id="755c4-169">Then copy hello output connection string and set hello `AZURE_STORAGE_CONNECTION_STRING` environment variable (you might need tooenclose hello connection string in quotes):</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> <span data-ttu-id="755c4-170">Aşağıdaki bölümlerde, bu makalenin hello tüm örneklerde hello ayarladığınızdan varsayın `AZURE_STORAGE_ACCOUNT` ve `AZURE_STORAGE_ACCESS_KEY` ortam değişkenleri.</span><span class="sxs-lookup"><span data-stu-id="755c4-170">All examples in hello following sections of this article assume that you've set hello `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY` environment variables.</span></span>
>

## <a name="create-and-manage-blobs"></a><span data-ttu-id="755c4-171">Oluşturma ve BLOB'ları yönetme</span><span class="sxs-lookup"><span data-stu-id="755c4-171">Create and manage blobs</span></span>
<span data-ttu-id="755c4-172">Azure Blob Depolama büyük miktarda gelen herhangi bir yere Merhaba Dünya HTTP veya HTTPS üzerinden erişilebilen metin veya ikili veriler gibi yapılandırılmamış veriyi depolamak için bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="755c4-172">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="755c4-173">Bu bölümde, zaten Azure Blob Depolama kavramlarına alışık olduğunuz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="755c4-173">This section assumes that you are already familiar with Azure Blob storage concepts.</span></span> <span data-ttu-id="755c4-174">Ayrıntılı bilgi için bkz: [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](storage-dotnet-how-to-use-blobs.md) ve [Blob hizmeti kavramları](/rest/api/storageservices/blob-service-concepts).</span><span class="sxs-lookup"><span data-stu-id="755c4-174">For detailed information, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](/rest/api/storageservices/blob-service-concepts).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="755c4-175">Bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="755c4-175">Create a container</span></span>
<span data-ttu-id="755c4-176">Azure depolama her blob bir kapsayıcıda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="755c4-176">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="755c4-177">Hello kullanarak bir kapsayıcı oluşturabilirsiniz `az storage container create` komutu:</span><span class="sxs-lookup"><span data-stu-id="755c4-177">You can create a container by using hello `az storage container create` command:</span></span>

```azurecli
az storage container create --name <container_name>
```

<span data-ttu-id="755c4-178">İsteğe bağlı hello belirterek üç düzeyinden birini okuma erişimi için yeni bir kapsayıcı ayarlayabilirsiniz `--public-access` bağımsız değişkeni:</span><span class="sxs-lookup"><span data-stu-id="755c4-178">You can set one of three levels of read access for a new container by specifying hello optional  `--public-access` argument:</span></span>

* <span data-ttu-id="755c4-179">`off`(varsayılan): kapsayıcı verileri, özel toohello hesap sahibi.</span><span class="sxs-lookup"><span data-stu-id="755c4-179">`off` (default): Container data is private toohello account owner.</span></span>
* <span data-ttu-id="755c4-180">`blob`: BLOB'lar ortak okuma erişimi.</span><span class="sxs-lookup"><span data-stu-id="755c4-180">`blob`: Public read access for blobs.</span></span>
* <span data-ttu-id="755c4-181">`container`: Ortak okuma ve liste toohello tüm kapsayıcı erişin.</span><span class="sxs-lookup"><span data-stu-id="755c4-181">`container`: Public read and list access toohello entire container.</span></span>

<span data-ttu-id="755c4-182">Daha fazla bilgi için bkz: [anonim okuma erişimini toocontainers ve BLOB'ları yönetmek](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="755c4-182">For more information, see [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md).</span></span>

### <a name="upload-a-blob-tooa-container"></a><span data-ttu-id="755c4-183">Bir blob tooa kapsayıcı karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="755c4-183">Upload a blob tooa container</span></span>
<span data-ttu-id="755c4-184">Azure Blob storage blok destekler, ekleme ve sayfa BLOB'ları.</span><span class="sxs-lookup"><span data-stu-id="755c4-184">Azure Blob storage supports block, append, and page blobs.</span></span> <span data-ttu-id="755c4-185">Karşıya yükleme BLOB'ların tooa kapsayıcı hello kullanarak `blob upload` komutu:</span><span class="sxs-lookup"><span data-stu-id="755c4-185">Upload blobs tooa container by using hello `blob upload` command:</span></span>

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 <span data-ttu-id="755c4-186">Varsayılan olarak, hello `blob upload` komutu *.vhd dosyaları toopage BLOB veya blok blobları aksi yükler.</span><span class="sxs-lookup"><span data-stu-id="755c4-186">By default, hello `blob upload` command uploads *.vhd files toopage blobs, or block blobs otherwise.</span></span> <span data-ttu-id="755c4-187">toospecify başka türü bir blob karşıya yükleme, hello kullanabilirsiniz `--type` izin verilen değerler bağımsız değişken-- `append`, `block`, ve `page`.</span><span class="sxs-lookup"><span data-stu-id="755c4-187">toospecify another type when you upload a blob, you can use hello `--type` argument--allowed values are `append`, `block`, and `page`.</span></span>

 <span data-ttu-id="755c4-188">Merhaba farklı blob türleri hakkında daha fazla bilgi için bkz: [anlama blok Blobları, ekleme Blobları ve sayfa Bloblarını](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span><span class="sxs-lookup"><span data-stu-id="755c4-188">For more information on hello different blob types, see [Understanding Block Blobs, Append Blobs, and Page Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span></span>


### <a name="download-a-blob-from-a-container"></a><span data-ttu-id="755c4-189">Kapsayıcıdan blob indirme</span><span class="sxs-lookup"><span data-stu-id="755c4-189">Download a blob from a container</span></span>
<span data-ttu-id="755c4-190">Bu örnekte gösterilmiştir nasıl toodownload bir kapsayıcı blobundan:</span><span class="sxs-lookup"><span data-stu-id="755c4-190">This example demonstrates how toodownload a blob from a container:</span></span>

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="755c4-191">Liste hello BLOB'ları bir kapsayıcıda</span><span class="sxs-lookup"><span data-stu-id="755c4-191">List hello blobs in a container</span></span>

<span data-ttu-id="755c4-192">Liste hello BLOB'ları bir kapsayıcıda hello ile [az depolama blob listesi](/cli/azure/storage/blob#list) komutu.</span><span class="sxs-lookup"><span data-stu-id="755c4-192">List hello blobs in a container with hello [az storage blob list](/cli/azure/storage/blob#list) command.</span></span>

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a><span data-ttu-id="755c4-193">BLOB kopyalama</span><span class="sxs-lookup"><span data-stu-id="755c4-193">Copy blobs</span></span>
<span data-ttu-id="755c4-194">Blobları, depolama hesaplarıyla bölgeler içinde veya bunların arasında zaman uyumsuz olarak kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="755c4-194">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="755c4-195">Merhaba aşağıdaki örnekte nasıl tooanother toocopy bloblarından bir depolama hesabı gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="755c4-195">hello following example demonstrates how toocopy blobs from one storage account tooanother.</span></span> <span data-ttu-id="755c4-196">İlk olarak bir kapsayıcı hello kaynak depolama hesabında kendi BLOB'lar için herkese okuma erişimi belirtme oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="755c4-196">We first create a container in hello source storage account, specifying public read-access for its blobs.</span></span> <span data-ttu-id="755c4-197">Ardından, biz bir dosya toohello kapsayıcısı ve son olarak, bu kapsayıcısından kopyalama hello blob bir kapsayıcıda hello hedef depolama hesabının içine karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="755c4-197">Next, we upload a file toohello container, and finally, copy hello blob from that container into a container in hello destination storage account.</span></span>

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob toocontainer in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account toodestination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

<span data-ttu-id="755c4-198">Yukarıdaki örnek Hello hello Hedef kapsayıcıyı hello hedef depolama hesabındaki hello kopyalama işlemi toosucceed için varolmalıdır.</span><span class="sxs-lookup"><span data-stu-id="755c4-198">In hello above example, hello destination container must already exist in hello destination storage account for hello copy operation toosucceed.</span></span> <span data-ttu-id="755c4-199">Ayrıca, hello kaynak blob Hello belirtilen `--source-uri` bağımsız değişkeni bir paylaşılan erişim imzası (SAS) belirteci eklemek veya bu örnekte olduğu gibi genel olarak erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="755c4-199">Additionally, hello source blob specified in hello `--source-uri` argument must either include a shared access signature (SAS) token, or be publicly accessible, as in this example.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="755c4-200">Blob silme</span><span class="sxs-lookup"><span data-stu-id="755c4-200">Delete a blob</span></span>
<span data-ttu-id="755c4-201">toodelete bir blob kullanmak hello `blob delete` komutu:</span><span class="sxs-lookup"><span data-stu-id="755c4-201">toodelete a blob, use hello `blob delete` command:</span></span>

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="755c4-202">Oluşturun ve dosya paylaşımlarını yönetmek</span><span class="sxs-lookup"><span data-stu-id="755c4-202">Create and manage file shares</span></span>
<span data-ttu-id="755c4-203">Azure File storage hello sunucu ileti bloğu (SMB) protokolünü kullanan uygulamalar için paylaşılan depolama alanı sağlar.</span><span class="sxs-lookup"><span data-stu-id="755c4-203">Azure File storage offers shared storage for applications using hello Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="755c4-204">Microsoft Azure sanal makineler ve bulut Hizmetleri yanı sıra, şirket içi uygulamalara bağlı paylaşımlar üzerinden dosya verileri paylaşabilir.</span><span class="sxs-lookup"><span data-stu-id="755c4-204">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="755c4-205">Dosya paylaşımları ve dosya verilerini hello Azure CLI aracılığıyla yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="755c4-205">You can manage file shares and file data via hello Azure CLI.</span></span> <span data-ttu-id="755c4-206">Azure File storage hakkında daha fazla bilgi için bkz: [Windows Azure File storage ile çalışmaya başlama](storage-dotnet-how-to-use-files.md) veya [nasıl toouse Linux Azure File storage](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="755c4-206">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) or [How toouse Azure File storage with Linux](storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="755c4-207">Dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="755c4-207">Create a file share</span></span>
<span data-ttu-id="755c4-208">Bir Azure dosya paylaşımı azure'da SMB dosya paylaşımı değil.</span><span class="sxs-lookup"><span data-stu-id="755c4-208">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="755c4-209">Tüm dizin ve dosyaların bir dosya paylaşımı oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="755c4-209">All directories and files must be created in a file share.</span></span> <span data-ttu-id="755c4-210">Bir hesapta sınırsız sayıda paylaşım olabilir ve bir paylaşım dosyaları, toohello kapasite limitlerini hello depolama hesabının sınırsız sayıda depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="755c4-210">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up toohello capacity limits of hello storage account.</span></span> <span data-ttu-id="755c4-211">Merhaba aşağıdaki örnek adlı bir dosya paylaşımı oluşturur **paylaşımım**.</span><span class="sxs-lookup"><span data-stu-id="755c4-211">hello following example creates a file share named **myshare**.</span></span>

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="755c4-212">Dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="755c4-212">Create a directory</span></span>
<span data-ttu-id="755c4-213">Bir dizin Azure dosya paylaşımının hiyerarşik yapıda sağlar.</span><span class="sxs-lookup"><span data-stu-id="755c4-213">A directory provides a hierarchical structure in an Azure file share.</span></span> <span data-ttu-id="755c4-214">Merhaba aşağıdaki örnek adlı bir dizin oluşturur **Dizinim** hello dosya paylaşımında.</span><span class="sxs-lookup"><span data-stu-id="755c4-214">hello following example creates a directory named **myDir** in hello file share.</span></span>

```azurecli
az storage directory create --name myDir --share-name myshare
```

<span data-ttu-id="755c4-215">Bir dizin yolu birden çok düzeyi, örneğin içerebilir **dizin1/dir2**.</span><span class="sxs-lookup"><span data-stu-id="755c4-215">A directory path can include multiple levels, for example **dir1/dir2**.</span></span> <span data-ttu-id="755c4-216">Ancak, tüm üst dizinleri bir alt dizin oluşturmadan önce mevcut olduğundan emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="755c4-216">However, you must ensure that all parent directories exist before creating a subdirectory.</span></span> <span data-ttu-id="755c4-217">Örneğin, yol **dizin1/dir2**, dizin oluşturmak **dizin1**, dizin oluşturma **dir2**.</span><span class="sxs-lookup"><span data-stu-id="755c4-217">For example, for path **dir1/dir2**, you must first create directory **dir1**, then create directory **dir2**.</span></span>

### <a name="upload-a-local-file-tooa-share"></a><span data-ttu-id="755c4-218">Bir yerel dosya tooa paylaşımı karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="755c4-218">Upload a local file tooa share</span></span>
<span data-ttu-id="755c4-219">Merhaba aşağıdaki örnek dosya karşıya yükleme **~/temp/samplefile.txt** hello tooroot **paylaşımım** dosya paylaşımı.</span><span class="sxs-lookup"><span data-stu-id="755c4-219">hello following example uploads a file from **~/temp/samplefile.txt** tooroot of hello **myshare** file share.</span></span> <span data-ttu-id="755c4-220">Merhaba `--source` bağımsız değişkeni hello var olan yerel dosya tooupload belirtir.</span><span class="sxs-lookup"><span data-stu-id="755c4-220">hello `--source` argument specifies hello existing local file tooupload.</span></span>

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

<span data-ttu-id="755c4-221">Dizin oluşturma gibi ile Merhaba paylaşımı tooupload hello dosya tooan var olan dizini içindeki hello paylaşımı içinde bir dizin yolu belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="755c4-221">As with directory creation, you can specify a directory path within hello share tooupload hello file tooan existing directory within hello share:</span></span>

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

<span data-ttu-id="755c4-222">Merhaba paylaşımda bir dosya boyutu too1 TB yukarı olabilir.</span><span class="sxs-lookup"><span data-stu-id="755c4-222">A file in hello share can be up too1 TB in size.</span></span>

### <a name="list-hello-files-in-a-share"></a><span data-ttu-id="755c4-223">Bir paylaşımda hello dosyaları listeleme</span><span class="sxs-lookup"><span data-stu-id="755c4-223">List hello files in a share</span></span>
<span data-ttu-id="755c4-224">Hello kullanarak dosyaları ve dizinleri bir paylaşımda listeleyebilirsiniz `az storage file list` komutu:</span><span class="sxs-lookup"><span data-stu-id="755c4-224">You can list files and directories in a share by using hello `az storage file list` command:</span></span>

```azurecli
# List hello files in hello root of a share
az storage file list --share-name myshare --output table

# List hello files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List hello files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a><span data-ttu-id="755c4-225">Dosyaları kopyalama</span><span class="sxs-lookup"><span data-stu-id="755c4-225">Copy files</span></span>      
<span data-ttu-id="755c4-226">Tooanother dosyası, dosya tooa blob veya bir blobu tooa dosyayı kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="755c4-226">You can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="755c4-227">Örneğin, farklı bir paylaşım dosya tooa dizininde toocopy:</span><span class="sxs-lookup"><span data-stu-id="755c4-227">For example, toocopy a file tooa directory in a different share:</span></span>        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a><span data-ttu-id="755c4-228">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="755c4-228">Next steps</span></span>
<span data-ttu-id="755c4-229">Azure CLI 2.0 hello ile çalışma hakkında daha fazla bilgi edinmek için bazı ek kaynaklar aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="755c4-229">Here are some additional resources for learning more about working with hello Azure CLI 2.0.</span></span>

* [<span data-ttu-id="755c4-230">Azure CLI 2.0 ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="755c4-230">Get started with Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="755c4-231">Azure CLI 2.0 komut başvurusu</span><span class="sxs-lookup"><span data-stu-id="755c4-231">Azure CLI 2.0 command reference</span></span>](/cli/azure)
* [<span data-ttu-id="755c4-232">Github'daki Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="755c4-232">Azure CLI 2.0 on GitHub</span></span>](https://github.com/Azure/azure-cli)
