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
# <a name="change-a-blob-path-from-hello-default-path-private-preview"></a>Bir blob yolu hello varsayılan yolundan (özel olarak incelenmektedir) değiştirme

Bu makalede, nasıl Azure yukarı tooset işlev toorename varsayılan blob dosya yolu açıklanmaktadır. 

## <a name="prerequisites"></a>Ön koşullar

Bir kaynak grubu içinde karma veri kaynağındaki doğru şekilde yapılandırılmış bir iş tanımı olduğundan emin olun.

## <a name="create-an-azure-function"></a>Bir Azure işlevi oluşturma

bir Azure işlevi toocreate hello aşağıdaki:

1. Toohello Git [Azure portal](http://portal.azure.com/).

2. Merhaba sol bölmesinde Hello üstünde tıklatın **yeni**. 

3. Merhaba, **arama** kutusuna **işlev uygulaması**, ve ardından Enter tuşuna basın.

    !["İşlev uygulaması" Merhaba arama kutusuna yazın](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. Merhaba, **sonuçları** tıklatın **işlev uygulaması**.

    ![Merhaba sonuçlar listesinde Hello işlevi Uygulama kaynağı seçin](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    Merhaba **işlev uygulaması** penceresi açılır.

5. **Oluştur**'a tıklayın.

    ![Merhaba işlev uygulaması penceresini "Oluştur" düğmesine](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. Merhaba üzerinde **işlev uygulaması** yapılandırma dikey penceresinde, aşağıdaki hello:

    a. Merhaba, **uygulama adı** kutusu, tür hello uygulama adı.
    
    b. Merhaba, **abonelik** kutusu, hello abonelik türü hello adı.

    c. Altında **kaynak grubu**, tıklatın **Yeni Oluştur**ve ardından türü hello hello kaynak grubunun adı.

    d. Merhaba, **barındırma planına** kutusuna **tüketim planlama**.

    e. Merhaba, **konumu** kutusunda türü başlangıç konumu.

    f. Altında **depolama hesabı**, mevcut bir depolama hesabını seçin veya yeni bir depolama hesabı oluşturun. Bir depolama hesabı hello işlevi için dahili olarak kullanılır.

    ![Yeni işlev uygulaması yapılandırma verilerini girin](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. **Oluştur**'a tıklayın.  
    Merhaba işlev uygulaması oluşturulur.

8. Merhaba sol bölmede **daha fazla hizmet**ve ardından aşağıdaki hello:
    
    a. Merhaba, **filtre** kutusuna **uygulama hizmetleri**.
    
    b. Tıklatın **uygulama hizmetleri**. 

    !["Daha fazla hizmet" bağlantısına hello sol bölmede](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. Uygulama Hizmetleri Hello listesinde hello işlev uygulaması hello adına tıklayın.  
    Merhaba işlevi uygulama sayfası açılır.

10. Merhaba sol bölmede **yeni işlev**ve ardından aşağıdaki hello: 

    a. Merhaba, **dil** listesinde **C#**.
    
    b. Şablon döşeme Hello dizisinde seçin **QueueTrigger CSharp**.

    c. Merhaba, **işlevinizi ad** işlevinizi için bir ad yazın.

    d. Merhaba, **sıra adı** veri dönüştürme işi tanımı adınızı yazın.

    e. Altında **depolama hesabı bağlantısı**, tıklatın **yeni**ve ardından toohello veri dönüştürme işi karşılık gelen hello hesabını seçin.  
        Merhaba bağlantı adını not edin. Daha sonra hello Azure işlevi Hello adı gerekiyor.

       ![Yeni bir C# işlevi oluşturma](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    f. **Oluştur**'a tıklayın.  
    Merhaba **işlevi** penceresi açılır.

11. Merhaba, **işlevi** penceresinde çalıştırın, _.csx_ dosyasını bulun ve ardından aşağıdaki hello:

    a. Hello aşağıdaki kodu yapıştırın:

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

    b. Değiştir **STORAGE_CONNECTIONNAME** üzerinde 11, depolama hesabı bağlantınızdaki satır (noktası 8 c bakın).

    c. Sol Hello üstünde tıklatın **kaydetmek**.

    ![İşlev Kaydet](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. toocomplete Merhaba işlevi, hello aşağıdakileri yaparak bir daha fazla dosya Ekle:

    a. Tıklatın **dosyaları görüntüleyebilir**.

       ![Merhaba "Dosyaları Görüntüle" bağlantısını](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    b. **Ekle**'ye tıklayın.
    
    c. Tür **project.json**, ve ardından Enter tuşuna basın.
    
    d. Merhaba, **project.json** dosya, hello aşağıdaki kodu yapıştırın:

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

    e. **Kaydet** düğmesine tıklayın.

Bir Azure işlevi oluşturdunuz. Bu işlev, yeni blob hello veri dönüştürme işlemi tarafından oluşturulan her zaman tetiklenir.

## <a name="next-steps"></a>Sonraki adımlar

[StorSimple veri Yöneticisi kullanıcı Arabirimi tootransform verilerinizi kullanma](storsimple-data-manager-ui.md)
