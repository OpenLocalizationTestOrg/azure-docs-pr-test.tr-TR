---
title: "Azure Active Directory etki alanı Hizmetleri: Dağıtım senaryoları | Microsoft Docs"
description: "Azure AD etki alanı Hizmetleri için dağıtım senaryoları"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c5216ec9-4c4f-4b7e-830b-9d70cf176b20
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: maheshu
ms.openlocfilehash: 8a64bd8f7c6eba8f6490e10fa62bef195b6b3d5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-scenarios-and-use-cases"></a>Dağıtım senaryoları ve kullanım örnekleri
Bu bölümde, birkaç senaryo ve Azure Active Directory (AD) etki alanı Hizmetleri'nden yararlanan kullanım örnekleri ele.

## <a name="secure-easy-administration-of-azure-virtual-machines"></a>Güvenli, kolay yönetim Azure sanal makineler
Azure sanal makinelerinizi Azure Active Directory etki alanı Hizmetleri toomanage kolay bir şekilde kullanabilirsiniz. Azure sanal makineler, böylece şirket AD içinde toolog kimlik bilgileri toouse etkinleştirme birleştirilmiş toohello yönetilen etki alanı olabilir. Bu yaklaşım, yerel yönetici hesapları her Azure sanal makinelerinizin bakımı gibi kimlik bilgisi yönetim Taahhüde önlemeye yardımcı olur.

Yönetilen etki alanına katılmış toohello sunucusu sanal makineleri de yönetilebilir ve Grup İlkesi kullanılarak güvenlik altına. Gerekli güvenlik temelleri tooyour Azure sanal uygulayabilirsiniz makineleri ve bunları Kurumsal güvenlik yönergelerine uygun olarak kilitleme. Örneğin, bu sanal makinelere Grup İlkesi Yönetim yetenekleri toorestrict hello başlatılabilir uygulama türlerini kullanabilirsiniz.

![Azure sanal makinelerin kolaylaştırılmış Yönetim](./media/active-directory-domain-services-scenarios/streamlined-vm-administration.png)

Contoso yaşam uç sunucuları ve diğer altyapıya ulaştığında gibi birçok uygulama şu anda içi toohello bulut üzerinde barındırılan taşımaktır. Geçerli kendi BT standart şirket uygulamaları barındıran sunucu etki alanına katılmış ve Grup İlkesi kullanılarak yönetilen olmalıdır olması zorunlu tutulmuştur. Contoso'nun BT yöneticisi Azure, daha kolay toomake yönetim dağıtılan toodomain birleştirme sanal makinelerin tercih eder. Sonuç olarak, Yöneticiler ve kullanıcılar şirket kimlik bilgilerini kullanarak oturum açabilir. Merhaba, aynı anda makineler Grup İlkesi kullanarak gerekli güvenlik temelleri ile yapılandırılmış toocomply olabilir. Contoso değil toohave toodeploy tercih izlemek ve Azure toosecure etki alanı denetleyicileri yönetmek Azure sanal makineler. Bu nedenle, Azure AD etki alanı Hizmetleri, bu kullanım örneği için harika bir sığdırma olur.

**Dağıtım notları**

Bu dağıtım senaryosu için önemli noktalar aşağıdaki hello göz önünde bulundurun:

* Azure AD etki alanı Hizmetleri tarafından sağlanan yönetilen etki alanları varsayılan olarak tek bir düz OU (kuruluş birimi) yapısı sağlar. Etki alanına katılmış tüm makinelerde tek bir düz OU'da bulunur. Ancak, özel OU'lar toocreate seçebilirsiniz.
* Azure AD etki alanı Hizmetleri, bir yerleşik GPO her hello kullanıcılar ve bilgisayarlar için hello formunda basit Grup İlkesi destekler kapsayıcıları. Özel GPO'ları oluşturmak ve bunları toocustom OU'lar hedefleyebilirsiniz.
* Azure AD etki alanı Hizmetleri hello temel AD bilgisayar nesnesi şemasının destekler. Merhaba bilgisayar nesnesi şemasının genişletemezsiniz.

## <a name="lift-and-shift-an-on-premises-application-that-uses-ldap-bind-authentication-tooazure-infrastructure-services"></a>Yükseltme-ve-shift LDAP bağlama kimlik doğrulaması tooAzure altyapı hizmetleri kullanan bir şirket içi uygulama
![LDAP bağlaması](./media/active-directory-domain-services-scenarios/ldap-bind.png)

Contoso birçok yıl önce bir ISV satın alınmış bir şirket içi uygulama sahiptir. Hello uygulama şu anda bakım modunda hello ISV tarafından ve istekte bulunan değişiklikleri toohello uygulama için Contoso şekilde basımı karşılamayacak kadar pahalıdır. Bu uygulama bir web formu kullanarak kullanıcı kimlik bilgilerini toplar ve ardından bir LDAP bağlama toohello gerçekleştirerek kullanıcıların kimliğini doğrulayan bir web tabanlı bir ön uç sahip kurumsal Active Directory'ye. Contoso toomigrate ister bu uygulama tooAzure altyapı hizmetleri. Merhaba uygulaması, herhangi bir değişiklik gerektirmeden olduğu gibi çalıştığını iyi bir şeydir. Ayrıca, kullanıcıların varolan şirket kimlik bilgilerini kullanarak mümkün tooauthenticate olması ve tooretrain kullanıcılar toodo şeyler farklı sahip olmadan gerekir. Diğer bir deyişle, son kullanıcıların Merhaba uygulaması çalıştığı oblivious olmalıdır ve hello geçiş saydam toothem olması gerekir.

**Dağıtım notları**

Bu dağıtım senaryosu için önemli noktalar aşağıdaki hello göz önünde bulundurun:

* Merhaba uygulaması toomodify/yazma toohello dizin gerekmez emin olun. LDAP yazma erişimi toomanaged etki alanlarının Azure AD etki alanı Hizmetleri tarafından sağlanan desteklenmiyor.
* Parolaları hello yönetilen etki alanına karşı doğrudan değiştiremezsiniz. Son kullanıcıların parolalarını değiştirebilir ya da Azure AD Self Servis parola değişikliği mekanizmasını kullanarak veya hello şirket içi dizin karşı. Bu değişiklikler hello yönetilen etki alanında otomatik olarak eşitlenmesi ve kullanılabilir.

## <a name="lift-and-shift-an-on-premises-application-that-uses-ldap-read-tooaccess-hello-directory-tooazure-infrastructure-services"></a>Yükseltme ve shift LDAP kullanan bir şirket içi uygulama tooaccess hello dizin tooAzure altyapı hizmetleri okuyun.
Contoso hemen önce bir on geliştirilmiştir bir şirket içi iş kolu (LOB) uygulama sahiptir. Bu uygulama dizini kullanan ve Windows Server AD ile tasarlanmış toowork oluştu. Merhaba uygulaması LDAP (Basit Dizin Erişimi Protokolü) tooread bilgi/öznitelikler Active Directory'den kullanıcıları hakkında kullanır. Merhaba uygulaması öznitelikleri değiştirmeyin veya aksi halde toohello directory yazma. Contoso toomigrate ister bu uygulama tooAzure altyapı hizmetleri ve şu anda bu uygulamayı barındıran hello eskime şirket içi donanım devre dışı bırakma. Merhaba uygulaması yeniden toouse modern dizin API'leri hello REST tabanlı Azure AD grafik API'si gibi olamaz. Bu nedenle, Hello uygulama bulutta kodunu değiştirme veya hello uygulama yeniden yazma işlemi olmadan Merhaba, geçirilen toorun olabilir aslına yükseltme shift seçeneği istenen.

**Dağıtım notları**

Bu dağıtım senaryosu için önemli noktalar aşağıdaki hello göz önünde bulundurun:

* Merhaba uygulaması toomodify/yazma toohello dizin gerekmez emin olun. LDAP yazma erişimi toomanaged etki alanlarının Azure AD etki alanı Hizmetleri tarafından sağlanan desteklenmiyor.
* Merhaba uygulaması özel genişletilmiş Active Directory Şeması'nı gerekmez emin olun. Şema uzantıları, Azure AD Etki Alanı Hizmetleri'nde desteklenmez.

## <a name="migrate-an-on-premises-service-or-daemon-application-tooazure-infrastructure-services"></a>Bir şirket içi hizmet veya arka plan programı uygulama tooAzure altyapı hizmetleri geçirme
Bazı uygulamalar, burada bir hello katmanı tooperform kimliği doğrulanmış çağrıları tooa arka uç katmanı veritabanı katmanı gibi gereken birden çok katman oluşur. Active Directory hizmet hesapları, bu kullanım durumları için yaygın olarak kullanılır. Yükseltme ve kaydırma için bu tür uygulamalar tooAzure altyapı hizmetleri ve kullanım hello kimlik gereksinimlerini bu uygulamaları için Azure AD etki alanı Hizmetleri. Seçebileceğiniz toouse Merhaba, şirket içi dizin tooAzure AD eşitlenen hizmet hesabıyla aynı. Alternatif olarak, önce özel bir OU oluşturmanız ve ardından bu OU'da toodeploy ayrı bir hizmet hesabı bu tür uygulamalar oluşturun.

![WIA kullanarak hizmeti hesabı](./media/active-directory-domain-services-scenarios/wia-service-account.png)

Contoso web ön uç, bir SQL server ve arka uç FTP sunucusu içeren bir özel olarak geliştirilmiş yazılımlar kasası uygulama vardır. Hizmet hesapları Windows tümleşik kimlik doğrulaması kullanılan tooauthenticate hello web ön uç toohello FTP sunucusudur. Merhaba web ön ucu toorun bir hizmet hesabı olarak ayarlanır. Merhaba arka uç sunucusu yapılandırılmış hello hizmet hesabından tooauthorize erişim hello web ön uç için. Contoso, bu uygulama tooAzure altyapı hizmetleri değil toohave toodeploy hello bulut toomove etki alanı denetleyicisi sanal makinede tercih eder. Contoso'nun BT yöneticisi hello web ön uç, SQL server ve hello FTP sunucusu tooAzure sanal makineleri barındıran hello sunucuları dağıtabilirsiniz. Etki alanına katılmış tooan Azure AD etki alanı Hizmetleri yönetilen sonra bu makinelerdir. Daha sonra kullanabilirsiniz hello kendi şirket içi dizininde hello uygulamanın kimlik doğrulama amacıyla hizmet hesabıyla aynı. Bu hizmet hesabı eşitlenmiş toohello Azure AD etki alanı Hizmetleri yönetilen etki alanı ve kullanıma hazırdır.

**Dağıtım notları**

Bu dağıtım senaryosu için önemli noktalar aşağıdaki hello göz önünde bulundurun:

* Merhaba uygulama kimlik doğrulaması için kullanıcı adı/parola kullandığından emin olun. Sertifika/akıllı kart tabanlı kimlik doğrulaması Azure AD etki alanı Hizmetleri tarafından desteklenmiyor.
* Parolaları hello yönetilen etki alanına karşı doğrudan değiştiremezsiniz. Son kullanıcıların parolalarını değiştirebilir ya da Azure AD Self Servis parola değişikliği mekanizmasını kullanarak veya hello şirket içi dizin karşı. Bu değişiklikler hello yönetilen etki alanında otomatik olarak eşitlenmesi ve kullanılabilir.

## <a name="windows-server-remote-desktop-services-deployments-in-azure"></a>Azure dağıtımları Windows Server Uzak Masaüstü Hizmetleri
Azure AD Etki Alanı Hizmetleri'ni tooprovide yönetilen AD kullanabilirsiniz etki alanı Hizmetleri tooyour Uzak Masaüstü sunucuları Azure'da dağıtılabilir.

Bu dağıtım senaryosu hakkında daha fazla bilgi için bkz. nasıl çok[RDS dağıtımı ile Azure AD etki alanı Hizmetleri Tümleştirme](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-azure-adds).
