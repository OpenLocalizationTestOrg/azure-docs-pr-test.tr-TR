---
title: "aaaGuide toocreating hello Market için veri hizmeti | Microsoft Docs"
description: "Nasıl toocreate, onaylamak ve dağıtmak için bir veri hizmeti ayrıntılı yönergeler hello üzerinde Azure Market satın alın."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 148f8638-ee80-4100-8d63-5afa4167ca1b
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 8917a43959834d15f70866297f98d24bb83e217f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="examples-of-mapping-an-existing-web-service-tooodata-through-csdls"></a><span data-ttu-id="d4f14-103">Varolan bir eşleme örnekleri hizmet tooOData CSDLs aracılığıyla web</span><span class="sxs-lookup"><span data-stu-id="d4f14-103">Examples of mapping an existing web service tooOData through CSDLs</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d4f14-104">**Şu anda artık ekleme duyuyoruz herhangi yeni veri hizmeti yayımcılar. Yeni dataservices listesine onaylanmamış.**</span><span class="sxs-lookup"><span data-stu-id="d4f14-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="d4f14-105">Bir SaaS iş uygulaması varsa toopublish istediğiniz AppSource hakkında daha fazla bilgi bulabilirsiniz [burada](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="d4f14-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="d4f14-106">Bir Iaas uygulamalar varsa veya Geliştirici hizmeti misiniz Azure Market'te toopublish gibi daha fazla bilgi bulabilirsiniz [burada](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="d4f14-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

## <a name="example-functionimport-for-raw-data-returned-using-post"></a><span data-ttu-id="d4f14-107">Örnek: Functionımport "POST" kullanarak döndürülen "Ham" veriler için</span><span class="sxs-lookup"><span data-stu-id="d4f14-107">Example: FunctionImport for "Raw" data returned using "POST"</span></span>
<span data-ttu-id="d4f14-108">Yeni bağımlı bir POST ham verileri toocreate kullanın ve kendi sunucu URL(location) tanımlanan veya URL hello hello sunucuda bağımlı tooupdate parçası tanımlanan döndürür.</span><span class="sxs-lookup"><span data-stu-id="d4f14-108">Use POST Raw data toocreate a new subordinate and return its server defined URL(location) or tooupdate part of hello subordinate at hello server defined URL.</span></span>  <span data-ttu-id="d4f14-109">Ex yani yapılandırılmamış bir akış hello bağımlı olduğu.</span><span class="sxs-lookup"><span data-stu-id="d4f14-109">Where hello subordinate is a stream, i.e. unstructured, ex.</span></span> <span data-ttu-id="d4f14-110">bir metin dosyası.</span><span class="sxs-lookup"><span data-stu-id="d4f14-110">a text file.</span></span>  <span data-ttu-id="d4f14-111">POST değil ıdempotent olmadan bir konum içinde kaybolacağını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d4f14-111">Beware POST in not idempotent without a location.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="AddUsageEvent" ReturnType="Raw(text/plain)" d:EncodeParameterValues="true" d:AllowedHttpMethods="POST" d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Add usage event (data acquisition)</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-using-delete"></a><span data-ttu-id="d4f14-112">Örnek: "DELETE" kullanarak Functionımport</span><span class="sxs-lookup"><span data-stu-id="d4f14-112">Example: FunctionImport using "DELETE"</span></span>
<span data-ttu-id="d4f14-113">DELETE tooremove belirtilen bir URI kullanın.</span><span class="sxs-lookup"><span data-stu-id="d4f14-113">Use DELETE tooremove a specified URI.</span></span>

        <EntitySet Name="DeleteUsageFileEntitySet" EntityType="MyOffer.DeleteUsageFileEntity" />
        <FunctionImport Name="DeleteUsageFile" EntitySet="DeleteUsageFileEntitySet" ReturnType="Collection(MyOffer.DeleteUsageFileEntity)"  d:AllowedHttpMethods="DELETE" d:EncodeParameterValues="true” d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643" >
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Delete usage File</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>
        <EntityType Name="DeleteUsageFileEntity" d:Map="//boolean">
        <Property Name="boolean" Type="String" Nullable="true" d:Map="./boolean" />
        </EntityType>

## <a name="example-functionimport-using-post"></a><span data-ttu-id="d4f14-114">Örnek: "POST" kullanarak Functionımport</span><span class="sxs-lookup"><span data-stu-id="d4f14-114">Example: FunctionImport using "POST"</span></span>
<span data-ttu-id="d4f14-115">Yeni bağımlı bir POST ham verileri toocreate kullanın ve kendi sunucu URL(location) tanımlanan veya URL hello hello sunucuda bağımlı tooupdate parçası tanımlanan döndürür.</span><span class="sxs-lookup"><span data-stu-id="d4f14-115">Use POST Raw data toocreate a new subordinate and return its server defined URL(location) or tooupdate part of hello subordinate at hello server defined URL.</span></span>  <span data-ttu-id="d4f14-116">Burada hello bağımlı bir yapıdır.</span><span class="sxs-lookup"><span data-stu-id="d4f14-116">Where hello subordinate is a structure.</span></span> <span data-ttu-id="d4f14-117">Dikkatli olun POST ıdempotent olmadan bir konum değil.</span><span class="sxs-lookup"><span data-stu-id="d4f14-117">Beware POST is not idempotent without a location.</span></span>

        <EntitySet Name="CreateANewModelEntitySet2" EntityType=" MyOffer.CreateANewModelEntity2" />
        <FunctionImport Name="CreateModel" EntitySet="CreateANewModelEntitySet2" ReturnType="Collection(MyOffer.CreateANewModelEntity2)" d:EncodeParameterValues="true" d:AllowedHttpMethods="POST" d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Create A New Model</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-using-put"></a><span data-ttu-id="d4f14-118">Örnek: "PUT" kullanarak Functionımport</span><span class="sxs-lookup"><span data-stu-id="d4f14-118">Example: FunctionImport using "PUT"</span></span>
<span data-ttu-id="d4f14-119">URL tooupdate hello tüm bağımlı bir sunucuda tanımlanan veya bağımlı yeni PUT toocreate kullanın.</span><span class="sxs-lookup"><span data-stu-id="d4f14-119">Use PUT toocreate a new subordinate or tooupdate hello entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="d4f14-120">Merhaba bağımlı bir yapı; Burada, birden fazla oluşumu hello aynı neden olacak şekilde PUT ıdempotent olduğu durum, yani</span><span class="sxs-lookup"><span data-stu-id="d4f14-120">Where hello subordinate is a structure, PUT is idempotent so multiple occurrences will result in hello same state, i.e</span></span> <span data-ttu-id="d4f14-121">x = 5.</span><span class="sxs-lookup"><span data-stu-id="d4f14-121">x=5.</span></span>  <span data-ttu-id="d4f14-122">PUT hello ile belirtilen Merhaba tam içerik kullanılmalıdır kaynak.</span><span class="sxs-lookup"><span data-stu-id="d4f14-122">Put should be used with hello full content of hello specified resource.</span></span>

        <EntitySet Name="UpdateAnExistingModelEntitySet" EntityType="MyOffer.UpdateAnExistingModelEntity" />
        <FunctionImport Name="UpdateModel" EntitySet="UpdateAnExistingModelEntitySet" ReturnType="Collection(MyOffer.UpdateAnExistingModelEntity)" d:EncodeParameterValues="true" d:AllowedHttpMethods="PUT" d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Update an Existing Model</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>
        <EntityType Name="UpdateAnExistingModelEntity" d:Map="//string">
        <Property Name="string"     Type="String" Nullable="true" d:Map="./string" />
        </EntityType>


## <a name="example-functionimport-for-raw-data-returned-using-put"></a><span data-ttu-id="d4f14-123">Örnek: Functionımport "PUT" kullanarak döndürülen "Ham" veriler için</span><span class="sxs-lookup"><span data-stu-id="d4f14-123">Example: FunctionImport for "Raw" data returned using "PUT"</span></span>
<span data-ttu-id="d4f14-124">PUT ham verileri toocreate bağımlı yeni veya tooupdate hello tüm alt tanımlı sunucusu URL'de kullanın.</span><span class="sxs-lookup"><span data-stu-id="d4f14-124">Use PUT Raw data toocreate a new subordinate or tooupdate hello entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="d4f14-125">Ex yani yapılandırılmamış bir akış hello bağımlı olduğu.</span><span class="sxs-lookup"><span data-stu-id="d4f14-125">Where hello subordinate is a stream, i.e. unstructured, ex.</span></span> <span data-ttu-id="d4f14-126">bir metin dosyası.</span><span class="sxs-lookup"><span data-stu-id="d4f14-126">a text file.</span></span>  <span data-ttu-id="d4f14-127">PUT birden fazla oluşumu hello aynı sonuçlanır ıdempotent olduğundan durum, yani</span><span class="sxs-lookup"><span data-stu-id="d4f14-127">PUT is idempotent so multiple occurrences will result in hello same state, i.e</span></span> <span data-ttu-id="d4f14-128">x = 5.</span><span class="sxs-lookup"><span data-stu-id="d4f14-128">x=5.</span></span>  <span data-ttu-id="d4f14-129">PUT hello ile belirtilen Merhaba tam içerik kullanılmalıdır kaynak.</span><span class="sxs-lookup"><span data-stu-id="d4f14-129">Put should be used with hello full content of hello specified resource.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="CancelBuild” ReturnType="Raw(text/plain)" d:AllowedHttpMethods="PUT" d:EncodeParameterValues="true" d:BaseUri=” http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Cancel Build</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>


## <a name="example-functionimport-for-raw-data-returned-using-get"></a><span data-ttu-id="d4f14-130">Örnek: Functionımport "GET" kullanarak döndürülen "Ham" veriler için</span><span class="sxs-lookup"><span data-stu-id="d4f14-130">Example: FunctionImport for "Raw" data returned using "GET"</span></span>
<span data-ttu-id="d4f14-131">Alma ham verileri tooreturn yapılandırılmamış, bağımlı bir yani metin kullanın.</span><span class="sxs-lookup"><span data-stu-id="d4f14-131">Use GET Raw data tooreturn a subordinate that is unstructured, i.e. text.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="GetModelUsageFile" ReturnType="Raw(text/plain)" d:EncodeParameterValues="true" d:AllowedHttpMethods="GET" d:BaseUri="https://cmla.cloudapp.net/api2/model/builder/build?buildId={buildId}&amp;apiVersion={apiVersion}">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Download A Models Usage File</d:Description>
        <d:Headers>
        <d:Header d:Name="Accept" d:Value="application/xml,application/xhtml+xml,text/html;" />
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-for-paging-through-returned-data"></a><span data-ttu-id="d4f14-132">Örnek: Functionımport döndürülen veriler aracılığıyla "sayfalama"</span><span class="sxs-lookup"><span data-stu-id="d4f14-132">Example: FunctionImport for "Paging" through returned data</span></span>
<span data-ttu-id="d4f14-133">Uygulama verilerinizi aracılığıyla RESTful disk belleği ile GET kullanın.</span><span class="sxs-lookup"><span data-stu-id="d4f14-133">Use implement RESTful paging through your data with GET.</span></span>  <span data-ttu-id="d4f14-134">Varsayılan disk belleği too100 sayfa başına veri satırının ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="d4f14-134">Default paging is set too100 row per page of data.</span></span>

        <EntitySet Name=”CropEntitySet" EntityType="MyOffer.CropEntity" />
        <FunctionImport    Name="GetCropReport" EntitySet="CropEntitySet” ReturnType="Collection(MyOffer.CropEntity)" d:EmitSelfLink="false" d:EncodeParameterValues="true" d:Paging="SkipTake" d:MaxPageSize="100" d:BaseUri="http://api.mydata.org/Crop? report={report}&amp;series={series}&amp;start={$skip}&amp;size=100">
        <Parameter Name="report" Type="Int32" Mode="In" Nullable="false" d:SampleValues="4"  d:enum="1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19"  />
        <Parameter Name="series"    Type="String"    Mode="In" Nullable="false" d:SampleValues="FARM" />
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="text/xml;charset=UTF-8" />
        </d:Headers>
        <d:Namespaces>
        <d:Namespace d:Prefix="diffgr" d:Uri="urn:schemas-microsoft-com:xml-diffgram-v1" />
        </d:Namespaces>
        </FunctionImport>

## <a name="see-also"></a><span data-ttu-id="d4f14-135">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="d4f14-135">See Also</span></span>
* <span data-ttu-id="d4f14-136">İçinde anlama ilgileniyorsanız hello genel OData eşleme işlemi ve amacı, bu makalede okuma [veri hizmeti OData eşleme](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview tanımları, yapılar ve yönergeler.</span><span class="sxs-lookup"><span data-stu-id="d4f14-136">If you are interested in understanding hello overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definitions, structures, and instructions.</span></span>
* <span data-ttu-id="d4f14-137">Öğrenme ve anlama hello belirli düğümler ve bunların parametrelerini ilgileniyorsanız, bu makaleyi okuyun [veri hizmeti OData eşleme düğümleri](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) tanımları ve açıklamalar, örnekler ve kullanım örneği bağlamı.</span><span class="sxs-lookup"><span data-stu-id="d4f14-137">If you are interested in learning and understanding hello specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="d4f14-138">Bu makaleyi okuyun bir veri hizmeti toohello Azure Marketi'nde yayımlama yolu belirlenen tooreturn toohello [veri hizmeti yayımlama Kılavuzu](marketplace-publishing-data-service-creation.md).</span><span class="sxs-lookup"><span data-stu-id="d4f14-138">tooreturn toohello prescribed path for publishing a Data Service toohello Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

