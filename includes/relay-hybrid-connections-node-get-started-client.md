### <a name="create-a-nodejs-application"></a><span data-ttu-id="de516-101">Node.js uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="de516-101">Create a Node.js application</span></span>

<span data-ttu-id="de516-102">`sender.js` adlı yeni bir JavaScript dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="de516-102">Create a new JavaScript file called `sender.js`.</span></span>

### <a name="add-the-relay-npm-package"></a><span data-ttu-id="de516-103">Geçiş NPM paketini ekleme</span><span class="sxs-lookup"><span data-stu-id="de516-103">Add the Relay NPM package</span></span>

<span data-ttu-id="de516-104">Proje klasörünüzdeki bir Düğüm komut isteminden `npm install hyco-ws` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="de516-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-to-send-messages"></a><span data-ttu-id="de516-105">İleti göndermek için bazı kodlar yazma</span><span class="sxs-lookup"><span data-stu-id="de516-105">Write some code to send messages</span></span>

1. <span data-ttu-id="de516-106">Aşağıdaki `constants` öğesini `sender.js` dosyasının başına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="de516-106">Add the following `constants` to the top of the `sender.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. <span data-ttu-id="de516-107">Karma bağlantı ayrıntıları için şu sabitleri `sender.js` dosyasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="de516-107">Add the following constants to the `sender.js` file for the hybrid connection details.</span></span> <span data-ttu-id="de516-108">Köşeli ayraçlar içindeki yer tutucuları, karma bağlantıyı oluştururken aldığınız değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="de516-108">Replace the placeholders in brackets with the values you obtained when you created the hybrid connection.</span></span>
   
   1. <span data-ttu-id="de516-109">`const ns` - Geçiş ad alanı.</span><span class="sxs-lookup"><span data-stu-id="de516-109">`const ns` - The Relay namespace.</span></span> <span data-ttu-id="de516-110">Tam ad alanı adını kullandığınızdan emin olun: örneğin, `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="de516-110">Be sure to use the fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="de516-111">`const path` - Karma bağlantının adı.</span><span class="sxs-lookup"><span data-stu-id="de516-111">`const path` - The name of the hybrid connection.</span></span>
   3. <span data-ttu-id="de516-112">`const keyrule` - SAS anahtarının adı.</span><span class="sxs-lookup"><span data-stu-id="de516-112">`const keyrule` - The name of the SAS key.</span></span>
   4. <span data-ttu-id="de516-113">`const key` - SAS anahtarının değeri.</span><span class="sxs-lookup"><span data-stu-id="de516-113">`const key` - The SAS key value.</span></span>

3. <span data-ttu-id="de516-114">`sender.js` dosyasına aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="de516-114">Add the following code to the `sender.js` file:</span></span>
   
    ```js
    WebSocket.relayedConnect(
        WebSocket.createRelaySendUri(ns, path),
        WebSocket.createRelayToken('http://'+ns, keyrule, key),
        function (wss) {
            readline.on('line', (input) => {
                wss.send(input, null);
            });
   
            console.log('Started client interval.');
            wss.on('close', function () {
                console.log('stopping client interval');
                process.exit();
            });
        }
    );
    ```
    <span data-ttu-id="de516-115">Sender.js dosyanız aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="de516-115">Here is what your sender.js file should look like:</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    WebSocket.relayedConnect(
        WebSocket.createRelaySendUri(ns, path),
        WebSocket.createRelayToken('http://'+ns, keyrule, key),
        function (wss) {
            readline.on('line', (input) => {
                wss.send(input, null);
            });
   
            console.log('Started client interval.');
            wss.on('close', function () {
                console.log('stopping client interval');
                process.exit();
            });
        }
    );
    ```

