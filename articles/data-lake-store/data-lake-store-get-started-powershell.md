---
title: "aaaUse PowerShell tooget Azure Data Lake Store ile çalışmaya | Microsoft Docs"
description: "Temel işlemleri gerçekleştirmek ve Azure PowerShell toocreate bir Data Lake Store hesabı kullanın"
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
ms.openlocfilehash: 9c958bfd63e412ec0b0a4113a149f61aee026bc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a><span data-ttu-id="19381-103">Azure PowerShell'i kullanarak Azure Data Lake Store ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="19381-103">Get started with Azure Data Lake Store using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="19381-104">Portal</span><span class="sxs-lookup"><span data-stu-id="19381-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="19381-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="19381-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="19381-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="19381-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="19381-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="19381-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="19381-108">REST API</span><span class="sxs-lookup"><span data-stu-id="19381-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="19381-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="19381-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="19381-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="19381-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="19381-111">Python</span><span class="sxs-lookup"><span data-stu-id="19381-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="19381-112">Bir Azure Data Lake toouse Azure PowerShell toocreate nasıl depolamak öğrenin hesap ve gibi klasör oluşturma karşıya yükleme ve veri dosyalarını indirme temel işlemleri gerçekleştirmek, vb., hesabınızı silme. Data Lake Store hakkında daha fazla bilgi için bkz. [Data Lake Store'a Genel Bakış](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="19381-112">Learn how toouse Azure PowerShell toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19381-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="19381-113">Prerequisites</span></span>
<span data-ttu-id="19381-114">Bu öğreticiye başlamadan önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="19381-114">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="19381-115">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="19381-115">**An Azure subscription**.</span></span> <span data-ttu-id="19381-116">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="19381-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="19381-117">**Azure PowerShell 1.0 veya üstü**.</span><span class="sxs-lookup"><span data-stu-id="19381-117">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="19381-118">Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="19381-118">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="authentication"></a><span data-ttu-id="19381-119">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="19381-119">Authentication</span></span>
<span data-ttu-id="19381-120">Bu makalede Azure hesabı kimlik bilgileriniz istendiğinde tooenter nerede Data Lake Store ile basit bir kimlik doğrulama yaklaşım kullanır.</span><span class="sxs-lookup"><span data-stu-id="19381-120">This article uses a simpler authentication approach with Data Lake Store where you are prompted tooenter your Azure account credentials.</span></span> <span data-ttu-id="19381-121">Merhaba erişim düzeyi tooData Lake Store hesabı ve dosya sistemi, kullanıcı oturum hello hello erişim düzeyi sonra tabidir.</span><span class="sxs-lookup"><span data-stu-id="19381-121">hello access level tooData Lake Store account and file system is then governed by hello access level of hello logged in user.</span></span> <span data-ttu-id="19381-122">Ancak, diğer yaklaşım vardır Data Lake Store ile iyi tooauthenticate olarak olan **son kullanıcı kimlik doğrulaması** veya **hizmeti için kimlik doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="19381-122">However, there are other approaches as well tooauthenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="19381-123">Yönergeler ve hakkında daha fazla bilgi için tooauthenticate, bkz: [son kullanıcı kimlik doğrulaması](data-lake-store-end-user-authenticate-using-active-directory.md) veya [hizmeti için kimlik doğrulama](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="19381-123">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="19381-124">Azure Data Lake Store hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="19381-124">Create an Azure Data Lake Store account</span></span>
1. <span data-ttu-id="19381-125">Masaüstünüzde yeni bir Windows PowerShell penceresi açın ve aşağıdaki kod parçacığında toolog tooyour Azure hesabı içinde hello girin, hello aboneliği ayarlamak ve hello Data Lake Store sağlayıcısını kaydetmek.</span><span class="sxs-lookup"><span data-stu-id="19381-125">From your desktop, open a new Windows PowerShell window, and enter hello following snippet toolog in tooyour Azure account, set hello subscription, and register hello Data Lake Store provider.</span></span> <span data-ttu-id="19381-126">' De, istendiğinde toolog emin yaptığınızda, bir hello Abonelik Yöneticisi/sahibi oturum açın:</span><span class="sxs-lookup"><span data-stu-id="19381-126">When prompted toolog in, make sure you log in as one of hello subscription admininistrators/owner:</span></span>

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. <span data-ttu-id="19381-127">Azure Data Lake Store hesabı, bir Azure Kaynak Grubu ile ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="19381-127">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="19381-128">Azure Kaynak Grubu oluşturma işlemiyle başlayın.</span><span class="sxs-lookup"><span data-stu-id="19381-128">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="19381-129">![Bir Azure kaynak grubu oluşturma](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")</span><span class="sxs-lookup"><span data-stu-id="19381-129">![Create an Azure Resource Group](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")</span></span>
3. <span data-ttu-id="19381-130">Bir Azure Data Lake Store hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="19381-130">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="19381-131">Belirttiğiniz hello adı yalnızca küçük harf ve sayı içermelidir.</span><span class="sxs-lookup"><span data-stu-id="19381-131">hello name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="19381-132">![Azure Data Lake Store hesabı oluşturma](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")</span><span class="sxs-lookup"><span data-stu-id="19381-132">![Create an Azure Data Lake Store account](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")</span></span>
4. <span data-ttu-id="19381-133">Merhaba hesabın başarıyla oluşturulduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="19381-133">Verify that hello account is successfully created.</span></span>

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    <span data-ttu-id="19381-134">Bu olmalıdır çıktısı hello **doğru**.</span><span class="sxs-lookup"><span data-stu-id="19381-134">hello output for this should be **True**.</span></span>

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a><span data-ttu-id="19381-135">Azure Data Lake Store'unuzda dizin yapıları oluşturma</span><span class="sxs-lookup"><span data-stu-id="19381-135">Create directory structures in your Azure Data Lake Store</span></span>
<span data-ttu-id="19381-136">Dizin, Azure Data Lake Store hesabı toomanage altında oluşturmak ve verileri depolamak.</span><span class="sxs-lookup"><span data-stu-id="19381-136">You can create directories under your Azure Data Lake Store account toomanage and store data.</span></span>

1. <span data-ttu-id="19381-137">Bir kök dizin belirtin.</span><span class="sxs-lookup"><span data-stu-id="19381-137">Specify a root directory.</span></span>

        $myrootdir = "/"
2. <span data-ttu-id="19381-138">Adlı yeni bir dizin oluşturun **mynewdirectory** hello belirtilen kök altında.</span><span class="sxs-lookup"><span data-stu-id="19381-138">Create a new directory called **mynewdirectory** under hello specified root.</span></span>

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. <span data-ttu-id="19381-139">Bu hello yeni bir dizin başarıyla oluşturuldu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="19381-139">Verify that hello new directory is successfully created.</span></span>

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    <span data-ttu-id="19381-140">Merhaba aşağıdaki gibi bir çıktı göstermesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="19381-140">It should show an output like hello following:</span></span>

    <span data-ttu-id="19381-141">![Dizin Doğrulama](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")</span><span class="sxs-lookup"><span data-stu-id="19381-141">![Verify Directory](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")</span></span>

## <a name="upload-data-tooyour-azure-data-lake-store"></a><span data-ttu-id="19381-142">Veri tooyour Azure Data Lake Store karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="19381-142">Upload data tooyour Azure Data Lake Store</span></span>
<span data-ttu-id="19381-143">Merhaba hesap içinde oluşturduğunuz doğrudan hello kök düzeyinde veya tooa dizininde tooData data Lake Store karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19381-143">You can upload your data tooData Lake Store directly at hello root level or tooa directory that you created within hello account.</span></span> <span data-ttu-id="19381-144">Merhaba parçacıkları göstermek nasıl tooupload bazı örnek veri toohello dizini (**mynewdirectory**) hello önceki bölümde oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="19381-144">hello snippets below demonstrate how tooupload some sample data toohello directory (**mynewdirectory**) you created in hello previous section.</span></span>

<span data-ttu-id="19381-145">Bazı örnek veri tooupload için arıyorsanız, hello alabilirsiniz **Ambulance Data** hello klasöründen [Azure Data Lake Git deposu](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="19381-145">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="19381-146">Merhaba dosyasını indirin ve C:\sampledata\ gibi bilgisayarınızdaki yerel bir klasörde saklayın.</span><span class="sxs-lookup"><span data-stu-id="19381-146">Download hello file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a><span data-ttu-id="19381-147">Data Lake Store'unuzda verileri yeniden adlandırma, indirme ve silme</span><span class="sxs-lookup"><span data-stu-id="19381-147">Rename, download, and delete data from your Data Lake Store</span></span>
<span data-ttu-id="19381-148">toorename bir dosya hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="19381-148">toorename a file, use hello following command:</span></span>

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="19381-149">toodownload bir dosya hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="19381-149">toodownload a file, use hello following command:</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

<span data-ttu-id="19381-150">toodelete bir dosya hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="19381-150">toodelete a file, use hello following command:</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="19381-151">İstendiğinde, girin **Y** toodelete hello öğesi.</span><span class="sxs-lookup"><span data-stu-id="19381-151">When prompted, enter **Y** toodelete hello item.</span></span> <span data-ttu-id="19381-152">Birden fazla dosya toodelete varsa, tüm hello yollarının virgülle ayırarak sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="19381-152">If you have more than one file toodelete, you can provide all hello paths separated by comma.</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a><span data-ttu-id="19381-153">Azure Data Lake Store hesabınızı silme</span><span class="sxs-lookup"><span data-stu-id="19381-153">Delete your Azure Data Lake Store account</span></span>
<span data-ttu-id="19381-154">Komut toodelete aşağıdaki hello Data Lake Store hesabınızı kullanın.</span><span class="sxs-lookup"><span data-stu-id="19381-154">Use hello following command toodelete your Data Lake Store account.</span></span>

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

<span data-ttu-id="19381-155">İstendiğinde, girin **Y** toodelete hello hesabı.</span><span class="sxs-lookup"><span data-stu-id="19381-155">When prompted, enter **Y** toodelete hello account.</span></span>

## <a name="performance-guidance-while-using-powershell"></a><span data-ttu-id="19381-156">PowerShell’i kullanırken performans rehberi</span><span class="sxs-lookup"><span data-stu-id="19381-156">Performance guidance while using PowerShell</span></span>

<span data-ttu-id="19381-157">Aşağıda hello PowerShell toowork Data Lake Store ile kullanırken bizi tooget hello en iyi performans olabilir en önemli ayarlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="19381-157">Below are hello most important settings that can be tuned tooget hello best performance while using PowerShell toowork with Data Lake Store:</span></span>

| <span data-ttu-id="19381-158">Özellik</span><span class="sxs-lookup"><span data-stu-id="19381-158">Property</span></span>            | <span data-ttu-id="19381-159">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="19381-159">Default</span></span> | <span data-ttu-id="19381-160">Açıklama</span><span class="sxs-lookup"><span data-stu-id="19381-160">Description</span></span> |
|---------------------|---------|-------------|
| <span data-ttu-id="19381-161">PerFileThreadCount</span><span class="sxs-lookup"><span data-stu-id="19381-161">PerFileThreadCount</span></span>  | <span data-ttu-id="19381-162">10</span><span class="sxs-lookup"><span data-stu-id="19381-162">10</span></span>      | <span data-ttu-id="19381-163">Bu parametre toochoose hello yükleyerek veya her dosya indirme için paralel iş parçacığı sayısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="19381-163">This parameter enables you toochoose hello number of parallel threads for uploading or downloading each file.</span></span> <span data-ttu-id="19381-164">Bu sayı, dosya başına ayrılabilen hello en fazla iş parçacığı temsil eder, ancak senaryonuza bağlı olarak daha az iş parçacığı alabilirsiniz (örn. bir 1 KB dosya yüklüyorsanız, 20 iş parçacığı isteyin olsa bile bir iş parçacığı alırsınız).</span><span class="sxs-lookup"><span data-stu-id="19381-164">This number represents hello max threads that can be allocated per file, but you may get less threads depending on your scenario (e.g. if you are uploading a 1KB file, you will get one thread even if you ask for 20 threads).</span></span>  |
| <span data-ttu-id="19381-165">ConcurrentFileCount</span><span class="sxs-lookup"><span data-stu-id="19381-165">ConcurrentFileCount</span></span> | <span data-ttu-id="19381-166">10</span><span class="sxs-lookup"><span data-stu-id="19381-166">10</span></span>      | <span data-ttu-id="19381-167">Bu parametre özellikle klasörlerin karşıya yüklenmesi ve indirilmesi içindir.</span><span class="sxs-lookup"><span data-stu-id="19381-167">This parameter is specifically for uploading or downloading folders.</span></span> <span data-ttu-id="19381-168">Bu parametre, karşıya veya karşıdan eşzamanlı dosya hello sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="19381-168">This parameter determines hello number of concurrent files that can be uploaded or downloaded.</span></span> <span data-ttu-id="19381-169">Bu sayı hello karşıya veya aynı anda indirilen eşzamanlı dosyaları en büyük sayısını temsil eder, ancak senaryonuza bağlı olarak daha az eşzamanlılık alabilirsiniz (örneğin iki dosya yüklüyorsanız sorduğunuz olsa bile iki eşzamanlı dosya yüklemeleri alırsınız 15).</span><span class="sxs-lookup"><span data-stu-id="19381-169">This number represents hello maximum number of concurrent files that can be uploaded or downloaded at one time, but you may get less concurrency depending on your scenario (e.g. if you are uploading two files, you will get two concurrent file uploads even if you ask for 15).</span></span> |

<span data-ttu-id="19381-170">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="19381-170">**Example**</span></span>

<span data-ttu-id="19381-171">Bu komut dosyası ve 100 eş zamanlı dosya başına 20 iş parçacığı kullanarak Azure Data Lake Store toohello kullanıcının yerel sürücüden dosyaları indirir.</span><span class="sxs-lookup"><span data-stu-id="19381-171">This command downloads files from Azure Data Lake Store toohello user's local drive using 20 threads per file and 100 concurrent files.</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-hello-value-tooset-for-these-parameters"></a><span data-ttu-id="19381-172">Bu parametre için değer tooset hello nasıl belirlerim?</span><span class="sxs-lookup"><span data-stu-id="19381-172">How do I determine hello value tooset for these parameters?</span></span>

<span data-ttu-id="19381-173">Aşağıda kullanabileceğiniz bazı yönergeler verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="19381-173">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="19381-174">**1. adım: hello toplam iş parçacığı sayısını belirleyin** -tarafından hesaplama hello toplam iş parçacığı sayısı toouse başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="19381-174">**Step 1: Determine hello total thread count** - You should start by calculating hello total thread count toouse.</span></span> <span data-ttu-id="19381-175">Genel bir kural olarak her fiziksel çekirdek için 6 iş parçacığı kullanmalısınız.</span><span class="sxs-lookup"><span data-stu-id="19381-175">As a general guideline, you should use 6 threads for each physical core.</span></span>

        Total thread count = total physical cores * 6

    <span data-ttu-id="19381-176">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="19381-176">**Example**</span></span>

    <span data-ttu-id="19381-177">Merhaba PowerShell kullanmakta olduğunuz varsayılarak D14 VM'den 16 çekirdeğe sahip komutları.</span><span class="sxs-lookup"><span data-stu-id="19381-177">Assuming you are running hello PowerShell commands from a D14 VM that has 16 cores</span></span>

        Total thread count = 16 cores * 6 = 96 threads


* <span data-ttu-id="19381-178">**2. adım: PerFileThreadCount hesaplamak** -biz hello hello dosya boyutuna göre bizim PerFileThreadCount hesaplanamıyor.</span><span class="sxs-lookup"><span data-stu-id="19381-178">**Step 2: Calculate PerFileThreadCount**  - We calculate our PerFileThreadCount based on hello size of hello files.</span></span> <span data-ttu-id="19381-179">2.5 GB'den küçük dosyalar için var. gerek toochange Bu parametre hello varsayılan olarak 10 yeterli olduğundan</span><span class="sxs-lookup"><span data-stu-id="19381-179">For files smaller than 2.5GB, there is no need toochange this parameter because hello default of 10 is sufficient.</span></span> <span data-ttu-id="19381-180">2.5 GB'den büyük olan dosyalar için Hello temeli ilk 2,5 GB hello ve dosya boyutu 1 iş parçacığı her ek 256 MB artırmak için ekleme gibi 10 iş parçacığı kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="19381-180">For files larger than 2.5GB, you should use 10 threads as hello base for hello first 2.5GB and add 1 thread for each additional 256MB increase in file size.</span></span> <span data-ttu-id="19381-181">Birçok farklı boyutta dosya içeren bir klasörü kopyalıyorsanız dosyaları benzer dosya boyutları halinde gruplandırmayı göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="19381-181">If you are copying a folder with a large range of file sizes, consider grouping them into similar file sizes.</span></span> <span data-ttu-id="19381-182">Dosya boyutlarının benzer olmaması performansın düşmesine neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="19381-182">Having dissimilar file sizes may cause non-optimal performance.</span></span> <span data-ttu-id="19381-183">Bu olası toogroup benzer dosya boyutları değilse, hello en büyük dosya boyutuna göre PerFileThreadCount ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="19381-183">If that's not possible toogroup similar file sizes, you should set PerFileThreadCount based on hello largest file size.</span></span>

        PerFileThreadCount = 10 threads for hello first 2.5GB + 1 thread for each additional 256MB increase in file size

    <span data-ttu-id="19381-184">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="19381-184">**Example**</span></span>

    <span data-ttu-id="19381-185">1 GB too10GB arasında değişen 100 dosyalarınız varsayıldığında, hello olarak en büyük hello 10 GB dosya boyutu hello aşağıdaki gibi okuduğunuz eşitlik için kullanırız.</span><span class="sxs-lookup"><span data-stu-id="19381-185">Assuming you have 100 files ranging from 1GB too10GB, we use hello 10GB as hello largest file size for equation, which would read like hello following.</span></span>

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* <span data-ttu-id="19381-186">**3. adım: ConcurrentFilecount hesaplamak** -kullanım hello toplam iş parçacığı sayısı ve PerFileThreadCount toocalculate ConcurrentFileCount göre eşitlik aşağıdaki hello üzerinde.</span><span class="sxs-lookup"><span data-stu-id="19381-186">**Step 3: Calculate ConcurrentFilecount** - Use hello total thread count and PerFileThreadCount toocalculate ConcurrentFileCount based on hello following equation.</span></span>

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    <span data-ttu-id="19381-187">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="19381-187">**Example**</span></span>

    <span data-ttu-id="19381-188">Biz kullanmakta olduğunuz hello örneği değerlerine göre</span><span class="sxs-lookup"><span data-stu-id="19381-188">Based on hello example values we have been using</span></span>

        96 = 40 * ConcurrentFileCount

    <span data-ttu-id="19381-189">Bu nedenle, **ConcurrentFileCount** olan **2.4**, hangi biz çok yuvarlama**2**.</span><span class="sxs-lookup"><span data-stu-id="19381-189">So, **ConcurrentFileCount** is **2.4**, which we can round off too**2**.</span></span>

### <a name="further-tuning"></a><span data-ttu-id="19381-190">Daha fazla ayar</span><span class="sxs-lookup"><span data-stu-id="19381-190">Further tuning</span></span>

<span data-ttu-id="19381-191">Dosya boyutları toowork ile bir dizi olduğundan ek ayarlama gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="19381-191">You might require further tuning because there is a range of file sizes toowork with.</span></span> <span data-ttu-id="19381-192">iyi tümünü veya bir hello dosyaların en büyük ve daha yakın toohello 10 GB aralık dışındaysa hello hesaplama üstünde çalışır.</span><span class="sxs-lookup"><span data-stu-id="19381-192">hello above calculation works well if all or most of hello files are larger and closer toohello 10GB range.</span></span> <span data-ttu-id="19381-193">Bunun yerine çoğu dosya küçük olacak şekilde birçok farklı dosya boyutu varsa PerFileThreadCount değerini azaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19381-193">If instead, there are many different files sizes with many files being smaller, then you could reduce PerFileThreadCount.</span></span> <span data-ttu-id="19381-194">Merhaba PerFileThreadCount azaltarak ConcurrentFileCount artırabilir.</span><span class="sxs-lookup"><span data-stu-id="19381-194">By reducing hello PerFileThreadCount, we can increase ConcurrentFileCount.</span></span> <span data-ttu-id="19381-195">Bu nedenle, bizim hesaplama varsayıyoruz olursa bizim dosyaları hello 5 GB aralığında küçük çoğu, parolanızı yeniden yapın:</span><span class="sxs-lookup"><span data-stu-id="19381-195">So, if we assume that most of our files are smaller in hello 5GB range, we can re-do our calculation:</span></span>

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

<span data-ttu-id="19381-196">Bu nedenle, **ConcurrentFileCount** şimdi 4.8 olan 96/20, çok yuvarlanacak**4**.</span><span class="sxs-lookup"><span data-stu-id="19381-196">So, **ConcurrentFileCount** will now be 96/20, which is 4.8, rounded off too**4**.</span></span>

<span data-ttu-id="19381-197">Merhaba değiştirerek bu ayarları tootune sürdürebilirsiniz **PerFileThreadCount** dosya boyutlarınızı hello dağıtımını bağlı yukarı ve aşağı olarak.</span><span class="sxs-lookup"><span data-stu-id="19381-197">You can continue tootune these settings by changing hello **PerFileThreadCount** up and down depending on hello distribution of your file sizes.</span></span>

### <a name="limitation"></a><span data-ttu-id="19381-198">Sınırlama</span><span class="sxs-lookup"><span data-stu-id="19381-198">Limitation</span></span>

* <span data-ttu-id="19381-199">**Dosya sayısı, ConcurrentFileCount değerinden**: hello karşıya dosya sayısı hello küçük olup olmadığını **ConcurrentFileCount** hesaplanmış ardından azaltmanız gerekir  **ConcurrentFileCount** toobe eşit toohello dosya sayısı.</span><span class="sxs-lookup"><span data-stu-id="19381-199">**Number of files is less than ConcurrentFileCount**: If hello number of files you are uploading is smaller than hello **ConcurrentFileCount** that you calculated, then you should reduce **ConcurrentFileCount** toobe equal toohello number of files.</span></span> <span data-ttu-id="19381-200">Kalan tüm iş parçacıklarının tooincrease kullanabileceğiniz **PerFileThreadCount**.</span><span class="sxs-lookup"><span data-stu-id="19381-200">You can use any remaining threads tooincrease **PerFileThreadCount**.</span></span>

* <span data-ttu-id="19381-201">**Çok fazla iş parçacığı**: iş parçacığı artırırsanız, küme boyutu artırmadan çok fazla sayısı, performans hello riskini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="19381-201">**Too many threads**: If you increase thread count too much without increasing your cluster size, you run hello risk of degraded performance.</span></span> <span data-ttu-id="19381-202">İçerik Geçişi hello CPU üzerinde Çekişme sorunları olabilir.</span><span class="sxs-lookup"><span data-stu-id="19381-202">There can be contention issues when context-switching on hello CPU.</span></span>

* <span data-ttu-id="19381-203">**Yetersiz eşzamanlılık**: hello eşzamanlılık yeterli değildir sonra kümenizi çok küçük olabilir.</span><span class="sxs-lookup"><span data-stu-id="19381-203">**Insufficient concurrency**: If hello concurrency is not sufficient, then your cluster may be too small.</span></span> <span data-ttu-id="19381-204">Daha fazla eşzamanlılık erişmenizi sağlayan kümedeki düğüm sayısını hello artırabilir.</span><span class="sxs-lookup"><span data-stu-id="19381-204">You can increase hello number of nodes in your cluster which will give you more concurrency.</span></span>

* <span data-ttu-id="19381-205">**Azaltma hataları**: Eşzamanlılığınız çok yüksekse azaltma hataları görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19381-205">**Throttling errors**: You may see throttling errors if your concurrency is too high.</span></span> <span data-ttu-id="19381-206">Hataları azaltma görüyorsanız hello eşzamanlılık azaltın veya bize ulaşın.</span><span class="sxs-lookup"><span data-stu-id="19381-206">If you are seeing throttling errors, you should either reduce hello concurrency or contact us.</span></span>

## <a name="next-steps"></a><span data-ttu-id="19381-207">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="19381-207">Next steps</span></span>
* [<span data-ttu-id="19381-208">Data Lake Store'da verilerin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="19381-208">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="19381-209">Azure Data Lake Analytics'i Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="19381-209">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="19381-210">Azure HDInsight'ı Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="19381-210">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

