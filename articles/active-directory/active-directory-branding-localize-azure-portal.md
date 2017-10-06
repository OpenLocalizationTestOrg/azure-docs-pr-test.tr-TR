---
title: "hello Azure Active Directory içinde tooyour oturum açma sayfası markalama aaaAdd dile özgü şirket | Microsoft Docs"
description: "Tooadd belirli bir dil nasıl şirket markasıyla resim ve metin tooan Azure oturum açma sayfası öğrenin"
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
ms.openlocfilehash: 1e33c31abc242e8455290beb1f03760be7b9ac42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-language-specific-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a><span data-ttu-id="859ee-103">Dile özgü şirket tooyour oturum açma sayfasında hello Azure Active Directory markası ekleme</span><span class="sxs-lookup"><span data-stu-id="859ee-103">Add language-specific company branding tooyour sign-in page in hello Azure Active Directory</span></span>
<span data-ttu-id="859ee-104">tooavoid Karışıklığı önlemek için birçok şirket tüm hello Web siteleri ve yönettikleri hizmetlerde tooapply tutarlı bir görünüm istiyor.</span><span class="sxs-lookup"><span data-stu-id="859ee-104">tooavoid confusion, many companies want tooapply a consistent look and feel across all hello websites and services they manage.</span></span> <span data-ttu-id="859ee-105">Azure Active Directory toocustomize hello hello oturum açma sayfası şirket Logonuzla ve özel renk düzenleri görünümünü sağlayarak bu yeteneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="859ee-105">Azure Active Directory provides this capability by allowing you toocustomize hello appearance of hello sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="859ee-106">Merhaba oturum açma sayfası 365 veya Azure AD kimlik sağlayıcınız olarak kullanan diğer web tabanlı uygulamalar tooOffice içinde oturum açtığınızda görüntülenen hello sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="859ee-106">hello sign-in page is hello page that appears when you sign in tooOffice 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="859ee-107">Kimlik bilgilerinizi bu sayfayı tooenter ile etkileşim.</span><span class="sxs-lookup"><span data-stu-id="859ee-107">You interact with this page tooenter your credentials.</span></span>

## <a name="customizing-hello-sign-in-page-for-another-language"></a><span data-ttu-id="859ee-108">Başka bir dil için Hello oturum açma sayfasını özelleştirme</span><span class="sxs-lookup"><span data-stu-id="859ee-108">Customizing hello sign-in page for another language</span></span>
<span data-ttu-id="859ee-109">Dile özgü öğeler tooyour özel oturum açma sayfası yalnızca, özel bir oturum açma sayfasında açıklandığı gibi oluşturduysanız ekleyebilirsiniz [tooyour oturum açma sayfası markalama şirket ekleme](active-directory-branding-custom-signon-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="859ee-109">You can add language-specific elements tooyour custom sign-in page only if you have already created a custom sign-in page as described in [Add company branding tooyour sign-in page](active-directory-branding-custom-signon-azure-portal.md).</span></span> <span data-ttu-id="859ee-110">Dizin başına bir oturum açma sayfası özelleştirilebilir öğeler varsayılan kümesiyle yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="859ee-110">You can configure one sign-in page per directory with a default set of customizable elements.</span></span> <span data-ttu-id="859ee-111">Merhaba varsayılan sayfa öğeleri kümesi yapılandırdıktan sonra farklı yerel ayarlar için daha fazla sürüm yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="859ee-111">After you’ve configured hello default set of page elements, you can configure more versions for different locales.</span></span> <span data-ttu-id="859ee-112">Ayrıca, çeşitli öğeleri karıştırabilir ve eşleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="859ee-112">You can also mix and match various elements.</span></span> <span data-ttu-id="859ee-113">Örneğin, olabilir:</span><span class="sxs-lookup"><span data-stu-id="859ee-113">For example, you could:</span></span>

* <span data-ttu-id="859ee-114">Varsayılan oluşturma **oturum açma sayfası görüntü** tüm kültürler için ardından oluşturduğunuz belirli sürümler İngilizce ve Fransızca için.</span><span class="sxs-lookup"><span data-stu-id="859ee-114">Create a default **Sign-in page image** that works for all cultures, then create specific versions for English and French.</span></span> <span data-ttu-id="859ee-115">Bu iki dillerden, tarayıcılar tooone ayarladığınızda, hello varsayılan çizim için tüm diğer dillere görüntülenirken hello dile özgü görüntüsü görünür.</span><span class="sxs-lookup"><span data-stu-id="859ee-115">When you set your browsers tooone of these two languages, hello language-specific image appears, while hello default illustration appears for all other languages.</span></span>
* <span data-ttu-id="859ee-116">Kuruluşunuz için farklı logolar (örneğin, Japonca veya İbranice sürümler) yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="859ee-116">Configure different logos for your organization (for example, Japanese or Hebrew versions).</span></span>

<span data-ttu-id="859ee-117">Merhaba dil Varyasyon sayısını düşük bakım ve performans nedenleriyle tutmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="859ee-117">We recommend that you keep hello number of language variations low, for maintenance and performance reasons.</span></span>

<span data-ttu-id="859ee-118">**tooadd şirket markasıyla tooyour dizini:**</span><span class="sxs-lookup"><span data-stu-id="859ee-118">**tooadd company branding tooyour directory:**</span></span>

1. <span data-ttu-id="859ee-119">İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="859ee-119">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="859ee-120">Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** hello metin kutusuna ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="859ee-120">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Açılış kullanıcı yönetimi](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. <span data-ttu-id="859ee-122">Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **şirket markası**.</span><span class="sxs-lookup"><span data-stu-id="859ee-122">On hello **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="859ee-123">Merhaba üzerinde **kullanıcılar ve gruplar - şirket markası** dikey penceresinde, select hello **dil eklemek** komutu.</span><span class="sxs-lookup"><span data-stu-id="859ee-123">On hello **Users and groups - Company branding** blade, select hello **Add language** command.</span></span>

    ![Dile özgü marka öğeleri ekleme](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. <span data-ttu-id="859ee-125">Toocustomize istediğiniz hello öğeleri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="859ee-125">Modify hello elements you want toocustomize.</span></span> <span data-ttu-id="859ee-126">Tüm öğeler isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="859ee-126">All elements are optional.</span></span>
6. <span data-ttu-id="859ee-127">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="859ee-127">Click **Save**.</span></span>

<span data-ttu-id="859ee-128">Oturum açma toohello yapılan değişiklikler marka tooappear sayfa için tooan saat sürebilir.</span><span class="sxs-lookup"><span data-stu-id="859ee-128">It can take up tooan hour for any changes you made toohello sign-in page branding tooappear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="859ee-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="859ee-129">Next steps</span></span>
[<span data-ttu-id="859ee-130">Şirket markası tooyour oturum açma sayfası ekleme</span><span class="sxs-lookup"><span data-stu-id="859ee-130">Add company branding tooyour sign-in page</span></span>](active-directory-branding-custom-signon-azure-portal.md)
