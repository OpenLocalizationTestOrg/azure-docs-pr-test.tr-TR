---
title: "aaaAzure Güvenlik Merkezi sorun giderme kılavuzu | Microsoft Docs"
description: "Bu belge Azure Güvenlik Merkezi'nde tootroubleshoot sorunları yardımcı olur."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 44462de6-2cc5-4672-b1d3-dbb4749a28cd
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 78b3c49eb66fe3a4f80efbba3a47a87b039c07ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-troubleshooting-guide"></a>Azure Güvenlik Merkezi Sorun Giderme Kılavuzu
Bu kılavuz, tootroubleshoot Güvenlik Merkezi ile ilgili sorunlarla bilgi teknolojisi (BT) uzmanları, bilgi güvenlik Çözümleyicileri ve, kuruluşlarının Azure Güvenlik Merkezi kullanıyor ve bulut yöneticileri içindir.

>[!NOTE] 
>Güvenlik Merkezi erken Haziran 2017'den itibaren hello Microsoft İzleme Aracısı toocollect ve depolama verileri kullanır. Bkz: [Azure Güvenlik Merkezi platformu geçiş](security-center-platform-migration.md) toolearn daha fazla. Bu makaledeki Hello bilgiler geçiş toohello sonra Microsoft İzleme Aracısı Güvenlik Merkezi işlevlerini temsil eder.
>

## <a name="troubleshooting-guide"></a>Sorun giderme kılavuzu
Bu kılavuz, tootroubleshoot Güvenlik Merkezi sorunları nasıl ilişkilendirileceğini açıklar. Güvenlik Merkezi'nde bitti hello sorun giderme çoğu kurulur hello bakarak [denetim günlüğü](https://azure.microsoft.com/updates/audit-logs-in-azure-preview-portal/) hello kayıtlarını bileşeni başarısız oldu. Denetim günlükleri ile aşağıdakileri belirleyebilirsiniz:

* Hangi işlemlerin gerçekleştirildiği
* Merhaba işlemi kimin başlattığını
* Ne zaman hello işlemi oluştu
* Merhaba işlem Hello durumu
* Merhaba işlemi yardımcı olabilecek diğer özelliklerin değerlerine Hello araştırma

okuma işlemleri (GET) içermez ancak hello denetim günlüğü kaynaklarınız üzerinde gerçekleştirilen tüm yazma işlemlerini (PUT, POST, DELETE) içerir.

## <a name="microsoft-monitoring-agent"></a>Microsoft Monitoring Agent
Güvenlik Merkezi, Microsoft Monitoring Agent hello kullanır – hello Operations Management Suite ve günlük analizi hizmeti – toocollect güvenlik verileri, Azure sanal makineler tarafından kullanılan aynı aracı hello budur. Veri toplama etkinleştirilir ve hello Aracısı doğru hello hedef makinede kurduktan sonra aşağıdaki hello işlemi yürütme olmalıdır:

* HealthService.exe

Merhaba Hizmetleri Yönetim Konsolu (services.msc) açarsanız, aşağıda gösterildiği gibi de hello Microsoft İzleme Aracısı hizmeti çalışıyor görürsünüz:

![Hizmetler](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig5.png)

hello Aracısı'nın hangi sürümü kullandığınız toosee açmak **Görev Yöneticisi'ni**, hello içinde **işlemleri** sekmesini bulmak hello **Microsoft İzleme Aracısı hizmeti**, üzerinde sağ tıklayın ve tıklatın **özellikleri**. Merhaba, **ayrıntıları** sekmesinde, aşağıda gösterildiği gibi hello dosya sürümü bakın:

![Dosya](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig6.png)
   

## <a name="microsoft-monitoring-agent-installation-scenarios"></a>Microsoft Monitoring Agent yükleme senaryoları
Merhaba Microsoft İzleme Aracısı, bilgisayarınızda yüklerken farklı sonuçlar üretebilir iki yükleme senaryosunda vardır. desteklenen hello senaryolar şunlardır:

* **Güvenlik Merkezi tarafından otomatik olarak yüklenen aracı**: Bu senaryoda konumları, Güvenlik Merkezi ve günlük arama yapabilir tooview hello uyarıları olacaktır. Merhaba abonelik hello kaynağın ait olduğu için hello güvenlik ilkesinde yapılandırılan e-posta bildirimleri toohello e-posta adresi alırsınız.
.
* **Aracı el ile bir VM'de yüklü bulunan Azure'da**: kullanıyorsanız bu senaryoda, aracıları el ile önceki tooFebruary 2017 yüklenip, yalnızca üzerinde hello filtre uygularsanız hello Güvenlik Merkezi Portal'da mümkün tooview hello uyarılarını olacaktır Abonelik hello çalışma ait. Merhaba abonelik hello kaynak filtreye, ait olduğu durumda mümkün toosee herhangi bir uyarı olmayacaktır. Merhaba abonelik hello çalışma ait olduğu için hello güvenlik ilkesinde yapılandırılan e-posta bildirimleri toohello e-posta adresi alırsınız.

>[!NOTE]
> Hello ikinci olarak, açıklanan tooavoid hello davranışı hello hello Aracısı'nın en son sürümü karşıdan emin olun.
> 

## <a name="troubleshooting-monitoring-agent-network-requirements"></a>Monitoring agent ağ gereksinimi sorunlarını giderme
Başlangıç bağlantı noktası numaraları ve etki alanı URL'leri dahil toonetwork erişimine, aracıları tooconnect tooand kaydolun Güvenlik Merkezi ile olmaları gerekir.

- Proxy sunucuları için uygun proxy sunucu kaynakları Aracısı ayarlarında yapılandırılan hello tooensure gerekir. Daha fazla bilgi için bu makaleyi okuyun [nasıl toochange hello proxy ayarlarını](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-windows-agents#configure-proxy-settings).
- Erişim toohello Internet kısıtlamak, güvenlik duvarları için güvenlik duvarı toopermit erişim tooOMS tooconfigure gerekir. Aracı ayarlarında bir işlem yapılması gerekmez.

Aşağıdaki tablonun hello iletişimi için gerekli kaynakları gösterir.

| Aracı Kaynağı | Bağlantı Noktaları | HTTPS denetlemesini atlama |
|---|---|---|
| *.ods.opinsights.azure.com | 443 | Evet |
| *.oms.opinsights.azure.com | 443 | Evet |
| *.blob.core.windows.net | 443 | Evet |
| *.azure-automation.net | 443 | Evet |

Merhaba aracıyla ekleme sorunlarla karşılaşırsanız, emin tooread hello makale olun [nasıl tootroubleshoot Operations Management Suite ekleme sorunları](https://support.microsoft.com/en-us/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues).


## <a name="troubleshooting-endpoint-protection-not-working-properly"></a>Uç nokta korumasıyla ilgili sorunları giderme işlemi düzgün çalışmıyor

Merhaba Konuk aracısı olan her şeyi hello üst işlemi hello [Microsoft Antimalware](../security/azure-security-antimalware.md) uzantı vermiyor. Merhaba Konuk Aracısı işlemi başarısız olduğunda, hello hello Konuk Aracısı bir alt işlem olarak çalışır Microsoft Antimalware de başarısız.  Bu gibi senaryolarda önerilen tooverify hello seçenekleri takip ediyor:

- Hello VM özel görüntü hedefidir ve hello Oluşturucusu hello VM, hiçbir zaman Konuk aracısı yüklü değilse.
- Merhaba hedef sonra bir Linux VM hello kötü amaçlı yazılımdan koruma uzantısı'nın hello Windows sürümünü yükleme Windows VM yerine bir Linux VM ise başarısız olur. Merhaba Linux Konuk Aracısı işletim sistemi sürümü ve gerekli paketleri açısından özel gereksinimleri vardır ve bu gereksinimleri karşılanmadı hello VM aracısı yok ya da çalışmaz. 
- Merhaba VM Konuk aracısının eski bir sürümüyle oluşturulduysa. Olduysa, bazı eski aracıları otomatik kendisini toohello daha yeni sürümü güncelleştirme değil ve bu toothis sorunu neden olduğunu aklınızda bulundurun. Her zaman kendi görüntülerinizden oluşturuyorsanız hello Konuk Aracısı en son sürümünü kullanın.
- Bazı üçüncü taraf yönetim yazılımı hello Konuk aracısını devre dışı veya erişim toocertain dosya konumları engelleyin. Üçüncü taraf, VM'de yüklü varsa, bu hello aracı hello dışlama listesinde olduğundan emin olun.
- Belirli güvenlik duvarı ayarları veya ağ güvenlik grubu (NSG) Konuk Aracısı gelen ağ trafiğini tooand engelleyebilir.
- Belirli bir Erişim Denetimi Listesi (ACL) disk erişimini engelleyebilir.
- Disk alanı yetersizliği hello Konuk aracısının düzgün çalışmasını engelleyebilir. 

Microsoft kötü amaçlı yazılımdan koruma kullanıcı arabirimini devre dışı varsayılan hello tarafından okuma [etkinleştirme Microsoft kötü amaçlı yazılımdan koruma kullanıcı arabiriminde Azure Kaynak Yöneticisi Vm'leri dağıtım sonrası](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/09/enabling-microsoft-antimalware-user-interface-post-deployment/) hakkında daha fazla bilgi için tooenable, gerekiyorsa.

## <a name="troubleshooting-problems-loading-hello-dashboard"></a>Merhaba Pano yükleme sorunlarını giderme

Merhaba Güvenlik Merkezi panosunu yüklenirken sorunlarla karşılaşırsanız, hello abonelik tooSecurity Merkezi (yani hello ilk kullanıcı hello abonelikle Güvenlik Merkezi açan) kaydeder, hello kullanıcı emin olun ve tooturn ister misiniz hello kullanıcının veri toplama olmalıdır *sahibi* veya *katkıda bulunan* hello abonelikte. Ayrıca kullanıcılar ile o andan *okuyucu* hello üzerinde abonelik hello Pano/uyarıları/öneri/İlkesi görebilirsiniz.

## <a name="contacting-microsoft-support"></a>Microsoft Destek ile iletişim kurma
Bu makalede sağlanan hello yönergeleri kullanarak bazı sorunlar tanımlanabilir, diğerleri de bulabilir hello Güvenlik Merkezi ortak belgelenen [Forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureSecurityCenter). Ancak, daha fazla sorun giderme bilgisi gerekirse, **Azure portalında** aşağıda gösterildiği gibi yeni bir destek isteği oluşturabilirsiniz: 

![Microsoft Destek](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig2.png)


## <a name="see-also"></a>Ayrıca bkz.
Bu belgede, nasıl öğrenilen Azure Güvenlik Merkezi'nde güvenlik ilkelerini tooconfigure. Azure Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi planlama ve işlemler Kılavuzu](security-center-planning-and-operations-guide.md) — öğrenin nasıl tooplan ve hello tasarım konuları tooadopt Azure Güvenlik Merkezi anladığınızdan emin olun.
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) — nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) — öğrenin nasıl toomanage ve yanıt toosecurity uyarıları
* [Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) — nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) — hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz
* [Azure Güvenlik Blogu](http://blogs.msdn.com/b/azuresecurity/) - Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz

