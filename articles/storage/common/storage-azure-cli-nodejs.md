---
title: aaaUsing hello Azure Storage ile Azure CLI 1.0 | Microsoft Docs
description: "Nasıl toouse Azure komut satırı arabirimi (Azure CLI) 1.0 ile Azure depolama toocreate hello ve depolama hesaplarını yönetme ve Azure BLOB'ları ve dosyalar ile çalışırken öğrenin. platformlar arası aracı Hello Azure CLI değil"
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: b502232a-e8f6-4d6c-befd-3476592e0e35
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: seguler
ms.openlocfilehash: 25e459403dde631741403c8722ed07beafac35c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-10-with-azure-storage"></a><span data-ttu-id="6e0ed-104">Hello Azure CLI 1.0 Azure Storage ile kullanma</span><span class="sxs-lookup"><span data-stu-id="6e0ed-104">Using hello Azure CLI 1.0 with Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="6e0ed-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="6e0ed-105">Overview</span></span>

<span data-ttu-id="6e0ed-106">Hello Azure CLI açık kaynak, bir dizi hello Azure platformu ile çalışmak için platformlar arası komutları sağlar.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-106">hello Azure CLI provides a set of open source, cross-platform commands for working with hello Azure Platform.</span></span> <span data-ttu-id="6e0ed-107">Aynı işlevselliği bulunan hello hello çoğunu sağlayan [Azure portal](https://portal.azure.com) de gibi zengin veri erişim işlevselliği.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-107">It provides much of hello same functionality found in hello [Azure portal](https://portal.azure.com) as well as rich data access functionality.</span></span>

<span data-ttu-id="6e0ed-108">Bu kılavuzda, biz ele alacağız nasıl toouse [Azure komut satırı arabirimi (Azure CLI)](../../cli-install-nodejs.md) tooperform çeşitli Azure Storage ile geliştirme ve yönetim görevleri.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-108">In this guide, we'll explore how toouse [Azure Command-Line Interface (Azure CLI)](../../cli-install-nodejs.md) tooperform a variety of development and administration tasks with Azure Storage.</span></span> <span data-ttu-id="6e0ed-109">İndirin ve yükleyin veya yükseltme toohello öneririz bu kılavuzu kullanmadan önce en son Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-109">We recommend that you download and install or upgrade toohello latest Azure CLI before using this guide.</span></span>

<span data-ttu-id="6e0ed-110">Bu kılavuz, Azure Storage hello temel kavramlarını anladığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-110">This guide assumes that you understand hello basic concepts of Azure Storage.</span></span> <span data-ttu-id="6e0ed-111">Merhaba Kılavuzu bir dizi betiği hello Azure Storage ile Azure CLI toodemonstrate hello kullanımı sağlar.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-111">hello guide provides a number of scripts toodemonstrate hello usage of hello Azure CLI with Azure Storage.</span></span> <span data-ttu-id="6e0ed-112">Her komut dosyası çalıştırılmadan önce yapılandırmanıza göre hello betik değişkenlerini emin tooupdate olması.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-112">Be sure tooupdate hello script variables based on your configuration before running each script.</span></span>

> [!NOTE]
> <span data-ttu-id="6e0ed-113">Başlangıç Kılavuzu, Klasik depolama hesapları için hello Azure CLI komut ve komut dosyası örnekler verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-113">hello guide provides hello Azure CLI command and script examples for classic storage accounts.</span></span> <span data-ttu-id="6e0ed-114">Bkz: [kullanma hello Mac, Linux ve Windows Azure kaynak yönetimi için Azure CLI](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) Resource Manager depolama hesapları için Azure CLI komutları için.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-114">See [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) for Azure CLI commands for Resource Manager storage accounts.</span></span>
>
>

[!INCLUDE [storage-cli-versions](../../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-hello-azure-cli-in-5-minutes"></a><span data-ttu-id="6e0ed-115">5 dakika içinde Azure Storage ve hello Azure CLI kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="6e0ed-115">Get started with Azure Storage and hello Azure CLI in 5 minutes</span></span>
<span data-ttu-id="6e0ed-116">Bu kılavuzda Ubuntu örnekler için kullanılır, ancak diğer işletim sistemi platformlarını benzer şekilde gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-116">This guide uses Ubuntu for examples, but other OS platforms should perform similarly.</span></span>

<span data-ttu-id="6e0ed-117">**Yeni tooAzure:** Microsoft Azure aboneliği ve bu abonelikle ilişkili bir Microsoft hesabı alın.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-117">**New tooAzure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="6e0ed-118">Azure satın alma seçenekleri hakkında daha fazla bilgi için bkz: [ücretsiz deneme](https://azure.microsoft.com/pricing/free-trial/), [satın alma seçenekleri](https://azure.microsoft.com/pricing/purchase-options/), ve [üye teklifleri](https://azure.microsoft.com/pricing/member-offers/) (MSDN, Microsoft iş ortağı ağı ve, BizSpark üyeleri için ve diğer Microsoft programları).</span><span class="sxs-lookup"><span data-stu-id="6e0ed-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="6e0ed-119">Bkz: [Azure Active Directory'de (Azure AD) yönetici rolleri atama](https://msdn.microsoft.com/library/azure/hh531793.aspx) Azure abonelikleri hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="6e0ed-120">**Microsoft Azure aboneliği ve hesabı oluşturduktan sonra:**</span><span class="sxs-lookup"><span data-stu-id="6e0ed-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="6e0ed-121">Azure CLI hello yönergeleri izleyerek özetlenen hello yükleyip [yükleme hello Azure CLI](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="6e0ed-121">Download and install hello Azure CLI following hello instructions outlined in [Install hello Azure CLI](../../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="6e0ed-122">Hello Azure CLI yüklendikten sonra mümkün toouse olacaktır Merhaba, komut satırı arabirimi (Bash, Terminal, komut istemi) tooaccess hello Azure CLI komutlarının azure komutu.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-122">Once hello Azure CLI has been installed, you will be able toouse hello azure command from your command-line interface (Bash, Terminal, Command prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="6e0ed-123">Türü hello _azure_ komut ve çıktı aşağıdaki hello görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-123">Type hello _azure_ command and you should see hello following output.</span></span>

    ![Azure komut çıktısı](./media/storage-azure-cli/azure_command.png)   
3. <span data-ttu-id="6e0ed-125">Merhaba komut satırı arabiriminde yazın `azure storage` tüm toolist hello azure depolama komutları ve hello işlevler hello Azure CLI'nin sağladığı bir ilk izlenim alın.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-125">In hello command-line interface, type `azure storage` toolist out all hello azure storage commands and get a first impression of hello functionalities hello Azure CLI provides.</span></span> <span data-ttu-id="6e0ed-126">Komut adı ile yazabilirsiniz **-h** parametresi (örneğin, `azure storage share create -h`) komut sözdizimi toosee ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-126">You can type command name with **-h** parameter (for example, `azure storage share create -h`) toosee details of command syntax.</span></span>
4. <span data-ttu-id="6e0ed-127">Şimdi, biz temel Azure CLI komutları tooaccess Azure Storage gösteren basit bir komut dosyası size.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-127">Now, we'll give you a simple script that shows basic Azure CLI commands tooaccess Azure Storage.</span></span> <span data-ttu-id="6e0ed-128">Merhaba komut dosyası ilk tooset iki değişken depolama hesabı ve anahtarı için istenir.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-128">hello script will first ask you tooset two variables for your storage account and key.</span></span> <span data-ttu-id="6e0ed-129">Ardından, hello betik bu yeni depolama hesabı yeni bir kapsayıcı oluşturur ve var olan bir görüntü dosyası (blob) toothat kapsayıcıyı karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-129">Then, hello script will create a new container in this new storage account and upload an existing image file (blob) toothat container.</span></span> <span data-ttu-id="6e0ed-130">Bu kapsayıcıdaki tüm blob'lara Hello komut dosyasını listeler sonra hello yerel bilgisayarda var olan hello görüntü dosyası toohello hedef dizini indirir.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-130">After hello script lists all blobs in that container, it will download hello image file toohello destination directory which exists on hello local computer.</span></span>

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating hello container..."
    azure storage container create $container_name

    echo "Uploading hello image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing hello blobs..."
    azure storage blob list $container_name

    echo "Downloading hello image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. <span data-ttu-id="6e0ed-131">Yerel bilgisayarınızda, tercih edilen metin düzenleyicisi (örneğin VIM) açın.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-131">In your local computer, open your preferred text editor (vim for example).</span></span> <span data-ttu-id="6e0ed-132">Betik yukarıdaki Merhaba, metin düzenleyicisi yazın.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-132">Type hello above script into your text editor.</span></span>
6. <span data-ttu-id="6e0ed-133">Şimdi, yapılandırma ayarlarınızı temel alan tooupdate hello komut dosyası değişkenleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-133">Now, you need tooupdate hello script variables based on your configuration settings.</span></span>

   * <span data-ttu-id="6e0ed-134">**< Storage_account_name >** hello komut dosyasında adı verilen hello kullanın veya depolama hesabınız için yeni bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-134">**<storage_account_name>** Use hello given name in hello script or enter a new name for your storage account.</span></span> <span data-ttu-id="6e0ed-135">**Önemli:** hello depolama hesabının adını hello Azure içinde benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-135">**Important:** hello name of hello storage account must be unique in Azure.</span></span> <span data-ttu-id="6e0ed-136">Çok küçük olmalıdır!</span><span class="sxs-lookup"><span data-stu-id="6e0ed-136">It must be lowercase, too!</span></span>
   * <span data-ttu-id="6e0ed-137">**< storage_account_key >** hello erişim anahtarını depolama hesabınızın.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-137">**<storage_account_key>** hello access key of your storage account.</span></span>
   * <span data-ttu-id="6e0ed-138">**< Container_name >** hello komut dosyasında adı verilen hello kullanın veya, kapsayıcı için yeni bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-138">**<container_name>** Use hello given name in hello script or enter a new name for your container.</span></span>
   * <span data-ttu-id="6e0ed-139">**< İmage_to_upload >** yolu tooa resim, yerel bilgisayarınızda gibi girin: "~ / images/HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="6e0ed-139">**<image_to_upload>** Enter a path tooa picture on your local computer, such as: "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="6e0ed-140">**< Destination_folder >** bir yolu tooa yerel dizin toostore dosyaları Azure Storage'dan gibi indirilen girin: "~/downloadImages".</span><span class="sxs-lookup"><span data-stu-id="6e0ed-140">**<destination_folder>** Enter a path tooa local directory toostore files downloaded from Azure Storage, such as: "~/downloadImages".</span></span>
7. <span data-ttu-id="6e0ed-141">Merhaba gerekli VIM değişkenlerde güncelleştirdikten sonra tuş bileşimlerini basın `ESC`, `:`, `wq!` toosave hello komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-141">After you've updated hello necessary variables in vim, press key combinations `ESC`, `:`, `wq!` toosave hello script.</span></span>
8. <span data-ttu-id="6e0ed-142">toorun bu komut, komut dosyası dosya adı hello bash konsolunda türü hello yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-142">toorun this script, simply type hello script file name in hello bash console.</span></span> <span data-ttu-id="6e0ed-143">Bu betik çalıştıktan sonra indirilen hello görüntü dosyasını içeren bir yerel hedef klasör olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-143">After this script runs, you should have a local destination folder that includes hello downloaded image file.</span></span> <span data-ttu-id="6e0ed-144">Merhaba ekran aşağıdaki örnek çıkış şunları gösterir:</span><span class="sxs-lookup"><span data-stu-id="6e0ed-144">hello following screenshot shows an example output:</span></span>

<span data-ttu-id="6e0ed-145">Merhaba betik çalıştıktan sonra indirilen hello görüntü dosyasını içeren bir yerel hedef klasör olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-145">After hello script runs, you should have a local destination folder that includes hello downloaded image file.</span></span>

## <a name="manage-storage-accounts-with-hello-azure-cli"></a><span data-ttu-id="6e0ed-146">Depolama hesapları hello Azure CLI ile yönetme</span><span class="sxs-lookup"><span data-stu-id="6e0ed-146">Manage storage accounts with hello Azure CLI</span></span>
### <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="6e0ed-147">Tooyour Azure aboneliğine bağlanma</span><span class="sxs-lookup"><span data-stu-id="6e0ed-147">Connect tooyour Azure subscription</span></span>
<span data-ttu-id="6e0ed-148">Merhaba depolama komutların çoğu Azure aboneliği çalışır ancak tooconnect tooyour hello Azure CLI abonelikten öneririz.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-148">While most of hello storage commands will work without an Azure subscription, we recommend you tooconnect tooyour subscription from hello Azure CLI.</span></span> <span data-ttu-id="6e0ed-149">Aboneliğinize tooconfigure hello Azure CLI toowork izleyin hello adımlarda [tooan Azure aboneliği hello Azure CLI ' bağlanma](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="6e0ed-149">tooconfigure hello Azure CLI toowork with your subscription, follow hello steps in [Connect tooan Azure subscription from hello Azure CLI](../../xplat-cli-connect.md).</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="6e0ed-150">Yeni depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e0ed-150">Create a new storage account</span></span>
<span data-ttu-id="6e0ed-151">toouse Azure depolama, depolama hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-151">toouse Azure storage, you will need a storage account.</span></span> <span data-ttu-id="6e0ed-152">Bilgisayar tooconnect tooyour aboneliğinizi yapılandırdıktan sonra yeni bir Azure depolama hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-152">You can create a new Azure storage account after you have configured your computer tooconnect tooyour subscription.</span></span>

```azurecli
azure storage account create <account_name>
```

<span data-ttu-id="6e0ed-153">Depolama hesabınızın adını Hello uzunluğu 3 ile 24 karakter arasında olmalı ve sayı ve yalnızca küçük harf kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-153">hello name of your storage account must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a><span data-ttu-id="6e0ed-154">Ortam değişkenleri varsayılan bir Azure depolama hesabı ayarlama</span><span class="sxs-lookup"><span data-stu-id="6e0ed-154">Set a default Azure storage account in environment variables</span></span>
<span data-ttu-id="6e0ed-155">Aboneliğinizde birden çok depolama hesabı olabilir.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-155">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="6e0ed-156">Bunlardan birini seçin ve tüm hello depolama hello aynı komutları için ortam değişkenlerini hello ayarlama oturumu.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-156">You can choose one of them and set it in hello environment variables for all hello storage commands in hello same session.</span></span> <span data-ttu-id="6e0ed-157">Bu komutlar hello depolama belirtmeden hesap ve açıkça anahtar toorun hello Azure CLI depolama sağlar.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-157">This enables you toorun hello Azure CLI storage commands without specifying hello storage account and key explicitly.</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="6e0ed-158">Başka bir şekilde tooset varsayılan depolama hesabı bağlantı dizesi kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-158">Another way tooset a default storage account is using connection string.</span></span> <span data-ttu-id="6e0ed-159">İlk olarak hello bağlantı dizesini komutla alın:</span><span class="sxs-lookup"><span data-stu-id="6e0ed-159">Firstly get hello connection string by command:</span></span>

```azurecli
azure storage account connectionstring show <account_name>
```

<span data-ttu-id="6e0ed-160">Merhaba çıkış bağlantı dizesini kopyalayın ve tooenvironment değişkeni ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="6e0ed-160">Then copy hello output connection string and set it tooenvironment variable:</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a><span data-ttu-id="6e0ed-161">Oluşturma ve BLOB'ları yönetme</span><span class="sxs-lookup"><span data-stu-id="6e0ed-161">Create and manage blobs</span></span>
<span data-ttu-id="6e0ed-162">Azure Blob Depolama büyük miktarda gelen herhangi bir yere Merhaba Dünya HTTP veya HTTPS üzerinden erişilebilen metin veya ikili veriler gibi yapılandırılmamış veriyi depolamak için bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-162">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="6e0ed-163">Bu bölümde, zaten hello Azure Blob Depolama kavramlarına alışık olduğunuz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-163">This section assumes that you are already familiar with hello Azure Blob storage concepts.</span></span> <span data-ttu-id="6e0ed-164">Ayrıntılı bilgi için bkz: [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../blobs/storage-dotnet-how-to-use-blobs.md) ve [Blob hizmeti kavramları](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="6e0ed-164">For detailed information, see [Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="6e0ed-165">Bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e0ed-165">Create a container</span></span>
<span data-ttu-id="6e0ed-166">Azure depolama her blob bir kapsayıcıda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-166">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="6e0ed-167">Hello kullanarak özel bir kapsayıcı oluşturabilirsiniz `azure storage container create` komutu:</span><span class="sxs-lookup"><span data-stu-id="6e0ed-167">You can create a private container using hello `azure storage container create` command:</span></span>

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> <span data-ttu-id="6e0ed-168">Anonim okuma erişimini üç düzeyi vardır: **kapalı**, **Blob**, ve **kapsayıcı**.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-168">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="6e0ed-169">tooprevent anonim erişim tooblobs, kümesi hello izni parametresi çok**devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-169">tooprevent anonymous access tooblobs, set hello Permission parameter too**Off**.</span></span> <span data-ttu-id="6e0ed-170">Varsayılan olarak, hello yeni kapsayıcı özeldir ve yalnızca hello hesap sahibi tarafından erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-170">By default, hello new container is private and can be accessed only by hello account owner.</span></span> <span data-ttu-id="6e0ed-171">tooallow anonim ortak okuma erişimine tooblob, ancak değil toocontainer meta veriler veya toohello listesi hello kapsayıcıdaki blobları, hello izni çok parametre**Blob**.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-171">tooallow anonymous public read access tooblob resources, but not toocontainer metadata or toohello list of blobs in hello container, set hello Permission parameter too**Blob**.</span></span> <span data-ttu-id="6e0ed-172">tooallow tam ortak okuma tooblob kaynaklara erişmesine, kapsayıcı meta verileri ve hello kapsayıcıdaki blobları hello listesi, hello izni çok parametre**kapsayıcı**.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-172">tooallow full public read access tooblob resources, container metadata, and hello list of blobs in hello container, set hello Permission parameter too**Container**.</span></span> <span data-ttu-id="6e0ed-173">Daha fazla bilgi için bkz: [anonim okuma erişimini toocontainers ve BLOB'ları yönetmek](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="6e0ed-173">For more information, see [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>
>
>

### <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="6e0ed-174">Bir kapsayıcıya bir blob yükleme</span><span class="sxs-lookup"><span data-stu-id="6e0ed-174">Upload a blob into a container</span></span>
<span data-ttu-id="6e0ed-175">Azure Blob Storage blok blobları ve sayfa bloblarını destekler.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-175">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="6e0ed-176">Daha fazla bilgi için bkz: [anlama blok Blobları, ekleme Blobları ve sayfa Bloblarını](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="6e0ed-176">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="6e0ed-177">tooa kapsayıcıdaki blobları tooupload, kullanabileceğiniz hello `azure storage blob upload`.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-177">tooupload blobs in tooa container, you can use hello `azure storage blob upload`.</span></span> <span data-ttu-id="6e0ed-178">Varsayılan olarak, bu komut hello yerel dosyaları tooa blok blobu yükler.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-178">By default, this command uploads hello local files tooa block blob.</span></span> <span data-ttu-id="6e0ed-179">toospecify hello türü hello blob için kullanabileceğiniz hello `--blobtype` parametresi.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-179">toospecify hello type for hello blob, you can use hello `--blobtype` parameter.</span></span>

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a><span data-ttu-id="6e0ed-180">Kapsayıcıdan BLOB indirmek</span><span class="sxs-lookup"><span data-stu-id="6e0ed-180">Download blobs from a container</span></span>
<span data-ttu-id="6e0ed-181">Aşağıdaki örnek hello nasıl toodownload kapsayıcıdan BLOB'ların gösterir.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-181">hello following example demonstrates how toodownload blobs from a container.</span></span>

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a><span data-ttu-id="6e0ed-182">BLOB kopyalama</span><span class="sxs-lookup"><span data-stu-id="6e0ed-182">Copy blobs</span></span>
<span data-ttu-id="6e0ed-183">Blobları, depolama hesaplarıyla bölgeler içinde veya bunların arasında zaman uyumsuz olarak kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-183">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="6e0ed-184">Merhaba aşağıdaki örnekte nasıl tooanother toocopy bloblarından bir depolama hesabı gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-184">hello following example demonstrates how toocopy blobs from one storage account tooanother.</span></span> <span data-ttu-id="6e0ed-185">Bu örnekte BLOB'lar nerede genel olarak, bir kapsayıcı oluşturuyoruz anonim olarak erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-185">In this sample we create a container where blobs are publicly, anonymously accessible.</span></span>

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

<span data-ttu-id="6e0ed-186">Bu örnek bir zaman uyumsuz kopya gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-186">This sample performs an asynchronous copy.</span></span> <span data-ttu-id="6e0ed-187">Merhaba çalıştırarak her kopyalama işlemi hello durumunu izleyebilirsiniz `azure storage blob copy show` işlemi.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-187">You can monitor hello status of each copy operation by running hello `azure storage blob copy show` operation.</span></span>

<span data-ttu-id="6e0ed-188">Merhaba kopyalama işlemi için sağlanan hello kaynak URL gerekir ya da genel olarak erişilebilir veya bir SAS (paylaşılan erişim imzası) belirteci dahil unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-188">Note that hello source URL provided for hello copy operation must either be publicly accessible, or include a SAS (shared access signature) token.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="6e0ed-189">Blob silme</span><span class="sxs-lookup"><span data-stu-id="6e0ed-189">Delete a blob</span></span>
<span data-ttu-id="6e0ed-190">toodelete bir blob hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="6e0ed-190">toodelete a blob, use hello below command:</span></span>

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="6e0ed-191">Oluşturun ve dosya paylaşımlarını yönetmek</span><span class="sxs-lookup"><span data-stu-id="6e0ed-191">Create and manage file shares</span></span>
<span data-ttu-id="6e0ed-192">Azure File storage hello standart SMB protokolünü kullanan uygulamalar için paylaşılan depolama alanı sağlar.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-192">Azure File storage offers shared storage for applications using hello standard SMB protocol.</span></span> <span data-ttu-id="6e0ed-193">Microsoft Azure sanal makineler ve bulut Hizmetleri yanı sıra, şirket içi uygulamalara bağlı paylaşımlar üzerinden dosya verileri paylaşabilir.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-193">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="6e0ed-194">Dosya paylaşımları ve dosya verilerini hello Azure CLI aracılığıyla yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-194">You can manage file shares and file data via hello Azure CLI.</span></span> <span data-ttu-id="6e0ed-195">Azure File storage hakkında daha fazla bilgi için bkz: [Windows Azure File storage ile çalışmaya başlama](../storage-dotnet-how-to-use-files.md) veya [nasıl toouse Linux Azure File storage](../storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6e0ed-195">For more information on Azure File storage, see [Get started with Azure File storage on Windows](../storage-dotnet-how-to-use-files.md) or [How toouse Azure File storage with Linux](../storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="6e0ed-196">Dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e0ed-196">Create a file share</span></span>
<span data-ttu-id="6e0ed-197">Bir Azure dosya paylaşımı azure'da SMB dosya paylaşımı değil.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-197">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="6e0ed-198">Tüm dizin ve dosyaların bir dosya paylaşımı oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-198">All directories and files must be created in a file share.</span></span> <span data-ttu-id="6e0ed-199">Bir hesapta sınırsız sayıda paylaşım olabilir ve bir paylaşım dosyaları, toohello kapasite limitlerini hello depolama hesabının sınırsız sayıda depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-199">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up toohello capacity limits of hello storage account.</span></span> <span data-ttu-id="6e0ed-200">Merhaba aşağıdaki örnek adlı bir dosya paylaşımı oluşturur **paylaşımım**.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-200">hello following example creates a file share named **myshare**.</span></span>

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="6e0ed-201">Dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e0ed-201">Create a directory</span></span>
<span data-ttu-id="6e0ed-202">Bir dizin, bir Azure dosya paylaşımı için isteğe bağlı hiyerarşik bir yapı sağlar.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-202">A directory provides an optional hierarchical structure for an Azure file share.</span></span> <span data-ttu-id="6e0ed-203">Merhaba aşağıdaki örnek adlı bir dizin oluşturur **Dizinim** hello dosya paylaşımında.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-203">hello following example creates a directory named **myDir** in hello file share.</span></span>

```azurecli
azure storage directory create myshare myDir
```

<span data-ttu-id="6e0ed-204">Bu dizin yolu, birden çok düzeyi içerebilir Not *örneğin*, **bir / b**.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-204">Note that directory path can include multiple levels, *e.g.*, **a/b**.</span></span> <span data-ttu-id="6e0ed-205">Ancak, tüm üst dizinleri var olduğundan emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-205">However, you must ensure that all parent directories exist.</span></span> <span data-ttu-id="6e0ed-206">Örneğin, yol **bir / b**, dizin oluşturmanız gerekir **bir** ilk olarak, ardından dizin oluşturma **b**.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-206">For example, for path **a/b**, you must create directory **a** first, then create directory **b**.</span></span>

### <a name="upload-a-local-file-toodirectory"></a><span data-ttu-id="6e0ed-207">Yerel dosya toodirectory karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="6e0ed-207">Upload a local file toodirectory</span></span>
<span data-ttu-id="6e0ed-208">Merhaba aşağıdaki örnek dosya karşıya yükleme **~/temp/samplefile.txt** toohello **Dizinim** dizin.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-208">hello following example uploads a file from **~/temp/samplefile.txt** toohello **myDir** directory.</span></span> <span data-ttu-id="6e0ed-209">Merhaba dosya yolu geçerli bir dosya tooa yerel makinenizde işaret şekilde düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="6e0ed-209">Edit hello file path so that it points tooa valid file on your local machine:</span></span>

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

<span data-ttu-id="6e0ed-210">Merhaba paylaşımda bir dosya boyutu too1 TB yukarı olabilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-210">Note that a file in hello share can be up too1 TB in size.</span></span>

### <a name="list-hello-files-in-hello-share-root-or-directory"></a><span data-ttu-id="6e0ed-211">Merhaba paylaşım kök veya dizinde hello dosyaları listeleme</span><span class="sxs-lookup"><span data-stu-id="6e0ed-211">List hello files in hello share root or directory</span></span>
<span data-ttu-id="6e0ed-212">Merhaba dosyaları ve alt dizinleri paylaşım kök ya da komut aşağıdaki hello kullanarak dizin listeleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6e0ed-212">You can list hello files and subdirectories in a share root or a directory using hello following command:</span></span>

```azurecli
azure storage file list myshare myDir
```

<span data-ttu-id="6e0ed-213">Bu hello dizin adı işlemi listeleme hello için isteğe bağlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-213">Note that hello directory name is optional for hello listing operation.</span></span> <span data-ttu-id="6e0ed-214">Atlanırsa, hello komutu hello hello paylaşımının hello kök dizinin içeriğini listeler.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-214">If omitted, hello command lists hello contents of hello root directory of hello share.</span></span>

### <a name="copy-files"></a><span data-ttu-id="6e0ed-215">Dosyaları kopyalama</span><span class="sxs-lookup"><span data-stu-id="6e0ed-215">Copy files</span></span>
<span data-ttu-id="6e0ed-216">Azure CLI 0.9.8 sürümü ile başlayarak, tooanother dosyası, dosya tooa blob veya bir blobu tooa dosyayı kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-216">Beginning with version 0.9.8 of Azure CLI, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="6e0ed-217">Aşağıda nasıl tooperform bu kopyalama göstermek CLI komutları kullanarak işlemleri.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-217">Below we demonstrate how tooperform these copy operations using CLI commands.</span></span> <span data-ttu-id="6e0ed-218">toocopy dosya toohello yeni bir dizin:</span><span class="sxs-lookup"><span data-stu-id="6e0ed-218">toocopy a file toohello new directory:</span></span>

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

<span data-ttu-id="6e0ed-219">toocopy bir blob tooa dosyası dizini:</span><span class="sxs-lookup"><span data-stu-id="6e0ed-219">toocopy a blob tooa file directory:</span></span>

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a><span data-ttu-id="6e0ed-220">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="6e0ed-220">Next Steps</span></span>

<span data-ttu-id="6e0ed-221">Burada depolama kaynaklarla çalışmak için Azure CLI 1.0 komut başvurusu bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6e0ed-221">You can find Azure CLI 1.0 command reference for working with Storage resources here:</span></span>

* [<span data-ttu-id="6e0ed-222">Kaynak Yöneticisi modunda Azure CLI komutları</span><span class="sxs-lookup"><span data-stu-id="6e0ed-222">Azure CLI commands in Resource Manager mode</span></span>](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [<span data-ttu-id="6e0ed-223">Azure Hizmet Yönetimi modunda Azure CLI komutları</span><span class="sxs-lookup"><span data-stu-id="6e0ed-223">Azure CLI commands in Azure Service Management mode</span></span>](../../cli-install-nodejs.md)

<span data-ttu-id="6e0ed-224">Tootry hello istiyor [Azure CLI 2.0](../storage-azure-cli.md), hello Resource Manager dağıtım modeli ile kullanmak için Python içinde yazılmış bizim nesil CLI.</span><span class="sxs-lookup"><span data-stu-id="6e0ed-224">You may also like tootry hello [Azure CLI 2.0](../storage-azure-cli.md), our next-generation CLI written in Python, for use with hello Resource Manager deployment model.</span></span>
