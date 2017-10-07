---
title: "Azure portal uygulaması aaaCreate kimlik | Microsoft Docs"
description: "Toocreate yeni bir Azure Active Directory uygulaması ve hizmet sorumlusu Azure Resource Manager toomanage hello rol tabanlı erişim denetimi ile kullanılabilecek tooresources nasıl erişim açıklar."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 9624715ac612f42df6f9e9e67b8233bd4b914174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-portal-toocreate-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a><span data-ttu-id="07da4-103">Bir Azure Active Directory Uygulama ve kaynaklarına erişebilir hizmet sorumlusu Portal toocreate kullanın</span><span class="sxs-lookup"><span data-stu-id="07da4-103">Use portal toocreate an Azure Active Directory application and service principal that can access resources</span></span>

<span data-ttu-id="07da4-104">Kaynakları göremeyen veya tooaccess gereken bir uygulamanız varsa, Azure Active Directory (AD) uygulama ayarlama ve gerekli hello izinleri tooit atamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="07da4-104">When you have an application that needs tooaccess or modify resources, you must set up an Azure Active Directory (AD) application and assign hello required permissions tooit.</span></span> <span data-ttu-id="07da4-105">Bu yaklaşım tercih toorunning hello uygulama kendi kimlik bilgileri altında nedeni:</span><span class="sxs-lookup"><span data-stu-id="07da4-105">This approach is preferable toorunning hello app under your own credentials because:</span></span>

* <span data-ttu-id="07da4-106">Kendi izinlerinizi farklı toohello uygulama kimliği izinleri atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07da4-106">You can assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="07da4-107">Genellikle, bu kısıtlı tooexactly hangi hello uygulamanın toodo ihtiyacı izinlerdir.</span><span class="sxs-lookup"><span data-stu-id="07da4-107">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="07da4-108">Sizin Sorumluluklarınız değiştirirseniz toochange hello uygulamanın kimlik bilgileri yok.</span><span class="sxs-lookup"><span data-stu-id="07da4-108">You do not have toochange hello app's credentials if your responsibilities change.</span></span> 
* <span data-ttu-id="07da4-109">Katılımsız betik yürütülürken, bir sertifika tooautomate kimlik doğrulaması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07da4-109">You can use a certificate tooautomate authentication when executing an unattended script.</span></span>

<span data-ttu-id="07da4-110">Bu konuda tooperform olanlar nasıl adımları aracılığıyla gösterilmektedir hello portal.</span><span class="sxs-lookup"><span data-stu-id="07da4-110">This topic shows you how tooperform those steps through hello portal.</span></span> <span data-ttu-id="07da4-111">Merhaba uygulaması yalnızca bir kuruluş içinde hedeflenen toorun olduğu bir tek kiracılı uygulama odaklanır.</span><span class="sxs-lookup"><span data-stu-id="07da4-111">It focuses on a single-tenant application where hello application is intended toorun within only one organization.</span></span> <span data-ttu-id="07da4-112">Genellikle tek Kiracı uygulamalar, kuruluşunuzun içinde çalışan satır iş kolu uygulamaları için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="07da4-112">You typically use single-tenant applications for line-of-business applications that run within your organization.</span></span>
 
## <a name="required-permissions"></a><span data-ttu-id="07da4-113">Gerekli izinler</span><span class="sxs-lookup"><span data-stu-id="07da4-113">Required permissions</span></span>
<span data-ttu-id="07da4-114">toocomplete Bu konu, yeterli izinleri tooregister bir uygulama ile Azure AD kiracınıza sahip ve Azure aboneliğinizde hello uygulama tooa rolünü atamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="07da4-114">toocomplete this topic, you must have sufficient permissions tooregister an application with your Azure AD tenant, and assign hello application tooa role in your Azure subscription.</span></span> <span data-ttu-id="07da4-115">Şimdi bu adımları hello doğru izinleri tooperform olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="07da4-115">Let's make sure you have hello right permissions tooperform those steps.</span></span>

### <a name="check-azure-active-directory-permissions"></a><span data-ttu-id="07da4-116">Azure Active Directory izinlerini denetleyin</span><span class="sxs-lookup"><span data-stu-id="07da4-116">Check Azure Active Directory permissions</span></span>
1. <span data-ttu-id="07da4-117">Tooyour Azure hesabı hello aracılığıyla oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="07da4-117">Log in tooyour Azure Account through hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="07da4-118">Seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07da4-118">Select **Azure Active Directory**.</span></span>

     ![Azure active Directory'yi seçin](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. <span data-ttu-id="07da4-120">Azure Active Directory'de seçin **kullanıcı ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="07da4-120">In Azure Active Directory, select **User settings**.</span></span>

     ![kullanıcı ayarlarını seçin](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. <span data-ttu-id="07da4-122">Merhaba denetleyin **uygulama kayıtlar** ayarı.</span><span class="sxs-lookup"><span data-stu-id="07da4-122">Check hello **App registrations** setting.</span></span> <span data-ttu-id="07da4-123">Varsa çok ayarlamak**Evet**, yönetici olmayan kullanıcıların AD uygulamaları kaydolabilir.</span><span class="sxs-lookup"><span data-stu-id="07da4-123">If set too**Yes**, non-admin users can register AD apps.</span></span> <span data-ttu-id="07da4-124">Bu ayar hello Azure AD kiracısı içinde herhangi bir kullanıcı bir uygulama kaydedebilirsiniz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="07da4-124">This setting means any user in hello Azure AD tenant can register an app.</span></span> <span data-ttu-id="07da4-125">Çok geçebilmeniz[denetleyin Azure abonelik izinleri](#check-azure-subscription-permissions).</span><span class="sxs-lookup"><span data-stu-id="07da4-125">You can proceed too[Check Azure subscription permissions](#check-azure-subscription-permissions).</span></span>

     ![Uygulama kayıtları görüntüle](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. <span data-ttu-id="07da4-127">Ayarı hello uygulama kayıtlar ayarlanır, çok**Hayır**, yalnızca yönetici kullanıcılar uygulamaların kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07da4-127">If hello app registrations setting is set too**No**, only admin users can register apps.</span></span> <span data-ttu-id="07da4-128">Hello Azure AD kiracısı için yönetici hesabınız olup olmadığını toocheck gerekir.</span><span class="sxs-lookup"><span data-stu-id="07da4-128">You need toocheck whether your account is an admin for hello Azure AD tenant.</span></span> <span data-ttu-id="07da4-129">Seçin **genel bakış** ve **kullanıcı Bul** hızlı görevleri.</span><span class="sxs-lookup"><span data-stu-id="07da4-129">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![Kullanıcı Bul](./media/resource-group-create-service-principal-portal/find-user.png)
6. <span data-ttu-id="07da4-131">Hesabınız için arama yapın ve bunu bulduğunuzda seçin.</span><span class="sxs-lookup"><span data-stu-id="07da4-131">Search for your account, and select it when you find it.</span></span>

     ![arama kullanıcı](./media/resource-group-create-service-principal-portal/show-user.png)
7. <span data-ttu-id="07da4-133">Hesabınız için seçin **dizin rolünü**.</span><span class="sxs-lookup"><span data-stu-id="07da4-133">For your account, select **Directory role**.</span></span> 

     ![dizin rolü](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. <span data-ttu-id="07da4-135">Atanmış dizini rolünüze Azure AD'de görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="07da4-135">View your assigned directory role in Azure AD.</span></span> <span data-ttu-id="07da4-136">Hesabınıza toohello kullanıcı rolüne atanan hello uygulama kayıt ayarından (adımları önceki hello) sınırlı tooadmin kullanıcılar varsa, yönetici tooeither atamak, tooan Yönetici rolü ya da tooenable kullanıcılar tooregister uygulamaları isteyin.</span><span class="sxs-lookup"><span data-stu-id="07da4-136">If your account is assigned toohello User role, but hello app registration setting (from hello preceding steps) is limited tooadmin users, ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

     ![Görünüm rolü](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a><span data-ttu-id="07da4-138">Azure abonelik izinlerinizi denetleyin</span><span class="sxs-lookup"><span data-stu-id="07da4-138">Check Azure subscription permissions</span></span>
<span data-ttu-id="07da4-139">Azure aboneliğinizde, hesabınızın olması gerekir `Microsoft.Authorization/*/Write` tooassign bir AD uygulama tooa rolü erişim.</span><span class="sxs-lookup"><span data-stu-id="07da4-139">In your Azure subscription, your account must have `Microsoft.Authorization/*/Write` access tooassign an AD app tooa role.</span></span> <span data-ttu-id="07da4-140">Bu eylemin hello verilir [sahibi](../active-directory/role-based-access-built-in-roles.md#owner) rol veya [kullanıcı erişimi Yöneticisi](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) rol.</span><span class="sxs-lookup"><span data-stu-id="07da4-140">This action is granted through hello [Owner](../active-directory/role-based-access-built-in-roles.md#owner) role or [User Access Administrator](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) role.</span></span> <span data-ttu-id="07da4-141">Hesabınızı toohello atanmışsa **katkıda bulunan** rolü, yeterli izniniz yok.</span><span class="sxs-lookup"><span data-stu-id="07da4-141">If your account is assigned toohello **Contributor** role, you do not have adequate permission.</span></span> <span data-ttu-id="07da4-142">Tooassign hello hizmet asıl tooa rolü çalışırken bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="07da4-142">You will receive an error when attempting tooassign hello service principal tooa role.</span></span> 

<span data-ttu-id="07da4-143">toocheck abonelik izinlerinizi:</span><span class="sxs-lookup"><span data-stu-id="07da4-143">toocheck your subscription permissions:</span></span>

1. <span data-ttu-id="07da4-144">Zaten Azure AD hesabınızla adımları önceki hello aradığınız değil, seçin **Azure Active Directory** hello sol bölmesinden.</span><span class="sxs-lookup"><span data-stu-id="07da4-144">If you are not already looking at your Azure AD account from hello preceding steps, select **Azure Active Directory** from hello left pane.</span></span>

2. <span data-ttu-id="07da4-145">Azure AD hesabınıza bulun.</span><span class="sxs-lookup"><span data-stu-id="07da4-145">Find your Azure AD account.</span></span> <span data-ttu-id="07da4-146">Seçin **genel bakış** ve **kullanıcı Bul** hızlı görevleri.</span><span class="sxs-lookup"><span data-stu-id="07da4-146">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![Kullanıcı Bul](./media/resource-group-create-service-principal-portal/find-user.png)
2. <span data-ttu-id="07da4-148">Hesabınız için arama yapın ve bunu bulduğunuzda seçin.</span><span class="sxs-lookup"><span data-stu-id="07da4-148">Search for your account, and select it when you find it.</span></span>

     ![arama kullanıcı](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. <span data-ttu-id="07da4-150">Seçin **Azure kaynaklarını**.</span><span class="sxs-lookup"><span data-stu-id="07da4-150">Select **Azure resources**.</span></span>

     ![kaynakları seçin](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. <span data-ttu-id="07da4-152">Atanan rollerinizi görüntüleyin ve bir AD uygulama tooa rolü yeterli izinlere tooassign olup olmadığını belirlemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="07da4-152">View your assigned roles, and determine if you have adequate permissions tooassign an AD app tooa role.</span></span> <span data-ttu-id="07da4-153">Aksi takdirde, abonelik yönetici tooadd isteyin, tooUser erişim Yönetici rolü.</span><span class="sxs-lookup"><span data-stu-id="07da4-153">If not, ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span> <span data-ttu-id="07da4-154">Görüntü aşağıdaki hello hello kullanıcı kullanıcının yeterli izinlere sahip anlamına gelir atanan toohello sahip iki abonelikler için rolüdür.</span><span class="sxs-lookup"><span data-stu-id="07da4-154">In hello following image, hello user is assigned toohello Owner role for two subscriptions, which means that user has adequate permissions.</span></span> 

     ![izinleri göster](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a><span data-ttu-id="07da4-156">Azure Active Directory Uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="07da4-156">Create an Azure Active Directory application</span></span>
1. <span data-ttu-id="07da4-157">Tooyour Azure hesabı hello aracılığıyla oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="07da4-157">Log in tooyour Azure Account through hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="07da4-158">Seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07da4-158">Select **Azure Active Directory**.</span></span>

     ![Azure active Directory'yi seçin](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. <span data-ttu-id="07da4-160">Seçin **uygulama kayıtlar**.</span><span class="sxs-lookup"><span data-stu-id="07da4-160">Select **App registrations**.</span></span>   

     ![Uygulama kayıtlar seçin](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. <span data-ttu-id="07da4-162">**Add (Ekle)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="07da4-162">Select **Add**.</span></span>

     ![Uygulama Ekle](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. <span data-ttu-id="07da4-164">Merhaba uygulaması için bir ad ve URL sağlayın.</span><span class="sxs-lookup"><span data-stu-id="07da4-164">Provide a name and URL for hello application.</span></span> <span data-ttu-id="07da4-165">Şunlardan birini seçin **Web uygulaması / API** veya **yerel** hello uygulama türünün toocreate istiyor.</span><span class="sxs-lookup"><span data-stu-id="07da4-165">Select either **Web app / API** or **Native** for hello type of application you want toocreate.</span></span> <span data-ttu-id="07da4-166">Merhaba değerleri ayarladıktan sonra Seç **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="07da4-166">After setting hello values, select **Create**.</span></span>

     ![Uygulama adı](./media/resource-group-create-service-principal-portal/create-app.png)

<span data-ttu-id="07da4-168">Uygulamanızı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="07da4-168">You have created your application.</span></span>

## <a name="get-application-id-and-authentication-key"></a><span data-ttu-id="07da4-169">Uygulama kimliği ile kimlik doğrulama anahtarı alma</span><span class="sxs-lookup"><span data-stu-id="07da4-169">Get application ID and authentication key</span></span>
<span data-ttu-id="07da4-170">Program aracılığıyla oturum açarken uygulamanız ve bir kimlik doğrulama anahtarı için hello kimliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="07da4-170">When programmatically logging in, you need hello ID for your application and an authentication key.</span></span> <span data-ttu-id="07da4-171">Bu değerleri, aşağıdaki adımları kullanın hello tooget:</span><span class="sxs-lookup"><span data-stu-id="07da4-171">tooget those values, use hello following steps:</span></span>

1. <span data-ttu-id="07da4-172">Gelen **uygulama kayıtlar** uygulamanızı Azure Active Directory'de seçin.</span><span class="sxs-lookup"><span data-stu-id="07da4-172">From **App registrations** in Azure Active Directory, select your application.</span></span>

     ![Uygulama seçin](./media/resource-group-create-service-principal-portal/select-app.png)
2. <span data-ttu-id="07da4-174">Kopya hello **uygulama kimliği** ve uygulama kodunuzda saklayın.</span><span class="sxs-lookup"><span data-stu-id="07da4-174">Copy hello **Application ID** and store it in your application code.</span></span> <span data-ttu-id="07da4-175">Merhaba hello uygulamalarda [örnek uygulamaları](#sample-applications) toothis değeri hello istemci kimliği olarak bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="07da4-175">hello applications in hello [sample applications](#sample-applications) section refer toothis value as hello client id.</span></span>

     ![istemci kimliği](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. <span data-ttu-id="07da4-177">toogenerate bir kimlik doğrulama anahtarı seçin **anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="07da4-177">toogenerate an authentication key, select **Keys**.</span></span>

     ![anahtarları seçin](./media/resource-group-create-service-principal-portal/select-keys.png)
4. <span data-ttu-id="07da4-179">Merhaba anahtarı ve bir süre hello anahtarı için bir açıklama sağlayın.</span><span class="sxs-lookup"><span data-stu-id="07da4-179">Provide a description of hello key, and a duration for hello key.</span></span> <span data-ttu-id="07da4-180">İşiniz bittiğinde, seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="07da4-180">When done, select **Save**.</span></span>

     ![anahtarı Kaydet](./media/resource-group-create-service-principal-portal/save-key.png)

     <span data-ttu-id="07da4-182">Başlangıç anahtarı kaydedildikten sonra hello anahtarın hello değeri görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="07da4-182">After saving hello key, hello value of hello key is displayed.</span></span> <span data-ttu-id="07da4-183">Bu değer, değil mümkün tooretrieve hello anahtarı daha sonra olduğundan kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="07da4-183">Copy this value because you are not able tooretrieve hello key later.</span></span> <span data-ttu-id="07da4-184">Merhaba anahtar değeri Merhaba uygulaması hello uygulama kimliği toolog sağlar.</span><span class="sxs-lookup"><span data-stu-id="07da4-184">You provide hello key value with hello application ID toolog in as hello application.</span></span> <span data-ttu-id="07da4-185">Burada, uygulamanızın alabildiği hello anahtar değer deposu.</span><span class="sxs-lookup"><span data-stu-id="07da4-185">Store hello key value where your application can retrieve it.</span></span>

     ![anahtar kaydedildi](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a><span data-ttu-id="07da4-187">Kiracı Kimliğinizi alma</span><span class="sxs-lookup"><span data-stu-id="07da4-187">Get tenant ID</span></span>
<span data-ttu-id="07da4-188">Program aracılığıyla oturum açarken, kimlik doğrulama isteği ile toopass hello Kiracı kimliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="07da4-188">When programmatically logging in, you need toopass hello tenant ID with your authentication request.</span></span> 

1. <span data-ttu-id="07da4-189">tooget hello Kiracı kimliği, select **özellikleri** Azure AD kiracınız için.</span><span class="sxs-lookup"><span data-stu-id="07da4-189">tooget hello tenant ID, select **Properties** for your Azure AD tenant.</span></span> 

     ![Azure AD Özellikler'i seçin](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. <span data-ttu-id="07da4-191">Kopya hello **dizin kimliği**.</span><span class="sxs-lookup"><span data-stu-id="07da4-191">Copy hello **Directory ID**.</span></span> <span data-ttu-id="07da4-192">Bu değer, Kiracı kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="07da4-192">This value is your tenant ID.</span></span>

     ![Kiracı kimliği](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-toorole"></a><span data-ttu-id="07da4-194">Uygulama toorole atayın</span><span class="sxs-lookup"><span data-stu-id="07da4-194">Assign application toorole</span></span>
<span data-ttu-id="07da4-195">tooaccess kaynakları aboneliğinizde hello uygulama tooa rolünü atamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="07da4-195">tooaccess resources in your subscription, you must assign hello application tooa role.</span></span> <span data-ttu-id="07da4-196">Merhaba uygulaması hello doğru izinleri rolünü karar verin.</span><span class="sxs-lookup"><span data-stu-id="07da4-196">Decide which role represents hello right permissions for hello application.</span></span> <span data-ttu-id="07da4-197">toolearn hello kullanılabilir rolleri hakkında bkz [RBAC: yerleşik roller](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="07da4-197">toolearn about hello available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="07da4-198">Merhaba kapsam hello abonelik, kaynak grubu ya da kaynak hello düzeyinde ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07da4-198">You can set hello scope at hello level of hello subscription, resource group, or resource.</span></span> <span data-ttu-id="07da4-199">Kapsam düzeyleri devralınan toolower izinlerdir.</span><span class="sxs-lookup"><span data-stu-id="07da4-199">Permissions are inherited toolower levels of scope.</span></span> <span data-ttu-id="07da4-200">Örneğin, bir kaynak grubu için bir uygulama toohello okuyucu rolüne geldiğini ekleme hello kaynak grubu ve içerdiği tüm kaynaklar okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="07da4-200">For example, adding an application toohello Reader role for a resource group means it can read hello resource group and any resources it contains.</span></span>

1. <span data-ttu-id="07da4-201">Toohello tooassign hello uygulamaya istediğiniz kapsam düzeyine gidin.</span><span class="sxs-lookup"><span data-stu-id="07da4-201">Navigate toohello level of scope you wish tooassign hello application to.</span></span> <span data-ttu-id="07da4-202">Örneğin, tooassign hello abonelik kapsamında bir rol seçin **abonelikleri**.</span><span class="sxs-lookup"><span data-stu-id="07da4-202">For example, tooassign a role at hello subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="07da4-203">Bunun yerine, bir kaynak grubu veya kaynak seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07da4-203">You could instead select a resource group or resource.</span></span>

     ![Abonelik seç](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. <span data-ttu-id="07da4-205">Merhaba belirli abonelik (kaynak grubu veya kaynak) tooassign hello uygulamaya seçin.</span><span class="sxs-lookup"><span data-stu-id="07da4-205">Select hello particular subscription (resource group or resource) tooassign hello application to.</span></span>

     ![atama için abonelik seçin](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. <span data-ttu-id="07da4-207">Seçin **erişim denetimi (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="07da4-207">Select **Access Control (IAM)**.</span></span>

     ![erişim seçin](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. <span data-ttu-id="07da4-209">**Add (Ekle)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="07da4-209">Select **Add**.</span></span>

     ![Select ekleme](./media/resource-group-create-service-principal-portal/select-add.png)
6. <span data-ttu-id="07da4-211">Tooassign toohello uygulama istediğiniz hello rolü seçin.</span><span class="sxs-lookup"><span data-stu-id="07da4-211">Select hello role you wish tooassign toohello application.</span></span> <span data-ttu-id="07da4-212">Merhaba aşağıdaki resimde gösterilmiştir hello **okuyucu** rol.</span><span class="sxs-lookup"><span data-stu-id="07da4-212">hello following image shows hello **Reader** role.</span></span>

     ![Rol Seç](./media/resource-group-create-service-principal-portal/select-role.png)

8. <span data-ttu-id="07da4-214">Uygulamanız için arayın ve seçin.</span><span class="sxs-lookup"><span data-stu-id="07da4-214">Search for your application, and select it.</span></span>

     ![uygulamayı arayın](./media/resource-group-create-service-principal-portal/search-app.png)
9. <span data-ttu-id="07da4-216">Seçin **Tamam** toofinish hello rol atama.</span><span class="sxs-lookup"><span data-stu-id="07da4-216">Select **OK** toofinish assigning hello role.</span></span> <span data-ttu-id="07da4-217">Merhaba listesinde uygulamanızın tooa rolü bu kapsamı için atanan kullanıcılar veya bakın.</span><span class="sxs-lookup"><span data-stu-id="07da4-217">You see your application in hello list of users assigned tooa role for that scope.</span></span>

## <a name="log-in-as-hello-application"></a><span data-ttu-id="07da4-218">Merhaba uygulaması oturum açın</span><span class="sxs-lookup"><span data-stu-id="07da4-218">Log in as hello application</span></span>

<span data-ttu-id="07da4-219">Uygulamanız artık Azure Active Directory'de ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="07da4-219">Your application is now set up in Azure Active Directory.</span></span> <span data-ttu-id="07da4-220">Bir kimliği ve Merhaba uygulaması oturum açmak için anahtar toouse var.</span><span class="sxs-lookup"><span data-stu-id="07da4-220">You have an ID and key toouse for signing in as hello application.</span></span> <span data-ttu-id="07da4-221">Merhaba uygulaması, belirli eylemleri verir tooa rolü atanır.</span><span class="sxs-lookup"><span data-stu-id="07da4-221">hello application is assigned tooa role that gives it certain actions it can perform.</span></span> <span data-ttu-id="07da4-222">Farklı platformlarda üzerinden hello uygulama olarak oturum açma hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="07da4-222">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="07da4-223">PowerShell</span><span class="sxs-lookup"><span data-stu-id="07da4-223">PowerShell</span></span>](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [<span data-ttu-id="07da4-224">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="07da4-224">Azure CLI</span></span>](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [<span data-ttu-id="07da4-225">REST</span><span class="sxs-lookup"><span data-stu-id="07da4-225">REST</span></span>](/rest/api/#create-the-request)
* [<span data-ttu-id="07da4-226">.NET</span><span class="sxs-lookup"><span data-stu-id="07da4-226">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="07da4-227">Java</span><span class="sxs-lookup"><span data-stu-id="07da4-227">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="07da4-228">Node.js</span><span class="sxs-lookup"><span data-stu-id="07da4-228">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="07da4-229">Python</span><span class="sxs-lookup"><span data-stu-id="07da4-229">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="07da4-230">Ruby</span><span class="sxs-lookup"><span data-stu-id="07da4-230">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a><span data-ttu-id="07da4-231">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="07da4-231">Next steps</span></span>
* <span data-ttu-id="07da4-232">çok kiracılı uygulamasının tooset bkz [Geliştirici Kılavuzu tooauthorization hello Azure Kaynak Yöneticisi API'si ile](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="07da4-232">tooset up a multi-tenant application, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="07da4-233">güvenlik ilkeleri belirtme hakkında toolearn bkz [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="07da4-233">toolearn about specifying security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>  
* <span data-ttu-id="07da4-234">Verilen veya toousers reddedilen kullanılabilir eylemler listesi için bkz: [Azure Resource Manager kaynak sağlayıcısı işlemleri](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="07da4-234">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
