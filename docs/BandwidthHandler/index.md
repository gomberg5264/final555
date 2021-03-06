---
api_name: BandwidthHandler
api_description: BandwidthHandler allows you manage application-level bandwidth and many other SDP-attributes
---

{% capture html %}

  <section id="usage">
    <h2><a href="#usage">Usage</a></h2>
    <pre style="background:#fff;color:#000"><span style="color:#ff5600">var</span> BandwidthHandler <span style="color:#ff5600">=</span> connection.BandwidthHandler;
connection.bandwidth <span style="color:#ff5600">=</span> {
    audio: 128,
    video: 256,
    <span style="color:#a535ae">screen</span>: 300
};
<span style="color:#a535ae">connection</span>.<span style="color:#21439c">processSdp</span> <span style="color:#ff5600">=</span> <span style="color:#ff5600">function</span>(sdp) {
    sdp <span style="color:#ff5600">=</span> BandwidthHandler.setApplicationSpecificBandwidth(sdp, connection.bandwidth, <span style="color:#ff5600">!</span><span style="color:#ff5600">!</span>connection.session.<span style="color:#a535ae">screen</span>);
    sdp <span style="color:#ff5600">=</span> BandwidthHandler.setVideoBitrates(sdp, {
        min: connection.bandwidth.video,
        max: connection.bandwidth.video
    });

    sdp <span style="color:#ff5600">=</span> BandwidthHandler.setOpusAttributes(sdp);

    sdp <span style="color:#ff5600">=</span> BandwidthHandler.setOpusAttributes(sdp, {
        <span style="color:#00a33f">'stereo'</span>: 1,
        <span style="color:#919191">//'sprop-stereo': 1,</span>
        <span style="color:#00a33f">'maxaveragebitrate'</span>: connection.bandwidth.audio <span style="color:#ff5600">*</span> 1000 <span style="color:#ff5600">*</span> 8,
        <span style="color:#00a33f">'maxplaybackrate'</span>: connection.bandwidth.audio <span style="color:#ff5600">*</span> 1000 <span style="color:#ff5600">*</span> 8,
        <span style="color:#919191">//'cbr': 1,</span>
        <span style="color:#919191">//'useinbandfec': 1,</span>
        <span style="color:#919191">// 'usedtx': 1,</span>
        <span style="color:#00a33f">'maxptime'</span>: 3
    });

    <span style="color:#ff5600">return</span> sdp;
};
</pre>
  </section>

  <section id="description">
    <h2><a href="#description">Description</a></h2>
    <div class="datagrid">
    <table>
    <thead><tr><th>parameter</th><th>description</th></tr></thead>
    <tbody>
      <tr>
        <td>BandwidthHandler.setApplicationSpecificBandwidth</td>
        <td>
            Set "AS=kbps"<br>
            1) first parameter is "sdp" string<br>
            2) second parameter is "bandwidth" object {audio: 50, video: 100}<br>
            3) last parameter is "isScreen" boolean; which forces 300kbps minimum video bitrates
        </td>
      </tr>
      <tr>
        <td>BandwidthHandler.setVideoBitrates</td>
        <td>
          1) first parameter is "sdp" string<br>
          2) last parameter is {min: bitrates, max: bitrates}
        </td>
      </tr>
      <tr>
        <td>BandwidthHandler.setOpusAttributes</td>
        <td>
          1) first parameter is "sdp" string<br>
          2) last parameter accepts all following:<br><pre style="background:#fff;color:#000">{
    <span style="color:#00a33f">'stereo'</span>: 1,
    <span style="color:#00a33f">'sprop-stereo'</span>: 1,
    <span style="color:#00a33f">'maxaveragebitrate'</span>: connection.bandwidth.audio <span style="color:#ff5600">*</span> 1000 <span style="color:#ff5600">*</span> 8,
    <span style="color:#00a33f">'maxplaybackrate'</span>: connection.bandwidth.audio <span style="color:#ff5600">*</span> 1000 <span style="color:#ff5600">*</span> 8,
    <span style="color:#00a33f">'cbr'</span>: 1,
    <span style="color:#00a33f">'useinbandfec'</span>: 1,
    <span style="color:#00a33f">'usedtx'</span>: 1,
    <span style="color:#00a33f">'maxptime'</span>: 3
}
</pre>
        </td>
      </tr>
    </tbody>
    </table>
    </div>
  </section>

  <section id="demo">
    <h2><a href="#demo">Demo</a></h2>
    <pre style="background:#fff;color:#000"><span style="color:#ff5600">&lt;</span>script src<span style="color:#ff5600">=</span><span style="color:#00a33f">"https://rtcmulticonnection.herokuapp.com/dist/RTCMultiConnection.min.js"</span><span style="color:#ff5600">></span><span style="color:#ff5600">&lt;</span>/script<span style="color:#ff5600">></span>
<span style="color:#ff5600">&lt;</span>script src<span style="color:#ff5600">=</span><span style="color:#00a33f">"https://rtcmulticonnection.herokuapp.com/socket.io/socket.io.js"</span><span style="color:#ff5600">></span><span style="color:#ff5600">&lt;</span>/script<span style="color:#ff5600">></span>

<span style="color:#ff5600">&lt;</span>script<span style="color:#ff5600">></span>
<span style="color:#ff5600">var</span> connection <span style="color:#ff5600">=</span> <span style="color:#ff5600">new</span> <span style="color:#21439c">RTCMultiConnection</span>();

<span style="color:#919191">// this line is VERY_important</span>
connection.socketURL <span style="color:#ff5600">=</span> <span style="color:#00a33f">'https://rtcmulticonnection.herokuapp.com:443/'</span>;

<span style="color:#919191">// if you want audio+video conferencing</span>
connection.session <span style="color:#ff5600">=</span> {
    audio: <span style="color:#a535ae">true</span>,
    video: <span style="color:#a535ae">true</span>
};

<span style="color:#ff5600">var</span> BandwidthHandler <span style="color:#ff5600">=</span> connection.BandwidthHandler;
connection.bandwidth <span style="color:#ff5600">=</span> {
    audio: 128,
    video: 256,
    <span style="color:#a535ae">screen</span>: 300
};
<span style="color:#a535ae">connection</span>.<span style="color:#21439c">processSdp</span> <span style="color:#ff5600">=</span> <span style="color:#ff5600">function</span>(sdp) {
    sdp <span style="color:#ff5600">=</span> BandwidthHandler.setApplicationSpecificBandwidth(sdp, connection.bandwidth, <span style="color:#ff5600">!</span><span style="color:#ff5600">!</span>connection.session.<span style="color:#a535ae">screen</span>);
    sdp <span style="color:#ff5600">=</span> BandwidthHandler.setVideoBitrates(sdp, {
        min: connection.bandwidth.video,
        max: connection.bandwidth.video
    });

    sdp <span style="color:#ff5600">=</span> BandwidthHandler.setOpusAttributes(sdp);

    sdp <span style="color:#ff5600">=</span> BandwidthHandler.setOpusAttributes(sdp, {
        <span style="color:#00a33f">'stereo'</span>: 1,
        <span style="color:#919191">//'sprop-stereo': 1,</span>
        <span style="color:#00a33f">'maxaveragebitrate'</span>: connection.bandwidth.audio <span style="color:#ff5600">*</span> 1000 <span style="color:#ff5600">*</span> 8,
        <span style="color:#00a33f">'maxplaybackrate'</span>: connection.bandwidth.audio <span style="color:#ff5600">*</span> 1000 <span style="color:#ff5600">*</span> 8,
        <span style="color:#919191">//'cbr': 1,</span>
        <span style="color:#919191">//'useinbandfec': 1,</span>
        <span style="color:#919191">// 'usedtx': 1,</span>
        <span style="color:#00a33f">'maxptime'</span>: 3
    });

    <span style="color:#ff5600">return</span> sdp;
};

connection.openOrJoin(<span style="color:#00a33f">'your-room-id'</span>);
<span style="color:#ff5600">&lt;</span>/script<span style="color:#ff5600">></span>
</pre>
  </section>

{% endcapture %}
{% include html_snippet.html html=html %}
