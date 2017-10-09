---
title: Power BI Embedded REST ile aaaHow toouse | Microsoft Docs
description: "Bilgi nasıl toouse Power BI Embedded REST ile "
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
ms.openlocfilehash: 98057724e60ba868f9c93de8c50383569eb8852d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-power-bi-embedded-with-rest"></a><span data-ttu-id="0a6ba-103">Nasıl toouse Power BI Embedded REST ile</span><span class="sxs-lookup"><span data-stu-id="0a6ba-103">How toouse Power BI Embedded with REST</span></span>

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a><span data-ttu-id="0a6ba-104">Power BI Embedded: Nedir ve ne işe yaradığını</span><span class="sxs-lookup"><span data-stu-id="0a6ba-104">Power BI Embedded: What it is and what it's for</span></span>

<span data-ttu-id="0a6ba-105">Power BI Embedded genel bakış hello resmi açıklanan [Power BI Embedded site](https://azure.microsoft.com/services/power-bi-embedded/), ancak REST ile kullanma hakkında ayrıntılar hello içine ulaşmadan hızlı bir göz atalım.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-105">An overview of Power BI Embedded is described in hello official [Power BI Embedded site](https://azure.microsoft.com/services/power-bi-embedded/), but let's take a quick look before we get into hello details about using it with REST.</span></span>

<span data-ttu-id="0a6ba-106">Gerçekten oldukça basit.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-106">It's quite simple, really.</span></span> <span data-ttu-id="0a6ba-107">toouse hello dinamik veri Görselleştirmelerini isteyebilirsiniz [Power BI](https://powerbi.microsoft.com) kendi uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-107">you may want toouse hello dynamic data visualizations of [Power BI](https://powerbi.microsoft.com) in your own application.</span></span>

<span data-ttu-id="0a6ba-108">Özel uygulamaların çoğu toodeliver hello veri mutlaka kendi kuruluşunuzdaki kullanıcılar kendi müşteriler için gerekir.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-108">Most custom applications need toodeliver hello data for their own customers, not necessarily users in their own organization.</span></span> <span data-ttu-id="0a6ba-109">Şirket A ve B şirketi için bazı hizmet sunma, örneğin, Şirket A kullanıcılar yalnızca veri kendi Şirket A'daki görmeniz gerekir Diğer bir deyişle, hello çoklu kiracı hello teslimat için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-109">For example, if you're delivering some service for both company A and company B, users in company A should only see data for their own company A. That is, hello multi-tenancy is needed for hello delivery.</span></span>

<span data-ttu-id="0a6ba-110">Merhaba özel uygulama, form kimlik doğrulama, temel kimlik doğrulama vb. gibi kendi kimlik doğrulama yöntemleri de sunumu..</span><span class="sxs-lookup"><span data-stu-id="0a6ba-110">hello custom application might also be offering its own authentication methods such as forms auth, basic auth, etc..</span></span> <span data-ttu-id="0a6ba-111">Ardından, çözüm katıştırma hello var olan bu kimlik doğrulama yöntemleri ile güvenli bir şekilde işbirliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-111">Then, hello embedding solution must collaborate with this existing authentication methods safely.</span></span> <span data-ttu-id="0a6ba-112">Ayrıca kullanıcılar toobe mümkün toouse için gerekli olan bu ISV uygulamaları olmadan hello fazladan satınalma ya da bir Power BI aboneliği lisans.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-112">It's also necessary for users toobe able toouse those ISV applications without hello extra purchase or licensing of a Power BI subscription.</span></span>

 <span data-ttu-id="0a6ba-113">**Power BI Embedded** tam olarak bu tür senaryoları için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-113">**Power BI Embedded** is designed for precisely these kinds of scenarios.</span></span> <span data-ttu-id="0a6ba-114">Bu nedenle, biz Bu hızlı giriş hello yolu dışında sahip olduğunuza göre şimdi bazı ayrıntılar alın</span><span class="sxs-lookup"><span data-stu-id="0a6ba-114">So, now that we have that quick introduction out of hello way, let's get into some details</span></span>

<span data-ttu-id="0a6ba-115">Merhaba .NET kullanabilirsiniz \(C#) veya Node.js SDK'sı, tooeasily Power BI Embedded ile uygulamanızı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-115">You can use hello .NET \(C#) or Node.js SDK, tooeasily build your application with Power BI Embedded.</span></span> <span data-ttu-id="0a6ba-116">Ancak, bu makalede, HTTP akışı hakkında açıklayacağız \(dahil AuthN) SDK'ları olmadan Power BI.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-116">But, in this article, we'll explain about HTTP flow \(incl. AuthN) of Power BI without SDKs.</span></span> <span data-ttu-id="0a6ba-117">Bu akış anlama, uygulamanızı oluşturabilir **herhangi bir programlama dili ile**, ve Power BI Embedded hello özünü derine anlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-117">Understanding this flow, you can build your application **with any programming language**, and you can understand deeply hello essence of Power BI Embedded.</span></span>

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a><span data-ttu-id="0a6ba-118">Power BI oluşturma çalışma alanı koleksiyonu ve get erişim tuşu \(hazırlama)</span><span class="sxs-lookup"><span data-stu-id="0a6ba-118">Create Power BI workspace collection, and get access key \(Provisioning)</span></span>

<span data-ttu-id="0a6ba-119">Power BI Embedded hello Azure Hizmetleri biridir.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-119">Power BI Embedded is one of hello Azure services.</span></span> <span data-ttu-id="0a6ba-120">Yalnızca hello Azure Portal kullanan ISV kullanım ücretleri için ücret \(saatlik kullanıcı oturumu başına), ve doldurulmamış veya hatta görünümleri hello rapor olmayan hello kullanıcının gerektiren bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-120">Only hello ISV who uses Azure Portal is charged for usage fees \(per hourly user session), and hello user who views hello report isn't charged or even require an Azure subscription.</span></span>
<span data-ttu-id="0a6ba-121">Bizim uygulama geliştirme başlatmadan önce biz hello oluşturmalısınız **Power BI çalışma alanı koleksiyonu** Azure portalını kullanarak.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-121">Before starting our application development, we must create hello **Power BI workspace collection** by using Azure Portal.</span></span>

<span data-ttu-id="0a6ba-122">Hello çalışma (Kiracı) her müşteri için Power BI Embedded her çalışma alanıdır ve her çalışma alanı koleksiyonu birçok çalışma alanları ekleyebiliriz.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-122">Each workspace of Power BI Embedded is hello workspace for each customer (tenant), and we can add many workspaces in each workspace collection.</span></span> <span data-ttu-id="0a6ba-123">Merhaba aynı erişim tuşu her çalışma alanı koleksiyonu kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-123">hello same access key is used in each workspace collection.</span></span> <span data-ttu-id="0a6ba-124">İçinde etkisi, Power BI Embedded için hello güvenlik sınırı hello çalışma koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-124">In-effect, hello workspace collection is hello security boundary for Power BI Embedded.</span></span>

![](media/power-bi-embedded-iframe/create-workspace.png)

<span data-ttu-id="0a6ba-125">Merhaba çalışma alanı koleksiyonu oluşturma sona erdiğinde hello erişim tuşunu Azure Portal'dan kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-125">When we finish creating hello workspace collection, copy hello access key from Azure Portal.</span></span>

![](media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> <span data-ttu-id="0a6ba-126">Biz de hello çalışma alanı koleksiyonu sağlayabilir ve erişim anahtarı REST API aracılığıyla alın.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-126">We can also provision hello workspace collection and get access key via REST API.</span></span> <span data-ttu-id="0a6ba-127">toolearn daha, fazla [Power BI kaynak sağlayıcısı API'leri](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span><span class="sxs-lookup"><span data-stu-id="0a6ba-127">toolearn more, see [Power BI Resource Provider APIs](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span></span>

## <a name="create-pbix-file-with-power-bi-desktop"></a><span data-ttu-id="0a6ba-128">Power BI Desktop ile .pbix dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="0a6ba-128">Create .pbix file with Power BI Desktop</span></span>

<span data-ttu-id="0a6ba-129">Ardından, biz hello veri bağlantısı ve katıştırılmış raporları toobe oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-129">Next, we must create hello data connection and reports toobe embedded.</span></span>
<span data-ttu-id="0a6ba-130">Bu görev için programlama veya kod yoktur.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-130">For this task, there’s no programming or code.</span></span> <span data-ttu-id="0a6ba-131">Yalnızca Power BI Desktop kullanırız.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-131">We just use Power BI Desktop.</span></span>
<span data-ttu-id="0a6ba-132">Bu makalede, biz hello ayrıntıları Git olmaz toouse Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-132">In this article, we won't go through hello details about how toouse Power BI Desktop.</span></span> <span data-ttu-id="0a6ba-133">Bazı burada yardıma gereksinim duyarsanız, bkz: [Power BI Desktop ile çalışmaya başlama](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="0a6ba-133">If you need some help here, see [Getting started with Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span></span> <span data-ttu-id="0a6ba-134">Bizim örneğimizde, yalnızca hello kullanacağız [Retail Analysis örnek](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span><span class="sxs-lookup"><span data-stu-id="0a6ba-134">For our example, we'll just use hello [Retail Analysis Sample](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span></span>

![](media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a><span data-ttu-id="0a6ba-135">Power BI çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0a6ba-135">Create a Power BI workspace</span></span>

<span data-ttu-id="0a6ba-136">Merhaba sağlama tüm yapılır, REST API'leri aracılığıyla hello çalışma alanı koleksiyonu, bir müşterinin çalışma oluşturmayı başlayalım.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-136">Now that hello provisioning is all done, let’s get started creating a customer’s workspace in hello workspace collection via REST APIs.</span></span> <span data-ttu-id="0a6ba-137">Merhaba aşağıdaki HTTP POST isteği (REST) hello yeni çalışma bizim mevcut çalışma alanı koleksiyonu oluşturuyor.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-137">hello following HTTP POST Request (REST) is creating hello new workspace in our existing workspace collection.</span></span> <span data-ttu-id="0a6ba-138">Merhaba budur [POST çalışma API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span><span class="sxs-lookup"><span data-stu-id="0a6ba-138">This is hello [POST Workspace API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span> <span data-ttu-id="0a6ba-139">Bizim örneğimizde, hello çalışma alanı koleksiyonu adı olan **mypbiapp**.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-139">In our example, hello workspace collection name is **mypbiapp**.</span></span> <span data-ttu-id="0a6ba-140">Yalnızca size daha önce kopyaladığınız, hello erişim tuşu ayarlarız olarak **AppKey**.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-140">We just set hello access key, which we previously copied, as **AppKey**.</span></span> <span data-ttu-id="0a6ba-141">Çok basit kimlik doğrulama kadar!</span><span class="sxs-lookup"><span data-stu-id="0a6ba-141">It’s very simple authentication!</span></span>

<span data-ttu-id="0a6ba-142">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="0a6ba-142">**HTTP Request**</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="0a6ba-143">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="0a6ba-143">**HTTP Response**</span></span>

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

<span data-ttu-id="0a6ba-144">döndürülen hello **Workspaceıd** sonraki API çağrıları aşağıdaki hello için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-144">hello returned **workspaceId** is used for hello following subsequent API calls.</span></span> <span data-ttu-id="0a6ba-145">Bu değer uygulamamız korumanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-145">Our application must retain this value.</span></span>

## <a name="import-pbix-file-into-hello-workspace"></a><span data-ttu-id="0a6ba-146">.Pbix dosyasını hello çalışma alanınıza alın</span><span class="sxs-lookup"><span data-stu-id="0a6ba-146">Import .pbix file into hello workspace</span></span>

<span data-ttu-id="0a6ba-147">Bir çalışma alanındaki her bir raporun tooa tek Power BI Desktop dosyası bir veri kümesi ile karşılık gelen \(veri kaynağı ayarları dahil).</span><span class="sxs-lookup"><span data-stu-id="0a6ba-147">Each report in a workspace corresponds tooa single Power BI Desktop file with a dataset \(including datasource settings).</span></span> <span data-ttu-id="0a6ba-148">Biz hello kodda aşağıda gösterildiği gibi bizim .pbix dosyası toohello çalışma içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-148">We can import our .pbix file toohello workspace as shown in hello code below.</span></span> <span data-ttu-id="0a6ba-149">Gördüğünüz gibi biz hello İkili MIME çok bölümlü http kullanarak .pbix dosyasının karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-149">As you can see, we can upload hello binary of .pbix file using MIME multipart in http.</span></span>

<span data-ttu-id="0a6ba-150">Merhaba URI parça **32960a09-6366-4208-a8bb-9e0678cdbb9d** hello Workspaceıd ve sorgu parametresi **datasetDisplayName** hello veri kümesi adı toocreate değil.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-150">hello uri fragment **32960a09-6366-4208-a8bb-9e0678cdbb9d** is hello workspaceId, and query parameter **datasetDisplayName** is hello dataset name toocreate.</span></span> <span data-ttu-id="0a6ba-151">oluşturulan hello dataset tutan ilgili tüm verileri yapıları .pbix dosyasında alınan verileri gibi hello işaretçi toohello veri kaynağı, vb...</span><span class="sxs-lookup"><span data-stu-id="0a6ba-151">hello created dataset holds all data related artifacts in .pbix file such as imported data, hello pointer toohello data source, etc..</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{hello content (binary) of .pbix file}
--A300testx--
```

<span data-ttu-id="0a6ba-152">Bu görevi Al bir süre çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-152">This import task might run for a while.</span></span> <span data-ttu-id="0a6ba-153">Tamamlandığında, uygulamamız hello görev durumu alma kimliğini kullanarak sorabilirsiniz. Bizim örneğimizde, hello alma kimliğidir **4eec64dd-533b-47c3-a72c-6508ad854659**.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-153">When complete, our application can ask hello task status using import id. In our example, hello import id is **4eec64dd-533b-47c3-a72c-6508ad854659**.</span></span>

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

<span data-ttu-id="0a6ba-154">Merhaba aşağıdaki bu içeri aktarma kimliği kullanarak durumunu soran:</span><span class="sxs-lookup"><span data-stu-id="0a6ba-154">hello following is asking status using this import id:</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="0a6ba-155">Merhaba görev tam değilse, HTTP yanıtı hello şöyle olabilir:</span><span class="sxs-lookup"><span data-stu-id="0a6ba-155">If hello task isn't complete, hello HTTP response could be like this:</span></span>

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

<span data-ttu-id="0a6ba-156">Merhaba görev tamamlandığında, hello HTTP yanıtı şuna daha fazla olabilir:</span><span class="sxs-lookup"><span data-stu-id="0a6ba-156">If hello task is complete, hello HTTP response could be more like this:</span></span>

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

## <a name="data-source-connectivity-and-multi-tenancy-of-data"></a><span data-ttu-id="0a6ba-157">Veri kaynağı bağlantısı \(ve verilerin çok kiracılı)</span><span class="sxs-lookup"><span data-stu-id="0a6ba-157">Data source connectivity \(and multi-tenancy of data)</span></span>

<span data-ttu-id="0a6ba-158">Neredeyse tüm .pbix dosyasında hello yapılarının bizim çalışma alanına alınırken, veri kaynaklarına hello kimlik bilgilerini değildir.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-158">While almost all of hello artifacts in .pbix file are imported into our workspace, hello  credentials for data sources are not.</span></span> <span data-ttu-id="0a6ba-159">Kullanırken, sonuç olarak, **DirectQuery modu**, hello yerleşik rapor düzgün gösterilemiyor.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-159">As a result, when using **DirectQuery mode**, hello embedded report cannot be shown correctly.</span></span> <span data-ttu-id="0a6ba-160">Ancak kullanırken **alma modunu**, biz hello varolan alınan verileri kullanarak hello raporu görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-160">But, when using **Import mode**, we can view hello report using hello existing imported data.</span></span> <span data-ttu-id="0a6ba-161">Böyle bir durumda, biz hello kimlik bilgisi hello REST çağrıları aşağıdaki adımları kullanarak ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-161">In such a case, we must set hello credential using hello following steps via REST calls.</span></span>

<span data-ttu-id="0a6ba-162">İlk olarak, biz hello ağ geçidi datasource almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-162">First, we must get hello gateway datasource.</span></span> <span data-ttu-id="0a6ba-163">Merhaba dataset biliyoruz **kimliği** hello önceden kimliği döndürülür.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-163">We know hello dataset **id** is hello previously returned id.</span></span>

<span data-ttu-id="0a6ba-164">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="0a6ba-164">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.GetBoundGatewayDatasources
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="0a6ba-165">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="0a6ba-165">**HTTP Response**</span></span>

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

<span data-ttu-id="0a6ba-166">Hello kullanarak döndürülen ağ geçidi kimliği ve veri kaynağı kimliği \(hello önceki bkz **gatewayId** ve **kimliği** hello sonuç döndürdü), bu veri kaynağının hello kimlik bilgisi gibi değişiklik yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0a6ba-166">Using hello returned gateway id and datasource id \(see hello previous **gatewayId** and **id** in hello returned result), we can change hello credential of this datasource as follows:</span></span>

<span data-ttu-id="0a6ba-167">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="0a6ba-167">**HTTP Request**</span></span>

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

<span data-ttu-id="0a6ba-168">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="0a6ba-168">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
RequestId: 0e533c13-266a-4a9d-8718-fdad90391099
```

<span data-ttu-id="0a6ba-169">Üretimde biz hello farklı bir bağlantı dizesi REST API kullanarak her çalışma alanı için de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-169">In production, we can also set hello different connection string for each workspace using REST API.</span></span> <span data-ttu-id="0a6ba-170">\(yani, biz hello veritabanı her müşteri için ayırabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="0a6ba-170">\(i.e, we can separate hello database for each customers.)</span></span>

<span data-ttu-id="0a6ba-171">Merhaba aşağıdaki hello bağlantı dizesi REST aracılığıyla veri kaynağının değiştiriyor.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-171">hello following is changing hello connection string of datasource via REST.</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

<span data-ttu-id="0a6ba-172">Veya, biz hello veri bir rapordaki her kullanıcı için ayrı ve biz satır düzeyi güvenlik Power BI Embedded kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-172">Or, we can use Row Level Security in Power BI Embedded and we can separate hello data for each users in one report.</span></span> <span data-ttu-id="0a6ba-173">As a Result, biz aynı .pbix her müşteri raporla sağlayabilirsiniz \(UI, vb.) ve farklı veri kaynakları.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-173">As a result, we can provision each customer report with same .pbix \(UI, etc.) and different data sources.</span></span>

> [!NOTE]
> <span data-ttu-id="0a6ba-174">Kullanıyorsanız, **alma modunu** yerine **DirectQuery modu**, hiçbir şekilde toorefresh modeli API aracılığıyla yoktur.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-174">If you’re using **Import mode** instead of **DirectQuery mode**, there’s no way toorefresh models via API.</span></span> <span data-ttu-id="0a6ba-175">Ve Power BI ağ geçidi üzerinden şirket içi veri kaynakları henüz Power BI Embedded içinde desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-175">And, on-premises datasources through Power BI gateway isn't yet supported in Power BI Embedded.</span></span> <span data-ttu-id="0a6ba-176">Ancak, gerçekten tookeep hello sayfasındaki tercih edersiniz [Power BI blog](https://powerbi.microsoft.com/blog/) yenilikler ve yakında gelecek için serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-176">However, you'll really want tookeep an eye on hello [Power BI blog](https://powerbi.microsoft.com/blog/) for what's new and what's coming in future releases.</span></span>

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a><span data-ttu-id="0a6ba-177">Kimlik doğrulaması ve web sayfamızı (katıştırma) raporlarında barındırma</span><span class="sxs-lookup"><span data-stu-id="0a6ba-177">Authentication and hosting (embedding) reports in our web page</span></span>

<span data-ttu-id="0a6ba-178">İçinde önceki REST API Merhaba, hello erişim tuşu kullanırız **AppKey** hello authorization üstbilgisi olarak kendisini.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-178">In hello previous REST API, we can use hello access key **AppKey** itself as hello authorization header.</span></span> <span data-ttu-id="0a6ba-179">Bu çağrıları hello arka uç sunucu tarafında ele alınması için güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-179">Because these calls can be handled on hello backend server side, it's safe.</span></span>

<span data-ttu-id="0a6ba-180">Ancak, biz web sayfamızı hello rapor ekleme, bu tür güvenlik bilgileri JavaScript kullanarak ele alınması \(ön uç).</span><span class="sxs-lookup"><span data-stu-id="0a6ba-180">But, when we embed hello report in our web page, this kind of security information would be handled using JavaScript \(frontend).</span></span> <span data-ttu-id="0a6ba-181">Ardından hello kimlik doğrulaması üstbilgi değeri güvenli hale getirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-181">Then hello authorization header value must be secured.</span></span> <span data-ttu-id="0a6ba-182">Bizim erişim tuşu kötü amaçlı kullanıcı ya da kötü amaçlı kod tarafından bulunmuşsa, bunlar bu anahtarı kullanarak herhangi bir işlem çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-182">If our access key is discovered by a malicious user or malicious code, they can call any operations using this key.</span></span>

<span data-ttu-id="0a6ba-183">Biz web sayfamızı hello rapor ekleme, biz hello hesaplanan belirteci erişim tuşu yerine kullanmalısınız **AppKey**.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-183">When we embed hello report in our web page, we must use hello computed token instead of access key **AppKey**.</span></span> <span data-ttu-id="0a6ba-184">Uygulamamız hello OAuth Json Web belirteci oluşturmanız gerekir \(JWT) hello talep ve hello hesaplanan dijital imzadan oluşur.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-184">Our application must create hello OAuth Json Web Token \(JWT) which consists of hello claims and hello computed digital signature.</span></span> <span data-ttu-id="0a6ba-185">Aşağıda gösterildiği gibi bu OAuth JWT nokta ayrılmış kodlu bir dize belirteçleri gereklidir.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-185">As illustrated below, this OAuth JWT is dot-delimited encoded string tokens.</span></span>

![](media/power-bi-embedded-iframe/oauth-jwt.png)

<span data-ttu-id="0a6ba-186">İlk olarak, biz daha sonra imzalı hello giriş değeri hazırlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-186">First, we must prepare hello input value, which is signed later.</span></span> <span data-ttu-id="0a6ba-187">Bu değer hello Base64 ile kodlanmış URL'si (rfc4648) json aşağıdaki hello dizesidir ve bunlar hello noktayla ayrılmış \(.) karakter.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-187">This value is hello base64 url encoded (rfc4648) string of hello following json, and these are delimited by hello dot \(.) character.</span></span> <span data-ttu-id="0a6ba-188">Daha sonra nasıl tooget hello rapor kimliği açıklayacağız.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-188">Later, we'll explain how tooget hello report id.</span></span>

> [!NOTE]
> <span data-ttu-id="0a6ba-189">Biz toouse Power BI Embedded ile satır düzeyi güvenlik (RLS) isterseniz, biz de belirtmeniz gerekir **kullanıcıadı** ve **rolleri** hello taleplerdeki.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-189">If we want toouse Row Level Security (RLS) with Power BI Embedded, we must also specify **username** and **roles** in hello claims.</span></span>

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

<span data-ttu-id="0a6ba-190">Ardından, biz hello base64 kodlu dize HMAC oluşturmalısınız \(hello imza) SHA256 algoritmasını ile.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-190">Next, we must create hello base64 encoded string of HMAC \(hello signature) with SHA256 algorithm.</span></span> <span data-ttu-id="0a6ba-191">Bu imzalı giriş hello önceki dize değeridir.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-191">This signed input value is hello previous string.</span></span>

<span data-ttu-id="0a6ba-192">Son olarak, biz hello giriş değeri ve imza dize nokta kullanarak birleştirmeniz gerekir \(.) karakter.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-192">Last, we must combine hello input value and signature string using period \(.) character.</span></span> <span data-ttu-id="0a6ba-193">Tamamlanan Merhaba, rapor hello katıştırmak için hello uygulama belirteci dizesidir.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-193">hello completed string is hello app token for hello report embedding.</span></span> <span data-ttu-id="0a6ba-194">Merhaba uygulama belirteci kötü niyetli bir kullanıcı tarafından bulunan olsa bile, bunlar hello özgün erişim anahtarı alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-194">Even if hello app token is discovered by a malicious user, they cannot get hello original access key.</span></span> <span data-ttu-id="0a6ba-195">Bu uygulama belirteci hızlı bir şekilde sona erecek.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-195">This app token will expire quickly.</span></span>

<span data-ttu-id="0a6ba-196">Bir PHP örnek için aşağıdaki adımları şöyledir:</span><span class="sxs-lookup"><span data-stu-id="0a6ba-196">Here's a PHP example for these steps:</span></span>

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

// 4. show result (which is hello apptoken)
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

## <a name="finally-embed-hello-report-into-hello-web-page"></a><span data-ttu-id="0a6ba-197">Son olarak, hello web sayfasına hello rapor ekleme</span><span class="sxs-lookup"><span data-stu-id="0a6ba-197">Finally, embed hello report into hello web page</span></span>

<span data-ttu-id="0a6ba-198">Bizim rapor katıştırmak için biz hello almalısınız url ve rapor katıştırmak **kimliği** REST API aşağıdaki hello kullanarak.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-198">For embedding our report, we must get hello embed url and report **id** using hello following REST API.</span></span>

<span data-ttu-id="0a6ba-199">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="0a6ba-199">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/reports
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="0a6ba-200">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="0a6ba-200">**HTTP Response**</span></span>

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

<span data-ttu-id="0a6ba-201">Biz hello rapor web uygulamamız hello önceki uygulama belirteci kullanılarak eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-201">We can embed hello report in our web app using hello previous app token.</span></span>
<span data-ttu-id="0a6ba-202">Biz hello sonraki örnek kodu bakarsanız, hello eski parçası olan hello hello önceki örnek ile aynı.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-202">If we look at hello next sample code, hello former part is hello same as hello previous example.</span></span> <span data-ttu-id="0a6ba-203">Merhaba ikinci bölümünde, bu örnek hello gösterir **embedUrl** \(hello önceki sonuçları görmek) IFRAME hello ve hello uygulama belirteci hello IFRAME gönderme.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-203">In hello latter part, this sample shows hello **embedUrl** \(see hello previous result) in hello iframe, and is posting hello app token into hello iframe.</span></span>

> [!NOTE]
> <span data-ttu-id="0a6ba-204">Toochange hello rapor kimliği değeri tooone kendi gerekir.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-204">You'll need toochange hello report id value tooone of your own.</span></span> <span data-ttu-id="0a6ba-205">Ayrıca, içerik yönetimi sistemimizde tooa hata, hello IFRAME etiketi hello kod örneğinde tam anlamıyla okunur.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-205">Also, due tooa bug in our content management system, hello iframe tag in hello code sample is read literally.</span></span> <span data-ttu-id="0a6ba-206">Bu örnek kodu kopyalayıp tutulabilir hello metin hello etiketinden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-206">Remove hello capped text from hello tag if you copy and paste this sample code.</span></span>

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

<span data-ttu-id="0a6ba-207">Ve bizim sonuç şöyledir:</span><span class="sxs-lookup"><span data-stu-id="0a6ba-207">And here's our result:</span></span>

![](media/power-bi-embedded-iframe/view-report.png)

<span data-ttu-id="0a6ba-208">Şu anda Power BI Embedded yalnızca hello rapor hello IFRAME gösterir.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-208">At this time, Power BI Embedded only shows hello report in hello iframe.</span></span> <span data-ttu-id="0a6ba-209">Merhaba üzerinde ancak tutmak bir göz [Power BI Blog](https://powerbi.microsoft.com/blog/).</span><span class="sxs-lookup"><span data-stu-id="0a6ba-209">But, keep an eye on hello [Power BI Blog](https://powerbi.microsoft.com/blog/).</span></span> <span data-ttu-id="0a6ba-210">Gelecekteki geliştirmeleri, yeni istemci tarafı bize hello IFRAME bilgiyi yanı sıra bilgi alacağınızı API'leri kullanabilirsiniz. Heyecan verici şeyler!</span><span class="sxs-lookup"><span data-stu-id="0a6ba-210">Future improvements could use new client side APIs that will let us send information into hello iframe as well as get information out. Exciting stuff!</span></span>

## <a name="see-also"></a><span data-ttu-id="0a6ba-211">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="0a6ba-211">See also</span></span>
* [<span data-ttu-id="0a6ba-212">Power BI Embedded ile kimlik doğrulaması ve yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="0a6ba-212">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)

<span data-ttu-id="0a6ba-213">Başka sorunuz mu var?</span><span class="sxs-lookup"><span data-stu-id="0a6ba-213">More questions?</span></span> [<span data-ttu-id="0a6ba-214">Merhaba Power BI topluluk deneyin</span><span class="sxs-lookup"><span data-stu-id="0a6ba-214">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

