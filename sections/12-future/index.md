---
title: Future work
has_children: false
nav_order: 13
---

# Known issues and future work

This section summarizes current limitations of Popcorn Meter and realistic next steps for improvement.

## What is missing or limited

- Recommendation depth: recommendations are currently heuristic-based (genres, watched history, feedback, and metadata signals), not model-based or collaborative.
- Streaming availability quality: streaming links are generic search links, not real-time provider availability by country.
- Account management scope: signup/login is available, but features like password reset, email verification, and profile editing are limited.
- Data portability: there is no export/import feature for watchlist, watched history, or feedback.
- Multi-device support: persistence is local SQLite-based; cloud synchronization between devices is not implemented.

## What does not work as it should (or needs improvement)

- External API dependency: OMDb/TMDb failures, rate limits, or missing keys can degrade search/trending/recommendation quality.
- Error transparency: some failures are intentionally shown as generic UI messages; troubleshooting can require checking logs.
- Hosted demo persistence: on Streamlit Cloud, storage can be ephemeral, so user data may not persist reliably across restarts/redeploys.
- UI test coverage: backend and service logic are tested well, but end-to-end UI behavior is still comparatively less covered.
- Runtime robustness: deployment/runtime differences (local vs cloud) can require extra packaging/path care.

## Potential future developments

- Improve recommendations with hybrid ranking (content + collaborative signals) and better explanation of why a movie is suggested.
- Integrate real provider APIs for accurate "where to watch" by region and subscription service.
- Add account enhancements: password reset, profile editing, optional OAuth login.
- Add data export/import (CSV/JSON) and optional cloud persistence layer.
- Expand analytics: personalized insights, trend dashboards, and recommendation quality feedback loops.
- Strengthen operational quality: better observability, retries/caching for API calls, and broader UI integration tests.
