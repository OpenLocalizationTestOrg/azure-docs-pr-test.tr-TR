---
title: "Azure Analysis Services öğreticisi 13. ders: Dağıtma | Microsoft Docs"
description: "Azure Analysis Services’a öğretici projesinin nasıl dağıtılacağını açıklar."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/17/2017
ms.author: owend
ms.openlocfilehash: 70dbf5786262f75199270aa8009e03b9b48b8559
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="lesson-13-deploy"></a>13. Ders: Dağıtma

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Bu derste, Azure Analysis Services sunucusunun model için bir ad belirtmesini sağlayarak dağıtım özelliklerini yapılandırırsınız. Daha sonra modeli bu örneğe dağıtırsınız. Modeliniz dağıtıldıktan sonra kullanıcılar bir raporlama istemci uygulaması kullanarak modele bağlanabilir. Daha fazla bilgi için bkz. [Azure Analysis Services’a Dağıtma](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).  
  
Bu dersin tahmini tamamlanma süresi: **5 dakika**  
  
## <a name="prerequisites"></a>Ön koşullar  
Bu konu, sırayla tamamlanması gereken bir tablo modelleme öğreticisinin bir parçasıdır. Bu dersteki görevleri gerçekleştirmeden önce, bir önceki dersi tamamlamış olmanız gerekir: [12. Ders: Excel’de çözümleme](../tutorials/aas-lesson-12-analyze-in-excel.md).  

> [!IMPORTANT]  
> Uzak Analysis Services sunucusunu dağıtmak için sunucu üzerinde [Yönetici izinlerine](../analysis-services-server-admins.md) sahip olmanız gerekir.  

> [!IMPORTANT]  
> AdventureWorksDW2014 örnek veritabanını şirket içi bir SQL Server’a yüklediyseniz ve modelinizi bir Azure Analysis Services sunucusuna dağıtacaksanız [Şirket içi veri ağ geçidi](../analysis-services-gateway.md) gereklidir.
  
## <a name="deploy-the-model"></a>Modeli dağıtma  
  
#### <a name="to-configure-deployment-properties"></a>Dağıtım özelliklerini yapılandırmak için  

  
1.  **Çözüm Gezgini**’nde **AW İnternet Satışları** projesine sağ tıklayıp **Özellikler**’e tıklayın.  
  
2.  **AW İnternet Satışları Özellik Sayfaları** iletişim kutusundaki **Dağıtım Sunucusu** altında bulunan **Server** özelliğine tüm sunucuyu girin.  

    ![aas-lesson13-deploy-property](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  **Database** özelliğine **Adventure Works İnternet Satışları** yazın.  
  
4.  **Model Name** özelliğine **Adventure Works İnternet Satışları Modeli** yazın.  
  
5.  Seçimlerinizi doğrulayıp **Tamam**’a tıklayın.  
  
#### <a name="to-deploy-the-adventure-works-internet-sales"></a>Adventure Works İnternet Satışlarını dağıtmak için
  
1.  **Çözüm Gezgini**’nde **AW İnternet Satışları** projesine sağ tıklayıp **Derleme**’ye tıklayın.  

2.  **AW İnternet Satışları** projesine sağ tıklayıp **Dağıt**’a tıklayın.

    Azure Analysis Services'a dağıtım yaparken hesabınızı girmeniz istenebilir. Kuruluş hesabınızı ve parolanızı girin, örneğin nancy@adventureworks.com. Bu hesap, sunucudaki Yöneticiler grubuna üye olmalıdır.
  
    Dağıtım iletişim kutusu görünür ve burada meta veriler ile modele dahil edilen her tablonun dağıtım durumu gösterilir.  
    
    ![aas-lesson13-deploy-status](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. Dağıtım başarıyla tamamlandığında devam edin ve **Kapat**’a tıklayın.  
  
## <a name="conclusion"></a>Sonuç  
Tebrikler! İlk Analysis Services Tablo modelinizi yazma ve dağıtma işlemini tamamladınız. Bu öğretici, bir tablo modeli oluştururken en yaygın görevleri tamamlamanıza yardımcı olmuştur. Adventure Works İnternet Satışları modeliniz artık dağıtıldığına göre SQL Server Management Studio’yu kullanarak modeli yönetebilir, işlem betikleri ve bir yedek plan oluşturabilirsiniz. Kullanıcılar artık ayrıca Microsoft Excel veya Power BI gibi bir raporlama istemci uygulaması kullanarak modele bağlanabilir.  

![aas-lesson13-ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a>Sırada ne var?
[Power BI Desktop ile bağlanma](../analysis-services-connect-pbi.md)   
[Ek Ders - Dinamik güvenlik](../tutorials/aas-supplemental-lesson-dynamic-security.md)   
[Ek Ders - Ayrıntı satırları](../tutorials/aas-supplemental-lesson-detail-rows.md)   
[Ek Ders - Düzensiz hiyerarşiler](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
