---
title: "Azure Active Directory B2C: grafik API'si kullanın | Microsoft Docs"
description: "İşlemini otomatikleştirmek için bir uygulama kimliği kullanarak bir B2C Kiracı için grafik API'sini çağırmak nasıl."
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
ms.openlocfilehash: c838fcad21875c4f813159ad78d4c87129a40a86
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-ad-b2c-use-the-graph-api"></a><span data-ttu-id="1f6fc-103">Azure AD B2C: grafik API'si kullanın</span><span class="sxs-lookup"><span data-stu-id="1f6fc-103">Azure AD B2C: Use the Graph API</span></span>
<span data-ttu-id="1f6fc-104">Azure Active Directory (Azure AD) B2C kiracılar çok büyük olma eğilimindedir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-104">Azure Active Directory (Azure AD) B2C tenants tend to be very large.</span></span> <span data-ttu-id="1f6fc-105">Bu, çok sayıda genel kiracı yönetim görevlerini programlı olarak yapılması gereken anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-105">This means that many common tenant management tasks need to be performed programmatically.</span></span> <span data-ttu-id="1f6fc-106">Kullanıcı Yönetimi buna birincil bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-106">A primary example is user management.</span></span> <span data-ttu-id="1f6fc-107">B2C Kiracı için var olan bir kullanıcı deposunun geçirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-107">You might need to migrate an existing user store to a B2C tenant.</span></span> <span data-ttu-id="1f6fc-108">Kullanıcı kaydı kendi sayfasında barındırmak ve arka planda Azure AD B2C dizininizde kullanıcı hesapları oluşturmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-108">You may want to host user registration on your own page and create user accounts in your Azure AD B2C directory behind the scenes.</span></span> <span data-ttu-id="1f6fc-109">Bu tür bir görev oluşturma, okuma, güncelleştirme gerektirir ve kullanıcı hesaplarını silin.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-109">These types of tasks require the ability to create, read, update, and delete user accounts.</span></span> <span data-ttu-id="1f6fc-110">Azure AD grafik API'sini kullanarak bu görevleri yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-110">You can do these tasks by using the Azure AD Graph API.</span></span>

<span data-ttu-id="1f6fc-111">B2C kiracılar için grafik API'si ile iletişim iki birincil modu mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-111">For B2C tenants, there are two primary modes of communicating with the Graph API.</span></span>

* <span data-ttu-id="1f6fc-112">Görevleri gerçekleştirdiğinizde etkileşimli, bir kez çalıştır görevler için bir yönetici hesabı B2C Kiracı olarak işlem yapmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-112">For interactive, run-once tasks, you should act as an administrator account in the B2C tenant when you perform the tasks.</span></span> <span data-ttu-id="1f6fc-113">Bu modu yönetici, yönetici grafik API'si yapılan her çağrı gerçekleştirmeden önce kimlik bilgileriyle oturum gerektirir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-113">This mode requires an administrator to sign in with credentials before that admin can perform any calls to the Graph API.</span></span>
* <span data-ttu-id="1f6fc-114">Otomatik, sürekli görevleri için bazı yönetim görevlerini gerçekleştirmek için gerekli ayrıcalıklara sağladığınız hizmet hesabı türünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-114">For automated, continuous tasks, you should use some type of service account that you provide with the necessary privileges to perform management tasks.</span></span> <span data-ttu-id="1f6fc-115">Azure AD'de uygulama kaydetme ve Azure AD ile kimlik doğrulaması tarafından bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-115">In Azure AD, you can do this by registering an application and authenticating to Azure AD.</span></span> <span data-ttu-id="1f6fc-116">Bu kullanılarak yapılır bir **uygulama kimliği** kullanan [OAuth 2.0 istemci kimlik bilgileri vermenizi](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="1f6fc-116">This is done by using an **Application ID** that uses the [OAuth 2.0 client credentials grant](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span></span> <span data-ttu-id="1f6fc-117">Bu durumda, uygulama grafik API'sini çağırmak için bir kullanıcı değil, olarak kendisini olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-117">In this case, the application acts as itself, not as a user, to call the Graph API.</span></span>

<span data-ttu-id="1f6fc-118">Bu makalede, biz otomatik kullanım örneğini gerçekleştirmek nasıl ele alacağız.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-118">In this article, we'll discuss how to perform the automated-use case.</span></span> <span data-ttu-id="1f6fc-119">Göstermek için size bir .NET 4.5 yapı `B2CGraphClient` gerçekleştiren kullanıcı oluşturma, okuma, güncelleştirme ve Sil (CRUD) işlemleridir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-119">To demonstrate, we'll build a .NET 4.5 `B2CGraphClient` that performs user create, read, update, and delete (CRUD) operations.</span></span> <span data-ttu-id="1f6fc-120">İstemci, bir Windows komut satırı çeşitli yöntemlerini çağırmasına izin veren arabirimi (CLI) sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-120">The client will have a Windows command-line interface (CLI) that allows you to invoke various methods.</span></span> <span data-ttu-id="1f6fc-121">Bununla birlikte, kod etkileşimsiz, otomatik bir şekilde davranmasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-121">However, the code is written to behave in a noninteractive, automated fashion.</span></span>

## <a name="get-an-azure-ad-b2c-tenant"></a><span data-ttu-id="1f6fc-122">Bir Azure AD B2C kiracısı edinme</span><span class="sxs-lookup"><span data-stu-id="1f6fc-122">Get an Azure AD B2C tenant</span></span>
<span data-ttu-id="1f6fc-123">Uygulama veya kullanıcıların oluşturabilir veya Azure AD ile etkileşimde önce Azure AD B2C Kiracı ve Kiracı genel Yönetici hesabında gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-123">Before you can create applications or users, or interact with Azure AD at all, you will need an Azure AD B2C tenant and a global administrator account in the tenant.</span></span> <span data-ttu-id="1f6fc-124">Zaten bir kiracı yoksa [Azure AD B2C ile çalışmaya başlama](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1f6fc-124">If you don't have a tenant already, [get started with Azure AD B2C](active-directory-b2c-get-started.md).</span></span>

## <a name="register-your-application-in-your-tenant"></a><span data-ttu-id="1f6fc-125">Kiracınızda uygulamanızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="1f6fc-125">Register your application in your tenant</span></span>
<span data-ttu-id="1f6fc-126">B2C Kiracı aldıktan sonra aracılığıyla uygulamanızı kaydetmeniz gerekir [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1f6fc-126">After you have a B2C tenant, you need to register your application via the [Azure Portal](https://portal.azure.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f6fc-127">Grafik API'si B2C kiracınızın kullanmak için genel kullanarak özel bir uygulamayı kaydetme gerekecektir *uygulama kayıtlar* Azure portaldaki dikey pencere **değil** Azure AD B2C'in  *Uygulamaları* dikey.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-127">To use the Graph API with your B2C tenant, you will need to register a dedicated application by using the generic *App Registrations* blade in the Azure Portal, **NOT** Azure AD B2C's *Applications* blade.</span></span> <span data-ttu-id="1f6fc-128">Azure AD B2C'de 's kayıtlı zaten varolan B2C uygulamaları tekrar kullanamazsınız *uygulamaları* dikey.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-128">You can't reuse the already-existing B2C applications that you registered in the Azure AD B2C's *Applications* blade.</span></span>

1. <span data-ttu-id="1f6fc-129">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-129">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1f6fc-130">Sayfanın sağ üst köşesinde hesabınızı seçerek Azure AD B2C kiracınızın seçin.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-130">Choose your Azure AD B2C tenant by selecting your account in the top right corner of the page.</span></span>
3. <span data-ttu-id="1f6fc-131">Sol Gezinti Bölmesi'nde seçin **daha Hizmetleri**, tıklatın **uygulama kayıtlar**, tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-131">In the left-hand navigation pane, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
4. <span data-ttu-id="1f6fc-132">Komut istemlerini izleyin ve yeni bir uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-132">Follow the prompts and create a new application.</span></span> 
    1. <span data-ttu-id="1f6fc-133">Seçin **Web uygulaması / API** uygulama türü olarak.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-133">Select **Web App / API** as the Application Type.</span></span>    
    2. <span data-ttu-id="1f6fc-134">Sağlamak **URI herhangi bir yeniden yönlendirme** (örneğin https://B2CGraphAPI) Bu örnek için uygun değil olarak.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-134">Provide **any redirect URI** (e.g. https://B2CGraphAPI) as it's not relevant for this example.</span></span>  
5. <span data-ttu-id="1f6fc-135">Uygulama şimdi yukarı uygulamalar listesinde göster elde etmek için **uygulama kimliği** (istemci kimliği olarak da bilinir).</span><span class="sxs-lookup"><span data-stu-id="1f6fc-135">The application will now show up in the list of applications, click on it to obtain the **Application ID** (also known as Client ID).</span></span> <span data-ttu-id="1f6fc-136">Bir sonraki bölümde gereksinim duyacağınız kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-136">Copy it as you'll need it in a later section.</span></span>
6. <span data-ttu-id="1f6fc-137">Ayarlar dikey penceresinde tıklayın **anahtarları** ve yeni bir anahtar (istemci gizli anahtarı olarak da bilinir) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-137">In the Settings blade, click on **Keys** and add a new key (also known as client secret).</span></span> <span data-ttu-id="1f6fc-138">Ayrıca daha sonraki bir bölüme kullanmak için kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-138">Also copy it for use in a later section.</span></span>

## <a name="configure-create-read-and-update-permissions-for-your-application"></a><span data-ttu-id="1f6fc-139">Yapılandırma oluşturmak, okumak ve güncelleştirmek, uygulamanız için izinler</span><span class="sxs-lookup"><span data-stu-id="1f6fc-139">Configure create, read and update permissions for your application</span></span>
<span data-ttu-id="1f6fc-140">Şimdi oluşturma, okuma, güncelleştirme ve kullanıcıları silmek için gerekli tüm izinleri almak için uygulamanızı yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-140">Now you need to configure your application to get all the required permissions to create, read, update and delete users.</span></span>

1. <span data-ttu-id="1f6fc-141">Azure portal'ın uygulama kayıtlar dikey penceresinde devam etmeden, uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-141">Continuing in the Azure portal's App Registrations blade, select your application.</span></span>
2. <span data-ttu-id="1f6fc-142">Ayarlar dikey penceresinde tıklayın **gerekli izinleri**.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-142">In the Settings blade, click on **Required permissions**.</span></span>
3. <span data-ttu-id="1f6fc-143">Gerekli izinleri dikey penceresinde tıklayın **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-143">In the Required permissions blade, click on **Windows Azure Active Directory**.</span></span>
4. <span data-ttu-id="1f6fc-144">Erişimi etkinleştir dikey penceresinde, seçin **dizin verilerini okuma ve yazma** iznini **uygulama izinleri** tıklatıp **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-144">In the Enable Access  blade, select the **Read and write directory data** permission from **Application Permissions** and click **Save**.</span></span>
5. <span data-ttu-id="1f6fc-145">Gerekli izinleri dikey geri, son olarak, tıklayın **izinler** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-145">Finally, back in the Required permissions blade, click on the **Grant Permissions** button.</span></span>

<span data-ttu-id="1f6fc-146">Artık oluşturmak, okumak ve B2C kiracınızın kullanıcılardan güncelleştirmek için izni olan bir uygulama var.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-146">You now have an application that has permission to create, read and update users from your B2C tenant.</span></span>

## <a name="configure-delete-permissions-for-your-application"></a><span data-ttu-id="1f6fc-147">Uygulamanız için silme izinleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1f6fc-147">Configure delete permissions for your application</span></span>
<span data-ttu-id="1f6fc-148">Şu anda *dizin verilerini okuma ve yazma* izin vermez **değil** kullanıcıları silme gibi tüm silme işlemleri yapmak için özelliğini içerir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-148">Currently, the *Read and write directory data* permission does **NOT** include the ability to do any deletions such as deleting users.</span></span> <span data-ttu-id="1f6fc-149">Uygulamanız kullanıcıların silme olanağı vermek istiyorsanız, PowerShell ile ilgili aşağıdaki ek adımları yapmanız gerekir, aksi halde, sonraki bölüme atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-149">If you want to give your application the ability to delete users, you'll need to do these extra steps that involve PowerShell, otherwise, you can skip to the next section.</span></span>

<span data-ttu-id="1f6fc-150">İlk olarak, indirin ve yükleyin [Microsoft Online Services oturum açma Yardımcısı](http://go.microsoft.com/fwlink/?LinkID=286152).</span><span class="sxs-lookup"><span data-stu-id="1f6fc-150">First, download and install the [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span> <span data-ttu-id="1f6fc-151">Ardından karşıdan yükleyip [64-bit Windows PowerShell için Azure Active Directory Modülü](http://go.microsoft.com/fwlink/p/?linkid=236297).</span><span class="sxs-lookup"><span data-stu-id="1f6fc-151">Then download and install the [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>

<span data-ttu-id="1f6fc-152">PowerShell modülü yükledikten sonra PowerShell'i açın ve B2C kiracınızın bağlanın.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-152">After you install the PowerShell module, open PowerShell and connect to your B2C tenant.</span></span> <span data-ttu-id="1f6fc-153">Çalıştırdıktan sonra `Get-Credential`, bir kullanıcı adı ve parolanızı girmeniz için kullanıcı adını ve parolasını B2C Kiracı yönetici hesabınız istenir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-153">After you run `Get-Credential`, you will be prompted for a user name and password, Enter the user name and password of your B2C tenant administrator account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f6fc-154">Bir B2C Kiracı yönetici hesabı kullanmanız gerekir **yerel** B2C kiracısına.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-154">You need to use a B2C tenant administrator account that is **local** to the B2C tenant.</span></span> <span data-ttu-id="1f6fc-155">Bu hesapları şuna: myusername@myb2ctenant.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-155">These accounts look like this: myusername@myb2ctenant.onmicrosoft.com.</span></span>

```powershell
Connect-MsolService
```

<span data-ttu-id="1f6fc-156">Kullanacağız artık **uygulama kimliği** uygulama kullanıcıları silmek için olanak tanıyan kullanıcı hesabı yönetici rolü atamak için aşağıdaki komut dosyasında.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-156">Now we'll use the **Application ID** in the script below to assign the application the user account administrator role which will allow it to delete users.</span></span> <span data-ttu-id="1f6fc-157">Tüm yapmanız gereken giriş bu rolleri iyi bilinen tanımlayıcıları sahip, bu nedenle, **uygulama kimliği** aşağıdaki betikte yer.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-157">These roles have well-known identifiers, so all you need to do is input your **Application ID** in the script below.</span></span>

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

<span data-ttu-id="1f6fc-158">Uygulamanızı şimdi de B2C kiracınızın kullanıcıları silme izni vardır.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-158">Your application now also has permissions to delete users from your B2C tenant.</span></span>

## <a name="download-configure-and-build-the-sample-code"></a><span data-ttu-id="1f6fc-159">Karşıdan yükleme, yapılandırma ve örnek kod derleme</span><span class="sxs-lookup"><span data-stu-id="1f6fc-159">Download, configure, and build the sample code</span></span>
<span data-ttu-id="1f6fc-160">İlk olarak, örnek kodu indirin ve çalışmasını alın.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-160">First, download the sample code and get it running.</span></span> <span data-ttu-id="1f6fc-161">Ardından biz yakından bakmak sürer.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-161">Then we will take a closer look at it.</span></span>  <span data-ttu-id="1f6fc-162">Yapabilecekleriniz [örnek kod bir .zip dosyası olarak karşıdan](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="1f6fc-162">You can [download the sample code as a .zip file](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span></span> <span data-ttu-id="1f6fc-163">Ayrıca tercih ettiğiniz dizinine kopyalayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1f6fc-163">You can also clone it into a directory of your choice:</span></span>

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

<span data-ttu-id="1f6fc-164">Açık `B2CGraphClient\B2CGraphClient.sln` Visual Studio çözümü Visual Studio'da.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-164">Open the `B2CGraphClient\B2CGraphClient.sln` Visual Studio solution in Visual Studio.</span></span> <span data-ttu-id="1f6fc-165">İçinde `B2CGraphClient` projesi, dosyayı açma `App.config`.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-165">In the `B2CGraphClient` project, open the file `App.config`.</span></span> <span data-ttu-id="1f6fc-166">Üç uygulama ayarlarını kendi değerlerinizle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="1f6fc-166">Replace the three app settings with your own values:</span></span>

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{The ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{The Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="1f6fc-167">Ardından, sağ tıklayın `B2CGraphClient` çözüm ve örnek yeniden oluşturma.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-167">Next, right-click on the `B2CGraphClient` solution and rebuild the sample.</span></span> <span data-ttu-id="1f6fc-168">Başarılı olursa, şimdi olmalıdır bir `B2C.exe` içinde bulunan yürütülebilir dosyasını `B2CGraphClient\bin\Debug`.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-168">If you are successful, you should now have a `B2C.exe` executable file located in `B2CGraphClient\bin\Debug`.</span></span>

## <a name="build-user-crud-operations-by-using-the-graph-api"></a><span data-ttu-id="1f6fc-169">Grafik API'sini kullanarak yapı kullanıcı CRUD işlemleri</span><span class="sxs-lookup"><span data-stu-id="1f6fc-169">Build user CRUD operations by using the Graph API</span></span>
<span data-ttu-id="1f6fc-170">B2CGraphClient kullanmak için açık bir `cmd` Windows komut istemine ve dizininize değiştirmek `Debug` dizin.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-170">To use the B2CGraphClient, open a `cmd` Windows command prompt and change your directory to the `Debug` directory.</span></span> <span data-ttu-id="1f6fc-171">Ardından çalıştırın `B2C Help` komutu.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-171">Then run the `B2C Help` command.</span></span>

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

<span data-ttu-id="1f6fc-172">Bu her komut kısa bir açıklamasını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-172">This will display a brief description of each command.</span></span> <span data-ttu-id="1f6fc-173">Aşağıdaki komutlardan birini çağırma her zaman `B2CGraphClient` Azure AD grafik API'sine isteğinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-173">Each time you invoke one of these commands, `B2CGraphClient` makes a request to the Azure AD Graph API.</span></span>

### <a name="get-an-access-token"></a><span data-ttu-id="1f6fc-174">Bir erişim belirteci alma</span><span class="sxs-lookup"><span data-stu-id="1f6fc-174">Get an access token</span></span>
<span data-ttu-id="1f6fc-175">Grafik API'si için herhangi bir istek kimlik doğrulaması için bir erişim belirteci gerektirir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-175">Any request to the Graph API requires an access token for authentication.</span></span> <span data-ttu-id="1f6fc-176">`B2CGraphClient`erişim belirteci almak için açık kaynak Active Directory Authentication Library (ADAL) kullanır.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-176">`B2CGraphClient` uses the open-source Active Directory Authentication Library (ADAL) to help acquire access tokens.</span></span> <span data-ttu-id="1f6fc-177">ADAL belirteç edinme basit bir API sağlayarak ve erişim belirteçleri önbelleğe alma gibi bazı önemli ayrıntıları alma verdiğiniz kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-177">ADAL makes token acquisition easier by providing a simple API and taking care of some important details, such as caching access tokens.</span></span> <span data-ttu-id="1f6fc-178">Belirteçleri, ancak almak için ADAL kullanmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-178">You don't have to use ADAL to get tokens, though.</span></span> <span data-ttu-id="1f6fc-179">Ayrıca, HTTP isteklerini hazırlayın tarafından belirteç alabilir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-179">You can also get tokens by crafting HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="1f6fc-180">Bu kod örneği ADAL v2 grafik API'si ile iletişim kurmak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-180">This code sample uses ADAL v2 in order to communicate with the Graph API.</span></span>  <span data-ttu-id="1f6fc-181">Azure AD grafik API'si ile kullanılabilen erişim belirteçleri almak için ADAL v2 veya v3 kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-181">You must use ADAL v2 or v3 in order to get access tokens which can be used with the Azure AD Graph API.</span></span>
> 
> 

<span data-ttu-id="1f6fc-182">Zaman `B2CGraphClient` çalıştığında, bir örneğini oluşturur `B2CGraphClient` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-182">When `B2CGraphClient` runs, it creates an instance of the `B2CGraphClient` class.</span></span> <span data-ttu-id="1f6fc-183">Bu sınıf oluşturucusu ADAL kimlik doğrulaması iskele kurma ayarlar:</span><span class="sxs-lookup"><span data-stu-id="1f6fc-183">The constructor for this class sets up an ADAL authentication scaffolding:</span></span>

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // The client_id, client_secret, and tenant are provided in Program.cs, which pulls the values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // The AuthenticationContext is ADAL's primary class, in which you indicate the tenant to use.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // The ClientCredential is where you pass in your client_id and client_secret, which are
    // provided to Azure AD in order to receive an access_token by using the app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

<span data-ttu-id="1f6fc-184">Kullanacağız `B2C Get-User` bir örnek olarak komutu.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-184">We'll use the `B2C Get-User` command as an example.</span></span> <span data-ttu-id="1f6fc-185">Zaman `B2C Get-User` , CLI aramaları gibi ek tüm girişleri çağrılan `B2CGraphClient.GetAllUsers(...)` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-185">When `B2C Get-User` is invoked without any additional inputs, the CLI calls the `B2CGraphClient.GetAllUsers(...)` method.</span></span> <span data-ttu-id="1f6fc-186">Bu yöntemi çağırır `B2CGraphClient.SendGraphGetRequest(...)`, grafik API'si için bir HTTP GET isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-186">This method calls `B2CGraphClient.SendGraphGetRequest(...)`, which submits an HTTP GET request to the Graph API.</span></span> <span data-ttu-id="1f6fc-187">Önce `B2CGraphClient.SendGraphGetRequest(...)` gönderir GET isteği, onu önce bir erişim ADAL kullanarak belirtecini alır:</span><span class="sxs-lookup"><span data-stu-id="1f6fc-187">Before `B2CGraphClient.SendGraphGetRequest(...)` sends the GET request, it first gets an access token by using ADAL:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL to acquire a token by using the app's identity (the credential)
    // The first parameter is the resource we want an access_token for; in this case, the Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

<span data-ttu-id="1f6fc-188">Access grafik API'si için ADAL çağırarak belirteci alma `AuthenticationContext.AcquireToken(...)` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-188">You can get an access token for the Graph API by calling the ADAL `AuthenticationContext.AcquireToken(...)` method.</span></span> <span data-ttu-id="1f6fc-189">Ardından ADAL döndüren bir `access_token` , uygulamanın kimliğini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-189">ADAL then returns an `access_token` that represents the application's identity.</span></span>

### <a name="read-users"></a><span data-ttu-id="1f6fc-190">Kullanıcıların okuma</span><span class="sxs-lookup"><span data-stu-id="1f6fc-190">Read users</span></span>
<span data-ttu-id="1f6fc-191">Kullanıcıların bir listesini almak veya belirli bir kullanıcı grafik API'SİNDEN elde etmek istediğinizde, bir HTTP gönderebilirsiniz `GET` isteği `/users` uç noktası.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-191">When you want to get a list of users or get a particular user from the Graph API, you can send an HTTP `GET` request to the `/users` endpoint.</span></span> <span data-ttu-id="1f6fc-192">Tüm Kiracı kullanıcılar için bir istek şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="1f6fc-192">A request for all of the users in a tenant looks like this:</span></span>

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="1f6fc-193">Bu istek görmek için çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="1f6fc-193">To see this request, run:</span></span>

 ```
 > B2C Get-User
 ```

<span data-ttu-id="1f6fc-194">Dikkat edilecek iki önemli noktalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1f6fc-194">There are two important things to note:</span></span>

* <span data-ttu-id="1f6fc-195">ADAL edinilen erişim belirteci eklenen `Authorization` kullanarak üstbilgi `Bearer` düzeni.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-195">The access token acquired via ADAL is added to the `Authorization` header by using the `Bearer` scheme.</span></span>
* <span data-ttu-id="1f6fc-196">B2C kiracılar için sorgu parametresi kullanmalısınız `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-196">For B2C tenants, you must use the query parameter `api-version=1.6`.</span></span>

<span data-ttu-id="1f6fc-197">Bu ayrıntıları her ikisi de işlenir `B2CGraphClient.SendGraphGetRequest(...)` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="1f6fc-197">Both of these details are handled in the `B2CGraphClient.SendGraphGetRequest(...)` method:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure to use the 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append the access token for the Graph API to the Authorization header of the request by using the Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a><span data-ttu-id="1f6fc-198">Tüketici kullanıcı hesapları oluşturun</span><span class="sxs-lookup"><span data-stu-id="1f6fc-198">Create consumer user accounts</span></span>
<span data-ttu-id="1f6fc-199">B2C kiracınızda kullanıcı hesapları oluştururken, bir HTTP gönderebilirsiniz `POST` isteği `/users` uç noktası:</span><span class="sxs-lookup"><span data-stu-id="1f6fc-199">When you create user accounts in your B2C tenant, you can send an HTTP `POST` request to the `/users` endpoint:</span></span>

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required to create consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier the user uses to sign in to the account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set to 'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying to the end user
    "mailNickname": "joec",                        // an email alias for the user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set to false
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

<span data-ttu-id="1f6fc-200">Bu isteği bu özelliklerin çoğu tüketici kullanıcıları oluşturmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-200">Most of these properties in this request are required to create consumer users.</span></span> <span data-ttu-id="1f6fc-201">Daha fazla bilgi edinmek için tıklayın [burada](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span><span class="sxs-lookup"><span data-stu-id="1f6fc-201">To learn more, click [here](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span></span> <span data-ttu-id="1f6fc-202">Unutmayın `//` açıklamaları çizim için dahil edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-202">Note that the `//` comments have been included for illustration.</span></span> <span data-ttu-id="1f6fc-203">Bunları, gerçek bir istekte dahil etmeyin.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-203">Do not include them in an actual request.</span></span>

<span data-ttu-id="1f6fc-204">İstek görmek için aşağıdaki komutlardan birini çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="1f6fc-204">To see the request, run one of the following commands:</span></span>

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

<span data-ttu-id="1f6fc-205">`Create-User` Komutu bir .json dosyası olarak bir giriş parametresi alır.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-205">The `Create-User` command takes a .json file as an input parameter.</span></span> <span data-ttu-id="1f6fc-206">Bu, bir kullanıcı nesnesinin bir JSON temsili içerir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-206">This contains a JSON representation of a user object.</span></span> <span data-ttu-id="1f6fc-207">Örnek kodda iki örnek .json dosyası vardır: `usertemplate-email.json` ve `usertemplate-username.json`.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-207">There are two sample .json files in the sample code: `usertemplate-email.json` and `usertemplate-username.json`.</span></span> <span data-ttu-id="1f6fc-208">Bu dosyalar, gereksinimlerinize uyacak şekilde değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-208">You can modify these files to suit your needs.</span></span> <span data-ttu-id="1f6fc-209">Yukarıdaki gerekli alanlara ek olarak, bu dosyaları kullanabileceğiniz birkaç isteğe bağlı alanları dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-209">In addition to the required fields above, several optional fields that you can use are included in these files.</span></span> <span data-ttu-id="1f6fc-210">İsteğe bağlı alanları ayrıntıları bulunabilir [Azure AD Graph API varlık başvurusu](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span><span class="sxs-lookup"><span data-stu-id="1f6fc-210">Details on the optional fields can be found in the [Azure AD Graph API entity reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span></span>

<span data-ttu-id="1f6fc-211">POST isteğini nasıl oluşturulur görebilirsiniz `B2CGraphClient.SendGraphPostRequest(...)`.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-211">You can see how the POST request is constructed in `B2CGraphClient.SendGraphPostRequest(...)`.</span></span>

* <span data-ttu-id="1f6fc-212">Bir erişim belirteci iliştirir `Authorization` isteği üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-212">It attaches an access token to the `Authorization` header of the request.</span></span>
* <span data-ttu-id="1f6fc-213">Bu ayarlar `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-213">It sets `api-version=1.6`.</span></span>
* <span data-ttu-id="1f6fc-214">Bu JSON kullanıcı nesnesi istek gövdesinde içerir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-214">It includes the JSON user object in the body of the request.</span></span>

> [!NOTE]
> <span data-ttu-id="1f6fc-215">Varolan bir kullanıcı mağazadan geçirmek istediğiniz hesapları varsa, daha düşük parola gücünü [Azure AD B2C tarafından zorlanan güçlü parola gücünü](https://msdn.microsoft.com/library/azure/jj943764.aspx), güçlü parola kullanma gereksinimini devre dışı bırakabilirsiniz `DisableStrongPassword` değer `passwordPolicies` özelliği.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-215">If the accounts that you want to migrate from an existing user store has lower password strength than the [strong password strength enforced by Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), you can disable the strong password requirement using the `DisableStrongPassword` value in the `passwordPolicies` property.</span></span> <span data-ttu-id="1f6fc-216">Örneğin, yukarıdaki gibi sağlanan oluşturma Kullanıcı isteği değiştirebilirsiniz: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-216">For instance, you can modify the create user request provided above as follows: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span></span>
> 
> 

### <a name="update-consumer-user-accounts"></a><span data-ttu-id="1f6fc-217">Tüketici kullanıcı hesaplarını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="1f6fc-217">Update consumer user accounts</span></span>
<span data-ttu-id="1f6fc-218">Kullanıcı nesneleri güncelleştirdiğinizde, kullanıcı nesneleri oluşturmak için kullandığınız bir benzer bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-218">When you update user objects, the process is similar to the one you use to create user objects.</span></span> <span data-ttu-id="1f6fc-219">Ancak bu işlem HTTP kullanan `PATCH` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="1f6fc-219">But this process uses the HTTP `PATCH` method:</span></span>

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only the user's displayName
}
```

<span data-ttu-id="1f6fc-220">Bir kullanıcı yeni verilerle, JSON dosyalarınızın güncelleştirerek güncelleştirmeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-220">Try to update a user by updating your JSON files with new data.</span></span> <span data-ttu-id="1f6fc-221">Daha sonra kullanabilirsiniz `B2CGraphClient` aşağıdaki komutlardan birini çalıştırmak için:</span><span class="sxs-lookup"><span data-stu-id="1f6fc-221">You can then use `B2CGraphClient` to run one of these commands:</span></span>

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

<span data-ttu-id="1f6fc-222">İnceleme `B2CGraphClient.SendGraphPatchRequest(...)` bu isteği göndermek hakkında ayrıntılar için yöntem.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-222">Inspect the `B2CGraphClient.SendGraphPatchRequest(...)` method for details on how to send this request.</span></span>

### <a name="search-users"></a><span data-ttu-id="1f6fc-223">Kullanıcılarda arama</span><span class="sxs-lookup"><span data-stu-id="1f6fc-223">Search users</span></span>
<span data-ttu-id="1f6fc-224">B2C kiracınızda çeşitli şekillerde kullanıcılar için arama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-224">You can search for users in your B2C tenant in a couple of ways.</span></span> <span data-ttu-id="1f6fc-225">Kullanıcının kullanarak bir nesne kimliği veya kullanıcının oturum açma tanımlayıcı kullanarak iki (yani, `signInNames` özelliği).</span><span class="sxs-lookup"><span data-stu-id="1f6fc-225">One, using the user's object ID or two, using the user's sign-in identifer (i.e., the `signInNames` property).</span></span>

<span data-ttu-id="1f6fc-226">Belirli bir kullanıcı için aramak için aşağıdaki komutlardan birini çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="1f6fc-226">Run one of the following commands to search for a specific user:</span></span>

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

<span data-ttu-id="1f6fc-227">Aşağıda birkaç örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1f6fc-227">Here are a couple of examples:</span></span>

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a><span data-ttu-id="1f6fc-228">Kullanıcıları silme</span><span class="sxs-lookup"><span data-stu-id="1f6fc-228">Delete users</span></span>
<span data-ttu-id="1f6fc-229">Bir kullanıcının silinmesi için basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-229">The process for deleting a user is straightforward.</span></span> <span data-ttu-id="1f6fc-230">HTTP kullanmak `DELETE` yöntemi ve yapı doğru URL'nin nesne kimliği:</span><span class="sxs-lookup"><span data-stu-id="1f6fc-230">Use the HTTP `DELETE` method and construct the URL with the correct object ID:</span></span>

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="1f6fc-231">Bir örnek görmek için şu komutu girin ve konsola yazdırılır silme isteği görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="1f6fc-231">To see an example, enter this command and view the delete request that is printed to the console:</span></span>

```
> B2C Delete-User <object-id-of-user>
```

<span data-ttu-id="1f6fc-232">İnceleme `B2CGraphClient.SendGraphDeleteRequest(...)` bu isteği göndermek hakkında ayrıntılar için yöntem.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-232">Inspect the `B2CGraphClient.SendGraphDeleteRequest(...)` method for details on how to send this request.</span></span>

<span data-ttu-id="1f6fc-233">Azure AD grafik API'si kullanıcı yönetimine ek olarak birçok başka eylemler gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-233">You can perform many other actions with the Azure AD Graph API in addition to user management.</span></span> <span data-ttu-id="1f6fc-234">[Azure AD Graph API Başvurusu](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) örnek istekleri yanı sıra her bir eylemde ayrıntıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-234">The [Azure AD Graph API reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) provides details on each action, along with sample requests.</span></span>

## <a name="use-custom-attributes"></a><span data-ttu-id="1f6fc-235">Özel öznitelikler kullanma</span><span class="sxs-lookup"><span data-stu-id="1f6fc-235">Use custom attributes</span></span>
<span data-ttu-id="1f6fc-236">Çoğu tüketici uygulamaları herhangi bir tür özel kullanıcı profili bilgilerini depolamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-236">Most consumer applications need to store some type of custom user profile information.</span></span> <span data-ttu-id="1f6fc-237">Bunu yapmak için bir yolu, özel bir öznitelik B2C kiracınızda tanımlamaktır.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-237">One way you can do this is to define a custom attribute in your B2C tenant.</span></span> <span data-ttu-id="1f6fc-238">Sonra bu öznitelik bir kullanıcı nesnesi üzerinde herhangi bir özellik işle aynı şekilde davranabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-238">You can then treat that attribute the same way you treat any other property on a user object.</span></span> <span data-ttu-id="1f6fc-239">Öznitelik güncelleştirmek, öznitelik Sil, özniteliğin sorgu, öznitelik oturum açma belirteçleri ve daha fazla talep olarak gönder.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-239">You can update the attribute, delete the attribute, query by the attribute, send the attribute as a claim in sign-in tokens, and more.</span></span>

<span data-ttu-id="1f6fc-240">Özel bir öznitelik B2C kiracınızda tanımlamak için bkz: [B2C özel öznitelik başvurusu](active-directory-b2c-reference-custom-attr.md).</span><span class="sxs-lookup"><span data-stu-id="1f6fc-240">To define a custom attribute in your B2C tenant, see the [B2C custom attribute reference](active-directory-b2c-reference-custom-attr.md).</span></span>

<span data-ttu-id="1f6fc-241">B2C kiracınızda kullanarak tanımlanan özel özniteliklere görüntüleyebilirsiniz `B2CGraphClient`:</span><span class="sxs-lookup"><span data-stu-id="1f6fc-241">You can view the custom attributes defined in your B2C tenant by using `B2CGraphClient`:</span></span>

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

<span data-ttu-id="1f6fc-242">Bu işlevler çıktısı gibi her özel öznitelik ayrıntılarını ortaya çıkarır:</span><span class="sxs-lookup"><span data-stu-id="1f6fc-242">The output of these functions reveals the details of each custom attribute, such as:</span></span>

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

<span data-ttu-id="1f6fc-243">Tam adı gibi kullanabilir `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, kullanıcı nesneleri bir özellik olarak.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-243">You can use the full name, such as `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, as a property on your user objects.</span></span>  <span data-ttu-id="1f6fc-244">Yeni özellik ve özelliği için bir değer ile .json dosyanızı güncelleştirin ve ardından çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="1f6fc-244">Update your .json file with the new property and a value for the property, and then run:</span></span>

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

<span data-ttu-id="1f6fc-245">Kullanarak `B2CGraphClient`, B2C Kiracı kullanıcılarınızın program aracılığıyla yönetebilen bir hizmet uygulaması sahip.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-245">By using `B2CGraphClient`, you have a service application that can manage your B2C tenant users programmatically.</span></span> <span data-ttu-id="1f6fc-246">`B2CGraphClient`Azure AD grafik API'sine kimliğini doğrulamak için kendi uygulama kimliğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-246">`B2CGraphClient` uses its own application identity to authenticate to the Azure AD Graph API.</span></span> <span data-ttu-id="1f6fc-247">Ayrıca, istemci parolasını kullanarak belirteçleri da alır.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-247">It also acquires tokens by using a client secret.</span></span> <span data-ttu-id="1f6fc-248">Bu işlev uygulamanıza dahil, B2C uygulamalar için birkaç önemli nokta unutmayın:</span><span class="sxs-lookup"><span data-stu-id="1f6fc-248">As you incorporate this functionality into your application, remember a few key points for B2C apps:</span></span>

* <span data-ttu-id="1f6fc-249">Uygulama doğru Kiracı izinleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-249">You need to grant the application the proper permissions in the tenant.</span></span>
* <span data-ttu-id="1f6fc-250">Şimdilik, erişim belirteçleri almak için ADAL (MSAL değil) kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-250">For now, you need to use ADAL (not MSAL) to get access tokens.</span></span> <span data-ttu-id="1f6fc-251">(Ayrıca protokol iletilerini doğrudan bir kitaplık kullanılarak olmadan gönderebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="1f6fc-251">(You can also send protocol messages directly, without using a library.)</span></span>
* <span data-ttu-id="1f6fc-252">Grafik API'si çağırdığınızda, kullanabilirsiniz `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-252">When you call the Graph API, use `api-version=1.6`.</span></span>
* <span data-ttu-id="1f6fc-253">Oluşturduğunuzda ve tüketici kullanıcıları güncelleştirmek birkaç özelliği yukarıda açıklandığı gibi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-253">When you create and update consumer users, a few properties are required, as described above.</span></span>

<span data-ttu-id="1f6fc-254">Herhangi bir sorunuz veya Eylemler B2C kiracınızın grafik API'sini kullanarak gerçekleştirmek istediğiniz isteklerinde varsa, bu makalede bir yorum yazın veya bir sorunu GitHub kod örnek deposunda dosya.</span><span class="sxs-lookup"><span data-stu-id="1f6fc-254">If you have any questions or requests for actions you would like to perform by using the Graph API on your B2C tenant, leave a comment on this article or file an issue in the GitHub code sample repository.</span></span>

