---
title: "Azure portalında ilk işlevinizi oluşturma | Microsoft Docs"
description: "Azure portalını kullanarak sunucusuz yürütme için ilk Azure İşlevinizi oluşturma hakkında bilgi edinin."
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
editor: 
tags: 
ms.assetid: 96cf87b9-8db6-41a8-863a-abb828e3d06d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/17/2017
ms.author: glenga
ms.custom: mvc, devcenter
ms.openlocfilehash: 754ca6e5297c3be9166efa7a40a5ba3714911c99
ms.sourcegitcommit: 48fce90a4ec357d2fb89183141610789003993d2
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/12/2018
---
# <a name="create-your-first-function-in-the-azure-portal"></a>Azure portalında ilk işlevinizi oluşturma

Azure İşlevleri, öncelikle bir VM oluşturmak veya bir web uygulaması yayımlamak zorunda kalmadan kodunuzu [sunucusuz](https://azure.microsoft.com/overview/serverless-computing/) bir ortamda yürütmenize olanak tanır. Bu konu başlığında, Azure portalında İşlevler’i kullanarak bir "hello world" işlevi oluşturmayı öğrenebilirsiniz.

![Azure portalında işlev uygulaması oluşturma](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="sign-in-to-azure"></a>Azure'da oturum açma

Azure portalı açın. Bunu yapmak için, Azure hesabınızla [Azure portalında](https://portal.azure.com/) oturum açın.

## <a name="create-a-function-app"></a>İşlev uygulaması oluşturma

İşlevlerinizin yürütülmesini barındıran bir işlev uygulamasına sahip olmanız gerekir. İşlev uygulaması, kaynakların daha kolay yönetilmesi, dağıtılması ve paylaşılması için işlevleri bir mantıksal birim olarak gruplandırmanıza olanak tanır. 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

Ardından, yeni işlev uygulamasında bir işlev oluşturun.

## <a name="create-function"></a>HTTP ile tetiklenen bir işlev oluşturma

1. Yeni işlev uygulamanızı genişletin, ardından **İşlevler**’in yanındaki **+** düğmesine tıklayın.

2.  **Hemen kullanmaya başlayın** sayfasında **Web Kancası + API**'ye tıklayın, **işleviniz için bir dil seçin** ve **Bu işlevi oluştur**'a tıklayın. 
   
    ![Azure portalındaki İşlevler hızlı başlangıcı.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

HTTP ile tetiklenen işlevin şablonu kullanılarak, seçtiğiniz dilde bir işlev oluşturulur. Bu konu, portaldaki bir C# betik işlevini gösterir, ancak herhangi bir [desteklenen dilde](supported-languages.md) işlev oluşturabilirsiniz. 

Artık bir HTTP isteği göndererek yeni işlevi çalıştırabilirsiniz.

## <a name="test-the-function"></a>İşlevi test etme

1. Yeni işlevinizde sağ üst kısımdaki **</> İşlev URL'sini al**'a tıklayın, **varsayılan (İşlev anahtarı)** seçeneğini belirleyin ve ardından **Kopyala**'ya tıklayın. 

    ![Azure portalından işlev URL’sini kopyalama](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. İşlev URL'sini tarayıcınızın adres çubuğuna yapıştırın. `&name=<yourname>` sorgu dizesi değerini bu URL’nin sonuna ekleyin ve isteği yürütmek için klavyenizdeki `Enter` tuşuna basın. İşlev tarafından döndürülen yanıtın tarayıcıda gösterildiğini görürsünüz.  

    Edge tarayıcısındaki yanıtın bir örneği aşağıda verilmiştir (diğer tarayıcılar XML gösterebilir):

    ![Tarayıcıdaki işlev yanıtı.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    İstek URL’si, işlevinize HTTP üzerinden erişmek için varsayılan olarak gerekli olan bir anahtar içerir.   

3. İşleviniz çalıştığında, izleme bilgileri günlüklere yazılır. Önceki yürütme işleminden alınan izleme çıktısını görmek için, portalda işlevinize geri dönün ve ekranın altındaki oka tıklayarak **Günlükler**’i genişletin. 

   ![Azure portalında İşlevler günlük görüntüleyicisi.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a>Kaynakları temizleme

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Sonraki adımlar

HTTP ile tetiklenen basit bir işlevi kullanarak işlev uygulaması oluşturdunuz.  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Daha fazla bilgi için bkz. [Azure İşlevleri HTTP ve web kancası bağlamaları](functions-bindings-http-webhook.md).



