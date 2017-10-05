---
title: "Logic apps içinde Twitter Bağlayıcısı'nı kullanmayı öğrenin | Microsoft Docs"
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
ms.openlocfilehash: be8163043535833ce45b3d50939a537406cf8152
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-twitter-connector"></a><span data-ttu-id="54458-103">Twitter Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="54458-103">Get started with the Twitter connector</span></span>
<span data-ttu-id="54458-104">Twitter Bağlayıcısı ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="54458-104">With the Twitter connector you can:</span></span>

* <span data-ttu-id="54458-105">Tweetler ve get tweet'leri</span><span class="sxs-lookup"><span data-stu-id="54458-105">Post tweets and get tweets</span></span>
* <span data-ttu-id="54458-106">Erişim zaman çizelgeleri, arkadaşlarınıza ve followers</span><span class="sxs-lookup"><span data-stu-id="54458-106">Access timelines, friends and followers</span></span>
* <span data-ttu-id="54458-107">Diğer Eylemler ve aşağıda açıklanan Tetikleyicileri gerçekleştirin</span><span class="sxs-lookup"><span data-stu-id="54458-107">Perform any of the other actions and triggers described below</span></span>  

<span data-ttu-id="54458-108">Kullanılacak [tüm bağlayıcıların](apis-list.md), ilk mantıksal uygulama oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="54458-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="54458-109">Tarafından başlayabiliriz [şimdi mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="54458-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>  

## <a name="connect-to-twitter"></a><span data-ttu-id="54458-110">Twitter hesabına bağlanma</span><span class="sxs-lookup"><span data-stu-id="54458-110">Connect to Twitter</span></span>
<span data-ttu-id="54458-111">Mantıksal uygulamanızı herhangi bir hizmet erişebilmeniz için önce ilk önce oluşturmanız gerekir bir *bağlantı* hizmet.</span><span class="sxs-lookup"><span data-stu-id="54458-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="54458-112">A [bağlantı](connectors-overview.md) bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="54458-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-twitter"></a><span data-ttu-id="54458-113">Twitter bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="54458-113">Create a connection to Twitter</span></span>
> [!INCLUDE [Steps to create a connection to Twitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a><span data-ttu-id="54458-114">Bir Twitter tetikleyici kullanın</span><span class="sxs-lookup"><span data-stu-id="54458-114">Use a Twitter trigger</span></span>
<span data-ttu-id="54458-115">Bir tetikleyici bir mantıksal uygulama tanımlı iş akışını başlatmak için kullanılan bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="54458-115">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="54458-116">[Tetikleyiciler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="54458-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="54458-117">Bu örnekte, ı size nasıl kullanılacağını gösterir **yeni tweet zaman nakledilir** #Seattle için arama ve #Seattle bulunursa, Dropbox dosyasında tweet metinden güncelleştirmek için tetikleyici.</span><span class="sxs-lookup"><span data-stu-id="54458-117">In this example, I will show you how to use the **When a new tweet is posted**  trigger to search for #Seattle and, if #Seattle is found, update a file in Dropbox with the text from the tweet.</span></span> <span data-ttu-id="54458-118">Bir kurumsal örnekte, şirketinizin adı aramak ve tweet metinden ile bir SQL veritabanı güncelleştirmesi.</span><span class="sxs-lookup"><span data-stu-id="54458-118">In an enterprise example, you could search for the name of your company and update a SQL database with the text from the tweet.</span></span>

1. <span data-ttu-id="54458-119">Girin *twitter* arama kutusuna logic apps tasarımcısında seçip **yeni tweet gönderildiğinde Twitter -** tetikleyici</span><span class="sxs-lookup"><span data-stu-id="54458-119">Enter *twitter* in the search box on the logic apps designer then select the **Twitter - When a new tweet is posted**  trigger</span></span>   
   <span data-ttu-id="54458-120">![Twitter tetikleyici görüntü 1](./media/connectors-create-api-twitter/trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="54458-120">![Twitter trigger image 1](./media/connectors-create-api-twitter/trigger-1.png)</span></span>  
2. <span data-ttu-id="54458-121">Girin *#Seattle* içinde **arama metni** denetimi</span><span class="sxs-lookup"><span data-stu-id="54458-121">Enter *#Seattle* in the **Search Text** control</span></span>  
   <span data-ttu-id="54458-122">![Twitter tetikleyici görüntü 2](./media/connectors-create-api-twitter/trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="54458-122">![Twitter trigger image 2](./media/connectors-create-api-twitter/trigger-2.png)</span></span> 

<span data-ttu-id="54458-123">Bu noktada, mantıksal uygulamanızı diğer tetikleyiciler ve Eylemler iş akışı bir farklı çalıştır başlayacak bir tetikleyici ile yapılandırıldı.</span><span class="sxs-lookup"><span data-stu-id="54458-123">At this point, your logic app has been configured with a trigger that will begin a run of the other triggers and actions in the workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="54458-124">Bir mantıksal uygulama işlevsel olması en az bir tetikleyici ve bir eylem içermelidir.</span><span class="sxs-lookup"><span data-stu-id="54458-124">For a logic app to be functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="54458-125">Bir eylem eklemek için sonraki bölümdeki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="54458-125">Follow the steps in the next section to add an action.</span></span>  
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="54458-126">Koşul ekle</span><span class="sxs-lookup"><span data-stu-id="54458-126">Add a condition</span></span>
<span data-ttu-id="54458-127">Biz yalnızca 50'den fazla kullanıcısı olan kullanıcılardan tweet'leri ilginizi olduğundan, mantıksal uygulama followers sayısı onaylar bir koşul önce eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="54458-127">Since we are only interested in tweets from users with more than 50 users, a condition that confirms the number of followers must first be added to the logic app.</span></span>  

1. <span data-ttu-id="54458-128">Seçin **+ yeni adım** #Seattle içinde yeni bir tweet bulunduğunda almak istediğiniz eylem eklemek için</span><span class="sxs-lookup"><span data-stu-id="54458-128">Select **+ New step** to add the action you would like to take when #Seattle is found in a new tweet</span></span>  
   <span data-ttu-id="54458-129">![Twitter eylem görüntü 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span><span class="sxs-lookup"><span data-stu-id="54458-129">![Twitter action image 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span></span>  
2. <span data-ttu-id="54458-130">Seçin **bir koşul eklemek** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="54458-130">Select the **Add a condition** link.</span></span>  
   <span data-ttu-id="54458-131">![Twitter koşul görüntü 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span><span class="sxs-lookup"><span data-stu-id="54458-131">![Twitter condition image 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span></span>  
   <span data-ttu-id="54458-132">Açılır **koşulu** burada kontrol edebilirsiniz koşulları gibi denetim *eşittir*, *olan değerinden*, *değerinden daha büyük*, *içeren*, vb..</span><span class="sxs-lookup"><span data-stu-id="54458-132">This opens the **Condition** control where you can check conditions such as *is equal to*, *is less than*, *is greater than*, *contains*, etc.</span></span>  
   <span data-ttu-id="54458-133">![Twitter koşul görüntü 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span><span class="sxs-lookup"><span data-stu-id="54458-133">![Twitter condition image 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span></span>   
3. <span data-ttu-id="54458-134">Seçin **bir değer seçin** denetim.</span><span class="sxs-lookup"><span data-stu-id="54458-134">Select the **Choose a value** control.</span></span>  
   <span data-ttu-id="54458-135">Bu denetimde, bir veya daha fazla özellik herhangi bir önceki eylem veya Tetikleyiciler koşulu değerlendirilecek değeri olarak doğru veya yanlış olarak seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54458-135">In this control, you can select one or more of the properties from any previous actions or triggers as the value whose condition will be evaluated to true or false.</span></span>
   <span data-ttu-id="54458-136">![Twitter koşul görüntü 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span><span class="sxs-lookup"><span data-stu-id="54458-136">![Twitter condition image 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span></span>   
4. <span data-ttu-id="54458-137">Seçin **...**  kullanılabilir olan tüm özellikler görebilmeniz için özellikler listesini genişletin.</span><span class="sxs-lookup"><span data-stu-id="54458-137">Select the **...** to expand the list of properties so you can see all the properties that are available.</span></span>        
   <span data-ttu-id="54458-138">![Twitter koşul görüntü 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span><span class="sxs-lookup"><span data-stu-id="54458-138">![Twitter condition image 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span></span>   
5. <span data-ttu-id="54458-139">Seçin **Followers sayısı** özelliği.</span><span class="sxs-lookup"><span data-stu-id="54458-139">Select the **Followers count** property.</span></span>    
   <span data-ttu-id="54458-140">![Twitter koşul görüntü 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span><span class="sxs-lookup"><span data-stu-id="54458-140">![Twitter condition image 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span></span>   
6. <span data-ttu-id="54458-141">Followers sayısı özelliği şimdi değer denetiminde olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="54458-141">Notice the Followers count property is now in the value control.</span></span>    
   ![Twitter koşul görüntü 6](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. <span data-ttu-id="54458-143">Seçin **değerinden daha büyük** işleçleri listesinden.</span><span class="sxs-lookup"><span data-stu-id="54458-143">Select **is greater than** from the operators list.</span></span>    
   <span data-ttu-id="54458-144">![Twitter koşul görüntü 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span><span class="sxs-lookup"><span data-stu-id="54458-144">![Twitter condition image 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span></span>   
8. <span data-ttu-id="54458-145">İşleneni olarak 50 girin *değerinden daha büyük* işleci.</span><span class="sxs-lookup"><span data-stu-id="54458-145">Enter 50 as the operand for the *is greater than* operator.</span></span>  
   <span data-ttu-id="54458-146">Koşul artık eklenir.</span><span class="sxs-lookup"><span data-stu-id="54458-146">The condition is now added.</span></span> <span data-ttu-id="54458-147">İş kullanarak Kaydet **kaydetmek** yukarıdaki menüsünde bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="54458-147">Save your work using the **Save** link on the menu above.</span></span>    
   <span data-ttu-id="54458-148">![Twitter koşul görüntü 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span><span class="sxs-lookup"><span data-stu-id="54458-148">![Twitter condition image 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span></span>   

## <a name="use-a-twitter-action"></a><span data-ttu-id="54458-149">Bir Twitter eylemi kullanın</span><span class="sxs-lookup"><span data-stu-id="54458-149">Use a Twitter action</span></span>
<span data-ttu-id="54458-150">Bir eylem, bir mantıksal uygulama içinde tanımlanan iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="54458-150">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="54458-151">[Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="54458-151">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="54458-152">Eklediğiniz bir tetikleyici, tetikleyici tarafından bulunan tweet'leri içeriğini yeni bir tweet gönderecek bir eylem eklemek için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="54458-152">Now that you have added a trigger, follow these steps to add an action that will post a new tweet with the contents of the tweets found by the trigger.</span></span> <span data-ttu-id="54458-153">Bu kılavuz amaçları için yalnızca 50'den fazla followers sahip kullanıcılardan tweet'leri nakledilir.</span><span class="sxs-lookup"><span data-stu-id="54458-153">For the purposes of this walk-through only tweets from users with more than 50 followers will be posted.</span></span>  

<span data-ttu-id="54458-154">Sonraki adımda, 50'den fazla followers sahip bir kullanıcı tarafından gönderilen her tweet özelliklerini kullanarak tweet gönderecek bir Twitter eylemi ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="54458-154">In the next step, you will add a Twitter action that will post a tweet using some of the properties of each tweet that has been posted by a user who has more than 50 followers.</span></span>  

1. <span data-ttu-id="54458-155">Seçin **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="54458-155">Select **Add an action**.</span></span> <span data-ttu-id="54458-156">Bu, diğer eylemler ve Tetikleyiciler için arayabileceğiniz arama denetimini açar.</span><span class="sxs-lookup"><span data-stu-id="54458-156">This opens the search control where you can search for other actions and triggers.</span></span>  
   <span data-ttu-id="54458-157">![Twitter koşul görüntü 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span><span class="sxs-lookup"><span data-stu-id="54458-157">![Twitter condition image 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span></span>   
2. <span data-ttu-id="54458-158">Girin *twitter* arama kutusuna seçip **Twitter - tweet sonrası** eylem.</span><span class="sxs-lookup"><span data-stu-id="54458-158">Enter *twitter* into the search box then select the **Twitter - Post a tweet** action.</span></span> <span data-ttu-id="54458-159">Bu açılır **tweet sonrası** gönderilmesini tweet için tüm ayrıntıları gireceğiniz denetim.</span><span class="sxs-lookup"><span data-stu-id="54458-159">This opens the **Post a tweet** control where you will enter all details for the tweet being posted.</span></span>      
   <span data-ttu-id="54458-160">![Eylem görüntü 1-5 twitter](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span><span class="sxs-lookup"><span data-stu-id="54458-160">![Twitter action image 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span></span>   
3. <span data-ttu-id="54458-161">Seçin **Tweet metin** denetim.</span><span class="sxs-lookup"><span data-stu-id="54458-161">Select the **Tweet text** control.</span></span> <span data-ttu-id="54458-162">Tüm çıktıları önceki Eylemler ve mantıksal uygulama Tetikleyicileri görünür.</span><span class="sxs-lookup"><span data-stu-id="54458-162">All outputs from previous actions and triggers in the logic app are now visible.</span></span> <span data-ttu-id="54458-163">Aşağıdakilerden herhangi birini seçin ve yeni tweet tweet metninin bir parçası olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="54458-163">You can select any of these and use them as part of the tweet text of the new tweet.</span></span>     
   <span data-ttu-id="54458-164">![Twitter eylem görüntü 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span><span class="sxs-lookup"><span data-stu-id="54458-164">![Twitter action image 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span></span>   
4. <span data-ttu-id="54458-165">Seçin **kullanıcı adı**</span><span class="sxs-lookup"><span data-stu-id="54458-165">Select **User name**</span></span>   
5. <span data-ttu-id="54458-166">Girin *diyor:* tweet metin denetimi.</span><span class="sxs-lookup"><span data-stu-id="54458-166">Enter *says:* in the tweet text control.</span></span> <span data-ttu-id="54458-167">Yalnızca kullanıcı adından sonra bunu.</span><span class="sxs-lookup"><span data-stu-id="54458-167">Do this just after User name.</span></span>  
6. <span data-ttu-id="54458-168">Seçin *Tweet metin*.</span><span class="sxs-lookup"><span data-stu-id="54458-168">Select *Tweet text*.</span></span>       
   <span data-ttu-id="54458-169">![Twitter eylem görüntüsü 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span><span class="sxs-lookup"><span data-stu-id="54458-169">![Twitter action image 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span></span>   
7. <span data-ttu-id="54458-170">Çalışmanızı kaydedin ve iş akışını etkinleştirmek için #Seattle diyez ile tweet gönderecek.</span><span class="sxs-lookup"><span data-stu-id="54458-170">Save your work and send a tweet with the #Seattle hashtag to activate your workflow.</span></span>  


## <a name="connector-specific-details"></a><span data-ttu-id="54458-171">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="54458-171">Connector-specific details</span></span>

<span data-ttu-id="54458-172">Tüm tetikleyiciler ve Eylemler swagger tanımlanan görüntüleyebilir ve ayrıca herhangi bir sınır bkz [Bağlayıcısı ayrıntıları](/connectors/twitterconnector/).</span><span class="sxs-lookup"><span data-stu-id="54458-172">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/twitterconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="54458-173">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="54458-173">Next steps</span></span>
[<span data-ttu-id="54458-174">Mantıksal uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="54458-174">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

