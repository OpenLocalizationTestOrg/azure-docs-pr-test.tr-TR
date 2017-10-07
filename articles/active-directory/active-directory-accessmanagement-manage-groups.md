---
title: "Azure Active Directory'de aaaManaging gruplarını | Microsoft Docs"
description: "Nasıl toocreate ve grupları toomanage Azure yönetmek kullanıcıları Azure Active Directory kullanarak."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d1f5451c-3807-423c-8bac-2822d27b893f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 9bee224655639740b3dd99983892b30c3c537aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-groups-in-azure-active-directory"></a><span data-ttu-id="5099a-103">Azure Active Directory içinde grupları yönetme</span><span class="sxs-lookup"><span data-stu-id="5099a-103">Managing groups in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5099a-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="5099a-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="5099a-105">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="5099a-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="5099a-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5099a-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="5099a-107">Azure Active Directory (Azure AD) kullanıcı yönetimi hello özelliklerini hello özelliği toocreate gruplarını biridir.</span><span class="sxs-lookup"><span data-stu-id="5099a-107">One of hello features of Azure Active Directory (Azure AD) user management is hello ability toocreate groups of users.</span></span> <span data-ttu-id="5099a-108">Lisans veya izinleri tooa sayısı, kullanıcı aynı anda atama gibi bir grup tooperform yönetim görevleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="5099a-108">You use a group tooperform management tasks such as assigning licenses or permissions tooa number of users at once.</span></span> <span data-ttu-id="5099a-109">Grupları tooassign erişim izni de kullanabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="5099a-109">You can also use groups tooassign access permission to</span></span>

* <span data-ttu-id="5099a-110">Merhaba directory içindeki nesneleri gibi kaynakları</span><span class="sxs-lookup"><span data-stu-id="5099a-110">Resources such as objects in hello directory</span></span>
* <span data-ttu-id="5099a-111">SaaS uygulamaları, Azure Hizmetleri, SharePoint siteleri veya şirket içi kaynaklar gibi kaynakları dış toohello dizini</span><span class="sxs-lookup"><span data-stu-id="5099a-111">Resources external toohello directory such as SaaS applications, Azure services, SharePoint sites, or on-premises resources</span></span>

<span data-ttu-id="5099a-112">Ayrıca, bir kaynak sahibi başka birisi tarafından sahip olunan erişim tooa kaynak tooan Azure AD grubuna atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5099a-112">In addition, a resource owner can also assign access tooa resource tooan Azure AD group owned by someone else.</span></span> <span data-ttu-id="5099a-113">Bu atama hello üyeleri bu Grup erişim toohello kaynağın verir.</span><span class="sxs-lookup"><span data-stu-id="5099a-113">This assignment grants hello members of that group access toohello resource.</span></span> <span data-ttu-id="5099a-114">Ardından, hello grubunun hello sahibi hello grubu üyeliği yönetir.</span><span class="sxs-lookup"><span data-stu-id="5099a-114">Then, hello owner of hello group manages membership in hello group.</span></span> <span data-ttu-id="5099a-115">Etkili bir şekilde hello kaynak sahibi temsilciler toohello hello Grup hello izin tooassign kullanıcılar tootheir kaynağın sahibi.</span><span class="sxs-lookup"><span data-stu-id="5099a-115">Effectively, hello resource owner delegates toohello owner of hello group hello permission tooassign users tootheir resource.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5099a-116">Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="5099a-116">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="5099a-117">Toomanage hello Azure AD Yönetim Merkezi'nde nasıl gruplar için bkz: [bir grup oluşturun ve Azure Active Directory'de üye ekleme](active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5099a-117">For how toomanage groups in hello Azure AD admin center, see [Create a group and add members in Azure Active Directory](active-directory-groups-create-azure-portal.md).</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="5099a-118">Nasıl grup oluşturulur?</span><span class="sxs-lookup"><span data-stu-id="5099a-118">How do I create a group?</span></span>
<span data-ttu-id="5099a-119">Kuruluşunuzun abone olduğu hello Hizmetleri toowhich bağlı olarak hello aşağıdakilerden birini kullanarak bir grup oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5099a-119">Depending on hello services toowhich your organization has subscribed, you can create a group using one of hello following:</span></span>

* <span data-ttu-id="5099a-120">Merhaba Klasik Azure portalı</span><span class="sxs-lookup"><span data-stu-id="5099a-120">hello Azure classic portal</span></span>
* <span data-ttu-id="5099a-121">Merhaba Office 365 hesap portalı</span><span class="sxs-lookup"><span data-stu-id="5099a-121">hello Office 365 account portal</span></span>
* <span data-ttu-id="5099a-122">Merhaba Windows Intune hesap portalı</span><span class="sxs-lookup"><span data-stu-id="5099a-122">hello Windows Intune account portal</span></span>

<span data-ttu-id="5099a-123">Görevleri hello Klasik Azure portalında gerçekleştirilen gibi açıklar.</span><span class="sxs-lookup"><span data-stu-id="5099a-123">We'll describe tasks as performed in hello Azure classic portal.</span></span> <span data-ttu-id="5099a-124">Azure AD dizininizi Azure olmayan Portal toomanage kullanma hakkında daha fazla bilgi için bkz: [Azure AD dizininizi yönetme](active-directory-administer.md).</span><span class="sxs-lookup"><span data-stu-id="5099a-124">For more information about using non-Azure portals toomanage your Azure AD directory, see [Administering your Azure AD directory](active-directory-administer.md).</span></span>

1. <span data-ttu-id="5099a-125">Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com)seçin **Active Directory**ve ardından, kuruluşunuz için hello hello dizinin adını seçin.</span><span class="sxs-lookup"><span data-stu-id="5099a-125">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="5099a-126">Select hello **grupları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5099a-126">Select hello **Groups** tab.</span></span>
3. <span data-ttu-id="5099a-127">**Grup Ekle**'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="5099a-127">Select **Add Group**.</span></span>
4. <span data-ttu-id="5099a-128">Merhaba, **Grup Ekle** penceresinde hello adı belirtin ve hello bir grubun açıklaması.</span><span class="sxs-lookup"><span data-stu-id="5099a-128">In hello **Add Group** window, specify hello name and hello description of a group.</span></span>

## <a name="how-do-i-add-or-remove-individual-users-in-a-security-group"></a><span data-ttu-id="5099a-129">Güvenlik grubuna bireysel kullanıcıları nasıl eklerim veya kaldırırım?</span><span class="sxs-lookup"><span data-stu-id="5099a-129">How do I add or remove individual users in a security group?</span></span>
<span data-ttu-id="5099a-130">**tooadd tek tek kullanıcı tooa grubu**</span><span class="sxs-lookup"><span data-stu-id="5099a-130">**tooadd an individual user tooa group**</span></span>

1. <span data-ttu-id="5099a-131">Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com)seçin **Active Directory**ve ardından, kuruluşunuz için hello hello dizinin adını seçin.</span><span class="sxs-lookup"><span data-stu-id="5099a-131">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="5099a-132">Select hello **grupları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5099a-132">Select hello **Groups** tab.</span></span>
3. <span data-ttu-id="5099a-133">Merhaba Grup toowhich tooadd üyelerinin istediğiniz açın.</span><span class="sxs-lookup"><span data-stu-id="5099a-133">Open hello group toowhich you want tooadd members.</span></span> <span data-ttu-id="5099a-134">Açık hello **üyeleri** hello sekmesinde seçtiyseniz grubu, zaten görüntüleme.</span><span class="sxs-lookup"><span data-stu-id="5099a-134">Open hello **Members** tab of hello selected group if it not already displaying.</span></span>
4. <span data-ttu-id="5099a-135">**Add Members (Üye Ekle)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="5099a-135">Select **Add Members**.</span></span>
5. <span data-ttu-id="5099a-136">Merhaba üzerinde **Add Members** sayfası, hello kullanıcı veya bu grubun bir üyesi olarak tooadd istediğiniz bir grup seçin hello adı.</span><span class="sxs-lookup"><span data-stu-id="5099a-136">On hello **Add Members** page, select hello name of hello user or a group that you want tooadd as a member of this group.</span></span> <span data-ttu-id="5099a-137">Bu ad toohello eklendiğinden emin olun **seçili** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="5099a-137">Make sure that this name is added toohello **Selected** pane.</span></span>

<span data-ttu-id="5099a-138">**tooremove tek bir kullanıcı bir gruptan**</span><span class="sxs-lookup"><span data-stu-id="5099a-138">**tooremove an individual user from a group**</span></span>

1. <span data-ttu-id="5099a-139">Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com)seçin **Active Directory**ve ardından, kuruluşunuz için hello hello dizinin adını seçin.</span><span class="sxs-lookup"><span data-stu-id="5099a-139">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="5099a-140">Select hello **grupları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5099a-140">Select hello **Groups** tab.</span></span>
3. <span data-ttu-id="5099a-141">Tooremove üyelerinin istediğiniz hello grubu açın.</span><span class="sxs-lookup"><span data-stu-id="5099a-141">Open hello group from which you want tooremove members.</span></span>
4. <span data-ttu-id="5099a-142">Select hello **üyeleri** sekmesi, bu gruptan tooremove istediğiniz ve ardından hello üyenin adını seçin hello **kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="5099a-142">Select hello **Members** tab, select hello name of hello member that you want tooremove from this group, and then click **Remove**.</span></span>
5. <span data-ttu-id="5099a-143">Merhaba isteminde hello gruptan bu üye tooremove istediğinizi onaylayın.</span><span class="sxs-lookup"><span data-stu-id="5099a-143">Confirm at hello prompt that you want tooremove this member from hello group.</span></span>

## <a name="how-can-i-manage-hello-membership-of-a-group-dynamically"></a><span data-ttu-id="5099a-144">Merhaba bir grubun üyeliğini dinamik olarak nasıl yönetebilirim?</span><span class="sxs-lookup"><span data-stu-id="5099a-144">How can I manage hello membership of a group dynamically?</span></span>
<span data-ttu-id="5099a-145">Azure AD içinde hangi kullanıcıların toobe hello grubunun üyesi olan bir basit kural toodetermine kolayca ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5099a-145">In Azure AD, you can very easily set up a simple rule toodetermine which users are toobe members of hello group.</span></span> <span data-ttu-id="5099a-146">Basit bir kural yalnızca tek bir karşılaştırma yapan kuraldır.</span><span class="sxs-lookup"><span data-stu-id="5099a-146">A simple rule is one that makes only a single comparison.</span></span> <span data-ttu-id="5099a-147">Örneğin, bir grup tooa SaaS uygulamasına atandıysa, iş unvanına "Satış Temsilcisi" sahip olan bir kural tooadd kullanıcıları ayarlayabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="5099a-147">For example, if a group is assigned tooa SaaS application, you can set up a rule tooadd users who have a job title of "Sales Rep."</span></span> <span data-ttu-id="5099a-148">Bu kural, dizininizdeki bu iş unvanına sahip toothis SaaS uygulama tooall kullanıcılar daha sonra erişim verir.</span><span class="sxs-lookup"><span data-stu-id="5099a-148">This rule then grants access toothis SaaS application tooall users with that job title in your directory.</span></span>

<span data-ttu-id="5099a-149">Herhangi bir kullanıcı değişiklik özniteliklerini hello sistem değerlendirildiğinde hello öznitelik değişikliği hello kullanıcının herhangi bir grup tetikleyecek varsa bir dizin toosee tüm dinamik Grup kurallarında ekler veya kaldırır.</span><span class="sxs-lookup"><span data-stu-id="5099a-149">When any attributes of a user change, hello system evaluates all dynamic group rules in a directory toosee if hello attribute change of hello user would trigger any group adds or removes.</span></span> <span data-ttu-id="5099a-150">Bir kullanıcı bir grupta kuralı uymazsa, bunlar üye toothat grup olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="5099a-150">If a user satisfies a rule on a group, they are added as a member toothat group.</span></span> <span data-ttu-id="5099a-151">Bunlar artık üyesi olan bir grup hello kuralı karşılamak varsa, bunlar bir üye olarak, bu gruptan kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="5099a-151">If they no longer satisfy hello rule of a group they are a member of, they are removed as a members from that group.</span></span>

> [!NOTE]
> <span data-ttu-id="5099a-152">Güvenlik gruplarında veya Office 365 gruplarında dinamik üyelik için bir kural ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5099a-152">You can set up a rule for dynamic membership on security groups or Office 365 groups.</span></span> <span data-ttu-id="5099a-153">İç içe geçmiş grup üyelikleri grup tabanlı atama tooapplications için şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="5099a-153">Nested group memberships aren't currently supported for group-based assignment tooapplications.</span></span>
>
> <span data-ttu-id="5099a-154">Atanmış bir Azure AD Premium lisansı toobe gruplara yönelik dinamik üyelikler gerektirir</span><span class="sxs-lookup"><span data-stu-id="5099a-154">Dynamic memberships for groups require an Azure AD Premium license toobe assigned to</span></span>
>
> * <span data-ttu-id="5099a-155">Merhaba grupta kuralı yöneten hello Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="5099a-155">hello administrator who manages hello rule on a group</span></span>
> * <span data-ttu-id="5099a-156">Merhaba grubunun tüm üyeleri</span><span class="sxs-lookup"><span data-stu-id="5099a-156">All members of hello group</span></span>
>
>

<span data-ttu-id="5099a-157">**bir grup için tooenable dinamik üyeliği**</span><span class="sxs-lookup"><span data-stu-id="5099a-157">**tooenable dynamic membership for a group**</span></span>

1. <span data-ttu-id="5099a-158">Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com)seçin **Active Directory**ve ardından, kuruluşunuz için hello hello dizinin adını seçin.</span><span class="sxs-lookup"><span data-stu-id="5099a-158">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="5099a-159">Select hello **grupları** sekme ve açık hello Grup tooedit istiyor.</span><span class="sxs-lookup"><span data-stu-id="5099a-159">Select hello **Groups** tab, and open hello group you want tooedit.</span></span>
3. <span data-ttu-id="5099a-160">Select hello **yapılandırma** sekmesini tıklatın ve ardından **dinamik üyelikleri etkinleştir** çok**Evet**.</span><span class="sxs-lookup"><span data-stu-id="5099a-160">Select hello **Configure** tab, and then set **Enable Dynamic Memberships** too**Yes**.</span></span>
4. <span data-ttu-id="5099a-161">Merhaba Grup toocontrol için tek bir basit kural ayarlayın bu grubun işlevleri için dinamik üyeliği.</span><span class="sxs-lookup"><span data-stu-id="5099a-161">Set up a simple single rule for hello group toocontrol how dynamic membership for this group functions.</span></span> <span data-ttu-id="5099a-162">Hello emin olun **kullanıcıları ekleme yeri** seçeneği seçilir ve ardından kullanıcı özelliği (örneğin, departman, iş unvanı, vb.), hello listeden seçin</span><span class="sxs-lookup"><span data-stu-id="5099a-162">Make sure hello **Add users where** option is selected, and then select a user property from hello list (for example, department, jobTitle, etc.),</span></span>
5. <span data-ttu-id="5099a-163">Ardından, bir koşul (Eşit Değildir, Eşittir, İle Başlamaz, İle Başlar, İçermez, İçerir, Eşleşmez, Eşleşir) seçin.</span><span class="sxs-lookup"><span data-stu-id="5099a-163">Next, select a condition (Not Equals, Equals, Not Starts With, Starts With, Not Contains, Contains, Not Match, Match).</span></span>
6. <span data-ttu-id="5099a-164">Seçili hello kullanıcı özelliği için bir karşılaştırma değer belirtin.</span><span class="sxs-lookup"><span data-stu-id="5099a-164">Specify a comparison value for hello selected user property.</span></span>

<span data-ttu-id="5099a-165">konusunda toolearn toocreate *Gelişmiş* kuralları (birden çok karşılaştırma içeren kurallar) dinamik grup üyeliği için bkz: [öznitelikleri toocreate kullanarak gelişmiş kurallar](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="5099a-165">toolearn about how toocreate *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes toocreate advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

## <a name="additional-information"></a><span data-ttu-id="5099a-166">Ek bilgiler</span><span class="sxs-lookup"><span data-stu-id="5099a-166">Additional information</span></span>
<span data-ttu-id="5099a-167">Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="5099a-167">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="5099a-168">Azure Active Directory grupları ile erişim tooresources yönetme</span><span class="sxs-lookup"><span data-stu-id="5099a-168">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="5099a-169">Grup ayarlarını yapılandırmak için Azure Active Directory cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="5099a-169">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="5099a-170">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="5099a-170">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="5099a-171">Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="5099a-171">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="5099a-172">Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="5099a-172">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
