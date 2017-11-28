---
title: "aaaNext adımları erişim yönetimi için grupları kullanma | Microsoft Docs"
description: "Nasıl Gelişmiş-için kullanıcının güvenlik gruplarını yönetme ve nasıl toouse bu grupları toomanage erişim tooa kaynak."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 44350a3c-8ea1-4da1-aaac-7fc53933dd21
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4fd55f893290fac3551a130f29bd12709cf551e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-owners-for-a-group"></a><span data-ttu-id="224d5-103">Bir grubun sahiplerini yönetme</span><span class="sxs-lookup"><span data-stu-id="224d5-103">Managing owners for a group</span></span>
<span data-ttu-id="224d5-104">Kaynak sahibine erişim tooa kaynak tooan Azure AD grubu atandıktan sonra hello hello grup üyeliğini hello Grup sahibi tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="224d5-104">Once a resource owner has assigned access tooa resource tooan Azure AD group, hello membership of hello group is managed by hello group owner.</span></span> <span data-ttu-id="224d5-105">Merhaba kaynak sahibi etkili bir şekilde hello izin tooassign kullanıcılar toohello kaynak toohello hello grubun sahibi atar.</span><span class="sxs-lookup"><span data-stu-id="224d5-105">hello resource owner effectively delegates hello permission tooassign users toohello resource toohello owner of hello group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="224d5-106">Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="224d5-106">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 

## <a name="assigning-group-ownership"></a><span data-ttu-id="224d5-107">Grup sahipliğini atama</span><span class="sxs-lookup"><span data-stu-id="224d5-107">Assigning group ownership</span></span>
<span data-ttu-id="224d5-108">**tooadd bir sahibi tooa grubu**</span><span class="sxs-lookup"><span data-stu-id="224d5-108">**tooadd an owner tooa group**</span></span>

1. <span data-ttu-id="224d5-109">Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com)seçin **Active Directory**ve ardından, kuruluşunuzun dizininde açın.</span><span class="sxs-lookup"><span data-stu-id="224d5-109">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="224d5-110">Select hello **grupları** sekme ve tooadd sahiplerine istediğiniz sonra açık hello grup.</span><span class="sxs-lookup"><span data-stu-id="224d5-110">Select hello **Groups** tab, and then open hello group that you want tooadd owners to.</span></span>
3. <span data-ttu-id="224d5-111">Seçin **sahipleri eklemek**.</span><span class="sxs-lookup"><span data-stu-id="224d5-111">Select **Add Owners**.</span></span>
4. <span data-ttu-id="224d5-112">Merhaba üzerinde **sahipleri eklemek** sayfası, bu grubun hello sahibi olarak tooadd istediğiniz ve bu ad, toohello eklendiğinden emin olun select hello kullanıcı **seçili** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="224d5-112">On hello **Add owners** page, select hello user that you want tooadd as hello owner of this group, and make sure this name is added toohello **Selected** pane.</span></span>

<span data-ttu-id="224d5-113">**tooremove bir gruptan sahibi**</span><span class="sxs-lookup"><span data-stu-id="224d5-113">**tooremove an owner from a group**</span></span>

1. <span data-ttu-id="224d5-114">Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com)seçin **Active Directory**ve ardından, kuruluşunuzun dizininde açın.</span><span class="sxs-lookup"><span data-stu-id="224d5-114">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="224d5-115">Select hello **grupları** sekmesini ve ardından açık hello Grup bir sahibinden tooremove istiyor.</span><span class="sxs-lookup"><span data-stu-id="224d5-115">Select hello **Groups** tab, and then open hello group that you want tooremove an owner from.</span></span>
3. <span data-ttu-id="224d5-116">Select hello **sahipleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="224d5-116">Select hello **Owners** tab.</span></span>
4. <span data-ttu-id="224d5-117">Bu gruptan tooremove istediğiniz ve ardından select hello sahibi **kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="224d5-117">Select hello owner that you want tooremove from this group, and then select **Remove**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="224d5-118">Ek bilgiler</span><span class="sxs-lookup"><span data-stu-id="224d5-118">Additional information</span></span>
<span data-ttu-id="224d5-119">Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="224d5-119">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="224d5-120">Azure Active Directory grupları ile erişim tooresources yönetme</span><span class="sxs-lookup"><span data-stu-id="224d5-120">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="224d5-121">Grup ayarlarını yapılandırmak için Azure Active Directory cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="224d5-121">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="224d5-122">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="224d5-122">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="224d5-123">Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="224d5-123">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="224d5-124">Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="224d5-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
