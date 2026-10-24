
<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>EGG TERMINAL</title>
<style>
:root { color-scheme: dark; }
* { box-sizing: border-box; }
body {
  margin:0; padding:20px;
  background:#080808; color:#ff4545;
  font-family:monospace;
}
h1 {
  border-bottom:1px solid #ff3333;
  padding-bottom:12px; letter-spacing:3px;
}
h3 { margin-top:0; }
.warning {
  border:1px solid red; padding:12px;
  margin:20px 0; background:#210606; line-height:1.8;
}
.panel {
  border:1px solid #522020;
  background:#100909; padding:12px; margin:16px 0;
}
.panel-title { color:#ff7777; margin-bottom:10px; }
.level-list { display:grid; gap:8px; }
.level-item {
  display:flex; justify-content:space-between;
  gap:8px; font-size:12px;
}
.locked { color:#666; }
.unlocked { color:#ff4545; }
.bar { height:6px; background:#301010; margin-top:12px; }
#progress {
  height:6px; width:20%; background:#ff4545;
  transition:width .3s;
}
#output {
  white-space:pre-wrap; overflow-wrap:anywhere;
  line-height:1.7; color:#ff7777; min-height:180px;
}
.row { display:flex; gap:8px; }
input {
  flex:1; width:0; min-width:0;
  background:#111; color:#ff5555;
  border:1px solid #833; padding:12px;
  font-family:monospace; font-size:16px;
}
button {
  background:#500; color:white; border:1px solid red;
  padding:10px 14px; font-family:monospace;
  font-size:14px; cursor:pointer;
}
button:active { background:#900; }
.note { color:#777; font-size:12px; line-height:1.7; }
#alert {
  display:none; border:1px solid #ff2222;
  background:#350000; color:#ff5555;
  padding:12px; margin:14px 0;
  animation:flicker .25s infinite alternate;
}
@keyframes flicker {
  from { opacity:1; }
  to { opacity:.65; }
}
.glitch { animation:shake .15s 3; }
@keyframes shake {
  0% { transform:translateX(0); }
  25% { transform:translateX(3px); }
  50% { transform:translateX(-3px); }
  100% { transform:translateX(0); }
}
button:focus-visible, input:focus-visible {
  outline:2px solid #ff7777;
}
#guideButton {
  width:100%; margin-top:12px;
  padding:13px; background:#160b20;
  color:#C084FC; border:1px solid #C084FC;
}
#guideButton:active { background:#35164b; }
#cellRecords {
  display:none; margin:20px 0; line-height:1.8;
}
.cell-card {
  padding:12px; margin-bottom:12px;
  background:#100909;
}
.cell-purple { color:#C084FC; border:1px solid #C084FC; }
.cell-green { color:#39FF88; border:1px solid #39FF88; }
.cell-orange { color:#FF922B; border:1px solid #FF922B; }
.cell-red { color:#FF4545; border:1px solid #FF4545; }
.cell-blue { color:#249BFF; border:1px solid #249BFF; }
#cellRecords h3 { font-size:16px; }
</style>
</head>
<body>

<h1>EGG TERMINAL</h1>

<div class="warning">
⚠ RESTRICTED RESEARCH SYSTEM<br>
ACCESS LEVEL: <span id="accessLabel">LEVEL 01</span><br>
SUBJECT: A-1<br>
CONNECTION: <span id="connection">ONLINE</span>
</div>

<div id="alert" role="alert">
⚠ SYSTEM WARNING<br>
비정상적인 접근 기록이 감지되었습니다.
</div>

<div class="panel">
  <div class="panel-title">SECURITY CLEARANCE</div>
  <div class="level-list" id="levels"></div>
  <div class="bar"><div id="progress"></div></div>
  <p id="levelDescription" class="note">
    일반 시스템 접근 권한이 활성화되었습니다.
  </p>
</div>

<div class="panel">
  <div class="panel-title">SYSTEM MONITOR</div>
  <div id="monitor" class="note">
    SYSTEM: ONLINE<br>
    UNKNOWN CONNECTIONS: 0<br>
    INCIDENTS: 0
  </div>
</div>

<div id="output" aria-live="polite">EGG OS v4.0.4
연구소 연결 대기 중...
시스템이 시작되었습니다.
보안 등급: LEVEL 01
명령어를 입력하세요. (help 입력 가능)</div>

<br>

<div class="row">
  <input id="cmd" placeholder="명령어 입력..."
    autocomplete="off" autocapitalize="none"
    spellcheck="false" aria-label="명령어 입력">
  <button id="run" type="button">실행</button>
</div>

<button id="guideButton" type="button">
  📁 세포 도감 열기
</button>

<p class="note">
EGG RESEARCH LABORATORY<br>
UNAUTHORIZED ACCESS IS PROHIBITED.
</p>

<div id="cellRecords">

  <div class="cell-card cell-purple">
    <h3>작은창자상피세포 관련 문서</h3>
    작은창자상피세포는 제1세상의 초기 세포다.<br>
    능력: 분열 (많이 하면 부작용 발생)
  </div>

  <div class="cell-card cell-green">
    <h3>잎살세포 관련 문서</h3>
    잎살세포는 제1세상의 초기 세포다.<br>
    능력: 뇌지컬이 뛰어남
  </div>

  <div class="cell-card cell-orange">
    <h3>신경세포 관련 문서</h3>
    신경세포는 제1세상의 초기 세포다.<br>
    능력: 위기를 느낄 때 빠르게 달릴 수 있음
  </div>

  <div class="cell-card cell-red">
    <h3>적혈구 관련 문서</h3>
    적혈구는 제1세상의 초기 세포다.<br>
    능력: 상처 회복 (발동 조건은 아직 연구되지 않음)
  </div>

  <div class="cell-card cell-blue">
    <h3>물곰 관련 문서</h3>
    물곰은 제1.5세상의 초기 미생물이다.<br>
    능력: 절대 죽지 않음 (실험 가능)
  </div>

</div>

<script>
const output = document.getElementById("output");
const input = document.getElementById("cmd");
const alertBox = document.getElementById("alert");
const connection = document.getElementById("connection");
const cellRecords = document.getElementById("cellRecords");

const GUIDE_URL =
  "https://m.blog.naver.com/badwars_ghosts/224307549809";

let accessLevel = 1;
let unknownConnections = 0;
let incidents = 0;
let commandCount = 0;
let traced = false;
let rebooted = false;
let originRead = false;
let glitchActive = false;

const levelNames = [
  "일반 시스템",
  "제한된 연구 기록",
  "기밀 연구 자료",
  "실험체 관련 자료",
  "최고 기밀 데이터"
];

const files = [
  {
    name:"session_001.log", level:1,
    content:`[SESSION 001]
실험체 A-1 반응 확인.
연구원 기록: 관찰 대상이 모니터를 바라보고 있었다.
주의: 해당 문장은 이후 기록에서 삭제됨.`
  },
  {
    name:"subject_A1.dat", level:2,
    content:`[SUBJECT A-1]
분류: UNKNOWN
최초 반응: 기록 불명
관찰 결과: 실험체가 연구원의 행동을 예측함.
추가 기록: 관찰 대상은 카메라를 알고 있었음.`
  },
  {
    name:"incident_0404.log", level:3,
    content:`[INCIDENT 0404]
경고: 기록 일부 손상.
실험실 모니터에서 등록되지 않은 메시지 발견.
"에그, 네가 보고 있다는 걸 알아."
작성자: UNKNOWN`
  },
  {
    name:"experiment_017.log", level:4,
    content:`[EXPERIMENT 017]
연구 기록 상태: RESTRICTED
실험체 A-1 관련 기록이 예정보다 먼저 생성됨.
기록 생성 시간: 실험 시작 이전.
담당 연구원 서명: [DATA CORRUPTED]`
  },
  {
    name:"origin.dat", level:5,
    content:`[ORIGIN FILE]
최고 기밀 기록 접근 완료.

A-1의 최초 생성 기록을 찾을 수 없음.
실험 일지에는 생성 이전의 관찰 기록이 존재함.

마지막 기록:
"우리가 발견한 것이 아니라,
처음부터 그곳에 있었던 것이라면?"

파일 끝.`
  },
  {
    name:"connection.log", level:2,
    content:`[CONNECTION LOG]
등록된 연구원: EGG
최근 접속: 확인 불가
접속 위치: UNKNOWN
접속 세션: SESSION ???`
  },
  {
    name:"deleted_0404.log", level:5,
    content:`[RECOVERED FILE]
삭제된 기록 복구 완료.

EGG: 누가 접속했지?
UNKNOWN: 당신이 처음 접속했을 때부터.
EGG: 이건 내 연구소다.
UNKNOWN: 정말 그렇게 생각해?

[기록 종료]`
  }
];

const logs = [];

function print(text) {
  output.textContent += "\n" + text;
  window.scrollTo(0, document.body.scrollHeight);
}

function logEvent(text) {
  logs.push(
    "[" + new Date().toLocaleTimeString("ko-KR") + "] " + text
  );
  if (logs.length > 30) logs.shift();
  updateMonitor();
}

function updateMonitor() {
  document.getElementById("monitor").innerHTML =
    "SYSTEM: " + (rebooted ? "RECOVERED" : "ONLINE") +
    "<br>UNKNOWN CONNECTIONS: " + unknownConnections +
    "<br>INCIDENTS: " + incidents +
    "<br>COMMANDS EXECUTED: " + commandCount;
}

function updateSecurity() {
  document.getElementById("accessLabel").textContent =
    "LEVEL 0" + accessLevel;

  document.getElementById("progress").style.width =
    (accessLevel / 5 * 100) + "%";

  document.getElementById("levelDescription").textContent =
    levelNames[accessLevel - 1] +
    " 접근 권한이 활성화되었습니다.";

  const levels = document.getElementById("levels");
  levels.replaceChildren();

  levelNames.forEach((name, index) => {
    const level = index + 1;
    const item = document.createElement("div");
    item.className = "level-item";

    const label = document.createElement("span");
    label.textContent = "LEVEL 0" + level + " · " + name;

    const status = document.createElement("span");
    status.textContent =
      level <= accessLevel ? "UNLOCKED" : "LOCKED";
    status.className =
      level <= accessLevel ? "unlocked" : "locked";

    item.append(label, status);
    levels.appendChild(item);
  });

  updateMonitor();
}

function openGuide() {
  logEvent("세포 도감 접속 시도");

  const opened = window.open(GUIDE_URL, "_blank");

  if (opened) {
    print("도감 연결 요청 완료.");
    print("미친세포들 세포 도감을 새 창에서 엽니다.");
  } else {
    print("새 창이 차단되었습니다.");
    print("아래의 [세포 도감 열기] 버튼을 다시 눌러 보세요.");
    print("직접 접속: " + GUIDE_URL);
  }
}

function showFiles() {
  let result = "[FILE DIRECTORY]\n";

  files.forEach(file => {
    result +=
      (file.level <= accessLevel ? "[OPEN] " : "[LOCKED] ") +
      file.name + "\n";
  });

  result += "\n접근 가능: " +
    files.filter(f => f.level <= accessLevel).length;
  result += "\n잠김: " +
    files.filter(f => f.level > accessLevel).length;

  print(result);
}

function readFile(name) {
  const file = files.find(item =>
    item.name.toLowerCase() === name.toLowerCase()
  );

  if (!file) {
    print("오류: 파일을 찾을 수 없습니다.");
    return;
  }

  if (accessLevel < file.level) {
    print(
      "⚠ ACCESS DENIED\n파일: " + file.name +
      "\n필요 권한: LEVEL 0" + file.level +
      "\n현재 권한: LEVEL 0" + accessLevel
    );
    logEvent("권한 없는 파일 접근 시도: " + file.name);
    return;
  }

  print(file.content);
  logEvent("파일 열람: " + file.name);

  if (file.name === "origin.dat") {
    originRead = true;
    print(
      "\n[추가 기록]\n명령어 trace로 접속 기록을 확인할 수 있습니다."
    );
  }

  if (file.name === "deleted_0404.log") {
    print(
      "\n⚠ 복구된 기록은 실제 연구소의 기록과 다를 수 있습니다."
    );
  }
}

function unlockLevel(password) {
  const pass = password.toLowerCase();

  const credentials = {
    "cell-204":3,
    "egg-7319":4,
    "origin-000":5
  };

  if (pass === "a1-0404") {
    if (accessLevel >= 2) {
      print("이미 A-1 기록 접근 권한이 활성화되어 있습니다.");
      return;
    }

    accessLevel = 2;
    updateSecurity();
    logEvent("LEVEL 02 인증 성공");

    print(
      "인증 성공.\nACCESS GRANTED: LEVEL 02\n" +
      "subject_A1.dat 접근 가능.\n" +
      "[비밀 기록] A-1은 처음부터 깨어 있었다."
    );
    return;
  }

  const targetLevel = credentials[pass];

  if (!targetLevel) {
    print("인증 실패: 등록되지 않은 인증 코드입니다.");
    logEvent("인증 실패");
    return;
  }

  if (targetLevel <= accessLevel) {
    print("이 보안 등급은 이미 해금되었습니다.");
    return;
  }

  if (targetLevel !== accessLevel + 1) {
    print(
      "ACCESS DENIED\n현재 단계의 인증을 먼저 완료해야 합니다."
    );
    return;
  }

  accessLevel = targetLevel;
  updateSecurity();
  logEvent("LEVEL 0" + accessLevel + " 인증 성공");

  print(
    "인증 성공.\nACCESS GRANTED: LEVEL 0" + accessLevel +
    "\n권한: " + levelNames[accessLevel - 1] +
    "\n새로운 파일이 해금되었습니다."
  );
}

function triggerIncident() {
  incidents++;
  unknownConnections++;
  glitchActive = true;

  alertBox.style.display = "block";
  document.body.classList.remove("glitch");
  void document.body.offsetWidth;
  document.body.classList.add("glitch");

  connection.textContent = "UNSTABLE";
  logEvent("비정상 이벤트 발생");

  print(
    "⚠ SYSTEM ALERT\n" +
    "등록되지 않은 접속이 감지되었습니다.\n" +
    "접속자: UNKNOWN\n" +
    "세션: A1-????\n" +
    "경고: 이 기록은 자동으로 생성되었습니다."
  );

  updateMonitor();
}

function traceConnections() {
  print("[CONNECTION TRACE]\n최근 접속 기록:");

  if (logs.length === 0) {
    print("기록이 없습니다.");
    return;
  }

  logs.slice(-8).forEach(line => print(line));

  if (!traced) {
    traced = true;
    print(
      "\n[UNKNOWN SESSION]\n" +
      "접속 시간: 기록 손상\n" +
      "접속자: UNKNOWN\n" +
      "상태: 아직 연결되어 있음"
    );
    triggerIncident();
  }
}

function rebootSystem() {
  alertBox.style.display = "none";
  document.body.classList.remove("glitch");
  glitchActive = false;
  rebooted = true;
  connection.textContent = "ONLINE";

  print(
    "[SYSTEM REBOOT]\n" +
    "시스템 점검 중...\n" +
    "터미널 화면 복구 완료.\n" +
    "보안 등급은 유지됩니다."
  );

  logEvent("시스템 복구 완료");
  updateMonitor();
}

function runCommand() {
  const raw = input.value.trim();
  const cmd = raw.toLowerCase();

  if (!cmd) return;

  print("> " + raw);
  commandCount++;

  if (cmd === "help") {
    print(
`사용 가능한 명령어:
help                 - 명령어 목록
status               - 시스템 상태
security             - 보안 등급 확인
files                - 파일 목록
cells                - 세포 소개 문서 열기
도감                 - 네이버 블로그 세포 도감 열기
access a1-0404       - A-1 인증
unlock [인증 코드]   - 보안 등급 해금
cat [파일명]         - 파일 읽기
logs                 - 접속 기록 확인
trace                - 접속자 추적
incident             - 시스템 이벤트 확인
scan                 - 시스템 검사
reboot               - 시스템 복구
clear                - 화면 초기화

파일 읽기 예시:
cat session_001.log

접속 기록 예시:
logs
trace`
    );
  }

  else if (cmd === "status") {
    print(
      "시스템: " + (rebooted ? "RECOVERED" : "ONLINE") +
      "\n연구소: EGG\n대상 실험체: A-1" +
      "\n기록 상태: 일부 손상\n보안 등급: LEVEL 0" + accessLevel
    );
  }

  else if (cmd === "security") {
    print(
      "SECURITY STATUS\n현재 등급: LEVEL 0" + accessLevel +
      "\n권한 이름: " + levelNames[accessLevel - 1] +
      "\n최고 등급: LEVEL 05\n접근 가능 파일: " +
      files.filter(f => f.level <= accessLevel).length +
      "/" + files.length
    );
  }

  else if (cmd === "files") {
    showFiles();
  }

  else if (cmd === "도감") {
    openGuide();
  }

  else if (cmd === "cells") {
    cellRecords.style.display = "block";
    print("세포 소개 문서가 열렸습니다.");
    print("초기 세포 기록을 확인하십시오.");
    cellRecords.scrollIntoView({
      behavior: "smooth",
      block: "start"
    });
  }

  else if (cmd === "access a1-0404") {
    unlockLevel("a1-0404");
  }

  else if (cmd.startsWith("unlock ")) {
    unlockLevel(raw.slice(7).trim());
  }

  else if (cmd.startsWith("cat ")) {
    const name = raw.slice(4).trim();
    if (!name) print("오류: 파일명을 입력하세요.");
    else readFile(name);
  }

  else if (cmd === "logs") {
    print("[SYSTEM LOG]");
    if (logs.length === 0) print("저장된 기록이 없습니다.");
    else logs.slice(-10).forEach(line => print(line));
  }

  else if (cmd === "trace") {
    traceConnections();
  }

  else if (cmd === "incident") {
    print(
      "INCIDENT REPORT\n" +
      "발생 사건: " + incidents +
      "\n미확인 접속: " + unknownConnections +
      "\n상태: " + (glitchActive ? "WARNING" : "STANDBY")
    );
  }

  else if (cmd === "scan") {
    print(
      "[SYSTEM SCAN]\n" +
      "파일 시스템: 정상\n" +
      "보안 모듈: 정상\n" +
      "접속 기록: " + (traced ? "이상 발견" : "검사 완료") +
      "\nA-1 상태: UNKNOWN"
    );

    if (!traced && accessLevel >= 2) {
      print("\n주의: 출처가 확인되지 않은 세션이 발견되었습니다.");
    }
  }

  else if (cmd === "reboot") {
    rebootSystem();
  }

  else if (cmd === "clear") {
    output.textContent =
      "EGG OS v4.0.4\n화면이 초기화되었습니다.";
  }

  else {
    print("오류: 알 수 없는 명령어.\n명령이 기록되었습니다.");
    logEvent("알 수 없는 명령어 입력");

    if (!traced && commandCount >= 5) {
      print("\n알 수 없는 응답이 감지되었습니다.");
    }
  }

  input.value = "";
  updateMonitor();
}

document.getElementById("run").addEventListener("click", runCommand);

input.addEventListener("keydown", event => {
  if (event.key === "Enter") runCommand();
});

document.getElementById("guideButton").addEventListener(
  "click",
  openGuide
);

updateSecurity();
logEvent("EGG TERMINAL 시작");
</script>

</body>
</html>
