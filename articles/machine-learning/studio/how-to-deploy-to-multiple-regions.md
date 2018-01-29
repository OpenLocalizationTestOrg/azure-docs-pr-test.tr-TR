---
title: "Bir Web hizmeti için birden çok bölgeye dağıtma | Microsoft Docs"
description: "(Kopya) yeni bir Web hizmeti diğer bölgeler dağıtmak için adımları."
services: machine-learning
documentationcenter: 
author: garyericson
manager: raymondl
editor: cgronlun
ms.assetid: 36c60411-f2db-4ee2-9b66-b1f1d77a8f44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: abd6f05e9b9ce711ce55e88f07aa13287c76ebc2
ms.sourcegitcommit: 42ee5ea09d9684ed7a71e7974ceb141d525361c9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/09/2017
---
# <a name="how-to-deploy-a-web-service-to-multiple-regions"></a>Web Hizmetini birden fazla bölgeye dağıtma
Yeni Azure Web Hizmetleri kolayca birden fazla abonelikleri veya çalışma alanları gerek kalmadan bir web hizmeti için birden çok bölgeye dağıtmanıza izin verin. 

Fiyatlandırma belirli, bu nedenle, web hizmeti dağıtacağınız her bölge için bir faturalandırma planı tanımlamalısınız bölgedir.

## <a name="to-create-a-plan-in-another-region"></a>Başka bir bölgede bir plan oluşturmak için
1. Oturum [Microsoft Azure Machine Learning Web Hizmetleri](https://services.azureml.net/).
2. Tıklatın **planları** menü seçeneği.
3. Görünüm sayfası üzerinden planlarında tıklatın **yeni**.
4. Gelen **abonelik** açılan listesinde, yeni plan bulunacağı aboneliği seçin.
5. Gelen **bölge** açılan listesinde, yeni plan için bölge seçin. Seçilen bölge için planlama seçenekleri görüntüleyecek **planlama seçenekleri** sayfasının bölümünde.
6. Gelen **kaynak grubu** bir kaynak grubu plan için açılan listesinde, seçin. Kaynak grupları hakkında daha fazla bilgi [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md).
7. İçinde **Plan adı** planın adını yazın.
8. Altında **planı seçenekleri**, yeni plan için fatura düzeyi'ı tıklatın.
9. **Oluştur**'a tıklayın.

## <a name="deploying-the-web-service-to-another-region"></a>Web hizmeti başka bir bölgeye dağıtmayı
1. Tıklatın **Web Hizmetleri** menü seçeneği.
2. Yeni bir bölgeye dağıtmayı Web hizmeti seçin.
3. Tıklatın **kopya**.
4. İçinde **Web hizmeti adı**, web hizmeti için yeni bir ad yazın.
5. İçinde **Web hizmeti açıklaması**, web hizmeti için bir açıklama yazın.
6. Gelen **abonelik** açılan listesinde, yeni web hizmeti bulunacağı aboneliği seçin.
7. Gelen **kaynak grubu** bir kaynak grubu için web hizmeti açılan listesinde, seçin. Kaynak grupları hakkında daha fazla bilgi [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md).
8. Gelen **bölge** açılan listesinde, web hizmeti dağıtmak üzere bölgeyi seçin.
9. Gelen **depolama hesabı** açılan listesinde, bir depolama birimi seçin, web hizmeti depolamak hesap.
10. Gelen **fiyat planı** açılan listesinde, 8. adımda seçtiğiniz bölgede planı seçin.
11. Tıklatın **kopya**.

