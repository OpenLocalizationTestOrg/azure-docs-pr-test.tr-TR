---
title: "ilk işlev hello Azure Portalı ' aaaCreate | Microsoft Docs"
description: "Bilgi nasıl ilk Azure işlev kullanılarak sunucusuz yürütme için toocreate hello Azure portalı."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 96cf87b9-8db6-41a8-863a-abb828e3d06d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/07/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 84283d7d4bc6015061946af4589f9a70ae61f36b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-in-hello-azure-portal"></a>Hello Azure portalını ilk işlevinizi oluşturma

Azure işlevleri sağlayan bir VM oluşturun veya bir web uygulaması yayımlama toofirst gerek kalmadan sunucusuz bir ortamda kodunuzu yürütün. Bu konuda, toouse toocreate hello Azure portalı "hello world" işlevinde nasıl çalıştığını öğrenin.

![Hello Azure portal işlev uygulaması oluşturma](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-tooazure"></a>İçinde tooAzure oturum

İçinde toohello oturum [Azure portal](https://portal.azure.com/).

## <a name="create-a-function-app"></a>İşlev uygulaması oluşturma

Bir işlev uygulaması toohost hello işlevlerinizin yürütülmesini olması gerekir. İşlev uygulaması, kaynakların daha kolay yönetilmesi, dağıtılması ve paylaşılması için işlevleri bir mantıksal birim olarak gruplandırmanıza olanak tanır. 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

Ardından, hello yeni işlev uygulamada bir işlev oluşturun.

## <a name="create-function"></a>HTTP ile tetiklenen bir işlev oluşturma

1. Yeni işlev uygulamanız genişletin ve ardından hello  **+**  sonraki çok düğmesini**işlevler**.

2.  Merhaba, **hızlı şekilde kullanmaya** sayfasında, **Web kancası + API**, **bir dil seçin** işlevi ve tıklatın **bu işlev oluşturma** . 
   
    ![Hello Azure portal işlevleri hızlı başlangıcı.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

Bir işlev hello şablonu için bir HTTP tetiklenen işlevi kullanarak seçmiş olduğunuz dili oluşturulur. Bir HTTP isteği göndererek hello yeni işlev çalıştırabilirsiniz.

## <a name="test-hello-function"></a>Test hello işlevi

1. Yeni işlevinizde **</> İşlev URL'sini al**'a tıklayın, **varsayılan (İşlev anahtarı)** seçeneğini belirleyin ve ardından **Kopyala**'ya tıklayın. 

    ![Azure portal hello Hello işlevi URL'sini Kopyala](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. Merhaba işlevi URL'sini tarayıcınızın adres çubuğuna yapıştırın. Merhaba sorgu dizesi eklemek `&name=<yourname>` toothis URL ve tuşuna hello `Enter` klavye tooexecute hello isteğiniz üzerinde anahtar. Merhaba, hello Edge tarayıcısında hello işlevi tarafından döndürülen hello yanıt örneği aşağıdadır:

    ![Merhaba tarayıcıda işlev yanıtı.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    Merhaba istek URL'sini içerir, varsayılan olarak, tooaccess gerekli bir anahtarı işlevinizi HTTP üzerinden.   

3. İşlevinizi çalıştığında, izleme bilgilerini toohello günlüklerine yazılır. Merhaba önceki yürütme toosee hello izleme çıktısını hello Portalı'nda tooyour işlevi dönün ve yukarı ok Merhaba ekranında tooexpand hello sonundaki hello **günlükleri**. 

   ![İşlevler Görüntüleyicisi hello Azure portalında oturum açın.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a>Kaynakları temizleme

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Sonraki adımlar

HTTP ile tetiklenen basit bir işlevi kullanarak işlev uygulaması oluşturdunuz.  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Daha fazla bilgi için bkz. [Azure İşlevleri HTTP ve web kancası bağlamaları](functions-bindings-http-webhook.md).



