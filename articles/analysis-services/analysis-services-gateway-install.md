---
title: "aaaInstall şirket içi veri ağ geçidi | Microsoft Docs"
description: "Bilgi nasıl tooinstall ve bir şirket içi veri ağ geçidi yapılandırın."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/22/2017
ms.author: owend
ms.openlocfilehash: e2878bf765c82910d452ae2cdd9264a343ec1990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a>Yükleme ve bir şirket içi veri ağ geçidi yapılandırma
Bir veya daha fazla Azure Analysis Services sunucuları aynı hello olduğunda bir şirket içi veri ağ geçidi gereklidir bölge tooon içi veri kaynaklarına bağlanın. toolearn hello ağ geçidi hakkında daha fazla bilgi görmek [şirket içi veri ağ geçidi](analysis-services-gateway.md).

## <a name="prerequisites"></a>Ön koşullar
**En düşük gereksinimler:**

* .NET 4.5 framework
* 64 bit sürümü Windows 7 / Windows Server 2008 R2 (veya üstü)

**Önerilen:**

* 8 çekirdekli CPU
* 8 GB bellek
* 64 bit sürümü Windows 2012 R2'in (veya üstü)

**Önemli noktalar:**

* Ağ geçidiniz Azure ile kaydedilirken Kurulum sırasında hello varsayılan bölge aboneliğiniz için seçilir. Farklı bir bölgeye seçebilirsiniz. Birden çok bölgede sunucularınız varsa, her bölge için bir ağ geçidi yüklemeniz gerekir. 
* Merhaba ağ geçidi etki alanı denetleyicisine yüklenemez.
* Yalnızca bir ağ geçidi tek bir bilgisayara yüklenebilir.
* Merhaba ağ geçidi üzerinde kalır ve toosleep geçmez bir bilgisayara yükleyin.
* Merhaba ağ geçidi, bir bilgisayar kablosuz olarak bağlı tooyour ağda yüklemeyin. Performans yayınladıklarını.


## <a name="download"></a>İndirme
 [Merhaba ağ geçidini indirin](https://aka.ms/azureasgateway)

## <a name="install"></a>Yükleme

1. Kur'u yeniden çalıştırın.

2. Bir konum seçin, hello koşullarını kabul edin ve ardından **yükleme**.

   ![Konum ve Lisans Koşulları'nı yükleme](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. Seçin **şirket içi veri ağ geçidi (önerilen)**. Azure Analysis Services kişisel modunu desteklemiyor.

   ![Ağ geçidi türünü seçin](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. Bir hesap toosign tooAzure girin. Merhaba hesabı kiracınıza ait Azure Active Directory'de olmalıdır. Bu hesap hello Ağ Geçidi Yöneticisi için kullanılır. 

   ![Bir hesap toosign tooAzure içinde girin](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > Bir etki alanı hesabıyla oturum açın, olacaktır Azure AD'de tooyour kuruluş hesabıyla eşlenir. Kuruluş hesabınızla hello hello Ağ Geçidi Yöneticisi olarak kullanılır.

## <a name="register"></a>Kaydetme
Sipariş toocreate Azure bir ağ geçidi kaynağı'da, ağ geçidi bulut Hizmeti'ne hello ile yüklü hello yerel örneği kaydetmeniz gerekir. 

1.  Seçin **bu bilgisayarda yeni bir ağ geçidini kaydetmek**.

    ![Kaydolma](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. Ağ geçidiniz için bir ad ve kurtarma anahtarı yazın. Varsayılan olarak, aboneliğiniz varsayılan bölge hello ağ geçidi kullanır. Tooselect farklı bir bölgeye gereksinim duyarsanız, seçin **değişikliğin bölgesini**.

   ![Kaydolma](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <a name="create-resource"></a>Bir Azure ağ geçidi kaynağı oluşturma
Yüklenen ve ağ geçidiniz kaydedilen sonra Azure aboneliğinizde toocreate bir ağ geçidi kaynağı gerekir. TooAzure hello ile aynı oturum açma hello ağ geçidi kaydederken kullanılan hesap.

1. Azure portalında tıklatın **yeni bir hizmet Oluştur** > **Kurumsal tümleştirme** > **şirket içi veri ağ geçidi**  >   **Oluşturma**.

   ![Bir ağ geçidi kaynağı oluşturun](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. İçinde **oluşturma bağlantı ağ geçidi**, bu ayarları girin:

    * **Ad**: ağ geçidi kaynağı için bir ad girin. 

    * **Abonelik**: seçin, ağ geçidi kaynağı ile Azure aboneliği tooassociate hello. 
    Bu abonelik olmalıdır hello sunucularıdır içinde aynı abonelik.
   
      Merhaba varsayılan abonelik hello toosign içinde kullanılan Azure hesabı temel alır.

    * **Kaynak grubu**: Kaynak grubu oluşturun veya mevcut bir kaynak grubunu seçin.

    * **Konum**: Select hello bölge, ağ geçidi kayıtlı.

    * **Yükleme adı**: ağ geçidi yüklemenizi seçili değilse, select hello ağ geçidi kayıtlı. 

    İşiniz bittiğinde tıklatın **oluşturma**.

## <a name="connect-servers"></a>Sunucuları toohello ağ geçidi kaynağına bağlanma

1. Azure Analysis Services sunucusu genel bakışta tıklatın **şirket içi veri ağ geçidi**.

   ![Sunucu toogateway Bağlan](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. İçinde **bir şirket içi veri ağ geçidi tooconnect çekme**, ağ geçidi kaynağı seçin ve ardından **Bağlan seçilen ağ geçidi**.

   ![Sunucu toogateway kaynak Bağlan](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > Ağ geçidiniz hello listede görünmüyorsa, sunucusu olası değil hello hello ağ geçidi kaydedilirken belirtilen hello bölge ile aynı bölgeye. 

Bu kadar. Tooopen bağlantı noktaları gerekir ya da sorun giderme yapın, çıkışı emin toocheck olması [şirket içi veri ağ geçidi](analysis-services-gateway.md).

## <a name="next-steps"></a>Sonraki adımlar
* [Çözümleme Hizmetleri yönetme](analysis-services-manage.md)   
* [Azure Analysis Services Veri Al](analysis-services-connect.md)
