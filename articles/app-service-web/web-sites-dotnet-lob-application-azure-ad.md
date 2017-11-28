---
title: "Azure Active Directory kimlik doğrulama iş Azure uygulamasıyla aaaCreate | Microsoft Docs"
description: "Bilgi nasıl toocreate bir ASP.NET MVC satır iş kolu uygulamanızın Azure App Service, kimlik doğrulamasını yapar Azure Active Directory ile"
services: app-service\web, active-directory
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: ad947bdb-4463-43ff-a5e3-91d9b2169b60
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 09/01/2016
ms.author: cephalin
ms.openlocfilehash: 3bcafad78ac0151889b3e336784cc561009f244f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a><span data-ttu-id="41f21-103">Azure Active Directory kimlik doğrulaması ile iş Azure uygulaması oluştur</span><span class="sxs-lookup"><span data-stu-id="41f21-103">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>
<span data-ttu-id="41f21-104">Bu makale size nasıl gösterir toocreate bir .NET satır iş kolu uygulaması [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) hello kullanarak [kimlik doğrulama / yetkilendirme](../app-service/app-service-authentication-overview.md) özelliği.</span><span class="sxs-lookup"><span data-stu-id="41f21-104">This article shows you how toocreate a .NET line-of-business app in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) using hello [Authentication / Authorization](../app-service/app-service-authentication-overview.md) feature.</span></span> <span data-ttu-id="41f21-105">Ayrıca gösterir nasıl toouse hello [Azure Active Directory grafik API'si](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) hello uygulamasındaki tooquery dizin verileri.</span><span class="sxs-lookup"><span data-stu-id="41f21-105">It also shows how toouse hello [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery directory data in hello application.</span></span>

<span data-ttu-id="41f21-106">kullandığınız hello Azure Active Directory Kiracı yalnızca Azure directory olabilir.</span><span class="sxs-lookup"><span data-stu-id="41f21-106">hello Azure Active Directory tenant that you use can be an Azure-only directory.</span></span> <span data-ttu-id="41f21-107">Veya olabilir [şirket içi Active Directory ile eşitlenen](../active-directory/active-directory-aadconnect.md) toocreate çoklu oturum açma deneyimini şirket içi ve uzak çalışanlar için.</span><span class="sxs-lookup"><span data-stu-id="41f21-107">Or, it can be [synced with your on-premises Active Directory](../active-directory/active-directory-aadconnect.md) toocreate a single sign-on experience for workers that are on-premises and remote.</span></span> <span data-ttu-id="41f21-108">Bu makalede Azure hesabınız için hello varsayılan dizini kullanır.</span><span class="sxs-lookup"><span data-stu-id="41f21-108">This article uses hello default directory for your Azure account.</span></span>

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="41f21-109">Yapı</span><span class="sxs-lookup"><span data-stu-id="41f21-109">What you will build</span></span>
<span data-ttu-id="41f21-110">App Service Web Apps basit bir iş kolu satır oluştur-okunur-güncelleştir-Sil (CRUD) uygulama parçaları ile Merhaba özellikler aşağıdaki öğeleri iş oluşturacak:</span><span class="sxs-lookup"><span data-stu-id="41f21-110">You will build a simple line-of-business Create-Read-Update-Delete (CRUD) application in App Service Web Apps that tracks work items with hello following features:</span></span>

* <span data-ttu-id="41f21-111">Azure Active Directory karşı kullanıcıların kimliğini doğrular</span><span class="sxs-lookup"><span data-stu-id="41f21-111">Authenticates users against Azure Active Directory</span></span>
* <span data-ttu-id="41f21-112">Sorgular directory kullanıcıları ve grupları kullanarak [Azure Active Directory grafik API'si](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span><span class="sxs-lookup"><span data-stu-id="41f21-112">Queries directory users and groups using [Azure Active Directory Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span></span>
* <span data-ttu-id="41f21-113">Kullanım hello ASP.NET MVC *doğrulaması yok* şablonu</span><span class="sxs-lookup"><span data-stu-id="41f21-113">Use hello ASP.NET MVC *No Authentication* template</span></span>

<span data-ttu-id="41f21-114">Azure'da satır iş kolu uygulamanız için rol tabanlı erişim denetimi (RBAC) gerekiyorsa, bkz: [sonraki adım](#next).</span><span class="sxs-lookup"><span data-stu-id="41f21-114">If you need role-based access control (RBAC) for your line-of-business app in Azure, see [Next Step](#next).</span></span>

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="41f21-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="41f21-115">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="41f21-116">Bu öğreticiyi toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="41f21-116">You need hello following toocomplete this tutorial:</span></span>

* <span data-ttu-id="41f21-117">Bir Azure Active Directory Kiracı çeşitli gruplarındaki kullanıcılar ile</span><span class="sxs-lookup"><span data-stu-id="41f21-117">An Azure Active Directory tenant with users in various groups</span></span>
* <span data-ttu-id="41f21-118">Hello Azure Active Directory kiracısı üzerinde izinleri toocreate uygulamalar</span><span class="sxs-lookup"><span data-stu-id="41f21-118">Permissions toocreate applications on hello Azure Active Directory tenant</span></span>
* <span data-ttu-id="41f21-119">Visual Studio 2013 güncelleştirme 4 veya üstü</span><span class="sxs-lookup"><span data-stu-id="41f21-119">Visual Studio 2013 Update 4 or later</span></span>
* [<span data-ttu-id="41f21-120">Azure SDK 2.8.1 ile veya daha yenisi</span><span class="sxs-lookup"><span data-stu-id="41f21-120">Azure SDK 2.8.1 or later</span></span>](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-tooazure"></a><span data-ttu-id="41f21-121">Oluşturma ve bir web uygulaması tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="41f21-121">Create and deploy a web app tooAzure</span></span>
1. <span data-ttu-id="41f21-122">Visual Studio'dan tıklatın **dosya** > **yeni** > **proje**.</span><span class="sxs-lookup"><span data-stu-id="41f21-122">From Visual Studio, click **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="41f21-123">Seçin **ASP.NET Web uygulaması**, projenizi adlandırın ve tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="41f21-123">Select **ASP.NET Web Application**, name your project, and click **OK**.</span></span>
3. <span data-ttu-id="41f21-124">Select hello **MVC** şablon hello kimlik doğrulaması da değiştirmem**doğrulaması yok**.</span><span class="sxs-lookup"><span data-stu-id="41f21-124">Select hello **MVC** template, then change hello authentication too**No Authentication**.</span></span> <span data-ttu-id="41f21-125">Emin olun **hello bulut ana** seçilir ve tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="41f21-125">Make sure **Host in hello Cloud** is selected and click **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. <span data-ttu-id="41f21-126">Merhaba, **App Service Oluştur** iletişim kutusunda, tıklatın **Hesap Ekle** (ve ardından **Hesap Ekle** hello açılır içinde) tooyour Azure hesabı toolog.</span><span class="sxs-lookup"><span data-stu-id="41f21-126">In hello **Create App Service** dialog, click **Add an account** (and then **Add an account** in hello dropdown) toolog in tooyour Azure account.</span></span>
5. <span data-ttu-id="41f21-127">Oturum açtıktan sonra web uygulamanızı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="41f21-127">Once logged in configure your web app.</span></span> <span data-ttu-id="41f21-128">Merhaba ilgili tıklayarak bir kaynak grubu ve yeni bir uygulama hizmeti planı oluştur **yeni** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="41f21-128">Create a resource group and a new App Service plan by clicking hello respective **New** button.</span></span> <span data-ttu-id="41f21-129">Tıklatın **diğer Azure hizmetlerini keşfedin** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="41f21-129">Click **Explore additional Azure services** toocontinue.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. <span data-ttu-id="41f21-130">Merhaba, **Hizmetleri** sekmesini tıklatın,  **+**  tooadd uygulamanız için bir SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="41f21-130">In hello **Services** tab, click **+** tooadd a SQL Database for your app.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. <span data-ttu-id="41f21-131">İçinde **SQL veritabanını yapılandırma**, tıklatın **yeni** toocreate bir SQL Server örneği.</span><span class="sxs-lookup"><span data-stu-id="41f21-131">In **Configure SQL Database**, click **New** toocreate a SQL Server instance.</span></span>
8. <span data-ttu-id="41f21-132">İçinde **SQL Server'ı Yapılandır**, SQL Server örneğinizi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="41f21-132">In **Configure SQL Server**, configure your SQL Server instance.</span></span> <span data-ttu-id="41f21-133">Ardından **Tamam**, **Tamam**, ve **oluşturma** tookick azure'da hello uygulama oluşturma devre dışı.</span><span class="sxs-lookup"><span data-stu-id="41f21-133">Then, click **OK**, **OK**, and **Create** tookick off hello app creation in Azure.</span></span>
9. <span data-ttu-id="41f21-134">İçinde **Azure App Service etkinliği**, başlangıç uygulaması oluşturma işleminin bittiği görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41f21-134">In **Azure App Service Activity**, you can see when hello app creation is finished.</span></span> <span data-ttu-id="41f21-135">Tıklatın  **Yayımla &lt;* appname*> toothis Web uygulaması şimdi **, ardından **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="41f21-135">Click **Publish &lt;*appname*> toothis Web App now**, then click **Publish**.</span></span> 
   
    <span data-ttu-id="41f21-136">Visual Studio tamamlandıktan sonra hello açar uygulama yayımlama hello tarayıcıda.</span><span class="sxs-lookup"><span data-stu-id="41f21-136">Once Visual Studio finishes, it opens hello publish app in hello browser.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a><span data-ttu-id="41f21-137">Kimlik doğrulama ve dizin erişimi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="41f21-137">Configure authentication and directory access</span></span>
1. <span data-ttu-id="41f21-138">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="41f21-138">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="41f21-139">Merhaba sol menüden **uygulama hizmetleri** > **&lt;*appname*> ** > **kimlik doğrulama / yetkilendirme**.</span><span class="sxs-lookup"><span data-stu-id="41f21-139">From hello left menu, click **App Services** > **&lt;*appname*>** > **Authentication / Authorization**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. <span data-ttu-id="41f21-140">Azure Active Directory authentication'ı tıklatarak açmak **üzerinde** > **Azure Active Directory** > **Express** > **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="41f21-140">Turn on Azure Active Directory authentication by clicking **On** > **Azure Active Directory** > **Express** > **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. <span data-ttu-id="41f21-141">Tıklatın **kaydetmek** hello komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="41f21-141">Click **Save** in hello command bar.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    <span data-ttu-id="41f21-142">Merhaba kimlik doğrulama ayarları başarıyla kaydedildi sonra tooyour uygulamayı yeniden hello tarayıcıda gezinme deneyin.</span><span class="sxs-lookup"><span data-stu-id="41f21-142">Once hello authentication settings are saved successfully, try navigating tooyour app again in hello browser.</span></span> <span data-ttu-id="41f21-143">Varsayılan ayarlarınızı hello tüm uygulama kimlik doğrulamasını zorunlu.</span><span class="sxs-lookup"><span data-stu-id="41f21-143">Your default settings enforce authentication on hello whole app.</span></span> <span data-ttu-id="41f21-144">Zaten oturum açmadıysanız, yeniden yönlendirilen tooa oturum açma ekranı olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="41f21-144">If you aren't already logged in, you are redirected tooa login screen.</span></span> <span data-ttu-id="41f21-145">Oturum açtıktan sonra uygulamanızı HTTPS ile güvenli bakın.</span><span class="sxs-lookup"><span data-stu-id="41f21-145">Once logged in, you see your app secured by HTTPS.</span></span> <span data-ttu-id="41f21-146">Ardından, tooenable erişim toodirectory veri gerekir.</span><span class="sxs-lookup"><span data-stu-id="41f21-146">Next, you need tooenable access toodirectory data.</span></span> 
5. <span data-ttu-id="41f21-147">Toohello gidin [Klasik portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="41f21-147">Navigate toohello [classic portal](https://manage.windowsazure.com).</span></span>
6. <span data-ttu-id="41f21-148">Merhaba sol menüden **Active Directory** > **varsayılan dizin** > **uygulamaları**  >   **&lt;* appname*> **.</span><span class="sxs-lookup"><span data-stu-id="41f21-148">From hello left menu, click **Active Directory** > **Default Directory** > **Applications** > **&lt;*appname*>**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    <span data-ttu-id="41f21-149">Uygulama hizmeti, tooenable hello için yetkilendirme oluşturulan hello Azure Active Directory Uygulama budur / kimlik doğrulama özelliği.</span><span class="sxs-lookup"><span data-stu-id="41f21-149">This is hello Azure Active Directory application that App Service created for you tooenable hello Authorization / Authentication feature.</span></span>
7. <span data-ttu-id="41f21-150">Tıklatın **kullanıcılar** ve **grupları** toomake, bazı kullanıcılar ve gruplar hello dizinine sahip olduğunuzdan emin.</span><span class="sxs-lookup"><span data-stu-id="41f21-150">Click **Users** and **Groups** toomake sure that you have some users and groups in hello directory.</span></span> <span data-ttu-id="41f21-151">Değilse, birkaç test kullanıcıları ve grupları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41f21-151">If not, create a few test users and groups.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. <span data-ttu-id="41f21-152">Tıklatın **yapılandırma** tooconfigure bu uygulama.</span><span class="sxs-lookup"><span data-stu-id="41f21-152">Click **Configure** tooconfigure this application.</span></span>
9. <span data-ttu-id="41f21-153">Toohello aşağı **anahtarları** bölüm ve bir süre seçerek bir anahtar ekleyin.</span><span class="sxs-lookup"><span data-stu-id="41f21-153">Scroll down toohello **Keys** section and add a key by selecting a duration.</span></span> <span data-ttu-id="41f21-154">Ardından **izinlere temsilci** seçip **dizin verilerini okuma**.</span><span class="sxs-lookup"><span data-stu-id="41f21-154">Then, click **Delegated Permissions** and select **Read directory data**.</span></span> 
   <span data-ttu-id="41f21-155">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="41f21-155">Click **Save**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. <span data-ttu-id="41f21-156">Ayarlarınız kaydedildikten sonra geri toohello kaydırma **anahtarları** hello'ye tıklayın **kopyalama** düğmesini toocopy hello istemci anahtarı.</span><span class="sxs-lookup"><span data-stu-id="41f21-156">Once your settings are saved, scroll back up toohello **Keys** section and click hello **Copy** button toocopy hello client key.</span></span> 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="41f21-157">Bu sayfayı terk şimdi giderseniz, bu istemci anahtar herhangi bir zamanda yeniden mümkün tooaccess olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="41f21-157">If you navigate away from this page now, you won't be able tooaccess this client key ever again.</span></span>
    > 
    > 
11. <span data-ttu-id="41f21-158">Ardından, tooconfigure bu anahtarla web uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="41f21-158">Next, you need tooconfigure your web app with this key.</span></span> <span data-ttu-id="41f21-159">İçinde toohello oturum [Azure kaynak Gezgini](https://resources.azure.com) Azure hesabınızla.</span><span class="sxs-lookup"><span data-stu-id="41f21-159">Log in toohello [Azure Resource Explorer](https://resources.azure.com) with your Azure account.</span></span>
12. <span data-ttu-id="41f21-160">Merhaba hello sayfanın en üstünde, tıklatın **okuma/yazma** toomake değişiklikleri hello Azure kaynak Gezgini.</span><span class="sxs-lookup"><span data-stu-id="41f21-160">At hello top of hello page, click **Read/Write** toomake changes in hello Azure Resource Explorer.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. <span data-ttu-id="41f21-161">Hello abonelikleri bulunan uygulamanız için kimlik doğrulama ayarlarını Bul >  **&lt;* varlığıyla subscriptionname*> ** > **resourceGroups**  >   **&lt;* resourcegroupname*> ** > **sağlayıcıları** > **Microsoft.Web**  >  **siteleri** > **&lt;*appname*> ** > **config**  >  **authsettings**.</span><span class="sxs-lookup"><span data-stu-id="41f21-161">Find hello authentication settings for your app, located at subscriptions > **&lt;*subscriptionname*>** > **resourceGroups** > **&lt;*resourcegroupname*>** > **providers** > **Microsoft.Web** > **sites** > **&lt;*appname*>** > **config** > **authsettings**.</span></span>
14. <span data-ttu-id="41f21-162">**Düzenle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="41f21-162">Click **Edit**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. <span data-ttu-id="41f21-163">Hello bölmesini düzenleme hello ayarlamak `clientSecret` ve `additionalLoginParams` aşağıdaki gibi özellikleri.</span><span class="sxs-lookup"><span data-stu-id="41f21-163">In hello editing pane, set hello `clientSecret` and `additionalLoginParams` properties as follows.</span></span>
    
        ...
        "clientSecret": "<client key from hello Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. <span data-ttu-id="41f21-164">Tıklatın **Put** en üst toosubmit değişikliklerinizi hello.</span><span class="sxs-lookup"><span data-stu-id="41f21-164">Click **Put** at hello top toosubmit your changes.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. <span data-ttu-id="41f21-165">Şimdi, tooaccess hello Azure Active Directory grafik API'sini belirteci, yalnızca gidin hello yetkilendirme varsa tootest  **https://&lt;*appname*> içinde.azurewebsites.net/.auth/me**, Tarayıcı.</span><span class="sxs-lookup"><span data-stu-id="41f21-165">Now, tootest if you have hello authorization token tooaccess hello Azure Active Directory Graph API, just navigate to **https://&lt;*appname*>.azurewebsites.net/.auth/me** in your browser.</span></span> <span data-ttu-id="41f21-166">Her şeyin doğru şekilde yapılandırdıysanız, hello görmelisiniz `access_token` hello JSON yanıt özelliği.</span><span class="sxs-lookup"><span data-stu-id="41f21-166">If you configured everything correctly, you should see hello `access_token` property in hello JSON response.</span></span>
    
    <span data-ttu-id="41f21-167">Merhaba `~/.auth/me` URL yolu App Service kimlik doğrulaması tarafından yönetilen /, tüm hello ilgili bilgileri kimlik doğrulaması tooyour oturumu yetkilendirme toogive.</span><span class="sxs-lookup"><span data-stu-id="41f21-167">hello `~/.auth/me` URL path is managed by App Service Authentication / Authorization toogive you all hello information related tooyour authenticated session.</span></span> <span data-ttu-id="41f21-168">Daha fazla bilgi için bkz: [kimlik doğrulama ve yetkilendirme Azure App Service'te](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="41f21-168">For more information, see [Authentication and authorization in Azure App Service](../app-service/app-service-authentication-overview.md).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="41f21-169">Merhaba `access_token` bir sona erme süresi vardır.</span><span class="sxs-lookup"><span data-stu-id="41f21-169">hello `access_token` has an expiration period.</span></span> <span data-ttu-id="41f21-170">Ancak, App Service kimlik doğrulama / yetkilendirme belirteci yenileme işlevleri ile sağlayan `~/.auth/refresh`.</span><span class="sxs-lookup"><span data-stu-id="41f21-170">However, App Service Authentication / Authorization provides token refresh functionality with `~/.auth/refresh`.</span></span> <span data-ttu-id="41f21-171">Hakkında daha fazla bilgi için toouse, bkz: [App Service Belirteç Deposu](https://cgillum.tech/2016/03/07/app-service-token-store/).</span><span class="sxs-lookup"><span data-stu-id="41f21-171">For more information on how toouse it, see [App Service Token Store](https://cgillum.tech/2016/03/07/app-service-token-store/).</span></span>
    > 
    > 

<span data-ttu-id="41f21-172">Ardından, dizin verileri ile faydalı bir şey yapar.</span><span class="sxs-lookup"><span data-stu-id="41f21-172">Next, you will do something useful with directory data.</span></span>

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-tooyour-app"></a><span data-ttu-id="41f21-173">İş işlevselliği tooyour uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="41f21-173">Add line-of-business functionality tooyour app</span></span>
<span data-ttu-id="41f21-174">Şimdi, basit bir CRUD iş öğeleri İzleyici oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41f21-174">Now, you create a simple CRUD work items tracker.</span></span>  

1. <span data-ttu-id="41f21-175">Merhaba ~\Models klasöründe WorkItem.cs adlı bir sınıf dosyası oluşturun ve değiştirin `public class WorkItem {...}` koddan hello ile:</span><span class="sxs-lookup"><span data-stu-id="41f21-175">In hello ~\Models folder, create a class file called WorkItem.cs, and replace `public class WorkItem {...}` with hello following code:</span></span>
   
     <span data-ttu-id="41f21-176">System.ComponentModel.DataAnnotations kullanarak;</span><span class="sxs-lookup"><span data-stu-id="41f21-176">using System.ComponentModel.DataAnnotations;</span></span>
   
     <span data-ttu-id="41f21-177">İş öğesi {ortak sınıfı</span><span class="sxs-lookup"><span data-stu-id="41f21-177">public class WorkItem   {</span></span>
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     <span data-ttu-id="41f21-178">}</span><span class="sxs-lookup"><span data-stu-id="41f21-178">}</span></span>
   
     <span data-ttu-id="41f21-179">Ortak enum WorkItemStatus {</span><span class="sxs-lookup"><span data-stu-id="41f21-179">public enum WorkItemStatus   {</span></span>
   
         Open,
         Investigating,
         Resolved,
         Closed
     <span data-ttu-id="41f21-180">}</span><span class="sxs-lookup"><span data-stu-id="41f21-180">}</span></span>
2. <span data-ttu-id="41f21-181">Merhaba proje toomake yeni model erişilebilir toohello yapı iskelesi mantığınızı Visual Studio'da derleme.</span><span class="sxs-lookup"><span data-stu-id="41f21-181">Build hello project toomake your new model accessible toohello scaffolding logic in Visual Studio.</span></span>
3. <span data-ttu-id="41f21-182">Yeni iskele kurulmuş Öğe Ekle `WorkItemsController` toohello ~\Controllers klasörü (sağ **denetleyicileri**, çok noktası**Ekle**seçip **yeni iskele kurulmuş öğe**).</span><span class="sxs-lookup"><span data-stu-id="41f21-182">Add a new scaffolded item `WorkItemsController` toohello ~\Controllers folder (right-click **Controllers**, point too**Add**, and select **New scaffolded item**).</span></span> 
4. <span data-ttu-id="41f21-183">Seçin **Entity Framework kullanarak MVC 5 denetleyici, görünümleri olan** tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="41f21-183">Select **MVC 5 Controller with views, using Entity Framework** and click **Add**.</span></span>
5. <span data-ttu-id="41f21-184">Oluşturduğunuz select hello modeli ardından  **+**  ve ardından **Ekle** tooadd bir veri bağlamı ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="41f21-184">Select hello model that you created, then click **+** and then **Add** tooadd a data context, and then click **Add**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. <span data-ttu-id="41f21-185">Merhaba ~\Views\WorkItems\Create.cshtml (otomatik olarak kurulmuş bir öğe), bulma `Html.BeginForm` yardımcı yöntem ve hello aşağıdaki vurgulanan değişiklikler yapın:</span><span class="sxs-lookup"><span data-stu-id="41f21-185">In ~\Views\WorkItems\Create.cshtml (an automatically scaffolded item), find hello `Html.BeginForm` helper method and make hello following highlighted changes:</span></span>  
   
   <pre class="prettyprint">
   @model WebApplication1.Models.WorkItem
   
   @{
    ViewBag.Title = &quot;Create&quot;;
   }
   
   &lt;h2&gt;Create&lt;/h2&gt;
   
   @using (Html.BeginForm(<mark>&quot;Create&quot;, &quot;WorkItems&quot;, FormMethod.Post, new { id = &quot;main-form&quot; }</mark>)) 
   {
    @Html.AntiForgeryToken()
   
    &lt;div class=&quot;form-horizontal&quot;&gt;
        &lt;h4&gt;WorkItem&lt;/h4&gt;
        &lt;hr /&gt;
        @Html.ValidationSummary(true, &quot;&quot;, new { @class = &quot;text-danger&quot; })
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToID, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToID, new { htmlAttributes = new { @class = &quot;form-control&quot;<mark>, @type = &quot;hidden&quot;</mark> } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToID, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToName, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToName, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToName, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Description, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.Description, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.Description, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EnumDropDownListFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;form-control&quot; })
                @Html.ValidationMessageFor(model =&gt; model.Status, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            &lt;div class=&quot;col-md-offset-2 col-md-10&quot;&gt;
                &lt;input type=&quot;submit&quot; value=&quot;Create&quot; class=&quot;btn btn-default&quot;<mark> id=&quot;submit-button&quot;</mark> /&gt;
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
   }
   
   &lt;div&gt;
    @Html.ActionLink(&quot;Back tooList&quot;, &quot;Index&quot;)
   &lt;/div&gt;
   
   @section Scripts {
    @Scripts.Render(&quot;~/bundles/jqueryval&quot;)
    <mark>&lt;script&gt;
        // People/Group Picker Code
        var maxResultsPerPage = 14;
        var input = document.getElementById(&quot;AssignedToName&quot;);
   
        // Access token from request header, and tenantID from claims identity
        var token = &quot;@Request.Headers[&quot;X-MS-TOKEN-AAD-ACCESS-TOKEN&quot;]&quot;;
        var tenant =&quot;@(System.Security.Claims.ClaimsPrincipal.Current.Claims
                        .Where(c => c.Type == &quot;http://schemas.microsoft.com/identity/claims/tenantid&quot;)
                        .Select(c => c.Value).SingleOrDefault())&quot;;
   
        var picker = new AadPicker(maxResultsPerPage, input, token, tenant);
   
        // Submit hello selected user/group toobe asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   <span data-ttu-id="41f21-186">Unutmayın `token` ve `tenant` hello tarafından kullanılan `AadPicker` nesne toomake Azure Active Directory grafik API'sini çağırır.</span><span class="sxs-lookup"><span data-stu-id="41f21-186">Note that `token` and `tenant` are used by hello `AadPicker` object toomake Azure Active Directory Graph API calls.</span></span> <span data-ttu-id="41f21-187">Ekleyeceksiniz `AadPicker` daha sonra.</span><span class="sxs-lookup"><span data-stu-id="41f21-187">You'll add `AadPicker` later.</span></span>     
   
   > [!NOTE]
   > <span data-ttu-id="41f21-188">Yalnızca de alabilirsiniz `token` ve `tenant` hello istemci tarafındaki ile `~/.auth/me`, ancak bu bir ek sunucu araması olacaktır.</span><span class="sxs-lookup"><span data-stu-id="41f21-188">You can just as well get `token` and `tenant` from hello client side with `~/.auth/me`, but that would be an additional server call.</span></span> <span data-ttu-id="41f21-189">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="41f21-189">For example:</span></span>
   > 
   > <span data-ttu-id="41f21-190">$.ajax ({veri türü: "json", url: "/.auth/me", başarı: işlevi (veri) {var belirteci verileri [0] = .access_token; var Kiracı verileri [0] .user_claims .find = (c = > c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val;}});</span><span class="sxs-lookup"><span data-stu-id="41f21-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span></span>
   > 
   > 
7. <span data-ttu-id="41f21-191">Merhaba sahip aynı değişiklik ~ \Views\WorkItems\Edit.cshtml.</span><span class="sxs-lookup"><span data-stu-id="41f21-191">Make hello same changes with ~\Views\WorkItems\Edit.cshtml.</span></span>
8. <span data-ttu-id="41f21-192">Merhaba `AadPicker` nesne tanımlanmış bir betikte tooadd tooyour proje gerekir.</span><span class="sxs-lookup"><span data-stu-id="41f21-192">hello `AadPicker` object is defined in a script that you need tooadd tooyour project.</span></span> <span data-ttu-id="41f21-193">Merhaba ~\Scripts klasöre sağ tıklayın, çok noktası**Ekle**, tıklatıp **JavaScript dosyası**.</span><span class="sxs-lookup"><span data-stu-id="41f21-193">Right-click hello ~\Scripts folder, point too**Add**, and click **JavaScript file**.</span></span> <span data-ttu-id="41f21-194">Tür `AadPickerLibrary` hello filename ve tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="41f21-194">Type `AadPickerLibrary` for hello filename and click **OK**.</span></span>
9. <span data-ttu-id="41f21-195">Merhaba içeriğine kopyalama [burada](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) içine ~ \Scripts\AadPickerLibrary.js.</span><span class="sxs-lookup"><span data-stu-id="41f21-195">Copy hello content from [here](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) into ~\Scripts\AadPickerLibrary.js.</span></span>
   
   <span data-ttu-id="41f21-196">Merhaba komut dosyasında hello `AadPicker` nesne çağrıları [Azure Active Directory grafik API'si](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch kullanıcıların ve grupların hello giriş eşleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="41f21-196">In hello script, hello `AadPicker` object calls [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch for users and groups that match hello input.</span></span>  
10. <span data-ttu-id="41f21-197">~\Scripts\AadPickerLibrary.js de hello kullanır [jQuery UI otomatik tamamlama pencere](https://jqueryui.com/autocomplete/).</span><span class="sxs-lookup"><span data-stu-id="41f21-197">~\Scripts\AadPickerLibrary.js also uses hello [jQuery UI Autocomplete widget](https://jqueryui.com/autocomplete/).</span></span> <span data-ttu-id="41f21-198">Bu nedenle tooadd jQuery UI tooyour proje gerekir.</span><span class="sxs-lookup"><span data-stu-id="41f21-198">So you need tooadd jQuery UI tooyour project.</span></span> <span data-ttu-id="41f21-199">Projenize sağ tıklatın ve **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="41f21-199">Right-click your project in and click **Manage NuGet Packages**.</span></span>
11. <span data-ttu-id="41f21-200">Hello NuGet Paket Yöneticisi, Gözat ' ı tıklatın. türü **jquery UI** hello arama çubuğu ve tıklatın **jQuery.UI.Combined**.</span><span class="sxs-lookup"><span data-stu-id="41f21-200">In hello NuGet Package Manager, click Browse, type **jquery-ui** in hello search bar, and click **jQuery.UI.Combined**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. <span data-ttu-id="41f21-201">Merhaba sağ bölmede **yükleme**, ardından **Tamam** tooproceed.</span><span class="sxs-lookup"><span data-stu-id="41f21-201">In hello right pane, click **Install**, then click **OK** tooproceed.</span></span>
13. <span data-ttu-id="41f21-202">~\App_Start\BundleConfig.cs açın ve aşağıdaki vurgulanan değişiklikler hello yapın:</span><span class="sxs-lookup"><span data-stu-id="41f21-202">Open ~\App_Start\BundleConfig.cs and make hello following highlighted changes:</span></span>  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
        // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
        bundles.Add(new ScriptBundle(&quot;~/bundles/modernizr&quot;).Include(
                    &quot;~/Scripts/modernizr-*&quot;));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/bootstrap&quot;).Include(
                    &quot;~/Scripts/bootstrap.js&quot;,
                    &quot;~/Scripts/respond.js&quot;));
    
        bundles.Add(new StyleBundle(&quot;~/Content/css&quot;).Include(
                    &quot;~/Content/bootstrap.css&quot;,
                    &quot;~/Content/site.css&quot;<mark>,
                    &quot;~/Content/themes/base/jquery-ui.css&quot;</mark>));
    }
    </pre>
    
    <span data-ttu-id="41f21-203">Daha fazla kullanıcı yolu toomanage JavaScript ve CSS dosyaları, uygulamanızda vardır.</span><span class="sxs-lookup"><span data-stu-id="41f21-203">There are more performant ways toomanage JavaScript and CSS files in your app.</span></span> <span data-ttu-id="41f21-204">Ancak, kolaylık sağlamak için yalnızca toopiggyback her görünümü ile yüklenen hello paketleri üzerinde oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="41f21-204">However, for simplicity you're just going toopiggyback on hello bundles that are loaded with every view.</span></span>
14. <span data-ttu-id="41f21-205">Son olarak, içinde ~ \Global.asax, hello kod satırı aşağıdaki hello eklemek `Application_Start()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="41f21-205">Finally, in ~\Global.asax, add hello following line of code in hello `Application_Start()` method.</span></span> <span data-ttu-id="41f21-206">`Ctrl`+`.`Her adlandırma çözümleme hatası çok Düzelt.</span><span class="sxs-lookup"><span data-stu-id="41f21-206">`Ctrl`+`.` on each naming resolution error too fix it.</span></span>
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > <span data-ttu-id="41f21-207">Merhaba varsayılan MVC şablonundaki kullandığından bu kod satırı gereksinim <code>[ValidateAntiForgeryToken]</code> decoration bazı hello eylemler.</span><span class="sxs-lookup"><span data-stu-id="41f21-207">You need this line of code because hello default MVC template uses <code>[ValidateAntiForgeryToken]</code> decoration on some of hello actions.</span></span> <span data-ttu-id="41f21-208">Tarafından açıklanan toohello davranışı nedeniyle [Brock Allen](https://twitter.com/BrockLAllen) adresindeki [MVC 4, AntiForgeryToken ve talep](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) HTTP POST sahteciliğe karşı koruma belirteci doğrulaması başarısız:</span><span class="sxs-lookup"><span data-stu-id="41f21-208">Due toohello behavior described by [Brock Allen](https://twitter.com/BrockLAllen) at [MVC 4, AntiForgeryToken and Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) your HTTP POST may fail anti-forgery token validation because:</span></span>
    > 
    > * <span data-ttu-id="41f21-209">Azure Active Directory, varsayılan olarak hello sahteciliğe karşı koruma belirteci tarafından gerekli olan hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider göndermez.</span><span class="sxs-lookup"><span data-stu-id="41f21-209">Azure Active Directory does not send hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, which is required by default by hello anti-forgery token.</span></span>
    > * <span data-ttu-id="41f21-210">Azure Active Directory dizin AD FS ile eşitlenen ise, AD FS toosend el ile yapılandırabilmenize karşın hello AD FS güven varsayılan hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider talep ya da, göndermez Bu talep.</span><span class="sxs-lookup"><span data-stu-id="41f21-210">If Azure Active Directory is directory synced with AD FS, hello AD FS trust by default does not send hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider claim either, although you can manually configure AD FS toosend this claim.</span></span>
    > 
    > <span data-ttu-id="41f21-211">`ClaimTypes.NameIdentifies`Merhaba talep belirtir `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, hangi Azure Active Directory sağlayın.</span><span class="sxs-lookup"><span data-stu-id="41f21-211">`ClaimTypes.NameIdentifies` specifies hello claim `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, which Azure Active Directory does supply.</span></span>  
    > 
    > 
15. <span data-ttu-id="41f21-212">Şimdi, değişikliklerinizi yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="41f21-212">Now, publish your changes.</span></span> <span data-ttu-id="41f21-213">Projenize sağ tıklatın ve **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="41f21-213">Right-click your project and click **Publish**.</span></span>
16. <span data-ttu-id="41f21-214">Tıklatın **ayarları**olduğunu denetleyin bir bağlantı dizesi tooyour SQL veritabanı, seçin **güncelleştirme veritabanı** toomake hello modeliniz için şema değişiklikleri ve tıklayın **Yayımla** .</span><span class="sxs-lookup"><span data-stu-id="41f21-214">Click **Settings**, make sure there is a connection string tooyour SQL Database, select **Update Database** toomake hello schema changes for your model, and click **Publish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. <span data-ttu-id="41f21-215">Merhaba tarayıcıda toohttps gidin: / /&lt;*appname*> tıklayın ve.azurewebsites.net/workitems **Yeni Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="41f21-215">In hello browser, navigate toohttps://&lt;*appname*>.azurewebsites.net/workitems and click **Create New**.</span></span>
18. <span data-ttu-id="41f21-216">Tıklatın hello **AssignedToName** kutusu.</span><span class="sxs-lookup"><span data-stu-id="41f21-216">Click in hello **AssignedToName** box.</span></span> <span data-ttu-id="41f21-217">Artık Azure Active Directory kiracınızda bir açılır kullanıcılar ve gruplar da görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="41f21-217">You should now see users and groups from your Azure Active Directory tenant in a dropdown.</span></span> <span data-ttu-id="41f21-218">Toofilter yazın veya hello kullanın `Up` veya `Down` anahtar veya tooselect hello kullanıcıyı veya grubu tıklatın.</span><span class="sxs-lookup"><span data-stu-id="41f21-218">You can type toofilter, or use hello `Up` or `Down` key or click tooselect hello user or group.</span></span> 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. <span data-ttu-id="41f21-219">Tıklatın **oluşturma** toosave hello değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="41f21-219">Click **Create** toosave hello changes.</span></span> <span data-ttu-id="41f21-220">Ardından **Düzenle** oluşturulan hello çalışma öğesi tooobserve hello aynı davranışı.</span><span class="sxs-lookup"><span data-stu-id="41f21-220">Then, click **Edit** on hello created work item tooobserve hello same behavior.</span></span>

<span data-ttu-id="41f21-221">Congrats, artık bir iş kolu satır uygulama Azure'da dizin erişimle çalıştırdığınız!</span><span class="sxs-lookup"><span data-stu-id="41f21-221">Congrats, you are now running a line-of-business app in Azure with directory access!</span></span> <span data-ttu-id="41f21-222">Grafik API'si hello ile yapabileceğiniz çok daha fazla yoktur.</span><span class="sxs-lookup"><span data-stu-id="41f21-222">There's a lot more you can do with hello Graph API.</span></span> <span data-ttu-id="41f21-223">Bkz: [Azure AD Graph API Başvurusu](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span><span class="sxs-lookup"><span data-stu-id="41f21-223">See [Azure AD Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span></span>

<a name="next"></a>

## <a name="next-step"></a><span data-ttu-id="41f21-224">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="41f21-224">Next Step</span></span>
<span data-ttu-id="41f21-225">Azure'da satır iş kolu uygulamanız için rol tabanlı erişim denetimi (RBAC) gerekiyorsa, bkz: [WebApp RoleClaims DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) hello Azure Active Directory ekibinden bir örnek için.</span><span class="sxs-lookup"><span data-stu-id="41f21-225">If you need role-based access control (RBAC) for your line-of-business app in azure, see [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) for a sample from hello Azure Active Directory team.</span></span> <span data-ttu-id="41f21-226">Size bir nasıl gösterir Azure Active Directory uygulamanız için tooenable rolleri ve hello kullanıcılar yetki `[Authorize]` decoration.</span><span class="sxs-lookup"><span data-stu-id="41f21-226">It shows you how tooenable roles for your Azure Active Directory application, and then authorize users with hello `[Authorize]` decoration.</span></span>

<span data-ttu-id="41f21-227">İş uygulamanızı tooon içi veri erişimi gerektirir, bkz: [erişim şirket içi Azure App Service içinde karma bağlantılar kullanarak kaynakları](web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="41f21-227">If your line-of-business app needs access tooon-premises data, see [Access on-premises resources using hybrid connections in Azure App Service](web-sites-hybrid-connection-get-started.md).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="41f21-228">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="41f21-228">Further resources</span></span>
* [<span data-ttu-id="41f21-229">Kimlik doğrulama ve yetkilendirme Azure uygulama hizmeti</span><span class="sxs-lookup"><span data-stu-id="41f21-229">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)
* [<span data-ttu-id="41f21-230">Azure uygulamanızı şirket içi Active Directory ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="41f21-230">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="41f21-231">AD FS kimlik doğrulaması ile bir satır iş kolu uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="41f21-231">Create a line-of-business app in Azure with AD FS authentication</span></span>](web-sites-dotnet-lob-application-adfs.md)
* [<span data-ttu-id="41f21-232">Uygulama hizmeti kimlik doğrulama ve hello Azure AD grafik API'si</span><span class="sxs-lookup"><span data-stu-id="41f21-232">App Service Auth and hello Azure AD Graph API</span></span>](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [<span data-ttu-id="41f21-233">Microsoft Azure Active Directory örnekler ve belgeler</span><span class="sxs-lookup"><span data-stu-id="41f21-233">Microsoft Azure Active Directory Samples and Documentation</span></span>](https://github.com/AzureADSamples)
* [<span data-ttu-id="41f21-234">Azure Active Directory desteklenen belirteç ve talep türleri</span><span class="sxs-lookup"><span data-stu-id="41f21-234">Azure Active Directory Supported Token and Claim Types</span></span>](http://msdn.microsoft.com/library/azure/dn195587.aspx)
