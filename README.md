<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    canvas {
      border: 1px solid #000;
    }
  </style>
  <title>Bouncing Ball with Callback</title>
</head>
<body>
  <canvas id="bouncingBallCanvas" width="400" height="200"></canvas>

  <script>
    const canvas = document.getElementById('bouncingBallCanvas');
    const ctx = canvas.getContext('2d');

    const ball = {
      x: 50,
      y: 50,
      radius: 20,
      color: '#0095DD',
      dx: 2,
      dy: 2,
    };

    function drawBall() {
      ctx.beginPath();
      ctx.arc(ball.x, ball.y, ball.radius, 0, Math.PI * 2);
      ctx.fillStyle = ball.color;
      ctx.fill();
      ctx.closePath();
    }

    function updateBallPosition(callback) {
      // Check boundaries and reverse direction if necessary
      if (ball.x + ball.dx > canvas.width - ball.radius || ball.x + ball.dx < ball.radius) {
        ball.dx = -ball.dx;
        callback('horizontal');
      }

      if (ball.y + ball.dy > canvas.height - ball.radius || ball.y + ball.dy < ball.radius) {
        ball.dy = -ball.dy;
        callback('vertical');
      }

      // Update ball position
      ball.x += ball.dx;
      ball.y += ball.dy;
    }

    function draw() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);

      drawBall();
      updateBallPosition(handleBounce);
      requestAnimationFrame(draw);
    }

    function handleBounce(direction) {
      console.log(`Bounce in ${direction} direction!`);
      // You can perform additional actions here when the ball bounces, based on the direction.
    }

    draw();
  </script>
</body>
</html>
