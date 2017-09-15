### <a name="create-a-nodejs-application"></a><span data-ttu-id="d877e-101">Node.js uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="d877e-101">Create a Node.js application</span></span>

<span data-ttu-id="d877e-102">`listener.js` adlı yeni bir JavaScript dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d877e-102">Create a new JavaScript file called `listener.js`.</span></span>

### <a name="add-the-relay-npm-package"></a><span data-ttu-id="d877e-103">Geçiş NPM paketini ekleme</span><span class="sxs-lookup"><span data-stu-id="d877e-103">Add the Relay NPM package</span></span>

<span data-ttu-id="d877e-104">Proje klasörünüzdeki bir Düğüm komut isteminden `npm install hyco-ws` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d877e-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-to-receive-messages"></a><span data-ttu-id="d877e-105">İleti almak için bazı kodlar yazma</span><span class="sxs-lookup"><span data-stu-id="d877e-105">Write some code to receive messages</span></span>

1. <span data-ttu-id="d877e-106">Aşağıdaki sabiti `listener.js` dosyasının başına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d877e-106">Add the following constant to the top of the `listener.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. <span data-ttu-id="d877e-107">Karma bağlantı ayrıntıları için şu sabitleri `listener.js` dosyasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d877e-107">Add the following constants to the `listener.js` file for the hybrid connection details.</span></span> <span data-ttu-id="d877e-108">Köşeli ayraçlar içindeki yer tutucuları, karma bağlantıyı oluştururken aldığınız değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d877e-108">Replace the placeholders in brackets with the values you obtained when you created the hybrid connection.</span></span>
   
   1. <span data-ttu-id="d877e-109">`const ns` - Geçiş ad alanı.</span><span class="sxs-lookup"><span data-stu-id="d877e-109">`const ns` - The Relay namespace.</span></span> <span data-ttu-id="d877e-110">Tam ad alanı adını kullandığınızdan emin olun: örneğin, `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="d877e-110">Be sure to use the fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="d877e-111">`const path` - Karma bağlantının adı.</span><span class="sxs-lookup"><span data-stu-id="d877e-111">`const path` - The name of the hybrid connection.</span></span>
   3. <span data-ttu-id="d877e-112">`const keyrule` - SAS anahtarının adı.</span><span class="sxs-lookup"><span data-stu-id="d877e-112">`const keyrule` - The name of the SAS key.</span></span>
   4. <span data-ttu-id="d877e-113">`const key` - SAS anahtarının değeri.</span><span class="sxs-lookup"><span data-stu-id="d877e-113">`const key` - The SAS key value.</span></span>

3. <span data-ttu-id="d877e-114">`listener.js` dosyasına aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d877e-114">Add the following code to the `listener.js` file:</span></span>
   
    ```js
    var wss = WebSocket.createRelayedServer(
    {
        server : WebSocket.createRelayListenUri(ns, path),
        token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(event.data);
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```
    <span data-ttu-id="d877e-115">Listener.js dosyanız şu şekilde görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="d877e-115">Here is what your listener.js file should look like:</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    var wss = WebSocket.createRelayedServer(
        {
            server : WebSocket.createRelayListenUri(ns, path),
            token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
        }, 
        function (ws) {
            console.log('connection accepted');
            ws.onmessage = function (event) {
                console.log(event.data);
            };
            ws.on('close', function () {
                console.log('connection closed');
            });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```

