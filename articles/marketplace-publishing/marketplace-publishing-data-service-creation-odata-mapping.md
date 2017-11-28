---
title: "aaaGuide toocreating hello Market için veri hizmeti | Microsoft Docs"
description: "Nasıl toocreate, onaylamak ve dağıtmak için bir veri hizmeti ayrıntılı yönergeler hello üzerinde Azure Market satın alın."
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
ms.openlocfilehash: deb2e52dd03f5beb2ad6a927bd2d03e47d20b691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="mapping-an-existing-web-service-tooodata-through-csdl"></a><span data-ttu-id="9565f-103">Var olan bir web hizmeti tooOData CSDL aracılığıyla eşleme</span><span class="sxs-lookup"><span data-stu-id="9565f-103">Mapping an existing web service tooOData through CSDL</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9565f-104">**Şu anda artık ekleme duyuyoruz herhangi yeni veri hizmeti yayımcılar. Yeni dataservices listesine onaylanmamış.**</span><span class="sxs-lookup"><span data-stu-id="9565f-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="9565f-105">Bir SaaS iş uygulaması varsa toopublish istediğiniz AppSource hakkında daha fazla bilgi bulabilirsiniz [burada](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="9565f-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="9565f-106">Bir Iaas uygulamalar varsa veya Geliştirici hizmeti misiniz Azure Market'te toopublish gibi daha fazla bilgi bulabilirsiniz [burada](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="9565f-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="9565f-107">Bu makalede hakkında genel bir fikir veren toouse CSDL toomap var olan bir hizmet tooan OData uyumlu hizmeti.</span><span class="sxs-lookup"><span data-stu-id="9565f-107">This article gives an overview on how toouse a CSDL toomap an existing service tooan OData compatible service.</span></span> <span data-ttu-id="9565f-108">Bunu nasıl toocreate hello eşleme belge (CSDL) hello giriş hello istemci hizmeti çağrısı ve hello aracılığıyla isteğinden Dönüşümleri (veri) geri toohello istemci OData uyumlu akışı aracılığıyla çıktı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9565f-108">It explains how toocreate hello mapping document (CSDL) that transforms hello input request from hello client via a service call and hello output (data) back toohello client via an OData compatible feed.</span></span> <span data-ttu-id="9565f-109">Microsoft Azure Marketi'nde Hizmetleri toohello son kullanıcılar hello OData protokolünü kullanarak kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="9565f-109">Microsoft’s Azure Marketplace exposes services toohello end-users by using hello OData protocol.</span></span> <span data-ttu-id="9565f-110">(Verileri sahiplerinin) içerik sağlayıcıları tarafından sunulan hizmetler, formlar, REST, SOAP, vb. gibi çeşitli sunulur.</span><span class="sxs-lookup"><span data-stu-id="9565f-110">Services that are exposed by content providers (Data Owners) are exposed in a variety of forms, such as REST, SOAP, etc.</span></span>

## <a name="what-is-a-csdl-and-its-structure"></a><span data-ttu-id="9565f-111">Bir CSDL ve yapısını nedir?</span><span class="sxs-lookup"><span data-stu-id="9565f-111">What is a CSDL and its structure?</span></span>
<span data-ttu-id="9565f-112">CSDL (kavramsal şema tanım dili) nasıl toodescribe web hizmeti veya veritabanı hizmet ortak XML duyuruları toohello Azure Marketi tanımlayan bir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="9565f-112">A CSDL (Conceptual Schema Definition Language) is a specification defining how toodescribe web service or database service in common XML verbiage toohello Azure Marketplace.</span></span>

<span data-ttu-id="9565f-113">Merhaba basit genel bakış **istek akışı:**</span><span class="sxs-lookup"><span data-stu-id="9565f-113">Simple overview of hello **request flow:**</span></span>

  `Client -> Azure Marketplace -> Content Provider’s Web Service (Get, Post, Delete, Put)`

<span data-ttu-id="9565f-114">Merhaba **veri akışı** hello olduğu yönü ters:</span><span class="sxs-lookup"><span data-stu-id="9565f-114">hello **data flow** is in hello opposite direction:</span></span>

  `Client <- Azure Marketplace <- Content Provider’s WebService`

<span data-ttu-id="9565f-115">**Şekil 1** diyagramları nasıl bir istemci verilerini bir içerik sağlayıcı (hizmetinizi) hello Azure Market giderek elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9565f-115">**Figure 1** diagrams how a client would obtain data from a content provider (your service) by going through hello Azure Marketplace.</span></span>  <span data-ttu-id="9565f-116">Merhaba içerik sağlayıcının hizmetlere ve istemci isteyen hello arasında veri iletmek ve Hello CSDL hello eşleme/dönüştürme bileşen toohandle hello isteği tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9565f-116">hello CSDL is used by hello Mapping/Transformation component toohandle hello request and data pass between hello content provider’s service(s) and hello requesting client.</span></span>

<span data-ttu-id="9565f-117">*Şekil 1: istemci toocontent sağlayıcısı aracılığıyla Azure Marketi isteyen gelen ayrıntılı akış*</span><span class="sxs-lookup"><span data-stu-id="9565f-117">*Figure 1: Detailed flow from requesting client toocontent provider via Azure Marketplace*</span></span>

  ![Çizim](media/marketplace-publishing-data-service-creation-odata-mapping/figure-1.png)

<span data-ttu-id="9565f-119">Atom, Atom Pub ve hello OData Protokolü hangi hello Azure Marketi uzantıları derleme sırasında arka plan için lütfen gözden geçirin: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)</span><span class="sxs-lookup"><span data-stu-id="9565f-119">For background on Atom, Atom Pub, and hello OData protocol upon which hello Azure Marketplace extensions build, please review: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)</span></span>

<span data-ttu-id="9565f-120">Bağlantı yukarıdaki alıntı: *"Merhaba açık veri Protokolü (bundan böyle başvurulan tooas OData) hello amacı protokolüdür tooprovide REST tabanlı veri hizmetleri sunulan kaynaklara karşı stili CRUD işlemleri (oluşturma, okuma, güncelleştirme ve silme). "Veri hizmeti" bir uç noktadır koleksiyonlardan bir veya daha fazla"" her ", oluşur sıfır veya daha fazla girişlerini" ile kullanıma sunulan veri olduğu adlı-değer çiftleri belirtilmiş. Toocan isteyen herkes yapı sunucuları, istemcileri veya Araçlar telif hakkı veya kısıtlamaları olmadan böylece OData OASIS (Merhaba terfi yapılandırılmış bilgi standartlar için kuruluş) standartları altında Microsoft tarafından yayımlanan."*</span><span class="sxs-lookup"><span data-stu-id="9565f-120">Excerpt from above link: *“hello purpose of hello Open Data protocol (hereafter referred tooas OData) is tooprovide a REST-based protocol for CRUD-style operations (Create, Read, Update and Delete) against resources exposed as data services. A “data service” is an endpoint where there is data exposed from one or more “collections” each with zero or more “entries”, which consist of typed named-value pairs. OData is published by Microsoft under OASIS (Organization for hello Advancement of Structured Information Standards) Standards so that anyone that wants toocan build servers, clients or tools without royalties or restrictions.”*</span></span>

### <a name="three-critical-pieces-that-have-toobe-defined-by-hello-csdl-are"></a><span data-ttu-id="9565f-121">Üç kritik CSDL hello tarafından tanımlanan toobe sahip parça şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9565f-121">Three Critical Pieces that have toobe defined by hello CSDL are:</span></span>
* <span data-ttu-id="9565f-122">Merhaba **endpoint** hello hizmet sağlayıcısı Web adresi (URI) hello hizmeti ile Merhaba</span><span class="sxs-lookup"><span data-stu-id="9565f-122">hello **endpoint** of hello Service Provider hello Web Address (URI) of hello Service</span></span>
* <span data-ttu-id="9565f-123">Merhaba **veri parametreleri** giriş toohello hizmet sağlayıcısı hello tanımları toohello veri türü toohello içerik sağlayıcının hizmeti gönderilen hello parametrelerinin geçirilen.</span><span class="sxs-lookup"><span data-stu-id="9565f-123">hello **data parameters** being passed as input toohello Service Provider hello definitions of hello parameters being sent toohello Content Provider’s service down toohello data type.</span></span>
* <span data-ttu-id="9565f-124">**Şema** toohello isteyen hizmeti hello şema hello içerik sağlayıcının hizmeti tarafından teslim edilmesini hello verinin döndürülmesini hello verilerinin kapsayıcı, koleksiyonları/tabloları, değişkenleri/sütunları ve veri türleri dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="9565f-124">**Schema** of hello data being returned toohello Requesting Service hello schema of hello data being delivered by hello Content Provider’s service, including Container, collections/tables, variables/columns, and data types.</span></span>

<span data-ttu-id="9565f-125">Diyagram aşağıdaki hello hello akış burada hello istemci hello OData deyimi (çağrı toohello içerik sağlayıcının web hizmeti) toogetting hello sonuçları/verileri geri girer gelen genel bir bakış gösterilir.</span><span class="sxs-lookup"><span data-stu-id="9565f-125">hello following diagram shows an overview of hello flow from where hello client enters hello OData statement (call toohello content provider’s web service) toogetting hello results/data back.</span></span>

  ![Çizim](media/marketplace-publishing-data-service-creation-odata-mapping/figure-2.png)

### <a name="steps"></a><span data-ttu-id="9565f-127">adımlar:</span><span class="sxs-lookup"><span data-stu-id="9565f-127">Steps:</span></span>
1. <span data-ttu-id="9565f-128">İstemci isteği hizmet aramasıyla giriş XML toohello Azure Marketi tanımlanan parametrelere sahip tam gönderir</span><span class="sxs-lookup"><span data-stu-id="9565f-128">Client sends request via Service call complete with Input Parameters defined in XML toohello Azure Marketplace</span></span>
2. <span data-ttu-id="9565f-129">CSDL kullanılan toovalidate hello hizmeti çağrısı ' dir.</span><span class="sxs-lookup"><span data-stu-id="9565f-129">CSDL is used toovalidate hello Service call.</span></span>
   * <span data-ttu-id="9565f-130">Merhaba biçimlendirilmiş hizmetini çağırmak toohello içerik sağlayıcıları hizmeti hello Azure Marketi tarafından gönderilir</span><span class="sxs-lookup"><span data-stu-id="9565f-130">hello Formatted Service Call is then sent toohello Content Providers Service by hello Azure Marketplace</span></span>
3. <span data-ttu-id="9565f-131">Merhaba Webservice yürütür ve hello eylemin hello Http Fiili preforms (yani GET) hello veriler döndürülür tooAzure burada hello istenen veriler (varsa) Market XML biçiminde toohello istemci çıkarır eşleme tanımlanan hello CSDL hello kullanarak.</span><span class="sxs-lookup"><span data-stu-id="9565f-131">hello Webservice executes and preforms hello action of hello Http Verb (i.e. GET) hello data is returned tooAzure Marketplace where hello requested data (if any) is exposes in XML Format toohello Client using hello Mapping defined in hello CSDL.</span></span>
4. <span data-ttu-id="9565f-132">Merhaba istemci hello veriler (varsa) XML veya JSON biçiminde gönderilir</span><span class="sxs-lookup"><span data-stu-id="9565f-132">hello Client is sent hello data (if any) in XML or JSON format</span></span>

## <a name="definitions"></a><span data-ttu-id="9565f-133">Tanımlar</span><span class="sxs-lookup"><span data-stu-id="9565f-133">Definitions</span></span>
### <a name="odata-atom-pub"></a><span data-ttu-id="9565f-134">OData ATOM pub</span><span class="sxs-lookup"><span data-stu-id="9565f-134">OData ATOM pub</span></span>
<span data-ttu-id="9565f-135">Her girişin bir sonucu olarak bir satır temsil ettiği bir uzantı toohello ATOM pub ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9565f-135">An extension toohello ATOM pub where each entry represents one row of a result set.</span></span> <span data-ttu-id="9565f-136">Merhaba içerik hello girişi Gelişmiş toocontain hello değerleri hello satırının – anahtar değer çiftleri olarak parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="9565f-136">hello content part of hello entry is enhanced toocontain hello values of hello row – as key value pairs.</span></span> <span data-ttu-id="9565f-137">Daha fazla bilgi aşağıda bulunan: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)</span><span class="sxs-lookup"><span data-stu-id="9565f-137">More information is found here: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)</span></span>

### <a name="csdl---conceptual-schema-definition-language"></a><span data-ttu-id="9565f-138">CSDL - kavramsal şema tanım dili</span><span class="sxs-lookup"><span data-stu-id="9565f-138">CSDL - Conceptual Schema Definition Language</span></span>
<span data-ttu-id="9565f-139">İşlevler (SPROCs) tanımlanmasına olanak sağlar ve bir veritabanı yoluyla kullanıma sunulan varlıklar.</span><span class="sxs-lookup"><span data-stu-id="9565f-139">Allows defining functions (SPROCs) and entities that are exposed through a database.</span></span> <span data-ttu-id="9565f-140">Burada bulunan daha fazla bilgi: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)</span><span class="sxs-lookup"><span data-stu-id="9565f-140">More information found here: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)</span></span>  

> [!TIP]
> <span data-ttu-id="9565f-141">Merhaba tıklatın **diğer sürümleri** açılır ve hello makale görmüyorsanız, bir sürümü seçin.</span><span class="sxs-lookup"><span data-stu-id="9565f-141">Click hello **other versions** dropdown and select a version if you don’t see hello article.</span></span>
> 
> 

### <a name="edm---entry-data-model"></a><span data-ttu-id="9565f-142">EDM - giriş veri modeli</span><span class="sxs-lookup"><span data-stu-id="9565f-142">EDM - Entry Data Model</span></span>
* <span data-ttu-id="9565f-143">Genel Bakış: [http://msdn.microsoft.com/library/vstudio/ee382825 (v=vs.100).aspx][OverviewLink]</span><span class="sxs-lookup"><span data-stu-id="9565f-143">Overview: [http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]</span></span>

[OverviewLink]:http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx
* <span data-ttu-id="9565f-144">Önizleme: [http://msdn.microsoft.com/library/aa697428 (v=vs.80).aspx][PreviewLink]</span><span class="sxs-lookup"><span data-stu-id="9565f-144">Preview: [http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]</span></span>

[PreviewLink]:http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx
* <span data-ttu-id="9565f-145">Veri türleri: [http://msdn.microsoft.com/library/bb399548 (v=VS.100).aspx][DataTypesLink]</span><span class="sxs-lookup"><span data-stu-id="9565f-145">Data types: [http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]</span></span>

[DataTypesLink]:http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx

<span data-ttu-id="9565f-146">Burada hello istemci hello OData deyimi (çağrı toohello içerik sağlayıcının web hizmeti) toogetting hello sonuçları/verileri geri girer gelen sol tooRight akış hello ayrıntılı Hello aşağıdakileri gösterir:</span><span class="sxs-lookup"><span data-stu-id="9565f-146">hello following shows hello detailed Left tooRight flow from where hello client enters hello OData statement (call toohello content provider’s web service) toogetting hello results/data back:</span></span>

  ![Çizim](media/marketplace-publishing-data-service-creation-odata-mapping/figure-3.png)

## <a name="csdl-basics"></a><span data-ttu-id="9565f-148">CSDL temelleri</span><span class="sxs-lookup"><span data-stu-id="9565f-148">CSDL Basics</span></span>
<span data-ttu-id="9565f-149">CSDL (kavramsal şema tanım dili) nasıl toodescribe web hizmeti veya veritabanı hizmet ortak XML duyuruları toohello Azure Marketi tanımlayan bir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="9565f-149">A CSDL (Conceptual Schema Definition Language) is a specification defining how toodescribe web service or database service in common XML verbiage toohello Azure Marketplace.</span></span> <span data-ttu-id="9565f-150">CSDL açıklar hello kritik parça **hello veri kaynağı toohello Azure Marketi gelen verilerin hello geçirme mümkün kılar.**</span><span class="sxs-lookup"><span data-stu-id="9565f-150">CSDL describes hello critical pieces that **makes hello passing of data from hello Data Source toohello Azure Marketplace possible.**</span></span> <span data-ttu-id="9565f-151">Merhaba ana parçalar aşağıda açıklanmıştır:</span><span class="sxs-lookup"><span data-stu-id="9565f-151">hello main pieces are described here:</span></span>

* <span data-ttu-id="9565f-152">Tüm genel kullanıma açık işlevleri (Functionımport düğümü) açıklayan bilgileri arabirimi</span><span class="sxs-lookup"><span data-stu-id="9565f-152">Interface information describing all publicly available functions (FunctionImport Node)</span></span>
* <span data-ttu-id="9565f-153">Veri türü bilgileri tüm ileti requests(input) ve ileti responses(outputs) (EntitySet/EntityContainer/EntityType düğümler)</span><span class="sxs-lookup"><span data-stu-id="9565f-153">Data type information for all message requests(input) and message responses(outputs) (EntityContainer/EntitySet/EntityType Nodes)</span></span>
* <span data-ttu-id="9565f-154">Merhaba Aktarım Protokolü toobe hakkında bilgi bağlama (üstbilgi düğümü) kullanılır</span><span class="sxs-lookup"><span data-stu-id="9565f-154">Binding information about hello transport protocol toobe used (Header Node)</span></span>
* <span data-ttu-id="9565f-155">Hizmet (tabanURI özniteliği) hello yerini adres bilgilerini belirtilen</span><span class="sxs-lookup"><span data-stu-id="9565f-155">Address information for locating hello specified service (BaseURI attribute)</span></span>

<span data-ttu-id="9565f-156">Buna koysalar hello CSDL hello hizmet istek sahibi ve hello hizmet sağlayıcısı arasında bir platform ve dilden bağımsız sözleşme temsil eder.</span><span class="sxs-lookup"><span data-stu-id="9565f-156">In a nutshell, hello CSDL represents a platform- and language-independent contract between hello service requestor and hello service provider.</span></span> <span data-ttu-id="9565f-157">Bir istemci, Hello CSDL'ı kullanarak bir web hizmeti/veritabanı hizmetini bulun ve herhangi bir genel kullanıma açık işlevlerini çağırma.</span><span class="sxs-lookup"><span data-stu-id="9565f-157">Using hello CSDL, a client can locate a web service/database service and invoke any of its publicly available functions.</span></span>

### <a name="relating-a-csdl-tooa-database-or-a-collection"></a><span data-ttu-id="9565f-158">CSDL tooa veritabanı veya bir koleksiyon ilgili</span><span class="sxs-lookup"><span data-stu-id="9565f-158">Relating a CSDL tooa Database or a Collection</span></span>
<span data-ttu-id="9565f-159">**Merhaba CSDL belirtimi**</span><span class="sxs-lookup"><span data-stu-id="9565f-159">**hello CSDL Specification**</span></span>

<span data-ttu-id="9565f-160">CSDL açıklayan bir web hizmeti için XML dilbilgisi ' dir.</span><span class="sxs-lookup"><span data-stu-id="9565f-160">CSDL is XML grammar for describing a web service.</span></span> <span data-ttu-id="9565f-161">Merhaba belirtimi kendisini 4 ana elemanlara bölünür: EntitySet, Functionımport; Ad alanı ve EntityType.</span><span class="sxs-lookup"><span data-stu-id="9565f-161">hello specification itself is divided into 4 major elements:  EntitySet, FunctionImport; NameSpace, and EntityType.</span></span>

<span data-ttu-id="9565f-162">Bu soyutlama daha kolay toounderstand CSDL tooa tablosu arasında ilişki toomake olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="9565f-162">toomake this abstraction easier toounderstand lets relate a CSDL tooa table.</span></span>

<span data-ttu-id="9565f-163">Unutmayın;</span><span class="sxs-lookup"><span data-stu-id="9565f-163">Remember;</span></span>

  <span data-ttu-id="9565f-164">CSDL temsil eden bir platform ve dilden bağımsız sözleşme hello arasında **hizmet istek sahibi** ve hello **hizmet sağlayıcısı**.</span><span class="sxs-lookup"><span data-stu-id="9565f-164">CSDL represents a platform- and language-independent contract between hello **service requestor** and hello **service provider**.</span></span> <span data-ttu-id="9565f-165">CSDL, kullanarak bir **istemci** bulabilir bir **web hizmeti/veritabanı hizmeti** ve kendi genel kullanıma açık hiçbirini çağırma **işlevleri.**</span><span class="sxs-lookup"><span data-stu-id="9565f-165">Using CSDL, a **client** can locate a **web service/database service** and invoke any of its publicly available **functions.**</span></span>

<span data-ttu-id="9565f-166">Bir veri hizmeti Merhaba bir CSDL dört bölümden, veritabanı, tablo, sütun ve deposu yordamı bakımından değerlendirilebilir.</span><span class="sxs-lookup"><span data-stu-id="9565f-166">For a Data Service hello four parts of a CSDL can be thought of in terms of a Database, Table, Column, and Store Procedure.</span></span>

<span data-ttu-id="9565f-167">Bu gibi bir veri hizmeti ile ilgili:</span><span class="sxs-lookup"><span data-stu-id="9565f-167">Relating these as follows for a Data Service:</span></span>

* <span data-ttu-id="9565f-168">EntityContainer ~ = veritabanı</span><span class="sxs-lookup"><span data-stu-id="9565f-168">EntityContainer  ~=  Database</span></span>
* <span data-ttu-id="9565f-169">EntitySet ~ = tablosu</span><span class="sxs-lookup"><span data-stu-id="9565f-169">EntitySet  ~=  Table</span></span>
* <span data-ttu-id="9565f-170">EntityType ~ sütunları =</span><span class="sxs-lookup"><span data-stu-id="9565f-170">EntityType  ~= Columns</span></span>
* <span data-ttu-id="9565f-171">Functionımport ~ saklı yordam =</span><span class="sxs-lookup"><span data-stu-id="9565f-171">FunctionImport  ~=  Stored Procedure</span></span>

<span data-ttu-id="9565f-172">**İzin verilen HTTP fiilleri**</span><span class="sxs-lookup"><span data-stu-id="9565f-172">**HTTP Verbs allowed**</span></span>

* <span data-ttu-id="9565f-173">GET-(bir koleksiyon döndürür) hello DB'den değerler verir</span><span class="sxs-lookup"><span data-stu-id="9565f-173">GET – returns values from hello db (returns a Collection)</span></span>
* <span data-ttu-id="9565f-174">POST – toopass veri tooand isteğe bağlı dönüş değerleri (Merhaba koleksiyonundaki dönüş kimliği/URI'si yeni bir giriş oluşturun) hello DB'den kullanılan</span><span class="sxs-lookup"><span data-stu-id="9565f-174">POST – used toopass data tooand optional return values from hello db (Create a new entry in hello collection, return id/URI)</span></span>
* <span data-ttu-id="9565f-175">SİLME – (koleksiyonu siler) hello DB verilerden siler</span><span class="sxs-lookup"><span data-stu-id="9565f-175">DELETE – Deletes data from hello DB (Deletes a collection)</span></span>
* <span data-ttu-id="9565f-176">PUT – bir Veritabanına veri güncelleştirme (bir koleksiyon değiştirin veya bir tane oluşturun)</span><span class="sxs-lookup"><span data-stu-id="9565f-176">PUT – Update data into a DB (replace a collection or create one)</span></span>

## <a name="metadatamapping-document"></a><span data-ttu-id="9565f-177">Meta veri/eşleme belge</span><span class="sxs-lookup"><span data-stu-id="9565f-177">Metadata/Mapping Document</span></span>
<span data-ttu-id="9565f-178">Böylece hello Azure Marketi sistem tarafından bir OData web hizmeti olarak verilebilen bir içerik sağlayıcının varolan web hizmetleri kullanılan toomap Hello meta veri/eşleme belgedir.</span><span class="sxs-lookup"><span data-stu-id="9565f-178">hello metadata/mapping document is used toomap a content provider’s existing web services so that it can be exposed as an OData web service by hello Azure Marketplace system.</span></span> <span data-ttu-id="9565f-179">Implements birkaç uzantıları tooCSDL tooaccommodate hello ihtiyaçlarını REST Azure Market üzerinden kullanıma sunulan web hizmetleri tabanlı ve CSDL üzerinde temel alır.</span><span class="sxs-lookup"><span data-stu-id="9565f-179">It is based on CSDL and implements a few extensions tooCSDL tooaccommodate hello needs of REST based web services exposed through Azure Marketplace.</span></span> <span data-ttu-id="9565f-180">Merhaba uzantıları hello bulundu [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) ad alanı.</span><span class="sxs-lookup"><span data-stu-id="9565f-180">hello extensions are found in hello [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) namespace.</span></span>

<span data-ttu-id="9565f-181">Merhaba CSDL örneği izler: (Kopyala ve Yapıştır hello örnek CSDL bir XML Düzenleyicisi içine aşağıda ve hizmetinizi toomatch değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9565f-181">An example of hello CSDL follows:  (Copy and paste hello below example CSDL into an XML editor and change toomatch your Service.</span></span>  <span data-ttu-id="9565f-182">CSDL eşleme DataService sekmesi altında hizmetinizi hello oluştururken yapıştırın [Azure Marketi'nde yayımlama portalında](https://publish.windowsazure.com)).</span><span class="sxs-lookup"><span data-stu-id="9565f-182">Then paste into CSDL Mapping under DataService tab when creating your service in hello  [Azure Marketplace Publishing Portal](https://publish.windowsazure.com)).</span></span>

<span data-ttu-id="9565f-183">**Koşulları:** Relating hello CSDL koşulları toohello [yayımlama portalında](https://publish.windowsazure.com) UI (PPUI) koşulları.</span><span class="sxs-lookup"><span data-stu-id="9565f-183">**Terms:** Relating hello CSDL terms toohello [Publishing Portal](https://publish.windowsazure.com) UI (PPUI) terms.</span></span>

* <span data-ttu-id="9565f-184">Merhaba PPUI "Title" tooMyWebOffer ilişkili sunma</span><span class="sxs-lookup"><span data-stu-id="9565f-184">Offer “Title” in hello PPUI relates tooMyWebOffer</span></span>
* <span data-ttu-id="9565f-185">Merhaba PPUI Şirketim ilişkili çok**yayımcı görünen adı** hello içinde [Microsoft Developer Center'da](http://dev.windows.com/registration?accountprogram=azure) kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="9565f-185">MyCompany in hello PPUI relates too**Publisher Display Name** in hello [Microsoft Developer Center](http://dev.windows.com/registration?accountprogram=azure) UI</span></span>
* <span data-ttu-id="9565f-186">API'nizi tooa Web veya veri hizmeti (Merhaba PPUI planında) ilişkilendirir</span><span class="sxs-lookup"><span data-stu-id="9565f-186">Your API relates tooa Web or Data Service (a Plan in hello PPUI)</span></span>

<span data-ttu-id="9565f-187">**Hiyerarşi:** tanesine olan tekliflerini sahibinin şirket (içerik sağlayıcısı), yani service(s), bir API ile hangi hizalamak.</span><span class="sxs-lookup"><span data-stu-id="9565f-187">**Hierarchy:** A Company (Content Provider) owns Offer(s) which have Plan(s), namely service(s), which line up with an API.</span></span>

### <a name="webservice-csdl-example"></a><span data-ttu-id="9565f-188">Web hizmeti CSDL örneği</span><span class="sxs-lookup"><span data-stu-id="9565f-188">WebService CSDL Example</span></span>
<span data-ttu-id="9565f-189">Bir web uygulaması uç noktası (örneğin, C# uygulaması) gösterme tooa hizmet bağlanır</span><span class="sxs-lookup"><span data-stu-id="9565f-189">Connects tooa service that is exposing an web application endpoint (like a C# application)</span></span>

        <?xml version="1.0" encoding="utf-8"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyWebOffer" Alias="MyOffer" xmlns="http://schemas.microsoft.com/ado/2009/08/edm" xmlns:d="http://schemas.microsoft.com/dallas/2010/04" >
        <!-- EntityContainer groups all hello web service calls together into a single offering. Every web service call has a FunctionImport definition. -->
          <EntityContainer Name="MyOffer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
        @Name is used as reference by FunctionImport @EntitySet. And is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition near hello bottom of this file. -->
            <EntitySet Name="MyEntities" EntityType="MyOffer.MyEntityType" />
        <!-- Add a FunctionImport for every service method. Multiple FunctionImports can share a single return type (EntityType). -->
        <!-- ReturnType is either Raw() for a stream or Collection() for an Atom feed. Ex. of Raw: ReturnType=”Raw(text/plain)” -->
        <!—EntitySet is hello entityset defined above, and is needed if ReturnType is not Raw -->
        <!-- BaseURI attribute defines hello service call, replace & with hello encode value (&amp;).
        In hello input name value pairs {param} represents passed in value.
        Or hello value can be hard coded as with AccountKey. -->
        <!-- AllowedHttpMethods optional (default = “GET”), allows hello CSDL toospecifically specify hello verb of hello service, “Get”, “Post”, “Put”, or “Delete”. -->
        <!-- EncodeParameterValues, True encodes hello parameter values, false does not. -->
        <!-- BaseURI is translated into an URITemplate which defines how hello web service call is exposed toomarketplace customers.
        Ex. https://api.datamarket.azure.com/mycompany/MyOfferPlan?name={name}
        BaseURI is XML encoded, hello {...} point toohello parameters defined below.
        Marketplace will read hello parameters from this URITemplate and fill hello values into hello corresponding parameters of hello BaseUri or RequestBody (below) during calls tooyour service.  
        It is okay for @d:BaseUri tooinclude information only for Marketplace consumption, it will not be exposed tooend users. i.e. hello hardcoded AccountKey in hello above BaseURI does not show up in hello client facing URITemplate. -->
            <FunctionImport Name="MyWebServiceMethod"
                            EntitySet="MyEntities"
                            ReturnType="Collection(MyOffer.MyEntityType)"
        d:AllowedHttpMethods="GET"
        d:EncodeParameterValues="true"
        d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <!-- Definition of hello RequestBody is only required for HTTP POST requests and is optional for HTTP GET requests. -->
        <d:RequestBody d:httpMethod="POST">
                <!-- Use {} for placeholders tooinsert parameters. -->
                <!-- This example uses SOAP formatting, but any POST body can be used. -->
            <!-- This example shows how toopass userid and password via hello header -->
                <![CDATA[<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:MyOffer="http://services.organization.net/MyServicePath">
                  <soapenv:Header/>
                  <soapenv:Body>
                    <MyOffer:ws_MyWebServiceMethod>
                      <myWebServiceMethodRequest>
                        <!--This information is not exposed tooend users. -->
                        <UserId>userid</UserId>
                        <Password>password</Password>
                        <!-- {name} is replaced with hello value read from @d:UriTemplate above -->
                        <Name>{name}</Name>
                        <!-- Parameters can be used more than once and are not limited tooappearing as hello value of an element -->
                        <CustomField Name="{name}" />
                        <MyField>Static content</MyField>
                      </myWebServiceMethodRequest>
                    </MyOffer:ws_MyWebServiceMethod>
                  </soapenv:Body>
                </soapenv:Envelope>      
              ]]>
        </d:RequestBody>
        <!-- Title, Rights and Description are optional and used toospecify values tooinsert into hello ATOM feed returned toohello end user.  You can specify hello element toocontain a fixed message by providing a value for hello element (this is hello default value).  @d:Map is an XPath expression that points into hello response returned by your service and is optional.  -->
        <d:Title d:Map="/MyResponse/Title">Default title.</d:Title>
        <d:Rights>© My copyright. This is a fixed response. It is okay tooalso add a d:Map attribute toooverride this text.</d:Rights>
        <d:Description d:Map="/MyResponse/Description"></d:Description>
        <d:Namespaces>
        <d:Namespace d:Prefix="p"  d:Uri="http://schemas.organization.net/2010/04/myNamespace" />
        <d:Namespace d:Prefix="p2" d:Uri="http://schemas.organization.net/2010/04/MyNamespace2" />
        </d:Namespaces>
        <!-- Parameters of hello web service call:
        @Name should match exactly (case sensitive) hello {…} placeholders in hello @d:BaseUri, @d:UriTemplate, and d:RequestBody, i.e. “name” parameter in above BaseURI.
        @Mode is always "In", compatibility with CSDL
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx
        @d:Nullable indicates whether hello parameter is required.
        @d:Regex - optional, attribute toodescribe hello string, limiting unwanted input at hello entry of hello system
        @d:Description - optional, is used by Service Explorer as help information
        @d:SampleValues - optional, is used by Service Explorer as help information. Multiple Sample values are separated by '|', e.g. "804735132|234534224|23409823234"
        @d:Enum - optional for string type. Contains an enumeration of possible values separated by a '|', e.g. d:enum="english|metric|raw". Will be converted in a dropdown list in hello Service Explorer.
        -->
        <Parameter name="name" Mode="In" Type="String" d:Nullable="false" d:Regex="^[a-zA-Z]*$" d:Description="A name that cannot contain any spaces or non-alpha non-English characters"
        d:Enum="George|John|Thomas|James"
        d:SampleValues="George"/>
        <Parameter Name=" AccountKey" Mode="In" Type="String" d:Nullable="false" />

        <!-- d:ErrorHandling is an optional element. Use it define standardized errors by evaluating hello service response. -->
        <d:ErrorHandling>
        <!-- Any number of d:Condition elements are allowed, they are evaluated in hello order listed.
        @d:Match is an Xpath query on hello service response, it should return true or false where true indicates an error.
        @d:httpStatusCode is hello error code tooreturn if an response matches hello error.
        @d:errorMessage is hello user friendly message tooreturn when an error occurs.
        -->
        <d:Condition d:Match="/Result/ErrorMessage[text()='Invalid token']" d:HttpStatusCode="403" d:ErrorMessage="User cannot connect toohello service." />
        </d:ErrorHandling>
           </FunctionImport>

            <!-- hello EntityContainer defines hello output data schema -->
        </EntityContainer>
        <!-- hello EntityType @d:Map defines hello repeating node (an XPath query) in hello response (output data schema). -->
        <!-- If these nodes are outside a namespace, add hello prefix in hello xpath. -->
        <!--
        @Name - define your user readable name, will become an XML element in hello ATOM feed, so comply with hello XML element naming restrictions (no spaces or other illegal characters).
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx.
        @d:Map uses an Xpath query toopoint at hello location tooextract hello content from your services response.
        hello "." is relative toohello repeating node in hello EntityType @d:Map Xpath expression.
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
> <span data-ttu-id="9565f-190">Daha fazla CSDL Web hizmeti örnekleri hello makalesinde görüntülemek [var olan eşleme örnekleri web hizmeti tooOData CSDLs aracılığıyla](marketplace-publishing-data-service-creation-odata-mapping-examples.md)</span><span class="sxs-lookup"><span data-stu-id="9565f-190">View more CSDL Web Service examples in hello article [Examples of mapping an existing web service tooOData through CSDLs](marketplace-publishing-data-service-creation-odata-mapping-examples.md)</span></span>
> 
> 

### <a name="dataservice-csdl-example"></a><span data-ttu-id="9565f-191">DataService CSDL örneği</span><span class="sxs-lookup"><span data-stu-id="9565f-191">DataService CSDL Example</span></span>
<span data-ttu-id="9565f-192">Örnek aşağıda bir uç nokta iki temel veriler için API API (tablolar yerine görünümleri kullanabilirsiniz) CSDL dayalı gösterildiği gibi bir veritabanı tablosu veya görünümü gösterme tooa hizmet bağlanır.</span><span class="sxs-lookup"><span data-stu-id="9565f-192">Connects tooa service that is exposing a database table or view as an endpoint Below example shows two APIs for Data base based API CSDL (can use views rather than tables).</span></span>

        <?xml version="1.0"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyDataOffer" Alias="MyOffer" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ado/2009/08/edm">
        <!-- EntityContainer groups all hello data service calls together into a single offering. Every web service call has a FunctionImport definition. -->
        <EntityContainer Name="MyOfferContainer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
            Think of hello EntitySet as a Service
        @Name is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition (returned set of table columns). -->
        <EntitySet Name="CompanyInfoEntitySet" EntityType="MyOffer.CompanyInfo" />
        <EntitySet Name="ProductInfoEntitySet" EntityType="MyOffer.ProductInfo" />
        </EntityContainer>
        <!-- EntityType defines result (output); hello table (or view) and columns toobe returned by hello data service.)
            Map is hello schema.tabel or schema.view
            dals.TableName is hello table Name
            Name is hello name identifier for hello EntityType and hello Name of hello service exposed toohello client via hello UI.
            dals:IsExposed determines if hello table schema is exposed (generally true).
            dals:IsView (optional) true if this is based on a view rather than a table
            dals:TableSchema is hello schema name of hello table/view
        -->
        <EntityType
        Map="[dbo].[CompanyInfo]"
        dals:TableName="CompanyInfo"
        Name="CompanyInfo"
        dals:IsExposed="true"
        dals:IsView="false"
        dals:TableSchema="dbo"
        xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <!-- Property defines hello column properties and hello output of hello service.
            dals:ColumnName is hello name of hello column in hello table /view.
            Type is hello emd.SimpleType
            Nullable determines if NULL is a valid output value
            dals.CharMaxLenght is hello maximum length of hello output value
            Name is hello name of hello Property and is exposed toohello client facing UI
            dals:IsReturned is hello Boolean that determines if hello Service exposes this value toohello client.
            IsQueryable is hello Boolean that determines if hello column can be used in a database query
            (For data Services: tooimprove Performance make sure that columns marked ISQueryable=”true” are in an index.)
            dals:OrdinalPosition is hello numerical position x in hello table or hello View, where x is from 1 toohello number of columns in hello table.
            dals:DatabaseDataType is hello data type of hello column in hello database, i.e. SQL data type dals:IsPrimaryKey indicates if hello column is hello Primary key in hello table/view.  (hello columns marked ISPrimaryKey are used in hello Order by clause when returning data.)
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

## <a name="see-also"></a><span data-ttu-id="9565f-193">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9565f-193">See Also</span></span>
* <span data-ttu-id="9565f-194">Öğrenme ve anlama hello belirli düğümler ve bunların parametrelerini ilgileniyorsanız, bu makaleyi okuyun [veri hizmeti OData eşleme düğümleri](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) tanımları ve açıklamalar, örnekler ve kullanım örneği bağlamı.</span><span class="sxs-lookup"><span data-stu-id="9565f-194">If you are interested in learning and understanding hello specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="9565f-195">Örnekler gözden geçirme ilgileniyorsanız, bu makaleyi okuyun [veri hizmeti OData eşleme örnekler](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee örnek kod ve kod sözdizimi ve bağlam anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9565f-195">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee sample code and understand code syntax and context.</span></span>
* <span data-ttu-id="9565f-196">Bu makaleyi okuyun bir veri hizmeti toohello Azure Marketi'nde yayımlama yolu belirlenen tooreturn toohello [veri hizmeti yayımlama Kılavuzu](marketplace-publishing-data-service-creation.md).</span><span class="sxs-lookup"><span data-stu-id="9565f-196">tooreturn toohello prescribed path for publishing a Data Service toohello Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

