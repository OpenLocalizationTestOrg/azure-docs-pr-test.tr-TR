---
title: "Azure geçişi karma bağlantılar düğümünde aaaGet Başlarken | Microsoft Docs"
description: "Azure Geçiş Karma Bağlantıları için bir Node.js konsol uygulaması yazın."
services: service-bus-relay
documentationcenter: node
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e44e4867-3cf3-46be-8f8a-7671e2013bc4
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: node
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: 235548399570074f7fd160fec28de8d3633625c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a>Geçiş Karma Bağlantıları ile çalışmaya başlama

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

Bu öğretici çok tanıtılmaktadır[Azure geçişi karma bağlantılar](relay-what-is-it.md#hybrid-connections)ve nasıl toouse Node.js toocreate gönderir bir istemci uygulaması tooa karşılık gelen dinleyicisi uygulama iletileri gösterir. 

## <a name="what-will-be-accomplished"></a>Ne elde edilecek

Karma Bağlantılar hem istemci hem de sunucu bileşenini gerektirdiğinden bu öğreticide iki konsol uygulaması oluşturulacaktır. Merhaba adımlar şunlardır:

1. Hello Azure portal kullanarak bir geçiş ad alanı oluşturun.
2. Hello Azure portal kullanarak bir karma bağlantı oluşturun.
3. Bir sunucu konsol uygulaması tooreceive iletileri yazma.
4. Bir istemci konsol uygulaması toosend iletileri yazma.

## <a name="prerequisites"></a>Ön koşullar

1. [Node.js](https://nodejs.org/en/).
2. Azure aboneliği.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Hello Azure portal kullanarak ad alanı oluşturma

Oluşturulan bir geçiş ad alanı zaten varsa, toohello atlama [hello Azure portal kullanarak karma bağlantı oluşturma](#2-create-a-hybrid-connection-using-the-azure-portal) bölümü.

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a>2. Hello Azure portal kullanarak karma bağlantı oluşturma

Oluşturulan karma bir bağlantı zaten varsa, toohello atlama [bir sunucu uygulaması oluştur](#3-create-a-server-application-listener) bölümü.

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a>3. Sunucu uygulaması (dinleyici) oluşturma

toolisten ileti alıp hello geçiş, biz bir Node.js konsol uygulamasını yazacaksınız.

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a>4. İstemci uygulaması (gönderici) oluşturma

toosend biz bir Node.js konsol uygulamasını yazacaksınız toohello geçiş iletileri.

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-hello-applications"></a>5. Merhaba uygulamaları çalıştırma

1. Merhaba sunucu uygulamayı çalıştırın: Node.js komut istemi türünden `node listener.js`.
2. Merhaba istemci uygulaması çalıştırın: Node.js komut istemi türünden `node sender.js`ve bazı metin girin.
3. Merhaba sunucu hello istemci uygulamasında girilen uygulama Konsolu çıkışları hello metin emin olun.

![running-applications](./media/relay-hybrid-connections-node-get-started/running-applications.png)

Tebrikler, Node.js kullanarak uçtan uca bir Karma Bağlantılar uygulaması oluşturdunuz!

## <a name="next-steps"></a>Sonraki adımlar:

* [Geçiş hakkında SSS](relay-faq.md)
* [Ad alanı oluşturma](relay-create-namespace-portal.md)
* [.NET kullanmaya başlama](relay-hybrid-connections-dotnet-get-started.md)
* [Node kullanmaya başlama](relay-hybrid-connections-node-get-started.md)

