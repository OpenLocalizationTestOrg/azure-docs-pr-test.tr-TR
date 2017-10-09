---
title: "aaaNo abonelik bulunamadı hatası toosign tooAzure portalında veya Azure hesap merkezi çalıştığınızda | Microsoft Docs"
description: "Hayır abonelik bulunamadı hata oluşur. sorunu için Hello çözümü sağlar tooAzure portalı veya Azure hesap merkezi oturum açtığınızda."
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
ms.openlocfilehash: def4d4a1f883dd948fe8132f2d85abc4c23ae624
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a><span data-ttu-id="744f6-103">Abonelik Azure portalında veya Azure hesap merkezi hata bulunamadı</span><span class="sxs-lookup"><span data-stu-id="744f6-103">No subscriptions found error in Azure portal or Azure account center</span></span>
<span data-ttu-id="744f6-104">Toohello toosign çalıştığınızda bir "abonelik bulunamadı" hata iletisini alabilirsiniz [Azure portal](https://portal.azure.com/) veya hello [Azure hesap Merkezi](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="744f6-104">You might receive a "No subscriptions found" error message when you try toosign in toohello [Azure portal](https://portal.azure.com/) or hello [Azure account center](https://account.windowsazure.com/Subscriptions).</span></span> <span data-ttu-id="744f6-105">Bu makalede, bu sorun için bir çözüm sağlar.</span><span class="sxs-lookup"><span data-stu-id="744f6-105">This article provides a solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="744f6-106">Belirti</span><span class="sxs-lookup"><span data-stu-id="744f6-106">Symptom</span></span>

<span data-ttu-id="744f6-107">Toohello toosign çalıştığınızda [Azure portal](https://portal.azure.com/) veya hello [Azure hesap Merkezi](https://account.windowsazure.com/Subscriptions), hello aşağıdaki hata iletisini alıyorsunuz: "abonelik bulunamadı".</span><span class="sxs-lookup"><span data-stu-id="744f6-107">When you try toosign in toohello [Azure portal](https://portal.azure.com/) or hello [Azure account center](https://account.windowsazure.com/Subscriptions), you receive hello following error message: "No subscriptions found".</span></span>

## <a name="cause"></a><span data-ttu-id="744f6-108">Nedeni</span><span class="sxs-lookup"><span data-stu-id="744f6-108">Cause</span></span>

<span data-ttu-id="744f6-109">Hesabınızın yeterli izinleri yoksa, bu sorun oluşur.</span><span class="sxs-lookup"><span data-stu-id="744f6-109">This problem occurs if your account doesn’t have sufficient permissions.</span></span> 

## <a name="solution"></a><span data-ttu-id="744f6-110">Çözüm</span><span class="sxs-lookup"><span data-stu-id="744f6-110">Solution</span></span>

<span data-ttu-id="744f6-111">Hello doğru yönetici olarak oturum açtığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="744f6-111">Make sure that you log in as hello correct administrator.</span></span> <span data-ttu-id="744f6-112">Bir hesabı yönetici yalnızca hello hesap Merkezi'nde erişebilir.</span><span class="sxs-lookup"><span data-stu-id="744f6-112">An Account Administrator can access only hello Account Center.</span></span> <span data-ttu-id="744f6-113">Hizmet yöneticileri (SA) ve ortak Yöneticiler (CA) erişim izni yalnızca toohello Azure portalında veya Klasik Azure portalı hello.</span><span class="sxs-lookup"><span data-stu-id="744f6-113">Service Administrators (SA) and Co-Administrators (CA) have access permission only toohello Azure portal or hello Azure classic portal.</span></span>

### <a name="scenario-1-error-message-is-received-in-hello-azure-portalhttpsportalazurecom"></a><span data-ttu-id="744f6-114">Senaryo 1: Hello hata iletisi alındığında [Azure portalı](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="744f6-114">Scenario 1: Error message is received in hello [Azure portal](https://portal.azure.com)</span></span>

<span data-ttu-id="744f6-115">toofix bu sorunu:</span><span class="sxs-lookup"><span data-stu-id="744f6-115">toofix this issue:</span></span>

* <span data-ttu-id="744f6-116">Azure directory hesabınıza hello üst sağ tıklayarak seçili doğru bu hello emin olun.</span><span class="sxs-lookup"><span data-stu-id="744f6-116">Make sure that hello correct Azure directory is selected by clicking your account at hello top right.</span></span>

  ![Merhaba SELECT hello dizininde hello Azure portal sağ üst](./media/billing-no-subscriptions-found/directory-switch.png)

* <span data-ttu-id="744f6-118">Merhaba sağ Azure directory seçiliyse ancak hello hata iletisini almaya devam [sahibi olarak eklenen hesabınızın](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="744f6-118">If hello right Azure directory is selected but you still receive hello error message, [have your account added as an Owner](billing-add-change-azure-subscription-administrator.md).</span></span>

### <a name="scenario-2-error-message-is-received-in-hello-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a><span data-ttu-id="744f6-119">Senaryo 2: Hello hata iletisi alındığında [Azure hesap Merkezi](https://account.windowsazure.com/Subscriptions)</span><span class="sxs-lookup"><span data-stu-id="744f6-119">Scenario 2: Error message is received in hello [Azure account center](https://account.windowsazure.com/Subscriptions)</span></span>

<span data-ttu-id="744f6-120">Merhaba hesabı hello Hesap Yöneticisi olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="744f6-120">Check whether hello account that you used is hello Account Administrator.</span></span> <span data-ttu-id="744f6-121">Hesap Yöneticisi hello tooverify, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="744f6-121">tooverify who hello Account Administrator is, follow these steps:</span></span>

1. <span data-ttu-id="744f6-122">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="744f6-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="744f6-123">Merhaba Hub menüsünde seçin **abonelik**.</span><span class="sxs-lookup"><span data-stu-id="744f6-123">On hello Hub menu, select **Subscription**.</span></span>
3. <span data-ttu-id="744f6-124">Toocheck istediğiniz ve ardından hello aboneliği seçin **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="744f6-124">Select hello subscription that you want toocheck, and then select **Settings**.</span></span>
4. <span data-ttu-id="744f6-125">Seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="744f6-125">Select **Properties**.</span></span> <span data-ttu-id="744f6-126">hello aboneliğin Hesap Yöneticisi Hello hello görüntülenen **Hesap Yöneticisi** kutusu.</span><span class="sxs-lookup"><span data-stu-id="744f6-126">hello account administrator of hello subscription is displayed in hello **Account Admin** box.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="744f6-127">Yardım mı gerekiyor?</span><span class="sxs-lookup"><span data-stu-id="744f6-127">Need help?</span></span> <span data-ttu-id="744f6-128">Desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="744f6-128">Contact support.</span></span>
<span data-ttu-id="744f6-129">Hala yardıma gereksiniminiz varsa [desteğine başvurun](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) sorunu Çözümlendi hızla tooget.</span><span class="sxs-lookup"><span data-stu-id="744f6-129">If you still need help, [contact support](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) tooget your issue resolved quickly.</span></span> 
