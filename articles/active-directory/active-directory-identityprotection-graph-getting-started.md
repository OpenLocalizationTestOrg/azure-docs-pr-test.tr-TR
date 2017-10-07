---
title: "aaaGet başlatılan Azure Active Directory kimlik koruması ve Microsoft Graph | Microsoft Docs"
description: "Bir giriş tooquery Microsoft Graph risk olaylarına ve ilişkili bilgi listesi için Azure Active Directory'den sağlar."
services: active-directory
keywords: "Azure active directory kimlik koruması, risk olay, güvenlik açığı, güvenlik ilkesi, Microsoft Graph"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: fa109ba7-a914-437b-821d-2bd98e681386
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 75b8b7629a0120d8101f6fde0d9163122503d276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a>Azure Active Directory kimlik koruması ve Microsoft Graph kullanmaya başlama
Microsoft Graph, Microsoft unified API uç noktası hello ve, ev hello [Azure Active Directory kimlik koruması](active-directory-identityprotection.md) API'leri. Merhaba ilk API **identityRiskEvents**, bir listesi için Microsoft Graph tooquery sağlar, [risk olayları](active-directory-identityprotection-risk-events-types.md) ve bilgileri ilişkilendirilmiş. Bu makalede bu API sorgulama başlamanızı sağlar. Bir ayrıntılı giriş, tam belgelere ve erişim toohello Graph Explorer'a için hello bakın [Microsoft Graph site](https://graph.microsoft.io/).

> [!IMPORTANT]
> Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı.

Üç adımları tooaccessing kimlik koruması verilerine Microsoft Graph vardır:

1. Bir istemci parolası uygulamayla ekleyin. 
2. Bu gizli anahtar ve birkaç bilgi tooauthenticate tooMicrosoft grafiği, bir kimlik doğrulama belirteci almanıza parçalarını kullanın. 
3. Bu belirteç toomake istekleri toohello API uç noktası kullan ve kimlik koruması verileri geri alın.

Başlamadan önce ihtiyacınız vardır:

* Azure AD'de yönetici ayrıcalıkları toocreate hello uygulaması
* Kiracı'nın etki alanı (örneğin, contoso.onmicrosoft.com) Hello adı

## <a name="add-an-application-with-a-client-secret"></a>Bir istemci parolası ile uygulama ekleme
1. [Oturum](https://manage.windowsazure.com) tooyour Klasik Azure portalında yönetici olarak. 
2. Merhaba sol gezinti bölmesinde, tıklayın **Active Directory**. 
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. Merhaba gelen **Directory** listesi, tooenable dizin tümleştirme istediğiniz select başlangıç dizini.
4. Hello içinde hello üst menüsünde **uygulamaları**.
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. Tıklatın **Ekle** hello sayfanın hello sonundaki.
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. Merhaba üzerinde **neler toodo istediğiniz** iletişim kutusunda, tıklatın **kuruluşumun geliştirmekte olduğu bir uygulama Ekle**.
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. Merhaba üzerinde **bize uygulamanızı anlatın** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    a. Merhaba, **adı** metin kutusuna, uygulamanız için bir ad yazın (örneğin: AADIP Risk olayı API uygulama).
   
    b. Olarak **türü**seçin **Web uygulaması ve / veya Web API**.
   
    c. **İleri**’ye tıklayın.
8. Merhaba üzerinde **uygulama özellikleri** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    a. Merhaba, **oturum açma URL'si** metin kutusuna, türü `http://localhost`.
   
    b. Merhaba, **uygulama kimliği URI'si** metin kutusuna, türü `http://localhost`.
   
    c. **Tamamla**’ya tıklayın.

Can şimdi uygulamanızı yapılandırın.

![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-toouse-hello-api"></a>Uygulama izni toouse hello API verin
1. Uygulamanızın sayfasında hello üst hello menüsünde tıklatın **yapılandırma**. 
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. Merhaba, **izinleri tooother uygulamaları** 'yi tıklatın **uygulama eklemek**.
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. Merhaba üzerinde **izinleri tooother uygulamaları** iletişim kutusunda, hello aşağıdaki adımları gerçekleştirin:
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    a. Seçin **Microsoft Graph**.
   
    b. **Tamamla**’ya tıklayın.
4. Tıklatın **uygulama izinleri: 0**ve ardından **tüm kimlik risk olay bilgilerini okuma**.
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. Tıklatın **kaydetmek** hello sayfanın hello sonundaki.
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a>Bir erişim anahtarı alma
1. Uygulamanızın sayfasında hello **anahtarları** bölümünde, 1 yıl süre olarak seçin.
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. Tıklatın **kaydetmek** hello sayfanın hello sonundaki.
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. Merhaba anahtarları bölümünde, yeni oluşturulan anahtarınızı hello değerini kopyalayın ve güvenli bir konuma yapıştırın.
   
    ![Uygulama oluşturma](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > Bu anahtar kaybederseniz, tooreturn toothis bölümü ve yeni bir anahtar oluşturun. Bu anahtarı bir gizli tutma: olan herkes verilerinize erişebilir.
   > 
   > 
4. Merhaba, **özellikleri** bölümü, kopyalama hello **istemci kimliği**ve güvenli bir konuma yapıştırın. 

## <a name="authenticate-toomicrosoft-graph-and-query-hello-identity-risk-events-api"></a>TooMicrosoft grafik ve sorgu hello kimlik Risk olayları API kimlik doğrulaması
Bu noktada, olmalıdır:

* Yukarıdaki kopyaladığınız hello istemci kimliği
* Yukarıdaki kopyaladığınız hello anahtarı
* Merhaba, kiracının etki alanı adı

tooauthenticate, gönderme bir post isteği çok`https://login.microsoft.com` şu parametreler hello gövdesindeki hello ile:

* grant_type: "**client_credentials**"
* Kaynak: "**https://graph.microsoft.com**"
* client_id:<your client ID>
* client_secret:<your key>

> [!NOTE]
> Merhaba tooprovide değerlerine gereksinim **client_id** ve hello **client_secret** parametresi.
> 
> 

Başarılı olursa, bu kimlik doğrulama belirtecini döndürür.  
toocall hello API, parametre aşağıdaki hello bir üstbilgi oluşturun:

    `Authorization`=”<token_type> <access_token>"


Kimlik doğrulamasını yaparken, belirteç döndürdü hello hello belirteç türü ve erişim belirteci bulabilirsiniz.

Bu üst API URL aşağıdaki isteği toohello gönder:`https://graph.microsoft.com/beta/identityRiskEvents`

Merhaba yanıt başarılı olursa, kimlik, risk olaylarını koleksiyonudur ve hello ayrıştırılır ve uygun gördüğünüz şekilde ele OData JSON biçimine verilerde ilişkili.

Kimlik doğrulaması ve Powershell kullanarak hello API'sini çağırmak için örnek kod aşağıda verilmiştir.  
Yalnızca istemci Kimliğiniz Ekle anahtarı ve Kiracı etki alanı.

    $ClientID       = "<your client ID here>"        # Should be a ~36 hex character string; insert your info here
    $ClientSecret   = "<your client secret here>"    # Should be a ~44 character string; insert your info here
    $tenantdomain   = "<your tenant domain here>"    # For example, contoso.onmicrosoft.com

    $loginURL       = "https://login.microsoft.com"
    $resource       = "https://graph.microsoft.com"

    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    Write-Output $oauth

    if ($oauth.access_token -ne $null) {
        $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

        $url = "https://graph.microsoft.com/beta/identityRiskEvents"
        Write-Output $url

        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)

        foreach ($event in ($myReport.Content | ConvertFrom-Json).value) {
            Write-Output $event
        }

    } else {
        Write-Host "ERROR: No Access Token"
    } 


## <a name="next-steps"></a>Sonraki adımlar
Tebrikler, ilk çağrı tooMicrosoft grafiği yaptığınız.  
Şimdi kimlik risk olaylarını sorgular ve uygun gördüğünüz ancak hello verileri kullanın.

toolearn Microsoft Graph hakkında daha fazla grafik API'sini kullanarak toobuild uygulamaları nasıl hello denetleyip hello [belgelerine](https://graph.microsoft.io/docs) ve hello hakkında daha fazla [Microsoft Graph site](https://graph.microsoft.io/). Ayrıca, emin toobookmark hello olun [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) tüm hello kimlik koruma API'leri grafiğinde kullanılabilir listeler sayfası. API aracılığıyla kimlik koruması ile yeni yolları toowork eklediğimiz gibi ilgili sayfada görürsünüz.

## <a name="additional-resources"></a>Ek kaynaklar
* [Azure Active Directory kimlik koruması](active-directory-identityprotection.md)
* [Azure Active Directory kimlik koruması tarafından algılanan risk olayı türleri](active-directory-identityprotection-risk-events-types.md)
* [Microsoft Graph](https://graph.microsoft.io/)
* [Microsoft Graph genel bakış](https://graph.microsoft.io/docs)
* [Azure AD kimlik koruması hizmet kök](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

