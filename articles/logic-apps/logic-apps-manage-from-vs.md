---
title: Visual Studio - Azure Logic Apps aaaManage logic apps | Microsoft Docs
description: "Mantıksal uygulamalar ve diğer Azure varlıkları Visual Studio bulut Gezgini ile yönetme"
author: klam
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 12/19/2016
ms.author: LADocs; klam
ms.openlocfilehash: 419f83eb062b56e4ac2642dea4de1a025f747521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a>Mantıksal uygulamalarınızı Visual Studio bulut Gezgini ile yönetme

Merhaba rağmen [Azure portal](https://portal.azure.com/) toodesign sizin için harika bir yol sunar ve Azure mantıksal uygulamaları yönetmek için Visual Studio Cloud Explorer mantıksal uygulamalar dahil olmak üzere birçok Azure varlıklar yönetmek için kullanabilirsiniz. Visual Studio bulut Gezgini, Gözat, yönetme, düzenleme sağlar ve logic apps indirme yayımlanır. Yönetim görevleri etkinleştir, devre dışı bırakma ve geçmişini görüntüleme çalıştırmak içerir. 

Erişebilir ve logic apps Visual Studio içinde yönetebilirsiniz önce yükleyin ve bu Visual Studio Araçları Azure Logic Apps için yapılandırın. 

## <a name="prerequisites"></a>Ön koşullar

* [Visual Studio 2015 veya Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* [En son Azure SDK'sı](https://azure.microsoft.com/downloads/) (2.9.1 veya üzeri)
* [Visual Studio bulut Gezgini](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* Merhaba katıştırılmış Tasarımcısı kullanırken erişim toohello web

## <a name="install-visual-studio-tools-for-logic-apps"></a>Mantıksal uygulamalar için Visual Studio araçlarını yükleme

Merhaba önkoşulları yüklendikten sonra karşıdan yükleyip hello Azure Logic Apps araçları Visual Studio için.

1. Visual Studio'yu açın. Merhaba üzerinde **Araçları** menüsünde, select **Uzantılar ve güncelleştirmeler**.
2. Merhaba genişletin **çevrimiçi** hello Visual Studio Galerisi çevrimiçi arama yapabilmeniz için kategori.
3. Göz atın veya arayın **Logic Apps** bulana kadar **Visual Studio için Azure Logic Apps Araçları**.
4. toodownload ve yükleme hello uzantısı,'ı **karşıdan**.
5. Yüklendikten sonra Visual Studio'yu yeniden başlatın.

> [!NOTE]
> toodownload hello Azure Logic Apps araçları Visual Studio için doğrudan toohello Git [Visual Studio Market'te](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).

## <a name="browse-for-logic-apps-in-cloud-explorer"></a>Logic apps Cloud Explorer'da gözatın.

1.  tooopen Cloud Explorer hello üzerinde **Görünüm** menüsünde seçin **Cloud Explorer**.
2.  Mantıksal uygulamanız için kaynak grubu veya kaynak türüne göre göz atın. 

    * Kaynak türüne göre göz atarsanız, Azure aboneliğinizi seçin, hello genişletin **Logic Apps** bölümünde ve mantıksal uygulamanızı seçin. 
    * Kaynak grubu tarafından göz atarsanız, mantıksal uygulamanızı sahip hello kaynak grubunu genişletin ve mantıksal uygulamanızı seçin.

    tooview komutları mantığı uygulamanız için mantıksal uygulamanızı sağ tıklayın ya da bulut Explorer hello altındaki hello seçin **Eylemler** menüsü.

    ![Mantıksal uygulamanızı gözatın.](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a>Mantıksal uygulamanızı Logic Apps Tasarımcısı ile Düzenle

Bulut Gezgini'nden hello şu anda dağıtılmış mantıksal uygulama açabilirsiniz hello Azure portalında kullandığınız aynı Tasarımcısı. 

* tooedit bulut Gezgini'nde mantıksal uygulamanızı mantıksal uygulamanızı sağ tıklatın ve seçin **mantığı uygulama Düzenleyicisi ile açık**. 

* toopublish, güncelleştirmelerinin toohello bulut, seçin **Yayımla**. 

* Yeni bir çalışma toostart seçin **tetikleyici çalıştırmak**.

![Logic Apps Tasarımcısı](./media/logic-apps-manage-from-vs/designer.png)

Merhaba Tasarımcısı'ndan şunları da yapabilirsiniz **karşıdan** bir mantıksal uygulama. Bu eylem otomatik olarak hello mantıksal uygulama tanımını parameterizes ve hello tanımı bir Azure Resource Manager dağıtım şablonu olarak kaydeder. Bu dağıtım şablonu tooyour Azure kaynak grubu projesi ekleyebilirsiniz.

## <a name="browse-your-logic-app-run-history"></a>Mantıksal uygulamanızı çalıştırma geçmişi göz atın

çalıştırma geçmişi mantığı uygulamanız için tooview hello mantıksal uygulamanızı sağ tıklatın ve seçin **açık çalıştırma geçmişi**. tooreorder çalıştırma geçmişi hello özellikleri gösterilen, select hello sütun başlığını hiçbirinde temel.

![çalıştırma geçmişi](media/logic-apps-manage-from-vs/runs.png)

hello çalıştırmak hello girişleri ve çıkışları her adımdan dahil olmak üzere sonuçları gözden geçirebilmeniz için çalıştırma geçmişi bir örneğinin tooshow hello örneklerinde Çalıştır hello birini çift tıklatın.

![Geçmiş sonuçlarını, giriş ve çıkış adımları çalıştırın](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a>Sonraki adımlar

* [İlk mantıksal uygulamanızı oluşturma](logic-apps-create-a-logic-app.md)
* [Tasarım, derleme ve logic apps Visual Studio içinde dağıtma](logic-apps-deploy-from-vs.md)
* [Sık rastlanan örnekleri ve senaryoları inceleyin](logic-apps-examples-and-scenarios.md)
* [Video: Azure Logic Apps ile iş süreçlerini otomatikleştirmek](http://channel9.msdn.com/Events/Build/2016/T694)
* [Video: sistemlerinizi Azure Logic Apps ile tümleştirme](http://channel9.msdn.com/Events/Build/2016/P462)
