---
title: "Bir soru verileri yanıt - veri bilimi sorunlarını - Azure Machine Learning isteyin | Microsoft Docs"
description: "Video 3 yeni başlayanlar için veri bilimi sharp veri bilimi sorusuna formüle öğrenin. Sınıflandırma ve regresyon soruları karşılaştırması içerir."
keywords: "Veri bilimi sorunları, veri bilimi soruları formüle sorular, regresyon sorular, sınıflandırma sorular, sharp soru"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: 5b9501e3-9964-417a-8ffc-8913103da77b
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: 0495dbab72024e504ae33d35f16a212a2084bc10
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="ask-a-question-you-can-answer-with-data"></a><span data-ttu-id="d24a8-105">Verilerle yanıtlayabileceğiniz bir soru sorun</span><span class="sxs-lookup"><span data-stu-id="d24a8-105">Ask a question you can answer with data</span></span>
## <a name="video-3-data-science-for-beginners-series"></a><span data-ttu-id="d24a8-106">Video 3: Yeni başlayanlar seri için veri bilimi</span><span class="sxs-lookup"><span data-stu-id="d24a8-106">Video 3: Data Science for Beginners series</span></span>
<span data-ttu-id="d24a8-107">Video 3 yeni başlayanlar için veri bilimi sorusuna içine veri bilimi sorunu formüle öğrenin.</span><span class="sxs-lookup"><span data-stu-id="d24a8-107">Learn how to formulate a data science problem into a question in Data Science for Beginners video 3.</span></span> <span data-ttu-id="d24a8-108">Bu videoda, Sınıflandırma ve regresyon algoritmalar için sorular karşılaştırması içerir.</span><span class="sxs-lookup"><span data-stu-id="d24a8-108">This video includes a comparison of questions for classification and regression algorithms.</span></span>

<span data-ttu-id="d24a8-109">Serinin en dışında almak için tümünü izleyin.</span><span class="sxs-lookup"><span data-stu-id="d24a8-109">To get the most out of the series, watch them all.</span></span> <span data-ttu-id="d24a8-110">[Videolar listesine Git](#other-videos-in-this-series)
</span><span class="sxs-lookup"><span data-stu-id="d24a8-110">[Go to the list of videos](#other-videos-in-this-series)
</span></span><br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Data-science-for-beginners-Ask-a-question-you-can-answer-with-data/player]
>
>

## <a name="other-videos-in-this-series"></a><span data-ttu-id="d24a8-111">Bu serideki diğer videolar</span><span class="sxs-lookup"><span data-stu-id="d24a8-111">Other videos in this series</span></span>
<span data-ttu-id="d24a8-112">*Yeni başlayanlar için veri bilimi* veri bilimi beş kısa videolar içindeki bir giriş değil.</span><span class="sxs-lookup"><span data-stu-id="d24a8-112">*Data Science for Beginners* is a quick introduction to data science in five short videos.</span></span>

* <span data-ttu-id="d24a8-113">Video 1: [5 veri bilimi yanıtlar sorular](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 dakika 14 saniye)*</span><span class="sxs-lookup"><span data-stu-id="d24a8-113">Video 1: [The 5 questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span></span>
* <span data-ttu-id="d24a8-114">Video 2: [verileriniz için veri bilimi hazır?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span><span class="sxs-lookup"><span data-stu-id="d24a8-114">Video 2: [Is your data ready for data science?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span></span> <span data-ttu-id="d24a8-115">*(4 min 56 sn)*</span><span class="sxs-lookup"><span data-stu-id="d24a8-115">*(4 min 56 sec)*</span></span>
* <span data-ttu-id="d24a8-116">Video 3: verilerle yanıtlayabilir bir soru sorun</span><span class="sxs-lookup"><span data-stu-id="d24a8-116">Video 3: Ask a question you can answer with data</span></span>
* <span data-ttu-id="d24a8-117">Video 4: [basit bir modelle bir yanıt tahmin](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sn)*</span><span class="sxs-lookup"><span data-stu-id="d24a8-117">Video 4: [Predict an answer with a simple model](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*</span></span>
* <span data-ttu-id="d24a8-118">Video 5: [veri bilimi yapmak için diğer kişilerin çalışma kopyalama](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 dakika 18 saniye)*</span><span class="sxs-lookup"><span data-stu-id="d24a8-118">Video 5: [Copy other people's work to do data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span></span>

## <a name="transcript-ask-a-question-you-can-answer-with-data"></a><span data-ttu-id="d24a8-119">Dökümü: verilerle yanıtlayabilir bir soru sorun</span><span class="sxs-lookup"><span data-stu-id="d24a8-119">Transcript: Ask a question you can answer with data</span></span>
<span data-ttu-id="d24a8-120">Serideki üçüncü video "Yeni başlayanlar için veri bilimi." Hoş Geldiniz</span><span class="sxs-lookup"><span data-stu-id="d24a8-120">Welcome to the third video in the series "Data Science for Beginners."</span></span>  

<span data-ttu-id="d24a8-121">Bu birinde verilerle yanıtlayabilir soru formulating için bazı ipuçları elde edersiniz.</span><span class="sxs-lookup"><span data-stu-id="d24a8-121">In this one, you'll get some tips for formulating a question you can answer with data.</span></span>

<span data-ttu-id="d24a8-122">İki önceki videolar bu serideki ilk izleme, bu videoda dışında daha fazla bilgi alabilirsiniz: "5 soruları veri bilimi yanıtlayabilir" ve "verileriniz için veri bilimi hazır mı?"</span><span class="sxs-lookup"><span data-stu-id="d24a8-122">You might get more out of this video, if you first watch the two earlier videos in this series: "The 5 questions data science can answer" and "Is your data is ready for data science?"</span></span>

## <a name="ask-a-sharp-question"></a><span data-ttu-id="d24a8-123">NET bir soru sorun</span><span class="sxs-lookup"><span data-stu-id="d24a8-123">Ask a sharp question</span></span>
<span data-ttu-id="d24a8-124">Veri bilimi bir yanıtını tahmin etmek için (kategorileri veya etiketleri olarak da adlandırılır) adlarını ve numaralarını kullanma işlemi nasıl olduğu hakkında açıklandı.</span><span class="sxs-lookup"><span data-stu-id="d24a8-124">We've talked about how data science is the process of using names (also called categories or labels) and numbers to predict an answer to a question.</span></span> <span data-ttu-id="d24a8-125">Ancak herhangi bir soru olamaz; olmak zorundadır bir *sharp soru.*</span><span class="sxs-lookup"><span data-stu-id="d24a8-125">But it can't be just any question; it has to be a *sharp question.*</span></span>

<span data-ttu-id="d24a8-126">Belirsiz bir soru bir ad veya sayı ile yanıtlanması gereken sahip değil.</span><span class="sxs-lookup"><span data-stu-id="d24a8-126">A vague question doesn't have to be answered with a name or a number.</span></span> <span data-ttu-id="d24a8-127">Sharp soru gerekir.</span><span class="sxs-lookup"><span data-stu-id="d24a8-127">A sharp question must.</span></span>

<span data-ttu-id="d24a8-128">Sihirli ampul istenir soru truthfully yanıtlayacak bir genie ile bulunan düşünün.</span><span class="sxs-lookup"><span data-stu-id="d24a8-128">Imagine you found a magic lamp with a genie who will truthfully answer any question you ask.</span></span> <span data-ttu-id="d24a8-129">Ancak yaramaz genie olan ve kendisine kendisi yerine ile alabilirsiniz gibi kendi yanıt belirsiz ve karmaşık hale getirmek deneyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d24a8-129">But it's a mischievous genie, and he'll try to make his answer as vague and confusing as he can get away with.</span></span> <span data-ttu-id="d24a8-130">Bir soruyla kendisi olamaz yardımcı olur ancak bilmek istediğiniz söyleyin, bu nedenle airtight sabitlemek ona istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="d24a8-130">You want to pin him down with a question so airtight that he can't help but tell you what you want to know.</span></span>

<span data-ttu-id="d24a8-131">Genie yanıt "Benim hisse olmasını neler olduğunu?", "fiyat değişir" gibi belirsiz bir soru sormak için olsaydı.</span><span class="sxs-lookup"><span data-stu-id="d24a8-131">If you were to ask a vague question, like "What's going to happen with my stock?", the genie might answer, "The price will change".</span></span> <span data-ttu-id="d24a8-132">Gerçek bir yanıt olan, ancak çok yararlı değildir.</span><span class="sxs-lookup"><span data-stu-id="d24a8-132">That's a truthful answer, but it's not very helpful.</span></span>

<span data-ttu-id="d24a8-133">Ancak "ne my hisse senedi 's satış fiyatı sonraki hafta?", genie olamaz Yardım ancak belirli bir size gibi keskin bir soru sorun olsaydı yanıtlayın ve satış fiyatını tahmin etmek.</span><span class="sxs-lookup"><span data-stu-id="d24a8-133">But if you were to ask a sharp question, like "What will my stock's sale price be next week?", the genie can't help but give you a specific answer and predict a sale price.</span></span>

## <a name="examples-of-your-answer-target-data"></a><span data-ttu-id="d24a8-134">Yanıtınız örnekleri: hedef veri</span><span class="sxs-lookup"><span data-stu-id="d24a8-134">Examples of your answer: Target data</span></span>
<span data-ttu-id="d24a8-135">Sorunuzun yanıtını formüle sonra verilerinizi yanıt örnekleri yüklü olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="d24a8-135">Once you formulate your question, check to see whether you have examples of the answer in your data.</span></span>

<span data-ttu-id="d24a8-136">Bizim Soru "Ne my hisse senedi 's satış fiyatı sonraki hafta olacak?" ise</span><span class="sxs-lookup"><span data-stu-id="d24a8-136">If our question is "What will my stock's sale price be next week?"</span></span> <span data-ttu-id="d24a8-137">ardından verilerimizi stok fiyat geçmişi içerdiğinden emin olmak sahibiz.</span><span class="sxs-lookup"><span data-stu-id="d24a8-137">then we have to make sure our data includes the stock price history.</span></span>

<span data-ttu-id="d24a8-138">Bizim Soru "hangi otomobil my Donanma içinde ilk başarısız olacağını?" ise</span><span class="sxs-lookup"><span data-stu-id="d24a8-138">If our question is "Which car in my fleet is going to fail first?"</span></span> <span data-ttu-id="d24a8-139">ardından verilerimizi önceki hataları hakkında bilgi içeren emin olmak sahibiz.</span><span class="sxs-lookup"><span data-stu-id="d24a8-139">then we have to make sure our data includes information about previous failures.</span></span>

![Hedef verileri - yanıtınız örnekleri.](./media/machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data/target-data.png)

<span data-ttu-id="d24a8-142">Bu örnek yanıt olarak bir hedef adı verilir.</span><span class="sxs-lookup"><span data-stu-id="d24a8-142">These examples of answers are called a target.</span></span> <span data-ttu-id="d24a8-143">Bir kategori veya bir sayı olup olmadığını ne numaralı gelecekteki veri noktaları hakkında tahmin etmek çalışıyoruz hata hedefidir.</span><span class="sxs-lookup"><span data-stu-id="d24a8-143">A target is what we are trying to predict about future data points, whether it's a category or a number.</span></span>

<span data-ttu-id="d24a8-144">Herhangi bir hedef veri yoksa, bazı almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d24a8-144">If you don't have any target data, you'll need to get some.</span></span> <span data-ttu-id="d24a8-145">Sorunuzu olmadan yanıt vermiyor.</span><span class="sxs-lookup"><span data-stu-id="d24a8-145">You won't be able to answer your question without it.</span></span>

## <a name="reformulate-your-question"></a><span data-ttu-id="d24a8-146">Sorunuzu reformulate</span><span class="sxs-lookup"><span data-stu-id="d24a8-146">Reformulate your question</span></span>
<span data-ttu-id="d24a8-147">Bazen, sorunuzu daha kullanışlı bir yanıt almak için yeniden ifade et.</span><span class="sxs-lookup"><span data-stu-id="d24a8-147">Sometimes you can reword your question to get a more useful answer.</span></span>

<span data-ttu-id="d24a8-148">"Bu veri noktası A veya B mi?" sorusunu</span><span class="sxs-lookup"><span data-stu-id="d24a8-148">The question "Is this data point A or B?"</span></span> <span data-ttu-id="d24a8-149">Kategori (adını veya etiketi), bir şeyin tahmin eder.</span><span class="sxs-lookup"><span data-stu-id="d24a8-149">predicts the category (or name or label) of something.</span></span> <span data-ttu-id="d24a8-150">Yanıt için kullanırız bir *sınıflandırma algoritmasıdır*.</span><span class="sxs-lookup"><span data-stu-id="d24a8-150">To answer it, we use a *classification algorithm*.</span></span>

<span data-ttu-id="d24a8-151">Soru "Ne kadar?"</span><span class="sxs-lookup"><span data-stu-id="d24a8-151">The question "How much?"</span></span> <span data-ttu-id="d24a8-152">veya "Kaç?"</span><span class="sxs-lookup"><span data-stu-id="d24a8-152">or "How many?"</span></span> <span data-ttu-id="d24a8-153">bir miktar tahmin eder.</span><span class="sxs-lookup"><span data-stu-id="d24a8-153">predicts an amount.</span></span> <span data-ttu-id="d24a8-154">Yanıt için kullanırız bir *regresyon algoritması*.</span><span class="sxs-lookup"><span data-stu-id="d24a8-154">To answer it we use a *regression algorithm*.</span></span>

<span data-ttu-id="d24a8-155">Biz bu nasıl dönüştürebilirsiniz görmek için "hangi haber öykü bu okuyucuya en ilginç mi?" sorusunu bakalım</span><span class="sxs-lookup"><span data-stu-id="d24a8-155">To see how we can transform these, let's look at the question, "Which news story is the most interesting to this reader?"</span></span> <span data-ttu-id="d24a8-156">Bu çok sayıda olasılıklar - arasından tek bir seçim tahminini diğer bir deyişle "Bu A veya B veya C D mi?" ister</span><span class="sxs-lookup"><span data-stu-id="d24a8-156">It asks for a prediction of a single choice from many possibilities - in other words "Is this A or B or C or D?"</span></span> <span data-ttu-id="d24a8-157">- ve bir sınıflandırma algoritmasıdır kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="d24a8-157">- and would use a classification algorithm.</span></span>

<span data-ttu-id="d24a8-158">Ancak, bu soruyu "Bu okuyucu için bu listede her hikaye nasıl ilginç?" olarak yeniden ifade et varsa yanıt daha kolay olabilir</span><span class="sxs-lookup"><span data-stu-id="d24a8-158">But, this question may be easier to answer if you reword it as "How interesting is each story on this list to this reader?"</span></span> <span data-ttu-id="d24a8-159">Şimdi her makale sayısal bir puan verebilirsiniz ve sonra Puanlama yüksek makaleyi tanımlamak kolaydır.</span><span class="sxs-lookup"><span data-stu-id="d24a8-159">Now you can give each article a numerical score, and then it's easy to identify the highest-scoring article.</span></span> <span data-ttu-id="d24a8-160">Sınıflandırma soru regresyon soru içine yeniden budur veya ne kadar?</span><span class="sxs-lookup"><span data-stu-id="d24a8-160">This is a rephrasing of the classification question into a regression question or How much?</span></span>

![Sorunuzu reformulate.](./media/machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data/classification-question-vs-regression-question.png)

<span data-ttu-id="d24a8-163">Bir soru algoritmayı bir ipucu olan isteyin nasıl yanıt verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d24a8-163">How you ask a question is a clue to which algorithm can give you an answer.</span></span>

<span data-ttu-id="d24a8-164">Algoritma - haber Öykü örneğimizde - olanlar gibi bazı aileleri yakından ilişkilidir bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d24a8-164">You'll find that certain families of algorithms - like the ones in our news story example - are closely related.</span></span> <span data-ttu-id="d24a8-165">Sorunuzu en yararlı yanıt verir algoritmayı reformulate.</span><span class="sxs-lookup"><span data-stu-id="d24a8-165">You can reformulate your question to use the algorithm that gives you the most useful answer.</span></span>

<span data-ttu-id="d24a8-166">Ancak, en önemlisi, o sharp soru - verilerle yanıtlayabilir soru sorun.</span><span class="sxs-lookup"><span data-stu-id="d24a8-166">But, most important, ask that sharp question - the question that you can answer with data.</span></span> <span data-ttu-id="d24a8-167">Ve yanıtlamak için doğru verilere sahip olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d24a8-167">And be sure you have the right data to answer it.</span></span>

<span data-ttu-id="d24a8-168">Verilerle yanıtlayabilir bir soru sormak bazı temel ilkeleri hakkında açıklandı.</span><span class="sxs-lookup"><span data-stu-id="d24a8-168">We've talked about some basic principles for asking a question you can answer with data.</span></span>

<span data-ttu-id="d24a8-169">"Veri bilimi için yeni başlayanlar" Microsoft Azure Machine learning'in diğer videoları kullanıma emin olun.</span><span class="sxs-lookup"><span data-stu-id="d24a8-169">Be sure to check out the other videos in "Data Science for Beginners" from Microsoft Azure Machine Learning.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d24a8-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d24a8-170">Next steps</span></span>
* [<span data-ttu-id="d24a8-171">İlk veri bilimi denemeyi Machine Learning Studio'da deneyin</span><span class="sxs-lookup"><span data-stu-id="d24a8-171">Try a first data science experiment with Machine Learning Studio</span></span>](machine-learning-create-experiment.md)
* [<span data-ttu-id="d24a8-172">Microsoft Azure Machine Learning giriş Al</span><span class="sxs-lookup"><span data-stu-id="d24a8-172">Get an introduction to Machine Learning on Microsoft Azure</span></span>](machine-learning-what-is-machine-learning.md)
