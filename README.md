# Email Guard

用 Gemini(or other ai) 给陌生邮件分类（辱骂 / 阴阳怪气 / 打扰 / 正常），可疑邮件自动打标签隔离。

Use Gemini(or other ai) put strange emails into many recycle bins or inbox(insult/distrub/sarcastic or mocking messages/normal),suspect emails automatic get ticks.

## 使用方法 useing method

1. `pip install -r requirements.txt`
2. 复制 `.env.example` 为 `.env`，填入你的 Gemini API Key
3. copy `.env.example` as `.env`，input your Gemini API Key.
4. 在 Google Cloud 启用 Gmail API，下载 `credentials.json` 放到本目录
5. start Gmail API on Google Cloud ，download `credentials.json` in this work space.
6. 运行 `python check_email.py`，首次会弹浏览器授权
7. run `python check_email.py`，the first should give auth..

## 流程 / How it works:

1. 熟人白名单（你发过邮件的人 + whitelist.txt）直接放行，不过 AI

   Friends list (people you've emailed + whitelist.txt) walk right in. No AI needed.

2. 验证码 / noreply 自动邮件：打标签、移出收件箱，不过 AI

   Verification codes / noreply robots: labeled and shoved out of the inbox, no AI needed.

   订阅 / 推广邮件（有退订头且 Gmail 验证 DMARC 通过，或 Gmail 归到推广/社交/论坛）：留在收件箱不动，不过 AI

   Newsletters / promos (unsubscribe header + Gmail says DMARC passed, or Gmail put it in Promotions/Social/Forums): left alone in the inbox, no AI needed.

3. 陌生邮件超过 BOMB_THRESHOLD 封：判定为被轰炸，整批进待审，不逐封调 AI

   Too many strangers at once = you're being bombed. Whole batch goes to review, AI wallet stays closed.

4. 其余陌生邮件交给 AI 三分类：辱骂 / 阴阳怪气 / 正常

   The remaining strangers get a 3-way verdict from the AI: insulting / sarcastic / normal.

- AI 接口是 OpenAI 兼容格式：Gemini / OpenAI / DeepSeek / Ollama 本地模型都能用，改 .env 就行

  The AI side speaks the OpenAI-compatible format: Gemini / OpenAI / DeepSeek / local Ollama all work, just edit .env.

## 用法 / Usage:

```bash
python check_email.py --dry-run
```
试运行：只打印，不动邮箱 / dry run: print only mailbox untouched

```bash
python check_email.py
```
正式运行 / the real thing

```bash
python check_email.py --days 7
```
检查最近 7 天（默认 3 天） / check the last 7 days(default3)

## 管理多个邮箱

```bash
python check_email.py --account work personal
```
给用户授权 / give large amount of users this app

```bash
python check_email.py --account work personal
```
一次性处理多个用户 / handle many usersssss in once running.

```bash
python check_email.py --account work personal --days 7
```
处理多个用户最近 7 天的邮件 / check the last 7 days of many users

## 可选设置 / Optional settings (.env)

- `BOMB_THRESHOLD`（默认 30）、`BOMB_WINDOW_MIN`（默认 60）：`BOMB_WINDOW_MIN` 分钟内陌生邮件超过 `BOMB_THRESHOLD` 封才算轰炸

  `BOMB_THRESHOLD` (default 30), `BOMB_WINDOW_MIN` (default 60): only more than `BOMB_THRESHOLD` strangers inside `BOMB_WINDOW_MIN` minutes counts as bombing

- `AI_DELAY`（默认 4）：两次 AI 调用间隔秒数 / seconds between AI calls

## 测试 / Tests

离线测试，用假的 Gmail 和假的 AI，不需要账号或 Key / offline tests with a fake Gmail and fake AI, no account or key needed:

```bash
python -m unittest discover -s tests -v
```

## 注意 firendly remind:

- 免费版 Gemini API 的内容可能被用于改进 Google 产品，请勿处理敏感邮件
- free-labor Gemini API 's content may improve their Google product，keep your emails private(if you received suspect emails.)

## 彩蛋(来自Claude和ChatGPT)：

Claude：致谢位置我给你留好了，具体用哪句你自己挑 😏

ChatGPT：项目致谢可以写：

- ' 特别感谢一次匿名的网络互动，它为该安全模块提供了灵感。'

哈哈哈哈哈哈哈哈。

## Easter egg (from Claude and ChatGPT):

Claude:I’ve left a spot for your acknowledgments—feel free to pick whichever phrasing you like best! 😏

ChatGPT: For project acknowledgments, you could write:

- Special thanks to an anonymous internet interaction that inspired the security module.

LOLLLLLLLLLLLLLLLLLLLLLLLLLLLLLLLLLLLLLL

# 所以致谢

虽然你提供的内容无效，但你带来的灵感很有价值。

# so the Acknowledgements

Your input was invalid, but your inspiration was valid.