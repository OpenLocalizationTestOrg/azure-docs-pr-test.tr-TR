---
title: "Azure mantıksal uygulamaları aaaDropbox Bağlayıcısı | Microsoft Docs"
description: "Logic apps ile Azure uygulama hizmeti oluşturun. TooDropbox toomanage dosyalarınızı bağlayın. Karşıya yükleme gibi çeşitli eylemleri, güncelleştirme, almak ve Dropbox dosyaları silin."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: cb0ae033-aba7-4ac9-beaa-be561a0f0cac
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 1f307477836104c0bc0008341604a1400860987f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-dropbox-connector"></a>Merhaba Dropbox Bağlayıcısı ile çalışmaya başlama
TooDropbox toomanage dosyalarınızı bağlayın. Karşıya yükleme gibi çeşitli eylemleri, güncelleştirme, almak ve Dropbox dosyaları silin.

toouse [tüm bağlayıcıların](apis-list.md), toocreate bir mantıksal uygulama ilk gerekir. Tarafından başlayabiliriz [şimdi mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toodropbox"></a>TooDropbox Bağlan
Mantıksal uygulamanızı herhangi bir hizmet erişebilmeniz için önce toocreate ilk gerekiyor bir *bağlantı* toohello hizmet. Bağlantı bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar. Örneğin, sipariş tooconnect tooDropbox ilk açılan kutu ihtiyacınız *bağlantı*. toocreate bir bağlantı, normalde tooconnect için istediğiniz tooaccess hello hizmeti kullandığınız tooprovide hello kimlik bilgileri gerekir. Bu nedenle, hello Dropbox örnekte hello kimlik bilgilerini tooyour sipariş toocreate hello bağlantı tooDropbox Dropbox hesabı gerekir. [Bağlantılar hakkında daha fazla bilgi edinin]()

### <a name="create-a-connection-toodropbox"></a>Bir bağlantı tooDropbox oluşturma
> [!INCLUDE [Steps toocreate a connection tooDropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a>Bir Dropbox tetikleyici kullanın
Bir tetikleyici bir mantıksal uygulama tanımlı kullanılan toostart hello iş akışı olabilecek bir olaydır. [Tetikleyiciler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

Bu örnekte, hello kullanacağız **bir dosya oluşturulduğunda** tetikleyici. Bu tetikleyici oluştuğunda hello numarayı arayacaktır **alma yolunu kullanarak dosya içeriğini** Dropbox eylem. 

1. Girin *dropbox* hello arama kutusuna hello Logic Apps tasarımcısında hello seçip **bir dosya oluşturulduğunda, Dropbox -** tetikleyici.      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. Tootrack dosya oluşturma istediğiniz hello klasörünü seçin. Seçin... (kırmızı hello kutusunda tanımlanır) ve istediğiniz tooselect hello tetikleyici için giriş Gözat toohello klasör.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a>Bir Dropbox eylemi kullanın
Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir. [Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

Merhaba tetikleyici eklenmiş durumda, bu adımları tooadd hello yeni dosyanın içeriğini alacak bir eylem izleyin.

1. Seçin **+ yeni adım** tooadd hello eylem istediğinizi tootake yeni bir dosya oluşturulurken.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. Seçin **Eylem Ekle**. Bu açılır hello arama kutusu için herhangi bir işlem, arayabileceğiniz tootake ister.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. Girin *dropbox* Eylemler ilgili tooDropbox toosearch.  
4. Seçin **Dropbox - yolunu kullanarak dosya alma içeriği** eylem tootake hello olarak yeni bir dosya hello oluşturulduğunda Dropbox klasörü seçilen. Merhaba eylem denetim bloğu açılır. İstendiğinde tooauthorize, Dropbox hesabını, daha önce yapmadıysanız, logic app tooaccess olacaktır.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. Seçin... (Merhaba sağ tarafında hello bulunan **dosya yolu** denetimi) ve toouse istediğinizi toohello dosya yolu göz atın. Ya da hello kullan **dosya yolu** belirteci toospeed logic app oluşturma ayarlama.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. Çalışmanızı kaydedin ve iş akışınızı Dropbox tooactivate yeni bir dosya oluşturun.  

## <a name="connector-specific-details"></a>Bağlayıcı özgü ayrıntıları

Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/dropbox/).

## <a name="more-connectors"></a>Daha fazla bağlayıcılar
Toohello dönün [API'leri listesi](apis-list.md).
