---
title: "aaaMonitor ve sanal makineleri ve fiziksel sunucuları için koruması sorunlarını giderme | Microsoft Docs"
description: "Azure Site Recovery hello çoğaltma, yük devretme ve kurtarma şirket içi sunucuları tooAzure veya ikincil bir veri merkezinde bulunan sanal makinelerin düzenler. Bu makale toomonitor kullanın ve Virtual Machine Manager veya Hyper-V sitesi koruması sorunlarını giderme."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 0fc8e368-0c0e-4bb1-9d50-cffd5ad0853f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: d790375db5f30e98f009c8d8272558188c51934c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-troubleshoot-protection-for-virtual-machines-and-physical-servers"></a>İzleme ve sanal makineleri ve fiziksel sunucuları için koruması sorunlarını giderme
Bu izleme ve sorun giderme kılavuzu yardımcı olduğu hakkında bilgi edineceksiniz nasıl tootrack çoğaltma sistem durumunu ve teknikleri Azure Site Recovery için sorun giderme.

## <a name="understand-hello-components"></a>Merhaba bileşenlerini anlama
### <a name="vmware-virtual-machine-or-physical-server-site-deployment-for-replication-between-on-premises-and-azure"></a>VMware sanal makine ya da şirket içi ve Azure arasında çoğaltma için fiziksel sunucu sitesi dağıtımı
tooset bir şirket içi VMware sanal makinesi veya fiziksel sunucu ve Azure arasında veritabanı kurtarma yukarı tooset hello yapılandırma sunucusu, ana hedef sunucusu ve sanal makine ya da sunucu üzerinde işlem sunucusu bileşenleri gerekir. Merhaba kaynak sunucu için korumayı etkinleştirdiğinizde, Azure Site Recovery hello Microsoft Azure App Service Mobile Apps özelliğini yükler. Şirket içi kesinti ve hello kaynak sunucu başarısız tooAzure üzerinden sonrasında, müşterilerin Azure işlem sunucusu ve şirket içi toorebuild hello kaynak sunucu şirket içi ana hedef sunucusunda tooset gerekir.

![Şirket içi ve Azure arasında çoğaltma için VMware/fiziksel sitesi dağıtımı](media/site-recovery-monitoring-and-troubleshooting/image18.png)

### <a name="virtual-machine-manager-site-deployment-for-replication-between-on-premises-sites"></a>Sanal Makine Yöneticisi site dağıtım için şirket içi siteler arasında çoğaltma
veritabanı kurtarma iki arasında yukarı tooset şirket içi konumlara, toodownload hello Azure Site Recovery sağlayıcısı gerekir ve hello Virtual Machine Manager sunucusuna yükleyin. Merhaba sağlayıcısının hello Azure portal ' tetiklenen tüm hello işlemleri çevrilmiş tooon içi işlemleri Al Internet bağlantısı tooensure gerekir.

![Sanal Makine Yöneticisi site dağıtım için şirket içi siteler arasında çoğaltma](media/site-recovery-monitoring-and-troubleshooting/image1.png)

### <a name="virtual-machine-manager-site-deployment-for-replication-between-on-premises-locations-and-azure"></a>Şirket içi konumları ve Azure arasında çoğaltma için Sanal Makine Yöneticisi sitesi dağıtımı
Şirket içi konumları ve Azure arasında veritabanı kurtarma ayarladığınızda, toodownload hello Azure Site Recovery sağlayıcısı gerekir ve hello Virtual Machine Manager sunucusuna yükleyin. Ayrıca tooinstall hello her Hyper-V ana bilgisayar üzerine yüklü toobe gereken Azure kurtarma Hizmetleri Aracısı gerekir. [Daha fazla bilgi edinin](site-recovery-hyper-v-azure-architecture.md) daha fazla bilgi için.

![Şirket içi konumları ve Azure arasında çoğaltma için Sanal Makine Yöneticisi sitesi dağıtımı](media/site-recovery-monitoring-and-troubleshooting/image2.png)

### <a name="hyper-v-site-deployment-for-replication-between-on-premises-locations-and-azure"></a>Şirket içi konumları ve Azure arasında çoğaltma için Hyper-V sitesi dağıtımı
Benzer tooVirtual Makine Yöneticisi dağıtım işlemidir. Merhaba yalnızca hello Azure Site Recovery sağlayıcısı ve Azure kurtarma Hizmetleri Aracısı hello Hyper-V ana bilgisayarın üzerinde yüklü farktır. [Daha fazla bilgi edinin](site-recovery-hyper-v-azure-architecture.md). .

## <a name="monitor-configuration-protection-and-recovery-operations"></a>Yapılandırma, koruma ve kurtarma işlemlerini izleme
Her işlem Azure Site Recovery, denetlenen ve hello altında izlenen **İŞLERİ** sekmesi. Yapılandırma, koruma veya kurtarma hatası için toohello Git **İŞLERİ** sekmesinde ve hatalar için bakın.

![Merhaba İŞLER sekmesinde Hello başarısız filtresi](media/site-recovery-monitoring-and-troubleshooting/image3.png)

Hataları hello altında bulursanız **İŞLERİ** sekmesinde hello iş'i tıklatın ve'ı tıklatın **hata ayrıntıları** iş.

![Merhaba hata ayrıntıları düğmesi](media/site-recovery-monitoring-and-troubleshooting/image4.png)

Merhaba hata ayrıntıları, olası nedeni ve hello sorunu için öneri belirlemenize yardımcı olur.

![Belirli bir iş için hata ayrıntılarını gösteren iletişim kutusu](media/site-recovery-monitoring-and-troubleshooting/image5.png)

Merhaba önceki örnekte, devam eden başka bir işlem hello koruma yapılandırması toofail neden toobe gibi görünüyor. Merhaba öneriye dayalı hello sorunu çözün ve ardından **RESART** tooinitiate hello işlemi yeniden.

![Merhaba İŞLER sekmesinde Hello yeniden Başlat düğmesi](media/site-recovery-monitoring-and-troubleshooting/image6.png)

Merhaba **yeniden** seçeneği tüm işlemler için kullanılabilir değil. Bir işlem hello yoksa **yeniden** seçeneği, toohello nesne geri dönün ve yeniden hello işlemini yineleyin. Devam eden herhangi bir işi iptal edebilirsiniz hello kullanarak **iptal** düğmesi.

![Merhaba iptal düğmesi](media/site-recovery-monitoring-and-troubleshooting/image7.png)

## <a name="monitor-replication-health-for-virtual-machines"></a>Sanal makineler için çoğaltma durumunu izleme
Hello Azure portal tooremotely İzleyici Azure Site Recovery sağlayıcıları her korumalı hello varlıklar için kullanabilirsiniz. Tıklatın **KORUNAN ÖĞELER**ve ardından **VMM BULUTLARI** veya **koruma grupları**. Merhaba **VMM BULUTLARI** sekmesi üzerinde Virtual Machine Manager tabanlı dağıtımlar için kullanılabilir, yalnızca. Merhaba altında diğer senaryolar için korumalı hello varlıklardır **koruma grupları** sekmesi.

![Merhaba VMM Bulutları ve koruma grupları seçenekleri](media/site-recovery-monitoring-and-troubleshooting/image8.png)

Kullanılabilir tüm işlemlerin hello alt bölmesinde gösterilir hello ilgili Bulut veya koruma grubu toosee altında bir Korunan varlık tıklatın.

![Seçilen bir Korunan varlık için kullanılabilir seçenekleri](media/site-recovery-monitoring-and-troubleshooting/image9.png)

Merhaba önceki ekran görüntüsünde gösterildiği gibi hello sanal makine sistem durumu olan **kritik**. Merhaba tıklayabilirsiniz **hata ayrıntıları** düğmesi hello alt toosee hello hata. Merhaba üzerinde temel **olası nedenleri** ve **öneri**, hello sorunu çözün.

![Merhaba hata ayrıntıları düğmesi](media/site-recovery-monitoring-and-troubleshooting/image10.png)

![Hatalar ve hello hata ayrıntıları iletişim kutusunda öneriler](media/site-recovery-monitoring-and-troubleshooting/image11.png)

> [!NOTE]
> Herhangi bir etkin işlem sürüyor veya başarısız oldu, toohello Git **İŞLERİ** belirli bir iş için belirtilen önceki tooview hello hata olarak görüntüle.
>
>

## <a name="troubleshoot-on-premises-hyper-v-issues"></a>Şirket içi Hyper-V sorunlarını giderme
Toohello şirket içi Hyper-V Yöneticisi konsolunda, select hello sanal makine, bağlanmak ve hello çoğaltma sistem durumunu görebilirsiniz.

![Merhaba Hyper-V Yöneticisi konsolunda seçeneği tooview çoğaltma durumu](media/site-recovery-monitoring-and-troubleshooting/image12.png)

Bu durumda, **çoğaltma sistem durumunu** olan **kritik**. Merhaba sanal makineye sağ tıklayın ve ardından **çoğaltma** > **çoğaltma durumunu görüntüle** toosee hello ayrıntıları.

![Belirli bir sanal makine için çoğaltma durumu](media/site-recovery-monitoring-and-troubleshooting/image13.png)

Merhaba sanal makine için çoğaltma duraklatıldı durumunda hello sanal makineye sağ tıklayın ve ardından **çoğaltma** > **çoğaltmayı devam ettir**.

![Merhaba Hyper-V Yöneticisi konsolunda seçeneği tooresume çoğaltma](media/site-recovery-monitoring-and-troubleshooting/image19.png)

Merhaba küme veya tek başına makine içinde yeni bir Hyper-V ana bilgisayar sanal makine geçirir ve hello Hyper-V konağı Azure Site Recovery ile yapılandırılmış, hello sanal makinesi için çoğaltma etkilenmiş olmayacaktır. Bu hello yeni Hyper-V ana bilgisayar tüm hello önkoşulları karşıladığını ve Azure Site Recovery kullanılarak yapılandırılan emin olun.

### <a name="event-log"></a>Olay günlüğü
| Olay kaynakları | Ayrıntılar |
| --- |:--- |
| **Uygulamalar ve hizmet günlükleri/Microsoft/VirtualMachineManager/Server/Admin** (Virtual Machine Manager sunucusu) |Yararlı günlük tootroubleshoot birçok farklı Sanal Makine Yöneticisi sorunları sağlar. |
| **Uygulamalar ve hizmet günlükleri/MicrosoftAzureRecoveryServices/çoğaltma** (Hyper-V ana bilgisayarı) |Yararlı günlük tootroubleshoot pek çok Microsoft Azure kurtarma Hizmetleri Aracısı sorunları sağlar. <br/> ![Hyper-V ana bilgisayar için çoğaltma olay kaynağı konumu](media/site-recovery-monitoring-and-troubleshooting/eventviewer03.png) |
| **Uygulamalar ve hizmet günlükleri/Microsoft/Azure Site kurtarma/sağlayıcı/Operational** (Hyper-V ana bilgisayarı) |Yararlı günlük tootroubleshoot pek çok Microsoft Azure Site Recovery hizmeti sorunları sağlar. <br/> ![Hyper-V ana bilgisayar için işletimsel olay kaynağı konumu](media/site-recovery-monitoring-and-troubleshooting/eventviewer02.png) |
| **Uygulamalar ve hizmet günlükleri/Microsoft/Windows/Hyper-V-VMMS/Admin** (Hyper-V ana bilgisayarı) |Yararlı günlük tootroubleshoot birçok Hyper-V sanal makine yönetimi konularını sağlar. <br/> ![Hyper-V ana bilgisayar için Sanal Makine Yöneticisi olay kaynağı konumu](media/site-recovery-monitoring-and-troubleshooting/eventviewer01.png) |

### <a name="hyper-v-replication-logging-options"></a>Hyper-V çoğaltma günlük seçenekleri
TooHyper-V çoğaltma ilgilidir tüm olayları hello Hyper-V-VMMS kaydedilir\\yönetici günlük uygulama ve hizmet günlükleri altında bulunan\\Microsoft\\Windows. Ayrıca, hello Hyper-V sanal makine Yönetimi hizmeti için analitik bir günlüğünü etkinleştirebilirsiniz. tooenable bu oturum, ilk analitik hello yapın ve hata ayıklama günlüklerini Olay Görüntüleyicisi'ni hello içinde görüntülenebilir. Olay Görüntüleyicisi'ni açın ve ardından **Görünüm** > **Analitik ve hata ayıklama günlüklerini göster**.

![Merhaba Analitik ve hata ayıklama günlüklerini göster seçeneği](media/site-recovery-monitoring-and-troubleshooting/image14.png)

Analitik günlüğü'nün altında görülebilir **Hyper-V-VMMS**.

![Merhaba analitik hello Olay Görüntüleyicisi'ni ağacında oturum](media/site-recovery-monitoring-and-troubleshooting/image15.png)

Merhaba, **Eylemler** bölmesinde tıklatın **günlüğü etkinleştir**. Bu özellik etkinleştirildikten sonra görünür **Performans İzleyicisi'ni** olarak bir **olay izleme oturumu** altında bulunan **veri toplayıcı kümeleri.**

![Olay izleme oturumları hello Performans İzleyicisi ağacında](media/site-recovery-monitoring-and-troubleshooting/image16.png)

tooview toplanan bilgileri Merhaba, ilk hello günlüğü devre dışı bırakarak hello izleme oturumunu durdur. Merhaba günlüğünü kaydedin ve yeniden Olay Görüntüleyicisi'nde açın veya diğer araçlar tooconvert kullanmak istediğiniz olarak.

## <a name="reach-out-for-microsoft-support"></a>Microsoft Support ulaşın
### <a name="log-collection"></a>Günlük toplama
Sanal Makine Yöneticisi site koruma için çok başvuran[Destek Tanılama Platformu (SDP) aracını kullanarak Azure Site Recovery günlük toplama](http://social.technet.microsoft.com/wiki/contents/articles/28198.asr-data-collection-and-analysis-using-the-vmm-support-diagnostics-platform-sdp-tool.aspx) toocollect hello gerekli günlükleri.

Hyper-V site koruma için indirme [aracı](https://dcupload.microsoft.com/tools/win7files/DIAG_ASRHyperV_global.DiagCab) ve'hello Hyper-V ana bilgisayar toocollect hello günlüklerini yürütün.

VMware/fiziksel sunucusu senaryoları için çok başvuran[VMware ve fiziksel site koruma için Azure Site Recovery günlük toplama](http://social.technet.microsoft.com/wiki/contents/articles/30677.azure-site-recovery-log-collection-for-vmware-and-physical-site-protection.aspx) toocollect hello gerekli günlükleri.

Merhaba aracı hello günlükleri rastgele adlandırılmış bir alt klasör % LocalAppData%\ElevatedDiagnostics altında yerel olarak toplar.

![Hyper-V sitesi korumadan gösterilen örnek adımlar.](media/site-recovery-monitoring-and-troubleshooting/animate01.gif)

### <a name="open-a-support-ticket"></a>Bir destek bileti açın
tooraise, Azure Site kurtarma için bir destek bileti URL'yi kullanarak destek tooAzure ulaşmak adresindeki <http://aka.ms/getazuresupport>.

## <a name="kb-articles"></a>KB makaleleri
* [Nasıl toopreserve hello sürücü harfi için korunan üzerinden başarısız veya tooAzure geçirilen bir sanal makine](http://support.microsoft.com/kb/3031135)
* [Nasıl toomanage tooAzure koruma ağ bant genişliği kullanımını şirket içi](https://support.microsoft.com/kb/3056159)
* [Bir sanal makine için korumayı tooenable çalıştığınızda azure Site Recovery: "Merhaba küme kaynağı bulunamadı" hatası](http://support.microsoft.com/kb/3010979)
* [Anlama ve sorun giderme Hyper-V çoğaltma Kılavuzu](http://social.technet.microsoft.com/wiki/contents/articles/21948.hyper-v-replica-troubleshooting-guide.aspx)

## <a name="common-azure-site-recovery-errors-and-their-resolutions"></a>Sık karşılaşılan Azure Site Recovery hataları ve bunların çözümleri
Sık karşılaşılan hataları ve bunların çözümleri aşağıda verilmiştir. Her hata ayrı wiki sayfa içinde belgelenmiştir.

### <a name="general"></a>Genel
* <span style="color:green;">Yeni</span> [işleri "bir işlem devam ediyor." hatasıyla başarısız oluyor Hata 505, 514, 532.](http://social.technet.microsoft.com/wiki/contents/articles/32190.azure-site-recovery-jobs-failing-with-error-an-operation-is-in-progress-error-505-514-532.aspx)
* <span style="color:green;">Yeni</span> ["Bağlı toohello Internet sunucusu değil" hatası ile başarısız olan işler. Hata 25018.](http://social.technet.microsoft.com/wiki/contents/articles/32192.azure-site-recovery-jobs-failing-with-error-server-isn-t-connected-to-the-internet-error-25018.aspx)

### <a name="setup"></a>Kurulum
* [Merhaba Sanal Makine Yöneticisi sunucusu tooan iç hata kaydedilemedi. Merhaba hata hakkında daha fazla ayrıntı için lütfen toohello hello Site Recovery portalında jobs görünümüne bakın. Kur'u yeniden tooregister hello sunucu.](http://social.technet.microsoft.com/wiki/contents/articles/25570.the-vmm-server-cannot-be-registered-due-to-an-internal-error-please-refer-to-the-jobs-view-in-the-site-recovery-portal-for-more-details-on-the-error-run-setup-again-to-register-the-server.aspx)
* [Bir bağlantı kurulan toohello Hyper-V kurtarma Yöneticisi kasası olamaz. Merhaba proxy ayarlarını doğrulayın veya daha sonra yeniden deneyin.](http://social.technet.microsoft.com/wiki/contents/articles/25571.a-connection-cant-be-established-to-the-hyper-v-recovery-manager-vault-verify-the-proxy-settings-or-try-again-later.aspx)

### <a name="configuration"></a>Yapılandırma
* [Koruma grubu oluşturulamıyor toocreate: hello sunucularının listesi alınırken bir hata oluştu.](http://blogs.technet.com/b/somaning/archive/2015/08/12/unable-to-create-the-protection-group-in-azure-site-recovery-portal.aspx)
* [Hyper-V konak kümesi en az bir statik ağ bağdaştırıcısı içeriyor veya hiçbir bağlı bağdaştırıcı DHCP yapılandırılmış toouse olan.](http://social.technet.microsoft.com/wiki/contents/articles/25498.hyper-v-host-cluster-contains-at-least-one-static-network-adapter-or-no-connected-adapters-are-configured-to-use-dhcp.aspx)
* [Sanal Makine Yöneticisi izinleri toocomplete bir eylem yok.](http://social.technet.microsoft.com/wiki/contents/articles/31110.vmm-does-not-have-permissions-to-complete-an-action.aspx)
* [Koruma yapılandırılırken hello abonelik içindeki Hello depolama hesabını seçemezsiniz.](http://social.technet.microsoft.com/wiki/contents/articles/32027.can-t-select-the-storage-account-within-the-subscription-while-configuring-protection.aspx)

### <a name="protection"></a>Koruma
* <span style="color:green;">Yeni</span> ["Koruma hello sanal makine için koruma yapılandırılamadı" hatası ile başarısız olan korumayı etkinleştir. Hata 60007, 40003.](http://social.technet.microsoft.com/wiki/contents/articles/32194.azure-site-recovery-enable-protection-failing-with-error-protection-couldn-t-be-configured-for-the-virtual-machine-error-60007-40003.aspx)
* <span style="color:green;">Yeni</span> ["Merhaba sanal makine için koruma etkinleştirilemedi." hatası ile başarısız olan korumayı etkinleştir Hata 70094.](http://social.technet.microsoft.com/wiki/contents/articles/32195.azure-site-recovery-enable-protection-failing-with-error-protection-couldn-t-be-enabled-for-the-virtual-machine-error-70094.aspx)
* <span style="color:green;">Yeni</span> [dinamik geçiş hata 23848 - hello sanal makine türü Canlı kullanılarak taşındı toobe geçiyor. Bu hello sanal makinenin hello kurtarma koruma durumunu bozar.](http://social.technet.microsoft.com/wiki/contents/articles/32021.live-migration-error-23848-the-virtual-machine-is-going-to-be-moved-using-type-live-this-could-break-the-recovery-protection-status-of-the-virtual-machine.aspx)
* [Aracı ana makinede yüklü değil bu yana korumayı etkinleştirme başarısız oldu.](http://social.technet.microsoft.com/wiki/contents/articles/31105.enable-protection-failed-since-agent-not-installed-on-host-machine.aspx)
* [Merhaba çoğaltma sanal makinesi için uygun bir konak - toolow işlem kaynakları bulunamıyor.](http://social.technet.microsoft.com/wiki/contents/articles/25501.a-suitable-host-for-the-replica-virtual-machine-can-t-be-found-due-to-low-compute-resources.aspx)
* [Merhaba çoğaltma sanal makinesi için uygun bir konak - toono mantıksal ağa bağlı bulunamıyor.](http://social.technet.microsoft.com/wiki/contents/articles/25502.a-suitable-host-for-the-replica-virtual-machine-can-t-be-found-due-to-no-logical-network-attached.aspx)
* [Toohello çoğaltma ana bilgisayar makinesi - bağlanamıyor bağlantı kurulamadı.](http://social.technet.microsoft.com/wiki/contents/articles/31106.cannot-connect-to-the-replica-host-machine-connection-could-not-be-established.aspx)

### <a name="recovery"></a>Kurtarma
* Sanal Makine Yöneticisi hello konak işlemini tamamlayamıyor:
  * [Sanal makine için seçilen toohello kurtarma noktası devreden: genel erişim reddedildi hatası.](http://social.technet.microsoft.com/wiki/contents/articles/25504.fail-over-to-the-selected-recovery-point-for-virtual-machine-general-access-denied-error.aspx)
  * [Hyper-V başarısız toofail toohello üzerinden seçili sanal makine için kurtarma noktası: işlem iptal edildi.  Daha yeni bir kurtarma noktası deneyin. (0x80004004).](http://social.technet.microsoft.com/wiki/contents/articles/25503.hyper-v-failed-to-fail-over-to-the-selected-recovery-point-for-virtual-machine-operation-aborted-try-a-more-recent-recovery-point-0x80004004.aspx)
  * Merhaba sunucusuyla bir bağlantı kurulan (0x00002EFD) bulunamadı.
    * [Hyper-V sanal makine için tooenable tersine çoğaltma başarısız oldu.](http://social.technet.microsoft.com/wiki/contents/articles/25505.a-connection-with-the-server-could-not-be-established-0x00002efd-hyper-v-failed-to-enable-reverse-replication-for-virtual-machine.aspx)
    * [Hyper-V sanal makinesi sanal makine için tooenable çoğaltma başarısız oldu.](http://social.technet.microsoft.com/wiki/contents/articles/25506.a-connection-with-the-server-could-not-be-established-0x00002efd-hyper-v-failed-to-enable-replication-for-virtual-machine-virtual-machine.aspx)
  * [Sanal makine için yük devretme kaydedilemedi.](http://social.technet.microsoft.com/wiki/contents/articles/25508.could-not-commit-failover-for-virtual-machine.aspx)
* [Merhaba kurtarma planı planlanan yük devretme için hazır olmayan sanal makineler içeriyor.](http://social.technet.microsoft.com/wiki/contents/articles/25509.the-recovery-plan-contains-virtual-machines-which-are-not-ready-for-planned-failover.aspx)
* [Merhaba sanal makine planlanmış yük devretme için hazır değil.](http://social.technet.microsoft.com/wiki/contents/articles/25507.the-virtual-machine-isn-t-ready-for-planned-failover.aspx)
* [Sanal makine çalışmıyorsa ve kapalı değil.](http://social.technet.microsoft.com/wiki/contents/articles/25510.virtual-machine-is-not-running-and-is-not-powered-off.aspx)
* [Bant dışı işlemi, bir sanal makine ve yürütme yük devretme işlemi başarısız oldu.](http://social.technet.microsoft.com/wiki/contents/articles/25507.the-virtual-machine-isn-t-ready-for-planned-failover.aspx)
* Yük devretme sınaması
  * [Test yük devretmesi sürüyor olduğundan, yük devretme başlatılamadı.](http://social.technet.microsoft.com/wiki/contents/articles/31111.failover-could-not-be-initiated-since-test-failover-is-in-progress.aspx)
* <span style="color:green;">Yeni</span> yük devretme zaman aşımına uğruyor 'PreFailoverWorkflow görevle WaitForScriptExecutionTaskTimeout' hello sanal makine veya hello alt toowhich hello makine ile ilişkilendirilmiş ağ güvenlik grubu hello toohello yapılandırma ayarları nedeniyle aittir. Çok başvuran['PreFailoverWorkflow görev WaitForScriptExecutionTaskTimeout'](https://aka.ms/troubleshoot-nsg-issue-azure-site-recovery) Ayrıntılar için.

### <a name="configuration-server-process-server-master-target"></a>Yapılandırma sunucusu, işlem sunucusu, ana hedef
* [Merhaba ESXi ana bilgisayar üzerinde hangi hello PS/CS VM olarak barındırılan renkli kilitlenme mor ekran ile başarısız olur.](http://social.technet.microsoft.com/wiki/contents/articles/31107.vmware-esxi-host-experiences-a-purple-screen-of-death.aspx)

### <a name="remote-desktop-troubleshooting-after-failover"></a>Uzak Masaüstü'nü yük devretme sonrasında sorun giderme
* Birçok müşteri sorunları tooconnect toohello azure'da sanal makine yük devredildi karşılaştığı. [Belge tooRDP hello sanal makinede sorun giderme kullanım hello](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

#### <a name="adding-a-public-ip-on-a-resource-manager-virtual-machine"></a>Bir kaynak yöneticisi sanal makinede bir genel IP ekleme
Merhaba, **Bağlan** hello portalda düğmesine görünüyorsa ve bir Express Route veya siteden siteye VPN bağlantısı üzerinden bağlı tooAzure olmayan, toocreate gerekir ve Uzaktan kullanmadan önce sanal makinenize genel bir IP adresi atayın. Masaüstü ve paylaşılan Kabuk. Genel IP hello sanal makinenin ağ arabirimi hello daha sonra ekleyebilirsiniz.  

![Genel IP üzerinde hello ağ arabirimi sanal makine eklenemedi](media/site-recovery-monitoring-and-troubleshooting/createpublicip.gif)
