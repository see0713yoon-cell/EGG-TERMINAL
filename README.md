# EGG-TERMINAL

<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>EGG TERMINAL</title>
<style>
body {
  background: #080808;
  color: #ff3030;
  font-family: monospace;
  padding: 20px;
}
h1 { border-bottom: 1px solid red; }
#out { white-space: pre-wrap; color: #ff7777; }
input {
  background: black;
  color: #ff4040;
  border: 1px solid red;
  padding: 10px;
  width: 90%;
}
</style>
</head>
<body>
<h1>EGG RESEARCH LAB</h1>
<p>⚠ RESTRICTED ACCESS</p>
<div id="out">EGG TERMINAL v1.0
시스템 대기 중...
help 를 입력하세요.</div>
<p>> <input id="cmd" placeholder="명령어 입력..."></p>
<script>
const out = document.getElementById('out');
const cmd = document.getElementById('cmd');

cmd.addEventListener('keydown', function(e) {
  if (e.key !== 'Enter') return;
  const c = cmd.value.trim();
  out.textContent += '\n\n> ' + c + '\n';
  if (c === 'help') {
    out.textContent += 'help - 명령어 목록\nstatus - 시스템 상태\nfiles - 파일 목록\naccess A1-0404 - 접근 시도';
  } else if (c === 'status') {
    out.textContent += 'SYSTEM: ONLINE\nSECURITY: RESTRICTED';
  } else if (c === 'files') {
    out.textContent += 'session_001.log\nexperiment_A1.dat\nsubject_cell_07.txt';
  } else if (c === 'access A1-0404') {
    out.textContent += 'ACCESS DENIED\n추가 인증이 필요합니다.';
  } else {
    out.textContent += '알 수 없는 명령어. help 를 입력하세요.';
  }
  cmd.value = '';
});
</script>
</body>
</html>
