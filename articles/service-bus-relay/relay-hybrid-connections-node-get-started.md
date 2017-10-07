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
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="9c08a-103">Geçiş Karma Bağlantıları ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="9c08a-103">Get started with Relay Hybrid Connections</span></span>

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="9c08a-104">Bu öğretici çok tanıtılmaktadır[Azure geçişi karma bağlantılar](relay-what-is-it.md#hybrid-connections)ve nasıl toouse Node.js toocreate gönderir bir istemci uygulaması tooa karşılık gelen dinleyicisi uygulama iletileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="9c08a-104">This tutorial provides an introduction too[Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how toouse Node.js toocreate a client application that sends messages tooa corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="9c08a-105">Ne elde edilecek</span><span class="sxs-lookup"><span data-stu-id="9c08a-105">What will be accomplished</span></span>

<span data-ttu-id="9c08a-106">Karma Bağlantılar hem istemci hem de sunucu bileşenini gerektirdiğinden bu öğreticide iki konsol uygulaması oluşturulacaktır.</span><span class="sxs-lookup"><span data-stu-id="9c08a-106">Because Hybrid Connections requires both a client and a server component, we will create two console applications in this tutorial.</span></span> <span data-ttu-id="9c08a-107">Merhaba adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9c08a-107">Here are hello steps:</span></span>

1. <span data-ttu-id="9c08a-108">Hello Azure portal kullanarak bir geçiş ad alanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9c08a-108">Create a Relay namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="9c08a-109">Hello Azure portal kullanarak bir karma bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9c08a-109">Create a hybrid connection, using hello Azure portal.</span></span>
3. <span data-ttu-id="9c08a-110">Bir sunucu konsol uygulaması tooreceive iletileri yazma.</span><span class="sxs-lookup"><span data-stu-id="9c08a-110">Write a server console application tooreceive messages.</span></span>
4. <span data-ttu-id="9c08a-111">Bir istemci konsol uygulaması toosend iletileri yazma.</span><span class="sxs-lookup"><span data-stu-id="9c08a-111">Write a client console application toosend messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c08a-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9c08a-112">Prerequisites</span></span>

1. <span data-ttu-id="9c08a-113">[Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="9c08a-113">[Node.js](https://nodejs.org/en/).</span></span>
2. <span data-ttu-id="9c08a-114">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="9c08a-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="9c08a-115">1. Hello Azure portal kullanarak ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9c08a-115">1. Create a namespace using hello Azure portal</span></span>

<span data-ttu-id="9c08a-116">Oluşturulan bir geçiş ad alanı zaten varsa, toohello atlama [hello Azure portal kullanarak karma bağlantı oluşturma](#2-create-a-hybrid-connection-using-the-azure-portal) bölümü.</span><span class="sxs-lookup"><span data-stu-id="9c08a-116">If you already have a Relay namespace created, jump toohello [Create a hybrid connection using hello Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a><span data-ttu-id="9c08a-117">2. Hello Azure portal kullanarak karma bağlantı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9c08a-117">2. Create a hybrid connection using hello Azure portal</span></span>

<span data-ttu-id="9c08a-118">Oluşturulan karma bir bağlantı zaten varsa, toohello atlama [bir sunucu uygulaması oluştur](#3-create-a-server-application-listener) bölümü.</span><span class="sxs-lookup"><span data-stu-id="9c08a-118">If you already have a hybrid connection created, jump toohello [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="9c08a-119">3. Sunucu uygulaması (dinleyici) oluşturma</span><span class="sxs-lookup"><span data-stu-id="9c08a-119">3. Create a server application (listener)</span></span>

<span data-ttu-id="9c08a-120">toolisten ileti alıp hello geçiş, biz bir Node.js konsol uygulamasını yazacaksınız.</span><span class="sxs-lookup"><span data-stu-id="9c08a-120">toolisten and receive messages from hello Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="9c08a-121">4. İstemci uygulaması (gönderici) oluşturma</span><span class="sxs-lookup"><span data-stu-id="9c08a-121">4. Create a client application (sender)</span></span>

<span data-ttu-id="9c08a-122">toosend biz bir Node.js konsol uygulamasını yazacaksınız toohello geçiş iletileri.</span><span class="sxs-lookup"><span data-stu-id="9c08a-122">toosend messages toohello Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-hello-applications"></a><span data-ttu-id="9c08a-123">5. Merhaba uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9c08a-123">5. Run hello applications</span></span>

1. <span data-ttu-id="9c08a-124">Merhaba sunucu uygulamayı çalıştırın: Node.js komut istemi türünden `node listener.js`.</span><span class="sxs-lookup"><span data-stu-id="9c08a-124">Run hello server application: from a Node.js command prompt type `node listener.js`.</span></span>
2. <span data-ttu-id="9c08a-125">Merhaba istemci uygulaması çalıştırın: Node.js komut istemi türünden `node sender.js`ve bazı metin girin.</span><span class="sxs-lookup"><span data-stu-id="9c08a-125">Run hello client application: from a Node.js command prompt type `node sender.js`, and enter some text.</span></span>
3. <span data-ttu-id="9c08a-126">Merhaba sunucu hello istemci uygulamasında girilen uygulama Konsolu çıkışları hello metin emin olun.</span><span class="sxs-lookup"><span data-stu-id="9c08a-126">Ensure that hello server application console outputs hello text that was entered in hello client application.</span></span>

![running-applications](./media/relay-hybrid-connections-node-get-started/running-applications.png)

<span data-ttu-id="9c08a-128">Tebrikler, Node.js kullanarak uçtan uca bir Karma Bağlantılar uygulaması oluşturdunuz!</span><span class="sxs-lookup"><span data-stu-id="9c08a-128">Congratulations, you have created an end-to-end Hybrid Connections application using Node.js!</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c08a-129">Sonraki adımlar:</span><span class="sxs-lookup"><span data-stu-id="9c08a-129">Next steps:</span></span>

* [<span data-ttu-id="9c08a-130">Geçiş hakkında SSS</span><span class="sxs-lookup"><span data-stu-id="9c08a-130">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="9c08a-131">Ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9c08a-131">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="9c08a-132">.NET kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="9c08a-132">Get started with .NET</span></span>](relay-hybrid-connections-dotnet-get-started.md)
* [<span data-ttu-id="9c08a-133">Node kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="9c08a-133">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

