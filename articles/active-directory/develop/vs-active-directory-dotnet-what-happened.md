---
title: "Azure AD ile bağlandığınızda bir MVC projede yapılan değişiklikleri | Microsoft Docs"
description: "Visual Studio bağlı hizmetleri kullanarak Azure AD'ye bağlanma ne olur MVC projenize açıklar"
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
ms.openlocfilehash: 095411a7fc854f4dce11921adb0f57c5389a8e13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-mvc-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="c6167-103">MVC proje için ne (Visual Studio Azure Active Directory bağlı hizmet)?</span><span class="sxs-lookup"><span data-stu-id="c6167-103">What happened to my MVC project (Visual Studio Azure Active Directory connected service)?</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c6167-104">Başlarken</span><span class="sxs-lookup"><span data-stu-id="c6167-104">Getting Started</span></span>](vs-active-directory-dotnet-getting-started.md)
> * [<span data-ttu-id="c6167-105">Ne oldu</span><span class="sxs-lookup"><span data-stu-id="c6167-105">What Happened</span></span>](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="c6167-106">Başvuruları eklendi</span><span class="sxs-lookup"><span data-stu-id="c6167-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="c6167-107">NuGet paket başvuruları</span><span class="sxs-lookup"><span data-stu-id="c6167-107">NuGet package references</span></span>
* <span data-ttu-id="c6167-108">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="c6167-108">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="c6167-109">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="c6167-109">**Microsoft.Owin**</span></span>
* <span data-ttu-id="c6167-110">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="c6167-110">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="c6167-111">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="c6167-111">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="c6167-112">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="c6167-112">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="c6167-113">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="c6167-113">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="c6167-114">**Owın**</span><span class="sxs-lookup"><span data-stu-id="c6167-114">**Owin**</span></span>
* <span data-ttu-id="c6167-115">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="c6167-115">**System.IdentityModel.Tokens.Jwt**</span></span>

### <a name="net-references"></a><span data-ttu-id="c6167-116">.NET başvuruları</span><span class="sxs-lookup"><span data-stu-id="c6167-116">.NET references</span></span>
* <span data-ttu-id="c6167-117">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="c6167-117">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="c6167-118">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="c6167-118">**Microsoft.Owin**</span></span>
* <span data-ttu-id="c6167-119">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="c6167-119">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="c6167-120">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="c6167-120">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="c6167-121">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="c6167-121">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="c6167-122">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="c6167-122">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="c6167-123">**Owın**</span><span class="sxs-lookup"><span data-stu-id="c6167-123">**Owin**</span></span>
* <span data-ttu-id="c6167-124">**System.IdentityModel**</span><span class="sxs-lookup"><span data-stu-id="c6167-124">**System.IdentityModel**</span></span>
* <span data-ttu-id="c6167-125">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="c6167-125">**System.IdentityModel.Tokens.Jwt**</span></span>
* <span data-ttu-id="c6167-126">**System.Runtime.Serialization**</span><span class="sxs-lookup"><span data-stu-id="c6167-126">**System.Runtime.Serialization**</span></span>

## <a name="code-has-been-added"></a><span data-ttu-id="c6167-127">Kod eklendi</span><span class="sxs-lookup"><span data-stu-id="c6167-127">Code has been added</span></span>
### <a name="code-files-were-added-to-your-project"></a><span data-ttu-id="c6167-128">Kod dosyaları projenize eklendi</span><span class="sxs-lookup"><span data-stu-id="c6167-128">Code files were added to your project</span></span>
<span data-ttu-id="c6167-129">Bir kimlik doğrulaması başlangıç sınıfı **App_Start/Startup.Auth.cs** Azure AD kimlik doğrulaması için başlangıç mantığı içeren projenize eklendi.</span><span class="sxs-lookup"><span data-stu-id="c6167-129">An authentication startup class, **App_Start/Startup.Auth.cs** was added to your project containing startup logic for Azure AD authentication.</span></span> <span data-ttu-id="c6167-130">Ayrıca, denetleyici sınıfını, Controllers/AccountController.cs içeren eklendi **SignIn()** ve **SignOut()** yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="c6167-130">Also, a controller class, Controllers/AccountController.cs was added which contains **SignIn()** and **SignOut()** methods.</span></span> <span data-ttu-id="c6167-131">Son olarak, kısmi Görünüm **Views/Shared/_LoginPartial.cshtml** Signın/SignOut için bir eylem bağlantısı içeren eklendi.</span><span class="sxs-lookup"><span data-stu-id="c6167-131">Finally, a partial view, **Views/Shared/_LoginPartial.cshtml** was added containing an action link for SignIn/SignOut.</span></span>

### <a name="startup-code-was-added-to-your-project"></a><span data-ttu-id="c6167-132">Başlangıç kodu projenize eklendi</span><span class="sxs-lookup"><span data-stu-id="c6167-132">Startup code was added to your project</span></span>
<span data-ttu-id="c6167-133">Başlangıç sınıfı projenizde, zaten sahipse **yapılandırma** yöntemi çağrısı içerecek şekilde güncelleştirildi **ConfigureAuth(app)**.</span><span class="sxs-lookup"><span data-stu-id="c6167-133">If you already had a Startup class in your project, the **Configuration** method was updated to include a call to **ConfigureAuth(app)**.</span></span> <span data-ttu-id="c6167-134">Aksi takdirde, başlangıç sınıfı projenize eklendi.</span><span class="sxs-lookup"><span data-stu-id="c6167-134">Otherwise, a Startup class was added to your project.</span></span>

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a><span data-ttu-id="c6167-135">App.config veya web.config yeni yapılandırma değeri var.</span><span class="sxs-lookup"><span data-stu-id="c6167-135">Your app.config or web.config has new configuration values</span></span>
<span data-ttu-id="c6167-136">Aşağıdaki yapılandırma girdileri eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="c6167-136">The following configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientId" value="ClientId from the new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="The selected Azure AD Domain" />
        <add key="ida:TenantId" value="The Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a><span data-ttu-id="c6167-137">Bir Azure Active Directory (AD) uygulama oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="c6167-137">An Azure Active Directory (AD) App was created</span></span>
<span data-ttu-id="c6167-138">Azure AD uygulaması sihirbazda seçtiğiniz dizin oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="c6167-138">An Azure AD Application was created in the directory that you selected in the wizard.</span></span>

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="c6167-139">I işaretlediyseniz *bireysel kullanıcı hesapları kimlik doğrulamasını devre dışı*, proje için ek değişiklikler yapıldı?</span><span class="sxs-lookup"><span data-stu-id="c6167-139">If I checked *disable Individual User Accounts authentication*, what additional changes were made to my project?</span></span>
<span data-ttu-id="c6167-140">NuGet paket referanslarını kaldırıldı ve dosyaları kaldırıldı ve yedeklendi.</span><span class="sxs-lookup"><span data-stu-id="c6167-140">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="c6167-141">Projenizi durumuna bağlı olarak, el ile ek başvurular veya dosyaları kaldırın veya uygun şekilde kodu değiştirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="c6167-141">Depending on the state of your project, you may have to manually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="c6167-142">NuGet paket referanslarını (olanlar için mevcut) kaldırıldı</span><span class="sxs-lookup"><span data-stu-id="c6167-142">NuGet package references removed (for those present)</span></span>
* <span data-ttu-id="c6167-143">**Microsoft.ASPNET.Identity.Core**</span><span class="sxs-lookup"><span data-stu-id="c6167-143">**Microsoft.AspNet.Identity.Core**</span></span>
* <span data-ttu-id="c6167-144">**Microsoft.ASPNET.Identity.entityframework**</span><span class="sxs-lookup"><span data-stu-id="c6167-144">**Microsoft.AspNet.Identity.EntityFramework**</span></span>
* <span data-ttu-id="c6167-145">**Microsoft.ASPNET.Identity.owin**</span><span class="sxs-lookup"><span data-stu-id="c6167-145">**Microsoft.AspNet.Identity.Owin**</span></span>

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="c6167-146">Kod dosyaları yedeklenebilir ve (olanlar için mevcut) kaldırıldı</span><span class="sxs-lookup"><span data-stu-id="c6167-146">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="c6167-147">Aşağıdaki dosyaların her birini yedeklendi ve projesinden kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="c6167-147">Each of following files was backed up and removed from the project.</span></span> <span data-ttu-id="c6167-148">Yedekleme dosyaları, projenin dizin kökündeki 'Yedekleme' klasöründe bulunur.</span><span class="sxs-lookup"><span data-stu-id="c6167-148">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* <span data-ttu-id="c6167-149">**App_Start\IdentityConfig.cs**</span><span class="sxs-lookup"><span data-stu-id="c6167-149">**App_Start\IdentityConfig.cs**</span></span>
* <span data-ttu-id="c6167-150">**Controllers\ManageController.cs**</span><span class="sxs-lookup"><span data-stu-id="c6167-150">**Controllers\ManageController.cs**</span></span>
* <span data-ttu-id="c6167-151">**Models\IdentityModels.cs**</span><span class="sxs-lookup"><span data-stu-id="c6167-151">**Models\IdentityModels.cs**</span></span>
* <span data-ttu-id="c6167-152">**Models\ManageViewModels.cs**</span><span class="sxs-lookup"><span data-stu-id="c6167-152">**Models\ManageViewModels.cs**</span></span>

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="c6167-153">(Olanlar için mevcut) yedeklenen kod dosyaları</span><span class="sxs-lookup"><span data-stu-id="c6167-153">Code files backed up (for those present)</span></span>
<span data-ttu-id="c6167-154">Aşağıdaki dosyaların her birini önce değiştirilen yedeklendi.</span><span class="sxs-lookup"><span data-stu-id="c6167-154">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="c6167-155">Yedekleme dosyaları, projenin dizin kökündeki 'Yedekleme' klasöründe bulunur.</span><span class="sxs-lookup"><span data-stu-id="c6167-155">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* <span data-ttu-id="c6167-156">**Haline**</span><span class="sxs-lookup"><span data-stu-id="c6167-156">**Startup.cs**</span></span>
* <span data-ttu-id="c6167-157">**App_Start\Startup.auth.cs**</span><span class="sxs-lookup"><span data-stu-id="c6167-157">**App_Start\Startup.Auth.cs**</span></span>
* <span data-ttu-id="c6167-158">**Controllers\AccountController.cs**</span><span class="sxs-lookup"><span data-stu-id="c6167-158">**Controllers\AccountController.cs**</span></span>
* <span data-ttu-id="c6167-159">**Görünümler/paylaşılan\_LoginPartial.cshtml**</span><span class="sxs-lookup"><span data-stu-id="c6167-159">**Views\Shared\_LoginPartial.cshtml**</span></span>

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="c6167-160">I işaretlediyseniz *dizin verilerini okuma*, proje için ek değişiklikler yapıldı?</span><span class="sxs-lookup"><span data-stu-id="c6167-160">If I checked *Read directory data*, what additional changes were made to my project?</span></span>
<span data-ttu-id="c6167-161">Ek başvurular eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="c6167-161">Additional references have been added.</span></span>

### <a name="additional-nuget-package-references"></a><span data-ttu-id="c6167-162">Ek NuGet paketi başvurular</span><span class="sxs-lookup"><span data-stu-id="c6167-162">Additional NuGet package references</span></span>
* <span data-ttu-id="c6167-163">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="c6167-163">**EntityFramework**</span></span>
* <span data-ttu-id="c6167-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="c6167-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="c6167-165">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="c6167-165">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="c6167-166">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="c6167-166">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="c6167-167">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="c6167-167">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="c6167-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="c6167-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="c6167-169">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="c6167-169">**System.Spatial**</span></span>

### <a name="additional-net-references"></a><span data-ttu-id="c6167-170">Ek .NET başvurular</span><span class="sxs-lookup"><span data-stu-id="c6167-170">Additional .NET references</span></span>
* <span data-ttu-id="c6167-171">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="c6167-171">**EntityFramework**</span></span>
* <span data-ttu-id="c6167-172">**EntityFramework.SqlServer**</span><span class="sxs-lookup"><span data-stu-id="c6167-172">**EntityFramework.SqlServer**</span></span>
* <span data-ttu-id="c6167-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="c6167-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="c6167-174">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="c6167-174">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="c6167-175">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="c6167-175">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="c6167-176">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="c6167-176">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="c6167-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="c6167-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="c6167-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span><span class="sxs-lookup"><span data-stu-id="c6167-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span></span>
* <span data-ttu-id="c6167-179">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="c6167-179">**System.Spatial**</span></span>

### <a name="additional-code-files-were-added-to-your-project"></a><span data-ttu-id="c6167-180">Ek kod dosyaları projenize eklendi</span><span class="sxs-lookup"><span data-stu-id="c6167-180">Additional Code files were added to your project</span></span>
<span data-ttu-id="c6167-181">Belirteç önbelleğe alma desteklemek için iki dosya eklendi: **Models\ADALTokenCache.cs** ve **Models\ApplicationDbContext.cs**.</span><span class="sxs-lookup"><span data-stu-id="c6167-181">Two files were added to support token caching: **Models\ADALTokenCache.cs** and **Models\ApplicationDbContext.cs**.</span></span>  <span data-ttu-id="c6167-182">Bir ek denetleyici ve görünüm Azure grafik API'leri kullanarak erişen kullanıcı profili bilgilerini göstermek için eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="c6167-182">An additional controller and view were added to illustrate accessing user profile information using Azure graph APIs.</span></span>  <span data-ttu-id="c6167-183">Bu dosyalar **Controllers\UserProfileController.cs** ve **Views\UserProfile\Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="c6167-183">These files are **Controllers\UserProfileController.cs** and **Views\UserProfile\Index.cshtml**.</span></span>

### <a name="additional-startup-code-was-added-to-your-project"></a><span data-ttu-id="c6167-184">Ek başlatma kod projenize eklendi</span><span class="sxs-lookup"><span data-stu-id="c6167-184">Additional Startup code was added to your project</span></span>
<span data-ttu-id="c6167-185">İçinde **startup.auth.cs** dosya, yeni bir **OpenIdConnectAuthenticationNotifications** nesne eklenmiş **bildirimleri** üyesi  **OpenIdConnectAuthenticationOptions**.</span><span class="sxs-lookup"><span data-stu-id="c6167-185">In the **startup.auth.cs** file, a new **OpenIdConnectAuthenticationNotifications** object was added to the **Notifications** member of the **OpenIdConnectAuthenticationOptions**.</span></span>  <span data-ttu-id="c6167-186">Bu OAuth kod alırken ve için bir erişim belirteci değişimi etkinleştirmek için yapılır.</span><span class="sxs-lookup"><span data-stu-id="c6167-186">This is to enable receiving the OAuth code and exchanging it for an access token.</span></span>

### <a name="additional-changes-were-made-to-your-appconfig-or-webconfig"></a><span data-ttu-id="c6167-187">App.config veya web.config için ek değişiklikler yapıldı</span><span class="sxs-lookup"><span data-stu-id="c6167-187">Additional changes were made to your app.config or web.config</span></span>
<span data-ttu-id="c6167-188">Aşağıdaki ek yapılandırma girdileri eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="c6167-188">The following additional configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

<span data-ttu-id="c6167-189">Aşağıdaki yapılandırma bölümlerini ve bağlantı dizesi eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="c6167-189">The following configuration sections and connection string have been added.</span></span>

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


### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="c6167-190">Azure Active Directory uygulamanızı güncelleştirildi</span><span class="sxs-lookup"><span data-stu-id="c6167-190">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="c6167-191">Azure Active Directory uygulamanızı içerecek şekilde güncelleştirildi *dizin verilerini okuma* izni ilave bir anahtar oluşturulduğu ve hangi ardından olarak kullanılan *IDA: ClientSecret* içinde  **Web.config** dosya.</span><span class="sxs-lookup"><span data-stu-id="c6167-191">Your Azure Active Directory App was updated to include the *Read directory data* permission and an additional key was created which was then used as the *ida:ClientSecret* in the **web.config** file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6167-192">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c6167-192">Next steps</span></span>
- [<span data-ttu-id="c6167-193">Azure Active Directory hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="c6167-193">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

