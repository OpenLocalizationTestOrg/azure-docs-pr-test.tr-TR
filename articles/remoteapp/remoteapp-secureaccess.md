---
title: "aaaSecuring erişim tooAzure RemoteApp ve ötesine | Microsoft Docs"
description: "Azure Active Directory'de koşullu erişim kullanarak ne kadar güvenli erişim tooAzure RemoteApp öğrenin"
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: a19b0b09-ab26-4beb-80bb-33a46da39887
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 98dfe69e2f5fa5014b6eb3157e01f131c287134d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-access-tooazure-remoteapp-and-beyond"></a>Erişim tooAzure RemoteApp, güvenli hale getirme ve ötesine
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Bu makalede biz nasıl yönetici hello son kullanıcının Azure RemoteApp üzerinden başlayarak ve bir SQL veritabanı veya başka bir uygulama arka uç gibi güvenli bir kaynak ile biten bir güvenli erişim kanal ayarlayabilirsiniz genel bir bakış sunar. Merhaba, toplantı hello koşullar uzak uygulamaları erişebilir ve güvenli arka uç hello istenen yalnızca yetkili kullanıcılar yalnızca denetimli hello Azure RemoteApp ortamından ve diğer konumlardan erişilebildiğinden emin toomake hedefidir.

Hello Yöneticisi adresindeki toolook gereken 3 önemli alanlar şunlardır:

![Azure RemoteApp koşullu erişim konuları](./media/remoteapp-secureaccess/ra-conditionalenvironment.png)

Bilgi ve yanıtlar toothese sorular için okumaya devam edin.

## <a name="who-can-access-hello-collection"></a>Merhaba koleksiyonu erişebilecek mi?
Hello Yöneticisi hello koleksiyonundaki uzak uygulamaları erişebilir hello kullanıcıları seçer. Azure Active Directory (Azure AD) iş veya Okul hesapları (daha önce adı, "Kurumsal hesaplar") veya Microsoft hesapları kullanabilirsiniz (örneğin @outlook.com). Çoğu kuruluş senaryoları Azure AD hesapları kullanın; Bunlar daha sonra ele alınan koşullu erişim özellikleri kullanmanıza olanak tanır ve ayrıca hello yalnızca etki alanına katılmış koleksiyonlar için bir seçimdir. Merhaba makalenin devamında, hello Azure RemoteApp ile Azure AD hesapları kullandığınızı varsayar.

**Ne biz gerçekleştirdiniz:**

Azure AD hesapları toocontrol erişim tooAzure RemoteApp bize iki şey veriyor kullanma:

1. Her zaman yayımladıysanız ve bu uygulamaları herhangi bir arka uç erişim uygulamaları bağlanmak hello erişebilecek kişileri biliyoruz.
2. Biz oluşturabilir ve delete kullanıcı hesapları, parola ilkeleri ayarlarsanız, çok faktörlü kimlik doğrulaması, vb. şekilde Azure AD temel hello kontrol eder. 

## <a name="how-is-hello-collection-accessed-from-where"></a>Merhaba koleksiyonu nasıl erişilir? Nereden?
Yaygın olarak Yöneticiler, Azure RemoteApp gibi bir ortak Internet'e ortamı erişmek için toodefine ilkeleri istiyor. Örneğin, tooensure hello ortamının hello şirket ağı dışında erişen kullanıcılar toouse çok faktörlü kimlik doğrulaması (MFA) toogain erişimi olmasını istediğiniz; veya belki de bunlar tamamen engellenmelidir.

Azure RemoteApp yöneticiler kendi Azure RemoteApp ortamı için Azure AD Premium tooset koşullu erişim ilkeleri kullanılabilen hello işlevini kullanabilirsiniz. Zengin raporlama ve hello ortamı nasıl erişiliyor uyarı özellikleri toomonitor de kullanabilirsiniz.

### <a name="how-tooset-up-conditional-access-for-azure-remoteapp"></a>Nasıl tooset Azure RemoteApp için koşullu erişim
Örnek bir senaryo üzerinden giderek toowalk duyuyoruz – kullanıcılar hello şirket ağının dışından olduğunda hello Azure RemoteApp Yöneticisi tooblock erişim toohello ortam ister.

> [!NOTE]
> Azure AD toohello Premium katmanı yükselttikten sonra en az bir Azure RemoteApp koleksiyonu oluşturdunuz varsayıyoruz.
> 
> 

1. Azure portalında hello tıklatın **Active Directory** sekmesi. Tooconfigure istediğiniz hello dizini'ye tıklayın.
   
   Unutmayın: tüm yapılandırma hello dizin düzeyinde yapıldığını için koşullu erişim dizininiz ve Azure RemoteApp, değil bir özelliğidir. Bu, aynı zamanda bu değişiklikleri toobe hello directory yönetici toomake gerekir anlamına gelir.
2. Tıklatın **uygulamaları**ve ardından **Microsoft Azure RemoteApp** tooset koşullu erişim. Her bir "hizmet olarak yazılım" uygulama için koşullu erişim dizininizde ayrı olarak ayarlayabilirsiniz unutmayın.
   ![Azure RemoteApp için koşullu erişimi ayarlama](./media/remoteapp-secureaccess/ra-conditionalaccessscreen.png)
3. Merhaba üzerinde **yapılandırma** sekmesinde, ayarlamak **erişim kurallarını etkinleştirme** tooON.
   ![Azure RemoteApp için erişim kurallarını etkinleştirin](./media/remoteapp-secureaccess/ra-enableaccessrules.png)
4. Şimdi çeşitli kurallarını yapılandırmak ve kimlerin tooapply seçin onları:
   
   1. Seçin **iş olduğunda değil, erişimi engelleme** toocompletely kullanıcılar hello ağ ortamının dışında belirttiğiniz Azure RemoteApp erişmesini engellemek.
   2. "Güvenilen ağınıza." oluşturan toodefine hello IP adres aralıklarını aşağıda Hello seçeneği tıklatın Olanlar dışında her şeyi reddedilir.
5. Belirttiğiniz hello aralığın dışında bir IP adresinden hello Azure RemoteApp istemci başlatarak yapılandırmanızı sınayın. Azure AD kimlik bilgilerinizle oturum sonra şuna benzer bir ileti görürsünüz:

![Reddedilen erişim tooAzure RemoteApp](./media/remoteapp-secureaccess/ra-accessdenied.png)

### <a name="future-conditional-access-features"></a>Gelecekteki koşullu erişim özellikleri
Hello Azure Active Directory ekibi, koşullu erişim sürümündeki yeni özellikler üzerinde çalışmaktadır. Yöneticiler mümkün toocreate yeni tür ağ konumuna dayalı kurallar ötesinde kuralların olacaktır. Merhaba yeni işlevsellik genel önizlemesini hemen kullanılabilir olması gerekir.

### <a name="how-toomonitor-access-tooazure-remoteapp"></a>Nasıl toomonitor erişim tooAzure RemoteApp
Koşullu erişim yanında bir önemli özellik toouse hello Azure Active Directory Premium raporlama işlevdir. Tüm şüpheli etkinlikleri algılamak ve ortamınıza erişen raporlar toomonitor kullanın.

Örneğin, Azure RemoteApp, yaptıkları işlemin, kaç kez erişilen hello kullanıcıların hello adlarını görebilirsiniz ve ne zaman.

1. Azure portalında tıklatın **Active Directory**ve ardından dizininizi'ı tıklatın.
2. Toohello Git **raporları** sekmesi.
3. Merhaba raporlar listesinden **uygulama kullanımı** altında **tümleşik uygulamalar**.
   
   Azure RemoteApp için bazı toplu istatistikler görürsünüz. 
   ![Toplanan Azure RemoteApp erişim istatistikleri](./media/remoteapp-secureaccess/ra-accessstats.png)
4. Azure RemoteApp erişen kullanıcılar hakkında Hello uygulama tooreveal bilgi tıklatın.
   ![Azure RemoteApp kullanıcı erişimi istatistikleri](./media/remoteapp-secureaccess/ra-userstats.png)

### <a name="summary"></a>Özet
Azure Active Directory Premium ile erişim kuralları tooAzure RemoteApp (ve diğer yazılım hizmet uygulamaları Azure AD üzerinden kullanılabilir olarak) ayarlayabilirsiniz. Kuralları şu anda sınırlı toonetwork göre konumuna ilkelerdir ancak hello gelecekteki kuruluş yönetimi tooother yönlerini uzatılır.

Azure AD Premium ayrıca raporlama sunar ve bunların Azure RemoteApp ortamınız üzerinde daha fazla hello denetim hello Yöneticisi genişletmek yetenekleri izleme sahiptir.

## <a name="how-do-i-make-sure-my-secure-resource-is-accessible-only-from-my-azure-remoteapp-environment"></a>My güvenli bir kaynak yalnızca benim Azure RemoteApp Ortamı'ndan erişilebilen nasıl emin?
Bu makalenin önceki bölümlerinde erişim toohello Azure RemoteApp ortamında güvenliğini sağlama konusunda odaklanır. Biz, erişim izni verilen hello kullanıcılar seçme ve erişim kuralları toofurther kontrolünü hello hizmeti nasıl kullanabileceklerini ayarlama elde.

Azure RemoteApp dağıtımlar için yaygın bir senaryo hello uzak uygulamalarını bir arka uç kaynağı, örneğin bir SQL veritabanı ile toocommunicate olmanızdır. Bu kaynak barındırılan ya da şirket içi (örneğin bir kurumsal ağ) veya hello bulutta (örneğin Azure Iaas). Yöneticiler genellikle toomake hello arka uç kaynak yalnızca Azure RemoteApp dağıtılan uygulamalar ve olmayan örneğin doğrudan bir kullanıcının bilgisayarı üzerinde çalışan ve ortak Internet üzerinden erişen bir uygulama tarafından erişilebildiğinden emin istiyor. Azure RemoteApp çok hello merkezi olarak yönetilen ve güvenli ortamı ve bu nedenle hello tek yolu üzerinden kullanıcılar ile etkileşimde arka uç kaynak hello görülür.

Merhaba tooplace, her ikisi de hello Azure RemoteApp ortamında ve hello güvenli kaynağında hello aynı Azure sanal ağ (VNET) çözümüdür. Merhaba kaynak farklı bir site ise, örneğin toocreate bir VNet yayılan hello Azure veri merkezi ve hello müşterinin şirket içi ortamına siteden siteye VPN bağlantısı kurabilirsiniz.

Azure RemoteApp koleksiyonu dağıtımları kendi VNET burada sağlayabilir iki türlerini destekler:

* Olmayan etki alanına katılmış: hello uygulamaları "görüş" hello, diğer kaynakları hello VNET gerekir. Örneğin, bu SQL kimlik doğrulaması kullanan kullanılan tooconnect uygulamaları tooa SQL veritabanı olabilir (uygulamaları hello veritabanı karşı doğrudan hello kullanıcı kimlik doğrulaması)
* Etki alanına katılmış: hello sanal Azure RemoteApp tarafından kullanılan birleştirilmiş tooa etki alanı denetleyicisi hello sanal makinelerdir. Merhaba uygulamaları sipariş tooget erişim tooa arka uç kaynak bir Windows etki alanı denetleyicisine karşı tooauthenticate gerektiğinde kullanışlıdır.
  ![Azure RemoteApp etki alanına katılmış bir koleksiyonda](./media/remoteapp-secureaccess/ra-domainjoined.png)

### <a name="how-toocreate-a-secure-connection-between-azure-and-my-on-premises-environment"></a>Nasıl toocreate my içi ortamınız ile Azure arasındaki güvenli bir bağlantı
Azure ve şirket içi ortamlarınızın bağlamak için çeşitli yapılandırma seçenekleri vardır. Başlangıç seçenekleri iyi bir genel bakış burada kullanılabilir.

Azure RemoteApp ile tooconfigure önce Vnet'inizi gerekir ve hello oluşturma işlemi sırasında koleksiyonun kullanın. 

## <a name="hello-complete-solution"></a>Merhaba çözümü
Merhaba diyagrama burada güvenli erişim kanal hello son kullanıcıdan aracılığıyla Azure RemoteApp (ARA), hello arka uç kaynağını oluşturduğumuz hello eksiksiz bir çözüm gösterir.
![Azure RemoteApp güvenli](./media/remoteapp-secureaccess/ra-secureoverview.png) aşama seçilen hello kullanıcılar ve ARA nasıl erişilebileceğini yöneten erişim kuralları oluşturulan 1. Merhaba aşağıdaki örnekte yalnızca erişim hello şirket ağından çalışan kullanıcılar için izin veriyoruz. Uyumlu olmayan kullanıcıları mümkün tooaccess hello ARA ortamı hiç olmaz.
Aşama 2'de biz hello arka uç kaynak biz denetleyen hello VNet/VPN yapılandırma yoluyla kullanıma sunulan. Azure RemoteApp yerleştirilen hello aynı sanal ağ. Merhaba son hello kaynağa yalnızca hello ARA ortamı üzerinden erişilmesi sonucudur.

