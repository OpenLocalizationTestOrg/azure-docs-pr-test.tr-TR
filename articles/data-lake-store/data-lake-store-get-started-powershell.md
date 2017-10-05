---
title: "PowerShell kullanarak Azure Data Lake Store ile çalışmaya başlama | Microsoft Docs"
description: "Bir Data Lake Store hesabı oluşturmak ve temel işlemleri gerçekleştirmek için Azure PowerShell'i kullanma"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf85f369-f9aa-4ca1-9ae7-e03a78eb7290
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 23c9aaa089251bff5132652475f4daadc2c128fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a><span data-ttu-id="ac28b-103">Azure PowerShell'i kullanarak Azure Data Lake Store ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ac28b-103">Get started with Azure Data Lake Store using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ac28b-104">Portal</span><span class="sxs-lookup"><span data-stu-id="ac28b-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="ac28b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac28b-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="ac28b-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="ac28b-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="ac28b-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="ac28b-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="ac28b-108">REST API</span><span class="sxs-lookup"><span data-stu-id="ac28b-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="ac28b-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ac28b-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="ac28b-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="ac28b-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="ac28b-111">Python</span><span class="sxs-lookup"><span data-stu-id="ac28b-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="ac28b-112">Azure Data Lake Store hesabı oluşturma ve klasör oluşturma, veri dosyalarını yükleme ve indirme, hesabınızı silme gibi temel işlemleri gerçekleştirmek için Azure PowerShell'in nasıl kullanılacağını öğrenin. Data Lake Store hakkında daha fazla bilgi için bkz. [Data Lake Store'a Genel Bakış](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ac28b-112">Learn how to use Azure PowerShell to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac28b-113">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="ac28b-113">Prerequisites</span></span>
<span data-ttu-id="ac28b-114">Bu öğreticiye başlamadan önce aşağıdakilere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ac28b-114">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="ac28b-115">**Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="ac28b-115">**An Azure subscription**.</span></span> <span data-ttu-id="ac28b-116">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ac28b-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ac28b-117">**Azure PowerShell 1.0 veya üstü**.</span><span class="sxs-lookup"><span data-stu-id="ac28b-117">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="ac28b-118">Bkz. [Azure PowerShell'i yükleme ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ac28b-118">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="authentication"></a><span data-ttu-id="ac28b-119">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="ac28b-119">Authentication</span></span>
<span data-ttu-id="ac28b-120">Bu makalede, Azure hesabı kimlik bilgilerinizi girmenizi isteyen daha basit bir Data Lake Store kimlik doğrulama yaklaşımı kullanılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ac28b-120">This article uses a simpler authentication approach with Data Lake Store where you are prompted to enter your Azure account credentials.</span></span> <span data-ttu-id="ac28b-121">Data Lake Store hesabına ve dosya sistemine erişim düzeyi bu durumda oturum açmış kullanıcının erişim düzeyine göre yönetilir.</span><span class="sxs-lookup"><span data-stu-id="ac28b-121">The access level to Data Lake Store account and file system is then governed by the access level of the logged in user.</span></span> <span data-ttu-id="ac28b-122">Ancak, Data Lake Store kimlik doğrulaması için **son kullanıcı kimlik doğrulaması** veya **hizmetten hizmete kimlik doğrulama** şeklinde diğer yaklaşımlar da mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="ac28b-122">However, there are other approaches as well to authenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="ac28b-123">Kimlik doğrulaması gerçekleştirmeyle ilgili yönergeler ve daha fazla bilgi için [Son kullanıcı kimlik doğrulaması](data-lake-store-end-user-authenticate-using-active-directory.md) veya [Hizmetten hizmete kimlik doğrulaması](data-lake-store-authenticate-using-active-directory.md) bölümlerine göz atın.</span><span class="sxs-lookup"><span data-stu-id="ac28b-123">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="ac28b-124">Azure Data Lake Store hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ac28b-124">Create an Azure Data Lake Store account</span></span>
1. <span data-ttu-id="ac28b-125">Masaüstünüzde yeni bir Windows PowerShell penceresi açın ve Azure hesabınızda oturum açmak, aboneliği ayarlamak ve Data Lake Store sağlayıcısını kaydetmek için aşağıdaki kod parçacığını girin.</span><span class="sxs-lookup"><span data-stu-id="ac28b-125">From your desktop, open a new Windows PowerShell window, and enter the following snippet to log in to your Azure account, set the subscription, and register the Data Lake Store provider.</span></span> <span data-ttu-id="ac28b-126">Oturum açmanız istendiğinde, bir abonelik yöneticisi/sahibi olarak oturum açtığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ac28b-126">When prompted to log in, make sure you log in as one of the subscription admininistrators/owner:</span></span>

        # Log in to your Azure account
        Login-AzureRmAccount

        # List all the subscriptions associated to your account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. <span data-ttu-id="ac28b-127">Azure Data Lake Store hesabı, bir Azure Kaynak Grubu ile ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="ac28b-127">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="ac28b-128">Azure Kaynak Grubu oluşturma işlemiyle başlayın.</span><span class="sxs-lookup"><span data-stu-id="ac28b-128">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="ac28b-129">![Bir Azure kaynak grubu oluşturma](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")</span><span class="sxs-lookup"><span data-stu-id="ac28b-129">![Create an Azure Resource Group](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")</span></span>
3. <span data-ttu-id="ac28b-130">Bir Azure Data Lake Store hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ac28b-130">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="ac28b-131">Belirttiğiniz ad yalnızca küçük harflerden ve rakamlardan oluşmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ac28b-131">The name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="ac28b-132">![Azure Data Lake Store hesabı oluşturma](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")</span><span class="sxs-lookup"><span data-stu-id="ac28b-132">![Create an Azure Data Lake Store account](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")</span></span>
4. <span data-ttu-id="ac28b-133">Hesabın başarıyla oluşturulduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="ac28b-133">Verify that the account is successfully created.</span></span>

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    <span data-ttu-id="ac28b-134">Bu işlemin çıktısı **True** olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ac28b-134">The output for this should be **True**.</span></span>

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a><span data-ttu-id="ac28b-135">Azure Data Lake Store'unuzda dizin yapıları oluşturma</span><span class="sxs-lookup"><span data-stu-id="ac28b-135">Create directory structures in your Azure Data Lake Store</span></span>
<span data-ttu-id="ac28b-136">Veri depolamak ve yönetmek için Azure Data Lake Store hesabınızın altında dizin oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac28b-136">You can create directories under your Azure Data Lake Store account to manage and store data.</span></span>

1. <span data-ttu-id="ac28b-137">Bir kök dizin belirtin.</span><span class="sxs-lookup"><span data-stu-id="ac28b-137">Specify a root directory.</span></span>

        $myrootdir = "/"
2. <span data-ttu-id="ac28b-138">Belirtilen kökün altında **mynewdirectory** adlı yeni bir dizin oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ac28b-138">Create a new directory called **mynewdirectory** under the specified root.</span></span>

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. <span data-ttu-id="ac28b-139">Yeni dizinin başarıyla oluşturulduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="ac28b-139">Verify that the new directory is successfully created.</span></span>

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    <span data-ttu-id="ac28b-140">Bu işlemin aşağıdakine benzer bir çıktı göstermesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="ac28b-140">It should show an output like the following:</span></span>

    <span data-ttu-id="ac28b-141">![Dizin Doğrulama](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")</span><span class="sxs-lookup"><span data-stu-id="ac28b-141">![Verify Directory](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")</span></span>

## <a name="upload-data-to-your-azure-data-lake-store"></a><span data-ttu-id="ac28b-142">Azure Data Lake Store'unuza veri yükleme</span><span class="sxs-lookup"><span data-stu-id="ac28b-142">Upload data to your Azure Data Lake Store</span></span>
<span data-ttu-id="ac28b-143">Verilerinizi Data Lake Store'a doğrudan kök düzeyinde veya hesap içinde oluşturduğunuz bir dizine yüklenecek şekilde yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac28b-143">You can upload your data to Data Lake Store directly at the root level or to a directory that you created within the account.</span></span> <span data-ttu-id="ac28b-144">Aşağıdaki kod parçacıkları, birtakım örnek verilerin önceki bölümde oluşturduğunuz dizine (**mynewdirectory**) nasıl yükleneceğini göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="ac28b-144">The snippets below demonstrate how to upload some sample data to the directory (**mynewdirectory**) you created in the previous section.</span></span>

<span data-ttu-id="ac28b-145">Karşıya yüklenecek örnek veri arıyorsanız [Azure Data Lake Git Deposu](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData)'ndan **Ambulance Data** klasörünü alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac28b-145">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="ac28b-146">Dosyayı indirin ve bilgisayarınızda C:\sampledata\ gibi yerel bir dizinde depolayın.</span><span class="sxs-lookup"><span data-stu-id="ac28b-146">Download the file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a><span data-ttu-id="ac28b-147">Data Lake Store'unuzda verileri yeniden adlandırma, indirme ve silme</span><span class="sxs-lookup"><span data-stu-id="ac28b-147">Rename, download, and delete data from your Data Lake Store</span></span>
<span data-ttu-id="ac28b-148">Bir dosyayı yeniden adlandırmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="ac28b-148">To rename a file, use the following command:</span></span>

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="ac28b-149">Bir dosyayı indirmek için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="ac28b-149">To download a file, use the following command:</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

<span data-ttu-id="ac28b-150">Bir dosyayı silmek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="ac28b-150">To delete a file, use the following command:</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="ac28b-151">İstendiğinde, öğeyi silmek için **Y** yazın.</span><span class="sxs-lookup"><span data-stu-id="ac28b-151">When prompted, enter **Y** to delete the item.</span></span> <span data-ttu-id="ac28b-152">Birden fazla dosyayı silmek istiyorsanız tüm yolları virgülle ayrılmış olarak sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac28b-152">If you have more than one file to delete, you can provide all the paths separated by comma.</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a><span data-ttu-id="ac28b-153">Azure Data Lake Store hesabınızı silme</span><span class="sxs-lookup"><span data-stu-id="ac28b-153">Delete your Azure Data Lake Store account</span></span>
<span data-ttu-id="ac28b-154">Data Lake Store hesabınızı silmek için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="ac28b-154">Use the following command to delete your Data Lake Store account.</span></span>

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

<span data-ttu-id="ac28b-155">İstendiğinde, hesabı silmek için **Y** yazın.</span><span class="sxs-lookup"><span data-stu-id="ac28b-155">When prompted, enter **Y** to delete the account.</span></span>

## <a name="performance-guidance-while-using-powershell"></a><span data-ttu-id="ac28b-156">PowerShell’i kullanırken performans rehberi</span><span class="sxs-lookup"><span data-stu-id="ac28b-156">Performance guidance while using PowerShell</span></span>

<span data-ttu-id="ac28b-157">Aşağıda, Data Lake Store ile çalışmak için PowerShell’i kullanırken en iyi performansı elde etmek için ayarlanabilecek en önemli ayarlar sağlanmıştır:</span><span class="sxs-lookup"><span data-stu-id="ac28b-157">Below are the most important settings that can be tuned to get the best performance while using PowerShell to work with Data Lake Store:</span></span>

| <span data-ttu-id="ac28b-158">Özellik</span><span class="sxs-lookup"><span data-stu-id="ac28b-158">Property</span></span>            | <span data-ttu-id="ac28b-159">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="ac28b-159">Default</span></span> | <span data-ttu-id="ac28b-160">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ac28b-160">Description</span></span> |
|---------------------|---------|-------------|
| <span data-ttu-id="ac28b-161">PerFileThreadCount</span><span class="sxs-lookup"><span data-stu-id="ac28b-161">PerFileThreadCount</span></span>  | <span data-ttu-id="ac28b-162">10</span><span class="sxs-lookup"><span data-stu-id="ac28b-162">10</span></span>      | <span data-ttu-id="ac28b-163">Bu parametre, her bir dosya karşıya yüklenirken veya indirilirken kaç paralel iş parçacığı kullanılacağını seçmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="ac28b-163">This parameter enables you to choose the number of parallel threads for uploading or downloading each file.</span></span> <span data-ttu-id="ac28b-164">Bu sayı dosya başına ayrılabilecek en fazla iş parçacığı sayısını temsil eder, ancak senaryonuza bağlı olarak daha az iş parçacığı elde edebilirsiniz (örneğin, 1 KB boyutlu bir dosyayı karşıya yüklüyorsanız 20 iş parçacığı isteseniz bile bir iş parçacığınız olur).</span><span class="sxs-lookup"><span data-stu-id="ac28b-164">This number represents the max threads that can be allocated per file, but you may get less threads depending on your scenario (e.g. if you are uploading a 1KB file, you will get one thread even if you ask for 20 threads).</span></span>  |
| <span data-ttu-id="ac28b-165">ConcurrentFileCount</span><span class="sxs-lookup"><span data-stu-id="ac28b-165">ConcurrentFileCount</span></span> | <span data-ttu-id="ac28b-166">10</span><span class="sxs-lookup"><span data-stu-id="ac28b-166">10</span></span>      | <span data-ttu-id="ac28b-167">Bu parametre özellikle klasörlerin karşıya yüklenmesi ve indirilmesi içindir.</span><span class="sxs-lookup"><span data-stu-id="ac28b-167">This parameter is specifically for uploading or downloading folders.</span></span> <span data-ttu-id="ac28b-168">Bu parametre, karşıya yüklenebilecek veya indirilebilecek eş zamanlı dosya sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="ac28b-168">This parameter determines the number of concurrent files that can be uploaded or downloaded.</span></span> <span data-ttu-id="ac28b-169">Bu sayı, tek seferde karşıya yüklenebilecek veya indirilebilecek en fazla eş zamanlı dosya sayısını temsil eder, ancak senaryonuza bağlı olarak daha az eş zamanlılık elde edebilirsiniz (örneğin, karşıya iki dosya yüklüyorsanız 15 eş zamanlı dosya yükleme isteseniz bile iki yükleme sağlanır).</span><span class="sxs-lookup"><span data-stu-id="ac28b-169">This number represents the maximum number of concurrent files that can be uploaded or downloaded at one time, but you may get less concurrency depending on your scenario (e.g. if you are uploading two files, you will get two concurrent file uploads even if you ask for 15).</span></span> |

<span data-ttu-id="ac28b-170">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="ac28b-170">**Example**</span></span>

<span data-ttu-id="ac28b-171">Bu komut, dosya başına 20 iş parçacığı ve 100 eşzamanlı dosya kullanarak dosyaları Azure Data Lake Store’dan kullanıcının yerel sürücüsüne indirir.</span><span class="sxs-lookup"><span data-stu-id="ac28b-171">This command downloads files from Azure Data Lake Store to the user's local drive using 20 threads per file and 100 concurrent files.</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-the-value-to-set-for-these-parameters"></a><span data-ttu-id="ac28b-172">Bu parametreler için ayarlanacak değerleri nasıl belirlerim?</span><span class="sxs-lookup"><span data-stu-id="ac28b-172">How do I determine the value to set for these parameters?</span></span>

<span data-ttu-id="ac28b-173">Aşağıda kullanabileceğiniz bazı yönergeler verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ac28b-173">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="ac28b-174">**1. Adım: Toplam iş parçacığı sayısını belirleyin** - İlk olarak kullanılması gereken toplam iş parçacığı sayısını hesaplayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac28b-174">**Step 1: Determine the total thread count** - You should start by calculating the total thread count to use.</span></span> <span data-ttu-id="ac28b-175">Genel bir kural olarak her fiziksel çekirdek için 6 iş parçacığı kullanmalısınız.</span><span class="sxs-lookup"><span data-stu-id="ac28b-175">As a general guideline, you should use 6 threads for each physical core.</span></span>

        Total thread count = total physical cores * 6

    <span data-ttu-id="ac28b-176">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="ac28b-176">**Example**</span></span>

    <span data-ttu-id="ac28b-177">PowerShell komutlarını 16 çekirdekli bir D14 VM’den çalıştırdığınız varsayılmıştır</span><span class="sxs-lookup"><span data-stu-id="ac28b-177">Assuming you are running the PowerShell commands from a D14 VM that has 16 cores</span></span>

        Total thread count = 16 cores * 6 = 96 threads


* <span data-ttu-id="ac28b-178">**2. Adım: PerFileThreadCount değerini hesaplayın**  - Kendi PerFileThreadCount değerimizi dosyaların boyutunu temel olarak hesaplıyoruz.</span><span class="sxs-lookup"><span data-stu-id="ac28b-178">**Step 2: Calculate PerFileThreadCount**  - We calculate our PerFileThreadCount based on the size of the files.</span></span> <span data-ttu-id="ac28b-179">2,5 GB’den küçük dosyalar için varsayılan değer olan 10 yeterli olduğundan bu parametreyi değiştirmek gerekmez.</span><span class="sxs-lookup"><span data-stu-id="ac28b-179">For files smaller than 2.5GB, there is no need to change this parameter because the default of 10 is sufficient.</span></span> <span data-ttu-id="ac28b-180">2,5 GB'tan büyük dosyalar için 10 iş parçacığını ilk 2,5 GB için bir temel olarak kullanın ve dosya boyutundaki her 256 MB’lık ek artış için 1 iş parçacığı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ac28b-180">For files larger than 2.5GB, you should use 10 threads as the base for the first 2.5GB and add 1 thread for each additional 256MB increase in file size.</span></span> <span data-ttu-id="ac28b-181">Birçok farklı boyutta dosya içeren bir klasörü kopyalıyorsanız dosyaları benzer dosya boyutları halinde gruplandırmayı göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="ac28b-181">If you are copying a folder with a large range of file sizes, consider grouping them into similar file sizes.</span></span> <span data-ttu-id="ac28b-182">Dosya boyutlarının benzer olmaması performansın düşmesine neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="ac28b-182">Having dissimilar file sizes may cause non-optimal performance.</span></span> <span data-ttu-id="ac28b-183">Benzer boyutlu dosyaları gruplandırmanız mümkün değilse PerFileThreadCount değerini en büyük dosya boyutuna göre ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ac28b-183">If that's not possible to group similar file sizes, you should set PerFileThreadCount based on the largest file size.</span></span>

        PerFileThreadCount = 10 threads for the first 2.5GB + 1 thread for each additional 256MB increase in file size

    <span data-ttu-id="ac28b-184">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="ac28b-184">**Example**</span></span>

    <span data-ttu-id="ac28b-185">Boyutu 1 GB ile 10 GB arasında değişen 100 dosyanız olduğunu varsayarsak, denklemde en büyük dosya boyutu olan 10 GB’ı kullanırız ve denklem aşağıdaki gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="ac28b-185">Assuming you have 100 files ranging from 1GB to 10GB, we use the 10GB as the largest file size for equation, which would read like the following.</span></span>

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* <span data-ttu-id="ac28b-186">**3. Adım: ConcurrentFilecount değerini hesaplayın** - Aşağıdaki denklemi temel alıp toplam iş parçacığı sayısı ve PerFileThreadCount değerini kullanarak ConcurrentFileCount değerini hesaplayın.</span><span class="sxs-lookup"><span data-stu-id="ac28b-186">**Step 3: Calculate ConcurrentFilecount** - Use the total thread count and PerFileThreadCount to calculate ConcurrentFileCount based on the following equation.</span></span>

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    <span data-ttu-id="ac28b-187">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="ac28b-187">**Example**</span></span>

    <span data-ttu-id="ac28b-188">Kullandığımız örnek değerler temel alınmıştır</span><span class="sxs-lookup"><span data-stu-id="ac28b-188">Based on the example values we have been using</span></span>

        96 = 40 * ConcurrentFileCount

    <span data-ttu-id="ac28b-189">Sonuç olarak **ConcurrentFileCount** değeri **2,4** ve bunu **2**’ye yuvarlayabiliriz.</span><span class="sxs-lookup"><span data-stu-id="ac28b-189">So, **ConcurrentFileCount** is **2.4**, which we can round off to **2**.</span></span>

### <a name="further-tuning"></a><span data-ttu-id="ac28b-190">Daha fazla ayar</span><span class="sxs-lookup"><span data-stu-id="ac28b-190">Further tuning</span></span>

<span data-ttu-id="ac28b-191">Üzerinde çalışılan dosyaların boyutu çeşitlilik gösterdiğinden daha fazla ayar yapmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="ac28b-191">You might require further tuning because there is a range of file sizes to work with.</span></span> <span data-ttu-id="ac28b-192">Dosyaların hepsi veya çoğu 10 GB aralığından büyükse veya bu aralığa daha yakınsa yukarıdaki hesaplama iyi bir sonuç verir.</span><span class="sxs-lookup"><span data-stu-id="ac28b-192">The above calculation works well if all or most of the files are larger and closer to the 10GB range.</span></span> <span data-ttu-id="ac28b-193">Bunun yerine çoğu dosya küçük olacak şekilde birçok farklı dosya boyutu varsa PerFileThreadCount değerini azaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac28b-193">If instead, there are many different files sizes with many files being smaller, then you could reduce PerFileThreadCount.</span></span> <span data-ttu-id="ac28b-194">PerFileThreadCount değerini azaltarak ConcurrentFileCount değerini artırabiliriz.</span><span class="sxs-lookup"><span data-stu-id="ac28b-194">By reducing the PerFileThreadCount, we can increase ConcurrentFileCount.</span></span> <span data-ttu-id="ac28b-195">Dolayısıyla, dosyalarımızın çoğunun daha küçük (5 GB aralığında) olduğunu varsayarsak hesaplamayı yeniden yapabiliriz:</span><span class="sxs-lookup"><span data-stu-id="ac28b-195">So, if we assume that most of our files are smaller in the 5GB range, we can re-do our calculation:</span></span>

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

<span data-ttu-id="ac28b-196">Bu durumda **ConcurrentFileCount** değeri 96/20 işlemi sonucunda 4.8 olarak bulunur **4**’e yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="ac28b-196">So, **ConcurrentFileCount** will now be 96/20, which is 4.8, rounded off to **4**.</span></span>

<span data-ttu-id="ac28b-197">Dosya boyutlarınızın dağılımına göre **PerFileThreadCount** değerini artırıp azaltarak bu ayarları değiştirmeye devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac28b-197">You can continue to tune these settings by changing the **PerFileThreadCount** up and down depending on the distribution of your file sizes.</span></span>

### <a name="limitation"></a><span data-ttu-id="ac28b-198">Sınırlama</span><span class="sxs-lookup"><span data-stu-id="ac28b-198">Limitation</span></span>

* <span data-ttu-id="ac28b-199">**Dosya sayısı ConcurrentFileCount değerinden az**: Karşıya yüklemekte olduğunuz dosyaların sayısı hesapladığınız **ConcurrentFileCount** değerinden azsa **ConcurrentFileCount** değerini dosya sayısına eşit olacak şekilde azaltmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ac28b-199">**Number of files is less than ConcurrentFileCount**: If the number of files you are uploading is smaller than the **ConcurrentFileCount** that you calculated, then you should reduce **ConcurrentFileCount** to be equal to the number of files.</span></span> <span data-ttu-id="ac28b-200">**PerFileThreadCount** değerini artırmak için kalan iş parçacıklarından dilediğinizi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac28b-200">You can use any remaining threads to increase **PerFileThreadCount**.</span></span>

* <span data-ttu-id="ac28b-201">**Çok fazla iş parçacığı**: Kümenizin boyutunu artırmadan iş parçacığı sayısını çok fazla artırırsanız düşük performans riskiyle karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac28b-201">**Too many threads**: If you increase thread count too much without increasing your cluster size, you run the risk of degraded performance.</span></span> <span data-ttu-id="ac28b-202">CPU’da bağlam değişimi sırasında çekişme sorunları olabilir.</span><span class="sxs-lookup"><span data-stu-id="ac28b-202">There can be contention issues when context-switching on the CPU.</span></span>

* <span data-ttu-id="ac28b-203">**Yetersiz eşzamanlılık**: Eşzamanlılık yeterli değilse kümeniz çok küçük olabilir.</span><span class="sxs-lookup"><span data-stu-id="ac28b-203">**Insufficient concurrency**: If the concurrency is not sufficient, then your cluster may be too small.</span></span> <span data-ttu-id="ac28b-204">Eşzamanlılığı artırmak için kümenizdeki düğüm sayısını artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac28b-204">You can increase the number of nodes in your cluster which will give you more concurrency.</span></span>

* <span data-ttu-id="ac28b-205">**Azaltma hataları**: Eşzamanlılığınız çok yüksekse azaltma hataları görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac28b-205">**Throttling errors**: You may see throttling errors if your concurrency is too high.</span></span> <span data-ttu-id="ac28b-206">Azaltma hataları görüyorsanız eşzamanlılığı azaltmanız veya bize ulaşmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ac28b-206">If you are seeing throttling errors, you should either reduce the concurrency or contact us.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac28b-207">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ac28b-207">Next steps</span></span>
* [<span data-ttu-id="ac28b-208">Data Lake Store'da verilerin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="ac28b-208">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="ac28b-209">Azure Data Lake Analytics'i Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="ac28b-209">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="ac28b-210">Azure HDInsight'ı Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="ac28b-210">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

