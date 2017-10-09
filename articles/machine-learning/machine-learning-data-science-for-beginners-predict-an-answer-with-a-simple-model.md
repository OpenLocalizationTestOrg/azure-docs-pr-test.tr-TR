---
title: "aaaPredict basit regresyon modeli - Azure Machine Learning ile bir yanıt | Microsoft Docs"
description: "Nasıl toocreate basit bir regresyon modeli toopredict veri bilimi video 4 yeni başlayanlar için bir fiyat. Hedef verilerle doğrusal regresyon içerir."
keywords: "bir model, basit modeli, fiyat tahmini, basit regresyon modeli oluşturma"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: a28f1fab-e2d8-4663-aa7d-ca3530c8b525
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: d4270c2237c33b7e898b78a08b292bc9d62e49ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="predict-an-answer-with-a-simple-model"></a><span data-ttu-id="65f3b-105">Basit model ile yanıtı tahmin etme</span><span class="sxs-lookup"><span data-stu-id="65f3b-105">Predict an answer with a simple model</span></span>
## <a name="video-4-data-science-for-beginners-series"></a><span data-ttu-id="65f3b-106">Video 4: Yeni başlayanlar seri için veri bilimi</span><span class="sxs-lookup"><span data-stu-id="65f3b-106">Video 4: Data Science for Beginners series</span></span>
<span data-ttu-id="65f3b-107">Nasıl toocreate basit regresyon modeli toopredict hello veri bilimi video 4 yeni başlayanlar için de bir Karo bedelinin öğrenin.</span><span class="sxs-lookup"><span data-stu-id="65f3b-107">Learn how toocreate a simple regression model toopredict hello price of a diamond in Data Science for Beginners video 4.</span></span> <span data-ttu-id="65f3b-108">Biz hedef verilerle bir regresyon modeli çekersiniz.</span><span class="sxs-lookup"><span data-stu-id="65f3b-108">We'll draw a regression model with target data.</span></span>

<span data-ttu-id="65f3b-109">tooget hello en hello serisi dışında tümünü izleyin.</span><span class="sxs-lookup"><span data-stu-id="65f3b-109">tooget hello most out of hello series, watch them all.</span></span> <span data-ttu-id="65f3b-110">[Videolar toohello listesi gidin](#other-videos-in-this-series)
</span><span class="sxs-lookup"><span data-stu-id="65f3b-110">[Go toohello list of videos](#other-videos-in-this-series)
</span></span><br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/data-science-for-beginners-series-predict-an-answer-with-a-simple-model/player]
>
>

## <a name="other-videos-in-this-series"></a><span data-ttu-id="65f3b-111">Bu serideki diğer videolar</span><span class="sxs-lookup"><span data-stu-id="65f3b-111">Other videos in this series</span></span>
<span data-ttu-id="65f3b-112">*Yeni başlayanlar için veri bilimi* beş kısa video içinde hızlı giriş toodata bilimsel olduğu.</span><span class="sxs-lookup"><span data-stu-id="65f3b-112">*Data Science for Beginners* is a quick introduction toodata science in five short videos.</span></span>

* <span data-ttu-id="65f3b-113">Video 1: [hello 5 sorular veri bilimi yanıtlar](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 dakika 14 saniye)*</span><span class="sxs-lookup"><span data-stu-id="65f3b-113">Video 1: [hello 5 questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span></span>
* <span data-ttu-id="65f3b-114">Video 2: [verileriniz için veri bilimi hazır?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span><span class="sxs-lookup"><span data-stu-id="65f3b-114">Video 2: [Is your data ready for data science?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span></span> <span data-ttu-id="65f3b-115">*(4 min 56 sn)*</span><span class="sxs-lookup"><span data-stu-id="65f3b-115">*(4 min 56 sec)*</span></span>
* <span data-ttu-id="65f3b-116">Video 3: [verilerle yanıt soru](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sn)*</span><span class="sxs-lookup"><span data-stu-id="65f3b-116">Video 3: [Ask a question you can answer with data](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*</span></span>
* <span data-ttu-id="65f3b-117">Video 4: basit bir modelle bir yanıt tahmin etme</span><span class="sxs-lookup"><span data-stu-id="65f3b-117">Video 4: Predict an answer with a simple model</span></span>
* <span data-ttu-id="65f3b-118">Video 5: [diğer kişilerin çalışma toodo veri bilimi kopyalama](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 dakika 18 saniye)*</span><span class="sxs-lookup"><span data-stu-id="65f3b-118">Video 5: [Copy other people's work toodo data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span></span>

## <a name="transcript-predict-an-answer-with-a-simple-model"></a><span data-ttu-id="65f3b-119">Dökümü: basit bir modelle bir yanıt tahmin</span><span class="sxs-lookup"><span data-stu-id="65f3b-119">Transcript: Predict an answer with a simple model</span></span>
<span data-ttu-id="65f3b-120">Merhaba "Veri bilimi için yeni başlayanlar" serisi dördüncü video toohello Hoş Geldiniz.</span><span class="sxs-lookup"><span data-stu-id="65f3b-120">Welcome toohello fourth video in hello "Data Science for Beginners" series.</span></span> <span data-ttu-id="65f3b-121">Bunu, biz basit bir model oluşturmak ve tahminde bulunmak.</span><span class="sxs-lookup"><span data-stu-id="65f3b-121">In this one, we'll build a simple model and make a prediction.</span></span>

<span data-ttu-id="65f3b-122">A *modeli* verilerimizi ilgili basitleştirilmiş bir öykü olduğu.</span><span class="sxs-lookup"><span data-stu-id="65f3b-122">A *model* is a simplified story about our data.</span></span> <span data-ttu-id="65f3b-123">I ı anlamı göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="65f3b-123">I'll show you what I mean.</span></span>

## <a name="collect-relevant-accurate-connected-enough-data"></a><span data-ttu-id="65f3b-124">İlgili, doğru bağlı, yeterli veri toplama</span><span class="sxs-lookup"><span data-stu-id="65f3b-124">Collect relevant, accurate, connected, enough data</span></span>
<span data-ttu-id="65f3b-125">İçin bir Karo tooshop istiyorum söyleyin.</span><span class="sxs-lookup"><span data-stu-id="65f3b-125">Say I want tooshop for a diamond.</span></span> <span data-ttu-id="65f3b-126">Toomy adı 1,35 ayar elmas için bir ayar ile ait bir halka sahip ve tooget ne kadar maliyetlidir hakkında bir fikir istiyor.</span><span class="sxs-lookup"><span data-stu-id="65f3b-126">I have a ring that belonged toomy grandmother with a setting for a 1.35 carat diamond, and I want tooget an idea of how much it will cost.</span></span> <span data-ttu-id="65f3b-127">I not defteri ve Kalem hello mücevher deposuna alın ve ı hello fiyat tüm hello Karo hello çalışması ve ne kadar bunlar içinde carats tartmanız yazın.</span><span class="sxs-lookup"><span data-stu-id="65f3b-127">I take a notepad and pen into hello jewelry store, and I write down hello price of all of hello diamonds in hello case and how much they weigh in carats.</span></span> <span data-ttu-id="65f3b-128">Merhaba ilk baklava - cihazın 1.01 carats ve $7,366 başlatılıyor.</span><span class="sxs-lookup"><span data-stu-id="65f3b-128">Starting with hello first diamond - it's 1.01 carats and $7,366.</span></span>

<span data-ttu-id="65f3b-129">Şimdi geçtikleri ve diğer Karo hello deposundaki tüm Merhaba bunu.</span><span class="sxs-lookup"><span data-stu-id="65f3b-129">Now I go through and do this for all hello other diamonds in hello store.</span></span>

![Karo veri sütunlarının](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/diamond-data.png)

<span data-ttu-id="65f3b-131">Bizim listesi iki sütuna sahip olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="65f3b-131">Notice that our list has two columns.</span></span> <span data-ttu-id="65f3b-132">Farklı bir öznitelik her sütununda - ağırlık carats ve fiyat - her satırda tek bir Karo temsil eden bir tek veri noktası.</span><span class="sxs-lookup"><span data-stu-id="65f3b-132">Each column has a different attribute - weight in carats and price - and each row is a single data point that represents a single diamond.</span></span>

<span data-ttu-id="65f3b-133">Küçük bir gerçekte oluşturduk veri kümesi burada - bir tablo.</span><span class="sxs-lookup"><span data-stu-id="65f3b-133">We've actually created a small data set here - a table.</span></span> <span data-ttu-id="65f3b-134">Kalite bizim ölçütlerini karşılayan dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="65f3b-134">Notice that it meets our criteria for quality:</span></span>

* <span data-ttu-id="65f3b-135">Merhaba veri **ilgili** -ağırlığı olan kesinlikle ilgili tooprice</span><span class="sxs-lookup"><span data-stu-id="65f3b-135">hello data is **relevant** - weight is definitely related tooprice</span></span>
* <span data-ttu-id="65f3b-136">Bunun **doğru** -biz biz yazma hello fiyatlar yeniden denetlediniz</span><span class="sxs-lookup"><span data-stu-id="65f3b-136">It's **accurate** - we double-checked hello prices that we write down</span></span>
* <span data-ttu-id="65f3b-137">Bunun **bağlı** -boş boşluk yoktur ya bu sütunlar</span><span class="sxs-lookup"><span data-stu-id="65f3b-137">It's **connected** - there are no blank spaces in either of these columns</span></span>
* <span data-ttu-id="65f3b-138">Ve anlatıldığı gibi var. **yeterli** veri tooanswer bizim soru</span><span class="sxs-lookup"><span data-stu-id="65f3b-138">And, as we'll see, it's **enough** data tooanswer our question</span></span>

## <a name="ask-a-sharp-question"></a><span data-ttu-id="65f3b-139">NET bir soru sorun</span><span class="sxs-lookup"><span data-stu-id="65f3b-139">Ask a sharp question</span></span>
<span data-ttu-id="65f3b-140">Şimdi biz bizim soru NET bir şekilde neden: "ne kadar olacak toobuy 1,35 ayar elmas Maliyet?"</span><span class="sxs-lookup"><span data-stu-id="65f3b-140">Now we'll pose our question in a sharp way: "How much will it cost toobuy a 1.35 carat diamond?"</span></span>

<span data-ttu-id="65f3b-141">Biz toouse hello bizim veri tooget bir yanıt toohello soru geri kalanı gerekir böylece bizim listesi 1,35 ayar elmas içinde yok.</span><span class="sxs-lookup"><span data-stu-id="65f3b-141">Our list doesn't have a 1.35 carat diamond in it, so we'll have toouse hello rest of our data tooget an answer toohello question.</span></span>

## <a name="plot-hello-existing-data"></a><span data-ttu-id="65f3b-142">Merhaba mevcut verileri Çiz</span><span class="sxs-lookup"><span data-stu-id="65f3b-142">Plot hello existing data</span></span>
<span data-ttu-id="65f3b-143">Biz gerçekleştirirsiniz hello ilk toochart hello ağırlıkları eksen adlı yatay numarası çizgi, çizme şeydir.</span><span class="sxs-lookup"><span data-stu-id="65f3b-143">hello first thing we'll do is draw a horizontal number line, called an axis, toochart hello weights.</span></span> <span data-ttu-id="65f3b-144">Biz, aralık ve yarı her ayar için çizgilerine put kapsayan bir satır çekersiniz şekilde hello hello ağırlıkları 0 too2 aralığıdır.</span><span class="sxs-lookup"><span data-stu-id="65f3b-144">hello range of hello weights is 0 too2, so we'll draw a line that covers that range and put ticks for each half carat.</span></span>

<span data-ttu-id="65f3b-145">Sonraki dikey eksen toorecord hello fiyat çizme ve toohello yatay ağırlık eksen bağlanın.</span><span class="sxs-lookup"><span data-stu-id="65f3b-145">Next we'll draw a vertical axis toorecord hello price and connect it toohello horizontal weight axis.</span></span> <span data-ttu-id="65f3b-146">Bu, ABD Doları birimlerinde olacaktır.</span><span class="sxs-lookup"><span data-stu-id="65f3b-146">This will be in units of dollars.</span></span> <span data-ttu-id="65f3b-147">Şimdi biz koordinat eksenleri kümesine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="65f3b-147">Now we have a set of coordinate axes.</span></span>

![Ağırlık ve fiyat eksenler](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/weight-and-price-axes.png)

<span data-ttu-id="65f3b-149">Geçerli giderek tootake bu veriler artık, içine kapatma bir *dağılım çizim*.</span><span class="sxs-lookup"><span data-stu-id="65f3b-149">We're going tootake this data now and turn it into a *scatter plot*.</span></span> <span data-ttu-id="65f3b-150">Yo toovisualize sayısal veri kümelerini budur.</span><span class="sxs-lookup"><span data-stu-id="65f3b-150">This is a great way toovisualize numerical data sets.</span></span>

<span data-ttu-id="65f3b-151">Merhaba ilk veri noktası için bir dikey satırında 1.01 carats eyeball.</span><span class="sxs-lookup"><span data-stu-id="65f3b-151">For hello first data point, we eyeball a vertical line at 1.01 carats.</span></span> <span data-ttu-id="65f3b-152">Ardından, $7,366 yatay satırında eyeball.</span><span class="sxs-lookup"><span data-stu-id="65f3b-152">Then, we eyeball a horizontal line at $7,366.</span></span> <span data-ttu-id="65f3b-153">Karşıladıklarından burada size bir nokta çizin.</span><span class="sxs-lookup"><span data-stu-id="65f3b-153">Where they meet, we draw a dot.</span></span> <span data-ttu-id="65f3b-154">Bu bizim ilk elmas temsil eder.</span><span class="sxs-lookup"><span data-stu-id="65f3b-154">This represents our first diamond.</span></span>

<span data-ttu-id="65f3b-155">Şimdi Biz bu listede her elmas gidin ve aynı şeyi hello.</span><span class="sxs-lookup"><span data-stu-id="65f3b-155">Now we go through each diamond on this list and do hello same thing.</span></span> <span data-ttu-id="65f3b-156">Biz işiniz bittiğinde, biz alma budur: bir grup noktalar, her Karo.</span><span class="sxs-lookup"><span data-stu-id="65f3b-156">When we're through, this is what we get: a bunch of dots, one for each diamond.</span></span>

![Çizim dağılım](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/scatter-plot.png)

## <a name="draw-hello-model-through-hello-data-points"></a><span data-ttu-id="65f3b-158">Merhaba modeli hello veri noktaları aracılığıyla çizme</span><span class="sxs-lookup"><span data-stu-id="65f3b-158">Draw hello model through hello data points</span></span>
<span data-ttu-id="65f3b-159">Merhaba noktalar ve squint bakın, şimdi hello koleksiyonu fat, benzer bir satır gibi durur.</span><span class="sxs-lookup"><span data-stu-id="65f3b-159">Now if you look at hello dots and squint, hello collection looks like a fat, fuzzy line.</span></span> <span data-ttu-id="65f3b-160">Bizim işaret alın ve düz bir çizgi geçen çizin.</span><span class="sxs-lookup"><span data-stu-id="65f3b-160">We can take our marker and draw a straight line through it.</span></span>

<span data-ttu-id="65f3b-161">Oluşturduğumuz bir satır çizerek bir *modeli*.</span><span class="sxs-lookup"><span data-stu-id="65f3b-161">By drawing a line, we created a *model*.</span></span> <span data-ttu-id="65f3b-162">Bu hello gerçek dünya alma ve bir simplistic çizgi sürümü yaparak olarak düşünün.</span><span class="sxs-lookup"><span data-stu-id="65f3b-162">Think of this as taking hello real world and making a simplistic cartoon version of it.</span></span> <span data-ttu-id="65f3b-163">Şimdi hello çizgi yanlış - hello satır tüm hello veri noktaları aracılığıyla Git değil.</span><span class="sxs-lookup"><span data-stu-id="65f3b-163">Now hello cartoon is wrong - hello line doesn't go through all hello data points.</span></span> <span data-ttu-id="65f3b-164">Ancak yararlı basitleştirme değil.</span><span class="sxs-lookup"><span data-stu-id="65f3b-164">But, it's a useful simplification.</span></span>

![Doğrusal regresyon satır](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/linear-regression-line.png)

<span data-ttu-id="65f3b-166">Tüm hello nokta tam olarak hello hattı üzerinden geçmez, hello olgu normaldir.</span><span class="sxs-lookup"><span data-stu-id="65f3b-166">hello fact that all hello dots don't go exactly through hello line is OK.</span></span> <span data-ttu-id="65f3b-167">Veri bilimcilerine açıklayabilir bu hello model - hello satır - olduğunu söyleyerek ve ardından her nokta bazı sahip *gürültü* veya *farkı* kendisiyle ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="65f3b-167">Data scientists explain this by saying that there's hello model - that's hello line - and then each dot has some *noise* or *variance* associated with it.</span></span> <span data-ttu-id="65f3b-168">Mükemmel bir ilişki temel hello yoktur ve ardından gürültü ve belirsizlik ekler Merhaba Görünüşün, gerçek dünya yoktur.</span><span class="sxs-lookup"><span data-stu-id="65f3b-168">There's hello underlying perfect relationship, and then there's hello gritty, real world that adds noise and uncertainty.</span></span>

<span data-ttu-id="65f3b-169">Biz tooanswer hello soru çalıştığınızdan *ne kadar?* bu adlı bir *regresyon*.</span><span class="sxs-lookup"><span data-stu-id="65f3b-169">Because we're trying tooanswer hello question *How much?* this is called a *regression*.</span></span> <span data-ttu-id="65f3b-170">Ve bir çizgide kullanmakta olduğunuz çünkü bu bir *doğrusal regresyon*.</span><span class="sxs-lookup"><span data-stu-id="65f3b-170">And because we're using a straight line, it's a *linear regression*.</span></span>

## <a name="use-hello-model-toofind-hello-answer"></a><span data-ttu-id="65f3b-171">Merhaba modeli toofind hello yanıt kullanın</span><span class="sxs-lookup"><span data-stu-id="65f3b-171">Use hello model toofind hello answer</span></span>
<span data-ttu-id="65f3b-172">Bir model sahibiz ve biz bizim soru sorun artık: ne kadar 1,35 ayar elmas maliyetini?</span><span class="sxs-lookup"><span data-stu-id="65f3b-172">Now we have a model and we ask it our question: How much will a 1.35 carat diamond cost?</span></span>

<span data-ttu-id="65f3b-173">tooanswer bizim soru biz 1,35 carats göz Küresi ve de dikey çizgi çizme.</span><span class="sxs-lookup"><span data-stu-id="65f3b-173">tooanswer our question, we eyeball 1.35 carats and draw a vertical line.</span></span> <span data-ttu-id="65f3b-174">Merhaba model satır kestiği burada biz yatay çizgi toohello dolar eksen eyeball.</span><span class="sxs-lookup"><span data-stu-id="65f3b-174">Where it crosses hello model line, we eyeball a horizontal line toohello dollar axis.</span></span> <span data-ttu-id="65f3b-175">Sağ taraftaki 10.000 kadardır.</span><span class="sxs-lookup"><span data-stu-id="65f3b-175">It hits right at 10,000.</span></span> <span data-ttu-id="65f3b-176">Müzik!</span><span class="sxs-lookup"><span data-stu-id="65f3b-176">Boom!</span></span> <span data-ttu-id="65f3b-177">Merhaba yanıt olan: 1,35 ayar elmas yaklaşık 10.000 $ maliyetleri.</span><span class="sxs-lookup"><span data-stu-id="65f3b-177">That's hello answer: A 1.35 carat diamond costs about $10,000.</span></span>

![Merhaba yanıt hello model üzerinde Bul](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/find-the-answer.png)

## <a name="create-a-confidence-interval"></a><span data-ttu-id="65f3b-179">Güvenirlik aralığını oluşturma</span><span class="sxs-lookup"><span data-stu-id="65f3b-179">Create a confidence interval</span></span>
<span data-ttu-id="65f3b-180">Bu tahmin olduğunu nasıl kesin doğal toowonder olur.</span><span class="sxs-lookup"><span data-stu-id="65f3b-180">It's natural toowonder how precise this prediction is.</span></span> <span data-ttu-id="65f3b-181">Merhaba 1,35 ayar elmas çok çok yakın gerektirmeyeceğini yararlı tooknow olan $10.000 ya da çok daha yüksek veya düşük.</span><span class="sxs-lookup"><span data-stu-id="65f3b-181">It's useful tooknow whether hello 1.35 carat diamond will be very close too$10,000, or a lot higher or lower.</span></span> <span data-ttu-id="65f3b-182">toofigure bu çıkışı, şimdi hello nokta çoğunu içeren hello regresyon satırı geçici Zarf çizin.</span><span class="sxs-lookup"><span data-stu-id="65f3b-182">toofigure this out, let's draw an envelope around hello regression line that includes most of hello dots.</span></span> <span data-ttu-id="65f3b-183">Bu Zarf adlı bizim *güvenirlik aralığını*: biz çünkü fiyatlar bu Zarf içinde kalan oldukça emin hello geçmiş içinde bunların çoğu vardır.</span><span class="sxs-lookup"><span data-stu-id="65f3b-183">This envelope is called our *confidence interval*: We're pretty confident that prices fall within this envelope, because in hello past most of them have.</span></span> <span data-ttu-id="65f3b-184">Merhaba üst ve alt bu zarfın hello hello 1,35 ayar satır burada kestiği biz iki daha yatay çizgiler çizebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65f3b-184">We can draw two more horizontal lines from where hello 1.35 carat line crosses hello top and hello bottom of that envelope.</span></span>

![Güvenirlik aralığını](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/confidence-interval.png)

<span data-ttu-id="65f3b-186">Şimdi biz bir şeyler bizim güvenirlik aralığını hakkında söyleyin: güvenle 1,35 ayar elmas hello bedelinin iş hakkında $10.000 - ancak 8000 kadar düşük olabilir ve 12.000 yüksek olabilir dediğimiz.</span><span class="sxs-lookup"><span data-stu-id="65f3b-186">Now we can say something about our confidence interval:  We can say confidently that hello price of a 1.35 carat diamond is about $10,000 - but it might be as low as $8,000 and it might be as high as $12,000.</span></span>

## <a name="were-done-with-no-math-or-computers"></a><span data-ttu-id="65f3b-187">Matematik ya da bilgisayarları bitmek</span><span class="sxs-lookup"><span data-stu-id="65f3b-187">We're done, with no math or computers</span></span>
<span data-ttu-id="65f3b-188">Hangi veri bilimcilerine toodo ödeme yaptığımız ve onu yalnızca çizerek yaptığımız:</span><span class="sxs-lookup"><span data-stu-id="65f3b-188">We did what data scientists get paid toodo, and we did it just by drawing:</span></span>

* <span data-ttu-id="65f3b-189">Biz biz verilerle yanıt bir soru sorular</span><span class="sxs-lookup"><span data-stu-id="65f3b-189">We asked a question that we could answer with data</span></span>
* <span data-ttu-id="65f3b-190">Oluşturduğumuz bir *modeli* kullanarak *doğrusal regresyon*</span><span class="sxs-lookup"><span data-stu-id="65f3b-190">We built a *model* using *linear regression*</span></span>
* <span data-ttu-id="65f3b-191">Biz yapılan bir *tahmin*ile tam bir *güvenirlik aralığını*</span><span class="sxs-lookup"><span data-stu-id="65f3b-191">We made a *prediction*, complete with a *confidence interval*</span></span>

<span data-ttu-id="65f3b-192">Ve matematik veya bilgisayarlar toodo kullanırız alamadık.</span><span class="sxs-lookup"><span data-stu-id="65f3b-192">And we didn't use math or computers toodo it.</span></span>

<span data-ttu-id="65f3b-193">Şimdi biz daha fazla bilgi olsaydı, ister...</span><span class="sxs-lookup"><span data-stu-id="65f3b-193">Now if we'd had more information, like...</span></span>

* <span data-ttu-id="65f3b-194">Merhaba hello elmas Kes</span><span class="sxs-lookup"><span data-stu-id="65f3b-194">hello cut of hello diamond</span></span>
* <span data-ttu-id="65f3b-195">renk değişimleri (ne kadar yakın hello elmas toobeing Beyaz'dır)</span><span class="sxs-lookup"><span data-stu-id="65f3b-195">color variations (how close hello diamond is toobeing white)</span></span>
* <span data-ttu-id="65f3b-196">Merhaba elmas içindeki içermeler Hello sayısı</span><span class="sxs-lookup"><span data-stu-id="65f3b-196">hello number of inclusions in hello diamond</span></span>

<span data-ttu-id="65f3b-197">.. .then biz olan daha fazla sütun.</span><span class="sxs-lookup"><span data-stu-id="65f3b-197">...then we would have had more columns.</span></span> <span data-ttu-id="65f3b-198">Bu durumda, Matematik yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="65f3b-198">In that case, math becomes helpful.</span></span> <span data-ttu-id="65f3b-199">İkiden fazla sütuna sahip, sabit toodraw nokta kağıda olur.</span><span class="sxs-lookup"><span data-stu-id="65f3b-199">If you have more than two columns, it's hard toodraw dots on paper.</span></span> <span data-ttu-id="65f3b-200">Merhaba matematik, o satırdaki veya düzlemi tooyour verilerin çok iyi sığacak olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="65f3b-200">hello math lets you fit that line or that plane tooyour data very nicely.</span></span>

<span data-ttu-id="65f3b-201">Ayrıca, yalnızca birkaç Karo varsa, yerine biz iki bin veya iki milyon vardı sonra çalışan bir bilgisayarla çok daha hızlı yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65f3b-201">Also, if instead of just a handful of diamonds, we had two thousand or two million, then you can do that work much faster with a computer.</span></span>

<span data-ttu-id="65f3b-202">Bugün, biz nasıl toodo doğrusal regresyon ve biz verileri kullanarak bir tahmini yapılan hakkında açıklandı.</span><span class="sxs-lookup"><span data-stu-id="65f3b-202">Today, we've talked about how toodo linear regression, and we made a prediction using data.</span></span>

<span data-ttu-id="65f3b-203">Merhaba çıkışı emin toocheck "Veri bilimi için yeni başlayanlar" Microsoft Azure Machine learning'in diğer videoları olabilir.</span><span class="sxs-lookup"><span data-stu-id="65f3b-203">Be sure toocheck out hello other videos in "Data Science for Beginners" from Microsoft Azure Machine Learning.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65f3b-204">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="65f3b-204">Next steps</span></span>
* [<span data-ttu-id="65f3b-205">İlk veri bilimi denemeyi Machine Learning Studio'da deneyin</span><span class="sxs-lookup"><span data-stu-id="65f3b-205">Try a first data science experiment with Machine Learning Studio</span></span>](machine-learning-create-experiment.md)
* [<span data-ttu-id="65f3b-206">Bir giriş tooMachine alma Microsoft Azure üzerinde öğrenme</span><span class="sxs-lookup"><span data-stu-id="65f3b-206">Get an introduction tooMachine Learning on Microsoft Azure</span></span>](machine-learning-what-is-machine-learning.md)
