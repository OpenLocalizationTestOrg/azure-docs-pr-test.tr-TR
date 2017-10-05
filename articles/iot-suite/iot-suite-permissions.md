---
title: Azure IOT paketi ve Azure Active Directory | Microsoft Docs
description: "Azure IoT Paketinin izinleri yönetmek için Azure Active Directory’i nasıl kullandığını açıklar."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 246228ba-954a-4d96-b6d6-e53e4590cb4f
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: dobett
ms.openlocfilehash: 518e6a481ab6385b03dd3ddc2e155fb724e677fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="permissions-on-the-azureiotsuitecom-site"></a><span data-ttu-id="d7cf0-103">azureiotsuite.com sitesindeki izinler</span><span class="sxs-lookup"><span data-stu-id="d7cf0-103">Permissions on the azureiotsuite.com site</span></span>

## <a name="what-happens-when-you-sign-in"></a><span data-ttu-id="d7cf0-104">Oturum açtığınızda ne olur</span><span class="sxs-lookup"><span data-stu-id="d7cf0-104">What happens when you sign in</span></span>

<span data-ttu-id="d7cf0-105">İlk kez oturum açtığınızda, [azureiotsuite.com][lnk-azureiotsuite], sahip şu anda seçili olan Azure Active Directory (AAD) kiracısına ve Azure aboneliğine göre izin düzeyleri site belirler.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-105">The first time you sign in at [azureiotsuite.com][lnk-azureiotsuite], the site determines the permission levels you have based on the currently selected Azure Active Directory (AAD) tenant and Azure subscription.</span></span>

1. <span data-ttu-id="d7cf0-106">İlk olarak, kullanıcı adınızın yanında görülen kiracılar listesini doldurmak için site Azure'dan hangi AAD kiracılarına ait olduğunuz öğrenir.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-106">First, to populate the list of tenants seen next to your username, the site finds out from Azure which AAD tenants you belong to.</span></span> <span data-ttu-id="d7cf0-107">Şu anda, site aynı anda yalnızca bir kiracı için kullanıcı belirteçleri alabilir.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-107">Currently, the site can only obtain user tokens for one tenant at a time.</span></span> <span data-ttu-id="d7cf0-108">Sağ üst köşedeki açılır menüyü kullanarak kiracılar geçiş yaptığınızda, bu nedenle, site size ilgili kiracının belirteçlerini almak için bu kiracıda kaydeder.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-108">Therefore, when you switch tenants using the dropdown in the top right corner, the site logs you in to that tenant to obtain the tokens for that tenant.</span></span>

2. <span data-ttu-id="d7cf0-109">Site daha sonra, seçilen kiracı ile hangi aboneliğin ilişkilendirildiğini Azure’dan öğrenir.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-109">Next, the site finds out from Azure which subscriptions you have associated with the selected tenant.</span></span> <span data-ttu-id="d7cf0-110">Önceden yapılandırılmış yeni bir çözüm oluşturduğunuzda kullanılabilir abonelikleri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-110">You see the available subscriptions when you create a new preconfigured solution.</span></span>

3. <span data-ttu-id="d7cf0-111">Site son olarak önceden yapılandırılmış çözümler olarak etiketlenmiş abonelikler ve kaynak gruplarındaki tüm kaynakları alır ve giriş sayfasındaki kutucukları doldurur.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-111">Finally, the site retrieves all the resources in the subscriptions and resource groups tagged as preconfigured solutions and populates the tiles on the home page.</span></span>

<span data-ttu-id="d7cf0-112">Aşağıdaki bölümlerde önceden yapılandırılmış çözümlere erişimi denetleyen roller açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-112">The following sections describe the roles that control access to the preconfigured solutions.</span></span>

## <a name="aad-roles"></a><span data-ttu-id="d7cf0-113">AAD rolleri</span><span class="sxs-lookup"><span data-stu-id="d7cf0-113">AAD roles</span></span>

<span data-ttu-id="d7cf0-114">AAD rolleri önceden yapılandırılmış çözümleri sağlama özelliğini denetler ve önceden yapılandırılmış bir çözümdeki kullanıcıları yönetir.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-114">The AAD roles control the ability provision preconfigured solutions and manage users in a preconfigured solution.</span></span>

<span data-ttu-id="d7cf0-115">AAD'de yönetici rolleri hakkında daha fazla bilgi bulabilirsiniz [Azure AD'de yönetici rolleri atama][lnk-aad-admin].</span><span class="sxs-lookup"><span data-stu-id="d7cf0-115">You can find more information about administrator roles in AAD in [Assigning administrator roles in Azure AD][lnk-aad-admin].</span></span> <span data-ttu-id="d7cf0-116">Geçerli makaleyi odaklanır **genel yönetici** ve **kullanıcı** olarak önceden yapılandırılmış çözümler tarafından kullanılan directory rolleri.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-116">The current article focuses on the **Global Administrator** and the **User** directory roles as used by the preconfigured solutions.</span></span>

### <a name="global-administrator"></a><span data-ttu-id="d7cf0-117">Genel yönetici</span><span class="sxs-lookup"><span data-stu-id="d7cf0-117">Global administrator</span></span>

<span data-ttu-id="d7cf0-118">AAD kiracısı başına çok sayıda genel yönetici olabilir:</span><span class="sxs-lookup"><span data-stu-id="d7cf0-118">There can be many global administrators per AAD tenant:</span></span>

* <span data-ttu-id="d7cf0-119">Bir AAD kiracısı oluşturduğunuzda varsayılan olarak bu kiracının genel yöneticisi olursunuz.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-119">When you create an AAD tenant, you are by default the global administrator of that tenant.</span></span>
* <span data-ttu-id="d7cf0-120">Genel yönetici önceden yapılandırılmış bir çözüm sağlayabilir ve atanmış bir **yönetici** AAD kiracısının içindeki uygulama için rol.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-120">The global administrator can provision a preconfigured solution and is assigned an **Admin** role for the application inside their AAD tenant.</span></span>
* <span data-ttu-id="d7cf0-121">Aynı AAD kiracısındaki başka bir kullanıcı bir uygulama oluşturduğunda genel yöneticinin varsayılan rolü olan **salt okunur**.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-121">If another user in the same AAD tenant creates an application, the default role granted to the global administrator is **ReadOnly**.</span></span>
* <span data-ttu-id="d7cf0-122">Genel yönetici kullanıcıları kullanarak uygulamalar için roller atayabilirsiniz [Azure portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="d7cf0-122">A global administrator can assign users to roles for applications using the [Azure portal][lnk-portal].</span></span>

### <a name="domain-user"></a><span data-ttu-id="d7cf0-123">Etki alanı kullanıcısı</span><span class="sxs-lookup"><span data-stu-id="d7cf0-123">Domain user</span></span>

<span data-ttu-id="d7cf0-124">AAD kiracısı başına çok sayıda etki alanı kullanıcı olabilir:</span><span class="sxs-lookup"><span data-stu-id="d7cf0-124">There can be many domain users per AAD tenant:</span></span>

* <span data-ttu-id="d7cf0-125">Bir etki alanı kullanıcısı üzerinden önceden yapılandırılmış bir çözüm sağlayabilir [azureiotsuite.com] [ lnk-azureiotsuite] site.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-125">A domain user can provision a preconfigured solution through the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="d7cf0-126">Varsayılan olarak, etki alanı kullanıcı izni **yönetici** sağlanan uygulama rolü.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-126">By default, the domain user is granted the **Admin** role in the provisioned application.</span></span>
* <span data-ttu-id="d7cf0-127">Bir etki alanı kullanıcısı build.cmd komut dosyasını kullanarak bir uygulama oluşturabilirsiniz [azure-iot-remote-monitoring][lnk-rm-github-repo], [azure-iot-predictive-maintenance] [ lnk-pm-github-repo], veya [azure-IOT-bağlı-Fabrika] [ lnk-cf-github-repo] deposu.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-127">A domain user can create an application using the build.cmd script in the [azure-iot-remote-monitoring][lnk-rm-github-repo],  [azure-iot-predictive-maintenance][lnk-pm-github-repo], or [azure-iot-connected-factory][lnk-cf-github-repo] repository.</span></span> <span data-ttu-id="d7cf0-128">Ancak, etki alanı kullanıcıya verilen varsayılan rol olan **ReadOnly**, bir etki alanı kullanıcı rolleri atamak için izni yok.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-128">However, the default role granted to the domain user is **ReadOnly**, because a domain user does not have permission to assign roles.</span></span>
* <span data-ttu-id="d7cf0-129">AAD kiracısında başka bir kullanıcı bir uygulama oluşturduğunda, etki alanı kullanıcısı atanır **ReadOnly** rolü bu uygulama için varsayılan.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-129">If another user in the AAD tenant creates an application, the domain user is assigned the **ReadOnly** role by default for that application.</span></span>
* <span data-ttu-id="d7cf0-130">Bir etki alanı kullanıcısı uygulamalar için roller atayamazsınız; Bu nedenle bunlar olsa bile bir etki alanı kullanıcısı kullanıcıları veya bir uygulama için kullanıcıların rollerini ekleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-130">A domain user cannot assign roles for applications; therefore a domain user cannot add users or roles for users for an application even if they provisioned it.</span></span>

### <a name="guest-user"></a><span data-ttu-id="d7cf0-131">Konuk kullanıcı</span><span class="sxs-lookup"><span data-stu-id="d7cf0-131">Guest User</span></span>

<span data-ttu-id="d7cf0-132">AAD kiracısı başına çok sayıda Konuk kullanıcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-132">There can be many guest users per AAD tenant.</span></span> <span data-ttu-id="d7cf0-133">Konuk kullanıcılar AAD kiracısında sınırlı bir haklar kümesine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-133">Guest users have a limited set of rights in the AAD tenant.</span></span> <span data-ttu-id="d7cf0-134">Sonuç olarak, konuk kullanıcılar AAD kiracısında önceden yapılandırılmış bir çözüm sağlayamaz.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-134">As a result, guest users cannot provision a preconfigured solution in the AAD tenant.</span></span>

<span data-ttu-id="d7cf0-135">Kullanıcılar ve roller aad'de hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="d7cf0-135">For more information about users and roles in AAD, see the following resources:</span></span>

* <span data-ttu-id="d7cf0-136">[Azure AD'de kullanıcı oluşturma][lnk-create-edit-users]</span><span class="sxs-lookup"><span data-stu-id="d7cf0-136">[Create users in Azure AD][lnk-create-edit-users]</span></span>
* <span data-ttu-id="d7cf0-137">[Kullanıcılar uygulamalara atama][lnk-assign-app-roles]</span><span class="sxs-lookup"><span data-stu-id="d7cf0-137">[Assign users to apps][lnk-assign-app-roles]</span></span>

## <a name="azure-subscription-administrator-roles"></a><span data-ttu-id="d7cf0-138">Azure abonelik yöneticisi rolleri</span><span class="sxs-lookup"><span data-stu-id="d7cf0-138">Azure subscription administrator roles</span></span>

<span data-ttu-id="d7cf0-139">Azure yöneticisi rolleri bir Azure aboneliğini bir AD kiracısıyla eşleme özelliğini denetler.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-139">The Azure admin roles control the ability to map an Azure subscription to an AD tenant.</span></span>

<span data-ttu-id="d7cf0-140">Makaleyi Azure yönetici rolleri hakkında daha fazla bilgi edinin [Azure ortak yönetici, Hizmet Yöneticisi ve Hesap Yöneticisi ekleme veya değiştirme konusunda][lnk-admin-roles].</span><span class="sxs-lookup"><span data-stu-id="d7cf0-140">Find out more about the Azure admin roles in the article [How to add or change Azure Co-Administrator, Service Administrator, and Account Administrator][lnk-admin-roles].</span></span>

## <a name="application-roles"></a><span data-ttu-id="d7cf0-141">Uygulama rolleri</span><span class="sxs-lookup"><span data-stu-id="d7cf0-141">Application roles</span></span>

<span data-ttu-id="d7cf0-142">Uygulama rolleri önceden yapılandırılmış çözümünüzdeki cihazlara erişimi denetler.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-142">The application roles control access to devices in your preconfigured solution.</span></span>

<span data-ttu-id="d7cf0-143">İki tanımlanmış rol ve sağlanan bir uygulamada bir örtük rol mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="d7cf0-143">There are two defined roles and one implicit role defined in a provisioned application:</span></span>

* <span data-ttu-id="d7cf0-144">**Yönetici:** ekleme, yönetme, cihazları kaldırın ve ayarlarını değiştirmek için tam denetime sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-144">**Admin:** Has full control to add, manage, remove devices, and modify settings.</span></span>
* <span data-ttu-id="d7cf0-145">**Salt okunur:** aygıtlar, kurallar, Eylemler, işleri ve telemetri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-145">**ReadOnly:** Can view devices, rules, actions, jobs, and telemetry.</span></span>

<span data-ttu-id="d7cf0-146">Her rol için atanan izinler bulabilirsiniz [RolePermissions.cs] [ lnk-resource-cs] kaynak dosyası.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-146">You can find the permissions assigned to each role in the [RolePermissions.cs][lnk-resource-cs] source file.</span></span>

### <a name="changing-application-roles-for-a-user"></a><span data-ttu-id="d7cf0-147">Bir kullanıcının uygulama rollerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="d7cf0-147">Changing application roles for a user</span></span>

<span data-ttu-id="d7cf0-148">Active Directory’de bir kullanıcıyı önceden yapılandırılmış çözümünüzün yöneticisi yapmak için aşağıdaki yordamı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-148">You can use the following procedure to make a user in your Active Directory an administrator of your preconfigured solution.</span></span>

<span data-ttu-id="d7cf0-149">Bir kullanıcının rollerini değiştirmek için AAD genel yöneticisi olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d7cf0-149">You must be an AAD global administrator to change roles for a user:</span></span>

1. <span data-ttu-id="d7cf0-150">[Azure Portalı][lnk-portal]’na gidin.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-150">Go to the [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="d7cf0-151">Seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-151">Select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="d7cf0-152">Çözümünüzü sağlarken azureiotsuite.com üzerinde seçtiğiniz dizin kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-152">Make sure you are using the directory you chose on azureiotsuite.com when you provisioned your solution.</span></span> <span data-ttu-id="d7cf0-153">Aboneliğinizle ilişkili birden fazla dizine sahipseniz, bunları hesap adınızı portalın sağ üst tıklatırsanız arasında geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-153">If you have multiple directories associated with your subscription, you can switch between them if you click your account name at the top-right of the portal.</span></span>
4. <span data-ttu-id="d7cf0-154">Tıklatın **kurumsal uygulamalar**, ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-154">Click **Enterprise applications**, then **All applications**.</span></span>
4. <span data-ttu-id="d7cf0-155">Göster **tüm uygulamaları** ile **herhangi** durumu.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-155">Show **All applications** with **Any** status.</span></span> <span data-ttu-id="d7cf0-156">Ardından, önceden yapılandırılmış çözümünüz ada sahip bir uygulama arayın.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-156">Then search for an application with name of your preconfigured solution.</span></span>
5. <span data-ttu-id="d7cf0-157">Önceden yapılandırılmış çözümünüzün adıyla eşleşen uygulamanın adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-157">Click the name of the application that matches your preconfigured solution name.</span></span>
6. <span data-ttu-id="d7cf0-158">tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-158">Click **Users and groups**.</span></span>
7. <span data-ttu-id="d7cf0-159">Rollerini değiştirmek istediğiniz kullanıcıyı seçin.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-159">Select the user you want to switch roles.</span></span>
8. <span data-ttu-id="d7cf0-160">**Ata**’ya tıklayın ve kullanıcıya atamak istediğiniz rolü (**Yönetici** gibi) seçip onay işaretine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-160">Click **Assign** and select the role (such as **Admin**) you'd like to assign to the user, click the check mark.</span></span>

## <a name="faq"></a><span data-ttu-id="d7cf0-161">SSS</span><span class="sxs-lookup"><span data-stu-id="d7cf0-161">FAQ</span></span>

### <a name="im-a-service-administrator-and-id-like-to-change-the-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a><span data-ttu-id="d7cf0-162">Hizmet yöneticisiyim ve aboneliğim ile belirli bir AAD kiracısı arasında dizin eşlemesini değiştirmek istiyorum.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-162">I'm a service administrator and I'd like to change the directory mapping between my subscription and a specific AAD tenant.</span></span> <span data-ttu-id="d7cf0-163">Bu görevi nasıl tamamlamak?</span><span class="sxs-lookup"><span data-stu-id="d7cf0-163">How do I complete this task?</span></span>

1. <span data-ttu-id="d7cf0-164">Git [Klasik Azure portalı][lnk-classic-portal], tıklatın **ayarları** sol taraftaki Hizmet listesinde.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-164">Go to the [Azure classic portal][lnk-classic-portal], click **Settings** in the list of services on the left-hand side.</span></span>
2. <span data-ttu-id="d7cf0-165">Dizin eşlemesini değiştirmek istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-165">Select the subscription you'd like to change the directory mapping to.</span></span>
3. <span data-ttu-id="d7cf0-166">**Dizini Düzenle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-166">Click **Edit Directory**.</span></span>
4. <span data-ttu-id="d7cf0-167">Açılır listede kullanmak istediğiniz **Dizin**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-167">Select the **Directory** you would like to use in the dropdown.</span></span> <span data-ttu-id="d7cf0-168">İleri okuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-168">Click the forward arrow.</span></span>
5. <span data-ttu-id="d7cf0-169">Dizin eşlemesini ve etkilenen ortak yöneticileri onaylayın.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-169">Confirm the directory mapping and affected co-administrators.</span></span> <span data-ttu-id="d7cf0-170">Başka bir dizinden taşıyorsanız, özgün dizindeki tüm ortak Yöneticiler kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-170">If you are moving from another directory, all the co-administrators from the original directory are removed.</span></span>

### <a name="im-a-domain-usermember-on-the-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a><span data-ttu-id="d7cf0-171">AAD kiracısı üzerinde etki alanı kullanıcısı/üyesiyim ve önceden yapılandırılmış bir çözüm oluşturdum.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-171">I'm a domain user/member on the AAD tenant and I've created a preconfigured solution.</span></span> <span data-ttu-id="d7cf0-172">Uygulamam için bana nasıl rol atanır?</span><span class="sxs-lookup"><span data-stu-id="d7cf0-172">How do I get assigned a role for my application?</span></span>

<span data-ttu-id="d7cf0-173">AAD kiracısında genel yönetici yapın ve ardından roller kullanıcılara kendinize atamak için genel yönetici isteyin.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-173">Ask a global administrator to make you a global administrator on the AAD tenant and then assign roles to users yourself.</span></span> <span data-ttu-id="d7cf0-174">Alternatif olarak, doğrudan bir rol atamasını isteyin.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-174">Alternatively, ask a global administrator to assign you a role directly.</span></span> <span data-ttu-id="d7cf0-175">Önceden yapılandırılmış çözümünüzün dağıtıldığı AAD kiracısını değiştirmek isterseniz sonraki soruya bakın.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-175">If you'd like to change the AAD tenant your preconfigured solution has been deployed to, see the next question.</span></span>

### <a name="how-do-i-switch-the-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a><span data-ttu-id="d7cf0-176">Uzaktan izlediğim önceden yapılandırılmış çözümümün ve uygulamamın atandığı AAD kiracısına nasıl geçiş yapabilirim?</span><span class="sxs-lookup"><span data-stu-id="d7cf0-176">How do I switch the AAD tenant my remote monitoring preconfigured solution and application are assigned to?</span></span>

<span data-ttu-id="d7cf0-177"><https://github.com/Azure/azure-iot-remote-monitoring> adresinden bir bulut dağıtımını yeniden çalıştırabilir ve yeni oluşturulan bir AAD kiracısı ile yeniden dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-177">You can run a cloud deployment from <https://github.com/Azure/azure-iot-remote-monitoring> and redeploy with a newly created AAD tenant.</span></span> <span data-ttu-id="d7cf0-178">Varsayılan olarak, bir AAD kiracısı oluşturduğunuzda, bir genel yönetici olduğu için kullanıcı ekleyin ve bu kullanıcılara roller atama için izinlere sahip.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-178">Because you are, by default, a global administrator when you create an AAD tenant, you have permissions to add users and assign roles to those users.</span></span>

1. <span data-ttu-id="d7cf0-179">Bir AAD dizini oluşturun [Azure portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="d7cf0-179">Create an AAD directory in the [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="d7cf0-180"><https://github.com/Azure/azure-iot-remote-monitoring> sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-180">Go to <https://github.com/Azure/azure-iot-remote-monitoring>.</span></span>
3. <span data-ttu-id="d7cf0-181">`build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` komutunu çalıştırın (Örneğin, `build.cmd cloud debug myRMSolution`)</span><span class="sxs-lookup"><span data-stu-id="d7cf0-181">Run `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (For example, `build.cmd cloud debug myRMSolution`)</span></span>
4. <span data-ttu-id="d7cf0-182">Sorulduğunda **tenantid** değerini önceki kiracınız yerine yeni oluşturduğunuz kiracı olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-182">When prompted, set the **tenantid** to be your newly created tenant instead of your previous tenant.</span></span>

### <a name="i-want-to-change-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a><span data-ttu-id="d7cf0-183">Şirket hesabıyla oturum açtığımda bir Hizmet Yöneticisini veya Ortak Yöneticiyi değiştirmek istiyorum</span><span class="sxs-lookup"><span data-stu-id="d7cf0-183">I want to change a Service Administrator or Co-Administrator when logged in with an organisational account</span></span>

<span data-ttu-id="d7cf0-184">Destek makalesine bakın [değiştirme Hizmet Yöneticisi ve bir hesabıyla oturum açtığımda ortak yöneticiyi][lnk-service-admins].</span><span class="sxs-lookup"><span data-stu-id="d7cf0-184">See the support article [Changing Service Administrator and Co-Administrator when logged in with an organisational account][lnk-service-admins].</span></span>

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-the-proper-permissions-to-create-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a><span data-ttu-id="d7cf0-185">Bu hatayı neden görüyorum?</span><span class="sxs-lookup"><span data-stu-id="d7cf0-185">Why am I seeing this error?</span></span> <span data-ttu-id="d7cf0-186">"Hesabınız bir çözüm oluşturmak için uygun izinlere sahip değil.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-186">"Your account does not have the proper permissions to create a solution.</span></span> <span data-ttu-id="d7cf0-187">Lütfen hesap yöneticinize başvurun veya farklı bir hesap ile deneyin."</span><span class="sxs-lookup"><span data-stu-id="d7cf0-187">Please check with your account administrator or try with a different account."</span></span>

<span data-ttu-id="d7cf0-188">Yönergeler için aşağıdaki çizime bakın:</span><span class="sxs-lookup"><span data-stu-id="d7cf0-188">Look at the following diagram for guidance:</span></span>

![][img-flowchart]

> [!NOTE]
> <span data-ttu-id="d7cf0-189">Görmeye devam ederseniz, doğrulama sonra hata: AAD kiracısında genel yönetici ve abonelikte ortak yönetici, hesap yöneticinizden kullanıcıyı kaldırmasını ve gerekli izinleri şu sırayla yeniden atamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-189">If you continue to see the error after validating you are a global administrator on the AAD tenant and a co-administrator on the subscription, have your account administrator remove the user and reassign necessary permissions in this order.</span></span> <span data-ttu-id="d7cf0-190">İlk olarak, kullanıcı genel yönetici olarak ekleyin ve ardından Azure aboneliğinde ortak yönetici olarak kullanıcı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-190">First, add the user as a global administrator and then add user as a co-administrator on the Azure subscription.</span></span> <span data-ttu-id="d7cf0-191">Sorun devam ederse başvurun [Yardım ve Destek][lnk-help-support].</span><span class="sxs-lookup"><span data-stu-id="d7cf0-191">If issues persist, contact [Help & Support][lnk-help-support].</span></span>

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-to-create-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a><span data-ttu-id="d7cf0-192">Bir Azure aboneliğim varken bu hatayı neden görüyorum?</span><span class="sxs-lookup"><span data-stu-id="d7cf0-192">Why am I seeing this error when I have an Azure subscription?</span></span> <span data-ttu-id="d7cf0-193">"Azure aboneliği önceden yapılandırılmış çözümler oluşturmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-193">"An Azure subscription is required to create pre-configured solutions.</span></span> <span data-ttu-id="d7cf0-194">Ücretsiz bir deneme hesabı yalnızca birkaç dakika içinde oluşturabileceğiniz."</span><span class="sxs-lookup"><span data-stu-id="d7cf0-194">You can create a free trial account in just a couple of minutes."</span></span>

<span data-ttu-id="d7cf0-195">Bir Azure aboneliğinizin olduğundan eminseniz aboneliğinizin kiracı eşlemesini doğrulayın ve açılır menüden doğru kiracının seçildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-195">If you're certain you have an Azure subscription, validate the tenant mapping for your subscription and ensure the correct tenant is selected in the dropdown.</span></span> <span data-ttu-id="d7cf0-196">Doğrulanacak istenilen kiracının doğru olduğunu, yukarıdaki diyagramı izleyin ve aboneliğiniz ile bu AAD kiracısının eşlemesini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d7cf0-196">If you’ve validated the desired tenant is correct, follow the preceding diagram and validate the mapping of your subscription and this AAD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7cf0-197">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d7cf0-197">Next steps</span></span>
<span data-ttu-id="d7cf0-198">IOT paketi hakkında bilgi almaya devam etmek için işlemine bakın [önceden yapılandırılmış çözümü özelleştirme][lnk-customize].</span><span class="sxs-lookup"><span data-stu-id="d7cf0-198">To continue learning about IoT Suite, see how you can [customize a preconfigured solution][lnk-customize].</span></span>

[img-flowchart]: media/iot-suite-permissions/flowchart.png

[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-rm-github-repo]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-pm-github-repo]: https://github.com/Azure/azure-iot-predictive-maintenance
[lnk-cf-github-repo]: https://github.com/Azure/azure-iot-connected-factory
[lnk-aad-admin]: ../active-directory/active-directory-assign-admin-roles.md
[lnk-classic-portal]: https://manage.windowsazure.com/
[lnk-portal]: https://portal.azure.com/
[lnk-create-edit-users]: ../active-directory/active-directory-create-users.md
[lnk-assign-app-roles]: ../active-directory/active-directory-coreapps-assign-user-azure-portal.md
[lnk-service-admins]: https://azure.microsoft.com/support/changing-service-admin-and-co-admin/
[lnk-admin-roles]: ../billing/billing-add-change-azure-subscription-administrator.md
[lnk-resource-cs]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/DeviceAdministration/Web/Security/RolePermissions.cs
[lnk-help-support]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
