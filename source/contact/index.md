---
title:  联系我们
layout: page
---

<form action="https://formspree.io/f/mjkrnqpg" method="POST">
  
  <div class="form-group">
    <label for="email">您的邮箱 <span class="required">*</span></label>
    <input type="email" id="email" name="_replyto" placeholder="请输入您的电子邮箱" required>
  </div>
  
  <div class="form-group">
    <label for="message">留言内容 <span class="required">*</span></label>
    <textarea id="message" name="message" placeholder="请输入您的留言内容..." required></textarea>
  </div>
  
  <!-- 隐藏字段 -->
  <input type="hidden" name="_language" value="zh-CN">
  <input type="hidden" name="_next" value="/thank-you">
  
  <button type="submit">发送消息</button>
  
  <div class="form-footer">
    <p>我们会在24小时内回复您的消息</p>
  </div>
</form>
