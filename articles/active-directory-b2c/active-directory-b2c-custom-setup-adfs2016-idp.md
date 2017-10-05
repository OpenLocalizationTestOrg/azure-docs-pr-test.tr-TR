---
title: "Azure Active Directory B2C: ADFS özel ilkelerini kullanma SAML kimlik sağlayıcısı ekleyin."
description: "ADFS SAML protokolü ve özel ilkeler kullanılarak 2016 ayarlama nasıl yapılır makalesi"
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
ms.openlocfilehash: ef0495460b5652dd6052a49ab9c722381e93458b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-add-adfs-as-a-saml-identity-provider-using-custom-policies"></a><span data-ttu-id="5430d-103">Azure Active Directory B2C: ADFS özel ilkelerini kullanma SAML kimlik sağlayıcısı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5430d-103">Azure Active Directory B2C: Add ADFS as a SAML identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="5430d-104">Bu makalede, oturum açma kullanılarak ADFS hesabından kullanıcılar için etkinleştirme gösterilmektedir [özel ilkeler](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="5430d-104">This article shows you how to enable sign-in for users from ADFS account through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5430d-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5430d-105">Prerequisites</span></span>

<span data-ttu-id="5430d-106">Bölümündeki adımları tamamlamanız [özel ilkeleri ile çalışmaya başlama](active-directory-b2c-get-started-custom.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="5430d-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="5430d-107">Bu adımlar şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="5430d-107">These steps include:</span></span>

1.  <span data-ttu-id="5430d-108">Bağlı olan taraf güveni ADFS oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="5430d-108">Creating an ADFS Relying Party Trust.</span></span>
2.  <span data-ttu-id="5430d-109">ADFS bağlı olan taraf güveni sertifika Azure AD B2C'ye ekleniyor.</span><span class="sxs-lookup"><span data-stu-id="5430d-109">Adding the ADFS Relying Party Trust certificate to Azure AD B2C.</span></span>
3.  <span data-ttu-id="5430d-110">Talep sağlayıcı için bir ilke ekleniyor.</span><span class="sxs-lookup"><span data-stu-id="5430d-110">Adding claims provider to a policy.</span></span>
4.  <span data-ttu-id="5430d-111">ADFS kaydetme hesabı kullanıcı gezisine sağlayıcısına talepleri.</span><span class="sxs-lookup"><span data-stu-id="5430d-111">Registering the ADFS account claims provider to a user journey.</span></span>
5.  <span data-ttu-id="5430d-112">İlke için bir Azure AD B2C karşıya yükleme, Kiracı ve test.</span><span class="sxs-lookup"><span data-stu-id="5430d-112">Uploading the policy to an Azure AD B2C tenant and test it.</span></span>

## <a name="to-create-a-claims-aware-relying-party-trust"></a><span data-ttu-id="5430d-113">Bir talep kullanan bağlı olan taraf güveni oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="5430d-113">To create a claims-aware Relying Party Trust</span></span>

<span data-ttu-id="5430d-114">ADFS Azure Active Directory (Azure AD) B2C bir kimlik sağlayıcısı olarak kullanmak için bir ADFS bağlı olan taraf güveni oluşturmak ve doğru parametrelerle sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5430d-114">To use ADFS as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an ADFS Relying Party Trust and supply it with the right parameters.</span></span>

<span data-ttu-id="5430d-115">AD FS Yönetimi ek bileşenini kullanarak yeni bir bağlı olan taraf güveni eklemek ve ayarları el ile yapılandırmak için bir federasyon sunucusu üzerinde aşağıdaki yordamı gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="5430d-115">To add a new relying party trust by using the AD FS Management snap-in and manually configure the settings, perform the following procedure on a federation server.</span></span>

<span data-ttu-id="5430d-116">Üyelik **Yöneticiler**, ya da eşdeğer yerel bilgisayarda bu yordamı tamamlamak için gereken en düşük gereksinimdir.</span><span class="sxs-lookup"><span data-stu-id="5430d-116">Membership in **Administrators**, or equivalent, on the local computer is the minimum required to complete this procedure.</span></span> <span data-ttu-id="5430d-117">Uygun hesapları kullanmayla ilgili ayrıntıları gözden geçirin ve grup üyeliklerini [yerel ve etki alanı varsayılan grupları](http://go.microsoft.com/fwlink/?LinkId=83477)</span><span class="sxs-lookup"><span data-stu-id="5430d-117">Review details about using the appropriate accounts and group memberships at [Local and Domain Default Groups](http://go.microsoft.com/fwlink/?LinkId=83477)</span></span>

1.  <span data-ttu-id="5430d-118">Sunucu Yöneticisi'nde **Araçları**ve ardından **ADFS Yönetim**.</span><span class="sxs-lookup"><span data-stu-id="5430d-118">In Server Manager, click **Tools**, and then select **ADFS Management**.</span></span>

2.  <span data-ttu-id="5430d-119">Tıklayın **bağlı olan taraf güveni ekleme**.</span><span class="sxs-lookup"><span data-stu-id="5430d-119">Click on **Add Relying Party Trust**.</span></span>
    <span data-ttu-id="5430d-120">![Bağlı olan taraf güveni ekleme](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span><span class="sxs-lookup"><span data-stu-id="5430d-120">![Add Relying Party Trust](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span></span>

3.  <span data-ttu-id="5430d-121">Üzerinde **Hoş Geldiniz** sayfasında, **talep kullanan** tıklatıp **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="5430d-121">On the **Welcome** page, choose **Claims aware** and click **Start**.</span></span>
    <span data-ttu-id="5430d-122">![Hoş Geldiniz sayfasında, talep kullanan seçin](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span><span class="sxs-lookup"><span data-stu-id="5430d-122">![On the Welcome page, choose Claims aware](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span></span>
4.  <span data-ttu-id="5430d-123">Üzerinde **veri kaynağı Seç** sayfasında, **bağlı olan taraf verilerini elle girin**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5430d-123">On the **Select Data Source** page, click **Enter data about the relying party manually**, and then click **Next**.</span></span>
    <span data-ttu-id="5430d-124">![Bağlı olan taraf verilerini girin](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span><span class="sxs-lookup"><span data-stu-id="5430d-124">![Enter data about the relying party](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span></span>

5.  <span data-ttu-id="5430d-125">Üzerinde **görünen adı belirt** sayfasında, bir ad yazın **görünen adı**altında **notları** bu bağlı olan taraf güveni için bir açıklama yazın ve ardından **sonraki** .</span><span class="sxs-lookup"><span data-stu-id="5430d-125">On the **Specify Display Name** page, type a name in **Display name**, under **Notes** type a description for this relying party trust, and then click **Next**.</span></span>
    <span data-ttu-id="5430d-126">![Görünen ad ve notlar belirtin](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span><span class="sxs-lookup"><span data-stu-id="5430d-126">![Specify Display Name and notes](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span></span>
6.  <span data-ttu-id="5430d-127">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="5430d-127">Optional.</span></span> <span data-ttu-id="5430d-128">Bir isteğe bağlı belirteç şifreleme sertifikası sonra varsa **sertifika Yapılandır** sayfasında, **Gözat** , sertifika dosyasını bulun ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5430d-128">If you have an optional token encryption certificate, then on the **Configure Certificate** page, click **Browse** to locate your certificate file, and then click **Next**.</span></span>
    <span data-ttu-id="5430d-129">![Sertifika yapılandırma](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span><span class="sxs-lookup"><span data-stu-id="5430d-129">![Configure Certificate](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span></span>
7.  <span data-ttu-id="5430d-130">Üzerinde **URL Yapılandır** sayfasında, **SAML 2.0 WebSSO protokolü için desteği etkinleştir** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="5430d-130">On the **Configure URL** page, select the **Enable support for the SAML 2.0 WebSSO protocol** check box.</span></span> <span data-ttu-id="5430d-131">Altında **bağlı olan taraf SAML 2.0 SSO hizmet URL'si**, bu bağlı olan taraf güveni için güvenlik onaylama işlemi biçimlendirme dili (SAML) Hizmeti uç nokta URL'sini yazın ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5430d-131">Under **Relying party SAML 2.0 SSO service URL**, type the Security Assertion Markup Language (SAML) service endpoint URL for this relying party trust, and then click **Next**.</span></span>  <span data-ttu-id="5430d-132">İçin **bağlı olan taraf SAML 2.0 SSO hizmet URL'si**, yapıştırma `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`.</span><span class="sxs-lookup"><span data-stu-id="5430d-132">For the **Relying party SAML 2.0 SSO service URL**, paste the `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`.</span></span> <span data-ttu-id="5430d-133">{Tenant} (örneğin, contosob2c.onmicrosoft.com), kiracının adıyla değiştirin ve {İlkesi} uzantıları ilke adı (örneğin, B2C_1A_TrustFrameworkExtensions) ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5430d-133">Replace {tenant} with your tenant's name (for example, contosob2c.onmicrosoft.com), and replace the {policy} with your extensions policy name (for example, B2C_1A_TrustFrameworkExtensions).</span></span>
    > [!IMPORTANT]
    ><span data-ttu-id="5430d-134">İlke adı signup_or_signin ilke, çünkü bu durumda devraldığı bilgisayardır: `B2C_1A_TrustFrameworkExtensions`.</span><span class="sxs-lookup"><span data-stu-id="5430d-134">The policy name  is the one that signup_or_signin policy inherits from, in this case it is: `B2C_1A_TrustFrameworkExtensions`.</span></span>
    ><span data-ttu-id="5430d-135">Örneğin bir URL olabilir: https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span><span class="sxs-lookup"><span data-stu-id="5430d-135">For example the URL could be:   https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span></span>

    ![Bağlı olan taraf SAML 2.0 SSO hizmet URL'si](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-6.png)
8. <span data-ttu-id="5430d-137">Üzerinde **tanımlayıcıları yapılandırma** sayfasında, önceki adımı olarak aynı URL'yi belirtin, **Ekle** bunları listeye ekleyin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5430d-137">On the **Configure Identifiers** page, specify the same URL as the previous step, click **Add** to add them to the list, and then click **Next**.</span></span>
    <span data-ttu-id="5430d-138">![Bağlı olan taraf güveni tanımlayıcıları](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span><span class="sxs-lookup"><span data-stu-id="5430d-138">![Relying party trust identifiers](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span></span>
9.  <span data-ttu-id="5430d-139">Üzerinde **erişim denetimi ilkesini seçin** bir ilke seçin ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5430d-139">On the **Choose Access Control Policy** select a policy and click **Next**.</span></span>
    <span data-ttu-id="5430d-140">![Erişim denetimi ilkesini seçin](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span><span class="sxs-lookup"><span data-stu-id="5430d-140">![Choose Access Control Policy](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span></span>
10.  <span data-ttu-id="5430d-141">Üzerinde **güven eklemeye hazır** sayfasında, ayarları gözden geçirin ve ardından **sonraki** bağlı olan taraf kaydetmek için güven bilgileri.</span><span class="sxs-lookup"><span data-stu-id="5430d-141">On the **Ready to Add Trust** page, review the settings, and then click **Next** to save your relying party trust information.</span></span>
    <span data-ttu-id="5430d-142">![Bağlı olan taraf güven bilgilerinizi Kaydet](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span><span class="sxs-lookup"><span data-stu-id="5430d-142">![Save your relying party trust information](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span></span>
11.  <span data-ttu-id="5430d-143">Üzerinde **son** sayfasında, **Kapat**, bu eylem otomatik olarak görüntüler **talep kurallarını Düzenle** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="5430d-143">On the **Finish** page, click **Close**, this action automatically displays the **Edit Claim Rules** dialog box.</span></span>
    <span data-ttu-id="5430d-144">![Talep kurallarını Düzenle](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span><span class="sxs-lookup"><span data-stu-id="5430d-144">![Edit Claim Rules](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span></span>
12. <span data-ttu-id="5430d-145">Tıklatın **Kuralı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="5430d-145">Click **Add Rule**.</span></span>  
      <span data-ttu-id="5430d-146">![Yeni Kural Ekle](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span><span class="sxs-lookup"><span data-stu-id="5430d-146">![Add new rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span></span>
13.  <span data-ttu-id="5430d-147">İçinde **talep kuralı şablonu**seçin **Gönder LDAP özniteliklerini talep olarak**.</span><span class="sxs-lookup"><span data-stu-id="5430d-147">In **Claim rule template**, select **Send LDAP attributes as claims**.</span></span>
    <span data-ttu-id="5430d-148">![Gönderme LDAP özniteliklerini talep şablonu kural olarak seçin](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span><span class="sxs-lookup"><span data-stu-id="5430d-148">![Select Send LDAP attributes as claims template rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span></span>
14.  <span data-ttu-id="5430d-149">Sağlamak **talep kuralı adı**.</span><span class="sxs-lookup"><span data-stu-id="5430d-149">Provide **Claim rule name**.</span></span> <span data-ttu-id="5430d-150">İçin **öznitelik deposu** seçin **seçin Active Directory** aşağıdaki talep ekleyin ve ardından **son** ve **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="5430d-150">For the **Attribute store** select **Select Active Directory** Add the following claims, then click **Finish** and **OK**.</span></span>
    <span data-ttu-id="5430d-151">![Kural özelliklerini ayarlama](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span><span class="sxs-lookup"><span data-stu-id="5430d-151">![Set rule properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span></span>
15.  <span data-ttu-id="5430d-152">Sunucu Yöneticisi'nde seçin **bağlı olan taraf güvenleri** sonra seçin bağlı olan taraf oluşturduğunuz güven ve ' **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="5430d-152">In Server Manager, select **Relying Party Trusts** then select the relying party trust you created and click **Properties**.</span></span>
    <span data-ttu-id="5430d-153">![Bağlı olan taraf Özellikleri Düzenle](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span><span class="sxs-lookup"><span data-stu-id="5430d-153">![Relying party edit properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span></span>
16.  <span data-ttu-id="5430d-154">Bir bağlı olan taraf güveni (B2C Demo) Özellikler penceresini tıklatın **imza** sekmesinde **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="5430d-154">One the relying party trust (B2C Demo) properties window click **Signature** tab and click **Add**.</span></span>  
    <span data-ttu-id="5430d-155">![Set imza](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span><span class="sxs-lookup"><span data-stu-id="5430d-155">![Set signature](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span></span>
17.  <span data-ttu-id="5430d-156">İmza sertifikanızı (özel anahtarı olmayan .cert dosyası) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5430d-156">Add your signature certificate (.cert file, without private key).</span></span>  
    ![İmza sertifikası ekleme](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-3.png)
18.  <span data-ttu-id="5430d-158">Bağlı olan taraf güveni (B2C Demo) Özellikleri penceresinde tıklatın **Gelişmiş** sekmesinde ve değiştirme **güvenli karma algoritması** için **SHA-1**, tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="5430d-158">On the relying party trust (B2C Demo) properties window click **Advanced** tab and change the **Secure hash algorithm** to **SHA-1**, Click **Ok**.</span></span>  
    <span data-ttu-id="5430d-159">![Güvenli Karma algoritması SHA-1 olarak ayarlayın](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span><span class="sxs-lookup"><span data-stu-id="5430d-159">![Set secure hash algorithm to SHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span></span>

## <a name="add-the-adfs-account-application-key-to-azure-ad-b2c"></a><span data-ttu-id="5430d-160">Azure AD B2C'ye ADFS hesap uygulama anahtarı Ekle</span><span class="sxs-lookup"><span data-stu-id="5430d-160">Add the ADFS account application key to Azure AD B2C</span></span>
<span data-ttu-id="5430d-161">ADFS hesaplarıyla federasyon güven Azure AD B2C uygulama adına ADFS hesabına istemci gizli anahtarı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5430d-161">Federation with ADFS accounts requires a client secret for ADFS account to trust Azure AD B2C on behalf of the application.</span></span> <span data-ttu-id="5430d-162">Azure AD B2C kiracınızda ADFS sertifikanızı depolamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5430d-162">You need to store your ADFS certificate in your Azure AD B2C tenant.</span></span> 

1.  <span data-ttu-id="5430d-163">Azure AD B2C kiracınızın gidin ve seçin **B2C ayarlarını** > **kimlik deneyimi Framework**</span><span class="sxs-lookup"><span data-stu-id="5430d-163">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="5430d-164">Seçin **İlkesi anahtarları** kiracınızda kullanılabilir tuşlarını görmek için.</span><span class="sxs-lookup"><span data-stu-id="5430d-164">Select **Policy Keys** to view the keys available in your tenant.</span></span>
3.  <span data-ttu-id="5430d-165">Tıklatın **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="5430d-165">Click **+Add**.</span></span>
4.  <span data-ttu-id="5430d-166">İçin **seçenekleri**, kullanın **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="5430d-166">For **Options**, use **Upload**.</span></span>
5.  <span data-ttu-id="5430d-167">İçin **adı**, kullanmak `ADFSSamlCert`.</span><span class="sxs-lookup"><span data-stu-id="5430d-167">For **Name**, use `ADFSSamlCert`.</span></span>  
    <span data-ttu-id="5430d-168">Önek `B2C_1A_` otomatik olarak eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="5430d-168">The prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="5430d-169">Dosya karşıya yükleme içinde ** özel anahtarla sertifika .pfx dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="5430d-169">In the File upload,** select your certificate .pfx file with private key.</span></span> <span data-ttu-id="5430d-170">Not: Bu sertifikayı (özel anahtarla) verilen ve ADFS bağlı olan taraf için kullanılan adla aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5430d-170">Note: this certificate (with the private key) should be the same one that issued and used for the ADFS relying party.</span></span>
<span data-ttu-id="5430d-171">![İlke anahtarını karşıya yükleyin](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span><span class="sxs-lookup"><span data-stu-id="5430d-171">![Upload policy key](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span></span>
7.  <span data-ttu-id="5430d-172">**Oluştur**'a tıklayın</span><span class="sxs-lookup"><span data-stu-id="5430d-172">Click **Create**</span></span>
8.  <span data-ttu-id="5430d-173">Anahtar oluşturduğunuz onaylayın `B2C_1A_ADFSSamlCert`.</span><span class="sxs-lookup"><span data-stu-id="5430d-173">Confirm that you've created the key `B2C_1A_ADFSSamlCert`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="5430d-174">Bir talep sağlayıcı uzantısı ilkenizde ekleme</span><span class="sxs-lookup"><span data-stu-id="5430d-174">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="5430d-175">ADFS hesabını kullanarak oturum açmalarını istiyorsanız, bir talep sağlayıcısı olarak ADFS hesap tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5430d-175">If you want users to sign in by using ADFS account, you need to define ADFS account as a claims provider.</span></span> <span data-ttu-id="5430d-176">Diğer bir deyişle, Azure AD B2C ile iletişim kuran bir uç nokta belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5430d-176">In other words, you need to specify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="5430d-177">Uç nokta Azure AD B2C tarafından belirli bir kullanıcı kimliği doğrulanmış olduğunu doğrulamak için kullanılan talep kümesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="5430d-177">The endpoint provides a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span>

<span data-ttu-id="5430d-178">ADFS ekleyerek bir talep sağlayıcısı olarak tanımlamak `<ClaimsProvider>` İlkesi uzantısının düğümünde:</span><span class="sxs-lookup"><span data-stu-id="5430d-178">Define ADFS as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1. <span data-ttu-id="5430d-179">Uzantı ilke dosyası (TrustFrameworkExtensions.xml) çalışma dizininizi açın.</span><span class="sxs-lookup"><span data-stu-id="5430d-179">Open the extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="5430d-180">Bir XML Düzenleyici, gerekirse [Visual Studio Code deneyin](https://code.visualstudio.com/download), basit bir platformlar arası Düzenleyici.</span><span class="sxs-lookup"><span data-stu-id="5430d-180">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2. <span data-ttu-id="5430d-181">Bul `<ClaimsProviders>` bölümü</span><span class="sxs-lookup"><span data-stu-id="5430d-181">Find the `<ClaimsProviders>` section</span></span>
3. <span data-ttu-id="5430d-182">Altında aşağıdaki XML parçacığını ekleyin `ClaimsProviders` öğesi ve Değiştir `identityProvider` DNS sunucunuzun (etki alanınızdaki gösterir rastgele değer) ile ve dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5430d-182">Add the following XML snippet under the `ClaimsProviders` element and replace `identityProvider` with your DNS (Arbitrary value that indicates your domain), and save the file.</span></span> 

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

## <a name="register-the-adfs-account-claims-provider-to-sign-up-or-sign-in-user-journey"></a><span data-ttu-id="5430d-183">Yukarı imzalamak için ADFS hesap talep sağlayıcısı kaydedilemedi veya kullanıcı gezisine oturum</span><span class="sxs-lookup"><span data-stu-id="5430d-183">Register the ADFS account claims provider to Sign up or Sign in user journey</span></span>
<span data-ttu-id="5430d-184">Bu noktada, kimlik sağlayıcısı ayarlandığına.</span><span class="sxs-lookup"><span data-stu-id="5430d-184">At this point, the identity provider has been set up.</span></span>  <span data-ttu-id="5430d-185">Ancak, oturumu-up/oturum açma ekranları hiçbirinde kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="5430d-185">However, it is not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="5430d-186">ADFS hesabı kimlik sağlayıcısı, kullanıcı eklemek gereken artık `SignUpOrSignIn` kullanıcı gezisine.</span><span class="sxs-lookup"><span data-stu-id="5430d-186">Now you need to add the ADFS account identity provider to your user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="5430d-187">Kullanılabilir hale getirmek için var olan bir şablonu kullanıcı gezisine tekrarı oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="5430d-187">To make it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="5430d-188">ADFS kimlik sağlayıcısı içerecek şekilde sonra biz değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5430d-188">Then, we modify it so it includes the ADFS identity provider:</span></span>
    >[!NOTE]
    >If you previously copied the `<UserJourneys>` element from base file of your policy to the extension file (TrustFrameworkExtensions.xml) you can skip this section.
1.  <span data-ttu-id="5430d-189">Temel dosya ilkenizin (örneğin, TrustFrameworkBase.xml) açın.</span><span class="sxs-lookup"><span data-stu-id="5430d-189">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="5430d-190">Bul `<UserJourneys>` öğesi ve tüm içeriğini kopyalayın `<UserJourneys>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="5430d-190">Find the `<UserJourneys>` element and copy the entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="5430d-191">Uzantı dosyası (örneğin, TrustFrameworkExtensions.xml) açın ve Bul `<UserJourneys>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="5430d-191">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="5430d-192">Öğe yoksa, ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5430d-192">If the element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="5430d-193">Tüm içeriğini yapıştırın `<UserJournesy>` bir alt öğesi olarak kopyaladığınız düğümü `<UserJourneys>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="5430d-193">Paste the entire content of `<UserJournesy>` node that you copied as a child of the `<UserJourneys>` element.</span></span>

### <a name="display-the-button"></a><span data-ttu-id="5430d-194">Görüntü düğmesi</span><span class="sxs-lookup"><span data-stu-id="5430d-194">Display the button</span></span>
<span data-ttu-id="5430d-195">`<ClaimsProviderSelections>` Öğesi talep sağlayıcısı seçme seçenekleri ve bunların sırası listesini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5430d-195">The `<ClaimsProviderSelections>` element defines the list of claims provider selection options and their order.</span></span>  <span data-ttu-id="5430d-196">`<ClaimsProviderSelection>`öğesi, bir oturumu-up/oturum açma sayfasında bir kimlik sağlayıcısı düğmesini benzerdir.</span><span class="sxs-lookup"><span data-stu-id="5430d-196">`<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="5430d-197">Eklerseniz bir `<ClaimsProviderSelection>` öğesi ADFS hesap için yeni bir düğme görüntülenir sayfasında bir kullanıcı adlandırıldığını olduğunda.</span><span class="sxs-lookup"><span data-stu-id="5430d-197">If you add a `<ClaimsProviderSelection>` element for  ADFS account, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="5430d-198">Bu öğe eklemek için:</span><span class="sxs-lookup"><span data-stu-id="5430d-198">To add this element:</span></span>

1.  <span data-ttu-id="5430d-199">Bul `<UserJourney>` içeren düğüm `Id="SignUpOrSignIn"` kopyaladığınız kullanıcı gezisine içinde.</span><span class="sxs-lookup"><span data-stu-id="5430d-199">Find the `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in the user journey that you copied.</span></span>
2.  <span data-ttu-id="5430d-200">Bulun `<OrchestrationStep>` içeren düğümü`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="5430d-200">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="5430d-201">Aşağıdaki XML parçacığını altında ekleyin `<ClaimsProviderSelections>` düğümü:</span><span class="sxs-lookup"><span data-stu-id="5430d-201">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```
### <a name="link-the-button-to-an-action"></a><span data-ttu-id="5430d-202">Düğme için bir eylem bağlantı kurun</span><span class="sxs-lookup"><span data-stu-id="5430d-202">Link the button to an action</span></span>

<span data-ttu-id="5430d-203">Yerinde bir düğmeye sahip olduğunuza göre bir eyleme bağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5430d-203">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="5430d-204">Eylem, bu durumda, bir belirteç almak için ADFS hesabı ile iletişim kurmak Azure AD B2C içindir.</span><span class="sxs-lookup"><span data-stu-id="5430d-204">The action, in this case, is for Azure AD B2C to communicate with ADFS account to receive a token.</span></span> <span data-ttu-id="5430d-205">Düğme, ADFS hesap talep sağlayıcısı teknik profili bağlayarak bir eyleme bağlantı:</span><span class="sxs-lookup"><span data-stu-id="5430d-205">Link the button to an action by linking the technical profile for your ADFS account claims provider:</span></span>

1.  <span data-ttu-id="5430d-206">Bul `<OrchestrationStep>` içeren `Order="2"` içinde `<UserJourney>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="5430d-206">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="5430d-207">Aşağıdaki XML parçacığını altında ekleyin `<ClaimsExchanges>` düğümü:</span><span class="sxs-lookup"><span data-stu-id="5430d-207">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

> [!NOTE]
> * <span data-ttu-id="5430d-208">Olun `Id` , aynı değere sahip `TargetClaimsExchangeId` önceki bölümde.</span><span class="sxs-lookup"><span data-stu-id="5430d-208">Ensure the `Id` has the same value as that of `TargetClaimsExchangeId` in the preceding section.</span></span>
> * <span data-ttu-id="5430d-209">Olun `TechnicalProfileReferenceId` ayarlanmış teknik profiline oluşturduğunuz önceki (Contoso-SAML2).</span><span class="sxs-lookup"><span data-stu-id="5430d-209">Ensure `TechnicalProfileReferenceId` is set to the technical profile you created earlier (Contoso-SAML2).</span></span>

## <a name="upload-the-policy-to-your-tenant"></a><span data-ttu-id="5430d-210">İlke kiracınız için karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="5430d-210">Upload the policy to your tenant</span></span>
1.  <span data-ttu-id="5430d-211">İçinde [Azure portal](https://portal.azure.com), içine geçiş [bağlam Azure AD B2C kiracınızın](active-directory-b2c-navigate-to-b2c-context.md), açarak **Azure AD B2C** dikey.</span><span class="sxs-lookup"><span data-stu-id="5430d-211">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open the **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="5430d-212">Seçin **kimlik deneyimi Framework**.</span><span class="sxs-lookup"><span data-stu-id="5430d-212">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="5430d-213">Açık **tüm ilkeler** dikey.</span><span class="sxs-lookup"><span data-stu-id="5430d-213">Open the **All Policies** blade.</span></span>
4.  <span data-ttu-id="5430d-214">Seçin **karşıya İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="5430d-214">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="5430d-215">Denetleme **varsa ilkesi üzerine** kutusu.</span><span class="sxs-lookup"><span data-stu-id="5430d-215">Check **Overwrite the policy if it exists** box.</span></span>
6.  <span data-ttu-id="5430d-216">**Karşıya yükleme** TrustFrameworkExtensions.xml ve doğrulama başlayabildiğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="5430d-216">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail the validation</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="5430d-217">Özel ilke Şimdi Çalıştır kullanarak test</span><span class="sxs-lookup"><span data-stu-id="5430d-217">Test the custom policy by using Run Now</span></span>
1.  <span data-ttu-id="5430d-218">Açık **Azure AD B2C ayarlarını** ve Git **kimlik deneyimi Framework**.</span><span class="sxs-lookup"><span data-stu-id="5430d-218">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="5430d-219">Açık **B2C_1A_signup_signin**, karşıya yüklediğiniz bağlı olan taraf (RP) özel ilke.</span><span class="sxs-lookup"><span data-stu-id="5430d-219">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="5430d-220">Seçin **Şimdi Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="5430d-220">Select **Run now**.</span></span>
3.  <span data-ttu-id="5430d-221">ADFS hesabı kullanarak oturum olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5430d-221">You should be able to sign in using ADFS account.</span></span>

## <a name="optional-register-the-adfs-account-claims-provider-to-profile-edit-user-journey"></a><span data-ttu-id="5430d-222">[İsteğe bağlı] Profil düzenleme kullanıcı gezisine ADFS hesap talep sağlayıcısını Kaydet</span><span class="sxs-lookup"><span data-stu-id="5430d-222">[Optional] Register the ADFS account claims provider to Profile-Edit user journey</span></span>
<span data-ttu-id="5430d-223">ADFS hesabı kimlik sağlayıcısı Ayrıca, kullanıcı eklemek isteyebilirsiniz `ProfileEdit` kullanıcı gezisine.</span><span class="sxs-lookup"><span data-stu-id="5430d-223">You may want to add the ADFS account identity provider also to your user `ProfileEdit` user journey.</span></span> <span data-ttu-id="5430d-224">Kullanılabilir hale getirmek için biz son iki adımı yineleyin:</span><span class="sxs-lookup"><span data-stu-id="5430d-224">To make it available, we repeat the last two steps:</span></span>

### <a name="display-the-button"></a><span data-ttu-id="5430d-225">Görüntü düğmesi</span><span class="sxs-lookup"><span data-stu-id="5430d-225">Display the button</span></span>
1.  <span data-ttu-id="5430d-226">Uzantı dosyası ilkenizin (örneğin, TrustFrameworkExtensions.xml) açın.</span><span class="sxs-lookup"><span data-stu-id="5430d-226">Open the extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="5430d-227">Bul `<UserJourney>` içeren düğüm `Id="ProfileEdit"` kopyaladığınız kullanıcı gezisine içinde.</span><span class="sxs-lookup"><span data-stu-id="5430d-227">Find the `<UserJourney>` node that includes `Id="ProfileEdit"` in the user journey that you copied.</span></span>
3.  <span data-ttu-id="5430d-228">Bulun `<OrchestrationStep>` içeren düğümü`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="5430d-228">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="5430d-229">Aşağıdaki XML parçacığını altında ekleyin `<ClaimsProviderSelections>` düğümü:</span><span class="sxs-lookup"><span data-stu-id="5430d-229">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="5430d-230">Düğme için bir eylem bağlantı kurun</span><span class="sxs-lookup"><span data-stu-id="5430d-230">Link the button to an action</span></span>
1.  <span data-ttu-id="5430d-231">Bul `<OrchestrationStep>` içeren `Order="2"` içinde `<UserJourney>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="5430d-231">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="5430d-232">Aşağıdaki XML parçacığını altında ekleyin `<ClaimsExchanges>` düğümü:</span><span class="sxs-lookup"><span data-stu-id="5430d-232">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

### <a name="test-the-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="5430d-233">Özel Profil Düzenleme İlkesi Şimdi Çalıştır kullanarak test</span><span class="sxs-lookup"><span data-stu-id="5430d-233">Test the custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="5430d-234">Açık **Azure AD B2C ayarlarını** ve Git **kimlik deneyimi Framework**.</span><span class="sxs-lookup"><span data-stu-id="5430d-234">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="5430d-235">Açık **B2C_1A_ProfileEdit**, karşıya yüklediğiniz bağlı olan taraf (RP) özel ilke.</span><span class="sxs-lookup"><span data-stu-id="5430d-235">Open **B2C_1A_ProfileEdit**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="5430d-236">Seçin **Şimdi Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="5430d-236">Select **Run now**.</span></span>
3.  <span data-ttu-id="5430d-237">ADFS hesabı kullanarak oturum olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5430d-237">You should be able to sign in using ADFS account.</span></span>

## <a name="download-the-complete-policy-files"></a><span data-ttu-id="5430d-238">Tam ilke dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="5430d-238">Download the complete policy files</span></span>
<span data-ttu-id="5430d-239">İsteğe bağlı: Dosyaları ile çalışmaya başlama özel ilkeler tamamladıktan sonra size yol kendi özel İlkesi kullanarak senaryonuz yapı öneririz.</span><span class="sxs-lookup"><span data-stu-id="5430d-239">Optional: We recommend you build your scenario using your own Custom policy files after completing the Getting Started with Custom Policies walk through.</span></span> [<span data-ttu-id="5430d-240">İlke örnek dosyaları yalnızca başvuru için</span><span class="sxs-lookup"><span data-stu-id="5430d-240">Policy sample files for reference only</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app)
