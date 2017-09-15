## <a name="create-a-ruby-application"></a><span data-ttu-id="12b4c-101">Ruby uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="12b4c-101">Create a Ruby application</span></span>
<span data-ttu-id="12b4c-102">Yönergeler için bkz: [Azure üzerinde bir Ruby uygulaması oluşturmak](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="12b4c-102">For instructions, see [Create a Ruby Application on Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="12b4c-103">Uygulamanızı kullanım hizmet veri yolu için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="12b4c-103">Configure Your application to Use Service Bus</span></span>
<span data-ttu-id="12b4c-104">Service Bus hizmetini kullanmak için karşıdan yükle ve storage REST Hizmetleri ile iletişim kuran bir dizi kolaylık içeren Azure Ruby paketini kullanın.</span><span class="sxs-lookup"><span data-stu-id="12b4c-104">To use Service Bus, download and use the Azure Ruby package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="12b4c-105">Paket elde etmek için RubyGems kullanın</span><span class="sxs-lookup"><span data-stu-id="12b4c-105">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="12b4c-106">Bir komut satırı arabirimi gibi kullandığınız **PowerShell** (Windows), **Terminal** (Mac) veya **Bash** (UNIX).</span><span class="sxs-lookup"><span data-stu-id="12b4c-106">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="12b4c-107">Gem ve bağımlılıklarını yüklemek için komut penceresinde "gem yükleme azure" yazın.</span><span class="sxs-lookup"><span data-stu-id="12b4c-107">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="12b4c-108">Paket alma</span><span class="sxs-lookup"><span data-stu-id="12b4c-108">Import the package</span></span>
<span data-ttu-id="12b4c-109">Sık kullandığınız metin Düzenleyicisi'ni kullanarak aşağıdaki depolama kullanmayı düşündüğünüz Söyleniş dosyasının üstüne ekleyin:</span><span class="sxs-lookup"><span data-stu-id="12b4c-109">Using your favorite text editor, add the following to the top of the Ruby file in which you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="12b4c-110">Hizmet veri yolu bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="12b4c-110">Set up a Service Bus connection</span></span>
<span data-ttu-id="12b4c-111">Ad alanı değerleri, anahtar, anahtar, imzalayan ve ana bilgisayar adını ayarlamak için aşağıdaki kodu kullanın:</span><span class="sxs-lookup"><span data-stu-id="12b4c-111">Use the following code to set the values of namespace, name of the key, key, signer and host:</span></span>

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

<span data-ttu-id="12b4c-112">Ad alanı değeri URL'nin tamamı yerine oluşturulan değere ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="12b4c-112">Set the namespace value to the value you created rather than the entire URL.</span></span> <span data-ttu-id="12b4c-113">Örneğin, **"yourexamplenamespace"**, değil "yourexamplenamespace.servicebus.windows.net".</span><span class="sxs-lookup"><span data-stu-id="12b4c-113">For example, use **"yourexamplenamespace"**, not "yourexamplenamespace.servicebus.windows.net".</span></span>
