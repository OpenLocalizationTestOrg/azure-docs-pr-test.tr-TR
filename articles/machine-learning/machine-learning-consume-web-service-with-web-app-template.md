---
title: "bir Machine Learning web hizmeti bir web uygulaması şablonu aaaConsume | Microsoft Docs"
description: "Azure Market tooconsume Azure Machine Learning Tahmine dayalı web hizmetinde bir web uygulaması şablonu kullanın."
keywords: "Web hizmeti, operationalization, REST API makine öğrenme"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e0d71683-61b9-4675-8df5-09ddc2f0d92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;raymondl
ms.openlocfilehash: 1199377bead470807d58ca7f7a667175cbb88450
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a><span data-ttu-id="f79eb-104">Bir Azure Machine Learning web hizmetini web uygulaması şablonu ile kullanma</span><span class="sxs-lookup"><span data-stu-id="f79eb-104">Consume an Azure Machine Learning web service with a web app template</span></span>

<span data-ttu-id="f79eb-105">Bir kez artık Tahmine dayalı modelde geliştirilen ve Machine Learning Studio kullanarak bir Azure web hizmeti dağıtılmış veya R veya Python gibi araçları kullanarak, bir REST API kullanarak hello kullanıma hazır hale getirilmiş modeli erişebilir.</span><span class="sxs-lookup"><span data-stu-id="f79eb-105">Once you've developed your predictive model and deployed it as an Azure web service using Machine Learning Studio, or using tools such as R or Python, you can access hello operationalized model using a REST API.</span></span>

<span data-ttu-id="f79eb-106">Tooconsume hello REST API ve erişim hello web hizmetini birkaç yolla vardır.</span><span class="sxs-lookup"><span data-stu-id="f79eb-106">There are a number of ways tooconsume hello REST API and access hello web service.</span></span> <span data-ttu-id="f79eb-107">Örneğin, bir uygulama C# ' ta R, yazabilirsiniz veya Python hello kullanarak örnek hello web hizmetini dağıttığınızda sizin için oluşturulan kod (Merhaba bulunan [Machine Learning Web Hizmetleri portalı](https://services.azureml.net/quickstart) veya hello web hizmeti panosunda Machine Learning Studio).</span><span class="sxs-lookup"><span data-stu-id="f79eb-107">For example, you can write an application in C#, R, or Python using hello sample code generated for you when you deployed hello web service (available in hello [Machine Learning Web Services Portal](https://services.azureml.net/quickstart) or in hello web service dashboard in Machine Learning Studio).</span></span> <span data-ttu-id="f79eb-108">Veya hello örnek Microsoft Excel çalışma kitabı hello sırasında oluşturduğunuz kullanabilirsiniz aynı anda.</span><span class="sxs-lookup"><span data-stu-id="f79eb-108">Or you can use hello sample Microsoft Excel workbook created for you at hello same time.</span></span>

<span data-ttu-id="f79eb-109">Ancak, web hizmetinin çalıştığı hello Web Uygulama Şablonları hello kullanılabilir aracılığıyla hızlı ve kolay bir yol tooaccess hello [Azure Web uygulaması Market](https://azure.microsoft.com/marketplace/web-applications/all/).</span><span class="sxs-lookup"><span data-stu-id="f79eb-109">But hello quickest and easiest way tooaccess your web service is through hello Web App Templates available in hello [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-azure-machine-learning-web-app-templates"></a><span data-ttu-id="f79eb-110">Hello Azure Machine Learning Web Uygulama Şablonları</span><span class="sxs-lookup"><span data-stu-id="f79eb-110">hello Azure Machine Learning Web App Templates</span></span>
<span data-ttu-id="f79eb-111">Merhaba web uygulama şablonları hello Azure Marketi kullanılabilir web hizmetinizin giriş verilerini ve beklenen sonuçları bildiği bir özel web uygulaması oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f79eb-111">hello web app templates available in hello Azure Marketplace can build a custom web app that knows your web service's input data and expected results.</span></span> <span data-ttu-id="f79eb-112">Toodo gereken tek şey hello web uygulama erişim tooyour web hizmeti ve veri verin ve hello şablon rest hello.</span><span class="sxs-lookup"><span data-stu-id="f79eb-112">All you need toodo is give hello web app access tooyour web service and data, and hello template does hello rest.</span></span>

<span data-ttu-id="f79eb-113">İki şablonlar kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="f79eb-113">Two templates are available:</span></span>

* [<span data-ttu-id="f79eb-114">Azure ML istek-yanıt hizmeti Web uygulaması şablonu</span><span class="sxs-lookup"><span data-stu-id="f79eb-114">Azure ML Request-Response Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [<span data-ttu-id="f79eb-115">Azure ML toplu iş yürütme hizmeti Web uygulaması şablonu</span><span class="sxs-lookup"><span data-stu-id="f79eb-115">Azure ML Batch Execution Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

<span data-ttu-id="f79eb-116">Her bir şablon web hizmetiniz için hello API URI ve anahtarı kullanarak bir örnek ASP.NET uygulaması oluşturur ve bir web sitesi tooAzure dağıtır.</span><span class="sxs-lookup"><span data-stu-id="f79eb-116">Each template creates a sample ASP.NET application, using hello API URI and Key for your web service, and deploys it as a web site tooAzure.</span></span> <span data-ttu-id="f79eb-117">Merhaba istek-yanıt hizmeti (RRS) şablonu toosend veri toohello web hizmeti tooget tek bir sonuç tek bir satır sağlayan bir web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f79eb-117">hello Request-Response Service (RRS) template creates a web app that allows you toosend a single row of data toohello web service tooget a single result.</span></span> <span data-ttu-id="f79eb-118">Merhaba toplu yürütme hizmeti (BES) şablonu oluşturur toosend sağlayan bir web uygulaması verileri tooget çok sayıda satırı birden çok sonuç.</span><span class="sxs-lookup"><span data-stu-id="f79eb-118">hello Batch Execution Service (BES) template creates a web app that allows you toosend many rows of data tooget multiple results.</span></span>

<span data-ttu-id="f79eb-119">Hiçbir kodlama Bu şablonlar gerekli toouse değil.</span><span class="sxs-lookup"><span data-stu-id="f79eb-119">No coding is required toouse these templates.</span></span> <span data-ttu-id="f79eb-120">Yalnızca hello API anahtarı ve URI sağlayın ve hello şablon hello uygulamayı sizin için oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f79eb-120">You just supply hello API Key and URI, and hello template builds hello application for you.</span></span>

<span data-ttu-id="f79eb-121">tooget hello API anahtarı ve bir web hizmeti için istek URI'si:</span><span class="sxs-lookup"><span data-stu-id="f79eb-121">tooget hello API key and Request URI for a web service:</span></span>

1. <span data-ttu-id="f79eb-122">Merhaba, [Web Hizmetleri portalı](https://services.azureml.net/quickstart), yeni bir web hizmeti için tıklatın **Web Hizmetleri** hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="f79eb-122">In hello [Web Services Portal](https://services.azureml.net/quickstart), for a New web service, click **Web Services** at hello top.</span></span> <span data-ttu-id="f79eb-123">Veya bir Klasik web hizmeti tıklatın **Klasik Web Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="f79eb-123">Or for a Classic web service click **Classic Web Services**.</span></span>
2. <span data-ttu-id="f79eb-124">Merhaba web hizmeti tooaccess istediğiniz'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f79eb-124">Click hello web service you want tooaccess.</span></span>
3. <span data-ttu-id="f79eb-125">Klasik web hizmeti, tooaccess istediğiniz hello uç noktası'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f79eb-125">For a Classic web service, click hello endpoint you want tooaccess.</span></span>
4. <span data-ttu-id="f79eb-126">Tıklatın **Tüket** hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="f79eb-126">Click **Consume** at hello top.</span></span>
5. <span data-ttu-id="f79eb-127">Kopya hello **birincil** veya **ikincil anahtar** ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f79eb-127">Copy hello **Primary** or **Secondary Key** and save it.</span></span>
6. <span data-ttu-id="f79eb-128">İstek-yanıt hizmeti (RRS) şablonu oluşturuyorsanız, hello kopyalama **istek-yanıt** URI ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f79eb-128">If you're creating a Request-Response Service (RRS) template, copy hello **Request-Response** URI and save it.</span></span> <span data-ttu-id="f79eb-129">Bir toplu iş yürütme hizmeti (BES) şablonu oluşturuyorsanız, hello kopyalama **toplu istekleri** URI ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f79eb-129">If you're creating a Batch Execution Service (BES) template, copy hello **Batch Requests** URI and save it.</span></span>


## <a name="how-toouse-hello-request-response-service-rrs-template"></a><span data-ttu-id="f79eb-130">Nasıl toouse hello istek-yanıt hizmeti (RRS) şablonu</span><span class="sxs-lookup"><span data-stu-id="f79eb-130">How toouse hello Request-Response Service (RRS) template</span></span>
<span data-ttu-id="f79eb-131">Bu adımları toouse hello RR web uygulaması şablonu, hello Aşağıdaki diyagramda gösterildiği gibi izleyin.</span><span class="sxs-lookup"><span data-stu-id="f79eb-131">Follow these steps toouse hello RRS web app template, as shown in hello following diagram.</span></span>

![İşlem toouse RRS web şablonu][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. <span data-ttu-id="f79eb-133">Toohello Git [Azure portal](https://portal.azure.com), **oturum açma**, tıklatın **yeni**, aramak ve seçmek **Azure ML istek-yanıt hizmeti Web uygulaması**,'ye tıklayın **Oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="f79eb-133">Go toohello [Azure portal](https://portal.azure.com), **Login**, click **New**, search for and select **Azure ML Request-Response Service Web App**, then click **Create**.</span></span> 
   
   * <span data-ttu-id="f79eb-134">Web uygulamanızı benzersiz bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="f79eb-134">Give your web app a unique name.</span></span> <span data-ttu-id="f79eb-135">Merhaba hello web uygulamasının URL'sini ve ardından bu ad olacaktır `.azurewebsites.net.` Örneğin,`http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="f79eb-135">hello URL of hello web app will be this name followed by `.azurewebsites.net.` For example, `http://carprediction.azurewebsites.net.`</span></span>
   * <span data-ttu-id="f79eb-136">Web hizmetiniz altında çalıştığı Hello Azure aboneliği ve hizmetleri seçin.</span><span class="sxs-lookup"><span data-stu-id="f79eb-136">Select hello Azure subscription and services under which your web service is running.</span></span>
   * <span data-ttu-id="f79eb-137">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f79eb-137">Click **Create**.</span></span>
     
     ![Web uygulaması oluşturma][image5]

4. <span data-ttu-id="f79eb-139">Azure hello web uygulamasına dağıtmayı bitirdiğinde, hello tıklatın **URL** hello Azure web uygulaması Ayarları sayfasında, veya bir web tarayıcısında hello URL'sini girin.</span><span class="sxs-lookup"><span data-stu-id="f79eb-139">When Azure has finished deploying hello web app, click hello **URL** on hello web app settings page in Azure, or enter hello URL in a web browser.</span></span> <span data-ttu-id="f79eb-140">Örneğin, `http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="f79eb-140">For example, `http://carprediction.azurewebsites.net.`</span></span>
5. <span data-ttu-id="f79eb-141">Web uygulaması ilk çalışır, sorar Merhaba'ne zaman hello **API gönderme URL'sini** ve **API anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="f79eb-141">When hello web app first runs it will ask you for hello **API Post URL** and **API Key**.</span></span>
   <span data-ttu-id="f79eb-142">Daha önce kaydettiğiniz hello değerleri girin (**istek URI'si** ve **API anahtarı**sırasıyla).</span><span class="sxs-lookup"><span data-stu-id="f79eb-142">Enter hello values you saved earlier (**Request URI** and **API Key**, respectively).</span></span>
     
     <span data-ttu-id="f79eb-143">Tıklatın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="f79eb-143">Click **Submit**.</span></span>
     
     ![POST URI ve API anahtarını girin][image6]

6. <span data-ttu-id="f79eb-145">web uygulaması görüntüler Hello kendi **Web Uygulama Yapılandırması** hello geçerli web hizmeti ayarları sayfası.</span><span class="sxs-lookup"><span data-stu-id="f79eb-145">hello web app displays its **Web App Configuration** page with hello current web service settings.</span></span> <span data-ttu-id="f79eb-146">Burada hello web uygulaması tarafından kullanılan toohello ayarlarını değişiklik yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f79eb-146">Here you can make changes toohello settings used by hello web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f79eb-147">Burada Hello ayarlarını değiştirdiğinizde yalnızca bunları bu web uygulaması için değişir.</span><span class="sxs-lookup"><span data-stu-id="f79eb-147">Changing hello settings here only changes them for this web app.</span></span> <span data-ttu-id="f79eb-148">Web hizmetinizin hello varsayılan ayarları değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="f79eb-148">It doesn't change hello default settings of your web service.</span></span> <span data-ttu-id="f79eb-149">Örneğin, hello değiştirirseniz **açıklama** burada hello web hizmeti panosundaki Machine Learning Studio'da gösterilen hello açıklama değişmez.</span><span class="sxs-lookup"><span data-stu-id="f79eb-149">For example, if you change hello **Description** here it doesn't change hello description shown on hello web service dashboard in Machine Learning Studio.</span></span>
   > 
   > 
   
    <span data-ttu-id="f79eb-150">İşiniz bittiğinde tıklatın **değişiklikleri kaydetmek**ve ardından **tooHome sayfa Git**.</span><span class="sxs-lookup"><span data-stu-id="f79eb-150">When you're done, click **Save changes**, and then click **Go tooHome Page**.</span></span>

7. <span data-ttu-id="f79eb-151">Hello toosend tooyour web hizmeti giriş sayfasına girdiğiniz değerleri.</span><span class="sxs-lookup"><span data-stu-id="f79eb-151">From hello home page you can enter values toosend tooyour web service.</span></span> <span data-ttu-id="f79eb-152">Tıklatın **gönderme** zaman işiniz bittiğinde ve hello sonuç döndürülecek.</span><span class="sxs-lookup"><span data-stu-id="f79eb-152">Click **Submit** when you're done, and hello result will be returned.</span></span>

<span data-ttu-id="f79eb-153">Tooreturn toohello istiyorsanız **yapılandırma** sayfasında, Git toohello `setting.aspx` hello web uygulaması sayfasında.</span><span class="sxs-lookup"><span data-stu-id="f79eb-153">If you want tooreturn toohello **Configuration** page, go toohello `setting.aspx` page of hello web app.</span></span> <span data-ttu-id="f79eb-154">Örneğin: `http://carprediction.azurewebsites.net/setting.aspx.` istendiğinde tooenter hello API anahtarı yeniden olacaktır - tooaccess hello sayfa ve hello ayarları güncelleştirme gerekir.</span><span class="sxs-lookup"><span data-stu-id="f79eb-154">For example: `http://carprediction.azurewebsites.net/setting.aspx.` You will be prompted tooenter hello API key again - you need that tooaccess hello page and update hello settings.</span></span>

<span data-ttu-id="f79eb-155">Durdurmak, yeniden başlatın veya hello Azure portal başka bir web uygulaması gibi hello web uygulamasında silin.</span><span class="sxs-lookup"><span data-stu-id="f79eb-155">You can stop, restart, or delete hello web app in hello Azure portal like any other web app.</span></span> <span data-ttu-id="f79eb-156">Çalıştığı sürece toohello ev web adresini göz atın ve yeni değerler girin.</span><span class="sxs-lookup"><span data-stu-id="f79eb-156">As long as it is running you can browse toohello home web address and enter new values.</span></span>

## <a name="how-toouse-hello-batch-execution-service-bes-template"></a><span data-ttu-id="f79eb-157">Nasıl toouse hello toplu yürütme hizmeti (BES) şablonu</span><span class="sxs-lookup"><span data-stu-id="f79eb-157">How toouse hello Batch Execution Service (BES) template</span></span>
<span data-ttu-id="f79eb-158">Merhaba BES kullanabilirsiniz hello aynı şekilde hello RR şablon olarak dışında oluşturulan bu hello web uygulaması web uygulaması şablonu etmenizi sağlar toosubmit verilerin birden çok satır ve birden çok sonuç alırsınız.</span><span class="sxs-lookup"><span data-stu-id="f79eb-158">You can use hello BES web app template in hello same way as hello RRS template, except that hello web app that's created will allow you toosubmit multiple rows of data and receive multiple results.</span></span>

<span data-ttu-id="f79eb-159">bir toplu iş yürütme web hizmeti için giriş değerleri Hello Azure depolama veya bir yerel dosya gelebilir; Merhaba sonuçları bir Azure depolama kapsayıcısında depolanır.</span><span class="sxs-lookup"><span data-stu-id="f79eb-159">hello input values for a batch execution web service can come from Azure storage or a local file; hello results are stored in an Azure storage container.</span></span>
<span data-ttu-id="f79eb-160">Bu nedenle, artıracaksınız bir Azure depolama kapsayıcısı toohold hello web uygulaması tarafından döndürülen sonuçları hello ve tooget giriş verilerinizi hazır olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f79eb-160">So, you'll need an Azure storage container toohold hello results returned by hello web app, and you'll need tooget your input data ready.</span></span>

![Toouse BES işlem web şablonu][image2]

1. <span data-ttu-id="f79eb-162">İzleme hello aynı yordamı toocreate hello BES web uygulaması Git dışında hello RR şablonu için olduğu gibi çok[Azure ML toplu iş yürütme hizmeti Web uygulaması şablonu](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen Azure Marketi BES şablona hello ve tıklayın **Web uygulaması oluşturma** .</span><span class="sxs-lookup"><span data-stu-id="f79eb-162">Follow hello same procedure toocreate hello BES web app as for hello RRS template, except go too[Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen hello BES template on Azure Marketplace and click **Create Web App**.</span></span>

2. <span data-ttu-id="f79eb-163">saklı hello sonuçları istediğiniz toospecify hello web uygulama giriş sayfasında hello hedef kapsayıcı bilgileri girin.</span><span class="sxs-lookup"><span data-stu-id="f79eb-163">toospecify where you want hello results stored, enter hello destination container information on hello web app home page.</span></span> <span data-ttu-id="f79eb-164">Ayrıca, başlangıç web uygulaması hello giriş değerleri, yerel bir dosya veya bir Azure depolama kapsayıcısı nereden belirtin.</span><span class="sxs-lookup"><span data-stu-id="f79eb-164">Also specify where hello web app can get hello input values, either in a local file or an Azure storage container.</span></span>
   <span data-ttu-id="f79eb-165">Tıklatın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="f79eb-165">Click **Submit**.</span></span>
   
    ![Depolama birimi bilgileri][image7]

<span data-ttu-id="f79eb-167">Merhaba web uygulaması iş durumunu içeren bir sayfa görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f79eb-167">hello web app will display a page with job status.</span></span>
<span data-ttu-id="f79eb-168">Hello iş tamamlandığında hello sonuçları Azure blob depolama alanındaki hello konumunu verilmesi.</span><span class="sxs-lookup"><span data-stu-id="f79eb-168">When hello job has completed you'll be given hello location of hello results in Azure blob storage.</span></span> <span data-ttu-id="f79eb-169">Merhaba sonuçları tooa yerel dosya indirilmesi hello seçeneğiniz de vardır.</span><span class="sxs-lookup"><span data-stu-id="f79eb-169">You also have hello option of downloading hello results tooa local file.</span></span>

## <a name="for-more-information"></a><span data-ttu-id="f79eb-170">Daha fazla bilgi için</span><span class="sxs-lookup"><span data-stu-id="f79eb-170">For more information</span></span>
<span data-ttu-id="f79eb-171">toolearn hakkında daha fazla bilgi...</span><span class="sxs-lookup"><span data-stu-id="f79eb-171">toolearn more about...</span></span>

* <span data-ttu-id="f79eb-172">machine learning denemeyi Machine Learning Studio ile bkz [Azure Machine Learning Studio'da ilk denemenizi oluşturma](machine-learning-create-experiment.md)</span><span class="sxs-lookup"><span data-stu-id="f79eb-172">creating a machine learning experiment with Machine Learning Studio, see [Create your first experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md)</span></span>
* <span data-ttu-id="f79eb-173">machine learning web hizmeti olarak denemeler toodeploy nasıl görürüm [bir Azure Machine Learning web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md)</span><span class="sxs-lookup"><span data-stu-id="f79eb-173">how toodeploy your machine learning experiment as a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md)</span></span>
* <span data-ttu-id="f79eb-174">diğer yolları tooaccess web hizmetiniz bkz [nasıl tooconsume bir Azure Machine Learning Web hizmeti](machine-learning-consume-web-services.md)</span><span class="sxs-lookup"><span data-stu-id="f79eb-174">other ways tooaccess your web service, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md)</span></span>

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
