---
title: ".NET içinde Azure geçişi karma bağlantılar aaaGet Başlarken | Microsoft Docs"
description: "Azure Geçişi Karma Bağlantıları için bir C# konsol uygulaması yazın."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d1386900-b942-4abf-acfc-38d2ef826253
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: 1e4af28e7cd4393c8ca965a149a0b83ebcc44f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a>Geçiş Karma Bağlantıları ile çalışmaya başlama
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

Bu öğretici çok tanıtılmaktadır[Azure geçişi karma bağlantılar](relay-what-is-it.md#hybrid-connections)ve nasıl toouse .NET toocreate gönderir bir istemci uygulaması tooa karşılık gelen dinleyicisi uygulama iletileri gösterir. 

## <a name="what-will-be-accomplished"></a>Ne elde edilecek
Karma bağlantılar, istemci ve sunucu bileşeni gerektirdiğinden, hello öğretici iki konsol uygulamaları oluşturur. Merhaba adımlar şunlardır:

1. Hello Azure portal kullanarak bir geçiş ad alanı oluşturun.
2. Karma bağlantı hello Azure portal kullanarak bu ad alanında oluşturun.
3. Bir sunucu (dinleyici) konsol uygulama tooreceive iletileri yazma.
4. Bir istemci (gönderen) konsol uygulama toosend iletileri yazma.

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu öğretici önkoşulları aşağıdaki hello gerekir:

1. [Visual Studio 2015 veya üzeri](http://www.visualstudio.com). Bu öğreticide Hello örnekler Visual Studio 2017 kullanın.
2. Azure aboneliği.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Hello Azure portal kullanarak ad alanı oluşturma
Bir geçiş ad alanı zaten oluşturduysanız, toohello atlama [hello Azure portal kullanarak karma bağlantı oluşturma](#2-create-a-hybrid-connection-using-the-azure-portal) bölümü.

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a>2. Hello Azure portal kullanarak karma bağlantı oluşturma
Karma bir bağlantı zaten oluşturduysanız, toohello atlama [bir sunucu uygulaması oluştur](#3-create-a-server-application-listener) bölümü.

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a>3. Sunucu uygulaması (dinleyici) oluşturma
toolisten ileti alıp hello geçiş, biz Visual Studio kullanarak C# konsol uygulaması yazacaksınız.

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a>4. İstemci uygulaması (gönderici) oluşturma
toosend iletileri toohello geçiş, Visual Studio kullanarak C# konsol uygulaması yazma.

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-hello-applications"></a>5. Merhaba uygulamaları çalıştırma
1. Merhaba sunucu uygulamasını çalıştırın.
2. Merhaba istemci uygulaması çalıştırın ve bazı metin girin.
3. Merhaba sunucu hello istemci uygulamasında girilen uygulama Konsolu çıkışları hello metin emin olun.

![running-applications](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

Tebrikler, uçtan uca Karma Bağlantılar uygulaması oluşturdunuz.

## <a name="next-steps"></a>Sonraki adımlar:
* [Geçiş hakkında SSS](relay-faq.md)
* [Ad alanı oluşturma](relay-create-namespace-portal.md)
* [Node kullanmaya başlama](relay-hybrid-connections-node-get-started.md)

