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
# <a name="diagnosing-errors-with-hello-azure-active-directory-connection-wizard"></a><span data-ttu-id="b5046-103">Hello Azure Active Directory Bağlantı Sihirbazı ile hataları tanılama</span><span class="sxs-lookup"><span data-stu-id="b5046-103">Diagnosing errors with hello Azure Active Directory Connection Wizard</span></span>
<span data-ttu-id="b5046-104">Önceki kimlik doğrulama kodu algılanırken hello Sihirbazı uyumsuz kimlik doğrulama türü algılandı.</span><span class="sxs-lookup"><span data-stu-id="b5046-104">While detecting previous authentication code, hello wizard detected an incompatible authentication type.</span></span>   

## <a name="what-is-being-checked"></a><span data-ttu-id="b5046-105">Ne denetlenen?</span><span class="sxs-lookup"><span data-stu-id="b5046-105">What is being checked?</span></span>
<span data-ttu-id="b5046-106">**Not:** toocorrectly projede önceki kimlik doğrulama kodu algılamak, Merhaba projeyi yeniden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b5046-106">**Note:** toocorrectly detect previous authentication code in a project, hello project must be built.</span></span>  <span data-ttu-id="b5046-107">Bu hata ile karşılaştı ve önceki bir kimlik doğrulama kodu projenizde sahip değilseniz, yeniden oluşturun ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="b5046-107">If you encountered this error and you don't have a previous authentication code in your project, rebuild and try again.</span></span>

### <a name="project-types"></a><span data-ttu-id="b5046-108">Proje türleri</span><span class="sxs-lookup"><span data-stu-id="b5046-108">Project Types</span></span>
<span data-ttu-id="b5046-109">Merhaba Sihirbazı hello projeye hello doğru kimlik doğrulaması mantığı ekleyemezsiniz şekilde geliştirirken projesi hello türünü denetler.</span><span class="sxs-lookup"><span data-stu-id="b5046-109">hello wizard checks hello type of project you’re developing so it can inject hello right authentication logic into hello project.</span></span>  <span data-ttu-id="b5046-110">Türetilen denetleyici ise `ApiController` hello projesinde Webapı proje başlangıç projesi olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="b5046-110">If there is any controller that derives from `ApiController` in hello project, hello project is considered a WebAPI project.</span></span>  <span data-ttu-id="b5046-111">Öğesinden türetilen denetleyicileri varsa `MVC.Controller` hello projesinde MVC projesinde başlangıç projesi olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="b5046-111">If there are only controllers that derive from `MVC.Controller` in hello project, hello project is considered an MVC project.</span></span>  <span data-ttu-id="b5046-112">Başka bir şey hello sihirbaz tarafından desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="b5046-112">Anything else is not supported by hello wizard.</span></span>

### <a name="compatible-authentication-code"></a><span data-ttu-id="b5046-113">Uyumlu kimlik doğrulama kodu</span><span class="sxs-lookup"><span data-stu-id="b5046-113">Compatible Authentication Code</span></span>
<span data-ttu-id="b5046-114">Başlangıç Sihirbazı'nı da önceden hello Sihirbazı ile yapılandırılmış veya hello Sihirbazı ile uyumlu olan kimlik doğrulama ayarlarını denetler.</span><span class="sxs-lookup"><span data-stu-id="b5046-114">hello wizard also checks for authentication settings that have been previously configured with hello wizard or are compatible with hello wizard.</span></span>  <span data-ttu-id="b5046-115">Tüm ayarları varsa, bir a durumu olarak kabul edilir ve hello Sihirbazı açılır hello ayarları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="b5046-115">If all settings are present, it is considered a re-entrant case, and hello wizard opens display hello settings.</span></span>  <span data-ttu-id="b5046-116">Yalnızca bazı hello ayarlarını mevcut bir hata durumu olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="b5046-116">If only some of hello settings are present, it is considered an error case.</span></span>

<span data-ttu-id="b5046-117">MVC projesinde, Başlangıç Sihirbazı'nın önceki kullanımdan sonuç ayarları aşağıdaki hello hiçbirini hello Sihirbazı'nı denetler:</span><span class="sxs-lookup"><span data-stu-id="b5046-117">In an MVC project, hello wizard checks for any of hello following settings, which result from previous use of hello wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

<span data-ttu-id="b5046-118">Ayrıca, herhangi bir hello Sihirbazı'nın önceki kullanımdan neden bir Web API projesi ayarlarında aşağıdaki hello için hello Sihirbazı'nı denetler:</span><span class="sxs-lookup"><span data-stu-id="b5046-118">In addition, hello wizard checks for any of hello following settings in a Web API project, which result from previous use of hello wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a><span data-ttu-id="b5046-119">Uyumsuz kimlik doğrulama kodu</span><span class="sxs-lookup"><span data-stu-id="b5046-119">Incompatible Authentication Code</span></span>
<span data-ttu-id="b5046-120">Son olarak, Başlangıç Sihirbazı'nı toodetect Visual Studio'nun önceki sürümleri ile yapılandırılan kimlik doğrulama kodu sürümlerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="b5046-120">Finally, hello wizard attempts toodetect versions of authentication code that have been configured with previous versions of Visual Studio.</span></span> <span data-ttu-id="b5046-121">Bu hatayı aldıysanız, projenizin bir uyumsuz kimlik doğrulama türünü içeren anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b5046-121">If you received this error, it means your project contains an incompatible authentication type.</span></span> <span data-ttu-id="b5046-122">Merhaba Sihirbazı şu kimlik doğrulama türlerini Visual Studio'nun önceki sürümlerden hello algılar:</span><span class="sxs-lookup"><span data-stu-id="b5046-122">hello wizard detects hello following types of authentication from previous versions of Visual Studio:</span></span>

* <span data-ttu-id="b5046-123">Windows Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="b5046-123">Windows Authentication</span></span> 
* <span data-ttu-id="b5046-124">Bireysel kullanıcı hesapları</span><span class="sxs-lookup"><span data-stu-id="b5046-124">Individual User Accounts</span></span> 
* <span data-ttu-id="b5046-125">Kurumsal hesaplar</span><span class="sxs-lookup"><span data-stu-id="b5046-125">Organizational Accounts</span></span> 

<span data-ttu-id="b5046-126">Windows kimlik doğrulaması toodetect MVC projesinde hello Sihirbazı görünür Merhaba `authentication` öğesinden, **web.config** dosya.</span><span class="sxs-lookup"><span data-stu-id="b5046-126">toodetect Windows Authentication in an MVC project, hello wizard looks for hello `authentication` element from your **web.config** file.</span></span>

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="b5046-127">Windows kimlik doğrulaması toodetect Web API projesinde, Başlangıç Sihirbazı görünür Merhaba `IISExpressWindowsAuthentication` projenizin öğesinden **.csproj** dosyası:</span><span class="sxs-lookup"><span data-stu-id="b5046-127">toodetect Windows Authentication in a Web API project, hello wizard looks for hello `IISExpressWindowsAuthentication` element from your project's **.csproj** file:</span></span>

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

<span data-ttu-id="b5046-128">toodetect bireysel kullanıcı hesapları kimlik doğrulaması, Başlangıç Sihirbazı'nı hello paket öğesinden arar, **Packages.config** dosya.</span><span class="sxs-lookup"><span data-stu-id="b5046-128">toodetect Individual User Accounts authentication, hello wizard looks for hello package element from your **Packages.config** file.</span></span>

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

<span data-ttu-id="b5046-129">toodetect eski tür Kurumsal hesap kimlik doğrulama, Başlangıç Sihirbazı'nı öğesinden aşağıdaki hello arar **web.config**:</span><span class="sxs-lookup"><span data-stu-id="b5046-129">toodetect an old form of Organizational Account authentication, hello wizard looks for hello following element from **web.config**:</span></span>

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="b5046-130">toochange hello kimlik doğrulama türü, hello uyumsuz kimlik doğrulama türünü kaldırmak ve hello Sihirbazı'nı yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b5046-130">toochange hello authentication type, remove hello incompatible authentication type and run hello wizard again.</span></span>

<span data-ttu-id="b5046-131">Daha fazla bilgi için bkz: [Azure AD için kimlik doğrulama senaryoları](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="b5046-131">For more information, see [Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md).</span></span>

#<a name="next-steps"></a><span data-ttu-id="b5046-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b5046-132">Next steps</span></span>
- [<span data-ttu-id="b5046-133">Azure AD için Kimlik Doğrulama Senaryoları</span><span class="sxs-lookup"><span data-stu-id="b5046-133">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)