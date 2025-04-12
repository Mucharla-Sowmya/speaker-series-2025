# 📢 Global AI Bootcamp 2025 Hyderabad - 12 April 2025

## Date Time: 12-Apr-2025 at 09:00 AM IST

## Event URL: [https://www.meetup.com/global-ai-hyderabad/events/306095644](https://www.meetup.com/global-ai-hyderabad/events/306095644/)




![WhatsApp Image 2025-04-10 at 21 34 30_1cbdeb2b](https://github.com/user-attachments/assets/e4d49f31-d892-4506-9715-62fcb6200f18)


![WhatsApp Image 2025-04-10 at 21 34 20_76850804](https://github.com/user-attachments/assets/e5a7ee67-94ba-4fc0-8438-0f7da5093842)




![Information](https://github.com/user-attachments/assets/122c9e59-d9a0-4096-8a11-9b5624eccf35)

![SeatBelt](https://github.com/user-attachments/assets/fd782a11-a255-4c8a-a9ed-cdd133437bf6)



## *🎯 Session Objective:*  
  ✅ Understand and fix CORS errors for secure API communication.

  ✅ Seamlessly connect the React UI with the Flask backend.

  ✅ Master how React sends API requests to Flask for dynamic data exchange.
  
---

## *📝 Demo Script:*

### *1️⃣ Introduction (1 min)*
- "With Tejasree having developed the UI, it’s time to integrate it with our Flask API."
- "In this session, we’ll focus on making smooth API calls from React to Flask and resolving CORS issues effectively."
- "By the end, our UI will send user prompts to Flask and receive dynamic AI responses!"

---

# The Architectural Diagram

![SystemArchitecture](https://github.com/user-attachments/assets/731f273c-590c-4c6b-a1b1-b965bf8a35e7)

- "Notice the flow: React sends requests → Flask processes them → Flask responds back to React."


### *2️⃣ "Notice the flow: React sends requests → Flask processes them → Flask responds back to React."*

- "When you encounter CORS errors, it means the browser is blocking requests from React to Flask due to cross-origin rules."

- *Install Flask-CORS:*
        bash

        pip install flask-cors
  
- **Update app.py:**

       
        from flask import Flask
        from flask_cors import CORS
      
        app = Flask(__name__)
        CORS(app)  # Enable CORS globally
  
- "Restart Flask after this, and the UI should communicate without CORS issues!"


---
### **3️⃣ Setting Up API Calls in React (2 min)*

- "Instead of embedding API calls in every component, we’ll create a reusable API utility."

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
  
- "This keeps our API calls clean, organized, and easy to maintain."


---

### *4️⃣ Updating Chat.tsx to Send Requests (1 min)**

- "Now, let's modify the Chat component to send requests to Flask."

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
  
- "With this, the UI now interacts with the Flask backend and displays responses dynamically!"


---

### *5️⃣ Wrap-up & Next Steps (1 min)*

- "We’ve successfully connected our React UI with Flask and handled CORS issues like pros!" 🎉
- "Thanks for participating!"
