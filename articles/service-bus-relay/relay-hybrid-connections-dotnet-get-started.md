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
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="6110d-103">Geçiş Karma Bağlantıları ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="6110d-103">Get started with Relay Hybrid Connections</span></span>
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="6110d-104">Bu öğretici çok tanıtılmaktadır[Azure geçişi karma bağlantılar](relay-what-is-it.md#hybrid-connections)ve nasıl toouse .NET toocreate gönderir bir istemci uygulaması tooa karşılık gelen dinleyicisi uygulama iletileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="6110d-104">This tutorial provides an introduction too[Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how toouse .NET toocreate a client application that sends messages tooa corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="6110d-105">Ne elde edilecek</span><span class="sxs-lookup"><span data-stu-id="6110d-105">What will be accomplished</span></span>
<span data-ttu-id="6110d-106">Karma bağlantılar, istemci ve sunucu bileşeni gerektirdiğinden, hello öğretici iki konsol uygulamaları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6110d-106">Because Hybrid Connections requires both a client and a server component, hello tutorial creates two console applications.</span></span> <span data-ttu-id="6110d-107">Merhaba adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="6110d-107">Here are hello steps:</span></span>

1. <span data-ttu-id="6110d-108">Hello Azure portal kullanarak bir geçiş ad alanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6110d-108">Create a Relay namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="6110d-109">Karma bağlantı hello Azure portal kullanarak bu ad alanında oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6110d-109">Create a hybrid connection in that namespace, using hello Azure portal.</span></span>
3. <span data-ttu-id="6110d-110">Bir sunucu (dinleyici) konsol uygulama tooreceive iletileri yazma.</span><span class="sxs-lookup"><span data-stu-id="6110d-110">Write a server (listener) console application tooreceive messages.</span></span>
4. <span data-ttu-id="6110d-111">Bir istemci (gönderen) konsol uygulama toosend iletileri yazma.</span><span class="sxs-lookup"><span data-stu-id="6110d-111">Write a client (sender) console application toosend messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6110d-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6110d-112">Prerequisites</span></span>

<span data-ttu-id="6110d-113">toocomplete Bu öğretici önkoşulları aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="6110d-113">toocomplete this tutorial, you'll need hello following prerequisites:</span></span>

1. <span data-ttu-id="6110d-114">[Visual Studio 2015 veya üzeri](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="6110d-114">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="6110d-115">Bu öğreticide Hello örnekler Visual Studio 2017 kullanın.</span><span class="sxs-lookup"><span data-stu-id="6110d-115">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="6110d-116">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="6110d-116">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="6110d-117">1. Hello Azure portal kullanarak ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6110d-117">1. Create a namespace using hello Azure portal</span></span>
<span data-ttu-id="6110d-118">Bir geçiş ad alanı zaten oluşturduysanız, toohello atlama [hello Azure portal kullanarak karma bağlantı oluşturma](#2-create-a-hybrid-connection-using-the-azure-portal) bölümü.</span><span class="sxs-lookup"><span data-stu-id="6110d-118">If you have already created a Relay namespace, jump toohello [Create a hybrid connection using hello Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a><span data-ttu-id="6110d-119">2. Hello Azure portal kullanarak karma bağlantı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6110d-119">2. Create a hybrid connection using hello Azure portal</span></span>
<span data-ttu-id="6110d-120">Karma bir bağlantı zaten oluşturduysanız, toohello atlama [bir sunucu uygulaması oluştur](#3-create-a-server-application-listener) bölümü.</span><span class="sxs-lookup"><span data-stu-id="6110d-120">If you have already created a hybrid connection, jump toohello [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="6110d-121">3. Sunucu uygulaması (dinleyici) oluşturma</span><span class="sxs-lookup"><span data-stu-id="6110d-121">3. Create a server application (listener)</span></span>
<span data-ttu-id="6110d-122">toolisten ileti alıp hello geçiş, biz Visual Studio kullanarak C# konsol uygulaması yazacaksınız.</span><span class="sxs-lookup"><span data-stu-id="6110d-122">toolisten and receive messages from hello Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="6110d-123">4. İstemci uygulaması (gönderici) oluşturma</span><span class="sxs-lookup"><span data-stu-id="6110d-123">4. Create a client application (sender)</span></span>
<span data-ttu-id="6110d-124">toosend iletileri toohello geçiş, Visual Studio kullanarak C# konsol uygulaması yazma.</span><span class="sxs-lookup"><span data-stu-id="6110d-124">toosend messages toohello Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-hello-applications"></a><span data-ttu-id="6110d-125">5. Merhaba uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="6110d-125">5. Run hello applications</span></span>
1. <span data-ttu-id="6110d-126">Merhaba sunucu uygulamasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6110d-126">Run hello server application.</span></span>
2. <span data-ttu-id="6110d-127">Merhaba istemci uygulaması çalıştırın ve bazı metin girin.</span><span class="sxs-lookup"><span data-stu-id="6110d-127">Run hello client application and enter some text.</span></span>
3. <span data-ttu-id="6110d-128">Merhaba sunucu hello istemci uygulamasında girilen uygulama Konsolu çıkışları hello metin emin olun.</span><span class="sxs-lookup"><span data-stu-id="6110d-128">Ensure that hello server application console outputs hello text that was entered in hello client application.</span></span>

![running-applications](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

<span data-ttu-id="6110d-130">Tebrikler, uçtan uca Karma Bağlantılar uygulaması oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="6110d-130">Congratulations, you have created an end-to-end Hybrid Connections application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6110d-131">Sonraki adımlar:</span><span class="sxs-lookup"><span data-stu-id="6110d-131">Next steps:</span></span>
* [<span data-ttu-id="6110d-132">Geçiş hakkında SSS</span><span class="sxs-lookup"><span data-stu-id="6110d-132">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="6110d-133">Ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6110d-133">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="6110d-134">Node kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="6110d-134">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

