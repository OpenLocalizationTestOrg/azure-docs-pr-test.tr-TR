---
title: "Office 365 ve Azure AD kullanıcıları için aaaCertificate yenileme | Microsoft Docs"
description: "Bu makalede tooOffice 365 kullanıcıların nasıl tooresolve bir sertifika yenileme hakkında bildirim e-postaları sorunlar açıklanmaktadır."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 543b7dc1-ccc9-407f-85a1-a9944c0ba1be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b9b309e06949dc5488cd628650be413f366ed347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="renew-federation-certificates-for-office-365-and-azure-active-directory"></a>Office 365 ve Azure Active Directory Federasyon sertifikalarını yenileme
## <a name="overview"></a>Genel Bakış
Azure Active Directory (Azure AD) ve Active Directory Federasyon Hizmetleri (AD FS) arasındaki başarılı Federasyon için Azure AD içinde yapılandırılmış AD FS toosign güvenlik belirteçleri tooAzure AD tarafından kullanılan hello sertifikaları eşleşmesi gerekir. Öğelerdeki uyuşmazlık toobroken güven yol açabilir. Azure AD, AD FS ve Web uygulama proxy'si (extranet erişimi için) dağıtırken bu bilgileri eşitlenmiş olarak saklanmasını sağlar.

Bu makalede, belirteç imzalama sertifikalarının, ek bilgi toomanage sağlar ve aşağıdaki durumlarda hello bunları Azure AD ile eşitlenmiş tut:

* Hello Web uygulaması Ara sunucusu dağıtma değil ve bu nedenle hello Federasyon meta verileri hello extranet mevcut değil.
* AD FS hello varsayılan yapılandırması için belirteç imzalama sertifikalarının kullanarak değil.
* Bir üçüncü taraf kimlik sağlayıcısı kullanıyor.

## <a name="default-configuration-of-ad-fs-for-token-signing-certificates"></a>AD FS belirteç imzalama sertifikaları için varsayılan yapılandırma
Merhaba belirteç imzalama ve belirteç şifre çözme sertifikaları genellikle otomatik olarak imzalanan sertifikalar ve bir yıl için iyidir. Varsayılan olarak, AD FS adlı bir otomatik yenileme işlemi içerir **AutoCertificateRollover**. Otomatik olarak AD FS 2.0 veya üstü, Office 365 ve Azure AD kullanıyorsanız, sertifikanızın süresi dolmadan önce güncelleştirin.

### <a name="renewal-notification-from-hello-office-365-portal-or-an-email"></a>Yenileme bildirim hello Office 365 portalı ya da bir e-posta
> [!NOTE]
> Bir e-posta veya toorenew soran bir portal bildirim alındı sertifikanızı Office için bkz: [yönetme değişiklikleri imzalama sertifikalarının tootoken](#managecerts) herhangi bir eylem tootake gerekiyorsa toocheck. Microsoft, hiçbir eylem gerekli olduğunda bile, gönderilen sertifika yenileme toonotifications yol açabilecek olası bir sorunu bilmektedir.
>
>

Azure AD toomonitor hello Federasyon meta verileri ve güncelleştirme hello belirteç imzalama sertifikaları bu meta verileri tarafından belirtildiği şekilde çalışır. 30 gün önce hello belirteç imzalama sertifikalarının, sona erme tarihi hello Azure AD hello Federasyon meta verileri yoklayarak yeni sertifikalar kullanılabilir olup olmadığını denetler.

* Bu başarılı şekilde hello Federasyon meta verileri sorgulamak ve hello yeni sertifika almak, e-posta bildirim veya uyarı hello Office 365 portalında toohello kullanıcı verilir.
* Merhaba yeni belirteç imzalama sertifikalarının alamıyorsa, ya da hello Federasyon meta verileri ulaşılabilir olmadığından veya otomatik sertifika aktarma etkin değil, Azure AD bir e-posta bildirimi ve hello Office 365 Portalı'nda bir uyarı verir.

![Office 365 portalı bildirim](./media/active-directory-aadconnect-o365-certs/notification.png)

> [!IMPORTANT]
> AD FS, tooensure iş sürekliliği, kullanıyorsanız Lütfen sunucularınızı bilinen sorunlara yönelik kimlik doğrulama hatalarının meydana gelmediğinden emin şu güncelleştirmeleri hello sahip olduğunuzu doğrulayın. Bu yenileme ve gelecekteki yenileme dönemleri için bilinen AD FS proxy sunucu sorunları azaltır:
>
> Server 2012 R2 - [Windows Server Mayıs 2014 paketi](http://support.microsoft.com/kb/2955164)
>
> Server 2008 R2 ve 2012 - [proxy üzerinden kimlik doğrulaması başarısız Windows Server 2012 veya Windows 2008 R2 SP1](http://support.microsoft.com/kb/3094446)
>
>

## Merhaba sertifikaları güncelleştirilmiş toobe gerekip gerekmediğini denetleyin<a name="managecerts"></a>
### <a name="step-1-check-hello-autocertificaterollover-state"></a>1. adım: Merhaba AutoCertificateRollover durumunu denetle
AD FS sunucunuzda, PowerShell'i açın. Merhaba AutoCertificateRollover değeri tooTrue ayarlanmış olduğundan emin olun.

    Get-Adfsproperties

![AutoCertificateRollover](./media/active-directory-aadconnect-o365-certs/autocertrollover.png)

>[!NOTE] 
>AD FS 2.0 kullanıyorsanız, önce Ekle-Pssnapın Microsoft.Adfs.Powershell çalıştırın.

### <a name="step-2-confirm-that-ad-fs-and-azure-ad-are-in-sync"></a>2. adım: AD FS ile Azure AD eşitleme olduğundan emin olun
AD FS sunucunuzun hello Azure AD PowerShell komut istemini açın ve tooAzure AD connect.

> [!NOTE]
> Azure AD PowerShell indirebilirsiniz [burada](https://technet.microsoft.com/library/jj151815.aspx).
>
>

    Connect-MsolService

AD FS Hello sertifikaları yapılandırılmış ve etki alanı hello Azure AD güven özelliklerinde belirtilen denetleyin.

    Get-MsolFederationProperty -DomainName <domain.name> | FL Source, TokenSigningCertificate

![Get-MsolFederationProperty](./media/active-directory-aadconnect-o365-certs/certsync.png)

Merhaba parmak izleri hem de çıkış hello varsa eşleşme sertifikalarınızı Azure AD ile eşitlenmiş.

### <a name="step-3-check-if-your-certificate-is-about-tooexpire"></a>3. adım: sertifikanızı hakkında tooexpire olup olmadığını denetleyin
Başlangıç tarihi altında "Değil sonra" Get-MsolFederationProperty veya Get-AdfsCertificate Hello çıktısında denetle Başlangıç tarihi 30 günden az hemen ise, eylemi gerçekleştirmelisiniz.

| AutoCertificateRollover | Sertifikaları Azure AD ile eşitleme | Federasyon meta verileri genel olarak erişilebilir | Geçerlilik | Eylem |
|:---:|:---:|:---:|:---:|:---:|
| Evet |Evet |Evet |- |Eyleme gerek yok. Bkz: [yenileme belirteç imzalama sertifikası otomatik olarak](#autorenew). |
| Evet |Hayır |- |15 günden az |Hemen yenileyin. Bkz: [el ile yenileme belirteç imzalama sertifikası](#manualrenew). |
| Hayır |- |- |30 günden az |Hemen yenileyin. Bkz: [el ile yenileme belirteç imzalama sertifikası](#manualrenew). |

\[-] Önemli değildir

## Merhaba belirteç imzalama sertifikası otomatik olarak yenilemek (önerilir)<a name="autorenew"></a>
Merhaba aşağıdaki her ikisi de doğruysa tooperform el ile adımlar gerekmez:

* Merhaba extranet erişimi toohello Federasyon meta verilerini etkinleştirebilirsiniz Web uygulaması proxy'si dağıtmış.
* Merhaba AD FS varsayılan yapılandırması (AutoCertificateRollover etkin) kullanıyor.

Sertifika hello tooconfirm aşağıdaki onay hello otomatik olarak güncelleştirilebilir.

**1. hello AD FS özelliği AutoCertificateRollover tooTrue ayarlamanız gerekir.** Bu, AD FS yeni belirteç imzalama ve belirteç şifre çözme sertifikaları hello eski olanları sona önce otomatik olarak oluşturur gösterir.

**2. hello AD FS federasyon meta verileri genel olarak erişilebilir.** Toohello giderek Federasyon meta verileri genel olarak erişilebilir olduğundan emin olun URL bir bilgisayardan aşağıdaki hello ortak Internet (dışına hello şirket ağı):

https:// (your_FS_name) /federationmetadata/2007-06/federationmetadata.xml

Burada `(your_FS_name) `kuruluşunuzun kullandığı, fs.contoso.com gibi hello Federasyon Hizmeti ana bilgisayar adı ile değiştirilir.  Mümkün tooverify varsa bu ayarları başarıyla da toodo başka bir şey yok.  

Örnek: https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml

## Merhaba belirteç imzalama sertifikasını el ile yenileme<a name="manualrenew"></a>
El ile Merhaba belirteç imzalama sertifikaları toorenew tercih edebilirsiniz. Örneğin, hello aşağıdaki senaryolarda daha iyi el ile yenileme için çalışabilir:

* Belirteç imzalama sertifikalarının otomatik olarak imzalanan sertifikalar. Merhaba en yaygın nedeni bu, kuruluşunuzun AD FS sertifikalarının bir kuruluş sertifika yetkilisinden kayıtlı yönetir olmasıdır.
* Ağ güvenliği hello Federasyon meta verileri toobe genel kullanıma açık izin vermiyor.

Merhaba belirteç imzalama sertifikalarının, güncelleştirdiğiniz her sefer bu senaryolarda da Office 365 etki alanınızın hello PowerShell komutu, güncelleştirme MsolFederatedDomain kullanarak güncelleştirmeniz gerekir.

### <a name="step-1-ensure-that-ad-fs-has-new-token-signing-certificates"></a>1. adım: AD FS yeni bir belirteç imzalama sertifikalarının sahip olduğundan emin olun.
**Varsayılan olmayan yapılandırma**

Varsayılan olmayan yapılandırma AD FS kullanıyorsanız, (burada **AutoCertificateRollover** çok ayarlanır**False**), büyük olasılıkla özel sertifikaları (kendinden imzalı) kullanıyor. Nasıl toorenew hello AD FS belirteç imzalama sertifikaları hakkında daha fazla bilgi için bkz: [yönergeler AD FS kullanmayan müşterileri için otomatik olarak imzalanan sertifikalar](https://msdn.microsoft.com/library/azure/JJ933264.aspx#BKMK_NotADFSCert).

**Federasyon meta veri genel kullanıma açık değil**

Üzerinde hello diğer yandan, **AutoCertificateRollover** çok ayarlanır**doğru**, ancak, Federasyon meta verileri genel olarak erişilebilir değil, öncelikle yeni belirteç imzalama sertifikaları AD tarafından oluşturulan olduğundan emin olun FS. Yeni bir belirteç imzalama sertifikalarının tarafından alma hello aşağıdaki adımları sahip onaylayın:

1. Toohello birincil AD FS sunucusuna kaydedildiğini doğrulayın.
2. Merhaba geçerli imzalama sertifikalarının, AD FS'de bir PowerShell komut penceresini açma ve komut aşağıdaki hello çalıştıran denetleyin:

    PS C:\>Get-ADFSCertificate – Encryption belirteç imzalama

   > [!NOTE]
   > AD FS 2.0 kullanıyorsanız, Add-Pssnapın Microsoft.Adfs.Powershell ilk çalıştırmanız gerekir.
   >
   >
3. Listelenen herhangi bir sertifika hello komutu çıktıyı bakın. AD FS yeni bir sertifika oluşturmuşsa hello çıktısında iki sertifika görmeniz gerekir: biri hangi hello **IsPrimary** değer **True** ve hello **NotAfter** tarihi 5 gün ve biri için hangi içinde **IsPrimary** olan **False** ve **NotAfter** hello gelecekteki yılda hakkındadır.
4. Yalnızca bir sertifika görürseniz ve hello **NotAfter** tarihi 5 gün içinde toogenerate yeni bir sertifika gerekir.
5. toogenerate yeni bir sertifika yürütme komut bir PowerShell komut isteminde aşağıdaki hello: `PS C:\>Update-ADFSCertificate –CertificateType token-signing`.
6. Komut yeniden aşağıdaki hello çalıştırarak Hello güncelleştirme doğrulayın: PS C:\>Get-ADFSCertificate – Encryption belirteç imzalama

İki sertifika artık listelenir, bunlardan biri olan bir **NotAfter** yaklaşık bir yıl hello gelecekteki ve hangi hello tarihi **IsPrimary** değer **False**.

### <a name="step-2-update-hello-new-token-signing-certificates-for-hello-office-365-trust"></a>2. adım: hello yeni belirteç imzalama sertifikalarının hello Office 365 güven güncelleştirmek
Office 365 gibi hello güven için kullanılan hello yeni belirteç imzalama sertifikaları toobe ile güncelleştirin.

1. Merhaba Microsoft Azure Active Directory için Windows PowerShell modülü açın.
2. $Cred Çalıştır Get-Credential =. Bu cmdlet, kimlik bilgilerini ister, bulut hizmet yönetici hesabı kimlik bilgilerini yazın.
3. Connect MsolService Çalıştır – kimlik bilgisi $cred. Bu cmdlet toohello bulut hizmetine bağlanır. Bağlanan bir içeriği toohello bulut hizmeti oluşturuluyor hello aracı tarafından yüklenen hello ek cmdlet'lerinden herhangi birini çalıştırmadan önce gereklidir.
4. Bu komutlar hello AD FS birincil Federasyon sunucusu olmayan bir bilgisayar üzerinde çalıştırıyorsanız, Set-MSOLAdfscontext Çalıştır-bilgisayar <AD FS primary server>, burada <AD FS primary server> hello iç FQDN hello birincil AD FS sunucusunun adıdır. Bu cmdlet, bağlanan bir içeriği tooAD FS oluşturur.
5. Güncelleştirme MSOLFederatedDomain – DomainName çalıştırmak <domain>. Bu cmdlet hello bulut hizmeti içine AD FS hello ayarlarını güncelleştirir ve hello hello iki arasında güven ilişkisi yapılandırır.

> [!NOTE]
> Contoso.com ve fabrikam.com, gibi birden çok üst düzey etki toosupport gerekiyorsa hello kullanmalısınız **SupportMultipleDomain** geçiş herhangi cmdlet'lerle. Daha fazla bilgi için bkz: [birden çok üst düzey etki alanı için destek](active-directory-aadconnect-multiple-domains.md).
>
>

## Azure AD Connect kullanarak Azure AD güvenini Onar<a name="connectrenew"></a>
Azure AD Connect kullanarak AD FS grubu ve Azure AD güveni yapılandırdıysanız, belirteç imzalama sertifikaları için herhangi bir eylem tootake gerekiyorsa, Azure AD Connect toodetect kullanabilirsiniz. Toorenew hello sertifikalar gerekiyorsa, Azure AD Connect toodo şekilde kullanabilirsiniz.

Daha fazla bilgi için bkz: [hello güven onarma](active-directory-aadconnect-federation-management.md).
