#BWCall
BWCall is used to control inbound/outbound audio calls. See [BWPhone](BWPhone.md) to create a BWCall.
#Api
##setRemoteAudioElement(element)
Sets the HTML audio element that will be used to play audio from the remote-side of the call.
If set after the call has connected, the audio will start playing immediately. If called before, it will automatically start playing once the call has connected.

**Parameters**

* `element` HTML element

HTML audio element

**Result**

no output


**Example**


```javascript
<audio id = "audio-remote"></audio>
var bwPhone = BWClient.createPhone({
    username: "user_123",
    domain: "prod.domain.com",
    password: "taco123",
});
var bwCall = bwPhone.call("bob@domain.com");
bwCall.setRemoteAudioElement(document.getElementById('audio-remote'));
```

##getInfo()
Returns call information

**Parameters**

None

**Result**
An object that contains information about the call

**Example**

```javascript
var info = call.getInfo();

//an example of what might be returned
{
	//direction is always given
	direction : "out",
    
    //state is always given. Possible states are
    // 'connecting', 'connected' 
    state     : "connecting",
    
    //your uri (always available for SIP calls)
    localUri  : "sip:bob123@domain.com",
    
    //the remote uri (always available for SIP calls)
    remoteUri : "sip:alice123@domain.com"
}
```

##hangup()
Hang up the call. The call must be in `connected` state.

**Parameters**

None

**Example**
```javascript
var bwCall = bwPhone.call("sip:user_234");
bwCall.on("ended",function(){
	//the call has ended
});
bwCall.hangup();
```

##sendDtmf(tone)
Send a DTMF (dual-tone multi-frequency) to the remote device.

**Parameters**

* `tone` String (size =1)

The tone to play. Can be (0-9), #,*


#Events
BWCall is an EventEmitter, and will emit the following events. No extra data is given with the event. Use `getInfo` to get additional information about the call.
###`connected`
For an outbound call, this is emitted once the call is connected, after the remote-audio has been started (if applicable).
###`ended`
The call has ended.

###Example
```javascript
var call = bwPhone.call("sip:jim-bob@domain.com");
call.on("connected",function(){
	//do something when the call has connected
});
```