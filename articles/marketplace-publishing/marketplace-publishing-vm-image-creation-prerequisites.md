---
title: "hello Azure Marketi için bir sanal makine görüntüsü oluşturmak için aaaTechnical önkoşulları | Microsoft Docs"
description: "Oluşturma ve başkaları için bir sanal makine görüntü toohello Azure Marketi dağıtma hello gereksinimleri anlamak toopurchase."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 63c16966-0304-4b17-a715-368a0a5ccb2c
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: fcae4d9e052581e3c1dfe7962e6d50ec31040419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="technical-prerequisites-for-creating-a-virtual-machine-image-for-hello-azure-marketplace"></a>Hello Azure Marketi için bir sanal makine görüntüsü oluşturmak için teknik önkoşulları
Merhaba işlemi başlamadan önce baştan sona okuyun ve nerede ve neden her adım gerçekleştirilir anlayın. Mümkün olduğunca, şirket bilgilerinizi ve diğer verileri hazırlama, gerekli Araçları'nı indirmek ve/veya teknik bileşenleri hello teklif oluşturma işlemi başlamadan önce oluşturun. Bu öğeler bu makaleyi gözden açık olmalıdır.  

## <a name="download-needed-tools--applications"></a>Gerekli Araçlar & uygulamaları yükle
Merhaba aşağıdaki öğelerindeki hello işlemine başlamadan önce hazır olması gerekir:

* Hangi işletim sistemine bağlı olarak, hedeflediğiniz, yükleme hello [Azure PowerShell cmdlet'lerini](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) veya [Linux komut satırı arabirimi aracı](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) hello gelen [Azure indirmeleri](https://azure.microsoft.com/downloads/) Sayfa.
* Azure Storage Gezgini Codeplex'ten yükleyin.
* Karşıdan yükleyip hello sertifika Test aracı Azure sertifikalı için:
  * [http://go.microsoft.com/fwlink/?LinkId=526913](http://go.microsoft.com/fwlink/?LinkID=526913). Bir Windows tabanlı bilgisayar toorun hello sertifika Aracı gerekir. Windows tabanlı bir bilgisayarda kullanılabilir yoksa, Windows tabanlı bir VM azure'da hello aracını çalıştırabilirsiniz.

## <a name="platforms-supported"></a>Desteklenen platformlar
Windows veya Linux Azure tabanlı VM'ler geliştirebilirsiniz. Bir Azure ile uyumlu sanal sabit disk (VHD)--farklı araçlarını kullanın ve hangi işletim sistemine bağlı olarak, kullandığınız adımları oluşturma gibi işlem--yayımlama hello bazı öğeleri:  

* Linux kullanıyorsanız, hello toohello "(Linux tabanlı) bir Azure uyumlu VHD oluşturma" bölümüne bakın [sanal makine görüntüsü yayımlama Kılavuzu](marketplace-publishing-vm-image-creation.md).
* Windows kullanıyorsanız, hello toohello "(Windows tabanlı) bir Azure uyumlu VHD oluşturma" bölümüne bakın [sanal makine görüntüsü yayımlama Kılavuzu](marketplace-publishing-vm-image-creation.md).

> [!NOTE]
> Windows tabanlı tooa makineye erişim:
> 
> * Merhaba sertifika doğrulama aracını çalıştırın.
> * Hello VHD paylaşılan erişim imzası hello VHD sertifika gönderme URL'sini oluşturun.
> 
> 

## <a name="develop-your-vhd"></a>VHD geliştirin
Merhaba Bulut veya şirket içinde Azure VHD'leri geliştirme yapabilirsiniz:

* Bulut tabanlı geliştirme tüm geliştirme adımları uzaktan Azure'da yerleşik bir VHD üzerinde gerçekleştirilen anlamına gelir.
* Şirket içi geliştirme VHD indiriliyor ve şirket içi altyapıyı kullanarak geliştirme gerektirir. Bu mümkün olsa da, bunu önermiyoruz. Windows veya SQL için geliştirme şirket içi, toohave hello içi ilgili lisans anahtarları gerektirir. Dahil etmek veya VM oluşturduktan sonra SQL Server yükleyin. Ayrıca, onaylanan SQL görüntüden hello Azure portalı üzerinde teklifiniz temel almanız gerekir. Toodevelop şirket içi karar verirseniz, bazı adımlar hello bulutta geliştirme, farklı bir biçimde gerçekleştirmeniz gerekir. İlgili bilgiler bulabilirsiniz [şirket içi VM görüntü oluşturma](marketplace-publishing-vm-image-creation-on-premise.md).

[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
