---
title: "Azure Active Directory Bağlantı Sihirbazı ile hataları tanılama"
description: "Active directory Bağlantı Sihirbazı'nı uyumsuz kimlik doğrulama türü algılandı"
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
ms.openlocfilehash: 4f29f62b2996cae98b02c1ed5fcb59eca09301ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="diagnosing-errors-with-the-azure-active-directory-connection-wizard"></a><span data-ttu-id="27c39-103">Azure Active Directory Bağlantı Sihirbazı ile hataları tanılama</span><span class="sxs-lookup"><span data-stu-id="27c39-103">Diagnosing errors with the Azure Active Directory Connection Wizard</span></span>
<span data-ttu-id="27c39-104">Sihirbaz, önceki kimlik doğrulama kodu algılanırken uyumsuz kimlik doğrulama türü algıladı.</span><span class="sxs-lookup"><span data-stu-id="27c39-104">While detecting previous authentication code, the wizard detected an incompatible authentication type.</span></span>   

## <a name="what-is-being-checked"></a><span data-ttu-id="27c39-105">Ne denetlenen?</span><span class="sxs-lookup"><span data-stu-id="27c39-105">What is being checked?</span></span>
<span data-ttu-id="27c39-106">**Not:** doğru projede önceki kimlik doğrulama kodu algılamak için proje oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="27c39-106">**Note:** To correctly detect previous authentication code in a project, the project must be built.</span></span>  <span data-ttu-id="27c39-107">Bu hata ile karşılaştı ve önceki bir kimlik doğrulama kodu projenizde sahip değilseniz, yeniden oluşturun ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="27c39-107">If you encountered this error and you don't have a previous authentication code in your project, rebuild and try again.</span></span>

### <a name="project-types"></a><span data-ttu-id="27c39-108">Proje türleri</span><span class="sxs-lookup"><span data-stu-id="27c39-108">Project Types</span></span>
<span data-ttu-id="27c39-109">Sihirbaz projeye sağ kimlik doğrulaması mantığı ekleyemezsiniz şekilde geliştirirken projesi türünü denetler.</span><span class="sxs-lookup"><span data-stu-id="27c39-109">The wizard checks the type of project you’re developing so it can inject the right authentication logic into the project.</span></span>  <span data-ttu-id="27c39-110">Türetilen denetleyici ise `ApiController` projede Proje Webapı proje olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="27c39-110">If there is any controller that derives from `ApiController` in the project, the project is considered a WebAPI project.</span></span>  <span data-ttu-id="27c39-111">Öğesinden türetilen denetleyicileri varsa `MVC.Controller` projesinde projeye MVC projesinde olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="27c39-111">If there are only controllers that derive from `MVC.Controller` in the project, the project is considered an MVC project.</span></span>  <span data-ttu-id="27c39-112">Başka bir şey, sihirbaz tarafından desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="27c39-112">Anything else is not supported by the wizard.</span></span>

### <a name="compatible-authentication-code"></a><span data-ttu-id="27c39-113">Uyumlu kimlik doğrulama kodu</span><span class="sxs-lookup"><span data-stu-id="27c39-113">Compatible Authentication Code</span></span>
<span data-ttu-id="27c39-114">Sihirbaz aynı zamanda daha önce Sihirbazı ile yapılandırılmış veya Sihirbazı ile uyumlu olan kimlik doğrulama ayarlarını denetler.</span><span class="sxs-lookup"><span data-stu-id="27c39-114">The wizard also checks for authentication settings that have been previously configured with the wizard or are compatible with the wizard.</span></span>  <span data-ttu-id="27c39-115">Tüm ayarları varsa, içe servis talebi kabul edilir ve Sihirbazı açılır ayarları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="27c39-115">If all settings are present, it is considered a re-entrant case, and the wizard opens display the settings.</span></span>  <span data-ttu-id="27c39-116">Yalnızca bazı ayarlar mevcut bir hata durumu olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="27c39-116">If only some of the settings are present, it is considered an error case.</span></span>

<span data-ttu-id="27c39-117">MVC projesinde, sihirbazın önceki kullanımdan neden aşağıdaki ayarlardan birini Sihirbazı'nı denetler:</span><span class="sxs-lookup"><span data-stu-id="27c39-117">In an MVC project, the wizard checks for any of the following settings, which result from previous use of the wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

<span data-ttu-id="27c39-118">Ayrıca, herhangi bir Web API projesi Sihirbazı'nın önceki kullanımdan sonucunda aşağıdaki ayarları Sihirbazı'nı denetler:</span><span class="sxs-lookup"><span data-stu-id="27c39-118">In addition, the wizard checks for any of the following settings in a Web API project, which result from previous use of the wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a><span data-ttu-id="27c39-119">Uyumsuz kimlik doğrulama kodu</span><span class="sxs-lookup"><span data-stu-id="27c39-119">Incompatible Authentication Code</span></span>
<span data-ttu-id="27c39-120">Son olarak, sihirbaz, Visual Studio'nun önceki sürümleri ile yapılandırılan kimlik doğrulama kodu sürümleri algılamaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="27c39-120">Finally, the wizard attempts to detect versions of authentication code that have been configured with previous versions of Visual Studio.</span></span> <span data-ttu-id="27c39-121">Bu hatayı aldıysanız, projenizin bir uyumsuz kimlik doğrulama türünü içeren anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="27c39-121">If you received this error, it means your project contains an incompatible authentication type.</span></span> <span data-ttu-id="27c39-122">Sihirbaz, Visual Studio'nun önceki sürümleri kimlik doğrulamasını aşağıdaki türlerini algılar:</span><span class="sxs-lookup"><span data-stu-id="27c39-122">The wizard detects the following types of authentication from previous versions of Visual Studio:</span></span>

* <span data-ttu-id="27c39-123">Windows Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="27c39-123">Windows Authentication</span></span> 
* <span data-ttu-id="27c39-124">Bireysel kullanıcı hesapları</span><span class="sxs-lookup"><span data-stu-id="27c39-124">Individual User Accounts</span></span> 
* <span data-ttu-id="27c39-125">Kurumsal hesaplar</span><span class="sxs-lookup"><span data-stu-id="27c39-125">Organizational Accounts</span></span> 

<span data-ttu-id="27c39-126">Sihirbaz Windows kimlik doğrulaması MVC projesinde algılamak için arar `authentication` öğesinden, **web.config** dosya.</span><span class="sxs-lookup"><span data-stu-id="27c39-126">To detect Windows Authentication in an MVC project, the wizard looks for the `authentication` element from your **web.config** file.</span></span>

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="27c39-127">Sihirbaz Windows kimlik doğrulaması Web API projesinde algılamak için arar `IISExpressWindowsAuthentication` projenizin öğesinden **.csproj** dosyası:</span><span class="sxs-lookup"><span data-stu-id="27c39-127">To detect Windows Authentication in a Web API project, the wizard looks for the `IISExpressWindowsAuthentication` element from your project's **.csproj** file:</span></span>

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

<span data-ttu-id="27c39-128">Bireysel kullanıcı hesapları kimlik doğrulaması algılamak için paket öğesinden sihirbaz arar, **Packages.config** dosya.</span><span class="sxs-lookup"><span data-stu-id="27c39-128">To detect Individual User Accounts authentication, the wizard looks for the package element from your **Packages.config** file.</span></span>

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

<span data-ttu-id="27c39-129">Kurumsal hesap kimlik doğrulaması eski bir formu algılamak için aşağıdaki öğeyi sihirbaz arar **web.config**:</span><span class="sxs-lookup"><span data-stu-id="27c39-129">To detect an old form of Organizational Account authentication, the wizard looks for the following element from **web.config**:</span></span>

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="27c39-130">Kimlik doğrulama türünü değiştirmek için uyumsuz kimlik doğrulama türünü kaldırmak ve sihirbazı yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="27c39-130">To change the authentication type, remove the incompatible authentication type and run the wizard again.</span></span>

<span data-ttu-id="27c39-131">Daha fazla bilgi için bkz: [Azure AD için kimlik doğrulama senaryoları](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="27c39-131">For more information, see [Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md).</span></span>

#<a name="next-steps"></a><span data-ttu-id="27c39-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="27c39-132">Next steps</span></span>
- [<span data-ttu-id="27c39-133">Azure AD için Kimlik Doğrulama Senaryoları</span><span class="sxs-lookup"><span data-stu-id="27c39-133">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)