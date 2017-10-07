---
title: "dönüşümler - Azure Logic Apps ile aaaConvert XML veri | Microsoft Docs"
description: "Dönüşümler veya mapps hello Kurumsal tümleştirme SDK kullanarak logic apps biçimlerde arasında tooconvert XML verileri oluşturma"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: add01429-21bc-4bab-8b23-bc76ba7d0bde
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: b56ec1072c5058d3aefc7f88ac9b2748ebe56456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-integration-with-xml-transforms"></a><span data-ttu-id="f374b-103">XML dönüşümler ile Kurumsal tümleştirme</span><span class="sxs-lookup"><span data-stu-id="f374b-103">Enterprise integration with XML transforms</span></span>
## <a name="overview"></a><span data-ttu-id="f374b-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f374b-104">Overview</span></span>
<span data-ttu-id="f374b-105">Merhaba Kurumsal tümleştirme dönüştürme Bağlayıcısı verileri bir biçim tooanother biçimden diğerine dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="f374b-105">hello Enterprise integration Transform connector converts data from one format tooanother format.</span></span> <span data-ttu-id="f374b-106">Örneğin, hello hello YearMonthDay biçiminde geçerli tarihi içeren gelen ileti olabilir.</span><span class="sxs-lookup"><span data-stu-id="f374b-106">For example, you may have an incoming message that contains hello current date in hello YearMonthDay format.</span></span> <span data-ttu-id="f374b-107">Merhaba MonthDayYear biçiminde bir dönüştürme tooreformat hello tarih toobe kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f374b-107">You can use a transform tooreformat hello date toobe in hello MonthDayYear format.</span></span>

## <a name="what-does-a-transform-do"></a><span data-ttu-id="f374b-108">Bir dönüştürme ne yapar?</span><span class="sxs-lookup"><span data-stu-id="f374b-108">What does a transform do?</span></span>
<span data-ttu-id="f374b-109">Kaynak XML Şeması (giriş hello) ve hedef XML Şeması (Merhaba çıktı) olarak da bilinen bir eşleme olduğundan, bir dönüşüm oluşur.</span><span class="sxs-lookup"><span data-stu-id="f374b-109">A Transform, which is also known as a map, consists of a Source XML schema (hello input) and a Target XML schema (hello output).</span></span> <span data-ttu-id="f374b-110">Toohelp yönetmek veya hello veri denetimi farklı yerleşik işlevler dahil dize işlemeleri, koşullu atamaları, aritmetik ifadeler, tarih saat biçimlendiricileri ve hatta döngü yapıları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f374b-110">You can use different built-in functions toohelp manipulate or control hello data, including string manipulations, conditional assignments, arithmetic expressions, date time formatters, and even looping constructs.</span></span>

## <a name="how-toocreate-a-transform"></a><span data-ttu-id="f374b-111">Nasıl toocreate bir dönüşüm?</span><span class="sxs-lookup"><span data-stu-id="f374b-111">How toocreate a transform?</span></span>
<span data-ttu-id="f374b-112">Merhaba Visual Studio kullanarak bir dönüşüm/eşlemesi oluşturabilirsiniz [Kurumsal tümleştirme SDK](https://aka.ms/vsmapsandschemas).</span><span class="sxs-lookup"><span data-stu-id="f374b-112">You can create a transform/map by using hello Visual Studio [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas).</span></span> <span data-ttu-id="f374b-113">Tamamlanmış oluşturma ve hello dönüştürme sınama olduğunda tümleştirme hesabınızda hello dönüştürme karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f374b-113">When you are finished creating and testing hello transform, you upload hello transform into your integration account.</span></span> 

## <a name="how-toouse-a-transform"></a><span data-ttu-id="f374b-114">Nasıl toouse bir dönüştürme</span><span class="sxs-lookup"><span data-stu-id="f374b-114">How toouse a transform</span></span>
<span data-ttu-id="f374b-115">Tümleştirme hesabınızda hello dönüştürme/map yükledikten sonra bir mantıksal uygulama toocreate kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f374b-115">After you upload hello transform/map into your integration account, you can use it toocreate a Logic app.</span></span> <span data-ttu-id="f374b-116">Merhaba mantıksal uygulama, dönüştürmeleri hello mantıksal uygulama tetiklenir (ve dönüştürülen toobe gereken Giriş bir içerik olduğunda) çalışır.</span><span class="sxs-lookup"><span data-stu-id="f374b-116">hello Logic app runs your transformations whenever hello Logic app is triggered (and there is input content that needs toobe transformed).</span></span>

<span data-ttu-id="f374b-117">**Bir dönüştürme hello adımları toouse işte**:</span><span class="sxs-lookup"><span data-stu-id="f374b-117">**Here are hello steps toouse a transform**:</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f374b-118">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f374b-118">Prerequisites</span></span>

* <span data-ttu-id="f374b-119">Bir tümleştirme hesabı oluşturun ve bir harita tooit ekleyin</span><span class="sxs-lookup"><span data-stu-id="f374b-119">Create an integration account and add a map tooit</span></span>  

<span data-ttu-id="f374b-120">Merhaba önkoşulların yapılan verdiğiniz göre zaman toocreate olduğu mantıksal uygulamanızı:</span><span class="sxs-lookup"><span data-stu-id="f374b-120">Now that you've taken care of hello prerequisites, it's time toocreate your Logic app:</span></span>  

1. <span data-ttu-id="f374b-121">Mantıksal uygulama oluşturma ve [tooyour tümleştirme hesap bağlantı](../logic-apps/logic-apps-enterprise-integration-accounts.md "toolink bir tümleştirme hesap tooa mantıksal uygulama öğrenin") hello eşlemesi içerir.</span><span class="sxs-lookup"><span data-stu-id="f374b-121">Create a Logic app and [link it tooyour integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn toolink an integration account tooa Logic app") that contains hello map.</span></span>
2. <span data-ttu-id="f374b-122">Ekleme bir **isteği** tetikleyici tooyour mantıksal uygulama</span><span class="sxs-lookup"><span data-stu-id="f374b-122">Add a **Request** trigger tooyour Logic app</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. <span data-ttu-id="f374b-123">Ekle hello **dönüştürme XML** ilk seçerek eylemi **Eylem Ekle** </span><span class="sxs-lookup"><span data-stu-id="f374b-123">Add hello **Transform XML** action by first selecting **Add an action** </span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. <span data-ttu-id="f374b-124">Merhaba sözcüğü girin *dönüştürme* hello arama kutusu toofilter tüm toouse istediğiniz eylemleri toohello bir hello</span><span class="sxs-lookup"><span data-stu-id="f374b-124">Enter hello word *transform* in hello search box toofilter all hello actions toohello one that you want toouse</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. <span data-ttu-id="f374b-125">Select hello **XML dönüştürme** eylem</span><span class="sxs-lookup"><span data-stu-id="f374b-125">Select hello **Transform XML** action</span></span>   
6. <span data-ttu-id="f374b-126">Merhaba XML eklemek **içerik** , dönüştüren.</span><span class="sxs-lookup"><span data-stu-id="f374b-126">Add hello XML **CONTENT** that you transform.</span></span> <span data-ttu-id="f374b-127">Merhaba HTTP isteği hello olarak aldığınız herhangi bir XML veri kullanabilirsiniz **içerik**.</span><span class="sxs-lookup"><span data-stu-id="f374b-127">You can use any XML data you receive in hello HTTP request as hello **CONTENT**.</span></span> <span data-ttu-id="f374b-128">Bu örnekte, hello hello mantıksal uygulama tetiklenen hello HTTP istek gövdesi seçin.</span><span class="sxs-lookup"><span data-stu-id="f374b-128">In this example, select hello body of hello HTTP request that triggered hello Logic app.</span></span>
7. <span data-ttu-id="f374b-129">Merhaba SELECT hello adını **harita** toouse tooperform hello dönüştürme istiyor.</span><span class="sxs-lookup"><span data-stu-id="f374b-129">Select hello name of hello **MAP** that you want toouse tooperform hello transformation.</span></span> <span data-ttu-id="f374b-130">Merhaba eşlemesi zaten tümleştirme hesabınız olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f374b-130">hello map must already be in your integration account.</span></span> <span data-ttu-id="f374b-131">Bir önceki adımda, eşleme içeren mantıksal uygulama erişim tooyour tümleştirme hesabınız zaten verdi.</span><span class="sxs-lookup"><span data-stu-id="f374b-131">In an earlier step, you already gave your Logic app access tooyour integration account that contains your map.</span></span>      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. <span data-ttu-id="f374b-132">Çalışmanızı kaydedin</span><span class="sxs-lookup"><span data-stu-id="f374b-132">Save your work</span></span>  
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

<span data-ttu-id="f374b-133">Bu noktada, map ayarlama tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="f374b-133">At this point, you are finished setting up your map.</span></span> <span data-ttu-id="f374b-134">Gerçek dünya uygulamada bir LOB uygulaması SalesForce gibi toostore hello dönüştürülmüş verileri isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f374b-134">In a real world application, you may want toostore hello transformed data in an LOB application such as SalesForce.</span></span> <span data-ttu-id="f374b-135">TooSalesforce hello eylem toosend hello çıktısı olarak kolayca dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f374b-135">You can easily as an action toosend hello output of hello transform tooSalesforce.</span></span> 

<span data-ttu-id="f374b-136">Ayrıca, bir istek toohello HTTP uç noktası yaparak, dönüştürme artık test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f374b-136">You can now test your transform by making a request toohello HTTP endpoint.</span></span>  

## <a name="features-and-use-cases"></a><span data-ttu-id="f374b-137">Özellikleri ve kullanım örnekleri</span><span class="sxs-lookup"><span data-stu-id="f374b-137">Features and use cases</span></span>
* <span data-ttu-id="f374b-138">Merhaba dönüştürme bir eşleminde oluşturulan bir ad ve adres bir belge tooanother kopyalama gibi basit olabilir.</span><span class="sxs-lookup"><span data-stu-id="f374b-138">hello transformation created in a map can be simple, such as copying a name and address from one document tooanother.</span></span> <span data-ttu-id="f374b-139">Veya daha karmaşık dönüşümleri hello Giden kutusu eşleme işlemleri kullanarak oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f374b-139">Or, you can create more complex transformations using hello out-of-the-box map operations.</span></span>  
* <span data-ttu-id="f374b-140">Birden çok eşleme işlemleri veya İşlevler dizeler, tarih saat işlevleri vb. dahil olmak üzere kullanıma hazır.</span><span class="sxs-lookup"><span data-stu-id="f374b-140">Multiple map operations or functions are readily available, including strings, date time functions, and so on.</span></span>  
* <span data-ttu-id="f374b-141">Merhaba Şemalar arasında doğrudan veri kopyalama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f374b-141">You can do a direct data copy between hello schemas.</span></span> <span data-ttu-id="f374b-142">Merhaba SDK Eşleyici dahil hello bu dekiler hello hedef şemasında ile Merhaba kaynak şemadaki hello öğelerin bağlayan bir çizgi çizme olarak kadar basittir.</span><span class="sxs-lookup"><span data-stu-id="f374b-142">In hello Mapper included in hello SDK, this is as simple as drawing a line that connects hello elements in hello source schema with their counterparts in hello destination schema.</span></span>  
* <span data-ttu-id="f374b-143">Bir harita oluştururken, tüm hello ilişkiler gösterilmektedir hello harita ve oluşturduğunuz bağlantıları grafik gösterimi görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="f374b-143">When creating a map, you view a graphical representation of hello map, which shows all hello relationships and links you create.</span></span>
* <span data-ttu-id="f374b-144">Merhaba Test eşleme özelliğini tooadd bir örnek XML ileti kullanın.</span><span class="sxs-lookup"><span data-stu-id="f374b-144">Use hello Test Map feature tooadd a sample XML message.</span></span> <span data-ttu-id="f374b-145">Bir basit tıklamayla oluşturulur ve oluşturulan hello çıktı görmeniz hello eşlemesi test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f374b-145">With a simple click, you can test hello map you created, and see hello generated output.</span></span>  
* <span data-ttu-id="f374b-146">Var olan eşlemeleri karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="f374b-146">Upload existing maps</span></span>  
* <span data-ttu-id="f374b-147">Merhaba XML biçimi için destek içerir.</span><span class="sxs-lookup"><span data-stu-id="f374b-147">Includes support for hello XML format.</span></span>

## <a name="learn-more"></a><span data-ttu-id="f374b-148">Daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="f374b-148">Learn more</span></span>
* [<span data-ttu-id="f374b-149">Merhaba Enterprise Integration Pack hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="f374b-149">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin")  
* [<span data-ttu-id="f374b-150">Eşlemeleri hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="f374b-150">Learn more about maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Kurumsal tümleştirme eşlemeleri hakkında bilgi edinin")  

