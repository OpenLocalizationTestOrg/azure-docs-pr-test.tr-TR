---
title: "Azure DevTest Labs VM'de aaaDiagnose yapı hataları | Microsoft Docs"
description: "Bilgi nasıl DevTest Labs de tootroubleshoot yapı hataları"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 115e0086-3293-4adf-8738-9f639f31f918
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: tarcher
ms.openlocfilehash: 40b3cea72cf071cc5d9a6d002d309d923c3d3084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-artifact-failures-in-hello-lab"></a>Merhaba laboratuarda yapı hataları tanılama 
Bir yapı oluşturduktan sonra başarılı veya başarısız olmadığını toosee kontrol edebilirsiniz. DevTest Labs yapı günlükleri toodiagnose bir yapı hatası kullanabileceğiniz bilgiler sağlar. Bir Windows VM hello yapı günlük bilgilerini görüntüleyebilirsiniz birkaç farklı yolu vardır.

> [!NOTE]
> hataları doğru şekilde tanımlanır ve açıklanan, hello yapı düzgün yapılandırılmış önemlidir, tooensure. Nasıl bir yapı oluşturmak toocorrectly hakkında daha fazla bilgi için bkz: [özel yapılar oluşturma](devtest-lab-artifact-author.md). Ve toosee örnek olarak düzgün yapılandırılmış bir yapı, bu denetleyin [Test parametre türleri](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) yapı.

## <a name="troubleshoot-artifact-failures-using-hello-azure-portal"></a>Hello Azure portal kullanarak yapı hatalarını giderme
toouse hello Azure portal toodiagnose hataları, yapı oluşturma sırasında şu adımları izleyin:

1. Laboratuvarınızı kaynaklar Hello listesinden seçin.

2. Merhaba tooinvestigate istediğiniz hello yapı içeren bir Windows VM seçin.

3. Altında hello sol panelinde **genel**, seçin **yapıları**. Bu VM ile ilişkili yapıları listesi görüntülenir, belirten hello yapı ve durumunu hello adı.

   ![Yapı git deposuna örnek](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifacts-failure.png)

4. Bir durumunu gösteren bir yapı seçin **başarısız**. Merhaba yapı açılır ve hello yapısı hello hata ayrıntılarını içeren bir uzantı iletisi gösterir.

   ![Yapı git deposuna örnek](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error.png)


## <a name="troubleshoot-artifact-failures-from-within-hello-vm"></a>Merhaba VM yapıt hatalarını giderme
tooview hello yapı günlükleri hello sanal makine içinde şu adımları izleyin:

1. Toohello toodiagnose istediğiniz hello yapı içeren VM oturum açın.

2. Burada "1.9 hello CSE sürüm numarasıdır. tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status gidin

   ![Yapı git deposuna örnek](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error-vm-status.png)

3. Açık hello **durum** dosya yardımcı o VM için yapı hataları tanılamak tooview bilgileri.




[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>İlgili blog gönderileri
* [VM tooexisting AD Azure DevTest Labs'de resource manager şablonu kullanarak etki alanına katılma](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[Git deposu tooa Laboratuvar ekleme](devtest-lab-add-artifact-repo.md).

