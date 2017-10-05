---
title: "Veri Hizmeti Market oluşturmaya Kılavuzu | Microsoft Docs"
description: "Oluşturma, sertifika ve bir veri hizmeti için dağıtma konusunda ayrıntılı yönergeler Azure Market satın alın."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 3a632825-db5b-49ec-98bd-887138798bc4
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: a853b4dbd1952ba4ea8ee68ea3ca98f588bb71a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="mapping-an-existing-web-service-to-odata-through-csdl"></a><span data-ttu-id="a5d52-103">Var olan bir web hizmetini CSDL aracılığıyla OData eşleme</span><span class="sxs-lookup"><span data-stu-id="a5d52-103">Mapping an existing web service to OData through CSDL</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a5d52-104">**Şu anda artık ekleme duyuyoruz herhangi yeni veri hizmeti yayımcılar. Yeni dataservices listesine onaylanmamış.**</span><span class="sxs-lookup"><span data-stu-id="a5d52-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="a5d52-105">Üzerinde AppSource yayımlamak istediğiniz bir SaaS iş uygulaması varsa daha fazla bilgi bulabilirsiniz [burada](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="a5d52-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="a5d52-106">Bir Iaas uygulamalar varsa veya Azure marketi, yayımlamak istediğiniz Geliştirici hizmet, daha fazla bilgi bulabilirsiniz [burada](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="a5d52-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="a5d52-107">Bu makalede bir CSDL var olan bir hizmeti bir OData uyumlu hizmetine eşlemek için nasıl kullanılacağı hakkında genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="a5d52-107">This article gives an overview on how to use a CSDL to map an existing service to an OData compatible service.</span></span> <span data-ttu-id="a5d52-108">Nasıl bir hizmet aramasıyla istemciden giriş isteğinde dönüştüren eşleme belge (CSDL) oluşturmak için ve çıkış (veri) ile uyumlu bir OData akışı istemciye geri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a5d52-108">It explains how to create the mapping document (CSDL) that transforms the input request from the client via a service call and the output (data) back to the client via an OData compatible feed.</span></span> <span data-ttu-id="a5d52-109">Microsoft Azure Marketi'nde OData protokolünü kullanarak son kullanıcılara hizmetleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="a5d52-109">Microsoft’s Azure Marketplace exposes services to the end-users by using the OData protocol.</span></span> <span data-ttu-id="a5d52-110">(Verileri sahiplerinin) içerik sağlayıcıları tarafından sunulan hizmetler, formlar, REST, SOAP, vb. gibi çeşitli sunulur.</span><span class="sxs-lookup"><span data-stu-id="a5d52-110">Services that are exposed by content providers (Data Owners) are exposed in a variety of forms, such as REST, SOAP, etc.</span></span>

## <a name="what-is-a-csdl-and-its-structure"></a><span data-ttu-id="a5d52-111">Bir CSDL ve yapısını nedir?</span><span class="sxs-lookup"><span data-stu-id="a5d52-111">What is a CSDL and its structure?</span></span>
<span data-ttu-id="a5d52-112">CSDL (kavramsal şema tanım dili) web hizmeti veya Azure Marketi'nde ortak XML duyuruları veritabanı hizmetinin açıklamak nasıl tanımlayan bir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="a5d52-112">A CSDL (Conceptual Schema Definition Language) is a specification defining how to describe web service or database service in common XML verbiage to the Azure Marketplace.</span></span>

<span data-ttu-id="a5d52-113">Basit genel bakış **istek akışı:**</span><span class="sxs-lookup"><span data-stu-id="a5d52-113">Simple overview of the **request flow:**</span></span>

  `Client -> Azure Marketplace -> Content Provider’s Web Service (Get, Post, Delete, Put)`

<span data-ttu-id="a5d52-114">**Veri akışı** ters yönde değil:</span><span class="sxs-lookup"><span data-stu-id="a5d52-114">The **data flow** is in the opposite direction:</span></span>

  `Client <- Azure Marketplace <- Content Provider’s WebService`

<span data-ttu-id="a5d52-115">**Şekil 1** diyagramları nasıl bir istemci verilerini bir içerik sağlayıcı (hizmetinizi) Azure Market üzerinden giderek elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5d52-115">**Figure 1** diagrams how a client would obtain data from a content provider (your service) by going through the Azure Marketplace.</span></span>  <span data-ttu-id="a5d52-116">İçerik sağlayıcının hizmetlere ve istekte bulunan istemci arasında veri iletmek ve CSDL isteği işlemek üzere eşleme/dönüştürme bileşen tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a5d52-116">The CSDL is used by the Mapping/Transformation component to handle the request and data pass between the content provider’s service(s) and the requesting client.</span></span>

<span data-ttu-id="a5d52-117">*Şekil 1: Azure Market üzerinden içerik sağlayıcı için istekte bulunan istemciden ayrıntılı akış*</span><span class="sxs-lookup"><span data-stu-id="a5d52-117">*Figure 1: Detailed flow from requesting client to content provider via Azure Marketplace*</span></span>

  ![Çizim](media/marketplace-publishing-data-service-creation-odata-mapping/figure-1.png)

<span data-ttu-id="a5d52-119">Gözden geçirme Atom arka planda için lütfen Atom Pub ve bağlı Azure Marketi uzantıları yapı, OData protokolü: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)</span><span class="sxs-lookup"><span data-stu-id="a5d52-119">For background on Atom, Atom Pub, and the OData protocol upon which the Azure Marketplace extensions build, please review: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)</span></span>

<span data-ttu-id="a5d52-120">Bağlantı yukarıdaki alıntı: *"amacı (bundan böyle OData adlandırılır) açık veri protokolü, REST tabanlı bir protokol veri hizmetleri sunulan kaynaklara karşı stili CRUD işlemleri (oluşturma, okuma, güncelleştirme ve silme) sağlamaktır. "Veri hizmeti" bir uç noktadır koleksiyonlardan bir veya daha fazla"" her ", oluşur sıfır veya daha fazla girişlerini" ile kullanıma sunulan veri olduğu adlı-değer çiftleri belirtilmiş. Böylece isteyen herkes derleme sunucuları, istemcileri veya Araçlar telif hakkı veya kısıtlamaları olmadan OData OASIS (terfi yapılandırılmış bilgi standartlar için kuruluş) standartları altında Microsoft tarafından yayımlanan."*</span><span class="sxs-lookup"><span data-stu-id="a5d52-120">Excerpt from above link: *“The purpose of the Open Data protocol (hereafter referred to as OData) is to provide a REST-based protocol for CRUD-style operations (Create, Read, Update and Delete) against resources exposed as data services. A “data service” is an endpoint where there is data exposed from one or more “collections” each with zero or more “entries”, which consist of typed named-value pairs. OData is published by Microsoft under OASIS (Organization for the Advancement of Structured Information Standards) Standards so that anyone that wants to can build servers, clients or tools without royalties or restrictions.”*</span></span>

### <a name="three-critical-pieces-that-have-to-be-defined-by-the-csdl-are"></a><span data-ttu-id="a5d52-121">Üç kritik CSDL tarafından tanımlanmış olması parçalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a5d52-121">Three Critical Pieces that have to be defined by the CSDL are:</span></span>
* <span data-ttu-id="a5d52-122">**Endpoint** , servis sağlayıcı Web adresi (URI) hizmetinin</span><span class="sxs-lookup"><span data-stu-id="a5d52-122">The **endpoint** of the Service Provider The Web Address (URI) of the Service</span></span>
* <span data-ttu-id="a5d52-123">**Veri parametreleri** veri türü için içerik sağlayıcının hizmetine gönderilen parametreleri tanımlarını giriş hizmet sağlayıcısı olarak geçirilen.</span><span class="sxs-lookup"><span data-stu-id="a5d52-123">The **data parameters** being passed as input to the Service Provider The definitions of the parameters being sent to the Content Provider’s service down to the data type.</span></span>
* <span data-ttu-id="a5d52-124">**Şema** isteyen hizmete içerik sağlayıcının hizmeti tarafından teslim edilmesini veri ve şema döndürülen veriler kapsayıcı, koleksiyonları/tabloları, değişkenleri/sütunları ve veri türleri dahil.</span><span class="sxs-lookup"><span data-stu-id="a5d52-124">**Schema** of the data being returned to the Requesting Service The schema of the data being delivered by the Content Provider’s service, including Container, collections/tables, variables/columns, and data types.</span></span>

<span data-ttu-id="a5d52-125">Aşağıdaki diyagramda burada sonuçlar/verileri geri almak için istemci OData deyimi (içerik sağlayıcının web hizmeti çağrısı) girer gelen akış özetini gösterir.</span><span class="sxs-lookup"><span data-stu-id="a5d52-125">The following diagram shows an overview of the flow from where the client enters the OData statement (call to the content provider’s web service) to getting the results/data back.</span></span>

  ![Çizim](media/marketplace-publishing-data-service-creation-odata-mapping/figure-2.png)

### <a name="steps"></a><span data-ttu-id="a5d52-127">adımlar:</span><span class="sxs-lookup"><span data-stu-id="a5d52-127">Steps:</span></span>
1. <span data-ttu-id="a5d52-128">İstemci isteği hizmeti çağrısı aracılığıyla Azure Marketi XML tanımlanan giriş parametreleri ile tam gönderir</span><span class="sxs-lookup"><span data-stu-id="a5d52-128">Client sends request via Service call complete with Input Parameters defined in XML to the Azure Marketplace</span></span>
2. <span data-ttu-id="a5d52-129">CSDL hizmeti çağrısı doğrulamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a5d52-129">CSDL is used to validate the Service call.</span></span>
   * <span data-ttu-id="a5d52-130">Biçimlendirilmiş hizmetini çağırmak için içerik sağlayıcıları hizmeti Azure Marketi tarafından gönderilir</span><span class="sxs-lookup"><span data-stu-id="a5d52-130">The Formatted Service Call is then sent to the Content Providers Service by the Azure Marketplace</span></span>
3. <span data-ttu-id="a5d52-131">Web hizmeti yürütür ve Http Fiili eylem preforms (yani GET) verileri Azure Marketi (varsa) istenen verileri istemciye XML biçiminde kullanıma sunar nerede CSDL tanımlı eşlemesi kullanarak döndürülür.</span><span class="sxs-lookup"><span data-stu-id="a5d52-131">The Webservice executes and preforms the action of the Http Verb (i.e. GET) The data is returned to Azure Marketplace where the requested data (if any) is exposes in XML Format to the Client using the Mapping defined in the CSDL.</span></span>
4. <span data-ttu-id="a5d52-132">İstemci veriler (varsa) XML veya JSON biçiminde gönderilir</span><span class="sxs-lookup"><span data-stu-id="a5d52-132">The Client is sent the data (if any) in XML or JSON format</span></span>

## <a name="definitions"></a><span data-ttu-id="a5d52-133">Tanımlar</span><span class="sxs-lookup"><span data-stu-id="a5d52-133">Definitions</span></span>
### <a name="odata-atom-pub"></a><span data-ttu-id="a5d52-134">OData ATOM pub</span><span class="sxs-lookup"><span data-stu-id="a5d52-134">OData ATOM pub</span></span>
<span data-ttu-id="a5d52-135">Her girişin bir sonucu olarak bir satır temsil ettiği ATOM pub uzantısı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a5d52-135">An extension to the ATOM pub where each entry represents one row of a result set.</span></span> <span data-ttu-id="a5d52-136">Giriş içerik parçası satırın – anahtar değer çiftleri olarak değerleri içerecek şekilde geliştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a5d52-136">The content part of the entry is enhanced to contain the values of the row – as key value pairs.</span></span> <span data-ttu-id="a5d52-137">Daha fazla bilgi aşağıda bulunan: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)</span><span class="sxs-lookup"><span data-stu-id="a5d52-137">More information is found here: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)</span></span>

### <a name="csdl---conceptual-schema-definition-language"></a><span data-ttu-id="a5d52-138">CSDL - kavramsal şema tanım dili</span><span class="sxs-lookup"><span data-stu-id="a5d52-138">CSDL - Conceptual Schema Definition Language</span></span>
<span data-ttu-id="a5d52-139">İşlevler (SPROCs) tanımlanmasına olanak sağlar ve bir veritabanı yoluyla kullanıma sunulan varlıklar.</span><span class="sxs-lookup"><span data-stu-id="a5d52-139">Allows defining functions (SPROCs) and entities that are exposed through a database.</span></span> <span data-ttu-id="a5d52-140">Burada bulunan daha fazla bilgi: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)</span><span class="sxs-lookup"><span data-stu-id="a5d52-140">More information found here: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)</span></span>  

> [!TIP]
> <span data-ttu-id="a5d52-141">Tıklatın **diğer sürümleri** açılır ve makale görmüyorsanız, bir sürümü seçin.</span><span class="sxs-lookup"><span data-stu-id="a5d52-141">Click the **other versions** dropdown and select a version if you don’t see the article.</span></span>
> 
> 

### <a name="edm---entry-data-model"></a><span data-ttu-id="a5d52-142">EDM - giriş veri modeli</span><span class="sxs-lookup"><span data-stu-id="a5d52-142">EDM - Entry Data Model</span></span>
* <span data-ttu-id="a5d52-143">Genel Bakış: [http://msdn.microsoft.com/library/vstudio/ee382825 (v=vs.100).aspx][OverviewLink]</span><span class="sxs-lookup"><span data-stu-id="a5d52-143">Overview: [http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]</span></span>

[OverviewLink]:http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx
* <span data-ttu-id="a5d52-144">Önizleme: [http://msdn.microsoft.com/library/aa697428 (v=vs.80).aspx][PreviewLink]</span><span class="sxs-lookup"><span data-stu-id="a5d52-144">Preview: [http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]</span></span>

[PreviewLink]:http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx
* <span data-ttu-id="a5d52-145">Veri türleri: [http://msdn.microsoft.com/library/bb399548 (v=VS.100).aspx][DataTypesLink]</span><span class="sxs-lookup"><span data-stu-id="a5d52-145">Data types: [http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]</span></span>

[DataTypesLink]:http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx

<span data-ttu-id="a5d52-146">Ayrıntılı soldan sağa akış istemci OData deyimi (içerik sağlayıcının web hizmeti çağrısı) burada girer gelen sonuçları/verileri almak için aşağıdaki gösterildiği yedekleyin:</span><span class="sxs-lookup"><span data-stu-id="a5d52-146">The following shows the detailed Left to Right flow from where the client enters the OData statement (call to the content provider’s web service) to getting the results/data back:</span></span>

  ![Çizim](media/marketplace-publishing-data-service-creation-odata-mapping/figure-3.png)

## <a name="csdl-basics"></a><span data-ttu-id="a5d52-148">CSDL temelleri</span><span class="sxs-lookup"><span data-stu-id="a5d52-148">CSDL Basics</span></span>
<span data-ttu-id="a5d52-149">CSDL (kavramsal şema tanım dili) web hizmeti veya Azure Marketi'nde ortak XML duyuruları veritabanı hizmetinin açıklamak nasıl tanımlayan bir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="a5d52-149">A CSDL (Conceptual Schema Definition Language) is a specification defining how to describe web service or database service in common XML verbiage to the Azure Marketplace.</span></span> <span data-ttu-id="a5d52-150">CSDL kritik açıklar, parça **veri geçirme veri kaynağından Azure Marketi mümkün kılar.**</span><span class="sxs-lookup"><span data-stu-id="a5d52-150">CSDL describes the critical pieces that **makes the passing of data from the Data Source to the Azure Marketplace possible.**</span></span> <span data-ttu-id="a5d52-151">Temel Parçalar aşağıda açıklanmıştır:</span><span class="sxs-lookup"><span data-stu-id="a5d52-151">The main pieces are described here:</span></span>

* <span data-ttu-id="a5d52-152">Tüm genel kullanıma açık işlevleri (Functionımport düğümü) açıklayan bilgileri arabirimi</span><span class="sxs-lookup"><span data-stu-id="a5d52-152">Interface information describing all publicly available functions (FunctionImport Node)</span></span>
* <span data-ttu-id="a5d52-153">Veri türü bilgileri tüm ileti requests(input) ve ileti responses(outputs) (EntitySet/EntityContainer/EntityType düğümler)</span><span class="sxs-lookup"><span data-stu-id="a5d52-153">Data type information for all message requests(input) and message responses(outputs) (EntityContainer/EntitySet/EntityType Nodes)</span></span>
* <span data-ttu-id="a5d52-154">Aktarım Protokolü şekilde hakkında bilgi bağlama (üstbilgi düğümü) kullanılır</span><span class="sxs-lookup"><span data-stu-id="a5d52-154">Binding information about the transport protocol to be used (Header Node)</span></span>
* <span data-ttu-id="a5d52-155">Belirtilen hizmet (tabanURI özniteliği) yerini adresi bilgileri</span><span class="sxs-lookup"><span data-stu-id="a5d52-155">Address information for locating the specified service (BaseURI attribute)</span></span>

<span data-ttu-id="a5d52-156">Buna koysalar CSDL hizmet istek sahibi ve hizmet sağlayıcısı arasında bir platform ve dilden bağımsız sözleşme temsil eder.</span><span class="sxs-lookup"><span data-stu-id="a5d52-156">In a nutshell, the CSDL represents a platform- and language-independent contract between the service requestor and the service provider.</span></span> <span data-ttu-id="a5d52-157">Bir istemci, CSDL'ı kullanarak bir web hizmeti/veritabanı hizmetini bulun ve herhangi bir genel kullanıma açık işlevlerini çağırma.</span><span class="sxs-lookup"><span data-stu-id="a5d52-157">Using the CSDL, a client can locate a web service/database service and invoke any of its publicly available functions.</span></span>

### <a name="relating-a-csdl-to-a-database-or-a-collection"></a><span data-ttu-id="a5d52-158">Bir veritabanı veya bir koleksiyon için bir CSDL ilgili</span><span class="sxs-lookup"><span data-stu-id="a5d52-158">Relating a CSDL to a Database or a Collection</span></span>
<span data-ttu-id="a5d52-159">**CSDL belirtimi**</span><span class="sxs-lookup"><span data-stu-id="a5d52-159">**The CSDL Specification**</span></span>

<span data-ttu-id="a5d52-160">CSDL açıklayan bir web hizmeti için XML dilbilgisi ' dir.</span><span class="sxs-lookup"><span data-stu-id="a5d52-160">CSDL is XML grammar for describing a web service.</span></span> <span data-ttu-id="a5d52-161">Belirtimi 4 ana öğeye ayrılmıştır: EntitySet, Functionımport; Ad alanı ve EntityType.</span><span class="sxs-lookup"><span data-stu-id="a5d52-161">The specification itself is divided into 4 major elements:  EntitySet, FunctionImport; NameSpace, and EntityType.</span></span>

<span data-ttu-id="a5d52-162">Bu soyutlama sağlar anlamak daha kolay hale getirmek için bir tabloya bir CSDL ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="a5d52-162">To make this abstraction easier to understand lets relate a CSDL to a table.</span></span>

<span data-ttu-id="a5d52-163">Unutmayın;</span><span class="sxs-lookup"><span data-stu-id="a5d52-163">Remember;</span></span>

  <span data-ttu-id="a5d52-164">CSDL temsil eden bir platform ve dilden bağımsız sözleşme arasında **hizmet istek sahibi** ve **hizmet sağlayıcısı**.</span><span class="sxs-lookup"><span data-stu-id="a5d52-164">CSDL represents a platform- and language-independent contract between the **service requestor** and the **service provider**.</span></span> <span data-ttu-id="a5d52-165">CSDL, kullanarak bir **istemci** bulabilir bir **web hizmeti/veritabanı hizmeti** ve kendi genel kullanıma açık hiçbirini çağırma **işlevleri.**</span><span class="sxs-lookup"><span data-stu-id="a5d52-165">Using CSDL, a **client** can locate a **web service/database service** and invoke any of its publicly available **functions.**</span></span>

<span data-ttu-id="a5d52-166">Veri Hizmeti için bir CSDL dört bölümden, veritabanı, tablo, sütun ve deposu yordamı bakımından değerlendirilebilir.</span><span class="sxs-lookup"><span data-stu-id="a5d52-166">For a Data Service the four parts of a CSDL can be thought of in terms of a Database, Table, Column, and Store Procedure.</span></span>

<span data-ttu-id="a5d52-167">Bu gibi bir veri hizmeti ile ilgili:</span><span class="sxs-lookup"><span data-stu-id="a5d52-167">Relating these as follows for a Data Service:</span></span>

* <span data-ttu-id="a5d52-168">EntityContainer ~ = veritabanı</span><span class="sxs-lookup"><span data-stu-id="a5d52-168">EntityContainer  ~=  Database</span></span>
* <span data-ttu-id="a5d52-169">EntitySet ~ = tablosu</span><span class="sxs-lookup"><span data-stu-id="a5d52-169">EntitySet  ~=  Table</span></span>
* <span data-ttu-id="a5d52-170">EntityType ~ sütunları =</span><span class="sxs-lookup"><span data-stu-id="a5d52-170">EntityType  ~= Columns</span></span>
* <span data-ttu-id="a5d52-171">Functionımport ~ saklı yordam =</span><span class="sxs-lookup"><span data-stu-id="a5d52-171">FunctionImport  ~=  Stored Procedure</span></span>

<span data-ttu-id="a5d52-172">**İzin verilen HTTP fiilleri**</span><span class="sxs-lookup"><span data-stu-id="a5d52-172">**HTTP Verbs allowed**</span></span>

* <span data-ttu-id="a5d52-173">GET-(bir koleksiyon döndürür) DB'den değerler verir</span><span class="sxs-lookup"><span data-stu-id="a5d52-173">GET – returns values from the db (returns a Collection)</span></span>
* <span data-ttu-id="a5d52-174">POST – veri ve isteğe bağlı dönüş değerleri (oluşturma koleksiyonu, dönüş kimliği/URI'si yeni bir giriş) DB'den iletmek için kullanılan</span><span class="sxs-lookup"><span data-stu-id="a5d52-174">POST – used to pass data to and optional return values from the db (Create a new entry in the collection, return id/URI)</span></span>
* <span data-ttu-id="a5d52-175">– (Koleksiyonu siler) veritabanından siler verileri Sil</span><span class="sxs-lookup"><span data-stu-id="a5d52-175">DELETE – Deletes data from the DB (Deletes a collection)</span></span>
* <span data-ttu-id="a5d52-176">PUT – bir Veritabanına veri güncelleştirme (bir koleksiyon değiştirin veya bir tane oluşturun)</span><span class="sxs-lookup"><span data-stu-id="a5d52-176">PUT – Update data into a DB (replace a collection or create one)</span></span>

## <a name="metadatamapping-document"></a><span data-ttu-id="a5d52-177">Meta veri/eşleme belge</span><span class="sxs-lookup"><span data-stu-id="a5d52-177">Metadata/Mapping Document</span></span>
<span data-ttu-id="a5d52-178">Meta veri/eşleme belge, böylece Azure Marketi sistem tarafından bir OData web hizmeti olarak verilebilen bir içerik sağlayıcının varolan web hizmetleri eşlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a5d52-178">The metadata/mapping document is used to map a content provider’s existing web services so that it can be exposed as an OData web service by the Azure Marketplace system.</span></span> <span data-ttu-id="a5d52-179">Implements REST ihtiyaçlarını karşılamak için CSDL birkaç uzantıları Azure Market üzerinden kullanıma sunulan web hizmetleri tabanlı ve CSDL üzerinde temel alır.</span><span class="sxs-lookup"><span data-stu-id="a5d52-179">It is based on CSDL and implements a few extensions to CSDL to accommodate the needs of REST based web services exposed through Azure Marketplace.</span></span> <span data-ttu-id="a5d52-180">Uzantıları bulunan [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) ad alanı.</span><span class="sxs-lookup"><span data-stu-id="a5d52-180">The extensions are found in the [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) namespace.</span></span>

<span data-ttu-id="a5d52-181">CSDL örneği izler: (Kopyala ve Yapıştır örnek CSDL bir XML Düzenleyicisi'ni ve değişiklik hizmetinizi eşleştirmek için aşağıda.</span><span class="sxs-lookup"><span data-stu-id="a5d52-181">An example of the CSDL follows:  (Copy and paste the below example CSDL into an XML editor and change to match your Service.</span></span>  <span data-ttu-id="a5d52-182">CSDL eşleme DataService sekmesi altında hizmetinizi oluştururken yapıştırın [Azure Marketi'nde yayımlama portalında](https://publish.windowsazure.com)).</span><span class="sxs-lookup"><span data-stu-id="a5d52-182">Then paste into CSDL Mapping under DataService tab when creating your service in the  [Azure Marketplace Publishing Portal](https://publish.windowsazure.com)).</span></span>

<span data-ttu-id="a5d52-183">**Koşulları:** CSDL ilgili koşulları için [yayımlama portalında](https://publish.windowsazure.com) UI (PPUI) koşulları.</span><span class="sxs-lookup"><span data-stu-id="a5d52-183">**Terms:** Relating the CSDL terms to the [Publishing Portal](https://publish.windowsazure.com) UI (PPUI) terms.</span></span>

* <span data-ttu-id="a5d52-184">PPUI "Title" MyWebOffer için ilgili teklif</span><span class="sxs-lookup"><span data-stu-id="a5d52-184">Offer “Title” in the PPUI relates to MyWebOffer</span></span>
* <span data-ttu-id="a5d52-185">PPUI Şirketim ilişkili **yayımcı görünen adı** içinde [Microsoft Developer Center'da](http://dev.windows.com/registration?accountprogram=azure) kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="a5d52-185">MyCompany in the PPUI relates to **Publisher Display Name** in the [Microsoft Developer Center](http://dev.windows.com/registration?accountprogram=azure) UI</span></span>
* <span data-ttu-id="a5d52-186">Bir Web veya veri hizmeti (PPUI planında) API'nizi öğesiyle ilişkili</span><span class="sxs-lookup"><span data-stu-id="a5d52-186">Your API relates to a Web or Data Service (a Plan in the PPUI)</span></span>

<span data-ttu-id="a5d52-187">**Hiyerarşi:** tanesine olan tekliflerini sahibinin şirket (içerik sağlayıcısı), yani service(s), bir API ile hangi hizalamak.</span><span class="sxs-lookup"><span data-stu-id="a5d52-187">**Hierarchy:** A Company (Content Provider) owns Offer(s) which have Plan(s), namely service(s), which line up with an API.</span></span>

### <a name="webservice-csdl-example"></a><span data-ttu-id="a5d52-188">Web hizmeti CSDL örneği</span><span class="sxs-lookup"><span data-stu-id="a5d52-188">WebService CSDL Example</span></span>
<span data-ttu-id="a5d52-189">Bir web uygulaması uç noktası (örneğin, C# uygulaması) gösterme hizmetine bağlanır</span><span class="sxs-lookup"><span data-stu-id="a5d52-189">Connects to a service that is exposing an web application endpoint (like a C# application)</span></span>

        <?xml version="1.0" encoding="utf-8"?>
        <!-- The namespace attribute below is used by our system to generate C#. You can change “MyCompany.MyOffer” to something that makes sense for you, but change “MyOffer” consistently throughout the document. -->
        <Schema Namespace="MyCompany.MyWebOffer" Alias="MyOffer" xmlns="http://schemas.microsoft.com/ado/2009/08/edm" xmlns:d="http://schemas.microsoft.com/dallas/2010/04" >
        <!-- EntityContainer groups all the web service calls together into a single offering. Every web service call has a FunctionImport definition. -->
          <EntityContainer Name="MyOffer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
        @Name is used as reference by FunctionImport @EntitySet. And is used in the customer facing UI as name of the Service.
        @EntityType is used to point at the type definition near the bottom of this file. -->
            <EntitySet Name="MyEntities" EntityType="MyOffer.MyEntityType" />
        <!-- Add a FunctionImport for every service method. Multiple FunctionImports can share a single return type (EntityType). -->
        <!-- ReturnType is either Raw() for a stream or Collection() for an Atom feed. Ex. of Raw: ReturnType=”Raw(text/plain)” -->
        <!—EntitySet is the entityset defined above, and is needed if ReturnType is not Raw -->
        <!-- BaseURI attribute defines the service call, replace & with the encode value (&amp;).
        In the input name value pairs {param} represents passed in value.
        Or the value can be hard coded as with AccountKey. -->
        <!-- AllowedHttpMethods optional (default = “GET”), allows the CSDL to specifically specify the verb of the service, “Get”, “Post”, “Put”, or “Delete”. -->
        <!-- EncodeParameterValues, True encodes the parameter values, false does not. -->
        <!-- BaseURI is translated into an URITemplate which defines how the web service call is exposed to marketplace customers.
        Ex. https://api.datamarket.azure.com/mycompany/MyOfferPlan?name={name}
        BaseURI is XML encoded, the {...} point to the parameters defined below.
        Marketplace will read the parameters from this URITemplate and fill the values into the corresponding parameters of the BaseUri or RequestBody (below) during calls to your service.  
        It is okay for @d:BaseUri to include information only for Marketplace consumption, it will not be exposed to end users. i.e. the hardcoded AccountKey in the above BaseURI does not show up in the client facing URITemplate. -->
            <FunctionImport Name="MyWebServiceMethod"
                            EntitySet="MyEntities"
                            ReturnType="Collection(MyOffer.MyEntityType)"
        d:AllowedHttpMethods="GET"
        d:EncodeParameterValues="true"
        d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <!-- Definition of the RequestBody is only required for HTTP POST requests and is optional for HTTP GET requests. -->
        <d:RequestBody d:httpMethod="POST">
                <!-- Use {} for placeholders to insert parameters. -->
                <!-- This example uses SOAP formatting, but any POST body can be used. -->
            <!-- This example shows how to pass userid and password via the header -->
                <![CDATA[<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:MyOffer="http://services.organization.net/MyServicePath">
                  <soapenv:Header/>
                  <soapenv:Body>
                    <MyOffer:ws_MyWebServiceMethod>
                      <myWebServiceMethodRequest>
                        <!--This information is not exposed to end users. -->
                        <UserId>userid</UserId>
                        <Password>password</Password>
                        <!-- {name} is replaced with the value read from @d:UriTemplate above -->
                        <Name>{name}</Name>
                        <!-- Parameters can be used more than once and are not limited to appearing as the value of an element -->
                        <CustomField Name="{name}" />
                        <MyField>Static content</MyField>
                      </myWebServiceMethodRequest>
                    </MyOffer:ws_MyWebServiceMethod>
                  </soapenv:Body>
                </soapenv:Envelope>      
              ]]>
        </d:RequestBody>
        <!-- Title, Rights and Description are optional and used to specify values to insert into the ATOM feed returned to the end user.  You can specify the element to contain a fixed message by providing a value for the element (this is the default value).  @d:Map is an XPath expression that points into the response returned by your service and is optional.  -->
        <d:Title d:Map="/MyResponse/Title">Default title.</d:Title>
        <d:Rights>© My copyright. This is a fixed response. It is okay to also add a d:Map attribute to override this text.</d:Rights>
        <d:Description d:Map="/MyResponse/Description"></d:Description>
        <d:Namespaces>
        <d:Namespace d:Prefix="p"  d:Uri="http://schemas.organization.net/2010/04/myNamespace" />
        <d:Namespace d:Prefix="p2" d:Uri="http://schemas.organization.net/2010/04/MyNamespace2" />
        </d:Namespaces>
        <!-- Parameters of the web service call:
        @Name should match exactly (case sensitive) the {…} placeholders in the @d:BaseUri, @d:UriTemplate, and d:RequestBody, i.e. “name” parameter in above BaseURI.
        @Mode is always "In", compatibility with CSDL
        @Type is the EDM.SimpleType of the parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx
        @d:Nullable indicates whether the parameter is required.
        @d:Regex - optional, attribute to describe the string, limiting unwanted input at the entry of the system
        @d:Description - optional, is used by Service Explorer as help information
        @d:SampleValues - optional, is used by Service Explorer as help information. Multiple Sample values are separated by '|', e.g. "804735132|234534224|23409823234"
        @d:Enum - optional for string type. Contains an enumeration of possible values separated by a '|', e.g. d:enum="english|metric|raw". Will be converted in a dropdown list in the Service Explorer.
        -->
        <Parameter name="name" Mode="In" Type="String" d:Nullable="false" d:Regex="^[a-zA-Z]*$" d:Description="A name that cannot contain any spaces or non-alpha non-English characters"
        d:Enum="George|John|Thomas|James"
        d:SampleValues="George"/>
        <Parameter Name=" AccountKey" Mode="In" Type="String" d:Nullable="false" />

        <!-- d:ErrorHandling is an optional element. Use it define standardized errors by evaluating the service response. -->
        <d:ErrorHandling>
        <!-- Any number of d:Condition elements are allowed, they are evaluated in the order listed.
        @d:Match is an Xpath query on the service response, it should return true or false where true indicates an error.
        @d:httpStatusCode is the error code to return if an response matches the error.
        @d:errorMessage is the user friendly message to return when an error occurs.
        -->
        <d:Condition d:Match="/Result/ErrorMessage[text()='Invalid token']" d:HttpStatusCode="403" d:ErrorMessage="User cannot connect to the service." />
        </d:ErrorHandling>
           </FunctionImport>

            <!-- The EntityContainer defines the output data schema -->
        </EntityContainer>
        <!-- The EntityType @d:Map defines the repeating node (an XPath query) in the response (output data schema). -->
        <!-- If these nodes are outside a namespace, add the prefix in the xpath. -->
        <!--
        @Name - define your user readable name, will become an XML element in the ATOM feed, so comply with the XML element naming restrictions (no spaces or other illegal characters).
        @Type is the EDM.SimpleType of the parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx.
        @d:Map uses an Xpath query to point at the location to extract the content from your services response.
        The "." is relative to the repeating node in the EntityType @d:Map Xpath expression.
        -->
            <EntityType Name="MyEntityType" d:Map="/MyResponse/MyEntities">
        <Property Name="ID"    d:IsPrimaryKey="True" Type="Int32"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="Amount"    Type="Double"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="City"    Type="String"    Nullable="false" d:Map="./City"/>
        <Property Name="State"    Type="String"    Nullable="false" d:Map="./State"/>
        <Property Name="Zip"    Type="Int32"    Nullable="false" d:Map="./Zip"/>
        <Property Name="Updated"    Type="DateTime"    Nullable="false" d:Map="./Updated"/>
        <Property Name="AdditionalInfo" Type="String" Nullable="true"
        d:Map="./Info/More[1]"/>
            </EntityType>
        </Schema>

> [!TIP]
> <span data-ttu-id="a5d52-190">Daha fazla CSDL Web hizmeti örnekleri makaleyi görüntülemek [var olan eşleme örnekleri web CSDLs aracılığıyla OData hizmeti](marketplace-publishing-data-service-creation-odata-mapping-examples.md)</span><span class="sxs-lookup"><span data-stu-id="a5d52-190">View more CSDL Web Service examples in the article [Examples of mapping an existing web service to OData through CSDLs](marketplace-publishing-data-service-creation-odata-mapping-examples.md)</span></span>
> 
> 

### <a name="dataservice-csdl-example"></a><span data-ttu-id="a5d52-191">DataService CSDL örneği</span><span class="sxs-lookup"><span data-stu-id="a5d52-191">DataService CSDL Example</span></span>
<span data-ttu-id="a5d52-192">Temel veriler için iki API'leri API (tablolar yerine görünümleri kullanabilirsiniz) CSDL dayalı bir uç nokta örnek aşağıda gösterildiği gibi bir veritabanı tablosu veya görünümü gösterme bir hizmete bağlanır.</span><span class="sxs-lookup"><span data-stu-id="a5d52-192">Connects to a service that is exposing a database table or view as an endpoint Below example shows two APIs for Data base based API CSDL (can use views rather than tables).</span></span>

        <?xml version="1.0"?>
        <!-- The namespace attribute below is used by our system to generate C#. You can change “MyCompany.MyOffer” to something that makes sense for you, but change “MyOffer” consistently throughout the document. -->
        <Schema Namespace="MyCompany.MyDataOffer" Alias="MyOffer" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ado/2009/08/edm">
        <!-- EntityContainer groups all the data service calls together into a single offering. Every web service call has a FunctionImport definition. -->
        <EntityContainer Name="MyOfferContainer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
            Think of the EntitySet as a Service
        @Name is used in the customer facing UI as name of the Service.
        @EntityType is used to point at the type definition (returned set of table columns). -->
        <EntitySet Name="CompanyInfoEntitySet" EntityType="MyOffer.CompanyInfo" />
        <EntitySet Name="ProductInfoEntitySet" EntityType="MyOffer.ProductInfo" />
        </EntityContainer>
        <!-- EntityType defines result (output); the table (or view) and columns to be returned by the data service.)
            Map is the schema.tabel or schema.view
            dals.TableName is the table Name
            Name is the name identifier for the EntityType and the Name of the service exposed to the client via the UI.
            dals:IsExposed determines if the table schema is exposed (generally true).
            dals:IsView (optional) true if this is based on a view rather than a table
            dals:TableSchema is the schema name of the table/view
        -->
        <EntityType
        Map="[dbo].[CompanyInfo]"
        dals:TableName="CompanyInfo"
        Name="CompanyInfo"
        dals:IsExposed="true"
        dals:IsView="false"
        dals:TableSchema="dbo"
        xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <!-- Property defines the column properties and the output of the service.
            dals:ColumnName is the name of the column in the table /view.
            Type is the emd.SimpleType
            Nullable determines if NULL is a valid output value
            dals.CharMaxLenght is the maximum length of the output value
            Name is the name of the Property and is exposed to the client facing UI
            dals:IsReturned is the Boolean that determines if the Service exposes this value to the client.
            IsQueryable is the Boolean that determines if the column can be used in a database query
            (For data Services: To improve Performance make sure that columns marked ISQueryable=”true” are in an index.)
            dals:OrdinalPosition is the numerical position x in the table or the View, where x is from 1 to the number of columns in the table.
            dals:DatabaseDataType is the data type of the column in the database, i.e. SQL data type dals:IsPrimaryKey indicates if the column is the Primary key in the table/view.  (The columns marked ISPrimaryKey are used in the Order by clause when returning data.)
        -->
        <Property dals:ColumnName="data" Type="String" Nullable="true" dals:CharMaxLength="-1" Name="data" dals:IsReturned="true" dals:IsQueryable="false" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="ticker" Type="String" Nullable="true" dals:CharMaxLength="10" Name="ticker" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        <EntityType Map="[dbo].[ProductInfo]" dals:TableName="ProductInfo" Name="ProductInfo" dals:IsExposed="true" dals:IsView="false" dals:TableSchema="dbo" xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <Property dals:ColumnName="companyid" Type="Int32" Nullable="true" Name="companyid" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="product" Type="String" Nullable="true" dals:CharMaxLength="50" Name="product" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        </Schema>

## <a name="see-also"></a><span data-ttu-id="a5d52-193">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a5d52-193">See Also</span></span>
* <span data-ttu-id="a5d52-194">Öğrenme ve belirli düğümler ve bunların parametrelerini anlama ilgileniyorsanız, bu makaleyi okuyun [veri hizmeti OData eşleme düğümleri](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) tanımları ve açıklamalar, örnekler ve kullanım örneği bağlamı.</span><span class="sxs-lookup"><span data-stu-id="a5d52-194">If you are interested in learning and understanding the specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="a5d52-195">Örnekler gözden geçirme ilgileniyorsanız, bu makaleyi okuyun [veri hizmeti OData eşleme örnekler](marketplace-publishing-data-service-creation-odata-mapping-examples.md) örnek kodu görmek ve kod sözdizimi ve bağlamı anlamak için.</span><span class="sxs-lookup"><span data-stu-id="a5d52-195">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) to see sample code and understand code syntax and context.</span></span>
* <span data-ttu-id="a5d52-196">Veri Hizmeti Azure Marketinde yayımlama için belirtilen yol dönmek için bu makaleyi okuyun [veri hizmeti yayımlama Kılavuzu](marketplace-publishing-data-service-creation.md).</span><span class="sxs-lookup"><span data-stu-id="a5d52-196">To return to the prescribed path for publishing a Data Service to the Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

