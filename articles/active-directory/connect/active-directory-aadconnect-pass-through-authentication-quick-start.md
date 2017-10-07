---
title: "Azure AD doğrudan kimlik doğrulama - hızlı başlangıç | Microsoft Docs"
description: "Bu makale, Azure Active Directory (Azure AD) doğrudan kimlik doğrulaması ile tooget nasıl başlatılacağını açıklar."
services: active-directory
keywords: "Azure AD Connect doğrudan kimlik doğrulama, Active Directory yükleyin gerekli bileşenleri Azure AD, SSO, çoklu oturum açma"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: billmath
ms.openlocfilehash: d6d0f85fe144cf36cc94676f6592d37988b20647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-quick-start"></a>Azure Active Directory doğrudan kimlik doğrulaması: Hızlı Başlangıç

## <a name="how-toodeploy-azure-ad-pass-through-authentication"></a>Nasıl toodeploy Azure AD doğrudan kimlik doğrulama

Azure Active Directory (Azure AD) doğrudan kimlik doğrulaması, kullanıcıların toosign tooboth şirket içi sağlar ve aynı parolayı kullanarak bulut tabanlı uygulamaları hello. Bu kullanıcıların parolalarını şirket içi Active Directory'nizi karşı doğrudan doğrulayarak açmaktadır.

>[!IMPORTANT]
>Azure AD doğrudan kimlik doğrulama şu anda önizlemede değil. Bu özellik Önizleme aracılığıyla kullanmakta olduğunuz, Önizleme sürümleri hello kimlik doğrulaması aracıları yükseltme hello yönergelerini kullanarak olmanız gerekir [burada](./active-directory-aadconnect-pass-through-authentication-upgrade-preview-authentication-agents.md).

Bu yönergeler toodeploy doğrudan kimlik doğrulama toofollow gerekir:

## <a name="step-1-check-prerequisites"></a>1. adım: Önkoşul denetimi

Önkoşullar aşağıdaki o hello yerinde olduğundan emin olun:

### <a name="on-hello-azure-active-directory-admin-center"></a>Hello Azure Active Directory Yönetim Merkezi'nde

1. Azure AD kiracınıza bir yalnızca bulut genel yönetici hesabı oluşturun. Bu şekilde, şirket içi hizmetlerinizi başarısız veya kullanılamaz hale kiracınızın hello yapılandırmasını yönetebilirsiniz. Hakkında bilgi edinin [bir yalnızca bulut genel yönetici hesabı ekleme](../active-directory-users-create-azure-portal.md). Bu adımı gerçekleştirmeden Kiracı, erişebilmenizin kritik tooensure olur.
2. Bir veya daha fazla Ekle [özel etki alanı adları](../active-directory-add-domain.md) tooyour Azure AD Kiracı. Kullanıcılarınız, bu etki alanı adlarından birini kullanarak oturum açın.

### <a name="in-your-on-premises-environment"></a>Şirket içi ortamınızda

1. Windows Server 2012 R2 veya daha sonra hangi toorun üzerinde Azure AD Connect çalıştıran bir sunucu tanımlayın. Merhaba sunucu toohello aynı AD ormanı parolaları toobe doğrulanması gereken hello kullanıcılar olarak ekleyin.
2. Merhaba yüklemek [Azure AD Connect'in en son sürümünü](https://www.microsoft.com/download/details.aspx?id=47594) önceki adımda belirlediğiniz hello sunucusunda. Azure AD Connect çalışan zaten varsa o hello sürümün 1.1.557.0 olduğundan emin olun veya sonraki bir sürümü.
3. Windows Server 2012 R2 çalıştıran ek bir sunucu tanımlayın veya tek başına kimlik doğrulama Aracısı bir sonraki hangi toorun. Merhaba kimlik doğrulama Aracısı sürümü gereken toobe 1.5.193.0 veya sonraki bir sürümü. Gerekli tooensure yüksek kullanılabilirlik, oturum açma isteklerinin sunucusudur. Merhaba sunucu toohello aynı AD ormanı parolaları toobe doğrulanması gereken hello kullanıcılar olarak ekleyin.
4. Sunucular ve Azure AD arasında bir güvenlik duvarı varsa, aşağıdaki öğelerindeki tooconfigure hello gerekir:
   - Kimlik Doğrulama Aracısı yaptığınızdan emin olun **giden** tooAzure AD bağlantı noktaları aşağıdaki hello ister:
   
   | Bağlantı noktası numarası | Nasıl kullanılır |
   | --- | --- |
   | **80** | İndirme sertifika iptal listeleri (CRL'ler hello SSL sertifikası doğrulanırken) |
   | **443** | Tüm giden iletişim hizmetimizdeki |
   
   Güvenlik duvarını toooriginating kullanıcılar göre kuralları zorlar, ağ hizmeti olarak çalışan Windows hizmetlerinden trafik için bu bağlantı noktalarını açın.
   - Güvenlik Duvarı veya proxy DNS uygulamaları, da beyaz liste bağlantıları güvenilir listeye almayı çok izin veriyorsa**\*. msappproxy.net** ve  **\*. servicebus.windows.net**. Aksi takdirde, çok erişime[Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/details.aspx?id=41653), hangi haftalık güncelleştirildi.
   - Kimlik doğrulama aracılarınızı çok erişmeniz**login.windows.net** ve **login.microsoftonline.com** ilk kaydı için bu URL'ler için için Güvenlik Duvarı'nı açın.
   - Sertifika doğrulama için aşağıdaki URL'lere hello engellemesini: **mscrl.microsoft.com:80**, **crl.microsoft.com:80**, **ocsp.msocsp.com:80** ve  **www.microsoft.com:80**. Engeli kaldırılmış bu URL'leri zaten olabilir şekilde bu URL'leri diğer Microsoft ürünleri ile sertifika doğrulaması için kullanılır.

## <a name="step-2-enable-exchange-activesync-support-optional"></a>2. adım: Exchange ActiveSync desteği (isteğe bağlı) etkinleştir

Bu yönergeler tooenable Exchange ActiveSync desteği izleyin:

1. Kullanım [Exchange PowerShell](https://technet.microsoft.com/library/mt587043(v=exchg.150).aspx) komutu aşağıdaki toorun hello:
```
Get-OrganizationConfig | fl per*
```

2. Merhaba Hello değerini denetleyin `PerTenantSwitchToESTSEnabled` ayarı. Merhaba değer ise **doğru**, kiracınızın'ın düzgün yapılandırıldığından - bu genellikle hello çoğu müşteri için bir durumdur. Merhaba değer ise **false**çalıştırın hello komutu aşağıdaki:
```
Set-OrganizationConfig -PerTenantSwitchToESTSEnabled:$true
```

3. Merhaba, hello değerini doğrulayın `PerTenantSwitchToESTSEnabled` şimdi ayar çok**doğru**. Taşıma toohello sonraki adıma önce bir saat bekleyin.

Bu adım sırasında sorunları yüz, denetleyin bizim [sorun giderme kılavuzu](active-directory-aadconnect-troubleshoot-pass-through-authentication.md#exchange-activesync-configuration-issues) daha fazla bilgi için.

## <a name="step-3-enable-hello-feature"></a>3. adım: hello özelliğini etkinleştir

Doğrudan kimlik doğrulama kullanarak etkinleştirilebilir [Azure AD Connect](active-directory-aadconnect.md).

>[!IMPORTANT]
>Doğrudan kimlik doğrulama hello Azure AD Connect birincil veya hazırlama sunucusunda etkinleştirilebilir. Merhaba birincil sunucudan etkinleştirmeniz önerilir.

Azure AD Connect hello için ilk kez yüklüyorsanız, hello seçin [özel yükleme yolu](active-directory-aadconnect-get-started-custom.md). Merhaba, **kullanıcı oturum açma** sayfasında, **doğrudan kimlik doğrulama** oturum yöntemi hello gibi. Başarılı tamamlanma hello üzerinde doğrudan kimlik doğrulama aracısı yüklü Azure AD Connect ile aynı sunucu. Ayrıca, hello doğrudan kimlik doğrulama özelliği, Kiracı'etkindir.

![Azure AD Connect - kullanıcı oturum açma](./media/active-directory-aadconnect-sso/sso3.png)

Azure AD Connect zaten yüklü değilse (hello kullanarak [hızlı yükleme](active-directory-aadconnect-get-started-express.md) veya hello [özel yükleme](active-directory-aadconnect-get-started-custom.md) yol) seçin **değişiklik kullanıcı oturum açma sayfası** Azure AD hakkında Bağlayın ve tıklatın **sonraki**. Ardından **doğrudan kimlik doğrulama** oturum yöntemi hello gibi. Başarılı tamamlanma hello üzerinde doğrudan kimlik doğrulama aracısı yüklü Azure AD Connect ve hello özelliği aynı sunucu üzerinde Kiracı etkindir.

![Azure AD Connect - değişiklik kullanıcı oturum açma](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

>[!IMPORTANT]
>Doğrudan kimlik doğrulaması, bir kiracı düzeyi özelliğidir. Açma etkiler oturum açma için kullanıcıları arasında _tüm_ hello yönetilen Kiracı etki alanlarında. AD FS kimlik tooPass aracılığıyla geçiş yapıyorsanız, öneririz, AD FS altyapınızın kapatılmadan önce en az 12 saat bekleyin - geçişi sırasında imzalama tutmak kullanıcıların tooExchange ActiveSync tooensure bu bekleme zamanı.

## <a name="step-4-test-hello-feature"></a>4. adım: Test hello özelliği

Doğrudan kimlik doğrulama doğru etkinleştirdiyseniz bu yönergeleri tooverify izleyin:

1. İçinde toohello oturum [Azure Active Directory Yönetim Merkezi](https://aad.portal.azure.com) hello kiracınız için genel yönetici kimlik bilgileriyle.
2. Seçin **Azure Active Directory** hello sol gezinti çubuğunda.
3. Seçin **Azure AD Connect**.
4. Bu hello doğrulayın **doğrudan kimlik doğrulama** özelliği gösterildiğinden **etkin**.
5. Seçin **doğrudan kimlik doğrulama**. Bu dikey kimlik doğrulaması aracılarınızı yüklendiği hello sunucuları listeler.

![Azure Active Directory Yönetim Merkezi - Azure AD Connect dikey penceresi](./media/active-directory-aadconnect-pass-through-authentication/pta7.png)

![Azure Active Directory Yönetim Merkezi - doğrudan kimlik doğrulama dikey penceresi](./media/active-directory-aadconnect-pass-through-authentication/pta8.png)

Bu aşamada, etki alanlarındaki kullanıcılar tüm yönetilen kiracınızda doğrudan kimlik doğrulaması kullanarak oturum açabilirsiniz. Ancak, Federasyon etki alanlarındaki kullanıcılar Active Directory Federasyon Hizmetleri (AD FS) ya da daha önce yapılandırdığınız başka bir Federasyon sağlayıcı kullanarak toosign devam edin. Bir etki Federasyon toomanaged dönüştürürseniz, o etki alanındaki tüm kullanıcıların geçişli kimlik doğrulaması kullanarak oturum açmayı otomatik olarak başlar. Yalnızca bulut kullanıcıları hello doğrudan kimlik doğrulama özelliği tarafından etkilenmez.

## <a name="step-5-ensure-high-availability"></a>5. adım: yüksek oranda kullanılabilirlik emin olun

Bir üretim ortamında toodeploy doğrudan kimlik doğrulama planlıyorsanız, tek başına bir kimlik doğrulama aracısını yüklemeniz gerekir. Bu ikinci kimlik doğrulama Aracısı bir sunucuya yüklemek _diğer_ bir çalışan Azure AD Connect hello ve ilk kimlik doğrulama Aracısı hello çok. Bu kurulum, yüksek kullanılabilirlik, oturum açma isteklerinin sağlar. Bu yönergeler toodeploy tek başına bir kimlik doğrulama Aracısı izleyin:

1. **Hello hello kimlik doğrulama Aracısı en son sürümünü indirin (sürümleri 1.5.193.0 veya sonrası)**: toohello içinde oturum [Azure Active Directory Yönetim Merkezi](https://aad.portal.azure.com) , kiracının genel yönetici kimlik bilgilerine sahip.
2. Seçin **Azure Active Directory** hello sol gezinti çubuğunda.
3. Seçin **Azure AD Connect** ve ardından **doğrudan kimlik doğrulama**. Seçip **Yükleme Aracısı**.
4. Merhaba tıklatın **koşullarını kabul & Yükle** düğmesi.
5. **Merhaba hello kimlik doğrulama Aracısı en son sürümünü yüklemek**: Çalıştır hello yürütülebilir indirilen adım önceki hello. İstendiğinde, kiracının genel Yöneticisi kimlik bilgilerini sağlayın.

![Azure Active Directory Yönetim Merkezi - kimlik doğrulama Aracısı Yükle düğmesi](./media/active-directory-aadconnect-pass-through-authentication/pta9.png)

![Azure Active Directory Yönetim Merkezi - aracıyı indir dikey penceresi](./media/active-directory-aadconnect-pass-through-authentication/pta10.png)

>[!NOTE]
>Ayrıca indirebilirsiniz kimlik doğrulama Aracısı'ndan hello [burada](https://aka.ms/getauthagent). Gözden geçirin ve hello kimlik doğrulama Aracısı'nın kabul olun [hizmet koşulları](https://aka.ms/authagenteula) _önce_ yükleme.

## <a name="next-steps"></a>Sonraki adımlar
- [**Geçerli sınırlamalar** ](active-directory-aadconnect-pass-through-authentication-current-limitations.md) -bu özellik şu anda önizlemede değil. Hangi senaryoları desteklenir ve hangilerinin olmayan öğrenin.
- [**Teknik derinlemesine** ](active-directory-aadconnect-pass-through-authentication-how-it-works.md) -bu özellik nasıl çalıştığını anlayın.
- [**Sık sorulan sorular** ](active-directory-aadconnect-pass-through-authentication-faq.md) -toofrequently sorular yanıtlanmaktadır.
- [**Sorun giderme** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -tooresolve ortak hello özelliğiyle nasıl sorunları öğrenin.
- [**Azure AD sorunsuz SSO** ](active-directory-aadconnect-sso.md) -tamamlayıcı bu özellik hakkında daha fazla bilgi edinin.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - yeni özellik istekleri dosyalama için.
