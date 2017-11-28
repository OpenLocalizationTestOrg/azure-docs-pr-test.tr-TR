---
title: "Azure Active Directory B2C: Kullanım hello grafik API'si | Microsoft Docs"
description: "Nasıl toocall hello grafik API'si bir B2C Kiracı için bir uygulama kimliği tooautomate hello işlemi kullanarak."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f9904516-d9f7-43b1-ae4f-e4d9eb1c67a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: parakhj
ms.openlocfilehash: a17cdc4adf57dbf22592d99ef8ecde41652763fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-use-hello-graph-api"></a><span data-ttu-id="eba8c-103">Azure AD B2C: hello grafik API'sini kullanın</span><span class="sxs-lookup"><span data-stu-id="eba8c-103">Azure AD B2C: Use hello Graph API</span></span>
<span data-ttu-id="eba8c-104">Azure Active Directory (Azure AD) B2C kiracılar toobe çok büyük eğilimlidir.</span><span class="sxs-lookup"><span data-stu-id="eba8c-104">Azure Active Directory (Azure AD) B2C tenants tend toobe very large.</span></span> <span data-ttu-id="eba8c-105">Bu, birçok genel kiracı yönetim görevlerini programlı olarak gerçekleştirilen toobe gerektiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="eba8c-105">This means that many common tenant management tasks need toobe performed programmatically.</span></span> <span data-ttu-id="eba8c-106">Kullanıcı Yönetimi buna birincil bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="eba8c-106">A primary example is user management.</span></span> <span data-ttu-id="eba8c-107">Mevcut bir kullanıcı deposu tooa B2C Kiracı toomigrate gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="eba8c-107">You might need toomigrate an existing user store tooa B2C tenant.</span></span> <span data-ttu-id="eba8c-108">Kendi sayfasında toohost kullanıcı kaydı istediğiniz ve hello perde arkasında Azure AD B2C dizininizde kullanıcı hesapları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="eba8c-108">You may want toohost user registration on your own page and create user accounts in your Azure AD B2C directory behind hello scenes.</span></span> <span data-ttu-id="eba8c-109">Bu tür bir görev hello özelliği toocreate, okuma, güncelleştirme gerektiren ve kullanıcı hesaplarını silin.</span><span class="sxs-lookup"><span data-stu-id="eba8c-109">These types of tasks require hello ability toocreate, read, update, and delete user accounts.</span></span> <span data-ttu-id="eba8c-110">Bu görevleri hello Azure AD Graph API kullanarak yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eba8c-110">You can do these tasks by using hello Azure AD Graph API.</span></span>

<span data-ttu-id="eba8c-111">B2C kiracılar için hello grafik API'si ile iletişim iki birincil modu mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="eba8c-111">For B2C tenants, there are two primary modes of communicating with hello Graph API.</span></span>

* <span data-ttu-id="eba8c-112">Merhaba görevleri gerçekleştirdiğinizde etkileşimli, bir kez çalıştır görevler için bir yönetici hesabı hello B2C Kiracı olarak işlem yapmalıdır.</span><span class="sxs-lookup"><span data-stu-id="eba8c-112">For interactive, run-once tasks, you should act as an administrator account in hello B2C tenant when you perform hello tasks.</span></span> <span data-ttu-id="eba8c-113">Yöneticinin tüm çağrıları toohello grafik API'si gerçekleştirmeden önce bu modu yönetici toosign kimlik bilgilerinizle gerektirir.</span><span class="sxs-lookup"><span data-stu-id="eba8c-113">This mode requires an administrator toosign in with credentials before that admin can perform any calls toohello Graph API.</span></span>
* <span data-ttu-id="eba8c-114">Otomatik, sürekli görevleri için bazı türünü sağladığınız hizmet hesabının hello gerekli ayrıcalıklara tooperform yönetim görevleri ile kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="eba8c-114">For automated, continuous tasks, you should use some type of service account that you provide with hello necessary privileges tooperform management tasks.</span></span> <span data-ttu-id="eba8c-115">Azure AD'de bu uygulama kaydetme ve tooAzure AD kimlik doğrulaması yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eba8c-115">In Azure AD, you can do this by registering an application and authenticating tooAzure AD.</span></span> <span data-ttu-id="eba8c-116">Bu kullanılarak yapılır bir **uygulama kimliği** hello kullanan [OAuth 2.0 istemci kimlik bilgileri vermenizi](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="eba8c-116">This is done by using an **Application ID** that uses hello [OAuth 2.0 client credentials grant](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span></span> <span data-ttu-id="eba8c-117">Bu durumda, hello uygulama bir kullanıcı olarak değil kendisini toocall hello grafik API'si görür.</span><span class="sxs-lookup"><span data-stu-id="eba8c-117">In this case, hello application acts as itself, not as a user, toocall hello Graph API.</span></span>

<span data-ttu-id="eba8c-118">Bu makalede, sizi nasıl tooperform hello otomatik kullanım örneği ele alacağız.</span><span class="sxs-lookup"><span data-stu-id="eba8c-118">In this article, we'll discuss how tooperform hello automated-use case.</span></span> <span data-ttu-id="eba8c-119">toodemonstrate, biz yapı .NET 4.5 `B2CGraphClient` gerçekleştiren kullanıcı oluşturma, okuma, güncelleştirme ve Sil (CRUD) işlemleridir.</span><span class="sxs-lookup"><span data-stu-id="eba8c-119">toodemonstrate, we'll build a .NET 4.5 `B2CGraphClient` that performs user create, read, update, and delete (CRUD) operations.</span></span> <span data-ttu-id="eba8c-120">Merhaba istemci bir Windows komut satırı tooinvoke sağlayan arabirimi (CLI) çeşitli yöntemlerle sahip olur.</span><span class="sxs-lookup"><span data-stu-id="eba8c-120">hello client will have a Windows command-line interface (CLI) that allows you tooinvoke various methods.</span></span> <span data-ttu-id="eba8c-121">Ancak, hello kodu toobehave etkileşimsiz, otomatik bir şekilde yazılır.</span><span class="sxs-lookup"><span data-stu-id="eba8c-121">However, hello code is written toobehave in a noninteractive, automated fashion.</span></span>

## <a name="get-an-azure-ad-b2c-tenant"></a><span data-ttu-id="eba8c-122">Bir Azure AD B2C kiracısı edinme</span><span class="sxs-lookup"><span data-stu-id="eba8c-122">Get an Azure AD B2C tenant</span></span>
<span data-ttu-id="eba8c-123">Uygulama veya kullanıcıların oluşturabilir veya Azure AD ile etkileşimde önce Azure AD B2C kiracısı ve hello kiracısında genel yönetici hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="eba8c-123">Before you can create applications or users, or interact with Azure AD at all, you will need an Azure AD B2C tenant and a global administrator account in hello tenant.</span></span> <span data-ttu-id="eba8c-124">Zaten bir kiracı yoksa [Azure AD B2C ile çalışmaya başlama](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="eba8c-124">If you don't have a tenant already, [get started with Azure AD B2C](active-directory-b2c-get-started.md).</span></span>

## <a name="register-your-application-in-your-tenant"></a><span data-ttu-id="eba8c-125">Kiracınızda uygulamanızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="eba8c-125">Register your application in your tenant</span></span>
<span data-ttu-id="eba8c-126">B2C Kiracı aldıktan sonra hello aracılığıyla uygulamanızı tooregister gerek [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="eba8c-126">After you have a B2C tenant, you need tooregister your application via hello [Azure Portal](https://portal.azure.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eba8c-127">toouse hello grafik API'si B2C kiracınızın ile Merhaba genel kullanarak tooregister adanmış bir uygulama gerekiyor *uygulama kayıtlar* dikey penceresinde hello Azure Portal, **değil** Azure AD B2C'in  *Uygulamaları* dikey.</span><span class="sxs-lookup"><span data-stu-id="eba8c-127">toouse hello Graph API with your B2C tenant, you will need tooregister a dedicated application by using hello generic *App Registrations* blade in hello Azure Portal, **NOT** Azure AD B2C's *Applications* blade.</span></span> <span data-ttu-id="eba8c-128">Hello Azure AD B2C'ın kayıtlı hello zaten varolan B2C uygulamaları tekrar kullanamazsınız *uygulamaları* dikey.</span><span class="sxs-lookup"><span data-stu-id="eba8c-128">You can't reuse hello already-existing B2C applications that you registered in hello Azure AD B2C's *Applications* blade.</span></span>

1. <span data-ttu-id="eba8c-129">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="eba8c-129">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="eba8c-130">Azure AD B2C kiracınızın hello sağ üst köşedeki hello sayfasının hesabınızı seçerek belirleyin.</span><span class="sxs-lookup"><span data-stu-id="eba8c-130">Choose your Azure AD B2C tenant by selecting your account in hello top right corner of hello page.</span></span>
3. <span data-ttu-id="eba8c-131">Merhaba sol gezinti bölmesinde seçin **daha Hizmetleri**, tıklatın **uygulama kayıtlar**, tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="eba8c-131">In hello left-hand navigation pane, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
4. <span data-ttu-id="eba8c-132">Merhaba komut istemlerini izleyin ve yeni bir uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="eba8c-132">Follow hello prompts and create a new application.</span></span> 
    1. <span data-ttu-id="eba8c-133">Seçin **Web uygulaması / API** uygulama türü hello gibi.</span><span class="sxs-lookup"><span data-stu-id="eba8c-133">Select **Web App / API** as hello Application Type.</span></span>    
    2. <span data-ttu-id="eba8c-134">Sağlamak **URI herhangi bir yeniden yönlendirme** (örneğin https://B2CGraphAPI) Bu örnek için uygun değil olarak.</span><span class="sxs-lookup"><span data-stu-id="eba8c-134">Provide **any redirect URI** (e.g. https://B2CGraphAPI) as it's not relevant for this example.</span></span>  
5. <span data-ttu-id="eba8c-135">Merhaba uygulama şimdi yukarı uygulamaları hello listesinde göster üzerinde tooobtain hello **uygulama kimliği** (istemci kimliği olarak da bilinir).</span><span class="sxs-lookup"><span data-stu-id="eba8c-135">hello application will now show up in hello list of applications, click on it tooobtain hello **Application ID** (also known as Client ID).</span></span> <span data-ttu-id="eba8c-136">Bir sonraki bölümde gereksinim duyacağınız kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="eba8c-136">Copy it as you'll need it in a later section.</span></span>
6. <span data-ttu-id="eba8c-137">Merhaba ayarlar dikey penceresinde tıklayın **anahtarları** ve yeni bir anahtar (istemci gizli anahtarı olarak da bilinir) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="eba8c-137">In hello Settings blade, click on **Keys** and add a new key (also known as client secret).</span></span> <span data-ttu-id="eba8c-138">Ayrıca daha sonraki bir bölüme kullanmak için kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="eba8c-138">Also copy it for use in a later section.</span></span>

## <a name="configure-create-read-and-update-permissions-for-your-application"></a><span data-ttu-id="eba8c-139">Yapılandırma oluşturmak, okumak ve güncelleştirmek, uygulamanız için izinler</span><span class="sxs-lookup"><span data-stu-id="eba8c-139">Configure create, read and update permissions for your application</span></span>
<span data-ttu-id="eba8c-140">Tooconfigure gereksinim artık tüm Merhaba, uygulama tooget izinleri toocreate gerekli, okuma, güncelleştirme ve kullanıcıları silme.</span><span class="sxs-lookup"><span data-stu-id="eba8c-140">Now you need tooconfigure your application tooget all hello required permissions toocreate, read, update and delete users.</span></span>

1. <span data-ttu-id="eba8c-141">İçinde etmeden Azure portal'ın uygulama kayıtlar dikey Merhaba, uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="eba8c-141">Continuing in hello Azure portal's App Registrations blade, select your application.</span></span>
2. <span data-ttu-id="eba8c-142">Merhaba ayarlar dikey penceresinde tıklayın **gerekli izinleri**.</span><span class="sxs-lookup"><span data-stu-id="eba8c-142">In hello Settings blade, click on **Required permissions**.</span></span>
3. <span data-ttu-id="eba8c-143">Merhaba gerekli izinleri dikey penceresinde tıklayın **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="eba8c-143">In hello Required permissions blade, click on **Windows Azure Active Directory**.</span></span>
4. <span data-ttu-id="eba8c-144">Merhaba erişimi etkinleştir dikey penceresinde hello seçin **dizin verilerini okuma ve yazma** iznini **uygulama izinleri** tıklatıp **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="eba8c-144">In hello Enable Access  blade, select hello **Read and write directory data** permission from **Application Permissions** and click **Save**.</span></span>
5. <span data-ttu-id="eba8c-145">Son olarak, geri hello gerekli izinleri dikey penceresinde hello üzerinde tıklayın **izinler** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="eba8c-145">Finally, back in hello Required permissions blade, click on hello **Grant Permissions** button.</span></span>

<span data-ttu-id="eba8c-146">B2C kiracınızın izin toocreate, okuma ve güncelleştirme kullanıcıları olan bir uygulama artık sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="eba8c-146">You now have an application that has permission toocreate, read and update users from your B2C tenant.</span></span>

## <a name="configure-delete-permissions-for-your-application"></a><span data-ttu-id="eba8c-147">Uygulamanız için silme izinleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="eba8c-147">Configure delete permissions for your application</span></span>
<span data-ttu-id="eba8c-148">Şu anda hello *dizin verilerini okuma ve yazma* izin vermez **değil** hello özelliği toodo kullanıcıları silme gibi tüm silme işlemleri içerir.</span><span class="sxs-lookup"><span data-stu-id="eba8c-148">Currently, hello *Read and write directory data* permission does **NOT** include hello ability toodo any deletions such as deleting users.</span></span> <span data-ttu-id="eba8c-149">Uygulama hello özelliği toodelete kullanıcılarınızın toogive istiyorsanız, PowerShell ile ilgili aşağıdaki ek adımları toodo gerekir, aksi takdirde, toohello sonraki bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eba8c-149">If you want toogive your application hello ability toodelete users, you'll need toodo these extra steps that involve PowerShell, otherwise, you can skip toohello next section.</span></span>

<span data-ttu-id="eba8c-150">İlk olarak, karşıdan yüklenip hello [Microsoft Online Services oturum açma Yardımcısı](http://go.microsoft.com/fwlink/?LinkID=286152).</span><span class="sxs-lookup"><span data-stu-id="eba8c-150">First, download and install hello [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span> <span data-ttu-id="eba8c-151">Ardından yükleyip hello [64-bit Windows PowerShell için Azure Active Directory Modülü](http://go.microsoft.com/fwlink/p/?linkid=236297).</span><span class="sxs-lookup"><span data-stu-id="eba8c-151">Then download and install hello [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>

<span data-ttu-id="eba8c-152">Merhaba PowerShell modülü yükledikten sonra PowerShell'i açın ve tooyour B2C Kiracı bağlanın.</span><span class="sxs-lookup"><span data-stu-id="eba8c-152">After you install hello PowerShell module, open PowerShell and connect tooyour B2C tenant.</span></span> <span data-ttu-id="eba8c-153">Çalıştırdıktan sonra `Get-Credential`, bir kullanıcı adı ve parola, hello kullanıcı adını girin ve B2C Kiracı yönetici hesabınızın parolası istenir.</span><span class="sxs-lookup"><span data-stu-id="eba8c-153">After you run `Get-Credential`, you will be prompted for a user name and password, Enter hello user name and password of your B2C tenant administrator account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eba8c-154">İhtiyacınız olan toouse bir B2C Kiracı yönetici hesabı **yerel** toohello B2C Kiracı.</span><span class="sxs-lookup"><span data-stu-id="eba8c-154">You need toouse a B2C tenant administrator account that is **local** toohello B2C tenant.</span></span> <span data-ttu-id="eba8c-155">Bu hesapları şuna: myusername@myb2ctenant.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="eba8c-155">These accounts look like this: myusername@myb2ctenant.onmicrosoft.com.</span></span>

```powershell
Connect-MsolService
```

<span data-ttu-id="eba8c-156">Merhaba kullanacağız artık **uygulama kimliği** toodelete kullanıcılar olanak tanıyan tooassign hello uygulama hello kullanıcı hesabı yönetici rolü aşağıdaki hello komut.</span><span class="sxs-lookup"><span data-stu-id="eba8c-156">Now we'll use hello **Application ID** in hello script below tooassign hello application hello user account administrator role which will allow it toodelete users.</span></span> <span data-ttu-id="eba8c-157">Bu roller, iyi bilinen tanımlayıcıları vardır, yani tüm toodo ihtiyacınız giriş, **uygulama kimliği** hello komut dosyasında aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="eba8c-157">These roles have well-known identifiers, so all you need toodo is input your **Application ID** in hello script below.</span></span>

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

<span data-ttu-id="eba8c-158">Uygulamanızı şimdi izinleri toodelete B2C kiracınızın kullanıcılardan de vardır.</span><span class="sxs-lookup"><span data-stu-id="eba8c-158">Your application now also has permissions toodelete users from your B2C tenant.</span></span>

## <a name="download-configure-and-build-hello-sample-code"></a><span data-ttu-id="eba8c-159">Karşıdan yükleme, yapılandırma ve hello örnek kodu derleme</span><span class="sxs-lookup"><span data-stu-id="eba8c-159">Download, configure, and build hello sample code</span></span>
<span data-ttu-id="eba8c-160">İlk olarak, hello örnek kodu indirin ve çalışmasını alın.</span><span class="sxs-lookup"><span data-stu-id="eba8c-160">First, download hello sample code and get it running.</span></span> <span data-ttu-id="eba8c-161">Ardından biz yakından bakmak sürer.</span><span class="sxs-lookup"><span data-stu-id="eba8c-161">Then we will take a closer look at it.</span></span>  <span data-ttu-id="eba8c-162">Yapabilecekleriniz [hello örnek kod bir .zip dosyası olarak karşıdan](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="eba8c-162">You can [download hello sample code as a .zip file](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span></span> <span data-ttu-id="eba8c-163">Ayrıca tercih ettiğiniz dizinine kopyalayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="eba8c-163">You can also clone it into a directory of your choice:</span></span>

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

<span data-ttu-id="eba8c-164">Açık hello `B2CGraphClient\B2CGraphClient.sln` Visual Studio çözümü Visual Studio'da.</span><span class="sxs-lookup"><span data-stu-id="eba8c-164">Open hello `B2CGraphClient\B2CGraphClient.sln` Visual Studio solution in Visual Studio.</span></span> <span data-ttu-id="eba8c-165">Merhaba, `B2CGraphClient` proje, açık hello dosya `App.config`.</span><span class="sxs-lookup"><span data-stu-id="eba8c-165">In hello `B2CGraphClient` project, open hello file `App.config`.</span></span> <span data-ttu-id="eba8c-166">Merhaba üç uygulama ayarlarını kendi değerlerinizle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="eba8c-166">Replace hello three app settings with your own values:</span></span>

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{hello ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{hello Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="eba8c-167">Ardından, hello üzerinde sağ `B2CGraphClient` hello örnek çözümü ve yeniden oluşturma.</span><span class="sxs-lookup"><span data-stu-id="eba8c-167">Next, right-click on hello `B2CGraphClient` solution and rebuild hello sample.</span></span> <span data-ttu-id="eba8c-168">Başarılı olursa, şimdi olmalıdır bir `B2C.exe` içinde bulunan yürütülebilir dosyasını `B2CGraphClient\bin\Debug`.</span><span class="sxs-lookup"><span data-stu-id="eba8c-168">If you are successful, you should now have a `B2C.exe` executable file located in `B2CGraphClient\bin\Debug`.</span></span>

## <a name="build-user-crud-operations-by-using-hello-graph-api"></a><span data-ttu-id="eba8c-169">Kullanıcı CRUD işlemleri hello grafik API'sini kullanarak oluşturma</span><span class="sxs-lookup"><span data-stu-id="eba8c-169">Build user CRUD operations by using hello Graph API</span></span>
<span data-ttu-id="eba8c-170">toouse hello B2CGraphClient, açık bir `cmd` Windows komut istemine ve dizin toohello değiştirmek `Debug` dizin.</span><span class="sxs-lookup"><span data-stu-id="eba8c-170">toouse hello B2CGraphClient, open a `cmd` Windows command prompt and change your directory toohello `Debug` directory.</span></span> <span data-ttu-id="eba8c-171">Merhaba çalıştırmak `B2C Help` komutu.</span><span class="sxs-lookup"><span data-stu-id="eba8c-171">Then run hello `B2C Help` command.</span></span>

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

<span data-ttu-id="eba8c-172">Bu her komut kısa bir açıklamasını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="eba8c-172">This will display a brief description of each command.</span></span> <span data-ttu-id="eba8c-173">Aşağıdaki komutlardan birini çağırma her zaman `B2CGraphClient` isteği toohello Azure AD Graph API sağlar.</span><span class="sxs-lookup"><span data-stu-id="eba8c-173">Each time you invoke one of these commands, `B2CGraphClient` makes a request toohello Azure AD Graph API.</span></span>

### <a name="get-an-access-token"></a><span data-ttu-id="eba8c-174">Bir erişim belirteci alma</span><span class="sxs-lookup"><span data-stu-id="eba8c-174">Get an access token</span></span>
<span data-ttu-id="eba8c-175">Tüm istek toohello grafik API'si bir erişim belirteci için kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="eba8c-175">Any request toohello Graph API requires an access token for authentication.</span></span> <span data-ttu-id="eba8c-176">`B2CGraphClient`kullandığı hello açık kaynak Active Directory Authentication Library (ADAL) toohelp erişim belirteci alın.</span><span class="sxs-lookup"><span data-stu-id="eba8c-176">`B2CGraphClient` uses hello open-source Active Directory Authentication Library (ADAL) toohelp acquire access tokens.</span></span> <span data-ttu-id="eba8c-177">ADAL belirteç edinme basit bir API sağlayarak ve erişim belirteçleri önbelleğe alma gibi bazı önemli ayrıntıları alma verdiğiniz kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="eba8c-177">ADAL makes token acquisition easier by providing a simple API and taking care of some important details, such as caching access tokens.</span></span> <span data-ttu-id="eba8c-178">Toouse ADAL tooget belirteçleri, ancak yok.</span><span class="sxs-lookup"><span data-stu-id="eba8c-178">You don't have toouse ADAL tooget tokens, though.</span></span> <span data-ttu-id="eba8c-179">Ayrıca, HTTP isteklerini hazırlayın tarafından belirteç alabilir.</span><span class="sxs-lookup"><span data-stu-id="eba8c-179">You can also get tokens by crafting HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="eba8c-180">Bu kod örneği hello grafik API'si ile sipariş toocommunicate ADAL v2 kullanır.</span><span class="sxs-lookup"><span data-stu-id="eba8c-180">This code sample uses ADAL v2 in order toocommunicate with hello Graph API.</span></span>  <span data-ttu-id="eba8c-181">ADAL v2 veya v3 hello Azure AD grafik API'si ile kullanılabilen sipariş tooget erişim belirteçleri kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="eba8c-181">You must use ADAL v2 or v3 in order tooget access tokens which can be used with hello Azure AD Graph API.</span></span>
> 
> 

<span data-ttu-id="eba8c-182">Zaman `B2CGraphClient` çalıştırır, hello örneği oluşturur `B2CGraphClient` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="eba8c-182">When `B2CGraphClient` runs, it creates an instance of hello `B2CGraphClient` class.</span></span> <span data-ttu-id="eba8c-183">Bu sınıf için Hello Oluşturucu ADAL kimlik doğrulaması iskele kurma ayarlar:</span><span class="sxs-lookup"><span data-stu-id="eba8c-183">hello constructor for this class sets up an ADAL authentication scaffolding:</span></span>

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // hello client_id, client_secret, and tenant are provided in Program.cs, which pulls hello values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // hello AuthenticationContext is ADAL's primary class, in which you indicate hello tenant toouse.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // hello ClientCredential is where you pass in your client_id and client_secret, which are
    // provided tooAzure AD in order tooreceive an access_token by using hello app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

<span data-ttu-id="eba8c-184">Merhaba kullanacağız `B2C Get-User` bir örnek olarak komutu.</span><span class="sxs-lookup"><span data-stu-id="eba8c-184">We'll use hello `B2C Get-User` command as an example.</span></span> <span data-ttu-id="eba8c-185">Zaman `B2C Get-User` , hello CLI çağrıları hello gibi ek tüm girişleri çağrılan `B2CGraphClient.GetAllUsers(...)` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="eba8c-185">When `B2C Get-User` is invoked without any additional inputs, hello CLI calls hello `B2CGraphClient.GetAllUsers(...)` method.</span></span> <span data-ttu-id="eba8c-186">Bu yöntemi çağırır `B2CGraphClient.SendGraphGetRequest(...)`, bir HTTP GET isteği toohello grafik API'si gönderir.</span><span class="sxs-lookup"><span data-stu-id="eba8c-186">This method calls `B2CGraphClient.SendGraphGetRequest(...)`, which submits an HTTP GET request toohello Graph API.</span></span> <span data-ttu-id="eba8c-187">Önce `B2CGraphClient.SendGraphGetRequest(...)` hello GET isteği gönderir, onu önce bir erişim ADAL kullanarak belirtecini alır:</span><span class="sxs-lookup"><span data-stu-id="eba8c-187">Before `B2CGraphClient.SendGraphGetRequest(...)` sends hello GET request, it first gets an access token by using ADAL:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL tooacquire a token by using hello app's identity (hello credential)
    // hello first parameter is hello resource we want an access_token for; in this case, hello Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

<span data-ttu-id="eba8c-188">Bir erişim hello grafik API'si çağırma hello ADAL tarafından için belirteç sağlayabilmek için `AuthenticationContext.AcquireToken(...)` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="eba8c-188">You can get an access token for hello Graph API by calling hello ADAL `AuthenticationContext.AcquireToken(...)` method.</span></span> <span data-ttu-id="eba8c-189">Ardından ADAL döndüren bir `access_token` hello uygulamanın kimliğini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="eba8c-189">ADAL then returns an `access_token` that represents hello application's identity.</span></span>

### <a name="read-users"></a><span data-ttu-id="eba8c-190">Kullanıcıların okuma</span><span class="sxs-lookup"><span data-stu-id="eba8c-190">Read users</span></span>
<span data-ttu-id="eba8c-191">Tooget kullanıcıların listesini istediğiniz veya belirli bir kullanıcı grafik API'si hello almak, bir HTTP gönderebilirsiniz `GET` toohello isteği `/users` uç noktası.</span><span class="sxs-lookup"><span data-stu-id="eba8c-191">When you want tooget a list of users or get a particular user from hello Graph API, you can send an HTTP `GET` request toohello `/users` endpoint.</span></span> <span data-ttu-id="eba8c-192">Tüm Kiracı hello kullanıcılar için bir istek şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="eba8c-192">A request for all of hello users in a tenant looks like this:</span></span>

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="eba8c-193">toosee çalıştırmak, bu isteği:</span><span class="sxs-lookup"><span data-stu-id="eba8c-193">toosee this request, run:</span></span>

 ```
 > B2C Get-User
 ```

<span data-ttu-id="eba8c-194">İki önemli noktalar toonote vardır:</span><span class="sxs-lookup"><span data-stu-id="eba8c-194">There are two important things toonote:</span></span>

* <span data-ttu-id="eba8c-195">Merhaba ADAL edinilen erişim belirteci toohello eklenen `Authorization` hello kullanarak üstbilgi `Bearer` düzeni.</span><span class="sxs-lookup"><span data-stu-id="eba8c-195">hello access token acquired via ADAL is added toohello `Authorization` header by using hello `Bearer` scheme.</span></span>
* <span data-ttu-id="eba8c-196">B2C kiracılar için hello sorgu parametresi kullanmalısınız `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="eba8c-196">For B2C tenants, you must use hello query parameter `api-version=1.6`.</span></span>

<span data-ttu-id="eba8c-197">Bu ayrıntıları her ikisi de hello işlenir `B2CGraphClient.SendGraphGetRequest(...)` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="eba8c-197">Both of these details are handled in hello `B2CGraphClient.SendGraphGetRequest(...)` method:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure toouse hello 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append hello access token for hello Graph API toohello Authorization header of hello request by using hello Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a><span data-ttu-id="eba8c-198">Tüketici kullanıcı hesapları oluşturun</span><span class="sxs-lookup"><span data-stu-id="eba8c-198">Create consumer user accounts</span></span>
<span data-ttu-id="eba8c-199">B2C kiracınızda kullanıcı hesapları oluştururken, bir HTTP gönderebilirsiniz `POST` toohello isteği `/users` uç noktası:</span><span class="sxs-lookup"><span data-stu-id="eba8c-199">When you create user accounts in your B2C tenant, you can send an HTTP `POST` request toohello `/users` endpoint:</span></span>

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required toocreate consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier hello user uses toosign in toohello account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set too'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying toohello end user
    "mailNickname": "joec",                        // an email alias for hello user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set toofalse
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

<span data-ttu-id="eba8c-200">Bu isteği bu özelliklerin çoğu, gerekli toocreate tüketici kullanıcılardır.</span><span class="sxs-lookup"><span data-stu-id="eba8c-200">Most of these properties in this request are required toocreate consumer users.</span></span> <span data-ttu-id="eba8c-201">toolearn daha fazlasını tıklatın [burada](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span><span class="sxs-lookup"><span data-stu-id="eba8c-201">toolearn more, click [here](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span></span> <span data-ttu-id="eba8c-202">Bu hello Not `//` açıklamaları çizim için dahil edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="eba8c-202">Note that hello `//` comments have been included for illustration.</span></span> <span data-ttu-id="eba8c-203">Bunları, gerçek bir istekte dahil etmeyin.</span><span class="sxs-lookup"><span data-stu-id="eba8c-203">Do not include them in an actual request.</span></span>

<span data-ttu-id="eba8c-204">toosee hello isteği, komutları aşağıdaki hello birini çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="eba8c-204">toosee hello request, run one of hello following commands:</span></span>

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

<span data-ttu-id="eba8c-205">Merhaba `Create-User` komutu bir .json dosyası olarak bir giriş parametresi alır.</span><span class="sxs-lookup"><span data-stu-id="eba8c-205">hello `Create-User` command takes a .json file as an input parameter.</span></span> <span data-ttu-id="eba8c-206">Bu, bir kullanıcı nesnesinin bir JSON temsili içerir.</span><span class="sxs-lookup"><span data-stu-id="eba8c-206">This contains a JSON representation of a user object.</span></span> <span data-ttu-id="eba8c-207">Merhaba örnek kodda iki örnek .json dosyası vardır: `usertemplate-email.json` ve `usertemplate-username.json`.</span><span class="sxs-lookup"><span data-stu-id="eba8c-207">There are two sample .json files in hello sample code: `usertemplate-email.json` and `usertemplate-username.json`.</span></span> <span data-ttu-id="eba8c-208">Bu dosyaları toosuit gereksinimlerinizi değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eba8c-208">You can modify these files toosuit your needs.</span></span> <span data-ttu-id="eba8c-209">Ayrıca toohello gerekli alanları yukarıdaki, kullanabileceğiniz birkaç isteğe bağlı alanları bu dosyaları dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="eba8c-209">In addition toohello required fields above, several optional fields that you can use are included in these files.</span></span> <span data-ttu-id="eba8c-210">Ayrıntılar hello isteğe bağlı alanları hello bulunabilir [Azure AD Graph API varlık başvurusu](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span><span class="sxs-lookup"><span data-stu-id="eba8c-210">Details on hello optional fields can be found in hello [Azure AD Graph API entity reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span></span>

<span data-ttu-id="eba8c-211">Merhaba POST isteği nasıl oluşturulur görebilirsiniz `B2CGraphClient.SendGraphPostRequest(...)`.</span><span class="sxs-lookup"><span data-stu-id="eba8c-211">You can see how hello POST request is constructed in `B2CGraphClient.SendGraphPostRequest(...)`.</span></span>

* <span data-ttu-id="eba8c-212">Bir erişim belirteci toohello iliştirir `Authorization` hello isteği üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="eba8c-212">It attaches an access token toohello `Authorization` header of hello request.</span></span>
* <span data-ttu-id="eba8c-213">Bu ayarlar `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="eba8c-213">It sets `api-version=1.6`.</span></span>
* <span data-ttu-id="eba8c-214">Bu, hello hello istek gövdesinde hello JSON kullanıcı nesnesi içerir.</span><span class="sxs-lookup"><span data-stu-id="eba8c-214">It includes hello JSON user object in hello body of hello request.</span></span>

> [!NOTE]
> <span data-ttu-id="eba8c-215">Merhaba hesapları var olan bir kullanıcı deposundan toomigrate başlangıç değerinden daha düşük parola gücünü sahip isterseniz [Azure AD B2C tarafından zorlanan güçlü parola gücünü](https://msdn.microsoft.com/library/azure/jj943764.aspx), hello kullanarakhellogüçlüparolagereksiniminidevredışıbırakabilirsiniz`DisableStrongPassword`hello değerinde `passwordPolicies` özelliği.</span><span class="sxs-lookup"><span data-stu-id="eba8c-215">If hello accounts that you want toomigrate from an existing user store has lower password strength than hello [strong password strength enforced by Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), you can disable hello strong password requirement using hello `DisableStrongPassword` value in hello `passwordPolicies` property.</span></span> <span data-ttu-id="eba8c-216">Merhaba örneği için değiştirebileceğiniz gibi yukarıda verilen kullanıcı isteği oluşturma: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span><span class="sxs-lookup"><span data-stu-id="eba8c-216">For instance, you can modify hello create user request provided above as follows: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span></span>
> 
> 

### <a name="update-consumer-user-accounts"></a><span data-ttu-id="eba8c-217">Tüketici kullanıcı hesaplarını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="eba8c-217">Update consumer user accounts</span></span>
<span data-ttu-id="eba8c-218">Kullanıcı nesneleri güncelleştirdiğinizde hello benzer toohello toocreate kullanıcı nesneleri kullandığınız işlemdir.</span><span class="sxs-lookup"><span data-stu-id="eba8c-218">When you update user objects, hello process is similar toohello one you use toocreate user objects.</span></span> <span data-ttu-id="eba8c-219">Ancak bu işlem hello HTTP kullanan `PATCH` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="eba8c-219">But this process uses hello HTTP `PATCH` method:</span></span>

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only hello user's displayName
}
```

<span data-ttu-id="eba8c-220">Tooupdate bir kullanıcı yeni verilerle, JSON dosyalarınızın güncelleştirerek deneyin.</span><span class="sxs-lookup"><span data-stu-id="eba8c-220">Try tooupdate a user by updating your JSON files with new data.</span></span> <span data-ttu-id="eba8c-221">Daha sonra `B2CGraphClient` toorun aşağıdaki komutlardan birini:</span><span class="sxs-lookup"><span data-stu-id="eba8c-221">You can then use `B2CGraphClient` toorun one of these commands:</span></span>

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

<span data-ttu-id="eba8c-222">Merhaba incelemek `B2CGraphClient.SendGraphPatchRequest(...)` yöntemi hakkında ayrıntılar için toosend bu isteği.</span><span class="sxs-lookup"><span data-stu-id="eba8c-222">Inspect hello `B2CGraphClient.SendGraphPatchRequest(...)` method for details on how toosend this request.</span></span>

### <a name="search-users"></a><span data-ttu-id="eba8c-223">Kullanıcılarda arama</span><span class="sxs-lookup"><span data-stu-id="eba8c-223">Search users</span></span>
<span data-ttu-id="eba8c-224">B2C kiracınızda çeşitli şekillerde kullanıcılar için arama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eba8c-224">You can search for users in your B2C tenant in a couple of ways.</span></span> <span data-ttu-id="eba8c-225">Merhaba kullanıcının nesne kimliği veya hello kullanıcının oturum açma tanımlayıcı kullanarak iki kullanarak bir (yani, hello `signInNames` özelliği).</span><span class="sxs-lookup"><span data-stu-id="eba8c-225">One, using hello user's object ID or two, using hello user's sign-in identifer (i.e., hello `signInNames` property).</span></span>

<span data-ttu-id="eba8c-226">Belirli bir kullanıcı için komutları toosearch aşağıdaki hello birini çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="eba8c-226">Run one of hello following commands toosearch for a specific user:</span></span>

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

<span data-ttu-id="eba8c-227">Aşağıda birkaç örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="eba8c-227">Here are a couple of examples:</span></span>

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a><span data-ttu-id="eba8c-228">Kullanıcıları silme</span><span class="sxs-lookup"><span data-stu-id="eba8c-228">Delete users</span></span>
<span data-ttu-id="eba8c-229">Kullanıcı silme hello basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="eba8c-229">hello process for deleting a user is straightforward.</span></span> <span data-ttu-id="eba8c-230">Kullanım hello HTTP `DELETE` hello yöntemi ve yapı hello URL'SİYLE düzeltmek nesne kimliği:</span><span class="sxs-lookup"><span data-stu-id="eba8c-230">Use hello HTTP `DELETE` method and construct hello URL with hello correct object ID:</span></span>

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="eba8c-231">toosee bir örnek yazdırılan toohello konsol bu komut ve görünüm hello silme isteği girin:</span><span class="sxs-lookup"><span data-stu-id="eba8c-231">toosee an example, enter this command and view hello delete request that is printed toohello console:</span></span>

```
> B2C Delete-User <object-id-of-user>
```

<span data-ttu-id="eba8c-232">Merhaba incelemek `B2CGraphClient.SendGraphDeleteRequest(...)` yöntemi hakkında ayrıntılar için toosend bu isteği.</span><span class="sxs-lookup"><span data-stu-id="eba8c-232">Inspect hello `B2CGraphClient.SendGraphDeleteRequest(...)` method for details on how toosend this request.</span></span>

<span data-ttu-id="eba8c-233">Toplama toouser Yönetimi'nde hello Azure AD Graph API birçok başka eylemler gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="eba8c-233">You can perform many other actions with hello Azure AD Graph API in addition toouser management.</span></span> <span data-ttu-id="eba8c-234">[Azure AD Graph API Başvurusu](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) örnek istekleri yanı sıra her bir eylemde ayrıntıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="eba8c-234">The [Azure AD Graph API reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) provides details on each action, along with sample requests.</span></span>

## <a name="use-custom-attributes"></a><span data-ttu-id="eba8c-235">Özel öznitelikler kullanma</span><span class="sxs-lookup"><span data-stu-id="eba8c-235">Use custom attributes</span></span>
<span data-ttu-id="eba8c-236">Çoğu tüketici uygulamaları herhangi bir tür özel kullanıcı profili bilgilerini toostore gerekir.</span><span class="sxs-lookup"><span data-stu-id="eba8c-236">Most consumer applications need toostore some type of custom user profile information.</span></span> <span data-ttu-id="eba8c-237">Bunu yapmak için bir toodefine B2C kiracınızın özel bir öznitelikte yoludur.</span><span class="sxs-lookup"><span data-stu-id="eba8c-237">One way you can do this is toodefine a custom attribute in your B2C tenant.</span></span> <span data-ttu-id="eba8c-238">Ardından bu özniteliği hello davranabilirsiniz aynı şekilde bir kullanıcı nesnesi üzerinde herhangi bir özellik işle.</span><span class="sxs-lookup"><span data-stu-id="eba8c-238">You can then treat that attribute hello same way you treat any other property on a user object.</span></span> <span data-ttu-id="eba8c-239">Merhaba özniteliği güncelleştirebilir Sil hello özniteliğinin, sorgu hello özniteliği tarafından hello özniteliği ve oturum açma belirteçleri talep olarak gönder.</span><span class="sxs-lookup"><span data-stu-id="eba8c-239">You can update hello attribute, delete hello attribute, query by hello attribute, send hello attribute as a claim in sign-in tokens, and more.</span></span>

<span data-ttu-id="eba8c-240">toodefine B2C kiracınızın özel bir öznitelikte bkz hello [B2C özel öznitelik başvurusu](active-directory-b2c-reference-custom-attr.md).</span><span class="sxs-lookup"><span data-stu-id="eba8c-240">toodefine a custom attribute in your B2C tenant, see hello [B2C custom attribute reference](active-directory-b2c-reference-custom-attr.md).</span></span>

<span data-ttu-id="eba8c-241">B2C kiracınızda kullanarak tanımlanan özel özniteliklere hello görüntüleyebilirsiniz `B2CGraphClient`:</span><span class="sxs-lookup"><span data-stu-id="eba8c-241">You can view hello custom attributes defined in your B2C tenant by using `B2CGraphClient`:</span></span>

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

<span data-ttu-id="eba8c-242">Bu işlevlerin Hello çıktı gibi her özel özniteliğinin hello ayrıntıları ortaya çıkarır:</span><span class="sxs-lookup"><span data-stu-id="eba8c-242">hello output of these functions reveals hello details of each custom attribute, such as:</span></span>

```JSON
{
      "odata.type": "Microsoft.DirectoryServices.ExtensionProperty",
      "objectType": "ExtensionProperty",
      "objectId": "cec6391b-204d-42fe-8f7c-89c2b1964fca",
      "deletionTimestamp": null,
      "appDisplayName": "",
      "name": "extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number",
      "dataType": "Integer",
      "isSyncedFromOnPremises": false,
      "targetObjects": [
        "User"
      ]
}
```

<span data-ttu-id="eba8c-243">Hello gibi tam adı kullanabilirsiniz `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, kullanıcı nesneleri bir özellik olarak.</span><span class="sxs-lookup"><span data-stu-id="eba8c-243">You can use hello full name, such as `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, as a property on your user objects.</span></span>  <span data-ttu-id="eba8c-244">Merhaba yeni özellik ve hello özelliği için bir değer ile .json dosyanızı güncelleştirin ve ardından çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="eba8c-244">Update your .json file with hello new property and a value for hello property, and then run:</span></span>

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

<span data-ttu-id="eba8c-245">Kullanarak `B2CGraphClient`, B2C Kiracı kullanıcılarınızın program aracılığıyla yönetebilen bir hizmet uygulaması sahip.</span><span class="sxs-lookup"><span data-stu-id="eba8c-245">By using `B2CGraphClient`, you have a service application that can manage your B2C tenant users programmatically.</span></span> <span data-ttu-id="eba8c-246">`B2CGraphClient`kendi uygulama kimliği tooauthenticate toohello Azure AD Graph API kullanır.</span><span class="sxs-lookup"><span data-stu-id="eba8c-246">`B2CGraphClient` uses its own application identity tooauthenticate toohello Azure AD Graph API.</span></span> <span data-ttu-id="eba8c-247">Ayrıca, istemci parolasını kullanarak belirteçleri da alır.</span><span class="sxs-lookup"><span data-stu-id="eba8c-247">It also acquires tokens by using a client secret.</span></span> <span data-ttu-id="eba8c-248">Bu işlev uygulamanıza dahil, B2C uygulamalar için birkaç önemli nokta unutmayın:</span><span class="sxs-lookup"><span data-stu-id="eba8c-248">As you incorporate this functionality into your application, remember a few key points for B2C apps:</span></span>

* <span data-ttu-id="eba8c-249">Toogrant hello uygulama hello uygun izinleri hello Kiracı gerekir.</span><span class="sxs-lookup"><span data-stu-id="eba8c-249">You need toogrant hello application hello proper permissions in hello tenant.</span></span>
* <span data-ttu-id="eba8c-250">Şimdilik, toouse ADAL (değil MSAL) tooget erişim belirteçleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="eba8c-250">For now, you need toouse ADAL (not MSAL) tooget access tokens.</span></span> <span data-ttu-id="eba8c-251">(Ayrıca protokol iletilerini doğrudan bir kitaplık kullanılarak olmadan gönderebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="eba8c-251">(You can also send protocol messages directly, without using a library.)</span></span>
* <span data-ttu-id="eba8c-252">Merhaba grafik API'si çağırdığınızda, kullanabilirsiniz `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="eba8c-252">When you call hello Graph API, use `api-version=1.6`.</span></span>
* <span data-ttu-id="eba8c-253">Oluşturduğunuzda ve tüketici kullanıcıları güncelleştirmek birkaç özelliği yukarıda açıklandığı gibi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="eba8c-253">When you create and update consumer users, a few properties are required, as described above.</span></span>

<span data-ttu-id="eba8c-254">Herhangi bir sorunuz veya Eylemler tooperform hello grafik API'sini kullanarak istediğiniz istekleri varsa B2C kiracınızın bu makalede bir yorum yazın veya bir sorunu hello GitHub kod örnek deposunda dosya.</span><span class="sxs-lookup"><span data-stu-id="eba8c-254">If you have any questions or requests for actions you would like tooperform by using hello Graph API on your B2C tenant, leave a comment on this article or file an issue in hello GitHub code sample repository.</span></span>

