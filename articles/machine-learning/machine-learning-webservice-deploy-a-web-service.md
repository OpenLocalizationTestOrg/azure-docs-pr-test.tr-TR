---
title: Yeni bir web hizmeti Azure Machine learning'de aaaDeploying | Microsoft Docs
description: "web hizmeti bir ARM dağıtma hello iş akışı tabanlı"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: a358b04f-0d08-4d50-820e-eeac971854cf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: v-donglo
ROBOTS: NOINDEX
redirect_url: machine-learning-publish-a-machine-learning-web-service
redirect_document_id: True
ms.openlocfilehash: 2cbfda44b97a6b992fbdfdfb0c761e6c9e169035
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-new-web-service"></a><span data-ttu-id="0d702-103">Yeni bir web hizmeti dağıtma</span><span class="sxs-lookup"><span data-stu-id="0d702-103">Deploy a new web service</span></span>
<span data-ttu-id="0d702-104">Microsoft Azure Machine şimdi learning temel alan web hizmetleri sağlar [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) yeni faturalama planı seçeneklerini ve web hizmeti toomultiple bölgeler dağıtma için izin verme.</span><span class="sxs-lookup"><span data-stu-id="0d702-104">Microsoft Azure Machine learning now provides web services that are based on [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) allowing for new billing plan options and deploying your web service toomultiple regions.</span></span>

<span data-ttu-id="0d702-105">Merhaba genel iş akışı toodeploy Microsoft Azure Machine Learning Web Hizmetleri kullanarak bir web hizmeti aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="0d702-105">hello general workflow toodeploy a web service using Microsoft Azure Machine Learning Web Services is:</span></span>

* <span data-ttu-id="0d702-106">Tahmine dayalı bir deneme oluşturma</span><span class="sxs-lookup"><span data-stu-id="0d702-106">Create a predictive experiment</span></span>
* <span data-ttu-id="0d702-107">dağıtın</span><span class="sxs-lookup"><span data-stu-id="0d702-107">deploy it</span></span>
* <span data-ttu-id="0d702-108">kendi adı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0d702-108">configure its name</span></span>
* <span data-ttu-id="0d702-109">Fatura planı</span><span class="sxs-lookup"><span data-stu-id="0d702-109">billing plan</span></span>
* <span data-ttu-id="0d702-110">test</span><span class="sxs-lookup"><span data-stu-id="0d702-110">test it</span></span>
* <span data-ttu-id="0d702-111">Bunu kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="0d702-111">consume it.</span></span>

<span data-ttu-id="0d702-112">Grafiği aşağıdaki hello hello iş akışı gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0d702-112">hello following graphic illustrates hello workflow.</span></span>

![Web hizmeti dağıtım iş akışı][1]

## <a name="deploy-web-service-from-studio"></a><span data-ttu-id="0d702-114">Studio'dan Web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="0d702-114">Deploy web service from Studio</span></span>
<span data-ttu-id="0d702-115">bir deneme yeni bir web hizmeti olarak toodeploy.</span><span class="sxs-lookup"><span data-stu-id="0d702-115">toodeploy an experiment as a new web service.</span></span> <span data-ttu-id="0d702-116">Machine Learning Studio Hello oturum açın ve yeni bir Tahmine dayalı web hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0d702-116">Sign into hello Machine Learning Studio and create a new predictive web service.</span></span> 

<span data-ttu-id="0d702-117">**Not**: Klasik web hizmeti olarak bir deneme zaten dağıttıysanız, yeni bir web hizmeti olarak dağıtamazsınız.</span><span class="sxs-lookup"><span data-stu-id="0d702-117">**Note**: If you have already deployed an experiment as a classic web service you cannot deploy it as a new web service.</span></span>

<span data-ttu-id="0d702-118">Tıklatın **çalıştırmak** hello hello altındaki tuvale deneyin ve ardından **Web hizmeti Dağıt** ve **Web hizmeti dağıtma [Yeni]**.</span><span class="sxs-lookup"><span data-stu-id="0d702-118">Click **Run** at hello bottom of hello experiment canvas and then click **Deploy Web Service** and **Deploy Web Service [New]**.</span></span> <span data-ttu-id="0d702-119">Merhaba Machine Learning Web Hizmeti Yöneticisi'nin Hello dağıtım sayfasını açar.</span><span class="sxs-lookup"><span data-stu-id="0d702-119">hello deployment page of hello Machine Learning Web Service manager will open.</span></span>

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a><span data-ttu-id="0d702-120">Machine Learning Web Hizmeti Yöneticisi'ni dağıtmak deneme sayfası</span><span class="sxs-lookup"><span data-stu-id="0d702-120">Machine Learning Web Service Manager Deploy Experiment Page</span></span>
<span data-ttu-id="0d702-121">Merhaba dağıtmak deneme sayfasında hello web hizmeti için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="0d702-121">On hello Deploy Experiment page, enter a name for hello web service.</span></span>
<span data-ttu-id="0d702-122">Fiyatlandırma planı seçin.</span><span class="sxs-lookup"><span data-stu-id="0d702-122">Select a pricing plan.</span></span> <span data-ttu-id="0d702-123">Aksi takdirde, seçebilirsiniz varolan bir fiyatlandırma planı varsa, hello hizmet için yeni bir fiyat planı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0d702-123">If you have an existing pricing plan you can select it, otherwise you must create a new price plan for hello service.</span></span> 

1. <span data-ttu-id="0d702-124">Merhaba, **fiyat planı** açılan, var olan bir planı veya seçin hello **Select yeni plan** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="0d702-124">In hello **Price Plan** drop down, select an existing plan or select hello **Select new plan** option.</span></span>
2. <span data-ttu-id="0d702-125">İçinde **Plan adı**, faturanızı hello planına tanımlayacak bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="0d702-125">In **Plan Name**, type a name that will identify hello plan on your bill.</span></span>
3. <span data-ttu-id="0d702-126">Merhaba birini **aylık Plan katmanlarını**.</span><span class="sxs-lookup"><span data-stu-id="0d702-126">Select one of hello **Monthly Plan Tiers**.</span></span> <span data-ttu-id="0d702-127">Merhaba plan katmanlarını toohello planları varsayılan bölgeniz ve web hizmetiniz için varsayılan not dağıtılan toothat bölgedir.</span><span class="sxs-lookup"><span data-stu-id="0d702-127">Note that hello plan tiers default toohello plans for your default region and your web service is deployed toothat region.</span></span>

<span data-ttu-id="0d702-128">Tıklatın **dağıtma** ve web hizmetiniz için hello hızlı başlangıç sayfasını açar.</span><span class="sxs-lookup"><span data-stu-id="0d702-128">Click **Deploy** and hello Quickstart page for your web service opens.</span></span>

## <a name="quickstart-page"></a><span data-ttu-id="0d702-129">Hızlı Başlangıç sayfası</span><span class="sxs-lookup"><span data-stu-id="0d702-129">Quickstart page</span></span>
<span data-ttu-id="0d702-130">Hello web hizmeti hızlı başlangıç sayfası yeni bir web hizmeti oluşturduktan sonra gerçekleştirecek hello en yaygın görevleri erişim ve rehberlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="0d702-130">hello web service Quickstart page gives you access and guidance on hello most common tasks you will perform after creating a new web service.</span></span> <span data-ttu-id="0d702-131">Buradan hem hello kolayca erişebilirsiniz **Test** sayfa ve **Tüket** sayfası.</span><span class="sxs-lookup"><span data-stu-id="0d702-131">From here you can easily access both hello **Test** page and **Consume** page.</span></span>

## <a name="testing-your-web-service"></a><span data-ttu-id="0d702-132">Web hizmeti test etme</span><span class="sxs-lookup"><span data-stu-id="0d702-132">Testing your web service</span></span>
<span data-ttu-id="0d702-133">Merhaba hızlı başlangıç sayfası, Ortak Görevler altında Test web hizmeti tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0d702-133">From hello Quickstart page, click Test web service under common tasks.</span></span>   

<span data-ttu-id="0d702-134">tootest hello web hizmeti bir istek-yanıt hizmeti'olarak (RR):</span><span class="sxs-lookup"><span data-stu-id="0d702-134">tootest hello web service as a Request-Response Service (RRS):</span></span>

* <span data-ttu-id="0d702-135">Tıklatın **Test** hello menü çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="0d702-135">Click **Test** on hello menu bar.</span></span>
* <span data-ttu-id="0d702-136">Tıklatın **istek-yanıt**.</span><span class="sxs-lookup"><span data-stu-id="0d702-136">Click **Request-Response**.</span></span>
* <span data-ttu-id="0d702-137">Merhaba giriş sütunlarının denemenizi için uygun değerleri girin.</span><span class="sxs-lookup"><span data-stu-id="0d702-137">Enter appropriate values for hello input columns of your experiment.</span></span>
* <span data-ttu-id="0d702-138">Test tıklatın **istek-yanıt**.</span><span class="sxs-lookup"><span data-stu-id="0d702-138">Click Test **Request-Response**.</span></span>

<span data-ttu-id="0d702-139">Merhaba sağ tarafta hello sayfasının, sonuçları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="0d702-139">You results will display on hello right hand side of hello page.</span></span>

<span data-ttu-id="0d702-140">tootest toplu yürütme hizmeti (BES) web hizmeti, bir CSV dosyası kullanır:</span><span class="sxs-lookup"><span data-stu-id="0d702-140">tootest a Batch Execution Service (BES) web service, you will use a CSV file:</span></span>

* <span data-ttu-id="0d702-141">Tıklatın **Test** hello menü çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="0d702-141">Click **Test** on hello menu bar.</span></span>
* <span data-ttu-id="0d702-142">Tıklatın **toplu**.</span><span class="sxs-lookup"><span data-stu-id="0d702-142">Click **Batch**.</span></span>
* <span data-ttu-id="0d702-143">Giriş altında Gözat'ı tıklatın ve tooyour örnek veri dosyası gidin.</span><span class="sxs-lookup"><span data-stu-id="0d702-143">Under your input, click Browse and navigate tooyour sample data file.</span></span>
* <span data-ttu-id="0d702-144">Tıklatın **Test**.</span><span class="sxs-lookup"><span data-stu-id="0d702-144">Click **Test**.</span></span>

<span data-ttu-id="0d702-145">test Hello durumunu altında görüntülenen **Test toplu işleri**.</span><span class="sxs-lookup"><span data-stu-id="0d702-145">hello status of your test is displayed under **Test Batch Jobs**.</span></span>

## <a name="consuming-your-web-service"></a><span data-ttu-id="0d702-146">Web hizmetini kullanma</span><span class="sxs-lookup"><span data-stu-id="0d702-146">Consuming your Web Service</span></span>
<span data-ttu-id="0d702-147">Bir web hizmeti olarak dağıtıldığında, Azure Machine Learning denemeleri çok çeşitli aygıtlar ve platformlar tarafından kullanılabilecek bir REST API sağlar.</span><span class="sxs-lookup"><span data-stu-id="0d702-147">When deployed as a web service, Azure Machine Learning experiments provide a REST API that can be consumed by a wide range of devices and platforms.</span></span> <span data-ttu-id="0d702-148">İletileri basit REST API kabul eder ve JSON ile yanıt verir Merhaba biçimlendirilmiş olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="0d702-148">This is because hello simple REST API accepts and responds with JSON formatted messages.</span></span> <span data-ttu-id="0d702-149">Hello Azure Machine Learning portal sağlar kullanılabilir kod toocall hello web hizmeti R, C# ve Python.</span><span class="sxs-lookup"><span data-stu-id="0d702-149">hello Azure Machine Learning portal provides code that can be used toocall hello web service in R, C#, and Python.</span></span>

<span data-ttu-id="0d702-150">Merhaba tüketim sayfasında bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0d702-150">On hello Consuming page you can find:</span></span>

* <span data-ttu-id="0d702-151">Merhaba API anahtarı ve web hizmeti uygulamalarda tüketimi için URI'si.</span><span class="sxs-lookup"><span data-stu-id="0d702-151">hello API key and URI's for consuming web service in apps.</span></span>
* <span data-ttu-id="0d702-152">Excel ve web uygulama şablonları tookick tüketim işlemi başlatın.</span><span class="sxs-lookup"><span data-stu-id="0d702-152">Excel and web app templates tookick start your consumption process.</span></span>
* <span data-ttu-id="0d702-153">C#, python ve R tooget örnek kodda, başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="0d702-153">Sample code in C#, python, and R tooget you started.</span></span>

<span data-ttu-id="0d702-154">Web hizmetleri kullanma ile ilgili daha fazla bilgi için bkz: [nasıl tooconsume bir Azure Machine Learning Web hizmeti](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="0d702-154">For more information on consuming web services, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d702-155">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="0d702-155">Next Steps</span></span>
<span data-ttu-id="0d702-156">Web hizmetleri kullanma ile ilgili daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="0d702-156">For more information on consuming web services, see:</span></span>

[<span data-ttu-id="0d702-157">Nasıl tooconsume bir Azure Machine Learning Web hizmeti</span><span class="sxs-lookup"><span data-stu-id="0d702-157">How tooconsume an Azure Machine Learning Web service</span></span>](machine-learning-consume-web-services.md)

[<span data-ttu-id="0d702-158">Azure Machine Learning Web Hizmetleri: Dağıtım ve kullanım</span><span class="sxs-lookup"><span data-stu-id="0d702-158">Azure Machine Learning Web Services: Deployment and consumption</span></span>](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->
