---
title: "aaaEncrypting içeriğinizi AMS REST API kullanarak depolama şifrelemesi ile"
description: "Bilgi nasıl tooencrypt içeriğinizi AMS REST API'lerini kullanarak depolama şifrelemesi ile."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a0a79f3d-76a1-4994-9202-59b91a2230e0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: d5f8cb8dd1dcded76c9fededccc772d8102ccbad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypting-your-content-with-storage-encryption"></a>İçeriğinizi depolama şifrelemesi ile şifreleme

Tooencrypt önerilir yerel olarak AES 256 kullanarak içeriğinizi bit şifrelemesi ve tooAzure bunu depolanacağı depolama şifrelenen yükleyin.

Bu makalede AMS depolama şifrelemesi genel bir bakış sunar ve nasıl tooupload hello depolama içeriğin şifreli gösterir:

* Bir içerik anahtarı oluşturun.
* Bir varlık oluşturun. Merhaba AssetCreationOption tooStorageEncryption hello varlık oluştururken ayarlayın.
  
     Şifrelenmiş varlıklar içerik anahtarlarla ilişkili toobe sahip.
* Bağlantı hello içerik anahtar toohello varlığı.  
* Ayarlama hello şifreleme ilgili hello AssetFile varlıklar üzerinde parametreleri.

## <a name="considerations"></a>Dikkat edilmesi gerekenler 

Toodeliver depolama şifrelenmiş varlık isterseniz hello varlığın teslim ilkesini yapılandırmanız gerekir. Varlığınızı akışı önce sunucu kaldırır hello depolama şifrelemesi ve akışlar hello kullanarak içeriğinizi akış hello teslim ilkesini belirtilen. Daha fazla bilgi için bkz: [varlık teslim ilkeleri yapılandırma](media-services-rest-configure-asset-delivery-policy.md).

Varlıklar Media Services erişirken, HTTP istekleri özel üstbilgi alanlarını ve değerlerini ayarlamanız gerekir. Daha fazla bilgi için bkz: [Media Services REST API geliştirme için Kurulum](media-services-rest-how-to-use.md). 

## <a name="connect-toomedia-services"></a>TooMedia Hizmetleri'ne Bağlama

Nasıl tooconnect toohello AMS API, bkz. bilgi [Azure AD kimlik doğrulaması ile erişim hello Azure Media Services API](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Başarıyla toohttps://media.windows.net bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız. Sonraki çağrılar toohello yapmanız gereken yeni bir URI.

## <a name="storage-encryption-overview"></a>Depolama Şifrelemesi'ne genel bakış
Merhaba AMS depolama şifrelemesi uygulayan **AES CTRL** mod şifreleme toohello tüm dosyası.  AES-CTRL, rastgele uzunlukta verileri doldurma gerek kalmadan şifreleyebilirsiniz bir blok şifreleme modudur. Merhaba AES algoritması ve ardından XOR lık hello çıktısını AES hello veri tooencrypt sahip olan bir sayaç bloğun şifreleyerek çalışır veya şifrelerini çözme.  kullanılan hello sayaç blok hello InitializationVector toobytes 0 too7 hello sayaç değerinin hello değerini kopyalayarak oluşturulur ve 8 bayt too15 hello sayaç değerinin toozero ayarlayın. Merhaba 16 bayt sayacı bloğunun, 8 bayt too15 (yani hello en az önemli bayt), bir sonraki her işlenen veri bloğu için artar ve bir basit 64 bit işaretsiz tamsayıyı ağ bayt sırasında tutulan olarak kullanılır. Bu tamsayı, artan hello en büyük değeri (0xFFFFFFFFFFFFFFFF) ulaşırsa hello sayacın (yani 0 bayt too7) 64 bit hello diğer etkilemeden hello blok sayaç toozero (8 bayt too15) sıfırlar unutmayın.   Sipariş toomaintain hello güvenlik hello AES CTRL modu şifreleme her içerik anahtarı her dosya için benzersiz olacaktır için InitializationVector değeri için belirtilen bir anahtarı tanımlayıcı hello ve dosyaları 2'den olacaktır ^ uzunluğu 64 engeller.  Hiçbir zaman bir sayaç değeri olan tooensure budur verilen anahtarla yeniden kullanılabilir. Merhaba CTRL modu hakkında daha fazla bilgi için bkz: [Bu wiki sayfa](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (Merhaba wiki makalesi kullanır hello terimi "InitializationVector" yerine "Nonce").

Kullanım **depolama şifreleme** tooencrypt AES 256 kullanarak yerel olarak Temizle içeriğinizi bit şifrelemesi ve tooAzure depolanır depolama şifrelenen yükleyin. Depolama şifrelemesi ile korunan varlıklar otomatik olarak şifrelenmemiş ve bir şifrelenmiş dosya sistemi önceki tooencoding ve yeni bir çıkış varlığı olarak geri isteğe bağlı olarak yeniden şifrelenmiş önceki toouploading yerleştirilir. Depolama şifrelemesinin birincil kullanım durumu hello yüksek kaliteli giriş medya dosyalarınızın güçlü şifrelemeyle diskte rest toosecure istediğiniz durumdur.

Sipariş toodeliver depolama şifrelenmiş varlık'da, Media Services toodeliver içeriğinizi nasıl istediğiniz bilmesi için hello varlığın teslim ilkesini yapılandırmanız gerekir. Varlığınızı akışı önce sunucu kaldırır hello depolama şifrelemesi ve akışlar hello kullanarak içeriğinizi akış hello teslim ilkesini (örneğin, AES, ortak şifreleme veya şifreleme) belirtildi.

## <a name="create-contentkeys-used-for-encryption"></a>Şifreleme için kullanılan ContentKeys oluşturma
Şifrelenmiş varlıklar depolama şifreleme anahtarıyla ilişkili toobe sahip. Merhaba içerik anahtar toobe hello varlık dosyaları oluşturmadan önce şifreleme için kullanılan oluşturmanız gerekir. Bu bölümde açıklanmıştır nasıl toocreate bir içerik anahtarı.

Merhaba şifrelenmiş toobe istediğiniz varlıklarla ilişkilendireceğiniz içerik anahtarları oluşturmak için genel adımlar verilmiştir. 

1. Depolama şifrelemesi için rastgele bir 32 baytlık AES anahtarı oluşturur. 
   
    Bu ilişkili tüm dosyalar anlamına gelir, varlık için içerik anahtarı hello olacaktır, varlıkla toouse aynı içerik anahtarı şifre çözme sırasında hello. 
2. Merhaba çağrısı [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) ve [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) yöntemleri tooget hello kullanılan tooencrypt olmalıdır doğru X.509 sertifikası, içerik anahtarı.
3. İçerik hello X.509 sertifikasının ortak anahtarı hello anahtarınızla şifreleyin. 
   
   Media Services .NET SDK'sı ile OAEP hello şifreleme yaparken RSA kullanır.  Merhaba .NET örnekte görebilirsiniz [EncryptSymmetricKeyData işlevi](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).
4. Başlangıç anahtarı tanımlayıcısı ve içerik anahtarı kullanılarak hesaplanan bir sağlama toplamı değeri oluşturun. .NET örnek aşağıdaki hello hello sağlama toplamı hello GUID hello anahtarı tanımlayıcısı bir kısmını kullanarak hesaplar ve hello içerik anahtarı temizleyin.

        public static string CalculateChecksum(byte[] contentKey, Guid keyId)
        {
            const int ChecksumLength = 8;
            const int KeyIdLength = 16;

            byte[] encryptedKeyId = null;

            // Checksum is computed by AES-ECB encrypting hello KID
            // with hello content key.
            using (AesCryptoServiceProvider rijndael = new AesCryptoServiceProvider())
            {
                rijndael.Mode = CipherMode.ECB;
                rijndael.Key = contentKey;
                rijndael.Padding = PaddingMode.None;

                ICryptoTransform encryptor = rijndael.CreateEncryptor();
                encryptedKeyId = new byte[KeyIdLength];
                encryptor.TransformBlock(keyId.ToByteArray(), 0, KeyIdLength, encryptedKeyId, 0);
            }

            byte[] retVal = new byte[ChecksumLength];
            Array.Copy(encryptedKeyId, retVal, ChecksumLength);

            return Convert.ToBase64String(retVal);
        }

1. Merhaba ile Merhaba içerik anahtarı oluşturun **EncryptedContentKey** (toobase64 kodlu dize dönüştürülen), **ProtectionKeyId**, **ProtectionKeyType**,  **ContentKeyType**, ve **sağlama toplamı** önceki adımlarda almış değerleri.

    Depolama şifrelemesi için hello aşağıdaki özellikleri hello istek gövdesinde yer alması gerekir.

    İstek gövdesi özelliği    | Açıklama
    ---|---
    Kimlik | Merhaba biz oluşturan ContentKey kimliği kendisini izleyen hello kullanarak biçimi, "nb:kid:UUID:<NEW GUID>".
    ContentKeyType | Bu içerik anahtarı için bir tamsayı olarak hello içerik anahtar türü budur. Biz depolama şifrelemesi için 1 hello değeri geçirin.
    EncryptedContentKey | 256 bitlik (32 bayt) bir değer olan yeni bir içerik anahtarı değeri oluşturuyoruz. başlangıç anahtarı hello GetProtectionKeyId ve GetProtectionKey yöntemleri için bir HTTP GET isteği yürüterek Microsoft Azure Media Services'den alıyoruz hello depolama şifreleme X.509 sertifikası kullanılarak şifrelenir. .NET kodu aşağıdaki hello bir örnek olarak bkz: Merhaba **EncryptSymmetricKeyData** tanımlanan yöntemi [burada](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).
    ProtectionKeyId | Bu olduğu hello koruma anahtar kimliği için kullanılan tooencrypt edildi hello depolama şifreleme X.509 sertifikası bizim içerik anahtarı.
    ProtectionKeyType | Bu hello şifreleme için kullanılan tooencrypt hello içerik anahtar: hello koruma anahtarı türüdür. Bu değer StorageEncryption(1) Bizim örneğimizde olur.
    Sağlama toplamı |Merhaba MD5 hello içerik anahtarı için hesaplanan sağlama. Merhaba içerik anahtarı kimliği içerikle hello şifreleyerek hesaplanır. Merhaba örnek kodu nasıl toocalculate hello sağlama toplamı gösterir.


### <a name="retrieve-hello-protectionkeyid"></a>Merhaba ProtectionKeyId alma
Aşağıdaki örnek hello nasıl tooretrieve hello ProtectionKeyId, hello sertifika içerik anahtarınızı şifrelerken kullanmak için bir sertifika parmak izini gösterir. Bu adım toomake makinenizde hello uygun sertifika zaten sahip olduğunuzdan emin yapın.

İsteği:

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net

Yanıtı:

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 139
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 2b6aa7a4-3a09-4b08-b581-26b55667f817
    x-ms-request-id: 2b6aa7a4-3a09-4b08-b581-26b55667f817
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 04 Feb 2015 02:42:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Edm.String","value":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C"}

### <a name="retrieve-hello-protectionkey-for-hello-protectionkeyid"></a>Merhaba ProtectionKey hello ProtectionKeyId alma
Merhaba aşağıdaki örnekte nasıl hello ProtectionKeyId kullanarak tooretrieve hello X.509 sertifikası hello önceki adımda aldığınız gösterilmektedir.

İsteği:

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net

Yanıtı:

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1227
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    request-id: 1523e8f3-8ed2-40fe-8a9a-5d81eb572cc8
    x-ms-request-id: 1523e8f3-8ed2-40fe-8a9a-5d81eb572cc8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 05 Feb 2015 07:52:30 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Edm.String",
    "value":"MIIDSTCCAjGgAwIBAgIQqf92wku/HLJGCbMAU8GEnDANBgkqhkiG9w0BAQQFADAuMSwwKgYDVQQDEyN3YW1zYmx1cmVnMDAxZW5jcnlwdGFsbHNlY3JldHMtY2VydDAeFw0xMjA1MjkwNzAwMDBaFw0zMjA1MjkwNzAwMDBaMC4xLDAqBgNVBAMTI3dhbXNibHVyZWcwMDFlbmNyeXB0YWxsc2VjcmV0cy1jZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAzR0SEbXefvUjb9wCUfkEiKtGQ5Gc328qFPrhMjSo+YHe0AVviZ9YaxPPb0m1AaaRV4dqWpST2+JtDhLOmGpWmmA60tbATJDdmRzKi2eYAyhhE76MgJgL3myCQLP42jDusWXWSMabui3/tMDQs+zfi1sJ4Ch/lm5EvksYsu6o8sCv29VRwxfDLJPBy2NlbV4GbWz5Qxp2tAmHoROnfaRhwp6WIbquk69tEtu2U50CpPN2goLAqx2PpXAqA+prxCZYGTHqfmFJEKtZHhizVBTFPGS3ncfnQC9QIEwFbPw6E5PO5yNaB68radWsp5uvDg33G1i8IT39GstMW6zaaG7cNQIDAQABo2MwYTBfBgNVHQEEWDBWgBCOGT2hPhsvQioZimw8M+jOoTAwLjEsMCoGA1UEAxMjd2Ftc2JsdXJlZzAwMWVuY3J5cHRhbGxzZWNyZXRzLWNlcnSCEKn/dsJLvxyyRgmzAFPBhJwwDQYJKoZIhvcNAQEEBQADggEBABcrQPma2ekNS3Wc5wGXL/aHyQaQRwFGymnUJ+VR8jVUZaC/U/f6lR98eTlwycjVwRL7D15BfClGEHw66QdHejaViJCjbEIJJ3p2c9fzBKhjLhzB3VVNiLIaH6RSI1bMPd2eddSCqhDIn3VBN605GcYXMzhYp+YA6g9+YMNeS1b+LxX3fqixMQIxSHOLFZ1G/H2xfNawv0VikH3djNui3EKT1w/8aRkUv/AAV0b3rYkP/jA1I0CPn0XFk7STYoiJ3gJoKq9EMXhit+Iwfz0sMkfhWG12/XO+TAWqsK1ZxEjuC9OzrY7pFnNxs4Mu4S8iinehduSpY+9mDd3dHynNwT4="}

### <a name="create-hello-content-key"></a>Merhaba içerik anahtarı oluşturun
Merhaba X.509 sertifikası alınır ve kendi ortak anahtar tooencrypt içerik anahtarınızı kullanılan sonra oluşturmanız bir **ContentKey** varlık ve onun özellik değerlerinin buna uygun olarak ayarla.

Ne zaman ayarlamalısınız hello değerlerden biri hello hello türü anahtarıdır içerik oluşturun. Merhaba depolama şifrelemesi durumunda hello '1' değeridir. 

örnekte gösterildiği nasıl aşağıdaki hello toocreate bir **ContentKey** ile bir **ContentKeyType** depolama şifreleme ("1") ve hello için ayarladığınız **ProtectionKeyType** Ayarla "0" çok koruma anahtarı kimliği hello tooindicate hello X.509 sertifika parmak izi ' dir.  

İstek

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net
    {
    "Name":"ContentKey",
    "ProtectionKeyId":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C", 
    "ContentKeyType":"1", 
    "ProtectionKeyType":"0",
    "EncryptedContentKey":"your encrypted content key",
    "Checksum":"calculated checksum"
    }

Yanıtı:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 777
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A9c8ea9c6-52bd-4232-8a43-8e43d8564a99')
    Server: Microsoft-IIS/8.5
    request-id: 76e85e0f-5cf1-44cb-b689-b3455888682c
    x-ms-request-id: 76e85e0f-5cf1-44cb-b689-b3455888682c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 04 Feb 2015 02:37:46 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeys/@Element",
    "Id":"nb:kid:UUID:9c8ea9c6-52bd-4232-8a43-8e43d8564a99","Created":"2015-02-04T02:37:46.9684379Z",
    "LastModified":"2015-02-04T02:37:46.9684379Z",
    "ContentKeyType":1,
    "EncryptedContentKey":"your encrypted content key",
    "Name":"ContentKey",
    "ProtectionKeyId":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C",
    "ProtectionKeyType":0,
    "Checksum":"calculated checksum"}

## <a name="create-an-asset"></a>Bir varlık oluşturun
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

    {"Name":"BigBuckBunny" "Options":1}

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
       "Options":1,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

## <a name="associate-hello-contentkey-with-an-asset"></a>Merhaba ContentKey bir varlıkla ilişkilendirme
Merhaba ContentKey oluşturduktan sonra hello aşağıdaki örnekte gösterildiği gibi hello $links işlemi kullanarak, varlık ile ilişkilendirin:

İsteği:

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Afbd7ce05-1087-401b-aaae-29f16383c801')/$links/ContentKeys HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeys('nb%3Akid%3AUUID%3A01e6ea36-2285-4562-91f1-82c45736047c')"}

Yanıtı:

    HTTP/1.1 204 No Content 

## <a name="create-an-assetfile"></a>Bir AssetFile oluşturma
Merhaba [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) varlığı temsil eden bir blob kapsayıcısında depolanır ses veya video dosyası. Bir varlık dosyası her zaman bir varlıkla ilişkilidir ve bir varlığı bir veya daha çok varlık dosyaları içerebilir. bir varlık dosyası nesne bir blob kapsayıcısında dijital bir dosyayla ilişkili değilse hello Media Services Kodlayıcısı görev başarısız olur.

Bu hello Not **AssetFile** örneği ve hello gerçek medya dosyası olan iki farklı nesneler. Merhaba medya dosyası hello gerçek medya içeriği içerirken hello AssetFile örneği hello medya dosyası hakkındaki meta verileri içerir.

Bir blob kapsayıcıya bir dijital medyayı dosyanızı karşıya sonra hello kullanacağı **birleştirme** medya dosyanızın (Bu konuda gösterilmez) hakkında bilgi içeren HTTP isteği tooupdate hello AssetFile. 

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
       "IsEncrypted":"true",
       "EncryptionScheme" : "StorageEncryption", 
       "EncryptionVersion" : "1.0",       
       "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510",
       "InitializationVector" : "397304628502661816</d:InitializationVector",
       "Options":0,
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
       "EncryptionVersion": "1.0",
       "EncryptionScheme": "StorageEncryption",
       "IsEncrypted":true,
       "EncryptionKeyId":"nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510",
       "InitializationVector":"397304628502661816</d:InitializationVector",
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }
