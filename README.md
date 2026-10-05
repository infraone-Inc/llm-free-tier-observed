# LLM free tier observed

What InfraOne Inc. observed in its own production calls to the free tiers of LLM APIs: the kinds of errors returned (rate limits, overloads and others) and whether access came back after the documented reset. This is not official information from the providers.

- Canonical page: https://infraone.jp/data/llm-free-tier/ (Japanese) / https://infraone.jp/en/data/llm-free-tier/ (English)
- Version: 2026-10-05 (updated daily; the window is the last 60 days)
- Providers: Alibaba Cloud Model Studio (Qwen, international / Singapore), Cloudflare Workers AI (free allocation), Google Gemini API (free tier), Groq (free plan), OpenRouter (free models, :free)
- Data: `data/latest.json` (identical to https://infraone.jp/data/llm-free-tier/latest.json) and `data/history/<date>.json`
- License: CC BY 4.0 (https://creativecommons.org/licenses/by/4.0/)

## How to cite

InfraOne Inc. (2026). *LLM free tier observed* (version 2026-10-05). https://infraone.jp/data/llm-free-tier/

See `CITATION.cff`.

## Method

- Source: application error log (status and response body; bodies truncated to 180 chars before 2026-10-02)
- Source: scrubbed full response bodies (from 2026-10-02)
- Source: successful call log (timestamp, provider, model)
- Classification: response body patterns (classify() in engine/freetier.py)
- Reset check: for each documented reset after a daily-limit error, whether our first call within 6 hours after the reset succeeded
- Replicate: call the provider's free tier from one project/account, log every non-2xx response body and every success timestamp with the model name, and compute the same aggregates over the same window

## Caveats

Observed by InfraOne from its own production calls (free tiers; where we use several keys separated by purpose for one provider, they are combined per provider; we do not pool keys to raise free limits); no extra requests were made. Failure counts include our own re-checks while limited, so they depend on our call pattern. Until 2026-10-01 our side paused a provider for hours after a limit, so there are no observations during those pauses.

These are observations, not the providers' terms. The providers' own documentation prevails.

No warranty: the data is provided as is, without warranty of any kind.

---

# LLM 無料枠の観測データ

株式会社インフラワンが自社の業務の呼び出しで観測した、LLM の API の無料枠の失敗の種類 (上限・混雑など) と、公表されたリセットの後に使えたかの記録です。各事業者の公式の情報ではありません。

- 正本: https://infraone.jp/data/llm-free-tier/ (日本語) / https://infraone.jp/en/data/llm-free-tier/ (英語)
- 版: 2026-10-05 (毎日更新。集計の期間は直近 60 日)
- 事業者: Alibaba Cloud Model Studio (Qwen、国際版・シンガポール)、Cloudflare Workers AI (無料枠)、Google Gemini API (無料枠)、Groq (無料の枠)、OpenRouter (無料のモデル :free)
- データ: `data/latest.json` (https://infraone.jp/data/llm-free-tier/latest.json と同じ内容) と `data/history/<日付>.json`
- ライセンス: CC BY 4.0 (https://creativecommons.org/licenses/by/4.0/)

## 引用の仕方

株式会社インフラワン (2026)。『LLM 無料枠の観測データ』(版 2026-10-05)。https://infraone.jp/data/llm-free-tier/

## 注意

当社の観測。当社の業務の呼び出し (無料枠。事業者によっては用途ごとに分けた複数の鍵の記録を事業者ごとに合算。無料の枠を足し合わせる使い方はしていない) の記録から集計し、追加の問い合わせはしていない。失敗の件数には、上限に当たっている間の当社の再確認も含む (件数は当社の呼び出し方に左右される)。2026-10-01 以前は、上限に当たると当社の側で数時間〜24時間止めていたので、その間の観測は無い。

観測であって、各事業者の規約ではありません。各事業者の公式の文書が優先します。

無保証: データは現状のまま提供し、いかなる保証もしません。
