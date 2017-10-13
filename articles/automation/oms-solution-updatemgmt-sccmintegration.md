---
title: "OMS Güncelleştirme Yönetiminde SCCM Koleksiyonlarını Kullanarak Güncelleştirmeleri Hedefleme | Microsoft Docs"
description: "Bu makale, SCCM ile yönetilen bilgisayarların güncelleştirmelerini yönetmek üzere System Center Configuration Manager’ı bu çözümle yapılandırmanıza yardımcı olmaya yöneliktir."
services: operations-management-suite
documentationcenter: 
author: eslesar
manager: carmonm
editor: 
ms.assetid: 
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/25/2017
ms.author: eslesar
ms.openlocfilehash: c3ae8da65e03fe9e11b5657a6a40d02de0567da6
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="integrate-system-center-configuration-manager-with-oms-update-management-preview"></a>System Center Configuration Manager’ı OMS Güncelleştirme Yönetimi ile Tümleştirme [Önizleme]

PC, sunucu ve mobil cihazları yönetmek için System Center Configuration Manager’a yatırım yapmış müşteriler aynı zamanda yazılım güncelleştirme yönetimi (SUM) döngüsünün bir parçası olarak yazılım güncelleştirmelerini yönetme gücünden ve olgunluğundan yararlanmaktadır.  

Günümüzde OMS ile Configuration Manager arasında var olan tümleştirmeye ek olarak, Configuration Manager’da yazılım güncelleştirme dağıtımları oluşturup ön hazırlığını yapabilir ve [Güncelleştirme Yönetimi çözümünü](../operations-management-suite/oms-solution-update-management.md) kullanarak tamamlanmış güncelleştirme dağıtımlarının ayrıntılı durumunu öğrenebilirsiniz. Configuration Manager’ı güncelleştirme uyumluluğu raporlama amacıyla kullanırken Windows sunucularınızla güncelleştirme dağıtımlarını yönetmek için kullanmıyorsanız, güvenlik güncelleştirmeleri OMS Güncelleştirme Yönetimi çözümü ile yönetilirken Configuration Manager’a rapor göndermeye devam edebilirsiniz.

## <a name="prerequisites"></a>Ön koşullar

* [Güncelleştirme Yönetimi çözümü](../operations-management-suite/oms-solution-update-management.md), Log Analytics çalışma alanınıza eklenmiş ve Otomasyon hesabınızla aynı kaynak grubu ve bölgesinde ilişkilendirilmiş olmalıdır.   
* Şu anda System Center Configuration Manager ortamınız tarafından yönetilen Windows sunucularının da Güncelleştirme Yönetimi çözümü etkin olan Log Analytics çalışma alanına rapor göndermesi gerekir.  
* Bu özellik System Center Configuration Manager geçerli dal sürümü 1606 ve üstünü destekler.  Configuration Manager merkezi yönetim sitenizi veya tek başına birincil sitenizi Log Analytics ile tümleştirmek ve koleksiyonları içeri aktarmak için [Configuration Manager’ı Log Analytics’e Bağlama](../log-analytics/log-analytics-sccm.md) makalesini gözden geçirin.  
* Windows aracıları Configuration Manager’dan güvenlik güncelleştirmeleri almazsa Windows Server Update Services (WSUS) sunucusuyla iletişim kuracak veya Microsoft Update’e erişecek şekilde yapılandırılmış olmalıdır.   

Azure IaaS içinde barındırılan istemcileri mevcut Configuration Manager ortamınızla nasıl yönettiğiniz birincil olarak Azure veri merkezleri ile altyapınız arasında mevcut olan bağlantıya bağlıdır. Bu bağlantı, Configuration Manager altyapısında yapmanız gereken her türlü tasarım değişikliğini ve bu değişiklikleri desteklemeyle ilgili maliyetleri etkiler.  Devam etmeden önce değerlendirmeniz gereken planlama konularını anlamak için, [Azure’da Configuration Manager - Sık Sorulan Sorular](https://docs.microsoft.com/sccm/core/understand/configuration-manager-on-azure#networking)’ı gözden geçirin.    

## <a name="configuration"></a>Yapılandırma

### <a name="manage-software-updates-from-configuration-manager"></a>Configuration Manager’dan yazılım güncelleştirmelerini yönetme 

Güncelleştirme dağıtımlarını Configuration Manager’dan yönetmeye devam edecekseniz aşağıdaki adımları gerçekleştirin.  OSM, Log Analytics çalışma alanınıza bağlı istemci bilgisayarlara güncelleştirmeleri uygulamak için Configuration Manager’a bağlanır. Güncelleştirme içeriği, dağıtım Configuration Manager’dan yönetiliyormuş gibi istemci bilgisayar önbelleğinden alınabilir.  

1. Configuration Manager hiyerarşinizde en üst düzeydeki siteden bir yazılım güncelleştirme dağıtımı oluşturmak için [yazılım güncelleştirme işlemini dağıtma](https://docs.microsoft.com/en-us/sccm/sum/deploy-use/deploy-software-updates) bölümünde açıklanan işlemi kullanın.  Standart bir dağıtımdan farklı şekilde yapılandırılması gereken tek ayar, dağıtım paketinin indirme davranışını denetlemeye yönelik **Yazılım güncelleştirmelerini yükleme** seçeneğidir. Bu davranış, sonraki adımda zamanlanmış bir güncelleştirme dağıtımı oluşturularak OMS Güncelleştirme Yönetimi çözümü tarafından yönetilir.  
2. Azure portalında, **Otomasyon hesabı** ekranından Otomasyon hesabınızı seçin ve [Azure portalıyla yeni bir değişken oluşturmak için](../automation/automation-variables.md#to-create-a-new-variable-with-the-azure-portal) adımlarını izleyerek **true** değerine sahip **UseOMSForSCCMUpdates** adlı boole türünde bir değişken oluşturun.
3. OMS portalında Güncelleştirme Yönetimi panosunu açın.  [Güncelleştirme Dağıtımı Oluşturma](../operations-management-suite/oms-solution-update-management.md#creating-an-update-deployment) içinde açıklanan adımları izleyerek yeni bir dağıtım oluşturun ve açılır listeden OMS bilgisayar grubu olarak ifade edilen uygun Configuration Manager koleksiyonunu seçin.  Aşağıdaki önemli noktaları göz önünde bulundurun:
    1. Seçili Configuration Manager cihaz koleksiyonunda bir bakım penceresi tanımlanmışsa, koleksiyonun üyeleri OMS’deki zamanlanmış dağıtımda tanımlanan **Süre** ayarı yerine bunu kullanır.
    2. Hedef koleksiyonun üyeleri İnternet bağlantısına sahip olmalıdır (doğrudan veya proxy sunucusu ya da OMS Ağ Geçidi aracılığıyla).  

OMS çözümüyle güncelleştirme dağıtımını tamamladıktan sonra, seçili bilgisayar grubunun üyesi olan hedef bilgisayarlar zamanlanan saatte yerel istemci önbelleğinden güncelleştirmeleri yükler.  Dağıtımınızın sonuçlarını izlemek için [güncelleştirme dağıtım durumunu görüntüleyebilirsiniz](../operations-management-suite/oms-solution-update-management.md#viewing-update-deployments).  

### <a name="manage-software-updates-from-oms"></a>OMS’den yazılım güncelleştirmelerini yönetme

Configuration Manager istemcisi olan Windows Server VM’lerinin güncelleştirmelerini yönetmek için, istemci ilkesini bu çözüm tarafından yönetilen tüm istemcilere ait Yazılım Güncelleştirme Yönetimi özelliğini devre dışı bırakacak şekilde yapılandırmanız gerekir.  Varsayılan olarak, istemci ayarları hiyerarşideki tüm cihazları hedefler.  Bu ilke ayarı ve nasıl yapılandırılacağı hakkında daha fazla bilgi için [System Center Configuration Manager'da istemci ayarlarını yapılandırma](https://docs.microsoft.com/sccm/core/clients/deploy/configure-client-settings) makalesini inceleyin.  

Bu yapılandırma değişikliğini uyguladıktan sonra, [Güncelleştirme Dağıtımı Oluşturma](../operations-management-suite/oms-solution-update-management.md#creating-an-update-deployment) içinde açıklanan adımları izleyerek yeni bir dağıtım oluşturun ve açılır listeden OMS bilgisayar grubu olarak ifade edilen uygun Configuration Manager koleksiyonunu seçin. 

