---
title: "Azure mantıksal uygulamaları bir şirket içi SAP sisteme bağlanma | Microsoft Docs"
description: "Bir şirket içi SAP sisteme mantığı uygulama akışınızı şirket içi veri ağ geçidi üzerinden bağlanması"
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
ms.openlocfilehash: 3fea93f558d5a4ef62550fd1f6486903cb812930
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-to-an-on-premises-sap-system-from-logic-apps-with-the-sap-connector"></a><span data-ttu-id="fe4af-103">Logic apps SAP Bağlayıcısı ile bir şirket içi SAP sistemine bağlanması</span><span class="sxs-lookup"><span data-stu-id="fe4af-103">Connect to an on-premises SAP system from logic apps with the SAP connector</span></span> 

<span data-ttu-id="fe4af-104">Şirket içi veri ağ geçidi verilerini yönetmek ve şirket kaynaklarına güvenle erişmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="fe4af-104">The on-premises data gateway enables you to manage data, and securely access resources that are on-premises.</span></span> <span data-ttu-id="fe4af-105">Bu konu, bir şirket içi SAP sisteme logic apps nasıl bağlanabilirsiniz gösterir.</span><span class="sxs-lookup"><span data-stu-id="fe4af-105">This topic shows how you can connect logic apps to an on-premises SAP system.</span></span> <span data-ttu-id="fe4af-106">Bu örnekte, mantıksal uygulamanızı IDOC HTTP istekleri ve yanıtı geri gönderir.</span><span class="sxs-lookup"><span data-stu-id="fe4af-106">In this example, your logic app requests an IDOC over HTTP and sends the response back.</span></span>    

> [!NOTE]
> <span data-ttu-id="fe4af-107">Geçerli sınırlamalar:</span><span class="sxs-lookup"><span data-stu-id="fe4af-107">Current limitations:</span></span> 
> - <span data-ttu-id="fe4af-108">Yanıt için gereken tüm adımları içinde son yok, mantıksal uygulamanızı zaman aşımına [istek zaman aşımı sınırı](./logic-apps-limits-and-config.md).</span><span class="sxs-lookup"><span data-stu-id="fe4af-108">Your logic app times out if all steps required for the response don't finish within the [request timeout limit](./logic-apps-limits-and-config.md).</span></span> <span data-ttu-id="fe4af-109">Bu senaryoda, istekleri engellenen.</span><span class="sxs-lookup"><span data-stu-id="fe4af-109">In this scenario, requests might get blocked.</span></span> 
> - <span data-ttu-id="fe4af-110">Dosya seçiciyi kullanılabilir tüm alanlar görüntülenmez.</span><span class="sxs-lookup"><span data-stu-id="fe4af-110">The file picker does not display all the available fields.</span></span> <span data-ttu-id="fe4af-111">Bu senaryoda, yollarını el ile ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe4af-111">In this scenario, you can manually add paths.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe4af-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fe4af-112">Prerequisites</span></span>

- <span data-ttu-id="fe4af-113">Yükleme ve yapılandırma en son [şirket içi veri ağ geçidi](https://www.microsoft.com/download/details.aspx?id=53127) sürüm 1.15.6150.1 ya da daha yeni.</span><span class="sxs-lookup"><span data-stu-id="fe4af-113">Install and configure the latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127) version 1.15.6150.1 or newer.</span></span> <span data-ttu-id="fe4af-114">[Bir mantıksal uygulama şirket içi veri ağ geçidi bağlanma](http://aka.ms/logicapps-gateway) adımlar listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="fe4af-114">[How to connect to the on-premises data gateway in a logic app](http://aka.ms/logicapps-gateway) lists the steps.</span></span> <span data-ttu-id="fe4af-115">Devam etmeden önce ağ geçidini bir şirket içi makineye yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe4af-115">The gateway must be installed on an on-premises machine before you can proceed.</span></span>

- <span data-ttu-id="fe4af-116">Karşıdan yükle ve veri ağ geçidinin yüklü olduğu makinede en son SAP istemci Kitaplığı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="fe4af-116">Download and install the latest SAP client library on the same machine where you installed the data gateway.</span></span> <span data-ttu-id="fe4af-117">SAP sürümlerinden birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="fe4af-117">Use any of the following SAP versions:</span></span> 
    - <span data-ttu-id="fe4af-118">SAP sunucusuna</span><span class="sxs-lookup"><span data-stu-id="fe4af-118">SAP Server</span></span>
        - <span data-ttu-id="fe4af-119">SAP sunucuların (NCo) 3.0 .NET bağlayıcı desteği</span><span class="sxs-lookup"><span data-stu-id="fe4af-119">Any SAP Server that support the .NET Connector (NCo) 3.0</span></span>
 
    - <span data-ttu-id="fe4af-120">SAP istemci</span><span class="sxs-lookup"><span data-stu-id="fe4af-120">SAP Client</span></span>
        - <span data-ttu-id="fe4af-121">SAP .NET bağlayıcı (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="fe4af-121">SAP .NET Connector (NCo) 3.0</span></span>

## <a name="add-triggers-and-actions-for-connecting-to-your-sap-system"></a><span data-ttu-id="fe4af-122">Tetikleyiciler ve Eylemler SAP sisteminize bağlamak için ekleme</span><span class="sxs-lookup"><span data-stu-id="fe4af-122">Add triggers and actions for connecting to your SAP system</span></span>

<span data-ttu-id="fe4af-123">SAP bağlayıcısı Eylemler ancak değil Tetikleyicileri vardır.</span><span class="sxs-lookup"><span data-stu-id="fe4af-123">The SAP connector has actions, but not triggers.</span></span> <span data-ttu-id="fe4af-124">Bu nedenle, biz iş akışının başlangıcında başka bir tetikleyici kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe4af-124">So, we have to use another trigger at the start of the workflow.</span></span> 

1. <span data-ttu-id="fe4af-125">İstek/yanıt tetikleyicisi ekleyin ve ardından **yeni adım**.</span><span class="sxs-lookup"><span data-stu-id="fe4af-125">Add the Request/Response trigger, and then select **New step**.</span></span>

2. <span data-ttu-id="fe4af-126">Seçin **Eylem Ekle**seçip SAP Bağlayıcısı'nı yazarak `SAP` arama alanında:</span><span class="sxs-lookup"><span data-stu-id="fe4af-126">Select **Add an action**, and then select the SAP connector by typing `SAP` in the search field:</span></span>    

     ![SAP uygulama sunucusu ya da SAP ileti sunucusu seçin](media/logic-apps-using-sap-connector/sap-action.png)

3. <span data-ttu-id="fe4af-128">Seçin [ **SAP uygulama sunucusu** ](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) veya [ **SAP ileti sunucusu**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), SAP kurulumunuzu göre.</span><span class="sxs-lookup"><span data-stu-id="fe4af-128">Select [**SAP Application Server**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) or [**SAP Message Server**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), based on your SAP setup.</span></span> <span data-ttu-id="fe4af-129">Varolan bir bağlantıyı sahip değilseniz, birini oluşturmanız istenir.</span><span class="sxs-lookup"><span data-stu-id="fe4af-129">If you don't have an existing connection, you are prompted to create one.</span></span>

   1. <span data-ttu-id="fe4af-130">Seçin **Connect şirket içi veri ağ geçidi üzerinden**ve SAP sisteminizi ayrıntıları girin:</span><span class="sxs-lookup"><span data-stu-id="fe4af-130">Select **Connect via on-premises data gateway**, and enter the details for your SAP system:</span></span>   

       ![SAP için bağlantı dizesi Ekle](media/logic-apps-using-sap-connector/picture2.png)  

   2. <span data-ttu-id="fe4af-132">Altında **ağ geçidi**, mevcut bir ağ geçidi seçin veya yeni bir ağ geçidi yüklemek için seçin **ağ geçidi yükleme**.</span><span class="sxs-lookup"><span data-stu-id="fe4af-132">Under **Gateway**, select an existing gateway, or to install a new gateway, select **Install Gateway**.</span></span>

        ![Yeni bir ağ geçidi yükleyin](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. <span data-ttu-id="fe4af-134">Tüm Ayrıntılar girdikten sonra Seç **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="fe4af-134">After you enter all the details, select **Create**.</span></span> 
   <span data-ttu-id="fe4af-135">Logic Apps yapılandırır ve bağlantı düzgün çalıştığından emin olmayı bağlantısını test eder.</span><span class="sxs-lookup"><span data-stu-id="fe4af-135">Logic Apps configures and tests the connection, making sure that the connection works properly.</span></span>

4. <span data-ttu-id="fe4af-136">SAP bağlantınız için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="fe4af-136">Enter a name for your SAP connection.</span></span>

5. <span data-ttu-id="fe4af-137">Farklı SAP seçenekleri şimdi kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fe4af-137">The different SAP options are now available.</span></span> <span data-ttu-id="fe4af-138">IDOC kategori bulmak için listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="fe4af-138">To find your IDOC category, select from the list.</span></span> <span data-ttu-id="fe4af-139">Veya el ile yolu yazın ve HTTP yanıtı seçin **gövde** alan:</span><span class="sxs-lookup"><span data-stu-id="fe4af-139">Or manually type in the path, and select the HTTP response in the **body** field:</span></span>

     ![SAP eylemi](media/logic-apps-using-sap-connector/picture3.png)

6. <span data-ttu-id="fe4af-141">Oluşturma eylem eklemek bir **HTTP yanıtı**.</span><span class="sxs-lookup"><span data-stu-id="fe4af-141">Add the action for creating an **HTTP Response**.</span></span> <span data-ttu-id="fe4af-142">Yanıt iletisi SAP çıkışı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fe4af-142">The response message should be from the SAP output.</span></span>

7. <span data-ttu-id="fe4af-143">Mantıksal uygulamanızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fe4af-143">Save your logic app.</span></span> <span data-ttu-id="fe4af-144">IDOC HTTP tetikleme URL'si aracılığıyla göndererek test.</span><span class="sxs-lookup"><span data-stu-id="fe4af-144">Test it by sending an IDOC through the HTTP trigger URL.</span></span> <span data-ttu-id="fe4af-145">IDOC gönderildikten sonra mantıksal uygulama yanıttan bekleyin:</span><span class="sxs-lookup"><span data-stu-id="fe4af-145">After the IDOC is sent, wait for the response from the logic app:</span></span>   

     > [!TIP]
     > <span data-ttu-id="fe4af-146">Nasıl yapılır kullanıma [mantıksal uygulamalarınızı izleme](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="fe4af-146">Check out how to [monitor your Logic Apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="fe4af-147">SAP bağlayıcısı mantıksal uygulamanızı eklenir, diğer işlevleri keşfetmeye başlayın:</span><span class="sxs-lookup"><span data-stu-id="fe4af-147">Now that the SAP connector is added to your logic app, start exploring other functionalities:</span></span>

- <span data-ttu-id="fe4af-148">BAPI</span><span class="sxs-lookup"><span data-stu-id="fe4af-148">BAPI</span></span>
- <span data-ttu-id="fe4af-149">RFC</span><span class="sxs-lookup"><span data-stu-id="fe4af-149">RFC</span></span>

## <a name="get-help"></a><span data-ttu-id="fe4af-150">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="fe4af-150">Get help</span></span>

<span data-ttu-id="fe4af-151">Sorular sormak, soruları yanıtlamak ve diğer Azure Logic Apps kullanıcılarının neler yaptığını öğrenmek için [Azure Logic Apps forumunu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="fe4af-151">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="fe4af-152">Azure Logic Apps ve bağlayıcıları geliştirmeye yardımcı olmak için, [Azure Logic Apps kullanıcı geri bildirim sitesinde](http://aka.ms/logicapps-wish) oy kullanın veya fikirlerinizi paylaşın.</span><span class="sxs-lookup"><span data-stu-id="fe4af-152">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe4af-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fe4af-153">Next steps</span></span>

- <span data-ttu-id="fe4af-154">Dönüştürme nasıl doğrulamak ve diğer BizTalk benzeri işlevlerde öğrenin [Kurumsal tümleştirme paketi](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fe4af-154">Learn how to validate, transform, and other BizTalk-like functions in the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span> 
- <span data-ttu-id="fe4af-155">[Şirket içi veri bağlanmak](../logic-apps/logic-apps-gateway-connection.md) mantığı uygulamalardan</span><span class="sxs-lookup"><span data-stu-id="fe4af-155">[Connect to on-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
