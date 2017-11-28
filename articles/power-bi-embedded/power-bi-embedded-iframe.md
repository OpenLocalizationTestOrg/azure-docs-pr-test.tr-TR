---
title: Power BI Embedded REST ile kullanma | Microsoft Docs
description: "Power BI Embedded KALAN ile kullanmayı öğrenin "
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 8bcef780-cca0-4f30-9a9b-9daa1a7ae865
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 02/06/2017
ms.author: asaxton
ms.openlocfilehash: 31624b9d15772a4f08cf013ac713b3aa636acfca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-power-bi-embedded-with-rest"></a><span data-ttu-id="5c6c8-103">Power BI Embedded REST ile kullanma</span><span class="sxs-lookup"><span data-stu-id="5c6c8-103">How to use Power BI Embedded with REST</span></span>

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a><span data-ttu-id="5c6c8-104">Power BI Embedded: Nedir ve ne işe yaradığını</span><span class="sxs-lookup"><span data-stu-id="5c6c8-104">Power BI Embedded: What it is and what it's for</span></span>

<span data-ttu-id="5c6c8-105">Power BI Embedded genel bakış resmi açıklanan [Power BI Embedded site](https://azure.microsoft.com/services/power-bi-embedded/), ancak biz REST ile kullanma hakkında ayrıntılı bilgi almak önce hızlı bir göz atalım.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-105">An overview of Power BI Embedded is described in the official [Power BI Embedded site](https://azure.microsoft.com/services/power-bi-embedded/), but let's take a quick look before we get into the details about using it with REST.</span></span>

<span data-ttu-id="5c6c8-106">Gerçekten oldukça basit.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-106">It's quite simple, really.</span></span> <span data-ttu-id="5c6c8-107">dinamik veri Görselleştirmelerini kullanmak isteyebilirsiniz [Power BI](https://powerbi.microsoft.com) kendi uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-107">you may want to use the dynamic data visualizations of [Power BI](https://powerbi.microsoft.com) in your own application.</span></span>

<span data-ttu-id="5c6c8-108">Kendi müşteriler için veriler, mutlaka kullanıcılar kendi kuruluşunda sunmak özel uygulamaların çoğu gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-108">Most custom applications need to deliver the data for their own customers, not necessarily users in their own organization.</span></span> <span data-ttu-id="5c6c8-109">Şirket A ve B şirketi için bazı hizmet sunma, örneğin, Şirket A kullanıcılar yalnızca veri kendi Şirket A'daki görmeniz gerekir Diğer bir deyişle, çoklu kiracı teslimat için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-109">For example, if you're delivering some service for both company A and company B, users in company A should only see data for their own company A. That is, the multi-tenancy is needed for the delivery.</span></span>

<span data-ttu-id="5c6c8-110">Özel uygulama, form kimlik doğrulama, temel kimlik doğrulama vb. gibi kendi kimlik doğrulama yöntemleri de sunumu..</span><span class="sxs-lookup"><span data-stu-id="5c6c8-110">The custom application might also be offering its own authentication methods such as forms auth, basic auth, etc..</span></span> <span data-ttu-id="5c6c8-111">Ardından, katıştırma çözüm var olan bu kimlik doğrulama yöntemleri ile güvenli bir şekilde işbirliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-111">Then, the embedding solution must collaborate with this existing authentication methods safely.</span></span> <span data-ttu-id="5c6c8-112">Kullanıcıların bu ISV uygulamalar fazladan satın almadan kullanmak için veya bir Power BI aboneliğin lisans olması için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-112">It's also necessary for users to be able to use those ISV applications without the extra purchase or licensing of a Power BI subscription.</span></span>

 <span data-ttu-id="5c6c8-113">**Power BI Embedded** tam olarak bu tür senaryoları için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-113">**Power BI Embedded** is designed for precisely these kinds of scenarios.</span></span> <span data-ttu-id="5c6c8-114">Bu nedenle, biz Bu hızlı giriş göz önünden sahip olduğunuza göre şimdi bazı ayrıntılar alın</span><span class="sxs-lookup"><span data-stu-id="5c6c8-114">So, now that we have that quick introduction out of the way, let's get into some details</span></span>

<span data-ttu-id="5c6c8-115">.NET kullanabilirsiniz \(C#) veya kolayca Power BI Embedded ile uygulamanızı oluşturmak için Node.js SDK.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-115">You can use the .NET \(C#) or Node.js SDK, to easily build your application with Power BI Embedded.</span></span> <span data-ttu-id="5c6c8-116">Ancak, bu makalede, HTTP akışı hakkında açıklayacağız \(dahil AuthN) SDK'ları olmadan Power BI.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-116">But, in this article, we'll explain about HTTP flow \(incl. AuthN) of Power BI without SDKs.</span></span> <span data-ttu-id="5c6c8-117">Bu akış anlama, uygulamanızı oluşturabilir **herhangi bir programlama dili ile**, ve Power BI Embedded özünü derine anlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-117">Understanding this flow, you can build your application **with any programming language**, and you can understand deeply the essence of Power BI Embedded.</span></span>

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a><span data-ttu-id="5c6c8-118">Power BI oluşturma çalışma alanı koleksiyonu ve get erişim tuşu \(hazırlama)</span><span class="sxs-lookup"><span data-stu-id="5c6c8-118">Create Power BI workspace collection, and get access key \(Provisioning)</span></span>

<span data-ttu-id="5c6c8-119">Power BI Embedded, Azure Hizmetleri biridir.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-119">Power BI Embedded is one of the Azure services.</span></span> <span data-ttu-id="5c6c8-120">Azure Portal kullanan ISV kullanım ücretleri için sizden ücret \(saatlik kullanıcı oturumu başına), ve rapor görünümleri kullanıcının ücret değil veya bile bir Azure aboneliği gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-120">Only the ISV who uses Azure Portal is charged for usage fees \(per hourly user session), and the user who views the report isn't charged or even require an Azure subscription.</span></span>
<span data-ttu-id="5c6c8-121">Bizim uygulama geliştirme başlatmadan önce biz oluşturmalısınız **Power BI çalışma alanı koleksiyonu** Azure portalını kullanarak.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-121">Before starting our application development, we must create the **Power BI workspace collection** by using Azure Portal.</span></span>

<span data-ttu-id="5c6c8-122">Power BI Embedded her çalışma (Kiracı) her müşteri için çalışma alanıdır ve her çalışma alanı koleksiyonu birçok çalışma alanları ekleyebiliriz.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-122">Each workspace of Power BI Embedded is the workspace for each customer (tenant), and we can add many workspaces in each workspace collection.</span></span> <span data-ttu-id="5c6c8-123">Aynı erişim anahtarını her çalışma alanı koleksiyonu kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-123">The same access key is used in each workspace collection.</span></span> <span data-ttu-id="5c6c8-124">İçinde etkisi, Power BI Embedded için güvenlik sınırı çalışma koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-124">In-effect, the workspace collection is the security boundary for Power BI Embedded.</span></span>

![](media/power-bi-embedded-iframe/create-workspace.png)

<span data-ttu-id="5c6c8-125">Çalışma alanı koleksiyonu oluşturma sona erdiğinde erişim tuşunu Azure Portal'dan kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-125">When we finish creating the workspace collection, copy the access key from Azure Portal.</span></span>

![](media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> <span data-ttu-id="5c6c8-126">Biz de çalışma alanı koleksiyonu sağlayabilir ve erişim anahtarı REST API aracılığıyla alın.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-126">We can also provision the workspace collection and get access key via REST API.</span></span> <span data-ttu-id="5c6c8-127">Daha fazla bilgi için bkz: [Power BI kaynak sağlayıcısı API'leri](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span><span class="sxs-lookup"><span data-stu-id="5c6c8-127">To learn more, see [Power BI Resource Provider APIs](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span></span>

## <a name="create-pbix-file-with-power-bi-desktop"></a><span data-ttu-id="5c6c8-128">Power BI Desktop ile .pbix dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="5c6c8-128">Create .pbix file with Power BI Desktop</span></span>

<span data-ttu-id="5c6c8-129">Ardından, biz katıştırılacak raporları ve veri bağlantısı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-129">Next, we must create the data connection and reports to be embedded.</span></span>
<span data-ttu-id="5c6c8-130">Bu görev için programlama veya kod yoktur.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-130">For this task, there’s no programming or code.</span></span> <span data-ttu-id="5c6c8-131">Yalnızca Power BI Desktop kullanırız.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-131">We just use Power BI Desktop.</span></span>
<span data-ttu-id="5c6c8-132">Bu makalede, biz Power BI Desktop kullanma hakkında ayrıntılar gidin olmaz.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-132">In this article, we won't go through the details about how to use Power BI Desktop.</span></span> <span data-ttu-id="5c6c8-133">Bazı burada yardıma gereksinim duyarsanız, bkz: [Power BI Desktop ile çalışmaya başlama](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="5c6c8-133">If you need some help here, see [Getting started with Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span></span> <span data-ttu-id="5c6c8-134">Bizim örneğimizde, biz yalnızca kullanacağız [Retail Analysis örnek](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span><span class="sxs-lookup"><span data-stu-id="5c6c8-134">For our example, we'll just use the [Retail Analysis Sample](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span></span>

![](media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a><span data-ttu-id="5c6c8-135">Power BI çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5c6c8-135">Create a Power BI workspace</span></span>

<span data-ttu-id="5c6c8-136">Sağlama tüm yapılır, REST API'leri aracılığıyla çalışma alanı koleksiyonu, bir müşterinin çalışma oluşturmayı başlayalım.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-136">Now that the provisioning is all done, let’s get started creating a customer’s workspace in the workspace collection via REST APIs.</span></span> <span data-ttu-id="5c6c8-137">Aşağıdaki HTTP POST isteği (REST) bizim mevcut çalışma alanı koleksiyonu yeni bir çalışma alanı oluşturuyor.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-137">The following HTTP POST Request (REST) is creating the new workspace in our existing workspace collection.</span></span> <span data-ttu-id="5c6c8-138">Bu [POST çalışma API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span><span class="sxs-lookup"><span data-stu-id="5c6c8-138">This is the [POST Workspace API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span> <span data-ttu-id="5c6c8-139">Bizim örneğimizde, çalışma alanı koleksiyonu addır **mypbiapp**.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-139">In our example, the workspace collection name is **mypbiapp**.</span></span> <span data-ttu-id="5c6c8-140">Yalnızca size daha önce kopyaladığınız, erişim tuşu ayarlarız olarak **AppKey**.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-140">We just set the access key, which we previously copied, as **AppKey**.</span></span> <span data-ttu-id="5c6c8-141">Çok basit kimlik doğrulama kadar!</span><span class="sxs-lookup"><span data-stu-id="5c6c8-141">It’s very simple authentication!</span></span>

<span data-ttu-id="5c6c8-142">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="5c6c8-142">**HTTP Request**</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="5c6c8-143">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="5c6c8-143">**HTTP Response**</span></span>

```
HTTP/1.1 201 Created
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces
RequestId: 4220d385-2fb3-406b-8901-4ebe11a5f6da

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/$metadata#workspaces/$entity",
  "workspaceId": "32960a09-6366-4208-a8bb-9e0678cdbb9d",
  "workspaceCollectionName": "mypbiapp"
}
```

<span data-ttu-id="5c6c8-144">Döndürülen **Workspaceıd** aşağıdaki sonraki API çağrıları için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-144">The returned **workspaceId** is used for the following subsequent API calls.</span></span> <span data-ttu-id="5c6c8-145">Bu değer uygulamamız korumanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-145">Our application must retain this value.</span></span>

## <a name="import-pbix-file-into-the-workspace"></a><span data-ttu-id="5c6c8-146">Çalışma alanına .pbix dosyasını içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="5c6c8-146">Import .pbix file into the workspace</span></span>

<span data-ttu-id="5c6c8-147">Bir veri kümesi ile tek bir Power BI Desktop dosyası bir çalışma alanındaki her bir raporun karşılık \(veri kaynağı ayarları dahil).</span><span class="sxs-lookup"><span data-stu-id="5c6c8-147">Each report in a workspace corresponds to a single Power BI Desktop file with a dataset \(including datasource settings).</span></span> <span data-ttu-id="5c6c8-148">Aşağıdaki kodda gösterildiği gibi çalışma alanına biz bizim .pbix dosyasını içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-148">We can import our .pbix file to the workspace as shown in the code below.</span></span> <span data-ttu-id="5c6c8-149">Gördüğünüz gibi biz MIME çok bölümlü http kullanarak .pbix dosyasını ikili karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-149">As you can see, we can upload the binary of .pbix file using MIME multipart in http.</span></span>

<span data-ttu-id="5c6c8-150">URI parça **32960a09-6366-4208-a8bb-9e0678cdbb9d** Workspaceıd ve sorgu parametresi **datasetDisplayName** oluşturmak için veri kümesi adı.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-150">The uri fragment **32960a09-6366-4208-a8bb-9e0678cdbb9d** is the workspaceId, and query parameter **datasetDisplayName** is the dataset name to create.</span></span> <span data-ttu-id="5c6c8-151">Oluşturulan veri kümesini .pbix yapıları gibi dosya ilgili tüm verileri tutan içeri aktarılan veriler, veri kaynağına işaretçi olarak vb...</span><span class="sxs-lookup"><span data-stu-id="5c6c8-151">The created dataset holds all data related artifacts in .pbix file such as imported data, the pointer to the data source, etc..</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{the content (binary) of .pbix file}
--A300testx--
```

<span data-ttu-id="5c6c8-152">Bu görevi Al bir süre çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-152">This import task might run for a while.</span></span> <span data-ttu-id="5c6c8-153">Tamamlandığında, uygulamamız alma kimliğini kullanarak görev durumu sorabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-153">When complete, our application can ask the task status using import id.</span></span> <span data-ttu-id="5c6c8-154">Bizim örneğimizde içeri aktarma kimliğidir **4eec64dd-533b-47c3-a72c-6508ad854659**.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-154">In our example, the import id is **4eec64dd-533b-47c3-a72c-6508ad854659**.</span></span>

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

<span data-ttu-id="5c6c8-155">Bu içeri aktarma kimliğini kullanarak durumu aşağıdaki istemesi:</span><span class="sxs-lookup"><span data-stu-id="5c6c8-155">The following is asking status using this import id:</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="5c6c8-156">Görev tam değilse, HTTP yanıtı şöyle olabilir:</span><span class="sxs-lookup"><span data-stu-id="5c6c8-156">If the task isn't complete, the HTTP response could be like this:</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: 614a13a5-4de7-43e8-83c9-9cd225535136

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Publishing",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "name": "mydataset01"
}
```

<span data-ttu-id="5c6c8-157">Görev tamamlandığında, HTTP yanıtı şuna daha fazla olabilir:</span><span class="sxs-lookup"><span data-stu-id="5c6c8-157">If the task is complete, the HTTP response could be more like this:</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: eb2c5a85-4d7d-4cc2-b0aa-0bafee4b1606

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Succeeded",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "reports": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://app.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c"
    }
  ],
  "datasets": [
    {
      "id": "458e0451-7215-4029-80b3-9627bf3417b0",
      "name": "mydataset01",
      "tables": [
      ],
      "webUrl": "https://app.powerbi.com/datasets/458e0451-7215-4029-80b3-9627bf3417b0"
    }
  ],
  "name": "mydataset01"
}
```

## <a name="data-source-connectivity-and-multi-tenancy-of-data"></a><span data-ttu-id="5c6c8-158">Veri kaynağı bağlantısı \(ve verilerin çok kiracılı)</span><span class="sxs-lookup"><span data-stu-id="5c6c8-158">Data source connectivity \(and multi-tenancy of data)</span></span>

<span data-ttu-id="5c6c8-159">Neredeyse tüm .pbix dosyasında yapılarının bizim çalışma alanına alınırken, veri kaynaklarına ilişkin kimlik bilgilerini değildir.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-159">While almost all of the artifacts in .pbix file are imported into our workspace, the  credentials for data sources are not.</span></span> <span data-ttu-id="5c6c8-160">Kullanırken, sonuç olarak, **DirectQuery modu**, yerleşik rapor düzgün gösterilemiyor.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-160">As a result, when using **DirectQuery mode**, the embedded report cannot be shown correctly.</span></span> <span data-ttu-id="5c6c8-161">Ancak kullanırken **alma modunu**, biz varolan alınan verileri kullanarak raporu görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-161">But, when using **Import mode**, we can view the report using the existing imported data.</span></span> <span data-ttu-id="5c6c8-162">Böyle bir durumda, biz REST çağrıları aracılığıyla aşağıdaki adımları kullanarak kimlik bilgilerini ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-162">In such a case, we must set the credential using the following steps via REST calls.</span></span>

<span data-ttu-id="5c6c8-163">İlk olarak, biz ağ geçidi datasource almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-163">First, we must get the gateway datasource.</span></span> <span data-ttu-id="5c6c8-164">Veri kümesi biliyoruz **kimliği** daha önce döndürülen kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-164">We know the dataset **id** is the previously returned id.</span></span>

<span data-ttu-id="5c6c8-165">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="5c6c8-165">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.GetBoundGatewayDatasources
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="5c6c8-166">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="5c6c8-166">**HTTP Response**</span></span>

```
GET HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: 574b0b18-a6fa-46a6-826c-e65840cf6e15

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#gatewayDatasources",
  "value": [
    {
      "id": "5f7ee2e7-4851-44a1-8b75-3eb01309d0ea",
      "gatewayId": "ca17e77f-1b51-429b-b059-6b3e3e9685d1",
      "datasourceType": "Sql",
      "connectionDetails": "{\"server\":\"testserver.database.windows.net\",\"database\":\"testdb01\"}"
    }
  ]
}
```

<span data-ttu-id="5c6c8-167">Döndürülen ağ geçidi kimliği ve veri kaynağı kimliği kullanarak \(önceki bkz **gatewayId** ve **kimliği** döndürülen sonuç), bu veri kaynağının kimlik bilgisi gibi değişiklik yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5c6c8-167">Using the returned gateway id and datasource id \(see the previous **gatewayId** and **id** in the returned result), we can change the credential of this datasource as follows:</span></span>

<span data-ttu-id="5c6c8-168">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="5c6c8-168">**HTTP Request**</span></span>

```
PATCH https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/gateways/ca17e77f-1b51-429b-b059-6b3e3e9685d1/datasources/5f7ee2e7-4851-44a1-8b75-3eb01309d0ea
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "credentialType": "Basic",
  "basicCredentials": {
    "username": "demouser",
    "password": "P@ssw0rd"
  }
}
```

<span data-ttu-id="5c6c8-169">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="5c6c8-169">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
RequestId: 0e533c13-266a-4a9d-8718-fdad90391099
```

<span data-ttu-id="5c6c8-170">Üretimde biz REST API kullanarak her çalışma alanı için farklı bağlantı dizesini de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-170">In production, we can also set the different connection string for each workspace using REST API.</span></span> <span data-ttu-id="5c6c8-171">\(yani, biz veritabanı her müşteri için ayırabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="5c6c8-171">\(i.e, we can separate the database for each customers.)</span></span>

<span data-ttu-id="5c6c8-172">Aşağıdaki REST aracılığıyla veri kaynağının bağlantı dizesi değiştiriyor.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-172">The following is changing the connection string of datasource via REST.</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

<span data-ttu-id="5c6c8-173">Veya, bir rapor her kullanıcılar için veri ayırmanıza ve biz satır düzeyi güvenlik Power BI Embedded içinde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-173">Or, we can use Row Level Security in Power BI Embedded and we can separate the data for each users in one report.</span></span> <span data-ttu-id="5c6c8-174">As a Result, biz aynı .pbix her müşteri raporla sağlayabilirsiniz \(UI, vb.) ve farklı veri kaynakları.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-174">As a result, we can provision each customer report with same .pbix \(UI, etc.) and different data sources.</span></span>

> [!NOTE]
> <span data-ttu-id="5c6c8-175">Kullanıyorsanız, **alma modunu** yerine **DirectQuery modu**, API aracılığıyla modelleri yenilemek için bir yolu yoktur.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-175">If you’re using **Import mode** instead of **DirectQuery mode**, there’s no way to refresh models via API.</span></span> <span data-ttu-id="5c6c8-176">Ve Power BI ağ geçidi üzerinden şirket içi veri kaynakları henüz Power BI Embedded içinde desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-176">And, on-premises datasources through Power BI gateway isn't yet supported in Power BI Embedded.</span></span> <span data-ttu-id="5c6c8-177">Bununla birlikte, gerçekten takip istersiniz [Power BI blog](https://powerbi.microsoft.com/blog/) yenilikler ve yakında gelecek için serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-177">However, you'll really want to keep an eye on the [Power BI blog](https://powerbi.microsoft.com/blog/) for what's new and what's coming in future releases.</span></span>

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a><span data-ttu-id="5c6c8-178">Kimlik doğrulaması ve web sayfamızı (katıştırma) raporlarında barındırma</span><span class="sxs-lookup"><span data-stu-id="5c6c8-178">Authentication and hosting (embedding) reports in our web page</span></span>

<span data-ttu-id="5c6c8-179">Önceki REST API biz erişim tuşunu kullanabilirsiniz **AppKey** authorization üstbilgisi olarak kendisini.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-179">In the previous REST API, we can use the access key **AppKey** itself as the authorization header.</span></span> <span data-ttu-id="5c6c8-180">Bu çağrı arka uç sunucu tarafında işlenebilir çünkü güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-180">Because these calls can be handled on the backend server side, it's safe.</span></span>

<span data-ttu-id="5c6c8-181">Ancak, biz web sayfamızı rapor ekleme, bu tür güvenlik bilgileri JavaScript kullanarak ele alınması \(ön uç).</span><span class="sxs-lookup"><span data-stu-id="5c6c8-181">But, when we embed the report in our web page, this kind of security information would be handled using JavaScript \(frontend).</span></span> <span data-ttu-id="5c6c8-182">Ardından kimlik doğrulaması üstbilgi değeri güvenli hale getirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-182">Then the authorization header value must be secured.</span></span> <span data-ttu-id="5c6c8-183">Bizim erişim tuşu kötü amaçlı kullanıcı ya da kötü amaçlı kod tarafından bulunmuşsa, bunlar bu anahtarı kullanarak herhangi bir işlem çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-183">If our access key is discovered by a malicious user or malicious code, they can call any operations using this key.</span></span>

<span data-ttu-id="5c6c8-184">Biz web sayfamızı rapor ekleme, hesaplanan belirtecin erişim tuşu yerine kullanırız gerekir **AppKey**.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-184">When we embed the report in our web page, we must use the computed token instead of access key **AppKey**.</span></span> <span data-ttu-id="5c6c8-185">Uygulamamız OAuth Json Web belirteci oluşturmak \(JWT) talepleri ve hesaplanan dijital imzadan oluşur.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-185">Our application must create the OAuth Json Web Token \(JWT) which consists of the claims and the computed digital signature.</span></span> <span data-ttu-id="5c6c8-186">Aşağıda gösterildiği gibi bu OAuth JWT nokta ayrılmış kodlu bir dize belirteçleri gereklidir.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-186">As illustrated below, this OAuth JWT is dot-delimited encoded string tokens.</span></span>

![](media/power-bi-embedded-iframe/oauth-jwt.png)

<span data-ttu-id="5c6c8-187">İlk olarak, biz daha sonra oturum giriş değeri hazırlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-187">First, we must prepare the input value, which is signed later.</span></span> <span data-ttu-id="5c6c8-188">Bu değer aşağıdaki json Base64 ile kodlanmış URL'si (rfc4648) dizesi ve bunlar noktayla ayrılmış \(.) karakter.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-188">This value is the base64 url encoded (rfc4648) string of the following json, and these are delimited by the dot \(.) character.</span></span> <span data-ttu-id="5c6c8-189">Daha sonra rapor kimliği alma açıklayacağız.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-189">Later, we'll explain how to get the report id.</span></span>

> [!NOTE]
> <span data-ttu-id="5c6c8-190">Biz satır düzeyi güvenlik (RLS) Power BI Embedded ile kullanmak istiyorsanız, biz de belirtmeniz gerekir **kullanıcıadı** ve **rolleri** taleplerdeki.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-190">If we want to use Row Level Security (RLS) with Power BI Embedded, we must also specify **username** and **roles** in the claims.</span></span>

```
{
  "typ":"JWT",
  "alg":"HS256"
}
```

```
{
  "wid":"{workspace id}",
  "rid":"{report id}",
  "wcn":"{workspace collection name}",
  "iss":"PowerBISDK",
  "ver":"0.2.0",
  "aud":"https://analysis.windows.net/powerbi/api",
  "nbf":{start time of token expiration},
  "exp":{end time of token expiration}
}
```

<span data-ttu-id="5c6c8-191">Ardından, biz base64 kodlu dize HMAC oluşturmalısınız \(imza) SHA256 algoritmasını ile.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-191">Next, we must create the base64 encoded string of HMAC \(the signature) with SHA256 algorithm.</span></span> <span data-ttu-id="5c6c8-192">Bu imzalı giriş önceki dize değeridir.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-192">This signed input value is the previous string.</span></span>

<span data-ttu-id="5c6c8-193">Son olarak, biz nokta kullanarak giriş değeri ve imza dizesi birleştirmeniz gerekir \(.) karakter.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-193">Last, we must combine the input value and signature string using period \(.) character.</span></span> <span data-ttu-id="5c6c8-194">Rapor katıştırmak için uygulama belirtecinde tamamlanmış dizesidir.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-194">The completed string is the app token for the report embedding.</span></span> <span data-ttu-id="5c6c8-195">Kötü niyetli bir kullanıcı tarafından uygulama belirtecinde bulunan olsa bile özgün erişim tuşu elde edilemiyor.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-195">Even if the app token is discovered by a malicious user, they cannot get the original access key.</span></span> <span data-ttu-id="5c6c8-196">Bu uygulama belirteci hızlı bir şekilde sona erecek.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-196">This app token will expire quickly.</span></span>

<span data-ttu-id="5c6c8-197">Bir PHP örnek için aşağıdaki adımları şöyledir:</span><span class="sxs-lookup"><span data-stu-id="5c6c8-197">Here's a PHP example for these steps:</span></span>

```
<?php
// 1. power bi access key
$accesskey = "MpaUgrTv5e...";

// 2. construct input value
$token1 = "{" .
  "\"typ\":\"JWT\"," .
  "\"alg\":\"HS256\"" .
  "}";
$token2 = "{" .
  "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
  "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
  "\"wcn\":\"mypbiapp\"," . // workspace collection name
  "\"iss\":\"PowerBISDK\"," .
  "\"ver\":\"0.2.0\"," .
  "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
  "\"nbf\":" . date("U") . "," .
  "\"exp\":" . date("U" , strtotime("+1 hour")) .
  "}";
$inputval = rfc4648_base64_encode($token1) .
  "." .
  rfc4648_base64_encode($token2);

// 3. get encoded signature
$hash = hash_hmac("sha256",
    $inputval,
    $accesskey,
    true);
$sig = rfc4648_base64_encode($hash);

// 4. show result (which is the apptoken)
$apptoken = $inputval . "." . $sig;
echo($apptoken);

// helper functions
function rfc4648_base64_encode($arg) {
  $res = $arg;
  $res = base64_encode($res);
  $res = str_replace("/", "_", $res);
  $res = str_replace("+", "-", $res);
  $res = rtrim($res, "=");
  return $res;
}
?>
```

## <a name="finally-embed-the-report-into-the-web-page"></a><span data-ttu-id="5c6c8-198">Son olarak, web sayfasına rapor ekleme</span><span class="sxs-lookup"><span data-stu-id="5c6c8-198">Finally, embed the report into the web page</span></span>

<span data-ttu-id="5c6c8-199">Bizim rapor katıştırmak için biz embed url ve rapor almalısınız **kimliği** aşağıdaki REST API kullanarak.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-199">For embedding our report, we must get the embed url and report **id** using the following REST API.</span></span>

<span data-ttu-id="5c6c8-200">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="5c6c8-200">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/reports
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="5c6c8-201">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="5c6c8-201">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: d4099022-405b-49d3-b3b7-3c60cf675958

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#reports",
  "value": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c",
      "isFromPbix": false
    }
  ]
}
```

<span data-ttu-id="5c6c8-202">Biz raporu web uygulamamız önceki uygulama belirteci kullanılarak eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-202">We can embed the report in our web app using the previous app token.</span></span>
<span data-ttu-id="5c6c8-203">Biz sonraki örnek kodu bakarsanız, önceki bölümü önceki örnek ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-203">If we look at the next sample code, the former part is the same as the previous example.</span></span> <span data-ttu-id="5c6c8-204">İkinci bölümü, bu örnek göstermektedir **embedUrl** \(önceki sonuçları görmek) IFRAME içinde ve uygulama belirteci IFRAME gönderme.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-204">In the latter part, this sample shows the **embedUrl** \(see the previous result) in the iframe, and is posting the app token into the iframe.</span></span>

> [!NOTE]
> <span data-ttu-id="5c6c8-205">Rapor Kimliği değeri, kendi birine değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-205">You'll need to change the report id value to one of your own.</span></span> <span data-ttu-id="5c6c8-206">Ayrıca, içerik yönetimi sistemimizde bir hata nedeniyle kod örnek IFRAME etiketinde tam anlamıyla okunur.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-206">Also, due to a bug in our content management system, the iframe tag in the code sample is read literally.</span></span> <span data-ttu-id="5c6c8-207">Bu örnek kodu kopyalayıp capped metin etiketinden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-207">Remove the capped text from the tag if you copy and paste this sample code.</span></span>

```
    <?php
    // 1. power bi access key
    $accesskey = "MpaUgrTv5e...";

    // 2. construct input value
    $token1 = "{" .
      "\"typ\":\"JWT\"," .
      "\"alg\":\"HS256\"" .
      "}";
    $token2 = "{" .
      "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
      "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
      "\"wcn\":\"mypbiapp\"," . // workspace collection name
      "\"iss\":\"PowerBISDK\"," .
      "\"ver\":\"0.2.0\"," .
      "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
      "\"nbf\":" . date("U") . "," .
      "\"exp\":" . date("U" , strtotime("+1 hour")) .
      "}";
    $inputval = rfc4648_base64_encode($token1) .
      "." .
      rfc4648_base64_encode($token2);

    // 3. get encoded signature value
    $hash = hash_hmac("sha256",
        $inputval,
        $accesskey,
        true);
    $sig = rfc4648_base64_encode($hash);

    // 4. get apptoken
    $apptoken = $inputval . "." . $sig;

    // helper functions
    function rfc4648_base64_encode($arg) {
      $res = $arg;
      $res = base64_encode($res);
      $res = str_replace("/", "_", $res);
      $res = str_replace("+", "-", $res);
      $res = rtrim($res, "=");
      return $res;
    }
    ?>
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <title>Test page</title>
      <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
      <button id="btnView">View Report !</button>
      <div id="divView">
        <**REMOVE THIS CAPPED TEXT IF COPIED** iframe id="ifrTile" width="100%" height="400"></iframe>
      </div>
      <script>
        (function () {
          document.getElementById('btnView').onclick = function() {
            var iframe = document.getElementById('ifrTile');
            iframe.src = 'https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c';
            iframe.onload = function() {
              var msgJson = {
                action: "loadReport",
                accessToken: "<?=$apptoken?>",
                height: 500,
                width: 722
              };
              var msgTxt = JSON.stringify(msgJson);
              iframe.contentWindow.postMessage(msgTxt, "*");
            };
          };
        }());
      </script>
    </body>
```

<span data-ttu-id="5c6c8-208">Ve bizim sonuç şöyledir:</span><span class="sxs-lookup"><span data-stu-id="5c6c8-208">And here's our result:</span></span>

![](media/power-bi-embedded-iframe/view-report.png)

<span data-ttu-id="5c6c8-209">Şu anda Power BI Embedded yalnızca rapor IFRAME gösterir.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-209">At this time, Power BI Embedded only shows the report in the iframe.</span></span> <span data-ttu-id="5c6c8-210">Ancak, bir göz açık tutmak [Power BI Blog](https://powerbi.microsoft.com/blog/).</span><span class="sxs-lookup"><span data-stu-id="5c6c8-210">But, keep an eye on the [Power BI Blog](https://powerbi.microsoft.com/blog/).</span></span> <span data-ttu-id="5c6c8-211">Gelecekteki geliştirmeleri, yeni istemci tarafı bize IFRAME bilgiyi yanı sıra bilgi alacağınızı API'leri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-211">Future improvements could use new client side APIs that will let us send information into the iframe as well as get information out.</span></span> <span data-ttu-id="5c6c8-212">Heyecan verici şeyler!</span><span class="sxs-lookup"><span data-stu-id="5c6c8-212">Exciting stuff!</span></span>

## <a name="see-also"></a><span data-ttu-id="5c6c8-213">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="5c6c8-213">See also</span></span>
* [<span data-ttu-id="5c6c8-214">Power BI Embedded ile kimlik doğrulaması ve yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="5c6c8-214">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)

<span data-ttu-id="5c6c8-215">Başka sorunuz mu var?</span><span class="sxs-lookup"><span data-stu-id="5c6c8-215">More questions?</span></span> [<span data-ttu-id="5c6c8-216">Power BI Topluluğu'nu deneyin</span><span class="sxs-lookup"><span data-stu-id="5c6c8-216">Try the Power BI Community</span></span>](http://community.powerbi.com/)

