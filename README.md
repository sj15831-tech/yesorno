<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>예/아니오 투표</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    body {
      font-family: 'Jua', 'Noto Sans KR', sans-serif;
      background: linear-gradient(180deg, #fef9f9 0%, #f3f4ff 100%);
      text-align: center;
      color: #333;
      margin: 0;
      padding: 2rem;
    }
    h1 {
      font-size: 1.6rem;
      margin-bottom: 1.2rem;
      color: #374151;
    }
    .button-container {
      display: flex;
      justify-content: center;
      gap: 1rem;
      margin-bottom: 2rem;
    }
    button {
      font-size: 1.2rem;
      padding: 1rem 2rem;
      border: none;
      border-radius: 30px;
      cursor: pointer;
      color: white;
      transition: all 0.3s ease;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
    }
    #yesBtn {
      background: linear-gradient(135deg, #34d399, #10b981);
    }
    #noBtn {
      background: linear-gradient(135deg, #f87171, #ef4444);
    }
    button:hover {
      transform: translateY(-2px);
      box-shadow: 0 6px 14px rgba(0,0,0,0.15);
    }
    #chartContainer {
      width: 320px;
      margin: 0 auto;
      background: white;
      border-radius: 20px;
      padding: 1rem;
      box-shadow: 0 4px 15px rgba(0,0,0,0.1);
    }
    #thanks {
      display: none;
      font-weight: bold;
      color: #059669;
      margin-top: 1.5rem;
      font-size: 1.1rem;
      animation: fadeIn 0.8s ease;
    }
    @keyframes fadeIn {
      from {opacity: 0; transform: translateY(10px);}
      to {opacity: 1; transform: translateY(0);}
    }
  </style>
</head>
<body>
  <h1>지금까지 수업 내용이 이해되시나요? 🧠</h1>
  <div class="button-container">
    <button id="yesBtn">😊 예</button>
    <button id="noBtn">😕 아니오</button>
  </div>
  <div id="thanks">💖 참여해 주셔서 감사합니다!</div>

  <div id="chartContainer">
    <canvas id="pollChart"></canvas>
  </div>

  <script>
    let yesCount = 0;
    let noCount = 0;

    const ctx = document.getElementById('pollChart');
    const pollChart = new Chart(ctx, {
      type: 'bar',
      data: {
        labels: ['예 😊', '아니오 😕'],
        datasets: [{
          label: '응답 수',
          data: [yesCount, noCount],
          backgroundColor: ['#6ee7b7', '#fca5a5'],
          borderRadius: 10,
          borderWidth: 1,
        }]
      },
      options: {
        scales: {
          y: {
            beginAtZero: true,
            ticks: { stepSize: 1 }
          }
        },
        plugins: {
          legend: { display: false }
        },
        animation: {
          duration: 700,
          easing: 'easeOutBounce'
        }
      }
    });

    const yesBtn = document.getElementById('yesBtn');
    const noBtn = document.getElementById('noBtn');
    const thanks = document.getElementById('thanks');

    function disableButtons() {
      yesBtn.disabled = true;
      noBtn.disabled = true;
      yesBtn.style.opacity = '0.6';
      noBtn.style.opacity = '0.6';
    }

    yesBtn.addEventListener('click', () => {
      yesCount++;
      updateChart();
      disableButtons();
      thanks.style.display = 'block';
    });

    noBtn.addEventListener('click', () => {
      noCount++;
      updateChart();
      disableButtons();
      thanks.style.display = 'block';
    });

    function updateChart() {
      pollChart.data.datasets[0].data = [yesCount, noCount];
      pollChart.update();
    }
  </script>
</body>
</html>
