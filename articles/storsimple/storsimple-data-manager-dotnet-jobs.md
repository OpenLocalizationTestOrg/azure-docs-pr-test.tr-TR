---
title: "Microsoft Azure StorSimple veri Yöneticisi işleri .NET SDK'yı kullanma | Microsoft Docs"
description: "StorSimple veri Yöneticisi işleri (özel olarak incelenmektedir) başlatmak için .NET SDK'sını kullanmayı öğrenin"
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
ms.openlocfilehash: 44d243a034b20b99faf284c8615e470bc6f9d020
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="use-the-net-sdk-to-initiate-data-transformation-private-preview"></a><span data-ttu-id="721f6-103">Veri dönüştürme (özel olarak incelenmektedir) başlatmak için .net SDK'sını kullanın</span><span class="sxs-lookup"><span data-stu-id="721f6-103">Use the .Net SDK to initiate data transformation (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="721f6-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="721f6-104">Overview</span></span>

<span data-ttu-id="721f6-105">Bu makalede, StorSimple cihaz verileri dönüştürmek için StorSimple veri Yöneticisi hizmeti içindeki veri dönüştürme özelliği nasıl kullanabileceğiniz açıklanır.</span><span class="sxs-lookup"><span data-stu-id="721f6-105">This article explains how you can use the data transformation feature within the StorSimple Data Manager service to transform StorSimple device data.</span></span> <span data-ttu-id="721f6-106">Dönüştürülen veriler daha sonra diğer Azure hizmetleriyle bulutta tarafından mı tüketiliyor.</span><span class="sxs-lookup"><span data-stu-id="721f6-106">The transformed data is then consumed by other Azure services in the cloud.</span></span> <span data-ttu-id="721f6-107">Makale ayrıca veri dönüştürme işi başlatmak için örnek bir .NET konsol uygulaması oluşturmaya yardımcı olmak için bir kılavuz vardır ve tamamlanmasını izlemek.</span><span class="sxs-lookup"><span data-stu-id="721f6-107">The article also has a walkthrough to help create a sample .NET console application to initiate a data transformation job and then track it for completion.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="721f6-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="721f6-108">Prerequisites</span></span>

<span data-ttu-id="721f6-109">Başlamadan önce şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="721f6-109">Before you begin, ensure that you have:</span></span>
*   <span data-ttu-id="721f6-110">Visual Studio 2012, 2013, 2015 veya yüklü 2017 sistemiyle.</span><span class="sxs-lookup"><span data-stu-id="721f6-110">A system with Visual Studio 2012, 2013, 2015, or 2017 installed.</span></span>
*   <span data-ttu-id="721f6-111">Azure Powershell yüklü.</span><span class="sxs-lookup"><span data-stu-id="721f6-111">Azure Powershell installed.</span></span> <span data-ttu-id="721f6-112">[Azure Powershell indirme](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="721f6-112">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="721f6-113">Veri dönüştürme işlemini başlatmak için yapılandırma ayarlarını (Bu ayarları almak için yönergeleri dahil burada).</span><span class="sxs-lookup"><span data-stu-id="721f6-113">Configuration settings to initialize the Data Transformation job (instructions to obtain these settings are included here).</span></span>
*   <span data-ttu-id="721f6-114">Bir kaynak grubu içinde karma veri kaynağındaki doğru şekilde yapılandırılmış bir iş tanımı.</span><span class="sxs-lookup"><span data-stu-id="721f6-114">A job definition that has been correctly configured in a Hybrid Data Resource within a Resource Group.</span></span>
*   <span data-ttu-id="721f6-115">Tüm gerekli DLL'leri.</span><span class="sxs-lookup"><span data-stu-id="721f6-115">All the required dlls.</span></span> <span data-ttu-id="721f6-116">Bu DLL'lerden karşıdan [GitHub deposunu](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span><span class="sxs-lookup"><span data-stu-id="721f6-116">Download these dlls from the [GitHub repository](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span></span>
*   <span data-ttu-id="721f6-117">`Get-ConfigurationParams.ps1`[betik](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) github'da depodan.</span><span class="sxs-lookup"><span data-stu-id="721f6-117">`Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) from the github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="721f6-118">Adım adım</span><span class="sxs-lookup"><span data-stu-id="721f6-118">Step-by-step</span></span>

<span data-ttu-id="721f6-119">Veri dönüştürme işi başlatmak için .NET kullanmak için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="721f6-119">Perform the following steps to use .NET to launch a data transformation job.</span></span>

1. <span data-ttu-id="721f6-120">Yapılandırma parametreleri almak için aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="721f6-120">To retrieve the configuration parameters, do the following steps:</span></span>
    1. <span data-ttu-id="721f6-121">Karşıdan `Get-ConfigurationParams.ps1` github depo komut `C:\DataTransformation` konumu.</span><span class="sxs-lookup"><span data-stu-id="721f6-121">Download the `Get-ConfigurationParams.ps1` from the github repository script in `C:\DataTransformation` location.</span></span>
    1. <span data-ttu-id="721f6-122">Çalıştırma `Get-ConfigurationParams.ps1` github deposuna betikten.</span><span class="sxs-lookup"><span data-stu-id="721f6-122">Run the `Get-ConfigurationParams.ps1` script from the github repository.</span></span> <span data-ttu-id="721f6-123">Aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="721f6-123">Type the following command:</span></span>

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        <span data-ttu-id="721f6-124">AppName ve ActiveDirectoryKey için herhangi bir değer geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="721f6-124">You can pass in any values for the ActiveDirectoryKey and AppName.</span></span>


2. <span data-ttu-id="721f6-125">Bu komut dosyasını aşağıdaki değerleri çıkarır:</span><span class="sxs-lookup"><span data-stu-id="721f6-125">This script outputs the following values:</span></span>
    * <span data-ttu-id="721f6-126">İstemci kimliği</span><span class="sxs-lookup"><span data-stu-id="721f6-126">Client ID</span></span>
    * <span data-ttu-id="721f6-127">Kiracı Kimliği</span><span class="sxs-lookup"><span data-stu-id="721f6-127">Tenant ID</span></span>
    * <span data-ttu-id="721f6-128">Active Directory anahtar (aynı Yukarıda girilen)</span><span class="sxs-lookup"><span data-stu-id="721f6-128">Active Directory key (same as the one entered above)</span></span>
    * <span data-ttu-id="721f6-129">Abonelik Kimliği</span><span class="sxs-lookup"><span data-stu-id="721f6-129">Subscription ID</span></span>

3. <span data-ttu-id="721f6-130">Visual Studio 2012 kullanarak, 2013 veya 2015, C# .NET konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="721f6-130">Using Visual Studio 2012, 2013 or 2015, create a C# .NET console application.</span></span>

    1. <span data-ttu-id="721f6-131">Başlatma **Visual Studio 2012/2013/2015**.</span><span class="sxs-lookup"><span data-stu-id="721f6-131">Launch **Visual Studio 2012/2013/2015**.</span></span>
    1. <span data-ttu-id="721f6-132">**Dosya**’ya tıklayın, **Yeni**’nin üzerine gelin ve **Proje**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="721f6-132">Click **File**, point to **New**, and click **Project**.</span></span>
    2. <span data-ttu-id="721f6-133">**Şablonlar**’ı genişletin ve **Visual C#** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="721f6-133">Expand **Templates**, and select **Visual C#**.</span></span>
    3. <span data-ttu-id="721f6-134">Sağ taraftaki proje türleri listesinden **Konsol Uygulaması**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="721f6-134">Select **Console Application** from the list of project types on the right.</span></span>
    4. <span data-ttu-id="721f6-135">Girin **DataTransformationApp** için **adı**.</span><span class="sxs-lookup"><span data-stu-id="721f6-135">Enter **DataTransformationApp** for the **Name**.</span></span>
    5. <span data-ttu-id="721f6-136">Seçin **C:\DataTransformation** için **konumu**.</span><span class="sxs-lookup"><span data-stu-id="721f6-136">Select **C:\DataTransformation** for the **Location**.</span></span>
    6. <span data-ttu-id="721f6-137">Projeyi oluşturmak için **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="721f6-137">Click **OK** to create the project.</span></span>

4.  <span data-ttu-id="721f6-138">Şimdi, mevcut tüm DLL'ler ekleyin [DLL'leri](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) klasörü olarak **başvuruları** oluşturduğunuz projesinde.</span><span class="sxs-lookup"><span data-stu-id="721f6-138">Now, add all DLLs present in the [dlls](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) folder as **References** in the project that you created.</span></span> <span data-ttu-id="721f6-139">Dll dosyaları indirmek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="721f6-139">To download the dll files, do the following:</span></span>

    1. <span data-ttu-id="721f6-140">Visual Studio'da Git **Görünüm > Çözüm Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="721f6-140">In Visual Studio, go to **View > Solution Explorer**.</span></span>
    1. <span data-ttu-id="721f6-141">Veri dönüştürme uygulama projesi solundaki oka tıklayın.</span><span class="sxs-lookup"><span data-stu-id="721f6-141">Click the arrow to the left of Data Transformation App project.</span></span> <span data-ttu-id="721f6-142">Tıklatın **başvuruları** ve ardından sağ tıklatarak **Başvuru Ekle**.</span><span class="sxs-lookup"><span data-stu-id="721f6-142">Click **References** and then right-click to **Add Reference**.</span></span>
    2. <span data-ttu-id="721f6-143">Paketleri klasör konumuna göz atın, tüm DLL'ler seçin ve tıklatın **Ekle**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="721f6-143">Browse to the location of the packages folder, select all the DLLs and click **Add**, and then click **OK**.</span></span>

5. <span data-ttu-id="721f6-144">Aşağıdaki **using** bildirimlerini projedeki kaynak dosyasına (Program.cs) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="721f6-144">Add the following **using** statements to the source file (Program.cs) in the project.</span></span>

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. <span data-ttu-id="721f6-145">Aşağıdaki kod, veri dönüştürme işi örneği başlatır.</span><span class="sxs-lookup"><span data-stu-id="721f6-145">The following code initializes the data transformation job instance.</span></span> <span data-ttu-id="721f6-146">Bu konuda eklemek **Main yönteminin**.</span><span class="sxs-lookup"><span data-stu-id="721f6-146">Add this in the **Main method**.</span></span> <span data-ttu-id="721f6-147">Yapılandırma parametrelerinin değerlerini daha önce edindiğiniz şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="721f6-147">Replace the values of configuration parameters as obtained earlier.</span></span> <span data-ttu-id="721f6-148">Değerlerini içinde takın **kaynak grubu adı** ve **karma veri kaynağı adı**.</span><span class="sxs-lookup"><span data-stu-id="721f6-148">Plug in the values of **Resource Group Name** and **Hybrid Data Resource name**.</span></span> <span data-ttu-id="721f6-149">**Kaynak grubu adı** iş tanımı yapılandırılmışsa karma veri kaynağı barındıran sunucudur.</span><span class="sxs-lookup"><span data-stu-id="721f6-149">The **Resource Group Name** is the one that hosts the Hybrid Data Resource on which the job definition was configured.</span></span>

    ```
    // Setup the configuration parameters.
    var configParams = new ConfigurationParams
    {
        ClientId = "client-id",
        TenantId = "tenant-id",
        ActiveDirectoryKey = "active-directory-key",
        SubscriptionId = "subscription-id",
        ResourceGroupName = "resource-group-name",
        ResourceName = "resource-name"
    };

    // Initialize the Data Transformation Job instance.
    DataTransformationJob dataTransformationJob = new DataTransformationJob(configParams);

    ```

7. <span data-ttu-id="721f6-150">Hangi iş tanımı çalıştırılması gerektiğini parametrelerini belirtin</span><span class="sxs-lookup"><span data-stu-id="721f6-150">Specify the parameters with which the job definition needs to be run</span></span>

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    <span data-ttu-id="721f6-151">(VEYA)</span><span class="sxs-lookup"><span data-stu-id="721f6-151">(OR)</span></span>

    <span data-ttu-id="721f6-152">Çalışma zamanı sırasında iş tanımı parametrelerini değiştirmek istiyorsanız, aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="721f6-152">If you want to change the job definition parameters during run time, then add the following code:</span></span>

    ```
    string jobDefinitionName = "job-definition-name";
    // Must start with a '\'
    var rootDirectories = new List<string> {@"\root"};

    // Name of the volume on the StorSimple device.
    var volumeNames = new List<string> {"volume-name"};

    var dataTransformationInput = new DataTransformationInput
    {
        // If you require the latest existing backup to be picked else use TakeNow to trigger a new backup.
        BackupChoice = BackupChoice.UseExistingLatest.ToString(),
        // Name of the StorSimple device.
        DeviceName = "device-name",
        // Name of the container in Azure storage where the files will be placed after execution.
        ContainerName = "container-name",
        // File name filter (search pattern) to be applied on files under the root directory. * - Match all files.
        FileNameFilter = "*",
        // List of root directories.
        RootDirectories = rootDirectories,
        // Name of the volume on StorSimple device on which the relevant data is present. 
        VolumeNames = volumeNames
    };
    
    ```

8. <span data-ttu-id="721f6-153">Başlatma iş tanımı bir veri dönüştürme işi tetiklemek için aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="721f6-153">After the initialization, add the following code to trigger a data transformation job on the job definition.</span></span> <span data-ttu-id="721f6-154">Uygun takın **iş tanımı adını**.</span><span class="sxs-lookup"><span data-stu-id="721f6-154">Plug in the appropriate **Job Definition Name**.</span></span>

    ```
    // Trigger a job, retrieve the jobId and the retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. <span data-ttu-id="721f6-155">Bu iş StorSimple birim kök dizininin altındaki mevcut eşleşen dosyaları belirtilen kapsayıcı yükler.</span><span class="sxs-lookup"><span data-stu-id="721f6-155">This job uploads the matched files present under the root directory on the StorSimple volume to the specified container.</span></span> <span data-ttu-id="721f6-156">Bir dosyayı karşıya yüklendiğinde, bir ileti sırasına (aynı depolama hesabındaki kapsayıcı olarak) iş tanımı aynı ada sahip bırakılır.</span><span class="sxs-lookup"><span data-stu-id="721f6-156">When a file is uploaded, a message is dropped in the queue (in the same storage account as the container) with the same name as the job definition.</span></span> <span data-ttu-id="721f6-157">Bu ileti her dosyanın işlenmesi başlatmak için bir tetikleyici olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="721f6-157">This message can be used as a trigger to initiate any further processing of the file.</span></span>

10. <span data-ttu-id="721f6-158">İş tetiklendi sonra iş için tamamlanma izlemek için aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="721f6-158">Once the job has been triggered, add the following code to track the job for completion.</span></span>

    ```
    Job jobDetails = null;

    // Poll the job.
    do
    {
        jobDetails = dataTransformationJob.GetJob(jobDefinitionName, jobId);

        // Wait before polling for the status again.
        Thread.Sleep(TimeSpan.FromSeconds(retryAfter));

    } while (jobDetails.Status == JobStatus.InProgress);

    // Completion status of the job.
    Console.WriteLine("JobStatus: {0}", jobDetails.Status);
    
    // To hold the console before exiting.
    Console.Read();

    ```


## <a name="next-steps"></a><span data-ttu-id="721f6-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="721f6-159">Next steps</span></span>

<span data-ttu-id="721f6-160">[StorSimple veri Yöneticisi'ni kullanın, verilerinizi dönüştürmek için kullanıcı Arabirimi](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="721f6-160">[Use StorSimple Data Manager UI to transform your data](storsimple-data-manager-ui.md).</span></span>
