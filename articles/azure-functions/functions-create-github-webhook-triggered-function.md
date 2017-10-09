---
title: "aaaCreate GitHub Web kancası tarafından tetiklenen Azure işlevinde | Microsoft Docs"
description: "Azure işlevleri toocreate GitHub Web kancası tarafından çağrılan sunucusuz bir işlevini kullanın."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 36ef34b8-3729-4940-86d2-cb8e176fcc06
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 8ffcde82c9310d749159ed53eab113658e38a030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-github-webhook"></a>GitHub web kancası tarafından tetiklenen bir işlev oluşturma

Bilgi nasıl toocreate HTTP Web kancası isteğiyle bir GitHub özgü yükü tarafından tetiklenen bir işlev.

![Github Web kancası hello Azure portal işlevinde tetiklendi](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Ön koşullar

+ En az bir proje içeren bir GitHub hesabı.
+ Azure aboneliği. Aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Azure İşlev uygulaması oluşturma

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![İşlev uygulaması başarıyla oluşturuldu.](./media/functions-create-first-azure-function/function-app-create-success.png)

Ardından, hello yeni işlev uygulamada bir işlev oluşturun.

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a>GitHub web kancası ile tetiklenen bir işlev oluşturma

1. Merhaba, işlev uygulaması'nı genişletin ve  **+**  sonraki çok düğmesini**işlevler**. Bu işlev uygulamanızda hello ilk işlevi ise seçin **özel işlevi**. Merhaba eksiksiz işlev şablonları görüntüler.

    ![Hello Azure portalı hızlı başlangıç sayfasında işlevleri](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. Select hello **GitHub Web kancası** istediğiniz dili için şablon. **İşlevinizi adlandırın** ve ardından **Oluştur**'a tıklayın.

     ![GitHub Web kancası tetiklenen işlevi hello Azure portal oluşturma](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

3. Yeni işlevinizi tıklatın **<> / Get işlevi URL**, daha sonra kopyalayın ve başlangıç değerleri kaydedin. Aynı şeyi hello **<> / alma GitHub gizli**. Bu değerleri tooconfigure hello Web kancası Github'da kullanın.

    ![Merhaba işlevi kod gözden geçirme](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

Ardından, GitHub deponuzda web kancasını oluşturursunuz.

## <a name="configure-hello-webhook"></a>Merhaba Web kancası yapılandırın

1. Github'da, sahip olduğunuz tooa depo gidin. Varsa çatallandırdığınız depoları da kullanabilirsiniz. Toofork depo gerekiyorsa kullanın <https://github.com/Azure-Samples/functions-quickstart>.

1. **Ayarlar**’a tıklayın, sonra da **Web Kancaları**’na ve **Web kancası ekle**’ye tıklayın.

    ![GitHub web kancası ekleme](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. Merhaba tabloda belirtildiği gibi ayarları kullanın ve ardından **Web kancası eklemek**.

    ![Merhaba Web kancası URL'si ve parolasını ayarlayın](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| Ayar | Önerilen değer | Açıklama |
|---|---|---|
| **Yük URL'si** | Kopyalanan değer | Tarafından döndürülen hello değeri kullanmak **<> / Get işlevi URL**. |
| **Gizli dizi**   | Kopyalanan değer | Tarafından döndürülen hello değeri kullanmak **<> / alma GitHub gizli**. |
| **İçerik türü** | uygulama/json | Merhaba işlevi bir JSON yükü bekliyor. |
| Olay tetikleyicileri | Olayları ayrı ayrı seçmeme izin ver | Yalnızca tootrigger sorunu açıklama olaylarına istiyoruz.  |
| | Sorun açıklaması |  |

Şimdi, Web kancası hello yeni bir sorun açıklama eklendiğinde yapılandırılmış tootrigger işlevinizi olur.

## <a name="test-hello-function"></a>Test hello işlevi

1. Merhaba, GitHub deposunda açmak **sorunları** yeni bir tarayıcı penceresi sekmesindedir.

1. Merhaba yeni penceresinde **yeni sorun**bir başlık yazın ve ardından **yeni sorun gönderme**.

1. Merhaba sayısındaki bir yorum yazın ve'ı tıklatın **açıklama**.

    ![GitHub sorun açıklaması ekleyin.](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. Toohello portalına geri dönün ve hello günlüklerine bakın. Merhaba yeni açıklama metni içeren bir izleme girişi görmeniz gerekir.

     ![Merhaba açıklama metni hello günlüklerinde görüntüleyin.](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a>Kaynakları temizleme

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Sonraki adımlar

GitHub web kancasından istek alındığında çalıştırılan bir işlev oluşturdunuz.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Web kancası bağlamaları hakkında daha fazla bilgi için bkz. [Azure İşlevleri HTTP ve web kancası bağlamaları](functions-bindings-http-webhook.md).
