---
title: "yapılan aaaChanges tooa MVC proje tooAzure AD bağlandığınızda | Microsoft Docs"
description: "Visual Studio bağlı hizmetleri kullanarak tooAzure AD connect ne olur tooyour MVC proje açıklar"
services: active-directory
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 8b24adde-547e-4ffe-824a-2029ba210216
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 5e6d4ce5331eacca5fc83429017ae454fadcc8e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-mvc-project-visual-studio-azure-active-directory-connected-service"></a>Ne oldu toomy MVC proje (Visual Studio Azure Active Directory bağlı hizmet)?
> [!div class="op_single_selector"]
> * [Başlarken](vs-active-directory-dotnet-getting-started.md)
> * [Ne oldu](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a>Başvuruları eklendi
### <a name="nuget-package-references"></a>NuGet paket başvuruları
* **Microsoft.IdentityModel.Protocol.Extensions**
* **Microsoft.Owin**
* **Microsoft.Owin.Host.SystemWeb**
* **Microsoft.Owin.Security**
* **Microsoft.Owin.Security.Cookies**
* **Microsoft.Owin.Security.OpenIdConnect**
* **Owın**
* **System.IdentityModel.Tokens.Jwt**

### <a name="net-references"></a>.NET başvuruları
* **Microsoft.IdentityModel.Protocol.Extensions**
* **Microsoft.Owin**
* **Microsoft.Owin.Host.SystemWeb**
* **Microsoft.Owin.Security**
* **Microsoft.Owin.Security.Cookies**
* **Microsoft.Owin.Security.OpenIdConnect**
* **Owın**
* **System.IdentityModel**
* **System.IdentityModel.Tokens.Jwt**
* **System.Runtime.Serialization**

## <a name="code-has-been-added"></a>Kod eklendi
### <a name="code-files-were-added-tooyour-project"></a>Kod dosyaları tooyour projesine eklendi
Bir kimlik doğrulaması başlangıç sınıfı **App_Start/Startup.Auth.cs** Azure AD kimlik doğrulaması için başlangıç mantığı içeren tooyour projesine eklendi. Ayrıca, denetleyici sınıfını, Controllers/AccountController.cs içeren eklendi **SignIn()** ve **SignOut()** yöntemleri. Son olarak, kısmi Görünüm **Views/Shared/_LoginPartial.cshtml** Signın/SignOut için bir eylem bağlantısı içeren eklendi.

### <a name="startup-code-was-added-tooyour-project"></a>Başlangıç kodu tooyour projesine eklendi
Projenizde zaten bir başlangıç sınıfı sahipse hello **yapılandırma** yöntemi olan güncelleştirilmiş tooinclude bir çağrı çok**ConfigureAuth(app)**. Aksi takdirde, başlangıç sınıfı tooyour proje eklendi.

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a>App.config veya web.config yeni yapılandırma değeri var.
Yapılandırma girdileri aşağıdaki hello eklenmiştir.

    <appSettings>
        <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="hello selected Azure AD Domain" />
        <add key="ida:TenantId" value="hello Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a>Bir Azure Active Directory (AD) uygulama oluşturuldu
Azure AD uygulaması hello Sihirbazı'nda seçtiğiniz hello dizin oluşturuldu.

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a>I işaretlediyseniz *bireysel kullanıcı hesapları kimlik doğrulamasını devre dışı*, toomy proje ek değişiklikler yapıldı?
NuGet paket referanslarını kaldırıldı ve dosyaları kaldırıldı ve yedeklendi. Projenizi Hello durumuna bağlı olarak, ek başvurular veya dosyaları kaldırın veya uygun şekilde kodu değiştirmeniz toomanually olabilir.

### <a name="nuget-package-references-removed-for-those-present"></a>NuGet paket referanslarını (olanlar için mevcut) kaldırıldı
* **Microsoft.ASPNET.Identity.Core**
* **Microsoft.ASPNET.Identity.entityframework**
* **Microsoft.ASPNET.Identity.owin**

### <a name="code-files-backed-up-and-removed-for-those-present"></a>Kod dosyaları yedeklenebilir ve (olanlar için mevcut) kaldırıldı
Aşağıdaki dosyaların her birini yedeklendi ve hello projesinden kaldırılmıştır. Yedekleme dosyaları hello kökündeki hello projenin dizininin 'Yedekleme' klasöründe bulunur.

* **App_Start\IdentityConfig.cs**
* **Controllers\ManageController.cs**
* **Models\IdentityModels.cs**
* **Models\ManageViewModels.cs**

### <a name="code-files-backed-up-for-those-present"></a>(Olanlar için mevcut) yedeklenen kod dosyaları
Aşağıdaki dosyaların her birini önce değiştirilen yedeklendi. Yedekleme dosyaları hello kökündeki hello projenin dizininin 'Yedekleme' klasöründe bulunur.

* **Haline**
* **App_Start\Startup.auth.cs**
* **Controllers\AccountController.cs**
* **Görünümler/paylaşılan\_LoginPartial.cshtml**

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a>I işaretlediyseniz *dizin verilerini okuma*, toomy proje ek değişiklikler yapıldı?
Ek başvurular eklenmiştir.

### <a name="additional-nuget-package-references"></a>Ek NuGet paketi başvurular
* **EntityFramework**
* **Microsoft.Azure.ActiveDirectory.GraphClient**
* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.IdentityModel.Clients.ActiveDirectory**
* **System.Spatial**

### <a name="additional-net-references"></a>Ek .NET başvurular
* **EntityFramework**
* **EntityFramework.SqlServer**
* **Microsoft.Azure.ActiveDirectory.GraphClient**
* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.IdentityModel.Clients.ActiveDirectory**
* **Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**
* **System.Spatial**

### <a name="additional-code-files-were-added-tooyour-project"></a>Ek kod dosyaları tooyour projesine eklendi
İki dosya toosupport eklendi belirteç önbelleğe alma: **Models\ADALTokenCache.cs** ve **Models\ApplicationDbContext.cs**.  Bir ek denetleyici ve görünüm Azure grafik API'leri kullanarak kullanıcı profil bilgilerine erişme tooillustrate eklendi.  Bu dosyalar **Controllers\UserProfileController.cs** ve **Views\UserProfile\Index.cshtml**.

### <a name="additional-startup-code-was-added-tooyour-project"></a>Ek başlatma kodunu tooyour projesine eklendi
Merhaba, **startup.auth.cs** dosya, yeni bir **OpenIdConnectAuthenticationNotifications** nesne toohello eklenen **bildirimleri** hello üyesi  **OpenIdConnectAuthenticationOptions**.  Merhaba OAuth kod alırken ve için bir erişim belirteci değişimi tooenable budur.

### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a>Ek değişiklikler tooyour app.config veya web.config yapıldı
Merhaba aşağıdaki ek yapılandırma girdileri eklenmiştir.

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

Merhaba aşağıdaki yapılandırma bölümlerini ve bağlantı dizesi eklenmiştir.

    <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
    </configSections>
    <connectionStrings>
        <add name="DefaultConnection" connectionString="Data Source=(localdb)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\aspnet-[AppName + Generated Id].mdf;Initial Catalog=aspnet-[AppName + Generated Id];Integrated Security=True" providerName="System.Data.SqlClient" />
    </connectionStrings>
    <entityFramework>
        <defaultConnectionFactory type="System.Data.Entity.Infrastructure.LocalDbConnectionFactory, EntityFramework">
          <parameters>
            <parameter value="mssqllocaldb" />
          </parameters>
        </defaultConnectionFactory>
        <providers>
          <provider invariantName="System.Data.SqlClient" type="System.Data.Entity.SqlServer.SqlProviderServices, EntityFramework.SqlServer" />
        </providers>
    </entityFramework>


### <a name="your-azure-active-directory-app-was-updated"></a>Azure Active Directory uygulamanızı güncelleştirildi
Azure Active Directory uygulamanızı güncelleştirilmiş tooinclude hello edildi *dizin verilerini okuma* izni ilave bir anahtar oluşturulduğu ve hangi sonra hello kullanılan *IDA: ClientSecret* hello içinde  **Web.config** dosya.

## <a name="next-steps"></a>Sonraki adımlar
- [Azure Active Directory hakkında daha fazla bilgi edinin](https://azure.microsoft.com/services/active-directory/)

