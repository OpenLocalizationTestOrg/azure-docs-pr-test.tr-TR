---
title: "Azure AD v2.0 uç Portalı'nı kullanarak bir uygulamayı kaydetme | Microsoft Docs"
description: "Bir uygulama oturum açma etkinleştirme ve v2.0 uç noktası kullanarak Microsoft hizmetlerine erişmek için Microsoft ile kaydetme"
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: bb2f701f-3bc3-4759-94a5-8b9d53a8a0b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: e6202aa8665c906382666fe08a561421e50e0a8d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-register-an-app-with-the-v20-endpoint"></a><span data-ttu-id="d72ee-103">Bir uygulamanın v2.0 uç noktası ile kaydetme</span><span class="sxs-lookup"><span data-stu-id="d72ee-103">How to register an app with the v2.0 endpoint</span></span>
<span data-ttu-id="d72ee-104">MSA & Azure AD kabul eden bir uygulama oluşturmak için oturum açma, önce bir uygulama Microsoft ile kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d72ee-104">To build an app that accepts both MSA & Azure AD sign-in, you'll first need to register an app with Microsoft.</span></span>  <span data-ttu-id="d72ee-105">Şu anda, Azure AD ile olabilecek mevcut uygulamalardan kullanmanız mümkün olmayacaktır veya MSA - yepyeni bir tane oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d72ee-105">At this time, you won't be able to use any existing apps you may have with Azure AD or MSA - you'll need to create a brand new one.</span></span>

> [!NOTE]
> <span data-ttu-id="d72ee-106">Tüm Azure Active Directory senaryolarını ve özelliklerini v2.0 uç noktası tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="d72ee-106">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="d72ee-107">V2.0 uç kullanmanızın gerekli olup olmadığını belirlemek için okuyun [v2.0 sınırlamaları](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="d72ee-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="visit-the-microsoft-app-registration-portal"></a><span data-ttu-id="d72ee-108">Microsoft uygulama kayıt Portalı'nı ziyaret edin</span><span class="sxs-lookup"><span data-stu-id="d72ee-108">Visit the Microsoft app registration portal</span></span>
<span data-ttu-id="d72ee-109">İlk şey ilk - gidin [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span><span class="sxs-lookup"><span data-stu-id="d72ee-109">First things first - navigate to [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span></span>  <span data-ttu-id="d72ee-110">Microsoft uygulamalarınızda yönetebileceği yeni bir uygulama kayıt portalı budur.</span><span class="sxs-lookup"><span data-stu-id="d72ee-110">This is a new app registration portal where you can manage your Microsoft apps.</span></span>

<span data-ttu-id="d72ee-111">Oturum ya da kişisel oturum, iş veya Okul Microsoft hesabı.</span><span class="sxs-lookup"><span data-stu-id="d72ee-111">Sign in with either a personal or work or school Microsoft account.</span></span>  <span data-ttu-id="d72ee-112">Ya da yoksa, yeni bir kişisel hesap için kaydolun.</span><span class="sxs-lookup"><span data-stu-id="d72ee-112">If you don't have either, sign up for a new personal account.</span></span> <span data-ttu-id="d72ee-113">Şimdi, uzun sürmez - biz burada beklemeniz.</span><span class="sxs-lookup"><span data-stu-id="d72ee-113">Go ahead, it won't take long - we'll wait here.</span></span>

<span data-ttu-id="d72ee-114">Bitti mi?</span><span class="sxs-lookup"><span data-stu-id="d72ee-114">Done?</span></span> <span data-ttu-id="d72ee-115">Şimdi Microsoft uygulamaları listesi büyük olasılıkla boş olduğu aramanız.</span><span class="sxs-lookup"><span data-stu-id="d72ee-115">You should now be looking at your list of Microsoft apps, which is probably empty.</span></span>  <span data-ttu-id="d72ee-116">Değiştirelim.</span><span class="sxs-lookup"><span data-stu-id="d72ee-116">Let's change that.</span></span>

<span data-ttu-id="d72ee-117">Tıklatın **bir uygulama ekleyin**ve bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="d72ee-117">Click **Add an app**, and give it a name.</span></span>  <span data-ttu-id="d72ee-118">Portal uygulamanızı daha sonra kodunuzda kullanacağınız genel benzersiz bir uygulama kimliği atar.</span><span class="sxs-lookup"><span data-stu-id="d72ee-118">The portal will assign your app a globally unique  Application Id that you'll use later in your code.</span></span>  <span data-ttu-id="d72ee-119">Uygulamanızı bir sunucu tarafı bileşeni içeriyorsa, erişim belirteçleri için arama API'leri gerekir (düşünün: Office, Azure veya web API), oluşturmak istersiniz bir **uygulama gizli anahtarı** burada da.</span><span class="sxs-lookup"><span data-stu-id="d72ee-119">If your app includes a server-side component that needs access tokens for calling APIs (think: Office, Azure, or your own web API), you'll want to create an **Application Secret** here as well.</span></span>

<span data-ttu-id="d72ee-120">Ardından, uygulamanızı kullanacağı platformları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d72ee-120">Next, add the Platforms that your app will use.</span></span>

* <span data-ttu-id="d72ee-121">Web tabanlı uygulamalar için bir **yeniden yönlendirme URI'si** burada oturum açma iletiler gönderilemez.</span><span class="sxs-lookup"><span data-stu-id="d72ee-121">For web based apps, provide a **Redirect URI** where sign-in messages can be sent.</span></span>
* <span data-ttu-id="d72ee-122">Mobil uygulamalarda, sizin için otomatik olarak oluşturulan varsayılan yeniden yönlendirme URI'si aşağı kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d72ee-122">For mobile apps, copy down the default redirect uri automatically created for you.</span></span>

<span data-ttu-id="d72ee-123">İsteğe bağlı olarak, oturum açma sayfanızda profil bölümü görünümünü özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d72ee-123">Optionally, you can customize the look and feel of your sign-in page in the Profile section.</span></span>  <span data-ttu-id="d72ee-124">Tıklattığınızdan emin olun **kaydetmek** geçmeden önce.</span><span class="sxs-lookup"><span data-stu-id="d72ee-124">Make sure to click **Save** before moving on.</span></span>

> [!NOTE]
> <span data-ttu-id="d72ee-125">Kullanarak bir uygulama oluşturduğunuzda [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), uygulama giriş Kiracı Portalı'na imzalamak için kullandığınız hesabın içinde kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="d72ee-125">When you create an application using [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), the application will be registered in the home tenant of the account that you use to sign into the portal.</span></span>  <span data-ttu-id="d72ee-126">Bu, bir uygulamayı kişisel bir Microsoft hesabı kullanarak, Azure AD kiracınızda kaydedebilirsiniz değil, anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="d72ee-126">This means that you can not register an application in your Azure AD tenant using a personal Microsoft account.</span></span>  <span data-ttu-id="d72ee-127">Açıkça belirli bir kiracı içinde bir uygulamayı kaydetmek istiyorsanız, başlangıçta Kiracı içinde oluşturulan bir hesapla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d72ee-127">If you explicitly wish to register an application in a particular tenant, sign in with an account originally created in that tenant.</span></span>
> 
> 

## <a name="build-a-quick-start-app"></a><span data-ttu-id="d72ee-128">Hızlı Başlangıç uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="d72ee-128">Build a quick start app</span></span>
<span data-ttu-id="d72ee-129">Bir Microsoft uygulaması sahip olduğunuza göre v2.0 hızlı başlangıç öğreticilerimizden birini tamamlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d72ee-129">Now that you have a Microsoft app, you can complete one of our v2.0 quick start tutorials.</span></span>  <span data-ttu-id="d72ee-130">İşte birkaç öneri:</span><span class="sxs-lookup"><span data-stu-id="d72ee-130">Here are a few recommendations:</span></span>

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

