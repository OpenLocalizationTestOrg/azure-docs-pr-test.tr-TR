---
title: "Azure Active Directory cihaz kaydı hizmetini kullanarak şirket içi koşullu erişim aaaSetting | Microsoft Docs"
description: "Windows Server 2012 R2'de Active Directory Federasyon Hizmetleri (AD FS) kullanarak bir adım adım kılavuzu tooenabling koşullu erişim tooon içi uygulamalar."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6ae9df8b-31fe-4d72-9181-cf50cfebbf05
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 808e3b96873102aebae667153f588dcdb205e884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-on-premises-conditional-access-by-using-azure-active-directory-device-registration"></a>Azure Active Directory cihaz kaydı kullanarak şirket içi koşullu erişimi ayarlama
Kendi kişisel cihazlarını toohello Azure Active Directory (Azure AD) cihaz kayıt hizmeti kullanıcıların tooworkplace birleşim gerektirdiğinde cihazlarını bilinen tooyour kuruluş olarak işaretlenebilir. Aşağıda, koşullu erişim tooon içi uygulamaları Windows Server 2012 R2'de Active Directory Federasyon Hizmetleri (AD FS) kullanarak etkinleştirmek için adım adım yönergeler verilmektedir.

> [!NOTE]
> Bir Office 365 lisansı veya Azure AD Premium lisansı Azure Active Directory cihaz kayıt hizmeti koşullu erişim ilkelerini kayıtlı cihazlar kullanılırken gereklidir. Bunlar şirket içi kaynakları'de AD FS tarafından uygulanan ilkeler içerir.
> 
> Şirket içi kaynaklar için hello koşullu erişim senaryoları hakkında daha fazla bilgi için bkz: [katılma herhangi bir CİHAZDAN tooworkplace SSO ve sorunsuz ikinci faktör kimlik doğrulaması için şirket uygulamaları arasında](https://technet.microsoft.com/library/dn280945.aspx).

Bu özellikler bir Azure Active Directory Premium lisansı satın kullanılabilir toocustomers ' dir.

## <a name="supported-devices"></a>Desteklenen cihazlar
* Windows 7 etki alanına katılmış cihazlar
* Windows 8.1 kişisel ve etki alanına katılmış aygıtlar
* iOS 6 ve üzeri hello Safari tarayıcısı
* Android 4.0 ve üzeri, Samsung GS3 veya üzeri telefonları, Samsung Galaxy Not 2 veya sonraki tabletler

## <a name="scenario-prerequisites"></a>Senaryo önkoşulları
* Abonelik tooOffice 365 veya Azure Active Directory Premium
* Azure Active Directory kiracısı
* Windows Server Active Directory (Windows Server 2008 veya üzeri)
* Windows Server 2012 R2'de güncelleştirilmiş şeması
* Azure Active Directory Premium lisansı
* Windows Server 2012 R2 Federasyon SSO tooAzure AD yapılandırılmış hizmetleri,
* Windows Server 2012 R2 Web uygulaması proxy'si 
* Microsoft Azure Active Directory Connect (Azure AD Connect) [(Azure AD Connect'i indirme)](http://www.microsoft.com/en-us/download/details.aspx?id=47594)
* Doğrulanmış etki alanı

## <a name="known-issues-in-this-release"></a>Bu sürümdeki bilinen sorunlar
* Cihaz temelli koşullu erişim ilkeleri cihaz nesnesi geri yazma tooActive Azure Active Directory'den dizin gerektirir. Cihaz nesneleri toobe tooActive dizine geri yazabilirsiniz için toothree saatlerini alabilir.
* iOS 7 aygıtları hello kullanıcı tooselect bir sertifika istemci sertifikası kimlik doğrulaması sırasında her zaman sor.
* İOS 8 iOS 8.3 çalışmıyor önce bazı sürümleri.

## <a name="scenario-assumptions"></a>Senaryo varsayımlar
Bu senaryo, Azure AD kiracısı ve bir şirket içi Active Directory oluşan karma bir ortamınız sahip olduğunuzu varsayar. Bu kiracılar Azure AD Connect, doğrulanmış bir etki alanı ve AD FS için SSO bağlı olması gerekir. Ortamınızı toohello gereksinimlerine göre yapılandırma denetim listesi toohelp aşağıdaki hello kullanın.

## <a name="checklist-prerequisites-for-conditional-access-scenario"></a>Denetim listesi: Koşullu erişim senaryo Önkoşullar
Azure AD kiracınıza şirket içi Active Directory örneğinizle bağlayın.

## <a name="configure-azure-active-directory-device-registration-service"></a>Azure Active Directory cihaz kayıt hizmeti yapılandırma
Bu kılavuzu toodeploy kullanın ve hello Azure Active Directory cihaz kayıt hizmeti, kuruluşunuz için yapılandırın.

Bu kılavuz, Windows Server Active Directory yapılandırdıysanız ve tooMicrosoft Azure Active Directory abone olduğunuz varsayar. Daha önce açıklanan hello önkoşullara bakın.

Denetim listesi sırayla aşağıdaki hello tam hello görevlerinde toodeploy hello Azure Active Directory cihaz kaydı hizmeti, Azure Active Directory ile Kiracı. Başvuru bağlantısı sizi tooa kavramsal konuya götürdüğünde toothis denetim listesi geri kalan görevleri hello ile devam edebilirsiniz böylece daha sonra döndür. Bazı görevler hello adım başarıyla tamamlanıp tamamlanmadığını olup olmadığını onaylayın yardımcı olabilecek bir senaryo doğrulama adımı içerir.

## <a name="part-1-enable-azure-active-directory-device-registration"></a>1. Kısım: Etkinleştir Azure Active Directory cihaz kaydı
Başlangıç denetim listesi tooenable Hello adımları izleyin ve hello Azure Active Directory cihaz Kayıt Hizmeti'ni yapılandırın.

| Görev | Başvuru | 
| --- | --- |
| Azure Active Directory Kiracı tooallow aygıtları toojoin hello çalışma alanınızda cihaz kaydını etkinleştirebilirsiniz. Varsayılan olarak, Azure multi-Factor Authentication hello hizmeti için etkin değil. Ancak, bir cihaz kaydettiğinizde, çok faktörlü kimlik doğrulaması kullanmanızı öneririz. Active Directory kayıt hizmetinde çok faktörlü kimlik doğrulamasını etkinleştirmeden önce AD FS çok faktörlü kimlik doğrulama sağlayıcısı için yapılandırıldığından emin olun. |[Azure Active Directory cihaz kaydı etkinleştirme](active-directory-device-registration-get-started.md)| 
|Cihazlar, iyi bilinen DNS kayıtlarına bakarak, Azure Active Directory cihaz kayıt hizmeti bulur. Böylece, Azure Active Directory cihaz kayıt hizmeti aygıtları bulabilir, şirketinizin DNS yapılandırın. |[Azure Active Directory cihaz kaydı keşfini yapılandırma](active-directory-device-registration-get-started.md)| 


## <a name="part-2-deploy-and-configure-windows-server-2012-r2-active-directory-federation-services-and-set-up-a-federation-relationship-with-azure-ad"></a>2. Kısım: Dağıtın ve Windows Server 2012 R2 Active Directory Federasyon Hizmetleri Yapılandırma ve Azure AD ile bir Federasyon ilişkisi ayarlayın

| Görev | Başvuru |
| --- | --- |
| Active Directory etki alanı Hizmetleri hello Windows Server 2012 R2 şema uzantılarıyla dağıtın. Herhangi bir etki alanı denetleyicileri tooWindows Server 2012 R2'in herhangi bir tooupgrade gerekmez. Merhaba şema yükseltme hello tek gereksinimdir. |[Active Directory etki alanı Hizmetleri şeması yükseltme](#upgrade-your-active-directory-domain-services-schema) |
| Cihazlar, iyi bilinen DNS kayıtlarına bakarak, Azure Active Directory cihaz kayıt hizmeti bulur. Böylece, Azure Active Directory cihaz kayıt hizmeti aygıtları bulabilir, şirketinizin DNS yapılandırın. |[Active Directory destek aygıtlarınızı hazırlama](#prepare-your-active-directory-to-support-devices) |

## <a name="part-3-enable-device-writeback-in-azure-ad"></a>3. Kısım: Etkinleştir cihaz geri yazma özelliğini Azure AD
| Görev | Başvuru |
| --- | --- |
| "Etkinleştirme cihaz geri yazma özelliğini Azure AD Connect." iki bölümü tamamlayın Bu dönüş toothis Kılavuzu tamamladıktan sonra. |[Azure AD Connect’te cihaz geri yazma özelliğini etkinleştirme](#upgrade-your-active-directory-domain-services-schema) |

## <a name="optional-part-4-enable-multi-factor-authentication"></a>[İsteğe bağlı] 4. Kısım: Etkinleştir çok faktörlü kimlik doğrulaması
Hello biri çok faktörlü kimlik doğrulaması için çeşitli Seçenekler yapılandırmanız önerilir. Toorequire çok faktörlü kimlik doğrulamasını istiyorsanız, bkz: [hello çok faktörlü kimlik doğrulaması güvenliği çözümü seçtiğiniz](../multi-factor-authentication/multi-factor-authentication-get-started.md). Her çözüm açıklamasını içerir ve tercih ettiğiniz hello çözümü yapılandırmak toohelp bağlar.

## <a name="part-5-verification"></a>Bölüm 5: doğrulama
Merhaba dağıtımı tamamlanmıştır ve bazı senaryolar deneyebilirsiniz. Aşağıdaki tooexperiment hello hizmetiyle bağlar ve özellikleri ile aşina hello kullanın.

| Görev | Başvuru |
| --- | --- |
| Azure Active Directory cihaz kayıt hizmeti kullanarak bazı cihazlar tooyour çalışma alanına katılma. İOS, Windows ve Android cihazlarını birleştirebilirsiniz. |[Azure Active Directory cihaz kayıt hizmeti kullanarak cihazları tooyour çalışma alanına katılma](#join-devices-to-your-workplace-using-azure-active-directory-device-registration) |
| Görüntülemek ve etkinleştirme veya hello Yönetici portalını kullanarak kayıtlı cihazlarını devre dışı bırakın. Bu görevde, kayıtlı bazı cihazların Merhaba Yönetici portalını kullanarak görüntüleyin. |[Azure Active Directory cihaz kayıt hizmetine genel bakış](active-directory-device-registration-get-started.md) |
| Cihaz nesneleri, Azure Active Directory tooWindows Server Active Directory geri yazılır doğrulayın. |[Kayıtlı cihazlar tooActive dizin geri yazılır doğrulayın](#verify-registered-devices-are-written-back-to-active-directory) |
| Kullanıcılar, cihazlarını kaydedebilir, uygulama oluşturabileceğiniz erişim ilkeleri yalnızca kayıtlı cihazlara izin AD FS'de. Bu görevde, bir uygulama erişim kuralı ve özel bir erişim reddedildi iletisi oluşturun. |[Bir uygulama erişim ilkesi ve özel erişim reddedildi iletisi oluştur](#create-an-application-access-policy-and-custom-access-denied-message) |

## <a name="integrate-azure-active-directory-with-on-premises-active-directory"></a>Azure Active Directory şirket içi Active Directory ile tümleştirme
Bu adım, Azure AD kiracısı Azure AD Connect kullanarak şirket içi Active Directory ile tümleştirmenize yardımcı olur. Merhaba adımları hello Klasik Azure portalında kullanılabilir olsa da, bu bölümde listelenen tüm özel yönergeleri not edin.

1. İçinde toohello Klasik Azure portalı, Azure AD genel yönetici olan bir hesabı kullanarak oturum açın.
2. Merhaba soldaki bölmede bulunan seçin **Active Directory**.
3. Merhaba üzerinde **Directory** sekmesinde, dizininizi seçin.
4. Select hello **dizin tümleştirme** sekmesi.
5. Merhaba altında **dağıtma ve yönetme** bölümünde, 1-3 toointegrate Azure Active Directory ile şirket içi dizininize arası adımları izleyin.
   
   1. Etki alanlarını ekleyin.
   2. Yükleme ve başlangıç yönergeleri kullanarak Azure AD Connect çalıştırma [Azure AD Connect özel yüklemesi](connect/active-directory-aadconnect-get-started-custom.md).
   3. Doğrulayın ve directory eşitleme yönetin. Çoklu oturum açma yönergeleri Bu adımı içinde kullanılabilir.
   
   Ayrıca, Federasyon kısmında özetlendiği gibi AD FS ile yapılandırmak [Azure AD Connect özel yüklemesi](connect/active-directory-aadconnect-get-started-custom.md).

## <a name="upgrade-your-active-directory-domain-services-schema"></a>Active Directory etki alanı Hizmetleri şeması yükseltme
> [!NOTE]
> Active Directory şemanızı yükselttikten sonra hello işlem tersine çevrilemez. Bir test ortamında bir hello yükseltme gerçekleştirmenizi öneririz.
> 

1. Tooyour etki alanı denetleyicisinde kuruluş yöneticisi ve şema yönetici haklarına sahip bir hesapla oturum açın.
2. Kopya hello **[media] \support\adprep** , Active Directory etki alanı denetleyicilerinin dizin ve alt dizinleri tooone (burada **[media]** hello yolu toohello Windows Server 2012 R2 yükleme ortamının ).
4. Bir komut isteminden toohello Git **adprep** dizin ve çalışma **adprep.exe/forestprep**. Merhaba ekrandaki yönergeleri toocomplete hello şema yükseltme izleyin.

## <a name="prepare-your-active-directory-toosupport-devices"></a>Active Directory toosupport aygıtlarınızı hazırlama
> [!NOTE]
> Bu, Active Directory orman toosupport aygıtlarınızı tooprepare çalıştırmalısınız tek seferlik bir işlemdir. toocomplete Bu yordam, kuruluş yöneticisi izinlerine oturum oturum açmanız gerekir ve Active Directory ormanınızın hello Windows Server 2012 R2 şema olması gerekir.
> 


### <a name="prepare-your-active-directory-forest"></a>Active Directory ormanı hazırlama
1. Federasyon sunucunuzda, Windows PowerShell komut penceresi açın ve ardından yazın **Initialize-ADDeviceRegistration**. 
2. İstendiğinde **ServiceAccountName**, AD FS için hello hizmet hesabı olarak seçilen hello hizmet hesabı hello adını girin. GMSA hesabı ise, hello hello hesabını girin **domain\accountname$** biçimi. Bir etki alanı hesabı için hello biçimini kullanın **domain\accountname**.

### <a name="enable-device-authentication-in-ad-fs"></a>AD FS'de cihaz kimlik doğrulamasını etkinleştir
1. Federasyon sunucunuzda, başlangıç AD FS Yönetimi konsolunu açın ve çok Git**AD FS** > **kimlik doğrulama ilkeleri**.
2. Merhaba üzerinde **Eylemler** bölmesinde, **Düzenle Genel birincil kimlik doğrulama**.
3. Denetleme **cihaz kimlik doğrulamasını etkinleştir**ve ardından **Tamam**.
4. Varsayılan olarak, AD FS, kullanılmayan aygıtlarını düzenli olarak Active Directory'den kaldırır. Böylece cihazlar Azure'da yönetilebilir Azure Active Directory cihaz kayıt hizmeti kullanırken bu görevi devre dışı bırakın.

### <a name="disable-unused-device-cleanup"></a>Kullanılmayan cihaz temizleme devre dışı bırak
Federasyon sunucunuzda, Windows PowerShell komut penceresi açın ve ardından yazın **kümesi AdfsDeviceRegistration - MaximumInactiveDays 0**.

### <a name="prepare-azure-ad-connect-for-device-writeback"></a>Cihaz geri yazma için Azure AD Connect'i hazırlama
Bölüm 1 tamamlamak: Azure AD Connect hazırlayın.

## <a name="join-devices-tooyour-workplace-by-using-azure-active-directory-device-registration-service"></a>Azure Active Directory cihaz kayıt hizmeti kullanarak cihazları tooyour çalışma alanına katılma

### <a name="join-an-ios-device-by-using-azure-active-directory-device-registration"></a>Azure Active Directory cihaz kaydı kullanarak bir iOS aygıtı birleştirme
Azure Active Directory cihaz kaydı iOS cihazları için hello Over-the-Air profili kayıt işlemi kullanır. Merhaba kullanıcı toohello profil kayıt URL'si ile Safari bağlandığında, bu işlemi başlar. Merhaba URL biçimi aşağıdaki gibidir:

    https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/"yourdomainname"

Bu durumda, `yourdomainname` , Azure Active Directory ile yapılandırdığınız hello etki alanı adıdır. Etki alanı adınız contoso.com ise, örneğin, hello URL aşağıdaki gibidir:

    https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/contoso.com

Bu URL tooyour kullanıcılar birçok farklı şekillerde toocommunicate vardır. Örneğin, bir yöntem öneririz bu URL'yi AD FS'de bir özel uygulama erişim reddedildi iletisi yayımlama. Bu bilgiler hello ilerideki bölümde kapsanmaktadır [bir uygulama erişim ilkesi ve özel erişim reddedildi iletisi Oluştur](#create-an-application-access-policy-and-custom-access-denied-message).

### <a name="join-a-windows-81-device-by-using-azure-active-directory-device-registration"></a>Azure Active Directory cihaz kaydı kullanarak bir Windows 8.1 cihaz birleştirme
1. Windows 8.1 Cihazınızı seçin **PC Ayarları** > **ağ** > **çalışma alanına**.
2. Kullanıcı adınızı UPN biçiminde girin; Örneğin,  **dan@contoso.com** .
3. Seçin **katılma**.
4. İstendiğinde, kimlik bilgilerinizle oturum açın. Merhaba aygıt artık birleştirilir.

### <a name="join-a-windows-7-device-by-using-azure-active-directory-device-registration"></a>Azure Active Directory cihaz kaydı kullanarak bir Windows 7 aygıtı birleştirme
tooregister Windows 7 etki alanına katılmış aygıtlar toodeploy hello cihaz kayıt yazılım paketini gerekir. Merhaba yazılım paketini Windows 7 için çalışma alanına katılma ve buna ait hello adresten kullanılabilir olarak adlandırılır [Microsoft Connect Web](https://connect.microsoft.com/site1164). 

Nasıl toouse hello paketi ile ilgili yönergeler bulunan [nasıl tooconfigure otomatik kayıt Windows etki alanına katılmış cihazları Azure Active Directory ile](active-directory-conditional-access-automatic-device-registration-setup.md).

## <a name="verify-that-registered-devices-are-written-back-tooactive-directory"></a>Kayıtlı cihazlar tooActive dizin geri yazılır doğrulayın
Görüntüleyebilir ve aygıt nesneleri geri tooyour Active Directory LDP.exe veya ADSI Düzenleyicisi kullanılarak yazılan olduğunu doğrulayın. Her ikisi de hello Active Directory Yöneticisi Araçları ile kullanılabilir.

Varsayılan olarak, Azure Active Directory'den geri yazılır aygıt nesneleri hello aynı yerleştirilir AD FS grubunuzu olarak etki alanı.

    CN=RegisteredDevices,defaultNamingContext

## <a name="create-an-application-access-policy-and-custom-access-denied-message"></a>Bir uygulama erişim ilkesi ve özel erişim reddedildi iletisi oluştur
Senaryo aşağıdaki hello göz önünde bulundurun: AD FS'de bağlı taraf güveni uygulama oluşturma ve yalnızca kayıtlı cihazlara izin veren bir verme yetkilendirme kuralı yapılandırın. Artık yalnızca kayıtlı cihazlar tooaccess Merhaba uygulaması izin verilir. 

toomake hakkında yönergeler içeren bir özel erişim reddedildi iletisi, kullanıcıların toogain erişim toohello uygulamanız için kolay, yapılandırdığınız toojoin cihazlarını. Artık bir uygulama erişebilmesi kullanıcılarınızın cihazlarını sorunsuz şekilde tooregister sahipsiniz.

Merhaba aşağıdaki adımlarda size yol gösterecektir tooimplement bu senaryo.

> [!NOTE]
> Bu bölümde, zaten bir bağlı olan taraf güveni için AD FS uygulamanızda yapılandırmış olduğunuz varsayılır.
> 

1. Merhaba AD FS MMC aracını açın ve ardından **AD FS** > **güven ilişkileri** > **bağlı olan taraf güvenleri**.
2. Yeni erişim kuralın uygulanacağı hello uygulama toowhich bulun. Merhaba uygulamaya sağ tıklayın ve ardından **talep kurallarını Düzenle**.
3. Select hello **verme yetkilendirme kuralları** sekmesini tıklatın ve ardından **Kuralı Ekle**.
4. Merhaba gelen **talep kuralı** şablonu aşağı açılan listesinden, **göre izin ver veya Reddet kullanıcılar bir gelen talep**. Ardından **sonraki**.
5. Merhaba, **talep kuralı adı** alanında, yazın **kayıtlı cihazlardan erişim izin**.
6. Merhaba gelen **gelen talep türü** aşağı açılan listesinden, **kayıtlı kullanıcı**.
7. Merhaba, **gelen talep değeri** alanında, yazın **doğru**.
8. Select hello **izin erişim toousers bu gelen talep ile** radyo düğmesi.
9. Seçin **son**ve ardından **Uygula**.
10. Oluşturduğunuz hello kural daha fazla izin veren herhangi bir kuralın kaldırın. Örneğin, hello varsayılan kuralı kaldırmak **erişilmesine tooall kullanıcılar**.

Yapılandırılmış tooallow erişim artık yalnızca kayıtlı ve toohello çalışma alanına katılmış bir CİHAZDAN hello kullanıcı çıkarken, uygulamasıdır. Daha gelişmiş erişim ilkeleri için bkz: [duyarlı uygulamalar için ek multi Factor Authentication ile Risk Yönetimi](https://technet.microsoft.com/library/dn280949.aspx).

Ardından, uygulamanız için bir özel hata iletisi yapılandırın. Merhaba hata iletisi hello uygulamaya erişebilmeniz bunlar kendi cihaz toohello çalışma alanına katılmalı bilmenize olanak sağlar. Özel HTML ve PowerShell kullanarak bir özel uygulama erişim reddedildi iletisi oluşturabilirsiniz.

Federasyon sunucunuzda bir PowerShell komut penceresi açın ve ardından komut aşağıdaki hello yazın. Merhaba komutu bölümlerini belirli tooyour sistem öğeleri ile değiştirin:

    Set-AdfsRelyingPartyWebContent -Name "relying party trust name" -ErrorPageAuthorizationErrorMessage
Bu uygulamaya erişebilmeniz için Cihazınızı kaydetmeniz gerekir.

**İOS cihazı kullanıyorsanız, bu bağlantı toojoin Cihazınızı seçin**:

    a href='https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/yourdomain.com

Bu iOS aygıtı tooyour çalışma alanına katılma.

Windows 8.1 cihaz kullanıyorsanız, seçerek Cihazınızı katılabilirsiniz **PC Ayarları**> **ağ** > **çalışma alanına**.

Komutları, önceki hello içinde **bağlı olan taraf güven adı** AD FS'de, uygulamanızın bağlı olan taraf güven nesnesi hello adıdır.
Ve **etkialaniniz.com** Azure Active Directory (örneğin, contoso.com) ile yapılandırdığınız hello etki alanı adıdır.
Tüm satır sonlarını (varsa) HTML hello toohello geçirdiğiniz içeriği emin tooremove olması **kümesi AdfsRelyingPartyWebContent** cmdlet'i.

Artık kullanıcılar hello Azure Active Directory cihaz kayıt hizmeti ile kayıtlı olmayan bir aygıt, uygulamanızın eriştiğinde, aşağıdaki ekran görüntüsüne benzer toohello benzeyen bir sayfasına bakın.

![Kullanıcıların cihazlarını Azure AD ile kayıtlı olmayabilirsiniz çalıştığında hatayla ekran görüntüsü](./media/active-directory-conditional-access/error-azureDRS-device-not-registered.gif)


