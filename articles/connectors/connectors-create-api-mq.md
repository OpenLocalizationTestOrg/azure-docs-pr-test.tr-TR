---
title: "aaaLearn nasıl toouse hello Azure Logic Apps MQ Bağlayıcısı | Microsoft Docs"
description: "Tooan şirket içi veya Azure MQ server, mantığı uygulama iş akışı toobrowse bağlanmak, almak ve iletileri tooWebSphere MQ Gönder"
services: logic-apps
author: valthom
manager: anneta
documentationcenter: 
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 06/01/2017
ms.author: valthom; ladocs
ms.openlocfilehash: 8b36d53b457ced1a7461c229aecfcf8e4ae668a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-ibm-mq-server-from-logic-apps-using-hello-mq-connector"></a>Merhaba MQ Bağlayıcısı'nı kullanarak mantığı uygulamalardan tooan IBM MQ server Bağlan 

MQ için Microsoft Connector gönderir ve MQ Server şirket içi veya Azure depolanan iletilerini alır. Bu bağlayıcı bir TCP/IP ağı üzerinden bir uzak IBM MQ sunucuyla iletişim kuran bir Microsoft MQ istemcisi içerir. Bu belgede bir başlangıç kılavuzu toouse hello MQ Bağlayıcıdır. Tek bir ileti üzerinde bir sıra göz atarak başlayın ve ardından çalışırken hello diğer eylemler önerilir.    

Merhaba MQ bağlayıcı eylemleri aşağıdaki hello içerir. Hiçbir Tetikleyicileri vardır.

-   IBM MQ Server hello selamlama iletisine silmeden tek İletiye Gözat
-   IBM MQ Server hello Merhaba iletileri silmeden toplu iletiler Gözat
-   Tek bir ileti alırsınız ve hello message IBM MQ Server hello silin
-   Toplu iletiler almak ve IBM MQ Server hello Merhaba iletileri sil
-   Tek ileti toohello IBM MQ Server Gönder 

## <a name="prerequisites"></a>Ön koşullar

* Bir şirket içi MQ server kullanıyorsanız [hello şirket içi veri ağ geçidi yükleme](../logic-apps/logic-apps-gateway-install.md) ağınızdaki bir sunucuda. Merhaba MQ Server genel olarak kullanılabilir veya Azure içinde kullanılabilir değilse, ardından hello veri ağ geçidi kullanılan gerekli veya değil.

    > [!NOTE]
    > Merhaba sunucu şirket içi veri ağ geçidinin yüklü hello gerekir de sahip olduğu .net Framework 4.6 hello MQ bağlayıcı toofunction için yüklü.

* Merhaba hello şirket içi veri ağ geçidi için-Azure kaynağını oluşturma [hello veri ağ geçidi bağlantısı kurma](../logic-apps/logic-apps-gateway-connection.md).

* Resmi olarak IBM WebSphere MQ sürümleri desteklenir:
   * MQ 7.5
   * MQ 8.0

## <a name="create-a-logic-app"></a>Mantıksal uygulama oluşturma

1. Merhaba, **Azure başlangıç Panosu**seçin  **+**  (artı işareti) **Web + mobil**ve ardından **mantıksal uygulama**. 
2. Merhaba girin **adı**, MQTestApp gibi **abonelik**, **kaynak grubu**, ve **konumu** (Merhaba konumu hello kullanın Şirket içi veri ağ geçidi bağlantı yapılandırılır). Seçin **PIN toodashboard**seçip **oluşturma**.  
![Mantıksal uygulama oluşturma](media/connectors-create-api-mq/Create_Logic_App.png)

## <a name="add-a-trigger"></a>Bir tetikleyici Ekle

> [!NOTE]
> Merhaba MQ bağlayıcı hiçbir tetikleyici yok. Bu nedenle, başka bir tetikleyici toostart hello gibi mantıksal uygulamanızı kullanmak **yineleme** tetikleyici. 

1. Merhaba **Logic Apps Tasarımcısı** açar, select **yineleme** ortak Tetikleyicileri hello listesinde.
2. Seçin **Düzenle** hello yinelenme tetikleyici içinde. 
3. Set hello **sıklığı** çok**gün**ve kümesi hello **aralığı** çok**7**. 

## <a name="browse-a-single-message"></a>Tek bir iletiye Gözat
1. Seçin **+ yeni adım**seçip **Eylem Ekle**.
2. Merhaba arama kutusuna yazın `mq`ve ardından **MQ - Gözat ileti**.  
![İleti Gözat](media/connectors-create-api-mq/Browse_message.png)

3. Varolan MQ bağlantısı yoksa hello bağlantısı oluştur:  

    1. Seçin **Connect şirket içi veri ağ geçidi üzerinden**ve MQ sunucunuzun hello özelliklerini girin.  
    İçin **Server**, hello MQ sunucu adı girin veya izleyen iki nokta üst üste ve başlangıç bağlantı noktası numarası ile başlangıç IP adresi girin. 
    2. Merhaba **ağ geçidi** açılır yapılandırılmış var olan tüm ağ geçidi bağlantıları listeler. Ağ geçidi seçin.
    3. Seçin **oluşturma** bitirdikten sonra. Bağlantınızı benzer toohello aşağıdaki gibidir:   
    ![Bağlantı özellikleri](media/connectors-create-api-mq/Connection_Properties.png)

4. Merhaba eylem Özellikleri'nde, şunları yapabilirsiniz:  

    * Kullanım hello **sıra** özelliği tooaccess hello bağlantısı içinde tanımlanan daha farklı kuyruk adı
    * Kullanım hello **MessageID**, **correlationıd değeri**, **GroupID**ve diğer özellikleri toobrowse hello farklı MQ ileti özelliğe göre bir ileti için
    * Ayarlama **IncludeInfo** çok**True** tooinclude ek ileti bilgi hello çıkışı. Ya da çok ayarlayın**False** toonot hello çıktısında ek ileti bilgiler içerir.
    * Girin bir **zaman aşımı** değeri toodetermine ileti tooarrive boş bir sorgudaki için ne kadar süreyle toowait. Hiçbir şey girilirse, hello sıradaki ilk iletiyi hello alınır ve ileti tooappear için beklerken geçen hiçbir zaman yok.  
    ![İleti özelliklerini göz atın](media/connectors-create-api-mq/Browse_message_Props.png)

5. **Kaydet** yaptığınız değişiklikleri ve ardından **çalıştırmak** mantıksal uygulamanızı:  
![Kaydet ve Çalıştır](media/connectors-create-api-mq/Save_Run.png)

6. Birkaç saniye sonra çalıştırmak hello hello adımları gösterilir ve hello çıkışına arayabilir. Her bir adımın Hello yeşil onay işareti toosee Ayrıntılar'ı seçin. Seçin **bkz ham çıkışları** hello hakkında daha fazla ayrıntı toosee çıkış verileri.  
![İleti çıkış Gözat](media/connectors-create-api-mq/Browse_message_output.png)  

    Ham çıktı:  
    ![İleti ham çıkış Gözat](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. Ne zaman hello **IncludeInfo** seçeneği tootrue ayarlanmışsa, çıktı aşağıdaki hello görüntülenir:  
![Gözat iletiyi bilgisi Ekle](media/connectors-create-api-mq/Browse_message_Include_Info.png)

## <a name="browse-multiple-messages"></a>Birden çok ileti Gözat
Merhaba **Gözat iletileri** eylemi içeren bir **BatchSize** seçeneği tooindicate kaç iletileri döndürülüp döndürülmediğini hello sıradan.  Varsa **BatchSize** giriş yok, tüm iletileri döndürülür. Merhaba çıktı iletileri dizisi döndürülür.

1. Merhaba eklerken **Gözat iletileri** eylem, yapılandırılmış hello ilk bağlantı, varsayılan olarak seçilidir. Seçin **değiştirmek bağlantı** toocreate yeni bir bağlantı veya farklı bir bağlantı seçin.

2. Gözat Hello çıktısını gösterir iletileri:  
![İletileri çıkış Gözat](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a>Tek bir ileti alırsınız
Merhaba **alma iletisi** eylem sahip hello aynı girişleri ve çıkışları hello **Gözat ileti** eylem. Kullanırken **alma iletisi**, selamlama iletisine hello sıradan silinir.

## <a name="receive-multiple-messages"></a>Birden çok ileti alma
Merhaba **alma iletileri** eylem sahip hello aynı girişleri ve çıkışları hello **Gözat iletileri** eylem. Kullanırken **alma iletileri**, karışılama iletileri hello sıradan silinir.

Varsa hiçbir ileti hello sırada bir Gözat veya alma işlemi yaparken, hello adım çıkış aşağıdaki hello ile başarısız olur:  
![MQ yok, hata iletisi](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a>İleti gönderme
1. Merhaba eklerken **ileti gönder** eylem, yapılandırılmış hello ilk bağlantı, varsayılan olarak seçilidir. Seçin **değiştirmek bağlantı** toocreate yeni bir bağlantı veya farklı bir bağlantı seçin. Merhaba geçerli **ileti türleri** olan **veri birimi**, **yanıt**, veya **isteği**.  
![Msg özellik Gönder](media/connectors-create-api-mq/Send_Msg_Props.png)

2. Merhaba ileti gönder çıktısını hello aşağıdaki gibi görünür:  
![Msg çıkış Gönder](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a>Bağlayıcı özgü ayrıntıları

Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/mq/).

## <a name="next-steps"></a>Sonraki adımlar
[Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md). Araştır Logic Apps içinde kullanılabilir diğer bağlayıcıları hello bizim [API'leri listesi](apis-list.md).
