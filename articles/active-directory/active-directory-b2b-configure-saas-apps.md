---
title: "Azure Active Directory'de SaaS uygulamaları B2B işbirliği için yapılandırma | Microsoft Docs"
description: "Azure Active Directory B2B işbirliği için PowerShell ve kod örnekleri"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 149a493f7b369415f0a2726dd6a576f0195c13d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a><span data-ttu-id="bd28b-103">SaaS uygulamaları B2B işbirliği için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bd28b-103">Configure SaaS apps for B2B collaboration</span></span>

<span data-ttu-id="bd28b-104">Azure AD ile tümleştirmek çoğu uygulamaları ile Azure Active Directory (Azure AD) B2B işbirliği çalışır.</span><span class="sxs-lookup"><span data-stu-id="bd28b-104">Azure Active Directory (Azure AD) B2B collaboration works with most apps that integrate with Azure AD.</span></span> <span data-ttu-id="bd28b-105">Bu bölümde, Azure AD B2B ile kullanmak için bazı yaygın SaaS uygulamaları yapılandırmaya yönelik yönergeler size rehberlik eder.</span><span class="sxs-lookup"><span data-stu-id="bd28b-105">In this section, we walk through instructions for configuring some popular SaaS apps for use with Azure AD B2B.</span></span>

<span data-ttu-id="bd28b-106">Uygulamaya özgü yönergeleri göz önünde bulundurmanız önce bazı kurallar altın şunlardır:</span><span class="sxs-lookup"><span data-stu-id="bd28b-106">Before you look at app-specific instructions, here are some rules of thumb:</span></span>

* <span data-ttu-id="bd28b-107">Uygulamaların çoğu için Kullanıcı Kurulumu el ile gerçekleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd28b-107">For most of the apps, user setup needs to happen manually.</span></span> <span data-ttu-id="bd28b-108">Diğer bir deyişle, kullanıcı uygulamada el ile oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd28b-108">That is, users must be created manually in the app as well.</span></span>

* <span data-ttu-id="bd28b-109">Dropbox gibi otomatik kurulum destekleyen uygulamalar için ayrı davetleri uygulamalardan oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="bd28b-109">For apps that support automatic setup, such as Dropbox, separate invitations are created from the apps.</span></span> <span data-ttu-id="bd28b-110">Kullanıcıların her daveti kabul etmek emin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd28b-110">Users must be sure to accept each invitation.</span></span>

* <span data-ttu-id="bd28b-111">Her zaman kullanıcı öznitelikleri karıştırılmış kullanıcı profili diski (UPD) Konuk kullanıcılar ile ilgili tüm sorunları hafifletmek için ayarlanmış **kullanıcı tanımlayıcısı** için **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="bd28b-111">In the user attributes, to mitigate any issues with mangled user profile disk (UPD) in guest users, always set **User Identifier** to **user.mail**.</span></span>


## <a name="dropbox-business"></a><span data-ttu-id="bd28b-112">Dropbox iş</span><span class="sxs-lookup"><span data-stu-id="bd28b-112">Dropbox Business</span></span>

<span data-ttu-id="bd28b-113">Kullanıcıların kendi kuruluş hesabını kullanarak oturum sağlamak için Dropbox Azure AD güvenlik onaylama işlemi biçimlendirme dili (SAML) kimlik sağlayıcısı kullanmak için iş el ile yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd28b-113">To enable users to sign in using their organization account, you must manually configure Dropbox Business to use Azure AD as a Security Assertion Markup Language (SAML) identity provider.</span></span> <span data-ttu-id="bd28b-114">Bunu yapmak için Dropbox iş yapılandırılmamış, bu isteyebilir veya aksi takdirde Azure AD kullanarak kullanıcıların oturum açmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="bd28b-114">If Dropbox Business has not been configured to do so, it cannot prompt or otherwise allow users to sign in using Azure AD.</span></span>

1. <span data-ttu-id="bd28b-115">Azure AD ile Dropbox iş uygulama eklemek için seçin **kurumsal uygulamalar** sol bölmesinde ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="bd28b-115">To add the Dropbox Business app into Azure AD, select **Enterprise applications** in the left pane, and then click **Add**.</span></span>

  ![Kuruluş uygulamaları sayfasında "Ekle" düğmesi](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. <span data-ttu-id="bd28b-117">İçinde **bir uygulama eklemek** penceresinde girin **dropbox** arama kutusuna ve ardından **iş için Dropbox** sonuçlar listesinde.</span><span class="sxs-lookup"><span data-stu-id="bd28b-117">In the **Add an application** window, enter **dropbox** in the search box, and then select **Dropbox for Business** in the results list.</span></span>

  ![Uygulama Sayfası Ekle "dropbox" arayın](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. <span data-ttu-id="bd28b-119">Üzerinde **çoklu oturum açma** sayfasında, **çoklu oturum açma** sol bölmede ve ardından girin **user.mail** içinde **kullanıcı tanımlayıcısı** kutusu.</span><span class="sxs-lookup"><span data-stu-id="bd28b-119">On the **Single sign-on** page, select **Single sign-on** in the left pane, and then enter **user.mail** in the **User Identifier** box.</span></span> <span data-ttu-id="bd28b-120">(Bunu UPN varsayılan olarak ayarlanır.)</span><span class="sxs-lookup"><span data-stu-id="bd28b-120">(It's set as UPN by default.)</span></span>

  ![Uygulama için çoklu oturum açmayı yapılandırma](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. <span data-ttu-id="bd28b-122">Dropbox yapılandırması için kullanılacak sertifikayı yüklemek üzere seçin **yapılandırma DropBox**ve ardından **SAML çoklu oturum üzerinde hizmet URL'si** listesinde.</span><span class="sxs-lookup"><span data-stu-id="bd28b-122">To download the certificate to use for Dropbox configuration, select **Configure DropBox**, and then select **SAML Single Sign On Service URL** in the list.</span></span>

  ![Dropbox yapılandırması için sertifika indirme](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. <span data-ttu-id="bd28b-124">Oturum açtığınızda Dropbox oturum açma URL'si ile **çoklu oturum açma** sayfası.</span><span class="sxs-lookup"><span data-stu-id="bd28b-124">Sign in to Dropbox with the sign-on URL from the **Single sign-on** page.</span></span>

  ![Dropbox oturum açma sayfası](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. <span data-ttu-id="bd28b-126">Menüsünde seçin **Yönetici Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="bd28b-126">On the menu, select **Admin Console**.</span></span>

  ![Dropbox menüsünde "Yönetici Konsolu" bağlantısı](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. <span data-ttu-id="bd28b-128">İçinde **kimlik doğrulaması** iletişim kutusunda **daha fazla**, sertifikayı karşıya yüklemek ve ardından **URL'de oturum** kutusuna, SAML çoklu oturum açma URL'si girin.</span><span class="sxs-lookup"><span data-stu-id="bd28b-128">In the **Authentication** dialog box, select **More**, upload the certificate and then, in the **Sign in URL** box, enter the SAML single sign-on URL.</span></span>

  ![Daraltılmış kimlik doğrulama iletişim kutusunda "Daha fazla" bağlantı](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  !["Oturum URL'de" genişletilmiş kimlik doğrulama iletişim kutusunda](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. <span data-ttu-id="bd28b-131">Otomatik kullanıcı kurulum Azure portalında yapılandırmak için seçin **sağlama** sol bölmesinde seçin **otomatik** içinde **sağlama modu** kutusuna ve ardından **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="bd28b-131">To configure automatic user setup in the Azure portal, select **Provisioning** in the left pane, select **Automatic** in the **Provisioning Mode** box, and then select **Authorize**.</span></span>

  ![Azure portalında otomatik kullanıcı sağlamayı yapılandırma](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

<span data-ttu-id="bd28b-133">Konuk veya üye kullanıcı Dropbox uygulamada ayarlanan sonra Dropbox'tan ayrı bir davet alırsınız.</span><span class="sxs-lookup"><span data-stu-id="bd28b-133">After guest or member users have been set up in the Dropbox app, they receive a separate invitation from Dropbox.</span></span> <span data-ttu-id="bd28b-134">Dropbox çoklu oturum açma kullanmak için davetlilerin daveti bir bağlantıya tıklayarak kabul etmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="bd28b-134">To use Dropbox single sign-on, invitees must accept the invitation by clicking a link in it.</span></span>

## <a name="box"></a><span data-ttu-id="bd28b-135">Box</span><span class="sxs-lookup"><span data-stu-id="bd28b-135">Box</span></span>
<span data-ttu-id="bd28b-136">SAML protokolünü temel Federasyon kullanarak Azure AD hesabıyla kutusunu konuk kullanıcıların kimliklerini doğrulamak kullanıcıların sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd28b-136">You can enable users to authenticate Box guest users with their Azure AD account by using federation that's based on the SAML protocol.</span></span> <span data-ttu-id="bd28b-137">Bu yordamda, meta veriler için Box.com yükleyin.</span><span class="sxs-lookup"><span data-stu-id="bd28b-137">In this procedure, you upload metadata to Box.com.</span></span>

1. <span data-ttu-id="bd28b-138">Box uygulamasına Kurumsal uygulamalardan ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bd28b-138">Add the Box app from the enterprise apps.</span></span>

2. <span data-ttu-id="bd28b-139">Çoklu oturum açma şu sırayla yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="bd28b-139">Configure single sign-on in the following order:</span></span>

  ![Kutusunu çoklu oturum açmayı yapılandırın](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 <span data-ttu-id="bd28b-141">a.</span><span class="sxs-lookup"><span data-stu-id="bd28b-141">a.</span></span> <span data-ttu-id="bd28b-142">İçinde **URL üzerinde oturum** kutusunda, Azure portalında kutusunu, oturum açma URL'si uygun şekilde ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="bd28b-142">In the **Sign on URL** box, ensure that the sign-on URL is set appropriately for Box in the Azure portal.</span></span> <span data-ttu-id="bd28b-143">Bu Box.com kiracınızın URL'dir.</span><span class="sxs-lookup"><span data-stu-id="bd28b-143">This URL is the URL of your Box.com tenant.</span></span> <span data-ttu-id="bd28b-144">Adlandırma kuralına uymalı *https://.box.com*.</span><span class="sxs-lookup"><span data-stu-id="bd28b-144">It should follow the naming convention *https://.box.com*.</span></span>  
 <span data-ttu-id="bd28b-145">**Tanımlayıcısı** bu uygulama için geçerli değildir, ancak bu zorunlu bir alan görünmeye devam eder.</span><span class="sxs-lookup"><span data-stu-id="bd28b-145">The **Identifier** does not apply to this app, but it still appears as a mandatory field.</span></span>

 <span data-ttu-id="bd28b-146">b.</span><span class="sxs-lookup"><span data-stu-id="bd28b-146">b.</span></span> <span data-ttu-id="bd28b-147">İçinde **kullanıcı tanımlayıcısı** kutusuna **user.mail** (için SSO Konuk hesapları için).</span><span class="sxs-lookup"><span data-stu-id="bd28b-147">In the **User identifier** box, enter **user.mail** (for SSO for guest accounts).</span></span>

 <span data-ttu-id="bd28b-148">c.</span><span class="sxs-lookup"><span data-stu-id="bd28b-148">c.</span></span> <span data-ttu-id="bd28b-149">Altında **SAML imzalama sertifikası**, tıklatın **yeni sertifika oluştur**.</span><span class="sxs-lookup"><span data-stu-id="bd28b-149">Under **SAML Signing Certificate**, click **Create new certificate**.</span></span>

 <span data-ttu-id="bd28b-150">d.</span><span class="sxs-lookup"><span data-stu-id="bd28b-150">d.</span></span> <span data-ttu-id="bd28b-151">Azure AD kimlik sağlayıcısı olarak kullanmak için Box.com Kiracı yapılandırmaya başlamak için meta veri dosyası karşıdan yükle ve yerel diskinize kaydedin.</span><span class="sxs-lookup"><span data-stu-id="bd28b-151">To begin configuring your Box.com tenant to use Azure AD as an identity provider, download the metadata file and then save it to your local drive.</span></span>

 <span data-ttu-id="bd28b-152">e.</span><span class="sxs-lookup"><span data-stu-id="bd28b-152">e.</span></span> <span data-ttu-id="bd28b-153">İleri kutusuna meta veri dosyası, çoklu oturum açma sizin için yapılandırır takım destekler.</span><span class="sxs-lookup"><span data-stu-id="bd28b-153">Forward the metadata file to the Box support team, which configures single sign-on for you.</span></span>

3. <span data-ttu-id="bd28b-154">Sol bölmede, Azure AD otomatik kullanıcı kurulumu seçin **sağlama**ve ardından **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="bd28b-154">For Azure AD automatic user setup, in the left pane, select **Provisioning**, and then select **Authorize**.</span></span>

  ![Azure AD kutusuna bağlanmak için yetki](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

<span data-ttu-id="bd28b-156">Dropbox davetlilerin gibi kutusunu davetlilerin Box uygulamasına kendi davetini almak gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd28b-156">Like Dropbox invitees, Box invitees must redeem their invitation from the Box app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd28b-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bd28b-157">Next steps</span></span>

<span data-ttu-id="bd28b-158">Azure AD B2B işbirliği aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="bd28b-158">See the following articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="bd28b-159">Azure AD B2B işbirliği nedir?</span><span class="sxs-lookup"><span data-stu-id="bd28b-159">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="bd28b-160">B2B işbirliği kullanıcı özellikleri</span><span class="sxs-lookup"><span data-stu-id="bd28b-160">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="bd28b-161">Bir role B2B işbirliği kullanıcı ekleme</span><span class="sxs-lookup"><span data-stu-id="bd28b-161">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="bd28b-162">B2B işbirliği davetleri temsilci seçme</span><span class="sxs-lookup"><span data-stu-id="bd28b-162">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="bd28b-163">Dinamik gruplar ve B2B işbirliği</span><span class="sxs-lookup"><span data-stu-id="bd28b-163">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="bd28b-164">B2B işbirliği kodu ve PowerShell örnekleri</span><span class="sxs-lookup"><span data-stu-id="bd28b-164">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="bd28b-165">B2B işbirliği kullanıcı belirteçleri</span><span class="sxs-lookup"><span data-stu-id="bd28b-165">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="bd28b-166">B2B işbirliği kullanıcı taleplerini eşleme</span><span class="sxs-lookup"><span data-stu-id="bd28b-166">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="bd28b-167">Office 365 dış paylaşım</span><span class="sxs-lookup"><span data-stu-id="bd28b-167">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="bd28b-168">B2B işbirliği geçerli sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="bd28b-168">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
