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
# <a name="use-hello-net-sdk-tooinitiate-data-transformation-private-preview"></a>Kullanım .net SDK hello tooinitiate veri dönüştürme (özel olarak incelenmektedir)

## <a name="overview"></a>Genel Bakış

Bu makalede hello veri dönüştürme özelliğini hello StorSimple veri Yöneticisi hizmeti tootransform StorSimple cihaz verileri içinde nasıl kullanabileceğiniz açıklanır. Merhaba dönüştürülen veriler daha sonra diğer Azure hizmetleriyle hello bulutta tarafından kullanılır. Merhaba makale ayrıca bir örnek .NET konsol uygulaması tooinitiate veri dönüştürme işi oluşturmak ve tamamlanmasını izlemek izlenecek toohelp sahiptir.

## <a name="prerequisites"></a>Ön koşullar

Başlamadan önce şunları yapın:
*   Visual Studio 2012, 2013, 2015 veya yüklü 2017 sistemiyle.
*   Azure Powershell yüklü. [Azure Powershell indirme](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
*   Yapılandırma ayarları tooinitialize hello veri dönüştürme işi (yönergeleri tooobtain bu ayarları buraya dahil).
*   Bir kaynak grubu içinde karma veri kaynağındaki doğru şekilde yapılandırılmış bir iş tanımı.
*   Tüm gerekli hello DLL'ler. Bu DLL'ler hello indirme [GitHub deposunu](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).
*   `Get-ConfigurationParams.ps1`[betik](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) hello github'da depodan.

## <a name="step-by-step"></a>Adım adım

Aşağıdaki adımları toouse .NET toolaunch veri dönüştürme işi hello gerçekleştirin.

1. tooretrieve hello yapılandırma parametreleri de adımları izleyerek hello:
    1. Merhaba karşıdan `Get-ConfigurationParams.ps1` hello github depo komut dosyasından `C:\DataTransformation` konumu.
    1. Merhaba çalıştırmak `Get-ConfigurationParams.ps1` hello github deposunu betikten. Merhaba aşağıdaki komutu yazın:

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        ActiveDirectoryKey ve AppName hello için herhangi bir değer geçirebilirsiniz.


2. Bu komut dosyası değerlerini aşağıdaki hello çıkarır:
    * İstemci kimliği
    * Kiracı Kimliği
    * Active Directory anahtar (bir Yukarıda girilen hello ile aynı)
    * Abonelik Kimliği

3. Visual Studio 2012 kullanarak, 2013 veya 2015, C# .NET konsol uygulaması oluşturun.

    1. Başlatma **Visual Studio 2012/2013/2015**.
    1. Tıklatın **dosya**, çok noktası**yeni**, tıklatıp **proje**.
    2. **Şablonlar**’ı genişletin ve **Visual C#** seçeneğini belirleyin.
    3. Seçin **konsol uygulaması** hello sağ proje türlerinde hello listesinden.
    4. Girin **DataTransformationApp** hello için **adı**.
    5. Seçin **C:\DataTransformation** hello için **konumu**.
    6. Tıklatın **Tamam** toocreate hello projesi.

4.  Şimdi, tüm DLL'ler hello mevcut ekleyin [DLL'leri](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) klasörü olarak **başvuruları** oluşturduğunuz hello projesinde. toodownload hello dll dosyaları hello aşağıdaki:

    1. Visual Studio'da çok gidin**Görünüm > Çözüm Gezgini**.
    1. Veri dönüştürme uygulaması projesinin Hello ok toohello sol tıklayın. Tıklatın **başvuruları** ve çok sağ**Başvuru Ekle**.
    2. Hello paketler klasörü toohello konumunu bulun, tüm hello DLL'ler seçin ve tıklatın **Ekle**ve ardından **Tamam**.

5. Merhaba aşağıdakileri ekleyin **kullanarak** hello projesindeki deyimleri toohello kaynak dosyasını (Program.cs).

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. koddan hello hello veri dönüştürme işi örneği başlatır. Bu hello eklemek **Main yönteminin**. Daha önce edindiğiniz gibi yapılandırma parametreleri Hello değerlerini değiştirin. Merhaba değerlerini içinde takın **kaynak grubu adı** ve **karma veri kaynağı adı**. Merhaba **kaynak grubu adı** hello hello karma veri kaynağı üzerinde hangi hello iş tanımı yapılandırılmışsa barındıran biridir.

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

7. Hangi hello ile iş tanımı toobe gereken parametreleri çalıştırın hello belirtin

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    (VEYA)

    Çalışma zamanı sırasında toochange hello iş tanımı parametrelerini istiyorsanız, hello aşağıdaki kodu ekleyin:

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

8. Hello başlatma sonra aşağıdaki kodu tootrigger hello iş tanımı bir veri dönüştürme işi hello ekleyin. Merhaba uygun takın **iş tanımı adını**.

    ```
    // Trigger a job, retrieve hello jobId and hello retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. Bu iş hello StorSimple birim toohello belirtilen kapsayıcısı üzerinde hello kök dizininin altında mevcut hello eşleşen dosyaları karşıya yükler. Bir dosyayı karşıya yüklendiğinde, bir ileti hello sırada bırakılan (Merhaba içinde hello kapsayıcı aynı depolama hesabı) hello ile aynı hello iş tanımı adlandırın. Bu iletiyi başka hello dosyasının işlemeyi bir tetikleyici tooinitiate kullanılabilir.

10. Merhaba iş tetiklendi sonra aşağıdaki kodu tootrack hello iş tamamlanma hello ekleyin.

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


## <a name="next-steps"></a>Sonraki adımlar

[StorSimple veri Yöneticisi kullanıcı Arabirimi tootransform verilerinizi kullanma](storsimple-data-manager-ui.md).
