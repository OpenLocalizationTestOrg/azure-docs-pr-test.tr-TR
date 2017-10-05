---
title: "Verileriniz veri bilimi için hazır mı? Veri değerlendirmesi - Azure Machine Learning | Microsoft Docs"
description: "Veri bilimi için hazır olmasını veriler için 4 ölçüt öğrenin. Veri bilimi video 2 yeni başlayanlar için temel veri değerlendirme ile yardımcı olmak için somut örnekler vardır."
keywords: "ilgili verileri verileri değerlendirmek, verileri, veri ölçütlerini, veri hazır hazırlayın"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: d502062c-da70-4b21-9054-0bfd9902612e
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: c4a8bc11aec2f71796f589c0af54cc92253e5180
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="is-your-data-ready-for-data-science"></a><span data-ttu-id="82de0-106">Verileriniz veri bilimi için hazır mı?</span><span class="sxs-lookup"><span data-stu-id="82de0-106">Is your data ready for data science?</span></span>
## <a name="video-2-data-science-for-beginners-series"></a><span data-ttu-id="82de0-107">Video 2: Veri bilimi yeni başlayanlar seri için</span><span class="sxs-lookup"><span data-stu-id="82de0-107">Video 2: Data Science for Beginners series</span></span>
<span data-ttu-id="82de0-108">Verilerinizi veri bilimi için hazır olması için temel ölçütlerini karşıladığından emin olmak için değerlendirilecek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="82de0-108">Learn how to evaluate your data to make sure it meets basic criteria to be ready for data science.</span></span>

<span data-ttu-id="82de0-109">Serinin en dışında almak için tümünü izleyin.</span><span class="sxs-lookup"><span data-stu-id="82de0-109">To get the most out of the series, watch them all.</span></span> <span data-ttu-id="82de0-110">[Videolar listesine Git](#other-videos-in-this-series)
</span><span class="sxs-lookup"><span data-stu-id="82de0-110">[Go to the list of videos](#other-videos-in-this-series)
</span></span><br>

> [!VIDEO https://channel9.msdn.com/Shows/SupervisionNotRequired/9/player]
>
>

## <a name="other-videos-in-this-series"></a><span data-ttu-id="82de0-111">Bu serideki diğer videolar</span><span class="sxs-lookup"><span data-stu-id="82de0-111">Other videos in this series</span></span>
<span data-ttu-id="82de0-112">*Yeni başlayanlar için veri bilimi* veri bilimi beş kısa videolar içindeki bir giriş değil.</span><span class="sxs-lookup"><span data-stu-id="82de0-112">*Data Science for Beginners* is a quick introduction to data science in five short videos.</span></span>

* <span data-ttu-id="82de0-113">Video 1: [5 veri bilimi yanıtlar sorular](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 dakika 14 saniye)*</span><span class="sxs-lookup"><span data-stu-id="82de0-113">Video 1: [The 5 questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span></span>
* <span data-ttu-id="82de0-114">Video 2: verileriniz için veri bilimi hazır mı?</span><span class="sxs-lookup"><span data-stu-id="82de0-114">Video 2: Is your data ready for data science?</span></span>
* <span data-ttu-id="82de0-115">Video 3: [verilerle yanıt soru](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sn)*</span><span class="sxs-lookup"><span data-stu-id="82de0-115">Video 3: [Ask a question you can answer with data](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*</span></span>
* <span data-ttu-id="82de0-116">Video 4: [basit bir modelle bir yanıt tahmin](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sn)*</span><span class="sxs-lookup"><span data-stu-id="82de0-116">Video 4: [Predict an answer with a simple model](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*</span></span>
* <span data-ttu-id="82de0-117">Video 5: [veri bilimi yapmak için diğer kişilerin çalışma kopyalama](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 dakika 18 saniye)*</span><span class="sxs-lookup"><span data-stu-id="82de0-117">Video 5: [Copy other people's work to do data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span></span>

## <a name="transcript-is-your-data-ready-for-data-science"></a><span data-ttu-id="82de0-118">Dökümü: verileriniz için veri bilimi hazır mı?</span><span class="sxs-lookup"><span data-stu-id="82de0-118">Transcript: Is your data ready for data science?</span></span>
<span data-ttu-id="82de0-119">Hoş Geldiniz "verileriniz için veri bilimi hazır mı?"</span><span class="sxs-lookup"><span data-stu-id="82de0-119">Welcome to "Is your data ready for data science?"</span></span> <span data-ttu-id="82de0-120">serideki ikinci video *yeni başlayanlar için veri bilimi*.</span><span class="sxs-lookup"><span data-stu-id="82de0-120">the second video in the series *Data Science for Beginners*.</span></span>  

<span data-ttu-id="82de0-121">Veri bilimi istediğiniz yanıt vermeden önce bazı yüksek kaliteli hammaddeleri çalışmak için vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="82de0-121">Before data science can give you the answers you want, you have to give it some high-quality raw materials to work with.</span></span> <span data-ttu-id="82de0-122">Daha iyi bir pizza daha iyi son ürünle, başlangıç malzemeleri yalnızca yapma gibi.</span><span class="sxs-lookup"><span data-stu-id="82de0-122">Just like making a pizza, the better the ingredients you start with, the better the final product.</span></span> 

## <a name="criteria-for-data"></a><span data-ttu-id="82de0-123">Veriler için ölçüt</span><span class="sxs-lookup"><span data-stu-id="82de0-123">Criteria for data</span></span>
<span data-ttu-id="82de0-124">Bu nedenle, veri bilimi durumunda birlikte çıkarmak için ihtiyacımız bazı malzemeleri vardır.</span><span class="sxs-lookup"><span data-stu-id="82de0-124">So, in the case of data science, there are some ingredients that we need to pull together.</span></span>

<span data-ttu-id="82de0-125">Verileri ihtiyacımız var:</span><span class="sxs-lookup"><span data-stu-id="82de0-125">We need data that is:</span></span>

* <span data-ttu-id="82de0-126">İlgili</span><span class="sxs-lookup"><span data-stu-id="82de0-126">Relevant</span></span>
* <span data-ttu-id="82de0-127">bağlı</span><span class="sxs-lookup"><span data-stu-id="82de0-127">Connected</span></span>
* <span data-ttu-id="82de0-128">Doğru</span><span class="sxs-lookup"><span data-stu-id="82de0-128">Accurate</span></span>
* <span data-ttu-id="82de0-129">Yeterli çalışmak için</span><span class="sxs-lookup"><span data-stu-id="82de0-129">Enough to work with</span></span>

## <a name="is-your-data-relevant"></a><span data-ttu-id="82de0-130">Verilerinizi ilgili mi?</span><span class="sxs-lookup"><span data-stu-id="82de0-130">Is your data relevant?</span></span>
<span data-ttu-id="82de0-131">Bu nedenle ilk tarifi - ilgili olan verileri ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="82de0-131">So the first ingredient - we need data that's relevant.</span></span>

![İlgili verileri ilgisiz verilerin - karşılaştırması veri değerlendir](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/relevant-and-irrelevant-data.png)

<span data-ttu-id="82de0-133">Sol tarafta tabloya bakın.</span><span class="sxs-lookup"><span data-stu-id="82de0-133">Look at the table on the left.</span></span> <span data-ttu-id="82de0-134">Biz Boston çubukları dışında yedi kişi yerine, kan Alkol düzeylerini, son kullanıcıların oyun kırmızı Sox batting ortalama ve en yakın Market sütlü fiyat ölçülür.</span><span class="sxs-lookup"><span data-stu-id="82de0-134">We met seven people outside of Boston bars, measured their blood alcohol level, the Red Sox batting average in their last game, and the price of milk in the nearest convenience store.</span></span>

<span data-ttu-id="82de0-135">Bu tüm mükemmel yasal verilerdir.</span><span class="sxs-lookup"><span data-stu-id="82de0-135">This is all perfectly legitimate data.</span></span> <span data-ttu-id="82de0-136">İlgili değil, yalnızca hataya değildir.</span><span class="sxs-lookup"><span data-stu-id="82de0-136">It’s only fault is that it isn’t relevant.</span></span> <span data-ttu-id="82de0-137">Bu sayılar arasında belirgin ilişkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="82de0-137">There's no obvious relationship between these numbers.</span></span> <span data-ttu-id="82de0-138">I sütlü ve kırmızı Sox batting ortalama geçerli fiyat vermiş, kan Alkol İçeriğim tahmin edebilir yolu yoktur.</span><span class="sxs-lookup"><span data-stu-id="82de0-138">If I gave you the current price of milk and the Red Sox batting average, there's no way you could guess my blood alcohol content.</span></span>

<span data-ttu-id="82de0-139">Şimdi sağ tarafta tabloya bakın.</span><span class="sxs-lookup"><span data-stu-id="82de0-139">Now look at the table on the right.</span></span> <span data-ttu-id="82de0-140">Bu süre, biz ölçülen her birinin gövde yığın ve sayılan sahip oldukları İçecekler sayısı.</span><span class="sxs-lookup"><span data-stu-id="82de0-140">This time we measured each person’s body mass and counted the number of drinks they’ve had.</span></span>  <span data-ttu-id="82de0-141">Her satır numaraları şimdi birbiriyle ilgili olur.</span><span class="sxs-lookup"><span data-stu-id="82de0-141">The numbers in each row are now relevant to each other.</span></span> <span data-ttu-id="82de0-142">I size my gövde verdiyse yığın ve ı vardı Margaritas sayısı, yaptığınız my kan konumundaki tahmin Alkol içerik.</span><span class="sxs-lookup"><span data-stu-id="82de0-142">If I gave you my body mass and the number of Margaritas I've had, you could make a guess at my blood alcohol content.</span></span>

## <a name="do-you-have-connected-data"></a><span data-ttu-id="82de0-143">Sahip bağlı veri?</span><span class="sxs-lookup"><span data-stu-id="82de0-143">Do you have connected data?</span></span>
<span data-ttu-id="82de0-144">Sonraki tarifi bağlı verilerdir.</span><span class="sxs-lookup"><span data-stu-id="82de0-144">The next ingredient is connected data.</span></span>

![Bağlı veri bağlantısı kesilmiş verileri - veri ölçütlerini hazır karşılaştırması](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/connected-vs-disconnected-data.png)

<span data-ttu-id="82de0-146">Hamburgers kalitesini bazı ilgili bilgiler aşağıdadır: sıcaklık, patty ağırlık ve dergi yerel yemek derecesi maske.</span><span class="sxs-lookup"><span data-stu-id="82de0-146">Here is some relevant data on the quality of hamburgers: grill temperature, patty weight, and rating in the local food magazine.</span></span> <span data-ttu-id="82de0-147">Ancak sol tablodaki boşlukları dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="82de0-147">But notice the gaps in the table on the left.</span></span>

<span data-ttu-id="82de0-148">Çoğu veri kümelerini bazı değerler eksik.</span><span class="sxs-lookup"><span data-stu-id="82de0-148">Most data sets are missing some values.</span></span> <span data-ttu-id="82de0-149">Böyle delik sağlamak için yaygın bir durumdur ve etrafında çalışmaya yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="82de0-149">It's common to have holes like this and there are ways to work around them.</span></span> <span data-ttu-id="82de0-150">Ancak, verilerinizi varsa çok fazla eksik, İsviçre Peynir gibi ara başlar.</span><span class="sxs-lookup"><span data-stu-id="82de0-150">But if there's too much missing, your data begins to look like Swiss cheese.</span></span>

<span data-ttu-id="82de0-151">Sol tarafta tabloya bakarsanız, olmadığından eksik kadar veri grill sıcaklık ve patty ağırlık ilişkiyi her türlü gündeme sabit.</span><span class="sxs-lookup"><span data-stu-id="82de0-151">If you look at the table on the left, there's so much missing data, it's hard to come up with any kind of relationship between grill temperature and patty weight.</span></span> <span data-ttu-id="82de0-152">Bu, bağlantısı kesilmiş veri örneğidir.</span><span class="sxs-lookup"><span data-stu-id="82de0-152">This is an example of disconnected data.</span></span>

<span data-ttu-id="82de0-153">Ancak sağ taraftaki tablo dolu olduğunda ve tamamlandı - bağlı veri örneği.</span><span class="sxs-lookup"><span data-stu-id="82de0-153">The table on the right, though, is full and complete - an example of connected data.</span></span>

## <a name="is-your-data-accurate"></a><span data-ttu-id="82de0-154">Verilerinizi geçerli mi?</span><span class="sxs-lookup"><span data-stu-id="82de0-154">Is your data accurate?</span></span>
<span data-ttu-id="82de0-155">İhtiyacımız sonraki tarifi doğruluğu ' dir.</span><span class="sxs-lookup"><span data-stu-id="82de0-155">The next ingredient we need is accuracy.</span></span> <span data-ttu-id="82de0-156">Oklarla isabet isteriz dört hedefleri şunlardır.</span><span class="sxs-lookup"><span data-stu-id="82de0-156">Here are four targets that we’d like to hit with arrows.</span></span>

![Doğru verileri yanlış data - veri ölçütlerini karşılaştırması](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/inaccurate-vs-accurate-data.png)

<span data-ttu-id="82de0-158">Sağ üst hedef bakın.</span><span class="sxs-lookup"><span data-stu-id="82de0-158">Look at the target in the upper right.</span></span> <span data-ttu-id="82de0-159">Biz sağ hedef merkezi etrafında sıkı bir gruplandırma açıyor.</span><span class="sxs-lookup"><span data-stu-id="82de0-159">We’ve got a tight grouping right around the bullseye.</span></span> <span data-ttu-id="82de0-160">Doğal olarak, doğru olur.</span><span class="sxs-lookup"><span data-stu-id="82de0-160">That, of course, is accurate.</span></span> <span data-ttu-id="82de0-161">Arasında veri bilimi dilde altındaki hedef sağdaki bizim performans da doğru olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="82de0-161">Oddly, in the language of data science, our performance on the target right below it is also considered accurate.</span></span>

<span data-ttu-id="82de0-162">Bu okları merkezi eşlemek için olsaydı, bu çok hedef merkezi yakın olduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="82de0-162">If you were to map out the center of these arrows, you'd see that it's very close to the bullseye.</span></span> <span data-ttu-id="82de0-163">Oklar, tüm hedef geçici kesin olmayan kabul ancak doğru kabul şekilde hedef merkezi ortalanmış yayılır.</span><span class="sxs-lookup"><span data-stu-id="82de0-163">The arrows are spread out all around the target, so they're considered imprecise, but they're centered around the bullseye, so they're considered accurate.</span></span>

<span data-ttu-id="82de0-164">Artık sol üst hedefe arayın.</span><span class="sxs-lookup"><span data-stu-id="82de0-164">Now look at the upper-left target.</span></span> <span data-ttu-id="82de0-165">Burada bizim okları çok birbirine sıkı bir gruplandırma ulaştı.</span><span class="sxs-lookup"><span data-stu-id="82de0-165">Here our arrows hit very close together, a tight grouping.</span></span> <span data-ttu-id="82de0-166">Kesin, ancak merkezi şekilde hedef merkezi devre dışı olduğundan, bunlar yanlış.</span><span class="sxs-lookup"><span data-stu-id="82de0-166">They're precise, but they're inaccurate because the center is way off the bullseye.</span></span> <span data-ttu-id="82de0-167">Ve Elbette, sol alt hedef okları yanlış ve kesin.</span><span class="sxs-lookup"><span data-stu-id="82de0-167">And, of course, the arrows in the bottom-left target are both inaccurate and imprecise.</span></span> <span data-ttu-id="82de0-168">Bu archer daha fazla uygulama gerekir.</span><span class="sxs-lookup"><span data-stu-id="82de0-168">This archer needs more practice.</span></span>

## <a name="do-you-have-enough-data-to-work-with"></a><span data-ttu-id="82de0-169">Çalışmak için yeterli veri var mı?</span><span class="sxs-lookup"><span data-stu-id="82de0-169">Do you have enough data to work with?</span></span>
<span data-ttu-id="82de0-170">Son olarak, malzeme #4 - biz yeterli veri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="82de0-170">Finally, ingredient #4 - we need to have enough data.</span></span>

![Analiz için yeterli veri var mı?](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/barely-enough-data.png)

<span data-ttu-id="82de0-173">Her veri noktası tablosundaki boyama içinde fırça vuruş olarak düşünün.</span><span class="sxs-lookup"><span data-stu-id="82de0-173">Think of each data point in your table as being a brush stroke in a painting.</span></span> <span data-ttu-id="82de0-174">Yalnızca birkaç tanesi varsa, boyama oldukça benzer - ne olduğunu ayırt etmek zordur.</span><span class="sxs-lookup"><span data-stu-id="82de0-174">If you have only a few of them, the painting can be pretty fuzzy - it's hard to tell what it is.</span></span>

<span data-ttu-id="82de0-175">Daha fazla bazı fırça vuruşları eklerseniz, boyama biraz daha net alma başlar.</span><span class="sxs-lookup"><span data-stu-id="82de0-175">If you add some more brush strokes, then your painting starts to get a little sharper.</span></span>

<span data-ttu-id="82de0-176">Neredeyse hiç yeterli vuruşları olduğunda yetecek kadar geniş bazı kararlar almak için görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82de0-176">When you have barely enough strokes, you can see just enough to make some broad decisions.</span></span> <span data-ttu-id="82de0-177">Bu bir yere ziyaret etmek istediğiniz mi?</span><span class="sxs-lookup"><span data-stu-id="82de0-177">Is it somewhere I might want to visit?</span></span> <span data-ttu-id="82de0-178">Açık görünüyor, temiz su gibi – Evet, burada tatile kullanacağım olan arar.</span><span class="sxs-lookup"><span data-stu-id="82de0-178">It looks bright, that looks like clean water – yes, that’s where I’m going on vacation.</span></span>

<span data-ttu-id="82de0-179">Daha fazla veri ekleme gibi resmi daha anlaşılır olur ve daha ayrıntılı kararlarını verebilir.</span><span class="sxs-lookup"><span data-stu-id="82de0-179">As you add more data, the picture becomes clearer and you can make more detailed decisions.</span></span> <span data-ttu-id="82de0-180">Artık sol bank üzerinde üç Oteller adresindeki gözden geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82de0-180">Now I can look at the three hotels on the left bank.</span></span> <span data-ttu-id="82de0-181">Bildiğiniz ı gerçekten mimari ön planda biri gibi özellikler.</span><span class="sxs-lookup"><span data-stu-id="82de0-181">You know, I really like the architectural features of the one in the foreground.</span></span> <span data-ttu-id="82de0-182">Üçüncü kat üzerinde kalır,.</span><span class="sxs-lookup"><span data-stu-id="82de0-182">I’ll stay there, on the third floor.</span></span>

<span data-ttu-id="82de0-183">İlgili, bağlı, doğru veri ve yeterli, biz ile sahip ihtiyacımız için tüm malzemeleri yapmak bazı yüksek kaliteli veri bilimi.</span><span class="sxs-lookup"><span data-stu-id="82de0-183">With data that's relevant, connected, accurate, and enough, we have all the ingredients we need to do some high-quality data science.</span></span>

<span data-ttu-id="82de0-184">Diğer dört videoları kullanıma özen *yeni başlayanlar için veri bilimi* Microsoft Azure Machine learning'in.</span><span class="sxs-lookup"><span data-stu-id="82de0-184">Be sure to check out the other four videos in *Data Science for Beginners* from Microsoft Azure Machine Learning.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82de0-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="82de0-185">Next steps</span></span>
* [<span data-ttu-id="82de0-186">İlk veri bilimi denemeyi Machine Learning Studio'da deneyin</span><span class="sxs-lookup"><span data-stu-id="82de0-186">Try a first data science experiment with Machine Learning Studio</span></span>](machine-learning-create-experiment.md)
* [<span data-ttu-id="82de0-187">Microsoft Azure Machine Learning giriş Al</span><span class="sxs-lookup"><span data-stu-id="82de0-187">Get an introduction to Machine Learning on Microsoft Azure</span></span>](machine-learning-what-is-machine-learning.md)
