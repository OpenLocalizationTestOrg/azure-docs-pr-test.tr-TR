---
title: "aaaCreate azure'da bir zamanlamaya göre çalışan bir işlev | Microsoft Docs"
description: "Nasıl toocreate çalıştıran Azure işlevinde tanımladığınız bir zamanlamaya göre öğrenin."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: ba50ee47-58e0-4972-b67b-828f2dc48701
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 793b06a65a154466dfd4c121bcc88082227cd597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a>Azure’da bir zamanlayıcı tarafından tetiklenen bir işlev oluşturma

Nasıl toouse Azure işlevleri toocreate çalıştırılan bir işlevi tanımladığınız bir zamanlamaya bağlı öğrenin.

![Hello Azure portal işlev uygulaması oluşturma](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu öğretici:

+ Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Azure İşlev uygulaması oluşturma

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![İşlev uygulaması başarıyla oluşturuldu.](./media/functions-create-first-azure-function/function-app-create-success.png)

Ardından, hello yeni işlev uygulamada bir işlev oluşturun.

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a>Zamanlayıcı ile tetiklenen işlev oluşturma

1. Merhaba, işlev uygulaması'nı genişletin ve  **+**  sonraki çok düğmesini**işlevler**. Bu işlev uygulamanızda hello ilk işlevi ise seçin **özel işlevi**. Merhaba eksiksiz işlev şablonları görüntüler.

    ![Hello Azure portalı hızlı başlangıç sayfasında işlevleri](./media/functions-create-scheduled-function/add-first-function.png)

2. Select hello **TimerTrigger** istediğiniz dili için şablon. Ardından hello tabloda belirtildiği gibi hello ayarları kullanın:

    ![Zamanlayıcı tetiklenen bir işlev hello Azure portal oluşturun.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | Ayar | Önerilen değer | Açıklama |
    |---|---|---|
    | **İşlevinizi adlandırın** | TimerTriggerCSharp1 | Tetiklenen Zamanlayıcı işlevinizin Hello adını tanımlar. |
    | **[Zamanlama](http://en.wikipedia.org/wiki/Cron#CRON_expression)** | 0 \*/1 \* \* \* \* | Altı alan [CRON ifade](http://en.wikipedia.org/wiki/Cron#CRON_expression) , işlevi toorun dakikada zamanlar. |

2. **Oluştur**'a tıklayın. Seçtiğiniz dilde her dakika çalışan bir işlev oluşturulur.

3. Yürütme toohello günlüklerine yazılmış izleme bilgilerini görüntüleyerek doğrulayın.

    ![İşlevler Görüntüleyicisi hello Azure portalında oturum açın.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

Şimdi, böylece daha az sıklıkta saatte gibi çalışır hello işlevin zamanlamasını değiştirebilirsiniz. 

## <a name="update-hello-timer-schedule"></a>Güncelleştirme hello Zamanlayıcı zamanlaması

1. İşlevinizi genişletin ve **Tümleştir**’e tıklayın. Bu, giriş tanımlayın ve bağlamaları işlevi için çıktı ve hello ayarlamaktır yerdir. 

2. `0 0 */1 * * *` şeklinde yeni bir **Zamanlama** değeri girin ve **Kaydet**’e tıklayın.  

![İşlevler hello Azure portal Zamanlayıcı zamanlamada güncelleştirin.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

Saatte bir çalışan bir işleviniz oldu. 

## <a name="clean-up-resources"></a>Kaynakları temizleme

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Sonraki adımlar

Bir zamanlamaya göre çalışan bir işlev oluşturdunuz.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Zamanlayıcı tetikleyicileri hakkında daha fazla bilgi edinmek için bkz. [Azure İşlevleri ile kod yürütme zamanlama](functions-bindings-timer.md).