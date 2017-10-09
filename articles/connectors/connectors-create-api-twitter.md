---
title: "aaaLearn nasıl toouse hello logic apps Twitter Bağlayıcısı | Microsoft Docs"
description: "Twitter Bağlayıcısı REST API parametrelerle genel bakış"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8bce2183-544d-4668-a2dc-9a62c152d9fa
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: ead4e4dc95bf894fd72b908c5375b407ba27642d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twitter-connector"></a><span data-ttu-id="c4acd-103">Merhaba Twitter Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="c4acd-103">Get started with hello Twitter connector</span></span>
<span data-ttu-id="c4acd-104">Merhaba Twitter Bağlayıcısı ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c4acd-104">With hello Twitter connector you can:</span></span>

* <span data-ttu-id="c4acd-105">Tweetler ve get tweet'leri</span><span class="sxs-lookup"><span data-stu-id="c4acd-105">Post tweets and get tweets</span></span>
* <span data-ttu-id="c4acd-106">Erişim zaman çizelgeleri, arkadaşlarınıza ve followers</span><span class="sxs-lookup"><span data-stu-id="c4acd-106">Access timelines, friends and followers</span></span>
* <span data-ttu-id="c4acd-107">Diğer Eylemler ve aşağıda açıklanan Tetikleyicileri hello birini gerçekleştirin</span><span class="sxs-lookup"><span data-stu-id="c4acd-107">Perform any of hello other actions and triggers described below</span></span>  

<span data-ttu-id="c4acd-108">toouse [tüm bağlayıcıların](apis-list.md), toocreate bir mantıksal uygulama ilk gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4acd-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="c4acd-109">Tarafından başlayabiliriz [şimdi mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="c4acd-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>  

## <a name="connect-tootwitter"></a><span data-ttu-id="c4acd-110">TooTwitter Bağlan</span><span class="sxs-lookup"><span data-stu-id="c4acd-110">Connect tooTwitter</span></span>
<span data-ttu-id="c4acd-111">Mantıksal uygulamanızı herhangi bir hizmet erişebilmeniz için önce toocreate ilk gerekiyor bir *bağlantı* toohello hizmet.</span><span class="sxs-lookup"><span data-stu-id="c4acd-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="c4acd-112">A [bağlantı](connectors-overview.md) bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="c4acd-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-tootwitter"></a><span data-ttu-id="c4acd-113">Bir bağlantı tooTwitter oluşturma</span><span class="sxs-lookup"><span data-stu-id="c4acd-113">Create a connection tooTwitter</span></span>
> [!INCLUDE [Steps toocreate a connection tooTwitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a><span data-ttu-id="c4acd-114">Bir Twitter tetikleyici kullanın</span><span class="sxs-lookup"><span data-stu-id="c4acd-114">Use a Twitter trigger</span></span>
<span data-ttu-id="c4acd-115">Bir tetikleyici bir mantıksal uygulama tanımlı kullanılan toostart hello iş akışı olabilecek bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="c4acd-115">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="c4acd-116">[Tetikleyiciler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="c4acd-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="c4acd-117">Bu örnekte, ı bunu nasıl yapacağınızı gösterir toouse hello **yeni tweet zaman nakledilir** #Seattle toosearch tetikleyebilir ve #Seattle bulunursa, Dropbox dosyasında hello tweet hello metinden ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="c4acd-117">In this example, I will show you how toouse hello **When a new tweet is posted**  trigger toosearch for #Seattle and, if #Seattle is found, update a file in Dropbox with hello text from hello tweet.</span></span> <span data-ttu-id="c4acd-118">Bir kurumsal örnekte hello şirketinizin adını arayın ve hello tweet hello metinden ile bir SQL veritabanı güncelleştirmesi.</span><span class="sxs-lookup"><span data-stu-id="c4acd-118">In an enterprise example, you could search for hello name of your company and update a SQL database with hello text from hello tweet.</span></span>

1. <span data-ttu-id="c4acd-119">Girin *twitter* hello arama kutusuna hello logic apps tasarımcısında hello seçip **yeni tweet gönderildiğinde Twitter -** tetikleyici</span><span class="sxs-lookup"><span data-stu-id="c4acd-119">Enter *twitter* in hello search box on hello logic apps designer then select hello **Twitter - When a new tweet is posted**  trigger</span></span>   
   <span data-ttu-id="c4acd-120">![Twitter tetikleyici görüntü 1](./media/connectors-create-api-twitter/trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="c4acd-120">![Twitter trigger image 1](./media/connectors-create-api-twitter/trigger-1.png)</span></span>  
2. <span data-ttu-id="c4acd-121">Girin *#Seattle* hello içinde **arama metni** denetimi</span><span class="sxs-lookup"><span data-stu-id="c4acd-121">Enter *#Seattle* in hello **Search Text** control</span></span>  
   <span data-ttu-id="c4acd-122">![Twitter tetikleyici görüntü 2](./media/connectors-create-api-twitter/trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="c4acd-122">![Twitter trigger image 2](./media/connectors-create-api-twitter/trigger-2.png)</span></span> 

<span data-ttu-id="c4acd-123">Bu noktada, mantıksal uygulamanızı hello yürütülmesi diğer tetikleyiciler ve Eylemler hello iş akışında başlayacak bir tetikleyici ile yapılandırıldı.</span><span class="sxs-lookup"><span data-stu-id="c4acd-123">At this point, your logic app has been configured with a trigger that will begin a run of hello other triggers and actions in hello workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="c4acd-124">Bir mantıksal uygulama toobe için işlev, en az bir tetikleyici ve bir eylem içermelidir.</span><span class="sxs-lookup"><span data-stu-id="c4acd-124">For a logic app toobe functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="c4acd-125">Merhaba sonraki bölümde tooadd eylemin Hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="c4acd-125">Follow hello steps in hello next section tooadd an action.</span></span>  
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="c4acd-126">Koşul ekle</span><span class="sxs-lookup"><span data-stu-id="c4acd-126">Add a condition</span></span>
<span data-ttu-id="c4acd-127">Biz yalnızca 50'den fazla kullanıcısı olan kullanıcılardan tweet'leri ilginizi olduğundan, followers hello sayısı onaylar bir koşul toohello mantıksal uygulama ilk eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4acd-127">Since we are only interested in tweets from users with more than 50 users, a condition that confirms hello number of followers must first be added toohello logic app.</span></span>  

1. <span data-ttu-id="c4acd-128">Seçin **+ yeni adım** tooadd hello eylem istediğinizi tootake #Seattle içinde yeni bir tweet bulunduğunda</span><span class="sxs-lookup"><span data-stu-id="c4acd-128">Select **+ New step** tooadd hello action you would like tootake when #Seattle is found in a new tweet</span></span>  
   <span data-ttu-id="c4acd-129">![Twitter eylem görüntü 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span><span class="sxs-lookup"><span data-stu-id="c4acd-129">![Twitter action image 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span></span>  
2. <span data-ttu-id="c4acd-130">Select hello **bir koşul eklemek** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="c4acd-130">Select hello **Add a condition** link.</span></span>  
   <span data-ttu-id="c4acd-131">![Twitter koşul görüntü 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span><span class="sxs-lookup"><span data-stu-id="c4acd-131">![Twitter condition image 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span></span>  
   <span data-ttu-id="c4acd-132">Merhaba açılır **koşulu** burada kontrol edebilirsiniz koşulları gibi denetim *eşittir*, *olan değerinden*, *değerinden daha büyük*, *içeren*, vb..</span><span class="sxs-lookup"><span data-stu-id="c4acd-132">This opens hello **Condition** control where you can check conditions such as *is equal to*, *is less than*, *is greater than*, *contains*, etc.</span></span>  
   <span data-ttu-id="c4acd-133">![Twitter koşul görüntü 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span><span class="sxs-lookup"><span data-stu-id="c4acd-133">![Twitter condition image 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span></span>   
3. <span data-ttu-id="c4acd-134">Select hello **bir değer seçin** denetim.</span><span class="sxs-lookup"><span data-stu-id="c4acd-134">Select hello **Choose a value** control.</span></span>  
   <span data-ttu-id="c4acd-135">Bu denetimde, bir veya daha fazla hello özellik herhangi bir önceki eylem veya Tetikleyiciler koşulu değerlendirilen tootrue veya yanlış olacak hello değeri olarak seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4acd-135">In this control, you can select one or more of hello properties from any previous actions or triggers as hello value whose condition will be evaluated tootrue or false.</span></span>
   <span data-ttu-id="c4acd-136">![Twitter koşul görüntü 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span><span class="sxs-lookup"><span data-stu-id="c4acd-136">![Twitter condition image 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span></span>   
4. <span data-ttu-id="c4acd-137">Select hello **...**  tooexpand hello kullanılabilir olan tüm hello özellikler görebilmeniz için özelliklerin listesi.</span><span class="sxs-lookup"><span data-stu-id="c4acd-137">Select hello **...** tooexpand hello list of properties so you can see all hello properties that are available.</span></span>        
   <span data-ttu-id="c4acd-138">![Twitter koşul görüntü 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span><span class="sxs-lookup"><span data-stu-id="c4acd-138">![Twitter condition image 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span></span>   
5. <span data-ttu-id="c4acd-139">Select hello **Followers sayısı** özelliği.</span><span class="sxs-lookup"><span data-stu-id="c4acd-139">Select hello **Followers count** property.</span></span>    
   <span data-ttu-id="c4acd-140">![Twitter koşul görüntü 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span><span class="sxs-lookup"><span data-stu-id="c4acd-140">![Twitter condition image 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span></span>   
6. <span data-ttu-id="c4acd-141">Count özelliği hello değer denetiminde sunulmuştur hello Followers dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="c4acd-141">Notice hello Followers count property is now in hello value control.</span></span>    
   ![Twitter koşul görüntü 6](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. <span data-ttu-id="c4acd-143">Seçin **değerinden daha büyük** hello işleçleri listesinden.</span><span class="sxs-lookup"><span data-stu-id="c4acd-143">Select **is greater than** from hello operators list.</span></span>    
   <span data-ttu-id="c4acd-144">![Twitter koşul görüntü 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span><span class="sxs-lookup"><span data-stu-id="c4acd-144">![Twitter condition image 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span></span>   
8. <span data-ttu-id="c4acd-145">Merhaba işleneni hello 50 girin *değerinden daha büyük* işleci.</span><span class="sxs-lookup"><span data-stu-id="c4acd-145">Enter 50 as hello operand for hello *is greater than* operator.</span></span>  
   <span data-ttu-id="c4acd-146">Merhaba koşulu şimdi eklenir.</span><span class="sxs-lookup"><span data-stu-id="c4acd-146">hello condition is now added.</span></span> <span data-ttu-id="c4acd-147">Hello kullanarak çalışmanızı kaydedin **kaydetmek** yukarıdaki hello menüsünde bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="c4acd-147">Save your work using hello **Save** link on hello menu above.</span></span>    
   <span data-ttu-id="c4acd-148">![Twitter koşul görüntü 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span><span class="sxs-lookup"><span data-stu-id="c4acd-148">![Twitter condition image 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span></span>   

## <a name="use-a-twitter-action"></a><span data-ttu-id="c4acd-149">Bir Twitter eylemi kullanın</span><span class="sxs-lookup"><span data-stu-id="c4acd-149">Use a Twitter action</span></span>
<span data-ttu-id="c4acd-150">Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="c4acd-150">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="c4acd-151">[Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="c4acd-151">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="c4acd-152">Bir tetikleyici eklediğiniz, bu adımları tooadd hello tetik tarafından bulunan hello tweet'leri hello içeriğiyle yeni tweet gönderecek bir eylem izleyin.</span><span class="sxs-lookup"><span data-stu-id="c4acd-152">Now that you have added a trigger, follow these steps tooadd an action that will post a new tweet with hello contents of hello tweets found by hello trigger.</span></span> <span data-ttu-id="c4acd-153">Bu kılavuz Hello amaçları için yalnızca 50'den fazla followers sahip kullanıcılardan tweet'leri nakledilir.</span><span class="sxs-lookup"><span data-stu-id="c4acd-153">For hello purposes of this walk-through only tweets from users with more than 50 followers will be posted.</span></span>  

<span data-ttu-id="c4acd-154">Merhaba sonraki adımda, 50'den fazla followers sahip bir kullanıcı tarafından gönderilen her tweet hello özelliklerini bazıları kullanarak tweet gönderecek bir Twitter eylemi ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="c4acd-154">In hello next step, you will add a Twitter action that will post a tweet using some of hello properties of each tweet that has been posted by a user who has more than 50 followers.</span></span>  

1. <span data-ttu-id="c4acd-155">Seçin **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="c4acd-155">Select **Add an action**.</span></span> <span data-ttu-id="c4acd-156">Bu, diğer eylemler ve Tetikleyiciler için arayabileceğiniz hello arama denetimini açar.</span><span class="sxs-lookup"><span data-stu-id="c4acd-156">This opens hello search control where you can search for other actions and triggers.</span></span>  
   <span data-ttu-id="c4acd-157">![Twitter koşul görüntü 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span><span class="sxs-lookup"><span data-stu-id="c4acd-157">![Twitter condition image 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span></span>   
2. <span data-ttu-id="c4acd-158">Girin *twitter* hello arama kutusuna hello seçip **Twitter - tweet sonrası** eylem.</span><span class="sxs-lookup"><span data-stu-id="c4acd-158">Enter *twitter* into hello search box then select hello **Twitter - Post a tweet** action.</span></span> <span data-ttu-id="c4acd-159">Merhaba açılır **tweet sonrası** gönderilmesini hello tweet için tüm ayrıntıları gireceğiniz denetim.</span><span class="sxs-lookup"><span data-stu-id="c4acd-159">This opens hello **Post a tweet** control where you will enter all details for hello tweet being posted.</span></span>      
   <span data-ttu-id="c4acd-160">![Eylem görüntü 1-5 twitter](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span><span class="sxs-lookup"><span data-stu-id="c4acd-160">![Twitter action image 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span></span>   
3. <span data-ttu-id="c4acd-161">Select hello **Tweet metin** denetim.</span><span class="sxs-lookup"><span data-stu-id="c4acd-161">Select hello **Tweet text** control.</span></span> <span data-ttu-id="c4acd-162">Tüm çıktıları önceki Eylemler ve Tetikleyicileri hello mantıksal uygulama içinde görünür.</span><span class="sxs-lookup"><span data-stu-id="c4acd-162">All outputs from previous actions and triggers in hello logic app are now visible.</span></span> <span data-ttu-id="c4acd-163">Aşağıdakilerden herhangi birini seçin ve hello tweet hello yeni tweet metninin bir parçası olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="c4acd-163">You can select any of these and use them as part of hello tweet text of hello new tweet.</span></span>     
   <span data-ttu-id="c4acd-164">![Twitter eylem görüntü 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span><span class="sxs-lookup"><span data-stu-id="c4acd-164">![Twitter action image 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span></span>   
4. <span data-ttu-id="c4acd-165">Seçin **kullanıcı adı**</span><span class="sxs-lookup"><span data-stu-id="c4acd-165">Select **User name**</span></span>   
5. <span data-ttu-id="c4acd-166">Girin *diyor:* hello tweet metin denetimi.</span><span class="sxs-lookup"><span data-stu-id="c4acd-166">Enter *says:* in hello tweet text control.</span></span> <span data-ttu-id="c4acd-167">Yalnızca kullanıcı adından sonra bunu.</span><span class="sxs-lookup"><span data-stu-id="c4acd-167">Do this just after User name.</span></span>  
6. <span data-ttu-id="c4acd-168">Seçin *Tweet metin*.</span><span class="sxs-lookup"><span data-stu-id="c4acd-168">Select *Tweet text*.</span></span>       
   <span data-ttu-id="c4acd-169">![Twitter eylem görüntüsü 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span><span class="sxs-lookup"><span data-stu-id="c4acd-169">![Twitter action image 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span></span>   
7. <span data-ttu-id="c4acd-170">Çalışmanızı kaydedin ve iş akışınızı hello #Seattle diyez tooactivate ile tweet gönderecek.</span><span class="sxs-lookup"><span data-stu-id="c4acd-170">Save your work and send a tweet with hello #Seattle hashtag tooactivate your workflow.</span></span>  


## <a name="connector-specific-details"></a><span data-ttu-id="c4acd-171">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="c4acd-171">Connector-specific details</span></span>

<span data-ttu-id="c4acd-172">Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/twitterconnector/).</span><span class="sxs-lookup"><span data-stu-id="c4acd-172">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/twitterconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c4acd-173">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c4acd-173">Next steps</span></span>
[<span data-ttu-id="c4acd-174">Mantıksal uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c4acd-174">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

