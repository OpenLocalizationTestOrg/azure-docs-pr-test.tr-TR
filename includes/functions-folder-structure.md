
<span data-ttu-id="23ce5-101">bir ana bilgisayar yapılandırma dosyası ve her biri aşağıdaki örneğine hello olduğu gibi ayrı bir işleve hello kodunu içeren bir veya daha fazla klasörleri içeren bir kök klasöründeki tüm verilen işlev uygulaması hello işlevlerin Hello kodunu yaşadığı:</span><span class="sxs-lookup"><span data-stu-id="23ce5-101">hello code for all of hello functions in a given function app lives in a root folder that contains a host configuration file and one or more subfolders, each of which contain hello code for a separate function, as in hello following example:</span></span>

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

<span data-ttu-id="23ce5-102">Merhaba *host.json* dosyası bazı çalışma zamanı özel yapılandırma içeriyor ve hello kök klasöründe hello işlev uygulaması bulunur.</span><span class="sxs-lookup"><span data-stu-id="23ce5-102">hello *host.json* file contains some runtime-specific configuration and sits in hello root folder of hello function app.</span></span> <span data-ttu-id="23ce5-103">Kullanılabilir ayarlar hakkında daha fazla bilgi için bkz: [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) hello WebJobs.Script depo Wiki'deki.</span><span class="sxs-lookup"><span data-stu-id="23ce5-103">For information on settings that are available, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) in hello WebJobs.Script repository wiki.</span></span>

<span data-ttu-id="23ce5-104">Her işlevi bir veya daha fazla kod dosyaları, hello function.json yapılandırma ve başka bir bağımlılık içeren bir klasörü vardır.</span><span class="sxs-lookup"><span data-stu-id="23ce5-104">Each function has a folder that contains one or more code files, hello function.json configuration and other dependencies.</span></span>

