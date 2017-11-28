---
title: "Azure Active Directory B2C: ADFS özel ilkelerini kullanma SAML kimlik sağlayıcısı ekleyin."
description: "ADFS SAML protokolü ve özel ilkeler kullanılarak 2016 ayarlama bir nasıl tooarticle"
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: 30fb7700e7834e3d91fab1fc1b169b761584b204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-adfs-as-a-saml-identity-provider-using-custom-policies"></a><span data-ttu-id="2806e-103">Azure Active Directory B2C: ADFS özel ilkelerini kullanma SAML kimlik sağlayıcısı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2806e-103">Azure Active Directory B2C: Add ADFS as a SAML identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="2806e-104">Bu makalede nasıl tooenable oturum açma için ADFS hesabı hello kullanımını üzerinden kullanıcılardan gösterilmektedir [özel ilkeler](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="2806e-104">This article shows you how tooenable sign-in for users from ADFS account through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2806e-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2806e-105">Prerequisites</span></span>

<span data-ttu-id="2806e-106">Tam hello adımları hello [özel ilkeleri ile çalışmaya başlama](active-directory-b2c-get-started-custom.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="2806e-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="2806e-107">Bu adımlar şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="2806e-107">These steps include:</span></span>

1.  <span data-ttu-id="2806e-108">Bağlı olan taraf güveni ADFS oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="2806e-108">Creating an ADFS Relying Party Trust.</span></span>
2.  <span data-ttu-id="2806e-109">Merhaba ADFS bağlı olan taraf güveni sertifika tooAzure AD B2C ekleniyor.</span><span class="sxs-lookup"><span data-stu-id="2806e-109">Adding hello ADFS Relying Party Trust certificate tooAzure AD B2C.</span></span>
3.  <span data-ttu-id="2806e-110">Talep sağlayıcı tooa ilke ekleniyor.</span><span class="sxs-lookup"><span data-stu-id="2806e-110">Adding claims provider tooa policy.</span></span>
4.  <span data-ttu-id="2806e-111">Kayıt hello ADFS hesap sağlayıcısı tooa kullanıcı gezisine talepleri.</span><span class="sxs-lookup"><span data-stu-id="2806e-111">Registering hello ADFS account claims provider tooa user journey.</span></span>
5.  <span data-ttu-id="2806e-112">Hello İlkesi tooan Azure AD B2C karşıya yükleme, Kiracı ve test.</span><span class="sxs-lookup"><span data-stu-id="2806e-112">Uploading hello policy tooan Azure AD B2C tenant and test it.</span></span>

## <a name="toocreate-a-claims-aware-relying-party-trust"></a><span data-ttu-id="2806e-113">toocreate talep kullanan bir bağlı taraf güveni</span><span class="sxs-lookup"><span data-stu-id="2806e-113">toocreate a claims-aware Relying Party Trust</span></span>

<span data-ttu-id="2806e-114">toouse ADFS kimlik sağlayıcısı Azure Active Directory (Azure AD) B2C içinde toocreate bir ADFS bağlı olan taraf güveni gerekir ve hello doğru parametrelerle sağlayın.</span><span class="sxs-lookup"><span data-stu-id="2806e-114">toouse ADFS as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate an ADFS Relying Party Trust and supply it with hello right parameters.</span></span>

<span data-ttu-id="2806e-115">Yeni bir bağlı olan taraf hello AD FS Yönetimi ek bileşenini kullanarak güven ve hello ayarları elle yapılandır tooadd hello bir federasyon sunucusu üzerinde aşağıdaki yordamı gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="2806e-115">tooadd a new relying party trust by using hello AD FS Management snap-in and manually configure hello settings, perform hello following procedure on a federation server.</span></span>

<span data-ttu-id="2806e-116">Üyelik **Yöneticiler**, veya eşdeğer bir gruba, hello yerel bilgisayarda hello minimum gerekli toocomplete bu yordamı.</span><span class="sxs-lookup"><span data-stu-id="2806e-116">Membership in **Administrators**, or equivalent, on hello local computer is hello minimum required toocomplete this procedure.</span></span> <span data-ttu-id="2806e-117">Merhaba uygun hesapları kullanmayla ilgili ayrıntıları gözden geçirin ve grup üyeliklerini [yerel ve etki alanı varsayılan grupları](http://go.microsoft.com/fwlink/?LinkId=83477)</span><span class="sxs-lookup"><span data-stu-id="2806e-117">Review details about using hello appropriate accounts and group memberships at [Local and Domain Default Groups](http://go.microsoft.com/fwlink/?LinkId=83477)</span></span>

1.  <span data-ttu-id="2806e-118">Sunucu Yöneticisi'nde **Araçları**ve ardından **ADFS Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="2806e-118">In Server Manager, click **Tools**, and then select **ADFS Management**.</span></span>

2.  <span data-ttu-id="2806e-119">Tıklayın **bağlı olan taraf güveni ekleme**.</span><span class="sxs-lookup"><span data-stu-id="2806e-119">Click on **Add Relying Party Trust**.</span></span>
    <span data-ttu-id="2806e-120">![Bağlı olan taraf güveni ekleme](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span><span class="sxs-lookup"><span data-stu-id="2806e-120">![Add Relying Party Trust](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span></span>

3.  <span data-ttu-id="2806e-121">Merhaba üzerinde **Hoş Geldiniz** sayfasında, **talep kullanan** tıklatıp **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="2806e-121">On hello **Welcome** page, choose **Claims aware** and click **Start**.</span></span>
    <span data-ttu-id="2806e-122">![Merhaba Hoş Geldiniz sayfasında, talep kullanan seçin](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span><span class="sxs-lookup"><span data-stu-id="2806e-122">![On hello Welcome page, choose Claims aware](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span></span>
4.  <span data-ttu-id="2806e-123">Merhaba üzerinde **veri kaynağı Seç** sayfasında, **hello bağlı olan taraf verilerini elle girin**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="2806e-123">On hello **Select Data Source** page, click **Enter data about hello relying party manually**, and then click **Next**.</span></span>
    <span data-ttu-id="2806e-124">![Merhaba bağlı olan taraf verilerini girin](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span><span class="sxs-lookup"><span data-stu-id="2806e-124">![Enter data about hello relying party](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span></span>

5.  <span data-ttu-id="2806e-125">Merhaba üzerinde **görünen adı belirt** sayfasında, bir ad yazın **görünen adı**altında **notları** bu bağlı olan taraf güveni için bir açıklama yazın ve ardından **sonraki** .</span><span class="sxs-lookup"><span data-stu-id="2806e-125">On hello **Specify Display Name** page, type a name in **Display name**, under **Notes** type a description for this relying party trust, and then click **Next**.</span></span>
    <span data-ttu-id="2806e-126">![Görünen ad ve notlar belirtin](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span><span class="sxs-lookup"><span data-stu-id="2806e-126">![Specify Display Name and notes](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span></span>
6.  <span data-ttu-id="2806e-127">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="2806e-127">Optional.</span></span> <span data-ttu-id="2806e-128">Bir isteğe bağlı belirteç şifreleme sertifikası sonra hello üzerinde varsa **sertifika Yapılandır** sayfasında, **Gözat** toolocate sertifika dosyasını ve ardından **sonraki** .</span><span class="sxs-lookup"><span data-stu-id="2806e-128">If you have an optional token encryption certificate, then on hello **Configure Certificate** page, click **Browse** toolocate your certificate file, and then click **Next**.</span></span>
    <span data-ttu-id="2806e-129">![Sertifika yapılandırma](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span><span class="sxs-lookup"><span data-stu-id="2806e-129">![Configure Certificate](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span></span>
7.  <span data-ttu-id="2806e-130">Merhaba üzerinde **URL Yapılandır** sayfası, select hello **hello SAML 2.0 WebSSO protokolü için desteği etkinleştir** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="2806e-130">On hello **Configure URL** page, select hello **Enable support for hello SAML 2.0 WebSSO protocol** check box.</span></span> <span data-ttu-id="2806e-131">Altında **bağlı olan taraf SAML 2.0 SSO hizmet URL'si**, bu bağlı olan taraf güveni hello güvenlik onaylama işlemi biçimlendirme dili (SAML) Hizmeti uç nokta URL'sini yazın ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="2806e-131">Under **Relying party SAML 2.0 SSO service URL**, type hello Security Assertion Markup Language (SAML) service endpoint URL for this relying party trust, and then click **Next**.</span></span>  <span data-ttu-id="2806e-132">Hello için **bağlı olan taraf SAML 2.0 SSO hizmet URL'si**, hello Yapıştır `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`.</span><span class="sxs-lookup"><span data-stu-id="2806e-132">For hello **Relying party SAML 2.0 SSO service URL**, paste hello `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`.</span></span> <span data-ttu-id="2806e-133">{Tenant} (örneğin, contosob2c.onmicrosoft.com), kiracının adıyla değiştirin ve hello {İlkesi} uzantıları ilke adı (örneğin, B2C_1A_TrustFrameworkExtensions) ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2806e-133">Replace {tenant} with your tenant's name (for example, contosob2c.onmicrosoft.com), and replace hello {policy} with your extensions policy name (for example, B2C_1A_TrustFrameworkExtensions).</span></span>
    > [!IMPORTANT]
    ><span data-ttu-id="2806e-134">Hello İlkesi adıdır signup_or_signin İlkesi, çünkü bu durumda devralan hello bir: `B2C_1A_TrustFrameworkExtensions`.</span><span class="sxs-lookup"><span data-stu-id="2806e-134">hello policy name  is hello one that signup_or_signin policy inherits from, in this case it is: `B2C_1A_TrustFrameworkExtensions`.</span></span>
    ><span data-ttu-id="2806e-135">Örneğin hello URL olabilir: https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span><span class="sxs-lookup"><span data-stu-id="2806e-135">For example hello URL could be:   https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span></span>

    ![Bağlı olan taraf SAML 2.0 SSO hizmet URL'si](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-6.png)
8. <span data-ttu-id="2806e-137">Merhaba üzerinde **tanımlayıcıları yapılandırma** sayfasında, hello belirtin hello önceki adımla aynı URL'yi tıklatın **Ekle** tooadd bunları toohello listeleyin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="2806e-137">On hello **Configure Identifiers** page, specify hello same URL as hello previous step, click **Add** tooadd them toohello list, and then click **Next**.</span></span>
    <span data-ttu-id="2806e-138">![Bağlı olan taraf güveni tanımlayıcıları](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span><span class="sxs-lookup"><span data-stu-id="2806e-138">![Relying party trust identifiers](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span></span>
9.  <span data-ttu-id="2806e-139">Merhaba üzerinde **erişim denetimi ilkesini seçin** bir ilke seçin ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="2806e-139">On hello **Choose Access Control Policy** select a policy and click **Next**.</span></span>
    <span data-ttu-id="2806e-140">![Erişim denetimi ilkesini seçin](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span><span class="sxs-lookup"><span data-stu-id="2806e-140">![Choose Access Control Policy](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span></span>
10.  <span data-ttu-id="2806e-141">Merhaba üzerinde **tooAdd güven hazır** sayfasında, hello ayarlarını gözden geçirin ve ardından **sonraki** toosave bağlı olan taraf güven bilgilerinizi.</span><span class="sxs-lookup"><span data-stu-id="2806e-141">On hello **Ready tooAdd Trust** page, review hello settings, and then click **Next** toosave your relying party trust information.</span></span>
    <span data-ttu-id="2806e-142">![Bağlı olan taraf güven bilgilerinizi Kaydet](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span><span class="sxs-lookup"><span data-stu-id="2806e-142">![Save your relying party trust information](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span></span>
11.  <span data-ttu-id="2806e-143">Merhaba üzerinde **son** sayfasında, **Kapat**, bu eylem otomatik olarak hello görüntüler **talep kurallarını Düzenle** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="2806e-143">On hello **Finish** page, click **Close**, this action automatically displays hello **Edit Claim Rules** dialog box.</span></span>
    <span data-ttu-id="2806e-144">![Talep kurallarını Düzenle](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span><span class="sxs-lookup"><span data-stu-id="2806e-144">![Edit Claim Rules](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span></span>
12. <span data-ttu-id="2806e-145">Tıklatın **Kuralı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="2806e-145">Click **Add Rule**.</span></span>  
      <span data-ttu-id="2806e-146">![Yeni Kural Ekle](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span><span class="sxs-lookup"><span data-stu-id="2806e-146">![Add new rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span></span>
13.  <span data-ttu-id="2806e-147">İçinde **talep kuralı şablonu**seçin **Gönder LDAP özniteliklerini talep olarak**.</span><span class="sxs-lookup"><span data-stu-id="2806e-147">In **Claim rule template**, select **Send LDAP attributes as claims**.</span></span>
    <span data-ttu-id="2806e-148">![Gönderme LDAP özniteliklerini talep şablonu kural olarak seçin](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span><span class="sxs-lookup"><span data-stu-id="2806e-148">![Select Send LDAP attributes as claims template rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span></span>
14.  <span data-ttu-id="2806e-149">Sağlamak **talep kuralı adı**.</span><span class="sxs-lookup"><span data-stu-id="2806e-149">Provide **Claim rule name**.</span></span> <span data-ttu-id="2806e-150">Hello için **öznitelik deposu** seçin **seçin Active Directory** talepler aşağıdaki hello ekleyin ve ardından **son** ve **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="2806e-150">For hello **Attribute store** select **Select Active Directory** Add hello following claims, then click **Finish** and **OK**.</span></span>
    <span data-ttu-id="2806e-151">![Kural özelliklerini ayarlama](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span><span class="sxs-lookup"><span data-stu-id="2806e-151">![Set rule properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span></span>
15.  <span data-ttu-id="2806e-152">Sunucu Yöneticisi'nde seçin **bağlı olan taraf güvenleri** ardından oluşturduğunuz hello bağlı olan taraf güveni tıklatıp **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="2806e-152">In Server Manager, select **Relying Party Trusts** then select hello relying party trust you created and click **Properties**.</span></span>
    <span data-ttu-id="2806e-153">![Bağlı olan taraf Özellikleri Düzenle](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span><span class="sxs-lookup"><span data-stu-id="2806e-153">![Relying party edit properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span></span>
16.  <span data-ttu-id="2806e-154">Bir bağlı olan taraf güveni (B2C Demo) Özellikleri penceresinde hello **imza** sekmesinde **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="2806e-154">One hello relying party trust (B2C Demo) properties window click **Signature** tab and click **Add**.</span></span>  
    <span data-ttu-id="2806e-155">![Set imza](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span><span class="sxs-lookup"><span data-stu-id="2806e-155">![Set signature](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span></span>
17.  <span data-ttu-id="2806e-156">İmza sertifikanızı (özel anahtarı olmayan .cert dosyası) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2806e-156">Add your signature certificate (.cert file, without private key).</span></span>  
    ![İmza sertifikası ekleme](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-3.png)
18.  <span data-ttu-id="2806e-158">Merhaba bağlı olan taraf güveni (B2C Demo) Özellikleri penceresinde tıklatın **Gelişmiş** sekmesinde ve hello değiştirin **güvenli karma algoritması** çok**SHA-1**, tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="2806e-158">On hello relying party trust (B2C Demo) properties window click **Advanced** tab and change hello **Secure hash algorithm** too**SHA-1**, Click **Ok**.</span></span>  
    <span data-ttu-id="2806e-159">![Güvenli Karma algoritması tooSHA-1 ayarlayın](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span><span class="sxs-lookup"><span data-stu-id="2806e-159">![Set secure hash algorithm tooSHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span></span>

## <a name="add-hello-adfs-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="2806e-160">Merhaba ADFS hesap uygulama anahtar tooAzure AD B2C ekleme</span><span class="sxs-lookup"><span data-stu-id="2806e-160">Add hello ADFS account application key tooAzure AD B2C</span></span>
<span data-ttu-id="2806e-161">ADFS hesaplarıyla Federasyon istemci parolasını ADFS hesap tootrust Azure AD B2C hello uygulama adına gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2806e-161">Federation with ADFS accounts requires a client secret for ADFS account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="2806e-162">Azure AD B2C kiracınızda ADFS sertifikanızı toostore gerekir.</span><span class="sxs-lookup"><span data-stu-id="2806e-162">You need toostore your ADFS certificate in your Azure AD B2C tenant.</span></span> 

1.  <span data-ttu-id="2806e-163">Tooyour Azure AD B2C Kiracı gidip seçin **B2C ayarlarını** > **kimlik deneyimi Framework**</span><span class="sxs-lookup"><span data-stu-id="2806e-163">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="2806e-164">Seçin **İlkesi anahtarları** tooview hello anahtarları kiracınızda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2806e-164">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="2806e-165">Tıklatın **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="2806e-165">Click **+Add**.</span></span>
4.  <span data-ttu-id="2806e-166">İçin **seçenekleri**, kullanın **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="2806e-166">For **Options**, use **Upload**.</span></span>
5.  <span data-ttu-id="2806e-167">İçin **adı**, kullanmak `ADFSSamlCert`.</span><span class="sxs-lookup"><span data-stu-id="2806e-167">For **Name**, use `ADFSSamlCert`.</span></span>  
    <span data-ttu-id="2806e-168">Merhaba önek `B2C_1A_` otomatik olarak eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="2806e-168">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="2806e-169">Merhaba dosya karşıya yükleme içinde ** özel anahtarla sertifika .pfx dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="2806e-169">In hello File upload,** select your certificate .pfx file with private key.</span></span> <span data-ttu-id="2806e-170">Not: Bu sertifikayla (Merhaba özel anahtarı) hello verilen ve hello ADFS bağlı olan taraf için kullanılan aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2806e-170">Note: this certificate (with hello private key) should be hello same one that issued and used for hello ADFS relying party.</span></span>
<span data-ttu-id="2806e-171">![İlke anahtarını karşıya yükleyin](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span><span class="sxs-lookup"><span data-stu-id="2806e-171">![Upload policy key](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span></span>
7.  <span data-ttu-id="2806e-172">**Oluştur**'a tıklayın</span><span class="sxs-lookup"><span data-stu-id="2806e-172">Click **Create**</span></span>
8.  <span data-ttu-id="2806e-173">Başlangıç anahtarı oluşturduğunuz onaylayın `B2C_1A_ADFSSamlCert`.</span><span class="sxs-lookup"><span data-stu-id="2806e-173">Confirm that you've created hello key `B2C_1A_ADFSSamlCert`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="2806e-174">Bir talep sağlayıcı uzantısı ilkenizde ekleme</span><span class="sxs-lookup"><span data-stu-id="2806e-174">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="2806e-175">Kullanıcıların toosign ADFS hesabı kullanarak isterseniz, bir talep sağlayıcısı olarak toodefine ADFS hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2806e-175">If you want users toosign in by using ADFS account, you need toodefine ADFS account as a claims provider.</span></span> <span data-ttu-id="2806e-176">Diğer bir deyişle, Azure AD B2C ile iletişim kuran bir uç nokta toospecify gerekir.</span><span class="sxs-lookup"><span data-stu-id="2806e-176">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="2806e-177">Merhaba endpoint belirli bir kullanıcı doğrulaması Azure AD B2C tooverify tarafından kullanılan talepler kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="2806e-177">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="2806e-178">ADFS ekleyerek bir talep sağlayıcısı olarak tanımlamak `<ClaimsProvider>` İlkesi uzantısının düğümünde:</span><span class="sxs-lookup"><span data-stu-id="2806e-178">Define ADFS as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1. <span data-ttu-id="2806e-179">Hello İlkesi uzantısının (TrustFrameworkExtensions.xml) çalışma dizininizi açın.</span><span class="sxs-lookup"><span data-stu-id="2806e-179">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="2806e-180">Bir XML Düzenleyici, gerekirse [Visual Studio Code deneyin](https://code.visualstudio.com/download), basit bir platformlar arası Düzenleyici.</span><span class="sxs-lookup"><span data-stu-id="2806e-180">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2. <span data-ttu-id="2806e-181">Hello bulur `<ClaimsProviders>` bölümü</span><span class="sxs-lookup"><span data-stu-id="2806e-181">Find hello `<ClaimsProviders>` section</span></span>
3. <span data-ttu-id="2806e-182">Aşağıdaki XML parçacığını hello altında hello eklemek `ClaimsProviders` öğesi ve Değiştir `identityProvider` DNS sunucunuzun (etki alanınızdaki gösterir rastgele değer) ile Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2806e-182">Add hello following XML snippet under hello `ClaimsProviders` element and replace `identityProvider` with your DNS (Arbitrary value that indicates your domain), and save hello file.</span></span> 

```xml
<ClaimsProvider>
    <Domain>contoso.com</Domain>
    <DisplayName>Contoso ADFS</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Contoso-SAML2">
        <DisplayName>Contoso ADFS</DisplayName>
        <Description>Login with your Contoso account</Description>
        <Protocol Name="SAML2"/>
        <Metadata>
        <Item Key="RequestsSigned">false</Item>
        <Item Key="WantsEncryptedAssertions">false</Item>
        <Item Key="PartnerEntity">https://{your_ADFS_domain}/federationmetadata/2007-06/federationmetadata.xml</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userPrincipalName" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="contoso.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication"/>
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-hello-adfs-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="2806e-183">Yukarı Hello ADFS hesap talep sağlayıcısı tooSign kaydetmek veya kullanıcı gezisine oturum</span><span class="sxs-lookup"><span data-stu-id="2806e-183">Register hello ADFS account claims provider tooSign up or Sign in user journey</span></span>
<span data-ttu-id="2806e-184">Bu noktada, hello kimlik sağlayıcısı ayarlandığına.</span><span class="sxs-lookup"><span data-stu-id="2806e-184">At this point, hello identity provider has been set up.</span></span>  <span data-ttu-id="2806e-185">Ancak, hello oturumu-up/oturum açma ekranları hiçbirinde kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="2806e-185">However, it is not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="2806e-186">Tooadd hello ADFS hesabı kimlik sağlayıcısı tooyour kullanıcı gerek artık `SignUpOrSignIn` kullanıcı gezisine.</span><span class="sxs-lookup"><span data-stu-id="2806e-186">Now you need tooadd hello ADFS account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="2806e-187">toomake kullanılabilir, biz var olan bir şablonu kullanıcı gezisine bir kopyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2806e-187">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="2806e-188">Merhaba ADFS kimlik sağlayıcısı içerecek şekilde sonra biz değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2806e-188">Then, we modify it so it includes hello ADFS identity provider:</span></span>
    >[!NOTE]
    >If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml) you can skip this section.
1.  <span data-ttu-id="2806e-189">Merhaba temel dosyanın ilkenizin (örneğin, TrustFrameworkBase.xml) açın.</span><span class="sxs-lookup"><span data-stu-id="2806e-189">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="2806e-190">Hello bulur `<UserJourneys>` öğesi ve kopyalama hello tüm içeriği `<UserJourneys>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="2806e-190">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="2806e-191">Merhaba uzantısının (örneğin, TrustFrameworkExtensions.xml) açın ve hello bulur `<UserJourneys>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="2806e-191">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="2806e-192">Merhaba öğe yoksa, ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2806e-192">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="2806e-193">Merhaba tüm içeriğini yapıştırın `<UserJournesy>` hello alt sitesi olarak kopyaladığınız düğümü `<UserJourneys>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="2806e-193">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="2806e-194">Görüntü hello düğmesi</span><span class="sxs-lookup"><span data-stu-id="2806e-194">Display hello button</span></span>
<span data-ttu-id="2806e-195">Merhaba `<ClaimsProviderSelections>` öğe, Talep sağlayıcı seçme seçenekleri hello listesi ve bunların sırası tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2806e-195">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="2806e-196">`<ClaimsProviderSelection>`benzer tooan kimlik sağlayıcısı düğmesi oturumu-up/oturum açma sayfasında bir öğedir.</span><span class="sxs-lookup"><span data-stu-id="2806e-196">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="2806e-197">Eklerseniz bir `<ClaimsProviderSelection>` öğesi ADFS hesap için yeni bir düğme görüntülenir hello sayfasında bir kullanıcı adlandırıldığını olduğunda.</span><span class="sxs-lookup"><span data-stu-id="2806e-197">If you add a `<ClaimsProviderSelection>` element for  ADFS account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="2806e-198">tooadd bu öğe:</span><span class="sxs-lookup"><span data-stu-id="2806e-198">tooadd this element:</span></span>

1.  <span data-ttu-id="2806e-199">Hello bulur `<UserJourney>` içeren düğüm `Id="SignUpOrSignIn"` kopyaladığınız hello kullanıcı gezisine içinde.</span><span class="sxs-lookup"><span data-stu-id="2806e-199">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="2806e-200">Merhaba bulun `<OrchestrationStep>` içeren düğümü`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="2806e-200">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="2806e-201">Aşağıdaki XML parçacığını altında ekleyin `<ClaimsProviderSelections>` düğümü:</span><span class="sxs-lookup"><span data-stu-id="2806e-201">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```
### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="2806e-202">Bağlantı hello düğmesi tooan eylemi</span><span class="sxs-lookup"><span data-stu-id="2806e-202">Link hello button tooan action</span></span>

<span data-ttu-id="2806e-203">Yerinde bir düğmeye sahip olduğunuza göre toolink gerekir, tooan eylem.</span><span class="sxs-lookup"><span data-stu-id="2806e-203">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="2806e-204">Merhaba, bu durumda, ADFS hesap tooreceive ile Azure AD B2C toocommunicate için bir belirteç eylemdir.</span><span class="sxs-lookup"><span data-stu-id="2806e-204">hello action, in this case, is for Azure AD B2C toocommunicate with ADFS account tooreceive a token.</span></span> <span data-ttu-id="2806e-205">Merhaba düğmesi tooan eylemi, ADFS hesap talep sağlayıcısı hello teknik profili bağlayarak Bağla:</span><span class="sxs-lookup"><span data-stu-id="2806e-205">Link hello button tooan action by linking hello technical profile for your ADFS account claims provider:</span></span>

1.  <span data-ttu-id="2806e-206">Hello bulur `<OrchestrationStep>` içeren `Order="2"` hello içinde `<UserJourney>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="2806e-206">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="2806e-207">Aşağıdaki XML parçacığını altında ekleyin `<ClaimsExchanges>` düğümü:</span><span class="sxs-lookup"><span data-stu-id="2806e-207">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

> [!NOTE]
> * <span data-ttu-id="2806e-208">Hello sağlamak `Id` hello aynı değeri aynı olan `TargetClaimsExchangeId` bölüm önceki hello içinde.</span><span class="sxs-lookup"><span data-stu-id="2806e-208">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section.</span></span>
> * <span data-ttu-id="2806e-209">Olun `TechnicalProfileReferenceId` önceki (Contoso-SAML2) oluşturulmuş toohello teknik profili ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2806e-209">Ensure `TechnicalProfileReferenceId` is set toohello technical profile you created earlier (Contoso-SAML2).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="2806e-210">Hello İlkesi tooyour Kiracı karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="2806e-210">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="2806e-211">Merhaba, [Azure portal](https://portal.azure.com), geçiş hello [bağlamı Azure AD B2C kiracınızın](active-directory-b2c-navigate-to-b2c-context.md)ve açık hello **Azure AD B2C** dikey.</span><span class="sxs-lookup"><span data-stu-id="2806e-211">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="2806e-212">Seçin **kimlik deneyimi Framework**.</span><span class="sxs-lookup"><span data-stu-id="2806e-212">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="2806e-213">Açık hello **tüm ilkeler** dikey.</span><span class="sxs-lookup"><span data-stu-id="2806e-213">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="2806e-214">Seçin **karşıya İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="2806e-214">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="2806e-215">Denetleme **varsa hello ilkesi üzerine** kutusu.</span><span class="sxs-lookup"><span data-stu-id="2806e-215">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="2806e-216">**Karşıya yükleme** TrustFrameworkExtensions.xml ve hello doğrulama başlayabildiğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="2806e-216">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="2806e-217">Şimdi Çalıştır kullanarak Hello özel ilkesini test</span><span class="sxs-lookup"><span data-stu-id="2806e-217">Test hello custom policy by using Run Now</span></span>
1.  <span data-ttu-id="2806e-218">Açık **Azure AD B2C ayarlarını** ve çok Git**kimlik deneyimi Framework**.</span><span class="sxs-lookup"><span data-stu-id="2806e-218">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="2806e-219">Açık **B2C_1A_signup_signin**, karşıya yüklediğiniz bağlı olan taraf (RP) özel ilke hello.</span><span class="sxs-lookup"><span data-stu-id="2806e-219">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="2806e-220">Seçin **Şimdi Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="2806e-220">Select **Run now**.</span></span>
3.  <span data-ttu-id="2806e-221">ADFS hesabı kullanarak mümkün toosign olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2806e-221">You should be able toosign in using ADFS account.</span></span>

## <a name="optional-register-hello-adfs-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="2806e-222">[İsteğe bağlı] Merhaba ADFS hesap talep sağlayıcısı tooProfile düzenleme kullanıcı gezisine kaydetme</span><span class="sxs-lookup"><span data-stu-id="2806e-222">[Optional] Register hello ADFS account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="2806e-223">Tooadd hello ADFS hesabı kimlik sağlayıcısı tooyour kullanıcı da isteyebilir `ProfileEdit` kullanıcı gezisine.</span><span class="sxs-lookup"><span data-stu-id="2806e-223">You may want tooadd hello ADFS account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="2806e-224">toomake, biz hello yineleyin kullanılabilir en son iki adımı:</span><span class="sxs-lookup"><span data-stu-id="2806e-224">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="2806e-225">Görüntü hello düğmesi</span><span class="sxs-lookup"><span data-stu-id="2806e-225">Display hello button</span></span>
1.  <span data-ttu-id="2806e-226">Merhaba uzantısının ilkenizin (örneğin, TrustFrameworkExtensions.xml) açın.</span><span class="sxs-lookup"><span data-stu-id="2806e-226">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="2806e-227">Hello bulur `<UserJourney>` içeren düğüm `Id="ProfileEdit"` kopyaladığınız hello kullanıcı gezisine içinde.</span><span class="sxs-lookup"><span data-stu-id="2806e-227">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="2806e-228">Merhaba bulun `<OrchestrationStep>` içeren düğümü`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="2806e-228">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="2806e-229">Aşağıdaki XML parçacığını altında ekleyin `<ClaimsProviderSelections>` düğümü:</span><span class="sxs-lookup"><span data-stu-id="2806e-229">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="2806e-230">Bağlantı hello düğmesi tooan eylemi</span><span class="sxs-lookup"><span data-stu-id="2806e-230">Link hello button tooan action</span></span>
1.  <span data-ttu-id="2806e-231">Hello bulur `<OrchestrationStep>` içeren `Order="2"` hello içinde `<UserJourney>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="2806e-231">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="2806e-232">Aşağıdaki XML parçacığını altında ekleyin `<ClaimsExchanges>` düğümü:</span><span class="sxs-lookup"><span data-stu-id="2806e-232">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="2806e-233">Şimdi Çalıştır kullanarak Hello özel profil Düzenleme İlkesi test</span><span class="sxs-lookup"><span data-stu-id="2806e-233">Test hello custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="2806e-234">Açık **Azure AD B2C ayarlarını** ve çok Git**kimlik deneyimi Framework**.</span><span class="sxs-lookup"><span data-stu-id="2806e-234">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="2806e-235">Açık **B2C_1A_ProfileEdit**, karşıya yüklediğiniz bağlı olan taraf (RP) özel ilke hello.</span><span class="sxs-lookup"><span data-stu-id="2806e-235">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="2806e-236">Seçin **Şimdi Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="2806e-236">Select **Run now**.</span></span>
3.  <span data-ttu-id="2806e-237">ADFS hesabı kullanarak mümkün toosign olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2806e-237">You should be able toosign in using ADFS account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="2806e-238">Merhaba tam ilke dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="2806e-238">Download hello complete policy files</span></span>
<span data-ttu-id="2806e-239">İsteğe bağlı: Size özel ilkeleri ile çalışmaya başlama yol hello tamamladıktan sonra kendi özel ilke dosyaları kullanarak senaryonuz yapı öneririz.</span><span class="sxs-lookup"><span data-stu-id="2806e-239">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through.</span></span> [<span data-ttu-id="2806e-240">İlke örnek dosyaları yalnızca başvuru için</span><span class="sxs-lookup"><span data-stu-id="2806e-240">Policy sample files for reference only</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app)
