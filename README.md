30325 이원태
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>LifeguardBot - 생명존중 챗봇</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f9ff;
      padding: 30px;
    }
    #chat-box {
      width: 100%;
      max-width: 600px;
      margin: auto;
      border: 1px solid #ccc;
      border-radius: 10px;
      background: white;
      padding: 20px;
    }
    .message {
      margin-bottom: 15px;
    }
    .user {
      text-align: right;
      color: #1e90ff;
    }
    .bot {
      text-align: left;
      color: #333;
    }
    textarea {
      width: 100%;
      height: 60px;
      margin-top: 10px;
    }
    button {
      margin-top: 10px;
      padding: 8px 16px;
      background: #1e90ff;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    .timestamp {
      font-size: 0.8em;
      color: #888;
      text-align: center;
    }
  </style>
</head>
<body>

<div id="chat-box">
  <h2>🤖 LifeguardBot - 생명존중 챗봇</h2>
  <div id="messages"></div>

  <textarea id="userInput" placeholder="지금 어떤 기분이신가요?"></textarea>
  <button onclick="sendMessage()">보내기</button>
</div>

<script>
  const riskKeywords = [
    "죽고 싶어", "살기 싫어", "자살", "끝내고 싶어", "의미 없어",
    "괴로워", "힘들어", "없어지고 싶어", "그만 살고 싶어"
  ];

  function isHighRisk(text) {
    return riskKeywords.some(keyword => text.includes(keyword));
  }

  function sendMessage() {
    const userInput = document.getElementById("userInput").value.trim();
    if (userInput === "") return;

    const messages = document.getElementById("messages");
    const time = new Date().toLocaleString();

    // 사용자 메시지 출력
    messages.innerHTML += `<div class="message user"><strong>나:</strong> ${userInput}</div>`;
    messages.innerHTML += `<div class="timestamp">${time}</div>`;

    // 위험도 판단
    let botResponse = "";
    if (isHighRisk(userInput)) {
      botResponse = `
        ❗ 위험 신호가 감지되었습니다.<br>
        당신은 소중한 존재입니다. 지금 힘든 마음은 반드시 지나갈 수 있어요.<br><br>
        📞 <strong>24시간 상담 지원:</strong><br>
        · 정신건강센터 ☎️ 1577-0199<br>
        · 청소년 전화 ☎️ 1388<br>
        · 생명의 전화 ☎️ 1588-9191<br><br>
        함께 이야기하고 싶다면 언제든지 다시 말씀해주세요.
      `;
    } else {
      botResponse = "말씀 잘 들었어요. 더 이야기해볼까요?";
    }

    messages.innerHTML += `<div class="message bot"><strong>봇:</strong> ${botResponse}</div>`;
    messages.innerHTML += `<div class="timestamp">${time}</div>`;
    document.getElementById("userInput").value = "";
    messages.scrollTop = messages.scrollHeight;
  }
</script>

</body>
</html>
