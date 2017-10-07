---
title: "Azure komut satırı 2.0 aaaUse arabirimi tooget Azure Data Lake Store ile çalışmaya | Microsoft Docs"
description: "Temel işlemleri gerçekleştirmek ve Azure platformlar arası komut satırı 2.0 toocreate bir Data Lake Store hesabı kullanın"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 4ffa0f4a-1cca-46ac-803d-1fc8538c685b
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 374dcd6cdbc13ad19f6c65502329986ecae60ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a><span data-ttu-id="00423-103">Azure CLI 2.0 kullanarak Azure Data Lake Store ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="00423-103">Get started with Azure Data Lake Store using Azure CLI 2.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="00423-104">Portal</span><span class="sxs-lookup"><span data-stu-id="00423-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="00423-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="00423-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="00423-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="00423-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="00423-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="00423-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="00423-108">REST API</span><span class="sxs-lookup"><span data-stu-id="00423-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="00423-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="00423-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="00423-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="00423-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="00423-111">Python</span><span class="sxs-lookup"><span data-stu-id="00423-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="00423-112">Bir Azure Data Lake toouse Azure CLI 2.0 toocreate nasıl depolamak öğrenin hesap ve gibi klasör oluşturma karşıya yükleme ve veri dosyalarını indirme temel işlemleri gerçekleştirmek, vb., hesabınızı silme. Data Lake Store hakkında daha fazla bilgi için bkz. [Data Lake Store'a Genel Bakış](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="00423-112">Learn how toouse Azure CLI 2.0 toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="00423-113">Hello Azure CLI 2.0 Azure kaynaklarını yönetmek için Azure'nın yeni komut satırı deneyimidir.</span><span class="sxs-lookup"><span data-stu-id="00423-113">hello Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="00423-114">MacOS, Linux ve Windows’da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="00423-114">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="00423-115">Daha fazla bilgi edinmek için bkz. [Azure CLI 2.0 aracına genel bakış](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="00423-115">For more information, see [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview).</span></span> <span data-ttu-id="00423-116">Hello de bakabilirsiniz [Azure Data Lake deposu CLI 2.0 başvurusu](https://docs.microsoft.com/cli/azure/dls) komutlar ve söz dizimi tam bir listesi.</span><span class="sxs-lookup"><span data-stu-id="00423-116">You can also look at hello [Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls) for a complete list of commands and syntax.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="00423-117">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="00423-117">Prerequisites</span></span>
<span data-ttu-id="00423-118">Bu makaleye başlamadan önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="00423-118">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="00423-119">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="00423-119">**An Azure subscription**.</span></span> <span data-ttu-id="00423-120">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="00423-120">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="00423-121">**Azure CLI 2.0** - Yönergeler için kz. [Azure CLI 2.0 aracını yükleme](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="00423-121">**Azure CLI 2.0** - See [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) for instructions.</span></span>

## <a name="authentication"></a><span data-ttu-id="00423-122">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="00423-122">Authentication</span></span>

<span data-ttu-id="00423-123">Bu makalede Data Lake Store için son kullanıcı olarak oturum açtığınız daha basit bir kimlik doğrulama yaklaşımı kullanılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="00423-123">This article uses a simpler authentication approach with Data Lake Store where you log in as an end-user user.</span></span> <span data-ttu-id="00423-124">Merhaba erişim düzeyi tooData Lake Store hesabı ve dosya sistemi, kullanıcı oturum hello hello erişim düzeyi sonra tabidir.</span><span class="sxs-lookup"><span data-stu-id="00423-124">hello access level tooData Lake Store account and file system is then governed by hello access level of hello logged in user.</span></span> <span data-ttu-id="00423-125">Ancak, diğer yaklaşım vardır Data Lake Store ile iyi tooauthenticate olarak olan **son kullanıcı kimlik doğrulaması** veya **hizmeti için kimlik doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="00423-125">However, there are other approaches as well tooauthenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="00423-126">Yönergeler ve hakkında daha fazla bilgi için tooauthenticate, bkz: [son kullanıcı kimlik doğrulaması](data-lake-store-end-user-authenticate-using-active-directory.md) veya [hizmeti için kimlik doğrulama](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="00423-126">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>


## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="00423-127">Azure aboneliği tooyour oturum</span><span class="sxs-lookup"><span data-stu-id="00423-127">Log in tooyour Azure subscription</span></span>

1. <span data-ttu-id="00423-128">Azure aboneliğinizde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="00423-128">Log into your Azure subscription.</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="00423-129">Kod toouse hello sonraki adımda alın.</span><span class="sxs-lookup"><span data-stu-id="00423-129">You get a code toouse in hello next step.</span></span> <span data-ttu-id="00423-130">Bir web tarayıcısı tooopen hello sayfa https://aka.ms/devicelogin kullanın ve hello kod tooauthenticate girin.</span><span class="sxs-lookup"><span data-stu-id="00423-130">Use a web browser tooopen hello page https://aka.ms/devicelogin and enter hello code tooauthenticate.</span></span> <span data-ttu-id="00423-131">Kimlik bilgilerinizi kullanarak istendiğinde toolog var.</span><span class="sxs-lookup"><span data-stu-id="00423-131">You are prompted toolog in using your credentials.</span></span>

2. <span data-ttu-id="00423-132">Oturum açtığında hello pencere listeleri tüm hesabınızla ilişkilendirilen Azure aboneliklerinin hello.</span><span class="sxs-lookup"><span data-stu-id="00423-132">Once you log in, hello window lists all hello Azure subscriptions that are associated with your account.</span></span> <span data-ttu-id="00423-133">Komut toouse belirli bir aboneliği aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="00423-133">Use hello following command toouse a specific subscription.</span></span>
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="00423-134">Azure Data Lake Store hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="00423-134">Create an Azure Data Lake Store account</span></span>

1. <span data-ttu-id="00423-135">Yeni bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="00423-135">Create a new resource group.</span></span> <span data-ttu-id="00423-136">Komutu aşağıdaki hello hello toouse istediğiniz parametre değerlerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="00423-136">In hello following command, provide hello parameter values you want toouse.</span></span> <span data-ttu-id="00423-137">Merhaba konum adı boşluk içeriyorsa, tırnak işaretleri içine alın.</span><span class="sxs-lookup"><span data-stu-id="00423-137">If hello location name contains spaces, put it in quotes.</span></span> <span data-ttu-id="00423-138">Örneğin, "Doğu ABD 2".</span><span class="sxs-lookup"><span data-stu-id="00423-138">For example "East US 2".</span></span> 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. <span data-ttu-id="00423-139">Merhaba Data Lake Store hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="00423-139">Create hello Data Lake Store account.</span></span>
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="00423-140">Data Lake Store hesabında klasör oluşturma</span><span class="sxs-lookup"><span data-stu-id="00423-140">Create folders in a Data Lake Store account</span></span>

<span data-ttu-id="00423-141">Azure Data Lake Store hesabı toomanage altında klasörleri oluşturun ve veri depolayın.</span><span class="sxs-lookup"><span data-stu-id="00423-141">You can create folders under your Azure Data Lake Store account toomanage and store data.</span></span> <span data-ttu-id="00423-142">Adlı bir klasör komutu toocreate aşağıdaki kullanım hello **mynewfolder** hello Data Lake Store hello kökü.</span><span class="sxs-lookup"><span data-stu-id="00423-142">Use hello following command toocreate a folder called **mynewfolder** at hello root of hello Data Lake Store.</span></span>

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> <span data-ttu-id="00423-143">Merhaba `--folder` parametre sağlar hello komutu bir klasör oluşturur.</span><span class="sxs-lookup"><span data-stu-id="00423-143">hello `--folder` parameter ensures that hello command creates a folder.</span></span> <span data-ttu-id="00423-144">Bu parametre mevcut değilse hello komut hello hello Data Lake Store hesabı kökünde mynewfolder adlı boş bir dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="00423-144">If this parameter is not present, hello command creates an empty file called mynewfolder at hello root of hello Data Lake Store account.</span></span>
> 
>

## <a name="upload-data-tooa-data-lake-store-account"></a><span data-ttu-id="00423-145">Veri tooa Data Lake Store hesabı karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="00423-145">Upload data tooa Data Lake Store account</span></span>

<span data-ttu-id="00423-146">Veri tooData Lake deposu hello hesap içinde oluşturduğunuz doğrudan hello kök düzeyinde veya tooa klasöründe karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00423-146">You can upload data tooData Lake Store directly at hello root level or tooa folder that you created within hello account.</span></span> <span data-ttu-id="00423-147">Merhaba parçacıkları göstermek nasıl tooupload bazı örnek veri toohello klasörü (**mynewfolder**) hello önceki bölümde oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="00423-147">hello snippets below demonstrate how tooupload some sample data toohello folder (**mynewfolder**) you created in hello previous section.</span></span>

<span data-ttu-id="00423-148">Bazı örnek veri tooupload için arıyorsanız, hello alabilirsiniz **Ambulance Data** hello klasöründen [Azure Data Lake Git deposu](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="00423-148">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="00423-149">Merhaba dosyasını indirin ve C:\sampledata\ gibi bilgisayarınızdaki yerel bir klasörde saklayın.</span><span class="sxs-lookup"><span data-stu-id="00423-149">Download hello file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> <span data-ttu-id="00423-150">Merhaba hedef için hello dosya adını içeren hello tam yolunu belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="00423-150">For hello destination, you must specify hello complete path including hello file name.</span></span>
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a><span data-ttu-id="00423-151">Data Lake Store hesabındaki dosyaları listeleme</span><span class="sxs-lookup"><span data-stu-id="00423-151">List files in a Data Lake Store account</span></span>

<span data-ttu-id="00423-152">Aşağıdaki komut toolist hello dosyaları bir Data Lake Store hesabındaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="00423-152">Use hello following command toolist hello files in a Data Lake Store account.</span></span>

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

<span data-ttu-id="00423-153">Merhaba çıktısını benzer toohello aşağıdaki gibi olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="00423-153">hello output of this should be similar toohello following:</span></span>

    [
        {
            "accessTime": 1491323529542,
            "aclBit": false,
            "blockSize": 268435456,
            "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "length": 1589881,
            "modificationTime": 1491323531638,
            "msExpirationTime": 0,
            "name": "mynewfolder/vehicle1_09142014.csv",
            "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "pathSuffix": "vehicle1_09142014.csv",
            "permission": "770",
            "replication": 1,
            "type": "FILE"
        }
    ]

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a><span data-ttu-id="00423-154">Data Lake Store hesabındaki verileri yeniden adlandırma, indirme ve silme</span><span class="sxs-lookup"><span data-stu-id="00423-154">Rename, download, and delete data from a Data Lake Store account</span></span> 

* <span data-ttu-id="00423-155">**bir dosya toorename**, komutu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="00423-155">**toorename a file**, use hello following command:</span></span>
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* <span data-ttu-id="00423-156">**bir dosya toodownload**, komutu aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="00423-156">**toodownload a file**, use hello following command.</span></span> <span data-ttu-id="00423-157">Önceden belirttiğiniz hello hedef yolu var olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="00423-157">Make sure hello destination path you specify already exists.</span></span>
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > <span data-ttu-id="00423-158">henüz yoksa hello komut hello hedef klasörü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="00423-158">hello command creates hello destination folder if it does not exist.</span></span>
    > 
    >

* <span data-ttu-id="00423-159">**bir dosya toodelete**, komutu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="00423-159">**toodelete a file**, use hello following command:</span></span>
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    <span data-ttu-id="00423-160">Toodelete hello klasörünün istiyorsanız **mynewfolder** ve hello dosya **vehicle1_09142014_copy.csv** birlikte bir komut kullanın hello--parametre recurse</span><span class="sxs-lookup"><span data-stu-id="00423-160">If you want toodelete hello folder **mynewfolder** and hello file **vehicle1_09142014_copy.csv** together in one command, use hello --recurse parameter</span></span>

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a><span data-ttu-id="00423-161">Data Lake Store hesabı için izin ve ACL’ler ile çalışma</span><span class="sxs-lookup"><span data-stu-id="00423-161">Work with permissions and ACLs for a Data Lake Store account</span></span>

<span data-ttu-id="00423-162">Bu bölümde hakkında bilgi edinin toomanage ACL'ler Azure CLI 2.0 kullanarak ve izinleri.</span><span class="sxs-lookup"><span data-stu-id="00423-162">In this section you learn about how toomanage ACLs and permissions using Azure CLI 2.0.</span></span> <span data-ttu-id="00423-163">Azure Data Lake Store’da ACL’lerin nasıl uygulandığıyla ilgili ayrıntılı bir tartışma için bkz. [Azure Data Lake Store’da erişim denetimi](data-lake-store-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="00423-163">For a detailed discussion on how ACLs are implemented in Azure Data Lake Store, see [Access control in Azure Data Lake Store](data-lake-store-access-control.md).</span></span>

* <span data-ttu-id="00423-164">**bir dosya/klasör tooupdate hello sahibi**, komutu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="00423-164">**tooupdate hello owner of a file/folder**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="00423-165">**tooupdate hello dosya/klasör izinlerini**, komutu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="00423-165">**tooupdate hello permissions for a file/folder**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* <span data-ttu-id="00423-166">**belirli bir yol için tooget hello ACL'ler**, komutu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="00423-166">**tooget hello ACLs for a given path**, use hello following command:</span></span>

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    <span data-ttu-id="00423-167">Merhaba çıkış benzer toohello aşağıdaki gibi olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="00423-167">hello output should be similar toohello following:</span></span>

        {
            "entries": [
            "user::rwx",
            "group::rwx",
            "other::---"
          ],
          "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "permission": "770",
          "stickyBit": false
        }

* <span data-ttu-id="00423-168">**tooset bir ACL için bir giriş**, komutu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="00423-168">**tooset an entry for an ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* <span data-ttu-id="00423-169">**tooremove bir ACL için bir giriş**, komutu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="00423-169">**tooremove an entry for an ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="00423-170">**tooremove tüm bir varsayılan ACL**, komutu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="00423-170">**tooremove an entire default ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* <span data-ttu-id="00423-171">**Tüm varsayılan olmayan ACL tooremove**, komutu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="00423-171">**tooremove an entire non-default ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="00423-172">Data Lake Store hesabını silme</span><span class="sxs-lookup"><span data-stu-id="00423-172">Delete a Data Lake Store account</span></span>
<span data-ttu-id="00423-173">Komut toodelete bir Data Lake Store hesabı aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="00423-173">Use hello following command toodelete a Data Lake Store account.</span></span>

```azurecli
az dls account delete --account mydatalakestore
```

<span data-ttu-id="00423-174">İstendiğinde, girin **Y** toodelete hello hesabı.</span><span class="sxs-lookup"><span data-stu-id="00423-174">When prompted, enter **Y** toodelete hello account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00423-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="00423-175">Next steps</span></span>

* [<span data-ttu-id="00423-176">Azure Data Lake Store CLI 2.0 başvurusu</span><span class="sxs-lookup"><span data-stu-id="00423-176">Azure Data Lake Store CLI 2.0 reference</span></span>](https://docs.microsoft.com/cli/azure/dls)
* [<span data-ttu-id="00423-177">Data Lake Store'da verilerin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="00423-177">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="00423-178">Azure Data Lake Analytics'i Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="00423-178">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="00423-179">Azure HDInsight'ı Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="00423-179">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
