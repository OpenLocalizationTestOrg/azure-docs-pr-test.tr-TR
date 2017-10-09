---
title: "Azure Active Directory B2C: Özel öznitelikleri | Microsoft Docs"
description: "Nasıl tüketicileriniz hakkında Azure Active Directory B2C toocollect bilgi toouse özel öznitelikler"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 055ffb0a-197b-4716-8dad-1fd8a01e174f
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: fb1bff77ad54c246c6d2f69f39c03eafb76fe6bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-toocollect-information-about-your-consumers"></a><span data-ttu-id="e5667-103">Azure Active Directory B2C: tüketicileriniz hakkında özel öznitelikler toocollect bilgileri kullanın</span><span class="sxs-lookup"><span data-stu-id="e5667-103">Azure Active Directory B2C: Use custom attributes toocollect information about your consumers</span></span>
<span data-ttu-id="e5667-104">Azure Active Directory (Azure AD) B2C dizininize bilgi (öznitelikler) yerleşik bir dizi birlikte gelir: verilen ad, Soyadı, şehir, posta kodu ve diğer öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="e5667-104">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of information (attributes): Given Name, Surname, City, Postal Code, and other attributes.</span></span> <span data-ttu-id="e5667-105">Bununla birlikte, her tüketiciye yönelik uygulama hangi özniteliklerin toogather tüketicileri gelen üzerinde benzersiz gereksinimleri vardır.</span><span class="sxs-lookup"><span data-stu-id="e5667-105">However, every consumer-facing application has unique requirements on what attributes toogather from consumers.</span></span> <span data-ttu-id="e5667-106">Azure AD B2C ile her tüketici hesapta depolanan öznitelikler hello kümesi genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5667-106">With Azure AD B2C, you can extend hello set of attributes stored on each consumer account.</span></span> <span data-ttu-id="e5667-107">Özel öznitelikler üzerinde hello oluşturabilirsiniz [Azure portal](https://portal.azure.com/) ve aşağıda gösterildiği gibi kaydolma ilkelerinizi kullanın.</span><span class="sxs-lookup"><span data-stu-id="e5667-107">You can create custom attributes on hello [Azure portal](https://portal.azure.com/) and use it in your sign-up policies, as shown below.</span></span> <span data-ttu-id="e5667-108">Aynı zamanda okuma ve hello kullanarak bu öznitelikler yazma [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="e5667-108">You can also read and write these attributes by using hello [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e5667-109">Özel öznitelikler kullanın [Azure AD Graph API Directory şema uzantıları](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span><span class="sxs-lookup"><span data-stu-id="e5667-109">Custom attributes use [Azure AD Graph API Directory Schema Extensions](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span></span>
> 
> 

## <a name="create-a-custom-attribute"></a><span data-ttu-id="e5667-110">Özel bir öznitelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="e5667-110">Create a custom attribute</span></span>
1. <span data-ttu-id="e5667-111">[Bu adımları toonavigate toohello B2C özellikleri dikey hello Azure portalı üzerinde izleyin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="e5667-111">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="e5667-112">Tıklatın **kullanıcı öznitelikleri**.</span><span class="sxs-lookup"><span data-stu-id="e5667-112">Click **User attributes**.</span></span>
3. <span data-ttu-id="e5667-113">Tıklatın **+ Ekle** hello dikey penceresinde hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="e5667-113">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="e5667-114">Sağlayan bir **adı** hello özel öznitelik (örneğin, "ShoeSize") ve isteğe bağlı olarak bir **açıklama**.</span><span class="sxs-lookup"><span data-stu-id="e5667-114">Provide a **Name** for hello custom attribute (for example, "ShoeSize") and optionally, a **Description**.</span></span> <span data-ttu-id="e5667-115">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e5667-115">Click **Create**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e5667-116">Yalnızca "Dize" Merhaba **veri türü** şu anda kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="e5667-116">Only hello "String" **Data Type** is currently available.</span></span>
   > 
   > 

<span data-ttu-id="e5667-117">Merhaba özel öznitelik hello listesinde yayımlamıştır **kullanıcı öznitelikleri**ve kaydolma ilkelerinizi kullanmak için.</span><span class="sxs-lookup"><span data-stu-id="e5667-117">hello custom attribute is now available in hello list of **User attributes**, and for use in your sign-up policies.</span></span>

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a><span data-ttu-id="e5667-118">Kaydolma ilkenizde özel bir öznitelik kullanın</span><span class="sxs-lookup"><span data-stu-id="e5667-118">Use a custom attribute in your sign-up policy</span></span>
1. <span data-ttu-id="e5667-119">[Bu adımları toonavigate toohello B2C özellikleri dikey hello Azure portalı üzerinde izleyin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="e5667-119">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="e5667-120">**Kaydolma ilkeleri**’ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e5667-120">Click **Sign-up policies**.</span></span>
3. <span data-ttu-id="e5667-121">Kayıt İlkesi (örneğin, "B2C_1_SiUp") tooopen'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e5667-121">Click your sign-up policy (for example, "B2C_1_SiUp") tooopen it.</span></span> <span data-ttu-id="e5667-122">Tıklatın **Düzenle** hello dikey penceresinde hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="e5667-122">Click **Edit** at hello top of hello blade.</span></span>
4. <span data-ttu-id="e5667-123">Tıklatın **kaydolma özniteliklerini** ve select hello özel öznitelik (örneğin, "ShoeSize").</span><span class="sxs-lookup"><span data-stu-id="e5667-123">Click **Sign-up attributes** and select hello custom attribute (for example, "ShoeSize").</span></span> <span data-ttu-id="e5667-124">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e5667-124">Click **OK**.</span></span>
5. <span data-ttu-id="e5667-125">Tıklatın **uygulama talepleri** ve select hello özel öznitelik.</span><span class="sxs-lookup"><span data-stu-id="e5667-125">Click **Application claims** and select hello custom attribute.</span></span> <span data-ttu-id="e5667-126">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e5667-126">Click **OK**.</span></span>
6. <span data-ttu-id="e5667-127">Tıklatın **kaydetmek** hello dikey penceresinde hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="e5667-127">Click **Save** at hello top of hello blade.</span></span>

<span data-ttu-id="e5667-128">Hello İlkesi tooverify hello tüketici deneyimi hello "Şimdi Çalıştır" özelliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5667-128">You can use hello "Run now" feature on hello policy tooverify hello consumer experience.</span></span> <span data-ttu-id="e5667-129">Şimdi "ShoeSize" Merhaba tüketici kaydolma sırasında toplanan özniteliklerinin listesini görmek ve hello belirteci gönderilen geri tooyour uygulamasındaki bakınız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5667-129">You should now see "ShoeSize" in hello list of attributes collected during consumer sign-up, and see it in hello token sent back tooyour application.</span></span>

## <a name="notes"></a><span data-ttu-id="e5667-130">Notlar</span><span class="sxs-lookup"><span data-stu-id="e5667-130">Notes</span></span>
* <span data-ttu-id="e5667-131">Kayıt ilkeleri ile birlikte özel öznitelikler de oturum açma veya kaydolma ilkeleri ve profil düzenleme ilkeleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e5667-131">Along with sign-up policies, custom attributes can also be used in sign-up or sign-in policies and profile editing policies.</span></span>
* <span data-ttu-id="e5667-132">Özel özniteliklerin bilinen bir sınırlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="e5667-132">There is a known limitation of custom attributes.</span></span> <span data-ttu-id="e5667-133">Yalnızca hello kullanıldığı ilk kez herhangi bir ilkede oluşturulan ve toohello listesini değil eklendiğinde olan **kullanıcı öznitelikleri**.</span><span class="sxs-lookup"><span data-stu-id="e5667-133">It is only created hello first time it is used in any policy, and not when you add it toohello list of **User attributes**.</span></span>

