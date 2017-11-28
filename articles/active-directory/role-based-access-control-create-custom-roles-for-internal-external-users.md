---
title: "Özel rol tabanlı erişim denetimi rolleri oluşturmak ve azure'da iç ve dış kullanıcılara atamak | Microsoft Docs"
description: "İç ve dış kullanıcılar için PowerShell ve CLI kullanılarak oluşturulan özel RBAC Rolleri Ata"
services: active-directory
documentationcenter: 
author: andreicradu
manager: catadinu
editor: kgremban
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/10/2017
ms.author: a-crradu
ms.openlocfilehash: d687f94bebfd0b6c1ec0690da798be5409640954
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
## <a name="intro-on-role-based-access-control"></a><span data-ttu-id="2ca2e-103">Giriş rol tabanlı erişim denetimi hakkında</span><span class="sxs-lookup"><span data-stu-id="2ca2e-103">Intro on role-based access control</span></span>

<span data-ttu-id="2ca2e-104">Rol tabanlı erişim denetimi belirli kaynak kapsamları ortamlarında yöneten diğer kullanıcılara ayrıntılı rolleri atamak sahipleri, bir abonelik sağlayan bir Azure portal yalnızca özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-104">Role-based access control is an Azure portal only feature allowing the owners of a subscription to assign granular roles to other users who can manage specific resource scopes in their environment.</span></span>

<span data-ttu-id="2ca2e-105">Dış ortak çalışanları, satıcılar veya ortamınızdaki belirli kaynaklara ancak mutlaka tüm altyapının veya herhangi bir erişim gereken freelancers ile çalışma RBAC büyük kuruluşlarda ve SMB'ler için daha iyi güvenlik yönetimi sağlar Faturalama ilgili kapsamlar.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-105">RBAC allows better security management for large organizations and for SMBs working with external collaborators, vendors or freelancers which need access to specific resources in your environment but not necessarily to the entire infrastructure or any billing-related scopes.</span></span> <span data-ttu-id="2ca2e-106">Bir Azure aboneliğine sahip esnekliğini yönetici hesabı (Hizmet Yöneticisi rolü bir abonelik düzeyinde) tarafından yönetilen ve birden çok kullanıcı aynı abonelik altında ancak tüm yönetim haklarına sahip olmayan çalışmak için davet edildi RBAC sağlar .</span><span class="sxs-lookup"><span data-stu-id="2ca2e-106">RBAC allows the flexibility of owning one Azure subscription managed by the administrator account (service administrator role at a subscription level) and have multiple users invited to work under the same subscription but without any administrative rights for it.</span></span> <span data-ttu-id="2ca2e-107">Bir yönetim ve fatura perspektifi, RBAC Özelliği Azure çeşitli senaryolarda kullanmak için saat ve yönetim verimli bir seçenek kanıtlar.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-107">From a management and billing perspective, the RBAC feature proves to be a time and management efficient option for using Azure in various scenarios.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ca2e-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2ca2e-108">Prerequisites</span></span>
<span data-ttu-id="2ca2e-109">RBAC kullanarak Azure ortamında gerektirir:</span><span class="sxs-lookup"><span data-stu-id="2ca2e-109">Using RBAC in the Azure environment requires:</span></span>

* <span data-ttu-id="2ca2e-110">Azure aboneliği kullanıcıya (abonelik rolü) sahibi olarak atanmış bir tek başına sahip</span><span class="sxs-lookup"><span data-stu-id="2ca2e-110">Having a standalone Azure subscription assigned to the user as owner (subscription role)</span></span>
* <span data-ttu-id="2ca2e-111">Azure aboneliğinin sahibi rolüne sahip</span><span class="sxs-lookup"><span data-stu-id="2ca2e-111">Have the Owner role of the Azure subscription</span></span>
* <span data-ttu-id="2ca2e-112">Erişimi [Azure portalı](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="2ca2e-112">Have access to the [Azure portal](https://portal.azure.com)</span></span>
* <span data-ttu-id="2ca2e-113">Kullanıcı abonelik için kaydedilmiş aşağıdaki kaynak sağlayıcıları bulunduğundan emin olun: **Microsoft.Authorization**.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-113">Make sure to have the following Resource Providers registered for the user subscription: **Microsoft.Authorization**.</span></span> <span data-ttu-id="2ca2e-114">Kaynak sağlayıcıları kaydetme hakkında daha fazla bilgi için bkz: [Resource Manager sağlayıcıları, bölgeleri, API sürümleri ve şemaları](/azure-resource-manager/resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="2ca2e-114">For more information on how to register the resource providers, see [Resource Manager providers, regions, API versions and schemas](/azure-resource-manager/resource-manager-supported-services.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2ca2e-115">Office 365 aboneliği veya Azure Active Directory lisansları (örneğin: Azure Active Directory'ye erişim) portal yok kalitesi RBAC kullanarak O365 sağlandı.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-115">Office 365 subscriptions or Azure Active Directory licenses (for example: Access to Azure Active Directory) provisioned from the O365 portal don't quality for using RBAC.</span></span>

## <a name="how-can-rbac-be-used"></a><span data-ttu-id="2ca2e-116">RBAC nasıl kullanılabileceğini</span><span class="sxs-lookup"><span data-stu-id="2ca2e-116">How can RBAC be used</span></span>
<span data-ttu-id="2ca2e-117">RBAC, Azure üç farklı kapsamlar adresindeki uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-117">RBAC can be applied at three different scopes in Azure.</span></span> <span data-ttu-id="2ca2e-118">En düşük bir üst kapsamdan bunlar şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="2ca2e-118">From the highest scope to the lowest one, they are as follows:</span></span>

* <span data-ttu-id="2ca2e-119">Abonelik (yüksek)</span><span class="sxs-lookup"><span data-stu-id="2ca2e-119">Subscription (highest)</span></span>
* <span data-ttu-id="2ca2e-120">Kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="2ca2e-120">Resource group</span></span>
* <span data-ttu-id="2ca2e-121">Kaynak kapsamı (tek başına bir Azure kaynak kapsam hedeflenen izinleri sunumu düşük erişim düzeyi)</span><span class="sxs-lookup"><span data-stu-id="2ca2e-121">Resource scope (the lowest access level offering targeted permissions to an individual Azure resource scope)</span></span>

## <a name="assign-rbac-roles-at-the-subscription-scope"></a><span data-ttu-id="2ca2e-122">Abonelik kapsamında RBAC Rolleri Ata</span><span class="sxs-lookup"><span data-stu-id="2ca2e-122">Assign RBAC roles at the subscription scope</span></span>
<span data-ttu-id="2ca2e-123">RBAC kullanılan (ancak bunlarla sınırlı olmamak kaydıyla olduğunda) iki ortak örnekler vardır:</span><span class="sxs-lookup"><span data-stu-id="2ca2e-123">There are two common examples when RBAC is used (but not limited to):</span></span>

* <span data-ttu-id="2ca2e-124">Dış kullanıcılar kuruluşlardan sahip bazı kaynaklar ya da tüm abonelik yönetmek için (yönetici kullanıcının Azure Active Directory Kiracı parçası değil) davet</span><span class="sxs-lookup"><span data-stu-id="2ca2e-124">Having external users from the organizations (not part of the admin user's Azure Active Directory tenant) invited to manage certain resources or the whole subscription</span></span>
* <span data-ttu-id="2ca2e-125">Kullanıcılar (bunlar parçası olan kullanıcının Azure Active Directory Kiracı) kuruluş ancak farklı ekipleri ve ayrıntılı erişim tüm abonelik ya da belirli kaynak grupları veya kaynak kapsamlarda gereken grupları parçası içinde ile çalışma ortamı</span><span class="sxs-lookup"><span data-stu-id="2ca2e-125">Working with users inside the organization (they are part of the user's Azure Active Directory tenant) but part of different teams or groups which need granular access either to the whole subscription or to certain resource groups or resource scopes in the environment</span></span>

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a><span data-ttu-id="2ca2e-126">Azure Active Directory dışındaki bir kullanıcı için erişim izni ver abonelik düzeyinde</span><span class="sxs-lookup"><span data-stu-id="2ca2e-126">Grant access at a subscription level for a user outside of Azure Active Directory</span></span>
<span data-ttu-id="2ca2e-127">RBAC rolleri olanağı verilir yalnızca **sahipleri** aboneliği, bu nedenle yönetici kullanıcı, önceden atanmış bu rolü veya Azure aboneliği oluşturduğu bir kullanıcı adıyla oturum açmış olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-127">RBAC roles can be granted only by **Owners** of the subscription therefore the admin user must be logged with a username which has this role pre-assigned or has created the Azure subscription.</span></span>

<span data-ttu-id="2ca2e-128">Oturum Yöneticisi olarak açma sonra Azure portalından "Abonelikleri" ve seçtiğiniz istenen bir seçin.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-128">From the Azure portal, after you sign-in as admin, select “Subscriptions” and chose the desired one.</span></span>
<span data-ttu-id="2ca2e-129">![Azure portalında abonelik dikey penceresinde](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) yönetici kullanıcı Azure aboneliği satın aldıysa varsayılan olarak, kullanıcı olarak görünecek **Hesap Yöneticisi**, bu abonelik rol bırakılıyor.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-129">![subscription blade in Azure portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) By default, if the admin user has purchased the Azure subscription, the user will show up as **Account Admin**, this being the subscription role.</span></span> <span data-ttu-id="2ca2e-130">Azure aboneliği rolleri hakkında daha fazla bilgi için bkz: [abonelik ya da hizmetleri yönetmek ekleme veya değiştirme Azure yönetici rolleri](/billing/billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="2ca2e-130">For more details on the Azure subscription roles, see [Add or change Azure administrator roles that manage the subscription or services](/billing/billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="2ca2e-131">Bu örnekte, kullanıcı "alflanigan@outlook.com" olan **sahibi** "ücretsiz deneme sürümü" AAD abonelikte Kiracı "varsayılan Kiracı Azure".</span><span class="sxs-lookup"><span data-stu-id="2ca2e-131">In this example, the user "alflanigan@outlook.com" is the **Owner** of the "Free Trial" subscription in the AAD tenant "Default tenant Azure".</span></span> <span data-ttu-id="2ca2e-132">Bu kullanıcı ilk Microsoft Account "Outlook" Azure aboneliği oluşturan olduğundan (Microsoft Account Outlook, Canlı vb. =) bu Kiracı eklenen diğer tüm kullanıcılar için varsayılan etki alanı adı olacaktır **"@alflaniganuoutlook.onmicrosoft.com"**.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-132">Since this user is the creator of the Azure subscription with the initial Microsoft Account “Outlook” (Microsoft Account = Outlook, Live etc.) the default domain name for all other users added in this tenant will be **"@alflaniganuoutlook.onmicrosoft.com"**.</span></span> <span data-ttu-id="2ca2e-133">Tasarım gereği, yeni etki alanının sözdizimi Kiracı oluşturan kullanıcının kullanıcı adı ve etki alanı adını bir araya getirilmesi ve uzantı ekleyerek biçimlendirildiğinden **". onmicrosoft.com"**.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-133">By design, the syntax of the new domain is formed by putting together the username and domain name of the user who created the tenant and adding the extension **".onmicrosoft.com"**.</span></span>
<span data-ttu-id="2ca2e-134">Ayrıca, kullanıcıların oturum Kiracı içinde bir özel etki alanı adıyla ekleme ve yeni bir kiracı için doğruladıktan sonra açma.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-134">Furthermore, users can sign-in with a custom domain name in the tenant after adding and verifying it for the new tenant.</span></span> <span data-ttu-id="2ca2e-135">Azure Active Directory kiracısı bir özel etki alanı adını doğrulama hakkında daha fazla ayrıntı için bkz: [bir özel etki alanı adı dizininize eklemek](/active-directory/active-directory-add-domain).</span><span class="sxs-lookup"><span data-stu-id="2ca2e-135">For more details on how to verify a custom domain name in an Azure Active Directory tenant, see [Add a custom domain name to your directory](/active-directory/active-directory-add-domain).</span></span>

<span data-ttu-id="2ca2e-136">Bu örnekte, yalnızca etki alanı adı olan kullanıcılar "Varsayılan Kiracı Azure" dizinini içeren "@alflanigan.onmicrosoft.com".</span><span class="sxs-lookup"><span data-stu-id="2ca2e-136">In this example, the "Default tenant Azure" directory contains only users with the domain name "@alflanigan.onmicrosoft.com".</span></span>

<span data-ttu-id="2ca2e-137">Abonelik seçtikten sonra yönetici kullanıcı tıklatmalısınız **erişim denetimi (IAM)** ve ardından **yeni rol ekleme**.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-137">After selecting the subscription, the admin user must click **Access Control (IAM)** and then **Add a new role**.</span></span>





![erişim denetimi IAM Özelliği Azure portalında](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![erişim denetimi IAM Özelliği Azure portalında yeni kullanıcı Ekle](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

<span data-ttu-id="2ca2e-140">Sonraki adım atanacak rol ve kullanıcı kim RBAC rolü atandı seçmektir.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-140">The next step is to select the role to be assigned and the user whom the RBAC role will be assigned to.</span></span> <span data-ttu-id="2ca2e-141">İçinde **rol** açılır menüsünde Yönetici kullanıcı Azure'da kullanılabilen yalnızca yerleşik RBAC rolleri görür.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-141">In the **Role** dropdown menu the admin user sees only the built-in RBAC roles which are available in Azure.</span></span> <span data-ttu-id="2ca2e-142">Her rol ve bunların atanabilir kapsamların açıklamalarını ayrıntılı için bkz: [Azure rol tabanlı erişim denetimi için yerleşik roller](/active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="2ca2e-142">For more detailed explanations of each role and their assignable scopes, see [Built-in roles for Azure Role-Based Access Control](/active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="2ca2e-143">Yönetici kullanıcı, ardından dış kullanıcı e-posta adresini eklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-143">The admin user then needs to add the email address of the external user.</span></span> <span data-ttu-id="2ca2e-144">Varolan Kiracı göstermemeyi dış kullanıcı için beklenen davranıştır bakın.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-144">The expected behavior is for the external user to not show up in the existing tenant.</span></span> <span data-ttu-id="2ca2e-145">Dış kullanıcı davet sonra kendisinin altında görünür olacak **abonelikleri > erişim denetimi (IAM)** hangi aboneliği kapsamında bir RBAC rolü atanmış olan tüm geçerli kullanıcı ile.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-145">After the external user has been invited, he will be visible under **Subscriptions > Access Control (IAM)** with all the current users which are currently assigned an RBAC role at the Subscription scope.</span></span>





![Yeni RBAC rolü izinleri ekleyin](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![Abonelik düzeyinde RBAC rollerinin listesi](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

<span data-ttu-id="2ca2e-148">Kullanıcı "chessercarlton@gmail.com" olması için davet bir **sahibi** "Ücretsiz deneme" aboneliği için.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-148">The user "chessercarlton@gmail.com" has been invited to be an **Owner** for the “Free Trial” subscription.</span></span> <span data-ttu-id="2ca2e-149">Daveti gönderdikten sonra dış kullanıcı etkinleştirme bağlantısı ile bir e-posta onayı alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-149">After sending the invitation, the external user will receive an email confirmation with an activation link.</span></span>
<span data-ttu-id="2ca2e-150">![e-posta daveti RBAC rolü için](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span><span class="sxs-lookup"><span data-stu-id="2ca2e-150">![email invitation for RBAC role](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span></span>

<span data-ttu-id="2ca2e-151">Kuruluş dış olmasının, yeni kullanıcı varolan öznitelikleri "Varsayılan Kiracı Azure" dizininde yok.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-151">Being external to the organization, the new user does not have any existing attributes in the "Default tenant Azure" directory.</span></span> <span data-ttu-id="2ca2e-152">Dış kullanıcı izin verdiği sonra bunlar oluşturulacak kendisine bir role atanmış olan aboneliği ile ilişkili olan dizin kaydedilecek.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-152">They will be created after the external user has given consent to be recorded in the directory which is associated with the subscription which he has been assigned a role to.</span></span>





![RBAC rolü için e-posta davet iletisi](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

<span data-ttu-id="2ca2e-154">Şu andan itibaren dış kullanıcı olarak Azure Active Directory Kiracı ve bu dış kullanıcı gösterir, hem Azure portalında hem de klasik Portalı'nda görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-154">The external user shows in the Azure Active Directory tenant from now on as external user and this can be viewed both in the Azure portal and in the classic portal.</span></span>





![Kullanıcılar dikey azure active Directory'yi Azure portalı](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![Kullanıcılar dikey azure active directory Klasik Azure portalı](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

<span data-ttu-id="2ca2e-157">İçinde **kullanıcılar** dış kullanıcılar tarafından tanımasını her iki portalları görünümünde:</span><span class="sxs-lookup"><span data-stu-id="2ca2e-157">In the **Users** view in both portals the external users can be recognized by:</span></span>

* <span data-ttu-id="2ca2e-158">Azure portalında farklı simge türü</span><span class="sxs-lookup"><span data-stu-id="2ca2e-158">The different icon type in the Azure portal</span></span>
* <span data-ttu-id="2ca2e-159">Klasik Portalı'nda farklı kaynak belirleme noktası</span><span class="sxs-lookup"><span data-stu-id="2ca2e-159">The different sourcing point in the classic portal</span></span>

<span data-ttu-id="2ca2e-160">Ancak, verme **sahibi** veya **katkıda bulunan** bir dış kullanıcı erişimi **abonelik** kapsamı, yönetici kullanıcının dizinine erişimi sürece izin vermiyor **Genel yönetici** verir.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-160">However, granting **Owner** or **Contributor** access to an external user at the **Subscription** scope, does not allow the access to the admin user's directory, unless the **Global Admin** allows it.</span></span> <span data-ttu-id="2ca2e-161">Kullanıcı proprieties içinde **kullanıcı türü** iki ortak parametreleri olan **üye** ve **Konuk** tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-161">In the user proprieties,  the **User Type** which has two common parameters, **Member** and **Guest** can be identified.</span></span> <span data-ttu-id="2ca2e-162">Konuk bir dış kaynaktan dizine davet bir kullanıcı olsa da dizinde kayıtlı bir kullanıcı bir üyesidir.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-162">A member is a user which is registered in the directory while a guest is a user invited to the directory from an external source.</span></span> <span data-ttu-id="2ca2e-163">Daha fazla bilgi için bkz: [nasıl Azure Active Directory yöneticileri ekleyin B2B işbirliği kullanıcılar](/active-directory/active-directory-b2b-admin-add-users).</span><span class="sxs-lookup"><span data-stu-id="2ca2e-163">For more information, see [How do Azure Active Directory admins add B2B collaboration users](/active-directory/active-directory-b2b-admin-add-users).</span></span>

> [!NOTE]
> <span data-ttu-id="2ca2e-164">Portalda kimlik bilgilerini girdikten sonra emin olun, dış kullanıcı oturum için açmak için doğru dizin seçer.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-164">Make sure that after entering the credentials in the portal, the external user selects the correct directory to sign-in to.</span></span> <span data-ttu-id="2ca2e-165">Aynı kullanıcı birden fazla dizine erişiminiz ve üst taraftaki Azure portalında kullanıcı tıklayarak bunları birini seçin ve ardından açılır listeden uygun dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-165">The same user can have access to multiple directories and can select either one of  them by clicking the username in the top right-hand side in the Azure portal and then choose the appropriate directory from the dropdown list.</span></span>

<span data-ttu-id="2ca2e-166">Dizinde Konuk olmasının, çalışırken dış kullanıcı Azure aboneliğine yönelik tüm kaynakları yönetebilir, ancak dizinine erişilemiyor.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-166">While being a guest in the directory, the external user can manage all resources for the Azure subscription, but can't access the directory.</span></span>





![Azure active Directory'yi Azure portalına sınırlı erişim](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

<span data-ttu-id="2ca2e-168">Azure Active Directory ve Azure aboneliği bir üst-alt ilişkisi gibi diğer Azure kaynaklarına sahip (örneğin: sanal makineler, sanal ağlar, web uygulamaları, depolama vb.) ile Azure aboneliğiniz yok.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-168">Azure Active Directory and an Azure subscription don't have a child-parent relation like other Azure resources (for example: virtual machines, virtual networks, web apps, storage etc.) have with an Azure subscription.</span></span> <span data-ttu-id="2ca2e-169">Tüm ikinci oluşturulur, yönetilen ve bir Azure dizinine erişimi yönetmek için bir Azure aboneliği kullanılırken bir Azure aboneliği altında faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-169">All the latter is created, managed and billed under an Azure subscription while an Azure subscription is used to manage the access to an Azure directory.</span></span> <span data-ttu-id="2ca2e-170">Daha fazla ayrıntı için bkz: [nasıl bir Azure aboneliğine Azure AD ile ilgili](/active-directory/active-directory-how-subscriptions-associated-directory).</span><span class="sxs-lookup"><span data-stu-id="2ca2e-170">For more details, see [How an Azure subscription is related to Azure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span></span>

<span data-ttu-id="2ca2e-171">Tüm rollerden yerleşik RBAC, **sahibi** ve **katkıda bulunan** katılımcı oluşturun ve yeni RBAC rollerini silme olmasına, fark ortamdaki tüm kaynaklar için tam yönetim erişimi sağlar .</span><span class="sxs-lookup"><span data-stu-id="2ca2e-171">From all the built-in RBAC roles, **Owner** and **Contributor** offer full management access to all resources in the environment, the difference being that a Contributor can't create and delete new RBAC roles.</span></span> <span data-ttu-id="2ca2e-172">Diğer yerleşik roller ister **sanal makine Katılımcısı** yalnızca bağımsız olarak, adıyla belirtilen kaynaklarına tam yönetim erişimi teklif **kaynak grubu** içine oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-172">The other built-in roles like **Virtual Machine Contributor** offer full management access only to the resources indicated by the name, regardless of the **Resource Group** they are being created into.</span></span>

<span data-ttu-id="2ca2e-173">Yerleşik RBAC rolü atama **sanal makine Katılımcısı** kullanıcı rolü atanmış bir abonelik düzeyinde anlamına gelir:</span><span class="sxs-lookup"><span data-stu-id="2ca2e-173">Assigning the built-in RBAC role of **Virtual Machine Contributor** at a subscription level, means that the user assigned the role:</span></span>

* <span data-ttu-id="2ca2e-174">Tüm sanal makineleri bakılmaksızın kendi dağıtım tarihi ve parçası olan kaynak gruplarını görüntüleyebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2ca2e-174">Can view all virtual machines regardless their deployment date and the resource groups they are part of</span></span>
* <span data-ttu-id="2ca2e-175">Abonelikteki sanal makinelerin tam yönetim erişimi olan</span><span class="sxs-lookup"><span data-stu-id="2ca2e-175">Has full management access to the virtual machines in the subscription</span></span>
* <span data-ttu-id="2ca2e-176">Başka bir kaynak türleri abonelikte görüntüleyemezsiniz</span><span class="sxs-lookup"><span data-stu-id="2ca2e-176">Can't view any other resource types in the subscription</span></span>
* <span data-ttu-id="2ca2e-177">Fatura perspektifi değişiklikler çalıştırılamıyor</span><span class="sxs-lookup"><span data-stu-id="2ca2e-177">Can't operate any changes from a billing perspective</span></span>

> [!NOTE]
> <span data-ttu-id="2ca2e-178">RBAC, Azure portal yalnızca özelliği olan Klasik portal erişim izni vermez.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-178">RBAC being an Azure portal only feature, it doesn't grant access to the classic portal.</span></span>

## <a name="assign-a-built-in-rbac-role-to-an-external-user"></a><span data-ttu-id="2ca2e-179">Bir dış kullanıcı için bir yerleşik RBAC rolü atayın</span><span class="sxs-lookup"><span data-stu-id="2ca2e-179">Assign a built-in RBAC role to an external user</span></span>
<span data-ttu-id="2ca2e-180">Bu test, dış kullanıcı farklı bir senaryo için "alflanigan@gmail.com" olarak eklenen bir **sanal makine Katılımcısı**.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-180">For a different scenario in this test, the external user "alflanigan@gmail.com" is added as a **Virtual Machine Contributor**.</span></span>




![sanal makine katkıda bulunan yerleşik rolü](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

<span data-ttu-id="2ca2e-182">Normal yerleşik bu rol ile dış bu kullanıcı için bakın ve yalnızca sanal makineler ve bitişik kaynak yöneticisi yalnızca kaynaklarını dağıtırken gereken yönetmek için bir davranıştır.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-182">The normal behavior for this external user with this built-in role is to see and manage only virtual machines and their adjacent Resource Manager only resources necessary while deploying.</span></span> <span data-ttu-id="2ca2e-183">Tasarım gereği, kısıtlı bu rolleri yalnızca Azure portalında oluşturulan karşılık düşen kaynaklarına erişimi sunmak, ne olursa olsun bazı hala Klasik portalda dağıtılabilir (örneğin: sanal makineler).</span><span class="sxs-lookup"><span data-stu-id="2ca2e-183">By design, these limited roles offer access only to their correspondent resources created in the Azure portal, regardless some can still be deployed in the classic portal as well (for example: virtual machines).</span></span>





![azure portalında sanal makine Katılımcısı rolüne genel bakış](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-the-same-directory"></a><span data-ttu-id="2ca2e-185">Aynı dizinde bir kullanıcı için erişim izni ver abonelik düzeyinde</span><span class="sxs-lookup"><span data-stu-id="2ca2e-185">Grant access at a subscription level for a user in the same directory</span></span>
<span data-ttu-id="2ca2e-186">İşlem akışı, bir dış kullanıcı ekleme ile aynıdır, hem kullanıcı yanı sıra RBAC rolü verme yönetici açısından rolüne erişim verilmeden.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-186">The process flow is identical to adding an external user, both from the admin perspective granting the RBAC role as well as the user being granted access to the role.</span></span> <span data-ttu-id="2ca2e-187">Burada oturum açtıktan sonra abonelik içindeki tüm kaynak kapsamları panosunda kullanılabilir olacak şekilde davet edilen kullanıcı e-posta Davetleri almaz farktır.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-187">The difference here is that the invited user will not receive any email invitations as all the resource scopes within the subscription will be available in the dashboard after signing in.</span></span>

## <a name="assign-rbac-roles-at-the-resource-group-scope"></a><span data-ttu-id="2ca2e-188">Kaynak grubu kapsamındaki RBAC Rolleri Ata</span><span class="sxs-lookup"><span data-stu-id="2ca2e-188">Assign RBAC roles at the resource group scope</span></span>
<span data-ttu-id="2ca2e-189">Bir RBAC rolü atama bir **kaynak grubu** kapsama sahip abonelik düzeyinde, her iki tür kullanıcı - harici veya dahili (aynı dizinde parçası) için rol atama için benzer bir işlem.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-189">Assigning an RBAC role at a **Resource Group** scope has an identical process for assigning the role at the subscription level, for both types of users - either external or internal (part of the same directory).</span></span> <span data-ttu-id="2ca2e-190">RBAC rolü atanmış kullanıcılar olduğu kaynak grubu, erişimden atanmış yalnızca ortamlarında görmek için **kaynak grupları** Azure portalında simgesi.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-190">The users which are assigned the RBAC role is to see in their environment only the resource group they have been assigned access from the **Resource Groups** icon in the Azure portal.</span></span>

## <a name="assign-rbac-roles-at-the-resource-scope"></a><span data-ttu-id="2ca2e-191">Kaynak kapsamındaki RBAC Rolleri Ata</span><span class="sxs-lookup"><span data-stu-id="2ca2e-191">Assign RBAC roles at the resource scope</span></span>
<span data-ttu-id="2ca2e-192">Bir kaynak kapsamda Azure RBAC rolü atama abonelik düzeyinde ya da aynı iş akışı içinde her iki senaryoları için aşağıdaki kaynak grubu düzeyinde rol atama için benzer bir işlem var.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-192">Assigning an RBAC role at a resource scope in Azure has an identical process for assigning the role at the subscription level or at the resource group level, following the same workflow for both scenarios.</span></span> <span data-ttu-id="2ca2e-193">RBAC rolü atanmış kullanıcılar yalnızca için ya da erişim, atanmış öğeleri yeniden görebilir **tüm kaynakları** sekmesini veya doğrudan kendi Pano.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-193">Again, the users which are assigned the RBAC role can see only the items that they have been assigned access to, either in the **All Resources** tab or directly in their dashboard.</span></span>

<span data-ttu-id="2ca2e-194">RBAC hem kaynak grup kapsamı veya kaynak kapsamı için önemli bir özelliği doğru dizinine oturum açmak emin olmak kullanıcıları içindir.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-194">An important aspect for RBAC both at resource group scope or resource scope is for the users to make sure to sign-in to the correct directory.</span></span>





![Azure portalında Directory oturum açma](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a><span data-ttu-id="2ca2e-196">Bir Azure Active Directory grubu için RBAC Rolleri Ata</span><span class="sxs-lookup"><span data-stu-id="2ca2e-196">Assign RBAC roles for an Azure Active Directory group</span></span>
<span data-ttu-id="2ca2e-197">Üç farklı kapsamlar Azure RBAC kullanarak tüm senaryoları yönetme, dağıtma ve kişisel bir aboneliği yönetme gerek kalmadan atanmış bir kullanıcı olarak çeşitli kaynakları yönetme ayrıcalık sunar.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-197">All the scenarios using RBAC at the three different scopes in Azure offer the privilege of managing, deploying and administering various resources as an assigned user without the need of managing a personal subscription.</span></span> <span data-ttu-id="2ca2e-198">Ne olursa olsun RBAC rolü abonelik, kaynak grubu veya kaynak kapsamı, tüm kullanıcıların erişimi sahip olduğu bir Azure aboneliği altında hakkında daha fazla atanmış kullanıcılar tarafından oluşturulan kaynakları faturalandırılır atanır.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-198">Regardless the RBAC role is assigned for a subscription, resource group or resource scope, all the resources created further on by the assigned users are billed under the one Azure subscription where the users have access to.</span></span> <span data-ttu-id="2ca2e-199">Bu şekilde, tüm Azure aboneliğiniz için yönetici izinleri faturalama kullanıcılar var. eksiksiz bir genel görünüm tüketimi, bakılmaksızın kimin kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="2ca2e-199">This way, the users who have billing administrator permissions for that entire Azure subscription has a complete overview on the consumption, regardless who is managing the resources.</span></span>

<span data-ttu-id="2ca2e-200">Büyük kuruluşlar için yönetici kullanıcının ekipleri ve tüm bölümler için bu nedenle dikkate alarak, her bir kullanıcı için değil tek tek parçalı erişim vermek istediği perspektif dikkate Azure Active Directory grupları için aynı şekilde RBAC rolleri uygulanabilir. Bu isteğe bağlı olarak son derece saat ve yönetim etkin.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-200">For larger organizations, RBAC roles can be applied in the same way for Azure Active Directory groups considering the perspective that the admin user wants to grant the granular access for teams or entire departments, not individually for each user, thus considering it as an extremely time and management efficient option.</span></span> <span data-ttu-id="2ca2e-201">Bu örnekte, göstermeye **katkıda bulunan** rol, bir kiracı abonelik düzeyinde gruplarının eklendi.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-201">To illustrate this example, the **Contributor** role has been added to one of the groups in the tenant at the subscription level.</span></span>





![AAD grupları için RBAC rolü Ekle](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

<span data-ttu-id="2ca2e-203">Bu grupları sağlanan ve yalnızca Azure Active Directory içinde yönetilen güvenlik gruplarıdır.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-203">These groups are security groups which are provisioned and managed only within Azure Active Directory.</span></span>

## <a name="create-a-custom-rbac-role-to-open-support-requests-using-powershell"></a><span data-ttu-id="2ca2e-204">PowerShell kullanarak destek istekleri açmak için özel bir RBAC rolü oluşturun</span><span class="sxs-lookup"><span data-stu-id="2ca2e-204">Create a custom RBAC role to open support requests using PowerShell</span></span>
<span data-ttu-id="2ca2e-205">Azure'da kullanılabilen yerleşik RBAC roller ortamında kullanılabilir kaynaklara dayalı belirli izin düzeyleri emin olun.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-205">The built-in RBAC roles which are available in Azure ensure certain permission levels based on the available resources in the environment.</span></span> <span data-ttu-id="2ca2e-206">Ancak, bu rollerin hiçbiri yönetici kullanıcının gereksinimlerinize uygun değilse, daha fazla özel RBAC rolleri oluşturarak erişimi sınırlamak için bir seçenek yoktur.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-206">However, if none of these roles suit the admin user's needs, there is the option to limit access even more by creating custom RBAC roles.</span></span>

<span data-ttu-id="2ca2e-207">Özel RBAC rolleri oluşturmak için bir yerleşik rolü, düzenlemek ve ortam geri almak için gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-207">Creating custom RBAC roles requires to take one built-in role, edit it and then import it back in the environment.</span></span> <span data-ttu-id="2ca2e-208">Rolünün karşıya yükleme ve indirme PowerShell veya CLI kullanılarak yönetilir.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-208">The download and upload of the role are managed using either PowerShell or CLI.</span></span>

<span data-ttu-id="2ca2e-209">Abonelik düzeyinde ayrıntılı erişim vermek ve aynı zamanda davet edilen kullanıcı destek isteği açma esnekliğini tanımak özel bir rol oluşturarak Önkoşullar anlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-209">It is important to understand the prerequisites of creating a custom role which can grant granular access at the subscription level and also allow the invited user the flexibility of opening support requests.</span></span>

<span data-ttu-id="2ca2e-210">Bu örneğin yerleşik rol **okuyucu** kullanıcılar tüm kaynak kapsamları görüntülemek üzere ancak bunları düzenleyin veya yeni kampanya oluşturmak erişim sağlayan destek isteği açma seçeneğini izin vermek için özelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-210">For this example the built-in role **Reader** which allows users access to view all the resource scopes but not to edit them or create new ones has been customized to allow the user the option of opening support requests.</span></span>

<span data-ttu-id="2ca2e-211">Dışarı aktarma ilk eylemi **okuyucu** rol PowerShell'de tamamlanması gerekiyor yönetici olarak yükseltilmiş izinlerle çalıştı.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-211">The first action of exporting the **Reader** role needs to be completed in PowerShell ran with elevated permissions as administrator.</span></span>

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![Okuyucu RBAC rolü için PowerShell ekran görüntüsü](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

<span data-ttu-id="2ca2e-213">Ardından rolünün JSON şablonunu ayıklamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-213">Then you need to extract the JSON template of the role.</span></span>





![Özel okuyucu RBAC rolü için JSON şablonunu](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

<span data-ttu-id="2ca2e-215">Tipik bir RBAC rolü üç ana bölüm dışında oluşan **Eylemler**, **NotActions** ve **AssignableScopes**.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-215">A typical RBAC role is composed out of three main sections, **Actions**, **NotActions** and **AssignableScopes**.</span></span>

<span data-ttu-id="2ca2e-216">İçinde **eylem** bölümü olan bu rol için izin verilen tüm işlemler listelenir.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-216">In the **Action** section are listed all the permitted operations for this role.</span></span> <span data-ttu-id="2ca2e-217">Her eylemin kaynak sağlayıcısından atandığı anlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-217">It's important to understand that each action is assigned from a resource provider.</span></span> <span data-ttu-id="2ca2e-218">Bu durumda, destek biletlerini oluşturmak için **Microsoft.Support** kaynak sağlayıcısı listelenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-218">In this case, for creating support tickets the **Microsoft.Support** resource provider must be listed.</span></span>

<span data-ttu-id="2ca2e-219">Kullanılabilir ve aboneliğinizde kayıtlı ilgili tüm kaynak sağlayıcıları kullanabilmek için PowerShell'i kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-219">To be able to see all the resource providers available and registered in your subscription, you can use PowerShell.</span></span>
```
Get-AzureRMResourceProvider

```
<span data-ttu-id="2ca2e-220">Ayrıca, kaynak sağlayıcıları yönetmek tüm kullanılabilir için PowerShell cmdlet'leri kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-220">Additionally, you can check for the all the available PowerShell cmdlets to manage the resource providers.</span></span>
    <span data-ttu-id="2ca2e-221">![Kaynak sağlayıcısı yönetimi için PowerShell ekran görüntüsü](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span><span class="sxs-lookup"><span data-stu-id="2ca2e-221">![PowerShell screenshot for resource provider management](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span></span>

<span data-ttu-id="2ca2e-222">Belirli bir RBAC rolü için tüm eylemleri kısıtlamak için kaynak sağlayıcıları bölümü altında listelenen **NotActions**.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-222">To restrict all the actions for a particular RBAC role, resource providers are listed under the section **NotActions**.</span></span>
<span data-ttu-id="2ca2e-223">Son olarak, RBAC rolü açık abonelik kimlikleri kullanıldığı içeren zorunludur.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-223">Last, it's mandatory that the RBAC role contains the explicit subscription IDs where it is used.</span></span> <span data-ttu-id="2ca2e-224">Abonelik kimlikleri altında listelenen **AssignableScopes**, aksi takdirde, aboneliğinizde rolünü içeri aktarmak için izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-224">The subscription IDs are listed under the **AssignableScopes**, otherwise you will not be allowed to import the role in your subscription.</span></span>

<span data-ttu-id="2ca2e-225">Oluşturma ve RBAC rolü özelleştirme sonra aktarılması gereken ortamını yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-225">After creating and customizing the RBAC role, it needs to be imported back the environment.</span></span>

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

<span data-ttu-id="2ca2e-226">Bu örnekte, özel bu RBAC rolü için "okuyucu destek biletleri erişim düzeyi kullanıcının her şeyi abonelikte görüntülemek ve destek istekleri açmaya izin verme" adıdır.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-226">In this example, the custom name for this RBAC role is "Reader support tickets access level" allowing the user to view everything in the subscription and also to open support requests.</span></span>

> [!NOTE]
> <span data-ttu-id="2ca2e-227">Destek isteği açma eylemi izin verme yalnızca iki yerleşik RBAC rolleri **sahibi** ve **katkıda bulunan**.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-227">The only two built-in RBAC roles allowing the action of opening of support requests are **Owner** and **Contributor**.</span></span> <span data-ttu-id="2ca2e-228">Destek istekleri açmak bir kullanıcı için tüm destek isteklerini bir Azure aboneliğine yönelik temel alınarak oluşturulur çünkü kendisine yalnızca abonelik kapsamında bir RBAC rolü atanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-228">For a user to be able to open support requests, he must be assigned an RBAC role only at the subscription scope, because all support requests are created based on an Azure subscription.</span></span>

<span data-ttu-id="2ca2e-229">Bu yeni özel rolü aynı dizinden bir kullanıcıya atandı.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-229">This new custom role has been assigned to an user from the same directory.</span></span>





![Azure portalında içeri özel RBAC rolü ekran görüntüsü](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![kullanıcı aynı dizinde özel alınan RBAC rol atama işleminin ekran görüntüsü](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![Özel alınan RBAC rolü izinlerini ekran görüntüsü](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

<span data-ttu-id="2ca2e-233">Bu özel RBAC rolü sınırları gibi vurgulamak için örnek daha ayrıntılı:</span><span class="sxs-lookup"><span data-stu-id="2ca2e-233">The example has been further detailed to emphasize the limits of this custom RBAC role as follows:</span></span>
* <span data-ttu-id="2ca2e-234">Yeni destek istekleri oluşturabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="2ca2e-234">Can create new support requests</span></span>
* <span data-ttu-id="2ca2e-235">Yeni kaynak kapsamlar oluşturulamıyor (örneğin: sanal makine)</span><span class="sxs-lookup"><span data-stu-id="2ca2e-235">Can't create new resource scopes (for example: virtual machine)</span></span>
* <span data-ttu-id="2ca2e-236">Yeni kaynak grupları oluşturulamıyor</span><span class="sxs-lookup"><span data-stu-id="2ca2e-236">Can't create new resource groups</span></span>





![Özel RBAC rolü destek istekleri oluşturma ekran görüntüsü](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![ekran görüntüsü özel RBAC rolü VM'ler oluşturmak mümkün değil](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![ekran görüntüsü özel RBAC rolü yeni RGs oluşturmak mümkün değil](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-to-open-support-requests-using-azure-cli"></a><span data-ttu-id="2ca2e-240">Azure CLI kullanarak destek istekleri açmak için özel bir RBAC rolü oluşturun</span><span class="sxs-lookup"><span data-stu-id="2ca2e-240">Create a custom RBAC role to open support requests using Azure CLI</span></span>
<span data-ttu-id="2ca2e-241">Mac ve PowerShell erişmesini olmadan çalışan, Azure CLI Git yoludur.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-241">Running on a Mac and without having access to PowerShell, Azure CLI is the way to go.</span></span>

<span data-ttu-id="2ca2e-242">Özel bir rol oluşturmak için aşağıdaki adımları, rol CLI kullanarak bir JSON şablonu indirilemiyor ancak CLI görüntülenebilir tek özel durumu ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-242">The steps to create a custom role are the same, with the sole exception that using CLI the role can't be downloaded in a JSON template, but it can be viewed in the CLI.</span></span>

<span data-ttu-id="2ca2e-243">Bu örnek için t yerleşik rolü seçtiniz **yedekleme okuyucu**.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-243">For this example I have chosen the built-in role of **Backup Reader**.</span></span>

```

azure role show "backup reader" --json

```





![CLI ekran görüntüsü yedekleme okuyucu rolüne Göster](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

<span data-ttu-id="2ca2e-245">Bir JSON şablonu proprieties kopyaladıktan sonra Visual Studio rolünde düzenleme **Microsoft.Support** kaynak sağlayıcısı eklendi **Eylemler** böylece bu kullanıcı destek bölümler Okuyucu için yedekleme kasalarını olmasını etmeden istek sayısı.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-245">Editing the role in Visual Studio after copying the proprieties in a JSON template, the **Microsoft.Support** resource provider has been added in the **Actions** sections so that this user can open support requests while continuing to be a reader for the backup vaults.</span></span> <span data-ttu-id="2ca2e-246">Burada bu rolü kullanılacak, abonelik kimliği eklemek gerekli olan yeniden **AssignableScopes** bölümü.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-246">Again it is necessary to add the subscription ID where this role will be used in the **AssignableScopes** section.</span></span>

```

azure role create --inputfile <path>

```





![Özel RBAC rolü alma CLI ekran görüntüsü](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

<span data-ttu-id="2ca2e-248">Yeni rol Azure portalında kullanılabilir ve atamasını önceki örneklerde olduğu gibi aynı işlemidir.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-248">The new role is now available in the Azure portal and the assignation process is the same as in the previous examples.</span></span>





![CLI 1.0 kullanılarak oluşturulan özel RBAC rolü Azure portal ekran görüntüsü](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

<span data-ttu-id="2ca2e-250">Son yapı 2017'dan sonra Azure bulut Kabuk genel kullanıma açıktır.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-250">As of the latest Build 2017, the Azure Cloud Shell is generally available.</span></span> <span data-ttu-id="2ca2e-251">Azure bulut Kabuk tamamlayan bir IDE ve Azure Portal ' dir.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-251">Azure Cloud Shell is a complement to IDE and the Azure Portal.</span></span> <span data-ttu-id="2ca2e-252">Bu hizmeti ile kimlik doğrulaması ve Azure içinde barındırılan ve tarayıcı tabanlı bir kabuk alın ve makinenize yüklü CLI yerine kullanın.</span><span class="sxs-lookup"><span data-stu-id="2ca2e-252">With this service, you get a browser-based shell that is authenticated and hosted within Azure and you can use it instead of CLI installed on your machine.</span></span>





![Azure bulut Kabuğu](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)
