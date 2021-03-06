---
api_name: streamEvents
api_description: This object stores all local and remote streams
---

{% capture html %}

  <section>
    <p>Use this object to access any stream (local or remote) from any user (based on userid or streamid).</p>
  </section>

  <section id="get-by-streamid">
    <h2><a href="#get-by-streamid">Get a stream using "streamid"</a></h2>
    <pre style="background:#fff;color:#000"><span style="color:#ff5600">var</span> stream <span style="color:#ff5600">=</span> connection.streamEvents[<span style="color:#00a33f">'stream-id'</span>].stream;
</pre>
  </section>

  <section id="get-by-userid">
    <h2><a href="#get-by-userid">Get all streams by userid</a></h2>
    <pre style="background:#fff;color:#000"><span style="color:#ff5600">var</span> allStreams <span style="color:#ff5600">=</span> [];

<span style="color:#a535ae">Object</span>.keys(connection.streamEvents).forEach(<span style="color:#ff5600">function</span>(streamid) {
    <span style="color:#ff5600">var</span> <span style="color:#a535ae">event</span> <span style="color:#ff5600">=</span> connection.streamEvents[streamid];

    <span style="color:#ff5600">if</span> (<span style="color:#a535ae">event</span>.userid <span style="color:#ff5600">===</span> <span style="color:#00a33f">'your-preferred-userid'</span>) {
        allStreams.<span style="color:#a535ae">push</span>(<span style="color:#a535ae">event</span>.stream);
    }
});

<span style="color:#a535ae">alert</span>(allStreams.<span style="color:#a535ae">length</span>);
</pre>
  </section>

  <section id="mute-unmute">
    <h2><a href="#mute-unmute">Mute or UnMute a stream by streamid</a></h2>
    <pre style="background:#fff;color:#000"><span style="color:#919191">// you can pass: 'audio' || 'video' || 'both</span>
connection.streamEvents[<span style="color:#00a33f">'stream-id'</span>].stream.mute(<span style="color:#00a33f">'both'</span>);

<span style="color:#919191">// or unmute</span>
connection.streamEvents[<span style="color:#00a33f">'stream-id'</span>].stream.unmute(<span style="color:#00a33f">'both'</span>);
</pre>
  </section>

  <section id="selectFirst">
    <h2><a href="#selectFirst">Use "selectFirst" to select first available stream</a></h2>
    <pre style="background:#fff;color:#000"><span style="color:#ff5600">var</span> firstStreamEvent <span style="color:#ff5600">=</span> connection.streamEvents.selectFirst({
    local: <span style="color:#a535ae">true</span>
});

firstStreamEvent.stream.getVideoTracks().forEach(<span style="color:#ff5600">function</span>(track) {
    track.<span style="color:#a535ae">stop</span>();
});
</pre>

    <div class="datagrid">
    <table>
    <thead><tr><th>parameter</th><th>description</th><th>usage</th></tr></thead>
    <tbody>
      <tr>
        <td>local:true</td>
        <td>get your first local stream</td>
        <td>
        <pre style="background:#fff;color:#000"><span style="color:#ff5600">var</span> firstLocalStream <span style="color:#ff5600">=</span> connection.streamEvents.selectFirst({
    local: <span style="color:#a535ae">true</span>
}).stream;
</pre>
        </td>
      </tr>

      <tr>
        <td>isVideo:true</td>
        <td>get first local or remote video stream (camera-only stream)</td>
        <td>
        <pre style="background:#fff;color:#000"><span style="color:#ff5600">var</span> firstLocalCameraStream <span style="color:#ff5600">=</span> connection.streamEvents.selectFirst({
    local: <span style="color:#a535ae">true</span>,
    isVideo: <span style="color:#a535ae">true</span>
}).stream;
</pre>
        </td>
      </tr>

      <tr>
        <td>isAudio:true</td>
        <td>get first local or remote audio stream (microphone-only stream)</td>
        <td>
        <pre style="background:#fff;color:#000"><span style="color:#ff5600">var</span> firstLocalMicrophoneStream <span style="color:#ff5600">=</span> connection.streamEvents.selectFirst({
    local: <span style="color:#a535ae">true</span>,
    isAudio: <span style="color:#a535ae">true</span>
}).stream;
</pre>
        </td>
      </tr>

      <tr>
        <td>remote:true</td>
        <td>get first remote stream</td>
        <td>
        <pre style="background:#fff;color:#000"><span style="color:#ff5600">var</span> firstRemoteStream <span style="color:#ff5600">=</span> connection.streamEvents.selectFirst({
    remote: <span style="color:#a535ae">true</span>
}).stream;
</pre>
        </td>
      </tr>

      <tr>
        <td>userid:string</td>
        <td>get first stream by a userid</td>
        <td>
        <pre style="background:#fff;color:#000"><span style="color:#ff5600">var</span> selectedUserFirstStream <span style="color:#ff5600">=</span> connection.streamEvents.selectFirst({
    userid: <span style="color:#00a33f">'selected-user-id'</span>
}).stream;
</pre>
        </td>
      </tr>

      <tr>
        <td>isScreen:true</td>
        <td>get first screen stream</td>
        <td>
        <pre style="background:#fff;color:#000"><span style="color:#ff5600">var</span> firstScreenStream <span style="color:#ff5600">=</span> connection.streamEvents.selectFirst({
    isScreen: <span style="color:#a535ae">true</span>
}).stream;
</pre>
        </td>
      </tr>
    </tbody>
    </table>
    </div>
  </section>

  <section id="selectAll">
    <h2><a href="#selectAll">Use "selectAll" to select all streams</a></h2>
    <pre style="background:#fff;color:#000">connection.streamEvents.selectAll({
    userid: <span style="color:#00a33f">'remote-userid'</span>
}).forEach(<span style="color:#ff5600">function</span>(streamEvent) {
    streamEvent.stream.getVideoTracks();
});
</pre>

    <div class="datagrid">
    <table>
    <thead><tr><th>parameter</th><th>description</th><th>usage</th></tr></thead>
    <tbody>
      <tr>
        <td>local:true</td>
        <td>get all local streams</td>
        <td>
        <pre style="background:#fff;color:#000">connection.streamEvents.selectAll({
    local: <span style="color:#a535ae">true</span>
}).forEach(<span style="color:#ff5600">function</span>(localStreamEvent) {
    localStreamEvent.stream.getVideoTracks();
});
</pre>
        </td>
      </tr>

      <tr>
        <td>isVideo:true</td>
        <td>get all local or remote video streams (camera-only streams)</td>
        <td>
        <pre style="background:#fff;color:#000">connection.streamEvents.selectAll({
    local: <span style="color:#a535ae">true</span>,
    isVideo: <span style="color:#a535ae">true</span>
}).forEach(<span style="color:#ff5600">function</span>(localVideoStreamEvent) {
    localVideoStreamEvent.stream.getVideoTracks();
});
</pre>
        </td>
      </tr>

      <tr>
        <td>isAudio:true</td>
        <td>get all local or remote audio streams (microphone-only streams)</td>
        <td>
        <pre style="background:#fff;color:#000">connection.streamEvents.selectAll({
    local: <span style="color:#a535ae">true</span>,
    isAudio: <span style="color:#a535ae">true</span>
}).forEach(<span style="color:#ff5600">function</span>(localAudioStreamEvent) {
    localAudioStreamEvent.stream.getVideoTracks();
});
</pre>
        </td>
      </tr>

      <tr>
        <td>remote:true</td>
        <td>get all remote streams</td>
        <td>
        <pre style="background:#fff;color:#000">connection.streamEvents.selectAll({
    remote: <span style="color:#a535ae">true</span>
}).forEach(<span style="color:#ff5600">function</span>(remoteStreamEvent) {
    remoteStreamEvent.stream.getVideoTracks();
});
</pre>
        </td>
      </tr>

      <tr>
        <td>userid:string</td>
        <td>get all streams by a userid</td>
        <td>
        <pre style="background:#fff;color:#000">connection.streamEvents.selectAll({
    userid: <span style="color:#00a33f">'selected-user-id'</span>
}).forEach(<span style="color:#ff5600">function</span>(remoteStreamEvent) {
    remoteStreamEvent.stream.getVideoTracks();
});
</pre>
        </td>
      </tr>

      <tr>
        <td>isScreen:true</td>
        <td>get all screen streams</td>
        <td>
        <pre style="background:#fff;color:#000">connection.streamEvents.selectAll({
    isScreen: <span style="color:#a535ae">true</span>
}).forEach(<span style="color:#ff5600">function</span>(screenEvent) {
    screenEvent.stream.getVideoTracks();
});
</pre>
        </td>
      </tr>
    </tbody>
    </table>
    </div>
  </section>

  <section id="takeSnapshot">
    <h2><a href="#takeSnapshot">Use "takeSnapshot" to get video snapshots</a></h2>

    <pre style="background:#fff;color:#000"><span style="color:#919191">// get first local video's snpashot</span>
connection.streamEvents.selectFirst({
    local: <span style="color:#a535ae">true</span>
}).takeSnapshot(<span style="color:#ff5600">function</span>(snapshotImage, blob) {
    yourImage.<span style="color:#a535ae">src</span> <span style="color:#ff5600">=</span> snapshotImage;
});


<span style="color:#919191">// get all remote videos' snapshots</span>
connection.streamEvents.selectAll({
    remote: <span style="color:#a535ae">true</span>
}).takeSnapshot(<span style="color:#ff5600">function</span>(snapshotImage, blob) {
    yourImage.<span style="color:#a535ae">src</span> <span style="color:#ff5600">=</span> snapshotImage;
});
</pre>
  </section>

  <section id="forEach">
    <h2><a href="#forEach">Use "forEach" to iterate over stream events</a></h2>

    <pre style="background:#fff;color:#000">connection.streamEvents.selectAll().forEach(<span style="color:#ff5600">function</span>(streamEvent) {
    streamEvent.stream.getVideoTracks();
});
</pre>
  </section>

  <section id="mute">
    <h2><a href="#mute">Use "mute" to disable your outgoing stream</a></h2>

    <pre style="background:#fff;color:#000"><span style="color:#919191">// mute first local stream</span>
connection.streamEvents.selectFirst(<span style="color:#00a33f">'local'</span>).mute();

<span style="color:#919191">// mute all local streams</span>
connection.streamEvents.selectAll(<span style="color:#00a33f">'local'</span>).mute();

<span style="color:#919191">// mute first local screen stream</span>
connection.streamEvents.selectFirst({
    isScreen: <span style="color:#a535ae">true</span>,
    local: <span style="color:#a535ae">true</span>
}).mute();

<span style="color:#919191">// mute first local stream's audio tracks (only audio tracks)</span>
connection.streamEvents.selectFirst().mute(<span style="color:#00a33f">'audio'</span>);
</pre>
  </section>

  <section id="unmute">
    <h2><a href="#unmute">Use "unmute" to disable your outgoing stream</a></h2>

    <pre style="background:#fff;color:#000"><span style="color:#919191">// unmute first local stream</span>
connection.streamEvents.selectFirst(<span style="color:#00a33f">'local'</span>).unmute();

<span style="color:#919191">// unmute all local streams</span>
connection.streamEvents.selectAll(<span style="color:#00a33f">'local'</span>).unmute();

<span style="color:#919191">// unmute first local screen stream</span>
connection.streamEvents.selectFirst({
    isScreen: <span style="color:#a535ae">true</span>,
    local: <span style="color:#a535ae">true</span>
}).unmute();

<span style="color:#919191">// unmute first local stream's audio tracks (only audio tracks)</span>
connection.streamEvents.selectFirst().unmute(<span style="color:#00a33f">'audio'</span>);
</pre>
  </section>

{% endcapture %}
{% include html_snippet.html html=html %}
