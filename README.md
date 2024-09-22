# E-Commerce Shop Backend

## Description

This project is a comprehensive e-commerce platform built with a focus on scalable architecture, robust API design, and efficient handling of business logic. It includes features such as product management, order processing, payment integration, and user authentication. The platform leverages modern technologies to ensure smooth operation and an enhanced user experience.

## Features

### Order Processing and Stock Management

- **Order Creation and Management**
  Supports the creation and management of user orders. Orders are validated for product availability and stock levels are adjusted accordingly. Order details, including delivery methods and discounts, are handled during the order creation process.

- **Stock Management**
  Automatically reduces product stock upon order placement and restores it in case of payment failure. An admin feature for manual stock adjustments is also provided.

- **Order and Payment Status Handling**
  Integrates with Stripe for payment processing. Handles different payment statuses and updates the order status accordingly. Provides real-time user notifications for order updates using SignalR.

### Response Caching and Optimization

- **API Response Caching**
  Implements caching for frequently accessed product endpoints to enhance performance. Supports cache invalidation to ensure data consistency when products are updated or deleted.

- **Cache Management**
  Uses Redis for caching and provides mechanisms to manage cache entries programmatically. This ensures optimal response times and reduces unnecessary load on the database.

### Admin and User Management

- **Admin Features**
  Admins can manage orders, process refunds, and update stock levels. Role-based access control is implemented to restrict admin-specific features to authorized users.

- **Password Reset Functionality**
  Allows users to reset their passwords securely. Admins can also manage user roles and permissions.

### Payment and Discounts

- **Coupon and Discount Support**
  Enables users to apply coupons to their orders. The system calculates discounts in real-time and adjusts the order total accordingly.

- **Stripe Integration**
  Manages payment intents and processes payments using Stripe. Supports full and partial refunds, and handles failed payment scenarios gracefully.

### Product Management and Filtering

- **Product CRUD Operations**
  Provides endpoints for creating, updating, deleting, and retrieving products. Supports brand and type filtering, and search functionality.

- **Pagination and Search**
  Implements pagination and search filtering for product listings to enhance the user experience and ensure efficient data retrieval.

### Shopping Cart Functionality

- **Cart Operations**
  Provides a shopping cart feature with operations to add, update, and remove items. Cart data is stored in Redis for fast retrieval and persistence.

### Error Handling and Security

- **Global Error Handling**
  Implements centralized error handling for consistent and informative API responses. Includes validation and error logging mechanisms.

- **Security and Authentication**
  Utilizes ASP.NET Core Identity for user authentication and authorization. Supports user registration, login, and role-based access control.

#### Technology Stack

- **Backend:** ASP.NET Core, Entity Framework Core
- **Database:** SQL Server, Redis
- **Authentication:** ASP.NET Core Identity
- **Payment Gateway:** Stripe API
- **Caching:** Redis
- **Real-time Communication:** SignalR
- **Containerization:** Docker
- **Other Tools:** AutoMapper, FluentValidation

## Installation

### Prerequisites

- [.NET 8.0 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)
- [Docker](https://www.docker.com/products/docker-desktop) (for running the database and Redis)
- [SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads) (if not using Docker)
- [Redis](https://redis.io/download) (if not using Docker)

### Environment Setup

1. Clone the repository:

   ```bash
   git clone https://github.com/elvan/ecommerce-platform.git
   cd ecommerce-platform
   ```

2. Create an `.env` file in the root directory with the following environment variables:

   ```env
   ConnectionStrings__DefaultConnection=Server=localhost;Database=EcommerceDB;User Id=sa;Password=your_password;
   StripeSettings__SecretKey=your_stripe_secret_key
   StripeSettings__WhSecret=your_stripe_webhook_secret
   ```

3. Install Docker containers for SQL Server and Redis:

   ```bash
   docker-compose up -d
   ```

4. Apply database migrations:

   ```bash
   dotnet ef database update --project Infrastructure
   ```

### Installation Commands

1. Restore dependencies:

   ```bash
   dotnet restore
   ```

2. Build the solution:

   ```bash
   dotnet build
   ```

3. Run the application:

   ```bash
   dotnet run --project API
   ```

## Usage

### Accessing the Application

1. Navigate to `https://localhost:5001` to access the API.

2. Use the following endpoints for key functionalities:

   - **Product Management:**

     - `GET /api/products` - Retrieve the list of products.
     - `POST /api/products` - Create a new product (Admin only).
     - `PUT /api/products/{id}` - Update a product (Admin only).
     - `DELETE /api/products/{id}` - Delete a product (Admin only).

   - **Order Management:**

     - `POST /api/orders` - Create a new order.
     - `GET /api/orders` - Get user-specific orders.

   - **Cart Management:**

     - `POST /api/cart` - Add or update a cart item.
     - `GET /api/cart/{id}` - Retrieve cart details.

   - **Admin Operations:**
     - `POST /api/admin/orders/refund/{id}` - Refund an order (Admin only).

3. Use a tool like Postman to interact with the API and test various functionalities, or integrate it with a frontend application.
