---
layout: none
---

<html lang="ru">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Видеокурс</title>

  <style>
    :root{
      --bg: #0b1220;
      --card: #0f1a2e;
      --card2: #0c1628;
      --text: #e7eefc;
      --muted: #a6b3cf;
      --border: rgba(255,255,255,0.10);
      --link: #8ab4ff;
      --link-hover: #b7d0ff;
      --shadow: 0 12px 30px rgba(0,0,0,.35);
      --radius: 14px;
    }

    *{ box-sizing: border-box; }

    body{
      margin: 0;
      font-family: system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
      background: radial-gradient(1200px 600px at 20% 0%, #142548 0%, var(--bg) 55%);
      color: var(--text);
      line-height: 1.45;
    }

    .wrap{
      max-width: 860px;
      margin: 0 auto;
      padding: 28px 16px 48px;
    }

    header{
      margin-bottom: 18px;
    }

    h1{
      margin: 0 0 8px;
      font-size: 28px;
      letter-spacing: .2px;
    }

    .subtitle{
      margin: 0;
      color: var(--muted);
      font-size: 14px;
    }

    .grid{
      display: grid;
      gap: 12px;
      margin-top: 18px;
    }

    details{
      background: linear-gradient(180deg, var(--card) 0%, var(--card2) 100%);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      box-shadow: var(--shadow);
      overflow: hidden;
    }

    summary{
      list-style: none;
      cursor: pointer;
      padding: 14px 16px;
      font-weight: 650;
      display: flex;
      align-items: center;
      gap: 10px;
      user-select: none;
    }

    /* Убираем стандартный треугольник */
    summary::-webkit-details-marker{ display:none; }

    /* Кастомный индикатор раскрытия */
    .chev{
      width: 18px;
      height: 18px;
      border: 1px solid var(--border);
      border-radius: 6px;
      display: grid;
      place-items: center;
      flex: 0 0 18px;
      background: rgba(255,255,255,0.04);
    }
    .chev::before{
      content: "›";
      display: block;
      transform: rotate(0deg);
      transition: transform .15s ease;
      font-size: 18px;
      line-height: 18px;
      color: var(--muted);
      margin-top: -1px;
    }
    details[open] .chev::before{
      transform: rotate(90deg);
    }

    .module-title{
      flex: 1;
    }

    .count{
      color: var(--muted);
      font-weight: 600;
      font-size: 12px;
      padding: 4px 8px;
      border: 1px solid var(--border);
      border-radius: 999px;
      background: rgba(255,255,255,0.03);
    }

    .content{
      padding: 0 16px 14px;
    }

    ul{
      margin: 0;
      padding: 0;
      list-style: none;
      display: grid;
      gap: 8px;
    }

    li a{
      display: flex;
      align-items: center;
      gap: 10px;
      padding: 10px 12px;
      border-radius: 12px;
      border: 1px solid rgba(255,255,255,0.08);
      background: rgba(255,255,255,0.03);
      color: var(--link);
      text-decoration: none;
      transition: transform .06s ease, background .12s ease, border-color .12s ease;
      word-break: break-word;
    }

    li a:hover{
      background: rgba(138,180,255,0.10);
      border-color: rgba(138,180,255,0.25);
      color: var(--link-hover);
      transform: translateY(-1px);
    }

    .dot{
      width: 8px;
      height: 8px;
      border-radius: 999px;
      background: rgba(138,180,255,0.8);
      flex: 0 0 8px;
    }

    footer{
      margin-top: 16px;
      color: var(--muted);
      font-size: 13px;
    }

    /* Мобильная дружелюбность */
    @media (max-width: 480px){
      h1{ font-size: 24px; }
      summary{ padding: 12px 12px; }
      .content{ padding: 0 12px 12px; }
      li a{ padding: 10px 10px; }
    }
  </style>
</head>

<body>
  <div class="wrap">
    <header>
      <h1>Видеокурс</h1>
      <p class="subtitle">Выбери модуль → открой урок. Ссылки открываются в новой вкладке.</p>
    </header>

    <div class="grid">
      {% for m in site.data.course.modules %}
        <details>
          <summary>
            <span class="chev" aria-hidden="true"></span>
            <span class="module-title">{{ m.title }}</span>
            <span class="count">{{ m.lessons | size }}</span>
          </summary>

          <div class="content">
            <ul>
              {% for l in m.lessons %}
                <li>
                  <a href="{{ l.url | escape }}" target="_blank" rel="noopener">
                    <span class="dot" aria-hidden="true"></span>
                    <span>{{ l.title }}</span>
                  </a>
                </li>
              {% endfor %}
            </ul>
          </div>
        </details>
      {% endfor %}
    </div>

    <footer>Если что-то не открывается: проверь ссылку в <code>_data/course.yml</code>.</footer>
  </div>
</body>
</html>
