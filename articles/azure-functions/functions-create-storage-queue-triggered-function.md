---
title: "Azure kuyruk iletileri tarafından tetiklenen bir işlev aaaCreate | Microsoft Docs"
description: "Kullanım Azure işlevleri toocreate iletileri tarafından çağrılan sunucusuz bir işlev tooan Azure depolama kuyruğu gönderildi."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361da2a4-15d1-4903-bdc4-cc4b27fc3ff4
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e9501ed336b502eaeee3fa62ec4ae085c76de0ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-queue-storage"></a>Azure Kuyruk Depolama tarafından tetiklenen bir işlev oluşturma

Nasıl toocreate iletileri olduğunda tetiklenen bir işlev tooan Azure Storage kuyruğuna gönderilen bilgi edinin.

![Merhaba günlüklerine iletiyi görüntüle.](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Ön koşullar

- Merhaba yükleyip [Microsoft Azure Storage Gezgini](http://storageexplorer.com/).

- Azure aboneliği. Aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Azure İşlev uygulaması oluşturma

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![İşlev uygulaması başarıyla oluşturuldu.](./media/functions-create-first-azure-function/function-app-create-success.png)

Ardından, hello yeni işlev uygulamada bir işlev oluşturun.

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a>Kuyruk ile tetiklenen bir işlev oluşturma

1. Merhaba, işlev uygulaması'nı genişletin ve  **+**  sonraki çok düğmesini**işlevler**. Bu işlev uygulamanızda hello ilk işlevi ise seçin **özel işlevi**. Merhaba eksiksiz işlev şablonları görüntüler.

    ![Hello Azure portalı hızlı başlangıç sayfasında işlevleri](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. Select hello **QueueTrigger** şablonu istediğiniz dili ve hello tabloda belirtildiği gibi hello ayarları kullanın.

    ![Merhaba depolama kuyruğu tetiklenen bir işlev oluşturun.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | Ayar | Önerilen değer | Açıklama |
    |---|---|---|
    | **Kuyruk adı**   | myqueue-items    | Merhaba adını, depolama hesabınız tooconnect tooin sırası. |
    | **Depolama hesabı bağlantısı** | AzureWebJobStorage | Merhaba depolama hesabı bağlantısı işlevi uygulamanız tarafından zaten kullanılmakta kullanın veya yeni bir tane oluşturun.  |
    | **İşlevinizi adlandırın** | İşlev uygulamanızda benzersiz olmalıdır | Kuyruk tarafından tetiklenen bu işlevin adı. |

3. Tıklatın **oluşturma** toocreate işlevinizi.

Ardından, tooyour Azure depolama hesabı bağlanmak ve hello oluşturmak **Sıram öğeleri** depolama kuyruğu.

## <a name="create-hello-queue"></a>Merhaba kuyruk oluşturma

1. İşlevinizde **Tümleştir**'e tıklayın, **Belgeler**'i genişletin ve hem **Hesap adı** hem de **Hesap anahtarı** değerlerini kopyalayın. Bu kimlik bilgileri tooconnect toohello depolama hesabı kullanın. Depolama hesabınız zaten bağlanmış olduğunuz toostep 4 atlayın.

    ![Merhaba depolama hesabı bağlantısı kimlik bilgilerini edinin.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)v

1. Merhaba çalıştırmak [Microsoft Azure Storage Gezgini](http://storageexplorer.com/) aracı, hello tıklatın Bağlan simgesi hello sol tarafta, seçin **bir depolama hesabı adı ve anahtar kullanmak**, tıklatıp **sonraki**.

    ![Merhaba depolama hesabı Gezgini aracını çalıştırın.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. Merhaba girin **hesap adı** ve **hesap anahtarı** 1. adımdaki tıklatın **sonraki** ve ardından **Bağlan**.

    ![Merhaba depolama kimlik bilgilerini girin ve bağlanın.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. Merhaba bağlı depolama hesabı'nı genişletin, sağ tıklatın **sıraları**, tıklatın **Oluşturma sırası**, türü `myqueue-items`, ve ENTER tuşuna basın.

    ![Depolama kuyruğu oluşturun.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

Bir depolama kuyruğu sahip olduğunuza göre bir ileti toohello sırası ekleyerek hello işlevi test edebilirsiniz.

## <a name="test-hello-function"></a>Test hello işlevi

1. Geri Azure portal hello, Gözat tooyour işlevi genişletin hello **günlükleri** hello sonunda hello sayfası ve emin olun, bu günlük akış duraklatıldı değil.

1. Depolama Gezgini'nde depolama hesabınızı genişletin, **Kuyruklar**'ı ve **myqueue-items** öğesini seçip **İleti ekle**'ye tıklayın.

    ![Bir ileti toohello sırası ekleyin.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. "Hello World!" iletinizi **İleti metni** alanına yazın ve **Tamam**'a tıklayın.

1. Birkaç saniye bekleyin, sonra tooyour işlev günlükleri geri dönün ve hello yeni ileti hello sırasından okuma doğrulayın.

    ![Merhaba günlüklerine iletiyi görüntüle.](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. Depolama Gezgini içinde geri tıklayın **yenileme** ve hello ileti işlendikten ve artık hello sırada olduğunu doğrulayın.

## <a name="clean-up-resources"></a>Kaynakları temizleme

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Sonraki adımlar

Bir ileti tooa depolama kuyruğu eklendiğinde çalıştırılan bir işlev oluşturdunuz.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Kuyruk depolama tetikleyicileri hakkında daha fazla bilgi için bkz. [Azure İşlevleri Kuyruk depolama bağlamaları](functions-bindings-storage-queue.md).