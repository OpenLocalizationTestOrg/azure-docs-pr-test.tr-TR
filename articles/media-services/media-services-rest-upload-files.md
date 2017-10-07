---
title: "REST kullanarak Media Services hesabı aaaUpload dosyalarıyla | Microsoft Docs"
description: "Oluşturma ve varlıklar karşıya tooget medya medya Hizmetleri içine nasıl içerik öğrenin."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 41df7cbe-b8e2-48c1-a86c-361ec4e5251f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 2a92cecdc32d747d7a478946f069c15931eb32b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-rest"></a>Dosyaları REST kullanarak bir Media Services hesabına veri yükleme
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> * [Portal](media-services-portal-upload-files.md)
> 
> 

Media Services’de dijital dosyalar bir varlığa yüklenir. Merhaba [varlık](https://docs.microsoft.com/rest/api/media/operations/asset) varlık içerebilir video, ses, görüntüler, küçük resim koleksiyonları, metin parçaları ve kapalı açıklamalı alt yazı dosyaları (ve bu dosyalar hakkında hello meta veriler.)  Hello varlığa Hello dosyalar yüklendiğinde, içeriğiniz sonraki işleme ve akışla için hello bulutta güvenli bir şekilde depolanır. 

> [!NOTE]
> ilgili önemli noktalar aşağıdaki hello Uygula:
> 
> * Media Services URL'leri içeriği (örneğin, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) akış Merhaba oluştururken hello hello IAssetFile.Name özellik değerini kullanır Bu nedenle, yüzde kodlama izin verilmiyor. Merhaba hello değerini **adı** özelliği hello aşağıdakilerden herhangi birini içeremez [yüzde kodlama-ayrılmış karakterleri](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ". Ayrıca, yalnızca bir olabilir '.' hello dosya adı uzantısı için.
> * Merhaba hello adının uzunluğu 260 karakterden uzun olmamalıdır.
> * Media Services işlemek için desteklenen bir toohello en büyük dosya boyutu sınırı yoktur. Lütfen bakın [bu](media-services-quotas-and-limitations.md) hello dosya boyutu sınırlaması hakkında ayrıntılı bilgi için konu.
> 

Varlıklar yüklemeyle hello temel iş akışı aşağıdaki bölümlerde hello ayrılır:

* Bir varlık oluşturun
* (İsteğe bağlı) bir varlık şifrele
* Bir dosya tooblob depolama yükleme

AMS ayrıca tooupload varlıklar toplu sağlar. Daha fazla bilgi için [bu](media-services-rest-upload-files.md#upload_in_bulk) bölüme bakın.

> [!NOTE]
> Varlıklar Media Services erişirken, HTTP istekleri özel üstbilgi alanlarını ve değerlerini ayarlamanız gerekir. Daha fazla bilgi için bkz: [Media Services REST API geliştirme için Kurulum](media-services-rest-how-to-use.md).
> 

## <a name="connect-toomedia-services"></a>TooMedia Hizmetleri'ne Bağlama

Nasıl tooconnect toohello AMS API, bkz. bilgi [Azure AD kimlik doğrulaması ile erişim hello Azure Media Services API](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Başarıyla toohttps://media.windows.net bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız. Sonraki çağrılar toohello yapmanız gereken yeni bir URI.

## <a name="upload-assets"></a>Varlıkları yükleyin

### <a name="create-an-asset"></a>Bir varlık oluşturun

Bir varlık, birden çok türleri veya Media Services, video, ses, görüntüler, küçük resim koleksiyonları, metin parçaları ve kapalı açıklamalı alt yazı dosyaları dahil olmak üzere nesne kümeleri için bir kapsayıcıdır. REST API bir varlık oluşturma, posta gönderme gerektirir hello tooMedia Hizmetleri isteyin ve hello istek gövdesinde Varlığınızı ilgili herhangi bir özellik bilgi yerleştirme.

Bir varlık oluşturma olduğunda belirtebilirsiniz hello özelliklerinden biri **seçenekleri**. **Seçenekler** bir varlığı ile oluşturulan hello şifreleme seçenekleri açıklayan bir numaralandırma değeridir. Geçerli bir değer hello listesinde aşağıdaki değerleri olmayan bir birleşimini hello değerlerinden biri. 

* **Hiçbiri** = **0**: şifreleme kullanılır. Merhaba varsayılan değer budur. Bu seçenek kullanıldığında, içeriğinizin aktarım veya deposunda kalan korunmadığını unutmayın.
    Aşamalı indirme kullanarak toodeliver bir MP4 planlıyorsanız, bu seçeneği kullanın. 
* **StorageEncrypted** = **1**: karşıya yükleme ve depolama için AES 256 bit şifreleme ile şifrelenmiş, dosyaları toobe için isteyip istemediğinizi belirtin.
  
    Şifrelenmiş depolama varlığınız olması durumunda, varlık teslim ilkesini yapılandırmanız gerekir. Daha fazla bilgi için bkz: [varlık teslim ilkesini yapılandırma](media-services-rest-configure-asset-delivery-policy.md).
* **CommonEncryptionProtected** = **2**: ortak bir şifreleme yöntemi (örneğin, PlayReady) ile korunan dosyaları karşıya varsa belirtin. 
* **EnvelopeEncryptionProtected** = **4**: AES dosyaları ile şifrelenmiş HLS karşıya varsa belirtin. Hello dosyaları gerekir alınan kodlanmış ve Transform Manager tarafından şifrelenmiş olduğunu unutmayın.

> [!NOTE]
> Varlığınızı şifreleme kullanacaksa, oluşturmalısınız bir **ContentKey** ve izleyen konu hello açıklandığı gibi tooyour varlık Bağla:[nasıl toocreate bir ContentKey](media-services-rest-create-contentkey.md). Merhaba varlığa hello dosyaları karşıya yükleme sonra tooupdate hello şifreleme özellikleri hello gerektiğini unutmayın **AssetFile** varlık hello sırasında aldığınız hello değerlerle **varlık** şifreleme. Bunu hello kullanarak **birleştirme** HTTP isteği. 
> 
> 

örnekte gösterildiği nasıl aşağıdaki hello toocreate bir varlık.

**HTTP isteği**

    POST https://media.windows.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"BigBuckBunny.mp4"}

**HTTP yanıtı**

Başarılı olursa, hello aşağıdaki verilir:

    HTP/1.1 201 Created
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
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT
    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a>Bir AssetFile oluşturma
Merhaba [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) varlığı temsil eden bir blob kapsayıcısında depolanır ses veya video dosyası. Bir varlık dosyası her zaman bir varlıkla ilişkilidir ve bir varlığı bir veya daha çok varlık dosyaları içerebilir. bir varlık dosyası nesne bir blob kapsayıcısında dijital bir dosyayla ilişkili değilse hello Media Services Kodlayıcısı görev başarısız olur.

Bu hello Not **AssetFile** örneği ve hello gerçek medya dosyası olan iki farklı nesneler. Merhaba medya dosyası hello gerçek medya içeriği içerirken hello AssetFile örneği hello medya dosyası hakkındaki meta verileri içerir.

Bir blob kapsayıcıya bir dijital medyayı dosyanızı karşıya sonra hello kullanacağı **birleştirme** medya dosyanızın (Merhaba konunun ilerleyen bölümlerinde gösterildiği gibi) hakkında bilgi içeren HTTP isteği tooupdate hello AssetFile. 

**HTTP isteği**

    POST https://media.windows.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
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

### <a name="creating-hello-accesspolicy-with-write-permission"></a>Merhaba AccessPolicy yazma izni olan oluşturuluyor.

>[!NOTE]
>Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için). Merhaba kullanması gereken her zaman kullanıyorsanız, aynı ilke kimliği hello aynı gün / erişim izinlerini, örneğin, uzun bir süre (karşıya yükleme olmayan ilkeleri) yerinde hedeflenen tooremain olan bulucular ilkeleri. Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.

Blob depolama alanına herhangi bir dosya karşıya yüklemeden önce hello erişim ilkesi hakları tooan varlık yazmak için ayarlayın. bir HTTP isteği toohello AccessPolicies varlık sonrası toodo ayarlayın. Oluşturulduktan sonra bir dakika Cinsiden Süre değer tanımlama veya yanıt olarak bir 500 İç sunucu hata iletisi alırsınız. AccessPolicies hakkında daha fazla bilgi için bkz: [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).

örnekte gösterildiği nasıl aşağıdaki hello toocreate bir AccessPolicy:

**HTTP isteği**

    POST https://media.windows.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"} 

**HTTP isteği**

    If successful, hello following response is returned:

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
tooreceive gerçek karşıya yükleme URL'si Merhaba, SAS Bulucu oluşturun. Bulucular bir varlık tooaccess dosyalarında istediğiniz istemciler için hello başlangıç saati ve bağlantı uç noktasının türünü tanımlayın. İstekleri ve gereksinimlerini verilen AccessPolicy ve varlık çifti toohandle farklı bir istemci için birden çok Bulucu varlık oluşturabilirsiniz. Her bu Bulucuyu hello StartTime değerinin yanı sıra hello AccessPolicy toodetermine hello süreyi bir URL kullanılabilir hello Dakika Cinsiden Süre değerini kullanın. Daha fazla bilgi için bkz: [Bulucu](https://docs.microsoft.com/rest/api/media/operations/locator).

Bir SAS URL'si biçimi aşağıdaki hello sahiptir:

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

Bazı dikkate alınması gereken noktalar vardır:

* Aynı anda belirli bir varlıkla ilişkilendirilen beşten fazla benzersiz Bulucular sahip olamaz. Daha fazla bilgi için Bulucu bakın.
* Dosyalarınızı hemen tooupload gerekiyorsa, StartTime değeri toofive dakika hello geçerli saati önce ayarlamanız gerekir. Bu; çünkü istemci makine ve Media Services arasında eğme saat olabilir. Ayrıca, StartTime değeriniz tarih saat biçiminde aşağıdaki hello olmalıdır: YYYY-MM-: ssZ (örneğin, "2014-05-23T17:53:50Z").    
* 30-40 saniyenin olabilir bir Bulucu kullanılabilir olmasından toowhen oluşturulduktan sonra gecikme. Bu sorun tooboth SAS URL'si ve Kaynak Konum Belirleyicisi geçerlidir.

Aşağıdaki örneğine hello nasıl toocreate bir SAS URL'si tarafından tanımlanan Bulucu, hello hello istek gövdesindeki (bir SAS Bulucu için "1") ve bir isteğe bağlı kaynak Bulucu için "2" Type özelliği gösterir. Merhaba **yolu** döndürülen özelliği içeren hello URL dosyanızı tooupload kullanmanız gerekir.

**HTTP isteği**

    POST https://media.windows.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
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
Merhaba AccessPolicy ve Bulucu kümesi oluşturduktan sonra hello gerçek hello Azure Storage REST API'leri kullanılarak karşıya yüklenen tooan Azure Blob Storage kapsayıcısına dosyasıdır. Blok blobları hello dosyalarını yüklemeniz gerekir. Sayfa bloblarını Azure Media Services tarafından desteklenmiyor.  

> [!NOTE]
> Merhaba dosya adı eklemelisiniz hello dosya için tooupload toohello Bulucu istediğiniz **yolu** hello önceki bölümde alınan değer. Örneğin, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4? . . . 
> 
> 

Azure depolama BLOB'ları ile çalışma hakkında daha fazla bilgi için bkz: [Blob hizmeti REST API'si](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).

### <a name="update-hello-assetfile"></a>Merhaba AssetFile güncelleştir
Dosyanızı yüklediğiniz, hello FileAsset boyut (ve diğer) bilgi güncelleştirin. Örneğin:

    MERGE https://media.windows.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


**HTTP yanıtı**

Başarılı, hello aşağıdaki döndürülür: HTTP/1.1 204 İçerik yok

### <a name="delete-hello-locator-and-accesspolicy"></a>Merhaba Bulucu ve AccessPolicy Sil
**HTTP isteği**

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

**HTTP yanıtı**

Başarılı olursa, hello aşağıdaki verilir:

    HTTP/1.1 204 No Content 
    ...

**HTTP isteği**

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

**HTTP yanıtı**

Başarılı olursa, hello aşağıdaki verilir:

    HTTP/1.1 204 No Content 
    ...

## <a id="upload_in_bulk"></a>Varlıkları toplu yükleyin
### <a name="create-hello-ingestmanifest"></a>Merhaba IngestManifest oluşturma
Merhaba IngestManifest varlıklar, varlık dosyaları ve olabilir istatistik bilgileri kümesi için bir kapsayıcıdır toodetermine hello ilerlemesini, toplu alma hello kümesi için kullanılır.

**HTTP isteği**

    POST https:// media.windows.net/API/IngestManifests HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 36
    Expect: 100-continue

    { "Name" : "ExampleManifestREST" }

### <a name="create-assets"></a>Varlıklar oluşturma
Merhaba IngestManifestAsset oluşturmadan önce toocreate hello toplu alanını kullanarak tamamlanacak varlık gerekir. Bir varlık, birden çok türleri veya Media Services, video, ses, görüntüler, küçük resim koleksiyonları, metin parçaları ve kapalı açıklamalı alt yazı dosyaları dahil olmak üzere nesne kümeleri için bir kapsayıcıdır. Hello REST API'da, bir varlık oluşturmak için bir HTTP POST isteği tooMicrosoft Azure Media Services gönderme ve hello istek gövdesinde Varlığınızı ilgili herhangi bir özellik bilgi yerleştirme gerekir. Bu örnekte, hello varlık hello istek gövdesi dahil hello StorageEncrption(1) seçeneği kullanılarak oluşturulur.

**HTTP yanıtı**

    POST https://media.windows.net/API/Assets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 55
    Expect: 100-continue

    { "Name" : "ExampleManifestREST_Asset", "Options" : 1 }

### <a name="create-hello-ingestmanifestassets"></a>Merhaba IngestManifestAssets oluşturma
IngestManifestAssets toplu alma ile kullanılan varlıklar bir IngestManifest içinde temsil eder. Merhaba temelde hello varlık toohello bildirimi bağlayın. Azure Media Services IngestManifestFiles ilişkili koleksiyon toohello IngestManifestAsset üzerinde temel hello dosya karşıya yükleme için dahili olarak izler. Bu dosyalar yüklendiğinde hello varlık tamamlandı. Bir HTTP POST isteği ile yeni bir IngestManifestAsset oluşturabilirsiniz. Merhaba istek gövdesinde hello IngestManifest kimliği ve hello varlık kimliği IngestManifestAsset toplu alma için birlikte bağlanması gereken bu hello içerir.

**HTTP yanıtı**

    POST https://media.windows.net/API/IngestManifestAssets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 152
    Expect: 100-continue
    { "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "Asset" : { "Id" : "nb:cid:UUID:b757929a-5a57-430b-b33e-c05c6cbef02e"}}


### <a name="create-hello-ingestmanifestfiles-for-each-asset"></a>Merhaba IngestManifestFiles her varlık için oluşturma
Bir IngestManifestFile bir varlık için toplu alma bir parçası olarak yüklenen gerçek ses veya video blob nesneyi temsil eder. Şifreleme ile ilgili bir şifreleme seçeneği hello varlık kullanmadığınız sürece özellikler gerekli değildir. Bu bölümde kullanılan hello örnek StorageEncryption varlık daha önce oluşturduğunuz Merhaba kullanan bir IngestManifestFile oluşturma gösterir.

**HTTP yanıtı**

    POST https://media.windows.net/API/IngestManifestFiles HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 367
    Expect: 100-continue

    { "Name" : "REST_Example_File.wmv", "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "ParentIngestManifestAssetId" : "nb:maid:UUID:beed8531-9a03-9043-b1d8-6a6d1044cdda", "IsEncrypted" : "true", "EncryptionScheme" : "StorageEncryption", "EncryptionVersion" : "1.0", "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510" }

### <a name="upload-hello-files-tooblob-storage"></a>Merhaba dosyaları tooBlob depolama karşıya yükle
Merhaba varlık dosyaları toohello blob depolama kapsayıcısını hello hello IngestManifest BlobStorageUriForUpload özelliği tarafından sağlanan URI karşıya yükleme özellikli tüm yüksek hızlı istemci uygulamasını kullanabilirsiniz. Bir önem düzeyindeki yüksek hızlı karşıya yükleme hizmeti [Aspera istendiğinde Azure uygulaması için](http://go.microsoft.com/fwlink/?LinkId=272001).

### <a name="monitor-bulk-ingest-progress"></a>İzleyici toplu ilerleme durumunu alma
Toplu işlemleri için bir IngestManifest hello IngestManifest hello istatistikleri özelliği yoklayarak alındıktan hello ilerlemesini izleyebilirsiniz. Özelliği bir karmaşık tür olup [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics). toopoll hello istatistikleri özelliği hello IngestManifest kimliği geçirme bir HTTP GET isteği gönder

## <a name="create-contentkeys-used-for-encryption"></a>Şifreleme için kullanılan ContentKeys oluşturma
Varlığınızı şifreleme kullanacaksa, varlık dosyaları hello oluşturmadan önce şifreleme için kullanılan hello ContentKey toobe oluşturmanız gerekir. Depolama şifrelemesi için hello aşağıdaki özellikleri hello istek gövdesinde yer alması gerekir.

| İstek gövdesi özelliği | Açıklama |
| --- | --- |
| Kimlik |Merhaba biz oluşturan ContentKey kimliği kendisini izleyen hello kullanarak biçimi, "nb:kid:UUID:<NEW GUID>". |
| ContentKeyType |Bu içerik anahtarı için bir tamsayı olarak hello içerik anahtar türü budur. Biz depolama şifrelemesi için 1 hello değeri geçirin. |
| EncryptedContentKey |256 bitlik (32 bayt) bir değer olan yeni bir içerik anahtarı değeri oluşturuyoruz. başlangıç anahtarı hello GetProtectionKeyId ve GetProtectionKey yöntemleri için bir HTTP GET isteği yürüterek Microsoft Azure Media Services'den alıyoruz hello depolama şifreleme X.509 sertifikası kullanılarak şifrelenir. |
| ProtectionKeyId |Bu olduğu hello koruma anahtar kimliği için kullanılan tooencrypt edildi hello depolama şifreleme X.509 sertifikası bizim içerik anahtarı. |
| ProtectionKeyType |Bu hello şifreleme için kullanılan tooencrypt hello içerik anahtar: hello koruma anahtarı türüdür. Bu değer StorageEncryption(1) Bizim örneğimizde olur. |
| Sağlama toplamı |Merhaba MD5 hello içerik anahtarı için hesaplanan sağlama. Merhaba içerik anahtarı kimliği içerikle hello şifreleyerek hesaplanır. Merhaba örnek kodu nasıl toocalculate hello sağlama toplamı gösterir. |

**HTTP yanıtı**

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 572
    Expect: 100-continue

    {"Id" : "nb:kid:UUID:316d14d4-b603-4d90-b8db-0fede8aa48f8", "ContentKeyType" : 1, "EncryptedContentKey" : "Y4NPej7heOFa2vsd8ZEOcjjpu/qOq3RJ6GRfxa8CCwtAM83d6J2mKOeQFUmMyVXUSsBCCOdufmieTKi+hOUtNAbyNM4lY4AXI537b9GaY8oSeje0NGU8+QCOuf7jGdRac5B9uIk7WwD76RAJnqyep6U/OdvQV4RLvvZ9w7nO4bY8RHaUaLxC2u4aIRRaZtLu5rm8GKBPy87OzQVXNgnLM01I8s3Z4wJ3i7jXqkknDy4VkIyLBSQvIvUzxYHeNdMVWDmS+jPN9ScVmolUwGzH1A23td8UWFHOjTjXHLjNm5Yq+7MIOoaxeMlKPYXRFKofRY8Qh5o5tqvycSAJ9KUqfg==", "ProtectionKeyId" : "7D9BB04D9D0A4A24800CADBFEF232689E048F69C", "ProtectionKeyType" : 1, "Checksum" : "TfXtjCIlq1Y=" }

### <a name="link-hello-contentkey-toohello-asset"></a>Bağlantı hello ContentKey toohello varlık
Merhaba ContentKey ilişkili tooone ya da daha fazla varlıklar bir HTTP POST isteği göndermektir. Merhaba aşağıdaki isteği olan bir örnek toolink hello örnek ContentKey toohello örnek varlığı kimliğe göre

**HTTP yanıtı**

    POST https://media.windows.net/API/Assets('nb:cid:UUID:b3023475-09b4-4647-9d6d-6fc242822e68')/$links/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 113
    Expect: 100-continue

    { "uri": "https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A32e6efaf-5fba-4538-b115-9d1cefe43510')"}

**HTTP yanıtı**

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a>Sonraki adımlar

Karşıya yüklenen varlıklarınızı artık kodlayabilirsiniz. Daha fazla bilgi için bkz. [Varlıkları kodlama](media-services-portal-encode.md).

Azure işlevleri tootrigger yapılandırılmış hello kapsayıcısında ulaşan bir dosyayı temel bir kodlama işi de kullanabilirsiniz. Daha fazla bilgi için [bu örneğe](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ) bakın.

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How tooGet a Media Processor]: media-services-get-media-processor.md

