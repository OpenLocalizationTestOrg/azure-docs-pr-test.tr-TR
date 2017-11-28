---
title: "3. adım: yeni bir Machine Learning deneme oluşturma | Microsoft Docs"
description: "Adım 3 / geliştirme Tahmine dayalı bir çözüm izlenecek yol: Azure Machine Learning Studio'da yeni bir eğitim deneme oluşturun."
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
ms.openlocfilehash: cd410316910bce76f5c915c06e83b24c034481b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a><span data-ttu-id="40f19-103">Kılavuz Adımı 3: Yeni bir Azure Machine Learning denemesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="40f19-103">Walkthrough Step 3: Create a new Azure Machine Learning experiment</span></span>
<span data-ttu-id="40f19-104">Bu kılavuzu, üçüncü adımdır [Azure Machine learning'de Tahmine dayalı analiz çözümü geliştirme](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="40f19-104">This is the third step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="40f19-105">Bir Machine Learning çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="40f19-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="40f19-106">Mevcut verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="40f19-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. <span data-ttu-id="40f19-107">**Yeni bir deneme oluşturma**</span><span class="sxs-lookup"><span data-stu-id="40f19-107">**Create a new experiment**</span></span>
4. [<span data-ttu-id="40f19-108">Modelleri eğitme ve değerlendirme</span><span class="sxs-lookup"><span data-stu-id="40f19-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="40f19-109">Web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="40f19-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="40f19-110">Web hizmetine erişim</span><span class="sxs-lookup"><span data-stu-id="40f19-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="40f19-111">Bu kılavuzda bir sonraki adım, Machine Learning Studio'da biz karşıya veri kümesi kullanan bir denemeyi oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="40f19-111">The next step in this walkthrough is to create an experiment in Machine Learning Studio that uses the dataset we uploaded.</span></span>  

1. <span data-ttu-id="40f19-112">Studio'da sırasıyla **+ yeni** pencerenin altındaki.</span><span class="sxs-lookup"><span data-stu-id="40f19-112">In Studio, click **+NEW** at the bottom of the window.</span></span>
2. <span data-ttu-id="40f19-113">Seçin **deneme**ve ardından "Boş deneme" seçin.</span><span class="sxs-lookup"><span data-stu-id="40f19-113">Select **EXPERIMENT**, and then select "Blank Experiment".</span></span> 

    ![Yeni bir deneme oluşturma][0]

2. <span data-ttu-id="40f19-115">Tuvale üstündeki varsayılan deneme adını seçin ve anlamlı yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="40f19-115">Select the default experiment name at the top of the canvas and rename it to something meaningful.</span></span>

    ![Denemeyi yeniden adlandırma][5]
   
   > [!TIP]
   > <span data-ttu-id="40f19-117">Doldurmak için iyi bir uygulamadır **Özet** ve **açıklama** denemesinde için **özellikleri** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="40f19-117">It's a good practice to fill in **Summary** and **Description** for the experiment in the **Properties** pane.</span></span> <span data-ttu-id="40f19-118">Bu özellikler, böylece daha sonra görünüyor herkes amaçlar ve yöntemler anlayabileceği deneme belge şansı.</span><span class="sxs-lookup"><span data-stu-id="40f19-118">These properties give you the chance to document the experiment so that anyone who looks at it later will understand your goals and methodology.</span></span>
   > 
   > ![Deneme özellikleri][6]
   > 
3. <span data-ttu-id="40f19-120">Deneme tuvalinin solundaki modül paletindeki genişletin **kaydedilen veri kümeleri**.</span><span class="sxs-lookup"><span data-stu-id="40f19-120">In the module palette to the left of the experiment canvas, expand **Saved Datasets**.</span></span>
4. <span data-ttu-id="40f19-121">Altında oluşturduğunuz veri kümesi bulma **My veri kümeleri** ve tuvale sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="40f19-121">Find the dataset you created under **My Datasets** and drag it onto the canvas.</span></span> <span data-ttu-id="40f19-122">Veri kümesi adı girerek bulabileceğiniz **arama** kutusunun palet üstünde.</span><span class="sxs-lookup"><span data-stu-id="40f19-122">You can also find the dataset by entering the name in the **Search** box above the palette.</span></span>  

    ![Veri kümesi için deneme ekleyin][7]

## <a name="prepare-the-data"></a><span data-ttu-id="40f19-124">Verileri hazırlama</span><span class="sxs-lookup"><span data-stu-id="40f19-124">Prepare the data</span></span>
<span data-ttu-id="40f19-125">Veri ilk 100 satırı ve tüm veri kümesi için bazı istatistiksel bilgileri görüntüleyebilirsiniz: (küçük daire altındaki) kümesinin çıkış bağlantı noktasına tıklayın ve **Görselleştir**.</span><span class="sxs-lookup"><span data-stu-id="40f19-125">You can view the first 100 rows of the data and some statistical information for the whole dataset: Click the output port of the dataset (the small circle at the bottom) and select **Visualize**.</span></span>  

<span data-ttu-id="40f19-126">Veri dosyasındaki sütun başlıkları ile eşleşmedi geldiğinden Studio genel başlıkları sağlamıştır (Col1, Col2, *vb.*).</span><span class="sxs-lookup"><span data-stu-id="40f19-126">Because the data file didn't come with column headings, Studio has provided generic headings (Col1, Col2, *etc.*).</span></span> <span data-ttu-id="40f19-127">İyi başlıkları bir model oluşturmak için gerekli değildir, ancak bunlar denemede verilerle çalışmayı kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="40f19-127">Good headings aren't essential to creating a model, but they make it easier to work with the data in the experiment.</span></span> <span data-ttu-id="40f19-128">Ayrıca, biz sonunda bu model bir web hizmeti yayımladığınızda, başlıkları hizmetinin kullanıcı sütunlara tanımlamaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="40f19-128">Also, when we eventually publish this model in a web service, the headings help identify the columns to the user of the service.</span></span>  

<span data-ttu-id="40f19-129">Sütun başlıklarını kullanarak ekleyebiliriz [Düzenle meta veri] [ edit-metadata] modülü.</span><span class="sxs-lookup"><span data-stu-id="40f19-129">We can add column headings using the [Edit Metadata][edit-metadata] module.</span></span>
<span data-ttu-id="40f19-130">Kullandığınız [Düzenle meta veri] [ edit-metadata] modülü bir veri kümesi ile ilişkili meta verileri değiştirmek için.</span><span class="sxs-lookup"><span data-stu-id="40f19-130">You use the [Edit Metadata][edit-metadata] module to change metadata associated with a dataset.</span></span> <span data-ttu-id="40f19-131">Bu durumda, bu sütun başlıkları için daha fazla kolay adlar sağlamak için kullanırız.</span><span class="sxs-lookup"><span data-stu-id="40f19-131">In this case, we use it to provide more friendly names for column headings.</span></span> 

<span data-ttu-id="40f19-132">Kullanılacak [Düzenle meta veri][edit-metadata], (Bu durumda, bunların tümünün.) değiştirmek için hangi sütunların ilk belirtin Ardından, bu sütunları (sütun başlıklarını değiştirme bu durumda,.) üzerinde gerçekleştirilecek eylemi belirtin</span><span class="sxs-lookup"><span data-stu-id="40f19-132">To use [Edit Metadata][edit-metadata], you first specify which columns to modify (in this case, all of them.) Next, you specify the action to be performed on those columns (in this case, changing column headings.)</span></span>

1. <span data-ttu-id="40f19-133">Modül paletindeki "meta veri" yazın **arama** kutusu.</span><span class="sxs-lookup"><span data-stu-id="40f19-133">In the module palette, type "metadata" in the **Search** box.</span></span> <span data-ttu-id="40f19-134">[Düzenle meta veri] [ edit-metadata] modül listesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="40f19-134">The [Edit Metadata][edit-metadata] appears in the module list.</span></span>

2. <span data-ttu-id="40f19-135">' I tıklatın ve sürükleyin [Düzenle meta veri] [ edit-metadata] tuvale modülü ve daha önce eklediğimiz dataset bırakın.</span><span class="sxs-lookup"><span data-stu-id="40f19-135">Click and drag the [Edit Metadata][edit-metadata] module onto the canvas and drop it below the dataset we added earlier.</span></span>

3. <span data-ttu-id="40f19-136">Veri kümesine Bağlan [Düzenle meta veri][edit-metadata]: (küçük daire alt kümesi) kümesinin çıkış bağlantı noktasına tıklayın, giriş bağlantı noktasına sürükleyin [Düzenle meta veri] [ edit-metadata] (modül üstündeki küçük daire) fare düğmesini bırakın.</span><span class="sxs-lookup"><span data-stu-id="40f19-136">Connect the dataset to the [Edit Metadata][edit-metadata]: click the output port of the dataset (the small circle at the bottom of the dataset), drag to the input port of [Edit Metadata][edit-metadata] (the small circle at the top of the module), then release the mouse button.</span></span> <span data-ttu-id="40f19-137">Ya da tuval üzerinde hareket ettirin olsa bile veri kümesi ve modül bağlı kalır.</span><span class="sxs-lookup"><span data-stu-id="40f19-137">The dataset and module remain connected even if you move either around on the canvas.</span></span>
   
   <span data-ttu-id="40f19-138">Denemeyi bu gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="40f19-138">The experiment should now look something like this:</span></span>  
   
   ![Düzen meta verileri ekleme][1]
   
   <span data-ttu-id="40f19-140">Kırmızı bir ünlem işareti Biz bu modül için özellikler henüz ayarlamadıysanız olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="40f19-140">The red exclamation mark indicates that we haven't set the properties for this module yet.</span></span> <span data-ttu-id="40f19-141">Biz bu sonraki gerçekleştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40f19-141">We'll do that next.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="40f19-142">Modüle çift tıklayıp metin girerek bir modüle yorum ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40f19-142">You can add a comment to a module by double-clicking the module and entering text.</span></span> <span data-ttu-id="40f19-143">Bu, modülün denemenizde ne işe yaradığını bir bakışta görmenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="40f19-143">This can help you see at a glance what the module is doing in your experiment.</span></span> <span data-ttu-id="40f19-144">Bu durumda, çift [Düzenle meta veri] [ edit-metadata] modülü ve Açıklama "Ekle sütun başlıkları" türü.</span><span class="sxs-lookup"><span data-stu-id="40f19-144">In this case, double-click the [Edit Metadata][edit-metadata] module and type the comment "Add column headings".</span></span> <span data-ttu-id="40f19-145">Metin kutusunu kapatmak için tuval üzerinde başka bir yerde'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="40f19-145">Click anywhere else on the canvas to close the text box.</span></span> <span data-ttu-id="40f19-146">Açıklamayı görüntülemek için modülü aşağı oka tıklayın.</span><span class="sxs-lookup"><span data-stu-id="40f19-146">To display the comment, click the down-arrow on the module.</span></span>
   > 
   > ![Meta veriler modülü açıklama eklendi Düzenle][8]
   > 
4. <span data-ttu-id="40f19-148">Seçin [Düzenle meta veri][edit-metadata]hem de **özellikleri** tuvalin sağındaki bölmesi **başlatma Sütun seçiciyi**.</span><span class="sxs-lookup"><span data-stu-id="40f19-148">Select [Edit Metadata][edit-metadata], and in the **Properties** pane to the right of the canvas, click **Launch column selector**.</span></span>

5. <span data-ttu-id="40f19-149">İçinde **seçin sütunları** iletişim kutusunda, tüm satırları seçin **kullanılabilir sütunlar** tıklatıp > taşımak için **seçili sütun**.</span><span class="sxs-lookup"><span data-stu-id="40f19-149">In the **Select columns** dialog, select all the rows in **Available Columns** and click > to move them to **Selected Columns**.</span></span>
   <span data-ttu-id="40f19-150">İletişim kutusu aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="40f19-150">The dialog should look like this:</span></span>

   ![Seçili tüm sütunlarla Sütun Seçici][2]

6. <span data-ttu-id="40f19-152">Tıklatın **Tamam** onay işareti.</span><span class="sxs-lookup"><span data-stu-id="40f19-152">Click the **OK** check mark.</span></span>

7. <span data-ttu-id="40f19-153">Geri **özellikleri** bölmesinde, Ara **yeni sütun adları** parametresi.</span><span class="sxs-lookup"><span data-stu-id="40f19-153">Back in the **Properties** pane, look for the **New column names** parameter.</span></span> <span data-ttu-id="40f19-154">Bu alanda virgülle ve sütun sırasını ayrılmış kümesindeki 21 sütunların adlarının bir listesini girin.</span><span class="sxs-lookup"><span data-stu-id="40f19-154">In this field, enter a list of names for the 21 columns in the dataset, separated by commas and in column order.</span></span> <span data-ttu-id="40f19-155">Veri kümesi belgelerindeki UCI Web sitesinde sütun adları elde edebilirsiniz veya kolaylık sağlamak için kopyalama ve yapıştırma aşağıdaki listede:</span><span class="sxs-lookup"><span data-stu-id="40f19-155">You can obtain the columns names from the dataset documentation on the UCI website, or for convenience you can copy and paste the following list:</span></span>  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   <span data-ttu-id="40f19-156">Özellikler bölmesinde şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="40f19-156">The Properties pane looks like this:</span></span>
   
   ![Özellikleri düzenleme meta veriler için][3]

> [!TIP]
> <span data-ttu-id="40f19-158">Sütun başlıklarını doğrulamak istiyorsanız, denemeyi çalıştırın (tıklatın **çalıştırmak** deneme tuvalinin altında).</span><span class="sxs-lookup"><span data-stu-id="40f19-158">If you want to verify the column headings, run the experiment (click **RUN** below the experiment canvas).</span></span> <span data-ttu-id="40f19-159">Çalışan bittiğinde (yeşil bir onay işareti görünür [Düzenle meta veri][edit-metadata]), çıkış bağlantı noktasına tıklayın [Düzenle meta veri] [ edit-metadata] modülü ve select **Görselleştir**.</span><span class="sxs-lookup"><span data-stu-id="40f19-159">When it finishes running (a green check mark appears on [Edit Metadata][edit-metadata]), click the output port of the [Edit Metadata][edit-metadata] module, and select **Visualize**.</span></span> <span data-ttu-id="40f19-160">Denemeyi verilerine ilerlemesini görüntülemek için aynı şekilde herhangi bir modül çıktısını görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="40f19-160">You can view the output of any module in the same way to view the progress of the data through the experiment.</span></span>
> 
> 

## <a name="create-training-and-test-datasets"></a><span data-ttu-id="40f19-161">Eğitim oluşturmak ve veri kümelerini test etme</span><span class="sxs-lookup"><span data-stu-id="40f19-161">Create training and test datasets</span></span>
<span data-ttu-id="40f19-162">Modeli eğitmek için bazı veriler ve bazı test etmek için ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="40f19-162">We need some data to train the model and some to test it.</span></span>
<span data-ttu-id="40f19-163">Denemeyi sonraki adımda size dataset iki ayrı kümelerine bölünmüş şekilde: modelimizi ve test için bir tane eğitim için bir tane.</span><span class="sxs-lookup"><span data-stu-id="40f19-163">So in the next step of the experiment, we split the dataset into two separate datasets: one for training our model and one for testing it.</span></span>

<span data-ttu-id="40f19-164">Bunu yapmak için kullanırız [bölünmüş veri] [ split] modülü.</span><span class="sxs-lookup"><span data-stu-id="40f19-164">To do this, we use the [Split Data][split] module.</span></span>  

1. <span data-ttu-id="40f19-165">Bul [bölünmüş veri] [ split] modülünü tuvale sürükleyin ve buna bağlanmak [Düzenle meta veri] [ edit-metadata] modülü.</span><span class="sxs-lookup"><span data-stu-id="40f19-165">Find the [Split Data][split] module, drag it onto the canvas, and connect it to the [Edit Metadata][edit-metadata] module.</span></span>

2. <span data-ttu-id="40f19-166">Varsayılan olarak, 0,5 bölünmüş orandır ve **Randomized bölünmüş** parametrenin ayarlanmış.</span><span class="sxs-lookup"><span data-stu-id="40f19-166">By default, the split ratio is 0.5 and the **Randomized split** parameter is set.</span></span> <span data-ttu-id="40f19-167">Bu rastgele yarı veri çıkışı bir bağlantı noktası üzerinden olduğu anlamına gelir [bölünmüş veri] [ split] modülü ve yarısı diğer aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="40f19-167">This means that a random half of the data is output through one port of the [Split Data][split] module, and half through the other.</span></span> <span data-ttu-id="40f19-168">Bu parametreleri ayarlayabilirsiniz yanı sıra **rastgele doldurma** eğitim ve test verileri arasında bölünmüş değiştirmek için parametre.</span><span class="sxs-lookup"><span data-stu-id="40f19-168">You can adjust these parameters, as well as the **Random seed** parameter, to change the split between training and testing data.</span></span> <span data-ttu-id="40f19-169">Bu örnekte, biz bunları olarak bırakın-değil.</span><span class="sxs-lookup"><span data-stu-id="40f19-169">For this example, we leave them as-is.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="40f19-170">Özellik **ilk çıkış veri kümesinde satır kesir** çıkışı üzerinden verilerin ne kadar olacağını belirler *sol* çıkış bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="40f19-170">The property **Fraction of rows in the first output dataset** determines how much of the data is output through the *left* output port.</span></span> <span data-ttu-id="40f19-171">İçin 0,7 oranını ayarlamak, örneği için % 70 ' veri çıkış sol bağlantı noktası üzerinden ve doğru bağlantı noktası üzerinden % 30 olur.</span><span class="sxs-lookup"><span data-stu-id="40f19-171">For instance, if you set the ratio to 0.7, then 70% of the data is output through the left port and 30% through the right port.</span></span>  
   > 
   > 

3. <span data-ttu-id="40f19-172">Çift [bölünmüş veri] [ split] modülü ve açıklama girin, "eğitim ve test veri Böl % 50".</span><span class="sxs-lookup"><span data-stu-id="40f19-172">Double-click the [Split Data][split] module and enter the comment, "Training/testing data split 50%".</span></span> 

<span data-ttu-id="40f19-173">Çıkışları kullanırız [bölünmüş veri] [ split] modülü ancak biz gibi çalışır, ancak şimdi eğitim verilerini ve sağa çıktı olarak test verilerini sol çıkış kullanacak şekilde seçin.</span><span class="sxs-lookup"><span data-stu-id="40f19-173">We can use the outputs of the [Split Data][split] module however we like, but let's choose to use the left output as training data and the right output as testing data.</span></span>  

<span data-ttu-id="40f19-174">Bölümünde belirtildiği gibi [önceki adımı](machine-learning-walkthrough-2-upload-data.md), düşük olarak yüksek kredi riski misclassifying maliyetidir beş kez yüksek olarak düşük kredi riski misclassifying maliyeti daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="40f19-174">As mentioned in the [previous step](machine-learning-walkthrough-2-upload-data.md), the cost of misclassifying a high credit risk as low is five times higher than the cost of misclassifying a low credit risk as high.</span></span> <span data-ttu-id="40f19-175">Bu hesap için Biz bu maliyet işlevi yansıtır yeni bir veri kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="40f19-175">To account for this, we generate a new dataset that reflects this cost function.</span></span> <span data-ttu-id="40f19-176">Yeni veri kümesi her düşük riskli örnek çoğaltılmaz sırasında beş kez her yüksek riskli örnek çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="40f19-176">In the new dataset, each high risk example is replicated five times, while each low risk example is not replicated.</span></span>   

<span data-ttu-id="40f19-177">Bu çoğaltma yapabiliriz R kodu kullanarak:</span><span class="sxs-lookup"><span data-stu-id="40f19-177">We can do this replication using R code:</span></span>  

1. <span data-ttu-id="40f19-178">Bulma ve sürükleyin [R betiği yürütün] [ execute-r-script] deneme tuvale modülü.</span><span class="sxs-lookup"><span data-stu-id="40f19-178">Find and drag the [Execute R Script][execute-r-script] module onto the experiment canvas.</span></span> 

2. <span data-ttu-id="40f19-179">Sol çıkış bağlantı noktasına bağlanmak [bölünmüş veri] [ split] ilk giriş bağlantı noktasını ("Dataset1") modülüne [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="40f19-179">Connect the left output port of the [Split Data][split] module to the first input port ("Dataset1") of the [Execute R Script][execute-r-script] module.</span></span>

3. <span data-ttu-id="40f19-180">Çift [R betiği yürütün] [ execute-r-script] modülü ve açıklamayı girin "maliyet ayarlaması Ayarla".</span><span class="sxs-lookup"><span data-stu-id="40f19-180">Double-click the [Execute R Script][execute-r-script] module and enter the comment, "Set cost adjustment".</span></span>

4. <span data-ttu-id="40f19-181">İçinde **özellikleri** bölmesinde, varsayılan metinde silme **R betiği** parametre ve bu komut dosyasını girin:</span><span class="sxs-lookup"><span data-stu-id="40f19-181">In the **Properties** pane, delete the default text in the **R Script** parameter and enter this script:</span></span>
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![R betiği R betiği yürütün Modülü][9]

<span data-ttu-id="40f19-183">Bu aynı her çıktısını çoğaltma işlemi yapmak ihtiyacımız [bölünmüş veri] [ split] modülü böylece eğitim ve test verileri aynı maliyet ayarlama.</span><span class="sxs-lookup"><span data-stu-id="40f19-183">We need to do this same replication operation for each output of the [Split Data][split] module so that the training and testing data have the same cost adjustment.</span></span> <span data-ttu-id="40f19-184">Bunu yapmanın en kolay çoğaltarak yoludur [R betiği yürütün] [ execute-r-script] biz yalnızca yapılan modülü ve diğer bağlanma çıkış bağlantı noktasına [bölünmüş veri] [ split] modülü.</span><span class="sxs-lookup"><span data-stu-id="40f19-184">The easiest way to do this is by duplicating the [Execute R Script][execute-r-script] module we just made and connecting it to the other output port of the [Split Data][split] module.</span></span>

1. <span data-ttu-id="40f19-185">Sağ [R betiği yürütün] [ execute-r-script] modülü ve select **kopya**.</span><span class="sxs-lookup"><span data-stu-id="40f19-185">Right-click the [Execute R Script][execute-r-script] module and select **Copy**.</span></span>

2. <span data-ttu-id="40f19-186">Deneme tuvalinin sağ tıklatıp **Yapıştır**.</span><span class="sxs-lookup"><span data-stu-id="40f19-186">Right-click the experiment canvas and select **Paste**.</span></span>

3. <span data-ttu-id="40f19-187">Yeni modül yerine sürükleyin ve doğru çıkış bağlantı noktasına bağlayın [bölünmüş veri] [ split] ilk giriş bağlantı noktası için bu yeni modül [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="40f19-187">Drag the new module into position, and then connect the right output port of the [Split Data][split] module to the first input port of this new [Execute R Script][execute-r-script] module.</span></span> 

4. <span data-ttu-id="40f19-188">Tuvalin altındaki tıklatın **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="40f19-188">At the bottom of the canvas, click **Run**.</span></span> 

> [!TIP]
> <span data-ttu-id="40f19-189">R betiği yürütün modülü kopyasını özgün modül olarak aynı komut dosyasını içerir.</span><span class="sxs-lookup"><span data-stu-id="40f19-189">The copy of the Execute R Script module contains the same script as the original module.</span></span> <span data-ttu-id="40f19-190">Tuvalde bir modül kopyalayıp, kopya özgün tüm özelliklerini korur.</span><span class="sxs-lookup"><span data-stu-id="40f19-190">When you copy and paste a module on the canvas, the copy retains all the properties of the original.</span></span>  
> 
> 

<span data-ttu-id="40f19-191">Bizim denemeyi şimdi şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="40f19-191">Our experiment now looks something like this:</span></span>

![Bölünmüş modülü ve R betiklerini ekleme][4]

<span data-ttu-id="40f19-193">Denemelerinizi içinde R betiklerini kullanma hakkında daha fazla bilgi için bkz: [denemenizi R ile genişletme](machine-learning-extend-your-experiment-with-r.md).</span><span class="sxs-lookup"><span data-stu-id="40f19-193">For more information on using R scripts in your experiments, see [Extend your experiment with R](machine-learning-extend-your-experiment-with-r.md).</span></span>

<span data-ttu-id="40f19-194">**Sonraki: [eğitimi ve modelleri değerlendir](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span><span class="sxs-lookup"><span data-stu-id="40f19-194">**Next: [Train and evaluate the models](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span></span>

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
