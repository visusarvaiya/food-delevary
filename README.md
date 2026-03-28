# food-delivery

A food delivery website project involves creating an online platform where users can browse through various restaurants, select items from their menus, place orders, make payments, and have the food delivered to their location. The website typically includes features like user registration and login, restaurant listings, menu displays, cart functionality, order tracking, payment gateways, and customer reviews. It requires designing user-friendly interfaces, integrating databases for storing menu items and user information, implementing secure payment methods, and setting up a system for managing orders and deliveries efficiently. Overall, the goal is to provide a convenient and seamless online food ordering experience for customers.



# Food Delivery Backend API

A comprehensive Node.js backend for a food delivery platform with features like user authentication, restaurant management, menu items, cart functionality, order processing, and payment integration.

## Features

- **User Management**
  - User registration and login with JWT authentication
  - Role-based access control (Customer, Restaurant Owner, Delivery Person, Admin)
  - Profile management with multiple delivery addresses
  - Password change functionality

- **Restaurant Management**
  - CRUD operations for restaurants
  - Restaurant search and filtering
  - Opening hours and delivery information
  - Rating and review system

- **Menu Management**
  - Menu items with categories and customizations
  - Dietary filters (Vegetarian, Vegan, Gluten-free)
  - Item availability management
  - Nutritional information

- **Shopping Cart**
  - Add/update/remove items
  - Restaurant-specific cart validation
  - Customization support

- **Order Management**
  - Order placement and tracking
  - Status updates (pending, confirmed, preparing, delivered, etc.)
  - Order history
  - Cancellation support

- **Payment Processing**
  - Multiple payment methods (Card, UPI, Wallet, Cash on Delivery)
  - Payment verification
  - Refund processing

- **Reviews & Ratings**
  - Customer reviews with ratings
  - Restaurant responses
  - Rating aggregation

## Tech Stack

- **Runtime:** Node.js
- **Framework:** Express.js
- **Database:** MongoDB with Mongoose ODM
- **Authentication:** JWT (JSON Web Tokens)
- **Password Hashing:** bcryptjs
- **Environment Variables:** dotenv

## Project Structure

```
food-delivery-backend/
├── models/
│   ├── User.js
│   ├── Restaurant.js
│   ├── MenuItem.js
│   ├── Order.js
│   └── Review.js
├── routes/
│   ├── auth.js
│   ├── users.js
│   ├── restaurants.js
│   ├── menu.js
│   ├── orders.js
│   ├── cart.js
│   ├── reviews.js
│   └── payment.js
├── middleware/
│   └── auth.js
├── server.js
├── package.json
└── .env
```

## Installation

1. **Clone the repository**
```bash
git clone <repository-url>
cd food-delivery-backend
```

2. **Install dependencies**
```bash
npm install
```

3. **Set up environment variables**
```bash
cp .env.example .env
```

Edit `.env` file with your configuration:
- MongoDB connection string
- JWT secret key
- Payment gateway credentials
- Other configuration

4. **Start MongoDB**
Make sure MongoDB is running on your system or use MongoDB Atlas.

5. **Run the server**

Development mode:
```bash
npm run dev
```

Production mode:
```bash
npm start
```

The server will start on `http://localhost:5000`

## API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `GET /api/auth/me` - Get current user

### Users
- `GET /api/users/profile` - Get user profile
- `PUT /api/users/profile` - Update profile
- `POST /api/users/address` - Add address
- `PUT /api/users/address/:addressId` - Update address
- `DELETE /api/users/address/:addressId` - Delete address
- `PUT /api/users/change-password` - Change password

### Restaurants
- `GET /api/restaurants` - Get all restaurants
- `GET /api/restaurants/:id` - Get single restaurant
- `POST /api/restaurants` - Create restaurant (Owner/Admin)
- `PUT /api/restaurants/:id` - Update restaurant (Owner/Admin)
- `DELETE /api/restaurants/:id` - Delete restaurant (Owner/Admin)

### Menu
- `GET /api/menu/restaurant/:restaurantId` - Get restaurant menu
- `GET /api/menu/:id` - Get single menu item
- `POST /api/menu` - Create menu item (Owner/Admin)
- `PUT /api/menu/:id` - Update menu item (Owner/Admin)
- `DELETE /api/menu/:id` - Delete menu item (Owner/Admin)

### Cart
- `GET /api/cart` - Get user's cart
- `POST /api/cart/add` - Add item to cart
- `PUT /api/cart/update` - Update cart item
- `DELETE /api/cart/remove/:menuItemId` - Remove item
- `DELETE /api/cart/clear` - Clear cart

### Orders
- `POST /api/orders` - Create order
- `GET /api/orders` - Get all orders (filtered by role)
- `GET /api/orders/:id` - Get single order
- `PUT /api/orders/:id/status` - Update order status
- `PUT /api/orders/:id/cancel` - Cancel order
- `PUT /api/orders/:id/assign-delivery` - Assign delivery person (Admin)

### Reviews
- `POST /api/reviews` - Create review
- `GET /api/reviews/restaurant/:restaurantId` - Get restaurant reviews
- `PUT /api/reviews/:id/response` - Add restaurant response

### Payment
- `POST /api/payment/process` - Process payment
- `POST /api/payment/verify` - Verify payment
- `POST /api/payment/refund` - Process refund (Admin)

## Authentication

Most endpoints require authentication. Include JWT token in the Authorization header:

```
Authorization: Bearer <your_jwt_token>
```

## User Roles

- **customer** - Can browse, order, and review
- **restaurant_owner** - Can manage their restaurants and menus
- **delivery_person** - Can view and update assigned deliveries
- **admin** - Full access to all resources

## Example Usage

### Register a User
```bash
curl -X POST http://localhost:5000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "name": "John Doe",
    "email": "john@example.com",
    "password": "password123",
    "phone": "+1234567890"
  }'
```

### Create a Restaurant
```bash
curl -X POST http://localhost:5000/api/restaurants \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <token>" \
  -d '{
    "name": "Amazing Restaurant",
    "description": "Best food in town",
    "cuisineType": ["Italian", "Pizza"],
    "address": {
      "street": "123 Main St",
      "city": "New York",
      "state": "NY",
      "zipCode": "10001"
    },
    "phone": "+1234567890",
    "email": "restaurant@example.com"
  }'
```

## Error Handling

The API returns appropriate HTTP status codes:
- `200` - Success
- `201` - Created
- `400` - Bad Request
- `401` - Unauthorized
- `403` - Forbidden
- `404` - Not Found
- `500` - Server Error

Error response format:
```json
{
  "success": false,
  "message": "Error message here"
}
```

## Future Enhancements

- Real-time order tracking with WebSockets
- Push notifications
- Advanced search with Elasticsearch
- Image upload functionality
- Analytics dashboard
- Promo codes and discounts
- Loyalty program
- Multi-language support
- Rate limiting
- API documentation with Swagger

## License

ISC

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.
