---
title: "toomanage AzureML web hizmetleri API Management kullanarak nasıl aaaLearn | Microsoft Docs"
description: "Toomanage AzureML web API Management kullanarak hizmetleri nasıl gösteren bir kılavuzdur."
keywords: "machine Learning, API Yönetimi"
services: machine-learning
documentationcenter: 
author: roalexan
manager: jhubbard
editor: 
ms.assetid: 05150ae1-5b6a-4d25-ac67-fb2f24a68e8d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/19/2017
ms.author: roalexan
ms.openlocfilehash: 6e764fbfd71be6cc908a1c8d3d8889969fc651a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-how-toomanage-azureml-web-services-using-api-management"></a><span data-ttu-id="7fbe4-104">Toomanage AzureML web API Management kullanarak hizmetleri nasıl öğrenin</span><span class="sxs-lookup"><span data-stu-id="7fbe4-104">Learn how toomanage AzureML web services using API Management</span></span>
## <a name="overview"></a><span data-ttu-id="7fbe4-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="7fbe4-105">Overview</span></span>
<span data-ttu-id="7fbe4-106">Bu kılavuz size nasıl gösterir tooquickly API Management toomanage AzureML web hizmetlerinizi kullanımına başlamanıza.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-106">This guide shows you how tooquickly get started using API Management toomanage your AzureML web services.</span></span>

## <a name="what-is-azure-api-management"></a><span data-ttu-id="7fbe4-107">Azure API Management nedir?</span><span class="sxs-lookup"><span data-stu-id="7fbe4-107">What is Azure API Management?</span></span>
<span data-ttu-id="7fbe4-108">Azure API Management REST API uç noktalarınızı kullanıcı erişimi, kullanım azaltma ve Pano izleme tanımlayarak yönetmenizi sağlayan bir Azure hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-108">Azure API Management is an Azure service that lets you manage your REST API endpoints by defining user access, usage throttling, and dashboard monitoring.</span></span> <span data-ttu-id="7fbe4-109">Tıklatın [burada](https://azure.microsoft.com/services/api-management/) Azure API Management hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-109">Click [here](https://azure.microsoft.com/services/api-management/) for details on Azure API Management.</span></span> <span data-ttu-id="7fbe4-110">Tıklatın [burada](../api-management/api-management-get-started.md) tooget Azure API Management ile çalışmaya nasıl üzerinde Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-110">Click [here](../api-management/api-management-get-started.md) for a guide on how tooget started with Azure API Management.</span></span> <span data-ttu-id="7fbe4-111">Bu kılavuz temel alır, bu diğer Kılavuzu, ürünler, geliştirici abonelikleri ve kullanım dashboarding oluşturma bildirim yapılandırmaları, fiyatlandırma katmanı, yanıt işleme, kullanıcı kimlik doğrulaması dahil olmak üzere daha fazla konuları kapsar.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-111">This other guide, which this guide is based on, covers more topics, including notification configurations, tier pricing, response handling, user authentication, creating products, developer subscriptions, and usage dashboarding.</span></span>

## <a name="what-is-azureml"></a><span data-ttu-id="7fbe4-112">AzureML nedir?</span><span class="sxs-lookup"><span data-stu-id="7fbe4-112">What is AzureML?</span></span>
<span data-ttu-id="7fbe4-113">AzureML tooeasily yapı sağlayan machine learning için bir Azure hizmetidir, dağıtmak ve Gelişmiş analiz çözümleri paylaşın.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-113">AzureML is an Azure service for machine learning that enables you tooeasily build, deploy, and share advanced analytics solutions.</span></span> <span data-ttu-id="7fbe4-114">Tıklatın [burada](https://azure.microsoft.com/services/machine-learning/) AzureML hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-114">Click [here](https://azure.microsoft.com/services/machine-learning/) for details on AzureML.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7fbe4-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7fbe4-115">Prerequisites</span></span>
<span data-ttu-id="7fbe4-116">toocomplete bu kılavuz, gerekir:</span><span class="sxs-lookup"><span data-stu-id="7fbe4-116">toocomplete this guide, you need:</span></span>

* <span data-ttu-id="7fbe4-117">Bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-117">An Azure account.</span></span> <span data-ttu-id="7fbe4-118">Bir Azure hesabınız yoksa tıklatın [burada](https://azure.microsoft.com/pricing/free-trial/) hakkında ayrıntılar için toocreate ücretsiz bir deneme hesabı.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-118">If you don’t have an Azure account, click [here](https://azure.microsoft.com/pricing/free-trial/) for details on how toocreate a free trial account.</span></span>
* <span data-ttu-id="7fbe4-119">AzureML hesaptır.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-119">An AzureML account.</span></span> <span data-ttu-id="7fbe4-120">AzureML hesabınız yoksa tıklatın [burada](https://studio.azureml.net/) hakkında ayrıntılar için toocreate ücretsiz bir deneme hesabı.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-120">If you don’t have an AzureML account, click [here](https://studio.azureml.net/) for details on how toocreate a free trial account.</span></span>
* <span data-ttu-id="7fbe4-121">Hello çalışma alanı, hizmet ve bir web hizmeti olarak dağıtılan bir AzureML deneme apı_key.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-121">hello workspace, service, and api_key for an AzureML experiment deployed as a web service.</span></span> <span data-ttu-id="7fbe4-122">Tıklatın [burada](machine-learning-create-experiment.md) nasıl toocreate bir AzureML denemeler hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-122">Click [here](machine-learning-create-experiment.md) for details on how toocreate an AzureML experiment.</span></span> <span data-ttu-id="7fbe4-123">Tıklatın [burada](machine-learning-publish-a-machine-learning-web-service.md) nasıl toodeploy bir AzureML denemeler bir web hizmeti olarak hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-123">Click [here](machine-learning-publish-a-machine-learning-web-service.md) for details on how toodeploy an AzureML experiment as a web service.</span></span> <span data-ttu-id="7fbe4-124">Alternatif olarak, ek A nasıl toocreate ve test basit AzureML deneyin ve bir web hizmeti olarak dağıtmak için yönergeler içerir.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-124">Alternately, Appendix A has instructions for how toocreate and test a simple AzureML experiment and deploy it as a web service.</span></span>

## <a name="create-an-api-management-instance"></a><span data-ttu-id="7fbe4-125">API Management örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="7fbe4-125">Create an API Management instance</span></span>
<span data-ttu-id="7fbe4-126">Aşağıdaki API Management toomanage kullanma hello AzureML web hizmetiniz adımlardır.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-126">Below are hello steps for using API Management toomanage your AzureML web service.</span></span> <span data-ttu-id="7fbe4-127">İlk olarak bir hizmet örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-127">First create a service instance.</span></span> <span data-ttu-id="7fbe4-128">İçinde toohello oturum [Klasik Portal](https://manage.windowsazure.com/) tıklatıp **yeni** > **uygulama hizmetleri** > **API Management**  >  **Oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-128">Log in toohello [Classic Portal](https://manage.windowsazure.com/) and click **New** > **App Services** > **API Management** > **Create**.</span></span>

![Örnek Oluştur](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

<span data-ttu-id="7fbe4-130">Benzersiz bir belirtin **URL**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-130">Specify a unique **URL**.</span></span> <span data-ttu-id="7fbe4-131">Bu kılavuzu kullanır **demoazureml** – toochoose bir şey farklı gerekir.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-131">This guide uses **demoazureml** – you will need toochoose something different.</span></span> <span data-ttu-id="7fbe4-132">İstenen hello seçin **abonelik** ve **bölge** hizmet Örneğiniz için.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-132">Choose hello desired **Subscription** and **Region** for your service instance.</span></span> <span data-ttu-id="7fbe4-133">Seçimlerinizi yaptıktan sonra hello İleri düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-133">After making your selections, click hello next button.</span></span>

![oluşturma-service-1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

<span data-ttu-id="7fbe4-135">Hello için bir değer belirtin **kuruluş adı**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-135">Specify a value for hello **Organization Name**.</span></span> <span data-ttu-id="7fbe4-136">Bu kılavuzu kullanır **demoazureml** – toochoose bir şey farklı gerekir.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-136">This guide uses **demoazureml** – you will need toochoose something different.</span></span> <span data-ttu-id="7fbe4-137">E-posta adresinizi hello **yönetici e-posta** alan.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-137">Enter your email address in hello **administrator e-mail** field.</span></span> <span data-ttu-id="7fbe4-138">Bu e-posta adresi hello API Management sisteminden gelen bildirimler için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-138">This email address is used for notifications from hello API Management system.</span></span>

![oluşturma-service-2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

<span data-ttu-id="7fbe4-140">Merhaba onay kutusunu toocreate hizmet örneğiniz'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-140">Click hello check box toocreate your service instance.</span></span> <span data-ttu-id="7fbe4-141">*Oluşturulan yeni bir hizmet toobe toothirty dakika kaplar*.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-141">*It takes up toothirty minutes for a new service toobe created*.</span></span>

## <a name="create-hello-api"></a><span data-ttu-id="7fbe4-142">Merhaba API'si oluşturma</span><span class="sxs-lookup"><span data-stu-id="7fbe4-142">Create hello API</span></span>
<span data-ttu-id="7fbe4-143">Merhaba hizmet örneği oluşturulduktan sonra sonraki adıma hello toocreate hello API'dır.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-143">Once hello service instance is created, hello next step is toocreate hello API.</span></span> <span data-ttu-id="7fbe4-144">Bir API, istemci uygulamasından çağrılabilen işlemler grubundan oluşur.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-144">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="7fbe4-145">API işlemleri yönlendirilirken tooexisting web hizmetleridir.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-145">API operations are proxied tooexisting web services.</span></span> <span data-ttu-id="7fbe4-146">Bu kılavuz API'leri AzureML RRS ve BES web Hizmetleri varolan bu proxy toohello oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-146">This guide creates APIs that proxy toohello existing AzureML RRS and BES web services.</span></span>

<span data-ttu-id="7fbe4-147">API oluşturulur ve hello Klasik Azure portalı erişilen hello API yayımcı portalında yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-147">APIs are created and configured from hello API publisher portal, which is accessed through hello Azure Classic Portal.</span></span> <span data-ttu-id="7fbe4-148">Hizmet örneği tooreach hello yayımcı portalı, seçin.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-148">tooreach hello publisher portal, select your service instance.</span></span>

![Select hizmet örneği](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

<span data-ttu-id="7fbe4-150">Tıklatın **Yönet** API Management hizmetiniz için Klasik Azure portalı hello içinde.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-150">Click **Manage** in hello Azure Classic Portal for your API Management service.</span></span>

![yönetme hizmeti](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

<span data-ttu-id="7fbe4-152">Tıklatın **API'leri** hello gelen **API Management** sol hello ve ardından menüsünde **API Ekle**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-152">Click **APIs** from hello **API Management** menu on hello left, and then click **Add API**.</span></span>

![API yönetimi menüsü](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

<span data-ttu-id="7fbe4-154">Tür **AzureML Demo API** hello olarak **Web API adı**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-154">Type **AzureML Demo API** as hello **Web API name**.</span></span> <span data-ttu-id="7fbe4-155">Tür **https://ussouthcentral.services.azureml.net** hello olarak **Web hizmeti URL'si**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-155">Type **https://ussouthcentral.services.azureml.net** as hello **Web service URL**.</span></span> <span data-ttu-id="7fbe4-156">Tür **azureml demo** hello olarak **Web API'si URL soneki**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-156">Type **azureml-demo** as hello **Web API URL suffix**.</span></span> <span data-ttu-id="7fbe4-157">Denetleme **HTTPS** hello olarak **Web API'si URL** düzeni.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-157">Check **HTTPS** as hello **Web API URL** scheme.</span></span> <span data-ttu-id="7fbe4-158">Seçin **Starter** olarak **ürünleri**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-158">Select **Starter** as **Products**.</span></span> <span data-ttu-id="7fbe4-159">Tamamlandığında tıklatarak **kaydetmek** toocreate hello API.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-159">When finished, click **Save** toocreate hello API.</span></span>

![Yeni-API Ekle](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-hello-operations"></a><span data-ttu-id="7fbe4-161">Merhaba işlemleri ekleme</span><span class="sxs-lookup"><span data-stu-id="7fbe4-161">Add hello operations</span></span>
<span data-ttu-id="7fbe4-162">Tıklatın **ekleme işlemi** tooadd operations toothis API.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-162">Click **Add operation** tooadd operations toothis API.</span></span>

![ekleme işlemi](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

<span data-ttu-id="7fbe4-164">Merhaba **yeni işlem** penceresinde görüntülenir ve hello **imza** sekmesi varsayılan olarak seçilir.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-164">hello **New operation** window will be displayed and hello **Signature** tab will be selected by default.</span></span>

## <a name="add-rrs-operation"></a><span data-ttu-id="7fbe4-165">RRS işlemi ekleyin</span><span class="sxs-lookup"><span data-stu-id="7fbe4-165">Add RRS Operation</span></span>
<span data-ttu-id="7fbe4-166">İlk hello AzureML RRS hizmeti için bir işlem oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-166">First create an operation for hello AzureML RRS service.</span></span> <span data-ttu-id="7fbe4-167">Seçin **POST** hello olarak **HTTP fiili**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-167">Select **POST** as hello **HTTP verb**.</span></span> <span data-ttu-id="7fbe4-168">Türü **/workspaces/ {çalışma} /services/ {hizmeti} / execute? api-version {apiversion} = & Ayrıntıları {ayrıntıları} =** hello olarak **URL şablon**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-168">Type **/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}** as hello **URL template**.</span></span> <span data-ttu-id="7fbe4-169">Tür **RRS yürütme** hello olarak **görünen adı**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-169">Type **RRS Execute** as hello **Display name**.</span></span>

![rrs-işlemi-imza ekle](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

<span data-ttu-id="7fbe4-171">Tıklatın **yanıtları** > **ekleme** hello seçin ve sol üzerinde **200 Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-171">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="7fbe4-172">Tıklatın **kaydetmek** toosave bu işlemi.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-172">Click **Save** toosave this operation.</span></span>

![Add-rrs işlemi-yanıt](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a><span data-ttu-id="7fbe4-174">BES işlemleri ekleme</span><span class="sxs-lookup"><span data-stu-id="7fbe4-174">Add BES Operations</span></span>
<span data-ttu-id="7fbe4-175">Ekran görüntüleri için dahil olmayan hello RR işlemi eklemek için çok benzer toothose oldukları gibi BES işlemleri hello.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-175">Screenshots are not included for hello BES operations as they are very similar toothose for adding hello RRS operation.</span></span>

### <a name="submit-but-not-start-a-batch-execution-job"></a><span data-ttu-id="7fbe4-176">Bir toplu iş yürütme iş gönderme (ancak başlatılmamasına)</span><span class="sxs-lookup"><span data-stu-id="7fbe4-176">Submit (but not start) a Batch Execution job</span></span>
<span data-ttu-id="7fbe4-177">Tıklatın **ekleme işlemi** tooadd hello AzureML BES işlemi toohello API.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-177">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="7fbe4-178">Seçin **POST** hello için **HTTP fiili**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-178">Select **POST** for hello **HTTP verb**.</span></span> <span data-ttu-id="7fbe4-179">Türü **/workspaces/ {çalışma} /services/ {hizmeti} / işleri? api-version = {apiversion}** hello için **URL şablon**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-179">Type **/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="7fbe4-180">Tür **BES gönderme** hello için **görünen adı**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-180">Type **BES Submit** for hello **Display name**.</span></span> <span data-ttu-id="7fbe4-181">Tıklatın **yanıtları** > **ekleme** hello seçin ve sol üzerinde **200 Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-181">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="7fbe4-182">Tıklatın **kaydetmek** toosave bu işlemi.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-182">Click **Save** toosave this operation.</span></span>

### <a name="start-a-batch-execution-job"></a><span data-ttu-id="7fbe4-183">Bir toplu iş yürütme işi Başlat</span><span class="sxs-lookup"><span data-stu-id="7fbe4-183">Start a Batch Execution job</span></span>
<span data-ttu-id="7fbe4-184">Tıklatın **ekleme işlemi** tooadd hello AzureML BES işlemi toohello API.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-184">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="7fbe4-185">Seçin **POST** hello için **HTTP fiili**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-185">Select **POST** for hello **HTTP verb**.</span></span> <span data-ttu-id="7fbe4-186">Türü **/workspaces/ {çalışma} /services/ {hizmeti} /jobs/ {JobId} / start? api-version = {apiversion}** hello için **URL şablon**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-186">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="7fbe4-187">Tür **BES Başlat** hello için **görünen adı**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-187">Type **BES Start** for hello **Display name**.</span></span> <span data-ttu-id="7fbe4-188">Tıklatın **yanıtları** > **ekleme** hello seçin ve sol üzerinde **200 Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-188">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="7fbe4-189">Tıklatın **kaydetmek** toosave bu işlemi.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-189">Click **Save** toosave this operation.</span></span>

### <a name="get-hello-status-or-result-of-a-batch-execution-job"></a><span data-ttu-id="7fbe4-190">Merhaba durum ya da bir toplu iş yürütme iş sonucu alın</span><span class="sxs-lookup"><span data-stu-id="7fbe4-190">Get hello status or result of a Batch Execution job</span></span>
<span data-ttu-id="7fbe4-191">Tıklatın **ekleme işlemi** tooadd hello AzureML BES işlemi toohello API.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-191">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="7fbe4-192">Seçin **almak** hello için **HTTP fiili**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-192">Select **GET** for hello **HTTP verb**.</span></span> <span data-ttu-id="7fbe4-193">Türü **/workspaces/ {çalışma} /services/ {hizmeti} /jobs/ {JobId}? api-version = {apiversion}** hello için **URL şablon**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-193">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="7fbe4-194">Tür **BES durum** hello için **görünen adı**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-194">Type **BES Status** for hello **Display name**.</span></span> <span data-ttu-id="7fbe4-195">Tıklatın **yanıtları** > **ekleme** hello seçin ve sol üzerinde **200 Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-195">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="7fbe4-196">Tıklatın **kaydetmek** toosave bu işlemi.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-196">Click **Save** toosave this operation.</span></span>

### <a name="delete-a-batch-execution-job"></a><span data-ttu-id="7fbe4-197">Bir toplu iş yürütme iş Sil</span><span class="sxs-lookup"><span data-stu-id="7fbe4-197">Delete a Batch Execution job</span></span>
<span data-ttu-id="7fbe4-198">Tıklatın **ekleme işlemi** tooadd hello AzureML BES işlemi toohello API.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-198">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="7fbe4-199">Seçin **silmek** hello için **HTTP fiili**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-199">Select **DELETE** for hello **HTTP verb**.</span></span> <span data-ttu-id="7fbe4-200">Türü **/workspaces/ {çalışma} /services/ {hizmeti} /jobs/ {JobId}? api-version = {apiversion}** hello için **URL şablon**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-200">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="7fbe4-201">Tür **BES silmek** hello için **görünen adı**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-201">Type **BES Delete** for hello **Display name**.</span></span> <span data-ttu-id="7fbe4-202">Tıklatın **yanıtları** > **ekleme** hello seçin ve sol üzerinde **200 Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-202">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="7fbe4-203">Tıklatın **kaydetmek** toosave bu işlemi.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-203">Click **Save** toosave this operation.</span></span>

## <a name="call-an-operation-from-hello-developer-portal"></a><span data-ttu-id="7fbe4-204">Merhaba Geliştirici Portalı ' bir işlem çağırma</span><span class="sxs-lookup"><span data-stu-id="7fbe4-204">Call an operation from hello Developer Portal</span></span>
<span data-ttu-id="7fbe4-205">İşlemler uygun şekilde tooview sağlayan doğrudan hello Geliştirici portalından çağrılabilir ve bir API'nin işlemlerini hello test edin.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-205">Operations can be called directly from hello Developer portal, which provides a convenient way tooview and test hello operations of an API.</span></span> <span data-ttu-id="7fbe4-206">Bu kılavuzu adımında, çağıracaktır hello **RRS yürütme** toohello eklendi yöntemi **AzureML Demo API**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-206">In this guide step you will call hello **RRS Execute** method that was added toohello **AzureML Demo API**.</span></span> <span data-ttu-id="7fbe4-207">Tıklatın **Geliştirici Portalı** hello hello menüden top hello Klasik Portal sağındaki.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-207">Click **Developer portal** from hello menu at hello top right of hello Classic Portal.</span></span>

![Geliştirici Portalı](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

<span data-ttu-id="7fbe4-209">Tıklatın **API'leri** hello üst menüsünden ve ardından **AzureML Demo API** toosee hello işlemleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-209">Click **APIs** from hello top menu, and then click **AzureML Demo API** toosee hello operations available.</span></span>

![demoazureml API](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

<span data-ttu-id="7fbe4-211">Seçin **RRS yürütme** hello işlemi için.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-211">Select **RRS Execute** for hello operation.</span></span> <span data-ttu-id="7fbe4-212">Tıklatın **deneyin**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-212">Click **Try It**.</span></span>

![try-BT](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

<span data-ttu-id="7fbe4-214">İstek parametreleri için yazın, **çalışma**, **hizmet**, **2.0** hello için **apiversion**, ve **true**hello için **ayrıntıları**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-214">For Request parameters, type your **workspace**,  **service**, **2.0** for hello **apiversion**, and  **true** for hello **details**.</span></span> <span data-ttu-id="7fbe4-215">Bulabilirsiniz, **çalışma** ve **hizmet** hello AzureML web hizmeti panosunda (bkz **Test hello web hizmeti** ek A içinde).</span><span class="sxs-lookup"><span data-stu-id="7fbe4-215">You can find your **workspace** and **service** in hello AzureML web service dashboard (see **Test hello web service** in Appendix A).</span></span>

<span data-ttu-id="7fbe4-216">İstek üstbilgilerini için tıklatın **Ekle üstbilgi** ve türü **Content-Type** ve **uygulama/json**, ardından **Ekle üstbilgi** ve türü **yetkilendirme** ve **taşıyıcı <YOUR AZUREML SERVICE API-KEY>** .</span><span class="sxs-lookup"><span data-stu-id="7fbe4-216">For Request headers, click **Add header** and type **Content-Type** and **application/json**, then click **Add header** and type **Authorization** and **Bearer <YOUR AZUREML SERVICE API-KEY>**.</span></span> <span data-ttu-id="7fbe4-217">Bulabilirsiniz, **API anahtarı** hello AzureML web hizmeti panosunda (bkz **Test hello web hizmeti** ek A içinde).</span><span class="sxs-lookup"><span data-stu-id="7fbe4-217">You can find your **api key** in hello AzureML web service dashboard (see **Test hello web service** in Appendix A).</span></span>

<span data-ttu-id="7fbe4-218">Tür **{"Girişler": {"input1": {"ColumnNames": "Değerlerini" ["Col2"]: [["Bu bir iyi günüdür"]]}}, "GlobalParameters": {}}** hello istek gövdesi için.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-218">Type **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}** for hello request body.</span></span>

![azureml demo API](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

<span data-ttu-id="7fbe4-220">Tıklatın **Gönder**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-220">Click **Send**.</span></span>

![Gönder](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

<span data-ttu-id="7fbe4-222">Bir işlem çağrıldıktan sonra hello Geliştirici Portalı hello görüntüler **istenen URL** hello arka uç hizmetinden hello **yanıt durumu**, hello **yanıt üstbilgilerini**, ve tüm **yanıt içeriği**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-222">After an operation is invoked, hello developer portal displays hello **Requested URL** from hello back-end service, hello **Response status**, hello **Response headers**, and any **Response content**.</span></span>

![yanıt durumu](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a><span data-ttu-id="7fbe4-224">Ek A - web hizmeti oluşturma ve basit bir AzureML test etme</span><span class="sxs-lookup"><span data-stu-id="7fbe4-224">Appendix A - Creating and testing a simple AzureML web service</span></span>
### <a name="creating-hello-experiment"></a><span data-ttu-id="7fbe4-225">Merhaba deneme oluşturma</span><span class="sxs-lookup"><span data-stu-id="7fbe4-225">Creating hello experiment</span></span>
<span data-ttu-id="7fbe4-226">Basit bir AzureML deneme oluşturma ve bir web hizmeti olarak dağıtma hello adımları aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-226">Below are hello steps for creating a simple AzureML experiment and deploying it as a web service.</span></span> <span data-ttu-id="7fbe4-227">Web hizmeti alır, rastgele metin sütunu giriş olarak hello ve bir tamsayı olarak temsil özellik kümesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-227">hello web service takes as input a column of arbitrary text and returns a set of features represented as integers.</span></span> <span data-ttu-id="7fbe4-228">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="7fbe4-228">For example:</span></span>

| <span data-ttu-id="7fbe4-229">Metin</span><span class="sxs-lookup"><span data-stu-id="7fbe4-229">Text</span></span> | <span data-ttu-id="7fbe4-230">Karma metin</span><span class="sxs-lookup"><span data-stu-id="7fbe4-230">Hashed Text</span></span> |
| --- | --- |
| <span data-ttu-id="7fbe4-231">Bu iyi bir günüdür</span><span class="sxs-lookup"><span data-stu-id="7fbe4-231">This is a good day</span></span> |<span data-ttu-id="7fbe4-232">1 1 2 2 0 2 0 1</span><span class="sxs-lookup"><span data-stu-id="7fbe4-232">1 1 2 2 0 2 0 1</span></span> |

<span data-ttu-id="7fbe4-233">İlk olarak, tercih ettiğiniz bir tarayıcı kullanarak gidin için: [https://studio.azureml.net/](https://studio.azureml.net/) ve, kimlik bilgileri toolog girin.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-233">First, using a browser of your choice, navigate to: [https://studio.azureml.net/](https://studio.azureml.net/) and enter your credentials toolog in.</span></span> <span data-ttu-id="7fbe4-234">Ardından, yeni bir boş deneme oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-234">Next, create a new blank experiment.</span></span>

![Arama deneme şablonları](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

<span data-ttu-id="7fbe4-236">Çok yeniden adlandırma**SimpleFeatureHashingExperiment**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-236">Rename it too**SimpleFeatureHashingExperiment**.</span></span> <span data-ttu-id="7fbe4-237">Genişletme **kaydedilen veri kümeleri** ve sürükleyin **Kitap incelemeleri Amazon gelen** denemenizi üzerine.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-237">Expand **Saved Datasets** and drag **Book Reviews from Amazon** onto your experiment.</span></span>

![Basit-özellik-karma-deneme](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

<span data-ttu-id="7fbe4-239">Genişletme **veri dönüştürme** ve **işleme** ve sürükleyin **Select Columns in Dataset sütun** denemenizi üzerine.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-239">Expand **Data Transformation** and **Manipulation** and drag **Select Columns in Dataset** onto your experiment.</span></span> <span data-ttu-id="7fbe4-240">Bağlantı **Kitap incelemeleri Amazon gelen** çok**Select Columns in Dataset sütun**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-240">Connect **Book Reviews from Amazon** too**Select Columns in Dataset**.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

<span data-ttu-id="7fbe4-242">Tıklatın **Select Columns in Dataset sütun** ve ardından **başlatma Sütun seçiciyi** seçip **Col2**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-242">Click **Select Columns in Dataset** and then click **Launch column selector** and select **Col2**.</span></span> <span data-ttu-id="7fbe4-243">Bu değişiklikler Hello onay işareti tooapply tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-243">Click hello checkmark tooapply these changes.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

<span data-ttu-id="7fbe4-245">Genişletme **metin analizi** ve sürükleyin **özellik karma** hello deneme üzerine.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-245">Expand **Text Analytics** and drag **Feature Hashing** onto hello experiment.</span></span> <span data-ttu-id="7fbe4-246">Bağlantı **Select Columns in Dataset sütun** çok**özellik karma**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-246">Connect **Select Columns in Dataset** too**Feature Hashing**.</span></span>

![Connect-proje-sütunlar](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

<span data-ttu-id="7fbe4-248">Tür **3** hello için **bitsize karma**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-248">Type **3** for hello **Hashing bitsize**.</span></span> <span data-ttu-id="7fbe4-249">Bu 8 (23) oluşturacak sütun.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-249">This will create 8 (23) columns.</span></span>

![karma bitsize](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

<span data-ttu-id="7fbe4-251">Bu noktada, tooclick isteyebilirsiniz **çalıştırmak** tootest hello deneme.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-251">At this point, you may want tooclick **Run** tootest hello experiment.</span></span>

![çalıştırma](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a><span data-ttu-id="7fbe4-253">Web hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="7fbe4-253">Create a web service</span></span>
<span data-ttu-id="7fbe4-254">Şimdi bir web hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-254">Now create a web service.</span></span> <span data-ttu-id="7fbe4-255">Genişletme **Web hizmeti** ve sürükleyin **giriş** denemenizi üzerine.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-255">Expand **Web Service** and drag **Input** onto your experiment.</span></span> <span data-ttu-id="7fbe4-256">Bağlantı **giriş** çok**özellik karma**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-256">Connect **Input** too**Feature Hashing**.</span></span> <span data-ttu-id="7fbe4-257">Ayrıca sürükleyin **çıkış** denemenizi üzerine.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-257">Also drag **output** onto your experiment.</span></span> <span data-ttu-id="7fbe4-258">Bağlantı **çıkış** çok**özellik karma**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-258">Connect **Output** too**Feature Hashing**.</span></span>

![Çıktı-için-özellik-karma](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

<span data-ttu-id="7fbe4-260">Tıklatın **web hizmeti yayımlama**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-260">Click **Publish web service**.</span></span>

![Yayımlama-web hizmeti](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

<span data-ttu-id="7fbe4-262">Tıklatın **Evet** toopublish hello deneme.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-262">Click **Yes** toopublish hello experiment.</span></span>

![Yayımlama Evet](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-hello-web-service"></a><span data-ttu-id="7fbe4-264">Test hello web hizmeti</span><span class="sxs-lookup"><span data-stu-id="7fbe4-264">Test hello web service</span></span>
<span data-ttu-id="7fbe4-265">AzureML web hizmeti RSS (istek/yanıt hizmeti) ve BES (toplu yürütme hizmeti) uç noktaları oluşur.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-265">An AzureML web service consists of RSS (request/response service) and BES (batch execution service) endpoints.</span></span> <span data-ttu-id="7fbe4-266">RSS için zaman uyumlu yürütme ' dir.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-266">RSS is for synchronous execution.</span></span> <span data-ttu-id="7fbe4-267">BES için zaman uyumsuz iş yürütme ' dir.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-267">BES is for asynchronous job execution.</span></span> <span data-ttu-id="7fbe4-268">web hizmeti hello örnek Python kaynağı ile aşağıdaki tootest ihtiyacınız olabilecek toodownload ve yükleme hello Azure SDK'sı için Python (bkz: [nasıl tooinstall Python](../python-how-to-install.md)).</span><span class="sxs-lookup"><span data-stu-id="7fbe4-268">tootest your web service with hello sample Python source below, you may need toodownload and install hello Azure SDK for Python (see: [How tooinstall Python](../python-how-to-install.md)).</span></span>

<span data-ttu-id="7fbe4-269">Merhaba de gerekir **çalışma**, **hizmet**, ve **apı_key** denemenizi hello örnek kaynağı için.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-269">You will also need hello **workspace**, **service**, and **api_key** of your experiment for hello sample source below.</span></span> <span data-ttu-id="7fbe4-270">Ya da tıklatarak hello çalışma ve hizmet bulabilirsiniz **istek/yanıt** veya **toplu iş yürütme** hello web hizmeti panosunda denemeniz için.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-270">You can find hello workspace and service by clicking either **Request/Response** or **Batch Execution** for your experiment in hello web service dashboard.</span></span>

![Bul çalışma-ve-hizmet](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

<span data-ttu-id="7fbe4-272">Merhaba bulabilirsiniz **apı_key** denemenizi hello web hizmeti panosunda tıklatarak.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-272">You can find hello **api_key** by clicking your experiment in hello web service dashboard.</span></span>

![Bul API anahtarı](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a><span data-ttu-id="7fbe4-274">Test RRS uç noktası</span><span class="sxs-lookup"><span data-stu-id="7fbe4-274">Test RRS endpoint</span></span>
##### <a name="test-button"></a><span data-ttu-id="7fbe4-275">Test düğmesi</span><span class="sxs-lookup"><span data-stu-id="7fbe4-275">Test button</span></span>
<span data-ttu-id="7fbe4-276">Tooclick bir kolay bir yolu tootest hello RR uç noktadır **Test** hello web hizmeti panosundaki.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-276">An easy way tootest hello RRS endpoint is tooclick **Test** on hello web service dashboard.</span></span>

![test etme](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

<span data-ttu-id="7fbe4-278">Tür **bu iyi bir günüdür** için **col2**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-278">Type **This is a good day** for **col2**.</span></span> <span data-ttu-id="7fbe4-279">Merhaba onay işaretine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-279">Click hello checkmark.</span></span>

![veri girme](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

<span data-ttu-id="7fbe4-281">Şöyle görürsünüz</span><span class="sxs-lookup"><span data-stu-id="7fbe4-281">You will see something like</span></span>

![örnek çıktı](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a><span data-ttu-id="7fbe4-283">Örnek kod</span><span class="sxs-lookup"><span data-stu-id="7fbe4-283">Sample Code</span></span>
<span data-ttu-id="7fbe4-284">Başka bir şekilde tootest, RRS istemci kodunuzdan ' dir.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-284">Another way tootest your RRS is from your client code.</span></span> <span data-ttu-id="7fbe4-285">Tıklatırsanız **istek/yanıt** hello Pano ve kaydırma toohello altta, örnek kod C#, Python ve r görürsünüz Merhaba sözdizimi hello RRS isteği hello isteğin URI, üst bilgiler ve gövde dahil olmak üzere, ayrıca görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-285">If you click **Request/response** on hello dashboard and scroll toohello bottom, you will see sample code for C#, Python, and R. You will also see hello syntax of hello RRS request, including hello request URI, headers, and body.</span></span>

<span data-ttu-id="7fbe4-286">Bu kılavuz, çalışan bir Python örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-286">This guide shows a working Python example.</span></span> <span data-ttu-id="7fbe4-287">Toomodify gerekir hello ile **çalışma**, **hizmet**, ve **apı_key** denemenizi biri.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-287">You will need toomodify it with hello **workspace**, **service**, and **api_key** of your experiment.</span></span>

    import urllib2
    import json
    workspace = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE WORKSPACE ID>"
    service = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE SERVICE ID>"
    api_key = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE API KEY>"
    data = {
    "Inputs": {
        "input1": {
            "ColumnNames": ["Col2"],
            "Values": [ [ "This is a good day" ] ]
        },
    },
    "GlobalParameters": { }
    }
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace + "/services/" + service + "/execute?api-version=2.0&details=true"
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}
    body = str.encode(json.dumps(data))
    try:
        req = urllib2.Request(url, body, headers)
        response = urllib2.urlopen(req)
        result = response.read()
        print "result:" + result
            except urllib2.HTTPError, error:
        print("hello request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a><span data-ttu-id="7fbe4-288">Test BES uç noktası</span><span class="sxs-lookup"><span data-stu-id="7fbe4-288">Test BES endpoint</span></span>
<span data-ttu-id="7fbe4-289">Tıklatın **toplu yürütme** altta hello Pano ve kaydırma toohello.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-289">Click **Batch execution** on hello dashboard and scroll toohello bottom.</span></span> <span data-ttu-id="7fbe4-290">C#, Python ve r için örnek kod görürsünüz Ayrıca, BES istekleri toosubmit bir işi Merhaba, bir işi başlatmak, hello durumu veya bir iş sonuçlarını almak ve bir işi silmek hello sözdizimi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-290">You will see sample code for C#, Python, and R. You will also see hello syntax of hello BES requests toosubmit a job, start a job, get hello status or results of a job, and delete a job.</span></span>

<span data-ttu-id="7fbe4-291">Bu kılavuz, çalışan bir Python örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-291">This guide shows a working Python example.</span></span> <span data-ttu-id="7fbe4-292">Toomodify ihtiyacınız hello ile **çalışma**, **hizmet**, ve **apı_key** denemenizi biri.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-292">You need toomodify it with hello **workspace**, **service**, and **api_key** of your experiment.</span></span> <span data-ttu-id="7fbe4-293">Ayrıca, toomodify hello ihtiyacınız **depolama hesabı adı**, **depolama hesabı anahtarı**, ve **depolama kapsayıcısı adı**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-293">Additionally, you need toomodify hello **storage account name**, **storage account key**, and **storage container name**.</span></span> <span data-ttu-id="7fbe4-294">Son olarak, toomodify hello hello konumunu gerekir **giriş dosyası** ve hello hello konumunu **çıktı dosyası**.</span><span class="sxs-lookup"><span data-stu-id="7fbe4-294">Lastly, you will need toomodify hello location of hello **input file** and hello location of hello **output file**.</span></span>

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH hello API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH hello LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH hello LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("hello request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading hello result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written toohello file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("hello results for " + outputName + " are available at hello following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "hello results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading hello input tooblob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded hello input tooblob storage"
    input_blob_path = "/" + storage_container_name + "/" + input_blob_name
    connection_string = "DefaultEndpointsProtocol=https;AccountName=" + storage_account_name + ";AccountKey=" + storage_account_key
    payload =  {
        "Input": {
            "ConnectionString": connection_string,
            "RelativeLocation": input_blob_path
        },
        "Outputs": {
            "output1": { "ConnectionString": connection_string, "RelativeLocation": "/" + storage_container_name + "/" + output_blob_name },
        },
        "GlobalParameters": {
        }
    }
        body = str.encode(json.dumps(payload))
    headers = { "Content-Type":"application/json", "Authorization":("Bearer " + api_key)}
    print("Submitting hello job...")
    # submit hello job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove hello enclosing double-quotes
    print("Job ID: " + job_id)
    # start hello job
    print("Starting hello job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking hello job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in hello follwing code
        req = urllib2.Request(url2, headers = { "Authorization":("Bearer " + api_key) })
        try:
            response = urllib2.urlopen(req)
        except urllib2.HTTPError, error:
            printHttpError(error)
            return
        result = json.loads(response.read())
        status = result["StatusCode"]
        print "status:" + status
        if (status == 0 or status == "NotStarted"):
            print("Job " + job_id + " not yet started...")
        elif (status == 1 or status == "Running"):
            print("Job " + job_id + " running...")
        elif (status == 2 or status == "Failed"):
            print("Job " + job_id + " failed!")
            print("Error details: " + result["Details"])
            break
        elif (status == 3 or status == "Cancelled"):
            print("Job " + job_id + " cancelled!")
            break
        elif (status == 4 or status == "Finished"):
            print("Job " + job_id + " finished!")
            processResults(result)
            break
        time.sleep(1) # wait one second
    return
    invokeBatchExecutionService()
