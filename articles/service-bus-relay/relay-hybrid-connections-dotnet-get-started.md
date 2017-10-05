---
title: ".NET’te Azure Geçiş Karma Bağlantıları ile çalışmaya başlama | Microsoft Docs"
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
ms.openlocfilehash: 1af23bfd46dd7d3781505473f7c1d86e65ea9bc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="90424-103">Geçiş Karma Bağlantıları ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="90424-103">Get started with Relay Hybrid Connections</span></span>
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="90424-104">Bu öğretici [Azure Geçişi Karma Bağlantıları](relay-what-is-it.md#hybrid-connections)’nı tanıtır ve .NET kullanarak, karşılık gelen dinleyici uygulamasına ileti gönderen bir istemci uygulaması oluşturma işlemini gösterir.</span><span class="sxs-lookup"><span data-stu-id="90424-104">This tutorial provides an introduction to [Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how to use .NET to create a client application that sends messages to a corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="90424-105">Ne elde edilecek</span><span class="sxs-lookup"><span data-stu-id="90424-105">What will be accomplished</span></span>
<span data-ttu-id="90424-106">Karma Bağlantılar hem istemci hem de sunucu bileşenini gerektirdiğinden bu öğreticide iki konsol uygulaması oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="90424-106">Because Hybrid Connections requires both a client and a server component, the tutorial creates two console applications.</span></span> <span data-ttu-id="90424-107">Adımlar aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="90424-107">Here are the steps:</span></span>

1. <span data-ttu-id="90424-108">Azure portalı kullanılarak Geçiş ad alanı oluşturma.</span><span class="sxs-lookup"><span data-stu-id="90424-108">Create a Relay namespace, using the Azure portal.</span></span>
2. <span data-ttu-id="90424-109">Azure portalını kullanarak o ad alanında karma bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="90424-109">Create a hybrid connection in that namespace, using the Azure portal.</span></span>
3. <span data-ttu-id="90424-110">İleti almak için bir sunucu (dinleyici) konsol uygulaması yazma.</span><span class="sxs-lookup"><span data-stu-id="90424-110">Write a server (listener) console application to receive messages.</span></span>
4. <span data-ttu-id="90424-111">İleti göndermek için bir istemci (gönderen) konsol uygulaması yazma.</span><span class="sxs-lookup"><span data-stu-id="90424-111">Write a client (sender) console application to send messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90424-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="90424-112">Prerequisites</span></span>

<span data-ttu-id="90424-113">Bu öğreticiyi tamamlamak için aşağıdaki önkoşulları karşılamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="90424-113">To complete this tutorial, you'll need the following prerequisites:</span></span>

1. <span data-ttu-id="90424-114">[Visual Studio 2015 veya üzeri](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="90424-114">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="90424-115">Bu öğreticideki örneklerde Visual Studio 2017 kullanılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="90424-115">The examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="90424-116">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="90424-116">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a><span data-ttu-id="90424-117">1. Azure portalı kullanılarak ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="90424-117">1. Create a namespace using the Azure portal</span></span>
<span data-ttu-id="90424-118">Daha önce oluşturduğunuz bir Geçiş ad alanı varsa [Azure portalını kullanarak karma bağlantı oluşturma](#2-create-a-hybrid-connection-using-the-azure-portal) bölümüne atlayın.</span><span class="sxs-lookup"><span data-stu-id="90424-118">If you have already created a Relay namespace, jump to the [Create a hybrid connection using the Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-the-azure-portal"></a><span data-ttu-id="90424-119">2. Azure portalını kullanarak karma bağlantı oluşturma</span><span class="sxs-lookup"><span data-stu-id="90424-119">2. Create a hybrid connection using the Azure portal</span></span>
<span data-ttu-id="90424-120">Daha önce bir karma bağlantı oluşturduysanız [Sunucu uygulaması oluşturma](#3-create-a-server-application-listener) bölümüne atlayın.</span><span class="sxs-lookup"><span data-stu-id="90424-120">If you have already created a hybrid connection, jump to the [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="90424-121">3. Sunucu uygulaması (dinleyici) oluşturma</span><span class="sxs-lookup"><span data-stu-id="90424-121">3. Create a server application (listener)</span></span>
<span data-ttu-id="90424-122">Geçiş hizmetinden ileti dinleyip almak için Visual Studio kullanılarak bir C# konsol uygulaması yazılacaktır.</span><span class="sxs-lookup"><span data-stu-id="90424-122">To listen and receive messages from the Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="90424-123">4. İstemci uygulaması (gönderici) oluşturma</span><span class="sxs-lookup"><span data-stu-id="90424-123">4. Create a client application (sender)</span></span>
<span data-ttu-id="90424-124">Geçiş’e ileti göndermek için Visual Studio kullanılarak bir C# konsol uygulaması yazılacaktır.</span><span class="sxs-lookup"><span data-stu-id="90424-124">To send messages to the Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-the-applications"></a><span data-ttu-id="90424-125">5. Uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="90424-125">5. Run the applications</span></span>
1. <span data-ttu-id="90424-126">Sunucu uygulamasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="90424-126">Run the server application.</span></span>
2. <span data-ttu-id="90424-127">İstemci uygulamasını çalıştırın ve metin girin.</span><span class="sxs-lookup"><span data-stu-id="90424-127">Run the client application and enter some text.</span></span>
3. <span data-ttu-id="90424-128">Sunucu uygulama konsolunun istemci uygulamasına girilen metni çıkardığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="90424-128">Ensure that the server application console outputs the text that was entered in the client application.</span></span>

![running-applications](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

<span data-ttu-id="90424-130">Tebrikler, uçtan uca Karma Bağlantılar uygulaması oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="90424-130">Congratulations, you have created an end-to-end Hybrid Connections application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90424-131">Sonraki adımlar:</span><span class="sxs-lookup"><span data-stu-id="90424-131">Next steps:</span></span>
* [<span data-ttu-id="90424-132">Geçiş hakkında SSS</span><span class="sxs-lookup"><span data-stu-id="90424-132">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="90424-133">Ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="90424-133">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="90424-134">Node kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="90424-134">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

