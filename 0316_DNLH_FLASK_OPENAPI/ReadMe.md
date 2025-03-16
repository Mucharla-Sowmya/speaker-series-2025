# 📢 Dot Net Learners House Meetup – Monthly Event - Mar 2025

## Date Time: 16-Mar-2025 at 09:00 AM IST

## Event URL: [https://www.meetup.com/dot-net-learners-house-hyderabad/events/304750920](https://www.meetup.com/dot-net-learners-house-hyderabad/events/304750920)

## YouTube URL: [https://www.youtube.com/watch?v=rrZqYt2YDFM](https://www.youtube.com/watch?v=rrZqYt2YDFM)



![Information | 100x100](./Documentation/Images/Information.PNG)

![Seat Belt | 100x100](./Documentation/Images/SeatBelt.PNG)



## *🎯 Goal of the Session:*  
✅ Handle *CORS errors & security*.
✅ Connect the *React UI* to the Flask backend.  
✅ Learn how *React sends API requests* to Flask.  
---

## *📝 Demo Script:*

### *1️⃣ Introduction (2 min)*
- "Now that Tejasree has built the UI, let’s integrate it with our Flask API."
- "We’ll focus on making *API calls from React to Flask* and fixing *CORS issues*."
- "By the end of this session, our UI will *send user prompts to Flask and receive AI responses.*"

---
![Architecture Diagram | 100x100](./Documentation/Images/ArchitectureDiagram.jpg)


### *2️⃣ Fixing CORS Issues in Flask (4 min)*
- "If we see *CORS errors*, we need to enable CORS in Flask."
- *Install Flask-CORS:*
  bash
  pip install flask-cors
  
- **Modify app.py:**
  python
  from flask import Flask
  from flask_cors import CORS

  app = Flask(__name__)
  CORS(app)  # Enable CORS globally
  
- "Now, restart Flask, and the UI should work!"

---
### **3️⃣ Setting Up API Calls in React (6 min)*
- "Instead of handling API calls inside every component, let’s *create a separate API utility*."
- **Create api.ts:**
  tsx
  export const fetchAIResponse = async (prompt: string): Promise<string> => {
    try {
      const res = await fetch("http://127.0.0.1:5009/api/completions", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ prompt }),
      });

      if (!res.ok) {
        throw new Error("Failed to fetch response");
      }

      return await res.text();
    } catch (error) {
      console.error("Error:", error);
      return "⚠ Error fetching response.";
    }
  };
  
- "This makes our API calls *cleaner and reusable*."

---

### *4️⃣ Modifying Chat.tsx to Send Requests (5 min)**
- "Now, let’s modify our UI to fetch responses."
- **Update Chat.tsx:**
  tsx
  import { useState } from "react";
  import { fetchAIResponse } from "./api";

  const Chat: React.FC = () => {
    const [prompt, setPrompt] = useState<string>("");
    const [response, setResponse] = useState<string>("Your response will appear here");

    const sendRequest = async () => {
      setResponse("Thinking... 🤔");
      setResponse(await fetchAIResponse(prompt));
    };

    return (
      <div className="p-6 w-full max-w-2xl mx-auto space-y-4 font-inter">
        <h2 className="text-2xl font-semibold text-gray-800">Chat with AI 🤖</h2>

        <div className="bg-gray-700 text-white p-4 rounded-lg border-l-4 border-blue-500 min-h-[100px] flex items-center">
          <p className="text-base font-light">{response}</p>
        </div>

        <textarea
          className="w-full p-3 border rounded-lg shadow-md focus:ring focus:ring-blue-300"
          placeholder="Type your question..."
          value={prompt}
          onChange={(e) => setPrompt(e.target.value)}
        />

        <button
          onClick={sendRequest}
          className="bg-blue-600 text-white px-6 py-2 rounded-lg hover:bg-blue-700 transition"
        >
          🚀 Send
        </button>
      </div>
    );
  };

  export default Chat;
  
- "Now, our UI can send requests to Flask and display responses!"

---

### *5️⃣ Wrap-up & Next Steps (2 min)*
- "Now our *React UI communicates with Flask without issues!* 🎉"
- "Swamy will now take over to discuss *.NET Aspire & more tech integrations.*"
- "Thanks for joining!"

---

### 🔹 *Final Thoughts*
- *Tejasree’s session* focused on UI development.  
- *Sowmya’s session* handled API integration, CORS, and structured API calls.  

These changes *perfectly align with the revised agenda!* 🚀 Let me know if you need any refinements.