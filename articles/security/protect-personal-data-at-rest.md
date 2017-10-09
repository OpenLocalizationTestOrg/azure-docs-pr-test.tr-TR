---
title: "aaaAzure şifrelemeli REST kişisel verileri koruma | Microsoft Docs"
description: "Bu makalede, Azure tooprotect kişisel verileri kullanmanıza yardımcı olacak bir dizi bir parçasıdır"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 9af182b4897f1d04f5f519e6671f53b85073bae1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-at-rest-with-encryption"></a>Azure şifreleme teknolojilerini: rest şifrelemeli kişisel verileri korumak

Bu makalede anlamak ve Azure şifreleme teknolojileri toosecure veri bekleyen kullanmanıza yardımcı olur.

En iyi yöntem tooprotect hassas veya kişisel veri ve toomeet uyumluluk ve veri gizlilik gereksinimleri kalan verileri şifrelemesini gereklidir.
Bekleyen şifreleme zaman diskteki veri şifrelenir hello sağlayarak şifrelenmemiş hello veri erişimini tasarlanmış tooprevent hello saldırgan ' dir.

## <a name="scenario"></a>Senaryo 

Merhaba Amerika Birleşik Devletleri, yönetim büyük seyahat şirket, kendi işlemleri toooffer programlarıyla hello İngiliz Adaları arasında yanı sıra hello Akdeniz ve Baltık seas genişletmektedir. toosupport bu çaba İtalya, Almanya, Danimarka ve hello İngiltere dayanarak birkaç küçük seyahat satırları aldı

Merhaba şirket hello bulutta Microsoft Azure toostore şirket verileri kullanır. Bu çalışan ve/veya müşteri bilgileri gibi içerebilir:

- adresleri
- Telefon numaraları
- Vergi kimlik numaraları
- Sağlık bilgileri
- Kredi kartı bilgileri

Merhaba şirket ihtiyaç veri erişilebilir toothose Departmanlar yaparken hello gizlilik çalışan ve Müşteri verilerinin korumanız gerekir. (bordro ve ayırmaları Departmanlar gibi)

Merhaba seyahat satır Ayrıca, kişisel bilgi tootrack ilişkileri geçerli ve geçmiş müşterilerle içeren büyük bir veritabanını ödül ve bağlılık programı üyeleri korur.

### <a name="problem-statement"></a>Sorun bildirimi

Merhaba şirket, çalışanların ve müşterilerin kişisel verilerin hello gizliliği (bordro ve ayırmaları Departmanlar gibi) gereken veri erişilebilir toothose Departmanlar yaparken korumanız gerekir. Bu kişisel verileri hello denetlenen kurumsal veri merkezi dışında depolanır ve hello şirketin fiziksel denetiminde değildir.

### <a name="company-goal"></a>Şirket hedefi

Çok katmanlı savunma güvenlik stratejisinin bir parçası, kişisel verileri içeren tüm veri kaynakları, bulut depolama alanında bulunan dahil olmak üzere şifrelenmesini şirket hedef tooensure değil. Kişi kazanç erişim toohello kişisel verileri yetkisiz okunamaz kılacak bir formda olması gerekir. Şifreleme uygulama kolay veya – kullanıcılar ve Yöneticiler için saydam olmalıdır.

## <a name="solutions"></a>Çözümler

Azure hizmetleri sağlayan birden çok Araçlar ve teknolojiler toohelp şifreleyerek rest kişisel verileri koruyun.

### <a name="azure-key-vault"></a>Azure Key Vault

[Azure anahtar kasası](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) hello anahtarları kullanılan tooencrypt veri Azure Hizmetleri bekleyen ve hello anahtar depolama ve yönetim çözümü önerilir güvenli depolama sağlar. Şifreleme anahtar yönetimi depolanan önemli toosecuring verilerdir.

#### <a name="how-do-i-use-azure-key-vault-tooprotect-keys-that-encrypt-personal-data"></a>Kişisel verileri şifrelemek Azure anahtar kasası tooprotect anahtarları nasıl kullanabilirim?

Azure anahtar kasası toouse, abonelik tooan Azure hesabı gerekir. Ayrıca Azure PowerShell yüklü gerekir. PowerShell cmdlet'leri toodo hello aşağıdakileri kullanarak adımları içerir:

1. Tooyour abonelikleri Bağlan

2. Bir anahtar kasası oluşturma

3. Bir anahtar veya gizli toohello anahtar kasası ekleme

4. Azure Active Directory ile Merhaba anahtar kasası kullanacak uygulamaları kaydetme

5. Merhaba uygulamaları toouse hello anahtar veya gizli yetkilendirmek

toocreate bir anahtar kasası hello New-AzureRmKeyVault PowerShell cmdlet'ini kullanın. Kasa adı, kaynak grubu adı ve coğrafi konum atar. Diğer cmdlet'ler anahtarlarında yönetirken hello kasa adını kullanacaksınız. Merhaba REST API aracılığıyla hello kasası kullanan uygulamaların hello kasa URI'si kullanır.

Azure anahtar kasası yazılımla korunan anahtardan sizin için sağlayabilir veya mevcut bir anahtarı içeri aktarabilirsiniz bir. PFX dosyası. Merhaba kasasına gizli anahtarları (Parolalar) de depolayabilir.

Ayrıca, yerel HSM'NİZDE bir anahtar oluşturmak ve hello HSM sınırını terk hello anahtar olmadan hello anahtar kasası hizmetindeki tooHSMs aktarım.

Azure anahtar kasası kullanma hakkında ayrıntılı yönergeler izleyin hello adımları [Azure anahtar kasası ile çalışmaya başlama.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)

Azure anahtar kasası ile kullanılan PowerShell cmdlet'leri listesi için bkz: [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).

### <a name="azure-disk-encryption-for-windows"></a>Windows için Azure Disk şifrelemesi

[Azure Disk şifrelemesi for Windows ve Linux Iaas VM'ler](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) Azure sanal makinelerde rest kişisel verilerinizi korur ve Azure anahtar kasası ile tümleşir. Azure Disk şifrelemesi kullanan [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) Windows ve [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) Linux tooencrypt hem işletim sistemi ve hello veri diskleri hello. Azure Disk şifrelemesi, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 ve Windows 8 ve Windows 10 istemcileri desteklenir.

#### <a name="how-do-i-use-azure-disk-encryption-tooprotect-personal-data"></a>Azure Disk şifrelemesi tooprotect kişisel verileri nasıl kullanabilirim?

Azure Disk şifrelemesi toouse, abonelik tooan Azure hesabı gerekir. için tooenable Azure Disk şifrelemesi Windows ve Linux VM'ler hello aşağıdaki:

1. Hello Azure Disk şifrelemesi Resource Manager şablonu, PowerShell veya hello komut satırı arabirimi (CLI) tooenable disk şifrelemesi kullanın ve şifreleme yapılandırması belirtin. 

2. GRANT erişim toohello Azure platformu tooread hello şifreleme anahtar kasanızı malzemesini.

3. Bir Azure Active Directory (AAD) uygulama kimliği toowrite hello şifreleme anahtar malzeme tooyour anahtar kasası sağlar.

Azure VM hello ve hello anahtar kasası yapılandırma güncelleyin ve şifrelenmiş VM'nizi ayarlayın.

Anahtar kasası toosupport Azure Disk şifrelemesi ayarladığınızda, ek güvenlik ve şifrelenmiş sanal makinelerin toosupport yedekleme için bir anahtar şifreleme anahtarı (KEK) ekleyebilirsiniz.

![](media/protect-personal-data-at-rest/create-key.png)

Ayrıntılı yönergeler belirli dağıtım senaryoları ve kullanıcı deneyimleri için dahil edilmiştir [için Azure Disk şifrelemesi Windows ve Linux Iaas VM'ler.](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)

### <a name="azure-storage-service-encryption"></a>Azure Depolama Hizmeti Şifrelemesi

[Azure Storage hizmeti şifreleme (SSE) bekleyen veri için](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) korumak ve veri toomeet, kuruluş güvenlik ve uyumluluk taahhüt korumaya yardımcı olur. Azure depolama otomatik olarak 256 bit AES şifreleme önceki toopersisting toostorage kullanarak verilerinizi şifreler ve önceki tooretrieval şifresini çözer. Bu hizmet, Azure BLOB'ları ve dosyaları için kullanılabilir.

#### <a name="how-do-i-use-storage-service-encryption-tooprotect-personal-data"></a>Depolama hizmeti şifrelemesi tooprotect kişisel verileri nasıl kullanabilirim?

tooenable depolama hizmeti şifrelemesi, hello aşağıdaki:

1. Hello Azure portalında oturum açın.

2. Bir depolama hesabı seçin.

3. Ayarları'nda, hello Blob hizmeti bölümü altında şifreleme seçin.

4. Hello dosya hizmeti bölümü altında şifreleme seçin.

Hello şifreleme ayarı tıkladıktan sonra etkinleştirme veya depolama hizmeti şifrelemesi devre dışı bırakabilirsiniz.

![](media/protect-personal-data-at-rest/storage-service-encryption.png)

Yeni veri şifrelenir. Bu depolama hesabı var olan dosyalardaki veriler şifrelenmemiş kalır.

Şifreleme etkinleştirdikten sonra yöntemler aşağıdaki hello birini kullanarak veri toohello depolama hesabı kopyalayın:

1. Kopyalama BLOB veya hello dosyalarıyla [AzCopy komut satırı yardımcı programı](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).

2. [SMB kullanan bir dosya paylaşımını bağlama](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) Robocopy toocopy dosyaları gibi bir yardımcı programını kullanabilirsiniz.

3. Depolama hesaplarını kullanarak blob veya dosya veri tooand blob depolama biriminden veya arasında kopyalama [depolama istemcisi kitaplıklarını .NET gibi](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).

4.  Kullanım bir [Depolama Gezgini](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) tooupload BLOB tooyour depolama hesabı'şifreleme etkin.

### <a name="transparent-data-encryption"></a>Saydam Veri Şifrelemesi

Saydam veri şifreleme (TDE), SQL Azure hem hello veritabanı ve sunucu düzeyi verileri şifrelemek bir özelliktir. TDE, şimdi tüm yeni oluşturulan veritabanı üzerinde varsayılan olarak etkindir. TDE, gerçek zamanlı I/O şifreleme ve şifre çözme hello veri ve günlük dosyalarının gerçekleştirir.

#### <a name="how-do-i-use-tde-tooprotect-personal-data"></a>TDE tooprotect kişisel verileri nasıl kullanabilirim?

TDE hello Azure portal hello REST API veya PowerShell kullanarak yapılandırabilirsiniz. tooenable TDE hello Azure Portal kullanarak var olan bir veritabanı üzerinde hello aşağıdaki:

1. Hello Azure'ı ziyaret edin, portal <https://portal.azure.com> ve Azure yönetici veya katkıda hesabınız ile oturum açın.

2. Merhaba sol başlık tooBROWSE'ı tıklatın ve ardından SQL veritabanları tıklayın.

3. Merhaba sol bölmede seçili SQL veritabanları ile kullanıcı veritabanınız'ı tıklatın.

4. Merhaba veritabanı dikey penceresinde tüm ayarlar'ı tıklatın.

5. Hello ayarları dikey penceresinde, saydam veri şifreleme bölümü tooopen hello saydam veri şifreleme dikey tıklayın.

6. Merhaba veri şifreleme dikey penceresinde hello veri şifreleme düğmesi tooOn taşıyın ve (Merhaba sayfanın en üstündeki hello) Kaydet'i tıklatın tooapply hello ayarı. Merhaba şifreleme durumu hello saydam veri şifreleme hello ilerlemesini yaklaşık.

![Veri şifrelemeyi etkinleştirme](media/protect-personal-data-at-rest/turn-data-encryption-on.png)

Tooenable TDE ve TDE korumalı veritabanları ve daha fazlasını çözme hakkında bilgi hello makalesinde nasıl bulunabilir yönergeleri [saydam veri şifrelemesi ile Azure SQL veritabanı.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)

## <a name="summary"></a>Özet

Merhaba şirket hello Azure bulut depolanan kişisel verileri şifreleme kendi amacı gerçekleştirebilirsiniz. Azure Disk şifrelemesi kullanarak bunu yapabilmeleri çok tüm birimlerini koruyun. Bu, hem hello işletim sistemi dosyalarını hem de kişisel olarak tanımlanabilir bilgileri ve diğer hassas verileri tutmak veri dosyaları içerebilir. Azure depolama hizmeti şifrelemesi, BLOB'lar ve dosyaları depolanan kullanılan tooprotect kişisel veriler olabilir. Azure SQL veritabanlarında depolanan veriler için saydam veri şifreleme yetkisiz Etkilenme kişisel bilgilerin kullanımına karşı koruma sağlar.

azure'da kullanılan tooencrypt veri tooprotect hello anahtarları, Azure anahtar kasası hello şirket kullanabilirsiniz. Bu hello anahtar yönetimi işlemini kolaylaştırır ve erişmek ve kişisel veri şifreleme anahtarları şirket toomaintain denetimini etkinleştirir hello.

## <a name="next-steps"></a>Sonraki adımlar

- [Azure Disk şifrelemesi sorun giderme kılavuzu](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-tsg)

- [Azure sanal Makine'yi şifreleme](https://docs.microsoft.com/en-us/azure/security-center/security-center-disk-encryption?toc=%2fazure%2fsecurity%2ftoc.json)

- [Azure Data Lake Store'da verilerin şifrelenmesi](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)

- [Bekleyen Azure Cosmos DB veritabanı şifreleme](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)
