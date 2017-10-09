---
title: "U-SQL betiği - Azure kullanarak aaaTransform veri | Microsoft Docs"
description: "Üzerinde Azure Data Lake Analytics U-SQL komut dosyaları çalıştırarak tooprocess veya dönüştürme veri hizmeti nasıl işlem öğrenin."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e17c1255-62c2-4e2e-bb60-d25274903e80
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: spelluru
ms.openlocfilehash: 51fdb40334d0c131720f65c3a96b4c5045a98b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a><span data-ttu-id="21121-103">Üzerinde Azure Data Lake Analytics U-SQL betiklerini çalıştırarak veri dönüştürme</span><span class="sxs-lookup"><span data-stu-id="21121-103">Transform data by running U-SQL scripts on Azure Data Lake Analytics</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="21121-104">Hive etkinliği</span><span class="sxs-lookup"><span data-stu-id="21121-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="21121-105">Pig etkinliği</span><span class="sxs-lookup"><span data-stu-id="21121-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="21121-106">MapReduce etkinliği</span><span class="sxs-lookup"><span data-stu-id="21121-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="21121-107">Hadoop akış etkinliği</span><span class="sxs-lookup"><span data-stu-id="21121-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="21121-108">Spark etkinliği</span><span class="sxs-lookup"><span data-stu-id="21121-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="21121-109">Machine Learning Batch Yürütme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="21121-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="21121-110">Machine Learning Kaynak Güncelleştirme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="21121-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="21121-111">Saklı Yordam Etkinliği</span><span class="sxs-lookup"><span data-stu-id="21121-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="21121-112">Data Lake Analytics U-SQL Etkinliği</span><span class="sxs-lookup"><span data-stu-id="21121-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="21121-113">.NET özel etkinlik</span><span class="sxs-lookup"><span data-stu-id="21121-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="21121-114">Bir Azure data factory işlem hattı bağlantılı işlem hizmetlerini kullanarak bağlantılı depolama Hizmetleri'nde verilerini işler.</span><span class="sxs-lookup"><span data-stu-id="21121-114">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="21121-115">Burada her etkinlik özel işleme işlemi gerçekleştiren etkinlikler dizisini içerir.</span><span class="sxs-lookup"><span data-stu-id="21121-115">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="21121-116">Bu makalede hello **Data Lake Analytics U-SQL etkinliği** çalıştıran bir **U-SQL** üzerinde komut dosyası bir **Azure Data Lake Analytics** bağlantılı hizmet işlem.</span><span class="sxs-lookup"><span data-stu-id="21121-116">This article describes hello **Data Lake Analytics U-SQL Activity** that runs a **U-SQL** script on an **Azure Data Lake Analytics** compute linked service.</span></span> 

> [!NOTE]
> <span data-ttu-id="21121-117">Bir Azure Data Lake Analytics hesabı, bir veri Lake Analytics U-SQL etkinliği ile işlem hattı oluşturmadan önce oluşturun.</span><span class="sxs-lookup"><span data-stu-id="21121-117">Create an Azure Data Lake Analytics account before creating a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="21121-118">Azure Data Lake Analytics hakkında toolearn bkz [Azure Data Lake Analytics ile çalışmaya başlama](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="21121-118">toolearn about Azure Data Lake Analytics, see [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span>
> 
> <span data-ttu-id="21121-119">Gözden geçirme hello [ilk ardışık düzen öğreticinizi yapı](data-factory-build-your-first-pipeline.md) ayrıntılı adımlar toocreate veri fabrikası için hizmetler, veri kümeleri ve işlem hattı bağlı.</span><span class="sxs-lookup"><span data-stu-id="21121-119">Review hello [Build your first pipeline tutorial](data-factory-build-your-first-pipeline.md) for detailed steps toocreate a data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="21121-120">JSON parçacığı, Data Factory Düzenleyici veya Visual Studio ya da Azure PowerShell toocreate Data Factory varlıklarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="21121-120">Use JSON snippets with Data Factory Editor or Visual Studio or Azure PowerShell toocreate Data Factory entities.</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="21121-121">Desteklenen kimlik doğrulama türleri</span><span class="sxs-lookup"><span data-stu-id="21121-121">Supported authentication types</span></span>
<span data-ttu-id="21121-122">Data Lake Analytics karşı kimlik doğrulama türleri aşağıdaki U-SQL etkinliği destekler:</span><span class="sxs-lookup"><span data-stu-id="21121-122">U-SQL activity supports below authentication types against Data Lake Analytics:</span></span>
* <span data-ttu-id="21121-123">Hizmet sorumlusu kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="21121-123">Service principal authentication</span></span>
* <span data-ttu-id="21121-124">Kullanıcı kimlik bilgisi (OAuth) kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="21121-124">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="21121-125">Zamanlanmış U-SQL yürütmesi için özellikle bir hizmet asıl kimlik doğrulaması kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="21121-125">We recommend that you use service principal authentication, especially for a scheduled U-SQL execution.</span></span> <span data-ttu-id="21121-126">Belirteç süre sonu davranış kullanıcı kimlik bilgilerinin ile ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="21121-126">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="21121-127">Merhaba yapılandırma ayrıntıları için bkz: [bağlantılı hizmet özellikleri](#azure-data-lake-analytics-linked-service) bölümü.</span><span class="sxs-lookup"><span data-stu-id="21121-127">For configuration details, see hello [Linked service properties](#azure-data-lake-analytics-linked-service) section.</span></span>

## <a name="azure-data-lake-analytics-linked-service"></a><span data-ttu-id="21121-128">Azure Data Lake Analytics hizmeti bağlı</span><span class="sxs-lookup"><span data-stu-id="21121-128">Azure Data Lake Analytics Linked Service</span></span>
<span data-ttu-id="21121-129">Oluşturduğunuz bir **Azure Data Lake Analytics** bağlantılı hizmet toolink bir Azure Data Lake Analytics işlem hizmeti tooan Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="21121-129">You create an **Azure Data Lake Analytics** linked service toolink an Azure Data Lake Analytics compute service tooan Azure data factory.</span></span> <span data-ttu-id="21121-130">Merhaba Data Lake Analytics U-SQL etkinliği hello ardışık düzende toothis bağlantılı hizmeti anlamına gelmektedir.</span><span class="sxs-lookup"><span data-stu-id="21121-130">hello Data Lake Analytics U-SQL activity in hello pipeline refers toothis linked service.</span></span> 

<span data-ttu-id="21121-131">Merhaba aşağıdaki tabloda Merhaba açıklamalarına hello JSON tanımını kullanılan genel özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="21121-131">hello following table provides descriptions for hello generic properties used in hello JSON definition.</span></span> <span data-ttu-id="21121-132">Daha fazla hizmet sorumlusu ve kullanıcı kimlik bilgileri doğrulaması arasında seçim yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21121-132">You can further choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="21121-133">Özellik</span><span class="sxs-lookup"><span data-stu-id="21121-133">Property</span></span> | <span data-ttu-id="21121-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21121-134">Description</span></span> | <span data-ttu-id="21121-135">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21121-135">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21121-136">**türü**</span><span class="sxs-lookup"><span data-stu-id="21121-136">**type**</span></span> |<span data-ttu-id="21121-137">Merhaba type özelliği ayarlanmalıdır: **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="21121-137">hello type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="21121-138">Evet</span><span class="sxs-lookup"><span data-stu-id="21121-138">Yes</span></span> |
| <span data-ttu-id="21121-139">**accountName**</span><span class="sxs-lookup"><span data-stu-id="21121-139">**accountName**</span></span> |<span data-ttu-id="21121-140">Azure Data Lake Analytics hesap adı.</span><span class="sxs-lookup"><span data-stu-id="21121-140">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="21121-141">Evet</span><span class="sxs-lookup"><span data-stu-id="21121-141">Yes</span></span> |
| <span data-ttu-id="21121-142">**dataLakeAnalyticsUri**</span><span class="sxs-lookup"><span data-stu-id="21121-142">**dataLakeAnalyticsUri**</span></span> |<span data-ttu-id="21121-143">Azure Data Lake Analytics URI.</span><span class="sxs-lookup"><span data-stu-id="21121-143">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="21121-144">Hayır</span><span class="sxs-lookup"><span data-stu-id="21121-144">No</span></span> |
| <span data-ttu-id="21121-145">**Subscriptionıd**</span><span class="sxs-lookup"><span data-stu-id="21121-145">**subscriptionId**</span></span> |<span data-ttu-id="21121-146">Azure abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="21121-146">Azure subscription id</span></span> |<span data-ttu-id="21121-147">Hayır (belirtilmezse, veri fabrikası kullanılan hello abonelik).</span><span class="sxs-lookup"><span data-stu-id="21121-147">No (If not specified, subscription of hello data factory is used).</span></span> |
| <span data-ttu-id="21121-148">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="21121-148">**resourceGroupName**</span></span> |<span data-ttu-id="21121-149">Azure kaynak grubu adı</span><span class="sxs-lookup"><span data-stu-id="21121-149">Azure resource group name</span></span> |<span data-ttu-id="21121-150">Hayır (belirtilmezse, veri fabrikası kullanılan hello kaynak grubu).</span><span class="sxs-lookup"><span data-stu-id="21121-150">No (If not specified, resource group of hello data factory is used).</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="21121-151">(Önerilen) hizmet asıl kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="21121-151">Service principal authentication (recommended)</span></span>
<span data-ttu-id="21121-152">Kayıt, hello Azure Active Directory (Azure AD) ve grant uygulama varlık toouse hizmet asıl kimlik doğrulaması, tooData Lake Store erişin.</span><span class="sxs-lookup"><span data-stu-id="21121-152">toouse service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it hello access tooData Lake Store.</span></span> <span data-ttu-id="21121-153">Ayrıntılı adımlar için bkz: [hizmeti için kimlik doğrulama](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="21121-153">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="21121-154">Kullandığınız değerler aşağıdaki hello Not toodefine hello bağlantılı hizmeti:</span><span class="sxs-lookup"><span data-stu-id="21121-154">Make note of hello following values, which you use toodefine hello linked service:</span></span>
* <span data-ttu-id="21121-155">Uygulama Kimliği</span><span class="sxs-lookup"><span data-stu-id="21121-155">Application ID</span></span>
* <span data-ttu-id="21121-156">Uygulama anahtarı</span><span class="sxs-lookup"><span data-stu-id="21121-156">Application key</span></span> 
* <span data-ttu-id="21121-157">Kiracı Kimliği</span><span class="sxs-lookup"><span data-stu-id="21121-157">Tenant ID</span></span>

<span data-ttu-id="21121-158">Aşağıdaki özelliklere hello belirterek hizmet asıl kimlik doğrulamasını kullan:</span><span class="sxs-lookup"><span data-stu-id="21121-158">Use service principal authentication by specifying hello following properties:</span></span>

| <span data-ttu-id="21121-159">Özellik</span><span class="sxs-lookup"><span data-stu-id="21121-159">Property</span></span> | <span data-ttu-id="21121-160">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21121-160">Description</span></span> | <span data-ttu-id="21121-161">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21121-161">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="21121-162">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="21121-162">**servicePrincipalId**</span></span> | <span data-ttu-id="21121-163">Merhaba uygulamanın istemci kimliği belirtin.</span><span class="sxs-lookup"><span data-stu-id="21121-163">Specify hello application's client ID.</span></span> | <span data-ttu-id="21121-164">Evet</span><span class="sxs-lookup"><span data-stu-id="21121-164">Yes</span></span> |
| <span data-ttu-id="21121-165">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="21121-165">**servicePrincipalKey**</span></span> | <span data-ttu-id="21121-166">Merhaba uygulamanın anahtarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="21121-166">Specify hello application's key.</span></span> | <span data-ttu-id="21121-167">Evet</span><span class="sxs-lookup"><span data-stu-id="21121-167">Yes</span></span> |
| <span data-ttu-id="21121-168">**Kiracı**</span><span class="sxs-lookup"><span data-stu-id="21121-168">**tenant**</span></span> | <span data-ttu-id="21121-169">Uygulamanızın bulunduğu altında Hello Kiracı bilgileri (etki alanı adı veya Kiracı kimliği) belirtin.</span><span class="sxs-lookup"><span data-stu-id="21121-169">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="21121-170">Vurgulama hello fare hello sağ üst köşesindeki hello Azure portal tarafından alabilir.</span><span class="sxs-lookup"><span data-stu-id="21121-170">You can retrieve it by hovering hello mouse in hello upper-right corner of hello Azure portal.</span></span> | <span data-ttu-id="21121-171">Evet</span><span class="sxs-lookup"><span data-stu-id="21121-171">Yes</span></span> |

<span data-ttu-id="21121-172">**Örnek: Hizmet asıl kimlik doğrulaması**</span><span class="sxs-lookup"><span data-stu-id="21121-172">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a><span data-ttu-id="21121-173">Kullanıcı kimlik bilgileri doğrulaması</span><span class="sxs-lookup"><span data-stu-id="21121-173">User credential authentication</span></span>
<span data-ttu-id="21121-174">Alternatif olarak, aşağıdaki özelliklere hello belirterek Data Lake Analytics için kullanıcı kimlik bilgilerinin kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="21121-174">Alternatively, you can use user credential authentication for Data Lake Analytics by specifying hello following properties:</span></span>

| <span data-ttu-id="21121-175">Özellik</span><span class="sxs-lookup"><span data-stu-id="21121-175">Property</span></span> | <span data-ttu-id="21121-176">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21121-176">Description</span></span> | <span data-ttu-id="21121-177">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21121-177">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="21121-178">**Yetkilendirme**</span><span class="sxs-lookup"><span data-stu-id="21121-178">**authorization**</span></span> | <span data-ttu-id="21121-179">Merhaba tıklatın **Authorize** hello Data Factory Düzenleyici'düğmesine tıklayın ve hello otomatik olarak oluşturulur yetkilendirme URL'si toothis özelliği atar kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="21121-179">Click hello **Authorize** button in hello Data Factory Editor and enter your credential that assigns hello autogenerated authorization URL toothis property.</span></span> | <span data-ttu-id="21121-180">Evet</span><span class="sxs-lookup"><span data-stu-id="21121-180">Yes</span></span> |
| <span data-ttu-id="21121-181">**SessionID**</span><span class="sxs-lookup"><span data-stu-id="21121-181">**sessionId**</span></span> | <span data-ttu-id="21121-182">Merhaba OAuth yetkilendirme oturumundan OAuth oturum kimliği.</span><span class="sxs-lookup"><span data-stu-id="21121-182">OAuth session ID from hello OAuth authorization session.</span></span> <span data-ttu-id="21121-183">Her oturum kimliği benzersiz olup yalnızca bir kez kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="21121-183">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="21121-184">Merhaba Data Factory Düzenleyici kullandığınızda bu ayarı otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="21121-184">This setting is automatically generated when you use hello Data Factory Editor.</span></span> | <span data-ttu-id="21121-185">Evet</span><span class="sxs-lookup"><span data-stu-id="21121-185">Yes</span></span> |

<span data-ttu-id="21121-186">**Örnek: Kullanıcı kimlik bilgileri doğrulaması**</span><span class="sxs-lookup"><span data-stu-id="21121-186">**Example: User credential authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a><span data-ttu-id="21121-187">Belirteç süre sonu</span><span class="sxs-lookup"><span data-stu-id="21121-187">Token expiration</span></span>
<span data-ttu-id="21121-188">Merhaba oluşturulan hello kullanarak Yetkilendirme kodu **Authorize** düğmesi süre sonra süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="21121-188">hello authorization code you generated by using hello **Authorize** button expires after sometime.</span></span> <span data-ttu-id="21121-189">Farklı türlerdeki kullanıcı hesapları için hello bitiş zamanları için aşağıdaki tablonun hello bakın.</span><span class="sxs-lookup"><span data-stu-id="21121-189">See hello following table for hello expiration times for different types of user accounts.</span></span> <span data-ttu-id="21121-190">Aşağıdaki hata iletisini hello görebilirsiniz zaman kimlik doğrulaması'nı hello **belirtecinin süresi dolmadan**: kimlik bilgisi işlemi hatası: invalid_grant - AADSTS70002: Kimlik doğrulanırken hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="21121-190">You may see hello following error message when hello authentication **token expires**: Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="21121-191">AADSTS70008: hello erişim izninin süresi doldu veya iptal sağlanan.</span><span class="sxs-lookup"><span data-stu-id="21121-191">AADSTS70008: hello provided access grant is expired or revoked.</span></span> <span data-ttu-id="21121-192">İzleme kimliği: d18629e8-af88-43c5-88e3-d8419eb1fca1 bağıntı kimliği: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 zaman damgası: 2015-12-15 21:09:31Z</span><span class="sxs-lookup"><span data-stu-id="21121-192">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z</span></span>

| <span data-ttu-id="21121-193">Kullanıcı türü</span><span class="sxs-lookup"><span data-stu-id="21121-193">User type</span></span> | <span data-ttu-id="21121-194">Kullanım süresi sonu</span><span class="sxs-lookup"><span data-stu-id="21121-194">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="21121-195">Azure Active Directory tarafından yönetilmeyen kullanıcı hesapları (@hotmail.com, @live.comvb..)</span><span class="sxs-lookup"><span data-stu-id="21121-195">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.)</span></span> |<span data-ttu-id="21121-196">12 saat</span><span class="sxs-lookup"><span data-stu-id="21121-196">12 hours</span></span> |
| <span data-ttu-id="21121-197">Azure Active Directory (AAD tarafından) yönetilen kullanıcı hesapları</span><span class="sxs-lookup"><span data-stu-id="21121-197">Users accounts managed by Azure Active Directory (AAD)</span></span> |<span data-ttu-id="21121-198">14 gün sonra hello son dilim çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="21121-198">14 days after hello last slice run.</span></span> <br/><br/><span data-ttu-id="21121-199">90 OAuth tabanlı bağlantılı hizmette dayanan bir dilim 14 günde bir en az bir kez çalıştırılıyorsa, gün.</span><span class="sxs-lookup"><span data-stu-id="21121-199">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span></span> |

<span data-ttu-id="21121-200">tooavoid/Çöz bu hata, hello kullanarak yeniden yetkilendirin **Authorize** düğmesini hello **belirtecinin süresi dolmadan** ve hello bağlantılı hizmeti yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="21121-200">tooavoid/resolve this error, reauthorize using hello **Authorize** button when hello **token expires** and redeploy hello linked service.</span></span> <span data-ttu-id="21121-201">Değerleri de oluşturabilirsiniz **SessionID** ve **yetkilendirme** kullanılarak programlı olarak kod şu şekilde özellikleri:</span><span class="sxs-lookup"><span data-stu-id="21121-201">You can also generate values for **sessionId** and **authorization** properties programmatically using code as follows:</span></span>

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

<span data-ttu-id="21121-202">Bkz: [AzureDataLakeStoreLinkedService sınıfı](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService sınıfı](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), ve [AuthorizationSessionGetResponse sınıfı](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) ayrıntıları konuları Merhaba kod içinde kullanılan hello Data Factory sınıfları hakkında.</span><span class="sxs-lookup"><span data-stu-id="21121-202">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about hello Data Factory classes used in hello code.</span></span> <span data-ttu-id="21121-203">Bir başvuru ekleyin: Merhaba WindowsFormsWebAuthenticationDialog sınıfı için Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll.</span><span class="sxs-lookup"><span data-stu-id="21121-203">Add a reference to: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll for hello WindowsFormsWebAuthenticationDialog class.</span></span> 

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="21121-204">Data Lake Analytics U-SQL Etkinliği</span><span class="sxs-lookup"><span data-stu-id="21121-204">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="21121-205">JSON parçacığı aşağıdaki hello bir Data Lake Analytics U-SQL etkinliği ile işlem hattı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="21121-205">hello following JSON snippet defines a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="21121-206">Merhaba etkinlik tanımı başvuru toohello daha önce oluşturduğunuz Azure Data Lake Analytics bağlantılı hizmet yok.</span><span class="sxs-lookup"><span data-stu-id="21121-206">hello activity definition has a reference toohello Azure Data Lake Analytics linked service you created earlier.</span></span>   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline toocompute events for en-gb locale and date less than 2012/02/19.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00Z",
        "end": "2015-08-08T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="21121-207">Merhaba aşağıdaki tabloda adları ve açıklamaları belirli toothis etkinlik özellikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="21121-207">hello following table describes names and descriptions of properties that are specific toothis activity.</span></span> 

| <span data-ttu-id="21121-208">Özellik</span><span class="sxs-lookup"><span data-stu-id="21121-208">Property</span></span> | <span data-ttu-id="21121-209">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21121-209">Description</span></span> | <span data-ttu-id="21121-210">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21121-210">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="21121-211">type</span><span class="sxs-lookup"><span data-stu-id="21121-211">type</span></span> |<span data-ttu-id="21121-212">Merhaba type özelliği çok ayarlanmalıdır**DataLakeAnalyticsU SQL**.</span><span class="sxs-lookup"><span data-stu-id="21121-212">hello type property must be set too**DataLakeAnalyticsU-SQL**.</span></span> |<span data-ttu-id="21121-213">Evet</span><span class="sxs-lookup"><span data-stu-id="21121-213">Yes</span></span> |
| <span data-ttu-id="21121-214">scriptPath</span><span class="sxs-lookup"><span data-stu-id="21121-214">scriptPath</span></span> |<span data-ttu-id="21121-215">Merhaba U-SQL betiğini içeren yolu toofolder.</span><span class="sxs-lookup"><span data-stu-id="21121-215">Path toofolder that contains hello U-SQL script.</span></span> <span data-ttu-id="21121-216">Merhaba dosyasının adı büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="21121-216">Name of hello file is case-sensitive.</span></span> |<span data-ttu-id="21121-217">Hayır (komut dosyası kullanırsanız)</span><span class="sxs-lookup"><span data-stu-id="21121-217">No (if you use script)</span></span> |
| <span data-ttu-id="21121-218">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="21121-218">scriptLinkedService</span></span> |<span data-ttu-id="21121-219">Merhaba betik toohello veri fabrikası içeren hello depolamayı bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21121-219">Linked service that links hello storage that contains hello script toohello data factory</span></span> |<span data-ttu-id="21121-220">Hayır (komut dosyası kullanırsanız)</span><span class="sxs-lookup"><span data-stu-id="21121-220">No (if you use script)</span></span> |
| <span data-ttu-id="21121-221">Komut dosyası</span><span class="sxs-lookup"><span data-stu-id="21121-221">script</span></span> |<span data-ttu-id="21121-222">ScriptPath ve scriptLinkedService belirtme yerine satır içi betiği belirtin.</span><span class="sxs-lookup"><span data-stu-id="21121-222">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="21121-223">Örneğin: `"script": "CREATE DATABASE test"`.</span><span class="sxs-lookup"><span data-stu-id="21121-223">For example: `"script": "CREATE DATABASE test"`.</span></span> |<span data-ttu-id="21121-224">Hayır (scriptPath ve scriptLinkedService kullanıyorsanız)</span><span class="sxs-lookup"><span data-stu-id="21121-224">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="21121-225">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="21121-225">degreeOfParallelism</span></span> |<span data-ttu-id="21121-226">Merhaba en fazla düğüm sayısını toorun hello işi aynı anda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="21121-226">hello maximum number of nodes simultaneously used toorun hello job.</span></span> |<span data-ttu-id="21121-227">Hayır</span><span class="sxs-lookup"><span data-stu-id="21121-227">No</span></span> |
| <span data-ttu-id="21121-228">Öncelik</span><span class="sxs-lookup"><span data-stu-id="21121-228">priority</span></span> |<span data-ttu-id="21121-229">Sıraya alınan tüm işlerden seçili toorun olması gereken ilk belirler.</span><span class="sxs-lookup"><span data-stu-id="21121-229">Determines which jobs out of all that are queued should be selected toorun first.</span></span> <span data-ttu-id="21121-230">Merhaba alt hello numarası hello yüksek hello önceliği.</span><span class="sxs-lookup"><span data-stu-id="21121-230">hello lower hello number, hello higher hello priority.</span></span> |<span data-ttu-id="21121-231">Hayır</span><span class="sxs-lookup"><span data-stu-id="21121-231">No</span></span> |
| <span data-ttu-id="21121-232">parametreler</span><span class="sxs-lookup"><span data-stu-id="21121-232">parameters</span></span> |<span data-ttu-id="21121-233">Merhaba U-SQL komut dosyası için parametreler</span><span class="sxs-lookup"><span data-stu-id="21121-233">Parameters for hello U-SQL script</span></span> |<span data-ttu-id="21121-234">Hayır</span><span class="sxs-lookup"><span data-stu-id="21121-234">No</span></span> |
| <span data-ttu-id="21121-235">runtimeVersion</span><span class="sxs-lookup"><span data-stu-id="21121-235">runtimeVersion</span></span> | <span data-ttu-id="21121-236">U-SQL hello altyapısı toouse çalışma zamanı sürümü</span><span class="sxs-lookup"><span data-stu-id="21121-236">Runtime version of hello U-SQL engine toouse</span></span> | <span data-ttu-id="21121-237">Hayır</span><span class="sxs-lookup"><span data-stu-id="21121-237">No</span></span> | 
| <span data-ttu-id="21121-238">compilationMode</span><span class="sxs-lookup"><span data-stu-id="21121-238">compilationMode</span></span> | <p><span data-ttu-id="21121-239">U-SQL derleme modu.</span><span class="sxs-lookup"><span data-stu-id="21121-239">Compilation mode of U-SQL.</span></span> <span data-ttu-id="21121-240">Şu değerlerden biri olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="21121-240">Must be one of these values:</span></span></p> <ul><li><span data-ttu-id="21121-241">**Anlam:** yalnızca anlamsal denetler ve gerekli sağlamlık denetimleri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="21121-241">**Semantic:** Only perform semantic checks and necessary sanity checks.</span></span></li><li><span data-ttu-id="21121-242">**Tam:** sözdizimi denetimi, en iyi duruma getirme, kod oluşturma, vb. dahil olmak üzere hello tam derleme gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="21121-242">**Full:** Perform hello full compilation, including syntax check, optimization, code generation, etc.</span></span></li><li><span data-ttu-id="21121-243">**SingleBox:** TargetType ayarı tooSingleBox ile Merhaba tam derleme gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="21121-243">**SingleBox:** Perform hello full compilation, with TargetType setting tooSingleBox.</span></span></li></ul><p><span data-ttu-id="21121-244">Bu özellik için bir değer belirtmezseniz, hello sunucu hello en iyi bir derleme moduna belirler.</span><span class="sxs-lookup"><span data-stu-id="21121-244">If you don't specify a value for this property, hello server determines hello optimal compilation mode.</span></span> </p>| <span data-ttu-id="21121-245">Hayır</span><span class="sxs-lookup"><span data-stu-id="21121-245">No</span></span> | 

<span data-ttu-id="21121-246">Bkz: [SearchLogProcessing.txt betik tanımı](#sample-u-sql-script) hello betik tanımı.</span><span class="sxs-lookup"><span data-stu-id="21121-246">See [SearchLogProcessing.txt Script Definition](#sample-u-sql-script) for hello script definition.</span></span> 

## <a name="sample-input-and-output-datasets"></a><span data-ttu-id="21121-247">Örnek girdi ve çıktı veri kümeleri</span><span class="sxs-lookup"><span data-stu-id="21121-247">Sample input and output datasets</span></span>
### <a name="input-dataset"></a><span data-ttu-id="21121-248">Girdi veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21121-248">Input dataset</span></span>
<span data-ttu-id="21121-249">Bu örnekte, bir Azure Data Lake Store (Merhaba datalake/giriş klasörünü dosyasında searchlog.tsv dosyasını) hello giriş verisi bulunur.</span><span class="sxs-lookup"><span data-stu-id="21121-249">In this example, hello input data resides in an Azure Data Lake Store (SearchLog.tsv file in hello datalake/input folder).</span></span> 

```json
{
    "name": "DataLakeTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}    
```

### <a name="output-dataset"></a><span data-ttu-id="21121-250">Çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21121-250">Output dataset</span></span>
<span data-ttu-id="21121-251">Bu örnekte, U-SQL betiği hello tarafından üretilen hello çıktı verilerini bir Azure Data Lake Store'da (datalake/çıkış klasörü) depolanır.</span><span class="sxs-lookup"><span data-stu-id="21121-251">In this example, hello output data produced by hello U-SQL script is stored in an Azure Data Lake Store (datalake/output folder).</span></span> 

```json
{
    "name": "EventsByRegionTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="sample-data-lake-store-linked-service"></a><span data-ttu-id="21121-252">Bağlantılı hizmetinin örnek veri Gölü deposu</span><span class="sxs-lookup"><span data-stu-id="21121-252">Sample Data Lake Store Linked Service</span></span>
<span data-ttu-id="21121-253">Azure Data Lake Store giriş/çıkış hello veri kümeleri tarafından kullanılan hizmet bağlı hello örnek hello tanımı aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="21121-253">Here is hello definition of hello sample Azure Data Lake Store linked service used by hello input/output datasets.</span></span> 

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
        }
    }
}
```

<span data-ttu-id="21121-254">Bkz: [veri tooand Azure Data Lake Deposu'ndan veri taşıma](data-factory-azure-datalake-connector.md) makale açıklamaları JSON özellikleri için.</span><span class="sxs-lookup"><span data-stu-id="21121-254">See [Move data tooand from Azure Data Lake Store](data-factory-azure-datalake-connector.md) article for descriptions of JSON properties.</span></span> 

## <a name="sample-u-sql-script"></a><span data-ttu-id="21121-255">Örnek U-SQL betiği</span><span class="sxs-lookup"><span data-stu-id="21121-255">Sample U-SQL Script</span></span>

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    too@out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

<span data-ttu-id="21121-256">Merhaba değerlerini  **@in**  ve  **@out**  hello U-SQL betiği parametrelerinde geçirilir dinamik olarak ADF tarafından hello 'parameters' bölümünü kullanarak.</span><span class="sxs-lookup"><span data-stu-id="21121-256">hello values for **@in** and **@out** parameters in hello U-SQL script are passed dynamically by ADF using hello ‘parameters’ section.</span></span> <span data-ttu-id="21121-257">Merhaba ardışık düzen tanımı Hello 'parameters' bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="21121-257">See hello ‘parameters’ section in hello pipeline definition.</span></span>

<span data-ttu-id="21121-258">DegreeOfParallelism ve öncelik gibi diğer özellikleri ardışık düzen tanımınızı hello Azure Data Lake Analytics hizmeti üzerinde çalıştırılan hello işleri için de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21121-258">You can specify other properties such as degreeOfParallelism and priority as well in your pipeline definition for hello jobs that run on hello Azure Data Lake Analytics service.</span></span>

## <a name="dynamic-parameters"></a><span data-ttu-id="21121-259">Dinamik parametreler</span><span class="sxs-lookup"><span data-stu-id="21121-259">Dynamic parameters</span></span>
<span data-ttu-id="21121-260">Merhaba örnek ardışık düzen tanımı'nda giriş ve çıkış parametreleri sabit kodlanmış değerler ile atandı.</span><span class="sxs-lookup"><span data-stu-id="21121-260">In hello sample pipeline definition, in and out parameters are assigned with hard-coded values.</span></span> 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

<span data-ttu-id="21121-261">Bunun yerine olası toouse dinamik parametreleri olur.</span><span class="sxs-lookup"><span data-stu-id="21121-261">It is possible toouse dynamic parameters instead.</span></span> <span data-ttu-id="21121-262">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="21121-262">For example:</span></span> 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

<span data-ttu-id="21121-263">Bu durumda, giriş dosyaları hala hello /datalake/input klasöründen toplanmış ve çıktı dosyalarını hello /datalake/output klasöründe oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="21121-263">In this case, input files are still picked up from hello /datalake/input folder and output files are generated in hello /datalake/output folder.</span></span> <span data-ttu-id="21121-264">Merhaba dosya hello dilim başlangıç zamanı temel alınarak dinamik adlardır.</span><span class="sxs-lookup"><span data-stu-id="21121-264">hello file names are dynamic based on hello slice start time.</span></span>  

