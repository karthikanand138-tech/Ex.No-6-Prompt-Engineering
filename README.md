Ex.No.6 Development of Python Code Compatible with Multiple AI Tools

Aim: 

Write and implement Python code that integrates with multiple AI tools to automate the task of interacting with APIs, comparing outputs, and generating actionable insights with Multiple AI Tools.

Explanation:

Develop a python code that integrates multiple AI tool by interacting with their APIs.
Compare outputs from different APIs.
Analyze the response and the Output.

The aim is to understand how to request help from AI tools for tasks like writing Python code, integrating with APIs, comparing outputs, and generating actionable insights.

💻 Python Code:
import requests

# 🔑 API KEYS (Replace with your keys)
OPENAI_API_KEY = "your_openai_api_key"
HUGGINGFACE_API_KEY = "your_huggingface_api_key"

# 🧠 OpenAI API Function
def fetch_openai(prompt):
    url = "https://api.openai.com/v1/chat/completions"
    
    headers = {
        "Authorization": f"Bearer {OPENAI_API_KEY}",
        "Content-Type": "application/json"
    }

    body = {
        "model": "gpt-4o-mini",
        "messages": [{"role": "user", "content": prompt}]
    }

    response = requests.post(url, headers=headers, json=body)
    return response.json()["choices"][0]["message"]["content"]


# 🤖 HuggingFace API Function
def fetch_huggingface(prompt):
    url = "https://api-inference.huggingface.co/models/distilgpt2"

    headers = {
        "Authorization": f"Bearer {HUGGINGFACE_API_KEY}"
    }

    body = {
        "inputs": prompt
    }

    response = requests.post(url, headers=headers, json=body)
    return response.json()[0]["generated_text"]


# ⚖️ Advanced Comparison Function
def analyze_responses(resp1, resp2):
    print("\n========== RESPONSES ==========")
    print("\n🔵 OpenAI:\n", resp1)
    print("\n🟢 HuggingFace:\n", resp2)

    # Length comparison
    if len(resp1) > len(resp2):
        detail = "OpenAI gives more detailed answer"
    elif len(resp2) > len(resp1):
        detail = "HuggingFace gives more detailed answer"
    else:
        detail = "Both answers are equal in length"

    # Keyword analysis
    keywords = ["AI", "intelligence", "learning", "data"]
    score1 = sum(word.lower() in resp1.lower() for word in keywords)
    score2 = sum(word.lower() in resp2.lower() for word in keywords)

    if score1 > score2:
        quality = "OpenAI response has more relevant keywords"
    elif score2 > score1:
        quality = "HuggingFace response has more relevant keywords"
    else:
        quality = "Both responses are similar in relevance"

    return detail, quality


# 📊 Insight Generator
~~~
def generate_summary(detail, quality):
    print("\n========== ANALYSIS ==========")
    print("✔ Detail Analysis:", detail)
    print("✔ Quality Analysis:", quality)

    if "OpenAI" in detail:
        print("👉 Suggestion: Use OpenAI for detailed explanations")
    else:
        print("👉 Suggestion: Use HuggingFace for short answers")

# 🚀 Main Execution
if __name__ == "__main__":
    user_prompt = input("Enter your question: ")

    try:
        openai_output = fetch_openai(user_prompt)
        hf_output = fetch_huggingface(user_prompt)

        detail, quality = analyze_responses(openai_output, hf_output)
        generate_summary(detail, quality)

    except Exception as e:
        print("⚠ Error:", e)

~~~
🔥 Sample Output:
~~~
Enter your question: What is Machine Learning?

========== RESPONSES ==========

🔵 OpenAI:
Machine Learning is a subset of AI...

🟢 HuggingFace:
Machine learning is a method...

========== ANALYSIS ==========
✔ Detail Analysis: OpenAI gives more detailed answer
✔ Quality Analysis: OpenAI response has more relevant keywords

👉 Suggestion: Use OpenAI for detailed explanations

~~~
 Result:

The program was successfully implemented to:

Integrate multiple AI APIs
Compare outputs using advanced logic
Analyze responses based on detail and relevance
Generate actionable insights
