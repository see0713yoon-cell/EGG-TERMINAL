<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>EGG TERMINAL</title>
<style>
:root {
  color-scheme: dark;
}
body {
  margin: 0;
  padding: 22px;
  background: #080808;
  color: #ff4545;
  font-family: monospace;
}
h1 {
  border-bottom: 1px solid #ff3333;
  padding-bottom: 12px;
  letter-spacing: 3px;
}
.warning {
  border: 1px solid red;
  padding: 12px;
  margin: 20px 0;
  background: #210606;
  line-height: 1.8;
}
.panel {
  border: 1px solid #522020;
  background: #100909;
  padding: 12px;
  margin: 16px 0;
}
.panel-title {
  color: #ff7777;
  margin-bottom: 10px;
}
.level-list {
  display: grid;
  gap: 8px;
}
.level-item {
  display: flex;
  justify-content: space-between;
  gap: 8px;
  font-size: 13px;
}
.locked {
  color: #666;
}
.unlocked {
  color: #ff4545;
}
.bar {
  height: 6px;
  background: #301010;
  margin-top: 12px;
}
#progress {
  height: 6px;
  width: 20%;
  background: #ff4545;
  transition: width .3s;
}
#output {
  white-space: pre-wrap;
  overflow-wrap: anywhere;
  line-height: 1.7;
  color: #ff7777;
  min-height: 180px;
}
.row {
  display: flex;
  gap: 8px;
}
input {
  flex: 1;
  width: 0;
  min-width: 0;
  background: #111;
  color: #ff5555;
  border: 1px solid #833;
  border-radius: 0;
  padding: 12px;
  font-family: monospace;
  font-size: 16px;
}
button {
  background: #500;
  color: white;
  border: 1px solid red;
  padding: 10px 14px;
  font-family: monospace;
  font-size: 14px;
  cursor: pointer;
}
button:active {
  background: #900;
}
.note {
  color: #777;
  font-size: 12px;
  line-height: 1.7;
}
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

<div class="panel">
  <div class="panel-title">SECURITY CLEARANCE</div>
  <div class="level-list" id="levels"></div>
  <div class="bar"><div id="progress"></div></div>
  <p id="levelDescription" class="note">
    일반 시스템 접근 권한이 활성화되었습니다.
  </p>
</div>

<div id="output">EGG OS v4.0.4
연구소 연결 대기 중...
시스템이 시작되었습니다.
보안 등급: LEVEL 01
명령어를 입력하세요. (help 입력 가능)</div>

<br>
<div class="row">
  <input id="cmd" placeholder="명령어 입력..."
         autocomplete="off" autocapitalize="none"
         spellcheck="false">
  <button id="run" type="button">실행</button>
</div>

<p class="note">
EGG RESEARCH LABORATORY<br>
UNAUTHORIZED ACCESS IS PROHIBITED.
</p>

<script>
const output = document.getElementById("output");
const input = document.getElementById("cmd");

let accessLevel = 1;

const levelNames = [
  "일반 시스템",
  "제한된 연구 기록",
  "기밀 연구 자료",
  "실험체 관련 자료",
  "최고 기밀 데이터"
];

const files = [
  {
    name: "session_001.log",
    level: 1,
    content:
`[SESSION 001]
실험체 A-1 반응 확인.
연구원 기록: 관찰 대상이 모니터를 바라보고 있었다.
주의: 해당 문장은 이후 기록에서 삭제됨.`
  },
  {
    name: "subject_A1.dat",
    level: 2,
    content:
`[SUBJECT A-1]
분류: UNKNOWN
최초 반응: 기록 불명
관찰 결과: 실험체가 연구원의 행동을 예측함.
추가 기록: 관찰 대상은 카메라를 알고 있었음.`
  },
  {
    name: "incident_0404.log",
    level: 3,
    content:
`[INCIDENT 0404]
경고: 기록 일부 손상.
실험실 모니터에서 등록되지 않은 메시지 발견.
메시지 내용:
"에그, 네가 보고 있다는 걸 알아."
작성자: UNKNOWN`
  },
  {
    name: "experiment_017.log",
    level: 4,
    content:
`[EXPERIMENT 017]
연구 기록 상태: RESTRICTED
실험체 A-1 관련 기록이 예정보다 먼저 생성됨.
기록 생성 시간: 실험 시작 이전.
담당 연구원 서명: [DATA CORRUPTED]`
  },
  {
    name: "origin.dat",
    level: 5,
    content:
`[ORIGIN FILE]
최고 기밀 기록 접근 완료.

A-1의 최초 생성 기록을 찾을 수 없음.
실험 일지에는 생성 이전의 관찰 기록이 존재함.

마지막 기록:
"우리가 발견한 것이 아니라,
처음부터 그곳에 있었던 것이라면?"

파일 끝.
`
  }
];

function print(text) {
  output.textContent += "\n" + text;
  window.scrollTo(0, document.body.scrollHeight);
}

function updateSecurity() {
  document.getElementById("accessLabel").textContent =
    "LEVEL 0" + accessLevel;

  document.getElementById("progress").style.width =
    (accessLevel / 5 * 100) + "%";

  document.getElementById("levelDescription").textContent =
    levelNames[accessLevel - 1] + " 접근 권한이 활성화되었습니다.";

  document.getElementById("levels").innerHTML = "";

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
    document.getElementById("levels").appendChild(item);
  });
}

function showFiles() {
  const available = files.filter(file =>
    file.level <= accessLevel
  );

  const lockedCount = files.length - available.length;

  let result = "[FILE DIRECTORY]\n";

  available.forEach(file => {
    result += "[OPEN] " + file.name + "\n";
  });

  result += "\n접근 가능한 파일: " + available.length;
  result += "\n잠긴 파일: " + lockedCount;

  if (lockedCount > 0) {
    result += "\n일부 파일은 상위 보안 등급이 필요합니다.";
  }

  print(result);
}

function readFile(name) {
  const file = files.find(item =>
    item.name.toLowerCase() === name
  );

  if (!file) {
    print("오류: 파일을 찾을 수 없습니다.");
    return;
  }

  if (accessLevel < file.level) {
    print(
      "⚠ ACCESS DENIED\n" +
      "파일: " + file.name + "\n" +
      "필요 권한: LEVEL 0" + file.level + "\n" +
      "현재 권한: LEVEL 0" + accessLevel + "\n" +
      "상위 보안 등급이 필요합니다."
    );
    return;
  }

  print(file.content);
}

function unlockLevel(password) {
  const pass = password.toLowerCase();

  const credentials = {
    "cell-204": 3,
    "egg-7319": 4,
    "origin-000": 5
  };

  // 기존 A-1 접근 명령은 유지
  if (pass === "a1-0404") {
    if (accessLevel >= 2) {
      print("이미 A-1 기록 접근 권한이 활성화되어 있습니다.");
      return;
    }

    accessLevel = 2;
    updateSecurity();

    print(
      "인증 성공.\n" +
      "ACCESS GRANTED: LEVEL 02\n" +
      "subject_A1.dat 접근 가능.\n" +
      "[비밀 기록] A-1은 처음부터 깨어 있었다."
    );
    return;
  }

  const targetLevel = credentials[pass];

  if (!targetLevel) {
    print("인증 실패: 등록되지 않은 인증 코드입니다.");
    return;
  }

  if (targetLevel <= accessLevel) {
    print("이 보안 등급은 이미 해금되었습니다.");
    return;
  }

  if (targetLevel !== accessLevel + 1) {
    print(
      "ACCESS DENIED\n" +
      "현재 단계의 인증을 먼저 완료해야 합니다."
    );
    return;
  }

  accessLevel = targetLevel;
  updateSecurity();

  print(
    "인증 성공.\n" +
    "ACCESS GRANTED: LEVEL 0" + accessLevel + "\n" +
    "권한: " + levelNames[accessLevel - 1] + "\n" +
    "새로운 파일이 해금되었습니다."
  );
}

function runCommand() {
  const raw = input.value.trim();
  const cmd = raw.toLowerCase();

  if (!cmd) return;

  print("> " + raw);

  if (cmd === "help") {
    print(
`사용 가능한 명령어:
help                  - 명령어 목록
status                - 시스템 상태
security              - 보안 등급 확인
files                 - 파일 목록
access a1-0404        - A-1 기록 인증
unlock [인증 코드]    - 다음 보안 등급 해금
cat [파일명]          - 파일 읽기
clear                 - 화면 초기화

파일 읽기 예시:
cat session_001.log`
    );
  }

  else if (cmd === "status") {
    print(
      "시스템: ONLINE\n" +
      "연구소: EGG\n" +
      "대상 실험체: A-1\n" +
      "기록 상태: 일부 손상\n" +
      "보안 등급: LEVEL 0" + accessLevel
    );
  }

  else if (cmd === "security") {
    print(
      "SECURITY STATUS\n" +
      "현재 등급: LEVEL 0" + accessLevel + "\n" +
      "권한 이름: " + levelNames[accessLevel - 1] + "\n" +
      "최고 등급: LEVEL 05\n" +
      "접근 가능 파일: " +
      files.filter(f => f.level <= accessLevel).length +
      "/" + files.length
    );
  }

  else if (cmd === "files") {
    showFiles();
  }

  else if (cmd === "access a1-0404") {
    unlockLevel("a1-0404");
  }

  else if (cmd.startsWith("unlock ")) {
    const password = raw.slice(7).trim();

    if (!password) {
      print("오류: 인증 코드를 입력하세요.");
    } else {
      unlockLevel(password);
    }
  }

  else if (cmd.startsWith("cat ")) {
    const name = cmd.slice(4).trim();

    if (!name) {
      print("오류: 파일명을 입력하세요.");
    } else {
      readFile(name);
    }
  }

  else if (cmd === "clear") {
    output.textContent =
      "EGG OS v4.0.4\n화면이 초기화되었습니다.";
  }

  else {
    print(
      "오류: 알 수 없는 명령어.\n" +
      "명령이 기록되었습니다."
    );
  }

  input.value = "";
}

document.getElementById("run").addEventListener(
  "click", runCommand
);

input.addEventListener("keydown", event => {
  if (event.key === "Enter") {
    runCommand();
  }
});

updateSecurity();
</script>
</body>
</html>
