---
title: "Microsoft Azure StorSimple veri Yöneticisi işleri için .NET SDK'sı aaaUse | Microsoft Docs"
description: "Toouse .NET SDK'sı toolaunch StorSimple veri Yöneticisi'ni (özel olarak incelenmektedir) nasıl işler öğrenin"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: b07fe64369574c994fd28d42786aa02dca435ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-net-sdk-tooinitiate-data-transformation-private-preview"></a><span data-ttu-id="35941-103">Kullanım .net SDK hello tooinitiate veri dönüştürme (özel olarak incelenmektedir)</span><span class="sxs-lookup"><span data-stu-id="35941-103">Use hello .Net SDK tooinitiate data transformation (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="35941-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="35941-104">Overview</span></span>

<span data-ttu-id="35941-105">Bu makalede hello veri dönüştürme özelliğini hello StorSimple veri Yöneticisi hizmeti tootransform StorSimple cihaz verileri içinde nasıl kullanabileceğiniz açıklanır.</span><span class="sxs-lookup"><span data-stu-id="35941-105">This article explains how you can use hello data transformation feature within hello StorSimple Data Manager service tootransform StorSimple device data.</span></span> <span data-ttu-id="35941-106">Merhaba dönüştürülen veriler daha sonra diğer Azure hizmetleriyle hello bulutta tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="35941-106">hello transformed data is then consumed by other Azure services in hello cloud.</span></span> <span data-ttu-id="35941-107">Merhaba makale ayrıca bir örnek .NET konsol uygulaması tooinitiate veri dönüştürme işi oluşturmak ve tamamlanmasını izlemek izlenecek toohelp sahiptir.</span><span class="sxs-lookup"><span data-stu-id="35941-107">hello article also has a walkthrough toohelp create a sample .NET console application tooinitiate a data transformation job and then track it for completion.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35941-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="35941-108">Prerequisites</span></span>

<span data-ttu-id="35941-109">Başlamadan önce şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="35941-109">Before you begin, ensure that you have:</span></span>
*   <span data-ttu-id="35941-110">Visual Studio 2012, 2013, 2015 veya yüklü 2017 sistemiyle.</span><span class="sxs-lookup"><span data-stu-id="35941-110">A system with Visual Studio 2012, 2013, 2015, or 2017 installed.</span></span>
*   <span data-ttu-id="35941-111">Azure Powershell yüklü.</span><span class="sxs-lookup"><span data-stu-id="35941-111">Azure Powershell installed.</span></span> <span data-ttu-id="35941-112">[Azure Powershell indirme](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="35941-112">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="35941-113">Yapılandırma ayarları tooinitialize hello veri dönüştürme işi (yönergeleri tooobtain bu ayarları buraya dahil).</span><span class="sxs-lookup"><span data-stu-id="35941-113">Configuration settings tooinitialize hello Data Transformation job (instructions tooobtain these settings are included here).</span></span>
*   <span data-ttu-id="35941-114">Bir kaynak grubu içinde karma veri kaynağındaki doğru şekilde yapılandırılmış bir iş tanımı.</span><span class="sxs-lookup"><span data-stu-id="35941-114">A job definition that has been correctly configured in a Hybrid Data Resource within a Resource Group.</span></span>
*   <span data-ttu-id="35941-115">Tüm gerekli hello DLL'ler.</span><span class="sxs-lookup"><span data-stu-id="35941-115">All hello required dlls.</span></span> <span data-ttu-id="35941-116">Bu DLL'ler hello indirme [GitHub deposunu](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span><span class="sxs-lookup"><span data-stu-id="35941-116">Download these dlls from hello [GitHub repository](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span></span>
*   <span data-ttu-id="35941-117">`Get-ConfigurationParams.ps1`[betik](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) hello github'da depodan.</span><span class="sxs-lookup"><span data-stu-id="35941-117">`Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) from hello github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="35941-118">Adım adım</span><span class="sxs-lookup"><span data-stu-id="35941-118">Step-by-step</span></span>

<span data-ttu-id="35941-119">Aşağıdaki adımları toouse .NET toolaunch veri dönüştürme işi hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="35941-119">Perform hello following steps toouse .NET toolaunch a data transformation job.</span></span>

1. <span data-ttu-id="35941-120">tooretrieve hello yapılandırma parametreleri de adımları izleyerek hello:</span><span class="sxs-lookup"><span data-stu-id="35941-120">tooretrieve hello configuration parameters, do hello following steps:</span></span>
    1. <span data-ttu-id="35941-121">Merhaba karşıdan `Get-ConfigurationParams.ps1` hello github depo komut dosyasından `C:\DataTransformation` konumu.</span><span class="sxs-lookup"><span data-stu-id="35941-121">Download hello `Get-ConfigurationParams.ps1` from hello github repository script in `C:\DataTransformation` location.</span></span>
    1. <span data-ttu-id="35941-122">Merhaba çalıştırmak `Get-ConfigurationParams.ps1` hello github deposunu betikten.</span><span class="sxs-lookup"><span data-stu-id="35941-122">Run hello `Get-ConfigurationParams.ps1` script from hello github repository.</span></span> <span data-ttu-id="35941-123">Merhaba aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="35941-123">Type hello following command:</span></span>

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        <span data-ttu-id="35941-124">ActiveDirectoryKey ve AppName hello için herhangi bir değer geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="35941-124">You can pass in any values for hello ActiveDirectoryKey and AppName.</span></span>


2. <span data-ttu-id="35941-125">Bu komut dosyası değerlerini aşağıdaki hello çıkarır:</span><span class="sxs-lookup"><span data-stu-id="35941-125">This script outputs hello following values:</span></span>
    * <span data-ttu-id="35941-126">İstemci kimliği</span><span class="sxs-lookup"><span data-stu-id="35941-126">Client ID</span></span>
    * <span data-ttu-id="35941-127">Kiracı Kimliği</span><span class="sxs-lookup"><span data-stu-id="35941-127">Tenant ID</span></span>
    * <span data-ttu-id="35941-128">Active Directory anahtar (bir Yukarıda girilen hello ile aynı)</span><span class="sxs-lookup"><span data-stu-id="35941-128">Active Directory key (same as hello one entered above)</span></span>
    * <span data-ttu-id="35941-129">Abonelik Kimliği</span><span class="sxs-lookup"><span data-stu-id="35941-129">Subscription ID</span></span>

3. <span data-ttu-id="35941-130">Visual Studio 2012 kullanarak, 2013 veya 2015, C# .NET konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="35941-130">Using Visual Studio 2012, 2013 or 2015, create a C# .NET console application.</span></span>

    1. <span data-ttu-id="35941-131">Başlatma **Visual Studio 2012/2013/2015**.</span><span class="sxs-lookup"><span data-stu-id="35941-131">Launch **Visual Studio 2012/2013/2015**.</span></span>
    1. <span data-ttu-id="35941-132">Tıklatın **dosya**, çok noktası**yeni**, tıklatıp **proje**.</span><span class="sxs-lookup"><span data-stu-id="35941-132">Click **File**, point too**New**, and click **Project**.</span></span>
    2. <span data-ttu-id="35941-133">**Şablonlar**’ı genişletin ve **Visual C#** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="35941-133">Expand **Templates**, and select **Visual C#**.</span></span>
    3. <span data-ttu-id="35941-134">Seçin **konsol uygulaması** hello sağ proje türlerinde hello listesinden.</span><span class="sxs-lookup"><span data-stu-id="35941-134">Select **Console Application** from hello list of project types on hello right.</span></span>
    4. <span data-ttu-id="35941-135">Girin **DataTransformationApp** hello için **adı**.</span><span class="sxs-lookup"><span data-stu-id="35941-135">Enter **DataTransformationApp** for hello **Name**.</span></span>
    5. <span data-ttu-id="35941-136">Seçin **C:\DataTransformation** hello için **konumu**.</span><span class="sxs-lookup"><span data-stu-id="35941-136">Select **C:\DataTransformation** for hello **Location**.</span></span>
    6. <span data-ttu-id="35941-137">Tıklatın **Tamam** toocreate hello projesi.</span><span class="sxs-lookup"><span data-stu-id="35941-137">Click **OK** toocreate hello project.</span></span>

4.  <span data-ttu-id="35941-138">Şimdi, tüm DLL'ler hello mevcut ekleyin [DLL'leri](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) klasörü olarak **başvuruları** oluşturduğunuz hello projesinde.</span><span class="sxs-lookup"><span data-stu-id="35941-138">Now, add all DLLs present in hello [dlls](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) folder as **References** in hello project that you created.</span></span> <span data-ttu-id="35941-139">toodownload hello dll dosyaları hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="35941-139">toodownload hello dll files, do hello following:</span></span>

    1. <span data-ttu-id="35941-140">Visual Studio'da çok gidin**Görünüm > Çözüm Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="35941-140">In Visual Studio, go too**View > Solution Explorer**.</span></span>
    1. <span data-ttu-id="35941-141">Veri dönüştürme uygulaması projesinin Hello ok toohello sol tıklayın.</span><span class="sxs-lookup"><span data-stu-id="35941-141">Click hello arrow toohello left of Data Transformation App project.</span></span> <span data-ttu-id="35941-142">Tıklatın **başvuruları** ve çok sağ**Başvuru Ekle**.</span><span class="sxs-lookup"><span data-stu-id="35941-142">Click **References** and then right-click too**Add Reference**.</span></span>
    2. <span data-ttu-id="35941-143">Hello paketler klasörü toohello konumunu bulun, tüm hello DLL'ler seçin ve tıklatın **Ekle**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="35941-143">Browse toohello location of hello packages folder, select all hello DLLs and click **Add**, and then click **OK**.</span></span>

5. <span data-ttu-id="35941-144">Merhaba aşağıdakileri ekleyin **kullanarak** hello projesindeki deyimleri toohello kaynak dosyasını (Program.cs).</span><span class="sxs-lookup"><span data-stu-id="35941-144">Add hello following **using** statements toohello source file (Program.cs) in hello project.</span></span>

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. <span data-ttu-id="35941-145">koddan hello hello veri dönüştürme işi örneği başlatır.</span><span class="sxs-lookup"><span data-stu-id="35941-145">hello following code initializes hello data transformation job instance.</span></span> <span data-ttu-id="35941-146">Bu hello eklemek **Main yönteminin**.</span><span class="sxs-lookup"><span data-stu-id="35941-146">Add this in hello **Main method**.</span></span> <span data-ttu-id="35941-147">Daha önce edindiğiniz gibi yapılandırma parametreleri Hello değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="35941-147">Replace hello values of configuration parameters as obtained earlier.</span></span> <span data-ttu-id="35941-148">Merhaba değerlerini içinde takın **kaynak grubu adı** ve **karma veri kaynağı adı**.</span><span class="sxs-lookup"><span data-stu-id="35941-148">Plug in hello values of **Resource Group Name** and **Hybrid Data Resource name**.</span></span> <span data-ttu-id="35941-149">Merhaba **kaynak grubu adı** hello hello karma veri kaynağı üzerinde hangi hello iş tanımı yapılandırılmışsa barındıran biridir.</span><span class="sxs-lookup"><span data-stu-id="35941-149">hello **Resource Group Name** is hello one that hosts hello Hybrid Data Resource on which hello job definition was configured.</span></span>

    ```
    // Setup hello configuration parameters.
    var configParams = new ConfigurationParams
    {
        ClientId = "client-id",
        TenantId = "tenant-id",
        ActiveDirectoryKey = "active-directory-key",
        SubscriptionId = "subscription-id",
        ResourceGroupName = "resource-group-name",
        ResourceName = "resource-name"
    };

    // Initialize hello Data Transformation Job instance.
    DataTransformationJob dataTransformationJob = new DataTransformationJob(configParams);

    ```

7. <span data-ttu-id="35941-150">Hangi hello ile iş tanımı toobe gereken parametreleri çalıştırın hello belirtin</span><span class="sxs-lookup"><span data-stu-id="35941-150">Specify hello parameters with which hello job definition needs toobe run</span></span>

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    <span data-ttu-id="35941-151">(VEYA)</span><span class="sxs-lookup"><span data-stu-id="35941-151">(OR)</span></span>

    <span data-ttu-id="35941-152">Çalışma zamanı sırasında toochange hello iş tanımı parametrelerini istiyorsanız, hello aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="35941-152">If you want toochange hello job definition parameters during run time, then add hello following code:</span></span>

    ```
    string jobDefinitionName = "job-definition-name";
    // Must start with a '\'
    var rootDirectories = new List<string> {@"\root"};

    // Name of hello volume on hello StorSimple device.
    var volumeNames = new List<string> {"volume-name"};

    var dataTransformationInput = new DataTransformationInput
    {
        // If you require hello latest existing backup toobe picked else use TakeNow tootrigger a new backup.
        BackupChoice = BackupChoice.UseExistingLatest.ToString(),
        // Name of hello StorSimple device.
        DeviceName = "device-name",
        // Name of hello container in Azure storage where hello files will be placed after execution.
        ContainerName = "container-name",
        // File name filter (search pattern) toobe applied on files under hello root directory. * - Match all files.
        FileNameFilter = "*",
        // List of root directories.
        RootDirectories = rootDirectories,
        // Name of hello volume on StorSimple device on which hello relevant data is present. 
        VolumeNames = volumeNames
    };
    
    ```

8. <span data-ttu-id="35941-153">Hello başlatma sonra aşağıdaki kodu tootrigger hello iş tanımı bir veri dönüştürme işi hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="35941-153">After hello initialization, add hello following code tootrigger a data transformation job on hello job definition.</span></span> <span data-ttu-id="35941-154">Merhaba uygun takın **iş tanımı adını**.</span><span class="sxs-lookup"><span data-stu-id="35941-154">Plug in hello appropriate **Job Definition Name**.</span></span>

    ```
    // Trigger a job, retrieve hello jobId and hello retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. <span data-ttu-id="35941-155">Bu iş hello StorSimple birim toohello belirtilen kapsayıcısı üzerinde hello kök dizininin altında mevcut hello eşleşen dosyaları karşıya yükler.</span><span class="sxs-lookup"><span data-stu-id="35941-155">This job uploads hello matched files present under hello root directory on hello StorSimple volume toohello specified container.</span></span> <span data-ttu-id="35941-156">Bir dosyayı karşıya yüklendiğinde, bir ileti hello sırada bırakılan (Merhaba içinde hello kapsayıcı aynı depolama hesabı) hello ile aynı hello iş tanımı adlandırın.</span><span class="sxs-lookup"><span data-stu-id="35941-156">When a file is uploaded, a message is dropped in hello queue (in hello same storage account as hello container) with hello same name as hello job definition.</span></span> <span data-ttu-id="35941-157">Bu iletiyi başka hello dosyasının işlemeyi bir tetikleyici tooinitiate kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="35941-157">This message can be used as a trigger tooinitiate any further processing of hello file.</span></span>

10. <span data-ttu-id="35941-158">Merhaba iş tetiklendi sonra aşağıdaki kodu tootrack hello iş tamamlanma hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="35941-158">Once hello job has been triggered, add hello following code tootrack hello job for completion.</span></span>

    ```
    Job jobDetails = null;

    // Poll hello job.
    do
    {
        jobDetails = dataTransformationJob.GetJob(jobDefinitionName, jobId);

        // Wait before polling for hello status again.
        Thread.Sleep(TimeSpan.FromSeconds(retryAfter));

    } while (jobDetails.Status == JobStatus.InProgress);

    // Completion status of hello job.
    Console.WriteLine("JobStatus: {0}", jobDetails.Status);
    
    // toohold hello console before exiting.
    Console.Read();

    ```


## <a name="next-steps"></a><span data-ttu-id="35941-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="35941-159">Next steps</span></span>

<span data-ttu-id="35941-160">[StorSimple veri Yöneticisi kullanıcı Arabirimi tootransform verilerinizi kullanma](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="35941-160">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
