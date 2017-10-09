---
title: "Site Recovery için aaaRun hello Hyper-V kapasite planlayıcısı aracı | Microsoft Docs"
description: "Nasıl toorun hello Hyper-V kapasite planlayıcısı aracı Azure Site Recovery için bu makalede"
services: site-recovery
documentationcenter: na
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 2bc3832f-4d6e-458d-bf0c-f00567200ca0
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: b853598e5cd290c48b59794ba48eefc72ac8ded6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-hyper-v-capacity-planner-tool-for-site-recovery"></a>Site Recovery için Hello Hyper-V kapasite planlayıcısı aracı çalıştırın

Azure Site Recovery dağıtımınızın bir parçası, çoğaltma ve bant genişliği gereksinimlerini toofigure gerekir. Site Recovery için Hello Hyper-V kapasite planlayıcısı aracı, toodo Bu, Hyper-V sanal makine çoğaltma için yardımcı olur.

Bu makalede nasıl toorun hello Hyper-V kapasite planlayıcısı aracı açıklanmaktadır. Bu araç, hello bilgileriyle birlikte kullanılması gerektiğini [kapasite planlaması için Site Recovery](site-recovery-capacity-planner.md).

## <a name="before-you-start"></a>Başlamadan önce
Bir Hyper-V sunucusunda veya küme düğümünde birincil sitenizi hello aracını çalıştırın. toorun hello aracı hello Hyper-V ana bilgisayar sunucuları gerekir:

* İşletim sistemi: Windows Server 2012 veya 2012 R2
* Bellek: 20 MB (en az)
* CPU: yüzde 5'i yükünü (en az)
* Disk alanı: 5 MB (en az)

Merhaba aracı çalıştırmadan önce tooprepare hello birincil site gerekir. Arasında çoğaltıyorsanız iki şirket içi sitelere ve toocheck bant genişliği istediğiniz, tooprepare aynı zamanda bir çoğaltma sunucusu gerekir.

## <a name="step-1-prepare-hello-primary-site"></a>1. adım: hello birincil site hazırlama

1. Merhaba birincil sitede hello Hyper-V sanal makinelerini istediğiniz tümünün listesini tooreplicate ve hello Hyper-V konakları/kümeleri üzerinde bulunduğu oldukları yapın. Hello aracı birden çok tek başına ana bilgisayarlar için veya tek bir küme, ancak ikisini birlikte için çalıştırabilirsiniz. Aşağıdaki gibi Hyper-V sunucuları hakkında bilgi toplamanız gereken şekilde, aynı zamanda toorun ayrı ayrı her işletim sistemi için gereken:

   * Windows Server 2012 tek başına sunucular
   * Windows Server 2012 kümeleri
   * Windows Server 2012 R2 tek başına sunucular
   * Windows Server 2012 R2 kümeleri
2. Uzaktan erişim tooWMI tüm hello Hyper-V konakları ve kümeleri etkinleştirin. Bu komut, her sunucu/kümede çalışan, toomake emin güvenlik duvarı kuralları ve kullanıcı izinleri ayarlanır:

        netsh firewall set service RemoteAdmin enable
3. Aşağıdaki gibi sunucuları ve kümeleri, performans izlemeyi etkinleştir:

   * Açık hello Windows Güvenlik Duvarı hello **Gelişmiş Güvenlik** ek bileşeni, ve ardından etkinleştir hello aşağıdaki gelen kuralları: **COM + Ağ erişimi (DCOM-ın)** ve hello tüm kuralları **Uzak Olay günlüğü Yönetim grubu**.

## <a name="step-2-prepare-a-replica-server-on-premises-tooon-premises-replication"></a>2. adım: çoğaltma sunucusunu (şirket içi tooon içi çoğaltma) hazırlama
TooAzure çoğaltıyorsanız toodo bu gerekmez.

Bir kukla VM çoğaltılmış tooit toocheck bant genişliği olması için tek bir Hyper-V ana bilgisayar kurtarma sunucusu olarak ayarlamanızı öneririz.  Bu atlayabilirsiniz, ancak bunu yapmanız sürece mümkün toomeasure bant genişliği olmayacaktır.

1. Toouse istiyorsanız, bir küme düğümü hello çoğaltma olarak Hyper-V çoğaltma aracısı yapılandırın:

   * İçinde **Sunucu Yöneticisi'ni**, açık **yük devretme kümesi Yöneticisi**.
   * Toohello kümesine bağlanın, hello küme adı vurgulayıp **Eylemler** > **rolü Yapılandır** tooopen hello Yüksek Kullanılabilirlik Sihirbazı.
   * İçinde **rolü Seç**, tıklatın **Hyper-V çoğaltma aracısı**. Başlangıç Sihirbazı'nda sağlayan bir **NetBIOS adı** ve hello **IP adresi** hello bağlantı noktası toohello küme (bir istemci erişim noktası denir) olarak kullanılan toobe. Merhaba **Hyper-V çoğaltma aracısı** dikkat etmeniz gerekir, bir istemci erişim noktası adı elde yapılandırılır.
   * Bu hello Hyper-V çoğaltma aracısı rolünün başarılı bir şekilde çevrimiçi olduğunu ve hello kümenin tüm düğümleri arasında yük devredebildiğini doğrulayın. toodo bunu hello rolüne sağ tıklayın, çok noktası**taşıma**ve ardından **düğüm Seç**. Bir düğüm seçin > **Tamam**.
   * Sertifika tabanlı kimlik doğrulaması kullanıyorsanız, tüm hello sertifikasının yüklü istemci erişim noktası hello ve her küme düğümüne emin olun.
2. Bir çoğaltma sunucusu etkinleştirin:

   * Bir küme için hata Küme Yöneticisi'ni açın, toohello kümesine bağlanın ve tıklayın **rolleri** > select rol > **çoğaltma ayarları** > **Bu kümeyi çoğaltma olarak etkinleştir Sunucu**. Bir küme hello çoğaltma olarak kullanırsanız, toohave hello Hyper-V çoğaltma aracısı rolünün hello küme hello da birincil sitedeki mevcut gerekir.
   * Tek başına bir sunucu için Hyper-V Yöneticisi'ni açın. Merhaba, **Eylemler** bölmesinde,'ı tıklatın **Hyper-V ayarları** tooenable, istediğiniz hello sunucusu için ve **çoğaltma yapılandırması** tıklatın **bunu etkinleştirin bilgisayarı çoğaltma sunucusu olarak**.
3. Kimlik doğrulaması ayarlayın:

   * İçinde **kimlik doğrulaması ve bağlantı noktaları**tooauthenticate hello nasıl birincil sunucu ve hello kimlik doğrulama bağlantı noktalarını seçin. Bir sertifika tıklatın kullanırsanız **Sertifika Seç** tooselect biri. Merhaba birincil ve kurtarma Hyper-V konakları hello Kerberos kullanırsanız aynı etki alanında veya güvenilen etki alanlarında. Farklı etki alanları için veya bir çalışma grubu dağıtımı için sertifikaları kullanın.
   * İçinde **yetkilendirme ve depolama**, izin **herhangi** (birincil) toosend çoğaltma verileri toothis çoğaltma sunucusu kimlik doğrulaması.

     ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image1.png)
   * Çalıştırma **netsh http show servicestate**, toocheck o hello dinleyicisi çalıştıran hello Protokolü/belirttiğiniz bağlantı noktası için:  
4. Güvenlik duvarları ayarlayın. Hyper-V yüklemesi sırasında güvenlik duvarı kuralları tooallow trafiği hello varsayılan bağlantı noktalarına (443 üzerindeki HTTPS, Kerberos 80 üzerinde) oluşturulur. Bu kurallar aşağıdaki gibi etkinleştirin:
  - Sertifika kimlik doğrulaması kümesindeki (443):``Get-ClusterNode | ForEach-Object {Invoke-command -computername \$\_.name -scriptblock {Enable-Netfirewallrule -displayname "Hyper-V Replica HTTPS Listener (TCP-In)"}}``
  - Kerberos kimlik doğrulaması kümesindeki (80):``Get-ClusterNode | ForEach-Object {Invoke-command -computername \$\_.name -scriptblock {Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"}}``
  - Tek başına sunucuda sertifika kimlik doğrulamasını:``Enable-Netfirewallrule -displayname "Hyper-V Replica HTTPS Listener (TCP-In)"``
  - Tek başına sunucuda Kerberos kimlik doğrulamasını:``Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"``

## <a name="step-3-run-hello-capacity-planner-tool"></a>3. adım: hello kapasite planlayıcısı aracı çalıştırma
Sonra birincil sitenizi hazırladığınız ve bir kurtarma sunucusu ayarlamanız, hello aracını çalıştırabilirsiniz.

1. [Karşıdan](https://www.microsoft.com/download/details.aspx?id=39057) hello Microsoft Download Center hello aracından.
2. Merhaba birincil sunuculardan biri (veya hello hello birincil küme düğümlerinden biri) Hello aracını çalıştırın. Merhaba .exe dosyasını sağ tıklatın ve ardından **yönetici olarak çalıştır**.
3. İçinde **başlamadan önce**, toocollect verilerin ne kadar süreyle istediğiniz belirtin. Üretim saatleri tooensure sırasında veri temsilcisidir hello aracı öneririz. Toovalidate ağ bağlantısı yalnızca çalışıyorsanız, yalnızca bir dakika toplayabilirsiniz.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image2.png)
4. İçinde **birincil site ayrıntıları**, hello sunucu adı veya FQDN için bir tek başına konak belirtin veya bir küme belirtmek için hello hello istemci FQDN'si noktası, küme adı veya hello kümedeki herhangi bir düğümün kabul etmek ve ardından **sonraki**. Merhaba aracı üzerinde çalıştırıldığı hello sunucusunun hello adı otomatik olarak algılar. Merhaba aracı Çekmeleri izlenebilir Vm'leri yedekleme belirtilen sunuculara hello.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image3.png)
5. İçinde **çoğaltma Site ayrıntıları**tooAzure çoğaltma yapıyorsanız ya da seçin tooa ikincil veri merkezine çoğaltma yapıyorsanız ve bir çoğaltma sunucusunu ayarlamadıysanız, **Atla çoğaltma sitesine içeren testler**. Tooa ikincil veri merkezine çoğaltma yapıyorsanız ve bir çoğaltma türü ayarladınız hello tek başına sunucu veya hello istemci erişim noktası FQDN'si hello küme için girin **sunucu adı (veya) Hyper-V çoğaltma aracısı CAP**.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image4.png)
6. İçinde **genişletilmiş çoğaltma ayrıntıları**, etkinleştirme **Atla hello testleri ilgili genişletilmiş çoğaltma sitesine**. Bu testler, Site Recovery tarafından desteklenmez.
7. İçinde **seçin VM'ler tooReplicate**, hello araçları toohello sunucuya veya kümeye bağlanır ve VM'ler görüntüler ve hello birincil sunucuda çalışan diskler üzerinde hello belirtilen hello ayarlara göre **Birincil Site ayrıntıları**  sayfası. VM'ler için çoğaltma zaten etkinleştirilmiş veya çalıştırmıyor, görüntülenmez. Toocollect ölçümleri istediğiniz hello sanal makineleri seçin. Merhaba VHD'ler otomatik olarak seçme çok hello VM'ler için verileri toplar.
8. Çoğaltma sunucusunun veya küme içinde yapılandırdığınız varsa **ağ bilgilerini**, düşündüğünüz hello yaklaşık WAN bant genişliğini kullanılacak hello birincil ve çoğaltma siteleri ve select hello sertifikaları arasında yapılandırmışsanız belirtin Sertifika kimlik doğrulaması.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image5.png)
9. İçinde **Özet**, hello ayarlarını denetleyin ve tıklayın **sonraki** ölçümleri toplama toobegin. Aracı ilerleme durumu ve durumu hello üzerinde görüntülenen **hesapla kapasite** sayfası. Merhaba aracı çalıştırma bittiğinde, bilgisayarınızı **raporu görüntüle** tooview hello çıktı. Varsayılan olarak, raporları ve günlükleri depolanmış **%systemdrive%\Users\Public\Documents\Capacity Planlayıcısı**.

   ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image6.png)

## <a name="step-4-interpret-hello-results"></a>4. adım: hello sonuçları yorumlama

Merhaba önemli ölçümleri şunlardır. Burada listelenmeyen ölçümleri yoksayabilirsiniz. Bunlar Site Recovery için uygun değil.

### <a name="on-premises-tooon-premises-replication"></a>Şirket içi tooon içi çoğaltma

* Çoğaltma hello birincil ana bilgisayarın hesaplama, bellek üzerindeki etkisi
* Çoğaltma hello birincil kurtarma konakları'nın depolama disk alanını IOPS üzerinde etkisi
* Değişim çoğaltması (Mbps) için gerekli toplam bant genişliği
* Merhaba birincil ana makinesi hello kurtarma ana bilgisayar (Mbps) arasındaki gözlenen ağ bant genişliği
* Merhaba ideal hello iki ana bilgisayarları/kümesi arasında etkin paralel aktarımı sayısını önerisi

### <a name="on-premises-tooazure-replication"></a>Şirket içi tooAzure çoğaltma

* Çoğaltma hello birincil ana bilgisayarın hesaplama, bellek üzerindeki etkisi
* Çoğaltma hello birincil konağın depolama disk alanı, IOPS etkisi
* Değişim çoğaltması (Mbps) için gerekli toplam bant genişliği

## <a name="more-resources"></a>Diğer kaynaklar
* Merhaba aracı hakkında ayrıntılı bilgi için hello aracı yükleme eşlik hello belgeyi okuyun.
* Bir kılavuz Keith Mayer'ın üzerinde hello aracının izleme [TechNet blogu](http://blogs.technet.com/b/keithmayer/archive/2014/02/27/guided-hands-on-lab-capacity-planner-for-windows-server-2012-hyper-v-replica.aspx).
* [Merhaba sonuçlar elde](site-recovery-performance-and-scaling-testing-on-premises-to-on-premises.md) şirket içi tooon içi Hyper-V çoğaltma için test bizim performansı

## <a name="next-steps"></a>Sonraki adımlar

Kapasite planlama bitirdikten sonra Site Recovery dağıtımı başlatabilirsiniz:

* [VMM Bulutları tooAzure Hyper-V Vm'lerini çoğaltma](site-recovery-vmm-to-azure.md)
* [Hyper-V Vm'lerini (VMM olmadan) tooAzure Çoğalt](site-recovery-hyper-v-site-to-azure.md)
* [Hyper-V Vm'lerini VMM siteler arası çoğaltma](site-recovery-vmm-to-vmm.md)
