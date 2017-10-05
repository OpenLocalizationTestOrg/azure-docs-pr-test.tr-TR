---
title: "Modelinizi Azure Machine Learning Studio'da dağıtımına hazırlamak nasıl | Microsoft Docs"
description: "Tahmine dayalı bir deneme Machine Learning Studio'da eğitim denemenizi dönüştürerek eğitilen modelinizi bir web hizmeti olarak dağıtımına hazırlamak nasıl."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: eb943c45-541a-401d-844a-c3337de82da6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: garye
ms.openlocfilehash: 716a9a9b723df7ff6eb111fa40f2b5941d57d67a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-prepare-your-model-for-deployment-in-azure-machine-learning-studio"></a><span data-ttu-id="51692-103">Modelinizi Azure Machine Learning Studio'daki dağıtımı için hazırlama</span><span class="sxs-lookup"><span data-stu-id="51692-103">How to prepare your model for deployment in Azure Machine Learning Studio</span></span>

<span data-ttu-id="51692-104">Azure Machine Learning Studio'da Tahmine dayalı bir analiz modeli geliştirmek ve bir Azure web hizmeti olarak dağıtarak faaliyete için ihtiyacınız olan araçları sağlar.</span><span class="sxs-lookup"><span data-stu-id="51692-104">Azure Machine Learning Studio gives you the tools you need to develop a predictive analytics model and then operationalize it by deploying it as an Azure web service.</span></span>

<span data-ttu-id="51692-105">Bunu yapmak için Studio adlı bir denemeyi - oluşturmak için kullandığınız bir *eğitim denemenizi* - burada eğitme, Puanlama ve modelinizi Düzenle.</span><span class="sxs-lookup"><span data-stu-id="51692-105">To do this, you use Studio to create an experiment - called a *training experiment* - where you train, score, and edit your model.</span></span> <span data-ttu-id="51692-106">Memnun kaldıktan sonra model eğitim denemenizi dönüştürerek dağıtmaya hazırlanırken bir *Tahmine dayalı denemeye* puan kullanıcı verilerini yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="51692-106">Once you're satisfied, you get your model ready to deploy by converting your training experiment to a *predictive experiment* that's configured to score user data.</span></span>

<span data-ttu-id="51692-107">Bu işlemde örneği görebilirsiniz [izlenecek yol: Azure Machine Learning kredi riski değerlendirmesi için Tahmine dayalı analiz çözümü geliştirme](machine-learning-walkthrough-develop-predictive-solution.md).</span><span class="sxs-lookup"><span data-stu-id="51692-107">You can see an example of this process in [Walkthrough: Develop a predictive analytics solution for credit risk assessment in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

<span data-ttu-id="51692-108">Bu makalede derinlemesine eğitim denemenizi Tahmine dayalı bir deneme nasıl dönüştürüldüğü ve bu Tahmine dayalı denemeye nasıl dağıtıldığını ayrıntılarını içine alır.</span><span class="sxs-lookup"><span data-stu-id="51692-108">This article takes a deep dive into the details of how a training experiment gets converted into a predictive experiment, and how that predictive experiment is deployed.</span></span> <span data-ttu-id="51692-109">Bu ayrıntılar anlayarak, dağıtılan modelinizi daha etkili olması için yapılandırmak nasıl öğrenebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51692-109">By understanding these details, you can learn how to configure your deployed model to make it more effective.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a><span data-ttu-id="51692-110">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="51692-110">Overview</span></span> 

<span data-ttu-id="51692-111">Tahmine dayalı bir deneme eğitim denemenizi dönüştürme işlemi üç adımdan oluşur:</span><span class="sxs-lookup"><span data-stu-id="51692-111">The process of converting a training experiment to a predictive experiment involves three steps:</span></span>

1. <span data-ttu-id="51692-112">Makine öğrenimi algoritması modüller, eğitilen model ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="51692-112">Replace the machine learning algorithm modules with your trained model.</span></span>
2. <span data-ttu-id="51692-113">Puanlama için gerekli olan modülleri denemede kesim.</span><span class="sxs-lookup"><span data-stu-id="51692-113">Trim the experiment to only those modules that are needed for scoring.</span></span> <span data-ttu-id="51692-114">Eğitim denemenizi eğitim için gerekli olan, ancak model eğitildi sonra gerekli olmayan modülleri sayısını içerir.</span><span class="sxs-lookup"><span data-stu-id="51692-114">A training experiment includes a number of modules that are necessary for training but are not needed once the model is trained.</span></span>
3. <span data-ttu-id="51692-115">Modelinizi web hizmeti kullanıcı verileri nasıl kabul ettiği ve hangi verilerin döndürülür tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="51692-115">Define how your model will accept data from the web service user, and what data will be returned.</span></span>

> [!TIP]
> <span data-ttu-id="51692-116">Eğitim denemenizi eğitim ve puanlama kendi verilerinizi kullanarak modelinizi ilgilenen.</span><span class="sxs-lookup"><span data-stu-id="51692-116">In your training experiment, you've been concerned with training and scoring your model using your own data.</span></span> <span data-ttu-id="51692-117">Ancak uygulama dağıtıldıktan sonra kullanıcılar modelinize yeni veri göndermek ve tahmin sonuçlarını döndürür.</span><span class="sxs-lookup"><span data-stu-id="51692-117">But once deployed, users will send new data to your model and it will return prediction results.</span></span> <span data-ttu-id="51692-118">Dağıtım için hazır hale getirmek için Tahmine dayalı bir deneme eğitim denemenizi dönüştürmek gibi bu nedenle, nasıl model başkaları tarafından kullanılacak göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="51692-118">So, as you convert your training experiment to a predictive experiment to get it ready for deployment, keep in mind how the model will be used by others.</span></span>
> 
> 

## <a name="set-up-web-service-button"></a><span data-ttu-id="51692-119">Web hizmetinin ayarı düğmesi</span><span class="sxs-lookup"><span data-stu-id="51692-119">Set Up Web Service button</span></span>
<span data-ttu-id="51692-120">Denemenizi çalıştırdıktan sonra (tıklatın **çalıştırmak** deneme tuvalinin altındaki), tıklatın **Web hizmetinin ayarı** düğmesini (seçin **Tahmine dayalı Web hizmeti** seçeneği).</span><span class="sxs-lookup"><span data-stu-id="51692-120">After you run your experiment (click **RUN** at the bottom of the experiment canvas), click the **Set Up Web Service** button (select the **Predictive Web Service** option).</span></span> <span data-ttu-id="51692-121">**Web hizmetinin ayarı** sizin için Tahmine dayalı bir deneme eğitim denemenizi dönüştürme üç adımları gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="51692-121">**Set Up Web Service** performs for you the three steps of converting your training experiment to a predictive experiment:</span></span>

1. <span data-ttu-id="51692-122">Eğitilmiş modelinizi kaydeder **eğitilmiş modeller** modül paletindeki (deneme tuvalinin sol) bölümü.</span><span class="sxs-lookup"><span data-stu-id="51692-122">It saves your trained model in the **Trained Models** section of the module palette (to the left of the experiment canvas).</span></span> <span data-ttu-id="51692-123">Ardından makine öğrenme algoritmasının yerine geçer ve [Train Model] [ train-model] kaydedilmiş eğitilen model modüllerle.</span><span class="sxs-lookup"><span data-stu-id="51692-123">It then replaces the machine learning algorithm and [Train Model][train-model] modules with the saved trained model.</span></span>
2. <span data-ttu-id="51692-124">Denemenizi analiz eder ve yalnızca eğitim için açıkça kullanılmış ve artık gerekmeyen modülleri kaldırır.</span><span class="sxs-lookup"><span data-stu-id="51692-124">It analyzes your experiment and removes modules that were clearly used only for training and are no longer needed.</span></span>
3. <span data-ttu-id="51692-125">Bunu ekler _Web hizmeti girişi_ ve _çıkış_ denemenizi (Bu modülleri kabul etmek ve kullanıcı verilerini dönmek) varsayılan konumlarda modüllerine.</span><span class="sxs-lookup"><span data-stu-id="51692-125">It inserts _Web service input_ and _output_ modules into default locations in your experiment (these modules accept and return user data).</span></span>

<span data-ttu-id="51692-126">Örneğin, aşağıdaki deneme örnek census verileri kullanarak iki sınıflı artırılmış karar ağacı modeli eğitir:</span><span class="sxs-lookup"><span data-stu-id="51692-126">For example, the following experiment trains a two-class boosted decision tree model using sample census data:</span></span>

![Eğitim denemenizi][figure1]

<span data-ttu-id="51692-128">Bu deneme modülleri temelde dört farklı işlevleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="51692-128">The modules in this experiment perform basically four different functions:</span></span>

![Modül işlevleri][figure2]

<span data-ttu-id="51692-130">Bu eğitim denemenizi Tahmine dayalı bir deneme dönüştürürken bazı bu modüllerin artık gerekli olmayan veya farklı bir amaç şimdi verdikleri:</span><span class="sxs-lookup"><span data-stu-id="51692-130">When you convert this training experiment to a predictive experiment, some of these modules are no longer needed, or they now serve a different purpose:</span></span>

* <span data-ttu-id="51692-131">**Veri** -Bu örnek veri kümesindeki veriler Puanlama sırasında kullanılmaz - web hizmeti kullanıcı belirtmek için veri sağlayacak.</span><span class="sxs-lookup"><span data-stu-id="51692-131">**Data** - The data in this sample dataset is not used during scoring - the user of the web service will supply the data to be scored.</span></span> <span data-ttu-id="51692-132">Ancak, veri türleri gibi bu veri kümesi meta verileri eğitilen modeli tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="51692-132">However, the metadata from this dataset, such as data types, is used by the trained model.</span></span> <span data-ttu-id="51692-133">Bu nedenle böylece bu meta verileri sağlayabilir Tahmine dayalı denemeye dataset tutmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="51692-133">So you need to keep the dataset in the predictive experiment so that it can provide this metadata.</span></span>

* <span data-ttu-id="51692-134">**Hazırlığı** - Puanlama için bu modülleri olabilir veya gelen verileri işlemek gerekli olmayabilir gönderilecek kullanıcı verilere bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="51692-134">**Prep** - Depending on the user data that will be submitted for scoring, these modules may or may not be necessary to process the incoming data.</span></span> <span data-ttu-id="51692-135">**Web hizmetinin ayarı** düğmesi bu touch değil - nasıl bunları işlemek istediğinize karar vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="51692-135">The **Set Up Web Service** button doesn't touch these - you need to decide how you want to handle them.</span></span>
  
    <span data-ttu-id="51692-136">Örneğin, örnek veri kümesi olabilir eksik değerleri, bu nedenle bu örnekte bir [Clean Missing Data] [ clean-missing-data] modülü bunlarla dağıtılacak dahil.</span><span class="sxs-lookup"><span data-stu-id="51692-136">For instance, in this example the sample dataset may have missing values, so a [Clean Missing Data][clean-missing-data] module was included to deal with them.</span></span> <span data-ttu-id="51692-137">Ayrıca, örnek veri kümesi modeli eğitmek için gerekli olmayan sütunları içerir.</span><span class="sxs-lookup"><span data-stu-id="51692-137">Also, the sample dataset includes columns that are not needed to train the model.</span></span> <span data-ttu-id="51692-138">Bu nedenle bir [Select Columns in Dataset sütun] [ select-columns] modülü veri akışından bu ek sütunları hariç tutulacak dahil.</span><span class="sxs-lookup"><span data-stu-id="51692-138">So a [Select Columns in Dataset][select-columns] module was included to exclude those extra columns from the data flow.</span></span> <span data-ttu-id="51692-139">Web hizmeti aracılığıyla Puanlama için gönderilen veri eksik değerleri olmaz ve ardından, kaldırabilirsiniz biliyorsanız [Clean Missing Data] [ clean-missing-data] modülü.</span><span class="sxs-lookup"><span data-stu-id="51692-139">If you know that the data that will be submitted for scoring through the web service will not have missing values, then you can remove the [Clean Missing Data][clean-missing-data] module.</span></span> <span data-ttu-id="51692-140">Ancak, bu yana [Select Columns in Dataset sütun] [ select-columns] modülü yardımcı olan eğitilen model bekliyor veri sütunlarının tanımlamak, bu modül kalması gerekir.</span><span class="sxs-lookup"><span data-stu-id="51692-140">However, since the [Select Columns in Dataset][select-columns] module helps define the columns of data that the trained model expects, that module needs to remain.</span></span>

* <span data-ttu-id="51692-141">**Eğitmek** -Bu modüller modeli eğitmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="51692-141">**Train** - These modules are used to train the model.</span></span> <span data-ttu-id="51692-142">Tıkladığınızda **Web hizmetinin ayarı**, bu modüller, eğitilmiş model içeren tek bir modülü ile değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="51692-142">When you click **Set Up Web Service**, these modules are replaced with a single module that contains the model you trained.</span></span> <span data-ttu-id="51692-143">Bu yeni modül kaydedilir **eğitilmiş modeller** modül paleti bölümü.</span><span class="sxs-lookup"><span data-stu-id="51692-143">This new module is saved in the **Trained Models** section of the module palette.</span></span>

* <span data-ttu-id="51692-144">**Puan** - Bu örnekte, [bölünmüş veri] [ split] modülü, veri akışı test verileri ve eğitim veri bölmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="51692-144">**Score** - In this example, the [Split Data][split] module is used to divide the data stream into test data and training data.</span></span> <span data-ttu-id="51692-145">Tahmine dayalı denemesinde biz artık, bunu Eğitim değil [bölünmüş veri] [ split] kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="51692-145">In the predictive experiment, we're not training anymore, so [Split Data][split] can be removed.</span></span> <span data-ttu-id="51692-146">Benzer şekilde, ikinci [Score Model] [ score-model] modülü ve [Evaluate Model] [ evaluate-model] modülü, bu nedenle test verileri sonuçları karşılaştırmak için kullanılır Bu modüller Tahmine dayalı denemeye gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="51692-146">Similarly, the second [Score Model][score-model] module and the [Evaluate Model][evaluate-model] module are used to compare results from the test data, so these modules are not needed in the predictive experiment.</span></span> <span data-ttu-id="51692-147">Kalan [Score Model] [ score-model] modülü, ancak, web hizmeti aracılığıyla bir puan sonuca dönmek için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="51692-147">The remaining [Score Model][score-model] module, however, is needed to return a score result through the web service.</span></span>

<span data-ttu-id="51692-148">İşte tıkladıktan sonra örneğimizde nasıl göründüğünü **Web hizmetinin ayarı**:</span><span class="sxs-lookup"><span data-stu-id="51692-148">Here is how our example looks after clicking **Set Up Web Service**:</span></span>

![Dönüştürülen tahmini deneme][figure3]

<span data-ttu-id="51692-150">Çalışmanın **Web hizmetinin ayarı** denemenizi bir web hizmeti olarak dağıtılması için hazırlamak yeterli olabilir.</span><span class="sxs-lookup"><span data-stu-id="51692-150">The work done by **Set Up Web Service** may be sufficient to prepare your experiment to be deployed as a web service.</span></span> <span data-ttu-id="51692-151">Ancak, bazı ek iş denemenizi için belirli yapmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51692-151">However, you may want to do some additional work specific to your experiment.</span></span>

### <a name="adjust-input-and-output-modules"></a><span data-ttu-id="51692-152">Giriş ve çıkış modülleri Ayarla</span><span class="sxs-lookup"><span data-stu-id="51692-152">Adjust input and output modules</span></span>
<span data-ttu-id="51692-153">Eğitim denemenizi bir eğitim veri kümesi kullanılan ve makine öğrenme algoritmasını gerekli bir formda veri almak için bazı işleme vermedi.</span><span class="sxs-lookup"><span data-stu-id="51692-153">In your training experiment, you used a set of training data and then did some processing to get the data in a form that the machine learning algorithm needed.</span></span> <span data-ttu-id="51692-154">Web hizmeti aracılığıyla almaya beklediğiniz verileri bu işlem gerekmez, atlayabilirsiniz: çıkışına bağlayın **Web hizmeti giriş Modülü** denemenizi farklı bir modüle için.</span><span class="sxs-lookup"><span data-stu-id="51692-154">If the data you expect to receive through the web service will not need this processing, you can bypass it: connect the output of the **Web service input module** to a different module in your experiment.</span></span> <span data-ttu-id="51692-155">Kullanıcının verileri artık bu konumda modelindeki ulaşırsınız.</span><span class="sxs-lookup"><span data-stu-id="51692-155">The user's data will now arrive in the model at this location.</span></span>

<span data-ttu-id="51692-156">Örneğin, varsayılan olarak **Web hizmetinin ayarı** koyar **Web hizmeti girişi** Yukarıdaki şekilde gösterildiği gibi veri akışı üstündeki modülü.</span><span class="sxs-lookup"><span data-stu-id="51692-156">For example, by default **Set Up Web Service** puts the **Web service input** module at the top of your data flow, as shown in the figure above.</span></span> <span data-ttu-id="51692-157">Ancak biz el ile yerleştirebilirsiniz **Web hizmeti girişi** veri işleme modülleri geçmiş:</span><span class="sxs-lookup"><span data-stu-id="51692-157">But we can manually position the **Web service input** past the data processing modules:</span></span>

![Web hizmeti girişi taşıma][figure4]

<span data-ttu-id="51692-159">Web hizmeti aracılığıyla sağlanan giriş verileri, herhangi bir önişleme olmadan doğrudan Score Model modüle şimdi geçer.</span><span class="sxs-lookup"><span data-stu-id="51692-159">The input data provided through the web service will now pass directly into the Score Model module without any preprocessing.</span></span>

<span data-ttu-id="51692-160">Benzer şekilde, varsayılan olarak **Web hizmetinin ayarı** Web hizmeti çıkış modülü, veri akışı sonundaki koyar.</span><span class="sxs-lookup"><span data-stu-id="51692-160">Similarly, by default **Set Up Web Service** puts the Web service output module at the bottom of your data flow.</span></span> <span data-ttu-id="51692-161">Bu örnekte, web hizmeti çıktısını kullanıcıya döndürülecek [Score Model] [ score-model] tam giriş verisi vektör artı Puanlama sonuçları içeren modülü.</span><span class="sxs-lookup"><span data-stu-id="51692-161">In this example, the web service will return to the user the output of the [Score Model][score-model] module, which includes the complete input data vector plus the scoring results.</span></span>
<span data-ttu-id="51692-162">Farklı bir şey döndürmek tercih ediyorsanız, ancak daha sonra önce ek modüller ekleyebilirsiniz **Web hizmeti çıkış** modülü.</span><span class="sxs-lookup"><span data-stu-id="51692-162">However, if you would prefer to return something different, then you can add additional modules before the **Web service output** module.</span></span> 

<span data-ttu-id="51692-163">Örneğin, yalnızca Puanlama sonuçları ve giriş verileri değil tüm vektörü döndürmek için ekleyin bir [Select Columns in Dataset sütun] [ select-columns] Puanlama sonuçları hariç tüm sütunlar hariç tutulacak modülü.</span><span class="sxs-lookup"><span data-stu-id="51692-163">For example, to return only the scoring results and not the entire vector of input data, add a [Select Columns in Dataset][select-columns] module to exclude all columns except the scoring results.</span></span> <span data-ttu-id="51692-164">Ardından taşıma **Web hizmeti çıkış** çıktısını modülüne [Select Columns in Dataset sütun] [ select-columns] modülü.</span><span class="sxs-lookup"><span data-stu-id="51692-164">Then move the **Web service output** module to the output of the [Select Columns in Dataset][select-columns] module.</span></span> <span data-ttu-id="51692-165">Denemeyi şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="51692-165">The experiment looks like this:</span></span>

![Web hizmeti çıkış taşıma][figure5]

### <a name="add-or-remove-additional-data-processing-modules"></a><span data-ttu-id="51692-167">Ek veri işleme modülleri Ekle Kaldır</span><span class="sxs-lookup"><span data-stu-id="51692-167">Add or remove additional data processing modules</span></span>
<span data-ttu-id="51692-168">Puanlama sırasında ihtiyaç bildiğiniz denemenizi daha fazla modülleri varsa bunlar kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="51692-168">If there are more modules in your experiment that you know will not be needed during scoring, these can be removed.</span></span> <span data-ttu-id="51692-169">Örneğin, biz taşınmış olduğundan **Web hizmeti girişi** noktasında veri işleme modülleri sonra modülü, biz kaldırabilirsiniz [Clean Missing Data] [ clean-missing-data] Modülü Tahmine dayalı denemeye.</span><span class="sxs-lookup"><span data-stu-id="51692-169">For example, because we moved the **Web service input** module to a point after the data processing modules, we can remove the [Clean Missing Data][clean-missing-data] module from the predictive experiment.</span></span>

<span data-ttu-id="51692-170">Bizim Tahmine dayalı denemeye şimdi şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="51692-170">Our predictive experiment now looks like this:</span></span>

![Ek modülü kaldırma][figure6]


### <a name="add-optional-web-service-parameters"></a><span data-ttu-id="51692-172">İsteğe bağlı Web hizmeti parametreleri ekleme</span><span class="sxs-lookup"><span data-stu-id="51692-172">Add optional Web Service Parameters</span></span>
<span data-ttu-id="51692-173">Bazı durumlarda, hizmet erişildiğinde modülleri davranışını değiştirmek kullanıcı web hizmetinizin izin vermek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51692-173">In some cases, you may want to allow the user of your web service to change the behavior of modules when the service is accessed.</span></span> <span data-ttu-id="51692-174">*Web hizmeti parametreleri* bu yapmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="51692-174">*Web Service Parameters* allow you to do this.</span></span>

<span data-ttu-id="51692-175">Yaygın bir örnek ayarlama bir [veri içeri aktarma] [ import-data] web hizmeti erişildiğinde dağıtılan web hizmeti kullanıcı farklı bir veri kaynağına belirtebilmeniz modülü.</span><span class="sxs-lookup"><span data-stu-id="51692-175">A common example is setting up an [Import Data][import-data] module so the user of the deployed web service can specify a different data source when the web service is accessed.</span></span> <span data-ttu-id="51692-176">Veya yapılandırma bir [verileri dışa aktar] [ export-data] modülü böylece farklı bir hedef belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="51692-176">Or configuring an [Export Data][export-data] module so that a different destination can be specified.</span></span>

<span data-ttu-id="51692-177">Web hizmeti parametreleri tanımlamak ve bir veya daha fazla modülü parametreleri ile ilişkilendirmek ve gerekli veya isteğe bağlı oldukları belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51692-177">You can define Web Service Parameters and associate them with one or more module parameters, and you can specify whether they are required or optional.</span></span> <span data-ttu-id="51692-178">Web hizmeti kullanıcı hizmete erişme ve modül Eylemler uygun şekilde değiştirilir Bu parametreler için değerler sağlar.</span><span class="sxs-lookup"><span data-stu-id="51692-178">The user of the web service provides values for these parameters when the service is accessed, and the module actions are modified accordingly.</span></span>

<span data-ttu-id="51692-179">Web hizmeti parametreleri nedir ve bunların nasıl kullanılacağını hakkında daha fazla bilgi için bkz: [kullanarak Azure Machine Learning Web hizmeti parametreleri][webserviceparameters].</span><span class="sxs-lookup"><span data-stu-id="51692-179">For more information about what Web Service Parameters are and how to use them, see [Using Azure Machine Learning Web Service Parameters][webserviceparameters].</span></span>

[webserviceparameters]: machine-learning-web-service-parameters.md


## <a name="deploy-the-predictive-experiment-as-a-web-service"></a><span data-ttu-id="51692-180">Tahmine dayalı denemeye bir web hizmeti olarak dağıtma</span><span class="sxs-lookup"><span data-stu-id="51692-180">Deploy the predictive experiment as a web service</span></span>
<span data-ttu-id="51692-181">Tahmine dayalı denemeye yeterince hazırlandı, bir Azure web hizmeti olarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51692-181">Now that the predictive experiment has been sufficiently prepared, you can deploy it as an Azure web service.</span></span> <span data-ttu-id="51692-182">Web hizmetini kullanarak, kullanıcılar modelinize veri gönderebilir ve model kendi tahminleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="51692-182">Using the web service, users can send data to your model and the model will return its predictions.</span></span>

<span data-ttu-id="51692-183">Tam dağıtım işlemi hakkında daha fazla bilgi için bkz: [bir Azure Machine Learning web hizmetini dağıtma][deploy]</span><span class="sxs-lookup"><span data-stu-id="51692-183">For more information on the complete deployment process, see [Deploy an Azure Machine Learning web service][deploy]</span></span>

[deploy]: machine-learning-publish-a-machine-learning-web-service.md


<!-- Images -->
[figure1]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure1.png
[figure2]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure2.png
[figure3]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure3.png
[figure4]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure4.png
[figure5]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure5.png
[figure6]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure6.png


<!-- Module References -->
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[export-data]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/
