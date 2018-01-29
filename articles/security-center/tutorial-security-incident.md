---
title: "Azure Güvenlik Merkezi Öğreticisi - Güvenlik olaylarına yanıt verme| Microsoft Docs"
description: "Azure Güvenlik Merkezi Öğreticisi - Güvenlik olaylarına yanıt verme"
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 181e3695-cbb8-4b4e-96e9-c4396754862f
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/07/2018
ms.author: yurid
ms.custom: mvc
ms.openlocfilehash: b6adf4bec2d9f92ee3cde9c73a03beb5a58c3f3f
ms.sourcegitcommit: 6fb44d6fbce161b26328f863479ef09c5303090f
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/10/2018
---
# <a name="tutorial-respond-to-security-incidents"></a>Öğretici: Güvenlik olaylarına yanıt verme
Güvenlik Merkezi, kötü amaçlı etkinlikler konusunda sizi uyarmak için gelişmiş analiz ve tehdit zekasından yararlanarak hibrit bulut iş yüklerinizi sürekli olarak analiz eder. Buna ek olarak, diğer güvenlik ürünleri ve hizmetleri tarafından sağlanan uyarıları Güvenlik Merkezi ile tümleştirebilir ve kendi göstergelerinizi ya da zeka kaynaklarınızı temel alan özel uyarılar oluşturabilirsiniz. Bir uyarı oluşturulduktan sonra sorunun incelenip düzeltilmesi için hemen harekete geçilmesi gerekir. Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:

> [!div class="checklist"]
> * Güvenlik uyarılarını önceliklendirme
> * Bir güvenlik olayını daha iyi araştırarak olayın kök nedenini ve kapsamını belirleme
> * Araştırmaya yardımcı olması için güvenlik verilerinde arama yapma

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/) oluşturun.

## <a name="prerequisites"></a>Önkoşullar
Bu öğreticide ele alınan özellikleri adım adım görmek için Güvenlik Merkezi’nin Standart fiyatlandırma katmanında olmanız gerekir. Güvenlik Merkezi Standart katmanını ilk 60 gün boyunca hiçbir ücret ödemeden deneyebilirsiniz. [Azure aboneliğinizi Güvenlik Merkezi Standart katmanına ekleme](security-center-get-started.md) başlıklı hızlı başlangıçta Standart katmanına nasıl yükseltebileceğiniz adım adım açıklanmıştır.

## <a name="triage-security-alerts"></a>Güvenlik uyarılarını önceliklendirme
Güvenlik Merkezi, tüm güvenlik uyarılarının birleşik bir görünümünü sağlar. Güvenlik uyarıları önem derecesi temel alınarak sıralanır ve mümkün olduğunda ilgili uyarılar bir güvenlik olayı altında birleştirilir. Uyarı ve olayları önceliklendirirken şunları yapmalısınız:

- Ek eylem gerektirmeyen uyarıları (örneğin, uyarı hatalı pozitif bir sonuçsa) kapatın
- Bilinen saldırıları gidermek için eylem gerçekleştirin (örneğin, kötü amaçlı bir IP adresinden gelen ağ trafiğini engelleme)
- Daha fazla araştırma gerektiren uyarıları belirleyin


1. Güvenlik Merkezi’nin ana menüsündeki **ALGILAMA** bölümünden **Güvenlik uyarıları**’nı seçin:

  ![Güvenlik uyarıları](./media/tutorial-security-incident/tutorial-security-incident-fig1.png)  

2. Çeşitli uyarıların birleşiminden oluşan bir güvenlik olayı hakkında daha fazla bilgi edinmek için uyarı listesinden ilgili olaya tıklayın. **Güvenlik olayı algılandı** ekranı açılır.

  ![Güvenlik olayı](./media/tutorial-security-incident/tutorial-security-incident-fig2.png)

3. Bu ekranın üst kısmında güvenlik olayının açıklaması, geri kalanında da bu olayın birer parçası olan uyarıların listesi yer alır. Daha fazla bilgi edinmek için daha iyi araştırmak istediğiniz uyarıya tıklayın.

  ![Güvenlik olayı](./media/tutorial-security-incident/tutorial-security-incident-fig3.png)

  Uyarı türü değişkenlik gösterebilir, uyarı türü ve olası düzeltme adımları hakkında daha ayrıntılı bilgi için bkz. [Azure Güvenlik Merkezi'ndeki güvenlik uyarılarını anlama](https://docs.microsoft.com/azure/security-center/security-center-alerts-type). Güvenli bir şekilde kapatılabilen uyarılar için uyarıya sağ tıklayıp **Kapat**’ı seçebilirsiniz:

  ![Uyarı](./media/tutorial-security-incident/tutorial-security-incident-fig4.png)

4. Kötü amaçlı etkinliğin kök nedeni ve kapsamı bilinmiyorsa araştırmaya devam etmek üzere bir sonraki adıma geçin.

## <a name="investigate-an-alert-or-incident"></a>Bir uyarıyı veya olayı araştırma
1. **Güvenlik uyarısı** sayfasında **Araştırma başlat** düğmesine tıklayın (zaten araştırma başlattıysanız düğme adı **Araştırmaya devam et** olarak değişir).

  ![Araştırma](./media/tutorial-security-incident/tutorial-security-incident-fig5.png)

  Araştırma haritası, bu güvenlik uyarısı veya olayı ile bağlantılı varlıkların grafik tabanlı temsilidir. Haritadaki bir varlığa tıklandığında bu varlıkla ilgili bilgiler tarafından yeni varlıklar görüntülenir ve harita genişler. Haritada seçilen varlığın özellikleri sayfanın sağ tarafındaki bölmede vurgulanır. Her sekmede sunulan bilgiler seçili varlığa göre değişkenlik gösterir. Araştırma sırasında saldırganın davranışlarını daha iyi anlamak için tüm ilgili bilgileri gözden geçirin.

2. Daha fazla kanıt bulmanız veya araştırma sırasında bulunan varlıkları daha iyi araştırmanız gerekiyorsa bir sonraki adıma geçin.

## <a name="search-data-for-investigation"></a>Araştırma için verilerde arama yapma

Güvenlik Merkezi’ndeki arama özelliklerini kullanarak güvenliği ihlal edilmiş sistemlere ilişkin daha fazla kanıt bulmanın yanı sıra araştırma kapsamındaki varlıklar hakkında daha ayrıntılı bilgi edinebilirsiniz.

Arama gerçekleştirmek için **Güvenlik Merkezi** panosunu açın, sol gezinti bölmesinden **Ara**’ya tıklayın, aramak istediğiniz varlıkları içeren çalışma alanını seçin, arama sorgusunu yazın ve Ara düğmesine tıklayın.

## <a name="clean-up-resources"></a>Kaynakları temizleme
Bu koleksiyondaki diğer hızlı başlangıçlar ve öğreticiler bu hızlı başlangıcı temel alır. Sonraki hızlı başlangıç ve öğreticilerle çalışmaya devam etmeyi planlıyorsanız Standart katmanını çalıştırmaya devam edin ve otomatik sağlamayı etkinleştirilmiş halde tutun. Devam etmeyi planlamıyorsanız veya Ücretsiz katmanına dönmek istiyorsanız:

1. Güvenlik Merkezi ana menüsüne dönüp **Güvenlik İlkesi**’ni seçin.
2. Ücretsiz katmanına döndürmek istediğiniz aboneliği veya ilkeyi seçin. **Güvenlik ilkesi** açılır.
3. **İLKE BİLEŞENLERİ** altında **Fiyatlandırma katmanı**’nı seçin.
4. Aboneliği Standart katmanından Ücretsiz katmanına geçirmek için **Ücretsiz**’i seçin.
5. **Kaydet**’i seçin.

Otomatik sağlamayı devre dışı bırakmak istiyorsanız:

1. Güvenlik Merkezi ana menüsüne dönüp **Güvenlik ilkesi**’ni seçin.
2. Otomatik sağlamayı hangi abonelik için devre dışı bırakmak istediğinizi belirtin.
3. Otomatik sağlamayı kapatmak için **Güvenlik ilkesi – Veri Toplama** altındaki **Ekleme** bölümünden **Kapalı**’yı seçin.
4. **Kaydet**’i seçin.

>[!NOTE]
> Otomatik sağlama devre dışı bırakıldığında Microsoft Monitoring Agent’ın sağlandığı Azure VM’lerinden aracı kaldırılmaz. Otomatik sağlamanın devre dışı bırakılması, kaynaklarınızın güvenliğinin izlenmesini kısıtlar.
>

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, aşağıdaki gibi güvenlik olaylarına yanıt vermek için kullanılacak Güvenlik Merkezi özelliklerini öğrendiniz:

> [!div class="checklist"]
> * Bir kaynak için ilgili uyarıların birleştirilmesinden oluşan güvenlik olayı
> * Bir güvenlik uyarısı veya olayı ile bağlantılı varlıkların grafik tabanlı temsili olan Araştırma haritası
> * Güvenliği ihlal edilmiş sistemlere ilişkin daha fazla kanıt bulmak için arama özellikleri

Güvenlik Merkezi’nin araştırma özelliği hakkında daha fazla bilgi edinmek için bkz.

> [!div class="nextstepaction"]
> [Olayları ve uyarıları araştırma](security-center-investigation.md)
