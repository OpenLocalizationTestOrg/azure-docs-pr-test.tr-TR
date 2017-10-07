---
title: "aaaFAQs - Azure Active Directory etki alanı Hizmetleri | Microsoft Docs"
description: "Azure Active Directory etki alanı hizmetleri hakkında sık sorulan sorular"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 48731820-9e8c-4ec2-95e8-83dba1e58775
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: maheshu
ms.openlocfilehash: 42a6d659f6408bf694cb2aa6ec24bff7a76b0565
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-domain-services-frequently-asked-questions-faqs"></a>Azure Active Directory etki alanı Hizmetleri: Sık sorulan sorular (SSS)
Bu sayfayı hello Azure Active Directory etki alanı hizmetleri hakkında sık sorulan sorular yanıtlanmaktadır. Geri Güncelleştirmeler denetleniyor tutun.

### <a name="troubleshooting-guide"></a>Sorun giderme kılavuzu
Tooour başvuran [sorun giderme kılavuzu](active-directory-ds-troubleshooting.md) çözümleri toocommon sorunları olduğunda karşılaştı yapılandırma veya Azure AD etki alanı Hizmetleri yönetme.

### <a name="configuration"></a>Yapılandırma
#### <a name="can-i-create-multiple-domains-for-a-single-azure-ad-directory"></a>Birden çok etki alanı için tek bir oluşturabilmeniz için Azure AD dizini?
Hayır. Tek bir Azure AD etki alanı Hizmetleri tarafından hizmet verilen tek bir etki alanı oluşturabilmeniz için Azure AD dizini.  

#### <a name="can-i-enable-azure-ad-domain-services-in-an-azure-resource-manager-virtual-network"></a>Bir Azure Resource Manager sanal ağı Azure AD Etki Alanı Hizmetleri'nde etkinleştirebilirim?
Hayır. Azure AD etki alanı Hizmetleri yalnızca klasik bir Azure sanal ağında etkinleştirilebilir. Sanal ağ eşleme toouse bir Resource Manager sanal ağdaki yönetilen etki alanınızı kullanarak hello Klasik sanal ağı tooa Resource Manager sanal ağ bağlanabilir.

#### <a name="can-i-enable-azure-ad-domain-services-in-a-federated-azure-ad-directory-i-use-adfs-tooauthenticate-users-for-access-toooffice-365-can-i-enable-azure-ad-domain-services-for-this-directory"></a>Azure AD Etki Alanı Hizmetleri'nde bir Federasyon Azure etkinleştirebilmeniz için AD dizini? ADFS tooauthenticate kullanıcıların erişim tooOffice 365 kullanıyorum. Bu dizin için Azure AD etki alanı Hizmetleri etkinleştirebilirim?
Hayır. Azure AD etki alanı Hizmetleri toohello parola karmaları, kullanıcı hesapları, NTLM veya Kerberos üzerinden tooauthenticate kullanıcılara erişimi gerektirir. Federe bir dizinde parola karmaları hello Azure AD dizininde depolanmaz. Bu nedenle, Azure AD etki alanı Hizmetleri çalışmıyor gibi Azure AD dizinleri.

#### <a name="can-i-make-azure-ad-domain-services-available-in-multiple-virtual-networks-within-my-subscription"></a>Azure AD etki alanı Hizmetleri bulunan birden çok sanal ağ içinde Aboneliğimi oluşturabilir miyim?
Merhaba hizmetin kendisini bu senaryo doğrudan desteklemez. Azure AD etki alanı Hizmetleri aynı anda yalnızca tek bir sanal ağ içinde mevcut değil. Ancak, birden çok sanal ağlar tooexpose Azure AD etki alanı Hizmetleri tooother sanal ağlar arasında bağlantı yapılandırabilirsiniz. Nasıl bu makalede [azure'da sanal ağlara bağlanabilir](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

#### <a name="can-i-enable-azure-ad-domain-services-using-powershell"></a>PowerShell kullanarak Azure AD etki alanı Hizmetleri etkinleştirebilirim?
PowerShell ve otomatik dağıtım Azure AD etki alanı Hizmetleri şu anda kullanılabilir değil.

#### <a name="is-azure-ad-domain-services-available-in-hello-new-azure-portal"></a>Azure AD etki alanı Hizmetleri hello yeni Azure Portalı'nda var mı?
Hayır. Azure AD etki alanı Hizmetleri yalnızca hello yapılandırılabilir [Klasik Azure portalı](https://manage.windowsazure.com). Merhaba tooextend desteği bekliyoruz [Azure portal](https://portal.azure.com) hello gelecekteki içinde.

#### <a name="can-i-add-domain-controllers-tooan-azure-ad-domain-services-managed-domain"></a>Etki alanı denetleyicileri tooan Azure AD etki alanı Hizmetleri yönetilen etki alanı ekleyebilir miyim?
Hayır. Azure AD etki alanı Hizmetleri tarafından sağlanan hello etki alanı yönetilen bir etki alanıdır. Tooprovision gerekmez, yapılandırma veya etki alanı denetleyicileri bu etki alanı - etkinlikleri bir hizmet olarak Microsoft tarafından sağlanan bu yönetim yönetmek. Bu nedenle, hello yönetilen etki alanı için ek etki alanı denetleyicileri (okuma-yazma veya salt okunur) ekleyemezsiniz.

### <a name="administration-and-operations"></a>Yönetim ve işlemler
#### <a name="can-i-connect-toohello-domain-controller-for-my-managed-domain-using-remote-desktop"></a>Uzak Masaüstü kullanarak yönetilen etki alanım için toohello etki alanı denetleyicisi bağlayabilir miyim?
Hayır. Uzak Masaüstü hello yönetilen etki alanı için izinleri tooconnect toodomain denetleyicileri sahip değilsiniz. Merhaba 'AAD DC Yöneticiler' grubunun üyeleri hello yönetilen etki hello Active Directory Yönetim Merkezi (ADAC) veya AD PowerShell gibi AD Yönetim Araçları'nı kullanarak yönetebilirsiniz. Merhaba 'uzak sunucu Yönetim Araçları' kullanarak bu araçlar yüklü bir Windows server özelliğini toohello yönetilen etki alanına katılmış.

#### <a name="ive-enabled-azure-ad-domain-services-what-user-account-do-i-use-toodomain-join-machines-toothis-domain"></a>Azure AD etki alanı Hizmetleri etkin. Hangi kullanıcı hesabı toodomain makineler toothis etki alanına katılma kullanabilirim?
'AAD DC Yöneticiler' hello yönetim grubunun üyeleri, etki alanına katılma makineler olabilir. Ayrıca, bu grubun üyeleri, etki alanına katılmış toohello silinmiş Uzak Masaüstü erişimi toomachines verilir.

#### <a name="do-i-have-domain-administrator-privileges-for-hello-managed-domain-provided-by-azure-ad-domain-services"></a>Azure AD etki alanı Hizmetleri tarafından sağlanan hello yönetilen etki alanı için etki alanı yönetici ayrıcalıkları var mı?
Hayır. Merhaba yönetilen etki alanı üzerinde yönetim ayrıcalıkları verilmez. ' Etki alanı Yöneticisi ' ve ' Kuruluş Yöneticisi ' ayrıcalıkları, toouse hello etki alanı içinde kullanılabilir değil. Ayrıca var olan etki alanı yöneticisi veya Kurumsal Yönetici grupları, Azure AD dizini içinde hello etki alanındaki etki alanı/kuruluş yönetici ayrıcalıkları verilmez.

#### <a name="can-i-modify-group-memberships-using-ldap-or-other-ad-administrative-tools-on-managed-domains"></a>Yönetilen etki alanlarında LDAP veya diğer AD yönetim araçlarını kullanarak grup üyeliklerini değişiklik yapabilirsiniz?
Hayır. Grup üyelikleri, Azure AD etki alanı Hizmetleri tarafından hizmet verilen etki alanları değiştirilemez. Merhaba, aynı kullanıcı öznitelikleri için geçerlidir. Azure AD veya şirket içi etki alanınızdaki grup üyeliklerini veya kullanıcı özniteliklerini ancak değişebilir. Bu değişiklikleri otomatik olarak eşitlenen tooAzure AD etki alanı Hizmetleri oluşturulur.

#### <a name="how-long-does-it-take-for-changes-i-make-toomy-azure-ad-directory-toobe-visible-in-my-managed-domain"></a>Ne kadar süreyle sürer değişiklikleri ı toomy Azure AD directory toobe my yönetilen etki alanında görünür yapmak?
Azure AD dizininizi hello Azure AD kullanıcı Arabirimi veya PowerShell kullanarak yapılan değişiklikler eşitlenmiş tooyour yönetilen etki alanı gelir. Bu eşitleme işlemi hello arka planda çalışır. Dizininizin Hello tek seferlik ilk eşitleme tamamlandıktan sonra yönetilen etki alanınızda genellikle 20 dakika içinde Azure AD toobe yapılan değişiklikleri alır yansıtılır.

#### <a name="can-i-extend-hello-schema-of-hello-managed-domain-provided-by-azure-ad-domain-services"></a>Azure AD etki alanı Hizmetleri tarafından sağlanan hello yönetilen etki alanı hello şemasını genişletebilir miyim?
Hayır. Merhaba şema hello yönetilen etki alanı için Microsoft tarafından yönetilir. Şema uzantıları, Azure AD etki alanı Hizmetleri tarafından desteklenmiyor.

#### <a name="can-i-modify-or-add-dns-records-in-my-managed-domain"></a>I değiştirebilir veya my yönetilen etki alanında DNS kayıtları eklemek?
Evet. Merhaba 'AAD DC Yöneticiler' grubunun üyeleri ' DNS Yöneticisi ' ayrıcalıkları verilmiş toomodify hello yönetilen etki alanında DNS kaydeder. Bunlar bir makine çalışan Windows Server birleştirilmiş toohello yönetilen etki alanında, toomanage DNS hello DNS Yöneticisi konsolunu kullanabilirsiniz. DNS Yöneticisi konsol toouse hello 'DNS sunucusu hello 'Uzak sunucu Yönetim Araçları' hello sunucuda isteğe bağlı bir özellik parçası olan Araçlar', yükleyin. Daha fazla bilgi [yönetme, izleme ve DNS sorunlarını giderme için yardımcı programlar](https://technet.microsoft.com/library/cc753579.aspx) TechNet üzerindeki kullanılabilir.

### <a name="billing-and-availability"></a>Faturalama ve kullanılabilirlik
#### <a name="is-azure-ad-domain-services-a-paid-service"></a>Ücretli bir hizmeti Azure AD etki alanı hizmetleri mi?
Evet. Daha fazla bilgi için bkz: Merhaba [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/active-directory-ds/).

#### <a name="is-there-a-free-trial-for-hello-service"></a>Merhaba hizmeti için ücretsiz deneme sürümü var mı?
Bu hizmet hello Azure ücretsiz deneme sürümü dahil edilir. Oturum açabileceğiniz bir [ücretsiz bir aylık deneme Azure](https://azure.microsoft.com/pricing/free-trial/).

#### <a name="can-i-get-azure-ad-domain-services-as-part-of-enterprise-mobility-suite-ems-do-i-need-azure-ad-premium-toouse-azure-ad-domain-services"></a>Enterprise Mobility Suite (EMS) bir parçası olarak Azure AD etki alanı Hizmetleri alabilir miyim? Azure AD Premium toouse Azure AD etki alanı Hizmetleri gerekiyor mu?
Hayır. Azure AD etki alanı Hizmetleri Kullandıkça Öde Azure hizmeti ve EMS bir parçası değil. Azure AD etki alanı Hizmetleri ile Azure ad tüm sürümleri kullanılabilir (ücretsiz, temel ve, Premium). Kullanım bağlı olarak bir saatlik olarak faturalandırılır.

#### <a name="what-azure-regions-is-hello-service-available-in"></a>Hangi Azure bölgeleri hizmettir hello kullanılabilir?
Toohello başvuran [bölgeye göre Azure Hizmetleri](https://azure.microsoft.com/regions/#services/) sayfa toosee listesini hello Azure bölgeleri Azure AD etki alanı Hizmetleri olduğu kullanılabilir.
