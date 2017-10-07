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
# <a name="mapping-an-existing-web-service-tooodata-through-csdl"></a>Var olan bir web hizmeti tooOData CSDL aracılığıyla eşleme
> [!IMPORTANT]
> **Şu anda artık ekleme duyuyoruz herhangi yeni veri hizmeti yayımcılar. Yeni dataservices listesine onaylanmamış.** Bir SaaS iş uygulaması varsa toopublish istediğiniz AppSource hakkında daha fazla bilgi bulabilirsiniz [burada](https://appsource.microsoft.com/partners). Bir Iaas uygulamalar varsa veya Geliştirici hizmeti misiniz Azure Market'te toopublish gibi daha fazla bilgi bulabilirsiniz [burada](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Bu makalede hakkında genel bir fikir veren toouse CSDL toomap var olan bir hizmet tooan OData uyumlu hizmeti. Bunu nasıl toocreate hello eşleme belge (CSDL) hello giriş hello istemci hizmeti çağrısı ve hello aracılığıyla isteğinden Dönüşümleri (veri) geri toohello istemci OData uyumlu akışı aracılığıyla çıktı açıklanmaktadır. Microsoft Azure Marketi'nde Hizmetleri toohello son kullanıcılar hello OData protokolünü kullanarak kullanıma sunar. (Verileri sahiplerinin) içerik sağlayıcıları tarafından sunulan hizmetler, formlar, REST, SOAP, vb. gibi çeşitli sunulur.

## <a name="what-is-a-csdl-and-its-structure"></a>Bir CSDL ve yapısını nedir?
CSDL (kavramsal şema tanım dili) nasıl toodescribe web hizmeti veya veritabanı hizmet ortak XML duyuruları toohello Azure Marketi tanımlayan bir özelliğidir.

Merhaba basit genel bakış **istek akışı:**

  `Client -> Azure Marketplace -> Content Provider’s Web Service (Get, Post, Delete, Put)`

Merhaba **veri akışı** hello olduğu yönü ters:

  `Client <- Azure Marketplace <- Content Provider’s WebService`

**Şekil 1** diyagramları nasıl bir istemci verilerini bir içerik sağlayıcı (hizmetinizi) hello Azure Market giderek elde edebilirsiniz.  Merhaba içerik sağlayıcının hizmetlere ve istemci isteyen hello arasında veri iletmek ve Hello CSDL hello eşleme/dönüştürme bileşen toohandle hello isteği tarafından kullanılır.

*Şekil 1: istemci toocontent sağlayıcısı aracılığıyla Azure Marketi isteyen gelen ayrıntılı akış*

  ![Çizim](media/marketplace-publishing-data-service-creation-odata-mapping/figure-1.png)

Atom, Atom Pub ve hello OData Protokolü hangi hello Azure Marketi uzantıları derleme sırasında arka plan için lütfen gözden geçirin: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)

Bağlantı yukarıdaki alıntı: *"Merhaba açık veri Protokolü (bundan böyle başvurulan tooas OData) hello amacı protokolüdür tooprovide REST tabanlı veri hizmetleri sunulan kaynaklara karşı stili CRUD işlemleri (oluşturma, okuma, güncelleştirme ve silme). "Veri hizmeti" bir uç noktadır koleksiyonlardan bir veya daha fazla"" her ", oluşur sıfır veya daha fazla girişlerini" ile kullanıma sunulan veri olduğu adlı-değer çiftleri belirtilmiş. Toocan isteyen herkes yapı sunucuları, istemcileri veya Araçlar telif hakkı veya kısıtlamaları olmadan böylece OData OASIS (Merhaba terfi yapılandırılmış bilgi standartlar için kuruluş) standartları altında Microsoft tarafından yayımlanan."*

### <a name="three-critical-pieces-that-have-toobe-defined-by-hello-csdl-are"></a>Üç kritik CSDL hello tarafından tanımlanan toobe sahip parça şunlardır:
* Merhaba **endpoint** hello hizmet sağlayıcısı Web adresi (URI) hello hizmeti ile Merhaba
* Merhaba **veri parametreleri** giriş toohello hizmet sağlayıcısı hello tanımları toohello veri türü toohello içerik sağlayıcının hizmeti gönderilen hello parametrelerinin geçirilen.
* **Şema** toohello isteyen hizmeti hello şema hello içerik sağlayıcının hizmeti tarafından teslim edilmesini hello verinin döndürülmesini hello verilerinin kapsayıcı, koleksiyonları/tabloları, değişkenleri/sütunları ve veri türleri dahil olmak üzere.

Diyagram aşağıdaki hello hello akış burada hello istemci hello OData deyimi (çağrı toohello içerik sağlayıcının web hizmeti) toogetting hello sonuçları/verileri geri girer gelen genel bir bakış gösterilir.

  ![Çizim](media/marketplace-publishing-data-service-creation-odata-mapping/figure-2.png)

### <a name="steps"></a>adımlar:
1. İstemci isteği hizmet aramasıyla giriş XML toohello Azure Marketi tanımlanan parametrelere sahip tam gönderir
2. CSDL kullanılan toovalidate hello hizmeti çağrısı ' dir.
   * Merhaba biçimlendirilmiş hizmetini çağırmak toohello içerik sağlayıcıları hizmeti hello Azure Marketi tarafından gönderilir
3. Merhaba Webservice yürütür ve hello eylemin hello Http Fiili preforms (yani GET) hello veriler döndürülür tooAzure burada hello istenen veriler (varsa) Market XML biçiminde toohello istemci çıkarır eşleme tanımlanan hello CSDL hello kullanarak.
4. Merhaba istemci hello veriler (varsa) XML veya JSON biçiminde gönderilir

## <a name="definitions"></a>Tanımlar
### <a name="odata-atom-pub"></a>OData ATOM pub
Her girişin bir sonucu olarak bir satır temsil ettiği bir uzantı toohello ATOM pub ayarlayın. Merhaba içerik hello girişi Gelişmiş toocontain hello değerleri hello satırının – anahtar değer çiftleri olarak parçasıdır. Daha fazla bilgi aşağıda bulunan: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)

### <a name="csdl---conceptual-schema-definition-language"></a>CSDL - kavramsal şema tanım dili
İşlevler (SPROCs) tanımlanmasına olanak sağlar ve bir veritabanı yoluyla kullanıma sunulan varlıklar. Burada bulunan daha fazla bilgi: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)  

> [!TIP]
> Merhaba tıklatın **diğer sürümleri** açılır ve hello makale görmüyorsanız, bir sürümü seçin.
> 
> 

### <a name="edm---entry-data-model"></a>EDM - giriş veri modeli
* Genel Bakış: [http://msdn.microsoft.com/library/vstudio/ee382825 (v=vs.100).aspx][OverviewLink]

[OverviewLink]:http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx
* Önizleme: [http://msdn.microsoft.com/library/aa697428 (v=vs.80).aspx][PreviewLink]

[PreviewLink]:http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx
* Veri türleri: [http://msdn.microsoft.com/library/bb399548 (v=VS.100).aspx][DataTypesLink]

[DataTypesLink]:http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx

Burada hello istemci hello OData deyimi (çağrı toohello içerik sağlayıcının web hizmeti) toogetting hello sonuçları/verileri geri girer gelen sol tooRight akış hello ayrıntılı Hello aşağıdakileri gösterir:

  ![Çizim](media/marketplace-publishing-data-service-creation-odata-mapping/figure-3.png)

## <a name="csdl-basics"></a>CSDL temelleri
CSDL (kavramsal şema tanım dili) nasıl toodescribe web hizmeti veya veritabanı hizmet ortak XML duyuruları toohello Azure Marketi tanımlayan bir özelliğidir. CSDL açıklar hello kritik parça **hello veri kaynağı toohello Azure Marketi gelen verilerin hello geçirme mümkün kılar.** Merhaba ana parçalar aşağıda açıklanmıştır:

* Tüm genel kullanıma açık işlevleri (Functionımport düğümü) açıklayan bilgileri arabirimi
* Veri türü bilgileri tüm ileti requests(input) ve ileti responses(outputs) (EntitySet/EntityContainer/EntityType düğümler)
* Merhaba Aktarım Protokolü toobe hakkında bilgi bağlama (üstbilgi düğümü) kullanılır
* Hizmet (tabanURI özniteliği) hello yerini adres bilgilerini belirtilen

Buna koysalar hello CSDL hello hizmet istek sahibi ve hello hizmet sağlayıcısı arasında bir platform ve dilden bağımsız sözleşme temsil eder. Bir istemci, Hello CSDL'ı kullanarak bir web hizmeti/veritabanı hizmetini bulun ve herhangi bir genel kullanıma açık işlevlerini çağırma.

### <a name="relating-a-csdl-tooa-database-or-a-collection"></a>CSDL tooa veritabanı veya bir koleksiyon ilgili
**Merhaba CSDL belirtimi**

CSDL açıklayan bir web hizmeti için XML dilbilgisi ' dir. Merhaba belirtimi kendisini 4 ana elemanlara bölünür: EntitySet, Functionımport; Ad alanı ve EntityType.

Bu soyutlama daha kolay toounderstand CSDL tooa tablosu arasında ilişki toomake olanak sağlar.

Unutmayın;

  CSDL temsil eden bir platform ve dilden bağımsız sözleşme hello arasında **hizmet istek sahibi** ve hello **hizmet sağlayıcısı**. CSDL, kullanarak bir **istemci** bulabilir bir **web hizmeti/veritabanı hizmeti** ve kendi genel kullanıma açık hiçbirini çağırma **işlevleri.**

Bir veri hizmeti Merhaba bir CSDL dört bölümden, veritabanı, tablo, sütun ve deposu yordamı bakımından değerlendirilebilir.

Bu gibi bir veri hizmeti ile ilgili:

* EntityContainer ~ = veritabanı
* EntitySet ~ = tablosu
* EntityType ~ sütunları =
* Functionımport ~ saklı yordam =

**İzin verilen HTTP fiilleri**

* GET-(bir koleksiyon döndürür) hello DB'den değerler verir
* POST – toopass veri tooand isteğe bağlı dönüş değerleri (Merhaba koleksiyonundaki dönüş kimliği/URI'si yeni bir giriş oluşturun) hello DB'den kullanılan
* SİLME – (koleksiyonu siler) hello DB verilerden siler
* PUT – bir Veritabanına veri güncelleştirme (bir koleksiyon değiştirin veya bir tane oluşturun)

## <a name="metadatamapping-document"></a>Meta veri/eşleme belge
Böylece hello Azure Marketi sistem tarafından bir OData web hizmeti olarak verilebilen bir içerik sağlayıcının varolan web hizmetleri kullanılan toomap Hello meta veri/eşleme belgedir. Implements birkaç uzantıları tooCSDL tooaccommodate hello ihtiyaçlarını REST Azure Market üzerinden kullanıma sunulan web hizmetleri tabanlı ve CSDL üzerinde temel alır. Merhaba uzantıları hello bulundu [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) ad alanı.

Merhaba CSDL örneği izler: (Kopyala ve Yapıştır hello örnek CSDL bir XML Düzenleyicisi içine aşağıda ve hizmetinizi toomatch değiştirin.  CSDL eşleme DataService sekmesi altında hizmetinizi hello oluştururken yapıştırın [Azure Marketi'nde yayımlama portalında](https://publish.windowsazure.com)).

**Koşulları:** Relating hello CSDL koşulları toohello [yayımlama portalında](https://publish.windowsazure.com) UI (PPUI) koşulları.

* Merhaba PPUI "Title" tooMyWebOffer ilişkili sunma
* Merhaba PPUI Şirketim ilişkili çok**yayımcı görünen adı** hello içinde [Microsoft Developer Center'da](http://dev.windows.com/registration?accountprogram=azure) kullanıcı Arabirimi
* API'nizi tooa Web veya veri hizmeti (Merhaba PPUI planında) ilişkilendirir

**Hiyerarşi:** tanesine olan tekliflerini sahibinin şirket (içerik sağlayıcısı), yani service(s), bir API ile hangi hizalamak.

### <a name="webservice-csdl-example"></a>Web hizmeti CSDL örneği
Bir web uygulaması uç noktası (örneğin, C# uygulaması) gösterme tooa hizmet bağlanır

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
> Daha fazla CSDL Web hizmeti örnekleri hello makalesinde görüntülemek [var olan eşleme örnekleri web hizmeti tooOData CSDLs aracılığıyla](marketplace-publishing-data-service-creation-odata-mapping-examples.md)
> 
> 

### <a name="dataservice-csdl-example"></a>DataService CSDL örneği
Örnek aşağıda bir uç nokta iki temel veriler için API API (tablolar yerine görünümleri kullanabilirsiniz) CSDL dayalı gösterildiği gibi bir veritabanı tablosu veya görünümü gösterme tooa hizmet bağlanır.

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

## <a name="see-also"></a>Ayrıca Bkz.
* Öğrenme ve anlama hello belirli düğümler ve bunların parametrelerini ilgileniyorsanız, bu makaleyi okuyun [veri hizmeti OData eşleme düğümleri](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) tanımları ve açıklamalar, örnekler ve kullanım örneği bağlamı.
* Örnekler gözden geçirme ilgileniyorsanız, bu makaleyi okuyun [veri hizmeti OData eşleme örnekler](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee örnek kod ve kod sözdizimi ve bağlam anladığınızdan emin olun.
* Bu makaleyi okuyun bir veri hizmeti toohello Azure Marketi'nde yayımlama yolu belirlenen tooreturn toohello [veri hizmeti yayımlama Kılavuzu](marketplace-publishing-data-service-creation.md).

