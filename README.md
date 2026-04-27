<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>旧土豆的小网页</title>
<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:system-ui,sans-serif}
body{background:#f2f2f2;color:#333}
.page{display:none;padding:20px 0 100px;height:100vh;overflow:auto}
.page.active{display:block}
.main-content{text-align:center;padding:60px 20px}
.main-content h1{font-size:28px;margin-bottom:12px}
.main-content a{color:#0066ff;text-decoration:underline}
.description{font-size:16px;color:#666;margin-bottom:40px}
.buttons{display:flex;flex-direction:column;gap:16px;max-width:400px;margin:0 auto}
.buttons button{padding:18px 0;border:none;border-radius:12px;background:#4caf50;color:white;font-size:18px}
.footer{text-align:center;margin-top:60px;padding:20px;color:#666}
.footer a{color:#4caf50}
.scroll-container{padding:20px}
h1{text-align:center;margin-bottom:24px;font-size: