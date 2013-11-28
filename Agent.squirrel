server.log("started on " + http.agenturl());

function requestHandler(request, response) {
    local reg = regexp("^[0-9]+$");
    local rex = regexp("(.*)=(.*)&");
    local msg = null;
    for(local i = 0; i < request.body.len(); i+=1)
    {
        local cap = rex.capture(request.body, i);
        local key = request.body.slice(cap[1].begin, cap[1].end)
        if(key == "Body")
        {
            msg = request.body.slice(cap[2].begin, cap[2].end);
            server.log(msg);
            msg = reg.capture((string) msg);
            sendToDevice(msg);
            break;
        }
        i = cap[2].end;
    }
    // send a response back saying everything was OK.
    response.header("content-type", "text/xml");
    response.send(200, "<Response><Message>Enjoy the piece.</Message></Response>");
}
function sendToDevice(msg) {
    device.send("incoming", msg);
}
 
function log (msg) {
    server.log(msg);
}


device.on("log", log);
// register the HTTP handler
http.onrequest(requestHandler);
