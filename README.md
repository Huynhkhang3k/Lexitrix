
<!DOCTYPE html>
<html lang="vi">
  <head>
    <meta charset="UTF-8" />
    <title> Lexitrix</title>
    <link rel="icon" type="image/jpeg" href="https://i.postimg.cc/Y0JRSkhL/bd20fb32-ea8b-4a3a-890a-fc860146e2d4.jpg" />

    <style>
      /* ======== RESET CƠ BẢN ======== */
      * {
        box-sizing: border-box;
        margin: 0;
        padding: 0;
      }
      html,
      body {
        height: 100%;
        margin: 0;
        padding: 0;
      }

      /* ======== NỀN THEO MỨC ĐỘ ======== */
      body.easy {
        background-color: #ffffff;
      }
      body.normal {
        background-color: #ffffff;
      }
      body.hard {
        background-color: #ffffff;
      }
      body.veryhard {
        background-color: #ffffff;
      }
      body.extreme {
        background-color: #ffffff;
      }
      body {
        font-family: "Segoe UI", sans-serif;
        line-height: 1.4;
        transition: background-color 0.4s;
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 20px;
        position: relative;
        overflow-x: hidden;
      }

      /* ======== HEADER BAR ======== */
      .header-bar {
        width: 100%;
        max-width: 1200px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 12px;
      }
      .header-bar-left {
        display: flex;
        align-items: center;
      }
      .header-bar-left label {
        margin-right: 8px;
        font-weight: bold;
      }
      .header-bar-left select {
        padding: 6px;
        font-size: 16px;
      }
      .btn.settings,
      .btn.export {
        padding: 10px 20px;
        border: 2px solid #555;
        border-radius: 8px;
        color: white;
        font-size: 16px;
        font-weight: bold;
        cursor: pointer;
        background-color: #555;
        box-shadow: 0 3px 6px rgba(0, 0, 0, 0.2);
        transition: background-color 0.2s, transform 0.1s;
        margin-left: 6px;
      }
      .btn.settings:hover,
      .btn.export:hover {
        background-color: #333;
      }
      .btn.settings:active,
      .btn.export:active {
        transform: scale(0.98);
      }

      /* ======== NÚT MỨC ĐỘ ======== */
      .difficulty-buttons {
        width: 100%;
        max-width: 1200px;
        text-align: center;
        margin-bottom: 20px;
      }
      .difficulty-buttons .btn {
        padding: 10px 20px;
        margin: 0 6px;
        border: 2px solid #555;
        border-radius: 8px;
        color: white;
        font-size: 16px;
        font-weight: bold;
        cursor: pointer;
        box-shadow: 0 3px 6px rgba(0, 0, 0, 0.2);
        transition: transform 0.1s;
      }
      .difficulty-buttons .btn:active {
        transform: scale(0.98);
      }
      .btn.easy {
        background-color: #0d9b37;
      }
      .btn.normal {
        background-color: #3d71d9;
      }
      .btn.hard {
        background-color: #da6033;
      }
      .btn.veryhard {
        background-color: #e04040;
      }
      .btn.extreme {
        background-color: #91098f;
      }

      /* ======== HIỂN THỊ QUIZ ======== */
      #timer {
        font-size: 20px;
        margin: 10px 0;
        font-weight: bold;
      }
      #quiz {
        width: 100%;
        max-width: 800px;
        background: #ffffff;
        padding: 20px;
        border-radius: 12px;
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
        text-align: left;
        margin-bottom: 40px;
      }
      .passage {
        font-style: italic;
        background: #343434;
        padding: 12px;
        border-radius: 8px;
        margin-bottom: 20px;
      }
      .question-container {
        margin-bottom: 24px;
      }
      .question-container p {
        font-size: 18px;
        margin-bottom: 8px;
      }
      .options label {
        display: block;
        margin: 6px 0;
        cursor: pointer;
      }
      .feedback {
        margin-top: 8px;
        font-weight: bold;
      }
      .feedback.correct {
        color: green;
      }
      .feedback.wrong {
        color: red;
      }

      /* ======== OVERLAY & PANEL ======== */
      #overlay {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.5);
        display: none;
        z-index: 100;
      }
      #settings-panel {
        position: fixed;
        top: 5%;
        left: 50%;
        transform: translateX(-50%);
        width: 90%;
        max-width: 900px;
        background: #ffffff;
        border-radius: 12px;
        box-shadow: 0 5px 15px rgba(0, 0, 0, 0.4);
        padding: 20px 30px;
        display: none;
        z-index: 200;
        max-height: 90vh;
        overflow-y: auto;
      }
      #settings-panel h2 {
        text-align: center;
        margin-bottom: 16px;
      }
      #settings-panel .close-btn {
        position: absolute;
        top: 12px;
        right: 16px;
        font-size: 22px;
        font-weight: bold;
        color: #888;
        cursor: pointer;
      }
      #settings-panel .close-btn:hover {
        color: #444;
      }
      #settings-panel .section {
        margin-bottom: 24px;
      }
      #settings-panel label {
        display: block;
        margin-bottom: 6px;
        font-weight: bold;
      }
      #settings-panel select,
      #settings-panel input[type="number"],
      #settings-panel textarea,
      #settings-panel input[type="text"] {
        width: 100%;
        padding: 8px;
        font-size: 14px;
        border: 1px solid #ccc;
        border-radius: 4px;
      }
      #settings-panel textarea {
        resize: vertical;
        height: 80px;
        font-family: monospace;
      }
      #settings-panel input[type="text"] {
        margin-bottom: 8px;
      }
      #settings-panel .actions {
        text-align: right;
      }
      #settings-panel .actions button {
        padding: 8px 16px;
        margin-left: 10px;
        font-size: 14px;
        border: none;
        border-radius: 6px;
        cursor: pointer;
      }
      #settings-panel .actions .save-btn {
        background-color: #ff7801;
        color: white;
      }
      #settings-panel .actions .cancel-btn {
        background-color: #888;
        color: white;
      }

      /* ======== QUẢN LÝ CÂU ======== */
      .question-editor {
        border: 1px solid #ccc;
        padding: 12px;
        border-radius: 8px;
        margin-bottom: 12px;
        background: #fafafa;
      }
      .question-editor h3 {
        font-size: 16px;
        margin-bottom: 10px;
      }
      .question-editor label {
        font-size: 14px;
        margin-top: 6px;
      }
      .question-editor input,
      .question-editor select {
        font-size: 14px;
        margin-top: 4px;
      }
      .nav-buttons {
        display: flex;
        justify-content: space-between;
        margin-top: 12px;
      }
      .nav-buttons button {
        padding: 6px 12px;
        font-size: 14px;
        border: 1px solid #555;
        border-radius: 6px;
        cursor: pointer;
        background: #fff;
      }
      .nav-buttons button:disabled {
        opacity: 0.5;
        cursor: not-allowed;
      }

      /* ======== CANVAS PHÁO HOA ======== */
      #fireworksCanvas {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        pointer-events: none;
        z-index: 300;
        display: none;
      }

      /* ======== BẢNG XẾP HẠNG ======== */
      #leaderboard-button {
        position: fixed;
        right: 20px;
        top: 50%;
        transform: translateY(-50%);
        padding: 10px 14px;
        background: #f4774a;
        color: white;
        font-weight: bold;
        border: none;
        border-radius: 8px;
        box-shadow: 0 3px 6px rgba(0, 0, 0, 0.2);
        cursor: pointer;
        z-index: 250;
      }
      #leaderboard-button:hover {
        background: #e0633a;
      }
      #leaderboard-panel {
        position: fixed;
        right: 0;
        top: 20%;
        width: 320px;
        max-height: 60%;
        background: #ffffff;
        border-radius: 8px 0 0 8px;
        box-shadow: -2px 2px 10px rgba(0, 0, 0, 0.2);
        overflow-y: auto;
        z-index: 260;
        display: none;
        padding: 16px;
      }
      #leaderboard-panel h3 {
        text-align: center;
        margin-bottom: 12px;
      }
      #leaderboard-panel .close-leaderboard {
        position: absolute;
        top: 8px;
        right: 12px;
        font-size: 18px;
        font-weight: bold;
        cursor: pointer;
        color: #888;
      }
      #leaderboard-panel .close-leaderboard:hover {
        color: #3e3e3e;
      }
      #leaderboard-panel table {
        width: 100%;
        border-collapse: collapse;
        margin-top: 8px;
      }
      #leaderboard-panel th,
      #leaderboard-panel td {
        border: 1px solid #ccc;
        padding: 6px;
        text-align: center;
        font-size: 14px;
      }
      #leaderboard-panel th {
        background: #f7f7f7;
      }

      /* ======== OVERLAY CHỌN VAI TRÒ ======== */
      #roleOverlay {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.7);
        display: flex;
        justify-content: center;
        align-items: center;
        z-index: 500;
      }
      #roleBox {
        background: #ffffff;
        padding: 30px 40px;
        border-radius: 12px;
        text-align: center;
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
      }
      #roleBox h2 {
        margin-bottom: 20px;
      }
      .role-button {
        padding: 12px 24px;
        margin: 0 12px;
        font-size: 16px;
        font-weight: bold;
        border: none;
        border-radius: 8px;
        cursor: pointer;
        transition: transform 0.1s;
      }
      .role-button.teacher {
        background-color: #1e90ff;
        color: white;
      }
      .role-button.student {
        background-color: #32cd32;
        color: white;
      }
      .role-button:hover {
        transform: scale(1.05);
      }
    </style>
  </head>

  <body class="easy">
    <!-- ======== OVERLAY CHỌN VAI TRÒ ======== -->
    <div id="roleOverlay">
      <div id="roleBox">
        <h2>Chọn vai trò của bạn</h2>
        <button class="role-button teacher" onclick="selectRole('teacher')">
          Giáo viên
        </button>
        <button class="role-button student" onclick="selectRole('student')">
          Học sinh
        </button>
      </div>
    </div>

    <!-- ======== HEADER BAR ======== -->
    <div class="header-bar">
      <div class="header-bar-left">
        <label for="classSelect">Chọn Lớp:</label>
        <select id="classSelect">
          <option value="6">Lớp 6</option>
          <option value="7">Lớp 7</option>
          <option value="8">Lớp 8</option>
          <option value="9" selected>Lớp 9</option>
        </select>
      </div>
      <div>
        <button
          id="export-btn"
          class="btn export"
          title="Tải file HTML chứa dữ liệu & mã nguồn hiện tại"
        >
          Xuất File
        </button>
        <button id="open-settings" class="btn settings">Cài đặt</button>
      </div>
    </div>

    <!-- ======== NÚT MỨC ĐỘ ======== -->
    <div class="difficulty-buttons">
      <button class="btn easy" onclick="startQuiz('easy')">Dễ</button>
      <button class="btn normal" onclick="startQuiz('normal')">
        Bình Thường
      </button>
      <button class="btn hard" onclick="startQuiz('hard')">Khó</button>
      <button class="btn veryhard" onclick="startQuiz('veryhard')">
        Rất Khó
      </button>
      <button class="btn extreme" onclick="startQuiz('extreme')">
        Cực Khó
      </button>
    </div>

    <!-- ======== HIỂN THỊ TIMER & QUIZ ======== -->
    <div id="timer"></div>
    <div id=" Lexitrix "></div>

    <!-- ======== CANVAS PHÁO HOA ======== -->
    <canvas id="fireworksCanvas"></canvas>

    <!-- ======== BẢNG XẾP HẠNG BUTTON ======== -->
    <button id="leaderboard-button">Bảng xếp hạng</button>
    <div id="leaderboard-panel">
      <span class="close-leaderboard" onclick="toggleLeaderboard()">✕</span>
      <h3>Bảng xếp hạng</h3>
      <table id="leaderboard-table">
        <thead>
          <tr>
            <th>Hạng</th>
            <th>Điểm (%)</th>
            <th>Thời gian</th>
            <th>Ngày</th>
          </tr>
        </thead>
        <tbody>
          <!-- Dữ liệu sẽ được đổ vào đây -->
        </tbody>
      </table>
    </div>

    <!-- ======== OVERLAY ======== -->
    <div id="overlay"></div>

    <!-- ======== PANEL CÀI ĐẶT ======== -->
    <div id="settings-panel">
      <span class="close-btn" onclick="closeSettings()">✕</span>
      <h2>CÀI ĐẶT CÂU HỎI CHO TỪNG LỚP & TỪNG MỨC ĐỘ</h2>
      <p>
        Chọn <strong>Lớp (6–9)</strong> và
        <strong>Mức độ (Dễ/Bình Thường/Khó/Rất Khó/Cực Khó)</strong>, rồi
        thêm/sửa câu Ngữ pháp, đoạn văn Reading & câu Reading. Dễ sử dụng, không
        cần biết code.
      </p>

      <!-- 1. Chọn Lớp -->
      <div class="section">
        <label for="settings-class-select">Chọn Lớp cần sửa:</label>
        <select id="settings-class-select">
          <option value="6">Lớp 6</option>
          <option value="7">Lớp 7</option>
          <option value="8">Lớp 8</option>
          <option value="9" selected>Lớp 9</option>
        </select>
      </div>

      <!-- 2. Chọn Mức Độ -->
      <div class="section">
        <label for="settings-mood-select">Chọn Mức độ cần sửa:</label>
        <select id="settings-mood-select">
          <option value="easy">Dễ</option>
          <option value="normal">Bình Thường</option>
          <option value="hard">Khó</option>
          <option value="veryhard">Rất Khó</option>
          <option value="extreme">Cực Khó</option>
        </select>
      </div>

      <!-- 3. Số câu tối đa -->
      <div class="section">
        <label for="numQuestions">
          Số câu hỏi tối đa khi chạy quiz để tránh lỗi:
          <input type="number" id="numQuestions" min="1" value="35" />
          <small style="color: #666">(mặc định 35)</small>
        </label>
      </div>

      <!-- 4. Quản lý câu Ngữ pháp -->
      <div class="section">
        <h3>1.Quản lý câu hỏi/trả lời đơn giản</h3>
        <div id="grammar-editor-container"></div>
        <button
          onclick="addGrammarQuestion()"
          style="margin-top: 8px; padding: 6px 12px"
        >
          ➕ Thêm câu mới
        </button>
      </div>

      <!-- 5. Đoạn Reading -->
      <div class="section">
        <label for="passage-input">
          2.1 Đoạn văn trích dẫn (Tiếng anh/Việt nếu có ):<br />
          <textarea
            id="passage-input"
            placeholder="Paste đoạn văn tại đây"
          ></textarea>
        </label>
      </div>

      <!-- 6. Quản lý câu Reading -->
      <div class="section">
        <h3>2.2 Quản lý câu hỏi /trả lời phần Đoạn văn trích dẫn</h3>
        <div id="reading-editor-container"></div>
        <button
          onclick="addReadingQuestion()"
          style="margin-top: 8px; padding: 6px 12px"
        >
          ➕ Thêm câu mới
        </button>
      </div>

      <!-- Nút Lưu / Hủy -->
      <div class="actions">
        <button class="save-btn" onclick="saveSettings()">Lưu</button>
        <button class="cancel-btn" onclick="closeSettings()">Hủy</button>
      </div>
    </div>

    <!-- ======== PHẦN AUDIO CẢNH BÁO (20 giây) ======== -->
    <audio
      id="warningSound"
      src="https://media.vocaroo.com/mp3/16mVZLZ3up3x"
    ></audio>
    <!-- ======== PHẦN AUDIO CHÚC MỪNG (hoàn thành sớm) ======== -->
    <audio
      id="celebrationSound"
      src="https://tiengdong.com/tieng-phao-no"
    ></audio>

    <script>
      /****************************************************************
       * XỬ LÝ CHỌN VAI TRÒ
       ****************************************************************/
      let userRole = null; // 'teacher' hoặc 'student'
      function selectRole(role) {
        userRole = role;
        // Ẩn overlay chọn vai trò
        document.getElementById("roleOverlay").style.display = "none";
        // Nếu là học sinh, ẩn nút Cài đặt và Xuất File
        if (userRole === "student") {
          document.getElementById("open-settings").style.display = "none";
          document.getElementById("export-btn").style.display = "none";
        }
      }

      /****************************************************************
       * Bước 1: Khởi tạo defaultData & clone thành questionsByClassAndMood
       ****************************************************************/
      const defaultData = {
        6: {
          easy: { grammar: [], reading: { passage: "", qs: [] } },
          normal: { grammar: [], reading: { passage: "", qs: [] } },
          hard: { grammar: [], reading: { passage: "", qs: [] } },
          veryhard: { grammar: [], reading: { passage: "", qs: [] } },
          extreme: { grammar: [], reading: { passage: "", qs: [] } },
        },
        7: {
          easy: { grammar: [], reading: { passage: "", qs: [] } },
          normal: { grammar: [], reading: { passage: "", qs: [] } },
          hard: { grammar: [], reading: { passage: "", qs: [] } },
          veryhard: { grammar: [], reading: { passage: "", qs: [] } },
          extreme: { grammar: [], reading: { passage: "", qs: [] } },
        },
        8: {
          easy: { grammar: [], reading: { passage: "", qs: [] } },
          normal: { grammar: [], reading: { passage: "", qs: [] } },
          hard: { grammar: [], reading: { passage: "", qs: [] } },
          veryhard: { grammar: [], reading: { passage: "", qs: [] } },
          extreme: { grammar: [], reading: { passage: "", qs: [] } },
        },
        9: {
          easy: {
            grammar: [
              {
                q: "If it rains tomorrow, we will...",
                opts: {
                  a: "stay at home",
                  b: "have stayed",
                  c: "stayed",
                  d: "will stayed",
                },
                a: "a",
              },
              {
                q: "If you study hard, you... the exam.",
                opts: {
                  a: "pass",
                  b: "will passed",
                  c: "are passing",
                  d: "will pass",
                },
                a: "d",
              },
              {
                q: "If they don't hurry, they... the bus.",
                opts: {
                  a: "miss",
                  b: "will miss",
                  c: "missed",
                  d: "will missed",
                },
                a: "b",
              },
              {
                q: "If she arrives early, she... the meeting.",
                opts: {
                  a: "will join",
                  b: "joins",
                  c: "would join",
                  d: "joined",
                },
                a: "a",
              },
              {
                q: "If I see him, I... him the news.",
                opts: { a: "tell", b: "will tell", c: "told", d: "will told" },
                a: "b",
              },
            ],
            reading: {
              passage:
                "Our planet needs our help. Pollution harms air and water. Many people throw trash everywhere and cut trees without planting new ones. To protect our world, we should throw trash into bins, use less plastic, and plant at least one tree each year. Each small action makes a big difference.",
              qs: [
                {
                  q: "What does pollution harm?",
                  opts: {
                    a: "air and water",
                    b: "trees only",
                    c: "animals only",
                    d: "soil only",
                  },
                  a: "a",
                },
                {
                  q: "What should we do with trash?",
                  opts: {
                    a: "Throw it anywhere",
                    b: "Throw into bins",
                    c: "Burn it",
                    d: "Bury it",
                  },
                  a: "b",
                },
                {
                  q: "How often should we plant a tree?",
                  opts: {
                    a: "Every month",
                    b: "At least one per year",
                    c: "Once in a lifetime",
                    d: "Every day",
                  },
                  a: "b",
                },
                {
                  q: "Why is each small action important?",
                  opts: {
                    a: "It doesn’t matter",
                    b: "It makes a big difference",
                    c: "It’s too small",
                    d: "It harms the environment",
                  },
                  a: "b",
                },
                {
                  q: "One way to use less plastic is to…?",
                  opts: {
                    a: "Use reusable bags",
                    b: "Buy more plastic",
                    c: "Throw plastic in bins",
                    d: "Burn plastic",
                  },
                  a: "a",
                },
              ],
            },
          },
          normal: { grammar: [], reading: { passage: "", qs: [] } },
          hard: { grammar: [], reading: { passage: "", qs: [] } },
          veryhard: { grammar: [], reading: { passage: "", qs: [] } },
          extreme: { grammar: [], reading: { passage: "", qs: [] } },
        },
      };

      // **PHẦN NÀY BẮT BUỘC PHẢI GIỐNG HỆ THỐNG**
      // để hàm export sau này tìm đúng và replace chính xác.
      let questionsByClassAndMood = JSON.parse(JSON.stringify(defaultData));

      /****************************************************************
       * Bước 2: Các phần tử DOM & khai báo biến dùng chung
       ****************************************************************/
      const overlay = document.getElementById("overlay");
      const panel = document.getElementById("settings-panel");
      const settingsClassSelect = document.getElementById(
        "settings-class-select"
      );
      const settingsMoodSelect = document.getElementById(
        "settings-mood-select"
      );
      const numQuestionsInput = document.getElementById("numQuestions");
      const grammarContainer = document.getElementById(
        "grammar-editor-container"
      );
      const passageInput = document.getElementById("passage-input");
      const readingContainer = document.getElementById(
        "reading-editor-container"
      );

      // Element cho pháo hoa
      const fireworksCanvas = document.getElementById("fireworksCanvas");
      const ctx = fireworksCanvas.getContext("2d");
      let fireworksAnimationFrame;
      let particles = [];

      // Audio elements
      const warningSound = document.getElementById("warningSound");
      const celebrationSound = document.getElementById("celebrationSound");

      /****************************************************************
       * Hàm khởi tạo kích thước Canvas và vẽ pháo hoa
       ****************************************************************/
      function resizeCanvas() {
        fireworksCanvas.width = window.innerWidth;
        fireworksCanvas.height = window.innerHeight;
      }
      window.addEventListener("resize", resizeCanvas);
      resizeCanvas();

      // Đối tượng hạt pháo hoa
      class Particle {
        constructor(x, y, hue) {
          this.x = x;
          this.y = y;
          this.angle = Math.random() * Math.PI * 2;
          this.speed = Math.random() * 6 + 2; // tăng tốc độ cho đẹp hơn
          this.friction = 0.92; // giảm độ ma sát để giữ hạt lâu hơn
          this.gravity = 0.8;
          this.hue = hue;
          this.brightness = Math.random() * 20 + 50;
          this.alpha = 1;
          this.decay = Math.random() * 0.02 + 0.015; // tăng decay cho chuyển dần mờ
          this.size = Math.random() * 3 + 2; // cho hạt có kích cỡ khác nhau
        }
        update() {
          this.speed *= this.friction;
          this.x += Math.cos(this.angle) * this.speed;
          this.y += Math.sin(this.angle) * this.speed + this.gravity;
          this.alpha -= this.decay;
        }
        draw() {
          ctx.save();
          ctx.globalCompositeOperation = "lighter";
          ctx.fillStyle = `hsla(${this.hue}, 100%, ${this.brightness}%, ${this.alpha})`;
          ctx.beginPath();
          ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
          ctx.fill();
          ctx.restore();
        }
      }

      // Khởi tạo một vụ nổ pháo hoa tại (x,y)
      function createFirework(x, y) {
        const hue = Math.random() * 360;
        const count = 150; // tăng số hạt cho rực rỡ hơn
        for (let i = 0; i < count; i++) {
          particles.push(new Particle(x, y, hue));
        }
      }

      // Vòng lặp vẽ pháo hoa
      function animateFireworks() {
        // Sử dụng rgba với alpha nhỏ để tạo vệt sáng mờ
        ctx.fillStyle = "rgba(0, 0, 0, 0.1)";
        ctx.fillRect(0, 0, fireworksCanvas.width, fireworksCanvas.height);

        for (let i = particles.length - 1; i >= 0; i--) {
          const p = particles[i];
          p.update();
          if (p.alpha <= p.decay) {
            particles.splice(i, 1);
          } else {
            p.draw();
          }
        }

        // Tạo liên tục nhiều vụ nổ ngẫu nhiên (nhưng ít hơn so với ban đầu)
        if (Math.random() < 0.08) {
          createFirework(
            Math.random() * fireworksCanvas.width,
            (Math.random() * fireworksCanvas.height) / 2
          );
        }

        if (particles.length > 0) {
          fireworksAnimationFrame = requestAnimationFrame(animateFireworks);
        } else {
          cancelAnimationFrame(fireworksAnimationFrame);
          fireworksCanvas.style.display = "none";
        }
      }

      // Bật hiệu ứng pháo hoa trong 5 giây
      function startFireworks() {
        fireworksCanvas.style.display = "block";
        particles = [];
        resizeCanvas();
        // Tạo vụ nổ ban đầu ở trung tâm
        createFirework(fireworksCanvas.width / 2, fireworksCanvas.height / 2);
        animateFireworks();
        // Tắt tạo thêm pháo hoa sau 5 giây
        setTimeout(() => {
          particles = [];
        }, 5000);
      }

      /****************************************************************
       * Bảng xếp hạng (Leaderboard) lưu trữ và hiển thị
       ****************************************************************/
      // Lấy leaderboard từ localStorage, trả về mảng
      function getLeaderboard() {
        const data = localStorage.getItem("quizLeaderboard");
        return data ? JSON.parse(data) : [];
      }
      // Lưu leaderboard vào localStorage
      function saveLeaderboard(arr) {
        localStorage.setItem("quizLeaderboard", JSON.stringify(arr));
      }

      // Thêm kết quả mới vào leaderboard
      function addToLeaderboard(entry) {
        const lb = getLeaderboard();
        lb.push(entry);
        saveLeaderboard(lb);
      }

      // Hiển thị bảng xếp hạng cho lớp và mức độ hiện tại
      function renderLeaderboard() {
        const cls = document.getElementById("classSelect").value;
        const mood = document.querySelector("body").className;
        const lb = getLeaderboard()
          .filter((e) => e.class === cls && e.difficulty === mood)
          .sort((a, b) => {
            if (b.scorePct !== a.scorePct) return b.scorePct - a.scorePct;
            return a.timeUsed - b.timeUsed;
          })
          .slice(0, 10);

        const tbody = document.querySelector("#leaderboard-table tbody");
        tbody.innerHTML = "";
        lb.forEach((e, idx) => {
          const tr = document.createElement("tr");
          const tdRank = document.createElement("td");
          tdRank.innerText = idx + 1;
          const tdScore = document.createElement("td");
          tdScore.innerText = e.scorePct;
          const tdTime = document.createElement("td");
          const m = Math.floor(e.timeUsed / 60);
          const s = e.timeUsed % 60;
          tdTime.innerText = `${m < 10 ? "0" + m : m}:${s < 10 ? "0" + s : s}`;
          const tdDate = document.createElement("td");
          tdDate.innerText = new Date(e.timestamp).toLocaleDateString("vi-VN");
          tr.appendChild(tdRank);
          tr.appendChild(tdScore);
          tr.appendChild(tdTime);
          tr.appendChild(tdDate);
          tbody.appendChild(tr);
        });
      }

      // Bật/tắt hiển thị panel leaderboard
      function toggleLeaderboard() {
        const panel = document.getElementById("leaderboard-panel");
        if (panel.style.display === "block") {
          panel.style.display = "none";
        } else {
          renderLeaderboard();
          panel.style.display = "block";
        }
      }

      // Gắn sự kiện cho nút
      document
        .getElementById("leaderboard-button")
        .addEventListener("click", toggleLeaderboard);

      /****************************************************************
       * Bước 3: Mở/Đóng panel "Cài đặt"
       ****************************************************************/
      document.getElementById("open-settings").onclick = function () {
        loadSettingsIntoPanel();
        overlay.style.display = "block";
        panel.style.display = "block";
      };
      function closeSettings() {
        overlay.style.display = "none";
        panel.style.display = "none";
      }
      document.querySelector("#settings-panel .close-btn").onclick =
        closeSettings;
      overlay.onclick = closeSettings;
      settingsClassSelect.onchange = loadSettingsIntoPanel;
      settingsMoodSelect.onchange = loadSettingsIntoPanel;

      /****************************************************************
       * Bước 4: Tạo form cho mỗi câu (grammar hoặc reading)
       ****************************************************************/
      function createQuestionForm(type, index) {
        const cls = settingsClassSelect.value;
        const mood = settingsMoodSelect.value;
        const data =
          type === "grammar"
            ? questionsByClassAndMood[cls][mood].grammar
            : questionsByClassAndMood[cls][mood].reading.qs;

        const container = document.createElement("div");
        container.className = "question-editor";
        container.setAttribute("data-type", type);
        container.setAttribute("data-index", index);

        // Tiêu đề nhỏ: "Câu thứ X / Tổng Y"
        const header = document.createElement("h3");
        header.innerText = `${
          type === "grammar" ? "Ngữ pháp" : "Reading"
        }: Câu ${index + 1} / ${data.length}`;
        container.appendChild(header);

        // Ô “Câu hỏi:”
        const qLabel = document.createElement("label");
        qLabel.innerText = "Câu hỏi:";
        const qInput = document.createElement("input");
        qInput.type = "text";
        qInput.value = data[index]?.q || "";
        qInput.style.width = "100%";
        qInput.oninput = () => {
          data[index].q = qInput.value;
        };
        container.appendChild(qLabel);
        container.appendChild(qInput);

        // Các input A, B, C, D
        ["a", "b", "c", "d"].forEach((letter) => {
          const optLabel = document.createElement("label");
          optLabel.innerText = `Đáp án ${letter.toUpperCase()}:`;
          const optInput = document.createElement("input");
          optInput.type = "text";
          optInput.value = data[index]?.opts[letter] || "";
          optInput.style.width = "100%";
          optInput.oninput = () => {
            data[index].opts[letter] = optInput.value;
          };
          container.appendChild(optLabel);
          container.appendChild(optInput);
        });

        // Dropdown chọn đáp án đúng
        const correctLabel = document.createElement("label");
        correctLabel.innerText = "Đáp án đúng:";
        const correctSelect = document.createElement("select");
        ["a", "b", "c", "d"].forEach((letter) => {
          const opt = document.createElement("option");
          opt.value = letter;
          opt.innerText = letter.toUpperCase();
          correctSelect.appendChild(opt);
        });
        correctSelect.value = data[index]?.a || "a";
        correctSelect.onchange = () => {
          data[index].a = correctSelect.value;
        };
        container.appendChild(correctLabel);
        container.appendChild(correctSelect);

        // Nút Xóa câu này
        const deleteBtn = document.createElement("button");
        deleteBtn.style.marginTop = "8px";
        deleteBtn.style.padding = "6px 10px";
        deleteBtn.style.backgroundColor = "#e74c3c";
        deleteBtn.style.color = "white";
        deleteBtn.style.border = "none";
        deleteBtn.style.borderRadius = "4px";
        deleteBtn.style.cursor = "pointer";
        deleteBtn.innerText = "🗑️ Xóa câu này";
        deleteBtn.onclick = () => {
          data.splice(index, 1);
          loadSettingsIntoPanel();
        };
        container.appendChild(deleteBtn);

        // Nút Điều hướng: ← Trước / Sau →
        const navDiv = document.createElement("div");
        navDiv.className = "nav-buttons";
        const prevBtn = document.createElement("button");
        prevBtn.innerText = "← Trước";
        prevBtn.disabled = index === 0;
        prevBtn.onclick = () => {
          loadSettingsIntoPanel();
          scrollToQuestion(type, index - 1);
        };
        const nextBtn = document.createElement("button");
        nextBtn.innerText = "Sau →";
        nextBtn.disabled = index === data.length - 1;
        nextBtn.onclick = () => {
          loadSettingsIntoPanel();
          scrollToQuestion(type, index + 1);
        };
        navDiv.appendChild(prevBtn);
        navDiv.appendChild(nextBtn);
        container.appendChild(navDiv);

        return container;
      }

      function scrollToQuestion(type, idx) {
        const selector = `[data-type="${type}"][data-index="${idx}"]`;
        const elem = document.querySelector(selector);
        if (elem) {
          elem.scrollIntoView({ behavior: "smooth", block: "center" });
        }
      }

      function addGrammarQuestion() {
        const cls = settingsClassSelect.value;
        const mood = settingsMoodSelect.value;
        const data = questionsByClassAndMood[cls][mood].grammar;
        data.push({
          q: "",
          opts: { a: "", b: "", c: "", d: "" },
          a: "a",
        });
        loadSettingsIntoPanel();
        setTimeout(() => scrollToQuestion("grammar", data.length - 1), 100);
      }

      function addReadingQuestion() {
        const cls = settingsClassSelect.value;
        const mood = settingsMoodSelect.value;
        const data = questionsByClassAndMood[cls][mood].reading.qs;
        data.push({
          q: "",
          opts: { a: "", b: "", c: "", d: "" },
          a: "a",
        });
        loadSettingsIntoPanel();
        setTimeout(() => scrollToQuestion("reading", data.length - 1), 100);
      }

      function loadSettingsIntoPanel() {
        const cls = settingsClassSelect.value;
        const mood = settingsMoodSelect.value;
        const data = questionsByClassAndMood[cls][mood];

        // Load Grammar
        grammarContainer.innerHTML = "";
        if (data.grammar.length === 0) {
          const p = document.createElement("p");
          p.style.color = "#666";
          p.innerText = "Chưa có câu Ngữ pháp. Hãy bấm 'Thêm câu mới' để tạo.";
          grammarContainer.appendChild(p);
        } else {
          data.grammar.forEach((_, idx) => {
            const form = createQuestionForm("grammar", idx);
            grammarContainer.appendChild(form);
          });
        }

        // Load Passage
        passageInput.value = data.reading.passage;

        // Load Reading Questions
        readingContainer.innerHTML = "";
        if (data.reading.qs.length === 0) {
          const p2 = document.createElement("p");
          p2.style.color = "#666";
          p2.innerText =
            "Chưa có câu Reading. Nếu có, bấm 'Thêm câu mới' để tạo.";
          readingContainer.appendChild(p2);
        } else {
          data.reading.qs.forEach((_, idx) => {
            const form2 = createQuestionForm("reading", idx);
            readingContainer.appendChild(form2);
          });
        }
      }

      function saveSettings() {
        const cls = settingsClassSelect.value;
        const mood = settingsMoodSelect.value;
        const data = questionsByClassAndMood[cls][mood];

        // Lưu Passage
        data.reading.passage = passageInput.value.trim();

        // Kiểm tra grammar
        for (let i = 0; i < data.grammar.length; i++) {
          const itm = data.grammar[i];
          if (
            itm.q.trim() === "" ||
            itm.opts.a.trim() === "" ||
            itm.opts.b.trim() === "" ||
            itm.opts.c.trim() === "" ||
            itm.opts.d.trim() === ""
          ) {
            alert(`Chưa điền đủ thông tin cho Câu Ngữ pháp thứ ${i + 1}.`);
            return;
          }
          if (!["a", "b", "c", "d"].includes(itm.a)) {
            alert(`Đáp án đúng của Câu Ngữ pháp thứ ${i + 1} phải là a/b/c/d.`);
            return;
          }
        }

        // Kiểm tra reading
        for (let i = 0; i < data.reading.qs.length; i++) {
          const itm = data.reading.qs[i];
          if (
            itm.q.trim() === "" ||
            itm.opts.a.trim() === "" ||
            itm.opts.b.trim() === "" ||
            itm.opts.c.trim() === "" ||
            itm.opts.d.trim() === ""
          ) {
            alert(`Chưa điền đủ thông tin cho Câu Reading thứ ${i + 1}.`);
            return;
          }
          if (!["a", "b", "c", "d"].includes(itm.a)) {
            alert(
              `Đáp án đúng của Câu đoạn trích thứ ${i + 1} phải là a/b/c/d.`
            );
            return;
          }
        }

        alert(`Đã lưu thành công cho Lớp ${cls} – ${capitalize(mood)}!`);
        closeSettings();
      }

      function capitalize(str) {
        return str.charAt(0).toUpperCase() + str.slice(1);
      }

      /****************************************************************
       * Bước 5: Logic Quiz (startQuiz, showQuestion, checkAnswer, endQuiz)
       ****************************************************************/
      let timer,
        remaining,
        idx = 0,
        score = 0,
        currentList = [];
      let hasPlayedWarning = false; // Đánh dấu để chỉ phát 1 lần

      // initialTime dùng để tính thời gian sử dụng
      let initialTime = 0;

      const times = {
        easy: 600,
        normal: 1200,
        hard: 1800,
        veryhard: 2400,
        extreme: 3600,
      };

      function startQuiz(mood) {
        const cls = document.getElementById("classSelect").value;
        document.body.className = mood; // Đổi nền

        // Nếu đang có audio cảnh báo đang phát, tắt nó trước
        warningSound.pause();
        warningSound.currentTime = 0;
        celebrationSound.pause();
        celebrationSound.currentTime = 0;
        hasPlayedWarning = false;

        clearInterval(timer);
        document.getElementById("quiz").innerHTML = "";

        const maxQ = parseInt(numQuestionsInput.value) || 35;
        const data = questionsByClassAndMood[cls][mood] || {
          grammar: [],
          reading: { passage: "", qs: [] },
        };
        // Ghép grammar + reading
        const allQ = [];
        data.grammar.forEach((it) => {
          allQ.push({ type: "grammar", content: it });
        });
        data.reading.qs.forEach((it) => {
          allQ.push({ type: "reading", content: it });
        });
        currentList = allQ.slice(0, maxQ);
        idx = 0;
        score = 0;
        remaining = times[mood] || 600;
        initialTime = remaining;
        updateTimer();

        if (currentList.length > 0) {
          showQuestion();
        } else {
          document.getElementById("quiz").innerHTML =
            "<p style='font-size:16px; color:#333; text-align:center; margin-top:20px;'>Chưa có bài tập cho Lớp " +
            cls +
            " – " +
            capitalize(mood) +
            ".<br>Vào Cài đặt để thêm nội dung.</p>";
        }

        timer = setInterval(() => {
          remaining--;
          updateTimer();

          // Chỉ xét âm thanh và pháo hoa khi remaining mới chuyển về 20
          if (remaining === 20 && !hasPlayedWarning) {
            hasPlayedWarning = true;
            // Phát âm thanh cảnh báo
            warningSound.play().catch((e) => {
              console.warn("Không thể phát âm thanh:", e);
            });
            // Bật hiệu ứng pháo hoa
            startFireworks();
          }

          // Nếu hết giờ
          if (remaining <= 0) {
            endQuiz(false); // false = không phải hoàn thành sớm
          }
        }, 1000);
      }

      function updateTimer() {
        const m = Math.floor(remaining / 60);
        const s = remaining % 60;
        document.getElementById("timer").innerText = `Thời gian còn: ${
          m < 10 ? "0" + m : m
        }:${s < 10 ? "0" + s : s}`;
      }

      function showQuestion() {
        const container = document.getElementById("quiz");
        container.innerHTML = "";

        // Nếu đến đoạn reading (sau hết grammar), chèn passage
        const cls = document.getElementById("classSelect").value;
        const mood = document.querySelector("body").className;
        const data = questionsByClassAndMood[cls][mood];
        const numGrammar = data.grammar.length;
        if (idx === numGrammar && data.reading.passage) {
          const p = document.createElement("div");
          p.className = "passage";
          p.innerText = data.reading.passage;
          container.appendChild(p);
        }

        // Nếu hết câu
        if (idx >= currentList.length) return endQuiz(true); // true = hoàn thành sớm

        // Hiển thị câu thứ idx
        const itWrap = currentList[idx];
        const it = itWrap.content; // { q, opts, a }
        const qDiv = document.createElement("div");
        qDiv.className = "question-container";
        qDiv.innerHTML = `<p>${idx + 1}. ${it.q}</p>`;
        const optsDiv = document.createElement("div");
        optsDiv.className = "options";
        for (let key in it.opts) {
          const lbl = document.createElement("label");
          lbl.innerHTML = `<input type="radio" name="opt" value="${key}"> ${key.toUpperCase()}. ${
            it.opts[key]
          }`;
          optsDiv.appendChild(lbl);
        }
        qDiv.appendChild(optsDiv);
        const btn = document.createElement("button");
        btn.textContent = "Nộp";
        btn.style.marginTop = "12px";
        btn.onclick = () => checkAnswer(it);
        qDiv.appendChild(btn);
        const fb = document.createElement("div");
        fb.className = "feedback";
        qDiv.appendChild(fb);
        container.appendChild(qDiv);
      }

      function checkAnswer(item) {
        const fb = document.querySelector(".feedback");
        const sel = document.querySelector("input[name=opt]:checked");
        const correct = sel && sel.value === item.a;
        if (correct) {
          score++;
          fb.innerText = "Đúng!";
          fb.classList.add("correct");
          fb.classList.remove("wrong");
        } else {
          fb.innerText = `Sai! Đáp án đúng: ${item.opts[item.a]}`;
          fb.classList.add("wrong");
          fb.classList.remove("correct");
        }
        setTimeout(() => {
          idx++;
          showQuestion();
        }, 800);
      }

      /**
       * endQuiz(sớm)
       *   - early: boolean, true nếu người dùng hoàn thành sớm, false nếu hết giờ
       */
      function endQuiz(early) {
        clearInterval(timer);

        // Nếu có audio cảnh báo đang phát, tắt nó
        warningSound.pause();
        warningSound.currentTime = 0;

        // Tính toán kết quả
        const total = currentList.length;
        const pct = total > 0 ? Math.round((score / total) * 100) : 0;
        let msg = "";
        if (pct === 100) msg = "Xuất sắc! 🌟";
        else if (pct >= 80) msg = "Rất tốt! 👍";
        else if (pct >= 50) msg = "Khá ổn! 😌";
        else msg = "Cần cố gắng thêm 🛠️";

        // Nếu hoàn thành sớm, phát âm thanh chúc mừng
        if (early && remaining > 0) {
          celebrationSound.play().catch((e) => {
            console.warn("Không thể phát âm thanh chúc mừng:", e);
          });
        }

        // Tính thời gian sử dụng (tính từ lúc bắt đầu tới lúc kết thúc)
        const timeUsed = initialTime - remaining;

        // Hiển thị kết quả lên UI
        document.getElementById("quiz").innerHTML = `
        <h2 style="text-align:center;">Kết quả: ${pct}% (${score}/${total})</h2>
        <p style="text-align:center; font-size:16px;">${msg}</p>
      `;

        // Lưu vào leaderboard (dù user hoàn thành sớm hay hết giờ đều tính)
        const cls = document.getElementById("classSelect").value;
        const mood = document.querySelector("body").className;
        const entry = {
          class: cls,
          difficulty: mood,
          scorePct: pct,
          timeUsed: timeUsed,
          timestamp: Date.now(),
        };
        addToLeaderboard(entry);
      }

      window.addEventListener("load", () => {
        settingsClassSelect.value = "9";
        settingsMoodSelect.value = "easy";
        loadSettingsIntoPanel();
      });

      /****************************************************************
       * Bước 6: PHẦN “XUẤT FILE” MỚI – gọn nhẹ, không cần giữ htmlTemplate
       ****************************************************************/
      document.getElementById("export-btn").onclick = function () {
        // 1. Lấy JSON dữ liệu mới đã chỉnh sửa
        const updatedJSON = JSON.stringify(questionsByClassAndMood, null, 2);

        // 2. Lấy nguyên toàn bộ HTML hiện tại (cả DOCTYPE, CSS, JS, DOM)
        let fullHTML = document.documentElement.outerHTML;

        // 3. Thay đoạn khai báo cũ bằng JSON mới
        fullHTML = fullHTML.replace(
          /let questionsByClassAndMood = JSON\.parse\(JSON\.stringify\(defaultData\)\);/,
          "let questionsByClassAndMood = JSON.parse(`" +
            updatedJSON.replace(/`/g, "\\`") +
            "`);"
        );

        // 4. Tạo Blob & cho phép tải file “quiz_app.html”
        const blob = new Blob([fullHTML], { type: "text/html" });
        const url = URL.createObjectURL(blob);
        const a = document.createElement("a");
        a.href = url;
        a.download = "quiz_app.html";
        document.body.appendChild(a);
        a.click();
        document.body.removeChild(a);
        URL.revokeObjectURL(url);
      };
    </script>
  </body>
</html>
