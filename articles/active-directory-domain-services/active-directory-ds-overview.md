---
title: "Azure Active Directory etki alanı Hizmetleri'nin aaaOverview | Microsoft Docs"
description: "Azure Active Directory etki alanı Hizmetleri'ne Genel Bakış"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 0d47178f-773e-45f9-9ff4-9e8cffa4ffa2
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 2b4884b3b8b639fcca438ddbab0bd3361aac53c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services"></a>Azure AD Domain Services
## <a name="overview"></a>Genel Bakış
Azure altyapı hizmetleri toodeploy çözümleri Çevik bir şekilde bilgi işlem çok çeşitli etkinleştirin. Azure Virtual Machines ile neredeyse anlık olarak dağıtabilir ve yalnızca hello dakikaya göre ödeme. Windows, Linux, SQL Server, Oracle, IBM, SAP ve BizTalk için destek kullanarak dağıtabileceğiniz herhangi bir iş yükü, neredeyse tüm işletim sisteminde herhangi bir dil. Avantajlar toomigrate dağıtılan eski uygulamalar şirket içi tooAzure, toosave üzerinde işletim masrafları'nı etkinleştirin.

Geçiş işleminin en önemli parçalarından uygulamaları tooAzure bu uygulamaların hello kimlik gereksinimlerini işleme şirket içi. Dizin ile uyumlu uygulamalar LDAP üzerinde okuma veya yazma erişimi toohello şirket dizini kullanır veya Windows tümleşik kimlik doğrulaması (Kerberos veya NTLM kimlik doğrulaması) tooauthenticate son kullanıcılara kullanır. Güvenli bir şekilde Grup İlkesi kullanılarak yönetilebilir dağıtılır, bu nedenle Windows Server'da çalışan satır iş kolu (LOB) uygulamaları genellikle etki alanına katılmış makinelerde. too'lift kaydırma ' şirket içi uygulamalar toohello bulut hello Kurumsal kimlik altyapısı bu bağımlılıkları çözülmüş toobe gerekir.

Yöneticiler genellikle çözümleri toosatisfy hello kimlik Azure'de dağıtılan uygulamalarını ihtiyaçlarını aşağıdaki hello tooone açın:

* Azure altyapı hizmetleri ve hello Kurumsal şirket içi dizin çalışan iş yükleri arasında bir siteden siteye VPN bağlantısı dağıtın.
* Azure sanal makineleri kullanarak kopya etki alanı denetleyicilerini ayarlayarak Hello şirket AD etki alanında/ormanda altyapısını genişletir.
* Tek başına bir etki alanında etki alanı denetleyicilerini Azure sanal makineleri olarak dağıtılan kullanarak Azure dağıtın.

Bu yaklaşım, yüksek maliyet ve yönetim yükünü yaşar. Azure'da sanal makineleri kullanarak gerekli toodeploy etki alanı denetleyicilerinin yöneticilerdir. Ayrıca, bunlar toomanage, güvenli, düzeltme eki, monitör, yedekleme gerekir ve bu sanal makineleri sorun giderme. VPN bağlantıları toohello Hello bağımlılık dizin Azure toobe savunmasız tootransient ağ hataları veya kesintileri dağıtılmış iş yükleri neden olan şirket içi. Bu ağ kesintileri alt açık kalma süresi ve bu uygulamalar için düşük güvenilirlik, sırayla sonuçlanır.

Biz, Azure AD etki alanı Hizmetleri tooprovide daha kolay alternatif tasarlanmıştır.

## <a name="introducing-azure-ad-domain-services"></a>Azure AD etki alanı hizmetlerine giriş
Azure AD etki alanı Hizmetleri yönetilen etki alanı Hizmetleri gibi etki alanına katılma, Windows Server Active Directory ile tamamen uyumlu Grup İlkesi, LDAP, Kerberos/NTLM kimlik doğrulaması sağlar. Bu etki alanı Hizmetleri, toodeploy hello gerek kalmadan kullanmak, yönetmek ve etki alanı denetleyicileri hello bulutta düzeltme eki. Azure AD etki alanı Hizmetleri bu nedenle, Kurumsal kimlik bilgilerini kullanarak oturum için kullanıcıların toolog edinerek, mevcut Azure AD kiracısı ile tümleşir. Ayrıca, böylece bir sorunsuz 'yükseltme-ve-shift' şirket içi kaynakları tooAzure altyapı hizmetleri, sağlama mevcut gruplar ve kullanıcı hesaplarını toosecure erişim tooresources kullanabilirsiniz.

Azure AD kiracınıza yalnızca Bulut veya şirket içi Active Directory ile eşitlenmiş olduğuna bakılmaksızın Azure AD etki alanı hizmetleri işlevleri sorunsuz çalışır.

### <a name="azure-ad-domain-services-for-cloud-only-organizations"></a>Yalnızca bulut kuruluşlar için Azure AD etki alanı Hizmetleri
Yalnızca bulutta Azure AD Kiracı (genellikle başvurulan tooas ' kiracılar yönetilen') tüm şirket içi kimlik alanlarına sahip değil. Diğer bir deyişle, kullanıcı hesaplarını, parolaları ve grup üyeliklerini diğer bir deyişle, oluşturulan ve Azure AD'de yönetilen, tüm yerel toohello bulut - var. Bir süre Contoso salt bulut olduğunu göz önünde bulundurun Azure AD kiracısı. Contoso'nun yönetici hello aşağıdaki çizimde gösterildiği gibi Azure altyapı Hizmetleri'nde bir sanal ağ yapılandırdı. Uygulamaları ve sunucu iş yükleri, bu sanal ağ Azure sanal makinelerde dağıtılır. Contoso bir yalnızca bulut Kiracı olduğundan, tüm kullanıcı kimlikleri, kimlik bilgileri ve grup üyeliklerini oluşturulur ve Azure AD içinde yönetilir.

![Azure AD etki alanı hizmetleri genel bakış](./media/active-directory-domain-services-overview/aadds-overview.png)

Contoso'nun BT yöneticisi kendi Azure AD kiracısı Azure AD Etki Alanı Hizmetleri'ni etkinleştirmek ve etki alanı Hizmetleri bu sanal ağda kullanılabilir toomake seçin. Bundan sonra Azure AD etki alanı Hizmetleri yönetilen etki alanı sağlar ve hello sanal ağınızda kullanılabilir hale getirir. Ayrıca tüm kullanıcı hesapları, grup üyelikleri ve kullanıcı kimlik bilgilerini Contoso Azure AD kiracısında kullanılabilir yeni oluşturulan bu etki alanında kullanılabilir. Bu özellik hello kuruluş toosign şirket kimlik bilgilerini - örneğin, Uzak Masaüstü aracılığıyla uzaktan toodomain katılmış makineler bağlanırken kullanarak toohello etki alanındaki kullanıcılar sağlar. Yöneticiler, var olan grup üyelikleri kullanarak hello etki alanındaki erişim tooresources sağlayabilir. Merhaba sanal ağdaki sanal makinelerinde dağıtılan uygulamalar gibi etki alanına katılma, LDAP okuma, LDAP bağlama, NTLM ve Kerberos kimlik doğrulaması ve Grup İlkesi özellikleri kullanabilirsiniz.

Azure AD etki alanı Hizmetleri tarafından sağlanan hello yönetilen etki alanı birkaç belirgin yönleri şunlardır:

* Contoso'nun BT yöneticisi toomanage, gerekli olmayan düzeltme eki veya bu etki alanına veya bu yönetilen etki alanı için etki alanı denetleyicisi izleyin.
* Bu etki alanı için gereksinim toomanage AD çoğaltma yoktur. Kullanıcı hesapları, grup üyelikleri ve Contoso Azure AD Kiracı kimlik bilgilerini Bu yönetilen etki alanı içinde otomatik olarak kullanılabilir.
* Azure AD etki alanı Hizmetleri tarafından Contoso ait Hello etki alanı yönetildiğinden BT yöneticisine bu etki alanında etki alanı yöneticisi veya kuruluş yöneticisi ayrıcalıkları yok.

### <a name="azure-ad-domain-services-for-hybrid-organizations"></a>Karma kuruluşlar için Azure AD etki alanı Hizmetleri
Karma BT altyapısı olan kuruluşlar, Bulut ve şirket kaynaklarının karışımını tüketir. Bu tür kuruluşlar kendi şirket içi dizin tootheir Azure AD Kiracı kimlik bilgilerinden eşitleyin. Azure AD etki alanı Hizmetleri karma kuruluşlar kendi şirket içi uygulamalar toohello bulutun, özellikle eski dizin kullanabilen uygulamaların, daha fazla toomigrate Ara yararlı toothem olabilir.

Lıtware Corporation dağıtılan [Azure AD Connect](../active-directory/active-directory-aadconnect.md), kendi şirket içi dizin tootheir Azure AD Kiracı toosynchronize kimlik bilgileri. Eşitlenen hello kimlik bilgileri, kullanıcı hesapları, kimlik doğrulaması (Parola Eşitleme) ve grup üyeliklerini kendi kimlik bilgisi karmalarını içerir.

> [!NOTE]
> **Karma kuruluşlar toouse Azure AD etki alanı Hizmetleri için parola eşitleme zorunludur**. Kullanıcıların kimlik bilgilerini yönetilen hello gerekli olduğu için bu etki alanı, bu kullanıcılar NTLM veya Kerberos kimlik doğrulama yöntemleri aracılığıyla tooauthenticate Azure AD etki alanı Hizmetleri tarafından sağlanan gereksinimdir.
>
>

![Lıtware Corporation için Azure AD etki alanı Hizmetleri](./media/active-directory-domain-services-overview/aadds-overview-synced-tenant.png)

Merhaba önceki çizim karma Lıtware Corporation gibi BT altyapısı olan kuruluşlar Azure AD etki alanı hizmetleri nasıl kullanabileceğinizi gösterir. Lıtware 's uygulamaları ve etki alanı Hizmetleri gerektiren sunucu iş yükleri, Azure altyapı Hizmetleri'nde bir sanal ağ içinde dağıtılır. Lıtware 's BT yöneticisi kendi Azure AD kiracısı Azure AD Etki Alanı Hizmetleri'ni etkinleştirmek ve yönetilen bir etki alanına bu sanal ağda kullanılabilir toomake seçin. Lıtware bir kuruluşla karma BT altyapısı olmadığından, kullanıcı hesaplarını, grupları ve kimlik bilgileri, şirket içi dizinlerini eşitlenmiş tootheir Azure AD kiracısı olan. Bu özellik şirket kimlik bilgilerini kullanarak toohello etki alanındaki kullanıcıların toosign sağlar - Örneğin, uzaktan bağlanırken toomachines Uzak Masaüstü toohello etki alanına katılmış. Yöneticiler, var olan grup üyelikleri kullanarak hello etki alanındaki erişim tooresources sağlayabilir. Merhaba sanal ağdaki sanal makinelerinde dağıtılan uygulamalar gibi etki alanına katılma, LDAP okuma, LDAP bağlama, NTLM ve Kerberos kimlik doğrulaması ve Grup İlkesi özellikleri kullanabilirsiniz.

Azure AD etki alanı Hizmetleri tarafından sağlanan hello yönetilen etki alanı birkaç belirgin yönleri şunlardır:

* Merhaba yönetilen etki alanı tek başına bir etki alanıdır. Uzantı Lıtware 's şirket içi etki alanının değil.
* Lıtware 's BT yöneticisi gerekmez toomanage, düzeltme eki veya İzleyici etki alanı denetleyicileri Bu yönetilen etki alanı için.
* Hiçbir gerek toomanage AD çoğaltma toothis etki alanı yoktur. Kullanıcı hesapları, grup üyelikleri ve Lıtware 's şirket içi dizin kimlik bilgilerini Azure AD Connect eşitlenmiş tooAzure AD var. Bu kullanıcı hesapları, grup üyelikleri ve kimlik bilgilerini hello yönetilen etki alanı içinde otomatik olarak kullanılabilir.
* Azure AD etki alanı Hizmetleri tarafından Lıtware 's Hello etki alanı yönetildiğinden BT yöneticisine bu etki alanında etki alanı yöneticisi veya kuruluş yöneticisi ayrıcalıkları yok.

## <a name="benefits"></a>Avantajlar
Azure AD etki alanı Hizmetleri ile avantajları aşağıdaki hello keyfini çıkarabilirsiniz:

* **Basit** – hello kimlik gereksinimlerini sanal makinelerin tooAzure altyapı hizmetleri birkaç basit tıklama ile dağıtılan karşılayabilen. Değil toodeploy gerekir ve kimlik altyapısında Azure veya Kurulum Bağlantı geri tooyour şirket içi kimlik altyapınızı yönetin.
* **Tümleşik** – Azure AD etki alanı Hizmetleri ile Azure AD kiracınıza son derece tümleşiktir. Şimdi, Azure AD modern uygulamalar ve geleneksel directory kullanabilen uygulamaların toohello gereksinimlerini caters bir tümleşik Kurumsal bulut tabanlı dizini olarak kullanabilirsiniz.
* **Uyumlu** – Azure AD etki alanı Hizmetleri, Itanium tabanlı sistemler için hello kanıtlanmış Kurumsal düzeyde altyapınız Windows Server Active Directory üzerinde oluşturulur. Bu nedenle, uygulamalarınızı bir Windows Server Active Directory özellikleri ile uyumluluk büyük ölçüde güvenebilirsiniz. Windows Server AD kullanılabilen tüm özellikleri şu anda Azure AD Etki Alanı Hizmetleri'nde kullanılabilir. Ancak, kullanılabilir özellikleri şirket içi altyapınızda Bel hello karşılık gelen Windows Server AD özellikleri ile uyumlu değildir. Merhaba LDAP Kerberos, NTLM, Grup İlkesi ve etki alanı katılma özellikleri, test ve çeşitli Windows Server sürümleri iyileştirilmiştir olgun bir teklifi oluşturur.
* **Düşük maliyetli** – Azure AD etki alanı Hizmetleri ile kimlik altyapısı toosupport geleneksel dizin algılayan uygulamaları yönetme ile ilişkili hello altyapı ve yönetim yükünü önleyebilirsiniz. Bu uygulamalar tooAzure altyapı hizmetleri taşıyın ve işletim masrafları'nı hakkında daha fazla tasarruf etmenizi yararlı.
