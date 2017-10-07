---
title: "Azure AD etki alanı Hizmetleri: Karşılaştırma Azure AD etki alanı Hizmetleri tooDIY etki alanı denetleyicileri | Microsoft Docs"
description: "Azure Active Directory etki alanı Hizmetleri tooDIY etki alanı denetleyicileri karşılaştırma"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 165249d5-e0e7-4ed1-aa26-91a05a87bdc9
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: maheshu
ms.openlocfilehash: 5e384f6a676e76e4f22ff62d4aeb578bc8481ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodecide-if-azure-ad-domain-services-is-right-for-your-use-case"></a>Azure AD etki alanı hizmetleri nasıl toodecide, kullanım durumu için doğru ise
Azure AD etki alanı Hizmetleri ile iş yüklerinizi Azure altyapı Hizmetleri'nde, azure'da kimlik altyapısını sürdürme hakkında tooworry gerek kalmadan dağıtabilirsiniz. Bu yönetilen hizmet dağıtmak ve yönetmek, kendi tipik bir Windows Server Active Directory Dağıtım farklıdır. Merhaba hizmeti kolay toodeploy ve otomatik sistem durumu izleme ve düzeltme sunar. Biz hello hizmeti tooadd desteği ortak dağıtım senaryoları için sürekli olarak artmaktadır.

toodecide toouse Azure AD etki alanı Hizmetleri olup olmadığını okuma malzemelerini aşağıdaki hello öneririz:

* Merhaba listesini görmek [özelliklerini Azure AD etki alanı Hizmetleri tarafından sunulan](active-directory-ds-features.md).
* Gözden geçirme ortak [Azure AD etki alanı Hizmetleri için dağıtım senaryoları](active-directory-ds-scenarios.md).
* Son olarak, [Azure AD etki alanı Hizmetleri tooa yazılanları AD seçeneği karşılaştırmak](active-directory-ds-comparison.md#compare-azure-ad-domain-services-to-diy-ad-domain-in-azure).

## <a name="compare-azure-ad-domain-services-toodiy-ad-domain-in-azure"></a>Azure AD etki alanı Hizmetleri tooDIY AD etki alanı Azure Karşılaştır
Merhaba aşağıdaki tabloda, Azure AD Etki Alanı Hizmetleri'ni kullanarak kendi Azure AD altyapısında yönetme arasında bir karar vermenize yardımcı olur.

| **Özellik** | **Azure AD etki alanı Hizmetleri** | **Azure VM'ler 'Yazılanları' AD** |
| --- |:---:|:---:|
| [**Yönetilen hizmet**](active-directory-ds-comparison.md#managed-service) |**&#x2713;** |**& #x 2715;** |
| [**Güvenli dağıtımlar**](active-directory-ds-comparison.md#secure-deployments) |**&#x2713;** |Yöneticinin toosecure hello dağıtım gerekir. |
| [**DNS sunucusu**](active-directory-ds-comparison.md#dns-server) |**& #x 2713;**  (yönetilen hizmet) |**&#x2713;** |
| [**Etki alanı veya kuruluş yönetici ayrıcalıkları**](active-directory-ds-comparison.md#domain-or-enterprise-administrator-privileges) |**& #x 2715;** |**&#x2713;** |
| [**Etki alanına katılma**](active-directory-ds-comparison.md#domain-join) |**&#x2713;** |**&#x2713;** |
| [**NTLM ve Kerberos kullanarak etki alanı kimlik doğrulaması**](active-directory-ds-comparison.md#domain-authentication-using-ntlm-and-kerberos) |**&#x2713;** |**&#x2713;** |
| [**Kısıtlı Kerberos temsilcisi seçme**](active-directory-ds-comparison.md#kerberos-constrained-delegation)|Kaynak tabanlı|Kaynak tabanlı & hesabı tabanlı|
| [**Özel OU yapısı**](active-directory-ds-comparison.md#custom-ou-structure) |**&#x2713;** |**&#x2713;** |
| [**Şema uzantıları**](active-directory-ds-comparison.md#schema-extensions) |**& #x 2715;** |**&#x2713;** |
| [**AD etki alanı/orman güvenleri**](active-directory-ds-comparison.md#ad-domain-or-forest-trusts) |**& #x 2715;** |**&#x2713;** |
| [**LDAP okuma**](active-directory-ds-comparison.md#ldap-read) |**&#x2713;** |**&#x2713;** |
| [**Güvenli LDAP (LDAPS)**](active-directory-ds-comparison.md#secure-ldap) |**&#x2713;** |**&#x2713;** |
| [**LDAP yazma**](active-directory-ds-comparison.md#ldap-write) |**& #x 2715;** |**&#x2713;** |
| [**Grup İlkesi**](active-directory-ds-comparison.md#group-policy) |**&#x2713;** |**&#x2713;** |
| [**Coğrafi olarak dağıtılan dağıtımları**](active-directory-ds-comparison.md#geo-dispersed-deployments) |**& #x 2715;** |**&#x2713;** |

#### <a name="managed-service"></a>Yönetilen hizmet
Azure AD etki alanı Hizmetleri etki alanı, Microsoft tarafından yönetilir. Düzeltme eki uygulama, güncelleştirmeler, yedeklemeler, izleme ve etki alanınızı kullanılabilir olmasını sağlamaya hakkında tooworry sahip değilsiniz. Bu yönetim görevleri, Microsoft Azure tarafından yönetilen etki alanları için bir hizmet olarak sunulur.

#### <a name="secure-deployments"></a>Güvenli dağıtımlar
Merhaba yönetilen etki alanı güvenli bir şekilde Microsoft'un güvenlik önerilerini AD dağıtımlar için uygun şekilde kilitlenmiştir. Bu öneriler, mühendislik ve AD dağıtımları destekleyen deneyimi hello AD ürün ekibinin on yılları gövdesi. Tootake belirli dağıtım ihtiyacınız yazılanları dağıtımları için dağıtım adımları toolock aşağı/güvenli.

#### <a name="dns-server"></a>DNS sunucusu
Azure AD etki alanı Hizmetleri yönetilen etki alanı, yönetilen DNS hizmetleri içerir. Merhaba 'AAD DC Yöneticiler' grubunun üyeleri hello yönetilen etki alanı DNS yönetebilirsiniz. Bu grubun üyeleri hello yönetilen etki alanı için tam DNS yönetim ayrıcalıkları verilir. DNS Yönetim hello 'hello Uzak Sunucu Yönetim Araçları (RSAT) paketindeki DNS Yönetim konsolunda' kullanılarak gerçekleştirilebilir.
[Daha fazla bilgi](active-directory-ds-admin-guide-administer-dns.md)

#### <a name="domain-or-enterprise-administrator-privileges"></a>Etki alanı veya kuruluş yöneticisi ayrıcalıkları
Bir AAD DS yönetilen etki alanında bu yükseltilmiş ayrıcalıklar önerilmez. Bu yükseltilmiş ayrıcalıklar AAD DS karşı dağıtılamıyor gerektiren bir uygulama etki alanları yönetilen. Kullanılabilir toomembers 'AAD DC Yöneticiler' adlı hello temsilci ile yönetim grubunun yönetim ayrıcalıkları daha küçük alt kümesidir. Bu ayrıcalıklar ayrıcalıkları tooconfigure DNS dahil, Grup İlkesi yapılandırmak, etki alanına katılan makineler vb. üzerinde yönetici ayrıcalıklarına sahip.

#### <a name="domain-join"></a>Etki alanına katılma
Sanal makine katılamaz toohello yönetilen etki alanı benzer toohow bilgisayarlar tooan AD etki alanına katılın.

#### <a name="domain-authentication-using-ntlm-and-kerberos"></a>NTLM ve Kerberos kullanarak etki alanı kimlik doğrulaması
Azure AD etki alanı Hizmetleri ile şirket kimlik bilgilerini tooauthenticate hello yönetilen etki alanı ile kullanabilirsiniz. Kimlik bilgileri Azure AD kiracınıza ile eşitlenmiş tutulur. Eşitlenmiş kiracılar için Azure AD Connect içi toocredentials yapılan değişiklikleri eşitlenmiş tooAzure AD olmasını sağlar. Yazılanları etki alanı kurulumu ile bir AD etki alanı tooset gerekebilir güven ile şirket içi Kurumsal kimlik ile kullanıcılar tooauthenticate için AD. Alternatif olarak, AD çoğaltma tooensure kullanıcı parolaları tooyour Azure etki alanı denetleyicisi sanal makinelerini eşitleme yukarı tooset gerekebilir.

#### <a name="kerberos-constrained-delegation"></a>Kısıtlı Kerberos temsilcisi seçme
Bir Active Directory etki alanı Hizmetleri yönetilen etki alanında ' etki alanı Yönetici ' ayrıcalıklarına sahip değil. Bu nedenle, hesap tabanlı (Geleneksel) kısıtlı Kerberos temsilcisi yapılandıramazsınız. Ancak, daha güvenli hello yapılandırabilirsiniz kaynak tabanlı Kısıtlı temsilci.
[Daha fazla bilgi](active-directory-ds-enable-kcd.md)

#### <a name="custom-ou-structure"></a>Özel OU yapısı
Merhaba 'AAD DC Yöneticiler' grubunun üyeleri hello yönetilen etki alanı içinde özel OU'lar oluşturabilirsiniz. Özel OU'lar Oluştur kullanıcılar hello OU üzerinde tam yönetim ayrıcalıklarına sahiptir.
[Daha fazla bilgi](active-directory-ds-admin-guide-create-ou.md)

#### <a name="schema-extensions"></a>Şema uzantıları
Bir Azure AD etki alanı Hizmetleri yönetilen etki alanının hello temel şema genişletemezsiniz. Bu nedenle, uzantıları tooAD şeması (örneğin, yeni öznitelikler hello kullanıcı nesnesi altında) kullanan uygulamalar kaldırılmış olamaz ve tooAAD DS etki alanlarının gölgeye.

#### <a name="ad-domain-or-forest-trusts"></a>AD etki alanı veya orman güvenleri
Yönetilen etki alanı güven ilişkileri (gelen/giden) diğer etki alanları ile yapılandırılmış tooset olamaz. Bu nedenle, kaynak ormanı dağıtım senaryoları Azure AD Etki Alanı Hizmetleri'ni kullanamazsınız. Benzer şekilde, burada değil toosynchronize parolaları tooAzure AD tercih dağıtımları Azure AD etki alanı Hizmetleri kullanamazsınız.

#### <a name="ldap-read"></a>LDAP okuma
Merhaba, etki alanı destekler LDAP okuma iş yükleri yönetilen. Bu nedenle, okuma işlemleri hello yönetilen etki alanına göre LDAP gerçekleştiren uygulamaları dağıtabilirsiniz.

#### <a name="secure-ldap"></a>Güvenli LDAP
Yönetilen Azure AD etki alanı Hizmetleri tooprovide güvenli LDAP erişim tooyour yapılandırabilirsiniz hello Internet üzerinden de dahil olmak üzere etki alanı.
[Daha fazla bilgi](active-directory-ds-admin-guide-configure-secure-ldap.md)

#### <a name="ldap-write"></a>LDAP yazma
Merhaba yönetilen etki alanı kullanıcı nesneleri için salt okunur durumdadır. Bu nedenle, hello kullanıcı nesnesinin öznitelikleri karşı LDAP yazma işlemlerini gerçekleştiren uygulamalar yönetilen bir etki alanında çalışmaz. Ayrıca, kullanıcı parolalarını hello yönetilen etki alanı içinde değiştirilemez. Başka bir örnek grup üyeliklerini veya izin hello yönetilen etki alanındaki grup öznitelikleri değiştirilmesine olabilir. Ancak, değişiklikleri toouser öznitelikleri veya Azure AD (PowerShell/Azure portalı) yoluyla yapılan parolaları veya şirket içi AD eşitlenir toohello AAD DS yönetilen etki alanı.

#### <a name="group-policy"></a>Grup İlkesi
Bir yerleşik GPO her hello "AADDC bilgisayarlar" ve "AADDC kullanıcıları" kapsayıcıları için yoktur. Bu yerleşik GPO'ları tooconfigure Grup İlkesi özelleştirebilirsiniz. Hello 'AAD DC Yöneticiler' grubunun üyeleri de özel GPO'ları oluşturmak ve onları (özel OU'lar dahil) tooexisting OU'lara bağlayın.
[Daha fazla bilgi](active-directory-ds-admin-guide-administer-group-policy.md)

#### <a name="geo-dispersed-deployments"></a>Coğrafi olarak dağınık dağıtımları
Azure AD etki alanı Hizmetleri yönetilen etki alanları, azure'da tek bir sanal ağda kullanılabilir. Merhaba dünya genelindeki etki alanı denetleyicileri toobe kullanılabilir birden çok Azure bölgelerindeki gerektiren senaryolar için Azure Iaas Vm'leri etki alanı denetleyicileri ayarlama hello daha iyi alternatif olabilir.


## <a name="do-it-yourself-diy-ad-deployment-options"></a>'Yazılanları' (DIY) AD dağıtım seçenekleri
Bazı Windows Server AD yüklemesi tarafından sunulan hello özelliklerini ihtiyaç duyacağınız dağıtım kullanım örnekleri olabilir. Bu durumlarda, aşağıdaki yazılanları (DIY) seçenekleri şu hello birini göz önünde bulundurun:

* **Tek başına bulut etki alanı:** tek başına ' etki alanı denetleyicileri olarak yapılandırılmış Azure sanal makineleri kullanarak bulut etki alanı' ayarlayabilirsiniz. Bu altyapı şirket içi ile tümleştirilmezse AD ortamı. Bu seçenek 'kimlik bilgileri bulut' toologin/yönetmek hello bulutta VM'ler farklı kümesi gerektirir.
* **Kaynak orman dağıtımı:** hello kaynak orman topoloji, bir etki alanına etki alanı denetleyicileri olarak yapılandırılmış Azure sanal makineleri kullanarak ayarlayabilirsiniz. Ardından, şirket içi ile AD güven ilişkisi yapılandırabilirsiniz AD ortamı. Etki alanına katılma bilgisayarları (Azure VM) toothis kaynak ormanı hello bulutta kullanabilirsiniz. Kullanıcı kimlik doğrulaması ya da bir VPN/ExpressRoute bağlantı tooyour şirket içi dizin olur.
* **Şirket içi etki alanı tooAzure genişletmek:** VPN/ExpressRoute Bağlantısı'nı kullanarak bir Azure sanal ağı tooyour şirket ağına bağlanabilir. Bu ayar Azure VM'ler toobe sağlar birleştirilmiş tooyour şirket içi AD. Başka bir toopromote çoğaltma etki alanı denetleyicilerini şirket içi etki alanınızda Azure VM olarak alternatiftir. Ardından tooreplicate bir VPN/ExpressRoute bağlantı tooyour şirket içi dizin ayarlayabilirsiniz. Bu dağıtım modu, şirket içi etki alanı tooAzure etkili bir şekilde genişletir.

> [!NOTE]
> Dıy seçeneği dağıtım kullanım örnekleri için daha uygun olan belirleyebilir. Göz önünde bulundurun [geri bildirim paylaşımı](active-directory-ds-contact-us.md) toohelp bize anlamak özellikleri yardımcı olacak Azure AD etki alanı Hizmetleri hello gelecekteki seçtiniz. Bu geri bildirim ve kullanım örnekleri dağıtımınızı gereken hello hizmet toobetter uyacak gelişmesi yardımcı olur.
>
>

Yayımlanan [yönergeleri dağıtma Windows Server Active Directory için Azure sanal makineler üzerinde](https://msdn.microsoft.com/library/azure/jj156090.aspx) toohelp Dıy yüklemeleri daha kolay olun.

## <a name="related-content"></a>İlgili İçerik
* [Özellikler - Azure AD etki alanı Hizmetleri](active-directory-ds-features.md)
* [Dağıtım senaryoları - Azure AD etki alanı Hizmetleri](active-directory-ds-scenarios.md)
* [Windows Server Active Directory, Azure sanal makinelerde dağıtmak için yönergeler](https://msdn.microsoft.com/library/azure/jj156090.aspx)
