---
title: aaaGet hello bulutta Azure MFA kullanmaya | Microsoft Docs
description: "Bu tooget hello bulutta Azure MFA ile çalışmaya nasıl açıklayan hello Microsoft Azure multi-Factor authentication sayfasıdır."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 6b2e6549-1a26-4666-9c4a-cbe5d64c4e66
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/24/2017
ms.author: kgremban
ms.openlocfilehash: a4aaf44bf08d96f2baad155072fdd6e0e727ce8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-in-hello-cloud"></a><span data-ttu-id="1a60a-103">Merhaba bulutta Azure multi Factor Authentication ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="1a60a-103">Getting started with Azure Multi-Factor Authentication in hello cloud</span></span>
<span data-ttu-id="1a60a-104">Bu makalede hello bulutta Azure multi-Factor Authentication kullanarak tooget nasıl başlatılacağını aracılığıyla anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1a60a-104">This article walks through how tooget started using Azure Multi-Factor Authentication in hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="1a60a-105">Merhaba aşağıdaki belgeleri bilgileri kullanarak tooenable kullanıcıların nasıl hello üzerinde sağlar **Klasik Azure portalı**.</span><span class="sxs-lookup"><span data-stu-id="1a60a-105">hello following documentation provides information on how tooenable users using hello **Azure Classic Portal**.</span></span> <span data-ttu-id="1a60a-106">Hakkında bilgi arıyorsanız O365 kullanıcıları için Azure multi-Factor Authentication yukarı tooset bakın [Office 365 için multi-Factor authentication ayarlayın.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span><span class="sxs-lookup"><span data-stu-id="1a60a-106">If you are looking for information on how tooset up Azure Multi-Factor Authentication for O365 users, see [Set up multi-factor authentication for Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span></span>

![MFA'hello bulut](./media/multi-factor-authentication-get-started-cloud/mfa_in_cloud.png)

## <a name="prerequisite"></a><span data-ttu-id="1a60a-108">Önkoşul</span><span class="sxs-lookup"><span data-stu-id="1a60a-108">Prerequisite</span></span>
<span data-ttu-id="1a60a-109">[Azure aboneliği için kaydolun](https://azure.microsoft.com/pricing/free-trial/) -zaten bir Azure aboneliğiniz yoksa toosign yukarı biri için gereksinim duyduğunuz.</span><span class="sxs-lookup"><span data-stu-id="1a60a-109">[Sign up for an Azure subscription](https://azure.microsoft.com/pricing/free-trial/) - If you do not already have an Azure subscription, you need toosign-up for one.</span></span> <span data-ttu-id="1a60a-110">Yeni başlıyor ve Azure MFA’yı henüz kullanmaya başlıyorsanız, deneme aboneliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a60a-110">If you are just starting out and using Azure MFA you can use a trial subscription</span></span>

## <a name="enable-azure-multi-factor-authentication"></a><span data-ttu-id="1a60a-111">Azure Multi-Factor Authentication’ı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="1a60a-111">Enable Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="1a60a-112">Kullanıcılarınızın Azure çok faktörlü kimlik doğrulamasını içeren lisanslara sahip olduğu sürece, hiçbir şey Azure MFA üzerinde toodo tooturn gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="1a60a-112">As long as your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need toodo tooturn on Azure MFA.</span></span> <span data-ttu-id="1a60a-113">Her kullanıcı için iki aşamalı doğrulama istemeye başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a60a-113">You can start requiring two-step verification on an individual user basis.</span></span> <span data-ttu-id="1a60a-114">Azure MFA'yı etkinleştirmek hello lisansları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1a60a-114">hello licenses that enable Azure MFA are:</span></span>
- <span data-ttu-id="1a60a-115">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="1a60a-115">Azure Multi-Factor Authentication</span></span>
- <span data-ttu-id="1a60a-116">Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="1a60a-116">Azure Active Directory Premium</span></span>
- <span data-ttu-id="1a60a-117">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="1a60a-117">Enterprise Mobility + Security</span></span>

<span data-ttu-id="1a60a-118">Bu üç lisanstan yoksa veya yeterli lisans toocover olmayan tüm çok Tamam kullanıcılarınızın,.</span><span class="sxs-lookup"><span data-stu-id="1a60a-118">If you don't have one of these three licenses, or you don't have enough licenses toocover all of your users, that's ok too.</span></span> <span data-ttu-id="1a60a-119">Ek bir adım toodo yalnızca sahip ve [multi-Factor Auth sağlayıcısı oluşturmak](multi-factor-authentication-get-started-auth-provider.md) dizininizde.</span><span class="sxs-lookup"><span data-stu-id="1a60a-119">You just have toodo an extra step and [Create a Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md) in your directory.</span></span>

## <a name="turn-on-two-step-verification-for-users"></a><span data-ttu-id="1a60a-120">Kullanıcılar için iki aşamalı doğrulamayı açma</span><span class="sxs-lookup"><span data-stu-id="1a60a-120">Turn on two-step verification for users</span></span>

<span data-ttu-id="1a60a-121">Listelenen hello yordamlardan birini kullanın [nasıl bir kullanıcı veya grup için toorequire iki aşamalı doğrulamayı](multi-factor-authentication-get-started-user-states.md) toostart Azure MFA kullanma.</span><span class="sxs-lookup"><span data-stu-id="1a60a-121">Use one of hello procedures listed in [How toorequire two-step verification for a user or group](multi-factor-authentication-get-started-user-states.md) toostart using Azure MFA.</span></span> <span data-ttu-id="1a60a-122">Tüm oturum açma işlemleri için tooenforce iki aşamalı doğrulamayı seçebilirsiniz veya yalnızca tooyou önemli koşullu erişim ilkeleri toorequire iki aşamalı doğrulamayı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a60a-122">You can choose tooenforce two-step verification for all sign-ins, or you can create conditional access policies toorequire two-step verification only when it matters tooyou.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a60a-123">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="1a60a-123">Next Steps</span></span>
<span data-ttu-id="1a60a-124">Merhaba bulutta Azure multi-Factor Authentication ayarlamak, yapılandırmak ve dağıtımınızın ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1a60a-124">Now that you have set up Azure Multi-Factor Authentication in hello cloud, you can configure and set up your deployment.</span></span> <span data-ttu-id="1a60a-125">Daha fazla bilgi için bkz. [Azure Multi-Factor Authentication’ı yapılandırma](multi-factor-authentication-whats-next.md).</span><span class="sxs-lookup"><span data-stu-id="1a60a-125">See [Configuring Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md) for more details.</span></span>

