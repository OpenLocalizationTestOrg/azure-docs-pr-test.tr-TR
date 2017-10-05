---
title: "Azure komut satırı arabirimi 2.0 aracını kullanarak Azure Data Lake Store ile çalışmaya başlama | Microsoft Docs"
description: "Bir Data Lake Store hesabı oluşturmak ve temel işlemleri gerçekleştirmek için Azure platformlar arası komut satırı 2.0 aracını kullanma"
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
ms.openlocfilehash: ed78d25f2bac0a9996f1796ee503f31a36940977
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a><span data-ttu-id="1c069-103">Azure CLI 2.0 kullanarak Azure Data Lake Store ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="1c069-103">Get started with Azure Data Lake Store using Azure CLI 2.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1c069-104">Portal</span><span class="sxs-lookup"><span data-stu-id="1c069-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="1c069-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c069-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="1c069-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="1c069-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="1c069-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="1c069-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="1c069-108">REST API</span><span class="sxs-lookup"><span data-stu-id="1c069-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="1c069-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1c069-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="1c069-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="1c069-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="1c069-111">Python</span><span class="sxs-lookup"><span data-stu-id="1c069-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="1c069-112">Azure Data Lake Store hesabı oluşturma ve klasör oluşturma, veri dosyalarını karşıya yükleme ve indirme, hesabınızı silme gibi temel işlemleri gerçekleştirmek için Azure CLI 2.0 (Önizleme) aracının nasıl kullanılacağını öğrenin. Data Lake Store hakkında daha fazla bilgi için bkz. [Data Lake Store'a Genel Bakış](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1c069-112">Learn how to use Azure CLI 2.0 to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="1c069-113">Azure CLI 2.0, Azure kaynaklarını yönetmek için Azure tarafından sunulan yeni komut satırı deneyimidir.</span><span class="sxs-lookup"><span data-stu-id="1c069-113">The Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="1c069-114">MacOS, Linux ve Windows’da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1c069-114">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="1c069-115">Daha fazla bilgi edinmek için bkz. [Azure CLI 2.0 aracına genel bakış](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1c069-115">For more information, see [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview).</span></span> <span data-ttu-id="1c069-116">Tam komut ve söz dizimi listesi için [Azure Data Lake Store CLI 2.0 başvurusuna](https://docs.microsoft.com/cli/azure/dls) da bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c069-116">You can also look at the [Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls) for a complete list of commands and syntax.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="1c069-117">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1c069-117">Prerequisites</span></span>
<span data-ttu-id="1c069-118">Bu makaleye başlamadan önce aşağıdakilere sahip olmanız ve aşağıdaki işlemleri yapmış olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="1c069-118">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="1c069-119">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="1c069-119">**An Azure subscription**.</span></span> <span data-ttu-id="1c069-120">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1c069-120">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="1c069-121">**Azure CLI 2.0** - Yönergeler için kz. [Azure CLI 2.0 aracını yükleme](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1c069-121">**Azure CLI 2.0** - See [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) for instructions.</span></span>

## <a name="authentication"></a><span data-ttu-id="1c069-122">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="1c069-122">Authentication</span></span>

<span data-ttu-id="1c069-123">Bu makalede Data Lake Store için son kullanıcı olarak oturum açtığınız daha basit bir kimlik doğrulama yaklaşımı kullanılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1c069-123">This article uses a simpler authentication approach with Data Lake Store where you log in as an end-user user.</span></span> <span data-ttu-id="1c069-124">Data Lake Store hesabına ve dosya sistemine erişim düzeyi bu durumda oturum açmış kullanıcının erişim düzeyine göre yönetilir.</span><span class="sxs-lookup"><span data-stu-id="1c069-124">The access level to Data Lake Store account and file system is then governed by the access level of the logged in user.</span></span> <span data-ttu-id="1c069-125">Ancak, Data Lake Store kimlik doğrulaması için **son kullanıcı kimlik doğrulaması** veya **hizmetten hizmete kimlik doğrulama** şeklinde diğer yaklaşımlar da mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="1c069-125">However, there are other approaches as well to authenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="1c069-126">Kimlik doğrulaması gerçekleştirmeyle ilgili yönergeler ve daha fazla bilgi için [Son kullanıcı kimlik doğrulaması](data-lake-store-end-user-authenticate-using-active-directory.md) veya [Hizmetten hizmete kimlik doğrulaması](data-lake-store-authenticate-using-active-directory.md) bölümlerine göz atın.</span><span class="sxs-lookup"><span data-stu-id="1c069-126">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>


## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="1c069-127">Azure aboneliğinizde oturum açın</span><span class="sxs-lookup"><span data-stu-id="1c069-127">Log in to your Azure subscription</span></span>

1. <span data-ttu-id="1c069-128">Azure aboneliğinizde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1c069-128">Log into your Azure subscription.</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="1c069-129">Sonraki adımda kullanmak üzere bir kod alırsınız.</span><span class="sxs-lookup"><span data-stu-id="1c069-129">You get a code to use in the next step.</span></span> <span data-ttu-id="1c069-130">Kimliğinizi doğrulamak için bir web tarayıcısı kullanarak https://aka.ms/devicelogin adresine gidin ve kodu girin.</span><span class="sxs-lookup"><span data-stu-id="1c069-130">Use a web browser to open the page https://aka.ms/devicelogin and enter the code to authenticate.</span></span> <span data-ttu-id="1c069-131">Kimlik bilgilerinizi kullanarak oturum açmanız istenir.</span><span class="sxs-lookup"><span data-stu-id="1c069-131">You are prompted to log in using your credentials.</span></span>

2. <span data-ttu-id="1c069-132">Oturum açtığınızda, pencerede hesabınızla ilişkili tüm Azure abonelikleri listelenir.</span><span class="sxs-lookup"><span data-stu-id="1c069-132">Once you log in, the window lists all the Azure subscriptions that are associated with your account.</span></span> <span data-ttu-id="1c069-133">Belirli bir aboneliği kullanmak için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="1c069-133">Use the following command to use a specific subscription.</span></span>
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="1c069-134">Azure Data Lake Store hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1c069-134">Create an Azure Data Lake Store account</span></span>

1. <span data-ttu-id="1c069-135">Yeni bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1c069-135">Create a new resource group.</span></span> <span data-ttu-id="1c069-136">Aşağıdaki komut içinde kullanmak istediğiniz parametre değerlerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="1c069-136">In the following command, provide the parameter values you want to use.</span></span> <span data-ttu-id="1c069-137">Konum adı boşluk içeriyorsa adı tırnak işaretleri içine alın.</span><span class="sxs-lookup"><span data-stu-id="1c069-137">If the location name contains spaces, put it in quotes.</span></span> <span data-ttu-id="1c069-138">Örneğin, "Doğu ABD 2".</span><span class="sxs-lookup"><span data-stu-id="1c069-138">For example "East US 2".</span></span> 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. <span data-ttu-id="1c069-139">Data Lake Store hesabını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1c069-139">Create the Data Lake Store account.</span></span>
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="1c069-140">Data Lake Store hesabında klasör oluşturma</span><span class="sxs-lookup"><span data-stu-id="1c069-140">Create folders in a Data Lake Store account</span></span>

<span data-ttu-id="1c069-141">Veri depolamak ve yönetmek için Azure Data Lake Store hesabınızın altında klasör oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c069-141">You can create folders under your Azure Data Lake Store account to manage and store data.</span></span> <span data-ttu-id="1c069-142">Aşağıdaki komutu kullanarak Data Lake Store'un kökünde **mynewfolder** adlı bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1c069-142">Use the following command to create a folder called **mynewfolder** at the root of the Data Lake Store.</span></span>

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> <span data-ttu-id="1c069-143">`--folder` parametresi, komutun bir klasör oluşturmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="1c069-143">The `--folder` parameter ensures that the command creates a folder.</span></span> <span data-ttu-id="1c069-144">Bu parametre yoksa, komut tarafından Data Lake Store hesabının kökünde mynewfolder adlı boş bir dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1c069-144">If this parameter is not present, the command creates an empty file called mynewfolder at the root of the Data Lake Store account.</span></span>
> 
>

## <a name="upload-data-to-a-data-lake-store-account"></a><span data-ttu-id="1c069-145">Data Lake Store hesabına veri yükleme</span><span class="sxs-lookup"><span data-stu-id="1c069-145">Upload data to a Data Lake Store account</span></span>

<span data-ttu-id="1c069-146">Data Lake Store'a doğrudan kök düzeyinde veya hesap içinde oluşturduğunuz bir klasöre yüklenecek şekilde veri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c069-146">You can upload data to Data Lake Store directly at the root level or to a folder that you created within the account.</span></span> <span data-ttu-id="1c069-147">Aşağıdaki kod parçacıkları, birtakım örnek verilerin önceki bölümde oluşturduğunuz klasöre (**mynewfolder**) nasıl yükleneceğini göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="1c069-147">The snippets below demonstrate how to upload some sample data to the folder (**mynewfolder**) you created in the previous section.</span></span>

<span data-ttu-id="1c069-148">Karşıya yüklenecek örnek veri arıyorsanız [Azure Data Lake Git Deposu](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData)'ndan **Ambulance Data** klasörünü alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c069-148">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="1c069-149">Dosyayı indirin ve bilgisayarınızda C:\sampledata\ gibi yerel bir dizinde depolayın.</span><span class="sxs-lookup"><span data-stu-id="1c069-149">Download the file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> <span data-ttu-id="1c069-150">Hedef için dosya adı dahil olmak üzere yolun tamamını belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c069-150">For the destination, you must specify the complete path including the file name.</span></span>
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a><span data-ttu-id="1c069-151">Data Lake Store hesabındaki dosyaları listeleme</span><span class="sxs-lookup"><span data-stu-id="1c069-151">List files in a Data Lake Store account</span></span>

<span data-ttu-id="1c069-152">Bir Data Lake Store hesabındaki dosyaları listelemek için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="1c069-152">Use the following command to list the files in a Data Lake Store account.</span></span>

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

<span data-ttu-id="1c069-153">Bunun çıktısının aşağıdakine benzer olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="1c069-153">The output of this should be similar to the following:</span></span>

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

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a><span data-ttu-id="1c069-154">Data Lake Store hesabındaki verileri yeniden adlandırma, indirme ve silme</span><span class="sxs-lookup"><span data-stu-id="1c069-154">Rename, download, and delete data from a Data Lake Store account</span></span> 

* <span data-ttu-id="1c069-155">**Bir dosyayı yeniden adlandırmak için** aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c069-155">**To rename a file**, use the following command:</span></span>
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* <span data-ttu-id="1c069-156">**Bir dosyayı indirmek için** aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="1c069-156">**To download a file**, use the following command.</span></span> <span data-ttu-id="1c069-157">Belirttiğiniz hedef yolun önceden var olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="1c069-157">Make sure the destination path you specify already exists.</span></span>
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > <span data-ttu-id="1c069-158">Bu komut, henüz mevcut değilse hedef klasörü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1c069-158">The command creates the destination folder if it does not exist.</span></span>
    > 
    >

* <span data-ttu-id="1c069-159">**Bir dosyayı silmek için** aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c069-159">**To delete a file**, use the following command:</span></span>
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    <span data-ttu-id="1c069-160">Hem **mynewfolder** klasörünü hem de **vehicle1_09142014_copy.csv** dosyasını tek bir komutla silmek istiyorsanız --recurse parametresini kullanın</span><span class="sxs-lookup"><span data-stu-id="1c069-160">If you want to delete the folder **mynewfolder** and the file **vehicle1_09142014_copy.csv** together in one command, use the --recurse parameter</span></span>

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a><span data-ttu-id="1c069-161">Data Lake Store hesabı için izin ve ACL’ler ile çalışma</span><span class="sxs-lookup"><span data-stu-id="1c069-161">Work with permissions and ACLs for a Data Lake Store account</span></span>

<span data-ttu-id="1c069-162">Bu bölümde, Azure CLI 2.0 aracını kullanarak ACL’leri ve izinleri nasıl yönetebileceğiniz hakkında bilgi edineceksiniz.</span><span class="sxs-lookup"><span data-stu-id="1c069-162">In this section you learn about how to manage ACLs and permissions using Azure CLI 2.0.</span></span> <span data-ttu-id="1c069-163">Azure Data Lake Store’da ACL’lerin nasıl uygulandığıyla ilgili ayrıntılı bir tartışma için bkz. [Azure Data Lake Store’da erişim denetimi](data-lake-store-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="1c069-163">For a detailed discussion on how ACLs are implemented in Azure Data Lake Store, see [Access control in Azure Data Lake Store](data-lake-store-access-control.md).</span></span>

* <span data-ttu-id="1c069-164">**Bir dosya veya klasörün sahibini güncelleştirmek için** aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c069-164">**To update the owner of a file/folder**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="1c069-165">**Bir dosya veya klasörün izinlerini güncelleştirmek için** aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c069-165">**To update the permissions for a file/folder**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* <span data-ttu-id="1c069-166">**Belirli bir yolun ACL’lerini almak için** aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c069-166">**To get the ACLs for a given path**, use the following command:</span></span>

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    <span data-ttu-id="1c069-167">Çıktının aşağıdakine benzer olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="1c069-167">The output should be similar to the following:</span></span>

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

* <span data-ttu-id="1c069-168">**ACL’ye yönelik bir giriş ayarlamak için** aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c069-168">**To set an entry for an ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* <span data-ttu-id="1c069-169">**ACL’ye yönelik bir girişi kaldırmak için** aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c069-169">**To remove an entry for an ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="1c069-170">**Varsayılan ACL’nin tamamını kaldırmak için** aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c069-170">**To remove an entire default ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* <span data-ttu-id="1c069-171">**Varsayılan olmayan bir ACL’nin tamamını kaldırmak için** aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c069-171">**To remove an entire non-default ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="1c069-172">Data Lake Store hesabını silme</span><span class="sxs-lookup"><span data-stu-id="1c069-172">Delete a Data Lake Store account</span></span>
<span data-ttu-id="1c069-173">Bir Data Lake Store hesabını silmek için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="1c069-173">Use the following command to delete a Data Lake Store account.</span></span>

```azurecli
az dls account delete --account mydatalakestore
```

<span data-ttu-id="1c069-174">İstendiğinde, hesabı silmek için **Y** yazın.</span><span class="sxs-lookup"><span data-stu-id="1c069-174">When prompted, enter **Y** to delete the account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c069-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1c069-175">Next steps</span></span>

* [<span data-ttu-id="1c069-176">Azure Data Lake Store CLI 2.0 başvurusu</span><span class="sxs-lookup"><span data-stu-id="1c069-176">Azure Data Lake Store CLI 2.0 reference</span></span>](https://docs.microsoft.com/cli/azure/dls)
* [<span data-ttu-id="1c069-177">Data Lake Store'da verilerin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="1c069-177">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="1c069-178">Azure Data Lake Analytics'i Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="1c069-178">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="1c069-179">Azure HDInsight'ı Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="1c069-179">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
