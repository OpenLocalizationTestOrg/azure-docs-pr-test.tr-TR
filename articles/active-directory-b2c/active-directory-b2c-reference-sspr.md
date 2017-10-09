---
title: "Azure Active Directory B2C: Self Servis parola sıfırlama | Microsoft Docs"
description: "Azure Active Directory B2C içinde tüketicileriniz için nasıl tooset Self Servis parola sıfırlama gösteren bir konu"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: curtand
ms.assetid: c87ed86e-1520-42b1-8c31-46cd44ed5310
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: ff87eea42259b610702da73af35d0a38eb7dd33d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a><span data-ttu-id="ffda9-103">Azure Active Directory B2C: Self Servis parola sıfırlama tüketicileriniz ayarlama</span><span class="sxs-lookup"><span data-stu-id="ffda9-103">Azure Active Directory B2C: Set up self-service password reset for your consumers</span></span>
<span data-ttu-id="ffda9-104">Merhaba ile Self Servis parola sıfırlama özelliği, (kaydolan yerel hesaplar için) tüketicileriniz üzerinde kendi parolalarını sıfırlayabilir.</span><span class="sxs-lookup"><span data-stu-id="ffda9-104">With hello self-service password reset feature, your consumers (who have signed up for local accounts) can reset their passwords on their own.</span></span> <span data-ttu-id="ffda9-105">Özellikle, uygulamanızın düzenli olarak kullanan tüketicilerin milyonlarca varsa bu destek ekibiniz üzerindeki hello yük önemli ölçüde azaltır.</span><span class="sxs-lookup"><span data-stu-id="ffda9-105">This significantly reduces hello burden on your support staff, especially if your application has millions of consumers using it on a regular basis.</span></span> <span data-ttu-id="ffda9-106">Şu anda yalnızca bir kurtarma yöntemi olarak doğrulanmış e-posta adresini kullanarak destekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="ffda9-106">Currently, we only support using a verified email address as a recovery method.</span></span> <span data-ttu-id="ffda9-107">Ek kurtarma yöntemleri (doğrulanmış telefon numarası, güvenlik soruları, vb.) hello gelecekte ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="ffda9-107">We will add additional recovery methods (verified phone number, security questions, etc.) in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="ffda9-108">Bu makale tooself hizmeti parolasını geçerlidir hello bir oturum açma ilkesi bağlamında kullanılan sıfırlama.</span><span class="sxs-lookup"><span data-stu-id="ffda9-108">This article applies tooself-service password reset used in hello context of a sign-in policy.</span></span> <span data-ttu-id="ffda9-109">Tam olarak özelleştirilebilir parola sıfırlama ilkeleri uygulamanızdan çağrılan gerekirse bkz [bu makalede](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span><span class="sxs-lookup"><span data-stu-id="ffda9-109">If you need fully customizable password reset policies invoked from your app, see [this article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span></span>
> 
> 

<span data-ttu-id="ffda9-110">Varsayılan olarak, Self Servis parola dizininize sahip olmaz sıfırlama açık.</span><span class="sxs-lookup"><span data-stu-id="ffda9-110">By default, your directory will not have self-service password reset turned on.</span></span> <span data-ttu-id="ffda9-111">Kullanım hello adımları tooturn, üzerinde:</span><span class="sxs-lookup"><span data-stu-id="ffda9-111">Use hello following steps tooturn it on:</span></span>

1. <span data-ttu-id="ffda9-112">İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com/) Abonelik Yöneticisi hello gibi.</span><span class="sxs-lookup"><span data-stu-id="ffda9-112">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) as hello Subscription Administrator.</span></span> <span data-ttu-id="ffda9-113">Aynı iş veya Okul hesabı veya aynı Microsoft hesabını dizininize toocreate kullanılan hello hello budur.</span><span class="sxs-lookup"><span data-stu-id="ffda9-113">This is hello same work or school account or hello same Microsoft account that you used toocreate your directory.</span></span>
2. <span data-ttu-id="ffda9-114">Merhaba hello sol taraftaki gezinti çubuğunda toohello Active Directory uzantısına gidin.</span><span class="sxs-lookup"><span data-stu-id="ffda9-114">Navigate toohello Active Directory extension on hello navigation bar on hello left side.</span></span>
3. <span data-ttu-id="ffda9-115">Dizininizi hello altında Bul **Directory** sekmesinde ve tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ffda9-115">Find your directory under hello **Directory** tab and click it.</span></span>
4. <span data-ttu-id="ffda9-116">Merhaba tıklatın **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="ffda9-116">Click hello **Configure** tab.</span></span>
5. <span data-ttu-id="ffda9-117">Toohello aşağı **kullanıcı parolası sıfırlama İlkesi** bölümü ve iki durumlu hello **kullanıcılar parola sıfırlama için etkin** çok seçenek**Evet**.</span><span class="sxs-lookup"><span data-stu-id="ffda9-117">Scroll down toohello **User password reset policy** section and toggle hello **Users enabled for password reset** option too**YES**.</span></span> <span data-ttu-id="ffda9-118">Bu hello fark **alternatif e-posta adresi** seçeneğini işaretli; olduğu gibi bırakın.</span><span class="sxs-lookup"><span data-stu-id="ffda9-118">Notice that hello **Alternate Email Address** option is checked; leave it as it is.</span></span>
   
    ![Self servis parola sıfırlama](./media/active-directory-b2c-reference-sspr/sspr.png)
6. <span data-ttu-id="ffda9-120">Tıklatın **kaydetmek** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="ffda9-120">Click **Save** at hello bottom of hello page.</span></span> <span data-ttu-id="ffda9-121">İşiniz bittiğinde!</span><span class="sxs-lookup"><span data-stu-id="ffda9-121">You're done!</span></span>

<span data-ttu-id="ffda9-122">tootest, kullanım hello "Şimdi Çalıştır" özelliğini yerel hesaplar için kimlik sağlayıcısı olarak sahip tüm oturum açma İlkesi'ni tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ffda9-122">tootest, use hello "Run now" feature on any sign-in policy that has local accounts as an identity provider.</span></span> <span data-ttu-id="ffda9-123">Merhaba yerel hesap oturum açma (burada, bir e-posta adresi ve parola veya kullanıcı adı ve parola girin) tıklatın sayfa **hesabınıza erişemiyor?** tooverify hello müşteri deneyimi.</span><span class="sxs-lookup"><span data-stu-id="ffda9-123">On hello local account sign-in page (where you enter an email address and password, or a username and password), click **Can't access your account?** tooverify hello consumer experience.</span></span>

> [!NOTE]
> <span data-ttu-id="ffda9-124">Merhaba Self Servis parola sıfırlama sayfaları hello kullanarak özelleştirilebilir [şirket markası özelliğini](../active-directory/active-directory-add-company-branding.md).</span><span class="sxs-lookup"><span data-stu-id="ffda9-124">hello self-service password reset pages can be customized by using hello [company branding feature](../active-directory/active-directory-add-company-branding.md).</span></span>
> 
> 

