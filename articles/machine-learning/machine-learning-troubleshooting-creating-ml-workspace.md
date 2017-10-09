---
title: "Sorunlarını giderme: Oluşturun ve tooa Machine Learning çalışma alanı bağlantı | Microsoft Docs"
description: "Oluşturma ve tooan Azure Machine Learning çalışma alanına bağlanma ortak sorunlar için çözümleri"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 1a8aec4b-35f9-44e8-9570-2575b8979ab1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 965a0025e85ba4e22c2b037edfa923e7f7599069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-create-and-connect-tooan-machine-learning-workspace"></a>Sorun giderme kılavuzu: oluşturmak ve tooan Machine Learning çalışma alanına bağlayın
Bu kılavuz, Azure Machine Learning çalışma alanlarınızı ayarlarken çözümleri için bazı sık zorluklar karşılaşılan sağlar.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a>Çalışma alanı sahibi
Machine Learning Studio'da bir çalışma alanı tooopen olmalıdır toohello Microsoft Account imzalı toocreate hello çalışma kullanılan veya tooreceive hello sahibi toojoin hello çalışma alanından bir davet gerekir. Azure portal Hello hello özelliği tooconfigure erişim içerir hello çalışma yönetebilirsiniz.

Bir çalışma alanı yönetme ile ilgili daha fazla bilgi için bkz: [bir Azure Machine Learning çalışma alanını yönetme].

[bir Azure Machine Learning çalışma alanını yönetme]: machine-learning-manage-workspace.md

## <a name="allowed-regions"></a>İzin verilen bölgeleri
Machine Learning bölgeler sınırlı bir süre içinde şu anda kullanılamıyor. Aboneliğiniz bu bölgelerinden içermiyorsa hello hata iletisi görebilirsiniz, "Hello bölgeler izin hiç aboneliğiniz yok."

bir bölge olması toorequest eklenen tooyour abonelik, Azure portal hello yeni bir Microsoft destek isteği oluşturmak, seçin **faturalama** hello sorun türü ve izleme hello isteğiniz toosubmit ister.

## <a name="storage-account"></a>Depolama hesabı
Merhaba Machine Learning hizmetindeki bir depolama hesabı toostore verileri gerekir. Mevcut bir depolama hesabını kullanabilir veya (yeni bir depolama hesabı'de kota toocreate varsa) hello yeni Machine Learning çalışma alanı oluşturduğunuzda, yeni bir depolama hesabı oluşturabilirsiniz.

Merhaba yeni Machine Learning çalışma alanı oluşturulduktan sonra toocreate hello çalışma kullanılan hello Microsoft hesabı kullanarak tooMachine Learning Studio imzalayabilirsiniz. Lütfen hello hata iletisi, "Çalışma alanı bulunamadı" (benzer toohello ekran aşağıdaki) karşılaşırsanız, aşağıdaki adımları toodelete hello tarayıcı tanımlama bilgilerinizi kullanın.

![Çalışma alanı bulunamadı][screen3]

**toodelete tarayıcı tanımlama**

1. Internet Explorer kullanıyorsanız, hello tıklatın **Araçları** hello sağ üst köşesinde düğmesine tıklayın ve ardından **Internet Seçenekleri**.  

![Internet Seçenekleri][screen4]

2. Merhaba altında **genel** sekmesini tıklatın, **silin...**

![Genel sekmesi][screen5]

3. Merhaba, **Gözatma Geçmişini Sil** iletişim kutusunda, emin olun **tanımlama bilgileri ve Web sitesi verileri** seçilir ve tıklatın **silmek**.

![Tanımlama bilgilerini silin][screen6]

Hello tanımlama bilgilerini silindikten sonra hello tarayıcı yeniden başlatın ve sonra toohello gidin [Microsoft Azure Machine Learning](https://studio.azureml.net) sayfası. Bir kullanıcı adı ve parolanızı girmeniz için sizden istendiğinde toocreate hello çalışma kullandığınız aynı Microsoft hesabı hello.

## <a name="comments"></a>Yorumlar

Amacımız toomake hello Machine Learning deneyiminizi olarak sorunsuz ' dir. Lütfen tüm yorumlar ve sorunları hello sonrası [Azure Machine Learning Forumu](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) bize hizmet, daha iyi toohelp.

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
