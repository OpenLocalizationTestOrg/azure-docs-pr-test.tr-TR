---
title: "Machine Learning için R dilde aaaQuickstart Öğreticisi | Microsoft Docs"
description: "Merhaba R dil Azure Machine Learning Studio toocreate tahmin çözümü hızlı bir şekilde kullanmaya öğretici tooget programlama bu R kullanın."
keywords: "Hızlı Başlangıç, r dil, r programlama dili, r programlama Öğreticisi"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 99a3a0fd-b359-481a-b236-66868deccd96
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 9995f8728f4d7bf9a5c15412015e4cf769cdac96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-tutorial-for-hello-r-programming-language-for-azure-machine-learning"></a><span data-ttu-id="a5592-104">Azure Machine Learning için hello R programlama dili için hızlı başlangıç Öğreticisi</span><span class="sxs-lookup"><span data-stu-id="a5592-104">Quickstart tutorial for hello R programming language for Azure Machine Learning</span></span>

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a><span data-ttu-id="a5592-105">Giriş</span><span class="sxs-lookup"><span data-stu-id="a5592-105">Introduction</span></span>
<span data-ttu-id="a5592-106">Bu hızlı başlangıç Öğreticisi, Azure Machine Learning hello R programlama dilini kullanarak genişletme hızla başlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="a5592-106">This quickstart tutorial helps you quickly start extending Azure Machine Learning by using hello R programming language.</span></span> <span data-ttu-id="a5592-107">Eğitmen toocreate programlama bu R izleyin, test ve Azure Machine Learning içinde R kodunu yürütün.</span><span class="sxs-lookup"><span data-stu-id="a5592-107">Follow this R programming tutorial toocreate, test and execute R code within Azure Machine Learning.</span></span> <span data-ttu-id="a5592-108">Öğreticide çalışırken, Azure Machine Learning ile Merhaba R dilini kullanarak eksiksiz bir tahmin çözüm oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a5592-108">As you work through tutorial, you will create a complete forecasting solution by using hello R language in Azure Machine Learning.</span></span>  

<span data-ttu-id="a5592-109">Microsoft Azure Machine Learning'de pek çok güçlü machine learning ve veri işleme modüller içerir.</span><span class="sxs-lookup"><span data-stu-id="a5592-109">Microsoft Azure Machine Learning contains many powerful machine learning and data manipulation modules.</span></span> <span data-ttu-id="a5592-110">Merhaba güçlü R dil hello en yaygın kullanılan analytics, açıklanan.</span><span class="sxs-lookup"><span data-stu-id="a5592-110">hello powerful R language has been described as hello lingua franca of analytics.</span></span> <span data-ttu-id="a5592-111">R kullanarak Azure Machine Learning analizi ve veri işleme sonsuza dek, Genişletilebilir Bu birleşimi hello ölçeklenebilirlik ve Azure Machine Learning dağıtımını kolaylığı hello esneklik ve r, derin analizi sağlar</span><span class="sxs-lookup"><span data-stu-id="a5592-111">Happily, analytics and data manipulation in Azure Machine Learning can be extended by using R. This combination provides hello scalability and ease of deployment of Azure Machine Learning with hello flexibility and deep analytics of R.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-hello-dataset"></a><span data-ttu-id="a5592-112">Tahmin ve hello veri kümesi</span><span class="sxs-lookup"><span data-stu-id="a5592-112">Forecasting and hello dataset</span></span>
<span data-ttu-id="a5592-113">Tahmin yaygın olarak kullanılan ve oldukça kullanışlıdır analitik yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="a5592-113">Forecasting is a widely employed and quite useful analytical method.</span></span> <span data-ttu-id="a5592-114">Genel en iyi stok düzeylerini, toopredicting macroeconomic değişkenleri belirleme Mevsimlik öğelerinin satış tahmin etmeye gelen aralığını kullanır.</span><span class="sxs-lookup"><span data-stu-id="a5592-114">Common uses range from predicting sales of seasonal items, determining optimal inventory levels, toopredicting macroeconomic variables.</span></span> <span data-ttu-id="a5592-115">Tahmin genellikle zaman serisi modelleri ile yapılır.</span><span class="sxs-lookup"><span data-stu-id="a5592-115">Forecasting is typically done with time series models.</span></span>

<span data-ttu-id="a5592-116">Zaman serisi veri hello değerleri bir zaman dizine sahip verilerdir.</span><span class="sxs-lookup"><span data-stu-id="a5592-116">Time series data is data in which hello values have a time index.</span></span> <span data-ttu-id="a5592-117">Örneğin, her ay ya da her dakika Hello süre dizininin normal, olabilir veya düzensiz.</span><span class="sxs-lookup"><span data-stu-id="a5592-117">hello time index can be regular, e.g. every month or every minute, or irregular.</span></span> <span data-ttu-id="a5592-118">Zaman serisi modeli zaman serisi verilerine dayalıdır.</span><span class="sxs-lookup"><span data-stu-id="a5592-118">A time series model is based on time series data.</span></span> <span data-ttu-id="a5592-119">Merhaba R programlama dili esnek framework ve kapsamlı analizi için zaman serisi veri içerir.</span><span class="sxs-lookup"><span data-stu-id="a5592-119">hello R programming language contains a flexible framework and extensive analytics for time series data.</span></span>

<span data-ttu-id="a5592-120">Bu Hızlı Başlangıç Kılavuzu'nda biz California Süt ürün çalışma ve veri fiyatlandırma.</span><span class="sxs-lookup"><span data-stu-id="a5592-120">In this quickstart guide we will be working with California dairy production and pricing data.</span></span> <span data-ttu-id="a5592-121">Bu veriler hello üretim birkaç Süt ürünlerin ve hello fiyat sütlü FAT, kıyaslama Emtia aylık bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="a5592-121">This data includes monthly information on hello production of several dairy products and hello price of milk fat, a benchmark commodity.</span></span>

<span data-ttu-id="a5592-122">Bu makalede, R betiklerini birlikte kullanılan hello veriler [burada indirilen][download].</span><span class="sxs-lookup"><span data-stu-id="a5592-122">hello data used in this article, along with R scripts, can be [downloaded here][download].</span></span> <span data-ttu-id="a5592-123">Bu veriler başlangıçta hello University Wisconsin http://future.aae.wisc.edu/tab/production.html konumunda bulunan bilgilerden oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="a5592-123">This data was originally synthesized from information available from hello University of Wisconsin at http://future.aae.wisc.edu/tab/production.html.</span></span>

### <a name="organization"></a><span data-ttu-id="a5592-124">Kuruluş</span><span class="sxs-lookup"><span data-stu-id="a5592-124">Organization</span></span>
<span data-ttu-id="a5592-125">Nasıl toocreate, test ve hello Azure Machine Learning ortamında analizi ve veri işleme R kod yürütmek öğrenirken size çeşitli adımlarda ilerleyeceğini.</span><span class="sxs-lookup"><span data-stu-id="a5592-125">We will progress through several steps as you learn how toocreate, test and execute analytics and data manipulation R code in hello Azure Machine Learning environment.</span></span>  

* <span data-ttu-id="a5592-126">İlk biz hello temelleri hello Azure Machine Learning Studio ortamında hello R dilini kullanarak inceleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="a5592-126">First we will explore hello basics of using hello R language in hello Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="a5592-127">Ardından biz toodiscussing çeşitli yönlerini g/ç için veri, R kodu ve grafik hello Azure Machine Learning ortamında ilerleme.</span><span class="sxs-lookup"><span data-stu-id="a5592-127">Then we progress toodiscussing various aspects of I/O for data, R code and graphics in hello Azure Machine Learning environment.</span></span>
* <span data-ttu-id="a5592-128">Biz ardından tahmin çözümümüzdür hello ilk bölümü veri temizleme ve dönüştürme için kod oluşturarak oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="a5592-128">We will then construct hello first part of our forecasting solution by creating code for data cleaning and transformation.</span></span>
* <span data-ttu-id="a5592-129">Hazırlanan bizim verilerle birkaç veri kümemizde hello değişkenlerin arasındaki hello bağıntıları analizini gerçekleştiririz.</span><span class="sxs-lookup"><span data-stu-id="a5592-129">With our data prepared we will perform an analysis of hello correlations between several of hello variables in our dataset.</span></span>
* <span data-ttu-id="a5592-130">Son olarak, sütlü üretim için Mevsimlik zaman serisi tahmin modeli oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="a5592-130">Finally, we will create a seasonal time series forecasting model for milk production.</span></span>

## <span data-ttu-id="a5592-131"><a id="mlstudio"></a>Machine Learning Studio'da R dil ile etkileşim</span><span class="sxs-lookup"><span data-stu-id="a5592-131"><a id="mlstudio"></a>Interact with R language in Machine Learning Studio</span></span>
<span data-ttu-id="a5592-132">Bu bölümde bazı temelleri hello R programlama dili hello Machine Learning Studio ortamında etkileşimde alır.</span><span class="sxs-lookup"><span data-stu-id="a5592-132">This section takes you through some basics of interacting with hello R programming language in hello Machine Learning Studio environment.</span></span> <span data-ttu-id="a5592-133">Merhaba R dil bir güçlü bir araç özelleştirilmiş toocreate analizi ve veri işleme modülleri hello Azure Machine Learning ortamında sağlar.</span><span class="sxs-lookup"><span data-stu-id="a5592-133">hello R language provides a powerful tool toocreate customized analytics and data manipulation modules within hello Azure Machine Learning environment.</span></span>

<span data-ttu-id="a5592-134">Küçük ölçekte Rstudio'dan toodevelop, test ve hata ayıklama R kodunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="a5592-134">I will use RStudio toodevelop, test and debug R code on a small scale.</span></span> <span data-ttu-id="a5592-135">Bu kodu ardından kesme ve yapıştırma içine bir [R betiği yürütün] [ execute-r-script] Machine Learning Studio hazır toorun modülünde.</span><span class="sxs-lookup"><span data-stu-id="a5592-135">This code is then cut and paste into an [Execute R Script][execute-r-script] module in Machine Learning Studio ready toorun.</span></span>  

### <a name="hello-execute-r-script-module"></a><span data-ttu-id="a5592-136">Merhaba R betiği yürütün Modülü</span><span class="sxs-lookup"><span data-stu-id="a5592-136">hello Execute R Script module</span></span>
<span data-ttu-id="a5592-137">Machine Learning Studio'da R betiklerini hello içinde çalıştırılan [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="a5592-137">Within Machine Learning Studio, R scripts are run within hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="a5592-138">Merhaba örneği [R betiği yürütün] [ execute-r-script] Machine Learning Studio'da modülü, Şekil 1'de gösterilir.</span><span class="sxs-lookup"><span data-stu-id="a5592-138">An example of hello [Execute R Script][execute-r-script] module in Machine Learning Studio is shown in Figure 1.</span></span>

 ![Programlama dili R: Machine Learning Studio'da seçili hello R betiği yürütün Modülü][1]

<span data-ttu-id="a5592-140">*Şekil 1 '. Seçili hello R betiği yürütün modülü gösteren hello Machine Learning Studio ortamı.*</span><span class="sxs-lookup"><span data-stu-id="a5592-140">*Figure 1. hello Machine Learning Studio environment showing hello Execute R Script module selected.*</span></span>

<span data-ttu-id="a5592-141">TooFigure 1 başvuran, bazı parçalarının hello anahtar hello ile çalışmak için hello Machine Learning Studio ortamı bakalım [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="a5592-141">Referring tooFigure 1, let's look at some of hello key parts of hello Machine Learning Studio environment for working with hello [Execute R Script][execute-r-script] module.</span></span>

* <span data-ttu-id="a5592-142">Merhaba deneme Hello modülleri hello merkezi bölmesinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="a5592-142">hello modules in hello experiment are shown in hello center pane.</span></span>
* <span data-ttu-id="a5592-143">Merhaba sağ bölmede üst kısmındaki Hello penceresi tooview içerir ve R komut dosyalarınızı düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="a5592-143">hello upper part of hello right pane contains a window tooview and edit your R scripts.</span></span>  
* <span data-ttu-id="a5592-144">sağ bölmede alt kısmı Hello gösterir hello bazı özellikleri [R betiği yürütün][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="a5592-144">hello lower part of right pane shows some properties of hello [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="a5592-145">Merhaba üzerindeki bu bölmesinin uygun noktaları tıklayarak hello hata ve Çıktı günlükleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5592-145">You can view hello error and output logs by clicking on hello appropriate spots of this pane.</span></span>

<span data-ttu-id="a5592-146">Biz doğal olarak, hello ele [R betiği yürütün] [ execute-r-script] hello kalan bu belgenin daha ayrıntılı.</span><span class="sxs-lookup"><span data-stu-id="a5592-146">We will, of course, be discussing hello [Execute R Script][execute-r-script] in greater detail in hello rest of this document.</span></span>

<span data-ttu-id="a5592-147">Karmaşık R işlevleri ile çalışırken, t, düzenleme, test ve Rstudio'dan içinde hata ayıklama öneririz.</span><span class="sxs-lookup"><span data-stu-id="a5592-147">When working with complex R functions, I recommend that you edit, test and debug in RStudio.</span></span> <span data-ttu-id="a5592-148">Tüm yazılım geliştirme olduğu gibi kodunuzu artımlı olarak genişletmek ve küçük basit test çalışmalarını test.</span><span class="sxs-lookup"><span data-stu-id="a5592-148">As with any software development, extend your code incrementally and test it on small simple test cases.</span></span> <span data-ttu-id="a5592-149">Ardından kesip işlevlerinizi hello R betiği penceresine hello [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="a5592-149">Then cut and paste your functions into hello R script window of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="a5592-150">Bu yaklaşım, tooharness Rstudio'dan tümleşik geliştirme ortamı (IDE) hello hem Azure Machine Learning gücünü hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="a5592-150">This approach allows you tooharness both hello RStudio integrated development environment (IDE) and hello power of Azure Machine Learning.</span></span>  

#### <a name="execute-r-code"></a><span data-ttu-id="a5592-151">R kodu yürütme</span><span class="sxs-lookup"><span data-stu-id="a5592-151">Execute R code</span></span>
<span data-ttu-id="a5592-152">Merhaba bir R kodda [R betiği yürütün] [ execute-r-script] modülü üzerinde hello tıklayarak hello deneme çalıştırdığınızda, yürütülecek **çalıştırmak** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a5592-152">Any R code in hello [Execute R Script][execute-r-script] module will execute when you run hello experiment by clicking on hello **Run** button.</span></span> <span data-ttu-id="a5592-153">Yürütme tamamlandığında, bir onay işareti hello üzerinde görünür [R betiği yürütün] [ execute-r-script] simgesi.</span><span class="sxs-lookup"><span data-stu-id="a5592-153">When execution has completed, a check mark will appear on hello [Execute R Script][execute-r-script] icon.</span></span>

#### <a name="defensive-r-coding-for-azure-machine-learning"></a><span data-ttu-id="a5592-154">Azure Machine Learning için savunma R kodlama</span><span class="sxs-lookup"><span data-stu-id="a5592-154">Defensive R coding for Azure Machine Learning</span></span>
<span data-ttu-id="a5592-155">Azure Machine Learning kullanarak R kodu söyleyin, bir web hizmeti için geliştiriyorsanız, kesinlikle kodunuzu beklenmeyen veri giriş ve özel durumları nasıl ilgilenecektir planlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a5592-155">If you are developing R code for, say, a web service by using Azure Machine Learning, you should definitely plan how your code will deal with an unexpected data input and exceptions.</span></span> <span data-ttu-id="a5592-156">toomaintain netlik ı çok hello denetleme veya özel durum işleme gösterilen hello kod örnekleri çoğunda eklemediniz.</span><span class="sxs-lookup"><span data-stu-id="a5592-156">toomaintain clarity, I have not included much in hello way of checking or exception handling in most of hello code examples shown.</span></span> <span data-ttu-id="a5592-157">İlerlemeden gibi ancak ı size çeşitli işlevleri örnekleri R'ın özel durum işleme yeteneği kullanarak sunar.</span><span class="sxs-lookup"><span data-stu-id="a5592-157">However, as we proceed I will give you several examples of functions by using R's exception handling capability.</span></span>  

<span data-ttu-id="a5592-158">Daha eksiksiz bir R özel durum işleme işlenmesi gerekiyorsa, ı hello defteri listelenen Wickham tarafından hello uygun bölümleri okumanız önerilir [ek B - daha fazla bilgi](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="a5592-158">If you need a more complete treatment of R exception handling, I recommend you read hello applicable sections of hello book by Wickham listed in [Appendix B - Further Reading](#appendixb).</span></span>

#### <a name="debug-and-test-r-in-machine-learning-studio"></a><span data-ttu-id="a5592-159">Hata ayıklama ve Machine Learning Studio'da R test</span><span class="sxs-lookup"><span data-stu-id="a5592-159">Debug and test R in Machine Learning Studio</span></span>
<span data-ttu-id="a5592-160">tooreiterate, test ve küçük ölçekte Rstudio'dan içinde R kodunuzdaki hataları ayıklamanıza öneririz.</span><span class="sxs-lookup"><span data-stu-id="a5592-160">tooreiterate, I recommend you test and debug your R code on a small scale in RStudio.</span></span> <span data-ttu-id="a5592-161">Ancak, burada gerekir hello R kodu sorunlarını aşağı tootrack durumlar vardır [R betiği yürütün] [ execute-r-script] kendisi.</span><span class="sxs-lookup"><span data-stu-id="a5592-161">However, there are cases where you will need tootrack down R code problems in hello [Execute R Script][execute-r-script] itself.</span></span> <span data-ttu-id="a5592-162">Buna ek olarak, iyi bir uygulama toocheck sonuçlarınızda olan Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="a5592-162">In addition, it is good practice toocheck your results in Machine Learning Studio.</span></span>

<span data-ttu-id="a5592-163">Merhaba yürütme R kodunuzu ve hello Azure Machine Learning platformunda çıktısını öncelikle içeren içinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="a5592-163">Output from hello execution of your R code and on hello Azure Machine Learning platform is found primarily in output.log.</span></span> <span data-ttu-id="a5592-164">Bazı ek bilgiler error.log görülür.</span><span class="sxs-lookup"><span data-stu-id="a5592-164">Some additional information will be seen in error.log.</span></span>  

<span data-ttu-id="a5592-165">Machine Learning Studio'da R kodunuzu çalıştırılırken bir hata meydana gelirse, eylem, ilk seyri toolook error.log adresindeki olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a5592-165">If an error occurs in Machine Learning Studio while running your R code, your first course of action should be toolook at error.log.</span></span> <span data-ttu-id="a5592-166">Bu dosya anlamak ve, hatayı düzeltmek yararlı hata iletileri toohelp içerebilir.</span><span class="sxs-lookup"><span data-stu-id="a5592-166">This file can contain useful error messages toohelp you understand and correct your error.</span></span> <span data-ttu-id="a5592-167">tooview error.log, tıklatıldığında **hata günlüğü görüntüle** hello üzerinde **Özellikler bölmesinde** hello için [R betiği yürütün] [ execute-r-script] hello hata içeren.</span><span class="sxs-lookup"><span data-stu-id="a5592-167">tooview error.log, click on **View error log** on hello **properties pane** for hello [Execute R Script][execute-r-script] containing hello error.</span></span>

<span data-ttu-id="a5592-168">Örneğin, içinde tanımlanmamış bir değişken y R kodu aşağıdaki hello çalıştırdım bir [R betiği yürütün] [ execute-r-script] Modülü:</span><span class="sxs-lookup"><span data-stu-id="a5592-168">For example, I ran hello following R code, with an undefined variable y, in an [Execute R Script][execute-r-script] module:</span></span>

    x <- 1.0
    z <- x + y

<span data-ttu-id="a5592-169">Bu kodu bir hata koşulu kaynaklanan tooexecute başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="a5592-169">This code fails tooexecute, resulting in an error condition.</span></span> <span data-ttu-id="a5592-170">Tıklayarak **hata günlüğü görüntüle** hello üzerinde **Özellikler bölmesinde** üretir hello Şekil 2'de gösterilen görüntüleme.</span><span class="sxs-lookup"><span data-stu-id="a5592-170">Clicking on **View error log** on hello **properties pane** produces hello display shown in Figure 2.</span></span>

  ![Hata iletisi açılır][2]

<span data-ttu-id="a5592-172">*Şekil 2 '. Hata iletisi açılır.*</span><span class="sxs-lookup"><span data-stu-id="a5592-172">*Figure 2. Error message pop-up.*</span></span>

<span data-ttu-id="a5592-173">Toolook içeren toosee hello R hata iletisindeki ihtiyacımız gibi görünüyor.</span><span class="sxs-lookup"><span data-stu-id="a5592-173">It looks like we need toolook in output.log toosee hello R error message.</span></span> <span data-ttu-id="a5592-174">Hello üzerinde tıklatın [R betiği yürütün] [ execute-r-script] ve üzerinde hello ardından **içeren görüntülemek** hello öğede **Özellikler bölmesinde** toohello sağ.</span><span class="sxs-lookup"><span data-stu-id="a5592-174">Click on hello [Execute R Script][execute-r-script] and then click on hello **View output.log** item on hello **properties pane** toohello right.</span></span> <span data-ttu-id="a5592-175">Yeni bir tarayıcı penceresi açar ve hello aşağıdakilere bakın.</span><span class="sxs-lookup"><span data-stu-id="a5592-175">A new browser window opens, and I see hello following.</span></span>

    [Critical]     Error: Error 0063: hello following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

<span data-ttu-id="a5592-176">Bu hata iletisi yok beklenmeyen durumları içerir ve açıkça hello sorun tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a5592-176">This error message contains no surprises and clearly identifies hello problem.</span></span>

<span data-ttu-id="a5592-177">R herhangi bir nesne tooinspect hello değeri, bu değerler toohello içeren dosyası yazdırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5592-177">tooinspect hello value of any object in R, you can print these values toohello output.log file.</span></span> <span data-ttu-id="a5592-178">temelde değerlerdir nesne incelenmesinin hello kuralları aynı etkileşimli bir R oturumu olduğu gibi hello.</span><span class="sxs-lookup"><span data-stu-id="a5592-178">hello rules for examining object values are essentially hello same as in an interactive R session.</span></span> <span data-ttu-id="a5592-179">Örneğin, bir satıra bir değişken adı yazın, hello nesnesinin başlangıç değeri yazdırılan toohello içeren dosya olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a5592-179">For example, if you type a variable name on a line, hello value of hello object will be printed toohello output.log file.</span></span>  

#### <a name="packages-in-machine-learning-studio"></a><span data-ttu-id="a5592-180">Machine Learning Studio'da paketleri</span><span class="sxs-lookup"><span data-stu-id="a5592-180">Packages in Machine Learning Studio</span></span>
<span data-ttu-id="a5592-181">Azure Machine Learning 350'den önceden yüklenmiş R dil paketleriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="a5592-181">Azure Machine Learning comes with over 350 preinstalled R language packages.</span></span> <span data-ttu-id="a5592-182">Merhaba kodda aşağıdaki hello kullanabilirsiniz [R betiği yürütün] [ execute-r-script] modülü tooretrieve hello listesini önceden yüklenen paketler.</span><span class="sxs-lookup"><span data-stu-id="a5592-182">You can use hello following code in hello [Execute R Script][execute-r-script] module tooretrieve a list of hello preinstalled packages.</span></span>

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

<span data-ttu-id="a5592-183">Merhaba şu anda bu kodu son satırının hello anlamadığınız okumaya devam edin.</span><span class="sxs-lookup"><span data-stu-id="a5592-183">If you don't understand hello last line of this code at hello moment, read on.</span></span> <span data-ttu-id="a5592-184">Bu belgenin Hello kalan yaygın hello Azure Machine Learning ortamda R kullanarak aşağıdakiler ele alınacaktır.</span><span class="sxs-lookup"><span data-stu-id="a5592-184">In hello rest of this document we will extensively discuss using R in hello Azure Machine Learning environment.</span></span>

### <a name="introduction-toorstudio"></a><span data-ttu-id="a5592-185">Giriş tooRStudio</span><span class="sxs-lookup"><span data-stu-id="a5592-185">Introduction tooRStudio</span></span>
<span data-ttu-id="a5592-186">R için yaygın olarak kullanılan bir IDE Rstudio'dan olduğu Rstudio'dan düzenleme, test ve bu Hızlı Başlangıç Kılavuzu'nda kullanılan hello R kodu bazıları hata ayıklama için kullanır.</span><span class="sxs-lookup"><span data-stu-id="a5592-186">RStudio is a widely used IDE for R. I will use RStudio for editing, testing and debugging some of hello R code used in this quick start guide.</span></span> <span data-ttu-id="a5592-187">R kodu test edilmiş ve hazır olduğunda size kesip hello Rstudio'dan Düzenleyicisi'nden bir Machine Learning Studio'ya [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="a5592-187">Once R code is tested and ready, you simply cut and paste from hello RStudio editor into a Machine Learning Studio [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="a5592-188">Masaüstü makinenize yüklü hello R programlama dili yoksa, bunu şimdi yapın ı öneririz.</span><span class="sxs-lookup"><span data-stu-id="a5592-188">If you do not have hello R programming language installed on your desktop machine, I recommend you do so now.</span></span> <span data-ttu-id="a5592-189">Açık kaynak R dilinin ücretsiz indirme hello kapsamlı R arşiv ağ (CRAN) kullanılabilir en [http://www.r-project.org/](http://www.r-project.org/).</span><span class="sxs-lookup"><span data-stu-id="a5592-189">Free downloads of open source R language are available at hello Comprehensive R Archive Network (CRAN) at [http://www.r-project.org/](http://www.r-project.org/).</span></span> <span data-ttu-id="a5592-190">Windows, Mac OS ve Linux/UNIX için kullanılabilir yüklemeler vardır.</span><span class="sxs-lookup"><span data-stu-id="a5592-190">There are downloads available for Windows, Mac OS, and Linux/UNIX.</span></span> <span data-ttu-id="a5592-191">Yakındaki bir yansıtma seçin ve hello yükleme yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="a5592-191">Choose a nearby mirror and follow hello download directions.</span></span> <span data-ttu-id="a5592-192">Ayrıca, CRAN bol miktarda yararlı analizi ve veri işleme paketleri içerir.</span><span class="sxs-lookup"><span data-stu-id="a5592-192">In addition, CRAN contains a wealth of useful analytics and data manipulation packages.</span></span>

<span data-ttu-id="a5592-193">Yeni tooRStudio varsa, indirin ve hello Masaüstü sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a5592-193">If you are new tooRStudio, you should download and install hello desktop version.</span></span> <span data-ttu-id="a5592-194">Rstudio'dan http://www.rstudio.com/products/RStudio/ Windows, Mac OS ve Linux/UNIX indirmeleri hello bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5592-194">You can find hello RStudio downloads for Windows, Mac OS, and Linux/UNIX at http://www.rstudio.com/products/RStudio/.</span></span> <span data-ttu-id="a5592-195">Masaüstü makinenizde tooinstall Rstudio'dan sağlanan hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="a5592-195">Follow hello directions provided tooinstall RStudio on your desktop machine.</span></span>  

<span data-ttu-id="a5592-196">Eğitmen giriş tooRStudio https://support.rstudio.com/hc/sections/200107586-Using-RStudio kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a5592-196">A tutorial introduction tooRStudio is available at https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span></span>

<span data-ttu-id="a5592-197">I içinde Rstudio'dan kullanarak bazı ek bilgiler sağlayan [ek A][appendixa].</span><span class="sxs-lookup"><span data-stu-id="a5592-197">I provide some additional information on using RStudio in [Appendix A][appendixa].</span></span>  

## <span data-ttu-id="a5592-198"><a id="scriptmodule"></a>Merhaba R betiği yürütün modülü ve dışındaki veri al</span><span class="sxs-lookup"><span data-stu-id="a5592-198"><a id="scriptmodule"></a>Get data in and out of hello Execute R Script module</span></span>
<span data-ttu-id="a5592-199">Bu bölümde içine ve dışına hello veri nereden aşağıdakiler ele alınacaktır [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="a5592-199">In this section we will discuss how you get data into and out of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="a5592-200">Biz içine ve dışına hello toohandle çeşitli veri türlerini nasıl okuma incelenecek [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="a5592-200">We will review how toohandle various data types read into and out of hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="a5592-201">Merhaba tam bu bölümde daha önce indirdiğiniz hello zip dosyasında kodudur.</span><span class="sxs-lookup"><span data-stu-id="a5592-201">hello complete code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="load-and-check-data-in-machine-learning-studio"></a><span data-ttu-id="a5592-202">Yük ve veri Machine Learning Studio'da denetleyin</span><span class="sxs-lookup"><span data-stu-id="a5592-202">Load and check data in Machine Learning Studio</span></span>
#### <span data-ttu-id="a5592-203"><a id="loading"></a>Yük hello veri kümesi</span><span class="sxs-lookup"><span data-stu-id="a5592-203"><a id="loading"></a>Load hello dataset</span></span>
<span data-ttu-id="a5592-204">Biz hello yükleyerek başlayacak **csdairydata.csv** Azure Machine Learning Studio dosyasına.</span><span class="sxs-lookup"><span data-stu-id="a5592-204">We will start by loading hello **csdairydata.csv** file into Azure Machine Learning Studio.</span></span>

* <span data-ttu-id="a5592-205">Azure Machine Learning Studio ortamınızı başlatın.</span><span class="sxs-lookup"><span data-stu-id="a5592-205">Start your Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="a5592-206">Tıklayın **+ yeni** hello seçin ve ekranın sol alt **Dataset**.</span><span class="sxs-lookup"><span data-stu-id="a5592-206">Click on **+ NEW** at hello lower left of your screen and select **Dataset**.</span></span>
* <span data-ttu-id="a5592-207">Seçin **yerel dosyadan**ve ardından **Gözat** tooselect hello dosya.</span><span class="sxs-lookup"><span data-stu-id="a5592-207">Select **From Local File**, and then **Browse** tooselect hello file.</span></span>
* <span data-ttu-id="a5592-208">Seçtiğiniz emin olun **genel CSV dosyası (.csv) üstbilgiyle** hello veri kümesi için hello türü.</span><span class="sxs-lookup"><span data-stu-id="a5592-208">Make sure you have selected **Generic CSV file with header (.csv)** as hello type for hello dataset.</span></span>
* <span data-ttu-id="a5592-209">Merhaba onay işaretine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a5592-209">Click hello check mark.</span></span>
* <span data-ttu-id="a5592-210">Merhaba dataset karşıya yüklendikten sonra hello üzerinde tıklayarak hello yeni veri kümesi görmelisiniz **veri kümeleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="a5592-210">After hello dataset has been uploaded, you should see hello new dataset by clicking on hello **Datasets** tab.</span></span>  

#### <a name="create-an-experiment"></a><span data-ttu-id="a5592-211">Bir deneme oluşturma</span><span class="sxs-lookup"><span data-stu-id="a5592-211">Create an experiment</span></span>
<span data-ttu-id="a5592-212">Machine Learning Studio'da sahip olduğumuz bazı verileri, toocreate deneme toodo hello analiz ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="a5592-212">Now that we have some data in Machine Learning Studio, we need toocreate an experiment toodo hello analysis.</span></span>  

* <span data-ttu-id="a5592-213">Tıklayın **+ yeni** hello sol alt ve seçin **deneme**, ardından **boş deneme**.</span><span class="sxs-lookup"><span data-stu-id="a5592-213">Click on **+ NEW** at hello lower left and select **Experiment**, then **Blank Experiment**.</span></span>
* <span data-ttu-id="a5592-214">Seçerek denemenizi adlandırın ve değiştirme hello **deneme oluşturulan...**  hello sayfanın üst kısmındaki hello başlığı.</span><span class="sxs-lookup"><span data-stu-id="a5592-214">You can name your experiment by selecting, and modifying, hello **Experiment created on ...** title at hello top of hello page.</span></span> <span data-ttu-id="a5592-215">Örneğin, çok değiştirme**CA günlük analizi**.</span><span class="sxs-lookup"><span data-stu-id="a5592-215">For example, changing it too**CA Dairy Analysis**.</span></span>
* <span data-ttu-id="a5592-216">Merhaba deneme sayfa Hello solda genişletin **kaydedilen veri kümeleri**ve ardından **My veri kümeleri**.</span><span class="sxs-lookup"><span data-stu-id="a5592-216">On hello left of hello experiment page, expand **Saved Datasets**, and then **My Datasets**.</span></span> <span data-ttu-id="a5592-217">Merhaba görmelisiniz **cadairydata.csv** daha önce yüklediğiniz.</span><span class="sxs-lookup"><span data-stu-id="a5592-217">You should see hello **cadairydata.csv** that you uploaded earlier.</span></span>
* <span data-ttu-id="a5592-218">Sürükle ve bırak hello **csdairydata.csv dataset** hello deneme üzerine.</span><span class="sxs-lookup"><span data-stu-id="a5592-218">Drag and drop hello **csdairydata.csv dataset** onto hello experiment.</span></span>
* <span data-ttu-id="a5592-219">Merhaba, **arama öğeleri denemeler** hello sol bölmede, türü hello üstündeki kutusunu [R betiği yürütün][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="a5592-219">In hello **Search experiment items** box on hello top of hello left pane, type [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="a5592-220">Merhaba arama listede hello modülü görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="a5592-220">You will see hello module appear in hello search list.</span></span>
* <span data-ttu-id="a5592-221">Sürükle ve bırak hello [R betiği yürütün] [ execute-r-script] , palet modülü.</span><span class="sxs-lookup"><span data-stu-id="a5592-221">Drag and drop hello [Execute R Script][execute-r-script] module onto your pallet.</span></span>  
* <span data-ttu-id="a5592-222">Merhaba Hello çıkışına bağlayın **csdairydata.csv dataset** toohello soldaki giriş (**Dataset1**) Merhaba, [R betiği yürütün][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="a5592-222">Connect hello output of hello **csdairydata.csv dataset** toohello leftmost input (**Dataset1**) of hello [Execute R Script][execute-r-script].</span></span>
* <span data-ttu-id="a5592-223">**'Kaydet' üzerinde tooclick unutmayın!**</span><span class="sxs-lookup"><span data-stu-id="a5592-223">**Don't forget tooclick on 'Save'!**</span></span>  

<span data-ttu-id="a5592-224">Bu noktada denemenizi Şekil 3 gibi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="a5592-224">At this point your experiment should look something like Figure 3.</span></span>

![Merhaba CA günlük analizi denemeler veri kümesi ve R betiği yürütün Modülü][3]

<span data-ttu-id="a5592-226">*Şekil 3 '. Merhaba CA günlük analizi veri kümesi ve R betiği yürütün modülü ile deneyin.*</span><span class="sxs-lookup"><span data-stu-id="a5592-226">*Figure 3. hello CA Dairy Analysis experiment with dataset and Execute R Script module.*</span></span>

#### <a name="check-on-hello-data"></a><span data-ttu-id="a5592-227">Merhaba veriyi denetle</span><span class="sxs-lookup"><span data-stu-id="a5592-227">Check on hello data</span></span>
<span data-ttu-id="a5592-228">Şimdi hello veri bizim deneme yüklemiş olduğunuz bir görünüme sahiptir.</span><span class="sxs-lookup"><span data-stu-id="a5592-228">Let's have a look at hello data we have loaded into our experiment.</span></span> <span data-ttu-id="a5592-229">Merhaba denemesinde hello hello çıktısını tıklatın **cadairydata.csv dataset** seçip **görselleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="a5592-229">In hello experiment, click on hello output of hello **cadairydata.csv dataset** and select **visualize**.</span></span> <span data-ttu-id="a5592-230">Şekil 4 gibi bir şey görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a5592-230">You should see something like Figure 4.</span></span>  

![Merhaba cadairydata.csv dataset özeti][4]

<span data-ttu-id="a5592-232">*Şekil 4 '. Merhaba cadairydata.csv dataset özeti.*</span><span class="sxs-lookup"><span data-stu-id="a5592-232">*Figure 4. Summary of hello cadairydata.csv dataset.*</span></span>

<span data-ttu-id="a5592-233">Bu görünümde çok sayıda yararlı bilgiler bakın.</span><span class="sxs-lookup"><span data-stu-id="a5592-233">In this view we see a lot of useful information.</span></span> <span data-ttu-id="a5592-234">Görebiliriz bu veri kümesinin ilk birkaç satır hello.</span><span class="sxs-lookup"><span data-stu-id="a5592-234">We can see hello first several rows of that dataset.</span></span> <span data-ttu-id="a5592-235">Biz bir sütun seçerseniz, hello istatistikleri bölüm hello sütun hakkında daha fazla bilgi gösterir.</span><span class="sxs-lookup"><span data-stu-id="a5592-235">If we select a column, hello Statistics section shows more information about hello column.</span></span> <span data-ttu-id="a5592-236">Örneğin, hello özellik türü satır bize Azure Machine Learning Studio atanmış bir toohello sütun hangi veri türlerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="a5592-236">For example, hello Feature Type row shows us what data types Azure Machine Learning Studio assigned toohello column.</span></span> <span data-ttu-id="a5592-237">Biz toodo herhangi bir önemli iş başlamadan önce bu gibi hızlı bir bakış sahip bir iyi sağlamlık olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="a5592-237">Having a quick look like this is a good sanity check before we start toodo any serious work.</span></span>

### <a name="first-r-script"></a><span data-ttu-id="a5592-238">İlk R betiği</span><span class="sxs-lookup"><span data-stu-id="a5592-238">First R script</span></span>
<span data-ttu-id="a5592-239">Bir basit ilk R betiği tooexperiment ile Azure Machine Learning Studio'da oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="a5592-239">Let's create a simple first R script tooexperiment with in Azure Machine Learning Studio.</span></span> <span data-ttu-id="a5592-240">I oluşturduktan ve Rstudio'dan komut dosyası izleyen hello test.</span><span class="sxs-lookup"><span data-stu-id="a5592-240">I have created and tested hello following script in RStudio.</span></span>  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    str(cadairydata)
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="a5592-241">Bu komut dosyası tooAzure Machine Learning Studio tootransfer ihtiyacım artık.</span><span class="sxs-lookup"><span data-stu-id="a5592-241">Now I need tootransfer this script tooAzure Machine Learning Studio.</span></span> <span data-ttu-id="a5592-242">Yalnızca kesin ve yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a5592-242">I could simply cut and paste.</span></span> <span data-ttu-id="a5592-243">Ancak, bu durumda, ı my R betiği bir zip dosyası aktarın.</span><span class="sxs-lookup"><span data-stu-id="a5592-243">However, in this case, I will transfer my R script via a zip file.</span></span>

### <a name="data-input-toohello-execute-r-script-module"></a><span data-ttu-id="a5592-244">Veri giriş toohello R betiği yürütün Modülü</span><span class="sxs-lookup"><span data-stu-id="a5592-244">Data input toohello Execute R Script module</span></span>
<span data-ttu-id="a5592-245">Şimdi hello girişleri toohello göz sahip [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="a5592-245">Let's have a look at hello inputs toohello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="a5592-246">Bu örnekte, biz hello California Süt veri hello okuyacaksa [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="a5592-246">In this example we will read hello California dairy data into hello [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="a5592-247">Hello için üç olası girişleri vardır [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="a5592-247">There are three possible inputs for hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="a5592-248">Herhangi bir ya da tüm bu girdi, uygulamaya bağlı olarak kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="a5592-248">You may use any one or all of these inputs, depending on your application.</span></span> <span data-ttu-id="a5592-249">Ayrıca, hiçbir giriş hiç alır mükemmel makul toouse bir R komut dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="a5592-249">It is also perfectly reasonable toouse an R script that takes no input at all.</span></span>  

<span data-ttu-id="a5592-250">Her sol tooright giderek bu girdi bakalım.</span><span class="sxs-lookup"><span data-stu-id="a5592-250">Let's look at each of these inputs, going from left tooright.</span></span> <span data-ttu-id="a5592-251">İmleç hello giriş yerleştirme ve hello araç ipucu okuma her hello girdi hello adlarını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5592-251">You can see hello names of each of hello inputs by placing your cursor over hello input and reading hello tooltip.</span></span>  

#### <a name="script-bundle"></a><span data-ttu-id="a5592-252">Komut dosyası paket</span><span class="sxs-lookup"><span data-stu-id="a5592-252">Script Bundle</span></span>
<span data-ttu-id="a5592-253">Merhaba betik paket giriş toopass Merhaba içeriğine bir zip dosyasına sağlar [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="a5592-253">hello Script Bundle input allows you toopass hello contents of a zip file into [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="a5592-254">R kodunuza komutları tooread hello hello ZIP dosyasının içeriğini aşağıdaki hello birini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5592-254">You can use one of hello following commands tooread hello contents of hello zip file into your R code.</span></span>

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> <span data-ttu-id="a5592-255">Azure Machine Learning hello src varsa gibi hello ZIP dosyaları işler / dizini ve bu nedenle, dosya adları bu dizin adı tooprefix gerekir.</span><span class="sxs-lookup"><span data-stu-id="a5592-255">Azure Machine Learning treats files in hello zip as if they are in hello src/ directory, so you need tooprefix your file names with this directory name.</span></span> <span data-ttu-id="a5592-256">Örneğin, hello zip hello dosyaları varsa `yourfile.R` ve `yourData.rdata` hello zip hello kökte olarak adresini `src/yourfile.R` ve `src/yourData.rdata` kullanırken `source` ve `load`.</span><span class="sxs-lookup"><span data-stu-id="a5592-256">For example, if hello zip contains hello files `yourfile.R` and `yourData.rdata` in hello root of hello zip, you would address these as `src/yourfile.R` and `src/yourData.rdata` when using `source` and `load`.</span></span>
> 
> 

<span data-ttu-id="a5592-257">Biz zaten yükleme kümelerinde ele [hello dataset yüklenirken](#loading).</span><span class="sxs-lookup"><span data-stu-id="a5592-257">We already discussed loading datasets in [Loading hello dataset](#loading).</span></span> <span data-ttu-id="a5592-258">Oluşturulan ve hello önceki bölümde gösterilen hello R betiği test sonra aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="a5592-258">Once you have created and tested hello R script shown in hello previous section, do hello following:</span></span>

1. <span data-ttu-id="a5592-259">Merhaba R komut dosyasına kaydedin bir. R dosyası.</span><span class="sxs-lookup"><span data-stu-id="a5592-259">Save hello R script into a .R file.</span></span> <span data-ttu-id="a5592-260">My komut dosyası "simpleplot. çağırın "R".</span><span class="sxs-lookup"><span data-stu-id="a5592-260">I call my script file "simpleplot.R".</span></span> <span data-ttu-id="a5592-261">Merhaba içeriği aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="a5592-261">Here's hello contents.</span></span>
   
        ## Only one of hello following two lines should be used
        ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
        ## If in RStudio, use hello second line with read.csv()
        cadairydata <- maml.mapInputPort(1)
        # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
        str(cadairydata)
        pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
        ## hello following line should be executed only when running in
        ## Azure Machine Learning Studio
        maml.mapOutputPort('cadairydata')
2. <span data-ttu-id="a5592-262">Zip dosyası oluşturun ve komut dosyanızı Bu zip dosyasına kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="a5592-262">Create a zip file and copy your script into this zip file.</span></span> <span data-ttu-id="a5592-263">Windows hello dosyasını sağ tıklatın ve seçin **göndermek**ve ardından **sıkıştırılmış klasörü**.</span><span class="sxs-lookup"><span data-stu-id="a5592-263">On Windows, you can right-click on hello file and select **Send to**, and then **Compressed folder**.</span></span> <span data-ttu-id="a5592-264">Bu hello "simpleplot. içeren yeni bir zip dosyası oluşturur R"dosyası.</span><span class="sxs-lookup"><span data-stu-id="a5592-264">This will create a new zip file containing hello "simpleplot.R" file.</span></span>
3. <span data-ttu-id="a5592-265">Dosya toohello ekleme **veri kümeleri** hello türü olarak belirterek Machine Learning Studio'daki **zip**.</span><span class="sxs-lookup"><span data-stu-id="a5592-265">Add your file toohello **datasets** in Machine Learning Studio, specifying hello type as **zip**.</span></span> <span data-ttu-id="a5592-266">Şimdi, veri kümelerinde hello zip dosyası görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a5592-266">You should now see hello zip file in your datasets.</span></span>
4. <span data-ttu-id="a5592-267">Sürükle ve bırak hello zip dosyasından **veri kümeleri** hello üzerine **ML Studio tuvale**.</span><span class="sxs-lookup"><span data-stu-id="a5592-267">Drag and drop hello zip file from **datasets** onto hello **ML Studio canvas**.</span></span>
5. <span data-ttu-id="a5592-268">Merhaba Hello çıkışına bağlayın **zip veri** simgesi toohello **betik paket** Merhaba, giriş [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="a5592-268">Connect hello output of hello **zip data** icon toohello **Script Bundle** input of hello [Execute R Script][execute-r-script] module.</span></span>
6. <span data-ttu-id="a5592-269">Türü hello `source()` zip dosyası hello kod penceresine için adınızı hello işleviyle [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="a5592-269">Type hello `source()` function with your zip file name into hello code window for hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="a5592-270">My durumda yazdım `source("src/simpleplot.R")`.</span><span class="sxs-lookup"><span data-stu-id="a5592-270">In my case I typed `source("src/simpleplot.R")`.</span></span>  
7. <span data-ttu-id="a5592-271">Tıklattığınız emin olun **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="a5592-271">Make sure you click **Save**.</span></span>

<span data-ttu-id="a5592-272">Bu adımları tamamlandıktan sonra hello [R betiği yürütün] [ execute-r-script] modülü yürütülecek hello R betiği hello zip dosyasında hello deneme çalıştırdığınızda.</span><span class="sxs-lookup"><span data-stu-id="a5592-272">Once these steps are complete, hello [Execute R Script][execute-r-script] module will execute hello R script in hello zip file when hello experiment is run.</span></span> <span data-ttu-id="a5592-273">Bu noktada denemenizi Şekil 5 gibi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="a5592-273">At this point your experiment should look something like Figure 5.</span></span>

![Daraltılmış R betiği kullanmayı deneyin][6]

<span data-ttu-id="a5592-275">*Şekil 5. Daraltılmış R betiği kullanmayı deneyin.*</span><span class="sxs-lookup"><span data-stu-id="a5592-275">*Figure 5. Experiment using zipped R script.*</span></span>

#### <a name="dataset1"></a><span data-ttu-id="a5592-276">DataSet1</span><span class="sxs-lookup"><span data-stu-id="a5592-276">Dataset1</span></span>
<span data-ttu-id="a5592-277">Merhaba Dataset1 giriş kullanarak verileri tooyour R kodu dikdörtgen tablosu geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5592-277">You can pass a rectangular table of data tooyour R code by using hello Dataset1 input.</span></span> <span data-ttu-id="a5592-278">Bizim basit bir komut dosyası hello içinde `maml.mapInputPort(1)` işlevi, bağlantı noktası 1 hello verileri okur.</span><span class="sxs-lookup"><span data-stu-id="a5592-278">In our simple script hello `maml.mapInputPort(1)` function reads hello data from port 1.</span></span> <span data-ttu-id="a5592-279">Bu verileri daha sonra kodunuzda tooa dataframe değişken adı atanır.</span><span class="sxs-lookup"><span data-stu-id="a5592-279">This data is then assigned tooa dataframe variable name in your code.</span></span> <span data-ttu-id="a5592-280">Bizim basit komut dosyasında kodun ilk satırı hello hello atama gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="a5592-280">In our simple script hello first line of code performs hello assignment.</span></span>

    cadairydata <- maml.mapInputPort(1)

<span data-ttu-id="a5592-281">Merhaba üzerinde tıklayarak denemenizin yürütme **çalıştırmak** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a5592-281">Execute your experiment by clicking on hello **Run** button.</span></span> <span data-ttu-id="a5592-282">Merhaba üzerinde Hello yürütme bittiğinde, bilgisayarınızı [R betiği yürütün] [ execute-r-script] modülü ve ardından **çıkış Günlüğü Görüntüle** hello Özellikler bölmesi.</span><span class="sxs-lookup"><span data-stu-id="a5592-282">When hello execution finishes, click on hello [Execute R Script][execute-r-script] module and then click **View output log** on hello properties pane.</span></span> <span data-ttu-id="a5592-283">Yeni bir sayfa hello hello içeren dosyanın içeriğini gösteren tarayıcınızda görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a5592-283">A new page should appear in your browser showing hello contents of hello output.log file.</span></span> <span data-ttu-id="a5592-284">Aşağı kaydırma yaptığınızda hello aşağıdaki gibi bir şey görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a5592-284">When you scroll down you should see something like hello following.</span></span>

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

<span data-ttu-id="a5592-285">Uzağa hello hello aşağıdaki gibi bir şey görünecektir hello sütunlar üzerinde daha ayrıntılı bilgi sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="a5592-285">Farther down hello page is more detailed information on hello columns, which will look something like hello following.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput]
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput]
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month            : chr  "Jan" "Feb" "Mar" "Apr" ...
    [ModuleOutput]
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput]
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput]
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput]
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...

<span data-ttu-id="a5592-286">Bu sonuçları 228 gözlemleri ve hello dataframe 9 sütunlarında beklendiği gibi genellikle olur.</span><span class="sxs-lookup"><span data-stu-id="a5592-286">These results are mostly as expected, with 228 observations and 9 columns in hello dataframe.</span></span> <span data-ttu-id="a5592-287">Merhaba sütun adları, hello R veri türü ve her sütunun bir örnek görebiliriz.</span><span class="sxs-lookup"><span data-stu-id="a5592-287">We can see hello column names, hello R data type and a sample of each column.</span></span>

> [!NOTE]
> <span data-ttu-id="a5592-288">Bu aynı çıktılar rahat hello R aygıt çıktısını hello kullanılabilir [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="a5592-288">This same printed output is conveniently available from hello R Device output of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="a5592-289">Merhaba hello çıkışları aşağıdakiler ele alınacaktır [R betiği yürütün] [ execute-r-script] hello sonraki bölümde modülü.</span><span class="sxs-lookup"><span data-stu-id="a5592-289">We will discuss hello outputs of hello [Execute R Script][execute-r-script] module in hello next section.</span></span>  
> 
> 

#### <a name="dataset2"></a><span data-ttu-id="a5592-290">Dataset2</span><span class="sxs-lookup"><span data-stu-id="a5592-290">Dataset2</span></span>
<span data-ttu-id="a5592-291">Merhaba hello Dataset2 giriş Dataset1, aynı toothat davranıştır.</span><span class="sxs-lookup"><span data-stu-id="a5592-291">hello behavior of hello Dataset2 input is identical toothat of Dataset1.</span></span> <span data-ttu-id="a5592-292">Bu girdi kullanarak R kodunuza ikinci bir dikdörtgen tablo veri geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5592-292">Using this input you can pass a second rectangular table of data into your R code.</span></span> <span data-ttu-id="a5592-293">Merhaba işlevi `maml.mapInputPort(2)`, 2 hello bağımsız değişkeniyle, kullanılan toopass bu verilerdir.</span><span class="sxs-lookup"><span data-stu-id="a5592-293">hello function `maml.mapInputPort(2)`, with hello argument 2, is used toopass this data.</span></span>  

### <a name="execute-r-script-outputs"></a><span data-ttu-id="a5592-294">R betiği çıkışları yürütme</span><span class="sxs-lookup"><span data-stu-id="a5592-294">Execute R Script outputs</span></span>
#### <a name="output-a-dataframe"></a><span data-ttu-id="a5592-295">Bir dataframe çıkış</span><span class="sxs-lookup"><span data-stu-id="a5592-295">Output a dataframe</span></span>
<span data-ttu-id="a5592-296">Hello kullanarak hello sonuç Dataset1 bağlantı noktası üzerinden dikdörtgen tablo olarak bir R dataframe Merhaba içeriğine çıkarabilirsiniz `maml.mapOutputPort()` işlevi.</span><span class="sxs-lookup"><span data-stu-id="a5592-296">You can output hello contents of an R dataframe as a rectangular table through hello Result Dataset1 port by using hello `maml.mapOutputPort()` function.</span></span> <span data-ttu-id="a5592-297">Bizim basit R betiği bu satırı aşağıdaki hello tarafından gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a5592-297">In our simple R script this is performed by hello following line.</span></span>

    maml.mapOutputPort('cadairydata')

<span data-ttu-id="a5592-298">Çalışan hello deneme sonrasında hello üzerinde sonuç Dataset1 çıkış bağlantı noktasına tıklayın ve tıklayın **Görselleştir**.</span><span class="sxs-lookup"><span data-stu-id="a5592-298">After running hello experiment, click on hello Result Dataset1 output port and then click on **Visualize**.</span></span> <span data-ttu-id="a5592-299">Şekil 6 gibi bir şey görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a5592-299">You should see something like Figure 6.</span></span>

![Merhaba görsel olarak hello California Süt veri hello çıktısı][7]

<span data-ttu-id="a5592-301">*Şekil 6. Merhaba California Süt veri hello çıktısını Hello görselleştirme.*</span><span class="sxs-lookup"><span data-stu-id="a5592-301">*Figure 6. hello visualization of hello output of hello California dairy data.*</span></span>

<span data-ttu-id="a5592-302">Bu çıktı bekliyorduk tam olarak aynı toohello giriş arar.</span><span class="sxs-lookup"><span data-stu-id="a5592-302">This output looks identical toohello input, exactly as we expected.</span></span>  

### <a name="r-device-output"></a><span data-ttu-id="a5592-303">R cihaz çıktısı</span><span class="sxs-lookup"><span data-stu-id="a5592-303">R Device output</span></span>
<span data-ttu-id="a5592-304">Merhaba aygıt çıktısını hello [R betiği yürütün] [ execute-r-script] modülü iletileri ve grafik çıktısı içerir.</span><span class="sxs-lookup"><span data-stu-id="a5592-304">hello Device output of hello [Execute R Script][execute-r-script] module contains messages and graphics output.</span></span> <span data-ttu-id="a5592-305">Her iki standart çıktı ve standart hata iletilerden R toohello R aygıt çıkış bağlantı noktasına gönderilir.</span><span class="sxs-lookup"><span data-stu-id="a5592-305">Both standard output and standard error messages from R are sent toohello R Device output port.</span></span>  

<span data-ttu-id="a5592-306">tooview hello R çıkışı, cihaz tıklatın hello bağlantı noktası ve ardından **Görselleştir**.</span><span class="sxs-lookup"><span data-stu-id="a5592-306">tooview hello R Device output, click on hello port and then on **Visualize**.</span></span> <span data-ttu-id="a5592-307">Biz hello standart çıktı ve standart hata Şekil 7'de hello R betikten bakın.</span><span class="sxs-lookup"><span data-stu-id="a5592-307">We see hello standard output and standard error from hello R script in Figure 7.</span></span>

![Standart çıktı ve standart hata hello R aygıtı bağlantı noktası][8]

<span data-ttu-id="a5592-309">*Şekil 7. Standart çıktı ve standart hata hello R aygıtı bağlantı noktası.*</span><span class="sxs-lookup"><span data-stu-id="a5592-309">*Figure 7. Standard output and standard error from hello R Device port.*</span></span>

<span data-ttu-id="a5592-310">Bkz: Şekil 8'deki bizim R betiği hello grafik çıktısı biz kaydırma.</span><span class="sxs-lookup"><span data-stu-id="a5592-310">Scrolling down we see hello graphics output from our R script in Figure 8.</span></span>  

![Grafik çıktısı hello R aygıtı bağlantı noktası][9]

<span data-ttu-id="a5592-312">*Şekil 8'de. R aygıtı bağlantı noktası Hello çıktı grafik.*</span><span class="sxs-lookup"><span data-stu-id="a5592-312">*Figure 8. Graphics output from hello R Device port.*</span></span>  

## <span data-ttu-id="a5592-313"><a id="filtering"></a>Verileri filtreleme ve dönüştürme</span><span class="sxs-lookup"><span data-stu-id="a5592-313"><a id="filtering"></a>Data filtering and transformation</span></span>
<span data-ttu-id="a5592-314">Bu bölümde biz bazı temel verileri filtreleme ve hello California Süt veri dönüştürme işlemlerini gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="a5592-314">In this section we will perform some basic data filtering and transformation operations on hello California dairy data.</span></span> <span data-ttu-id="a5592-315">Bu bölümde Hello ucu tarafından analitik bir model oluşturmak için uygun bir biçim biz veri sahip olur.</span><span class="sxs-lookup"><span data-stu-id="a5592-315">By hello end of this section we will have data in a format suitable for building an analytic model.</span></span>  

<span data-ttu-id="a5592-316">Daha açık belirtmek gerekirse, bu bölümde birkaç ortak veri temizleme ve dönüştürme görevleri gerçekleştiririz: tür dönüştürme, yeni hesaplanan sütunlar ekleme dataframes üzerinde filtreleme ve değer dönüşümler.</span><span class="sxs-lookup"><span data-stu-id="a5592-316">More specifically, in this section we will perform several common data cleaning and transformation tasks: type transformation, filtering on dataframes, adding new computed columns, and value transformations.</span></span> <span data-ttu-id="a5592-317">Bu arka plan gerçek dünyadaki sorunları karşılaştı pek çok Çeşitleme hello ile ilgilenir yardımcı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a5592-317">This background should help you deal with hello many variations encountered in real-world problems.</span></span>

<span data-ttu-id="a5592-318">Bu bölüm için tam R kod Hello hello zip dosyasında daha önce indirdiğiniz kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a5592-318">hello complete R code for this section is available in hello zip file you downloaded earlier.</span></span>

### <a name="type-transformations"></a><span data-ttu-id="a5592-319">Tür dönüştürmeleri</span><span class="sxs-lookup"><span data-stu-id="a5592-319">Type transformations</span></span>
<span data-ttu-id="a5592-320">Biz hello hello R koda hello California Süt verileri okuyabilir göre [R betiği yürütün] [ execute-r-script] modül ihtiyacımız hello sütunlardaki hello verileri hedeflenen hello türünü ve biçimini olduğunu tooensure.</span><span class="sxs-lookup"><span data-stu-id="a5592-320">Now that we can read hello California dairy data into hello R code in hello [Execute R Script][execute-r-script] module, we need tooensure that hello data in hello columns has hello intended type and format.</span></span>  

<span data-ttu-id="a5592-321">R veri türleri gerektiği gibi bir tooanother gelen yüklenen anlamına gelir dinamik olarak yazılan bir dildir.</span><span class="sxs-lookup"><span data-stu-id="a5592-321">R is a dynamically typed language, which means that data types are coerced from one tooanother as required.</span></span> <span data-ttu-id="a5592-322">R Hello atomik veri türü sayısal, mantıksal ve karakter içerir.</span><span class="sxs-lookup"><span data-stu-id="a5592-322">hello atomic data types in R include numeric, logical and character.</span></span> <span data-ttu-id="a5592-323">Merhaba faktörü kullanılan toocompactly deposu kategorik veri türüdür.</span><span class="sxs-lookup"><span data-stu-id="a5592-323">hello factor type is used toocompactly store categorical data.</span></span> <span data-ttu-id="a5592-324">Merhaba başvurularında veri türleri hakkında daha fazla bilgi bulabilirsiniz [ek B - daha fazla bilgi](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="a5592-324">You can find much more information on data types in hello references in [Appendix B - Further reading](#appendixb).</span></span>

<span data-ttu-id="a5592-325">Tablo verisi R bir dış kaynaktan içine okunduğunda her zaman hello sütunları türlerinde kaynaklanan bir fikir toocheck hello gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="a5592-325">When tabular data is read into R from an external source, it is always a good idea toocheck hello resulting types in hello columns.</span></span> <span data-ttu-id="a5592-326">Bir sütun türü karakterinin isteyebilirsiniz, ancak çoğu durumda bu faktör olarak (veya tersi) görünür.</span><span class="sxs-lookup"><span data-stu-id="a5592-326">You may want a column of type character, but in many cases this will show up as factor or vice versa.</span></span> <span data-ttu-id="a5592-327">Diğer durumlarda bir sütun olması düşündüğünüz sayısal karakter verileri tarafından örneğin temsil edilir bir kayan olarak 1,23 yerine '1,23' nokta sayısı.</span><span class="sxs-lookup"><span data-stu-id="a5592-327">In other cases a column you think should be numeric is represented by character data, e.g. '1.23' rather than 1.23 as a floating point number.</span></span>  

<span data-ttu-id="a5592-328">Neyse ki, eşleme mümkündür sürece kolay tooconvert bir türü tooanother değildir.</span><span class="sxs-lookup"><span data-stu-id="a5592-328">Fortunately, it is easy tooconvert one type tooanother, as long as mapping is possible.</span></span> <span data-ttu-id="a5592-329">Örneğin, sayısal bir değer 'Nevada'ya' dönüştürülemiyor ancak tooa faktörü (kategorik değişken) dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5592-329">For example, you cannot convert 'Nevada' into a numeric value, but you can convert it tooa factor (categorical variable).</span></span> <span data-ttu-id="a5592-330">Başka bir örnek olarak, bir karakter '1' ya da bir faktör sayısal 1 dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5592-330">As another example, you can convert a numeric 1 into a character '1' or a factor.</span></span>  

<span data-ttu-id="a5592-331">Merhaba diziminin dönüştürmeler basittir: `as.datatype()`.</span><span class="sxs-lookup"><span data-stu-id="a5592-331">hello syntax for any of these conversions is simple: `as.datatype()`.</span></span> <span data-ttu-id="a5592-332">Bu tür dönüştürme işlevleri hello şunları içerir.</span><span class="sxs-lookup"><span data-stu-id="a5592-332">These type conversion functions include hello following.</span></span>

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

<span data-ttu-id="a5592-333">Merhaba önceki bölümde giriyoruz hello sütunların veri türlerini hello bakarak: türü sayısal, türü karakteri olan'Month ' etiketli hello sütun dışında tüm sütunlar:.</span><span class="sxs-lookup"><span data-stu-id="a5592-333">Looking at hello data types of hello columns we input in hello previous section: all columns are of type numeric, except for hello column labeled 'Month', which is of type character.</span></span> <span data-ttu-id="a5592-334">Şimdi bu tooa faktörü dönüştürün ve test hello sonuçları.</span><span class="sxs-lookup"><span data-stu-id="a5592-334">Let's convert this tooa factor and test hello results.</span></span>  

<span data-ttu-id="a5592-335">Merhaba scatterplot matris oluşturulur ve hello 'Month' sütun tooa faktörü dönüştürme bir satır eklenir hello satır silindi.</span><span class="sxs-lookup"><span data-stu-id="a5592-335">I have deleted hello line that created hello scatterplot matrix and added a line converting hello 'Month' column tooa factor.</span></span> <span data-ttu-id="a5592-336">Denememe t yalnızca hello R kod kesip hello kod penceresine hello [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="a5592-336">In my experiment I will just cut and paste hello R code into hello code window of hello [Execute R Script][execute-r-script] Module.</span></span> <span data-ttu-id="a5592-337">Ayrıca hello zip dosyasını güncelleştirme ve tooAzure Machine Learning Studio karşıya yükleme, ancak bu çeşitli adımları gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="a5592-337">You could also update hello zip file and upload it tooAzure Machine Learning Studio, but this takes several steps.</span></span>  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(cadairydata$Month)
    str(cadairydata) # Check hello result
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="a5592-338">Şimdi bu kodu yürütür ve hello R betiği için hello çıktı günlüğüne bakın.</span><span class="sxs-lookup"><span data-stu-id="a5592-338">Let's execute this code and look at hello output log for hello R script.</span></span> <span data-ttu-id="a5592-339">Şekil 9'Hello ilgili verileri hello günlüğünden gösterilir.</span><span class="sxs-lookup"><span data-stu-id="a5592-339">hello relevant data from hello log is shown in Figure 9.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 14 levels "Apr","April",..: 6 5 9 1 11 8 7 3 14 13 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="a5592-340">*Şekil 9. Merhaba dataframe faktörü değişkeniyle özeti.*</span><span class="sxs-lookup"><span data-stu-id="a5592-340">*Figure 9. Summary of hello dataframe with a factor variable.*</span></span>

<span data-ttu-id="a5592-341">Merhaba türü ay için şimdi söyleyin '**14 düzeyleri içeren faktörü**'.</span><span class="sxs-lookup"><span data-stu-id="a5592-341">hello type for Month should now say '**Factor w/ 14 levels**'.</span></span> <span data-ttu-id="a5592-342">Merhaba yıl içinde yalnızca 12 ay olduğundan bu bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="a5592-342">This is a problem since there are only 12 months in hello year.</span></span> <span data-ttu-id="a5592-343">Türü hello toosee kontrol edebilirsiniz, **Görselleştir** hello sonuç veri kümesi bağlantı noktası olduğundan '**Categorical**'.</span><span class="sxs-lookup"><span data-stu-id="a5592-343">You can also check toosee that hello type in **Visualize** of hello Result Dataset port is '**Categorical**'.</span></span>

<span data-ttu-id="a5592-344">Merhaba, bu sütun sistematik olarak kodlanmış değil'Month ' hello sorunudur.</span><span class="sxs-lookup"><span data-stu-id="a5592-344">hello problem is that hello 'Month' column has not been coded systematically.</span></span> <span data-ttu-id="a5592-345">Bazı durumlarda bir ay Nisan adı verilir ve diğerleri Apr kısaltılır. Merhaba dize too3 karakterleri kırpma tarafından size bu sorunu çözebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5592-345">In some cases a month is called April and in others it is abbreviated as Apr. We can solve this problem by trimming hello string too3 characters.</span></span> <span data-ttu-id="a5592-346">Merhaba satırlık bir kod artık hello aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="a5592-346">hello line of code now looks like hello following:</span></span>

    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

<span data-ttu-id="a5592-347">Merhaba deneme yeniden çalıştırın ve hello çıktı günlüğüne bakın.</span><span class="sxs-lookup"><span data-stu-id="a5592-347">Rerun hello experiment and view hello output log.</span></span> <span data-ttu-id="a5592-348">Merhaba, sonuçları Şekil 10'da gösterilen bekleniyordu.</span><span class="sxs-lookup"><span data-stu-id="a5592-348">hello expected results are shown in Figure 10.</span></span>  

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="a5592-349">*Şekil 10. Merhaba dataframe faktörü düzeyleri doğru sayısıyla özeti.*</span><span class="sxs-lookup"><span data-stu-id="a5592-349">*Figure 10. Summary of hello dataframe with correct number of factor levels.*</span></span>

<span data-ttu-id="a5592-350">Bizim faktörü değişkeni istenen hello 12 düzeyleri artık sahiptir.</span><span class="sxs-lookup"><span data-stu-id="a5592-350">Our factor variable now has hello desired 12 levels.</span></span>

### <a name="basic-data-frame-filtering"></a><span data-ttu-id="a5592-351">Çerçeve temel verileri filtreleme</span><span class="sxs-lookup"><span data-stu-id="a5592-351">Basic data frame filtering</span></span>
<span data-ttu-id="a5592-352">R dataframes güçlü filtreleme yetenekleri için destek.</span><span class="sxs-lookup"><span data-stu-id="a5592-352">R dataframes support powerful filtering capabilities.</span></span> <span data-ttu-id="a5592-353">Veri kümeleri, satır veya sütun üzerinde mantıksal filtreleri kullanarak alt kümelenmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="a5592-353">Datasets can be subsetted by using logical filters on either rows or columns.</span></span> <span data-ttu-id="a5592-354">Çoğu durumda, karmaşık filtre ölçütlerini gerekli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a5592-354">In many cases, complex filter criteria will be required.</span></span> <span data-ttu-id="a5592-355">Merhaba başvuran [ek B - daha fazla bilgi](#appendixb) dataframes filtreleme kapsamlı örnekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="a5592-355">hello references in [Appendix B - Further reading](#appendixb) contain extensive examples of filtering dataframes.</span></span>  

<span data-ttu-id="a5592-356">Bir bit yoktur filtre biz kümemize üzerinde yapmalısınız.</span><span class="sxs-lookup"><span data-stu-id="a5592-356">There is one bit of filtering we should do on our dataset.</span></span> <span data-ttu-id="a5592-357">Merhaba cadairydata dataframe hello sütunlarında bakarsanız, iki gereksiz sütunları görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="a5592-357">If you look at hello columns in hello cadairydata dataframe, you will see two unnecessary columns.</span></span> <span data-ttu-id="a5592-358">Merhaba ilk sütun yalnızca çok kullanışlı değil bir satır numarası tutar.</span><span class="sxs-lookup"><span data-stu-id="a5592-358">hello first column just holds a row number, which is not very useful.</span></span> <span data-ttu-id="a5592-359">Merhaba ikinci sütun, Year.Month, yedek bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="a5592-359">hello second column, Year.Month, contains redundant information.</span></span> <span data-ttu-id="a5592-360">Biz kolayca bu sütunları R koddan hello kullanarak hariç tutabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5592-360">We can easily exclude these columns by using hello following R code.</span></span>

> [!NOTE]
> <span data-ttu-id="a5592-361">Üzerinde bu bölümde, ı yalnızca gösterecektir artık gelen, ı hello ekleme ek kod hello [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="a5592-361">From now on in this section, I will just show you hello additional code I am adding in hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="a5592-362">Her yeni satır ekleyeceğim **önce** hello `str()` işlevi.</span><span class="sxs-lookup"><span data-stu-id="a5592-362">I will add each new line **before** hello `str()` function.</span></span> <span data-ttu-id="a5592-363">Bu işlev tooverify Azure Machine Learning Studio'da my sonuçları kullanın.</span><span class="sxs-lookup"><span data-stu-id="a5592-363">I use this function tooverify my results in Azure Machine Learning Studio.</span></span>
> 
> 

<span data-ttu-id="a5592-364">Satır toomy R kodu hello hello eklemek [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="a5592-364">I add hello following line toomy R code in hello [Execute R Script][execute-r-script] module.</span></span>

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

<span data-ttu-id="a5592-365">Denemenizde bu kodu çalıştırmak ve hello sonucundan hello çıktı günlüğüne bakın.</span><span class="sxs-lookup"><span data-stu-id="a5592-365">Run this code in your experiment and check hello result from hello output log.</span></span> <span data-ttu-id="a5592-366">Bu sonuçları Şekil 11'de gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a5592-366">These results are shown in Figure 11.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  7 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="a5592-367">*Şekil 11. İki sütun ile Merhaba dataframe özetini kaldırıldı.*</span><span class="sxs-lookup"><span data-stu-id="a5592-367">*Figure 11. Summary of hello dataframe with two columns removed.*</span></span>

<span data-ttu-id="a5592-368">İyi haber!</span><span class="sxs-lookup"><span data-stu-id="a5592-368">Good news!</span></span> <span data-ttu-id="a5592-369">Biz hello beklenen sonuçları alın.</span><span class="sxs-lookup"><span data-stu-id="a5592-369">We get hello expected results.</span></span>

### <a name="add-a-new-column"></a><span data-ttu-id="a5592-370">Yeni bir sütun ekleyin</span><span class="sxs-lookup"><span data-stu-id="a5592-370">Add a new column</span></span>
<span data-ttu-id="a5592-371">toocreate zaman serisi modeli içeren bir sütun hello aydan hello zaman serisi hello başlangıcı beri uygun toohave olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a5592-371">toocreate time series models it will be convenient toohave a column containing hello months since hello start of hello time series.</span></span> <span data-ttu-id="a5592-372">Yeni bir sütun 'Month.Count' oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="a5592-372">We will create a new column 'Month.Count'.</span></span>

<span data-ttu-id="a5592-373">toohelp biz bizim ilk basit işlevi oluşturacak hello kod düzenleme `num.month()`.</span><span class="sxs-lookup"><span data-stu-id="a5592-373">toohelp organize hello code we will create our first simple function, `num.month()`.</span></span> <span data-ttu-id="a5592-374">Biz bu işlevi toocreate hello dataframe yeni bir sütunda sonra uygulanır.</span><span class="sxs-lookup"><span data-stu-id="a5592-374">We will then apply this function toocreate a new column in hello dataframe.</span></span> <span data-ttu-id="a5592-375">Merhaba yeni kod aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="a5592-375">hello new code is as follows.</span></span>

    ## Create a new column with hello month count
    ## Function toofind hello number of months from hello first
    ## month of hello time series
    num.month <- function(Year, Month) {
      ## Find hello starting year
      min.year  <- min(Year)

      ## Compute hello number of months from hello start of hello time series
      12 * (Year - min.year) + Month - 1
    }

    ## Compute hello new column for hello dataframe
    cadairydata$Month.Count <- num.month(cadairydata$Year, cadairydata$Month.Number)

<span data-ttu-id="a5592-376">Şimdi güncelleştirilmiş hello denemeyi çalıştırın ve hello çıktı günlük tooview hello sonuçları kullanın.</span><span class="sxs-lookup"><span data-stu-id="a5592-376">Now run hello updated experiment and use hello output log tooview hello results.</span></span> <span data-ttu-id="a5592-377">Şekil 12'de bu sonuçları gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a5592-377">These results are shown in Figure 12.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="a5592-378">*Şekil 12. Merhaba dataframe hello ek sütunla özeti.*</span><span class="sxs-lookup"><span data-stu-id="a5592-378">*Figure 12. Summary of hello dataframe with hello additional column.*</span></span>

<span data-ttu-id="a5592-379">Her şey çalışıyor gibi görünüyor.</span><span class="sxs-lookup"><span data-stu-id="a5592-379">It looks like everything is working.</span></span> <span data-ttu-id="a5592-380">Bizim dataframe yeni bir sütun hello hello beklenen değerlerle sahibiz.</span><span class="sxs-lookup"><span data-stu-id="a5592-380">We have hello new column with hello expected values in our dataframe.</span></span>

### <a name="value-transformations"></a><span data-ttu-id="a5592-381">Değer dönüşümler</span><span class="sxs-lookup"><span data-stu-id="a5592-381">Value transformations</span></span>
<span data-ttu-id="a5592-382">Bu bölümde biz bizim dataframe hello sütunlarının bazıları hello değerleri bazı basit dönüşümleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="a5592-382">In this section we will perform some simple transformations on hello values in some of hello columns of our dataframe.</span></span> <span data-ttu-id="a5592-383">Merhaba R dil neredeyse rastgele değeri dönüşümleri destekler.</span><span class="sxs-lookup"><span data-stu-id="a5592-383">hello R language supports nearly arbitrary value transformations.</span></span> <span data-ttu-id="a5592-384">Merhaba başvuran [ek B - daha fazla bilgi](#appendixb) kapsamlı örnekler içeriyor.</span><span class="sxs-lookup"><span data-stu-id="a5592-384">hello references in [Appendix B - Further Reading](#appendixb) contain extensive examples.</span></span>

<span data-ttu-id="a5592-385">Bizim dataframe hello özetlerini hello değerleri bakarsanız tek bir şey burada görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a5592-385">If you look at hello values in hello summaries of our dataframe you should see something odd here.</span></span> <span data-ttu-id="a5592-386">Daha fazla dondurma sütlü daha İzmir'de oluşturulur?</span><span class="sxs-lookup"><span data-stu-id="a5592-386">Is more ice cream than milk produced in California?</span></span> <span data-ttu-id="a5592-387">Bu hiçbir mantıklı gibi Hayır, Kuşkusuz bu olgu olarak üzücü toosome bizi dondurma lovers olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="a5592-387">No, of course not, as this makes no sense, sad as this fact may be toosome of us ice cream lovers.</span></span> <span data-ttu-id="a5592-388">Merhaba birimleri farklıdır.</span><span class="sxs-lookup"><span data-stu-id="a5592-388">hello units are different.</span></span> <span data-ttu-id="a5592-389">Merhaba birimleri BİZE pound, olan 1 M birimlerinde ABD pound, dondurma 1.000 birimlerinde BİZE galon ve cottage Peynir 1.000 ABD pound birimlerinde sütlü fiyatıdır.</span><span class="sxs-lookup"><span data-stu-id="a5592-389">hello price is in units of US pounds, milk is in units of 1 M US pounds, ice cream is in units of 1,000 US gallons, and cottage cheese is in units of 1,000 US pounds.</span></span> <span data-ttu-id="a5592-390">Dondurma hafiftir galon başına yaklaşık 6.5 pound varsayıldığında, biz kolayca tüm eşit, biriminde 1.000 pound; bu nedenle bu değerleri çarpma tooconvert hello.</span><span class="sxs-lookup"><span data-stu-id="a5592-390">Assuming ice cream weighs about 6.5 pounds per gallon, we can easily do hello multiplication tooconvert these values so they are all in equal units of 1,000 pounds.</span></span>

<span data-ttu-id="a5592-391">Tahmin modelimiz için çarpma modeli eğilim ve bu verileri Mevsimlik düzeltilmesi için kullanırız.</span><span class="sxs-lookup"><span data-stu-id="a5592-391">For our forecasting model we use a multiplicative model for trend and seasonal adjustment of this data.</span></span> <span data-ttu-id="a5592-392">Bir günlük dönüştürmesi bize toouse bu işlem basitleştirme doğrusal bir model sağlar.</span><span class="sxs-lookup"><span data-stu-id="a5592-392">A log transformation allows us toouse a linear model, simplifying this process.</span></span> <span data-ttu-id="a5592-393">Biz hello günlük aynı hello çarpanı burada uygulanan işlevi hello dönüşümünde uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5592-393">We can apply hello log transformation in hello same function where hello multiplier is applied.</span></span>

<span data-ttu-id="a5592-394">Koddan hello ı yeni bir işlev tanımlayın `log.transform()`ve hello sayısal değerleri içeren toohello satırları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="a5592-394">In hello following code, I define a new function, `log.transform()`, and apply it toohello rows containing hello numerical values.</span></span> <span data-ttu-id="a5592-395">Merhaba R `Map()` işlevidir kullanılan tooapply hello `log.transform()` işlevi toohello seçili hello dataframe sütunlarının.</span><span class="sxs-lookup"><span data-stu-id="a5592-395">hello R `Map()` function is used tooapply hello `log.transform()` function toohello selected columns of hello dataframe.</span></span> <span data-ttu-id="a5592-396">`Map()`çok benzer`apply()` ancak bağımsız değişken toohello işlevi birden fazla listesini verir.</span><span class="sxs-lookup"><span data-stu-id="a5592-396">`Map()` is similar too`apply()` but allows for more than one list of arguments toohello function.</span></span> <span data-ttu-id="a5592-397">Not çarpanları listesini hello ikinci bağımsız değişkeni toohello sağlayan `log.transform()` işlevi.</span><span class="sxs-lookup"><span data-stu-id="a5592-397">Note that a list of multipliers supplies hello second argument toohello `log.transform()` function.</span></span> <span data-ttu-id="a5592-398">Merhaba `na.omit()` işlevi bir bit temizleme tooensure biz eksik yok veya tanımsız değerlerde hello dataframe olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a5592-398">hello `na.omit()` function is used as a bit of cleanup tooensure we do not have missing or undefined values in hello dataframe.</span></span>

    log.transform <- function(invec, multiplier = 1) {
      ## Function for hello transformation, which is hello log
      ## of hello input value times a multiplier

      warningmessages <- c("ERROR: Non-numeric argument encountered in function log.transform",
                           "ERROR: Arguments toofunction log.transform must be greate than zero",
                           "ERROR: Aggurment multiplier toofuncition log.transform must be a scaler",
                           "ERROR: Invalid time seies value encountered in function log.transform"
                           )

      ## Check hello input arguments
      if(!is.numeric(invec) | !is.numeric(multiplier)) {warning(warningmessages[1]); return(NA)}  
      if(any(invec < 0.0) | any(multiplier < 0.0)) {warning(warningmessages[2]); return(NA)}
      if(length(multiplier) != 1) {{warning(warningmessages[3]); return(NA)}}

      ## Wrap hello multiplication in tryCatch
      ## If there is an exception, print hello warningmessage to
      ## standard error and return NA
      tryCatch(log(multiplier * invec),
               error = function(e){warning(warningmessages[4]); NA})
    }


    ## Apply hello transformation function toohello 4 columns
    ## of hello dataframe with production data
    multipliers  <- list(1.0, 6.5, 1000.0, 1000.0)
    cadairydata[, 4:7] <- Map(log.transform, cadairydata[, 4:7], multipliers)

    ## Get rid of any rows with NA values
    cadairydata <- na.omit(cadairydata)  

<span data-ttu-id="a5592-399">Merhaba içinde oldukça bit oluşmasını yoktur `log.transform()` işlevi.</span><span class="sxs-lookup"><span data-stu-id="a5592-399">There is quite a bit happening in hello `log.transform()` function.</span></span> <span data-ttu-id="a5592-400">Bu kod çoğu hello bağımsız değişkenleri ile ilgili olası sorunları denetleme veya hala hello hesaplamalar sırasında ortaya çıkabilecek özel durumlarla birlikte ele alma.</span><span class="sxs-lookup"><span data-stu-id="a5592-400">Most of this code is checking for potential problems with hello arguments or dealing with exceptions, which can still arise during hello computations.</span></span> <span data-ttu-id="a5592-401">Bu kod yalnızca birkaç satırlık gerçekte hesaplamalar hello.</span><span class="sxs-lookup"><span data-stu-id="a5592-401">Only a few lines of this code actually do hello computations.</span></span>

<span data-ttu-id="a5592-402">Merhaba hello savunma programlama tooprevent hello hata işleme devam etmesini engelleyen tek bir işlevin hedefidir.</span><span class="sxs-lookup"><span data-stu-id="a5592-402">hello goal of hello defensive programming is tooprevent hello failure of a single function that prevents processing from continuing.</span></span> <span data-ttu-id="a5592-403">Uzun süre çalışan çözümleme ani bir başarısızlığını kullanıcılar için oldukça can sıkıcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="a5592-403">An abrupt failure of a long-running analysis can be quite frustrating for users.</span></span> <span data-ttu-id="a5592-404">Bu durumda, varsayılan dönüş değerleri seçilmelidir sınırlar tooavoid toodownstream işleme zarar verebilir.</span><span class="sxs-lookup"><span data-stu-id="a5592-404">tooavoid this situation, default return values must be chosen that will limit damage toodownstream processing.</span></span> <span data-ttu-id="a5592-405">Bir ileti ayrıca bir şeyler yanlış geçti üretilen tooalert kullanıcı sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="a5592-405">A message is also produced tooalert users that something has gone wrong.</span></span>

<span data-ttu-id="a5592-406">R kullanılan toodefensive programlamada değil varsa, bu kod bir bit bunaltıcı görünebilir.</span><span class="sxs-lookup"><span data-stu-id="a5592-406">If you are not used toodefensive programming in R, all this code may seem a bit overwhelming.</span></span> <span data-ttu-id="a5592-407">I hello ana adımlarda size yol gösterir:</span><span class="sxs-lookup"><span data-stu-id="a5592-407">I will walk you through hello major steps:</span></span>

1. <span data-ttu-id="a5592-408">Vektör dört iletilerinin tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="a5592-408">A vector of four messages is defined.</span></span> <span data-ttu-id="a5592-409">Bu iletiler, bazı hello olası hatalar ve bu kodu ile oluşan özel durumlar hakkında kullanılan toocommunicate bilgilerdir.</span><span class="sxs-lookup"><span data-stu-id="a5592-409">These messages are used toocommunicate information about some of hello possible errors and exceptions that can occur with this code.</span></span>
2. <span data-ttu-id="a5592-410">I BELİRTİLMEYEN değeri her bir olay döndürür.</span><span class="sxs-lookup"><span data-stu-id="a5592-410">I return a value of NA for each case.</span></span> <span data-ttu-id="a5592-411">Daha az yan etkileri olabilir diğer birçok olasılık vardır.</span><span class="sxs-lookup"><span data-stu-id="a5592-411">There are many other possibilities that might have fewer side effects.</span></span> <span data-ttu-id="a5592-412">Vektör sıfır değerini veya hello özgün giriş vektör, örneğin dönüş.</span><span class="sxs-lookup"><span data-stu-id="a5592-412">I could return a vector of zeroes, or hello original input vector, for example.</span></span>
3. <span data-ttu-id="a5592-413">Denetimleri hello bağımsız değişkenleri toohello işlevi üzerinde gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a5592-413">Checks are run on hello arguments toohello function.</span></span> <span data-ttu-id="a5592-414">Her durumda, bir hata algılandığında, varsayılan bir değer döndürülür ve bir ileti hello tarafından üretilen `warning()` işlevi.</span><span class="sxs-lookup"><span data-stu-id="a5592-414">In each case, if an error is detected, a default value is returned and a message is produced by hello `warning()` function.</span></span> <span data-ttu-id="a5592-415">Kullanıyorum `warning()` yerine `stop()` hello sonraki yürütme, tam olarak neyi çalışıyorum sonlandıracak gibi tooavoid.</span><span class="sxs-lookup"><span data-stu-id="a5592-415">I am using `warning()` rather than `stop()` as hello latter will terminate execution, exactly what I am trying tooavoid.</span></span> <span data-ttu-id="a5592-416">I bu kodu bu durumda olduğu gibi bir yordam stili karmaşık ve belirsiz seemed işlevsel bir yaklaşım yazılmış olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a5592-416">Note that I have written this code in a procedural style, as in this case a functional approach seemed complex and obscure.</span></span>
4. <span data-ttu-id="a5592-417">Merhaba günlük hesaplamalar sarılır `tryCatch()` böylece özel durumlar ani durdurmak tooprocessing neden olmaz.</span><span class="sxs-lookup"><span data-stu-id="a5592-417">hello log computations are wrapped in `tryCatch()` so that exceptions will not cause an abrupt halt tooprocessing.</span></span> <span data-ttu-id="a5592-418">Olmadan `tryCatch()` hataların çoğu bunu yapan bir durdurma sinyali R işlevleri sonucu olarak gerçekleşti.</span><span class="sxs-lookup"><span data-stu-id="a5592-418">Without `tryCatch()` most errors raised by R functions result in a stop signal, which does just that.</span></span>

<span data-ttu-id="a5592-419">Bu R kodu denemenizde yürütün ve hello göz hello içeren dosyasındaki çıktıyı yazdırılan.</span><span class="sxs-lookup"><span data-stu-id="a5592-419">Execute this R code in your experiment and have a look at hello printed output in hello output.log file.</span></span> <span data-ttu-id="a5592-420">Şekil 13'te gösterildiği gibi şimdi hello hello dört sütun oturum, dönüştürülmüş hello değerlerini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="a5592-420">You will now see hello transformed values of hello four columns in hello log, as shown in Figure 13.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="a5592-421">*Şekil 13. Merhaba özetini hello dataframe değerleri dönüştürüldüğünde.*</span><span class="sxs-lookup"><span data-stu-id="a5592-421">*Figure 13. Summary of hello transformed values in hello dataframe.*</span></span>

<span data-ttu-id="a5592-422">Merhaba değerleri dönüştürülen bakın.</span><span class="sxs-lookup"><span data-stu-id="a5592-422">We see hello values have been transformed.</span></span> <span data-ttu-id="a5592-423">Şimdi sütlü üretim büyük ölçüde şimdi günlük ölçekte arıyoruz, geri çağırma tüm diğer Süt ürün üretim aşıyor.</span><span class="sxs-lookup"><span data-stu-id="a5592-423">Milk production now greatly exceeds all other dairy product production, recalling that we are now looking at a log scale.</span></span>

<span data-ttu-id="a5592-424">Bu noktada verilerimizi temizlenir ve biz bazı modelleme için hazır olursunuz.</span><span class="sxs-lookup"><span data-stu-id="a5592-424">At this point our data is cleaned up and we are ready for some modeling.</span></span> <span data-ttu-id="a5592-425">Sonuç veri kümesini çıktı olarak hello için Özet hello görselleştirme bakarak bizim [R betiği yürütün] [ execute-r-script] modül hello 'Month' sütundur 'Categorical' 12 benzersiz değerlerle yeniden, biz istediği gibi görürsünüz .</span><span class="sxs-lookup"><span data-stu-id="a5592-425">Looking at hello visualization summary for hello Result Dataset output of our [Execute R Script][execute-r-script] module, you will see hello 'Month' column is 'Categorical' with 12 unique values, again, just as we wanted.</span></span>

## <span data-ttu-id="a5592-426"><a id="timeseries"></a>Zaman serisi nesneleri ve bağıntı çözümleme</span><span class="sxs-lookup"><span data-stu-id="a5592-426"><a id="timeseries"></a>Time series objects and correlation analysis</span></span>
<span data-ttu-id="a5592-427">Bu bölümde biz birkaç temel R zaman serisi nesneleri keşfedin ve bazı hello değişkenler arasındaki hello bağıntıları analiz edin.</span><span class="sxs-lookup"><span data-stu-id="a5592-427">In this section we will explore a few basic R time series objects and analyze hello correlations between some of hello variables.</span></span> <span data-ttu-id="a5592-428">Amacımız toooutput bir dataframe hello pairwise bağıntı bilgi içeren birkaç gecikmelere adresindeki ' dir.</span><span class="sxs-lookup"><span data-stu-id="a5592-428">Our goal is toooutput a dataframe containing hello pairwise correlation information at several lags.</span></span>

<span data-ttu-id="a5592-429">Merhaba tam R Bu bölümde daha önce indirdiğiniz hello zip dosyasında kodudur.</span><span class="sxs-lookup"><span data-stu-id="a5592-429">hello complete R code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="time-series-objects-in-r"></a><span data-ttu-id="a5592-430">R zaman serisi nesneleri</span><span class="sxs-lookup"><span data-stu-id="a5592-430">Time series objects in R</span></span>
<span data-ttu-id="a5592-431">Yukarıda belirtildiği gibi zaman serisinin zaten zamanına göre dizine veri değerleri bir dizi olduğundan.</span><span class="sxs-lookup"><span data-stu-id="a5592-431">As already mentioned, time series are a series of data values indexed by time.</span></span> <span data-ttu-id="a5592-432">R zaman serisi nesneleri kullanılan toocreate ve hello zaman dizinini yönetme.</span><span class="sxs-lookup"><span data-stu-id="a5592-432">R time series objects are used toocreate and manage hello time index.</span></span> <span data-ttu-id="a5592-433">Birkaç avantaj toousing zaman serisi nesneleri vardır.</span><span class="sxs-lookup"><span data-stu-id="a5592-433">There are several advantages toousing time series objects.</span></span> <span data-ttu-id="a5592-434">Zaman serisi nesneleri hello nesnesinde kapsüllenmiş hello zaman serisi dizini değerleri yönetme birçok ayrıntıları hello boş.</span><span class="sxs-lookup"><span data-stu-id="a5592-434">Time series objects free you from hello many details of managing hello time series index values that are encapsulated in hello object.</span></span> <span data-ttu-id="a5592-435">Ayrıca, zaman serisi nesneler yazdırma, modelleme, vb., toouse hello Çizdirmek, çoğu zaman serisi yöntemleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="a5592-435">In addition, time series objects allow you toouse hello many time series methods for plotting, printing, modeling, etc.</span></span>

<span data-ttu-id="a5592-436">Merhaba POSIXct zaman serisi sınıfı yaygın olarak kullanılır ve görece daha basittir.</span><span class="sxs-lookup"><span data-stu-id="a5592-436">hello POSIXct time series class is commonly used and is relatively simple.</span></span> <span data-ttu-id="a5592-437">Bu zaman serisi sınıf hello hello dönem, 1 Ocak 1970'ten başından süreyi ölçer.</span><span class="sxs-lookup"><span data-stu-id="a5592-437">This time series class measures time from hello start of hello epoch, January 1, 1970.</span></span> <span data-ttu-id="a5592-438">Bu örnekte POSIXct zaman serisi nesneleri kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="a5592-438">We will use POSIXct time series objects in this example.</span></span> <span data-ttu-id="a5592-439">Diğer yaygın olarak kullanılan R zaman serisi nesne sınıfları zoo ve xts, Genişletilebilir zaman serisi içerir.</span><span class="sxs-lookup"><span data-stu-id="a5592-439">Other widely used R time series object classes include zoo and xts, extensible time series.</span></span>
<!-- Additional information on R time series objects is provided in hello references in Section 5.7. [commenting because this section doesn't exist, even in hello original] -->

### <a name="time-series-object-example"></a><span data-ttu-id="a5592-440">Zaman serisi nesnesi örneği</span><span class="sxs-lookup"><span data-stu-id="a5592-440">Time series object example</span></span>
<span data-ttu-id="a5592-441">Bizim örneğimizde ile başlayalım.</span><span class="sxs-lookup"><span data-stu-id="a5592-441">Let's get started with our example.</span></span> <span data-ttu-id="a5592-442">Sürükleme ve bırakma bir **yeni** [R betiği yürütün] [ execute-r-script] denemenizi modüle.</span><span class="sxs-lookup"><span data-stu-id="a5592-442">Drag and drop a **new** [Execute R Script][execute-r-script] module into your experiment.</span></span> <span data-ttu-id="a5592-443">Merhaba varolan hello sonuç Dataset1 çıkış bağlantı noktasına bağlanmak [R betiği yürütün] [ execute-r-script] modülü toohello Dataset1 giriş hello yeni bağlantı noktası [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="a5592-443">Connect hello Result Dataset1 output port of hello existing [Execute R Script][execute-r-script] module toohello Dataset1 input port of hello new [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="a5592-444">Merhaba ilk örnekler için yaptığınız gibi biz yapacağınızı gösterir bazı noktalarda hello örnek ilerlemeyi yalnızca hello artımlı ek kod satırı bulunmaktadır R her adımında.</span><span class="sxs-lookup"><span data-stu-id="a5592-444">As I did for hello first examples, as we progress through hello example, at some points I will show only hello incremental additional lines of R code at each step.</span></span>  

#### <a name="reading-hello-dataframe"></a><span data-ttu-id="a5592-445">Merhaba dataframe okuma</span><span class="sxs-lookup"><span data-stu-id="a5592-445">Reading hello dataframe</span></span>
<span data-ttu-id="a5592-446">İlk adım olarak şimdi bir dataframe okuyun ve biz hello beklenen sonuçları elde emin olun.</span><span class="sxs-lookup"><span data-stu-id="a5592-446">As a first step, let's read in a dataframe and make sure we get hello expected results.</span></span> <span data-ttu-id="a5592-447">Merhaba aşağıdaki kodu yapmalısınız hello işi.</span><span class="sxs-lookup"><span data-stu-id="a5592-447">hello following code should do hello job.</span></span>

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check hello results

<span data-ttu-id="a5592-448">Şimdi, hello denemeyi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a5592-448">Now, run hello experiment.</span></span> <span data-ttu-id="a5592-449">Merhaba günlük hello yeni R betiği yürütün şeklin Şekil 14 gibi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="a5592-449">hello log of hello new Execute R Script shape should look like Figure 14.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...

<span data-ttu-id="a5592-450">*Şekil 14. Merhaba dataframe hello R betiği yürütün modülünde özeti.*</span><span class="sxs-lookup"><span data-stu-id="a5592-450">*Figure 14. Summary of hello dataframe in hello Execute R Script module.*</span></span>

<span data-ttu-id="a5592-451">Bu, beklenen hello türleri ve biçimde verilerdir.</span><span class="sxs-lookup"><span data-stu-id="a5592-451">This data is of hello expected types and format.</span></span> <span data-ttu-id="a5592-452">Merhaba 'Month' sütun türü faktörü olduğunu ve hello düzey sayısı beklenen sahip unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a5592-452">Note that hello 'Month' column is of type factor and has hello expected number of levels.</span></span>

#### <a name="creating-a-time-series-object"></a><span data-ttu-id="a5592-453">Zaman serisi nesnesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="a5592-453">Creating a time series object</span></span>
<span data-ttu-id="a5592-454">Bir zaman serisi nesne tooour dataframe tooadd ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="a5592-454">We need tooadd a time series object tooour dataframe.</span></span> <span data-ttu-id="a5592-455">Merhaba geçerli kod POSIXct sınıfının yeni bir sütun ekler hello şununla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a5592-455">Replace hello current code with hello following, which adds a new column of class POSIXct.</span></span>

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check hello results

<span data-ttu-id="a5592-456">Şimdi, hello günlüğünü denetleyin.</span><span class="sxs-lookup"><span data-stu-id="a5592-456">Now, check hello log.</span></span> <span data-ttu-id="a5592-457">Şekil 15 gibi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="a5592-457">It should look like Figure 15.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

<span data-ttu-id="a5592-458">*Şekil 15. Bir zaman serisi nesnesiyle hello dataframe özeti.*</span><span class="sxs-lookup"><span data-stu-id="a5592-458">*Figure 15. Summary of hello dataframe with a time series object.*</span></span>

<span data-ttu-id="a5592-459">Bu hello yeni bir sütun aslında POSIXct sınıfıdır hello Özet görebiliriz.</span><span class="sxs-lookup"><span data-stu-id="a5592-459">We can see from hello summary that hello new column is in fact of class POSIXct.</span></span>

### <a name="exploring-and-transforming-hello-data"></a><span data-ttu-id="a5592-460">Keşfetmek ve hello veri dönüştürme</span><span class="sxs-lookup"><span data-stu-id="a5592-460">Exploring and transforming hello data</span></span>
<span data-ttu-id="a5592-461">Bu veri kümesinde hello değişkenlerinin bazıları inceleyelim.</span><span class="sxs-lookup"><span data-stu-id="a5592-461">Let's explore some of hello variables in this dataset.</span></span> <span data-ttu-id="a5592-462">Scatterplot matrisini en iyi yolu tooproduce hızlı bir görünümünü verir.</span><span class="sxs-lookup"><span data-stu-id="a5592-462">A scatterplot matrix is a good way tooproduce a quick look.</span></span> <span data-ttu-id="a5592-463">Merhaba değiştirme `str()` hello önceki R kod satırı aşağıdaki hello ile işlevinde.</span><span class="sxs-lookup"><span data-stu-id="a5592-463">I am replacing hello `str()` function in hello previous R code with hello following line.</span></span>

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

<span data-ttu-id="a5592-464">Bu kodu çalıştırmak ve ne olduğunu gözleyin.</span><span class="sxs-lookup"><span data-stu-id="a5592-464">Run this code and see what happens.</span></span> <span data-ttu-id="a5592-465">R aygıtı bağlantı noktası Hello üretilen hello çizim Şekil 16 gibi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="a5592-465">hello plot produced at hello R Device port should look like Figure 16.</span></span>

![Seçili değişkenleri Scatterplot Matrisi][17]

<span data-ttu-id="a5592-467">*Şekil 16. Seçili değişkenleri Scatterplot matrisi.*</span><span class="sxs-lookup"><span data-stu-id="a5592-467">*Figure 16. Scatterplot matrix of selected variables.*</span></span>

<span data-ttu-id="a5592-468">Bu değişkenler arasında hello ilişkilerde bazı garip görünüşlü yapısı yoktur.</span><span class="sxs-lookup"><span data-stu-id="a5592-468">There is some odd-looking structure in hello relationships between these variables.</span></span> <span data-ttu-id="a5592-469">Belki de bu hello verilerindeki eğilimleri ve biz hello değişkenleri standartlaşmış değil, hello olgu ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="a5592-469">Perhaps this arises from trends in hello data and from hello fact that we have not standardized hello variables.</span></span>

### <a name="correlation-analysis"></a><span data-ttu-id="a5592-470">Bağıntı çözümleme</span><span class="sxs-lookup"><span data-stu-id="a5592-470">Correlation analysis</span></span>
<span data-ttu-id="a5592-471">tooboth ihtiyacımız tooperform bağıntı çözümleme XML'deki eğilimi ve hello değişkenleri standart hale getirme.</span><span class="sxs-lookup"><span data-stu-id="a5592-471">tooperform correlation analysis we need tooboth de-trend and standardize hello variables.</span></span> <span data-ttu-id="a5592-472">Biz yalnızca hello R kullanabilirsiniz `scale()` merkezleri hem değişkenleri ölçeklendirir işlevi.</span><span class="sxs-lookup"><span data-stu-id="a5592-472">We could simply use hello R `scale()` function, which both centers and scales variables.</span></span> <span data-ttu-id="a5592-473">Bu işlev iyi daha hızlı çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="a5592-473">This function might well run faster.</span></span> <span data-ttu-id="a5592-474">Ancak, tooshow istiyorum, r içinde savunma programing örneği</span><span class="sxs-lookup"><span data-stu-id="a5592-474">However, I want tooshow you an example of defensive programing in R.</span></span>

<span data-ttu-id="a5592-475">Merhaba `ts.detrend()` aşağıda gösterilen işlevi bu işlemlerin her ikisini de gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="a5592-475">hello `ts.detrend()` function shown below performs both of these operations.</span></span> <span data-ttu-id="a5592-476">Merhaba aşağıdaki iki satır kod hello veri XML'deki eğilimi ve hello değerleri standart hale getirme.</span><span class="sxs-lookup"><span data-stu-id="a5592-476">hello following two lines of code de-trend hello data and then standardize hello values.</span></span>

    ts.detrend <- function(ts, Time, min.length = 3){
      ## Function toode-trend and standardize a time series

      ## Define some messages if they are NULL  
      messages <- c('ERROR: ts.detrend requires arguments ts and Time toohave hello same length',
                    'ERROR: ts.detrend requires argument ts toobe of type numeric',
                    paste('WARNING: ts.detrend has encountered a time series with length less than', as.character(min.length)),
                    'ERROR: ts.detrend has encountered a Time argument not of class POSIXct',
                    'ERROR: Detrend regression has failed in ts.detrend',
                    'ERROR: Exception occurred in ts.detrend while standardizing time series in function ts.detrend'
      )
      # Create a vector of zeros tooreturn as a default in some cases
      zerovec  <- rep(length(ts), 0.0)

      # hello input arguments are not of hello same length, return ts and quit
      if(length(Time) != length(ts)) {warning(messages[1]); return(ts)}

      # If hello ts is not numeric, just return a zero vector and quit
      if(!is.numeric(ts)) {warning(messages[2]); return(zerovec)}

      # If hello ts is too short, just return it and quit
      if((ts.length <- length(ts)) < min.length) {warning(messages[3]); return(ts)}

      ## Check that hello Time variable is of class POSIXct
      if(class(cadairydata$Time)[[1]] != "POSIXct") {warning(messages[4]); return(ts)}

      ## De-trend hello time series by using a linear model
      ts.frame  <- data.frame(ts = ts, Time = Time)
      tryCatch({ts <- ts - fitted(lm(ts ~ Time, data = ts.frame))},
               error = function(e){warning(messages[5]); zerovec})

      tryCatch( {stdev <- sqrt(sum((ts - mean(ts))^2))/(ts.length - 1)
                 ts <- ts/stdev},
                error = function(e){warning(messages[6]); zerovec})

      ts
    }  
    ## Apply hello detrend.ts function toohello variables of interest
    df.detrend <- data.frame(lapply(cadairydata[, 4:7], ts.detrend, cadairydata$Time))

    ## Plot hello results toolook at hello relationships
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = df.detrend, main = "Pairwise Scatterplots of detrended standardized time series")

<span data-ttu-id="a5592-477">Merhaba içinde oldukça bit oluşmasını yoktur `ts.detrend()` işlevi.</span><span class="sxs-lookup"><span data-stu-id="a5592-477">There is quite a bit happening in hello `ts.detrend()` function.</span></span> <span data-ttu-id="a5592-478">Bu kod çoğu hello bağımsız değişkenleri ile ilgili olası sorunları denetleme veya hala hello hesaplamalar sırasında ortaya çıkabilecek özel durumlarla birlikte ele alma.</span><span class="sxs-lookup"><span data-stu-id="a5592-478">Most of this code is checking for potential problems with hello arguments or dealing with exceptions, which can still arise during hello computations.</span></span> <span data-ttu-id="a5592-479">Bu kod yalnızca birkaç satırlık gerçekte hesaplamalar hello.</span><span class="sxs-lookup"><span data-stu-id="a5592-479">Only a few lines of this code actually do hello computations.</span></span>

<span data-ttu-id="a5592-480">Biz zaten savunma programlamada örneği ele alınan [değer dönüşümler](#valuetransformations).</span><span class="sxs-lookup"><span data-stu-id="a5592-480">We have already discussed an example of defensive programming in [Value transformations](#valuetransformations).</span></span> <span data-ttu-id="a5592-481">Her iki hesaplama blokları kaydırılır `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="a5592-481">Both computation blocks are wrapped in `tryCatch()`.</span></span> <span data-ttu-id="a5592-482">İsteğe bağlı olarak bazı hatalar için anlamlı tooreturn hello özgün giriş vektör yapar ve diğer durumlarda, ı vektör sıfır değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="a5592-482">For some errors it makes sense tooreturn hello original input vector, and in other cases, I return a vector of zeros.</span></span>  

<span data-ttu-id="a5592-483">Merhaba doğrusal regresyon XML'deki eğilimleri belirlemek için kullanılan bir zaman serisi gerileme olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a5592-483">Note that hello linear regression used for de-trending is a time series regression.</span></span> <span data-ttu-id="a5592-484">Merhaba bir göstergesi olduğu değişken bir zaman serisi nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="a5592-484">hello predictor variable is a time series object.</span></span>  

<span data-ttu-id="a5592-485">Bir kez `ts.detrend()` tanımlanmış biz bizim dataframe ilgi toohello değişkenlerinin uygulayın.</span><span class="sxs-lookup"><span data-stu-id="a5592-485">Once `ts.detrend()` is defined we apply it toohello variables of interest in our dataframe.</span></span> <span data-ttu-id="a5592-486">Tarafından oluşturulan hello sonuç listesini coerce gerekir `lapply()` kullanarak toodata dataframe `as.data.frame()`.</span><span class="sxs-lookup"><span data-stu-id="a5592-486">We must coerce hello resulting list created by `lapply()` toodata dataframe by using `as.data.frame()`.</span></span> <span data-ttu-id="a5592-487">Savunma yönlerini nedeniyle `ts.detrend()`, hello değişkenlerinden biri engellemez hatası tooprocess başkalarının hello işlenmesini düzeltin.</span><span class="sxs-lookup"><span data-stu-id="a5592-487">Because of defensive aspects of `ts.detrend()`, failure tooprocess one of hello variables will not prevent correct processing of hello others.</span></span>  

<span data-ttu-id="a5592-488">kodun son satırı Hello pairwise scatterplot oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a5592-488">hello final line of code creates a pairwise scatterplot.</span></span> <span data-ttu-id="a5592-489">Merhaba R kodu çalıştırdıktan sonra hello scatterplot hello sonuçlarını şekil 17'de gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a5592-489">After running hello R code, hello results of hello scatterplot are shown in Figure 17.</span></span>

![XML'deki koleksiyonunuzdaki ve standartlaştırılmış zaman serisinin pairwise scatterplot][18]

<span data-ttu-id="a5592-491">*Şekil 17. Pairwise scatterplot XML'deki koleksiyonunuzdaki ve standartlaştırılmış zaman serisinin.*</span><span class="sxs-lookup"><span data-stu-id="a5592-491">*Figure 17. Pairwise scatterplot of de-trended and standardized time series.*</span></span>

<span data-ttu-id="a5592-492">Şekil 16'da gösterilen bu sonuçları toothose karşılaştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5592-492">You can compare these results toothose shown in Figure 16.</span></span> <span data-ttu-id="a5592-493">Merhaba eğilimi kaldırıldı ve hello değişkenleri standartlaştırılmış, biz bu değişkenleri arasındaki hello ilişkileri çok daha az yapısında bakın.</span><span class="sxs-lookup"><span data-stu-id="a5592-493">With hello trend removed and hello variables standardized, we see a lot less structure in hello relationships between these variables.</span></span>

<span data-ttu-id="a5592-494">Merhaba kod toocompute hello bağıntıları R ccf nesneler olarak aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="a5592-494">hello code toocompute hello correlations as R ccf objects is as follows.</span></span>

    ## A function toocompute pairwise correlations from a
    ## list of time series value vectors
    pair.cor <- function(pair.ind, ts.list, lag.max = 1, plot = FALSE){
      ccf(ts.list[[pair.ind[1]]], ts.list[[pair.ind[2]]], lag.max = lag.max, plot = plot)
    }

    ## A list of hello pairwise indices
    corpairs <- list(c(1,2), c(1,3), c(1,4), c(2,3), c(2,4), c(3,4))

    ## Compute hello list of ccf objects
    cadairycorrelations <- lapply(corpairs, pair.cor, df.detrend)  

    cadairycorrelations

<span data-ttu-id="a5592-495">Bu kodu çalıştırmak Şekil 18'de gösterilen hello günlük üretir.</span><span class="sxs-lookup"><span data-stu-id="a5592-495">Running this code produces hello log shown in Figure 18.</span></span>

    [ModuleOutput] Loading objects:
    [ModuleOutput]   port1
    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] [[1]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.148 0.358 0.317 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[2]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.395 -0.186 -0.238 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[3]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.059 -0.089 -0.127 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[4]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.140 0.294 0.293 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[5]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.002 -0.074 -0.124 

<span data-ttu-id="a5592-496">*Şekil 18. Ccf listesi hello pairwise bağıntı çözümlemesinden nesneleri.*</span><span class="sxs-lookup"><span data-stu-id="a5592-496">*Figure 18. List of ccf objects from hello pairwise correlation analysis.*</span></span>

<span data-ttu-id="a5592-497">Her gecikme için bir bağıntı değer yoktur.</span><span class="sxs-lookup"><span data-stu-id="a5592-497">There is a correlation value for each lag.</span></span> <span data-ttu-id="a5592-498">Bu bağıntı değerleri hiçbiri büyüklükte toobe önemli değildir.</span><span class="sxs-lookup"><span data-stu-id="a5592-498">None of these correlation values is large enough toobe significant.</span></span> <span data-ttu-id="a5592-499">Biz biz her bir değişken bağımsız olarak model oluşturabilirsiniz, bu nedenle tamamlanabilmesi.</span><span class="sxs-lookup"><span data-stu-id="a5592-499">We can therefore conclude that we can model each variable independently.</span></span>

### <a name="output-a-dataframe"></a><span data-ttu-id="a5592-500">Bir dataframe çıkış</span><span class="sxs-lookup"><span data-stu-id="a5592-500">Output a dataframe</span></span>
<span data-ttu-id="a5592-501">Biz hello pairwise bağıntıları R ccf nesneleri listesi olarak hesaplanan.</span><span class="sxs-lookup"><span data-stu-id="a5592-501">We have computed hello pairwise correlations as a list of R ccf objects.</span></span> <span data-ttu-id="a5592-502">Merhaba sonuç veri kümesinin çıkış bağlantı noktasına bir dataframe gerçekten gerektirdiğinden bu biraz bir sorunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="a5592-502">This presents a bit of a problem as hello Result Dataset output port really requires a dataframe.</span></span> <span data-ttu-id="a5592-503">Ayrıca, hello ccf nesnesi kendisini listesini ve yalnızca hello değerleri bu listenin hello bağıntıları hello adresindeki hello ilk öğesindeki çeşitli gecikmelere istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="a5592-503">Further, hello ccf object is itself a list and we want only hello values in hello first element of this list, hello correlations at hello various lags.</span></span>

<span data-ttu-id="a5592-504">kod ayıklar hello gecikme değerleri hello kendilerini listeleridir ccf nesneleri listesinden aşağıdaki hello.</span><span class="sxs-lookup"><span data-stu-id="a5592-504">hello following code extracts hello lag values from hello list of ccf objects, which are themselves lists.</span></span>

    df.correlations <- data.frame(do.call(rbind, lapply(cadairycorrelations, '[[', 1)))

    c.names <- c("correlation pair", "-1 lag", "0 lag", "+1 lag")
    r.names  <- c("Corr Cot Cheese - Ice Cream",
                  "Corr Cot Cheese - Milk Prod",
                  "Corr Cot Cheese - Fat Price",
                  "Corr Ice Cream - Mik Prod",
                  "Corr Ice Cream - Fat Price",
                  "Corr Milk Prod - Fat Price")

    ## Build a dataframe with hello row names column and the
    ## correlation data frame and assign hello column names
    outframe <- cbind(r.names, df.correlations)
    colnames(outframe) <- c.names
    outframe


    ## WARNING!
    ## hello following line works only in Azure Machine Learning
    ## When running in RStudio, this code will result in an error
    #maml.mapOutputPort('outframe')

<span data-ttu-id="a5592-505">Merhaba ilk satırının kod biraz zor olduğu ve bazı açıklama onu anlamanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="a5592-505">hello first line of code is a bit tricky, and some explanation may help you understand it.</span></span> <span data-ttu-id="a5592-506">Hello içinde dışarı çalışma biz hello aşağıdaki vardır:</span><span class="sxs-lookup"><span data-stu-id="a5592-506">Working from hello inside out we have hello following:</span></span>

1. <span data-ttu-id="a5592-507">Merhaba '**[[**'işleci' hello bağımsız değişkeniyle**1**' seçer hello hello gecikmelere hello ccf nesne listesinin hello ilk öğeden adresindeki bağıntıları vektörü.</span><span class="sxs-lookup"><span data-stu-id="a5592-507">hello '**[[**' operator with hello argument '**1**' selects hello vector of correlations at hello lags from hello first element of hello ccf object list.</span></span>
2. <span data-ttu-id="a5592-508">Merhaba `do.call()` işlevi uygular hello `rbind()` hello listesinin hello öğelerini üzerinden işlevi döndürür tarafından `lapply()`.</span><span class="sxs-lookup"><span data-stu-id="a5592-508">hello `do.call()` function applies hello `rbind()` function over hello elements of hello list returns by `lapply()`.</span></span>
3. <span data-ttu-id="a5592-509">Merhaba `data.frame()` işlevi tarafından üretilen hello sonuç olacak şekilde zorlar `do.call()` tooa dataframe.</span><span class="sxs-lookup"><span data-stu-id="a5592-509">hello `data.frame()` function coerces hello result produced by `do.call()` tooa dataframe.</span></span>

<span data-ttu-id="a5592-510">Merhaba satır adlarını hello dataframe sütununda olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a5592-510">Note that hello row names are in a column of hello dataframe.</span></span> <span data-ttu-id="a5592-511">Bunun yapılması korur hello satır adlarını hello çıktısını olduklarında [R betiği yürütün][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="a5592-511">Doing so preserves hello row names when they are output from hello [Execute R Script][execute-r-script].</span></span>

<span data-ttu-id="a5592-512">Merhaba kod çalıştırmasını çıktılar şekil 19'gösterilen hello zaman ı **Görselleştir** hello çıktıyı hello sonuç Dataset bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="a5592-512">Running hello code produces hello output shown in Figure 19 when I **Visualize** hello output at hello Result Dataset port.</span></span> <span data-ttu-id="a5592-513">Merhaba satır hello ilk sütunda, beklendiği gibi adlardır.</span><span class="sxs-lookup"><span data-stu-id="a5592-513">hello row names are in hello first column, as intended.</span></span>

![Merhaba bağıntı analiz sonuçları çıktısı][20]

<span data-ttu-id="a5592-515">*Şekil 19. Merhaba bağıntı çözümlemesinden çıktı sonuçları.*</span><span class="sxs-lookup"><span data-stu-id="a5592-515">*Figure 19. Results output from hello correlation analysis.*</span></span>

## <span data-ttu-id="a5592-516"><a id="seasonalforecasting"></a>Zaman serisi örnek: Mevsimlik tahmin</span><span class="sxs-lookup"><span data-stu-id="a5592-516"><a id="seasonalforecasting"></a>Time series example: seasonal forecasting</span></span>
<span data-ttu-id="a5592-517">Bizim veri analizi için uygun bir biçimde sunulmuştur ve hello değişkenleri arasındaki önemli hiçbir bağıntıları vardır belirledik.</span><span class="sxs-lookup"><span data-stu-id="a5592-517">Our data is now in a form suitable for analysis, and we have determined there are no significant correlations between hello variables.</span></span> <span data-ttu-id="a5592-518">Şimdi geçmek ve bir zaman serisi modeli tahmin oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a5592-518">Let's move on and create a time series forecasting model.</span></span> <span data-ttu-id="a5592-519">Bu modeli kullanarak biz California sütlü üretim hello için 2013 12 ay tahmin.</span><span class="sxs-lookup"><span data-stu-id="a5592-519">Using this model we will forecast California milk production for hello 12 months of 2013.</span></span>

<span data-ttu-id="a5592-520">Tahmin modelimizi eğilim bileşeni ve Mevsimlik bileşeni olmak üzere iki bileşenden sahip olur.</span><span class="sxs-lookup"><span data-stu-id="a5592-520">Our forecasting model will have two components, a trend component and a seasonal component.</span></span> <span data-ttu-id="a5592-521">Merhaba tam tahmin, bu iki bileşenden hello üründür.</span><span class="sxs-lookup"><span data-stu-id="a5592-521">hello complete forecast is hello product of these two components.</span></span> <span data-ttu-id="a5592-522">Bu model türüne çarpma model olarak bilinir.</span><span class="sxs-lookup"><span data-stu-id="a5592-522">This type of model is known as a multiplicative model.</span></span> <span data-ttu-id="a5592-523">Merhaba, ek bir model alternatiftir.</span><span class="sxs-lookup"><span data-stu-id="a5592-523">hello alternative is an additive model.</span></span> <span data-ttu-id="a5592-524">Biz bu çözümleme tractable yapar ilgi günlük dönüştürme toohello değişkenlerinin zaten uyguladınız.</span><span class="sxs-lookup"><span data-stu-id="a5592-524">We have already applied a log transformation toohello variables of interest, which makes this analysis tractable.</span></span>

<span data-ttu-id="a5592-525">Merhaba tam R Bu bölümde daha önce indirdiğiniz hello zip dosyasında kodudur.</span><span class="sxs-lookup"><span data-stu-id="a5592-525">hello complete R code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="creating-hello-dataframe-for-analysis"></a><span data-ttu-id="a5592-526">Merhaba dataframe çözümleme için oluşturma</span><span class="sxs-lookup"><span data-stu-id="a5592-526">Creating hello dataframe for analysis</span></span>
<span data-ttu-id="a5592-527">Başlangıç ekleyerek bir **yeni** [R betiği yürütün] [ execute-r-script] modülü tooyour deneme.</span><span class="sxs-lookup"><span data-stu-id="a5592-527">Start by adding a **new** [Execute R Script][execute-r-script] module tooyour experiment.</span></span> <span data-ttu-id="a5592-528">Merhaba bağlanmak **sonuç Dataset** hello varolan çıktı [R betiği yürütün] [ execute-r-script] modülü toohello **Dataset1** hello yeni modülünün giriş.</span><span class="sxs-lookup"><span data-stu-id="a5592-528">Connect hello **Result Dataset** output of hello existing [Execute R Script][execute-r-script] module toohello **Dataset1** input of hello new module.</span></span> <span data-ttu-id="a5592-529">Merhaba sonuç Şekil 20 gibi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="a5592-529">hello result should look something like Figure 20.</span></span>

![Merhaba eklenen hello yeni R betiği yürütün modülüyle denemeler][21]

<span data-ttu-id="a5592-531">*Şekil 20. Merhaba eklenen hello yeni R betiği yürütün modülüyle deneyin.*</span><span class="sxs-lookup"><span data-stu-id="a5592-531">*Figure 20. hello experiment with hello new Execute R Script module added.*</span></span>

<span data-ttu-id="a5592-532">Gibi hello bağıntı çözümlemesi biz yalnızca tamamlandı, biz tooadd POSIXct zaman serisi nesne içeren bir sütun gerekir.</span><span class="sxs-lookup"><span data-stu-id="a5592-532">As with hello correlation analysis we just completed, we need tooadd a column with a POSIXct time series object.</span></span> <span data-ttu-id="a5592-533">koddan hello yalnızca bunu yapın.</span><span class="sxs-lookup"><span data-stu-id="a5592-533">hello following code will do just this.</span></span>

    # If running in Machine Learning Studio, uncomment hello first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

<span data-ttu-id="a5592-534">Bu kodu çalıştırmak ve hello günlüğüne bakın.</span><span class="sxs-lookup"><span data-stu-id="a5592-534">Run this code and look at hello log.</span></span> <span data-ttu-id="a5592-535">Merhaba sonuç şekil 21 gibi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="a5592-535">hello result should look like Figure 21.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

<span data-ttu-id="a5592-536">*Şekil 21. Merhaba dataframe özeti.*</span><span class="sxs-lookup"><span data-stu-id="a5592-536">*Figure 21. A summary of hello dataframe.*</span></span>

<span data-ttu-id="a5592-537">Bu sonuçla duyuyoruz hazır toostart bizim çözümleme.</span><span class="sxs-lookup"><span data-stu-id="a5592-537">With this result, we are ready toostart our analysis.</span></span>

### <a name="create-a-training-dataset"></a><span data-ttu-id="a5592-538">Bir eğitim veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="a5592-538">Create a training dataset</span></span>
<span data-ttu-id="a5592-539">Oluşturulan hello dataframe ile toocreate bir eğitim veri kümesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a5592-539">With hello dataframe constructed we need toocreate a training dataset.</span></span> <span data-ttu-id="a5592-540">Bu verileri tüm 2013 hello yılın son 12 hello dışında hello gözlemleri test kümemize olduğu içerir.</span><span class="sxs-lookup"><span data-stu-id="a5592-540">This data will include all of hello observations except hello last 12, of hello year 2013, which is our test dataset.</span></span> <span data-ttu-id="a5592-541">Merhaba aşağıdaki alt kümelerini hello dataframe kod ve çizimler hello Süt üretim ve değişkenlerin fiyat oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a5592-541">hello following code subsets hello dataframe and creates plots of hello dairy production and price variables.</span></span> <span data-ttu-id="a5592-542">I, ardından hello çizimleri dört üretim ve fiyat değişkenleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a5592-542">I then create plots of hello four production and price variables.</span></span> <span data-ttu-id="a5592-543">Adsız bir işlev bazı güçlendirir çizim için kullanılan toodefine olan ve hello hello listesi yineleme diğer iki bağımsız değişkenlerle `Map()`.</span><span class="sxs-lookup"><span data-stu-id="a5592-543">An anonymous function is used toodefine some augments for plot, and then iterate over hello list of hello other two arguments with `Map()`.</span></span> <span data-ttu-id="a5592-544">Size, düşünüyor varsa bir döngü ince burada çalışılan için doğru.</span><span class="sxs-lookup"><span data-stu-id="a5592-544">If you are thinking that a for loop would have worked fine here, you are correct.</span></span> <span data-ttu-id="a5592-545">Ancak, R ı işlevsel bir yaklaşım gösteren işlevsel bir dili olduğundan.</span><span class="sxs-lookup"><span data-stu-id="a5592-545">But, since R is a functional language I am showing you a functional approach.</span></span>

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

<span data-ttu-id="a5592-546">Hello kodu çalıştırmak hello R aygıt çıktısından Şekil 22'de gösterilen zaman serisi serisi çizer hello üretir.</span><span class="sxs-lookup"><span data-stu-id="a5592-546">Running hello code produces hello series of time series plots from hello R Device output shown in Figure 22.</span></span> <span data-ttu-id="a5592-547">Bu hello zaman ekseni tarihleri, yöntemi seriyi çizmek hello zaman iyi bir yararı birimlerinde olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a5592-547">Note that hello time axis is in units of dates, a nice benefit of hello time series plot method.</span></span>

![Zaman serisi çizimleri California Süt üretim ve fiyat verilerinin ilk](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![Zaman serisi çizimleri California Süt üretim ve fiyat veri saniyesi](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![Zaman serisi çizimleri California Süt üretim ve fiyat veri üçüncü](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![Zaman serisi çizimleri California Süt üretim ve fiyat veri dördüncü](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

<span data-ttu-id="a5592-552">*Şekil 22. Zaman serisi çizimleri California Süt üretim ve fiyat verileri.*</span><span class="sxs-lookup"><span data-stu-id="a5592-552">*Figure 22. Time series plots of California dairy production and price data.*</span></span>

### <a name="a-trend-model"></a><span data-ttu-id="a5592-553">Eğilim modeli</span><span class="sxs-lookup"><span data-stu-id="a5592-553">A trend model</span></span>
<span data-ttu-id="a5592-554">Bir zaman serisi nesnesi ve hello veri gördüğünüze oluşturulduktan sonra tooconstruct hello California sütlü üretim verileri için bir eğilim modeli başlayalım.</span><span class="sxs-lookup"><span data-stu-id="a5592-554">Having created a time series object and having had a look at hello data, let's start tooconstruct a trend model for hello California milk production data.</span></span> <span data-ttu-id="a5592-555">Zaman serisi regresyon ile biz bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5592-555">We can do this with a time series regression.</span></span> <span data-ttu-id="a5592-556">Ancak biz eğimi ve ıntercept tooaccurately birden fazla hello eğitim verilerini eğilimi gözlenen hello model olduğunu temizleyin hello çizim olur.</span><span class="sxs-lookup"><span data-stu-id="a5592-556">However, it is clear from hello plot that we will need more than a slope and intercept tooaccurately model hello observed trend in hello training data.</span></span>

<span data-ttu-id="a5592-557">Hello küçük ölçekli hello veri verildiğinde, t Rstudio'dan eğilimi hello model oluşturmak ve ardından kesip hello sonuç olarak oluşan model Azure Machine Learning yapıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5592-557">Given hello small scale of hello data, I will build hello model for trend in RStudio and then cut and paste hello resulting model into Azure Machine Learning.</span></span> <span data-ttu-id="a5592-558">Rstudio'dan etkileşimli analiz bu tür için etkileşimli bir ortam sağlar.</span><span class="sxs-lookup"><span data-stu-id="a5592-558">RStudio provides an interactive environment for this type of interactive analysis.</span></span>

<span data-ttu-id="a5592-559">Bir ilk girişimi ı polinom regresyon too3 yukarı powers ile çalışacaktır.</span><span class="sxs-lookup"><span data-stu-id="a5592-559">As a first attempt, I will try a polynomial regression with powers up too3.</span></span> <span data-ttu-id="a5592-560">Bu tür modelleri aşırı sığdırma, gerçek bir tehlike yoktur.</span><span class="sxs-lookup"><span data-stu-id="a5592-560">There is a real danger of over-fitting these kinds of models.</span></span> <span data-ttu-id="a5592-561">Bu nedenle en iyi tooavoid yüksek sipariş terimler olur.</span><span class="sxs-lookup"><span data-stu-id="a5592-561">Therefore, it is best tooavoid high order terms.</span></span> <span data-ttu-id="a5592-562">Merhaba `I()` işlevi engeller hello içeriği yorumu ('olduğundan' hello içeriği yorumlar) ve bir regresyon denklemi toowrite tam anlamıyla yorumlanan işlevi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a5592-562">hello `I()` function inhibits interpretation of hello contents (interprets hello contents 'as is') and allows you toowrite a literally interpreted function in a regression equation.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

<span data-ttu-id="a5592-563">Merhaba aşağıdaki oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a5592-563">This generates hello following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3),
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12667 -0.02730  0.00236  0.02943  0.10586
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.33e+00   1.45e-01   43.60   <2e-16 ***
    ## Time              1.63e-09   1.72e-10    9.47   <2e-16 ***
    ## I(Month.Count^2) -1.71e-06   4.89e-06   -0.35    0.726
    ## I(Month.Count^3) -3.24e-08   1.49e-08   -2.17    0.031 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0418 on 212 degrees of freedom
    ## Multiple R-squared:  0.941,    Adjusted R-squared:  0.94
    ## F-statistic: 1.12e+03 on 3 and 212 DF,  p-value: <2e-16

<span data-ttu-id="a5592-564">P değerlerinden (Pr (> | t |)) bu çıktısında bu hello görebiliriz squared terim belirgin olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="a5592-564">From P values (Pr(>|t|)) in this output, we can see that hello squared term may not be significant.</span></span> <span data-ttu-id="a5592-565">Merhaba kullanacağım `update()` bu modeli bırakma hello tarafından kare terimi toomodify işlev.</span><span class="sxs-lookup"><span data-stu-id="a5592-565">I will use hello `update()` function toomodify this model by dropping hello squared term.</span></span>

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

<span data-ttu-id="a5592-566">Merhaba aşağıdaki oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a5592-566">This generates hello following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12597 -0.02659  0.00185  0.02963  0.10696
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.38e+00   4.07e-02   156.6   <2e-16 ***
    ## Time              1.57e-09   4.32e-11    36.3   <2e-16 ***
    ## I(Month.Count^3) -3.76e-08   2.50e-09   -15.1   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0417 on 213 degrees of freedom
    ## Multiple R-squared:  0.941,  Adjusted R-squared:  0.94
    ## F-statistic: 1.69e+03 on 2 and 213 DF,  p-value: <2e-16

<span data-ttu-id="a5592-567">Bu, daha iyi görünür.</span><span class="sxs-lookup"><span data-stu-id="a5592-567">This looks better.</span></span> <span data-ttu-id="a5592-568">Merhaba koşullarının tamamını önemlidir.</span><span class="sxs-lookup"><span data-stu-id="a5592-568">All of hello terms are significant.</span></span> <span data-ttu-id="a5592-569">Ancak, hello 2e-16 değeri varsayılan değerdir ve çok ciddi alınmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="a5592-569">However, hello 2e-16 value is a default value, and should not be taken too seriously.</span></span>  

<span data-ttu-id="a5592-570">Sağlamlık test olarak bir zaman serisi çizim hello California Süt üretim verileri, gösterilen hello eğilimi eğri olalım.</span><span class="sxs-lookup"><span data-stu-id="a5592-570">As a sanity test, let's make a time series plot of hello California dairy production data with hello trend curve shown.</span></span> <span data-ttu-id="a5592-571">Hello Azure Machine Learning kodda aşağıdaki hello eklemiş olduğunuz [R betiği yürütün] [ execute-r-script] modeli (değil Rstudio'dan) toocreate hello modeli ve bir çizim yapın.</span><span class="sxs-lookup"><span data-stu-id="a5592-571">I have added hello following code in hello Azure Machine Learning [Execute R Script][execute-r-script] model (not RStudio) toocreate hello model and make a plot.</span></span> <span data-ttu-id="a5592-572">Merhaba sonuç şekil 23'te gösterilir.</span><span class="sxs-lookup"><span data-stu-id="a5592-572">hello result is shown in Figure 23.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![California sütlü üretim verileri ile gösterilen eğilimi modeli](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

<span data-ttu-id="a5592-574">*Şekil 23. California sütlü üretim verileriyle gösterilen eğilimi modeli.*</span><span class="sxs-lookup"><span data-stu-id="a5592-574">*Figure 23. California milk production data with trend model shown.*</span></span>

<span data-ttu-id="a5592-575">Merhaba eğilimi modeli hello veri oldukça iyi uygun gibi görünüyor.</span><span class="sxs-lookup"><span data-stu-id="a5592-575">It looks like hello trend model fits hello data fairly well.</span></span> <span data-ttu-id="a5592-576">Ayrıca, değil gözükmüyor atlayarak sığdırma toobe kanıtı gibi hello modeli eğrisindeki tek wiggles.</span><span class="sxs-lookup"><span data-stu-id="a5592-576">Further, there does not seem toobe evidence of over-fitting, such as odd wiggles in hello model curve.</span></span>  

### <a name="seasonal-model"></a><span data-ttu-id="a5592-577">Mevsimlik modeli</span><span class="sxs-lookup"><span data-stu-id="a5592-577">Seasonal model</span></span>
<span data-ttu-id="a5592-578">Bir eğilim modelinde el ile toopush gereken ve hello Mevsimlik efektleri içerir.</span><span class="sxs-lookup"><span data-stu-id="a5592-578">With a trend model in hand, we need toopush on and include hello seasonal effects.</span></span> <span data-ttu-id="a5592-579">Merhaba Doğrusal model toocapture hello ay ay etkisi kukla bir değişkende olarak hello yılın hello ayı kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="a5592-579">We will use hello month of hello year as a dummy variable in hello linear model toocapture hello month-by-month effect.</span></span> <span data-ttu-id="a5592-580">Bir modele faktörü değişkenleri aldığımızda, hello ıntercept'in değil hesaplanan gerekir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a5592-580">Note that when you introduce factor variables into a model, hello intercept must not be computed.</span></span> <span data-ttu-id="a5592-581">Bunu yapmazsanız, hello formülü aşırı belirtilen ise ve R bırakacaktır hello birini Etkenler istenen ancak hello ıntercept terim tutun.</span><span class="sxs-lookup"><span data-stu-id="a5592-581">If you do not do this, hello formula is over-specified and R will drop one of hello desired factors but keep hello intercept term.</span></span>

<span data-ttu-id="a5592-582">Biz tatmin edici eğilimi modeline sahip olduğundan biz hello kullanabilir `update()` işlevi tooadd hello yeni koşulları toohello varolan modeli.</span><span class="sxs-lookup"><span data-stu-id="a5592-582">Since we have a satisfactory trend model we can use hello `update()` function tooadd hello new terms toohello existing model.</span></span> <span data-ttu-id="a5592-583">Merhaba -1 hello güncelleştirme formülünde hello ıntercept terim bırakır.</span><span class="sxs-lookup"><span data-stu-id="a5592-583">hello -1 in hello update formula drops hello intercept term.</span></span> <span data-ttu-id="a5592-584">İçinde Rstudio'dan hello şu anda devam:</span><span class="sxs-lookup"><span data-stu-id="a5592-584">Continuing in RStudio for hello moment:</span></span>

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

<span data-ttu-id="a5592-585">Merhaba aşağıdaki oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a5592-585">This generates hello following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3) + Month - 1,
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.06879 -0.01693  0.00346  0.01543  0.08726
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## Time              1.57e-09   2.72e-11    57.7   <2e-16 ***
    ## I(Month.Count^3) -3.74e-08   1.57e-09   -23.8   <2e-16 ***
    ## MonthApr          6.40e+00   2.63e-02   243.3   <2e-16 ***
    ## MonthAug          6.38e+00   2.63e-02   242.2   <2e-16 ***
    ## MonthDec          6.38e+00   2.64e-02   241.9   <2e-16 ***
    ## MonthFeb          6.31e+00   2.63e-02   240.1   <2e-16 ***
    ## MonthJan          6.39e+00   2.63e-02   243.1   <2e-16 ***
    ## MonthJul          6.39e+00   2.63e-02   242.6   <2e-16 ***
    ## MonthJun          6.38e+00   2.63e-02   242.4   <2e-16 ***
    ## MonthMar          6.42e+00   2.63e-02   244.2   <2e-16 ***
    ## MonthMay          6.43e+00   2.63e-02   244.3   <2e-16 ***
    ## MonthNov          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## MonthOct          6.37e+00   2.63e-02   241.8   <2e-16 ***
    ## MonthSep          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0263 on 202 degrees of freedom
    ## Multiple R-squared:     1,    Adjusted R-squared:     1
    ## F-statistic: 1.42e+06 on 14 and 202 DF,  p-value: <2e-16

<span data-ttu-id="a5592-586">Biz bu hello modeli artık bir kesme noktası terim ve 12 önemli ay Etkenler sahip bakın.</span><span class="sxs-lookup"><span data-stu-id="a5592-586">We see that hello model no longer has an intercept term and has 12 significant month factors.</span></span> <span data-ttu-id="a5592-587">Bu tam biz istedik olduğundan toosee.</span><span class="sxs-lookup"><span data-stu-id="a5592-587">This is exactly what we wanted toosee.</span></span>

<span data-ttu-id="a5592-588">Merhaba California Süt üretim verileri toosee hello Mevsimlik modeli ne kadar iyi çalıştığı, başka bir zaman serisi çizim olalım.</span><span class="sxs-lookup"><span data-stu-id="a5592-588">Let's make another time series plot of hello California dairy production data toosee how well hello seasonal model is working.</span></span> <span data-ttu-id="a5592-589">Hello Azure Machine Learning kodda aşağıdaki hello eklemiş olduğunuz [R betiği yürütün] [ execute-r-script] toocreate hello modeli ve bir çizim yapın.</span><span class="sxs-lookup"><span data-stu-id="a5592-589">I have added hello following code in hello Azure Machine Learning [Execute R Script][execute-r-script] toocreate hello model and make a plot.</span></span>

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

<span data-ttu-id="a5592-590">Azure Machine Learning ile bu kodu çalıştırmak hello çizim şekil 24'te gösterilen üretir.</span><span class="sxs-lookup"><span data-stu-id="a5592-590">Running this code in Azure Machine Learning produces hello plot shown in Figure 24.</span></span>

![California sütlü üretim Mevsimlik efektler dahil modeli](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

<span data-ttu-id="a5592-592">*Şekil 24. California sütlü üretim Mevsimlik efektler dahil modeli.*</span><span class="sxs-lookup"><span data-stu-id="a5592-592">*Figure 24. California milk production with model including seasonal effects.*</span></span>

<span data-ttu-id="a5592-593">Merhaba şekil 24'te gösterilen uygun toohello yerine encouraging verilerdir.</span><span class="sxs-lookup"><span data-stu-id="a5592-593">hello fit toohello data shown in Figure 24 is rather encouraging.</span></span> <span data-ttu-id="a5592-594">Merhaba eğilim ve hello Mevsimlik etkili (aylık değişim) makul arayın.</span><span class="sxs-lookup"><span data-stu-id="a5592-594">Both hello trend and hello seasonal effect (monthly variation) look reasonable.</span></span>

<span data-ttu-id="a5592-595">Bizim model üzerinde başka bir onay, şirketinizdeki hello Kalanlar göz vardır.</span><span class="sxs-lookup"><span data-stu-id="a5592-595">As another check on our model, let's have a look at hello residuals.</span></span> <span data-ttu-id="a5592-596">Merhaba aşağıdaki kodu hesaplar bizim iki modeli tahmin edilen değerler hello hello Kalanlar hello Mevsimlik modeli için hesaplar ve bu Kalanlar hello eğitim verileri için çizer.</span><span class="sxs-lookup"><span data-stu-id="a5592-596">hello following code computes hello predicted values from our two models, computes hello residuals for hello seasonal model, and then plots these residuals for hello training data.</span></span>

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot hello residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

<span data-ttu-id="a5592-597">Merhaba fazlalık çizim şekil 25 gösterilir.</span><span class="sxs-lookup"><span data-stu-id="a5592-597">hello residual plot is shown in Figure 25.</span></span>

![Kalanlar hello Mevsimlik modelinin hello eğitim verileri](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

<span data-ttu-id="a5592-599">*Şekil 25. Kalanlar hello Mevsimlik modelinin hello eğitim verileri.*</span><span class="sxs-lookup"><span data-stu-id="a5592-599">*Figure 25. Residuals of hello seasonal model for hello training data.*</span></span>

<span data-ttu-id="a5592-600">Bu Kalanlar makul arayın.</span><span class="sxs-lookup"><span data-stu-id="a5592-600">These residuals look reasonable.</span></span> <span data-ttu-id="a5592-601">Bizim modeli için hesaplamaz hello 2008-2009 recession hello etkisini dışında hiçbir belirli yapısı yoktur özellikle iyi.</span><span class="sxs-lookup"><span data-stu-id="a5592-601">There is no particular structure, except hello effect of hello 2008-2009 recession, which our model does not account for particularly well.</span></span>

<span data-ttu-id="a5592-602">Merhaba çizim şekil 25 gösterilen herhangi zamana bağımlı desenleri hello Kalanlar algılamak için yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="a5592-602">hello plot shown in Figure 25 is useful for detecting any time-dependent patterns in hello residuals.</span></span> <span data-ttu-id="a5592-603">hello açık yaklaşım, hesaplama ve kullandım hello çizme hello çizim zaman siparişte hello Kalanlar yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="a5592-603">hello explicit approach of computing and plotting hello residuals I used places hello residuals in time order on hello plot.</span></span> <span data-ttu-id="a5592-604">Merhaba diğer yandan, ı çizilen, `milk.lm$residuals`, hello çizim süre sırada değil olabilirdi.</span><span class="sxs-lookup"><span data-stu-id="a5592-604">If, on hello other hand, I had plotted `milk.lm$residuals`, hello plot would not have been in time order.</span></span>

<span data-ttu-id="a5592-605">Aynı zamanda `plot.lm()` tooproduce tanılama çizimler bir dizi.</span><span class="sxs-lookup"><span data-stu-id="a5592-605">You can also use `plot.lm()` tooproduce a series of diagnostic plots.</span></span>

    ## Show hello diagnostic plots for hello model
    plot(milk.lm2, ask = FALSE)

<span data-ttu-id="a5592-606">Bu kod, bir dizi şekil 26'da gösterilen tanılama çizimleri üretir.</span><span class="sxs-lookup"><span data-stu-id="a5592-606">This code produces a series of diagnostic plots shown in Figure 26.</span></span>

![Merhaba Mevsimlik modeli için tanılama çizimleri ilk](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![Tanılama çizimleri ikinci hello Mevsimlik modeli için](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![Merhaba Mevsimlik modeli için tanılama çizimleri üçüncü](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![Merhaba Mevsimlik modeli için tanılama çizimleri dördüncü](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

<span data-ttu-id="a5592-611">*Şekil 26. Tanılama hello Mevsimlik model için çizer.*</span><span class="sxs-lookup"><span data-stu-id="a5592-611">*Figure 26. Diagnostic plots for hello seasonal model.*</span></span>

<span data-ttu-id="a5592-612">Bu çizimler, ancak hiçbir şey tanımlanan birkaç yüksek etkili noktası toocause harika sorun.</span><span class="sxs-lookup"><span data-stu-id="a5592-612">There are a few highly influential points identified in these plots, but nothing toocause great concern.</span></span> <span data-ttu-id="a5592-613">Ayrıca, biz hello Normal Q-Q çizim hello Kalanlar dağıtılmış, Kapat toonormally doğrusal modeller için önemli varsayılır olduğunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5592-613">Further, we can see from hello Normal Q-Q plot that hello residuals are close toonormally distributed, an important assumption for linear models.</span></span>

### <a name="forecasting-and-model-evaluation"></a><span data-ttu-id="a5592-614">Tahmin ve model değerlendirme</span><span class="sxs-lookup"><span data-stu-id="a5592-614">Forecasting and model evaluation</span></span>
<span data-ttu-id="a5592-615">Bizim örneğimizde tek daha fazla şey toodo toocomplete yoktur.</span><span class="sxs-lookup"><span data-stu-id="a5592-615">There is just one more thing toodo toocomplete our example.</span></span> <span data-ttu-id="a5592-616">Biz toocompute tahminleri gerekir ve hello hata hello gerçek veri karşı ölçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5592-616">We need toocompute forecasts and measure hello error against hello actual data.</span></span> <span data-ttu-id="a5592-617">Bizim tahmin Merhaba 2013 12 ay olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a5592-617">Our forecast will be for hello 12 months of 2013.</span></span> <span data-ttu-id="a5592-618">Biz eğitim kümemize parçası olmayan bu tahmin toohello gerçek veri için bir hata ölçü hesaplayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5592-618">We can compute an error measure for this forecast toohello actual data that is not part of our training dataset.</span></span> <span data-ttu-id="a5592-619">Ayrıca, biz hello performansı test verilerinin 12 ay eğitim veri toohello 18 yıllık karşılaştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5592-619">Additionally, we can compare performance on hello 18 years of training data toohello 12 months of test data.</span></span>  

<span data-ttu-id="a5592-620">Ölçümleri sayısı kullanılan toomeasure hello zaman serisi modelleri performansını.</span><span class="sxs-lookup"><span data-stu-id="a5592-620">A number of metrics are used toomeasure hello performance of time series models.</span></span> <span data-ttu-id="a5592-621">Örneğimizde hello kök Ortalama kare (RMS) hata kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="a5592-621">In our case we will use hello root mean square (RMS) error.</span></span> <span data-ttu-id="a5592-622">Merhaba aşağıdaki işlevi iki serinin arasındaki hello RMS hatası hesaplar.</span><span class="sxs-lookup"><span data-stu-id="a5592-622">hello following function computes hello RMS error between two series.</span></span>  

    RMS.error <- function(series1, series2, is.log = TRUE, min.length = 2){
      ## Function toocompute hello RMS error or difference between two
      ## series or vectors

      messages <- c("ERROR: Input arguments toofunction RMS.error of wrong type encountered",
                    "ERROR: Input vector toofunction RMS.error is too short",
                    "ERROR: Input vectors toofunction RMS.error must be of same length",
                    "WARNING: Funtion rms.error has received invald input time series.")

      ## Check hello arguments
      if(!is.numeric(series1) | !is.numeric(series2) | !is.logical(is.log) | !is.numeric(min.length)) {
        warning(messages[1])
        return(NA)}

      if(length(series1) < min.length) {
        warning(messages[2])
        return(NA)}

      if((length(series1) != length(series2))) {
           warning(messages[3])
        return(NA)}

      ## If is.log is TRUE exponentiate hello values, else just copy
      if(is.log) {
        tryCatch( {
          temp1 <- exp(series1)
          temp2 <- exp(series2) },
          error = function(e){warning(messages[4]); NA}
        )
      } else {
        temp1 <- series1
        temp2 <- series2
      }

     ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute hello RMS error in a dataframe
      tryCatch( {
        sqrt(sum((temp1 - temp2)^2) / length(temp1))},
        error = function(e){warning(messages[4]); NA})
    }

<span data-ttu-id="a5592-623">Merhaba olduğu gibi `log.transform()` biz ele alınmıştır işlevi Merhaba "dönüşümleri değer" bölümü, oldukça çok sayıda hata denetimi ve özel durum kurtarma kodu Bu işlevde yoktur.</span><span class="sxs-lookup"><span data-stu-id="a5592-623">As with hello `log.transform()` function we discussed in hello "Value transformations" section, there is quite a lot of error checking and exception recovery code in this function.</span></span> <span data-ttu-id="a5592-624">işe hello ilkeleri olan hello aynı.</span><span class="sxs-lookup"><span data-stu-id="a5592-624">hello principles employed are hello same.</span></span> <span data-ttu-id="a5592-625">Merhaba iş sarmalanmış iki yerde yapılır `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="a5592-625">hello work is done in two places wrapped in `tryCatch()`.</span></span> <span data-ttu-id="a5592-626">İlk olarak, biz hello değerleri hello günlükleriyle çalışma olduğundan hello zaman serisi exponentiated, ' dir.</span><span class="sxs-lookup"><span data-stu-id="a5592-626">First, hello time series are exponentiated, since we have been working with hello logs of hello values.</span></span> <span data-ttu-id="a5592-627">İkinci olarak, hello gerçek RMS hatası hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="a5592-627">Second, hello actual RMS error is computed.</span></span>  

<span data-ttu-id="a5592-628">Bir işlev toomeasure hello RMS hatası ile donatılmış, şimdi oluşturun ve hello RMS hata içeren bir dataframe çıktı.</span><span class="sxs-lookup"><span data-stu-id="a5592-628">Equipped with a function toomeasure hello RMS error, let's build and output a dataframe containing hello RMS errors.</span></span> <span data-ttu-id="a5592-629">Merhaba eğilimi model tek başına koşulları ve hello tam Mevsimlik Etkenler modeliyle dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="a5592-629">We will include terms for hello trend model alone and hello complete model with seasonal factors.</span></span> <span data-ttu-id="a5592-630">Merhaba aşağıdaki kodu iş biz oluşturulan hello iki doğrusal modellerin kullanarak hello.</span><span class="sxs-lookup"><span data-stu-id="a5592-630">hello following code does hello job by using hello two linear models we have constructed.</span></span>

    ## Compute hello RMS error in a dataframe
    ## Include hello row names in hello first column so they will
    ## appear in hello output of hello Execute R Script
    RMS.df  <-  data.frame(
    rowNames = c("Trend Model", "Seasonal Model"),
      Traing = c(
      RMS.error(predict1[1:216], cadairydata$Milk.Prod[1:216]),
      RMS.error(predict2[1:216], cadairydata$Milk.Prod[1:216])),
      Forecast = c(
        RMS.error(predict1[217:228], cadairydata$Milk.Prod[217:228]),
        RMS.error(predict2[217:228], cadairydata$Milk.Prod[217:228]))
    )
    RMS.df

    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('RMS.df')

<span data-ttu-id="a5592-631">Bu kodu çalıştırmak sonuç veri kümesinin çıkış bağlantı noktasına hello şekil 27'de gösterilen hello çıkışı üretir.</span><span class="sxs-lookup"><span data-stu-id="a5592-631">Running this code produces hello output shown in Figure 27 at hello Result Dataset output port.</span></span>

![Merhaba modelleri için RMS hataları karşılaştırması][26]

<span data-ttu-id="a5592-633">*Şekil 27. Karşılaştırma hello modelleri için RMS hata sayısı.*</span><span class="sxs-lookup"><span data-stu-id="a5592-633">*Figure 27. Comparison of RMS errors for hello models.*</span></span>

<span data-ttu-id="a5592-634">Bu sonuçlarından hello Mevsimlik Etkenler toohello ekleme modeli hello RMS hatası önemli ölçüde azaltır, bkz.</span><span class="sxs-lookup"><span data-stu-id="a5592-634">From these results, we see that adding hello seasonal factors toohello model reduces hello RMS error significantly.</span></span> <span data-ttu-id="a5592-635">Çok edilebileceği hello RMS hata verileri eğitim hello için biraz küçük Merhaba tahmin.</span><span class="sxs-lookup"><span data-stu-id="a5592-635">Not too surprisingly, hello RMS error for hello training data is a bit less than for hello forecast.</span></span>

## <span data-ttu-id="a5592-636"><a id="appendixa"></a>Ek A: Kılavuzu tooRStudio</span><span class="sxs-lookup"><span data-stu-id="a5592-636"><a id="appendixa"></a>APPENDIX A: Guide tooRStudio</span></span>
<span data-ttu-id="a5592-637">Bu ekte ı bazı bağlantılar toohello başlattığınız hello Rstudio'dan belgelerine tooget anahtar bölümlerini sağlayacak şekilde Rstudio'dan oldukça iyi belgelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="a5592-637">RStudio is quite well documented, so in this appendix I will provide some links toohello key sections of hello RStudio documentation tooget you started.</span></span>

1. <span data-ttu-id="a5592-638">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="a5592-638">Creating projects</span></span>
   
   <span data-ttu-id="a5592-639">Düzenleyebilir ve Rstudio'dan kullanarak R kodunuzu projelere yönetin.</span><span class="sxs-lookup"><span data-stu-id="a5592-639">You can organize and manage your R code into projects by using RStudio.</span></span> <span data-ttu-id="a5592-640">projeleri kullanan hello belgelerine https://support.rstudio.com/hc/articles/200526207-Using-Projects bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="a5592-640">hello documentation that uses projects can be found at https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span></span>
   
   <span data-ttu-id="a5592-641">I bu yönergeleri izleyin ve bu belgede hello R kod örnekleri için bir proje oluşturun öneririz.</span><span class="sxs-lookup"><span data-stu-id="a5592-641">I recommend that you follow these directions and create a project for hello R code examples in this document.</span></span>  
2. <span data-ttu-id="a5592-642">Düzenleme ve R kodu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="a5592-642">Editing and executing R code</span></span>
   
   <span data-ttu-id="a5592-643">Rstudio'dan düzenleme ve R kod yürütmek için tümleşik bir ortam sağlar.</span><span class="sxs-lookup"><span data-stu-id="a5592-643">RStudio provides an integrated environment for editing and executing R code.</span></span> <span data-ttu-id="a5592-644">Belge https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="a5592-644">Documentation can be found at https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span></span>
3. <span data-ttu-id="a5592-645">Hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="a5592-645">Debugging</span></span>
   
   <span data-ttu-id="a5592-646">Rstudio'dan güçlü hata ayıklama özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="a5592-646">RStudio includes powerful debugging capabilities.</span></span> <span data-ttu-id="a5592-647">Bu özellikler için belgeleri https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio ' dir.</span><span class="sxs-lookup"><span data-stu-id="a5592-647">Documentation for these features is at https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span></span>
   
   <span data-ttu-id="a5592-648">Merhaba kesme noktası sorun giderme özellikleri https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting belgelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="a5592-648">hello breakpoint troubleshooting features are documented at https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span></span>

## <span data-ttu-id="a5592-649"><a id="appendixb"></a>Ek B: Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="a5592-649"><a id="appendixb"></a>APPENDIX B: Further reading</span></span>
<span data-ttu-id="a5592-650">Eğitmen kapsar hello temel programlama bu R hangi, Azure Machine Learning Studio'da R dil toouse hello.</span><span class="sxs-lookup"><span data-stu-id="a5592-650">This R programming tutorial covers hello basics of what you need toouse hello R language with Azure Machine Learning Studio.</span></span> <span data-ttu-id="a5592-651">R ile bilmiyorsanız, iki tanıtımları CRAN üzerinde kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="a5592-651">If you are not familiar with R, two introductions are available on CRAN:</span></span>

* <span data-ttu-id="a5592-652">R Emmanuel Paradis tarafından yeni başlayanlar için http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf en iyi toostart ' dir.</span><span class="sxs-lookup"><span data-stu-id="a5592-652">R for Beginners by Emmanuel Paradis is a good place toostart at http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span></span>  
* <span data-ttu-id="a5592-653">Bir giriş tooR W. n tarafından</span><span class="sxs-lookup"><span data-stu-id="a5592-653">An Introduction tooR by W. N.</span></span> <span data-ttu-id="a5592-654">Venables et.</span><span class="sxs-lookup"><span data-stu-id="a5592-654">Venables et.</span></span> <span data-ttu-id="a5592-655">Al.</span><span class="sxs-lookup"><span data-stu-id="a5592-655">al.</span></span> <span data-ttu-id="a5592-656">biraz daha derinliğinde, http://cran.r-project.org/doc/manuals/R-intro.html geçer.</span><span class="sxs-lookup"><span data-stu-id="a5592-656">goes into a bit more depth, at http://cran.r-project.org/doc/manuals/R-intro.html.</span></span>

<span data-ttu-id="a5592-657">Başlamanıza yardımcı olabilecek R birçok books vardır.</span><span class="sxs-lookup"><span data-stu-id="a5592-657">There are many books on R that can help you get started.</span></span> <span data-ttu-id="a5592-658">Yararlı bulabilirim birkaç şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a5592-658">Here are a few I find useful:</span></span>

* <span data-ttu-id="a5592-659">Merhaba resim R Programming: A Tur, istatistiksel yazılım Norman Matloff tarafından tasarımdır mükemmel giriş tooprogramming r içinde</span><span class="sxs-lookup"><span data-stu-id="a5592-659">hello Art of R Programming: A Tour of Statistical Software Design by Norman Matloff is an excellent introduction tooprogramming in R.</span></span>  
* <span data-ttu-id="a5592-660">R Kılavuzu Paul Teetor tarafından bir sorunu ve çözümü yaklaşım toousing r sağlar</span><span class="sxs-lookup"><span data-stu-id="a5592-660">R Cookbook by Paul Teetor provides a problem and solution approach toousing R.</span></span>  
* <span data-ttu-id="a5592-661">Eylem Robert Kabacoff tarafından R başka yararlı tanıtım Rehberi ' dir.</span><span class="sxs-lookup"><span data-stu-id="a5592-661">R in Action by Robert Kabacoff is another useful introductory book.</span></span> <span data-ttu-id="a5592-662">Merhaba Yardımcısı hızlı R Web sitesi http://www.statmethods.net/ en kullanışlı bir kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="a5592-662">hello companion Quick R website is a useful resource at http://www.statmethods.net/.</span></span>
* <span data-ttu-id="a5592-663">R Inferno CAN yanıklara tarafından r hello Defteri'nde programlamada karşılaştı hassas ve zor konular sayısıyla ilgilidir şaşırtıcı esprili bir kitap ücretsiz http://www.burns-stat.com/documents/books/the-r-inferno/ kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a5592-663">R Inferno by Patrick Burns is a surprisingly humorous book that deals with a number of tricky and difficult topics that can be encountered when programming in R. hello book is available for free at http://www.burns-stat.com/documents/books/the-r-inferno/.</span></span>
* <span data-ttu-id="a5592-664">Derinlemesine Gelişmiş konular R, içine istiyorsanız hello defteri Gelişmiş R Hadley Wickham tarafından bakmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="a5592-664">If you want a deep dive into advanced topics in R, have a look at hello book Advanced R by Hadley Wickham.</span></span> <span data-ttu-id="a5592-665">Bu kitap çevrimiçi sürümünü Hello ücretsiz http://adv-r.had.co.nz/ kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a5592-665">hello online version of this book is available for free at http://adv-r.had.co.nz/.</span></span>

<span data-ttu-id="a5592-666">Merhaba CRAN görev görünümü zaman serisi çözümleme için bir katalog R zaman serisi paketlerin bulunabilir: http://cran.r-project.org/web/views/TimeSeries.html.</span><span class="sxs-lookup"><span data-stu-id="a5592-666">A catalogue of R time series packages can be found in hello CRAN Task View for time series analysis: http://cran.r-project.org/web/views/TimeSeries.html.</span></span> <span data-ttu-id="a5592-667">Belirli bir zaman serisi nesnesi paketleri hakkında daha fazla bilgi için bu paket için toohello belgelerine başvurmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a5592-667">For information on specific time series object packages, you should refer toohello documentation for that package.</span></span>

<span data-ttu-id="a5592-668">Merhaba kitap Paul Cowpertwait ve Barış Metcalfe r Giriş zaman serisi zaman serisi çözümleme için giriş toousing R sağlar.</span><span class="sxs-lookup"><span data-stu-id="a5592-668">hello book Introductory Time Series with R by Paul Cowpertwait and Andrew Metcalfe provides an introduction toousing R for time series analysis.</span></span> <span data-ttu-id="a5592-669">Çok fazla teorik metinleri R örnekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="a5592-669">Many more theoretical texts provide R examples.</span></span>

<span data-ttu-id="a5592-670">Harika bazı Internet kaynakların:</span><span class="sxs-lookup"><span data-stu-id="a5592-670">Some great internet resources:</span></span>

* <span data-ttu-id="a5592-671">DataCamp: Hello rahatlık tarayıcınızın video dersleri ve kodlama alıştırmaları içinde R DataCamp öğretir.</span><span class="sxs-lookup"><span data-stu-id="a5592-671">DataCamp: DataCamp teaches R in hello comfort of your browser with video lessons and coding exercises.</span></span> <span data-ttu-id="a5592-672">Etkileşimli öğreticiler hello son R teknikleri ve paketleri vardır.</span><span class="sxs-lookup"><span data-stu-id="a5592-672">There are interactive tutorials on hello latest R techniques and packages.</span></span> <span data-ttu-id="a5592-673">Merhaba ücretsiz etkileşimli R https://www.datacamp.com/courses/introduction-to-r Öğreticisi</span><span class="sxs-lookup"><span data-stu-id="a5592-673">Take hello free interactive R tutorial at https://www.datacamp.com/courses/introduction-to-r</span></span>
* <span data-ttu-id="a5592-674">Bir alma üzerinde R ile Programiz https://www.programiz.com/r-programming Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="a5592-674">A guide on Getting started with R from Programiz https://www.programiz.com/r-programming</span></span>
* <span data-ttu-id="a5592-675">Bir hızlı R Öğreticisi tarafından Kelly siyah Clarkson University http://www.cyclismo.org/tutorial/R/ gelen</span><span class="sxs-lookup"><span data-stu-id="a5592-675">A quick R tutorial by Kelly Black from Clarkson University http://www.cyclismo.org/tutorial/R/</span></span>
* <span data-ttu-id="a5592-676">R http://www.ComputerWorld.com/article/2497464/Business-intelligence-60-r-Resources-to-improve-Your-Data-skills.HTML listelenen 60 + kaynakları</span><span class="sxs-lookup"><span data-stu-id="a5592-676">60+ R resources listed at http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span></span>

<!--Image references-->
[1]: ./media/machine-learning-r-quickstart/fig1.png
[2]: ./media/machine-learning-r-quickstart/fig2.png
[3]: ./media/machine-learning-r-quickstart/fig3.png
[4]: ./media/machine-learning-r-quickstart/fig4.png
[5]: ./media/machine-learning-r-quickstart/fig5.png
[6]: ./media/machine-learning-r-quickstart/fig6.png
[7]: ./media/machine-learning-r-quickstart/fig7.png
[8]: ./media/machine-learning-r-quickstart/fig8.png
[9]: ./media/machine-learning-r-quickstart/fig9.png
[10]: ./media/machine-learning-r-quickstart/fig10.png
[11]: ./media/machine-learning-r-quickstart/fig11.png
[12]: ./media/machine-learning-r-quickstart/fig12.png
[13]: ./media/machine-learning-r-quickstart/fig13.png
[14]: ./media/machine-learning-r-quickstart/fig14.png
[15]: ./media/machine-learning-r-quickstart/fig15.png
[16]: ./media/machine-learning-r-quickstart/fig16.png
[17]: ./media/machine-learning-r-quickstart/fig17.png
[18]: ./media/machine-learning-r-quickstart/fig18.png
[19]: ./media/machine-learning-r-quickstart/fig19.png
[20]: ./media/machine-learning-r-quickstart/fig20.png
[21]: ./media/machine-learning-r-quickstart/fig21.png
[22]: ./media/machine-learning-r-quickstart/fig22.png

[26]: ./media/machine-learning-r-quickstart/fig26.png

<!--links-->
[appendixa]: #appendixa
[download]: https://azurebigdatatutorials.blob.core.windows.net/rquickstart/RFiles.zip


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
