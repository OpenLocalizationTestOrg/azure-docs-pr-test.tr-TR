---
title: "Azure AD Connect: Hesapları ve izinleri | Microsoft Docs"
description: "Bu konuda kullanılan ve oluşturulan hello hesapları ve gereken izinler açıklanmaktadır."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.reviewer: cychua
ms.assetid: b93e595b-354a-479d-85ec-a95553dd9cc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: 70a7013e0353d74714ec8a3ff54b3e811789a0b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-accounts-and-permissions"></a>Azure AD Connect: Hesapları ve izinleri
Hello Azure AD Connect Yükleme Sihirbazı'nı iki farklı yollarını sunar:

* Express ayarlarında hello Sihirbazı daha fazla ayrıcalıkları gerektirir.  Bu, böylelikle toocreate kullanıcıların gerek kalmadan yapılandırmanızı kolayca ayarlayın veya izinlerini yapılandırın.
* Özel ayarlar hello Sihirbazı daha fazla seçenek ve seçenekler sunar. Ancak, kendiniz hello doğru izinlere sahip tooensure gereken bazı durumlar vardır.

## <a name="related-documentation"></a>İlgili belgeler
Merhaba belge üzerinde okuduğunuz değil, [şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](../active-directory-aadconnect.md), hello aşağıdaki tabloda bağlantıları toorelated konuları sağlar.

|Konu |Bağlantı|  
| --- | --- |
|Azure AD Connect'i indirme | [Azure AD Connect’i indirme](http://go.microsoft.com/fwlink/?LinkId=615771)|
|Hızlı ayarları kullanarak yükleme | [Azure AD Connect’i hızlı yükleme](./active-directory-aadconnect-get-started-express.md)|
|Özelleştirilmiş ayarları kullanarak yükleme | [Azure AD Connect özel yüklemesi](./active-directory-aadconnect-get-started-custom.md)|
|DirSync'ten yükseltme | [Azure AD eşitleme aracından (DirSync) yükseltme](./active-directory-aadconnect-dirsync-upgrade-get-started.md)|
|Yükleme işleminden sonra | [Merhaba yüklemeyi doğrulayın ve lisansları atama](active-directory-aadconnect-whats-next.md)|

## <a name="express-settings-installation"></a>Hızlı ayarları yükleme
Express ayarlarında hello Yükleme Sihirbazı'nı AD DS kuruluş yöneticisi kimlik bilgilerini ister.  Şirket içi Active Directory'nizi Azure AD Connect için gerekli izinlere sahip yapılandırılabilir şekilde budur. Dirsync'ten yükseltme yapıyorsanız, kullanılan tooreset hello DirSync tarafından kullanılan hello hesabının parolasını hello AD DS Enterprise Admins kimlik bilgileridir. Ayrıca Azure AD genel yönetici kimlik bilgileri gerekir.

| Sihirbaz sayfası | Toplanan kimlik bilgileri | Gerekli izinler | İçin kullanılır |
| --- | --- | --- | --- |
| Yok |Kullanıcı çalışan hello Yükleme Sihirbazı |Yerel sunucunun hello Yöneticisi |<li>Hello kullanılan hello yerel hesabı oluşturur [eşitleme altyapısı hizmet hesabı](#azure-ad-connect-sync-service-account). |
| TooAzure AD connect |Azure AD directory kimlik bilgileri |Azure AD genel Yönetici rolüne |<li>Hello Azure AD dizini eşitleme etkinleştiriliyor.</li>  <li>Merhaba oluşturulmasını [Azure AD hesabının](#azure-ad-service-account) kullanılan devam eden eşitleme işlemleri için Azure AD içinde.</li> |
| TooAD DS Bağlan |Şirket içi Active Directory kimlik bilgileri |Active Directory'de hello Enterprise Admins (EA) grubunun üyesi |<li>Oluşturur bir [hesap](#active-directory-account) Active Directory ve izinleri tooit verir. Bu hesabı oluşturuldu kullanılan tooread ve yazma dizin eşitleme sırasında bilgilerdir.</li> |

### <a name="enterprise-admin-credentials"></a>Kuruluş Yöneticisi kimlik bilgileri
Bu kimlik bilgileri yalnızca başlangıç yüklemesi sırasında kullanılır ve hello yükleme tamamlandıktan sonra kullanılmaz. Merhaba Kurumsal Yönetici, hello etki alanı yöneticisi tüm etki alanlarında Active Directory hello izinlerini ayarlanabilir emin olmanız gerekir.

### <a name="global-admin-credentials"></a>Genel yönetici kimlik bilgileri
Bu kimlik bilgileri yalnızca başlangıç yüklemesi sırasında kullanılır ve hello yükleme tamamlandıktan sonra kullanılmaz. Kullanılan toocreate hello olan [Azure AD hesabının](#azure-ad-service-account) değişiklikleri tooAzure AD eşitlemek için kullanılır. Merhaba hesabı, Azure AD içinde bir özellik olarak eşitleme de sağlar.

### <a name="permissions-for-hello-created-ad-ds-account-for-express-settings"></a>Hızlı ayarlar için AD DS hesabı hello izinlerini oluşturuldu
Merhaba [hesap](#active-directory-account) okumak ve DS aşağıdaki tarafından hızlı ayarları oluşturduğunuzda izinleri hello sahip tooAD yazmak için oluşturuldu:

| İzin | İçin kullanılır |
| --- | --- |
| <li>Dizin Değişikliklerini Çoğaltma</li><li>Tüm çoğaltma dizini değiştirir |Parola Eşitleme |
| Okuma/yazma tüm özellikleri kullanıcı |İçeri aktarma ve Exchange karma |
| Okuma/yazma tüm özellikleri iNetOrgPerson |İçeri aktarma ve Exchange karma |
| Tüm özellikleri Grup okuma/yazma |İçeri aktarma ve Exchange karma |
| Tüm özellikleri okuma/yazma başvurun |İçeri aktarma ve Exchange karma |
| Parola sıfırlama |Parola geri yazma özelliğini etkinleştirmek için hazırlama |

## <a name="custom-settings-installation"></a>Özel ayarlarını yükleme
Azure AD Connect sürüm 1.1.524.0 ve daha sonra hello kullanılan hesap tooconnect tooActive dizin oluşturma hello seçeneği toolet hello Azure AD Connect Sihirbazı sahiptir.  Önceki sürümlerde hello hesap hello yüklemeden önce oluşturduğunuz gerektirir. Merhaba izinleri vermeniz gerekir, bu hesabı bulunabilir [hello AD DS hesabı oluşturma](#create-the-ad-ds-account). 

| Sihirbaz sayfası | Toplanan kimlik bilgileri | Gerekli izinler | İçin kullanılır |
| --- | --- | --- | --- |
| Yok |Kullanıcı çalışan hello Yükleme Sihirbazı |<li>Yerel sunucunun hello Yöneticisi</li><li>Tam SQL Server kullanıyorsanız, hello kullanıcının SQL'de Sistem Yöneticisi (SA) olması gerekir</li> |Varsayılan olarak, oluşturulan hello kullanılan hello yerel hesap [eşitleme altyapısı hizmet hesabı](#azure-ad-connect-sync-service-account). Hello Yöneticisi belirli bir hesabı belirtmediğinde hello hesabı yalnızca oluşturulur. |
| Eşitleme hizmetlerini, hizmet hesabı seçeneği yükleme |AD veya yerel kullanıcı hesabı kimlik bilgileri |Merhaba Yükleme Sihirbazı tarafından verilen kullanıcı izinleri |Hello Yöneticisi bir hesap belirtiyorsa, bu hesap hello eşitleme hizmeti için hello hizmet hesabı olarak kullanılır. |
| TooAzure AD connect |Azure AD directory kimlik bilgileri |Azure AD genel Yönetici rolüne |<li>Hello Azure AD dizini eşitleme etkinleştiriliyor.</li>  <li>Merhaba oluşturulmasını [Azure AD hesabının](#azure-ad-service-account) kullanılan devam eden eşitleme işlemleri için Azure AD içinde.</li> |
| Dizinlerinizi bağlama |Şirket içi bağlı tooAzure AD olan her bir orman için Active Directory kimlik bilgileri |Merhaba izinler bağlıdır hangi özellikleri etkinleştirmek ve bulunabilir [hello AD DS hesabı oluşturma](#create-the-ad-ds-account) |Eşitleme sırasında kullanılan tooread ve yazma dizin bilgilerini hesabıdır. |
| AD FS Sunucuları |Başlangıç Sihirbazı'nı çalıştıran hello kullanıcının Hello oturum açma kimlik bilgileri yetersiz tooconnect olduğunda hello listesindeki her sunucu için Başlangıç Sihirbazı'nı kimlik bilgilerini toplar. |Etki alanı yöneticisi |Yükleme ve yapılandırmasını hello AD FS sunucu rolü. |
| Web uygulaması proxy sunucuları |Başlangıç Sihirbazı'nı çalıştıran hello kullanıcının Hello oturum açma kimlik bilgileri yetersiz tooconnect olduğunda hello listesindeki her sunucu için Başlangıç Sihirbazı'nı kimlik bilgilerini toplar. |Merhaba hedef makinede yerel yönetici |Yükleme ve yapılandırma WAP sunucu rolünün. |
| Proxy güven kimlik bilgileri |Federasyon Hizmeti güven kimlik bilgileri (hello kimlik bilgilerini hello proxy tooenroll hello FS güven sertifikadan kullanımları |Merhaba AD FS sunucusunun yerel yönetici olan etki alanı hesabı |İlk kayıttan FS WAP güven sertifikası. |
| "Bir etki alanı kullanıcı hesabı seçeneğini kullan" AD FS hizmet hesabı sayfası |AD kullanıcı hesabı kimlik bilgileri |Etki alanı kullanıcısı |Merhaba AD kullanıcı hesabı kimlik bilgilerini sağlanan hello AD FS hizmetinin başlangıç oturum açma hesabı olarak kullanılır. |

### <a name="create-hello-ad-ds-account"></a>Merhaba AD DS hesabı oluşturma
Merhaba hello üzerinde belirttiğiniz hesap **dizinlerinizi bağlama** sayfa Active Directory önceki tooinstallation içinde bulunmalıdır.  Ayrıca verilen hello gerekli izinlere sahip olmalıdır. Merhaba Yükleme Sihirbazı'nı hello izinleri ve herhangi bir sorun yalnızca eşitleme sırasında bulunan doğrulamaz.

İhtiyaç duyduğunuz hangi izinlerin bağlıdır hello isteğe bağlı özellikleri sağlar. Birden çok etki alanı varsa, hello ormandaki tüm etki alanları için hello izinleri verilmelidir. Bu özelliklerden herhangi birini etkinleştirmezseniz varsayılan hello **etki alanı kullanıcısı** izinleri yeterli olur.

| Özellik | İzinler |
| --- | --- |
| msDS-ConsistencyGuid özelliği |Yazma izinleri toohello msDS-ConsistencyGuid özniteliği belgelenen [tasarım kavramları - sourceAnchor msDS-ConsistencyGuid kullanarak](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor). | 
| Parola Eşitleme |<li>Dizin Değişikliklerini Çoğaltma</li>  <li>Tüm çoğaltma dizini değiştirir |
| Exchange karma dağıtımı |İzinleri toohello öznitelikleri belgelenen yazma [Exchange karma geri yazma](active-directory-aadconnectsync-attributes-synchronized.md#exchange-hybrid-writeback) kullanıcılar, gruplar ve kişiler için. |
| Exchange posta ortak klasörü |Okuma izinleri toohello öznitelikleri belgelenen [Exchange posta ortak klasör](active-directory-aadconnectsync-attributes-synchronized.md#exchange-mail-public-folder) ortak klasörleri için. | 
| Parola geri yazma |İzinleri toohello öznitelikleri belgelenen yazma [parola yönetimine Başlarken](../active-directory-passwords-writeback.md) kullanıcılar için. |
| Cihaz geri yazma |Bölümünde açıklandığı gibi bir PowerShell Betiği ile verilen izinler [cihaz geri yazma](active-directory-aadconnect-feature-device-writeback.md). |
| Grup geri yazma |Okuma, grup oluşturma, güncelleştirme ve silme eşitlenmesi için nesneleri **Office 365 grupları**.  Daha fazla bilgi için bkz: [grup geri yazma](active-directory-aadconnect-feature-preview.md#group-writeback).|

## <a name="upgrade"></a>Yükseltme
Azure AD Connect tooa yeni sürümde bir sürümünden yükselttiğinizde, aşağıdaki izinleri hello gerekir:

| Asıl | Gerekli izinler | İçin kullanılır |
| --- | --- | --- |
| Kullanıcı çalışan hello Yükleme Sihirbazı |Yerel sunucunun hello Yöneticisi |İkili dosyaları güncelleştirin. |
| Kullanıcı çalışan hello Yükleme Sihirbazı |ADSyncAdmins üyesi |TooSync kuralları ve diğer yapılandırma değişiklik yapma. |
| Kullanıcı çalışan hello Yükleme Sihirbazı |Tam bir SQL server kullanıyorsanız: DBO (veya benzeri) hello eşitleme altyapısı veritabanı |Yeni sütunlarla tablo güncelleştirme gibi veritabanı düzeyi değişiklikleri yapın. |

## <a name="more-about-hello-created-accounts"></a>Daha fazla hesapları oluşturulan hello hakkında
### <a name="active-directory-account"></a>Active Directory hesabı
Hızlı ayarları kullanırsanız, Active Directory'de eşitleme için kullanılan bir hesabı oluşturulur. oluşturulan hello hesabı hello orman kök etki alanında hello Kullanıcılar kapsayıcısı içinde bulunur ve adı önekine sahip olan **MSOL_**. Merhaba hesap dolmayan uzun karmaşık bir parola ile oluşturulur. Etki alanınızda bir parola ilkesi varsa, uzun olduğundan emin olun ve karmaşık parolalar bu hesap için izin verilir.

![AD hesabı](./media/active-directory-aadconnect-accounts-permissions/adsyncserviceaccount.png)

Özel ayarları kullanırsanız, daha sonra hello yüklemeye başlamadan önce hello hesabı oluşturmak için sorumludur.

### <a name="azure-ad-connect-sync-service-account"></a>Azure AD Connect eşitleme hizmeti hesabı
Merhaba eşitleme hizmeti farklı hesaplar altında çalışabilir. Altında çalıştırabilirsiniz bir **sanal hizmet hesabı** (VSA) bir **Grup yönetilen hizmet hesabı** (gMSA/sMSA) veya normal bir kullanıcı hesabı. Yeni bir yüklemesidir yaptığınızda desteklenen hello seçenekleri ile Merhaba Bağlan 2017 Nisan sürümü değiştirildi. Azure AD Connect, önceki bir sürümünden yükseltirseniz, bu ek seçenekleri kullanılamaz.

| Hesap türü | Yükleme seçeneği | Açıklama |
| --- | --- | --- |
| [Sanal hizmet hesabı](#virtual-service-account) | Express hem de özel 2017 Nisan ve sonraki sürümler | Bir etki alanı denetleyicisi yüklemelerinde dışında tüm express yüklemeleri için kullanılan hello seçenek budur. Başka bir seçenek kullanılmadığı sürece özel için bunu hello varsayılan seçenektir. |
| [Grup yönetilen hizmet hesabı](#group-managed-service-account) | Özel, 2017 Nisan ve sonraki sürümler | Uzak bir SQL server kullanın, sonra bir grup toouse öneririz, yönetilen hizmet hesabı. |
| [Kullanıcı hesabı](#user-account) | Express hem de özel 2017 Nisan ve sonraki sürümler | Bir kullanıcı hesabı ile AAD_ öneki yalnızca Windows Server 2008 ve bir etki alanı denetleyicisine yüklendiğinde yüklendiğinde yükleme sırasında oluşturulur. |
| [Kullanıcı hesabı](#user-account) | Express hem de özel 2017 Mart ve önceki sürümleri | Yerel bir hesap ile AAD_ önekli yüklemesi sırasında oluşturulur. Özel yükleme kullanırken, başka bir hesap belirtilebilir. |

2017 Mart derleme ile Bağlan'ı kullanın veya önceki sürümlerde, bu yana Windows hello hello hizmet hesabının parolasını sıfırlama sonra güvenlik nedenleriyle hello şifreleme anahtarları bozar varsa. Azure AD Connect'i yeniden yüklemeden başka bir hesap hello hesap tooany değiştiremezsiniz. Tooa derleme Nisan 2017 ' yükseltme veya daha sonra ardından desteklenen toochange hello parola hello hizmet hesabı üzerinde değil ancak kullanılan hello hesabı değiştiremezsiniz.

> [!Important]
> Yalnızca ilk yüklemesinde hello hizmet hesabı ayarlayabilirsiniz. Değil hello yükleme tamamlandıktan sonra toochange hello hizmet hesabı desteklenmez.

Bu önerilen hello varsayılan tablodur ve hizmet hesabı hello için desteklenen seçenekler eşitleyin.

Gösterge:

- **Kalın** hello varsayılan seçeneği gösterir ve çoğu durumda hello seçeneği önerilir.
- *İtalik* gösterir hello hello varsayılan seçenek olmadığı durumlarda seçeneği önerilir.
- 2008 - Windows Server 2008'de yüklendiğinde varsayılan seçeneği
- Non-kalın - desteklenen seçeneği
- Yerel hesap - yerel kullanıcı hesabı hello sunucuda
- Etki alanı hesabı - etki alanı kullanıcı hesabı
- sMSA - [tek başına yönetilen hizmet hesabı](https://technet.microsoft.com/library/dd548356.aspx)
- gMSA - [Grup yönetilen hizmet hesabı](https://technet.microsoft.com/library/hh831782.aspx)

| | Yerel veritabanı</br>Express | Yerel veritabanı/LocalSQL</br>Özel | Uzak SQL</br>Özel |
| --- | --- | --- | --- |
| **tek başına/çalışma grubu makinesi** | Desteklenmiyor | **VSA**</br>Yerel hesap (2008)</br>Yerel hesap |  Desteklenmiyor |
| **Makine etki alanına katılmış** | **VSA**</br>Yerel hesap (2008) | **VSA**</br>Yerel hesap (2008)</br>Yerel hesap</br>Etki alanı hesabı</br>smsa'yı, gMSA | **gMSA**</br>Etki alanı hesabı |
| **Etki alanı denetleyicisi** | **Etki alanı hesabı** | *gMSA*</br>**Etki alanı hesabı**</br>sMSA| *gMSA*</br>**Etki alanı hesabı**|

#### <a name="virtual-service-account"></a>Sanal hizmet hesabı
Bir sanal hizmet hesabı, bir parola sahip değil ve Windows tarafından yönetilen hesap özel türüdür.

![VSA](./media/active-directory-aadconnect-accounts-permissions/aadsyncvsa.png)

Merhaba VSA olduğu hedeflenen toobe hello eşitleme altyapısı ve SQL üzerinde hello nerede senaryolarla kullanılan aynı sunucu. Uzak SQL kullanın, sonra toouse öneririz, bir [Grup yönetilen hizmet hesabı](#managed-service-account) yerine.

Bu özellik, Windows Server 2008 R2 gerektirir veya sonraki bir sürümü. Windows Server 2008 üzerinde Azure AD Connect'i yüklemek sonra hello yükleme döner geri toousing bir [kullanıcı hesabı](#user-account) yerine.

#### <a name="group-managed-service-account"></a>Grup yönetilen hizmet hesabı
Uzak bir SQL server kullanmak sonra toousing öneririz bir **Grup yönetilen hizmet hesabı**. Hakkında daha fazla bilgi için Active Directory Grup yönetilen hizmet hesabı için tooprepare bkz [Grup yönetilen hizmet hesaplarına genel bakış](https://technet.microsoft.com/library/hh831782.aspx).

Bu seçenek, üzerinde hello toouse [gerekli bileşenleri yüklemeniz](active-directory-aadconnect-get-started-custom.md#install-required-components) sayfasında, **varolan hizmet hesabını kullan**seçip **yönetilen hizmet hesabı**.  
![VSA](./media/active-directory-aadconnect-accounts-permissions/serviceaccount.png)  
Ayrıca desteklenen toouse olan bir [tek başına yönetilen hizmet hesabı](https://technet.microsoft.com/library/dd548356.aspx). Ancak, bunlar yalnızca hello yerel makine üzerinde kullanılabilir olup olmadığını hiçbir avantajı toouse hello varsayılan sanal hizmet hesabı üzerinden bunları.

Bu özellik, Windows Server 2012 veya sonraki sürümünü gerektirir. Uzak SQL kullanın ve toouse daha eski bir işletim sistemi gerekir durumunda kullanmalısınız bir [kullanıcı hesabı](#user-account).

#### <a name="user-account"></a>Kullanıcı hesabı
(Merhaba hesap toouse özel ayarlarında belirtmediğiniz sürece) local service hesabı hello Yükleme Sihirbazı tarafından oluşturulur. Merhaba hesabı önekli **AAD_** ve hello gerçek eşitleme hizmeti toorun kullanılır. Azure AD Connect etki alanı denetleyicisine yüklerseniz, hello hesap hello etki alanında oluşturulur. Merhaba **AAD_** hizmet hesabı, hello etki alanında bulunmalıdır:
   - SQL server çalıştıran uzak bir sunucu kullanın
   - kimlik doğrulaması gerektiren bir proxy kullanın

![Eşitleme hizmeti hesabı](./media/active-directory-aadconnect-accounts-permissions/syncserviceaccount.png)

Merhaba hesap dolmayan uzun karmaşık bir parola ile oluşturulur.

Bu hesap hello için kullanılan toostore hello parolaları diğer hesapları güvenli bir şekilde değil. Bu diğer hesapları parolaların hello veritabanında şifrelenmiş olarak depolanır. Hello özel anahtarları hello şifreleme anahtarları için Windows Data Protection API (DPAPI) kullanarak hello Şifreleme Hizmetleri gizli anahtar şifrelemesiyle korunur.

Tam bir SQL Server kullanıyorsanız, ardından hello hizmet hello hello eşitleme altyapısı için oluşturulan hello veritabanı DBO hesabıdır. Merhaba hizmeti, diğer herhangi bir izinle beklendiği gibi çalışmayacaktır. Bir SQL oturum açma da oluşturulur.

Merhaba hesabına izinler toofiles, kayıt defteri anahtarları ve diğer nesneleri ilgili toohello eşitleme altyapısı de verilir.

### <a name="azure-ad-service-account"></a>Azure AD hizmet hesabı
Azure AD'de bir hesap hello eşitleme hizmetinin kullanım için oluşturulur. Bu hesap, görünen ada göre tanımlanabilir.

![AD hesabı](./media/active-directory-aadconnect-accounts-permissions/aadsyncserviceaccount.png)

Merhaba sunucu hello hesabının Hello adı kullanılır hello kullanıcı adının hello ikinci bölümü üzerinde tanımlanabilir. Merhaba resimde FABRIKAMCON hello sunucu adıdır. Sunucuları hazırlama varsa, her sunucu, kendi hesabı vardır.

Merhaba hizmet hesabı dolmayan uzun karmaşık bir parola ile oluşturulur. Özel bir rol verilen **Directory eşitleme hesapları** yalnızca izinleri tooperform dizin eşitleme görevleri vardır. Bu özel yerleşik rol hello Azure AD Connect Sihirbazı dışında verilemez. Hello Azure portal gösterir hello rolü bu hesapla **kullanıcı**.

Azure AD'de 20 eşitleme hizmet hesapları bir sınırı yoktur. tooget hello Azure AD PowerShell cmdlet'i aşağıdaki hello çalıştırmak mevcut Azure AD hizmet hesaplarının listesini, Azure ad:`Get-AzureADDirectoryRole | where {$_.DisplayName -eq "Directory Synchronization Accounts"} | Get-AzureADDirectoryRoleMember`

kullanılmayan tooremove Azure AD hizmet hesapları, Azure AD PowerShell cmdlet'i aşağıdaki hello çalıştırın:`Remove-AzureADUser -ObjectId <ObjectId-of-the-account-you-wish-to-remove>`

## <a name="next-steps"></a>Sonraki adımlar
[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](../active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.
