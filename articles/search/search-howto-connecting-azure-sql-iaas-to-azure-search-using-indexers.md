---
title: "aaaSQL VM bağlantı tooAzure arama | Microsoft Docs"
description: "Şifreli bağlantıları etkinleştirmek ve bir Azure sanal makineden (VM) bir Azure Search oluşturucuda hello güvenlik duvarı tooallow bağlantıları tooSQL sunucusu yapılandırın."
services: search
documentationcenter: 
author: HeidiSteen
manager: pablocas
editor: 
ms.assetid: 46e42e0e-c8de-4fec-b11a-ed132db7e7bc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: heidist
ms.openlocfilehash: 1f0db8a2812b0a7d012e58bb873c4b2b29fa1338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-connection-from-an-azure-search-indexer-toosql-server-on-an-azure-vm"></a>Azure VM temelinde bir Azure Search dizin oluşturucu tooSQL Server öğesinden bir bağlantı yapılandırın
İçinde belirtildiği gibi [Azure SQL veritabanına bağlanma tooAzure arama dizin oluşturucular kullanma](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md#faq), dizin oluşturucular karşı oluşturma **Azure Vm'lerde SQL Server** (veya **SQL Azure VM'ler** kısaca) olan Azure Search tarafından desteklenen ancak ilk care of birkaç güvenlikle ilgili Önkoşullar tootake vardır. 

**Görev süresi:** yaklaşık 30 dakika zaten bir sertifika hello VM üzerinde yüklü.

## <a name="enable-encrypted-connections"></a>Şifreli bağlantıları etkinleştir
Azure arama şifreli kanal tüm dizin oluşturucu istekleri için ortak bir internet bağlantısı üzerinden gerektirir. Bu bölümde, bu iş hello adımları toomake listelenir.

1. Merhaba sertifika tooverify hello konu adı Hello özelliklerini olup hello Azure VM hello tam etki alanı adı (FQDN) denetleyin. Sertifikalar ek bileşenini tooview hello özellikleri hello ya da CertUtils gibi bir araç kullanın. Merhaba VM hizmeti dikey 's Essentials bölümünden, hello hello FQDN alabilirsiniz **genel IP adresi/DNS ad etiketi** hello alan [Azure portal](https://portal.azure.com/).
   
   * Merhaba yeni kullanılarak oluşturulan VM'ler için **Resource Manager** şablonu, FQDN Merhaba biçimlendirilmiş olarak `<your-VM-name>.<region>.cloudapp.azure.com`. 
   * Eski VM'ler olarak oluşturulan bir **Klasik** VM, FQDN olarak biçimlendirilmiş hello `<your-cloud-service-name.cloudapp.net>`. 
2. Merhaba Kayıt Defteri Düzenleyicisi'ni (regedit) kullanarak SQL Server toouse hello sertifika yapılandırın. 
   
    SQL Server Configuration Manager bu görev için genellikle kullanılsa da, bu senaryo için kullanamazsınız. Merhaba hello Azure VM FQDN'sini hello hello (Merhaba etki alanı hello yerel bilgisayar veya onu katılmışsa hello ağ etki alanı toowhich olarak tanımladığı) VM tarafından belirlenen FQDN eşleşmediği için sertifika hello içeri bulamaz. Adları eşleşmediğinde regedit toospecify hello sertifikası kullanın.
   
   * Regedit içinde toothis kayıt defteri anahtarını bulun: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\[MSSQL13.MSSQLSERVER]\MSSQLServer\SuperSocketNetLib\Certificate`.
     
     Merhaba `[MSSQL13.MSSQLSERVER]` bölümü sürümü ve örnek adı göre değişir. 
   * Merhaba hello değerini ayarlamak **sertifika** anahtar toohello **parmak izi** toohello VM içe hello SSL sertifikasının.
     
     Bazı daha iyi diğerlerinden birkaç yolu tooget hello parmak izi, vardır. Hello kopyalarsanız **sertifikaları** ek bileşenini MMC'de, büyük olasılıkla bir görünmez başında karakter çeker [Bu destek makalesinde açıklandığı gibi](https://support.microsoft.com/kb/2023869/), size çalıştığında hatayla sonuçlanır bir bağlantı. Birkaç geçici çözüm bu sorunu düzeltmek için mevcut. Merhaba kolay toobackspace sona erer ve hello ilk karakteri hello parmak izi tooremove hello başında karakter regedit hello anahtar değeri alanında yeniden yazın. Alternatif olarak, farklı aracı toocopy hello parmak kullanabilirsiniz.
3. Toohello hizmet hesabı izinleri verin. 
   
    Merhaba SQL Server hizmeti hesabının uygun hello özel anahtara hello SSL sertifikasının izni verildiğini doğrulayın. Bu adım overlook, SQL Server başlatılmaz. Merhaba kullanabilirsiniz **sertifikaları** ek bileşenini veya **CertUtils** bu görev için.
4. Merhaba SQL Server hizmetini yeniden başlatın.

## <a name="configure-sql-server-connectivity-in-hello-vm"></a>SQL Server bağlantısı hello VM Yapılandır
Azure Search tarafından gerekli hello şifreli bağlantı kurduktan sonra ek yapılandırma adımları iç tooSQL Azure vm'lerinde Server vardır. Henüz yapmadıysanız, hello sonraki adım Bu makaleler birini kullanarak toofinish yapılandırmadır:

* İçin bir **Resource Manager** VM bkz [tooa Azure Kaynak Yöneticisi'ni kullanarak SQL Server sanal makineye bağlanma](../virtual-machines/windows/sql/virtual-machines-windows-sql-connect.md). 
* İçin bir **Klasik** VM bkz [tooa Klasik Azure üzerinde SQL Server sanal makinesine bağlanmak](../virtual-machines/windows/classic/sql-connect.md).

Özellikle, her makale için hello bölümünde gözden "üzerinden bağlanan Internet Hello ifadesini".

## <a name="configure-hello-network-security-group-nsg"></a>Merhaba ağ güvenlik grubu (NSG) yapılandırma
Olağan dışı bir durum değil tooconfigure Azure VM erişilebilir tooother tarafların NSG ve karşılık gelen Azure uç noktası ya da erişim denetimi listesi (ACL) toomake hello. Bu, kendi uygulama mantığını tooconnect tooyour SQL Azure VM tooallow önce yaptıktan yüksektir. Bir Azure Search bağlantı tooyour SQL Azure VM için farklı değildir. 

Aşağıdaki Hello bağlantıları VM dağıtımlar için NSG yapılandırma hakkında yönergeler sağlar. TooACL bir Azure SEarch uç nokta IP adresine göre bu yönergeleri kullanın.

> [!NOTE]
> Arka plan için bkz: [bir ağ güvenlik grubu nedir?](../virtual-network/virtual-networks-nsg.md)
> 
> 

* İçin bir **Resource Manager** VM bkz [nasıl ARM dağıtımlar için Nsg'ler toocreate](../virtual-network/virtual-networks-create-nsg-arm-pportal.md). 
* İçin bir **Klasik** VM bkz [nasıl Klasik dağıtımlar için Nsg'ler toocreate](../virtual-network/virtual-networks-create-nsg-classic-ps.md).

IP adresleme hello sorunu ve olası geçici çözümler farkında olması durumunda, kolayca üstesinden birkaç yol açabilir. Merhaba kalan bölümler hello ACL sorunları ilgili tooIP adresleri işleme için öneriler sağlar.

#### <a name="restrict-access-toohello-search-service-ip-address"></a>Erişim toohello arama hizmeti IP adresi kısıtla
SQL Azure tooany bağlantı isteklerini açık VMs yapılmak yerine hello erişim toohello IP adresini hello ACL arama hizmetinizdeki kısıtlamak öneririz. Merhaba IP kolayca bulabilirsiniz adresine ping göre hello FQDN (örneğin, `<your-search-service-name>.search.windows.net`) search hizmetinizin.

#### <a name="managing-ip-address-fluctuations"></a>IP adresi dalgalanmaları yönetme
Arama hizmetinizi yalnızca bir arama birimi (diğer bir deyişle, bir çoğaltma ve bir bölüm) varsa, başlangıç IP adresi rutin hizmet yeniden başlatıldığında, search hizmetinizin IP adresine sahip varolan bir ACL geçersiz kılmalarını sırasında değiştirir.

Tek yönlü tooavoid hello sonraki bağlantı toouse birden fazla bir çoğaltma ve Azure Search'te bir bölüm hatasıdır. Bunun yapılması hello maliyetini artırır, ancak ayrıca hello IP adresi sorunu çözer. Birden fazla arama birimi varsa, Azure Search'te IP adreslerini değiştirmeyin.

İkinci bir yaklaşım tooallow hello bağlantı toofail olan ve hello NSG ACL'leri hello yeniden yapılandırın. Ortalama, IP adresleri toochange birkaç haftada bekleyebilirsiniz. Denetimli bir sık aralıklarla dizin yapan müşteriler için bu yaklaşım uygun olabilir.

Bir üçüncü uygulanabilir (ancak özellikle güvenli olmayan) toospecify hello IP adres aralığı hello arama hizmetinizi burada sağlanan Azure bölgesi yaklaşımdır. IP aralıklarını, genel IP adresleri tooAzure kaynakları ayrılır Hello listesi konumunda yayımlanır [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/details.aspx?id=41653). 

#### <a name="include-hello-azure-search-portal-ip-addresses"></a>Hello Azure Search portal IP adreslerini içerir
Hello Azure portal toocreate bir dizin oluşturucu kullanıyorsanız, Azure Search portal mantığı erişim tooyour SQL Azure VM oluşturma zamanı sırasında da gerekir. Azure arama portal IP adreslerini ping atılarak bulunabilir `stamp2.search.ext.azure.com`.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba yolu dışında yapılandırma ile artık bir SQL Server Azure VM'de bir Azure Search dizin oluşturucu için hello veri kaynağı olarak belirtebilirsiniz. Bkz: [Azure SQL veritabanına bağlanma tooAzure arama dizin oluşturucular kullanma](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md) daha fazla bilgi için.

