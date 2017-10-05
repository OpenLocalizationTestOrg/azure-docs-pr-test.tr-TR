---
title: "Azure RemoteApp ve ötesinde erişim güvenliğini sağlama | Microsoft Docs"
description: "Azure Active Directory'de koşullu erişim kullanarak Azure RemoteApp nasıl güvenli erişim öğrenin"
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
ms.openlocfilehash: 28ee4698515d11964e5371628d21dbc00687c861
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="securing-access-to-azure-remoteapp-and-beyond"></a>Azure RemoteApp ve ötesinde erişim güvenliğini sağlama
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

Bu makalede biz nasıl yönetici son kullanıcının Azure RemoteApp üzerinden başlayarak ve bir SQL veritabanı veya başka bir uygulama arka uç gibi güvenli bir kaynak ile biten bir güvenli erişim kanal ayarlayabilirsiniz genel bir bakış sunar. Hedef, istenen koşullara uyan yalnızca yetkili kullanıcılar uzak uygulamalar erişebilir ve güvenli arka uç yalnızca denetimli Azure RemoteApp ortamından ve diğer konumlardan erişilebildiğinden emin olmaktır.

Yönetici bakmak için gereken 3 önemli alanlar şunlardır:

![Azure RemoteApp koşullu erişim konuları](./media/remoteapp-secureaccess/ra-conditionalenvironment.png)

Bilgi ve bu soruların yanıtları için okuma.

## <a name="who-can-access-the-collection"></a>Koleksiyon erişebilecek mi?
Yöneticinin uzak uygulamaları koleksiyondaki erişebilir kullanıcıları seçer. Azure Active Directory (Azure AD) iş veya Okul hesapları (daha önce adı, "Kurumsal hesaplar") veya Microsoft hesapları kullanabilirsiniz (örneğin @outlook.com). Çoğu kuruluş senaryoları Azure AD hesapları kullanın; Bunlar özellikleri daha sonra ele alınan ve aynı zamanda yalnızca etki alanına katılmış koleksiyonlar için seçimdir koşullu erişim kullanmanıza olanak tanır. Makalenin kalanında Azure RemoteApp ile Azure AD hesapları kullandığınızı varsayar.

**Ne biz gerçekleştirdiniz:**

Azure RemoteApp erişimi denetlemek için Azure AD hesapları kullanarak bize iki şey sağlar:

1. Her zaman yayımladıysanız ve erişmesi uygulamaları erişebilecek kişileri biliyoruz arka uçları bu uygulamalara bağlanmak için.
2. Temel alınan Azure AD oluşturabilir ve delete kullanıcı hesapları, parola ilkeleri ayarlarsanız, çok faktörlü kimlik doğrulaması, vb. şekilde denetler. 

## <a name="how-is-the-collection-accessed-from-where"></a>Koleksiyon nasıl erişilir? Nereden?
Yaygın olarak yöneticiler Azure RemoteApp gibi genel Internet'e yönelik ortam erişim ilkeleri tanımlamak istersiniz. Örneğin, bunlar şirket ağı dışından ortamından erişen kullanıcıların erişim kazanmak için çok faktörlü kimlik doğrulaması (MFA) kullanmak zorunda olmak istiyorsanız; veya belki de bunlar tamamen engellenmelidir.

Azure RemoteApp Yöneticiler, Azure RemoteApp ortamlarına için koşullu erişim ilkeleri ayarlamak için Azure AD Premium kullanılabilir işlevini kullanabilirsiniz. Bunlar ayrıca zengin raporlama ve özellikleri uyarı ortamı nasıl erişiliyor izlemek için kullanabilirsiniz.

### <a name="how-to-set-up-conditional-access-for-azure-remoteapp"></a>Azure RemoteApp için koşullu erişimi ayarlama
Örnek bir senaryo – yönetici, kullanıcıların şirket ağının dışından olduğunda ortamına erişimi engellemek istediği Azure RemoteApp rehberlik olacak.

> [!NOTE]
> Azure AD Premium katmanına yükselttikten sonra en az bir Azure RemoteApp koleksiyonu oluşturdunuz varsayıyoruz.
> 
> 

1. Azure portal'ı tıklayın **Active Directory** sekmesi. Ardından yapılandırmak istediğiniz dizine tıklayın.
   
   Unutmayın: tüm yapılandırma dizin düzeyinde yapıldığını için koşullu erişim dizininiz ve Azure RemoteApp, değil bir özelliğidir. Bu, aynı zamanda bu değişiklikleri yapmak için dizin yöneticisi olmanız gerekir anlamına gelir.
2. Tıklatın **uygulamaları**ve ardından **Microsoft Azure RemoteApp** koşullu erişimi ayarlamak için. Her bir "hizmet olarak yazılım" uygulama için koşullu erişim dizininizde ayrı olarak ayarlayabilirsiniz unutmayın.
   ![Azure RemoteApp için koşullu erişimi ayarlama](./media/remoteapp-secureaccess/ra-conditionalaccessscreen.png)
3. Üzerinde **yapılandırma** sekmesinde, ayarlamak **erişim kurallarını etkinleştirme** açık.
   ![Azure RemoteApp için erişim kurallarını etkinleştirin](./media/remoteapp-secureaccess/ra-enableaccessrules.png)
4. Şimdi, çeşitli kurallarını yapılandırın ve bunları uygulamak seçen:
   
   1. Seçin **iş olduğunda değil, erişimi engelleme** tamamen kullanıcıların Azure RemoteApp, belirttiğiniz ağ ortamının dışında erişimini engellemek için.
   2. "Güvenilen ağınıza." oluşturan IP adresi aralıklarını tanımlamak için aşağıdaki seçeneklerden birini tıklatın Olanlar dışında her şeyi reddedilir.
5. Belirlediğiniz aralığın dışında bir IP adresinden Azure RemoteApp istemci başlatarak yapılandırmanızı sınayın. Azure AD kimlik bilgilerinizle oturum sonra şuna benzer bir ileti görürsünüz:

![Azure RemoteApp reddedilen erişimi](./media/remoteapp-secureaccess/ra-accessdenied.png)

### <a name="future-conditional-access-features"></a>Gelecekteki koşullu erişim özellikleri
Azure Active Directory ekibi, koşullu erişim sürümündeki yeni özellikler üzerinde çalışmaktadır. Yöneticiler yeni tür ağ ötesinde kuralların göre konumuna kuralları oluşturmak mümkün olacaktır. Yeni işlevselliği ortak önizlemesini hemen kullanılabilir olması gerekir.

### <a name="how-to-monitor-access-to-azure-remoteapp"></a>Azure RemoteApp erişimi izlemek nasıl
Azure Active Directory Premium Raporlama işlevini koşullu erişim kullanmak için harika bir özelliktir. Tüm şüpheli etkinlikleri algılamak ve ortamınıza erişen izlemek raporları kullanın.

Örneğin, Azure RemoteApp, yaptıkları işlemin, kaç kez erişilen kullanıcılarının adlarını görebilirsiniz ve ne zaman.

1. Azure portalında tıklatın **Active Directory**ve ardından dizininizi'ı tıklatın.
2. Git **raporları** sekmesi.
3. Raporlar listesinden seçin **uygulama kullanımı** altında **tümleşik uygulamalar**.
   
   Azure RemoteApp için bazı toplu istatistikler görürsünüz. 
   ![Toplanan Azure RemoteApp erişim istatistikleri](./media/remoteapp-secureaccess/ra-accessstats.png)
4. Azure RemoteApp erişen kullanıcılar hakkında bilgi almak için uygulamayı tıklatın.
   ![Azure RemoteApp kullanıcı erişimi istatistikleri](./media/remoteapp-secureaccess/ra-userstats.png)

### <a name="summary"></a>Özet
Azure Active Directory Premium ile Azure RemoteApp (ve diğer yazılım hizmet uygulamaları Azure AD üzerinden kullanılabilir olarak) erişim kuralları ayarlayabilirsiniz. Kuralları ağ konumuna göre ilkeleri şu anda sınırlı ancak kuruluş yönetimi diğer yönlerini gelecekte uzatılır.

Azure AD Premium ayrıca raporlama sunar ve bunların Azure RemoteApp ortamınız üzerinde daha fazla yönetim denetimini genişletme özellikleri izleme sahiptir.

## <a name="how-do-i-make-sure-my-secure-resource-is-accessible-only-from-my-azure-remoteapp-environment"></a>My güvenli bir kaynak yalnızca benim Azure RemoteApp Ortamı'ndan erişilebilen nasıl emin?
Bu makalenin önceki bölümlerde Azure RemoteApp ortamında erişimin güvenliğini sağlama konusunda odaklanır. Biz, erişim izni verilen kullanıcıları seçme ve hizmetin nasıl kullanabileceklerini daha fazla denetlemek üzere erişim kurallarını ayarlama elde.

Azure RemoteApp dağıtımlar için yaygın bir senaryo, uzak uygulamalarını örneğin bir SQL veritabanı bir arka uç kaynak ile iletişim kurması gereken ' dir. Bu kaynak barındırılan ya da şirket içi (örneğin bir kurumsal ağ) veya bulutta (örneğin Azure Iaas). Yöneticiler genellikle arka uç kaynak yalnızca Azure RemoteApp dağıtılan uygulamalar ve olmayan örneğin doğrudan bir kullanıcının bilgisayarı üzerinde çalışan ve ortak Internet üzerinden erişen bir uygulama tarafından erişilebildiğinden emin olmak istersiniz. Azure RemoteApp çok merkezi olarak yönetilen ve güvenli bir ortam ve böylece kullanıcılar ile arka uç kaynak etkileşim kuracağını tek bir yolu olarak görülür.

Azure RemoteApp ortamında ve güvenli bir kaynak aynı Azure sanal ağ (VNET içinde) yerleştirmek için çözümüdür. Kaynak farklı bir site ise, örneğin Azure veri merkezi ile müşterinin şirket içi ortamına yayılan bir VNet oluşturmak bir siteden siteye VPN bağlantısı kurabilirsiniz.

Azure RemoteApp koleksiyonu dağıtımları kendi VNET burada sağlayabilir iki türlerini destekler:

* Olmayan etki alanına katılmış: uygulamaları "görüş", diğer kaynakları AĞDA sahip olur. Örneğin, bu uygulamalar, SQL kimlik doğrulaması kullanan bir SQL veritabanına bağlanmak için kullanılabilir (uygulamaları veritabanına karşı doğrudan kullanıcı kimlik doğrulaması)
* Etki alanına katılmış: Azure RemoteApp tarafından kullanılan sanal makineleri sanal ağ içindeki bir etki alanı denetleyicisine birleştirilir. Uygulamaları bir arka uç kaynağa erişmek için bir Windows etki alanı denetleyicisine karşı kimlik doğrulaması gerektiğinde kullanışlıdır.
  ![Azure RemoteApp etki alanına katılmış bir koleksiyonda](./media/remoteapp-secureaccess/ra-domainjoined.png)

### <a name="how-to-create-a-secure-connection-between-azure-and-my-on-premises-environment"></a>My içi ortamınız ile Azure arasındaki güvenli bir bağlantı oluşturma
Azure ve şirket içi ortamlarınızın bağlamak için çeşitli yapılandırma seçenekleri vardır. Seçenekleri iyi bir genel bakış burada kullanılabilir.

Azure RemoteApp ile koleksiyonunuzu oluşturma işlemi sırasında kullanın ve ağınızı ilk yapılandırmanız gerekir. 

## <a name="the-complete-solution"></a>Eksiksiz çözümü
Aşağıdaki diyagram, burada güvenli erişim kanal üzerinden Azure RemoteApp (ARA), son kullanıcının arka uç kaynağını oluşturduğumuz eksiksiz çözüm gösterir.
![Azure RemoteApp güvenli](./media/remoteapp-secureaccess/ra-secureoverview.png) aşama Seçili kullanıcıları ve ARA nasıl erişilebileceğini yöneten erişim kuralları oluşturulan 1. Aşağıdaki örnekte yalnızca erişim ve şirket ağından çalışan kullanıcılar için izin veriyoruz. Uyumlu olmayan kullanıcıları ARA ortamı hiç erişebilir olmaz.
Aşama 2'de biz arka uç kaynak biz denetleyen VNet/VPN yapılandırma yoluyla kullanıma sunulan. Azure RemoteApp aynı Vnet'i yerleştirildi. Sonuç kaynak yalnızca ARA ortamı üzerinden erişilebilir olduğunu.

