
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>GET SCRIPT</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      background: linear-gradient(135deg, #007bff, #ffffff);
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }

    .container {
      background: #ffffff;
      border-radius: 20px;
      padding: 30px 20px;
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
      max-width: 380px;
      width: 100%;
      text-align: center;
    }

    .title {
      font-size: 30px;
      font-weight: bold;
      color: #007bff;
      margin-bottom: 15px;
    }

    .subtitle {
      background: #ffeeba;
      color: #856404;
      padding: 12px;
      border-radius: 10px;
      font-size: 16px;
      font-weight: 500;
      margin-bottom: 25px;
    }

    select, input {
      width: calc(100% - 20px);
      padding: 15px;
      margin-bottom: 20px;
      border: 1px solid #ccc;
      border-radius: 8px;
      font-size: 16px;
    }

    .button {
      background: linear-gradient(90deg, #28a745, #218838);
      color: #fff;
      border: none;
      padding: 15px;
      width: calc(100% - 20px);
      font-size: 18px;
      border-radius: 8px;
      cursor: pointer;
    }

    .footer {
      margin-top: 20px;
      font-size: 15px;
      color: #555;
    }

    /* Thêm style cho nút mới */
    .url-bot-button {
      background-color: #007bff;
      color: white;
      padding: 15px;
      width: calc(100% - 20px);
      font-size: 18px;
      border-radius: 8px;
      cursor: pointer;
      margin-top: 15px;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="title">🚀 𝙂𝙀𝙏 𝙎𝘾𝙍𝙄𝙋𝙏 𝙁𝙍𝙀𝙀 𝘼𝙐𝙏𝙊 🇻🇳</div>
    <div class="subtitle">🎉 Nhập 𝙄𝘿 Telegram và chọn file mã 𝙎𝘾𝙍𝙄𝙋𝙏 bạn muốn nhận.</div>
    <form id="codeForm">
      <input type="text" id="telegramId" placeholder="Nhập 𝙄𝘿 Telegram" required />
      <select id="fileSelection" required>
        <option value="">𝘾𝙝𝙤𝙣 𝙁𝙞𝙡𝙚𝙨</option>
        <option value="file1">𝙎𝘾𝙍𝙄𝙋𝙏 𝘽𝙊𝙏 𝙏𝙓 🌌</option>
        <option value="file2">𝙆𝙃𝙊𝙉𝙃 𝘾𝙊</option>
        <option value="file3">𝙆𝙃𝙊𝙉𝙃 𝘾𝙊</option>
      </select>
      <button type="submit" class="button">🚀 𝙂𝙀𝙏 𝙎𝘾𝙍𝙄𝙋𝙏 </button>
    </form>
    <div class="footer"> 🌌 𝙏𝙊𝙉𝙂 𝙐𝙎𝙀𝙍 𝘿𝘼 𝙉𝙃𝘼𝙉 <span id="userCount">0</span> 𝙎𝘾𝙍𝙄𝙋𝙏</div>

    <!-- Nút URL BOT dẫn đến URL -->
    <button class="url-bot-button" id="urlBotButton">𝘽𝙊𝙏 𝙂𝙀𝙏 𝙎𝘾𝙍𝙄𝙋𝙏 𝙐𝙍𝙇</button>
  </div>

  <script>
    const form = document.getElementById('codeForm');
    const userCountEl = document.getElementById('userCount');
    let userCount = 0;

    const urlBotButton = document.getElementById('urlBotButton');

    form.addEventListener('submit', async (e) => {
      e.preventDefault();
      
      const telegramId = document.getElementById('telegramId').value;
      const fileSelection = document.getElementById('fileSelection').value;

      if (!telegramId || !fileSelection) {
        alert('𝙏𝙃𝙄𝙀𝙐 𝘿𝘼𝙏𝘼 !?');
        return;
      }

      // Tăng số lượng người nhận mã code
      userCount++;
      userCountEl.textContent = userCount;

      // Gửi yêu cầu tới backend (Flask) để xử lý và gửi yêu cầu đến Telegram bot
      try {
        const response = await fetch('http://localhost:5002/send_code', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            telegramId: telegramId,
            fileSelection: fileSelection
          })
        });

        const data = await response.json();

        if (data.success) {
          alert(`𝙑𝙐𝙄 𝙇𝙊𝙉𝙂 𝙆𝙄𝙀𝙈 𝙏𝙍𝘼 𝙏𝙍𝙀𝙉 𝘽𝙊𝙏 ✅`);
        } else {
          alert('𝙑𝙐𝙄 𝙇𝙊𝙉𝙂 𝙎𝙏𝘼𝙍𝙏 𝘽𝙊𝙏 𝙉𝙐𝙏 𝘽𝙀𝙉 𝘿𝙐𝙊𝙄 🚫');
        }
      } catch (error) {
        console.error('Error:', error);
        alert('𝙁𝙄𝙇𝙀𝙎 𝙏𝙍𝙀𝙉 𝙎𝙀𝙍𝙑𝙀𝙍 𝙆𝙃𝙊𝙉𝙂 𝙃𝙊𝘼𝙏 𝘿𝙊𝙉𝙂!');
      }
    });

    // Xử lý sự kiện bấm nút "URL BOT"
    urlBotButton.addEventListener('click', () => {
      // Chuyển hướng đến URL của bot (thay đổi URL này với bot của bạn)
      window.location.href = 'http://t.me/NhancodeADSbot';  // Thay đổi URL với URL bot của bạn
    });
  </script>
</body>
</html>
