---
title: "Grupları kullanma erişim yönetimi için'sonraki adımlar | Microsoft Docs"
description: "Nasıl Gelişmiş-için kullanıcının güvenlik grupları ve bu grupların bir kaynağa erişimi yönetmek için nasıl kullanılacağını yönetme."
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
ms.openlocfilehash: 82fbeb379e90add09f7c569111053f6e9b1bc9c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="managing-owners-for-a-group"></a><span data-ttu-id="22b83-103">Bir grubun sahiplerini yönetme</span><span class="sxs-lookup"><span data-stu-id="22b83-103">Managing owners for a group</span></span>
<span data-ttu-id="22b83-104">Kaynak sahibi Azure AD grubundaki bir kaynağa erişim atandıktan sonra Grup üyeliğini Grup sahibi tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="22b83-104">Once a resource owner has assigned access to a resource to an Azure AD group, the membership of the group is managed by the group owner.</span></span> <span data-ttu-id="22b83-105">Kaynak sahibi etkili bir şekilde kaynak grubunun sahibi için kullanıcılar atama izni verilir.</span><span class="sxs-lookup"><span data-stu-id="22b83-105">The resource owner effectively delegates the permission to assign users to the resource to the owner of the group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="22b83-106">Microsoft, Azure AD’yi bu makalede bahsedilen Klasik Azure Portalı yerine Azure portalındaki [Azure AD yönetim merkezini](https://aad.portal.azure.com) kullanarak yönetmenizi öneriyor.</span><span class="sxs-lookup"><span data-stu-id="22b83-106">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 

## <a name="assigning-group-ownership"></a><span data-ttu-id="22b83-107">Grup sahipliğini atama</span><span class="sxs-lookup"><span data-stu-id="22b83-107">Assigning group ownership</span></span>
<span data-ttu-id="22b83-108">**Bir sahip bir gruba eklemek için**</span><span class="sxs-lookup"><span data-stu-id="22b83-108">**To add an owner to a group**</span></span>

1. <span data-ttu-id="22b83-109">İçinde [Klasik Azure portalı](https://manage.windowsazure.com)seçin **Active Directory**ve ardından, kuruluşunuzun dizininde açın.</span><span class="sxs-lookup"><span data-stu-id="22b83-109">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="22b83-110">Seçin **grupları** sekmesini ve ardından sahiplerine eklemek istediğiniz grubu açın.</span><span class="sxs-lookup"><span data-stu-id="22b83-110">Select the **Groups** tab, and then open the group that you want to add owners to.</span></span>
3. <span data-ttu-id="22b83-111">Seçin **sahipleri eklemek**.</span><span class="sxs-lookup"><span data-stu-id="22b83-111">Select **Add Owners**.</span></span>
4. <span data-ttu-id="22b83-112">Üzerinde **sahipleri eklemek** sayfasında, bu grubun sahibi olarak ekleyin ve bu ad eklendiğinden emin olun istediğiniz kullanıcıyı seçin **seçili** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="22b83-112">On the **Add owners** page, select the user that you want to add as the owner of this group, and make sure this name is added to the **Selected** pane.</span></span>

<span data-ttu-id="22b83-113">**Bir sahip bir gruptan kaldırmak için**</span><span class="sxs-lookup"><span data-stu-id="22b83-113">**To remove an owner from a group**</span></span>

1. <span data-ttu-id="22b83-114">İçinde [Klasik Azure portalı](https://manage.windowsazure.com)seçin **Active Directory**ve ardından, kuruluşunuzun dizininde açın.</span><span class="sxs-lookup"><span data-stu-id="22b83-114">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="22b83-115">Seçin **grupları** sekmesini ve ardından bir sahibinden kaldırmak istediğiniz grubu açın.</span><span class="sxs-lookup"><span data-stu-id="22b83-115">Select the **Groups** tab, and then open the group that you want to remove an owner from.</span></span>
3. <span data-ttu-id="22b83-116">Seçin **sahipleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="22b83-116">Select the **Owners** tab.</span></span>
4. <span data-ttu-id="22b83-117">Bu gruptan kaldırın ve ardından istediğiniz sahibi seçin **kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="22b83-117">Select the owner that you want to remove from this group, and then select **Remove**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="22b83-118">Ek bilgiler</span><span class="sxs-lookup"><span data-stu-id="22b83-118">Additional information</span></span>
<span data-ttu-id="22b83-119">Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="22b83-119">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="22b83-120">Azure Active Directory grupları ile kaynaklara erişimi yönetme</span><span class="sxs-lookup"><span data-stu-id="22b83-120">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="22b83-121">Grup ayarlarını yapılandırmak için Azure Active Directory cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="22b83-121">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="22b83-122">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="22b83-122">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="22b83-123">Azure Active Directory nedir?</span><span class="sxs-lookup"><span data-stu-id="22b83-123">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="22b83-124">Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="22b83-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
