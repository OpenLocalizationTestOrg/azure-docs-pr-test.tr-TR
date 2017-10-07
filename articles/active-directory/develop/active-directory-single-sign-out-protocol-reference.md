---
title: "aaaAzure tek oturum çıkışı SAML Protokolü | Microsoft Docs"
description: "Bu makalede hello Azure Active Directory'de tek Sign-Out SAML Protokolü"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 0e4aa75d-d1ad-4bde-a94c-d8a41fb0abe6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.custom: aaddev
ms.openlocfilehash: 889c9b3397a601c16ba6971d2b15bfee305576de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# Çoklu oturum kapatma SAML Protokolü
Azure Active Directory (Azure AD) destekler hello SAML 2.0 web tarayıcısı tek oturum kapatma profil. Çoklu oturum kapatma toowork için doğru hello **LogoutURL** Merhaba uygulaması açıkça uygulama kaydı sırasında Azure AD ile kaydedilmesi gerekir. Bunlar oturumu kapattınız sonra hello LogoutURL tooredirect kullanıcıları azure AD kullanır.

Bu diyagramda hello Azure AD çoklu oturum kapatma işlemini hello iş akışı gösterilmektedir.

![Çoklu oturum açma iş akışı çıkışı](media/active-directory-single-sign-out-protocol-reference/active-directory-saml-single-sign-out-workflow.png)

## LogoutRequest
Bulut hizmeti gönderir Hello bir `LogoutRequest` ileti tooAzure AD tooindicate bir oturum sonlandırıldı. Merhaba aşağıdaki alıntı gösteren bir örnek `LogoutRequest` öğesi.

```
<samlp:LogoutRequest xmlns="urn:oasis:names:tc:SAML:2.0:metadata" ID="idaa6ebe6839094fe4abc4ebd5281ec780" Version="2.0" IssueInstant="2013-03-28T07:10:49.6004822Z" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.workaad.com</Issuer>
  <NameID xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
</samlp:LogoutRequest>
```

### LogoutRequest
Merhaba `LogoutRequest` gönderilen öğesi tooAzure AD özniteliklerini aşağıdaki hello gerektirir:

* `ID`: Bu hello oturum kapatma isteği tanımlar. Merhaba değerini `ID` bir sayı ile başlamamalıdır. Merhaba tipik uygulamadır tooappend **kimliği** bir GUID toohello dize gösterimi.
* `Version`: Bu öğe hello değerini çok ayarlamak**2.0**. Bu değer gereklidir.
* `IssueInstant`: Bu bir `DateTime` dize koordine Evrensel Saat (UTC) değerine sahip ve [gidiş dönüş biçimi ("o")](https://msdn.microsoft.com/library/az4se3k1.aspx). Azure AD bu türde bir değer Bekliyor, ancak bu zorunlu değildir.

### Veren
Merhaba `Issuer` öğesinde bir `LogoutRequest` hello biri tam olarak eşleşmelidir **ServicePrincipalNames** Azure AD'de hello bulut hizmetindeki. Genellikle, bu toohello ayarlanır **uygulama kimliği URI'si** uygulama kaydı sırasında belirtilir.

### NameID
Merhaba hello değerini `NameID` öğesi hello tam olarak eşleşmelidir `NameID` imzalanmakta çıkışı hello kullanıcı.

## LogoutResponse
Azure AD gönderir bir `LogoutResponse` yanıt tooa içinde `LogoutRequest` öğesi. Merhaba aşağıdaki alıntı gösteren bir örnek `LogoutResponse`.

```
<samlp:LogoutResponse ID="_f0961a83-d071-4be5-a18c-9ae7b22987a4" Version="2.0" IssueInstant="2013-03-18T08:49:24.405Z" InResponseTo="iddce91f96e56747b5ace6d2e2aa9d4f8c" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://sts.windows.net/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
  </samlp:Status>
</samlp:LogoutResponse>
```

### LogoutResponse
Azure AD ayarlar hello `ID`, `Version` ve `IssueInstant` hello değerleri `LogoutResponse` öğesi. Ayrıca hello ayarlar `InResponseTo` hello öğesi toohello değeri `ID` hello özniteliği `LogoutRequest` hello yanıt elicited.

### Veren
Azure AD ayarlar bu değeri çok`https://login.microsoftonline.com/<TenantIdGUID>/` burada <TenantIdGUID> hello Kiracı hello Azure AD Kiracı kimliğidir.

Merhaba tooevaluate hello değeri `Issuer` öğesi, hello kullan hello değeri **uygulama kimliği URI'si** uygulama kaydı sırasında sağlanan.

### Durum
Azure AD kullanır hello `StatusCode` hello öğesinde `Status` öğesi tooindicate hello başarısını veya başarısızlığını oturum kapatma. Merhaba oturum kapatma girişimi başarısız olduğunda, hello `StatusCode` öğesi özel hata iletileri de içerebilir.
