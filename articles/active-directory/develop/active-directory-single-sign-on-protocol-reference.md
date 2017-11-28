---
title: "aaaAzure tek oturum üzerinde SAML Protokolü | Microsoft Docs"
description: "Bu makalede Azure Active Directory'de hello üzerinde tek oturum SAML Protokolü"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: ad8437f5-b887-41ff-bd77-779ddafc33fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.custom: aaddev
ms.openlocfilehash: 435cfe0e7be3f2defd34e8b6f6b0f08596ee1f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# Çoklu oturum açma SAML Protokolü
Bu makalede hello SAML 2.0 kimlik doğrulama isteklerini ve Azure Active Directory (Azure AD) için çoklu oturum açmayı destekleyen yanıtları kapsar.

Aşağıdaki Hello Protokolü diyagram oturum açma hello tek sıralamasını açıklar. Merhaba bulut hizmeti (Merhaba hizmet sağlayıcısı) kullanan bir HTTP yeniden yönlendirme bağlama toopass bir `AuthnRequest` (kimlik doğrulama isteği) öğesi tooAzure AD (Merhaba kimlik sağlayıcısı). Ardından Azure AD kullanan bir HTTP post bağlama toopost bir `Response` öğesi toohello bulut hizmeti.

![Çoklu oturum açma iş akışı](media/active-directory-single-sign-on-protocol-reference/active-directory-saml-single-sign-on-workflow.png)

## AuthnRequest
Bulut Hizmetleri toorequest kullanıcı kimlik doğrulaması, gönderme bir `AuthnRequest` öğesi tooAzure AD. Örnek SAML 2.0 `AuthnRequest` şöyle:

```
<samlp:AuthnRequest
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="id6c1c178c166d486687be4aaf5e482730"
Version="2.0" IssueInstant="2013-03-18T03:28:54.1839884Z"
xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.contoso.com</Issuer>
</samlp:AuthnRequest>
```


| Parametre |  | Açıklama |
| --- | --- | --- |
| Kimlik |Gerekli |Azure AD kullanır bu öznitelik toopopulate hello `InResponseTo` özniteliği hello yanıt döndürdü. Ortak bir strateji tooprepend toohello dize gösterimini bir GUID "id" gibi bir dize olacak şekilde kimliği bir rakamla başlayamaz. Örneğin, `id6c1c178c166d486687be4aaf5e482730` geçerli kimliğidir. |
| Sürüm |Gerekli |Bu olmalıdır **2.0**. |
| IssueInstant |Gerekli |Bu, UTC değerine sahip DateTime dizedir ve [gidiş dönüş biçimi ("o")](https://msdn.microsoft.com/library/az4se3k1.aspx). Azure AD bu türde bir DateTime değer bekler ancak değerlendirmek veya hello değerini kullanın. |
| AssertionConsumerServiceUrl |İsteğe bağlı |Sağlanırsa, bu hello eşleşmelidir `RedirectUri` hello bulut hizmetinin Azure AD'de. |
| ForceAuthn |İsteğe bağlı | Bu mantıksal bir değerdir. TRUE, bu hello kullanıcı olacağı zorlanmış toore anlamına gelir,-Azure AD ile geçerli bir oturum olsa bile, kimlik doğrulama. |
| IsPassive |İsteğe bağlı |Azure AD hello kullanıcı sessizce, kullanıcı etkileşimi olmadan varsa hello oturum tanımlama bilgisi kullanarak kimlik doğrulamalıdır olup olmadığını belirten bir Boole değeri budur. True ise, Azure AD tooauthenticate hello kullanıcı hello oturum tanımlama bilgisi kullanarak çalışacaktır. |

Diğer tüm `AuthnRequest` öznitelikleri gibi onay, hedef, AssertionConsumerServiceIndex, AttributeConsumerServiceIndex ve ProviderName **göz ardı**.

Azure AD de hello yoksayar `Conditions` öğesinde `AuthnRequest`.

### Veren
Merhaba `Issuer` öğesinde bir `AuthnRequest` hello biri tam olarak eşleşmelidir **ServicePrincipalNames** Azure AD'de hello bulut hizmetindeki. Genellikle, bu toohello ayarlanır **uygulama kimliği URI'si** uygulama kaydı sırasında belirtilir.

Merhaba içeren bir örnek SAML alıntı `Issuer` öğesi şu şekilde görünür:

```
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.contoso.com</Issuer>
```

### NameIDPolicy
Bu öğe bir belirli ad kimliği biçimi hello yanıt istediğinde ve isteğe bağlı olarak `AuthnRequest` gönderilen öğeleri tooAzure AD.

Bir örnek `NameIdPolicy` öğesi şu şekilde görünür:

```
<NameIDPolicy Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"/>
```

Varsa `NameIDPolicy` , isteğe bağlı içerebilir sağlanmış `Format` özniteliği. Merhaba `Format` öznitelik değerleri aşağıdaki hello yalnızca biri; diğer bir hataya değer olabilir.

* `urn:oasis:names:tc:SAML:2.0:nameid-format:persistent`: Azure Active Directory ikili bir tanımlayıcı olarak hello NameID talebi verir.
* `urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress`: Azure Active Directory e-posta adresi biçiminde hello NameID talebi verir.
* `urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified`: Azure Active Directory tooselect hello talep biçimi bu değer verir. Azure Active Directory hello NameID ikili bir tanımlayıcı olarak verir.
* `urn:oasis:names:tc:SAML:2.0:nameid-format:transient`: Azure Active Directory benzersiz toohello geçerli SSO işlem rastgele oluşturulan bir değer hello NameID talebi verir. Bunun anlamı hello değeri geçicidir ve kullanılan tooidentify hello kullanıcı kimlik doğrulaması yapılamıyor.

Azure AD yoksayar hello `AllowCreate` özniteliği.

### RequestAuthnContext
Merhaba `RequestedAuthnContext` öğesi hello istenen kimlik doğrulama yöntemlerini belirtir. İsteğe bağlı olarak `AuthnRequest` gönderilen öğeleri tooAzure AD. Azure AD destekleyen tek `AuthnContextClassRef` değeri: `urn:oasis:names:tc:SAML:2.0:ac:classes:Password`.

### Kapsamı
Merhaba `Scoping` kimlik sağlayıcıları listesini içeren öğesi, isteğe bağlı olarak `AuthnRequest` gönderilen öğeleri tooAzure AD.

Sağlanırsa, hello içermez `ProxyCount` özniteliği `IDPListOption` veya `RequesterID` öğesi, desteklenmediği gibi.

### İmza
İçermeyen bir `Signature` öğesinde `AuthnRequest` öğeleri, Azure AD desteklemediği oturumu olarak kimlik doğrulama istekleri.

### Konu
Azure AD yoksayar hello `Subject` öğesinin `AuthnRequest` öğeleri.

## Yanıt
Bir istenen oturum açma işlemi başarıyla tamamlandığında, Azure AD yanıt toohello bulut hizmetine gönderir. Örnek yanıt tooa başarılı bir oturum açma girişimi şu şekildedir:

```
<samlp:Response ID="_a4958bfd-e107-4e67-b06d-0d85ade2e76a" Version="2.0" IssueInstant="2013-03-18T07:38:15.144Z" Destination="https://contoso.com/identity/inboundsso.aspx" InResponseTo="id758d0ef385634593a77bdf7e632984b6" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
    ...
  </ds:Signature>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
  </samlp:Status>
  <Assertion ID="_bf9c623d-cc20-407a-9a59-c2d0aee84d12" IssueInstant="2013-03-18T07:38:15.144Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">
    <Issuer>https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      ...
    </ds:Signature>
    <Subject>
      <NameID>Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="id758d0ef385634593a77bdf7e632984b6" NotOnOrAfter="2013-03-18T07:43:15.144Z" Recipient="https://contoso.com/identity/inboundsso.aspx" />
      </SubjectConfirmation>
    </Subject>
    <Conditions NotBefore="2013-03-18T07:38:15.128Z" NotOnOrAfter="2013-03-18T08:48:15.128Z">
      <AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
      </AudienceRestriction>
    </Conditions>
    <AttributeStatement>
      <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
        <AttributeValue>testuser@contoso.com</AttributeValue>
      </Attribute>
      <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
        <AttributeValue>3F2504E0-4F89-11D3-9A0C-0305E82C3301</AttributeValue>
      </Attribute>
      ...
    </AttributeStatement>
    <AuthnStatement AuthnInstant="2013-03-18T07:33:56.000Z" SessionIndex="_bf9c623d-cc20-407a-9a59-c2d0aee84d12">
      <AuthnContext>
        <AuthnContextClassRef> urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
      </AuthnContext>
    </AuthnStatement>
  </Assertion>
</samlp:Response>
```

### Yanıt
Merhaba `Response` öğesi hello yetkilendirme isteği hello sonucunu içerir. Azure AD ayarlar hello `ID`, `Version` ve `IssueInstant` hello değerleri `Response` öğesi. Ayrıca, öznitelikler aşağıdaki hello ayarlar:

* `Destination`: Oturum açma başarıyla tamamlandığında, bu toohello ayarlanır `RedirectUri` hello hizmet sağlayıcısının (bulut hizmeti).
* `InResponseTo`: Bu toohello ayarlanır `ID` hello özniteliği `AuthnRequest` hello yanıt başlatılan öğesi.

### Veren
Azure AD ayarlar hello `Issuer` öğesi çok`https://login.microsoftonline.com/<TenantIDGUID>/` burada <TenantIDGUID> hello Kiracı hello Azure AD Kiracı kimliğidir.

Örneğin, bir örnek yanıt veren öğesiyle şöyle:

```
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
```

### Durum
Merhaba `Status` öğenin ilettiği hello başarılı veya başarısız oturum açma. Merhaba içeren `StatusCode` bir kod veya hello hello isteğinin durumunu temsil eden iç içe geçmiş kodları kümesi içeren öğe. Ayrıca hello içerir `StatusMessage` hello oturum açma işlemi sırasında oluşturulan özel hata iletileri içeren öğe.

<!-- TODO: Add a authentication protocol error reference -->

Merhaba, bir SAML yanıt tooan başarısız oturum açma girişimi aşağıdadır.

```
<samlp:Response ID="_f0961a83-d071-4be5-a18c-9ae7b22987a4" Version="2.0" IssueInstant="2013-03-18T08:49:24.405Z" InResponseTo="iddce91f96e56747b5ace6d2e2aa9d4f8c" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://sts.windows.net/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Requester">
      <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:RequestUnsupported" />
    </samlp:StatusCode>
    <samlp:StatusMessage>AADSTS75006: An error occurred while processing a SAML2 Authentication request. AADSTS90011: hello SAML authentication request property 'NameIdentifierPolicy/SPNameQualifier' is not supported.
Trace ID: 66febed4-e737-49ff-ac23-464ba090d57c
Timestamp: 2013-03-18 08:49:24Z</samlp:StatusMessage>
  </samlp:Status>
```

### onaylama işlemi
Toplama toohello içinde `ID`, `IssueInstant` ve `Version`, Azure AD ayarlar hello öğelerinde aşağıdaki hello `Assertion` hello yanıt öğesidir.

#### Veren
Bu çok ayarlanır`https://sts.windows.net/<TenantIDGUID>/`burada <TenantIDGUID> hello hello Azure AD Kiracı Kiracı kimliği değil.

```
<Issuer>https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
```

#### İmza
Azure AD içinde yanıt tooa başarılı oturum açma hello onaylama imzalar. Merhaba `Signature` öğe hello bulut hizmeti tooauthenticate hello kaynak tooverify hello bütünlüğünü hello onaylama kullanabilirsiniz dijital bir imza içeriyor.

Bu dijital imza, Azure AD kullanır toogenerate hello hello imzalama anahtarında `IDPSSODescriptor` meta veri belgesi öğesidir.

```
<ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      digital_signature_here
    </ds:Signature>
```

#### Konu
Merhaba konu hello onaylama hello deyimlerinin hello asıl belirtir. İçerdiği bir `NameID` hello kimliği doğrulanmış kullanıcıyı temsil eden öğe. Merhaba `NameID` hello belirteci hello kitlesi yönlendirilmiş yalnızca toohello hizmet sağlayıcısı hedeflenen bir tanımlayıcı bir değerdir. Kalıcı - iptal edilebilir, ancak hiçbir zaman atanır. Ayrıca opak, değildir hello kullanıcı hakkında hiçbir şey açığa çıkarmadığınızdan ve öznitelik sorguları için tanımlayıcı olarak kullanılamaz.

Merhaba `Method` hello özniteliği `SubjectConfirmation` öğe her zaman ayarlanmış çok`urn:oasis:names:tc:SAML:2.0:cm:bearer`.

```
<Subject>
      <NameID>Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="id758d0ef385634593a77bdf7e632984b6" NotOnOrAfter="2013-03-18T07:43:15.144Z" Recipient="https://contoso.com/identity/inboundsso.aspx" />
      </SubjectConfirmation>
</Subject>
```

#### Koşullar
Bu öğe SAML onaylar hello kabul edilebilir tanımlayan koşulları kullanın belirtir.

```
<Conditions NotBefore="2013-03-18T07:38:15.128Z" NotOnOrAfter="2013-03-18T08:48:15.128Z">
      <AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
      </AudienceRestriction>
</Conditions>
```

Merhaba `NotBefore` ve `NotOnOrAfter` öznitelikleri sırasında hangi hello onaylama geçerli hello aralığı belirtin.

* Merhaba hello değerini `NotBefore` özniteliktir eşit tooor biraz (saniyeden az) hello değerinden daha sonra `IssueInstant` hello özniteliği `Assertion` öğesi. Azure AD kendisi ve hello arasındaki zaman farklılığı hesabı olmayan bulut hizmeti (hizmet sağlayıcısı) ve tüm arabellek toothis süresini eklemez.
* Merhaba hello değerini `NotOnOrAfter` hello hello değerinden daha sonra 70 dakikada bir özniteliktir `NotBefore` özniteliği.

#### Hedef kitle
Bu, bir hedef kitle tanımlayan bir URI içeriyor. Azure AD ayarlar bu öğe toohello değerinin hello değerini `Issuer` hello öğesinin `AuthnRequest` , başlatılan hello oturum açma. tooevaluate hello `Audience` değeri, hello hello değerini kullanın `App ID URI` uygulama kaydı sırasında belirtildi.

```
<AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
</AudienceRestriction>
```

Hello gibi `Issuer` hello değerini `Audience` değeri tam olarak eşleşmelidir Azure AD'de hello bulut hizmeti temsil eden hello hizmet asıl adlarından biri. Ancak, hello değeri Merhaba, `Issuer` öğesi değil bir URI değeri hello `Audience` değerdir hello yanıt hello `Issuer` değeri önekiyle `spn:`.

#### AttributeStatement
Merhaba konu veya kullanıcı hakkında talepleri içerir. Merhaba aşağıdaki alıntı içeren bir örnek `AttributeStatement` öğesi. Bu hello öğesi birden çok öznitelikleri ve öznitelik değerleri içerebilir Hello üç nokta gösterir.

```
<AttributeStatement>
      <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
        <AttributeValue>testuser@contoso.com</AttributeValue>
      </Attribute>
      <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
        <AttributeValue>3F2504E0-4F89-11D3-9A0C-0305E82C3301</AttributeValue>
      </Attribute>
      ...
</AttributeStatement>
```        

* **Ad talep** : Merhaba hello değerini `Name` özniteliği (`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`) hello kimliği doğrulanmış hello kullanıcının kullanıcı asıl adı olduğu gibi `testuser@managedtenant.com`.
* **Objectıdentifier talep** : Merhaba hello değerini `ObjectIdentifier` özniteliği (`http://schemas.microsoft.com/identity/claims/objectidentifier`) hello olduğu `ObjectId` hello temsil eden hello dizin nesnesi Azure AD'de kullanıcı kimlik doğrulaması. `ObjectId`bir, genel benzersiz sabittir ve hello güvenli tanıtıcısı yeniden kullanım kullanıcı kimliği.

#### AuthnStatement
Bu öğe, belirli bir yöntem belirli bir zamandaki o hello onaylama konu doğrulandı onaylar.

* Merhaba `AuthnInstant` özniteliği, Azure AD ile kimlik doğrulaması hangi hello kullanıcının hello zaman belirtir.
* Merhaba `AuthnContext` öğesi belirttiğinden hello kimlik doğrulaması bağlamı kullanılan tooauthenticate hello kullanıcı.

```
<AuthnStatement AuthnInstant="2013-03-18T07:33:56.000Z" SessionIndex="_bf9c623d-cc20-407a-9a59-c2d0aee84d12">
      <AuthnContext>
        <AuthnContextClassRef> urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
      </AuthnContext>
</AuthnStatement>
```