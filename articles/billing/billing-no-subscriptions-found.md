---
title: "Abonelik bulunamadı hatası Azure portalında veya Azure hesap merkezi oturum açmaya çalıştığınızda | Microsoft Docs"
description: "Hayır abonelik bulunamadı hata oluşur. sorunu için çözüm sağlar Azure portalında veya Azure hesap merkezi ne zaman oturum açın."
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: d1545298-99db-4941-8e97-f24a06bb7cb6
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: genli
ms.openlocfilehash: a4ce9b219c05f8469379c2aac5241fcfffd16033
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a><span data-ttu-id="c6271-103">Abonelik Azure portalında veya Azure hesap merkezi hata bulunamadı</span><span class="sxs-lookup"><span data-stu-id="c6271-103">No subscriptions found error in Azure portal or Azure account center</span></span>
<span data-ttu-id="c6271-104">Oturum açmaya çalıştığınızda "abonelik bulunamadı" hata iletisini alabilirsiniz [Azure portal](https://portal.azure.com/) veya [Azure hesap Merkezi](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="c6271-104">You might receive a "No subscriptions found" error message when you try to sign in to the [Azure portal](https://portal.azure.com/) or the [Azure account center](https://account.windowsazure.com/Subscriptions).</span></span> <span data-ttu-id="c6271-105">Bu makalede, bu sorun için bir çözüm sağlar.</span><span class="sxs-lookup"><span data-stu-id="c6271-105">This article provides a solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="c6271-106">Belirti</span><span class="sxs-lookup"><span data-stu-id="c6271-106">Symptom</span></span>

<span data-ttu-id="c6271-107">Oturum açmaya çalıştığınızda [Azure portal](https://portal.azure.com/) veya [Azure hesap Merkezi](https://account.windowsazure.com/Subscriptions), aşağıdaki hata iletisini alıyorsunuz: "abonelik bulunamadı".</span><span class="sxs-lookup"><span data-stu-id="c6271-107">When you try to sign in to the [Azure portal](https://portal.azure.com/) or the [Azure account center](https://account.windowsazure.com/Subscriptions), you receive the following error message: "No subscriptions found".</span></span>

## <a name="cause"></a><span data-ttu-id="c6271-108">Nedeni</span><span class="sxs-lookup"><span data-stu-id="c6271-108">Cause</span></span>

<span data-ttu-id="c6271-109">Hesabınızın yeterli izinleri yoksa, bu sorun oluşur.</span><span class="sxs-lookup"><span data-stu-id="c6271-109">This problem occurs if your account doesn’t have sufficient permissions.</span></span> 

## <a name="solution"></a><span data-ttu-id="c6271-110">Çözüm</span><span class="sxs-lookup"><span data-stu-id="c6271-110">Solution</span></span>

<span data-ttu-id="c6271-111">Doğru yönetici olarak oturum açtığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c6271-111">Make sure that you log in as the correct administrator.</span></span> <span data-ttu-id="c6271-112">Bir hesabı yönetici yalnızca hesap merkezi erişebilir.</span><span class="sxs-lookup"><span data-stu-id="c6271-112">An Account Administrator can access only the Account Center.</span></span> <span data-ttu-id="c6271-113">Hizmet yöneticileri (SA) ve ortak Yöneticiler (CA) yalnızca Azure portalından veya Klasik Azure portalı için erişim iznine sahip.</span><span class="sxs-lookup"><span data-stu-id="c6271-113">Service Administrators (SA) and Co-Administrators (CA) have access permission only to the Azure portal or the Azure classic portal.</span></span>

### <a name="scenario-1-error-message-is-received-in-the-azure-portalhttpsportalazurecom"></a><span data-ttu-id="c6271-114">Senaryo 1: Hata iletisi alındığında [Azure portalı](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="c6271-114">Scenario 1: Error message is received in the [Azure portal](https://portal.azure.com)</span></span>

<span data-ttu-id="c6271-115">Bu sorunu gidermek için:</span><span class="sxs-lookup"><span data-stu-id="c6271-115">To fix this issue:</span></span>

* <span data-ttu-id="c6271-116">Hesabınızı sağ üst köşedeki tıklayarak doğru Azure directory seçildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="c6271-116">Make sure that the correct Azure directory is selected by clicking your account at the top right.</span></span>

  ![Üst dizini seçin Azure portalının sağ](./media/billing-no-subscriptions-found/directory-switch.png)

* <span data-ttu-id="c6271-118">Sağ Azure directory seçilir, ancak hata iletisini almaya devam [sahibi olarak eklenen hesabınızın](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="c6271-118">If the right Azure directory is selected but you still receive the error message, [have your account added as an Owner](billing-add-change-azure-subscription-administrator.md).</span></span>

### <a name="scenario-2-error-message-is-received-in-the-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a><span data-ttu-id="c6271-119">Senaryo 2: Hata iletisi alındığında [Azure hesap Merkezi](https://account.windowsazure.com/Subscriptions)</span><span class="sxs-lookup"><span data-stu-id="c6271-119">Scenario 2: Error message is received in the [Azure account center](https://account.windowsazure.com/Subscriptions)</span></span>

<span data-ttu-id="c6271-120">Kullandığınız hesabın hesap yöneticisi olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="c6271-120">Check whether the account that you used is the Account Administrator.</span></span> <span data-ttu-id="c6271-121">Hesap Yöneticisi olan doğrulamak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c6271-121">To verify who the Account Administrator is, follow these steps:</span></span>

1. <span data-ttu-id="c6271-122">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c6271-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c6271-123">Hub menüsünde seçin **abonelik**.</span><span class="sxs-lookup"><span data-stu-id="c6271-123">On the Hub menu, select **Subscription**.</span></span>
3. <span data-ttu-id="c6271-124">Kontrol edin ve ardından istediğiniz aboneliği seçin **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="c6271-124">Select the subscription that you want to check, and then select **Settings**.</span></span>
4. <span data-ttu-id="c6271-125">Seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="c6271-125">Select **Properties**.</span></span> <span data-ttu-id="c6271-126">Aboneliğin Hesap Yöneticisi görüntülenen **Hesap Yöneticisi** kutusu.</span><span class="sxs-lookup"><span data-stu-id="c6271-126">The account administrator of the subscription is displayed in the **Account Admin** box.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="c6271-127">Yardım mı gerekiyor?</span><span class="sxs-lookup"><span data-stu-id="c6271-127">Need help?</span></span> <span data-ttu-id="c6271-128">Desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="c6271-128">Contact support.</span></span>
<span data-ttu-id="c6271-129">Hala yardıma gereksiniminiz varsa [desteğine başvurun](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) hızla çözümlenen sorunu almak için.</span><span class="sxs-lookup"><span data-stu-id="c6271-129">If you still need help, [contact support](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) to get your issue resolved quickly.</span></span> 
