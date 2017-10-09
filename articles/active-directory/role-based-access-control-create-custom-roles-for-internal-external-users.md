---
title: "aaaCreate özel rol tabanlı erişim denetimi rolleri ve toointernal ve azure'da dış kullanıcılar atayın | Microsoft Docs"
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
ms.openlocfilehash: 26793a66d6ca2f771338eed87d10ce2b3b431841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="intro-on-role-based-access-control"></a><span data-ttu-id="f851d-103">Giriş rol tabanlı erişim denetimi hakkında</span><span class="sxs-lookup"><span data-stu-id="f851d-103">Intro on role-based access control</span></span>

<span data-ttu-id="f851d-104">Rol tabanlı erişim denetimi belirli kaynak kapsamları ortamlarında yönetebilen tooassign ayrıntılı rolleri tooother kullanıcıların bir abonelik hello sahipleri vererek bir Azure portal yalnızca özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="f851d-104">Role-based access control is an Azure portal only feature allowing hello owners of a subscription tooassign granular roles tooother users who can manage specific resource scopes in their environment.</span></span>

<span data-ttu-id="f851d-105">Dış ortak çalışanları, satıcılar veya ortamınızda ancak mutlaka toohello tüm altyapının veya herhangi bir toospecific kaynaklara erişim freelancers ile çalışma RBAC büyük kuruluşlarda ve SMB'ler için daha iyi güvenlik yönetimi sağlar Faturalama ilgili kapsamlar.</span><span class="sxs-lookup"><span data-stu-id="f851d-105">RBAC allows better security management for large organizations and for SMBs working with external collaborators, vendors or freelancers which need access toospecific resources in your environment but not necessarily toohello entire infrastructure or any billing-related scopes.</span></span> <span data-ttu-id="f851d-106">RBAC hello yönetici hesabı (Hizmet Yöneticisi rolü bir abonelik düzeyinde) tarafından yönetilen bir Azure aboneliğine sahip hello esnekliği sağlar ve sahip birden çok kullanıcıları davet toowork altında hello aynı aboneliği olmadan herhangi Yönetim Bu hakları.</span><span class="sxs-lookup"><span data-stu-id="f851d-106">RBAC allows hello flexibility of owning one Azure subscription managed by hello administrator account (service administrator role at a subscription level) and have multiple users invited toowork under hello same subscription but without any administrative rights for it.</span></span> <span data-ttu-id="f851d-107">Yönetim ve fatura perspektifi hello RBAC Özelliği Azure çeşitli senaryolarda kullanmak için saat ve yönetim verimli bir seçenek toobe kanıtlar.</span><span class="sxs-lookup"><span data-stu-id="f851d-107">From a management and billing perspective, hello RBAC feature proves toobe a time and management efficient option for using Azure in various scenarios.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f851d-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f851d-108">Prerequisites</span></span>
<span data-ttu-id="f851d-109">RBAC hello Azure ortamı kullanmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="f851d-109">Using RBAC in hello Azure environment requires:</span></span>

* <span data-ttu-id="f851d-110">Tek başına sahip Azure aboneliği toohello kullanıcı (abonelik rolü) sahibi olarak atanmış.</span><span class="sxs-lookup"><span data-stu-id="f851d-110">Having a standalone Azure subscription assigned toohello user as owner (subscription role)</span></span>
* <span data-ttu-id="f851d-111">Merhaba sahibi hello Azure aboneliği rolünüz</span><span class="sxs-lookup"><span data-stu-id="f851d-111">Have hello Owner role of hello Azure subscription</span></span>
* <span data-ttu-id="f851d-112">Erişim toohello sahip [Azure portalı](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="f851d-112">Have access toohello [Azure portal](https://portal.azure.com)</span></span>
* <span data-ttu-id="f851d-113">Kaynak sağlayıcıları aşağıdaki toohave hello hello kullanıcı abonelik için kayıtlı olduğundan emin olun: **Microsoft.Authorization**.</span><span class="sxs-lookup"><span data-stu-id="f851d-113">Make sure toohave hello following Resource Providers registered for hello user subscription: **Microsoft.Authorization**.</span></span> <span data-ttu-id="f851d-114">Nasıl tooregister hello kaynak sağlayıcıları ile ilgili daha fazla bilgi için bkz: [Resource Manager sağlayıcıları, bölgeleri, API sürümleri ve şemaları](/azure-resource-manager/resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="f851d-114">For more information on how tooregister hello resource providers, see [Resource Manager providers, regions, API versions and schemas](/azure-resource-manager/resource-manager-supported-services.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f851d-115">Office 365 aboneliği veya Azure Active Directory lisansları (örneğin: tooAzure Active Directory erişimi) portal yok kalitesi RBAC kullanarak hello O365 sağlandı.</span><span class="sxs-lookup"><span data-stu-id="f851d-115">Office 365 subscriptions or Azure Active Directory licenses (for example: Access tooAzure Active Directory) provisioned from hello O365 portal don't quality for using RBAC.</span></span>

## <a name="how-can-rbac-be-used"></a><span data-ttu-id="f851d-116">RBAC nasıl kullanılabileceğini</span><span class="sxs-lookup"><span data-stu-id="f851d-116">How can RBAC be used</span></span>
<span data-ttu-id="f851d-117">RBAC, Azure üç farklı kapsamlar adresindeki uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="f851d-117">RBAC can be applied at three different scopes in Azure.</span></span> <span data-ttu-id="f851d-118">Merhaba yüksek kapsam toohello düşük bir, bunlar şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="f851d-118">From hello highest scope toohello lowest one, they are as follows:</span></span>

* <span data-ttu-id="f851d-119">Abonelik (yüksek)</span><span class="sxs-lookup"><span data-stu-id="f851d-119">Subscription (highest)</span></span>
* <span data-ttu-id="f851d-120">Kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="f851d-120">Resource group</span></span>
* <span data-ttu-id="f851d-121">Kaynak kapsamı (tooan tek başına bir Azure kaynak kapsam hedeflenen izinleri sunumu hello düşük erişim düzeyi)</span><span class="sxs-lookup"><span data-stu-id="f851d-121">Resource scope (hello lowest access level offering targeted permissions tooan individual Azure resource scope)</span></span>

## <a name="assign-rbac-roles-at-hello-subscription-scope"></a><span data-ttu-id="f851d-122">Merhaba abonelik kapsamında RBAC Rolleri Ata</span><span class="sxs-lookup"><span data-stu-id="f851d-122">Assign RBAC roles at hello subscription scope</span></span>
<span data-ttu-id="f851d-123">RBAC kullanılan (ancak bunlarla sınırlı olmamak kaydıyla olduğunda) iki ortak örnekler vardır:</span><span class="sxs-lookup"><span data-stu-id="f851d-123">There are two common examples when RBAC is used (but not limited to):</span></span>

* <span data-ttu-id="f851d-124">Dış kullanıcılar hello kuruluşların (Merhaba yönetici kullanıcının Azure Active Directory Kiracı parçası değil) sahip toomanage belirli kaynaklar veya hello tüm abonelik davet</span><span class="sxs-lookup"><span data-stu-id="f851d-124">Having external users from hello organizations (not part of hello admin user's Azure Active Directory tenant) invited toomanage certain resources or hello whole subscription</span></span>
* <span data-ttu-id="f851d-125">Merhaba kuruluş (bunlar hello kullanıcının Azure Active Directory Kiracı parçası olan), ancak farklı ekipler veya ayrıntılı erişmeniz gruplarını parçası içindeki kullanıcılarla ya da toohello çalışma, tüm abonelik veya toocertain kaynak grupları veya kaynak hello kapsamları ortamı</span><span class="sxs-lookup"><span data-stu-id="f851d-125">Working with users inside hello organization (they are part of hello user's Azure Active Directory tenant) but part of different teams or groups which need granular access either toohello whole subscription or toocertain resource groups or resource scopes in hello environment</span></span>

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a><span data-ttu-id="f851d-126">Azure Active Directory dışındaki bir kullanıcı için erişim izni ver abonelik düzeyinde</span><span class="sxs-lookup"><span data-stu-id="f851d-126">Grant access at a subscription level for a user outside of Azure Active Directory</span></span>
<span data-ttu-id="f851d-127">RBAC rolleri olanağı verilir yalnızca **sahipleri** hello aboneliği, bu nedenle hello yönetici kullanıcı, önceden atanmış bu rolü veya hello Azure aboneliği oluşturduğu bir kullanıcı adıyla oturum açmış olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f851d-127">RBAC roles can be granted only by **Owners** of hello subscription therefore hello admin user must be logged with a username which has this role pre-assigned or has created hello Azure subscription.</span></span>

<span data-ttu-id="f851d-128">Hello Azure portal sonra oturum açma yönetici, seçin "Abonelikleri" ve seçtiğiniz hello bir istenen.</span><span class="sxs-lookup"><span data-stu-id="f851d-128">From hello Azure portal, after you sign-in as admin, select “Subscriptions” and chose hello desired one.</span></span>
<span data-ttu-id="f851d-129">![Azure portalında abonelik dikey penceresinde](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) hello yönetici kullanıcı hello Azure aboneliği satın aldıysa varsayılan olarak, hello kullanıcı olarak görüntülenecek **Hesap Yöneticisi**, bu hello abonelik rol bırakılıyor.</span><span class="sxs-lookup"><span data-stu-id="f851d-129">![subscription blade in Azure portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) By default, if hello admin user has purchased hello Azure subscription, hello user will show up as **Account Admin**, this being hello subscription role.</span></span> <span data-ttu-id="f851d-130">Hello Azure aboneliği rolleri hakkında daha fazla bilgi için bkz: [hello abonelik ya da hizmetleri yönetmek ekleme veya değiştirme Azure yönetici rolleri](/billing/billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="f851d-130">For more details on hello Azure subscription roles, see [Add or change Azure administrator roles that manage hello subscription or services](/billing/billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="f851d-131">Bu örnekte, kullanıcı hello "alflanigan@outlook.com" Merhaba olan **sahibi** "Ücretsiz deneme" hello hello AAD abonelikte Kiracı "varsayılan Kiracı Azure".</span><span class="sxs-lookup"><span data-stu-id="f851d-131">In this example, hello user "alflanigan@outlook.com" is hello **Owner** of hello "Free Trial" subscription in hello AAD tenant "Default tenant Azure".</span></span> <span data-ttu-id="f851d-132">Bu kullanıcı hello Azure aboneliği hello ile Merhaba oluşturan olduğundan Microsoft Account "Outlook" ilk (Microsoft Account Outlook, Canlı vb. =) bu Kiracı eklenen diğer tüm kullanıcılar için hello varsayılan etki alanı adı olacaktır **"@alflaniganuoutlook.onmicrosoft.com"**.</span><span class="sxs-lookup"><span data-stu-id="f851d-132">Since this user is hello creator of hello Azure subscription with hello initial Microsoft Account “Outlook” (Microsoft Account = Outlook, Live etc.) hello default domain name for all other users added in this tenant will be **"@alflaniganuoutlook.onmicrosoft.com"**.</span></span> <span data-ttu-id="f851d-133">Tasarım gereği, birlikte hello Kiracı ve ekleme hello uzantısı oluşturan hello kullanıcının hello kullanıcı adı ve etki alanı adı koyarak hello sözdizimi hello yeni etki alanının biçimlendirildiğinden **". onmicrosoft.com"**.</span><span class="sxs-lookup"><span data-stu-id="f851d-133">By design, hello syntax of hello new domain is formed by putting together hello username and domain name of hello user who created hello tenant and adding hello extension **".onmicrosoft.com"**.</span></span>
<span data-ttu-id="f851d-134">Ayrıca, kullanıcıların oturum hello Kiracı içinde bir özel etki alanı adıyla ekleme ve hello yeni Kiracı için doğruladıktan sonra açma.</span><span class="sxs-lookup"><span data-stu-id="f851d-134">Furthermore, users can sign-in with a custom domain name in hello tenant after adding and verifying it for hello new tenant.</span></span> <span data-ttu-id="f851d-135">Tooverify bir Azure Active Directory Kiracı özel etki alanı adının nasıl görürüm hakkında daha fazla ayrıntı için [bir özel etki alanı adı tooyour dizin eklemek](/active-directory/active-directory-add-domain).</span><span class="sxs-lookup"><span data-stu-id="f851d-135">For more details on how tooverify a custom domain name in an Azure Active Directory tenant, see [Add a custom domain name tooyour directory](/active-directory/active-directory-add-domain).</span></span>

<span data-ttu-id="f851d-136">Bu örnekte, yalnızca hello etki alanı adına sahip kullanıcılar hello "varsayılan Kiracı Azure" dizinini içeren "@alflanigan.onmicrosoft.com".</span><span class="sxs-lookup"><span data-stu-id="f851d-136">In this example, hello "Default tenant Azure" directory contains only users with hello domain name "@alflanigan.onmicrosoft.com".</span></span>

<span data-ttu-id="f851d-137">Merhaba abonelik seçtikten sonra hello yönetici kullanıcı tıklatmalısınız **erişim denetimi (IAM)** ve ardından **yeni rol ekleme**.</span><span class="sxs-lookup"><span data-stu-id="f851d-137">After selecting hello subscription, hello admin user must click **Access Control (IAM)** and then **Add a new role**.</span></span>





![erişim denetimi IAM Özelliği Azure portalında](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![erişim denetimi IAM Özelliği Azure portalında yeni kullanıcı Ekle](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

<span data-ttu-id="f851d-140">Merhaba sonraki atanan tooselect hello rol toobe ve hello RBAC rolü atandı hello kullanıcıyı adımdır.</span><span class="sxs-lookup"><span data-stu-id="f851d-140">hello next step is tooselect hello role toobe assigned and hello user whom hello RBAC role will be assigned to.</span></span> <span data-ttu-id="f851d-141">Merhaba, **rol** açılır menü hello yönetici kullanıcı Azure'da kullanılabilen yalnızca hello yerleşik RBAC rolleri görür.</span><span class="sxs-lookup"><span data-stu-id="f851d-141">In hello **Role** dropdown menu hello admin user sees only hello built-in RBAC roles which are available in Azure.</span></span> <span data-ttu-id="f851d-142">Her rol ve bunların atanabilir kapsamların açıklamalarını ayrıntılı için bkz: [Azure rol tabanlı erişim denetimi için yerleşik roller](/active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="f851d-142">For more detailed explanations of each role and their assignable scopes, see [Built-in roles for Azure Role-Based Access Control](/active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="f851d-143">Merhaba yönetici kullanıcı ardından hello dış kullanıcı tooadd hello e-posta adresi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="f851d-143">hello admin user then needs tooadd hello email address of hello external user.</span></span> <span data-ttu-id="f851d-144">Merhaba hello dış kullanıcı toonot görünecektir Kiracı varolan hello için davranış bekleniyordu.</span><span class="sxs-lookup"><span data-stu-id="f851d-144">hello expected behavior is for hello external user toonot show up in hello existing tenant.</span></span> <span data-ttu-id="f851d-145">Merhaba dış kullanıcı davet sonra kendisinin altında görünür olacak **abonelikleri > erişim denetimi (IAM)** hello abonelik kapsamını bir RBAC rolü atanmış olan tüm hello geçerli kullanıcılar ile.</span><span class="sxs-lookup"><span data-stu-id="f851d-145">After hello external user has been invited, he will be visible under **Subscriptions > Access Control (IAM)** with all hello current users which are currently assigned an RBAC role at hello Subscription scope.</span></span>





![izinleri toonew RBAC rolü Ekle](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![Abonelik düzeyinde RBAC rollerinin listesi](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

<span data-ttu-id="f851d-148">Merhaba kullanıcı "chessercarlton@gmail.com" davet edilen toobe bırakıldı bir **sahibi** hello "Ücretsiz deneme" aboneliği için.</span><span class="sxs-lookup"><span data-stu-id="f851d-148">hello user "chessercarlton@gmail.com" has been invited toobe an **Owner** for hello “Free Trial” subscription.</span></span> <span data-ttu-id="f851d-149">Hello davet gönderdikten sonra hello dış kullanıcı etkinleştirme bağlantısı ile bir e-posta onayı alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="f851d-149">After sending hello invitation, hello external user will receive an email confirmation with an activation link.</span></span>
<span data-ttu-id="f851d-150">![e-posta daveti RBAC rolü için](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span><span class="sxs-lookup"><span data-stu-id="f851d-150">![email invitation for RBAC role](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span></span>

<span data-ttu-id="f851d-151">Dış toohello kuruluş olmasının, hello yeni kullanıcı varolan öznitelikleri hello "varsayılan Kiracı Azure" dizininde yok.</span><span class="sxs-lookup"><span data-stu-id="f851d-151">Being external toohello organization, hello new user does not have any existing attributes in hello "Default tenant Azure" directory.</span></span> <span data-ttu-id="f851d-152">Merhaba dış kullanıcı onayı toobe kendisine bir role atanan hello aboneliği ile ilişkili olan hello dizinde kayıtlı verdiği sonra bunlar oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f851d-152">They will be created after hello external user has given consent toobe recorded in hello directory which is associated with hello subscription which he has been assigned a role to.</span></span>





![RBAC rolü için e-posta davet iletisi](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

<span data-ttu-id="f851d-154">Merhaba dış kullanıcı hello Azure Active Directory Kiracı şu andan itibaren dış kullanıcı olarak gösterilir ve bu hello Azure portalına hem hello Klasik Portalı'nda görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="f851d-154">hello external user shows in hello Azure Active Directory tenant from now on as external user and this can be viewed both in hello Azure portal and in hello classic portal.</span></span>





![Kullanıcılar dikey azure active Directory'yi Azure portalı](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![Kullanıcılar dikey azure active directory Klasik Azure portalı](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

<span data-ttu-id="f851d-157">Merhaba, **kullanıcılar** hem portalları hello dış kullanıcılar görünümünde tarafından tanımasını:</span><span class="sxs-lookup"><span data-stu-id="f851d-157">In hello **Users** view in both portals hello external users can be recognized by:</span></span>

* <span data-ttu-id="f851d-158">hello Azure portal Hello farklı simge türü</span><span class="sxs-lookup"><span data-stu-id="f851d-158">hello different icon type in hello Azure portal</span></span>
* <span data-ttu-id="f851d-159">başlangıç noktası hello Klasik Portalı'ndaki kaynak Hizmeti'nden farklı</span><span class="sxs-lookup"><span data-stu-id="f851d-159">hello different sourcing point in hello classic portal</span></span>

<span data-ttu-id="f851d-160">Ancak, verme **sahibi** veya **katkıda bulunan** hello kullanıcıya erişim tooan dış **abonelik** kapsam, hello erişim toohello yönetici kullanıcının dizin izin vermiyor sürece hello **genel yönetici** verir.</span><span class="sxs-lookup"><span data-stu-id="f851d-160">However, granting **Owner** or **Contributor** access tooan external user at hello **Subscription** scope, does not allow hello access toohello admin user's directory, unless hello **Global Admin** allows it.</span></span> <span data-ttu-id="f851d-161">Merhaba kullanıcı proprieties içinde hello **kullanıcı türü** iki ortak parametreleri olan **üye** ve **Konuk** tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="f851d-161">In hello user proprieties,  hello **User Type** which has two common parameters, **Member** and **Guest** can be identified.</span></span> <span data-ttu-id="f851d-162">Konuk kullanıcı davet toohello directory bir dış kaynaktan olsa da, hello dizinde kayıtlı bir kullanıcı bir üyesidir.</span><span class="sxs-lookup"><span data-stu-id="f851d-162">A member is a user which is registered in hello directory while a guest is a user invited toohello directory from an external source.</span></span> <span data-ttu-id="f851d-163">Daha fazla bilgi için bkz: [nasıl Azure Active Directory yöneticileri ekleyin B2B işbirliği kullanıcılar](/active-directory/active-directory-b2b-admin-add-users).</span><span class="sxs-lookup"><span data-stu-id="f851d-163">For more information, see [How do Azure Active Directory admins add B2B collaboration users](/active-directory/active-directory-b2b-admin-add-users).</span></span>

> [!NOTE]
> <span data-ttu-id="f851d-164">Merhaba Portalı'nda Hello kimlik bilgilerini girdikten sonra hello dış kullanıcı hello doğru dizinde toosign-için seçtiği emin olun.</span><span class="sxs-lookup"><span data-stu-id="f851d-164">Make sure that after entering hello credentials in hello portal, hello external user selects hello correct directory toosign-in to.</span></span> <span data-ttu-id="f851d-165">Merhaba aynı kullanıcı erişim toomultiple dizinler sahiptir ve ya da bunlardan birini üst sağ taraftaki hello Azure portal hello hello kullanıcı tıklayarak seçebilir ve ardından hello uygun dizin hello açılır listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="f851d-165">hello same user can have access toomultiple directories and can select either one of  them by clicking hello username in hello top right-hand side in hello Azure portal and then choose hello appropriate directory from hello dropdown list.</span></span>

<span data-ttu-id="f851d-166">Merhaba dizinde Konuk olmasının, çalışırken hello dış kullanıcı hello Azure aboneliği için tüm kaynakları yönetebilir, ancak hello dizinine erişilemiyor.</span><span class="sxs-lookup"><span data-stu-id="f851d-166">While being a guest in hello directory, hello external user can manage all resources for hello Azure subscription, but can't access hello directory.</span></span>





![kısıtlı tooazure active Directory'yi Azure portalına erişim](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

<span data-ttu-id="f851d-168">Azure Active Directory ve Azure aboneliği bir üst-alt ilişkisi gibi diğer Azure kaynaklarına sahip (örneğin: sanal makineler, sanal ağlar, web uygulamaları, depolama vb.) ile Azure aboneliğiniz yok.</span><span class="sxs-lookup"><span data-stu-id="f851d-168">Azure Active Directory and an Azure subscription don't have a child-parent relation like other Azure resources (for example: virtual machines, virtual networks, web apps, storage etc.) have with an Azure subscription.</span></span> <span data-ttu-id="f851d-169">Tüm hello ikinci oluşturulur, yönetilen ve bir Azure aboneliği kullanılan toomanage hello erişim tooan Azure directory olsa da bir Azure aboneliği altında faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="f851d-169">All hello latter is created, managed and billed under an Azure subscription while an Azure subscription is used toomanage hello access tooan Azure directory.</span></span> <span data-ttu-id="f851d-170">Daha fazla ayrıntı için bkz: [nasıl bir Azure aboneliği olan ilgili tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span><span class="sxs-lookup"><span data-stu-id="f851d-170">For more details, see [How an Azure subscription is related tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span></span>

<span data-ttu-id="f851d-171">Tüm rollerden hello yerleşik RBAC, **sahibi** ve **katkıda bulunan** tooall kaynaklarında hello ortamı, katılımcı oluşturulamıyor hello fark olan ve yeni Sil tam yönetim erişimi sağlar RBAC rolleri.</span><span class="sxs-lookup"><span data-stu-id="f851d-171">From all hello built-in RBAC roles, **Owner** and **Contributor** offer full management access tooall resources in hello environment, hello difference being that a Contributor can't create and delete new RBAC roles.</span></span> <span data-ttu-id="f851d-172">Merhaba diğer yerleşik roller ister **sanal makine Katılımcısı** tam yönetim erişimi yalnızca hello bakılmaksızın hello adıyla belirtilen toohello kaynakları sunan **kaynak grubu** bunlar oluşturuluyor .</span><span class="sxs-lookup"><span data-stu-id="f851d-172">hello other built-in roles like **Virtual Machine Contributor** offer full management access only toohello resources indicated by hello name, regardless of hello **Resource Group** they are being created into.</span></span>

<span data-ttu-id="f851d-173">Atama hello yerleşik RBAC rolü **sanal makine Katılımcısı** abonelik düzeyinde o hello kullanıcıya atanan hello rol anlamına gelir:</span><span class="sxs-lookup"><span data-stu-id="f851d-173">Assigning hello built-in RBAC role of **Virtual Machine Contributor** at a subscription level, means that hello user assigned hello role:</span></span>

* <span data-ttu-id="f851d-174">Tüm sanal makineleri bakılmaksızın parçası olan kendi dağıtım tarihi ve hello kaynak grupları görüntüleyebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f851d-174">Can view all virtual machines regardless their deployment date and hello resource groups they are part of</span></span>
* <span data-ttu-id="f851d-175">Tam yönetim erişimi toohello sanal makineye hello abonelikte sahiptir</span><span class="sxs-lookup"><span data-stu-id="f851d-175">Has full management access toohello virtual machines in hello subscription</span></span>
* <span data-ttu-id="f851d-176">Başka bir kaynak türleri hello abonelikte görüntüleyemezsiniz</span><span class="sxs-lookup"><span data-stu-id="f851d-176">Can't view any other resource types in hello subscription</span></span>
* <span data-ttu-id="f851d-177">Fatura perspektifi değişiklikler çalıştırılamıyor</span><span class="sxs-lookup"><span data-stu-id="f851d-177">Can't operate any changes from a billing perspective</span></span>

> [!NOTE]
> <span data-ttu-id="f851d-178">RBAC, Azure portal yalnızca özelliği olan erişim toohello Klasik portal izni vermez.</span><span class="sxs-lookup"><span data-stu-id="f851d-178">RBAC being an Azure portal only feature, it doesn't grant access toohello classic portal.</span></span>

## <a name="assign-a-built-in-rbac-role-tooan-external-user"></a><span data-ttu-id="f851d-179">Yerleşik RBAC rolü tooan dış kullanıcı atama</span><span class="sxs-lookup"><span data-stu-id="f851d-179">Assign a built-in RBAC role tooan external user</span></span>
<span data-ttu-id="f851d-180">Bu test farklı bir senaryo için dış kullanıcı hello "alflanigan@gmail.com" olarak eklenen bir **sanal makine Katılımcısı**.</span><span class="sxs-lookup"><span data-stu-id="f851d-180">For a different scenario in this test, hello external user "alflanigan@gmail.com" is added as a **Virtual Machine Contributor**.</span></span>




![sanal makine katkıda bulunan yerleşik rolü](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

<span data-ttu-id="f851d-182">Bu yerleşik rolü bu dış kullanıcı için normal davranışı Hello toosee olduğu ve yalnızca sanal makineler ve bitişik kaynak yöneticisi yalnızca kaynaklarını dağıtırken gereken yönetin.</span><span class="sxs-lookup"><span data-stu-id="f851d-182">hello normal behavior for this external user with this built-in role is toosee and manage only virtual machines and their adjacent Resource Manager only resources necessary while deploying.</span></span> <span data-ttu-id="f851d-183">Tasarım gereği, kısıtlı bu rolleri erişim hello Azure portalında oluşturulan yalnızca tootheir karşılık düşen kaynakları sunar, ne olursa olsun bazı hala hello Klasik Portalı'nda da dağıtılabilir (örneğin: sanal makineler).</span><span class="sxs-lookup"><span data-stu-id="f851d-183">By design, these limited roles offer access only tootheir correspondent resources created in hello Azure portal, regardless some can still be deployed in hello classic portal as well (for example: virtual machines).</span></span>





![azure portalında sanal makine Katılımcısı rolüne genel bakış](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-hello-same-directory"></a><span data-ttu-id="f851d-185">GRANT erişim hello bir kullanıcı için bir abonelik düzeyinde aynı dizin</span><span class="sxs-lookup"><span data-stu-id="f851d-185">Grant access at a subscription level for a user in hello same directory</span></span>
<span data-ttu-id="f851d-186">Merhaba işlem akışı aynı tooadding hem erişim toohello rolü verilmeden hello kullanıcı yanı sıra hello Yöneticisi perspektif izni veriliyor hello RBAC rolü bir dış kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="f851d-186">hello process flow is identical tooadding an external user, both from hello admin perspective granting hello RBAC role as well as hello user being granted access toohello role.</span></span> <span data-ttu-id="f851d-187">Merhaba burada oturum açtıktan sonra hello abonelik içindeki tüm hello kaynak kapsamları hello panosunda kullanılabilir olacak şekilde bu davet hello kullanıcının e-posta Davetleri almaz farktır.</span><span class="sxs-lookup"><span data-stu-id="f851d-187">hello difference here is that hello invited user will not receive any email invitations as all hello resource scopes within hello subscription will be available in hello dashboard after signing in.</span></span>

## <a name="assign-rbac-roles-at-hello-resource-group-scope"></a><span data-ttu-id="f851d-188">Merhaba Kaynak Grup kapsamı RBAC rollerini atama</span><span class="sxs-lookup"><span data-stu-id="f851d-188">Assign RBAC roles at hello resource group scope</span></span>
<span data-ttu-id="f851d-189">Bir RBAC rolü atama bir **kaynak grubu** kapsamı hello abonelik düzeyinde, her iki tür kullanıcı - harici veya dahili hello rol atama için benzer bir işlem var (Merhaba parçası aynı dizinde).</span><span class="sxs-lookup"><span data-stu-id="f851d-189">Assigning an RBAC role at a **Resource Group** scope has an identical process for assigning hello role at hello subscription level, for both types of users - either external or internal (part of hello same directory).</span></span> <span data-ttu-id="f851d-190">Merhaba hello RBAC rolü atanmış kullanıcılar olan kullanıcıların, ortamlarında toosee hello kaynak grubu, erişim hello atanmış yalnızca **kaynak grupları** hello Azure Portalı'ndaki simgesini.</span><span class="sxs-lookup"><span data-stu-id="f851d-190">hello users which are assigned hello RBAC role is toosee in their environment only hello resource group they have been assigned access from hello **Resource Groups** icon in hello Azure portal.</span></span>

## <a name="assign-rbac-roles-at-hello-resource-scope"></a><span data-ttu-id="f851d-191">Merhaba kaynak kapsamda RBAC Rolleri Ata</span><span class="sxs-lookup"><span data-stu-id="f851d-191">Assign RBAC roles at hello resource scope</span></span>
<span data-ttu-id="f851d-192">Bir kaynak kapsamda Azure RBAC rolü atama hello rol hello abonelik düzeyinde veya hello kaynak grubu düzeyinde atamak için özdeş bir işlemi varsa, aşağıdaki hello aynı her iki senaryo için iş akışı.</span><span class="sxs-lookup"><span data-stu-id="f851d-192">Assigning an RBAC role at a resource scope in Azure has an identical process for assigning hello role at hello subscription level or at hello resource group level, following hello same workflow for both scenarios.</span></span> <span data-ttu-id="f851d-193">Merhaba RBAC rolü atanan hello kullanıcılar yalnızca, erişim için ya da hello atanmış olduğunu hello öğeleri yeniden görebilirsiniz **tüm kaynakları** sekmesini veya doğrudan kendi Pano.</span><span class="sxs-lookup"><span data-stu-id="f851d-193">Again, hello users which are assigned hello RBAC role can see only hello items that they have been assigned access to, either in hello **All Resources** tab or directly in their dashboard.</span></span>

<span data-ttu-id="f851d-194">RBAC hem kaynak grup kapsamı veya kaynak kapsamı için önemli bir yönü hello kullanıcılar toomake emin toosign bileşenini toohello doğru dizinidir.</span><span class="sxs-lookup"><span data-stu-id="f851d-194">An important aspect for RBAC both at resource group scope or resource scope is for hello users toomake sure toosign-in toohello correct directory.</span></span>





![Azure portalında Directory oturum açma](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a><span data-ttu-id="f851d-196">Bir Azure Active Directory grubu için RBAC Rolleri Ata</span><span class="sxs-lookup"><span data-stu-id="f851d-196">Assign RBAC roles for an Azure Active Directory group</span></span>
<span data-ttu-id="f851d-197">Merhaba üç farklı kapsamlarda yönetme, dağıtma ve hello olmayan atanmış bir kullanıcı olarak çeşitli kaynakları yönetme Azure teklifi hello ayrıcalık RBAC kullanarak tüm hello senaryoları, kişisel abonelik yönetebilme gerekir.</span><span class="sxs-lookup"><span data-stu-id="f851d-197">All hello scenarios using RBAC at hello three different scopes in Azure offer hello privilege of managing, deploying and administering various resources as an assigned user without hello need of managing a personal subscription.</span></span> <span data-ttu-id="f851d-198">Abonelik, kaynak grubu veya kaynak kapsamı için bakılmaksızın hello RBAC rolü atanmış, burada hello kullanıcıların erişimi hello bir Azure aboneliği altında hakkında daha fazla hello atanmış kullanıcılar tarafından oluşturulan tüm hello kaynakları faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="f851d-198">Regardless hello RBAC role is assigned for a subscription, resource group or resource scope, all hello resources created further on by hello assigned users are billed under hello one Azure subscription where hello users have access to.</span></span> <span data-ttu-id="f851d-199">Bu şekilde hello faturalama, tüm Azure aboneliğiniz için yönetici izinlerine sahip kullanıcılar sahip hello kaynakları yöneten bir eksiksiz bir genel bakış hello tüketim, ne olursa olsun.</span><span class="sxs-lookup"><span data-stu-id="f851d-199">This way, hello users who have billing administrator permissions for that entire Azure subscription has a complete overview on hello consumption, regardless who is managing hello resources.</span></span>

<span data-ttu-id="f851d-200">Büyük kuruluşlar için RBAC rolleri uygulanabilir hello hello perspektif hello yönetici kullanıcının dikkate Azure Active Directory grupları ile aynı şekilde toogrant hello ayrıntılı erişim için ekipler veya değil ayrı ayrı her bir kullanıcı için tüm Departmanlar böylece istiyor son derece saat ve yönetim verimli isteğe bağlı olarak düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f851d-200">For larger organizations, RBAC roles can be applied in hello same way for Azure Active Directory groups considering hello perspective that hello admin user wants toogrant hello granular access for teams or entire departments, not individually for each user, thus considering it as an extremely time and management efficient option.</span></span> <span data-ttu-id="f851d-201">tooillustrate Bu örnek, hello **katkıda bulunan** rol hello kiracısında hello abonelik düzeyinde hello gruplarının tooone eklendi.</span><span class="sxs-lookup"><span data-stu-id="f851d-201">tooillustrate this example, hello **Contributor** role has been added tooone of hello groups in hello tenant at hello subscription level.</span></span>





![AAD grupları için RBAC rolü Ekle](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

<span data-ttu-id="f851d-203">Bu grupları sağlanan ve yalnızca Azure Active Directory içinde yönetilen güvenlik gruplarıdır.</span><span class="sxs-lookup"><span data-stu-id="f851d-203">These groups are security groups which are provisioned and managed only within Azure Active Directory.</span></span>

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-powershell"></a><span data-ttu-id="f851d-204">Bir özel RBAC rolü tooopen destek istekleri PowerShell kullanarak oluşturma</span><span class="sxs-lookup"><span data-stu-id="f851d-204">Create a custom RBAC role tooopen support requests using PowerShell</span></span>
<span data-ttu-id="f851d-205">Azure'da kullanılabilen hello yerleşik RBAC rolleri hello kullanılabilir kaynakları hello ortamında göre belirli izin düzeyleri emin olun.</span><span class="sxs-lookup"><span data-stu-id="f851d-205">hello built-in RBAC roles which are available in Azure ensure certain permission levels based on hello available resources in hello environment.</span></span> <span data-ttu-id="f851d-206">Ancak, bu rollerin hiçbiri hello yönetici kullanıcının gereksinimlerinize uygun değilse, hello seçeneği toolimit erişimi daha da olan en fazla özel RBAC rolleri oluşturarak yoktur.</span><span class="sxs-lookup"><span data-stu-id="f851d-206">However, if none of these roles suit hello admin user's needs, there is hello option toolimit access even more by creating custom RBAC roles.</span></span>

<span data-ttu-id="f851d-207">Özel RBAC rolleri oluşturmak için bir yerleşik rol tootake gerekir, düzenlemek ve hello Ortamı'nda içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="f851d-207">Creating custom RBAC roles requires tootake one built-in role, edit it and then import it back in hello environment.</span></span> <span data-ttu-id="f851d-208">Merhaba indirme ve karşıya yükleme hello rolünün PowerShell veya CLI kullanarak yönetilir.</span><span class="sxs-lookup"><span data-stu-id="f851d-208">hello download and upload of hello role are managed using either PowerShell or CLI.</span></span>

<span data-ttu-id="f851d-209">Merhaba abonelik düzeyinde ayrıntılı erişim vermek ve ayrıca destek isteği açma davet hello kullanıcı hello esneklik izin özel bir rol oluşturma önemli toounderstand hello Önkoşullar olur.</span><span class="sxs-lookup"><span data-stu-id="f851d-209">It is important toounderstand hello prerequisites of creating a custom role which can grant granular access at hello subscription level and also allow hello invited user hello flexibility of opening support requests.</span></span>

<span data-ttu-id="f851d-210">Bu örnek hello yerleşik rol için **okuyucu** hello kaynağın tüm kullanıcılara erişim tooview sağlayan değil tooedit bunları kapsamları veya yenilerini oluşturun bırakıldı destek isteği açma tooallow hello kullanıcı hello seçeneği özelleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="f851d-210">For this example hello built-in role **Reader** which allows users access tooview all hello resource scopes but not tooedit them or create new ones has been customized tooallow hello user hello option of opening support requests.</span></span>

<span data-ttu-id="f851d-211">Merhaba verme işleminin ilk eylemin Hello **okuyucu** PowerShell'de tamamlandı rol gereksinimlerini toobe yönetici olarak yükseltilmiş izinlerle çalıştı.</span><span class="sxs-lookup"><span data-stu-id="f851d-211">hello first action of exporting hello **Reader** role needs toobe completed in PowerShell ran with elevated permissions as administrator.</span></span>

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![Okuyucu RBAC rolü için PowerShell ekran görüntüsü](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

<span data-ttu-id="f851d-213">Daha sonra tooextract hello JSON şablonunu hello rolünün gerekir.</span><span class="sxs-lookup"><span data-stu-id="f851d-213">Then you need tooextract hello JSON template of hello role.</span></span>





![Özel okuyucu RBAC rolü için JSON şablonunu](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

<span data-ttu-id="f851d-215">Tipik bir RBAC rolü üç ana bölüm dışında oluşan **Eylemler**, **NotActions** ve **AssignableScopes**.</span><span class="sxs-lookup"><span data-stu-id="f851d-215">A typical RBAC role is composed out of three main sections, **Actions**, **NotActions** and **AssignableScopes**.</span></span>

<span data-ttu-id="f851d-216">Merhaba, **eylem** bölümde listelenen tüm bu rol için izin verilen işlemler hello.</span><span class="sxs-lookup"><span data-stu-id="f851d-216">In hello **Action** section are listed all hello permitted operations for this role.</span></span> <span data-ttu-id="f851d-217">Bu, her eylemin kaynak sağlayıcısından atandığı önemli toounderstand olur.</span><span class="sxs-lookup"><span data-stu-id="f851d-217">It's important toounderstand that each action is assigned from a resource provider.</span></span> <span data-ttu-id="f851d-218">Bu durumda, destek biletlerini hello oluşturmak için **Microsoft.Support** kaynak sağlayıcısı listelenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="f851d-218">In this case, for creating support tickets hello **Microsoft.Support** resource provider must be listed.</span></span>

<span data-ttu-id="f851d-219">toobe mümkün toosee tüm kaynak sağlayıcıları kullanılabilir ve aboneliğinizde kayıtlı Merhaba, PowerShell'i kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f851d-219">toobe able toosee all hello resource providers available and registered in your subscription, you can use PowerShell.</span></span>
```
Get-AzureRMResourceProvider

```
<span data-ttu-id="f851d-220">Ayrıca, tüm hello kullanılabilir PowerShell cmdlet'leri toomanage hello kaynak sağlayıcıları için hello kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f851d-220">Additionally, you can check for hello all hello available PowerShell cmdlets toomanage hello resource providers.</span></span>
    <span data-ttu-id="f851d-221">![Kaynak sağlayıcısı yönetimi için PowerShell ekran görüntüsü](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span><span class="sxs-lookup"><span data-stu-id="f851d-221">![PowerShell screenshot for resource provider management](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span></span>

<span data-ttu-id="f851d-222">Tüm eylemler için belirli bir RBAC rolü olan kaynak sağlayıcıları hello bölümü altında listelenen hello toorestrict **NotActions**.</span><span class="sxs-lookup"><span data-stu-id="f851d-222">toorestrict all hello actions for a particular RBAC role, resource providers are listed under hello section **NotActions**.</span></span>
<span data-ttu-id="f851d-223">Son olarak, bu hello RBAC rolü hello açık abonelik kullanıldığı kimlikleri içeriyor zorunludur.</span><span class="sxs-lookup"><span data-stu-id="f851d-223">Last, it's mandatory that hello RBAC role contains hello explicit subscription IDs where it is used.</span></span> <span data-ttu-id="f851d-224">Merhaba abonelik kimlikleri hello altında listelenen **AssignableScopes**, aksi takdirde, tooimport hello rol aboneliğinizde izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="f851d-224">hello subscription IDs are listed under hello **AssignableScopes**, otherwise you will not be allowed tooimport hello role in your subscription.</span></span>

<span data-ttu-id="f851d-225">Oluşturma ve hello RBAC rolü özelleştirme sonra toobe alınan geri hello ortamın gerekir.</span><span class="sxs-lookup"><span data-stu-id="f851d-225">After creating and customizing hello RBAC role, it needs toobe imported back hello environment.</span></span>

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

<span data-ttu-id="f851d-226">Bu örnekte, hello özel bu RBAC rolü için "Merhaba abonelik yanı sıra tooopen destek istekleri hello kullanıcı tooview her şeyi sağlayan okuyucu destek biletleri erişim düzeyi" adıdır.</span><span class="sxs-lookup"><span data-stu-id="f851d-226">In this example, hello custom name for this RBAC role is "Reader support tickets access level" allowing hello user tooview everything in hello subscription and also tooopen support requests.</span></span>

> [!NOTE]
> <span data-ttu-id="f851d-227">Merhaba destek isteği açma hello eylemi izin verme yalnızca iki yerleşik RBAC rolleridir **sahibi** ve **katkıda bulunan**.</span><span class="sxs-lookup"><span data-stu-id="f851d-227">hello only two built-in RBAC roles allowing hello action of opening of support requests are **Owner** and **Contributor**.</span></span> <span data-ttu-id="f851d-228">Tüm destek isteklerini bir Azure aboneliğine yönelik temel alınarak oluşturulur çünkü bir kullanıcı toobe mümkün tooopen destek istekleri için kendisinin RBAC rolü yalnızca kapsamda hello abonelik, atanmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f851d-228">For a user toobe able tooopen support requests, he must be assigned an RBAC role only at hello subscription scope, because all support requests are created based on an Azure subscription.</span></span>

<span data-ttu-id="f851d-229">Bu yeni özel rolü hello tooan kullanıcıdan atanan aynı dizin.</span><span class="sxs-lookup"><span data-stu-id="f851d-229">This new custom role has been assigned tooan user from hello same directory.</span></span>





![hello Azure portal içeri özel RBAC rolü ekran görüntüsü](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![Merhaba, içeri aktarılan özel RBAC rolü toouser atama ekran aynı dizinde](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![Özel alınan RBAC rolü izinlerini ekran görüntüsü](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

<span data-ttu-id="f851d-233">Merhaba örneği daha fazla gibi ayrıntılı tooemphasize hello sınırları bu özel RBAC rolü bırakıldı:</span><span class="sxs-lookup"><span data-stu-id="f851d-233">hello example has been further detailed tooemphasize hello limits of this custom RBAC role as follows:</span></span>
* <span data-ttu-id="f851d-234">Yeni destek istekleri oluşturabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f851d-234">Can create new support requests</span></span>
* <span data-ttu-id="f851d-235">Yeni kaynak kapsamlar oluşturulamıyor (örneğin: sanal makine)</span><span class="sxs-lookup"><span data-stu-id="f851d-235">Can't create new resource scopes (for example: virtual machine)</span></span>
* <span data-ttu-id="f851d-236">Yeni kaynak grupları oluşturulamıyor</span><span class="sxs-lookup"><span data-stu-id="f851d-236">Can't create new resource groups</span></span>





![Özel RBAC rolü destek istekleri oluşturma ekran görüntüsü](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![ekran görüntüsü özel RBAC rolü erişilemiyor toocreate VM'ler](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![ekran görüntüsü özel RBAC rolü erişilemiyor toocreate yeni RGs](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-azure-cli"></a><span data-ttu-id="f851d-240">Bir özel RBAC rolü tooopen destek istekleri Azure CLI kullanarak oluşturma</span><span class="sxs-lookup"><span data-stu-id="f851d-240">Create a custom RBAC role tooopen support requests using Azure CLI</span></span>
<span data-ttu-id="f851d-241">Mac'te ve erişim tooPowerShell kalmadan, Azure CLI hello yolu toogo çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="f851d-241">Running on a Mac and without having access tooPowerShell, Azure CLI is hello way toogo.</span></span>

<span data-ttu-id="f851d-242">aynı, CLI kullanarak hello rol bir JSON şablonu, ancak bunu karşıdan yüklenemediğini hello tek özel durum ile Merhaba CLI görüntülenebilir hello Hello adımları toocreate özel bir rol var.</span><span class="sxs-lookup"><span data-stu-id="f851d-242">hello steps toocreate a custom role are hello same, with hello sole exception that using CLI hello role can't be downloaded in a JSON template, but it can be viewed in hello CLI.</span></span>

<span data-ttu-id="f851d-243">Bu örnek için ı hello yerleşik rolü seçtiniz **yedekleme okuyucu**.</span><span class="sxs-lookup"><span data-stu-id="f851d-243">For this example I have chosen hello built-in role of **Backup Reader**.</span></span>

```

azure role show "backup reader" --json

```





![CLI ekran görüntüsü yedekleme okuyucu rolüne Göster](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

<span data-ttu-id="f851d-245">Visual Studio'da Hello rol bir JSON şablonu hello proprieties kopyaladıktan sonra düzenleme hello **Microsoft.Support** kaynak sağlayıcısı hello eklendi **Eylemler** bu kullanıcı açabileceği bölümler toobe hello yedekleme kasalarını için bir okuyucu devam ederken destek istekleri.</span><span class="sxs-lookup"><span data-stu-id="f851d-245">Editing hello role in Visual Studio after copying hello proprieties in a JSON template, hello **Microsoft.Support** resource provider has been added in hello **Actions** sections so that this user can open support requests while continuing toobe a reader for hello backup vaults.</span></span> <span data-ttu-id="f851d-246">Yeniden bu rolü hello nerede kullanılacak gerekli tooadd hello abonelik kimliği olan **AssignableScopes** bölümü.</span><span class="sxs-lookup"><span data-stu-id="f851d-246">Again it is necessary tooadd hello subscription ID where this role will be used in hello **AssignableScopes** section.</span></span>

```

azure role create --inputfile <path>

```





![Özel RBAC rolü alma CLI ekran görüntüsü](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

<span data-ttu-id="f851d-248">Merhaba yeni rol hello Azure portalında kullanılabilir ve hello atamasını işlemi olduğundan hello aynı hello önceki örneklerde olduğu gibi.</span><span class="sxs-lookup"><span data-stu-id="f851d-248">hello new role is now available in hello Azure portal and hello assignation process is hello same as in hello previous examples.</span></span>





![CLI 1.0 kullanılarak oluşturulan özel RBAC rolü Azure portal ekran görüntüsü](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

<span data-ttu-id="f851d-250">İtibariyle Hello son yapı 2017, hello Azure bulut Kabuk genel kullanıma açıktır.</span><span class="sxs-lookup"><span data-stu-id="f851d-250">As of hello latest Build 2017, hello Azure Cloud Shell is generally available.</span></span> <span data-ttu-id="f851d-251">Azure bulut Kabuk tamamlama tooIDE ve hello Azure Portal ' dir.</span><span class="sxs-lookup"><span data-stu-id="f851d-251">Azure Cloud Shell is a complement tooIDE and hello Azure Portal.</span></span> <span data-ttu-id="f851d-252">Bu hizmeti ile kimlik doğrulaması ve Azure içinde barındırılan ve tarayıcı tabanlı bir kabuk alın ve makinenize yüklü CLI yerine kullanın.</span><span class="sxs-lookup"><span data-stu-id="f851d-252">With this service, you get a browser-based shell that is authenticated and hosted within Azure and you can use it instead of CLI installed on your machine.</span></span>





![Azure bulut Kabuğu](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)
