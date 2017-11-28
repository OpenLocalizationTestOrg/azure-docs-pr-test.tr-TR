---
title: Azure Storage ile Azure CLI 1.0 kullanma | Microsoft Docs
description: "Azure komut satırı arabirimi (Azure CLI) 1.0 oluşturmak ve depolama hesaplarını yönetme ve çalışmak için Azure Storage ile Azure BLOB'ları ve dosyalar ile kullanmayı öğrenin. Azure CLI platformlar arası bir araçtır"
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
ms.openlocfilehash: 837cf0f2b8db011b38de795339560574027030f8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="using-the-azure-cli-10-with-azure-storage"></a><span data-ttu-id="1ebc3-104">Azure Storage ile Azure CLI 1.0 kullanma</span><span class="sxs-lookup"><span data-stu-id="1ebc3-104">Using the Azure CLI 1.0 with Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="1ebc3-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="1ebc3-105">Overview</span></span>

<span data-ttu-id="1ebc3-106">Azure CLI, Azure platformu ile çalışmak için platformlar arası komutları açık kaynak kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-106">The Azure CLI provides a set of open source, cross-platform commands for working with the Azure Platform.</span></span> <span data-ttu-id="1ebc3-107">Bulunan aynı işlevlerinin çoğunu sağlayan [Azure portal](https://portal.azure.com) de gibi zengin veri erişim işlevselliği.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-107">It provides much of the same functionality found in the [Azure portal](https://portal.azure.com) as well as rich data access functionality.</span></span>

<span data-ttu-id="1ebc3-108">Bu kılavuzda, biz nasıl kullanılacağını ele alacağız [Azure komut satırı arabirimi (Azure CLI)](../../cli-install-nodejs.md) çeşitli Azure Storage ile geliştirme ve yönetim görevlerini gerçekleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-108">In this guide, we'll explore how to use [Azure Command-Line Interface (Azure CLI)](../../cli-install-nodejs.md) to perform a variety of development and administration tasks with Azure Storage.</span></span> <span data-ttu-id="1ebc3-109">İndirin ve yükleyin veya bu kılavuzu kullanmadan önce en son Azure CLI yükseltme öneririz.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-109">We recommend that you download and install or upgrade to the latest Azure CLI before using this guide.</span></span>

<span data-ttu-id="1ebc3-110">Bu kılavuz, Azure Storage temel kavramlarını anladığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-110">This guide assumes that you understand the basic concepts of Azure Storage.</span></span> <span data-ttu-id="1ebc3-111">Kılavuz bir sayıda Azure Storage ile Azure CLI'ın kullanımını göstermek için betik sağlar.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-111">The guide provides a number of scripts to demonstrate the usage of the Azure CLI with Azure Storage.</span></span> <span data-ttu-id="1ebc3-112">Her komut dosyası çalıştırılmadan önce yapılandırmanıza göre komut dosyası değişkenleri güncelleştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-112">Be sure to update the script variables based on your configuration before running each script.</span></span>

> [!NOTE]
> <span data-ttu-id="1ebc3-113">Kılavuzu Klasik depolama hesapları için Azure CLI komut ve komut dosyası örnekler verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-113">The guide provides the Azure CLI command and script examples for classic storage accounts.</span></span> <span data-ttu-id="1ebc3-114">Bkz: [Mac, Linux ve Windows Azure kaynak yönetimi için Azure CLI kullanarak](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) Resource Manager depolama hesapları için Azure CLI komutları için.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-114">See [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) for Azure CLI commands for Resource Manager storage accounts.</span></span>
>
>

[!INCLUDE [storage-cli-versions](../../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-the-azure-cli-in-5-minutes"></a><span data-ttu-id="1ebc3-115">5 dakika içinde Azure Storage ve Azure CLI kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="1ebc3-115">Get started with Azure Storage and the Azure CLI in 5 minutes</span></span>
<span data-ttu-id="1ebc3-116">Bu kılavuzda Ubuntu örnekler için kullanılır, ancak diğer işletim sistemi platformlarını benzer şekilde gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-116">This guide uses Ubuntu for examples, but other OS platforms should perform similarly.</span></span>

<span data-ttu-id="1ebc3-117">**Yeni Azure:** Microsoft Azure aboneliği ve bu abonelikle ilişkili bir Microsoft hesabı alın.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-117">**New to Azure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="1ebc3-118">Azure satın alma seçenekleri hakkında daha fazla bilgi için bkz: [ücretsiz deneme](https://azure.microsoft.com/pricing/free-trial/), [satın alma seçenekleri](https://azure.microsoft.com/pricing/purchase-options/), ve [üye teklifleri](https://azure.microsoft.com/pricing/member-offers/) (MSDN, Microsoft iş ortağı ağı ve, BizSpark üyeleri için ve diğer Microsoft programları).</span><span class="sxs-lookup"><span data-stu-id="1ebc3-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="1ebc3-119">Bkz: [Azure Active Directory'de (Azure AD) yönetici rolleri atama](https://msdn.microsoft.com/library/azure/hh531793.aspx) Azure abonelikleri hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="1ebc3-120">**Microsoft Azure aboneliği ve hesabı oluşturduktan sonra:**</span><span class="sxs-lookup"><span data-stu-id="1ebc3-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="1ebc3-121">Özetlenen yönergeleri izleyerek Azure CLI yükleyip [Azure CLI yükleme](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="1ebc3-121">Download and install the Azure CLI following the instructions outlined in [Install the Azure CLI](../../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="1ebc3-122">Azure CLI yüklendikten sonra Azure CLI komutlara erişmek için azure komut, komut satırı arabiriminden (Bash, Terminal, komut istemi) kullanmanız mümkün olacaktır.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-122">Once the Azure CLI has been installed, you will be able to use the azure command from your command-line interface (Bash, Terminal, Command prompt) to access the Azure CLI commands.</span></span> <span data-ttu-id="1ebc3-123">Tür _azure_ komutunu ve aşağıdaki çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-123">Type the _azure_ command and you should see the following output.</span></span>

    ![Azure komut çıktısı](./media/storage-azure-cli/azure_command.png)   
3. <span data-ttu-id="1ebc3-125">Komut satırı arabirimini yazın `azure storage` tüm azure depolama komutları listelemek ve işlevlerin bir ilk izlenim Azure CLI almak için sağlar.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-125">In the command-line interface, type `azure storage` to list out all the azure storage commands and get a first impression of the functionalities the Azure CLI provides.</span></span> <span data-ttu-id="1ebc3-126">Komut adı ile yazabilirsiniz **-h** parametresi (örneğin, `azure storage share create -h`) komut sözdizimi ayrıntılarını görmek için.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-126">You can type command name with **-h** parameter (for example, `azure storage share create -h`) to see details of command syntax.</span></span>
4. <span data-ttu-id="1ebc3-127">Şimdi, Azure depolama alanına erişmek için temel Azure CLI komutları gösterir basit bir komut dosyası sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-127">Now, we'll give you a simple script that shows basic Azure CLI commands to access Azure Storage.</span></span> <span data-ttu-id="1ebc3-128">Komut dosyası, depolama hesabı ve anahtarı için iki değişkenleri ayarlamak için ilk isteyecektir.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-128">The script will first ask you to set two variables for your storage account and key.</span></span> <span data-ttu-id="1ebc3-129">Ardından, betik yeni bir kapsayıcı bu yeni depolama hesabı oluşturun ve varolan bir görüntü dosyası (blob) kapsayıcıya karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-129">Then, the script will create a new container in this new storage account and upload an existing image file (blob) to that container.</span></span> <span data-ttu-id="1ebc3-130">Komut dosyası bu kapsayıcıdaki tüm blob'lara listeler sonra yerel bilgisayarda var olan hedef dizinine görüntü dosyasını indirir.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-130">After the script lists all blobs in that container, it will download the image file to the destination directory which exists on the local computer.</span></span>

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating the container..."
    azure storage container create $container_name

    echo "Uploading the image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing the blobs..."
    azure storage blob list $container_name

    echo "Downloading the image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. <span data-ttu-id="1ebc3-131">Yerel bilgisayarınızda, tercih edilen metin düzenleyicisi (örneğin VIM) açın.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-131">In your local computer, open your preferred text editor (vim for example).</span></span> <span data-ttu-id="1ebc3-132">Yukarıdaki komut, metin düzenleyicisi yazın.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-132">Type the above script into your text editor.</span></span>
6. <span data-ttu-id="1ebc3-133">Şimdi, yapılandırma ayarlarınızı temel alan komut dosyası değişkenleri güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-133">Now, you need to update the script variables based on your configuration settings.</span></span>

   * <span data-ttu-id="1ebc3-134">**< Storage_account_name >** komut dosyasında verilen ad kullanın veya depolama hesabınız için yeni bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-134">**<storage_account_name>** Use the given name in the script or enter a new name for your storage account.</span></span> <span data-ttu-id="1ebc3-135">**Önemli:** depolama hesabı adının Azure'da benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-135">**Important:** The name of the storage account must be unique in Azure.</span></span> <span data-ttu-id="1ebc3-136">Çok küçük olmalıdır!</span><span class="sxs-lookup"><span data-stu-id="1ebc3-136">It must be lowercase, too!</span></span>
   * <span data-ttu-id="1ebc3-137">**< Storage_account_key >** , depolama hesabının erişim anahtarı.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-137">**<storage_account_key>** The access key of your storage account.</span></span>
   * <span data-ttu-id="1ebc3-138">**< Container_name >** komut dosyasında verilen ad kullanın veya, kapsayıcı için yeni bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-138">**<container_name>** Use the given name in the script or enter a new name for your container.</span></span>
   * <span data-ttu-id="1ebc3-139">**< İmage_to_upload >** , yerel bilgisayarınızda bir resim yolu gibi girin: "~ / images/HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="1ebc3-139">**<image_to_upload>** Enter a path to a picture on your local computer, such as: "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="1ebc3-140">**< Destination_folder >** gibi Azure Storage'dan indirilen dosyaları depolamak için bir yerel dizinin yolunu girin: "~/downloadImages".</span><span class="sxs-lookup"><span data-stu-id="1ebc3-140">**<destination_folder>** Enter a path to a local directory to store files downloaded from Azure Storage, such as: "~/downloadImages".</span></span>
7. <span data-ttu-id="1ebc3-141">VIM gerekli değişkenlerde güncelleştirdikten sonra tuş bileşimlerini basın `ESC`, `:`, `wq!` komut dosyasını kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-141">After you've updated the necessary variables in vim, press key combinations `ESC`, `:`, `wq!` to save the script.</span></span>
8. <span data-ttu-id="1ebc3-142">Bu komut dosyasını çalıştırmak için betik dosyası adı bash konsolunda yazın.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-142">To run this script, simply type the script file name in the bash console.</span></span> <span data-ttu-id="1ebc3-143">Bu betik çalıştıktan sonra indirilen görüntü dosyasını içeren bir yerel hedef klasör olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-143">After this script runs, you should have a local destination folder that includes the downloaded image file.</span></span> <span data-ttu-id="1ebc3-144">Aşağıdaki ekran görüntüsünde bir örnek çıkış şunları gösterir:</span><span class="sxs-lookup"><span data-stu-id="1ebc3-144">The following screenshot shows an example output:</span></span>

<span data-ttu-id="1ebc3-145">Betik çalıştıktan sonra indirilen görüntü dosyasını içeren bir yerel hedef klasör olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-145">After the script runs, you should have a local destination folder that includes the downloaded image file.</span></span>

## <a name="manage-storage-accounts-with-the-azure-cli"></a><span data-ttu-id="1ebc3-146">Depolama hesaplarını Azure CLI ile yönetme</span><span class="sxs-lookup"><span data-stu-id="1ebc3-146">Manage storage accounts with the Azure CLI</span></span>
### <a name="connect-to-your-azure-subscription"></a><span data-ttu-id="1ebc3-147">Azure aboneliğinize bağlanma</span><span class="sxs-lookup"><span data-stu-id="1ebc3-147">Connect to your Azure subscription</span></span>
<span data-ttu-id="1ebc3-148">Depolama komutların çoğu Azure aboneliği çalışır ancak Azure CLI üzerinden aboneliğinize bağlanmak için önerilir.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-148">While most of the storage commands will work without an Azure subscription, we recommend you to connect to your subscription from the Azure CLI.</span></span> <span data-ttu-id="1ebc3-149">Aboneliğiniz ile birlikte çalışmak için Azure CLI yapılandırmak için adımları [Azure clı'dan Azure aboneliğine Bağlan](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="1ebc3-149">To configure the Azure CLI to work with your subscription, follow the steps in [Connect to an Azure subscription from the Azure CLI](../../xplat-cli-connect.md).</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="1ebc3-150">Yeni depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ebc3-150">Create a new storage account</span></span>
<span data-ttu-id="1ebc3-151">Azure depolama kullanan bir depolama hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-151">To use Azure storage, you will need a storage account.</span></span> <span data-ttu-id="1ebc3-152">Aboneliğinize bağlanmak için bilgisayarınızı yapılandırdıktan sonra yeni bir Azure depolama hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-152">You can create a new Azure storage account after you have configured your computer to connect to your subscription.</span></span>

```azurecli
azure storage account create <account_name>
```

<span data-ttu-id="1ebc3-153">Depolama hesabınızın adını uzunluğu 3 ile 24 karakter arasında olmalı ve sayı ve yalnızca küçük harf kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-153">The name of your storage account must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a><span data-ttu-id="1ebc3-154">Ortam değişkenleri varsayılan bir Azure depolama hesabı ayarlama</span><span class="sxs-lookup"><span data-stu-id="1ebc3-154">Set a default Azure storage account in environment variables</span></span>
<span data-ttu-id="1ebc3-155">Aboneliğinizde birden çok depolama hesabı olabilir.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-155">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="1ebc3-156">Bunlardan birini seçin ve aynı oturum tüm depolama komutları için ortam değişkenleri içindeki ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-156">You can choose one of them and set it in the environment variables for all the storage commands in the same session.</span></span> <span data-ttu-id="1ebc3-157">Bu depolama hesabı belirtmeden Azure CLI depolama komutlarını çalıştırın ve açıkça anahtar sağlar.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-157">This enables you to run the Azure CLI storage commands without specifying the storage account and key explicitly.</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="1ebc3-158">Başka bir yolu varsayılan depolama hesabı bağlantı dizesi kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-158">Another way to set a default storage account is using connection string.</span></span> <span data-ttu-id="1ebc3-159">İlk olarak bağlantı dizesini komutla alın:</span><span class="sxs-lookup"><span data-stu-id="1ebc3-159">Firstly get the connection string by command:</span></span>

```azurecli
azure storage account connectionstring show <account_name>
```

<span data-ttu-id="1ebc3-160">Ardından çıktı bağlantı dizesini kopyalayın ve ortam değişkenine ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="1ebc3-160">Then copy the output connection string and set it to environment variable:</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a><span data-ttu-id="1ebc3-161">Oluşturma ve BLOB'ları yönetme</span><span class="sxs-lookup"><span data-stu-id="1ebc3-161">Create and manage blobs</span></span>
<span data-ttu-id="1ebc3-162">Azure Blob Depolama, büyük miktarlarda herhangi bir yere HTTP veya HTTPS aracılığıyla erişilebilen metin veya ikili veriler gibi yapılandırılmamış verileri depolamak için bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-162">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="1ebc3-163">Bu bölümde, zaten Azure Blob Depolama kavramlarını olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-163">This section assumes that you are already familiar with the Azure Blob storage concepts.</span></span> <span data-ttu-id="1ebc3-164">Ayrıntılı bilgi için bkz: [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../blobs/storage-dotnet-how-to-use-blobs.md) ve [Blob hizmeti kavramları](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ebc3-164">For detailed information, see [Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="1ebc3-165">Bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ebc3-165">Create a container</span></span>
<span data-ttu-id="1ebc3-166">Azure depolama her blob bir kapsayıcıda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-166">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="1ebc3-167">Özel bir kapsayıcı kullanılarak oluşturabilirsiniz `azure storage container create` komutu:</span><span class="sxs-lookup"><span data-stu-id="1ebc3-167">You can create a private container using the `azure storage container create` command:</span></span>

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> <span data-ttu-id="1ebc3-168">Anonim okuma erişimini üç düzeyi vardır: **kapalı**, **Blob**, ve **kapsayıcı**.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-168">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="1ebc3-169">Bloblar için anonim erişimi engellemek için izni parametre kümesini **devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-169">To prevent anonymous access to blobs, set the Permission parameter to **Off**.</span></span> <span data-ttu-id="1ebc3-170">Varsayılan olarak yeni kapsayıcı özeldir ve yalnızca hesap sahibi tarafından erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-170">By default, the new container is private and can be accessed only by the account owner.</span></span> <span data-ttu-id="1ebc3-171">Anonim izin vermek için herkese okuma erişimi blob kaynaklarına ancak kapsayıcı meta verileri için veya kapsayıcıdaki blobları listesine izin parametre kümesine **Blob**.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-171">To allow anonymous public read access to blob resources, but not to container metadata or to the list of blobs in the container, set the Permission parameter to **Blob**.</span></span> <span data-ttu-id="1ebc3-172">Kaynaklar, kapsayıcı meta verileri ve kapsayıcıdaki blobları listesi blob tam ortak okuma erişimi sağlamak üzere izin parametre kümesini **kapsayıcı**.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-172">To allow full public read access to blob resources, container metadata, and the list of blobs in the container, set the Permission parameter to **Container**.</span></span> <span data-ttu-id="1ebc3-173">Daha fazla bilgi için bkz: [kapsayıcılar ve bloblar için anonim okuma erişimini yönetme](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="1ebc3-173">For more information, see [Manage anonymous read access to containers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>
>
>

### <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="1ebc3-174">Bir kapsayıcıya bir blob yükleme</span><span class="sxs-lookup"><span data-stu-id="1ebc3-174">Upload a blob into a container</span></span>
<span data-ttu-id="1ebc3-175">Azure Blob Storage blok blobları ve sayfa bloblarını destekler.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-175">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="1ebc3-176">Daha fazla bilgi için bkz: [anlama blok Blobları, ekleme Blobları ve sayfa Bloblarını](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ebc3-176">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="1ebc3-177">BLOB'ları bir kapsayıcıya karşıya yüklemek için kullanabileceğiniz `azure storage blob upload`.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-177">To upload blobs in to a container, you can use the `azure storage blob upload`.</span></span> <span data-ttu-id="1ebc3-178">Varsayılan olarak, bu komutu bir blok blobuna yerel dosyaları karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-178">By default, this command uploads the local files to a block blob.</span></span> <span data-ttu-id="1ebc3-179">Blob türü belirtmek için kullanabileceğiniz `--blobtype` parametresi.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-179">To specify the type for the blob, you can use the `--blobtype` parameter.</span></span>

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a><span data-ttu-id="1ebc3-180">Kapsayıcıdan BLOB indirmek</span><span class="sxs-lookup"><span data-stu-id="1ebc3-180">Download blobs from a container</span></span>
<span data-ttu-id="1ebc3-181">Aşağıdaki örnek, bir kapsayıcıdan BLOB indirmek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-181">The following example demonstrates how to download blobs from a container.</span></span>

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a><span data-ttu-id="1ebc3-182">BLOB kopyalama</span><span class="sxs-lookup"><span data-stu-id="1ebc3-182">Copy blobs</span></span>
<span data-ttu-id="1ebc3-183">Blobları, depolama hesaplarıyla bölgeler içinde veya bunların arasında zaman uyumsuz olarak kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-183">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="1ebc3-184">Aşağıdaki örnekte blobların bir depolama hesabından diğerine nasıl kopyalandığı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-184">The following example demonstrates how to copy blobs from one storage account to another.</span></span> <span data-ttu-id="1ebc3-185">Bu örnekte BLOB'lar nerede genel olarak, bir kapsayıcı oluşturuyoruz anonim olarak erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-185">In this sample we create a container where blobs are publicly, anonymously accessible.</span></span>

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

<span data-ttu-id="1ebc3-186">Bu örnek bir zaman uyumsuz kopya gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-186">This sample performs an asynchronous copy.</span></span> <span data-ttu-id="1ebc3-187">Çalıştırarak her kopyalama işlemi durumunu izleyebilirsiniz `azure storage blob copy show` işlemi.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-187">You can monitor the status of each copy operation by running the `azure storage blob copy show` operation.</span></span>

<span data-ttu-id="1ebc3-188">Kaynak URL kopyalama işlemi sağlanan Not gerekir genel olarak erişilebilir ya da bir SAS (paylaşılan erişim imzası) belirteci içerir.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-188">Note that the source URL provided for the copy operation must either be publicly accessible, or include a SAS (shared access signature) token.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="1ebc3-189">Blob silme</span><span class="sxs-lookup"><span data-stu-id="1ebc3-189">Delete a blob</span></span>
<span data-ttu-id="1ebc3-190">Bir blobu silmek için kullanın komutu altında:</span><span class="sxs-lookup"><span data-stu-id="1ebc3-190">To delete a blob, use the below command:</span></span>

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="1ebc3-191">Oluşturun ve dosya paylaşımlarını yönetmek</span><span class="sxs-lookup"><span data-stu-id="1ebc3-191">Create and manage file shares</span></span>
<span data-ttu-id="1ebc3-192">Azure File storage standart SMB protokolünü kullanan uygulamalar için paylaşılan depolama alanı sağlar.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-192">Azure File storage offers shared storage for applications using the standard SMB protocol.</span></span> <span data-ttu-id="1ebc3-193">Microsoft Azure sanal makineler ve bulut Hizmetleri yanı sıra, şirket içi uygulamalara bağlı paylaşımlar üzerinden dosya verileri paylaşabilir.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-193">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="1ebc3-194">Dosya paylaşımları ve dosya verilerini Azure CLI aracılığıyla yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-194">You can manage file shares and file data via the Azure CLI.</span></span> <span data-ttu-id="1ebc3-195">Azure File storage hakkında daha fazla bilgi için bkz: [Windows Azure File storage ile çalışmaya başlama](../storage-dotnet-how-to-use-files.md) veya [Azure File storage'ı Linux ile kullanma konusunda](../storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1ebc3-195">For more information on Azure File storage, see [Get started with Azure File storage on Windows](../storage-dotnet-how-to-use-files.md) or [How to use Azure File storage with Linux](../storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="1ebc3-196">Dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ebc3-196">Create a file share</span></span>
<span data-ttu-id="1ebc3-197">Bir Azure dosya paylaşımı azure'da SMB dosya paylaşımı değil.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-197">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="1ebc3-198">Tüm dizin ve dosyaların bir dosya paylaşımı oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-198">All directories and files must be created in a file share.</span></span> <span data-ttu-id="1ebc3-199">Bir hesapta sınırsız sayıda paylaşım olabilir ve bir paylaşım dosyaları, depolama hesabının kapasite sınırlarına kadar sınırsız sayıda depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-199">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up to the capacity limits of the storage account.</span></span> <span data-ttu-id="1ebc3-200">Aşağıdaki örnek adlı bir dosya paylaşımı oluşturur **paylaşımım**.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-200">The following example creates a file share named **myshare**.</span></span>

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="1ebc3-201">Dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ebc3-201">Create a directory</span></span>
<span data-ttu-id="1ebc3-202">Bir dizin, bir Azure dosya paylaşımı için isteğe bağlı hiyerarşik bir yapı sağlar.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-202">A directory provides an optional hierarchical structure for an Azure file share.</span></span> <span data-ttu-id="1ebc3-203">Aşağıdaki örnek adlı bir dizin oluşturur **Dizinim** dosya paylaşımında.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-203">The following example creates a directory named **myDir** in the file share.</span></span>

```azurecli
azure storage directory create myshare myDir
```

<span data-ttu-id="1ebc3-204">Bu dizin yolu, birden çok düzeyi içerebilir Not *örneğin*, **bir / b**.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-204">Note that directory path can include multiple levels, *e.g.*, **a/b**.</span></span> <span data-ttu-id="1ebc3-205">Ancak, tüm üst dizinleri var olduğundan emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-205">However, you must ensure that all parent directories exist.</span></span> <span data-ttu-id="1ebc3-206">Örneğin, yol **bir / b**, dizin oluşturmanız gerekir **bir** ilk olarak, ardından dizin oluşturma **b**.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-206">For example, for path **a/b**, you must create directory **a** first, then create directory **b**.</span></span>

### <a name="upload-a-local-file-to-directory"></a><span data-ttu-id="1ebc3-207">Dizine yerel bir dosya karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="1ebc3-207">Upload a local file to directory</span></span>
<span data-ttu-id="1ebc3-208">Aşağıdaki örnekte bir dosyadan yükler **~/temp/samplefile.txt** için **Dizinim** dizin.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-208">The following example uploads a file from **~/temp/samplefile.txt** to the **myDir** directory.</span></span> <span data-ttu-id="1ebc3-209">Dosya yolunu yerel makinenizdeki geçerli bir dosyaya işaret şekilde düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="1ebc3-209">Edit the file path so that it points to a valid file on your local machine:</span></span>

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

<span data-ttu-id="1ebc3-210">Bir dosya paylaşımında boyutu 1 TB'ye kadar olabileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-210">Note that a file in the share can be up to 1 TB in size.</span></span>

### <a name="list-the-files-in-the-share-root-or-directory"></a><span data-ttu-id="1ebc3-211">Dosya paylaşım kök veya dizinde Listele</span><span class="sxs-lookup"><span data-stu-id="1ebc3-211">List the files in the share root or directory</span></span>
<span data-ttu-id="1ebc3-212">Bir paylaşım kök veya aşağıdaki komutu kullanarak bir dizinde alt dizinlerin ve dosyaların listeleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1ebc3-212">You can list the files and subdirectories in a share root or a directory using the following command:</span></span>

```azurecli
azure storage file list myshare myDir
```

<span data-ttu-id="1ebc3-213">Dizin adı listeleme işlemi için isteğe bağlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-213">Note that the directory name is optional for the listing operation.</span></span> <span data-ttu-id="1ebc3-214">Atlanırsa, komut paylaşımının kök dizinin içeriğini listeler.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-214">If omitted, the command lists the contents of the root directory of the share.</span></span>

### <a name="copy-files"></a><span data-ttu-id="1ebc3-215">Dosyaları kopyalama</span><span class="sxs-lookup"><span data-stu-id="1ebc3-215">Copy files</span></span>
<span data-ttu-id="1ebc3-216">Azure CLI 0.9.8 sürümü ile başlayarak, bir dosyaya kopyalayabilirsiniz başka bir dosyaya, bir dosyayı bir bloba veya bir blobu bir dosyaya.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-216">Beginning with version 0.9.8 of Azure CLI, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="1ebc3-217">Aşağıda CLI komutları kullanarak bu kopyalama işlemlerini gerçekleştirmek nasıl göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-217">Below we demonstrate how to perform these copy operations using CLI commands.</span></span> <span data-ttu-id="1ebc3-218">Yeni dizine dosya kopyalamak için:</span><span class="sxs-lookup"><span data-stu-id="1ebc3-218">To copy a file to the new directory:</span></span>

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

<span data-ttu-id="1ebc3-219">Bir blob dosya dizinine kopyalamak için:</span><span class="sxs-lookup"><span data-stu-id="1ebc3-219">To copy a blob to a file directory:</span></span>

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a><span data-ttu-id="1ebc3-220">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="1ebc3-220">Next Steps</span></span>

<span data-ttu-id="1ebc3-221">Burada depolama kaynaklarla çalışmak için Azure CLI 1.0 komut başvurusu bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1ebc3-221">You can find Azure CLI 1.0 command reference for working with Storage resources here:</span></span>

* [<span data-ttu-id="1ebc3-222">Kaynak Yöneticisi modunda Azure CLI komutları</span><span class="sxs-lookup"><span data-stu-id="1ebc3-222">Azure CLI commands in Resource Manager mode</span></span>](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [<span data-ttu-id="1ebc3-223">Azure Hizmet Yönetimi modunda Azure CLI komutları</span><span class="sxs-lookup"><span data-stu-id="1ebc3-223">Azure CLI commands in Azure Service Management mode</span></span>](../../cli-install-nodejs.md)

<span data-ttu-id="1ebc3-224">Ayrıca denemek ister [Azure CLI 2.0](../storage-azure-cli.md), Resource Manager dağıtım modeli ile kullanmak için Python içinde yazılmış bizim nesil CLI.</span><span class="sxs-lookup"><span data-stu-id="1ebc3-224">You may also like to try the [Azure CLI 2.0](../storage-azure-cli.md), our next-generation CLI written in Python, for use with the Resource Manager deployment model.</span></span>
