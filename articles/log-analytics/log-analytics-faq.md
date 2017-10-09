---
title: aaaLog Analytics SSS | Microsoft Docs
description: "Hello Azure günlük analizi hizmeti hakkında sorular yanıtlar toofrequently."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: ad536ff7-2c60-4850-a46d-230bc9e1ab45
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 25931f521cbb6ec840184221c6c1a5794b3445f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-faq"></a>Log Analytics SSS
Bu Microsoft FAQ günlük analizi Microsoft Operations Management Suite (OMS) hakkında sık sorulan soruların listesidir. Ek günlük analizi hakkında sorularınız varsa, toohello gidin [tartışma Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights) ve sorularınızı gönderin. Sık sorulan bir soru, böylece hızla ve kolayca bulunabilir biz bunu toothis makale ekleyin.

## <a name="general"></a>Genel

### <a name="q-does-log-analytics-use-hello-same-agent-as-azure-security-center"></a>Q. Günlük analizi hello kullanmaz Azure Güvenlik Merkezi olarak aynı aracı?

A. Erken Haziran 2017 içinde hello Microsoft İzleme Aracısı toocollect ve deposu verileri kullanarak Azure Güvenlik Merkezi başlamıştır. toolearn daha, fazla [Azure Güvenlik Merkezi platformu geçiş ile ilgili SSS](../security-center/security-center-platform-migration-faq.md).

### <a name="q-what-checks-are-performed-by-hello-ad-and-sql-assessment-solutions"></a>Q. Hangi denetimleri hello AD ve SQL değerlendirmesi çözümleri tarafından yapılır?

A. Merhaba aşağıdaki sorgu şu anda gerçekleştirilen tüm denetimler açıklamasını gösterir:

```
(Type=SQLAssessmentRecommendation OR Type=ADAssessmentRecommendation) | dedup RecommendationId | select FocusArea, ActionArea, Recommendation, Description | sort Type, FocusArea,ActionArea, Recommendation
```

Merhaba sonuçları sonra daha fazla inceleme için dışarı aktarılan tooExcel olabilir.

### <a name="q-why-do-i-see-something-different-than-oms-in-system-center-operations-manager-console"></a>S: görmemin nedeni farklı bir şey *OMS* System Center Operations Manager konsolunda?

A: hangi güncelleştirme toplaması Operations, bulunduğunuz Yöneticisi'nin üzerinde bağlı olarak, bir düğüm için görebilirsiniz *System Center Advisor*, *operasyonel Öngörüler*, veya *günlük analizi*.

metin dizesini güncelleştirme çok hello*OMS* el ile içeri toobe gereken bir yönetim paketinde bulunur. toosee hello geçerli metin ve işlevsellik, hello son System Center Operations Manager güncelleştirme toplaması KB makalesi ve yenileme hello konsolda hello yönergeleri izleyin.

### <a name="q-is-there-an-on-premises-version-of-log-analytics"></a>S: yoktur bir *şirket içi* günlük analizi sürümü?

Y: No Günlük analizi işler ve büyük miktarlarda veri depolar. Bir bulut hizmeti günlük analizi yapabilir tooscale yukarı gerekirse olduğu ve herhangi bir performans etkisi tooyour ortam kaçının.

Ek avantajları şunlardır:
- Maliyetleri kaydetme hello günlük analizi altyapısı, Microsoft çalışır
- Normal dağıtım özelliği güncelleştirmeler ve düzeltmeler.

### <a name="q-how-do-i-troubleshoot-that-log-analytics-is-no-longer-collecting-data"></a>Q. Günlük analizi artık veri toplama nasıl giderebilirim?

A: Merhaba fiyatlandırma katmanı boş olan ve birden fazla veri 500 MB günde göndermiş varsa, veri toplama hello gün hello kalanı için durur. Ulaşması hello günlük sınır olan günlük analizi veri toplamayı durdurur karşılaşılan bir nedeni ya da veri görünür toobe eksik.

Günlük analizi oluşturur olay türü *işlemi* ne zaman veri toplamayı başlatır ve durdurur. 

Merhaba günlük sınır ulaşmak ve verileri eksik arama toocheck sorguda aşağıdaki hello çalıştırın:`Type=Operation OperationCategory="Data Collection Status"`

Veri toplama durduğunda, hello *OperationStatus* olan **uyarı**. Veri toplama başladığında hello *OperationStatus* olan **başarılı**. 

Merhaba aşağıdaki tabloda açıklanmaktadır veri toplamayı durdurur nedenler ve önerilen eylem tooresume veri toplama:

| Neden veri toplamayı durdurur                       | tooresume veri toplama |
| -------------------------------------------------- | ----------------  |
| Boş veri günlük sınırına<sup>1</sup>       | Koleksiyon tooautomatically yeniden başlatma, günlük aşağıdaki hello kadar bekleyin veya<br> Fiyatlandırma katmanı değişikliği tooa Ücretli |
| Azure aboneliği nedeniyle askıya alınmış durumda olduğundan: <br> Ücretsiz deneme sürümü sona erdi <br> Azure geçiş süresi <br> Aylık harcama sınırı (örneğin bir MSDN veya Visual Studio abonelikte) ulaşıldı                          | Ücretli aboneliği tooa Dönüştür <br> Ücretli aboneliği tooa Dönüştür <br> Sınırı kaldırın veya sınırı sıfırlar kadar bekleyin |

<sup>1</sup> çalışma alanınızı hello fiyatlandırma katmanı boş ise, sınırlı toosending gün toohello hizmeti başına veri 500 MB. Merhaba Günlük sınıra ulaştığınızda, hello sonraki güne kadar veri toplamayı durdurur. Veri toplama durdurulduğunda gönderilen veriler dizinli değil ve arama amacıyla kullanılamıyor. Veri toplama çıktığında işleme gönderilen yalnızca yeni verileri oluşur. 

Günlük analizi UTC saati kullanır ve her gün UTC gece yarısı başlar. Merhaba çalışma hello günlük sınır ulaşırsa, işleme hello ilk saatlik hello UTC bir sonraki gün sırasında sürdürür.

### <a name="q-how-can-i-be-notified-when-data-collection-stops"></a>Q. Veri toplama durduğunda nasıl bildirim?

A: açıklanan başlangıç adımları kullanın [bir uyarı kuralı oluştur](log-analytics-alerts-creating.md#create-an-alert-rule) toobe bildirim veri toplama durduğunda.

Veri toplama durduğunda hello uyarıyı oluştururken ayarlayın:
- **Ad** çok*veri toplama durdu*
- **Önem derecesi** çok*uyarı*
- **Arama sorgusu** çok`Type=Operation OperationCategory="Data Collection Status" OperationStatus=Warning`
- **Zaman penceresi** çok*2 saat*.
- **Uyarı sıklığı** toobe bir hello kullanım verileri yalnızca saatte bir kez güncelleştiren bir işlem olduğundan saat.
- **Temel uyarı Oluştur** toobe *sonuçları sayısı*
- **Sonuç sayısı** toobe *0'dan büyük*

Açıklanan başlangıç adımları kullanın [Eylemler tooalert kuralları eklemeniz](log-analytics-alerts-actions.md) hello uyarı kuralı için bir e-posta, Web kancası veya runbook eylemi yapılandırın.


## <a name="configuration"></a>Yapılandırma
### <a name="q-can-i-change-hello-name-of-hello-tableblob-container-used-tooread-from-azure-diagnostics-wad"></a>Q. Azure tanılama (WAD) hello tablo/blob kapsayıcı kullanılan tooread hello adını değiştirebilir miyim?

A. Hayır, şu anda olası tooread rasgele tablolar veya kapsayıcıları Azure depolama alanında değil.

### <a name="q-what-ip-addresses-does-hello-log-analytics-service-use-how-do-i-ensure-that-my-firewall-only-allows-traffic-toohello-log-analytics-service"></a>Q. Hangi IP adresleri günlük analizi hizmeti kullanım hello? Duvarım yalnızca trafik toohello günlük analizi hizmeti verir nasıl emin olursunuz?

A. Merhaba günlük analizi hizmeti, Azure üzerinde oluşturulmuştur. Günlük analizi IP adresleridir hello [Microsoft Azure veri merkezi IP aralıkları](http://www.microsoft.com/download/details.aspx?id=41653).

Hizmet dağıtımları yapıldığı gibi hello günlük analizi hizmeti hello gerçek IP adreslerini değiştirin. Merhaba DNS adlarını tooallow, güvenlik duvarı üzerinden adresindeki belgelenmiştir [günlük analizi proxy ve güvenlik duvarı ayarlarını yapılandırma](log-analytics-proxy-firewall.md).

### <a name="q-i-use-expressroute-for-connecting-tooazure-does-my-log-analytics-traffic-use-my-expressroute-connection"></a>Q. I tooAzure bağlamak için ExpressRoute kullanın. My günlük analizi trafik ExpressRoute bağlantım kullanıyor mu?

A. Merhaba farklı ExpressRoute trafik türlerini hello açıklanan [ExpressRoute belgeleri](../expressroute/expressroute-faqs.md#supported-services).

Trafik tooLog Analytics hello genel eşliği expressroute bağlantı hattı kullanır.

### <a name="q-is-there-a-simple-and-easy-way-toomove-an-existing-log-analytics-workspace-tooanother-log-analytics-workspaceazure-subscription"></a>Q. Basit ve kolay bir yol toomove var olan bir günlük analizi çalışma alanı tooanother günlük analizi çalışma alanı/Azure abonelik var?

A. Merhaba `Move-AzureRmResource` cmdlet günlük analizi çalışma alanı ve aynı zamanda bir Otomasyon hesabı bir Azure aboneliği tooanother taşımanıza olanak tanır. Daha fazla bilgi için bkz: [taşıma AzureRmResource](http://msdn.microsoft.com/library/mt652516.aspx).

Bu değişiklik ayrıca hello Azure portal yapılabilir.

Bir günlük analizi çalışma alanı tooanother veri taşınamıyor veya günlük analizi veri depolanan hello bölgeyi değiştirin.

### <a name="q-how-do-i-add-log-analytics-toosystem-center-operations-manager"></a>S: günlük analizi tooSystem Center Operations Manager nasıl eklenir?

Y: toohello en son güncelleştirme paketini güncelleştirme ve yönetim paketlerini içeri tooconnect Operations Manager tooLog analizi sağlar.

>[!NOTE]
>Merhaba Operations Manager bağlantısı tooLog Analytics yalnızca System Center Operations Manager 2012 SP1 ve sonraki sürümleri için kullanılabilir.

### <a name="q-how-can-i-confirm-that-an-agent-is-able-toocommunicate-with-log-analytics"></a>S: bir aracı günlük analizi ile mümkün toocommunicate olduğunu nasıl doğrulayabilirsiniz?

Y: tooensure bu hello aracı iletişim kurabilir OMS ile gidin: Denetim Masası, güvenlik ve ayarları, **Microsoft İzleme Aracısı**.

Merhaba altında **Azure günlük analizi (OMS)** sekmesinde, yeşil bir onay işareti için bakın. Yeşil onay işareti simgesi bu hello aracı mümkün toocommunicate hello OMS hizmetine sahip olduğunu doğrular.

Sarı bir uyarı simgesi hello Aracısı OMS ile iletişim sorunları yaşıyor anlamına gelir. Bir ortak hello Microsoft İzleme Aracısı Hizmeti durdu nedeni. Hizmet Denetimi Yöneticisi toorestart hello hizmeti kullanın.

### <a name="q-how-do-i-stop-an-agent-from-communicating-with-log-analytics"></a>S: günlük analizi ile iletişim kurmasını bir aracı nasıl Durdur?

A: System Center Operations Manager'da, hello bilgisayar hello Advisor yönetilen bilgisayar listesinden kaldırın. Operations Manager güncelleştirmelerini hello Aracısı toono uzun rapor tooLog Analytics yapılandırmasını hello. Aracıları tooLog Analytics doğrudan bağlı için bunları aracılığıyla iletişim kurmasını durdurabilirsiniz: Denetim Masası, güvenlik ve ayarları, **Microsoft İzleme Aracısı**.
Altında **Azure günlük analizi (OMS)**, listelenen tüm çalışma alanlarını kaldırın.

### <a name="q-why-am-i-getting-an-error-when-i-try-toomove-my-workspace-from-one-azure-subscription-tooanother"></a>Toomove my çalışma alanından bir Azure aboneliği tooanother çalıştığımda neden bir hata alıyorum?

A: hello Azure portal kullanıyorsanız, çalışma alanı hello hello taşıma için seçili olduğundan emin olun. Merhaba çalışma taşındıktan sonra otomatik olarak taşır hello çözümleri--seçmeyin. 

Her iki Azure aboneliklerini izninizin olduğundan emin olun.

## <a name="agent-data"></a>Aracı verileri
### <a name="q-how-much-data-can-i-send-through-hello-agent-toolog-analytics-is-there-a-maximum-amount-of-data-per-customer"></a>Q. Ne kadar veri hello Aracısı tooLog Analytics gönderebilirim? Yüksek miktarda verinin müşteri başına var mı?
A. Hello ücretsiz planı çalışma alanı bir günlük sınır 500 MB'lık ayarlar. Merhaba standart ve premium planları sınır hello karşıya veri miktarına sahip. Günlük analizi bir bulut hizmeti olarak tasarlanmıştır tooautomatically ölçek büyütme toohandle hello birim günde terabayt olsa bile, müşteriden – geliyor.

Merhaba günlük analizi aracı küçük bir yer olan tasarlanmış tooensure oluştu. Müşterilerimizin birini bizim aracısı ve oldukları nasıl devam etmesini karşı gerçekleştirilen hello testleri hakkında bir blog yazıldı. Merhaba veri birimi etkinleştirmeniz hello çözümleri göre değişir. Merhaba veri birimi ile ilgili ayrıntılı bilgiler bulmak ve hello çözümde tarafından hello paketlerdeki bkz [kullanım](log-analytics-usage.md) sayfası.

Daha fazla bilgi için okuduğunuz bir [müşteri blog](http://thoughtsonopsmgr.blogspot.com/2015/09/one-small-footprint-for-server-one.html) hello az alan kaplaması hello OMS Aracısı'nın hakkında.

### <a name="q-how-much-network-bandwidth-is-used-by-hello-microsoft-management-agent-mma-when-sending-data-toolog-analytics"></a>Q. Ne kadar ağ bant genişliği, veri tooLog Analytics gönderirken hello Microsoft Yönetim Aracısı'nı (MMA) tarafından kullanılıyor?

A. Bant genişliği hello gönderilen veri miktarını üzerinde bir işlevdir. Merhaba ağ üzerinden gönderilen veri sıkıştırılır.

### <a name="q-how-much-data-is-sent-per-agent"></a>Q. Ne kadar veri her aracı gönderilir?

A. Her aracı için gönderilen veri miktarını Hello bağlıdır:

* etkinleştirdiğiniz hello çözümleri
* toplanmakta olan Hello sayısı günlüklerini ve performans sayaçları
* Hello hello günlüklerine veri hacmi

Merhaba ücretsiz fiyatlandırma katmanı en iyi yolu tooonboard birkaç sunucuya olan ve hello tipik veri birimi ölçer. Genel kullanım hello üzerinde gösterilen [kullanım](log-analytics-usage.md) sayfası.

Mümkün toorun hello WireData aracı olan bilgisayarlar için ne kadar veri gönderilen sorgu toosee aşağıdaki hello kullan:

```
Type=WireData (ProcessName="C:\\Program Files\\Microsoft Monitoring Agent\\Agent\\MonitoringHost.exe") (Direction=Outbound) | measure Sum(TotalBytes) by Computer
```



## <a name="next-steps"></a>Sonraki adımlar
* [Günlük Analytics ile çalışmaya başlama](log-analytics-get-started.md) toolearn günlük analizi ve get dakika içinde çalışır durumda hakkında daha fazla bilgi.
