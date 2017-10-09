---
title: "Azure AD uygulama proxy'si kullanarak yayımlanan uygulamalar için özel bir ana sayfa aaaSet | Microsoft Docs"
description: "Merhaba temel Azure AD uygulama proxy'si bağlayıcılar hakkında bilgiler yer almaktadır"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5bb695e904d285c3b440520f107c7bf63ba5cac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a>Azure AD uygulama proxy'si kullanarak yayımlanan uygulamalar için özel bir ana sayfa ayarlayın

Bu makalede ele nasıl tooconfigure uygulamaları toodirect kullanıcılar tooa özel giriş sayfası. Uygulama proxy'si ile bir uygulama yayımladığınızda, bir iç URL ayarlanmış ancak bazen, kullanıcılarınızın ilk görmelisiniz hello sayfa değil. Özel bir ana sayfa hello uygulamaları hello Azure Active Directory erişim paneli veya hello Office 365 uygulama Başlatıcı eriştiklerinde, kullanıcılarınızın toohello sağ sayfa Git şekilde ayarlayın.

Kullanıcıların hello uygulama başlattığında, hello yayımlanan uygulama için varsayılan toohello kök etki alanı URL'si tarafından yönlendirilirsiniz. Merhaba giriş sayfası genellikle hello giriş sayfası URL'si olarak ayarlanır. Uygulama kullanıcıların tooland hello uygulama içinde belirli bir sayfada istediğinizde hello Azure AD PowerShell modülü toodefine özel giriş sayfası URL'si kullanın. 

Örneğin:
- Kullanıcılar, şirket ağı içinde çok giderek*https://ExpenseApp/login/login.aspx* toosign içinde ve uygulamanızı erişebilirsiniz.
- Uygulama proxy'si hello klasör yapısının hello üst düzeyde tooaccess gerektiğini görüntüleri gibi diğer varlıklar olduğundan hello uygulamayla yayımlama *https://ExpenseApp* İç URL hello gibi.
- dış URL varsayılan Hello *https://ExpenseApp-contoso.msappproxy.net*, değil almakta kullanıcılar toohello oturum sayfasında.  
- Ayarlama *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* kullanıcılarınız gibi hello giriş sayfası URL'si toogive sorunsuz bir deneyim. 

>[!NOTE]
>Toopublished uygulamaları kullanıcılara erişim vermek, hello uygulamaları hello görüntülenen [Azure AD erişim paneli](active-directory-saas-access-panel-introduction.md) ve hello [Office 365 uygulama Başlatıcı](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).

## <a name="before-you-start"></a>Başlamadan önce

Merhaba giriş sayfası URL'si ayarlamadan önce aşağıdaki gereksinimleri göz hello tutun:

* Bir alt etki alanı yolu hello kök etki alanı URL'si belirtmeniz hello yol olduğundan emin olun.

  Merhaba kök etki alanı URL ise, örneğin, https://apps.contoso.com/app1/, yapılandırdığınız hello giriş sayfası URL'si ile https://apps.contoso.com/app1/ başlatmanız gerekir.

* Bir değişiklik yaparsanız, toohello yayımlanan uygulama, hello değişiklik hello giriş sayfası URL'si hello değerini sıfırlama. Hello gelecekteki hello uygulamada güncelleştirdiğinizde yeniden denetle ve gerekir, gerekirse hello giriş sayfası URL'si güncelleştirin.

## <a name="change-hello-home-page-in-hello-azure-portal"></a>Hello Azure portal'de Hello giriş sayfasını değiştirme

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) yönetici olarak.
2. Çok gidin**Azure Active Directory** > **uygulama kayıtlar** ve uygulamanızı hello listeden seçin. 
3. Seçin **özellikleri** hello ayarları.
4. Güncelleştirme hello **giriş sayfası URL'si** yeni yol ile alan. 

   ![Yeni giriş sayfası URL'si belirtin](./media/application-proxy-office365-app-launcher/homepage.png)

5. Seçin **Kaydet**

## <a name="change-hello-home-page-with-powershell"></a>PowerShell ile Merhaba giriş sayfasını Değiştir

### <a name="install-hello-azure-ad-powershell-module"></a>Hello Azure AD PowerShell modülünü yükleyin

PowerShell kullanarak özel giriş sayfası URL'si tanımlamadan önce hello Azure AD PowerShell modülünü yükleyin. Hello hello paketini indirebilirsiniz [PowerShell Galerisi](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), hangi hello Graph API uç noktası kullanır. 

tooinstall hello paketini, şu adımları izleyin:

1. Standart bir PowerShell penceresi açın ve ardından hello aşağıdaki komutu çalıştırın:

    ```
     Install-Module -Name AzureAD
    ```
    Bir yönetici olmayan hello komutu çalıştırıyorsanız hello kullan `-scope currentuser` seçeneği.
2. Merhaba yükleme sırasında seçin **Y** tooinstall iki Nuget.org paketler. Her iki paketin de gereklidir. 

### <a name="find-hello-objectid-of-hello-app"></a>Hello hello uygulamasının objectID bulur

Hello hello uygulamasının objectID alın ve ardından hello uygulaması için kendi giriş sayfası tarafından arayın.

1. PowerShell'i açın ve hello Azure AD modülünü içeri aktarın.

    ```
    Import-Module AzureAD
    ```

2. Toohello içinde Azure AD modülünü hello Kiracı Yöneticisi olarak oturum açın.

    ```
    Connect-AzureAD
    ```
3. Kendi giriş sayfası URL'sine bağlı hello uygulamayı bulun. Çok giderek hello URL hello Portalı'nda bulabilirsiniz**Azure Active Directory** > **kurumsal uygulamalar** > **tüm uygulamaları**. Bu örnekte *sharepoint iddemo*.

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. Benzer toohello bir burada gösterilen bir sonuç almanız gerekir. Merhaba objectID GUID toouse hello sonraki bölümde kopyalayın.

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-hello-home-page-url"></a>Güncelleştirme hello giriş sayfası URL'si

Adım 1 ' için kullanılan aynı PowerShell modülü Hello hello aşağıdaki adımları gerçekleştirin:

1. Uygulama düzeltin ve değiştirme hello sahip olduğunuzdan emin olun *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* hello hello önceki adımda kopyaladığınız objectID ile.

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 Merhaba uygulama Onaylandı, hazır tooupdate hello giriş sayfasında, aşağıdaki gibi demektir.

2. Boş uygulama nesnesi toohold toomake istediğiniz hello değişiklikleri oluşturun. Bu değişken tooupdate istediğiniz hello değerler tutar. Hiçbir şey bu adımda oluşturulur.

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. İstediğiniz hello giriş sayfası URL'si toohello değerini ayarlayın. Merhaba değerin hello yayımlanan uygulama bir alt yolu olması gerekir. Giriş sayfası URL'den değiştirirseniz gibi hello *https://sharepoint-iddemo.msappproxy.net/* çok*https://sharepoint-iddemo.msappproxy.net/hybrid/*, uygulama kullanıcılarınızın Git doğrudan toohello özel Giriş sayfası.

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. Merhaba, kopyalanan GUID (objectID) kullanarak güncelleştirme hello olun "1. adım: Bul hello hello uygulamasının objectID."

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. Merhaba değişiklik başarılı olduğunu tooconfirm hello uygulamayı yeniden başlatın.

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
>Toohello uygulama yaptığınız tüm değişiklikler hello giriş sayfası URL'si sıfırlayabilir. Giriş sayfası URL'nizi sıfırlar, 2. adımı yineleyin.

## <a name="next-steps"></a>Sonraki adımlar

- [Azure AD uygulama proxy'si ile uzaktan erişim tooSharePoint etkinleştir](application-proxy-enable-remote-access-sharepoint.md)
- [Hello Azure portalında uygulama ara sunucusunu etkinleştirme](active-directory-application-proxy-enable.md)
