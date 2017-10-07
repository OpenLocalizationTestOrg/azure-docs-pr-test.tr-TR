---
title: "Azure Blob Depolama Birimi tarafından tetiklenen bir işlev aaaCreate | Microsoft Docs"
description: "Kullanım Azure işlevleri toocreate öğeleri tarafından çağrılan sunucusuz bir işlev tooAzure Blob Depolama eklendi."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: d6bff41c-a624-40c1-bbc7-80590df29ded
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: acb7d29abb07a22da11d0e65d2ed54591f8e3f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-blob-storage"></a>Azure Blob depolama ile tetiklenen bir işlev oluşturma

Toocreate dosyaları olduğunda tetiklenen bir işlev Azure Blob depolama alanına güncelleştirilmiş tooor nasıl karşıya öğrenin.

![Merhaba günlüklerine iletiyi görüntüle.](./media/functions-create-storage-blob-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Ön koşullar

+ Merhaba yükleyip [Microsoft Azure Storage Gezgini](http://storageexplorer.com/).
+ Azure aboneliği. Aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Azure İşlev uygulaması oluşturma

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![İşlev uygulaması başarıyla oluşturuldu.](./media/functions-create-first-azure-function/function-app-create-success.png)

Ardından, hello yeni işlev uygulamada bir işlev oluşturun.

<a name="create-function"></a>

## <a name="create-a-blob-storage-triggered-function"></a>Blob depolama ile tetiklenen bir işlev oluşturma

1. Merhaba, işlev uygulaması'nı genişletin ve  **+**  sonraki çok düğmesini**işlevler**. Bu işlev uygulamanızda hello ilk işlevi ise seçin **özel işlevi**. Merhaba eksiksiz işlev şablonları görüntüler.

    ![Hello Azure portalı hızlı başlangıç sayfasında işlevleri](./media/functions-create-storage-blob-triggered-function/add-first-function.png)

2. Select hello **BlobTrigger** şablonu istediğiniz dili ve hello tabloda belirtildiği gibi hello ayarları kullanın.

    ![Merhaba Blob Depolama tetiklenen bir işlev oluşturun.](./media/functions-create-storage-blob-triggered-function/functions-create-blob-storage-trigger-portal.png)

    | Ayar | Önerilen değer | Açıklama |
    |---|---|---|
    | **Path**   | mycontainer/{name}    | İzlenmekte olan Blob depolamanın konumu. Merhaba dosya adı hello BLOB hello bağlama hello olarak geçirilir _adı_ parametresi.  |
    | **Depolama hesabı bağlantısı** | AzureWebJobStorage | Merhaba depolama hesabı bağlantısı işlevi uygulamanız tarafından zaten kullanılmakta kullanın veya yeni bir tane oluşturun.  |
    | **İşlevinizi adlandırın** | İşlev uygulamanızda benzersiz olmalıdır | Blob ile tetiklenen bu işlevin adı. |

3. Tıklatın **oluşturma** toocreate işlevinizi.

Ardından, tooyour Azure depolama hesabı bağlanmak ve hello oluşturmak **mycontainer** kapsayıcı.

## <a name="create-hello-container"></a>Merhaba kapsayıcı oluşturma

1. İşlevinizde **Tümleştir**'e tıklayın, **Belgeler**'i genişletin ve hem **Hesap adı** hem de **Hesap anahtarı** değerlerini kopyalayın. Bu kimlik bilgileri tooconnect toohello depolama hesabı kullanın. Depolama hesabınız zaten bağlanmış olduğunuz toostep 4 atlayın.

    ![Merhaba depolama hesabı bağlantısı kimlik bilgilerini edinin.](./media/functions-create-storage-blob-triggered-function/functions-storage-account-connection.png)

1. Merhaba çalıştırmak [Microsoft Azure Storage Gezgini](http://storageexplorer.com/) aracı, hello tıklatın Bağlan simgesi hello sol tarafta, seçin **bir depolama hesabı adı ve anahtar kullanmak**, tıklatıp **sonraki**.

    ![Merhaba depolama hesabı Gezgini aracını çalıştırın.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-1.png)

1. Merhaba girin **hesap adı** ve **hesap anahtarı** 1. adımdaki tıklatın **sonraki** ve ardından **Bağlan**. 

    ![Merhaba depolama kimlik bilgilerini girin ve bağlanın.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-2.png)

1. Merhaba bağlı depolama hesabı'nı genişletin, sağ tıklatın **Blob kapsayıcıları**, tıklatın **oluşturma blob kapsayıcısı**, türü `mycontainer`, ve ENTER tuşuna basın.

    ![Depolama kuyruğu oluşturun.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-create-blob-container.png)

Bir blob kapsayıcısını sahip olduğunuza göre bir dosya toohello kapsayıcısı yükleyerek hello işlevi test edebilirsiniz.

## <a name="test-hello-function"></a>Test hello işlevi

1. Geri Azure portal hello, Gözat tooyour işlevi genişletin hello **günlükleri** hello sonunda hello sayfası ve emin olun, bu günlük akış duraklatıldı değil.

1. Depolama Gezgini’nde depolama hesabınızı genişletin, **Blob kapsayıcıları** ve **mycontainer** öğesine tıklayın. **Karşıya Yükle**’ye ve ardından **Dosyaları yükle...** seçeneğine tıklayın.

    ![Bir dosya toohello blob kapsayıcısı karşıya yükleyin.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-upload-file-blob.png)

1. Merhaba, **dosyaları karşıya yükleme** iletişim kutusunda, hello **dosyaları** alan. Bir görüntü dosyası gibi yerel bilgisayarınızda tooa dosyasını bulun, seçin ve **açık** ve ardından **karşıya**.

1. Tooyour işlev günlükleri gidip bu hello blobu okuma emin olun.

   ![Merhaba günlüklerine iletiyi görüntüle.](./media/functions-create-storage-blob-triggered-function/functions-blob-storage-trigger-view-logs.png)

    >[!NOTE]
    > İşlevi uygulamanızı hello varsayılan tüketim planında çalıştığında, olabilir bir gecikme dakika arasında hello eklenen veya güncelleştirilen blob ile Merhaba tooseveral yukarı işlev tetiklenen. Blob ile tetiklenen işlevlerde düşük gecikme süresi gerekiyorsa, işlev uygulamanızı bir App Service planında çalıştırmayı düşünün.

## <a name="clean-up-resources"></a>Kaynakları temizleme

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Sonraki adımlar

Güncelleştirilmiş tooor Blob storage'da bir blob eklendiğinde çalıştırılan bir işlev oluşturdunuz. 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Blob depolama tetikleyicileri hakkında daha fazla bilgi için bkz. [Azure İşlevleri Blob depolama bağlamaları](functions-bindings-storage-blob.md).
