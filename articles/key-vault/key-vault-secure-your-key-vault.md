---
title: "anahtarınızı aaaSecure kasa | Microsoft Docs"
description: "Kasaları ve anahtarlar ile parolaları yönetmek için anahtar kasasına yönelik erişim izinlerini yönetin. Anahtar kasası ve nasıl toosecure anahtarınızı kasa için kimlik doğrulama ve yetkilendirme modeli"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: e5b4e083-4a39-4410-8e3a-2832ad6db405
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: 84f5fc18142a1ad89babbd11f4f65eca105afc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-key-vault"></a>Anahtar kasanızın güvenliğini sağlama
Azure Anahtar Kasası, bulut uygulamalarınıza ait şifreleme anahtarlarını ve parolaları (sertifikalar, bağlantı dizeleri, parolalar gibi) koruyan bir bulut hizmetidir. Bu veri duyarlı ve kritik iş olduğundan, böylece uygulamalar yalnızca yetkili toosecure erişim tooyour anahtar kasalarını istediğiniz ve anahtar kasası erişebilir. Bu makalede anahtar kasası erişim modeline genel bakış sağlar, kimlik doğrulama ve yetkilendirme açıklar ve nasıl toosecure erişim tookey kasa örneği ile bulut uygulamalarınız için açıklar.

## <a name="overview"></a>Genel Bakış
Erişim tooa anahtar kasası, iki ayrı arabirimleri aracılığıyla denetlenir: Yönetim düzlemi ve veri düzlemi. Her iki düzlemleri için uygun kimlik doğrulama ve yetkilendirme gereklidir (bir kullanıcı ya da uygulama) çağıran erişim tookey kasası sağlayabilmek için önce. Yetkilendirme hangi işlemleri hello arayan tooperform izin belirlerken kimlik doğrulaması hello arayanın hello kimliği oluşturur.

Kimlik doğrulaması için yönetim düzlemi ve veri düzleminde Azure Active Directory kullanılır. Yetkilendirme için yönetim düzleminde rol tabanlı erişim denetimi (RBAC), veri düzleminde ise anahtar kasası erişim ilkesi kullanılır.

Kapsanan hello konular kısa bir genel bakış şöyledir:

[Azure Active Directory'yi kullanarak kimlik doğrulaması](#authentication-using-azure-active-directory) -Bu bölümde çağıran ile Azure Active Directory tooaccess bir anahtar kasası yönetim düzlemi ve veri düzlemi aracılığıyla nasıl gerçekleştireceğini açıklar. 

[Yönetim düzlemi ve veri düzlemi](#management-plane-and-data-plane) - Yönetim düzlemi ve veri düzlemi, anahtar kasanıza erişmek için kullanılan iki erişim düzlemidir. Her erişim düzlemi belirli işlemleri destekler. Bu bölümde hello erişim uç noktalar açıklanmaktadır, işlemleri desteklenen ve denetim yöntemi her düzlem tarafından kullanılan erişim. 

[Yönetim düzlemi erişim denetimi](#management-plane-access-control) - biz Ara rol tabanlı erişim denetimi kullanarak toomanagement düzlemi işlemleri erişimine bu bölümdeki.

[Veri düzlemi erişim denetimi](#data-plane-access-control) -toouse anahtar kasası erişim ilkesi toocontrol veri erişimi nasıl düzlemine Bu bölümde açıklanmaktadır.

[Örnek](#example) -Bu örnek nasıl toosetup erişim denetimi, anahtar kasası tooallow üç farklı ekipler için (güvenlik ekibi, geliştiricilerin/işleçler ve denetçiler) açıklar tooperform belirli görevleri toodevelop, yönetme ve azure'da bir uygulamayı izleme .

## <a name="authentication-using-azure-active-directory"></a>Azure Active Directory'yi kullanarak kimlik doğrulama
Bir Azure aboneliği bir anahtar kasası oluşturduğunuzda, hello aboneliğinin Azure Active Directory Kiracı ile otomatik olarak ilişkilendirilir. (Kullanıcılar ve uygulamalar) tüm arayanlar olmalıdır bu Kiracı tooaccess bu anahtar kasasında kayıtlı. Bir uygulama veya bir kullanıcı Azure Active Directory tooaccess anahtar kasası ile kimlik doğrulaması gerekir. Bu tooboth yönetim düzlemi ve veri düzlemi geçerlidir erişim. Her iki durumda da bir uygulama, anahtar kasasına iki şekilde erişebilir:

* **kullanıcı+uygulama erişimi** - bu seçenek genellikle oturum açmış bir kullanıcı adına anahtar kasasına erişen uygulamalar için geçerlidir. Azure PowerShell ve Azure Portalı bu tür erişimin örneğidir. Toogrant erişim toousers iki yolu vardır: herhangi bir uygulamadan anahtar kasası erişebilmeleri toogrant erişim toousers tek yönlü ve hello başka bir yolla toogrant bir kullanıcı erişimi tookey kasası yalnızca belirli bir uygulama (başvurulan tooas bileşik kimlik) kullandığınızda. 
* **yalnızca uygulama erişim** - arka plan programı hizmetlerini çalıştırmak, vs. hello uygulamanın kimlik verilir arka plan işleri toohello erişim uygulamaları anahtar kasası için.

Her iki tür uygulamalarda Merhaba uygulaması Azure hello birini kullanarak Active Directory'e ile kimlik doğrulaması [desteklenen kimlik doğrulama yöntemlerini](../active-directory/active-directory-authentication-scenarios.md) ve bir belirteç alır. Kullanılan kimlik doğrulama yöntemi hello uygulama türüne bağlıdır. Ardından Merhaba uygulaması bu belirtecini kullanır ve REST API'si isteği tookey kasası gönderir. Yönetim düzlemi erişim hello durumunda istekleri Azure Resource Manager uç noktası aracılığıyla yönlendirilir. Veri düzlemi erişirken hello uygulamaları ettiği doğrudan tooa anahtar kasası uç noktası. Merhaba hakkında daha fazla ayrıntı görmek [tüm kimlik doğrulama akışı](../active-directory/active-directory-protocols-oauth-code.md). 

kendisi için bir belirteç hello uygulama isteklerini hello kaynak adı Merhaba uygulaması Yönetim düzeyi veya veri düzlemi erişme bağlı olarak farklı değildir. Bu nedenle hello kaynak adı hello Azure ortamı bağlı olarak daha sonraki bir bölüme hello tabloda açıklandığı ya da Yönetim düzlemi veya veri düzlemi uç noktadır.

Kimlik doğrulama tooboth için tek bir mekanizma sahip yönetimi ve veri düzlemi kendi faydası vardır:

* Kuruluşlar merkezi olarak erişim tooall anahtar kasalarını kuruluşlarındaki kontrol edebilirsiniz
* Bir kullanıcı ayrılsa bunlar hemen tooall anahtar kasalarını hello kuruluşunuzdaki erişimi kaybetmek
* Kuruluşlar hello seçenekleri Azure Active Directory'de (örneğin, etkinleştirme çok faktörlü kimlik doğrulaması ek güvenlik için) üzerinden kimlik doğrulaması özelleştirebilirsiniz

## <a name="management-plane-and-data-plane"></a>Yönetim düzlemi ve veri düzlemi
Azure Anahtar Kasası, Azure Resource Manager dağıtım modeli üzerinden kullanılabilen bir Azure hizmetidir. Bir anahtar kasası oluşturduğunuzda, içinde anahtar, parola ve sertifika gibi diğer nesneleri oluşturabileceğiniz sanal bir kapsayıcı elde edersiniz. Daha sonra Yönetim düzlemi ve veri düzlemi tooperform belirli işlemlerini kullanarak, anahtar kasanızı erişin. Yönetim düzlemi anahtarınızı kasa oluşturma, silme, anahtar kasası özniteliklerini güncelleştirmeyi ve veri düzlemi için erişim ilkeleri ayarlamak gibi kendisini kullanılan toomanage arabirimidir. Veri düzlemi arabirimidir kullanılan tooadd, silme, değiştirebilirsiniz ve hello anahtarları, gizli anahtarları ve anahtar kasasında depolanan sertifikalar kullanabilirsiniz.

Merhaba yönetim düzlemi ve veri düzlemi arabirimleri (tabloya bakın) farklı uç noktaları erişilir. Merhaba tabloda Hello ikinci sütun Bu uç noktalar farklı Azure ortamlarda hello DNS adlarını açıklar. Merhaba üçüncü sütun her erişim düzlemi gerçekleştirebileceğiniz hello işlemler açıklanmaktadır. Her erişim düzlemi kendi erişim denetimi mekanizmasına sahiptir: yönetim düzlemi için erişim denetimi Azure Resource Manager Rol Tabanlı Access Control (RBAC) kullanılarak ayarlanırken veri düzlemi erişim denetimi, anahtar kasası erişim ilkesi kullanılarak ayarlanır.

| Erişim düzlemi | Erişim uç noktaları | İşlemler | Erişim denetimi mekanizması |
| --- | --- | --- | --- |
| Yönetim düzlemi |**Genel:**<br> management.azure.com:443<br><br> **Azure Çin:**<br> management.chinacloudapi.cn:443<br><br> **Azure ABD:**<br> management.usgovcloudapi.net:443<br><br> **Azure Almanya:**<br> management.microsoftazure.de:443 |Anahtar kasası oluşturma/okuma/güncelleştirme/silme <br> Anahtar kasası için erişim ilkelerini ayarlama<br>Anahtar kasası etiketlerini ayarlama |Azure Resource Manager Rol Tabanlı Access Control (RBAC) |
| Veri düzlemi |**Genel:**<br> &lt;vault-name&gt;.vault.azure.net:443<br><br> **Azure Çin:**<br> &lt;vault-name&gt;.vault.azure.cn:443<br><br> **Azure ABD:**<br> &lt;vault-name&gt;.vault.usgovcloudapi.net:443<br><br> **Azure Almanya:**<br> &lt;vault-name&gt;.vault.microsoftazure.de:443 |Anahtarlar için: Şifre Çöz, Şifrele, UnwrapKey, WrapKey, Doğrula, İmzala, Al, Listele, Güncelleştir, Oluştur, İçeri Aktar, Sil, Yedekle, Geri Yükle<br><br> Parolalar için: Al, Listele, Ayarla, Sil |Anahtar kasası erişim ilkesi |

Merhaba yönetim düzlemi ve veri düzlemi erişim denetimleri bağımsız olarak çalışır. Örneğin, bir uygulama erişim toouse anahtarları bir anahtar Kasası'toogrant istiyorsanız anahtar kasası erişim ilkelerini kullanarak toogrant veri düzlemi erişim izinlerini yeterlidir ve yönetim düzlemi erişim yok, bu uygulama için gereklidir. Ve buna karşılık, bir kullanıcı toobe mümkün istiyorsanız tooread özellikleri ve etiketleri kasa, ancak herhangi bir erişim tookeys, gizli veya sertifika yüklü değil, bu kullanıcı verebilirsiniz, 'read' erişim RBAC ve hiçbir erişim toodata düzlemi kullanarak gereklidir.

## <a name="management-plane-access-control"></a>Yönetim düzlemi erişim denetimi
Merhaba Yönetim düzeyi, anahtar kasası hello kendisini etkileyen işlemden oluşur. Örneğin, bir anahtar kasası oluşturabilir veya silebilirsiniz. Bir abonelikteki kasaların listesini alabilirsiniz. Anahtar kasası özellikleri (örneğin, SKU, etiketleri) alabilir ve anahtar kasası hello kullanıcıları ve anahtarları ve gizli anahtarları hello anahtar kasasında erişebileceği uygulamaları Denetim erişim ilkeleri ayarlayabilirsiniz. Yönetim düzlemi erişim denetimi, RBAC kullanır. Önceki bölümde içinde hello tablosundaki Yönetim düzeyi aracılığıyla gerçekleştirilebilir anahtar kasası işlemleri Hello tam listesine bakın. 

### <a name="role-based-access-control-rbac"></a>Rol Tabanlı Access Control (RBAC)
Her Azure aboneliği bir Azure Active Directory’ye sahiptir. Kullanıcılar, gruplar ve uygulamalar bu dizinden erişim toomanage hello Azure Resource Manager dağıtım modeli kullanmanız hello Azure aboneliği kaynaklarında verilebilir. Bu erişim denetimi başvurulan tooas rol tabanlı erişim denetimi (RBAC) türüdür. toomanage bu erişimi, hello kullanabilirsiniz [Azure portal](https://portal.azure.com/), hello [Azure CLI araçlarını](../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), veya hello [Azure Resource Manager REST API'leri](https://msdn.microsoft.com/library/azure/dn906885.aspx).

Hello Azure Resource Manager modeli ile Azure Active Directory kullanarak bir kaynak grubu ve Denetim erişim toohello Yönetim düzeyi bu anahtar kasasının içinde anahtar kasanızı oluşturun. Örneğin, kullanıcı veya grup bir özelliği toomanage anahtar kasalarını belirli bir kaynak grubunda verebilirsiniz.

Uygun RBAC rolü atama tarafından erişim toousers, gruplar ve uygulamalar belirli bir kapsamda verebilirsiniz. Örneğin, toogrant erişim tooa kullanıcı toomanage anahtar kasalarını toothis kullanıcı belirli bir kapsamda bir önceden tanımlanmış role 'anahtar kasası katkıda bulunan' atamanız gerekir. Merhaba kapsamı, bir abonelik, bir kaynak grubu ya da yalnızca belirli bir anahtar kasası bu durumda olacaktır. Abonelik düzeyinde atanan bir rol tooall kaynak grupları ve bu abonelik içindeki kaynaklara uygulanır. Kaynak grubu düzeyinde atanan bir rol tooall kaynakların kaynak grubunda geçerlidir. Belirli bir kaynak için atanmış bir rolü yalnızca toothat kaynak geçerlidir. Birçok önceden tanımlanmış roller vardır (bkz [RBAC: yerleşik roller](../active-directory/role-based-access-built-in-roles.md)), ve hello rolleri önceden tanımlanmış durumunda değil sığacak gereksinimlerinizi kendi rolleri de tanımlayabilirsiniz.

> [!IMPORTANT]
> Bir kullanıcıya katkıda bulunan izinleri (RBAC) tooa anahtar kasası Yönetim düzeyi varsa, bunları kendisini erişim toodata düzlemi erişim toodata düzlemi denetimleri anahtar kasası erişim ilkesi ayarlayarak verebileceği unutmayın. Bu nedenle, 'erişim tooyour anahtar kasalarını tooensure yalnızca yetkili kişiler erişmek ve anahtar kasalarını, anahtarları, gizli ve sertifikaları yönetmek katkıda bulunan' olan tootightly denetim önerilir.
> 
> 

## <a name="data-plane-access-control"></a>Veri düzlemi erişim denetimi
Sertifikalar, parolaları ve anahtarlar gibi bir anahtar kasası hello nesneleri etkileyen işlemler Hello anahtar kasası veri düzlemi oluşur.  Buna anahtar oluşturma, içeri aktarma, güncelleştirme, listeleme, yedekleme ve geri yükleme gibi anahtar işlemleri, anahtar etiketlerini ve diğer özniteliklerini imzalama, doğrulama, şifreleme, şifresini çözme, sarmalama, sarmalamadan çıkarma ve ayarlama gibi şifreleme işlemleri dahildir. Benzer şekilde, parolalar için alma, ayarlama, listeleme ve silme işlemleri dahildir.

Veri düzlemi erişimi, bir anahtar kasasına ilişkin erişim ilkeleri ayarlanarak verilir. Bir kullanıcı, Grup veya uygulama Yönetim düzeyi, anahtar kasası için bir anahtar kasası toobe mümkün tooset erişim ilkeleri için (RBAC) katkıda bulunan izinleri olmalıdır. Bir kullanıcı, Grup veya uygulama için bir anahtar veya gizli bir anahtar kasasına erişim tooperform belirli işlemler verilebilir. Bir anahtar kasası için too16 erişim ilkesi girişleri anahtar kasası desteği. Bir Azure Active Directory güvenlik grubu oluşturun ve kullanıcıların toothat Grup toogrant veri düzlemi erişim tooseveral kullanıcılar tooa anahtar kasası ekleyin.

### <a name="key-vault-access-policies"></a>Key Vault Erişim İlkeleri
Anahtar kasası erişim ilkelerini izinleri tookeys, parolaları ve sertifikaları ayrı olarak verin. Örneğin, bir kullanıcı erişimi tooonly anahtarları, ancak gizli izin verebilirsiniz. Ancak, izinleri tooaccess anahtar veya gizli veya sertifika hello kasası düzeyindedir. Diğer bir deyişle, anahtar kasası erişim ilkesi nesne düzeyinde izinleri desteklemez. Kullanabileceğiniz [Azure portal](https://portal.azure.com/), hello [Azure CLI araçlarını](../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), veya hello [anahtar kasası Yönetimi REST API'lerine](https://msdn.microsoft.com/library/azure/mt620024.aspx) tooset erişim ilkeleri bir anahtar kasası için.

> [!IMPORTANT]
> Anahtar kasası erişim ilkelerini hello kasası düzeyinde geçerli olduğunu unutmayın. Örneğin, kullanıcı izni toocreate ve delete tuşlarına verildiğinde aynen bu anahtar kasasında tüm anahtarları üzerinde bu işlemler gerçekleştirebilirsiniz.
> 
> 

## <a name="example"></a>Örnek
SSL için sertifika, verileri depolamak için Azure depolama ve imzalama işlemleri için RSA 2048 bit anahtarı kullanan bir uygulama geliştirdiğinizi varsayalım. Bu uygulamanın bir VM (veya VM Ölçek Kümesi) içinde çalıştığını kabul edelim. Tüm uygulama parolaları ve Azure Active Directory ile Merhaba uygulama tooauthenticate tarafından kullanılan kullanım anahtar kasası toostore hello önyükleme sertifikası hello bir anahtar kasası toostore kullanabilirsiniz.

Bu nedenle, bir anahtar kasasında depolanan tüm hello anahtarları ve gizli anahtarları toobe özetini İşte.

* **SSL Sertifikası** - SSL için kullanılır
* **Depolama anahtarı** -tooget erişim tooStorage hesabı
* **RSA 2048 bit anahtarı** - imzalama işlemleri için kullanılır
* **Önyükleme sertifika** -kullanılan tooauthenticate tooAzure Active Directory, tooget erişim tookey kasa toofetch hello depolama anahtarı ve hello RSA anahtarı kullan imzalamak için.

Şimdi yönetme, dağıtma ve bu uygulama denetimi hello kişiler şirketinizdeki karşılamak. Bu örnekte üç rol kullanılacaktır.

* **Güvenlik ekibine** - bunlar genellikle hello 'office' hello CSO (baş güvenlik yetkilisi), BT personelinden olup veya eşdeğeri, sorumlu gizli dizilerin uygun yerleriniz gibi hello SSL sertifikaları, bağlantı dizeleri için imzalama için kullanılan RSA anahtarları veritabanları, depolama hesabı anahtarları.
* **Geliştiriciler/işleçleri** -bu uygulama geliştirme ve Azure'da dağıtmak hello terimleri bunlar. Genellikle, bunlar hello güvenlik ekibi, bir parçası değildir ve bu nedenle bunlar erişim tooany benzeri gizli verilerin SSL sertifikalarını, RSA anahtarları olmaması gereken ancak bunlar dağıtmak hello uygulama erişim toothose olması gerekir.
* **Denetçiler** -bu genellikle farklı hello geliştiricileri ve genel BT personeli yalıtılmış kişiler kümesidir. Sorumluluğu tooreview düzgün kullanımını ve sertifikalar, anahtarları, vb. Bakım ve veri güvenliği standartları ile uyum sağlamak. 

Bu uygulama, ancak belirtilen ilgili burada toobe dış hello kapsamı olan ve hello abonelik (veya kaynak grubu) olacak bir daha fazla role yönetici. Abonelik Yöneticisi hello güvenlik ekibine ilk erişim izinlerini ayarlar. Burada bu hello Abonelik Yöneticisi erişim toohello güvenlik takım tooa kaynak grubunun tüm bu uygulama reside için gerekli kaynakları hello verildi varsayalım.

Artık her rol hello bu uygulama bağlamında gerçekleştirir hangi eylemleri görelim.

* **Güvenlik ekibi**
  * Anahtar kasaları oluşturma
  * Anahtar kasası günlüğünü açma
  * Anahtar/parola ekleme
  * Olağanüstü durum kurtarma için anahtarların yedeğini oluşturma
  * Anahtar kasası erişim ilkesi toogrant izinleri toousers ve uygulamaları tooperform belirli ayarlama işlemleri
  * Anahtarları/parolaları düzenli aralıklarla alma
* **Geliştiriciler/operatörler**
  * Başvuruları toobootstrap ve SSL sertifikaları (parmak izleri), depolama anahtarı (gizli URI) ve imzalama anahtarı (anahtar URI) Güvenlik ekibinden alın
  * Anahtarlara ve parolalara programlı olarak erişen uygulamayı geliştirme ve dağıtma
* **Denetçiler**
  * Kullanım günlükleri tooconfirm düzgün anahtarı/parola kullanımını ve veri güvenliği standartları ile uyum gözden geçirin

Şimdi ne erişim izinleri tookey kasası her rol (ve hello uygulama) tarafından gerekli görelim tooperform kendilerine atanan görevleri. 

| Kullanıcı Rolü | Yönetim düzlemi izinleri | Veri düzlemi izinleri |
| --- | --- | --- |
| Güvenlik Ekibi |anahtar kasasına Katkıda Bulunan |Anahtarlar: yedekleme, oluşturma, silme, alma, içeri aktarma, listeleme, geri yükleme <br> Parolalar: tümü |
| Geliştiriciler/Operatörler |anahtar kasası dağıtmadan izni bunlar dağıtmak hello VM'ler gizli hello anahtar Kasası'nı getirebilirsiniz |None |
| Denetçiler |None |Anahtarlar: listeleme<br>Parolalar: listeleme |
| Uygulama |None |Anahtarlar: imzalama<br>Parolalar: imzalama |

> [!NOTE]
> Denetçiler anahtarları ve etiketler gibi hello günlüklerde gösterilen değil gizli anahtarları için öznitelikler inceleyebilirsiniz şekilde anahtarları ve gizli anahtarları için izin listesinde etkinleştirme ve sona erme tarihleri.
> 
> 

İzni tookey kasası yanı sıra, tüm üç rolleri de tooother kaynaklarına erişim. Örneğin, toobe mümkün toodeploy VM'ler (veya Web Apps vs.) Geliştiriciler/işleçleri 'Katılımcısı' erişim toothose kaynak türleri de gerekir. Denetçiler hello anahtar kasası günlükleri depolandığı okuma erişimi toohello depolama hesabınızın olması gerekir.

Bu makalenin Hello odak erişim tooyour anahtar kasası getirilmesidir olduğundan, biz yalnızca toothis konu ilgili hello ilgili bölümleri göstermek ve sertifikaları dağıtmak, anahtarları ve gizli anahtarları program aracılığıyla vb. erişimi ile ilgili Ayrıntıları atla. Bu ayrıntıları başka bölümlerde zaten ele alınmaktadır. Anahtar kasası tooVMs depolanan sertifikalarını dağıtma kapsanan olarak bir [blog gönderisi](https://blogs.technet.microsoft.com/kv/2016/09/14/updated-deploy-certificates-to-vms-from-customer-managed-key-vault/)ve [örnek koduna](https://www.microsoft.com/download/details.aspx?id=45343) kullanılabilir, nasıl toouse önyükleme sertifika tooauthenticate tooAzure AD tooget gösterir erişim tookey kasası.

Azure portalını kullanarak hello erişim izinleri çoğunu verilebilir, ancak sonuç toogrant ayrıntılı izinler toouse Azure PowerShell (veya Azure CLI) tooachieve hello gerekebilir istenen. 

PowerShell parçacıkları aşağıdaki hello varsayın:

* Hello Azure Active Directory Yöneticisi hello üç rolleri, yani Contoso güvenlik ekibi, Contoso uygulaması Devops, Contoso uygulaması denetçiler temsil eden güvenlik gruplarını oluşturdu. Hello Yöneticisi ait oldukları toohello gruplara da ekledi.
* **ContosoAppRG** hello kaynak tüm hello kaynakların bulunduğu grubudur. **contosologstorage** hello günlüklerinin depolandığı değil. 
* Anahtar kasası **ContosoKeyVault** ve anahtar kasası günlükleri için kullanılan depolama hesabı **contosologstorage** hello olmalıdır aynı Azure konumu

İlk hello Abonelik Yöneticisi, 'anahtar kasası katkıda bulunan' ve ' kullanıcı erişimi Yöneticisi ' rolleri toohello güvenlik ekibine atar. Bu hello güvenlik takım toomanage tooother kaynaklara erişmesine izin verir ve hello kaynak grubunda ContosoAppRG anahtar kasalarını yönetme.

```
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -RoleDefinitionName "key vault Contributor" -ResourceGroupName ContosoAppRG
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -RoleDefinitionName "User Access Administrator" -ResourceGroupName ContosoAppRG
```

Merhaba aşağıdaki betik nasıl hello güvenlik ekibine bir anahtar kasası oluşturabilir, günlüğü kurulumu ve diğer rolleri ve hello uygulama için erişim izinlerini ayarlayın gösterilmektedir. 

```
# Create key vault and enable logging
$sa = Get-AzureRmStorageAccount -ResourceGroup ContosoAppRG -Name contosologstorage
$kv = New-AzureRmKeyVault -VaultName ContosoKeyVault -ResourceGroup ContosoAppRG -SKU premium -Location 'westus' -EnabledForDeployment
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

# Data plane permissions for Security team
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoKeyVault -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -PermissionsToKeys backup,create,delete,get,import,list,restore -PermissionsToSecrets all

# Management plane permissions for Dev/ops
# Create a new role from an existing role
$devopsrole = Get-AzureRmRoleDefinition -Name "Virtual Machine Contributor"
$devopsrole.Id = $null
$devopsrole.Name = "Contoso App Devops"
$devopsrole.Description = "Can deploy VMs that need secrets from key vault"
$devopsrole.AssignableScopes = @("/subscriptions/<SUBSCRIPTION-GUID>")

# Add permission for dev/ops so they can deploy VMs that have secrets deployed from key vaults
$devopsrole.Actions.Add("Microsoft.KeyVault/vaults/deploy/action")
New-AzureRmRoleDefinition -Role $devopsrole

# Assign this newly defined role tooDev ops security group
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso App Devops')[0].Id -RoleDefinitionName "Contoso App Devops" -ResourceGroupName ContosoAppRG

# Data plane permissions for Auditors
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoKeyVault -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso App Auditors')[0].Id -PermissionsToKeys list -PermissionsToSecrets list
```

Merhaba özel rol tanımlı, yalnızca atanabilir toohello abonelik hello ContosoAppRG kaynak grubunun oluşturulduğu. Merhaba aynı özel roller diğer projeler diğer abonelikler için kullanılacaksa, buna ait kapsam eklenen daha fazla abonelik olabilir.

Merhaba özel rol ataması hello geliştiriciler/işleçleri hello "dağıtmak/eylem" izni için kapsamlı toohello kaynak grubudur. Bu şekilde yalnızca hello VM'ler 'ContosoAppRG' hello gizli (SSL sertifikası ve önyükleme cert) alacak hello kaynak grubunda oluşturuldu. Farklı bir kaynak grubunda dev/ops ekibinin bir üyesi oluşturur herhangi bir VM hello gizli URI'ler biliyorsa bile mümkün tooget bu Sırları olmaz.

Bu örnekte basit bir senaryo gösterilmektedir. Gerçek Hayatta senaryoları daha karmaşık olabilir ve tooadjust izinleri tooyour anahtar kasası gereksinimlerinize göre gerekebilir. Örneğin, Bizim örneğimizde, bu güvenlik ekibi, geliştiricilerin/işleçleri takım gerek tooreference kendi uygulamalarında hello anahtarı ve gizli başvurular (URI'ler ve parmak izleri) sağlayacak varsayıyoruz. Bu nedenle, bunlar herhangi bir veri düzlemi erişim toogrant geliştiriciler/işleçleri gerekmez. Ayrıca, bu örnekte anahtar kasanızın güvenliğini sağlama konusuna odaklanılmıştır. Benzer göz önünde bulundurarak toosecure verilen [Vm'leriniz](https://azure.microsoft.com/services/virtual-machines/security/), [depolama hesapları](../storage/common/storage-security-guide.md) ve diğer Azure kaynaklarına çok.

> [!NOTE]
> Not: Bu örnekte, üretim sırasında anahtar kasası erişiminin nasıl kilitleneceği gösterilmektedir. Merhaba geliştiricilerin kendi abonelik veya kaynak grubu, tam izinleri toomanage kendi kasa, sanal makineleri ve depolama hesabı nerede bunlar hello uygulama geliştirmek sahip oldukları olması gerekir.
> 
> 

## <a name="resources"></a>Kaynaklar
* [Azure Active Directory Rol Tabanlı Erişim Denetimi](../active-directory/role-based-access-control-configure.md)
  
  Bu makalede hello açıklanmaktadır Azure Active Directory rol tabanlı erişim denetimi ve nasıl çalışır.
* [RBAC: Yerleşik Roller](../active-directory/role-based-access-built-in-roles.md)
  
  Bu makale ayrıntıları tüm kullanılabilir RBAC yerleşik rolleri hello.
* [Resource Manager dağıtımını ve klasik dağıtımı anlama](../azure-resource-manager/resource-manager-deployment-model.md)
  
  Bu makalede hello Resource Manager dağıtımını ve klasik dağıtım modellerine açıklanmakta ve hello Resource Manager ve kaynak grupları kullanmanın yararları hello açıklanmaktadır
* [Rol Tabanlı Erişim Denetimini Azure PowerShell ile Yönetme](../active-directory/role-based-access-control-manage-access-powershell.md)
  
  Bu makalede, nasıl toomanage rol tabanlı erişim denetimini Azure PowerShell ile açıklanmaktadır.
* [Rol tabanlı erişim denetimini hello REST API ile yönetme](../active-directory/role-based-access-control-manage-access-rest.md)
  
  Bu makalede nasıl toouse hello REST API toomanage RBAC gösterilmektedir.
* [Ignite’tan Microsoft Azure için Rol Tabanlı Erişim Denetimi](https://channel9.msdn.com/events/Ignite/2015/BRK2707)
  
  Bağlantı tooa hello 2015 MS Ignite Konferanstan Channel 9 video budur. Bu oturumda, bunlar hakkında konuşun erişim yönetimi ve Azure raporlama özellikleri ve tooAzure abonelikleri Azure Active Directory'yi kullanarak erişimi güvenli hale getirme geçici en iyi yöntemler keşfedin.
* [OAuth 2.0 ile Azure Active Directory kullanarak erişim tooweb uygulamaları yetkilendirmek](../active-directory/active-directory-protocols-oauth-code.md)
  
  Bu makalede Azure Active Directory ile kimlik doğrulaması için tam OAuth 2.0 akışı açıklanmaktadır.
* [anahtar kasası Yönetim REST API’leri](https://msdn.microsoft.com/library/azure/mt620024.aspx)
  
  Bu belge, anahtar kasası erişim ilkesi ayarı dahil olmak üzere, anahtarınızı programlı olarak kasa hello REST API'leri toomanage hello başvurudur.
* [anahtar kasası REST API’leri](https://msdn.microsoft.com/library/azure/dn903609.aspx)
  
  Bağlantı tookey kasası REST API başvuru belgeleri.
* [Anahtar erişim denetimi](https://msdn.microsoft.com/library/azure/dn903623.aspx#BKMK_KeyAccessControl)
  
  Bağlantı tooSecret erişim denetimi başvuru belgeleri.
* [Gizli anahtar erişim denetimi](https://msdn.microsoft.com/library/azure/dn903623.aspx#BKMK_SecretAccessControl)
  
  Bağlantı tooKey erişim denetimi başvuru belgeleri.
* PowerShell kullanarak anahtar kasası erişimini [ayarlama](https://msdn.microsoft.com/library/mt603625.aspx) ve [kaldırma](https://msdn.microsoft.com/library/mt619427.aspx)
  
  PowerShell cmdlet'leri toomanage anahtar kasası erişim ilkesi için bağlantılar tooreference belgeleri.

## <a name="next-steps"></a>Sonraki Adımlar
Bir yöneticiye yönelik başlama öğreticisi için bkz. [Azure anahtar kasası ile çalışmaya başlama](key-vault-get-started.md).

Anahtar Kasası'na yönelik kullanım günlüğü hakkında daha fazla bilgi için bkz. [Azure anahtar kasası günlüğü](key-vault-logging.md).

Azure anahtar kasası ile anahtarları ve gizli anahtarları kullanma hakkında daha fazla bilgi için bkz. [Anahtarlar ve Gizli Anahtarlar Hakkında](https://msdn.microsoft.com/library/azure/dn903623.aspx).

Anahtar kasası hakkında sorularınız varsa, hello ziyaret [Azure anahtar kasası forumları](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault)

