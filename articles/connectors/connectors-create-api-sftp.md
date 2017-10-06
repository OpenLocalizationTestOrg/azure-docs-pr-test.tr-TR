---
title: "aaaLearn nasıl toouse hello mantıksal uygulamalarınızı SFTP Bağlayıcısı | Microsoft Docs"
description: "Logic apps ile Azure uygulama hizmeti oluşturun. TooSFTP API toosend bağlanmak ve dosyaları alabilirsiniz. Gibi oluştururken, güncelleştirme, almak veya dosyaları silme çeşitli işlemler gerçekleştirebilirsiniz."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 697eb8b0-4a66-40c7-be7b-6aa6b131c7ad
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/20/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 3f50570191c9b9339fe6584b9056b2549512b789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sftp-connector"></a>Merhaba SFTP Bağlayıcısı ile çalışmaya başlama
Merhaba SFTP bağlayıcı tooaccess SFTP hesap toosend kullanın ve dosyaları alabilirsiniz. Gibi oluştururken, güncelleştirme, almak veya dosyaları silme çeşitli işlemler gerçekleştirebilirsiniz.  

toouse [tüm bağlayıcıların](apis-list.md), toocreate bir mantıksal uygulama ilk gerekir. Tarafından başlayabiliriz [şimdi mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toosftp"></a>TooSFTP Bağlan
Mantıksal uygulamanızı herhangi bir hizmet erişebilmeniz için önce toocreate ilk gerekiyor bir *bağlantı* toohello hizmet. A [bağlantı](connectors-overview.md) bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar.  

### <a name="create-a-connection-toosftp"></a>Bir bağlantı tooSFTP oluşturma
> [!INCLUDE [Steps toocreate a connection tooSFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a>SFTP tetikleyici kullanın
Bir tetikleyici bir mantıksal uygulama tanımlı kullanılan toostart hello iş akışı olabilecek bir olaydır. [Tetikleyiciler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

Bu örnekte, hello **bir dosya eklendiğinde veya SFTP -** tetikleyici olduğunda kullanılan tooinitiate mantığı uygulama iş akışı bir dosya için eklenemez veya bir SFTP sunucusunda, değiştirilemez. Ayrıca, hello yeni veya değiştirilmiş dosyasının Merhaba içeriğine denetler ve içeriğini, hello içeriği kullanmadan önce ayıklanması gereken olduğunu gösteriyorsa karar tooextract hello dosya yapar bir koşul de ekleyin. Son olarak, bir dosyanın bir eylem tooextract hello içeriğini ekleyin ve ayıklanan hello içeriği hello SFTP sunucusundaki bir klasöre yerleştirin. 

Kurumsal örnek, bu tetikleyici toomonitor SFTP klasörü müşteri siparişleri temsil eden yeni dosyaları kullanabilirsiniz.  Ardından bir SFTP bağlayıcı eylem gibi kullanabilir **dosya içeriğini almak**, tooget hello içeriği başka bir işleme ve siparişleri veritabanında depolama için hello sırası.

> [!INCLUDE [Steps toocreate an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a>Koşul ekle
> [!INCLUDE [Steps tooadd a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a>SFTP eylemini kullanın
Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir. [Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

> [!INCLUDE [Steps toocreate an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a>Bağlayıcı özgü ayrıntıları

Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/sftpconnector/).

## <a name="more-connectors"></a>Daha fazla bağlayıcılar
Toohello dönün [API'leri listesi](apis-list.md).
