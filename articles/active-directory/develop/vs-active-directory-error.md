---
title: "aaaHow toodiagnose hatalarla hello Azure Active Directory Bağlantı Sihirbazı"
description: "Merhaba active directory Bağlantı Sihirbazı uyumsuz kimlik doğrulama türü algılandı"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: dd89ea63-4e45-4da1-9642-645b9309670a
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/05/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: f71c5b41457c0c8db05042e8d5f723e58ad11844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnosing-errors-with-hello-azure-active-directory-connection-wizard"></a>Hello Azure Active Directory Bağlantı Sihirbazı ile hataları tanılama
Önceki kimlik doğrulama kodu algılanırken hello Sihirbazı uyumsuz kimlik doğrulama türü algılandı.   

## <a name="what-is-being-checked"></a>Ne denetlenen?
**Not:** toocorrectly projede önceki kimlik doğrulama kodu algılamak, Merhaba projeyi yeniden oluşturulur.  Bu hata ile karşılaştı ve önceki bir kimlik doğrulama kodu projenizde sahip değilseniz, yeniden oluşturun ve yeniden deneyin.

### <a name="project-types"></a>Proje türleri
Merhaba Sihirbazı hello projeye hello doğru kimlik doğrulaması mantığı ekleyemezsiniz şekilde geliştirirken projesi hello türünü denetler.  Türetilen denetleyici ise `ApiController` hello projesinde Webapı proje başlangıç projesi olarak kabul edilir.  Öğesinden türetilen denetleyicileri varsa `MVC.Controller` hello projesinde MVC projesinde başlangıç projesi olarak kabul edilir.  Başka bir şey hello sihirbaz tarafından desteklenmiyor.

### <a name="compatible-authentication-code"></a>Uyumlu kimlik doğrulama kodu
Başlangıç Sihirbazı'nı da önceden hello Sihirbazı ile yapılandırılmış veya hello Sihirbazı ile uyumlu olan kimlik doğrulama ayarlarını denetler.  Tüm ayarları varsa, bir a durumu olarak kabul edilir ve hello Sihirbazı açılır hello ayarları görüntüleyin.  Yalnızca bazı hello ayarlarını mevcut bir hata durumu olarak kabul edilir.

MVC projesinde, Başlangıç Sihirbazı'nın önceki kullanımdan sonuç ayarları aşağıdaki hello hiçbirini hello Sihirbazı'nı denetler:

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

Ayrıca, herhangi bir hello Sihirbazı'nın önceki kullanımdan neden bir Web API projesi ayarlarında aşağıdaki hello için hello Sihirbazı'nı denetler:

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a>Uyumsuz kimlik doğrulama kodu
Son olarak, Başlangıç Sihirbazı'nı toodetect Visual Studio'nun önceki sürümleri ile yapılandırılan kimlik doğrulama kodu sürümlerinde çalışır. Bu hatayı aldıysanız, projenizin bir uyumsuz kimlik doğrulama türünü içeren anlamına gelir. Merhaba Sihirbazı şu kimlik doğrulama türlerini Visual Studio'nun önceki sürümlerden hello algılar:

* Windows Kimlik Doğrulaması 
* Bireysel kullanıcı hesapları 
* Kurumsal hesaplar 

Windows kimlik doğrulaması toodetect MVC projesinde hello Sihirbazı görünür Merhaba `authentication` öğesinden, **web.config** dosya.

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

Windows kimlik doğrulaması toodetect Web API projesinde, Başlangıç Sihirbazı görünür Merhaba `IISExpressWindowsAuthentication` projenizin öğesinden **.csproj** dosyası:

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

toodetect bireysel kullanıcı hesapları kimlik doğrulaması, Başlangıç Sihirbazı'nı hello paket öğesinden arar, **Packages.config** dosya.

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

toodetect eski tür Kurumsal hesap kimlik doğrulama, Başlangıç Sihirbazı'nı öğesinden aşağıdaki hello arar **web.config**:

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

toochange hello kimlik doğrulama türü, hello uyumsuz kimlik doğrulama türünü kaldırmak ve hello Sihirbazı'nı yeniden çalıştırın.

Daha fazla bilgi için bkz: [Azure AD için kimlik doğrulama senaryoları](active-directory-authentication-scenarios.md).

#<a name="next-steps"></a>Sonraki adımlar
- [Azure AD için Kimlik Doğrulama Senaryoları](active-directory-authentication-scenarios.md)