---
title: "Azure Güvenlik Merkezi'nde güvenlik uyarılarını aaaHandling | Microsoft Docs"
description: "Bu belge toouse Azure Güvenlik Merkezi özellikleri toohandle güvenlik olaylarına yardımcı olur."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: e8feb669-8f30-49eb-ba38-046edf3f9656
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: edb911c298a2ce93cd0ea5b22ce002005040090f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="handling-security-incidents-in-azure-security-center"></a>Azure Güvenlik Merkezi’nde Güvenlik Olaylarını İşleme
Önceliklendirme ve güvenlik uyarıları İnceleme olabilir zaman bile hello en becerikli güvenlik analistleri için alıcı ve çoğu için sabit tooeven bilmeniz nerede olduğu toobegin. Kullanarak [analytics](security-center-detection-capabilities.md) ayrı arasında tooconnect hello bilgi [güvenlik uyarıları](security-center-managing-and-responding-alerts.md), Güvenlik Merkezi, bir saldırı kampanya tek bir görünümünü sağlayabilir ve ilişkili tüm hello uyarılar – yapabilecekleriniz hızlı bir şekilde hangi eylemleri hello saldırgan sürdü ve hangi kaynaklara etkilendiğini anlayın.

Bu belge nasıl toouse güvenlik uyarısı Güvenlik Merkezi tooassist özelliği, güvenlik olaylarını işleme açıklanır.

## <a name="what-is-a-security-incident"></a>Güvenlik olayı nedir?
Güvenlik Merkezi'nde bir güvenlik olayı, bir kaynağın [sonlandırma zinciri](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) desenleri ile hizalanan tüm uyarılarının toplamıdır. Olaylar görünür hello [güvenlik uyarıları](security-center-managing-and-responding-alerts.md) döşeme ve dikey. Bir olay, tooobtain sağlayan hello ilgili uyarıların listesi, her oluşumu hakkında daha fazla bilgi görüntüleyebilirsiniz.

## <a name="managing-security-incidents"></a>Güvenlik olaylarını yönetme
Hello güvenlik uyarıları kutucuğuna bakarak geçerli güvenlik olayları gözden geçirebilirsiniz. Hello Azure portalına erişmek ve her güvenlik olay hakkında daha fazla ayrıntı toosee hello adımları izleyin:

1. Merhaba Güvenlik Merkezi panosunda hello görürsünüz **güvenlik uyarıları** döşeme.

    ![Güvenlik Merkezi'nde güvenlik uyarıları kutucuğu](./media/security-center-incident/security-center-incident-fig1.png)

2. Bu kutucuğu tooexpand ve bir güvenlik olayı algılandığında varsa, aşağıda gösterildiği gibi hello güvenlik uyarıları grafik altında görünür tıklatın:

    ![Güvenlik olayı](./media/security-center-incident/security-center-incident-fig2.png)

3. Karşılaştırıldığında, tooother uyarıları Hello güvenlik olay açıklaması farklı bir simge sahip olmadığına dikkat edin. ' I tıklatın, üzerinde tooview bu olay hakkında daha ayrıntılı.

    ![Güvenlik olayı](./media/security-center-incident/security-center-incident-fig3.png)

4. Merhaba üzerinde **olay** daha görürsünüz dikey geçerli durumunu (, bu durumda yüksek olan), önem derecesi, tam açıklamasını içerir, bu güvenlik olay hakkında ayrıntıları (Bu durumda hala olduğunu *etkin*, hangi hello kullanıcı anlamına gelir, bir eylem tooit gerçekleştirilecek kurmadı - bu hello olay hello içinde sağ tıklayarak yapılabilir **güvenlik uyarıları** dikey), hello saldırıya kaynak (Bu durumda *VM1*) hello olay için düzeltme adımları hello ve hello alt bölmede bu olayın dahil edilen hello uyarıların vardır. Her uyarı hakkında daha fazla bilgi tooobtain istiyorsanız, onu ve başka bir dikey pencere yalnızca'ı tıklatın, aşağıda gösterildiği gibi açılır:

    ![Güvenlik olayı](./media/security-center-incident/security-center-incident-fig4.png)

Bu dikey penceresinde Hello bilgi according toohello uyarı değişir. Okuma [yönetme ve yanıt toosecurity Azure Güvenlik Merkezi'nde uyarıları](security-center-managing-and-responding-alerts.md) hakkında daha fazla bilgi için toomanage Bu uyarılar. Bu özellik ile ilgili bazı önemli noktalar:

* Yeni bir filtre görünüm tooIncident uyarıları yalnızca, yalnızca toocustomize ya da her ikisini de sağlar.
* Merhaba aynı uyarının bir olay (varsa) yanı sıra toobe tek başına uyarı olarak görünür bir parçası olarak bulunabilir.

## <a name="see-also"></a>Ayrıca bkz.
Bu belgede, Güvenlik Merkezi'nde güvenlik olay özelliği toouse hello nasıl öğrendiniz. Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Yönetme ve Azure Güvenlik Merkezi'nde toosecurity uyarılarını yanıt](security-center-managing-and-responding-alerts.md)
* [Azure Güvenlik Merkezi Algılama Özellikleri](security-center-detection-capabilities.md)
* [Azure Güvenlik Merkezi Planlama ve İşlemler Kılavuzu](security-center-planning-and-operations-guide.md)
* [Yönetme ve Azure Güvenlik Merkezi'nde toosecurity uyarılarını yanıt](security-center-managing-and-responding-alerts.md)
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md)--hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure Güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) - Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz
