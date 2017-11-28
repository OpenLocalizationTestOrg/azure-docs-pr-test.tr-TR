---
title: "aaaRegister hello Azure AD v2.0 uç hello portalı kullanarak bir uygulama | Microsoft Docs"
description: "Nasıl tooregister oturum açma etkinleştirmek ve Microsoft erişmek için Microsoft ile bir uygulama hello v2.0 uç hizmetlerini kullanma"
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
ms.openlocfilehash: c56c98906656062435516e820cb318a04c03149c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooregister-an-app-with-hello-v20-endpoint"></a><span data-ttu-id="803fb-103">Nasıl tooregister hello v2.0 uç noktası ile uygulama</span><span class="sxs-lookup"><span data-stu-id="803fb-103">How tooregister an app with hello v2.0 endpoint</span></span>
<span data-ttu-id="803fb-104">toobuild MSA & Azure AD kabul eden bir uygulama oturum açma, ilk tooregister Microsoft ile bir uygulama gerekir.</span><span class="sxs-lookup"><span data-stu-id="803fb-104">toobuild an app that accepts both MSA & Azure AD sign-in, you'll first need tooregister an app with Microsoft.</span></span>  <span data-ttu-id="803fb-105">Şu anda olmaz mümkün toouse Azure AD ile olabilecek uygulamalardan mevcut olması veya MSA - toocreate marka yeni bir tane gerekir.</span><span class="sxs-lookup"><span data-stu-id="803fb-105">At this time, you won't be able toouse any existing apps you may have with Azure AD or MSA - you'll need toocreate a brand new one.</span></span>

> [!NOTE]
> <span data-ttu-id="803fb-106">Tüm Azure Active Directory senaryolarını ve özelliklerini hello v2.0 uç noktası tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="803fb-106">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="803fb-107">Merhaba v2.0 uç noktası, kullanmanız gereken varsa toodetermine okuyun hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="803fb-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="visit-hello-microsoft-app-registration-portal"></a><span data-ttu-id="803fb-108">Merhaba Microsoft uygulama kayıt portalı ziyaret edin</span><span class="sxs-lookup"><span data-stu-id="803fb-108">Visit hello Microsoft app registration portal</span></span>
<span data-ttu-id="803fb-109">İlk şey ilk - gidin çok[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span><span class="sxs-lookup"><span data-stu-id="803fb-109">First things first - navigate too[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span></span>  <span data-ttu-id="803fb-110">Microsoft uygulamalarınızda yönetebileceği yeni bir uygulama kayıt portalı budur.</span><span class="sxs-lookup"><span data-stu-id="803fb-110">This is a new app registration portal where you can manage your Microsoft apps.</span></span>

<span data-ttu-id="803fb-111">Oturum ya da kişisel oturum, iş veya Okul Microsoft hesabı.</span><span class="sxs-lookup"><span data-stu-id="803fb-111">Sign in with either a personal or work or school Microsoft account.</span></span>  <span data-ttu-id="803fb-112">Ya da yoksa, yeni bir kişisel hesap için kaydolun.</span><span class="sxs-lookup"><span data-stu-id="803fb-112">If you don't have either, sign up for a new personal account.</span></span> <span data-ttu-id="803fb-113">Şimdi, uzun sürmez - biz burada beklemeniz.</span><span class="sxs-lookup"><span data-stu-id="803fb-113">Go ahead, it won't take long - we'll wait here.</span></span>

<span data-ttu-id="803fb-114">Bitti mi?</span><span class="sxs-lookup"><span data-stu-id="803fb-114">Done?</span></span> <span data-ttu-id="803fb-115">Şimdi Microsoft uygulamaları listesi büyük olasılıkla boş olduğu aramanız.</span><span class="sxs-lookup"><span data-stu-id="803fb-115">You should now be looking at your list of Microsoft apps, which is probably empty.</span></span>  <span data-ttu-id="803fb-116">Değiştirelim.</span><span class="sxs-lookup"><span data-stu-id="803fb-116">Let's change that.</span></span>

<span data-ttu-id="803fb-117">Tıklatın **bir uygulama ekleyin**ve bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="803fb-117">Click **Add an app**, and give it a name.</span></span>  <span data-ttu-id="803fb-118">Merhaba portal uygulamanızı daha sonra kodunuzda kullanacağınız genel benzersiz bir uygulama kimliği atar.</span><span class="sxs-lookup"><span data-stu-id="803fb-118">hello portal will assign your app a globally unique  Application Id that you'll use later in your code.</span></span>  <span data-ttu-id="803fb-119">Uygulamanızı bir sunucu tarafı bileşeni içeriyorsa, erişim belirteçleri için arama API'leri gerekir (düşünün: Office, Azure veya web API), toocreate isteyeceksiniz bir **uygulama gizli anahtarı** burada da.</span><span class="sxs-lookup"><span data-stu-id="803fb-119">If your app includes a server-side component that needs access tokens for calling APIs (think: Office, Azure, or your own web API), you'll want toocreate an **Application Secret** here as well.</span></span>

<span data-ttu-id="803fb-120">Ardından, hello uygulamanızı kullanacağı platformları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="803fb-120">Next, add hello Platforms that your app will use.</span></span>

* <span data-ttu-id="803fb-121">Web tabanlı uygulamalar için bir **yeniden yönlendirme URI'si** burada oturum açma iletiler gönderilemez.</span><span class="sxs-lookup"><span data-stu-id="803fb-121">For web based apps, provide a **Redirect URI** where sign-in messages can be sent.</span></span>
* <span data-ttu-id="803fb-122">Mobil uygulamalarda, sizin için otomatik olarak oluşturulan URI hello varsayılan basılı kopya yönlendirin.</span><span class="sxs-lookup"><span data-stu-id="803fb-122">For mobile apps, copy down hello default redirect uri automatically created for you.</span></span>

<span data-ttu-id="803fb-123">İsteğe bağlı olarak, oturum açma sayfanızda hello profil bölümü hello Görünüm ve yapısını özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="803fb-123">Optionally, you can customize hello look and feel of your sign-in page in hello Profile section.</span></span>  <span data-ttu-id="803fb-124">Emin tooclick olun **kaydetmek** geçmeden önce.</span><span class="sxs-lookup"><span data-stu-id="803fb-124">Make sure tooclick **Save** before moving on.</span></span>

> [!NOTE]
> <span data-ttu-id="803fb-125">Kullanarak bir uygulama oluşturduğunuzda [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), Merhaba uygulaması kayıtlı hello ev kiracısında hello hesabının hello Portalı'na toosign kullanın.</span><span class="sxs-lookup"><span data-stu-id="803fb-125">When you create an application using [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), hello application will be registered in hello home tenant of hello account that you use toosign into hello portal.</span></span>  <span data-ttu-id="803fb-126">Bu, bir uygulamayı kişisel bir Microsoft hesabı kullanarak, Azure AD kiracınızda kaydedebilirsiniz değil, anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="803fb-126">This means that you can not register an application in your Azure AD tenant using a personal Microsoft account.</span></span>  <span data-ttu-id="803fb-127">Açıkça tooregister bir uygulama içinde belirli bir kiracı istiyorsanız, ilk Kiracı içinde oluşturulan bir hesapla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="803fb-127">If you explicitly wish tooregister an application in a particular tenant, sign in with an account originally created in that tenant.</span></span>
> 
> 

## <a name="build-a-quick-start-app"></a><span data-ttu-id="803fb-128">Hızlı Başlangıç uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="803fb-128">Build a quick start app</span></span>
<span data-ttu-id="803fb-129">Bir Microsoft uygulaması sahip olduğunuza göre v2.0 hızlı başlangıç öğreticilerimizden birini tamamlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="803fb-129">Now that you have a Microsoft app, you can complete one of our v2.0 quick start tutorials.</span></span>  <span data-ttu-id="803fb-130">İşte birkaç öneri:</span><span class="sxs-lookup"><span data-stu-id="803fb-130">Here are a few recommendations:</span></span>

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

