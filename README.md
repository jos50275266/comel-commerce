# comel-commerce

# TIL

## Error Handling Middleware

```javascript
const express = require("express");
const app = express();
const port = 3000;

// 비동기 함수를 다룰 때는 next 함수를 통해 오류를 처리해야 합니다.
app.get("/a", (req, res, next) => {
  setTimeout(() => {
    try {
      aconsole.log("Asynchronous Code");
    } catch (err) {
      // next가 built-in 오류 미들웨어로 에러를 전달합니다.
      next(err);
    }
  }, 1000);

  // next(new Error("some error occurred"));
});

app.use("/api", apiRoutes);

// /a 라우터를 가진 함수를 호출할 때, next 함수가 더는 존재하지 않아 보이지만
// 실제로는 다음과 같이 Default Middleware가 존재합니다.

// Default
app.use((error, req, res, next) => {
  console.error(error);
  res.status(500).json({
    message: error.message,
    stack: error.stack,
  });
});

app.listen(port, () => {
  console.log(`Listening on port ${port}`);
});
```
