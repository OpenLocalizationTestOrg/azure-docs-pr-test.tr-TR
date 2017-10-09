---
title: "Azure Active Directory B2C: Twitter yapılandırma | Microsoft Docs"
description: "Uygulamalarınızda Azure Active Directory B2C tarafından güvenliği sağlanan Twitter hesaplarıyla kaydolma ve oturum açma tooconsumers sağlar."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 579a6841-9329-45b8-a351-da4315a6634e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/06/2017
ms.author: parakhj
ms.openlocfilehash: 275c5c73fd5e8e5075e77fee942cbc1b5e1586cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-twitter-accounts"></a><span data-ttu-id="fb332-103">Azure Active Directory B2C: Kaydolma ve oturum açma tooconsumers Twitter hesaplarıyla sağlayın.</span><span class="sxs-lookup"><span data-stu-id="fb332-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Twitter accounts</span></span>

> [!NOTE]
> <span data-ttu-id="fb332-104">Bu özelliğin önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="fb332-104">This feature is in preview.</span></span>
> 

## <a name="create-a-twitter-application"></a><span data-ttu-id="fb332-105">Bir Twitter uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="fb332-105">Create a Twitter application</span></span>
<span data-ttu-id="fb332-106">toouse Twitter kimlik sağlayıcısı Azure Active Directory (Azure AD) B2C içinde hello doğru parametrelerle sağlayın ve toocreate bir Twitter uygulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fb332-106">toouse Twitter as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Twitter application and supply it with hello right parameters.</span></span> <span data-ttu-id="fb332-107">Bu bir Twitter Geliştirici hesabı toodo gerekir.</span><span class="sxs-lookup"><span data-stu-id="fb332-107">You need a Twitter developer account toodo this.</span></span> <span data-ttu-id="fb332-108">Bir sahip değilseniz, yerinde edinebilirsiniz [https://dev.twitter.com/](https://dev.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="fb332-108">If you don’t have one, you can get it at [https://dev.twitter.com/](https://dev.twitter.com/).</span></span>

1. <span data-ttu-id="fb332-109">Toohello Git [Geliştirici Web sitesi Twitter](https://dev.twitter.com/) ve kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="fb332-109">Go toohello [Twitter developer's website](https://dev.twitter.com/) and sign in with your credentials.</span></span>
2. <span data-ttu-id="fb332-110">Tıklatın **uygulamalarım** altında **araçları ve Destek** ve ardından **yeni uygulama oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="fb332-110">Click **My apps** under **Tools & Support** and then click **Create New App**.</span></span> 
3. <span data-ttu-id="fb332-111">Merhaba biçiminde hello için bir değer sağlayın **adı**, **açıklama**, ve **Web sitesi**.</span><span class="sxs-lookup"><span data-stu-id="fb332-111">In hello form, provide a value for hello **Name**, **Description**, and **Website**.</span></span>
4. <span data-ttu-id="fb332-112">Hello için **geri çağırma URL'si**, girin `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="fb332-112">For hello **Callback URL**, enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span></span> <span data-ttu-id="fb332-113">Emin tooreplace olun **{tenant}** , kiracının adlı (örneğin, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="fb332-113">Make sure tooreplace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
5. <span data-ttu-id="fb332-114">Merhaba kutusunu tooagree toohello denetleyin **Geliştirici anlaşma** tıklatıp **Twitter uygulamanızı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="fb332-114">Check hello box tooagree toohello **Developer Agreement** and click **Create your Twitter application**.</span></span>
6. <span data-ttu-id="fb332-115">Merhaba uygulama oluşturulduktan sonra tıklatın **anahtarları ve erişim belirteçleri**.</span><span class="sxs-lookup"><span data-stu-id="fb332-115">Once hello app is created, click **Keys and Access Tokens**.</span></span>
7. <span data-ttu-id="fb332-116">Merhaba değerini kopyalayın **tüketici anahtarı** ve **tüketici gizli**.</span><span class="sxs-lookup"><span data-stu-id="fb332-116">Copy hello value of **Consumer Key** and **Consumer Secret**.</span></span> <span data-ttu-id="fb332-117">Bunların her ikisi gerekir tooconfigure Twitter kiracınızda kimlik sağlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="fb332-117">You will need both of them tooconfigure Twitter as an identity provider in your tenant.</span></span>

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="fb332-118">Twitter kimlik sağlayıcısı kiracınızda yapılandırın</span><span class="sxs-lookup"><span data-stu-id="fb332-118">Configure Twitter as an identity provider in your tenant</span></span>
1. <span data-ttu-id="fb332-119">Bu adımları çok[toohello B2C özellikleri dikey penceresine gidin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure portalı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="fb332-119">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="fb332-120">Merhaba B2C özellikleri dikey penceresinde **kimlik sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="fb332-120">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="fb332-121">Tıklatın **+ Ekle** hello dikey penceresinde hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="fb332-121">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="fb332-122">Kolay bir sağlamak **adı** hello kimlik sağlayıcı yapılandırması için.</span><span class="sxs-lookup"><span data-stu-id="fb332-122">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="fb332-123">Örneğin, "Twitter" girin.</span><span class="sxs-lookup"><span data-stu-id="fb332-123">For example, enter "Twitter".</span></span>
5. <span data-ttu-id="fb332-124">Tıklatın **kimlik sağlayıcısı türü**seçin **Twitter**, tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="fb332-124">Click **Identity provider type**, select **Twitter**, and click **OK**.</span></span>
6. <span data-ttu-id="fb332-125">Tıklatın **bu kimlik sağlayıcısı'nı ayarlama** ve hello Twitter girin **tüketici anahtarı** hello için **istemci kimliği** ve Twitter hello **tüketici gizli**hello için **gizli**.</span><span class="sxs-lookup"><span data-stu-id="fb332-125">Click **Set up this identity provider** and enter hello Twitter **Consumer Key** for hello **Client id** and hello Twitter **Consumer Secret** for hello **Client secret**.</span></span>
7. <span data-ttu-id="fb332-126">Tıklatın **Tamam**ve ardından **oluşturma** toosave Twitter yapılandırmanızı.</span><span class="sxs-lookup"><span data-stu-id="fb332-126">Click **OK**, and then click **Create** toosave your Twitter configuration.</span></span>

