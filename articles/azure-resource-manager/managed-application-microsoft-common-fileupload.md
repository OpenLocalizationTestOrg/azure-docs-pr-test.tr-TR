---
title: "Azure yönetilen uygulama dosya yükleme UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Microsoft.Common.FileUpload kullanıcı Arabirimi öğesi açıklar"
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
ms.openlocfilehash: 217e9e63eb7cd198f70cee42b418867df9f1f993
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a><span data-ttu-id="50e8c-103">Microsoft.Common.FileUpload UI öğesi</span><span class="sxs-lookup"><span data-stu-id="50e8c-103">Microsoft.Common.FileUpload UI element</span></span>
<span data-ttu-id="50e8c-104">Karşıya yüklemek için bir veya daha fazla belirtmesine imkan tanıyan bir denetimi.</span><span class="sxs-lookup"><span data-stu-id="50e8c-104">A control that allows a user to specify one or more files to upload.</span></span> <span data-ttu-id="50e8c-105">Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="50e8c-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="50e8c-106">Kullanıcı Arabirimi örneği</span><span class="sxs-lookup"><span data-stu-id="50e8c-106">UI sample</span></span>
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a><span data-ttu-id="50e8c-108">Şema</span><span class="sxs-lookup"><span data-stu-id="50e8c-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="50e8c-109">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="50e8c-109">Remarks</span></span>
- <span data-ttu-id="50e8c-110">`constraints.accept`Tarayıcının dosyası iletişim kutusunda gösterilen dosya türlerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="50e8c-110">`constraints.accept` specifies the types of files that are shown in the browser's file dialog.</span></span> <span data-ttu-id="50e8c-111">Bkz: [HTML5 belirtimi](http://www.w3.org/TR/html5/forms.html#attr-input-accept) için izin verilen değerler.</span><span class="sxs-lookup"><span data-stu-id="50e8c-111">See the [HTML5 specification](http://www.w3.org/TR/html5/forms.html#attr-input-accept) for allowed values.</span></span> <span data-ttu-id="50e8c-112">Varsayılan değer **null**.</span><span class="sxs-lookup"><span data-stu-id="50e8c-112">The default value is **null**.</span></span>
- <span data-ttu-id="50e8c-113">Varsa `options.multiple` ayarlanır **doğru**, kullanıcının tarayıcısının dosyası iletişim kutusunda birden fazla dosya seçmesine izin verilen.</span><span class="sxs-lookup"><span data-stu-id="50e8c-113">If `options.multiple` is set to **true**, the user is allowed to select more than one file in the browser's file dialog.</span></span> <span data-ttu-id="50e8c-114">Varsayılan değer **false**.</span><span class="sxs-lookup"><span data-stu-id="50e8c-114">The default value is **false**.</span></span>
- <span data-ttu-id="50e8c-115">Bu öğe değerine göre iki modda karşıya yükleme dosyalarını destekler `options.uploadMode`.</span><span class="sxs-lookup"><span data-stu-id="50e8c-115">This element supports uploading files in two modes based on the value of `options.uploadMode`.</span></span> <span data-ttu-id="50e8c-116">Varsa **dosya** belirtildi, çıktıyı bir BLOB dosyanın içeriğini içerir.</span><span class="sxs-lookup"><span data-stu-id="50e8c-116">If **file** is specified, the output contains the contents of the file as a blob.</span></span> <span data-ttu-id="50e8c-117">Varsa **url** belirtilmişse dosyanın geçici bir konuma yüklenir ve çıktı blob URL'sini içerir.</span><span class="sxs-lookup"><span data-stu-id="50e8c-117">If **url** is specified, then the file is uploaded to a temporary location, and the output contains the URL of the blob.</span></span> <span data-ttu-id="50e8c-118">Geçici BLOB'lar 24 saat sonra temizlenecek.</span><span class="sxs-lookup"><span data-stu-id="50e8c-118">Temporary blobs will be purged after 24 hours.</span></span> <span data-ttu-id="50e8c-119">Varsayılan değer **dosya**.</span><span class="sxs-lookup"><span data-stu-id="50e8c-119">The default value is **file**.</span></span>
- <span data-ttu-id="50e8c-120">Değeri `options.openMode` nasıl dosyayı okuma belirler.</span><span class="sxs-lookup"><span data-stu-id="50e8c-120">The value of `options.openMode` determines how the file is read.</span></span> <span data-ttu-id="50e8c-121">Dosya düz metin olması bekleniyor, belirtin **metin**; başka belirtin **ikili**.</span><span class="sxs-lookup"><span data-stu-id="50e8c-121">If the file is expected to be plain text, specify **text**; else, specify **binary**.</span></span> <span data-ttu-id="50e8c-122">Varsayılan değer **metin**.</span><span class="sxs-lookup"><span data-stu-id="50e8c-122">The default value is **text**.</span></span>
- <span data-ttu-id="50e8c-123">Varsa `options.uploadMode` ayarlanır **dosya** ve `options.openMode` ayarlanır **ikili**, base64 ile kodlanmış çıktı.</span><span class="sxs-lookup"><span data-stu-id="50e8c-123">If `options.uploadMode` is set to **file** and `options.openMode` is set to **binary**, the output is base64-encoded.</span></span>
- <span data-ttu-id="50e8c-124">`options.encoding`Dosya okunurken kullanılacak kodlama belirtir.</span><span class="sxs-lookup"><span data-stu-id="50e8c-124">`options.encoding` specifies the encoding to use when reading the file.</span></span> <span data-ttu-id="50e8c-125">Varsayılan değer **UTF-8**ve kullanılan yalnızca `options.openMode` ayarlanır **metin**.</span><span class="sxs-lookup"><span data-stu-id="50e8c-125">The default value is **UTF-8**, and is used only when `options.openMode` is set to **text**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="50e8c-126">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="50e8c-126">Sample output</span></span>
<span data-ttu-id="50e8c-127">Options.Multiple false ise ve options.uploadMode dosyadır, çıktı JSON dizesi olarak dosyanın içeriğini içerir:</span><span class="sxs-lookup"><span data-stu-id="50e8c-127">If options.multiple is false and options.uploadMode is file, then the output contains the contents of the file as a JSON string:</span></span>

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

<span data-ttu-id="50e8c-128">Options.Multiple true ise and'options.uploadMode dosyasıdır ve çıktı dosyaların içeriğini bir JSON dizisi olarak içerir:</span><span class="sxs-lookup"><span data-stu-id="50e8c-128">If options.multiple is true and\`options.uploadMode is file, then the output contains the contents of the files as a JSON array:</span></span>

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

<span data-ttu-id="50e8c-129">Options.Multiple false ise ve options.uploadMode URL'dir çıktıyı JSON dizesi olarak bir URL içerir:</span><span class="sxs-lookup"><span data-stu-id="50e8c-129">If options.multiple is false and options.uploadMode is url, then the output contains a URL as a JSON string:</span></span>

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

<span data-ttu-id="50e8c-130">Options.Multiple geçerlidir ve url options.uploadMode ise, çıktı bir JSON dizisi olarak URL'lerin bir listesini içerir:</span><span class="sxs-lookup"><span data-stu-id="50e8c-130">If options.multiple is true and options.uploadMode is url, then the output contains a list of URLs as a JSON array:</span></span>
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

<span data-ttu-id="50e8c-131">Bir CreateUiDefinition test edilirken (Google Chrome gibi) bazı tarayıcılar tarayıcı konsoluna Microsoft.Common.FileUpload öğe tarafından oluşturulan URL'leri keser.</span><span class="sxs-lookup"><span data-stu-id="50e8c-131">When testing a CreateUiDefinition, some browsers (like Google Chrome) truncate URLs generated by the Microsoft.Common.FileUpload element in the browser console.</span></span> <span data-ttu-id="50e8c-132">Tam URL'leri kopyalamak için tek bağlantılar sağ gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="50e8c-132">You may need to right-click individual links to copy the full URLs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="50e8c-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="50e8c-133">Next steps</span></span>
* <span data-ttu-id="50e8c-134">Yönetilen uygulamaların giriş için bkz: [Azure yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="50e8c-134">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="50e8c-135">UI tanımları oluşturmak için bir giriş için bkz [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="50e8c-135">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="50e8c-136">Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="50e8c-136">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
