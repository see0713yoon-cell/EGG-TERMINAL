<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>EGG TERMINAL</title>
<style>
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
}
#output {
  white-space: pre-wrap;
  line-height: 1.7;
  color: #ff7777;
}
.row {
  display: flex;
  gap: 8px;
}
input {
  flex: 1;
  min-width: 0;
  background: #111;
  color: #ff5555;
  border: 1px solid #833;
  padding: 12px;
  font-family: monospace;
  font-size: 16px;
}
button {
  background: #500;
  color: white;
  border: 1px solid red;
  padding: 10px;
}
</style>
</head>
<body>
<h1>EGG TERMINAL</h1>

<div class="warning">
⚠ RESTRICTED RESEARCH SYSTEM<br>
ACCESS LEVEL: UNKNOWN<br>
SUBJECT: A-1
</div>

<div id="output">EGG OS v4.0.4
연구소 연결 대기 중...
시스템이 시작되었습니다.
명령어를 입력하세요. (help 입력 가능)</div>

<br>
<div class="row">
<input id="cmd" placeholder="명령어 입력..." autocomplete="off">
<button id="run">실행</button>
</div>

<script>
const output = document.getElementById("output");
const input = document.getElementById("cmd");

function runCommand() {
  const cmd = input.value.trim().toLowerCase();
  if (!cmd) return;

  output.textContent += "\n\n> " + cmd + "\n";

  const commands = {
    "help": "사용 가능한 명령어: help, status, files, access A1-0404, cat session_001.log, clear",
    "status": "시스템: ONLINE\n연구소: EGG\n대상 실험체: A-1\n기록 상태: 일부 손상",
    "files": "검색된 파일:\nsession_001.log\nsubject_A1.dat\nincident_0404.log",
    "access a1-0404": "접근 코드 확인 중...\n인증 성공.\n기록 일부가 해금되었습니다.\n[비밀 기록] A-1은 처음부터 깨어 있었다.",
    "cat session_001.log": "[SESSION 001]\n실험체 A-1 반응 확인.\n연구원 기록: 관찰 대상이 모니터를 바라보고 있었다.\n주의: 해당 문장은 이후 기록에서 삭제됨."
  };

  if (cmd === "clear") {
    output.textContent = "EGG OS v4.0.4\n화면이 초기화되었습니다.";
  } else {
    output.textContent += commands[cmd] || "오류: 알 수 없는 명령어.\n명령이 기록되었습니다.";
  }

  input.value = "";
  window.scrollTo(0, document.body.scrollHeight);
}

document.getElementById("run").addEventListener("click", runCommand);
input.addEventListener("keydown", event => {
  if (event.key === "Enter") runCommand();
});
</script>
</body>
</html>
