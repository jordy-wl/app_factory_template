# Law Book: Stripe Integration & Revenue Readiness Protocols

> This document is the primary authority for all payment and subscription logic. Monetization integrity is critical; all agents must follow these rules to ensure secure, reliable, and user-aligned revenue operations.

## 1. Stripe Architecture (The Handshake)
* **Server-Side Execution**: All Stripe Secret Keys and sensitive API calls MUST remain within the `src/backend/` environment. Never expose secret keys to the frontend.
* **Webhook Mandate**: Every revenue-ready app MUST implement a secure `/api/v1/webhooks/stripe` endpoint in FastAPI to handle critical events: `checkout.session.completed`, `customer.subscription.updated`, and `customer.subscription.deleted`.
* **Webhook Security**: Agents MUST utilize `stripe.Webhook.construct_event` with the `STRIPE_WEBHOOK_SECRET` to verify event signatures and prevent spoofing.

## 2. Subscription & Data Models
* **Structured Tiers**: Use Pydantic enums to define subscription tiers (e.g., `BASIC`, `PRO`, `ENTERPRISE`) and billing statuses (e.g., `ACTIVE`, `PAST_DUE`, `CANCELED`) in `models.py`.
* **Supabase Synchronization**: The `subscriptions` table in Supabase MUST be the source of truth for user access levels. RLS policies must ensure `(auth.uid() = user_id)` for all billing data.
* **Idempotency**: Use Stripe's `idempotency_key` for any request that modifies a customer's financial state to prevent duplicate charges during network retries.

## 3. Frontend Checkout Protocols (React 19)
* **Action-Driven Checkout**: Use React 19 `useActionState` to handle the transition to Stripe Checkout. This provides immediate "Pending" feedback to the user while the backend generates the session URL.
* **Success/Cancel Routes**: Every implementation MUST define clear `/checkout/success` and `/checkout/cancel` routes in the App Router to handle user returns gracefully.

## 4. Documentation & Context Links
* **Stripe API Reference**: https://stripe.com/docs/api
* **Subscription Lifecycle**: https://stripe.com/docs/billing/subscriptions/overview
* **Webhook Handling**: https://stripe.com/docs/webhooks

## 5. Anti-Patterns
* ❌ **Hardcoded Price IDs**: Never hardcode Stripe Price or Product IDs. Use environment variables (e.g., `STRIPE_PRO_PRICE_ID`).
* ❌ **Polling for Status**: Do not poll the database for subscription updates. Rely on Webhooks for asynchronous, reliable state synchronization.
* ❌ **Frontend API Calls**: Forbidden to call `stripe.checkout.sessions.create` directly from the browser. This must be a secure Backend-to-Backend call.