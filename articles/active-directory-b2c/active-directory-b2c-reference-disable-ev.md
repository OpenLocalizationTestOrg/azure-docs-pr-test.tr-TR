---
title: "Azure Active Directory B2C: E-posta doğrulama tüketici kaydolma sırasında devre dışı bırakma | Microsoft Docs"
description: "Nasıl toodisable e-posta doğrulama tüketici Azure Active Directory B2C'de kaydolma sırasında gösteren bir konu"
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
ms.openlocfilehash: a8a42eddcb577725f04d70e1b1ebbebf10b5937c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a><span data-ttu-id="ed44f-103">Azure Active Directory B2C: Tüketicinin kaydolma devre dışı bırak e-posta doğrulama</span><span class="sxs-lookup"><span data-stu-id="ed44f-103">Azure Active Directory B2C: Disable email verification during consumer sign-up</span></span>
<span data-ttu-id="ed44f-104">Etkin olduğunda, tüketici bir Azure Active Directory (Azure AD) B2C verir özelliği toosign uygulamalar için bir e-posta adresi sağlayarak ve yerel bir hesap oluşturma hello.</span><span class="sxs-lookup"><span data-stu-id="ed44f-104">When enabled, Azure Active Directory (Azure AD) B2C gives a consumer hello ability toosign up for applications by providing an email address and creating a local account.</span></span> <span data-ttu-id="ed44f-105">Azure AD B2C, tüketiciye tooverify kılarak geçerli e-posta adresleri sağlar hello kaydolma işlemi sırasında bunları.</span><span class="sxs-lookup"><span data-stu-id="ed44f-105">Azure AD B2C ensures valid email addresses by requiring consumers tooverify them during hello sign-up process.</span></span> <span data-ttu-id="ed44f-106">Ayrıca, kötü amaçlı bir otomatik işlem'in hello uygulamaları için sahte hesapları oluşturma engeller.</span><span class="sxs-lookup"><span data-stu-id="ed44f-106">It also prevents a malicious automated process from generating fake accounts for hello applications.</span></span>

<span data-ttu-id="ed44f-107">Bazı uygulama geliştiricileri tooskip e-posta doğrulama hello kaydolma işlemi sırasında tercih ve bunun yerine hello e-posta adresini doğrulayın. daha sonra bir tüketiciye sahip.</span><span class="sxs-lookup"><span data-stu-id="ed44f-107">Some application developers prefer tooskip email verification during hello sign-up process and instead have consumers verify hello email address later.</span></span> <span data-ttu-id="ed44f-108">Bu, Azure AD B2C için toosupport yapılandırılmış toodisable e-posta doğrulama olabilir.</span><span class="sxs-lookup"><span data-stu-id="ed44f-108">toosupport this, Azure AD B2C can be configured toodisable email verification.</span></span> <span data-ttu-id="ed44f-109">Bunun yapılması daha sorunsuz bir kaydolma işlemi oluşturur ve geliştiricilerin sahip değilse bu Tüketiciler, e-posta adresinden doğruladıktan hello esneklik toodifferentiate hello tüketicileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="ed44f-109">Doing so creates a smoother sign-up process and gives developers hello flexibility toodifferentiate hello consumers that have verified their email address from those consumers that have not.</span></span>

<span data-ttu-id="ed44f-110">Varsayılan olarak, e-posta doğrulama açık kayıt ilkeleri vardır.</span><span class="sxs-lookup"><span data-stu-id="ed44f-110">By default, sign-up policies have email verification turned on.</span></span> <span data-ttu-id="ed44f-111">Kullanım hello adımları tooturn onu devre dışı:</span><span class="sxs-lookup"><span data-stu-id="ed44f-111">Use hello following steps tooturn it off:</span></span>

1. <span data-ttu-id="ed44f-112">[Bu adımları toonavigate toohello B2C özellikleri dikey hello Azure portalı üzerinde izleyin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="ed44f-112">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="ed44f-113">Tıklatın **kayıt ilkeleri** veya **oturum açma veya kaydolma ilkeleri** için yapılandırdığınıza bağlı olarak kaydolma.</span><span class="sxs-lookup"><span data-stu-id="ed44f-113">Click **Sign-up policies** or **Sign-up or sign-in policies** depending on what you configured for sign-up.</span></span>
3. <span data-ttu-id="ed44f-114">İlke (örneğin, "B2C_1_SiUp") tooopen'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ed44f-114">Click your policy (for example, "B2C_1_SiUp") tooopen it.</span></span> <span data-ttu-id="ed44f-115">Tıklatın **Düzenle** hello dikey penceresinde hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="ed44f-115">Click **Edit** at hello top of hello blade.</span></span>
4. <span data-ttu-id="ed44f-116">Tıklatın **sayfa UI özelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="ed44f-116">Click **Page UI Customization**.</span></span>
5. <span data-ttu-id="ed44f-117">Tıklatın **yerel hesap kayıt sayfasına**.</span><span class="sxs-lookup"><span data-stu-id="ed44f-117">Click **Local account sign-up page**.</span></span>
6. <span data-ttu-id="ed44f-118">Tıklatın **e-posta adresi** hello içinde **adı** hello sütununda **kaydolma özniteliklerini** bölümü.</span><span class="sxs-lookup"><span data-stu-id="ed44f-118">Click **Email Address** in hello **Name** column under hello **Sign-up attributes** section.</span></span>
7. <span data-ttu-id="ed44f-119">İki durumlu hello **bölgedeki tüm sitelerden** çok seçenek**Hayır**.</span><span class="sxs-lookup"><span data-stu-id="ed44f-119">Toggle hello **Require verification** option too**No**.</span></span>
8. <span data-ttu-id="ed44f-120">Tıklatın **Tamam** hello ulaşana kadar hello altındaki **Düzenle İlkesi** dikey.</span><span class="sxs-lookup"><span data-stu-id="ed44f-120">Click **OK** at hello bottom until you reach hello **Edit policy** blade.</span></span>
9. <span data-ttu-id="ed44f-121">Tıklatın **kaydetmek** hello dikey penceresinde hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="ed44f-121">Click **Save** at hello top of hello blade.</span></span> <span data-ttu-id="ed44f-122">İşiniz bittiğinde!</span><span class="sxs-lookup"><span data-stu-id="ed44f-122">You're done!</span></span>

> [!NOTE]
> <span data-ttu-id="ed44f-123">E-posta doğrulama hello kaydolma işlemini devre dışı bırakma toospam neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="ed44f-123">Disabling email verification in hello sign-up process may lead toospam.</span></span> <span data-ttu-id="ed44f-124">Merhaba varsayılan devre dışı bırakırsanız, kendi doğrulama sistemi ekleme öneririz.</span><span class="sxs-lookup"><span data-stu-id="ed44f-124">If you disable hello default one, we recommend adding your own verification system.</span></span>
> 
> 

<span data-ttu-id="ed44f-125">Her zaman açık toofeedback ve öneriler duyuyoruz!</span><span class="sxs-lookup"><span data-stu-id="ed44f-125">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="ed44f-126">Bu konu ile bir güçlükle sahip veya bu içeriğin geliştirilmesi için öneriler varsa, hello sayfanın hello sonundaki görüşlerinize değer veriyoruz.</span><span class="sxs-lookup"><span data-stu-id="ed44f-126">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="ed44f-127">Özellik istekleri için çok eklemediğiniz[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="ed44f-127">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
