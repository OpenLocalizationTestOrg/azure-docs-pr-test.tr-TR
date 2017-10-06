---
title: "tooAzure AD bağlandığınızda yapılan aaaChanges tooa Webapı proje | Microsoft Docs"
description: "Visual Studio kullanarak tooAzure AD connect ne olur tooyour Webapı proje açıklar"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 57630aee-26a2-4326-9dbb-ea2a66daa8b0
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 1ea77b6c75b2dc273219fa6c43f02c7a7c5312ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-webapi-project-visual-studio-azure-active-directory-connected-service"></a>Ne oldu toomy Webapı proje (Visual Studio Azure Active Directory bağlı hizmeti)
> [!div class="op_single_selector"]
> * [Başlarken](vs-active-directory-webapi-getting-started.md)
> * [Ne oldu](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a>Başvuruları eklendi
### <a name="nuget-package-references"></a>NuGet paket başvuruları
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a>.NET başvuruları
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a>Kod değişiklikleri
### <a name="code-files-were-added-tooyour-project"></a>Kod dosyaları tooyour projesine eklendi
Bir kimlik doğrulaması başlangıç sınıfı **App_Start/Startup.Auth.cs** Azure AD kimlik doğrulaması için başlangıç mantığı içeren tooyour projesine eklendi.

### <a name="startup-code-was-added-tooyour-project"></a>Başlangıç kodu tooyour projesine eklendi
Projenizde zaten bir başlangıç sınıfı sahipse hello **yapılandırma** yöntemi olan güncelleştirilmiş tooinclude bir çağrı çok`ConfigureAuth(app)`. Aksi takdirde, başlangıç sınıfı tooyour proje eklendi.

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a>App.config veya web.config dosyanızda yeni yapılandırma değeri içeriyor.
Yapılandırma girdileri aşağıdaki hello eklenmiştir.

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="hello App ID Uri from hello wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a>Azure AD uygulaması oluşturuldu
Azure AD uygulaması hello Sihirbazı'nda seçtiğiniz hello dizin oluşturuldu.

[Azure Active Directory hakkında daha fazla bilgi edinin](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a>I işaretlediyseniz *bireysel kullanıcı hesapları kimlik doğrulamasını devre dışı*, toomy proje ek değişiklikler yapıldı?
NuGet paket referanslarını kaldırıldı ve dosyaları kaldırıldı ve yedeklendi. Projenizi Hello durumuna bağlı olarak, ek başvurular veya dosyaları kaldırın veya uygun şekilde kodu değiştirmeniz toomanually olabilir.

### <a name="nuget-package-references-removed-for-those-present"></a>NuGet paket referanslarını (olanlar için mevcut) kaldırıldı
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a>Kod dosyaları yedeklenebilir ve (olanlar için mevcut) kaldırıldı
Aşağıdaki dosyaların her birini yedeklendi ve hello projesinden kaldırılmıştır. Yedekleme dosyaları hello kökündeki hello projenin dizininin 'Yedekleme' klasöründe bulunur.

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a>(Olanlar için mevcut) yedeklenen kod dosyaları
Aşağıdaki dosyaların her birini önce değiştirilen yedeklendi. Yedekleme dosyaları hello kökündeki hello projenin dizininin 'Yedekleme' klasöründe bulunur.

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a>I işaretlediyseniz *dizin verilerini okuma*, toomy proje ek değişiklikler yapıldı?
### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a>Ek değişiklikler tooyour app.config veya web.config yapıldı
Merhaba aşağıdaki ek yapılandırma girdileri eklenmiştir.

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a>Azure Active Directory uygulamanızı güncelleştirildi
Azure Active Directory uygulamanızı güncelleştirilmiş tooinclude hello edildi *dizin verilerini okuma* izni ilave bir anahtar oluşturulduğu ve hangi sonra hello kullanılan *IDA: parola* hello içinde `web.config` dosya.

## <a name="next-steps"></a>Sonraki adımlar
- [Azure Active Directory hakkında daha fazla bilgi edinin](https://azure.microsoft.com/services/active-directory/)

