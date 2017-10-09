---
title: "Merhaba varsayılan aaaChange blob yolundan | Microsoft Docs"
description: "Nasıl bir Azure yukarı tooset işlev toorename bir blob dosya yolu (özel olarak incelenmektedir) öğrenin"
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
ms.openlocfilehash: 2c414603514223c701ab1a3bd0b81ee18f1af666
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="change-a-blob-path-from-hello-default-path-private-preview"></a><span data-ttu-id="aa473-103">Bir blob yolu hello varsayılan yolundan (özel olarak incelenmektedir) değiştirme</span><span class="sxs-lookup"><span data-stu-id="aa473-103">Change a blob path from hello default path (private preview)</span></span>

<span data-ttu-id="aa473-104">Bu makalede, nasıl Azure yukarı tooset işlev toorename varsayılan blob dosya yolu açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="aa473-104">This article describes how tooset up an Azure function toorename a default blob file path.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="aa473-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="aa473-105">Prerequisites</span></span>

<span data-ttu-id="aa473-106">Bir kaynak grubu içinde karma veri kaynağındaki doğru şekilde yapılandırılmış bir iş tanımı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="aa473-106">Ensure that you have a job definition that has been correctly configured in a hybrid data resource within a resource group.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="aa473-107">Bir Azure işlevi oluşturma</span><span class="sxs-lookup"><span data-stu-id="aa473-107">Create an Azure function</span></span>

<span data-ttu-id="aa473-108">bir Azure işlevi toocreate hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="aa473-108">toocreate an Azure function, do hello following:</span></span>

1. <span data-ttu-id="aa473-109">Toohello Git [Azure portal](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="aa473-109">Go toohello [Azure portal](http://portal.azure.com/).</span></span>

2. <span data-ttu-id="aa473-110">Merhaba sol bölmesinde Hello üstünde tıklatın **yeni**.</span><span class="sxs-lookup"><span data-stu-id="aa473-110">At hello top of hello left pane, click **New**.</span></span> 

3. <span data-ttu-id="aa473-111">Merhaba, **arama** kutusuna **işlev uygulaması**, ve ardından Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="aa473-111">In hello **Search** box, type **Function App**, and then press Enter.</span></span>

    !["İşlev uygulaması" Merhaba arama kutusuna yazın](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. <span data-ttu-id="aa473-113">Merhaba, **sonuçları** tıklatın **işlev uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="aa473-113">In hello **Results** list, click **Function App**.</span></span>

    ![Merhaba sonuçlar listesinde Hello işlevi Uygulama kaynağı seçin](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    <span data-ttu-id="aa473-115">Merhaba **işlev uygulaması** penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="aa473-115">hello **Function App** window opens.</span></span>

5. <span data-ttu-id="aa473-116">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="aa473-116">Click **Create**.</span></span>

    ![Merhaba işlev uygulaması penceresini "Oluştur" düğmesine](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. <span data-ttu-id="aa473-118">Merhaba üzerinde **işlev uygulaması** yapılandırma dikey penceresinde, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="aa473-118">On hello **Function App** configuration blade, do hello following:</span></span>

    <span data-ttu-id="aa473-119">a.</span><span class="sxs-lookup"><span data-stu-id="aa473-119">a.</span></span> <span data-ttu-id="aa473-120">Merhaba, **uygulama adı** kutusu, tür hello uygulama adı.</span><span class="sxs-lookup"><span data-stu-id="aa473-120">In hello **App name** box, type hello app name.</span></span>
    
    <span data-ttu-id="aa473-121">b.</span><span class="sxs-lookup"><span data-stu-id="aa473-121">b.</span></span> <span data-ttu-id="aa473-122">Merhaba, **abonelik** kutusu, hello abonelik türü hello adı.</span><span class="sxs-lookup"><span data-stu-id="aa473-122">In hello **Subscription** box, type hello name of hello subscription.</span></span>

    <span data-ttu-id="aa473-123">c.</span><span class="sxs-lookup"><span data-stu-id="aa473-123">c.</span></span> <span data-ttu-id="aa473-124">Altında **kaynak grubu**, tıklatın **Yeni Oluştur**ve ardından türü hello hello kaynak grubunun adı.</span><span class="sxs-lookup"><span data-stu-id="aa473-124">Under **Resource Group**, click **Create new**, and then type hello name of hello resource group.</span></span>

    <span data-ttu-id="aa473-125">d.</span><span class="sxs-lookup"><span data-stu-id="aa473-125">d.</span></span> <span data-ttu-id="aa473-126">Merhaba, **barındırma planına** kutusuna **tüketim planlama**.</span><span class="sxs-lookup"><span data-stu-id="aa473-126">In hello **Hosting Plan** box, type **Consumption Plan**.</span></span>

    <span data-ttu-id="aa473-127">e.</span><span class="sxs-lookup"><span data-stu-id="aa473-127">e.</span></span> <span data-ttu-id="aa473-128">Merhaba, **konumu** kutusunda türü başlangıç konumu.</span><span class="sxs-lookup"><span data-stu-id="aa473-128">In hello **Location** box, type hello location.</span></span>

    <span data-ttu-id="aa473-129">f.</span><span class="sxs-lookup"><span data-stu-id="aa473-129">f.</span></span> <span data-ttu-id="aa473-130">Altında **depolama hesabı**, mevcut bir depolama hesabını seçin veya yeni bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="aa473-130">Under **Storage account**, select an existing storage account or create a new storage account.</span></span> <span data-ttu-id="aa473-131">Bir depolama hesabı hello işlevi için dahili olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="aa473-131">A storage account is used internally for hello function.</span></span>

    ![Yeni işlev uygulaması yapılandırma verilerini girin](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. <span data-ttu-id="aa473-133">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="aa473-133">Click **Create**.</span></span>  
    <span data-ttu-id="aa473-134">Merhaba işlev uygulaması oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="aa473-134">hello function app is created.</span></span>

8. <span data-ttu-id="aa473-135">Merhaba sol bölmede **daha fazla hizmet**ve ardından aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="aa473-135">In hello left pane, click **More services**, and then do hello following:</span></span>
    
    <span data-ttu-id="aa473-136">a.</span><span class="sxs-lookup"><span data-stu-id="aa473-136">a.</span></span> <span data-ttu-id="aa473-137">Merhaba, **filtre** kutusuna **uygulama hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="aa473-137">In hello **Filter** box, type **App services**.</span></span>
    
    <span data-ttu-id="aa473-138">b.</span><span class="sxs-lookup"><span data-stu-id="aa473-138">b.</span></span> <span data-ttu-id="aa473-139">Tıklatın **uygulama hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="aa473-139">Click **App Services**.</span></span> 

    !["Daha fazla hizmet" bağlantısına hello sol bölmede](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. <span data-ttu-id="aa473-141">Uygulama Hizmetleri Hello listesinde hello işlev uygulaması hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="aa473-141">In hello list of app services, click hello name of hello function app.</span></span>  
    <span data-ttu-id="aa473-142">Merhaba işlevi uygulama sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="aa473-142">hello function app page opens.</span></span>

10. <span data-ttu-id="aa473-143">Merhaba sol bölmede **yeni işlev**ve ardından aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="aa473-143">In hello left pane, click **New Function**, and then do hello following:</span></span> 

    <span data-ttu-id="aa473-144">a.</span><span class="sxs-lookup"><span data-stu-id="aa473-144">a.</span></span> <span data-ttu-id="aa473-145">Merhaba, **dil** listesinde **C#**.</span><span class="sxs-lookup"><span data-stu-id="aa473-145">In hello **Language** list, select **C#**.</span></span>
    
    <span data-ttu-id="aa473-146">b.</span><span class="sxs-lookup"><span data-stu-id="aa473-146">b.</span></span> <span data-ttu-id="aa473-147">Şablon döşeme Hello dizisinde seçin **QueueTrigger CSharp**.</span><span class="sxs-lookup"><span data-stu-id="aa473-147">In hello array of template tiles, select **QueueTrigger-CSharp**.</span></span>

    <span data-ttu-id="aa473-148">c.</span><span class="sxs-lookup"><span data-stu-id="aa473-148">c.</span></span> <span data-ttu-id="aa473-149">Merhaba, **işlevinizi ad** işlevinizi için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="aa473-149">In hello **Name your function** box, type a name for your function.</span></span>

    <span data-ttu-id="aa473-150">d.</span><span class="sxs-lookup"><span data-stu-id="aa473-150">d.</span></span> <span data-ttu-id="aa473-151">Merhaba, **sıra adı** veri dönüştürme işi tanımı adınızı yazın.</span><span class="sxs-lookup"><span data-stu-id="aa473-151">In hello **Queue name** box, type your data-transformation job definition name.</span></span>

    <span data-ttu-id="aa473-152">e.</span><span class="sxs-lookup"><span data-stu-id="aa473-152">e.</span></span> <span data-ttu-id="aa473-153">Altında **depolama hesabı bağlantısı**, tıklatın **yeni**ve ardından toohello veri dönüştürme işi karşılık gelen hello hesabını seçin.</span><span class="sxs-lookup"><span data-stu-id="aa473-153">Under **Storage account connection**, click **new**, and then select hello account that corresponds toohello data-transformation job.</span></span>  
        <span data-ttu-id="aa473-154">Merhaba bağlantı adını not edin.</span><span class="sxs-lookup"><span data-stu-id="aa473-154">Make a note of hello connection name.</span></span> <span data-ttu-id="aa473-155">Daha sonra hello Azure işlevi Hello adı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="aa473-155">hello name is required later in hello Azure function.</span></span>

       ![Yeni bir C# işlevi oluşturma](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    <span data-ttu-id="aa473-157">f.</span><span class="sxs-lookup"><span data-stu-id="aa473-157">f.</span></span> <span data-ttu-id="aa473-158">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="aa473-158">Click **Create**.</span></span>  
    <span data-ttu-id="aa473-159">Merhaba **işlevi** penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="aa473-159">hello **Function** window opens.</span></span>

11. <span data-ttu-id="aa473-160">Merhaba, **işlevi** penceresinde çalıştırın, _.csx_ dosyasını bulun ve ardından aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="aa473-160">In hello **Function** window, run _.csx_ file, and then do hello following:</span></span>

    <span data-ttu-id="aa473-161">a.</span><span class="sxs-lookup"><span data-stu-id="aa473-161">a.</span></span> <span data-ttu-id="aa473-162">Hello aşağıdaki kodu yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="aa473-162">Paste hello following code:</span></span>

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

        // Create hello blob client.
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
            // Skip toocopy hello blob toonew container, if source blob doesn't exist
            log.Info($"hello specified blob does not exist.");
            log.Info($"Blob Uri: {blob.Uri}");
            return;
        }

        CloudBlockBlob blobCopy = newContainer.GetBlockBlobReference(newBlobName);
        if (!blobCopy.Exists())
        {
            blobCopy.StartCopy(blob);
            // Delete old blob, after copy toonew container
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

    <span data-ttu-id="aa473-163">b.</span><span class="sxs-lookup"><span data-stu-id="aa473-163">b.</span></span> <span data-ttu-id="aa473-164">Değiştir **STORAGE_CONNECTIONNAME** üzerinde 11, depolama hesabı bağlantınızdaki satır (noktası 8 c bakın).</span><span class="sxs-lookup"><span data-stu-id="aa473-164">Replace **STORAGE_CONNECTIONNAME** on line 11 with your storage account connection (refer point 8c).</span></span>

    <span data-ttu-id="aa473-165">c.</span><span class="sxs-lookup"><span data-stu-id="aa473-165">c.</span></span> <span data-ttu-id="aa473-166">Sol Hello üstünde tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="aa473-166">At hello top left, click **Save**.</span></span>

    ![İşlev Kaydet](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. <span data-ttu-id="aa473-168">toocomplete Merhaba işlevi, hello aşağıdakileri yaparak bir daha fazla dosya Ekle:</span><span class="sxs-lookup"><span data-stu-id="aa473-168">toocomplete hello function, add one more file by doing hello following:</span></span>

    <span data-ttu-id="aa473-169">a.</span><span class="sxs-lookup"><span data-stu-id="aa473-169">a.</span></span> <span data-ttu-id="aa473-170">Tıklatın **dosyaları görüntüleyebilir**.</span><span class="sxs-lookup"><span data-stu-id="aa473-170">Click **View files**.</span></span>

       ![Merhaba "Dosyaları Görüntüle" bağlantısını](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    <span data-ttu-id="aa473-172">b.</span><span class="sxs-lookup"><span data-stu-id="aa473-172">b.</span></span> <span data-ttu-id="aa473-173">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="aa473-173">Click **Add**.</span></span>
    
    <span data-ttu-id="aa473-174">c.</span><span class="sxs-lookup"><span data-stu-id="aa473-174">c.</span></span> <span data-ttu-id="aa473-175">Tür **project.json**, ve ardından Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="aa473-175">Type **project.json**, and then press Enter.</span></span>
    
    <span data-ttu-id="aa473-176">d.</span><span class="sxs-lookup"><span data-stu-id="aa473-176">d.</span></span> <span data-ttu-id="aa473-177">Merhaba, **project.json** dosya, hello aşağıdaki kodu yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="aa473-177">In hello **project.json** file, paste hello following code:</span></span>

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

    <span data-ttu-id="aa473-178">e.</span><span class="sxs-lookup"><span data-stu-id="aa473-178">e.</span></span> <span data-ttu-id="aa473-179">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="aa473-179">Click **Save**.</span></span>

<span data-ttu-id="aa473-180">Bir Azure işlevi oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="aa473-180">You have created an Azure function.</span></span> <span data-ttu-id="aa473-181">Bu işlev, yeni blob hello veri dönüştürme işlemi tarafından oluşturulan her zaman tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="aa473-181">This function is triggered each time a new blob is generated by hello data-transformation job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa473-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aa473-182">Next steps</span></span>

[<span data-ttu-id="aa473-183">StorSimple veri Yöneticisi kullanıcı Arabirimi tootransform verilerinizi kullanma</span><span class="sxs-lookup"><span data-stu-id="aa473-183">Use StorSimple Data Manager UI tootransform your data</span></span>](storsimple-data-manager-ui.md)
