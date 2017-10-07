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
# <a name="what-happened-toomy-mvc-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="5157b-103">Ne oldu toomy MVC proje (Visual Studio Azure Active Directory bağlı hizmet)?</span><span class="sxs-lookup"><span data-stu-id="5157b-103">What happened toomy MVC project (Visual Studio Azure Active Directory connected service)?</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5157b-104">Başlarken</span><span class="sxs-lookup"><span data-stu-id="5157b-104">Getting Started</span></span>](vs-active-directory-dotnet-getting-started.md)
> * [<span data-ttu-id="5157b-105">Ne oldu</span><span class="sxs-lookup"><span data-stu-id="5157b-105">What Happened</span></span>](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="5157b-106">Başvuruları eklendi</span><span class="sxs-lookup"><span data-stu-id="5157b-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="5157b-107">NuGet paket başvuruları</span><span class="sxs-lookup"><span data-stu-id="5157b-107">NuGet package references</span></span>
* <span data-ttu-id="5157b-108">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="5157b-108">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="5157b-109">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="5157b-109">**Microsoft.Owin**</span></span>
* <span data-ttu-id="5157b-110">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="5157b-110">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="5157b-111">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="5157b-111">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="5157b-112">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="5157b-112">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="5157b-113">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="5157b-113">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="5157b-114">**Owın**</span><span class="sxs-lookup"><span data-stu-id="5157b-114">**Owin**</span></span>
* <span data-ttu-id="5157b-115">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="5157b-115">**System.IdentityModel.Tokens.Jwt**</span></span>

### <a name="net-references"></a><span data-ttu-id="5157b-116">.NET başvuruları</span><span class="sxs-lookup"><span data-stu-id="5157b-116">.NET references</span></span>
* <span data-ttu-id="5157b-117">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="5157b-117">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="5157b-118">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="5157b-118">**Microsoft.Owin**</span></span>
* <span data-ttu-id="5157b-119">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="5157b-119">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="5157b-120">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="5157b-120">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="5157b-121">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="5157b-121">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="5157b-122">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="5157b-122">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="5157b-123">**Owın**</span><span class="sxs-lookup"><span data-stu-id="5157b-123">**Owin**</span></span>
* <span data-ttu-id="5157b-124">**System.IdentityModel**</span><span class="sxs-lookup"><span data-stu-id="5157b-124">**System.IdentityModel**</span></span>
* <span data-ttu-id="5157b-125">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="5157b-125">**System.IdentityModel.Tokens.Jwt**</span></span>
* <span data-ttu-id="5157b-126">**System.Runtime.Serialization**</span><span class="sxs-lookup"><span data-stu-id="5157b-126">**System.Runtime.Serialization**</span></span>

## <a name="code-has-been-added"></a><span data-ttu-id="5157b-127">Kod eklendi</span><span class="sxs-lookup"><span data-stu-id="5157b-127">Code has been added</span></span>
### <a name="code-files-were-added-tooyour-project"></a><span data-ttu-id="5157b-128">Kod dosyaları tooyour projesine eklendi</span><span class="sxs-lookup"><span data-stu-id="5157b-128">Code files were added tooyour project</span></span>
<span data-ttu-id="5157b-129">Bir kimlik doğrulaması başlangıç sınıfı **App_Start/Startup.Auth.cs** Azure AD kimlik doğrulaması için başlangıç mantığı içeren tooyour projesine eklendi.</span><span class="sxs-lookup"><span data-stu-id="5157b-129">An authentication startup class, **App_Start/Startup.Auth.cs** was added tooyour project containing startup logic for Azure AD authentication.</span></span> <span data-ttu-id="5157b-130">Ayrıca, denetleyici sınıfını, Controllers/AccountController.cs içeren eklendi **SignIn()** ve **SignOut()** yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="5157b-130">Also, a controller class, Controllers/AccountController.cs was added which contains **SignIn()** and **SignOut()** methods.</span></span> <span data-ttu-id="5157b-131">Son olarak, kısmi Görünüm **Views/Shared/_LoginPartial.cshtml** Signın/SignOut için bir eylem bağlantısı içeren eklendi.</span><span class="sxs-lookup"><span data-stu-id="5157b-131">Finally, a partial view, **Views/Shared/_LoginPartial.cshtml** was added containing an action link for SignIn/SignOut.</span></span>

### <a name="startup-code-was-added-tooyour-project"></a><span data-ttu-id="5157b-132">Başlangıç kodu tooyour projesine eklendi</span><span class="sxs-lookup"><span data-stu-id="5157b-132">Startup code was added tooyour project</span></span>
<span data-ttu-id="5157b-133">Projenizde zaten bir başlangıç sınıfı sahipse hello **yapılandırma** yöntemi olan güncelleştirilmiş tooinclude bir çağrı çok**ConfigureAuth(app)**.</span><span class="sxs-lookup"><span data-stu-id="5157b-133">If you already had a Startup class in your project, hello **Configuration** method was updated tooinclude a call too**ConfigureAuth(app)**.</span></span> <span data-ttu-id="5157b-134">Aksi takdirde, başlangıç sınıfı tooyour proje eklendi.</span><span class="sxs-lookup"><span data-stu-id="5157b-134">Otherwise, a Startup class was added tooyour project.</span></span>

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a><span data-ttu-id="5157b-135">App.config veya web.config yeni yapılandırma değeri var.</span><span class="sxs-lookup"><span data-stu-id="5157b-135">Your app.config or web.config has new configuration values</span></span>
<span data-ttu-id="5157b-136">Yapılandırma girdileri aşağıdaki hello eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="5157b-136">hello following configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="hello selected Azure AD Domain" />
        <add key="ida:TenantId" value="hello Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a><span data-ttu-id="5157b-137">Bir Azure Active Directory (AD) uygulama oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="5157b-137">An Azure Active Directory (AD) App was created</span></span>
<span data-ttu-id="5157b-138">Azure AD uygulaması hello Sihirbazı'nda seçtiğiniz hello dizin oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="5157b-138">An Azure AD Application was created in hello directory that you selected in hello wizard.</span></span>

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="5157b-139">I işaretlediyseniz *bireysel kullanıcı hesapları kimlik doğrulamasını devre dışı*, toomy proje ek değişiklikler yapıldı?</span><span class="sxs-lookup"><span data-stu-id="5157b-139">If I checked *disable Individual User Accounts authentication*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="5157b-140">NuGet paket referanslarını kaldırıldı ve dosyaları kaldırıldı ve yedeklendi.</span><span class="sxs-lookup"><span data-stu-id="5157b-140">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="5157b-141">Projenizi Hello durumuna bağlı olarak, ek başvurular veya dosyaları kaldırın veya uygun şekilde kodu değiştirmeniz toomanually olabilir.</span><span class="sxs-lookup"><span data-stu-id="5157b-141">Depending on hello state of your project, you may have toomanually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="5157b-142">NuGet paket referanslarını (olanlar için mevcut) kaldırıldı</span><span class="sxs-lookup"><span data-stu-id="5157b-142">NuGet package references removed (for those present)</span></span>
* <span data-ttu-id="5157b-143">**Microsoft.ASPNET.Identity.Core**</span><span class="sxs-lookup"><span data-stu-id="5157b-143">**Microsoft.AspNet.Identity.Core**</span></span>
* <span data-ttu-id="5157b-144">**Microsoft.ASPNET.Identity.entityframework**</span><span class="sxs-lookup"><span data-stu-id="5157b-144">**Microsoft.AspNet.Identity.EntityFramework**</span></span>
* <span data-ttu-id="5157b-145">**Microsoft.ASPNET.Identity.owin**</span><span class="sxs-lookup"><span data-stu-id="5157b-145">**Microsoft.AspNet.Identity.Owin**</span></span>

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="5157b-146">Kod dosyaları yedeklenebilir ve (olanlar için mevcut) kaldırıldı</span><span class="sxs-lookup"><span data-stu-id="5157b-146">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="5157b-147">Aşağıdaki dosyaların her birini yedeklendi ve hello projesinden kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="5157b-147">Each of following files was backed up and removed from hello project.</span></span> <span data-ttu-id="5157b-148">Yedekleme dosyaları hello kökündeki hello projenin dizininin 'Yedekleme' klasöründe bulunur.</span><span class="sxs-lookup"><span data-stu-id="5157b-148">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* <span data-ttu-id="5157b-149">**App_Start\IdentityConfig.cs**</span><span class="sxs-lookup"><span data-stu-id="5157b-149">**App_Start\IdentityConfig.cs**</span></span>
* <span data-ttu-id="5157b-150">**Controllers\ManageController.cs**</span><span class="sxs-lookup"><span data-stu-id="5157b-150">**Controllers\ManageController.cs**</span></span>
* <span data-ttu-id="5157b-151">**Models\IdentityModels.cs**</span><span class="sxs-lookup"><span data-stu-id="5157b-151">**Models\IdentityModels.cs**</span></span>
* <span data-ttu-id="5157b-152">**Models\ManageViewModels.cs**</span><span class="sxs-lookup"><span data-stu-id="5157b-152">**Models\ManageViewModels.cs**</span></span>

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="5157b-153">(Olanlar için mevcut) yedeklenen kod dosyaları</span><span class="sxs-lookup"><span data-stu-id="5157b-153">Code files backed up (for those present)</span></span>
<span data-ttu-id="5157b-154">Aşağıdaki dosyaların her birini önce değiştirilen yedeklendi.</span><span class="sxs-lookup"><span data-stu-id="5157b-154">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="5157b-155">Yedekleme dosyaları hello kökündeki hello projenin dizininin 'Yedekleme' klasöründe bulunur.</span><span class="sxs-lookup"><span data-stu-id="5157b-155">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* <span data-ttu-id="5157b-156">**Haline**</span><span class="sxs-lookup"><span data-stu-id="5157b-156">**Startup.cs**</span></span>
* <span data-ttu-id="5157b-157">**App_Start\Startup.auth.cs**</span><span class="sxs-lookup"><span data-stu-id="5157b-157">**App_Start\Startup.Auth.cs**</span></span>
* <span data-ttu-id="5157b-158">**Controllers\AccountController.cs**</span><span class="sxs-lookup"><span data-stu-id="5157b-158">**Controllers\AccountController.cs**</span></span>
* <span data-ttu-id="5157b-159">**Görünümler/paylaşılan\_LoginPartial.cshtml**</span><span class="sxs-lookup"><span data-stu-id="5157b-159">**Views\Shared\_LoginPartial.cshtml**</span></span>

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="5157b-160">I işaretlediyseniz *dizin verilerini okuma*, toomy proje ek değişiklikler yapıldı?</span><span class="sxs-lookup"><span data-stu-id="5157b-160">If I checked *Read directory data*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="5157b-161">Ek başvurular eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="5157b-161">Additional references have been added.</span></span>

### <a name="additional-nuget-package-references"></a><span data-ttu-id="5157b-162">Ek NuGet paketi başvurular</span><span class="sxs-lookup"><span data-stu-id="5157b-162">Additional NuGet package references</span></span>
* <span data-ttu-id="5157b-163">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="5157b-163">**EntityFramework**</span></span>
* <span data-ttu-id="5157b-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="5157b-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="5157b-165">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="5157b-165">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="5157b-166">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="5157b-166">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="5157b-167">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="5157b-167">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="5157b-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="5157b-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="5157b-169">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="5157b-169">**System.Spatial**</span></span>

### <a name="additional-net-references"></a><span data-ttu-id="5157b-170">Ek .NET başvurular</span><span class="sxs-lookup"><span data-stu-id="5157b-170">Additional .NET references</span></span>
* <span data-ttu-id="5157b-171">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="5157b-171">**EntityFramework**</span></span>
* <span data-ttu-id="5157b-172">**EntityFramework.SqlServer**</span><span class="sxs-lookup"><span data-stu-id="5157b-172">**EntityFramework.SqlServer**</span></span>
* <span data-ttu-id="5157b-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="5157b-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="5157b-174">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="5157b-174">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="5157b-175">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="5157b-175">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="5157b-176">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="5157b-176">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="5157b-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="5157b-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="5157b-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span><span class="sxs-lookup"><span data-stu-id="5157b-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span></span>
* <span data-ttu-id="5157b-179">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="5157b-179">**System.Spatial**</span></span>

### <a name="additional-code-files-were-added-tooyour-project"></a><span data-ttu-id="5157b-180">Ek kod dosyaları tooyour projesine eklendi</span><span class="sxs-lookup"><span data-stu-id="5157b-180">Additional Code files were added tooyour project</span></span>
<span data-ttu-id="5157b-181">İki dosya toosupport eklendi belirteç önbelleğe alma: **Models\ADALTokenCache.cs** ve **Models\ApplicationDbContext.cs**.</span><span class="sxs-lookup"><span data-stu-id="5157b-181">Two files were added toosupport token caching: **Models\ADALTokenCache.cs** and **Models\ApplicationDbContext.cs**.</span></span>  <span data-ttu-id="5157b-182">Bir ek denetleyici ve görünüm Azure grafik API'leri kullanarak kullanıcı profil bilgilerine erişme tooillustrate eklendi.</span><span class="sxs-lookup"><span data-stu-id="5157b-182">An additional controller and view were added tooillustrate accessing user profile information using Azure graph APIs.</span></span>  <span data-ttu-id="5157b-183">Bu dosyalar **Controllers\UserProfileController.cs** ve **Views\UserProfile\Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="5157b-183">These files are **Controllers\UserProfileController.cs** and **Views\UserProfile\Index.cshtml**.</span></span>

### <a name="additional-startup-code-was-added-tooyour-project"></a><span data-ttu-id="5157b-184">Ek başlatma kodunu tooyour projesine eklendi</span><span class="sxs-lookup"><span data-stu-id="5157b-184">Additional Startup code was added tooyour project</span></span>
<span data-ttu-id="5157b-185">Merhaba, **startup.auth.cs** dosya, yeni bir **OpenIdConnectAuthenticationNotifications** nesne toohello eklenen **bildirimleri** hello üyesi  **OpenIdConnectAuthenticationOptions**.</span><span class="sxs-lookup"><span data-stu-id="5157b-185">In hello **startup.auth.cs** file, a new **OpenIdConnectAuthenticationNotifications** object was added toohello **Notifications** member of hello **OpenIdConnectAuthenticationOptions**.</span></span>  <span data-ttu-id="5157b-186">Merhaba OAuth kod alırken ve için bir erişim belirteci değişimi tooenable budur.</span><span class="sxs-lookup"><span data-stu-id="5157b-186">This is tooenable receiving hello OAuth code and exchanging it for an access token.</span></span>

### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a><span data-ttu-id="5157b-187">Ek değişiklikler tooyour app.config veya web.config yapıldı</span><span class="sxs-lookup"><span data-stu-id="5157b-187">Additional changes were made tooyour app.config or web.config</span></span>
<span data-ttu-id="5157b-188">Merhaba aşağıdaki ek yapılandırma girdileri eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="5157b-188">hello following additional configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

<span data-ttu-id="5157b-189">Merhaba aşağıdaki yapılandırma bölümlerini ve bağlantı dizesi eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="5157b-189">hello following configuration sections and connection string have been added.</span></span>

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


### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="5157b-190">Azure Active Directory uygulamanızı güncelleştirildi</span><span class="sxs-lookup"><span data-stu-id="5157b-190">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="5157b-191">Azure Active Directory uygulamanızı güncelleştirilmiş tooinclude hello edildi *dizin verilerini okuma* izni ilave bir anahtar oluşturulduğu ve hangi sonra hello kullanılan *IDA: ClientSecret* hello içinde  **Web.config** dosya.</span><span class="sxs-lookup"><span data-stu-id="5157b-191">Your Azure Active Directory App was updated tooinclude hello *Read directory data* permission and an additional key was created which was then used as hello *ida:ClientSecret* in hello **web.config** file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5157b-192">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5157b-192">Next steps</span></span>
- [<span data-ttu-id="5157b-193">Azure Active Directory hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="5157b-193">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

