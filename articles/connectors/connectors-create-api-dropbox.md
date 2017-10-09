---
title: "Azure mantıksal uygulamaları aaaDropbox Bağlayıcısı | Microsoft Docs"
description: "Logic apps ile Azure uygulama hizmeti oluşturun. TooDropbox toomanage dosyalarınızı bağlayın. Karşıya yükleme gibi çeşitli eylemleri, güncelleştirme, almak ve Dropbox dosyaları silin."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: cb0ae033-aba7-4ac9-beaa-be561a0f0cac
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 1f307477836104c0bc0008341604a1400860987f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-dropbox-connector"></a><span data-ttu-id="1ac77-105">Merhaba Dropbox Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="1ac77-105">Get started with hello Dropbox connector</span></span>
<span data-ttu-id="1ac77-106">TooDropbox toomanage dosyalarınızı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="1ac77-106">Connect tooDropbox toomanage your files.</span></span> <span data-ttu-id="1ac77-107">Karşıya yükleme gibi çeşitli eylemleri, güncelleştirme, almak ve Dropbox dosyaları silin.</span><span class="sxs-lookup"><span data-stu-id="1ac77-107">You can perform various actions such as upload, update, get, and delete files in Dropbox.</span></span>

<span data-ttu-id="1ac77-108">toouse [tüm bağlayıcıların](apis-list.md), toocreate bir mantıksal uygulama ilk gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ac77-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="1ac77-109">Tarafından başlayabiliriz [şimdi mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="1ac77-109">You can get started by [creating a Logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toodropbox"></a><span data-ttu-id="1ac77-110">TooDropbox Bağlan</span><span class="sxs-lookup"><span data-stu-id="1ac77-110">Connect tooDropbox</span></span>
<span data-ttu-id="1ac77-111">Mantıksal uygulamanızı herhangi bir hizmet erişebilmeniz için önce toocreate ilk gerekiyor bir *bağlantı* toohello hizmet.</span><span class="sxs-lookup"><span data-stu-id="1ac77-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="1ac77-112">Bağlantı bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="1ac77-112">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="1ac77-113">Örneğin, sipariş tooconnect tooDropbox ilk açılan kutu ihtiyacınız *bağlantı*.</span><span class="sxs-lookup"><span data-stu-id="1ac77-113">For example, in order tooconnect tooDropbox, you first need a Dropbox *connection*.</span></span> <span data-ttu-id="1ac77-114">toocreate bir bağlantı, normalde tooconnect için istediğiniz tooaccess hello hizmeti kullandığınız tooprovide hello kimlik bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ac77-114">toocreate a connection, you would need tooprovide hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="1ac77-115">Bu nedenle, hello Dropbox örnekte hello kimlik bilgilerini tooyour sipariş toocreate hello bağlantı tooDropbox Dropbox hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ac77-115">So, in hello Dropbox example, you would need hello credentials tooyour Dropbox account in order toocreate hello connection tooDropbox.</span></span> [<span data-ttu-id="1ac77-116">Bağlantılar hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="1ac77-116">Learn more about connections</span></span>]()

### <a name="create-a-connection-toodropbox"></a><span data-ttu-id="1ac77-117">Bir bağlantı tooDropbox oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ac77-117">Create a connection tooDropbox</span></span>
> [!INCLUDE [Steps toocreate a connection tooDropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a><span data-ttu-id="1ac77-118">Bir Dropbox tetikleyici kullanın</span><span class="sxs-lookup"><span data-stu-id="1ac77-118">Use a Dropbox trigger</span></span>
<span data-ttu-id="1ac77-119">Bir tetikleyici bir mantıksal uygulama tanımlı kullanılan toostart hello iş akışı olabilecek bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="1ac77-119">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="1ac77-120">[Tetikleyiciler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="1ac77-120">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="1ac77-121">Bu örnekte, hello kullanacağız **bir dosya oluşturulduğunda** tetikleyici.</span><span class="sxs-lookup"><span data-stu-id="1ac77-121">In this example, we will use hello **When a file is created** trigger.</span></span> <span data-ttu-id="1ac77-122">Bu tetikleyici oluştuğunda hello numarayı arayacaktır **alma yolunu kullanarak dosya içeriğini** Dropbox eylem.</span><span class="sxs-lookup"><span data-stu-id="1ac77-122">When this trigger occurs, we will call hello **Get file content using path** Dropbox action.</span></span> 

1. <span data-ttu-id="1ac77-123">Girin *dropbox* hello arama kutusuna hello Logic Apps tasarımcısında hello seçip **bir dosya oluşturulduğunda, Dropbox -** tetikleyici.</span><span class="sxs-lookup"><span data-stu-id="1ac77-123">Enter *dropbox* in hello search box on hello Logic Apps designer, then select hello **Dropbox - When a file is created** trigger.</span></span>      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. <span data-ttu-id="1ac77-124">Tootrack dosya oluşturma istediğiniz hello klasörünü seçin.</span><span class="sxs-lookup"><span data-stu-id="1ac77-124">Select hello folder in which you want tootrack file creation.</span></span> <span data-ttu-id="1ac77-125">Seçin... (kırmızı hello kutusunda tanımlanır) ve istediğiniz tooselect hello tetikleyici için giriş Gözat toohello klasör.</span><span class="sxs-lookup"><span data-stu-id="1ac77-125">Select ... (identified in hello red box) and browse toohello folder you wish tooselect for hello trigger's input.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a><span data-ttu-id="1ac77-126">Bir Dropbox eylemi kullanın</span><span class="sxs-lookup"><span data-stu-id="1ac77-126">Use a Dropbox action</span></span>
<span data-ttu-id="1ac77-127">Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="1ac77-127">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="1ac77-128">[Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="1ac77-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="1ac77-129">Merhaba tetikleyici eklenmiş durumda, bu adımları tooadd hello yeni dosyanın içeriğini alacak bir eylem izleyin.</span><span class="sxs-lookup"><span data-stu-id="1ac77-129">Now that hello trigger has been added, follow these steps tooadd an action that will get hello new file's content.</span></span>

1. <span data-ttu-id="1ac77-130">Seçin **+ yeni adım** tooadd hello eylem istediğinizi tootake yeni bir dosya oluşturulurken.</span><span class="sxs-lookup"><span data-stu-id="1ac77-130">Select **+ New Step** tooadd hello action you would like tootake when a new file is created.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. <span data-ttu-id="1ac77-131">Seçin **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="1ac77-131">Select **Add an action**.</span></span> <span data-ttu-id="1ac77-132">Bu açılır hello arama kutusu için herhangi bir işlem, arayabileceğiniz tootake ister.</span><span class="sxs-lookup"><span data-stu-id="1ac77-132">This opens hello search box where you can search for any action you would like tootake.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. <span data-ttu-id="1ac77-133">Girin *dropbox* Eylemler ilgili tooDropbox toosearch.</span><span class="sxs-lookup"><span data-stu-id="1ac77-133">Enter *dropbox* toosearch for actions related tooDropbox.</span></span>  
4. <span data-ttu-id="1ac77-134">Seçin **Dropbox - yolunu kullanarak dosya alma içeriği** eylem tootake hello olarak yeni bir dosya hello oluşturulduğunda Dropbox klasörü seçilen.</span><span class="sxs-lookup"><span data-stu-id="1ac77-134">Select **Dropbox - Get file content using path** as hello action tootake when a new file is created in hello selected Dropbox folder.</span></span> <span data-ttu-id="1ac77-135">Merhaba eylem denetim bloğu açılır.</span><span class="sxs-lookup"><span data-stu-id="1ac77-135">hello action control block opens.</span></span> <span data-ttu-id="1ac77-136">İstendiğinde tooauthorize, Dropbox hesabını, daha önce yapmadıysanız, logic app tooaccess olacaktır.</span><span class="sxs-lookup"><span data-stu-id="1ac77-136">You will be prompted tooauthorize your logic app tooaccess your Dropbox account if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. <span data-ttu-id="1ac77-137">Seçin... (Merhaba sağ tarafında hello bulunan **dosya yolu** denetimi) ve toouse istediğinizi toohello dosya yolu göz atın.</span><span class="sxs-lookup"><span data-stu-id="1ac77-137">Select ... (located at hello right side of hello **File Path** control) and browse toohello file path you would like toouse.</span></span> <span data-ttu-id="1ac77-138">Ya da hello kullan **dosya yolu** belirteci toospeed logic app oluşturma ayarlama.</span><span class="sxs-lookup"><span data-stu-id="1ac77-138">Or, use hello **file path** token toospeed up your logic app creation.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. <span data-ttu-id="1ac77-139">Çalışmanızı kaydedin ve iş akışınızı Dropbox tooactivate yeni bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1ac77-139">Save your work and create a new file in Dropbox tooactivate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="1ac77-140">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="1ac77-140">Connector-specific details</span></span>

<span data-ttu-id="1ac77-141">Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/dropbox/).</span><span class="sxs-lookup"><span data-stu-id="1ac77-141">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/dropbox/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="1ac77-142">Daha fazla bağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="1ac77-142">More connectors</span></span>
<span data-ttu-id="1ac77-143">Toohello dönün [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="1ac77-143">Go back toohello [APIs list](apis-list.md).</span></span>
