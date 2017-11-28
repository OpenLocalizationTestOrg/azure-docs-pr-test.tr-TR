---
title: "Azure Active Directory B2C: Özel öznitelikleri | Microsoft Docs"
description: "Tüketicileriniz hakkında bilgi toplamak için Azure Active Directory B2C'de özel öznitelikleri kullanma"
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
ms.openlocfilehash: 356aaeff3a78fc7b682d621e8e0de9312582b2fe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-to-collect-information-about-your-consumers"></a><span data-ttu-id="7c911-103">Azure Active Directory B2C: tüketicileriniz hakkında bilgi toplamak için özel öznitelikler kullanın.</span><span class="sxs-lookup"><span data-stu-id="7c911-103">Azure Active Directory B2C: Use custom attributes to collect information about your consumers</span></span>
<span data-ttu-id="7c911-104">Azure Active Directory (Azure AD) B2C dizininize bilgi (öznitelikler) yerleşik bir dizi birlikte gelir: verilen ad, Soyadı, şehir, posta kodu ve diğer öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="7c911-104">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of information (attributes): Given Name, Surname, City, Postal Code, and other attributes.</span></span> <span data-ttu-id="7c911-105">Bununla birlikte, her tüketiciye yönelik uygulama tüketici toplamak için benzersiz gereksinimleri ne öznitelikleri üzerinde vardır.</span><span class="sxs-lookup"><span data-stu-id="7c911-105">However, every consumer-facing application has unique requirements on what attributes to gather from consumers.</span></span> <span data-ttu-id="7c911-106">Azure AD B2C ile her tüketici hesapta depolanan öznitelikler kümesi genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c911-106">With Azure AD B2C, you can extend the set of attributes stored on each consumer account.</span></span> <span data-ttu-id="7c911-107">Özel öznitelikler oluşturabileceğiniz [Azure portal](https://portal.azure.com/) ve aşağıda gösterildiği gibi kaydolma ilkelerinizi kullanın.</span><span class="sxs-lookup"><span data-stu-id="7c911-107">You can create custom attributes on the [Azure portal](https://portal.azure.com/) and use it in your sign-up policies, as shown below.</span></span> <span data-ttu-id="7c911-108">Aynı zamanda okuma ve yazma bu öznitelikleri kullanarak [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="7c911-108">You can also read and write these attributes by using the [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7c911-109">Özel öznitelikler kullanın [Azure AD Graph API Directory şema uzantıları](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span><span class="sxs-lookup"><span data-stu-id="7c911-109">Custom attributes use [Azure AD Graph API Directory Schema Extensions](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span></span>
> 
> 

## <a name="create-a-custom-attribute"></a><span data-ttu-id="7c911-110">Özel bir öznitelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c911-110">Create a custom attribute</span></span>
1. <span data-ttu-id="7c911-111">[Azure portalındaki B2C özellikleri dikey penceresine gitmek için aşağıdaki adımları izleyin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="7c911-111">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="7c911-112">Tıklatın **kullanıcı öznitelikleri**.</span><span class="sxs-lookup"><span data-stu-id="7c911-112">Click **User attributes**.</span></span>
3. <span data-ttu-id="7c911-113">Dikey pencerenin en üstündeki **+Add (+Ekle)** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c911-113">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="7c911-114">Sağlayan bir **adı** özel öznitelik (örneğin, "ShoeSize") ve isteğe bağlı olarak bir **açıklama**.</span><span class="sxs-lookup"><span data-stu-id="7c911-114">Provide a **Name** for the custom attribute (for example, "ShoeSize") and optionally, a **Description**.</span></span> <span data-ttu-id="7c911-115">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c911-115">Click **Create**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7c911-116">Yalnızca "dize" **veri türü** şu anda kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="7c911-116">Only the "String" **Data Type** is currently available.</span></span>
   > 
   > 

<span data-ttu-id="7c911-117">Özel öznitelik listesinde kullanılabilir **kullanıcı öznitelikleri**ve kaydolma ilkelerinizi kullanmak için.</span><span class="sxs-lookup"><span data-stu-id="7c911-117">The custom attribute is now available in the list of **User attributes**, and for use in your sign-up policies.</span></span>

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a><span data-ttu-id="7c911-118">Kaydolma ilkenizde özel bir öznitelik kullanın</span><span class="sxs-lookup"><span data-stu-id="7c911-118">Use a custom attribute in your sign-up policy</span></span>
1. <span data-ttu-id="7c911-119">[Azure portalındaki B2C özellikleri dikey penceresine gitmek için aşağıdaki adımları izleyin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="7c911-119">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="7c911-120">**Kaydolma ilkeleri**’ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c911-120">Click **Sign-up policies**.</span></span>
3. <span data-ttu-id="7c911-121">Açmak için kayıt ilkesi (örneğin, "B2C_1_SiUp") tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c911-121">Click your sign-up policy (for example, "B2C_1_SiUp") to open it.</span></span> <span data-ttu-id="7c911-122">Tıklatın **Düzenle** dikey pencerenin üstündeki.</span><span class="sxs-lookup"><span data-stu-id="7c911-122">Click **Edit** at the top of the blade.</span></span>
4. <span data-ttu-id="7c911-123">Tıklatın **kaydolma özniteliklerini** ve özel öznitelik (örneğin, "ShoeSize") seçin.</span><span class="sxs-lookup"><span data-stu-id="7c911-123">Click **Sign-up attributes** and select the custom attribute (for example, "ShoeSize").</span></span> <span data-ttu-id="7c911-124">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c911-124">Click **OK**.</span></span>
5. <span data-ttu-id="7c911-125">Tıklatın **uygulama talepleri** ve özel özniteliği seçin.</span><span class="sxs-lookup"><span data-stu-id="7c911-125">Click **Application claims** and select the custom attribute.</span></span> <span data-ttu-id="7c911-126">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c911-126">Click **OK**.</span></span>
6. <span data-ttu-id="7c911-127">Tıklatın **kaydetmek** dikey pencerenin üstündeki.</span><span class="sxs-lookup"><span data-stu-id="7c911-127">Click **Save** at the top of the blade.</span></span>

<span data-ttu-id="7c911-128">Müşteri Deneyimi doğrulamak için ilkeyi "Şimdi Çalıştır" özelliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c911-128">You can use the "Run now" feature on the policy to verify the consumer experience.</span></span> <span data-ttu-id="7c911-129">Şimdi "ShoeSize" tüketici kaydolma sırasında toplanan özniteliklerinin listesini görmek ve uygulamanıza geri gönderilen belirteçte bkz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c911-129">You should now see "ShoeSize" in the list of attributes collected during consumer sign-up, and see it in the token sent back to your application.</span></span>

## <a name="notes"></a><span data-ttu-id="7c911-130">Notlar</span><span class="sxs-lookup"><span data-stu-id="7c911-130">Notes</span></span>
* <span data-ttu-id="7c911-131">Kayıt ilkeleri ile birlikte özel öznitelikler de oturum açma veya kaydolma ilkeleri ve profil düzenleme ilkeleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7c911-131">Along with sign-up policies, custom attributes can also be used in sign-up or sign-in policies and profile editing policies.</span></span>
* <span data-ttu-id="7c911-132">Özel özniteliklerin bilinen bir sınırlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="7c911-132">There is a known limitation of custom attributes.</span></span> <span data-ttu-id="7c911-133">Yalnızca ilk defa herhangi bir ilkede kullanıldığında oluşturulan ve listesine değil eklendiğinde olan **kullanıcı öznitelikleri**.</span><span class="sxs-lookup"><span data-stu-id="7c911-133">It is only created the first time it is used in any policy, and not when you add it to the list of **User attributes**.</span></span>

