---
title: "aaaConfigure SaaS uygulamaları için Azure Active Directory B2B işbirliği | Microsoft Docs"
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
ms.openlocfilehash: c3f22f81567c04ac23ef2316c09de718ecb15d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a><span data-ttu-id="cb1c9-103">SaaS uygulamaları B2B işbirliği için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cb1c9-103">Configure SaaS apps for B2B collaboration</span></span>

<span data-ttu-id="cb1c9-104">Azure AD ile tümleştirmek çoğu uygulamaları ile Azure Active Directory (Azure AD) B2B işbirliği çalışır.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-104">Azure Active Directory (Azure AD) B2B collaboration works with most apps that integrate with Azure AD.</span></span> <span data-ttu-id="cb1c9-105">Bu bölümde, Azure AD B2B ile kullanmak için bazı yaygın SaaS uygulamaları yapılandırmaya yönelik yönergeler size rehberlik eder.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-105">In this section, we walk through instructions for configuring some popular SaaS apps for use with Azure AD B2B.</span></span>

<span data-ttu-id="cb1c9-106">Uygulamaya özgü yönergeleri göz önünde bulundurmanız önce bazı kurallar altın şunlardır:</span><span class="sxs-lookup"><span data-stu-id="cb1c9-106">Before you look at app-specific instructions, here are some rules of thumb:</span></span>

* <span data-ttu-id="cb1c9-107">Merhaba uygulamalarının çoğu için Kullanıcı Kurulumu el ile toohappen gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-107">For most of hello apps, user setup needs toohappen manually.</span></span> <span data-ttu-id="cb1c9-108">Diğer bir deyişle, kullanıcılar da hello uygulamada el ile oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-108">That is, users must be created manually in hello app as well.</span></span>

* <span data-ttu-id="cb1c9-109">Dropbox gibi otomatik kurulum destekleyen uygulamalar için ayrı davetleri hello uygulamalardan oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-109">For apps that support automatic setup, such as Dropbox, separate invitations are created from hello apps.</span></span> <span data-ttu-id="cb1c9-110">Kullanıcıların her davet emin tooaccept olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-110">Users must be sure tooaccept each invitation.</span></span>

* <span data-ttu-id="cb1c9-111">Merhaba kullanıcı öznitelikleri, tüm sorunları Konuk kullanıcılar karıştırılmış kullanıcı profili diski (UPD) ile toomitigate için her zaman kümesindeki **kullanıcı tanımlayıcısı** çok**user.mail**.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-111">In hello user attributes, toomitigate any issues with mangled user profile disk (UPD) in guest users, always set **User Identifier** too**user.mail**.</span></span>


## <a name="dropbox-business"></a><span data-ttu-id="cb1c9-112">Dropbox iş</span><span class="sxs-lookup"><span data-stu-id="cb1c9-112">Dropbox Business</span></span>

<span data-ttu-id="cb1c9-113">kendi kuruluş hesabı kullanarak tooenable kullanıcılar toosign güvenlik onaylama işlemi biçimlendirme dili (SAML) kimlik sağlayıcısı Dropbox iş toouse Azure AD el ile yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-113">tooenable users toosign in using their organization account, you must manually configure Dropbox Business toouse Azure AD as a Security Assertion Markup Language (SAML) identity provider.</span></span> <span data-ttu-id="cb1c9-114">Bu nedenle, Dropbox iş yapılandırılmış toodo olmadıysa sor veya aksi takdirde Azure AD kullanarak kullanıcıların toosign izin olamaz.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-114">If Dropbox Business has not been configured toodo so, it cannot prompt or otherwise allow users toosign in using Azure AD.</span></span>

1. <span data-ttu-id="cb1c9-115">Azure AD, select INTO tooadd hello Dropbox iş uygulama **kurumsal uygulamalar** hello sol bölmesinde ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-115">tooadd hello Dropbox Business app into Azure AD, select **Enterprise applications** in hello left pane, and then click **Add**.</span></span>

  ![Merhaba Kurumsal uygulamaları sayfasındaki Hello "Ekle" düğmesi](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. <span data-ttu-id="cb1c9-117">Merhaba, **bir uygulama eklemek** penceresinde girin **dropbox** hello arama kutusuna ve ardından **iş için Dropbox** hello sonuçları listesinde.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-117">In hello **Add an application** window, enter **dropbox** in hello search box, and then select **Dropbox for Business** in hello results list.</span></span>

  ![Merhaba "dropbox" için arama uygulama sayfası ekleme](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. <span data-ttu-id="cb1c9-119">Merhaba üzerinde **çoklu oturum açma** sayfasında, **çoklu oturum açma** hello sol bölmesinde ve ardından girin **user.mail** hello içinde **kullanıcı tanımlayıcısı** bir kutu.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-119">On hello **Single sign-on** page, select **Single sign-on** in hello left pane, and then enter **user.mail** in hello **User Identifier** box.</span></span> <span data-ttu-id="cb1c9-120">(Bunu UPN varsayılan olarak ayarlanır.)</span><span class="sxs-lookup"><span data-stu-id="cb1c9-120">(It's set as UPN by default.)</span></span>

  ![Merhaba uygulama için çoklu oturum açmayı yapılandırma](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. <span data-ttu-id="cb1c9-122">Dropbox yapılandırması için toodownload hello sertifika toouse seçin **yapılandırma DropBox**ve ardından **SAML çoklu oturum üzerinde hizmet URL'si** hello listesinde.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-122">toodownload hello certificate toouse for Dropbox configuration, select **Configure DropBox**, and then select **SAML Single Sign On Service URL** in hello list.</span></span>

  ![Dropbox yapılandırması için Hello sertifika yükleme](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. <span data-ttu-id="cb1c9-124">Oturum açma tooDropbox hello ile oturum açma URL'si hello **çoklu oturum açma** sayfası.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-124">Sign in tooDropbox with hello sign-on URL from hello **Single sign-on** page.</span></span>

  ![Merhaba Dropbox oturum açma sayfası](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. <span data-ttu-id="cb1c9-126">Başlangıç menüsünden seçin **Yönetici Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-126">On hello menu, select **Admin Console**.</span></span>

  ![Merhaba Dropbox menüsünde Hello "Yönetici Konsolu" bağlantısı](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. <span data-ttu-id="cb1c9-128">Merhaba, **kimlik doğrulaması** iletişim kutusunda **daha fazla**, hello sertifikasını karşıya yükleyin ve ardından hello **URL'de oturum** kutusunda, hello SAML çoklu oturum açma URL'sini girin.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-128">In hello **Authentication** dialog box, select **More**, upload hello certificate and then, in hello **Sign in URL** box, enter hello SAML single sign-on URL.</span></span>

  ![Merhaba hello "Daha fazla" bağlantısına daraltılmış kimlik doğrulama iletişim kutusu](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![kimlik doğrulama iletişim kutusu Hello "Oturum açma URL'si" Merhaba genişletilmiş](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. <span data-ttu-id="cb1c9-131">tooconfigure otomatik kullanıcı hello Azure portal, Kurulum'da seçin **sağlama** hello sol bölmesinde seçin **otomatik** hello içinde **sağlama modu** kutusuna ve ardından seçin **Yetkilendirmek**.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-131">tooconfigure automatic user setup in hello Azure portal, select **Provisioning** in hello left pane, select **Automatic** in hello **Provisioning Mode** box, and then select **Authorize**.</span></span>

  ![Otomatik kullanıcı sağlamayı hello Azure portalını yapılandırma](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

<span data-ttu-id="cb1c9-133">Konuk veya üye kullanıcı hello Dropbox uygulamada ayarlanan sonra Dropbox'tan ayrı bir davet alırsınız.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-133">After guest or member users have been set up in hello Dropbox app, they receive a separate invitation from Dropbox.</span></span> <span data-ttu-id="cb1c9-134">toouse Dropbox çoklu oturum açma davetlilerin bir bağlantıya tıklayarak hello daveti kabul etmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-134">toouse Dropbox single sign-on, invitees must accept hello invitation by clicking a link in it.</span></span>

## <a name="box"></a><span data-ttu-id="cb1c9-135">Box</span><span class="sxs-lookup"><span data-stu-id="cb1c9-135">Box</span></span>
<span data-ttu-id="cb1c9-136">SAML Protokolü hello üzerinde temel Federasyon kullanarak kullanıcıların tooauthenticate kutusunu Konuk kullanıcılar kendi Azure AD hesabı ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-136">You can enable users tooauthenticate Box guest users with their Azure AD account by using federation that's based on hello SAML protocol.</span></span> <span data-ttu-id="cb1c9-137">Bu yordamda, meta veri tooBox.com karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-137">In this procedure, you upload metadata tooBox.com.</span></span>

1. <span data-ttu-id="cb1c9-138">Merhaba kutusunu uygulama hello Kurumsal uygulamalardan ekleyin.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-138">Add hello Box app from hello enterprise apps.</span></span>

2. <span data-ttu-id="cb1c9-139">Çoklu oturum açma sırasının hello yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="cb1c9-139">Configure single sign-on in hello following order:</span></span>

  ![Kutusunu çoklu oturum açmayı yapılandırın](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 <span data-ttu-id="cb1c9-141">a.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-141">a.</span></span> <span data-ttu-id="cb1c9-142">Merhaba, **URL üzerinde oturum** kutusunda, hello Azure portal kutusunu, hello oturum açma URL'si uygun şekilde ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-142">In hello **Sign on URL** box, ensure that hello sign-on URL is set appropriately for Box in hello Azure portal.</span></span> <span data-ttu-id="cb1c9-143">Bu hello Box.com kiracınızın URL'dir.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-143">This URL is hello URL of your Box.com tenant.</span></span> <span data-ttu-id="cb1c9-144">Merhaba adlandırma kuralına uymalı *https://.box.com*.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-144">It should follow hello naming convention *https://.box.com*.</span></span>  
 <span data-ttu-id="cb1c9-145">Merhaba **tanımlayıcısı** toothis uygulanmaz uygulama, ancak bu zorunlu bir alan görünmeye.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-145">hello **Identifier** does not apply toothis app, but it still appears as a mandatory field.</span></span>

 <span data-ttu-id="cb1c9-146">b.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-146">b.</span></span> <span data-ttu-id="cb1c9-147">Merhaba, **kullanıcı tanımlayıcısı** kutusuna **user.mail** (için SSO Konuk hesapları için).</span><span class="sxs-lookup"><span data-stu-id="cb1c9-147">In hello **User identifier** box, enter **user.mail** (for SSO for guest accounts).</span></span>

 <span data-ttu-id="cb1c9-148">c.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-148">c.</span></span> <span data-ttu-id="cb1c9-149">Altında **SAML imzalama sertifikası**, tıklatın **yeni sertifika oluştur**.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-149">Under **SAML Signing Certificate**, click **Create new certificate**.</span></span>

 <span data-ttu-id="cb1c9-150">d.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-150">d.</span></span> <span data-ttu-id="cb1c9-151">Box.com Kiracı toouse Azure AD kimlik sağlayıcısı olarak, yapılandırma toobegin hello meta veri dosyasını indirin ve tooyour yerel sürücüye kaydedin.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-151">toobegin configuring your Box.com tenant toouse Azure AD as an identity provider, download hello metadata file and then save it tooyour local drive.</span></span>

 <span data-ttu-id="cb1c9-152">e.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-152">e.</span></span> <span data-ttu-id="cb1c9-153">Çoklu oturum açma, yapılandıran hello meta veri dosyası toohello kutusunu destek ekibi, iletin.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-153">Forward hello metadata file toohello Box support team, which configures single sign-on for you.</span></span>

3. <span data-ttu-id="cb1c9-154">Merhaba sol bölmesinde, Azure AD otomatik kullanıcı kurulumu seçin **sağlama**ve ardından **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-154">For Azure AD automatic user setup, in hello left pane, select **Provisioning**, and then select **Authorize**.</span></span>

  ![Azure AD tooconnect tooBox yetkilendirmek](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

<span data-ttu-id="cb1c9-156">Dropbox davetlilerin gibi kutusunu davetlilerin hello Box uygulamasına kendi davetini almak gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb1c9-156">Like Dropbox invitees, Box invitees must redeem their invitation from hello Box app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb1c9-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cb1c9-157">Next steps</span></span>

<span data-ttu-id="cb1c9-158">Azure AD B2B işbirliği makalelerini aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="cb1c9-158">See hello following articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="cb1c9-159">Azure AD B2B işbirliği nedir?</span><span class="sxs-lookup"><span data-stu-id="cb1c9-159">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="cb1c9-160">B2B işbirliği kullanıcı özellikleri</span><span class="sxs-lookup"><span data-stu-id="cb1c9-160">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="cb1c9-161">B2B işbirliği kullanıcı tooa rolü ekleme</span><span class="sxs-lookup"><span data-stu-id="cb1c9-161">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="cb1c9-162">B2B işbirliği davetleri temsilci seçme</span><span class="sxs-lookup"><span data-stu-id="cb1c9-162">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="cb1c9-163">Dinamik gruplar ve B2B işbirliği</span><span class="sxs-lookup"><span data-stu-id="cb1c9-163">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="cb1c9-164">B2B işbirliği kodu ve PowerShell örnekleri</span><span class="sxs-lookup"><span data-stu-id="cb1c9-164">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="cb1c9-165">B2B işbirliği kullanıcı belirteçleri</span><span class="sxs-lookup"><span data-stu-id="cb1c9-165">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="cb1c9-166">B2B işbirliği kullanıcı taleplerini eşleme</span><span class="sxs-lookup"><span data-stu-id="cb1c9-166">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="cb1c9-167">Office 365 dış paylaşım</span><span class="sxs-lookup"><span data-stu-id="cb1c9-167">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="cb1c9-168">B2B işbirliği geçerli sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="cb1c9-168">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
