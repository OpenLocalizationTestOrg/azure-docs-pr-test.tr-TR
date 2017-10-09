---
title: "5. adım: hello Machine Learning web hizmetini dağıtma | Microsoft Docs"
description: "5. adımını hello geliştirmek Tahmine dayalı bir çözüm izlenecek yol: Tahmine dayalı bir denemeyi Machine Learning Studio'da bir web hizmeti olarak dağıtın."
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
ms.openlocfilehash: 76391010972ed1450bbda8bfb2352c7b22b51ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-5-deploy-hello-azure-machine-learning-web-service"></a><span data-ttu-id="1e722-103">Gözden geçirme adım 5: hello Azure Machine Learning web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="1e722-103">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>
<span data-ttu-id="1e722-104">Merhaba kılavuzun hello beşinci adım budur [Azure Machine learning'de Tahmine dayalı analiz çözümü geliştirme](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="1e722-104">This is hello fifth step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="1e722-105">Bir Machine Learning çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1e722-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="1e722-106">Mevcut verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="1e722-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="1e722-107">Yeni bir deneme oluşturma</span><span class="sxs-lookup"><span data-stu-id="1e722-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="1e722-108">Eğitmek ve hello modelleri değerlendir</span><span class="sxs-lookup"><span data-stu-id="1e722-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. <span data-ttu-id="1e722-109">**Merhaba web hizmetini dağıtma**</span><span class="sxs-lookup"><span data-stu-id="1e722-109">**Deploy hello web service**</span></span>
6. [<span data-ttu-id="1e722-110">Erişim hello web hizmeti</span><span class="sxs-lookup"><span data-stu-id="1e722-110">Access hello web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="1e722-111">toogive başka bir fırsat toouse hello Biz bu kılavuzda geliştirilen Tahmine dayalı bir model, biz bunu Azure üzerinde bir web hizmeti olarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e722-111">toogive others a chance toouse hello predictive model we've developed in this walkthrough, we can deploy it as a web service on Azure.</span></span>

<span data-ttu-id="1e722-112">Toothis noktası biz modelimizi eğitim ile denemeler.</span><span class="sxs-lookup"><span data-stu-id="1e722-112">Up toothis point we've been experimenting with training our model.</span></span> <span data-ttu-id="1e722-113">Ancak dağıtılan hello hizmeti artık toodo eğitim geçiyor - toogenerate yeni tahminleri bizim modelini temel alan hello kullanıcının giriş Puanlama tarafından gittiği.</span><span class="sxs-lookup"><span data-stu-id="1e722-113">But hello deployed service is no longer going toodo training - it's going toogenerate new predictions by scoring hello user's input based on our model.</span></span> <span data-ttu-id="1e722-114">Toodo yapacağız şekilde bazı hazırlık tooconvert bu deneme gelen bir ***eğitim*** tooa denemeler ***Tahmine dayalı*** deneyin.</span><span class="sxs-lookup"><span data-stu-id="1e722-114">So we're going toodo some preparation tooconvert this experiment from a ***training*** experiment tooa ***predictive*** experiment.</span></span> 

<span data-ttu-id="1e722-115">Bu üç adımlık bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="1e722-115">This is a three-step process:</span></span>  

1. <span data-ttu-id="1e722-116">Merhaba modelleri kaldırın</span><span class="sxs-lookup"><span data-stu-id="1e722-116">Remove one of hello models</span></span>
2. <span data-ttu-id="1e722-117">Merhaba Dönüştür *eğitim denemenizi* içine oluşturduk bir *tahmini deneme*</span><span class="sxs-lookup"><span data-stu-id="1e722-117">Convert hello *training experiment* we've created into a *predictive experiment*</span></span>
3. <span data-ttu-id="1e722-118">Bir web hizmeti olarak Hello tahmini deneme dağıtma</span><span class="sxs-lookup"><span data-stu-id="1e722-118">Deploy hello predictive experiment as a web service</span></span>

## <a name="remove-one-of-hello-models"></a><span data-ttu-id="1e722-119">Merhaba modelleri kaldırın</span><span class="sxs-lookup"><span data-stu-id="1e722-119">Remove one of hello models</span></span>

<span data-ttu-id="1e722-120">İlk olarak, tootrim bu deneme aşağı biraz ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="1e722-120">First, we need tootrim this experiment down a little.</span></span> <span data-ttu-id="1e722-121">Şu anda iki farklı modelleri hello denemesinde sahip olduğumuz ancak Biz bu web hizmeti olarak dağıttığınızda yalnızca toouse bir model istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="1e722-121">We currently have two different models in hello experiment, but we only want toouse one model when we deploy this as a web service.</span></span>  

<span data-ttu-id="1e722-122">Biz bu boosted hello ağacı modeli hello SVM modeli daha iyi gerçekleştirilen karar varsayalım.</span><span class="sxs-lookup"><span data-stu-id="1e722-122">Let's say we've decided that hello boosted tree model performed better than hello SVM model.</span></span> <span data-ttu-id="1e722-123">Merhaba ilk şey toodo Kaldır hello olacak şekilde [iki sınıflı destek vektör makinesi] [ two-class-support-vector-machine] modülü ve eğitim için kullanılan hello modüller.</span><span class="sxs-lookup"><span data-stu-id="1e722-123">So hello first thing toodo is remove hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module and hello modules that were used for training it.</span></span> <span data-ttu-id="1e722-124">Tıklayarak toomake hello deneme kopyasını ilk isteyebilirsiniz **Kaydet** tuvale hello hello sonunda deneme.</span><span class="sxs-lookup"><span data-stu-id="1e722-124">You may want toomake a copy of hello experiment first by clicking **Save As** at hello bottom of hello experiment canvas.</span></span>

<span data-ttu-id="1e722-125">Modüller aşağıdaki toodelete hello ihtiyacımız var:</span><span class="sxs-lookup"><span data-stu-id="1e722-125">We need toodelete hello following modules:</span></span>  

* <span data-ttu-id="1e722-126">[İki sınıflı destekli vektör makinesi][two-class-support-vector-machine]</span><span class="sxs-lookup"><span data-stu-id="1e722-126">[Two-Class Support Vector Machine][two-class-support-vector-machine]</span></span>
* <span data-ttu-id="1e722-127">[Modeli eğitmek] [ train-model] ve [Score Model] [ score-model] bağlı tooit olan modülleri</span><span class="sxs-lookup"><span data-stu-id="1e722-127">[Train Model][train-model] and [Score Model][score-model] modules that were connected tooit</span></span>
* <span data-ttu-id="1e722-128">[Veri normalleştirin] [ normalize-data] (her ikisi de)</span><span class="sxs-lookup"><span data-stu-id="1e722-128">[Normalize Data][normalize-data] (both of them)</span></span>
* <span data-ttu-id="1e722-129">[Modeli değerlendirin] [ evaluate-model] (biz hello modelleri değerlendirme tamamlanmış olduğundan)</span><span class="sxs-lookup"><span data-stu-id="1e722-129">[Evaluate Model][evaluate-model] (because we're finished evaluating hello models)</span></span>

<span data-ttu-id="1e722-130">Her modül ve hello Delete anahtar ya da sağ tıklatma hello modülü basın seçip **silmek**.</span><span class="sxs-lookup"><span data-stu-id="1e722-130">Select each module and press hello Delete key, or right-click hello module and select **Delete**.</span></span> 

![Merhaba SVM modeli kaldırıldı][3a]

<span data-ttu-id="1e722-132">Modelimizi bu gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="1e722-132">Our model should now look something like this:</span></span>

![Merhaba SVM modeli kaldırıldı][3]

<span data-ttu-id="1e722-134">Hazır toodeploy ki artık bu model hello kullanarak [iki-Class Boosted karar ağacı][two-class-boosted-decision-tree].</span><span class="sxs-lookup"><span data-stu-id="1e722-134">Now we're ready toodeploy this model using hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].</span></span>

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a><span data-ttu-id="1e722-135">Merhaba eğitim deneme tooa Tahmine dayalı denemeye Dönüştür</span><span class="sxs-lookup"><span data-stu-id="1e722-135">Convert hello training experiment tooa predictive experiment</span></span>

<span data-ttu-id="1e722-136">tooget Bu model hazır dağıtımı için tooconvert deneme tooa Tahmine dayalı denemeye eğitim gerekli.</span><span class="sxs-lookup"><span data-stu-id="1e722-136">tooget this model ready for deployment, we need tooconvert this training experiment tooa predictive experiment.</span></span> <span data-ttu-id="1e722-137">Bu üç adımdan oluşur:</span><span class="sxs-lookup"><span data-stu-id="1e722-137">This involves three steps:</span></span>

1. <span data-ttu-id="1e722-138">Merhaba modeli eğittiğimize ve bizim eğitim modüllerini Değiştir kaydedin</span><span class="sxs-lookup"><span data-stu-id="1e722-138">Save hello model we've trained and then replace our training modules</span></span>
2. <span data-ttu-id="1e722-139">Eğitim için yalnızca gerekli olan hello deneme tooremove modülleri kırpma</span><span class="sxs-lookup"><span data-stu-id="1e722-139">Trim hello experiment tooremove modules that were only needed for training</span></span>
3. <span data-ttu-id="1e722-140">Burada hello web hizmeti girişi kabul eder ve burada hello çıktı üretir tanımlayın</span><span class="sxs-lookup"><span data-stu-id="1e722-140">Define where hello web service will accept input and where it generates hello output</span></span>

<span data-ttu-id="1e722-141">El ile yapabileceğimiz ancak tıklayarak üç adımı Neyse gerçekleştirilebilir **Web hizmetinin ayarı** hello deneme tuvalinin hello sonundaki (Merhaba seçerek **Tahmine dayalı Web hizmeti** seçenek).</span><span class="sxs-lookup"><span data-stu-id="1e722-141">We could do this manually, but fortunately all three steps can be accomplished by clicking **Set Up Web Service** at hello bottom of hello experiment canvas (and selecting hello **Predictive Web Service** option).</span></span>

> [!TIP]
> <span data-ttu-id="1e722-142">Daha fazla bilgi isterseniz Tahmine dayalı bir eğitim deneme tooa Dönüştür ne olur denemeler bkz [nasıl tooprepare modelinizi Azure Machine Learning Studio'daki dağıtımı için](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="1e722-142">If you want more details on what happens when you convert a training experiment tooa predictive experiment, see [How tooprepare your model for deployment in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span></span>

<span data-ttu-id="1e722-143">Tıkladığınızda **Web hizmetinin ayarı**, olacaklar:</span><span class="sxs-lookup"><span data-stu-id="1e722-143">When you click **Set Up Web Service**, several things happen:</span></span>

* <span data-ttu-id="1e722-144">Merhaba eğitilen model olan tek dönüştürülmüş tooa **eğitilen Model** modülü ve hello modül paleti toohello içinde depolanan hello solundaki deneme tuvaline (altında bulabilirsiniz **eğitilmiş modeller**)</span><span class="sxs-lookup"><span data-stu-id="1e722-144">hello trained model is converted tooa single **Trained Model** module and stored in hello module palette toohello left of hello experiment canvas (you can find it under **Trained Models**)</span></span>
* <span data-ttu-id="1e722-145">Eğitim için kullanılan modülleri kaldırılır; özellikle:</span><span class="sxs-lookup"><span data-stu-id="1e722-145">Modules that were used for training are removed; specifically:</span></span>
  * <span data-ttu-id="1e722-146">[İki sınıflı artırılmış karar ağacı][two-class-boosted-decision-tree]</span><span class="sxs-lookup"><span data-stu-id="1e722-146">[Two-Class Boosted Decision Tree][two-class-boosted-decision-tree]</span></span>
  * <span data-ttu-id="1e722-147">[Train Model][train-model]</span><span class="sxs-lookup"><span data-stu-id="1e722-147">[Train Model][train-model]</span></span>
  * <span data-ttu-id="1e722-148">[Veri bölme][split]</span><span class="sxs-lookup"><span data-stu-id="1e722-148">[Split Data][split]</span></span>
  * <span data-ttu-id="1e722-149">Merhaba ikinci [R betiği yürütün] [ execute-r-script] test verileri için kullanılan Modülü</span><span class="sxs-lookup"><span data-stu-id="1e722-149">hello second [Execute R Script][execute-r-script] module that was used for test data</span></span>
* <span data-ttu-id="1e722-150">kaydedilen hello eğitilen model geri hello deneme eklenir</span><span class="sxs-lookup"><span data-stu-id="1e722-150">hello saved trained model is added back into hello experiment</span></span>
* <span data-ttu-id="1e722-151">**Web hizmeti girişi** ve **Web hizmeti çıkış** modülleri eklenir (bunlar hello kullanıcının verileri hello model burada girer ve hello web hizmeti erişildiğinde hangi verilerin döndürülen belirleme)</span><span class="sxs-lookup"><span data-stu-id="1e722-151">**Web service input** and **Web service output** modules are added (these identify where hello user's data will enter hello model, and what data is returned, when hello web service is accessed)</span></span>

> [!NOTE]
> <span data-ttu-id="1e722-152">Merhaba deneme hello deneme tuvalinin hello üstünde eklenen sekmeleri altında iki bölümden kaydedilir görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e722-152">You can see that hello experiment is saved in two parts under tabs that have been added at hello top of hello experiment canvas.</span></span> <span data-ttu-id="1e722-153">Merhaba özgün eğitim denemenizi olduğu hello sekmesi altında **eğitim denemenizi**, ve yeni oluşturulan Tahmine dayalı denemeye hello altında **Tahmine dayalı denemeye**.</span><span class="sxs-lookup"><span data-stu-id="1e722-153">hello original training experiment is under hello tab **Training experiment**, and hello newly created predictive experiment is under **Predictive experiment**.</span></span> <span data-ttu-id="1e722-154">Merhaba Tahmine dayalı denemeye hello bir web hizmeti olarak dağıtma ' dir.</span><span class="sxs-lookup"><span data-stu-id="1e722-154">hello predictive experiment is hello one we'll deploy as a web service.</span></span>

<span data-ttu-id="1e722-155">Bir ek adım belirli bu deneme tootake ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="1e722-155">We need tootake one additional step with this particular experiment.</span></span>
<span data-ttu-id="1e722-156">İki eklediğimiz [R betiği yürütün] [ execute-r-script] modülleri tooprovide ağırlığı toohello veri işlev.</span><span class="sxs-lookup"><span data-stu-id="1e722-156">We added two [Execute R Script][execute-r-script] modules tooprovide a weighting function toohello data.</span></span> <span data-ttu-id="1e722-157">Bu modüller hello son modelinde çıkışı olabilmesi için biz eğitim ve test için gerekli bir eli oluştu.</span><span class="sxs-lookup"><span data-stu-id="1e722-157">That was just a trick we needed for training and testing, so we can take out those modules in hello final model.</span></span>
<span data-ttu-id="1e722-158">Machine Learning Studio kaldırılmış bir [R betiği yürütün] [ execute-r-script] hello kaldırıldığında Modülü [bölünmüş] [ split] modülü.</span><span class="sxs-lookup"><span data-stu-id="1e722-158">Machine Learning Studio removed one [Execute R Script][execute-r-script] module when it removed hello [Split][split] module.</span></span> <span data-ttu-id="1e722-159">Biz kaldırabilirsiniz artık diğer hello ve bağlanın [meta verileri Düzenleyicisi] [ metadata-editor] doğrudan çok[Score Model][score-model].</span><span class="sxs-lookup"><span data-stu-id="1e722-159">Now we can remove hello other and connect [Metadata Editor][metadata-editor] directly too[Score Model][score-model].</span></span>    

<span data-ttu-id="1e722-160">Bizim deneme gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="1e722-160">Our experiment should now look like this:</span></span>  

![Merhaba, eğitilen modeli Puanlama][4]  

> [!NOTE]
> <span data-ttu-id="1e722-162">Biz hello Tahmine dayalı denemesinde hello UCI Almanca kredi kartı verileri dataset neden sol merak ediyor olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e722-162">You may be wondering why we left hello UCI German Credit Card Data dataset in hello predictive experiment.</span></span> <span data-ttu-id="1e722-163">Merhaba hizmet tooscore hello kullanıcının verileri, değil hello özgün veri kümesi, bu nedenle neden hello özgün dataset hello modelinde bırakın geçiyor?</span><span class="sxs-lookup"><span data-stu-id="1e722-163">hello service is going tooscore hello user's data, not hello original dataset, so why leave hello original dataset in hello model?</span></span>
> 
> <span data-ttu-id="1e722-164">Hello hizmet özgün kredi kartı verileri hello olmayan geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1e722-164">It's true that hello service doesn't need hello original credit card data.</span></span> <span data-ttu-id="1e722-165">Ancak, hello şeması vardır kaç sütunlar gibi bilgileri içerir ve hangi sütunların sayısal bu verileri, gerekir.</span><span class="sxs-lookup"><span data-stu-id="1e722-165">But it does need hello schema for that data, which includes information such as how many columns there are and which columns are numeric.</span></span> <span data-ttu-id="1e722-166">Bu şema bilgileri gerekli toointerpret hello kullanıcının verilerdir.</span><span class="sxs-lookup"><span data-stu-id="1e722-166">This schema information is necessary toointerpret hello user's data.</span></span> <span data-ttu-id="1e722-167">Biz bu bileşenlerin Merhaba hizmeti çalışırken hello Puanlama modülü hello dataset şeması sahip olması bağlı bırakın.</span><span class="sxs-lookup"><span data-stu-id="1e722-167">We leave these components connected so that hello scoring module has hello dataset schema when hello service is running.</span></span> <span data-ttu-id="1e722-168">Merhaba veri değil kullanıldığında, yalnızca hello şema.</span><span class="sxs-lookup"><span data-stu-id="1e722-168">hello data isn't used, just hello schema.</span></span>  
> 
> 

<span data-ttu-id="1e722-169">Merhaba denemeyi son bir kez çalıştırın (tıklatın **çalıştırmak**.) Model hello tooverify çalışmaya devam isterseniz, hello hello çıktısını tıklatın [Score Model] [ score-model] modülü ve select **sonuçları görüntüleme**.</span><span class="sxs-lookup"><span data-stu-id="1e722-169">Run hello experiment one last time (click **Run**.) If you want tooverify that hello model is still working, click hello output of hello [Score Model][score-model] module and select **View Results**.</span></span> <span data-ttu-id="1e722-170">Merhaba özgün veriler, hello kredi riski değeri ("skoru etiketleri") ve olasılık değeri ("skoru olasılıklar".) Puanlama hello birlikte görüntülendiğini görebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1e722-170">You can see that hello original data is displayed, along with hello credit risk value ("Scored Labels") and hello scoring probability value ("Scored Probabilities".)</span></span> 

## <a name="deploy-hello-web-service"></a><span data-ttu-id="1e722-171">Merhaba web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="1e722-171">Deploy hello web service</span></span>
<span data-ttu-id="1e722-172">Merhaba deneme ya da Klasik web hizmeti olarak ya da Azure Resource Manager tabanlı yeni bir web hizmeti olarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e722-172">You can deploy hello experiment as either a Classic web service, or as a New web service that's based on Azure Resource Manager.</span></span>

### <a name="deploy-as-a-classic-web-service"></a><span data-ttu-id="1e722-173">Klasik web hizmeti olarak dağıtma</span><span class="sxs-lookup"><span data-stu-id="1e722-173">Deploy as a Classic web service</span></span>
<span data-ttu-id="1e722-174">Klasik web hizmeti bizim deneme türetilen toodeploy tıklatın **Web hizmeti Dağıt** hello tuvale ve seçin **Web hizmeti Dağıt [Klasik]**.</span><span class="sxs-lookup"><span data-stu-id="1e722-174">toodeploy a Classic web service derived from our experiment, click **Deploy Web Service** below hello canvas and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="1e722-175">Machine Learning Studio'da bir web hizmeti olarak hello deneme dağıtır ve toohello Pano, web hizmeti alır.</span><span class="sxs-lookup"><span data-stu-id="1e722-175">Machine Learning Studio deploys hello experiment as a web service and takes you toohello dashboard for that web service.</span></span> <span data-ttu-id="1e722-176">Bu sayfadan toohello deneme döndürebilirsiniz (**görünüm anlık görüntü** veya **görüntülemek son**) ve basit bir sınama hello web hizmetinin çalıştırın (bkz **Test hello web hizmeti** aşağıda).</span><span class="sxs-lookup"><span data-stu-id="1e722-176">From this page you can return toohello experiment (**View snapshot** or **View latest**) and run a simple test of hello web service (see **Test hello web service** below).</span></span> <span data-ttu-id="1e722-177">Merhaba web hizmetine (daha ayrıntılı hello sonraki adımda bu kılavuzun) erişebilirsiniz uygulamaları oluşturmak için buradaki bilgiler bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1e722-177">There is also information here for creating applications that can access hello web service (more on that in hello next step of this walkthrough).</span></span>

![Web hizmeti Panosu][6]

<span data-ttu-id="1e722-179">Merhaba tıklatarak hello hizmet yapılandırabilirsiniz **yapılandırma** sekmesi. Burada hello hizmet adını (verilen hello deneme adını varsayılan olarak değil) değiştirebilirsiniz ve bir açıklama girin.</span><span class="sxs-lookup"><span data-stu-id="1e722-179">You can configure hello service by clicking hello **CONFIGURATION** tab. Here you can modify hello service name (it's given hello experiment name by default) and give it a description.</span></span> <span data-ttu-id="1e722-180">Daha fazla kolay etiketleri Merhaba verebilirsiniz girdi ve çıktı verilerini.</span><span class="sxs-lookup"><span data-stu-id="1e722-180">You can also give more friendly labels for hello input and output data.</span></span>  

![Merhaba web hizmetini yapılandır][5]  

### <a name="deploy-as-a-new-web-service"></a><span data-ttu-id="1e722-182">Yeni bir web hizmeti olarak dağıtma</span><span class="sxs-lookup"><span data-stu-id="1e722-182">Deploy as a New web service</span></span>

> [!NOTE] 
> <span data-ttu-id="1e722-183">toodeploy hello abonelik toowhich dağıttığınız yeterli izinlere sahip yeni bir web hizmetini web hizmeti hello.</span><span class="sxs-lookup"><span data-stu-id="1e722-183">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you are deploying hello web service.</span></span> <span data-ttu-id="1e722-184">Daha fazla bilgi için bkz: [hello Azure Machine Learning Web Hizmetleri portalı kullanarak bir web hizmeti yönetmek](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="1e722-184">For more information, see [Manage a web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="1e722-185">Yeni bir web hizmeti toodeploy bizim deneme türetilmiş:</span><span class="sxs-lookup"><span data-stu-id="1e722-185">toodeploy a New web service derived from our experiment:</span></span>

1. <span data-ttu-id="1e722-186">Tıklatın **Web hizmeti Dağıt** hello tuvale ve seçin **Web hizmeti dağıtma [Yeni]**.</span><span class="sxs-lookup"><span data-stu-id="1e722-186">Click **Deploy Web Service** below hello canvas and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="1e722-187">Machine Learning Studio toohello Azure Machine Learning web hizmetleri aktarır **dağıtmak deneme** sayfası.</span><span class="sxs-lookup"><span data-stu-id="1e722-187">Machine Learning Studio transfers you toohello Azure Machine Learning web services **Deploy Experiment** page.</span></span>

2. <span data-ttu-id="1e722-188">Merhaba web hizmeti için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="1e722-188">Enter a name for hello web service.</span></span> 

3. <span data-ttu-id="1e722-189">İçin **fiyat planı**, var olan bir fiyatlandırma planı seçin veya Seç "Yeni Oluştur" ve verin hello yeni bir ad ve select hello aylık plan seçeneği planlayın.</span><span class="sxs-lookup"><span data-stu-id="1e722-189">For **Price Plan**, you can select an existing pricing plan, or select "Create new" and give hello new plan a name and select hello monthly plan option.</span></span> <span data-ttu-id="1e722-190">Katmanları toohello planları varsayılan bölgeniz ve web hizmetiniz için varsayılan hello planı dağıtılan toothat bölgedir.</span><span class="sxs-lookup"><span data-stu-id="1e722-190">hello plan tiers default toohello plans for your default region and your web service is deployed toothat region.</span></span>

4. <span data-ttu-id="1e722-191">Tıklatın **dağıtmak**.</span><span class="sxs-lookup"><span data-stu-id="1e722-191">Click **Deploy**.</span></span>

<span data-ttu-id="1e722-192">Birkaç dakika sonra hello **Hızlı Başlangıç** web hizmetiniz için sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="1e722-192">After a few minutes, hello **Quickstart** page for your web service opens.</span></span>

<span data-ttu-id="1e722-193">Merhaba tıklatarak hello hizmet yapılandırabilirsiniz **yapılandırma** sekmesi. Burada hello hizmet değiştirebilirsiniz başlığı ve bir açıklama girin.</span><span class="sxs-lookup"><span data-stu-id="1e722-193">You can configure hello service by clicking hello **Configure** tab. Here you can modify hello service title and give it a description.</span></span> 

<span data-ttu-id="1e722-194">tootest hello web hizmeti, hello tıklatın **Test** sekmesini (bkz **Test hello web hizmeti** aşağıda).</span><span class="sxs-lookup"><span data-stu-id="1e722-194">tootest hello web service, click hello **Test** tab (see **Test hello web service** below).</span></span> <span data-ttu-id="1e722-195">Merhaba hello web hizmeti erişebileceği uygulamaları oluşturma hakkında daha fazla bilgi için tıklatın **Tüket** sekmesinde (Merhaba sonraki adım bu kılavuzda daha fazla ayrıntıya çıkar).</span><span class="sxs-lookup"><span data-stu-id="1e722-195">For information on creating applications that can access hello web service, click hello **Consume** tab (hello next step in this walkthrough will go into more detail).</span></span>

> [!TIP]
> <span data-ttu-id="1e722-196">Dağıttıktan sonra sonra hello web hizmeti güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e722-196">You can update hello web service after you've deployed it.</span></span> <span data-ttu-id="1e722-197">Örneğin, modelinizi toochange istiyorsanız, ardından hello eğitim denemenizi düzenleyebilir, hello modeli parametreleri ince ayar ve tıklatın **Web hizmeti Dağıt**, seçme **Web hizmeti Dağıt [Klasik]** veya  **[Yeni] Web hizmetini dağıtma**.</span><span class="sxs-lookup"><span data-stu-id="1e722-197">For example, if you want toochange your model, then you can edit hello training experiment, tweak hello model parameters, and click **Deploy Web Service**, selecting **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span> <span data-ttu-id="1e722-198">Merhaba deneme yeniden dağıttığınızda, artık güncelleştirilmiş model kullanarak hello web hizmeti değiştirir.</span><span class="sxs-lookup"><span data-stu-id="1e722-198">When you deploy hello experiment again, it replaces hello web service, now using your updated model.</span></span>  
> 
> 

## <a name="test-hello-web-service"></a><span data-ttu-id="1e722-199">Test hello web hizmeti</span><span class="sxs-lookup"><span data-stu-id="1e722-199">Test hello web service</span></span>

<span data-ttu-id="1e722-200">Merhaba web hizmeti erişildiğinde hello kullanıcının verileri hello girer **Web hizmeti girişi** burada da geçtikten toohello Modülü [Score Model] [ score-model] modülü ve skoru.</span><span class="sxs-lookup"><span data-stu-id="1e722-200">When hello web service is accessed, hello user's data enters through hello **Web service input** module where it's passed toohello [Score Model][score-model] module and scored.</span></span> <span data-ttu-id="1e722-201">Merhaba şekilde, biz hello Tahmine dayalı denemeye ayarladınız hello modeli aynı hello özgün kredi riski veri kümesi biçimi hello içinde veri bekliyor.</span><span class="sxs-lookup"><span data-stu-id="1e722-201">hello way we've set up hello predictive experiment, hello model expects data in hello same format as hello original credit risk dataset.</span></span>
<span data-ttu-id="1e722-202">Merhaba aracılığıyla hello web hizmetinden, toohello kullanıcı Hello sonuçlarının döndürüldüğü **Web hizmeti çıkış** modülü.</span><span class="sxs-lookup"><span data-stu-id="1e722-202">hello results are returned toohello user from hello web service through hello **Web service output** module.</span></span>

> [!TIP]
> <span data-ttu-id="1e722-203">Merhaba şekilde yapılandırılmış, hello Tahmine dayalı denemeye hello tüm sahibiz hello sonuçları [Score Model] [ score-model] modülü döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1e722-203">hello way we have hello predictive experiment configured, hello entire results from hello [Score Model][score-model] module are returned.</span></span> <span data-ttu-id="1e722-204">Bu, tüm hello giriş verisi artı hello kredi riski değeri ve olasılık Puanlama hello içerir.</span><span class="sxs-lookup"><span data-stu-id="1e722-204">This includes all hello input data plus hello credit risk value and hello scoring probability.</span></span> <span data-ttu-id="1e722-205">Ancak isterseniz, farklı bir şey dönebilirsiniz - Örneğin, yalnızca hello kredi riski değer döndürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e722-205">But you can return something different if you want - for example, you could return just hello credit risk value.</span></span> <span data-ttu-id="1e722-206">toodo Bu, INSERT bir [proje sütunları] [ project-columns] modülü arasında [Score Model] [ score-model] ve hello **Web hizmeti çıkış** istemediğiniz tooeliminate sütunları hello web hizmeti tooreturn.</span><span class="sxs-lookup"><span data-stu-id="1e722-206">toodo this, insert a [Project Columns][project-columns] module between [Score Model][score-model] and hello **Web service output** tooeliminate columns you don't want hello web service tooreturn.</span></span> 
> 
> 

<span data-ttu-id="1e722-207">Klasik web test edebilirsiniz ya da hizmet **Machine Learning Studio** veya hello **Azure Machine Learning Web Hizmetleri** portal.</span><span class="sxs-lookup"><span data-stu-id="1e722-207">You can test a Classic web service either in **Machine Learning Studio** or in hello **Azure Machine Learning Web Services** portal.</span></span>
<span data-ttu-id="1e722-208">Yeni bir web hizmeti yalnızca hello test **Machine Learning Web Hizmetleri** portal.</span><span class="sxs-lookup"><span data-stu-id="1e722-208">You can test a New web service only in hello **Machine Learning Web Services** portal.</span></span>

> [!TIP]
> <span data-ttu-id="1e722-209">Hello Azure Machine Learning Web Hizmetleri Portalı'nda test edilirken tootest hello istek-yanıt hizmeti kullanabileceğiniz örnek veri oluşturma hello portal olabilir.</span><span class="sxs-lookup"><span data-stu-id="1e722-209">When testing in hello Azure Machine Learning Web Services portal, you can have hello portal create sample data that you can use tootest hello Request-Response service.</span></span> <span data-ttu-id="1e722-210">Merhaba üzerinde **yapılandırma** sayfasında, için "Evet" seçeneğini **örnek veriler etkin?**.</span><span class="sxs-lookup"><span data-stu-id="1e722-210">On hello **Configure** page, select "Yes" for **Sample Data Enabled?**.</span></span> <span data-ttu-id="1e722-211">Merhaba hello istek-yanıt sekmesinde açtığınızda **Test** sayfasında hello portal hello özgün kredi riski veri kümesinden alınan örnek verileri doldurur.</span><span class="sxs-lookup"><span data-stu-id="1e722-211">When you open hello Request-Response tab on hello **Test** page, hello portal fills in sample data taken from hello original credit risk dataset.</span></span>

### <a name="test-a-classic-web-service"></a><span data-ttu-id="1e722-212">Klasik web hizmetini sınama</span><span class="sxs-lookup"><span data-stu-id="1e722-212">Test a Classic web service</span></span>

<span data-ttu-id="1e722-213">Machine Learning Studio'da veya hello Machine Learning Web Hizmetleri portalında bir Klasik web hizmeti test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e722-213">You can test a Classic web service in Machine Learning Studio or in hello Machine Learning Web Services portal.</span></span> 

#### <a name="test-in-machine-learning-studio"></a><span data-ttu-id="1e722-214">Machine Learning Studio'da test</span><span class="sxs-lookup"><span data-stu-id="1e722-214">Test in Machine Learning Studio</span></span>

1. <span data-ttu-id="1e722-215">Merhaba üzerinde **PANO** hello sayfasında hello web hizmeti için **Test** altında düğmesini **varsayılan uç nokta**.</span><span class="sxs-lookup"><span data-stu-id="1e722-215">On hello **DASHBOARD** page for hello web service, click hello **Test** button under **Default Endpoint**.</span></span> <span data-ttu-id="1e722-216">Bir iletişim kutusu açılır ve hello hizmeti için bir giriş verisi hello sorar.</span><span class="sxs-lookup"><span data-stu-id="1e722-216">A dialog pops up and asks you for hello input data for hello service.</span></span> <span data-ttu-id="1e722-217">Bunlar hello hello özgün kredi riski dataset içinde görünen aynı sütunları olur.</span><span class="sxs-lookup"><span data-stu-id="1e722-217">These are hello same columns that appeared in hello original credit risk dataset.</span></span>  

2. <span data-ttu-id="1e722-218">Bir veri kümesi girin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="1e722-218">Enter a set of data and then click **OK**.</span></span> 

#### <a name="test-in-hello-machine-learning-web-services-portal"></a><span data-ttu-id="1e722-219">Merhaba Machine Learning Web Hizmetleri Portalı'nda test</span><span class="sxs-lookup"><span data-stu-id="1e722-219">Test in hello Machine Learning Web Services portal</span></span>

1. <span data-ttu-id="1e722-220">Merhaba üzerinde **PANO** hello sayfasında hello web hizmeti için **Test Önizleme** altında bağlantı **varsayılan uç nokta**.</span><span class="sxs-lookup"><span data-stu-id="1e722-220">On hello **DASHBOARD** page for hello web service, click hello **Test preview** link under **Default Endpoint**.</span></span> <span data-ttu-id="1e722-221">Merhaba web hizmeti uç noktası için hello Azure Machine Learning Web Hizmetleri portalında Hello test sayfası açılır ve hello hizmeti için bir giriş verisi hello sorar.</span><span class="sxs-lookup"><span data-stu-id="1e722-221">hello test page in hello Azure Machine Learning Web Services portal for hello web service endpoint opens and asks you for hello input data for hello service.</span></span> <span data-ttu-id="1e722-222">Bunlar hello hello özgün kredi riski dataset içinde görünen aynı sütunları olur.</span><span class="sxs-lookup"><span data-stu-id="1e722-222">These are hello same columns that appeared in hello original credit risk dataset.</span></span>

2. <span data-ttu-id="1e722-223">Tıklatın **Test istek-yanıt**.</span><span class="sxs-lookup"><span data-stu-id="1e722-223">Click **Test Request-Response**.</span></span> 

### <a name="test-a-new-web-service"></a><span data-ttu-id="1e722-224">Yeni bir web hizmeti test etme</span><span class="sxs-lookup"><span data-stu-id="1e722-224">Test a New web service</span></span>

<span data-ttu-id="1e722-225">Yalnızca hello Machine Learning Web Hizmetleri portalında yeni bir web hizmeti test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e722-225">You can test a New web service only in hello Machine Learning Web Services portal.</span></span>

1. <span data-ttu-id="1e722-226">Merhaba, [Azure Machine Learning Web Hizmetleri](https://services.azureml.net/quickstart) portal tıklatın **Test** hello sayfanın üst kısmındaki hello.</span><span class="sxs-lookup"><span data-stu-id="1e722-226">In hello [Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal, click **Test** at hello top of hello page.</span></span> <span data-ttu-id="1e722-227">Merhaba **Test** sayfası açılır ve hello hizmeti verileri girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e722-227">hello **Test** page opens and you can input data for hello service.</span></span> <span data-ttu-id="1e722-228">Görüntülenen hello giriş alanları hello özgün kredi riski dataset içinde görünen toohello sütunlar karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="1e722-228">hello input fields displayed correspond toohello columns that appeared in hello original credit risk dataset.</span></span> 

2. <span data-ttu-id="1e722-229">Bir veri kümesi girin ve ardından **Test istek-yanıt**.</span><span class="sxs-lookup"><span data-stu-id="1e722-229">Enter a set of data and then click **Test Request-Response**.</span></span>

<span data-ttu-id="1e722-230">Merhaba hello test sonuçlarını hello sağ tarafında hello çıkış sütununun hello sayfasında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="1e722-230">hello results of hello test are displayed on hello right-hand side of hello page in hello output column.</span></span> 


## <a name="manage-hello-web-service"></a><span data-ttu-id="1e722-231">Merhaba web hizmetini yönetme</span><span class="sxs-lookup"><span data-stu-id="1e722-231">Manage hello web service</span></span>

### <a name="manage-a-classic-web-service-in-hello-azure-classic-portal"></a><span data-ttu-id="1e722-232">Merhaba Klasik Azure portalında bir Klasik web hizmeti yönetme</span><span class="sxs-lookup"><span data-stu-id="1e722-232">Manage a Classic web service in hello Azure classic portal</span></span>

<span data-ttu-id="1e722-233">Klasik web hizmeti dağıttıktan sonra sonra hello yönetebilirsiniz [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="1e722-233">Once you've deployed your Classic web service, you can manage it from hello [Azure classic portal](https://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="1e722-234">İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="1e722-234">Sign in toohello [Azure classic portal](https://manage.windowsazure.com)</span></span>
2. <span data-ttu-id="1e722-235">Merhaba Microsoft Azure Hizmetleri panelinde tıklatın **MACHINE LEARNING**</span><span class="sxs-lookup"><span data-stu-id="1e722-235">In hello Microsoft Azure services panel, click **MACHINE LEARNING**</span></span>
3. <span data-ttu-id="1e722-236">Çalışma alanınızı tıklatın</span><span class="sxs-lookup"><span data-stu-id="1e722-236">Click your workspace</span></span>
4. <span data-ttu-id="1e722-237">Merhaba tıklatın **Web Hizmetleri** sekmesi</span><span class="sxs-lookup"><span data-stu-id="1e722-237">Click hello **Web services** tab</span></span>
5. <span data-ttu-id="1e722-238">Oluşturduğumuz hello web hizmeti</span><span class="sxs-lookup"><span data-stu-id="1e722-238">Click hello web service we created</span></span>
6. <span data-ttu-id="1e722-239">Merhaba "varsayılan" uç noktasına tıklayın</span><span class="sxs-lookup"><span data-stu-id="1e722-239">Click hello "default" endpoint</span></span>

<span data-ttu-id="1e722-240">Buradan, hello web hizmeti nasıl çalıştığını izlemek gibi şeyler ve kaç tane eşzamanlı çağrıları hello hizmet işleyebilir değiştirerek performans tweaks hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e722-240">From here, you can do things like monitor how hello web service is doing and make performance tweaks by changing how many concurrent calls hello service can handle.</span></span>

<span data-ttu-id="1e722-241">Daha ayrıntılı bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="1e722-241">For more details, see:</span></span>

* [<span data-ttu-id="1e722-242">Uç noktaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="1e722-242">Creating Endpoints</span></span>](machine-learning-create-endpoint.md)
* [<span data-ttu-id="1e722-243">Web hizmeti ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="1e722-243">Scaling web service</span></span>](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-hello-azure-machine-learning-web-services-portal"></a><span data-ttu-id="1e722-244">Klasik veya yeni bir web hizmeti hello Azure Machine Learning Web Hizmetleri portalında Yönet</span><span class="sxs-lookup"><span data-stu-id="1e722-244">Manage a Classic or New web service in hello Azure Machine Learning Web Services portal</span></span>

<span data-ttu-id="1e722-245">Klasik ya da yeni web hizmetinizi dağıttıktan sonra sonra hello yönetebilirsiniz [Microsoft Azure Machine Learning Web Hizmetleri](https://services.azureml.net/quickstart) portal.</span><span class="sxs-lookup"><span data-stu-id="1e722-245">Once you've deployed your web service, whether Classic or New, you can manage it from hello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal.</span></span>

<span data-ttu-id="1e722-246">web hizmetinizin toomonitor hello performans:</span><span class="sxs-lookup"><span data-stu-id="1e722-246">toomonitor hello performance of your web service:</span></span>

1. <span data-ttu-id="1e722-247">İçinde toohello oturum [Microsoft Azure Machine Learning Web Hizmetleri](https://services.azureml.net/quickstart) portalı</span><span class="sxs-lookup"><span data-stu-id="1e722-247">Sign in toohello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal</span></span>
2. <span data-ttu-id="1e722-248">Tıklatın **Web Hizmetleri**</span><span class="sxs-lookup"><span data-stu-id="1e722-248">Click **Web services**</span></span>
3. <span data-ttu-id="1e722-249">Web hizmeti</span><span class="sxs-lookup"><span data-stu-id="1e722-249">Click your web service</span></span>
4. <span data-ttu-id="1e722-250">Merhaba tıklatın **Panosu**</span><span class="sxs-lookup"><span data-stu-id="1e722-250">Click hello **Dashboard**</span></span>

- - -
<span data-ttu-id="1e722-251">**Sonraki: [erişim hello web hizmeti](machine-learning-walkthrough-6-access-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="1e722-251">**Next: [Access hello web service](machine-learning-walkthrough-6-access-web-service.md)**</span></span>

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
