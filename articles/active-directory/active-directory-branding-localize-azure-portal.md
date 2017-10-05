---
title: "Dile özgü şirket, oturum açma sayfasına Azure Active Directory'de markası ekleme | Microsoft Docs"
description: "Belirli bir dil şirketten eklemeyi öğrenin marka resimler ve Azure bir oturum açma sayfası metni"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a0310d6a-aaa7-4ea0-991d-6d3135b4382a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: e1fe8d855386ceec39edbc985538cdf32d78a13b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="add-language-specific-company-branding-to-your-sign-in-page-in-the-azure-active-directory"></a><span data-ttu-id="d146b-103">Dile özgü şirket, oturum açma sayfasına Azure Active Directory'de markası ekleme</span><span class="sxs-lookup"><span data-stu-id="d146b-103">Add language-specific company branding to your sign-in page in the Azure Active Directory</span></span>
<span data-ttu-id="d146b-104">Birçok şirket, karışıklığı önlemek için yönettikleri hizmetlerde ve web sitelerinde tutarlı bir genel görünüm uygulamak ister.</span><span class="sxs-lookup"><span data-stu-id="d146b-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span></span> <span data-ttu-id="d146b-105">Azure Active Directory şirket Logonuzla ve özel renk düzenleri ile oturum açma sayfasının görünümünü özelleştirmenize olanak tanıyarak bu yeteneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="d146b-105">Azure Active Directory provides this capability by allowing you to customize the appearance of the sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="d146b-106">Oturum açma sayfası, Office 365 veya Azure AD kimlik sağlayıcınız olarak kullanan diğer web tabanlı uygulamalar için oturum açtığınızda görüntülenen sayfadır.</span><span class="sxs-lookup"><span data-stu-id="d146b-106">The sign-in page is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="d146b-107">Kimlik bilgilerinizi girmek için bu sayfayı ile etkileşim.</span><span class="sxs-lookup"><span data-stu-id="d146b-107">You interact with this page to enter your credentials.</span></span>

## <a name="customizing-the-sign-in-page-for-another-language"></a><span data-ttu-id="d146b-108">Başka bir dil için oturum açma sayfasını özelleştirme</span><span class="sxs-lookup"><span data-stu-id="d146b-108">Customizing the sign-in page for another language</span></span>
<span data-ttu-id="d146b-109">Yalnızca, özel bir oturum açma sayfasında açıklandığı gibi oluşturduysanız, özel oturum açma sayfasına dile özgü öğeleri ekleyebilirsiniz [şirket markası, oturum açma sayfasına ekleme](active-directory-branding-custom-signon-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d146b-109">You can add language-specific elements to your custom sign-in page only if you have already created a custom sign-in page as described in [Add company branding to your sign-in page](active-directory-branding-custom-signon-azure-portal.md).</span></span> <span data-ttu-id="d146b-110">Dizin başına bir oturum açma sayfası özelleştirilebilir öğeler varsayılan kümesiyle yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d146b-110">You can configure one sign-in page per directory with a default set of customizable elements.</span></span> <span data-ttu-id="d146b-111">Sayfa öğeleri varsayılan kümesini yapılandırdıktan sonra farklı yerel ayarlar için daha fazla sürüm yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d146b-111">After you’ve configured the default set of page elements, you can configure more versions for different locales.</span></span> <span data-ttu-id="d146b-112">Ayrıca, çeşitli öğeleri karıştırabilir ve eşleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d146b-112">You can also mix and match various elements.</span></span> <span data-ttu-id="d146b-113">Örneğin, olabilir:</span><span class="sxs-lookup"><span data-stu-id="d146b-113">For example, you could:</span></span>

* <span data-ttu-id="d146b-114">Varsayılan oluşturma **oturum açma sayfası görüntü** tüm kültürler için ardından oluşturduğunuz belirli sürümler İngilizce ve Fransızca için.</span><span class="sxs-lookup"><span data-stu-id="d146b-114">Create a default **Sign-in page image** that works for all cultures, then create specific versions for English and French.</span></span> <span data-ttu-id="d146b-115">Tarayıcılarınızı bu iki dilden birine ayarladığınızda, varsayılan çizim için tüm diğer dillere görüntülenirken dile özgü görüntüsü görünür.</span><span class="sxs-lookup"><span data-stu-id="d146b-115">When you set your browsers to one of these two languages, the language-specific image appears, while the default illustration appears for all other languages.</span></span>
* <span data-ttu-id="d146b-116">Kuruluşunuz için farklı logolar (örneğin, Japonca veya İbranice sürümler) yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d146b-116">Configure different logos for your organization (for example, Japanese or Hebrew versions).</span></span>

<span data-ttu-id="d146b-117">Dil Varyasyon sayısını düşük bakım ve performans nedenleriyle tutmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="d146b-117">We recommend that you keep the number of language variations low, for maintenance and performance reasons.</span></span>

<span data-ttu-id="d146b-118">**Şirket markası dizininize eklemek için:**</span><span class="sxs-lookup"><span data-stu-id="d146b-118">**To add company branding to your directory:**</span></span>

1. <span data-ttu-id="d146b-119">Oturum [Azure portal](https://portal.azure.com) dizini için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="d146b-119">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="d146b-120">Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** metin kutusuna ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="d146b-120">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Açılış kullanıcı yönetimi](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. <span data-ttu-id="d146b-122">Üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **şirket markası**.</span><span class="sxs-lookup"><span data-stu-id="d146b-122">On the **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="d146b-123">Üzerinde **kullanıcılar ve gruplar - şirket markası** dikey penceresinde, select **dil eklemek** komutu.</span><span class="sxs-lookup"><span data-stu-id="d146b-123">On the **Users and groups - Company branding** blade, select the **Add language** command.</span></span>

    ![Dile özgü marka öğeleri ekleme](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. <span data-ttu-id="d146b-125">Özelleştirmek istediğiniz öğeleri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d146b-125">Modify the elements you want to customize.</span></span> <span data-ttu-id="d146b-126">Tüm öğeler isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="d146b-126">All elements are optional.</span></span>
6. <span data-ttu-id="d146b-127">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d146b-127">Click **Save**.</span></span>

<span data-ttu-id="d146b-128">Bunu görünmesi marka oturum açma sayfasına yapılan değişiklikler bir saate kadar sürebilir.</span><span class="sxs-lookup"><span data-stu-id="d146b-128">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d146b-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d146b-129">Next steps</span></span>
[<span data-ttu-id="d146b-130">Şirket, oturum açma sayfasına markası ekleme</span><span class="sxs-lookup"><span data-stu-id="d146b-130">Add company branding to your sign-in page</span></span>](active-directory-branding-custom-signon-azure-portal.md)
