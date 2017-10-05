---
title: "Azure Active Directory B2C: E-posta doğrulama tüketici kaydolma sırasında devre dışı bırakma | Microsoft Docs"
description: "E-posta doğrulama tüketici Azure Active Directory B2C'de kaydolma sırasında devre dışı bırakma gösteren bir konu"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 433f32b8-96d2-4113-aa82-efcf42fa9827
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/06/2017
ms.author: parakhj
ms.openlocfilehash: d8e44a8aade60d21734477d60bccc2bd5194436e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a><span data-ttu-id="5bd23-103">Azure Active Directory B2C: Tüketicinin kaydolma devre dışı bırak e-posta doğrulama</span><span class="sxs-lookup"><span data-stu-id="5bd23-103">Azure Active Directory B2C: Disable email verification during consumer sign-up</span></span>
<span data-ttu-id="5bd23-104">Etkinleştirildiğinde, Azure Active Directory (Azure AD) B2C tüketici uygulamaları için bir e-posta adresi sağlayarak ve yerel bir hesap oluşturma kaydolun olanağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="5bd23-104">When enabled, Azure Active Directory (Azure AD) B2C gives a consumer the ability to sign up for applications by providing an email address and creating a local account.</span></span> <span data-ttu-id="5bd23-105">Azure AD B2C, kayıt işlemi sırasında doğrulamak tüketicilere gerektirerek geçerli e-posta adresleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="5bd23-105">Azure AD B2C ensures valid email addresses by requiring consumers to verify them during the sign-up process.</span></span> <span data-ttu-id="5bd23-106">Ayrıca, kötü amaçlı bir otomatik işlem'in uygulamaları için sahte hesapları oluşturma engeller.</span><span class="sxs-lookup"><span data-stu-id="5bd23-106">It also prevents a malicious automated process from generating fake accounts for the applications.</span></span>

<span data-ttu-id="5bd23-107">Bazı uygulama geliştiricileri e-posta doğrulama kaydolma işlemi sırasında atlayın ve bunun yerine e-posta adresini doğrulayın. daha sonra bir tüketiciye sahip tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="5bd23-107">Some application developers prefer to skip email verification during the sign-up process and instead have consumers verify the email address later.</span></span> <span data-ttu-id="5bd23-108">Bunu desteklemek için Azure AD B2C e-posta doğrulama devre dışı bırakmak için yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="5bd23-108">To support this, Azure AD B2C can be configured to disable email verification.</span></span> <span data-ttu-id="5bd23-109">Bunun yapılması daha sorunsuz bir kaydolma işlemi oluşturur ve geliştiricilerin sahip değilse bu Tüketiciler, e-posta adresinden doğruladıktan tüketicileri ayırt esnekliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="5bd23-109">Doing so creates a smoother sign-up process and gives developers the flexibility to differentiate the consumers that have verified their email address from those consumers that have not.</span></span>

<span data-ttu-id="5bd23-110">Varsayılan olarak, e-posta doğrulama açık kayıt ilkeleri vardır.</span><span class="sxs-lookup"><span data-stu-id="5bd23-110">By default, sign-up policies have email verification turned on.</span></span> <span data-ttu-id="5bd23-111">Devre dışı bırakmak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="5bd23-111">Use the following steps to turn it off:</span></span>

1. <span data-ttu-id="5bd23-112">[Azure portalındaki B2C özellikleri dikey penceresine gitmek için aşağıdaki adımları izleyin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="5bd23-112">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="5bd23-113">Tıklatın **kayıt ilkeleri** veya **oturum açma veya kaydolma ilkeleri** için yapılandırdığınıza bağlı olarak kaydolma.</span><span class="sxs-lookup"><span data-stu-id="5bd23-113">Click **Sign-up policies** or **Sign-up or sign-in policies** depending on what you configured for sign-up.</span></span>
3. <span data-ttu-id="5bd23-114">Açmak için ilke (örneğin, "B2C_1_SiUp") tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5bd23-114">Click your policy (for example, "B2C_1_SiUp") to open it.</span></span> <span data-ttu-id="5bd23-115">Tıklatın **Düzenle** dikey pencerenin üstündeki.</span><span class="sxs-lookup"><span data-stu-id="5bd23-115">Click **Edit** at the top of the blade.</span></span>
4. <span data-ttu-id="5bd23-116">Tıklatın **sayfa UI özelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="5bd23-116">Click **Page UI Customization**.</span></span>
5. <span data-ttu-id="5bd23-117">Tıklatın **yerel hesap kayıt sayfasına**.</span><span class="sxs-lookup"><span data-stu-id="5bd23-117">Click **Local account sign-up page**.</span></span>
6. <span data-ttu-id="5bd23-118">Tıklatın **e-posta adresi** içinde **adı** sütunu altında **kaydolma özniteliklerini** bölümü.</span><span class="sxs-lookup"><span data-stu-id="5bd23-118">Click **Email Address** in the **Name** column under the **Sign-up attributes** section.</span></span>
7. <span data-ttu-id="5bd23-119">İki durumlu **bölgedeki tüm sitelerden** için seçenek **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="5bd23-119">Toggle the **Require verification** option to **No**.</span></span>
8. <span data-ttu-id="5bd23-120">Tıklatın **Tamam** ulaşana kadar altındaki **Düzenle İlkesi** dikey.</span><span class="sxs-lookup"><span data-stu-id="5bd23-120">Click **OK** at the bottom until you reach the **Edit policy** blade.</span></span>
9. <span data-ttu-id="5bd23-121">Tıklatın **kaydetmek** dikey pencerenin üstündeki.</span><span class="sxs-lookup"><span data-stu-id="5bd23-121">Click **Save** at the top of the blade.</span></span> <span data-ttu-id="5bd23-122">İşiniz bittiğinde!</span><span class="sxs-lookup"><span data-stu-id="5bd23-122">You're done!</span></span>

> [!NOTE]
> <span data-ttu-id="5bd23-123">E-posta doğrulama kayıt işlemini devre dışı bırakma istenmeyen posta göndermek için neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="5bd23-123">Disabling email verification in the sign-up process may lead to spam.</span></span> <span data-ttu-id="5bd23-124">Varsayılan devre dışı bırakırsanız, kendi doğrulama sistemi ekleme öneririz.</span><span class="sxs-lookup"><span data-stu-id="5bd23-124">If you disable the default one, we recommend adding your own verification system.</span></span>
> 
> 

<span data-ttu-id="5bd23-125">Biz her zaman görüş ve öneriler için açık!</span><span class="sxs-lookup"><span data-stu-id="5bd23-125">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="5bd23-126">Bu konu ile bir güçlükle sahip veya bu içeriğin geliştirilmesi için öneriler varsa, sayfanın sonundaki görüşlerinize değer veriyoruz.</span><span class="sxs-lookup"><span data-stu-id="5bd23-126">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="5bd23-127">Özellik istekleri için bunları Ekle [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="5bd23-127">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>