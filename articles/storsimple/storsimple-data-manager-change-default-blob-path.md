---
title: "Varsayılan blob yolu Değiştir | Microsoft Docs"
description: "Bir blob dosya yolu (özel olarak incelenmektedir) yeniden adlandırmak için bir Azure işlevini ayarlamak öğrenin"
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
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 057d4d7370207859617eb63238bf425bfa6d3e16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="change-a-blob-path-from-the-default-path-private-preview"></a><span data-ttu-id="2a76c-103">Varsayılan yol (özel olarak incelenmektedir) blob yolunu değiştirme</span><span class="sxs-lookup"><span data-stu-id="2a76c-103">Change a blob path from the default path (private preview)</span></span>

<span data-ttu-id="2a76c-104">Bu makalede, bir varsayılan blob dosya yolu yeniden adlandırmak için bir Azure işlevini ayarlamak açıklar.</span><span class="sxs-lookup"><span data-stu-id="2a76c-104">This article describes how to set up an Azure function to rename a default blob file path.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2a76c-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2a76c-105">Prerequisites</span></span>

<span data-ttu-id="2a76c-106">Bir kaynak grubu içinde karma veri kaynağındaki doğru şekilde yapılandırılmış bir iş tanımı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="2a76c-106">Ensure that you have a job definition that has been correctly configured in a hybrid data resource within a resource group.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="2a76c-107">Bir Azure işlevi oluşturma</span><span class="sxs-lookup"><span data-stu-id="2a76c-107">Create an Azure function</span></span>

<span data-ttu-id="2a76c-108">Bir Azure işlevi oluşturmak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="2a76c-108">To create an Azure function, do the following:</span></span>

1. <span data-ttu-id="2a76c-109">[Azure Portal](http://portal.azure.com/) gidin.</span><span class="sxs-lookup"><span data-stu-id="2a76c-109">Go to the [Azure portal](http://portal.azure.com/).</span></span>

2. <span data-ttu-id="2a76c-110">Sol bölmenin en üstünde tıklatın **yeni**.</span><span class="sxs-lookup"><span data-stu-id="2a76c-110">At the top of the left pane, click **New**.</span></span> 

3. <span data-ttu-id="2a76c-111">İçinde **arama** kutusuna **işlev uygulaması**, ve ardından Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="2a76c-111">In the **Search** box, type **Function App**, and then press Enter.</span></span>

    ![Arama kutusuna "İşlev uygulaması" yazın](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. <span data-ttu-id="2a76c-113">İçinde **sonuçları** tıklatın **işlev uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="2a76c-113">In the **Results** list, click **Function App**.</span></span>

    ![Sonuçlar listesinde işlevi Uygulama kaynağı seçin](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    <span data-ttu-id="2a76c-115">**İşlev uygulaması** penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="2a76c-115">The **Function App** window opens.</span></span>

5. <span data-ttu-id="2a76c-116">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2a76c-116">Click **Create**.</span></span>

    ![İşlev uygulaması penceresini "Oluştur" düğmesine](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. <span data-ttu-id="2a76c-118">Üzerinde **işlev uygulaması** yapılandırma dikey penceresinde aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="2a76c-118">On the **Function App** configuration blade, do the following:</span></span>

    <span data-ttu-id="2a76c-119">a.</span><span class="sxs-lookup"><span data-stu-id="2a76c-119">a.</span></span> <span data-ttu-id="2a76c-120">İçinde **uygulama adı** kutusunda, uygulama adını yazın.</span><span class="sxs-lookup"><span data-stu-id="2a76c-120">In the **App name** box, type the app name.</span></span>
    
    <span data-ttu-id="2a76c-121">b.</span><span class="sxs-lookup"><span data-stu-id="2a76c-121">b.</span></span> <span data-ttu-id="2a76c-122">İçinde **abonelik** abonelik adını yazın.</span><span class="sxs-lookup"><span data-stu-id="2a76c-122">In the **Subscription** box, type the name of the subscription.</span></span>

    <span data-ttu-id="2a76c-123">c.</span><span class="sxs-lookup"><span data-stu-id="2a76c-123">c.</span></span> <span data-ttu-id="2a76c-124">Altında **kaynak grubu**, tıklatın **Yeni Oluştur**ve ardından kaynak grubunun adını yazın.</span><span class="sxs-lookup"><span data-stu-id="2a76c-124">Under **Resource Group**, click **Create new**, and then type the name of the resource group.</span></span>

    <span data-ttu-id="2a76c-125">d.</span><span class="sxs-lookup"><span data-stu-id="2a76c-125">d.</span></span> <span data-ttu-id="2a76c-126">İçinde **barındırma planına** kutusuna **tüketim planlama**.</span><span class="sxs-lookup"><span data-stu-id="2a76c-126">In the **Hosting Plan** box, type **Consumption Plan**.</span></span>

    <span data-ttu-id="2a76c-127">e.</span><span class="sxs-lookup"><span data-stu-id="2a76c-127">e.</span></span> <span data-ttu-id="2a76c-128">İçinde **konumu** konumunu yazın.</span><span class="sxs-lookup"><span data-stu-id="2a76c-128">In the **Location** box, type the location.</span></span>

    <span data-ttu-id="2a76c-129">f.</span><span class="sxs-lookup"><span data-stu-id="2a76c-129">f.</span></span> <span data-ttu-id="2a76c-130">Altında **depolama hesabı**, mevcut bir depolama hesabını seçin veya yeni bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2a76c-130">Under **Storage account**, select an existing storage account or create a new storage account.</span></span> <span data-ttu-id="2a76c-131">Bir depolama hesabı işlevi için dahili olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2a76c-131">A storage account is used internally for the function.</span></span>

    ![Yeni işlev uygulaması yapılandırma verilerini girin](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. <span data-ttu-id="2a76c-133">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2a76c-133">Click **Create**.</span></span>  
    <span data-ttu-id="2a76c-134">İşlev uygulaması oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2a76c-134">The function app is created.</span></span>

8. <span data-ttu-id="2a76c-135">Sol bölmede **daha fazla hizmet**, ve ardından aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="2a76c-135">In the left pane, click **More services**, and then do the following:</span></span>
    
    <span data-ttu-id="2a76c-136">a.</span><span class="sxs-lookup"><span data-stu-id="2a76c-136">a.</span></span> <span data-ttu-id="2a76c-137">İçinde **filtre** kutusuna **uygulama hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="2a76c-137">In the **Filter** box, type **App services**.</span></span>
    
    <span data-ttu-id="2a76c-138">b.</span><span class="sxs-lookup"><span data-stu-id="2a76c-138">b.</span></span> <span data-ttu-id="2a76c-139">Tıklatın **uygulama hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="2a76c-139">Click **App Services**.</span></span> 

    ![Sol bölmede "Daha fazla hizmet" bağlantısına](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. <span data-ttu-id="2a76c-141">Uygulama hizmetleri listesinde, işlev uygulaması adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2a76c-141">In the list of app services, click the name of the function app.</span></span>  
    <span data-ttu-id="2a76c-142">İşlev uygulama sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="2a76c-142">The function app page opens.</span></span>

10. <span data-ttu-id="2a76c-143">Sol bölmede **yeni işlev**, ve ardından aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="2a76c-143">In the left pane, click **New Function**, and then do the following:</span></span> 

    <span data-ttu-id="2a76c-144">a.</span><span class="sxs-lookup"><span data-stu-id="2a76c-144">a.</span></span> <span data-ttu-id="2a76c-145">İçinde **dil** listesinde **C#**.</span><span class="sxs-lookup"><span data-stu-id="2a76c-145">In the **Language** list, select **C#**.</span></span>
    
    <span data-ttu-id="2a76c-146">b.</span><span class="sxs-lookup"><span data-stu-id="2a76c-146">b.</span></span> <span data-ttu-id="2a76c-147">Şablon döşeme dizisinde seçin **QueueTrigger CSharp**.</span><span class="sxs-lookup"><span data-stu-id="2a76c-147">In the array of template tiles, select **QueueTrigger-CSharp**.</span></span>

    <span data-ttu-id="2a76c-148">c.</span><span class="sxs-lookup"><span data-stu-id="2a76c-148">c.</span></span> <span data-ttu-id="2a76c-149">İçinde **işlevinizi ad** işlevinizi için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="2a76c-149">In the **Name your function** box, type a name for your function.</span></span>

    <span data-ttu-id="2a76c-150">d.</span><span class="sxs-lookup"><span data-stu-id="2a76c-150">d.</span></span> <span data-ttu-id="2a76c-151">İçinde **sıra adı** veri dönüştürme işi tanımı adınızı yazın.</span><span class="sxs-lookup"><span data-stu-id="2a76c-151">In the **Queue name** box, type your data-transformation job definition name.</span></span>

    <span data-ttu-id="2a76c-152">e.</span><span class="sxs-lookup"><span data-stu-id="2a76c-152">e.</span></span> <span data-ttu-id="2a76c-153">Altında **depolama hesabı bağlantısı**, tıklatın **yeni**ve ardından veri dönüştürme işi karşılık gelen bir hesap seçin.</span><span class="sxs-lookup"><span data-stu-id="2a76c-153">Under **Storage account connection**, click **new**, and then select the account that corresponds to the data-transformation job.</span></span>  
        <span data-ttu-id="2a76c-154">Bağlantı adı not edin.</span><span class="sxs-lookup"><span data-stu-id="2a76c-154">Make a note of the connection name.</span></span> <span data-ttu-id="2a76c-155">Daha sonra Azure işlevinde adı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="2a76c-155">The name is required later in the Azure function.</span></span>

       ![Yeni bir C# işlevi oluşturma](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    <span data-ttu-id="2a76c-157">f.</span><span class="sxs-lookup"><span data-stu-id="2a76c-157">f.</span></span> <span data-ttu-id="2a76c-158">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2a76c-158">Click **Create**.</span></span>  
    <span data-ttu-id="2a76c-159">**İşlevi** penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="2a76c-159">The **Function** window opens.</span></span>

11. <span data-ttu-id="2a76c-160">İçinde **işlevi** penceresinde çalıştırın, _.csx_ dosyasını bulun ve ardından aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="2a76c-160">In the **Function** window, run _.csx_ file, and then do the following:</span></span>

    <span data-ttu-id="2a76c-161">a.</span><span class="sxs-lookup"><span data-stu-id="2a76c-161">a.</span></span> <span data-ttu-id="2a76c-162">Aşağıdaki kodu yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="2a76c-162">Paste the following code:</span></span>

    ```
    using System;
    using System.Configuration;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage.Queue;
    using Microsoft.WindowsAzure.Storage;
    using System.Collections.Generic;
    using System.Linq;

    public static void Run(QueueItem myQueueItem, TraceWriter log)
    {
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConfigurationManager.AppSettings["STORAGE_CONNECTIONNAME"]);

        string storageAccUriEndswith = "windows.net/";
        string uri = myQueueItem.TargetLocation.Replace("%20", " ");
        log.Info($"Blob Uri: {uri}");

        // Remove storage account uri string
        uri = uri.Substring(uri.IndexOf(storageAccUriEndswith) + storageAccUriEndswith.Length);

        string containerName = uri.Substring(0, uri.IndexOf("/")); 

        // Remove container name string
        uri = uri.Substring(containerName.Length + 1);

        // Current blob path
        string blobName = uri; 

        string volumeName = uri.Substring(containerName.Length + 1);
        volumeName = uri.Substring(0, uri.IndexOf("/"));

        // Remove volume name string
        uri = uri.Substring(volumeName.Length + 1);

        string newContainerName = uri.Substring(0, uri.IndexOf("/")).ToLower();
        string newBlobName = uri.Substring(newContainerName.Length + 1);

        log.Info($"Container name: {containerName}");
        log.Info($"Volume name: {volumeName}");
        log.Info($"New container name: {newContainerName}");

        log.Info($"Blob name: {blobName}");
        log.Info($"New blob name: {newBlobName}");

        // Create the blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Container reference
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlobContainer newContainer = blobClient.GetContainerReference(newContainerName);
        newContainer.CreateIfNotExists();

        if(!container.Exists())
        {
            log.Info($"Container - {containerName} not exists");
            return;
        }

        if(!newContainer.Exists())
        {
            log.Info($"Container - {newContainerName} not exists");
            return;
        }

        CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
        if (!blob.Exists())
        {
            // Skip to copy the blob to new container, if source blob doesn't exist
            log.Info($"The specified blob does not exist.");
            log.Info($"Blob Uri: {blob.Uri}");
            return;
        }

        CloudBlockBlob blobCopy = newContainer.GetBlockBlobReference(newBlobName);
        if (!blobCopy.Exists())
        {
            blobCopy.StartCopy(blob);
            // Delete old blob, after copy to new container
            blob.DeleteIfExists();
            log.Info($"Blob file path renamed completed successfully");
        }
        else
        {
            log.Info($"Blob file path renamed already done");
            // Delete old blob, if already exists.
            blob.DeleteIfExists();
        }
    }

    public class QueueItem
    {
        public string SourceLocation {get;set;}
        public long SizeInBytes {get;set;}
        public string Status {get;set;}
        public string JobID {get;set;}
        public string TargetLocation {get; set;}
    }

    ```

    <span data-ttu-id="2a76c-163">b.</span><span class="sxs-lookup"><span data-stu-id="2a76c-163">b.</span></span> <span data-ttu-id="2a76c-164">Değiştir **STORAGE_CONNECTIONNAME** üzerinde 11, depolama hesabı bağlantınızdaki satır (noktası 8 c bakın).</span><span class="sxs-lookup"><span data-stu-id="2a76c-164">Replace **STORAGE_CONNECTIONNAME** on line 11 with your storage account connection (refer point 8c).</span></span>

    <span data-ttu-id="2a76c-165">c.</span><span class="sxs-lookup"><span data-stu-id="2a76c-165">c.</span></span> <span data-ttu-id="2a76c-166">En üstünde sol tıklayın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="2a76c-166">At the top left, click **Save**.</span></span>

    ![İşlev Kaydet](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. <span data-ttu-id="2a76c-168">İşlev tamamlamak için aşağıdakileri yaparak bir daha fazla dosya ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2a76c-168">To complete the function, add one more file by doing the following:</span></span>

    <span data-ttu-id="2a76c-169">a.</span><span class="sxs-lookup"><span data-stu-id="2a76c-169">a.</span></span> <span data-ttu-id="2a76c-170">Tıklatın **dosyaları görüntüleyebilir**.</span><span class="sxs-lookup"><span data-stu-id="2a76c-170">Click **View files**.</span></span>

       !["Dosyaları Görüntüle" bağlantısını](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    <span data-ttu-id="2a76c-172">b.</span><span class="sxs-lookup"><span data-stu-id="2a76c-172">b.</span></span> <span data-ttu-id="2a76c-173">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2a76c-173">Click **Add**.</span></span>
    
    <span data-ttu-id="2a76c-174">c.</span><span class="sxs-lookup"><span data-stu-id="2a76c-174">c.</span></span> <span data-ttu-id="2a76c-175">Tür **project.json**, ve ardından Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="2a76c-175">Type **project.json**, and then press Enter.</span></span>
    
    <span data-ttu-id="2a76c-176">d.</span><span class="sxs-lookup"><span data-stu-id="2a76c-176">d.</span></span> <span data-ttu-id="2a76c-177">İçinde **project.json** dosya, aşağıdaki kodu yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="2a76c-177">In the **project.json** file, paste the following code:</span></span>

    ```
    {
    "frameworks": {
        "net46":{
        "dependencies": {
            "windowsazure.storage": "8.1.1"
        }
        }
    }
    }

    ```

    <span data-ttu-id="2a76c-178">e.</span><span class="sxs-lookup"><span data-stu-id="2a76c-178">e.</span></span> <span data-ttu-id="2a76c-179">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2a76c-179">Click **Save**.</span></span>

<span data-ttu-id="2a76c-180">Bir Azure işlevi oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="2a76c-180">You have created an Azure function.</span></span> <span data-ttu-id="2a76c-181">Bu işlev, yeni blob veri dönüştürme işlemi tarafından oluşturulan her zaman tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="2a76c-181">This function is triggered each time a new blob is generated by the data-transformation job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a76c-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2a76c-182">Next steps</span></span>

[<span data-ttu-id="2a76c-183">StorSimple veri Yöneticisi'ni kullanın, verilerinizi dönüştürmek için kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="2a76c-183">Use StorSimple Data Manager UI to transform your data</span></span>](storsimple-data-manager-ui.md)
