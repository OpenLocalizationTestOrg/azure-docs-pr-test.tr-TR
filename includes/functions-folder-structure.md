
<span data-ttu-id="95251-101">Bir ana bilgisayar yapılandırma dosyası içeren bir kök klasörü ve her biri aşağıdaki örnekteki gibi ayrı bir işleve kodunu içeren bir veya daha fazla alt tüm işlevleri verilen işlevi uygulama kodunu yaşadığı:</span><span class="sxs-lookup"><span data-stu-id="95251-101">The code for all of the functions in a given function app lives in a root folder that contains a host configuration file and one or more subfolders, each of which contain the code for a separate function, as in the following example:</span></span>

```
wwwroot
 | - host.json
 | - mynodefunction
 | | - function.json
 | | - index.js
 | | - node_modules
 | | | - ... packages ...
 | | - package.json
 | - mycsharpfunction
 | | - function.json
 | | - run.csx
```

<span data-ttu-id="95251-102">*Host.json* dosyası bazı çalışma zamanı özel yapılandırma içeriyor ve işlev uygulaması kök klasöründe bulunur.</span><span class="sxs-lookup"><span data-stu-id="95251-102">The *host.json* file contains some runtime-specific configuration and sits in the root folder of the function app.</span></span> <span data-ttu-id="95251-103">Kullanılabilir ayarlar hakkında daha fazla bilgi için bkz: [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) WebJobs.Script depo Wiki'deki.</span><span class="sxs-lookup"><span data-stu-id="95251-103">For information on settings that are available, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) in the WebJobs.Script repository wiki.</span></span>

<span data-ttu-id="95251-104">Her işlevi bir veya daha fazla kod dosyaları, function.json yapılandırma ve başka bir bağımlılık içeren bir klasörü vardır.</span><span class="sxs-lookup"><span data-stu-id="95251-104">Each function has a folder that contains one or more code files, the function.json configuration and other dependencies.</span></span>

