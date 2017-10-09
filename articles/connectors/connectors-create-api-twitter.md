---
title: "aaaLearn nasıl toouse hello logic apps Twitter Bağlayıcısı | Microsoft Docs"
description: "Twitter Bağlayıcısı REST API parametrelerle genel bakış"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8bce2183-544d-4668-a2dc-9a62c152d9fa
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: ead4e4dc95bf894fd72b908c5375b407ba27642d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twitter-connector"></a>Merhaba Twitter Bağlayıcısı ile çalışmaya başlama
Merhaba Twitter Bağlayıcısı ile şunları yapabilirsiniz:

* Tweetler ve get tweet'leri
* Erişim zaman çizelgeleri, arkadaşlarınıza ve followers
* Diğer Eylemler ve aşağıda açıklanan Tetikleyicileri hello birini gerçekleştirin  

toouse [tüm bağlayıcıların](apis-list.md), toocreate bir mantıksal uygulama ilk gerekir. Tarafından başlayabiliriz [şimdi mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).  

## <a name="connect-tootwitter"></a>TooTwitter Bağlan
Mantıksal uygulamanızı herhangi bir hizmet erişebilmeniz için önce toocreate ilk gerekiyor bir *bağlantı* toohello hizmet. A [bağlantı](connectors-overview.md) bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar.  

### <a name="create-a-connection-tootwitter"></a>Bir bağlantı tooTwitter oluşturma
> [!INCLUDE [Steps toocreate a connection tooTwitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a>Bir Twitter tetikleyici kullanın
Bir tetikleyici bir mantıksal uygulama tanımlı kullanılan toostart hello iş akışı olabilecek bir olaydır. [Tetikleyiciler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

Bu örnekte, ı bunu nasıl yapacağınızı gösterir toouse hello **yeni tweet zaman nakledilir** #Seattle toosearch tetikleyebilir ve #Seattle bulunursa, Dropbox dosyasında hello tweet hello metinden ile güncelleştirin. Bir kurumsal örnekte hello şirketinizin adını arayın ve hello tweet hello metinden ile bir SQL veritabanı güncelleştirmesi.

1. Girin *twitter* hello arama kutusuna hello logic apps tasarımcısında hello seçip **yeni tweet gönderildiğinde Twitter -** tetikleyici   
   ![Twitter tetikleyici görüntü 1](./media/connectors-create-api-twitter/trigger-1.png)  
2. Girin *#Seattle* hello içinde **arama metni** denetimi  
   ![Twitter tetikleyici görüntü 2](./media/connectors-create-api-twitter/trigger-2.png) 

Bu noktada, mantıksal uygulamanızı hello yürütülmesi diğer tetikleyiciler ve Eylemler hello iş akışında başlayacak bir tetikleyici ile yapılandırıldı. 

> [!NOTE]
> Bir mantıksal uygulama toobe için işlev, en az bir tetikleyici ve bir eylem içermelidir. Merhaba sonraki bölümde tooadd eylemin Hello adımları izleyin.  
> 
> 

## <a name="add-a-condition"></a>Koşul ekle
Biz yalnızca 50'den fazla kullanıcısı olan kullanıcılardan tweet'leri ilginizi olduğundan, followers hello sayısı onaylar bir koşul toohello mantıksal uygulama ilk eklenmesi gerekir.  

1. Seçin **+ yeni adım** tooadd hello eylem istediğinizi tootake #Seattle içinde yeni bir tweet bulunduğunda  
   ![Twitter eylem görüntü 1](../../includes/media/connectors-create-api-twitter/action-1.png)  
2. Select hello **bir koşul eklemek** bağlantı.  
   ![Twitter koşul görüntü 1](../../includes/media/connectors-create-api-twitter/condition-1.png)   
   Merhaba açılır **koşulu** burada kontrol edebilirsiniz koşulları gibi denetim *eşittir*, *olan değerinden*, *değerinden daha büyük*, *içeren*, vb..  
   ![Twitter koşul görüntü 2](../../includes/media/connectors-create-api-twitter/condition-2.png)   
3. Select hello **bir değer seçin** denetim.  
   Bu denetimde, bir veya daha fazla hello özellik herhangi bir önceki eylem veya Tetikleyiciler koşulu değerlendirilen tootrue veya yanlış olacak hello değeri olarak seçebilirsiniz.
   ![Twitter koşul görüntü 3](../../includes/media/connectors-create-api-twitter/condition-3.png)   
4. Select hello **...**  tooexpand hello kullanılabilir olan tüm hello özellikler görebilmeniz için özelliklerin listesi.        
   ![Twitter koşul görüntü 4](../../includes/media/connectors-create-api-twitter/condition-4.png)   
5. Select hello **Followers sayısı** özelliği.    
   ![Twitter koşul görüntü 5](../../includes/media/connectors-create-api-twitter/condition-5.png)   
6. Count özelliği hello değer denetiminde sunulmuştur hello Followers dikkat edin.    
   ![Twitter koşul görüntü 6](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. Seçin **değerinden daha büyük** hello işleçleri listesinden.    
   ![Twitter koşul görüntü 7](../../includes/media/connectors-create-api-twitter/condition-7.png)   
8. Merhaba işleneni hello 50 girin *değerinden daha büyük* işleci.  
   Merhaba koşulu şimdi eklenir. Hello kullanarak çalışmanızı kaydedin **kaydetmek** yukarıdaki hello menüsünde bağlantısı.    
   ![Twitter koşul görüntü 8](../../includes/media/connectors-create-api-twitter/condition-8.png)   

## <a name="use-a-twitter-action"></a>Bir Twitter eylemi kullanın
Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir. [Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

Bir tetikleyici eklediğiniz, bu adımları tooadd hello tetik tarafından bulunan hello tweet'leri hello içeriğiyle yeni tweet gönderecek bir eylem izleyin. Bu kılavuz Hello amaçları için yalnızca 50'den fazla followers sahip kullanıcılardan tweet'leri nakledilir.  

Merhaba sonraki adımda, 50'den fazla followers sahip bir kullanıcı tarafından gönderilen her tweet hello özelliklerini bazıları kullanarak tweet gönderecek bir Twitter eylemi ekleyeceksiniz.  

1. Seçin **Eylem Ekle**. Bu, diğer eylemler ve Tetikleyiciler için arayabileceğiniz hello arama denetimini açar.  
   ![Twitter koşul görüntü 9](../../includes/media/connectors-create-api-twitter/condition-9.png)   
2. Girin *twitter* hello arama kutusuna hello seçip **Twitter - tweet sonrası** eylem. Merhaba açılır **tweet sonrası** gönderilmesini hello tweet için tüm ayrıntıları gireceğiniz denetim.      
   ![Eylem görüntü 1-5 twitter](../../includes/media/connectors-create-api-twitter/action-1-5.png)   
3. Select hello **Tweet metin** denetim. Tüm çıktıları önceki Eylemler ve Tetikleyicileri hello mantıksal uygulama içinde görünür. Aşağıdakilerden herhangi birini seçin ve hello tweet hello yeni tweet metninin bir parçası olarak kullanın.     
   ![Twitter eylem görüntü 2](../../includes/media/connectors-create-api-twitter/action-2.png)   
4. Seçin **kullanıcı adı**   
5. Girin *diyor:* hello tweet metin denetimi. Yalnızca kullanıcı adından sonra bunu.  
6. Seçin *Tweet metin*.       
   ![Twitter eylem görüntüsü 3](../../includes/media/connectors-create-api-twitter/action-3.png)   
7. Çalışmanızı kaydedin ve iş akışınızı hello #Seattle diyez tooactivate ile tweet gönderecek.  


## <a name="connector-specific-details"></a>Bağlayıcı özgü ayrıntıları

Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/twitterconnector/). 

## <a name="next-steps"></a>Sonraki adımlar
[Mantıksal uygulama oluşturun.](../logic-apps/logic-apps-create-a-logic-app.md)

