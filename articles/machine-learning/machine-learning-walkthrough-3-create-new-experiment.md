---
title: "3. adım: yeni bir Machine Learning deneme oluşturma | Microsoft Docs"
description: "Adım 3 / hello geliştirmek Tahmine dayalı bir çözüm izlenecek yol: Azure Machine Learning Studio'da yeni bir eğitim deneme oluşturun."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 660e3c27-55ef-4c33-a4e9-dff4d1224630
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 4697d461a205c50c8d2aa6a3bd56697840cb30f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a><span data-ttu-id="036eb-103">Kılavuz Adımı 3: Yeni bir Azure Machine Learning denemesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="036eb-103">Walkthrough Step 3: Create a new Azure Machine Learning experiment</span></span>
<span data-ttu-id="036eb-104">Hello kılavuzun hello üçüncü adım budur [Azure Machine learning'de Tahmine dayalı analiz çözümü geliştirme](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="036eb-104">This is hello third step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="036eb-105">Bir Machine Learning çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="036eb-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="036eb-106">Mevcut verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="036eb-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. <span data-ttu-id="036eb-107">**Yeni bir deneme oluşturma**</span><span class="sxs-lookup"><span data-stu-id="036eb-107">**Create a new experiment**</span></span>
4. [<span data-ttu-id="036eb-108">Eğitmek ve hello modelleri değerlendir</span><span class="sxs-lookup"><span data-stu-id="036eb-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="036eb-109">Merhaba Web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="036eb-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="036eb-110">Merhaba Web hizmetine erişim</span><span class="sxs-lookup"><span data-stu-id="036eb-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="036eb-111">Bu kılavuzda Hello sonraki adım toocreate biz karşıya hello veri kümesi kullanan bir Machine Learning Studio'da bir denemeyi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="036eb-111">hello next step in this walkthrough is toocreate an experiment in Machine Learning Studio that uses hello dataset we uploaded.</span></span>  

1. <span data-ttu-id="036eb-112">Studio'da sırasıyla **+ yeni** hello pencerenin hello altındaki.</span><span class="sxs-lookup"><span data-stu-id="036eb-112">In Studio, click **+NEW** at hello bottom of hello window.</span></span>
2. <span data-ttu-id="036eb-113">Seçin **deneme**ve ardından "Boş deneme" seçin.</span><span class="sxs-lookup"><span data-stu-id="036eb-113">Select **EXPERIMENT**, and then select "Blank Experiment".</span></span> 

    ![Yeni bir deneme oluşturma][0]

2. <span data-ttu-id="036eb-115">Select hello varsayılan hello tuvale hello başındaki ad denemeler ve toosomething anlamlı yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="036eb-115">Select hello default experiment name at hello top of hello canvas and rename it toosomething meaningful.</span></span>

    ![Denemeyi yeniden adlandırma][5]
   
   > [!TIP]
   > <span data-ttu-id="036eb-117">İyi bir uygulama toofill konusu **Özet** ve **açıklama** hello hello denemesinde için **özellikleri** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="036eb-117">It's a good practice toofill in **Summary** and **Description** for hello experiment in hello **Properties** pane.</span></span> <span data-ttu-id="036eb-118">Böylece daha sonra görünüyor herkes amaçlar ve yöntemler anlayabileceği fırsat toodocument hello deneme hello bu özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="036eb-118">These properties give you hello chance toodocument hello experiment so that anyone who looks at it later will understand your goals and methodology.</span></span>
   > 
   > ![Deneme özellikleri][6]
   > 
3. <span data-ttu-id="036eb-120">İçinde Hello modül paleti toohello sol tarafındaki hello deneme tuvalinin genişletin **kaydedilen veri kümeleri**.</span><span class="sxs-lookup"><span data-stu-id="036eb-120">In hello module palette toohello left of hello experiment canvas, expand **Saved Datasets**.</span></span>
4. <span data-ttu-id="036eb-121">Bul hello veri kümesi altında oluşturduğunuz **My veri kümeleri** hello tuvale sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="036eb-121">Find hello dataset you created under **My Datasets** and drag it onto hello canvas.</span></span> <span data-ttu-id="036eb-122">Hello hello adı girerek hello dataset bulabilirsiniz **arama** kutusunun hello palet üstünde.</span><span class="sxs-lookup"><span data-stu-id="036eb-122">You can also find hello dataset by entering hello name in hello **Search** box above hello palette.</span></span>  

    ![Merhaba dataset toohello deneme ekleme][7]

## <a name="prepare-hello-data"></a><span data-ttu-id="036eb-124">Merhaba verileri hazırlama</span><span class="sxs-lookup"><span data-stu-id="036eb-124">Prepare hello data</span></span>
<span data-ttu-id="036eb-125">Görüntüleyebileceğiniz hello veri ilk 100 satırı ve bazı istatistiksel bilgileri hello tam veri kümesi için hello: hello veri kümesi (Merhaba küçük bir daire hello altındaki) hello çıkış bağlantı noktasına tıklayın ve **Görselleştir**.</span><span class="sxs-lookup"><span data-stu-id="036eb-125">You can view hello first 100 rows of hello data and some statistical information for hello whole dataset: Click hello output port of hello dataset (hello small circle at hello bottom) and select **Visualize**.</span></span>  

<span data-ttu-id="036eb-126">Merhaba veri dosyası sütun başlıkları ile eşleşmedi geldiğinden Studio genel başlıkları sağlamıştır (Col1, Col2, *vb.*).</span><span class="sxs-lookup"><span data-stu-id="036eb-126">Because hello data file didn't come with column headings, Studio has provided generic headings (Col1, Col2, *etc.*).</span></span> <span data-ttu-id="036eb-127">Temel toocreating bir model iyi başlıkları değil, ancak bunlar hello verilerle daha kolay toowork hello denemesinde olun.</span><span class="sxs-lookup"><span data-stu-id="036eb-127">Good headings aren't essential toocreating a model, but they make it easier toowork with hello data in hello experiment.</span></span> <span data-ttu-id="036eb-128">Ayrıca, biz sonunda bu model bir web hizmeti yayımladığınızda, hello başlıkları hello sütunları toohello kullanıcı hello hizmetinin tanımlamaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="036eb-128">Also, when we eventually publish this model in a web service, hello headings help identify hello columns toohello user of hello service.</span></span>  

<span data-ttu-id="036eb-129">Sütun başlıkları hello kullanarak ekleyebiliriz [Düzenle meta veri] [ edit-metadata] modülü.</span><span class="sxs-lookup"><span data-stu-id="036eb-129">We can add column headings using hello [Edit Metadata][edit-metadata] module.</span></span>
<span data-ttu-id="036eb-130">Merhaba kullandığınız [Düzenle meta veri] [ edit-metadata] modülü toochange meta veri kümesiyle ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="036eb-130">You use hello [Edit Metadata][edit-metadata] module toochange metadata associated with a dataset.</span></span> <span data-ttu-id="036eb-131">Bu durumda, daha fazla kolay adlar tooprovide sütun başlıkları kullanırız.</span><span class="sxs-lookup"><span data-stu-id="036eb-131">In this case, we use it tooprovide more friendly names for column headings.</span></span> 

<span data-ttu-id="036eb-132">toouse [Düzenle meta veri][edit-metadata], hangi sütunların toomodify (Bu durumda, bunların tümünün.) ilk belirtin Ardından, bu sütunları (sütun başlıklarını değiştirme bu durumda,.) üzerinde gerçekleştirilen hello eylem toobe belirtin</span><span class="sxs-lookup"><span data-stu-id="036eb-132">toouse [Edit Metadata][edit-metadata], you first specify which columns toomodify (in this case, all of them.) Next, you specify hello action toobe performed on those columns (in this case, changing column headings.)</span></span>

1. <span data-ttu-id="036eb-133">Merhaba "meta" Merhaba modül paletindeki yazın **arama** kutusu.</span><span class="sxs-lookup"><span data-stu-id="036eb-133">In hello module palette, type "metadata" in hello **Search** box.</span></span> <span data-ttu-id="036eb-134">Merhaba [Düzenle meta veri] [ edit-metadata] hello modül listesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="036eb-134">hello [Edit Metadata][edit-metadata] appears in hello module list.</span></span>

2. <span data-ttu-id="036eb-135">Merhaba sürükleyip [Düzenle meta veri] [ edit-metadata] hello modülü tuvale ve daha önce eklediğimiz hello dataset bırakın.</span><span class="sxs-lookup"><span data-stu-id="036eb-135">Click and drag hello [Edit Metadata][edit-metadata] module onto hello canvas and drop it below hello dataset we added earlier.</span></span>

3. <span data-ttu-id="036eb-136">Merhaba dataset toohello bağlanmak [Düzenle meta veri][edit-metadata]: hello veri kümesi (Merhaba küçük bir daire hello dataset hello sonundaki) hello çıkış bağlantı noktasına tıklayın, toohello giriş bağlantı noktası sürükleyin [meta verileri düzenleme ] [ edit-metadata] (Merhaba küçük daire hello modülü hello üstündeki), hello fare düğmesini serbest bırakın.</span><span class="sxs-lookup"><span data-stu-id="036eb-136">Connect hello dataset toohello [Edit Metadata][edit-metadata]: click hello output port of hello dataset (hello small circle at hello bottom of hello dataset), drag toohello input port of [Edit Metadata][edit-metadata] (hello small circle at hello top of hello module), then release hello mouse button.</span></span> <span data-ttu-id="036eb-137">ya da hello tuval üzerinde hareket ettirin olsa bile hello veri kümesi ve modül bağlı kalır.</span><span class="sxs-lookup"><span data-stu-id="036eb-137">hello dataset and module remain connected even if you move either around on hello canvas.</span></span>
   
   <span data-ttu-id="036eb-138">Merhaba deneme bu gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="036eb-138">hello experiment should now look something like this:</span></span>  
   
   ![Düzen meta verileri ekleme][1]
   
   <span data-ttu-id="036eb-140">Merhaba kırmızı bir ünlem işareti Biz bu modül için hello özellikleri henüz ayarlamadıysanız olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="036eb-140">hello red exclamation mark indicates that we haven't set hello properties for this module yet.</span></span> <span data-ttu-id="036eb-141">Biz bu sonraki gerçekleştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="036eb-141">We'll do that next.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="036eb-142">Bir yorum tooa modülü bağlantısındaki hello modülü ve metin girme tarafından ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="036eb-142">You can add a comment tooa module by double-clicking hello module and entering text.</span></span> <span data-ttu-id="036eb-143">Bu, bir bakışta görmenize yardımcı hangi hello modülün denemenizde yapıyor.</span><span class="sxs-lookup"><span data-stu-id="036eb-143">This can help you see at a glance what hello module is doing in your experiment.</span></span> <span data-ttu-id="036eb-144">Bu durumda, hello çift [Düzenle meta veri] [ edit-metadata] modülü ve türü hello Açıklama "Ekle sütun başlıkları".</span><span class="sxs-lookup"><span data-stu-id="036eb-144">In this case, double-click hello [Edit Metadata][edit-metadata] module and type hello comment "Add column headings".</span></span> <span data-ttu-id="036eb-145">Başka bir yerde hello tuvale tooclose hello metin kutusuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="036eb-145">Click anywhere else on hello canvas tooclose hello text box.</span></span> <span data-ttu-id="036eb-146">toodisplay Merhaba yorum, hello modül hello aşağı oku tıklatın.</span><span class="sxs-lookup"><span data-stu-id="036eb-146">toodisplay hello comment, click hello down-arrow on hello module.</span></span>
   > 
   > ![Meta veriler modülü açıklama eklendi Düzenle][8]
   > 
4. <span data-ttu-id="036eb-148">Seçin [Düzenle meta veri][edit-metadata]ve hello **özellikleri** bölmesinde toohello hello tuvale sağına tıklayın **başlatma Sütun seçiciyi**.</span><span class="sxs-lookup"><span data-stu-id="036eb-148">Select [Edit Metadata][edit-metadata], and in hello **Properties** pane toohello right of hello canvas, click **Launch column selector**.</span></span>

5. <span data-ttu-id="036eb-149">Merhaba, **sütunları seçin** iletişim, tüm satırlarda hello select **kullanılabilir sütunlar** tıklatıp > toomove bunları çok**seçili sütun**.</span><span class="sxs-lookup"><span data-stu-id="036eb-149">In hello **Select columns** dialog, select all hello rows in **Available Columns** and click > toomove them too**Selected Columns**.</span></span>
   <span data-ttu-id="036eb-150">Merhaba iletişim aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="036eb-150">hello dialog should look like this:</span></span>

   ![Seçili tüm sütunlarla Sütun Seçici][2]

6. <span data-ttu-id="036eb-152">Merhaba tıklatın **Tamam** onay işareti.</span><span class="sxs-lookup"><span data-stu-id="036eb-152">Click hello **OK** check mark.</span></span>

7. <span data-ttu-id="036eb-153">Merhaba edilene **özellikleri** bölmesinde, hello arayın **yeni sütun adları** parametresi.</span><span class="sxs-lookup"><span data-stu-id="036eb-153">Back in hello **Properties** pane, look for hello **New column names** parameter.</span></span> <span data-ttu-id="036eb-154">Bu alanda virgülle ve sütun sırasını ayrılmış hello kümesindeki hello 21 sütunların adlarının bir listesini girin.</span><span class="sxs-lookup"><span data-stu-id="036eb-154">In this field, enter a list of names for hello 21 columns in hello dataset, separated by commas and in column order.</span></span> <span data-ttu-id="036eb-155">Merhaba dataset belgelerindeki hello UCI Web sitesinde hello sütun adları elde edebilirsiniz veya kolaylık sağlamak için kopyalama ve yapıştırma listesi aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="036eb-155">You can obtain hello columns names from hello dataset documentation on hello UCI website, or for convenience you can copy and paste hello following list:</span></span>  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   <span data-ttu-id="036eb-156">Merhaba Özellikler bölmesinde şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="036eb-156">hello Properties pane looks like this:</span></span>
   
   ![Özellikleri düzenleme meta veriler için][3]

> [!TIP]
> <span data-ttu-id="036eb-158">Tooverify hello sütun başlıkları istiyorsanız hello denemeyi çalıştırın (tıklatın **çalıştırmak** hello deneme tuvalinin altında).</span><span class="sxs-lookup"><span data-stu-id="036eb-158">If you want tooverify hello column headings, run hello experiment (click **RUN** below hello experiment canvas).</span></span> <span data-ttu-id="036eb-159">Çalışan bittiğinde (yeşil bir onay işareti görünür [Düzenle meta veri][edit-metadata]), hello hello çıkış bağlantı noktasına tıklayın [Düzenle meta veri] [ edit-metadata] Modül ' nı seçip **Görselleştir**.</span><span class="sxs-lookup"><span data-stu-id="036eb-159">When it finishes running (a green check mark appears on [Edit Metadata][edit-metadata]), click hello output port of hello [Edit Metadata][edit-metadata] module, and select **Visualize**.</span></span> <span data-ttu-id="036eb-160">Herhangi bir modül hello çıktısını hello görüntüleyebilirsiniz aynı şekilde tooview hello ilerlemesini hello deneme hello verilerine.</span><span class="sxs-lookup"><span data-stu-id="036eb-160">You can view hello output of any module in hello same way tooview hello progress of hello data through hello experiment.</span></span>
> 
> 

## <a name="create-training-and-test-datasets"></a><span data-ttu-id="036eb-161">Eğitim oluşturmak ve veri kümelerini test etme</span><span class="sxs-lookup"><span data-stu-id="036eb-161">Create training and test datasets</span></span>
<span data-ttu-id="036eb-162">Bazı veri tootrain hello modeli ve bazı tootest ihtiyacımız onu.</span><span class="sxs-lookup"><span data-stu-id="036eb-162">We need some data tootrain hello model and some tootest it.</span></span>
<span data-ttu-id="036eb-163">Merhaba sonraki adımında hello deneme biz hello dataset iki ayrı kümelerine bölünmüş şekilde: modelimizi ve test için bir tane eğitim için bir tane.</span><span class="sxs-lookup"><span data-stu-id="036eb-163">So in hello next step of hello experiment, we split hello dataset into two separate datasets: one for training our model and one for testing it.</span></span>

<span data-ttu-id="036eb-164">toodo bunu hello kullanırız [bölünmüş veri] [ split] modülü.</span><span class="sxs-lookup"><span data-stu-id="036eb-164">toodo this, we use hello [Split Data][split] module.</span></span>  

1. <span data-ttu-id="036eb-165">Hello bulur [bölünmüş veri] [ split] modül hello tuvale sürükleyin ve toohello bağlayın [Düzenle meta veri] [ edit-metadata] modülü.</span><span class="sxs-lookup"><span data-stu-id="036eb-165">Find hello [Split Data][split] module, drag it onto hello canvas, and connect it toohello [Edit Metadata][edit-metadata] module.</span></span>

2. <span data-ttu-id="036eb-166">Varsayılan olarak, hello bölünmüş 0,5 ve hello orandır **Randomized bölünmüş** parametrenin ayarlanmış.</span><span class="sxs-lookup"><span data-stu-id="036eb-166">By default, hello split ratio is 0.5 and hello **Randomized split** parameter is set.</span></span> <span data-ttu-id="036eb-167">Bu rastgele yarı hello veri çıkışı hello bir bağlantı noktası üzerinden olduğu anlamına gelir [bölünmüş veri] [ split] modülü ve yarı ile Merhaba diğer.</span><span class="sxs-lookup"><span data-stu-id="036eb-167">This means that a random half of hello data is output through one port of hello [Split Data][split] module, and half through hello other.</span></span> <span data-ttu-id="036eb-168">Siz bu parametreleri ayarlamak yanı sıra hello **rastgele doldurma** parametresi, eğitim ve test verileri arasında bölme toochange hello.</span><span class="sxs-lookup"><span data-stu-id="036eb-168">You can adjust these parameters, as well as hello **Random seed** parameter, toochange hello split between training and testing data.</span></span> <span data-ttu-id="036eb-169">Bu örnekte, biz bunları olarak bırakın-değil.</span><span class="sxs-lookup"><span data-stu-id="036eb-169">For this example, we leave them as-is.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="036eb-170">Merhaba özelliği **hello satırlar için kesir değerini ilk çıkış veri kümesi** çıkışı hello üzerinden hello verilerin ne kadar olacağını belirler *sol* çıkış bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="036eb-170">hello property **Fraction of rows in hello first output dataset** determines how much of hello data is output through hello *left* output port.</span></span> <span data-ttu-id="036eb-171">Örneğin, hello oranı too0.7 ayarlarsanız, % 70'hello veri çıkışı hello doğru bağlantı noktası üzerinden sol bağlantı noktası ve % 30 hello üzerinden olabilir.</span><span class="sxs-lookup"><span data-stu-id="036eb-171">For instance, if you set hello ratio too0.7, then 70% of hello data is output through hello left port and 30% through hello right port.</span></span>  
   > 
   > 

3. <span data-ttu-id="036eb-172">Merhaba çift [bölünmüş veri] [ split] modülü ve hello açıklama girin, "eğitim ve test veri Böl % 50".</span><span class="sxs-lookup"><span data-stu-id="036eb-172">Double-click hello [Split Data][split] module and enter hello comment, "Training/testing data split 50%".</span></span> 

<span data-ttu-id="036eb-173">Merhaba hello çıkışları kullanırız [bölünmüş veri] [ split] ancak biz gibi çalışır, ancak şimdi toouse seçin hello eğitim verisi olarak sol çıkış ve sağa hello modülü çıkış olarak test verileri.</span><span class="sxs-lookup"><span data-stu-id="036eb-173">We can use hello outputs of hello [Split Data][split] module however we like, but let's choose toouse hello left output as training data and hello right output as testing data.</span></span>  

<span data-ttu-id="036eb-174">Hello belirtildiği gibi [önceki adımı](machine-learning-walkthrough-2-upload-data.md), düşük olarak yüksek kredi riski misclassifying hello maliyetidir beş kez yüksek olarak düşük kredi riski misclassifying hello maliyeti daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="036eb-174">As mentioned in hello [previous step](machine-learning-walkthrough-2-upload-data.md), hello cost of misclassifying a high credit risk as low is five times higher than hello cost of misclassifying a low credit risk as high.</span></span> <span data-ttu-id="036eb-175">Bu tooaccount, bu maliyet işlevi yansıtır yeni bir veri kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="036eb-175">tooaccount for this, we generate a new dataset that reflects this cost function.</span></span> <span data-ttu-id="036eb-176">Her düşük riskli örnek çoğaltılmaz sırada hello yeni kümesindeki her yüksek riskli örnek beş kez çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="036eb-176">In hello new dataset, each high risk example is replicated five times, while each low risk example is not replicated.</span></span>   

<span data-ttu-id="036eb-177">Bu çoğaltma yapabiliriz R kodu kullanarak:</span><span class="sxs-lookup"><span data-stu-id="036eb-177">We can do this replication using R code:</span></span>  

1. <span data-ttu-id="036eb-178">Bulma ve hello sürükleyin [R betiği yürütün] [ execute-r-script] hello deneme tuvale modülü.</span><span class="sxs-lookup"><span data-stu-id="036eb-178">Find and drag hello [Execute R Script][execute-r-script] module onto hello experiment canvas.</span></span> 

2. <span data-ttu-id="036eb-179">Merhaba çıkış bağlantı noktasına sol hello bağlanmak [bölünmüş veri] [ split] modülü toohello Merhaba ilk bağlantı noktası ("Dataset1") giriş [R betiği yürütün] [ execute-r-script] Modül.</span><span class="sxs-lookup"><span data-stu-id="036eb-179">Connect hello left output port of hello [Split Data][split] module toohello first input port ("Dataset1") of hello [Execute R Script][execute-r-script] module.</span></span>

3. <span data-ttu-id="036eb-180">Merhaba çift [R betiği yürütün] [ execute-r-script] modülü ve hello yorum girin "maliyet ayarlaması Ayarla".</span><span class="sxs-lookup"><span data-stu-id="036eb-180">Double-click hello [Execute R Script][execute-r-script] module and enter hello comment, "Set cost adjustment".</span></span>

4. <span data-ttu-id="036eb-181">Merhaba, **özellikleri** bölmesinde, delete hello varsayılan hello metinde **R betiği** parametre ve bu komut dosyasını girin:</span><span class="sxs-lookup"><span data-stu-id="036eb-181">In hello **Properties** pane, delete hello default text in hello **R Script** parameter and enter this script:</span></span>
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![R betiği hello R betiği yürütün Modülü][9]

<span data-ttu-id="036eb-183">Bu aynı çoğaltma işlemi için her çıktı Merhaba, toodo ihtiyacımız [bölünmüş veri] [ split] sahip eğitim ve test verileri bu hello hello şekilde aynı modülü maliyet ayarlama.</span><span class="sxs-lookup"><span data-stu-id="036eb-183">We need toodo this same replication operation for each output of hello [Split Data][split] module so that hello training and testing data have hello same cost adjustment.</span></span> <span data-ttu-id="036eb-184">Merhaba çoğaltarak budur en kolay yolu toodo hello [R betiği yürütün] [ execute-r-script] modülü biz yalnızca yapılan ve toohello bağlanan diğer çıkış başlangıç bağlantı noktası [bölünmüş veri] [ split] modülü.</span><span class="sxs-lookup"><span data-stu-id="036eb-184">hello easiest way toodo this is by duplicating hello [Execute R Script][execute-r-script] module we just made and connecting it toohello other output port of hello [Split Data][split] module.</span></span>

1. <span data-ttu-id="036eb-185">Sağ hello [R betiği yürütün] [ execute-r-script] modülü ve select **kopya**.</span><span class="sxs-lookup"><span data-stu-id="036eb-185">Right-click hello [Execute R Script][execute-r-script] module and select **Copy**.</span></span>

2. <span data-ttu-id="036eb-186">Merhaba deneme tuvalinin sağ tıklatıp **Yapıştır**.</span><span class="sxs-lookup"><span data-stu-id="036eb-186">Right-click hello experiment canvas and select **Paste**.</span></span>

3. <span data-ttu-id="036eb-187">Merhaba yeni modül konumu sürükleyin ve hello hello sağ çıkış bağlantı noktasına bağlanmak [bölünmüş veri] [ split] modülü toohello ilk giriş bağlantı noktası bu yeni [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="036eb-187">Drag hello new module into position, and then connect hello right output port of hello [Split Data][split] module toohello first input port of this new [Execute R Script][execute-r-script] module.</span></span> 

4. <span data-ttu-id="036eb-188">Merhaba tuvale Hello altındaki tıklatın **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="036eb-188">At hello bottom of hello canvas, click **Run**.</span></span> 

> [!TIP]
> <span data-ttu-id="036eb-189">Merhaba R betiği yürütün modülü Hello kopyasını hello aynı hello özgün modülü olarak komut dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="036eb-189">hello copy of hello Execute R Script module contains hello same script as hello original module.</span></span> <span data-ttu-id="036eb-190">Merhaba tuvalde bir modül kopyalayıp, hello kopyalama hello özgün tüm hello özelliklerini korur.</span><span class="sxs-lookup"><span data-stu-id="036eb-190">When you copy and paste a module on hello canvas, hello copy retains all hello properties of hello original.</span></span>  
> 
> 

<span data-ttu-id="036eb-191">Bizim denemeyi şimdi şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="036eb-191">Our experiment now looks something like this:</span></span>

![Bölünmüş modülü ve R betiklerini ekleme][4]

<span data-ttu-id="036eb-193">Denemelerinizi içinde R betiklerini kullanma hakkında daha fazla bilgi için bkz: [denemenizi R ile genişletme](machine-learning-extend-your-experiment-with-r.md).</span><span class="sxs-lookup"><span data-stu-id="036eb-193">For more information on using R scripts in your experiments, see [Extend your experiment with R](machine-learning-extend-your-experiment-with-r.md).</span></span>

<span data-ttu-id="036eb-194">**Sonraki: [eğitimi ve hello modelleri değerlendir](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span><span class="sxs-lookup"><span data-stu-id="036eb-194">**Next: [Train and evaluate hello models](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span></span>

[0]: ./media/machine-learning-walkthrough-3-create-new-experiment/create-new-experiment.png
[5]: ./media/machine-learning-walkthrough-3-create-new-experiment/rename-experiment.png
[6]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-properties.png
[7]: ./media/machine-learning-walkthrough-3-create-new-experiment/add-dataset-to-experiment.png
[8]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-with-comment.png
[9]: ./media/machine-learning-walkthrough-3-create-new-experiment/execute-r-script.png
[1]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-with-edit-metadata-module.png
[2]: ./media/machine-learning-walkthrough-3-create-new-experiment/select-columns.png
[3]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-properties.png
[4]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
