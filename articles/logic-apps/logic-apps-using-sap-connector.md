---
title: "aaaConnect tooan şirket içi Azure Logic Apps SAP sisteminde | Microsoft Docs"
description: "Mantıksal uygulama akışınızı hello şirket içi veri ağ geçidi üzerinden tooan şirket içi SAP sistemine bağlanması"
services: logic-apps
author: padmavc
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/01/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 594ec5fed337398bf931d396684630ee9f907d2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-on-premises-sap-system-from-logic-apps-with-hello-sap-connector"></a><span data-ttu-id="c89e5-103">Logic apps hello SAP Bağlayıcısı ile tooan şirket içi SAP sistemine bağlanması</span><span class="sxs-lookup"><span data-stu-id="c89e5-103">Connect tooan on-premises SAP system from logic apps with hello SAP connector</span></span> 

<span data-ttu-id="c89e5-104">Merhaba şirket içi veri ağ geçidi toomanage veri sağlar ve şirket içi kaynaklara güvenle erişin.</span><span class="sxs-lookup"><span data-stu-id="c89e5-104">hello on-premises data gateway enables you toomanage data, and securely access resources that are on-premises.</span></span> <span data-ttu-id="c89e5-105">Bu konu, logic apps tooan şirket içi SAP sistemine nasıl bağlanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="c89e5-105">This topic shows how you can connect logic apps tooan on-premises SAP system.</span></span> <span data-ttu-id="c89e5-106">Bu örnekte, mantıksal uygulamanızı IDOC HTTP istekleri ve hello yanıtı geri gönderir.</span><span class="sxs-lookup"><span data-stu-id="c89e5-106">In this example, your logic app requests an IDOC over HTTP and sends hello response back.</span></span>    

> [!NOTE]
> <span data-ttu-id="c89e5-107">Geçerli sınırlamalar:</span><span class="sxs-lookup"><span data-stu-id="c89e5-107">Current limitations:</span></span> 
> - <span data-ttu-id="c89e5-108">Merhaba yanıt için gereken tüm adımları hello içinde son yok, mantıksal uygulamanızı zaman aşımına [istek zaman aşımı sınırı](./logic-apps-limits-and-config.md).</span><span class="sxs-lookup"><span data-stu-id="c89e5-108">Your logic app times out if all steps required for hello response don't finish within hello [request timeout limit](./logic-apps-limits-and-config.md).</span></span> <span data-ttu-id="c89e5-109">Bu senaryoda, istekleri engellenen.</span><span class="sxs-lookup"><span data-stu-id="c89e5-109">In this scenario, requests might get blocked.</span></span> 
> - <span data-ttu-id="c89e5-110">Merhaba dosya seçiciyi tüm hello kullanılabilir alanlar görüntülenmez.</span><span class="sxs-lookup"><span data-stu-id="c89e5-110">hello file picker does not display all hello available fields.</span></span> <span data-ttu-id="c89e5-111">Bu senaryoda, yollarını el ile ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c89e5-111">In this scenario, you can manually add paths.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c89e5-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c89e5-112">Prerequisites</span></span>

- <span data-ttu-id="c89e5-113">Merhaba son yükleyip [şirket içi veri ağ geçidi](https://www.microsoft.com/download/details.aspx?id=53127) sürüm 1.15.6150.1 ya da daha yeni.</span><span class="sxs-lookup"><span data-stu-id="c89e5-113">Install and configure hello latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127) version 1.15.6150.1 or newer.</span></span> <span data-ttu-id="c89e5-114">[Nasıl tooconnect toohello bir mantıksal uygulama veri ağ geçidi şirket içi](http://aka.ms/logicapps-gateway) hello adımları listeler.</span><span class="sxs-lookup"><span data-stu-id="c89e5-114">[How tooconnect toohello on-premises data gateway in a logic app](http://aka.ms/logicapps-gateway) lists hello steps.</span></span> <span data-ttu-id="c89e5-115">devam etmeden önce bir şirket içi makinede hello ağ geçidi yüklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="c89e5-115">hello gateway must be installed on an on-premises machine before you can proceed.</span></span>

- <span data-ttu-id="c89e5-116">İndirme ve yükleme hello son SAP istemci kitaplığı hello üzerinde aynı hello veri ağ geçidinin yüklü olduğu makine.</span><span class="sxs-lookup"><span data-stu-id="c89e5-116">Download and install hello latest SAP client library on hello same machine where you installed hello data gateway.</span></span> <span data-ttu-id="c89e5-117">SAP sürümleri aşağıdaki hello birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="c89e5-117">Use any of hello following SAP versions:</span></span> 
    - <span data-ttu-id="c89e5-118">SAP sunucusuna</span><span class="sxs-lookup"><span data-stu-id="c89e5-118">SAP Server</span></span>
        - <span data-ttu-id="c89e5-119">Herhangi bir SAP sunucusuna bu destek hello .NET Connector (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="c89e5-119">Any SAP Server that support hello .NET Connector (NCo) 3.0</span></span>
 
    - <span data-ttu-id="c89e5-120">SAP istemci</span><span class="sxs-lookup"><span data-stu-id="c89e5-120">SAP Client</span></span>
        - <span data-ttu-id="c89e5-121">SAP .NET bağlayıcı (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="c89e5-121">SAP .NET Connector (NCo) 3.0</span></span>

## <a name="add-triggers-and-actions-for-connecting-tooyour-sap-system"></a><span data-ttu-id="c89e5-122">Tetikleyiciler ve Eylemler tooyour SAP sistemine bağlanmak için ekleme</span><span class="sxs-lookup"><span data-stu-id="c89e5-122">Add triggers and actions for connecting tooyour SAP system</span></span>

<span data-ttu-id="c89e5-123">Merhaba SAP bağlayıcısı Eylemler ancak değil Tetikleyicileri vardır.</span><span class="sxs-lookup"><span data-stu-id="c89e5-123">hello SAP connector has actions, but not triggers.</span></span> <span data-ttu-id="c89e5-124">Bu nedenle, hello hello iş akışının başlangıcında başka bir tetikleyici toouse sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="c89e5-124">So, we have toouse another trigger at hello start of hello workflow.</span></span> 

1. <span data-ttu-id="c89e5-125">Merhaba istek/yanıt tetikleyicisi ekleyin ve ardından **yeni adım**.</span><span class="sxs-lookup"><span data-stu-id="c89e5-125">Add hello Request/Response trigger, and then select **New step**.</span></span>

2. <span data-ttu-id="c89e5-126">Seçin **Eylem Ekle**seçip hello SAP bağlayıcısı yazarak `SAP` hello arama alanında:</span><span class="sxs-lookup"><span data-stu-id="c89e5-126">Select **Add an action**, and then select hello SAP connector by typing `SAP` in hello search field:</span></span>    

     ![SAP uygulama sunucusu ya da SAP ileti sunucusu seçin](media/logic-apps-using-sap-connector/sap-action.png)

3. <span data-ttu-id="c89e5-128">Seçin [ **SAP uygulama sunucusu** ](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) veya [ **SAP ileti sunucusu**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), SAP kurulumunuzu göre.</span><span class="sxs-lookup"><span data-stu-id="c89e5-128">Select [**SAP Application Server**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) or [**SAP Message Server**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), based on your SAP setup.</span></span> <span data-ttu-id="c89e5-129">Varolan bir bağlantıyı yoksa, istendiğinde toocreate biri demektir.</span><span class="sxs-lookup"><span data-stu-id="c89e5-129">If you don't have an existing connection, you are prompted toocreate one.</span></span>

   1. <span data-ttu-id="c89e5-130">Seçin **Connect şirket içi veri ağ geçidi üzerinden**ve SAP sisteminizi hello ayrıntılarını girin:</span><span class="sxs-lookup"><span data-stu-id="c89e5-130">Select **Connect via on-premises data gateway**, and enter hello details for your SAP system:</span></span>   

       ![Bağlantı dizesi tooSAP Ekle](media/logic-apps-using-sap-connector/picture2.png)  

   2. <span data-ttu-id="c89e5-132">Altında **ağ geçidi**, bir var olan ağ geçidi ya da tooinstall yeni bir ağ geçidi seçin, **ağ geçidi yükleme**.</span><span class="sxs-lookup"><span data-stu-id="c89e5-132">Under **Gateway**, select an existing gateway, or tooinstall a new gateway, select **Install Gateway**.</span></span>

        ![Yeni bir ağ geçidi yükleyin](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. <span data-ttu-id="c89e5-134">Tüm hello ayrıntıları girdikten sonra Seç **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="c89e5-134">After you enter all hello details, select **Create**.</span></span> 
   <span data-ttu-id="c89e5-135">Logic Apps yapılandırır ve hello bağlantı düzgün çalıştığından emin olmayı hello bağlantısını test eder.</span><span class="sxs-lookup"><span data-stu-id="c89e5-135">Logic Apps configures and tests hello connection, making sure that hello connection works properly.</span></span>

4. <span data-ttu-id="c89e5-136">SAP bağlantınız için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="c89e5-136">Enter a name for your SAP connection.</span></span>

5. <span data-ttu-id="c89e5-137">Merhaba farklı SAP seçenekleri şimdi kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c89e5-137">hello different SAP options are now available.</span></span> <span data-ttu-id="c89e5-138">toofind, IDOC kategorisi, hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="c89e5-138">toofind your IDOC category, select from hello list.</span></span> <span data-ttu-id="c89e5-139">Merhaba yolu ve select hello HTTP yanıt hello olarak el ile yazın veya **gövde** alan:</span><span class="sxs-lookup"><span data-stu-id="c89e5-139">Or manually type in hello path, and select hello HTTP response in hello **body** field:</span></span>

     ![SAP eylemi](media/logic-apps-using-sap-connector/picture3.png)

6. <span data-ttu-id="c89e5-141">Merhaba eylem oluşturmak için Ekle bir **HTTP yanıtı**.</span><span class="sxs-lookup"><span data-stu-id="c89e5-141">Add hello action for creating an **HTTP Response**.</span></span> <span data-ttu-id="c89e5-142">Merhaba yanıt iletisi hello SAP çıktısını olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c89e5-142">hello response message should be from hello SAP output.</span></span>

7. <span data-ttu-id="c89e5-143">Mantıksal uygulamanızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c89e5-143">Save your logic app.</span></span> <span data-ttu-id="c89e5-144">IDOC hello HTTP tetikleme URL'si aracılığıyla göndererek test.</span><span class="sxs-lookup"><span data-stu-id="c89e5-144">Test it by sending an IDOC through hello HTTP trigger URL.</span></span> <span data-ttu-id="c89e5-145">IDOC gönderilen hello sonra hello mantıksal uygulama hello yanıttan bekleyin:</span><span class="sxs-lookup"><span data-stu-id="c89e5-145">After hello IDOC is sent, wait for hello response from hello logic app:</span></span>   

     > [!TIP]
     > <span data-ttu-id="c89e5-146">Nasıl çok denetleyin[mantıksal uygulamalarınızı izleme](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="c89e5-146">Check out how too[monitor your Logic Apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="c89e5-147">Merhaba SAP bağlayıcısı tooyour mantıksal uygulama eklenir, diğer işlevleri keşfetmeye başlayın:</span><span class="sxs-lookup"><span data-stu-id="c89e5-147">Now that hello SAP connector is added tooyour logic app, start exploring other functionalities:</span></span>

- <span data-ttu-id="c89e5-148">BAPI</span><span class="sxs-lookup"><span data-stu-id="c89e5-148">BAPI</span></span>
- <span data-ttu-id="c89e5-149">RFC</span><span class="sxs-lookup"><span data-stu-id="c89e5-149">RFC</span></span>

## <a name="get-help"></a><span data-ttu-id="c89e5-150">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="c89e5-150">Get help</span></span>

<span data-ttu-id="c89e5-151">tooask sorular soruları ve hangi diğer Azure mantığı kullanıcılar gittiğini, uygulamaların ziyaret hello öğrenin [Azure Logic Apps Forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="c89e5-151">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="c89e5-152">toohelp Azure mantıksal uygulamaları ve bağlayıcıların geliştirmek, oy veya hello fikir gönderme [Azure Logic Apps kullanıcı geri bildirim sitesi](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="c89e5-152">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c89e5-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c89e5-153">Next steps</span></span>

- <span data-ttu-id="c89e5-154">Bilgi nasıl toovalidate, dönüştürme ve diğer BizTalk benzeri işlevleri hello [Kurumsal tümleştirme paketi](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c89e5-154">Learn how toovalidate, transform, and other BizTalk-like functions in hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span> 
- <span data-ttu-id="c89e5-155">[Tooon içi veri bağlanmak](../logic-apps/logic-apps-gateway-connection.md) mantığı uygulamalardan</span><span class="sxs-lookup"><span data-stu-id="c89e5-155">[Connect tooon-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
