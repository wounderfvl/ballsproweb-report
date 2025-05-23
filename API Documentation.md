# Borneo Anfield Loyalty System
# API Documentation
 
## Overview

API for booking futsal stadiums with loyalty program features. Supports three user roles: Customer, Admin, and Super Admin.

## Base URL

```plaintext
https://api.balls.com/v1
```

## Authentication

Most endpoints require authentication using JWT token.

## User Management

### Register

**Endpoint**

```plaintext
/auth/register
```

**Method**

```plaintext
POST
```

**Request Body**

- `username` as string, must be unique
- `email` as string, must be unique
- `password` as string, must be at least 8 characters
- `full_name` as string
- `phone_number` as string


**Response**

```json
{
  "error": false,
  "message": "User registered successfully",
  "data": {
    "user_id": "user-123abc",
    "username": "johndoe"
  }
}
```

### Login

**Endpoint**

```plaintext
/auth/login
```

**Method**

```plaintext
POST
```

**Request Body**

- `email` as string
- `password` as string


**Response**

```json
{
  "error": false,
  "message": "Login successful",
  "data": {
    "user_id": "user-123abc",
    "username": "johndoe",
    "full_name": "John Doe",
    "user_type": "customer",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
  }
}
```

### Get User Profile

**Endpoint**

```plaintext
/users/profile
```

**Method**

```plaintext
GET
```

**Headers**

- `Authorization: Bearer <token>`


**Response**

```json
{
  "error": false,
  "message": "Profile retrieved successfully",
  "data": {
    "user_id": "user-123abc",
    "username": "johndoe",
    "email": "john@example.com",
    "full_name": "John Doe",
    "phone_number": "1234567890",
    "user_type": "customer",
    "created_at": "2023-01-01T00:00:00.000Z",
    "is_active": true
  }
}
```

### Update User Profile

**Endpoint**

```plaintext
/users/profile
```

**Method**

```plaintext
PUT
```

**Headers**

- `Authorization: Bearer <token>`


**Request Body**

- `full_name` as string, optional
- `phone_number` as string, optional
- `password` as string, optional, must be at least 8 characters


**Response**

```json
{
  "error": false,
  "message": "Profile updated successfully"
}
```

# Checkpoint - 1` Register, Login, Profil CRUD
------------------------------------------------------------------------------------------------------------------------------------
## Field Management

### Get All Fields

**Endpoint**

```plaintext
/fields
```

**Method**

```plaintext
GET
```

**Parameters**

- `available` as boolean, optional (filter by availability)
- `type` as string, optional (filter by field type)
- `page` as integer, optional (default: 1)
- `limit` as integer, optional (default: 10)


**Response**

```json
{
  "error": false,
  "message": "Fields retrieved successfully",
  "data": {
    "fields": [
      {
        "field_id": "field-123abc",
        "field_name": "Field A",
        "description": "Standard futsal field with artificial grass",
        "capacity": 10,
        "hoEndpointy_rate": 150000,
        "field_type": "indoor",
        "is_available": true,
        "images": [
          {
            "image_id": "img-123",
            "image_Endpoint": "https://example.com/images/field-a.jpg",
            "is_primary": true
          }
        ]
      }
    ],
    "pagination": {
      "total_items": 15,
      "total_pages": 2,
      "current_page": 1,
      "per_page": 10
    }
  }
}
```

### Get Field Detail

**Endpoint**

```plaintext
/fields/:field_id
```

**Method**

```plaintext
GET
```

**Response**

```json
{
  "error": false,
  "message": "Field retrieved successfully",
  "data": {
    "field_id": "field-123abc",
    "field_name": "Field A",
    "description": "Standard futsal field with artificial grass",
    "capacity": 10,
    "hoEndpointy_rate": 150000,
    "field_type": "indoor",
    "is_available": true,
    "images": [
      {
        "image_id": "img-123",
        "image_Endpoint": "https://example.com/images/field-a.jpg",
        "is_primary": true
      },
      {
        "image_id": "img-124",
        "image_Endpoint": "https://example.com/images/field-a-2.jpg",
        "is_primary": false
      }
    ],
    "created_at": "2023-01-01T00:00:00.000Z",
    "updated_at": "2023-01-01T00:00:00.000Z"
  }
}
```

### Add New Field (Admin Only)

**Endpoint**

```plaintext
/fields
```

**Method**

```plaintext
POST
```

**Headers**

- `Content-Type: multipart/form-data`
- `Authorization: Bearer <token>`


**Request Body**

- `field_name` as string
- `description` as string, optional
- `capacity` as integer
- `hoEndpointy_rate` as decimal
- `field_type` as string
- `images` as files, optional, multiple files allowed


**Response**

```json
{
  "error": false,
  "message": "Field added successfully",
  "data": {
    "field_id": "field-123abc"
  }
}
```

### Update Field (Admin Only)

**Endpoint**

```plaintext
/fields/:field_id
```

**Method**

```plaintext
PUT
```

**Headers**

- `Content-Type: multipart/form-data`
- `Authorization: Bearer <token>`


**Request Body**

- `field_name` as string, optional
- `description` as string, optional
- `capacity` as integer, optional
- `hoEndpointy_rate` as decimal, optional
- `field_type` as string, optional
- `is_available` as boolean, optional
- `images` as files, optional, multiple files allowed


**Response**

```json
{
  "error": false,
  "message": "Field updated successfully"
}
```

### Delete Field (Admin Only)

**Endpoint**

```plaintext
/fields/:field_id
```

**Method**

```plaintext
DELETE
```

**Headers**

- `Authorization: Bearer <token>`


**Response**

```json
{
  "error": false,
  "message": "Field deleted successfully"
}
```

## Booking Management

### Check Field Availability

**Endpoint**

```plaintext
/fields/:field_id/availability
```

**Method**

```plaintext
GET
```

**Parameters**

- `date` as string (YYYY-MM-DD format)


**Response**

```json
{
  "error": false,
  "message": "Availability retrieved successfully",
  "data": {
    "field_id": "field-123abc",
    "field_name": "Field A",
    "date": "2023-06-15",
    "available_slots": [
      {
        "start_time": "08:00:00",
        "end_time": "09:00:00"
      },
      {
        "start_time": "09:00:00",
        "end_time": "10:00:00"
      }
    ],
    "booked_slots": [
      {
        "start_time": "10:00:00",
        "end_time": "12:00:00"
      }
    ]
  }
}
```

### Create Booking

**Endpoint**

```plaintext
/bookings
```

**Method**

```plaintext
POST
```

**Headers**

- `Authorization: Bearer <token>`
- `Content-Type: application/json`


**Request Body**

- `field_id` as string
- `booking_date` as string (YYYY-MM-DD format)
- `start_time` as string (HH:MM:SS format)
- `end_time` as string (HH:MM:SS format)
- `notes` as string, optional


**Response**

```json
{
  "error": false,
  "message": "Booking created successfully",
  "data": {
    "booking_id": "booking-123abc",
    "total_amount": 300000,
    "duration_hours": 2,
    "payment_methods": [
      {
        "method_id": 1,
        "method_name": "credit_card"
      },
      {
        "method_id": 2,
        "method_name": "bank_transfer"
      }
    ]
  }
}
```

### Get User Bookings

**Endpoint**

```plaintext
/bookings
```

**Method**

```plaintext
GET
```

**Headers**

- `Authorization: Bearer <token>`


**Parameters**

- `status` as string, optional (filter by booking status)
- `from_date` as string (YYYY-MM-DD format), optional
- `to_date` as string (YYYY-MM-DD format), optional
- `page` as integer, optional (default: 1)
- `limit` as integer, optional (default: 10)


**Response**

```json
{
  "error": false,
  "message": "Bookings retrieved successfully",
  "data": {
    "bookings": [
      {
        "booking_id": "booking-123abc",
        "field_id": "field-123abc",
        "field_name": "Field A",
        "booking_date": "2023-06-15",
        "start_time": "10:00:00",
        "end_time": "12:00:00",
        "duration_hours": 2,
        "total_amount": 300000,
        "booking_status": "confirmed",
        "payment_status": "completed",
        "created_at": "2023-06-10T00:00:00.000Z"
      }
    ],
    "pagination": {
      "total_items": 5,
      "total_pages": 1,
      "current_page": 1,
      "per_page": 10
    }
  }
}
```

### Get Booking Detail

**Endpoint**

```plaintext
/bookings/:booking_id
```

**Method**

```plaintext
GET
```

**Headers**

- `Authorization: Bearer <token>`


**Response**

```json
{
  "error": false,
  "message": "Booking retrieved successfully",
  "data": {
    "booking_id": "booking-123abc",
    "user": {
      "user_id": "user-123abc",
      "full_name": "John Doe",
      "phone_number": "1234567890"
    },
    "field": {
      "field_id": "field-123abc",
      "field_name": "Field A",
      "image_Endpoint": "https://example.com/images/field-a.jpg"
    },
    "booking_date": "2023-06-15",
    "start_time": "10:00:00",
    "end_time": "12:00:00",
    "duration_hours": 2,
    "total_amount": 300000,
    "booking_status": "confirmed",
    "notes": "Please prepare water",
    "payment": {
      "payment_id": "payment-123abc",
      "method": "bank_transfer",
      "status": "completed",
      "payment_date": "2023-06-10T12:30:00.000Z"
    },
    "points_earned": 30,
    "created_at": "2023-06-10T00:00:00.000Z",
    "updated_at": "2023-06-10T12:30:00.000Z"
  }
}
```

### Cancel Booking

**Endpoint**

```plaintext
/bookings/:booking_id/cancel
```

**Method**

```plaintext
PUT
```

**Headers**

- `Authorization: Bearer <token>`


**Response**

```json
{
  "error": false,
  "message": "Booking cancelled successfully",
  "data": {
    "booking_id": "booking-123abc",
    "refund_status": "processing",
    "refund_amount": 270000
  }
}
```

### Get All Bookings (Admin Only)

**Endpoint**

```plaintext
/admin/bookings
```

**Method**

```plaintext
GET
```

**Headers**

- `Authorization: Bearer <token>`


**Parameters**

- `status` as string, optional (filter by booking status)
- `field_id` as string, optional
- `user_id` as string, optional
- `from_date` as string (YYYY-MM-DD format), optional
- `to_date` as string (YYYY-MM-DD format), optional
- `page` as integer, optional (default: 1)
- `limit` as integer, optional (default: 10)


**Response**

```json
{
  "error": false,
  "message": "Bookings retrieved successfully",
  "data": {
    "bookings": [
      {
        "booking_id": "booking-123abc",
        "user": {
          "user_id": "user-123abc",
          "full_name": "John Doe"
        },
        "field": {
          "field_id": "field-123abc",
          "field_name": "Field A"
        },
        "booking_date": "2023-06-15",
        "start_time": "10:00:00",
        "end_time": "12:00:00",
        "total_amount": 300000,
        "booking_status": "confirmed",
        "payment_status": "completed",
        "created_at": "2023-06-10T00:00:00.000Z"
      }
    ],
    "pagination": {
      "total_items": 25,
      "total_pages": 3,
      "current_page": 1,
      "per_page": 10
    }
  }
}
```

### Update Booking Status (Admin Only)

**Endpoint**

```plaintext
/admin/bookings/:booking_id/status
```

**Method**

```plaintext
PUT
```

**Headers**

- `Authorization: Bearer <token>`
- `Content-Type: application/json`


**Request Body**

- `booking_status` as string (pending, confirmed, completed, cancelled)
- `notes` as string, optional


**Response**

```json
{
  "error": false,
  "message": "Booking status updated successfully"
}
```

# Checkpoint - 2`  -  Booking CRUD, Fields CRUD, and Integration with User
## Payment Management

### Create Payment

**Endpoint**

```plaintext
/payments
```

**Method**

```plaintext
POST
```

**Headers**

- `Authorization: Bearer <token>`
- `Content-Type: application/json`


**Request Body**

- `booking_id` as string
- `method_id` as integer
- `amount` as decimal
- `transaction_id` as string, optional (for online payments)


**Response**

```json
{
  "error": false,
  "message": "Payment created successfully",
  "data": {
    "payment_id": "payment-123abc",
    "status": "pending",
    "verification_required": true
  }
}
```

### Get Payment Detail

**Endpoint**

```plaintext
/payments/:payment_id
```
```plaintext
admin/payments/:payment_id
```

**Method**

```plaintext
GET
```

**Headers**

- `Authorization: Bearer <token>`


**Response**

```json
{
  "error": false,
  "message": "Payment retrieved successfully",
  "data": {
    "payment_id": "payment-123abc",
    "booking_id": "booking-123abc",
    "amount": 300000,
    "method": "bank_transfer",
    "status": "completed",
    "transaction_id": "BT12345678",
    "payment_date": "2023-06-10T12:30:00.000Z",
    "notes": "Payment verified"
  }
}
```

### Verify Payment (Admin Only)

**Endpoint**

```plaintext
/admin/payments/:payment_id/verify
```

**Method**

```plaintext
PUT
```

**Headers**

- `Authorization: Bearer <token>`
- `Content-Type: application/json`


**Request Body**

- `status_id` as integer (2 for completed, 3 for failed)
- `notes` as string, optional


**Response**

```json
{
  "error": false,
  "message": "Payment verified successfully"
}
```

### Get All Payment (Admin Only)

**Endpoint**

```plaintext
/admin/payments
```

**Method**

```plaintext
GET
```

**Response**

```json
{
  "error": false,
  "message": "Payments generated successfully",
  "data": {
    "period": {
      "from_date": "2023-06-01",
      "to_date": "2023-06-30"
    },
    "total_revenue": 6750000,
    "payment": [
      {
        "method_name": "bank_transfer",
        "count": 30,
        "amount": 4500000,
        "payment_id": "payment-123abc",
        "booking_id": "booking-123abc",
        "status": "completed",
        "transaction_id": "BT12345678",
        "payment_date": "2023-06-10T12:30:00.000Z",
        "notes": "Payment verified"
      },
      {
        "method_name": "credit_card",
        "count": 15,
        "amount": 2250000,
        "payment_id": "payment-123abc",
        "booking_id": "booking-123abc",
        "status": "completed",
        "transaction_id": "BT12345678",
        "payment_date": "2023-06-10T12:30:00.000Z",
        "notes": "Payment verified"
      }
    ],
  }
}
```

### Get Payment Methods

**Endpoint**

```plaintext
/payment-methods
```

**Method**

```plaintext
GET
```

**Response**

```json
{
  "error": false,
  "message": "Payment methods retrieved successfully",
  "data": [
    {
      "method_id": 1,
      "method_name": "credit_card"
    },
    {
      "method_id": 2,
      "method_name": "bank_transfer"
    },
    {
      "method_id": 3,
      "method_name": "cash"
    },
    {
      "method_id": 4,
      "method_name": "e_wallet"
    }
  ]
}
```
# Checkpoint - 3` - Payment
## Loyalty Program Management

### Get User Points

**Endpoint**

```plaintext
/loyalty/points
```

**Method**

```plaintext
GET
```

**Headers**

- `Authorization: Bearer <token>`


**Response**

```json
{
  "error": false,
  "message": "Points retrieved successfully",
  "data": {
    "total_points": 150,
    "active_points": 120,
    "used_points": 30,
    "expired_points": 0,
    "points_history": [
      {
        "point_id": "point-123abc",
        "points_earned": 30,
        "source": "booking",
        "reference": "booking-123abc",
        "earned_date": "2023-06-10T12:30:00.000Z",
        "expiry_date": "2024-06-10T00:00:00.000Z",
        "is_used": false
      }
    ]
  }
}
```

### Get Available Loyalty Programs

**Endpoint**

```plaintext
/loyalty/programs
```
```plaintext
/admin/loyalty/programs
```

**Method**

```plaintext
GET
```

**Headers**

- `Authorization: Bearer <token>`


**Response**

```json
{
  "error": false,
  "message": "Loyalty programs retrieved successfully",
  "data": [
    {
      "program_id": "program-123abc",
      "program_name": "Free 1-Hour Booking",
      "description": "Redeem your points for a free 1-hour booking on any field",
      "points_required": 100,
      "reward_type": "discount",
      "reward_value": "100%",
      "is_active": true,
      "start_date": "2023-01-01",
      "end_date": "2023-12-31"
    }
  ]
}
```

### Redeem Points

**Endpoint**

```plaintext
/loyalty/redeem
```

**Method**

```plaintext
POST
```

**Headers**

- `Authorization: Bearer <token>`
- `Content-Type: application/json`


**Request Body**

- `program_id` as string
- `points_used` as integer


**Response**

```json
{
  "error": false,
  "message": "Points redeemed successfully",
  "data": {
    "redemption_id": "redemption-123abc",
    "program_name": "Free 1-Hour Booking",
    "points_used": 100,
    "status": "completed",
    "redemption_code": "FREE1HR-123ABC"
  }
}
```

### Get Redemption History

**Endpoint**

```plaintext
/loyalty/redemptions
```

**Method**

```plaintext
GET
```

**Headers**

- `Authorization: Bearer <token>`


**Response**

```json
{
  "error": false,
  "message": "Redemption history retrieved successfully",
  "data": [
    {
      "redemption_id": "redemption-123abc",
      "program_name": "Free 1-Hour Booking",
      "points_used": 100,
      "redemption_date": "2023-06-15T10:30:00.000Z",
      "status": "completed",
      "redemption_code": "FREE1HR-123ABC",
      "notes": "Valid until July 15, 2023"
    }
  ]
}
```

### Create Loyalty Program (Admin Only)

**Endpoint**

```plaintext
/admin/loyalty/programs
```

**Method**

```plaintext
POST
```

**Headers**

- `Authorization: Bearer <token>`
- `Content-Type: application/json`


**Request Body**

- `program_name` as string
- `description` as string
- `points_required` as integer
- `reward_type` as string (discount, free_booking, merchandise)
- `reward_value` as string
- `start_date` as string (YYYY-MM-DD format)
- `end_date` as string (YYYY-MM-DD format), optional


**Response**

```json
{
  "error": false,
  "message": "Loyalty program created successfully",
  "data": {
    "program_id": "program-123abc"
  }
}
```

### Update Loyalty Program (Admin Only)

**Endpoint**

```plaintext
/admin/loyalty/programs/:program_id
```

**Method**

```plaintext
PUT
```

**Headers**

- `Authorization: Bearer <token>`
- `Content-Type: application/json`


**Request Body**

- `program_name` as string, optional
- `description` as string, optional
- `points_required` as integer, optional
- `reward_type` as string, optional
- `reward_value` as string, optional
- `is_active` as boolean, optional
- `start_date` as string (YYYY-MM-DD format), optional
- `end_date` as string (YYYY-MM-DD format), optional


**Response**

```json
{
  "error": false,
  "message": "Loyalty program updated successfully"
}
```

### Delete Loyalty Program (Admin Only)

**Endpoint**

```plaintext
/admin/loyalty/programs/:program_id
```

**Method**

```plaintext
DELETE
```

**Headers**

- `Authorization: Bearer <token>`


**Response**

```json
{
  "error": false,
  "message": "Loyalty program deleted successfully"
}
```

# Checkpoint - 4` - Loyalty, Poin Redemption
## Admin Management (Super Admin Only)

### Create Admin Account

**Endpoint**

```plaintext
/super-admin/admins
```

**Method**

```plaintext
POST
```

**Headers**

- `Authorization: Bearer <token>`
- `Content-Type: application/json`


**Request Body**

- `username` as string, must be unique
- `email` as string, must be unique
- `password` as string, must be at least 8 characters
- `full_name` as string
- `phone_number` as string


**Response**

```json
{
  "error": false,
  "message": "Admin account created successfully",
  "data": {
    "user_id": "user-456def",
    "username": "admin1"
  }
}
```

### Get All Admins

**Endpoint**

```plaintext
/super-admin/admins
```

**Method**

```plaintext
GET
```

**Headers**

- `Authorization: Bearer <token>`


**Response**

```json
{
  "error": false,
  "message": "Admin accounts retrieved successfully",
  "data": [
    {
      "user_id": "user-456def",
      "username": "admin1",
      "email": "admin1@example.com",
      "full_name": "Admin One",
      "is_active": true,
      "created_at": "2023-01-01T00:00:00.000Z"
    }
  ]
}
```

### Update Admin Account

**Endpoint**

```plaintext
/super-admin/admins/:user_id
```

**Method**

```plaintext
PUT
```

**Headers**

- `Authorization: Bearer <token>`
- `Content-Type: application/json`


**Request Body**

- `full_name` as string, optional
- `phone_number` as string, optional
- `is_active` as boolean, optional
- `password` as string, optional, must be at least 8 characters


**Response**

```json
{
  "error": false,
  "message": "Admin account updated successfully"
}
```

### Delete Admin Account

**Endpoint**

```plaintext
/super-admin/admins/:user_id
```

**Method**

```plaintext
DELETE
```

**Headers**

- `Authorization: Bearer <token>`


**Response**

```json
{
  "error": false,
  "message": "Admin account deleted successfully"
}
```

## Reports (Admin & Super Admin)

### Get Booking Reports 

**Endpoint**

```plaintext
/admin/reports/bookings
```
```plaintext
/super-admin/reports/bookings
```

**Method**

```plaintext
GET
```

**Headers**

- `Authorization: Bearer <token>`


**Parameters**

- `from_date` as string (YYYY-MM-DD format)
- `to_date` as string (YYYY-MM-DD format)
- `field_id` as string, optional
- `format` as string, optional (json, csv, pdf, default: json)


**Response**

```json
{
  "error": false,
  "message": "Booking report generated successfully",
  "data": {
    "period": {
      "from_date": "2023-06-01",
      "to_date": "2023-06-30"
    },
    "total_bookings": 45,
    "completed_bookings": 40,
    "cancelled_bookings": 5,
    "total_revenue": 6750000,
    "fields_usage": [
      {
        "field_id": "field-123abc",
        "field_name": "Field A",
        "bookings_count": 25,
        "total_hours": 50,
        "revenue": 3750000
      }
    ],
    "daily_bookings": [
      {
        "date": "2023-06-01",
        "bookings_count": 3,
        "revenue": 450000
      }
    ]
  }
}
```

### Get Revenue Reports 

**Endpoint**

```plaintext
/admin/reports/revenue
```
```plaintext
/super-admin/reports/revenue
```

**Method**

```plaintext
GET
```

**Headers**

- `Authorization: Bearer <token>`


**Parameters**

- `from_date` as string (YYYY-MM-DD format)
- `to_date` as string (YYYY-MM-DD format)
- `group_by` as string, optional (day, week, month, default: day)
- `format` as string, optional (json, csv, pdf, default: json)


**Response**

```json
{
  "error": false,
  "message": "Revenue report generated successfully",
  "data": {
    "period": {
      "from_date": "2023-06-01",
      "to_date": "2023-06-30"
    },
    "total_revenue": 6750000,
    "payment_methods": [
      {
        "method_name": "bank_transfer",
        "count": 30,
        "amount": 4500000
      },
      {
        "method_name": "credit_card",
        "count": 15,
        "amount": 2250000
      }
    ],
    "revenue_by_period": [
      {
        "period": "2023-06-01",
        "revenue": 450000
      }
    ]
  }
}
```

### Get Loyalty Program Reports 

**Endpoint**

```plaintext
/admin/reports/loyalty
```
```plaintext
/super-admin/reports/loyalty
```

**Method**

```plaintext
GET
```

**Headers**

- `Authorization: Bearer <token>`


**Parameters**

- `from_date` as string (YYYY-MM-DD format)
- `to_date` as string (YYYY-MM-DD format)
- `format` as string, optional (json, csv, pdf, default: json)


**Response**

```json
{
  "error": false,
  "message": "Loyalty program report generated successfully",
  "data": {
    "period": {
      "from_date": "2023-06-01",
      "to_date": "2023-06-30"
    },
    "total_points_issued": 4500,
    "total_points_redeemed": 1200,
    "active_users": 35,
    "programs_usage": [
      {
        "program_id": "program-123abc",
        "program_name": "Free 1-Hour Booking",
        "redemptions_count": 12,
        "points_used": 1200
      }
    ],
    "top_users": [
      {
        "user_id": "user-123abc",
        "full_name": "John Doe",
        "points_earned": 150,
        "points_redeemed": 100
      }
    ]
  }
}
```

### Get System Statistics (Super Admin Only)

**Endpoint**

```plaintext
/super-admin/statistics
```

**Method**

```plaintext
GET
```

**Headers**

- `Authorization: Bearer <token>`


**Parameters**

- `period` as string, optional (daily, weekly, monthly, yearly, default: monthly)


**Response**

```json
{
  "error": false,
  "message": "System statistics retrieved successfully",
  "data": {
    "users": {
      "total": 500,
      "active": 450,
      "new_this_period": 25
    },
    "bookings": {
      "total": 1200,
      "completed": 1100,
      "cancelled": 100,
      "this_period": 150
    },
    "revenue": {
      "total": 180000000,
      "this_period": 22500000,
      "growth_percentage": 5.2
    },
    "fields": {
      "total": 8,
      "active": 8,
      "most_booked": {
        "field_id": "field-123abc",
        "field_name": "Field A",
        "bookings_count": 250
      }
    },
    "loyalty": {
      "total_points_issued": 45000,
      "total_points_redeemed": 12000,
      "most_popular_program": {
        "program_id": "program-123abc",
        "program_name": "Free 1-Hour Booking",
        "redemptions_count": 120
      }
    }
  }
}
```

## Notifications

### Subscribe to Push Notifications

**Endpoint**

```plaintext
/notifications/subscribe
```

**Method**

```plaintext
POST
```

**Headers**

- `Authorization: Bearer <token>`
- `Content-Type: application/json`


**Request Body**

- `endpoint` as string
- `keys` as object

- `p256dh` as string
- `auth` as string





**Response**

```json
{
  "error": false,
  "message": "Successfully subscribed to push notifications",
  "data": {
    "subscription_id": "sub-123abc"
  }
}
```

### Unsubscribe from Push Notifications

**Endpoint**

```plaintext
/notifications/unsubscribe
```

**Method**

```plaintext
DELETE
```

**Headers**

- `Authorization: Bearer <token>`
- `Content-Type: application/json`


**Request Body**

- `endpoint` as string


**Response**

```json
{
  "error": false,
  "message": "Successfully unsubscribed from push notifications"
}
```

### Get User Notifications

**Endpoint**

```plaintext
/notifications
```

**Method**

```plaintext
GET
```

**Headers**

- `Authorization: Bearer <token>`


**Parameters**

- `page` as integer, optional (default: 1)
- `limit` as integer, optional (default: 10)
- `read` as boolean, optional (filter by read status)


**Response**

```json
{
  "error": false,
  "message": "Notifications retrieved successfully",
  "data": {
    "notifications": [
      {
        "notification_id": "notif-123abc",
        "title": "Booking Confirmed",
        "message": "Your booking for Field A on June 15, 2023 has been confirmed",
        "type": "booking",
        "reference_id": "booking-123abc",
        "is_read": false,
        "created_at": "2023-06-10T12:30:00.000Z"
      }
    ],
    "pagination": {
      "total_items": 15,
      "total_pages": 2,
      "current_page": 1,
      "per_page": 10
    }
  }
}
```

### Mark Notification as Read

**Endpoint**

```plaintext
/notifications/:notification_id/read
```

**Method**

```plaintext
PUT
```

**Headers**

- `Authorization: Bearer <token>`


**Response**

```json
{
  "error": false,
  "message": "Notification marked as read"
}
```

### Send Notification (Admin Only)

**Endpoint**

```plaintext
/admin/notifications
```

**Method**

```plaintext
POST
```

**Headers**

- `Authorization: Bearer <token>`
- `Content-Type: application/json`


**Request Body**

- `user_id` as string, optional (if null, send to all users)
- `title` as string
- `message` as string
- `type` as string (system, promotion, booking)
- `reference_id` as string, optional


**Response**

```json
{
  "error": false,
  "message": "Notification sent successfully",
  "data": {
    "recipients_count": 1
  }
}
```

## Error Responses

### Validation Error

```json
{
  "error": true,
  "message": "Validation error",
  "errors": [
    {
      "field": "email",
      "message": "Email is not valid"
    }
  ]
}
```

### Authentication Error

```json
{
  "error": true,
  "message": "Authentication failed",
  "code": "AUTH_ERROR"
}
```

### Authorization Error

```json
{
  "error": true,
  "message": "You are not authorized to access this resource",
  "code": "FORBIDDEN"
}
```

### Resource Not Found

```json
{
  "error": true,
  "message": "Resource not found",
  "code": "NOT_FOUND"
}
```

### Server Error

```json
{
  "error": true,
  "message": "Internal server error",
  "code": "SERVER_ERROR"
}
```

## Web Push Notification

### VAPID Public Key

```plaintext
BLJozWWVVS7-QWMPQqZiVsVQjGsfish5eSdYLx_E4WypPRn9o7jJZ-VaUJzSLsj0_uxruQHQBvYGKF1FG5yW5Ks
```

### Notification JSON Schema

```json
{
  "title": "Booking Confirmation",
  "options": {
    "body": "Your booking for Field A on June 15, 2023 has been confirmed",
    "icon": "https://balls.com/images/logo.png",
    "data": {
      "type": "booking",
      "booking_id": "booking-123abc"
    }
  }
}
```

## Rate Limiting

The API implements rate limiting to prevent abuse. The limits are:

- 100 requests per minute for authenticated users
- 30 requests per minute for unauthenticated users


When rate limit is exceeded, the API will respond with HTTP status code 429 (Too Many Requests).

## Versioning

The current API version is v1. The version is included in the Endpoint path.

## Pagination

Most list endpoints support pagination with the following parameters:

- `page`: Page number (starting from 1)
- `limit`: Number of items per page


The response includes pagination information in the `pagination` object.
