---
title: "aaaGet başlatılan REST kullanarak isteğe bağlı içerik göndermeye | Microsoft Docs"
description: "Bu öğretici, REST API kullanarak Azure Media Services ile bir üzerinde isteğe bağlı içerik teslim uygulaması gerçekleştirilmesinin hello adım adım anlatılmaktadır."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 88194b59-e479-43ac-b179-af4f295e3780
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: f270ed59e9ae9745e8403ec6e19d5c3533fc82b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-rest"></a>REST kullanarak isteğe bağlı içerik göndermeye başlama
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

Bu hızlı başlangıç Azure Media Services (AMS) REST API'lerini kullanarak bir isteğe bağlı video (VoD) içerik teslim uygulaması gerçekleştirilmesinin hello adımlarda size yol gösterir.

Başlangıç Öğreticisi hello temel Media Services iş akışı, hello en genel programlama nesnelerini ve Media Services geliştirmek için gereken görevleri tanıtır. Başlangıç Öğreticisi Hello tamamlandığında mümkün toostream olması veya aşamalı olarak örnek bir medya dosyasını karşıya kodlanmış ve yüklenen indirebilirsiniz.

Merhaba aşağıdaki görüntüde bazılarını hello en yaygın olarak kullanılan nesneler hello Media Services OData modelde VoD uygulamaları geliştirirken gösterir.

Merhaba görüntü tooview boyutu tam'ı tıklatın.  

<a href="./media/media-services-rest-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-rest-get-started/media-services-overview-object-model-small.png"></a> 

## <a name="prerequisites"></a>Ön koşullar
Merhaba aşağıdaki önkoşullar REST API'leri ile Media Services ile geliştirme gerekli toostart bulunmaktadır.

* Bir Azure hesabı. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).
* Bir Media Services hesabı. bir Media Services hesabı toocreate bkz [nasıl tooCreate Media Services hesabı](media-services-portal-create-account.md).
* Nasıl anlayış toodevelop Media Services REST API ile. Daha fazla bilgi için bkz: [Media Services REST API genel bakış](media-services-rest-how-to-use.md).
* HTTP istekleri ve yanıtları göndermek tercih ettiğiniz bir uygulama. Bu öğretici kullanır [Fiddler](http://www.telerik.com/download/fiddler).

Bu hızlı başlangıcı görevleri aşağıdaki hello gösterilmektedir.

1. Akış uç noktası (hello Azure portal kullanarak) başlatın.
2. REST API'si ile toohello Media Services hesabına bağlanın.
3. Yeni bir varlık oluşturun ve REST API ile video dosyası yükleyin.
4. Merhaba kaynak dosyayı Uyarlamalı bit hızlı MP4 dosyaları REST API ile kodlayın.
5. Merhaba varlığı yayımlayın ve get akış ve aşamalı indirme URL'lerini REST API ile.
6. İçeriğinizi oynatın.

>[!NOTE]
>Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için). Merhaba kullanması gereken her zaman kullanıyorsanız, aynı ilke kimliği hello aynı gün / erişim izinlerini, örneğin, uzun bir süre (karşıya yükleme olmayan ilkeleri) yerinde hedeflenen tooremain olan bulucular ilkeleri. Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.

Bu konuda kullanılan AMS REST varlıklar hakkında daha fazla ayrıntı için bkz: [Azure Media Services REST API Başvurusu](/rest/api/media/services/azure-media-services-rest-api-reference). Ayrıca bkz [Azure Media Services kavramları](media-services-concepts.md).

>[!NOTE]
>Varlıklar Media Services erişirken, HTTP istekleri özel üstbilgi alanlarını ve değerlerini ayarlamanız gerekir. Daha fazla bilgi için bkz: [Media Services REST API geliştirme için Kurulum](media-services-rest-how-to-use.md).

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a>Akış uç noktaları Hello Azure portal kullanarak Başlat

Merhaba en sık karşılaşılan senaryolardan biri, video bit hızı Uyarlamalı akış iletmektir Azure Media Services ile çalışırken. Media Services, bit hızı Uyarlamalı MP4 kodlanmış içeriğinizi Media Services (MPEG DASH, HLS, kesintisiz akış) tam zamanında tarafından önceden paketlenmiş toostore kalmadan desteklenen akış biçimlerinde toodeliver sağlayan dinamik paketleme sağlar Bu akış biçimlerine her da sürümleri.

>[!NOTE]
>AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu. İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu.

toostart akış uç Merhaba, aşağıdaki hello:

1. Merhaba oturum açma [Azure portal](https://portal.azure.com/).
2. Hello Ayarları penceresinde, akış uç noktaları'ı tıklatın.
3. Merhaba varsayılan akış uç noktası'ı tıklatın.

    Merhaba varsayılan akış uç noktası AYRINTILAR penceresi görüntülenir.

4. Merhaba başlangıç simgesine tıklayın.
5. Merhaba Kaydet düğmesine toosave değişikliklerinizi'ı tıklatın.

## <a id="connect"></a>REST API'si ile toohello Media Services hesabına bağlanma

Nasıl tooconnect toohello AMS API, bkz. bilgi [Azure AD kimlik doğrulaması ile erişim hello Azure Media Services API](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Başarıyla toohttps://media.windows.net bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız. Sonraki çağrılar toohello yapmanız gereken yeni bir URI.

Örneğin, tooconnect çalışıyorsanız, sonra hello aşağıdaki var:

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/

Sonraki API çağrıları toohttps://wamsbayclus001rest-hs.cloudapp.net/api/ göndermeniz gerekir.

## <a id="upload"></a>Yeni bir varlık oluşturun ve REST API ile video dosyası yükleyin

Media Services’de dijital dosyalar bir varlığa yüklenir. Merhaba **varlık** varlık içerebilir video, ses, görüntüler, küçük resim koleksiyonları, metin parçaları ve kapalı açıklamalı alt yazı dosyaları (ve bu dosyalar hakkında hello meta veriler.)  Hello varlığa Hello dosyalar yüklendiğinde, içeriğiniz sonraki işleme ve akışla için hello bulutta güvenli bir şekilde depolanır.

Bir varlık oluşturma varlık oluşturma seçeneklerden olduğunda tooprovide sahip hello değerlerinden biri. Merhaba **seçenekleri** bir varlığı ile oluşturulan hello şifreleme seçenekleri açıklayan bir numaralandırma değeri bir özelliktir. Geçerli bir değer değil Bu listeden bir değerler birleşimi aşağıdaki hello listeden hello değerlerinden biri:

* **Hiçbiri** = **0** -şifreleme kullanılmaz. Bu seçenek kullanıldığında, içeriğinizin aktarım veya deposunda kalan korunmaz.
    Aşamalı indirme kullanarak toodeliver bir MP4 planlıyorsanız, bu seçeneği kullanın.
* **StorageEncrypted** = **1** - Temizle içeriğinizi yerel olarak AES 256 bit şifreleme kullanarak şifreler ve tooAzure depolanır depolama şifrelenen yükler. Depolama şifrelemesi ile korunan varlıklar otomatik olarak şifrelenmemiş ve bir şifrelenmiş dosya sistemi önceki tooencoding ve yeni bir çıkış varlığı olarak geri isteğe bağlı olarak yeniden şifrelenmiş önceki toouploading yerleştirilir. Depolama şifrelemesinin birincil kullanım durumu hello yüksek kaliteli giriş medya dosyalarınızı REST güçlü şifrelemeyle diskte toosecure istediğiniz durumdur.
* **CommonEncryptionProtected** = **2** -zaten şifrelenmiş ve ortak şifreleme veya PlayReady DRM (örneğin, ile korunan kesintisiz akış PlayReady DRM) ile korunan içerik yüklüyorsanız bu seçeneği kullanın.
* **EnvelopeEncryptionProtected** = **4** – AES ile şifrelenmiş HLS yüklüyorsanız bu seçeneği kullanın. Merhaba dosyaları kodlanmış ve Transform Manager tarafından şifrelenmiş gerekir.

### <a name="create-an-asset"></a>Bir varlık oluşturun
Bir varlık, birden çok türleri veya Media Services, video, ses, görüntüler, küçük resim koleksiyonları, metin parçaları ve kapalı açıklamalı alt yazı dosyaları dahil olmak üzere nesne kümeleri için bir kapsayıcıdır. REST API bir varlık oluşturma, posta gönderme gerektirir hello tooMedia Hizmetleri isteyin ve hello istek gövdesinde Varlığınızı ilgili herhangi bir özellik bilgi yerleştirme.

örnekte gösterildiği nasıl aşağıdaki hello toocreate bir varlık.

**HTTP isteği**

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 45

    {"Name":"BigBuckBunny.mp4", "Options":"0"}


**HTTP yanıtı**

Başarılı olursa, hello aşağıdaki verilir:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 452
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    request-id: e98be122-ae09-473a-8072-0ccd234a0657
    x-ms-request-id: e98be122-ae09-473a-8072-0ccd234a0657
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny2.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a>Bir AssetFile oluşturma
Merhaba [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) varlığı temsil eden bir blob kapsayıcısında depolanır ses veya video dosyası. Bir varlık dosyası her zaman bir varlıkla ilişkilidir ve bir varlığı bir veya daha çok AssetFiles içerebilir. bir varlık dosyası nesne bir blob kapsayıcısında dijital bir dosyayla ilişkili değilse hello Media Services Kodlayıcısı görev başarısız olur.

Bir blob kapsayıcıya bir dijital medyayı dosyanızı karşıya sonra hello kullanın **birleştirme** medya dosyanızın (Merhaba konunun ilerleyen bölümlerinde gösterildiği gibi) hakkında bilgi içeren HTTP isteği tooupdate hello AssetFile.

**HTTP isteği**

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


**HTTP yanıtı**

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 535
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5')
    Server: Microsoft-IIS/8.5
    request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    x-ms-request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 00:34:07 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Files/@Element",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "Name":"BigBuckBunny.mp4",
       "ContentFileSize":"0",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "EncryptionVersion":null,
       "EncryptionScheme":null,
       "IsEncrypted":false,
       "EncryptionKeyId":null,
       "InitializationVector":null,
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }


### <a name="creating-hello-accesspolicy-with-write-permission"></a>Yazma izni olan Hello AccessPolicy oluşturma
Blob depolama alanına herhangi bir dosya karşıya yüklemeden önce hello erişim ilkesi hakları tooan varlık yazmak için ayarlayın. bir HTTP isteği toohello AccessPolicies varlık sonrası toodo ayarlayın. Oluşturulduktan sonra bir dakika Cinsiden Süre değer tanımlama veya yanıt olarak bir 500 İç sunucu hata iletisi alırsınız. AccessPolicies hakkında daha fazla bilgi için bkz: [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).

örnekte gösterildiği nasıl aşağıdaki hello toocreate bir AccessPolicy:

**HTTP isteği**

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 74

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"}

**HTTP yanıtı**

Başarılı olursa, yanıt aşağıdaki hello verilir:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 312
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae')
    Server: Microsoft-IIS/8.5
    request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    x-ms-request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:18:06 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#AccessPolicies/@Element",
       "Id":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "Created":"2015-01-18T22:18:06.6370575Z",
       "LastModified":"2015-01-18T22:18:06.6370575Z",
       "Name":"NewUploadPolicy",
       "DurationInMinutes":440.0,
       "Permissions":2
    }

### <a name="get-hello-upload-url"></a>Merhaba karşıya yükleme URL'si Al

tooreceive gerçek karşıya yükleme URL'si Merhaba, SAS Bulucu oluşturun. Bulucular bir varlık tooaccess dosyalarında istediğiniz istemciler için hello başlangıç saati ve bağlantı uç noktasının türünü tanımlayın. İstekleri ve gereksinimlerini verilen AccessPolicy ve varlık çifti toohandle farklı bir istemci için birden çok Bulucu varlık oluşturabilirsiniz. Her bu Bulucuyu hello StartTime değerinin yanı sıra hello AccessPolicy toodetermine hello süreyi bir URL kullanılabilir hello Dakika Cinsiden Süre değerini kullanır. Daha fazla bilgi için bkz: [Bulucu](https://docs.microsoft.com/rest/api/media/operations/locator).

Bir SAS URL'si biçimi aşağıdaki hello sahiptir:

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

Bazı dikkate alınması gereken noktalar vardır:

* Aynı anda belirli bir varlıkla ilişkilendirilen beşten fazla benzersiz Bulucular sahip olamaz. Daha fazla bilgi için Bulucu bakın.
* Dosyalarınızı hemen tooupload gerekiyorsa, StartTime değeri toofive dakika hello geçerli saati önce ayarlamanız gerekir. Bu; çünkü istemci makine ve Media Services arasında eğme saat olabilir. Ayrıca, StartTime değeriniz tarih saat biçiminde aşağıdaki hello olmalıdır: YYYY-MM-: ssZ (örneğin, "2014-05-23T17:53:50Z").    
* 30-40 saniyenin olabilir bir Bulucu kullanılabilir olmasından toowhen oluşturulduktan sonra gecikme. Bu sorun tooboth SAS URL'si ve Kaynak Konum Belirleyicisi geçerlidir.

SAS hakkında daha fazla bilgi için bkz: bulucular [bu](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blogu.

Aşağıdaki örneğine hello nasıl toocreate bir SAS URL'si tarafından tanımlanan Bulucu, hello hello istek gövdesindeki (bir SAS Bulucu için "1") ve bir isteğe bağlı kaynak Bulucu için "2" Type özelliği gösterir. Merhaba **yolu** döndürülen özelliği içeren hello URL dosyanızı tooupload kullanmanız gerekir.

**HTTP isteği**

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 178

    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }


**HTTP yanıtı**

Başarılı olursa, yanıt aşağıdaki hello verilir:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 949
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54')
    Server: Microsoft-IIS/8.5
    request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    x-ms-request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 03:01:29 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Locators/@Element",
       "Id":"nb:lid:UUID:af57bdd8-6751-4e84-b403-f3c140444b54",
       "ExpirationDateTime":"2015-02-19T00:05:53",
       "Type":1,
       "Path":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "BaseUri":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247",
       "ContentAccessComponent":"?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Name":null
    }

### <a name="upload-a-file-into-a-blob-storage-container"></a>Bir blob depolama kapsayıcısının içine bir dosyayı karşıya yüklemek
Merhaba AccessPolicy ve Bulucu kümesi oluşturduktan sonra hello gerçek hello Azure Storage REST API'leri kullanılarak karşıya yüklenen tooan Azure blob depolama kapsayıcısını dosyasıdır. Blok blobları hello dosyalarını yüklemeniz gerekir. Sayfa bloblarını Azure Media Services tarafından desteklenmiyor.  

> [!NOTE]
> Merhaba dosya adı eklemelisiniz hello dosya için tooupload toohello Bulucu istediğiniz **yolu** hello önceki bölümde alınan değer. Örneğin, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4? . . .
>
>

Azure depolama BLOB'ları ile çalışma hakkında daha fazla bilgi için bkz: [Blob hizmeti REST API'si](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).

### <a name="update-hello-assetfile"></a>Merhaba AssetFile güncelleştir
Dosyanızı yüklediğiniz, hello FileAsset boyut (ve diğer) bilgi güncelleştirin. Örneğin:

    MERGE https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


**HTTP yanıtı**

Başarılı olursa, hello aşağıdaki verilir:

    HTTP/1.1 204 No Content
    ...

## <a name="delete-hello-locator-and-accesspolicy"></a>Merhaba Bulucu ve AccessPolicy Sil
**HTTP isteği**

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


**HTTP yanıtı**

Başarılı olursa, hello aşağıdaki verilir:

    HTTP/1.1 204 No Content
    ...

**HTTP isteği**

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

**HTTP yanıtı**

Başarılı olursa, hello aşağıdaki verilir:

    HTTP/1.1 204 No Content
    ...

## <a id="encode"></a>Merhaba kaynak dosya bit hızı Uyarlamalı MP4 dosyaları kümesine kodlayın

Önce varlıklar Media Services, medya içine olarak kodlanmış alma, filigran, biçimini ve benzeri, sonra tooclients teslim edilir. Bu etkinlikler zamanlanmış ve birden fazla arka plan rol örnekleri tooensure yüksek performans ve kullanılabilirlik karşı çalıştırın. Bu etkinliklere işler adı verilir ve her bir iş hello varlık dosyası üzerinde asıl işi hello atomik görevlerin oluşur (daha fazla bilgi için bkz: [iş](/rest/api/media/services/job), [görev](/rest/api/media/services/task) açıklamaları).

Ne zaman daha önce belirtildiği gibi Azure Media Services bir hello en yaygın senaryolar ile çalışma bit hızı Uyarlamalı tooyour istemcileri akış iletmektir. Media Services dinamik olarak paketini bit hızı Uyarlamalı MP4 dosyaları kümesini biçimleri aşağıdaki hello birine: HTTP canlı akışı (HLS), kesintisiz akış, MPEG DASH.

bölümden hello nasıl toocreate bir kodlama içeren bir işi görev gösterir. Merhaba görev tootranscode hello Ara dosyayı Uyarlamalı bit hızlı MP4s kullanarak bir kümesini **Medya Kodlayıcısı standart**. Merhaba bölümü de nasıl toomonitor hello işleme ilerleyişini görüntüler. Merhaba iş tamamlandıktan sonra gerekli tooget erişim tooyour varlıklar mümkün toocreate bulucular olacaktır.

### <a name="get-a-media-processor"></a>Medya işlemcisi Al
Media Services'de medya işlemcisi kodlama, biçimini dönüştürme, şifreleme veya şifresi çözme medya içeriği gibi ek olarak, belirli işleme görevi işleyen bir bileşenidir. Bu öğreticide gösterilen görev kodlama hello, biz toouse hello Medya Kodlayıcısı standart adımıdır.

Aşağıdaki kod istekleri hello Kodlayıcı'nın kimliği hello.

**HTTP isteği**

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


**HTTP yanıtı**

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 273
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    x-ms-request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 07:54:09 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "Description":"Media Encoder Standard",
             "Name":"Media Encoder Standard",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

### <a name="create-a-job"></a>Bir iş oluşturma
Her iş sahip olabilir veya tooaccomplish, işleme hello türüne bağlı olarak daha fazla görev istiyor. Merhaba REST API, işler ve bunların ilgili görevleri aşağıdaki iki yöntemden biriyle oluşturabilirsiniz: görevler, satır içi olarak tanımlanan OData toplu işlemin veya iş varlıkları hello görevleri gezinti özelliği üzerinden olabilir. Merhaba Media Services SDK'sı toplu işleme kullanır. Ancak, bu konudaki hello kod örnekleri hello okunabilir olması için satır içi olarak tanımlanan görevlerdir. Toplu işleme hakkında daha fazla bilgi için bkz: [açık veri Protokolü (OData) toplu işleme](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).

Aşağıdaki örneğine hello nasıl toocreate ve sonrası bir görev bir işle tooencode bir video belirli çözümleme ve kalite ayarlama gösterir. bir belge bölümü aşağıdaki hello tüm hello hello listesini içeren [görev hazır](http://msdn.microsoft.com/library/mt269960) hello Medya Kodlayıcısı standart işlemcisi tarafından desteklenir.  

**HTTP isteği**

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: application/json
    Accept: application/json;odata=verbose
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 482

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"Adaptive Streaming",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset>
                <outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          }
       ]
    }

**HTTP yanıtı**

Başarılı olursa, yanıt aşağıdaki hello verilir:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1215
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')
    Server: Microsoft-IIS/8.5
    request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    x-ms-request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:04:35 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Job"
          },
          "Tasks":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Tasks"
             }
          },
          "OutputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets"
             }
          },
          "InputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')/InputMediaAssets"
             }
          },
          "Id":"nb:jid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "Name":"NewTestJob",
          "Created":"2015-01-19T08:04:34.3287057Z",
          "LastModified":"2015-01-19T08:04:34.3287057Z",
          "EndTime":null,
          "Priority":0,
          "RunningDuration":0,
          "StartTime":null,
          "State":0,
          "TemplateId":null,
          "JobNotificationSubscriptions":{  
             "__metadata":{  
                "type":"Collection(Microsoft.Cloud.Media.Vod.Rest.Data.Models.JobNotificationSubscription)"
             },
             "results":[  

             ]
          }
       }
    }


Tüm iş isteği birkaç önemli nokta toonote vardır:

* TaskBody özellikleri değişmez değer XML toodefine hello sayısı giriş ya da görev hello tarafından kullanılan çıkış varlıklar kullanmanız gerekir. Merhaba görev konu hello XML Merhaba XML şema tanımı içerir.
* Her iç Hello TaskBody tanımı, değer <inputAsset> ve <outputAsset> JobInputAsset(value) veya JobOutputAsset(value) ayarlanması gerekir.
* Bir görev, birden fazla çıkış varlığına sahip olabilir. Bir JobOutputAsset(x) yalnızca bir kez bir görevin bir İşte bir çıkış olarak kullanılabilir.
* Bir görev bir giriş varlık JobInputAsset veya JobOutputAsset belirtebilirsiniz.
* Görevler bir döngü oluşturmuyor gerekir.
* tooJobInputAsset veya JobOutputAsset geçirmek hello değer parametresi için bir varlık hello dizin değeri temsil eder. Merhaba gerçek bir varlıklar hello iş varlık tanımı hello InputMediaAssets ve OutputMediaAssets Gezinti özellikleri tanımlanır.

> [!NOTE]
> Media Services üzerinde OData v3 oluşturulduğundan, tek tek varlıkları InputMediaAssets hello ve OutputMediaAssets gezinti özelliği koleksiyonlar aracılığıyla başvurulan bir "__metadata: URI" ad-değer çifti.
>
>

* InputMediaAssets tooone ya da daha fazla varlıklar Media Services ile oluşturduğunuz eşler. OutputMediaAssets hello sistem tarafından oluşturulur. Var olan bir varlık başvuru değil.
* OutputMediaAssets hello assetName özniteliği kullanılarak adlandırılabilir. Bu öznitelik yok sonra hello hello OutputMediaAsset adıdır hello ne olursa olsun hello iç metin değeri <outputAsset> öğesidir hello iş adı değeri veya hello iş kimliği değeri (durumda hello Name özelliği tanımlanmadı burada hello) soneki. AssetName için bir değer ayarlarsanız, örneğin, çok "Örnek" sonra hello OutputMediaAsset özelliğinin ayarlanması adı çok "Sample". AssetName için bir değer ayarlı değil, ancak hello iş adı ayarlama ancak, çok "NewJob" sonra hello OutputMediaAsset adı "JobOutputAsset (değer) _NewJob" olacaktır.

    Aşağıdaki örnek hello nasıl tooset hello assetName özniteliği gösterir:

        "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"
* tooenable görev zincirleme:

  * Bir işi en az iki görev olmalıdır
  * Merhaba işteki başka bir görev çıktısını girişi olan en az bir görev olması gerekir.

Daha fazla bilgi için [hello Media Services REST API ile bir kodlama işi oluşturma](media-services-rest-encode-asset.md).

### <a name="monitor-processing-progress"></a>Devam eden işlem İzleyicisi
Hello aşağıdaki örnekte gösterildiği gibi hello durum özelliğini kullanarak hello iş durumu alabilirsiniz.

**HTTP isteği**

    GET https://wamsbayclus001rest-hs.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-2233-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908022&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=RYXOraO6Z%2f7l9whWZQN%2bypeijgHwIk8XyikA01Kx1%2bk%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 0


**HTTP yanıtı**

Başarılı olursa, yanıt aşağıdaki hello verilir:

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 17
    Content-Type: application/json;odata=verbose;charset=utf-8
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 01324d81-18e2-4493-a3e5-c6186209f0c8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Sun, 13 May 2012 05:16:53 GMT

    {"d":{"State":2}}


### <a name="cancel-a-job"></a>Bir işi iptal etme
Media Services CancelJob işlevi hello çalışan iş toocancel sağlar. Bu çağrı denerseniz toocancel bir iş durumu iptal edildiğinde, iptal etme, hata 400 hata kodunu döndürür veya tamamlanmış.

örnekte gösterildiği nasıl aşağıdaki hello toocall CancelJob.

**HTTP isteği**

    GET https://wamsbayclus001rest-hs.net/API/CancelJob?jobid='nb%3ajid%3aUUID%3a71d2dd33-efdf-ec43-8ea1-136a110bd42c' HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.2
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908753&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kolAgnFfbQIeRv4lWxKSFa4USyjWXRm15Kd%2bNd5g8eA%3d
    Host: wamsbayclus001rest-hs.net


Başarılı olursa, 204 yanıt kodu ile ileti gövdesi yok döndürülür.

> [!NOTE]
> URL kodlama hello iş kimliği gerekir (normalde nb:jid:UUID: somevalue) içinde bir parametre tooCancelJob geçirilirken.
>
>

### <a name="get-hello-output-asset"></a>Merhaba çıkış varlığı edinme
Merhaba aşağıdaki kod toorequest hello varlık kimliği nasıl çıktısını gösterir

**HTTP isteği**

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets() HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


**HTTP yanıtı**

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 445
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    x-ms-request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:28:13 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets",
       "value":[  
          {  
             "Id":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "State":0,
             "Created":"2015-01-19T07:52:15.603",
             "LastModified":"2015-01-19T07:52:15.603",
             "AlternateId":null,
             "Name":"Multibitrate MP4s",
             "Options":0,
             "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "StorageAccountName":"storagetestaccount001"
          }
       ]
    }



## <a id="publish_get_urls"></a>Merhaba varlığı yayımlayın ve get akış ve aşamalı indirme URL'lerini REST API'si

toostream veya indirme bir varlık, ilk çok "bir Bulucu oluşturarak yayımlamadan". Bulucular hello varlıkta bulunan erişim toofiles sağlar. Media Services iki tür Bulucuyu destekler: OnDemandOrigin bulucuları, kullanılan toostream medya (örneğin, MPEG DASH, HLS veya kesintisiz akış) ve erişim imzası (SAS) bulucular kullanılan toodownload medya dosyaları. SAS hakkında daha fazla bilgi için bkz: bulucular [bu](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blogu.

Merhaba bulucuları oluşturduktan sonra kullanılan toostream veya dosyalarınızı karşıdan hello URL'leri oluşturabilirsiniz.

>[!NOTE]
>AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu. İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu.

Bir akış URL'si kesintisiz akış biçimini izleyen hello sahiptir:

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

HLS akış URL'sini biçimini izleyen hello sahiptir:

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

MPEG DASH bir akış URL'si biçimi aşağıdaki hello sahiptir:

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


Bir SAS kullanılan URL toodownload dosyaları biçimini izleyen hello sahiptir:

    {blob container name}/{asset name}/{file name}/{SAS signature}

Bu bölümde, nasıl tooperform hello aşağıdaki gerekli çok "varlıklarınızı yayımlamak" görevler gösterir.  

* Okuma izni olan Hello AccessPolicy oluşturma
* İçerik indirme için bir SAS URL'si oluşturma
* İçerik akışı için bir kaynak URL'sini oluşturma

### <a name="creating-hello-accesspolicy-with-read-permission"></a>Okuma izni olan Hello AccessPolicy oluşturma
İndirme veya hiçbir medya içeriği akış önce ilk olarak okuma izinlerine sahip bir AccessPolicy tanımlamak ve hello türünü belirten hello uygun Bulucu varlık oluşturma teslim mekanizması istemcileriniz için tooenable istiyor. Kullanılabilir hello özellikleri hakkında daha fazla bilgi için bkz: [AccessPolicy varlık özellikleri](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).

Aşağıdaki örnek hello nasıl toospecify hello AccessPolicy belirli bir varlık için Okuma izinleri gösterir.

    POST https://wamsbayclus001rest-hs.net/API/AccessPolicies HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 74
    Expect: 100-continue

    {"Name": "DownloadPolicy", "DurationInMinutes" : "300", "Permissions" : 1}

Başarılı olursa, oluşturduğunuz hello AccessPolicy varlık açıklayan 201 başarı kodu döndürülür. Ardından hello AccessPolicy kimliği hello (örneğin, bir çıkış varlığı) toodeliver toocreate hello Bulucu varlık istediğiniz hello dosyasını içeren hello varlık varlık kimliği ile birlikte kullanabilirsiniz.

> [!NOTE]
> Bu temel iş akışı olan hello (Bu konuda daha önce açıklanan) bir varlık alma, bir dosyayı karşıya yüklemeyi aynıdır. Ayrıca, sizin (veya istemcileriniz) tooaccess ihtiyacınız varsa dosyaları, dosyalarınızı hemen yükleme gibi, StartTime değeri toofive dakika önce hello geçerli saati ayarlayın. Bu eylem gereklidir çünkü hello istemci ve Media Services arasında eğme saat olabilir. Merhaba StartTime değeri, DateTime biçimi aşağıdaki hello olmalıdır: YYYY-MM-: ssZ (örneğin, "2014-05-23T17:53:50Z").
>
>

### <a name="creating-a-sas-url-for-downloading-content"></a>İçerik indirme için bir SAS URL'si oluşturma
koddan hello nasıl tooget kullanılan toodownload bir medya dosyasını olabilir bir URL oluşturulduğunu ve daha önce karşıya gösterir. Merhaba AccessPolicy izinler kümesi okuma ve tooa SAS indirme URL'si hello Bulucu yol gösteriyor.

    POST https://wamsbayclus001rest-hs.net/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-b1ae-2233-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c", "StartTime" : "2014-05-17T16:45:53", "Type":1}

Başarılı olursa, yanıt aşağıdaki hello verilir:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1150
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 8cfd8556-3064-416a-97f2-67d9e35f0911
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:32 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Asset"
             }
          },
          "Id":"nb:lid:UUID:8e5a821d-2194-4d00-8884-adf979856874",
          "ExpirationDateTime":"\/Date(1337049393000)\/",
          "Type":1,
          "Path":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c?st=2012-05-14T21%3A36%3A33Z&se=2012-05-15T02%3A36%3A33Z&sr=c&si=8e5a821d-2194-4d00-8884-adf979856874&sig=y75dViDpC5V8WutrXM%2B%2FGpR3uOtqmlISiNlHU1YUBOg%3D",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "StartTime":"\/Date(1337031393000)\/"
       }
    }


döndürülen hello **yolu** özelliği hello SAS URL içerir.

> [!NOTE]
> Şifrelenmiş depolama içeriği yüklerseniz, el ile işlemeden önce şifresini veya gerekir depolama şifre çözme MediaProcessor işleme görev toooutput içinde hello Temizle tooan OutputAsset dosyalarında işlenir ve bu varlığından karşıdan hello kullanın. İşlem hakkında daha fazla bilgi için bkz: hello Media Services REST API ile bir kodlama işi oluşturma. Ayrıca, oluşturulduktan sonra SAS URL Bulucular güncelleştirilemiyor. Örneğin, yeniden kullanamazsınız güncelleştirilmiş StartTime değerle aynı Bulucu hello. Bu SAS URL'leri oluşturulur hello nedeniyle yoludur. Bir Bulucu süresi dolduktan sonra karşıdan tooaccess bir varlık istiyorsanız, yeni bir StartTime ile yeni bir tane oluşturmanız gerekir.
>
>

### <a name="download-files"></a>Dosyaları indirme
Merhaba AccessPolicy ve Bulucu kümesi oluşturduktan sonra hello Azure Storage REST API'leri kullanarak dosyaları indirebilir.  

> [!NOTE]
> Merhaba dosya adı eklemelisiniz hello dosya için toodownload toohello Bulucu istediğiniz **yolu** hello önceki bölümde alınan değer. Örneğin, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4? . . .
>
>

Azure depolama BLOB'ları ile çalışma hakkında daha fazla bilgi için bkz: [Blob hizmeti REST API'si](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).

Daha önce gerçekleştirdiğiniz iş kodlama hello (Uyarlamalı MP4 kümesine kodlama) sonucunda aşamalı olarak indirebilirsiniz birden çok MP4 dosyaları sahiptir. Örneğin:    

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


### <a name="creating-a-streaming-url-for-streaming-content"></a>İçerik akışı için bir akış URL'si oluşturma
kodun gösterdiği nasıl aşağıdaki hello toocreate akış URL'si Bulucusu:

    POST https://wamsbayclus001rest-hs/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3", "StartTime" : "2014-05-17T16:45:53",, "Type":2}

Başarılı olursa, yanıt aşağıdaki hello verilir:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 981
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 2eac4158-fc78-4fa2-81ee-c9f582dc385f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:39 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/Asset"
             }
          },
          "Id":"nb:lid:UUID:52034bf6-dfae-4d83-aad3-3bd87dcb1a5d",
          "ExpirationDateTime":"\/Date(1337049395000)\/",
          "Type":2,
          "Path":"http://wamsbayclus001rest-hs.net/52034bf6-dfae-4d83-aad3-3bd87dcb1a5d/",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3",
          "StartTime":"\/Date(1337031395000)\/"
       }
    }

toostream bir akış medya oynatıcı kesintisiz akış kaynak URL, kesintisiz akış bildirim dosyası, ardından "/ bildirimi" Merhaba hello adıyla hello Path özelliği eklemeniz gerekir.

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

toostream HLS, ekleme (format = m3u8-aapl) hello sonra "/ bildirimi".

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

toostream MPEG DASH ekleme (biçim mpd zaman csf =) hello sonra "/ bildirimi".

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)


## <a id="play"></a>İçeriğinizi oynatma
toostream video, kullandığınız [Azure Media Services Oynatıcısı](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

tootest aşamalı indirmek için bir URL (örneğin, IE, Chrome, Safari) bir tarayıcıya yapıştırın.

## <a name="next-steps-media-services-learning-paths"></a>Sonraki Adımlar: Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
