---
title: "Azure Güvenlik Merkezi'nde aaaPartner tümleştirme | Microsoft Docs"
description: "Azure Güvenlik Merkezi ile iş ortakları tooenhance nasıl tümleştirilir hakkında bilgi edinin Azure kaynaklarınızın genel güvenlik."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 6af354da-f27a-467a-8b7e-6cbcf70fdbcb
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: yurid
ms.openlocfilehash: 3621335730a076721cb3c23788a47be50aa8fc73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="partner-integration-in-azure-security-center"></a>Azure Güvenlik Merkezi'nde İş Ortağı tümleştirmesi

Bu makalede, sizi Azure Güvenlik Merkezi ile iş ortakları toohelp nasıl tümleşik çalıştığını açıklamak genel güvenliği artırın. Güvenlik Merkezi, azure'da tümleşik bir deneyim sunan ve sertifika ve faturalama hello Azure Marketi ortak yararlanır.

> [!NOTE] 
> Haziran 2017 itibariyle, Güvenlik Merkezi hello Microsoft İzleme Aracısı toocollect ve deposu verileri kullanır. Daha fazla bilgi için bkz. [Azure Güvenlik Merkezi platform geçişi](security-center-platform-migration.md). Bu makaledeki Hello bilgiler geçiş toohello sonra Microsoft İzleme Aracısı Güvenlik Merkezi işlevlerini temsil eder.
>

## <a name="why-deploy-partner-solutions-from-security-center"></a>Neden Güvenlik Merkezi’nden iş ortağı çözümleri dağıtmalı

Güvenlik Merkezi'nde dört temel nedenlerinden tooleverage iş ortağı tümleştirme şunlardır:

- **Dağıtım kolaylığı**. Güvenlik Merkezi öneri aşağıdaki hello tarafından bir iş ortağı çözümü dağıtma daha kolaydır. Merhaba dağıtım işlemi tam olarak bir varsayılan kurulum ve ağ topolojisi kullanarak otomatik olarak yapılabilir. Alternatif olarak, müşteriler daha fazla esneklik ve özelleştirme için yarı-otomatik bir seçeneği tercih edebilir.
- **Tümleşik algılamalar**. İş ortağı çözümlerinden gelen güvenlik olayları otomatik olarak toplanır, birleştirilir ve Güvenlik Merkezi uyarıları ve olaylarının bir parçası olarak görüntülenir. Bu olaylar ayrıca algılamaların dışında Gelişmiş tehdit algılama özellikleri diğer kaynakları tooprovide ile Sigortalı.
- **Birleşik sistem durumu izleme ve yönetimi**. Müşteriler tümleşik sistem durumu olayları toomonitor bir bakışta tüm iş ortağı çözümleri kullanabilirsiniz. Temel yönetim hello iş ortağı çözümü kullanarak kolay erişim tooadvanced kurulumu ile kullanılabilir.
- **TooSIEM verme**. Müşteriler tüm Güvenlik Merkezi verebilirsiniz ve ortak iş ortağı Azure günlük tümleştirme (Önizleme) kullanarak olay biçimi (CEF) tooon içi güvenlik bilgileri ve Olay yönetimi (SIEM) sistemleri uyarır.


## <a name="partners-that-integrate-with-security-center"></a>Güvenlik Merkezi ile tümleştirilen iş ortakları

Güvenlik Merkezi şu anda aşağıdaki çözümlerle tümleştirilebilir:

- Uç nokta koruması ([Trend Micro](https://help.deepsecurity.trendmicro.com/azure-marketplace-getting-started-with-deep-security.html), Symantec, [Azure Cloud Services ve Sanal Makineler için Microsoft Kötü Amaçlı Yazılımdan Koruma Yazılımı](https://docs.microsoft.com/azure/security/azure-security-antimalware)) 
- Web uygulaması güvenlik duvarı ([Barracuda](https://www.barracuda.com/products/webapplicationfirewall), [F5](https://support.f5.com/kb/en-us/products/big-ip_asm/manuals/product/bigip-ve-web-application-firewall-microsoft-azure-12-0-0.html), [Imperva](https://www.imperva.com/Products/WebApplicationFirewall-WAF), [Fortinet](https://www.fortinet.com/resources.html?limit=10&search=&document-type=data-sheets) ve [Azure Application Gateway](https://azure.microsoft.com/blog/azure-web-application-firewall-waf-generally-available/)) 
- Yeni nesil güvenlik duvarı ([Check Point](https://www.checkpoint.com/products/vsec-microsoft-azure/), [Barracuda](https://campus.barracuda.com/product/nextgenfirewallf/article/NGF/AzureDeployment/), [Fortinet](http://docs.fortinet.com/d/fortigate-fortios-handbook-the-complete-guide-to-fortios-5.2) ve [Cisco](http://www.cisco.com/c/en/us/td/docs/security/firepower/quick_start/azure/ftdv-azure-qsg.html)) 
- Güvenlik açığı değerlendirmesi ([Qualys](https://www.qualys.com/public-clouds/microsoft-azure/))  

Zamanla, Güvenlik Merkezi bu kategorilerde ortakları hello sayısı genişletin ve yeni kategoriler eklemek. 

## <a name="deploy-a-partner-solution"></a>İş ortağı çözümü dağıtma

Merhaba Kurulumu Azure ortamı ve tanımladığınız hello güvenlik ilkesini temel alarak, Güvenlik Merkezi bir iş ortağı çözümü dağıtmak önerebilir. Güvenlik Merkezi öneri Hello seçme ve iş ortağı çözümü yükleme hello işleminde size rehberlik eder. Merhaba genel dağıtım deneyimi, çözüm ve kullandığınız ortağı hello türüne bağlı olarak değişebilir. Daha fazla bilgi için aşağıdaki makaleler hello bakın:

- [Uç nokta korumasını yükleme](security-center-install-endpoint-protection.md)
- [Web uygulaması güvenlik duvarı ekleme](security-center-add-web-application-firewall.md)
- [Yeni nesil güvenlik duvarı ekleme](security-center-add-next-generation-firewall.md)
- [Güvenlik açığı değerlendirmesi yüklü değil](security-center-vulnerability-assessment-recommendations.md)

## <a name="manage-partner-solutions"></a>İş ortağı çözümlerini yönetme

Dağıtım sonra tooview ve hakkında bilgi hello hello çözüm durumunu hello üzerinde temel yönetim görevlerini gerçekleştirmek **Güvenlik Merkezi** dikey penceresinde, select hello **iş ortağı çözümleri** seçeneği. Güvenlik Merkezi'nde iş ortağı çözümlerini yönetme hakkında daha fazla bilgi edinmek, bkz. [Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md).

![İş ortağı tümleştirmesi](./media/security-center-partner-integration/security-center-partner-integration-fig1-new2.png)

> [!NOTE]
> Symantec endpoint protection desteği sınırlı toodiscovery değil. Sistem durumu uyarıları sağlanmaz.
>

## <a name="see-also"></a>Ayrıca bkz.

Bu makalede, nasıl toointegrate iş ortağı çözümleri Azure Güvenlik Merkezi'nde öğrendiniz. Güvenlik Merkezi hakkında daha fazla toolearn makaleler hello bakın:

* [Güvenlik Merkezi planlama ve işlemler kılavuzu](security-center-planning-and-operations-guide.md)
* [Yönetme ve Güvenlik Merkezi'nde toosecurity uyarılarını yanıtlama](security-center-managing-and-responding-alerts.md)
* [Güvenlik Merkezi’nde türlerine göre güvenlik uyarıları](security-center-alerts-type.md)
* [Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md). Nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.
* [Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md). Nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi SSS](security-center-faq.md). Merhaba hizmeti kullanımı ile ilgili sorular yanıtlar toofrequently alın.
* [Azure Güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/). Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulun.
