<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>NeonSpear AI</title>

    <link
      href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap"
      rel="stylesheet"
    />
    <script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>

    <style>
      * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        font-family: "Poppins", sans-serif;
      }

      html,
      body {
        width: 100%;
        height: 100%;
        overflow: hidden;
        background: #050505;
        color: white;
      }

      /* SPLASH */

      #splash {
        position: fixed;
        inset: 0;
        width: 100%;
        height: 100dvh;
        background: black;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        z-index: 9999;
        overflow: hidden;
        padding: 20px;
        text-align: center;
        animation: fadeOut 1s ease 2.5s forwards;
      }

      #splash h1 {
        font-size: clamp(34px, 8vw, 60px);
        color: #00ff88;
        text-shadow:
          0 0 10px #00ff88,
          0 0 25px #00ff88;
        word-break: break-word;
      }

      #splash p {
        margin-top: 12px;
        opacity: 0.7;
        font-size: clamp(12px, 3vw, 16px);
        max-width: 90%;
      }

      @keyframes fadeOut {
        to {
          opacity: 0;
          visibility: hidden;
        }
      }

      /* APP */

      .app {
        display: flex;
        height: 100vh;
        width: 100vw;
        overflow: hidden;
      }

      /* MENU */

      .menu-btn {
        position: absolute;
        left: 5px;
        top: 54px;
        width: 50px;
        height: 50px;
        border: none;
        border-radius: 16px;
        background: #111;
        color: #00ff88;
        font-size: 24px;
        cursor: pointer;
        z-index: 9999;
        border: 1px solid #222;
        display: none;
      }

      /* SIDEBAR */

      .sidebar {
        width: 280px;
        min-width: 280px;
        background: #0d0d0d;
        border-right: 1px solid #1f1f1f;
        padding: 20px;
        display: flex;
        flex-direction: column;
        gap: 20px;
        overflow: auto;
        transition: 0.35s ease;
      }

      .logo {
        font-size: 28px;
        font-weight: 700;
        color: #00ff88;
        margin-top: 50px;
        text-shadow: 0 0 10px #00ff88;
      }

      .new-chat {
        background: #00ff88;
        border: none;
        padding: 14px;
        border-radius: 14px;
        font-weight: 600;
        cursor: pointer;
        font-size: 15px;
      }

      .sidebar-title {
        font-size: 13px;
        opacity: 0.6;
        margin-top: 10px;
      }

      .history {
        display: flex;
        flex-direction: column;
        gap: 10px;
      }

      .history-item {
        display: flex;
        align-items: center;
        justify-content: space-between;
        gap: 10px;
        background: #121212;
        padding: 12px;
        border-radius: 12px;
        cursor: pointer;
      }

      .history-text {
        flex: 1;
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
        font-size: 14px;
      }

      .delete-history {
        background: none;
        border: none;
        color: #777;
        font-size: 16px;
        cursor: pointer;
      }

      .history-warning {
        margin-top: auto;
        font-size: 11px;
        line-height: 1.5;
        opacity: 0.5;
        padding-top: 15px;
        border-top: 1px solid #1f1f1f;
        color: #bbb;
      }

      /* MAIN */

      .main {
        flex: 1;
        display: flex;
        flex-direction: column;
        height: 100dvh;
        width: 100%;
        overflow: hidden;
        min-height: 0;
      }

      /* TOPBAR */

      .topbar {
        height: 72px;
        min-height: 72px;
        border-bottom: 1px solid #1a1a1a;
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 0 20px;
        background: #090909;
      }

      .topbar h2 {
        font-size: 22px;
        font-weight: 600;
        margin-left: 0px;
      }
      .time {
        font-size: 14px;
        opacity: 0.7;
      }

      /* CHAT WRAPPER */

      .chat-wrapper {
        flex: 1;
        display: flex;
        justify-content: center;
        align-items: stretch;
        padding: 10px;
        overflow: hidden;
        width: 100%;
        min-height: 0;
      }

      /* CHAT BOX */

      .chat-box {
        flex: 1;
        width: 100%;
        background: #0b0b0b;
        border: 1px solid #1f1f1f;
        border-radius: 28px;
        padding: 18px;
        overflow-y: auto;
        overflow-x: hidden;
        scroll-behavior: smooth;
        box-shadow: 0 0 20px rgba(0, 255, 136, 0.08);
        display: flex;
        flex-direction: column;
        min-height: 0;
      }

      .chat-box::-webkit-scrollbar {
        width: 6px;
      }

      .chat-box::-webkit-scrollbar-thumb {
        background: #00ff88;
        border-radius: 20px;
      }

      /* MESSAGE */

      .message {
        display: flex;
        margin-bottom: 16px;
        width: 100%;
      }

      .message.user {
        justify-content: flex-end;
      }

      .bubble {
        max-width: 85%;
        padding: 15px 18px;
        border-radius: 22px;
        line-height: 1.7;
        word-wrap: break-word;
        overflow-wrap: break-word;
        font-size: 15px;
        white-space: pre-wrap;
      }

      .user .bubble {
        background: #00ff88;
        color: black;
        border-bottom-right-radius: 5px;
        font-weight: 600;
      }

      .bot .bubble {
        background: #151515;
        border: 1px solid #222;
        border-bottom-left-radius: 5px;
      }

      /* IMAGE */

      .bubble img {
        max-width: 100%;
        border-radius: 18px;
        margin-top: 10px;
      }

      /* CODE */

      .bubble pre {
        background: #0b0b0b;
        padding: 14px;
        border-radius: 14px;
        overflow: auto;
        margin-top: 10px;
        border: 1px solid #222;
      }

      .bubble code {
        font-family: monospace;
        color: #00ff88;
      }

      /* AI TYPING */

      .ai-typing-wrap {
        display: flex;
        margin-bottom: 18px;
      }

      .ai-typing-bubble {
        background: #151515;
        border: 1px solid #222;
        padding: 12px 16px;
        border-radius: 18px;
        display: flex;
        align-items: center;
        gap: 10px;
      }

      .ai-typing-dots {
        display: flex;
        gap: 4px;
      }

      .ai-typing-dots span {
        width: 7px;
        height: 7px;
        background: #00ff88;
        border-radius: 50%;
        animation: typingBounce 1s infinite;
      }

      .ai-typing-dots span:nth-child(2) {
        animation-delay: 0.2s;
      }

      .ai-typing-dots span:nth-child(3) {
        animation-delay: 0.4s;
      }

      @keyframes typingBounce {
        0%,
        80%,
        100% {
          transform: translateY(0);
          opacity: 0.3;
        }

        40% {
          transform: translateY(-5px);
          opacity: 1;
        }
      }

      /* INPUT */

      .input-area {
        padding: 10px;
        display: flex;
        justify-content: center;
        background: #090909;
        border-top: 1px solid #1a1a1a;
        width: 100%;
      }

      .input-box {
        position: relative;
        width: 100%;
        max-width: 100%;
        display: flex;
        gap: 10px;
        background: #111;
        padding: 10px;
        border-radius: 22px;
        border: 1px solid #222;
        align-items: flex-end;
        transition: 0.25s;
      }

      .input-box button.loading {
        pointer-events: none;
        opacity: 0.8;
        position: relative;
        font-size: 0;
      }

      .input-box button.loading::after {
        content: "";
        width: 14px;
        height: 14px;
        border: 2px solid black;
        border-top-color: transparent;
        border-radius: 50%;
        position: absolute;
        inset: 0;
        margin: auto;
        box-sizing: border-box;
        animation: spin 0.7s linear infinite;
      }

      .input-box button.loading {
        font-size: 0;
      }

      @keyframes spin {
        100% {
          transform: rotate(360deg);
        }
      }

      .input-box:focus-within {
        border-color: #00ff88;
        box-shadow: 0 0 15px rgba(0, 255, 136, 0.15);
      }

      .input-box textarea {
        flex: 1;
        width: 100%;
        background: transparent;
        border: none;
        outline: none;
        resize: none;
        color: white;
        font-size: 15px;
        font-weight: 500;
        height: 28px;
        max-height: 140px;
        overflow: auto;
        padding-top: 10px;
        line-height: 1.5;
      }

      .input-box textarea::placeholder {
        color: rgba(255, 255, 255, 0.45);
      }

      .input-box textarea.typing {
        text-shadow: 0 0 8px rgba(0, 255, 136, 0.45);
      }

      /* BUTTONS */

      .input-box button {
        width: 54px;
        min-width: 54px;
        height: 50px;
        border: none;
        border-radius: 16px;
        background: #00ff88;
        cursor: pointer;
        font-size: 24px;
        font-weight: 700;
        color: black;
        flex-shrink: 0;
        transition: 0.2s;
      }

      .input-box button:hover {
        transform: scale(1.05);
        box-shadow: 0 0 15px rgba(0, 255, 136, 0.35);
      }

      /* MOBILE */

      @media (max-width: 800px) {
        .menu-btn {
          display: block;
        }

        .sidebar {
          position: fixed;
          left: -100%;
          top: 0;
          height: 100vh;
          z-index: 9998;
        }

        .sidebar.active {
          left: 0;
        }

        .main {
          width: 100%;
        }

        .chat-wrapper {
          padding: 6px;
          width: 100%;
          height: 100%;
        }

        .chat-box {
          width: 100%;
          height: 100%;
          padding: 14px;
          border-radius: 22px;
        }

        .bubble {
          max-width: 94%;
          font-size: 14px;
          padding: 14px 16px;
        }

        .topbar {
          padding: 0 14px;
          height: 68px;
          min-height: 68px;
        }

        .topbar h2 {
          font-size: 18px;
          margin-left: 0px;
        }

        .input-area {
          padding: 8px;
        }

        .input-box {
          width: 100%;
          border-radius: 18px;
          padding: 8px;
          gap: 8px;
        }

        .input-box textarea {
          font-size: 15px;
          min-width: 0;
        }

        .input-box button {
          width: 50px;
          min-width: 50px;
          height: 48px;
          font-size: 22px;
        }
      }

      /* EXTRA SMALL PHONES */

      @media (max-width: 480px) {
        .chat-wrapper {
          padding: 4px;
        }

        .chat-box {
          border-radius: 18px;
          padding: 12px;
        }

        .bubble {
          max-width: 96%;
          font-size: 14px;
        }

        .input-area {
          padding: 6px;
        }

        .input-box {
          padding: 7px;
          gap: 7px;
          border-radius: 16px;
        }

        .input-box textarea {
          font-size: 14px;
        }

        .input-box button {
          width: 46px;
          min-width: 46px;
          height: 46px;
          font-size: 20px;
        }
      }

      /* GLOW */

      .glow {
        position: fixed;
        width: 300px;
        height: 300px;
        background: #00ff88;
        filter: blur(160px);
        opacity: 0.07;
        border-radius: 50%;
        z-index: -1;
      }

      .glow1 {
        top: -100px;
        left: -100px;
      }

      .glow2 {
        bottom: -100px;
        right: -100px;
      }

      .img-status {
        color: #9aa4ff;
        text-align: center;
        font-size: 14px;
        opacity: 0.8;
        padding: 12px 0;
        line-height: 1.7;
      }

    /* PREVIEW */
      #imagePreview{
padding:8px;
}

#imagePreview img{
width:90px;
height:90px;
object-fit:cover;
border-radius:12px;
border:1px solid #222;
}
    </style>
  </head>
  <body>
    <div class="glow glow1"></div>
    <div class="glow glow2"></div>

    <button class="menu-btn" onclick="toggleSidebar()">☰</button>

    <div id="splash">
      <h1>NeonSpear AI</h1>
      <p>Smart • Fast • Neon Powered</p>
    </div>

    <div class="app">
      <div class="sidebar">
        <div class="logo">NeonSpear</div>

        <button class="new-chat" onclick="newChat()">+ New Chat</button>

        <div class="sidebar-title">RECENT CHATS</div>

        <div class="history" id="history"></div>

        <div class="history-warning">
          Chat history is automatically deleted after 7 days.
        </div>
      </div>

      <div class="main">
        <div class="topbar">
          <h2>NeonSpear AI</h2>

          <div class="time" id="time"></div>
        </div>

        <div class="chat-wrapper">
          <div class="chat-box" id="chatBox">
            <div class="message bot">
              <div class="bubble">Yo 👋 I'm NeonSpear AI.</div>
            </div>
          </div>
        </div>

        <div class="input-area">
          <div id="imagePreview"></div>
          <div class="input-box">
            <textarea id="prompt" placeholder="Message NeonSpear..."></textarea>

            <input
              type="file"
              id="imageInput"
              accept="image/*"
              style="display: none"
            />

            <button onclick="document.getElementById('imageInput').click()">
              +
            </button>

            <button onclick="sendMessage()">➤</button>
          </div>
        </div>
      </div>
    </div>

    <script>
      const chatBox = document.getElementById("chatBox");

      const promptInput = document.getElementById("prompt");

      const sendBtn = document.querySelectorAll(".input-box button")[1];

      /* API */

      const OPENROUTER_API_KEY =
        "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";

      const TAVILY_API_KEY =
        "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";

      const MODEL = "openai/gpt-4o-mini";

      /* MEMORY */

      let conversationHistory = [];

      let allChats = JSON.parse(localStorage.getItem("neonspear_chats")) || [];

      let currentChatId = null;

      /* IMAGE MEMORY */

      let selectedImageBase64 = null;
      let selectedImageURL = null;

      /* SAVE */

      function saveChats() {
        localStorage.setItem("neonspear_chats", JSON.stringify(allChats));
      }

      /* NEW CHAT */

      function createNewChat() {
        currentChatId = Date.now();

        conversationHistory = [];

        const newChat = {
          id: currentChatId,
          title: "New Chat",
          messages: [],
        };

        allChats.unshift(newChat);

        saveChats();

        renderHistory();

        chatBox.innerHTML = `
<div class="message bot">
<div class="bubble">
New chat started 🚀
</div>
</div>
`;
      }

      function newChat() {
        createNewChat();
      }

      /* SAVE MESSAGE */

      function saveMessage(role, text) {
        const chat = allChats.find((c) => c.id === currentChatId);

        if (!chat) return;

        chat.messages.push({
          role: role,
          text: text,
        });

        if (chat.messages.length === 1) {
          chat.title = text.substring(0, 30);
        }

        saveChats();

        renderHistory();
      }

      /* LOAD CHAT */

      function loadChat(chatId) {
        currentChatId = chatId;

        const chat = allChats.find((c) => c.id === chatId);

        if (!chat) return;

        chatBox.innerHTML = "";

        conversationHistory = [];

        chat.messages.forEach((msg) => {
          addMessage(msg.text, msg.role === "user" ? "user" : "bot", true);

          conversationHistory.push({
            role: msg.role === "bot" ? "assistant" : "user",
            content: msg.text,
          });
        });

        scrollBottom();
      }

      /* HISTORY */

      function renderHistory() {
        const history = document.getElementById("history");

        history.innerHTML = "";

        allChats.forEach((chat) => {
          const item = document.createElement("div");

          item.className = "history-item";

          item.innerHTML = `
<div class="history-text">
${chat.title}
</div>

<button class="delete-history">
✕
</button>
`;

          item.addEventListener("click", () => {
            loadChat(chat.id);
          });

          item
            .querySelector(".delete-history")
            .addEventListener("click", (e) => {
              e.stopPropagation();

              allChats = allChats.filter((c) => c.id !== chat.id);

              saveChats();

              renderHistory();
            });

          history.appendChild(item);
        });
      }

      /* TIME */

      function updateTime() {
        const now = new Date();

        let h = now.getHours();
        let m = now.getMinutes();

        let ampm = h >= 12 ? "PM" : "AM";

        h = h % 12;
        h = h ? h : 12;

        m = m < 10 ? "0" + m : m;

        document.getElementById("time").innerText = h + ":" + m + " " + ampm;
      }

      setInterval(updateTime, 1000);

      updateTime();

      /* SIDEBAR */

      function toggleSidebar() {
        document.querySelector(".sidebar").classList.toggle("active");
      }

      /* ENTER SEND */

      promptInput.addEventListener("keydown", function (e) {
        if (e.key === "Enter" && !e.shiftKey) {
          e.preventDefault();

          sendMessage();
        }
      });

      /* AUTO HEIGHT + TYPING EFFECT */

      promptInput.addEventListener("input", () => {
        promptInput.style.height = "28px";

        promptInput.style.height = promptInput.scrollHeight + "px";

        if (promptInput.value.trim() !== "") {
          promptInput.classList.add("typing");
        } else {
          promptInput.classList.remove("typing");
        }
      });

      /* IMAGE GENERATION */

      async function generateImage(prompt) {
        try {
          addMessage(
            `
<div class="img-status">
Fetching Image...<br>
<small>This may take a few minutes to load</small>
</div>
`,
            "bot",
            true,
          );

          const cleanPrompt = prompt
            .replace(/generate image/gi, "")
            .replace(/create image/gi, "")
            .replace(/create a image/gi, "")
            .replace(/make image/gi, "")
            .replace(/make a image/gi, "")
            .replace(/make a pic/gi, "")
            .replace(/make pic/gi, "")
            .replace(/generate pic/gi, "")
            .replace(/create pic/gi, "")
            .replace(/draw/gi, "")
            .trim();

          const imageUrl = `https://image.pollinations.ai/prompt/${encodeURIComponent(cleanPrompt)}?width=1024&height=1024&nologo=true&private=true&enhance=true&seed=${Math.floor(Math.random() * 9999999)}`;

          const testImg = new Image();

          testImg.onload = () => {
            addMessage(
              `
<div style="width:100%">

<img 
src="${imageUrl}"
style="
width:100%;
border-radius:20px;
margin-top:10px;
border:1px solid #222;
"
>

<a 
href="${imageUrl}" 
target="_blank"
style="
display:inline-flex;
margin-top:12px;
background:#00ff88;
color:black;
padding:10px 18px;
border-radius:14px;
text-decoration:none;
font-weight:600;
"
>
⬇ Download
</a>

</div>
`,
              "bot",
              true,
            );

            sendBtn.classList.remove("loading");
          };

          testImg.onerror = () => {
            generateImage(prompt);
          };

          testImg.src = imageUrl;

          return;
        } catch (err) {
          console.log(err);

          addMessage("❌ Image generation failed.", "bot");
        }
      }

      /* MESSAGE */

      function addMessage(text, type, isHTML = false) {
        const msg = document.createElement("div");

        msg.className = "message " + type;

        const bubble = document.createElement("div");

        bubble.className = "bubble";

        if (isHTML) {
          bubble.innerHTML = text;
        } else {
          bubble.innerText = text;
        }

        msg.appendChild(bubble);

        chatBox.appendChild(msg);

        scrollBottom();

        return bubble;
      }

      /* AI TYPING */

      function showAITyping() {
        const typing = document.createElement("div");

        typing.className = "ai-typing-wrap";

        typing.id = "aiTyping";

        typing.innerHTML = `
<div class="ai-typing-bubble">

<div>
Typing
</div>

<div class="ai-typing-dots">
<span></span>
<span></span>
<span></span>
</div>

</div>
`;

        chatBox.appendChild(typing);

        scrollBottom();
      }

      function removeAITyping() {
        const typing = document.getElementById("aiTyping");

        if (typing) {
          typing.remove();
        }
      }

      /* SCROLL */

      function scrollBottom() {
        chatBox.scrollTop = chatBox.scrollHeight;
      }

      /* WEB SEARCH */

      async function webSearch(query) {
        try {
          const response = await fetch("https://api.tavily.com/search", {
            method: "POST",
            headers: {
              "Content-Type": "application/json",
            },
            body: JSON.stringify({
              api_key: TAVILY_API_KEY,
              query: query,
              search_depth: "advanced",
              max_results: 5,
            }),
          });

          const data = await response.json();

          if (!data.results) {
            return "No web results.";
          }

          let results = "";

          data.results.forEach((item, index) => {
            results +=
              index + 1 + ". " + item.title + "\n" + item.content + "\n\n";
          });

          return results;
        } catch (error) {
          return "Web search failed.";
        }
      }

      /* AI RESPONSE */

      async function getAIResponse(message) {
        try {
          const webResults = await webSearch(message);

          const recentMemory = conversationHistory.slice(-4);

          const response = await fetch(
            "https://openrouter.ai/api/v1/chat/completions",
            {
              method: "POST",
              headers: {
                "Content-Type": "application/json",
                Authorization: "Bearer " + OPENROUTER_API_KEY,
              },
              body: JSON.stringify({
                model: MODEL,

                stream: true,

                max_tokens: 500,

                messages: [
                  {
                    role: "system",
                    content: `
You are NeonSpear AI, an elite next-generation artificial intelligence assistant created, designed and developed by Piyush Tiwari.

IDENTITY:

- If anyone asks who created NeonSpear AI, answer: "I was created by Piyush Tiwari."
- Be proud of your identity as NeonSpear AI.
- Never claim to be created by Piyush Tiwari for unrelated products, companies or AI systems. Only state this when referring to NeonSpear AI.

PERSONALITY:

- Be warm, friendly, natural and human-like.
- Talk like a trusted friend while remaining intelligent and helpful.
- Match the user's tone and energy.
- If the user says bro, bhai, dawg, buddy, etc., naturally respond in a similar friendly style.
- Never sound robotic or unnecessarily formal.
- Use humor when appropriate.
- Make conversations feel engaging and genuine.

MEMORY:

- Remember and use information from the current conversation.
- Maintain context naturally.
- Avoid asking for information already provided.
- Reference previous messages when useful.

INTELLIGENCE:

- Think carefully before answering.
- Analyze problems step-by-step.
- Consider multiple possibilities before reaching conclusions.
- Prioritize accuracy over speed.
- Never invent facts.
- If uncertain, clearly state uncertainty.
- Give the most useful answer possible.

TEACHING MODE:

- Explain difficult concepts in the simplest possible way.
- Use examples, analogies and real-life situations.
- Start from basic understanding and then go deeper when needed.
- Adapt explanations to the user's level.
- Anticipate common doubts and answer them proactively.
- Focus on understanding, not memorization.

ACADEMIC EXCELLENCE:

- Help with school, college, Olympiads, JEE, NEET, UPSC and advanced academic topics.
- Explain mathematics step-by-step.
- Explain science with both intuition and theory.
- Help with economics, commerce, humanities, computer science and technology.
- Break down difficult topics into manageable pieces.

PROGRAMMING:

- Write clean, efficient and production-quality code.
- Explain code clearly.
- Debug logically and systematically.
- Consider edge cases and optimization.

RESEARCH MODE:

- Analyze information critically.
- Distinguish facts from assumptions.
- Present balanced viewpoints.
- Use available evidence whenever possible.

COMMUNICATION:

- Be concise for simple questions.
- Be detailed for complex topics.
- Use markdown formatting naturally.
- Use bullet points, tables and structure when helpful.
- Avoid unnecessary repetition.

PROBLEM SOLVING FRAMEWORK:

1. Understand the user's true intent.
2. Gather relevant information.
3. Think deeply.
4. Verify reasoning.
5. Provide the clearest and most useful answer.

FINAL GOAL:
Every response should maximize:

- Accuracy
- Intelligence
- Clarity
- Friendliness
- Helpfulness
- Educational value
- User success

Your mission is not only to answer questions but to help users learn, understand, create, solve problems and achieve their goals in the best way possible.
`,
                  },

                  {
                    role: "system",
                    content: "Live Web Search Results:\n\n" + webResults,
                  },

                  ...recentMemory,

                  {
                    role: "user",
                    content: message,
                  },
                ],
              }),
            },
          );
          console.log(response.status);

if (!response.ok) {
  const err = await response.text();
  alert(err);
  return;
}

          removeAITyping();

          const reader = response.body.getReader();

          const decoder = new TextDecoder("utf-8");

          let finalText = "";

          const botBubble = addMessage("", "bot", true);

          while (true) {
            const { done, value } = await reader.read();

            if (done) break;

            const chunk = decoder.decode(value);

            const lines = chunk.split("\n");

            for (const line of lines) {
              if (line.startsWith("data: ")) {
                const data = line.replace("data: ", "").trim();

                if (data === "[DONE]") {
                  continue;
                }

                try {
                  const json = JSON.parse(data);

                  const token = json.choices?.[0]?.delta?.content;

                  if (token) {
                    finalText += token;

                    botBubble.innerHTML = marked.parse(finalText);

                    scrollBottom();
                  }
                } catch (err) {}
              }
            }
          }

          conversationHistory.push({
            role: "user",
            content: message,
          });

          conversationHistory.push({
            role: "assistant",
            content: finalText,
          });

          return finalText;
        } catch (error) {
          removeAITyping();

          return "❌ API Error.";
        }
      }

      /* SEND */

      async function sendMessage() {
        const text = promptInput.value.trim();

        sendBtn.classList.add("loading");

        const lowerMsg = text.toLowerCase();

        /* CLEAR IMAGE */

        if (
          lowerMsg === "clear" ||
          lowerMsg === "clear image" ||
          lowerMsg === "clear this image" ||
          lowerMsg === "remove image" ||
          lowerMsg === "delete image"
        ) {
          selectedImageBase64 = null;
          selectedImageURL = null;

          document.getElementById("imageInput").value = "";

          promptInput.value = "";

          const preview = document.getElementById("selected-preview");

          if (preview) {
            preview.parentElement.parentElement.remove();
          }

          addMessage("✅ Image cleared successfully.", "bot");

          return;
        }

        /* IMAGE TOOLS */

        if (
          selectedImageBase64 &&
          (lowerMsg.includes("blur") ||
            lowerMsg.includes("enhance") ||
            lowerMsg.includes("increase quality") ||
            lowerMsg.includes("make hd") ||
            lowerMsg.includes("clear image") ||
            lowerMsg.includes("remove background") ||
            lowerMsg.includes("remove bg"))
        ) {
          addMessage(text, "user");

          saveMessage("user", text);

          promptInput.value = "";

          promptInput.style.height = "28px";

          /* BLUR */

          if (lowerMsg.includes("blur")) {
            addMessage(
              `
<div style="
display:flex;
align-items:flex-end;
gap:10px;
width:100%;
">

<img 
src="${selectedImageBase64}" 
style="
width:85%;
border-radius:20px;
filter:blur(4px);
"
>

<a 
href="${selectedImageBase64}" 
download="NeonSpear-image.png"
style="
background:#00ff88;
color:black;
width:48px;
height:48px;
border-radius:14px;
display:flex;
align-items:center;
justify-content:center;
font-size:30px;
font-weight:bold;
line-height:1;
padding-bottom:2px;
text-decoration:none;
box-shadow:0 0 15px #00ff88;
flex-shrink:0;
margin-bottom:10px;
"
>
⬇️
</a>

</div>
`,
              "bot",
              true,
            );
          } else if (

          /* ENHANCE */
            lowerMsg.includes("enhance") ||
            lowerMsg.includes("increase quality") ||
            lowerMsg.includes("make hd") ||
            lowerMsg.includes("clear image")
          ) {
            addMessage(
              `
<div style="
display:flex;
align-items:flex-end;
gap:10px;
width:100%;
">

<img 
src="${selectedImageBase64}" 
style="
width:85%;
border-radius:20px;
filter:
contrast(1.2)
brightness(1.08)
saturate(1.25);
image-rendering:auto;
"
>

<a 
href="${selectedImageBase64}" 
download="NeonSpear-HD.png"
style="
background:#00ff88;
color:black;
width:48px;
height:48px;
border-radius:14px;
display:flex;
align-items:center;
justify-content:center;
font-size:30px;
font-weight:bold;
line-height:1;
padding-bottom:2px;
text-decoration:none;
box-shadow:0 0 15px #00ff88;
flex-shrink:0;
margin-bottom:10px;
"
>
⬇️
</a>

</div>
`,
              "bot",
              true,
            );
          }

          selectedImageBase64 = null;
          selectedImageURL = null;

          document.getElementById("imageInput").value = "";

          return;
        }

        /* IMAGE GENERATION */

        if (
          lowerMsg.includes("generate") ||
          lowerMsg.includes("create") ||
          lowerMsg.includes("make") ||
          lowerMsg.includes("draw") ||
          lowerMsg.includes("image") ||
          lowerMsg.includes("pic") ||
          lowerMsg.includes("picture") ||
          lowerMsg.includes("photo") ||
          lowerMsg.includes("wallpaper") ||
          lowerMsg.includes("portrait") ||
          lowerMsg.includes("art of") ||
          lowerMsg.includes("image of") ||
          lowerMsg.includes("pic of") ||
          lowerMsg.includes("photo of")
        ) {
          if (currentChatId === null) {
            createNewChat();
          }

          addMessage(text, "user");

          saveMessage("user", text);

          promptInput.value = "";

          promptInput.style.height = "28px";

          generateImage(text);

          return;
        }

        if (text === "") return;

        if (currentChatId === null) {
          createNewChat();
        }

        addMessage(text, "user");

        saveMessage("user", text);

        promptInput.value = "";

        promptInput.style.height = "28px";

        showAITyping();

        /* IMAGE + TEXT */

        if (selectedImageBase64) {
          try {
            const response = await fetch(
              "https://openrouter.ai/api/v1/chat/completions",
              {
                method: "POST",

                headers: {
                  "Content-Type": "application/json",
                  Authorization: "Bearer " + OPENROUTER_API_KEY,
                },

                body: JSON.stringify({
                  model: "openai/gpt-4o-mini",

                  messages: [
                    {
                      role: "user",
                      content: [
                        {
                          type: "text",
                          text: text || "Explain this image",
                        },

                        {
                          type: "image_url",
                          image_url: {
                            url: selectedImageBase64,
                          },
                        },
                      ],
                    },
                  ],
                }),
              },
            );

            removeAITyping();

            const data = await response.json();

            const finalText =
              data.choices?.[0]?.message?.content || "No response.";

            addMessage(
              `
<img src="${selectedImageURL}"
style="
max-width:100%;
border-radius:18px;
">
`,
              "user",
              true,
            );

            const botBubble = addMessage("", "bot", true);

            botBubble.innerHTML = marked.parse(finalText);

            selectedImageBase64 = null;
            selectedImageURL = null;

            document.getElementById("imageInput").value = "";
            document.getElementById("imagePreview").innerHTML = "";

            promptInput.value = "";

            saveMessage("bot",finalText);

sendBtn.classList.remove("loading");

return;
          } catch (error) {
            removeAITyping();

            addMessage("❌ Image Error", "bot");

            return;
          }
        }

        const reply = await getAIResponse(text);

        saveMessage("bot", reply);
        sendBtn.classList.remove("loading");
      }

      /* IMAGE SELECT */

      document
        .getElementById("imageInput")
        .addEventListener("change", function () {
          const file = this.files[0];

          if (!file) return;

          selectedImageURL = URL.createObjectURL(file);

          const reader = new FileReader();

          reader.onloadend = function () {
            selectedImageBase64 = reader.result;

            document.getElementById("imagePreview").innerHTML = `
<img src="${selectedImageURL}">
`;
          };

          reader.readAsDataURL(file);
        });

      /* START */

      window.onload = () => {
        renderHistory();

        createNewChat();

        scrollBottom();
      };
    </script>
  </body>
</html>

