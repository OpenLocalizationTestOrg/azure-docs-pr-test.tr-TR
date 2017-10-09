---
title: "2. adım: Verileri bir Machine Learning deneme yükleme | Microsoft Docs"
description: "Adım 2 / hello geliştirmek Tahmine dayalı bir çözüm izlenecek yol: karşıya yükleme Azure Machine Learning Studio'ya genel verilere depolanır."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 9f4bc52e-9919-4dea-90ea-5cf7cc506d85
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 0ea21dcca2d0934ed06508560cf85cf31b48ce6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a><span data-ttu-id="80375-103">Kılavuz Adımı 2: Mevcut verileri bir Azure Machine Learning denemesine yükleme</span><span class="sxs-lookup"><span data-stu-id="80375-103">Walkthrough Step 2: Upload existing data into an Azure Machine Learning experiment</span></span>
<span data-ttu-id="80375-104">Merhaba kılavuzun hello ikinci adım budur [Azure Machine learning'de Tahmine dayalı analiz çözümü geliştirme](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="80375-104">This is hello second step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="80375-105">Bir Machine Learning çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="80375-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. <span data-ttu-id="80375-106">**Mevcut verileri yükleme**</span><span class="sxs-lookup"><span data-stu-id="80375-106">**Upload existing data**</span></span>
3. [<span data-ttu-id="80375-107">Yeni bir deneme oluşturma</span><span class="sxs-lookup"><span data-stu-id="80375-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="80375-108">Eğitmek ve hello modelleri değerlendir</span><span class="sxs-lookup"><span data-stu-id="80375-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="80375-109">Merhaba Web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="80375-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="80375-110">Merhaba Web hizmetine erişim</span><span class="sxs-lookup"><span data-stu-id="80375-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="80375-111">toodevelop kredi riski için Tahmine dayalı bir model, biz tootrain kullanın ve böylelikle hello modeli test veri gerekir.</span><span class="sxs-lookup"><span data-stu-id="80375-111">toodevelop a predictive model for credit risk, we need data that we can use tootrain and then test hello model.</span></span> <span data-ttu-id="80375-112">Bu kılavuzda hello UC Irvine Machine Learning depodan hello "UCI Statlog (Almanca kredi veri) veri kümesi" kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="80375-112">For this walkthrough, we'll use hello "UCI Statlog (German Credit Data) Data Set" from hello UC Irvine Machine Learning repository.</span></span> <span data-ttu-id="80375-113">Burada bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="80375-113">You can find it here:</span></span>  
<span data-ttu-id="80375-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ML/DataSets/Statlog+(German+Credit+Data)</a></span><span class="sxs-lookup"><span data-stu-id="80375-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a></span></span>

<span data-ttu-id="80375-115">Adlı hello dosya kullanacağız **german.data**.</span><span class="sxs-lookup"><span data-stu-id="80375-115">We'll use hello file named **german.data**.</span></span> <span data-ttu-id="80375-116">Bu dosya tooyour yerel sabit diske yükleyin.</span><span class="sxs-lookup"><span data-stu-id="80375-116">Download this file tooyour local hard drive.</span></span>  

<span data-ttu-id="80375-117">Merhaba **german.data** dataset kredi için son 1000 başvuran 20 değişkenlerin satırları içerir.</span><span class="sxs-lookup"><span data-stu-id="80375-117">hello **german.data** dataset contains rows of 20 variables for 1000 past applicants for credit.</span></span> <span data-ttu-id="80375-118">Bu 20 değişkenleri hello veri kümesi'nin özellikler kümesini temsil eden (Merhaba *özelliği vektör*), her kredi başvuran için tanımlayıcı özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="80375-118">These 20 variables represent hello dataset's set of features (hello *feature vector*), which provides identifying characteristics for each credit applicant.</span></span> <span data-ttu-id="80375-119">Her satırda ek bir sütun düşük kredi riski ve 300 yüksek riskli olarak tanımlanan 700 başvuran ile Merhaba Başvuranın hesaplanan kredi riski temsil eder.</span><span class="sxs-lookup"><span data-stu-id="80375-119">An additional column in each row represents hello applicant's calculated credit risk, with 700 applicants identified as a low credit risk and 300 as a high risk.</span></span>

<span data-ttu-id="80375-120">Merhaba UCI hello özelliği vektör bu veriler için başlangıç özniteliklerini açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="80375-120">hello UCI website provides a description of hello attributes of hello feature vector for this data.</span></span> <span data-ttu-id="80375-121">Bu, finansal bilgileri, kredi geçmişi, çalışma durumu ve kişisel bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="80375-121">This includes financial information, credit history, employment status, and personal information.</span></span> <span data-ttu-id="80375-122">Her başvuran için ikili bir derecelendirme belirli bir düşük olup olmadığını gösteren veya yüksek olmuştur kredi riski.</span><span class="sxs-lookup"><span data-stu-id="80375-122">For each applicant, a binary rating has been given indicating whether they are a low or high credit risk.</span></span> 

<span data-ttu-id="80375-123">Bu veri tootrain bir Tahmine dayalı bir analiz modeli kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="80375-123">We'll use this data tootrain a predictive analytics model.</span></span> <span data-ttu-id="80375-124">Biz bittiğinde modelimizi mümkün tooaccept yeni bir tek bir özellik vektörünü olması ve çözemiyorsa düşük veya yüksek kredi riski olup olmadığını tahmin etmek.</span><span class="sxs-lookup"><span data-stu-id="80375-124">When we're done, our model should be able tooaccept a feature vector for a new individual and predict whether he or she is a low or high credit risk.</span></span>  

<span data-ttu-id="80375-125">Burada, ilginç geçiş verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="80375-125">Here's an interesting twist.</span></span> <span data-ttu-id="80375-126">Merhaba UCI Web sitesi belirtilenlerden hello veri kümesine açıklaması biz bir kişinin kredi riski misclassify varsa ne maliyetleri hello.</span><span class="sxs-lookup"><span data-stu-id="80375-126">hello description of hello dataset on hello UCI website mentions what it costs if we misclassify a person's credit risk.</span></span>
<span data-ttu-id="80375-127">Bir yüksek kredi riski gerçekten düşük kredi riski yapılandırabilecek için Hello modeli tahmin, hello modeli bir misclassification yaptı.</span><span class="sxs-lookup"><span data-stu-id="80375-127">If hello model predicts a high credit risk for someone who is actually a low credit risk, hello model has made a misclassification.</span></span>
<span data-ttu-id="80375-128">Ancak hello ters misclassification beş kez daha pahalı toohello finansal kuruluştan: hello modeli düşük kredi riski gerçekte bir yüksek kredi riski yapılandırabilecek için tahmin durumunda.</span><span class="sxs-lookup"><span data-stu-id="80375-128">But hello reverse misclassification is five times more costly toohello financial institution: if hello model predicts a low credit risk for someone who is actually a high credit risk.</span></span>

<span data-ttu-id="80375-129">Bu türdeki misclassification Hello maliyetini beş kez hello başka bir yolla misclassifying daha yüksek olmasını sağlamak, tootrain modelimizi istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="80375-129">So, we want tootrain our model so that hello cost of this latter type of misclassification is five times higher than misclassifying hello other way.</span></span>
<span data-ttu-id="80375-130">Bir basit yol toodo bu bizim deneme hello modelinde eğitim olduğunda yüksek kredi riski birisiyle temsil eden (beş kez) girişler çoğaltarak.</span><span class="sxs-lookup"><span data-stu-id="80375-130">One simple way toodo this when training hello model in our experiment is by duplicating (five times) those entries that represent someone with a high credit risk.</span></span> <span data-ttu-id="80375-131">Gerçekte yüksek riskli olduğunuzda hello modeli birisi düşük kredi riski olarak misclassifies, daha sonra hello model, aynı misclassification beş kez kez için her yinelenen yapar.</span><span class="sxs-lookup"><span data-stu-id="80375-131">Then, if hello model misclassifies someone as a low credit risk when they're actually a high risk, hello model does that same misclassification five times, once for each duplicate.</span></span> <span data-ttu-id="80375-132">Bu, bu hata hello eğitim sonuçlarında hello maliyetini artırır.</span><span class="sxs-lookup"><span data-stu-id="80375-132">This will increase hello cost of this error in hello training results.</span></span>


## <a name="convert-hello-dataset-format"></a><span data-ttu-id="80375-133">Merhaba dataset biçimine dönüştürün</span><span class="sxs-lookup"><span data-stu-id="80375-133">Convert hello dataset format</span></span>
<span data-ttu-id="80375-134">Merhaba özgün veri kümesi boş ayrılmış bir biçim kullanır.</span><span class="sxs-lookup"><span data-stu-id="80375-134">hello original dataset uses a blank-separated format.</span></span> <span data-ttu-id="80375-135">Virgül ile alanları değiştirerek hello dataset biz dönüştürme machine Learning Studio'da bir virgülle ayrılmış değer (CSV) dosyası ile daha iyi çalışır.</span><span class="sxs-lookup"><span data-stu-id="80375-135">Machine Learning Studio works better with a comma-separated value (CSV) file, so we'll convert hello dataset by replacing spaces with commas.</span></span>  

<span data-ttu-id="80375-136">Bu veriler birçok yolu tooconvert vardır.</span><span class="sxs-lookup"><span data-stu-id="80375-136">There are many ways tooconvert this data.</span></span> <span data-ttu-id="80375-137">Tek yönlü hello aşağıdaki Windows PowerShell komutunu kullanmaktır:</span><span class="sxs-lookup"><span data-stu-id="80375-137">One way is by using hello following Windows PowerShell command:</span></span>   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

<span data-ttu-id="80375-138">Merhaba UNIX azaltılabilir komutunu kullanarak başka bir yöntemdir:</span><span class="sxs-lookup"><span data-stu-id="80375-138">Another way is by using hello Unix sed command:</span></span>  

    sed 's/ /,/g' german.data > german.csv  

<span data-ttu-id="80375-139">Her iki durumda da adlı bir dosya hello verileri virgülle ayrılmış bir sürümünü oluşturduk **german.csv** , bizim deneme kullanırız.</span><span class="sxs-lookup"><span data-stu-id="80375-139">In either case, we have created a comma-separated version of hello data in a file named **german.csv** that we can use in our experiment.</span></span>

## <a name="upload-hello-dataset-toomachine-learning-studio"></a><span data-ttu-id="80375-140">Merhaba dataset tooMachine Learning Studio karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="80375-140">Upload hello dataset tooMachine Learning Studio</span></span>
<span data-ttu-id="80375-141">Dönüştürülen tooCSV biçiminde Hello verileri silindikten sonra tooupload ihtiyacımız Machine Learning Studio içine.</span><span class="sxs-lookup"><span data-stu-id="80375-141">Once hello data has been converted tooCSV format, we need tooupload it into Machine Learning Studio.</span></span> 

1. <span data-ttu-id="80375-142">Açık hello Machine Learning Studio giriş sayfası ([https://studio.azureml.net](https://studio.azureml.net)).</span><span class="sxs-lookup"><span data-stu-id="80375-142">Open hello Machine Learning Studio home page ([https://studio.azureml.net](https://studio.azureml.net)).</span></span> 

2. <span data-ttu-id="80375-143">Merhaba menüsünü ![menü][1] hello sol üst köşesinde hello penceresi tıklatın **Azure Machine Learning**seçin **Studio**ve oturum açın.</span><span class="sxs-lookup"><span data-stu-id="80375-143">Click hello menu ![Menu][1] in hello upper-left corner of hello window, click **Azure Machine Learning**, select **Studio**, and sign in.</span></span>

3. <span data-ttu-id="80375-144">Tıklatın **+ yeni** hello pencerenin hello altındaki.</span><span class="sxs-lookup"><span data-stu-id="80375-144">Click **+NEW** at hello bottom of hello window.</span></span>

4. <span data-ttu-id="80375-145">Seçin **DATASET**.</span><span class="sxs-lookup"><span data-stu-id="80375-145">Select **DATASET**.</span></span>

5. <span data-ttu-id="80375-146">Seçin **yerel DOSYADAN**.</span><span class="sxs-lookup"><span data-stu-id="80375-146">Select **FROM LOCAL FILE**.</span></span>

    ![Yerel bir dosyadan bir veri kümesi ekleyin][2]

6. <span data-ttu-id="80375-148">Merhaba, **yeni bir veri kümesi karşıya** iletişim kutusunda, tıklatın **Gözat** ve hello bulur **german.csv** , oluşturduğunuz dosya.</span><span class="sxs-lookup"><span data-stu-id="80375-148">In hello **Upload a new dataset** dialog, click **Browse** and find hello **german.csv** file you created.</span></span>

7. <span data-ttu-id="80375-149">Merhaba veri kümesi için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="80375-149">Enter a name for hello dataset.</span></span> <span data-ttu-id="80375-150">Bu kılavuzda "UCI Almanca kredi kartı verileri" çağrısı.</span><span class="sxs-lookup"><span data-stu-id="80375-150">For this walkthrough, call it "UCI German Credit Card Data".</span></span>

8. <span data-ttu-id="80375-151">Veri türü için **üst bilgi içeren genel CSV dosyası (. nh.csv)**.</span><span class="sxs-lookup"><span data-stu-id="80375-151">For data type, select **Generic CSV File With no header (.nh.csv)**.</span></span>

9. <span data-ttu-id="80375-152">İsterseniz bir açıklama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="80375-152">Add a description if you’d like.</span></span>

10. <span data-ttu-id="80375-153">Merhaba tıklatın **Tamam** onay işareti.</span><span class="sxs-lookup"><span data-stu-id="80375-153">Click hello **OK** check mark.</span></span>  

    ![Merhaba dataset karşıya yükle][3]

<span data-ttu-id="80375-155">Bir deneme kullandığımız bir veri kümesi modüle hello veri yükler.</span><span class="sxs-lookup"><span data-stu-id="80375-155">This uploads hello data into a dataset module that we can use in an experiment.</span></span>

<span data-ttu-id="80375-156">Merhaba tıklayarak tooStudio yüklediğiniz veri kümeleri yönetebilir **veri KÜMELERİ** sekmesini toohello hello Studio penceresinin sol.</span><span class="sxs-lookup"><span data-stu-id="80375-156">You can manage datasets that you've uploaded tooStudio by clicking hello **DATASETS** tab toohello left of hello Studio window.</span></span>

![Veri kümelerini yönetme][4]

<span data-ttu-id="80375-158">Bir deneme diğer veri türleri alma hakkında daha fazla bilgi için bkz: [eğitim verilerinizi Azure Machine Learning Studio'ya içeri](machine-learning-data-science-import-data.md).</span><span class="sxs-lookup"><span data-stu-id="80375-158">For more information about importing other types of data into an experiment, see [Import your training data into Azure Machine Learning Studio](machine-learning-data-science-import-data.md).</span></span>

<span data-ttu-id="80375-159">**Sonraki: [yeni bir deneme oluşturma](machine-learning-walkthrough-3-create-new-experiment.md)**</span><span class="sxs-lookup"><span data-stu-id="80375-159">**Next: [Create a new experiment](machine-learning-walkthrough-3-create-new-experiment.md)**</span></span>

[1]: media/machine-learning-walkthrough-2-upload-data/menu.png
[2]: media/machine-learning-walkthrough-2-upload-data/add-dataset.png
[3]: media/machine-learning-walkthrough-2-upload-data/upload-dataset.png
[4]: media/machine-learning-walkthrough-2-upload-data/dataset-list.png
