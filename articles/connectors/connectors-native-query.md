---
title: "logic apps içinde aaaAdd hello sorgu eylemi | Microsoft Docs"
description: "Filtre dizisi gibi eylemleri gerçekleştirmek için hello sorgu eylemi genel bakış."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 34e702c7-f9e5-4885-9266-fc7404adecfe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2016
ms.author: jehollan
ms.openlocfilehash: 3d4be901e7e6bf1b644057648930667ab34f2124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-query-action"></a><span data-ttu-id="4fae0-103">Merhaba sorgu eylemi ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="4fae0-103">Get started with hello query action</span></span>
<span data-ttu-id="4fae0-104">Merhaba sorgu eylemini kullanarak toplu ve diziler tooaccomplish iş akışları için çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4fae0-104">By using hello query action, you can work with batches and arrays tooaccomplish workflows to:</span></span>

* <span data-ttu-id="4fae0-105">Tüm yüksek öncelikli kayıtları için bir görev veritabanından oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4fae0-105">Create a task for all high-priority records from a database.</span></span>
* <span data-ttu-id="4fae0-106">Bir Azure blob e-postalara tüm PDF ekleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4fae0-106">Save all PDF attachments for emails into an Azure blob.</span></span>

<span data-ttu-id="4fae0-107">bir mantıksal uygulama Hello sorgu eylemi kullanmaya tooget bkz [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="4fae0-107">tooget started using hello query action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-query-action"></a><span data-ttu-id="4fae0-108">Merhaba sorgu eylemi kullanın</span><span class="sxs-lookup"><span data-stu-id="4fae0-108">Use hello query action</span></span>
<span data-ttu-id="4fae0-109">Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="4fae0-109">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="4fae0-110">[Eylemler hakkında daha fazla bilgi](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4fae0-110">[Learn more about actions](connectors-overview.md).</span></span>  

<span data-ttu-id="4fae0-111">Merhaba sorgu eylemi, şu anda hello Tasarımcısı'nda gösterilen hello filtre dizisi adlı bir işlem yok.</span><span class="sxs-lookup"><span data-stu-id="4fae0-111">hello query action currently has one operation, called hello filter array, that is exposed in hello designer.</span></span> <span data-ttu-id="4fae0-112">Bu tooquery bir dizi verir ve filtrelenmiş sonuç kümesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="4fae0-112">This allows you tooquery an array and return a set of filtered results.</span></span>

<span data-ttu-id="4fae0-113">İşte nasıl bir mantıksal uygulama ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4fae0-113">Here's how you can add it in a logic app:</span></span>

1. <span data-ttu-id="4fae0-114">Select hello **yeni adım** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4fae0-114">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="4fae0-115">Seçin **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="4fae0-115">Choose **Add an action**.</span></span>
3. <span data-ttu-id="4fae0-116">Merhaba eylem arama kutusuna yazın **filtre** toolist hello **filtre dizisi** eylem.</span><span class="sxs-lookup"><span data-stu-id="4fae0-116">In hello action search box, type **filter** toolist hello **Filter array** action.</span></span>
   
    ![Merhaba sorgu eylemi seçin](./media/connectors-native-query/using-action-1.png)
4. <span data-ttu-id="4fae0-118">Bir dizi toofilter seçin.</span><span class="sxs-lookup"><span data-stu-id="4fae0-118">Select an array toofilter.</span></span> <span data-ttu-id="4fae0-119">(Merhaba aşağıdaki ekran görüntüsünde bir Twitter Arama sonuçlarından hello dizisi gösterir.)</span><span class="sxs-lookup"><span data-stu-id="4fae0-119">(hello following screenshot shows hello array of results from a Twitter search.)</span></span>
5. <span data-ttu-id="4fae0-120">Bir koşul tooevaluate her bir öğede oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4fae0-120">Create a condition tooevaluate on each item.</span></span> <span data-ttu-id="4fae0-121">(ekran aşağıdaki hello tweet'leri 100'den fazla followers olan kullanıcılardan filtreler.)</span><span class="sxs-lookup"><span data-stu-id="4fae0-121">(hello following screenshot filters tweets from users who have more than 100 followers.)</span></span>
   
    ![Tam hello sorgu eylemi](./media/connectors-native-query/using-action-2.png)
   
    <span data-ttu-id="4fae0-123">Merhaba eylemin hello filtre gereksinimlerini karşılaması sonuçlarını içeren yeni bir dizi çıkarır.</span><span class="sxs-lookup"><span data-stu-id="4fae0-123">hello action will output a new array that contains only results that met hello filter requirements.</span></span>
6. <span data-ttu-id="4fae0-124">Merhaba sol üst köşesindeki hello araç toosave ve, logic app kazandırır hem'ı tıklatın ve yayımlama (etkinleştirin).</span><span class="sxs-lookup"><span data-stu-id="4fae0-124">Click hello upper-left corner of hello toolbar toosave, and your logic app will both save and publish (activate).</span></span>

## <a name="query-action"></a><span data-ttu-id="4fae0-125">Sorgu eylemi</span><span class="sxs-lookup"><span data-stu-id="4fae0-125">Query action</span></span>
<span data-ttu-id="4fae0-126">Aşağıda, bu bağlayıcıyı destekler hello eylemin hello Ayrıntılar verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4fae0-126">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="4fae0-127">Merhaba Bağlayıcısı olası eylem vardır.</span><span class="sxs-lookup"><span data-stu-id="4fae0-127">hello connector has one possible action.</span></span>

| <span data-ttu-id="4fae0-128">Eylem</span><span class="sxs-lookup"><span data-stu-id="4fae0-128">Action</span></span> | <span data-ttu-id="4fae0-129">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4fae0-129">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4fae0-130">Filtre dizisi</span><span class="sxs-lookup"><span data-stu-id="4fae0-130">Filter array</span></span> |<span data-ttu-id="4fae0-131">Dizideki her öğe için bir koşulu değerlendirir ve hello sonuçları döndürür</span><span class="sxs-lookup"><span data-stu-id="4fae0-131">Evaluates a condition for each item in an array and returns hello results</span></span> |

## <a name="action-details"></a><span data-ttu-id="4fae0-132">Eylem ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="4fae0-132">Action details</span></span>
<span data-ttu-id="4fae0-133">Merhaba sorgu eylemi bir olası eylemiyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="4fae0-133">hello query action comes with one possible action.</span></span> <span data-ttu-id="4fae0-134">Merhaba aşağıdaki tablolar hello gerekli ve isteğe bağlı giriş alanları hello eylem ve hello eylemini kullanarak ile ilişkili hello karşılık gelen çıkış ayrıntıları için açıklamaktadır.</span><span class="sxs-lookup"><span data-stu-id="4fae0-134">hello following tables describe hello required and optional input fields for hello action and hello corresponding output details that are associated with using hello action.</span></span>

### <a name="filter-array"></a><span data-ttu-id="4fae0-135">Filtre dizisi</span><span class="sxs-lookup"><span data-stu-id="4fae0-135">Filter array</span></span>
<span data-ttu-id="4fae0-136">Merhaba, HTTP giden isteğinde hello eylemi için girdi alanlarının verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4fae0-136">hello following are input fields for hello action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="4fae0-137">A * gerekli bir alan olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="4fae0-137">A * means that it is a required field.</span></span>

| <span data-ttu-id="4fae0-138">Görünen ad</span><span class="sxs-lookup"><span data-stu-id="4fae0-138">Display name</span></span> | <span data-ttu-id="4fae0-139">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="4fae0-139">Property name</span></span> | <span data-ttu-id="4fae0-140">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4fae0-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4fae0-141">Gelen *</span><span class="sxs-lookup"><span data-stu-id="4fae0-141">From*</span></span> |<span data-ttu-id="4fae0-142">Kaynak</span><span class="sxs-lookup"><span data-stu-id="4fae0-142">from</span></span> |<span data-ttu-id="4fae0-143">Merhaba dizi toofilter</span><span class="sxs-lookup"><span data-stu-id="4fae0-143">hello array toofilter</span></span> |
| <span data-ttu-id="4fae0-144">Koşul *</span><span class="sxs-lookup"><span data-stu-id="4fae0-144">Condition*</span></span> |<span data-ttu-id="4fae0-145">Burada</span><span class="sxs-lookup"><span data-stu-id="4fae0-145">where</span></span> |<span data-ttu-id="4fae0-146">her öğe için bir koşul tooevaluate hello</span><span class="sxs-lookup"><span data-stu-id="4fae0-146">hello condition tooevaluate for each item</span></span> |

<br>

### <a name="output-details"></a><span data-ttu-id="4fae0-147">Çıkış Ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="4fae0-147">Output details</span></span>
<span data-ttu-id="4fae0-148">Merhaba, hello HTTP yanıtının çıkış ayrıntıları verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4fae0-148">hello following are output details for hello HTTP response.</span></span>

| <span data-ttu-id="4fae0-149">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="4fae0-149">Property name</span></span> | <span data-ttu-id="4fae0-150">Veri türü</span><span class="sxs-lookup"><span data-stu-id="4fae0-150">Data type</span></span> | <span data-ttu-id="4fae0-151">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4fae0-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4fae0-152">Filtrelenmiş dizisi</span><span class="sxs-lookup"><span data-stu-id="4fae0-152">Filtered array</span></span> |<span data-ttu-id="4fae0-153">Dizi</span><span class="sxs-lookup"><span data-stu-id="4fae0-153">array</span></span> |<span data-ttu-id="4fae0-154">Her filtre uygulanmış bir sonucu için bir nesne içeren bir dizi</span><span class="sxs-lookup"><span data-stu-id="4fae0-154">An array that contains an object for each filtered result</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4fae0-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4fae0-155">Next steps</span></span>
<span data-ttu-id="4fae0-156">Şimdi, hello platform deneyin ve [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="4fae0-156">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="4fae0-157">Keşfedebilirsiniz bakarak logic apps içinde kullanılabilir diğer bağlayıcıları hello bizim [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="4fae0-157">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

