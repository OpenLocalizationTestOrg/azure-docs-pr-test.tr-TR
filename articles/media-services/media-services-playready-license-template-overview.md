---
title: "aaaMedia Hizmetleri PlayReady lisans şablonu genel bakış"
description: "Bu konuda tooconfigure PlayReady lisansları kullanılan PlayReady lisans şablonu genel bir bakış sağlar."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: fddce5d0-1278-478f-ae05-9b985c748731
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 5a5ba930c56f70038db204681486ebc4308199fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-playready-license-template-overview"></a>Medya Hizmetleri PlayReady lisans şablonu genel bakış
Azure Media Services, artık Microsoft PlayReady lisansları teslim etmek için bir hizmet sunar. Merhaba son kullanıcı player (örneğin, Silverlight) tooplay çalıştığında, PlayReady korumalı içeriği, bir istek gönderilen toohello lisans teslimat hizmeti tooobtain lisans. Merhaba lisans hizmeti hello isteği onaylarsa, gönderilen toohello istemcisi olan hello lisans verir ve olması kullanılan toodecrypt ve play hello belirtilen içerik.

Media Services PlayReady lisanslarınızı yapılandırmanıza olanak tanıyan API'ler de sağlar. Bir kullanıcı tooplayback çalışırken, PlayReady DRM çalışma zamanı tooenforce Merhaba istediğiniz kısıtlamaları korumalı içeriği ve lisansları hello hakları içerir.
Aşağıda, belirtebilirsiniz PlayReady lisans kısıtlamaları bazı örnekleri şunlardır:

* Merhaba DateTime hangi hello Lisans geçerli değil.
* Merhaba hello Lisans sona erdiğinde tarih saat değeri. 
* İçin hello lisans toobe hello istemcide kalıcı depolama alanına kaydedildi. Kalıcı lisansları genellikle kullanılan tooallow çevrimdışı kayıttan yürütme hello içerik var.
* Merhaba en düşük güvenlik düzeyi bir oynatıcı içeriğinizi tooplay olması gerekir. 
* Merhaba hello çıkış denetimleri audio\video içerik koruma düzeyi çıktı. 
* Hello çıkış (3.5) içinde hello bölümünde denetimleri daha fazla bilgi için bkz: [PlayReady uyumluluk kuralları](https://www.microsoft.com/playready/licensing/compliance/) belge.

> [!NOTE]
> Şu anda yalnızca hello PlayRight hello PlayReady lisans (Bu hakkı gereklidir) yapılandırabilirsiniz. Merhaba PlayRight hello istemci hello özelliği tooplayback hello içeriği sağlar. Merhaba PlayRight de kısıtlamaları belirli tooplayback yapılandırılmasına olanak tanır. Daha fazla bilgi için bkz: [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).
> 
> 

Media Services kullanarak tooconfigure PlayReady lisansları hello Media Services PlayReady lisans şablonu yapılandırmanız gerekir. Merhaba şablonu XML dosyasında tanımlanır.

Merhaba aşağıdaki örnekte bir temel akış lisans yapılandırır hello basit (ve en yaygın) şablonu gösterir. Bu lisansı ile istemcileriniz mümkün tooplayback olacaktır, PlayReady korumalı içeriği.

    <?xml version="1.0" encoding="utf-8"?>
    <PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" 
                                      xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1">
      <LicenseTemplates>
        <PlayReadyLicenseTemplate>
          <ContentKey i:type="ContentEncryptionKeyFromHeader" />
          <PlayRight />
        </PlayReadyLicenseTemplate>
      </LicenseTemplates>
    </PlayReadyLicenseResponseTemplate>

Merhaba XML toohello PlayReady lisans şablonu XML Şeması hello PlayReady lisans şablonu XML Şeması bölümünde tanımlanan uyumludur.

Media Services de kullanılan tooserialized ve seri durumdan çıkarılmış tooand hello XML gelen olabilir .NET sınıfları kümesini tanımlar. Ana sınıf bir açıklaması için bkz: [Media Services .NET sınıfları](media-services-playready-license-template-overview.md#classes). kullanılan tooconfigure lisans şablonları olan.

.NET kullanan bir uçtan uca örnek tooconfigure hello PlayReady lisans şablonu sınıfları için bkz: [dinamik şifreleme kullanarak PlayReady ve lisans teslimat hizmeti](media-services-protect-with-drm.md).

## <a id="classes"></a>Kullanılan tooconfigure lisans şablonlarıdır Media Services .NET sınıfları
Merhaba ana .NET sınıfları kullanılan tooconfigure Media Services PlayReady lisans şablonlarıdır Hello aşağıda verilmiştir. Bu sınıfların tanımlanan toohello türlerini eşleme [PlayReady lisans şablonu XML Şeması](media-services-playready-license-template-overview.md#schema).

Merhaba [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) sınıfının kullanılan tooserialize olması ve hello Media Services lisans şablondan XML tooand seri durumdan.

### <a name="playreadylicenseresponsetemplate"></a>PlayReadyLicenseResponseTemplate
[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) -gönderilen hello yanıtı geri toohello son kullanıcı için bu sınıf hello şablonu temsil eder. Bir veya daha fazla lisans şablonların listesi yanı sıra hello lisans sunucusu ve Merhaba uygulaması (için özel uygulama mantığını yararlı olabilir) arasında bir özel veri dize için bir alan içeriyor.

Bu hello "üst düzey" Merhaba şablonu hiyerarşisindeki sınıftır. Merhaba yanıt şablonu lisans şablonları listesini içerir ve hello lisans şablonları içerir (doğrudan veya dolaylı olarak) anlamına tüm hello hello şablonu veri toobe seri hale diğer sınıflar.

### <a name="playreadylicensetemplate"></a>PlayReadyLicenseTemplate
[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) -hello sınıfı, PlayReady lisansları toobe toohello son kullanıcılar döndürülen oluşturmak için bir lisans şablonu temsil eder. Hello içerik anahtarı hello lisans hello verilerini içerir ve hakları veya kısıtlamaları toobe tarafından hello PlayReady DRM çalışma zamanı hello içerik anahtarı kullanarak zorunlu tutulur.

### <a id="PlayReadyPlayRight"></a>PlayReadyPlayRight
[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) -Bu sınıf hello PlayReady lisans PlayRight temsil eder. Merhaba içerik konu toohello sıfır veya daha fazla kısıtlama hello lisans ve hello PlayRight kendisini (için kayıttan yürütme belirli bir ilke) yapılandırılmış hello kullanıcı hello özelliği tooplayback verir. Merhaba PlayRight hello İlkesi çoğunu toodo hello içerik üzerinden çalınabilir çıkışları hello türlerini denetlemek çıkış kısıtlamaları ve belirli bir çıkış kullanırken yerinde götürüldüğü kısıtlamalar vardır. Örneğin, DRM çalışma zamanı yalnızca hello DigitalVideoOnlyContentRestriction etkin, ardından Merhaba, dijital çıkışları (analog video çıkışına toopass hello içerik izin verilmeyecek) görüntülenen hello video toobe izin verir.

> [!IMPORTANT]
> Bu tür kısıtlamaların çok güçlü olabilir ancak hello tüketici deneyimini de etkileyebilir. Merhaba çıkışı korumalardan çok kısıtlayıcı olarak yapılandırılırsa, hello içerik bazı istemcilerde unplayable olabilir. Daha fazla bilgi için bkz: Merhaba [PlayReady uyumluluk kuralları](https://www.microsoft.com/playready/licensing/compliance/) belge.
> 
> 

Silverlight destekler ne koruma düzeyleri örneği için bkz: [çıkışı korumalardan Silverlight desteği](http://go.microsoft.com/fwlink/?LinkId=617318).

## <a id="schema"></a>PlayReady lisans şablonu XML Şeması
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:ser="http://schemas.microsoft.com/2003/10/Serialization/" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:import namespace="http://schemas.microsoft.com/2003/10/Serialization/" />
      <xs:complexType name="AgcAndColorStripeRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction" />
      <xs:simpleType name="ContentType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Unspecified" />
          <xs:enumeration value="UltravioletDownload" />
          <xs:enumeration value="UltravioletStreaming" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="ContentType" nillable="true" type="tns:ContentType" />
      <xs:complexType name="ExplicitAnalogTelevisionRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="BestEffort" type="xs:boolean" />
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ExplicitAnalogTelevisionRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction" />
      <xs:complexType name="PlayReadyContentKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="PlayReadyContentKey" nillable="true" type="tns:PlayReadyContentKey" />
      <xs:complexType name="ContentEncryptionKeyFromHeader">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence />
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromHeader" nillable="true" type="tns:ContentEncryptionKeyFromHeader" />
      <xs:complexType name="ContentEncryptionKeyFromKeyIdentifier">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence>
              <xs:element minOccurs="0" name="KeyIdentifier" type="ser:guid" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromKeyIdentifier" nillable="true" type="tns:ContentEncryptionKeyFromKeyIdentifier" />
      <xs:complexType name="PlayReadyLicenseResponseTemplate">
        <xs:sequence>
          <xs:element name="LicenseTemplates" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
          <xs:element minOccurs="0" name="ResponseCustomData" nillable="true" type="xs:string">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseResponseTemplate" nillable="true" type="tns:PlayReadyLicenseResponseTemplate" />
      <xs:complexType name="ArrayOfPlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfPlayReadyLicenseTemplate" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
      <xs:complexType name="PlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AllowTestDevices" type="xs:boolean" />
          <xs:element minOccurs="0" name="BeginDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element name="ContentKey" nillable="true" type="tns:PlayReadyContentKey" />
          <xs:element minOccurs="0" name="ContentType" type="tns:ContentType">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExpirationDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="GracePeriod" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="LicenseType" type="tns:PlayReadyLicenseType" />
          <xs:element minOccurs="0" name="PlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
      <xs:simpleType name="PlayReadyLicenseType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Nonpersistent" />
          <xs:enumeration value="Persistent" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="PlayReadyLicenseType" nillable="true" type="tns:PlayReadyLicenseType" />
      <xs:complexType name="PlayReadyPlayRight">
        <xs:sequence>
          <xs:element minOccurs="0" name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AllowPassingVideoContentToUnknownOutput" type="tns:UnknownOutputPassingOption">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AnalogVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="DigitalVideoOnlyContentRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExplicitAnalogTelevisionOutputRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="FirstPlayExpiration" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComponentVideoRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComputerMonitorRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyPlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
      <xs:simpleType name="UnknownOutputPassingOption">
        <xs:restriction base="xs:string">
          <xs:enumeration value="NotAllowed" />
          <xs:enumeration value="Allowed" />
          <xs:enumeration value="AllowedWithVideoConstriction" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="UnknownOutputPassingOption" nillable="true" type="tns:UnknownOutputPassingOption" />
      <xs:complexType name="ScmsRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction" />
    </xs:schema>



## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

