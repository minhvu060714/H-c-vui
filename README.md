export default {
  async fetch(req, env) {
    if (req.method !== "POST") {
      return new Response("OK");
    }

    const { level } = await req.json();

    const prompt = `
Bạn là chuyên gia phong thuỷ.
Tạo 1 câu hỏi trắc nghiệm phong thuỷ.
Mức độ: ${level}

Yêu cầu:
- 4 đáp án
- 1 đáp án đúng
- Giải thích ngắn gọn, dễ hiểu
- Không mê tín cực đoan

Trả về JSON đúng mẫu:
{
  "question": "",
  "options": ["", "", "", ""],
  "correct": 0,
  "explain": ""
}
`;

    const aiRes = await fetch("https://api.openai.com/v1/chat/completions", {
      method: "POST",
      headers: {
        "Authorization": `Bearer ${env.OPENAI_KEY}`,
        "Content-Type": "application/json"
      },
      body: JSON.stringify({
        model: "gpt-4.1-mini",
        messages: [{ role: "user", content: prompt }],
        temperature: 0.7
      })
    });

    const data = await aiRes.json();
    const content = data.choices[0].message.content;

    return new Response(content, {
      headers: { "Content-Type": "application/json" }
    });
  }
};