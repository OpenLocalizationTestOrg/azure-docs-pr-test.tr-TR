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
# <a name="media-services-playready-license-template-overview"></a><span data-ttu-id="7e4f3-103">Medya Hizmetleri PlayReady lisans şablonu genel bakış</span><span class="sxs-lookup"><span data-stu-id="7e4f3-103">Media Services PlayReady license template overview</span></span>
<span data-ttu-id="7e4f3-104">Azure Media Services, artık Microsoft PlayReady lisansları teslim etmek için bir hizmet sunar.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-104">Azure Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="7e4f3-105">Merhaba son kullanıcı player (örneğin, Silverlight) tooplay çalıştığında, PlayReady korumalı içeriği, bir istek gönderilen toohello lisans teslimat hizmeti tooobtain lisans.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-105">When hello end user player (for example, Silverlight) tries tooplay your PlayReady protected content, a request is sent toohello license delivery service tooobtain a license.</span></span> <span data-ttu-id="7e4f3-106">Merhaba lisans hizmeti hello isteği onaylarsa, gönderilen toohello istemcisi olan hello lisans verir ve olması kullanılan toodecrypt ve play hello belirtilen içerik.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-106">If hello license service approves hello request, it issues hello license which is sent toohello client and can be used toodecrypt and play hello specified content.</span></span>

<span data-ttu-id="7e4f3-107">Media Services PlayReady lisanslarınızı yapılandırmanıza olanak tanıyan API'ler de sağlar.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-107">Media Services also provides APIs that let you configure your PlayReady licenses.</span></span> <span data-ttu-id="7e4f3-108">Bir kullanıcı tooplayback çalışırken, PlayReady DRM çalışma zamanı tooenforce Merhaba istediğiniz kısıtlamaları korumalı içeriği ve lisansları hello hakları içerir.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-108">Licenses contain hello rights and restrictions that you want for hello PlayReady DRM runtime tooenforce when a user is trying tooplayback protected content.</span></span>
<span data-ttu-id="7e4f3-109">Aşağıda, belirtebilirsiniz PlayReady lisans kısıtlamaları bazı örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="7e4f3-109">Below are some examples of PlayReady license restrictions that you can specify:</span></span>

* <span data-ttu-id="7e4f3-110">Merhaba DateTime hangi hello Lisans geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-110">hello DateTime from which hello license is valid.</span></span>
* <span data-ttu-id="7e4f3-111">Merhaba hello Lisans sona erdiğinde tarih saat değeri.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-111">hello DateTime value when hello license expires.</span></span> 
* <span data-ttu-id="7e4f3-112">İçin hello lisans toobe hello istemcide kalıcı depolama alanına kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-112">For hello license toobe saved in persistent storage on hello client.</span></span> <span data-ttu-id="7e4f3-113">Kalıcı lisansları genellikle kullanılan tooallow çevrimdışı kayıttan yürütme hello içerik var.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-113">Persistent licenses are typically used tooallow offline playback of hello content.</span></span>
* <span data-ttu-id="7e4f3-114">Merhaba en düşük güvenlik düzeyi bir oynatıcı içeriğinizi tooplay olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-114">hello minimum security level that a player must have tooplay your content.</span></span> 
* <span data-ttu-id="7e4f3-115">Merhaba hello çıkış denetimleri audio\video içerik koruma düzeyi çıktı.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-115">hello output protection level for hello output controls for audio\video content.</span></span> 
* <span data-ttu-id="7e4f3-116">Hello çıkış (3.5) içinde hello bölümünde denetimleri daha fazla bilgi için bkz: [PlayReady uyumluluk kuralları](https://www.microsoft.com/playready/licensing/compliance/) belge.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-116">For more information, see hello Output Controls section (3.5) in hello [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>

> [!NOTE]
> <span data-ttu-id="7e4f3-117">Şu anda yalnızca hello PlayRight hello PlayReady lisans (Bu hakkı gereklidir) yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-117">Currently, you can only configure hello PlayRight of hello PlayReady license (this right is required).</span></span> <span data-ttu-id="7e4f3-118">Merhaba PlayRight hello istemci hello özelliği tooplayback hello içeriği sağlar.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-118">hello PlayRight gives hello client hello ability tooplayback hello content.</span></span> <span data-ttu-id="7e4f3-119">Merhaba PlayRight de kısıtlamaları belirli tooplayback yapılandırılmasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-119">hello PlayRight also allows configuring restrictions specific tooplayback.</span></span> <span data-ttu-id="7e4f3-120">Daha fazla bilgi için bkz: [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span><span class="sxs-lookup"><span data-stu-id="7e4f3-120">For more information, see [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span></span>
> 
> 

<span data-ttu-id="7e4f3-121">Media Services kullanarak tooconfigure PlayReady lisansları hello Media Services PlayReady lisans şablonu yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-121">tooconfigure PlayReady licenses using Media Services, you must configure hello Media Services PlayReady license template.</span></span> <span data-ttu-id="7e4f3-122">Merhaba şablonu XML dosyasında tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-122">hello template is defined in XML.</span></span>

<span data-ttu-id="7e4f3-123">Merhaba aşağıdaki örnekte bir temel akış lisans yapılandırır hello basit (ve en yaygın) şablonu gösterir.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-123">hello following example shows hello simplest (and most common) template that configures a basic streaming license.</span></span> <span data-ttu-id="7e4f3-124">Bu lisansı ile istemcileriniz mümkün tooplayback olacaktır, PlayReady korumalı içeriği.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-124">With this license, your clients would be able tooplayback your PlayReady protected content.</span></span>

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

<span data-ttu-id="7e4f3-125">Merhaba XML toohello PlayReady lisans şablonu XML Şeması hello PlayReady lisans şablonu XML Şeması bölümünde tanımlanan uyumludur.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-125">hello XML conforms toohello PlayReady license template XML schema defined in hello PlayReady license template XML schema section.</span></span>

<span data-ttu-id="7e4f3-126">Media Services de kullanılan tooserialized ve seri durumdan çıkarılmış tooand hello XML gelen olabilir .NET sınıfları kümesini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-126">Media Services also defines a set of .NET classes that could be used tooserialized and deserialized tooand from hello XML.</span></span> <span data-ttu-id="7e4f3-127">Ana sınıf bir açıklaması için bkz: [Media Services .NET sınıfları](media-services-playready-license-template-overview.md#classes).</span><span class="sxs-lookup"><span data-stu-id="7e4f3-127">For description of main classes, see [Media Services .NET classes](media-services-playready-license-template-overview.md#classes).</span></span> <span data-ttu-id="7e4f3-128">kullanılan tooconfigure lisans şablonları olan.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-128">that are used tooconfigure license templates.</span></span>

<span data-ttu-id="7e4f3-129">.NET kullanan bir uçtan uca örnek tooconfigure hello PlayReady lisans şablonu sınıfları için bkz: [dinamik şifreleme kullanarak PlayReady ve lisans teslimat hizmeti](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="7e4f3-129">For an end-to-end example that uses .NET classes tooconfigure hello PlayReady license template, see [Using PlayReady Dynamic Encryption and License Delivery Service](media-services-protect-with-drm.md).</span></span>

## <span data-ttu-id="7e4f3-130"><a id="classes"></a>Kullanılan tooconfigure lisans şablonlarıdır Media Services .NET sınıfları</span><span class="sxs-lookup"><span data-stu-id="7e4f3-130"><a id="classes"></a>Media Services .NET classes that are used tooconfigure license templates</span></span>
<span data-ttu-id="7e4f3-131">Merhaba ana .NET sınıfları kullanılan tooconfigure Media Services PlayReady lisans şablonlarıdır Hello aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-131">hello following are hello main .NET classes are used tooconfigure Media Services PlayReady license templates.</span></span> <span data-ttu-id="7e4f3-132">Bu sınıfların tanımlanan toohello türlerini eşleme [PlayReady lisans şablonu XML Şeması](media-services-playready-license-template-overview.md#schema).</span><span class="sxs-lookup"><span data-stu-id="7e4f3-132">These classes map toohello types defined in [PlayReady license template XML schema](media-services-playready-license-template-overview.md#schema).</span></span>

<span data-ttu-id="7e4f3-133">Merhaba [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) sınıfının kullanılan tooserialize olması ve hello Media Services lisans şablondan XML tooand seri durumdan.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-133">hello [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) class is used tooserialize and deserialize tooand from hello Media Services license template XML.</span></span>

### <a name="playreadylicenseresponsetemplate"></a><span data-ttu-id="7e4f3-134">PlayReadyLicenseResponseTemplate</span><span class="sxs-lookup"><span data-stu-id="7e4f3-134">PlayReadyLicenseResponseTemplate</span></span>
<span data-ttu-id="7e4f3-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) -gönderilen hello yanıtı geri toohello son kullanıcı için bu sınıf hello şablonu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) - This class represents hello template for hello response sent back toohello end user.</span></span> <span data-ttu-id="7e4f3-136">Bir veya daha fazla lisans şablonların listesi yanı sıra hello lisans sunucusu ve Merhaba uygulaması (için özel uygulama mantığını yararlı olabilir) arasında bir özel veri dize için bir alan içeriyor.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-136">It contains a field for a custom data string between hello license server and hello application (may be useful for custom app logic) as well as a list of one or more license templates.</span></span>

<span data-ttu-id="7e4f3-137">Bu hello "üst düzey" Merhaba şablonu hiyerarşisindeki sınıftır.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-137">This is hello “top level” class in hello template hierarchy.</span></span> <span data-ttu-id="7e4f3-138">Merhaba yanıt şablonu lisans şablonları listesini içerir ve hello lisans şablonları içerir (doğrudan veya dolaylı olarak) anlamına tüm hello hello şablonu veri toobe seri hale diğer sınıflar.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-138">Meaning that hello response template includes a list of license templates and hello license templates include (directly or indirectly) all of hello other classes that make up hello template data toobe serialized.</span></span>

### <a name="playreadylicensetemplate"></a><span data-ttu-id="7e4f3-139">PlayReadyLicenseTemplate</span><span class="sxs-lookup"><span data-stu-id="7e4f3-139">PlayReadyLicenseTemplate</span></span>
<span data-ttu-id="7e4f3-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) -hello sınıfı, PlayReady lisansları toobe toohello son kullanıcılar döndürülen oluşturmak için bir lisans şablonu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) - hello class represents a license template for creating PlayReady licenses toobe returned toohello end users.</span></span> <span data-ttu-id="7e4f3-141">Hello içerik anahtarı hello lisans hello verilerini içerir ve hakları veya kısıtlamaları toobe tarafından hello PlayReady DRM çalışma zamanı hello içerik anahtarı kullanarak zorunlu tutulur.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-141">It contains hello data on hello content key in hello license and any rights or restrictions toobe enforced by hello PlayReady DRM runtime when using hello content key.</span></span>

### <span data-ttu-id="7e4f3-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span><span class="sxs-lookup"><span data-stu-id="7e4f3-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span></span>
<span data-ttu-id="7e4f3-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) -Bu sınıf hello PlayReady lisans PlayRight temsil eder.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) - This class represents hello PlayRight of a PlayReady license.</span></span> <span data-ttu-id="7e4f3-144">Merhaba içerik konu toohello sıfır veya daha fazla kısıtlama hello lisans ve hello PlayRight kendisini (için kayıttan yürütme belirli bir ilke) yapılandırılmış hello kullanıcı hello özelliği tooplayback verir.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-144">It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions configured in hello license and on hello PlayRight itself (for playback specific policy).</span></span> <span data-ttu-id="7e4f3-145">Merhaba PlayRight hello İlkesi çoğunu toodo hello içerik üzerinden çalınabilir çıkışları hello türlerini denetlemek çıkış kısıtlamaları ve belirli bir çıkış kullanırken yerinde götürüldüğü kısıtlamalar vardır.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-145">Much of hello policy on hello PlayRight has toodo with output restrictions which control hello types of outputs that hello content can be played over and any restrictions that must be put in place when using a given output.</span></span> <span data-ttu-id="7e4f3-146">Örneğin, DRM çalışma zamanı yalnızca hello DigitalVideoOnlyContentRestriction etkin, ardından Merhaba, dijital çıkışları (analog video çıkışına toopass hello içerik izin verilmeyecek) görüntülenen hello video toobe izin verir.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-146">For example, if hello DigitalVideoOnlyContentRestriction is enabled, then hello DRM runtime will only allow hello video toobe displayed over digital outputs (analog video outputs won’t be allowed toopass hello content).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e4f3-147">Bu tür kısıtlamaların çok güçlü olabilir ancak hello tüketici deneyimini de etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-147">These types of restrictions can be very powerful but can also affect hello consumer experience.</span></span> <span data-ttu-id="7e4f3-148">Merhaba çıkışı korumalardan çok kısıtlayıcı olarak yapılandırılırsa, hello içerik bazı istemcilerde unplayable olabilir.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-148">If hello output protections are configured too restrictive, hello content might be unplayable on some clients.</span></span> <span data-ttu-id="7e4f3-149">Daha fazla bilgi için bkz: Merhaba [PlayReady uyumluluk kuralları](https://www.microsoft.com/playready/licensing/compliance/) belge.</span><span class="sxs-lookup"><span data-stu-id="7e4f3-149">For more information, see hello [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>
> 
> 

<span data-ttu-id="7e4f3-150">Silverlight destekler ne koruma düzeyleri örneği için bkz: [çıkışı korumalardan Silverlight desteği](http://go.microsoft.com/fwlink/?LinkId=617318).</span><span class="sxs-lookup"><span data-stu-id="7e4f3-150">For an example of what protection levels Silverlight supports, see: [Silverlight support for output protections](http://go.microsoft.com/fwlink/?LinkId=617318).</span></span>

## <span data-ttu-id="7e4f3-151"><a id="schema"></a>PlayReady lisans şablonu XML Şeması</span><span class="sxs-lookup"><span data-stu-id="7e4f3-151"><a id="schema"></a>PlayReady license template XML schema</span></span>
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



## <a name="media-services-learning-paths"></a><span data-ttu-id="7e4f3-152">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="7e4f3-152">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7e4f3-153">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="7e4f3-153">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

