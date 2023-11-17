<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>OpenAI Integration</title>
</head>
<body>
<header>
        <h1>OpenAI Integration</h1>
    </header>
<main>
        <div id="ai-content">
<div id="chat-window">
            <div id="chat-area"></div>
            <div id="input-area">
                <input type="text" id="user-input" placeholder="Your message...">
            </div>
            <button type="submit" id="send-button">Send</button>
        </div>
    </main>
<script src="https://cdn.jsdelivr.net/npm/openai@0.30.0"></script> <script>
  // Get the necessary elements from your HTML
  const chatArea = document.getElementById("chat-area");
  const userInput = document.getElementById("user-input");
  const sendButton = document.getElementById("send-button");
  const systemPromptInput = document.getElementById("system-prompt-input");
  
  // Store the initial system prompt
  let systemPrompt = systemPromptInput.value;

  // Listen for user input and handle it
  sendButton.addEventListener("click", async () => {
    const userMessage = userInput.value;
    
    // If the user changes the system prompt, update it
    if (systemPromptInput.value !== "") {
      systemPrompt = systemPromptInput.value;
    }

    const response = await fetch('/api/completion', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ userMessage, systemPrompt })
    });

    const { aiResponse } = await response.json();

    // Display the user's message
    chatArea.innerHTML += `<p>You: ${userMessage}</p>`;

    // Display the AI's response
    chatArea.innerHTML += `<p>AI: ${aiResponse}</p>`;

    userInput.value = "";
  });

  // Feel free to add more code to enhance your chatbot's functionality
</script>
</body>
</html>