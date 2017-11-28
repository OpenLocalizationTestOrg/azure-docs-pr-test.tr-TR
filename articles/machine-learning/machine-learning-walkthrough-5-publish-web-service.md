---
title: "5. adım: Machine Learning web hizmetini dağıtma | Microsoft Docs"
description: "5. adımını geliştirme Tahmine dayalı bir çözüm izlenecek yol: Tahmine dayalı bir denemeyi Machine Learning Studio'da bir web hizmeti olarak dağıtın."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 3fca74a3-c44b-4583-a218-c14c46ee5338
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: cec1bcceea158a20742c7019a266dcefaac4c9cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-5-deploy-the-azure-machine-learning-web-service"></a><span data-ttu-id="10c55-103">Kılavuz Adımı 5: Azure Machine Learning web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="10c55-103">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>
<span data-ttu-id="10c55-104">Bu izlenecek yol beşinci adımdır [Azure Machine learning'de Tahmine dayalı analiz çözümü geliştirme](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="10c55-104">This is the fifth step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="10c55-105">Bir Machine Learning çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="10c55-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="10c55-106">Mevcut verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="10c55-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="10c55-107">Yeni bir deneme oluşturma</span><span class="sxs-lookup"><span data-stu-id="10c55-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="10c55-108">Modelleri eğitme ve değerlendirme</span><span class="sxs-lookup"><span data-stu-id="10c55-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. <span data-ttu-id="10c55-109">**Web hizmetini dağıtma**</span><span class="sxs-lookup"><span data-stu-id="10c55-109">**Deploy the web service**</span></span>
6. [<span data-ttu-id="10c55-110">Web hizmetine erişme</span><span class="sxs-lookup"><span data-stu-id="10c55-110">Access the web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="10c55-111">Başkalarının Biz bu kılavuzda geliştirdik Tahmine dayalı bir model kullanma olanağı vermek için biz bunu Azure üzerinde bir web hizmeti olarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10c55-111">To give others a chance to use the predictive model we've developed in this walkthrough, we can deploy it as a web service on Azure.</span></span>

<span data-ttu-id="10c55-112">Bu noktaya kadar biz modelimizi eğitim ile denemeler.</span><span class="sxs-lookup"><span data-stu-id="10c55-112">Up to this point we've been experimenting with training our model.</span></span> <span data-ttu-id="10c55-113">Ancak artık dağıtılmış hizmet eğitim yapacaksınız - bizim modelini temel alan kullanıcı girişi Puanlama tarafından yeni tahminleri oluşturmak için geçiyor.</span><span class="sxs-lookup"><span data-stu-id="10c55-113">But the deployed service is no longer going to do training - it's going to generate new predictions by scoring the user's input based on our model.</span></span> <span data-ttu-id="10c55-114">Bu deneme gelen dönüştürmek için bazı hazırlıklar yapmanız oluşturacağız şekilde bir ***eğitim*** için deneme bir ***Tahmine dayalı*** deneyin.</span><span class="sxs-lookup"><span data-stu-id="10c55-114">So we're going to do some preparation to convert this experiment from a ***training*** experiment to a ***predictive*** experiment.</span></span> 

<span data-ttu-id="10c55-115">Bu üç adımlık bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="10c55-115">This is a three-step process:</span></span>  

1. <span data-ttu-id="10c55-116">Modellerin kaldırın</span><span class="sxs-lookup"><span data-stu-id="10c55-116">Remove one of the models</span></span>
2. <span data-ttu-id="10c55-117">Dönüştürme *eğitim denemenizi* içine oluşturduk bir *tahmini deneme*</span><span class="sxs-lookup"><span data-stu-id="10c55-117">Convert the *training experiment* we've created into a *predictive experiment*</span></span>
3. <span data-ttu-id="10c55-118">Tahmine dayalı denemeye bir web hizmeti olarak dağıtma</span><span class="sxs-lookup"><span data-stu-id="10c55-118">Deploy the predictive experiment as a web service</span></span>

## <a name="remove-one-of-the-models"></a><span data-ttu-id="10c55-119">Modellerin kaldırın</span><span class="sxs-lookup"><span data-stu-id="10c55-119">Remove one of the models</span></span>

<span data-ttu-id="10c55-120">İlk olarak, biz bu deneme aşağı biraz kırpma gerekir.</span><span class="sxs-lookup"><span data-stu-id="10c55-120">First, we need to trim this experiment down a little.</span></span> <span data-ttu-id="10c55-121">Şu anda iki farklı modelleri denemesinde sahip olduğumuz ancak yalnızca bir model Biz bu web hizmeti olarak dağıtırken kullanılacak istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="10c55-121">We currently have two different models in the experiment, but we only want to use one model when we deploy this as a web service.</span></span>  

<span data-ttu-id="10c55-122">Biz boosted ağacı modeli SVM modeli daha iyi gerçekleştirilen karar varsayalım.</span><span class="sxs-lookup"><span data-stu-id="10c55-122">Let's say we've decided that the boosted tree model performed better than the SVM model.</span></span> <span data-ttu-id="10c55-123">Yapılacak ilk şey kaldırmak nedenle [iki sınıflı destek vektör makinesi] [ two-class-support-vector-machine] modülü ve eğitim için kullanılan modül.</span><span class="sxs-lookup"><span data-stu-id="10c55-123">So the first thing to do is remove the [Two-Class Support Vector Machine][two-class-support-vector-machine] module and the modules that were used for training it.</span></span> <span data-ttu-id="10c55-124">Bir denemeyi ilk tıklayarak kopyasını isteyebilirsiniz **Kaydet** deneme tuvalinin altındaki.</span><span class="sxs-lookup"><span data-stu-id="10c55-124">You may want to make a copy of the experiment first by clicking **Save As** at the bottom of the experiment canvas.</span></span>

<span data-ttu-id="10c55-125">Aşağıdaki modüller silmek ihtiyacımız var:</span><span class="sxs-lookup"><span data-stu-id="10c55-125">We need to delete the following modules:</span></span>  

* <span data-ttu-id="10c55-126">[İki sınıflı destekli vektör makinesi][two-class-support-vector-machine]</span><span class="sxs-lookup"><span data-stu-id="10c55-126">[Two-Class Support Vector Machine][two-class-support-vector-machine]</span></span>
* <span data-ttu-id="10c55-127">[Modeli eğitmek] [ train-model] ve [Score Model] [ score-model] ona bağlı modüller</span><span class="sxs-lookup"><span data-stu-id="10c55-127">[Train Model][train-model] and [Score Model][score-model] modules that were connected to it</span></span>
* <span data-ttu-id="10c55-128">[Veri normalleştirin] [ normalize-data] (her ikisi de)</span><span class="sxs-lookup"><span data-stu-id="10c55-128">[Normalize Data][normalize-data] (both of them)</span></span>
* <span data-ttu-id="10c55-129">[Modeli değerlendirin] [ evaluate-model] (biz modelleri değerlendirme tamamlanmış olduğundan)</span><span class="sxs-lookup"><span data-stu-id="10c55-129">[Evaluate Model][evaluate-model] (because we're finished evaluating the models)</span></span>

<span data-ttu-id="10c55-130">Her modülü seçin ve Delete tuşuna basın veya modülü sağ tıklatın ve seçin **silmek**.</span><span class="sxs-lookup"><span data-stu-id="10c55-130">Select each module and press the Delete key, or right-click the module and select **Delete**.</span></span> 

![SVM modeli kaldırıldı][3a]

<span data-ttu-id="10c55-132">Modelimizi bu gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="10c55-132">Our model should now look something like this:</span></span>

![SVM modeli kaldırıldı][3]

<span data-ttu-id="10c55-134">Bu modeli kullanarak dağıtmaya hazır değiliz artık [iki-Class Boosted karar ağacı][two-class-boosted-decision-tree].</span><span class="sxs-lookup"><span data-stu-id="10c55-134">Now we're ready to deploy this model using the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].</span></span>

## <a name="convert-the-training-experiment-to-a-predictive-experiment"></a><span data-ttu-id="10c55-135">Tahmine dayalı bir deneme eğitim denemenizi Dönüştür</span><span class="sxs-lookup"><span data-stu-id="10c55-135">Convert the training experiment to a predictive experiment</span></span>

<span data-ttu-id="10c55-136">Bu model dağıtım için hazır hale getirmek için Biz bu eğitim denemenizi Tahmine dayalı bir deneme dönüştürmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="10c55-136">To get this model ready for deployment, we need to convert this training experiment to a predictive experiment.</span></span> <span data-ttu-id="10c55-137">Bu üç adımdan oluşur:</span><span class="sxs-lookup"><span data-stu-id="10c55-137">This involves three steps:</span></span>

1. <span data-ttu-id="10c55-138">Modeli eğittiğimize ve bizim eğitim modüllerini Değiştir kaydedin</span><span class="sxs-lookup"><span data-stu-id="10c55-138">Save the model we've trained and then replace our training modules</span></span>
2. <span data-ttu-id="10c55-139">Eğitim için yalnızca gerekli olan modülleri kaldırmak için deneme kırpma</span><span class="sxs-lookup"><span data-stu-id="10c55-139">Trim the experiment to remove modules that were only needed for training</span></span>
3. <span data-ttu-id="10c55-140">Burada web hizmeti girişi kabul eder ve burada bir çıktı üretir tanımlayın</span><span class="sxs-lookup"><span data-stu-id="10c55-140">Define where the web service will accept input and where it generates the output</span></span>

<span data-ttu-id="10c55-141">El ile yapabileceğimiz ancak tıklayarak üç adımı Neyse gerçekleştirilebilir **Web hizmetinin ayarı** deneme tuvalinin altındaki (ve seçerek **Tahmine dayalı Web hizmeti** seçeneği).</span><span class="sxs-lookup"><span data-stu-id="10c55-141">We could do this manually, but fortunately all three steps can be accomplished by clicking **Set Up Web Service** at the bottom of the experiment canvas (and selecting the **Predictive Web Service** option).</span></span>

> [!TIP]
> <span data-ttu-id="10c55-142">Daha fazla bilgi isterseniz ne olur Tahmine dayalı bir deneme eğitim denemenizi dönüştürürken bkz [modelinizi Azure Machine Learning Studio'da dağıtımına hazırlamak nasıl](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="10c55-142">If you want more details on what happens when you convert a training experiment to a predictive experiment, see [How to prepare your model for deployment in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span></span>

<span data-ttu-id="10c55-143">Tıkladığınızda **Web hizmetinin ayarı**, olacaklar:</span><span class="sxs-lookup"><span data-stu-id="10c55-143">When you click **Set Up Web Service**, several things happen:</span></span>

* <span data-ttu-id="10c55-144">Tek bir eğitim modeli dönüştürülür **eğitilen Model** modülü ve deneme tuvaline solundaki modül paletindeki depolanan (altında bulabilirsiniz **eğitilmiş modeller**)</span><span class="sxs-lookup"><span data-stu-id="10c55-144">The trained model is converted to a single **Trained Model** module and stored in the module palette to the left of the experiment canvas (you can find it under **Trained Models**)</span></span>
* <span data-ttu-id="10c55-145">Eğitim için kullanılan modülleri kaldırılır; özellikle:</span><span class="sxs-lookup"><span data-stu-id="10c55-145">Modules that were used for training are removed; specifically:</span></span>
  * <span data-ttu-id="10c55-146">[İki sınıflı artırılmış karar ağacı][two-class-boosted-decision-tree]</span><span class="sxs-lookup"><span data-stu-id="10c55-146">[Two-Class Boosted Decision Tree][two-class-boosted-decision-tree]</span></span>
  * <span data-ttu-id="10c55-147">[Train Model][train-model]</span><span class="sxs-lookup"><span data-stu-id="10c55-147">[Train Model][train-model]</span></span>
  * <span data-ttu-id="10c55-148">[Veri bölme][split]</span><span class="sxs-lookup"><span data-stu-id="10c55-148">[Split Data][split]</span></span>
  * <span data-ttu-id="10c55-149">İkinci [R betiği yürütün] [ execute-r-script] test verileri için kullanılan Modülü</span><span class="sxs-lookup"><span data-stu-id="10c55-149">the second [Execute R Script][execute-r-script] module that was used for test data</span></span>
* <span data-ttu-id="10c55-150">Kaydedilen eğitilen model yeniden deneme eklenir</span><span class="sxs-lookup"><span data-stu-id="10c55-150">The saved trained model is added back into the experiment</span></span>
* <span data-ttu-id="10c55-151">**Web hizmeti girişi** ve **Web hizmeti çıkış** modülleri eklenir (Bu kullanıcının veri modeli burada girer ve web hizmeti erişildiğinde hangi verilerin döndürülen belirleme)</span><span class="sxs-lookup"><span data-stu-id="10c55-151">**Web service input** and **Web service output** modules are added (these identify where the user's data will enter the model, and what data is returned, when the web service is accessed)</span></span>

> [!NOTE]
> <span data-ttu-id="10c55-152">Deneme tuvalinin üstünde eklenen sekmeleri altında iki bölümden deneme kaydedilir görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10c55-152">You can see that the experiment is saved in two parts under tabs that have been added at the top of the experiment canvas.</span></span> <span data-ttu-id="10c55-153">Özgün eğitim denemenizi sekmesi altında olan **eğitim denemenizi**, ve yeni oluşturulan Tahmine dayalı denemeye altında **Tahmine dayalı denemeye**.</span><span class="sxs-lookup"><span data-stu-id="10c55-153">The original training experiment is under the tab **Training experiment**, and the newly created predictive experiment is under **Predictive experiment**.</span></span> <span data-ttu-id="10c55-154">Tahmine dayalı denemeye, biz web hizmeti olarak dağıtacaksınız adrestir.</span><span class="sxs-lookup"><span data-stu-id="10c55-154">The predictive experiment is the one we'll deploy as a web service.</span></span>

<span data-ttu-id="10c55-155">Biz bu belirli deneme ile ek bir adım gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="10c55-155">We need to take one additional step with this particular experiment.</span></span>
<span data-ttu-id="10c55-156">İki eklediğimiz [R betiği yürütün] [ execute-r-script] ağırlıklı işlevi veri sağlamak için modül.</span><span class="sxs-lookup"><span data-stu-id="10c55-156">We added two [Execute R Script][execute-r-script] modules to provide a weighting function to the data.</span></span> <span data-ttu-id="10c55-157">Bu modüller son modelindeki çıkışı olabilmesi için biz eğitim ve test için gerekli bir eli oluştu.</span><span class="sxs-lookup"><span data-stu-id="10c55-157">That was just a trick we needed for training and testing, so we can take out those modules in the final model.</span></span>
<span data-ttu-id="10c55-158">Machine Learning Studio kaldırılmış bir [R betiği yürütün] [ execute-r-script] onu kaldırıldığında Modülü [bölünmüş] [ split] modülü.</span><span class="sxs-lookup"><span data-stu-id="10c55-158">Machine Learning Studio removed one [Execute R Script][execute-r-script] module when it removed the [Split][split] module.</span></span> <span data-ttu-id="10c55-159">Biz diğer kaldırın ve connect artık [meta verileri Düzenleyicisi] [ metadata-editor] doğrudan [Score Model][score-model].</span><span class="sxs-lookup"><span data-stu-id="10c55-159">Now we can remove the other and connect [Metadata Editor][metadata-editor] directly to [Score Model][score-model].</span></span>    

<span data-ttu-id="10c55-160">Bizim deneme gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="10c55-160">Our experiment should now look like this:</span></span>  

![Eğitim modeli Puanlama][4]  

> [!NOTE]
> <span data-ttu-id="10c55-162">Biz Tahmine dayalı denemeye UCI Almanca kredi kartı veri kümesi neden sol merak ediyor olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10c55-162">You may be wondering why we left the UCI German Credit Card Data dataset in the predictive experiment.</span></span> <span data-ttu-id="10c55-163">Hizmet geçiyor kullanıcının verileri, özgün dataset puan, bu nedenle özgün veri kümesi modelde neden bırakın?</span><span class="sxs-lookup"><span data-stu-id="10c55-163">The service is going to score the user's data, not the original dataset, so why leave the original dataset in the model?</span></span>
> 
> <span data-ttu-id="10c55-164">Hizmet asıl kredi kartı veri gerekmez geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="10c55-164">It's true that the service doesn't need the original credit card data.</span></span> <span data-ttu-id="10c55-165">Ancak, şemayı vardır kaç sütunlar gibi bilgileri içerir ve hangi sütunların sayısal bu verileri, gerekir.</span><span class="sxs-lookup"><span data-stu-id="10c55-165">But it does need the schema for that data, which includes information such as how many columns there are and which columns are numeric.</span></span> <span data-ttu-id="10c55-166">Bu şema bilgileri, kullanıcının verileri yorumlamak gereklidir.</span><span class="sxs-lookup"><span data-stu-id="10c55-166">This schema information is necessary to interpret the user's data.</span></span> <span data-ttu-id="10c55-167">Biz bu bileşenlerin hizmet çalışırken Puanlama modülü dataset şeması sahip olması bağlı bırakın.</span><span class="sxs-lookup"><span data-stu-id="10c55-167">We leave these components connected so that the scoring module has the dataset schema when the service is running.</span></span> <span data-ttu-id="10c55-168">Veri kullanılmaz, yalnızca şema.</span><span class="sxs-lookup"><span data-stu-id="10c55-168">The data isn't used, just the schema.</span></span>  
> 
> 

<span data-ttu-id="10c55-169">Son bir kez denemeyi çalıştırın (tıklatın **çalıştırmak**.) Modelin hala çalıştığından emin olmak istiyorsanız, çıktısını tıklatın [Score Model] [ score-model] modülü ve Seç **sonuçları görüntüleme**.</span><span class="sxs-lookup"><span data-stu-id="10c55-169">Run the experiment one last time (click **Run**.) If you want to verify that the model is still working, click the output of the [Score Model][score-model] module and select **View Results**.</span></span> <span data-ttu-id="10c55-170">Özgün veriler, kredi riski değeri ("skoru etiketleri") ve puanlama olasılık değeri ("skoru olasılıklar".) ile birlikte görüntülendiğini görebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="10c55-170">You can see that the original data is displayed, along with the credit risk value ("Scored Labels") and the scoring probability value ("Scored Probabilities".)</span></span> 

## <a name="deploy-the-web-service"></a><span data-ttu-id="10c55-171">Web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="10c55-171">Deploy the web service</span></span>
<span data-ttu-id="10c55-172">Deneme ya da Klasik web hizmeti olarak ya da Azure Resource Manager tabanlı yeni bir web hizmeti olarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10c55-172">You can deploy the experiment as either a Classic web service, or as a New web service that's based on Azure Resource Manager.</span></span>

### <a name="deploy-as-a-classic-web-service"></a><span data-ttu-id="10c55-173">Klasik web hizmeti olarak dağıtma</span><span class="sxs-lookup"><span data-stu-id="10c55-173">Deploy as a Classic web service</span></span>
<span data-ttu-id="10c55-174">Bizim deneme türetilmiş bir Klasik web hizmeti dağıtmak için **Web hizmeti Dağıt** seçin ve tuvalin altındaki **Web hizmeti Dağıt [Klasik]**.</span><span class="sxs-lookup"><span data-stu-id="10c55-174">To deploy a Classic web service derived from our experiment, click **Deploy Web Service** below the canvas and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="10c55-175">Machine Learning Studio'da deneme bir web hizmeti olarak dağıtır ve bu web hizmeti panoya alır.</span><span class="sxs-lookup"><span data-stu-id="10c55-175">Machine Learning Studio deploys the experiment as a web service and takes you to the dashboard for that web service.</span></span> <span data-ttu-id="10c55-176">Bu sayfadan denemede döndürebilirsiniz (**görünüm anlık görüntü** veya **görüntülemek son**) ve basit bir sınama web hizmetinin çalıştırın (bkz **web hizmetini sınama** aşağıda).</span><span class="sxs-lookup"><span data-stu-id="10c55-176">From this page you can return to the experiment (**View snapshot** or **View latest**) and run a simple test of the web service (see **Test the web service** below).</span></span> <span data-ttu-id="10c55-177">(Daha ayrıntılı bu kılavuzun sonraki adımda) web hizmeti erişebileceği uygulamaları oluşturmak için buradaki bilgiler bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="10c55-177">There is also information here for creating applications that can access the web service (more on that in the next step of this walkthrough).</span></span>

![Web hizmeti Panosu][6]

<span data-ttu-id="10c55-179">Tıklatarak hizmeti yapılandırabilirsiniz **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="10c55-179">You can configure the service by clicking the **CONFIGURATION** tab.</span></span> <span data-ttu-id="10c55-180">(Bunu verilen deneme adını varsayılan olarak) hizmet adı burada değiştirebilirsiniz ve bir açıklama girin.</span><span class="sxs-lookup"><span data-stu-id="10c55-180">Here you can modify the service name (it's given the experiment name by default) and give it a description.</span></span> <span data-ttu-id="10c55-181">Daha fazla kolay etiketleri için girdi ve çıktı verilerini de verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10c55-181">You can also give more friendly labels for the input and output data.</span></span>  

![Web hizmetini yapılandır][5]  

### <a name="deploy-as-a-new-web-service"></a><span data-ttu-id="10c55-183">Yeni bir web hizmeti olarak dağıtma</span><span class="sxs-lookup"><span data-stu-id="10c55-183">Deploy as a New web service</span></span>

> [!NOTE] 
> <span data-ttu-id="10c55-184">Yeni bir web hizmeti dağıtmak için web hizmetini dağıtma abonelikte yeterli izniniz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="10c55-184">To deploy a New web service you must have sufficient permissions in the subscription to which you are deploying the web service.</span></span> <span data-ttu-id="10c55-185">Daha fazla bilgi için bkz: [Azure Machine Learning Web Hizmetleri Portalı'nı kullanarak bir web hizmetini yönetmek](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="10c55-185">For more information, see [Manage a web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="10c55-186">Yeni bir web hizmeti dağıtmak için bizim deneme türetilen:</span><span class="sxs-lookup"><span data-stu-id="10c55-186">To deploy a New web service derived from our experiment:</span></span>

1. <span data-ttu-id="10c55-187">Tıklatın **Web hizmeti Dağıt** seçin ve tuvalin altındaki **Web hizmeti dağıtma [Yeni]**.</span><span class="sxs-lookup"><span data-stu-id="10c55-187">Click **Deploy Web Service** below the canvas and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="10c55-188">Machine Learning Studio aktarır, Azure Machine Learning web hizmetleri için **dağıtmak deneme** sayfası.</span><span class="sxs-lookup"><span data-stu-id="10c55-188">Machine Learning Studio transfers you to the Azure Machine Learning web services **Deploy Experiment** page.</span></span>

2. <span data-ttu-id="10c55-189">Web hizmeti için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="10c55-189">Enter a name for the web service.</span></span> 

3. <span data-ttu-id="10c55-190">İçin **fiyat planı**, var olan bir fiyatlandırma planı seçebilir ya da "Yeni Oluştur" seçeneğini belirleyin ve yeni plan bir ad verin ve aylık plan seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="10c55-190">For **Price Plan**, you can select an existing pricing plan, or select "Create new" and give the new plan a name and select the monthly plan option.</span></span> <span data-ttu-id="10c55-191">Varsayılan bölgeniz ve web hizmetiniz için planlara planı katmanları varsayılan bu bölgeye dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="10c55-191">The plan tiers default to the plans for your default region and your web service is deployed to that region.</span></span>

4. <span data-ttu-id="10c55-192">Tıklatın **dağıtmak**.</span><span class="sxs-lookup"><span data-stu-id="10c55-192">Click **Deploy**.</span></span>

<span data-ttu-id="10c55-193">Birkaç dakika sonra **Hızlı Başlangıç** web hizmetiniz için sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="10c55-193">After a few minutes, the **Quickstart** page for your web service opens.</span></span>

<span data-ttu-id="10c55-194">Tıklatarak hizmeti yapılandırabilirsiniz **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="10c55-194">You can configure the service by clicking the **Configure** tab.</span></span> <span data-ttu-id="10c55-195">Hizmet burada değiştirebilirsiniz başlığı ve bir açıklama girin.</span><span class="sxs-lookup"><span data-stu-id="10c55-195">Here you can modify the service title and give it a description.</span></span> 

<span data-ttu-id="10c55-196">Web hizmeti sınamak için **Test** sekmesinde (bkz **web hizmetini sınama** aşağıda).</span><span class="sxs-lookup"><span data-stu-id="10c55-196">To test the web service, click the **Test** tab (see **Test the web service** below).</span></span> <span data-ttu-id="10c55-197">Web hizmeti erişebileceği uygulamaları oluşturma hakkında daha fazla bilgi için tıklatın **Tüket** sekmesinde (Bu kılavuzda bir sonraki adım, daha fazla ayrıntıya çıkar).</span><span class="sxs-lookup"><span data-stu-id="10c55-197">For information on creating applications that can access the web service, click the **Consume** tab (the next step in this walkthrough will go into more detail).</span></span>

> [!TIP]
> <span data-ttu-id="10c55-198">Bunu dağıttıktan sonra web hizmeti güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10c55-198">You can update the web service after you've deployed it.</span></span> <span data-ttu-id="10c55-199">Örneğin, eğitim denemenizi düzenleyin ve sonra da, modelinizde değiştirmek istiyorsanız, model parametreleri ince ayar ve tıklatın **Web hizmeti Dağıt**, seçme **Web hizmeti Dağıt [Klasik]** veya **[Yeni] Web hizmetini dağıtma**.</span><span class="sxs-lookup"><span data-stu-id="10c55-199">For example, if you want to change your model, then you can edit the training experiment, tweak the model parameters, and click **Deploy Web Service**, selecting **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span> <span data-ttu-id="10c55-200">Denemeyi yeniden dağıttığınızda, artık güncelleştirilmiş model kullanarak web hizmeti değiştirir.</span><span class="sxs-lookup"><span data-stu-id="10c55-200">When you deploy the experiment again, it replaces the web service, now using your updated model.</span></span>  
> 
> 

## <a name="test-the-web-service"></a><span data-ttu-id="10c55-201">Web hizmetini sınama</span><span class="sxs-lookup"><span data-stu-id="10c55-201">Test the web service</span></span>

<span data-ttu-id="10c55-202">Web hizmeti erişildiğinde aracılığıyla kullanıcının verileri girer **Web hizmeti girişi** burada da iletilir Modülü [Score Model] [ score-model] modülü ve skoru.</span><span class="sxs-lookup"><span data-stu-id="10c55-202">When the web service is accessed, the user's data enters through the **Web service input** module where it's passed to the [Score Model][score-model] module and scored.</span></span> <span data-ttu-id="10c55-203">Tahmine dayalı denemeye ayarlarız şekilde, özgün kredi riski dataset aynı biçimde veri modeli bekliyor.</span><span class="sxs-lookup"><span data-stu-id="10c55-203">The way we've set up the predictive experiment, the model expects data in the same format as the original credit risk dataset.</span></span>
<span data-ttu-id="10c55-204">Web hizmetinden döndürülen sonuçları kullanıcıya **Web hizmeti çıkış** modülü.</span><span class="sxs-lookup"><span data-stu-id="10c55-204">The results are returned to the user from the web service through the **Web service output** module.</span></span>

> [!TIP]
> <span data-ttu-id="10c55-205">Tüm yapılandırılmış, Tahmine dayalı denemeye sahibiz şekilde oluşur [Score Model] [ score-model] modülü döndürülür.</span><span class="sxs-lookup"><span data-stu-id="10c55-205">The way we have the predictive experiment configured, the entire results from the [Score Model][score-model] module are returned.</span></span> <span data-ttu-id="10c55-206">Bu, tüm giriş verilerini artı kredi riski değeri ve puanlama olasılık içerir.</span><span class="sxs-lookup"><span data-stu-id="10c55-206">This includes all the input data plus the credit risk value and the scoring probability.</span></span> <span data-ttu-id="10c55-207">Ancak isterseniz, farklı bir şey dönebilirsiniz - Örneğin, yalnızca kredi riski değer döndürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10c55-207">But you can return something different if you want - for example, you could return just the credit risk value.</span></span> <span data-ttu-id="10c55-208">Bunu yapmak için INSERT bir [proje sütunları] [ project-columns] modülü arasında [Score Model] [ score-model] ve **Web hizmeti çıkış**sütunları ortadan kaldırmak için geri dönmek için web hizmeti istemediğiniz.</span><span class="sxs-lookup"><span data-stu-id="10c55-208">To do this, insert a [Project Columns][project-columns] module between [Score Model][score-model] and the **Web service output** to eliminate columns you don't want the web service to return.</span></span> 
> 
> 

<span data-ttu-id="10c55-209">Klasik web test edebilirsiniz ya da hizmet **Machine Learning Studio** veya **Azure Machine Learning Web Hizmetleri** portal.</span><span class="sxs-lookup"><span data-stu-id="10c55-209">You can test a Classic web service either in **Machine Learning Studio** or in the **Azure Machine Learning Web Services** portal.</span></span>
<span data-ttu-id="10c55-210">Yeni bir web testi yalnızca hizmet **Machine Learning Web Hizmetleri** portal.</span><span class="sxs-lookup"><span data-stu-id="10c55-210">You can test a New web service only in the **Machine Learning Web Services** portal.</span></span>

> [!TIP]
> <span data-ttu-id="10c55-211">Azure Machine Learning Web Hizmetleri Portalı'nda test edilirken istek-yanıt hizmeti test etmek için kullanabileceğiniz örnek veri oluşturma portal olabilir.</span><span class="sxs-lookup"><span data-stu-id="10c55-211">When testing in the Azure Machine Learning Web Services portal, you can have the portal create sample data that you can use to test the Request-Response service.</span></span> <span data-ttu-id="10c55-212">Üzerinde **yapılandırma** sayfasında, için "Evet" seçeneğini **örnek veriler etkin?**.</span><span class="sxs-lookup"><span data-stu-id="10c55-212">On the **Configure** page, select "Yes" for **Sample Data Enabled?**.</span></span> <span data-ttu-id="10c55-213">Üzerinde istek-yanıt sekmesini açtığınızda **Test** sayfasında, portal özgün kredi riski kümesinden alınan örnek verileri doldurur.</span><span class="sxs-lookup"><span data-stu-id="10c55-213">When you open the Request-Response tab on the **Test** page, the portal fills in sample data taken from the original credit risk dataset.</span></span>

### <a name="test-a-classic-web-service"></a><span data-ttu-id="10c55-214">Klasik web hizmetini sınama</span><span class="sxs-lookup"><span data-stu-id="10c55-214">Test a Classic web service</span></span>

<span data-ttu-id="10c55-215">Machine Learning Studio'da veya Machine Learning Web Hizmetleri portalında bir Klasik web hizmeti test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10c55-215">You can test a Classic web service in Machine Learning Studio or in the Machine Learning Web Services portal.</span></span> 

#### <a name="test-in-machine-learning-studio"></a><span data-ttu-id="10c55-216">Machine Learning Studio'da test</span><span class="sxs-lookup"><span data-stu-id="10c55-216">Test in Machine Learning Studio</span></span>

1. <span data-ttu-id="10c55-217">Üzerinde **PANO** sayfasında web hizmeti için **Test** altında düğmesini **varsayılan uç nokta**.</span><span class="sxs-lookup"><span data-stu-id="10c55-217">On the **DASHBOARD** page for the web service, click the **Test** button under **Default Endpoint**.</span></span> <span data-ttu-id="10c55-218">Bir iletişim kutusu açılır ve hizmet için bir giriş verisi sorar.</span><span class="sxs-lookup"><span data-stu-id="10c55-218">A dialog pops up and asks you for the input data for the service.</span></span> <span data-ttu-id="10c55-219">Özgün kredi riski kümesinde görünen aynı sütunlara bunlar.</span><span class="sxs-lookup"><span data-stu-id="10c55-219">These are the same columns that appeared in the original credit risk dataset.</span></span>  

2. <span data-ttu-id="10c55-220">Bir veri kümesi girin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="10c55-220">Enter a set of data and then click **OK**.</span></span> 

#### <a name="test-in-the-machine-learning-web-services-portal"></a><span data-ttu-id="10c55-221">Machine Learning Web Hizmetleri Portalı'nda test</span><span class="sxs-lookup"><span data-stu-id="10c55-221">Test in the Machine Learning Web Services portal</span></span>

1. <span data-ttu-id="10c55-222">Üzerinde **PANO** sayfasında web hizmeti için **Test Önizleme** altında bağlantı **varsayılan uç nokta**.</span><span class="sxs-lookup"><span data-stu-id="10c55-222">On the **DASHBOARD** page for the web service, click the **Test preview** link under **Default Endpoint**.</span></span> <span data-ttu-id="10c55-223">Web hizmeti uç noktası için Azure Machine Learning Web Hizmetleri portalında test sayfası açılır ve hizmet için bir giriş verisi sorar.</span><span class="sxs-lookup"><span data-stu-id="10c55-223">The test page in the Azure Machine Learning Web Services portal for the web service endpoint opens and asks you for the input data for the service.</span></span> <span data-ttu-id="10c55-224">Özgün kredi riski kümesinde görünen aynı sütunlara bunlar.</span><span class="sxs-lookup"><span data-stu-id="10c55-224">These are the same columns that appeared in the original credit risk dataset.</span></span>

2. <span data-ttu-id="10c55-225">Tıklatın **Test istek-yanıt**.</span><span class="sxs-lookup"><span data-stu-id="10c55-225">Click **Test Request-Response**.</span></span> 

### <a name="test-a-new-web-service"></a><span data-ttu-id="10c55-226">Yeni bir web hizmeti test etme</span><span class="sxs-lookup"><span data-stu-id="10c55-226">Test a New web service</span></span>

<span data-ttu-id="10c55-227">Yalnızca Machine Learning Web Hizmetleri portalında yeni bir web hizmeti test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10c55-227">You can test a New web service only in the Machine Learning Web Services portal.</span></span>

1. <span data-ttu-id="10c55-228">İçinde [Azure Machine Learning Web Hizmetleri](https://services.azureml.net/quickstart) portal tıklatın **Test** sayfanın üst kısmındaki.</span><span class="sxs-lookup"><span data-stu-id="10c55-228">In the [Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal, click **Test** at the top of the page.</span></span> <span data-ttu-id="10c55-229">**Test** sayfası açılır ve veri hizmeti için girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10c55-229">The **Test** page opens and you can input data for the service.</span></span> <span data-ttu-id="10c55-230">Görüntülenen giriş alanları, özgün kredi riski kümesinde görünen sütunlara karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="10c55-230">The input fields displayed correspond to the columns that appeared in the original credit risk dataset.</span></span> 

2. <span data-ttu-id="10c55-231">Bir veri kümesi girin ve ardından **Test istek-yanıt**.</span><span class="sxs-lookup"><span data-stu-id="10c55-231">Enter a set of data and then click **Test Request-Response**.</span></span>

<span data-ttu-id="10c55-232">Test sonuçlarını çıkış sütununda sayfasının sağ tarafında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="10c55-232">The results of the test are displayed on the right-hand side of the page in the output column.</span></span> 


## <a name="manage-the-web-service"></a><span data-ttu-id="10c55-233">Web hizmeti yönetme</span><span class="sxs-lookup"><span data-stu-id="10c55-233">Manage the web service</span></span>

### <a name="manage-a-classic-web-service-in-the-azure-classic-portal"></a><span data-ttu-id="10c55-234">Klasik Azure portalında bir Klasik web hizmeti yönetme</span><span class="sxs-lookup"><span data-stu-id="10c55-234">Manage a Classic web service in the Azure classic portal</span></span>

<span data-ttu-id="10c55-235">Klasik web hizmeti dağıttıktan sonra sonra buradan yönetebilirsiniz [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="10c55-235">Once you've deployed your Classic web service, you can manage it from the [Azure classic portal](https://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="10c55-236">Oturum [Klasik Azure portalı](https://manage.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="10c55-236">Sign in to the [Azure classic portal](https://manage.windowsazure.com)</span></span>
2. <span data-ttu-id="10c55-237">Microsoft Azure Hizmetleri panelinde tıklatın **MACHINE LEARNING**</span><span class="sxs-lookup"><span data-stu-id="10c55-237">In the Microsoft Azure services panel, click **MACHINE LEARNING**</span></span>
3. <span data-ttu-id="10c55-238">Çalışma alanınızı tıklatın</span><span class="sxs-lookup"><span data-stu-id="10c55-238">Click your workspace</span></span>
4. <span data-ttu-id="10c55-239">Tıklatın **Web Hizmetleri** sekmesi</span><span class="sxs-lookup"><span data-stu-id="10c55-239">Click the **Web services** tab</span></span>
5. <span data-ttu-id="10c55-240">Oluşturduğumuz web hizmeti</span><span class="sxs-lookup"><span data-stu-id="10c55-240">Click the web service we created</span></span>
6. <span data-ttu-id="10c55-241">"Varsayılan" uç noktasına tıklayın</span><span class="sxs-lookup"><span data-stu-id="10c55-241">Click the "default" endpoint</span></span>

<span data-ttu-id="10c55-242">Buradan, web hizmetinin nasıl çalıştığını izlemek gibi işlemler yapabilir ve değiştirerek eşzamanlı olarak kaç hizmeti çağrıları yapma performansı tweaks işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="10c55-242">From here, you can do things like monitor how the web service is doing and make performance tweaks by changing how many concurrent calls the service can handle.</span></span>

<span data-ttu-id="10c55-243">Daha ayrıntılı bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="10c55-243">For more details, see:</span></span>

* [<span data-ttu-id="10c55-244">Uç noktaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="10c55-244">Creating Endpoints</span></span>](machine-learning-create-endpoint.md)
* [<span data-ttu-id="10c55-245">Web hizmeti ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="10c55-245">Scaling web service</span></span>](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-the-azure-machine-learning-web-services-portal"></a><span data-ttu-id="10c55-246">Klasik ya da Azure Machine Learning Web Hizmetleri portalında yeni bir web hizmeti yönetme</span><span class="sxs-lookup"><span data-stu-id="10c55-246">Manage a Classic or New web service in the Azure Machine Learning Web Services portal</span></span>

<span data-ttu-id="10c55-247">Klasik ya da yeni web hizmetinizi dağıttıktan sonra sonra buradan yönetebilirsiniz [Microsoft Azure Machine Learning Web Hizmetleri](https://services.azureml.net/quickstart) portal.</span><span class="sxs-lookup"><span data-stu-id="10c55-247">Once you've deployed your web service, whether Classic or New, you can manage it from the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal.</span></span>

<span data-ttu-id="10c55-248">Web hizmetinizin performansını izlemek için:</span><span class="sxs-lookup"><span data-stu-id="10c55-248">To monitor the performance of your web service:</span></span>

1. <span data-ttu-id="10c55-249">Oturum [Microsoft Azure Machine Learning Web Hizmetleri](https://services.azureml.net/quickstart) portalı</span><span class="sxs-lookup"><span data-stu-id="10c55-249">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal</span></span>
2. <span data-ttu-id="10c55-250">Tıklatın **Web Hizmetleri**</span><span class="sxs-lookup"><span data-stu-id="10c55-250">Click **Web services**</span></span>
3. <span data-ttu-id="10c55-251">Web hizmeti</span><span class="sxs-lookup"><span data-stu-id="10c55-251">Click your web service</span></span>
4. <span data-ttu-id="10c55-252">Tıklatın **Panosu**</span><span class="sxs-lookup"><span data-stu-id="10c55-252">Click the **Dashboard**</span></span>

- - -
<span data-ttu-id="10c55-253">**Sonraki: [web hizmetine erişim](machine-learning-walkthrough-6-access-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="10c55-253">**Next: [Access the web service](machine-learning-walkthrough-6-access-web-service.md)**</span></span>

[3]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3.png
[3a]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3a.png
[4]: ./media/machine-learning-walkthrough-5-publish-web-service/publish4.png
[5]: ./media/machine-learning-walkthrough-5-publish-web-service/publish5.png
[6]: ./media/machine-learning-walkthrough-5-publish-web-service/publish6.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[metadata-editor]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[project-columns]: https://msdn.microsoft.com/en-us/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
