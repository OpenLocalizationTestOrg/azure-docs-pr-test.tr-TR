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
# <a name="connect-tooan-ibm-mq-server-from-logic-apps-using-hello-mq-connector"></a><span data-ttu-id="42f62-103">Merhaba MQ Bağlayıcısı'nı kullanarak mantığı uygulamalardan tooan IBM MQ server Bağlan</span><span class="sxs-lookup"><span data-stu-id="42f62-103">Connect tooan IBM MQ server from logic apps using hello MQ connector</span></span> 

<span data-ttu-id="42f62-104">MQ için Microsoft Connector gönderir ve MQ Server şirket içi veya Azure depolanan iletilerini alır.</span><span class="sxs-lookup"><span data-stu-id="42f62-104">Microsoft Connector for MQ sends and retrieves messages stored in an MQ Server on-premises, or in Azure.</span></span> <span data-ttu-id="42f62-105">Bu bağlayıcı bir TCP/IP ağı üzerinden bir uzak IBM MQ sunucuyla iletişim kuran bir Microsoft MQ istemcisi içerir.</span><span class="sxs-lookup"><span data-stu-id="42f62-105">This connector includes a Microsoft MQ client that communicates with a remote IBM MQ server across a TCP/IP network.</span></span> <span data-ttu-id="42f62-106">Bu belgede bir başlangıç kılavuzu toouse hello MQ Bağlayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="42f62-106">This document is a starter guide toouse hello MQ connector.</span></span> <span data-ttu-id="42f62-107">Tek bir ileti üzerinde bir sıra göz atarak başlayın ve ardından çalışırken hello diğer eylemler önerilir.</span><span class="sxs-lookup"><span data-stu-id="42f62-107">We recommended you begin by browsing a single message on a queue, and then trying hello other actions.</span></span>    

<span data-ttu-id="42f62-108">Merhaba MQ bağlayıcı eylemleri aşağıdaki hello içerir.</span><span class="sxs-lookup"><span data-stu-id="42f62-108">hello MQ connector includes hello following actions.</span></span> <span data-ttu-id="42f62-109">Hiçbir Tetikleyicileri vardır.</span><span class="sxs-lookup"><span data-stu-id="42f62-109">There are no triggers.</span></span>

-   <span data-ttu-id="42f62-110">IBM MQ Server hello selamlama iletisine silmeden tek İletiye Gözat</span><span class="sxs-lookup"><span data-stu-id="42f62-110">Browse a single message without deleting hello message from hello IBM MQ Server</span></span>
-   <span data-ttu-id="42f62-111">IBM MQ Server hello Merhaba iletileri silmeden toplu iletiler Gözat</span><span class="sxs-lookup"><span data-stu-id="42f62-111">Browse a batch of messages without deleting hello messages from hello IBM MQ Server</span></span>
-   <span data-ttu-id="42f62-112">Tek bir ileti alırsınız ve hello message IBM MQ Server hello silin</span><span class="sxs-lookup"><span data-stu-id="42f62-112">Receive a single message and delete hello message from hello IBM MQ Server</span></span>
-   <span data-ttu-id="42f62-113">Toplu iletiler almak ve IBM MQ Server hello Merhaba iletileri sil</span><span class="sxs-lookup"><span data-stu-id="42f62-113">Receive a batch of messages and delete hello messages from hello IBM MQ Server</span></span>
-   <span data-ttu-id="42f62-114">Tek ileti toohello IBM MQ Server Gönder</span><span class="sxs-lookup"><span data-stu-id="42f62-114">Send a single message toohello IBM MQ Server</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="42f62-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="42f62-115">Prerequisites</span></span>

* <span data-ttu-id="42f62-116">Bir şirket içi MQ server kullanıyorsanız [hello şirket içi veri ağ geçidi yükleme](../logic-apps/logic-apps-gateway-install.md) ağınızdaki bir sunucuda.</span><span class="sxs-lookup"><span data-stu-id="42f62-116">If using an on-premises MQ server, [install hello on-premises data gateway](../logic-apps/logic-apps-gateway-install.md) on a server within your network.</span></span> <span data-ttu-id="42f62-117">Merhaba MQ Server genel olarak kullanılabilir veya Azure içinde kullanılabilir değilse, ardından hello veri ağ geçidi kullanılan gerekli veya değil.</span><span class="sxs-lookup"><span data-stu-id="42f62-117">If hello MQ Server is publicly available, or available within Azure, then hello data gateway is not used or required.</span></span>

    > [!NOTE]
    > <span data-ttu-id="42f62-118">Merhaba sunucu şirket içi veri ağ geçidinin yüklü hello gerekir de sahip olduğu .net Framework 4.6 hello MQ bağlayıcı toofunction için yüklü.</span><span class="sxs-lookup"><span data-stu-id="42f62-118">hello server where hello On-Premises Data Gateway is installed must also have .Net Framework 4.6 installed for hello MQ Connector toofunction.</span></span>

* <span data-ttu-id="42f62-119">Merhaba hello şirket içi veri ağ geçidi için-Azure kaynağını oluşturma [hello veri ağ geçidi bağlantısı kurma](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="42f62-119">Create hello Azure resource for hello on-premises data gateway - [Set up hello data gateway connection](../logic-apps/logic-apps-gateway-connection.md).</span></span>

* <span data-ttu-id="42f62-120">Resmi olarak IBM WebSphere MQ sürümleri desteklenir:</span><span class="sxs-lookup"><span data-stu-id="42f62-120">Officially supported IBM WebSphere MQ versions:</span></span>
   * <span data-ttu-id="42f62-121">MQ 7.5</span><span class="sxs-lookup"><span data-stu-id="42f62-121">MQ 7.5</span></span>
   * <span data-ttu-id="42f62-122">MQ 8.0</span><span class="sxs-lookup"><span data-stu-id="42f62-122">MQ 8.0</span></span>

## <a name="create-a-logic-app"></a><span data-ttu-id="42f62-123">Mantıksal uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="42f62-123">Create a logic app</span></span>

1. <span data-ttu-id="42f62-124">Merhaba, **Azure başlangıç Panosu**seçin  **+**  (artı işareti) **Web + mobil**ve ardından **mantıksal uygulama**.</span><span class="sxs-lookup"><span data-stu-id="42f62-124">In hello **Azure start board**, select **+** (plus sign), **Web + Mobile**, and then **Logic App**.</span></span> 
2. <span data-ttu-id="42f62-125">Merhaba girin **adı**, MQTestApp gibi **abonelik**, **kaynak grubu**, ve **konumu** (Merhaba konumu hello kullanın Şirket içi veri ağ geçidi bağlantı yapılandırılır).</span><span class="sxs-lookup"><span data-stu-id="42f62-125">Enter hello **Name**, such as MQTestApp, **Subscription**, **Resource group**, and **Location** (use hello location where hello on-premises Data Gateway connection is configured).</span></span> <span data-ttu-id="42f62-126">Seçin **PIN toodashboard**seçip **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="42f62-126">Select **Pin toodashboard**, and select **Create**.</span></span>  
<span data-ttu-id="42f62-127">![Mantıksal uygulama oluşturma](media/connectors-create-api-mq/Create_Logic_App.png)</span><span class="sxs-lookup"><span data-stu-id="42f62-127">![Create Logic App](media/connectors-create-api-mq/Create_Logic_App.png)</span></span>

## <a name="add-a-trigger"></a><span data-ttu-id="42f62-128">Bir tetikleyici Ekle</span><span class="sxs-lookup"><span data-stu-id="42f62-128">Add a trigger</span></span>

> [!NOTE]
> <span data-ttu-id="42f62-129">Merhaba MQ bağlayıcı hiçbir tetikleyici yok.</span><span class="sxs-lookup"><span data-stu-id="42f62-129">hello MQ Connector does not have any triggers.</span></span> <span data-ttu-id="42f62-130">Bu nedenle, başka bir tetikleyici toostart hello gibi mantıksal uygulamanızı kullanmak **yineleme** tetikleyici.</span><span class="sxs-lookup"><span data-stu-id="42f62-130">So, use another trigger toostart your logic app, such as hello **Recurrence** trigger.</span></span> 

1. <span data-ttu-id="42f62-131">Merhaba **Logic Apps Tasarımcısı** açar, select **yineleme** ortak Tetikleyicileri hello listesinde.</span><span class="sxs-lookup"><span data-stu-id="42f62-131">hello **Logic Apps Designer** opens, select **Recurrence** in hello list of common triggers.</span></span>
2. <span data-ttu-id="42f62-132">Seçin **Düzenle** hello yinelenme tetikleyici içinde.</span><span class="sxs-lookup"><span data-stu-id="42f62-132">Select **Edit** within hello Recurrence Trigger.</span></span> 
3. <span data-ttu-id="42f62-133">Set hello **sıklığı** çok**gün**ve kümesi hello **aralığı** çok**7**.</span><span class="sxs-lookup"><span data-stu-id="42f62-133">Set hello **Frequency** too**Day**, and set hello **Interval** too**7**.</span></span> 

## <a name="browse-a-single-message"></a><span data-ttu-id="42f62-134">Tek bir iletiye Gözat</span><span class="sxs-lookup"><span data-stu-id="42f62-134">Browse a single message</span></span>
1. <span data-ttu-id="42f62-135">Seçin **+ yeni adım**seçip **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="42f62-135">Select **+ New step**, and select **Add an action**.</span></span>
2. <span data-ttu-id="42f62-136">Merhaba arama kutusuna yazın `mq`ve ardından **MQ - Gözat ileti**.</span><span class="sxs-lookup"><span data-stu-id="42f62-136">In hello search box, type `mq`, and then select **MQ - Browse message**.</span></span>  
<span data-ttu-id="42f62-137">![İleti Gözat](media/connectors-create-api-mq/Browse_message.png)</span><span class="sxs-lookup"><span data-stu-id="42f62-137">![Browse message](media/connectors-create-api-mq/Browse_message.png)</span></span>

3. <span data-ttu-id="42f62-138">Varolan MQ bağlantısı yoksa hello bağlantısı oluştur:</span><span class="sxs-lookup"><span data-stu-id="42f62-138">If there isn't an existing MQ connection, then create hello connection:</span></span>  

    1. <span data-ttu-id="42f62-139">Seçin **Connect şirket içi veri ağ geçidi üzerinden**ve MQ sunucunuzun hello özelliklerini girin.</span><span class="sxs-lookup"><span data-stu-id="42f62-139">Select **Connect via on-premises data gateway**, and enter hello properties of your MQ server.</span></span>  
    <span data-ttu-id="42f62-140">İçin **Server**, hello MQ sunucu adı girin veya izleyen iki nokta üst üste ve başlangıç bağlantı noktası numarası ile başlangıç IP adresi girin.</span><span class="sxs-lookup"><span data-stu-id="42f62-140">For **Server**, you can enter hello MQ server name, or enter hello IP address followed by a colon and hello port number.</span></span> 
    2. <span data-ttu-id="42f62-141">Merhaba **ağ geçidi** açılır yapılandırılmış var olan tüm ağ geçidi bağlantıları listeler.</span><span class="sxs-lookup"><span data-stu-id="42f62-141">hello **gateway** dropdown lists any existing gateway connections that have been configured.</span></span> <span data-ttu-id="42f62-142">Ağ geçidi seçin.</span><span class="sxs-lookup"><span data-stu-id="42f62-142">Select your gateway.</span></span>
    3. <span data-ttu-id="42f62-143">Seçin **oluşturma** bitirdikten sonra.</span><span class="sxs-lookup"><span data-stu-id="42f62-143">Select **Create** when finished.</span></span> <span data-ttu-id="42f62-144">Bağlantınızı benzer toohello aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="42f62-144">Your connection looks similar toohello following:</span></span>   
    <span data-ttu-id="42f62-145">![Bağlantı özellikleri](media/connectors-create-api-mq/Connection_Properties.png)</span><span class="sxs-lookup"><span data-stu-id="42f62-145">![Connection Properties](media/connectors-create-api-mq/Connection_Properties.png)</span></span>

4. <span data-ttu-id="42f62-146">Merhaba eylem Özellikleri'nde, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="42f62-146">In hello action properties, you can:</span></span>  

    * <span data-ttu-id="42f62-147">Kullanım hello **sıra** özelliği tooaccess hello bağlantısı içinde tanımlanan daha farklı kuyruk adı</span><span class="sxs-lookup"><span data-stu-id="42f62-147">Use hello **Queue** property tooaccess a different queue name than what is defined in hello connection</span></span>
    * <span data-ttu-id="42f62-148">Kullanım hello **MessageID**, **correlationıd değeri**, **GroupID**ve diğer özellikleri toobrowse hello farklı MQ ileti özelliğe göre bir ileti için</span><span class="sxs-lookup"><span data-stu-id="42f62-148">Use hello **MessageId**, **CorrelationId**, **GroupId**, and other properties toobrowse for a message based on hello different MQ message properties</span></span>
    * <span data-ttu-id="42f62-149">Ayarlama **IncludeInfo** çok**True** tooinclude ek ileti bilgi hello çıkışı.</span><span class="sxs-lookup"><span data-stu-id="42f62-149">Set **IncludeInfo** too**True** tooinclude additional message information in hello output.</span></span> <span data-ttu-id="42f62-150">Ya da çok ayarlayın**False** toonot hello çıktısında ek ileti bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="42f62-150">Or, set it too**False** toonot include additional message information in hello output.</span></span>
    * <span data-ttu-id="42f62-151">Girin bir **zaman aşımı** değeri toodetermine ileti tooarrive boş bir sorgudaki için ne kadar süreyle toowait.</span><span class="sxs-lookup"><span data-stu-id="42f62-151">Enter a **Timeout** value toodetermine how long toowait for a message tooarrive in an empty queue.</span></span> <span data-ttu-id="42f62-152">Hiçbir şey girilirse, hello sıradaki ilk iletiyi hello alınır ve ileti tooappear için beklerken geçen hiçbir zaman yok.</span><span class="sxs-lookup"><span data-stu-id="42f62-152">If nothing is entered, hello first message in hello queue is retrieved, and there is no time spent waiting for a message tooappear.</span></span>  
    <span data-ttu-id="42f62-153">![İleti özelliklerini göz atın](media/connectors-create-api-mq/Browse_message_Props.png)</span><span class="sxs-lookup"><span data-stu-id="42f62-153">![Browse Message Properties](media/connectors-create-api-mq/Browse_message_Props.png)</span></span>

5. <span data-ttu-id="42f62-154">**Kaydet** yaptığınız değişiklikleri ve ardından **çalıştırmak** mantıksal uygulamanızı:</span><span class="sxs-lookup"><span data-stu-id="42f62-154">**Save** your changes, and then **Run** your logic app:</span></span>  
<span data-ttu-id="42f62-155">![Kaydet ve Çalıştır](media/connectors-create-api-mq/Save_Run.png)</span><span class="sxs-lookup"><span data-stu-id="42f62-155">![Save and run](media/connectors-create-api-mq/Save_Run.png)</span></span>

6. <span data-ttu-id="42f62-156">Birkaç saniye sonra çalıştırmak hello hello adımları gösterilir ve hello çıkışına arayabilir.</span><span class="sxs-lookup"><span data-stu-id="42f62-156">After a few seconds, hello steps of hello run are shown, and you can look at hello output.</span></span> <span data-ttu-id="42f62-157">Her bir adımın Hello yeşil onay işareti toosee Ayrıntılar'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="42f62-157">Select hello green checkmark toosee details of each step.</span></span> <span data-ttu-id="42f62-158">Seçin **bkz ham çıkışları** hello hakkında daha fazla ayrıntı toosee çıkış verileri.</span><span class="sxs-lookup"><span data-stu-id="42f62-158">Select **See raw outputs** toosee additional details on hello output data.</span></span>  
<span data-ttu-id="42f62-159">![İleti çıkış Gözat](media/connectors-create-api-mq/Browse_message_output.png)</span><span class="sxs-lookup"><span data-stu-id="42f62-159">![Browse message output](media/connectors-create-api-mq/Browse_message_output.png)</span></span>  

    <span data-ttu-id="42f62-160">Ham çıktı:</span><span class="sxs-lookup"><span data-stu-id="42f62-160">Raw output:</span></span>  
    ![İleti ham çıkış Gözat](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. <span data-ttu-id="42f62-162">Ne zaman hello **IncludeInfo** seçeneği tootrue ayarlanmışsa, çıktı aşağıdaki hello görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="42f62-162">When hello **IncludeInfo** option is set tootrue, hello following output is displayed:</span></span>  
<span data-ttu-id="42f62-163">![Gözat iletiyi bilgisi Ekle](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span><span class="sxs-lookup"><span data-stu-id="42f62-163">![Browse message include info](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span></span>

## <a name="browse-multiple-messages"></a><span data-ttu-id="42f62-164">Birden çok ileti Gözat</span><span class="sxs-lookup"><span data-stu-id="42f62-164">Browse multiple messages</span></span>
<span data-ttu-id="42f62-165">Merhaba **Gözat iletileri** eylemi içeren bir **BatchSize** seçeneği tooindicate kaç iletileri döndürülüp döndürülmediğini hello sıradan.</span><span class="sxs-lookup"><span data-stu-id="42f62-165">hello **Browse messages** action includes a **BatchSize** option tooindicate how many messages should be returned from hello queue.</span></span>  <span data-ttu-id="42f62-166">Varsa **BatchSize** giriş yok, tüm iletileri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="42f62-166">If **BatchSize** has no entry, all messages are returned.</span></span> <span data-ttu-id="42f62-167">Merhaba çıktı iletileri dizisi döndürülür.</span><span class="sxs-lookup"><span data-stu-id="42f62-167">hello returned output is an array of messages.</span></span>

1. <span data-ttu-id="42f62-168">Merhaba eklerken **Gözat iletileri** eylem, yapılandırılmış hello ilk bağlantı, varsayılan olarak seçilidir.</span><span class="sxs-lookup"><span data-stu-id="42f62-168">When adding hello **Browse messages** action, hello first connection that is configured is selected by default.</span></span> <span data-ttu-id="42f62-169">Seçin **değiştirmek bağlantı** toocreate yeni bir bağlantı veya farklı bir bağlantı seçin.</span><span class="sxs-lookup"><span data-stu-id="42f62-169">Select **Change connection** toocreate a new connection, or select a different connection.</span></span>

2. <span data-ttu-id="42f62-170">Gözat Hello çıktısını gösterir iletileri:</span><span class="sxs-lookup"><span data-stu-id="42f62-170">hello output of Browse messages shows:</span></span>  
![İletileri çıkış Gözat](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a><span data-ttu-id="42f62-172">Tek bir ileti alırsınız</span><span class="sxs-lookup"><span data-stu-id="42f62-172">Receive a single message</span></span>
<span data-ttu-id="42f62-173">Merhaba **alma iletisi** eylem sahip hello aynı girişleri ve çıkışları hello **Gözat ileti** eylem.</span><span class="sxs-lookup"><span data-stu-id="42f62-173">hello **Receive message** action has hello same inputs and outputs as hello **Browse message** action.</span></span> <span data-ttu-id="42f62-174">Kullanırken **alma iletisi**, selamlama iletisine hello sıradan silinir.</span><span class="sxs-lookup"><span data-stu-id="42f62-174">When using **Receive message**, hello message is deleted from hello queue.</span></span>

## <a name="receive-multiple-messages"></a><span data-ttu-id="42f62-175">Birden çok ileti alma</span><span class="sxs-lookup"><span data-stu-id="42f62-175">Receive multiple messages</span></span>
<span data-ttu-id="42f62-176">Merhaba **alma iletileri** eylem sahip hello aynı girişleri ve çıkışları hello **Gözat iletileri** eylem.</span><span class="sxs-lookup"><span data-stu-id="42f62-176">hello **Receive messages** action has hello same inputs and outputs as hello **Browse messages** action.</span></span> <span data-ttu-id="42f62-177">Kullanırken **alma iletileri**, karışılama iletileri hello sıradan silinir.</span><span class="sxs-lookup"><span data-stu-id="42f62-177">When using **Receive messages**, hello messages are deleted from hello queue.</span></span>

<span data-ttu-id="42f62-178">Varsa hiçbir ileti hello sırada bir Gözat veya alma işlemi yaparken, hello adım çıkış aşağıdaki hello ile başarısız olur:</span><span class="sxs-lookup"><span data-stu-id="42f62-178">If there are no messages in hello queue when doing a browse or a receive, hello step fails with hello following output:</span></span>  
![MQ yok, hata iletisi](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a><span data-ttu-id="42f62-180">İleti gönderme</span><span class="sxs-lookup"><span data-stu-id="42f62-180">Send a message</span></span>
1. <span data-ttu-id="42f62-181">Merhaba eklerken **ileti gönder** eylem, yapılandırılmış hello ilk bağlantı, varsayılan olarak seçilidir.</span><span class="sxs-lookup"><span data-stu-id="42f62-181">When adding hello **Send message** action, hello first connection that is configured is selected by default.</span></span> <span data-ttu-id="42f62-182">Seçin **değiştirmek bağlantı** toocreate yeni bir bağlantı veya farklı bir bağlantı seçin.</span><span class="sxs-lookup"><span data-stu-id="42f62-182">Select **Change connection** toocreate a new connection, or select a different connection.</span></span> <span data-ttu-id="42f62-183">Merhaba geçerli **ileti türleri** olan **veri birimi**, **yanıt**, veya **isteği**.</span><span class="sxs-lookup"><span data-stu-id="42f62-183">hello valid **Message Types** are **Datagram**, **Reply**, or **Request**.</span></span>  
<span data-ttu-id="42f62-184">![Msg özellik Gönder](media/connectors-create-api-mq/Send_Msg_Props.png)</span><span class="sxs-lookup"><span data-stu-id="42f62-184">![Send Msg Props](media/connectors-create-api-mq/Send_Msg_Props.png)</span></span>

2. <span data-ttu-id="42f62-185">Merhaba ileti gönder çıktısını hello aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="42f62-185">hello output of Send message looks like hello following:</span></span>  
![Msg çıkış Gönder](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a><span data-ttu-id="42f62-187">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="42f62-187">Connector-specific details</span></span>

<span data-ttu-id="42f62-188">Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/mq/).</span><span class="sxs-lookup"><span data-stu-id="42f62-188">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/mq/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="42f62-189">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="42f62-189">Next steps</span></span>
<span data-ttu-id="42f62-190">[Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="42f62-190">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="42f62-191">Araştır Logic Apps içinde kullanılabilir diğer bağlayıcıları hello bizim [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="42f62-191">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
