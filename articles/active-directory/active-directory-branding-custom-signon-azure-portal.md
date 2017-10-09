---
title: "oturum açma işleminiz sayfa hello Azure Active Directory aaaCustomize | Microsoft Docs"
description: "Bilgi nasıl tooadd şirket markasıyla toohello Azure oturum açma sayfası"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 151521e3b9cbc6a438a589735058fbff78443cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a><span data-ttu-id="adf27-103">Şirket tooyour oturum açma sayfasında hello Azure Active Directory markası ekleme</span><span class="sxs-lookup"><span data-stu-id="adf27-103">Add company branding tooyour sign-in page in hello Azure Active Directory</span></span>
<span data-ttu-id="adf27-104">tooavoid Karışıklığı önlemek için birçok şirket tüm hello Web siteleri ve yönettikleri hizmetlerde tooapply tutarlı bir görünüm istiyor.</span><span class="sxs-lookup"><span data-stu-id="adf27-104">tooavoid confusion, many companies want tooapply a consistent look and feel across all hello websites and services they manage.</span></span> <span data-ttu-id="adf27-105">Azure Active Directory toocustomize hello hello oturum açma sayfası şirket Logonuzla ve özel renk düzenleri görünümünü sağlayarak bu yeteneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="adf27-105">Azure Active Directory provides this capability by allowing you toocustomize hello appearance of hello sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="adf27-106">Merhaba oturum açma sayfası 365 veya Azure AD kimlik sağlayıcınız olarak kullanan diğer web tabanlı uygulamalar tooOffice içinde oturum açtığınızda görüntülenen hello sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="adf27-106">hello sign-in page is hello page that appears when you sign in tooOffice 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="adf27-107">Kimlik bilgilerinizi bu sayfayı tooenter ile etkileşim.</span><span class="sxs-lookup"><span data-stu-id="adf27-107">You interact with this page tooenter your credentials.</span></span>

<span data-ttu-id="adf27-108">Şirketinizin markasını, renklerini ve diğer özelleştirilebilir öğelerini bu sayfadaki tooshow istiyorsanız, hello iki deneyim arasındaki görüntüleri toounderstand hello fark aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="adf27-108">If you want tooshow your company brand, colors and other customizable elements on this page, see hello following images toounderstand hello difference between hello two experiences.</span></span>

<span data-ttu-id="adf27-109">Merhaba ekran gösterir ve örnek hello Office 365 oturum açma sayfasında bir masaüstü bilgisayar için aşağıdaki **önce** bir özelleştirme:</span><span class="sxs-lookup"><span data-stu-id="adf27-109">hello following screenshot shows and example for hello Office 365 sign-in page on a desktop computer **before** a customization:</span></span>

![Özelleştirmeden önce Office 365 oturum açma sayfası](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

<span data-ttu-id="adf27-111">Merhaba ekran gösterir ve örnek hello Office 365 oturum açma sayfasında bir masaüstü bilgisayar için aşağıdaki **sonra** bir özelleştirme:</span><span class="sxs-lookup"><span data-stu-id="adf27-111">hello following screenshot shows and example for hello Office 365 sign-in page on a desktop computer **after** a customization:</span></span>

![Özelleştirmeden sonra Office 365 oturum açma sayfası](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-hello-sign-in-page"></a><span data-ttu-id="adf27-113">Merhaba oturum açma sayfasını özelleştirme</span><span class="sxs-lookup"><span data-stu-id="adf27-113">Customizing hello sign-in page</span></span>
<span data-ttu-id="adf27-114">Genellikle, tarayıcı tabanlı erişim tooyour bulut uygulamalarınıza ve kuruluşunuzun abonesi olduğu hizmetlere gerekiyorsa, hello oturum açma sayfasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="adf27-114">Typically, if you need browser-based access tooyour cloud apps and services that your organization subscribes to, you use hello sign-in page.</span></span>

<span data-ttu-id="adf27-115">Değişiklikleri tooyour oturum açma sayfası uyguladıysanız, tooan saat hello değişiklikleri tooappear için yukarı alabilir.</span><span class="sxs-lookup"><span data-stu-id="adf27-115">If you have applied changes tooyour sign-in page, it can take up tooan hour for hello changes tooappear.</span></span>

<span data-ttu-id="adf27-116">Bir hizmeti, https://outlook.com/**contoso**.com veya https://mail.**contoso**.com gibi yalnızca kiracıya özgü bir URL ile ziyaret ettiğinizde markalı oturum açma sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="adf27-116">A branded sign-in page only appears when you visit a service with a tenant-specific URL such as https://outlook.com/**contoso**.com, or https://mail.**contoso**.com.</span></span>

<span data-ttu-id="adf27-117">Hizmeti https://mail.office365.com gibi kiracıya özgü olmayan bir URL ile ziyaret ederseniz markasız oturum açma sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="adf27-117">When you visit a service with non-tenant specific URLs (e.g.: https://mail.office365.com), a non-branded sign-in page appears.</span></span> <span data-ttu-id="adf27-118">Bu durumda markanız, kullanıcı kimliğinizi girdiğinizde veya kullanıcı kutucuğunu seçtiğinizde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="adf27-118">in this case, your branding appears once you have entered your user ID or you have selected a user tile.</span></span>

> [!NOTE]
> * <span data-ttu-id="adf27-119">Etki alanı adınızı hello "Etkin" olarak görünmesi gereken **etki alanları** kısmı hello yapılandırılmış markalama Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="adf27-119">Your domain name must appear as “Active" in hello **Domains** portion of hello Azure portal in which you have configured branding.</span></span> <span data-ttu-id="adf27-120">Daha fazla bilgi için bkz: [özel etki alanı adlarını Ekle](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="adf27-120">For more information, see [Add custom domain names](active-directory-domains-add-azure-portal.md).</span></span>
> * <span data-ttu-id="adf27-121">Oturum açma sayfası markalama toohello tüketici oturum açma sayfasına Microsoft üzerinden taşımak değil.</span><span class="sxs-lookup"><span data-stu-id="adf27-121">Sign-in page branding doesn’t carry over toohello consumer sign in page of Microsoft.</span></span> <span data-ttu-id="adf27-122">Bir Microsoft hesabıyla oturum açarsanız Azure AD tarafından işlenen kullanıcı kutucuklarının markalı bir listesini görebilirsiniz ancak kuruluşunuzun hello markası toohello Microsoft hesabı oturum açma sayfasına uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="adf27-122">If you sign in with a Microsoft account, you may see a branded list of user tiles rendered by Azure AD, but hello branding of your organization does not apply toohello Microsoft account sign-in page.</span></span>
>
>

<span data-ttu-id="adf27-123">Oturum açma sayfanızda hello **Oturumumu açık bırak** onay kutusunu kapatın ve yeniden tarayıcısında açın açtığınız kullanıcı tooremain sağlar.</span><span class="sxs-lookup"><span data-stu-id="adf27-123">On your sign-in page, hello **Keep me signed in** checkbox allows a user tooremain signed in when they close and re-open their browser.</span></span>

   ![Oturumum açık kalsın](./media/active-directory-branding-custom-signon-azure-portal/01.png)

<span data-ttu-id="adf27-125">Bu durum oturum ömrünü etkilemez.</span><span class="sxs-lookup"><span data-stu-id="adf27-125">It does not effect session lifetime.</span></span> <span data-ttu-id="adf27-126">Oturum açma hello Azure Active Directory sayfasında hello onay kutusunu gizleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="adf27-126">You can hide hello checkbox on hello Azure Active Directory sign-in page.</span></span>
<span data-ttu-id="adf27-127">Merhaba onay kutusu görüntülenip görüntülenmeyeceğini, hello ayarına bağlıdır **Oturumumu devre dışı açık tutmak**.</span><span class="sxs-lookup"><span data-stu-id="adf27-127">Whether hello checkbox is displayed depends on hello setting of **Keep me signed in disabled**.</span></span>

   ![Oturumum açık kalsın](./media/active-directory-branding-custom-signon-azure-portal/02.png)

<span data-ttu-id="adf27-129">toohide onay kutusunu Merhaba, bu çok ayarını yapılandırmak**Evet**.</span><span class="sxs-lookup"><span data-stu-id="adf27-129">toohide hello checkbox, configure this setting too**Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="adf27-130">Bu kutu mümkün toocheck olan kullanıcılar SharePoint Online ve Office 2010 bazı özelliklerine bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="adf27-130">Some features of SharePoint Online and Office 2010 depend on users being able toocheck this box.</span></span> <span data-ttu-id="adf27-131">Bu ayar toohidden yapılandırırsanız, kullanıcılarınızın ek ve beklenmeyen komut istemlerini toosign de görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="adf27-131">If you configure this setting toohidden, your users may see additional and unexpected prompts toosign-in.</span></span>
>
>

<span data-ttu-id="adf27-132">**tooadd şirket markasıyla tooyour dizini:**</span><span class="sxs-lookup"><span data-stu-id="adf27-132">**tooadd company branding tooyour directory:**</span></span>

1. <span data-ttu-id="adf27-133">İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="adf27-133">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="adf27-134">Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** hello metin kutusuna ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="adf27-134">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Açılış kullanıcı yönetimi](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. <span data-ttu-id="adf27-136">Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **şirket markası**.</span><span class="sxs-lookup"><span data-stu-id="adf27-136">On hello **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="adf27-137">Merhaba üzerinde **kullanıcılar ve gruplar - şirket markası** dikey penceresinde, select hello **Düzenle** komutu.</span><span class="sxs-lookup"><span data-stu-id="adf27-137">On hello **Users and groups - Company branding** blade, select hello **Edit** command.</span></span>

    ![Özel marka Düzenle](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. <span data-ttu-id="adf27-139">Toocustomize istediğiniz hello öğeleri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="adf27-139">Modify hello elements you want toocustomize.</span></span> <span data-ttu-id="adf27-140">Tüm öğeler isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="adf27-140">All elements are optional.</span></span>
6. <span data-ttu-id="adf27-141">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="adf27-141">Click **Save**.</span></span>

<span data-ttu-id="adf27-142">Oturum açma toohello yapılan değişiklikler marka tooappear sayfa için tooan saat sürebilir.</span><span class="sxs-lookup"><span data-stu-id="adf27-142">It can take up tooan hour for any changes you made toohello sign-in page branding tooappear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="adf27-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="adf27-143">Next steps</span></span>
[<span data-ttu-id="adf27-144">Dile özgü şirket markası ekleme</span><span class="sxs-lookup"><span data-stu-id="adf27-144">Add language-specific company branding</span></span>](active-directory-branding-localize-azure-portal.md)
