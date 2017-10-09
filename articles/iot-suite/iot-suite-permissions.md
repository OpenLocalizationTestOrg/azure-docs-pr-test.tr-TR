---
title: aaaAzure IOT paketi ve Azure Active Directory | Microsoft Docs
description: "Azure IOT paketi Azure Active Directory toomanage izinleri nasıl kullandığını açıklar."
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
ms.openlocfilehash: 4768630f2de4bb431731fbd4e8929232bc80b9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-on-hello-azureiotsuitecom-site"></a><span data-ttu-id="78b35-103">Merhaba azureiotsuite.com sitesindeki izinler</span><span class="sxs-lookup"><span data-stu-id="78b35-103">Permissions on hello azureiotsuite.com site</span></span>

## <a name="what-happens-when-you-sign-in"></a><span data-ttu-id="78b35-104">Oturum açtığınızda ne olur</span><span class="sxs-lookup"><span data-stu-id="78b35-104">What happens when you sign in</span></span>

<span data-ttu-id="78b35-105">Merhaba, oturum açtığınızda ilk kez [azureiotsuite.com][lnk-azureiotsuite], hello site belirler sahip hello üzerinde şu anda hello izin düzeyleri seçili Azure Active Directory (AAD) kiracısına ve Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="78b35-105">hello first time you sign in at [azureiotsuite.com][lnk-azureiotsuite], hello site determines hello permission levels you have based on hello currently selected Azure Active Directory (AAD) tenant and Azure subscription.</span></span>

1. <span data-ttu-id="78b35-106">İlk olarak, toopopulate hello listesi görülen kiracılar sonraki tooyour kullanıcıadı hello site Azure'dan hangi AAD kiracılarına ait olduğunuz öğrenir.</span><span class="sxs-lookup"><span data-stu-id="78b35-106">First, toopopulate hello list of tenants seen next tooyour username, hello site finds out from Azure which AAD tenants you belong to.</span></span> <span data-ttu-id="78b35-107">Şu anda hello site aynı anda yalnızca bir kiracı için kullanıcı belirteçleri alabilir.</span><span class="sxs-lookup"><span data-stu-id="78b35-107">Currently, hello site can only obtain user tokens for one tenant at a time.</span></span> <span data-ttu-id="78b35-108">Merhaba açılır hello sağ üst köşedeki kullanarak kiracılar geçiş yaptığınızda, bu nedenle, hello siteyi, toothat Kiracı tooobtain hello belirteçlerinde bu Kiracı için günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="78b35-108">Therefore, when you switch tenants using hello dropdown in hello top right corner, hello site logs you in toothat tenant tooobtain hello tokens for that tenant.</span></span>

2. <span data-ttu-id="78b35-109">Kiracı hello ile ilişkili abonelikleri seçili Azure'dan ardından, hello site öğrenir.</span><span class="sxs-lookup"><span data-stu-id="78b35-109">Next, hello site finds out from Azure which subscriptions you have associated with hello selected tenant.</span></span> <span data-ttu-id="78b35-110">Yeni bir önceden yapılandırılmış çözümü oluşturduğunuzda hello kullanılabilir abonelikleri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="78b35-110">You see hello available subscriptions when you create a new preconfigured solution.</span></span>

3. <span data-ttu-id="78b35-111">Son olarak, tüm hello kaynakları hello Aboneliklerde hello site alır ve kaynak grupları önceden yapılandırılmış çözümler olarak etiketlenmiş ve hello hello giriş sayfasındaki kutucukları doldurur.</span><span class="sxs-lookup"><span data-stu-id="78b35-111">Finally, hello site retrieves all hello resources in hello subscriptions and resource groups tagged as preconfigured solutions and populates hello tiles on hello home page.</span></span>

<span data-ttu-id="78b35-112">Aşağıdaki bölümlerde hello erişim toohello önceden yapılandırılmış çözümleri denetlemek hello roller açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="78b35-112">hello following sections describe hello roles that control access toohello preconfigured solutions.</span></span>

## <a name="aad-roles"></a><span data-ttu-id="78b35-113">AAD rolleri</span><span class="sxs-lookup"><span data-stu-id="78b35-113">AAD roles</span></span>

<span data-ttu-id="78b35-114">Merhaba AAD rolleri hello özelliği önceden yapılandırılmış çözümleri sağlama denetlemek ve önceden yapılandırılmış bir çözümdeki kullanıcıları yönetme.</span><span class="sxs-lookup"><span data-stu-id="78b35-114">hello AAD roles control hello ability provision preconfigured solutions and manage users in a preconfigured solution.</span></span>

<span data-ttu-id="78b35-115">AAD'de yönetici rolleri hakkında daha fazla bilgi bulabilirsiniz [Azure AD'de yönetici rolleri atama][lnk-aad-admin].</span><span class="sxs-lookup"><span data-stu-id="78b35-115">You can find more information about administrator roles in AAD in [Assigning administrator roles in Azure AD][lnk-aad-admin].</span></span> <span data-ttu-id="78b35-116">Merhaba geçerli makale üzerinde hello odaklanır **genel yönetici** ve hello **kullanıcı** hello tarafından kullanılan directory rolleri önceden yapılandırılmış çözümleri.</span><span class="sxs-lookup"><span data-stu-id="78b35-116">hello current article focuses on hello **Global Administrator** and hello **User** directory roles as used by hello preconfigured solutions.</span></span>

### <a name="global-administrator"></a><span data-ttu-id="78b35-117">Genel yönetici</span><span class="sxs-lookup"><span data-stu-id="78b35-117">Global administrator</span></span>

<span data-ttu-id="78b35-118">AAD kiracısı başına çok sayıda genel yönetici olabilir:</span><span class="sxs-lookup"><span data-stu-id="78b35-118">There can be many global administrators per AAD tenant:</span></span>

* <span data-ttu-id="78b35-119">Bir AAD kiracısı oluşturduğunuzda varsayılan hello genel yönetici, Kiracı tarafından olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="78b35-119">When you create an AAD tenant, you are by default hello global administrator of that tenant.</span></span>
* <span data-ttu-id="78b35-120">Merhaba genel yönetici önceden yapılandırılmış bir çözüm sağlayabilir ve atanmış bir **yönetici** hello uygulamanın AAD kiracısının içinde rol.</span><span class="sxs-lookup"><span data-stu-id="78b35-120">hello global administrator can provision a preconfigured solution and is assigned an **Admin** role for hello application inside their AAD tenant.</span></span>
* <span data-ttu-id="78b35-121">Başka bir kullanıcı aynı Merhaba, AAD kiracısı bir uygulama oluşturur, hello varsayılan rol toohello genel yönetici verilir **salt okunur**.</span><span class="sxs-lookup"><span data-stu-id="78b35-121">If another user in hello same AAD tenant creates an application, hello default role granted toohello global administrator is **ReadOnly**.</span></span>
* <span data-ttu-id="78b35-122">Genel yönetici hello kullanan uygulamalar için kullanıcıların tooroles atayabilirsiniz [Azure portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="78b35-122">A global administrator can assign users tooroles for applications using hello [Azure portal][lnk-portal].</span></span>

### <a name="domain-user"></a><span data-ttu-id="78b35-123">Etki alanı kullanıcısı</span><span class="sxs-lookup"><span data-stu-id="78b35-123">Domain user</span></span>

<span data-ttu-id="78b35-124">AAD kiracısı başına çok sayıda etki alanı kullanıcı olabilir:</span><span class="sxs-lookup"><span data-stu-id="78b35-124">There can be many domain users per AAD tenant:</span></span>

* <span data-ttu-id="78b35-125">Bir etki alanı kullanıcısı hello üzerinden önceden yapılandırılmış bir çözüm sağlayabilir [azureiotsuite.com] [ lnk-azureiotsuite] site.</span><span class="sxs-lookup"><span data-stu-id="78b35-125">A domain user can provision a preconfigured solution through hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="78b35-126">Varsayılan olarak, hello hello etki alanı kullanıcı izni **yönetici** hello rolünde sağlanan uygulama.</span><span class="sxs-lookup"><span data-stu-id="78b35-126">By default, hello domain user is granted hello **Admin** role in hello provisioned application.</span></span>
* <span data-ttu-id="78b35-127">Bir etki alanı kullanıcısı hello hello build.cmd komut dosyası kullanarak bir uygulama oluşturabilirsiniz [azure-iot-remote-monitoring][lnk-rm-github-repo], [azure-iot-predictive-maintenance] [ lnk-pm-github-repo], veya [azure-IOT-bağlı-Fabrika] [ lnk-cf-github-repo] deposu.</span><span class="sxs-lookup"><span data-stu-id="78b35-127">A domain user can create an application using hello build.cmd script in hello [azure-iot-remote-monitoring][lnk-rm-github-repo],  [azure-iot-predictive-maintenance][lnk-pm-github-repo], or [azure-iot-connected-factory][lnk-cf-github-repo] repository.</span></span> <span data-ttu-id="78b35-128">Ancak, hello varsayılan rol toohello etki alanı kullanıcısı verilir **salt okunur**, çünkü bir etki alanı kullanıcı izni tooassign rolleri yok.</span><span class="sxs-lookup"><span data-stu-id="78b35-128">However, hello default role granted toohello domain user is **ReadOnly**, because a domain user does not have permission tooassign roles.</span></span>
* <span data-ttu-id="78b35-129">Merhaba AAD kiracısında başka bir kullanıcı bir uygulama oluşturduğunda hello etki alanı kullanıcısı hello atanan **ReadOnly** rolü bu uygulama için varsayılan.</span><span class="sxs-lookup"><span data-stu-id="78b35-129">If another user in hello AAD tenant creates an application, hello domain user is assigned hello **ReadOnly** role by default for that application.</span></span>
* <span data-ttu-id="78b35-130">Bir etki alanı kullanıcısı uygulamalar için roller atayamazsınız; Bu nedenle bunlar olsa bile bir etki alanı kullanıcısı kullanıcıları veya bir uygulama için kullanıcıların rollerini ekleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="78b35-130">A domain user cannot assign roles for applications; therefore a domain user cannot add users or roles for users for an application even if they provisioned it.</span></span>

### <a name="guest-user"></a><span data-ttu-id="78b35-131">Konuk kullanıcı</span><span class="sxs-lookup"><span data-stu-id="78b35-131">Guest User</span></span>

<span data-ttu-id="78b35-132">AAD kiracısı başına çok sayıda Konuk kullanıcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="78b35-132">There can be many guest users per AAD tenant.</span></span> <span data-ttu-id="78b35-133">Konuk kullanıcılar hello AAD kiracısında sınırlı bir haklar kümesine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="78b35-133">Guest users have a limited set of rights in hello AAD tenant.</span></span> <span data-ttu-id="78b35-134">Sonuç olarak, Konuk kullanıcılar hello AAD kiracısında önceden yapılandırılmış bir çözüm sağlayamaz.</span><span class="sxs-lookup"><span data-stu-id="78b35-134">As a result, guest users cannot provision a preconfigured solution in hello AAD tenant.</span></span>

<span data-ttu-id="78b35-135">Kullanıcılar ve roller aad'de hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="78b35-135">For more information about users and roles in AAD, see hello following resources:</span></span>

* <span data-ttu-id="78b35-136">[Azure AD'de kullanıcı oluşturma][lnk-create-edit-users]</span><span class="sxs-lookup"><span data-stu-id="78b35-136">[Create users in Azure AD][lnk-create-edit-users]</span></span>
* <span data-ttu-id="78b35-137">[Kullanıcıların tooapps atayın][lnk-assign-app-roles]</span><span class="sxs-lookup"><span data-stu-id="78b35-137">[Assign users tooapps][lnk-assign-app-roles]</span></span>

## <a name="azure-subscription-administrator-roles"></a><span data-ttu-id="78b35-138">Azure abonelik yöneticisi rolleri</span><span class="sxs-lookup"><span data-stu-id="78b35-138">Azure subscription administrator roles</span></span>

<span data-ttu-id="78b35-139">Hello Azure yönetici rolleri hello özelliği toomap bir Azure aboneliği tooan AD Kiracı denetler.</span><span class="sxs-lookup"><span data-stu-id="78b35-139">hello Azure admin roles control hello ability toomap an Azure subscription tooan AD tenant.</span></span>

<span data-ttu-id="78b35-140">Merhaba makalede hello Azure yöneticisi rolleri hakkında daha fazla bilgi [nasıl tooadd veya Azure ortak yönetici, Hizmet Yöneticisi ve Hesap Yöneticisi değiştirme][lnk-admin-roles].</span><span class="sxs-lookup"><span data-stu-id="78b35-140">Find out more about hello Azure admin roles in hello article [How tooadd or change Azure Co-Administrator, Service Administrator, and Account Administrator][lnk-admin-roles].</span></span>

## <a name="application-roles"></a><span data-ttu-id="78b35-141">Uygulama rolleri</span><span class="sxs-lookup"><span data-stu-id="78b35-141">Application roles</span></span>

<span data-ttu-id="78b35-142">Merhaba uygulama rolleri önceden yapılandırılmış çözümünüzdeki erişim toodevices denetler.</span><span class="sxs-lookup"><span data-stu-id="78b35-142">hello application roles control access toodevices in your preconfigured solution.</span></span>

<span data-ttu-id="78b35-143">İki tanımlanmış rol ve sağlanan bir uygulamada bir örtük rol mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="78b35-143">There are two defined roles and one implicit role defined in a provisioned application:</span></span>

* <span data-ttu-id="78b35-144">**Yönetici:** yönetmek, cihazları kaldırın ve ayarlarını değiştirme tam denetim tooadd sahiptir.</span><span class="sxs-lookup"><span data-stu-id="78b35-144">**Admin:** Has full control tooadd, manage, remove devices, and modify settings.</span></span>
* <span data-ttu-id="78b35-145">**Salt okunur:** aygıtlar, kurallar, Eylemler, işleri ve telemetri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78b35-145">**ReadOnly:** Can view devices, rules, actions, jobs, and telemetry.</span></span>

<span data-ttu-id="78b35-146">Merhaba izinlerine hello tooeach rolünde bulabilirsiniz [RolePermissions.cs] [ lnk-resource-cs] kaynak dosyası.</span><span class="sxs-lookup"><span data-stu-id="78b35-146">You can find hello permissions assigned tooeach role in hello [RolePermissions.cs][lnk-resource-cs] source file.</span></span>

### <a name="changing-application-roles-for-a-user"></a><span data-ttu-id="78b35-147">Bir kullanıcının uygulama rollerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="78b35-147">Changing application roles for a user</span></span>

<span data-ttu-id="78b35-148">Aşağıdaki yordam toomake bir kullanıcı Active Directory'de yönetici önceden yapılandırılmış çözümünüzün hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78b35-148">You can use hello following procedure toomake a user in your Active Directory an administrator of your preconfigured solution.</span></span>

<span data-ttu-id="78b35-149">Bir kullanıcı için bir AAD genel Yöneticisi toochange rolleri olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="78b35-149">You must be an AAD global administrator toochange roles for a user:</span></span>

1. <span data-ttu-id="78b35-150">Toohello Git [Azure portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="78b35-150">Go toohello [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="78b35-151">Seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="78b35-151">Select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="78b35-152">Çözümünüzü sağlarken azureiotsuite.com üzerinde seçtiğiniz hello dizin kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="78b35-152">Make sure you are using hello directory you chose on azureiotsuite.com when you provisioned your solution.</span></span> <span data-ttu-id="78b35-153">Aboneliğinizle ilişkili birden fazla dizine sahipseniz, bunları hesap adınızı hello sağ üst hello Portal'ı tıklatırsanız arasında geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78b35-153">If you have multiple directories associated with your subscription, you can switch between them if you click your account name at hello top-right of hello portal.</span></span>
4. <span data-ttu-id="78b35-154">Tıklatın **kurumsal uygulamalar**, ardından **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="78b35-154">Click **Enterprise applications**, then **All applications**.</span></span>
4. <span data-ttu-id="78b35-155">Göster **tüm uygulamaları** ile **herhangi** durumu.</span><span class="sxs-lookup"><span data-stu-id="78b35-155">Show **All applications** with **Any** status.</span></span> <span data-ttu-id="78b35-156">Ardından, önceden yapılandırılmış çözümünüz ada sahip bir uygulama arayın.</span><span class="sxs-lookup"><span data-stu-id="78b35-156">Then search for an application with name of your preconfigured solution.</span></span>
5. <span data-ttu-id="78b35-157">Merhaba, önceden yapılandırılmış çözümünüzün adıyla eşleşen hello uygulamanın adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="78b35-157">Click hello name of hello application that matches your preconfigured solution name.</span></span>
6. <span data-ttu-id="78b35-158">tıklatın **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="78b35-158">Click **Users and groups**.</span></span>
7. <span data-ttu-id="78b35-159">Tooswitch rolleri hello kullanıcıyı seçin.</span><span class="sxs-lookup"><span data-stu-id="78b35-159">Select hello user you want tooswitch roles.</span></span>
8. <span data-ttu-id="78b35-160">' I tıklatın **atamak** ve select hello rolü (gibi **yönetici**) tooassign toohello kullanıcı istediğiniz hello onay işaretine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="78b35-160">Click **Assign** and select hello role (such as **Admin**) you'd like tooassign toohello user, click hello check mark.</span></span>

## <a name="faq"></a><span data-ttu-id="78b35-161">SSS</span><span class="sxs-lookup"><span data-stu-id="78b35-161">FAQ</span></span>

### <a name="im-a-service-administrator-and-id-like-toochange-hello-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a><span data-ttu-id="78b35-162">Bir hizmet yöneticisiyim ve Aboneliğim ile belirli bir AAD kiracısı arasında toochange hello dizin eşlemesini istiyorum.</span><span class="sxs-lookup"><span data-stu-id="78b35-162">I'm a service administrator and I'd like toochange hello directory mapping between my subscription and a specific AAD tenant.</span></span> <span data-ttu-id="78b35-163">Bu görevi nasıl tamamlamak?</span><span class="sxs-lookup"><span data-stu-id="78b35-163">How do I complete this task?</span></span>

1. <span data-ttu-id="78b35-164">Toohello Git [Klasik Azure portalı][lnk-classic-portal], tıklatın **ayarları** hello hello sol taraftaki Hizmet listesinde.</span><span class="sxs-lookup"><span data-stu-id="78b35-164">Go toohello [Azure classic portal][lnk-classic-portal], click **Settings** in hello list of services on hello left-hand side.</span></span>
2. <span data-ttu-id="78b35-165">Toochange hello dizin eşlemesi için istediğiniz hello aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="78b35-165">Select hello subscription you'd like toochange hello directory mapping to.</span></span>
3. <span data-ttu-id="78b35-166">**Dizini Düzenle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="78b35-166">Click **Edit Directory**.</span></span>
4. <span data-ttu-id="78b35-167">Select hello **Directory** hello açılır toouse istersiniz.</span><span class="sxs-lookup"><span data-stu-id="78b35-167">Select hello **Directory** you would like toouse in hello dropdown.</span></span> <span data-ttu-id="78b35-168">Merhaba İleri okuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="78b35-168">Click hello forward arrow.</span></span>
5. <span data-ttu-id="78b35-169">Merhaba dizin eşlemesini doğrulayın ve etkilenen ortak yöneticileri.</span><span class="sxs-lookup"><span data-stu-id="78b35-169">Confirm hello directory mapping and affected co-administrators.</span></span> <span data-ttu-id="78b35-170">Başka bir dizinden taşıyorsanız, hello özgün dizindeki tüm hello ortak Yöneticiler kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="78b35-170">If you are moving from another directory, all hello co-administrators from hello original directory are removed.</span></span>

### <a name="im-a-domain-usermember-on-hello-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a><span data-ttu-id="78b35-171">Merhaba AAD kiracısı üzerinde etki alanı kullanıcısı/üyesi ben ve önceden yapılandırılmış bir çözüm oluşturduğunuzu düşünün.</span><span class="sxs-lookup"><span data-stu-id="78b35-171">I'm a domain user/member on hello AAD tenant and I've created a preconfigured solution.</span></span> <span data-ttu-id="78b35-172">Uygulamam için bana nasıl rol atanır?</span><span class="sxs-lookup"><span data-stu-id="78b35-172">How do I get assigned a role for my application?</span></span>

<span data-ttu-id="78b35-173">Genel yönetici toomake hello AAD genel bir yönetici, Kiracı ve rolleri toousers kendinize atayın isteyin.</span><span class="sxs-lookup"><span data-stu-id="78b35-173">Ask a global administrator toomake you a global administrator on hello AAD tenant and then assign roles toousers yourself.</span></span> <span data-ttu-id="78b35-174">Alternatif olarak, bir genel yönetici tooassign isteyin, doğrudan bir rolü.</span><span class="sxs-lookup"><span data-stu-id="78b35-174">Alternatively, ask a global administrator tooassign you a role directly.</span></span> <span data-ttu-id="78b35-175">Önceden yapılandırılmış çözümünüzün dağıtıldı toochange hello AAD kiracısı isterseniz hello sonraki soruya bakın.</span><span class="sxs-lookup"><span data-stu-id="78b35-175">If you'd like toochange hello AAD tenant your preconfigured solution has been deployed to, see hello next question.</span></span>

### <a name="how-do-i-switch-hello-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a><span data-ttu-id="78b35-176">My önceden yapılandırılmış Uzaktan izleme çözümü ve uygulama atandığını hello AAD kiracısına nasıl geçiş yapabilirim?</span><span class="sxs-lookup"><span data-stu-id="78b35-176">How do I switch hello AAD tenant my remote monitoring preconfigured solution and application are assigned to?</span></span>

<span data-ttu-id="78b35-177"><https://github.com/Azure/azure-iot-remote-monitoring> adresinden bir bulut dağıtımını yeniden çalıştırabilir ve yeni oluşturulan bir AAD kiracısı ile yeniden dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78b35-177">You can run a cloud deployment from <https://github.com/Azure/azure-iot-remote-monitoring> and redeploy with a newly created AAD tenant.</span></span> <span data-ttu-id="78b35-178">Varsayılan olarak, bir AAD kiracısı oluşturduğunuzda, bir genel yönetici olduğu için tooadd kullanıcıların izinlere sahip ve toothose kullanıcı rolleri atayın.</span><span class="sxs-lookup"><span data-stu-id="78b35-178">Because you are, by default, a global administrator when you create an AAD tenant, you have permissions tooadd users and assign roles toothose users.</span></span>

1. <span data-ttu-id="78b35-179">Hello bir AAD dizini oluşturun [Azure portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="78b35-179">Create an AAD directory in hello [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="78b35-180">Çok Git<https://github.com/Azure/azure-iot-remote-monitoring>.</span><span class="sxs-lookup"><span data-stu-id="78b35-180">Go too<https://github.com/Azure/azure-iot-remote-monitoring>.</span></span>
3. <span data-ttu-id="78b35-181">`build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` komutunu çalıştırın (Örneğin, `build.cmd cloud debug myRMSolution`)</span><span class="sxs-lookup"><span data-stu-id="78b35-181">Run `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (For example, `build.cmd cloud debug myRMSolution`)</span></span>
4. <span data-ttu-id="78b35-182">İstendiğinde, hello ayarlamak **tenantıd** toobe değerini önceki kiracınız yerine yeni oluşturduğunuz Kiracı.</span><span class="sxs-lookup"><span data-stu-id="78b35-182">When prompted, set hello **tenantid** toobe your newly created tenant instead of your previous tenant.</span></span>

### <a name="i-want-toochange-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a><span data-ttu-id="78b35-183">Bir Hizmet Yöneticisi veya bir hesabıyla oturum açtığımda ortak yöneticiyi toochange istiyorum</span><span class="sxs-lookup"><span data-stu-id="78b35-183">I want toochange a Service Administrator or Co-Administrator when logged in with an organisational account</span></span>

<span data-ttu-id="78b35-184">Merhaba destek makalesine bakın [değiştirme Hizmet Yöneticisi ve bir hesabıyla oturum açtığımda ortak yöneticiyi][lnk-service-admins].</span><span class="sxs-lookup"><span data-stu-id="78b35-184">See hello support article [Changing Service Administrator and Co-Administrator when logged in with an organisational account][lnk-service-admins].</span></span>

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-hello-proper-permissions-toocreate-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a><span data-ttu-id="78b35-185">Bu hatayı neden görüyorum?</span><span class="sxs-lookup"><span data-stu-id="78b35-185">Why am I seeing this error?</span></span> <span data-ttu-id="78b35-186">"Hesabınız hello uygun izinleri toocreate bir çözüm yok.</span><span class="sxs-lookup"><span data-stu-id="78b35-186">"Your account does not have hello proper permissions toocreate a solution.</span></span> <span data-ttu-id="78b35-187">Lütfen hesap yöneticinize başvurun veya farklı bir hesap ile deneyin."</span><span class="sxs-lookup"><span data-stu-id="78b35-187">Please check with your account administrator or try with a different account."</span></span>

<span data-ttu-id="78b35-188">Diyagram Kılavuzu izleyerek hello bakın:</span><span class="sxs-lookup"><span data-stu-id="78b35-188">Look at hello following diagram for guidance:</span></span>

![][img-flowchart]

> [!NOTE]
> <span data-ttu-id="78b35-189">Toosee hello hata devam ederse doğrulandıktan sonra hello AAD kiracısında genel yönetici ve hello abonelik ortak yönetici demektir, hesap yöneticinize hello kullanıcıyı kaldırabilir ve gerekli izinleri şu sırayla yeniden atamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="78b35-189">If you continue toosee hello error after validating you are a global administrator on hello AAD tenant and a co-administrator on hello subscription, have your account administrator remove hello user and reassign necessary permissions in this order.</span></span> <span data-ttu-id="78b35-190">İlk olarak, hello kullanıcı genel yönetici olarak ekleyin ve sonra hello Azure aboneliğinin ortak yönetici olarak kullanıcı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="78b35-190">First, add hello user as a global administrator and then add user as a co-administrator on hello Azure subscription.</span></span> <span data-ttu-id="78b35-191">Sorun devam ederse başvurun [Yardım ve Destek][lnk-help-support].</span><span class="sxs-lookup"><span data-stu-id="78b35-191">If issues persist, contact [Help & Support][lnk-help-support].</span></span>

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-toocreate-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a><span data-ttu-id="78b35-192">Bir Azure aboneliğim varken bu hatayı neden görüyorum?</span><span class="sxs-lookup"><span data-stu-id="78b35-192">Why am I seeing this error when I have an Azure subscription?</span></span> <span data-ttu-id="78b35-193">"Azure aboneliği gerekli toocreate önceden yapılandırılmış çözümleri 'dir.</span><span class="sxs-lookup"><span data-stu-id="78b35-193">"An Azure subscription is required toocreate pre-configured solutions.</span></span> <span data-ttu-id="78b35-194">Ücretsiz bir deneme hesabı yalnızca birkaç dakika içinde oluşturabileceğiniz."</span><span class="sxs-lookup"><span data-stu-id="78b35-194">You can create a free trial account in just a couple of minutes."</span></span>

<span data-ttu-id="78b35-195">Bir Azure aboneliğinizin olduğundan eminseniz aboneliğinizin eşleme hello Kiracı doğrulayın ve hello doğru Kiracı hello açılır listede seçildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="78b35-195">If you're certain you have an Azure subscription, validate hello tenant mapping for your subscription and ensure hello correct tenant is selected in hello dropdown.</span></span> <span data-ttu-id="78b35-196">Doğrulanacak hello Kiracı doğru istenen, diyagram önceki hello izleyin ve aboneliğiniz ile bu AAD kiracısının hello eşleme doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="78b35-196">If you’ve validated hello desired tenant is correct, follow hello preceding diagram and validate hello mapping of your subscription and this AAD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="78b35-197">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="78b35-197">Next steps</span></span>
<span data-ttu-id="78b35-198">IOT paketi hakkında öğrenme toocontinue bkz nasıl [önceden yapılandırılmış çözümü özelleştirme][lnk-customize].</span><span class="sxs-lookup"><span data-stu-id="78b35-198">toocontinue learning about IoT Suite, see how you can [customize a preconfigured solution][lnk-customize].</span></span>

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
