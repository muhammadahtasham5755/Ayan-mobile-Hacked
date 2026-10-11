function rain(){cx.fillStyle="rgba(3,3,4,.12)";cx.fillRect(0,0,cv.width,cv.height);cx.fillStyle="#00ff7f";cx.font=fs+"px monospace";
for(var i=0;i<cols;i++){cx.fillText(ch[Math.floor(Math.random()*ch.length)],i*fs,drops[i]*fs);if(drops[i]*fs>cv.height&&Math.random()>.975)drops[i]=0;drops[i]++}}
if(!RM)setInterval(rain,60);
// sound (off by default)
var AC=null,on=false;
$("snd").onclick=function(){on=!on;this.textContent=on?"🔊 Sound on":"🔇 Sound off";this.setAttribute("aria-pressed",on);if(on&&!AC){try{AC=new(window.AudioContext||window.webkitAudioContext)()}catch(e){}}};
function beep(f){if(!on||!AC)return;var o=AC.createOscillator(),g=AC.createGain();o.frequency.value=f;g.gain.value=.03;o.connect(g);g.connect(AC.destination);o.start();o.stop(AC.currentTime+.08)}
// typing helper
function type(el,text,speed,done){var i=0;(function t(){if(i<text.length){el.textContent+=text.charAt(i++);if(i%3==0)beep(700);setTimeout(t,speed)}else if(done)done()})()}
// loading
var msgs=["INITIALIZING CYBER SYSTEM...","ESTABLISHING VIRTUAL CONNECTION...","STARTING SECURITY SIMULATION...","ANALYZING DEMONSTRATION DATA...","GENERATING SYSTEM REPORT...","PROCESSING SIMULATION RESULTS...","LOADING COMPLETE: 100%"];
var log=$("log"),intro=$("intro");
if(!RM)intro.classList.add("shake");
var DUR=RM?1500:15000,t0=performance.now(),mi=0,finished=false;
function nextMsg(){if(mi>=msgs.length)return;var d=document.createElement("div");log.insertBefore(d,null);var s=msgs[mi++];type(d,"> "+s,RM?0:22,function(){setTimeout(nextMsg,RM?0:DUR/msgs.length-s.length*22)})}
nextMsg();
function frame(now){var p=Math.min(1,(now-t0)/DUR),e=p*100;
$("pct").textContent=Math.floor(e)+"%";$("fill").style.width=e+"%";$("arc").style.strokeDashoffset=352*(1-p);
if(p<1)requestAnimationFrame(frame);else if(!finished){finished=true;setTimeout(showReport,900)}}
requestAnimationFrame(frame);
// report
function showReport(){intro.style.opacity=0;setTimeout(function(){intro.style.display="none";var r=$("report");r.style.display="block";window.scrollTo(0,0);requestAnimationFrame(function(){r.classList.add("on")});runReport()},RM?0:1000)}
function runReport(){
setInterval(function(){$("net").textContent=(Math.floor(Math.random()*900)+100)+" kb/s (fake)"},900);
var lines=["[01] Fictional scan stage 1 ... done","[02] Virtual network check ... OK (demo)","[03] Simulated security indicators ... green","[04] Demo encryption handshake ... complete","[05] Virtual server ping ... 12ms (fictional)","[06] Demonstration tasks ... 6/6 completed","[07] Real device data accessed ... NONE","[08] Report status ... READY"];
var el=$("tr"),i=0;(function nx(){if(i<lines.length){var s=lines[i++]+"\n";type(el,s,RM?0:18,function(){setTimeout(nx,RM?0:250)})}else el.classList.remove("cur")})()}
})();
</script>
</body>
</html>

