---
title: "Azure Log Analytics ile şirketi içi Windows bilgisayarlardan veri toplama | Microsoft Docs"
description: "Azure'un dışındaki bilgisayarlarda çalıştırılan Windows için Log Analytics aracısını dağıtmayı ve Log Analytics ile veri toplamayı etkinleştirmeyi öğrenin."
services: log-analytics
documentationcenter: log-analytics
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 12/14/2017
ms.author: magoedte
ms.custom: mvc
ms.openlocfilehash: 4462276724628de09fdefb21ff0f3eb61561a09e
ms.sourcegitcommit: 3fca41d1c978d4b9165666bb2a9a1fe2a13aabb6
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/15/2017
---
# <a name="collect-data-from-windows-computers-hosted-in-your-environment"></a>Ortamınızda barındırılan Windows bilgisayarlardan verileri toplama
[Azure Log Analytics](log-analytics-overview.md), doğrudan fiziksel veya sanal Windows bilgisayarlarınızdan ve ortamınızdaki diğer kaynaklardan verileri ayrıntılı analiz ve bağıntı için tek bir depoda toplayabilir.  Bu hızlı başlangıçta birkaç kolay adımda Windows bilgisayarınızı nasıl yapılandırabileceğiniz ve veri toplayabileceğiniz gösterilmektedir.  Azure Windows VM’leri için [Azure Sanal Makineler hakkında veri toplama](log-analytics-quick-collect-azurevm.md) konusuna bakın.  

Windows aracısını dağıtmak için ağ ve sistem gereksinimleri hakkında bilgilere [Azure Log Analytics ile ortamınızdan veri toplama](log-analytics-concept-hybrid.md#prerequisites) sayfasından ulaşabilirsiniz.
 
Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.

## <a name="log-in-to-azure-portal"></a>Azure portalında oturum açın
[https://portal.azure.com](https://portal.azure.com) adresinde Azure portalında oturum açın. 

## <a name="create-a-workspace"></a>Çalışma alanı oluşturma
1. Azure portalının sol alt köşesinde bulunan **Diğer hizmetler**'e tıklayın. Kaynak listesinde **Log Analytics** yazın. Yazmaya başladığınızda liste, girişinize göre filtrelenir. **Log Analytics**’i seçin.<br><br> ![Azure portalı](media/log-analytics-quick-collect-azurevm/azure-portal-01.png)<br><br>  
2. **Oluştur**’a tıklayın, ardından şu öğeler için seçim yapın:

  * Yeni **OMS Çalışma Alanı** için *DefaultLAWorkspace* gibi bir ad sağlayın. 
  * Varsayılan seçili abonelik uygun değilse açılan listeden bağlanacak bir **Abonelik** seçin.
  * **Kaynak Grubu** için, bir veya daha fazla Azure sanal makinesi içeren mevcut bir kaynak grubunu seçin.  
  * VM’lerinizin dağıtıldığı **Konum**’u seçin.  Ek bilgi için bkz. [Log Analytics’in sunulduğu bölgeler](https://azure.microsoft.com/regions/services/).
  * Log Analytics’te üç farklı **fiyatlandırma katmanından** birini seçebilirsiniz ancak bu hızlı başlangıçta **ücretsiz** katmanı seçeceğiz.  Katmanlar hakkında daha fazla bilgi için bkz. [Log Analytics Fiyatlandırma Ayrıntıları](https://azure.microsoft.com/pricing/details/log-analytics/).

        ![Create Log Analytics resource blade](media/log-analytics-quick-collect-azurevm/create-loganalytics-workspace-01.png)<br>  
3. **OMS Çalışma Alanı** bölmesinde gerekli bilgileri girdikten sonra **Tamam**’a tıklayın.  

Bilgilerin doğrulanıp çalışma alanının oluşturulması sırasında işlemin ilerleme durumunu menüdeki **Bildirimler**’in altından izleyebilirsiniz. 

## <a name="obtain-workspace-id-and-key"></a>Çalışma alanı kimliği ve anahtarını alma
Windows için Microsoft Monitoring Agent'ı yüklemeden önce, Log Analytics çalışma alanınızın kimliği ve anahtarına ihtiyacınız olacak.  Bu bilgiler kurulum sihirbazının aracıyı düzgün bir şekilde yapılandırması ve Log Analytics ile başarılı bir şekilde iletişim kurabilmesi için gereklidir.  

1. Azure portalının sol alt köşesinde bulunan **Diğer hizmetler**'e tıklayın. Kaynak listesinde **Log Analytics** yazın. Yazmaya başladığınızda liste, girişinize göre filtrelenir. **Log Analytics**’i seçin.
2. Log Analytics çalışma alanlarınızın listesinde, daha önceden oluşturduğunuz *DefaultLAWorkspace* çalışma alanını seçin.
3. **Gelişmiş ayarlar**’ı seçin.<br><br> ![Log Analytics Gelişmiş Ayarlar](media/log-analytics-quick-collect-azurevm/log-analytics-advanced-settings-01.png)<br><br>  
4. **Bağlı Kaynaklar**’ı seçin ve ardından **Windows Sunucuları**’nı seçin.   
5. **Çalışma Alanı Kimliği** ve **Birincil Anahtar**’ın sağındaki değer. Her ikisini de kopyalayıp sık kullandığınız bir düzenleyiciye yapıştırın.   

## <a name="install-the-agent-for-windows"></a>Windows için aracıyı yükleme
Aşağıdaki adımlar, bilgisayarınızda Microsoft Monitoring Agent'ın kurulumunu kullanarak Azure'da ve Azure Kamu bulutunda Log Analytics'in aracısını yükler ve yapılandırır.  

1. **Windows Sunucuları** sayfasında, Windows işletim sisteminin işlemci mimarisine bağlı olarak indirilecek uygun **Windows Aracısını İndir** sürümünü seçin.
2. Aracıyı bilgisayarınıza yüklemek için Kurulum'u çalıştırın.
2. **Hoş Geldiniz** sayfasında **İleri**'ye tıklayın.
3. **Lisans Koşulları** sayfasında, lisansı okuyun ve **Kabul Ediyorum**'a tıklayın.
4. **Hedef Klasör** sayfasında, varsayılan yükleme klasörünü değiştirin veya koruyun ve ardından **İleri**'ye tıklayın.
5. **Aracı Kurulum Seçenekleri** sayfasında, aracıyı Azure Log Analytics'e (OMS) bağlamayı seçin ve ardından **İleri**'ye tıklayın.   
6. **Azure Log Analytics** sayfasında aşağıdakileri yapın:
   1. Daha önce kopyaladığınız **Çalışma Alanı Kimliği** ve **Çalışma Alanı Anahtarı (Birincil Anahtar)** değerlerini yapıştırın.  Bilgisayarın Azure Kamu bulutundaki bir Log Analytics çalışma alanına raporlaması gerekiyorsa, **Azure Cloud** açılan listesinden **Azure ABD Kamu**'yu seçin.  
   2. Bilgisayarın Log Analytics hizmetiyle bir ara sunucu üzerinden iletişim kurması gerekiyorsa, **Gelişmiş**'e tıklayın ve ara sunucunun URL'siyle bağlantı noktası numarasını sağlayın.  Ara sunucunuz kimlik doğrulaması gerektiriyorsa, ara sunucuyla kimlik doğrulaması yapmak için kullanıcı adını ve parolayı yazın, ardından **İleri**'ye tıklayın.  
7. Gerekli yapılandırma ayarlarını sağlamayı tamamladığınızda **İleri**'ye tıklayın.<br><br> ![Çalışma Alanı Kimliği ve Birincil Anahtarı'nı yapıştırın](media/log-analytics-quick-collect-windows-computer/log-analytics-mma-setup-laworkspace.png)<br><br>
8. **Yüklemeye Hazır** sayfasında seçimlerinizi gözden geçirin ve ardından **Yükle**'ye tıklayın.
9. **Yapılandırma başarıyla tamamlandı** sayfasında **Son**'a tıklayın.

Tamamlandığında, **Denetim Masası**'nda **Microsoft Monitoring Agent** gösterilir. Yapılandırmanızı gözden geçirebilir ve aracının Log Analytics'e bağlandığını doğrulayabilirsiniz. Bağlandığında, **Azure Log Analytics (OMS)** sekmesinde aracı şöyle bir ileti görüntüler: **Microsoft Monitoring Agent Microsoft Operations Management Suite hizmetine başarıyla bağlandı**.<br><br> ![MMA'nın Log Analytics'e bağlantı durumu](media/log-analytics-quick-collect-windows-computer/log-analytics-mma-laworkspace-status.png)

## <a name="collect-event-and-performance-data"></a>Olay ve performans verilerini toplama
Log Analytics uzun süreli analiz ve raporlama için belirttiğiniz Windows olay günlüğü ve performans sayaçlarından olayları toplayarak belirli bir koşul algılandığında işlem yapabilir.  Windows olay günlüğünden olayları toplamayı yapılandırmak ve birkaç ortak performans sayacı ile başlamak için bu adımları izleyin.  

1. Azure portalının sol alt köşesinde bulunan **Diğer hizmetler**'e tıklayın. Kaynak listesinde **Log Analytics** yazın. Yazmaya başladığınızda liste, girişinize göre filtrelenir. **Log Analytics**’i seçin.
2. **Gelişmiş ayarlar**’ı seçin.<br><br> ![Log Analytics Gelişmiş Ayarlar](media/log-analytics-quick-collect-azurevm/log-analytics-advanced-settings-01.png)<br><br> 
3. **Veri**’yi seçin ve ardından **Windows Olay Günlükleri**’ni seçin.  
4. Bir olay günlüğü eklemek için günlüğün adını yazın.  **Sistem** yazıp artı işaretine **+** tıklayın.  
5. Tabloda, **Hata** ve **Uyarı** önem derecelerini işaretleyin.   
6. Yapılandırmayı kaydetmek için sayfanın en üstünde yer alan **Kaydet**’e tıklayın.
7. Bir Windows bilgisayarda performans sayaçlarını toplamayı etkinleştirmek için **Windows Performans Verileri**’ni seçin. 
8. Yeni bir Log Analytics çalışma alanı için Windows Performans sayaçlarını ilk kez yapılandırırken, birkaç ortak sayacı hızlı bir şekilde oluşturma seçenekleri sunulur. Her birinin yanında bir onay kutusu görüntülenir.<br> ![Varsayılan Windows performans sayaçları seçildi](media/log-analytics-quick-collect-azurevm/windows-perfcounters-default.png).<br> **Seçili performans sayaçlarını ekle**’ye tıklayın.  Eklenir ve on saniye koleksiyon örnek aralığı ile ayarlanır.  
9. Yapılandırmayı kaydetmek için sayfanın en üstünde yer alan **Kaydet**’e tıklayın.

## <a name="view-data-collected"></a>Toplanan verileri görüntüleyin
Veri toplamayı etkinleştirdiyseniz, şimdi hedef bilgisayardan verileri görmek için basit bir günlük araması örneği çalıştıralım.  

1. Azure Portal'da, seçili çalışma alanının altında **Günlük Araması** kutucuğuna tıklayın.  
2. Günlük Araması bölmesinde, sorgu alanında `Perf` yazıp Enter tuşuna basın veya sorgu alanının sağındaki arama düğmesine tıklayın.<br><br> ![Log Analytics günlük araması sorgu örneği](media/log-analytics-quick-collect-linux-computer/log-analytics-portal-queryexample.png)<br><br> Örneğin, aşağıdaki resimdeki sorgu 735 Performans kaydı döndürdü.<br><br> ![Log Analytics günlük araması sonucu](media/log-analytics-quick-collect-windows-computer/log-analytics-search-perf.png)

## <a name="clean-up-resources"></a>Kaynakları temizleme
Artık gerekli olmadığında, aracıyı Windows bilgisayardan kaldırıp Log Analytics çalışma alanını silebilirsiniz.  

Aracıyı kaldırmak için aşağıdaki adımları izleyin.

1. **Denetim Masası**'nı açın.
2. **Programlar ve Özellikler**'i açın.
3. **Programlar ve Özellikler**'de **Microsoft Monitoring Agent**'ı seçin ve **Kaldır**'a tıklayın.

Çalışma alanını silmek için, önceden oluşturduğunuz Log Analytics çalışma alanını seçin ve kaynak sayfasında **Sil**’e tıklayın.<br><br> ![Log Analytics kaynağını silme](media/log-analytics-quick-collect-azurevm/log-analytics-portal-delete-resource.png)

## <a name="next-steps"></a>Sonraki adımlar
Şimdi şirket içi Linux bilgisayarınızdan işletimsel verileri ve performans verilerini topluyorsunuz ve *ücretsiz* olarak topladığınız verileri kolayca keşfetmeye, analiz etmeye ve verilerde işlem gerçekleştirmeye başlayabilirsiniz.  

Verileri görüntüleme ve analiz etmeyi öğrenmek için, öğreticiye devam edin.   

> [!div class="nextstepaction"]
> [Log Analytics’te verileri görüntüleme veya analiz etme](log-analytics-tutorial-viewdata.md)
