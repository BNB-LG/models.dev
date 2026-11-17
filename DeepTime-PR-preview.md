# feat(providers): add DeepTime with DeepSeek and Qwen models

Add [DeepTime](https://deeptimetoken.com/en/models) as an OpenAI-compatible Chat Completions provider with three public model IDs, API-key configuration (`DEEPTIME_API_KEY`) and a monochrome [provider logo](https://deeptimetoken.com/favicon.fad5d46f940a.svg?v=3). The API base URL is `https://tokenapi.deeptimetoken.com/v1`.

### Models and retail prices

USD per million tokens, checked November 17, 2026. Model links document the request IDs, limits, capabilities and prices.

| Model | Context / max output | Input | Output | Cache read |
| --- | ---: | ---: | ---: | ---: |
| [deepseek-v4.1-flash-1017](https://deeptimetoken.com/en/models/deepseek) · off-peak | 1,000,000 / 384,000 | $0.05958 | $0.2383 | $0.001192 |
| Same model · peak | 1,000,000 / 384,000 | $0.1192 | $0.4766 | $0.002383 |
| [qwen3.8-flash](https://deeptimetoken.com/en/models/qwen?model=hon%3Aqwen3.8-flash) | 1,000,000 / 131,072 | $0.07149 | $0.2413 | $0.008937 |
| [qwen3.8-max](https://deeptimetoken.com/en/models/qwen?model=hon%3Aqwen3.8-max) | 1,000,000 / 131,072 | $1.072 | $3.217 | $0.1341 |

Prices use DeepTime’s published conversion of 6.7138 CNY per USD. DeepSeek peak hours are Monday–Friday, 09:00–12:00 and 14:00–18:00 (UTC+8). DeepTime does not specify a holiday exception. The [console](https://console.deeptimetoken.com/?lang=en&tab=docs) notes that supplier fallback can change the served model and price.

### Capabilities and sources

All three routes list tool calling, structured output and reasoning. The entries reuse the DeepSeek and Alibaba base models. DeepTime lists text, image and video inputs for both Qwen routes, so the Max entry omits the lab’s PDF input.

Reasoning controls follow the documented upstream baselines for [DeepSeek](https://api-docs.deepseek.com/guides/thinking_mode/) and [Qwen](https://www.alibabacloud.com/help/en/model-studio/qwen-api-via-openai-chat-completions). DeepTime’s route docs do not enumerate the individual controls. Pass-through, streaming and tool calls have not been tested with a live DeepTime key.

### Validation

- `bun validate` passed. All three generated entries resolve to the expected OpenCode runtime, endpoint, token limits and retail prices.
- SDK generation and typecheck passed; all 25 SDK tests passed.
- `bun run v1:check` exited 1 for the expected additions: the new provider and its three models. No existing provider or model changed.

---

[Review the five changed files](https://github.com/anomalyco/models.dev/compare/dev...BNB-LG:add-deeptime-provider) · [Open the prefilled pull request form](https://github.com/anomalyco/models.dev/compare/dev...BNB-LG:add-deeptime-provider?expand=1&title=feat%28providers%29%3A%20add%20DeepTime%20with%20DeepSeek%20and%20Qwen%20models&body=Add%20%5BDeepTime%5D%28https%3A%2F%2Fdeeptimetoken.com%2Fen%2Fmodels%29%20as%20an%20OpenAI-compatible%20Chat%20Completions%20provider%20with%20three%20public%20model%20IDs%2C%20API-key%20configuration%20%28%60DEEPTIME_API_KEY%60%29%20and%20a%20monochrome%20%5Bprovider%20logo%5D%28https%3A%2F%2Fdeeptimetoken.com%2Ffavicon.fad5d46f940a.svg%3Fv%3D3%29.%20The%20API%20base%20URL%20is%20%60https%3A%2F%2Ftokenapi.deeptimetoken.com%2Fv1%60.%0A%0A%23%23%23%20Models%20and%20retail%20prices%0A%0AUSD%20per%20million%20tokens%2C%20checked%20November%2017%2C%202026.%20Model%20links%20document%20the%20request%20IDs%2C%20limits%2C%20capabilities%20and%20prices.%0A%0A%7C%20Model%20%7C%20Context%20%2F%20max%20output%20%7C%20Input%20%7C%20Output%20%7C%20Cache%20read%20%7C%0A%7C%20---%20%7C%20---%3A%20%7C%20---%3A%20%7C%20---%3A%20%7C%20---%3A%20%7C%0A%7C%20%5Bdeepseek-v4.1-flash-1017%5D%28https%3A%2F%2Fdeeptimetoken.com%2Fen%2Fmodels%2Fdeepseek%29%20%C2%B7%20off-peak%20%7C%201%2C000%2C000%20%2F%20384%2C000%20%7C%20%240.05958%20%7C%20%240.2383%20%7C%20%240.001192%20%7C%0A%7C%20Same%20model%20%C2%B7%20peak%20%7C%201%2C000%2C000%20%2F%20384%2C000%20%7C%20%240.1192%20%7C%20%240.4766%20%7C%20%240.002383%20%7C%0A%7C%20%5Bqwen3.8-flash%5D%28https%3A%2F%2Fdeeptimetoken.com%2Fen%2Fmodels%2Fqwen%3Fmodel%3Dhon%253Aqwen3.8-flash%29%20%7C%201%2C000%2C000%20%2F%20131%2C072%20%7C%20%240.07149%20%7C%20%240.2413%20%7C%20%240.008937%20%7C%0A%7C%20%5Bqwen3.8-max%5D%28https%3A%2F%2Fdeeptimetoken.com%2Fen%2Fmodels%2Fqwen%3Fmodel%3Dhon%253Aqwen3.8-max%29%20%7C%201%2C000%2C000%20%2F%20131%2C072%20%7C%20%241.072%20%7C%20%243.217%20%7C%20%240.1341%20%7C%0A%0APrices%20use%20DeepTime%E2%80%99s%20published%20conversion%20of%206.7138%20CNY%20per%20USD.%20DeepSeek%20peak%20hours%20are%20Monday%E2%80%93Friday%2C%2009%3A00%E2%80%9312%3A00%20and%2014%3A00%E2%80%9318%3A00%20%28UTC%2B8%29.%20DeepTime%20does%20not%20specify%20a%20holiday%20exception.%20The%20%5Bconsole%5D%28https%3A%2F%2Fconsole.deeptimetoken.com%2F%3Flang%3Den%26tab%3Ddocs%29%20notes%20that%20supplier%20fallback%20can%20change%20the%20served%20model%20and%20price.%0A%0A%23%23%23%20Capabilities%20and%20sources%0A%0AAll%20three%20routes%20list%20tool%20calling%2C%20structured%20output%20and%20reasoning.%20The%20entries%20reuse%20the%20DeepSeek%20and%20Alibaba%20base%20models.%20DeepTime%20lists%20text%2C%20image%20and%20video%20inputs%20for%20both%20Qwen%20routes%2C%20so%20the%20Max%20entry%20omits%20the%20lab%E2%80%99s%20PDF%20input.%0A%0AReasoning%20controls%20follow%20the%20documented%20upstream%20baselines%20for%20%5BDeepSeek%5D%28https%3A%2F%2Fapi-docs.deepseek.com%2Fguides%2Fthinking_mode%2F%29%20and%20%5BQwen%5D%28https%3A%2F%2Fwww.alibabacloud.com%2Fhelp%2Fen%2Fmodel-studio%2Fqwen-api-via-openai-chat-completions%29.%20DeepTime%E2%80%99s%20route%20docs%20do%20not%20enumerate%20the%20individual%20controls.%20Pass-through%2C%20streaming%20and%20tool%20calls%20have%20not%20been%20tested%20with%20a%20live%20DeepTime%20key.%0A%0A%23%23%23%20Validation%0A%0A-%20%60bun%20validate%60%20passed.%20All%20three%20generated%20entries%20resolve%20to%20the%20expected%20OpenCode%20runtime%2C%20endpoint%2C%20token%20limits%20and%20retail%20prices.%0A-%20SDK%20generation%20and%20typecheck%20passed%3B%20all%2025%20SDK%20tests%20passed.%0A-%20%60bun%20run%20v1%3Acheck%60%20exited%201%20for%20the%20expected%20additions%3A%20the%20new%20provider%20and%20its%20three%20models.%20No%20existing%20provider%20or%20model%20changed.)
