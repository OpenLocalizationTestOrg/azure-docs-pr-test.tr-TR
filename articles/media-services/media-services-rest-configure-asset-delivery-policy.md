---
title: "Media Services REST API kullanarak aaaConfiguring varlık teslim ilkeleri | Microsoft Docs"
description: "Bu konuda gösterilmektedir nasıl Media Services REST API kullanarak tooconfigure farklı varlık teslim ilkeleri."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5cb9d32a-e68b-4585-aa82-58dded0691d0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 8203230d570935e17382c598820dbfe42f83f8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-asset-delivery-policies"></a>Varlık teslim ilkeleri yapılandırma
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

Dinamik olarak şifrelenmiş toodeliver varlıklar planlıyorsanız, hello birini hello medya Hizmetleri içerik teslim iş akışı varlıklar için teslim ilkelerini yapılandırma adımları. Merhaba varlık teslim ilkesini Media Services nasıl teslim, varlık toobe için istediğinizi söyler: toodynamically istediğiniz olup olmadığına bakılmaksızın hangi akış protokolüne Varlığınızı dinamik olarak (örneğin, MPEG DASH, HLS, kesintisiz akış veya tümü için), paketlenmiş Varlığınızı şifrelemek ve nasıl (Zarf veya ortak şifreleme).

Bu konuda neden ve nasıl anlatılmaktadır toocreate ve varlık teslim ilkeleri yapılandırın.

>[!NOTE]
>AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu. İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu. 
>
>Ayrıca, toobe mümkün toouse dinamik paketleme ve dinamik şifreleme Varlığınızı içermelidir Uyarlamalı bit hızlı MP4s veya uyarlamalı bit hızlı kesintisiz akış dosyaları kümesidir.

Farklı ilkeleri toohello uygulayabilir aynı varlık. Örneğin, PlayReady şifreleme tooSmooth akış ve AES zarfı şifreleme tooMPEG uygulayabilir DASH ve HLS. Bir teslim ilkesinde tanımlanmayan tüm protokollerin (örneğin, yalnızca hello protokol olarak HLS belirten tek bir ilke ekliyorsunuz) akışla aktarılması engellenir. Merhaba özel durum toothis hiç tanımlanmış hiçbir varlık teslim ilkesini varsa ' dir. Ardından, tüm protokoller hello Temizle izin verilir.

Toodeliver depolama şifrelenmiş varlık isterseniz hello varlığın teslim ilkesini yapılandırmanız gerekir. Varlığınızı akışı önce sunucu kaldırır hello depolama şifrelemesi ve akışlar hello kullanarak içeriğinizi akış hello teslim ilkesini belirtilen. Örneğin, toodeliver Varlığınızı Gelişmiş Şifreleme Standardı (AES) Zarf şifreleme anahtarıyla şifrelenir, çok hello ilke türünü ayarlayın**DynamicEnvelopeEncryption**. tooremove depolama şifreleme ve hello Temizle, akış hello varlığı ayarlamak hello ilke türü çok**NoDynamicEncryption**. Bu ilke türleri tooconfigure nasıl izleyin Göster örnekleri.

Hello varlık teslim ilkesini nasıl yapılandırdığınıza bağlı mümkün toodynamically paketi, dinamik olarak şifrelemek ve akış akış protokolleri aşağıdaki hello: kesintisiz akış, HLS, MPEG DASH akışları.

Liste gösterir hello aşağıdaki hello toostream kesintisiz, HLS, DASH kullandığınız biçimlendirir.

Kesintisiz akış:

{akış uç noktası adı-media services hesabı adı}.streaming.mediaservices.windows.net/{konum kimliği}/{dosya adı}.ism/Manifest

HLS:

{uç nokta adı media services hesabı name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl) akış

MPEG DASH

{uç nokta adı media services hesabı name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf) akış


Yönergeler için nasıl toopublish bir varlık ve yapı bir akış URL'si bkz [akış URL'si oluşturma](media-services-deliver-streaming-content.md).

## <a name="considerations"></a>Dikkat edilmesi gerekenler
* Bu varlık için bir (akış) OnDemand Bulucu bulunmakla birlikte bir varlıkla ilişkilendirilen AssetDeliveryPolicy silemezsiniz. Merhaba tooremove hello hello varlık ilkesinden hello İlkesi silmeden önce önerilir.
* Hiçbir varlık teslim ilkesini ayarlandığında akış Bulucusu bir depolama şifrelenmiş varlık oluşturulamıyor.  Merhaba varlık şifrelenmiş depolama değilse, hello sistem, bir varlık teslim ilkesini olmadan temizleyin hello Bulucu ve akış hello varlık oluşturmak olanak tanır.
* Tek bir varlık ile ilişkili birden çok varlık teslim ilkeleri olabilir ancak yalnızca tek yönlü toohandle verilen AssetDeliveryProtocol belirtebilirsiniz.  Bir istemci bir kesintisiz akış bir istekte bulunduğunda hello sistem hangisinin bilmediğinden, bir hatayla sonuçlanır hello AssetDeliveryProtocol.SmoothStreaming protokolü belirtmek toolink iki teslim İlkesi çalışırsanız anlamına tooapply istediğiniz.
* Bir varlığı ile var olan bir akış Bulucu varsa, yeni bir ilke toohello varlık bağlantı olamaz, mevcut bir hello varlık ilkesinden bağlantısını veya hello varlık ile ilişkili bir teslim ilkesini güncelleştirin.  İlk tooremove hello akış Bulucusu sahip hello ilkeleri ayarlamak ve akış Bulucu hello yeniden oluşturun.  İçerik hello Menşe veya bir aşağı akış CDN tarafından önbelleğe bu yana, istemciler için sorunlara neden olmaz Bulucu ancak Akış hello yeniden oluşturduğunuzda aynı locatorId emin olmalısınız hello kullanabilirsiniz.

>[!NOTE]

>Varlıklar Media Services erişirken, HTTP istekleri özel üstbilgi alanlarını ve değerlerini ayarlamanız gerekir. Daha fazla bilgi için bkz: [Media Services REST API geliştirme için Kurulum](media-services-rest-how-to-use.md).

## <a name="connect-toomedia-services"></a>TooMedia Hizmetleri'ne Bağlama

Nasıl tooconnect toohello AMS API, bkz. bilgi [Azure AD kimlik doğrulaması ile erişim hello Azure Media Services API](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Başarıyla toohttps://media.windows.net bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız. Sonraki çağrılar toohello yapmanız gereken yeni bir URI.

## <a name="clear-asset-delivery-policy"></a>Clear varlık teslim ilkesini
### <a id="create_asset_delivery_policy"></a>Varlık teslim ilkesini oluşturma
Hello aşağıdaki HTTP isteği toonot dinamik şifreleme uygulanır ve aşağıdaki hello hiçbirinde toodeliver hello akış protokolleri belirten bir varlık teslim ilkesi oluşturur: MPEG DASH, HLS ve kesintisiz akış protokollerini. 

Merhaba, değerleri bilgi bir AssetDeliveryPolicy oluştururken belirtebilirsiniz için bkz: [AssetDeliveryPolicy tanımlarken kullanılan türleri](#types) bölümü.   

İsteği:

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    Host: media.windows.net

    {"Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null}

Yanıtı:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 363
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    x-ms-request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 06:21:27 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element",
    "Id":"nb:adpid:UUID:92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd",
    "Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null,
    "Created":"2015-02-08T06:21:27.6908329Z",
    "LastModified":"2015-02-08T06:21:27.6908329Z"}

### <a id="link_asset_with_asset_delivery_policy"></a>Varlık teslim ilkesini bağlantı varlığı
HTTP isteği bağlantılar hello aşağıdaki hello varlık toohello varlık teslim ilkesini için belirtilmiş.

İsteği:

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A86933344-9539-4d0c-be7d-f842458693e0')/$links/DeliveryPolicies HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-3344-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 56d2763f-6e72-419d-ba3c-685f6db97e81
    Host: media.windows.net

    {"uri":"https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')"}

Yanıtı:

    HTTP/1.1 204 No Content


## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a>DynamicEnvelopeEncryption varlık teslim ilkesini
### <a name="create-content-key-of-hello-envelopeencryption-type-and-link-it-toohello-asset"></a>Merhaba EnvelopeEncryption tür içerik anahtarı oluşturun ve toohello varlık Bağla
DynamicEnvelopeEncryption teslim İlkesi belirtirken, varlık tooa içerik anahtarı hello EnvelopeEncryption türü toomake emin toolink gerekir. Daha fazla bilgi için bkz: [bir içerik anahtarı oluşturma](media-services-rest-create-contentkey.md)).

### <a id="get_delivery_url"></a>Teslim URL'sini alma
Get hello teslim hello URL'sini hello içerik anahtarı hello önceki adımda oluşturduğunuz teslim yöntemi belirtilmiş. URL toorequest döndürülen hello bir istemcinin kullandığı bir AES anahtarı ya da bir sipariş tooplayback hello PlayReady lisans korumalı içeriği.

Merhaba URL tooget Hello türü hello hello HTTP isteğinin gövdesinde belirtin. Bir Media Services PlayReady lisans edinme URL'si isteği içeriğinizi PlayReady ile koruyorsanız 1 hello keyDeliveryType kullanılarak: {"keyDeliveryType": 1}. İçeriğinizi hello Zarf şifrelemeli koruyorsanız, bir anahtar alım keyDeliveryType için 2 belirterek istek URL'si: {"keyDeliveryType": 2}.

İsteği:

    POST https://media.windows.net/api/ContentKeys('nb:kid:UUID:dc88f996-2859-4cf7-a279-c52a9d6b2f04')/GetKeyDeliveryUrl HTTP/1.1
    Content-Type: application/json
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423452029&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=IEXV06e3drSIN5naFRBdhJZCbfEqQbFZsGSIGmawhEo%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    Host: media.windows.net
    Content-Length: 21

    {"keyDeliveryType":2}

Yanıtı:

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 198
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    x-ms-request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 21:42:30 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#Edm.String","value":"https://amsaccount1.keydelivery.mediaservices.windows.net/?KID=dc88f996-2859-4cf7-a279-c52a9d6b2f04"}


### <a name="create-asset-delivery-policy"></a>Varlık teslim ilkesini oluşturma
Merhaba aşağıdaki HTTP isteği oluşturur hello **AssetDeliveryPolicy** diğer bir deyişle yapılandırılmış tooapply dinamik Zarf şifreleme (**DynamicEnvelopeEncryption**) toohello **HLS**Protokolü (Bu örnekte, diğer protokolleri akışla aktarılması engellenir). 

Merhaba, değerleri bilgi bir AssetDeliveryPolicy oluştururken belirtebilirsiniz için bkz: [AssetDeliveryPolicy tanımlarken kullanılan türleri](#types) bölümü.   

İsteği:

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]"}


Yanıtı:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 460
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3Aec9b994e-672c-4a5b-8490-a464eeb7964b')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    x-ms-request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 09 Feb 2015 05:24:38 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element","Id":"nb:adpid:UUID:ec9b994e-672c-4a5b-8490-a464eeb7964b","Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]","Created":"2015-02-09T05:24:38.9167436Z","LastModified":"2015-02-09T05:24:38.9167436Z"}


### <a name="link-asset-with-asset-delivery-policy"></a>Varlık teslim ilkesini bağlantı varlığı
Bkz: [varlık teslim ilkesini bağlantı varlığı](#link_asset_with_asset_delivery_policy)

## <a name="dynamiccommonencryption-asset-delivery-policy"></a>DynamicCommonEncryption varlık teslim ilkesini
### <a name="create-content-key-of-hello-commonencryption-type-and-link-it-toohello-asset"></a>Merhaba CommonEncryption tür içerik anahtarı oluşturun ve toohello varlık Bağla
DynamicCommonEncryption teslim İlkesi belirtirken, varlık tooa içerik anahtarı hello CommonEncryption türü toomake emin toolink gerekir. Daha fazla bilgi için bkz: [bir içerik anahtarı oluşturma](media-services-rest-create-contentkey.md)).

### <a name="get-delivery-url"></a>Teslim URL'sini alma
Merhaba PlayReady teslim yöntemini hello içerik anahtarının hello önceki adımda oluşturduğunuz Hello teslim URL'sini alma. Bir istemci bir sipariş tooplayback hello PlayReady lisans korumalı URL toorequest içerik döndürülen hello kullanır. Daha fazla bilgi için bkz: [alma teslim URL](#get_delivery_url).

### <a name="create-asset-delivery-policy"></a>Varlık teslim ilkesini oluşturma
Merhaba aşağıdaki HTTP isteği oluşturur hello **AssetDeliveryPolicy** diğer bir deyişle yapılandırılmış tooapply dinamik ortak şifreleme (**DynamicCommonEncryption**) toohello **kesintisiz akış**  Protokolü (Bu örnekte, diğer protokolleri akışla aktarılması engellenir). 

Merhaba, değerleri bilgi bir AssetDeliveryPolicy oluştururken belirtebilirsiniz için bkz: [AssetDeliveryPolicy tanımlarken kullanılan türleri](#types) bölümü.   

İsteği:

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":1,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\/PlayReady\/"}]"}


Widevine DRM kullanarak içeriğinizi tooprotect istiyorsanız hello AssetDeliveryConfiguration değerleri toouse (7 hello değeri olan) WidevineLicenseAcquisitionUrl güncelleştirin ve bir lisans teslimat hizmetinin hello URL'sini belirtin. Widevine lisansları teslim AMS ortaklarını toohelp aşağıdaki hello kullanabilirsiniz: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).

Örneğin: 

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":2,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":7,\"Value\":\"https:\\/\\/example.net\/WidevineLicenseAcquisition\/"}]"}

> [!NOTE]
> Widevine ile şifrelerken tire kullanarak mümkün toodeliver yalnızca olacaktır. Emin toospecify tire (2) içinde hello varlık teslim Protokolü olun.
> 
> 

### <a name="link-asset-with-asset-delivery-policy"></a>Varlık teslim ilkesini bağlantı varlığı
Bkz: [varlık teslim ilkesini bağlantı varlığı](#link_asset_with_asset_delivery_policy)

## <a id="types"></a>AssetDeliveryPolicy tanımlarken kullanılan türleri

### <a name="assetdeliveryprotocol"></a>AssetDeliveryProtocol

Merhaba aşağıdaki enum hello varlık teslim protokolü için ayarlayabileceğiniz değerler açıklar.

    [Flags]
    public enum AssetDeliveryProtocol
    {
        /// <summary>
        /// No protocols.
        /// </summary>
        None = 0x0,

        /// <summary>
        /// Smooth streaming protocol.
        /// </summary>
        SmoothStreaming = 0x1,

        /// <summary>
        /// MPEG Dynamic Adaptive Streaming over HTTP (DASH)
        /// </summary>
        Dash = 0x2,

        /// <summary>
        /// Apple HTTP Live Streaming protocol.
        /// </summary>
        HLS = 0x4,

        ProgressiveDownload = 0x10, 
 
        /// <summary>
        /// Include all protocols.
        /// </summary>
        All = 0xFFFF
    }

### <a name="assetdeliverypolicytype"></a>AssetDeliveryPolicyType

Merhaba aşağıdaki enum hello varlık teslim İlkesi türü için ayarlayabileceğiniz değerler açıklar.  

    public enum AssetDeliveryPolicyType
    {
        /// <summary>
        /// Delivery Policy Type not set.  An invalid value.
        /// </summary>
        None,

        /// <summary>
        /// hello Asset should not be delivered via this AssetDeliveryProtocol. 
        /// </summary>
        Blocked, 

        /// <summary>
        /// Do not apply dynamic encryption toohello asset.
        /// </summary>
        /// 
        NoDynamicEncryption,  

        /// <summary>
        /// Apply Dynamic Envelope encryption.
        /// </summary>
        DynamicEnvelopeEncryption,

        /// <summary>
        /// Apply Dynamic Common encryption.
        /// </summary>
        DynamicCommonEncryption
        }

### <a name="contentkeydeliverytype"></a>ContentKeyDeliveryType

Merhaba aşağıdaki enum değerleri hello içerik anahtar toohello istemci tooconfigure hello teslim yöntemini kullanabilirsiniz açıklanmaktadır.
    
    public enum ContentKeyDeliveryType
    {
        /// <summary>
        /// None.
        ///
        </summary>
        None = 0,

        /// <summary>
        /// Use PlayReady License acquistion protocol
        ///
        </summary>
        PlayReadyLicense = 1,

        /// <summary>
        /// Use MPEG Baseline HTTP key protocol.
        ///
        </summary>
        BaselineHttp = 2,

        /// <summary>
        /// Use Widevine License acquistion protocol
        ///
        </summary>
        Widevine = 3

    }


### <a name="assetdeliverypolicyconfigurationkey"></a>AssetDeliveryPolicyConfigurationKey

Enum aşağıdaki hello tooconfigure kullanılan anahtarları tooget belirli yapılandırma için bir varlık teslim ilkesini ayarlayabilirsiniz değerleri açıklanmaktadır.

    public enum AssetDeliveryPolicyConfigurationKey
    {
        /// <summary>
        /// No policies.
        /// </summary>
        None,

        /// <summary>
        /// Exact Envelope key URL.
        /// </summary>
        EnvelopeKeyAcquisitionUrl,

        /// <summary>
        /// Base key url that will have KID=<Guid> appended for Envelope.
        /// </summary>
        EnvelopeBaseKeyAcquisitionUrl,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption in Base64 format.
        /// </summary>
        EnvelopeEncryptionIVAsBase64,

        /// <summary>
        /// hello PlayReady License Acquisition Url toouse for common encryption.
        /// </summary>
        PlayReadyLicenseAcquisitionUrl,

        /// <summary>
        /// hello PlayReady Custom Attributes tooadd toohello PlayReady Content Header
        /// </summary>
        PlayReadyCustomAttributes,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption.
        /// </summary>
        EnvelopeEncryptionIV,

        /// <summary>
        /// Widevine DRM acquisition url
        /// </summary>
        WidevineLicenseAcquisitionUrl
    }

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

