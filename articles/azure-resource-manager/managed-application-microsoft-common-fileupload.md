---
title: "aaaAzure yönetilen uygulama dosya yükleme UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Hello Microsoft.Common.FileUpload UI öğesi açıklar"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 7af5bec992e3f120afb1bdf56d8b4c19a8e5e834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a><span data-ttu-id="8a783-103">Microsoft.Common.FileUpload UI öğesi</span><span class="sxs-lookup"><span data-stu-id="8a783-103">Microsoft.Common.FileUpload UI element</span></span>
<span data-ttu-id="8a783-104">Bir veya daha fazla kullanıcı toospecify sağlayan bir denetimi tooupload dosyaları.</span><span class="sxs-lookup"><span data-stu-id="8a783-104">A control that allows a user toospecify one or more files tooupload.</span></span> <span data-ttu-id="8a783-105">Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="8a783-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="8a783-106">Kullanıcı Arabirimi örneği</span><span class="sxs-lookup"><span data-stu-id="8a783-106">UI sample</span></span>
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a><span data-ttu-id="8a783-108">Şema</span><span class="sxs-lookup"><span data-stu-id="8a783-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.FileUpload",
  "label": "Some file upload",
  "toolTip": "",
  "constraints": {
    "required": true,
    "accept": ".doc,.docx,.xml,application/msword"
  },
  "options": {
    "multiple": false,
    "uploadMode": "file",
    "openMode": "text",
    "encoding": "UTF-8"
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="8a783-109">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="8a783-109">Remarks</span></span>
- <span data-ttu-id="8a783-110">`constraints.accept`Merhaba hello tarayıcının dosyası iletişim kutusunda gösterilen dosya türlerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="8a783-110">`constraints.accept` specifies hello types of files that are shown in hello browser's file dialog.</span></span> <span data-ttu-id="8a783-111">Merhaba bkz [HTML5 belirtimi](http://www.w3.org/TR/html5/forms.html#attr-input-accept) için izin verilen değerler.</span><span class="sxs-lookup"><span data-stu-id="8a783-111">See hello [HTML5 specification](http://www.w3.org/TR/html5/forms.html#attr-input-accept) for allowed values.</span></span> <span data-ttu-id="8a783-112">Merhaba varsayılan değer **null**.</span><span class="sxs-lookup"><span data-stu-id="8a783-112">hello default value is **null**.</span></span>
- <span data-ttu-id="8a783-113">Varsa `options.multiple` çok ayarlanır**doğru**, hello tarayıcının dosya iletişim kutusu bir dosyada birden çok tooselect hello kullanıcı izin verilir.</span><span class="sxs-lookup"><span data-stu-id="8a783-113">If `options.multiple` is set too**true**, hello user is allowed tooselect more than one file in hello browser's file dialog.</span></span> <span data-ttu-id="8a783-114">Merhaba varsayılan değer **false**.</span><span class="sxs-lookup"><span data-stu-id="8a783-114">hello default value is **false**.</span></span>
- <span data-ttu-id="8a783-115">Bu öğe hello değerine göre iki modda karşıya yükleme dosyalarını destekler `options.uploadMode`.</span><span class="sxs-lookup"><span data-stu-id="8a783-115">This element supports uploading files in two modes based on hello value of `options.uploadMode`.</span></span> <span data-ttu-id="8a783-116">Varsa **dosya** belirtilirse, hello çıktı hello bir BLOB hello dosyanın içeriğini içerir.</span><span class="sxs-lookup"><span data-stu-id="8a783-116">If **file** is specified, hello output contains hello contents of hello file as a blob.</span></span> <span data-ttu-id="8a783-117">Varsa **url** belirtilmişse hello dosyasıdır karşıya yüklenen tooa geçici konuma ve hello çıktı hello blob hello URL'sini içerir.</span><span class="sxs-lookup"><span data-stu-id="8a783-117">If **url** is specified, then hello file is uploaded tooa temporary location, and hello output contains hello URL of hello blob.</span></span> <span data-ttu-id="8a783-118">Geçici BLOB'lar 24 saat sonra temizlenecek.</span><span class="sxs-lookup"><span data-stu-id="8a783-118">Temporary blobs will be purged after 24 hours.</span></span> <span data-ttu-id="8a783-119">Merhaba varsayılan değer **dosya**.</span><span class="sxs-lookup"><span data-stu-id="8a783-119">hello default value is **file**.</span></span>
- <span data-ttu-id="8a783-120">Merhaba değerini `options.openMode` nasıl hello dosyayı okuma belirler.</span><span class="sxs-lookup"><span data-stu-id="8a783-120">hello value of `options.openMode` determines how hello file is read.</span></span> <span data-ttu-id="8a783-121">Merhaba beklenen toobe düz metin dosyasıysa belirtin **metin**; başka belirtin **ikili**.</span><span class="sxs-lookup"><span data-stu-id="8a783-121">If hello file is expected toobe plain text, specify **text**; else, specify **binary**.</span></span> <span data-ttu-id="8a783-122">Merhaba varsayılan değer **metin**.</span><span class="sxs-lookup"><span data-stu-id="8a783-122">hello default value is **text**.</span></span>
- <span data-ttu-id="8a783-123">Varsa `options.uploadMode` çok ayarlanır**dosya** ve `options.openMode` çok ayarlanır**ikili**, hello çıkış base64 ile kodlanmış.</span><span class="sxs-lookup"><span data-stu-id="8a783-123">If `options.uploadMode` is set too**file** and `options.openMode` is set too**binary**, hello output is base64-encoded.</span></span>
- <span data-ttu-id="8a783-124">`options.encoding`Merhaba kodlama toouse hello dosyası okunurken belirtir.</span><span class="sxs-lookup"><span data-stu-id="8a783-124">`options.encoding` specifies hello encoding toouse when reading hello file.</span></span> <span data-ttu-id="8a783-125">Merhaba varsayılan değer **UTF-8**ve kullanılan yalnızca `options.openMode` çok ayarlanır**metin**.</span><span class="sxs-lookup"><span data-stu-id="8a783-125">hello default value is **UTF-8**, and is used only when `options.openMode` is set too**text**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="8a783-126">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="8a783-126">Sample output</span></span>
<span data-ttu-id="8a783-127">Options.Multiple false ise ve options.uploadMode dosyadır, çıktı hello dosyasının Merhaba içeriğine JSON dizesi olarak içerir:</span><span class="sxs-lookup"><span data-stu-id="8a783-127">If options.multiple is false and options.uploadMode is file, then the output contains hello contents of hello file as a JSON string:</span></span>

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

<span data-ttu-id="8a783-128">Options.Multiple true ise and'options.uploadMode dosyasıdır ve çıktı hello dosyaları Merhaba içeriğine bir JSON dizisi olarak içerir:</span><span class="sxs-lookup"><span data-stu-id="8a783-128">If options.multiple is true and\`options.uploadMode is file, then the output contains hello contents of hello files as a JSON array:</span></span>

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

<span data-ttu-id="8a783-129">Options.Multiple false ise ve options.uploadMode URL'dir çıktıyı JSON dizesi olarak bir URL içerir:</span><span class="sxs-lookup"><span data-stu-id="8a783-129">If options.multiple is false and options.uploadMode is url, then the output contains a URL as a JSON string:</span></span>

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

<span data-ttu-id="8a783-130">Options.Multiple geçerlidir ve url options.uploadMode ise, çıktı bir JSON dizisi olarak URL'lerin bir listesini içerir:</span><span class="sxs-lookup"><span data-stu-id="8a783-130">If options.multiple is true and options.uploadMode is url, then the output contains a list of URLs as a JSON array:</span></span>
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

<span data-ttu-id="8a783-131">Bir CreateUiDefinition test edilirken (Google Chrome gibi) bazı tarayıcılar hello tarayıcı konsoluna hello Microsoft.Common.FileUpload öğe tarafından oluşturulan URL'leri keser.</span><span class="sxs-lookup"><span data-stu-id="8a783-131">When testing a CreateUiDefinition, some browsers (like Google Chrome) truncate URLs generated by hello Microsoft.Common.FileUpload element in hello browser console.</span></span> <span data-ttu-id="8a783-132">Tooright tıklatma tek bağlantılar toocopy hello tam URL'leri gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="8a783-132">You may need tooright-click individual links toocopy hello full URLs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8a783-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8a783-133">Next steps</span></span>
* <span data-ttu-id="8a783-134">Bir giriş toomanaged uygulamalar için bkz [Azure yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8a783-134">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="8a783-135">Bir giriş toocreating UI tanımları için bkz: [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8a783-135">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="8a783-136">Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="8a783-136">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
