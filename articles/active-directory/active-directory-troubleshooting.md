---
title: "Sorun giderme: 'Active Directory' öğesi eksik veya kullanılabilir değil | Microsoft Docs"
description: "Active Directory menü öğesi hello Azure Yönetim Portalı görünmüyor olduğunda hangi toodo."
services: active-directory
documentationcenter: na
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 3383020d-6397-43ea-b7aa-c6a9d6a1e3df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.openlocfilehash: d7355a4e39141f0b09272dc5615c309b23c8c70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a><span data-ttu-id="62341-103">Sorun giderme: 'Active Directory' öğesi eksik veya kullanılabilir değil</span><span class="sxs-lookup"><span data-stu-id="62341-103">Troubleshooting: 'Active Directory' item is missing or not available</span></span>
<span data-ttu-id="62341-104">Azure Active Directory özelliklerini ve hizmetlerini kullanma hello yönergeleri çoğunu ile başlayan "toohello Azure yönetim portalına gidin ve tıklayın **Active Directory**."</span><span class="sxs-lookup"><span data-stu-id="62341-104">Many of hello instructions for using Azure Active Directory features and services begin with "Go toohello Azure Management Portal and click **Active Directory**."</span></span> <span data-ttu-id="62341-105">Ancak ne yaparsınız hello Active Directory uzantısına veya menü öğesini görünmüyorsa veya işaretlenmiş olması durumunda **kullanılamaz**?</span><span class="sxs-lookup"><span data-stu-id="62341-105">But what do you do if hello Active Directory extension or menu item does not appear or if it is marked **Not Available**?</span></span> <span data-ttu-id="62341-106">Bu konu tasarlanmış toohelp ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="62341-106">This topic is designed toohelp.</span></span> <span data-ttu-id="62341-107">Merhaba hangi koşullar altında açıklar **Active Directory** görünmez veya kullanılamaz durumda ve açıklar nasıl tooproceed.</span><span class="sxs-lookup"><span data-stu-id="62341-107">It describes hello conditions under which **Active Directory** does not appear or is unavailable and explains how tooproceed.</span></span>

## <a name="active-directory-is-missing"></a><span data-ttu-id="62341-108">Active Directory eksik</span><span class="sxs-lookup"><span data-stu-id="62341-108">Active Directory is missing</span></span>
<span data-ttu-id="62341-109">Genellikle, bir **Active Directory** öğesi hello sol gezinti menüsünde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="62341-109">Typically, an **Active Directory** item appears in hello left navigation menu.</span></span> <span data-ttu-id="62341-110">Azure Active Directory yordamları Hello yönergeleri Bu öğe görünümünüzde olduğunu varsayın.</span><span class="sxs-lookup"><span data-stu-id="62341-110">hello instructions in Azure Active Directory procedures assume that this item is in your view.</span></span>

![Ekran görüntüsü: Azure Active Directory'de](./media/active-directory-troubleshooting/typical-view.png)

<span data-ttu-id="62341-112">Aşağıdaki koşullar Merhaba, doğru olduğunda hello Active Directory öğesi hello sol gezinti menüsünde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="62341-112">hello Active Directory item appears in hello left navigation menu when any of hello following conditions is true.</span></span> <span data-ttu-id="62341-113">Aksi takdirde hello öğesi görünmez.</span><span class="sxs-lookup"><span data-stu-id="62341-113">Otherwise, hello item does not appear.</span></span>

* <span data-ttu-id="62341-114">(önceki adıyla Windows Live ID bilinir) bir Microsoft hesabı ile oturum açmış geçerli kullanıcı hello.</span><span class="sxs-lookup"><span data-stu-id="62341-114">hello current user signed on with a Microsoft account (formerly known as a Windows Live ID).</span></span>
  
    <span data-ttu-id="62341-115">OR</span><span class="sxs-lookup"><span data-stu-id="62341-115">OR</span></span>
* <span data-ttu-id="62341-116">Hello Azure Kiracı bir dizine sahip ve hello geçerli hesap bir dizin yöneticisidir.</span><span class="sxs-lookup"><span data-stu-id="62341-116">hello Azure tenant has a directory and hello current account is a directory administrator.</span></span>
  
    <span data-ttu-id="62341-117">OR</span><span class="sxs-lookup"><span data-stu-id="62341-117">OR</span></span>
* <span data-ttu-id="62341-118">Hello Azure Kiracı en az bir Azure AD erişim denetimi (ACS) ad alanı vardır.</span><span class="sxs-lookup"><span data-stu-id="62341-118">hello Azure tenant has at least one Azure AD Access Control (ACS) namespace.</span></span> <span data-ttu-id="62341-119">Daha fazla bilgi için bkz: [erişim denetimi Namespace](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span><span class="sxs-lookup"><span data-stu-id="62341-119">For more information, see [Access Control Namespace](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span></span>
  
    <span data-ttu-id="62341-120">OR</span><span class="sxs-lookup"><span data-stu-id="62341-120">OR</span></span>
* <span data-ttu-id="62341-121">Hello Azure Kiracı en az bir Azure çok faktörlü kimlik doğrulama sağlayıcısı sahiptir.</span><span class="sxs-lookup"><span data-stu-id="62341-121">hello Azure tenant has at least one Azure Multi-Factor Authentication provider.</span></span> <span data-ttu-id="62341-122">Daha fazla bilgi için bkz: [yönetme Azure çok faktörlü kimlik doğrulama sağlayıcıları](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="62341-122">For more information, see [Administering Azure Multi-Factor Authentication Providers](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>

<span data-ttu-id="62341-123">Erişim denetimi ad alanı veya bir çok faktörlü kimlik doğrulama sağlayıcısı toocreate tıklatın **+ yeni** > **uygulama hizmetleri** > **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="62341-123">toocreate an Access Control namespace or a Multi-Factor Authentication provider, click **+New** > **App Services** > **Active Directory**.</span></span>

<span data-ttu-id="62341-124">tooget yönetici hakları tooa dizin sahip bir yönetici atamak Yönetici rolü tooyour hesabı.</span><span class="sxs-lookup"><span data-stu-id="62341-124">tooget administrative rights tooa directory, have an administrator assign an administrator role tooyour account.</span></span> <span data-ttu-id="62341-125">Ayrıntılar için bkz [yönetici rolleri atama](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="62341-125">For details, see [Assigning administrator roles](active-directory-assign-admin-roles.md).</span></span>

## <a name="active-directory-is-not-available"></a><span data-ttu-id="62341-126">Active Directory kullanılabilir değil</span><span class="sxs-lookup"><span data-stu-id="62341-126">Active Directory is not available</span></span>
<span data-ttu-id="62341-127">Tıkladığınızda **+ yeni** > **uygulama hizmetleri**, bir **Active Directory** öğesi görünür.</span><span class="sxs-lookup"><span data-stu-id="62341-127">When you click **+New** > **App Services**, an **Active Directory** item appears.</span></span> <span data-ttu-id="62341-128">Özellikle, dizin, erişim denetimi veya çok faktörlü yetki sağlayıcı gibi hello Active Directory özelliklerinden herhangi birini kullanılabilir toohello geçerli kullanıcı olmadığında hello Active Directory öğesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="62341-128">Specifically, hello Active Directory item appears when any of hello Active Directory features, such as Directory, Access Control, or Multi-Factor Auth Provider, are available toohello current user.</span></span>

<span data-ttu-id="62341-129">Ancak, hello sayfa yüklenirken hello öğesi soluk ve işaretlenmiş **kullanılamaz**.</span><span class="sxs-lookup"><span data-stu-id="62341-129">However, while hello page is loading, hello item is dimmed and is marked **Not Available**.</span></span> <span data-ttu-id="62341-130">Bu geçici bir durumdur.</span><span class="sxs-lookup"><span data-stu-id="62341-130">This is a temporary state.</span></span> <span data-ttu-id="62341-131">Birkaç saniye bekleyin, hello öğesi kullanılabilir hale gelir.</span><span class="sxs-lookup"><span data-stu-id="62341-131">If you wait a few seconds, hello item becomes available.</span></span> <span data-ttu-id="62341-132">Merhaba gecikme uzatılırsa yenileme hello web sayfası genellikle hello sorunu giderir.</span><span class="sxs-lookup"><span data-stu-id="62341-132">If hello delay is prolonged, refreshing hello web page often resolves hello problem.</span></span>

![Ekran görüntüsü: Active Directory kullanılabilir değil](./media/active-directory-troubleshooting/not-available.png)

