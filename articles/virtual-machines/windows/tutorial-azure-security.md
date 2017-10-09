---
title: "azure'da aaaAzure Güvenlik Merkezi ve Windows sanal makineler | Microsoft Docs"
description: "Azure Güvenlik Merkezi ile Azure Windows sanal makineniz için güvenlik hakkında bilgi edinin."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/01/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 238bf4e266a24a536d35dd647db6056ab39a1f1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a>Azure Güvenlik Merkezi'ni kullanarak sanal makine güvenlik izleme

Azure Güvenlik Merkezi güvenlik uygulamaları, Azure kaynak görünürlük elde size yardımcı olabilir. Güvenlik Merkezi, tümleşik güvenlik izleme sunar. Kaçabilecek tehditleri algılayabilir. Bu öğreticide, Azure Güvenlik Merkezi hakkında bilgi edinmek ve nasıl yapılır:
 
> [!div class="checklist"]
> * Veri toplamayı ayarlama
> * Güvenlik ilkeleri Ayarla
> * Görüntüleme ve yapılandırma sistem durumu sorunları giderin
> * Algılanan tehditler gözden geçirin  

## <a name="security-center-overview"></a>Güvenlik Merkezi'ne genel bakış

Güvenlik Merkezi olası sanal makine (VM) yapılandırma sorunları tanımlar ve güvenlik tehditlerini hedeflenen. Bu ağ güvenlik grupları, şifrelenmemiş diskleri ve kaba kuvvet Uzak Masaüstü Protokolü (RDP) saldırıları eksik olan VM'ler içerebilir. Merhaba bilgiler kolay okunur grafiklerde hello Güvenlik Merkezi panosunda görüntülenir.

tooaccess hello Güvenlik Merkezi panosunda hello hello menüsünde select Azure portal **Güvenlik Merkezi**. Merhaba Panoda Azure ortamınıza hello güvenlik durumunu görmek, geçerli önerileri sayısını bulun ve tehdit uyarıları hello geçerli durumunu görüntülemek. Daha fazla ayrıntı her üst düzey grafik toosee genişletebilirsiniz.

![Güvenlik Merkezi Panosu](./media/tutorial-azure-security/asc-dash.png)

Güvenlik Merkezi veri bulma tooprovide önerileri algıladığı sorunların ötesinde gider. Örneğin, bir VM bir bağlı ağ güvenlik grubu dağıttıysanız, Güvenlik Merkezi ile yapabileceğiniz düzeltme adımları bir öneri görüntüler. Güvenlik Merkezi Merhaba içeriğine ayrılmadan otomatik düzeltme alın.  

![Öneriler](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a>Veri toplamayı ayarlama

VM Güvenlik yapılandırmaları görünürlük sağlayabilmek için önce Güvenlik Merkezi veri toplama yukarı tooset gerekir. Bu, veri koleksiyonu açık kapatarak ve bir Azure depolama hesabı toohold toplanan verileri oluşturma içerir. 

1. Merhaba Güvenlik Merkezi panosunda tıklatın **Güvenlik İlkesi**, aboneliğinizi seçin. 
2. İçin **veri toplama**seçin **üzerinde**.
3. toocreate bir depolama hesabı seçin **depolama hesabı seç**. Ardından, seçin **Tamam**.
4. Merhaba üzerinde **Güvenlik İlkesi** dikey penceresinde, select **kaydetmek**. 

Merhaba Güvenlik Merkezi veri toplama Aracısı sonra tüm Vm'lere yüklü ve veri toplama başlar. 

## <a name="set-up-a-security-policy"></a>Bir güvenlik ilkesi ayarlama

Güvenlik ilkeleri, Güvenlik Merkezi veri toplar ve öneriler sağlar kullanılan toodefine hello öğelerdir. Farklı güvenlik ilkeleri toodifferent Azure kaynaklarını kümesi uygulayabilirsiniz. Varsayılan olarak Azure kaynaklarına karşı tüm ilke öğeleri değerlendirilir rağmen tüm Azure kaynakları için veya bir kaynak grubu için tek tek ilke öğelerini devre dışı bırakabilirsiniz. Güvenlik Merkezi güvenlik ilkeleri hakkında ayrıntılı bilgi için bkz: [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](../../security-center/security-center-policies.md). 

Tüm Azure kaynakları için güvenlik ilkesi tooset:

1. Merhaba Güvenlik Merkezi panosunda seçin **Güvenlik İlkesi**, aboneliğinizi seçin.
2. Seçin **önleme İlkesi**.
3. Açma veya Azure kaynaklarını tooapply tooall istediğiniz ilke öğeleri devre dışı bırakma.
4. Ayarlarınızı seçerek tamamladığınızda seçin **Tamam**.
5. Merhaba üzerinde **Güvenlik İlkesi** dikey penceresinde, select **kaydetmek**. 

belirli bir kaynak grubunun İlkesi tooset:

1. Merhaba Güvenlik Merkezi panosunda seçin **Güvenlik İlkesi**, bir kaynak grubunu seçin.
2. Seçin **önleme İlkesi**.
3. Açma veya tooapply toohello kaynak grubu istediğiniz ilke öğeleri devre dışı bırakma.
4. Altında **DEVRALMA**seçin **benzersiz**.
5. Ayarlarınızı seçerek tamamladığınızda seçin **Tamam**.
6. Merhaba üzerinde **Güvenlik İlkesi** dikey penceresinde, select **kaydetmek**.  

Bu sayfada belirli bir kaynak grubu için verilerin toplanmasını kapatabilirsiniz.

Aşağıdaki örneğine hello adlı bir kaynak grubu için benzersiz bir ilke oluşturuldu *myResoureGroup*. Bu ilkede disk şifreleme ve web uygulaması güvenlik duvarı önerileri devre dışı bırakılmıştır.

![Benzersiz bir ilke](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a>VM yapılandırma durumunu görüntüle

Veri toplama açık ve bir güvenlik ilkesi ayarladıktan sonra Güvenlik Merkezi tooprovide uyarısı ve öneri başlar. Sanal makineleri dağıtılan gibi hello veri toplama Aracısı yüklenir. Güvenlik Merkezi hello için verilerle doldurulur sonra yeni VM'ler. VM yapılandırma sistem durumu hakkında ayrıntılı bilgi için bkz: [Güvenlik Merkezi'nde, Vm'leri koruma](../../security-center/security-center-virtual-machine-recommendations.md). 

Toplanan veriler gibi her bir VM ve ilgili Azure kaynağı için hello kaynak durumu toplanır. Hello bilgiler bir kolay okunur grafiğinde gösterilir. 

tooview kaynak durumu:

1.  Merhaba Güvenlik Merkezi panosunda altında **kaynak güvenlik durumu**seçin **işlem**. 
2.  Merhaba üzerinde **işlem** dikey penceresinde, select **sanal makineleri**. Bu görünüm tüm VM'ler için hello yapılandırma durumunun bir özetini sağlar.

![İşlem durumu](./media/tutorial-azure-security/compute-health.png)

toosee bir VM için tüm öneriler hello VM seçin. Öneriler ve düzeltme hello Bu öğreticinin sonraki bölümünde daha ayrıntılı olarak ele alınmaktadır.

## <a name="remediate-configuration-issues"></a>Yapılandırma sorunlarını düzeltmek

Güvenlik Merkezi ile yapılandırma verilerini toopopulate başladıktan sonra öneriler ayarladığınız hello güvenlik ilkesine göre yapılır. Örneğin, bir VM ilişkili ağ güvenlik grubu olmadan ayarlarsanız, bir öneri toocreate bir yapılır. 

toosee tüm önerilerin bir listesi: 

1. Merhaba Güvenlik Merkezi panosunda seçin **önerileri**.
2. Belirli bir öneri seçin. Kendisi için tüm kaynakların hello öneri geçerli bir listesi görüntülenir.
3. tooapply bir öneri, belirli bir kaynak seçin. 
4. Düzeltme adımları Hello yönergeleri izleyin. 

Çoğu durumda, Güvenlik Merkezi işlem yapılabilir adımları sağlar. Güvenlik Merkezi ayrılmadan bir öneri tooaddress alabilir. Aşağıdaki örneğine hello sınırsız bir gelen kuralı sahip bir ağ güvenlik grubu Güvenlik Merkezi algılar. Merhaba öneri sayfasında hello seçebilirsiniz **gelen kuralları Düzenle** düğmesi. Merhaba gerekli toomodify hello kural kullanıcı Arabirimi görüntülenir. 

![Öneriler](./media/tutorial-azure-security/remediation.png)

Öneriler çözümlendi olarak çözümlendi olarak işaretlenir. 

## <a name="view-detected-threats"></a>Algılanan tehditler görüntüleyin

Ayrıca tooresource yapılandırma önerileri, Güvenlik Merkezi, tehdit algılama uyarıları görüntüler. Merhaba güvenlik uyarıları özelliği her VM, Azure ağ günlükleri ve bağlı iş ortağı çözümleri toodetect güvenlik tehditlerine karşı Azure kaynaklarını toplanan verileri toplar. Güvenlik Merkezi tehdit algılaması özellikleri hakkında ayrıntılı bilgi için bkz: [Azure Güvenlik Merkezi algılama özellikleri](../../security-center/security-center-detection-capabilities.md).

Merhaba güvenlik uyarıları özelliği gerektirir hello güvenlik katmanı toobe gelen artan fiyatlandırma Merkezi *serbest* çok*standart*. 30 günlük **ücretsiz deneme sürümü** toothis fiyatlandırma katmanı daha yüksek taşıdığınızda kullanılabilir. 

toochange hello fiyatlandırma katmanı:  

1. Merhaba Güvenlik Merkezi panosunda tıklatın **Güvenlik İlkesi**, aboneliğinizi seçin.
2. Seçin **fiyatlandırma katmanı**.
3. Merhaba yeni katmanı seçin ve ardından **seçin**.
4. Merhaba üzerinde **Güvenlik İlkesi** dikey penceresinde, select **kaydetmek**. 

Fiyatlandırma katmanı hello değiştirdikten sonra güvenlik tehditleri algılandığında hello güvenlik uyarıları grafik toopopulate başlar.

![Güvenlik uyarıları](./media/tutorial-azure-security/security-alerts.png)

Bir uyarı tooview bilgileri seçin. Örneğin, hello tehdit, hello algılama zamanı, tüm tehdit girişimleri açıklamasını görmek ve önerilen düzeltme hello. Aşağıdaki örneğine hello bir RDP yanılma saldırısı, ile 294 başarısız RDP deneme algılandı. Önerilen çözüm sağlanır.

![RDP saldırısı](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a>Sonraki adımlar
Bu öğretici, Azure Güvenlik Merkezi ayarlayın ve ardından VM'ler Güvenlik Merkezi'nde gözden. Şunları öğrendiniz:

> [!div class="checklist"]
> * Veri toplamayı ayarlama
> * Güvenlik ilkeleri Ayarla
> * Görüntüleme ve yapılandırma sistem durumu sorunları giderin
> * Algılanan tehditler gözden geçirin

Toohello sonraki öğretici toolearn toocreate CI/CD kanal nasıl ile Visual Studio Team Services ve IIS çalıştıran bir Windows VM ilerleyin.

> [!div class="nextstepaction"]
> [Visual Studio Team Services CI/CD ardışık düzen](./tutorial-vsts-iis-cicd.md)
