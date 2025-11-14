# Order Execution Engine

## Overview
This project is an Order Execution Engine built using Fastify, TypeScript, PostgreSQL, Redis, and BullMQ.  
It processes market orders on decentralized exchanges (DEX) with intelligent routing, retries, and real-time updates via WebSocket.

## Features
- Supports market order execution between token pairs on DEXs Raydium and Meteora.
- Fetches token swap quotes from multiple DEXs, compares prices, and routes orders for best execution.
- Real-time order status updates through a WebSocket connection.
- Persistence using PostgreSQL and caching for active orders in Redis.
- Robust error handling and graceful shutdown support.
- Designed for high concurrency with BullMQ to queue and process orders.

## How It Works
1. **Order Submission**: Client submits a market order specifying input and output tokens and amount.
2. **DEX Routing**: System fetches quotes from both Raydium and Meteora pools and selects the best price.
3. **Order Execution**: Submits order to selected DEX (mocked execution).
4. **Status Updates**: Sends WebSocket messages for every execution stage: pending, routing, building, submitted, confirmed.
5. **Order Persistence**: Stores order details in PostgreSQL and caches active orders in Redis.

## API Endpoints
### REST endpoints
- `GET /health`: System health status.
- `GET /api/orders`: List all orders with pagination.
- `GET /api/orders/:orderId`: Fetch specific order details.

### WebSocket endpoint
- `GET /api/orders/execute`: Upgrade to WebSocket for submitting orders and receiving live status updates.

## How to Run
1. Clone repository and install dependencies:
npm install

text
2. Setup environment variables (see `.env.example`):
- `DATABASE_URL`
- `REDIS_HOST`
- `PORT` (optional)

3. Start server:
npm run dev

text

4. Use WebSocket client to execute orders and receive real-time status.

## How to Extend
- Support additional order types (limit, sniper).
- Add support for more DEXs for routing.
- Integrate with live Solana Devnet instead of mocks.
- Add authentication and user management.

## Why Market Order
Market orders ensure immediate execution at current best price, suitable for a real-time DEX environment.  
This engine can be extended to add limit and sniper orders with slight changes to order matching logic and status flows.

## License
This project is for demonstration and educational purposes.
