---
title: "Sık sorulan sorular - Azure Active Directory etki alanı Hizmetleri | Microsoft Docs"
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
ms.openlocfilehash: 7f3212350b1158cd51a34ee1b20a456a73d41672
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-domain-services-frequently-asked-questions-faqs"></a>Azure Active Directory etki alanı Hizmetleri: Sık sorulan sorular (SSS)
Bu sayfa, Azure Active Directory etki alanı hizmetleri hakkında sık sorulan sorular yanıtlanmaktadır. Geri Güncelleştirmeler denetleniyor tutun.

### <a name="troubleshooting-guide"></a>Sorun giderme kılavuzu
Başvurmak bizim [sorun giderme kılavuzu](active-directory-ds-troubleshooting.md) yapılandırma veya Azure AD etki alanı Hizmetleri yönetme karşılaştığınız sık karşılaşılan sorunlara çözümler için.

### <a name="configuration"></a>Yapılandırma
#### <a name="can-i-create-multiple-domains-for-a-single-azure-ad-directory"></a>Birden çok etki alanı için tek bir oluşturabilmeniz için Azure AD dizini?
Hayır. Tek bir Azure AD etki alanı Hizmetleri tarafından hizmet verilen tek bir etki alanı oluşturabilmeniz için Azure AD dizini.  

#### <a name="can-i-enable-azure-ad-domain-services-in-an-azure-resource-manager-virtual-network"></a>Bir Azure Resource Manager sanal ağı Azure AD Etki Alanı Hizmetleri'nde etkinleştirebilirim?
Hayır. Azure AD etki alanı Hizmetleri yalnızca klasik bir Azure sanal ağında etkinleştirilebilir. Klasik sanal ağ sanal ağ bir Resource Manager sanal ağdaki yönetilen etki alanınızı kullanacak şekilde eşleme özelliğini kullanarak bir Resource Manager sanal ağa bağlanabilir.

#### <a name="can-i-enable-azure-ad-domain-services-in-a-federated-azure-ad-directory-i-use-adfs-to-authenticate-users-for-access-to-office-365-can-i-enable-azure-ad-domain-services-for-this-directory"></a>Azure AD Etki Alanı Hizmetleri'nde bir Federasyon Azure etkinleştirebilmeniz için AD dizini? Office 365 erişimi için kullanıcıların kimliğini doğrulamak için ADFS kullanıyorum. Bu dizin için Azure AD etki alanı Hizmetleri etkinleştirebilirim?
Hayır. Azure AD etki alanı Hizmetleri NTLM veya Kerberos üzerinden kullanıcıların kimliğini doğrulamak için kullanıcı hesaplarının, parola karmaları erişimi olmalıdır. Federe bir dizinde parola karmaları Azure AD dizininde depolanmaz. Bu nedenle, Azure AD etki alanı Hizmetleri çalışmıyor gibi Azure AD dizinleri.

#### <a name="can-i-make-azure-ad-domain-services-available-in-multiple-virtual-networks-within-my-subscription"></a>Azure AD etki alanı Hizmetleri bulunan birden çok sanal ağ içinde Aboneliğimi oluşturabilir miyim?
Hizmet, bu senaryo doğrudan desteklemez. Azure AD etki alanı Hizmetleri aynı anda yalnızca tek bir sanal ağ içinde mevcut değil. Ancak, diğer sanal ağlar Azure AD Etki Alanı Hizmetleri'ne kullanıma sunmak için birden çok sanal ağlar arasında bağlantı yapılandırabilirsiniz. Nasıl bu makalede [azure'da sanal ağlara bağlanabilir](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

#### <a name="can-i-enable-azure-ad-domain-services-using-powershell"></a>PowerShell kullanarak Azure AD etki alanı Hizmetleri etkinleştirebilirim?
PowerShell ve otomatik dağıtım Azure AD etki alanı Hizmetleri şu anda kullanılabilir değil.

#### <a name="is-azure-ad-domain-services-available-in-the-new-azure-portal"></a>Azure AD etki alanı Hizmetleri, yeni Azure portalında kullanılabilir?
Hayır. Azure AD etki alanı Hizmetleri yalnızca yapılandırılabilir [Klasik Azure portalı](https://manage.windowsazure.com). Desteğini genişletmek bekliyoruz [Azure portal](https://portal.azure.com) gelecekte.

#### <a name="can-i-add-domain-controllers-to-an-azure-ad-domain-services-managed-domain"></a>Bir Azure AD etki alanı Hizmetleri yönetilen etki alanının etki alanı denetleyicileri ekleyebilir miyim?
Hayır. Azure AD etki alanı Hizmetleri tarafından sağlanan etki alanı yönetilen bir etki alanıdır. Sağlama, yapılandırma veya etki alanı denetleyicileri bu etki alanı - yönetmek gerekmez bu yönetim etkinlikleri bir hizmet olarak Microsoft tarafından sağlanır. Bu nedenle, yönetilen etki alanı için ek etki alanı denetleyicileri (okuma-yazma veya salt okunur) ekleyemezsiniz.

### <a name="administration-and-operations"></a>Yönetim ve işlemler
#### <a name="can-i-connect-to-the-domain-controller-for-my-managed-domain-using-remote-desktop"></a>Uzak Masaüstü kullanarak yönetilen etki alanım için etki alanı denetleyicisine bağlanabilir miyim?
Hayır. Uzak Masaüstü aracılığıyla yönetilen etki alanı için etki alanı denetleyicilerine bağlanmak için gerekli izinlere sahip değil. 'AAD DC Yöneticiler' grubunun üyeleri, yönetilen etki alanı Active Directory Yönetim Merkezi (ADAC) veya AD PowerShell gibi AD Yönetim Araçları'nı kullanarak yönetebilirsiniz. Bu araçlar, yönetilen etki alanına katılmış bir Windows server üzerinde 'Uzak sunucu Yönetim Araçları' özelliği kullanılarak yüklenir.

#### <a name="ive-enabled-azure-ad-domain-services-what-user-account-do-i-use-to-domain-join-machines-to-this-domain"></a>Azure AD etki alanı Hizmetleri etkin. Bu etki alanı için etki alanı katılma makinelere hangi kullanıcı hesabını kullanıyor?
'AAD DC Yöneticiler' yönetim grubunun üyeleri, etki alanına katılma makineler olabilir. Ayrıca, bu grubun üyeleri, etki alanına katılan makineler için Uzak Masaüstü erişimi verilir.

#### <a name="do-i-have-domain-administrator-privileges-for-the-managed-domain-provided-by-azure-ad-domain-services"></a>Azure AD etki alanı Hizmetleri tarafından sağlanan yönetilen etki alanı için etki alanı yönetici ayrıcalıkları var mı?
Hayır. Yönetilen etki alanı üzerinde yönetim ayrıcalıkları verilmez. ' Etki alanı Yöneticisi ' ve ' Kuruluş Yöneticisi ' ayrıcalıkları, etki alanı içinde kullanmak kullanılabilir değil. Ayrıca var olan etki alanı yöneticisi veya Kurumsal Yönetici grupları, Azure AD dizini içinde etki alanındaki etki alanı/kuruluş yönetici ayrıcalıkları verilmez.

#### <a name="can-i-modify-group-memberships-using-ldap-or-other-ad-administrative-tools-on-managed-domains"></a>Yönetilen etki alanlarında LDAP veya diğer AD yönetim araçlarını kullanarak grup üyeliklerini değişiklik yapabilirsiniz?
Hayır. Grup üyelikleri, Azure AD etki alanı Hizmetleri tarafından hizmet verilen etki alanları değiştirilemez. Aynı kullanıcı öznitelikleri için geçerlidir. Azure AD veya şirket içi etki alanınızdaki grup üyeliklerini veya kullanıcı özniteliklerini ancak değişebilir. Bu değişiklikleri otomatik olarak Azure AD Etki Alanı Hizmetleri'ne eşitlenir.

#### <a name="how-long-does-it-take-for-changes-i-make-to-my-azure-ad-directory-to-be-visible-in-my-managed-domain"></a>Ne kadar süreyle sürer değişiklikleri ı my Azure AD dizinine my yönetilen etki alanında görülebilir yapmak?
Azure AD dizininizi Azure AD kullanıcı Arabirimi veya PowerShell kullanarak yapılan değişiklikler, yönetilen etki alanınıza eşitlenir. Bu eşitleme işlemi arka planda çalışır. Dizininizin tek seferlik ilk eşitleme tamamlandıktan sonra genellikle Azure AD'de yönetilen etki alanınızda yansıtılması değişikliklerinin yaklaşık 20 dakika sürer.

#### <a name="can-i-extend-the-schema-of-the-managed-domain-provided-by-azure-ad-domain-services"></a>Azure AD etki alanı Hizmetleri tarafından yönetilen etki alanı tarafından sağlanan şema genişletebilir miyim?
Hayır. Şema, yönetilen etki alanı için Microsoft tarafından yönetilir. Şema uzantıları, Azure AD etki alanı Hizmetleri tarafından desteklenmiyor.

#### <a name="can-i-modify-or-add-dns-records-in-my-managed-domain"></a>I değiştirebilir veya my yönetilen etki alanında DNS kayıtları eklemek?
Evet. 'AAD DC Yöneticiler' grubunun üyeleri yönetilen etki alanındaki DNS kayıtlarını değiştirmek için ' DNS Yöneticisi ', ayrıcalıklarına sahiptir. Bunlar DNS Yöneticisi konsolunu yönetilen etki alanına katılan Windows Server çalıştıran bir makinede DNS yönetmede kullanabilirsiniz. DNS Yöneticisi konsolunu kullanmak için 'DNS sunucusu sunucuda 'Uzak sunucu Yönetim Araçları' isteğe bağlı özellik parçası olan Araçlar','ı yükleyin. Daha fazla bilgi [yönetme, izleme ve DNS sorunlarını giderme için yardımcı programlar](https://technet.microsoft.com/library/cc753579.aspx) TechNet üzerindeki kullanılabilir.

### <a name="billing-and-availability"></a>Faturalama ve kullanılabilirlik
#### <a name="is-azure-ad-domain-services-a-paid-service"></a>Ücretli bir hizmeti Azure AD etki alanı hizmetleri mi?
Evet. Daha fazla bilgi edinmek için bkz. [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/active-directory-ds/).

#### <a name="is-there-a-free-trial-for-the-service"></a>Hizmeti için ücretsiz deneme sürümü var mı?
Bu hizmet Azure ücretsiz deneme sürümüne dahil edilir. Oturum açabileceğiniz bir [ücretsiz bir aylık deneme Azure](https://azure.microsoft.com/pricing/free-trial/).

#### <a name="can-i-get-azure-ad-domain-services-as-part-of-enterprise-mobility-suite-ems-do-i-need-azure-ad-premium-to-use-azure-ad-domain-services"></a>Enterprise Mobility Suite (EMS) bir parçası olarak Azure AD etki alanı Hizmetleri alabilir miyim? Azure AD Etki Alanı Hizmetleri'ni kullanmak için Azure AD Premium'a gerekiyor mu?
Hayır. Azure AD etki alanı Hizmetleri Kullandıkça Öde Azure hizmeti ve EMS bir parçası değil. Azure AD etki alanı Hizmetleri ile Azure ad tüm sürümleri kullanılabilir (ücretsiz, temel ve, Premium). Kullanım bağlı olarak bir saatlik olarak faturalandırılır.

#### <a name="what-azure-regions-is-the-service-available-in"></a>Hangi Azure bölgeleri hizmettir kullanılabilir?
Başvurmak [bölgeye göre Azure Hizmetleri](https://azure.microsoft.com/regions/#services/) burada Azure AD etki alanı Hizmetleri, mevcut Azure bölgelerin bir listesi görmek için sayfayı.
