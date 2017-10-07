---
title: "Data Lake Store'da güvenlik aaaOverview | Microsoft Docs"
description: "Azure Data Lake Store daha güvenli bir büyük veri deposu nasıl özellikleri anlama"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ebd5b2ac-c5cc-46d4-9cfd-1a1ee70024c2
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 69e20bd046a9427202074baf59bff13f5b6a83ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="security-in-azure-data-lake-store"></a>Azure Data Lake Store'da güvenlik
Çoğu kurum iş Öngörüler toohelp kararları akıllı yapmak için büyük veri analizi avantajlarından sürüyor. Bir kuruluşun farklı kullanıcılar artan sayıda ile karmaşık ve düzenlenen bir ortam olabilir. Kritik iş verilerini hello doğru tooindividual kullanıcılara verilen erişim düzeyini ile daha güvenli bir şekilde saklandığından emin bir kurumsal toomake önemlidir. Azure Data Lake Store tasarlanmıştır toohelp bu güvenlik gereksinimlerini karşılayacak. Bu makalede, Data Lake Store, hello güvenlik özellikleri hakkında bilgi edinmek dahil olmak üzere:

* Kimlik Doğrulaması
* Yetkilendirme
* Ağ yalıtımı
* Veri koruma
* Denetim

## <a name="authentication-and-identity-management"></a>Kimlik doğrulama ve Kimlik Yönetimi
Kimlik doğrulama hello kullanıcı tooData Lake Store bağlanan herhangi bir hizmeti veya Data Lake Store ile etkileşim zaman, bir kullanıcının kimliği doğrulanır hello işlemidir. Kimlik Yönetimi ve kimlik doğrulaması için Data Lake Store kullanan [Azure Active Directory](../active-directory/active-directory-whatis.md), kullanıcılar ve gruplar hello yönetimini kolaylaştıran bir kapsamlı kimlik ve erişim yönetimi bulut çözümü.

Her Azure aboneliğinin Azure Active Directory örneği ile ilişkili olabilir. Yalnızca kullanıcılar ve Azure Active Directory hizmetinizi tanımlı hizmet kimlikleri Data Lake Store hesabınızı hello Azure portal, komut satırı araçlarını kullanarak veya hello Azure verileri kullanarak, kuruluşunuz oluşturur istemci uygulamaları aracılığıyla erişebilir Lake Store SDK. Bir merkezi erişim denetimi mekanizması Azure Active Directory'yi kullanarak anahtar avantajları şunlardır:

* Basitleştirilmiş kimlik yaşam döngüsü yönetimi. bir kullanıcı veya hizmet (bir hizmet asıl kimliği) Hello kimliğini hızlı bir şekilde oluşturulur ve yalnızca silme veya hello dizin hello hesabında devre dışı bırakarak hızlı bir şekilde iptal.
* Çok faktörlü kimlik doğrulaması. [Çok faktörlü kimlik doğrulaması](../multi-factor-authentication/multi-factor-authentication.md) kullanıcı oturum açmaları ve işlemleri için ek bir güvenlik katmanı sağlar.
* OAuth veya Openıd gibi standart bir açık protokolü aracılığıyla herhangi bir istemciden kimlik doğrulaması.
* Kurumsal Dizin Hizmetleri ve bulut kimlik sağlayıcıları ile Federasyon.

## <a name="authorization-and-access-control"></a>Yetkilendirme ve erişim denetimi
Merhaba kullanıcı Azure Data Lake Store erişebilmesi için Azure Active Directory kullanıcı kimlik doğrulaması yaptıktan sonra Data Lake Store izinlerini erişimi yetkilendirme kontrol eder. Data Lake Store şekilde aşağıdaki hello hesabı ve veri ilgili etkinlikler için yetkilendirme ayırır:

* [Rol tabanlı erişim denetimi](../active-directory/role-based-access-control-what-is.md) (RBAC) hesap yönetimi için Azure tarafından sağlanan
* POSIX hello deposu veri erişimi için ACL

### <a name="rbac-for-account-management"></a>Hesap yönetimi için RBAC
Dört temel roller Data Lake Store için varsayılan olarak tanımlanır. Merhaba rolleri farklı işlemler hello Azure portal, PowerShell cmdlet'leri ve REST API'leri aracılığıyla Data Lake Store hesabındaki izin verir. Merhaba sahibi ve katkıda bulunan rollerinin yönetim işlevleri, çeşitli hello hesabında gerçekleştirebilirsiniz. Yalnızca veri ile etkileşim hello okuyucu rolü toousers atayabilirsiniz.

![RBAC rolleri](./media/data-lake-store-security-overview/rbac-roles.png "RBAC rolleri")

Hesap yönetimi için rolleri atanmış rağmen bazı roller erişim toodata etkileyeceğini unutmayın. Toouse hello dosya sisteminde bir kullanıcının gerçekleştirebileceği ACL'ler toocontrol erişim toooperations gerekir. Aşağıdaki tablonun hello varsayılan rolleri yönetim haklarını ve veri erişim haklarını hello özetini gösterir.

| Roller | Yönetim hakları | Veri erişim hakları | Açıklama |
| --- | --- | --- | --- |
| Atanmış bir role yok |None |ACL ile yönetilen |Merhaba kullanıcı hello Azure portal ya da Azure PowerShell cmdlet'leri toobrowse Data Lake Store kullanamaz. Merhaba kullanıcı yalnızca komut satırı araçlarını kullanabilirsiniz. |
| Sahip |Tümü |Tümü |Merhaba sahibinin bir süper kullanıcı rolüdür. Bu rolü her şeyi yönetebilir ve tam erişim toodata sahip. |
| Okuyucu |Salt okunur |ACL ile yönetilen |Merhaba okuyucu rolüne her şeyi toowhich rol atanmış kullanıcı gibi hesap yönetimi ile ilgili görüntüleyebilirsiniz. Merhaba okuyucu rolüne değişiklik yapamazsınız. |
| Katılımcı |Tüm ekleme ve kaldırma rolleri dışında |ACL ile yönetilen |Merhaba katkıda bulunan rolü dağıtımları ve oluşturma ve Uyarıları yönetme gibi bir hesap, bazı yönlerini yönetebilirsiniz. Merhaba katkıda bulunan rolü ekleme veya rollerini kaldırın. |
| Kullanıcı Erişimi Yöneticisi |Rol Ekleme ve kaldırma |ACL ile yönetilen |Merhaba kullanıcı erişimi yöneticisi rolü, kullanıcı erişim tooaccounts yönetebilirsiniz. |

Yönergeler için bkz: [kullanıcıların veya güvenlik gruplarının tooData Lake Store hesaplarını atayın](data-lake-store-secure-data.md#assign-users-or-security-groups-to-azure-data-lake-store-accounts).

### <a name="using-acls-for-operations-on-file-systems"></a>ACL'leri kullanarak dosya sistemi işlemleri
Data Lake Store olan hiyerarşik dosya sistemi gibi Hadoop dağıtılmış dosya sistemi (HDFS) ve onu destekleyen [POSIX ACL'leri](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_Access_Control_Lists). Okuma (r) denetimleri, yazma (w) ve Yürütme (izinleri tooresources hello sahip rolü, hello sahipleri grup ve diğer kullanıcılar ve gruplar için x). Hello Data Lake Store genel Önizlemesi (Merhaba geçerli sürüm), ACL hello kök klasör, alt klasörler ve dosyaları tek tek etkinleştirilebilir. Data Lake Store bağlanımda ACL’lerin nasıl çalıştığı üzerine daha fazla bilgi için bkz. [Data Lake Store’da erişim denetimi](data-lake-store-access-control.md).

ACL'leri kullanarak birden çok kullanıcı için tanımladığınız öneririz [güvenlik grupları](../active-directory/active-directory-accessmanagement-manage-groups.md). Kullanıcılar tooa güvenlik grubunu ekleyin ve bir dosya veya klasör toothat güvenlik grubu için hello ACL'ler atayın. Tooprovide özel erişim, istediğiniz zaman sınırlı tooadding en fazla dokuz girişleri özel erişim için olduğundan kullanışlıdır. Toobetter Azure Active Directory güvenlik gruplarını kullanarak Data Lake Store'da depolanan verilerin güvenliğini nasıl hakkında daha fazla bilgi için bkz: [ACL'ler toohello Azure Data Lake Store dosya sistemi kullanıcılar veya güvenlik grubu atayın](data-lake-store-secure-data.md#filepermissions).

![Liste standart ve özel erişim](./media/data-lake-store-security-overview/adl.acl.2.png "listesinde standart ve özel erişim")

## <a name="network-isolation"></a>Ağ yalıtımı
Merhaba ağ düzeyinde kullanım Data Lake Store toohelp Denetim erişim tooyour verileri depolar. Güvenlik duvarları kurmak ve güvenilir istemcileriniz için bir IP adresi aralığı tanımlayabilirsiniz. Bir IP adresi aralığı ile tanımlanan hello aralığında bir IP adresine sahip yalnızca istemcileri tooData Lake Store bağlanabilir.

![Güvenlik Duvarı ayarları ve IP erişim](./media/data-lake-store-security-overview/firewall-ip-access.png "Güvenlik Duvarı ayarları ve IP adresi")

## <a name="data-protection"></a>Veri koruma
Azure Data Lake Store yaşam döngüsü boyunca verilerinizi korur. Aktarımdaki verileri için Data Lake Store hello ağ üzerinden hello endüstri standardı Aktarım Katmanı Güvenliği (TLS) protokolü toosecure verileri kullanır.

![Data Lake Store'da şifreleme](./media/data-lake-store-security-overview/adls-encryption.png "Data Lake Store'da şifreleme")

Data Lake Store ayrıca hello hesapta depolanan veriler için şifreleme sağlar. Şifreleme için kabul veya seçtiğiniz toohave şifrelenmiş verilerinizi kullanabilirsiniz. Şifreleme için kabul ederseniz, Data Lake Store içinde depolanan şifrelenmiş önceki toostoring kalıcı medyada verilerdir. Böyle bir durumda, Data Lake Store otomatik olarak veri önceki toopersisting şifreler ve hello verilere erişme tamamen saydam toohello istemci olacak şekilde veri önceki tooretrieval şifresini çözer. Merhaba istemci tarafı tooencrypt/şifre çözme veriler üzerinde gerekli kod değişiklik yoktur.

Anahtar Yönetimi için Data Lake Store hello Data Lake Store depolanan verilerin şifresini çözmek için gerekli olan ana şifreleme anahtarlarınızı (MEKs) yönetmek için iki mod sağlar. Data Lake Store hello MEKs yönettiğiniz veya Azure anahtar kasası hesabınızı kullanarak hello MEKs tooretain sahipliğini seçin ya da izin verebilirsiniz. Bir Data Lake Store hesabı oluşturma sırasında sırasında anahtar yönetimi hello modunu belirtin. Hakkında daha fazla bilgi için tooprovide şifreleme ilgili yapılandırma için bkz: [Azure Data Lake hello Azure Portal kullanarak Store ile çalışmaya başlama](data-lake-store-get-started-portal.md).

## <a name="auditing-and-diagnostic-logs"></a>Denetim ve tanılama günlükleri
Yönetim ilgili etkinlikleri veya ilgili verileri etkinlik günlükleri için mi aradığınız bağlı olarak, denetim veya tanılama günlüklerini kullanabilir.

* Yönetim ilgili etkinlikleri hello Azure portal denetim günlüklerini çıkmış ve Azure Resource Manager API'leri kullanın.
* Veri ilgili etkinlikleri ve hello Azure portal tanılama günlüklerini çıkmış WebHDFS REST API'lerini kullanın.

### <a name="auditing-logs"></a>Denetim günlükleri
belirli olaylara toodig gerekiyorsa toocomply düzenlemelere yeterli denetim izleri kuruluş gerektirebilir. Data Lake Store yerleşik izleme ve denetim sahiptir ve tüm hesap yönetimi etkinlikleri günlüğe kaydeder.

Hesap Yönetimi denetim izleri görüntülemek ve hello sütunları seçin toolog istiyor. Denetim günlükleri tooAzure depolama da verebilirsiniz.

![Denetim günlükleri](./media/data-lake-store-security-overview/audit-logs.png "Denetim günlükleri")

### <a name="diagnostic-logs"></a>Tanılama günlükleri
Veri erişimi denetim izleri hello Azure portalında (tanılama ayarları) olarak ayarlayın ve hello günlüklerinin depolandığı bir Azure Blob Depolama hesabı oluşturun.

![Tanılama günlüklerini](./media/data-lake-store-security-overview/diagnostic-logs.png "tanılama günlükleri")

Tanılama ayarlarını yapılandırdıktan sonra üzerinde hello hello günlüklerini görüntüleyebilirsiniz **tanılama günlüklerini** sekmesi.

Tanılama günlükleri Azure Data Lake Store ile çalışma hakkında daha fazla bilgi için bkz: [erişim Data Lake Store için tanılama günlükleri](data-lake-store-diagnostic-logs.md).

## <a name="summary"></a>Özet
Kurumsal müşteriler, güvenli ve kolay toouse bir veri analizi bulut platformunu talep. Azure Data Lake Store tasarlanmıştır toohelp adres kimlik yönetimi ve Azure Active Directory ile tümleştirme, ACL tabanlı yetkilendirme, ağ yalıtımı, veri şifreleme Aktarımdaki ve (hello gelen REST aracılığıyla kimlik doğrulaması aracılığıyla bu gereksinimleri Gelecekteki) ve denetim.

Data Lake Store'da toosee yeni özellikler istiyorsanız, bize Geri bildiriminizi hello gönderin [Data Lake deposu UserVoice Forumu](https://feedback.azure.com/forums/327234-data-lake).

## <a name="see-also"></a>Ayrıca bkz.
* [Azure Data Lake Store'a Genel Bakış](data-lake-store-overview.md)
* [Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md)
* [Data Lake Store'da verilerin güvenliğini sağlama](data-lake-store-secure-data.md)

