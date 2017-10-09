---
title: "Power BI ile Azure Güvenlik Merkezi verilerinden aaaGet ınsights | Microsoft Docs"
description: "Hello Azure Güvenlik Merkezi Power BI içerik paketi kolay toofind güvenlik uyarılarının, önerilerin kolaylaştırır, kaynakların saldırıya ve eğilimlerin, raporlama için oluşturulmuş bir veri kümesini temel."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 0ded6bc7-52e8-43b4-8940-0bee137526e3
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: yurid
ms.openlocfilehash: af68aef626034fe03d793c36b515a3f26619e5f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-insights-from-azure-security-center-data-with-power-bi"></a>Power BI ile Azure Güvenlik Merkezi verilerinden öngörü edinme
Merhaba [Power BI panosuna](http://aka.ms/azure-security-center-power-bi) toovisualize sağlayan Azure Güvenlik Merkezi için çözümleme ve öneriler ve güvenlik uyarılarını her yerden, mobil cihazınız dahil filtre. Desenler - kaynak veya kaynak IP adresine göre güvenlik uyarılarını ve kaynak ya da yaşa göre olmayan güvenlik risklerini saldırılara ve Hello Power BI Panosu tooreveal eğilimleri kullanın.

Ayrıca, Güvenlik Merkezi önerilerini ve güvenlik uyarılarını, örneğin [Azure Denetim Günlükleri](https://powerbi.microsoft.com/blog/monitor-azure-audit-logs-with-power-bi/) ve [Azure SQL Veritabanı Denetimi](https://powerbi.microsoft.com/blog/monitor-your-azure-sql-database-auditing-activity-with-power-bi/)’nden alınan verileri kullanarak, ilginç bir şekilde diğer verilerle birleştirebilirsiniz. Her ikisi de Power BI panolarını sunan ve kolay bulut kaynaklarınızın güvenlik durumuna hello raporlama için bu veri tooExcel dışarı aktarabilirsiniz.

## <a name="using-azure-security-center-dashboard-tooaccess-power-bi"></a>Azure Güvenlik Merkezi Panosu tooaccess Power BI kullanma
Hello Azure Güvenlik Merkezi Panosu tooaccess Power BI raporları de kullanabilirsiniz. Bu görev Hello adımları tooperform izleyin:

1. Merhaba, **Azure Güvenlik Merkezi** panoyu tıklatın **Power BI** düğmesi.

    ![TooAzure Güvenlik Merkezi Power BI kullanarak bağlan](./media/security-center-powerbi/security-center-powerbi-fig1-1-newUI-2017.png)
2. Merhaba **Power BI** hello ekran aşağıdaki gösterildiği gibi hello sağ tarafta bir dikey pencere açılır:

    ![TooAzure Güvenlik Merkezi Power BI kullanarak bağlan](./media/security-center-powerbi/security-center-powerbi-fig1-new11-2017.png)
3. Merhaba hello Power BI panosunu ilk kez oluşturuyorsanız, hello aşağıdaki seçenekleri hello seçebilirsiniz **Power bı'da araştırma** dikey penceresinde:

   * **Güvenlik öngörüleri Panosu**: toocreate güvenlik durumunu, tehditleri ve algılamaları içeren bir Pano istiyorsanız bu seçeneği belirleyin. Bu seçenek, aboneliklerde algılanan uyarıları ve koruma durumlarını çözümlemekle sorumlu olan DevOps rolü için daha yaygın kullanılan bir seçenektir.
   * **İlke yönetimi Panosu**: tooexplore yönetim ve zorlama ilkesini istiyorsanız bu seçeneği belirleyin.  Bu seçenek, daha çok idare üzerine odaklanan Merkezi BT için yaygın kullanılan bir seçenektir. Bunlar bu Pano toogain görünürlük ve öngörü güvenlik ilkesi uygunluğuna kuruluşlarındaki kullanabilirsiniz.
   * Power BI Panosu zaten varsa, tıklatın **Git tooyour geçerli Power BI panosuna**.
4. Bu örnek için **Güvenlik öngörüleri panosu** seçeneğine tıklayın. Bu hello ilk kez kullanıyorsanız, Güvenlik Merkezi olduğunuz tooinstall hello içerik paketi istenir için Power BI panosuna oluşturuyorsunuz. Tıklatın **almak** hello düğmesini **için Power BI içerik paketleri** hello ekran aşağıdaki gösterildiği gibi penceresi:

    ![Azure Güvenlik Merkezi Güvenlik Öngörüleri panosu](./media/security-center-powerbi/security-center-powerbi-fig1-new3.png)
5. Merhaba **tooAzure Güvenlik Merkezi güvenlik öngörüleri bağlanmak** penceresi görünür. Merhaba emin olun **kimlik doğrulaması** yöntemi **oAuth2** aşağıda gösterildiği gibi tıklatıp **oturum** düğmesi.

    ![Kimlik Doğrulaması](./media/security-center-powerbi/security-center-powerbi-fig1-new4.png)
6. Tooauthenticate yeniden Azure kimlik bilgilerinizle istenebilir. Kimlik doğrulamasından sonra panonuz oluşturulur. Merhaba Pano oluşturulduktan sonra hello ekran aşağıdaki gösterildiği gibi hello benzer yapıya sahip bir rapor bakın:

    ![Power BI Panosu](./media/security-center-powerbi/security-center-powerbi-fig1-new5.png)

> [!NOTE]
> Merhaba rapor yenileme, günlük olarak zamanlanan tootake yerdir. Bu yenilemede bir hatasıyla karşılaşan durumda okuma [hello Azure Güvenlik Merkezi Power BI ile olası yenileme sorunları](https://blogs.msdn.microsoft.com/azuresecurity/2016/04/07/azure-security-center-power-bi-refresh-fails/), hakkında daha fazla bilgi için tootroubleshoot.
>
>

Burada VM'ler, Azure SQL veritabanı ve Azure Güvenlik Merkezi tarafından izlenen ağ kaynaklarına hello sayısı yanı sıra güvenlik uyarısı ve öneri hello sayısını görebilirsiniz.

Bağlantı tooAzure Güvenlik Merkezi, Azure portal toohello yönlendirir. Merhaba grafikleri kolay toovisualize bilgilerini güvenlik önerileri ve uyarılar, dahil olmak üzere kolaylaştırır:

* Kaynak Güvenlik Durumu
* Bekleyen Öneriler
* VM Önerileri
* Süreçteki Uyarılar
* Saldırıya Uğrayan Kaynaklar
* Saldırıya Uğrayan IP'ler

Her grafiğin arkasında ek öngörüler vardır. Döşeme toosee daha fazla bilgi seçin. Örneğin, hello **kaynak güvenlik durumu** kutucuğunda gösterilir ek ayrıntılar hakkında öneriler kaynaklar tarafından hello ekran aşağıdaki gösterildiği gibi:

![Öneriler](./media/security-center-powerbi/security-center-powerbi-fig1-new6.png)

Bu grafikteki herhangi bir satıra tıklarsanız, hello başkalarının toogray çıkışı ve odaklanmanıza yalnızca bir seçtiğiniz hello üzerinde adımıdır. tooreturn toohello Pano tıklatın **Azure Güvenlik Merkezi** hello altında **panolar** bu sayfanın hello sol bölmedeki seçeneği.

> [!NOTE]
> Toocustomize isterseniz, raporlarınızı ilave alanlar ekleyerek veya var olan görselleri değiştirerek hello raporu düzenleyebilirsiniz. Daha fazla bilgi için [Power BI'da Görünüm Düzenleme seçeneğindeki bir rapor ile etkileşimde bulunma](https://powerbi.microsoft.com/documentation/powerbi-service-interact-with-a-report-in-editing-view/) bölümünü okuyun.
>
>

Merhaba **süreçteki uyarı, Saldırıya uğrayan kaynaklar** ve **saldırgan IP'ler** döşeme her biri, üzerine tıkladığınızda hello benzer bir çıktıya sahiptir. Merhaba rapor bu üç değişkenin ilgili bilgileri toplar ve çağırır Bunun nedeni **Saldırıya uğrayan kaynaklar** hello ekran aşağıdaki gösterildiği gibi:

![Saldırıya uğrayan kaynaklar](./media/security-center-powerbi/security-center-powerbi-fig1-new7.png)

Bu noktada Ayrıca bu raporun bir kopyasını kaydetmek, yazdırmak veya hello hello seçenekleri kullanarak hello Web'de Yayımlama **dosya** menüsü.

![Dosya menüsü](./media/security-center-powerbi/security-center-powerbi-fig8.png)

## <a name="exploring-your-azure-security-center-data-with-power-bi-services"></a>Power BI hizmetleri ile Azure Güvenlik Merkezi verilerinizi araştırma
Toohello bağlanmak [Power BI içerik paketi Hizmetleri](https://msit.powerbi.com/groups/me/getdata/services) Power bı'da ve aşağıdaki adımları hello yürütün:

1. Merhaba, **Power BI için içerik paketi** penceresi aşağıda gösterildiği gibi iki seçenek görürsünüz.

    ![Power BI için içerik paketi](./media/security-center-powerbi/security-center-powerbi-fig1-new.png)

   > [!NOTE]
   > Zaten bu makalenin ilk bölümü hello yürütülürse Azure Güvenlik Merkezi ilke yönetimi, yalnızca bir seçeneğini görürsünüz.
   >
   >
2. Bu örnek Hello amaçla tıklatın **almak** hello içinde **Azure Güvenlik Merkezi ilke yönetimi** döşeme.
3. Merhaba, **tooAzure Güvenlik Merkezi ilke yönetimi bağlanmak** penceresinde, yapma emin tooselect **oAuth2** altında **kimlik doğrulama yöntemini** aşağıda gösterildiği gibi aşağı bırakın ve'ı tıklatın **Oturum** düğmesi.

    ![İlke Yönetimi penceresi](./media/security-center-powerbi/security-center-powerbi-fig1-new8.png)
4. Burada, tooconnect tooAzure Güvenlik Merkezi'ni kullanma hello kimlik bilgilerini yazmanız gereken yeniden yönlendirilen tooan kimlik doğrulaması sayfası olacaktır. Merhaba kimlik doğrulama işlemi tamamlandıktan sonra Power BI veri toobuild içeri aktarmaya raporlarınızı başlar. Bu süre boyunca hello sağ köşesindeki tarayıcınız üzerinde iletiden hello görebilirsiniz:

    ![TooAzure Güvenlik Merkezi Power BI kullanarak bağlan](./media/security-center-powerbi/security-center-powerbi-fig4.png)

   > [!NOTE]
   > ilk kez Merhaba Hello Pano oluşturulduğunda çoğunlukla birden fazla aboneliğine sahip olduğu senaryolar için normalden daha uzun sürebilir.
   >
   >
5. Merhaba işlemi tamamlandıktan sonra Azure Güvenlik Merkezi Power BI panonuz hello ile yükleyecek **İlkesi Yönetimi** benzer toohello aşağıda gösterilene bildirin:

    ![İlke Yönetimi panosu](./media/security-center-powerbi/security-center-powerbi-fig1-new9.png)

## <a name="see-also"></a>Ayrıca bkz.
Bu belgede, nasıl öğrenilen toouse Azure Güvenlik Merkezi'nde Power BI. Azure Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi planlama ve işlemler Kılavuzu](security-center-planning-and-operations-guide.md) — öğrenin nasıl tooplan Azure Güvenlik Merkezi'ni benimsemeyi.
* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) — öğrenin nasıl tooconfigure Azure Güvenlik Merkezi'nde güvenlik ayarları
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) — öğrenin nasıl toomanage ve yanıt toosecurity uyarıları
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) — hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz
* [Azure Güvenlik Blogu](http://blogs.msdn.com/b/azuresecurity/) - Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz
