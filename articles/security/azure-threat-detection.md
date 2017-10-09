---
title: "aaaAzure Gelişmiş tehdit algılama | Microsoft Docs"
description: "Kimlik koruması ve yeteneklerini öğrenin."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: 63e2c541fd4ce2c571af9d5845c9a9bd4b03b2a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-advanced-threat-detection"></a>Azure Gelişmiş tehdit algılama
## <a name="introduction"></a>Giriş

### <a name="overview"></a>Genel Bakış

Microsoft teknik incelemeler, güvenlik genel bakışlar, en iyi yöntemler ve denetim listeleri tooassist Azure bir dizi geliştirilen müşterilerinden hello çeşitli çevresindeki hello Azure platformu ve güvenlikle ilgili özellikleri kullanılabilir. Merhaba konuları avantajlarına ve derinliği bakımından aralığı ve düzenli aralıklarla güncelleştirilir. Bu belge, soyut bölümden hello özetlendiği gibi serisi bir parçası değil.

### <a name="azure-platform"></a>Azure platformu

Azure hello İlkler seçimi programlama dilleri, çerçeveleri, Araçlar, veritabanları ve aygıtları işletim sistemlerini destekler genel bulut hizmeti platformudur.
Programlama dilleri aşağıdaki hello destekler:
-   Linux kapsayıcıları Docker Tümleştirmesi ile çalıştırın.
-   JavaScript, Python, .NET, PHP, Java ve Node.js ile uygulamalar oluşturma
-   Yapı geri-iOS, Android ve Windows cihazları sona erer.

Azure genel bulut Hizmetleri, geliştiriciler ve BT uzmanları, aynı teknolojileri milyonlarca zaten kullanır ve güven hello destekler.

Bir kuruluşla tooa genel bulut geçirirken bu kuruluş verilerinizi sorumlu tooprotect olduğundan ve güvenlik ve idare hello sistem geçici sağlayın.

Azure'nın altyapı hello tesis tooapplications aynı anda milyonlarca müşteri barındırmak için gelen tasarlanmıştır ve güvenlik gereksinimlerine bağlı işletmeler karşılayabilecek güvenilir bir temel sağlar. Azure güvenlik toomeet hello gereksinimleri uygulama dağıtımlarını özelleştirme ve çok çeşitli seçenekler tooconfigure sağlar. Bu belge, bu gereksinimleri karşılayan yardımcı olur.

### <a name="abstract"></a>Özet

Microsoft Azure teklifleri Hizmetleri aracılığıyla Gelişmiş tehdit algılama işlevselliği yerleşik Azure Active Directory, Azure Operations Management Suite (OMS) ve Azure Güvenlik Merkezi gibi. Bu koleksiyon güvenlik hizmetlerini ve özellikleri, Azure dağıtımlarınızı içinde neler olduğunu basit ve hızlı şekilde toounderstand sağlar.

Bu teknik incelemede, hello "Microsoft Azure yaklaşımlar" tehdit güvenlik açığı tanılama yardımcı olur ve hello risk analiz sunucuları ve diğer Azure kaynaklarına karşı hedeflenen hello kötü amaçlı etkinliği ile ilişkili. Çözümleri hello Azure platformu, Müşteri'e dönük güvenlik hizmetleri ve teknolojileri ile güvenlik açığı yönetimi en iyi duruma getirilmiş ve bu tooidentify hello yöntemleri tanımı yardımcı olur.

Bu teknik incelemede Azure platformu ve müşteri dönük denetimlerin hello teknolojisine odaklanır ve tooaddress fiyatlandırma modelleri ve DevOps yöntem değerlendirmeleri SLA denemez.

## <a name="azure-active-directory-identity-protection"></a>Azure Active Directory Kimlik Koruması

![Azure Active Directory Kimlik Koruması](./media/azure-threat-detection/azure-threat-detection-fig1.png)


[Azure Active Directory kimlik koruması](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection) hello özelliğidir [Azure AD Premium P2](https://docs.microsoft.com/azure/active-directory/active-directory-editions) hello risk olaylarına ve olası güvenlik açıklarını kuruluşunuzun etkileyen genel bir bakış sağlar edition kimlikler. İçin bulut tabanlı kimlikleri on Microsoft güvenliğini sağlama ve Azure AD kimlik koruması ile Microsoft kullanılabilir tooenterprise müşteriler bu aynı koruma sistemleri yapılmasıdır. Kimlik koruması kullanan mevcut Azure AD anomali algılama özellikleri aracılığıyla kullanılabilen [Azure AD anormal etkinlik raporları](https://docs.microsoft.com/azure/active-directory/active-directory-view-access-usage-reports#anomalous-activity-reports)ve gerçek zamanlı anormallikleri algılayabilir yeni risk olayı türleri sunar.

Kimlik koruması Uyarlamalı machine learning algoritmaları ve buluşsal yöntemler toodetect anormallikleri ve bir kimlik tehlikede olduğunu gösterebilecek risk olaylarını kullanır. Bu verileri kullanarak, kimlik koruması raporları ve tooinvestigate etkinleştirmek uyarıları bu risk olaylar oluşturur ve gerekli düzeltme veya azaltma adımları uygulayın.

Ancak Azure Active Directory kimlik koruması birden çok bir izleme ve raporlama aracıdır. Risk olaylarına bağlı olarak, her kullanıcı için bir kullanıcı risk düzeyi kimlik koruması hesaplar, sağlayarak tooautomatically korumak tooconfigure risk tabanlı ilkeleri, kuruluşunuzun kimlikleri hello.

Bu riski tabanlı ilkeleri toplama tooother [koşullu erişim denetimleri](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) Azure Active Directory tarafından sağlanan ve [EMS](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access), otomatik olarak engelleyebilir veya dahil Uyarlamalı düzeltme eylemleri sunar parola sıfırlama ve çok faktörlü kimlik doğrulaması zorlama.

### <a name="identity-protections-capabilities"></a>Identity Protection'ın özellikleri

Azure Active Directory kimlik koruması izleme ve Raporlama Aracı büyük. tooprotect kuruluşunuzdaki kimlikleri, belirtilen risk düzeyi erişildiğinde toodetected sorunları otomatik olarak yanıt veren risk tabanlı ilkeleri yapılandırabilirsiniz. Bu ilkeler ayrıca tooother koşullu erişim kontrolü Azure Active Directory ve EMS tarafından sağlanan, otomatik olarak engellemek ya da parola sıfırlama ve çok faktörlü kimlik doğrulaması zorlama gibi uyarlamalı düzeltme eylemleri başlatmak.

Hesaplarınızı Azure kimlik koruması yardımcı olabilecek hello yollardan bazılarını örnekleri güvenli ve kimlikler şunları içerir:

[Algılama risk olaylarına ve riskli hesapları:](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#detection)
-   Machine learning ve buluşsal kurallarını kullanarak altı risk olayı türleri algılama
-   Kullanıcı risk düzeyleri hesaplama
-   Özel öneriler tooimprove sağlayan güvenlik açıkları vurgulama tarafından genel güvenlik duruşunu

[Risk olaylarını araştırma:](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#investigation)
-   Risk olayları için bildirimleri gönderme
-   Risk olaylarını ilgili ve bağlamsal bilgileri kullanarak araştırma
-   Tootrack araştırmalar temel iş akışı sağlama
-   Parola sıfırlama gibi tooremediation eylemleri kolay erişim sağlama

[Risk bağlı olarak koşullu erişim ilkeleri:](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#risky-sign-ins)
-   İlke toomitigate riskli gerçekleştirilen oturum açma tarafından gerçekleştirilen oturum açma engelleme veya çok faktörlü kimlik doğrulaması zorluklarını gerektirerek.
-   İlke tooblock veya güvenli riskli kullanıcı hesapları
-   Çok faktörlü kimlik doğrulama İlkesi toorequire kullanıcılar tooregister

### <a name="azure-ad-privileged-identity-management-pim"></a>Azure AD Privileged Identity Management (PIM)

İle [Azure Active Directory (AD) Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure),

![Azure AD Privileged Identity Management](./media/azure-threat-detection/azure-threat-detection-fig2.png)

yönetin, denetleyin ve erişimi kuruluşunuz içinde izleyin. Bu erişim tooresources Azure AD'de ve Office 365 veya Microsoft Intune gibi diğer Microsoft online services içerir.

Azure AD Privileged Identity Management yardımcı olur:

-   Bir uyarı alırsınız ve Azure AD Yöneticiler ve "tam zamanında" yönetimsel erişimi tooMicrosoft Office 365 ve Intune gibi çevrimiçi hizmetlere raporlama

-   Yönetici erişim geçmişine ve değişiklikler hakkında raporlar yönetici atamaları alma

-   Erişim tooa ayrıcalıklı rol hakkında uyarı alın

## <a name="microsoft-operations-management-suite-oms"></a>Microsoft Operations Management Suite (OMS)

[Microsoft Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) , yönetmek ve şirket içi korumak ve bulut altyapısı yardımcı olan Microsoft'un bulut tabanlı BT yönetimi çözümüdür. OMS, bulut tabanlı bir hizmet olarak uygulandığından altyapı hizmetlerine en az yatırımla onu kısa süre içinde çalışır duruma getirebilirsiniz. Yeni güvenlik özellikleri, devam eden bakım kaydetme otomatik olarak teslim edilir ve maliyetleri yükseltin.

Ayrıca kendi, OMS tooproviding değerli Services'de System Center bileşenleriyle gibi tümleştirebilirsiniz [System Center Operations Manager](https://blogs.technet.microsoft.com/cbernier/2013/10/23/monitoring-windows-azure-with-system-center-operations-manager-2012-get-me-started/) tooextend, varolan güvenlik yönetimi yatırımlarınızı hello bulut. System Center ve OMS tam karma Yönetimi deneyimini tooprovide birlikte çalışabilir.

### <a name="holistic-security-and-compliance-posture"></a>Bütünsel güvenlik ve uyumluluk duruş

Merhaba [OMS güvenlik ve Denetim Panosu](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) kuruluşunuzun kapsamlı bir görünüme sağlar BT güvenlik tutumunu dikkat etmeniz gereken önemli sorunlar için yerleşik arama sorguları. Merhaba güvenlik ve Denetim Panosu, OMS toosecurity hello giriş ekranı her şey için ilgili ' dir. Bilgisayarlarınızı hello güvenlik durumunu üst düzey bir anlayış sağlar. Son 24 saat, 7 gün hello tüm olayları veya diğer özel zaman çerçevesi ayrıca hello özelliği tooview içerir.

OMS panolar Yardım hızla ve kolayca anlamak hello tüm BT işlemleri dahil olmak üzere, Merhaba içeriğine içinde herhangi bir ortamın genel güvenlik duruşunu: yazılım güncelleştirme değerlendirme, kötü amaçlı yazılımdan koruma değerlendirmesi ve yapılandırma temellerini. Ayrıca, güvenlik günlüğü verilerini erişilmeye toostreamline hello güvenlik ve uyumluluk denetim işlemleri.

Merhaba OMS güvenlik ve Denetim Panosu dört ana kategoride düzenlenmiştir:

![OMS Güvenlik ve Denetim panosu](./media/azure-threat-detection/azure-threat-detection-fig3.jpg)

-   **Güvenlik etki alanları:** Bu alanda sunulan mümkün toofurther olacaktır zaman içindeki güvenlik kayıtları keşfetmek, erişim kötü amaçlı yazılım değerlendirmesi, değerlendirme, ağ güvenliği, kimlik ve erişim bilgileri, bilgisayarları güvenlik olayları ile güncelleştirin ve hızlı bir şekilde sahip erişim tooAzure Güvenlik Merkezi panosunu.

-   **Önem düzeyindeki sorunlar:** tooquickly sayesinde bu seçeneği etkin sorunlar hello sayısını tanımlamak ve hello bu sorunların önem derecesi.

-   **Algılama (Önizleme):** kaynaklarınızı karşı yer alırken güvenlik uyarıları görselleştirme tooidentify saldırı desenleri sağlar.

-   **Tehdit bilgileri:** hello sayısı toplam giden kötü amaçlı IP trafiğinin, hello kötü amaçlı tehdit türünü ve burada bu IP'leri geliyor gelen gösteren bir harita sunucularıyla görselleştirme tarafından tooidentify saldırı desenleri sağlar.

-   **Genel güvenlik sorgular:** bu seçenek, hello en yaygın güvenlik listesini sorgular ortamınızı toomonitor kullanabileceğiniz sağlar. Bu sorguların birine tıkladığınızda, bu sorgu için hello sonuçlarla hello arama dikey penceresinde açar.

### <a name="insight-and-analytics"></a>Insight and Analytics
Merhaba ortada bulunan [günlük analizi](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) hello Azure bulut barındırılan hello OMS deposu.

![Insight and Analytics](./media/azure-threat-detection/azure-threat-detection-fig4.png)

Verileri hello depoya yapılandırma veri kaynakları ve ekleme çözümleri tooyour abonelik tarafından bağlı kaynaklardan toplanır.

![aboneliği](./media/azure-threat-detection/azure-threat-detection-fig5.png)

Veri kaynakları ve çözümleri her kendi özellikleri vardır, ancak hala birlikte sorguları toohello deposunda analiz farklı kayıt türleri oluşturur. Bu, farklı veri türleri ile aynı araçları ve yöntemleri toowork farklı bir kaynak tarafından toplanan toouse hello sağlar.


Günlük analizi ile etkileşim çoğunu olan herhangi bir tarayıcısında çalışır ve erişim tooconfiguration ayarlar ve birden çok araçları tooanalyze ve toplanan verileri vermemizi sağlayan hello OMS portalı üzerinden. Hello Portalı'ndan kullandığınız [oturum aramaları](https://docs.microsoft.com/azure/log-analytics/log-analytics-log-searches) sorguları tooanalyze toplanan verileri oluşturmak burada [panolar](https://docs.microsoft.com/azure/log-analytics/log-analytics-dashboards), en değerli arar ve Grafikgörünümlerleözelleştirebileceğiniz[çözümleri](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions), ek işlevsellik ve çözümleme araçları sağlar.

![Analiz Araçları](./media/azure-threat-detection/azure-threat-detection-fig6.png)

Çözümleri işlevselliği tooLog Analytics ekleyin. Bunlar öncelikle hello bulutta çalışacak ve hello OMS deposunda toplanan verilerin analizini sağlar. Bunlar, ayrıca günlük aramaları veya hello OMS panosunda hello çözümü tarafından sağlanan ek kullanıcı arabirimi tarafından çözümlenebilir toplanan yeni kayıt türleri toobe tanımlayabilir.
Merhaba güvenlik ve denetim çözümleri bu tür bir örnek verilmiştir.



### <a name="automation--control-alert-on-security-configuration-drifts"></a>Otomasyon ve Denetim: güvenlik yapılandırması uyarıdaki drifts

Azure Automation PowerShell üzerine dayalı olan ve hello Azure bulut çalıştırmak runbook'larla yönetim işlemleri otomatik hale getirir. Runbook'ları, bir sunucuda yerel veri merkezi toomanage Yerel kaynaklarınızı da çalıştırılabilir. Azure Otomasyonu PowerShell DSC (İstenen durum yapılandırması) ile yapılandırma yönetimini sağlar.

![Azure Otomasyonu](./media/azure-threat-detection/azure-threat-detection-fig7.png)

Oluşturabilir ve Azure üzerinde barındırılan DSC kaynakları yönetmek ve toocloud ve şirket içi sistemleri toodefine uygulamak ve otomatik olarak yapılandırmalarını zorunlu veya raporları Al kayması üzerinde toohelp güvence altına güvenlik yapılandırmalarını ilke içinde kalır.

## <a name="azure-security-center"></a>Azure Güvenlik Merkezi

Azure Güvenlik Merkezi, Azure kaynaklarınızı korumanıza yardımcı olur. Aboneliklerinizde tümleşik güvenlik izleme ve ilke yönetimi, Azure sağlar. Merhaba Hizmeti'nde misiniz toodefine ilkeleri yalnızca, Azure aboneliklerinize karşı aynı zamanda karşı [kaynak grupları](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal), daha ayrıntılı olabilir.

![Azure Güvenlik Merkezi](./media/azure-threat-detection/azure-threat-detection-fig8.png)

Microsoft Güvenlik Araştırmacıları sürekli olarak tehditleri hello lookout bulunur. Bunlar Microsoft'un hello Bulut ve şirket içindeki genel varlığından alanından elde edilen telemetri erişim tooan korunmalarını kümesine sahip. Geniş kapsamlı ve çeşitlilik barındıran bu veri kümeleri koleksiyonunu Microsoft toodiscover yeni saldırı desenleri ve eğilimleri şirket içi müşteri ve kuruluş ürünlerinin yanı sıra arasında çevrimiçi hizmetleri sağlar.

Bu nedenle, saldırganlar yeni ve giderek karmaşık ortaya çıkardıkça Güvenlik Merkezi algılama algoritmalarını hızlı bir şekilde güncelleştirebilirsiniz. Bu yaklaşım ayak ile hızlı taşıma tehdit ortamında tutmanıza yardımcı olur.

![Güvenlik Merkezi](./media/azure-threat-detection/azure-threat-detection-fig9.jpg)

Güvenlik Merkezi tehdit algılaması Azure kaynaklarını, hello ağ ve bağlı iş ortağı çözümlerinden güvenlik bilgileri otomatik olarak toplayarak çalışır.  Birden fazla kaynaktan tooidentify tehditleri bilgileri ilişkilendirerek, bu bilgileri çözümler.
Güvenlik uyarıları nasıl tooremediate hello tehdit ilişkin öneriler birlikte Güvenlik Merkezi'nde önceliklendirilir.

Güvenlik Merkezi, imza tabanlı yaklaşımların ötesine geçen gelişmiş güvenlik analizleri kullanır. Büyük veri sıçramalar ve [makine öğrenme](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) teknolojilerdir kullanılan tooevaluate olayları elle yaklaşımlar kullanılarak ve hello tahmin etmeye imkansız tooidentify olacak tehditler hello tüm bulut yapısındaki – saldırıları evrimi. Bu güvenlik analizleri hello aşağıdakileri içerir.

### <a name="threat-intelligence"></a>Tehdit Bilgisi

Microsoft yoğun miktarda genel tehdit bilgisine sahiptir.
Azure, Office 365, Microsoft CRM online, Microsoft Dynamics AX, outlook.com, MSN.com, hello Microsoft dijital Suçlar birimi (DCU) ve Microsoft Güvenlik Yanıt Merkezi (MSRC) gibi birden fazla kaynaktan, telemetri akar.

![Tehdit Bilgisi](./media/azure-threat-detection/azure-threat-detection-fig10.jpg)

Araştırmacılar ayrıca büyük bulut hizmeti sağlayıcıları arasında paylaşılan ve Üçüncü taraflardan toothreat akışlarına abone tehdit Bilgileri'ni alırsınız. Azure Güvenlik Merkezi, bu bilgileri tooalert kullanabilir, bilinen kötü aktörlerden gelen toothreats. Bazı örnekler:

-   **Merhaba güç, Machine Learning - gücünden** Azure Güvenlik Merkezi erişim tooa çok büyük miktarda veri olabilir bulut ağ etkinliği hakkında sahip Azure dağıtımlarınızı hedefleme toodetect tehditleri kullanılır. Örneğin:

-   **Deneme yanılma zorla algılamaların -** Machine learning kullanılan toocreate toodetect deneme yanılma saldırılarına karşı SSH, RDP ve SQL bağlantı noktaları sağlar geçmiş bir uzaktan erişim girişimlerini desenini olduğu.

-   **Giden DDoS ve Botnet algılama** -ortak amacı bulut kaynakları hedefleme saldırıları, bu kaynakları tooexecute toouse hello işlem gücünü diğer saldırılara olduğu.

-   **Yeni davranış analizi sunucularını ve Vm'leri -** bir sunucu veya sanal makine tehlikeye sonra saldırganlar çok çeşitli teknikleri tooexecute kötü amaçlı kod sistemdeki algılama önleme, Kalıcılık olduktan ve maliyet sırasında tespit Güvenlik denetimleri.

-   **Azure SQL veritabanı tehdit algılama -** tehdit algılama olağan dışı ve zararlı gösteren anormal veritabanı etkinliklerini tanımlayan Azure SQL veritabanı için tooaccess veya yararlanma veritabanı çalışır.

### <a name="behavioral-analytics"></a>Davranış analizi

Davranış analizi, analiz eden ve bilinen modeller veri tooa koleksiyonuyla karşılaştıran bir tekniktir. Ancak, bu modeller basit imzalar değildir. Bunlar uygulanan toomassive veri kümeleri olan karmaşık machine learning algoritmaları belirlenen var.

![Davranış analizi](./media/azure-threat-detection/azure-threat-detection-fig11.jpg)


Bunlar, kötü amaçlı davranışların uzman analistler tarafından dikkatlice çözümlenmesiyle de belirlenir. Azure Güvenlik Merkezi sanal makine günlükleri, sanal ağ cihaz günlükleri, yapı günlükleri, kilitlenme bilgi dökümleri ve diğer kaynakları analize dayalı davranış analizi tehlikeye tooidentify kaynakları kullanabilir.

Ayrıca, yaygın bir kampanyanın kanıt desteklemek için diğer sinyaller toocheck ile bağıntı yoktur. Bu bağıntı yerleşik tehlike göstergeleriyle tutarlı tooidentify olayları yardımcı olur.

Bazı örnekler:
-   **Şüpheli işlem yürütme:** saldırganlar tespit birkaç teknikleri tooexecute kötü amaçlı yazılım algılama olmadan. Örneğin, bir saldırganın kötü amaçlı yazılım hello yasal sistem dosyalarıyla aynı adı vermek ancak bu dosyaları alternatif bir konuma yerleştirmek için çok iyi amaçlı bir dosyaya veya maskesi hello dosyanın gerçek uzantısını gibi bir ad kullanın. Güvenlik Merkezi modelleri, davranışları işler ve izleyiciler gibi bu yürütmeleri toodetect aykırı değerlerini işler.

-   **Gizli kötü amaçlı yazılım ve istismarı denemeleri:** karmaşık kötü amaçlı yazılımlar alınmadan kurtulması geleneksel kötü amaçlı yazılımdan koruma ürünleri hiçbir zaman toodisk yazma veya diske depolanmış yazılım bileşenlerini şifreleyerek. Merhaba kötü amaçlı yazılım izlemeleri bellek toofunction bırakmak zorunda olduğundan ancak, bu tür kötü amaçlı yazılım bellek analizi kullanılarak algılanabilir. Yazılım kilitlendiğinde bir kilitlenme dökümü hello kilitlenme hello aynı anda belleğin bir kısmını yakalar. Merhaba kilitlenme döküm Hello bellekte analiz ederek Azure Güvenlik Merkezi teknikleri tooexploit güvenlik açıkları yazılım kullanılan algılayabilir, gizli verilere erişmek ve gizlice hello performansını etkilemeden tehlikeye giren bir makineye içinde kalır makinenizde.

-   **Yanal hareket ve iç keşif:** toopersist güvenliği aşılmış bir ağ ve bulmak/toplamak değerli veri saldırganlar genellikle toomove yanal tehlikeye hello gelen deneyin içinde makine tooothers hello aynı ağ. Güvenlik Merkezi işlem izler ve oturum açma etkinliklerini toodiscover tooexpand bir saldırganın uzaktan komut yürütme, ağ araştırma ve hesap numaralandırma gibi hello ağ içinde çalışır.

-   **Kötü amaçlı PowerShell komut dosyaları:** PowerShell kullanılabilir hedef sanal makinelerde tooexecute kötü amaçlı kod saldırganlar tarafından çeşitli amaçlarla. Güvenlik Merkezi şüpheli etkinliklerin kanıtı için PowerShell etkinliğini inceler.

-   **Giden saldırılar:** saldırganlar genellikle bulut kaynaklarını bu kaynakları toomount ek saldırılarını kullanmasını hello amacı hedef. Riskli sanal makineler, örneğin, diğer sanal makinelere karşı deneme yanılma saldırıları kullanılan toolaunch olması, istenmeyen posta göndermek veya açık bağlantı noktalarını ve hello Internet üzerindeki diğer cihazlar tarama. Makine uygulayarak giden ağ iletişimlerinin hello normu aştığını toonetwork trafiği öğrenme, Güvenlik Merkezi algılayabilir. Ne zaman istenmeyen posta, Güvenlik Merkezi ayrıca karşılık gelen olağandışı e-posta trafiğini Office 365 toodetermine'ten ile Merhaba posta büyük olasılıkla olup alınan ya da bir meşru e-posta kampanya hello sonucu.

### <a name="anomaly-detection"></a>Anomali algılama

Azure Güvenlik Merkezi, ayrıca anomali algılama tooidentify tehditleri kullanır. (Bu, büyük veri kümelerinden türetilmiş bilinen modellere bağlıdır) Karşıtlık toobehavioral analytics'te anomali algılama daha fazla "kişiselleştirilmiştir" ve belirli tooyour dağıtımları temelleri odaklanır. Machine learning dağıtımlarınızın normal etkinliğini uygulanan toodetermine, ve bir güvenlik olayını gösterebilecek aykırı değer koşullarını oluşturulan toodefine kurallardır. Bir örneği aşağıda verilmiştir:

-   **RDP/SSH deneme yanılma saldırıları gelen:** dağıtımlarınız her gün ve diğer sanal birkaç veya tüm oturumları makinelerde birçok oturumları yoğun sanal makineler olabilir. Azure Güvenlik Merkezi bu sanal makineler için taban çizgisi oturum açma etkinliğini belirler ve machine learning toodefine hello normal oturum açma etkinliklerini geçici kullanın. Merhaba taban çizgisi için tanımlanan herhangi bir farklılık olması halinde bir uyarı oluşturulabilir daha sonra oturum açma özellikleri, ilgili. Yine machine learning neyin önemli olduğunu belirler.

### <a name="continuous-threat-intelligence-monitoring"></a>Sürekli tehdit bilgileri izleme

Azure Güvenlik Merkezi hello tehdit kapsamındaki değişiklikleri sürekli olarak izleyen güvenlik araştırması ve veri bilimi ekipleri Merhaba dünya genelinde ile çalışır. Bu girişimleri aşağıdaki hello içerir:

-   **Tehdit bilgisi izleme:** tehdit Intelligence mekanizmaları, göstergeleri, uygulamaları ve var olan veya yeni ortaya çıkan tehditlere uygulanabilir öneriler içerir. Bu bilgiler hello güvenlik topluluğu içinde paylaşılır ve Microsoft iç ve dış kaynaklardan gelen tehdit bilgisi akışlarını sürekli olarak izler.

-   **Sinyal paylaşımı:** Bulut ve şirket içi hizmetler, sunucular ve istemci uç noktası cihazları arasında Microsoft'un geniş Portföyünde güvenlik ekiplerinden alınan bilgiler paylaşılır ve analiz edilir.

-   **Microsoft Güvenlik uzmanları:** hukuk gibi Uzman güvenlik alanlarında çalışan ve web saldırıcı algılama takımlar arasında Microsoft ile devam eden katılım.

-   **Algılama ayarı:** gerçek müşteri veri kümelerine göre algoritmalar çalıştırılır ve güvenlik Araştırmacıları müşteriler toovalidate hello sonuçları. TRUE ve false kullanılan toorefine machine learning algoritmaları durumlarıdır.

Hangi konumdan anında yararlanabilirsiniz yeni ve geliştirilmiş algılama içinde bu birleşik çabalar culminate –, tootake için bir eylem yok.

## <a name="advanced-threat-detection-features---other-azure-services"></a>Gelişmiş tehdit algılama özellikleri - diğer Azure Hizmetleri

### <a name="virtual-machine-microsoft-antimalware"></a>Sanal makine: Microsoft kötü amaçlı yazılımdan koruma

[Microsoft Antimalware](https://docs.microsoft.com/azure/security/azure-security-antimalware) Azure uygulamaları ve Kiracı ortamları için bir tek Aracısı çözümü için İnsan aracılığı olmadan hello arka planda toorun tasarlanmıştır. İle ya da temel güvenli--varsayılan olarak, uygulama iş yüklerinin hello gereksinimlerini temel veya Gelişmiş kötü amaçlı yazılımdan koruma izleme de dahil olmak üzere özel yapılandırma koruması dağıtabilirsiniz. Azure kötü amaçlı yazılımdan koruma güvenlik için Azure sanal makineleri bir seçenektir ve tüm Azure PaaS sanal makinelere otomatik olarak yüklenir.

**Özelliklerini Azure toodeploy ve uygulamalarınız için Microsoft Antimalware etkinleştir**

#### <a name="microsoft-antimalware-core-features"></a>Microsoft kötü amaçlı yazılımdan koruma çekirdek Özellikler

-   **Gerçek zamanlı koruma -** etkinlik bulut Hizmetleri ve sanal makineleri toodetect ve blok kötü amaçlı yazılım yürütme izler.

-   **Zamanlanmış tarama -** etkin olarak çalışan programlar dahil olmak üzere hedeflenen tarama toodetect kötü amaçlı yazılım, düzenli olarak gerçekleştirir.

-   **Kötü amaçlı yazılım düzeltme -** otomatik olarak algılanan kötü amaçlı yazılım silme veya kötü amaçlı dosyaları karantinaya alma ve kötü amaçlı kayıt defteri girdilerini temizleme gibi eylemi alır.

-   **İmza güncelleştirmeleri -** otomatik olarak yükler hello son koruma imzaları (virüs tanımları) tooensure koruma önceden belirlenen bir frekansında güncel olduğundan.

-   **Kötü amaçlı yazılımdan koruma Altyapısı güncelleştirmeleri -** otomatik olarak güncelleştirmeleri Microsoft Antimalware altyapısı hello.

-   **Kötü amaçlı yazılımdan koruma platformu güncelleştirmeleri –** otomatik olarak güncelleştirmeleri Microsoft Antimalware platform hello.

-   **Etkin bir koruma -** algılanan Tehditler ve tehdit gelişen ve gerçek zamanlı zaman uyumlu imza teslim aracılığıyla etkinleştirme şüpheli kaynakları tooMicrosoft Azure tooensure hızlı yanıt toohello hakkında telemetri meta verileri raporları Merhaba Microsoft etkin koruma sistem (MAPS).

-   **Örnekleri raporlama -** sağlar ve örnek raporları toohello Microsoft Antimalware service toohelp hello service ve enable sorun giderme daraltın.

-   **Dışlamalar –** korumadan bunları ve performans ve/veya diğer nedenlerle tarama tooexclude sürücüler ve uygulama ve hizmet yöneticileri tooconfigure işlemleri, belirli dosyaları sağlar.

-   **Kötü amaçlı yazılımdan koruma olay toplama -** hello kötü amaçlı yazılımdan koruma hizmeti durumu, kuşkulu etkinlikleri ve hello işletim sistem olay günlüğünde gerçekleştirilecek düzeltme eylemleri kaydeder ve hello müşterinin Azure Storage hesabınıza toplar.

### <a name="azure-sql-database-threat-detection"></a>Azure SQL veritabanı tehdit algılama

[Azure SQL veritabanı tehdit algılama](https://azure.microsoft.com/blog/azure-sql-database-threat-detection-your-built-in-security-expert/) hello Azure SQL veritabanı hizmetinin oluşturulmuş yeni bir güvenlik Intelligence özelliğidir. Merhaba çözümüne toolearn, profil çıkış ve anormal veritabanı etkinliklerini algılar, olası tehditler toohello veritabanını Azure SQL veritabanı tehdit algılama tanımlar.

Bunlar ortaya çıktığında güvenlik görevlileri veya diğer atanmış yöneticileri şüpheli veritabanı etkinlikleri hakkında anında bildirim edinebilirsiniz. Her bir bildirim hello şüpheli Etkinlik ayrıntıları sağlar ve nasıl toofurther araştırın ve hello tehdidi azaltmak önerir.

Şu anda, Azure SQL veritabanı tehdit algılama, olası güvenlik açıkları ve SQL ekleme saldırıları ve anormal veritabanı erişimi desenleri algılar.

Tehdit algılama e-posta bildirimi aldıktan sonra kullanıcılar bir denetim Görüntüleyicisi'ni ve/veya hello ilgili denetim gösterir önceden yapılandırılmış denetim Excel şablonu açar hello Mail'de hello ayrıntılı bağlantısı kullanarak mümkün toonavigate ve görünüm hello ilgili denetim kayıtlarıdır Merhaba şüpheli olay toohello aşağıdaki göre hello sırada geçici kaydeder:
-   Merhaba veritabanı/sunucuyla hello anormal veritabanı etkinliklerini denetim depolama

-   Merhaba olay toowrite denetim günlüğü hello aynı anda kullanılan ilgili denetim depolama tablosu

-   Merhaba olay oluştuğunda gerçekleştiğinden saat aşağıdaki hello kayıtlarının denetim.

-   Denetim kayıtlarının benzer olay kimliği hello zaman hello olayının (bazı algılayıcılar için isteğe bağlı)

SQL veritabanı tehdit algılayıcılar algılama yöntemlerini aşağıdaki hello birini kullanın:

-   **Belirlenimci algılama –** şüpheli desenler (dayalı kurallar) bilinen saldırıları eşleşen hello SQL istemci sorgularda algılar. Bu yöntemler yüksek algılama ve düşük yanlış pozitif sahiptir ancak "atomik algılama" Merhaba kategoride kaldığından kapsamı sınırlı.

-   **Behavioural algılama –** hello sırasında son 30 gün görülen değil hello veritabanı için olağan dışı davranış anormal bir etkinliğin hataları.  SQL istemci anormal etkinliği için bir örnek depo başarısız oturum açma/sorguları, ayıklanırken veri hacmi yüksek, olağan dışı kurallı sorgular ve tanınmayan IP adresleri kullanılan tooaccess hello veritabanı olabilir

### <a name="application-gateway-web-application-firewall"></a>Uygulama ağ geçidi Web uygulaması güvenlik duvarı

[Web uygulaması güvenlik duvarı](https://docs.microsoft.com/azure/app-service-web/app-service-app-service-environment-web-application-firewall) özelliğidir [Azure uygulama ağ geçidi](https://docs.microsoft.com/azure/application-gateway/application-gateway-webapplicationfirewall-overview) için standart uygulama ağ geçidini kullanan tooweb uygulamaları koruma sağlar [uygulama teslim denetimi](https://kemptechnologies.com/in/application-delivery-controllers) işlevleri. Web uygulaması güvenlik duvarı olmadığından bu hello çoğunu karşı koruma tarafından [OWASP ilk 10 ortak web güvenlik açıkları](https://www.owasp.org/index.php/Top_10_2010-Main)

![Uygulama ağ geçidi Web uygulaması Firewally](./media/azure-threat-detection/azure-threat-detection-fig13.png)

-   SQL ekleme koruması

-   Siteler arası komut dosyası koruması

-   Komut ekleme, HTTP isteği kaçakçılığı, HTTP yanıtı bölme ve uzak dosya ekleme saldırıcı gibi Yaygın Web Saldırıları Koruması

-   HTTP protokolü ihlallerine karşı koruma

-   Eksik konak kullanıcısı-aracısı ve kabul üst bilgileri gibi HTTP protokolü anormalliklerine karşı koruma

-   Robotlar, gezginler ve tarayıcıları önleme

-   Ortak uygulama yapılandırma hataları (diğer bir deyişle, Apache, IIS, vb.) algılanması

Uygulama ağ geçidi WAF yapılandırma avantajı tooyou aşağıdaki hello sağlar:

-   Web uygulamanızı web Güvenlik Açıkları ve değişikliği toobackend kodu olmadan saldırılara karşı koruma.

-   Birden çok web korumak hello uygulamasını aynı anda bir uygulama ağ geçidi. Uygulama ağ geçidi too20 Web sitelerinin tüm web saldırılarına karşı korumalı tek bir ağ geçidi arkasında barındırma destekler.

-   Uygulama ağ geçidi WAF günlükleri tarafından oluşturulan gerçek zamanlı raporları kullanarak web uygulamanızı saldırılara karşı izleyin.

-   Belirli uyumluluk denetimleri bitiş noktalarını toobe WAF çözümü tarafından korunan tüm Internet'e gerektirir. WAF etkinken uygulama ağ geçidini kullanarak, bu uyumluluk gereksinimlerini karşılayabilirsiniz.

### <a name="anomaly-detection--an-api-built-with-azure-machine-learning"></a>Anomali algılama – Azure Machine Learning ile yerleşik bir API

Anomali algılama anormal desenleri farklı türde zaman serisi verilerinizi algılamak için yararlı olan Azure Machine Learning ile yerleşik bir API'dir. Merhaba API atar puan tooeach veri noktası uyarıları oluşturmak için kullanılabilir, hello zaman serisi içinde bir anomali izleme panoları veya gişe sistemleri ile bağlama.

Merhaba [Anomali algılama API](https://docs.microsoft.com/azure/machine-learning/machine-learning-apps-anomaly-detection-api) zaman serisi veri üzerinde şu anormallikleri türlerini hello algılayabilir:

-   **Ani ve Dips:** Örneğin, oturum açma hataları tooa hizmet hello sayısını veya bir e-ticaret sitesi kullanıma sayısında izlerken, olağan dışı ani dıps güvenlik saldırılarına belirtmek veya hizmet kesintilerini.

-   **Pozitif ve negatif eğilimleri:** bilgi işlem bellek kullanımı izlerken, örneğin, boş bellek boyutu küçültme olası bir bellek sızıntısı hatırlanması; hizmet sırası uzunluğu izlerken, kalıcı bir yukarı eğilim bir arka plandaki gösterebilir yazılım sorunu.

-   **Düzey değişiklikleri ve dinamik aralık değerleri değişiklikleri:** hizmet yükseltin ya da yükseltme ilginç toomonitor olabilir sonra özel durumlar düzeylerde alt sonra düzeyindeki bir hizmet gecikmeleri Örneğin, değişiklikleri.

Merhaba machine learning göre API sağlar:

-   **Esnek ve sağlam algılama:** hello anomali algılama modelleri tooconfigure duyarlılık ayarlarını kullanıcıların ve anormallikleri Mevsimlik ve Mevsimlik olmayan veri kümesi arasında algılayabilir. Kullanıcıların hello anomali algılama modelini toomake hello algılama API daha az ayarlayabilir veya daha hassas according tootheir gerekiyor. Bu hello algılama daha az veya daha fazla görünür anormallikleri veri ile ve Mevsimlik desenleri olmadan anlamına gelir.

-   **Ölçeklenebilir ve zamanında algılama:** uzmanlar etki alanı bilgi sahibi ayarlamak mevcut eşiklerle izleme hello geleneksel bir yöntemdir dinamik olarak veri kümeleri değiştirmenin maliyetli ve ölçeklenebilir olmaması toomillions. Bu API Hello anomali algılama modellerinde öğrenilen ve modelleri geçmiş ve gerçek zamanlı verileri otomatik olarak ayarlanmıştır.

-   **Öngörülü ve tıklatılabilir algılama:** yavaş eğilim ve düzey değişikliği algılama erken anomali algılama için uygulanır. Merhaba erken anormal sinyalleri algılanan kullanılan toodirect insanlar tooinvestigate olması ve hello sorunlu alanları üzerinde hareket.  Ayrıca, kök neden analizi modelleri ve uyarı araçları bu anomali algılama API hizmeti üstünde geliştirilebilir.

Merhaba anomali algılama API kadar çeşitli senaryoları hizmet durumu ve izleme, IOT, performans izlemeyi ve ağ trafiğini izleme KPI gibi için etkili ve verimli bir çözümdür. Burada, bu API yararlı olabilir bazı yaygın senaryolar şunlardır:
- BT departmanları zamanında araçları tootrack olayları, hata kodu, kullanım günlük ve performans (CPU, bellek ve benzeri) gerekir.

-   Çevrimiçi Ticaret siteleri tootrack müşteri etkinlikleri, sayfa görünümleri, tıklama ve benzeri istiyor.

-   Yardımcı programı şirketler su, gaz, elektrik ve diğer kaynakları tootrack tüketimini istiyor.

-   Yönetim Hizmetleri tesis/oluşturma toomonitor sıcaklık, nemi, trafiği ve benzeri istiyor.

-   IOT/üreticileri istediğiniz zaman serisi toomonitor toouse algılayıcı verileri iş akışı, kalite ve benzeri.

-   Çağrı merkezleri toomonitor hizmet isteğe bağlı eğilimi, olay birimi gerektiği gibi hizmet sağlayıcıları, kuyruk uzunluğu vb. bekleyin.

-   İş analizi grupları (örneğin, Satış Birim, fiyatlandırma müşteri düşüncelerin) toomonitor iş KPI'leri istediğiniz gerçek zamanlı anormal taşıma.

### <a name="cloud-app-security"></a>Cloud App Security

[Cloud App Security](https://docs.microsoft.com/cloud-app-security/what-is-cloud-app-security) hello Microsoft Cloud Security yığınının kritik bir bileşendir. Bulut uygulamalarının hello promise tam anlamıyla tootake taşımak, ancak denetim etkinlik geliştirilmiş görünürlük aracılığıyla bulundurmanız, kuruluşunuzun yardımcı olabilecek kapsamlı bir çözümdür. Ayrıca, bulut uygulamaları genelinde kritik veri korumasını hello artırmaya yardımcı olur.

Gölge BT ortaya çıkarmaya, riskleri değerlendirmeye, ilkeleri zorunlu tutmanıza, etkinlikleri araştırmaya ve tehditleri durdurmaya yardımcı olan araçlar ile kuruluşunuz daha güvenli bir şekilde toohello bulut kritik verilerin denetimini korurken taşıyabilirsiniz.

<table style="width:100%">
 <tr>
   <td>Keşif</td>
   <td>BT Cloud App Security ile gölge BT'yi ortaya çıkarın. Uygulamaları, etkinlikleri, kullanıcılar, veri ve bulut ortamınızdaki dosyaları bularak görünürlük elde edilir. Bağlı olan üçüncü taraf uygulamaları Bul tooyour bulut.</td>
 </tr>
 <tr>
   <td>Araştır</td>
   <td>Riskli uygulamalar, belirli kullanıcılar ve ağınızdaki dosya bulut adli araçları toodeep-Dalış kullanarak, bulut uygulamalarınızı araştırın. Toplanan hello verilerdeki düzenleri bulun. Raporları toomonitor bulut oluşturun.</td>

 </tr>
 <tr>
   <td>denetimi</td>
   <td>Ağ bulut trafiği üzerinde en yüksek düzeyde denetim tooachieve ilkeler ve uyarılar ayarlayarak riski azaltın. Cloud App Security toomigrate tasdikli bulut uygulaması alternatiflerine, kullanıcıların toosafe kullanın.</td>

 </tr>
 <tr>
   <td>Koruma</td>
   <td>Cloud App Security toosanction kullanın veya uygulamaları engelle, veri kaybını önleme, Denetim izinleri ve paylaşımı zorlamak ve özel raporlar ve uyarılar oluşturur.</td>

 </tr>
 <tr>
   <td>denetimi</td>
   <td>Ağ bulut trafiği üzerinde en yüksek düzeyde denetim tooachieve ilkeler ve uyarılar ayarlayarak riski azaltın. Cloud App Security toomigrate tasdikli bulut uygulaması alternatiflerine, kullanıcıların toosafe kullanın.</td>

 </tr>
</table>


![Cloud App Security](./media/azure-threat-detection/azure-threat-detection-fig14.png)

Cloud App Security görünürlük tarafından bulut ile tümleşir.

-   Cloud Discovery toomap kullanarak bulut ortamınızı tanımlamak ve kuruluşunuzun kullanarak bulut uygulamalarını hello.


-   Tasdit etme ve bulut uygulamalarında yasaklamaktadır.



-   Görünürlüğü ve İdaresi, bağlandığınız uygulamalar için API ' larını sağlayıcısı yararlanmak dağıtımı kolay uygulama bağlayıcıları kullanma.

-   Sürekli denetimi ayarı ve sürekli olarak ince ayar, ilkeleri tarafından size yardımcı olur.

Bu kaynaklardan veri toplama üzerinde Cloud App Security Gelişmiş bir analiz hello veri üzerinde çalışır. Hemen tooanomalous etkinlikleri uyarıları ve bulut ortamınıza derin bir görünürlük sağlar. Cloud App Security bir ilke yapılandırın ve tooprotect kullanın, bulut ortamınızdaki her şeyi.

## <a name="third-party-atd-capabilities-through-azure-marketplace"></a>Azure Market üzerinden üçüncü taraf ATD özellikleri

### <a name="web-application-firewall"></a>Web Uygulaması Güvenlik Duvarı

Web uygulaması güvenlik duvarı gelen web trafiği ve blokları SQL eklemelerini, siteler arası komut dosyası, kötü amaçlı yazılım yüklemeleri ve uygulama DDoS ve web uygulamalarınızı hedefleyen diğer saldırılara olup olmadığını denetler. Ayrıca hello yanıtları hello arka uç web sunucularından veri kaybını önleme (DLP) inceler. Merhaba tümleşik erişim denetimi altyapısı, kimlik doğrulama, yetkilendirme ve hesap oluşturma (kuruluşlar güçlü kimlik doğrulama ve kullanıcı denetimi sağlayan AAA), yöneticiler toocreate ayrıntılı erişim denetimi ilkeleri sağlar.

**Vurgular:**
-   Algılar ve SQL eklemelerini, siteler arası komut dosyası, kötü amaçlı yazılım yüklemeleri, uygulama DDoS veya herhangi bir uygulamanız saldırıları engeller.

-   Kimlik doğrulaması ve erişim denetimi.

-   Giden trafik toodetect hassas verileri tarar ve maskeleyebilirsiniz veya engelleme hello bilgilerinin sızmasını.

-   Web uygulama içeriğini önbelleğe alma, sıkıştırma ve diğer trafik iyileştirmeleri gibi özelliklerini kullanarak, Hello dağıtımını hızlandırır.

Web uygulaması güvenlik duvarı Azure Market yerinde kullanılabilir örneği aşağıda verilmiştir:

[Barracuda Web uygulaması güvenlik duvarı, Brocade sanal Web uygulaması Güvenlik Duvarı (Brocade vWAF), Imperva SecureSphere ve hello ThreatSTOP IP Güvenlik Duvarı.](https://azure.microsoft.com/marketplace/partners/brocade_communications/brocade-virtual-web-application-firewall-templatevtmcluster/)

## <a name="next-steps"></a>Sonraki Adımlar

- [Azure Güvenlik Merkezi algılama özellikleri](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities)

Azure Güvenlik Merkezi'nin Gelişmiş algılama özelliklerini hello Öngörüler sizinle toorespond hızla gerekli sağlar ve Microsoft Azure kaynaklarınızı hedefleyen etkin tehditleri tooidentify yardımcı olur.

- [Azure SQL veritabanı tehdit algılama](https://azure.microsoft.com/blog/azure-sql-database-threat-detection-your-built-in-security-expert/)

Azure SQL veritabanı tehdit algılama, kendi endişelere olası tehditler tootheir veritabanı hakkında Yardım.
