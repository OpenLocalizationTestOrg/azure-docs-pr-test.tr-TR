---
title: "Azure Active Directory B2C: Self Servis parola sıfırlama | Microsoft Docs"
description: "Self Servis parola sıfırlama, Azure Active Directory B2C tüketici için ayarlamak üzere nasıl gösteren bir konu"
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
ms.openlocfilehash: 0508868e3b00c5771cc26038a3dd71fde6625a84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a><span data-ttu-id="4a075-103">Azure Active Directory B2C: Self Servis parola sıfırlama tüketicileriniz ayarlama</span><span class="sxs-lookup"><span data-stu-id="4a075-103">Azure Active Directory B2C: Set up self-service password reset for your consumers</span></span>
<span data-ttu-id="4a075-104">Self Servis parola sıfırlama özelliğiyle (kaydolan yerel hesaplar için) tüketicileriniz üzerinde kendi parolalarını sıfırlayabilir.</span><span class="sxs-lookup"><span data-stu-id="4a075-104">With the self-service password reset feature, your consumers (who have signed up for local accounts) can reset their passwords on their own.</span></span> <span data-ttu-id="4a075-105">Özellikle, uygulamanızın düzenli olarak kullanan tüketicilerin milyonlarca varsa bu destek ekibiniz üzerindeki yük önemli ölçüde azaltır.</span><span class="sxs-lookup"><span data-stu-id="4a075-105">This significantly reduces the burden on your support staff, especially if your application has millions of consumers using it on a regular basis.</span></span> <span data-ttu-id="4a075-106">Şu anda yalnızca bir kurtarma yöntemi olarak doğrulanmış e-posta adresini kullanarak destekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="4a075-106">Currently, we only support using a verified email address as a recovery method.</span></span> <span data-ttu-id="4a075-107">Ek kurtarma yöntemleri (doğrulanmış telefon numarası, güvenlik soruları, vb.) gelecekte ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="4a075-107">We will add additional recovery methods (verified phone number, security questions, etc.) in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="4a075-108">Bu makalede Self Servis parola için geçerli bir oturum açma ilkesi bağlamında kullanılan sıfırlama.</span><span class="sxs-lookup"><span data-stu-id="4a075-108">This article applies to self-service password reset used in the context of a sign-in policy.</span></span> <span data-ttu-id="4a075-109">Tam olarak özelleştirilebilir parola sıfırlama ilkeleri uygulamanızdan çağrılan gerekirse bkz [bu makalede](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span><span class="sxs-lookup"><span data-stu-id="4a075-109">If you need fully customizable password reset policies invoked from your app, see [this article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span></span>
> 
> 

<span data-ttu-id="4a075-110">Varsayılan olarak, Self Servis parola dizininize sahip olmaz sıfırlama açık.</span><span class="sxs-lookup"><span data-stu-id="4a075-110">By default, your directory will not have self-service password reset turned on.</span></span> <span data-ttu-id="4a075-111">Etkinleştirmek için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="4a075-111">Use the following steps to turn it on:</span></span>

1. <span data-ttu-id="4a075-112">[Klasik Azure portalında](https://manage.windowsazure.com/) Abonelik Yöneticisi olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4a075-112">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) as the Subscription Administrator.</span></span> <span data-ttu-id="4a075-113">Aynı iş veya Okul hesabı veya dizin oluşturmak için kullanılan aynı Microsoft hesabını budur.</span><span class="sxs-lookup"><span data-stu-id="4a075-113">This is the same work or school account or the same Microsoft account that you used to create your directory.</span></span>
2. <span data-ttu-id="4a075-114">Sol taraftaki gezinti çubuğunda Active Directory uzantısına gidin.</span><span class="sxs-lookup"><span data-stu-id="4a075-114">Navigate to the Active Directory extension on the navigation bar on the left side.</span></span>
3. <span data-ttu-id="4a075-115">Dizininizi altında Bul **Directory** sekmesinde ve tıklatın.</span><span class="sxs-lookup"><span data-stu-id="4a075-115">Find your directory under the **Directory** tab and click it.</span></span>
4. <span data-ttu-id="4a075-116">**Configure (Yapılandır)** sekmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4a075-116">Click the **Configure** tab.</span></span>
5. <span data-ttu-id="4a075-117">Ekranı aşağı kaydırarak **kullanıcı parolası sıfırlama İlkesi** bölümü ve geçiş **kullanıcılar parola sıfırlama için etkin** için seçenek **Evet**.</span><span class="sxs-lookup"><span data-stu-id="4a075-117">Scroll down to the **User password reset policy** section and toggle the **Users enabled for password reset** option to **YES**.</span></span> <span data-ttu-id="4a075-118">Dikkat **alternatif e-posta adresi** seçeneğini işaretli; olduğu gibi bırakın.</span><span class="sxs-lookup"><span data-stu-id="4a075-118">Notice that the **Alternate Email Address** option is checked; leave it as it is.</span></span>
   
    ![Self servis parola sıfırlama](./media/active-directory-b2c-reference-sspr/sspr.png)
6. <span data-ttu-id="4a075-120">Sayfanın alt kısmındaki **Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4a075-120">Click **Save** at the bottom of the page.</span></span> <span data-ttu-id="4a075-121">İşiniz bittiğinde!</span><span class="sxs-lookup"><span data-stu-id="4a075-121">You're done!</span></span>

<span data-ttu-id="4a075-122">Test etmek için bir kimlik sağlayıcısı yerel hesaplarına sahip tüm oturum açma ilkesinde "Şimdi Çalıştır" özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="4a075-122">To test, use the "Run now" feature on any sign-in policy that has local accounts as an identity provider.</span></span> <span data-ttu-id="4a075-123">Yerel hesap oturum açma (burada, bir e-posta adresi ve parola veya kullanıcı adı ve parola girin) tıklatın sayfa **hesabınıza erişemiyor?** Müşteri Deneyimi doğrulanamadı.</span><span class="sxs-lookup"><span data-stu-id="4a075-123">On the local account sign-in page (where you enter an email address and password, or a username and password), click **Can't access your account?** to verify the consumer experience.</span></span>

> [!NOTE]
> <span data-ttu-id="4a075-124">Self Servis parola sıfırlama sayfalarını kullanarak özelleştirilebilir [şirket markası özelliğini](../active-directory/active-directory-add-company-branding.md).</span><span class="sxs-lookup"><span data-stu-id="4a075-124">The self-service password reset pages can be customized by using the [company branding feature](../active-directory/active-directory-add-company-branding.md).</span></span>
> 
> 

