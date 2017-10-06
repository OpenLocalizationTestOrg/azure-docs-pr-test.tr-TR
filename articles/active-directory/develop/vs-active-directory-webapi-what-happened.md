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
# <a name="what-happened-toomy-webapi-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="3d11c-103">Ne oldu toomy Webapı proje (Visual Studio Azure Active Directory bağlı hizmeti)</span><span class="sxs-lookup"><span data-stu-id="3d11c-103">What happened toomy WebApi project (Visual Studio Azure Active Directory connected service)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3d11c-104">Başlarken</span><span class="sxs-lookup"><span data-stu-id="3d11c-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="3d11c-105">Ne oldu</span><span class="sxs-lookup"><span data-stu-id="3d11c-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="3d11c-106">Başvuruları eklendi</span><span class="sxs-lookup"><span data-stu-id="3d11c-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="3d11c-107">NuGet paket başvuruları</span><span class="sxs-lookup"><span data-stu-id="3d11c-107">NuGet package references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a><span data-ttu-id="3d11c-108">.NET başvuruları</span><span class="sxs-lookup"><span data-stu-id="3d11c-108">.NET references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a><span data-ttu-id="3d11c-109">Kod değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="3d11c-109">Code changes</span></span>
### <a name="code-files-were-added-tooyour-project"></a><span data-ttu-id="3d11c-110">Kod dosyaları tooyour projesine eklendi</span><span class="sxs-lookup"><span data-stu-id="3d11c-110">Code files were added tooyour project</span></span>
<span data-ttu-id="3d11c-111">Bir kimlik doğrulaması başlangıç sınıfı **App_Start/Startup.Auth.cs** Azure AD kimlik doğrulaması için başlangıç mantığı içeren tooyour projesine eklendi.</span><span class="sxs-lookup"><span data-stu-id="3d11c-111">An authentication startup class, **App_Start/Startup.Auth.cs** was added tooyour project containing startup logic for Azure AD authentication.</span></span>

### <a name="startup-code-was-added-tooyour-project"></a><span data-ttu-id="3d11c-112">Başlangıç kodu tooyour projesine eklendi</span><span class="sxs-lookup"><span data-stu-id="3d11c-112">Startup code was added tooyour project</span></span>
<span data-ttu-id="3d11c-113">Projenizde zaten bir başlangıç sınıfı sahipse hello **yapılandırma** yöntemi olan güncelleştirilmiş tooinclude bir çağrı çok`ConfigureAuth(app)`.</span><span class="sxs-lookup"><span data-stu-id="3d11c-113">If you already had a Startup class in your project, hello **Configuration** method was updated tooinclude a call too`ConfigureAuth(app)`.</span></span> <span data-ttu-id="3d11c-114">Aksi takdirde, başlangıç sınıfı tooyour proje eklendi.</span><span class="sxs-lookup"><span data-stu-id="3d11c-114">Otherwise, a Startup class was added tooyour project.</span></span>

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a><span data-ttu-id="3d11c-115">App.config veya web.config dosyanızda yeni yapılandırma değeri içeriyor.</span><span class="sxs-lookup"><span data-stu-id="3d11c-115">Your app.config or web.config file has new configuration values.</span></span>
<span data-ttu-id="3d11c-116">Yapılandırma girdileri aşağıdaki hello eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="3d11c-116">hello following configuration entries have been added.</span></span>

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="hello App ID Uri from hello wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a><span data-ttu-id="3d11c-117">Azure AD uygulaması oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="3d11c-117">An Azure AD App was created</span></span>
<span data-ttu-id="3d11c-118">Azure AD uygulaması hello Sihirbazı'nda seçtiğiniz hello dizin oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="3d11c-118">An Azure AD Application was created in hello directory that you selected in hello wizard.</span></span>

[<span data-ttu-id="3d11c-119">Azure Active Directory hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="3d11c-119">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="3d11c-120">I işaretlediyseniz *bireysel kullanıcı hesapları kimlik doğrulamasını devre dışı*, toomy proje ek değişiklikler yapıldı?</span><span class="sxs-lookup"><span data-stu-id="3d11c-120">If I checked *disable Individual User Accounts authentication*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="3d11c-121">NuGet paket referanslarını kaldırıldı ve dosyaları kaldırıldı ve yedeklendi.</span><span class="sxs-lookup"><span data-stu-id="3d11c-121">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="3d11c-122">Projenizi Hello durumuna bağlı olarak, ek başvurular veya dosyaları kaldırın veya uygun şekilde kodu değiştirmeniz toomanually olabilir.</span><span class="sxs-lookup"><span data-stu-id="3d11c-122">Depending on hello state of your project, you may have toomanually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="3d11c-123">NuGet paket referanslarını (olanlar için mevcut) kaldırıldı</span><span class="sxs-lookup"><span data-stu-id="3d11c-123">NuGet package references removed (for those present)</span></span>
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="3d11c-124">Kod dosyaları yedeklenebilir ve (olanlar için mevcut) kaldırıldı</span><span class="sxs-lookup"><span data-stu-id="3d11c-124">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="3d11c-125">Aşağıdaki dosyaların her birini yedeklendi ve hello projesinden kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="3d11c-125">Each of following files was backed up and removed from hello project.</span></span> <span data-ttu-id="3d11c-126">Yedekleme dosyaları hello kökündeki hello projenin dizininin 'Yedekleme' klasöründe bulunur.</span><span class="sxs-lookup"><span data-stu-id="3d11c-126">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="3d11c-127">(Olanlar için mevcut) yedeklenen kod dosyaları</span><span class="sxs-lookup"><span data-stu-id="3d11c-127">Code files backed up (for those present)</span></span>
<span data-ttu-id="3d11c-128">Aşağıdaki dosyaların her birini önce değiştirilen yedeklendi.</span><span class="sxs-lookup"><span data-stu-id="3d11c-128">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="3d11c-129">Yedekleme dosyaları hello kökündeki hello projenin dizininin 'Yedekleme' klasöründe bulunur.</span><span class="sxs-lookup"><span data-stu-id="3d11c-129">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="3d11c-130">I işaretlediyseniz *dizin verilerini okuma*, toomy proje ek değişiklikler yapıldı?</span><span class="sxs-lookup"><span data-stu-id="3d11c-130">If I checked *Read directory data*, what additional changes were made toomy project?</span></span>
### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a><span data-ttu-id="3d11c-131">Ek değişiklikler tooyour app.config veya web.config yapıldı</span><span class="sxs-lookup"><span data-stu-id="3d11c-131">Additional changes were made tooyour app.config or web.config</span></span>
<span data-ttu-id="3d11c-132">Merhaba aşağıdaki ek yapılandırma girdileri eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="3d11c-132">hello following additional configuration entries have been added.</span></span>

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="3d11c-133">Azure Active Directory uygulamanızı güncelleştirildi</span><span class="sxs-lookup"><span data-stu-id="3d11c-133">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="3d11c-134">Azure Active Directory uygulamanızı güncelleştirilmiş tooinclude hello edildi *dizin verilerini okuma* izni ilave bir anahtar oluşturulduğu ve hangi sonra hello kullanılan *IDA: parola* hello içinde `web.config` dosya.</span><span class="sxs-lookup"><span data-stu-id="3d11c-134">Your Azure Active Directory App was updated tooinclude hello *Read directory data* permission and an additional key was created which was then used as hello *ida:Password* in hello `web.config` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d11c-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3d11c-135">Next steps</span></span>
- [<span data-ttu-id="3d11c-136">Azure Active Directory hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="3d11c-136">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

