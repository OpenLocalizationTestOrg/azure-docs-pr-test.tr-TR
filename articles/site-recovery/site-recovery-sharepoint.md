---
title: "Azure Site Recovery kullanan çok katmanlı SharePoint uygulaması aaaReplicate | Microsoft Docs"
description: "Bu makalede nasıl tooreplicate Azure Site Recovery özelliklerini kullanarak çok katmanlı SharePoint uygulaması."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: sutalasi
ms.openlocfilehash: d856034ac2a3c95b0c1f0cf85e62c4e7a5a3210f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-sharepoint-application-for-disaster-recovery-using-azure-site-recovery"></a>Azure Site RECOVERY'yi kullanarak olağanüstü durum kurtarma için çok katmanlı bir SharePoint uygulama Çoğalt

Bu makalede ayrıntılı olarak nasıl kullanarak bir SharePoint uygulama tooprotect [Azure Site Recovery](site-recovery-overview.md).


## <a name="overview"></a>Genel Bakış

Microsoft SharePoint grubu yardımcı olabilecek güçlü bir uygulamadır veya departman düzenlemek, birlikte çalışın ve bilgileri paylaşın. SharePoint intranet portalları, belge ve dosya yönetimi, işbirliği, sosyal ağlara, extranet'ler, Web siteleri, kurumsal arama ve business Intelligence sağlayabilir. Ayrıca, sistem tümleştirme, işlem tümleştirme ve iş akışı Otomasyon özellikleri de sahiptir. Genellikle, kuruluşların Katman 1 uygulama hassas toodowntime ve veri kaybı düşünün.

Bugün, Microsoft SharePoint tüm giden kutusu olağanüstü durum kurtarma özellikleri sağlamaz. Merhaba türü ve bir olağanüstü durum ölçeğini bakılmaksızın, Kurtarma hello gruba kurtarabilirsiniz bir yedek veri merkezi hello kullanmayı içerir. Bekleme veri merkezleri burada yerel olarak yedekli sistemler ve yedeklemeleri hello kesinti hello birincil veri merkezindeki kurtaramazsınız senaryoları için gereklidir.

İyi olağanüstü durum kurtarma çözümü modelleme kurtarma planlarının bir SharePoint gibi hello karmaşık uygulama mimarileri geçici izin vermeniz gerekir. Ayrıca hello özelliği özelleştirilmiş tooadd adımları toohandle uygulama eşlemeleri çeşitli katmanları ve bu nedenle bir olağanüstü durum hello olayı içinde daha düşük RTO ile tek yük devretme sağlayarak arasında olması gerekir.

Bu makalede ayrıntılı olarak nasıl kullanarak bir SharePoint uygulama tooprotect [Azure Site Recovery](site-recovery-overview.md). Bu makalede, bir üç katmanı SharePoint uygulama tooAzure, nasıl bir olağanüstü durum kurtarma detaylandırma yapabilirsiniz ve yük devretme hello uygulama tooAzure işlemine çoğaltma için en iyi yöntemler ele alınacaktır.

Bir çoklu katmanı uygulama tooAzure kurtarma hakkında video aşağıda hello izleyebilirsiniz.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/Disaster-Recovery-of-load-balanced-multi-tier-applications-using-Azure-Site-Recovery/player]


## <a name="prerequisites"></a>Ön koşullar

Başlamadan önce hello aşağıdaki anladığınızdan emin olun:

1. [Bir sanal makine tooAzure çoğaltma](site-recovery-vmware-to-azure.md)
2. Nasıl çok[kurtarma ağını tasarlama](site-recovery-network-design.md)
3. [Bir test yük devretme tooAzure yapılması](site-recovery-test-failover-to-azure.md)
4. [Bir yük devretme tooAzure yapılması](site-recovery-failover.md)
5. Nasıl çok[bir etki alanı denetleyicisi çoğaltma](site-recovery-active-directory.md)
6. Nasıl çok[SQL Server çoğaltma](site-recovery-sql.md)

## <a name="sharepoint-architecture"></a>SharePoint mimarisi

SharePoint sunucularında, bir veya daha çok katmanlı topoloji ve sunucu rollerini tooimplement belirli hedefler ve hedefleri karşılayan bir grubu tasarımı kullanılarak dağıtılabilir. Çok sayıda eşzamanlı kullanıcı ve çok sayıda içerik öğelerini destekleyen bir tipik büyük, yüksek isteğe SharePoint sunucu grubu hizmeti gruplandırma kendi ölçeklenebilirlik stratejisinin bir parçası kullanın. Bu yaklaşım, bu hizmetleri birlikte gruplandırma ve ardından hello sunucuları dışında bir grup olarak ölçekleme adanmış sunuculara Hizmetleri çalıştırılmasını içerir. Merhaba aşağıdaki topoloji hello hizmeti ve üç katmanı bir SharePoint sunucu grubu gruplandırma server gösterir. Lütfen farklı SharePoint topolojileri hakkında ayrıntılı yönergeler için tooSharePoint belgeleri ve ürün satır mimarileri bakın. SharePoint 2013 dağıtımı hakkında daha fazla ayrıntı bulabilirsiniz [bu belgeyi](https://technet.microsoft.com/en-us/library/cc303422.aspx).



![Dağıtım modeli 1](./media/site-recovery-sharepoint/sharepointarch.png)


## <a name="site-recovery-support"></a>Site kurtarma desteği

Bu makalede oluşturmak için Windows Server 2012 R2 Enterprise VMware sanal makineleri kullanılmıştır. SharePoint 2013 Enterprise edition ve SQL server 2014 Enterprise edition kullanılmıştır. Site Recovery çoğaltma uygulama belirsiz olduğu gibi hello önerileri burada beklenen toohold üzerinde de aşağıdaki senaryolar için sağlanır.

### <a name="source-and-target"></a>Kaynak ve hedef

**Senaryo** | **tooa ikincil site** | **tooAzure**
--- | --- | ---
**Hyper-V** | Evet | Evet
**VMware** | Evet | Evet
**Fiziksel sunucu** | Evet | Evet

### <a name="sharepoint-versions"></a>SharePoint sürümleri
SharePoint server sürümleri aşağıdaki hello desteklenir.

* SharePoint server 2013 standart
* SharePoint server 2013 Enterprise
* SharePoint server 2016 standart
* SharePoint server 2016 Enterprise

### <a name="things-tookeep-in-mind"></a>Şeyler tookeep unutmayın

Paylaşılan bir disk tabanlı küme herhangi bir katmanı uygulamanızda kullandığınız sonra yapmamayı bu sanal makineleri mümkün toouse Site Recovery çoğaltma tooreplicate olabilir. Merhaba uygulama tarafından sağlanan yerel çoğaltma kullanın ve ardından bir [kurtarma planı](site-recovery-create-recovery-plans.md) toofailover tüm katmanları.

## <a name="replicating-virtual-machines"></a>Çoğaltma sanal makineler

İzleyin [bu kılavuz](site-recovery-vmware-to-azure.md) toostart hello sanal makine tooAzure çoğaltılıyor.

* Merhaba çoğaltma tamamlandıktan sonra her katman tooeach sanal makineye gidin ve aynı kullanılabilirlik kümesinde seçin emin olun ' yinelenmiş öğesi > Ayarlar > Özellikler > işlem ve ağ '. Örneğin, web katmanı 3 VM varsa, aynı kullanılabilirlik kümesinde Azure'da toobe parçası 3 VM'ler tüm hello yapılandırılmış emin olun.

    ![Set kullanılabilirlik kümesi](./media/site-recovery-sharepoint/select-av-set.png)

* Active Directory ve DNS'yi koruma ile ilgili yönergeler için çok başvuran[korumak Active Directory ve DNS](site-recovery-active-directory.md) belge.

* Veritabanı katmanı SQL sunucusunda çalışan koruma ile ilgili yönergeler için çok başvuran[SQL Server koruma](site-recovery-active-directory.md) belge.

## <a name="networking-configuration"></a>Ağ yapılandırması

### <a name="network-properties"></a>Ağ Özellikleri

* Merhaba VM'ler ekli toohello doğru DR Ağ Yük devretme sonrasında elde etmeniz hello uygulaması ve Web Katmanı VM'ler için Azure portalında ağ ayarlarını yapılandırın.

    ![Ağı seçin](./media/site-recovery-sharepoint/select-network.png)


* Bir statik IP kullanıyorsanız, sanal makine tootake hello içinde hello istediğiniz hello IP belirtin **hedef IP** alan

    ![Statik IP Ayarla](./media/site-recovery-sharepoint/set-static-ip.png)

### <a name="dns-and-traffic-routing"></a>DNS ve trafik yönlendirme

Siteler, Internet'e için ['Priority' türünde bir Traffic Manager profili oluşturma](../traffic-manager/traffic-manager-create-profile.md) hello Azure aboneliği içindeki. Ve ardından aşağıdaki şekilde hello DNS ve trafik Yöneticisi profili yapılandırın.


| **Burada** | **Kaynak** | **Hedef**|
| --- | --- | --- |
| Genel DNS | Genel DNS SharePoint siteleri için <br/><br/> Örn: sharepoint.contoso.com | Traffic Manager <br/><br/> contososharepoint.trafficmanager.NET |
| Şirket içi DNS | sharepointonprem.contoso.com | Merhaba şirket içi grubu üzerinde genel IP |


Merhaba trafik Yöneticisi profili içinde [hello birincil ve kurtarma uç noktaları oluşturma](../traffic-manager/traffic-manager-configure-priority-routing-method.md). Şirket içi uç nokta ve Azure uç noktası için genel IP Hello dış uç noktası kullanın. Merhaba önceliği yüksek tooon içi uç nokta ayarlandığından emin olun.

Ana bilgisayar katmanındaki hello SharePoint web sırada trafik Yöneticisi tooautomatically için belirli bir bağlantı noktası (örneğin, 800) bir test sayfası kullanılabilirlik post yük devretme algıla. Anonim kimlik doğrulaması, SharePoint siteleri hiçbirinde etkinleştiremiyor durumda geçici bir çözüm budur.

[Merhaba trafik Yöneticisi profili yapılandırma](../traffic-manager/traffic-manager-configure-priority-routing-method.md) hello ayarları aşağıda ile.

* Yönlendirme yöntemi - 'Priority'
* DNS toolive (TTL) - ' 30 saniye saat
* Anonim kimlik doğrulamasını etkinleştirirseniz, uç nokta izleme ayarları - belirli bir Web uç noktası verebilirsiniz. Veya belirli bir bağlantı noktasına (örneğin, 800) bir test sayfası kullanabilirsiniz.

## <a name="creating-a-recovery-plan"></a>Bir kurtarma planı oluşturma

Bir kurtarma planı çeşitli katmanlarda çok katmanlı bir uygulama, bu nedenle, uygulama tutarlılığını sağlamak hello yük devretme sıralama sağlar. Çok katmanlı web uygulaması için bir kurtarma planı oluşturulurken Hello aşağıdaki adımları izleyin. [Bir kurtarma planı oluşturma hakkında daha fazla bilgi](site-recovery-runbook-automation.md#customize-the-recovery-plan).

### <a name="adding-virtual-machines-toofailover-groups"></a>Sanal makineler toofailover grupları ekleme

1. Ekleme hello uygulaması ve Web Katmanı VM'ler tarafından bir kurtarma planı oluşturun.
2. 'Özelleştir' toogroup hello VM'ler üzerinde'ı tıklatın. Varsayılan olarak, tüm VM'ler 'Grubu 1' bir parçasıdır.

    ![RP özelleştirme](./media/site-recovery-sharepoint/rp-groups.png)

3. Başka bir grup (Grup 2) oluşturmak ve hello Web Katmanı VM'ler hello yeni grubuna taşıyın. Uygulama katmanınızı VM'ler 'Grubu 1' parçası olması gerekir ve Web Katmanı VM'ler 'Grubu 2' parçası olması gerekir. Uygulama katmanı VM'ler ilk Web Katmanı VM'ler tarafından izlenen önyüklenebilir hello tooensure budur.


### <a name="adding-scripts-toohello-recovery-plan"></a>Toohello kurtarma planı komutlar ekleme

En yaygın olarak kullanılan hello Azure Site Recovery betikleri hello 'tooAzure dağıtma' düğmesini tıklatarak Otomasyon hesabınızda dağıtabilirsiniz. Yayımlanmış herhangi komut dosyası kullanırken, hello hello betik yönergeleri emin olun.

[![TooAzure dağıtma](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)

1. Bir ön eylem betiği too'Group 1' toofailover SQL kullanılabilirlik grubu ekleyin. Merhaba örnek komut dosyalarını yayımlanan hello 'ASR-SQL-FailoverAG' komut dosyası kullanın. Merhaba betik hello yönergeleri ve gerekli hello hello komut dosyasında uygun şekilde değişiklik emin olun.

    ![Add-AG-komut dosyası--1. adım](./media/site-recovery-sharepoint/add-ag-script-step1.png)

    ![Add-AG-komut dosyası--2. adım](./media/site-recovery-sharepoint/add-ag-script-step2.png)

2. Bir yük dengeleyici hello üzerinde sanal makinelerin Web Katmanı (Grup 2) başarısız oldu post eylem betiği tooattach ekleyin. Merhaba örnek komut dosyalarını yayımlanan hello 'ASR-AddSingleLoadBalancer' komut dosyası kullanın. Merhaba betik hello yönergeleri ve gerekli hello hello komut dosyasında uygun şekilde değişiklik emin olun.

    ![Add-LB-komut dosyası--1. adım](./media/site-recovery-sharepoint/add-lb-script-step1.png)

    ![Add-LB-komut dosyası--2. adım](./media/site-recovery-sharepoint/add-lb-script-step2.png)

3. El ile adım tooupdate hello DNS kayıtları toopoint toohello yeni bir grubu Azure'da ekleyin.

    * Siteleri için Internet'e, gerekli post yük devretme hiçbir DNS güncelleştirmelerdir. Merhaba 'Ağ Kılavuzu' bölümüne tooconfigure trafik Yöneticisi açıklanan başlangıç adımları izleyin. Merhaba trafik Yöneticisi profili hello önceki bölümde açıklandığı şekilde ayarlanmış olması durumunda, bir komut dosyası tooopen kukla bağlantı noktası (800 hello örnekte) hello Azure VM üzerinde ekleyin.

    * Dahili kullanıma yönelik siteleri için el ile adım tooupdate hello DNS kaydı toopoint toohello yeni Web Katmanı VM'in yük dengeleyici IP ekleyin.

4. Bir yedek kopyadan el ile adım toorestore arama uygulaması ekleyin veya yeni bir arama hizmeti başlatın.

5. Arama hizmeti uygulaması bir yedekten geri yüklemek için aşağıdaki adımları izleyin.

    * Bu yöntem hello arama hizmeti uygulaması yedeğini hello yıkıcı olay önce gerçekleştirilen ve hello yedekleme hello DR sitede kullanılabilir olduğunu varsayar.
    * Bu kolayca hello yedekleme zamanlaması (örneğin, günde bir kez) ve hello DR sitede kopya yordamı tooplace hello Yedekleme kullanılarak gerçekleştirilebilir. Kopyalama yordamlarını AzCopy (Azure kopya) veya DFSR (Dağıtılmış Dosya Hizmetleri çoğaltma) ayarlama gibi komut dosyalı programları içerebilir.
    * Şimdi bu SharePoint grubu çalıştığından, hello 'Yedekleme ve geri yükleme' hello Merkezi Yönetim gidin ve geri yükleme seçin. Merhaba geri yükleme interrogates belirtilen hello yedekleme konumu (tooupdate hello değeri gerekebilir). Toorestore istediğiniz hello arama hizmeti uygulaması yedeklemeyi seçin.
    * Arama geri yüklendi. Geri yükleme hello unutmayın bekliyor toofind hello aynı topolojisi (sunucuları aynı sayıda) ve aynı sabit sürücü harfleri atanan toothose sunucuları. Daha fazla bilgi için bkz: ['Geri arama hizmeti uygulaması SharePoint 2013'te '](https://technet.microsoft.com/library/ee748654.aspx) belge.


6. Yeni bir arama hizmeti uygulaması başlatmak için aşağıdaki adımları izleyin.

    * Bu yöntem hello "Arama Yönetim" veritabanının bir yedeğini hello DR sitede kullanılabilir olduğunu varsayar.
    * Merhaba diğer arama hizmeti uygulaması veritabanları çoğaltılmaz olduğundan, yeniden oluşturulacak toobe ihtiyaç duyar. Bu nedenle, toodo tooCentral yönetim gidin ve hello arama hizmeti uygulaması silin. Tüm sunucularda hangi ana hello arama dizini hello dizin dosyalarını silin.
    * Merhaba arama hizmeti uygulaması yeniden oluşturun ve bu hello veritabanlarını yeniden oluşturur. Toohave önerilir bu yeniden oluşturur hazırlanmış bir komut dosyası hizmet uygulaması olası tooperform olmadığından hello GUI aracılığıyla tüm eylemler. Örneğin, hello arama topolojisi hello dizin sürücü konumunu ayarlama ve yalnızca SharePoint PowerShell cmdlet'lerini kullanarak mümkündür. Geri yükleme SPEnterpriseSearchServiceApplication Hello Windows PowerShell cmdlet'ini kullanın ve hello günlük aktarmalı ve arama yönetim veritabanı, Search_Service__DB çoğaltılmış belirtin. Bu cmdlet hello arama yapılandırması, şema, yönetilen özellikleri, kuralları ve kaynaklar sağlar ve diğer bileşenleri hello varsayılan kümesi oluşturur.
    * Arama hizmeti uygulaması sahip hello yeniden oluşturulan sonra her içerik kaynağı toorestore hello arama hizmeti için tam gezinme başlatmanız gerekir. Bazı analytics bilgileri arama önerileri gibi hello şirket içi gruptan kaybedersiniz.

7. Tüm hello adımları, hello kurtarma planı tamamlandıktan sonra hello son kurtarma planı aşağıdaki gibi görünür.

    ![Kaydedilen RP](./media/site-recovery-sharepoint/saved-rp.png)

## <a name="doing-a-test-failover"></a>Yük devretme sınamasını yapmak
İzleyin [bu kılavuz](site-recovery-test-failover-to-azure.md) toodo yük devretme sınaması.

1.  TooAzure portal gidin ve kurtarma hizmeti kasanızı seçin.
2.  SharePoint uygulaması için oluşturulmuş hello kurtarma planı tıklayın.
3.  'Test yük devretme üzerinde' tıklayın.
4.  Kurtarma noktası ve Azure sanal ağı toostart hello test yük devretme işlemi seçin.
5.  Merhaba ikincil ortamı kurma olduğunda, doğrulama gerçekleştirebilirsiniz.
6.  Merhaba doğrulama tamamlandıktan sonra 'Temizleme test Yük Devretmesini' hello kurtarma planı'ı tıklatın ve hello yük devretme sınama ortamı temizlendi.

AD için yük devretme testi yapılması konusunda yönergeler için ve DNS, çok[Test yük devretme AD için ilgili önemli noktalar ve DNS](site-recovery-active-directory.md#test-failover-considerations) belge.

Yük devretme testi SQL Always ON kullanılabilirlik grupları yapılması ile ilgili yönergeler için çok başvuran[yapılması Test yük devretme için SQL Server Always On](site-recovery-sql.md#steps-to-do-a-test-failover) belge.

## <a name="doing-a-failover"></a>Bir yük devretme işleminden
İzleyin [bu kılavuz](site-recovery-failover.md) bir yük devretme yapmak için.

1.  TooAzure portal gidin ve kurtarma Hizmetleri kasanız seçin.
2.  SharePoint uygulaması için oluşturulmuş hello kurtarma planı tıklayın.
3.  'Failover' üzerinde'ı tıklatın.
4.  Kurtarma noktası toostart hello yük devretme işlemini seçin.

## <a name="next-steps"></a>Sonraki adımlar
Hakkında daha fazla bilgiyi [diğer uygulamaları çoğaltma](site-recovery-workload.md) Site RECOVERY'yi kullanarak.
