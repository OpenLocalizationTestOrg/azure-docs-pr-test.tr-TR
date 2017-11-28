---
title: "aaaIs verilerinizi veri bilimi için hazır mısınız? Veri değerlendirmesi - Azure Machine Learning | Microsoft Docs"
description: "Veri toobe veri bilimi için hazır Hello 4 ölçütlerine öğrenin. Veri bilimi video 2 yeni başlayanlar için temel veri değerlendirme ile somut örnekler toohelp sahiptir."
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
ms.openlocfilehash: ef6bb680ace771537157dbdd50a4ccce0a3eb7ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="is-your-data-ready-for-data-science"></a><span data-ttu-id="48733-106">Verileriniz veri bilimi için hazır mı?</span><span class="sxs-lookup"><span data-stu-id="48733-106">Is your data ready for data science?</span></span>
## <a name="video-2-data-science-for-beginners-series"></a><span data-ttu-id="48733-107">Video 2: Veri bilimi yeni başlayanlar seri için</span><span class="sxs-lookup"><span data-stu-id="48733-107">Video 2: Data Science for Beginners series</span></span>
<span data-ttu-id="48733-108">Bilgi nasıl tooevaluate temel ölçütleri toobe veri bilimi için hazır karşıladığından emin, veri toomake.</span><span class="sxs-lookup"><span data-stu-id="48733-108">Learn how tooevaluate your data toomake sure it meets basic criteria toobe ready for data science.</span></span>

<span data-ttu-id="48733-109">tooget hello en hello serisi dışında tümünü izleyin.</span><span class="sxs-lookup"><span data-stu-id="48733-109">tooget hello most out of hello series, watch them all.</span></span> <span data-ttu-id="48733-110">[Videolar toohello listesi gidin](#other-videos-in-this-series)
</span><span class="sxs-lookup"><span data-stu-id="48733-110">[Go toohello list of videos](#other-videos-in-this-series)
</span></span><br>

> [!VIDEO https://channel9.msdn.com/Shows/SupervisionNotRequired/9/player]
>
>

## <a name="other-videos-in-this-series"></a><span data-ttu-id="48733-111">Bu serideki diğer videolar</span><span class="sxs-lookup"><span data-stu-id="48733-111">Other videos in this series</span></span>
<span data-ttu-id="48733-112">*Yeni başlayanlar için veri bilimi* beş kısa video içinde hızlı giriş toodata bilimsel olduğu.</span><span class="sxs-lookup"><span data-stu-id="48733-112">*Data Science for Beginners* is a quick introduction toodata science in five short videos.</span></span>

* <span data-ttu-id="48733-113">Video 1: [hello 5 sorular veri bilimi yanıtlar](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 dakika 14 saniye)*</span><span class="sxs-lookup"><span data-stu-id="48733-113">Video 1: [hello 5 questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span></span>
* <span data-ttu-id="48733-114">Video 2: verileriniz için veri bilimi hazır mı?</span><span class="sxs-lookup"><span data-stu-id="48733-114">Video 2: Is your data ready for data science?</span></span>
* <span data-ttu-id="48733-115">Video 3: [verilerle yanıt soru](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sn)*</span><span class="sxs-lookup"><span data-stu-id="48733-115">Video 3: [Ask a question you can answer with data](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*</span></span>
* <span data-ttu-id="48733-116">Video 4: [basit bir modelle bir yanıt tahmin](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sn)*</span><span class="sxs-lookup"><span data-stu-id="48733-116">Video 4: [Predict an answer with a simple model](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*</span></span>
* <span data-ttu-id="48733-117">Video 5: [diğer kişilerin çalışma toodo veri bilimi kopyalama](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 dakika 18 saniye)*</span><span class="sxs-lookup"><span data-stu-id="48733-117">Video 5: [Copy other people's work toodo data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span></span>

## <a name="transcript-is-your-data-ready-for-data-science"></a><span data-ttu-id="48733-118">Dökümü: verileriniz için veri bilimi hazır mı?</span><span class="sxs-lookup"><span data-stu-id="48733-118">Transcript: Is your data ready for data science?</span></span>
<span data-ttu-id="48733-119">Hoş Geldiniz çok "verileriniz için veri bilimi hazır mı?"</span><span class="sxs-lookup"><span data-stu-id="48733-119">Welcome too"Is your data ready for data science?"</span></span> <span data-ttu-id="48733-120">İkinci video hello serideki hello *yeni başlayanlar için veri bilimi*.</span><span class="sxs-lookup"><span data-stu-id="48733-120">hello second video in hello series *Data Science for Beginners*.</span></span>  

<span data-ttu-id="48733-121">Veri bilimi vermeden önce istediğiniz yanıtlar Merhaba, toogive sahip, bazı yüksek kaliteli hammaddeleri toowork ile.</span><span class="sxs-lookup"><span data-stu-id="48733-121">Before data science can give you hello answers you want, you have toogive it some high-quality raw materials toowork with.</span></span> <span data-ttu-id="48733-122">Yalnızca bir pizza yapma gibi başlangıç hello daha iyi hello malzemeleri hello daha iyi hello son ürün.</span><span class="sxs-lookup"><span data-stu-id="48733-122">Just like making a pizza, hello better hello ingredients you start with, hello better hello final product.</span></span> 

## <a name="criteria-for-data"></a><span data-ttu-id="48733-123">Veriler için ölçüt</span><span class="sxs-lookup"><span data-stu-id="48733-123">Criteria for data</span></span>
<span data-ttu-id="48733-124">Bu nedenle, veri bilimi hello durumda biz toopull birlikte gereken bazı malzemeleri vardır.</span><span class="sxs-lookup"><span data-stu-id="48733-124">So, in hello case of data science, there are some ingredients that we need toopull together.</span></span>

<span data-ttu-id="48733-125">Verileri ihtiyacımız var:</span><span class="sxs-lookup"><span data-stu-id="48733-125">We need data that is:</span></span>

* <span data-ttu-id="48733-126">İlgili</span><span class="sxs-lookup"><span data-stu-id="48733-126">Relevant</span></span>
* <span data-ttu-id="48733-127">bağlı</span><span class="sxs-lookup"><span data-stu-id="48733-127">Connected</span></span>
* <span data-ttu-id="48733-128">Doğru</span><span class="sxs-lookup"><span data-stu-id="48733-128">Accurate</span></span>
* <span data-ttu-id="48733-129">Yeterli toowork ile</span><span class="sxs-lookup"><span data-stu-id="48733-129">Enough toowork with</span></span>

## <a name="is-your-data-relevant"></a><span data-ttu-id="48733-130">Verilerinizi ilgili mi?</span><span class="sxs-lookup"><span data-stu-id="48733-130">Is your data relevant?</span></span>
<span data-ttu-id="48733-131">Bu nedenle hello ilk tarifi - ilgili olan verileri ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="48733-131">So hello first ingredient - we need data that's relevant.</span></span>

![İlgili verileri ilgisiz verilerin - karşılaştırması veri değerlendir](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/relevant-and-irrelevant-data.png)

<span data-ttu-id="48733-133">Merhaba tablosunda hello solda arayın.</span><span class="sxs-lookup"><span data-stu-id="48733-133">Look at hello table on hello left.</span></span> <span data-ttu-id="48733-134">Biz Boston çubukları dışında yedi kişi yerine, kendi kan Alkol düzeyi, son kullanıcıların oyun hello kırmızı Sox batting ortalama ve Market en yakın hello sütlü hello fiyatını ölçülür.</span><span class="sxs-lookup"><span data-stu-id="48733-134">We met seven people outside of Boston bars, measured their blood alcohol level, hello Red Sox batting average in their last game, and hello price of milk in hello nearest convenience store.</span></span>

<span data-ttu-id="48733-135">Bu tüm mükemmel yasal verilerdir.</span><span class="sxs-lookup"><span data-stu-id="48733-135">This is all perfectly legitimate data.</span></span> <span data-ttu-id="48733-136">İlgili değil, yalnızca hataya değildir.</span><span class="sxs-lookup"><span data-stu-id="48733-136">It’s only fault is that it isn’t relevant.</span></span> <span data-ttu-id="48733-137">Bu sayılar arasında belirgin ilişkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="48733-137">There's no obvious relationship between these numbers.</span></span> <span data-ttu-id="48733-138">I verdiyse sütlü ve hello kırmızı Sox batting ortalama geçerli fiyat Merhaba, kan Alkol İçeriğim tahmin bir yolu yoktur.</span><span class="sxs-lookup"><span data-stu-id="48733-138">If I gave you hello current price of milk and hello Red Sox batting average, there's no way you could guess my blood alcohol content.</span></span>

<span data-ttu-id="48733-139">Şimdi hello sağ hello tablosuna bakın.</span><span class="sxs-lookup"><span data-stu-id="48733-139">Now look at hello table on hello right.</span></span> <span data-ttu-id="48733-140">Bu süre her birinin gövde yığın ve sayılan hello sahip İçecekler sayısı ölçülür.</span><span class="sxs-lookup"><span data-stu-id="48733-140">This time we measured each person’s body mass and counted hello number of drinks they’ve had.</span></span>  <span data-ttu-id="48733-141">Her satırda Hello numaraları diğer ilgili tooeach sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="48733-141">hello numbers in each row are now relevant tooeach other.</span></span> <span data-ttu-id="48733-142">I size my gövde yığın ve hello sayısı sahip Margaritas verdiyse, my kan konumundaki tahmin Alkol içerik hale getirebilir.</span><span class="sxs-lookup"><span data-stu-id="48733-142">If I gave you my body mass and hello number of Margaritas I've had, you could make a guess at my blood alcohol content.</span></span>

## <a name="do-you-have-connected-data"></a><span data-ttu-id="48733-143">Sahip bağlı veri?</span><span class="sxs-lookup"><span data-stu-id="48733-143">Do you have connected data?</span></span>
<span data-ttu-id="48733-144">Merhaba sonraki tarifi bağlı verilerdir.</span><span class="sxs-lookup"><span data-stu-id="48733-144">hello next ingredient is connected data.</span></span>

![Bağlı veri bağlantısı kesilmiş verileri - veri ölçütlerini hazır karşılaştırması](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/connected-vs-disconnected-data.png)

<span data-ttu-id="48733-146">Hamburgers hello kalitesini bazı ilgili bilgiler aşağıdadır: sıcaklık, patty ağırlık ve hello yerel yemek dergi derecesi maske.</span><span class="sxs-lookup"><span data-stu-id="48733-146">Here is some relevant data on hello quality of hamburgers: grill temperature, patty weight, and rating in hello local food magazine.</span></span> <span data-ttu-id="48733-147">Ancak hello boşluklar hello soldaki hello tablosundaki dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="48733-147">But notice hello gaps in hello table on hello left.</span></span>

<span data-ttu-id="48733-148">Çoğu veri kümelerini bazı değerler eksik.</span><span class="sxs-lookup"><span data-stu-id="48733-148">Most data sets are missing some values.</span></span> <span data-ttu-id="48733-149">Bu gibi ortak toohave delik olduğunu ve yolları toowork etrafında.</span><span class="sxs-lookup"><span data-stu-id="48733-149">It's common toohave holes like this and there are ways toowork around them.</span></span> <span data-ttu-id="48733-150">Ancak çok fazla eksik olduğundan, verilerinizi İsviçre Peynir gibi toolook başlar.</span><span class="sxs-lookup"><span data-stu-id="48733-150">But if there's too much missing, your data begins toolook like Swiss cheese.</span></span>

<span data-ttu-id="48733-151">Merhaba solda hello tablosunda bakarsanız, olmadığından arasındaki ilişkiyi her türlü ile yukarı sabit toocome olduğu kadar eksik veri maske sıcaklık ve patty ağırlık.</span><span class="sxs-lookup"><span data-stu-id="48733-151">If you look at hello table on hello left, there's so much missing data, it's hard toocome up with any kind of relationship between grill temperature and patty weight.</span></span> <span data-ttu-id="48733-152">Bu, bağlantısı kesilmiş veri örneğidir.</span><span class="sxs-lookup"><span data-stu-id="48733-152">This is an example of disconnected data.</span></span>

<span data-ttu-id="48733-153">Merhaba sağ taraftaki tablo ancak Merhaba, tam ve tamamlandı - bağlı veri örneği.</span><span class="sxs-lookup"><span data-stu-id="48733-153">hello table on hello right, though, is full and complete - an example of connected data.</span></span>

## <a name="is-your-data-accurate"></a><span data-ttu-id="48733-154">Verilerinizi geçerli mi?</span><span class="sxs-lookup"><span data-stu-id="48733-154">Is your data accurate?</span></span>
<span data-ttu-id="48733-155">Merhaba ihtiyacımız sonraki tarifi doğruluğu olur.</span><span class="sxs-lookup"><span data-stu-id="48733-155">hello next ingredient we need is accuracy.</span></span> <span data-ttu-id="48733-156">Burada, dört hedefleri oklarla toohit isteriz bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="48733-156">Here are four targets that we’d like toohit with arrows.</span></span>

![Doğru verileri yanlış data - veri ölçütlerini karşılaştırması](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/inaccurate-vs-accurate-data.png)

<span data-ttu-id="48733-158">Sağ üstteki hello hello hedef bakın.</span><span class="sxs-lookup"><span data-stu-id="48733-158">Look at hello target in hello upper right.</span></span> <span data-ttu-id="48733-159">Biz sağ hello hedef merkezi etrafında sıkı bir gruplandırma açıyor.</span><span class="sxs-lookup"><span data-stu-id="48733-159">We’ve got a tight grouping right around hello bullseye.</span></span> <span data-ttu-id="48733-160">Doğal olarak, doğru olur.</span><span class="sxs-lookup"><span data-stu-id="48733-160">That, of course, is accurate.</span></span> <span data-ttu-id="48733-161">Arasında veri bilimi hello dilde hello hedef hemen altındaki bizim performans da doğru olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="48733-161">Oddly, in hello language of data science, our performance on hello target right below it is also considered accurate.</span></span>

<span data-ttu-id="48733-162">Bu okları hello merkezi çıkışı toomap olsaydı, çok yakın toohello hedef merkezi olduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="48733-162">If you were toomap out hello center of these arrows, you'd see that it's very close toohello bullseye.</span></span> <span data-ttu-id="48733-163">Merhaba okları kesin olmayan kabul ancak doğru kabul şekilde hello hedef merkezi ortalanmış tüm hello hedef, geçici yayılır.</span><span class="sxs-lookup"><span data-stu-id="48733-163">hello arrows are spread out all around hello target, so they're considered imprecise, but they're centered around hello bullseye, so they're considered accurate.</span></span>

<span data-ttu-id="48733-164">Şimdi hello sol üst hedefe arayın.</span><span class="sxs-lookup"><span data-stu-id="48733-164">Now look at hello upper-left target.</span></span> <span data-ttu-id="48733-165">Burada bizim okları çok birbirine sıkı bir gruplandırma ulaştı.</span><span class="sxs-lookup"><span data-stu-id="48733-165">Here our arrows hit very close together, a tight grouping.</span></span> <span data-ttu-id="48733-166">Kesin ancak hello merkezi şekilde hello hedef merkezi devre dışı olduğundan, bunlar yanlış.</span><span class="sxs-lookup"><span data-stu-id="48733-166">They're precise, but they're inaccurate because hello center is way off hello bullseye.</span></span> <span data-ttu-id="48733-167">Ve Elbette, hello sol alt hedef hello okları yanlış ve kesin.</span><span class="sxs-lookup"><span data-stu-id="48733-167">And, of course, hello arrows in hello bottom-left target are both inaccurate and imprecise.</span></span> <span data-ttu-id="48733-168">Bu archer daha fazla uygulama gerekir.</span><span class="sxs-lookup"><span data-stu-id="48733-168">This archer needs more practice.</span></span>

## <a name="do-you-have-enough-data-toowork-with"></a><span data-ttu-id="48733-169">Yeterli veri toowork ile var mı?</span><span class="sxs-lookup"><span data-stu-id="48733-169">Do you have enough data toowork with?</span></span>
<span data-ttu-id="48733-170">Son olarak, malzeme #4 - yeterli veri toohave ihtiyacımız.</span><span class="sxs-lookup"><span data-stu-id="48733-170">Finally, ingredient #4 - we need toohave enough data.</span></span>

![Analiz için yeterli veri var mı?](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/barely-enough-data.png)

<span data-ttu-id="48733-173">Her veri noktası tablosundaki boyama içinde fırça vuruş olarak düşünün.</span><span class="sxs-lookup"><span data-stu-id="48733-173">Think of each data point in your table as being a brush stroke in a painting.</span></span> <span data-ttu-id="48733-174">Yalnızca birkaç tanesi sahip, hello boyama oldukça benzer olabilir - sabit tootell olup olmadığını nedir.</span><span class="sxs-lookup"><span data-stu-id="48733-174">If you have only a few of them, hello painting can be pretty fuzzy - it's hard tootell what it is.</span></span>

<span data-ttu-id="48733-175">Daha fazla bazı fırça vuruşları eklerseniz, boyama tooget biraz daha keskin başlatır.</span><span class="sxs-lookup"><span data-stu-id="48733-175">If you add some more brush strokes, then your painting starts tooget a little sharper.</span></span>

<span data-ttu-id="48733-176">Neredeyse hiç yeterli vuruşları sahip olduğunuzda, bazı geniş kararları yeterli toomake görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48733-176">When you have barely enough strokes, you can see just enough toomake some broad decisions.</span></span> <span data-ttu-id="48733-177">Bu bir yere toovisit istediğiniz mi?</span><span class="sxs-lookup"><span data-stu-id="48733-177">Is it somewhere I might want toovisit?</span></span> <span data-ttu-id="48733-178">Açık görünüyor, temiz su gibi – Evet, burada tatile kullanacağım olan arar.</span><span class="sxs-lookup"><span data-stu-id="48733-178">It looks bright, that looks like clean water – yes, that’s where I’m going on vacation.</span></span>

<span data-ttu-id="48733-179">Daha fazla veri ekleme gibi hello resim daha anlaşılır olur ve daha ayrıntılı kararlarını verebilir.</span><span class="sxs-lookup"><span data-stu-id="48733-179">As you add more data, hello picture becomes clearer and you can make more detailed decisions.</span></span> <span data-ttu-id="48733-180">Merhaba hello sol bank üzerinde üç Oteller şimdi bakabilirim.</span><span class="sxs-lookup"><span data-stu-id="48733-180">Now I can look at hello three hotels on hello left bank.</span></span> <span data-ttu-id="48733-181">Bildiğiniz ı gerçekten hello mimari hello ön planda hello özelliklerini ister.</span><span class="sxs-lookup"><span data-stu-id="48733-181">You know, I really like hello architectural features of hello one in hello foreground.</span></span> <span data-ttu-id="48733-182">Merhaba üçüncü kat üzerinde kalır,.</span><span class="sxs-lookup"><span data-stu-id="48733-182">I’ll stay there, on hello third floor.</span></span>

<span data-ttu-id="48733-183">İlgili, bağlı, doğru verilerle ve yeterli, tüm hello malzemeleri ihtiyacımız toodo bazı yüksek kaliteli veri bilimi sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="48733-183">With data that's relevant, connected, accurate, and enough, we have all hello ingredients we need toodo some high-quality data science.</span></span>

<span data-ttu-id="48733-184">Diğer dört videoları hello çıkışı emin toocheck olması *yeni başlayanlar için veri bilimi* Microsoft Azure Machine learning'in.</span><span class="sxs-lookup"><span data-stu-id="48733-184">Be sure toocheck out hello other four videos in *Data Science for Beginners* from Microsoft Azure Machine Learning.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48733-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="48733-185">Next steps</span></span>
* [<span data-ttu-id="48733-186">İlk veri bilimi denemeyi Machine Learning Studio'da deneyin</span><span class="sxs-lookup"><span data-stu-id="48733-186">Try a first data science experiment with Machine Learning Studio</span></span>](machine-learning-create-experiment.md)
* [<span data-ttu-id="48733-187">Bir giriş tooMachine alma Microsoft Azure üzerinde öğrenme</span><span class="sxs-lookup"><span data-stu-id="48733-187">Get an introduction tooMachine Learning on Microsoft Azure</span></span>](machine-learning-what-is-machine-learning.md)
